## **Advanced Lane Line Detection***

## Rohit Kukreja

**Youtube video**
[![Youtube Video]("output_images/hqdefault.jpg")](https://www.youtube.com/watch?v=E9UsSixMfNk)


 Goal of the project is  to write a software pipeline to identify the lane boundaries in a video.
 Check out the [Github](https://github.com/rohit5945/CarND-Advanced-Lane-Lines) for this project   


The Project
---

The goals / steps of this project are the following:

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Use color transforms, gradients, etc., to create a thresholded binary image.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Detect lane pixels and fit to find the lane boundary.
* Determine the curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.

The images for camera calibration are stored in the folder called `camera_cal`.  The images in `test_images` are for testing your pipeline on single frames.  If you want to extract more test images from the videos, you can simply use an image writing method like `cv2.imwrite()`, i.e., you can read the video in frame by frame as usual, and for frames you want to save for later you can write to an image file.  


## Camera Calibration##

The first step we will take is to find the calibration matrix, along with distortion coefficient for the camera that was used to take pictures of the road. This is necessary because the convex shape of camera lenses curves light rays as the enter the pinhole, therefore causing distortions to the real image. Therefore lines that are straight in the real world may not be anymore on our photos.

To compute the camera the transformation matrix and distortion coefficients, we use a multiple pictures of a chessboard on a flat surface taken by the same camera. OpenCV has a convenient method called findChessboardCorners that will identify the points where black and white squares intersect and reverse engineer the distorsion matrix this way. The image below shows the identified chessboard corners traced on a sample image

![Camera Calibration]("output_images/found_chessboard_corners.png")

We can see that corners are very well identified. Next we run our chessboard finding algorithm over multiple chessboard images taken from different angles to identify image and object points to calibrate the camera. The former refers to coordinates in our 2D mapping while the latter represents the real-world coordinates of those image points in 3D space (with z axis, or depth = 0 for our chessboard images). Those mappings enable us to find out how to properly undistort an image taken from the same camera. You can witness it's effectiveness on the image below.

![Undistorted]("output_images/distorted_vs_undistorted_chessboard_images.png")


## Gradient and Color thresholding ##

After calibrating the input images we do a thresholding on the image using the gradient on different color channels.

Steps:
1. Convert from RGB to HLS 
2. take the S-channel and L-channel
3. Perform gradient on L-channel and color thresholding on L- channel
4. create a binary image using OR(|) for both the thresholds.

![color gradient]("output_images/color_gradient_image.jpg")

## Perspective Transformation##

Perspective transformation is done for better detecting the curved lanes.
We do a transformation to birds eye view .

![perspective transform]("output_images/perspective_image.jpg")

## Polynomial fitting ##

Fit a second degree polynomial to the detected lanes using the sliding window transformations.

![polynomial]("output_images/polynomial_image.jpg")

## Warp image##

Convert the image form birds eye view to the image world using inverse perspective tranformation and warp on the bas image.

![warp]("output_images/final.jpg")

## Radius of curvature ##

Calculate the radius of curvature of left and right lane and map onto image.

![radius]("output_images/final.jpg")




