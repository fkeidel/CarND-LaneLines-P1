# **Finding Lane Lines on the Road** 

## Writeup

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection

### 1. Describe your pipeline. 

	The lane finding pipeline consists of 11 steps.
	Since color is not relevant to edge detection, in the first step, the original image is converted into gray scale.
	Because noise can disturb the edge detection algorithm, in the second step, noise is reduced with an gaussian filter with kernel size 5.
	In step 3 edges are detected with the canny algorithm.
    In step 4 a polygon is created, which is used in step 5 to mask a region of interest (ROI).
    In step 6 the detected edges in the ROI are converted into a list of line segments with the help of a Hough line transformation.
    Then, in step 7 the line segments get classified into left an right lines by discriminating with the help of the line gradient.
    In step 8, the left and right line segments, are merged to one line each by using a median filter over the gradients and intersections of the line segments. 
    To prepare for drawing the lines, in step 9, the vanishing point is calculated by intersecting the left and right line. The vanishing point is used as the upper endpoint of both lines, the left and right line respectively.
    To get the lower endpoints of the lines, in step 10 the x values are calculated at the bottom of the image with the help of the gradients and intersections of the lines. The lines are drawn on a black image and the ROI is taken.
	In the last step, the original image and the line image get overlaid.
    
### 2. Identify potential shortcomings with your current pipeline

One potential shortcoming is the missing error handling. If the Hough transform cannot find line segments, the calculation of the lines will fail and there is no fallback solution.

The calculated lines do not exactly fit the lane lines in all test images.

In the video, the lines appear to stable. It seems as if the line is calculated only once and is standing still. I couldn't find the cause (potential error) in my code.

### 3. Suggest possible improvements to your pipeline

A possible improvement would be to add error handling. 

For video processing a potential improvement could be to remember the parameters of the last lines and to use them as fallback if no lines could be detected in the current frame. 
