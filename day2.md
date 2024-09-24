# Polar Programming with Python: Day 2
### @diffs true

```python
scene.set_background_image(img("""..."""))

#variable initialization
info.set_score(0)
info.set_life(3)

#player sprite
let elf = sprites.create(img("""..."""), SpriteKind.player)
elf.set_position(80, 120)
elf.set_stay_in_screen(True)
controller.move_sprite(elf, 100, 0)

#food sprite
def on_update_interval():
    gingerbread = sprites.create(img("""..."""), SpriteKind.food)
    gingerbread.set_position(randint(0, 160), 0)
    gingerbread.set_velocity(0, 50)
game.on_update_interval(1500, on_update_interval)

def on_score():
    game.set_game_over_effect(True, effects.blizzard)
    game.game_over(True)
info.on_score(20, on_score)

#enemy sprite
def on_update_interval2():
    snowball = sprites.create(img("""..."""), SpriteKind.enemy)
    snowball.set_position(randint(0, 160), 0)
    snowball.set_velocity(0, 50)
game.on_update_interval(2000, on_update_interval2)

#overlap code
def on_overlap(sprite, otherSprite):
    sprites.destroy(otherSprite)
    info.change_score_by(1)
    music.play(music.melody_playable(music.ba_ding), music.PlaybackMode.UNTIL_DONE)
sprites.on_overlap(SpriteKind.player, SpriteKind.food, on_overlap)

def on_overlap2(sprite, otherSprite):
    sprites.destroy(otherSprite)
    info.change_life_by(-1)
    music.play(music.melody_playable(music.power_down), music.PlaybackMode.UNTIL_DONE)
sprites.on_overlap(SpriteKind.player, SpriteKind.enemy, on_overlap2)
```


## Polar Programming with Python - Day 2! @showdialog

Welcome to your next Python project code along! Today you will be creating a project using everything you have learned so far, plus score and life variables and functions, game update loops, music, and game over effects. 

Click ``||loops:Ok||`` to get started!

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

## Add a Background Image and a Player sprite!

See if you remember how to code these things in a project:
- :tree: Add a ``||scene:background image||`` from the Gallery.
- :paper plane: Add a ``||sprites:Player sprite||`` using an image from the Gallery.
- :paper plane: Set the Player sprite's ``||sprites:position||`` so it appears along the bottom middle of the screen.
- :game controller: Set the Player sprite to only move left to right along the x-axis. Inside the parentheses of the ``||controller:move_sprite||`` function, add a comma next to the Player sprite variable name, then type **100** as the **vx** parameter, or speed the sprite can move left and right. Add another comma then type **0** as the **vy** parameter, or speed the sprite can move up and down.
- :paper plane: Set the Player sprite to ``||sprites:stay_in_screen||``.

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

## Food is falling from the sky!

Let's make Food sprites that appear at the top of the screen then fall to the bottom repeatedly, every few seconds.

---

- :circle: To make it easier to use the ``||game:on_update_interval||`` loop, click on ``||game:Game||`` in the code menu, then select this block and drag it into the coding canvas beneath the existing code: ![block](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/game%20update%20interval.png?raw=true "game update block") 
- :paper plane: Inside the function definition, delete "pass" then create a Food sprite using an image from the Gallery or My Assets.
- :paper plane: Set the Food sprite's ``||sprites:position||`` using ``||math:randint||`` to set a random x-value between 0 and 160. Set the y-value to 0 so the sprite always starts at the top of the screen.
- :paper plane: To make the Food sprite move, type the sprite's name, a dot ``||sprites:.||``, and select ``||sprites:set_velocity||`` from the code completion tool. Set the **vx** parameter to **0** and the **vy** parameter to **50** so the Food sprite moves in a downward direction.
- :circle: On the last line - the loop's function call - adjust the ``||game:interval parameter||`` to change how often the Food sprite appears then falls. This number is in milliseconds, so 1000ms equals 1 second!

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

```python
scene.set_background_image(img("""..."""))

#player sprite
elf = sprites.create(img("""..."""), SpriteKind.player)
elf.set_position(80, 120)
elf.set_stay_in_screen(True)
controller.move_sprite(elf, 100, 0)

#food sprite
def on_update_interval():
    gingerbread = sprites.create(img("""..."""), SpriteKind.food)
    gingerbread.set_position(randint(0, 160), 0)
    gingerbread.set_velocity(0, 50)
game.on_update_interval(1500, on_update_interval)
```

## Challenge: Add a falling Enemy!

Use what you just learned as you created a falling Food sprite to create an Enemy sprite the exact same way! 

Try changing the ``||sprites:set_velocity||`` and ``||game:interval parameter||`` values to make the Enemy sprite appear and move at a different rate than the Food sprite.

