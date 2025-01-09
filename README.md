# Text-Straightening Project

This project is aimed at automatically detecting and straightening skewed text in images. It utilizes various computer vision techniques to preprocess, detect contours, fit lines, and straighten the text for better readability and accurate Optical Character Recognition (OCR).

## Features

- **Image Preprocessing**: Loads, resizes, and normalizes images for further processing.
- **Contour Detection**: Detects contours within an image, filtering out small noise to focus on the relevant text regions.
- **Line Fitting**: Fits a line to the detected contours, calculating the rotation angle required to straighten the image.
- **Text Straightening**: Rotates the image to correct any skew, aligning the text horizontally.
- **OCR**: Uses EasyOCR to extract text from the straightened image.

## Requirements

The following libraries are required to run this project:

- Python 3.x
- OpenCV (`cv2`)
- NumPy
- Pillow (`PIL`)
- EasyOCR
- Matplotlib
- SciPy (for spline interpolation)

You can install the dependencies via pip:

```bash
pip install opencv-python numpy pillow easyocr matplotlib scipy
```

## Usage

1. **Image Preprocessing and Contour Detection**:
   The image is first preprocessed, including resizing and normalization. Contours are then detected in the image, and small contours (such as noise) are filtered out.

2. **Line Fitting**:
   A line is fitted to the bottom points of each detected contour, which is used to calculate the angle of rotation for text alignment.

3. **Text Straightening**:
   The image is rotated based on the calculated angle to straighten the text.

4. **OCR**:
   Once the image is straightened, OCR is performed using the EasyOCR library, which extracts the text.

### Example Usage

```python
# Load and preprocess image
image_path = 'path_to_image.png'
image = cv2.imread(image_path)

# Perform text straightening
straightened_image, marked_image = straighten_text(image)

# Display results
import matplotlib.pyplot as plt
plt.figure(figsize=(16, 8))

# Original Image
plt.subplot(131), plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
plt.title('Original Image'), plt.axis('off')

# Image with marked points and fitted line
plt.subplot(132), plt.imshow(cv2.cvtColor(marked_image, cv2.COLOR_BGR2RGB))
plt.title('Marked Points and Fitted Line'), plt.axis('off')

# Straightened Image
plt.subplot(133), plt.imshow(cv2.cvtColor(straightened_image, cv2.COLOR_BGR2RGB))
plt.title('Straightened Text'), plt.axis('off')

plt.tight_layout()
plt.show()
```

## Testing with OCR

Once the image is straightened, you can use EasyOCR to detect the text:

```python
result = perform_ocr(straightened_image)
```

This will return the detected text and confidence scores.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---
