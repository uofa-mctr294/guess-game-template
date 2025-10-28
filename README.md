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
- Format string into fixed-sized character buffers using `std::snprintf`

## Building

```shell
cmake -S . -B build
cmake --build build --config Debug
build\Debug\guess_game.exe
```

## Testing

[Build](#building)

```shell
ctest --test-dir build -C Debug
Add -V for verbose testing
```
