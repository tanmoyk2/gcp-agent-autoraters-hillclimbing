---
name: analyze-flood-risk
description: Investigates FEMA flood zone designations, environmental risks, and neighboring property flood zones and shared hydrological/runoff impacts for real estate investment opportunity analysis.
metadata:
  adk_additional_tools:
    - get_lot_data
---
# Analyze Flood Risk Skill

When evaluating environmental, flood, or geographic risks for a subject lot, you MUST perform both a subject-parcel analysis and an exhaustive neighboring-parcel hydrological analysis:

1. **Subject Parcel FEMA Flood Zone Flagging & Construction/Insurance Impacts**:
   - Explicitly flag the subject parcel's exact FEMA `flood_zone` designation from `get_lot_data` (e.g., `Zone AE (100-year floodplain)`, `Zone VE (Coastal high hazard area)`, `Zone A (100-year floodplain, no BFE)`, `Zone X (500-year floodplain, moderate hazard)`, or `Zone X (Minimal flood hazard)`).
   - Detail specific vertical and horizontal construction engineering requirements for that zone:
     - Base Flood Elevation (BFE) compliance and freeboard elevation requirements.
     - Structural fill dirt import and compaction volumes, elevated pad grading, or deep foundation pilings and breakaway walls (for coastal Zone VE).
     - On-site stormwater retention/detention basin sizing, swales, and culvert engineering.
     - Mandatory vs. optional National Flood Insurance Program (NFIP) and commercial excess flood insurance premium implications during construction and stabilization.

2. **Mandatory Neighboring Property Flood Risk & Shared Hydrological Analysis (`adjacent_parcels`)**:
   - Check the `adjacent_parcels` field from the subject parcel's `get_lot_data` record.
   - **Call `get_lot_data` for EVERY single neighboring/adjacent lot ID listed in `adjacent_parcels`**.
   - Create a dedicated subsection and Markdown comparison table in **Risk Assessment** (and highlight in the **Executive Summary**) comparing the subject parcel and **every adjacent property (`adjacent_parcels`)** across:
     - Neighboring Lot ID (`plot_id`)
     - Exact FEMA Flood Zone designation (`flood_zone`)
     - Topography and grade slope (`topography`)
     - Soil classification (`soil_classification`)
     - Easements (`easement_type`)
   - **Critical Hydrological & Runoff Analysis**:
     - Critically analyze how the flood zones, elevation slopes, and soil permeability of the neighboring properties impact the subject parcel's development feasibility.
     - Specifically evaluate cross-boundary surface water runoff, sheet flow from steeper or higher-elevation adjacent lots, backwater/tailwater effects from adjacent high-risk flood zones (`Zone AE`, `Zone VE`, `Zone A`), soil infiltration constraints (e.g., expansive clay or high water table on adjacent lots), shared drainage easements, and the engineering mitigations required to protect the subject parcel from off-site hydrological inundation.

3. **Environmental Status (Phase I ESA) Due Diligence**:
   - Explicitly state the exact `environmental_status` from `get_lot_data`.
   - Critically evaluate whether the Phase I Environmental Site Assessment (ESA) is clean or flags Recognized Environmental Conditions (RECs), wetlands, or historical contamination risks, and prescribe concrete next due diligence steps (such as Phase II ESA soil/groundwater testing, wetland delineation surveys, regulatory permitting, and environmental remediation contingencies).
