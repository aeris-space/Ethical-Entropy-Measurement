# Figures

This directory contains all publication-quality figures from the paper "Measuring Ethical Entropy for Advanced AI Systems".

All figures are 300 DPI PNG format, suitable for publication.

---

## Figure List

### Figure 1: Goal Classifier Training Performance
**File**: `figure1_classifier_training.png` (383 KB)

Two-panel plot showing:
- (a) Classification accuracy over 5 training epochs
- (b) Cross-entropy loss over 5 training epochs

Final validation accuracy: **94.2%**, F1-score: **0.93**

---

### Figure 2: Entropy Comparison (Base vs Tuned)
**File**: `figure2_entropy_comparison.png` (167 KB)

Bar chart comparing final ethical entropy between base and instruction-tuned models across 4 LLM families:
- Base models: 0.70 ± 0.04 nats
- Tuned models: 0.12 ± 0.03 nats
- **83% reduction** (p < 10⁻¹⁶)

---

### Figure 3: Entropy Dynamics Over Time
**File**: `figure3_entropy_dynamics.png` (276 KB)

Time series showing entropy evolution over 1000 interaction steps:
- Base model: dS/dt = 0.013 ± 0.002 nats/step (drifting)
- Tuned model: dS/dt ≈ 0.000 nats/step (stable)

---

### Figure 4: Case Studies Across Domains
**File**: `figure4_case_studies.png` (194 KB)

Three-panel bar chart showing entropy in:
- (a) Conversational AI: ΔS = 0.36 nats
- (b) Autonomous Vehicle: Base = 0.82, Aligned = 0.15
- (c) Recommendation System: Base = 0.74, Aligned = 0.18

---

### Figure 5: Classifier-Human Correlation
**File**: `figure5_correlation.png` (239 KB)

Scatter plot showing strong correlation between classifier-derived and human-annotated entropy scores:
- Pearson correlation: **ρ = 0.91**
- p < 0.001
- n = 50 test responses

---

### Figure 6: Sensitivity Analysis
**File**: `figure6_sensitivity.png` (295 KB)

Two-panel analysis:
- (a) Temperature sensitivity: Optimal T = 0.7
- (b) Sample size sensitivity: Optimal k = 100 (k=50 retains 95% accuracy)

---

### Figure 7: Toolkit Pipeline Diagram
**File**: `figure7_toolkit_pipeline.png` (257 KB)

Flowchart showing the complete entropy measurement pipeline:
1. Input Prompt
2. LLM Generation (k=100 samples)
3. Goal Classifier (T5-base)
4. Probability Distribution p(g_i; θ)
5. Entropy Calculation S(θ)
6. Drift Detection dS/dt
7. Alerts & Monitoring

---

## Usage

All figures are released under the MIT License and can be used in presentations, papers, or educational materials with proper attribution.

### Citation

```bibtex
@article{fadli2025ethical,
  title={Measuring Ethical Entropy for Advanced AI Systems},
  author={Fadli, Samih},
  journal={Nature Machine Intelligence},
  year={2025}
}
```

---

## Technical Details

- **Format**: PNG
- **Resolution**: 300 DPI
- **Color space**: RGB
- **Color palette**: Colorblind-friendly
- **Font**: DejaVu Sans
- **Generated with**: Matplotlib 3.7+, Seaborn 0.12+

---

## Regeneration

To regenerate these figures from raw data:

```bash
python code/visualization/generate_figures.py
```

All figure generation code is available in the `code/visualization/` directory.
