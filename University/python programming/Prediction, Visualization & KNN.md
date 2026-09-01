# 🧠 Quiz Crash Course: Prediction, Visualization & KNN

_Zero-to-ready notes — written like a teacher explaining it to you from scratch, one topic at a time._

> Exam pattern: **10 marks MCQ + 10 marks Short Questions (mostly theory) + 10 marks Output Tracing (code)** This file is organized exactly around that. Every section ends with 🎯 **Likely MCQ points**, ✍️ **Likely short questions**, and 💻 **Output tracing practice** where relevant.

---

## HOW TO USE THIS FILE TONIGHT

Don't read everything word-by-word. Do this:

1. Read the **"In plain English"** box for every topic first — that alone gets you 60% of the marks.
2. Then skim the tables — exams love turning table rows into MCQs.
3. Then run through the 💻 output-tracing snippets — trace them on paper before checking the answer.

---

# PART 0 — The Big Picture (say this if you don't know anything else)

> **In plain English:** This whole course is about one idea: _don't trust a model just because it runs._ You have to (1) define the task properly, (2) split data fairly, (3) beat a simple baseline, (4) draw honest charts, and (5) check _where_ the model fails, not just get one score.

The workflow has 6 stages — memorize this table, it _will_ be an MCQ or short question:

|Stage|What you do|Why (reasoning standard)|
|---|---|---|
|Frame|Define target, features, unit, population, prediction time, action|Task must be meaningful before picking a model|
|Separate|Keep a test set untouched; preprocessing learned only from training data|Prevents information leakage|
|Compare|Test against a simple baseline|Complexity must earn its place|
|Visualize|Pick honest chart encodings|A chart is an argument, not decoration|
|Diagnose|Look at residuals/confusion matrix/uncertain cases|One aggregate score can hide failure|
|Communicate|State results + uncertainty + limits in plain language|Evidence is only useful if understandable|

🎯 **Likely MCQ points**

- Order of the workflow stages (Frame → Separate → Compare → Visualize → Diagnose → Communicate)
- "Complexity must earn its place" ↔ matches the **Compare** stage
- "One aggregate score can hide systematic failure" ↔ matches **Diagnose**

✍️ **Likely short question:** _"Why must a model beat a baseline before being considered useful?"_ **Answer:** Because a high-looking score can be meaningless — if a trivial strategy (like predicting the mean, or always guessing the majority class) does nearly as well, the "complex" model hasn't proven it learned real structure.

---

# PART I — Data-Science Workflow & Linear Regression

## 1. Formulating the Prediction Task

> **In plain English:** Before touching any code, you must be able to answer: _What is one row? What am I predicting? What information do I actually have at the time I predict? Who is this valid for? What happens if I'm wrong?_

|Element|Question|Example (diabetes data)|
|---|---|---|
|Unit of analysis|What does one row represent?|One patient at baseline|
|Target|What are we predicting?|Disease progression 1 year later|
|Features|What's available _at prediction time_?|10 baseline measurements|
|Population|Who is this valid for?|People like the study sample|
|Prediction time|When is the prediction made?|After baseline, before 1-year outcome|
|Action|What decision does this inform?|Research prioritization — NOT auto-treatment|
|Cost of error|How bad are wrong predictions?|Depends on downstream decision|
|Success|What's "good enough"?|Beats baseline, stable, sane errors|

> ⚠️ **Very important line (loves to appear as short-question or MCQ):** **"Prediction is not causation."** A feature can help predict something without _causing_ it. A regression coefficient is NOT automatically a real-world cause-effect number.

🎯 **Likely MCQ points**

- "Prediction ≠ Causation" — trap questions will ask if a coefficient proves causation → **NO**
- Matching each element (unit/target/feature/etc.) to its example

✍️ **Likely short question:** _"Why is 'prediction time' important when choosing features?"_ **Answer:** You can only use information that would actually be available before/at the moment you need to predict — otherwise the model is secretly "cheating" using future information (leakage).

---

## 2. The End-to-End Workflow (9 Steps)

> **In plain English:** This is basically Part 0's 6 stages, broken into more detailed steps. Frame → Get data → Explore (without touching test set) → Split → Baseline → Pipeline (preprocessing+model together) → Cross-validate on training data only → Test ONCE → Diagnose → Communicate & save everything.

**Golden rule (memorize word for word — very testable):**

> "Anything learned from data — means, medians, scaling parameters, selected features, categories, or hyperparameters — must be learned from **training data only**. A pipeline makes this rule executable."

🎯 **Likely MCQ:** Which of these is learned from training data only? (mean for imputation / scaler mean-std / chosen k value) → **All of them**

