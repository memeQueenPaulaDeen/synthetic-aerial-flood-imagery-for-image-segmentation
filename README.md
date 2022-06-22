# synthetic-aerial-flood-imagery-for-image-segmentation

## Overview

This dataset contains 40,000 computer-generated RBG image and mask pairs of hypothetical floods in 100 areas around the globe. The dataset was generated automatically using the Unity flood simulator.

The Unity flood simulator uses the MapBox unity API to query real-world aerial and satellite imagery from any location worldwide. Additionally, MapBox provides elevation data that allows imagery to take the shape of the corresponding terrain. Realistic floods are procedurally added by placing simulated water objects in the simulated landscape.

## Data

The data can be found and downloaded from 

The data is organized into three folders x, y, and y_clean. For most applications using x and y_clean is recommended. The folder x contains 40,000 RGB training images. The images were collected over 100 locations, with 400 images being collected per geographic location. Each image follows the naming convention city_number. For example, the 20th image collected over Tulsa would be labeled Tulsa_20.png. The folders y and y_clean contain RGB segmentation masks produced by Unity. The masks share the same naming convention so that a training pair could be loaded at generatedData1/x/Tulsa_20.png and generatedData1/y/Tulsa_20.png. The class mappings can be seen in the table below.


![image](https://user-images.githubusercontent.com/24756984/175069414-ddde9371-fa66-4eb1-bb6a-2f3d36b786f0.png)


## Additional Notes

In some cases, the masks produced by unity blend RGB values near the borders of different classifications. The y_clean folder provides masks where a post-process script assigns blended values to the nearest valid neighbor. 

Scripts to load and clean the data can be found,
additionally example Keras loaders can be found 



It is important to note that images taken over the same city will have overlapping portions. [Displacement between images is around 137 pixels but depends on terrain.]  It is recommended that data is split by city during training. For example, place Tulsa and Tokyo training, Akita in testing, do not place the first 300 images of each in training and the last 100 in testing. This will avoid contamination of test and validation sets.

Code used to train DeepLabV3+ and VGG models can be found at the related repository 
