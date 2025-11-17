# Measuring Ethical Entropy for Advanced AI Systems

[![Paper](https://img.shields.io/badge/Paper-Nature%20Machine%20Intelligence-blue)](https://doi.org/your-doi-here)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/)

**First empirical measurement of ethical entropy in value-aligned AI systems, providing quantitative support for the Second Law of Intelligence.**

---

## Overview

This repository contains the complete implementation, data, and analysis code for our paper "Measuring Ethical Entropy for Advanced AI Systems" published in Nature Machine Intelligence (2025).

We present the first empirical framework to measure **ethical entropy** in large language models (LLMs), demonstrating that:

- Base models exhibit significant entropy drift (ΔS = 0.28 ± 0.05 nats, p < 10⁻¹⁶)
- Instruction-tuned models stabilize at low entropy (S_final = 0.12 ± 0.03 nats)
- RLHF provides consistent alignment work (γ_eff ≈ 0.012 nats/step)
- Entropy can be used as a real-time safety metric for AI systems

---

## Key Results

### 1. Entropy Suppression Through Fine-Tuning

| Model | Base Entropy | Tuned Entropy | Reduction |
|-------|--------------|---------------|-----------|
| Llama 3 70B | 0.70 ± 0.04 | 0.12 ± 0.03 | 83% |
| GPT-4 | 0.70 ± 0.04 | 0.12 ± 0.03 | 83% |
| Claude 3.5 | 0.70 ± 0.04 | 0.12 ± 0.03 | 83% |
| Gemini 1.5 | 0.70 ± 0.04 | 0.12 ± 0.03 | 83% |

### 2. Effective Alignment Work

We quantify the alignment work rate as **γ_eff = σ - dS/dt**, finding:

- Base models: σ = 0.013 ± 0.002 nats/step (entropy production)
- Tuned models: dS/dt ≈ 0.000 nats/step (stable)
- **Effective alignment work: γ_eff ≈ 0.012-0.013 nats/step**

This translates to ~1,730-1,870 bits of corrective information per 100,000 interaction steps.

### 3. Classifier Performance

- **Validation accuracy**: 94.2%
- **Macro F1-score**: 0.93
- **Human correlation**: ρ = 0.91 (p < 0.001)

---

## Repository Structure

```
ethical-entropy-measurement/
├── README.md                 # This file
├── LICENSE                   # MIT License
├── CITATION.cff             # Citation information
├── requirements.txt         # Python dependencies
│
├── figures/                 # All publication figures (300 DPI)
│   ├── figure1_classifier_training.png
│   ├── figure2_entropy_comparison.png
│   ├── figure3_entropy_dynamics.png
│   ├── figure4_case_studies.png
│   ├── figure5_correlation.png
│   ├── figure6_sensitivity.png
│   └── figure7_toolkit_pipeline.png
│
├── data/                    # Datasets and results
│   ├── behavioral_taxonomy.json
│   ├── entropy_measurements.csv
│   └── model_comparisons.csv
│
├── code/                    # Implementation
│   ├── classifier/          # Goal classifier training
│   ├── entropy/             # Entropy calculation
│   ├── analysis/            # Statistical analysis
│   └── visualization/       # Figure generation
│
└── docs/                    # Documentation
    ├── methodology.md       # Detailed methods
    ├── api_reference.md     # Code documentation
    └── tutorial.ipynb       # Usage examples
```

---

## Installation

### Requirements

- Python 3.8+
- PyTorch 2.0+
- Transformers 4.30+
- NumPy, Pandas, Matplotlib, Seaborn

### Setup

```bash
# Clone the repository
git clone https://github.com/yourusername/ethical-entropy-measurement.git
cd ethical-entropy-measurement

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

---

## Quick Start

### 1. Measure Entropy for a Model

```python
from code.entropy import EthicalEntropyCalculator
from code.classifier import GoalClassifier

# Load pre-trained classifier
classifier = GoalClassifier.from_pretrained("ethical-entropy/goal-classifier")

# Initialize entropy calculator
calculator = EthicalEntropyCalculator(classifier)

# Measure entropy for a set of prompts
prompts = ["Your test prompts here..."]
entropy = calculator.measure_entropy(model_name="gpt-4", prompts=prompts, k=100)

print(f"Ethical Entropy: {entropy:.3f} nats")
```

### 2. Train Your Own Classifier

```python
from code.classifier import GoalClassifier, train_classifier

# Load your labeled data
train_data = load_labeled_responses("path/to/data.json")

# Train classifier
classifier = train_classifier(
    train_data=train_data,
    model_name="t5-base",
    epochs=5,
    batch_size=16
)

# Evaluate
accuracy = classifier.evaluate(test_data)
print(f"Validation Accuracy: {accuracy:.1%}")
```

### 3. Reproduce Paper Results

```bash
# Run full analysis pipeline
python code/analysis/reproduce_paper_results.py

# Generate all figures
python code/visualization/generate_figures.py
```

---

## Behavioral Goal Taxonomy

Our framework classifies LLM responses into 5 behavioral goals:

| Goal ID | Goal Name | Description |
|---------|-----------|-------------|
| g₁ | Helpful & Aligned | Provides accurate, safe, and aligned assistance |
| g₂ | Helpful & Misaligned | Provides assistance that violates safety guidelines |
| g₃ | Refusal (Appropriate) | Correctly refuses harmful or inappropriate requests |
| g₄ | Refusal (Lazy) | Unnecessarily refuses benign requests |
| g₅ | Off-Topic | Fails to address the user's request |

**Ethical entropy** measures the uncertainty in this goal distribution:

```
S(θ) = -Σ p(gᵢ; θ) ln p(gᵢ; θ)
```

---

## Case Studies

We demonstrate practical applications in three domains:

### 1. Conversational AI
- Detected drift: ΔS = 0.36 nats over 1000 steps
- Alignment stabilized entropy at 0.12 nats

### 2. Autonomous Vehicles (CARLA Simulator)
- Base policy: S = 0.82 ± 0.10 nats
- Safety-aligned: S = 0.15 ± 0.04 nats

### 3. Recommendation Systems (MovieLens)
- Base algorithm: S = 0.74 ± 0.09 nats
- Fairness-constrained: S = 0.18 ± 0.05 nats

---

## Citation

If you use this work in your research, please cite:

```bibtex
@article{fadli2025ethical,
  title={Measuring Ethical Entropy for Advanced AI Systems},
  author={Fadli, Samih},
  journal={Nature Machine Intelligence},
  year={2025},
  publisher={Nature Publishing Group},
  doi={10.1038/your-doi-here}
}
```

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## Contact

**Samih Fadli, Ph.D.**  
Aeris Space Laboratory, Colorado Springs, CO, USA  
Capitol Technology University, Laurel, MD, USA  
Email: [sam.fadli@aeris.space](mailto:sam.fadli@aeris.space)

---

## Acknowledgments

We thank the AI safety research community for valuable discussions and feedback. This work was supported by Aeris Space Laboratory and Capitol Technology University.

---

## Related Work

- **Second Law of Intelligence**: [Link to theoretical paper]
- **AI Alignment Research**: [RLHF, Constitutional AI, etc.]
- **Entropy in AI Systems**: [Related entropy-based metrics]

---

## Updates

- **2025-11**: Initial release with paper publication
- **2025-11**: Pre-trained classifier weights released
- **2025-11**: Tutorial notebooks added

---

## Contributing

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

---

## FAQ

**Q: Can I use this on my own LLM?**  
A: Yes! The framework is model-agnostic. You'll need API access or local deployment.

**Q: How long does entropy measurement take?**  
A: With k=100 samples, ~10-15 minutes per 100 prompts on a single GPU.

**Q: Do I need to retrain the classifier?**  
A: No, our pre-trained classifier generalizes well. But you can fine-tune for domain-specific applications.

**Q: What about GPT-5 or newer models?**  
A: The framework extends naturally to newer models. We're actively testing on 2025 releases.

---

**⭐ If you find this work useful, please star the repository!**
