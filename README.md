# Amazon_Vine_Analysis

## Overview

The purpose of this project is to check for bias in reviews for Amazon's Vine program and determine if the program is successful. Vine is a service where products are provided to customers for free in exchange for a published review.  To examine the quality of the program, we were given access to 50 datasets of Amazon reviews based on product categories. Choosing one dataset, we were tasked with using AWS RDS, Google Colab, PySpark, Postgres, SQL, and Pandas to analyze the reviews. I chose the <b>"Pet Products"</b> dataset and performed the following tasks to begin my analysis:
  - In Google Colab using PySpark, I extracted and transformed the data into specific tables, connected to my AWS RDS, and loaded the new datasets into SQL tables using Postgres through PgAdmin.
- These new tables were extracted from Postgres into csvs, and I read the vine_table.csv into Jupyter Notebook to analyze using Pandas.

## Results

Once in Jupyter Notebook, we still needed to make the dataset more manageable for the analysis.  Not all reviews are rated equal, which is why Amazon has a "helpful_votes" system where users can review or mark customer reviews.  I filtered the dataset and created a new dataframe that contained only those reviews that had at least 20 or more total votes.  This took the number of rows in our dataset down to <b>39,376</b> rows from <b>2,643,619</b>, making our analysis much more focused. We further trimmed this down by filtering out the less effective reviews by calculating how helpful the reviews were. If a review's helpful_votes were less than 50% of its total_votes, it was removed, and our final working dataframe was now at <b>38,010</b> rows.

![high_votes](link)

Since we are analyzing a program that essentially "pays" for reviews, we are most interested in the reviews which give products five star ratings since these are the most likely to show bias. Therefore, we used .loc and groupby to count the number of reviews, both "Paid" and "Unpaid", with 5.0 star_rating.
```
five_star =high_votes.loc[high_votes['star_rating'] == 5.0].groupby('vine').count()
five_star["review_id"]
```

![five_star_count](link)

Through our analysis we discovered
- Out of 38,010 helpful reviews, only 170 of them were Vine reviews, or 0.45% while 99.55% (37,840) were non-Vine program reviews.

![total_reviews_count](link)

- Out of these reviews, only 65 of the Vine reviews gave the products five stars. In comparison, 20,612 of the non-Vine reviews gave the products five stars.

![five_star_count](link)

- The size of each category (Paid vs Unpaid) is vastly different, so we need to examine the percentage per category. The Vine reviews have only 38.54% five star reviews while 54.47% of the non-Vine reviews have five stars.

![percent_five_star](link)

## Summary

In conclusion, from analysis of this dataset there does not seem to be any positivity bias for the reviews in the Vine program since only 38.54% of the reviews are five star reviews compared to 54.47% of the non-Vine reviews. The participants in the Vine program seem more critical in their assessments of these products, but the sample is much smaller than the rest of the dataset. To provide a more thorough analysis, I suggest including four star reviews in the analysis since these also could contribute to positivity bias. Or, since the Vine reviews are such a small portion of the total reviews, we could loosen our initial filters. For instance, if we change the total_votes filter from >=20 to >=10, the dataset expands to 91,314 rows which allows us to filter further but adds more Vine reviews to the pool we are examining.
