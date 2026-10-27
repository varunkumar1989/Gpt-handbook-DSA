# AI-First Data Engineer - Complete Reference

## The learning model

For each topic, be able to answer five things:

1. **Definition** - what it is.
2. **Use** - when it helps in a real business workflow.
3. **Example** - a small formula, query, measure or code snippet.
4. **Explanation** - how to say it without jargon.
5. **Validation** - what can go wrong and how you would check it.

## Excel

| Concept | Definition and use | Example |
|---|---|---|
| Data grain | The real-world unit represented by one row. It prevents invalid totals and joins. | An order-line table has one product line per order. |
| Table | A structured range that expands formulas and filters safely. | `=SUM(Orders[Sales])` |
| References | Relative references move when copied; absolute references remain fixed. | `=C2*$F$1` |
| Aggregation | A formula that summarizes values. | `=SUM(C2:C100)`, `=AVERAGE(C2:C100)` |
| Cleaning | Transform inconsistent values before matching or grouping. | `=TRIM(PROPER(A2))` |
| Date key | A stable reporting period from a date. | `=TEXT(B2,"yyyy-mm")` |
| Logic | Applies a rule and returns a result. | `=IF(AND(C2>0.3,D2=""),"Review","OK")` |
| Lookup | Fetches a related value using a shared key. | `=XLOOKUP(A2,Products[SKU],Products[Category],"Missing")` |
| Pivot Table | Interactive aggregation by fields, filters and measures. | Revenue by month and category. |
| Power Query | Recorded, refreshable data preparation steps. | Source -> change type -> unpivot -> load. |

**Explain it simply:** Excel is suitable for quick exploration and operating reports when the data is well structured. The crucial discipline is to keep one consistent row grain, preserve raw data and make calculations repeatable.

## SQL

| Concept | Definition and use | Example |
|---|---|---|
| ERD | Map of entities and their relationships. | Customers 1-to-many Orders. |
| Primary key | A value that uniquely identifies a row. | `customer_id` |
| Foreign key | A value linking a record to a related table. | `orders.customer_id` |
| Filter | Limits the rows answering a question. | `WHERE status='Paid'` |
| Aggregation | Calculates metrics at a stated grain. | `SUM(sales) GROUP BY month` |
| HAVING | Filters aggregated groups. | `HAVING SUM(sales)>100000` |
| Join | Combines tables using related keys. | `LEFT JOIN customers USING(customer_id)` |
| CTE | Named temporary query step. | `WITH clean_orders AS (...)` |
| Window function | Calculates across related rows while retaining detail. | `RANK() OVER(PARTITION BY month ORDER BY sales DESC)` |
| Quality test | Makes completeness, uniqueness and referential expectations checkable. | `GROUP BY order_id HAVING COUNT(*)>1` |

**Interview answer:** “Before I join tables, I state the row grain and test key uniqueness. After joining, I reconcile row count and revenue. That is how I avoid fan-out inflating a KPI.”

## Power BI

| Concept | Definition and use | Example |
|---|---|---|
| Star schema | Fact table with connected dimensions. | Orders fact + Date, Customer, Product dimensions. |
| Semantic model | Shared relationships, measures and business labels behind reports. | One Revenue measure used across reports. |
| Power Query | Transformation layer prior to modelling. | Append files, set types, unpivot data. |
| Measure | Calculation evaluated in visual filter context. | `Revenue = SUM(Orders[Sales])` |
| CALCULATE | Changes filter context for a measure. | `CALCULATE([Revenue], ALL(Product))` |
| Date table | Continuous calendar supporting time intelligence. | `Revenue LY = CALCULATE([Revenue], SAMEPERIODLASTYEAR(Date[Date]))` |
| Drill-through | Navigation from a summary result to relevant detail. | Click a customer segment to view its orders. |

**Explain it simply:** A Power BI report is only as trustworthy as the semantic model and metric definition underneath it. Build the model first, then visuals.

