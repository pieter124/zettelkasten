
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



**References**
*Pikuma's*
**2D Game Engine Course**
