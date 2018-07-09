# Loops and Conditionals {#top}

Now that we've got some foundation out of the way, let's start turning up the dial!  It is time to apply some control structures such as `if` statements and `while` loops.

{% include "./instruction-steps.html" %}

## Setting up our Program Loop {#mainloop} <span class="navigate-top"><a href="#top" title="Take me to the top of page"><i class="fa fa-chevron-circle-up" aria-hidden="true"></i></a></span>

Some programs accept some input and produce some output.  When run, these programs do their job and then exit.  Other programs run on the computer and are constantly processing.  These types of programs require what we call a main loop.  We'll put a simple one in place with a very simple `while` loop.  

Add the while loop before the current player position gathering:

```python
while True:
    x, y, z = mc.player.getTilePos()
```

{% hint style='tip' %}
Indentation is very important in Python.  Note that anything that is indented within a control structure is what is considered within the "scope" of that structure.  In other words, everything that is indented will be _in_ our `while` loop.
{% endhint %}

## Fun with Expressions {#expressions} <span class="navigate-top"><a href="#top" title="Take me to the top of page"><i class="fa fa-chevron-circle-up" aria-hidden="true"></i></a></span>

Let's enhance this a bit further by using some expressions to help us determine if the player has moved to a new tile position.  We'll store the result of this in a special variable we can use to do something when the player moves from one tile to another.

Add the new lines of code below to your project:

```python
from mcpi.minecraft import Minecraft
mc = Minecraft.create()

# Block Definitions
water = 8
lava = 10
air = 0
yellow_flower = 37

# Get the initial tile position of the player
last_x, last_y, last_z = mc.player.getTilePos()

while True:
    # Get the current tile position of the player
    x, y, z = mc.player.getTilePos()

    # Capture if the player has moved
    player_moved = last_x != x or last_y != y or last_z != z

    # Sync up the last and current positions
    last_x, last_y, last_z = x, y, z

    # Output when the player has moved
    if player_moved:
        print("Player has moved to a new tile")
```

Okay, we've got a bit to unpack.  Let's review some of what we've put in above:

- Prior to our loop we "initialize" our variables to track the last known position of the player.  We'll use these to compare to the current position.
- The `player_moved` variable is assigned the result of an expression that will be `True` if either `x`, `y`, or `z` doesn't match the last known positions.
- After we set our `player_moved` we make the last known values equal to the current values.  If the player doesn't move, then they'll continue to be the same.

Go ahead and _Run_ this code and then move your player around.  You'll see output in the "Shell" area when you move to a new tile.

{% hint style='tip' %}
Since we now have a loop that never ends, you'll need to use the `Stop` button to interrupt your code.  It will print some scary stuff in the _Shell_ section, but that is normal, don't worry. 😀
{% endhint %}