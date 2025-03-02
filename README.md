

# Requirements
Ensure you have the following dependencies installed:
- Python 3.x
- OpenCV (cv2)
- NumPy
- Matplotlib

You can install the required libraries using:

pip install opencv-python numpy matplotlib


# Q1: Coin Segmentation using OpenCV
## Overview
The problem involved segmenting and counting the number of coins in an image using OpenCV. The approach includes grayscale conversion, smoothing, thresholding, edge detection, and contour detection to identify coin boundaries.

##  Methodology
- Image Loading: I load the image in color and convert it to RGB format for proper visualization in Matplotlib.
- Grayscale Conversion: I convert the image to grayscale to simplify processing, as color is not required for segmentation.
- Gaussian Blur: I apply a 5x5 Gaussian kernel to smoothen the image, reducing noise and minor variations that could affect thresholding.
- Edge Detection: Before thresholding, I use Canny edge detection to highlight regions with sharp intensity changes, which helps in detecting coin boundaries more accurately. I set threshold values (100, 200) to capture significant edges while reducing noise.
- Dynamic Thresholding : Instead of setting a fixed threshold, I use Otsu’s thresholding (cv2.THRESH_BINARY + cv2.THRESH_OTSU). This method dynamically determines the optimal threshold value by analyzing the image histogram, ensuring robust segmentation across varying lighting conditions. Since this technique classifies pixels into foreground and background regions based on intensity, it falls under region-based segmentation.
- Contour Detection: Using cv2.findContours(), I identify connected components in the thresholded image. Contours are extracted from the binarized image to detect object boundaries, helping in isolating individual coins.
- Sorting Contours by Area: I sort the detected contours in descending order based on their area to prioritize larger objects (coins) over noise.Also a form of region based segmentation as I form an area mask.
- Counting Coins: The first detected contour typically corresponds to the entire image, so I ignore it. I then count contours with an area greater than 10,000 pixels, assuming they represent coins.
- Drawing Contours: I draw the detected contours on the original image to visualize the segmented coins.

# Q2: Creating a stitched panorama from multiple overlapping images

## Overview

This approach involves stitching together a series of images to create a panorama. The methodology utilizes the SIFT feature detector and BFMatcher to match features between images and then computes the homography matrix to stitch the images together.

##Methodology
- Image Loading: Images are loaded from a specified directory.
- SIFT Feature Detection: SIFT keypoints and descriptors are detected for each image. This helps in finding distinctive features that can be matched across images.
- Matching Features: BFMatcher is used to match descriptors between consecutive images, and good matches are selected based on distance.
- Homography Calculation: Using the matched keypoints, a homography matrix is computed using RANSAC, which aligns the images based on their feature points.
- Image Stitching: The images are warped and blended to create a seamless panorama.
- Cropping Black Regions: After stitching, black regions (from the warping process) are cropped out to ensure the final image only contains the relevant content.




