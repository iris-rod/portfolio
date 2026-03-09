---
layout: default
---

# Other Projects

## Programming projects

There are projects where my main role was as a programmer. Fortunatelly, I've done some projects where we had an artist, so the programmers could focus entirely on programming and nothing else. These are the projects I love doing the most, since I can improve my abilities, work in a group of people with different responsabilities and knowledge and learn from them.

### Global Game Jam 2026 Participation

"You need to do what you must to survive in today's market. You found a rotting house on Idiotlista and now you're trying to flip it for as much money as you can get. But no one has time to actually fix the house up, just cover it up, no one will notice!"

<p align="center">
    <img src="https://github.com/iris-rod/portfolio/blob/master/img/Logo.png?raw=true" width="45%"/>
</p>

In this game you are a crafty rackoon that is a house flipper, you buy crappy looking houses for very low prices and then fix them up to re-sell at a higher price. However, your concept of fixing is a bit different from humans, or at least, any decent one. The way you fix the house is by covering up everything that is wrong with it by throwing anything you have on your garbage truck at it. The goal is to cover up, I mean, fix it as much as you can within the time limit to sell it at the highest price possible.

After a few years without participating in a GGJ, this year I teamed up with some really cool people to get back into the GGJ spirit that I hadn't had in a while.
Our team had 3 programmers (one of them was me), 2 artists and 1 sound artist. We had a very relaxed approach with this jam, since we're all older now, we can't keep up with all-nighters. But we still brought a lot of enthusiasm and it was a very fun weekend with everyone making this game!
Since we were quite a few people, we first organised all of our ideas for mechanics, art, animations etc and then created a small board to keep track of our work throughout the weekend. My role was to implement a few of the mechanics:

- Garbage scavenger - pick up random objects from the garbage truck. Each item had a probability of being picked up and obviously, the better the item the lower the probability of it dropping. The player could either do a quick search by pressing "E" or doing a longer search, called dumpster dive, to try to fetch better items by pressing and holding "E" for a bit. If the player did a dumpster dive, the probability weights were adapted to give higher weight to rarer items.
- Feng Shui system - the player gets extra money for placing certain items at certain places in the house. I took advantage of the work one of our members did for the covering mechanism in which we used empty objects to detect when another object is colliding with it and trigger events when it happens. These events can then be used to trigger any behaviour we might need in those scenarios. For the Feng Shui, I simply reused those, added a tag to them and placed them in the house and called them Feng Shui Placements. Then in the manager class, where it is listening for those events that detect that the props collided with a placement, I created a map of pairs of props and placement tags with scores which I parse through to update the score if the prop and placement pair match one on the list.

I also tried to have a nice looping effect on our background music where we would loop through the middle section of the song and when the timer was almost running out, change to the climax of the song. However, this still needs some improvement. It's working, but not as well as I would have liked it to be.

