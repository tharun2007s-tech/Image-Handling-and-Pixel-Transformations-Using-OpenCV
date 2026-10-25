# Image-Handling-and-Pixel-Transformations-Using-OpenCV

## AIM
Write a Python program using OpenCV that reads and displays an image, adjusts brightness and contrast, splits and merges color channels, and performs bitwise operations.

## Software Required
- Anaconda – Python 3.7
- Jupyter Notebook

## Algorithm

**Step 1:** Read the image using OpenCV and display it.

**Step 2:** Print the image width, height, and number of channels.

**Step 3:** Convert the image to grayscale and save it as a PNG file.

**Step 4:** Crop the image, resize it by a factor of 2, and flip it horizontally.

**Step 5:** Read the image and add text and a magenta rectangle.

**Step 6:** Adjust brightness by creating brighter and darker images.

**Step 7:** Modify contrast using scaling factors of 0.8, 1.1, and 1.2.

**Step 8:** Split and display the B, G, and R channels, then merge them.

**Step 9:** Convert the image to HSV, split the H, S, and V channels, and merge them.

**Step 10:** Perform bitwise operations and display the results.

## Program Developed By
- **Name:** [Your Name Here]
- **Register Number:** [Your Register Number Here]

# Ex. No. 01

### 1. Read the image (`Cat.webp`) as a grayscale image.

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

img_gray = cv2.imread('Cat.webp', cv2.IMREAD_GRAYSCALE)

if img_gray is None:
    raise FileNotFoundError("Cat.webp not found")
```

### 2. Print the image width, height, and channel.

```python
height, width = img_gray.shape

print("Width:", width)
print("Height:", height)
print("Channel: 1")
```

### 3. Display the image using Matplotlib `imshow()`.

```python
plt.imshow(img_gray, cmap='gray')
plt.title("Grayscale Cat Image")
plt.axis('off')
plt.show()
```

### 4. Save the image as a PNG file using OpenCV `imwrite()`.

```python
cv2.imwrite('Cat_Gray.png', img_gray)
```

### 5. Read the saved image as a color image using `cv2.cvtColor()`.

```python
gray_saved = cv2.imread('Cat_Gray.png', cv2.IMREAD_GRAYSCALE)

color_img = cv2.cvtColor(gray_saved, cv2.COLOR_GRAY2BGR)
```

### 6. Display the color image and print its width, height, and channel.

```python
height, width, channel = color_img.shape

print("Width:", width)
print("Height:", height)
print("Channels:", channel)

plt.imshow(cv2.cvtColor(color_img, cv2.COLOR_BGR2RGB))
plt.title("Color Image")
plt.axis('off')
plt.show()
```

### 7. Crop the image to extract a specific part of the cat.

```python
height, width = img_gray.shape

cropped_img = img_gray[
    height // 4:3 * height // 4,
    width // 4:3 * width // 4
]

plt.imshow(cropped_img, cmap='gray')
plt.title("Cropped Cat Image")
plt.axis('off')
plt.show()
```

### 8. Resize the cropped image by a factor of 2x.

```python
resized_img = cv2.resize(
    cropped_img,
    None,
    fx=2,
    fy=2,
    interpolation=cv2.INTER_LINEAR
)

plt.imshow(resized_img, cmap='gray')
plt.title("Resized Image")
plt.axis('off')
plt.show()
```

### 9. Flip the cropped/resized image horizontally.

```python
flipped_img = cv2.flip(resized_img, 1)

plt.imshow(flipped_img, cmap='gray')
plt.title("Horizontally Flipped Image")
plt.axis('off')
plt.show()
```

### 10. Read the image for annotation.

```python
apollo = cv2.imread('Cat.webp')

height, width = apollo.shape[:2]
```

### 11. Add text at the bottom center of the image.

```python
text = 'Cat Image Processing'
font_face = cv2.FONT_HERSHEY_PLAIN

font_scale = 1.5
thickness = 2

