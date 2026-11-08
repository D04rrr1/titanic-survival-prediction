# Titanic Survival Prediction | Machine Learning Portfolio Project

A reproducible Python project that investigates passenger survival patterns in the Titanic dataset and compares a Random Forest baseline with a three-model ensemble.

> **This is a learning and experimentation project, not a claim of perfect prediction.** The project includes honest reporting of cross-validation results, Kaggle public scores, data-leakage concerns, and unsuccessful experiments.

## Research question

**How accurately can passenger characteristics predict survival on the Titanic, and which modeling choices generalize beyond the training passengers?**

## What I built

- Explored missing values and survival patterns by sex and passenger class using **pandas** and **matplotlib**.
- Engineered `FamilySize`, `IsAlone`, `Title`, `TicketGroupSize`, and `Deck` features.
- Built preprocessing pipelines with **median imputation**, **most-frequent categorical imputation**, and **one-hot encoding**.
- Compared a **Random Forest baseline** with a **soft-voting ensemble** (Gradient Boosting, Random Forest, Extra Trees).
- Evaluated the models using **StratifiedGroupKFold** so passengers sharing tickets stay together during validation.
- Analyzed held-out errors with a **confusion matrix** and accuracy by passenger group.
- Generated a competition-formatted CSV with 418 predictions.

## Results (recorded from earlier Kaggle experiments)

| Metric | Observed result | Interpretation |
|---|---:|---|
| Best confirmed Kaggle public score | **0.77033 (77.03%)** | From an earlier submission, not automatically the model in the cleaned notebook |
| Original ensemble: grouped CV, seeds 101 and 303 | **83.46%** | Mean of 10 fold scores across two grouped-split configurations |
| Original ensemble: repeated stratified CV | **83.67%** | Different evaluation design; not a Kaggle public score |
| Tuned Gradient Boosting: searched CV | **84.51%** | Selected after hyperparameter search; optimistic as a model-selection score |
| Tuned Gradient Boosting: Kaggle public score | **0.75358 (75.36%)** | Shows validation accuracy does not guarantee public leaderboard accuracy |

These historical results come from the project's exploratory notebooks and screenshots. **Run the clean notebook to produce its own current validation numbers.** The final selection and new `submission.csv` in the cleaned notebook have **not** been verified with an official Kaggle public score.

The complete experiment record, including unsuccessful approaches, is in [`results/experiment_log.md`](results/experiment_log.md).

## Reproduce the notebook

**Kaggle (recommended):**

1. Open [Titanic — Machine Learning from Disaster](https://www.kaggle.com/competitions/titanic) and join the competition.
2. Create or import a Kaggle notebook using [`notebooks/Titanic_Survival_Portfolio.ipynb`](notebooks/Titanic_Survival_Portfolio.ipynb).
3. Attach the **official Titanic competition data** using **Add Input**. The notebook looks for files under `/kaggle/input/competitions/titanic` or `/kaggle/input/titanic`.
4. Select **Run All**. Inspect the validation results and error analysis.
5. The last code cell creates `/kaggle/working/submission.csv`. This **does not submit anything automatically**.

**Locally:** Install the packages in `requirements.txt`, place `train.csv` and `test.csv` from the Kaggle competition under a local `data/` folder, then run the notebook with Jupyter.

## Repository structure

```text
Titanic_Survival_Portfolio/
├── README.md
├── notebooks/
│   └── Titanic_Survival_Portfolio.ipynb
├── results/
│   └── experiment_log.md
├── requirements.txt
└── .gitignore
```

Raw competition data, submissions, and large notebook output files are deliberately not included in this repository.

## Methodological considerations

- **No historical survival lookups:** This clean notebook does **not** use the true outcomes of competition-test passengers or the known survival status of their companions to make predictions.
- **Transductive feature:** `TicketGroupSize` counts ticket appearances across the supplied train and test feature tables, without using target outcomes. This may not generalize to settings where all prospective records are not available together.
- **Validation and leaderboard are not interchangeable:** Kaggle's public evaluation subset differs from group-aware held-out folds.
- **Model selection bias:** Many ideas and hyperparameters were tested on the same small dataset. Treat selected CV numbers as descriptive estimates, not independent proof of generalization.
- **Transparency:** A separate V7 exploratory notebook tested adjustments using known companion outcomes; that approach is retrospective and is not included in the clean model.

## What I learned

This project taught me that **higher training or validation accuracy does not guarantee better performance on unseen test data**. Clear methodology, reproducible preprocessing, and careful analysis of overfitting and leakage are as important as model complexity.

## Dataset and attribution

Dataset: [Kaggle Titanic — Machine Learning from Disaster](https://www.kaggle.com/competitions/titanic). See Kaggle's competition page for rules and data terms. Techniques were studied alongside public Kaggle notebook discussions, but the cleaned code is organized around this project's own sequence of experiments.
