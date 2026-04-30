# Social Distancing Detector: A Pose Estimation Project
**Developed by:** Punith Akash Balachandran
**Academic Context:** UMBC Master's in Data Science

## The Vision
In this lab, I implemented an AI safety assistant designed to understand human proximity in real-time. Rather than relying on simple bounding boxes, this project utilizes human pose estimation to identify the center of gravity for each person and calculate whether they are maintaining a safe distance.

## Implementation Logic
The system follows a specific geometric workflow to monitor distancing:

* [cite_start]**Finding Joints:** Using the poseNet model, the AI identifies 18 human joint keypoints, including shoulders, elbows, and knees. [cite: 5, 21]
* [cite_start]**Locating the Hips:** To establish a consistent center for each person, the script extracts Keypoint 11 (Left Hip) and Keypoint 12 (Right Hip). [cite: 24]
* [cite_start]**The Midpoint Logic:** The code calculates the midpoint between these two hip coordinates to represent the person's location in the 2D frame. [cite: 24, 25]
* [cite_start]**Measuring Distance:** I implemented a Euclidean distance calculation to measure the straight-line pixel distance between every detected person. [cite: 17, 25]
* [cite_start]**The Alert System:** If the calculated distance drops below 150 pixels, the HUD triggers a visual warning. [cite: 8, 26]

## Visual Feedback
* **All Clear:** When individuals are at a safe distance, the indicators remain green.
* **Violation:** When people move closer than the threshold, the system draws a red connecting line and flags a "VIOLATION" on the HUD.

## Setup and Running
[cite_start]This project was developed for the NVIDIA Jetson platform using the jetson-inference library. [cite: 10, 11]


## Results and Testing
I tested the system under various conditions to ensure the Euclidean distance logic was accurate.

### Social Distancing Violations
Below are cases where the system correctly identified that people were closer than the 300px threshold:
![Violation 1](violation1.jpeg)
![Violation 2](violation2.jpeg)
![Violation 3](violation3.jpeg)

### Safe Distancing (All Clear)
The system correctly remains in "All Clear" mode when proper distance is maintained:
![Clear Case](clear.jpeg)


To launch the detector:
```bash
python3 pose_distance.py /dev/video0


