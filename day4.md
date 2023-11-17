# Arctic Code Quest: Day 4
### @diffs true

```python
# game initialization
scene.set_background_image(assets.image("""winterBackground"""))
game.splash("Oh no!", "Santa lost his presents!")
game.splash("Collect all the presents", "before the time runs out!")
game.splash("Avoid the milk and cookies", "they take away time!")
tiles.set_current_tilemap(tilemap("""level"""))
info.start_countdown(30)

# player sprite
player_sprite = sprites.create(assets.image("""santaRight"""), SpriteKind.player)
tiles.place_on_tile(player_sprite, tiles.get_tile_location(0, 6))
controller.move_sprite(player_sprite, 100, 0)
scene.camera_follow_sprite(player_sprite)
player_sprite.ay = 500

# player button pressed events
def on_a_pressed():
    if player_sprite.is_hitting_tile(CollisionDirection.BOTTOM):
        player_sprite.vy = -200
controller.A.on_event(ControllerButtonEvent.PRESSED, on_a_pressed)

def on_right_pressed():
    player_sprite.set_image(assets.image("""santaRight"""))
controller.right.on_event(ControllerButtonEvent.PRESSED, on_right_pressed)

def on_left_pressed():
    player_sprite.set_image(assets.image("""santaLeft"""))
controller.left.on_event(ControllerButtonEvent.PRESSED, on_left_pressed)

# food sprites
for value in tiles.get_tiles_by_type(assets.tile("""foodSpawnTile""")):
    present_sprite = sprites.create(assets.image("""greenGift"""), SpriteKind.food)
    tiles.place_on_tile(present_sprite, value)
    tiles.set_tile_at(value, assets.tile("""transparency16"""))

# enemy sprites
for value2 in tiles.get_tiles_by_type(assets.tile("""enemySpawnTile""")):
    cookie_sprite = sprites.create(assets.image("""milkGlassCookie"""), SpriteKind.enemy)
    tiles.place_on_tile(cookie_sprite, value2)
    tiles.set_tile_at(value2, assets.tile("""transparency16"""))

# overlap events
def on_on_overlap(sprite2, otherSprite):
    sprites.destroy(otherSprite, effects.smiles, 500)
    music.play(music.melody_playable(music.magic_wand), music.PlaybackMode.UNTIL_DONE)
    if len(sprites.all_of_kind(SpriteKind.food)) == 0:
            game.game_over(True)
sprites.on_overlap(SpriteKind.player, SpriteKind.food, on_on_overlap)

def on_on_overlap2(sprite3, otherSprite2):
    sprites.destroy(otherSprite2, effects.disintegrate, 500)
    info.change_countdown_by(-5)
    music.play(music.melody_playable(music.zapped), music.PlaybackMode.UNTIL_DONE)
sprites.on_overlap(SpriteKind.player, SpriteKind.enemy, on_on_overlap2)

def on_overlap_tile(sprite, location):
    tiles.place_on_tile(sprite, tiles.get_tile_location(0, 0))
    music.play(music.melody_playable(music.big_crash), music.PlaybackMode.UNTIL_DONE)
scene.on_overlap_tile(SpriteKind.player, assets.tile("""snowPath13"""), on_overlap_tile)
```

## Arctic Code Quest: Python Edition - Day 4! @showdialog

Welcome to your next Python project code along! Today you will be creating a project using everything you have learned so far, plus 2D tilemaps, simple physics, and conditionals! 

Click ``||loops:Ok||`` to get started!

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

## Create a 2D Platformer Tilemap

Create a 2D Platformer tilemap, that is at least 40 tiles wide, for your Player sprite to navigate!

---

- :tree: Type ``||scene:tiles||``, a dot operator ``||.||``, and the ``||scene:set_current_tilemap||`` function. Pressing Tab will insert the ``||scene:(tilemap(""" """))||`` code into the function.
- :map: Click the map icon to the left of the line of code to design a tilemap that is at least **40** tiles wide and exactly **8** tiles in height using any of the available tiles. 
- :map: Add tiles along the bottom that will function as **ground** tiles for a sprite to walk along. Leave a few gaps between the ground tiles to create hazards in a future step. ![image](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/tilemap%202d%20basic.png?raw=true "tilemap 2d")
- :map: Create **platforms** for a sprite to jump up on at least 1 tile above the ground tiles. Add **layers of tiles** on top of the ground tiles to create obstacles to climb up. ![image](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/tilemap%202d%20platforms.png?raw=true "tilemap 2d platforms")
- :map: Use the Draw Walls tool to turn all of these tiles into **walls** so a sprite can stand on top of them. ![image](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/tilemap%202d%20walls.png?raw=true "tilemap 2d walls")

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

