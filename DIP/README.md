## Introduction

As we have knowledge, we, as humans, want to reduce the amount of work done by us and substitute for machines. Digital Image Processing is making us one step closer to this.

This page contains the exercises of DIP course lectured by Professor Agostinho Brito Jr, and by that we have an apresentation of the problems and how we solved them, including codes, input images and output images. Check this subject repository clicking [here](https://github.com/paulovictorcorreia/Digital-Image-Processing), where every file and picture we talk about is.

## 1. Initial Concepts

There were no exercises on this section, but we have to present the makefile for compiling the code and the various modules of the OpenCV library: 
```makefile
.SUFFIXES:
.SUFFIXES: .c .cpp

CC = gcc
GCC = g++

.c:
	$(CC) -I$(INCDIR) $(CFLAGS) $< $(GL_LIBS) -o $@

.cpp:
	$(GCC) -Wall -Wunused -std=c++11 -O2 `pkg-config --cflags opencv` $< -o $@ `pkg-config --libs opencv`


```

For compiling a single c++ file, we must execute the following command for a filename.cpp file:
` $ make filename `
