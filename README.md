## Forams Classification 2025 - 1st Place Solution

Kaggle competition page:<br>
https://www.kaggle.com/competitions/forams-classification-2025

<br>
<img src="https://github.com/vbookshelf/Forams-2025-Kaggle-Comp-Solution/blob/main/images/labelled_foram_00002.jpg" height="300"></img>
<i>300x600 RGB image of a foram<br>
  Top: Volume Rendering<br>
  Bottom: Surface rendering</i><br>
<br>

### Goal

Classify volumetric images of forams into one of 15 classes (14 foram species and 1 "unknown" class).

### Data

Training data:
- 210 labeled volumes
- 210 RGB images of the labeled volumes - sample shown above. Each image shows a volume rendering and a surface rendering.
- No labeled examples of the "unknown" class were provided.

Test data:
- 18,216 unlabeled volumes
- 18,216 unlabeled RGB images

### Solution Overview
- Use only the 210 RGB images for model training and validation.
- Train only on 14 classes i.e. don't consider the "unknown class" during model training.
- Model: swin_large_patch4_window12_384 (from the Timm package)
- Use heavy image augmentation to reduce overfitting and improve the chances that the model will generalize well.
- Resize images from 300x300 to 384x384 to match the input size that the Swin model needs.

Approach:<br>
- Step 1: Train five folds using the volume rendering (top half of image) (Exp23)
- Step 2: Train five folds using the surface rendering (bottom half of image) (Exp24)
- Step 3: Ensemble (average) the test set predictions of all 10 fold models that were trained in steps 1 and 2. (Exp 26)
- Step 4: Determine the "unknown" class (class 14) based on the predicted probabilities from step 3. If a probability is <= 0.25 then assign that test example to the "unknown" class (class 14).

### Leaderboard scores
Step 1: Train five folds using volume rendering images (Exp23)<br>
Public LB: 0.78425<br>
Private LB:<br>

Step 2: Train five folds using surface rendering images (Exp24)<br>
Public LB: 0.70453<br>
Private LB:<br>

Step 3: Average the test set predictions of all 10 fold models (Exp 26) <i>[Selected submission]</i><br> 
Public LB: 0.83469<br>
Private LB:<br>

Step 4: Determine the "unknown" class (class 14) based on prediction probability scores (Exp27) <i>[Selected submission]</i><br>
Public LB: 0.83469<br>
Private LB:<br>

### Jupyter notebooks
Step 1: Train five folds using volume rendering images (Exp23)<br>
https://github.com/vbookshelf/Forams-2025-Kaggle-Comp-Solution/blob/main/jupyter-notebooks/exp23-forams-train-models-using-volume-rendering-image.ipynb

Step 2: Train five folds using surface rendering images (Exp24)<br>
https://github.com/vbookshelf/Forams-2025-Kaggle-Comp-Solution/blob/main/jupyter-notebooks/exp24-forams-train-models-using-surface-rendering-image.ipynb

Step 3: Average the test set predictions of all 10 fold models (Exp26)<br>
https://github.com/vbookshelf/Forams-2025-Kaggle-Comp-Solution/blob/main/jupyter-notebooks/exp26-forams-ensemble-exp23-and-exp24-preds.ipynb

Step 4: Determine the "unknown" class (class 14) based on the predicted probabilities in step 3 (Exp27)<br>
https://github.com/vbookshelf/Forams-2025-Kaggle-Comp-Solution/blob/main/jupyter-notebooks/exp27-forams-identify-class-14-using-exp26-probs.ipynb
