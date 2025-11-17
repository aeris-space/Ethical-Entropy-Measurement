# Contributing to Ethical Entropy Measurement

Thank you for your interest in contributing! This document provides guidelines for contributing to this project.

---

## Ways to Contribute

1. **Bug Reports**: Report issues or bugs
2. **Feature Requests**: Suggest new features or improvements
3. **Code Contributions**: Submit pull requests
4. **Documentation**: Improve docs, tutorials, or examples
5. **Testing**: Test on new models or datasets
6. **Research**: Extend the methodology or theory

---

## Getting Started

### 1. Fork the Repository

```bash
# Fork on GitHub, then clone your fork
git clone https://github.com/YOUR_USERNAME/ethical-entropy-measurement.git
cd ethical-entropy-measurement
```

### 2. Set Up Development Environment

```bash
# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Install development dependencies
pip install pytest black flake8 mypy
```

### 3. Create a Branch

```bash
git checkout -b feature/your-feature-name
```

---

## Code Style

We follow PEP 8 style guidelines with some modifications:

### Formatting

```bash
# Format code with black
black code/

# Check style with flake8
flake8 code/

# Type checking with mypy
mypy code/
```

### Guidelines

- **Line length**: 100 characters (not 80)
- **Docstrings**: Google style
- **Type hints**: Required for all functions
- **Comments**: Explain *why*, not *what*

### Example

```python
def calculate_entropy(probabilities: np.ndarray) -> float:
    """Calculate Shannon entropy from probability distribution.
    
    Args:
        probabilities: Array of probabilities (must sum to 1)
        
    Returns:
        Entropy in nats (natural logarithm base)
        
    Raises:
        ValueError: If probabilities don't sum to 1
    """
    if not np.isclose(probabilities.sum(), 1.0):
        raise ValueError("Probabilities must sum to 1")
    
    # Remove zero probabilities to avoid log(0)
    probs = probabilities[probabilities > 0]
    
    return -np.sum(probs * np.log(probs))
```

---

## Testing

### Running Tests

```bash
# Run all tests
pytest

# Run with coverage
pytest --cov=code --cov-report=html

# Run specific test file
pytest tests/test_entropy.py
```

### Writing Tests

```python
import pytest
from code.entropy import calculate_entropy

def test_entropy_uniform():
    """Test entropy of uniform distribution."""
    probs = np.array([0.2, 0.2, 0.2, 0.2, 0.2])
    expected = np.log(5)  # ln(5) for uniform over 5 categories
    assert np.isclose(calculate_entropy(probs), expected)

def test_entropy_deterministic():
    """Test entropy of deterministic distribution."""
    probs = np.array([1.0, 0.0, 0.0, 0.0, 0.0])
    assert calculate_entropy(probs) == 0.0

def test_entropy_invalid():
    """Test that invalid probabilities raise error."""
    probs = np.array([0.5, 0.3, 0.1])  # Doesn't sum to 1
    with pytest.raises(ValueError):
        calculate_entropy(probs)
```

---

## Pull Request Process

### 1. Before Submitting

- [ ] Code follows style guidelines
- [ ] All tests pass
- [ ] New tests added for new features
- [ ] Documentation updated
- [ ] Commit messages are clear

### 2. Commit Messages

Follow conventional commits:

```
feat: Add temperature sensitivity analysis
fix: Correct entropy calculation for edge case
docs: Update methodology documentation
test: Add tests for classifier training
refactor: Simplify probability estimation
```

### 3. Pull Request Template

```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Documentation update
- [ ] Performance improvement
- [ ] Code refactoring

## Testing
Describe tests added or run

## Checklist
- [ ] Code follows style guidelines
- [ ] Tests pass
- [ ] Documentation updated
- [ ] No breaking changes (or documented)
```

### 4. Review Process

1. Automated checks run (tests, linting)
2. Maintainer reviews code
3. Address feedback
4. Approval and merge

---

## Documentation

### Docstrings

Use Google style:

```python
def train_classifier(
    train_data: List[Dict],
    model_name: str = "t5-base",
    epochs: int = 5
) -> GoalClassifier:
    """Train goal classifier on labeled data.
    
    Args:
        train_data: List of dicts with 'text' and 'label' keys
        model_name: HuggingFace model identifier
        epochs: Number of training epochs
        
    Returns:
        Trained classifier instance
        
    Raises:
        ValueError: If train_data is empty
        
    Example:
        >>> data = load_data("train.json")
        >>> classifier = train_classifier(data, epochs=5)
        >>> accuracy = classifier.evaluate(test_data)
    """
```

### README Updates

If adding new features, update:
- Main README.md
- Relevant section READMEs
- API documentation

---

## Research Contributions

### Extending the Methodology

If you're extending the research:

1. **Propose first**: Open an issue to discuss
2. **Document thoroughly**: Explain theory and motivation
3. **Validate empirically**: Provide experimental results
4. **Compare**: Benchmark against existing methods

### Adding New Models

To add support for a new LLM:

```python
# code/models/new_model.py
from code.models.base import BaseModel

class NewModel(BaseModel):
    """Support for NewModel LLM."""
    
    def generate(self, prompt: str, k: int = 100) -> List[str]:
        """Generate k responses to prompt."""
        # Implementation here
        pass
```

---

## Community Guidelines

### Code of Conduct

- Be respectful and inclusive
- Welcome newcomers
- Focus on constructive feedback
- Assume good intentions

### Communication

- **Issues**: For bugs, features, questions
- **Discussions**: For general topics
- **Pull Requests**: For code contributions
- **Email**: For private matters

---

## Recognition

Contributors will be:
- Listed in CONTRIBUTORS.md
- Acknowledged in release notes
- Cited in derivative research (if significant contribution)

---

## Questions?

- **Email**: [sam.fadli@aeris.space](mailto:sam.fadli@aeris.space)
- **Issues**: [GitHub Issues](https://github.com/yourusername/ethical-entropy-measurement/issues)
- **Discussions**: [GitHub Discussions](https://github.com/yourusername/ethical-entropy-measurement/discussions)

---

Thank you for contributing to AI safety research! 🚀