```python
tiles.set_current_tilemap(tilemap("""level"""))
```

## Add a background to the 2D Platformer Tilemap!

Use a background color or image to add a backdrop for your 2D Platformer tilemap.

- :tree: Use either ``||scene:scene.set_background_color||`` with a number parameter, 1-15, or ``||scene:scene.set_background_image||`` with a background image asset, to add a backdrop behind your 2D tilemap.

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

```python
# game initialization
scene.set_background_image(assets.image("""winterBackground"""))
tiles.set_current_tilemap(tilemap("""level"""))
```

## Create a Player sprite to move around the tilemap!

Add a Player sprite to the project to navigate the 2D tilemap!

---

- :paper plane: Add a Player sprite to the project. Select an image asset that is facing right.
- :tree: Position the Player sprite on top of the first ground tile farthest to the right using ``||scene:tiles.place_on_tile||``.
- :game controller: Add code to move the Player sprite around the tilemap.
- :tree: Add code to make the camera follow the sprite across the tilemap. 

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

```python
# game initialization
scene.set_background_image(assets.image("""winterBackground"""))
tiles.set_current_tilemap(tilemap("""level"""))

# player sprite
player_sprite = sprites.create(assets.image("""santaRight"""), SpriteKind.player)
tiles.place_on_tile(player_sprite, tiles.get_tile_location(0, 6))
controller.move_sprite(player_sprite, 100, 0)
scene.camera_follow_sprite(player_sprite)
```

## Code the Player sprite to jump!

Using simple physics, code the Player sprite to jump up when the A button is pressed, and then be pulled back down to the ground.

---

- :paper plane: Type the Player sprite's name variable, a dot operator, and ``||sprites:ay||`` to set the y-acceleration that will pull the Player sprite down to the ground.
- :paper plane: Use an assignment operator ``||=||`` to set the ``||sprites:ay||`` value to a large positive number, such as **500**.
- :game controller: From ``||controller:Controller||`` drag this code into the editor under the other Player sprite code: ![image](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/button%20event%20code.png?raw=true "button pressed code") It will make something happen when the A button is pressed.
- :game controller: Change the word "event" to "a" in the function definition, then change it inside the parentheses of the function call. 
- :game controller: Replace "pass" with the Player sprite's name variable, a dot operator, and ``||sprites:vy||`` to set the y-velocity that will counteract the y-acceleration and make the Player sprite jump up.
- :game controller: Use an assignment operator ``||=||`` to set the ``||sprites:vy||`` value to a smaller negative number, such as **-200**.
- :play: Click the Play button to test out the sprite jump code!

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

```python
# game initialization
scene.set_background_image(assets.image("""winterBackground"""))
tiles.set_current_tilemap(tilemap("""level"""))

# player sprite
player_sprite = sprites.create(assets.image("""santaRight"""), SpriteKind.player)
tiles.place_on_tile(player_sprite, tiles.get_tile_location(0, 6))
controller.move_sprite(player_sprite, 100, 0)
scene.camera_follow_sprite(player_sprite)
player_sprite.ay = 500

# player button pressed events
def on_a_pressed():
    player_sprite.vy = -200
controller.A.on_event(ControllerButtonEvent.PRESSED, on_a_pressed)
```

## Prevent the Player sprite from double jumping!

Add a **conditional** to your A button code to prevent the Player sprite from "double jumping".

---

- :shuffle: Inside the ``||controller:on_a_pressed||`` function definition, add a space above the ``||sprites:vy||`` code, then type the word ``||logic:if||``. This will create a **conditional** that will only run the code inside if something is True.
- :shuffle: Next to ``||logic:if||`` type the Player sprite's name variable, a dot operator, and type/select ``||scene:is_hitting_tile||``.
- :tree: Inside the parentheses, replace ``||scene:LEFT||`` with ``||scene:BOTTOM||`` so the conditional checks if the bottom of the Player sprite is touching a tilemap wall before running the code inside.
- :shuffle: Add a colon **:** after the parentheses, then ensure the ``||sprites:vy||`` code is indented inside the ``||logic:if||`` statement.
- :play: Click the Play button to test the revised jump code, making sure the Player sprite can only jump up if the bottom of the sprite is in contact with a tilemap wall. 

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

