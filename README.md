# EXP - 4 GEOMETRIC TRANSFORMATIONS USING OPEN CV

---

## Aim:

To write a Python program using OpenCV to perform various geometric transformations on an image.

The program performs the following operations:

- Image Translation  
- Image Scaling (Resizing)  
- Image Shearing  
- Image Reflection (Flipping)  
- Image Rotation  

---

##  Software Used:

- Anaconda – Python 3.7  
- Jupyter Notebook / VS Code  
- OpenCV (`cv2`)  
- NumPy  
- Matplotlib  

---

##  Algorithm:

### Step 1:
Import the required libraries: OpenCV, NumPy, and Matplotlib.

### Step 2:
Read the input image in color mode.

### Step 3: Image Translation
- Create a translation matrix to shift the image  
- Move the image 50 pixels to the right and 80 pixels down  
- Apply transformation using `cv2.warpAffine()`  
- Display original and translated images  

### Step 4: Image Scaling
- Resize the image to 0.5× (downscale)  
- Resize the image to 2× (upscale)  
- Use `cv2.resize()`  
- Display original, downscaled, and upscaled images  

### Step 5: Image Shearing
- Create transformation matrices for:
  - Horizontal shearing  
  - Vertical shearing  
- Apply transformations using `cv2.warpAffine()`  
- Display original and sheared images  

### Step 6: Image Reflection
- Perform flipping using `cv2.flip()`:
  - Horizontal reflection  
  - Vertical reflection  
  - Both axes  
- Display all reflected images  

### Step 7: Image Rotation
- Create rotation matrices for:
  - 45° rotation  
  - 90° rotation  
- Use `cv2.getRotationMatrix2D()` and `cv2.warpAffine()`  
- Display original and rotated images  

---

##  Program:

### Developed By:
**Name:** R P Loshini

**Register No:** 212225230155 

#### Image Translation
```
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Step 2: Read the input image in color mode and convert BGR to RGB for display
image_path = r"C:\Users\acer\DIPT\baseball.jpg"
img_bgr = cv2.imread(image_path)
img_rgb = cv2.cvtColor(img_bgr, cv2.COLOR_BGR2RGB)
h, w = img_rgb.shape[:2]

# Step 3: Image Translation
# Create translation matrix M = [[1, 0, tx], [0, 1, ty]] to move 50px right and 80px down
M_translate = np.float32([
    [1, 0, 50],
    [0, 1, 80]
])

# Apply transformation using cv2.warpAffine()
translated_img = cv2.warpAffine(img_rgb, M_translate, (w, h))

# Display original and translated images
fig, axes = plt.subplots(1, 2, figsize=(10, 5))
axes[0].imshow(img_rgb)
axes[0].set_title("Original Image")
axes[0].axis('off')

axes[1].imshow(translated_img)
axes[1].set_title("Translated Image (50px Right, 80px Down)")
axes[1].axis('off')

plt.tight_layout()
plt.show()
```

#### Image Scaling
```
# Step 4: Image Scaling
# Resize image to 0.5x (downscale) and 2x (upscale) using cv2.resize()
downscaled_img = cv2.resize(img_rgb, (0, 0), fx=0.5, fy=0.5, interpolation=cv2.INTER_AREA)
upscaled_img = cv2.resize(img_rgb, (0, 0), fx=2.0, fy=2.0, interpolation=cv2.INTER_CUBIC)

# Display original, downscaled, and upscaled images
fig, axes = plt.subplots(1, 3, figsize=(12, 4))
axes[0].imshow(img_rgb)
axes[0].set_title("Original Image")
axes[0].axis('off')

axes[1].imshow(downscaled_img)
axes[1].set_title("Downscaled Image (0.5x)")
axes[1].axis('off')

axes[2].imshow(upscaled_img)
axes[2].set_title("Upscaled Image (2x)")
axes[2].axis('off')

plt.tight_layout()
plt.show()
```

