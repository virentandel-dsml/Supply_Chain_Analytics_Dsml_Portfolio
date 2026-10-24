# Supplier Risk & Supplier Analytics — Business Insights

## Project overview

- **Purpose:** Review supplier delivery, lead time, and quality.
- **Dataset:** Synthetic data for portfolio use.
- **Suppliers:** 30
- **Materials:** 40
- **Purchase order lines:** 2,200

## 1. Delivery performance

| Delivery status | PO lines | Share |
|---|---:|---:|
| On time | 1,045 | 47.5% |
| Late | 1,073 | 48.8% |
| Not yet received | 82 | 3.7% |

**Key points**
- 49.34% of completed lines arrived on time.
- The average supplier-level on-time rate was 48.07%.
- Late lines slightly outnumbered on-time lines.

**Suggested action**
- Review repeated delivery delays.
- Check whether promised dates are realistic.

## 2. Lead time

**Key points**
- Eight suppliers were selected for priority review.
- Their average lead time was 2.71 days above standard.
- The gap ranged from 1.70 to 3.87 days.

**Suggested action**
- Discuss lead-time gaps with these suppliers.
- Check order timing, supplier capacity, transport, and receiving.
- Confirm the cause before deciding on corrective action.

## 3. Quality

**Key points**
- Quantity inspected: 651,475 units.
- Quantity rejected: 13,768 units.
- Overall rejection rate: 2.11%.
- Longmeadow Sensor Assemblies had a 2.60% rejection rate.
- Its expected rejection rate was 2.40%.
- This was the largest gap above expectation among the suppliers highlighted in the quality analysis.

**Suggested action**
- Review the affected materials and receipts.
- Discuss recurring defects with the relevant suppliers.
- Agree on corrective actions after checking the details.

## 4. Supplier risk

| Risk category | Suppliers |
|---|---:|
| High | 9 |
| Medium | 7 |
| Low | 2 |
| Not assessed | 12 |

The score checks three warning signs:
- On-time delivery below target.
- Actual lead time above standard.
- Rejection rate above expectation.

**Key points**
- Eight high-risk suppliers with at least 30 completed delivery lines were selected for priority review.
- Twelve suppliers had no purchase orders.
- Nine suppliers were flagged for small-sample validation.

**Suggested action**
- Start with the priority-review suppliers.
- Collect more data for suppliers with small samples.
- Do not treat the score as a final supplier judgement.

## 5. Data checks

- 30 suppliers and 40 materials.
- 2,200 purchase order lines.
- 2,497 goods receipts.
- 2,497 quality inspections.
- No missing values were found in the columns checked.
- No duplicate IDs were found in the key ID fields checked.
- The checked links between the files were valid.

## 6. Limitations

- The data is synthetic.
- The risk score uses simple rules.
- The score does not predict future performance.
- The analysis does not explain the cause of a supplier issue.
- Supplier rates based on few deliveries may be less reliable.
- Real procurement data and supplier context should be checked before decisions are made.

## Conclusion

**Main areas to review**
- Late deliveries.
- Lead times above standard.
- Rejection rates above expectation.
- Suppliers with limited or no activity.

Use the risk score to set review priorities. Confirm the details before taking action.
