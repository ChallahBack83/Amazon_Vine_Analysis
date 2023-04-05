# Amazon_Vine_Analysis

## Overview

The purpose of this project is to check for bias in reviews for Amazon's Vine program and determine if the program is successful. Vine is a service where products are provided to customers for free in exchange for a published review.  To examine the quality of the program, we were given access to 50 datasets of Amazon reviews based on product categories. Choosing one dataset, we were tasked with using AWS RDS, Google Colab, PySpark, Postgres, SQL, and Pandas to analyze the reviews. I chose the <b>"Pet Products"</b> dataset and performed the following tasks to begin my analysis:
  - In Google Colab using PySpark, I extracted and transformed the data into specific tables, connected to my AWS RDS, and loaded the new datasets into SQL tables using Postgres through PgAdmin.
- These new tables were extracted from Postgres into csvs, and I read the vine_table.csv into Jupyter Notebook to analyze using Pandas.

## Results

Once in Jupyter Notebook, we still needed to make the dataset more manageable for the analysis.  Not all reviews are rated equal, which is why Amazon has a "helpful_votes" system where users can review or mark customer reviews.  I filtered the dataset and created a new dataframe that contained only those reviews that had at least 20 or more total votes.  This took the number of rows in our dataset down to <b>39,376</b> rows from <b>2,643,619</b>, making our analysis much more focused. We further trimmed this down by filtering out the less effective reviews by calculating how helpful the reviews were. If a review's helpful_votes were less than 50% of its total_votes, it was removed, and our final working dataframe was now at <b>38,010</b> rows.

![high_votes](link)

Next, in order to search for bias, we really only needed to care about reviews which awarded products five star ratings.

Bulleted list  & images of DataFrames as support

- How many Vine reviews and non-Vine reviews were there?

- How many Vine reviews were 5 starts? How many non-Vine reviews were 5 stars?

- What percentage of Vine reviews were 5 starts? What percentage of non-Vine reviews were 5 stars?

## Summary

Is there any positivity bias for reviews in Vine program. Use results to support statement.

Provide additional analysis you could do using dataset to support your statement.
