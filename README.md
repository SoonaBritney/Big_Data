# Big_Data

# Resources
1. Data Source: Amazon customer review datasets (https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt), and I picked the music data. (https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Music_v1_00.tsv.gz)
2. Software: AWS, Google Colab Notebook, PySpark, SQL

# ETL Process
- Extract the dataset from the S3 bucket and load into a DataFrame.
- Count the number of records (rows) in the dataset.
- Transform the dataset to fit the tables in the schema file.
- Load the DataFrames that correspond to tables into an RDS instance.

# Chellenge Overview
Since your work with Jennifer on the SellBy project was so successful, you’ve been tasked with another, larger project: analyzing Amazon reviews written by members of the paid Amazon Vine program. The Amazon Vine program is a service that allows manufacturers and publishers to receive reviews for their products. Companies like SellBy pay a small fee to Amazon and provide products to Amazon Vine members, who are then required to publish a review.

In this project, you’ll have access to approximately 50 datasets. Each one contains reviews of a specific product, from clothing apparel to wireless products. You’ll need to pick one of these datasets and use PySpark to perform the ETL process to extract the dataset, transform the data, connect to an AWS RDS instance, and load the transformed data into pgAdmin. Next, you’ll use PySpark, Pandas, or SQL to determine if there is any bias toward favorable reviews from Vine members in your dataset. Then, you’ll write a summary of the analysis for Jennifer to submit to the SellBy stakeholders.

# Challenge Objectives
This new assignment consists of two technical analysis deliverables and a written report. You will submit the following:

1. Deliverable 1: Perform ETL on Amazon Product Reviews
2. Deliverable 2: Determine Bias of Vine Reviews
3. Deliverable 3: A Written Report on the Analysis (README.md)

# Challenge Summary

1. Deliverable 1:

## Amazon Revies_ETL: [Amazon Revies_ETL](https://github.com/SoonaBritney/Big_Data/blob/main/Amazon_Reviews_ETL.ipynb)

your knowledge of the cloud ETL process, you’ll create an AWS RDS database with tables in pgAdmin, pick a dataset from the Amazon Review datasets (Links to an external site.), and extract the dataset into a DataFrame. You'll transform the DataFrame into four separate DataFrames that match the table schema in pgAdmin. Then, you'll upload the transformed data into the appropriate tables and run queries in pgAdmin to confirm that the data has been uploaded.

    - The Amazon_Reviews_ETL.ipynb file does the following:
    - An Amazon Review dataset is extracted as a DataFrame (10 pt)
    - The extracted dataset is transformed into four DataFrames with the correct columns (20 pt)
    - All four DataFrames are loaded into their respective tables in pgAdmin (10 pt)

2. Deliverable 2: Determine Bias of Vine Reviews

## Vine_Review_Analysis: [Vine_Review_Analysis](https://github.com/SoonaBritney/Big_Data/blob/main/Vine_Reviews_Analysis.ipynb)

Using your knowledge of PySpark, Pandas, or SQL, you’ll determine if there is any bias towards reviews that were written as part of the Vine program. For this analysis, you'll determine if having a paid Vine review makes a difference in the percentage of 5-star reviews.

    - The analysis does the following:
    - There is a DataFrame or table for the vine_table data using one of three methods - I chose Amazon AWS
    - The data is filtered to create a DataFrame or table where there are 20 or more total votes (5 pt) 
    - The data is filtered to create a DataFrame or table where the percentage of helpful_votes is equal to or greater than 50% (5 pt)
    - The data is filtered to create a DataFrame or table where there is a Vine review (5 pt)
    - The data is filtered to create a DataFrame or table where there isn’t a Vine review (5 pt)
    - The total number of reviews, the number of 5-star reviews, and the percentage 5-star reviews are calculated for all Vine and non-Vine reviews (15 pt)

**Summary: Determining if the Vine reviews are biased**

Here is the final summary:

    1) Total rows of Vine_df: 4750852
    2) Total Reviews (vote count> 50% and total_votes > 20):105969
    3) Total five star_counts: 67568
    4) analyzed the five star % when vine == Y (Paid):0.6676168119830092
    5) analyzed the five star % when vine == N (not paid): 0.631526959365101

In this summary, when vine is Yes (means paid), the five star rate is slightly higher (0.6676168119830092), and seems biased.
(0.6676168119830092 - 0.631526959365101 = 0.0360 )

Although, it is possible that there could have other factors, or it is a simply coinsident, and my conclusion is it maybe be biased, but not a gerat deal and certain. Thank you! It is a greatly fun project.

## Vine Review Analtsis: ![Vine Review Analtsis](https://github.com/SoonaBritney/Big_Data/blob/main/vine_analysis.JPG)

3. Deliverable 3: A Written Report on the Analysis
For this part of the Challenge, you’ll write a report that summarizes the analysis you performed in Deliverable 2.

- The report should contain the following:
        - Overview of the analysis: Explain the purpose of this analysis.
        - Results: Using bulleted lists and images of DataFrames as support, address the following questions:
            + How many Vine reviews and non-Vine reviews were there?
            + How many Vine reviews were 5 stars? How many non-Vine reviews were 5 stars?
            + What percentage of Vine reviews were 5 stars? What percentage of non-Vine reviews were 5 stars?
            
        - Summary: In your summary, state if there is any positivity bias for reviews in the Vine program. Use the results of your analysis to support your statement. Then, provide one additional analysis that you could do with the dataset to support your statement.
        
        
