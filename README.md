# Computer Vision & Deep Learning Research Portfolio

> **Three computational research projects spanning multiscale image processing, video motion analysis, and deep learning for visual recognition.**

This repository brings together three independent but conceptually connected computer-vision studies. The projects progress from **hand-designed multiscale image representations**, to **feature-based motion estimation**, and finally to **learned hierarchical representations with convolutional neural networks**.

The common research theme is the role of **representation, scale, parameter selection, and model design** in extracting useful information from visual data.

---

## Projects

| Project | Research Area | Core Methods | Focus |
|---|---|---|---|
| **[Laplacian Pyramid Image Coding](./laplacian-pyramid-image-coding/)** | Image Processing | Gaussian/Laplacian pyramids, entropy, quantization, PSNR | Multiscale representation and reconstruction fidelity |
| **[Pyramidal Optical Flow](./pyramidal-optical-flow-motion-analysis/)** | Video Analysis | Harris, Shi–Tomasi, Lucas–Kanade, image pyramids | Sparse motion estimation and tracking robustness |
| **[CNN Image Classification & Transfer Learning](./cnn-image-classification-transfer-learning/)** | Deep Learning | LeNet, AlexNet, VGG, custom CNN, VGG16 | Architecture comparison, regularization, and transfer learning |

---

## 1. Laplacian Pyramid Image Coding and Reconstruction

**Research area:** Image Processing · Multiscale Representation · Image Compression

This project investigates the **Laplacian pyramid** as a compact multiscale image representation following the classical Burt–Adelson framework. Gaussian reduction and Laplacian residuals are used to decompose images across spatial scales, followed by exact reconstruction, entropy analysis, and coefficient quantization.

The experimental study focuses on how the generating-kernel parameter **α**, pyramid depth, and quantization strength affect the statistical compactness of the representation and the quality of the reconstructed image.

### Selected Findings

- Increasing α generally produces more concentrated Laplacian coefficient distributions in the tested images.
- Approximately **α = 0.6** provides the lowest measured entropy across most evaluated pyramid levels.
- Coarser quantization reduces entropy while increasing reconstruction error.
- Quantized reconstructions retain moderate visual fidelity, with reported **PSNR values around 30 dB**.

**Methods:** Gaussian pyramids · Laplacian pyramids · multiscale filtering · entropy · quantization · PSNR

**[Explore the full project →](./laplacian-pyramid-image-coding/)**

---

## 2. Pyramidal Optical Flow for Video Motion Analysis

**Research area:** Computer Vision · Video Analysis · Motion Estimation

This project studies **sparse motion estimation in surveillance video** using Harris and Shi–Tomasi feature detection together with pyramidal Lucas–Kanade optical flow.

The analysis examines how detector configuration, Lucas–Kanade window size, pyramid depth, feature initialization, dynamic feature refresh, and salt-and-pepper noise influence trajectory stability and motion coverage.

### Selected Findings

- **Shi–Tomasi** generally provides stronger qualitative tracking on the clean surveillance sequence.
- Larger Lucas–Kanade windows and deeper pyramids improve trajectory consistency in the tested scene.
- Detecting features only in the first frame limits coverage of objects appearing later.
- Dynamic feature refresh improves motion coverage.
- Salt-and-pepper noise introduces spurious corners and significantly degrades tracking; under the tested noisy conditions, Harris retains more tracks for longer periods.

**Methods:** Harris corners · Shi–Tomasi · pyramidal Lucas–Kanade · sparse optical flow · dynamic feature acquisition · noise robustness

**[Explore the full project →](./pyramidal-optical-flow-motion-analysis/)**

---

## 3. CNN Image Classification and Transfer Learning

**Research area:** Computer Vision · Deep Learning · Image Classification

This project compares multiple convolutional neural-network architectures on a reproducible **CIFAR-100 subset**. LeNet, AlexNet, VGG, and a custom CNN are evaluated under different optimization configurations before the study is extended with regularization and **VGG16 transfer learning**.

The experiments connect architecture design with optimizer behavior, batch size, overfitting, generalization, pretrained feature extraction, and partial fine-tuning.

### Selected Findings

- Adam converges rapidly and performs strongly across several tested architectures.
- Optimizer effectiveness varies with architecture.
- **AlexNet** achieves the strongest held-out performance among the four directly trained architectures in the reported experiments.
- Dropout, early stopping, and data augmentation reduce the observed overfitting of the custom CNN.
- Frozen VGG16 features provide rapid transfer-learning convergence, while partial fine-tuning improves adaptation in the reported comparison.

**Methods:** LeNet · AlexNet · VGG · custom CNN · TensorFlow/Keras · dropout · augmentation · transfer learning · VGG16 · fine-tuning

**[Explore the full project →](./cnn-image-classification-transfer-learning/)**

