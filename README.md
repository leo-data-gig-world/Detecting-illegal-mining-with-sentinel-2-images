# Detecting Illegal Mining with Sentinel-2 Images

> Dissertation Project - Object Detection using Transfer Learning

## Overview

This project examines the possibility of using satellite imagery from the **Sentinel-2** Earth observation mission to detect illegal mining activities through transfer learning in deep neural networks.

The approach transfers learning from a pre-trained model (COCO dataset) and adapts it with annotated satellite imagery of legal and illegal mining sites, training a model that can automatically recognize illegal mines.

## Results Summary

- Models showed **certain level of performance** during training
- Performance **improved by increasing input scale** during training
- When tested on new data (simulating real-world), models showed **significant regression**
- **Conclusion**: Not ready for practical use; further research needed

---

## Repository Structure

```
├── notebooks/              # Jupyter notebooks for training/evaluation
├── scripts/                # Python utility scripts
├── requirements.txt        # Python dependencies
└── README.md               # This file
```

### External Dependencies (Not in Repo)

You'll need to download separately:

| Component | Source |
|-----------|--------|
| TensorFlow Object Detection API | [GitHub](https://github.com/tensorflow/models/tree/master/research/object_detection) |
| Pre-trained Model | [TF2 Detection Zoo](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/tf2_detection_zoo.md) |

### Required Folder Structure

```
project-root/
├── workspace/
│   └── trained_model/      # Your trained models go here
├── addons/                 # Object Detection API addons
├── models/                 # TensorFlow models repository
├── scripts/                # Training scripts
└── TestDataset/            # Test dataset for evaluation
```

---

## Setup

### 1. Environment

```bash
# Create conda environment
conda create -n mining-detection python=3.7.13
conda activate mining-detection

# Install dependencies
pip install -r requirements.txt
```

### 2. TensorFlow Object Detection API

```bash
# Clone TensorFlow models
git clone https://github.com/tensorflow/models.git

# Follow installation instructions:
# https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/tf2.md
```

### 3. Download Pre-trained Model

```bash
# Download Faster R-CNN ResNet50 from model zoo
wget http://download.tensorflow.org/models/object_detection/tf2/20200711/faster_rcnn_resnet50_v1_640x640_coco17_tpu-8.tar.gz

# Extract to models/ directory
```

### 4. Prepare Dataset

1. Collect Sentinel-2 imagery for:
   - Legal mining sites
   - Illegal mining sites
2. Annotate with bounding boxes (use LabelImg or similar)
3. Convert to TFRecord format

### 5. Train

```bash
# Update pipeline.config with your paths
# Run training script from notebooks/
```

---

## Technical Details

### Model Architecture

**Faster R-CNN ResNet50** - chosen for:
- Time-efficient training
- Good balance of speed and accuracy
- Pre-trained on COCO dataset (80 object categories)

### Data

- **Source**: Sentinel-2 satellite imagery
- **Annotation**: Bounding boxes for mining sites
- **Classes**: Legal mining, Illegal mining

### Training

- Transfer learning from COCO weights
- Progressive scaling of input images improved results
- Multiple training runs with different configurations

---

## Requirements

| Package | Version |
|---------|---------|
| Python | 3.7.13 |
| TensorFlow | 2.9 |
| CUDA | 11.2 |
| CuDNN | 8.1.0.77 |
| opencv-python-headless | 4.1.2.30 |
| pycocotools | 2.0.4 |

---

## Findings

### What Worked

- Transfer learning successfully adapted to satellite imagery
- Increasing input scale improved model performance
- Training converged with reasonable loss values

### Challenges

- **Domain gap**: Model performance regressed significantly on new data
- **Generalization**: Not yet robust enough for real-world deployment
- **Data scarcity**: Limited annotated satellite imagery available

### Future Work

- Larger and more diverse training dataset
- Data augmentation techniques specific to satellite imagery
- Experiment with other architectures (YOLO, EfficientDet)
- Multi-temporal analysis (detecting changes over time)
- Integration with other satellite data sources

---

## Citation

If you use this work, please cite:

```
@misc{illegal_mining_detection_2024,
  author = {Leo Wong},
  title = {Detecting Illegal Mining with Sentinel-2 Images using Transfer Learning},
  year = {2024},
  publisher = {GitHub},
  url = {https://github.com/leo-data-gig-world/Detecting-illegal-mining-with-sentinel-2-images}
}
```

---

## License

This project is for academic research purposes.

## Acknowledgments

- European Space Agency (ESA) for Sentinel-2 imagery
- TensorFlow team for Object Detection API
- COCO dataset for pre-trained weights
