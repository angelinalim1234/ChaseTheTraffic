## Table of contents
* [General Information](#general-information)
* [Features](#features)
* [Setup](#setup)
* [Technologies](#technologies)
* [Usage](#usage)
* [Status](#status)
* [Room for Improvement](#room-for-improvement)
* [Acknowledgements](#acknowledgements)
* [Contact](#contact)

  ## General info
This game is called Chase the traffic and the aim of the game is so that we can improve our motoric skill, 

## Features
* Sprite will jump when you press the A button
* Enemy will always try to chase wherever you go
* Have to collect the traffic sprite before the time ends
* Shouldn't fall to the base of ground

## Setup
How to set up the game to Tinker Gen Game go game console 
1) To run this project on , go to make code arcade and open your game project, press F4 for the hardware 
2) Click the Download button on the Arcade interface. Select F4 from the pop-up window.
3) Find and right click on the downloaded uf2 file on your computer. Send it to GameGo, Or, you can copy the file and paste it onto GameGo. When downloading the project. make sure the LED indicator on GameGo keeps blinking and only becomes steady after downloading completes.

## Technologies
I am using MakeCode arcade platform to make this game. Makecode arcade uses blocks and python technologies

## Usage

    def on_a_pressed():
    if mySprite.vy == 0:
#the sprite could only jump once they have touch the tiles, when vy is exactly 0 the sprite is not moving vertically

    mySprite.vy = -150
    controller.A.on_event(ControllerButtonEvent.PRESSED, on_a_pressed)

#the height level that they could jump, i set -150 because it is perfect for the platform that i build, it is not going to jump so high but not too low as well, gives the sprite an upward velocity, creating the effect of a jump. This value is negative because moving up corresponds to a negative y direction.

    def on_on_overlap(sprite, otherSprite):
      sprites.destroy(otherSprite)
    
#when the car touch the red flag it is going to destroy it, so that it is going to dissapear at the screen
    
    info.change_countdown_by(-2)
    sprites.on_overlap(SpriteKind.player, SpriteKind.redflag2, on_on_overlap)

#if the car hit the red flag, the time is gonna be deducted by 2 seconds.

    def on_overlap_tile(sprite2, location):
    game.game_over(False)
    scene.on_overlap_tile(SpriteKind.player,
    assets.tile("""
        myTile1
    """),
    on_overlap_tile)

#if the sprite falls to the base ground, the game is over

    def on_on_overlap2(sprite4, otherSprite2):
    sprites.destroy(otherSprite2)
    if mySprite.y < mySprite3.y:
        info.change_countdown_by(2)
    else:
#If the car hits on top of the human enemy, we get 2 second extra

        info.change_life_by(-1)
    sprites.on_overlap(SpriteKind.player, SpriteKind.enemy, on_on_overlap2)

#if the car hits beside of the human enemy, we will lose one of our life.

    def on_on_score():
    game.game_over(True)
    info.on_score(100, on_on_score)

#when the score reaches 100 the game is over

    mySprite3.set_position(mySprite.x + randint(0, 200), mySprite.y + randint(0, 150))
#Set the enemy sprite randomly appear horizontally by 0 to 200 pixels from car sprite's x coordinate, and randomly offsets it vertically by 0 to 150 pixel from car sprite y coordinate.
 
    mySprite3.follow(mySprite, 100)
#The speed of the enemy sprite following the car sprite

    info.start_countdown(10)
#start time is 10 seconds

    info.change_score_by(10)
    sprites.on_overlap(SpriteKind.player, SpriteKind.traffic, on_on_overlap3)
#When car sprite overlaps with the traffic, the time is going to be add up by 10 seconds

    mySprite = sprites.create(img("""
        ..............................
            ..............................
            ..............................
            ..............................
            ..............................
            ..............................
            ..............................
            ..............................
            .........ffffff...............
            .........f1ff1f...............
            .....ffffffffffffff...........
            .....ffffffffffffff...........
            .....ffffffffffffff...........
            .......ff......ff.............
            ..............................
            ..............................
            ..............................
            ..............................
            ..............................
            ..............................
            ..............................
            ..............................
            ..............................
            ..............................
            ..............................
            ..............................
            ..............................
            ..............................
            ..............................
            ..............................
        """),
        SpriteKind.player)
#making the sprite or making the character of the game

        controller.move_sprite(mySprite, 100, 0)
#adding the controller so that we can move the sprite with our keyboard, 100 for the vx and 0 for the vy so that it can only move left and right(only x direction)

        mySprite.ay = 200
#ay is the acceleration in the vertical direction, so that sprite would always fall downwards, 200 because it is the perfect pace, if it is 100 it is going to fall so slowly while if it is 400 it is going too fall so quickly
        
        info.set_life(3)
#Setting the amount of life which is 3
        
        info.start_countdown(10)
#Start countdown at 10 seconds

      for value2 in tiles.get_tiles_by_type(assets.tile("""
      myTile2
      """)):
      TRAFFIC = sprites.create(img("""
            . . . . . . . . . . . . . . . . 
                    . . . . . . . . . . . . . . . . 
                    . . . . . . 2 2 2 . . . . . . . 
                    . . . . . . 2 2 2 . . . . . . . 
                    . . . . . . 2 2 2 . . . . . . . 
                    . . . . . . 4 4 4 . . . . . . . 
                    . . . . . . 4 4 4 . . . . . . . 
                    . . . . . . 4 4 4 . . . . . . . 
                    . . . . . . 7 7 7 . . . . . . . 
                    . . . . . . 7 7 7 . . . . . . . 
                    . . . . . . 7 7 7 . . . . . . . 
                    . . . . . . . f . . . . . . . . 
                    . . . . . . . f . . . . . . . . 
                    . . . . . . . f . . . . . . . . 
                    . . . . . . . f . . . . . . . . 
                    . . . . . . . f . . . . . . . .
        """),
        SpriteKind.traffic)
        
#creating sprite traffic as our mission, we have to collect as much as we can

      tiles.place_on_tile(TRAFFIC, value2)
      tiles.set_tile_at(value2, assets.tile("""
        transparency16
      """))
#put traffic sprites on specific tiles(value 2) and replaces those tiles with transparency

      REDFLAG = sprites.create(img("""
            . . . . . . . . . . . . . . . . 
                    . . . . . . . . . . . . . . . . 
                    . . . . . . . . . . . . . . . . 
                    . . . . . . . 2 2 2 2 2 2 2 . . 
                    . . . . . . . 2 2 2 2 2 2 2 . . 
                    . . . . . . . 2 2 2 2 2 2 2 . . 
                    . . . . . . . 2 2 2 2 2 2 2 . . 
                    . . . . . . . 2 2 2 2 2 2 2 . . 
                    . . . . . . . 2 2 2 2 2 2 2 . . 
                    . . . . . . . 2 2 2 2 2 2 2 . . 
                    . . . . . . . 2 2 2 2 2 2 2 . . 
                    . . . . . . . f . . . . . . . . 
                    . . . . . . . f . . . . . . . . 
                    . . . . . . . f . . . . . . . . 
                    . . . . . . . f . . . . . . . . 
                    . . . . . . . f . . . . . . . .
        """),
        SpriteKind.redflag2)
        
#creating red flag sprites

      tiles.place_on_tile(REDFLAG, value3)
      tiles.set_tile_at(value3, assets.tile("""
        transparency16
      """))
#put red flag sprites on specific tiles(value 3) and replaces those tiles with transparency

    scene.camera_follow_sprite(mySprite)
#So that the screen follows where the sprite goes instead of just focusing on one screen

## Status
Project is complete


## Room for improvement
* Adding music so that the players can feel more engage to the game
* More graphic to make the game looks professional

## Acknowledgements
Brain, M. (2024, March 5). How Television Works. Howstuffworks. How Television Works | HowStuffWorks

Crawford, C. (1984). The art of computer game design. McGraw-Hill/Osborne Media.

Hunicke, R., Leblanc, M., & Zubek, R. (2004). MDA: A Formal Approach to Game Design and Game Research. ResearchGate. (PDF) MDA: A Formal Approach to Game Design and Game Research

Susskind, J. (2018). Code is Power. In Future politics: Living together in a world transformed by tech (pp. 89–99). Oxford University Press.

Microsoft. Create. MakeCode. create

Microsoft. On Life Zero. MakeCode. on Life Zero

Microsoft. Over. MakeCode. over

Microsoft MakeCode. (2020, March 18). How to Make a Platformer Game [Part 1: Intro, sprites, movement & tile map] [Video]. YouTube. How to Make a Platformer Game [Part 1: Intro, sprites, movement & tile map]

Microsoft MakeCode. (2020, March 25). How to Make a Platformer Game [Part 2: Animations, AI, collision & spawning] [Video]. YouTube. How to Make a Platformer Game [Part 2: Animations, AI, collision & spawning]

Microsoft MakeCode. (2021, March 27). How to create an arcade game [Video]. YouTube. How to create an Arcade Game


Ramos, L. (2024). Basic Data Types in Python: A Quick Exploration. Real Python. 

Woodys Workshop. (2021, April 12). MakeCode Arcade - Space Game Tutorial [Video]. YouTube. MakeCode Arcade - Space Game Tutorial

## Contact 
Ceated by @Angelinalim1234
    
