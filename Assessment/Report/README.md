# Report title goes here

Author: Chen Yanjun

Project Link: https://github.com/ucfnchb/casa0018/tree/main/Assessment/Projects/Final%20Project

## Introduction

Smart homes are becoming essential today, providing more convenience, better efficiency, and improved security. Inspired by these advantages, I created a voice-controlled smart curtain system to make daily life easier and more accessible using embedded AI technology. This system uses voice recognition and trained models to make smart home technology more user-friendly and tailored to individual needs.

This project involves developing a voice recognition model that can reliably respond to commands "Open curtain" and "Close curtain." The model training begins with gathering a diverse dataset through two primary methods: capturing voice recordings via phone and collecting environmental sounds to simulate real-world conditions. The finalized model is deployed on the Arduino Nano 33 BLE Sense, a compact device equipped with various sensors suited for embedded machine learning applications.  


## Research Question

How does the training of AI models impact the accuracy of voice recognition in smart home systems like voice-controlled smart curtains?


## Application Overview

Gathering data, splitting data, training the AI model, and deployment into Arduino Nano 33 BLE are all subjects of this project. The data collected from both voice command via phone and external environmental noise and unknown voice datasets are processed and augmented. Using Edge Impulse, the deep learning model is trained to find the best parameter combination for deployment to the Arduino Nano 33 BLE Sense. In this project, it performs keyword voice recognition, where a device is set up to listen for a specific command and then performs an action based on it: "open curtain" or "close curtain."

## Data

To develop the model, it is essential to have a comprehensive dataset for training. Data collection is being conducted through two ways. Firstly, voice recordings are being captured via phone, using its sensor to capture the voice data, the two commands "Open curtain" and "Close curtain." These recordings include contributions from myself and ten friends who differ in gender, age, and nationality to ensure a diverse and representative dataset. Secondly, environmental data pertinent to real-world application scenarios, such as background noise and the unknown sounds, are also being added. The Noise and Unknown dataset files  are downloaded from: https://docs.edgeimpulse.com/docs/pre-built-datasets/keyword-spotting.

After collecting the two commands "Open curtain" and "Close curtain," correctly label them and then these samples need to be cut into segments, cutting out the part where says these keywords by splitting samples. Split it up typically into one second, to accurately refine the data with minimal noise to make sure the datasets are reliable. Also, in order to balance the datasets well, similar amounts of noise, commands, and unknown data are important, so I balanced each dataset to around 2 minutes and 40 seconds to prevent potential bias. Lastly, split the training data class into 10 minutes and the testing class into 4 minutes.

