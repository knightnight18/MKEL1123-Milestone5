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

![Picture1](https://user-images.githubusercontent.com/104575093/178266313-83d18dc1-1924-4c82-b6fd-aba87c2669ae.png)

Done for the pack installed part. Next we will upload the pack onto the board. To do so, we save the configuration we have done on .ioc tab then a window pop out will show to generate the code. Click "Yes". This is the important part, make sure "Middleware" folder is generated because this is where all your impulse and required libraries are. Rename the main.c file under Core/Src to main.cpp as C++ language is preferred.  

![Picture2](https://user-images.githubusercontent.com/104575093/178266529-139918b9-fd3d-472f-82f5-7ce42830b22e.png)

Edit main.cpp file by copy and paste this code from here:
[main.cpp](https://github.com/knightnight18/MKEL1123-Milestone5-Pneumonia-Detection-Device-Using-CMSIS-Neural-Network-on-STM-32/blob/50da393551f789dbc152ae24ccc1fe2984f5527d/main.cpp) 

![Picture3](https://user-images.githubusercontent.com/104575093/178267073-cddb2a0e-7c09-4550-a36a-caaffe57c498.png)

To upload the code into the board, click on the play button icon. Leave all the settings to default and make sure you already connected your board prior clicking the play button icon. This message will show if you have successfully uploaded your code onto the board.

![Picture4](https://user-images.githubusercontent.com/104575093/178267348-717950c0-1c8c-4067-9bdb-24ef31139dba.png)

To display the output, open puTTY. Then choose "Serial" as the connection type. Set the speed to "115200". For the serial line, to know which COMx to use, open "Device Manager" to check. Below is the setting we use.

![Picture5](https://user-images.githubusercontent.com/104575093/178267521-6e77d613-bed5-4a69-98b3-54b3e1668ef5.png)
![Picture6](https://user-images.githubusercontent.com/104575093/178269246-0a85fc89-81e0-4bbd-8541-0cc391851cdb.png)

The result will be shown on puTTy interface as shown below.

![Picture7](https://user-images.githubusercontent.com/104575093/178269592-963df650-d694-4d8b-aad7-b61926319afc.png)

To change the dataset, we can copy the raw features of each image. To do so, go back to Edge Impulse, at the left side, choose "Live Classification" and under "Classify existing test sample" choose which image you want to have its raw features. Then click the "Load sample" and wait for classification results to come out. Then, copy the raw features and paste it into this line of code in the main.cpp file.

![Picture8](https://user-images.githubusercontent.com/104575093/178269769-1e28961e-4f5e-4898-ac14-1284122b4811.png)

![Picture9](https://user-images.githubusercontent.com/104575093/178269865-15c1a518-a7b8-424f-8c7a-87e2c900bb63.png)