```python
# game initialization
scene.set_background_image(assets.image("""winterBackground"""))
tiles.set_current_tilemap(tilemap("""level"""))

# player sprite
player_sprite = sprites.create(assets.image("""santaRight"""), SpriteKind.player)
tiles.place_on_tile(player_sprite, tiles.get_tile_location(0, 6))
controller.move_sprite(player_sprite, 100, 0)
scene.camera_follow_sprite(player_sprite)
player_sprite.ay = 500

# player button pressed events
def on_a_pressed():
    if player_sprite.is_hitting_tile(CollisionDirection.BOTTOM):
        player_sprite.vy = -200
controller.A.on_event(ControllerButtonEvent.PRESSED, on_a_pressed)
```

## Change the Player sprite image so it faces the direction it is moving!

Use different right- and left-facing images so the Player sprite appears to be facing the direction it is moving in!

- :game controller: Create 2 new ``||controller:on_event_pressed||`` functions, copy/pasting the code for the A button pressed event.
- :game controller: Replace all 3 instances of the button name with **left** in one function and **right** in the other.
- :paper plane: Inside each function, type the Player sprite's name variable, a dot operator, and ``||sprites:set_image||``. In the image parameter, select the cooresponding left- or right-facing image for your Player sprite.
- :play: Click the Play button to test that the Player sprite is facing the correct direction as it moves and jumps around the tilemap.

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

```python
# game initialization
scene.set_background_image(assets.image("""winterBackground"""))
tiles.set_current_tilemap(tilemap("""level"""))

# player sprite
player_sprite = sprites.create(assets.image("""santaRight"""), SpriteKind.player)
tiles.place_on_tile(player_sprite, tiles.get_tile_location(0, 6))
controller.move_sprite(player_sprite, 100, 0)
scene.camera_follow_sprite(player_sprite)
player_sprite.ay = 500

# player button pressed events
def on_a_pressed():
    if player_sprite.is_hitting_tile(CollisionDirection.BOTTOM):
        player_sprite.vy = -200
controller.A.on_event(ControllerButtonEvent.PRESSED, on_a_pressed)

def on_right_pressed():
    player_sprite.set_image(assets.image("""santaRight"""))
controller.right.on_event(ControllerButtonEvent.PRESSED, on_right_pressed)

def on_left_pressed():
    player_sprite.set_image(assets.image("""santaLeft"""))
controller.left.on_event(ControllerButtonEvent.PRESSED, on_left_pressed)
```

## Spawn Food sprites to collect throughout the tilemap!

Use **spawn tiles** and ``||loops:for||`` loops to place Food sprites throughout the tilemap! 

- :map: Open the tilemap to edit it. Select or create a new tile that will be used to **spawn**, or create, Food sprites on your tilemap. Place the spawn tiles strategically on the tilemap in places where the Player sprite will be able to reach them! ![image](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/tilemap%202d%20spawn%20tiles.png?raw=true "tilemap 2d spawn tiles")
- :repeat: Create a for loop by typing the keyword ``||loops:for||`` followed by the variable name **value** and the keyword ``||loops:in||``. 
- :tree: After ``||loops:in||`` add ``||scene:tiles.get_tiles_by_type||`` then use the name of the spawn tile created above as the parameter.
- :repeat: Add a colon **:** at the end of the statement, then press Enter to add code inside the loop.
- :paper plane: Indented inside the loop, add code to create a Food sprite.
- :tree: Position the Food sprites on spawn tiles by typing ``||scene:tiles.place_on_tile||`` using the Food sprite's variable name as the sprite parameter, and the loop's **value** variable as the location parameter.
- :tree: Replace the spawn tile with a blank transparent tile by typing ``||scene:tiles.set_tile_at||`` using the loop's **value** variable as the location parameter, and ``||scene:assets.tile||`` ``||scene:("""transparency16""")||`` as the tile parameter.
- :repeat: When the loop runs, it will add a Food sprite and remove the spawn tile for every spawn tile on the tilemap.
- :play: Click the Play button to test the Food sprite code, ensuring all spawn tiles are replaced with Food sprites.

