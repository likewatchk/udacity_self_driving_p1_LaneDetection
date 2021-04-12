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

My pipeline consisted of 5 steps.
First, I converted the images to grayscale.
Second, I applied 'Gaussian Blurring' to the image for bringing edges to light.
Third, I extracted the edges of image with 'Canny'. 
Fourth, to extract only the edges of lanes on the image, I masked the image with polygon.
Fifth, to acheive lines on lanes on the image, I used 'Hough Transform' with 'cv2.HoughLinesP'. It makes lines with edge points.

In order to draw a single line on the left and right lanes,

I split the hough lines to right and left devided by half of the width of the image.
And to make one line in each part, I used 'np.polyfit' for regression with the end-poionts of hough lines by part. and I made 'polygonial class' using 'np.poly1d' so that I could find the intersection point of masking boundary(the below outline of image and y=319) and right/left line.

After that, I could have two points of right side of image, and two points of left side of image. I draw two lines(right and left) with 'cv2.line'.

