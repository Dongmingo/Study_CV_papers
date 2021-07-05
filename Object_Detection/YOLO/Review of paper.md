# You Only Look Once(YOLO) : Unified, Real-Time Object Detection

## Purpose of Paper
 <p>Previous Object Detection models takes quite long time compare to human's recognition system</p>
 <p align ="center"><img src="https://user-images.githubusercontent.com/61967107/124428360-8ffe0b80-dda7-11eb-8e3a-6cc553611177.gif" width="50%"></p>
 
## Problems
- The Models for object detection problem not only classifies, but also need to determine the location of object bounding box : for previous models(e.g.DPM or R-CNN), it was seperated by post-processing. Thus it was time-consuming and hard to optimize</p>
- Background error

## Key Structures
- Single Regression Model : Solution for Problems
<p align = "center"><img src="https://user-images.githubusercontent.com/61967107/124429254-993ba800-dda8-11eb-8646-9aba914ff264.png" width="50%"></p>
<p> 5 features in tensor indicates (x,y,w,h,confidence)</p>

- x,y indicates the relative position of bounding box center in grid cell [0,1]
- w,h indicates the relative size of bounding box to total image [0,1]
- confidence scores accuraties of prediction bounding box :
<p align = "center"><img src="https://user-images.githubusercontent.com/61967107/124430445-23d0d700-ddaa-11eb-87e7-1f768b052c4e.png" width="30%"></p>

## Network Architetcture
<p align ="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbcD1Ts%2FbtqKBPsHQGp%2FKu8dlxjrsyWFbcjv6XMnqk%2Fimg.png"></p>
- Uses 24 conv layers. Fast YOLO uses filters and less number of  9 conv layers

### Training
- Pre-train 20 conv layers with ImageNet dataset
- Add 4 conv layers and 2 fully connected layers
- Use Leaky ReLU for every activation function but for last layer, use linear activation function 

### Loss Function
<p align ="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcDocKb%2FbtqKwSxuIQK%2FAO4jemksYpCGktMP2pFoWK%2Fimg.png" width="60%"></p>
- Mediate weights of localization loss and classification loss(λ_coord=5, λ_noobj=0.5) : To fix model unbalance caused by lack of objects
- Square root to width, heigth : To fix loss function changes sensitive to small bounding box

## Limitations of YOLO
- One Grid cell detects only one objects : hard to seperate several small adjacent objects
