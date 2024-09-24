# Polar Programming with Python: Day 4
### @diffs true

```python
# game initialization
scene.set_background_image(img("""..."""))
game.splash("Oh no!", "Santa lost his presents!")
game.splash("Collect all the presents", "before the time runs out!")
game.splash("Avoid the milk and cookies", "they take away time!")
tiles.set_current_tilemap(tilemap("""level"""))
info.start_countdown(30)

# player sprite
player_sprite = sprites.create(assets.image, SpriteKind.player)
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
    player_sprite.set_image(img("""..."""))
controller.right.on_event(ControllerButtonEvent.PRESSED, on_right_pressed)

def on_left_pressed():
    player_sprite.set_image(img("""..."""))
controller.left.on_event(ControllerButtonEvent.PRESSED, on_left_pressed)

# food sprites
for value in tiles.get_tiles_by_type(assets.tile("""...""")):
    present_sprite = sprites.create(img("""..."""), SpriteKind.food)
    tiles.place_on_tile(present_sprite, value)
    tiles.set_tile_at(value, assets.tile("""transparency16"""))

# enemy sprites
for value2 in tiles.get_tiles_by_type(assets.tile("""...""")):
    cookie_sprite = sprites.create(img("""..."""), SpriteKind.enemy)
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
scene.on_overlap_tile(SpriteKind.player, assets.tile("""..."""), on_overlap_tile)
```

