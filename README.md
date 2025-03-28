# DIP_Predicting_SIE
# Introduction
# Digital Image Processing Techniques
## Pre-Processing Polar Image Data

Data is pre-processed using the following image processing techniques:
- ```Optical Character Recognition (OCR)```: The missing data are handled using OCR to detect the specific text(NO DATA) from images and remove such images.
  
![no data](https://github.com/user-attachments/assets/82bafdbd-155d-40c3-84fe-dd7b4dd3acd7)

- ```Resizing```: All images are resized maintaining a uniform size (512x512) for alignment.
- ```Oriented FAST and Rotated BRIEF (ORB)```: Images are aligned to a reference image using keypoint matching and geometric transformation, which is used for correcting shifts or rotations between different temporal images of the same region.
- ```Gaussian Blur```: Gaussian Blur is used to reduce sensor noise and smooth atmospheric distortions.
- ```Grayscale Conversion & Normalization```: Gray scale conversion is performed to reduce computational complexity, and normalization ensures uniform contrast across all images.
- ```Otsu's Thresholding```: Otsu's thresholding is used to automatically separate sea ice (white) from background (black) using intensity distribution.


![preprocess](https://github.com/user-attachments/assets/dce19c1a-1f04-412a-ac76-7fb1a03f5615)


## Feature Extraction from Polar Image Data
