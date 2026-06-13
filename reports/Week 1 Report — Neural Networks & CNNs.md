## Objective

The objective of this week's project was to understand the fundamentals of neural networks and convolutional neural networks by building an image classification pipeline on the FashionMNIST dataset using PyTorch.

---
## Dataset

FashionMNIST is a benchmark image classification dataset consisting of 70,000 grayscale images of clothing items belonging to 10 categories.

- Training Samples: 60,000
- Test Samples: 10,000
- Image Size: 28 × 28
- Number of Classes: 10

---
## Data Pipeline

The dataset was loaded using `torchvision.datasets.FashionMNIST`.
Preprocessing steps included:
- Conversion of images to tensors
- Scaling pixel values to the range \[0,1]
- Mini-batch loading using DataLoader
Training batches were shuffled during training to improve generalization.

---
## Model Architecture
Two architectures were implemented during this project.
### Fully Connected Neural Network
The baseline model consisted of fully connected layers operating on flattened FashionMNIST images.

Architecture:
- Input Layer: 784 neurons (28 × 28 image flattened)
- Hidden Layer 1: 1024 neurons + ReLU
- Hidden Layer 2: 512 neurons + ReLU
- Output Layer: 10 neurons
### Convolutional Neural Network
The final model used convolutional layers for feature extraction followed by fully connected layers for classification.
#### Feature Extraction

Block 1:
- Conv2D (1 → 32)
- ReLU
- Conv2D (32 → 32)
- ReLU
- MaxPool2D

Block 2:
- Conv2D (32 → 64)
- ReLU
- Conv2D (64 → 64)
- ReLU
- MaxPool2D

#### Classification Head
- Linear (3136 → 256)
- ReLU
- Linear (256 → 128)
- ReLU
- Linear (128 → 10)

The CNN architecture was used for the final training and submission generation.

---
## Training Configuration

|Parameter|Value|
|---|---|
|Optimizer|Adam|
|Learning Rate|1e-3|
|Batch Size|64|
|Epochs|10|
|Loss Function|CrossEntropyLoss|
Training was accelerated using CUDA-enabled GPU hardware.

---
## Results
The model demonstrated strong performance on FashionMNIST and achieved approximately 88% test accuracy after the first epoch, with further improvements observed during subsequent training, reaching 92.6% after the tenth epoch.
The CNN significantly outperformed a simple fully-connected neural network by exploiting spatial patterns through convolutional layers.

---
## Key Learnings
- Understanding the complete deep learning workflow in PyTorch.
- Building custom neural network architectures using `nn.Module`.
- Implementing training and evaluation loops.
- Using GPU acceleration for faster training.
- Understanding how convolutional layers extract spatial features.
- Appreciating the performance advantages of CNNs over traditional fully-connected networks for image tasks.
---
