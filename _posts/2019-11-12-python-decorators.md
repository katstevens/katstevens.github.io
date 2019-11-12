---
layout: post
author: Kat
title: Python decorators
tags: [Python]
---
Let’s talk about Python decorators!

If you’ve developed web apps using [Flask](https://flask.palletsprojects.com/en/1.1.x/patterns/viewdecorators/) or [Django](https://docs.djangoproject.com/en/2.2/topics/http/decorators/), you’re probably familiar with the handy `@` functions above your views, enforcing certain rules like making sure a user is logged in before rendering the view, or checking whether the HTTP method being used is allowed.

## A Flask(ish) example

The documentation links above give specific examples of decorators for those frameworks. Let’s look at an example view similar to the one from the Flask docs:

```
@app.route('/secret_page')
@login_required
def secret_page():
    return "OK", 200
```

There are two decorators on the `secret_page` view: 
- `@app.route` tells Flask which URL the view is associated with
- `@login_required` checks whether a user is logged in before proceeding.

`@app.route` is actually just another function. If we weren’t using decorators, we could register the route with a long-winded function like this:

```
def secret_page():
    return "OK", 200 

def register_route(url, view_func, **):
    # Let’s pretend Flask stores URLs as a big list of tuples!
    my_big_list_of_global_app_urls.append(
        (url, view_func, **)
    )

register_route('/secret_page', secret_page)
```

Behold, the magic of functional programming! We are passing the entire `secret_page` function to `register_route` as the `view_func` argument. It’s functions all the way down, hashtag Inception etc. 

(The  `**` refers to any arguments that `secret_page` might take.)

`@login_required` would look a little different when written out as a function:

```
def secret_page():
    return "OK", 200 

def login_required(view_func, **):
    # Again, this is a huge simplification of what happens
    if session.user_is_logged_in:
        return view_func(**)
    return “You need to log in to view this page”, 403

response, status_code = login_required(secret_page)
```

When we call `login_required`, it’s actually returning the result of `view_func` (assuming we’re logged in, of course). `login_required` is acting as an outer protective shell, wrapping `secret_page` and bailing out with a 403 if it fails the login check. 

The `@app.route` decorator doesn’t work as a wrapper in quite the same way as `@login_required` - Flask calls it when the app is initialised, to build its big list of available routes.

This is why `@app.route` is always placed above other custom decorators on a view. What would happen if the decorators were the other way around?

## Ordering decorators

Let’s flip the ordering:

```
@login_required
@app.route('/secret_page')
def secret_page():
    return "OK", 200
``` 

Flask will still discover the view and add it to its big list of routes. But it won’t be registered as a `login_required` route, because decorators are evaluated ‘from the inside out’ (the closest decorator to the `def` gets called first).  

So `@app.route` gets called first, and adds the URL to the big Flask route list. But the `view_func` that gets passed to it doesn’t know anything about `login_required` yet! So when Flask later evaluates the route and sends traffic to `/secret_page`, that route is associated with the bare, unprotected view. Yikes.

## Defining a decorator

Actual decorators don’t look like the ‘flat’ functions I’ve written out above. We need to declare something like this:

```
def login_required(view_func):
    @wraps
    def my_inner_func(*args, **kwargs):
        # Here’s where we do our custom stuff
        if session.user_is_logged_in:
            return view_func(*args, **kwargs)
        return “You need to log in to view this page”, 403
    return my_inner_func
```

Our outermost layer is `login_required`: this is the name we’ll use to decorate our view functions. It takes  `view_func` as an argument and returns another function, `my_inner_func`. The key thing to note is that it is not returning the **result** of `my_inner_func`;, it’s returning the **definition** of that function.

`my_inner_func` is where any custom logic or checks will happen. It has access to `view_func` from the outer scope, and this example either returns the **result** of `view_func`, or an error.

So having defined `@login_required` above, we know it returns a function definition. When we use it to decorate the `secret_page` view, we are wrapping that view definition with our decorator definition, without actually evaluating anything yet (unlike our 'flat' functions above). Hurray!

A quick note about `@wraps`: it is a sanity-preserving, built-in helper (and yet another decorator!) that allows the innermost function (your original`secret_page` view) to bubble up seamlessly through all the layers without odd side effects. The [python docs](https://docs.python.org/3/library/functools.html#functools.wraps) have more info on how this works.

## Top tips

Decorators can all be a bit mind boggling, especially when you are debugging. My top tips for dealing with them:

- Remember to work from the ‘inside out’
- Remember that returning a function **definition** is not the same as returning a function **result**
- Think very carefully before writing your own decorator from scratch, it is almost never worth bothering with on small projects
- If you do decide to write your own, pay careful attention to what gets evaluated when. Read up on [pickling](https://www.pythoncentral.io/how-to-pickle-unpickle-tutorial/)!
