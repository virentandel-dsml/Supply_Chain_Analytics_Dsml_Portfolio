# Business Insights

## Project overview

This project explores manufacturing performance and production delays
for a fictional manufacturer. The dataset contains **2,000 synthetic
production orders** and is used for learning and portfolio demonstration
only.

The analysis looks at delay patterns across plants, product families,
order priorities, material delays, and capacity-load groups. It also
compares classification models for identifying orders at risk of delay.
The findings describe this dataset; they are not claims about a real
company.

## 1. Data quality

- **Production orders:** 2,000
- **Columns:** 26
- **Duplicate production order IDs:** 0
- **Missing values:** None in the columns checked
- **Delayed orders:** 452 (22.6%)
- **Orders not delayed:** 1,548 (77.4%)

**Business implication:** The dataset was complete for the checks
performed. In a real manufacturing environment, data definitions and how
the delay flag is assigned should also be confirmed before using the
results.

## 2. Delay rates by plant

| Plant                            | Total orders | Delayed orders | Delay rate |
|----------------------------------|-------------:|---------------:|-----------:|
| Ahmedabad Components Works       |          583 |            137 |     23.50% |
| Nashik Assembly Facility         |          480 |            112 |     23.33% |
| Pune Precision Engineering Plant |          561 |            124 |     22.10% |
| Vadodara Industrial Works        |          376 |             79 |     21.01% |

Ahmedabad Components Works had the highest observed delay rate at
**23.50%**. Vadodara Industrial Works had the lowest rate at **21.01%**.

**Business implication:** Review the planning and execution processes at
plants with higher delay rates. Check differences in product mix, work
centers, and order conditions before deciding on corrective action.

## 3. Delay rates by product family

| Product family        | Total orders | Delayed orders | Delay rate |
|-----------------------|-------------:|---------------:|-----------:|
| Pneumatic             |          136 |             37 |     27.21% |
| Valve                 |          141 |             38 |     26.95% |
| Rotating Equipment    |           68 |             16 |     23.53% |
| Automation            |           68 |             16 |     23.53% |
| Metal Components      |           56 |             13 |     23.21% |
| Fluid Handling        |          208 |             48 |     23.08% |
| Structural Components |          191 |             44 |     23.04% |
| Hydraulic             |          259 |             57 |     22.01% |
| Power Transmission    |          457 |             98 |     21.44% |
| Linear Motion         |          141 |             30 |     21.28% |
| Gearbox               |          143 |             30 |     20.98% |
| Heavy Equipment       |           71 |             14 |     19.72% |
| Material Handling     |           61 |             11 |     18.03% |

Pneumatic and Valve orders had the highest observed delay rates among
the listed product families. Material Handling had the lowest rate,
based on 61 orders.

**Business implication:** Pneumatic and Valve orders may be useful
starting points for further review. Order volumes differ by family, so
consider the rate alongside volume and operating context.

## 4. Delay rates by order priority

| Order priority | Total orders | Delayed orders | Delay rate |
|----------------|-------------:|---------------:|-----------:|
| Routine        |          307 |             92 |     29.97% |
| Standard       |          929 |            212 |     22.82% |
| High           |          583 |            115 |     19.73% |
| Critical       |          181 |             33 |     18.23% |

Routine orders had the highest observed delay rate at **29.97%**, while
Critical orders had the lowest at **18.23%**.

**Business implication:** This does not mean lower-priority orders
should automatically receive higher priority. Review how priorities are
assigned and whether routine orders have different planning or
scheduling conditions.

## 5. Material delay

| Material delay (days) | Total orders | Delayed orders | Delay rate |
|----------------------:|-------------:|---------------:|-----------:|
|                     0 |        1,204 |            213 |     17.69% |
|                     1 |          294 |             58 |     19.73% |
|                     2 |          213 |             60 |     28.17% |
|                     3 |          110 |             36 |     32.73% |
|                     5 |          123 |             56 |     45.53% |
|                     7 |           56 |             29 |     51.79% |

The observed delay rate generally increased as material-delay days
increased. Orders with seven days of material delay had a **51.79%**
delay rate, compared with **17.69%** for orders with no material delay.

**Business implication:** Material availability is worth reviewing
before production starts. This pattern shows an association in the
synthetic dataset; it does not prove that material delay alone caused
production delay.

## 6. Capacity load

