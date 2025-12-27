# Quickstart: miniRT

This guide provides the basic steps to build and run the `miniRT` ray tracer.

## Prerequisites

- A C compiler (e.g., `gcc` or `clang`)
- `make`
- The SDL2 library installed on your system.

### SDL2 Installation

**macOS (using Homebrew):**
```sh
brew install sdl2
```

**Debian/Ubuntu:**
```sh
sudo apt-get update
sudo apt-get install libsdl2-dev
```

## Building the Project

1.  Clone the repository.
2.  Navigate to the project's root directory.
3.  Run `make` to build the executable.

```sh
git clone <repository_url>
cd miniRT
make
```

This will create the `miniRT` executable in the root directory.

## Running the Application

To render a scene, provide the path to a `.rt` scene file as a command-line argument.

```sh
./miniRT scenes/example.rt
```

A window will appear displaying the rendered image.

- To **close the window**, press the `ESC` key or click the window's close button.

## Cleaning Up

To remove the executable and object files, run:
```sh
make clean
```

To remove all generated files, including the executable:
```sh
make fclean
```
