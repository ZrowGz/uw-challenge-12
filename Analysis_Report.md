# High Risk Loan Identification Analysis
*Modeling Default Risk for Loans on a Peer to Peer Lending Platform*

---

## Overview of the Analysis

This is an analysis of a basket of 77,535 various loans from a peer to peer lending company, which I will analyze the risk of default of using Supervised Machine Learning and Logistic Regression (`LogisticRegression()`) modeling to predict the likelihood of loan's default risk.

This is a critical value to get correct since defaulted loans can quickly wipe out profits and even cause substantial losses. It is more important to correctly identify High-Risk Loans as such than to incorrectly categorize Healthy Loans incorrectly due to the elevated risk of financial loss in the first case.

The various components of the loans that was analyzed were:
- Loan Size
- Interest Rate
- Borrower's Income
- Borrower's Debt to Income Ratio
- Borrower's Number of Accounts
- Number of Borrower's Derogatory Marks
- Borrower's Total Debt
- Risk Classification Category 
  - Healthy Loans assigned `0`
  - High Default Risk Loans assigned `1`

Due to the fact that the vast majority of loans are not at risk for defaulting, I was aware of the fact that the data was going to be massively imbalanced. To attempt to address this imbalanced data set and improve the ability to correctly identify high risk loans, a second attempt was made using Oversampling (`RandomOverSampler()`). 

---

## Results

Using bulleted lists, describe the balanced accuracy scores and the precision and recall scores of all machine learning models.

* Machine Learning Model 1:
  * Model 1 used `LogisticRegression()` to model the data.
    * Due to the data being highly imbalanced, a sub-optimal result was expected.
  * Results for Model 1 by category:
    * Accuracy 95.2%
    * Precision:
      * Healthy Loans (`0`): 100%
      * High-Risk Loans (`1`): 85%
    * Recall:
      * Healthy Loans (`0`): 99%
      * High-Risk Loans (`1`): 91%


* Machine Learning Model 2:
  * Model 2 again used `LogisticRegression()` to model the data.
    * To compensate for the imbalanced dataset, Over Sampling was performed using `RandomOverSampler()`
  * Results for Model 2 by category:
    * Accuracy 99.4%
    * Precision:
      * Healthy Loans (`0`): 100%
      * High-Risk Loans (`1`): 84%
    * Recall:
      * Healthy Loans (`0`): 99%
      * High-Risk Loans (`1`): 99%
  
---

## Summary 

The goal of this analysis is to be able to correctly identify any loan that increases the risk of the portfolio through loan defaults. I believe it is more beneficial to label a loan as "High Risk" when it may not actually be, rather than to incorrectly label a "High Risk" Loan as "Healthy" because of the potential for loss of capital. Additionally, due to the fact that there is an essentially limitless pool of loans to fund, ruling some out that could have actually been healthy poses no risk to the ongoing operation of the investment business, whereas the inverse is not true: funding defaulting loans does impair buisiness operations.

### Review of Model 1 
- This model had better precision for `1` than Model 2, which shows that it categorized fewer "Healthy Loans" as "High Risk"
- The Recall was significantly lower at 85% for this model, which means that it failed to identify 15% of the High-Risk Loans
- With the High Risk Loans making up 3% of the analyzed data, 9% of the High Risk category would leave 0.27% of the portfolio exposed to loss. 
  - (100 x 0.03) = 3; 
  - (3 * .09) = 0.27; 
  - (0.27 / 100) = 0.27%
- This is not a terrible amount of loans to default, but it is certainly better to avoid this if at all possible.

### Review of Model 2 
- This model incorrectly identified more "Healthy" Loans as "High Risk" than model 1, by 1% (84% correctly for model 2 versus 85% correctly for model 1).
  - This difference is negligible since the pool of loans to choose from are essentially limitless.
- The Recall for model 2 was significantly better, 99% vs. model 1's 91%. 
  - This indicates that that it only incorrectly labeled a High Risk loan as a Healthy loan 1 in 100 times of encountering a high risk loan. 
  - With high risk loans only making up 3% of the basket of analyzed loans, this means I would be left holding the bag on only 0.03% of the loans I fund.


### Conclusion
In conclusion, **I recommend Model 2**, using Over Sampling of the data set as the more optimized method for screening potential loans on this peer to peer lending platform.

However, if you were attempting to gift money to borrowers or operating a charity, it would likely be more important to screen out the Healhty Loans by only wishing to fund the High Risk ones. In this case, you would be more tolerant of a lower precision and perhaps would end up going with model 1. But if that was the goal, you would probably not fund people using a peer to peer lending platform since gifting people money this way will also ruin their credit scores and probably worsen their quality of life in the long term.