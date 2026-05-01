# Team Sport Analytics — Project Summary

**Group:** Team Sport Analytics  
**Members:** Sumit Shrestha, Jake Crumley, Matija Malisic, Carter Alemania  
**Course:** CS 133  
**Dataset:** NBA team advanced stats (`db/nba_team_stats_advanced.csv`), supported by `db/nba_player_stats.csv` and `db/nba_quarter_scores.csv`. Source: NBA.com via the `nba_api`, mirrored on Kaggle ("Historical NBA Data and Player Box Scores," Eoin Amoore).

---

## Five Analytical Questions

1. **Is home court advantage real?**
2. **Does scoring early help you win?**
3. **What is the distribution of player ages on winning teams?**
4. **Who will win the 2026 MVP?**
5. **Who will win the 2026 NBA Finals?**

---

## Results of the Five Questions

The visualizations and analysis across `P1_relplot_scatter.ipynb`, `P2_categorical-plot_pI.ipynb`, and `P3_interactive (updated).ipynb` produced the following findings.

### Result 1 — Home court advantage

Using the `matchup` field in `nba_team_stats_advanced.csv` home teams win at a noticeably higher rate than away teams across the dataset. The relplot exploration in P1 also shows home teams clustering at slightly higher Offensive Ratings on average, supporting the idea that home court delivers a real but moderate efficiency boost rather than a dominant effect.

### Result 2 — Does scoring early help you win?

Using `nba_quarter_scores.csv`, we examined Q1 scoring relative to final outcome. Teams that won Q1 went on to win the game more often than not, but the relationship is far from deterministic. as fourth quarter scoring matters at least as much. The categorical plot in P2 (Q2) showed the **Cleveland Cavaliers** lead the league in average 4th quarter points for the 2025-26 season, closely followed by the **Minnesota Timberwolves**, reinforcing that late game scoring is a strong differentiator at the top of the league. So early scoring helps, but it is not the single deciding factor.

### Result 3 — Player age distribution on winning teams

From `nba_player_stats.csv`, the age distribution on winning teams skews toward the **late 20s prime range** (roughly 26 to 30), with a noticeable secondary mass of veterans 31+. youth movements appear less often among consistent winners. This matches the conventional view that championship teams stars with experienced role players.

### Result 4 — 2026 MVP prediction

*This question was scoped down during the project.* Predicting MVP would require season long player modeling and voter behavior analysis, which was outside the scope of our game level win/loss pipeline. As a partial substitute, our P2 categorical analysis highlighted standout team performances that may point to MVP level contributors. A full MVP model is listed in **Future Work**.

### Result 5 — 2026 NBA Finals prediction

*This question was also scoped down.* Predicting a champion would require playoff simulation, seeding logic, matchup modeling, and multi game prediction, which we did not implement. However, our pipeline shows that per game outcomes are highly learnable from team efficiency metrics, making playoff Monte Carlo simulation the most natural extension of the project.

### Synthesis

The visual results across all five questions pointed to a small set of efficiency oriented features (`offRating`, `defRating`, `pace`, `astTo`, `rebPct`, `tsPct`, `efgPct`) as the strongest team level predictors of winning. That feature set is what we carried into the machine learning pipeline.

---

## Machine Learning Results

Three models were trained inside a scikit-learn `Pipeline` with `StandardScaler`, using an 80/20 stratified train/test split and 5-fold `StratifiedKFold` cross-validation:

- **Logistic Regression** — baseline linear model, chosen as a benchmark per the project proposal.
- **Random Forest** — non linear tree ensemble.
- **Support Vector Classifier (SVC)** — margin based non linear comparison.

All three models achieved strong performance across accuracy, precision, recall, F1, and ROC-AUC. The best performing model was tested on the held out 20% test set and produced a confusion matrix dominated by correct predictions with very few misclassifications, confirming that team level efficiency metrics are highly predictive of in game win/loss outcomes.

---

## Conclusion

Overall, this project showed that NBA game outcomes can be predicted reasonably well using team level efficiency metrics. Although we scoped down the MVP and Finals prediction questions, the final pipeline still answered the core goal of building a game level win/loss predictor. The results show that statistics like offensive rating, defensive rating, pace, and other efficiency based features can capture meaningful differences between teams.

While the project does not fully solve season level forecasting, it creates a strong foundation for future work. A natural next step would be adding player level data for MVP prediction and using the game level model inside a playoff Monte Carlo simulation for Finals forecasting. In the end, our pipeline demonstrates that NBA outcomes are learnable at the game level and can be expanded into more advanced season level predictions.

---

## References

- NBA Stats — https://www.nba.com/stats
- Kaggle — "Historical NBA Data and Player Box Scores" by Eoin Amoore — https://www.kaggle.com/datasets/eoinamoore/historical-nba-data-and-player-box-scores
- `nba_api` Python client — https://github.com/swar/nba_api
- scikit-learn (Pedregosa et al., 2011) — https://scikit-learn.org
- pandas, NumPy, Matplotlib, Seaborn, Plotly, Panel, geopy — standard Python data-science stack
