### Deep Learning Application Project - Behavioral Cloning

#### Overview

Deep learning has been proven as a powerful tool to recognize patterns in images. In this project, we aim to build a convolutional neural network (CNN) to map image pixel values to steering angles for an autonomous car in a simulator. We collect data by driving the car manually in the simulator and recording both the images and angles. We train the CNN on an AWS EC2 instance with GPU enabled. To test the effectiveness of our CNN model, we test it in the simulator in an autonomous mode meaning the model takes image as an input and outputs the steering angles to control the car.

Here is a clip of the car in the autonomous mode.

#### Network Architecture

##### General strategy to find a solution architecture

Generally we start from the LeNet-5 since it has been shown as an effective neural network for image recognition task. We then use bias-variance trade-off to firstly identify a satisfactory low-bias model and secondly leverage regularization techinique to further identify a satisfactory low bias and low variance model.

<p align='center'>
  <img src = "https://github.com/wenbo5565/appliedproject_behavioralcloning/blob/master/image/cnn.JPG" height="10%">
</p>

##### Architecture for this project

Fortunately for this specific task, we don't need to start from LeNet-5 since Nvidia has published a very effective neural network architecture for self-driving cars. We start from this neural network and it turns out to be an effective architecture for our project.

<p align='center'>
  <img src = "https://github.com/wenbo5565/appliedproject_behavioralcloning/blob/master/image/lenet.png">
</p>

#### Link for submission purpose only
==========================

[drive.py](https://github.com/wenbo5565/appliedproject_behavioralcloning/blob/master/drive.py)

[model.py](https://github.com/wenbo5565/appliedproject_behavioralcloning/blob/master/model.py)

[model.h5](https://github.com/wenbo5565/appliedproject_behavioralcloning/blob/master/model.h5)

[video.mp4 - recording of one lap of automous drive](https://github.com/wenbo5565/appliedproject_behavioralcloning/blob/master/autonomous%20mode%20recording.mp4)

[written summary](https://github.com/wenbo5565/appliedproject_behavioralcloning/blob/master/project_submission_writeup.md)
