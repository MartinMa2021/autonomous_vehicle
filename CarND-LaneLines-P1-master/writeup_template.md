# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps:
First, I converted the images to grayscale to reduce the number of channels
Second, I blurred the image using Gaussian blur to remove noise
Third, I thinned the edges using Canny edge (threshold is determined using Otsu's method)
Fourth, I identified the Region of Interest (RoI)
After examining the test images, it seems like a centered trapezoid would identify RoI
the best. 
	The bottom of the trapezoid accounts for 90% of the width of the picture.
	The height of the trapezoid accounts for 40% of the height of the picture.
	The top of the trapezoid acccounts for 10% of the width of the picture.
	The trapezoid is centered with the center of the picture.
	Note: the coordinate system's origin is on top left

Fifth, I found and drew the lines using Hough transform
After examining the example images and some trials:
	The resolution of r is set to 1 pixel
	The resolution of theta is set to 1 degree (pi/180)
	The threshold is set to 20 counts
	The minimum length to be considered as a line should be 80 pixels 
	The max line gap should be set to 200 pixels
When dividing many lines to 2 lines (left and right lane):
	Note: the coordinate system's origin is on top left
	If slope < 0, the line is part of left lane, otherwise right lane
	Count the line iif 20 degree < abs(arctan(slope)) < 60 degree, discard the line otherwise (the line is not part of left or right lane)
	Find the averages of left slopes and right slopes, find the averages of the left points and right points. (I initialled used medians but realized the lines are very jumpy image to image in the video, changing to means stablize the lanes)
	The left lane is the mean of the left slopes that passes through the median of the left points. The same things goes for the right lane



In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
