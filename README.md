# Pymaceuticals-Python

## Overview
This repository contains the analysis of a recent animal study conducted by Pymaceuticals, Inc., focusing on the effectiveness of various drug regimens for treating squamous cell carcinoma (SCC), a common form of skin cancer. The study involved 249 mice undergoing treatment with different medications over a 45-day period.

## Objective
The goal is to clean data tables and different plots for analysis. The primary goal is to compare the performance of the company's drug of interest, Capomulin, against other treatment regimens.


## Tasks
1. **Data Aggregation**: Prepare the data (datasets merg, removing duplicates, data cleaning), generate summary statistics (mean, median, var, sem, std), creating bar, pie charts, calculate Quartiles, find Outliers, and create a Box Plot.
2. **Trend Identification**: Analyze key metrics to uncover drugs' performance, including:
   - Highlighting the tumor development trends associated with each treatment.
   - Comparison Capomulin, against other treatment regimens.
3. **Insights Generation**: Summary statistics for the treatment effects, Effectiveness of Capomulin.

## Analysis Approach
- **Summary staistics for the treatment effects**: Compare how effectiveness each drug type affect the tumor growth.
- **Data Visualization**: Use visual tools to illustrate the equality in study, reducing the bias in result. Displaying correlation coefficient to prove a strong positive relationship between mouse weihgt and average tumor volume.
- **Statistical Analysis of Capomulin vs other drugs**: Outliers could either indicate extreme cases of drug inefficiency or effectiveness, or they might suggest data entry errors. Capomulin treatment, the IQR shows that central tendency is fairly consistent and less variability.
  
## Tools and Technologies
- **Python**: For data manipulation, analysis, and visualization.
- **Pandas**: For efficient data handling and aggregation.
- **Matplotlib**: For creating meaningful visualizations of the data.
- **Jupyter Notebook**: For an interactive analysis environment.

## Expected Outcomes
This analysis aims to provide the executive team with a clear understanding of the clinical study results:
- The efficacy of Capomulin in treating compared to other treatments.
- Promising results of Capomulin, further studies could explore dosage optimization, long-term effects.

## How to Use This Repository
1. Clone the repository:
    ```bash
    git clone https://github.com/hiepxuanho/Pandas-challenge
    
    ```
2. Install/Imported the required dependencies:
    ```bash
    pip install --upgrade ipython
    pip install --upgrade notebook

    import matplotlib.pyplot as plt
    import pandas as pd
    ```
3. Open and run the Jupyter notebooks to explore the analysis and visualizations.
    ```bash
    conda activate dev
    jupyter notebook
    ```

## Note:

I got confused at the instruction "Our data should be uniquely identified by Mouse ID and Timepoint". I did know that we definitely needed to use duplicate() function, but I had no idea how to return the right result since the data should be uniquely indentified both Mouse ID and Timepoint. 

After getting explanation from the professor, I realize that inorder to identify duplicate rows where the combination of Mouse ID and Timepoint shows up more than once. However, I only knew how to use duplicated() function with one condition.

Therefore I had to look up on Chat GPT on how to solve this question. It gave me the result of using duplicated() function with a subset = ["Mouse ID", "Timepoint"]. In this way, we can find the duplicate not only on Mouse ID but also Timepoint as well.

/------------Chat GPT code---------------------------/

duplicate_mice = mouse_study_complete[mouse_study_complete.duplicated(subset=['Mouse ID', 'Timepoint'], keep=False)]

/----------------------------------------------------/

And for us to find the duplicate mice by ID number, we had to use unique() function on the duplicate mouse data we just found by using duplicated().

/------------Chat GPT code---------------------------/

duplicate_mouse_ids = duplicate_mice['Mouse ID'].unique()

/----------------------------------------------------/

I had to look up Chat GPT to find out what function to drop a specific Mouse ID. It gave me the solution with function isin() which was very new to me. This eventually returned a correct answer.

/------------Chat GPT code---------------------------/

cleaned_mouse_data = mouse_study_complete[~mouse_study_complete['Mouse ID'].isin(duplicate_mouse_id)]

/----------------------------------------------------/

I had a problem while calculating the IQR by using a for loop. The TA and professor gave me the hints and showed me how to find the Quartiles first and IQR = upper bound - lowerer bound. As for the Outliers, I used Chat GPT to find the result.

/------------Chat GPT code---------------------------/

outliers = tumor_volumes[(tumor_volumes < lower_bound) | (tumor_volumes > upper_bound)]

/----------------------------------------------------/

When Generating a scatter plot of mouse weight vs. the average observed tumor volume for the entire Capomulin regimen. We firstly needed to find the Capomulin regimen data, then the average mouse weight as well as average tumor vol.

For Capomulin data, using loc with the condition ['Drug Regimen'] == 'Capomulin'. And for the two average values, we use groupby the Mouse ID and then use mean() funciton to calculate ['Tumor Volume (mm3)'] and ['Weight (g)']. In addtion, without adding (numeric_only=True) codes wouldn't run.

I had to look up how to find the linear regression model.

/------------Chat GPT code---------------------------/

(slope, intercept, rvalue, pvalue, stderr) = st.linregress(avg_mouse_weight, avg_tumor_vol)

regress = slope * avg_mouse_weight + intercept

/----------------------------------------------------/


