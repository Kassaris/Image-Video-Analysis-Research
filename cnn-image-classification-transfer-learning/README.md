# CNN Image Classification and Transfer Learning

> **Comparative convolutional architectures, optimization, regularization, and pretrained visual representations**

**Research domain:** Computer Vision · Deep Learning · Image Classification · Transfer Learning

---

## Abstract

This project compares classical and custom convolutional neural-network architectures on a reproducible CIFAR-100 subset. LeNet, AlexNet, VGG, and a custom CNN are studied under multiple optimization configurations before the custom-model workflow is extended with regularization and VGG16-based transfer learning.

The project is structured as a comparative deep-learning study rather than a sequence of architecture-building exercises. Training dynamics, held-out performance, overfitting, optimization behavior, and pretrained representations are analyzed as connected parts of the same experimental workflow.

## Research Motivation

CNN performance depends on substantially more than architectural depth. Optimizer choice, batch size, regularization, training duration, dataset complexity, and pretrained representations all affect convergence and generalization.

Comparing several architectures under controlled conditions provides a way to study these interactions directly. Transfer learning then extends the analysis from models trained from scratch to a setting where visual representations learned elsewhere are reused and adapted to a new classification task.

## Research Questions

- **How do architectural depth and convolutional design affect training and held-out classification performance?**
- **How does optimizer choice interact with different CNN architectures?**
- **What effect does batch size have on convergence behavior, update variability, and training cost?**
- **Can dropout, early stopping, and data augmentation reduce overfitting in the custom CNN?**
- **How quickly can pretrained VGG16 features adapt to the target classification problem?**
- **Does partial fine-tuning improve on a fully frozen pretrained convolutional base?**

## Methodology

### Architecture Comparison
LeNet, AlexNet, VGG, and a custom CNN are trained as distinct model families on the same reproducible CIFAR-100 subset.

### Optimization Study
Multiple optimizer, batch-size, and training-duration configurations are compared using training and validation histories.

### Held-Out Evaluation
The strongest configuration from each architecture is evaluated on the test split to compare generalization beyond the data used for model selection.

### Custom CNN
A stronger custom convolutional feature extractor and classification head provide an additional architecture for experimentation beyond the three established model families.

### Regularization
Dropout, early stopping, and data augmentation are introduced to reduce the observed overfitting of the custom CNN.

### Transfer Learning
A pretrained VGG16 convolutional base is evaluated in two regimes: frozen feature extraction and partial fine-tuning.

### Scalable Data Handling
TFRecord is discussed as a path from convenient in-memory experimentation toward streaming input pipelines suitable for larger datasets.

## Experimental Data

Experiments use a deterministic subset of CIFAR-100 selected by the existing notebook workflow. Keeping the subset fixed supports repeatable comparisons across architectures and training configurations.

## Experimental Protocol

1. Inspect the architectural differences among LeNet, AlexNet, and VGG.
2. Construct and train LeNet, AlexNet, VGG, and `MyCNN`.
3. Compare multiple optimizer and batch-size configurations.
4. Analyze training and validation curves.
5. Evaluate the strongest configuration from each model on held-out test data.
6. Introduce regularization into the custom CNN.
7. Compare validation and test behavior after overfitting control.
8. Reuse pretrained VGG16 features with a frozen convolutional base.
9. Partially fine-tune higher-level pretrained layers.
10. Compare transfer-learning convergence and generalization.

## Key Findings

- Adam converges rapidly and performs strongly across several tested architectures.
- VGG shows different optimizer behavior from the shallower models, emphasizing that optimizer effectiveness is architecture-dependent.
- Larger batch sizes reduce update variance and shorten epoch execution, but they also alter convergence behavior.
- AlexNet achieves the strongest held-out accuracy among the four directly trained architectures in the reported runs.
- Dropout, early stopping, and data augmentation reduce the observed overfitting of the custom CNN.
- Frozen VGG16 transfer learning converges quickly because the convolutional representation is already pretrained.
- Partial fine-tuning improves adaptation of the pretrained representation to the target classes in the reported comparison.

## Technical Implementation

The complete workflow is contained in:

`notebooks/cnn_image_classification_transfer_learning.ipynb`

**Technology stack:** Python · TensorFlow · Keras · NumPy · Matplotlib · scikit-learn · Jupyter

## Repository Structure

```text
cnn-image-classification-transfer-learning/
├── README.md
├── requirements.txt
├── .gitignore
├── LICENSE
├── notebooks/
│   └── cnn_image_classification_transfer_learning.ipynb
├── data/
│   └── README.md
└── figures/
    └── .gitkeep
```

## Reproducibility

```bash
pip install -r requirements.txt
jupyter notebook
```

Dataset retrieval, pretrained weights, and saved model artifacts follow the existing TensorFlow/Keras workflow in the notebook.

## Results and Interpretation

The project deliberately separates **training performance**, **validation behavior**, and **held-out test performance**. This distinction is important because a model that optimizes the training objective effectively may still generalize poorly.

The architecture comparison also shows why optimizer results should not be generalized independently of model design. Likewise, the transfer-learning experiments demonstrate that pretrained representations can substantially change the optimization problem by replacing low-level feature learning with adaptation of an existing visual representation.

## Limitations

The study uses a selected CIFAR-100 subset rather than a full large-scale benchmark protocol. Hyperparameter exploration is finite, repeated-run uncertainty is not systematically reported, and the custom architectures are evaluated within the computational workflow of the notebook. Results should therefore be interpreted as comparative experimental findings rather than definitive architecture rankings.

## Future Research Directions

- repeat experiments across multiple random seeds;
- expand to the complete CIFAR-100 dataset;
- add precision, recall, F1, and per-class confusion analysis;
- introduce learning-rate schedules and modern optimizers;
- compare additional pretrained architectures such as ResNet or EfficientNet;
- perform systematic fine-tuning-depth experiments;
- add calibration and uncertainty analysis;
- automate experiment tracking and checkpoint management;
- move reusable model definitions into tested Python modules.

## Methodological Context

The project draws on the established LeNet, AlexNet, VGG/VGG16, regularization, and transfer-learning paradigms implemented in the notebook.

## Portfolio Relevance

This project demonstrates comparative deep-learning experimentation, CNN architecture implementation, hyperparameter analysis, generalization control, transfer learning, and interpretation of model behavior.

## Scope Statement

This repository is presented as a **research-style personal project**. It does not claim peer-reviewed publication, state-of-the-art CIFAR-100 performance, or benchmark conclusions beyond the experiments contained in the notebook.

## License

Project code is distributed under the included license. CIFAR-100, pretrained weights, and external model resources remain subject to their respective original terms.
