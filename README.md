Performing Dense Prediction Using Deep Learning

This repository contains the implementation and results of a semantic segmentation project focused on dense prediction using deep learning. The goal is to classify every pixel of high-resolution aerial imagery into meaningful land-cover classes such as buildings, roads, vegetation, cars, and low vegetation.

The project compares two architectures:

Hypercolumns-based model (baseline using VGG16 feature fusion)

U-Net encoder–decoder (main model)

🔍 Overview

Dense prediction assigns a label to each pixel of an image. This is essential for tasks such as:

Urban mapping

Autonomous navigation

Remote sensing analysis

This project uses the ISPRS Vaihingen aerial dataset, which provides RGB images and pixel-wise ground truth masks for 6 classes.

📂 Dataset

High-resolution aerial images from Vaihingen, Germany

Six semantic classes: Buildings, Roads, Trees, Low Vegetation, Cars, Clutter

Large tiles (~2500×2500 px)

Tiles are split into 256×256 patches for efficient training

16 tiles used for training & validation; remaining tiles reserved as unseen test data

Patch extraction helps with GPU efficiency, data diversity, and stable model learning.

🧠 Model Architectures
1️⃣ Hypercolumns Model (Baseline)

Uses a pretrained VGG-16 backbone

Extracts feature maps from shallow, mid, and deep layers

Resizes and concatenates all features to form “hypercolumns”

Final convolution layers perform per-pixel classification

Limitations:
Produces coarse segmentations and struggles with fine boundaries and small objects.

2️⃣ U-Net Architecture

Classical encoder–decoder design

Encoder extracts semantic and contextual features

Decoder upsamples back to original resolution

Skip connections transfer fine details from encoder to decoder

Designed specifically for pixel-wise prediction tasks

Strengths:
Sharp boundaries, accurate localization, improved detection of small objects.

⚙️ Training Pipeline

Load high-resolution tiles

Extract 256×256 image–mask patches

Split into training and validation sets

Train using:

Categorical Cross-Entropy Loss

Adam optimizer (lr = 0.001)

Evaluate using Mean Intersection over Union (Mean IoU)

Save best model weights based on validation metrics

📊 Results
Quantitative Performance
Model	Mean IoU	Notes
Hypercolumns	~0.45	Coarse masks and weaker boundary localization
U-Net	~0.75	Best performer; sharp and accurate segmentation