*Consider updating your tilemap design to adjust the number of Food sprites on screen!*

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

```python
# game initialization
scene.set_background_image(assets.image("""winterBackground"""))
tiles.set_current_tilemap(tilemap("""level"""))

# player sprite
player_sprite = sprites.create(assets.image("""santaRight"""), SpriteKind.player)
tiles.place_on_tile(player_sprite, tiles.get_tile_location(0, 6))
controller.move_sprite(player_sprite, 100, 0)
scene.camera_follow_sprite(player_sprite)
player_sprite.ay = 500

# player button pressed events
def on_a_pressed():
    if player_sprite.is_hitting_tile(CollisionDirection.BOTTOM):
        player_sprite.vy = -200
controller.A.on_event(ControllerButtonEvent.PRESSED, on_a_pressed)

def on_right_pressed():
    player_sprite.set_image(assets.image("""santaRight"""))
controller.right.on_event(ControllerButtonEvent.PRESSED, on_right_pressed)

def on_left_pressed():
    player_sprite.set_image(assets.image("""santaLeft"""))
controller.left.on_event(ControllerButtonEvent.PRESSED, on_left_pressed)

# food sprites
for value in tiles.get_tiles_by_type(assets.tile("""foodSpawnTile""")):
    present_sprite = sprites.create(assets.image("""greenGift"""), SpriteKind.food)
    tiles.place_on_tile(present_sprite, value)
    tiles.set_tile_at(value, assets.tile("""transparency16"""))
```

## Challenge: Create multiple Enemy sprites!

Use what you just learned to create multiple Enemy sprites on the tilemap using **spawn tiles** and a **for loop**.

---

**Hints!**

💡 Copy / paste the code you wrote for your Food sprite, and update it for the Enemy sprite!

💡 Don't forget to add different spawn tiles for Enemy sprites on your tilemap!

*Consider updating your tilemap design to adjust the number of Enemy sprites on screen!*

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

```python
# game initialization
scene.set_background_image(assets.image("""winterBackground"""))
tiles.set_current_tilemap(tilemap("""level"""))

# player sprite
player_sprite = sprites.create(assets.image("""santaRight"""), SpriteKind.player)
tiles.place_on_tile(player_sprite, tiles.get_tile_location(0, 6))
controller.move_sprite(player_sprite, 100, 0)
scene.camera_follow_sprite(player_sprite)
player_sprite.ay = 500

# player button pressed events
def on_a_pressed():
    if player_sprite.is_hitting_tile(CollisionDirection.BOTTOM):
        player_sprite.vy = -200
controller.A.on_event(ControllerButtonEvent.PRESSED, on_a_pressed)

def on_right_pressed():
    player_sprite.set_image(assets.image("""santaRight"""))
controller.right.on_event(ControllerButtonEvent.PRESSED, on_right_pressed)

def on_left_pressed():
    player_sprite.set_image(assets.image("""santaLeft"""))
controller.left.on_event(ControllerButtonEvent.PRESSED, on_left_pressed)

# food sprites
for value in tiles.get_tiles_by_type(assets.tile("""foodSpawnTile""")):
    present_sprite = sprites.create(assets.image("""greenGift"""), SpriteKind.food)
    tiles.place_on_tile(present_sprite, value)
    tiles.set_tile_at(value, assets.tile("""transparency16"""))

# enemy sprites
for value2 in tiles.get_tiles_by_type(assets.tile("""enemySpawnTile""")):
    cookie_sprite = sprites.create(assets.image("""milkGlassCookie"""), SpriteKind.enemy)
    tiles.place_on_tile(cookie_sprite, value2)
    tiles.set_tile_at(value2, assets.tile("""transparency16"""))
```

## Add sprite overlap events!

Make something happen when the Player sprite overlaps the Food and Enemy sprites.

