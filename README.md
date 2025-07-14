# Synthetic Data Generation with Amazon Bedrock for Visual Quality Inspection

This repository demonstrates techniques for generating synthetic image data to address data imbalance challenges in training visual quality inspection models for manufacturing.

## Overview

End of Line (EOL) testing with visual quality inspection is critical in manufacturing to detect defects like scratches, incorrect assembly, or missing components. A key challenge in training machine learning models for this task is the limited availability of defect images, as production processes typically aim to produce defect-free products.

## The Data Imbalance Problem

Imbalanced datasets create several challenges for ML models:

- Models may optimize for accuracy by predicting "good" most of the time, missing crucial defects
- Limited exposure to defect variations leads to poor generalization
- Standard evaluation metrics become misleading (e.g., 98% accuracy might mean failing to detect any defects)

## Dataset

This repository uses a public dataset containing mobile phone images with three defect types (oil, scratch, and strain), focusing specifically on scratch defects.

**Setup:**
1. Download the dataset from: https://github.com/jianzhang96/MSD
2. Extract the good.zip folder and save "0001.png" in your local directory

## Methods

We demonstrate two approaches for generating synthetic defect images:

### 1. Zero-Shot Prompting
- Directly generates images with defects using different random seeds
- Leverages pre-trained knowledge without task-specific training

### 2. Inpainting & Masking
- Selectively modifies specific regions of an image
- Generates new content within masked areas based on provided prompts

## Implementation Details

### Data Preprocessing
- Checks and resizes images to comply with Stability AI's 1048576 pixel limit (1024×1024)

### Amazon Bedrock Integration
- Utilizes Amazon Bedrock to access Stability AI's Stable Diffusion model
- Simplifies the image generation process

### Post-Processing
The repository includes code for:
1. **Blur Detection and Filtering**
   - Calculates Laplacian variance to measure image sharpness
   - Filters out blurry images based on a threshold

2. **Background Conversion**
   - Converts screen content to black background
   - Preserves and enhances visible scratches

## Limitations and Future Work

This implementation doesn't cover fine-tuning of Large Language Models (LLMs), which could further improve model performance. Fine-tuning options include:

- Using SageMaker JumpStart APIs to fine-tune stable diffusion models
- Leveraging Amazon Bedrock and Amazon SageMaker services for LLM customization

## Requirements

- AWS account with Amazon Bedrock access
- Python with OpenCV, NumPy, and AWS SDK dependencies
- Access to the MSD dataset

## Getting Started

1. Clone this repository
2. Download and prepare the dataset as described above
3. Configure your AWS credentials
4. Run the notebooks to generate synthetic defect images
5. Use the generated dataset to train your visual quality inspection models
