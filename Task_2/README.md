Markdown

# How to Train YOLOv11 Object Detection on a Custom Dataset

[![Roboflow Notebooks](https://media.roboflow.com/notebooks/template/bannertest2-2.png?ik-sdk-version=javascript-1.4.3&updatedAt=1672932710194)](https://github.com/roboflow/notebooks)

[![GitHub](https://badges.aleen42.com/src/github.svg)](https://github.com/ultralytics/ultralytics)

This notebook demonstrates how to train YOLOv11 object detection model on a custom dataset. YOLOv11 builds on the advancements introduced in YOLOv9 and YOLOv10, incorporating improved architectural designs, enhanced feature extraction techniques, and optimized training methods.  YOLOv11m achieves a higher mean mAP score on the COCO dataset while using 22% fewer parameters than YOLOv8m, making it computationally lighter without sacrificing performance. YOLOv11 is available in 5 different sizes, ranging from `2.6M` to `56.9M` parameters, and capable of achieving from `39.5` to `54.7` mAP on the COCO dataset.

## Getting Started

### Prerequisites

*   A GPU is highly recommended for training. Verify GPU access using `nvidia-smi`. If no GPU is detected, navigate to `Edit` -> `Notebook settings` -> `Hardware accelerator` and set it to `GPU`.
*   Python environment with necessary libraries.  This notebook uses `ultralytics`, `supervision`, and `roboflow`.

### Installation

1.  Clone this repository (replace with your repo URL if forking).
2.  Install the required packages:

```bash
pip install "ultralytics<=8.3.40" supervision roboflow
Dataset Preparation
Dataset Location: YOLOv11 expects data to be located in the datasets directory. You can change this default location via Ultralytics' settings.json.
Dataset Format: This notebook uses a dataset from Roboflow Universe. Download your dataset in the yolov11 export format. Roboflow provides a convenient way to convert data into this format. Make sure your dataset is in the correct format for YOLOv11 training.
Roboflow Integration (Optional): If using a Roboflow dataset, you'll need your Roboflow API key. The notebook provides an example of how to download a dataset directly from Roboflow.
Training
Data YAML: A data.yaml file is required in your dataset directory. This file defines the number of classes, training and validation paths, and class names. Roboflow exports include this file automatically.
Model Selection: Choose a YOLOv11 model size (e.g., yolo11s.pt, yolo11m.pt, etc.). The notebook uses yolo11s.pt as an example. Download the pre-trained model. You can find different model sizes in the Ultralytics YOLOv11 repository.
Training Command: Run the training command, specifying the model, data YAML file, and other hyperparameters (e.g., number of epochs, batch size).
Bash

yolo task=detect mode=train model=yolo11s.pt data=/path/to/your/data.yaml epochs=100 imgsz=640
Replace /path/to/your/data.yaml with the actual path to your data.yaml file.

Example Usage (using Roboflow)
The following code snippet demonstrates how to download a dataset from Roboflow and start training:

Python

import os
HOME = os.getcwd()
!mkdir {HOME}/datasets
%cd {HOME}/datasets

!pip install roboflow

from roboflow import Roboflow
rf = Roboflow(api_key="YOUR_ROBOFLOW_API_KEY") # Replace with your API key
project = rf.workspace("YOUR_WORKSPACE").project("YOUR_PROJECT_ID") # Replace with your workspace and project ID
version = project.version(YOUR_VERSION_NUMBER)  # Replace with your dataset version number
dataset = version.download("yolov11")

!yolo task=detect mode=train model=yolo11s.pt data={dataset.location}/data.yaml epochs=100 imgsz=640
Results
Training results (weights, logs, and predictions) are saved in the runs/detect/train directory by default.  You can monitor training progress using TensorBoard:

Bash

tensorboard --logdir runs/detect/train
Contributing
Contributions are welcome!  Please open an issue or submit a pull request.
