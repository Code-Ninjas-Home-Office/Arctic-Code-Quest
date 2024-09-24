# Polar Programming with Python: Day 3 
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
playerSprite = sprites.create(winterImg.boyFront, SpriteKind.player)
tiles.place_on_tile(playerSprite, tiles.get_tile_location(1, 18))
controller.move_sprite(playerSprite)
scene.camera_follow_sprite(playerSprite)

#food sprite
for i in range(8):
    candySprite = sprites.create(winterImg.candycane, SpriteKind.food)
    tiles.place_on_random_tile(candySprite, winterTile.snowPath16)

def on_score():
    game.set_game_over_effect(True, effects.smiles)
    game.game_over(True)
info.on_score(10, on_score)

#enemy sprite
for i in range(8):
    enemySprite = sprites.create(winterImg.bearFront, SpriteKind.enemy)
    tiles.place_on_random_tile(enemySprite, winterTile.snowPath16)
    enemySprite.set_velocity(randint(-50,50), randint(-50,50))
    enemySprite.set_bounce_on_wall(True)

#overlap events
def on_overlap(sprite, otherSprite):
    tiles.place_on_random_tile(otherSprite, winterTile.snowPath16)
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
scene.on_overlap_tile(SpriteKind.player, assets.tile"""...""", on_overlap_tile)
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

## Polar Programming with Python - Day 3! @showdialog

Welcome to your next Python project code along! Today you will be creating a project using everything you have learned so far, plus tilemaps, tilemap functions, and for loops! 

Click ``||loops:Ok||`` to get started!

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

## Create a Winter Wonderland Tilemap

Create a maze for your sprites to move about using a tilemap!

---

- :tree: Type ``||scene:tiles||``, a dot operator ``||scene:.||``, and the ``||scene:set_current_tilemap||`` function. Pressing Tab will insert the ``||scene:(tilemap(""" """))||`` code into the function.
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
- :tree: Position the Player sprite on a specific tile location by typing ``||scene:tiles||``, a dot operator ``||scene:.||``, and ``||scene:place_on_tile||``. Replace the first parameter with the Player sprite variable name.
- :tree: Tinker with the tilemap coordinates in ``||scene:tiles.get_tile_location||`` to place the Player sprite on a maze path tile - not on a wall!
- :game controller: Add code to move the Player sprite around the tilemap.
- :tree: Oh no! The Player sprite moves off the tilemap! From ``||scene:Scene||`` use the ``||scene:camera_follow_sprite||`` function to ensure the camera follows the Player sprite around the tilemap.

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

```python
tiles.set_current_tilemap(tilemap("""level"""))

#player sprite
playerSprite = sprites.create(img("""..."""), SpriteKind.player)
tiles.place_on_tile(playerSprite, tiles.get_tile_location(1, 18))
controller.move_sprite(playerSprite)
scene.camera_follow_sprite(playerSprite)
```

## Create Food sprites to collect throughout the maze!

Use a **for loop** to create multiple Food sprites for the Player sprite to collect!

- :repeat: Using the ``||loops:Loops||`` code menu or the code completion tool, add a **for loop** that looks like this: ``||loops:for i in range(8):||``. Don't forget the colon **:** at the end of the statement!
- :paper plane: Indented inside the **for loop**, add code to create a Food sprite.
- :tree: Position the Food sprites on random path tiles throughout the maze by typing ``||scene:tiles||``, a dot operator ``||scene:.||``. and ``||scene:place_on_random_tile||``. Replace the first parameter with the Food sprite variable name.
- :tree:  Click the palette icon or find the tile name from the tilemap editor or Assets tab to use as the tile parameter.
- :play: Click the Play button to test the Food sprite code, ensuring multiple Food sprites are positioned on different tiles throughout the maze. 

*Consider updating your tilemap design if there are not enough tiles of the same kind for all of the Food sprites!*

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

```python
tiles.set_current_tilemap(tilemap("""level"""))

#player sprite
playerSprite = sprites.create(img("""..."""), SpriteKind.player)
tiles.place_on_tile(playerSprite, tiles.get_tile_location(1, 18))
controller.move_sprite(playerSprite)
scene.camera_follow_sprite(playerSprite)

#food sprite
for i in range(8):
    candySprite = sprites.create(img("""..."""), SpriteKind.food)
    tiles.place_on_random_tile(candySprite, assets.tile("""..."""))
```

