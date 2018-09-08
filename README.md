
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

The original dataset is from [SKI10 contest](http://www.ski10.org/) - It is composed of 100 MRIs and their corresponding segmentations. I am not allowed to upload the dataset. Check their [website](http://www.ski10.org/) to download the full dataset.

![ski10 slice](https://user-images.githubusercontent.com/39532549/45259360-43d8b580-b388-11e8-8754-e97a64866b7f.PNG)

Say what the step will be

```
Give the example
```

And repeat

```
until finished
```

End with an example of getting some data out of the system or using it for a little demo

## Running the tests

Explain how to run the automated tests for this system

### Pre-processing

Run the notebook Pre-processing.ipynb to pre-process the data. 
Below are the steps to pre-process the labels.

![pre processing3](https://user-images.githubusercontent.com/39532549/45259411-733bf200-b389-11e8-9cae-1984b5de1a3c.PNG)


Check the notebook for more details.

```
Give an example
```

### Training

Explain what these tests test and why

![training](https://user-images.githubusercontent.com/39532549/45259475-26591b00-b38b-11e8-84aa-d9b5c9164c26.png)


```
Give an example
```

## Networks combination

![combination](https://user-images.githubusercontent.com/39532549/45259484-64563f00-b38b-11e8-8ff3-efcfb744846f.PNG)

Add additional notes about how to deploy this on a live system

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