## Python and analytics

| Concept | Definition and use | Example |
|---|---|---|
| Function | Reusable named logic with a clear input/output contract. | `def valid_sales(x): ...` |
| Exception | Explicit handling of a known failure state. | `raise ValueError("sales cannot be negative")` |
| NumPy vectorization | Performing an operation across an array without manual loops. | `z=(x-x.mean())/x.std()` |
| DataFrame | Labelled table for analysis. | `df.info()` |
| Cleaning | Fix types, duplicates and missingness before analysis. | `df=df.drop_duplicates()` |
| Groupby | Aggregation at a chosen grain. | `df.groupby("month")["sales"].sum()` |
| Merge | Join of two DataFrames. | `orders.merge(products,on="product_id",how="left")` |
| Hypothesis test | Formal check of evidence against a stated null hypothesis. | Compare campaign A/B means after checking assumptions. |

**Explain it simply:** A reproducible Python analysis is one another analyst can restart, rerun and inspect without hidden steps or private paths.

## Machine learning

| Concept | Definition and use | Example |
|---|---|---|
| Problem framing | Connects a decision, target, features, metric and baseline. | Churn in 30 days -> retention offer. |
| Train/test split | Keeps a final unseen sample for honest performance estimation. | `train_test_split(X,y,test_size=.2)` |
| Leakage | Using future or outcome information that will not exist when predicting. | A post-default field in a default model. |
| Linear regression | Numeric prediction based on weighted input relationships. | `y_hat=b0+b1*x1+b2*x2` |
| Logistic regression | Class-probability model used with a decision threshold. | `p=1/(1+exp(-z))` |
| Precision | Of predicted positives, share that are true. | `TP/(TP+FP)` |
| Recall | Of actual positives, share found. | `TP/(TP+FN)` |
| Cross-validation | Repeated training/validation across folds. | `GridSearchCV(...,cv=5)` |
| RFM | Recency, frequency, monetary segmentation. | VIP / loyal / at-risk actions. |

**Interview answer:** “I choose the metric from error cost. For fraud, accuracy can be misleading because non-fraud is common; I compare precision, recall and PR-AUC and set a threshold based on review capacity.”

## Data engineering and GenAI

| Concept | Definition and use | Example |
|---|---|---|
| Pipeline | Controlled movement from source to trusted serving layer. | Source -> raw -> staging -> marts -> metrics. |
| Data contract | Producer/consumer agreement about schema, owner, freshness and meaning. | `order_id` non-null and daily refresh by 08:00. |
| Lineage | Trace of where a value came from. | Revenue <- metrics model <- cleaned orders. |
| Metrics layer | Centralized business calculation definitions. | Paid sales minus refunds, at order-line grain. |
| LLM | Token-prediction model used for language tasks. | Context + task + constraints + output schema. |
| RAG | Retrieval of approved passages before answer generation. | Retrieve policy chunk, then answer with citation. |
| Structured output | Response limited to a validated schema. | JSON category, priority, rationale. |
| Tool contract | Allowed arguments, permissions, results and approval rules for a tool. | Read-only balance lookup with validated customer ID. |
| Agent | Controlled loop for planning and tool use. | Plan -> tool -> validate -> evaluate -> human approve. |
| Prompt injection | Untrusted content attempts to change system instructions. | Treat documents as data, not authority. |
| FDE | Forward Deployed Engineering: close-to-user technical delivery focused on adoption and outcomes. | Workflow discovery -> integration -> data contract -> success metric. |

## Portfolio sequence

1. Use a permitted ecommerce dataset.
2. Clean it in Excel/Power Query; state the row grain.
3. Build SQL quality tests and KPIs.
4. Create a Power BI semantic model and report.
5. Produce a reproducible Python analysis.
6. Build and validate a simple ML or RFM project.
7. Build a grounded assistant over an approved data dictionary.
8. Publish a README with question, data contract, validation, limits and next action.
