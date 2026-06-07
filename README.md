# Computer Vision Edge, Shape Detection, and Active Contours Pipeline

A high-performance, native C++ desktop application engineered using the Qt framework to implement, benchmark, and visualize advanced low-level computer vision algorithms from mathematical primitives. This project features a completely custom 5-step Canny Edge Detection engine, parameterized Hough Transform modules for geometric primitive extraction (Lines, Circles, and Ellipses), and an iterative energy-minimizing Active Contour (Snakes) spline framework for deformable segmentation and object boundary tracking.

---

## Technical Pipeline Architecture

The application isolates intensive matrix operations and mathematical optimization loops from the Qt graphical rendering thread, maintaining smooth visual feedback during multi-parameter space iterations.

```text
+-------------------------------------------------------------------------+
|                                QT GUI LAYER                             |
|          (Dynamic Parameter Sliders, Canvas Renderers, Iteration Logs)  |
+-------------------------------------------------------------------------+
                                    |
                                    v
+-------------------------------------------------------------------------+
|                     ALGORITHMIC CORE PIPELINE (C++)                     |
|  [Canny Engine]  -->  [Hough Parametric Spaces]  -->  [Active Contours] |
+-------------------------------------------------------------------------+
                                    |
                                    v
+-------------------------------------------------------------------------+
|                       MATHEMATICAL OPTIMIZATION                         |
|    (Accumulator Arrays, Dynamic Energy Splines, Distance Transforms)    |
+-------------------------------------------------------------------------+

```

###  Core Algorithmic Capabilities

* **5-Step Canny Edge Detection Subsystem:** A rigorous implementation of edge thinning and tracking from first principles:
* *Gaussian Noise Attenuation:* 2D convolution masking to remove high-frequency noise.
* *Sobel Gradient Vectorization:* Computes local directional spatial derivatives ($I_x, I_y$), magnitude, and quantized orientation angles.
* *Non-Maximum Suppression:* Edge thinning by isolating local maxima along gradient directions.
* *Hysteresis Thresholding:* Dual-thresholding arrays to isolate strong, weak, and non-edge pixels.
* *Edge Tracking:* Recursive topological analysis to preserve weak edges physically connected to valid structures.


* **Parameterized Hough Transform Engines:** Maps spatial edge tokens into multi-dimensional accumulator spaces to isolate geometric shapes despite partial occlusions:
* *Hough Line Detector:* Leverages the normal parameterization ($\rho = x\cos\theta + y\sin\theta$) to vote on linear structures.
* *Hough Circle Detector:* Maps pixels to a 3-dimensional Hough space $(x, y, r)$ using gradient direction optimization to restrict vote allocation vectors.
* *Hough Ellipse Detector:* Solves multi-dimensional constraints to segment complex elliptical orientations from binary edge inputs.


* **Deformable Active Contours (Snakes):** Implements an iterative optimization spline that deforms over temporal steps to capture object boundaries by minimizing a comprehensive Lagrangian energy functional:

$$E_{\text{total}} = \int \left( \alpha E_{\text{continuity}} + \beta E_{\text{curvature}} + \gamma E_{\text{image}} \right) ds$$



The framework balances internal elastic forces (continuity and smoothness) against localized image external forces (gradients and edge distance maps) to snap precisely onto irregular silhouettes.

---

## Application Output Gallery

### 1. Hough Transform: Multi-Shape Detection (Lines & Circles)

Simultaneous detection and parametric overlay of linear and circular primitives within a unified scene graph.

<img width="1502" height="1038" alt="image" src="https://github.com/user-attachments/assets/85c3eca5-1477-42ed-8d34-1e1068616824" />


### 2. Hough Transform: Circular Primitive Extraction

Robust isolation of circular structures leveraging optimized gradient-directed accumulator arrays.

<img width="1502" height="913" alt="image" src="https://github.com/user-attachments/assets/7752661c-e621-4554-86a9-8f98df949b91" />

