---
layout: post
author: Kat
title: Recursive Triangles
tags: [Python]
---
A _kata_ is another name for a programming exercise. Usually they're designed to help highlight or hone a particular programming technique such as pairing or tests. 

[Here's a kata on recursion](https://www.codewars.com/kata/insane-coloured-triangles/train/python): creating a downward-pointing triangle of red, blue or green pieces, where the colour is determined by the two 'parent' pieces on the row above it. If both parents are the same colour, the child colour beneath is also that colour. If the two parents are different colours (say red and green), the child colour is the remaining colour (blue).

Our job is to write a function that, given the top row, will output the single-piece bottom row. It's simple enough, but I'll talk through how I approached it*:

First, let's write a test to make sure our colours are being picked correctly:

```
import pytest
from triangles import pick_colour_below


@pytest.mark.parametrize(
    'parents, child',
    [
        # Test same colour
        (('R', 'R'), 'R'),
        (('G', 'G'), 'G'),
        (('B', 'B'), 'B'),
        # Test different colours
        (('G', 'R'), 'B'),
        (('R', 'B'), 'G'),
        (('G', 'B'), 'R'),
        # And test left-to-right doesn't matter
        (('R', 'G'), 'B'),
        (('B', 'R'), 'G'),
        (('B', 'G'), 'R'),
    ]
)
def test_pick_colour_below(parents, child):
    assert pick_colour_below(parents[0], parents[1]) == child
```

I've used `pytest`'s `parametrize` decorator to feed in a bunch of scenarios for the same test.

The function under test, `pick_colour_below` looks like this:

```
def pick_colour_below(left_parent, right_parent):
    if left_parent == right_parent:
        return left_parent  # doesn't matter which one
    (leftover,) = {'R', 'B', 'G'} - {left_parent, right_parent}
    return leftover
```

Now we can add a test for the simple case, where our top row is 1 piece long. We know that should
return itself:

```
@pytest.mark.parametrize('top_row', ['R', 'G', 'B'])
def test_single_row_triangle_produces_same_colour(top_row):
    assert generate_triangle(top_row) == top_row
```

Now we can create our main function:

```
def generate_triangle(top_row):
    if len(top_row) == 1:
        return top_row
    else:
        return "Patience, grasshopper"

```

Now we need to think about the case where the top row is longer than 1 piece. Thankfully the kata gives us some expected test data to use:

```
@pytest.mark.parametrize(
    'top_row, expected_bottom_row',
    [
        ('GB', 'R'),
        ('RRR', 'R'),
        ('RGBG', 'B'),
        ('RBRGBRB', 'G'),
        ('RBRGBRBGGRRRBGBBBGG', 'G'),
    ]
)
def test_multi_row_triangle(top_row, expected_bottom_row):
    assert generate_triangle(top_row) == expected_bottom_row
```

These tests currently fail, as none of 'R', 'B' or 'G' equal 'Patience, grasshopper'. 

We need another helper function, that will do a bit more heavy lifting and build a longer row for us:

```
def get_next_row(this_row):
    next_row = ''
    left_parent_position = 0
    while left_parent_position < (len(this_row) - 1):
        next_row += pick_colour_below(
            this_row[left_parent_position],
            this_row[left_parent_position + 1]
        )
        left_parent_position += 1
    return next_row
```

The function works its way along the current row, using `pick_colour_below` to generate the `next_row` pieces, until it reaches the penultimate piece. 

Let's write a test to go with it:

```
@pytest.mark.parametrize(
    'this_row, next_row',
    [
        ('RB', 'G'),
        ('GG', 'G'),
        ('GGB', 'GR'),
        ('GGBR', 'GRG'),
    ]
)
def test_get_next_row_is_correct(this_row, next_row):
    assert get_next_row(this_row) == next_row
```

We're ready to stick `get_next_row` into our main `generate_triangle` function. It recursively calls itself it until the final 1-piece row.

```
def generate_triangle(top_row):
    if len(top_row) == 1:
        return top_row
    return generate_triangle(get_next_row(top_row))
```

And that's it! The tests pass, so we can be confident that the functions are doing the right thing. Here's the whole code:

```
def pick_colour_below(left_parent, right_parent):
    if left_parent == right_parent:
        return left_parent  # gotta pick one, I guess
    (leftover,) = {'R', 'B', 'G'} - {left_parent, right_parent}
    return leftover


def get_next_row(this_row):
    next_row = ''
    left_parent_position = 0
    while left_parent_position < (len(this_row) - 1):
        next_row += pick_colour_below(
            this_row[left_parent_position],
            this_row[left_parent_position + 1]
        )
        left_parent_position += 1
    return next_row


def generate_triangle(top_row):
    if len(top_row) == 1:
        return top_row
    return generate_triangle(get_next_row(top_row))
```

By splitting the problem into these three parts, I've kept the colour-picking logic, the row generation and the recursion separate from each other, so if there was a problem with one of those parts, it would be easier to unpick.

This solution is limited by the recursion settings on my local installation of Python. If I try a scenario with a very long top row, I get this:

```
def test_multi_row_triangle():
    assert generate_triangle('R'*1000) == 'R'

$ pytest
E       RecursionError: maximum recursion depth exceeded in comparison
```

The max length `top_row` my machine can handle is 940 characters, which is fine for this kata. If we wanted to handle a longer string, we'd have to use a data structure somewhere (perhaps storing the result of smaller triangles). But we're out of time, so that'll have to be an 'exercise for the reader' :)

*I actually misread the problem at first and thought we needed to work from the centre of each row. All that meant was that `get_next_row` was a bit more complex - the other two functions were unchanged.
