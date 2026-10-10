# Business Insights

## Project overview

This project explores demand forecasting and inventory performance for a fictional industrial manufacturer. The datasets are synthetic and are used for learning and demonstration only.

The analysis combines historical demand, inventory snapshots, and purchase-order information to identify areas that may need further investigation. The findings below describe the supplied dataset; they are not claims about a real company.

## 1. Demand data quality

- The original demand file contained 27,500 rows.
- There were 25 exact duplicate rows. Removing those duplicates leaves 27,475 rows.
- There were 27 missing values in `Demand_Units`. Missing demand should not automatically be treated as zero, because a missing value and zero demand mean different things.

**Business implication:** Validate duplicate and missing-demand records before using demand history for forecasting or planning.

## 2. Forecasting results

A single product-location series was used to demonstrate the forecasting workflow. The analysis compared a naive baseline, a four-week moving-average baseline, and a Linear Regression model using lagged demand and calendar features. Evaluation used a chronological train/test split and recursive multi-step forecasting.

**Business implication:** A more complex model should only be preferred when it improves performance against simple baselines on the same test period. Forecasts are decision-support estimates, not guaranteed demand values.

## 3. Inventory stockout and excess snapshots

- 3,140 of 27,475 inventory snapshots were marked as stockouts, approximately **11.43%**.
- 151 snapshots were marked as excess inventory, approximately **0.55%**.
- These are proportions of inventory snapshots in this synthetic dataset, not the percentage of customer orders lost or the percentage of time the whole business was out of stock.

**Business implication:** Stockout exposure appears more prominent than excess-inventory flags in this dataset. Investigate affected product-location combinations before deciding whether to adjust replenishment parameters.

## 4. Products with higher historical stockout rates

The products with the highest observed stockout rates included:

| Product | Stockout snapshots | Total snapshots | Stockout rate |
|---|---:|---:|---:|
| Conveyor Roller Assembly (PRD-1027) | 237 | 785 | 30.19% |
| Heavy-Duty Coupling (PRD-1005) | 238 | 942 | 25.27% |
| Industrial Bearing Carrier (PRD-1010) | 179 | 785 | 22.80% |
| Heavy Equipment Bush (PRD-1023) | 171 | 785 | 21.78% |
| Variable Speed Coupling (PRD-1035) | 165 | 785 | 21.02% |
| High-Pressure Piston Rod (PRD-1017) | 143 | 785 | 18.22% |
| Timing Pulley Hub (PRD-1014) | 111 | 628 | 17.68% |
| Pneumatic Manifold Plate (PRD-1026) | 110 | 628 | 17.52% |
| Stainless Process Flange (PRD-1007) | 165 | 942 | 17.52% |
| Actuator Linkage Kit (PRD-1019) | 102 | 628 | 16.24% |

**Business implication:** Conveyor Roller Assembly and Heavy-Duty Coupling are useful starting points for reviewing demand patterns, supplier lead times, safety-stock assumptions, and inventory-record accuracy. A high historical stockout rate alone does not prove that increasing stock is the right action.

## 5. Location-level stockout rates

| Location | Historical stockout rate |
|---|---:|
| Pune Components Plant | 14.83% |
| Bengaluru Distribution Centre | 11.31% |
| Chennai Distribution Centre | 11.21% |
| Nashik Assembly Plant | 10.89% |
| Ahmedabad Manufacturing Plant | 10.60% |
| Mumbai Regional Warehouse | 10.54% |
| Delhi Industrial Warehouse | 10.54% |

**Business implication:** Pune Components Plant had the highest stockout snapshot rate in this dataset. Review its product mix, replenishment settings, and supply constraints before proposing changes.

## 6. Product-location combination to investigate first

The highest-risk combination identified in the analysis was **Conveyor Roller Assembly (PRD-1027) at Pune Components Plant**:

- Stockout snapshots: **61**
- Total weekly snapshots: **157**
- Historical stockout rate: **38.85%**

Other product-location combinations also showed elevated rates. These results are historical signals from synthetic data and should be treated as a prioritization aid rather than a prediction of future stockouts.

## 7. Inventory balance checks

The simplified inventory equation used was:

`Expected closing inventory = Opening inventory + Receipts - Demand`

There were **3,140 inventory records (11.43%)** where the calculated expected balance did not match the recorded closing inventory. All these discrepancies were associated with a stockout flag. The largest absolute difference was 216 units.

This can occur in a simplified dataset when closing stock is capped at zero while demand exceeds available inventory. However, the data alone does not establish how uncovered demand was handled (for example, lost sales, backorders, or another process).

**Business implication:** Do not overwrite recorded closing inventory based on this simplified check. Confirm the inventory transaction rules and the treatment of unmet demand first.

## 8. Purchase-order lead times

- Average actual purchase-order lead time: **19.7 days**.
- 95th percentile of actual lead time: **29 days**.

The notebook also examines purchase orders for the priority product-location combination, supplier-level performance within that subset, promised versus actual receipt dates, and the difference between standard and observed lead time.

**Business implication:** Average lead time alone may not provide enough protection against variability. Review the lead-time distribution and supplier-specific results before setting replenishment buffers.

## 9. Recommended next actions

1. **Validate data quality:** Investigate missing demand and duplicate records before production use.
2. **Prioritize stockout review:** Start with Conveyor Roller Assembly at Pune Components Plant, then review other high-rate combinations.
3. **Check replenishment inputs:** Compare demand variability, standard lead time, actual lead time, and supplier reliability.
4. **Use simple model comparisons:** Retain a forecasting model only if it improves test-set performance over suitable baselines.
5. **Avoid unsupported savings claims:** This analysis does not calculate verified cost savings, service-level improvement, or revenue recovered.
6. **Validate with real business data:** Confirm these patterns with actual ERP transactions and planning policies before taking operational action.

## Limitations

- All supplied data is synthetic and represents a learning scenario.
- The forecast demonstration uses one product-location series; results may not generalize to other products or locations.
- Stockout flags are historical labels in the dataset and do not directly measure lost sales.
- The simplified inventory balance check does not model every possible inventory transaction or backorder process.