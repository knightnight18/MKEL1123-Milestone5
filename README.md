# Pneumonia Detection Device Using CMSIS Neural Network on STM-32
## MKEL1123-Milestone 5

## Software and Hardware
- Edge Impulse
- STM-32
- USB-A to Mini-A cable

## Procedure
Step-by-step can be categorised into 3 sections:
1. Kaggle
2. Edge Impulse
3. STM32

### ***Kaggle***
- Data used is acquired from [Kaggle](https://www.kaggle.com/datasets/paultimothymooney/chest-xray-pneumonia) which consist of pneumonia and normal lungs that have been categorized into a test and train set.

### ***[Edge Impulse](https://studio.edgeimpulse.com)***
#### 1) Data Acquisition
- From Kaggle, 1003 samples are uploaded into the test and train sets for our impulse, these samples are divided into 81% train and 19% test.

#### 2) Impulse Design
##### *Create Impulse*
![Create Impulse](https://user-images.githubusercontent.com/104577236/178251758-65769cee-b092-4b45-bf51-6d16b65598de.jpg)

Impulse is created by taking raw data, using signal processing to extract features and using a learning block to classify the data. In our project, the image data from kaggle were uploaded into two sets of trains and tests which are categorized into pneumonia and normal lungs. Features from each image are extracted and Keras Classification is used as the learning block.

##### *Images*
![images](https://user-images.githubusercontent.com/104577236/178254508-a50ce398-4f0c-41cc-9347-935da3b6bd97.jpg)

In the image tab, we will generate features for all of the test and train sets that were uploaded earlier. Next, we can extract any individual images that we desired to extract its features for our testing in STM32 

##### *NN Classifier (Classification Keras)*
![Classifier](https://user-images.githubusercontent.com/104577236/178254881-ac66665e-a0f1-415f-96fc-e80229e35f75.jpg)

In this tab, we will specify the training setting. We set ours as in the image above.

##### *Model Testing*
![Model Testing](https://user-images.githubusercontent.com/104577236/178255790-cceb8889-4442-4bb9-93e5-0e19fa18b38b.jpg)

Test the impulse model with the test set from the data acquisition tab.

##### *Deployment*
![Deploy](https://user-images.githubusercontent.com/104577236/178257449-06f799df-e55e-4dc4-bd55-c2c0ed4bb973.jpg)

Model can be deployed to STM32 using the Cube.MX CMSIS-PACK library and optimized for int8 to use less memory but lower accuracy depending on model built.

![Deploy2](https://user-images.githubusercontent.com/104577236/178257360-d664e34d-021e-4e5b-ae3f-9339f2c9819b.jpg)

### ***STM-32***
Open the STM32Cube IDE and create a new STM32 project to deploy the pack onto an STM32 board. A new window will appear. Go to the top side and look for the NUCLEO-F446RE Board, as that is the board we are utilizing. It is dependent on the board you are using at this point.

![Deploy stm](https://user-images.githubusercontent.com/104577236/178259665-f3d99944-964b-4e79-bd09-d29ed76296a6.jpg)

Enter the project name, and choose "C++" as the targeted language. Then click on "Finish". If there is a window pop out asking whether to "Initialize all peripherals with their default mode" click "Yes”. Make sure you have <project_name>. ioc tab open after clicking "Finish" button.

![Setup STM](https://user-images.githubusercontent.com/104577236/178261005-d2281aa0-fe6e-4be5-bf9a-e699ae8a3eee.jpg)

On the .ioc tab, go to "Pinout & Configuration" > "Computing" > "CRC". Click on "CRC" to enable it.

![pinout](https://user-images.githubusercontent.com/104577236/178261510-54be1557-0819-4a8c-a516-5dc0c8824beb.jpg)

To upload the pack downloaded before from Edge Impulse, go to "Help" > "Manage Embedded Software Packages" > "From Local...". Then, search for the downloaded pack from your local computer and select it. A window pop out for license agreement will show. Read the "License and Agreement" and click "Yes" if you agree with it. The pack will be installed after you click "Yes".

![embedded software](https://user-images.githubusercontent.com/104577236/178262606-ff91e0f6-3ac5-4497-b010-d08a6c42e05c.jpg)

After having the pack installed. Go back to .ioc tab and go to "Pinout & Configuration" > "Software packs" > "Select components". Select the pack you previously installed and under selection, click on the checkbox to use the pack. Then go back to .ioc tab, go to "Pinout & Configuration" > "Software Packs". Select the pack you installed, and under "Mode" check the checkbox.

![pack mode](https://user-images.githubusercontent.com/104577236/178263711-8a053c22-d653-4c6b-80c6-286b5e40d822.jpg)




