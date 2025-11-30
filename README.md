# AI-Based Prediction of Tensile Strength for WAAM 9Cr-1Mo Steel


## Project Overview

This project presents a novel **Artificial Intelligence framework** to predict the anisotropic tensile strength (Stress & Strain) of **9Cr-1Mo steel** components fabricated via **Wire Arc Additive Manufacturing (WAAM)**.

By analyzing over **22,000 experimental data points**, this work addresses the critical challenge of **anisotropy** caused by complex thermal cycles in WAAM. The proposed solution replaces costly destructive testing with a high-precision **Stacked Hybrid Model** that generalizes across six distinct scanning strategies.

---

## Key Features

* **Comprehensive Dataset:** 22,771 time-series data points covering 6 scanning strategies (Base, In-Out, Out-In, Inclined, Longitudinal, Transverse).
* **Novel Architecture:** A **Stacked Hybrid Model** combining **BiLSTM** (Bidirectional LSTM), **GRU** (Gated Recurrent Units), and **XGBoost**.
* **State-of-the-Art Accuracy:** Achieved an **R² of ~1.0000** for Stress prediction, significantly outperforming classical ML models (SVR, RF).
* **Physical Interpretability:** Validated using **SHAP (SHapley Additive exPlanations)** to ensure the model learns fundamental laws of mechanics ($\sigma \propto \text{Load}$, $\epsilon \propto \text{Extension}$).
* **Statistical Validation:** Rigorous **ANOVA** testing proving the model's superiority is statistically significant ($P < 0.05$).

---

## Model Architecture

The champion model utilizes a **Two-Level Stacking Ensemble** approach:

1.  **Level-0 (Feature Extraction):**
    * **BiLSTM Layer:** Captures forward and backward temporal dependencies (e.g., hysteresis loops, elastic-plastic transition).
    * **GRU Layer:** Acts as a filter to summarize complex temporal features efficiently.
2.  **Level-1 (Meta-Learner):**
    * **XGBoost Regressor:** Takes the deep learning predictions + original features to correct residual errors and refine the final output.

---

## Results

| Model | Target | R² Score | RMSE | MAE |
| :--- | :--- | :--- | :--- | :--- |
| **Stacked Hybrid** | **Stress** | **0.976** | **1.65 MPa** | **1.58 MPa** |
| **Stacked Hybrid** | **Strain** | **0.972** | **0.0003** | **0.0003** |
| LSTM | Stress | 0.964 | 2.99 MPa | 2.99 MPa |
| SVR | Stress | 0.912 | 29.56 MPa | 29.56 MPa |

*The hybrid model effectively eliminates the prediction lag often seen in standard RNNs.*

---

## Installation & Usage

### Prerequisites
* Python 3.8+
* Jupyter Notebook / Google Colab

### Installation
1.  Clone the repository:
    ```bash
    git clone [https://github.com/yourusername/waam-tensile-prediction.git](https://github.com/yourusername/waam-tensile-prediction.git)
    cd waam-tensile-prediction
    ```

2.  Install dependencies:
    ```bash
    pip install -r requirements.txt
    ```

### Running the Code
The main logic is contained in `ai_powered_prediction_of_tensile_strength.py` (or `.ipynb`).
1.  Ensure the dataset `BTP Dataset - Sheet1.csv` is in the root directory.
2.  Run the script to train models and generate plots:
    ```bash
    python ai_powered_prediction_of_tensile_strength.py
    ```

---

## Directory Structure

```text
├── data/
│   └── BTP Dataset - Sheet1.csv    # Experimental Data
├── images/                         # Generated plots (Stress-Strain curves, SHAP, etc.)
├── src/
│   ├── models.py                   # Model architectures (BiLSTM, GRU, XGBoost)
│   ├── preprocessing.py            # Scaling and Sequencing logic
│   └── visualization.py            # Plotting functions
├── ai_powered_prediction.py        # Main execution script
├── README.md
└── requirements.txt