![image](https://github.com/ucfnchb/casa0018/assets/146333771/04e90c2e-e147-43df-8e4e-4305ec49352a)


![image](https://github.com/ucfnchb/casa0018/assets/146333771/77c473f3-865a-4bda-a721-86ce118b07f9)


## Model

Design a model architecture, training is the process by which a model learns to produce the correct output for a given set of input. Designing impulse, I used the "Mel Frequency Cepstral Coefficients (MFCC)" signal processing block, which extracts features from audio signals using Mel Frequency Cepstral coefficients. It is great for human voice and is a way of turning raw audio, which contains a large amount of redundant information, into a simplified form. I chose MFCC rather than MFE because it is better suited for dealing with human speech. Next, Neural Network (Keras) for learning block as it learns patterns from data and can apply these to new data. Great for categorizing movement or recognizing audio.

![image](https://github.com/ucfnchb/casa0018/assets/146333771/574414f3-1a8f-4172-aa64-5a938422e062)

# Signal Processing Block

Configure the MFCC block to explore my data and examine the types of spectrograms it produces. Continue monitoring the on-device performance with different dataset parameters, including processing time and peak RAM usage. By generating features across all the data in the dataset, run the feature extraction pipeline and then visualize the dataset in 3D to see if it separates nicely or if there are problems with the dataset. The feature explorer allows me to assess the dataset quality and whether the data separates nicely before doing any machine learning. Figure 5, from the fourth experiment, shows that the unknown data and noise data are not nicely separated. In contrast, Figure 6 from the ninth experiment shows that “noise”, "Close curtain," and "Open curtain" datasets have good separation. This allows me to check whether the dataset contains incorrect items and to validate if my dataset is suitable for machine learning.

![image](https://github.com/ucfnchb/casa0018/assets/146333771/6cba337e-fe14-4f5b-a0f5-426856f919f0)


## Experiments

Train the neural network to distinguish between classes and find the optimal parameters for the highest accuracy. The parameters are tested across 10 experiments include Learning Rate, Neurons, Input Layer, Reshape Layer, Output Layer, and Dropout Rate. Advanced training settings involve auto-weighting classes, and data augmentation includes adding noise low, none or high. Additionally, I chose a preset 1D Convolutional network while keeping some default settings unchanged: Validation set size at 20%, number of training cycles at 100, time band masking at low, and no frequency band masking.

![image](https://github.com/ucfnchb/casa0018/assets/146333771/8f2ee7b6-54a9-452a-baff-672e1871588f)

To execute, under the Audio Training Options in the classifier, data augmentation involves randomly transforming data during training to allow more cycles without overfitting, which can improve accuracy; I tried to adjust the noise to None, Low, or High to compare the results. And tried the advanced training settings include the option to enable auto-weighting of classes by selecting yes or no. After conducting 10 experiments, the most accurate parameter combination was found in the 8th experiment. Moreover, after 10 rounds of training with various parameters combinations, I reviewed the test dataset, modified samples flagged as uncertain, and evaluated them on the classification page to ensure they met the expected outcomes before moving them to the training set for enhanced model performance.

![image](https://github.com/ucfnchb/casa0018/assets/146333771/d0b1352f-fe74-4f49-8343-b09cc0a17f8b)

## Deployment

The next step is to deploy the model to my device, the Arduino Nano 33 BLE Sense, using the highest accuracy dataset (8th). The Nano 33 BLE is perfect for embedded machine learning applications as it combines a tiny form factor with various environmental sensors capable of detecting color, proximity, gesture, motion, temperature, humidity, audio, and barometric pressure. Edge Impulse’s TinyML is excellent for quickly creating projects that rely on large amounts of data to detect when events are occurring. It supports keyword voice recognition, where the device is set up to listen for a specific keywords and then performs an action based on it as "open curtain" or "close curtain."


## Results and Observations

# results

The training outcomes indicate that the optimal parameter combination tested during the experimental phase resulted in an accuracy of 94.30% testing set and 92.40% training set. This represents a significant improvement from the lowest accuracy of 82.50%. Also, deploying the trained model on the Nano 33 BLE Sense demonstrated the practical application of TinyML in real-time voice recognition tasks within a smart home context.  With well-trained data exported form Edge Impulse，the Nano 33 BLE Sense performed very well. 

![image](https://github.com/ucfnchb/casa0018/assets/146333771/bd1d9cee-bfd6-468a-8b5b-a118ca5f72a4)

# Observations

Firstly, the high accuracy can be attributed to the quality of the dataset used in my training process. The ideal dataset was relevant and representative, covering enough voice recordings. The dataset was also balanced to prevent potential biases, with an even split of training samples into noise and command datasets. Additionally, the reliability was ensured through correctly labelled data that contained minimal noise. These factors collectively contributed to the marked increase in model accuracy. 
Despite the high accuracy, the system sometimes failed to recognize commands correctly in noisy environments or when spoken by individuals with accents different from those in the training set. To improve this, the more diverse dataset, which included a variety of voices and background noises, need to be added for training a robust model.
Secondly, conducting enough experiments is essential, tested dataset combinations, for example the experiments (2nd- 6th) that with unknown data are less accurate than those without it (experiments 1st , 7th, 8th 9th), it is possibly because of the unknown data are very similar to the noise data, it is hard for the model to classify as Feature Explorer showed they are highly overlapped.

![image](https://github.com/ucfnchb/casa0018/assets/146333771/1b50a666-ef83-44c3-9bcb-41026e3b0ec7)

Also, adjusting parameters such as learning rates, neuron counts, layer types, and dropout rates is critical for enhancing model accuracy. Moving forward, I plan to carry out a series of experiments with different neural network architectures to evaluate their impact on performance. Lastly, deploying the project to the Nano 33 BLE Sense via the Arduino IDE on a Windows system required up to 20 minutes, a relatively unimportant problem but has not yet been resolved.

In conclusion, while the voice-controlled smart curtain system demonstrated promising results, continuous improvements are necessary to fully realize its potential.

## Bibliography

Tate, L. (2022). How Consumers are Adapting to Voice Technology in the Smart Home. https://www.kardome.com/blog-posts/consumers-adapting-voice-technology-smart-home

## Declaration of Authorship

I, AUTHORS CHEN YANJUN, confirm that the work presented in this assessment is my own. Where information has been derived from other sources, I confirm that this has been indicated in the work.

Stella


24 APRIL 2024