## Challenge: Create multiple moving Enemy sprites!

Use what you just learned to create multiple Enemy sprites on the tilemap using a **for loop**.

---

**Hints!**

💡 Where can you find the code for the ``||loops:for||`` loop? Where in the code can you change how many times the loop runs?

💡 What function places the sprites on a random tile? Where do you set the sprite kind and tile kind?

---

- :paper plane: Add code to the Enemy sprite's for loop that sets each Enemy sprite's ``||sprites:velocity||`` to random vx and vy values from a range of -50 to 50.
- :paper plane: To ensure Enemy sprites don't get stuck on a tilemap wall, type the Enemy sprite variable name, a ``||sprites:.||``, and a ``||sprites:set_bounce_on_wall||`` function set to True.
- :play: Click the Play button to test the Enemy sprite code, ensuring multiple Enemy sprites are positioned on different tiles and moving throughout the maze. 

*Consider updating your tilemap design if there are not enough tiles of the same kind for all of the Enemy sprites!*

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

```python
tiles.set_current_tilemap(tilemap("""level"""))

#player sprite
playerSprite = sprites.create(img("""..."""), SpriteKind.player)
tiles.place_on_tile(playerSprite, tiles.get_tile_location(1, 18))
controller.move_sprite(playerSprite)
scene.camera_follow_sprite(playerSprite)

#food sprite
for i in range(8):
    candySprite = sprites.create(img("""..."""), SpriteKind.food)
    tiles.place_on_random_tile(candySprite, assets.tile("""..."""))

#enemy sprite
for i in range(8):
    enemySprite = sprites.create(img("""..."""), SpriteKind.enemy)
    tiles.place_on_random_tile(enemySprite, assets.tile("""..."""))
    enemySprite.set_velocity(randint(-50,50), randint(-50,50))
    enemySprite.set_bounce_on_wall(True)
```

## Add sprite overlap events!

Make something happen when the Player sprite overlaps the Food and Enemy sprites.

- :paper plane: Using the ``||sprites:on_overlap||`` code from the menu or the code completion tool, create 2 different functions: 1 for the Player and Enemy overlap and 1 for the Player and Food overlap.
- :paper plane: Inside the **Player/Enemy** overlap function, delete "pass" then type ``||sprites:sprites.destroy||`` to remove the Enemy sprite when it overlaps the Player sprite.
- :paper plane: Replace ``||sprites:mySprite||`` inside the parentheses with the ``||sprites:otherSprite||`` parameter from the ``||sprites:on_overlap||`` function. This will now destroy *any* Enemy sprite that overlaps the Player sprite.
- :tree: Inside the **Player/Food** overlap function, delete "pass" then type ``||scene:tiles.place_on_random_tile||`` to move the Food sprite to a different tile.
- :paper plane: Replace **none** inside the parentheses with the ``||sprites:otherSprite||`` parameter from the ``||sprites:on_overlap||`` function. This will now reposition *any* Food sprite that overlaps the Player sprite.
- :play: Click the Play button to test the overlap function code on both Food and Enemy sprites before moving on to the next step.

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo")

