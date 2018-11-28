# Advanced Lane Finding P2

## Advanced Lane Detection Project which includes advanced image processing to detect lanes irrespective of the road texture, brightness, contrast, curves etc. Used Image warping and sliding window approach to find and plot the lane lines. Also determined the real curvature of the lane and vehicle position with respect to center.

# The Steps involved are:

##### Computing the camera calibration matrix and distortion coefficients given a set of chessboard images. (9x6)
##### Apply a distortion correction to raw images.
##### Use color transforms, gradients, etc., to create a thresholded binary image.
##### Apply a perspective transform to rectify binary image ("birds-eye view") to get a warped image.
##### Detect lane pixels and fit to find the lane boundary.
##### Determine the real curvature of the lane and vehicle position with respect to center.
##### Warp the detected lane boundaries back onto the original image.
##### Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.

# Rubric Points

## Camera Calibration

#### 1. Briefly state how you computed the camera matrix and distortion coefficients. Provide an example of a distortion corrected calibration image.

## Pipeline (test images)

#### 1. Provide an example of a distortion-corrected image.

Some examples of distortion corrected images are :

![output_1](https://user-images.githubusercontent.com/34116562/49129716-d0936f80-f2f6-11e8-9165-fbbdbc7e96ec.png)
![output_2](https://user-images.githubusercontent.com/34116562/49129717-d1c49c80-f2f6-11e8-993a-03642ccce32a.png)
![output_3](https://user-images.githubusercontent.com/34116562/49129719-d2f5c980-f2f6-11e8-8875-a3a3445d4d00.png)
![output_4](https://user-images.githubusercontent.com/34116562/49129720-d4bf8d00-f2f6-11e8-9ed2-e2eb9256bbdf.png)
![output_5](https://user-images.githubusercontent.com/34116562/49129735-e4d76c80-f2f6-11e8-9a3e-af0ace294a08.png)
![output_6](https://user-images.githubusercontent.com/34116562/49129738-e6089980-f2f6-11e8-98a4-804e9e632a4a.png)


#### 2. Describe how (and identify where in your code) you used color transforms, gradients or other methods to create a thresholded binary image. Provide an example of a binary image result.

Detecting edges around trees or cars is okay because these lines can be mostly filtered out by applying a mask to the image and essentially cropping out the area outside of the lane lines. It's most important that we reliably detect different colors of lane lines under varying degrees of daylight and shadow. So, that our self driving car does not become blind in extreme daylight hours or under the shadow of a tree.
 
I performed gradient threshold and color threshold individually and then created a binary combination of these two images to map out where either the color or gradient thresholds were met called the combined_binary in the code.

![output_1](https://user-images.githubusercontent.com/34116562/49129596-68448e00-f2f6-11e8-8d0d-bfa31bbc1dbe.png)
![output_1](https://user-images.githubusercontent.com/34116562/49129605-6c70ab80-f2f6-11e8-9678-c058d70bd1a3.png)
![output_2](https://user-images.githubusercontent.com/34116562/49129599-6a0e5180-f2f6-11e8-9539-b4d630e90a84.png)
![output_2](https://user-images.githubusercontent.com/34116562/49129607-6e3a6f00-f2f6-11e8-926a-bc7c87323ce2.png)


#### 3. Describe how (and identify where in your code) you performed a perspective transform and provide an example of a transformed image.

![output_1](https://user-images.githubusercontent.com/34116562/49129781-1d774600-f2f7-11e8-80df-2d0d6b0a3950.png)
![output_2](https://user-images.githubusercontent.com/34116562/49129782-1f410980-f2f7-11e8-894a-94fdf6f519d8.png)
![output_3](https://user-images.githubusercontent.com/34116562/49129786-20723680-f2f7-11e8-9268-273b2526af11.png)
![output_4](https://user-images.githubusercontent.com/34116562/49129788-223bfa00-f2f7-11e8-9aed-0555271d53ed.png)
![output_5](https://user-images.githubusercontent.com/34116562/49129790-2405bd80-f2f7-11e8-90c8-61f1f9490cab.png)
![output_6](https://user-images.githubusercontent.com/34116562/49129795-2700ae00-f2f7-11e8-8987-eda7e5cc51a2.png)


#### 4. Describe how (and identify where in your code) you identified lane-line pixels and fit their positions with a polynomial?

### Finding the lines - Sliding Window and fitting a polynomial

![output_1](https://user-images.githubusercontent.com/34116562/49129915-9bd3e800-f2f7-11e8-9d7b-7ee1480b480c.png)
![output_2](https://user-images.githubusercontent.com/34116562/49129917-9c6c7e80-f2f7-11e8-8b37-4791cb2e60e3.png)
![output_3](https://user-images.githubusercontent.com/34116562/49129920-9e364200-f2f7-11e8-9852-5e35607d7c07.png)
![output_4](https://user-images.githubusercontent.com/34116562/49129924-9f676f00-f2f7-11e8-81fb-aa529361acfc.png)


### Finding the lines - Search From Prior and fitting a polynomial



#### 5. Describe how (and identify where in your code) you calculated the radius of curvature of the lane and the position of the vehicle with respect to center.

#### 6. Provide an example image of your result plotted back down onto the road such that the lane area is identified clearly.

# Pipeline (video)

#### 1. Provide a link to your final video output. Your pipeline should perform reasonably well on the entire project video (wobbly lines are ok but no catastrophic failures that would cause the car to drive off the road!)

# Discussion

#### 1. Briefly discuss any problems / issues you faced in your implementation of this project. Where will your pipeline likely fail? What could you do to make it more robust?
