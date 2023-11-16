# Arctic Code Quest: Day 3 
### @diffs true


```python
#tilemap setup
scene.set_background_color(9)
game.splash("Find the candy!", "Avoid the polar bears!")
game.splash("Slip on the ice and you'll", "lose all your candy!")
tiles.set_current_tilemap(tilemap("""level"""))

#variable set up
info.set_score(0)
info.set_life(3)
info.start_countdown(30)

#player sprite
playerSprite = sprites.create(assets.image("""boyFront"""), SpriteKind.player)
tiles.place_on_tile(playerSprite, tiles.get_tile_location(1, 18))
controller.move_sprite(playerSprite)
scene.camera_follow_sprite(playerSprite)

#food sprite
for i in range(8):
    candySprite = sprites.create(assets.image("""candycane"""), SpriteKind.food)
    tiles.place_on_random_tile(candySprite, assets.tile("""snowPath16"""))

def on_score():
    game.set_game_over_effect(True, effects.smiles)
    game.game_over(True)
info.on_score(10, on_score)

#enemy sprite
for i in range(8):
    enemySprite = sprites.create(assets.image("""bearFront"""), SpriteKind.enemy)
    tiles.place_on_random_tile(enemySprite, assets.tile("""snowPath16"""))
    enemySprite.set_velocity(randint(-50,50), randint(-50,50))
    enemySprite.set_bounce_on_wall(True)

#overlap events
def on_overlap(sprite, otherSprite):
    tiles.place_on_random_tile(otherSprite, assets.tile("""snowPath16"""))
    info.change_score_by(1)
    music.play(music.melody_playable(music.ba_ding), music.PlaybackMode.UNTIL_DONE)
sprites.on_overlap(SpriteKind.player, SpriteKind.food, on_overlap)

def on_overlap2(sprite, otherSprite):
    sprites.destroy(otherSprite)
    info.change_life_by(-1)
    music.play(music.melody_playable(music.power_down), music.PlaybackMode.UNTIL_DONE)
sprites.on_overlap(SpriteKind.player, SpriteKind.enemy, on_overlap2)

def on_overlap_tile(sprite, location):
    info.set_score(0)
    music.play(music.melody_playable(music.knock), music.PlaybackMode.UNTIL_DONE)
scene.on_overlap_tile(SpriteKind.player, assets.tile("""ice"""), on_overlap_tile)
```

## Arctic Code Quest: Python Edition - Day 3! @showdialog

Welcome to your next Python project code along! Today you will be creating a project using everything you have learned so far, plus tilemaps, tilemap functions, and for loops! 

Click ``||loops:Ok!||`` to get started!

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

## Create a Winter Wonderland Tilemap

Create a maze for your sprites to move about using a tilemap!

---

- :tree: Type ``||scene:tiles||``, a dot operator ``||.||``, and the ``||scene:set_current_tilemap||`` function. Pressing Tab will insert the ``||scene:(tilemap(""" """))||`` code into the function.
- :map: Click the map icon to the left of the line of code, then design a tilemap that is at least **16x16** using any of the available tiles. ![image](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/tilemap%20no%20walls.png?raw=true "tilemap no walls")
- :map: Add tiles that will function as a **path** for the sprite to walk along. Then add tiles that will serve as **walls**. Use the Draw Walls tool to turn those tiles into actual walls on the tilemap. ![Icon](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/draw%20walls.png?raw=true "Draw Walls tool") ![image](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/tilemap%20walls.png?raw=true "tilemap walls")

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

```python
tiles.set_current_tilemap(tilemap("""level"""))
```

## Create a Player sprite to move around the tilemap!

Add a Player sprite to the project to navigate the tilemap maze!

---

- :paper plane: Add a Player sprite to the project.
- :tree: Position the Player sprite on a specific tile location by typing ``||scene:tiles||``, a dot operator ``||.||``, and ``||scene:place_on_tile||``. Replace the first parameter with the Player sprite variable name.
- :tree: Tinker with the tilemap coordinates in ``||scene:tiles.get_tile_location||`` to place the Player sprite on a maze path tile - not on a wall!
- :game controller: Add code to move the Player sprite around the tilemap.
- :tree: Oh no! The Player sprite moves off the tilemap! From ``||scene:Scene||`` use the ``||scene:camera_follow_sprite||`` function to ensure the camera follows the Player sprite around the tilemap.

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

