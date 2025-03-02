# VRAssignment1_Rishita_MS2024014

This repository contains the code and resources for the first assignment of the Virtual Reality course. The assignment involves two main tasks:
1. **Coin Detection and Segmentation**
2. **Panorama Creation**

## Repository Structure

```
VR_Assignment1_[YourName]_[YourRollNo]/
│
├── Coin Detection/
│   ├── input_images/                  # Folder containing input images for coin detection
│   ├── detection_results/             # Folder to store coin detection and segmentation results
│   ├── visualization_results/         # Folder to store visualizations of the processing steps
│   └── coin_detection.py              # Script for coin detection and segmentation
│
├── Panorama/
│   ├── images1/                       # First set of images for panorama creation
│   ├── images2/                       # Second set of images for panorama creation
│   ├── output_folder1/                # Output folder for panorama results
│   ├── output_folder2/                # Output folder for panorama results
│   └── [6 more output folders]        # Additional output folders for panorama results
│   └── panorama_creation.py           # Script for panorama creation
│
├── README.md                          # This file
└── requirements.txt                   # List of dependencies
```

## Requirements

The following Python packages are required to run the code:
```
numpy
opencv-python
matplotlib
```

You can install these dependencies using pip:
```bash
pip install -r requirements.txt
```

## How to Run the Code

### Prerequisites

1. **Python 3.x**: Ensure you have Python 3.x installed on your system.
2. **Dependencies**: Install the required Python packages as mentioned above.

### Running the Coin Detection and Segmentation Script

1. Navigate to the Coin Detection directory:
   ```bash
   cd "Coin Detection"
   ```
2. Place the images you want to process in the `input_images` folder.
3. Run the `coin_detection.py` script:
   ```bash
   python coin_detection.py
   ```
4. The script will process the images, detect and segment coins, and save the results in the `detection_results` and `visualization_results` folders.

### Running the Panorama Creation Script

1. Navigate to the Panorama directory:
   ```bash
   cd Panorama
   ```
2. The `images1` and `images2` folders should contain the sets of images you want to stitch into panoramas.
3. Run the `panorama_creation.py` script:
   ```bash
   python panorama_creation.py
   ```
4. The script will create panoramas from the input images and save the results in the various output folders.

## Methods and Results

### Coin Detection and Segmentation

#### Methods Used

1. **Image Pre-processing**:
   - **Grayscale Conversion**: Convert the image to grayscale for easier processing.
   - **Noise Removal**: Apply Gaussian blur with kernel size (7, 7) to reduce noise.
   - **Contrast Enhancement**: Normalize pixel values to full 0-255 range for better contrast.
   - **High-Pass Filtering (HPF)**: Apply HPF to enhance edges and remove background.

2. **Edge Detection**:
   - **Marr-Hildreth Method**: Detect edges using Laplacian of Gaussian (LoG) with sigma=2.0.
   - **Canny Edge Detection**: Apply Canny algorithm with low threshold=100 and high threshold=450.

3. **Coin Segmentation**:
   - **Contour Detection**: Find contours in the edge-detected images.
   - **Minimum Enclosing Circle**: Calculate circles that enclose each contour.
   - **Radius-based Filtering**: Filter detected circles based on radius thresholds (min_radius_ratio=0.23, max_radius_ratio=0.7).
   - **Individual Coin Extraction**: Extract and save each detected coin as a separate image.

4. **Visualization**:
   - Detection results with green circles around detected coins.
   - Color-coded segmentation masks with different colors for each coin.
   - Grid display of individual segmented coins.

#### Results

The script outputs several files for each input image:
- Edge detection results (Marr-Hildreth and Canny)
- Coin detection with green circles around detected coins
- Segmentation masks with different colors for each coin
- Individual extracted coins
- The number of detected coins is logged and displayed in the visualizations

### Panorama Creation

#### Methods

- **Feature Detection**: Detect keypoints and descriptors using SIFT.
- **Feature Matching**: Match keypoints between images.
- **Homography Estimation**: Compute the homography matrix to align images.
- **Image Warping and Blending**: Warp and blend images to create the panorama.

