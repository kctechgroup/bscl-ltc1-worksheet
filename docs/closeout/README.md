# You're done! {#top}

![](https://media.giphy.com/media/11sBLVxNs7v6WA/giphy.gif)

Hopefully you've enjoyed learning a bit about programming with Python and Minecraft.  Feel free to experiment some with your code and try new things!  There is much more to learn, but one of the great things about the Python language in particular is how much you can do so quickly from the start.  It is a popular language amongst disciplines outside of just computer programming.  Data scientists and engineers of all disciplines leverage Python everyday for a wide variety of program solving initiatives.

{% collapse title='Show me the final version of the code!' %}
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

# Turn a block (via a block event position) into water
def turn_block_into_water(block_pos):
    x, y, z = pos
    mc.setBlock(hit_x, hit_y, hit_z, water)

# Begin Main Loop
while True:
    # Get the current tile position of the player
    x, y, z = mc.player.getTilePos()

    # Plant Flowers and Capture Player Movement
    player_moved = plant_flowers(x, y, z, last_x, last_y, last_z)

    # Gather Block Events
    block_events = mc.events.pollBlockHits()
    for block_event in block_events:
        turn_block_into_water(block_event.pos)

    # Sync up the last and current positions
    last_x, last_y, last_z = x, y, z
```
{% endcollapse %}

At this point, you've learned the following:

- Working with Data Types such as `int`, `float`, `boolean`, and `string`
- How to use _Variables_ to store data
- How to leverage _Expressions_ to compute results
- How to use _Loops_ to run repeated sections of code
- How to use _Functions_ to collect code into reusable sections

Take a look at the [Resources](/resources.md) section for more information on how to extend what you've done in this class as well as some resources for continued learning in programming and Python!

-- Happy Coding! 😎