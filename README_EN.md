[[Japanese](README.md)/English] 

# TFLite-ModelMaker-EfficientDet-Colab-Hands-On
<img src="https://user-images.githubusercontent.com/37477845/121361039-e4ac9300-c96f-11eb-81f5-d8ee3c08bd16.png" width="60%"><br>

Hands-on for TensorFlow Lite Model Maker.<br>
Annotation with VoTT is performed on the local PC, and learning-inference is performed on Colaboratory.<br>
You can also use the annotated dataset without annotating it.<br><br>
This repository contains the following:<br>
* Dataset (Annotation not implemented)
* Dataset (Annotated)
* Script for Google Colaboratory(Environment setting, model training, inference result confirmation)

# Requirement
Tensorflow 2.5.0 or later

# Overview
This hands-on assumes about 1.5 hours.
1. VoTT：Annotation(30-60minutes)
1. Colaboratory：Environmental preparation
1. Colaboratory：Convert to format read by object_detector
1. Colaboratory：Model training(About 5minutes)
1. Colaboratory：Inference

# Preparations
The following is required as a preliminary preparation.
* Clone this repository to your local PC.
* [VoTT](https://github.com/microsoft/VoTT) installation.

# 1. VoTT：Annotation
Annotate using [VoTT](https://github.com/microsoft/VoTT) and output in CSV format.

<details>
<summary>VoTT project settings</summary>
	
#### Select "New Project"
![2020-09-19 (3)](https://user-images.githubusercontent.com/37477845/94047557-38407600-fe0d-11ea-8d10-041a27546e85.png)
#### Make project settings
Display name：TFLite-ModelMaker-EfficientDet-Colab-Hands-On<br>
Security token：Generate New Security Token<br>
Source connection：Press「Add Connection」<br>
![2021-06-09 (1)](https://user-images.githubusercontent.com/37477845/121363447-ec6d3700-c971-11eb-93fb-3d9dc666a4a0.png)
#### Set the connection of the source connection
Display name：TFLite-ModelMaker-EfficientDet-Colab-Hands-On-TrainData
![2021-06-09 (2)](https://user-images.githubusercontent.com/37477845/121363605-1292d700-c972-11eb-9b4f-6a6a59815e53.png)
Provider: Local file system
![2021-06-09 (3)](https://user-images.githubusercontent.com/37477845/121364024-62719e00-c972-11eb-8973-475206566d58.png)
Folder path：Specify the "01_dataset" directory of the cloned repository
![2021-06-09 (4)](https://user-images.githubusercontent.com/37477845/121364031-630a3480-c972-11eb-9fb9-0ab94f4e53b7.png)
#### Set the connection of the target connection
Target connection：Add Connection
![2021-06-09 (5)](https://user-images.githubusercontent.com/37477845/121364032-63a2cb00-c972-11eb-9694-aa31354b6177.png)
Display name：TFLite-ModelMaker-EfficientDet-Colab-Hands-On-Target<br>
Provider:Local file system<br>
Folder path：Arbitrary directory<br>
![2021-06-09 (6)](https://user-images.githubusercontent.com/37477845/121364035-643b6180-c972-11eb-85d0-af841609a1df.png)
#### Add tags and save settings
Tags：Add "Fish"<br>
Press "Save Project"
![94047577-3d9dc080-fe0d-11ea-9f4f-b5fe7727fc12](https://user-images.githubusercontent.com/37477845/94283906-98a9f180-ff8c-11ea-9e16-a546b26ba763.png)
</details>

<details>
<summary>Annotate using VoTT</summary>
	
#### Select a fish by left dragging the mouse
![2020-09-19 (13)](https://user-images.githubusercontent.com/37477845/94047578-3e365700-fe0d-11ea-86b9-2d88ef24d0c0.png)
#### Select "Fish" from TAGS
You can lock the tag you want to use by selecting the padlock mark.
![2020-09-19 (14)](https://user-images.githubusercontent.com/37477845/94047588-41314780-fe0d-11ea-9574-0cb6c77f8be5.png)
<!-- #### 12
![2020-09-19 (15)](https://user-images.githubusercontent.com/37477845/94047598-442c3800-fe0d-11ea-9285-d72713520a65.png)-->
</details>

<details>
<summary>CSV export</summary>
	
#### Export settings
Provider：Comma separated values（CSV）<br>
Asset status: Tagged assets only<br>
Press "Save Export Settings"
![2021-06-09 (8)](https://user-images.githubusercontent.com/37477845/121364839-1bd07380-c973-11eb-90ca-25e237abb6f5.png)
Click the export icon from the annotation screen to export CSV.
![2020-09-19 (14)](https://user-images.githubusercontent.com/37477845/94047588-41314780-fe0d-11ea-9574-0cb6c77f8be5.png)
</details>

# 2. Colaboratory：Environmental preparation
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Kazuhito00/TFLite-ModelMaker-EfficientDet-Colab-Hands-On/blob/main/%5BColaboratory%5DTFLite_ModelMaker_Hands_On.ipynb)<br>
Subsequent work will be performed on Google Colaboratory. <br>
Open your notebook from the [Open In Colab] link and run it in the following order.
* Install the required packages
* Import the required packages

# 3.Colaboratory：Convert to format read by object_detector
After executing "!mkdir dataset", store the image file and CSV file exported from VoTT.<br>
After storing, execute the following.<br>
If you do not want to perform the annotation hands-on, or if you want to try using the annotated data, change the following "if False:" to "if True:" and execute it.
```
if False:
    !git clone https://github.com/Kazuhito00/TFLite-ModelMaker-EfficientDet-Colab-Hands-On
    !cp -r TFLite-ModelMaker-EfficientDet-Colab-Hands-On/02_dataset\(Annotated\)/* ./dataset
```
* Read CSV
* Split Training data/validation data/Test data
* Convert to format read by object_detector

# 4. Colaboratory：Model training
Please execute in the following order.
* Import csv file with Model Maker
* Choose an object detection model archiecture
* Training
* Model evaluate
* Export to TensorFlow Lite format(Full integer quantization)
* Export to TensorFlow Lite format(Float16 quantization) 

# 5. Colaboratory：Inference
Please execute in the following order.
* Inference(Full integer quantization)
* Inference(Float16 quantization) 

# Author
Kazuhito Takahashi(https://twitter.com/KzhtTkhs)
 
# License 
TFLite-ModelMaker-EfficientDet-Colab-Hands-On is under [MIT license](https://en.wikipedia.org/wiki/MIT_License).
