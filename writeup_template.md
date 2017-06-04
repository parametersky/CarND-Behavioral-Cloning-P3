#**Behavioral Cloning** 
---

**Behavioral Cloning Project**

The goals / steps of this project are the following:
* Use the simulator to collect data of good driving behavior
* Build, a convolution neural network in Keras that predicts steering angles from images
* Train and validate the model with a training and validation set
* Test that the model successfully drives around track one without leaving the road
* Summarize the results with a written report


## Rubric Points
###Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/432/view) individually and describe how I addressed each point in my implementation.  

---
###Files Submitted & Code Quality

####1. Submission includes all required files and can be used to run the simulator in autonomous mode

My project includes the following files:
* model.py containing the script to create and train the model
* drive.py for driving the car in autonomous mode
* model.h5 containing a trained convolution neural network 
* writeup_report.md or writeup_report.pdf summarizing the results

####2. Submission includes functional code
Using the Udacity provided simulator and my drive.py file, the car can be driven autonomously around the track by executing 
```sh
python drive.py model.h5
```

####3. Submission code is usable and readable

The model.py file contains the code for training and saving the convolution neural network. The file shows the pipeline I used for training and validating the model, and it contains comments to explain how the code works.
1. read from csv file to get all images path, and split to training and validating samples
2. build model using Nvidia network
3. build generator 
4. training model 
###Model Architecture and Training Strategy

####1. An appropriate model architecture has been employed
I use Nvidia network for training. First I add cropping layer to remove 70px from the top and 20px from the bottom.
The model consists of 5 convolution neural network with 3x3 filter,5x5 fileter sizes and depths between 24 and 64 (model.py lines 65~70) 

Before I train the model, I grayscale all images and do normalization by (data-128.0)/128.0.


####3. Model parameter tuning

The model used an adam optimizer, so the learning rate was not tuned manually (model.py line 79).

####4. Appropriate training data

Training data was chosen to keep the vehicle driving on the road. I used a combination of center lane driving, recovering from the left and right sides of the road, handling road type change.

For details about how I created the training data, see the next section. 

###Model Architecture and Training Strategy

####1. Solution Design Approach

Follow the course, first I using LeNet and then find that Nvidia's network have a better performance. Later I decide to get more training data to train the model.

In order to gauge how well the model was working, I split my image and steering angle data into a training and validation set. I found that my first model had a low mean squared error on the training set but a high mean squared error on the validation set. This implied that the model was overfitting. 

To combat the overfitting, I gather more training data.


The final step was to run the simulator to see how well the car was driving around track one. There were a few spots where the vehicle fell off the track:
1. running to the brown track, to improve the driving behavior in these cases, I gather data around the brown track and train the model 

At the end of the process, the vehicle is able to drive autonomously around the track without leaving the road.

####2. Final Model Architecture

The final model architecture (model.py lines 67-79) consisted of a convolution neural network with the following layers and layer sizes:
1. Cropping2D layer to resize the image
2. Convolution layer with depth 24 and 5x5 filter
3. Convolution layer with depth 36 and 5x5 filter
4. Convolution layer with depth 48 and 5x5 filter
5. Convolution layer with depth 64 and 3x3 filter
6. Convolution layer with depth 64 and 3x3 filter
7. Flatten layer
8. Dense layer with 100
9. Dense layer with 50
10. Dense layer with 10
11. Dense layer with 1


####3. Creation of the Training Set & Training Process

To capture good driving behavior, I first recorded 1 laps on track one using center lane driving. 

I then recorded the vehicle recovering from the left side and right sides of the road back to center so that the vehicle

I also record data for some place that vechile cannot stay on road like place around the brown track and near the lake.

To augment the data sat, I also flipped images and angles thinking that this would add more data for the training For example.



After the collection process, I had 20000 number of data points. I then preprocessed this data by grayscale


I finally randomly shuffled the data set and put 20% of the data into a validation set. 

I used this training data for training the model. The validation set helped determine if the model was over or under fitting. The ideal number of epochs was 3. I used an adam optimizer so that manually training the learning rate wasn't necessary.
