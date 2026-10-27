# Histogram Equalization Using OpenCV (Grayscale & Color Images)

---

## Aim

To write a Python program using OpenCV to perform histogram equalization on both grayscale and color images to enhance image contrast and brightness.

The program performs the following operations:

- Read and display a grayscale image  
- Plot histogram of the grayscale image  
- Apply histogram equalization on grayscale image  
- Read and display a color image  
- Plot histogram of B, G, R channels  
- Convert image to HSV color space  
- Apply histogram equalization on the Value (V) channel  
- Convert the enhanced image back to BGR format  
- Display original and enhanced images with histograms  

---

## Software Used

- Anaconda – Python 3.7  
- Jupyter Notebook / VS Code  
- OpenCV (`cv2`)  
- NumPy  
- Matplotlib  

---

## Algorithm

### Step 1:
Import the required libraries: OpenCV, NumPy, and Matplotlib.

### Step 2:
Read the image `parrot.jpg` in grayscale format.

### Step 3:
Display the grayscale image and plot its histogram.

### Step 4:
Apply histogram equalization using `cv2.equalizeHist()` to enhance contrast.

### Step 5:
Display original grayscale image, its histogram, enhanced image, and its histogram using a 2 × 2 grid.

### Step 6:
Read the same image in color format.

### Step 7:
Split the image into B, G, R channels and plot their histograms.

### Step 8:
Convert the image from BGR to HSV color space.

### Step 9:
Apply histogram equalization on the V (Value) channel.

### Step 10:
Merge the channels and convert the image back to BGR format.

### Step 11:
Display original color image, histogram, enhanced image, and enhanced histogram using a 2 × 2 grid.

---

## Program

### Developed By:
**Name: INDHUJA.K**

### Register No: 212225040133

## Program
## 1. Import the required libraries and read the grayscale image.
```
import cv2
import numpy as np
import matplotlib.pyplot as plt

img_gray = cv2.imread('scenery.jpeg', cv2.IMREAD_GRAYSCALE)

if img_gray is None:
    print("Image not found")
else:
    plt.imshow(img_gray, cmap='gray')
    plt.title('Original Grayscale Image')
    plt.axis('off')
    plt.show()
```

<img width="568" height="497" alt="image" src="https://github.com/user-attachments/assets/90345a99-7dd0-4929-96d9-d115b43b7dba" />

## 2. Plot the histogram of the grayscale image.
```
plt.hist(img_gray.ravel(), bins=256, range=[0, 256], color='gray')
plt.title('Histogram of Original Grayscale Image')
plt.xlabel('Pixel Intensity')
plt.ylabel('Frequency')
plt.show()
```
<img width="748" height="558" alt="image" src="https://github.com/user-attachments/assets/18a3a0b4-b70f-4e27-a048-cbdccda10ea2" />

## 3. Apply histogram equalization.
```
equalized_gray = cv2.equalizeHist(img_gray)
```
## 4. Display the histogram of the equalized image.
```
plt.hist(equalized_gray.ravel(), bins=256, range=[0, 256], color='gray')
plt.title('Histogram of Equalized Grayscale Image')
plt.xlabel('Pixel Intensity')
plt.ylabel('Frequency')
plt.show()
```
<img width="793" height="558" alt="image" src="https://github.com/user-attachments/assets/58aae172-c19c-4428-b144-ead554826414" />

## 5. Display the equalized grayscale image.
```
plt.imshow(equalized_gray, cmap='gray')
plt.title('Equalized Grayscale Image')
plt.axis('off')
plt.show()
```
<img width="580" height="501" alt="image" src="https://github.com/user-attachments/assets/a81882dc-efed-4775-a513-fa9635104d17" />

## 6. Read the image in color mode and convert to HSV.
```
img_color = cv2.imread('scenery.jpeg')

if img_color is None:
    print("Image not found")
else:
    img_rgb = cv2.cvtColor(img_color, cv2.COLOR_BGR2RGB)
    img_hsv = cv2.cvtColor(img_color, cv2.COLOR_BGR2HSV)

    b, g, r = cv2.split(img_color)

    plt.figure(figsize=(10, 4))
    plt.hist(b.ravel(), bins=256, range=[0, 256], color='blue', alpha=0.5)
    plt.hist(g.ravel(), bins=256, range=[0, 256], color='green', alpha=0.5)
    plt.hist(r.ravel(), bins=256, range=[0, 256], color='red', alpha=0.5)
    plt.title('Histogram of B, G, R Channels')
    plt.xlabel('Pixel Intensity')
    plt.ylabel('Frequency')
    plt.show()
```
<img width="1161" height="481" alt="image" src="https://github.com/user-attachments/assets/93c05ffa-4682-4bbd-a030-784276e7e883" />

