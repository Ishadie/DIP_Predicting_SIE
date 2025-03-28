# Satellite Image Processing in the Circumpolar North: Approaches for Understanding Climate Crisis by Predicting Arctic Sea Ice Extent 

# Introduction
Over the past few decades, extreme weather events have become more common and violent due to the retreat of the Arctic Sea ice, which has changed regional and global climate patterns. The satellite image patterns show that enormous sea ice loss is critical to Arctic amplification. The Arctic sea ice retreat due to climate change threatens the environment significantly. As a critical component that helps understand the climate crisis, changes in Arctic ice require accurate analysis and prediction. Various researchers have used machine learning and deep learning models for sea ice forecasting. 

This research focuses on processing satellite images using digital image processing techniques and uses a deep learning model that takes multimodal data to analyze time series forecasting of future ice extent. We leverage image processing techniques such as Optical Character Recognition (OCR) for detecting the text of the image and handling missing data, Oriented FAST and Rotated BRIEF (ORB) for aligning images, low-pass filter for denoising satellite images, and Otsu’s thresholding for segmenting ice regions from land and ocean. We then use Canny Edge Detection for feature extraction to highlight sea ice boundaries. We extract contours, calculate the ice retreat percentage from the image, and finally, find changes in ice coverage using image subtraction. After processing the images, we use a transformer-based model to perform a time series prediction of future ice extent. The transformer-based model is designed in a way that it takes multimodal data, one modality is hand-crafted numerical features from satellite images while the other modality is processed satellite images. 

![DIP SIE workflow](https://github.com/user-attachments/assets/ecaa764d-e1df-41a6-8471-0ce6fd17cea3)


# Dataset
We will use Arctic sea ice data acquired from the National Snow and Ice Data Center (NSIDC) in this research. The data we are using consists of images from July 16th to August 16th of the years 1979 to 2024. If there is no data at all for a day, the image is labeled with “NO DATA”. The naming convention ```“h_yyyymmdd_extn_[blmrbl]_[hires]_vX.x.png”``` is used for labeling the images.

The whole dataset is available ​​at https://noaadata.apps.nsidc.org/NOAA/G02135/north/daily/images/

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

From the pre-processed images, three handcrafted features - ice coverage, ice retreat percentage from the previous year, and ice retreat percentage since 1979 are extracted by using the following techniques:

- ```Circular Masking```: We have applied a circular binary mask to remove legends, borders and kept only the polar region.
- ```Edge Detection```: Canny Edge detection has been used to highlight the sharp boundaries of sea ice edges.
- ```Contour Detection```: Contours are extracted from the ice mask.
- ```Ice Area Calculation```: We have measured the pixel area of all valid contours and computed the ice coverage as a percentage of the total image size.
- ```Image Subtraction```: Image subtraction is performed to find the absolute pixel difference between two masks (previous vs. current year).
- ```Retreated Area Calculation```: Retreat area is computed as a percentage of total image area, based on the thresholded difference mask.
- ```Overlay Visualization```: Overlay visualization has been performed to evaluate if the ice-covered area is properly detected.

  ![image feature extraction](https://github.com/user-attachments/assets/b96bfb44-f209-4792-9d88-8e5035589a3a)