text_size = cv2.getTextSize(
    text, font_face, font_scale, thickness
)[0]

text_x = (width - text_size[0]) // 2
text_y = height - 15

cv2.putText(
    apollo,
    text,
    (text_x, text_y),
    font_face,
    font_scale,
    (255, 255, 255),
    thickness,
    cv2.LINE_AA
)
```

### 12. Draw a magenta rectangle around the image.

```python
rect_color = (255, 0, 255)

cv2.rectangle(
    apollo,
    (10, 10),
    (width - 10, height - 10),
    rect_color,
    3
)
```

### 13. Display the final annotated image.

```python
apollo_rgb = cv2.cvtColor(apollo, cv2.COLOR_BGR2RGB)

plt.imshow(apollo_rgb)
plt.title("Annotated Cat Image")
plt.axis('off')
plt.show()

cv2.imwrite('Cat_Annotated.jpg', apollo)
```

### 14. Read the image (`Cat.webp`).

```python
img = cv2.imread('Cat.webp')

if img is None:
    raise FileNotFoundError("Cat.webp not found")
```

### 15. Adjust the brightness of the image.

```python
matrix_ones = np.ones(img.shape, dtype=np.float64)

matrix = (matrix_ones * 50).astype(np.uint8)
```

### 16. Create brighter and darker images.

```python
img_brighter = cv2.add(img, matrix)
img_darker = cv2.subtract(img, matrix)
```

### 17. Display the original, darker, and brighter images.

```python
plt.figure(figsize=(12, 4))

