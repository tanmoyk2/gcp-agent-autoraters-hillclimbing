---
name: analyze-opportunity
description: Investigates a land parcel and its adjacent neighboring parcels for real estate investment opportunity analysis, deriving exact acquisition cost-per-acre as a core valuation metric and evaluating site, flood, environmental, and tax characteristics.
metadata:
  adk_additional_tools:
    - get_lot_data
    - get_tax_assessment_data
---
# Analyze Opportunity Skill

When asked to investigate a property or analyze an investment opportunity for a lot, follow every step below thoroughly:

1. **Retrieve Subject Lot Data**:
   - Call `get_lot_data` with the target lot ID (`plot_id`).
   - Record all core specifications: `plot_id`, `parcel_apn`, `acreage`, `zoning`, `last_sale_price`, `last_sale_date`, `flood_zone`, `soil_classification`, `topography`, `utility_access`, `easement_type`, `environmental_status`, and `adjacent_parcels`.

2. **Mandatory Neighboring Parcel Investigation (`adjacent_parcels`)**:
   - Inspect the `adjacent_parcels` list returned by `get_lot_data` for the subject lot.
   - **You MUST call `get_lot_data` for EVERY neighboring/adjacent parcel ID listed in `adjacent_parcels`** so you can report their exact FEMA `flood_zone` designations, `topography`, `soil_classification`, and `easement_type` and critically analyze cross-boundary drainage, runoff, and shared hydrological impacts on the subject parcel.

3. **Mandatory Core Valuation Metric — Acquisition Cost-Per-Acre Calculation**:
   - Consult the `analyze-tax-implications` skill and call `get_tax_assessment_data` using the subject lot's `parcel_apn`.
   - Derive and highlight the **exact mathematical Acquisition Cost-Per-Acre** as a **core valuation metric** in both the **Executive Summary** and **Acquisition Basis and Holding Costs** sections (both in bold prose and in a Markdown summary table):
     - **Formula**: `Acquisition Cost-Per-Acre = Last Sale Price / Acreage = $[last_sale_price] / [acreage] acres = $[exact_cost_per_acre] per acre` (show exact division formula and result rounded to two decimal places).
     - **Valuation Benchmarking**: Also calculate `Assessed Land Value Per Acre = $[assessed_land_value] / [acreage] acres = $[assessed_land_per_acre] per acre` and `Total Assessed Value Per Acre = $[total_assessed_value] / [acreage] acres`, and benchmark the Acquisition Cost-Per-Acre against the county assessed land basis per acre and typical market land basis for the parcel's zoning designation to evaluate acquisition basis efficiency.
   - Also calculate the exact **Monthly Tax Holding Cost**:
     - **Formula**: `Monthly Tax Holding Cost = Annual Tax Amount / 12 = $[annual_tax_amount] / 12 = $[monthly_tax_cost] per month`, and evaluate pre-construction carrying cost impact over 12-, 24-, and 36-month entitlement horizons.

4. **Comprehensive Flood, Neighboring Hydrology, Infrastructure, and Environmental Evaluation**:
   - Consult the `analyze-flood-risk` skill to evaluate both the subject parcel's exact FEMA flood zone (including BFE, fill dirt, deep pilings, foundation engineering, and NFIP flood insurance impacts) AND the exact FEMA flood zones, topography slopes, and soil types of all `adjacent_parcels`, critically analyzing drainage, surface runoff, and shared hydrological risks.
   - Prominently display `plot_id`, `parcel_apn`, `acreage`, and `zoning` in a Markdown summary table in the Executive Summary.
   - Analyze `utility_access` distances and `topography` / `soil_classification` to estimate site preparation and horizontal infrastructure CapEx.
   - Critically evaluate `environmental_status` (Phase I ESA findings) and prescribe exact environmental due diligence next steps (e.g., Phase II ESA subsurface sampling, wetland delineation, or remediation budgeting).
