---
layout: post
author: Kat
title: My Ideal Function
---
Us Python programmers are quite lucky, I think. We're allowed to do pretty much whatever we like with our functions, as long as there's a `def` at the top. But with great power comes great responsibility! I've seen some pretty rotten functions in my time, including ones I have written myself. What does my ideal function look like, then? Get ready for some Opinions!

## 1. It does a thing

'A' being the important word here - a function that does more than one thing is probably a candidate for splitting into two functions. 

This is often a sticking point when writing web applications, where a view function ends up doing all sorts of things in one request. A view for `display_user_dashboard()` could have all sorts of database queries and logic going on. That's actually fine by me, as long as that view _broadly_ does one thing (displaying the dashboard). We can't all be [RESTful](https://en.wikipedia.org/wiki/Representational_state_transfer) all the time but keeping the scope clear helps everyone know what to expect. Which leads me to...

## 2. The name reflects that thing

Naming is hard, we all know that. My ideal function includes a verb in its name, that relates to what it's doing. For example, `convert_this_to_that()`, `validate_json_for_bad_stuff()` or `send_invite_email_to_new_user()`.

For that last one, I could have written just plain old `send_email()`, but adding in what sort of email and who it's being sent to will help me debug it more quickly when my email server goes up the wazoo. It may lead to less [DRYness](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) in the long run, but I will take verbosity over confusion any day.

Reiterating point 1, if a function name includes the word `and`, it's a candidate for either renaming, splitting in two, or ditching entirely. It's hard to design well-structured functions like this in the real world of legacy code and third-party depedencies, but remember this is my idealised dream scenario and I can do what I like. 

(Unlike `and`, I think the word `or` is fine to include in a function name, for example Flask's   `get_object_or_404()`.) 

## 3. The thing is non-trivial

There is no point in writing a function that adds two numbers together. I'm also not keen on functions whose sole purpose is to wrap another function (perhaps because the arguments are in the wrong order, or the name refers to something confusing). That implies to me that the target function either needs renaming/rewriting, or shouldn't be being used in the first place! It also adds an extra layer that you have to maintain and debug. Ugh. 

The difficulty here is striking a balance between a function that does just one thing, and ensuring that thing is important enough. 

## 4. The inputs and outputs are clear

I hope this goes without saying. Python 3.5+ supports [type annotations](https://docs.python.org/3/library/typing.html), and once you get over how weird it looks, it's a neat way of self-documenting a function.

Here's a quick example where the function takes a string, and returns `None`:
```
def send_invite_email_to_new_user(email_address: str) -> None:
    validate_email_or_400(email_address)    
    send_email(email_address, template='new_user_invite')
```

I could delve deeper into type annotations but this blog post is long enough already. If you don't want to introduce type annotations, a simple docstring will do the job nicely.  

## 5. It has sufficient` test coverage

And by this I mean at least two tests! If your function doesn't need two or more tests, it's probably not important enough to be a function (see point 3). Expect more opinions on testing in future blogs!

I'll have to stop there for now, as the cat has decided to 'help' by sitting on the laptop.
