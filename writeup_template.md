# **Finding Lane Lines on the Road** 


---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

The pipeline consists of several steps:

1. The input image is converted to grayscale
2. Gaussian Blur with a kernel size of 3 is applied. This helps reduce any noise that is present in the image to aid edge detection
3. A Canny transform is used to detect all the edges in the image. The output is an image containing the detected edges.
4. The unwanted portion of the image (anything that is not in front of the vehicle, to just before the vanashing point) is masked out.
5. A Hough Transform is used on the remaining portion of the image. This gives an array of detected lines (in vector format)
6. The draw_lines() function was modified to convert the array of lines into slope/intercept form, split into left and right, and averaged together. The left slope is assumed to be -0.7 +- 0.1 and the right slope 0.6 +- 0.1. To redraw the lines onto the image, y values of y=height * 0.6 and y=height were chosen, and the x values calculated by x = (y - b) / m. A line was drawn between these two points.


### 2. Identify potential shortcomings with your current pipeline

* The current pipeline can only work on straight lines so if there is curvature in the road, lens distortion, or lane markings without straight lines, the line fitting procedure will not work very accurately or at all.
* There is no filtering or noise reduction, so the reconstructed lane lines will jump around significantly in areas with vauge inputs.


### 3. Suggest possible improvements to your pipeline

* Filtering the output to reduce noise
* Add the ability to better deal with changes in light and contrast
* Use parabolic curves rather than straight lines
* Add some sort of weighting to the edge analysis so that good/clear information is given a higher weighting than potential noise.