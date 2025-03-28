# OpenGL Project Setup Guide

Follow these steps to set up and build the OpenGL project.

## 1. Install Dependencies

First, update your package list and install necessary packages.

```bash
sudo apt-get update
sudo apt-get install cmake pkg-config
sudo apt-get install mesa-utils libglu1-mesa-dev freeglut3-dev mesa-common-dev
sudo apt-get install libglew-dev libglfw3-dev libglm-dev
sudo apt-get install libao-dev libmpg123-dev
```
## 2. Make your project folder and install files
make a new folder
```bash
mkdir openGL
```
```bash
cd openGL
git clone https://github.com/glfw/glfw.git
cd glfw
sudo cmake .
sudo make
sudo make install
```
## 3. Install GLAD Dependencies
To obtain the glad subdirectory. I did the following thing:
1. Go to [GLAD web service](https://glad.dav1d.de/)
2. Choose Language: C/C++, specification: OpenGL, API gl: Version 4.6, profile:Core
3. download the generated .zip folder and extract inside openGL folder.

## 4. See your first traingle using OpenGL pipeline
To build the executable, go inside the build diredtory and execute the following commands:
```bash
cd build
cmake ..
make
./OpenGL_Project
```
## 5. Resources
1. Articles by [Songhoo.ca](https://www.songho.ca/opengl/gl_sphere.html)
