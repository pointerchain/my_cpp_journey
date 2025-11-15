## 2025-11-14
- Made significant progress on `Pong Game` by integrating core systems **[cpp_pong](https://github.com/pointerchain/cpp_pong/tree/92cd05d768c87ce1be603f05eaa6baa5aaf508d2)**
    - Implemented `EventHandlingSystem` for *decoupled input* processing.
    - Added `PhysicsSystem` to handle entity movement and physics updates.
    - Created `BorderCheckingSystem` to keep entities within *game boundaries*.
    - Set up `RenderSystem` for drawing all game entities.
    - Updated `Game` class to manage window positioning and entity creation.
    - Trying to use the knowledge I read about yesterday.

## 2025-11-13
- Read the second chapter of `A Tour of C++ Third Edition by Bjarne Stroustrup`.
- Started setting up initial structure for a `Pong Game` **[cpp_pong](https://github.com/pointerchain/cpp_pong/tree/cfd1c929316d5fe66533d968dadd94d84dd85823)**
    - No actual pong elements yet, just applying the architectural patterns I learned today.
    - Trying to *implement everything properly* from the start based on what I read.
- Read *extensively* about `EnTT` and `SFML` integration and best practices.
    - Learned that `EnTT` is a *container, not a framework* - you control the main loop completely, just use the registry like any other data container.
    - Discovered `registry.ctx()` works as a *service locator* for global objects like `sf::RenderWindow`, keeping systems decoupled.
    - Use `entt::view` by default for most systems, only upgrade to `entt::group` when profiling reveals actual bottlenecks.
    - Learned to decouple input using `entt::dispatcher` - translate SFML events into game-specific events so systems listen to the dispatcher instead of SFML directly.
    - Components should be *Plain Old Data* (POD) only - no heavy objects like `sf::Sprite` inside components. Systems should use transient objects and map component data onto them.
    - Safe deletion pattern: tag entities with a `ToDestroy` component, then a `CleanupSystem` runs at the end of the loop to safely destroy them. *Never* call `registry.destroy()` inside iteration loops.
    - For collisions, use a dedicated spatial structure (like a `quadtree`) for broad-phase detection, then use ECS to get components for precise checks.
- Created a private project `CPP Sandbox` for fast testing and messing around in C++.
    - A simple codebase to quickly *prototype* and *experiment* with new C++ concepts without the overhead of setting up a full project each time.
    - Probably should of made this early lol.

## 2025-11-12
- Deep dive into `EnTT` and set up a fully functional project combining `EnTT` with `SFML` **[entt_testing](https://github.com/pointerchain/entt_testing/tree/a89101a2c5ed8b886653f31d065c9c55bdd3c5c2)**
    - Implemented several core `ECS systems` including `RenderSystem`, `PhysicsSystem`, and `InputSystem`.
    - Got *much more comfortable* with the `Entity Component System` architecture pattern.
    - Learned how to properly structure and organize systems to work together in the *game loop*.
    - I'd say I got the hang up of it *pretty fast*. I enjoy the `ECS pattern` and find it some what intuitive, planning to make bigger project soon with it.

## 2025-11-11
- Started learning about `EnTT` the `ECS library`.
    - Set up a small project for testing.
    - Learning to use along side `SFML`.
- Updated my `cpp_starter_template` to have `vcpkg` support and also added a `.clangd` file to help with linter problems **[cpp_start_template](https://github.com/pointerchain/cpp_starter_template/tree/469b749ce2eb4bf0a1e34e754f7ae4d5f8083c69)**
- Installed and set up `vcpkg`.
    - Set up path in `~/.bashrc`

## 2025-11-10
- Added an `Enemy` system to my `Roguelike Game` project **[roguelike_game](https://github.com/pointerchain/roguelike_game/tree/1726c5ec46b755cbc12547d86a948be417a42452)**
    - This was a *pretty big* update but I am happy so far with how it turned out, still a lot I want to add but this is just the start of it.
    - `Acceleration`-based movement, very similar to `Character`.
    - Implemented `Boids Separation` behavior to prevent enemies from *clumping together* too much.
    - Also set up a simple `State Machine`, currently with two possible states: `kIdle` and `kChasing` with a working *aggro range* to switch states.

## 2025-11-09
- Added a `Dashing` movement feature to my `Roguelike Game` **[roguelike_game](https://github.com/pointerchain/roguelike_game/tree/ccaf2caea63e2a3e91dc00301c48d8aaab9e460a)**
    - Moved away from constant move speed to an `acceleration`-based movement system.
    - Added a `CharacterState` enum class and `state_` character member to store the character's current state (kNormal, kDashing)
    - Added `dashing` by listening for spacebar down to activate a *burst of movement* in a specific direction.
    - Honestly *pretty happy* with how I implemented this, went *relatively smoothly*.
- Refactored all *game loop logic*, abstracting it out of main.cpp into a `Game` class **[roguelike_game](https://github.com/pointerchain/roguelike_game/tree/487f2be5d089fb09b5690f4b7d9a2a435b79803b)**
    - I didn't really like how all the logic was just in the main function, so I decided to move it to a *dedicated class* so that the *state* is easier to manage across function calls for *better organization*.
- Added a `Camera` system to my `Roguelike Game` project **[roguelike_game](https://github.com/pointerchain/roguelike_game/tree/0535c88e5466920a89f99a0a02c15ef6acf21a26)**
    - Created a `Camera` class and used `sf::View` to track the Character's sprite position.
- Added a `Map` system to my `Roguelike Game` project **[roguelike_game](https://github.com/pointerchain/roguelike_game/tree/917bcfbe0b18bffebf0dde053874ddeebbcd3888)**
    - Created a `Map` class and used `sf::VertexArray` to create a `tilemap`.
    - Learned a lot about *actually connecting* it with the proper `texture`.

## 2025-11-08
- Successfully created a C++ solution for the LeetCode problem `Climbing Stairs` **[0070_climbing_stairs](https://github.com/pointerchain/leetcode_solutions/tree/f8f3f50d860e0102223080f884752bb14f3f3326/0070_climbing_stairs)**
    - Got some *good practice* with `recursion` and learned about `memoization`.
- Updated `Roguelike Game` to have `sprite` support **[roguelike_game](https://github.com/pointerchain/roguelike_game/tree/49e6c87d9754dca1618d5b7843d012a9a9e03bc0)**
    - Got rid of the old `sf::RectangleShape` in favor of using `sf::Texture` and `sf::Sprite`.
    - Downloaded a *free* sprite pack from `itch.io` to use for the game.
    - Had to use `setTextureRect` because the PNG was a `sprite sheet`.
    - Got the sprite to flip using `setScale` so the sprite *properly faces* the direction the character is moving.
- Created a `Roguelike Game` project on GitHub **[roguelike_game](https://github.com/pointerchain/roguelike_game/tree/d5bfc84ed07e6d6091fe4a9a47550c33ef68808b)**
    - I decided to move away from the `2D Platformer` in favor of making a `Roguelike Game` instead, just thought it would be a *little more fun*.
    - Set up simple `Character` class, very similar to my `2d_platformer` game with some *refinements*.
    - Created an `Input` namespace for input-related functions.
    - Created a `Config` namespace for game constants, similar to `2d_platformer`.
- In `cpp_starter_template`, updated `README.md` to include requirements/build information and updated `CMakeLists.txt` to have proper target_include_directories support for /include **[cpp_starter_template](https://github.com/pointerchain/cpp_starter_template/tree/9638d719d783fa148b52552d9d3926a11d1a8583)**
- Updated `README.md` and `CMakeLists.txt` in `2d_platformer` to properly reflect name change and added more information to `README.md` **[2d_platformer](https://github.com/pointerchain/2d_platformer/tree/6b2cf30c3bbb59784d7cd3f0a49acd8419ae005a)**
- Going to try to add `Requirements` and `Build` sections to all my future project's `README.md`s for *easier usage*.
- Been learning about `Conventional Commits`.
    - Using proper `Types` (feat: / fix: / refactor: / etc).
    - Using `Imperative Mood` ("Add x" rather than "Added x").
    - Use `(scope)` to easily give *extra context* on what this change directly affects (fix(player): Jump collision bug).
    - Probably should have got this down earlier but will be trying to *hammer it down* for all my commit messages going forward.
- Renamed GitHub repo for `cpp_sfml_testing` to `2d_platformer` to reflect the actual project better.
- Big refactor for my 2D Platformer **[cpp_sfml_testing](https://github.com/pointerchain/cpp_sfml_testing/tree/655642f801e7e813924101686a2ff9adb85b80c3)**
    - *Encapsulated* logic for character-esque logic to a concrete `Character` class (with respective .hpp and .cpp) that handles all character-related logic.
    - Moved away from using different variables to hold stats "in_air" to a proper enum class `ActionState` that is encapsulated inside Character.
    - Created a struct `PlayerInput` to merge player input logic for better *scalability* over passing each as their own variable directly as arguments.
    - Created a `config.hpp` header to hold game *constants*.
- Added `jumping capabilities` to my 2D Platformer **[cpp_sfml_testing](https://github.com/pointerchain/cpp_sfml_testing/tree/f23c025e6d14d06c85a87d74ef187331e5032deb)**

## 2025-11-07
- Created a `C++ SFML Testing` project on GitHub **[cpp_sfml_testing](https://github.com/pointerchain/cpp_sfml_testing/tree/7d5a6f24e353659a0b3b009dc66fc375bce9a861)**
    - This is my *first time ever* using an `external C++ library`. Had to download and correctly set up the `CMakeLists.txt`.
    - This kind of turned into a `2D Platformer`.
    - You can move left and right using `A` and `D`. (Originally had `W` and `S` support as well but changed it for gravity instead)
    - I also added `gravity` and `collision checking` for window boundaries.
    - It's kind of a *lot of little things* I did that I don't think are worth typing them all out here but you can always look at the repo.

## 2025-11-06
- Successfully created a C++ solution for the LeetCode problem `Plus One` **[0066_plus_one](https://github.com/pointerchain/leetcode_solutions/tree/989f23893c630fd89c5684298f962e3d7b223be5/0066_plus_one)**
- Successfully added `task priority` support for adding new tasks by prefixing it with a tag `[h/m/l]` **[cpp_todo_list_utility](https://github.com/pointerchain/cpp_todo_list_utility/tree/d2569d08a0ac0850c5100c69ad20f224afcaca48)**
    - Got a lot more *comfortable* working with `std::string` and `std::stringstream`.
    - Learned about `lambdas [&]() {};` and also learned about `IIFE [&]() {}();` which I needed to use because my FileEditor does not have a `default constructor`.
- Added a utils.hpp file for simple inline functions for cpp_todo_list_utility **[cpp_todo_list_utility](https://github.com/pointerchain/cpp_todo_list_utility/tree/1b80ef63cd9dc170c213a3e7c406eac075c986a3)**
    - Learned about using `inline` for *simple helpers* where it's preferred to only have a header file versus a header file and source file.

## 2025-11-05
- Successfully got interactive mode working for cpp_todo_list_utility **[cpp_todo_list_utility](https://github.com/pointerchain/cpp_todo_list_utility/tree/dfe54b69fd311583b7e22b2e28e2614d376874a2)**
    - Went *smoothly* for the most part, happy with the result.

## 2025-11-04
- Worked on the interactive mode for the cpp_todo_list_utility, didn't get a working version yet. Going to finish tomorrow.
- Learned about some *string parsing techniques* like using `std::stringstream`.

## 2025-11-03
- Completed a *major refactor* and feature update for the cpp_todo_list_utility **[cpp_todo_list_utility](https://github.com/pointerchain/cpp_todo_list_utility/commit/7067e85f1f499f7d6e75e1c97918366f61d47821)**
    - Refactored the application by introducing a new `TodoList` class, abstracting all *business logic* away from main.
    - Added *several new features*, including `edit`, `done`, `clear`, and `help` commands, complete with *short aliases* (e.g., e, d, c, h).
    - Implemented the done functionality to move *completed tasks* from todo.txt to a new done.txt file.
    - *Modernized* the project's error handling by replacing `C-Style integer return codes` with `std::expected` and `custom error enums` (TodoListError, FileEditorError).
    - Enhanced the `FileEditor` class with new `EditLine`, `GetLine`, and `Delete` methods to support the new features.
    - Improved `command-line argument parsing` to correctly handle *multi-word task inputs*.

## 2025-11-02
- Successfully created a C++ solution for the LeetCode problem `Remove Element` **[0027_remove_element](https://github.com/pointerchain/leetcode_solutions/tree/af0efd533199c6bda9883a443b6243be856d7aca/0027_remove_element)**
- Read more about `CMake` and also read about using `package managers` like `vcpkg`.
- Also read about `JSON` and `Protobuf` which help avoid the *headaches* of compatibility and versioning.
- Read a lot about files and writing in `binary mode`, learned about `versioning` and `serialization`.

## 2025-11-01
- Created a Command-Line Utility `C++ To-Do List Utility` **[cpp_todo_list_utility](https://github.com/pointerchain/cpp_todo_list_utility/tree/4abadb67bf9aebd8ef84ef556dfd695fb2384009)**
    - Took me around two hours. Was a *little rocky* but I pulled through.
    - Learned a lot about `Command-Line Arguments`.
    - Learned a lot about working with the *File System* in C++ using `fstream` and `filesystem`.
    - Improved my knowledge of *catching exceptions*.
    - Really tried to *hammer in good practices* and modern C++ idioms, though it's obviously a WIP.
- Fixed a bunch of VS Code config issues and updated `settings.json` to work with Clang.
- Switched from using `GCC` to `Clang`.
- Downloaded and started using the `GitHub CLI`.
- Created a C++ starter template GitHub template project **[cpp_starter_template](https://github.com/pointerchain/cpp_starter_template)**
    - Learned about CMakePresets.json
- Took a break but I am now *getting back on the grind*.

## 2025-10-23
- Successfully created a C++ solution for the LeetCode problem `Valid Parentheses` **[0020_valid_parentheses](https://github.com/pointerchain/leetcode_solutions/tree/8c25db692b95652fcd13c8f23d0b1e2f6ece3e13/0020_valid_parentheses)**
    - Learned about `std::stack`.
- Installed the *terminal multiplexer* `zellij`.

## 2025-10-22
- Learned about *proper naming conventions* according to the Google Style Guide for C++.
- Read the second chapter of `A Tour of C++ Third Edition by Bjarne Stroustrup`.
- Did some research into `neovim`, thinking about switching from `VS Code` to `neovim`.
- Successfully created a C++ solution for the LeetCode problem `Roman to Integer` **[0013_roman_to_integer](https://github.com/pointerchain/leetcode_solutions/tree/d6a34cbe57ccabfb61d802cff7e15f18fc7833f0/0013_roman_to_integer)**

## 2025-10-21
- Successfully created my *first* C++ solution for the LeetCode problem `Two Sum` **[0001_two_sum](https://github.com/pointerchain/leetcode_solutions/tree/8648d6acc5e577919ba518c975ee7280c1dd08df/0001_two_sum)**
- Made a GitHub repo for LeetCode solutions **[leetcode_solutions](https://github.com/pointerchain/leetcode_solutions)**
- Updated/Refactored the `C++ Rock Paper Scissors`, moving over to **C++23** from **C++20** **[cpp_rock_paper_scissors](https://github.com/pointerchain/cpp_rock_paper_scissors/tree/17006e4f783e4b4259da433b7e74fd3c9b11a0bf)**
    - Took me around 15 minutes to update it. Was planning on sticking with C++20 and under for a little while but decided to just go to C++23 because I think it will be *more beneficial* in the long run.
    - Learned about using `std::print`, `std::println`, and `std::unreachable`.
- Created a console-based `C++ Rock Paper Scissors` application **[cpp_rock_paper_scissors](https://github.com/pointerchain/cpp_rock_paper_scissors/tree/2c349137b2d187d980a3bcf6dd214c399e72a099)**
    - Took me around an hour and a half to write, felt happy with the results.
    - Learned about `std::unordered_map`, practiced using `enum class`, learned how to use `static` local variables *effectively*, and a *lot more*.
    - Learned a lot about *modern ways* to generate random numbers, using `std::random_device`, `std::mt19937`, and `std::uniform_int_distribution`.

## 2025-10-20
- Spent most of the day taking care of my dog after he had his teeth pulled.
- Read the first chapter of `A Tour of C++ Third Edition by Bjarne Stroustrup`.

## 2025-10-19
- Created a console-based `C++ Calculator` application **[cpp_calculator](https://github.com/pointerchain/cpp_calculator/tree/42b5cceeb532d98bd5c1b34d91f5128bd9170014)**
    - This was my first project using the complete workflow, and I'm proud of how it went.
    - Took me around 45 minutes to write, actually had a good amount of fun and went pretty smoothly.
    - Learned a lot about how to properly use `std::cin`, how to write good *robust* and *safe* code.
    - Got some good practice with *control flow* and *minimizing variable scope*. 
- Practiced making `CMakeLists.txt` from scratch; got comfortable with it after a few projects.
- Practiced C++ project creation workflow (`mkdir` -> `git init` -> `mkdir src include build` -> etc).
- Installed `alacritty` and set up as default terminal emulator over the prepackaged one.
- Re-set up all of Fedora environment, installing packages and fixing configs.
- Installed a fresh Fedora 42 i3 Spin because of Nvidia compatibility issues with Wayland.

## 2025-10-18
- Installed the C++ development toolchain (`g++`, `clang++`, `gdb`, `make`, `cmake`).
- Set up a bunch of CLI tools like `fzf`, `zoxide`, and `git`.
- Committed my first code repo **[pointerchain](https://github.com/pointerchain/pointerchain)**
- Set up VS Code on new Fedora 42 Sway Spin.
- Reinstalled a fresh Fedora 42 Sway Spin and deleted the old boot partition.
- Created a new Gmail and GitHub account for my new C++ journey. 
- Set up GitHub repos **[Profile README](https://github.com/pointerchain/pointerchain)** and **[Done List](https://github.com/pointerchain/my_cpp_journey)**. `[Admin]`
- **The start of my C++ and Linux journey! Wish me luck!**