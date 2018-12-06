## Advanced Lane Finding
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

![](giphy5.gif)

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

The first step in the pipeline is to undistort the camera. Some images of a 9x6 chessboard are given and are distorted. Our task is to find the Chessboard corners an plot them. For this, after loading the images we calibrate the camera. Open CV functions like findChessboardCorners(), drawChessboardCorners() and calibrateCamera() help us do this.

##### Distortion Corrected Calibrated Image:

![input](https://user-images.githubusercontent.com/34116562/49130314-4d274d80-f2f9-11e8-8ef8-c6697e9ff4c5.png)

##### Some Calibrated Images with points drawn: 

![output](https://user-images.githubusercontent.com/34116562/49130381-a4c5b900-f2f9-11e8-954f-d7f68e7e4768.png)



## Pipeline (test images)

#### 1. Provide an example of a distortion-corrected image.

#### Some examples of Distortion Corrected Images are given below.

The images in the test_images folder serve as our original image. Our task is to Undistort them. For this, I defined a function cal_undistort() which takes in a image and returns the undistorted one using cv2.undistort().

#### These images are Distortion Corrected :


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

Perspective Transform is the Bird's eye view for Lane images. We want to look at the lanes from the top and have a clear picture about their curves. Implementing Perspective Transform was the most interesting one for me. I used values of src and dst as shown below: 

src = np.float32([[590,450],[687,450],[1100,720],[200,720]])

dst = np.float32([[300,0],[900,0],[900,720],[300,720]])

Also, made a function warper(img, src, dst) which takes in the BInary Warped Image and return the perspective transform using cv2.getPerspectiveTransform(src, dst) and cv2.warpPerspective(img, M, img_size, flags=cv2.INTER_NEAREST). The results are shown below:


![output_1](https://user-images.githubusercontent.com/34116562/49129781-1d774600-f2f7-11e8-80df-2d0d6b0a3950.png)
![output_2](https://user-images.githubusercontent.com/34116562/49129782-1f410980-f2f7-11e8-894a-94fdf6f519d8.png)
![output_3](https://user-images.githubusercontent.com/34116562/49129786-20723680-f2f7-11e8-9268-273b2526af11.png)
![output_4](https://user-images.githubusercontent.com/34116562/49129788-223bfa00-f2f7-11e8-9aed-0555271d53ed.png)
![output_5](https://user-images.githubusercontent.com/34116562/49129790-2405bd80-f2f7-11e8-90c8-61f1f9490cab.png)
![output_6](https://user-images.githubusercontent.com/34116562/49129795-2700ae00-f2f7-11e8-8987-eda7e5cc51a2.png)


#### 4. Describe how (and identify where in your code) you identified lane-line pixels and fit their positions with a polynomial?

Once I got the Perspective Transform of the binary warped images, I first used the sliding window method to plot the lane lines and fitted a polynomial using fit_polynomial(img) function. Later on, I used the Search from prior technique and fitted a more accurate polynomial through my perspective transformed images using search_around_poly(image) funtion. Proper markings are there in the code to indicate each and every step.

### Finding the lines - Sliding Window and fitting a polynomial

![output_1](https://user-images.githubusercontent.com/34116562/49129915-9bd3e800-f2f7-11e8-9d7b-7ee1480b480c.png)
![output_2](https://user-images.githubusercontent.com/34116562/49129917-9c6c7e80-f2f7-11e8-8b37-4791cb2e60e3.png)
![output_3](https://user-images.githubusercontent.com/34116562/49129920-9e364200-f2f7-11e8-9852-5e35607d7c07.png)
![output_4](https://user-images.githubusercontent.com/34116562/49129924-9f676f00-f2f7-11e8-81fb-aa529361acfc.png)


### Finding the lines - Search From Prior and fitting a polynomial

![output_1](https://user-images.githubusercontent.com/34116562/49129956-b60dc600-f2f7-11e8-82e2-c8e48d9e3d3f.png)
![output_2](https://user-images.githubusercontent.com/34116562/49129958-b73ef300-f2f7-11e8-9898-bada3f974564.png)
![output_3](https://user-images.githubusercontent.com/34116562/49129959-b8702000-f2f7-11e8-9477-95f0ef30d523.png)
![output_4](https://user-images.githubusercontent.com/34116562/49129961-b9a14d00-f2f7-11e8-8d33-315251f554fb.png)
![output_5](https://user-images.githubusercontent.com/34116562/49129965-bb6b1080-f2f7-11e8-9d74-91581421f7f2.png)
![output_6](https://user-images.githubusercontent.com/34116562/49129969-bdcd6a80-f2f7-11e8-8428-96e62595f872.png)


#### 5. Describe how (and identify where in your code) you calculated the radius of curvature of the lane and the position of the vehicle with respect to center.

For calculating the radius of curvature and the position of the vehicle with respect to center, I made a function called radius_and_offset(warped_image) which returns curvature_string and offset. Used left_lane_inds and right_lane_inds for performing the task. Used function fit_poly(image.shape, leftx, lefty, rightx, righty) which returns left_fitx, right_fitx, ploty to calcuate the real radius of curvature and offset.

#### 6. Provide an example image of your result plotted back down onto the road such that the lane area is identified clearly.

After implementing all the steps, it's time to create the pipeline for one image. Created a function process_image() as the main pipeline function. Also, I put the Radius of Curvature and Center Offset on the final image using cv2.putText() function. The result is shown below: 

##### Lane Area Drawn without Information:

![output-without-info](https://user-images.githubusercontent.com/34116562/49130028-fec57f00-f2f7-11e8-8293-34e09bc07880.png)

##### Lane Area Drawn with Radius of Curvature and Central Offset:

![output-with-radius-and-offset](https://user-images.githubusercontent.com/34116562/49130030-008f4280-f2f8-11e8-8ed1-8a1aad84de5a.png)


# Pipeline (video)

#### 1. Provide a link to your final video output. Your pipeline should perform reasonably well on the entire project video (wobbly lines are ok but no catastrophic failures that would cause the car to drive off the road!)

##### Here is the Link to the Project Video 

https://www.youtube.com/watch?v=5q50SOwfwAg

# Discussion

#### 1. Briefly discuss any problems / issues you faced in your implementation of this project. Where will your pipeline likely fail? What could you do to make it more robust?

The project video ran smoothly.  It was successfully drawing the lane area over the road with the radius of curvature and center offset clearly plotted and changing their values. I also ran the Pipeline over the challenge video and the hard-challenge video. 

For a standout submission, I followed the suggestion in the lesson to not just search blindly for the lane lines in each frame of video, but rather, once I have a high-confidence detection, using that to inform the search for the position of the lines in subsequent frames of video. For example, if a polynomial fit was found to be robust in the previous frame, then rather than search the entire next frame for the lines, just a window around the previous detection could be searched. This will improve speed and provide a more robust method for rejecting outliers. I performed this step with the help of search_around_poly(image) function.

I think the pipeline will fail when the road curves a lot and there is a sudden change in the direction like the roads in hilly areas as the case in hard-challenge-video. Some measures could be taken so as to adjust the pipeline so that it also draws lane areas over the roads of hilly areas as well i.e. where there are a lot of curves.
