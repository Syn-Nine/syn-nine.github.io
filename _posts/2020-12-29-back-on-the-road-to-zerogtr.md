---
title: "Back on the road to Zero GTR"
date: 2020-12-29T11:20:00-04:00
#last_modified_at: 2016-03-09T16:20:02-05:00
categories:
  - blog
tags:
  - Zero GTR
  - Rust
---
### Can't Sleep
I woke up at 2:30 am and couldn't get back to sleep thinking about my old anti-gravity racing game concept, Zero GTR. I had made some rough gesture drawings of racer concepts a couple days ago just for sketching practice. 

![Rough racer gesture sketches](/assets/images/posts/racers_2020-12-27.jpg)

It appears that my brain is finally ready to have another go at this idea. I think I've had 7 or so false starts on this project over the last decade due to one reason or another. The last false start I had was primarily because I got to the point to start making game art assets and couldn't get my ideas out of my head - everything I drew or modeled left me unsatisfied. After that, I decided to put some serious effort into working on my drawing and design skills.

Recent drawings / designs:
![Mech Design](/assets/images/posts/wip-1.jpg)
![Creature Design](/assets/images/posts/concept-4-sm.jpg)


### Making it in Rust
Lately, I've been making mini-games in the Rust programming language. The language has some appeal as a safe concurrent systems level programming language and may be a popular language for making games in the future. Programming this game in Rust would help me develop my skill with the language so that I can leverage it professionally in my modeling and simulation career. I can also use the game/engine as an AI test bed in my ongoing PhD research.

Since I couldn't sleep, I figured I would start a new development log for the game with the hope of documenting my development process and creating a nice behind-the-design book if it ever ships.

Starting an engine from scratch - in a language I barely know - with pretty much no personal codebase to build off of, it'd be a good idea to make a map of the major components needed, and a path for how to get there.

### General game engine features needed
- Physics
- Collision Detection
- Rendering
- Input
- Networking
- Scene Data
- AI
- Art Assets
- Menus
- HUD
- Sound/Music
- File IO
- Particles
- Dynamic Camera Replay

I have successfully built my own TCP and UDP libraries in C++ with connection state management, however, I haven't done that in Rust. It looks like people are working on networking libraries though. From personal experience, the network layer needs to get built into the engine very early or else the complexity of adding it later gets incredibly high.

### Requirements
This will not be a general use engine, but a federation of systems, this way pieces like File IO and input handling can be used for other projects. However, there are some important gameplay elements that I've settled on that help direct the scope of the game-specific engine components:
- I can use other people's low level utilities, such as for playing sound effects, but cannot use other people's engines or game-development-kits.
- The game is an anti-gravity racing game, therefore the racecraft must float.
- Also, since the game is anti-gravity racing, gravity doesn't apply, and the direction of "down" is not constant. The tracks must be able to twist and curve in any direction while still feeling fun and playable.
- The game is 3D, and must support 3D collision and collision response (axial and rotational).
- Must use a modern deferred rendering pipeline.
- The AI must present a reasonable challenge, but also obey the game rules. This one will be particularly hard, because the AI must avoid collision with walls and other vehicles, while also trying to win.

Even though the track twists and turns, it can be broken down into tiny segments that are locally flat, much like taking the derivative of a curve. Inside these segments, the gameplay can be approximated like a 2D top down racing game, ie, your only motion is forward and in the direction of yaw. Using that approximation, most of the engine components can be initially developed as a 2D top down racing mini-game. Other components that require 3D can be developed in small parallel test projects. Creating this as a mini-game will also be helpful with controlling technical debt while I'm getting better at programming in Rust.

### Next Steps
Going forward, the next critical elements to get working are simple polygon rendering, game clock tick, and gamepad input. In parallel, I need to start defining the scope of the art assets so that I can start art pre-production.

Cheers
-Syn9