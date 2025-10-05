# Shape Detection: Circle vs Rectangle
Task CV-1-30 for NSU "Computer Vision" course

## Task Description
Detect and classify geometric shapes (circles, rectangles, others) on an image using contour analysis and shape approximation.  
Combines external modules from **CV-1-05** (contour detection) and **CV-1-24** (shape identification).

## Features
- **Contour Detection:** Uses `counting_contours` (from CV-1-05) for preprocessed edge and area-based contour extraction.  
- **Shape Classification:** Uses `ShapeDetector` (from CV-1-24) with an additional circularity metric.  
- **Flexible Input:** Works both with user-provided and built-in (`skimage.data.coins`) images.  
- **Visualization:** Draws contours on the image:
  - 🟢 Green — circles  
  - 🔵 Blue — rectangles/squares  
- **Error Handling:** Verifies file existence and correct input format.  
- **Parameterization:** Adjustable thresholds for different image conditions.

## Functions

### `classify_contours(contours, circularity_threshold=0.8)`
Classifies contours into circles, rectangles, or others based on circularity and shape approximation.

**Parameters:**
- `contours` (list): Contours from `counting_contours`.
- `circularity_threshold` (float): Threshold for circularity to consider a shape a circle (default: 0.8).

**Returns:**
- Tuple of three lists: `(circles, rectangles, others)`.

### `draw_contours(image, contours, color)`
Draws contours of a specific class on the image.

**Parameters:**
- `image` (ndarray): Input image (grayscale or color).
- `contours` (list): List of contours to draw.
- `color` (tuple): BGR color for drawing.

**Returns:**
- Image with contours drawn.

### `main()`
Main execution script. Prompts the user for an image path or uses `skimage.data.coins` as default.  
Performs contour detection, classification, and visualization.

**Features:**
- Interactive console input for image path.  
- Parameterized contour detection for user or built-in image.  
- Error handling for invalid or missing files.  
- Saves output to `data/result.png`.

## Running the Demo
```bash
python datect_shapes.py
```

**Example Output:**
```bash
Print the image path (Enter for 'coins'):
data/1.png
Processing user image...
Countours found: 10
Circles: 2, Rectangles: 4, Others: 4
Result saved: data/result.png
```

Result image will appear in `data/result.png`.

## Adjustable Parameters
The quality of classification depends on adjusting these parameters inside `main()` and `counting_contours()`:

| Parameter | Typical Values | Description |
|------------|----------------|--------------|
| `canny1`, `canny2` | 50–150 (coins), 100–255 (color) | Canny edge detection thresholds |
| `thresh_min`, `thresh_max` | 127–255 | Binary threshold range |
| `area_min`, `area_max` | 200–5000 or 500–20000 | Minimum and maximum contour area |
| `circularity_threshold` | 0.8–0.85 | Circle detection sensitivity |

> **Note:** Optimal values vary across images. Try adjusting thresholds to achieve stable results.

## Dependencies
- `opencv-python` 
- `numpy`
- `scikit-image`

Install dependencies:
```bash
pip install opencv-python numpy scikit-image
```

## Implementation Details
- Integrates **CV-1-05** (`counting_contours`) and **CV-1-24** (`ShapeDetector`) external modules.  
- Combines geometric (area, circularity) and approximative (vertex count) analysis.  
- Supports grayscale and color images.  
- Includes file validation and exception handling for robustness.

## Materials
- [OpenCV Documentation](https://docs.opencv.org/4.x/)
- [CV-1-05: Contour Detection](https://github.com/cyberpsychozz/Project-task-1-CV-01-05-)
- [CV-1-24: Shape Detector](https://github.com/DrPAHAN/Mironenko_Pavel_IIR/tree/main/block_1)


---
*Tested on coins dataset and generated geometric test images (rectangles, circles, mixed shapes).*