```assetjson
{
  "README.md": " ",
  "assets.json": "",
  "images.g.jres": "{\n    \"*\": {\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"dataEncoding\": \"base64\",\n        \"namespace\": \"myImages\"\n    }\n}",
  "images.g.ts": "// Auto-generated code. Do not edit.\nnamespace myImages {\n\n    helpers._registerFactory(\"image\", function(name: string) {\n        switch(helpers.stringTrim(name)) {\n\n        }\n        return null;\n    })\n\n    helpers._registerFactory(\"animation\", function(name: string) {\n        switch(helpers.stringTrim(name)) {\n\n        }\n        return null;\n    })\n\n    helpers._registerFactory(\"song\", function(name: string) {\n        switch(helpers.stringTrim(name)) {\n\n        }\n        return null;\n    })\n\n}\n// Auto-generated code. Do not edit.\n",
  "main.blocks": "<xml xmlns=\"https://developers.google.com/blockly/xml\"><variables><variable type=\"KIND_SpriteKind\" id=\"%1cxk5^N?w`0^]h2:LA]\">Player</variable><variable type=\"KIND_SpriteKind\" id=\"~tE=AAwq8iv;#+)7E5dt\">Projectile</variable><variable type=\"KIND_SpriteKind\" id=\"Kxp@B-Hm:!vfuqR;aIMP\">Food</variable><variable type=\"KIND_SpriteKind\" id=\"]^CCZXnDYCa/4-UJ;J5W\">Enemy</variable><variable id=\"Bgc~yCg/Qs#iH/XyK`kS\">mySprite</variable><variable id=\"]7T/=j5H%kB#*+f}`exb\">boyList</variable><variable id=\"1659GMM*@jt*E@Hx9M.C\">value</variable><variable id=\"P+2A|]}u5VbCdXdGsQfq\">girlList</variable><variable id=\"rdTD!8lUGhPK^$(dU]+R\">elfList</variable><variable id=\"LX1i:qkLf76kMn_8o:r)\">santaList</variable><variable id=\"2A|=da*yhay_YfFY#T,4\">penguinList</variable><variable id=\"4Cp$P72`Z*AmE=VF~;AL\">bearList</variable><variable id=\"6CH+7F`ubVk$M@){Y0m7\">presentList</variable><variable id=\"C=X`R;%|ORLbF]b1PC=t\">itemList</variable><variable id=\"O.@fqw^~muj{M+`rE@xx\">giftList</variable><variable id=\"o6[%?X.pMwvn@|;KiHzn\">milkList</variable><variable id=\"0f;CqH);oMxngR$.(Rg}\">largeItemList</variable></variables><block type=\"pxt-on-start\" x=\"0\" y=\"0\"></block></xml>",
  "main.py": "\n",
  "main.ts": "\n",
  "pxt.json": "{\n    \"name\": \"JSON Winter Assets Tiles\",\n    \"description\": \"\",\n    \"dependencies\": {\n        \"device\": \"*\"\n    },\n    \"files\": [\n        \"main.blocks\",\n        \"main.ts\",\n        \"README.md\",\n        \"assets.json\",\n        \"images.g.jres\",\n        \"images.g.ts\",\n        \"tilemap.g.jres\",\n        \"tilemap.g.ts\",\n        \"main.py\"\n    ],\n    \"targetVersions\": {\n        \"branch\": \"v1.12.46\",\n        \"tag\": \"v1.12.46\",\n        \"commits\": \"https://github.com/microsoft/pxt-arcade/commits/e66fb08db35df2249cd64300195259c64d497106\",\n        \"target\": \"1.12.46\",\n        \"pxt\": \"8.5.57\"\n    },\n    \"preferredEditor\": \"pyprj\"\n}\n",
  "tilemap.g.jres": "{\n    \"tile1\": {\n        \"data\": \"hwQQABAAAAAREYERERERERERERkRERERGREREREREYERERERERERmBEREREREREREREREREREREREREZERERERERERkRERERERERERERERERERERERERERERERERERkREREREYERkRERGRERmBEREZEREREZERERkRERERERERGBERgREREREQ==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"snow0\"\n    },\n    \"tile2\": {\n        \"data\": \"hwQQABAAAAAYEREREREREZERERkREZERERERkRERgRERERERERERGREREREREREREREREREREREREREREREREREREREREREREREREREREREYERERERERkRERERERkREREREREREYERERGREREREREZERERERERERkRERERERERGBEREZEREREQ==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"snow1\"\n    },\n    \"tile3\": {\n        \"data\": \"hwQQABAAAACREREZERERERgREREREREREZGYmJiYmJgRgY2NjY2NjRGR2N3d3d3dEYHd3d3d0d0Rkdjd293d3RGB3b3R3d27EZHY3d293bsYgd3d3d3d3RGR2B3d3d3dEYHd3d3d3d0Rkdjd3R3b2xGB3d3dvd3dEZHYHd293d0Rgd0d0d3dHQ==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"snowPath0\"\n    },\n    \"tile4\": {\n        \"data\": \"hwQQABAAAAARgd3d3d3d3RGR2N3d3d3dEYHd3d290d0Rkdjd3d3b3RGB3d3d3d3dEZHY3d3d3REYgd3d3d3dERGR2N3d3d3bEYHdvdHd3d0Rkdjd293d3RGB3d3d3d3dEZHY3d3d3d0RgY2NjY2NjRGRmJiYmJiYGBERERERERGREREZEREREQ==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"snowPath1\"\n    },\n    \"tile5\": {\n        \"data\": \"hwQQABAAAADd3d3d3d2NEd3d3d3d3ZgR3d3dvd3djRHd3d3R3d2YEd293d3d3Y0R3Rvd3d3dmBHd3d3d3d2NEd3d3d3d3ZgR3d3d3b3djRHd3d3d292YEd3d3R3d3Y2R3d3d3d3dmBGNjY2NjY2NEZiYmJiYmJgRERERERERERERERERERERkQ==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"snowPath2\"\n    },\n    \"tile6\": {\n        \"data\": \"hwQQABAAAAARERGBERERmBERERERERERmJiYmJiYmBGNjY2NjY2NEd3d3d3d3ZgR293d3d3djRHd3dHd0d2Ykd0d3d293Y0R3d3d3d3dmJHd3d3d3d2NEd0b3d3d3ZgR3b3d3d3djRHd3d0R3dGYEd3d3Rvd3Y0R3d3d3d3dmBEd3d3d3dGNEQ==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"snowPath3\"\n    },\n    \"tile7\": {\n        \"data\": \"hwQQABAAAAARERERERERERERERERERERmJiYmJiYmJiNjY2NjY2Njd3d3d3d3d3d3d3dvd3dvd3d3d0b3d0d2x3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d0d0d293d3d3R3R3b3R3dvd3d3d3dvd3d3d3d3d3d3d3dvdHd3d3d3du93d3d3b3Q==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"snowPath4\"\n    },\n    \"tile8\": {\n        \"data\": \"hwQQABAAAADdHd3d3d3d3d3d0d3R3d293d3d3d3d3dHd3d3d3dvd292x3d290d3d3Rvd3d3d3d3d293d3d3d3d3d3d3d3d3d3d3d3d3du93dHd293d273d3d3b3d3d3d3d3d3d3d3d2NjY2NjY2NjZiYmJiYmJiYEREREREREREREREREREREQ==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"snowPath5\"\n    },\n    \"tile9\": {\n        \"data\": \"hwQQABAAAAARgd3d0d0d2xGR2N3dHd3dEYHd3d3d3d0Rkdix3d3d3RGB3dvd3d3dEZHY3d3dvd0Rgd3d3d3d3RGR2N0d293dEYHd3b3R3d0Rkbjb3d293RGBvdHd3d3REZHY3d3dvd0Rgd3d3d3d3RGR2B3R3d3dEYHdHdvdvd0Rkdjd3d3d3Q==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"snowPath6\"\n    },\n    \"tile10\": {\n        \"data\": \"hwQQABAAAAC90d3dHdGYEd293dEd0Y0R3d3d3d3dmBHd3d3d3d2NEd3d3b3d3ZgR3R3R3d3djRHdHdHd3d2YER3d3d3d3Y0R3d3d3R3bmBHd3d3R3d2NEd3d3d3d3ZgRu93d3d3djRG73dvd3d2YEd3dsdvd3Y0R3d3d3R3dmBHd3d3d3d2NEQ==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"snowPath7\"\n    },\n    \"tile11\": {\n        \"data\": \"hwQQABAAAACREREZERERERgRERERERERERGIiIiIiIgRgZGZmZmZmRGBGZmZmZmREYGZmZmZmRkRgZmZGRmZmRGBmZmZkZGZEYGZmZmZmZkYgZmZmZmZmRGBGRmZmZmZEYGZkZGZmZkRgZmZmZmZmRGBmZmZmZmZEYGRmZmRmZkRgRmZmRmZmQ==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"snowPath8\"\n    },\n    \"tile12\": {\n        \"data\": \"hwQQABAAAAARgZGZmZmZmRGBGZmZmZmZEYGZmZmZkZkRgZmZmZkZmRGBmZmZmZmREYGZmZmZmZkYgZmZmZmZmRGBmZmZmZmZEYGZmRGZmZkRgZmZGZmZmRGBmZmZmZmZEYGZmZmZmZkRgZGZmZmZmRERiIiIiIiIGBERERERERGREREZEREREQ==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"snowPath9\"\n    },\n    \"tile14\": {\n        \"data\": \"hwQQABAAAAAREREYERGRGBEREZERERERiIiIiIiIGBGZmZmZmRmJEZmZmZmZmYERmZmZmZmZiRGZmZmZkZmJEZmZmZkZmYkRmZmZmZmZiZGZmZmZmZmJEZmZmZmZmYkRmZmRmZmZiRGZmRmZmZmJEZGZmZGZmYkRGZmZmZkZiRGZmZmZmZmBEQ==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"snowPath11\"\n    },\n    \"tile13\": {\n        \"data\": \"hwQQABAAAACZmZmZmZmJEZmZmZmZmYkRmZmZmZGRiRGZmZmZGRmJEZmRmZmZmYERmRmZmZmZiRGZmZmZmZmJEZmZmZmZmYmRmZmZmZGZiRGZmZmZGZmJEZGZmZmZmYkRGZmZmZmZiRGZmZmZmZmJEYiIiIiIiBgRERERkREREREREREYERGRGA==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"snowPath10\"\n    },\n    \"tile17\": {\n        \"data\": \"hwQQABAAAAARgZmZmZmZmRGBmZmZmZmREYGZGZmZmRkRgZmZkZmZmRGBmZmZmZmZEYGZmZkZmZkZgZmZmZmRmZGBmZmZmZmZEYGZmZmZmZkRgZmRmZmZmRGBmZmZmZmZEYGZmZmRmZkRgZmZmRmZGRmBmZmZmZmZEYGZGZmZmZkRgZmZkZmZmQ==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"snowPath12\"\n    },\n    \"tile18\": {\n        \"data\": \"hwQQABAAAACZmZmZmZmJEZmZmZmZmYkRmZmZmZmZiRGZmRkZmZmJEZmZmZGRmYkRkZmZmRmZiREZmZmZmZmJEZmZmZmZmYmRmZmZmZmZiRGZmZmZmZmJEZmZGZmZmYkRmZmZkZmZiRGZmZmZmZmJEZmRmZmZkYkRmRmZmZmRiRGZmZmZmRmJGQ==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"snowPath13\"\n    },\n    \"tile19\": {\n        \"data\": \"hwQQABAAAAARGRERERERERERkRERERERiIiIiIiIiIiZGZmZmZmZmZmZkZmZmZmZmZmZmZkZmZmZmZmZmZmRmZmZmZGRmZmZmZmZGZmZmZmZmZmZmZmZmZmZmZmZmZmZmRmZmZmZmZmZmZGZmZmZmZmZmZmZmZmZmZmZmZmRmZmZmZmZmRmZmQ==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"snowPath14\"\n    },\n    \"tile20\": {\n        \"data\": \"hwQQABAAAACZmZmRmZmZmZmZmRmZmZGZkZmZmZmZGZkZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZGZmZmZmZmZGRmZmZGZmZmZkZGZGZmZmZmZmZmZmZmRmZmZmZmZmRmZmZmZmZmZmZmZmZmZmYiIiIiIiIiIEREREREREREREREREREREQ==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"snowPath15\"\n    },\n    \"tile16\": {\n        \"data\": \"hwQQABAAAADd3d3d3d3d3d3d3d3d3d3d3d29Hd3d3d3d3b3d3R3b3d3d3d3dvd3d3dHd3d3d3d3d3d3d3d3d3d3d3d3d3d3d3d3dHdHdHd3d3d0d0d3d3d29293d3d3d3b3b3d3d3d3d3d3dvd3d3d3d3d3d3d3b3d3d3d3d3d3d3d3d3d3d3Q==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"snowPath16\"\n    },\n    \"tile15\": {\n        \"data\": \"hwQQABAAAAARERERERgREREYERGBiRERERGBEYGJERkREZgYERgRgRERmBgRERERERGBERGBEREREREREZgYERERERgRmBgRkRGBiRGBEREYEYGJERERERERERgRGBEREREREYGJEREREYERgYkRERERmBgRGBGRERmYGBERERgREYEREREREQ==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"snowPath17\"\n    },\n    \"tile21\": {\n        \"data\": \"hwQQABAAAAAREYERERERERERmBgREYkRkRGYGBEYERERGIERgYkRERERERGBiREREREYEREYERERgYkRERERERGBiRGBEREREREYEZgYERkRERERmBgRERERgRGBERERERGYGBEREREREZgYERgRERERgRGBiRERgREREYGJkRERERERERgREQ==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"snowPath18\"\n    },\n    \"tile22\": {\n        \"data\": \"hwQQABAAAAAREREREREREREREREZERERgRERERERERmRERERERERERGBGBEREYEYEZiJEYgRmIkRgRiBmRiBGBERERGIERERERERERERERGBGBEREYEYEZiJEYgRmIkRgRiBmRiBGBERERGIERERERGBERERERERERkRERERERgREREREREREQ==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"snowPath19\"\n    },\n    \"tile23\": {\n        \"data\": \"hwQQABAAAAAREREREREREREZEREREREYEYERERERERERERGIEREREYEYgZkYgRgRmIkRiBGYiRGBGBEREYEYEREREREREREREREREYgRERERgRiBmRiBGBGYiRGIEZiJEYEYERERgRiREREREREREYEREREREREZERERERkREREREREREREREQ==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"snowPath20\"\n    },\n    \"tile24\": {\n        \"data\": \"hwQQABAAAAAREREREREREZERERGBGBGBGBEREZiJERkRERERgYkRERERgRERGBERERGYGBEREREREZiJERGIERERgRgRgZkYERERERERmBgRERERgRGBERERERGYGBEREREREZiJEZERERERgRgRGRGBERERERERERkRERERERERERERERGREQ==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"snowPath21\"\n    },\n    \"tile25\": {\n        \"data\": \"hwQQABAAAAARERERERGREREZEREREREREYERERERERERERERgRgRGRERERGYiRGREREREZgYERERERERgRGBEREREREREZgYERGBGBGBmRgREZiJERGIERERmBgRERERERGBEREYERERERERgYkRERgRERGYiREZkREREYEYEYEREREREREREQ==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"snowPath22\"\n    },\n    \"tile26\": {\n        \"data\": \"hwQQABAAAACREREREREREREREYEYERERERERmIkRERERERGYGBERGREREYERgRGRERERERGYGBERgRgRgZkYERGYiRERiBEREZgYERERERERgRERGBEREREREYGJERERERERmIkRGRERERGBGBERERgRERERERGRkREREREREYEREREREREREQ==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"snowPath23\"\n    },\n    \"tile27\": {\n        \"data\": \"hwQQABAAAAARGREREREREREREREREZERERERERERGBGREYEYERERERkRmIkRERERERGBiRERERERGBEYEREREYGJERERERERgZkYEYEYERERiBERmIkRERERERGBiRERERGBEREYEREREZgYEREREZERmIkRERGBGBGBGBERERkREREREREREQ==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"snowPath24\"\n    },\n    \"tile28\": {\n        \"data\": \"hwQQABAAAAARkZmZGRERERERiYiYERERGREREREZEREYEREREZEREYEZGZERgREREYEYERmBGREREZEREREZERERERkRERgRERERkRERkRGRERGBERGBEREREYEZEYEZERkRgRmRgRkRGREZERmBEZERERgRERkRERGBGRERmBEREYEZEYEZEQ==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"snowPath25\"\n    },\n    \"tile29\": {\n        \"data\": \"hwQQABAAAAAREYEZEYEZERERgRkREZgRkRERGBERGRERGREZERmBEREZEYEZkYEZERERgRkRgRmRERGBERGBEREREZEREZERERERGRERGBEREZEREREZERGBGBEZgRkRgRkZkRGBEREYEREREZERERkRERERGRERERGJiJgRERERkZmZGREREQ==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"snowPath26\"\n    },\n    \"tile30\": {\n        \"data\": \"hwQQABAAAAARkRgRkRgRERGJERGRGBEREZEREYERERkRGJERkRGREZEYGZEYEZERkRgRkRgRERERGBERGBERGREZEREZEREREYEREZERERERkRERERkRERGRGJERgRgREREYERmRkRgRERkRERERgRERkRERERGRERERiYiYERERERGRmZkZEQ==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"snowPath27\"\n    },\n    \"tile31\": {\n        \"data\": \"hwQQABAAAAARERGRmZkZEREREYmImBERERGREREREZERERkRERERgRERGBEZkZEYEZEYkRGBGBERkRERERkRERGBERGRERERERkRERkRERERGBERGBERGZEYEZEYERERkRgZkRgRkRERGJERkRGRERGRERGBEREZEYkREZEYERERkRgRkRgREQ==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"snowPath28\"\n    },\n    \"tile32\": {\n        \"data\": \"hwQQABAAAAARkRGRERGRERGBEREZERkREYERERgRGBERERkRGBGRERERGBGYEYERkRGREZERERmREYERgRERGBEZERmBGRGRERERGIEZEZERERGYERkRgRERkRERGBGBkRGBERGYEYERGREZERkRgREZEZiRERGBkRGRERkREZERERmRERERGA==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"snowPath29\"\n    },\n    \"transparency16\": {\n        \"data\": \"hwQQABAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true\n    },\n    \"*\": {\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"dataEncoding\": \"base64\",\n        \"namespace\": \"myTiles\"\n    }\n}",
  "tilemap.g.ts": "// Auto-generated code. Do not edit.\nnamespace myTiles {\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile1 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile2 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile3 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile4 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile5 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile6 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile7 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile8 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile9 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile10 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile11 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile12 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile14 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile13 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile17 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile18 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile19 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile20 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile16 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile15 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile21 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile22 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile23 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile24 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile25 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile26 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile27 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile28 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile29 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile30 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile31 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile32 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const transparency16 = image.ofBuffer(hex``);\n\n    helpers._registerFactory(\"tile\", function(name: string) {\n        switch(helpers.stringTrim(name)) {\n            case \"snow0\":\n            case \"tile1\":return tile1;\n            case \"snow1\":\n            case \"tile2\":return tile2;\n            case \"snowPath0\":\n            case \"tile3\":return tile3;\n            case \"snowPath1\":\n            case \"tile4\":return tile4;\n            case \"snowPath2\":\n            case \"tile5\":return tile5;\n            case \"snowPath3\":\n            case \"tile6\":return tile6;\n            case \"snowPath4\":\n            case \"tile7\":return tile7;\n            case \"snowPath5\":\n            case \"tile8\":return tile8;\n            case \"snowPath6\":\n            case \"tile9\":return tile9;\n            case \"snowPath7\":\n            case \"tile10\":return tile10;\n            case \"snowPath8\":\n            case \"tile11\":return tile11;\n            case \"snowPath9\":\n            case \"tile12\":return tile12;\n            case \"snowPath11\":\n            case \"tile14\":return tile14;\n            case \"snowPath10\":\n            case \"tile13\":return tile13;\n            case \"snowPath12\":\n            case \"tile17\":return tile17;\n            case \"snowPath13\":\n            case \"tile18\":return tile18;\n            case \"snowPath14\":\n            case \"tile19\":return tile19;\n            case \"snowPath15\":\n            case \"tile20\":return tile20;\n            case \"snowPath16\":\n            case \"tile16\":return tile16;\n            case \"snowPath17\":\n            case \"tile15\":return tile15;\n            case \"snowPath18\":\n            case \"tile21\":return tile21;\n            case \"snowPath19\":\n            case \"tile22\":return tile22;\n            case \"snowPath20\":\n            case \"tile23\":return tile23;\n            case \"snowPath21\":\n            case \"tile24\":return tile24;\n            case \"snowPath22\":\n            case \"tile25\":return tile25;\n            case \"snowPath23\":\n            case \"tile26\":return tile26;\n            case \"snowPath24\":\n            case \"tile27\":return tile27;\n            case \"snowPath25\":\n            case \"tile28\":return tile28;\n            case \"snowPath26\":\n            case \"tile29\":return tile29;\n            case \"snowPath27\":\n            case \"tile30\":return tile30;\n            case \"snowPath28\":\n            case \"tile31\":return tile31;\n            case \"snowPath29\":\n            case \"tile32\":return tile32;\n            case \"transparency16\":return transparency16;\n        }\n        return null;\n    })\n\n}\n// Auto-generated code. Do not edit.\n"
}
```

## Polar Programming with Python - Day 4! @showdialog

Welcome to your next Python project code along! Today you will be creating a project using everything you have learned so far, plus 2D tilemaps, simple physics, and conditionals! 

Click ``||loops:Ok||`` to get started!

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

## Create a 2D Platformer Tilemap

Create a 2D Platformer tilemap, that is at least 40 tiles wide, for your Player sprite to navigate!

---

- :tree: Type ``||scene:tiles||``, a dot operator ``||scene:.||``, and the ``||scene:set_current_tilemap||`` function. Pressing Tab will insert the ``||scene:(tilemap(""" """))||`` code into the function.
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
scene.set_background_image(img("""..."""))
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
scene.set_background_image(img("""..."""))
tiles.set_current_tilemap(tilemap("""level"""))

# player sprite
player_sprite = sprites.create(img("""..."""), SpriteKind.player)
tiles.place_on_tile(player_sprite, tiles.get_tile_location(0, 6))
controller.move_sprite(player_sprite, 100, 0)
scene.camera_follow_sprite(player_sprite)
```

