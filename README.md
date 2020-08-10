# Advanced Lane Finding
The goal of this project is to build a pipeline that will take in an image and highlight the driving lane in the image.



 ## Project Steps
 
The steps of this project are as follows:

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Use color transforms, gradients, etc., to create a thresholded binary image.
* Detect lane pixels and fit to find the lane boundary.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.

The images for camera calibration are stored in the folder called `camera_cal`.  The images in `test_images` are for testing your pipeline on single frames. All output images will write to `output_images`.

[//]: # (Image References)

[image1]: ./output_images/camera_cal/1.jpg "Camera Calibration Image Example"
[image2]: ./output_images/undistorted_images/1.jpg "Undistorted Road Example"
[image3]: ./output_images/perspective_transformed_images/1.jpg "Perspective Transformed Example"
[image4]: ./output_images/binary_threshold_images/all_binary_1.png "Binary Threshold Example"
[image5]: ./output_images/color_threshold_images/all_color_1.png "Color Threshold Example"
[image6]: ./output_images/sliding_box_images/1.jpg "Sliding Box Example"
[image7]: ./output_images/lane_margin_images/1.jpg "Lane Margin Example"
[image8]: ./output_images/shaded_images/1.jpg "Shaded Lane Example"
[image9]: ./output_images/histograms/1.png "Histogram Example"
[image10]: ./output_images/final_output/1.jpg "Final Output Example"

[gif1]: ./project_video_output.gif "GIF output"

## Image Processing Pipeline

#### Camera Calibration
Camera is calibrated by using a series of checkerboard images to determine the calibration matrix and distortion coefficients of the camera.

![alt text][image1]

#### Undistort Image
Using the calibration matrix and distortion coefficients of the camera, undistort the source image.

![alt text][image2]

#### Perspective Transform Image
Transform the perspective of the undistorted image to get a "Bird's Eye View" of the lane.

![alt text][image3]
#### Apply Binary Thresholds
Applies various binary thresholds to the transformed image. The goal here is to isolate the lane markers as much as possible.

![alt text][image4]
#### Apply Color Thresholds
Applies color thresholds to the transformed image. Uses HSV values and yellow/white color values to attempt to isolate the lane markers.

![alt text][image5]
#### Define Histogram of White Pixels
Create a histogram of white pixels

![alt text][image9]
#### Fit Polynomial to White Pixels
Using the peaks of the histogram, we identify a region (green box) and highlight (red and blue) the pixels that fall within this region. This will help reduce noise outside the lane marker areas. The region also shifts in X and Y as the lane changes direction. Finally a second order polynomial is fit to these points (representing the lane lines).


![alt text][image6] ![alt text][image7]
#### Highlight Lane Region between Polynomials
The area between left and right polynomials is highlighted here in green.

![alt text][image8]
#### Reverse Perspective Transform
The final output reverses the perspective transform on this region and overlays it with the original undistorted image.

![alt text][image10]
## Video Test
Using the same pipeline as before, process the test video

![alt text][gif1]
