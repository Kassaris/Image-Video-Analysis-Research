# Pyramidal Optical Flow for Video Motion Analysis

> **Sparse feature tracking, multiscale Lucas–Kanade estimation, dynamic feature acquisition, and noise robustness**

**Research domain:** Computer Vision · Video Analysis · Motion Estimation · Feature Tracking

---

## Abstract

This project studies sparse motion estimation in surveillance video through the interaction between feature detection and pyramidal Lucas–Kanade optical flow. Harris and Shi–Tomasi corners are compared under multiple detector and tracker configurations, followed by experiments on dynamic feature refresh and robustness to salt-and-pepper noise.

The repository is organized as an experimental computer-vision study. Rather than presenting isolated implementation tasks, it connects detector configuration, multiscale tracking, temporal feature management, and image corruption to the quality of the resulting motion trajectories.

## Research Motivation

Sparse optical flow depends on two coupled decisions: **which image locations should be tracked** and **how displacement should be estimated across frames**. A strong motion estimator cannot recover reliable trajectories from unstable features, while a good detector can still fail when motion exceeds the local search scale.

Image pyramids address part of this problem by estimating large displacement first at coarse spatial resolution and refining it at progressively finer levels. The experiments in this repository investigate how that strategy behaves in a real surveillance sequence.

## Research Questions

- **How do Harris and Shi–Tomasi detector parameters affect the density and spatial usefulness of trackable features?**
- **How do Lucas–Kanade window size and pyramid depth influence trajectory stability?**
- **What limitations arise when tracking is initialized exclusively from features visible in the first frame?**
- **How much does dynamic feature refresh improve coverage of objects entering the scene later?**
- **How does salt-and-pepper noise alter feature quality and the relative behavior of Harris and Shi–Tomasi tracking?**

## Methodology

### Video Preprocessing
The VIRAT surveillance sequence is resized to 50% of its original spatial dimensions to reduce computational cost while preserving the scene geometry required for tracking.

### Harris and Shi–Tomasi Feature Detection
The detectors are compared while varying `maxCorners`, `qualityLevel`, and `minDistance`. The analysis considers not only feature count but also whether detected corners occupy structures that remain useful along object trajectories.

### Pyramidal Lucas–Kanade Tracking
Sparse optical flow is estimated across multiple `winSize`, `maxLevel`, and convergence-criterion configurations. The coarse-to-fine pyramid allows larger image displacement to be represented as smaller motion at coarser scales.

### Trajectory Analysis
Tracked points are accumulated over time to reveal stable motion, vertical drift, premature track termination, and missed motion.

### Dynamic Feature Refresh
The baseline is extended by detecting new features after the initial frame. This allows objects and structures that appear later to participate in the tracking process.

### Noise Robustness
Salt-and-pepper noise is introduced at two intensities to evaluate sensitivity to impulsive corruption and spurious corner formation.

## Experimental Data

The experimental sequence is:

`VIRAT_S_010200_00_000060_000218.mp4`

All detector and optical-flow comparisons use the same resized sequence.

## Experimental Protocol

1. Resize and inspect the video sequence.
2. Compare Harris and Shi–Tomasi detector configurations.
3. Select representative feature settings.
4. Evaluate pyramidal Lucas–Kanade parameter combinations.
5. Compare fixed first-frame initialization with dynamic feature refresh.
6. Introduce salt-and-pepper noise at multiple intensities.
7. Interpret trajectory stability and detector robustness.

## Key Findings

- Shi–Tomasi generally provides stronger qualitative tracking on the clean surveillance sequence.
- Very small Lucas–Kanade search windows produce less stable trajectories and miss portions of the observed motion.
- A larger search window and deeper pyramid improve trajectory consistency in the tested scene.
- First-frame-only initialization is restrictive when moving objects enter after tracking begins.
- Refreshing the feature set improves motion coverage and reduces dependence on the initial frame.
- Salt-and-pepper noise creates spurious high-contrast corners and substantially degrades tracking.
- Under the tested noisy conditions, Harris retains more tracks for longer periods than Shi–Tomasi.

## Technical Implementation

The complete workflow is contained in:

`notebooks/pyramidal_optical_flow_motion_analysis.ipynb`

**Technology stack:** Python · OpenCV · NumPy · Matplotlib · scikit-image · Jupyter

## Reproducibility

```bash
pip install -r requirements.txt
jupyter notebook
```

The VIRAT sequence is not bundled with the repository and should be supplied locally in accordance with its original usage terms.

## Limitations

The evaluation is based on one surveillance sequence and is primarily qualitative. The current study does not use optical-flow ground truth, endpoint error, or repeated statistical trials. Detector performance is therefore interpreted within the observed scene rather than as a general benchmark.

## Future Research Directions

- evaluate on multiple surveillance and motion datasets;
- use ground-truth flow or annotated trajectories;
- report endpoint error and track-survival statistics;
- compare with dense optical flow and modern deep optical-flow models;
- investigate automatic feature-refresh schedules;
- study robustness to blur, compression artifacts, illumination changes, and occlusion;
- export trajectory statistics and publication-quality visualizations.

## Methodological Context

The project uses classical image pyramids, Harris/Shi–Tomasi feature detection, and pyramidal Lucas–Kanade optical flow.

## Portfolio Relevance

This project demonstrates feature engineering, multiscale computer vision, temporal tracking, controlled robustness experiments, and interpretation of algorithm behavior in real video.

## Scope Statement

This repository is presented as a **research-style personal project** and does not claim benchmark-level optical-flow performance or peer-reviewed publication.

## License

Project code is distributed under the included license. External video data remains subject to the original provider's terms.