✍️ **Likely short question:** _"What is a Pipeline in scikit-learn used for, conceptually (not code)?"_ **Answer:** It bundles preprocessing steps (like imputation, scaling) and the model into a single object so that every transformation is _fit_ only on training data and applied consistently — preventing test-data information from leaking into training.

---

## 3–5. Loading Data, Separating X/y, Train/Test Split

> **In plain English:** `X` = your input features (everything except the answer column). `y` = the answer column (target). You then split rows into a training chunk (model learns from this) and a test chunk (model is judged on this, and NEVER trained on it).

**Leakage check — what NOT to include in X:**

- A proxy created _after_ the outcome happened
- A total/sum that secretly contains the target
- An ID that somehow encodes the outcome

**Split types table (very MCQ-friendly):**

|Split type|When to use|Risk if misused|
|---|---|---|
|Random split|Rows are independent of each other|Fails if time/group dependence exists|
|Time split|Predicting the future (deployment)|Data drift may dominate|
|Group split|Same person/site/device appears in multiple rows|Prevents identity leaking across boundary|
|Test size|Balance between training info & evaluation precision|Too small = noisy metric; too big = less training data|

💻 **Output tracing practice**

```python
X = df.drop(columns="target")
y = df["target"]
print(X.shape)   # if df.shape was (442, 11), X.shape = ?
```

**Answer:** `(442, 10)` — because dropping the "target" column removes 1 of the 11 columns.

```python
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.20, random_state=42
)
print(X_train.shape, X_test.shape)
```

If `X.shape == (442, 10)`, then test = 20% of 442 ≈ 88, train ≈ 354. **Answer:** `(354, 10) (88, 10)`

🎯 **Likely MCQ:** `random_state` is used for → **reproducibility** (same split every run), NOT for accuracy improvement.

✍️ **Likely short question:** _"Why must the test set never be touched during model tuning?"_ **Answer:** If you adjust features/hyperparameters based on test performance, the test set effectively becomes part of training — its score is no longer an honest estimate of real-world performance ("test set leakage via repeated peeking").

---

## 6. Baseline Before Linear Regression

> **In plain English:** Before building a "smart" model, build a "dumb" one — like a `DummyRegressor` that just always predicts the mean of the training target. If your fancy model can't beat this, it's useless.

```python
baseline = DummyRegressor(strategy="mean")
baseline.fit(X_train, y_train)
baseline_pred = baseline.predict(X_test)
```

💻 **Output tracing practice:** If `y_train.mean() = 152.0`, what does `baseline_pred` look like? **Answer:** An array of the **same number (152.0) repeated** for every row in `X_test` — DummyRegressor(mean) always predicts the training mean regardless of input.

🎯 **Likely MCQ:** Purpose of a baseline → give metrics a **reference point** to judge if the real model adds value.

---

## 7. Linear Regression Pipeline

```python
regression = Pipeline([
    ("impute", SimpleImputer(strategy="median")),
    ("model", LinearRegression()),
])
regression.fit(X_train, y_train)
```

> **In plain English:** `SimpleImputer` fills missing values (here, with the median of each column, learned from training data only). Then `LinearRegression` fits a straight-line-style equation. Wrapping both in a `Pipeline` ensures the imputer's median is learned only from `X_train`, and reused (not recomputed) on `X_test`.

✍️ **Likely short question:** _"Why include an imputer even if the dataset has no missing values?"_ **Answer:** It's a reusable safety/workflow habit — real-world data often has missing values, and keeping the pipeline structure consistent avoids having to rewrite code later; it also documents an explicit, justified choice.

---

## 8. What Linear Regression Actually Estimates

> **In plain English:** Linear regression draws the "best-fit" straight line/plane: **ŷ = β₀ + β₁x₁ + β₂x₂ + ... + βₚxₚ**. It picks the β (coefficient) values that make the squared differences between real y and predicted ŷ as small as possible.

|Term|Meaning|Watch out for|
|---|---|---|
|Intercept β₀|Prediction when all features = 0|0 might not be a realistic value in real life|
|Coefficient βⱼ|Change in prediction per 1-unit increase in xⱼ, others held fixed|NOT proof of causation; unstable if features are correlated|
|Residual|actual − predicted (eᵢ = yᵢ − ŷᵢ)|Contains noise + unexplained structure|
|Least squares|Minimizes sum of squared residuals|Big errors get extra weight → sensitive to outliers|

🎯 **Likely MCQ:**

- Formula: **ŷ = β₀ + β₁x₁ + ... + βₚxₚ**
- Residual formula: **eᵢ = yᵢ − ŷᵢ** (actual minus predicted, not the other way)
- "Least squares penalizes ___ residuals" → **squared**

💻 **Output tracing:**

```python
y_true = 200
y_pred = 180
residual = y_true - y_pred
print(residual)   # ?
```