- :paper plane: Using the ``||sprites:on_overlap||`` code from the menu or the code completion tool, create 2 different functions: 1 for the Player and Enemy overlap and 1 for the Player and Food overlap.
- :paper plane: Inside both overlap functions, delete "pass" then type ``||sprites:sprites.destroy||`` and use ``||sprites:otherSprite||`` to remove any Enemy or Food sprite when the Player overlaps it.
- :paper plane: Inside the parentheses after ``||sprites:otherSprite||`` add a comma then use ``||sprites:effects.||`` to select a sprite effect to happen as the sprite is being destroyed. Use another comma to set how long the effect will last.
- :headphones: Use the ``||music:music.play||`` function to add a sound effect to each ``||sprites:on_overlap||`` function, too!
- :play: Click the Play button to test the overlap function code on both Food and Enemy sprites before moving on to the next step.

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo")

```python
# game initialization
scene.set_background_image(assets.image("""winterBackground"""))
tiles.set_current_tilemap(tilemap("""level"""))

# player sprite
player_sprite = sprites.create(assets.image("""santaRight"""), SpriteKind.player)
tiles.place_on_tile(player_sprite, tiles.get_tile_location(0, 6))
controller.move_sprite(player_sprite, 100, 0)
scene.camera_follow_sprite(player_sprite)
player_sprite.ay = 500

# player button pressed events
def on_a_pressed():
    if player_sprite.is_hitting_tile(CollisionDirection.BOTTOM):
        player_sprite.vy = -200
controller.A.on_event(ControllerButtonEvent.PRESSED, on_a_pressed)

def on_right_pressed():
    player_sprite.set_image(assets.image("""santaRight"""))
controller.right.on_event(ControllerButtonEvent.PRESSED, on_right_pressed)

def on_left_pressed():
    player_sprite.set_image(assets.image("""santaLeft"""))
controller.left.on_event(ControllerButtonEvent.PRESSED, on_left_pressed)

# food sprites
for value in tiles.get_tiles_by_type(assets.tile("""foodSpawnTile""")):
    present_sprite = sprites.create(assets.image("""greenGift"""), SpriteKind.food)
    tiles.place_on_tile(present_sprite, value)
    tiles.set_tile_at(value, assets.tile("""transparency16"""))

# enemy sprites
for value2 in tiles.get_tiles_by_type(assets.tile("""enemySpawnTile""")):
    cookie_sprite = sprites.create(assets.image("""milkGlassCookie"""), SpriteKind.enemy)
    tiles.place_on_tile(cookie_sprite, value2)
    tiles.set_tile_at(value2, assets.tile("""transparency16"""))

# overlap events
def on_on_overlap(sprite2, otherSprite):
    sprites.destroy(otherSprite, effects.smiles, 500)
    music.play(music.melody_playable(music.magic_wand), music.PlaybackMode.UNTIL_DONE)
sprites.on_overlap(SpriteKind.player, SpriteKind.food, on_on_overlap)

def on_on_overlap2(sprite3, otherSprite2):
    sprites.destroy(otherSprite2, effects.disintegrate, 500)
    music.play(music.melody_playable(music.zapped), music.PlaybackMode.UNTIL_DONE)
sprites.on_overlap(SpriteKind.player, SpriteKind.enemy, on_on_overlap2)
```

## End the game when the Player collects all the Food sprites!

Use a **conditional** to end the game when all of the Food sprites have been collected!

---

- :shuffle: Inside the overlap function for the Player/Food sprites, under the existing code, type ``||logic:if||`` to create a **conditional** that will check if the length of the **array** - or list - of Food sprites remaining on screen is equal to 0.
- :numbered list: Type ``||arrays:len||`` followed by ``||sprites:sprites.all_of_kind||`` with the parameter ``||sprites:SpriteKind.food||`` to find the **length** of the **array** of Food sprites.
- :shuffle: Type 2 equals signs ``||logic:==||`` then the number ``||math:0||`` and a colon **:** to complete the condition to check for.
- :circle: Indented underneath, add code to end the game in a "win" when the length of the array of Food sprites is equal to 0 *meaning all of the Food sprites have been collected*.
- :play: Click the Play button to test that the game ends when all of the Food sprites have been collected!

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