---

**Hints!**

💡 Where can you find the code for the ``||game:on_update_interval||`` loop? Where in the code can you change the interval parameter?

💡 What x and y values should you set for the Enemy sprite's position?

💡 What vx and vy values should you set for the Enemy sprite's velocity?

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

## Collect the falling sprites!

Destroy the Food and Enemy sprites when they overlap the Player sprite!

- :paper plane: Using the ``||sprites:on_overlap||`` code from the menu or the code completion tool, create 2 different functions: 1 for the Player and Enemy overlap and 1 for the Player and Food overlap.
- :paper plane: Inside each overlap function, delete "pass" then type ``||sprites:sprites.destroy||`` to remove the falling sprite when it overlaps the Player sprite.
- :paper plane: Replace ``||sprites:mySprite||`` inside the parentheses with the ``||sprites:otherSprite||`` parameter from the ``||sprites:on_overlap||`` function. This will now destroy *any* Food or Enemy sprite that overlaps the Player sprite.
- :play: Click the Play button to test the overlap function code on both Food and Enemy sprites before moving on to the next step.

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo")

```python
scene.set_background_image(img("""..."""))

#player sprite
elf = sprites.create(img("""..."""), SpriteKind.player)
elf.set_position(80, 120)
elf.set_stay_in_screen(True)
controller.move_sprite(elf, 100, 0)

#food sprite
def on_update_interval():
    gingerbread = sprites.create(img("""..."""), SpriteKind.food)
    gingerbread.set_position(randint(0, 160), 0)
    gingerbread.set_velocity(0, 50)
game.on_update_interval(1500, on_update_interval)

#enemy sprite
def on_update_interval2():
    snowball = sprites.create(img("""..."""), SpriteKind.enemy)
    snowball.set_position(randint(0, 160), 0)
    snowball.set_velocity(0, 50)
game.on_update_interval(2000, on_update_interval2)

#overlap code
def on_overlap(sprite, otherSprite):
    sprites.destroy(otherSprite)
sprites.on_overlap(SpriteKind.player, SpriteKind.food, on_overlap)

def on_overlap2(sprite, otherSprite):
    sprites.destroy(otherSprite)
sprites.on_overlap(SpriteKind.player, SpriteKind.enemy, on_overlap2)
```

## Add a score to the game!

Use MakeCode Arcade's built-in score variable to keep track of how many Food sprites the Player sprite catches!

---

- :id card: At the top of the code editor, below the code that sets the background image, type ``||info:info||`` and a dot operator ``||info:.||`` followed by ``||info:set_score||``. This will set the score to 0 and place the score label in the upper right part of the screen.
- :id card: Inside the Player / Food ``||sprites:on_overlap||`` function, under the ``||sprites:destroy||`` code, type ``||info:info||`` and a dot operator ``||info:.||`` followed by ``||info:change_score_by||``. 
- :play: Click the Play button to test the score feature, ensuring it increases each time the Player sprite catches a Food sprite!

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

```python
scene.set_background_image(img("""..."""))

#variable initialization
info.set_score(0)

#player sprite
elf = sprites.create(img("""..."""), SpriteKind.player)
elf.set_position(80, 120)
elf.set_stay_in_screen(True)
controller.move_sprite(elf, 100, 0)

#food sprite
def on_update_interval():
    gingerbread = sprites.create(img("""..."""), SpriteKind.food)
    gingerbread.set_position(randint(0, 160), 0)
    gingerbread.set_velocity(0, 50)
game.on_update_interval(1500, on_update_interval)

#enemy sprite
def on_update_interval2():
    snowball = sprites.create(img("""..."""), SpriteKind.enemy)
    snowball.set_position(randint(0, 160), 0)
    snowball.set_velocity(0, 50)
game.on_update_interval(2000, on_update_interval2)

#overlap code
def on_overlap(sprite, otherSprite):
    sprites.destroy(otherSprite)
    info.change_score_by(1)
sprites.on_overlap(SpriteKind.player, SpriteKind.food, on_overlap)

def on_overlap2(sprite, otherSprite):
    sprites.destroy(otherSprite)
sprites.on_overlap(SpriteKind.player, SpriteKind.enemy, on_overlap2)
```
## Challenge: Add Player life to the game!

Use what you just learned as you set and changed the score in the game to set and change the Player's life when overlapping with an Enemy sprite!

---

**Hints!**

💡 Look in the same category for the life code as you did for the score code!

💡 Set the Player's life where you set the score.

💡 Change the Player's life in the function that makes something happen when the Player and Enemy overlap.

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

## Add sound effects!

