
2025-07-08 

Tags: [[project]] [[programming]]

# **Displaying the Game Window**

**Game Loop**
At a very abstracted view, the game loop is processing input, then updating the game and finally rendering it to the user.

So:
- **Process the input**
- **Update the game**
- **Render to user**

```cpp
while (true) {
	game->processInput();
	game->update();
	game->render();
}
```

This will happen depending on our frame rate we set on the game.

**Game Class**
When building a project, it is a good idea to think through levels of abstraction to de-clutter the phase where you start building / implementing.

In the header files, we do not declare the body of the functions.

Game.h
```cpp
class Game {
	private:
		//...
	public:
		Game();
		~Game();
		void Initialize();
		void Run();
		void ProcessInput();
		void Update();
		void Render();
		void Destroy();
};
```

In the .cpp file, the first thing you need to do is include the header file within quotation marks. 

But why are some quotation marks and some angled brackets? 
The quick answer to that is, whenever you include things between angled brackets, the compiler is going to look in the operating system, include folders, so the compiler knows how to resolve the include statement. Since our file is in the same folder, we can use quotation marks.

Game.cpp
```cpp
#include "Game.h"

Game::Game() {

}
```

The $\text{Game::Game()}$ statement follows as so:
The scope resolution -> The function name -> The body of the function.

Every header file we create, we need to always add what we call a $\text{protection guard}$.

Protection guard:
```cpp
#ifndef GAME_H
#define GAME_H

/* Header file code.....
...
...
*/
#endif
```

This is just a way of us protecting the pre-processor from, including the header file multiple times in our project.