```python
# game initialization
scene.set_background_image(assets.image("""winterBackground"""))
tiles.set_current_tilemap(tilemap("""level"""))

# player sprite
player_sprite = sprites.create(assets.image("""santaRight"""), SpriteKind.player)
tiles.place_on_tile(player_sprite, tiles.get_tile_location(0, 6))
controller.move_sprite(player_sprite, 100, 0)
scene.camera_follow_sprite(player_sprite)
player_sprite.ay = 500

# player button pressed events
def on_a_pressed():
    if player_sprite.is_hitting_tile(CollisionDirection.BOTTOM):
        player_sprite.vy = -200
controller.A.on_event(ControllerButtonEvent.PRESSED, on_a_pressed)

def on_right_pressed():
    player_sprite.set_image(assets.image("""santaRight"""))
controller.right.on_event(ControllerButtonEvent.PRESSED, on_right_pressed)

def on_left_pressed():
    player_sprite.set_image(assets.image("""santaLeft"""))
controller.left.on_event(ControllerButtonEvent.PRESSED, on_left_pressed)

# food sprites
for value in tiles.get_tiles_by_type(assets.tile("""foodSpawnTile""")):
    present_sprite = sprites.create(assets.image("""greenGift"""), SpriteKind.food)
    tiles.place_on_tile(present_sprite, value)
    tiles.set_tile_at(value, assets.tile("""transparency16"""))

# enemy sprites
for value2 in tiles.get_tiles_by_type(assets.tile("""enemySpawnTile""")):
    cookie_sprite = sprites.create(assets.image("""milkGlassCookie"""), SpriteKind.enemy)
    tiles.place_on_tile(cookie_sprite, value2)
    tiles.set_tile_at(value2, assets.tile("""transparency16"""))

# overlap events
def on_on_overlap(sprite2, otherSprite):
    sprites.destroy(otherSprite, effects.smiles, 500)
    music.play(music.melody_playable(music.magic_wand), music.PlaybackMode.UNTIL_DONE)
    if len(sprites.all_of_kind(SpriteKind.food)) == 0:
            game.game_over(True)
sprites.on_overlap(SpriteKind.player, SpriteKind.food, on_on_overlap)

def on_on_overlap2(sprite3, otherSprite2):
    sprites.destroy(otherSprite2, effects.disintegrate, 500)
    music.play(music.melody_playable(music.zapped), music.PlaybackMode.UNTIL_DONE)
sprites.on_overlap(SpriteKind.player, SpriteKind.enemy, on_on_overlap2)
```

## Add a timer to increase the challenge!

Add a timer to your game! Decrease the timer by 5 seconds every time your Player sprite collides with an Enemy sprite!

---

- :id card: Use ``||info:info.start_countdown||`` to set a countdown timer to start at the beginning of the game.
- :id card: Use ``||info:info.change_countdown_by||`` to reduce the countdown timer by a value, such as 5, every time a Player and Enemy sprite overlap!
- :play: Click the Play button to test the timer code, ensuring the timer decreases when the Player overlaps an Enemy, and that there is enough time given to make the game challenging, but not impossible!

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

```python
# game initialization
scene.set_background_image(assets.image("""winterBackground"""))
tiles.set_current_tilemap(tilemap("""level"""))
info.start_countdown(30)

# player sprite
player_sprite = sprites.create(assets.image("""santaRight"""), SpriteKind.player)
tiles.place_on_tile(player_sprite, tiles.get_tile_location(0, 6))
controller.move_sprite(player_sprite, 100, 0)
scene.camera_follow_sprite(player_sprite)
player_sprite.ay = 500

# player button pressed events
def on_a_pressed():
    if player_sprite.is_hitting_tile(CollisionDirection.BOTTOM):
        player_sprite.vy = -200
controller.A.on_event(ControllerButtonEvent.PRESSED, on_a_pressed)

def on_right_pressed():
    player_sprite.set_image(assets.image("""santaRight"""))
controller.right.on_event(ControllerButtonEvent.PRESSED, on_right_pressed)

def on_left_pressed():
    player_sprite.set_image(assets.image("""santaLeft"""))
controller.left.on_event(ControllerButtonEvent.PRESSED, on_left_pressed)

# food sprites
for value in tiles.get_tiles_by_type(assets.tile("""foodSpawnTile""")):
    present_sprite = sprites.create(assets.image("""greenGift"""), SpriteKind.food)
    tiles.place_on_tile(present_sprite, value)
    tiles.set_tile_at(value, assets.tile("""transparency16"""))

# enemy sprites
for value2 in tiles.get_tiles_by_type(assets.tile("""enemySpawnTile""")):
    cookie_sprite = sprites.create(assets.image("""milkGlassCookie"""), SpriteKind.enemy)
    tiles.place_on_tile(cookie_sprite, value2)
    tiles.set_tile_at(value2, assets.tile("""transparency16"""))

# overlap events
def on_on_overlap(sprite2, otherSprite):
    sprites.destroy(otherSprite, effects.smiles, 500)
    music.play(music.melody_playable(music.magic_wand), music.PlaybackMode.UNTIL_DONE)
    if len(sprites.all_of_kind(SpriteKind.food)) == 0:
            game.game_over(True)
sprites.on_overlap(SpriteKind.player, SpriteKind.food, on_on_overlap)

def on_on_overlap2(sprite3, otherSprite2):
    sprites.destroy(otherSprite2, effects.disintegrate, 500)
    info.change_countdown_by(-5)
    music.play(music.melody_playable(music.zapped), music.PlaybackMode.UNTIL_DONE)
sprites.on_overlap(SpriteKind.player, SpriteKind.enemy, on_on_overlap2)
```

