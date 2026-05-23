# Face Spoofing Detection: Data Analytics Competition (DAC) Find IT! 2026

## Description
With the rapid advancement of technology, facial recognition systems have been widely implemented across various sectors, ranging from mobile device unlocking and attendance systems to identity verification in financial services. Despite providing convenience and efficiency, these systems remain vulnerable to security threats, particularly face spoofing. Face spoofing is an attack designed to deceive facial recognition systems using visual media such as printed photos, screen displays, or other facial representations. 

This repository contains the implementation of a robust image-based computer vision model to detect face spoofing attacks. The project was developed for the Data Analytics Competition (DAC) Find IT! 2026, focusing on classifying facial images into six distinct classes while distinguishing between genuine faces and spoofing attempts under varying real-world conditions.

## Objectives
* To develop an image-based deep learning model capable of accurately differentiating between real faces and various spoofing attacks.
* To classify facial images into six target categories: `realperson`, `fake_printed`, `fake_screen`, `fake_mask`, `fake_mannequin`, and `fake_unknown`.
* To build a robust architecture with strong generalization capabilities across different lighting conditions, camera angles, and attack variations.

## Dataset
The dataset comprises facial images categorized into six primary classes:
* **realperson**: Genuine facial images of individuals without any manipulation or attack.
* **fake_printed**: Attacks utilizing printed photos (print attacks) to deceive the system.
* **fake_screen**: Attacks leveraging facial images displayed on digital screens, such as smartphones or monitors.
* **fake_mask**: Attacks involving the use of facial masks, including 3D or silicone masks.
* **fake_mannequin**: Attacks utilizing human replicas, such as mannequins.
* **fake_unknown**: Various other types of spoofing attacks that do not fall into the predefined categories.

## Tech Stack
* **Language**: Python 3
* **Deep Learning Framework**: PyTorch
* **Core Architecture**: DINOv2 (Self-Supervised Vision Transformer)
* **Data Processing & Augmentation**: OpenCV, Pillow (PIL), NumPy, Pandas
* **Evaluation & Metrics**: scikit-learn

## Methodology
1. **Data Preprocessing**: Facial images are cropped, resized, and normalized. Data augmentation techniques are applied to handle variations in lighting and capture angles to reflect real-world scenarios.
2. **Feature Extraction**: The pipeline utilizes the DINOv2 architecture to extract high-level, self-supervised semantic features from the images. This Vision Transformer approach is highly effective in capturing the intricate, pixel-level artifacts necessary to identify spoofing.
3. **Classification Head**: A custom dense neural network layer is trained on top of the DINOv2 representations to perform multi-class classification into the six defined categories.
4. **Inference & Formatting**: The model predicts the class labels for the test set, formatting the output into the required `sample_submission.csv` structure mapped by ID and corresponding label.

## Evaluation
The model is evaluated using the **Macro F1-Score**, which calculates the unweighted mean of the F1-Scores for each class. This metric was strictly selected to account for potential imbalanced distributions within the dataset, ensuring that every class contributes equally to the final score and preventing the model from biasing toward the dominant class.

## Author
Zakki Farian