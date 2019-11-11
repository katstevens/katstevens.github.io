---
layout: post
author: Kat
title: When to use a class
tags: [Python]
---
“_When should you use a class in a script, and when should you just bash it out?_”

This excellently-phrased question comes from Jonathan, who kindly prompted me when I was stuck for a topic today.

Let’s imagine a scenario. I am ploughing through a big CSV file and I need to gather some stats on the data. It’s a one-off script, and if it takes me longer to write than googling the spreadsheet formula to do the same job, I will be cross. 

I am going to start by writing something like this:

```
if __name__ == ‘__main__’:  # blatantly had to look up the correct underscore syntax here
    # Load the file
    # Initialise my stat-collecting data structure
    # For row in file do a thing
    # Output the results    
```

Then I’ll iterate with:

```
def load_file(filename):
    # some csv gubbins here

def use_pokemon(row):
    if ‘squirtle’ in row[‘name’]:
        return 1  # My spreadsheet skills suck, OK?
    return 0

if __name__ == ‘__main__’:  
    rows = load_file(‘kanto_pokedex.csv’)
    running_total = 0
    for row in rows:
        running_total += use_pokemon(row)
    print(running_total)    
```

The helper functions are good enough for what I need here. I don’t want to overcomplicate things.

But what if `use_pokemon` is a more complex function?

```
def use_pokemon(row, health=100):
    annotate_row_with_battle_stats(row)
    health = battle(row)
    if health < 10:
        return swap_out_of_battle(
            get_weaknesses(row, ‘fire’), 
            get_strengths(row, ‘grass’)
        )        
    return victory(row)
```

There is a lot going on now with ‘row’ - what’s happening in those functions? Is the data changing at any point? How much control do we need over the state of ‘row’?

A class might be useful here to keep track of what’s happening:

```
class Pokemon:
    def __init__(self, row):
        self._type = row[‘type’]
        self._name = row[‘name’]
        self.in_ball = True
        self.in_battle = False
        self.health = 100
        if ‘weaknesses’ in row:
            self._weaknesses = [row[‘weaknesses’]]
        if ‘strengths’ in row:
            self._strengths = [row[‘strengths’]]

    def receive_critical_hit(self)
        self.health = self.health * 0.1

    def battle(self)        
        self.in_ball = False
        self.in_battle = True
        # etc, I can’t be bothered writing a full game here
```

And our script would look something more like this:

```
if __name__ == ‘__main__’:  
    rows = load_file(‘kanto_pokedex.csv’)
    running_total = 0
    for row in rows:
        pokemon = Pokemon(row)
        result = pokemon.battle()        
        running_total += 1 if result == ‘win’ else 0
```

Here the separation between my data and my logic is clearer. My immutable data from `row` is safely stored as protected attributes of the class instance. My methods use that shared data, and can update mutable attributes like `self.health`.

Warning signs that you don’t need a class:
- it’s stuffed full of methods that don’t use `self`
- the methods always have to be done in a certain order
- you’re having trouble naming the class as a noun (or its naming its methods as a verb)
- you could have done the calculation in Google Sheets by now

At the end of the day, classes describe a type of object. An instance is a concrete example of that  object type. If your script is a sequence of steps, that is a procedure, not a class. 
