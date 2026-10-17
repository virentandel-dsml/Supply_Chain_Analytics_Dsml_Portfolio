# Manufacturing Performance & Predictive Analytics

## What this project does

This project uses synthetic production-order data to explore
manufacturing delays. I used Python to review the data, compare delay
rates across different manufacturing groups, and test whether machine
learning could help identify orders at risk of delay.

The company and data are fictional. The data is for learning and
portfolio use only.

## Tools used

-   Python
-   pandas
-   Matplotlib
-   scikit-learn
-   Google Colab

## How to run

1.  Upload the notebook and `Manufacturing_Production_Orders.csv` to
    Google Colab.
2.  Keep the CSV file in the main Colab file area (`/content`), as
    expected by the notebook.
3.  Open the notebook and choose **Runtime → Run all**.

The notebook reads `Manufacturing_Production_Orders.csv` from
`/content`. If you store the file in another folder, update the
`data_folder` line in the first code cell.

## What I looked at

-   Duplicate order IDs and missing values
-   Overall production delay rate
-   Delay rates by plant, product family, and order priority
-   Delay rates by material-delay days and capacity-load group
-   A baseline model, Logistic Regression, and Random Forest
-   Precision, recall, F1-score, and accuracy
-   Different Logistic Regression prediction thresholds
-   A confusion matrix and Logistic Regression coefficients

## Notes and limitations

This is a learning project using synthetic data, not a production
delay-prediction system. The results depend on the assumptions used to
generate the data. The test set contains fewer delayed orders than
non-delayed orders, so accuracy alone does not show how well a model
identifies delays.

Lowering the prediction threshold can identify more delayed orders, but
it also creates more false alarms. The model and threshold would need
further validation with real manufacturing data before being used for
production planning.