| Capacity-load group | Total orders | Delayed orders | Delay rate |
|---------------------|-------------:|---------------:|-----------:|
| Below 60%           |          186 |             28 |     15.05% |
| 60–75%              |          641 |            100 |     15.60% |
| 75–90%              |          821 |            216 |     26.31% |
| Above 90%           |          352 |            108 |     30.68% |

Orders with capacity load above 90% had the highest delay rate at
**30.68%**. The rate was also higher for the 75–90% group than for the
two lower-load groups.

**Business implication:** Review highly loaded work centers and check
whether production workloads can be balanced. Assess capacity load with
the production schedule and work-center constraints before changing
plans.

## 7. Classification model results

The notebook used a stratified 80/20 split, with **1,600 training
records** and **400 test records**. The test set contained 90 delayed
orders and 310 non-delayed orders.

| Model               | Accuracy | Precision | Recall | F1-score |
|---------------------|---------:|----------:|-------:|---------:|
| Baseline            |    77.5% |     0.000 |  0.000 |    0.000 |
| Logistic Regression |    77.7% |     0.524 |  0.122 |    0.198 |
| Random Forest       |    77.7% |     1.000 |  0.011 |    0.022 |

At the default classification threshold, Logistic Regression had the
highest recall and F1-score of the three models, although its recall was
only **12.2%**. Random Forest identified very few delayed orders at its
default threshold. The baseline achieved 77.5% accuracy by predicting
the majority class, but did not identify delayed orders.

**Business implication:** Accuracy alone is not enough for this problem.
Recall matters when the goal is to identify more delayed orders.
Precision also matters because false alarms take planners' time to
investigate.

## 8. Prediction threshold analysis

The notebook tested different prediction thresholds for Logistic
Regression.

| Threshold | Predicted delays | Precision | Recall | F1-score |
|----------:|-----------------:|----------:|-------:|---------:|
|      0.50 |               21 |     0.524 |  0.122 |    0.198 |
|      0.40 |               52 |     0.462 |  0.267 |    0.338 |
|      0.30 |              104 |     0.365 |  0.422 |    0.392 |
|      0.20 |              210 |     0.305 |  0.711 |    0.427 |
|      0.10 |              354 |     0.237 |  0.933 |    0.378 |

At a threshold of **0.20**, the model flagged 210 orders as potentially
delayed. It identified 64 of the 90 delayed orders in the test set,
missed 26 delayed orders, and incorrectly flagged 146 non-delayed
orders. Precision was **30.5%** and recall was **71.1%**.

Lowering the threshold to 0.10 raised recall to **93.3%**, but precision
fell to **23.7%**, and 354 orders were flagged.

**Business implication:** A lower threshold may help planners find more
orders at risk, but it can also create many false alarms. The
appropriate threshold depends on the cost of a missed delay and the
workload created by investigating flagged orders. These results are
exploratory and require independent validation.

## 9. Logistic Regression coefficients

The notebook reviewed the largest Logistic Regression coefficients by
absolute value. Among the largest displayed terms were Routine order
priority, material-delay days, capacity load, and planned production
days.

These coefficients describe how the model uses the encoded input fields.
They do not prove that a field causes a delay, and categorical
coefficients are interpreted relative to the model's reference
categories.

**Business implication:** Use the coefficients to help understand the
model, not as a standalone ranking of business causes. Validate
operational explanations with manufacturing and planning teams.

## 10. Recommended next actions

1.  **Review material availability.** Check material-delay cases before
    production starts.
2.  **Review high capacity loads.** Investigate work centers and orders
    in the higher capacity-load groups.
3.  **Compare plant and product-family patterns.** Check operating
    context and order volume before deciding where to intervene.
4.  **Choose model metrics based on the business need.** Consider both
    missed delays and false alarms, not just accuracy.
5.  **Validate the model further.** Test the model and threshold on
    separate data before using its flags to support production planning.
6.  **Avoid unsupported savings claims.** This analysis does not
    calculate verified cost savings, productivity gains, or delay
    reductions.

## Limitations

- The dataset is synthetic and represents a learning scenario.
- The results describe the supplied data and do not establish cause and
  effect.
- The model has not been validated for operational use.

## Conclusion

The analysis found higher observed delay rates among orders with longer
material delays and higher capacity loads. Pneumatic and Valve product
families and Ahmedabad Components Works also had higher delay rates in
this dataset.

Logistic Regression provided a way to explore delay-risk flags, but the
results depend on the selected threshold. The model should be treated as
an exploratory decision-support exercise, not an automated
production-planning rule.
