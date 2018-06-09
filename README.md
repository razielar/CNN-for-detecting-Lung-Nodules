# CNN for detecting Lung Nodules from CT scans


### Content

1. [Prerequisites](#Prerequisites)
2. [Introduction](#Introduction)
3. [Data from CT scans](#Data)
4. [Preprocessing](#LUNA16)
5. [Building a Convolutional Neural Network](#CNN)
6. [References](#References)

### <a id='Prerequisites'></a> Prerequisites:

* Install [Tensorflow](https://www.tensorflow.org/install/)
* Install [Tflearn](http://tflearn.org/)
* Install [SimpleITK](http://www.simpleitk.org/)
* Install [PIL](http://pythonware.com/products/pil/) (Python Imaging Library)

## <a id='Introduction'></a> Introduction


A **computerized tomography (CT)** scan consists of a series of X-ray images taken from different angles and combines them to create *cross-sectional images*, or slices, of the bones, soft tissues, etc. inside our body.

Since CT scans consist of *slices* which amalgamate a **3D view**, this technology allows radiologists to analyze the body in high-resolution 3D representations.


## <a id='Data'></a> Data from CT scans


CT scans contain 2D arrays with *pixel intensities* in DICOM files. However CT scans are not in the standard *0–255 range*, but are instead in **HU (Hounsfield Units)**

> **HU** measure the radio-intensity of particular  mediums based on their attenuation coefficients. *Attenuation coefficients* give a measure of how easily X-rays can pass through a particular medium.

They range from *-1000 HU for air, to 0 HU for distilled water*. In our case *Lung CT scans*, we have the following range:


* Max HU: 400
* Min HU: -1000

Once we clamp our input to a **particular intensity window range** as a preprocessing step, we can *normalize the resulting data to 0–255* and produce an image which can be used to train machine learning models.

## <a id='LUNA16'></a> Preprocessing


We are going to use the [LUNA16](https://luna16.grand-challenge.org/home/) dataset which contains *888 CT scans*. The images have a *.mhd format* and *.raw files*. The [SimpleITK](http://www.simpleitk.org/) library can be used to read the .mhd files. Each CT scan has dimensions of **512x512xn**, where **n** is the number of axial scans. There are about **200 images** in **each CT scan**.

There are a total of **551065 annotations**. Of all the annotations provided, **1351** were labeled as **nodules**, rest were labeled negative (**549714**). So there *big class imbalance*.

We could potentially *train the CNN on all the pixels*, but that would *increase the computational cost and training time*. So instead I just decided to **crop the images around** the **coordinates provided** in the annotations. The annotation were provided in **Cartesian coordinates**. So they had to be **converted to voxel coordinates**. Also the **image intensity** was defined in **HU scale**. So it had to be rescaled for image processing purposes.

The script would generate **50 x 50 grayscale images** for training, testing and validating a CNN.

## <a id='CNN'></a> Building a Convolutional Neural Network


For building a CNN [Tflearn](http://tflearn.org/) will be used. Tflearn is a high-level API wrapper around tensorflow. Using a 3 convolutional layers in the architecture.

### <a id='References'></a> References:

1. [Stanford AI for Healthcare](https://medium.com/stanford-ai-for-healthcare/superman-isnt-the-only-one-with-x-ray-vision-deep-learning-for-ct-scans-290aaa7ba5c1)

2. [Example of the 3 Convolutional layer](https://github.com/swethasubramanian/LungCancerDetection)

3. [Dataset: LUNA16](https://luna16.grand-challenge.org/home/)

4. [Tutorial to manage to open, visualize, transform cartesian coordinates to voxel coordinates](https://luna16.grand-challenge.org/tutorial/)