## Add hazard tiles to your tilemap!

Edit your tilemap to include a few new **hazard** tiles that will reset the Player sprite back to the beginning of the tilemap.

---

- :tree: Open the tilemap editor and select a new tile, not already in the tilemap, to act as a **hazard**. Fill in the gaps along the bottom of the tilemap with the new hazard tile. ![image](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/tilemap%202d%20hazard%20tiles.png?raw=true "tilemap 2d hazard tiles")
- :tree: From the ``||scene:Scene||`` code menu, drag a ``||scene:on_overlap_tile||`` function into the coding editor.
- :tree: Inside the ``||scene:on_overlap_tile||`` function definition, remove "pass" and add code to set the Player sprite's position back to the starting point and play a sound effect.
- :tree: In the ``||scene:on_overlap_tile||`` function call, set the first parameter to the Player sprite kind, and the second to the name of the new hazard tile you just added to your tilemap.
- :play: Click the Play button to test the tile overlap function, and tinker with the code and the placement of the hazard tiles until it works as expected.

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

```python
# game initialization
scene.set_background_image(assets.image("""winterBackground"""))
tiles.set_current_tilemap(tilemap("""level"""))
info.start_countdown(30)

# player sprite
player_sprite = sprites.create(assets.image("""santaRight"""), SpriteKind.player)
tiles.place_on_tile(player_sprite, tiles.get_tile_location(0, 6))
controller.move_sprite(player_sprite, 100, 0)
scene.camera_follow_sprite(player_sprite)
player_sprite.ay = 500

# player button pressed events
def on_a_pressed():
    if player_sprite.is_hitting_tile(CollisionDirection.BOTTOM):
        player_sprite.vy = -200
controller.A.on_event(ControllerButtonEvent.PRESSED, on_a_pressed)

def on_right_pressed():
    player_sprite.set_image(assets.image("""santaRight"""))
controller.right.on_event(ControllerButtonEvent.PRESSED, on_right_pressed)

def on_left_pressed():
    player_sprite.set_image(assets.image("""santaLeft"""))
controller.left.on_event(ControllerButtonEvent.PRESSED, on_left_pressed)

# food sprites
for value in tiles.get_tiles_by_type(assets.tile("""foodSpawnTile""")):
    present_sprite = sprites.create(assets.image("""greenGift"""), SpriteKind.food)
    tiles.place_on_tile(present_sprite, value)
    tiles.set_tile_at(value, assets.tile("""transparency16"""))

# enemy sprites
for value2 in tiles.get_tiles_by_type(assets.tile("""enemySpawnTile""")):
    cookie_sprite = sprites.create(assets.image("""milkGlassCookie"""), SpriteKind.enemy)
    tiles.place_on_tile(cookie_sprite, value2)
    tiles.set_tile_at(value2, assets.tile("""transparency16"""))

# overlap events
def on_on_overlap(sprite2, otherSprite):
    sprites.destroy(otherSprite, effects.smiles, 500)
    music.play(music.melody_playable(music.magic_wand), music.PlaybackMode.UNTIL_DONE)
    if len(sprites.all_of_kind(SpriteKind.food)) == 0:
            game.game_over(True)
sprites.on_overlap(SpriteKind.player, SpriteKind.food, on_on_overlap)

def on_on_overlap2(sprite3, otherSprite2):
    sprites.destroy(otherSprite2, effects.disintegrate, 500)
    info.change_countdown_by(-5)
    music.play(music.melody_playable(music.zapped), music.PlaybackMode.UNTIL_DONE)
sprites.on_overlap(SpriteKind.player, SpriteKind.enemy, on_on_overlap2)

def on_overlap_tile(sprite, location):
    tiles.place_on_tile(sprite, tiles.get_tile_location(0, 0))
    music.play(music.melody_playable(music.big_crash), music.PlaybackMode.UNTIL_DONE)
scene.on_overlap_tile(SpriteKind.player, assets.tile("""snowPath13"""), on_overlap_tile)
```

