[Home](https://paulovictorcorreia.github.io/)

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

## 2. Manipulating pixels on an image

On this section, we're going to see how we can manipulate pixels on OpenCV.

### 2.1 Regions

This exercise asks us to make a program in which asks the user for 2 points on a two dimentional plane, P1 and P2, and then draw a rectangle with the inverted colors of the pixels in the area of the rectangle.

The base image we used is:
![Base image for the exercises on section 2]
(biel.png)

For this first exercise, we wrote the following code:
```c++
#include <iostream>
#include <opencv2/opencv.hpp>

using namespace cv;
using namespace std;

int main(int, char**){
  Mat image;
  int P1[2], P2[2];//points in which the user determines the area of the rectangle
  uchar aux;//Auxiliar variable to help inverting the colors
  int minX, minY;//minimum values of parameters X and Y of the rectangle
  int maxX, maxY;//maximum values of parameters X and Y of the rectangle
  int rows, cols;
  //write the image file into a Mat object
  image= imread("biel.png",CV_LOAD_IMAGE_GRAYSCALE);
  if(!image.data){
    cout << "nao abriu biel.png" << endl;
    exit(0);
  }
  rows = image.rows;//number of rows
  cols = image.cols;//number of columns  
  //read area that user wishes to invert the colors
  //and do this only, if only, the given area is
  //valid within the size of the image
  do{
    cout << "P1(x, y): ";
    cin >> P1[0];
    cin >> P1[1];
    cout << "P2(x, y): ";
    cin >> P2[0];
    cin >> P2[1];
  }while((P1[0]>rows) || (P2[0]>rows) || (P1[1]>cols) || (P2[1]>cols));

  //Condition that checks the minimum and maximum
  //values of the cordinate X
  if(P1[0] > P2[0]){
    minX = P2[0];
    maxX = P1[0];
  }
  else{
    minX = P1[0];
    maxX = P2[0];
  }
  //Condition that checks the minimum and maximum
  //values of the cordinate Y
  if(P1[1] > P2[1]){
    minY = P2[1];
    maxY = P1[1];
  }
  else{
    minY = P1[1];
    maxY = P2[1];
  }
  //loop that uses the ranges previously determined to invert
  //the colors of each pixel on grayscale
  for(int i=minX;i<maxX;i++){
    for(int j=minY;j<maxY;j++){
      aux = image.at<uchar>(i,j);
      image.at<uchar>(i,j) = 255 - aux;
    }
  }
  //shows image on a window
  imshow("janela", image);  
  waitKey();

  return 0;
}

```

The entry command on the Linux terminal was this:

![Command line entry]
(terminal_regions.png)

And, finally, the output picture of the inverted colors on _biel.png_ picture:
![Inverted region of the picture]
(biel_regions.png)
