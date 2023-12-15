# OpenGL Setup with Visual Studio 2019

## Introduction
This repository provides guidance on setting up OpenGL within Visual Studio 2019. Included is a sample code demonstrating the Midpoint Ellipse Algorithm for drawing ellipses.

## Setup Instructions

### Step 1: Download GLUT Files
Download the necessary GLUT files pre-compiled for Intel platforms:
- **Option 1:** Download the [glutdlls37beta.zip file](https://www.opengl.org/resources/libraries/glut/glut_downloads.php) from the official website.
- **Option 2:** Alternatively, use the provided ZIP file from this repository.

### Step 2: File Placement
Follow these instructions to place the downloaded files correctly:
- **glut.h**: Copy to:
  C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\VC\Auxiliary\VS\include\gl
- **glut.lib**: Paste in:
  C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\VC\Auxiliary\VS\lib\x64
- **glut32.lib**: Add to:
  C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\VC\Auxiliary\VS\lib\x86
- **glut.dll** and **glut32.dll**: Place in:
  C:\Windows\SysWOW64
- **glut32.dll**: Finally, copy to:
  C:\Windows\System32


## Sample Code

### Code Snippet
Here's a code snippet demonstrating the Midpoint Ellipse Algorithm for drawing ellipses using OpenGL:
```cpp
#include <GL/glut.h>
#include<iostream>
using namespace std;
int rx = 100, ry = 125;
int xCenter = 250, yCenter = 250;

void myinit(void)
{
	glClearColor(1.0, 1.0, 1.0, 0.0);
	glMatrixMode(GL_PROJECTION);
	glLoadIdentity();
	gluOrtho2D(0.0, 640.0, 0.0, 480.0);
}

void setPixel(GLint x, GLint y)
{
	glBegin(GL_POINTS);
	glVertex2i(x, y);
	glEnd();
}
void ellipseMidPoint()
{
	float x = 0;
	float y = ry;
	float p1 = ry * ry - (rx * rx) * ry + (rx * rx) * (0.25);
	float dx = 2 * (ry * ry) * x;
	float dy = 2 * (rx * rx) * y;
	glColor3ub(rand() % 255, rand() % 255, rand() % 255);
	while (dx < dy)
	{
		setPixel(xCenter + x, yCenter + y);
		setPixel(xCenter - x, yCenter + y);
		setPixel(xCenter + x, yCenter - y);
		setPixel(xCenter - x, yCenter - y);
		if (p1 < 0)
		{
			x = x + 1;
			dx = 2 * (ry * ry) * x;
			p1 = p1 + dx + (ry * ry);
		}
		else
		{
			x = x + 1;
			y = y - 1;
			dx = 2 * (ry * ry) * x;
			dy = 2 * (rx * rx) * y;
			p1 = p1 + dx - dy + (ry * ry);
		}
	}
	glFlush();

	float p2 = (ry * ry) * (x + 0.5) * (x + 0.5) + (rx * rx) * (y
		- 1) * (y - 1) - (rx * rx) * (ry * ry);
	glColor3ub(rand() % 255, rand() % 255, rand() % 255);
	while (y > 0)
	{
		setPixel(xCenter + x, yCenter + y);
		setPixel(xCenter - x, yCenter + y);
		setPixel(xCenter + x, yCenter - y);
		setPixel(xCenter - x, yCenter - y);
		if (p2 > 0)
		{
			x = x;
			y = y - 1;
			dy = 2 * (rx * rx) * y;
			p2 = p2 - dy + (rx * rx);
		}
		else
		{
			x = x + 1;
			y = y - 1;
			dy = dy - 2 * (rx * rx);
			dx = dx + 2 * (ry * ry);
			p2 = p2 + dx -
				dy + (rx * rx);
		}
	}
	glFlush();
}
void display()
{
	glClear(GL_COLOR_BUFFER_BIT);
	glColor3f(1.0, 0.0, 0.0);
	glPointSize(2.0);
	ellipseMidPoint();
	glFlush();
}
int main(int argc, char** argv)
{
	glutInit(&argc, argv);
	glutInitWindowSize(640, 480);
	glutInitWindowPosition(10, 10);
	glutCreateWindow("User_Name");
	myinit();
	glutDisplayFunc(display);
	glutMainLoop();
	return 0;
}
```
## Output

### Image Result
![output of sample code](https://media.geeksforgeeks.org/wp-content/uploads/20210223002929/Screenshot315.png)
