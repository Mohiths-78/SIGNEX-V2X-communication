# Collaborative V2X Perception for Intelligent and Safer Autonomous Vehicles

> An AI-enabled collaborative perception system that allows connected vehicles to share real-time environmental information through V2X communication to improve situational awareness and road safety.

## Overview

Autonomous vehicles typically depend on their own cameras and sensors to understand their surroundings. However, occlusion, blind spots, limited field of view, and poor visibility can prevent a vehicle from detecting important objects.

This project proposes a **Collaborative V2X Perception System** in which multiple connected vehicles and roadside infrastructure share detected-object information. The system combines these observations to create a more complete and reliable perception of the road environment.

For example, if a pedestrian is hidden behind a truck and cannot be detected by Vehicle A, another nearby Vehicle B can detect the pedestrian and share the information with Vehicle A through V2X communication. Vehicle A can then use this information to generate a safety warning.

## Objectives

- Enable collaborative perception between connected vehicles.
- Detect vehicles, pedestrians, cyclists, and road obstacles.
- Reduce the impact of occlusion and sensor blind spots.
- Exchange perception information using V2X communication.
- Fuse observations from multiple vehicles.
- Prevent duplicate objects from being counted multiple times.
- Maintain safety during communication delays or temporary disconnections.
- Provide real-time safety and collision-risk warnings.

## System Workflow

```text
Vehicles / Roadside Units
          |
          v
   Cameras & Sensors
          |
          v
    Object Detection
          |
          v
   V2X Information Sharing
          |
          v
 Coordinate Transformation
          |
          v
  Collaborative Perception
          |
          v
 Object Fusion & Tracking
          |
          v
 Duplicate Object Removal
          |
          v
 Shared Perception View
          |
          v
 Safety / Collision Warning
```

## Key Features

- Multi-vehicle collaborative perception
- V2V and V2I communication
- Real-time object detection
- Occlusion-aware perception
- Multi-source object fusion
- Duplicate object handling
- Object tracking
- Safety and collision warnings
- Local perception fallback
- Simulation-based testing

## Technology Stack

| Technology | Role |
|---|---|
| Python | Core programming |
| CARLA | Autonomous driving simulation |
| OpenCDA | Cooperative driving and V2X |
| OpenCOOD | Collaborative perception |
| YOLO | Object detection |
| PyTorch | Deep learning |
| OpenCV | Computer vision |
| ROS 2 | Communication middleware |
| FastAPI | Backend API |
| React | Web dashboard |

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/<your-username>/<your-repository>.git
cd <your-repository>
```

### 2. Create a Virtual Environment

```bash
python -m venv venv
```

**Windows:**
```bash
venv\Scripts\activate
```

**Linux/macOS:**
```bash
source venv/bin/activate
```

### 3. Install Python Dependencies

```bash
pip install -r requirements.txt
```

If `requirements.txt` has not been created yet:

```bash
pip install numpy opencv-python torch torchvision ultralytics fastapi uvicorn
```

### 4. Install CARLA

Install a compatible CARLA release for your operating system and verify that the simulator starts successfully.

### 5. Install OpenCDA, OpenCOOD and ROS 2

Install the required versions according to the project configuration and operating system.

## Usage

### 1. Start CARLA

Launch the CARLA simulator.

On Linux:

```bash
./CarlaUE4.sh
```

On Windows, launch the CARLA executable from its installation directory.

### 2. Start Object Detection

```bash
python perception/detection.py
```

The perception module detects vehicles, pedestrians, cyclists, and other obstacles.

### 3. Start V2X Communication

```bash
python communication/v2x.py
```

Detected-object information is exchanged between simulated vehicles.

### 4. Run Collaborative Fusion

```bash
python perception/fusion.py
```

The fusion module:

1. Receives local and remote detections.
2. Aligns object coordinates.
3. Matches objects detected by multiple vehicles.
4. Removes duplicate detections.
5. Generates a shared perception view.

### 5. Run the Safety Module

```bash
python safety/warning.py
```

The system analyzes the shared perception and generates warnings for potentially dangerous situations.

> **Note:** Update the commands above according to the final filenames and implementation in the repository.

## Example Scenario: Occluded Pedestrian

Consider an intersection where a truck blocks Vehicle A's view of a pedestrian.

```text
             Vehicle B
                 |
                 v
            Pedestrian
                 |
          +-------------+
          |    Truck    |
          +-------------+
                 |
                 v
             Vehicle A