#### Results

- The script outputs stitched panorama images saved in the various output folders.

## Parameters

### Coin Detection Parameters

The script uses the following default parameters which can be modified in the code:

- `blur_kernel`: (7, 7) - Size of Gaussian blur kernel for noise reduction
- `marr_hildreth_sigma`: 2.0 - Sigma for Marr-Hildreth edge detection
- `canny_low`: 100 - Lower threshold for Canny edge detection
- `canny_high`: 450 - Upper threshold for Canny edge detection
- `min_radius_ratio`: 0.23 - Minimum radius as a ratio of image size
- `max_radius_ratio`: 0.7 - Maximum radius as a ratio of image size

## Observations

### Coin Detection

1. **Edge Detection Performance**:
   - Marr-Hildreth method is generally better at detecting smooth, continuous edges but may miss some finer details.
   - Canny method excels at detecting finer details but may produce more fragmented edges.
   - Canny edge detection generally performed better in images with varying lighting conditions.

2. **Coin Detection Accuracy**:
   - The Canny method typically detects more coins due to its sensitivity to fine edges.
   - Marr-Hildreth tends to be more robust against noise but may miss some coins in complex backgrounds.

3. **Radius Filtering Impact**:
   - The choice of minimum and maximum radius ratios significantly affects detection rates.
   - Current parameters work well for images where coins occupy a substantial portion of the frame.

4. **Segmentation Quality**:
   - The circular approximation works well for most coin images.
   - Some overlapping coins may not be properly separated.

### Panorama Creation

- The panorama creation script works well for images with sufficient overlapping regions.
- It may struggle with images that have significant differences in lighting or perspective.
- Best results are achieved with images taken from the same position with consistent lighting.
- Multiple output folders contain different variations or tests of the panorama creation process.

## Example Results

### Coin Detection and Segmentation

#### Original Image
![Original Image](Coin%20Detection/input_images/1.jpeg)

#### Edge Detection
![Marr-Hildreth Edges](Coin%20Detection/visualization_results/1_edges_marr_hildreth.jpg)
![Canny Edges](Coin%20Detection/visualization_results/1_edges_canny.jpg)

#### Coin Detection
![Marr-Hildreth Detection](Coin%20Detection/detection_results/1_marr_hildreth_detection.jpg)
![Canny Detection](Coin%20Detection/detection_results/1_canny_detection.jpg)

#### Segmentation Masks
![Marr-Hildreth Segmentation](Coin%20Detection/detection_results/1_marr_hildreth_segmentation.jpg)
![Canny Segmentation](Coin%20Detection/detection_results/1_canny_segmentation.jpg)

#### Individual Coins
![Marr-Hildreth Coins](Coin%20Detection/visualization_results/1_marr_hildreth_coins.png)
![Canny Coins](Coin%20Detection/visualization_results/1_canny_coins.png)

### Panorama Creation

![Panorama Example 1](Panorama/output_folder1/panorama_result.jpg)
![Panorama Example 2](Panorama/output_folder2/panorama_result.jpg)

## Limitations and Future Work

### Coin Detection

- Current implementation assumes coins are approximately circular.
- Overlapping coins are not handled optimally.
- Background complexity can significantly affect detection performance.
- Future work could include:
  - Machine learning approaches for more robust coin detection.
  - Improved segmentation for overlapping coins.
  - Coin classification by size and appearance.
  - Support for non-circular coins.

### Panorama Creation

- The current implementation works best with images that have significant overlap.
- Future improvements could include:
  - Advanced blending techniques to handle exposure differences.
  - Support for vertical panoramas.
  - Cylindrical or spherical warping for wide-angle panoramas.

## Captured Images

- The captured images used for coin detection are included in the `Coin Detection/input_images` folder.
- The captured images used for panorama creation are included in the `Panorama/images1` and `Panorama/images2` folders.

---

This README provides an overview of the repository, instructions for running the code, and a summary of the methods and results. For any questions or issues, please contact [YourName] at [YourEmail].
