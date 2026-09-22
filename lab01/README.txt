Laboratory
Lab 1 — Building Your Deep Learning Workbench

Objective
The objective of this lab experiment was to get hands-on with GitHub, Google Colab, as well as other tools to test a pretrained image-classification model.

Tools Used
Python
Google Colab
PyTorch
GitHub
Hugging Face

Model Used
vit-base-patch16-224 (Vision Transformer, BERT-like architecture)

Main Result
The model correctly classified three of the six images. For the correctly classified images, the model had a confidence score of at least 0.95. Among the incorrectly classified images, for two of them, the model failed to include the correct classification in the top-5 predictions. The other image had the correct classification as the fourth prediction.

Interesting Failure
Unexpectedly, the model misclassified a car motor, failing to include the correct classification in the top-5 predictions. It also, as expected, misclassified the anti-face-recognition T-shirts. Interestingly, for one of the T-shirts, the model had only a 0.07 confidence-score difference between the first and third predictions, while assigning a confidence score of only 0.06 to the fourth prediction, which was correct. It also failed to include the correct classification in the top-5 predictions for the other T-shirt, assigning a relatively high confidence score of 0.67 to the first and incorrect prediction.