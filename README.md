# EXP-6 EDGE DETECTION
---

## Aim

To implement a basic edge detection pipeline using OpenCV by completing missing code segments at specified locations.

---

## Learning Objective

* Understand each stage of image processing
* Learn how to build a complete computer vision pipeline
* Practice writing code in guided sections

**Important Instruction:**

👉 Write code **ONLY in places marked as `# Your Code Here`**  
👉 Do NOT modify any other part of the code

---

## Software Used

* Anaconda – Python 3.7
* Jupyter Notebook / VS Code
* OpenCV (cv2)
* NumPy
* Matplotlib

---

## Algorithm & Explanation

---

### Step 1: Import Libraries

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

---

### Step 2: Read the Image

```python
# Read the image using OpenCV

###
# Your Code Here
###

image = cv2.imread('Qn_7_.jpg')
```

---

### Step 3: Convert to Grayscale

```python
# Convert to grayscale.

###
# Your Code Here
###

gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
```

---

### Step 4: Display Images

```python
plt.figure(figsize=(10,5))

###
# Your Code Here
###

plt.subplot(1, 2, 1)
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis("off")

plt.subplot(1, 2, 2)
plt.imshow(gray_image, cmap="gray")
plt.title("Grayscale Image")
plt.axis("off")

plt.show()
```

---

### Step 5: Thresholding

```python
# Apply thresholding

threshold = cv2.threshold(
    gray_image,
    127,
    255,
    cv2.THRESH_BINARY
)[1]

plt.imshow(threshold, cmap="gray")
plt.title("Thresholded Image")
plt.axis("off")
plt.show()
```

---

### Step 6: Region of Interest (ROI)

```python
# ROI masking already provided
height, width = threshold.shape

# Define a broad polygonal region of interest
roi_vertices = np.array([[
    (0, height),
    (0, int(height * 0.45)),
    (width, int(height * 0.45)),
    (width, height)
]], dtype=np.int32)

roi_mask = np.zeros_like(threshold)
cv2.fillPoly(roi_mask, roi_vertices, 255)
roi_image = cv2.bitwise_and(threshold, roi_mask)
```

---

### Step 7: Edge Detection (Canny)

```python
# Perform Edge Detection

###
# Your Code Here
###

edges = cv2.Canny(
    gray_image,
    50,
    150
)

plt.imshow(edges, cmap="gray")
plt.title("Canny Edge Detection")
plt.axis("off")
plt.show()
```

---

### Step 8: Gaussian Blur

```python
# Apply Gaussian Blur

###
# Your Code Here
###

blurred = cv2.GaussianBlur(
    edges,
    (5, 5),
    0
)

plt.imshow(blurred, cmap="gray")
plt.title("Smoothed Image")
plt.axis("off")
plt.show()
```

---

### Step 9: Hough Transform

```python
# Detect lines using Hough Transform

###
# Your Code Here
###

lines = cv2.HoughLinesP(
    blurred,
    1,
    np.pi / 180,
    threshold=100,
    minLineLength=50,
    maxLineGap=10
)
```

---

### Step 10: Edge Detection Logic

```python
# Already implemented
# Step 5: Detect lines using HoughLinesP
lines = cv2.HoughLinesP(
    edges,
    1,
    np.pi / 180,
    100,
    minLineLength=50,
    maxLineGap=10
)
# Step 6: Using a for loop, draw the lines on the original image using the detected coordinates
# The lines variable contains the endpoints of the detected lines
if lines is not None:
    print(lines.shape)
    print(lines[:5])
    for line in lines:
        x1, y1, x2, y2 = line
        cv2.line(image, (x1, y1), (x2, y2), (0, 255, 0), 2)
# Display the result of Hough Transform (Image with lines)
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))  # Image with lines drawn
plt.title("Result of Hough Transform")
plt.axis('off')

```

---

## Expected Output
### Original image

<img width="1004" height="543" alt="image" src="https://github.com/user-attachments/assets/94a54825-9f12-4366-9644-22fb8133781d" />

  
### Grayscale image
<img width="879" height="559" alt="image" src="https://github.com/user-attachments/assets/393de772-5383-427f-a54b-8235f2182cc1" />

### Thresholded image

<img width="764" height="768" alt="image" src="https://github.com/user-attachments/assets/92077411-5b0a-4830-a93e-de8d93f62a7d" />


### ROI masked image
<img width="496" height="764" alt="image" src="https://github.com/user-attachments/assets/93f27bf1-c69b-49e0-9772-b5a7073186f0" />

### Edge detected image

<img width="770" height="405" alt="image" src="https://github.com/user-attachments/assets/b71b0780-041f-4899-985c-9fd1b817b907" />

### Smoothed image

<img width="497" height="764" alt="image" src="https://github.com/user-attachments/assets/ac0ada69-5181-43a1-9dfa-b9d2f1dd28d2" />

### Detected lines

```
(373, 4)
[[146 732 146  57]
 [148 769 148 100]
 [152 774 152  58]
 [158 771 158  59]
 [ 94 575  98 330]]
```

### Final edge detection output

<img width="972" height="431" alt="image" src="https://github.com/user-attachments/assets/223d494f-aad6-4a57-9399-9766539af683" />


---

## Instructions

* Fill ONLY in `# Your Code Here` sections
* Do NOT change existing code
* Run step-by-step
* Verify outputs

---

## Result

Thus, the edge detection pipeline is successfully implemented by completing the missing code sections. The system detects and highlights edges and lines effectively.

---
