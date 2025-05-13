## Forams Classification 2025 - 1st Place Solution

Kaggle competition page:<br>
https://www.kaggle.com/competitions/forams-classification-2025

<br>
<img src="https://github.com/vbookshelf/Forams-2025-Kaggle-Comp-Solution/blob/main/images/labelled_foram_00002.jpg" height="300"></img>
<i>300x600 RGB image of a volume<br>
  Top: Volume Rendering<br>
  Bottom: Surface rendering</i><br>
<br>

### Goal

Classify volumetric images of forams into one of 15 classes (14 foram species and 1 "unknown" class).

### Data

Training data:
- 210 labeled volumes
- 210 RGB images of the labeled volumes - sample shown above. Each image shows a volume rendering and a surface rendering.

Test data:
- 18,216 unlabeled volumes
- 18,216 unlabeled RGB images

### Solution Overview
- Use only the 210 RGB images for model training
- Model: swin_large_patch4_window12_384 (from the Timm package)
- Use heavy image augmentation to reduce overfitting and improve the chances that the model will generalize well.
- Resize images from 300x300 to 384x384 to match the input size that the Swin model needs.
- Step 1: Train five folds using the surface rendering (bottom half of image).
- Step 2: Train five folds using the volume rendering (top half of image).
- Step 3: Ensemble (average) the preds of all 10 fold models that were trained in steps 1 and 2.

### Results

### Jupyter notebooks

