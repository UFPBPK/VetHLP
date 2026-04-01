# VetHLP

# A Unified Multi-Task Transformer Framework for Predicting Drug Half-Lives Across Six Food-Producing Species

## Overview

This repository presents a **unified deep learning framework** for predicting drug half-lives
((\lambda_{Z,HL})) in plasma and multiple tissues across **six major food-producing species**
(e.g., cattle, swine, chicken).

The model is built on a **Multi-Task Transformer architecture** derived from **ChemBERTa**, and is specifically designed to address **data scarcity in veterinary pharmacokinetics** through shared representation learning. By incorporating **stereochemical awareness** and **hybrid molecular–contextual features**, the framework achieves robust and generalizable half-life predictions across species, tissues, and administration routes.

---

## Key Features 🚀

* **Multi-Task Learning (MTL)**
  Jointly learns pharmacokinetic profiles across multiple species, improving performance for data-limited species via shared latent representations.

* **Stereochemical Awareness**
  Enhanced SMILES tokenization explicitly preserves chirality and bond isomerism (`/`, `\`, `@`) to improve structure–activity learning.

* **Hybrid Feature Integration**
  Combines transformer-based molecular embeddings with contextual metadata:

  * Tissue / Matrix type
  * Route of administration
  * Drug dosage (log-scaled)

* **Automated Hyperparameter Optimization**
  Uses **Optuna** for systematic tuning of learning rates, model capacity, and SMILES augmentation strategies.

* **Explainability Ready**
  Compatible with **SHAP** for post-hoc interpretation of molecular and contextual contributions.

---

## Installation & Setup 🛠️

This project is designed to run in **Google Colab** or a **local Linux environment**.

### Dependencies

**Cheminformatics**

* `rdkit`
* `deepchem`

**Deep Learning**

* `torch`
* `transformers` (Hugging Face)

**Optimization & Explainability**

* `optuna`
* `shap`

**Data Science & Visualization**

* `pandas`
* `scikit-learn`
* `matplotlib`
* `seaborn`

### Installation

```bash
pip install rdkit deepchem torch transformers optuna shap
```

---

## Project Structure 📂

The codebase is organized as sequential notebook cells:

* **Cell 1–2**: Environment setup and data ingestion
* **Cell 3–5**: SMILES validation, categorical encoding, and three-way data splitting
* **Cell 6–8**: Transformer tokenization and `HybridMultiTaskModel` architecture
* **Cell 10–12**: Optuna hyperparameter optimization study
* **Cell 13–14**: Final model training and evaluation on the held-out test set
* **Cell 15–16**: Performance visualization and SMILES augmentation impact analysis

---

## Model Architecture 📊

The framework employs a **shared ChemBERTa-77M-MTR backbone** to extract molecular features from SMILES strings. These embeddings are concatenated with:

* Learned embeddings for **tissue (matrix)** and **route of administration**
* **Stereochemical mean-pool embeddings** derived from chiral and isomeric tokens
* **Numerical dosage information** (log-scaled)

The combined feature vector is passed through a **shared trunk network**, followed by **species-specific output heads** that produce final half-life predictions.

---

## Performance 📈

Model performance is evaluated using:

* **Coefficient of Determination** ((R^2))
* **Root Mean Squared Error (RMSE)**

across all species.

Hyperparameter optimization experiments demonstrate that **SMILES augmentation** significantly stabilizes validation (R^2) by exposing the model to diverse canonical and non-canonical molecular representations.

---

## Usage 📝

### 1. Data Preparation

Ensure input CSV includes the following columns:

* `SMILES`
* `Species`
* `Matrix`
* `Route`
* `Dose`
* `LambdaZHl`

### 2. Hyperparameter Optimization

Run the Optuna optimization cell to identify optimal values for:

* `bert_lr`
* `head_lr`
* `n_augment`

### 3. Final Training

Train the production model using the best configuration.
The final model is saved as:

```text
best_single_model.pt
```

---

## Citation 🎓

This manuscript is under review. If you use this framework in your research, please search the title to see the publication status and please cite it:

Zhang Z, Tell LA, Lin Z. A Unified Multi-Task Transformer Framework for Predicting Drug Half-Lives Across Six Food-Producing Species. Under review.

