#**Finding Lane Lines on the Road** 

##Writeup


---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report



---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I applied a 9 * 9 Gaussian smoothing before running **Canny**. I masked the region of interest  with a four sided polygon (_(130, imshape[0]), (450, 320), (550, 320), (imshape[1]-120, imshape[0])_), finally ran **Hough** on this masked area with the input parameters(_rho = 1, theta = np.pi/180, threshold = 15, min_line_length = 100, max_line_gap = 160_).

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by dividing the region of interest into two smaller regions, other for right lane line area, then I selected a reference point between them( almost in the middle of picture). The main task was to find one point nearest to the reference point as one selected point (on left lane line side, the selected point is in the northeast of its region, and in the northwest on right lane line side) and selected other point nearest to the bottom. I used these two points for calculating the slope and the intercept, finally got a final line on both sides. I applied this method because there are fewer noise lines in the area from the middle to the bottom than the one from the middle to the top, and less in the middle than the sides. 


###2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be that the change of light in the picture could have an enormous impact on the result.  
Another shortcoming could be poor error correcting capability when the noise lines with similar shape appear in the region of interest.

###3. Suggest possible improvements to your pipeline

A possible improvement would be to generalize the slope and intercept in the draw_lines function by averaging them or selecting 75% nearest points.

Another potential improvement could be to adjust the parameters in **Canny** and **Hough**.
