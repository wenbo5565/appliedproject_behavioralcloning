# **Behavioral Cloning** 

---

**Behavioral Cloning Project**

The goals / steps of this project are the following:
* Use the simulator to collect data of good driving behavior
* Build, a convolution neural network in Keras that predicts steering angles from images
* Train and validate the model with a training and validation set
* Test that the model successfully drives around track one without leaving the road
* Summarize the results with a written report

## Rubric Points
### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/432/view) individually and describe how I addressed each point in my implementation.  

---
### Files Submitted & Code Quality

#### 1. Submission includes all required files and can be used to run the simulator in autonomous mode

My project includes the following files:
* model.py containing the script to create and train the model
* drive.py for driving the car in autonomous mode
* model.h5 containing a trained convolution neural network 
* writeup_report.md summarizing the results

#### 2. Submission includes functional code
Using the Udacity provided simulator and my drive.py file, the car can be driven autonomously around the track by executing 
```sh
python drive.py model.h5
```

#### 3. Submission code is usable and readable

The model.py file contains the code for training and saving the convolution neural network. The file shows the pipeline I used for training and validating the model, and it contains comments to explain how the code works.

### Model Architecture and Training Strategy

#### 1. An appropriate model architecture has been employed

Nvidia proposes a powerful neural network architecture in the paper [End to End Learning for Self-Driving Cars](https://images.nvidia.com/content/tegra/automotive/images/2016/solutions/pdf/end-to-end-dl-using-px.pdf). We leverage the same neural network as our task is very similar to theirs'.

The architecture is showed as follows:

<p align="center"> 
<img src = "https://github.com/wenbo5565/appliedproject_behavioralcloning/blob/master/image/cnn.JPG" height=30%>
</p>

#### 2. Attempts to reduce overfitting in the model

The model was trained and validated on different data sets to ensure that the model was not overfitting. Although there is deviance between training loss and validation loss, the model was tested by running it through the simulator and was demonstrated that the vehicle could stay on the track.

In addition, I also experimented L2 regularization techniques. The model with L2 penalization doesn't perform well in autonomous mode.

So I keep a neural network without regularization.

<p align="center"> 
<img src="https://github.com/wenbo5565/appliedproject_behavioralcloning/blob/master/image/loss.png">
</p align="center"> 

#### 3. Model parameter tuning

The model used an adam optimizer, so the learning rate was not tuned manually.

#### 4. Appropriate training data

Training data was chosen to keep the vehicle driving on the road. I used a combination of center lane driving, recovering from the left and right sides of the road. Training data contains images from all three center, left and right placed cameras.

For details about how I created the training data, see the next section. 

### Model Architecture and Training Strategy

#### 1. Solution Design Approach

In order to derive an effective architecture, we leverage bias-variance trade-off in the training process. Our general philosphy is

 * Start from a simple model to see if training loss is satisfactory (small enough) to our project
 * If training loss is large, then adding model complexity by increasing layers or neurons in the simple neural network
 * If training loss is small but validation loss is large, it indicates our model suffers from high variance. We have to use regularization techniques to decrease the variance such as add dropout layers or penalization terms.
 * If both training loss and validation loss are satisfactory, we test our model on the automous mode to see if the vehicle can drive autonomously around the track.

Since Nvidia has published a very powerful architecture as mentioned above, we directly start from its architecture. Fortunately this architecture performs very well for our project as well

#### 2. Final Model Architecture

Plese see viasulizaiton of the architecture as above.

#### 3. Creation of the Training Set & Training Process

To capture good driving behavior, we first record two laps on track one using center lane driving. Here is an example image of center lane driving:

<p align="center"> 
    <img src ="https://github.com/wenbo5565/appliedproject_behavioralcloning/blob/master/image/center1.jpg">
</p>

To avoid biases in the data set (much more left turns than right turns) , we also drive the car on the reversed direction. Here is an example of flipped images.

<p align="center"> 
<img src ="https://github.com/wenbo5565/appliedproject_behavioralcloning/blob/master/image/reverse.jpg">
</p>

After preliminary training and testing, we found that the vechile performs not well in areas that lane marking is not well defined. So we collect more data specific to those areas to augment our dataset. Here is an example of such an area.

<p align="center"> 
<img src ="https://github.com/wenbo5565/appliedproject_behavioralcloning/blob/master/image/unclearmarking.jpg">
</p>

We finally randomly shuffled the data set and put 20% of the data into a validation set. 

We used this training data for training the model. The validation set helped determine if the model was over or under fitting. The ideal number of epochs was 15 as evidenced by the training/validation loss figure. We used an Adam optimizer so that manually training the learning rate wasn't necessary.

### Simulation Test

We test the final model in automous mode in Udacity's simulator. The trained neural network model drives the vechile well without leaving away drivable way. A sample video recording can be found at [autonomous recording](https://github.com/wenbo5565/appliedproject_behavioralcloning/blob/master/autonomous%20mode%20recording.mp4)