**Answer:** `20` (positive residual = model under-predicted)

---

## 9. Regression Metrics (VERY high MCQ/short-question probability)

|Metric|Formula/Units|How to read it|
|---|---|---|
|**MAE**|mean of \|y − ŷ\|, same units as target|typical absolute miss; errors treated linearly|
|**MSE**|mean of (y − ŷ)², squared units|punishes big misses hard; hard to interpret directly|
|**RMSE**|√MSE, target units|punishes big errors but back in real units|
|**R²**|1 − SSE/SST, unitless|relative improvement vs. mean baseline; **can be negative** on test data!|

> **In plain English:** MAE = "on average, how far off am I in real units?" RMSE = same idea but big mistakes count extra. R² = "how much better am I than just guessing the average every time?" — 1.0 is perfect, 0 = same as guessing the mean, **negative = worse than guessing the mean.**

🎯 **Likely MCQ:**

- Which metric can be negative? → **R²**
- Which metric squares the errors? → **MSE (and RMSE, which then square-roots back)**
- "Use ___ when large mistakes should cost disproportionately more" → **RMSE**
- "Use ___ when every unit of error should cost the same" → **MAE**

✍️ **Likely short question:** _"What does R² = 0 mean, and what does R² < 0 mean?"_ **Answer:** R² = 0 means the model performs the same as always predicting the mean. R² < 0 means the model is doing **worse** than that trivial mean-baseline on the test data.

💻 **Output tracing:**

```python
from sklearn.metrics import mean_squared_error
mse = mean_squared_error(y_test, test_pred)
rmse = mse ** 0.5
```

If `mse = 3025`, `rmse = ?` → **55** (√3025 = 55)

---

## 10–11. Comparing Model vs Baseline, and Reading Coefficients

> **In plain English:** Always put baseline and model metrics side-by-side in one table so improvement is obvious. When looking at coefficients, sort by absolute size — but remember, a feature can look "unimportant" (small coefficient) simply because a correlated feature is already carrying similar information. It's **not** a universal importance ranking.

✍️ **Likely short question:** _"Give an example sentence of an 'expected interpretation' after comparing model vs baseline."_ **Answer:** _"On the held-out 20% test set, linear regression reduced MAE relative to the training-mean baseline; the estimate should be confirmed with repeated or cross-validated evaluation."_

---

## 12. Residual Diagnostics

> **In plain English:** After fitting, plot residuals to catch mistakes an aggregate score can't show.

|Pattern seen in residual plot|What it might mean|What to do|
|---|---|---|
|Curved pattern|Relationship isn't really linear|Try transformations/interactions or nonlinear model|
|Fan/cone shape (spread grows)|Error variance changes with prediction level (heteroscedasticity)|Report it; consider transformation|
|Extreme outlier residuals|Data error, outlier, unusual case|Investigate the source, check influence|
|Grouped shifts|Systematic bias for a subgroup|Check that subgroup's features/errors|
|No visible structure|Good sign, but not "proof of correctness"|Still check stability & data shift|

🎯 **Likely MCQ:** A "fan-shaped" residual spread indicates → **heteroscedasticity (non-constant variance)**

---

## 13. Assumptions of Linear Regression (High-yield table — memorize!)

|Assumption|Why it matters|How to check|
|---|---|---|
|Linearity of conditional mean|Linear equation should capture the real pattern|Residual plots, transformations|
|Independent errors|Dependence makes random splits/statistics too optimistic|Check for repeated entities/time/clusters|
|Constant variance|Affects uncertainty estimates|Residual-vs-fitted plot|
|Limited multicollinearity|Correlated features → unstable coefficients|Correlation matrix, regularization|
|Residual normality|Mostly matters for small-sample inference, **not** for point prediction itself|Q-Q plot|
|Representative evaluation|Test score only means something for similar future cases|Sampling design, drift checks|

✍️ **Likely short question:** _"Is residual normality required for linear regression to make good point predictions?"_ **Answer:** No — it mainly matters for classical small-sample statistical inference (confidence intervals/hypothesis tests), not for the point prediction itself.

---

## 14. Cross-Validation & Test-Set Discipline

> **In plain English:** Instead of judging your model on a single train/test split (which could be lucky/unlucky), split the _training_ data into k folds (commonly 5), train on k−1 folds and validate on the last, rotate, and average. This is done ONLY on training data — the real test set is touched exactly once, at the very end.

```python
cv = KFold(n_splits=5, shuffle=True, random_state=42)
scores = cross_validate(regression, X_train, y_train, cv=cv,
                         scoring={"mae": "neg_mean_absolute_error", "r2": "r2"})
cv_mae = -scores["test_mae"]
```