Add different sound effects that will play when the Player catches a Food or Enemy sprite!

---

- :headphones: Inside the Player / Food ``||sprites:on_overlap||`` function, under the ``||sprites:destroy||`` and ``||info:change_score_by||`` code, drag in this code from the ``||music:Music||`` menu: ![Block](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/play%20sound%20block.png?raw=true "sound block image")
- :headphones: Highlight this code to copy it, then paste it inside the Player / Enemy ``||sprites:on_overlap||`` function, under the ``||sprites:destroy||`` and ``||info:change_life_by||`` code. Delete ``||music:ba_ding||`` to replace it with a different sound effect.
- :play: Click the Play button to test the sound effects. Tinker with the sounds until you are happy with them.

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

```python
scene.set_background_image(img("""..."""))

#variable initialization
info.set_score(0)
info.set_life(3)

#player sprite
elf = sprites.create(img("""..."""), SpriteKind.player)
elf.set_position(80, 120)
elf.set_stay_in_screen(True)
controller.move_sprite(elf, 100, 0)

#food sprite
def on_update_interval():
    gingerbread = sprites.create(img("""..."""), SpriteKind.food)
    gingerbread.set_position(randint(0, 160), 0)
    gingerbread.set_velocity(0, 50)
game.on_update_interval(1500, on_update_interval)

#enemy sprite
def on_update_interval2():
    snowball = sprites.create(img("""..."""), SpriteKind.enemy)
    snowball.set_position(randint(0, 160), 0)
    snowball.set_velocity(0, 50)
game.on_update_interval(2000, on_update_interval2)

#overlap code
def on_overlap(sprite, otherSprite):
    sprites.destroy(otherSprite)
    info.change_score_by(1)
    music.play(music.melody_playable(music.ba_ding), music.PlaybackMode.UNTIL_DONE)
sprites.on_overlap(SpriteKind.player, SpriteKind.food, on_overlap)

def on_overlap2(sprite, otherSprite):
    sprites.destroy(otherSprite)
    info.change_life_by(-1)
    music.play(music.melody_playable(music.power_down), music.PlaybackMode.UNTIL_DONE)
sprites.on_overlap(SpriteKind.player, SpriteKind.enemy, on_overlap2)
```

## End the game when the Player collects enough Food!

There's no way to win the game unless you add code to end at a certain score!

---

- :id card: Drag this code from the ``||info:Info||`` category underneath the existing code in the editor: ![Block](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/run%20code%20on%20score.png?raw=true "code block")
- :id card: Change the value in the parameter to the score you want to end the game at.
- :circle: Inside, add code from ``||game:Game||`` to end the game in a "win" when the Player reaches that score.
- :circle: Explore other code from ``||game:Game||`` that can be used to customize the game over screen. Be sure to add this code before the ``||game:game_over||`` function!

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo")

```python
scene.set_background_image(img("""..."""))

#variable initialization
info.set_score(0)
info.set_life(3)

#player sprite
elf = sprites.create(img("""..."""), SpriteKind.player)
elf.set_position(80, 120)
elf.set_stay_in_screen(True)
controller.move_sprite(elf, 100, 0)

#food sprite
def on_update_interval():
    gingerbread = sprites.create(img("""..."""), SpriteKind.food)
    gingerbread.set_position(randint(0, 160), 0)
    gingerbread.set_velocity(0, 50)
game.on_update_interval(1500, on_update_interval)
def on_score():
    game.set_game_over_effect(True, effects.blizzard)
    game.game_over(True)
info.on_score(20, on_score)

#enemy sprite
def on_update_interval2():
    snowball = sprites.create(img("""..."""), SpriteKind.enemy)
    snowball.set_position(randint(0, 160), 0)
    snowball.set_velocity(0, 50)
game.on_update_interval(2000, on_update_interval2)

#overlap code
def on_overlap(sprite, otherSprite):
    sprites.destroy(otherSprite)
    info.change_score_by(1)
    music.play(music.melody_playable(music.ba_ding), music.PlaybackMode.UNTIL_DONE)
sprites.on_overlap(SpriteKind.player, SpriteKind.food, on_overlap)

def on_overlap2(sprite, otherSprite):
    sprites.destroy(otherSprite)
    info.change_life_by(-1)
    music.play(music.melody_playable(music.power_down), music.PlaybackMode.UNTIL_DONE)
sprites.on_overlap(SpriteKind.player, SpriteKind.enemy, on_overlap2)
```

## Finishing your game!

Congratulations! You just finished the Day 2 code along!

Get ready because you are now going to use everything you just learned to create your own original project using Python!

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo")

```package
winterImg=github:Code-Ninjas-Home-Office/winter-assets-image-pack
```
