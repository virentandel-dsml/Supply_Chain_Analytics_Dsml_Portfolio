# Supply Chain Risk & Supplier Analytics

## What this project does

This project uses synthetic supplier data to review delivery, lead time,
and product quality. I used Python to compare supplier performance,
check results against supplier targets, and group suppliers by risk level
to help identify which suppliers may need closer review.

The company and data are fictional. The data is for learning and
portfolio use only.

## Tools used

- Python
- pandas
- Matplotlib
- Google Colab

## How to run

1. Upload the notebook and all five CSV files to Google Colab:
   `Supplier_Master.csv`, `Material_Master.csv`, `Purchase_Orders.csv`,
   `Goods_Receipts.csv`, and `Quality_Inspections.csv`.
2. Keep the CSV files in the main Colab file area (`/content`), as
   expected by the notebook.
3. Open the notebook and choose **Runtime → Run all**.

The notebook reads the CSV files from `/content`. If you store the files
in another folder, update the file paths in the first code cell.

## What I looked at

- Missing values, duplicate IDs, and links between the files
- On-time, late, and not-yet-received purchase order lines
- Supplier on-time delivery percentages
- Actual lead times compared with supplier standards
- Rejection rates compared with expected defect rates
- A simple supplier risk score and risk categories
- Suppliers selected for priority review
- Charts comparing delivery, lead time, and quality results

## Notes and limitations

This is a learning project using synthetic data, not a live supplier-risk
system. The results depend on the assumptions used to generate the data.
The risk score is a simple rule-based method that flags delivery, lead-time,
and quality concerns; it does not predict future supplier performance.

Some suppliers have no purchase orders or limited delivery history, so
their results cannot be assessed with the same confidence as suppliers
with more data. The findings should be reviewed alongside business
context and real supplier information before making procurement decisions.
