Working with images in Python can mean several things depending on your goal:

- Loading and displaying images
    
- Editing (cropping, resizing, rotating)
    
- Filtering and transformations
    
- Image processing (OpenCV)
    
- Computer vision & ML

---
## 1) Main Libraries for Working with Images

There are three major libraries:

### 1. Pillow (PIL)

Best for:

- Basic image editing
    
- Simple manipulation
    
- Easy to learn
    

Install:
```
pip install pillow
```
### 2. OpenCV

Best for:

- Computer vision
    
- Image processing
    
- Face detection
    
- Real-time camera work
    

Install:
```
pip install opencv-python
```

---
### 3. Matplotlib

Best for:

- Displaying images
    
- Visualization
    

Install:
```
pip install matplotlib
```

---
## 2) Working with Pillow (PIL)

Import:
```
from PIL import Image
```
### Open an Image
```
img = Image.open("photo.jpg")
img.show()
```
### Get Image Info
```
print(img.format)   # JPEG, PNG
print(img.size)     # (width, height)
print(img.mode)     # RGB, L (grayscale)
```
### Resize
```
resized = img.resize((300, 200))
resized.show()
```
### Rotate
```
rotated = img.rotate(90)
rotated.show()
```
### Crop
```
cropped = img.crop((left, top, right, bottom))
cropped.show()
```
Example:
```
cropped = img.crop((100, 100, 400, 400))
```
### Convert to Grayscale
```
gray = img.convert("L")
gray.show()
```
### Save Image
```
img.save("new_image.png")
```

---
## 3) Working with OpenCV

Import:
```
import cv2
```
### Read Image
```
img = cv2.imread("photo.jpg")
```
Note: `OpenCV` loads images in **BGR format**, not RGB.

### Display Image
```
cv2.imshow("Image", img)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
### Convert to Grayscale
```
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
```
### Resize
```
resized = cv2.resize(img, (300, 200))
```
### Edge Detection
```
edges = cv2.Canny(img, 100, 200)
```
### Save Image
```
cv2.imwrite("output.jpg", img)
```

---
## 4) Working with NumPy (Important Concept)

Images in Python are actually **NumPy arrays**.

Example:
```
import numpy as np
print(type(img))
```
You’ll see:
```
<class 'numpy.ndarray'>
```
This means:

- You can manipulate pixels directly
    
- You can use slicing
### Access Pixel
```
pixel = img[100, 200]
print(pixel)
```
### Change Pixel Color
```
img[100, 200] = [255, 0, 0]  # Red
```

---
## 5) Displaying with Matplotlib
```
import matplotlib.pyplot as plt
import cv2

img = cv2.imread("photo.jpg")
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

plt.imshow(img_rgb)
plt.axis("off")
plt.show()
```
We convert BGR → RGB so colors look correct.

---
## 6) Common Image Operations

### ✔ Blurring
```
blur = cv2.GaussianBlur(img, (5, 5), 0)
```
### ✔ Thresholding (Binary Image)
```
_, thresh = cv2.threshold(gray, 127, 255, cv2.THRESH_BINARY)
```
### ✔ Drawing Shapes
```
cv2.rectangle(img, (50, 50), (200, 200), (0, 255, 0), 2)
```
### ✔ Face Detection (Example)
```
face_cascade = cv2.CascadeClassifier("haarcascade_frontalface_default.xml")
faces = face_cascade.detectMultiScale(gray, 1.3, 5)
```

---
## 7) Image Formats & Modes
| Mode | Meaning                    |
| ---- | -------------------------- |
| RGB  | Red, Green, Blue           |
| BGR  | OpenCV format              |
| L    | Grayscale                  |
| RGBA | RGB + Alpha (transparency) |

---
## 8) Advanced Areas

Once you master basics, you can explore:

- Image segmentation
    
- Object detection (YOLO, TensorFlow)
    
- Image classification
    
- OCR (text extraction)
    
- Deep learning (CNNs)
    

---

## 9) Typical Workflow Example

Example: Resize all images in a folder
```
import os
from PIL import Image

folder = "images/"

for file in os.listdir(folder):
    if file.endswith(".jpg"):
        img = Image.open(folder + file)
        img = img.resize((300, 300))
        img.save("resized_" + file)
```

---
## 10) Summary

Working with images in Python includes:

- Loading images
    
- Editing (resize, crop, rotate)
    
- Converting formats
    
- Pixel manipulation
    
- Applying filters
    
- Computer vision tasks
    

Main tools:

- Pillow → Simple editing
    
- OpenCV → Advanced processing
    
- NumPy → Pixel-level control
    
- Matplotlib → Displaying images