#### Image Shearing
```
# Step 5: Image Shearing
# Horizontal Shearing Matrix
M_shear_x = np.float32([
    [1, 0.2, 0],
    [0, 1, 0]
])

# Vertical Shearing Matrix
M_shear_y = np.float32([
    [1, 0, 0],
    [0.2, 1, 0]
])

# Apply transformations using cv2.warpAffine()
sheared_x = cv2.warpAffine(img_rgb, M_shear_x, (int(w * 1.2), h))
sheared_y = cv2.warpAffine(img_rgb, M_shear_y, (w, int(h * 1.2)))

# Display original, horizontal sheared, and vertical sheared images
fig, axes = plt.subplots(1, 3, figsize=(12, 4))
axes[0].imshow(img_rgb)
axes[0].set_title("Original Image")
axes[0].axis('off')

axes[1].imshow(sheared_x)
axes[1].set_title("Horizontally Sheared Image")
axes[1].axis('off')

axes[2].imshow(sheared_y)
axes[2].set_title("Vertically Sheared Image")
axes[2].axis('off')

plt.tight_layout()
plt.show()
```

#### Image Reflection/Flipping
```
# Step 6: Image Reflection
# Perform flipping using cv2.flip(): 1 = Horizontal, 0 = Vertical, -1 = Both axes
flipped_h = cv2.flip(img_rgb, 1)
flipped_v = cv2.flip(img_rgb, 0)
flipped_both = cv2.flip(img_rgb, -1)

# Display all reflected images
fig, axes = plt.subplots(2, 2, figsize=(10, 8))

axes[0, 0].imshow(img_rgb)
axes[0, 0].set_title("Original Image")
axes[0, 0].axis('off')

axes[0, 1].imshow(flipped_h)
axes[0, 1].set_title("Horizontally Flipped")
axes[0, 1].axis('off')

axes[1, 0].imshow(flipped_v)
axes[1, 0].set_title("Vertically Flipped")
axes[1, 0].axis('off')

axes[1, 1].imshow(flipped_both)
axes[1, 1].set_title("Both-Axis Flipped")
axes[1, 1].axis('off')

plt.tight_layout()
plt.show()
```

#### Image Rotation
```
# Step 7: Image Rotation
center = (w // 2, h // 2)

# Create rotation matrices using cv2.getRotationMatrix2D()
M_rot_45 = cv2.getRotationMatrix2D(center, 45, 1.0)
M_rot_90 = cv2.getRotationMatrix2D(center, 90, 1.0)

# Apply rotation using cv2.warpAffine()
rotated_45 = cv2.warpAffine(img_rgb, M_rot_45, (w, h))
rotated_90 = cv2.warpAffine(img_rgb, M_rot_90, (w, h))

# Display original and rotated images
fig, axes = plt.subplots(1, 3, figsize=(12, 4))
axes[0].imshow(img_rgb)
axes[0].set_title("Original Image")
axes[0].axis('off')

axes[1].imshow(rotated_45)
axes[1].set_title("45° Rotated Image")
axes[1].axis('off')

axes[2].imshow(rotated_90)
axes[2].set_title("90° Rotated Image")
axes[2].axis('off')

plt.tight_layout()
plt.show()
```

---

##  Output:

### Image Translation
- Original image is displayed  
- Translated image (shifted right and down) is displayed
<img width="979" height="327" alt="image" src="https://github.com/user-attachments/assets/9d76e73e-03cd-4ce7-ad3a-f70670bc3226" />


### Image Scaling
- Original image is displayed  
- Downscaled image (0.5×) is displayed  
- Upscaled image (2×) is displayed  
<img width="1088" height="244" alt="image" src="https://github.com/user-attachments/assets/a41482a9-f569-4c4c-87d3-eb44f978eb46" />


### Image Shearing
- Original image is displayed  
- Horizontally sheared image is displayed  
- Vertically sheared image is displayed  
<img width="1093" height="285" alt="image" src="https://github.com/user-attachments/assets/df69ca38-7852-43cc-8e30-314fae8ca767" />


### Image Reflection
- Original image is displayed  
- Horizontally flipped image is displayed  
- Vertically flipped image is displayed  
- Both-axis flipped image is displayed  
<img width="976" height="695" alt="image" src="https://github.com/user-attachments/assets/14de0502-da7c-405f-bdef-e3748321cc63" />


### Image Rotation
- Original image is displayed  
- 45° rotated image is displayed  
- 90° rotated image is displayed  
<img width="1081" height="242" alt="image" src="https://github.com/user-attachments/assets/0f059218-7e3d-49d7-b383-4079fedb9f62" />


---

##  Result:

Thus, various geometric transformations such as translation, scaling, shearing, reflection, and rotation are successfully performed using OpenCV. These transformations demonstrate how images can be spatially manipulated for different computer vision applications.