You can check out our submission for the GGJ at [Global Game Jam 2026 submission page](https://globalgamejam.org/games/2026/home-wreckoon-ii-trash-pandemonium-9) or try it online through one of our members [itch.io link](https://antoniocpacheco.itch.io/home-wreckoon)


### Puzzle tile game

This is a small project that I started last year with the goal to improve my algorithm and general C++ knowledge. I also wanted to implement a simple event based system in this game. It was fully developed using SDL libraries on Visual Studio (no engines).

To be completly honest, another goal was to have this project completed within a month, maybe two, however I had many moments were I was either too tired or unmotivated to pick it up and this made the implementation take a lot longer than what I wanted. I kept working on it, even if it was just 1 hour or 2 a week or every two weeks, because I would still be able to improve and see progress no matter how little or how slow it was, and I didn't want to leave this project unfinished. It is now completed and I'm happy and proud that I finished it and, more importantly, that I grew and learned from it.

This game is very simple: there are pieces of different colours randomly generated in columns and pushed into the board every x seconds. Whenever there are 2 or more pieces of the same colour connected to each other (either verticaly or horizontaly) you can click on them to remove them from the board and gain points. The goal is to reach the number of points to advance to the next level before the board reaches the end of the platform.

The main focus of this project was on mechanics/algorithm and coding, which means that the art is extremely simple (every texture looks more like a placeholder instead of actual game art), I did not implement animations, there are also no sound effects or music. The algorithm I used to remove the same colored pieces and re-organise the board accordingly was:

- Checked if the clicked piece has neighbours (verticaly or horizontaly) of the same colour
- Remove all pieces that are of the same colour and neighbours of each other
- Reorganise each column that had pieces removed to eliminate empty spaces on the bottom and/or in the middle of the column
- Move columns back (to the right) if there is any empty column

The event system implemented uses a priority queue which allows for this specific order of events to happen: remove pieces (PIECE_REMOVED), organise columns (COLUMN_UPDATE) and then move columns (EMPTY_COLUMN). 

- Whenever a piece is removed the PIECE_REMOVED event is triggered which is listened by every piece on the board. This event allows the pieces to verify if the removed one was their neighbour and if they share the same colour. If both conditions are true, then they should be removed as well.
- The COLUMN_UPDATE event is also triggered when a piece is removed, but this event is only listened by the board which will reorganise the column to eliminate empty spaces, if there are any at the bottom or middle of the column. 
- If the column turns out to be empty after organising it, the EMPTY_COLUMN event is triggered. This event is also only handled by the board and it will move the columns back to eliminate this empty column if it's not the last column.

To make the game a bit more dynamic I also added a button that allows the player to add a new column immediately instead of waiting the hardcoded x amount of time for it to be generated. This addition removes the scenario where the player is stuck waiting for a new column to be generated when there are no more pieces that he can remove from the current state of the board.

<p align="center">
    <img src="https://github.com/iris-rod/portfolio/blob/master/img/ore_main.png?raw=true" width="45%"/>
    <img src="https://github.com/iris-rod/portfolio/blob/master/img/ore_in_game.png?raw=true" width="45%"/>
</p>
<p align="center">
    <img src="https://github.com/iris-rod/portfolio/blob/master/img/ore_lost.png?raw=true" width="45%"/>
    <img src="https://github.com/iris-rod/portfolio/blob/master/img/ore_next_level.png?raw=true" width="45%"/>
</p>

If you want to play it, you can download it from here: <a href="img/PuzzleGame.zip">Download game</a> (Extract .zip file and play executable that is inside the Release folder)

If you're keen to check the code, you can go [here](https://github.com/iris-rod/PuzzleGame)

### Global Game Jam 2021 Participation

"A game about a mustache trying to be reunited with his owner in a world were mustaches are illegal. OBJECTIVE: Help the mustache to be reunited with his owner: for this you need to find in which store in the town your owner is while avoid the BB (brigada do bigode or mustache's patrol). To help you to identify the correct store your owner is in keep an eye on the mustachometer that indicates how close you are, get inside the store and be reunited with your maker."

In this year our team consisted of 2 programmers, so I also took on the role of 2D artist, which means that our game has very simple and goofy art style and animations. This time we decided to participate with a much more relaxed approach, so we didn't pull a all-nighter nor did we worry about making the best and most creative game ever. We just wanted to have fun making a bug-free game that we could run and show to others without saying "this was working before!", so we focused on very few mechanics and made sure that they were working properly. Another change this year was that we had a better planning: we planned and prioritised tasks each morning and night, we had regular checkpoints to merge our work and reorganise the tasks left and we were also better at version control with Git. I wholeheartedly believe that these two factors were the biggest contributes to successfully achieve our goal for this year's GGJ.

In this game the player is a mustache that wanders around the town trying to find is owner while avoiding the mustache's patrol. The patrol will follow the player once they see it, and will stop if he goes out of sight or too far away, but if they catch him, the mustache is arrested and the player loses the game. The player can hide from the patrol by attaching itself to animals or objects, such as birds and bushes. Once attached, the patrol will not see them. To find out in which store the owner is located, the player must keep an eye in the mustacheometer which will indicate him how near he is to the correct store. Once he finds the owner, he wins the game.

As I mentioned previously, I did all the art for this game, also some animations (bird's movement and water dripping from mustache). As a programmer I implemented:

- Brigada do Bigode (mustache's patrol) movement and behaviour
- Locking and unlocking the doors when mustache is being followed
- Attaching and dettaching from objects and animals
- Particle systems to indicate if the user can interact with the objects and animals
- Main menu and transition between both scenes
- Bird and bush behaviour
- Entering and exiting the stores
- Added some sound effects

Some of these things were added after the game jam ended, like the bushes, the particle systems and the main menu. I wanted to polish the game a bit more and I'm happy with the result. Here's a small video showcasing the game: [Mustache me when I'm Gone Gameplay](https://youtu.be/-iSa1NYuzGU)

<p align="center">
    <img src="https://github.com/iris-rod/portfolio/blob/master/img/cover_GGJ21.png?raw=true" width="50%"/>
</p>

If you want to play it, you can download it from here: <a href="img/MustacheMeWhenImGone.zip">Download Mustache me when I'm gone</a> (Extract .zip file and play executable)

Or you can check out our submission for the GGJ (it is slightly outdated): [Global Game Jam 2021 submission page](https://globalgamejam.org/2021/games/mustache-me-when-im-gone-9)

### Escape Room online course

I created a small Escape Room type game through an online game development course for Unreal. The main mechanics introduced in the course are of opening doors by placing weighted objects on a trigger and when they are removed the doors close.

This course was really good to learn, not only more about what Unreal offers and how to use it's components in the best way possible, but also to practice more C++ programming, since it only uses C++ classes and no blueprints. The course touched on several basic aspects of programming in general, like good programming practices and coder refactoring, and also some aspects specific to C++ language like pointers and memory. It didn't go to deep into any of these topics, it talked about it in a more general way so that less experienced programmers could understand it easily, but it's still great to make sure the basics are covered and fully understood.

The course taught how to implement two mechanics: grab objects and open doors by placing objects on triggers. From those mechanics we then should build a level with assets and the mechanics. I also implemented a small variation to the "open doors" mechanic, where instead of just using the weight to determine whether the door should open, it needs to be a specific item that is placed on the trigger and it might be necessary to use more than 1 item.

It's still a work in progress, there are some tweaks and improvements I want to make, specially on the grab mechanic, but here is a small video with the result for now [Escape Room Gameplay](https://www.youtube.com/watch?v=lAG7DJLP4Wc&fbclid=IwAR2s-0OFEO4bl5hCrYkkphk93dvLu1vOGNSZ19BmfHMGL5sV4sVDTJ0R7y8) (It has some subtitles along that provide some explanation on the gameplay and how it is working)

### Global Game Jam 2020 Participation

"Two Giant Stars have just merged together affecting several of the inhabited planets nearby, Many species are in danger of extinction, and it is up to you to change that. In RE-Evolution, you are a robotic worker of the Re-adaptation Species Space Company working tirelessly to change the species of your planets representative clients."

In this Global Game Jam we were more artists than programmers, there were 3 artists and 2 programmers (one of them was me)! This meant that we had really good art and animations to work with, which made us really excited. Unfortunatelly, we were way too ambitious with our ideas and in the end, we left out some of the work the artists made because we didn't have time to add everything with the gameplay.

The game was heavily inspired by Overcooked where there are 'orders' that come in and the players need to put the items together properly to deliver the 'order' correctly. In our case, the orders are combinations of body parts of different animals, for example, fish legs, duck head and crocodile body. To create the body parts, you have to pick up the essence of the animal and the body part, put them in the cauldron and it will combine the two to create the desired result. After that, you shoot it at the default doll passing by on the rails to set it! The game can have up to 4 players, creating more mayhem and caos when trying to get the orders right and get the most points.

My role in this was combining the body parts with the animal essences to generate the correct combination, as well as the rails and order system, which included generation the orders, replacing the default body part on the doll with the body part that was shot through the cannon and the rails movement.

I worked on the game for a while after the jam ended to improve it and improve my skills at the same time.

Link to this submission on Global Game Jam 2020 at [Re-Evolution](https://globalgamejam.org/2020/games/re-evolution-1).

<p align="center">
    <img src="https://github.com/iris-rod/portfolio/blob/master/img/ggj3.png?raw=true" width="45%"/>
    <img src="https://github.com/iris-rod/portfolio/blob/master/img/ggj4.png?raw=true" width="45%"/>
</p>
<p align="center">
    <img src="https://github.com/iris-rod/portfolio/blob/master/img/ggj5.png?raw=true" width="45%"/>
    <img src="https://github.com/iris-rod/portfolio/blob/master/img/ggj6.png?raw=true" width="45%"/>
</p>

### Global Game Jam 2019 Participation

"It's cleaning day and the whole family has to clean up the house! However, not everyone agrees on what should go where. The toilet paper doesn't always show up in the bathroom, and some socks are stored away in the kitchen. Try to clean the house the way that makes you feel like home!"

For this year Global Game Jam we had a pretty awesome team of 3 programmers (me included) and 1 artist, which meant we could create not only good gameplay mechanics but also cool and original art! Our game consisted on having 4 players and 3 items in the house, the player that cleans up the most items in their right place, wins. However, since there are fewer items than players, they will have to be faster and tackle the others to get the most points. The biggest downside to this version is that it was designed for 4 players, so if you play with less people, it will not have the same feel. 

My part on this jam consisted on randomnly generating the different items on the level and checking if the player was delivering the item to the right room. I also added some sound effects and special effects (the good old friends, particle systems) to enhance the feedback that the player had from the actions he performed.

Here is a small video with the gameplay: [Not Under My Roof!!!! Gameplay](https://www.youtube.com/watch?v=PojqQ88-C4A&feature=youtu.be)

Download this game at [Not Under My Roof!!!!](https://globalgamejam.org/2019/games/not-under-my-roof) and have fun with your friends!

<p align="center">
    <img src="https://github.com/iris-rod/portfolio/blob/master/img/NotUndeerMyRoof1.png?raw=true" width="50%"/>
</p>
<p align="center">
    <img src="https://github.com/iris-rod/portfolio/blob/master/img/NotUndeerMyRoof2.png?raw=true" width="45%"/>
    <img src="https://github.com/iris-rod/portfolio/blob/master/img/NotUndeerMyRoof3.png?raw=true" width="45%"/>
</p>

### Global Game Jam 2018 Participation

"Three amigos from the latino side of America want to feed their family and get a nice job in the land of the free. But there is only one passport! 
Cooperate with your fellows to cross the border without getting caught by the Immigration Control."

I participated in the Global Game Jam 2018 edition and created a fun multiplayer game with some friends. My job on the team was to create differet types of traps to be set in different levels as a way to increase the difficulty as the players progress through the game.

Check out this fun little game at: [Juan Forrest Juan!](https://globalgamejam.org/2018/games/juan-forrest-juan)

<p align="center">
    <img src="https://github.com/iris-rod/portfolio/blob/master/img/GGJ.png?raw=true" width="40%"/>
</p>

## Artist projects

These are projects that I participated more as an artist instead of a programmer. Although my focus is programming, I have some skills at drawing and animating, so when I'm in a group where we don't have any artist and we want to have coherent and original art, I take that role and my priority becomes the art. I enjoy doing these projects because it helps me to understand a little better the artist side, what they need to do, how they do it, how much time and requirements they need to do what they are asked, among other things.

### Sugar Jam Participation

This game jam was a different experience from the previous game jams that I had already participated in, but still fun and a good opportunity to explore new things. The whole concept of this jam was to use Sugar, a social gamification asset that helps adding competitive, cooperative and goal based mechanics. We were a team of 3, all programmers, and we decided to make a joust like game between robots. You built your robot with different parts (machine gun, shield, cannon,...) which are represented as cards, and fight other player's robot to win more cards. The judges of the game jam gaves the third place, which was really good and showed us that our hard work was recognized!

I made the robots parts and animated them using the Puppet 2D asset from Unity. This made it easier to create cool animations to the different body parts of the robot without having to create several sprites. It was a challenging and fun concept to tackle in this game jam and, although there are a lot of things I would improve, it was a good way to learn a bit more about animation. 

Find more about this game here: [Diet Beat](https://ratuspro.itch.io/diet-beat)

<p align="center">
    <img src="https://github.com/iris-rod/portfolio/blob/master/img/DB1.png?raw=true" width="50%"/>
</p>
<p align="center">
    <img src="https://github.com/iris-rod/portfolio/blob/master/img/DB2.png?raw=true" width="40%"/>
    <img src="https://github.com/iris-rod/portfolio/blob/master/img/DB3.png?raw=true" width="40%"/>
</p>
<p align="center">
    <img src="https://github.com/iris-rod/portfolio/blob/master/img/DB4.png?raw=true" width="40%"/>
    <img src="https://github.com/iris-rod/portfolio/blob/master/img/DB5.png?raw=true" width="40%"/>
</p>

### Breaking Dev 2018 Participation

"Dare to face your fears in your own dreams with the help of your trust worthy teddy bear!"

I participated in the Breaking Dev 2018 edition at Instituto Superior Técnico Campus TagusPark and created another multiplayer game, this time in a two-man team. We made it all from scratch, except the sounds and my main focus was the art and animations, which was the first time I had ever done it. Everything was drawn using Gimp and I made the character's and enemie's animations frame by frame, which took along time, but it was very enlightning to understand the process of drawing a full animation. They didn't turn out the prettiest or the best, but it was a great learning experience and a nice change from coding (although I realised I really do enjoy implementing mechanics more than drawing and animating). Overall, it was a full-on weekend of drawing and coding, but it was a lot of fun!

Check out the gameplay here: [Keep Dreamin' Gameplay](https://www.youtube.com/watch?v=oz2d1VIaBFA&feature=youtu.be)

<p align="center">
    <img src="https://github.com/iris-rod/portfolio/blob/master/img/KD_screenshot.png?raw=true" width="40%"/>
</p>





