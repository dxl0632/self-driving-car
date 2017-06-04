# **Finding Lane Lines on the Road** 


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

My pipeline consisted of 6 steps:

1. Convert original image to gray image
2. Do Gaussian smoothing
3. Run Canny edge detection
4. Generate masked edges images
5. Use Hough transformation to find lines
6. Map lines back to the original image 

For drawing smooth lines, here is how I modified the `draw_lines()`:

1. Caculate slopes for each line
2. Seperate lines into `left_lines` and `right_lines` based on the value of slope
3. Fit a line use the points from either `left_lines` or `right_lines` to get slope `m` and intercept `b`. Here I leveraged the function `np.linalg.lstsq`.
4. Find the min and max `y` from `left_lines` or `right_lines`, and use `m` and `b` to calculate its corresponding `x`. So I get fou
5. Use `cv2.line` to draw a single line using two points obtained above, i.e., `(min_left_x, min_left_y), (max_left_x, max_left_y)`.
6. Use `(min_right_x, min_right_y), (max_right_x, max_right_y)` to draw another line.


This is how the images look like after the pipeline:

![alt text](https://github.com/dxl0632/self-driving-car/blob/master/CarND-LaneLines-P1/test_images_output/solidWhiteCurve.jpg)

![alt text](https://github.com/dxl0632/self-driving-car/blob/master/CarND-LaneLines-P1/test_images_output/solidWhiteRight.jpg)

![alt text](https://github.com/dxl0632/self-driving-car/blob/master/CarND-LaneLines-P1/test_images_output/solidYellowCurve.jpg)



### 2. Identify potential shortcomings with your current pipeline


One shortcoming is now the parameters (thresholds, vertices, etc.) for the pipeline is configured manually. I wonder if this can be detected automatically.

Another shortcoming is the `draw_lines` function is sensitive to outliers, and it only works well for relatively straight lines. So if I apply this to the last challenge, the detection is miserable, possibly due to the curves.

### 3. Suggest possible improvements to your pipeline

A possible improvement would be improving the `draw_lines` to be able to handle curves.

Another possible improvement would be automatically tune the parameters for the pipeline.

 