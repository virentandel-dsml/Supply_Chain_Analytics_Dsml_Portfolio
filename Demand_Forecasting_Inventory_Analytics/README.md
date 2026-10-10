# Demand Forecasting & Inventory Decision Analytics

## What this project does

This project uses sample manufacturing data to explore demand forecasting and inventory problems. I used Python to clean and review the data, compare a few forecasting methods, and look for products and locations with inventory risk.

The company and data are fictional. The data is for learning and portfolio use only.

## Tools used

- Python
- pandas
- NumPy
- Matplotlib
- scikit-learn
- Google Colab

## How to run

1. Upload the notebook and all seven CSV files to Google Colab.
2. Keep the CSV files in the main Colab file area (`/content`), as expected by the notebook.
3. Open the notebook and choose **Runtime → Run all**.

You can also download this repository and adjust the `data_folder` line in the first code cell to match the folder where you put the CSV files.

## What I looked at

- Basic data-quality checks
- Weekly demand patterns
- Naive and moving-average forecasting baselines
- A linear regression forecasting model
- Forecast error comparison
- Inventory stockout and excess-stock flags
- Stockout patterns by product and location
- Purchase order lead times and supplier-related measures

## Notes and limitations

This is a learning project using synthetic data, not a production forecasting system. The results depend on the assumptions used to generate the data. Forecast accuracy alone is not enough to decide inventory levels; lead time, product importance, cost, and service targets would also need to be considered.