## At a splash screen at the beginning!

Use a splash screen to display a message at the beginning of the game, letting the player know how to play your game!

---

- :circle: At the top of the editor, above all other code, type ``||game:game.splash||`` to add a text box that will contain a message.
- :circle: Inside the parentheses, type a short message - known as a **string** - surrounded by quotation marks. Use a comma to type a second **string** to appear in the same message box below the first **string**.
- :circle: Add additional ``||game:game.splash||`` functions to create more on-screen text boxes.

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo")

```python
# game initialization
scene.set_background_image(assets.image("""winterBackground"""))
game.splash("Oh no!", "Santa lost his presents!")
game.splash("Collect all the presents", "before the time runs out!")
game.splash("Avoid the milk and cookies", "they take away time!")
tiles.set_current_tilemap(tilemap("""level"""))
info.start_countdown(30)

# player sprite
player_sprite = sprites.create(assets.image("""santaRight"""), SpriteKind.player)
tiles.place_on_tile(player_sprite, tiles.get_tile_location(0, 6))
controller.move_sprite(player_sprite, 100, 0)
scene.camera_follow_sprite(player_sprite)
player_sprite.ay = 500

# player button pressed events
def on_a_pressed():
    if player_sprite.is_hitting_tile(CollisionDirection.BOTTOM):
        player_sprite.vy = -200
controller.A.on_event(ControllerButtonEvent.PRESSED, on_a_pressed)

def on_right_pressed():
    player_sprite.set_image(assets.image("""santaRight"""))
controller.right.on_event(ControllerButtonEvent.PRESSED, on_right_pressed)

def on_left_pressed():
    player_sprite.set_image(assets.image("""santaLeft"""))
controller.left.on_event(ControllerButtonEvent.PRESSED, on_left_pressed)

# food sprites
for value in tiles.get_tiles_by_type(assets.tile("""foodSpawnTile""")):
    present_sprite = sprites.create(assets.image("""greenGift"""), SpriteKind.food)
    tiles.place_on_tile(present_sprite, value)
    tiles.set_tile_at(value, assets.tile("""transparency16"""))

# enemy sprites
for value2 in tiles.get_tiles_by_type(assets.tile("""enemySpawnTile""")):
    cookie_sprite = sprites.create(assets.image("""milkGlassCookie"""), SpriteKind.enemy)
    tiles.place_on_tile(cookie_sprite, value2)
    tiles.set_tile_at(value2, assets.tile("""transparency16"""))

# overlap events
def on_on_overlap(sprite2, otherSprite):
    sprites.destroy(otherSprite, effects.smiles, 500)
    music.play(music.melody_playable(music.magic_wand), music.PlaybackMode.UNTIL_DONE)
    if len(sprites.all_of_kind(SpriteKind.food)) == 0:
            game.game_over(True)
sprites.on_overlap(SpriteKind.player, SpriteKind.food, on_on_overlap)

def on_on_overlap2(sprite3, otherSprite2):
    sprites.destroy(otherSprite2, effects.disintegrate, 500)
    info.change_countdown_by(-5)
    music.play(music.melody_playable(music.zapped), music.PlaybackMode.UNTIL_DONE)
sprites.on_overlap(SpriteKind.player, SpriteKind.enemy, on_on_overlap2)

def on_overlap_tile(sprite, location):
    tiles.place_on_tile(sprite, tiles.get_tile_location(0, 0))
    music.play(music.melody_playable(music.big_crash), music.PlaybackMode.UNTIL_DONE)
scene.on_overlap_tile(SpriteKind.player, assets.tile("""snowPath13"""), on_overlap_tile)
```

## Finishing your game!

Congratulations! You just finished the Day 4 code along!

Get ready because you are now going to use everything you just learned to create your own original project using Python!

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo")
