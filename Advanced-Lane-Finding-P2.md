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
