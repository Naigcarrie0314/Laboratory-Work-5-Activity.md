##  Colab Notebook
 [Open in Google Colab][https://colab.research.google.com/drive/1E-q5dXuUdJVeRP0tYu_paPbXbnvmI0lV?usp=sharing](https://colab.research.google.com/drive/1cj-l0AhJ3MHJJ5AWwnTsgOEfssbgb5SQ?usp=sharing)


#  CNN Model Comparison and Analysis (Final Reflection)

---

##  A. Model Performance

A. Model Performance & Comparison
1. Highest Accuracy Model
MobileNetV2 achieved the highest accuracy.

Final Validation Accuracy: 85.47%.

Why? Its architecture uses depthwise separable convolutions, which are highly efficient at extracting complex features (like the unique vein and leaf patterns of the 20 Begonia species) while maintaining a low parameter count that prevents excessive overfitting on a dataset of this size.

2. Lowest Performance Model
ResNet50 had the lowest performance.

Final Validation Accuracy: 8.18%.

Reason: ResNet50 is a deep, heavy architecture. Given the training logs showing only 10 epochs, this model likely underfit. It requires more training time or a better-tuned learning rate to move past initial weights and start distinguishing between the species.

3. Loss Value Comparison
Best Model (MobileNetV2): Lowest validation loss (0.7112).

Poor Models: EfficientNetB0 (2.9937) and ResNet50 (2.8062) showed much higher losses, indicating they were essentially guessing across the 20 classes.

B. Evaluation Metrics
4. Why Accuracy isn't Enough
As seen in your data counts (e.g., Begonia bowerae with 260 images vs. Begonia australis with 310), there is a slight class imbalance. Accuracy can be misleading if the model performs well on common classes but fails on rarer ones.

5. F1-Score Importance
The model with the highest F1-score (MobileNetV2) is the most reliable because the F1-score balances Precision (avoiding false IDs) and Recall (capturing all instances of a species).

C. Confusion Matrix & Explainability
7. Frequently Misclassified Classes
In a botanical dataset like this, species with similar visual traits—such as Begonia maculata and Begonia 'Tiger Paws'—are often confused due to similar leaf spotting or edge textures.

### 11. Grad-CAM Insights
Grad-CAM heatmaps for a good model should highlight the leaf texture or flower center. If the heatmap highlights the background or the pot, the model is making decisions based on irrelevant data, making it less reliable for deployment.

F. Deployment & Improvement

### 14. Recommended Model for Deployment
MobileNetV2.

Reason: It is the only model that reached a high level of accuracy (85%+) within 10 epochs. It is also lightweight, making it perfect for the mobile/web applications mentioned in your workflow.

### 15. Further Improvements
Fine-Tuning: Unfreeze the top layers of the pre-trained MobileNetV2 base to specialize in Begonia features.

Data Augmentation: Apply random rotations and color shifts to help the model learn the leaf shapes rather than specific lighting conditions in the photos.

G. Real-World Application

### 18. Mobile/Web Integration
To move this system into production:

Conversion: Export the trained MobileNetV2 to TensorFlow Lite or TensorFlow.js.

API: Set up a Flask or Django backend to handle the image uploads.

Preprocessing: Ensure the app resizes user photos to 224x224, matching the input shape used during training.

What kind of interface were you planning for the user to upload their Begonia photos—a simple web form or a dedicated mobile app?

