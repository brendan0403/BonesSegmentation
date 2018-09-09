
# Knee MRI Bones segmentation by Deep Learning

This project is the segmentation of knee bones on MRI images using a U-net network.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

What things you need to install the software and how to install them

```
Give examples
```

### Data

The original dataset is from [SKI10 contest](http://www.ski10.org/) - It is composed of 100 MRIs and their corresponding segmentations. 

![ski10 slice](https://user-images.githubusercontent.com/39532549/45259360-43d8b580-b388-11e8-8754-e97a64866b7f.PNG)

I am not allowed to upload the dataset. Check SKI10 [website](http://www.ski10.org/) to download the full dataset.


### Pre-processing

As I use U-net 2D it is necessary to provide images at the input of the network. I chose to provide the network with 128x128 slices because the GPU memory of my machine did not allow more.
Below are the steps to pre-process the SKI10 labels.

![pre processing3](https://user-images.githubusercontent.com/39532549/45259411-733bf200-b389-11e8-9cae-1984b5de1a3c.PNG)

Run the notebook Pre-processing.ipynb to pre-process the data and check it for more details.



### Network

## Model

The architecture was inspired by [U-Net: Convolutional Networks for Biomedical Image Segmentation](https://lmb.informatik.uni-freiburg.de/people/ronneber/u-net/)
I tried several architectures and this one had the best results.


![unet](https://user-images.githubusercontent.com/39532549/45259622-23135e80-b38e-11e8-900c-3c56b398ccd7.PNG)



## Training

Once the data has been pre-processed, the network is ready to be trained. 
Training on 150 epochs takes around 8 hours with a Nvidia geforce gtx 1080 TI (batch size=32). However 60 epochs are enough. 
For the training I used the DICE coefficient as a cost function.
Check the notebook training.ipynb for more hyperparameters.

![training](https://user-images.githubusercontent.com/39532549/45259475-26591b00-b38b-11e8-84aa-d9b5c9164c26.png)


## Networks combination

In addition to network optimization, I was trying to come up with ideas to improve my segmentations thanks to pre-processing or post-processing. I had the idea to combine 3 U-net neural networks. My concept was to train each of them for a different view and then combine the results.

After slightly changing the pre-processing and training the three networks independently I had to find a way to combine their segmentations.
The main challenge to combine the different segmentations is that the volumes are not cubic. Indeed, even if every slices are resized in 128x128 during the pre-processing, the number of slices for each plane is not the same because originally the volumes were not cubic.
Therefore, to combine the results of the three segmentations, it is necessary to group the segmented slices of the same MRI into a volume for each network and then to rotate and resize the segmented volumes so that they have the same dimensions and orientation. 

In the notebook Networks combination - DICE Calculation.ipynb you can either resize the volume in 128x128x128 or resize it to its original size.
You can also calculate the DICE coefficient between the combined segmentation and the gold standard for a whole volume. DICE coefficient is also calculated for the Sagittal, Axial, and Coronnal segmentation independently.

![combination](https://user-images.githubusercontent.com/39532549/45259539-a2079780-b38c-11e8-99ec-eaea68e99af1.PNG)


## Results


![resultsv](https://user-images.githubusercontent.com/39532549/45259532-5bb23880-b38c-11e8-8e95-d97a9195b9a3.PNG)



* [Dropwizard](http://www.dropwizard.io/1.0.2/docs/) - The web framework used
* [Maven](https://maven.apache.org/) - Dependency Management
* [ROME](https://rometools.github.io/rome/) - Used to generate RSS Feeds

## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/your/project/tags). 

## Authors

* **Billie Thompson** - *Initial work* - [PurpleBooth](https://github.com/PurpleBooth)

See also the list of [contributors](https://github.com/your/project/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Hat tip to anyone whose code was used
* Inspiration
* etc

```