```python
tiles.set_current_tilemap(tilemap("""level"""))

#player sprite
playerSprite = sprites.create(assets.image("""boyFront"""), SpriteKind.player)
tiles.place_on_tile(playerSprite, tiles.get_tile_location(1, 18))
controller.move_sprite(playerSprite)
scene.camera_follow_sprite(playerSprite)
```

## Create Food sprites to collect throughout the maze!

Use a **for loop** to create multiple Food sprites for the Player sprite to collect!

- :repeat: Using the ``||loops:Loops||`` code menu or the code completion tool, add a **for loop** that looks like this: ``||loops:for i in range(8):||``. Don't forget the colon **:** at the end of the statement!
- :paper plane: Indented inside the **for loop**, add code to create a Food sprite.
- :tree: Position the Food sprites on random path tiles throughout the maze by typing ``||scene:tiles||``, a dot operator ``||.||``. and ``||scene:place_on_random_tile||``. Replace the first parameter with the Food sprite variable name.
- :tree:  Click the palette icon or find the tile name from the tilemap editor or Assets tab to use as the tile parameter.
- :play: Click the Play button to test the Food sprite code, ensuring multiple Food sprites are positioned on different tiles throughout the maze. 

*Consider updating your tilemap design if there are not enough tiles of the same kind for all of the Food sprites!*

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

```python
tiles.set_current_tilemap(tilemap("""level"""))

#player sprite
playerSprite = sprites.create(assets.image("""boyFront"""), SpriteKind.player)
tiles.place_on_tile(playerSprite, tiles.get_tile_location(1, 18))
controller.move_sprite(playerSprite)
scene.camera_follow_sprite(playerSprite)

#food sprite
for i in range(8):
    candySprite = sprites.create(assets.image("""candycane"""), SpriteKind.food)
    tiles.place_on_random_tile(candySprite, assets.tile("""snowPath16"""))
```

## Challenge: Create multiple moving Enemy sprites!

Use what you just learned to create multiple Enemy sprites on the tilemap using a **for loop**.

---

**Hints!**

💡 Where can you find the code for the ``||loops:for||`` loop? Where in the code can you change how many times the loop runs?

💡 What function places the sprites on a random tile? Where do you set the sprite kind and tile kind?

---

- :paper plane: Add code to the Enemy sprite's for loop that sets each Enemy sprite's ``||sprites:velocity||`` to random vx and vy values from a range of -50 to 50.
- :paper plane: To ensure Enemy sprites don't get stuck on a tilemap wall, type the Enemy sprite variable name, a ``||.||``, and a ``||sprites:set_bounce_on_wall||`` function set to True.
- :play: Click the Play button to test the Enemy sprite code, ensuring multiple Enemy sprites are positioned on different tiles and moving throughout the maze. 

*Consider updating your tilemap design if there are not enough tiles of the same kind for all of the Enemy sprites!*

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

```python
tiles.set_current_tilemap(tilemap("""level"""))

#player sprite
playerSprite = sprites.create(assets.image("""boyFront"""), SpriteKind.player)
tiles.place_on_tile(playerSprite, tiles.get_tile_location(1, 18))
controller.move_sprite(playerSprite)
scene.camera_follow_sprite(playerSprite)

#food sprite
for i in range(8):
    candySprite = sprites.create(assets.image("""candycane"""), SpriteKind.food)
    tiles.place_on_random_tile(candySprite, assets.tile("""snowPath16"""))

#enemy sprite
for i in range(8):
    enemySprite = sprites.create(assets.image("""bearFront"""), SpriteKind.enemy)
    tiles.place_on_random_tile(enemySprite, assets.tile("""snowPath16"""))
    enemySprite.set_velocity(randint(-50,50), randint(-50,50))
    enemySprite.set_bounce_on_wall(True)
```

## Add sprite overlap events!

Make something happen when the Player sprite overlaps the Food and Enemy sprites.

