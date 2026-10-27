# Data & AI Interview Workbook

## Answer structure

Use **definition -> context -> example -> trade-off -> validation**.

## Technical questions

1. **What is data grain?**  
   The real-world unit represented by a row. I state it before aggregation or joins; for example, an order-line table has one product line per record. I validate that totals still reconcile after grouping.

2. **What is the difference between WHERE and HAVING?**  
   WHERE filters rows before aggregation; HAVING filters groups after aggregation. I use HAVING when the condition depends on a metric such as total sales.

3. **How do you prevent join duplication?**  
   I document row grain and key cardinality, test uniqueness on the right side, and reconcile count and sum before/after the join.

4. **Measure versus calculated column in Power BI?**  
   A calculated column is computed row-by-row during refresh; a measure evaluates at query time in filter context. I use measures for responsive KPIs and columns when a row-level attribute is needed.

5. **What does CALCULATE do?**  
   CALCULATE evaluates a measure under modified filter context. I use it for time intelligence or controlled filter removal and test it in a table visual.

6. **How do you make Python work reproducible?**  
   I separate configuration from code, pin dependencies, document source and grain, rerun from a fresh kernel, and remove hidden manual steps and secrets.

7. **What is data leakage?**  
   A feature contains information unavailable at the time of prediction. I split data before preprocessing and review every field from the perspective of prediction time.

8. **Precision versus recall?**  
   Precision is the share of predicted positives that are correct; recall is the share of actual positives found. I choose the balance based on false-positive and false-negative cost.

9. **Why is a test set protected?**  
   It estimates future performance. If I tune against it repeatedly, it stops being independent and performance is optimistic.

10. **When would you use RAG?**  
    When answers must be based on changing or approved documents and need citations. I still test relevance, permissions and unsupported questions.

11. **Why use structured outputs?**  
    They let the application validate a predictable schema rather than trusting free-form prose. I reject or retry invalid data before any action.

12. **What makes an agent safe?**  
    Narrow tools, explicit permissions, validated inputs/outputs, logs, evaluation cases, safe failure behavior and human approval for consequential actions.

13. **What is prompt injection?**  
    Untrusted content attempting to override the system objective. I treat retrieved documents as data, prevent them from directing tools and enforce trusted instruction priority.

14. **How would you explain FDE?**  
    Forward Deployed Engineering brings technical delivery close to the user workflow: discover needs, integrate safely, define data contracts, measure adoption and hand off a maintainable solution.

## Scenario drills

- A dashboard total changed overnight: inspect source freshness, schema, transformation, relationship cardinality, filter context, metric definition and reconciliation before changing a visual.
- A GenAI assistant answers confidently without evidence: require citations, add an unsupported-answer test, strengthen retrieval and return an unknown response when no support exists.
- A model has high accuracy but misses costly cases: evaluate class balance, precision/recall and threshold against the cost of false negatives.
- A stakeholder asks for full agent autonomy: clarify the action risk, start with a constrained workflow and require human approval for publishing, changing data or external communication.
