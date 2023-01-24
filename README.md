# MediaPipe Face Mesh

## INTRODUCE

MediaPipe Face Mesh is a solution that estimates 468 3D face landmarks in real-time even on mobile devices. It employs machine learning (ML) to infer the 3D facial surface, requiring only a single camera input without the need for a dedicated depth sensor. Utilizing lightweight model architectures together with GPU acceleration throughout the pipeline, the solution delivers real-time performance critical for live experiences.
Additionally, the solution is bundled with the Face Transform module that bridges the gap between the face landmark estimation and useful real-time augmented reality (AR) applications. It establishes a metric 3D space and uses the face landmark screen positions to estimate a face transform within that space. The face transform data consists of common 3D primitives, including a face pose transformation matrix and a triangular face mesh. Under the hood, a lightweight statistical analysis method called Procrustes Analysis is employed to drive a robust, performant and portable logic. The analysis runs on CPU and has a minimal speed/memory footprint on top of the ML model inference.

# Models
FACE DETECTION MODEL
The face detector is the same BlazeFace model used in MediaPipe Face Detection. Please refer to MediaPipe Face Detection for details.

FACE LANDMARK MODEL
For 3D face landmarks we employed transfer learning and trained a network with several objectives: the network simultaneously predicts 3D landmark coordinates on synthetic rendered data and 2D semantic contours on annotated real-world data. The resulting network provided us with reasonable 3D landmark predictions not just on synthetic but also on real-world data.

The 3D landmark network receives as input a cropped video frame without additional depth input. The model outputs the positions of the 3D points, as well as the probability of a face being present and reasonably aligned in the input. A common alternative approach is to predict a 2D heatmap for each landmark, but it is not amenable to depth prediction and has high computational costs for so many points. We further improve the accuracy and robustness of our model by iteratively bootstrapping and refining predictions. That way we can grow our dataset to increasingly challenging cases, such as grimaces, oblique angle and occlusions.

You can find more information about the face landmark model in this [paper](https://arxiv.org/abs/1907.06724).
# OUTPUT 
> Real image
![2](https://user-images.githubusercontent.com/92161283/214234073-0a4485dc-0fa1-46fb-8c08-e66792295768.png)
> real output
![2](https://user-images.githubusercontent.com/92161283/214234219-b1c26e9e-4ca6-465e-b330-9c9f9d14dc6d.png)
