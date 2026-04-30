# NBA Sports Analytics Project

## Project Overview
- This project analyzes NBA team statistics to identify patterns related to winning.
- It combines data visualization and machine learning to better understand team performance and predict game outcomes.
- The prediction task is a binary classification problem: win or loss.

## Dataset
- Main dataset: `db/nba_team_stats_advanced.csv`
- Target variable: `wl`
- Encoded target: `win_flag`
  - `W = 1`
  - `L = 0`
- Features used for modeling:
  - `offRating`
  - `defRating`
  - `pace`
  - `astTo`
  - `rebPct`
  - `tsPct`
  - `efgPct`

## Project Structure
- `Project Assignments/`
  - `P1_relplot_scatter.ipynb`
    - Exploratory data analysis and relationship plots
  - `P2_categorical-plot_pl.ipynb`
    - Categorical plots and additional visual analysis
  - `P3_interactive.ipynb`
    - Interactive visualizations and the final machine learning pipeline
- `db/`
  - CSV dataset files used in the project

## Machine Learning Approach
- Machine learning is implemented inside `P3_interactive (updated).ipynb`
- Models used:
  - Logistic Regression
  - Random Forest
  - Support Vector Classifier (SVC)
- Preprocessing:
  - `StandardScaler`
  - scikit-learn `Pipeline`
- Data split:
  - 80/20 train-test split
  - Stratified to preserve class balance
- Validation:
  - 5-fold `StratifiedKFold`
- Evaluation metrics:
  - Accuracy
  - Precision
  - Recall
  - F1-score
  - ROC-AUC
- Model evaluation also includes a confusion matrix visualization

## Results
- The models showed strong overall performance in predicting NBA game outcomes.
- The best-performing model achieved high accuracy with very few misclassifications.
- These results suggest that team-level efficiency metrics are strong predictors of wins and losses.

## How to Run
- Make sure the dataset files are placed in the `db/` folder.
- Open the notebooks in Jupyter Notebook, JupyterLab, or Google Colab.
- Run the notebooks in order:
  - `P1_relplot_scatter.ipynb`
  - `P2_categorical-plot_pl.ipynb`
  - `P3_interactive.ipynb`
- Run all cells in `P3_interactive.ipynb` to view the interactive analysis and machine learning workflow.

## Requirements
- pandas
- numpy
- scikit-learn
- matplotlib
- seaborn

## Contributors
- Jake Crumley
- Matija Malisic
- Sumit Shrestha
- Carter Alemania
