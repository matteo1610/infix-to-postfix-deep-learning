# Infix-to-Postfix Translation with Deep Learning

An encoder-decoder neural network that learns to translate arithmetic expressions
from **infix notation** to **postfix notation** (Reverse Polish Notation).

For example:

```text
Infix:  (a+b)*c
Postfix: a b + c *
```

This project was developed as a deep learning study project and is maintained
as a reproducible portfolio project.

## Why this project

The task combines symbolic sequence generation with a compact, fully synthetic
dataset. It demonstrates:

- grammar-aware generation of arithmetic expressions;
- tokenization and vocabulary design with `PAD`, `SOS`, and `EOS` tokens;
- sequence-to-sequence modelling with an encoder-decoder architecture;
- teacher forcing during training;
- autoregressive decoding at inference time;
- early stopping, checkpointing, and qualitative evaluation.

## Repository layout

```text
.
├── models/
│   └── best_model.keras
├── notebooks/
│   ├── infix_to_postfix_translation.ipynb
│   └── specification.ipynb
├── archive/
│   └── legacy/                 # Previous experiments and checkpoints
├── .gitignore
├── LICENSE
├── README.md
└── requirements.txt
```

The main deliverable is
[`notebooks/infix_to_postfix_translation.ipynb`](notebooks/infix_to_postfix_translation.ipynb).
The specification notebook records the initial project definition. Historical
versions are retained in `archive/legacy/` for provenance but are not part of
the recommended workflow.

## Getting started

### 1. Clone and create an environment

```bash
git clone <your-repository-url>
cd infix-to-postfix-deep-learning
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

On Windows, activate the environment with:

```powershell
.venv\Scripts\Activate.ps1
```

### 2. Run the notebook

Open the notebook in VS Code or Jupyter:

```bash
python -m pip install jupyter
jupyter notebook notebooks/infix_to_postfix_translation.ipynb
```

Run the cells from top to bottom. The notebook generates training examples,
builds and trains the model, evaluates predictions, and demonstrates inference.
The tracked checkpoint in `models/best_model.keras` can be used when you want
to inspect a trained model without keeping newly generated training artifacts.

## Reproducibility notes

- The project targets Python 3.11 or newer.
- TensorFlow/Keras, NumPy, Matplotlib, and gdown versions are pinned in
  [`requirements.txt`](requirements.txt).
- Random seeds are set in the notebook where data and model randomness are
  introduced.
- The dataset is generated programmatically, so no private or external dataset
  is required.
- Training can be CPU-intensive. A previously trained Keras checkpoint is
  included for convenient inspection.

## Limitations and possible extensions

The current vocabulary and expression grammar are intentionally small:
identifiers are limited to `a`–`f`, operators to `+`, `-`, `*`, and `/`, and
expressions use a bounded sequence length. Natural next steps include:

1. adding exponentiation and unary operators;
2. supporting numeric literals and multi-character identifiers;
3. measuring exact-sequence accuracy on a held-out test set;
4. comparing the neural model with a deterministic stack-based converter;
5. exposing inference through a small command-line or web API.

## License

Released under the MIT License. See [`LICENSE`](LICENSE).
