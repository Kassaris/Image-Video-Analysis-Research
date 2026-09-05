# Laplacian Pyramid Image Coding and Reconstruction

> **Multiscale image representation, entropy analysis, quantization, and reconstruction fidelity**

**Research domain:** Image Processing · Multiscale Signal Representation · Image Compression

---

## Abstract

This project investigates the Laplacian pyramid as a compact multiscale representation for image coding. Following the classical Burt–Adelson framework, the study examines how Gaussian reduction, Laplacian residuals, pyramid depth, the generating-kernel parameter α, and coefficient quantization influence coding entropy and reconstruction quality.

The repository is structured as a self-contained computational research study rather than an assignment. The emphasis is on methodological motivation, reproducible implementation, controlled experimentation, parameter sensitivity, and interpretation of observed behavior.

## Research Motivation

Multiscale representations provide a natural way to separate image information according to spatial scale. In a Laplacian pyramid, successive prediction-error images preserve the detail removed when moving from one Gaussian level to the next. This creates a representation that is both reconstructable and suitable for studying compact image coding.

The central experimental question is not simply whether a pyramid can be constructed, but how its design affects the statistical structure of its coefficients and the quality of the reconstructed image after information is discarded through quantization.

## Research Questions

- **How does the generating-kernel parameter α change the distribution of image information across spatial scales?**
- **How does pyramid depth affect coefficient statistics and measured entropy?**
- **Which α values produce the most compact representation for the tested images?**
- **How aggressively can Laplacian coefficients be quantized before reconstruction degradation becomes visually significant?**
- **How does the entropy–distortion trade-off behave across grayscale and color imagery?**

## Methodology

### Gaussian Pyramid Construction
Repeated low-pass filtering and spatial reduction create progressively coarser image representations while suppressing frequencies that cannot be represented after subsampling.

### Laplacian Decomposition
Adjacent Gaussian levels are related through expansion and subtraction. The resulting residual images isolate information lost between scales and form the Laplacian pyramid.

### Exact Inverse Reconstruction
The coarsest representation is recursively expanded and combined with the stored Laplacian residuals. This stage validates lossless reconstruction before quantization is introduced.

### Parameter Sensitivity
The generating-kernel parameter α and pyramid depth are varied independently to study their effect on smoothing, coefficient concentration, visual structure, and entropy.

### Entropy Analysis
Entropy is used as a quantitative proxy for coding compactness. Coefficient distributions and their histograms are compared across images, α values, and pyramid depths.

### Quantization
Multiple coefficient binning strategies are applied to investigate the compression–distortion trade-off. Coarser quantization lowers the number of effective coefficient values but introduces reconstruction error.

### Reconstruction Quality
Reconstructed outputs are examined visually and through signal-quality measurements including PSNR.

## Experimental Data

Experiments use grayscale and color versions of Lena together with the standard cameraman image. This provides single-channel and multichannel cases with different edge, texture, and intensity structures.

## Experimental Protocol

1. Construct Gaussian and Laplacian pyramids.
2. Verify exact reconstruction in the unquantized case.
3. Sweep α over the tested range and inspect the resulting pyramid structure.
4. Vary pyramid depth independently.
5. Measure entropy and coefficient distributions.
6. Identify low-entropy parameter settings.
7. Quantize Laplacian coefficients with multiple bin configurations.
8. Reconstruct the images and compare fidelity.

## Key Findings

- Increasing α generally concentrates the Laplacian coefficient distribution and lowers measured entropy in the tested images.
- The experiments identify **α≈0.6** as the strongest overall entropy-minimizing setting across most evaluated pyramid levels.
- Increasing pyramid depth tends to broaden the multiscale representation and can increase measured entropy.
- Coarser quantization reduces entropy but introduces larger reconstruction errors.
- The tested quantized reconstructions retain moderate visual fidelity, with reported PSNR values around **30 dB**.

These findings are specific to the tested images, parameter ranges, and implementation and are not presented as universal compression benchmarks.

## Technical Implementation

The complete workflow is contained in:

`notebooks/laplacian_pyramid_image_coding.ipynb`

**Technology stack:** Python · NumPy · SciPy · OpenCV · scikit-image · Matplotlib · Jupyter

## Repository Structure

## Reproducibility

```bash
pip install -r requirements.txt
jupyter notebook
```

Execute the notebook in order. External image assets are intentionally not duplicated when their licensing makes repository inclusion inappropriate.

## Limitations

The study uses a small collection of representative images and a finite parameter sweep. Some conclusions are therefore empirical rather than statistical. Repeated experiments over larger image datasets and rate–distortion curves would strengthen the evaluation.

## Future Research Directions

- evaluate the method on a larger and more diverse image corpus;
- construct explicit rate–distortion curves;
- compare uniform and adaptive quantization;
- compare Laplacian pyramids with wavelet and modern transform coding;
- automate parameter sweeps and experiment logging;
- export publication-quality figures and tables;
- separate reusable pyramid operators into tested Python modules.

## Methodological Context

The theoretical foundation follows P. J. Burt and E. H. Adelson, *The Laplacian Pyramid as a Compact Image Code*.

## Portfolio Relevance

This project demonstrates multiscale signal-processing implementation, controlled parameter analysis, quantitative evaluation, and interpretation of the trade-off between compact representation and reconstruction fidelity.

## Scope Statement

This repository is presented as a **research-style personal project**. It does not claim peer-reviewed publication, state-of-the-art compression performance, or results beyond those supported by the experiments in the notebook.

## License

Project code is distributed under the included license. External images and publications remain subject to their original terms.
