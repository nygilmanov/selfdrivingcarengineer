# **Finding Lane Lines on the Road** 

---


The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


### 1. Pipeline Description . 

My pipeline consisted of 5 steps. 


Original image 

![image1](https://github.com/nygilmanov/selfdrivingcarengineer/blob/main/CarND-LaneLines-P1/flow%20/0original.png)


1. Converted the images to grayscale (cv2.cvtColor)


![image1](https://github.com/nygilmanov/selfdrivingcarengineer/blob/main/CarND-LaneLines-P1/flow%20/1gray.png)


2. Removed the noise from the image (cv2.GaussianBlur)
3. Calculated image gradients to highlight the edges on the image (cv2.Canny)

![image2](https://github.com/nygilmanov/selfdrivingcarengineer/blob/main/CarND-LaneLines-P1/flow%20/3edges.png)


4. Defined the area of interest which covers lane lines and excludes everything outside of it.


![image4](https://github.com/nygilmanov/selfdrivingcarengineer/blob/main/CarND-LaneLines-P1/flow%20/4region.png)


![image3](https://github.com/nygilmanov/selfdrivingcarengineer/blob/main/CarND-LaneLines-P1/flow%20/2blur.png)



5. Defined hough lines and finally drawn all the lines on the image


![image5](https://github.com/nygilmanov/selfdrivingcarengineer/blob/main/CarND-LaneLines-P1/flow%20/5final.png)




### Modification of the draw_lines() function.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function 

1. Calculated the slope for each line which we get from hough space
2. Separated left and right lines depending on the sign of the slope
3. For each set of lines (right,left) have calcualted average center and average slope
4. Knowing the slope and center coordinates of right and left lines have calculated the values of x1,x2 by putting known y1,y2 
    (y1-y')=M(x1-x') where M - is the known slope


### 2. Potential shortcomings with the pipeline
 
1. Initially the pipiline was working on the test images and first 2 videos only 
   and was drawing number of lines on the top of each other.
2. The video on the turn (challenge) did not reflect the lines in a correct way
3. Right lines on the challenge video were not reflecting at all.

Have tried to use linear regression as extrapolation technique. It was working worse then simple averaging described above.
Finally has stopped on simple averaging.


In general
1. This approah may not be able to define lane lines in the traffic jam. Currently there are no any other cars in front of the car.


 
### 3. Improvements of the pipeline

1. Applied lines averaging technique by taking mean points and slopes as an extrapolation technique.
2. Applied color filter. Finally yellow and white lines were taken whereas other lines were filtered. 
   This approach allowed not to take lines  which are not lane lines but actually look like lines on the image
   
3. Have changed the size of the trapezoid as right line on the challenge video was not included
   1.1 Have changed the scaling of trapezoid depending on the image size (previously images points were specific to concrete image size and after moving to another image lines were drawn incorrectly)
   
In general
1. For the cases where lines are not seen we may use gaps between cars as lines and bias towards real lane lines.
   This means we can inderectly define lane lines by positions of the cars and dark zones between them 




### FINAL VIDEOS

*Part1 Click On The Image


[![IMAGE ALT TEXT](https://github.com/nygilmanov/selfdrivingcarengineer/blob/main/CarND-LaneLines-P1/flow%20/Part1.png)](https://www.youtube.com/watch?v=qUHU9EWCf5Q "Step1")


*Part2 Click On The Image


[![IMAGE ALT TEXT](https://github.com/nygilmanov/selfdrivingcarengineer/blob/main/CarND-LaneLines-P1/flow%20/Part2.png)](https://www.youtube.com/watch?v=pdssKjVWwds "Step2")


*Part3 Click On The Image

[![IMAGE ALT TEXT](https://github.com/nygilmanov/selfdrivingcarengineer/blob/main/CarND-LaneLines-P1/flow%20/Part3.png)](https://www.youtube.com/watch?v=A_3RtlQtea0 "Step3")