## Code the Player sprite to jump!

Using simple physics, code the Player sprite to jump up when the A button is pressed, and then be pulled back down to the ground.

---

- :paper plane: Type the Player sprite's name variable, a dot operator, and ``||sprites:ay||`` to set the y-acceleration that will pull the Player sprite down to the ground.
- :paper plane: Use an assignment operator ``||variables:=||`` to set the ``||sprites:ay||`` value to a large positive number, such as **500**.
- :game controller: From ``||controller:Controller||`` drag this code into the editor under the other Player sprite code: ![image](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/button%20event%20code.png?raw=true "button pressed code") It will make something happen when the A button is pressed.
- :game controller: Change the word "event" to "a" in the function definition, then change it inside the parentheses of the function call. 
- :game controller: Replace "pass" with the Player sprite's name variable, a dot operator, and ``||sprites:vy||`` to set the y-velocity that will counteract the y-acceleration and make the Player sprite jump up.
- :game controller: Use an assignment operator ``||variables:=||`` to set the ``||sprites:vy||`` value to a smaller negative number, such as **-200**.
- :play: Click the Play button to test out the sprite jump code!

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

```python
# game initialization
scene.set_background_image(img("""..."""))
tiles.set_current_tilemap(tilemap("""level"""))

# player sprite
player_sprite = sprites.create(img("""..."""), SpriteKind.player)
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
scene.set_background_image(img("""..."""))
tiles.set_current_tilemap(tilemap("""level"""))

# player sprite
player_sprite = sprites.create(img("""..."""), SpriteKind.player)
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
scene.set_background_image(img("""..."""))
tiles.set_current_tilemap(tilemap("""level"""))

# player sprite
player_sprite = sprites.create(img("""..."""), SpriteKind.player)
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
    player_sprite.set_image(img("""..."""))
controller.right.on_event(ControllerButtonEvent.PRESSED, on_right_pressed)

def on_left_pressed():
    player_sprite.set_image(img("""..."""))
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
scene.set_background_image(img("""..."""))
tiles.set_current_tilemap(tilemap("""level"""))

# player sprite
player_sprite = sprites.create(img("""..."""), SpriteKind.player)
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
    player_sprite.set_image(img("""..."""))
controller.right.on_event(ControllerButtonEvent.PRESSED, on_right_pressed)

def on_left_pressed():
    player_sprite.set_image(img("""..."""))
controller.left.on_event(ControllerButtonEvent.PRESSED, on_left_pressed)

# food sprites
for value in tiles.get_tiles_by_type(assets.tile("""...""")):
    present_sprite = sprites.create(img("""..."""), SpriteKind.food)
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
scene.set_background_image(img("""..."""))
tiles.set_current_tilemap(tilemap("""level"""))

# player sprite
player_sprite = sprites.create(img("""..."""), SpriteKind.player)
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
    player_sprite.set_image(img("""..."""))
controller.right.on_event(ControllerButtonEvent.PRESSED, on_right_pressed)

def on_left_pressed():
    player_sprite.set_image(img("""..."""))
controller.left.on_event(ControllerButtonEvent.PRESSED, on_left_pressed)

# food sprites
for value in tiles.get_tiles_by_type(assets.tile("""...""")):
    present_sprite = sprites.create(img("""..."""), SpriteKind.food)
    tiles.place_on_tile(present_sprite, value)
    tiles.set_tile_at(value, assets.tile("""transparency16"""))

# enemy sprites
for value2 in tiles.get_tiles_by_type(assets.tile("""...""")):
    cookie_sprite = sprites.create(img("""..."""), SpriteKind.enemy)
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
scene.set_background_image(img("""..."""))
tiles.set_current_tilemap(tilemap("""level"""))

# player sprite
player_sprite = sprites.create(img("""..."""), SpriteKind.player)
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
    player_sprite.set_image(img("""..."""))
controller.right.on_event(ControllerButtonEvent.PRESSED, on_right_pressed)

def on_left_pressed():
    player_sprite.set_image(img("""..."""))
controller.left.on_event(ControllerButtonEvent.PRESSED, on_left_pressed)

# food sprites
for value in tiles.get_tiles_by_type(assets.tile("""...""")):
    present_sprite = sprites.create(img("""..."""), SpriteKind.food)
    tiles.place_on_tile(present_sprite, value)
    tiles.set_tile_at(value, assets.tile("""transparency16"""))

# enemy sprites
for value2 in tiles.get_tiles_by_type(assets.tile("""...""")):
    cookie_sprite = sprites.create(img("""..."""), SpriteKind.enemy)
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
scene.set_background_image(img("""..."""))
tiles.set_current_tilemap(tilemap("""level"""))

# player sprite
player_sprite = sprites.create(img("""..."""), SpriteKind.player)
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
    player_sprite.set_image(img("""..."""))
controller.right.on_event(ControllerButtonEvent.PRESSED, on_right_pressed)

def on_left_pressed():
    player_sprite.set_image(img("""..."""))
controller.left.on_event(ControllerButtonEvent.PRESSED, on_left_pressed)

# food sprites
for value in tiles.get_tiles_by_type(assets.tile("""...""")):
    present_sprite = sprites.create(img("""..."""), SpriteKind.food)
    tiles.place_on_tile(present_sprite, value)
    tiles.set_tile_at(value, assets.tile("""transparency16"""))

# enemy sprites
for value2 in tiles.get_tiles_by_type(assets.tile("""...""")):
    cookie_sprite = sprites.create(img("""..."""), SpriteKind.enemy)
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
scene.set_background_image(img("""..."""))
tiles.set_current_tilemap(tilemap("""level"""))
info.start_countdown(30)

# player sprite
player_sprite = sprites.create(img("""..."""), SpriteKind.player)
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
    player_sprite.set_image(img("""..."""))
controller.right.on_event(ControllerButtonEvent.PRESSED, on_right_pressed)

def on_left_pressed():
    player_sprite.set_image(img("""..."""))
controller.left.on_event(ControllerButtonEvent.PRESSED, on_left_pressed)

# food sprites
for value in tiles.get_tiles_by_type(assets.tile("""...""")):
    present_sprite = sprites.create(img("""..."""), SpriteKind.food)
    tiles.place_on_tile(present_sprite, value)
    tiles.set_tile_at(value, assets.tile("""transparency16"""))

# enemy sprites
for value2 in tiles.get_tiles_by_type(assets.tile("""...""")):
    cookie_sprite = sprites.create(img("""..."""), SpriteKind.enemy)
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
scene.set_background_image(img("""..."""))
tiles.set_current_tilemap(tilemap("""level"""))
info.start_countdown(30)

# player sprite
player_sprite = sprites.create(img("""..."""), SpriteKind.player)
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
    player_sprite.set_image(img("""..."""))
controller.right.on_event(ControllerButtonEvent.PRESSED, on_right_pressed)

def on_left_pressed():
    player_sprite.set_image(img("""..."""))
controller.left.on_event(ControllerButtonEvent.PRESSED, on_left_pressed)

# food sprites
for value in tiles.get_tiles_by_type(assets.tile("""...""")):
    present_sprite = sprites.create(img("""..."""), SpriteKind.food)
    tiles.place_on_tile(present_sprite, value)
    tiles.set_tile_at(value, assets.tile("""transparency16"""))

# enemy sprites
for value2 in tiles.get_tiles_by_type(assets.tile("""...""")):
    cookie_sprite = sprites.create(img("""..."""), SpriteKind.enemy)
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
scene.on_overlap_tile(SpriteKind.player, assets.tile("""..."""), on_overlap_tile)
```

