# guess-game

## Requirements

Make a guessing game.

- Define a function called getRandomGuessableNumber that matches the signature in guess.hpp
- Create the game's main loop
  - While the game is running, it should prompt the user to guess an integer between a minimum and a maximum value
  - If they guess incorrectly it should tell them if they are too low or too high
  - If they enter a non-integer it should tell them their guess is invalid
  - If they guess correctly they should be asked if they wish to play again
- All source files should go in `src/guess`

### Hints

- `src/guess/guess.hpp` contains preprocessor defines for prompt strings and other constants
- To generate a random number you can use `<random>` or rand in `stdlib.h`. Here is an example using `<random>`:

```c++
int32_t getRandomGuessableNumber(int32_t min, int32_t max)
{
    if (min > max)
    {
        throw std::invalid_argument("min must be <= max");
    }

    std::random_device rd;
    // Use mt19937 seeded from random_device for reproducible non-determinism
    std::mt19937 gen(rd());
    std::uniform_int_distribution<int32_t> dist(min, max);
    return dist(gen);
}
```

- You can manage input and output to the console using `std::cout`, `std::cin` & `std::getline`. See [cpp-io](https://en.cppreference.com/w/cpp/io.html) for more options
- Format strings into fixed-size character buffers using `std::snprintf`

## Bonus

- Create your own implementation of a pseudo-random number generator ([PRNG](https://en.wikipedia.org/wiki/Pseudorandom_number_generator))
- There are many different algorithms one could use for a pRNG, one option is a [linear congruential generator](https://en.wikipedia.org/wiki/Linear_congruential_generator)
- Your generator function should initialize a seed value the first time it is run, and use each returned result as the next seed.

## Building

```shell
cmake -S . -B build
cmake --build build --config Debug
./build/Debug/guess_game.exe
```

### Note

In these assignments we provide a `CMakeLists.txt` that contains build instructions for the sake of automating and standardizing building and testing, but don't forget that compiling code is often as simple as choosing a compiler, providing inputs, and asking for outputs. Sometimes those outputs need to be combined using a linker, or you will need to ask the compiler to enable optional features, but don't let the verbosity of build systems obfuscate that.

Try building your program directly with a compiler:

Windows (MSVC `cl`):

```powershell
# Adjust sources as needed; example if your entry point is src/main.cpp. Use a * if you want to grab all cpp files in a directory
cl /std:c++17 /I src src\main.cpp /Fe:guess_game.exe
cl /std:c++17 /I src src\*.cpp /Fe:guess_game.exe
```

Linux/macOS (GCC/Clang):

```bash
# Adjust sources as needed; example if your entry point is src/main.cpp. Use a * if you want to grab all cpp files in a directory
g++ -std=c++17 -Isrc -o guess_game src/main.cpp
g++ -std=c++17 -Isrc -o guess_game src/*.cpp
```
