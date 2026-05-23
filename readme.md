# Ceramic Defect Detection System

## Overview
The Ceramic Defect Detection System is an automated computer vision solution designed to inspect ceramic tiles and identify surface anomalies. By leveraging traditional image processing techniques and geometric analysis, the system categorizes tiles into three distinct states: **NORMAL**, **CRACK**, and **HOLE**. This project aims to streamline quality control processes in manufacturing lines by reducing the reliance on manual visual inspection.

## Table of Contents
- [Features](#features)
- [Technology Stack](#technology-stack)
- [Methodology and Pipeline](#methodology-and-pipeline)
- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [License](#license)

## Features
- **Automated Defect Classification**: Accurately distinguishes between structural cracks and surface holes based on geometric properties.
- **Adaptive Lighting Correction**: Utilizes advanced histogram equalization to mitigate inconsistencies caused by factory lighting and shadows.
- **Noise Reduction**: Preserves critical edge data while smoothing surface textures (e.g., sand or dust) to prevent false positives.
- **Conveyor Belt Exclusion**: Automatically masks the outer frames or conveyor belt edges to focus solely on the ceramic tile surface.
- **Visual Reporting**: Generates side-by-side comparative plots showing the original image, morphological masks, and the final bounding box annotations.

## Technology Stack
- **Language**: Python 3.8+
- **Computer Vision**: OpenCV (`cv2`)
- **Numerical Computation**: NumPy
- **Data Visualization**: Matplotlib
- **Standard Libraries**: `pathlib`, `typing`

## Methodology and Pipeline

The system processes each image through a rigid, sequential pipeline composed of three main stages:

### 1. Pre-Processing
The initial stage focuses on standardizing the input image to prepare it for feature extraction.
- **Grayscale Conversion**: Simplifies the computational matrix by converting the BGR image to a single-channel grayscale image.
- **CLAHE (Contrast Limited Adaptive Histogram Equalization)**: Equalizes the contrast locally across the image. This step is crucial for revealing faint defects hidden in shadows or overexposed areas.
- **Bilateral Filtering**: Applies a non-linear, edge-preserving, and noise-reducing smoothing filter. It eliminates granular surface noise while maintaining the sharp gradients of actual defects.

### 2. Edge Detection and Morphology
This stage extracts the structural anomalies from the pre-processed image.
- **Auto-Canny Edge Detection**: Dynamically calculates the upper and lower thresholds based on the image's median pixel intensity, ensuring robust edge detection across varying lighting conditions.
- **Dilation**: Thickens the detected edges using a rectangular structuring element to bridge minor gaps in continuous cracks.
- **Morphological Opening**: Removes small, isolated white specks (false positives) from the binary mask.
- **Frame Removal**: Applies a zero-matrix mask to the outer margins of the image, actively ignoring structural lines caused by the conveyor belt or scanning frame.

### 3. Feature Classification
The final stage analyzes the connected components within the binary mask to determine the defect type.
- **Connected Components Analysis**: Filters out exceptionally small objects based on a minimum area threshold.
- **Contour Extraction**: Generates bounding boxes around the remaining valid artifacts.
- **Geometric Rule Engine**:
  - **Cracks**: Identified by high diagonal lengths or extreme aspect ratios (highly elongated or highly flattened contours).
  - **Holes**: Identified by moderate diagonal lengths combined with aspect ratios closer to 1.0 (circular or blocky shapes).
- **Annotation**: Overlays color-coded bounding boxes on the original image (Red for cracks, Green for holes).

## Installation

1. Clone this repository to your local machine:
```bash
   git clone [https://github.com/yourusername/ceramic-defect-detection.git](https://github.com/yourusername/ceramic-defect-detection.git)
   cd ceramic-defect-detection

```

2. Create and activate a virtual environment (recommended):

```bash
   python -m venv venv
   source venv/bin/activate  # On Windows use: venv\Scripts\activate

```

3. Install the required dependencies:

```bash
   pip install opencv-python numpy matplotlib

```

## Usage

1. Ensure your target images are placed in the `dataset/` directory. The system specifically targets `.png` files.
2. Execute the main script:

```bash
   python main.py

```

3. The system will iterate through the dataset, outputting the processing status in the console and rendering a Matplotlib figure for each processed tile. Close the current figure window to proceed to the next image.

## Project Structure


ceramic-defect-detection/
│
├── dataset/                # Directory containing input .png images
│   ├── sample_01.png
│   └── sample_02.png
│
├── main.py                 # The core detection script
├── README.md               # Project documentation
└── requirements.txt        # Python dependencies

## License

This project is licensed under the MIT License. You are free to modify and distribute the software as per the terms of the license.