### 3. Hough Transform: Elliptical Geometry Extraction

Segmenting elliptical silhouettes by computing localized spatial constraints in parameter space.

<img width="1502" height="1038" alt="image" src="https://github.com/user-attachments/assets/2e21b31b-3776-41a5-ba68-5f0c87c65e33" />

### 4. Active Contours (Snakes) Boundary Tracking

Visualizing the step-by-step deformation loop as the initialized spline minimizes its energy fields to snap onto target contours.

<img width="1502" height="913" alt="image" src="https://github.com/user-attachments/assets/6058c04a-729f-40ea-a121-1434eef76928" />

<img width="1502" height="913" alt="image" src="https://github.com/user-attachments/assets/02eb24a0-ba00-4cd3-8f5d-b07c26142654" />

---

## Key Engineering Standards Applied

* **First-Principles Algorithm Synthesis:** Core analytical engines (Canny, Hough spaces, Spline optimization) are engineered natively without relying on high-level opencv function wrappers, preserving `cv::Mat` strictly as an efficient pixel storage matrix.
* **Accumulator Array Optimization:** Memory footprints for high-dimensional Hough spaces are structurally managed to ensure low allocation latencies and highly localized cache-line search passes.
* **Numerical Spline Stability:** The Active Contour optimizer handles matrix inversion constraints deterministically, ensuring stable step transformations without risking geometric convergence collapse.
* **Modern C++ Compliance:** Built entirely using C++17 paradigms, incorporating strong type safety, strict pointer boundaries, and efficient structure passing to maintain real-time usability profiles.

---

## Repository Directory Tree

```text
project6-cv-edge-shape-detection/
├── CMakeLists.txt                 # Master build configuration and linkage rules
├── activecontour.cpp              # Spline initialization, internal/external energy loops
├── activecontour.h                # Parameter matrices and contour step optimization declarations
├── cannyedgedetector.cpp          # Gaussian blur, Sobel gradients, NMS, and hysteresis tracking
├── cannyedgedetector.h            # Edge tracking maps and kernel parameter declarations
├── houghcircledetector.cpp        # 3D accumulator voting loops for radial geometries
├── houghcircledetector.h          # Circle parameter mapping and local maxima classes
├── houghellipsedetector.cpp       # Multi-dimensional parameter mapping for complex curves
├── houghellipsedetector.h         # Ellipse scoring functions and spatial configurations
├── houghlinedetector.cpp          # Normal-plane accumulator mapping for linear extraction
├── houghlinedetector.h            # Theta-rho parameter space configuration definitions
├── main.cpp                       # Master Qt application setup entrypoint
├── mainwindow.cpp                 # Slot routing, slider transformations, canvas renders
├── mainwindow.h                   # GUI state trackers, timer slots, and image matrices
├── mainwindow.ui                  # Qt Designer layout blueprints for user interaction
└── assets/                        # Output gallery assets (Active_contour.jpeg, circle_detection.jpeg, etc.)

```

---

## Toolchain Setup and Deployment

### Prerequisites

* Build System: CMake (Version 3.16 or higher).
* Core UI Packages: Qt Creator / Qt5 or Qt6 development environments.
* Dependency Matrix: OpenCV Development Libraries (For matrix structures and basic file I/O).
* Compiler Profile: Modern C++17 capable compiler (GCC, Clang, or MSVC).

### Build Pipeline

1. Clone the project tree structure along with its localized submodules:
```bash
git clone git@github.com:lyan2003/Modern-CPP-Computer-Vision-Edge-Shape-Detection.git

```


2. Move into the project workspace and initialize CMake parameters:
```bash
mkdir build && cd build
cmake ..

```


3. Compile the structural translation units into native binary targets:
```bash
cmake --build .

```


4. Fire up the resulting interactive desktop application artifact:
```bash
./CVEdgeShapeDetectorApp

```
