## Motivation

**For what purpose was the dataset created?**
The dataset was originally created to examine the effectiveness of direct telemarketing (phone call) campaigns by a Portuguese banking institution, specifically whether customers would subscribe to a term deposit.

**Who created the dataset and on behalf of which entity? Who funded the creation of the dataset?**
The dataset was provided by Sérgio Moro, P. Cortez, and P. Rita (as referenced in their paper “A data-driven approach to predict the success of bank telemarketing”), and was hosted in the UCI Machine Learning Repository. Research for this dataset was partly affiliated with the Portuguese banking institution involved, though specific funding details are not fully documented in the UCI repository reference.
 
## Composition
**What do the instances represent?**
Each instance (row) represents a single customer who was contacted in a direct marketing campaign (telephonic outreach). The dataset details customer demographics, financial status, and the outcome of the campaign.

**How many instances of each type are there?**
The bank-full.csv version contains 45,211 instances (rows) and 17 features (columns) plus the target (y). Other versions (bank-additional.csv, bank-additional-full.csv, etc.) have slightly different row/column counts.

**Is there any missing data?**
No, according to the UCI reference, there are no explicit missing values except for the category 'unknown' in certain fields (which can be treated as missing or a separate category).

**Does the dataset contain data that might be considered confidential?**
No direct personally identifiable information (like full names, addresses, or phone numbers) is included. However, it does contain potentially sensitive financial information (balance, loan status), so care should be taken with usage.

## Collection process
**How was the data acquired?**
Data was collected by phone calls during marketing campaigns between May 2008 and November 2010. Each record logs a single client’s attributes and final subscription outcome.

**If the data is a sample, what was the sampling strategy?**
    - bank-full.csv includes all examples in chronological order.
    - The smaller derivatives (e.g., bank.csv) are random samples of 10% from the full set.

**Over what time frame was the data collected?**
From May 2008 to November 2010 during consecutive direct marketing campaigns.

## Preprocessing/cleaning/labelling
**Was any preprocessing done?**
    - The original authors mention that categorical variables may include 'unknown' values. For this project, the code explicitly replaces 'unknown' entries with NaN and then drops those rows.
    - The dataset is otherwise structured with integer or categorical fields.
    - The “raw” data was presumably stored by the authors; the UCI version is the result of their final compilation and labeling (e.g., “yes/no” for the target).

**Was the “raw” data saved in addition to the preprocessed/cleaned/labeled data?**
It is unclear if the authors kept raw call records. The dataset on UCI is the final curated version.
 
## Uses
**What other tasks could the dataset be used for?**
    - Classification tasks: subscription prediction, customer segmentation.
    - Time-series analysis of campaign effectiveness (if one uses the date order).
    - Feature engineering for advanced marketing models (predicting loan or cross-sell uptake).

**Are there any concerns that might affect future uses (unfair treatment, legal, financial risks)?**
    - Since it contains sensitive financial data like balance and loan status, usage must respect privacy laws and data-protection regulations.
    - The dataset only represents Portuguese bank customers from 2008–2010, so applying the model to other contexts or time frames might lead to demographic biases or poor generalization.

**Are there tasks for which the dataset should not be used?**
    - Avoid using it to make decisions that require modern, up-to-date economic factors, or for extracting real personal information (since it’s partially anonymized).
    - It should not be used to draw broad conclusions about global banking customers without acknowledging the specific cultural and temporal context.

## Distribution
**How has the dataset already been distributed?**
It is publicly available in the UCI Machine Learning Repository under open data principles for research and educational purposes.

**Is it subject to any copyright or other IP license?**
The UCI repository generally states datasets are for research and educational uses. Users should review the UCI terms of use for specifics.

## Maintenance
**Who maintains the dataset?**
The UCI Machine Learning Repository currently hosts and maintains this dataset. Any official updates or corrections are typically managed by UCI or the dataset authors (Moro, Cortez, Rita). So far, there has been no known major revision of the bank marketing data.
