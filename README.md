##  Colab Notebook
 [Open in Google Colab][https://colab.research.google.com/drive/1E-q5dXuUdJVeRP0tYu_paPbXbnvmI0lV?usp=sharing](https://colab.research.google.com/drive/1cj-l0AhJ3MHJJ5AWwnTsgOEfssbgb5SQ?usp=sharing)


#  CNN Model Comparison and Analysis (Final Reflection)

---

##  A. Model Performance

### 1. Which pre-trained model achieved the highest accuracy? Why?
MobileNetV2 achieved the highest accuracy of 0.8547.

Reasons: Its architecture uses inverted residual blocks and depthwise separable convolutions, which allow it to extract sophisticated features efficiently while maintaining a lower parameter count, preventing the overfitting that often plagues larger models on smaller datasets.

### 2. Which model had the lowest performance? What could be the reason?
EfficientNetB0 (or ResNet50 in some runs) had the lowest performance, with a Final Validation Accuracy of approximately 0.0818.

Reasons: This is likely due to underfitting or incorrect preprocessing; EfficientNet typically expects inputs in a specific range (0 to 255) rather than the normalized -1 to 1 range used for MobileNetV2.

### 3. How did loss values compare across models?
MobileNetV2 had the lowest validation loss of 0.7112, indicating high confidence.

EfficientNetB0 and ResNet50 showed much higher validation losses (above 2.80), suggesting they struggled to differentiate between the 20 classes.

Overfitting: A low training loss paired with high validation loss indicates the model memorized the training set rather than learning general features.

B. Evaluation Metrics
### 4. Why is accuracy not enough to evaluate a model?
Accuracy can be misleading when there is a class imbalance. In your dataset, some classes (like Begonia_australis) have more images than others, so a model could achieve high accuracy just by predicting the majority class correctly.

### 5. Which model had the best F1-score? What does it indicate?
MobileNetV2 had the best F1-score of 0.8288.

Indication: This indicates a strong balance between Precision (avoiding false positives) and Recall (avoiding false negatives).

### 6. How did Precision and Recall differ across models?
MobileNetV2 maintained a high balance (Macro Precision: 0.83, Macro Recall: 0.85).

The poor-performing models had extremely low values (near 0.05), failing to reliably identify specific Begonia species.

C. Confusion Matrix Analysis
### 7. Which classes were frequently misclassified?
Classes with similar visual features, such as Begonia_maculata and Begonia_Tiger_Paws, are hardest for the model to distinguish.

### 8. What patterns did you observe in the confusion matrix?
Correct predictions appear on the diagonal.

Errors occur between visually similar classes (off-diagonal values).

D. ROC and AUC
### 9. Which model had the highest AUC score?
MobileNetV2 had the highest AUC score of 0.9856.

### 10. What does AUC tell us about model performance?
AUC measures the model’s ability to distinguish between classes; a score close to 1.0 indicates excellent performance.

E. Explainability (Grad-CAM)
### 11. What did Grad-CAM reveal about model decision-making?
Grad-CAM shows the important regions influencing a prediction. In image_cc5779.jpg, it reveals where the model "looked" to decide a plant was Begonia_Acetosa.

### 12. Did the model focus on relevant image regions?
MobileNetV2 focused on the leaf structures.

ResNet50 had a more spread-out heatmap, potentially looking at background noise despite its high confidence.

### 13. Which model produced the most meaningful heatmaps?
MobileNetV2 produced the most focused heatmaps, highlighting the center of the plant rather than irrelevant background areas.

F. Model Comparison & Improvement
### 14. Which model would you recommend for deployment? Why?
MobileNetV2.

Reason: It achieved the highest accuracy, F1-score, and AUC, and it is lightweight enough for mobile/web apps.

### 15. How can you further improve your best-performing model?
Fine-tuning: Unfreeze deeper layers for more specific training.

Data Augmentation: Use random rotations/crops.

Regularization: Apply Dropout to prevent overfitting.

G. Real-World Application
### 16. How can your model be applied in real-world scenarios?
It can be used for image classification systems, medical diagnosis, or botanical monitoring (e.g., identifying plants in a greenhouse).

### 17. What are the risks of deploying an inaccurate model?
Risks include incorrect predictions, misleading decisions, and loss of user trust.

### 18. How can this system be integrated into a mobile/web app?
Convert the model to TensorFlow Lite (mobile) or use a Flask/Django API (web).

Preprocess the input images to the same size used in training (224x224).
