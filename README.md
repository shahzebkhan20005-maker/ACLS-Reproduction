# ACLS: Adaptive and Conditional Label Smoothing for Network Calibration

## Project Overview

This project reproduces selected experiments from the research paper **"ACLS: Adaptive and Conditional Label Smoothing for Network Calibration" (ICCV 2023)**.

The main objective is to compare a standard Cross-Entropy (CE) loss function with the Adaptive and Conditional Label Smoothing (ACLS) loss function.

The experiments are performed using the CIFAR-10 dataset and a ResNet-50 architecture adapted for 10 output classes.

The project evaluates both models based on:
- Classification Accuracy
- Expected Calibration Error (ECE)
- Adaptive Expected Calibration Error (AECE)

## Research Paper

**Title:** ACLS: Adaptive and Conditional Label Smoothing for Network Calibration

**Conference:** IEEE/CVF International Conference on Computer Vision (ICCV), 2023

**Official GitHub Repository:** https://github.com/cvlab-yonsei/ACLS

## Dataset

**Dataset:** CIFAR-10

CIFAR-10 contains 60,000 color images divided into 10 classes.

- Training images: 50,000
- Testing images: 10,000
- Image size: 32 × 32 pixels
- Number of classes: 10

The dataset is loaded using the `torchvision.datasets.CIFAR10` utility.

### Preprocessing

The following preprocessing techniques are used:

- Random cropping with padding.
- Random horizontal flipping.
- Conversion of images into tensors.
- Normalization using CIFAR-10 mean and standard deviation.

A validation portion is separated from the training data.

## Model Architecture

The project uses ResNet-50, modified for CIFAR-10 classification.

The final fully connected layer is changed to produce 10 output classes. The initial convolution and max-pooling layers are also adapted for CIFAR-10 images.

Two experimental approaches are compared:

### 1. Baseline Model

The baseline model uses the standard Cross-Entropy (CE) loss function.

### 2. ACLS Model

The ACLS model uses the ACLS loss function, which adds calibration-related regularization to the classification loss.

## Experimental Setup

| Setting | Value |
|---|---|
| Dataset | CIFAR-10 |
| Architecture | ResNet-50 |
| Optimizer | SGD |
| Batch Size | 128 |
| Epochs | 5 |
| Momentum | 0.9 |
| Weight Decay | 0.0005 |
| Learning Rate | Refer to experiment_config.json |
| Framework | PyTorch |
| Environment | Kaggle Notebook |

The ACLS experiment also uses gradient clipping and a reduced learning rate to address training instability. These adjustments are documented in the experiment configuration.

## Evaluation Metrics

The models are evaluated using three metrics:

- **Accuracy:** Measures the percentage of correctly classified images.
- **ECE:** Measures the difference between model confidence and actual accuracy using equal-width confidence bins.
- **AECE:** Measures calibration error using equal-count confidence bins.

Reliability diagrams are also generated to visualize model calibration.

## Project Structure

```text
ACLS-Reproduction/
│
├── ACLS_CIFAR10_Reproduction.ipynb
├── README.md
├── requirements.txt
├── Assignment_02_Report.pdf
│
├── results/
│   ├── training_curves/
│   ├── calibration/
│   ├── class_distribution.png
│   ├── experiment_config.json
│   ├── original_vs_reproduced_comparison.csv
│   ├── reproduced_test_results.csv
│   └── results_summary.txt
│
└── models/
```

## How to Run the Project

1. Clone or download this repository.
2. Install the required Python libraries using:

```bash
pip install -r requirements.txt
```

3. Open `ACLS_CIFAR10_Reproduction.ipynb` in Jupyter Notebook or Kaggle.
4. Run the notebook cells in their correct order.
5. The CIFAR-10 dataset will be loaded through torchvision.
6. Train the baseline and ACLS models.
7. Evaluate the models using Accuracy, ECE, and AECE.
8. View the generated graphs and comparison results in the results folder.

**Note:** Running the notebook from the beginning will train the models again. The saved results are provided separately for reference.

## Results

The project includes:

- Training loss curves.
- Validation accuracy curves.
- Reliability diagrams.
- Reproduced test evaluation metrics.
- Original paper versus reproduced results comparison.

The numerical results are available in:

- `reproduced_test_results.csv`
- `original_vs_reproduced_comparison.csv`

The detailed experiment settings are available in `experiment_config.json`.

## Reproducibility and Limitations

The reproduced experiments do not exactly match the original paper's experimental conditions.

Differences include training duration, optimization settings, and implementation choices. The ACLS experiment also required stability adjustments.

The original paper reports validation results, whereas this reproduction evaluates the held-out test set. Therefore, the results should not be treated as a direct, identical-protocol comparison.

The project documents these differences and reports the actual experimental results.

## Author

**Student Project – Deep Learning Assignment 02**

