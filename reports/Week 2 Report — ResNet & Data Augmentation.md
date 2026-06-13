## Objective
The objective of this week's project was twofold:
1. Evaluate the FashionMNIST CNN developed during Week 1 using detailed classification metrics.
2. Build and train a ResNet-inspired image classification model on the EuroSAT dataset while exploring residual learning, batch normalisation, and data augmentation techniques.

---

## Part I — Model Evaluation on FashionMNIST

### Evaluation Metrics
The CNN trained during Week 1 was evaluated using:
- Classification Report
- Confusion Matrix
- Per-Class Accuracy
These metrics provide a more detailed understanding of model performance than overall accuracy alone.

### Observations
1. Analysis of the confusion matrix revealed that the model struggled most with visually similar upper-body garments such as shirt, T-Shirt,  Pullover,  Coat
2. The Shirt category produced the lowest diagonal value in the confusion matrix, indicating that it was the most difficult class to classify correctly.
This highlights the importance of class-wise evaluation rather than relying solely on aggregate accuracy.
---
## Part II — EuroSAT Classification Pipeline

### Dataset
The EuroSAT dataset consists of satellite imagery belonging to multiple land-use categories.
Images were loaded using the ImageFolder API and split into training and validation sets.

---
## Data Augmentation
To improve model generalisation and reduce overfitting, several augmentation techniques were applied during training:
- Resize (64 × 64)
- Random Horizontal Flip
- Random Vertical Flip
- Random Rotation
- Color Jitter
- Normalisation
Validation images used only resizing and normalisation.
---
## Model Architecture
A custom ResNet-inspired architecture was implemented.
### Stem
- Convolution Layer
- Batch Normalisation
- ReLU Activation
### Residual Blocks
The network employed residual blocks containing:
- Convolution Layers
- Batch Normalisation
- ReLU Activations
- Identity Shortcut Connections
These skip connections allow gradients to flow more effectively through deeper networks and help alleviate degradation issues.
### Classification Head
The extracted features were passed through fully connected layers to produce predictions for the ten EuroSAT classes.

---
## Training Configuration

|Parameter|Value|
|---|---|
|Optimizer|AdamW|
|Learning Rate|1e-3|
|Weight Decay|1e-4|
|Batch Size|64|
|Epochs|20|
|Loss Function|CrossEntropyLoss|
A learning rate scheduler was used to improve convergence during training.
The best-performing model was automatically saved using validation accuracy as the selection criterion.

---
## Validation and Performance Analysis
Model performance was evaluated on the validation set using:
- Validation Accuracy
- Classification Report
- Confusion Matrix
These metrics were used to identify class-specific strengths and weaknesses and to assess the effectiveness of residual learning and data augmentation.

---
## Key Learnings
- Computing and interpreting classification reports.
- Analysing confusion matrices and per-class accuracy.
- Understanding residual learning through practical implementation.
- Applying data augmentation to improve generalization.
- Using Batch Normalization to stabilize training.
- Training deeper convolutional networks using AdamW optimization.

---