```

1. Vehicle B detects the pedestrian.
2. Vehicle B generates object information.
3. The information is transmitted through V2X.
4. Vehicle A receives the information.
5. The system matches and fuses the detection.
6. Vehicle A becomes aware of the hidden pedestrian.
7. A safety warning is generated.

## Handling Technical Challenges

### Duplicate Objects

The same object may be detected by several vehicles. Object IDs, position matching, timestamps, and tracking are used to identify and merge duplicate detections.

### V2X Latency or Packet Loss

If V2X communication becomes unreliable, the vehicle continues using local sensor perception. Safety-critical messages can also be prioritized to maintain important information exchange.

### Occlusion

Information from another vehicle can reveal objects that are hidden from the local vehicle's sensors.

## Project Structure

```text
Collaborative-V2X-Perception/
|
├── perception/
│   ├── detection.py
│   ├── tracking.py
│   └── fusion.py
|
├── communication/
│   ├── v2x.py
│   ├── sender.py
│   └── receiver.py
|
├── simulation/
│   ├── carla_client.py
│   ├── vehicle_manager.py
│   └── scenario.py
|
├── safety/
│   ├── collision_detection.py
│   └── warning.py
|
├── dashboard/
│   ├── frontend/
│   └── backend/
|
├── models/
│   └── README.md
|
├── data/
│   └── README.md
|
├── tests/
│   ├── test_detection.py
│   ├── test_fusion.py
│   └── test_communication.py
|
├── requirements.txt
├── README.md
└── LICENSE
```

## Dependencies

### Software

- Python 3.x
- CARLA
- OpenCDA
- OpenCOOD
- ROS 2
- Git

### Python Packages

```text
numpy
opencv-python
torch
torchvision
ultralytics
fastapi
uvicorn
```

Install dependencies with:

```bash
pip install -r requirements.txt
```

## Dataset

The project can use collaborative perception datasets such as:

- **OPV2V**
- **V2XSet**

These datasets can support the development and evaluation of multi-vehicle perception and object-fusion approaches.

## Performance Evaluation

The system can be evaluated using:

- Object detection accuracy
- Precision and recall
- Detection latency
- V2X communication latency
- Packet-loss tolerance
- Duplicate detection rate
- Collision-warning accuracy
- Occluded-object detection performance

## Applications

- Autonomous vehicles
- Smart intersections
- Highway safety
- Pedestrian protection
- Blind-spot awareness
- Emergency vehicle coordination
- Connected transportation
- Intelligent Transportation Systems
- Smart-city infrastructure

## Future Scope

- 5G / C-V2X communication
- LiDAR-based collaborative perception
- Edge computing
- Advanced collision prediction
- Traffic signal coordination
- Emergency vehicle prioritization
- Large-scale multi-vehicle simulation
- Real-world vehicle and roadside-unit deployment

## Contribution Guidelines

Contributions are welcome.

### 1. Fork the Repository

Create your own fork of the project.

### 2. Create a Feature Branch

```bash
git checkout -b feature/your-feature
```

### 3. Make Your Changes

Implement your feature or fix while maintaining the existing project structure.

### 4. Test Your Changes

```bash
pytest
```

Ensure that existing functionality is not affected.

### 5. Commit Your Changes

```bash
git add .
git commit -m "Add collaborative perception feature"
```

### 6. Push the Branch

```bash
git push origin feature/your-feature
```

### 7. Create a Pull Request

Describe:

- What was changed
- Why the change was required
- How it was tested
- Any limitations or dependencies

## Acknowledgements

This project builds upon open-source research and simulation technologies including:

- CARLA
- OpenCDA
- OpenCOOD
- OPV2V
- YOLO
- PyTorch
- OpenCV
- ROS 2

## License

This project is intended for academic, research, and educational purposes. Add an appropriate open-source license, such as MIT, before public distribution.

## Project Vision

> **"See beyond your sensors through collaborative intelligence."**

The goal is to demonstrate how **V2X communication + AI-based perception + multi-vehicle collaboration** can create a safer and more aware transportation environment.
