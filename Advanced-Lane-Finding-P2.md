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

#### 2. Describe how (and identify where in your code) you used color transforms, gradients or other methods to create a thresholded binary image. Provide an example of a binary image result.

#### 3. Describe how (and identify where in your code) you performed a perspective transform and provide an example of a transformed image.

#### 4. Describe how (and identify where in your code) you identified lane-line pixels and fit their positions with a polynomial?

#### 5. Describe how (and identify where in your code) you calculated the radius of curvature of the lane and the position of the vehicle with respect to center.

#### 6. Provide an example image of your result plotted back down onto the road such that the lane area is identified clearly.

# Pipeline (video)

#### 1. Provide a link to your final video output. Your pipeline should perform reasonably well on the entire project video (wobbly lines are ok but no catastrophic failures that would cause the car to drive off the road!)

# Discussion

#### 1. Briefly discuss any problems / issues you faced in your implementation of this project. Where will your pipeline likely fail? What could you do to make it more robust?
