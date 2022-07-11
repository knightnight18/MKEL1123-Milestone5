# Pneumonia Detection Device Using CMSIS Neural Network on STM-32
## MKEL1123-Milestone 5

## Software and Hardware
- Edge Impulse
- STM-32
- USB-A to Mini-A cable

## Procedure
1. Kaggle
2. Edge Impulse
3. STM32

### Kaggle
- Data used is acquired from [Kaggle](https://www.kaggle.com/datasets/paultimothymooney/chest-xray-pneumonia) which consist of pneumonia and normal lungs that have been categorized into a test and train set.

### Edge Impulse
#### 1) Data Acquisition
- From Kaggle, 1003 samples are uploaded into the test and train sets for our impulse, these samples are divided into 81% train and 19% test.

#### 2) Impulse Design
##### Create Impulse
![Create Impulse](https://user-images.githubusercontent.com/104577236/178251758-65769cee-b092-4b45-bf51-6d16b65598de.jpg)
Impulse is created by taking raw data, using signal processing to extract features and using a learning block to classify the data. In our project, the image data from kaggle were uploaded into two sets of trains and tests which are categorized into pneumonia and normal lungs. Features from each image are extracted and Keras Classification is used as the learning block.


