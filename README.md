# Student Performance Prediction System

A machine learning project that predicts a student's final academic grade using demographic, social, and school-related information from the UCI Student Performance dataset.

The project is implemented in a Jupyter Notebook and uses a **Linear Regression** model with a preprocessing pipeline for numerical and categorical features.

## Overview

The notebook fetches the Student Performance dataset from the UCI Machine Learning Repository using `ucimlrepo`, prepares the features, trains a regression model, evaluates its predictions, and demonstrates how to predict a final grade for an individual student.

### Project workflow

1. Fetch the dataset from the UCI Machine Learning Repository.
2. Separate the input features from the target.
3. Predict the final grade (`G3`) while excluding the earlier-period grades (`G1` and `G2`) from the model inputs.
4. Remove rows with missing target grades and remove columns that contain no values.
5. Split the data into training and testing sets.
6. Impute missing numerical and categorical values and one-hot encode categorical features.
7. Train a Linear Regression model.
8. Evaluate performance using MAE, RMSE, and R².
9. Compare actual and predicted grades in a table and scatter plot.
10. Demonstrate an individual prediction and a reusable prediction function.

## Dataset

- **Source:** [UCI Machine Learning Repository — Student Performance](https://archive.ics.uci.edu/dataset/320/student+performance)
- **Dataset ID:** `320`
- **Target:** `G3`, the final grade
- **Grade scale used by the notebook:** 0–20

The notebook downloads the dataset at runtime with `fetch_ucirepo(id=320)`. An internet connection may therefore be required when running it for the first time.

The model deliberately excludes `G1` and `G2` (earlier-period grades) from the input features, with the aim of making a prediction without relying on those grades.

## Technologies

- **Python** — programming language
- **Jupyter Notebook** — interactive development and execution
- **pandas** and **NumPy** — data handling
- **Matplotlib** and **Seaborn** — data visualization libraries (Matplotlib is used for the evaluation plot in the current notebook)
- **scikit-learn** — preprocessing, model training, and evaluation
- **ucimlrepo** — retrieving the UCI dataset

## Model and preprocessing

The notebook uses a scikit-learn `Pipeline` containing a `ColumnTransformer` and `LinearRegression`.

| Feature type | Preprocessing |
|---|---|
| Numerical | Missing values are filled with the median |
| Categorical | Missing values are filled with the most frequent value, then one-hot encoded |
| Unseen categories | Ignored by `OneHotEncoder(handle_unknown="ignore")` |

The dataset is split into **80% training data** and **20% test data**, using `random_state=42` for reproducibility.

### Evaluation metrics

The notebook reports:

- **Mean Absolute Error (MAE):** average absolute difference between actual and predicted grades.
- **Root Mean Squared Error (RMSE):** gives greater weight to larger prediction errors.
- **R² score:** measures how well the model explains variation in the test-set grades.

The metric values are calculated when the notebook runs; they are not fixed in this README because they depend on successful dataset retrieval and execution.

## Getting started

### 1. Clone the repository

```bash
git clone https://github.com/rudy0senpai/Student-Performance-Prediction-System.git
cd Student-Performance-Prediction-System
```

Replace the URL and folder name with your GitHub repository details.

### 2. Create and activate a virtual environment (recommended)

**Windows PowerShell**

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

**Linux / macOS**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
python -m pip install --upgrade pip
python -m pip install jupyter pandas numpy matplotlib seaborn scikit-learn ucimlrepo
```

### 4. Launch Jupyter Notebook

Open the notebook included in the repository:

```bash
jupyter notebook
```

Then open `Student_Performance_Prediction_System(2).ipynb` and run the cells from top to bottom.

> **Tip:** If you rename the notebook to something simpler, such as `student_performance_prediction.ipynb`, use that new filename in your repository and documentation.

## Making a prediction

The notebook defines a reusable function named `predict_student_performance()`. It accepts a dictionary containing feature names and values that match the model's input columns and returns a predicted grade clipped to the 0–20 range.

Example from the notebook:

```python
example_student = X_test.iloc[0].to_dict()
predicted_grade = predict_student_performance(example_student)
print(f"Predicted final grade: {predicted_grade:.2f} / 20")
```

This example reuses a row from the test set. To predict for a new student, provide a dictionary of appropriate feature values using the same feature names and value formats as the dataset.

## Repository structure

```text
.
├── README.md
└── Student_Performance_Prediction_System(2).ipynb
```

Your repository may include additional files as you develop the project.

## Limitations and responsible use

- This is an educational machine learning project, not a validated academic decision system.
- Predictions are estimates, not guaranteed outcomes. They should not be used as the sole basis for grading, admissions, discipline, or other consequential decisions about students.
- Model performance depends on the dataset, its representativeness, and the selected features.
- A random train/test split provides a basic evaluation; it does not establish that the model generalizes to every school, region, or student population.
- The notebook clips the displayed individual prediction to the 0–20 grade range. This range restriction does not make the prediction inherently accurate.
- Student data can be sensitive. Avoid publishing personally identifiable information, and follow applicable data-protection and institutional policies when using real student records.

## Future improvements

Potential next steps include:

- Compare Linear Regression with models such as Random Forest Regressor and Gradient Boosting.
- Add cross-validation and systematic hyperparameter evaluation.
- Examine residuals and error patterns across relevant student groups.
- Add a clear input-validation layer for new student records.
- Save and load the trained pipeline for reuse without retraining.
- Build a simple web interface for entering student features and viewing predictions.

## Contributing

Contributions and suggestions are welcome. For substantial changes, consider opening an issue first to discuss the proposed improvement.

## License

No license is specified in the current notebook. Before publishing the repository, add a `LICENSE` file if you want to state the terms under which others may use, modify, and distribute your code. Check the dataset's source terms separately.
