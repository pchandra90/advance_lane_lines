**Advanced Lane Finding Project**

The goals / steps of this project are the following:

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Use color transforms, gradients, etc., to create a thresholded binary image.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Detect lane pixels and fit to find the lane boundary.
* Determine the curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.

[//]: # (Image References)

[calibration]: ./camera_cal/calibration1.jpg
[undistort_calibration]: ./output_images/undistort_calibration1.jpg
[test1_original_image]: ./output_images/test1_original_image.jpg
[test1_undistort_image]: ./output_images/test1_undistort_image.jpg
[test1_binary_image]: ./output_images/test1_binary_image.jpg
[test1_bird_eys_image]: ./output_images/test1_bird_eys_image.jpg
[test1_final_output_image]: ./output_images/test1_final_output_image.jpg
[poly_fit_test1]: ./output_images/poly_fit_test1.png
[prespective_straight_lines1_before_tranform]: ./output_images/prespective_straight_lines1_before_tranform.jpg
[prespective_straight_lines1_after_transform]: ./output_images/prespective_straight_lines1_after_transform.jpg
[prespective_straight_lines1_after_revert_transform]: ./output_images/prespective_straight_lines1_after_revert_transform.jpg


## [Rubric](https://review.udacity.com/#!/rubrics/571/view) Points

### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

---

### Camera Calibration

The code for this step is contained in the fourth code cell of the IPython notebook located in "P2.ipynb".  

I start by preparing "object points", which will be the (x, y, z) coordinates of the chessboard corners in the world. Here I am assuming the chessboard is fixed on the (x, y) plane at z=0, such that the object points are the same for each calibration image.  Thus, `objp` is just a replicated array of coordinates, and `objpoints` will be appended with a copy of it every time I successfully detect all chessboard corners in a test image.  `imgpoints` will be appended with the (x, y) pixel position of each of the corners in the image plane with each successful chessboard detection.  

I then used the output `objpoints` and `imgpoints` to compute the camera calibration and distortion coefficients using the `cv2.calibrateCamera()` function.  I applied this distortion correction to the test image using the `cv2.undistort()` function and obtained this result: 

#### Original Image

![alt text][calibration]

#### Undistorted Image

![alt text][undistort_calibration]

### Pipeline (for single image)

#### With an example of a image, I will explain all concepts briefly.

#### 0. Input image

![alt text][test1_original_image]

#### 1. Undistort Image

By using camera calibration and distortion coefficients I undistort the image. Undistorted output:

![alt text][test1_undistort_image]

#### 2. Color transforms and gradients methods are used to get thresholded binary image

I have used HLS color transform. Sobel gradient in x and y direction conbined to get thresholded binary image. 
The code for this step is contained in the eighth code cell of the IPython notebook located in "P2.ipynb".
Following is binary image:

![alt text][test1_binary_image]

#### 3. Perspective Transform

The code for this step is contained in the tenth code cell of the IPython notebook located in "P2.ipynb".
Its takes source and destination point, which uses `cv2.getPerspectiveTransform(src, dst)` and return transformation matrix. 
When source and destination got interchanged we get inverse transformation matrix, which will be used in 
reverting the transformed image. I have use straight line image to do so. This matrix is used to transformation of 
other images.

##### Original image

![alt text][prespective_straight_lines1_before_tranform]

##### After Prespective Transformation

![alt text][prespective_straight_lines1_after_transform]

##### After Reverting Prespective Transformation

![alt text][prespective_straight_lines1_after_revert_transform]

##### Prespective Transformation on Thresholded Binary Image

![alt text][test1_bird_eys_image]


#### 4. Fit Second degree polynomial on Prespective Transformed Image

The code for this step is contained in the fifteenth code cell of the IPython notebook located in "P2.ipynb".

##### Intuitional image, this will make easy to understand code

![alt text][poly_fit_test1]

#### 5. Radious of Curvature and Distance from Center

The code for this step is contained in the seventeenth code cell of the IPython notebook located in "P2.ipynb".


#### 6. Above Steps are Combined in Pipline

The code for this step is contained in the eighteenth code cell of the IPython notebook located in "P2.ipynb".

##### Final Image Output

![alt text][test1_final_output_image]

---

### Pipeline (video)

The code for this step is contained in the twenty-eighth code cell of the IPython notebook located in "P2.ipynb".

Here's a [link to my output video result](./project_video_output.mp4)

---

### Discussion

- Other gradients can be use to detection eg. Laplacian.
- Code can be optimize to be faster by avoiding calaulation repetation.
- Accuracy can be improved by using information in sequence of images instead dealing with single image.