- :paper plane: Using the ``||sprites:on_overlap||`` code from the menu or the code completion tool, create 2 different functions: 1 for the Player and Enemy overlap and 1 for the Player and Food overlap.
- :paper plane: Inside the **Player/Enemy** overlap function, delete "pass" then type ``||sprites:sprites.destroy||`` to remove the Enemy sprite when it overlaps the Player sprite.
- :paper plane: Replace ``||sprites:mySprite||`` inside the parentheses with the ``||sprites:otherSprite||`` parameter from the ``||sprites:on_overlap||`` function. This will now destroy *any* Enemy sprite that overlaps the Player sprite.
- :tree: Inside the **Player/Food** overlap function, delete "pass" then type ``||tiles.place_on_random_tile||`` to move the Food sprite to a different tile.
- :paper plane: Replace ``||sprites:none|`` inside the parentheses with the ``||sprites:otherSprite||`` parameter from the ``||sprites:on_overlap||`` function. This will now reposition *any* Food sprite that overlaps the Player sprite.
- :play: Click the Play button to test the overlap function code on both Food and Enemy sprites before moving on to the next step.

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo")

```python
tiles.set_current_tilemap(tilemap("""level"""))

#player sprite
playerSprite = sprites.create(assets.image("""boyFront"""), SpriteKind.player)
tiles.place_on_tile(playerSprite, tiles.get_tile_location(1, 18))
controller.move_sprite(playerSprite)
scene.camera_follow_sprite(playerSprite)

#food sprite
for i in range(8):
    candySprite = sprites.create(assets.image("""candycane"""), SpriteKind.food)
    tiles.place_on_random_tile(candySprite, assets.tile("""snowPath16"""))

#enemy sprite
for i in range(8):
    enemySprite = sprites.create(assets.image("""bearFront"""), SpriteKind.enemy)
    tiles.place_on_random_tile(enemySprite, assets.tile("""snowPath16"""))
    enemySprite.set_velocity(randint(-50,50), randint(-50,50))
    enemySprite.set_bounce_on_wall(True)

#overlap events
def on_overlap(sprite, otherSprite):
    tiles.place_on_random_tile(otherSprite, assets.tile("""snowPath16"""))
sprites.on_overlap(SpriteKind.player, SpriteKind.food, on_overlap)

def on_overlap2(sprite, otherSprite):
    sprites.destroy(otherSprite)
sprites.on_overlap(SpriteKind.player, SpriteKind.enemy, on_overlap2)
```

## Add Player score and lives to the game!

Use MakeCode Arcade's built-in score and life variables to keep track of how many Food sprites the Player sprite collects, and how many Enemy sprites the Player sprite collides with!

---

- :id card: At the top of the code editor, below the code that sets the tilemap, add code from the ``||info:Info||`` category to set the Player sprite's starting **score** and **lives**.
- :id card: Inside the **Player/Food** ``||sprites:on_overlap||`` function, change the score by 1. 
- :id card: Inside the **Player/Enemy** ``||sprites:on_overlap||`` function, change the life by -1. 
- :headphones: Use the ``||music:music.play||`` function to add a sound effect to each ``||sprites:on_overlap||`` function, too!
- :play: Click the Play button to test the score, lives, and sound effects, tinkering with the code to ensure everything works as expected!

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

```python
tiles.set_current_tilemap(tilemap("""level"""))

#variable set up
info.set_score(0)
info.set_life(3)

#player sprite
playerSprite = sprites.create(assets.image("""boyFront"""), SpriteKind.player)
tiles.place_on_tile(playerSprite, tiles.get_tile_location(1, 18))
controller.move_sprite(playerSprite)
scene.camera_follow_sprite(playerSprite)

#food sprite
for i in range(8):
    candySprite = sprites.create(assets.image("""candycane"""), SpriteKind.food)
    tiles.place_on_random_tile(candySprite, assets.tile("""snowPath16"""))

#enemy sprite
for i in range(8):
    enemySprite = sprites.create(assets.image("""bearFront"""), SpriteKind.enemy)
    tiles.place_on_random_tile(enemySprite, assets.tile("""snowPath16"""))
    enemySprite.set_velocity(randint(-50,50), randint(-50,50))
    enemySprite.set_bounce_on_wall(True)

#overlap events
def on_overlap(sprite, otherSprite):
    tiles.place_on_random_tile(otherSprite, assets.tile("""snowPath16"""))
    info.change_score_by(1)
    music.play(music.melody_playable(music.ba_ding), music.PlaybackMode.UNTIL_DONE)
sprites.on_overlap(SpriteKind.player, SpriteKind.food, on_overlap)

def on_overlap2(sprite, otherSprite):
    sprites.destroy(otherSprite)
    info.change_life_by(-1)
    music.play(music.melody_playable(music.power_down), music.PlaybackMode.UNTIL_DONE)
sprites.on_overlap(SpriteKind.player, SpriteKind.enemy, on_overlap2)
```

