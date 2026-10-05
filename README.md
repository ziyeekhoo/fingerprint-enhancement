# Fingerprint Enhancement & Minutiae Detection Using Gabor Filtering

A Python computer vision pipeline for enhancing latent fingerprint images and detecting candidate fingerprint features under challenging image conditions.

## Overview

Latent fingerprints captured from everyday surfaces can have low contrast, uneven lighting and fragmented ridge patterns. This project explores how classical image-processing techniques can improve ridge visibility and support subsequent feature detection.

The implementation combines custom strided filtering, gradient-based analysis, a multi-orientation Gabor filter bank and corner-based feature detection. Intermediate visualisations make it possible to inspect each stage and compare enhancement settings across two fingerprint images.

## Features

- Grayscale conversion and manual cropping to isolate fingerprint regions.
- Histogram equalisation to improve image contrast.
- Custom strided 2D cross-correlation implemented with NumPy.
- Gaussian smoothing and Sobel derivatives for gradient analysis.
- Block-level orientation analysis and orientation histograms.
- Gabor filtering across multiple orientations.
- Maximum-response aggregation and threshold-based binarisation.
- Candidate feature detection using OpenCV's Shi–Tomasi corner detector.
- Parameter comparisons across two images with different visual characteristics.
- Visualisation and export of annotated feature-detection results.

## Processing Pipeline

| Stage | Method | Purpose |
| --- | --- | --- |
| Region selection | Grayscale conversion and manual cropping | Isolate the fingerprint |
| Contrast enhancement | Histogram equalisation | Improve ridge visibility |
| Gradient analysis | Gaussian smoothing and Sobel derivatives | Examine image structure and gradient directions |
| Orientation analysis | Block averaging and orientation histograms | Inspect the distribution of gradient orientations |
| Ridge enhancement | Multi-orientation Gabor filter bank | Emphasise directional ridge patterns |
| Binarisation | Maximum filter response and relative thresholding | Produce a binary enhanced image |
| Feature detection | Shi–Tomasi corner detection | Identify candidate fingerprint features |
| Comparison and export | Matplotlib and OpenCV | Inspect results and save annotated images |

The implementation also compares enhanced-image detections with detections on the equalised image, and enhanced binarisation with an Otsu-thresholded baseline.

## Parameter Exploration

The code explores Gaussian smoothing, Gabor kernel size and sigma, filter aspect ratio, orientation-bin count, threshold ratio and corner-detector settings.

Separate configurations are compared for the two input images to examine how enhancement and detection respond to different contrast, ridge structure and lighting conditions. Results are inspected through intermediate plots and annotated output images.

In the current tuning loop, output selection uses the number of detected corners. This is a simple heuristic rather than a measure of minutiae accuracy.

## Technologies

- **Python**
- **NumPy** — array operations and custom filtering
- **OpenCV** — preprocessing, Gabor filtering and feature detection
- **Matplotlib** — intermediate visualisations and result comparisons

Install the core dependencies:

```bash
pip install numpy opencv-python matplotlib
```

## Inputs and Outputs

The implementation expects two input images, `glass.png` and `reddit.jpeg`, in the working directory. Crop coordinates are configured for these images and need adjustment when using different inputs.

The workflow generates preprocessing comparisons, gradient maps, orientation histograms, Gabor kernels and responses, binary images and feature overlays.

Annotated outputs are saved as:

- `best_minutiae_glass.png`
- `best_minutiae_reddit.png`

## Limitations

- Detected corners are candidate features; ridge endings and bifurcations are not explicitly classified or verified.
- The Gabor filter bank combines responses globally rather than selecting filters from a local ridge-orientation field.
- The implementation uses a fixed Gabor wavelength rather than estimating local ridge spacing.
- Cropping and enhancement parameters require manual configuration.
- Direct averaging of gradient angles can be affected by angle wraparound.
- Corner counts do not establish detection accuracy, and no ground-truth minutiae evaluation is included.
- Fingerprint matching and identity recognition are outside the current scope.

## References and Acknowledgements

The enhancement approach is informed by:

Hong, L., Wan, Y., and Jain, A. K. (1998). *Fingerprint image enhancement: Algorithm and performance evaluation.* IEEE Transactions on Pattern Analysis and Machine Intelligence, 20(8), 777–789.

The initial Gabor helper was supplied with the source exercise materials. The project builds on this helper through preprocessing, custom strided filtering, gradient analysis, filter-response aggregation, parameter exploration and feature visualisation.
