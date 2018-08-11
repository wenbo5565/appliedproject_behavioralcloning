### Deep Learning Application Project - Behavioral Cloning

by Wenbo Ma

#### 1. Overview

Deep learning has been proven as a powerful tool to recognize patterns in images. In this project, we aim to build a convolutional neural network (CNN) to map image pixel values to steering angles for an autonomous car in a simulator. We collect data by driving the car manually in the simulator and recording both the images and angles. We train the CNN on an AWS EC2 instance with GPU enabled. To test the effectiveness of our CNN model, we test it in the simulator in an autonomous mode meaning the model takes image as an input and outputs the steering angles to control the car.

Here is a clip of the car in the autonomous mode.

#### 2. Network Architecture

##### General strategy to find a solution architecture

Generally we start from the LeNet-5 since it has been shown as an effective neural network for image recognition task. We then use bias-variance trade-off to firstly identify a satisfactory low-bias model and secondly leverage regularization techinique to further identify a satisfactory low bias and low variance model.

<p align='center'>
  <img src = "https://github.com/wenbo5565/appliedproject_behavioralcloning/blob/master/image/cnn.JPG" height="20%" width="60%">
</p>

##### Architecture for this project

Fortunately for this specific task, we don't need to start from LeNet-5 since Nvidia has published a very effective neural network architecture for self-driving cars. We start from this neural network and it turns out to be an effective architecture for our project.

<p align='center'>
  <img src = "https://github.com/wenbo5565/appliedproject_behavioralcloning/blob/master/image/lenet.png" height="100%" width="80%">
</p>

#### 3. Model Building

We split the entire dataset into training set (80%) and validation set (20%). We use the Adam optimizer to adaptively set the step length in the optimization algorithm. Additionly we divide the training set into batches, each of which consists of 32 samples. We train the model for 14 epoches as the validation loss starts to increase after 14 epoches.

<p align='center'>
  <img src = "https://github.com/wenbo5565/appliedproject_behavioralcloning/blob/master/image/loss.png" height="40%" width="40%">
</p>

From the figure above, we can see that the model suffers from high variance. To remedy this problem, we seek to add l2 penalization to all weights in the neural network. We observe that regularization decreases the variance, the regularized model is worse than the un-regularized one under autonomous mode in the simulator. So we keep the un-regularized network as our final model.

#### 4. Testing

We deploy the trained neural network in the simulator to drive the car autonomously. The result demonstrate that the trained model can effectively drive the car without leaving away the road.

You can find related technical details at

[model.py](https://github.com/wenbo5565/appliedproject_behavioralcloning/blob/master/model.py) - Python code for building the CNN model

[model.h5](https://github.com/wenbo5565/appliedproject_behavioralcloning/blob/master/model.h5) - Trained CNN model

[video.mp4 - recording of one lap of automous drive](https://github.com/wenbo5565/appliedproject_behavioralcloning/blob/master/autonomous%20mode%20recording.mp4) - A video clip demonstrating the autonomous test

[written summary](https://github.com/wenbo5565/appliedproject_behavioralcloning/blob/master/project_submission_writeup.md) - Technical summary