## Add a few traps to your tilemap!

Edit your tilemap to include a few new **trap** tiles that will take away all of the Player sprite's points!

---

- :tree: Open the tilemap editor and select a new tile, not already in the tilemap, to act as a **trap**. Replace a few of the path tiles with the new trap tile. ![image](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/tilemap%20trap%20tiles.png?raw=true "tilemap traps")
- :tree: From the ``||scene:Scene||`` code menu, drag a ``||scene:on_overlap_tile||`` function into the coding editor.
- :tree: Inside the ``||scene:on_overlap_tile||`` function definition, remove "pass" and add code to set the score back to 0 and play a sound effect.
- :tree: In the ``||scene:on_overlap_tile||`` function call, set the first parameter to the Player sprite kind, and the second to the name of the new "trap" tile you just added to your project.
- :play: Click the Play button to test the tile overlap function, and tinker with the code and the placement of the "trap" tiles until it works as expected.


![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

```python
tiles.set_current_tilemap(tilemap("""level"""))

#variable set up
info.set_score(0)
info.set_life(3)

#player sprite
playerSprite = sprites.create(assets.image("""boyFront"""), SpriteKind.player)
tiles.place_on_tile(playerSprite, tiles.get_tile_location(1, 18))
controller.move_sprite(playerSprite)
scene.camera_follow_sprite(playerSprite)

#food sprite
for i in range(8):
    candySprite = sprites.create(assets.image("""candycane"""), SpriteKind.food)
    tiles.place_on_random_tile(candySprite, assets.tile("""snowPath16"""))

#enemy sprite
for i in range(8):
    enemySprite = sprites.create(assets.image("""bearFront"""), SpriteKind.enemy)
    tiles.place_on_random_tile(enemySprite, assets.tile("""snowPath16"""))
    enemySprite.set_velocity(randint(-50,50), randint(-50,50))
    enemySprite.set_bounce_on_wall(True)

#overlap events
def on_overlap(sprite, otherSprite):
    tiles.place_on_random_tile(otherSprite, assets.tile("""snowPath16"""))
    info.change_score_by(1)
    music.play(music.melody_playable(music.ba_ding), music.PlaybackMode.UNTIL_DONE)
sprites.on_overlap(SpriteKind.player, SpriteKind.food, on_overlap)

def on_overlap2(sprite, otherSprite):
    sprites.destroy(otherSprite)
    info.change_life_by(-1)
    music.play(music.melody_playable(music.power_down), music.PlaybackMode.UNTIL_DONE)
sprites.on_overlap(SpriteKind.player, SpriteKind.enemy, on_overlap2)

def on_overlap_tile(sprite, location):
    info.set_score(0)
    music.play(music.melody_playable(music.knock), music.PlaybackMode.UNTIL_DONE)
scene.on_overlap_tile(SpriteKind.player, assets.tile("""ice"""), on_overlap_tile)
```

## Create the Game Over conditions!

End the game when the Player's score reaches a certain number, or when the timer reaches 0!

---

- :id card: At the top of the code editor, below the code that sets the score and lives, add ``||info:info.start_countdown||`` to set a countdown timer to begin when the game starts.  
- :id card: Use the ``||info:on_score||`` function from the ``||info:Info||`` code menu or the code completion tool. Change the value in the parameter to the score you want to end the game at.
- :circle: Inside, add code from ``||game:Game||`` to end the game in a "win" when the Player reaches that score. Customize the game over screen, adding this code before the ``||game:game_over||`` function!

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

```python
tiles.set_current_tilemap(tilemap("""level"""))

#variable set up
info.set_score(0)
info.set_life(3)
info.start_countdown(30)

def on_score():
    game.set_game_over_effect(True, effects.smiles)
    game.game_over(True)
info.on_score(10, on_score)

#player sprite
playerSprite = sprites.create(assets.image("""boyFront"""), SpriteKind.player)
tiles.place_on_tile(playerSprite, tiles.get_tile_location(1, 18))
controller.move_sprite(playerSprite)
scene.camera_follow_sprite(playerSprite)

#food sprite
for i in range(8):
    candySprite = sprites.create(assets.image("""candycane"""), SpriteKind.food)
    tiles.place_on_random_tile(candySprite, assets.tile("""snowPath16"""))

#enemy sprite
for i in range(8):
    enemySprite = sprites.create(assets.image("""bearFront"""), SpriteKind.enemy)
    tiles.place_on_random_tile(enemySprite, assets.tile("""snowPath16"""))
    enemySprite.set_velocity(randint(-50,50), randint(-50,50))
    enemySprite.set_bounce_on_wall(True)

#overlap events
def on_overlap(sprite, otherSprite):
    tiles.place_on_random_tile(otherSprite, assets.tile("""snowPath16"""))
    info.change_score_by(1)
    music.play(music.melody_playable(music.ba_ding), music.PlaybackMode.UNTIL_DONE)
sprites.on_overlap(SpriteKind.player, SpriteKind.food, on_overlap)

def on_overlap2(sprite, otherSprite):
    sprites.destroy(otherSprite)
    info.change_life_by(-1)
    music.play(music.melody_playable(music.power_down), music.PlaybackMode.UNTIL_DONE)
sprites.on_overlap(SpriteKind.player, SpriteKind.enemy, on_overlap2)

def on_overlap_tile(sprite, location):
    info.set_score(0)
    music.play(music.melody_playable(music.knock), music.PlaybackMode.UNTIL_DONE)
scene.on_overlap_tile(SpriteKind.player, assets.tile("""ice"""), on_overlap_tile)
```

## At a splash screen at the beginning!

Use a splash screen to display a message at the beginning of the game, letting the player know how to play your game!

---

- :circle: At the top of the editor, above all other code, type ``||game:game.splash||`` to add a text box that will contain a message.
- :circle: Inside the parentheses, type a short message - known as a **string** surrounded by quotation marks. Use a comma to type a second **string** to appear in the same message box below the first **string**.
- :circle: Add additional ``||game:game.splash||`` functions to create more on-screen text boxes.
- :tree: Optionally, use ``||scene:scene.set_background_color||`` with a number parameter, 1-15, to set a background color behind the splash screen.

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo")

```python
scene.set_background_color(9)
game.splash("Find the candy!", "Avoid the polar bears!")
game.splash("Slip on the ice and you'll", "lose all your candy!")
tiles.set_current_tilemap(tilemap("""level"""))

#variable set up
info.set_score(0)
info.set_life(3)
info.start_countdown(30)

def on_score():
    game.set_game_over_effect(True, effects.smiles)
    game.game_over(True)
info.on_score(10, on_score)

#player sprite
playerSprite = sprites.create(assets.image("""boyFront"""), SpriteKind.player)
tiles.place_on_tile(playerSprite, tiles.get_tile_location(1, 18))
controller.move_sprite(playerSprite)
scene.camera_follow_sprite(playerSprite)

#food sprite
for i in range(8):
    candySprite = sprites.create(assets.image("""candycane"""), SpriteKind.food)
    tiles.place_on_random_tile(candySprite, assets.tile("""snowPath16"""))

#enemy sprite
for i in range(8):
    enemySprite = sprites.create(assets.image("""bearFront"""), SpriteKind.enemy)
    tiles.place_on_random_tile(enemySprite, assets.tile("""snowPath16"""))
    enemySprite.set_velocity(randint(-50,50), randint(-50,50))
    enemySprite.set_bounce_on_wall(True)

#overlap events
def on_overlap(sprite, otherSprite):
    tiles.place_on_random_tile(otherSprite, assets.tile("""snowPath16"""))
    info.change_score_by(1)
    music.play(music.melody_playable(music.ba_ding), music.PlaybackMode.UNTIL_DONE)
sprites.on_overlap(SpriteKind.player, SpriteKind.food, on_overlap)

def on_overlap2(sprite, otherSprite):
    sprites.destroy(otherSprite)
    info.change_life_by(-1)
    music.play(music.melody_playable(music.power_down), music.PlaybackMode.UNTIL_DONE)
sprites.on_overlap(SpriteKind.player, SpriteKind.enemy, on_overlap2)

def on_overlap_tile(sprite, location):
    info.set_score(0)
    music.play(music.melody_playable(music.knock), music.PlaybackMode.UNTIL_DONE)
scene.on_overlap_tile(SpriteKind.player, assets.tile("""ice"""), on_overlap_tile)
```

## Finishing your game!

Congratulations! You just finished the Day 3 code along!

Get ready because you are now going to use everything you just learned to create your own original project using Python!

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo")
