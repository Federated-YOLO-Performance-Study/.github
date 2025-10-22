## Hi there
# Experimental Setup

[![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python&logoColor=white)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.1-orange?logo=pytorch&logoColor=white)](https://pytorch.org/)
[![Docker](https://img.shields.io/badge/Docker-20.10-blue?logo=docker&logoColor=white)](https://www.docker.com/)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)

This repository contains the hardware and software setup for evaluating the YOLO12s model on different edge devices.

---

## Table of Contents

- [Edge Devices](#edge-devices)
- [Software Setup](#software-setup)
  - [Key Details](#key-details)
- [Procedure](#procedure)

---

## Edge Devices

The setup includes three edge devices:

- **Titan 300 TGL-UP3**
- **ASUS NUC 14 Pro+**
- **NVIDIA Jetson AGX Orin 64GB Developer Kit**

These devices cover both Intel-based and ARM-based architectures, allowing performance evaluation on **CPU**, **GPU**, and **NPU** platforms.

| Device | Architecture | Platform |
|--------|--------------|----------|
| Titan 300 TGL-UP3 | Intel | CPU / GPU / NPU |
| ASUS NUC 14 Pro+ | Intel | CPU / GPU |
| NVIDIA Jetson AGX Orin 64GB | ARM | GPU / NPU |

---

## Software Setup

The software environment uses **Docker** with custom images optimized for each device:

| Device | Base Image | Framework | OS | Kernel |
|--------|------------|-----------|----|--------|
| Titan 300 TGL-UP3 | Custom Docker (OpenVINO optimized) | PyTorch / OpenVINO | Ubuntu 20.04.6 LTS | 5.15.0-139-generic |
| ASUS NUC 14 Pro+ | Custom Docker (OpenVINO optimized) | PyTorch / OpenVINO | Ubuntu 24.04.2 LTS | 6.11.0-26-generic |
| NVIDIA Jetson AGX Orin 64GB | JetPack SDK base image | PyTorch | Ubuntu 20.04.6 LTS | 5.10.120-tegra |

### Key Details

- **Frameworks:** [PyTorch](https://pytorch.org/) for model deployment, [OpenVINO](https://docs.openvino.ai/) for Intel devices.
- Validation used the argument `--half=True` to enable FP16 inference, reducing memory usage.
- Differences in OS versions may slightly affect performance due to kernel and scheduling differences, but the impact is minimal.
- Python libraries used:
  - [Ultralytics](https://docs.ultralytics.com/) for YOLO model handling
  - [PyRAPL](https://pypi.org/project/pyRAPL/) for energy measurement
  - [psutil](https://pypi.org/project/psutil/) for system monitoring

All experiment results are stored in **CSV files** for easy access and structured analysis.

---

## Procedure

1. **Model Training**  
   The YOLO12s model was trained in a **federated learning** setup with one server and ten clients. Each node ran a GPU-enabled Conda virtual environment.

2. **Model Evaluation**  
   The final **global model** from the server was used for evaluation on the testing datasets during **validation** and **prediction** phases.

3. **Image Processing**  
   - All input images were resized to **640 × 640** pixels.  
   - Most datasets had varying resolutions; **Green Grapes** and **Purple Grapes** datasets were originally **389 × 480**.

4. **Data Recording**  
   - Python scripts were used for grape detection and system monitoring.  
   - Results were saved in **CSV format** for structured analysis.




<img width="958" height="595" alt="image" src="https://github.com/user-attachments/assets/ea85574e-122c-41f7-b632-ea01adb75724" />

<img width="640" height="640" alt="image" src="https://github.com/user-attachments/assets/53a0f54a-64d6-4c06-8813-7442789ae0d5" />

<img width="355" height="355" alt="image" src="https://github.com/user-attachments/assets/dbc1ee4b-5e36-4673-80f5-1735dd7d16f4" />


Deploy the federated global model, pre-trained on YOLOv12, on various edge nodes, including the Titan 300 TGL-UP3, Asus NUC 14 PRO+ AI Ready Mini-PCs, and the NVIDIA Jetson AGX Orin 64GB Developer Kit.
