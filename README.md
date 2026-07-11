# Flappy-Bird

Midnight Flappy Bird
A sleek, modern recreation of the classic arcade mechanics built entirely with HTML5 Canvas, pure JavaScript, and CSS. This project features a dark-mode "cyberpunk" aesthetic, utilizing canvas shadow effects to create glowing neon visuals for the player character, obstacles, and typography.

**Features**
HTML5 Canvas Rendering: Utilizes the Canvas API for high-performance 2D rendering and smooth frame updates.

Neon Visual Design: Employs ctx.shadowBlur and ctx.shadowColor to create a glowing yellow player avatar, cyan pipes with cap detailing, and a striking crimson "System Crash" game-over screen.

Custom Physics Engine: Implements continuous gravity and velocity variables to create a smooth, responsive falling and jumping arc.

Dynamic Obstacle Generation: Procedurally generates pipe obstacles with randomized vertical positioning while maintaining a consistent, navigable gap.

Responsive Controls: Supports both keyboard (Spacebar) and mouse/touch (Click) inputs for universal accessibility.

**How to Play**
Start the Game: Click the canvas or press the Spacebar to make your first jump. The game begins immediately.

Navigate: Repeatedly click or press Spacebar to apply upward lift, fighting gravity to navigate through the gaps in the approaching neon pipes.

Score Points: Each pipe successfully bypassed adds a point to your glowing counter at the top of the screen.

Reboot: If you hit a pipe, the ceiling, or the floor, the system crashes. Click or press Spacebar once more to instantly restart your run.

**JavaScript Architecture & Core Functions**
The game's logic is structured around a continuous rendering loop and modular functions that handle physics, rendering, and state management.

Game Loop & Rendering
gameLoop(): The heartbeat of the application. It utilizes requestAnimationFrame(gameLoop) to sync the game's update and draw cycles with the monitor's refresh rate, ensuring smooth, tear-free animation.

draw(): Responsible for clearing the canvas (ctx.clearRect) and repainting all visual elements on every frame. It handles the specific styling, such as the glowing roundRect for the bird, the multi-layered rectangles for the pipes to create visual depth, and the overlay UI during a "System Crash" state.

**Physics & Entity Management**
update(): Handles all mathematical state changes per frame before they are drawn.

Applies the gravity constant (0.4) to the bird's velocity, and updates the bird's vertical y position.

Moves all existing pipes to the left by decrementing their x coordinates.

Removes pipes from the array memory once they pass the left edge of the screen using splice(), preventing memory leaks.

spawnPipe(): Triggered every 100 frames. It calculates a random vertical anchor point (topHeight) within a constrained mathematical range and pushes a new pipe object—containing x, top, bottom, and width coordinates—into the pipes array.

**Interaction & Collision Logic**
flap(): The input handler. If the game is active, it resets the bird's downward velocity to a negative lift value (-7), causing the bird to jump. If the gameOver flag is true, triggering flap() reroutes to resetGame() instead.

Collision Detection: Embedded within the update() loop, this logic continuously checks for Axis-Aligned Bounding Box (AABB) intersections. It compares the bird's coordinate boundaries against every active pipe's boundaries, as well as the canvas floor and ceiling. If an intersection is detected, it flips the gameOver flag to true, halting the physics engine.
