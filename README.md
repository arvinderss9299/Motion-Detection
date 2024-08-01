# Motion Detection Using Image Filtering

## Overview

This project demonstrates a technique for motion detection in image sequences captured with a stationary camera. The main objective is to become familiar with image manipulation and filtering techniques. The project focuses on detecting motion by analyzing temporal gradients in pixel intensity values.

## Project Description

The core idea of this project is to detect moving objects in an image sequence where most pixels belong to a stationary background. When a moving object passes in front of the camera, it causes a sudden change in pixel intensity values, which can be detected by observing large gradients in these temporal changes.

## Key Components

1. **Motion Detection**
   - Detects motion by analyzing temporal gradients in pixel intensity values over a sequence of images.
   - Uses image filtering techniques to enhance the detection of moving objects.

2. **Project Implementation**
   - The program reads a sequence of image frames, converts them to grayscale, and applies image filtering techniques to detect motion.
   - The program includes implementations of various filtering methods and thresholding strategies to refine motion detection.

## Requirements

- Python 3.x
- OpenCV (`cv2`)
- NumPy

## Installation

## Installation

1. **Clone the Repository:**

   Clone this repository to your local machine:

   ```bash
   git clone https://github.com/arvinderss9299/Motion-Detection.git

2. **Navigate to the Project Directory:**

   ```bash
    cd Motion-Detection

3. **Install the Required Python Packages:**

   ```bash
    pip install opencv-python-headless numpy
    ```

## Usage

### Prepare Image Sequence

1. **Place your sequence of image frames in a directory.**
   - Ensure the image frames are in a format that can be read by OpenCV (e.g., `.jpg`, `.png`).

2. **Update the `images_path` variable in the `MotionDetection` class with the path to this directory.**
   - Modify the `images_path` parameter in the `MotionDetection` class constructor to point to your image directory.

### Configure Parameters

1. **Choose the type of temporal derivative mask.**
   - You can select from different types of temporal derivative masks such as "simple", "prewitt", or "gaussian".
   - Update the `type_derivative_mask` parameter in the `MotionDetection` class accordingly.

2. **Adjust filtering methods and thresholding strategies as needed.**
   - The program allows for different spatial and temporal filtering techniques. You can experiment with various filters and thresholding methods to optimize motion detection.

### Run the Program

1. **Create a Python file (e.g., `run_motion_detection.py`) and include the following code:**

   ```python
   from motion_detection import MotionDetection
   import cv2

   if __name__ == "__main__":
       # Initialize MotionDetection with the path to your images and desired derivative mask type
       md = MotionDetection(images_path='path_to_your_images', type_derivative_mask="simple")

       # Load images from the specified directory
       array_of_images = md.img_array()

       # Apply spatial filtering to the images (e.g., Gaussian filter)
       filter_images = md.filtering('gauss', array_of_images)

       # Compute temporal derivatives of the filtered images
       temp_derivative = md.temporal_derivative(filter_images)

       # Determine the optimal threshold for motion detection
       thresh = md.thresholding(temp_derivative[:20], "std")

       # Combine the thresholded mask with the original images to highlight detected motion
       masked_images = md.combine_mask(temp_derivative, filter_images, thresh)

       # Save the processed images with detected motion to the output directory
       for ind in range(len(masked_images)):
           cv2.imwrite(f"Threshold_output/image{ind}.png", masked_images[ind])

## Review Results

- **Processed Images:**
  - The images with detected motion will be saved in the `Threshold_output` directory. Each image in this directory represents the result of applying motion detection to the corresponding frame in the sequence.
  
- **Evaluating Results:**
  - Open the images in the `Threshold_output` directory to review how well the motion detection algorithm performed. Look for clear delineation of moving objects against the background.
  
- **Analysis:**
  - Assess the effectiveness of different filtering and thresholding techniques based on the clarity and accuracy of detected motion in the output images.
  - Consider factors such as:
    - **False Positives:** Areas where the algorithm detects motion where there is none.
    - **False Negatives:** Areas where the algorithm misses actual motion.
    - **Noise Reduction:** Evaluate how well the filtering methods reduce noise while preserving actual motion.

## Variations and Exploration

### Temporal Derivative Filters

- **Comparison:**
  - Compare different temporal derivative filters, such as:
    - A simple [−1, 0, 1] filter.
    - A Gaussian derivative filter with varying standard deviations (`sigma`).
  - Analyze how different filters affect the detection of motion and the clarity of results.

### Spatial Smoothing Filters

- **Application:**
  - Apply various 2D spatial smoothing filters to the images before computing temporal derivatives, including:
    - 3x3 and 5x5 box filters.
    - Gaussian filters with different standard deviations (`sigma`).
  - Evaluate the impact of these filters on the motion detection performance.

### Thresholding Strategies

- **Experimentation:**
  - Test different thresholding techniques to determine the most effective method for creating a mask of detected motion.
  - Strategies to explore include:
    - Thresholding based on maximum pixel intensity.
    - Thresholding based on standard deviation of temporal derivatives.
  - Find the threshold value that optimally separates moving objects from the background.

## Results and Discussion

- **Included in the project_report.pdf**

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.

## Acknowledgments

- [OpenCV Documentation](https://docs.opencv.org/)
- [NumPy Documentation](https://numpy.org/doc/)

---