## Add a splash screen at the beginning!

Use a splash screen to display a message at the beginning of the game, letting the player know how to play your game!

---

- :circle: At the top of the editor, above all other code, type ``||game:game.splash||`` to add a text box that will contain a message.
- :circle: Inside the parentheses, type a short message - known as a **string** - surrounded by quotation marks. Use a comma to type a second **string** to appear in the same message box below the first **string**.
- :circle: Add additional ``||game:game.splash||`` functions to create more on-screen text boxes.

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo")

```python
# game initialization
scene.set_background_image(img("""..."""))
game.splash("Oh no!", "Santa lost his presents!")
game.splash("Collect all the presents", "before the time runs out!")
game.splash("Avoid the milk and cookies", "they take away time!")
tiles.set_current_tilemap(tilemap("""level"""))
info.start_countdown(30)

# player sprite
player_sprite = sprites.create(img("""..."""), SpriteKind.player)
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
    player_sprite.set_image(img("""..."""))
controller.right.on_event(ControllerButtonEvent.PRESSED, on_right_pressed)

def on_left_pressed():
    player_sprite.set_image(img("""..."""))
controller.left.on_event(ControllerButtonEvent.PRESSED, on_left_pressed)

# food sprites
for value in tiles.get_tiles_by_type(assets.tile("""...""")):
    present_sprite = sprites.create(img("""..."""), SpriteKind.food)
    tiles.place_on_tile(present_sprite, value)
    tiles.set_tile_at(value, assets.tile("""transparency16"""))

# enemy sprites
for value2 in tiles.get_tiles_by_type(assets.tile("""...""")):
    cookie_sprite = sprites.create(img("""..."""), SpriteKind.enemy)
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
scene.on_overlap_tile(SpriteKind.player, assets.tile("""..."""), on_overlap_tile)
```

## Finishing your game!

Congratulations! You just finished the Day 4 code along!

Get ready because you are now going to use everything you just learned to create your own original project using Python!

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo")

```package
winterImg=github:Code-Ninjas-Home-Office/winter-assets-image-pack
```
