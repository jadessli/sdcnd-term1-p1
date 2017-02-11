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

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by dividing the region of interest into two smaller regions, one for left-laneline area, other for right-laneline area, then selected a reference point between them, which almost in the middle of picture. The main task is to find the point nearest to the reference point, which means in left-laneline side the point is in the northest of its region, and in the northwest in right-laneline side. I applied this menthod because there are fewer noise lines in the area from the middle to the bottom than the one from the middle to the up, and less in the middle than the sides. 


###2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the change of light in the picture could have an enormous impact on the result.  

Another shortcoming could be apt to be influenced by the close noise-lines with similar shape.

###3. Suggest possible improvements to your pipeline

A possible improvement would be to generalize the slope and intercept in the draw_lines function by averaging them or selecting 75% nearest points.

Another potential improvement could be to adjust the parameters in **Canny** and **Hough**.
