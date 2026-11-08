# Experiment log — Titanic survival prediction

The following numbers were observed in Kaggle notebook outputs and conversation screenshots during project development. They are **not** independent reproductions from this packaged notebook.

| Stage | Model / experiment | Evaluation | Observed result | Lesson |
|---|---|---|---:|---|
| V1 | Random Forest baseline | Single 80/20 validation split | 78.21% | First predictive model |
| V1–V3 | Early submissions | Kaggle public leaderboard | **77.03%** best confirmed | Public scores differ from local validation |
| Tuned GB | RandomizedSearchCV | Chosen 5-fold CV score | 84.51% | Tuned score may be optimistic |
| Tuned GB | Same tuned model | New repeated stratified CV | 82.27% | Model-selection bias / split variability |
| Tuned GB | Submission | Kaggle public leaderboard | 75.36% | Higher CV did not improve public test performance |
| Ensemble | GB + RF + ET | Repeated stratified CV | 83.67% | Ensemble improved on these splits |
| Ensemble | GB + RF + ET | Ticket-group CV, seed 42 | 81.39% | Group splits can be harder |
| V4 | More numerical/categorical features | Ticket-group CV, seeds 7 & 2026 | Advanced 82.05% vs original 82.26% | Extra features did not help consistently |
| V5 | Age/family/title interactions | Ticket-group CV, seeds 101 & 303 | V5 82.69% vs original 83.46% | More complexity reduced results |
| V6 | Title/class age imputation | Group CV, two seeds | 82.13% vs baseline 82.18% | No meaningful gain |
| V6 | Multi-seed ensemble | Group CV, two seeds | 81.74% vs baseline 82.18% | Multi-seed approach did not help |
| V7 | Companion-outcome adjustment | Ordinary stratified CV, 10 folds | 84.85% vs baseline 84.40% | Retrospective group outcome signal can help locally |
| V7 | Same group adjustment | Strict ticket-group CV | 83.35% vs baseline 83.35% | No known same-ticket companions in held-out ticket groups |
| V7 | Notebook submission | Kaggle public leaderboard | 76.315% | Submitted notebook score; precise selected output CSV was not independently verified in screenshot |

## Validation caveats

- **Different metrics and splits must not be compared as if identical.** Report how each number was calculated.
- **Repeated model selection on small data makes CV estimates optimistic.** A final untouched test set is unavailable locally because Kaggle holds back target labels.
- **V7 companion-survival signals are retrospective.** They use known survival outcomes of related passengers and should not be described as predictions based only on pre-disaster characteristics.
- **TicketGroupSize is transductive.** It counts all provided competition records; no survival outcomes are used.
- **Original Kaggle score of 0.77033** belongs to previous submitted notebooks; the clean GitHub notebook's new selected model is not yet leaderboard-tested.

## Practical conclusion

The main outcome is a reproducible end-to-end workflow and a better understanding of cross-validation, model-selection bias, and data leakage—not a claim of state-of-the-art leaderboard accuracy.
