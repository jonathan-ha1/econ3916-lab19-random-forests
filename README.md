# Tree-Based Models: Random Forests

## Objective
This lab compares a single decision tree, OLS, Ridge and a random forest on California Housing to see whether the forest's added complexity gives better predictions, how two measures of feature importance disagree, and how much tuning by cross-validation changes the result.

## Methodology
- Split the 20,640 California Housing block groups into 16,512 training rows and 4,128 test rows, using 8 features to predict the median house value.
- Fit a single decision tree with no depth limit, OLS, Ridge behind a StandardScaler, and a random forest of 100 trees on the same training rows, then scored each on both sets by RMSE and R².
- Compared the forest's feature importance two ways, by impurity, which is measured on the training rows, and by permutation, which shuffles each feature on the test rows and records the fall in R².
- Tuned the forest's max_depth and max_features with 3-fold cross-validation using GridSearchCV, then scored the winning forest on the test rows.
- Wrote a prompt asking an AI for a function that charts a model's permutation importances and returns them as a table, then checked its numbers against the lab's own results.

## Key Findings
- The single tree had a test R² of 0.6228 after memorizing its training rows with almost one leaf per row, Ridge reached 0.5758, and the random forest reached 0.8046, so averaging many trees beat both the single tree and the linear models by a wide margin.
- Latitude scored only 0.0890 by impurity but 0.4427 by permutation, because its effect works together with Longitude through many deep splits that each reach only a few training rows, so impurity undercounts how much the forest's predictions depend on it.
- The tuned forest reached a test R² of 0.8094, a small gain that came from letting each split choose from half the features instead of all eight.
- The AI's function took 2 rounds, and in both rounds every importance matched the lab's numbers exactly at +0% apart, including on a different model and rows it had never seen.
