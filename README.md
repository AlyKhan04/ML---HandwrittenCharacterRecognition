# Handwritten Character Recognition

A Jupyter Notebook-based project that trains a **Convolutional Neural Network (CNN)** to recognize handwritten characters (A–Z) from the [A–Z Handwritten Alphabets dataset on Kaggle](https://www.kaggle.com/datasets/sachinpatel21/az-handwritten-alphabets-in-csv-format). The project includes an interactive drawing canvas for real-time predictions.

---

## 🚀 Methodology

### Data & Preprocessing
- **Dataset**: [A–Z Handwritten Alphabets (Kaggle)](https://www.kaggle.com/datasets/sachinpatel21/az-handwritten-alphabets-in-csv-format).
- **Transforms**: Images are resized to `28x28`, converted to grayscale, and normalized to values between 0 and 1.
- **Labels**: Each image is assigned one of 26 classes corresponding to English uppercase letters (A–Z).
- **Interface**: The notebook includes a simple canvas for drawing input characters.

---

### Model Architecture
The CNN was designed to progressively extract visual features from handwritten letters.  

**Layers Breakdown:**
1. **Input (28×28×1)** – grayscale character image.  
2. **Conv2D (32 filters, 3×3, ReLU)** – Detects simple edges and strokes.  
3. **Conv2D (64 filters, 3×3, ReLU)** – Builds on earlier features to capture corners and curves.  
4. **MaxPooling (2×2) + Dropout (0.25)** – Reduces spatial dimensions and prevents overfitting.  

5. **Two Convolution Blocks (128 filters, 3×3, padding='same') + ReLU** – Learns higher-level patterns such as loops and angles.  
   - Followed by **MaxPooling (2×2)** and **Dropout (0.25)**.  

6. **Two Convolution Blocks (256 filters, 3×3, padding='same') + ReLU** – Extracts deep, complex features distinguishing between similar letters (e.g., O vs Q).  
   - Followed by **MaxPooling (2×2)** and **Dropout (0.25)**.  

7. **Flatten Layer** – Converts feature maps into a feature vector.  

8. **Fully Connected Layers**:  
   - **Dense (512, ReLU) + BatchNorm + Dropout (0.5)** – Learns abstract feature combinations.  
   - **Dense (256, ReLU) + BatchNorm + Dropout (0.5)** – Further refines features.  

9. **Output Layer**:  
   - **Dense (26, Softmax)** – Produces probability distribution across 26 character classes.  

This structure balances **deep feature extraction** with **regularization** (Dropout + BatchNorm) to improve generalization.

---

### Training & Inference
1. **Training**:
   - Run `ModelHandwritingComplete.ipynb`.  
   - Trains the CNN and saves the model as `modelhandwritingfinal2.keras`.  

2. **Inference**:
   - Load the pretrained model.  
   - Draw a character in the canvas.  
   - The model outputs the predicted letter along with class probabilities.  

---

## 📊 Results

- **Final Training Accuracy**: ~98%  
- **Validation Accuracy**: ~96%  
- **Test Accuracy**: ~95%  

The model shows strong generalization, but accuracy may drop on noisier, real-world handwritten inputs (e.g., messy or stylized writing).  

Example notebook outputs show interactive predictions directly from user-drawn letters.

---

## 🛠️ How to Run

### Option A: Train from Scratch
1. Download dataset from [Kaggle](https://www.kaggle.com/datasets/sachinpatel21/az-handwritten-alphabets-in-csv-format).  
2. Open `ModelHandwritingComplete.ipynb`.  
3. Run all cells to train → model saved as `modelhandwritingfinal2.keras`.  
4. Use the canvas to draw and test predictions.  

### Option B: Use Pretrained Model
1. Ensure `ModelHandwritingComplete.ipynb` and `modelhandwritingfinal2.keras` are in the same folder.  
2. Run the final notebook cells to launch the canvas.  
3. Draw letters A–Z and see predictions instantly.  

---

## 📦 Repository Structure
```
├── ModelHandwritingComplete.ipynb   # Notebook: preprocessing, model, training, canvas
├── modelhandwritingfinal2.keras     # Pretrained CNN model
├── README.md                        # Documentation
└── .gitignore
```

---

## 📌 Notes & Future Work
- **Quick Testing**: Use the pretrained model without retraining.  
- **Canvas Interface**: Provides intuitive, real-time evaluation.  
- **Possible Extensions**:
  - Add **data augmentation** (rotations, shear, noise) for more robustness.  
  - Experiment with **transfer learning** (e.g., ResNet, MobileNet).  
  - Enhance outputs with **confidence visualization** (top-k predictions).  

## Example Input
### Below is an example of an input from the user.
<img width="350" alt="Screenshot 2024-08-02 at 1 18 50 AM" src="https://github.com/user-attachments/assets/3bbc019e-ba72-4e38-b376-2f6bf668dee6">

## Example Output
### Below is an example of the model output in response to the user input.
<img width="350" alt="Screenshot 2024-08-02 at 1 18 55 AM" src="https://github.com/user-attachments/assets/4f33ee75-f85e-4006-98e0-ef48c91e079f">
