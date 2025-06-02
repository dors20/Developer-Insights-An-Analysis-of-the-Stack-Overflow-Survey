# Developer Insights: An Analysis of the Stack Overflow Survey

## About This Project

This project involves the analysis of the Stack Overflow Developer Survey public dataset (`survey_results_public.csv`). The goal is to extract meaningful insights about developers, including their demographics, coding experience, work habits, and preferences. The analysis focuses on data cleaning, preprocessing, and exploratory data analysis (EDA) to understand various aspects of the developer community.

## Dataset

* **Source:** Stack Overflow Developer Survey (publicly available CSV file: `survey_results_public.csv`)
* **Original Columns:** The original dataset contains 85 columns.
* **Selected Columns for Analysis:** For this project, the analysis is focused on a subset of 11 key columns:
    * `Hobbyist`
    * `Country`
    * `Student`
    * `YearsCode`
    * `Age1stCode`
    * `YearsCodePro`
    * `WorkLoc`
    * `Age`
    * `Gender`
    * `WorkWeekHrs`
    * `OpSys` (Operating System)

## Analysis Steps

The Jupyter Notebook (`ids project.ipynb`) performs the following key steps:

1.  **Data Loading:** The `survey_results_public.csv` dataset is loaded into a pandas DataFrame.
2.  **Data Subsetting:** The DataFrame is reduced to the 11 selected columns mentioned above.
3.  **Data Type Inspection and Initial Description:** Basic data types and descriptive statistics are examined.
4.  **Unique Value Analysis:** Unique values for each selected column are explored to understand the categorical and numerical data ranges.
5.  **Missing Value (NaN) Handling:**
    * The number of missing values for each column is identified.
    * Various strategies are employed to fill or handle NaN values:
        * `Student`: Forward fill (`ffill`) method.
        * `YearsCode`: Converted to numeric after removing string entries like 'Less than 1 year' and 'More than 50 years'. NaN values are filled with the mean.
        * `Age1stCode`: Converted to numeric after removing string entries like 'Younger than 5 years' and 'Older than 85'. NaN values are filled with the median.
        * `YearsCodePro`: Initially attempted to fill with mode, then forward fill (`ffill`) for categorical nature.
        * `Gender`: Rows with NaN dropped, then remaining NaNs filled with the mode.
        * `OpSys`: Rows with NaN dropped, then remaining NaNs filled with the mode.
        * `WorkLoc`: Filled with the mode.
        * `Age`: Filled with the mean.
        * `WorkWeekHrs`: Filled with the median.
        * `Country`: Rows with NaN dropped, then remaining NaNs filled with the mode. (The notebook mentions a plan to use multiple logistic regression for `Country` later, but the provided code uses mode.)
6.  **Data Sampling:** The preprocessed dataset (originally ~88,000 rows) is sampled down to 10,000 rows for more manageable analysis and visualization (`data=data.sample(10000)`).
7.  **Data Visualization (Examples):**
    * Bar charts and scatter plots are generated using `matplotlib.pyplot` to show the distribution of developer ages.
    * Bar charts and scatter plots are generated to show the distribution of developer work locations (`WorkLoc`).
    * A bar plot shows the country-wise distribution of developers based on their average age.
    * A regression plot shows the relationship between 'Age' and 'WorkWeekHrs'.
    * Another regression plot shows the relationship between 'Age' and 'Age1stCode'.
    * Value counts for `Hobbyist` are displayed.

## How to Run This Project

### Prerequisites

* Python 3.x
* Jupyter Notebook or JupyterLab
* The following Python libraries:
    * pandas
    * numpy
    * matplotlib
    * seaborn (used for `sns.barplot` and `sns.regplot`)
    * scikit-learn (though `LinearRegression` is imported, its usage beyond fitting is not fully detailed in the provided snippets for prediction/evaluation)

### Setup

1.  **Clone or Download the Repository:** Get the project files, including `ids project.ipynb` and `survey_results_public.csv`.
2.  **Install Libraries:** If you don't have the necessary libraries, install them using pip:
    ```bash
    pip install pandas numpy matplotlib seaborn scikit-learn jupyterlab
    ```
3.  **Place Dataset:** Ensure `survey_results_public.csv` is in the same directory as the Jupyter Notebook, or update the path in the notebook accordingly.

### Execution

1.  **Start Jupyter:** Open your terminal or command prompt, navigate to the project directory, and run:
    ```bash
    jupyter lab
    ```
    or
    ```bash
    jupyter notebook
    ```
2.  **Open Notebook:** In the Jupyter interface, open `ids project.ipynb`.
3.  **Run Cells:** Execute the cells in the notebook sequentially to perform the data loading, preprocessing, analysis, and visualization.

## Key Observations (from the provided code snippets)

* A significant portion of developers in the survey identify as "Yes" for `Hobbyist`.
* The preferred `WorkLoc` appears to be "Office", followed by "Home".
* The age distribution of developers is visualized, providing insights into the age demographics of the surveyed population.
* The analysis attempts to impute missing values using various statistical measures (mean, median, mode) and filling methods.

## Future Work (Potential)

* Implement the planned multiple logistic regression for imputing missing `Country` values.
* Perform more in-depth statistical analysis and hypothesis testing.
* Explore relationships between other variables in the dataset.
* Apply machine learning models for predictive tasks (e.g., predicting salary, job satisfaction, based on developer characteristics, though these columns were not in the selected subset).
* Enhance visualizations for clearer communication of insights.
