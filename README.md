<img width="612" height="358" alt="Picture5" src="https://github.com/user-attachments/assets/28c4ad78-ebd5-4031-9ebf-20cb4d479a39" />
# Fashion MNIST Clothing Classifier — CNN in MATLAB

MSc Artificial Intelligence Architectures (EG7227) | Group B Competition | University of Leicester, 2025–26

## Overview

This project was developed as part of an in-module AI competition where each group trained a Convolutional Neural Network to classify clothing items from the Fashion MNIST dataset. The goal was to maximise test accuracy while also evaluating the model against real-world clothing images sourced by each team member.

Group B achieved a team average of **91% test accuracy**, with the top individual submission reaching **93%**.

## Dataset

The model was trained and evaluated on the [Fashion MNIST](https://github.com/zalandoresearch/fashion-mnist) dataset, which contains 70,000 greyscale images (60,000 training, 10,000 test) across 10 clothing categories:

| Label | Class |
|-------|-------|
| 0 | T-shirt / Top |
| 1 | Trouser |
| 2 | Pullover |
| 3 | Dress |
| 4 | Coat |
| 5 | Sandal |
| 6 | Shirt |
| 7 | Sneaker |
| 8 | Bag |
| 9 | Ankle boot |

In addition to the standard test set, each team member sourced their own real clothing images to serve as an extended evaluation set.

## Implementation

The classifier was built entirely in MATLAB using the Deep Learning Toolbox. The main script `traintestCNNonClothes.mlx` covers the full pipeline: data loading, preprocessing, CNN architecture definition, training, and evaluation against both the standard test set and the custom clothing images.

<img width="612" height="358" alt="Picture5" src="https://github.com/user-attachments/assets/158fb7b7-036d-4ef6-a25f-2be6ac75fe2e" />

## Results

| Submission | Test Accuracy |
|------------|---------------|
| Individual (Enio Mecaj) | **92%** |
| Group B Average | 91% |

## Team

Group B members: Enio Mecaj, Kai, Adrian, Ankit

Each member contributed personal clothing images used for real-world model evaluation, stored under their respective `*ClothingImages` folders.

## Requirements

- MATLAB R2024b or later
- Deep Learning Toolbox

## How to Run

1. Clone or download this repository
2. Open `traintestCNNonClothes.mlx` in MATLAB
3. Run the live script — training, evaluation, and results are all self-contained within the file
4. To test against custom images, add your own images to a folder and update the image path in the script

## Repository Structure

```
├── traintestCNNonClothes.mlx       # Main MATLAB live script
├── train-images-idx3-ubyte         # Fashion MNIST training images
├── train-labels-idx1-ubyte         # Fashion MNIST training labels
├── t10k-images-idx3-ubyte          # Fashion MNIST test images
├── t10k-labels-idx1-ubyte          # Fashion MNIST test labels
├── EnioClothingImages/             # Real clothing images (Enio)
├── KaiClothingImages/              # Real clothing images (Kai)
├── AdrianClothingImages/           # Real clothing images (Adrian)
└── AnkitClothingImages/            # Real clothing images (Ankit)
```