## 7. Apply histogram equalization to the V channel.
```
h, s, v = cv2.split(img_hsv)

v_equalized = cv2.equalizeHist(v)

img_hsv_equalized = cv2.merge((h, s, v_equalized))
```
## 8. Convert the enhanced HSV image back to BGR.
```
equalized_color = cv2.cvtColor(
    img_hsv_equalized, cv2.COLOR_HSV2BGR
)

equalized_rgb = cv2.cvtColor(
    equalized_color, cv2.COLOR_BGR2RGB
)
```
## 9. Display the original and equalized color images.
```
plt.figure(figsize=(10, 5))

plt.subplot(1, 2, 1)
plt.imshow(img_rgb)
plt.title('Original Color Image')
plt.axis('off')

plt.subplot(1, 2, 2)
plt.imshow(equalized_rgb)
plt.title('Equalized Color Image')
plt.axis('off')

plt.tight_layout()
plt.show()
```
<img width="1237" height="542" alt="image" src="https://github.com/user-attachments/assets/417d6a79-9b78-44c9-840e-fa8564cb93af" />

## 10. Display the original and equalized images along with their histograms.
```
plt.figure(figsize=(12, 10))

plt.subplot(2, 2, 1)
plt.imshow(img_gray, cmap='gray')
plt.title('Original Grayscale Image')
plt.axis('off')

plt.subplot(2, 2, 2)
plt.hist(img_gray.ravel(), bins=256, range=[0, 256], color='gray')
plt.title('Original Grayscale Histogram')

plt.subplot(2, 2, 3)
plt.imshow(equalized_gray, cmap='gray')
plt.title('Equalized Grayscale Image')
plt.axis('off')

plt.subplot(2, 2, 4)
plt.hist(equalized_gray.ravel(), bins=256, range=[0, 256], color='gray')
plt.title('Equalized Grayscale Histogram')

plt.tight_layout()
plt.show()

plt.figure(figsize=(12, 8))

plt.subplot(2, 2, 1)
plt.imshow(img_rgb)
plt.title('Original Color Image')
plt.axis('off')

plt.subplot(2, 2, 2)
for channel, color in zip(cv2.split(img_color), ['blue', 'green', 'red']):
    plt.hist(channel.ravel(), bins=256, range=[0, 256],
             color=color, alpha=0.4)
plt.title('Original BGR Histogram')

plt.subplot(2, 2, 3)
plt.imshow(equalized_rgb)
plt.title('Equalized Color Image')
plt.axis('off')

plt.subplot(2, 2, 4)
for channel, color in zip(cv2.split(equalized_color), ['blue', 'green', 'red']):
    plt.hist(channel.ravel(), bins=256, range=[0, 256],
             color=color, alpha=0.4)
plt.title('Equalized BGR Histogram')

plt.tight_layout()
plt.show()
```
<img width="902" height="755" alt="image" src="https://github.com/user-attachments/assets/d9ed1958-b5fd-40fb-981b-acf5b72d443a" />
<img width="911" height="657" alt="image" src="https://github.com/user-attachments/assets/8f6dc15f-f863-4612-bea3-d7fb65052772" />

### Grayscale Histogram Equalization

- Original grayscale image is displayed  
- Histogram of original grayscale image is plotted  
- Enhanced image after histogram equalization is displayed  
- Histogram of enhanced grayscale image shows improved contrast  

### Color Image Histogram Equalization

- Original color image is displayed  
- Histogram of B, G, R channels is plotted  
- Enhanced image after HSV-based equalization is displayed  
- Histogram of enhanced image shows better intensity distribution  

---

## Result

Thus, histogram equalization is successfully performed on both grayscale and color images using OpenCV. The contrast and brightness of the images are significantly improved, enhancing visual quality and feature visibility.
