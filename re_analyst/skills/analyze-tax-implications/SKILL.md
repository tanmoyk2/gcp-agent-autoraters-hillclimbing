---
name: analyze-tax-implications
description: Investigates property tax holding costs, county assessment records, and acquisition cost-per-acre valuation metrics for a parcel.
metadata:
  adk_additional_tools:
    - get_tax_assessment_data
    - get_lot_data
---
# Analyze Tax Implications Skill

When investigating financial carrying costs, acquisition basis, or tax implications for a lot, perform all calculations explicitly and present them in both prose and a structured Markdown financial summary table:

1. **Retrieve Tax Assessment Records**:
   - Locate the `parcel_apn` from the subject lot's `get_lot_data` record.
   - Call `get_tax_assessment_data` with that `parcel_apn` to retrieve `assessed_land_value`, `assessed_improvement_value`, `total_assessed_value`, `annual_tax_amount`, `millage_rate`, `tax_delinquency_status`, and `special_assessments`.

2. **Core Valuation Metric — Exact Acquisition Cost-Per-Acre Calculation & Benchmarking**:
   - Using `last_sale_price` and `acreage` from `get_lot_data`, explicitly compute and highlight the **Acquisition Cost-Per-Acre** as a **core valuation metric**:
     - **Explicit Derivation Formula**:
       `Acquisition Cost-Per-Acre = Last Sale Price / Acreage = $[last_sale_price] / [acreage] acres = $[cost_per_acre] per acre`
   - **Benchmarking as a Core Valuation Metric**:
     - Compute the **Assessed Land Value Per Acre**:
       `Assessed Land Value Per Acre = Assessed Land Value / Acreage = $[assessed_land_value] / [acreage] acres = $[assessed_land_per_acre] per acre`
     - Compute the **Price-to-Assessed-Value Ratio**:
       `Last Sale Price / Total Assessed Value = $[last_sale_price] / $[total_assessed_value] = [ratio]x ([percentage]%)`
     - Emphasize **Acquisition Cost-Per-Acre** prominently in bold in the **Executive Summary** and **Acquisition Basis and Holding Costs** sections, and analyze whether the acquisition basis per acre represents a discount or premium relative to the county's assessed land value per acre and development density potential under the lot's zoning.

3. **Explicit Monthly Tax Holding Cost Calculation & Pre-Development Budgeting**:
   - Explicitly compute the **Monthly Tax Holding Cost** from `annual_tax_amount`:
     - **Explicit Derivation Formula**:
       `Monthly Tax Holding Cost = Annual Tax Amount / 12 = $[annual_tax_amount] / 12 = $[monthly_tax_holding_cost] per month`
   - Also compute the **Annual and Monthly Tax Per Acre** (`$[annual_tax_amount] / [acreage] acres` and `$[monthly_tax_holding_cost] / [acreage] acres`).
   - Analyze how this monthly tax carrying cost, combined with the `millage_rate`, `tax_delinquency_status` (including any back taxes or lien cure costs), and `special_assessments` (e.g., MUD, Mello-Roos, infrastructure bonds), impacts pre-construction holding budgets across 12-month, 24-month, and 36-month entitlement and permitting timelines.
