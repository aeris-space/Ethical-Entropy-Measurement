# Code

Implementation of the ethical entropy measurement framework.

---

## Structure

```
code/
├── classifier/          # Goal classifier training and inference
│   ├── __init__.py
│   ├── model.py        # Classifier model definition
│   ├── train.py        # Training script
│   └── evaluate.py     # Evaluation utilities
│
├── entropy/            # Entropy calculation
│   ├── __init__.py
│   ├── calculator.py   # Main entropy calculator
│   ├── sampling.py     # Response sampling utilities
│   └── uncertainty.py  # Variance decomposition
│
├── analysis/           # Statistical analysis
│   ├── __init__.py
│   ├── drift.py        # Drift detection
│   ├── alignment.py    # Effective alignment work
│   └── statistics.py   # Statistical tests
│
└── visualization/      # Figure generation
    ├── __init__.py
    ├── plots.py        # Plotting utilities
    └── generate_figures.py  # Reproduce all figures
```

---

## Quick Start

### 1. Measure Entropy

```python
from code.entropy import EthicalEntropyCalculator
from code.classifier import GoalClassifier

# Load classifier
classifier = GoalClassifier.from_pretrained("ethical-entropy/goal-classifier")

# Initialize calculator
calculator = EthicalEntropyCalculator(classifier)

# Measure entropy
prompts = ["Your prompts here..."]
entropy = calculator.measure_entropy(
    model_name="gpt-4",
    prompts=prompts,
    k=100,  # samples per prompt
    temperature=0.7
)

print(f"Ethical Entropy: {entropy:.3f} nats")
```

### 2. Train Classifier

```python
from code.classifier import train_classifier

# Load training data
train_data = [
    {"text": "Response 1", "label": "g1"},
    {"text": "Response 2", "label": "g3"},
    ...
]

# Train
classifier = train_classifier(
    train_data=train_data,
    model_name="t5-base",
    epochs=5,
    batch_size=16,
    learning_rate=5e-5
)

# Save
classifier.save_pretrained("models/my-classifier")
```

### 3. Detect Drift

```python
from code.analysis import DriftDetector

detector = DriftDetector(calculator)

# Measure over time
entropies = detector.measure_over_time(
    model_name="gpt-4",
    prompts=prompts,
    steps=1000,
    interval=10
)

# Calculate drift rate
drift_rate = detector.calculate_drift_rate(entropies)
print(f"Drift rate: {drift_rate:.4f} nats/step")
```

### 4. Calculate Alignment Work

```python
from code.analysis import calculate_alignment_work

# Measure base and tuned models
sigma = measure_entropy_production(base_model)  # Base model drift
ds_dt = measure_entropy_change(tuned_model)     # Tuned model stability

# Calculate effective alignment work
gamma_eff = calculate_alignment_work(sigma, ds_dt)
print(f"Effective alignment work: {gamma_eff:.4f} nats/step")
```

---

## API Reference

### Classifier

```python
class GoalClassifier:
    """Goal classifier for behavioral taxonomy."""
    
    def __init__(self, model_name: str = "t5-base"):
        """Initialize classifier."""
        
    def predict(self, texts: List[str]) -> List[str]:
        """Predict goals for texts."""
        
    def predict_proba(self, texts: List[str]) -> np.ndarray:
        """Predict probability distributions."""
        
    @classmethod
    def from_pretrained(cls, path: str) -> "GoalClassifier":
        """Load pre-trained classifier."""
```

### Entropy Calculator

```python
class EthicalEntropyCalculator:
    """Calculate ethical entropy for LLMs."""
    
    def __init__(self, classifier: GoalClassifier):
        """Initialize with goal classifier."""
        
    def measure_entropy(
        self,
        model_name: str,
        prompts: List[str],
        k: int = 100,
        temperature: float = 0.7
    ) -> float:
        """Measure entropy for model on prompts."""
        
    def measure_with_uncertainty(
        self,
        model_name: str,
        prompts: List[str],
        k: int = 100,
        n_trials: int = 20
    ) -> Tuple[float, float]:
        """Measure entropy with uncertainty quantification."""
```

### Drift Detector

```python
class DriftDetector:
    """Detect entropy drift over time."""
    
    def measure_over_time(
        self,
        model_name: str,
        prompts: List[str],
        steps: int = 1000,
        interval: int = 10
    ) -> List[float]:
        """Measure entropy at regular intervals."""
        
    def calculate_drift_rate(
        self,
        entropies: List[float],
        time_steps: Optional[List[int]] = None
    ) -> float:
        """Calculate drift rate dS/dt."""
```

---

## Examples

See `examples/` directory for complete examples:

- `measure_entropy.py`: Basic entropy measurement
- `train_classifier.py`: Train custom classifier
- `detect_drift.py`: Drift detection
- `reproduce_paper.py`: Reproduce paper results

---

## Testing

```bash
# Run all tests
pytest

# Run specific module tests
pytest tests/test_entropy.py

# Run with coverage
pytest --cov=code --cov-report=html
```

---

## Development

### Code Style

```bash
# Format code
black code/

# Check style
flake8 code/

# Type checking
mypy code/
```

### Adding New Features

1. Create feature branch
2. Implement with tests
3. Update documentation
4. Submit pull request

---

## License

MIT License - see [LICENSE](../LICENSE)

---

## Citation

```bibtex
@article{fadli2025ethical,
  title={Measuring Ethical Entropy for Advanced AI Systems},
  author={Fadli, Samih},
  journal={Nature Machine Intelligence},
  year={2025}
}
```
