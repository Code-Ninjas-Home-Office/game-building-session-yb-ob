# Code Ninjas Yellow Belt GBS

```blocks
scene.onOverlapTile(SpriteKind.Player, assets.tile`myTile`, function (sprite, location) {
    if (info.score() == 3) {
        game.gameOver(true)
    } else {
        game.showLongText("You need more coins!", DialogLayout.Center)
    }
    pause(1000)
})
scene.onOverlapTile(SpriteKind.Player, sprites.dungeon.hazardWater, function (sprite, location) {
    sprites.destroy(sprite)
    music.play(music.melodyPlayable(music.jumpDown), music.PlaybackMode.InBackground)
    scene.cameraShake(4, 500)
    tiles.placeOnRandomTile(hero, sprites.castle.tileDarkGrass3)
})
sprites.onOverlap(SpriteKind.Player, SpriteKind.Food, function (sprite, otherSprite) {
    sprites.destroy(otherSprite)
    info.changeScoreBy(1)
    music.play(music.melodyPlayable(music.baDing), music.PlaybackMode.InBackground)
})
sprites.onOverlap(SpriteKind.Player, SpriteKind.Enemy, function (sprite, otherSprite) {
    sprites.destroy(otherSprite)
    info.changeLifeBy(-1)
    music.play(music.melodyPlayable(music.knock), music.PlaybackMode.InBackground)
    scene.cameraShake(4, 500)
    tiles.placeOnRandomTile(hero, sprites.castle.tileDarkGrass3)
})
let enemySprite: Sprite = null
let coin: Sprite = null
let mySprite: Sprite = null
tiles.setCurrentTilemap(tilemap`level1`)
info.startCountdown(10)
game.splash("")
mySprite = sprites.create(img`
    . . . . . . f f f f . . . . . . 
    . . . . f f f 2 2 f f f . . . . 
    . . . f f f 2 2 2 2 f f f . . . 
    . . f f f e e e e e e f f f . . 
    . . f f e 2 2 2 2 2 2 e e f . . 
    . . f e 2 f f f f f f 2 e f . . 
    . . f f f f e e e e f f f f . . 
    . f f e f b f 4 4 f b f e f f . 
    . f e e 4 1 f d d f 1 4 e e f . 
    . . f e e d d d d d d e e f . . 
    . . . f e e 4 4 4 4 e e f . . . 
    . . e 4 f 2 2 2 2 2 2 f 4 e . . 
    . . 4 d f 2 2 2 2 2 2 f d 4 . . 
    . . 4 4 f 4 4 5 5 4 4 f 4 4 . . 
    . . . . . f f f f f f . . . . . 
    . . . . . f f . . f f . . . . . 
    `, SpriteKind.Player)
controller.moveSprite(mySprite)
tiles.placeOnRandomTile(mySprite, sprites.castle.tileDarkGrass3)
scene.cameraFollowSprite(mySprite)
for (let index = 0; index < 3; index++) {
    coin = sprites.create(img`
        . . b b b b . . 
        . b 5 5 5 5 b . 
        b 5 d 3 3 d 5 b 
        b 5 3 5 5 1 5 b 
        c 5 3 5 5 1 d c 
        c d d 1 1 d d c 
        . f d d d d f . 
        . . f f f f . . 
        `, SpriteKind.Food)
    tiles.placeOnRandomTile(coin, sprites.builtin.brick)
}
for (let index = 0; index < 8; index++) {
    enemySprite = sprites.create(img`
        . . . . . . . c c c . . . . . . 
        . . . . . . c b 5 c . . . . . . 
        . . . . c c c 5 5 c c c . . . . 
        . . c c b c 5 5 5 5 c c c c . . 
        . c b b 5 b 5 5 5 5 b 5 b b c . 
        . c b 5 5 b b 5 5 b b 5 5 b c . 
        . . f 5 5 5 b b b b 5 5 5 c . . 
        . . f f 5 5 5 5 5 5 5 5 f f . . 
        . . f f f b f e e f b f f f . . 
        . . f f f 1 f b b f 1 f f f . . 
        . . . f f b b b b b b f f . . . 
        . . . e e f e e e e f e e . . . 
        . . e b c b 5 b b 5 b f b e . . 
        . . e e f 5 5 5 5 5 5 f e e . . 
        . . . . c b 5 5 5 5 b c . . . . 
        . . . . . f f f f f f . . . . . 
        `, SpriteKind.Enemy)
    enemySprite.vy = randint(20, 50)
    enemySprite.setBounceOnWall(true)
    tiles.placeOnRandomTile(enemySprite, sprites.builtin.brick)
}
info.setScore(0)
info.setLife(3)
game.showLongText("Collect all 3 coins and then find the flower tile to win!", DialogLayout.Center)
```


