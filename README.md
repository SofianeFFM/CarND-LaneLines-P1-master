# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/solidWhiteCurve.jpg "Solid white curve"
[image2]: ./test_images_output/solidWhiteRight.jpg "Solid white right"
[image3]: ./test_images_output/solidYellowCurve.jpg "Solid yellow curve"
[image4]: ./test_images_output/solidYellowCurve2.jpg "Solid yellow curve 2"
[image5]: ./test_images_output/solidYellowLeft.jpg "Solid yellow left"
[image6]: ./test_images_output/whiteCarLaneSwitch.jpg "Shite car lane switch"


---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. 

Step 1: I converted the images to grayscale.
Step 2: I applied gaussian smoothing to reduce noise as Canny filter is very sensitive to noise. 
Step 3: I apllied Canny filter. As I struggled with the values, I looked if there's a way to auto calculate it. 
		One of the methos was AutoCanny from this link: https://www.pyimagesearch.com/2015/04/06/zero-parameter-automatic-canny-edge-detection-with-python-and-opencv/
		As the sample images and videos are token in good conditions with "clear" edges, this function can help. In other circumstances 
		a more powerful method should be adopted.
Step 4: Define a region of interest. This should "reproduce" the angle view of the driver and set the focus on the Lane.
Step 5: Run Hough and draw the lines.


In order to draw a single line on the left and right lanes, I modified the draw_lines() function by splitting the coords in two groups: left line (negative slope) and right line (positive slope). Then I allowed only slopes between ±0,35 and ±0,95 in order to eliminate the almost horizontal lines. 
Before hitting the extrapolation part, y_min had to be defined. A minimum value of 3/5 was set to minimize the risk of having the two lines intersected. 
After calulating all the paameters, the lines were drawn and the image is returned.

Below is he output of the processed images:

![alt text][image1]
![alt text][image2]
![alt text][image3]
![alt text][image4]
![alt text][image5]
![alt text][image6]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when we have bad weather or not enough sharpness or brightness of the images.
Curves, haveing two lines close to each other on one side (for example by repair/construction) could "confuse" the pipeline.

### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use automated functions to calculate the parameters of canny and hough.
It's also mandatory to split the image in two halfs and ignore the lines that have the same slope from the other half. Otherwise the calculation of the averga e can be heavily affected.
It's also better to use 2nd grade polynomial functions instead of 1st grad ones to obtain better results on curves. 

Another potential improvement could be another approach!