# Big_Data

# Resources
1. Data Source: Amazon customer review datasets (https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt), and I picked the music data. (https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Music_v1_00.tsv.gz)
2. Software: Amazon AWS, Google Colab Notebook, PySpark, SQL (pgAdmin4)

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

# 1. Deliverable 1:

## Amazon Revies_ETL: [Amazon Revies_ETL](https://github.com/SoonaBritney/Big_Data/blob/main/Amazon_Reviews_ETL.ipynb)

Your knowledge of the cloud ETL process, you’ll create an AWS RDS database with tables in pgAdmin, pick a dataset from the Amazon Review datasets (Links to an external site.), and extract the dataset into a DataFrame. You'll transform the DataFrame into four separate DataFrames that match the table schema in pgAdmin. Then, you'll upload the transformed data into the appropriate tables and run queries in pgAdmin to confirm that the data has been uploaded.

### How to Set Up Systems:
- Amazon AWS can be set up here: https://aws.amazon.com/console/  (RDS for Database Setup, S3 for Storage) 
- pgAdmin4: We connect the AWS database here to do our development: http://127.0.0.1:53838/browser/
- Google Drive to install Google Colaboraty: https://drive.google.com/drive/my-drive

#### Deliverable 1 Content: ETL Process

- The Amazon_Reviews_ETL.ipynb file does the following: 
    - An Amazon Review dataset is extracted as a DataFrame: 
        - I chose music data (https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Music_v1_00.tsv.gz)
        - It was uploaded into my Amzon RDS
         ![AMAZON RDS](https://github.com/SoonaBritney/Big_Data/blob/main/Capture_amazon_rds.JPG)
         
         ![AMAZON AWS](https://github.com/SoonaBritney/Big_Data/blob/main/Capture_amazon_S3.JPG)
        
        - Now, it was connected to pgAdmin SQL editor, the AWS Database is visible, and created tables per schema:
        
        ![pgAdmin](https://github.com/SoonaBritney/Big_Data/blob/main/Capture_pgAdmin.JPG)
        
        - Database tables schema is here: - [SQL DB Tables schema](https://github.com/SoonaBritney/Big_Data/blob/main/challenge_schema.sql) 
    
    - Using the Google Drive Colaboratory library, we open the Amazon_Reviews_ETL:
        - extracted dataset is transformed into four DataFrames with the correct columns: (customes_df, product_df, review_id_df, and vine_df.)
        - To macth with the tablkes schema in SQL, we modified the reviee date format as datetime (from sting), and created a customer _count colum using groupby, aggregation SQL function. 
    - All four DataFrames are loaded into their respective tables in pgAdmin from Amazon_Reviews_ETL.ipynb. it is checked out that all the eows were sucesfully uploaded in RDS. 
        ![RDS upload](https://github.com/SoonaBritney/Big_Data/blob/main/Capture_upload_to_RDS.JPG)
    - Great Success! All the 4 tables were populted as planned.    
    

### AMAZON REVIEW ETL CODE: https://github.com/SoonaBritney/Big_Data/blob/main/Amazon_Reviews_ETL.ipynb


# 2. Deliverable 2: Determine Bias of Vine Reviews

## Vine_Review_Analysis: [Vine_Review_Analysis](https://github.com/SoonaBritney/Big_Data/blob/main/Vine_Reviews_Analysis.ipynb)

Using our knowledge of PySpark, Pandas, or SQL, we determine if there is any bias towards reviews that were written as part of the Vine program. 
For this analysis, I will determine if having a paid Vine review makes a difference in the percentage of 5-star reviews.

    - In my analysis:
    - There is a DataFrame or table for the vine_table data using one of three methods: I connected to Amazon AWS RDS database via Goodle Corlaboratu pyspark package, and then I reviwed with pgAdmin SQL Suery as well to ensure the accuracy. 
    - The data is filtered to create a DataFrame or table where there are 20 or more total votes 
    - In vine_table: 
        - Before filtering, there were 4,750,852 records, 
    - (Step 1) filtered with a condition of (total_votes >= 20), which means reviewes who votes aften (more than or equal to 20 times)    
    - (Step 2) filtered to create a DataFrame or table where the percentage of helpful_votes is equal to or greater than 50% (vote_counte["helpful_votes"]/vote_count["total_votes"]>0.5). It means we are targeting the reviwes, who has tendency of postive review ratings   
        - After Step 1 and 2, we created the dataframe, "new_table", which consists only 105,069 record.
    - (Step 3) the data filtered to create a DataFrame or table where there is a Vine review (vine == "Y")
    - (Step 4) The data is filtered to create a DataFrame where there isn’t a Vine review (vine == "N")
    - (Step 5) The total number of reviews, the number of 5-star reviews, and the percentage 5-star reviews are calculated for all Vine and non-Vine reviews (15 pt)

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


# Deliverable 3: A Written Report on the Analysis

 The report should contain the following:
        - Overview of the analysis: Explain the purpose of this analysis.
        - Results: Using bulleted lists and images of DataFrames as support, address the following questions:
            + How many Vine reviews and non-Vine reviews were there?
            + How many Vine reviews were 5 stars? How many non-Vine reviews were 5 stars?
            + What percentage of Vine reviews were 5 stars? What percentage of non-Vine reviews were 5 stars?
            
        - Summary: In your summary, state if there is any positivity bias for reviews in the Vine program. Use the results of your analysis to support your statement. Then, provide one additional analysis that you could do with the dataset to support your statement.
        
        
