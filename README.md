
# Knee MRI Bones segmentation by Deep Learning

This project is the segmentation of knee bones on MRI images using a U-net network. It was part of my end-of-studies internship at AMMI laboratory in University of Alberta.

## Prerequisites

This project depends on the following libraries:

```
Keras
Tensorflow
Numpy
Opencv
SimpleITK
Scipy
Skimage
Matplotlib
```
It has been developped using Python 3.6, Anaconda and Jupyter Notebook.

## Data

The original dataset is from [SKI10 contest](http://www.ski10.org/) - It is composed of 100 MRIs and their corresponding segmentations. 

![ski10 slice](https://user-images.githubusercontent.com/39532549/45259360-43d8b580-b388-11e8-8754-e97a64866b7f.PNG)

I am not allowed to upload the dataset. Check SKI10 [website](http://www.ski10.org/) to download the full dataset then copy it in the data folder.


## Pre-processing

As I use U-net 2D it is necessary to provide images at the input of the network. I chose to provide the network with 128x128 slices because the GPU memory of my machine did not allow more.
Below are the steps to pre-process the SKI10 labels.

![pre processing3](https://user-images.githubusercontent.com/39532549/45259411-733bf200-b389-11e8-9cae-1984b5de1a3c.PNG)

Run the notebook Pre-processing.ipynb to pre-process the data and check it for more details.



## Network

### Model

The architecture was inspired by [U-Net: Convolutional Networks for Biomedical Image Segmentation](https://lmb.informatik.uni-freiburg.de/people/ronneber/u-net/)
I tried several architectures and this one had the best results.


![unet](https://user-images.githubusercontent.com/39532549/45259622-23135e80-b38e-11e8-900c-3c56b398ccd7.PNG)



### Training

Once the data has been pre-processed, the network is ready to be trained. 
Training on 150 epochs takes around 8 hours with a Nvidia geforce gtx 1080 TI (batch size=32). However 60 epochs are enough. 
For the training I used the DICE coefficient as a cost function.
Check the notebook training.ipynb for more hyperparameters.

![train loss](https://user-images.githubusercontent.com/39532549/45259782-1abd2280-b392-11e8-9c04-6d5efd2df5ca.PNG)

The network weight files are too large to be uploaded on Github. Train the networks by yourself or contact me.

## Networks combination

In addition to the hyperparameters tuning, I tried to improve my segmentations thanks to pre-processing or post-processing. I also had the idea to combine three U-net neural networks. The concept was to train each of them for a different plane (Sagittal, Axial and Coronal) and then combine the results.

After slightly changing the pre-processing and training the three networks independently I had to find a way to combine their segmentations.
The main challenge to combine the different segmentations is that the volumes are not cubic. Indeed, even if every slices are resized in 128x128 during the pre-processing, the number of slices for each plane is not the same because originally the volumes are not cubic.
Therefore, to combine the results of the three segmentations, it is necessary to aggregate the segmented slices of the same MRI into a volume for each network and then to rotate and resize the segmented volumes so that they have the same dimensions and orientation. 

In the notebook Networks combination - DICE Calculation.ipynb it is possible to resize the segmentations in 128x128x128 or to its original size.
To evaluate the segmentation, DICE coefficient between the combined segmentation and the gold standard is calculated for a whole volume. DICE coefficient is also calculated for the Sagittal, Axial, and Coronnal segmentation independently.

![combination](https://user-images.githubusercontent.com/39532549/45259539-a2079780-b38c-11e8-99ec-eaea68e99af1.PNG)


## Results

Segmentations of the test set are very accurate, the average DICE coefficient is 0.98.

Test set segmentations visualized on Slicer 3D :

![resultsv](https://user-images.githubusercontent.com/39532549/45259532-5bb23880-b38c-11e8-8e95-d97a9195b9a3.PNG)




## Authors

* **Brendan Robert** - *AMMI Lab* - University of Alberta

