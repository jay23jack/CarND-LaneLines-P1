# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/pipeline.png

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of a few steps:
1. converted the images to grayscale and applied gaussian smoothing
1. used Canny Edge Detection to find the pixels of the edges
1. used a four sided polygon to filter out pixels from the region of interest
1. run Hough Line Gransform to detect line segments from the pixels

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by:
1. partition line segments into left lines and right lines based on the X axis
1. average left line segments by extrapolating each segment to a full line and calcuating the x_low and x_high, and then averaging them based on segment length.  
1. in the average function, I also exclude segments with absolute slope angle less than 20 degree, to account for some horizontal white lines in the second video.

Here're the images to show how the pipeline works: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline

Potential shortcomings include:
1. the four sided polygon may not be generalizable.  I used hard-coded ratio to find the polygon.
1. the average function is a bit ad-hoc. 


### 3. Suggest possible improvements to your pipeline

Possible improvements:
1. the pipeline only processes images individually and didn't leverage adjacent images and the fact that lanes are continuous. that can make the lane prediction more smooth. 
