## Problem: What engineering problem are you solving?
This lab aimed to solve an engineering image-classification problem. Specifically, a surface inspection problem. The model is trained to predict six different manufacturing defects in steel surfaces, making it a multiclass classification problem.

---

## Dataset: What are the six defect classes?
1. **Crazing**: Network of fine cracks.
2. **Inclusion**: Foreign material embedded in the surface.
3. **Patches**: Irregular surface patches.
4. **Pitted Surface**: Small pits or cavities.
5. **Rolled-in Scale**: Oxide scale pressed into the steel surface.
6. **Scratches**: Linear surface scratches.

---

## Deep Neural Network: Describe the fully connected model.
The DNN flattens the 64x64 images into a 1D vector of 4096 values. 

* **Architecture**:
  * **Input Layer**: 4096 inputs
  * **Dense Layer 1**: 256 neurons + ReLU activation
  * **Dense Layer 2**: 64 nuerons + ReLU activation
  * **Output Layer**: 6 outputs, one for each defect class.
* **Parameters**: 1065670 trainable parameters.
* **Limitation**: Different from CNN, DNN can not see spatial relationships between neighboring pixels, missing edges and spatial depth.

---

## CNN: Describe the convolutional model.
The CNN is a solution to the spatial limitations of the DNN. It processes images natively in 2D space by passing a filter that can spot edges and other spatial characteristics.

* **Architecture**:
  * **Block 1**: Conv2D (1→16 filters, 3x3, padding=1) → ReLU → MaxPool2D (2 x2)
  * **Block 2**: Conv2D (16→32 filters, 3x3, padding=1) → ReLU → MaxPool2D (2 x2)
  * **Block 3**: Conv2D (32→64 filters, 3x3, padding=1) → ReLU → MaxPool2D (2 x2)
  * **Fully Connected**: Flatten (64x8x8=4096 inputs) → Linear (128 units) → ReLU → Linear (6 units)
* **Parameters**: 548486 trainable parameters (nearly half of the DNN).

---

## Evaluation: Report test accuracy, per-class performance, confusion matrix, and major failure cases.
Both models were trained using the *Adam Optimizer* with a learning rate of 0.001 and a 70/15/15 train/validation/test split.

| Model Metric | Deep NN (20 Epochs) | Original CNN (20 Epochs) | Modified CNN (40 Epochs) |
| :--- | :---: | :---: | :---: |
| **Parameters** | 1065670 | 548486 | 548486 |
| **Val. Accuracy** | 46.70% | 91.50% | 95.20% |
| **Test Accuracy** | 48.52% | 91.85% | 94.07% |

### Why does the CNN outperform the DNN?
* **Spatial Correlation**: CNNs preserve the 2D layout of pixels, detecting edges, textures, and local shapes that are destroyed when a DNN flattens the image.
* **Weight Sharing**: CNNs apply the same filter across the entire image, which reduces overfitting.

### Per-Class Performance
Based on the test split classification report:
* **Highest Recall**: `patches` (0.976) and `rolled_in_scale` (1.000), making them extremely easy for the CNN to detect.
* **Lowest Recall**: `inclusion` (0.854), showing the model occasionally misses these defects.

---

## Model Comparison: Which model performed better and why?
The CNN models outperformed the DNN. CNNs do this because they process images natively in 2D, applying filters that detect edges and other spatial features, rather than flattening images into a 1D vector as DNNs do.

---

## Application: Explain how to run the classifier application.
The app is integrated into the lab04 code. After defining and training the model, the app uses it to classify any image uploaded to it. Simply upload any image you want to be classified, and the app will do so using the trained model.

## Engineering Conclusion: Would you deploy this model? Explain the limitations.
I would not deploy this model. I think that the test accuracy of 94.07% is still low for a model intended to be implemented in the manufacturing quality contro industry.
