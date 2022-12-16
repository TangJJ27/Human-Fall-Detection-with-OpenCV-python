# Human-Fall-Detection-with-OpenCV-python

## Introduction
This project is one of the parts in my uni's integrated design project "Smart Kitchen". Fall Detection in Smart Kitchen aimed to detect human falls occur in the kitchen especially for the elders. Kitchen is a place which is wet and slippery. Nowadays, the elders are often left at home alone while other adults went to study or work. There is a risk if the elders fell and no one awares, this may cause them to miss the emergency rescue time and fatal fall happens. The fall detection system can also be applied in other situation other thann kitchen.

## Methodology
OpenCV backgroundSubtractorMOG2 was used to extract the background image. The capturing image is compared with background image to obtain moving contours. The largest contour entering the scene is assumed to be the person entering the scene. The largest contour will be bounded with a rectangle using boundRect function in OpenCV. Activity status of the person can then been analysed with the bounded rectangle. 

To determine fall, the following steps is taken:
1) Standard deviation of the coordinates of the rectangle is obtained.
    - If the standard deviation of coordinates < 1, the person is not moving/ stationery.
    - If the standard deviation of coordinates > 1, the person is moving in the scene. 
2) Width and length of the rectangle is anaylzed.
    - If width < length, the person is in an upright position.
    - If length > width, the person is in a horizontal position.
    
    ![Width Length Detection](https://user-images.githubusercontent.com/113175359/208013926-6be0df8a-7046-4828-a08b-230f2ae02abd.png)
    
3) Status of the person:
    - Moving and upright ==> Normal/ Moving
    - Stationary and upright ==> Normal/ Standing
    - Moving and horizontal ==> Falling/ Warning
    - Stationary and horizontal ==> Falled

## Functionality 
The program can be run on a Raspberry Pi with a camera module connected to it. In my project, I used Raspberry Pi 4 model B+ with 1GB ram and a Pi camera. The program is also connected to an IoT platform (not included in the uploaded code). When fall is detected, the IoT platform will be triggered to send alert email. A screenshot will be taken when fall is detected.

## Shortcomings
- The background scene must not have other moving objects.
- Per person detection only.
- Easily affected by minor moving of background object when stationary. 
- Low frame rate (The frame rate will be at around 8-20 fps while showing frame and running Anydesk)

## Notes
- The code for connecting IoT has been removed due to different way of connecting for different IoT platform.

## References 
- https://github.com/caox5/Real-time-embedded-project