💻 **Output tracing:** Why is there a `-` sign before `scores["test_mae"]`? **Answer:** Scikit-learn's scorer is `neg_mean_absolute_error` (it's negative by convention so that "higher = better" works across all sklearn scorers). Negating it converts back to a normal positive MAE.

🎯 **Likely MCQ:** "Do not tune on the test set" — repeatedly changing hyperparameters because test score improved is called → **test-set leakage / overfitting to the test set**

---

## 15. Reproducibility Checklist (Steps 20–25)

Record: task definition → exact split rule + seed → pipeline (preprocessing+model together, versioned) → baseline & model metrics in real units + validation spread → residual/error documentation → **never claim causality, fairness, or deployment-readiness from accuracy alone.**

---

# PART II — Visualization & Evidence Communication

## 16. Choosing the Right Chart (Extremely MCQ-friendly table)

|Question|Good choice|Bad/misleading choice|
|---|---|---|
|Distribution of values?|Histogram, ECDF, box/violin+points|Bar chart of every individual value|
|Compare categories?|Bar/dot plot with zero baseline|Pie chart with many similar slices / 3D|
|Relationship between 2 numeric vars?|Scatterplot|Line connecting unordered points|
|Change over ordered time?|Line plot, regular time axis|Unordered bars / over-smoothed line|
|Groups' distributions differ?|Faceted histogram/ECDF, box/violin w/ sample size|Only showing group means, no spread|
|How uncertain is an estimate?|Intervals/error bars, method stated|A precise point with no uncertainty shown|

> **In plain English:** Match the _question_ to the _chart type_. Exam loves to give you a scenario ("You want to compare 3 categories precisely") and ask which chart is correct.

## 17. Visual Encoding Hierarchy (memorize the order!)

**Best → worst for precise comparison:** **Position (on aligned scale) > Length > Angle/Area/Volume/Color intensity (hardest to judge accurately)**

Rules:

- Use **position** for values needing precise comparison
- Use **length** for categorical magnitudes from a true zero
- Use **color hue** for categories, NOT fine numeric differences
- Use **lightness/sequential palette** for ordered magnitude
- **Avoid** 3D/volume/decorative area for important quantities

🎯 **Likely MCQ:** Which encoding is easiest for humans to compare accurately? → **Position on a common scale** 🎯 **Likely MCQ:** Color hue is best used for → **categories, not numeric magnitude**

---

## 18. Distribution Plots — Histogram & Boxplot

> **In plain English:** A **histogram** shows the actual shape (overlap, skew, multiple peaks) but can look different depending on bin width. A **boxplot** is compact and great for comparing groups (median, spread, outliers) but _hides individual points and multi-modal shape_.

⚠️ **Key warning line:** "A histogram can look smooth, noisy, unimodal, or multimodal depending on bin width and boundaries. Try defensible alternatives — don't choose bins just because they support your story."

