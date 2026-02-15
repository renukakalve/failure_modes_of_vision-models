# Research Notes — Failure Modes of CNNs Under Distribution Shift

---

## 1. Motivation

Modern vision models achieve high accuracy on curated benchmarks, yet real-world deployment environments are inherently imperfect. Noise, blur, compression artifacts, and environmental distortions frequently introduce distribution shifts that challenge model stability.

While many student projects prioritize accuracy improvements, robustness remains comparatively underexplored at the undergraduate level. This project was motivated by a desire to move beyond performance metrics and instead understand **how models behave when their assumptions break.**

The primary objective was not only to observe whether convolutional neural networks fail under corruption, but to characterize the structure and progression of those failures.

---

## 2. Core Research Question

Do convolutional neural networks degrade gradually under distribution shift, or do certain corruptions cause sharp, predictable failure patterns?

Understanding this distinction is critical for developing reliable perception systems intended for real-world deployment.

---

## 3. Initial Hypotheses

Prior to experimentation, the following hypotheses were formed:

- Structural corruptions (contrast, fog, motion blur) would produce greater degradation than pixel-level perturbations.
- Dense connectivity might improve robustness by preserving feature reuse across layers.
- Model failures would not be uniform; instead, different corruptions would trigger distinct collapse dynamics.

These hypotheses guided the experimental design.

---

## 4. Model Selection Rationale

Two architectures were chosen to provide contrasting connectivity patterns:

### ResNet18
Residual connections stabilize gradient flow and enable deeper feature hierarchies.

### DenseNet121
Dense connections promote feature reuse, potentially preserving information under corruption.

Rather than maximizing architectural diversity, the goal was controlled comparison.

---

## 5. Dataset Choice

### CIFAR-10
Selected for its standardized training protocol and computational efficiency, allowing rapid experimentation.

### CIFAR-10-C
Provides algorithmically generated corruptions across five severity levels, enabling structured robustness analysis rather than anecdotal evaluation.

The pairing allowed clean baseline measurement followed by controlled distribution shift.

---

## 6. Experimental Design Decisions

Several deliberate decisions shaped the study:

- Evaluate multiple severity levels rather than a single corruption strength.
- Measure performance drop relative to clean accuracy.
- Compare architectures under identical conditions.
- Complement quantitative metrics with interpretability analysis.

This design prioritizes behavioral insight over leaderboard-style reporting.

---

## 7. Why These Corruptions?

The selected corruptions target different aspects of the feature hierarchy:

- **Contrast:** disrupts edge gradients critical for early convolutional filters.
- **Fog:** reduces global visibility, challenging object separation.
- **Motion Blur:** weakens spatial structure and boundary clarity.
- **Gaussian Noise:** injects stochastic pixel-level perturbations.
- **JPEG Compression:** introduces structured artifacts.
- **Brightness:** alters intensity without heavily distorting geometry.

This diversity enables observation of corruption-specific vulnerabilities.

---

## 8. Severity Curve Observations

Analyzing performance across severity levels revealed distinct degradation regimes:

- **Contrast → near-linear collapse**
- **Fog → threshold-driven failure**
- **Motion blur → early damage followed by partial stabilization**

These patterns suggest that CNN fragility is tied to the type of information disrupted, particularly edge structure and object boundaries.

Robustness therefore appears **corruption-dependent rather than uniform.**

---

## 9. Key Experimental Findings

- Models experienced up to a **43% accuracy drop** under severe contrast.
- Structural corruptions were consistently more damaging than pixel-level shifts.
- JPEG compression and brightness produced comparatively graceful degradation.
- DenseNet121 showed marginally stronger resilience but remained vulnerable.

These results indicate that distribution shift induces **structured failure regimes**, not merely gradual decay.

---

## 10. Interpretability Insights (Grad-CAM)

Grad-CAM analysis provided mechanistic evidence of failure.

### Clean Inputs
Activation remained object-centric with strong localization.

### Corrupted Inputs
Several failure signatures emerged:

- Attention drift toward background regions  
- Diffused activation maps  
- Weak feature localization  

This suggests that corruption disrupts hierarchical feature extraction, leading to what can be described as **feature collapse.**

Failures were therefore not random — they reflected representational instability.

---

## 11. Architectural Reflection

While DenseNet demonstrated slightly improved robustness, the difference was not transformative.

This implies that:

> Improved connectivity alone does not guarantee distributional resilience.

Robustness likely requires training strategies explicitly designed to handle distribution shift rather than relying solely on architectural innovation.

---

## 12. What Was Most Surprising

Several observations challenged initial expectations:

- JPEG compression proved less damaging than anticipated.
- Fog produced sharper collapse than Gaussian noise.
- Robustness varied dramatically by corruption type rather than degrading uniformly.

These outcomes reinforced the importance of evaluating models across multiple perturbation classes.

---

## 13. Limitations

This work emphasizes controlled analysis over scale.

Key limitations include:

- CIFAR-10’s low spatial resolution (32×32)
- Exclusive focus on CNN architectures
- Synthetic rather than naturally occurring corruptions
- Absence of robustness training techniques

Recognizing these constraints is essential to avoid overgeneralization.

---

## 14. Future Research Directions

If extended, this work could explore:

- Vision Transformer robustness comparison
- Robust training methods (e.g., AugMix, DeepAugment)
- Higher-resolution datasets
- Frequency-domain analysis of corruption sensitivity
- Failure prediction and uncertainty estimation

Understanding why feature hierarchies destabilize remains a particularly promising direction.

---

## 15. Personal Takeaway

This project reinforced a critical lesson:

> Model evaluation should extend beyond accuracy.

Understanding **failure behavior** is equally important for building reliable AI systems.

The process emphasized hypothesis-driven experimentation, interpretability, and reflective analysis — all essential components of research-oriented machine learning practice.

---

## 16. Project Summary

This project investigates how convolutional neural networks behave under distribution shift using CIFAR-10-C. By evaluating ResNet18 and DenseNet121 across multiple corruption types and severity levels, structured degradation patterns were identified. Grad-CAM analysis further revealed that failures stem from attention drift and feature collapse rather than random misclassification. The findings highlight that robustness is corruption-dependent and remains an open challenge in deep vision systems.
