# Convolutional Neural Network for detecting Lung Nodules

### Content

1. Prerequisites

### Prerequisites:

* Install [Tensorflow](https://www.tensorflow.org/install/)
* Install [Tflearn](http://tflearn.org/)
* Install [SimpleITK](http://www.simpleitk.org/)
* Install [PIL](http://pythonware.com/products/pil/) (Python Imaging Library)

## Introduction

A **computerized tomography (CT)** scan consists of a series of X-ray images taken from different angles and combines them to create *cross-sectional images*, or slices, of the bones, soft tissues, etc. inside our body.

Since CT scans consist of *slices* which amalgamate a **3D view**, this technology allows radiologists to analyze the body in high-resolution 3D representations.

## Data from CT scans

CT scans contain 2D arrays with *pixel intensities* in DICOM files. However CT scans are not in the standard *0–255 range*, but are instead in **HU (Hounsfield Units)**

> **HU** measure the radio-intensity of particular  mediums based on their attenuation coefficients. *Attenuation coefficients* give a measure of how easily X-rays can pass through a particular medium.

They range from *-1000 HU for air, to 0 HU for distilled water*. In our case *Lung CT scans*, we have the following range:

* Max HU: 400
* Min HU: -1000

Once we clamp our input to a **particular intensity window range** as a preprocessing step, we can *normalize the resulting data to 0–255* and produce an image which can be used to train machine learning models.

## Dataset



### References:

1. [Stanford AI for Healthcare](https://medium.com/stanford-ai-for-healthcare/superman-isnt-the-only-one-with-x-ray-vision-deep-learning-for-ct-scans-290aaa7ba5c1)

2. [Example of the 3 Convolutional layer](https://github.com/swethasubramanian/LungCancerDetection)

3. [Dataset: LUNA16](https://luna16.grand-challenge.org/home/)

4. [Tutorial to manage to open, visualize, transform cartesian coordinates to voxel coordinates](https://luna16.grand-challenge.org/tutorial/)