```python
tiles.set_current_tilemap(tilemap("""level"""))

#player sprite
playerSprite = sprites.create(img("""...""")), SpriteKind.player)
tiles.place_on_tile(playerSprite, tiles.get_tile_location(1, 18))
controller.move_sprite(playerSprite)
scene.camera_follow_sprite(playerSprite)

#food sprite
for i in range(8):
    candySprite = sprites.create(img("""...""")), SpriteKind.food)
    tiles.place_on_random_tile(candySprite, assets.tile("""..."""))

#enemy sprite
for i in range(8):
    enemySprite = sprites.create(img("""..."""), SpriteKind.enemy)
    tiles.place_on_random_tile(enemySprite, assets.tile("""..."""))
    enemySprite.set_velocity(randint(-50,50), randint(-50,50))
    enemySprite.set_bounce_on_wall(True)

#overlap events
def on_overlap(sprite, otherSprite):
    tiles.place_on_random_tile(otherSprite, assets.tile("""..."""))
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
playerSprite = sprites.create(img("""..."""), SpriteKind.player)
tiles.place_on_tile(playerSprite, tiles.get_tile_location(1, 18))
controller.move_sprite(playerSprite)
scene.camera_follow_sprite(playerSprite)

#food sprite
for i in range(8):
    candySprite = sprites.create(img("""..."""), SpriteKind.food)
    tiles.place_on_random_tile(candySprite, assets.tile("""..."""))

#enemy sprite
for i in range(8):
    enemySprite = sprites.create(img("""..."""), SpriteKind.enemy)
    tiles.place_on_random_tile(enemySprite, assets.tile("""..."""))
    enemySprite.set_velocity(randint(-50,50), randint(-50,50))
    enemySprite.set_bounce_on_wall(True)

#overlap events
def on_overlap(sprite, otherSprite):
    tiles.place_on_random_tile(otherSprite, assets.tile("""..."""))
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
playerSprite = sprites.create(img("""..."""), SpriteKind.player)
tiles.place_on_tile(playerSprite, tiles.get_tile_location(1, 18))
controller.move_sprite(playerSprite)
scene.camera_follow_sprite(playerSprite)

#food sprite
for i in range(8):
    candySprite = sprites.create(img("""..."""), SpriteKind.food)
    tiles.place_on_random_tile(candySprite, assets.tile("""..."""))

#enemy sprite
for i in range(8):
    enemySprite = sprites.create(img("""..."""), SpriteKind.enemy)
    tiles.place_on_random_tile(enemySprite, assets.tile("""..."""))
    enemySprite.set_velocity(randint(-50,50), randint(-50,50))
    enemySprite.set_bounce_on_wall(True)

#overlap events
def on_overlap(sprite, otherSprite):
    tiles.place_on_random_tile(otherSprite, assets.tile("""..."""))
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
scene.on_overlap_tile(SpriteKind.player, assets.tile("""..."""), on_overlap_tile)
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
playerSprite = sprites.create(img("""..."""), SpriteKind.player)
tiles.place_on_tile(playerSprite, tiles.get_tile_location(1, 18))
controller.move_sprite(playerSprite)
scene.camera_follow_sprite(playerSprite)

#food sprite
for i in range(8):
    candySprite = sprites.create(img("""..."""), SpriteKind.food)
    tiles.place_on_random_tile(candySprite, assets.tile("""..."""))

#enemy sprite
for i in range(8):
    enemySprite = sprites.create(img("""..."""), SpriteKind.enemy)
    tiles.place_on_random_tile(enemySprite, assets.tile("""..."""))
    enemySprite.set_velocity(randint(-50,50), randint(-50,50))
    enemySprite.set_bounce_on_wall(True)

#overlap events
def on_overlap(sprite, otherSprite):
    tiles.place_on_random_tile(otherSprite, assets.tile("""..."""))
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
scene.on_overlap_tile(SpriteKind.player, assets.tile("""..."""), on_overlap_tile)
```

## Add a splash screen at the beginning!

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
playerSprite = sprites.create(img("""..."""), SpriteKind.player)
tiles.place_on_tile(playerSprite, tiles.get_tile_location(1, 18))
controller.move_sprite(playerSprite)
scene.camera_follow_sprite(playerSprite)

#food sprite
for i in range(8):
    candySprite = sprites.create(img("""..."""), SpriteKind.food)
    tiles.place_on_random_tile(candySprite, assets.tile("""..."""))

#enemy sprite
for i in range(8):
    enemySprite = sprites.create(img("""..."""), SpriteKind.enemy)
    tiles.place_on_random_tile(enemySprite, assets.tile("""..."""))
    enemySprite.set_velocity(randint(-50,50), randint(-50,50))
    enemySprite.set_bounce_on_wall(True)

#overlap events
def on_overlap(sprite, otherSprite):
    tiles.place_on_random_tile(otherSprite, assets.tile("""..."""))
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
scene.on_overlap_tile(SpriteKind.player, assets.tile("""..."""), on_overlap_tile)
```

## Finishing your game!

Congratulations! You just finished the Day 3 code along!

Get ready because you are now going to use everything you just learned to create your own original project using Python!

![Logo](https://github.com/Code-Ninjas-Home-Office/arctic-code-quest/blob/master/images/CN-Logo.png?raw=true "CN Logo")

```package
winterImg=github:Code-Ninjas-Home-Office/winter-assets-image-pack
```