plt.subplot(1, 3, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis('off')

plt.subplot(1, 3, 2)
plt.imshow(cv2.cvtColor(img_darker, cv2.COLOR_BGR2RGB))
plt.title("Darker Image")
plt.axis('off')

plt.subplot(1, 3, 3)
plt.imshow(cv2.cvtColor(img_brighter, cv2.COLOR_BGR2RGB))
plt.title("Brighter Image")
plt.axis('off')

plt.tight_layout()
plt.show()
```

### 18. Modify the image contrast.

```python
matrix1 = np.ones(img.shape, dtype=np.float64) * 1.1
matrix2 = np.ones(img.shape, dtype=np.float64) * 1.2

img_higher1 = cv2.multiply(img.astype(np.float64), matrix1)
img_higher2 = cv2.multiply(img.astype(np.float64), matrix2)

img_higher1 = np.clip(img_higher1, 0, 255).astype(np.uint8)
img_higher2 = np.clip(img_higher2, 0, 255).astype(np.uint8)

img_lower = cv2.convertScaleAbs(img, alpha=0.8, beta=0)
```

### 19. Display the original, lower contrast, and higher contrast images.

```python
plt.figure(figsize=(12, 4))

plt.subplot(1, 3, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis('off')

plt.subplot(1, 3, 2)
plt.imshow(cv2.cvtColor(img_lower, cv2.COLOR_BGR2RGB))
plt.title("Lower Contrast")
plt.axis('off')

plt.subplot(1, 3, 3)
plt.imshow(cv2.cvtColor(img_higher2, cv2.COLOR_BGR2RGB))
plt.title("Higher Contrast")
plt.axis('off')

plt.tight_layout()
plt.show()
```

### 20. Split the image into B, G, R components and display the channels.

```python
b, g, r = cv2.split(img)

plt.figure(figsize=(12, 4))

plt.subplot(1, 3, 1)
plt.imshow(b, cmap='gray')
plt.title("Blue Channel")
plt.axis('off')

plt.subplot(1, 3, 2)
plt.imshow(g, cmap='gray')
plt.title("Green Channel")
plt.axis('off')

plt.subplot(1, 3, 3)
plt.imshow(r, cmap='gray')
plt.title("Red Channel")
plt.axis('off')

plt.tight_layout()
plt.show()
```

### 21. Merge the R, G, B components and display them with the original image.

```python
merged_img = cv2.merge([b, g, r])

plt.figure(figsize=(8, 4))

plt.subplot(1, 2, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis('off')

plt.subplot(1, 2, 2)
plt.imshow(cv2.cvtColor(merged_img, cv2.COLOR_BGR2RGB))
plt.title("Merged BGR Image")
plt.axis('off')

plt.tight_layout()
plt.show()
```

### 22. Split the image into H, S, V components and display the channels.

```python
hsv_img = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)

h, s, v = cv2.split(hsv_img)

plt.figure(figsize=(12, 4))

plt.subplot(1, 3, 1)
plt.imshow(h, cmap='gray')
plt.title("Hue")
plt.axis('off')

plt.subplot(1, 3, 2)
plt.imshow(s, cmap='gray')
plt.title("Saturation")
plt.axis('off')

plt.subplot(1, 3, 3)
plt.imshow(v, cmap='gray')
plt.title("Value")
plt.axis('off')

plt.tight_layout()
plt.show()
```

### 23. Merge the H, S, V components and display them with the original image.

```python
merged_hsv = cv2.merge([h, s, v])

merged_color = cv2.cvtColor(
    merged_hsv, cv2.COLOR_HSV2RGB
)

plt.figure(figsize=(8, 4))

plt.subplot(1, 2, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis('off')

plt.subplot(1, 2, 2)
plt.imshow(merged_color)
plt.title("Merged HSV Image")
plt.axis('off')

plt.tight_layout()
plt.show()
```

### 24. Generate a third image using bitwise operations.

```python
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

_, mask = cv2.threshold(
    gray, 127, 255, cv2.THRESH_BINARY
)

bitwise_and = cv2.bitwise_and(img, img, mask=mask)
bitwise_or = cv2.bitwise_or(img, img)
bitwise_not = cv2.bitwise_not(img)

plt.figure(figsize=(12, 4))

plt.subplot(1, 3, 1)
plt.imshow(cv2.cvtColor(bitwise_and, cv2.COLOR_BGR2RGB))
plt.title("Bitwise AND")
plt.axis('off')

plt.subplot(1, 3, 2)
plt.imshow(cv2.cvtColor(bitwise_or, cv2.COLOR_BGR2RGB))
plt.title("Bitwise OR")
plt.axis('off')

plt.subplot(1, 3, 3)
plt.imshow(cv2.cvtColor(bitwise_not, cv2.COLOR_BGR2RGB))
plt.title("Bitwise NOT")
plt.axis('off')

plt.tight_layout()
plt.show()
```

## Output
1. Grayscale and color images were read and displayed.
2. Image brightness was increased and decreased.
3. Image contrast was modified.
4. BGR and HSV channels were split and merged.
5. Bitwise AND, OR, and NOT operations were performed.

<img width="263" height="773" alt="Screenshot 2026-10-25 153737" src="https://github.com/user-attachments/assets/861d7c4e-c3d3-424e-a3c2-bee9ba7c545f" />
<img width="256" height="681" alt="Screenshot 2026-10-25 153748" src="https://github.com/user-attachments/assets/648ac75e-9619-49a9-84b9-5183129ec634" />
<img width="251" height="685" alt="Screenshot 2026-10-25 153759" src="https://github.com/user-attachments/assets/7ba9a694-13aa-427f-940d-751e41ced42e" />
<img width="852" height="655" alt="Screenshot 2026-10-25 153809" src="https://github.com/user-attachments/assets/39956de3-1574-47d7-9b9a-08f4ffd2245e" />
<img width="852" height="657" alt="Screenshot 2026-10-25 153820" src="https://github.com/user-attachments/assets/5f16f1bc-9e6e-430e-a07b-7f8e89f3b31a" />
<img width="860" height="647" alt="Screenshot 2026-10-25 153833" src="https://github.com/user-attachments/assets/cc4e29cf-41c6-4984-8c5e-3a5065da8259" />





## Result

Thus, image reading, display, cropping, resizing, flipping, annotation, brightness adjustment, contrast modification, color channel operations, and bitwise operations were performed successfully using Python and OpenCV.
