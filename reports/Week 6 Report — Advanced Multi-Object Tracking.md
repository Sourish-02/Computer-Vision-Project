## Objective
The objective of the final project was to improve the baseline YOLOv8 + SORT tracking pipeline developed during Weeks 4–5 by incorporating appearance-based matching, adaptive motion estimation, and more robust data association techniques. The goal was to maintain object identities under challenging conditions such as occlusions, missed detections, and crowded scenes.

---
## Dataset
The project was evaluated on a more challenging pedestrian tracking video containing multiple interacting individuals, frequent occlusions, and complex motion patterns.
Frames were processed sequentially to evaluate both object detection accuracy and long-term tracking consistency.

---
## Detection Pipeline
YOLOv8x was used as the object detector.

Compared to the previous implementation, detection quality was improved through:
- Higher inference resolution (1280 × 1280)
- YOLOv8x pretrained weights
- Confidence thresholding
- Non-Maximum Suppression

Only person detections were forwarded to the tracking module.

---
## Tracking Pipeline
The baseline SORT tracker was extended into a DeepSORT-inspired hybrid tracker.
### Motion Model
- Adaptive Kalman Filter
- Confidence-aware process noise
- Mahalanobis distance gating
### Appearance Model
A pretrained ResNet-based appearance encoder was used to extract feature embeddings for each detected pedestrian.
Appearance similarity enabled identity preservation even when motion information alone became unreliable.
### Data Association
The tracking framework combined:
- Appearance similarity
- Mahalanobis distance
- Intersection over Union (IoU)
using a matching cascade inspired by DeepSORT.

Low-confidence detections were further processed using IoU-based association to recover missed matches.

---
## Additional Improvements

Several refinements were introduced beyond the baseline tracker:

- Adaptive process noise scaling
- Trajectory interpolation across short detection gaps
- Duplicate detection suppression
- Improved track management
- Hybrid appearance-motion matching    

These enhancements significantly improved tracking robustness on crowded scenes.

---
## Configuration

|Component|Configuration|
|---|---|
|Detector|YOLOv8x|
|Input Resolution|1280 × 1280|
|Motion Model|Adaptive Kalman Filter|
|Appearance Model|ResNet-based ReID|
|Data Association|Mahalanobis + Appearance + IoU|
|Tracking Framework|Hybrid DeepSORT-inspired Tracker|

---
## Results
The enhanced tracking pipeline demonstrated improved robustness compared to the baseline SORT implementation.

The incorporation of appearance embeddings and adaptive data association substantially reduced identity switches and improved tracking continuity during occlusions and dense pedestrian interactions. The final system achieved more stable long-term tracking while maintaining real-time performance.

---
## Key Learnings

- Extending SORT into a DeepSORT-inspired tracking framework.
- Integrating appearance embeddings with motion-based tracking.
- Using Mahalanobis distance for robust data association.
- Implementing matching cascades for identity preservation.
- Designing adaptive Kalman Filters for confidence-aware tracking.
- Handling occlusions and missed detections through trajectory interpolation.
- Building an end-to-end real-time multi-object tracking pipeline using modern computer vision techniques.

---
