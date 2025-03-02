Requirements

Ensure you have the following dependencies installed:

Python 3.x
OpenCV (cv2)
NumPy
Matplotlib

You can install the required libraries using:

pip install opencv-python numpy matplotlib



## Q1: Coin Segmentation using OpenCV

## Overview

The problem involved  segmenting and counting the number of coins in an image using OpenCV. The approach includes grayscale conversion, smoothing, thresholding, edge detection, and contour detection to identify coin boundaries.


### Methodology

1. **Image Loading**: I load the image in color and convert it to RGB format for proper visualization in Matplotlib.
2. **Grayscale Conversion**: I convert the image to grayscale to simplify processing, as color is not required for segmentation.
3. **Gaussian Blur**: I apply a 5x5 Gaussian kernel to smoothen the image, reducing noise and minor variations that could affect thresholding.
4. **Edge Detection**: Before thresholding, I use Canny edge detection to highlight regions with sharp intensity changes, which helps in detecting coin boundaries more accurately. I set threshold values (100, 200) to capture significant edges while reducing noise.
5. **Dynamic Thresholding (Region-Based Segmentation)**: Instead of setting a fixed threshold, I use Otsu’s thresholding (`cv2.THRESH_BINARY + cv2.THRESH_OTSU`). This method dynamically determines the optimal threshold value by analyzing the image histogram, ensuring robust segmentation across varying lighting conditions. Since this technique classifies pixels into foreground and background regions based on intensity, it falls under **region-based segmentation**.
6. **Contour Detection**: Using `cv2.findContours()`, I identify connected components in the thresholded image. Contours are extracted from the binarized image to detect object boundaries, helping in isolating individual coins.
7. **Sorting Contours by Area**: I sort the detected contours in descending order based on their area to prioritize larger objects (coins) over noise.
8. **Counting Coins**: The first detected contour typically corresponds to the entire image, so I ignore it. I then count contours with an area greater than 10,000 pixels, assuming they represent coins.
9. **Drawing Contours**: I draw the detected contours on the original image to visualize the segmented coins.

### Results and Observations

- The script successfully identifies and counts coins in the image.
- The first contour detected corresponds to the entire image, so I ignore it.
- Contours with an area greater than 10,000 pixels are considered coins.
- Canny edge detection improves segmentation by enhancing coin boundaries.
- **Thresholding is a region-based segmentation method**, as it segments the image into foreground and background.
- **Contours are extracted from the thresholded image to detect object boundaries** but are not inherently region-based.
- The number of detected coins is printed and displayed with contours drawn around them.