---

## How the Projects Connect

The three projects represent a progression through different approaches to visual information.

### 1. Hand-Designed Multiscale Representation

The Laplacian-pyramid project explicitly separates image information according to spatial scale using predefined filtering, reduction, and expansion operations.

### 2. Multiscale Motion Estimation

The optical-flow project extends multiscale processing into the temporal domain. Image pyramids make larger displacements manageable, while selected image features provide spatial anchors for tracking.

### 3. Learned Hierarchical Representation

The CNN project replaces manually specified visual features with representations learned directly from data. Successive convolutional layers construct increasingly abstract feature hierarchies optimized for classification.

The overall progression is therefore:

**Multiscale signal decomposition → Multiscale motion estimation → Learned visual representation**

A second connection is the importance of **scale**:

| Project | Role of Scale |
|---|---|
| Laplacian Pyramid | Separates image information across spatial frequencies |
| Optical Flow | Enables coarse-to-fine estimation of larger displacement |
| CNN Classification | Builds increasingly abstract representations over larger effective receptive fields |

---

## Research Approach

Across the portfolio, the emphasis is not simply on implementing algorithms, but on **experimentally examining their behavior**.

The projects share several methodological principles:

- controlled parameter variation rather than single-configuration demonstrations;
- direct comparison between alternative algorithms or model configurations;
- analysis of both quantitative metrics and visual outputs;
- interpretation of failure modes and trade-offs;
- explicit distinction between training/optimization behavior and generalization where applicable;
- reproducible notebook-based experimentation.

Examples include α and pyramid-depth sweeps, Harris versus Shi–Tomasi tracking, fixed versus dynamic feature acquisition, optimizer and batch-size comparisons, regularization experiments, and frozen versus fine-tuned transfer learning.

---

## Repository Structure

```text
computer-vision-research-portfolio/
│
├── README.md
├── LICENSE
├── .gitignore
│
├── laplacian-pyramid-image-coding/
│   ├── README.md
│   ├── requirements.txt
│   ├── notebooks/
│   ├── data/
│   └── figures/
│
├── pyramidal-optical-flow-motion-analysis/
│   ├── README.md
│   ├── requirements.txt
│   ├── notebooks/
│   ├── data/
│   └── figures/
│
└── cnn-image-classification-transfer-learning/
    ├── README.md
    ├── requirements.txt
    ├── notebooks/
    ├── data/
    └── figures/
```

Each project contains its own detailed README with the full research motivation, methodology, experimental analysis, findings, limitations, and reproducibility information.

---

## Technology Stack

**Scientific Computing**  
Python · NumPy · SciPy

**Image & Video Processing**  
OpenCV · scikit-image

**Deep Learning**  
TensorFlow · Keras

**Machine Learning & Evaluation**  
scikit-learn

**Visualization & Experimentation**  
Matplotlib · Jupyter Notebook

---

## Reproducibility

Dependencies are maintained at the project level because the three studies use different software stacks.

```bash
cd <project-directory>
pip install -r requirements.txt
jupyter notebook
```

Open the notebook inside the selected project's `notebooks/` directory and execute it in order.

Some experiments require external images, video data, pretrained weights, or generated files that are not bundled directly with the repository because of licensing or storage considerations. The corresponding project documentation describes the expected inputs.

---

## Skills Demonstrated

This portfolio covers practical work in:

- multiscale image and signal processing;
- Gaussian and Laplacian pyramids;
- entropy, quantization, reconstruction, and PSNR;
- feature detection and sparse optical flow;
- temporal feature tracking and robustness analysis;
- CNN architecture design and comparative training;
- optimization and hyperparameter analysis;
- regularization and generalization;
- transfer learning and fine-tuning;
- experimental design and parameter sensitivity analysis;
- quantitative and qualitative result interpretation;
- reproducible technical documentation.

---

## Research Scope

This repository is presented as a **personal computational research portfolio**.

The projects are research-oriented implementations and experimental studies, not claims of peer-reviewed publication or state-of-the-art benchmark performance. Results should be interpreted within the datasets, parameter ranges, and experimental conditions documented in the individual projects.

The detailed project READMEs discuss project-specific limitations and potential extensions.

---

## Methodological Context

The Laplacian-pyramid study follows the classical framework introduced by **P. J. Burt and E. H. Adelson** in *The Laplacian Pyramid as a Compact Image Code*.

The motion-analysis study uses classical **Harris/Shi–Tomasi feature detection** and **pyramidal Lucas–Kanade optical flow**.

The image-classification study explores established **LeNet, AlexNet, VGG/VGG16**, regularization, and transfer-learning paradigms.

---

## License

Project code is distributed under the licenses included in the repository. External datasets, images, videos, pretrained weights, and referenced publications remain subject to the terms of their respective owners or providers.