Instead of using this type of guard, some developers like to use something called
$\text{\#pragma once}$ at the top of their header files. The "$\text{\#pragma once}$" does virtually the same thing, and it has the benefit of us not having to remember to change the name of the definition in every .h file we create. This is not standard, meaning it is "implementation specific" (not portable and depends on how each compiler decides to implement it).

The constructor method is called when the game object is declared. Since we are not using the $\text{"new"}$ keyword to create the object, the object will be stored on the $\text{stack}$ and will be destroyed when the scope ends.

**Creating an SDL Window**

If we want to open windows in a certain operating system, we have to invoke operating system specific functions to open that window. Thankfully, SDL handles all this for us.
We use $\text{SDL\_Init(SDL\_INIT\_EVERYTHING)}$ to initialise the graphics, the keyboard, the input.

What if our user's machine doesn't have a graphical interface, like a linux server?
$\text{SDL\_Init}$ will return 0 if everything was okay or some other number corresponding to the error code.

To create an $\text{SDL\_Window}$ we have to create a pointer to the $\text{SDL\_Window}$ struct.
We also need to create something called a renderer. This lets us draw things inside the window.

Must always check if a null pointer is returned and exit the program if so.

```cpp
void Game::Initialize() {

if (SDL_Init(SDL_INIT_EVERYTHING) != 0) {

std::cerr << "Error initializing SDL." << std::endl;

return;

}

window = SDL_CreateWindow(NULL, SDL_WINDOWPOS_CENTERED, SDL_WINDOWPOS_CENTERED,

800,

600,

SDL_WINDOW_BORDERLESS

);

if (!window) {

std::cerr << "Error creating SDL window." << std::endl;

return;

}

renderer = SDL_CreateRenderer(window, -1, 0);

if (!renderer) {

std::cerr << "Error creating SDL renderer." << std::endl;

}

}
```

**Polling SDL Events**

We need to clean up resources after the program has finished, destroying the SDL items we have made. However, we declared the window and the renderer locally inside the $\text{Initialize}$ function. So we have to store the declaration in the header file, inside the private identifier. This is so all methods can have access to the member variables that is the SDL window and renderer.

When destroying the SDL items, we must destroy in a specific order, so the renderer, the window then closing the SDL state. 

```cpp
void Game::Destroy() {

SDL_DestroyRenderer(renderer);

SDL_DestroyWindow(window);

SDL_Quit();

std::cout << "Game destroyed!" << std::endl;

}
```

Now we want to implement the user pressing the escape key to quit the loop. We need to use something called an SDL event. We also need to add an SDL poll event to check for pending events in the event queue and process them without blocking the program.

But several things can happen in our system in one frame, so we have to keep polling. This is put into a while loop as our main loop condition.

**Rendering our SDL Window**

We use $\text{SDL\_SetRenderDrawColor}$ to draw a solid colour on the canvas of the window.
We then clear the renderer with $\text{SDL\_RenderClear}$ and draw / present it with $\text{SDL\_RenderPresent}$.

Now we have a displayed window!

Code for rendering:
```cpp
void Game::Render() {

SDL_SetRenderDrawColor(renderer, 255, 255, 255, 255);
SDL_RenderClear(renderer);  

// TODO: Render all game objects.

SDL_RenderPresent(renderer);
}
```

**Fullscreen Window**

We should have a public member variable that keeps track of the window width and window height. We pass that into the create window function. There is a special SDL struct called $\text{SDL\_DisplayMode}$ which has functions to retrieve the current width and height of our screen.

Code change:
```cpp
SDL_DisplayMode displayMode;
SDL_GetCurrentDisplayMode(0, &displayMode);

windowWidth = displayMode.w;
windowHeight = displayMode.h;

window = SDL_CreateWindow(NULL, SDL_WINDOWPOS_CENTERED, SDL_WINDOWPOS_CENTERED,
windowWidth,
windowHeight,
SDL_WINDOW_BORDERLESS
);
```

This is a very C-style way of doing things. 
This is what is called a fake fullscreen as the video mode was not actually changed to fullscreen.

**Fake Fullscreen & Real Fullscreen**

There is a problem though, let us say the user has a very small screen, if we use fake fullscreen, then we just fill the screen up. And if we are playing against a user that has a much larger screen, they would be able to see much more of the map. Essentially, we do not want to give people with larger screens an advantage. 
So we have to give our game engine / game a fixed size.

**SDL GPU Acceleration & VSync**

SDL is a very smart library. By default, it will try to figure out if your system has a dedicated graphics card and use it to render screen objects.

When we invoke $\text{SDL\_CreateRenderer}$, we can manually instruct SDL to try to use accelerated GPU. This should be SDL's default behaviour anyway, but if you want to force the system to try finding a GPU, you can pass a special flag at the end of the $\text{SDL\_CreateRenderer}$ call:

```cpp
SDL_CreateRenderer(
window,
-1
SDL_RENDERER_ACCELERATED
)
```

And since we are talking about these special renderer flags, there's another one that I think we should pay attention to. SDL allows us to send a flag to force synchronization with VSync. VSync (or vertical sync) is a graphics technology that synchronizes the frame rate of a game with a gaming monitor's refresh rate. Enabling VSync will prevent some screen tearing artifacts when we display displaying our objects in our game loop, as it will try to synchronize the rendering of our frame with the refresh rate of the monitor.

Keep in mind that enabling VSync can (and most likely will) affect your FPS. For example, your game might be running at 3000 FPS but if your monitor runs at 60Hz, your frames per second with VSync will drop to 60 FPS. Of course, your rendering FPS will be limited but you can find ways of still updating the game's logic or physics step more than 60 FPS.

Therefore, we can also go ahead and manually instruct the SDL renderer that we want to use VSync. We can join both flags using a bitwise "or" operator:

```cpp
SDL_CreateRenderer(
window,
-1
SDL_RENDERER_ACCELERATED | SDL_RENDERER_PRESENTVSYNC
);
```

This will use both flags, telling SDL to use hardware acceleration and also use VSync to prevent any screen tearing in the future.

**References**
*Pikuma's*
**2D Game Engine Course**
