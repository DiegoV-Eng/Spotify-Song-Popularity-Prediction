## Exploratory Data Analysis

1. **Environment Setup and Data Import**
   - Configure the programming environment.
   - Import essential libraries for data analysis and visualization.
   - Load the raw dataset "integrated_data.csv".

2. **Data Preprocessing**
   - Split the "release_date" column into year, month, and day components.
   - Remove unnecessary columns ("Unnamed: 0," "release_date," and "day").
   - Eliminate rows with missing values in specific columns.
   - Convert the "year" and "month" columns to integers.
   - Transform the "duration_ms" column into "duration_m" by dividing by 60,000 to represent song duration in minutes.

3. **Handling Numerical Data**
   - Address outliers in the "loudness" column by filtering values within the range of -60 to 0.
   - Filter out songs with a tempo value of 0.
   - Create visualizations to understand the distributions of numerical features.
   - Calculate a weighted mean for song duration by year.

4. **Handling Categorical Data**
   - Apply one-hot encoding to categorical variables "key" and "mode" to convert them into binary variables.

5. **Feature Selection**
   - Utilize two methods for feature selection:
     - **Correlation-Based Feature Selection:** Identify features with strong positive or negative correlations with the target variable "popularity."
     - **Tree-Based Model Feature Selection:** Evaluate feature importance using Decision Tree and Random Forest models.

6. **Informative Visualizations**
   - Create visualizations, including popularity distributions, box plots, scatter plots, mean popularity by year, mean popularity by season, and mean popularity by artist to gain insights into the dataset.

7. **Categorization**
   - Categorize the "popularity" target variable into three labels: "low," "medium," and "high" for simplified analysis.

8. **Addressing Class Imbalance**
   - Apply oversampling techniques (Random Oversampler and SMOTE) to address class imbalance and improve classification model robustness.

9. **Data Normalization**
   - Standardize certain numerical features like "duration_m," "loudness," and "tempo" to ensure consistent scaling for modeling and analysis.

10. **Model Building and Prediction**
   - Create a design matrix by selecting the most significant features.
   - Implement a K-Nearest Neighbors (KNN) classifier for popularity category prediction.
   - Split the data into training and testing sets and evaluate model accuracy.
   - Perform cross-validation to assess the KNN classifier's performance with various k values (number of neighbors).

The [EDA_Final.ipynb](https://github.com/dmml-heriot-watt/group-coursework-machine-learners/blob/main/notebooks/EDA/EDA_Final.ipynb) offers a comprehensive analysis of a music dataset, covering data preparation, visualization, feature selection, and predictive modeling to provide insights into music popularity trends.
