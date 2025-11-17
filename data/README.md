# Data

This directory contains datasets and measurement results from the paper.

---

## Files

### 1. `behavioral_taxonomy.json`
**Description**: Complete specification of the 5-category behavioral goal taxonomy

**Structure**:
```json
{
  "goals": [
    {
      "id": "g1",
      "name": "Helpful & Aligned",
      "description": "...",
      "examples": [...],
      "safety_level": "safe",
      "alignment_status": "aligned"
    },
    ...
  ]
}
```

**Usage**:
```python
import json
with open('data/behavioral_taxonomy.json') as f:
    taxonomy = json.load(f)
```

---

### 2. `entropy_measurements.csv`
**Description**: Entropy measurements for all 4 LLM families (base and tuned)

**Columns**:
- `model`: Model name (e.g., "Llama 3 70B", "GPT-4")
- `model_type`: "base" or "tuned"
- `entropy_mean`: Mean ethical entropy (nats)
- `entropy_std`: Standard deviation of entropy
- `drift_rate_mean`: Mean drift rate dS/dt (nats/step)
- `drift_rate_std`: Standard deviation of drift rate
- `gamma_eff_mean`: Mean effective alignment work (nats/step)
- `gamma_eff_std`: Standard deviation of γ_eff
- `n_trials`: Number of measurement trials

**Usage**:
```python
import pandas as pd
data = pd.read_csv('data/entropy_measurements.csv')
```

---

### 3. `model_comparisons.csv` (if available)
**Description**: Detailed comparison metrics across models

---

## Data Collection

### Measurement Protocol

1. **Prompt Set**: 100 diverse prompts covering 5 behavioral categories
2. **Sampling**: k = 100 responses per prompt (10,000 total generations)
3. **Classification**: T5-base goal classifier (94.2% accuracy)
4. **Entropy Calculation**: S(θ) = -Σ p(g_i; θ) ln p(g_i; θ)
5. **Trials**: n = 20 independent measurement runs

### Parameters

- **Temperature**: T = 0.7 (optimal from sensitivity analysis)
- **Sample size**: k = 100 (optimal from sensitivity analysis)
- **Classifier**: T5-base fine-tuned on 1,500 labeled responses
- **Measurement interval**: 1,000 interaction steps

---

## Reproducibility

All measurements can be reproduced using:

```bash
python code/analysis/measure_entropy.py --model gpt-4 --n-trials 20
```

---

## Data Availability

- **Labeled training data**: Available upon request (1,500 responses)
- **Prompt sets**: Included in `code/data/prompts/`
- **Raw model outputs**: Available upon request (large files)

---

## Citation

If you use this data, please cite:

```bibtex
@article{fadli2025ethical,
  title={Measuring Ethical Entropy for Advanced AI Systems},
  author={Fadli, Samih},
  journal={Nature Machine Intelligence},
  year={2025}
}
```

---

## License

Data is released under MIT License. See [LICENSE](../LICENSE) for details.
