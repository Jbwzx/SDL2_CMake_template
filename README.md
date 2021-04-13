# SDL2 Starter template using CMake
*Time to time I see people struggle setting up SDL2 with CMake on their machines. This template project shows one of the possible solutions to do so.*

### This template:
 - Has SDL2 as [git submodule](https://git-scm.com/book/en/v2/Git-Tools-Submodules) 
 - Fetches && sets up [SDL2](https://www.libsdl.org/) library for use in the project

## Installation guide
 1. Clone repository to your desired location
 2. Run cmake
	 1. IDEs and text editors with CMake support / extensions will pick everything up automatically
	 2. For manual build: from repository's root directory run `cmake -S . -B build` command, where `.` is your source directory and `build` is build one.
3. Wait for CMake to finish fetching SDL2, index files and build program
4. When finished program can be run where simple SDL2 window will be present