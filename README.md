# Stardancer - WIP! NOT FINISHED!!!
A 2D platformer game in which you play as a square in outer space traversing through 30 levels, gaining the ability to turn into various shapes along the way, each with their own powers!

-> insert a gameplay gif here

Watch the 100% walkthrough of the game here: [I'll add the link here eventually]

Play the game here: [I'll add the link here eventually]

## So what's in the game?
- 30 distinct, challenging levels featuring puzzles and shortcuts
- A plethora of unique obstacles and environments
- 5 different playable shapes, each with a distinct powerup
- "Easy to learn, hard to master"-type controls (think Celeste)
- Coins scattered throughout each level as an extra collectible
- Level timers, death counts, and more
- Hand-made SFX and artwork, with clean UI and transitions
- Interactive menus, such as a handbook and settings menu

## Controls
Note: you can change every single one of these controls in game thanks to the keybind menu!
| Action | Default Key |
|--------|-------------|
| Go Right | Right Arrow |
| Go Left | Left Arrow |
| Jump | Up Arrow |
| Go Down | Down Arrow |
| Restart | R |
| Go Back / Pause | Escape |
| Switch to Square | 1 |
| Switch to Circle | 2 |
| Switch to Octagon | 3 |
| Switch to Triangle | 4 |
| Switch to Hexagon | 5 |
| Special Key 1 | Left Shift |
| Special Key 2 | Right Shift |
  
## How does it work?
This game was made using purely C++ and the Simple and Fast Multimedia Library (SFML), which is a low-level graphics library used for rendering 2D graphics and shapes as well as basic SFX and the like. I did not use any external game engines, such as Godot or Unity, to create this project.
<br><br>
Relying solely on C++ and SFML was limiting because the scope of things you can actually do is not the largest; however it's still possible to create simple visual effects using its various features. Additionally, simply using C++ and SFML is enough to create a fully functional, fun-to-play game, as this game proves you do not need external game engines to make something enjoyable to play.
<br><br>
The shapeshifting feature is (in my opinion) quite a unique feature compared to other platformers. To create this system, I set a master entity class which includes all objects affected by physics (i.e. pushable blocks and players). This branches into the player sub-class, which branches further into sub-classes for each individual playable shape. Each contains the various playstyle quirks and visual appearances associated with each shape, and in the main game loop, an instance of the player is set to a square by default using std::make_unique<square>(). Whenever a switch occurs, make_unique<>() is run again with the according shape. Every frame runs a position and velocity capture so that when a switch occurs, it's easy to transfer the position and velocity by overriding the reset from shape creation. 
<br><br>
Another key aspect is the collision system. This game uses Separating Axis Theorem (SAT) collision, which checks if axes of two polygons intersect to determine collision, rather than Axis-Aligned Bounding Box (AABB) collision, which checks if the edges of two bounding rectangles overlap to determine collision. Using SAT collision was crucial for the game, as it uses multiple regular polygons that are often being rotated and AABB checks would result in erroneous collision. All collision-related functions and logic are stored in ```collisions.h```, such as returning vertices and axes of an object, translating objects by the Minimum Translation Vector (MTV) so they stop colliding, and checking if axes intersect i.e. if shapes are even colliding to begin with. Additionally, the rotation feature ties in well with the collision. There are two primary types of rotation in the game: rolling and tipping. Rolling logic is straightforward, simply using SFML's transformation system on each shape; settling down to a flat face is another rotation feature, but it's more of a sub-feature in rolling. Tipping is a more complex endeavor, involving:
- detecting whether or not a shape's midpoint is located directly above open air, 
- deciding which direction it should tip, 
- tipping the shape in that direction, and 
- deciding when the shape enters a freefall state and doesn't need to keep forcibly tipping.

## Building from Source (Local Development)
**Note:** Local builds are currently only tested and supported on **Windows** (Visual Studio).

If you want to compile and run *Stardancer* locally, follow these steps:

### Prerequisites
* **CMake** (Version 3.28 or higher)
* A C++17 compatible compiler
* **Git**

### Steps

1. Clone the repository by running:
```
git clone https://github.com/HughMann635/Stardancer.git
cd Stardancer
```

2. Configure the project with CMake (CMake will automatically download and configure SFML 3.1.0 via FetchContent):
```
cmake -B build
```

3. Build the executable:
```
cmake --build build --config Release
```

4. Run the game. Find the binary and assets automatically placed in
```
build/bin/Release/stardancer.exe
```


## Credits and Acknowledgements
- AI use: Used AI for minor debugging in physics and collision-related sections, but all artwork, game design, UI, etc. was created by me (as well as most initial physics/collision logic)
- I heavily relied on the **Simple and Fast Multimedia Library (SFML)** in creating this game.

© Zahran Galib 2026
