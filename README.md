# Automated Data Cleaning Pipeline for Revenue Projections

This project creates an automated data cleaning pipeline for preparing revenue projection data, enabling streamlined reporting and analysis in Power BI. The pipeline cleans raw data, handles missing values, and calculates cumulative revenue figures.

## Project Objective

The objective of this project is to create a data cleaning pipeline that processes raw revenue data, transforming it into a format suitable for reporting. This includes handling missing values, formatting, and calculating cumulative values for revenue analysis.

## How to Achieve the Objective

1. **Load Raw Data**: Import revenue data from `raw/revenue_report.csv`.
2. **Data Cleaning**:
   - Standardize date formats in the `Month` column.
   - Fill missing `Projected_Revenue` values using forward-fill to ensure consistent projections.
   - Replace missing `Actual_Revenue` values with `0` for periods with no revenue.
3. **Data Transformation**:
   - Calculate cumulative sums for `Projected_Revenue` and `Actual_Revenue` within each `Region`, enabling comprehensive analysis.
4. **Save Cleaned Data**: Output the cleaned data as a new CSV file in the `cleaned` directory, ready for use in Power BI or other analytics tools.

## Tools and Libraries Used

- **Python**: Programming language used for scripting the data cleaning pipeline.
- **pandas**: For data manipulation, handling missing values, and performing cumulative calculations.
- **logging**: To track each step in the data cleaning process and log any issues.
- **Jupyter Lab**: To run the script in a notebook environment and inspect intermediate steps.

## Setup and Requirements

To set up the project, ensure that the following Python packages are installed:

```bash
pip install pandas jupyterlab

You’ll also need to clone this repository and create the necessary directories:

# Clone the repository
git clone https://github.com/yourusername/revenue-cleaning-pipeline.git

# Navigate to the project directory
cd revenue-cleaning-pipeline

# Create the raw and cleaned directories if they don’t exist
mkdir -p raw cleaned


```

Place the raw data file `(revenue_report.csv)` in the raw directory.

## Running the Project
Open Jupyter Lab:

```bash
jupyter lab
```

## Run the Data Cleaning Notebook:

Open the Jupyter notebook and execute each cell to load, clean, transform, and save the data.

## Check the Output:

After running the notebook, the cleaned dataset will be saved in the cleaned/cumulative_revenue_report.csv file.
A log file (data_cleaning.log) will be generated to record all actions performed during the cleaning process.
Project Workflow

**1. Loading Raw Data**

Load raw revenue data from raw/revenue_report.csv using pandas.read_csv.

**2. Data Cleaning Steps**

Date Standardization: Convert the Month column to a consistent datetime format.
Forward Fill Projected Revenue: Fill missing Projected_Revenue values using forward-fill within each Region.
Fill Actual Revenue with Zeroes: Replace missing values in Actual_Revenue with 0 to indicate months with no revenue.

**3. Data Transformation Steps**

Calculate Cumulative Revenue: For each Region, compute cumulative values for both Projected_Revenue and Actual_Revenue.

**5. Saving the Output**

Save the cleaned and transformed data to cleaned/cumulative_revenue_report.csv for use in analytics platforms like Power BI.

Example Code Snippets
Here's a quick look at the code used for data cleaning and cumulative calculations:

``` python
# Load data
df = pd.read_csv('raw/revenue_report.csv')

# Data Cleaning
df['Month'] = pd.to_datetime(df['Month'], errors='coerce', format='%Y-%m')
df['Projected_Revenue'] = df.groupby('Region')['Projected_Revenue'].transform(lambda x: x.ffill())
df['Actual_Revenue'] = df['Actual_Revenue'].fillna(0)

# Cumulative Calculations
df['Cumulative_Projected_Revenue'] = df.groupby('Region')['Projected_Revenue'].transform('cumsum')
df['Cumulative_Actual_Revenue'] = df.groupby('Region')['Actual_Revenue'].transform('cumsum')

# Save cleaned data
df.to_csv('cleaned/cumulative_revenue_report.csv', index=False)

```

Then you may proceed with visualizing the data using BI tool such as PBI/Tableau . 

## Data Visualization 

WIP

## License
This project is licensed under the MIT License - see the LICENSE file for details.
