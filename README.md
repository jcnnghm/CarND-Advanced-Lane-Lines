## Advanced Lane Finding

### Submission Notes

To identify the lane lines, I:

* Calibrated the camera and undistorted input images.
* Calculated a perspective transform and un-transform.
* Graphed RGB and HLS images, and created an algorithm to merge color channels (S and R) to better identify lane lines.
* Combined the color filter, with sobel and magnitude filters to identify lane lines.
* Applied the thresholding filters with the top-down filters, to create a top-down view of just the lane lines.
* Created an algorithm to mask lane lines in the input image, then fit polynomials to the masked line pixels.
* Create a lane mask using the fitted lines, transformed it to the original perspective, and applied it.
* Created a video-processing pipeline that starts using the histogram matching method, and then uses the fit polynomials when a strong match is found.
* Created a debugging mode, to show the top-down and fitted perspective images.
* Calculated left and right line radius, and the cars distance to center.

See `Advanced Lane Lines.ipynb` file for a complete overview of the pipeline,
and extensive example images for each step.

The `output.mp4` file shows the final fitted lane, and the `debug_output.mp4`
file contains the output image, as well as two images from the pipeline.  The
left image contains the filtered input image from a top-down perspective, with
the lane-line masks overlaid.  The right image features the top-down image
after filtering by the masks, with the current fit polynomial overlaid in green,
and the smoothed fit line overlaid in red.

#### Future Work and Potential Failures

The pipeline is not resilient to other highly-visible lines running vertically
parallel to the lane lines.  It's also unlikely to work for lane lines that
are a very different color, or under significantly different lighting
conditions.  The image filtering step could likely be significantly improved
by training a neural network to identify the lines.  The brightness and
contrast could be adjusted (and maybe also the lane line colors) to simulate
other lighting or road conditions.  More importantly, in the real world, things
like old lines that have been partially removed, unmarked lines, or road
construction could easily confuse the algorithm.

The perspective adjustment could be improved by adjusting for uphill or downhill
driving, since the assumption at this point is for straight and flat driving.
Adaptive perspective adjustment would enable more true calculation or turn
radius, but even absent that, the algorithm does a good job of fitting road
lines.

### Project Goals

[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

The goals / steps of this project are the following:

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply the distortion correction to the raw image.
* Use color transforms, gradients, etc., to create a thresholded binary image.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Detect lane pixels and fit to find lane boundary.
* Determine curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.

---

The images for camera calibration are stored in the folder called `camera_cal`.  The images in `test_images` are for testing your pipeline on single frames.  To help the reviewer examine your work, please save examples of the output from each stage of your pipeline in the folder called `ouput_images`, and include a description in the README for the project of what each image shows.    The video called `project_video.mp4` is the video your pipeline should work well on.

The `challenge_video.mp4` video is an extra (and optional) challenge for you if you want to test your pipeline under somewhat trickier conditions.  The `harder_challenge.mp4` video is another optional challenge and is brutal!

If you're feeling ambitious (again, totally optional though), don't stop there!  We encourage you to go out and take video of your own, calibrate your camera and show us how you would implement this project from scratch!
