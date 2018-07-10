# Using Functions {#top}

Variables allowed us to hold onto values.  Functions allow us to hold onto a set of code instructions.  We can then do work with functions without knowing all of the steps involved.  

{% include "./instruction-steps.html" %}

## Breaking out our Flowers {#flowers} <span class="navigate-top"><a href="#top" title="Take me to the top of page"><i class="fa fa-chevron-circle-up" aria-hidden="true"></i></a></span>

Let's review where our programs sits right now:

```python
from mcpi.minecraft import Minecraft
mc = Minecraft.create()

# Block Definitions
water = 8
lava = 10
air = 0
yellow_flower = 37
tnt = 46

# Get the initial tile position of the player
last_x, last_y, last_z = mc.player.getTilePos()

while True:
    # Get the current tile position of the player
    x, y, z = mc.player.getTilePos()

    # Capture if the player has moved
    player_moved = last_x != x or last_y != y or last_z != z

    # Output when the player has moved
    if player_moved:
        print("Player has moved to a new tile")
        mc.setBlock(last_x, last_y, last_z, yellow_flower)

    # Gather Block Events
    block_events = mc.events.pollBlockHits()
    for block_event in block_events:
        print("Hit a block!")

        # Retrieve hit position from the block event
        hit_x, hit_y, hit_z = block_event.pos
        mc.setBlock(hit_x, hit_y, hit_z, water)

    # Sync up the last and current positions
    last_x, last_y, last_z = x, y, z
```

We've got a pretty long program now.  Using functions, we can better organize our program.  Let's start by creating a function that will perform the following steps:

- Accept the current and last position variables as arguments
- Determine if the player has moved to a new tile
- Drop a yellow flower on the last position if the player has moved
- Return a boolean of `True` if player has moved or `False` if not

{% hint style='tip' %}
Another common practice in programming is taking requirements like the ones listed above and writing code to make those requirements a reality!
{% endhint %}

We'll place our function above our main `while` loop so that it is ready in by our program and available to call when we need it.  Then, we'll call the function in place of what we removed from our `while` loop.

{% collapse title='Show me the Plant Flowers Function!' %}
```python
def plant_flowers(curr_x, curr_y, curr_z, last_x, last_y, last_z):
    # Capture if the player has moved
    player_moved = last_x != curr_x or last_y != curr_y or last_z != curr_z

    # Output when the player has moved
    if player_moved:
        print("Player has moved to a new tile")
        mc.setBlock(last_x, last_y, last_z, yellow_flower)
    
    return player_moved
```
{% endcollapse %}

{% hint style='working' %}
Can you think of how you might change your function so that you could use it to plant different types of blocks depending on your you called it?
{% endhint %}

Now we can use the function call within our `while` loop and really clean things up:

```python
player_moved = plant_flowers(x, y, z, last_x, last_y, last_z)
```

{% collapse title='Show me the whole code!' %}
```python
from mcpi.minecraft import Minecraft
mc = Minecraft.create()

# Block Definitions
water = 8
lava = 10
air = 0
yellow_flower = 37
tnt = 46

# Get the initial tile position of the player
last_x, last_y, last_z = mc.player.getTilePos()

# Flower Planting Function
def plant_flowers(curr_x, curr_y, curr_z, last_x, last_y, last_z):
    # Capture if the player has moved
    player_moved = last_x != curr_x or last_y != curr_y or last_z != curr_z

    # Output when the player has moved
    if player_moved:
        print("Player has moved to a new tile")
        mc.setBlock(last_x, last_y, last_z, yellow_flower)
    
    return player_moved

# Begin Main Loop
while True:
    # Get the current tile position of the player
    x, y, z = mc.player.getTilePos()

    # Plant Flowers and Capture Player Movement
    player_moved = plant_flowers(x, y, z, last_x, last_y, last_z)

    # Gather Block Events
    block_events = mc.events.pollBlockHits()
    for block_event in block_events:
        print("Hit a block!")

        # Retrieve hit position from the block event
        hit_x, hit_y, hit_z = block_event.pos
        mc.setBlock(hit_x, hit_y, hit_z, water)

    # Sync up the last and current positions
    last_x, last_y, last_z = x, y, z
```
{% endcollapse %}

## Breaking out our Water {#water} <span class="navigate-top"><a href="#top" title="Take me to the top of page"><i class="fa fa-chevron-circle-up" aria-hidden="true"></i></a></span>

Let's do the same with our water-creation code in our for loop as our final exercise.  Write your function to behave as described below:

- Accept a block position (that comes from a block event) as the only argument
- Extract the coordinates from the position into helper variables
- Use the `setBlock` function to turn the block into a water block.

Have a go at writing this one on your own, but know that there will be some code below to help you if you get stuck.  

{% collapse title='Show me the Water Creation Function!' %}
```python
# Turn a block (via a block event position) into water
def turn_block_into_water(block_pos):
    x, y, z = block_pos
    mc.setBlock(x, y, z, water)
```
{% endcollapse %}

Finally, replace the code in your `while` loop with a call to your new function.  Notice how much shorter our main loop is now.  It is much easier to read!

{% hint style='info' %}
Did you know that we've been using functions already prior to this section?  The `setBlock()` and `getTilePos()` are both functions!  So is `print()`!  You can now see the benefit of functions--they allow someone to use code that has been written without knowing each and every step that makes up that function.  Such is the joy of code reuse!
{% endhint %}

This concludes _Part II_ of the worksheet.  You can review the final codebase in the [Closeout](/closeout/README.md) section.