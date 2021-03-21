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

TEST!!!!!

### 1. Pipeline Description . 

My pipeline consisted of 5 steps. 

1. Converted the images to grayscale (cv2.cvtColor)
2. Removed the noise from the image (cv2.GaussianBlur)
3. Calculated image gradients to highlight the edges on the image (cv2.Canny)
4. Defined the area of interest which covers lane lines and excludes everything outside of it.
5. Defined hough lines and finally drawn all the lines on the image


### Modification of the draw_lines() function.
In order to draw a single line on the left and right lanes, I modified the draw_lines() function 

1. Calculated the slope for each line
2. Separated left and right lines depending on the sign of the slope
3. For each set of lines (right,left) have calcualted average center and average slope
4. Knowing the slope and center coordinates of right and left line have calculated the values of x1,x2 by putting known y1,y2 
    (y1-y')=M(x1-x') where M - is the known slope


If you'd like to include images to show how the pipeline works, here is how to include an image: 


### 2. Identify potential shortcomings with your current pipeline

Reflecting shortcomings which i had with the solution
 
1. Initially the pipiline was working on the test images and first 2 videos only 
   and was drawing number of lines on the top of each other.
2. The video on the turn (challenge) did not reflect the lines correct way
3. Right line on the challenge video was not reflecting at all.

Have tried to use linear regression as extrapolation technique. It was working worse then simple averaging described above.
Finally has stopped on simple averaging.


In general
1. This approah may not be able to define lane lines in the traffic jam. Currently there are no any other cars in front of the car.


 
### 3. Suggest possible improvements to your pipeline

1. Applied lines averaging technique by taking mean points and slopes averaging  as an extrapolation technique.
2. Applied color filter. Finally yellow and white lines were taken whereas other lines were filtered. 
   This approach allowed not to take lines  which are not lane lines but actually look like lines on the image
   
3. Have changed the size of the trapezoid as right line on the challenge video was not included
   1.1 Have changed the scaling of trapezoid depending on the image size (previously images points were specific to concrete image size and after moving to another image lines were drawn incorrectly)
   
In general
1. For the cases where lines are not seen we may use gaps between cars as lines and bias towards real lane lines.
   This means we can inderectly define lane lines by positions of the cars and dark zones between them 



   
    


