# Vehicle Detection
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

The Project
---

The goals / steps of this project are the following:

* Perform a Histogram of Oriented Gradients (HOG) feature extraction on a labeled training set of images and train a classifier Linear SVM classifier
* Implement a sliding-window technique and use your trained classifier to search for vehicles in images.
* Run your pipeline on a video stream (start with the test_video.mp4 and later implement on full project_video.mp4) and create a heat map of recurring detections frame by frame to reject outliers and follow detected vehicles.
* Estimate a bounding box for vehicles detected.

[//]: # (Image References)

[image1]: ./output_images/car_samples.png "Car Samples"
[image3]: ./output_images/non_car_samples.png "Non-car Samples"
[image4]: ./output_images/HOG_comparison.png "HOG Comparison"
[image5]: ./output_images/bbox_vis.png "Region Proposal Visualisation"
[image6]: ./output_images/heatmap.png "Heatmap"
[image7]: ./output_images/video_thumbnail.jpg "Video Thumbnail"

Here are links to the labeled data for [vehicle](https://s3.amazonaws.com/udacity-sdc/Vehicle_Tracking/vehicles.zip) and [non-vehicle](https://s3.amazonaws.com/udacity-sdc/Vehicle_Tracking/non-vehicles.zip) examples provided by Udacity.  These example images come from a combination of the [GTI vehicle image database](http://www.gti.ssr.upm.es/data/Vehicle_database.html), the [KITTI vision benchmark suite](http://www.cvlibs.net/datasets/kitti/).

## Basic Summary of Dataset
We begin in Vehicle_Detector.ipynb cell 3, with a summary of the provided dataset:

No. of car images:  8792

No of non-car images:  8968

Image shape:  (64, 64, 3)

The dataset is fairly balanced.

### Car Image Examples
![alt_text][image1]

### Non-car Image Examples
![alt_text][image3]

## Feature Extraction Method
Methods for feature extraction are created in cell 6. This is code previously prepared
during the Udacity lecture. 

`bin_spatial()` computes binned colour features by scaling images down.

`color_hist()` computes colour histogram features.

`get_hog_features()` returns HOG features and visualisation.

`extract_features()` wraps and combines the above functions.

## HOG Visualisation
![alt_text][image4]

## Data Preparation
I felt the dataset was large enough, and did not require further augmentation for this relatively simple classifier.
In cell 9 we apply a scaler to the feature vector, and split the data into training/validation sets.

## Classifier
In cell 11 I run the classifier on the dataset with a 0.989 accuracy. There is a chance of overfitting here,
but its effects proved to be acceptable for the purposes of this exercise.

## HOG Sub-sampling Window Search
In cell 14, I build the function for the HOG window search routine. This is a region proposer that scans select portions of the image
and checks for presence of a vehicle. The cell size and cell position are determined by the way the road is laid out, and the
distance of vehicles from the camera. An example is shown below, of where the window search is told to look.

![alt_text][image5]
 
## Heatmap
By overlaying successful hits in each bounding box, I am able to form a heatmap of the areas on the image which are likely to be cars.
![alt_text][image6]

## Final Pipeline
All that's left to do now is to process the entire video. Here is it on Youtube.
[![Vehicle Detection][image7]](https://www.youtube.com/watch?v=zNlnjWxU6DM&feature=youtu.be "Vehicle Detection Video")

## Conclusion
This algorithm is not a fast one - it appears to take 15 minutes on my (slow) laptop.
Nonetheless, it was a fantastic learning experience. There's quite a bit of noise from the opposing lane,
but for the purposes of this exercise, I felt it was acceptable.

I'd like to attempt a deep learning approach to this project. Perhaps an implementation of the
[tinyYOLO network by pjreddie](https://pjreddie.com/darknet/yolo/), which is fast and (relatively) accurate.
 