## Introduction @showdialog 
**Yellow Belt Game Building Session**

In this tutorial, you will explore an activity similar to what you might find in Code Ninjas' Yellow Belt curriculum, which focuses on practicing coding skills while using **tilemaps** in MakeCode Arcade.

Click **Ok** to get started! 

![Game Example](https://github.com/Code-Ninjas-Home-Office/game-building-session-yb-ob/blob/master/images/GBSYBProject.gif?raw=true "Ninja Riddle Quest project") 

![Logo](https://github.com/Code-Ninjas-Home-Office/game-building-session-tutorials-2024/blob/master/images/CN-Logo.png?raw=true "CN Logo") 
 
## Add a tilemap   

A **tilemap** is a game map made up of different squares, or **tiles**, that can be customized to create different types of 2D and top-down perspective games. Today, you will be using a tilemap to create a maze game.

- :tree: Open ``||scene:Scene|`` and drag ``||scene:set tilemap to||`` inside the ``||loops:on start||`` container already on screen. 
- :mouse pointer: Click the grey square in the block to open the **tilemap editor**. Explore the editor, then click **Done** to return to the tutorial.

![Logo](https://github.com/Code-Ninjas-Home-Office/game-building-session-tutorials-2024/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

```blocks
tiles.setCurrentTilemap(tilemap``)
```  

## Create a tilemap
Design a maze using tiles from the tilemap editor's **Gallery**. 

- :tree: Read the steps below, then open the tilemap editor by clicking on the gray square in the ``||scene:set tilemap to||`` block.
- :tree: First, select one type of tile to create a **path** for a sprite to move along. Be creative with your path design with lots of twists and turns but a clear start and finish.
- :tree: Then, fill in the tilemap area around the path with a different type of tile to create **walls**.
- :mouse pointer: Click on **Draw walls** to turn the wall tiles into actual tilemap walls that sprites will not be able to move through.
![draw walls icon](https://github.com/Code-Ninjas-Home-Office/game-building-session-yb-ob/blob/master/images/tilemap%20draw%20walls%20button.png?raw=true "Draw Walls icon")
- :mouse pointer: Click **Done** after completing these steps.

## The Game Window 
As you add code to your project, look at the Game Window on the **lower right** of your screen to see it update! 

![Game Window](https://github.com/Code-Ninjas-Home-Office/game-building-session-tutorials-2024/blob/master/images/GameWindow.png?raw=true "Game Window") 

![Logo](https://github.com/Code-Ninjas-Home-Office/game-building-session-tutorials-2024/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

## Customize the tilemap
Replace **path** tiles with **start** and **goal** tiles that will serve as a start and end point of your maze.

- :tree: Read the steps below, then open the tilemap editor by clicking on the gray square in the ``||scene:set tilemap to||`` block.
- :tree: Select a different type of tile to replace 1 or 2 path tiles with a tile that will be used as a **starting point** for the Player sprite.
- :tree: Select another type of tile to replace 1 or 2 path tiles with a tile that will be used as a **goal** for the Player sprite to reach.
- :mouse pointer: Click **Done** after completing these steps.

## Add a Player Sprite 
Create a Player sprite who will navigate through the tilemap maze. 

- :paper plane: Open ``||sprites:Sprites||`` and drag the ``||variables(sprites):set mySprite to||`` block to the bottom of the ``||loops: on start||`` container. 
- :mouse pointer: Click the gray square and select any image you would like from the **Gallery** of sprite images. 
- :tree: Open ``||scene:Scene||`` and drag a ``||scene:place mySprite on top of random||`` block to the bottom of the ``||loops:on start||``.
- :mouse pointer: Click the blank tile image then select your **start** tile from the dropdown.

![Logo](https://github.com/Code-Ninjas-Home-Office/game-building-session-tutorials-2024/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

```blocks
tiles.setCurrentTilemap(tilemap``)
let mySprite = sprites.create(img`
    . . . . . . f f f f . . . . . . 
    . . . . f f f 2 2 f f f . . . . 
    . . . f f f 2 2 2 2 f f f . . . 
    . . f f f e e e e e e f f f . . 
    . . f f e 2 2 2 2 2 2 e e f . . 
    . . f e 2 f f f f f f 2 e f . . 
    . . f f f f e e e e f f f f . . 
    . f f e f b f 4 4 f b f e f f . 
    . f e e 4 1 f d d f 1 4 e e f . 
    . . f e e d d d d d d e e f . . 
    . . . f e e 4 4 4 4 e e f . . . 
    . . e 4 f 2 2 2 2 2 2 f 4 e . . 
    . . 4 d f 2 2 2 2 2 2 f d 4 . . 
    . . 4 4 f 4 4 5 5 4 4 f 4 4 . . 
    . . . . . f f f f f f . . . . . 
    . . . . . f f . . f f . . . . . 
    `, SpriteKind.Player)
tiles.placeOnRandomTile(mySprite, assets.tile``)
```

## Let's Get Moving 
Code the sprite to move around the screen.

- :game controller: Open ``||controller:Controller||`` and drag ``||controller:move mySprite with buttons||`` block to the bottom of the ``||loops:on start||``. 
- :tree: Open ``||scene:Scene||`` and drag ``||scene:camera follow sprite||`` below it.

Try it out: use the **arrow keys** or **WASD** to move the sprite around the screen. Notice how the camera follows the sprite as it navigates the tilemap.

![Logo](https://github.com/Code-Ninjas-Home-Office/game-building-session-tutorials-2024/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

```blocks
tiles.setCurrentTilemap(tilemap``)
let mySprite = sprites.create(img`
    . . . . . . f f f f . . . . . . 
    . . . . f f f 2 2 f f f . . . . 
    . . . f f f 2 2 2 2 f f f . . . 
    . . f f f e e e e e e f f f . . 
    . . f f e 2 2 2 2 2 2 e e f . . 
    . . f e 2 f f f f f f 2 e f . . 
    . . f f f f e e e e f f f f . . 
    . f f e f b f 4 4 f b f e f f . 
    . f e e 4 1 f d d f 1 4 e e f . 
    . . f e e d d d d d d e e f . . 
    . . . f e e 4 4 4 4 e e f . . . 
    . . e 4 f 2 2 2 2 2 2 f 4 e . . 
    . . 4 d f 2 2 2 2 2 2 f d 4 . . 
    . . 4 4 f 4 4 5 5 4 4 f 4 4 . . 
    . . . . . f f f f f f . . . . . 
    . . . . . f f . . f f . . . . . 
    `, SpriteKind.Player)
tiles.placeOnRandomTile(mySprite, assets.tile``)
controller.moveSprite(mySprite)
scene.cameraFollowSprite(mySprite)
```

## Add Something to Collect
Add multiple objects for the Player sprite to collect as it navigates the maze.

- :repeat: Open ``||loops:Loops||`` and drag a ``||loops:repeat||`` block into the bottom of the ``||loops:on start||`` container.
- :paper plane: Add a ``||variables(sprites):set mySprite to||`` block inside the ``||loops:repeat||``. Click the gray square to select an image from the **Gallery**.
- :mouse pointer: Click on ``||variables:mySprite||`` to create a new **variable** name for this sprite. 
- :mouse pointer: Click on ``||sprites:Player||`` to change the **Sprite Kind** from Player to **Food**. 
- :tree: Add a ``||scene:place mySprite on top of random||`` block inside the ``||loops:repeat||``. Change ``||variables:mySprite||`` to the new sprite variable name, and select the **path** tile from the dropdown.

Explore the tilemap to look for the collectible sprites. Adjust the number in the ``||loops:repeat||`` to create more or less collectible objects.

![Logo](https://github.com/Code-Ninjas-Home-Office/game-building-session-tutorials-2024/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

```blocks
tiles.setCurrentTilemap(tilemap``)
let mySprite = sprites.create(img`
    . . . . . . f f f f . . . . . . 
    . . . . f f f 2 2 f f f . . . . 
    . . . f f f 2 2 2 2 f f f . . . 
    . . f f f e e e e e e f f f . . 
    . . f f e 2 2 2 2 2 2 e e f . . 
    . . f e 2 f f f f f f 2 e f . . 
    . . f f f f e e e e f f f f . . 
    . f f e f b f 4 4 f b f e f f . 
    . f e e 4 1 f d d f 1 4 e e f . 
    . . f e e d d d d d d e e f . . 
    . . . f e e 4 4 4 4 e e f . . . 
    . . e 4 f 2 2 2 2 2 2 f 4 e . . 
    . . 4 d f 2 2 2 2 2 2 f d 4 . . 
    . . 4 4 f 4 4 5 5 4 4 f 4 4 . . 
    . . . . . f f f f f f . . . . . 
    . . . . . f f . . f f . . . . . 
    `, SpriteKind.Player)
tiles.placeOnRandomTile(mySprite, assets.tile``)
controller.moveSprite(mySprite)
scene.cameraFollowSprite(mySprite)
for (let index = 0; index < 3; index++) {
    let coin = sprites.create(img`
        . . b b b b . . 
        . b 5 5 5 5 b . 
        b 5 d 3 3 d 5 b 
        b 5 3 5 5 1 5 b 
        c 5 3 5 5 1 d c 
        c d d 1 1 d d c 
        . f d d d d f . 
        . . f f f f . . 
        `, SpriteKind.Food)
    tiles.placeOnRandomTile(coin, assets.tile``)
}
```

## Keep Track of the Score!
Increase the score and destroy the collectible sprite when the Player overlaps it.

- :paper plane: Open ``||sprites:Sprites||`` and drag out a ``||sprites:on sprite overlaps||`` container and place it anywhere in the editor. Change the second ``||sprites:Player||`` to ``||sprites:Food||``.
- :paper plane: Open ``||sprites:Sprites||`` and drag a ``||sprites:destroy||`` block into the ``||sprites:overlap||`` container.
- :mouse pointer: Drag the ``||variables:otherSprite||`` oval from the ``||sprites:overlap||`` container into the ``||sprites:destroy||`` block.
- :id card: From ``||info:Info||``, drag a ``||info:set score||`` block into the ``||loops:on start||`` and a ``||info:change score||`` block into the ``||sprites:overlap||``.

Test your game: do the Food sprites disappear and the score increase, as expected?

![Logo](https://github.com/Code-Ninjas-Home-Office/game-building-session-tutorials-2024/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

```blocks
sprites.onOverlap(SpriteKind.Player, SpriteKind.Food, function (sprite, otherSprite) {
    sprites.destroy(otherSprite)
    info.changeScoreBy(1)
})
info.setScore(0)
```

## Add Enemy Sprites!
Add several Enemy sprites to make the maze more challenging to navigate!

- :repeat: Drag another ``||loops:repeat||`` block into the bottom of the ``||loops:on start||`` container.
- :paper plane: Add a ``||variables(sprites):set mySprite to||`` block inside then select a sprite image from the **Gallery**.
- :mouse pointer: Create a new **variable** name for this sprite, then change the **Sprite Kind** from Player to **Enemy**. 
- :tree: Use a ``||scene:place mySprite on top of random||`` block set to the new sprite variable name and the **path** tile to place multiple Enemy sprites along the tilemap.

Test your game. Adjust the number in the ``||loops:repeat||`` to create more or less Enemy sprites.

![Logo](https://github.com/Code-Ninjas-Home-Office/game-building-session-tutorials-2024/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

```blocks
info.setScore(0)
tiles.setCurrentTilemap(tilemap``)
let mySprite = sprites.create(img`
    . . . . . . f f f f . . . . . . 
    . . . . f f f 2 2 f f f . . . . 
    . . . f f f 2 2 2 2 f f f . . . 
    . . f f f e e e e e e f f f . . 
    . . f f e 2 2 2 2 2 2 e e f . . 
    . . f e 2 f f f f f f 2 e f . . 
    . . f f f f e e e e f f f f . . 
    . f f e f b f 4 4 f b f e f f . 
    . f e e 4 1 f d d f 1 4 e e f . 
    . . f e e d d d d d d e e f . . 
    . . . f e e 4 4 4 4 e e f . . . 
    . . e 4 f 2 2 2 2 2 2 f 4 e . . 
    . . 4 d f 2 2 2 2 2 2 f d 4 . . 
    . . 4 4 f 4 4 5 5 4 4 f 4 4 . . 
    . . . . . f f f f f f . . . . . 
    . . . . . f f . . f f . . . . . 
    `, SpriteKind.Player)
tiles.placeOnRandomTile(mySprite, assets.tile``)
controller.moveSprite(mySprite)
scene.cameraFollowSprite(mySprite)
for (let index = 0; index < 3; index++) {
    let coin = sprites.create(img`
        . . b b b b . . 
        . b 5 5 5 5 b . 
        b 5 d 3 3 d 5 b 
        b 5 3 5 5 1 5 b 
        c 5 3 5 5 1 d c 
        c d d 1 1 d d c 
        . f d d d d f . 
        . . f f f f . . 
        `, SpriteKind.Food)
    tiles.placeOnRandomTile(coin, assets.tile``)
}
for (let index = 0; index < 8; index++) {
    let enemySprite = sprites.create(img`
        . . . . . . . c c c . . . . . . 
        . . . . . . c b 5 c . . . . . . 
        . . . . c c c 5 5 c c c . . . . 
        . . c c b c 5 5 5 5 c c c c . . 
        . c b b 5 b 5 5 5 5 b 5 b b c . 
        . c b 5 5 b b 5 5 b b 5 5 b c . 
        . . f 5 5 5 b b b b 5 5 5 c . . 
        . . f f 5 5 5 5 5 5 5 5 f f . . 
        . . f f f b f e e f b f f f . . 
        . . f f f 1 f b b f 1 f f f . . 
        . . . f f b b b b b b f f . . . 
        . . . e e f e e e e f e e . . . 
        . . e b c b 5 b b 5 b f b e . . 
        . . e e f 5 5 5 5 5 5 f e e . . 
        . . . . c b 5 5 5 5 b c . . . . 
        . . . . . f f f f f f . . . . . 
        `, SpriteKind.Enemy)
    tiles.placeOnRandomTile(enemySprite, assets.tile``)
}
``` 

## Make the Enemy Sprites Move!
Add code to make the Enemy sprites move across the tilemap path.

- :paper plane: Open ``||sprites:Sprites||`` and drag ``||sprites:set mySprite x||`` inside the ``||loops:repeat||``. Change mySprite to the Enemy sprite variable name, then select **vy (velocity y)** from the dropdown.
- :calculator: Open ``||math:Math||`` and drag ``||math:pick random||`` into the parameter bubble of the ``||sprites:set mySprite vy||`` block. Update the range to be **20 to 50**.
- :paper plane: Open ``||sprites:Sprites||`` and drag ``||sprites:set mySprite bounce on wall||`` inside the ``||loops:repeat||``, then update the sprite's variable name.

Test your game. Adjust the **vy** speed as needed; change **vy** to **vx** if left-right movement works better than up-down movement in your maze.

![Logo](https://github.com/Code-Ninjas-Home-Office/game-building-session-tutorials-2024/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

```blocks
info.setScore(0)
tiles.setCurrentTilemap(tilemap``)
let mySprite = sprites.create(img`
    . . . . . . f f f f . . . . . . 
    . . . . f f f 2 2 f f f . . . . 
    . . . f f f 2 2 2 2 f f f . . . 
    . . f f f e e e e e e f f f . . 
    . . f f e 2 2 2 2 2 2 e e f . . 
    . . f e 2 f f f f f f 2 e f . . 
    . . f f f f e e e e f f f f . . 
    . f f e f b f 4 4 f b f e f f . 
    . f e e 4 1 f d d f 1 4 e e f . 
    . . f e e d d d d d d e e f . . 
    . . . f e e 4 4 4 4 e e f . . . 
    . . e 4 f 2 2 2 2 2 2 f 4 e . . 
    . . 4 d f 2 2 2 2 2 2 f d 4 . . 
    . . 4 4 f 4 4 5 5 4 4 f 4 4 . . 
    . . . . . f f f f f f . . . . . 
    . . . . . f f . . f f . . . . . 
    `, SpriteKind.Player)
tiles.placeOnRandomTile(mySprite, assets.tile``)
controller.moveSprite(mySprite)
scene.cameraFollowSprite(mySprite)
for (let index = 0; index < 3; index++) {
    let coin = sprites.create(img`
        . . b b b b . . 
        . b 5 5 5 5 b . 
        b 5 d 3 3 d 5 b 
        b 5 3 5 5 1 5 b 
        c 5 3 5 5 1 d c 
        c d d 1 1 d d c 
        . f d d d d f . 
        . . f f f f . . 
        `, SpriteKind.Food)
    tiles.placeOnRandomTile(coin, assets.tile``)
}
for (let index = 0; index < 8; index++) {
    let enemySprite = sprites.create(img`
        . . . . . . . c c c . . . . . . 
        . . . . . . c b 5 c . . . . . . 
        . . . . c c c 5 5 c c c . . . . 
        . . c c b c 5 5 5 5 c c c c . . 
        . c b b 5 b 5 5 5 5 b 5 b b c . 
        . c b 5 5 b b 5 5 b b 5 5 b c . 
        . . f 5 5 5 b b b b 5 5 5 c . . 
        . . f f 5 5 5 5 5 5 5 5 f f . . 
        . . f f f b f e e f b f f f . . 
        . . f f f 1 f b b f 1 f f f . . 
        . . . f f b b b b b b f f . . . 
        . . . e e f e e e e f e e . . . 
        . . e b c b 5 b b 5 b f b e . . 
        . . e e f 5 5 5 5 5 5 f e e . . 
        . . . . c b 5 5 5 5 b c . . . . 
        . . . . . f f f f f f . . . . . 
        `, SpriteKind.Enemy)
    tiles.placeOnRandomTile(enemySprite, assets.tile``)
    enemySprite.vy = randint(20, 50)
    enemySprite.setBounceOnWall(true)
}
```

## Don't Lose a Life!
Decrease the Player's life and destroy the Enemy when the sprites overlap.

- :paper plane: Open ``||sprites:Sprites||`` and drag out a ``||sprites:on sprite overlaps||`` container. Change the second ``||sprites:Player||`` to ``||sprites:Enemy||``.
- :paper plane: Open ``||sprites:Sprites||`` and drag a ``||sprites:destroy||`` block into the ``||sprites:overlap||`` container.
- :mouse pointer: Drag the ``||variables:otherSprite||`` oval from the ``||sprites:overlap||`` container into the ``||sprites:destroy||`` block.
- :id card: From ``||info:Info||``, drag a ``||info:set life||`` block into the ``||loops:on start||`` and a ``||info:change life||`` block into the ``||sprites:overlap||``.
- :tree: From ``||scene:Scene||``, use a ``||scene:place mySprite on top of random||`` to set the Player sprite back to a **start** tile. Then use a ``||scene:camera shake||`` block to create a screen shaking effect.

Test your game: do the Enemy sprites disappear and the lives decrease, as expected?

![Logo](https://github.com/Code-Ninjas-Home-Office/game-building-session-tutorials-2024/blob/master/images/CN-Logo.png?raw=true "CN Logo") 

```blocks
sprites.onOverlap(SpriteKind.Player, SpriteKind.Enemy, function (sprite, otherSprite) {
    sprites.destroy(otherSprite)
    info.changeLifeBy(-1)
    tiles.placeOnRandomTile(sprite, assets.tile``)
    scene.cameraShake(4, 500)
})
info.setScore(0)
info.setLife(3)
```

## Win the Game!
Code the **goal** tiles so the Player can win the game!

- :tree: Open ``||scene:Scene||`` and drag out an ``||scene:on sprite overlaps tile||`` container. Select the **goal** tile from the tile dropdown.
- :shuffle: Open ``||logic:Logic||`` and drag an ``||logic:if else||`` container into the ``||scene:overlap||`` container.
- :shuffle: Replace ``||logic:<true>||`` with a ``||logic:<0=0>||`` block.
- :id card: Open ``||info:Info||`` and drag a ``||info:score||`` oval into the left side of the ``||logic:<0=0>||`` block. On the right side, replace **0** with the number of Food sprites used in your game.
- :circle: Open ``||game:Game||`` and drag a ``||game:game over||`` block into the **if** part of the ``||logic:if else||`` container.
- :circle: Open ``||game:Game||`` again and drag a ``||game:show long text||`` block into the **else** part of the ``||logic:if else||`` container. Add a message to tell the player to collect all of the Food sprites.
- :repeat: Open ``||loops:Loops||`` and drag a ``||loops:pause||`` block below the ``||logic:if else||`` container to pause the overlap event from running immediately.

Test your game to see what happens when the Player touches a **goal** tile!

```blocks
scene.onOverlapTile(SpriteKind.Player, assets.tile``, function (sprite, location) {
    if (info.score() == 3) {
        game.gameOver(true)
    } else {
        game.showLongText("You need more coins!", DialogLayout.Center)
    }
    pause(1000)
})
```

## Add the finishing touches!
Here are a few additional things you can add to your maze game:

- :tree: Add a **hazard** tile! Replace some of the **path** tiles with a new tile, then use a ``||scene:on sprite overlaps tile||`` container to make something happen when the Player sprite overlaps a hazard.
- :circle: Use ``||game:splash||`` or ``||game:show long text||`` blocks to add game instructions.
- :headphones: Use a ``||music:play sound||`` block to add sound effects for even more fun!
- :paint brush: Customize the sprites and background to your liking.
- :id card: Use a ``||info:start countdown||`` timer to challenge the user to solve the riddle in a certain amount of time.

When you have finished, click **Done**. Then, follow your Code Sensei's guidance to create a shareable link that will let you play your game at home!

![Logo](https://github.com/Code-Ninjas-Home-Office/game-building-session-tutorials-2024/blob/master/images/CN-Logo.png?raw=true "CN Logo") 
