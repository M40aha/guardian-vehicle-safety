🚗 GUARDIAN – Vehicle Safety Perception System

GUARDIAN is a real-time, safety-first perception system designed for vehicles and Advanced Driver Assistance Systems (ADAS).
The system focuses on detecting dangerous situations on the road and immediately overriding normal driving behavior when an obstacle appears in the vehicle’s path.

Core philosophy:
If something is physically in the driving lane, safety decisions must override everything else.

🧠 Motivation

In many vision-based driving systems:

An object may be detected visually (bounding box appears),

but the decision system remains in NORMAL mode,

especially under:

Night driving conditions

Low-confidence detections

Misclassification (e.g., pedestrian detected as a car)

This disconnect between perception and decision-making can lead to dangerous outcomes.

GUARDIAN was built to eliminate this gap.

🎯 Project Objective

The objective of GUARDIAN is to design a robust vehicle safety perception framework that:

Reacts immediately to sudden obstacles

Prioritizes collision risk over object class labels

Guarantees that no obstacle can appear in the driving lane while the system remains in NORMAL mode`

✨ Key Features
🚧 Lane-Aware Safety (ROI-Based)

Defines a Region of Interest (ROI) representing the vehicle’s driving lane

Only objects that physically occupy this region are considered hazardous

📐 Bottom-Center Geometry (Critical Design Choice)

Instead of using the bounding-box center, GUARDIAN uses the bottom-center point:

Pedestrian feet location

Vehicle tire-to-road contact point

This provides a physically meaningful indicator of whether an object is actually on the road and blocking the vehicle’s path.

🚨 Safety Override Mechanism (Core Innovation)

GUARDIAN enforces a hard safety override:

If any obstacle enters the lane ROI → CRITICAL mode

The override is applied:

During fast hazard scanning

After inference using the same detection results that are visualized

This guarantees that visual detection always leads to a correct safety decision.

🚗 Hazard-Agnostic Design

Safety decisions are not limited to pedestrians.

The system reacts to any obstacle that may cause a collision:

Person

Bicycle

Car

Motorbike

Bus

Truck

Even if a pedestrian is misclassified as a vehicle, the safety response is still triggered.

⚡ Efficient Two-Stage Inference

To balance speed and accuracy, GUARDIAN uses:

Fast Hazard Scan (YOLOv8n)

Lightweight and fast

Immediate reaction to obstacles

Normal Inference (YOLOv8s)

Higher detection accuracy

Post-inference safety override guarantees reliability

🔄 Decision Pipeline
Input Frame
   ↓
Fast Hazard Scan
   ↓
Obstacle inside lane ROI?
   ├── YES → CRITICAL MODE (Immediate Override)
   └── NO
        ↓
Normal Inference
        ↓
Post-Inference Safety Override
        ├── Obstacle in ROI → CRITICAL MODE
        └── Else → NORMAL / ADAPTIVE MODE

Guarantee:
An obstacle can never appear in the driving lane while the system remains in NORMAL mode.

🖼 Visual Output

Each processed frame includes:

Detected object bounding boxes

Lane ROI overlay

On-screen dashboard showing:

STATUS: NORMAL / CRITICAL / ADAPTIVE

Latency per frame

Example:

STATUS: CRITICAL: OBSTACLE IN PATH (OVERRIDE)
LATENCY: 0.0138s
⚙️ System Requirements

Python 3.8+

OpenCV

PyTorch

Ultralytics YOLOv8

📦 Installation
pip install ultralytics torch opencv-python numpy
▶️ How to Run

Place your dashcam video in the project directory

Update the input file name in the code:

INPUT_FILE = "T2.MP4"

Run the system:

python guardian.py

The processed output video will be generated automatically.

📊 Why GUARDIAN Is Different

Traditional perception systems:

Rely on object class labels

Use bounding-box center points

Allow detection without safety action

GUARDIAN:

Uses geometry and physical lane occupancy

Relies on bottom-center contact points

Guarantees safety override when risk is detected

Treats any lane obstacle as a critical event

🚀 Future Improvements

Time-To-Collision (TTC) estimation

Optical flow for sudden stopping detection

Depth estimation for accurate distance measurement

Multi-lane awareness

Integration with braking or alert systems

👩‍💻 Author

Developed as an advanced vehicle safety perception project
focused on real-world ADAS and autonomous driving scenarios.

⚠️ Disclaimer

This project is intended for research and educational purposes only.
It is not a certified autonomous driving or collision avoidance system.

⭐ If you find this project useful, feel free to star the repository!
