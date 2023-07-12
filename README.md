
<div align="center">
  <h1>Gesture Volume Control Using OpenCV and MediaPipe</h1>
  <img alt="output" src="images/output.gif" />
 </div>

> This Project uses OpenCV and MediaPipe to Control system volume 

## 💾 REQUIREMENTS
+ opencv-python
+ mediapipe
+ comtypes
+ numpy
+ pycaw

```bash
pip install -r requirements.txt
```
***
### MEDIAPIPE
<div align="center">
  <img alt="mediapipeLogo" src="images/mediapipe.png" />
</div>

> MediaPipe offers open-source cross-platform, customizable ML solutions for live and streaming media.

#### Hand Landmark Model
After detecting the palm over the whole image, our subsequent hand landmark model uses regression, or direct coordinate prediction, to accomplish precise keypoint localization of 21 3D hand-knuckle coordinates inside the detected hand regions. The model acquires a reliable internal hand posture representation and is unaffected by self-occlusions or partially visible hands.

As shown below, we manually annotated around 30K real-world photographs with 21 3D coordinates in order to gather ground truth data (we take the Z-value from the image depth map, if it exists, per the associated point). We additionally render a high-quality synthetic hand model over a variety of backgrounds and map it to the associated 3D coordinates in order to better cover the range of possible hand poses and provide additional supervision on the nature of hand geometry.<br>

#### Solution APIs
##### Configuration Options
> Naming style and availability may differ slightly across platforms/languages.

+ <b>STATIC_IMAGE_MODE</b><br>
If false is selected, the program processes the supplied pictures like a video stream. In the first input photographs, it will attempt to identify hands; if successful, it will then further localize the hand landmarks. Following the detection of all max_num_hands hands and the localization of the associated hand landmarks, it simply monitors those landmarks in successive photos without triggering another detection until it loses track of any of the hands. When processing video frames, this lowers latency. The ideal way to handle a batch of static, potentially unrelated photographs is to set the value of hand detection to true, which runs on every incoming image. False by default.

+ <b>MAX_NUM_HANDS</b><br>
Maximum hands to be detected. By default, 2.

+ <b>MODEL_COMPLEXITY</b><br>
Complexity of the hand landmark model: 0 or 1. Landmark accuracy as well as inference latency generally go up with the model complexity. Default to 1.

+ <b>MIN_DETECTION_CONFIDENCE</b><br>
Minimum confidence value ([0.0, 1.0]) from the hand detection model for the detection to be considered successful. Default to 0.5.

+ <b>MIN_TRACKING_CONFIDENCE:</b><br>
The hand landmarks must have a minimum confidence value ([0.0, 1.0]) from the landmark-tracking model to be regarded successfully tracked; otherwise, hand detection will be activated automatically on the following input image. By increasing it, the solution's robustness can be improved at the cost of an increase in latency. If static_image_mode is set to true, hand detection is ignored and executed on each image. 0.5 is the default.

<br>

