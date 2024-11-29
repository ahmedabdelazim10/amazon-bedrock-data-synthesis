# amazon-bedrock-data-synthesis

## Synthetic data generation with Amazon Bedrock for visual quality inspection model training

### Introduction

End of Line (EOL) testing that involves visual quality inspection is a critical step in the manufacturing process. The main goal of visual quality inspection is to detect any defects or irregularities that might have occurred during the manufacturing process. This can include issues like surface imperfections (ex. scratches), incorrect assembly or missing components. Visual quality inspection can involve both manual and automated inspection. The automated systems use cameras and machine learning models to perform the visual quality inspection. <br>
 
One of the key challenges when training these machine learning models is the availability of images showing failures of the final product. This is understandable because the companies are normally producing failure-free products. In other words, the dataset of images with failures is small which presents several challenges (ex. data imbalance) that can significantly impact the machine learning model’s performance. To overcome this problem so called foundation models can be used to increase the size of the dataset by generating more images with failures.<br> <span style="color:red"> CAN YOU ELABORATE A BIT MORE WHY A IMBALANCED DATASET MAY NOT BE IDEAL TO TRAIN A VISUAL INSPECTION MODEL </span>

Imbalanced datasets pose significant challenges for machine learning models because they can lead to biased predictions favoring the majority class, reducing the model's real-world effectiveness. In visual inspection, having for example 1000 images of good parts but only 50 defective ones can create several problems like:

1. The model may optimize for accuracy by simply predicting "good" most of the time, missing crucial defect detections
2. Limited exposure to defect variations means poor generalization to new defect types
3. Standard evaluation metrics become misleading - 98% accuracy could mean failing to detect any defects

The public dataset used in this notebook contains pictures of mobile phones with 3 types of defects (oil, scratch and strain). We focus only in this notebook on the scratch type. 
https://github.com/jianzhang96/MSD

We'll present 2 different methods how to generate data for visual quality inspection model training (i.e. images of mobile phones with scratches)
- Directly using zero-shot prompting
- Using inpainting and masking API offered by Stability AI (Stable Diffusion)