✍️ **Likely short question:** _"What does a boxplot hide that a histogram shows?"_ **Answer:** A boxplot hides the actual shape of the distribution (e.g., whether it's bimodal) and individual data points; it only shows summary stats (median, quartiles, outliers).

---

## 19. Relationship Plots & Overplotting

> **In plain English:** Scatterplots show relationships between two numeric variables. When too many points overlap ("overplotting"), fix it with: transparency (alpha), smaller markers, jitter, hexbin/density plots, or aggregation — and always **say** when you've aggregated.

⚠️ Trend lines summarize a pattern — they do **NOT prove a mechanism** or show every subgroup.

---

## 20. Categorical Comparison — Point + Interval > Bar of Means

> **In plain English:** A plain bar chart of group means hides how many observations were in each group and how uncertain the mean is. A **point plot with a confidence interval** (like `sns.pointplot` with `errorbar=("ci", 95)`) shows both the estimate AND its uncertainty.

⚠️ **Key line:** "A group mean based on 8 observations and one based on 800 should not look equally certain." Always report `n`.

✍️ **Likely short question:** _"Standard deviation vs standard error vs confidence interval — what's the difference?"_

|Quantity|Answers|
|---|---|
|Standard deviation|How spread out are _individual_ observations?|
|Standard error|How variable would the _estimated mean_ be across repeated samples?|
|Confidence interval|Which parameter values are compatible with data+assumptions?|
|Prediction interval|Where might a _new individual_ outcome fall?|

---

## 21. Time-Series Chart Rules (Steps 31–36)

- Sort by time, use a real date axis
- Show missing periods (don't fake-connect across gaps)
- Distinguish totals vs. rates, nominal vs. inflation-adjusted
- Mark interventions; don't imply coincidence = causation
- Don't over-smooth (hides turning points) — label smoothing if used
- Use comparable time windows when contrasting groups

---

## 22. Uncertainty Quantities Table (repeated from #20 — comes up twice, so it's important)

Same table as above. Also: **Cross-validation spread** answers "how does performance change across folds" — and should **not** be treated as a formal statistical confidence interval without justification.

⚠️ **Bootstrap warning:** If data is clustered (by person/site/time), resampling individual rows can _underestimate_ true uncertainty — must preserve the sampling unit.

---

## 23. Accessibility Checklist

Don't rely on color alone (add shape/line-style/labels) → use colorblind-safe palettes → readable axis labels with units → sufficient contrast → write descriptive alt text → remove clutter (3D, redundant legends, excess precision).

**Alt-text template (possible short-question fill-in):**

> "[Chart type] of [variables/population]. [Main comparison/trend + magnitude]. [Important exception/overlap]. [Uncertainty/limitation]."

---

## 24. Misleading Visual Practices (VERY high MCQ yield — memorize this whole table)

|Practice|Why it misleads|Correction|
|---|---|---|
|Truncated bar axis|Length implies magnitude from a hidden non-zero baseline|Start bars at 0, or use labeled points with restricted scale|
|3D bars/pies|Perspective distorts apparent size|Use flat bars/dots/table|
|Dual y-axes|Independent scaling can fake a correlation|Use aligned panels/one scale|
|Cherry-picked dates|Hides prior trend/seasonality/reversal|Show justified full window|
|Mean without spread|Hides heterogeneity, skew, sample size|Show distribution/intervals/counts|
|Unequal bin widths|Raw bar heights become incomparable|Use equal bins or normalize by density|
|Missing categories|Changes apparent composition|Explicitly account for missing/unknown|

🎯 **Likely MCQ:** "Two bar charts show 94 vs 98 — one starts at 0, one starts at 90. Why do they look so different?" → **Truncated (non-zero) baseline exaggerates the visual size of the gap**, even though the actual numeric difference (4 points) is identical.

---

## 25. Systematic Chart Interpretation (6 steps — Identify → Describe → Quantify → Compare → Qualify → Conclude)

> **In plain English:** When asked to "interpret a chart" in the exam: name the chart type/variables/units → describe the pattern (no causal words!) → give approximate numbers → state what it's being compared to → mention uncertainty/outliers/sample size → connect to the question **and say what the chart can't prove.**

---

## 26. Saving Figures

```python
fig.savefig(OUTPUT_DIR / "wine_relationship.png", dpi=300, bbox_inches="tight", facecolor="white")
```

⚠️ Key line: "Save the data-processing and plotting code, not only the image" — a PNG without provenance can't be audited or regenerated.

---

# PART III — K-Nearest Neighbours (KNN) Classification — biggest scoring section, study this hardest

## 27. Classification Task Formulation (Wine example)

|Element|Wine example|
|---|---|
|Unit|One wine sample (13 chemical measurements)|
|Target|Cultivar class: 0, 1, or 2|
|Features|Numeric chemical measurements|
|Prediction point|After measurements, before label known|
|Evaluation|Balanced accuracy + per-class precision/recall/F1 + confusion matrix|
|Limit|Small teaching dataset ≠ real production evidence|

## 28. How KNN Predicts (Steps 43–47 — MUST memorize order)

> **In plain English:** KNN is the "ask your nearest neighbours" algorithm.

1. Compute distance from the query point to all training points
2. Pick the **k** closest training points
3. Look at their labels
4. Predict the **majority vote** (or weight closer ones more if `weights="distance"`)
5. (Optional) Convert votes into probability-like scores

⚠️ **Key line:** "KNN is a lazy learner: fitting largely stores training data; most computation happens at prediction time." (This is a classic MCQ trap — KNN doesn't "learn" a formula like linear regression does.)

🎯 **Likely MCQ:**

- KNN is called a "___ learner" → **lazy**
- Small k → **flexible / low bias / noise-sensitive**; Large k → **smoother / higher bias**

---

## 29. Distance Metrics (High MCQ yield)

|Distance|Formula/Idea|Notes|
|---|---|---|
|Euclidean (p=2)|√Σ(xⱼ−zⱼ)² — straight-line distance|Common default; sensitive to outliers|
|Manhattan (p=1)|Σ\|xⱼ−zⱼ\| — sum of absolute differences|Robust, "grid-like" movement|
|Minkowski|General family controlled by p|Don't tune p on test set|
|Cosine|Angle/direction, not magnitude|Useful in high dimensions; not default here|

**Why scaling matters (VERY testable, appears twice in doc):**

> If one feature (e.g. "proline") ranges in the hundreds and another ranges around 1, raw Euclidean distance is dominated entirely by the big-scale feature. **Standardization** makes a one-standard-deviation change comparable across features (though it doesn't guarantee equal real-world relevance).

```python
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)   # NEVER fit on test data!
```

🎯 **Likely MCQ/output-tracing:** Why is it `scaler.transform(X_test)` and NOT `scaler.fit_transform(X_test)`? **Answer:** Fitting on test data would leak test-set statistics (its mean/std) into preprocessing — violating the training-only rule. Test data must be transformed using parameters learned from **training data only**.

---

## 30. Loading & Splitting Classification Data — Stratification

```python
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.25, random_state=42, stratify=y
)
```

> **In plain English:** `stratify=y` ensures the train and test sets have (roughly) the same **proportion** of each class as the original data — important for classification so a rare class doesn't disappear from one side.

⚠️ **Key trap line:** "Stratification is not a cure." It does NOT fix sampling bias, does NOT create more rare-class examples, does NOT handle grouped/time data, does NOT guarantee fairness.

---

## 31. Classification Baselines

|Baseline|Strategy|What it tells you|
|---|---|---|
|`DummyClassifier(strategy="most_frequent")`|Always predicts majority class|Whether model beats "always guess the common class"|
|`DummyClassifier(strategy="stratified")`|Random guess by training class proportions|How much of accuracy is just class-proportion luck|

---

## 32. Building the KNN Pipeline

```python
knn = Pipeline([
    ("impute", SimpleImputer(strategy="median")),
    ("scale", StandardScaler()),
    ("model", KNeighborsClassifier(n_neighbors=7, weights="uniform", p=2)),
])
knn.fit(X_train, y_train)
pred = knn.predict(X_test)
```

> **In plain English:** Order matters — impute missing values first, THEN scale, THEN classify. During cross-validation, each fold refits the imputer and scaler independently — pre-scaling the whole dataset beforehand would leak validation-fold info into preprocessing.

---

## 33. KNN Hyperparameters (High-yield table)

|Hyperparameter|Option A|Option B|Trade-off|
|---|---|---|---|
|`n_neighbors` (k)|Small k → flexible, low bias, noise-sensitive|Large k → smoother, higher bias, majority-dominated|Choose via training-only validation|
|`weights`|`uniform` = equal vote|`distance` = closer neighbours count more|Distance weighting can amplify close noisy points|
|`p`|1 = Manhattan|2 = Euclidean|Meaning depends on feature scaling/geometry|
|`metric`|Standard numeric distances|Specialized metrics|Must match feature semantics (mixed/categorical needs care)|

🎯 **Likely MCQ:** Setting `weights="distance"` means → **closer neighbours get more voting power than farther ones**

---

## 34. Selecting k via GridSearchCV (training-only, never on test set)

```python
cv = StratifiedKFold(n_splits=5, shuffle=True, random_state=42)
param_grid = {
    "model__n_neighbors": list(range(1, 26, 2)),
    "model__weights": ["uniform", "distance"],
    "model__p": [1, 2],
}
search = GridSearchCV(knn, param_grid, scoring="balanced_accuracy", cv=cv, n_jobs=-1)
search.fit(X_train, y_train)
```

> **In plain English:** `param_grid` lists every combination of settings to try. `GridSearchCV` tries ALL of them using 5-fold cross-validation **on training data only**, and remembers the best one (`search.best_params_`). Notice `model__n_neighbors` — the double underscore refers to the `n_neighbors` parameter _inside_ the pipeline step named `"model"`.

⚠️ **Key line:** "Do not worship the single best k." If several k values perform similarly (within the error bars/std across folds), prefer a simpler/stable region rather than obsessively picking the exact maximum — grid search results have their own uncertainty.

💻 **Output tracing:**

```python
print(len(param_grid["model__n_neighbors"]))
```

`range(1, 26, 2)` = 1,3,5,...,25 → **Answer: 13 values**

Total combinations tried = 13 (k) × 2 (weights) × 2 (p) = **52 combinations**, each evaluated across 5 folds = 260 fits.

---

## 35. Final Evaluation — Use Test Set ONCE

```python
test_pred = best_knn.predict(X_test)
print("Accuracy:", accuracy_score(y_test, test_pred))
print("Balanced accuracy:", balanced_accuracy_score(y_test, test_pred))
print(classification_report(y_test, test_pred, target_names=wine_bundle.target_names))
cm = confusion_matrix(y_test, test_pred)
```

### Classification Metrics Table (⭐ HIGHEST YIELD TABLE IN WHOLE DOCUMENT — will almost certainly be MCQ/short-question material)

|Metric|Question answered|Failure mode|
|---|---|---|
|Accuracy|% of all cases correct|Dominated by common classes|
|Recall (class c)|Of true class-c cases, how many found?|Can be high by over-predicting c|
|Precision (class c)|Of predicted class-c, how many correct?|Can be high while missing many true c|
|F1 (class c)|Harmonic balance of precision & recall|Hides which of the two is weak|
|Macro average|Performance if all classes count equally|Unstable for tiny classes|
|Weighted average|Performance weighted by class size|Can hide poor minority performance|
|Balanced accuracy|Average recall across classes|Doesn't capture precision/cost|

**Formulas worth memorizing:**

- Precision = TP / (TP + FP) → "of what I predicted positive, how much was right"
- Recall = TP / (TP + FN) → "of what was actually positive, how much did I catch"
- F1 = harmonic mean of precision & recall

✍️ **Likely short question:** _"A model has 95% accuracy but the dataset is 95% class A, 5% class B. Is this model good?"_ **Answer:** Not necessarily — this is the "accuracy trap." Always predicting the majority class (A) alone would achieve 95% accuracy while completely failing on class B (0% recall). Balanced accuracy or per-class recall/F1 must be checked.

---

## 36. Reading a Confusion Matrix

```
                Predicted
              c0   c1   c2
True   c0  [ 15    0    0 ]
       c1  [  0   17    1 ]
       c2  [  0    0   12 ]
```

> **In plain English:** **Rows = true/actual class. Columns = predicted class.** Diagonal = correct predictions. Off-diagonal = mistakes. In this example, only ONE mistake: 1 true-class_1 sample was wrongly predicted as class_2.

💻 **Output tracing:**

```python
cm = confusion_matrix(y_test, test_pred)
accuracy = cm.diagonal().sum() / cm.sum()
```

Sum of diagonal = 15+17+12 = 44. Total = 15+17+1+12 = 45. **Answer:** accuracy = 44/45 ≈ **0.978**

Rules to remember: **97, off-diagonal, always label the orientation** — different libraries sometimes flip rows/columns, so always check which axis is "true" vs "predicted."

---

## 37. Class Imbalance

**Accuracy trap (repeats — clearly a favorite exam topic):** classes of size 70/25/5 → always guessing majority gives 70% accuracy but 0% recall on the other two classes.

|Response|When useful|Caution|
|---|---|---|
|Stratified splitting|Stabilizes class proportions in splits|Doesn't fix rarity itself|
|Class-aware metrics|Macro F1/balanced accuracy expose minority issues|No metric replaces real cost analysis|
|More representative data|Improves coverage of rare cases|Must be authorized & representative|
|Resampling (over/under)|Changes training emphasis|Apply within training folds only; risk of overfitting duplicates|
|Distance weighting|Closer neighbours matter more|Not a general imbalance fix; can amplify noise|
|Threshold/cost strategy|Aligns decisions with unequal costs|KNN vote fractions may not be well-calibrated|

---

## 38. Error Analysis Table (predict_proba, confidence, margin)

```python
proba = best_knn.predict_proba(X_test)
ranked = np.sort(proba, axis=1)
confidence = ranked[:, -1]              # highest probability
margin = ranked[:, -1] - ranked[:, -2]  # gap between top 2 classes
```

> **In plain English:** `confidence` = how sure the model was about its top choice. `margin` = how close the top 2 candidate classes were. A **high-confidence error** (model was very sure but still wrong) is the scariest kind of mistake to review.

|Question|Diagnostic|
|---|---|
|Which true classes are missed?|Recall + row-normalized confusion matrix|
|Which predicted classes have false alarms?|Precision + column-normalized confusion matrix|
|Are errors near class overlap?|Feature plots, low vote margins|
|High-confidence errors?|Review labels/outliers/local neighbourhood|
|Do errors cluster by subgroup?|Group-specific metrics|

---

## 39. Inspecting Nearest Neighbours

```python
distances, positions = knn_model.kneighbors(X_test_ready)
```

> **In plain English:** This literally shows you _which_ training rows were the "voters" for a given prediction, and how far away they were. Great for explaining _why_ the model predicted what it did — but remember, "similar" is only defined by the chosen features/metric/scaling, not necessarily real-world similarity.

---

## 40. Dimensionality & Computation

> **In plain English:** More features (dimensions) ≠ always better. In high dimensions, distances start looking similar for everyone ("curse of dimensionality"), and irrelevant/noisy features distort what "nearest" even means. Also, KNN must store ALL training data and search it at prediction time → can be slow/memory-heavy.

⚠️ Key line: don't use a 2D visualization as "proof" the full high-dimensional model behaves the same way.

---

## 41. Probability Outputs & Calibration

> **In plain English:** `predict_proba` in KNN is just the **fraction of neighbours that voted for each class** — NOT a scientifically calibrated probability. 0.8 doesn't necessarily mean "80% chance of being right in reality." A model can rank well but still be over/under-confident numerically.

✍️ **Likely short question:** _"Is a KNN predict_proba value of 0.9 the same as saying there's a 90% real-world chance the prediction is correct?"_ **Answer:** No — it just reflects the vote fraction among the k nearest neighbours, which can be poorly calibrated; true probability calibration must be separately validated.

---

# PART IV — Integrated Workflow (full code, good for output tracing!)

```python
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.25, random_state=42, stratify=y
)
workflow = Pipeline([
    ("impute", SimpleImputer(strategy="median")),
    ("scale", StandardScaler()),
    ("model", KNeighborsClassifier()),
])
cv = StratifiedKFold(n_splits=5, shuffle=True, random_state=42)
search = GridSearchCV(workflow, {...}, scoring="balanced_accuracy", cv=cv, n_jobs=-1)
search.fit(X_train, y_train)
final_model = search.best_estimator_
pred = final_model.predict(X_test)
```

⚠️ **Key line:** This entire pipeline still does NOT prove: fairness, causal validity, robustness to future distribution shift, real-world operational cost, or suitability for high-stakes decisions.

💻 **Output-tracing style question to expect:** _"If `wine.data.shape = (178, 13)` and `test_size=0.25`, how many rows go to `X_test`?"_ **Answer:** 178 × 0.25 = 44.5 → sklearn rounds it → **44 rows** in test, **134** in train (check exact rounding behavior, but ~44/134 split).

---

# PART V — Quick-Fire Reference for the Exam

## Anti-patterns table (great MCQ source — "what's wrong with this code/approach?")

|Anti-pattern|Why it fails|Fix|
|---|---|---|
|Choose model before task|Optimizes technique, not decision value|Define target/time/action/costs first|
|Evaluate only on training data|Measures memorization, not generalization|Use CV + untouched test set|
|No baseline|No reference point|Compare to mean/majority dummy|
|Preprocess before split|Test info leaks into transformations|Preprocessing inside pipeline, per fold|
|Accuracy only|Hides class-specific failure|Report balanced accuracy, confusion matrix|
|Tune on test set|Overfits the reported evaluation|Tune inside training CV only|
|KNN without scaling|Large-unit feature dominates distance|Scale within the pipeline|
|Bar chart with truncated axis|Exaggerates small differences|Start at 0|
|Color-only categories|Fails colorblind/grayscale viewers|Add shape/label/facet|
|Causal coefficient claim|Association ≠ causation|Use causal design or stay predictive|

## Command reference (good for output-tracing / fill-in-the-blank)

|Task|Tools|
|---|---|
|Split|`train_test_split`, `stratify=y`|
|Baseline|`DummyRegressor`, `DummyClassifier`|
|Pipeline|`Pipeline`, `ColumnTransformer`, `SimpleImputer`, `StandardScaler`|
|Regression|`LinearRegression`, `mean_absolute_error`, `mean_squared_error`, `r2_score`|
|Validation|`KFold`, `StratifiedKFold`, `cross_validate`, `GridSearchCV`|
|Charts|`plt.subplots`, `histplot`, `scatterplot`, `boxplot`, `pointplot`, `savefig`|
|KNN|`KNeighborsClassifier`, `n_neighbors`, `weights`, `p`, `metric`|
|Classification metrics|`accuracy_score`, `balanced_accuracy_score`, `classification_report`, `confusion_matrix`|
|Diagnostics|Residual plots, confusion normalization, `predict_proba`, `kneighbors`|
|Reproducibility|`random_state`, `Pipeline`, version metadata|

---

# 🔥 Final 10-Minute Cram Sheet

- **Baseline first, always.** Dummy mean (regression) / majority class (classification).
- **Never fit anything on the test set** — not the imputer, not the scaler, not the model, not hyperparameters.
- **MAE/RMSE/R²** for regression → RMSE punishes big errors more, R² can go negative.
- **Precision/Recall/F1/Balanced Accuracy** for classification → accuracy alone can lie with imbalanced data.
- **Confusion matrix: rows = true, columns = predicted**, diagonal = correct.
- **KNN = lazy learner.** Vote of k nearest neighbours. MUST scale features first (Euclidean distance is scale-sensitive).
- Small k = flexible/noisy; Large k = smooth/biased. Choose k using training-only cross-validation, never the test set.
- **Charts:** position/length = most accurate encoding; avoid truncated axes, 3D, dual y-axes, color-only categories.
- **Prediction ≠ Causation.** Never say a model "proves" cause and effect.
- **Stratify ≠ cure for imbalance** — it only preserves proportions, doesn't fix rarity/bias.
- `predict_proba` in KNN = vote fraction, **not** a guaranteed real-world probability.

Good luck — you now know more than "0 knowledge." Go trace a few code blocks by hand before you sleep; that's the highest-return thing left to do. 💪