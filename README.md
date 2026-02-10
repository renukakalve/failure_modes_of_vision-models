# failure-modes-of-vision-models

When CNNs Fail: Robustness Under Distribution Shift

Research Question:
Do convolutional neural networks degrade gracefully under distribution shift, or do structured corruptions induce predictable failure modes?

Modern vision models achieve high accuracy on curated benchmarks, yet real-world environments introduce noise, blur, compression artifacts, and weather-related distortions. This project investigates how CNNs behave when these assumptions break — focusing not only on whether models fail, but how failure unfolds.

Problem:
High benchmark accuracy does not guarantee real-world reliability.

Models optimized for clean datasets often exhibit brittle behavior when exposed to distribution shifts. Understanding the structure of these failures is essential for building dependable AI systems.

Why It Matters
Real-world deployment rarely resembles benchmark conditions.

Autonomous systems, medical imaging pipelines, and safety-critical perception models must operate under imperfect sensing conditions. Robustness is therefore not a secondary metric — it is a prerequisite for trustworthy AI.

This raises a central question:
Do modern CNNs fail gradually, or collapse under specific perturbations?


Method
Two convolutional architectures were evaluated:
ResNet18
DenseNet121

Training:
Dataset: CIFAR-10
Standard augmentation pipeline
Cross-entropy optimization

Robustness Evaluation
Models were tested on CIFAR-10-C, which introduces controlled corruptions across five severity levels.

Primary corruptions analyzed:

Contrast
Fog
Motion Blur
Gaussian Noise
JPEG Compression
Brightness

Rather than reporting a single robustness score, this study examines behavioral degradation patterns across severity levels.

Key Findings

Models experienced up to a 43% accuracy drop under severe contrast.

Robustness is corruption-dependent, not uniform.

Structural corruptions (contrast, fog, blur) were significantly more damaging than pixel-level perturbations.

JPEG compression and brightness shifts showed comparatively graceful degradation.

DenseNet121 demonstrated slightly stronger resilience, suggesting benefits from dense feature reuse.

These results indicate that distribution shift induces distinct failure regimes, not merely performance decay.

Robustness Degradation Curves

Severity-based evaluation reveals different collapse dynamics:

Contrast → near-linear degradation

Fog → threshold-driven collapse

Motion Blur → early feature damage followed by stabilization

This suggests that CNN vulnerability is tied to the type of information disrupted — particularly edge structure and object boundaries.

Interpretability: Why Do Models Fail?

Grad-CAM was used to examine model attention under corruption.

Observed Behavior:

Clean inputs produce object-centric activation.

Severe corruptions cause attention drift toward background regions.

Feature localization weakens, indicating disruption of hierarchical representations.

This provides mechanistic evidence that robustness failures stem from feature collapse, not random misclassification.

Architecture Insight

While DenseNet121 showed marginally better robustness, both architectures remained vulnerable to structural distortions.

This highlights a broader limitation:

Improved connectivity does not necessarily translate to distributional resilience.

Robustness remains an open challenge in deep vision systems.

Limitations

This work prioritizes controlled analysis over scale.

CIFAR-10 is low resolution (32×32).

Only CNN architectures were studied.

Corruptions are synthetic rather than naturally occurring.

No robustness training methods were applied.

Recognizing these constraints is critical for proper interpretation of results.

Future Directions

Potential extensions include:

Vision Transformer robustness comparison

Robust training strategies (AugMix, DeepAugment, etc.)

Evaluation on higher-resolution datasets

Failure prediction and uncertainty metrics

Repository Structure:


Takeaway

Robustness is not a binary property.

Convolutional networks exhibit structured, corruption-specific degradation patterns that can be systematically analyzed.

Understanding these failure modes is a necessary step toward building reliable vision systems for real-world deployment.
