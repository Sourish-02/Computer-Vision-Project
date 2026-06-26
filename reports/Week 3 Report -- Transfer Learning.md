## Objective

The objective of this week's project was to explore Transfer Learning by leveraging pretrained ResNet-18 models on the EuroSAT dataset. The project focused on comparing feature extraction using a frozen backbone with full model fine-tuning and analysing the advantages of pretrained models over training from scratch.

---
## Dataset
The EuroSAT dataset, introduced in Week 2, was used for all experiments.

Images were loaded using the `ImageFolder` API and divided into training and validation subsets. The same preprocessing pipeline from the previous week was retained to ensure a fair comparison between models.

---
## Data Pipeline
The dataset preprocessing pipeline consisted of:
### Training Transformations
- Resize (64 × 64)
- Random Horizontal Flip
- Random Vertical Flip
- Random Rotation
- Color Jitter
- Normalization

### Validation Transformations
- Resize (64 × 64)
- Normalization

Mini-batches were loaded using the PyTorch `DataLoader` with GPU acceleration for efficient training.

---
## Model Architectures
Two transfer learning strategies were implemented using a pretrained ResNet-18 backbone.

### Frozen Backbone
The pretrained convolutional backbone was frozen, preventing its weights from being updated during training. Only the final fully connected classification layer was replaced and trained on the EuroSAT dataset.

Architecture:
- Pretrained ResNet-18 Feature Extractor (Frozen)
- Fully Connected Classification Layer (10 Classes)

---
### Fine-Tuned ResNet-18
The pretrained ResNet-18 model was initialized with ImageNet weights, after which all network parameters were allowed to update during training.

Architecture:
- Pretrained ResNet-18 Backbone
- Fully Connected Classification Layer (10 Classes)
- End-to-End Fine-Tuning

---
## Training Configuration

| Parameter     | Value            |
| ------------- | ---------------- |
| Optimizer     | AdamW            |
| Learning Rate | 1e-3             |
| Weight Decay  | 1e-4             |
| Batch Size    | 64               |
| Epochs        | 15               |
| Loss Function | CrossEntropyLoss |

A learning rate scheduler was employed to improve convergence throughout training. Model checkpoints were saved based on the best validation accuracy.

---
## Performance Evaluation

The performance of the transfer learning models was evaluated using:

- Validation Accuracy
- Validation Loss
- Classification Report
- Confusion Matrix

The results were compared with the CNN trained from scratch in Week 2 to evaluate the effectiveness of transfer learning on satellite imagery classification.

---
## Results
Three approaches were evaluated on the EuroSAT dataset:

- CNN trained from scratch: Train Loss: 0.1137 | Val Loss: 0.1036 | Val Acc: 96.28%
- Frozen ResNet-18: Train Loss: 0.2568 | Val Loss: 0.2306 | Val Acc: 91.98%
- Fine-Tuned ResNet-18: Train Loss: 0.0149 | Val Loss: 0.0364 | Val Acc: 98.80%

The fine-tuned ResNet-18 achieved the best overall performance, attaining a validation accuracy of **98.80%** with the lowest validation loss. While the frozen backbone converged quickly with minimal training, allowing the pretrained network to fine-tune its weights resulted in a substantial improvement in classification performance. The CNN trained from scratch performed competitively but was ultimately outperformed by the fine-tuned transfer learning model.

---
## Key Learnings

- Understanding the motivation behind transfer learning.
- Implementing feature extraction using a frozen pretrained backbone.
- Fine-tuning pretrained convolutional networks for domain-specific datasets.
- Using pretrained ImageNet weights to accelerate convergence.
- Comparing frozen and fine-tuned transfer learning strategies.
- Applying learning rate scheduling and model checkpointing during training.
- Evaluating pretrained models using validation metrics, confusion matrices, and classification reports.
- Analysing the trade-offs between training from scratch and transfer learning.

---
