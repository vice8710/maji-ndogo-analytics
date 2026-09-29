# Case Study: Maji Ndogo Analytical Engineering Engine

## 1. Executive Summary & Business Problem
The Ministry of Agriculture required an urgent planting recommendation for northern highland plots based on 5,654 field survey records. Legacy operations relied on unvalidated dictionary objects and unindexed linear loops, exposing downstream agricultural policy decisions to data entry errors and severe scalability bottlenecks.

* **Data Integrity Risk:** Unvalidated raw inputs allowed corrupted entries (e.g., negative plot sizes or impossible pollution levels above 100%) to pass unchecked into downstream reporting scripts.
* **Scalability Bottlenecks:** Unindexed $O(n)$ linear list scans created latency during field inspector queries. As dataset volume expands toward 1,000,000 records, linear lookups become unviable.
* **Objective:** Build an enterprise-grade analytical pipeline using Python OOP and Pandas to validate inputs at the ingestion boundary, perform relational SQLite joins, and deliver data-backed crop recommendations under a strict delivery deadline.

---

## 2. Technical Architecture & Stack

* **Data Ingestion & Integrity:** Custom Python classes using `@property` getters and setters to enforce schema-level validation and raise early `ValueError` exceptions upon invalid data ingestion.
* **Algorithmic Efficiency:** Custom sorting algorithms paired with $O(\log n)$ Binary Search routines to ensure efficient record lookups across high-volume datasets.
* **Relational Database & Analytics:** SQLite for relational survey queries coupled with Pandas DataFrames for data cleaning, multi-table joins, and statistical aggregations.
* **Version Control Hygiene:** Git terminal workflow with a strict `.gitignore` policy excluding raw SQLite files (`*.db`) and local runtime artifacts.

---

## 3. Implementation Details & Evidence Trail

### Data Integrity & Validation Boundary
To protect downstream analytics from corrupted field reports, inputs are encapsulated at the object layer. Attempting to instantiate or update a record with out-of-bounds metrics triggers an explicit exception before reaching the database.

![Data Validation Error](images/01-data-validation-error.png)  
*Figure 1: OOP encapsulation triggering an explicit `ValueError` when an out-of-bounds pollution reading is ingested.*

 ## High-Performance Search Execution
 Replacing $O(n)$ linear scans with an $O(\log n)$ Binary Search routine reduces maximum query steps across 1,000,000 records from 1,000,000 comparisons down to approximately 20 steps.Figure 2: Execution results confirming filtering and search logic across field records.Traceable Analytical PipelineFour relational tables (geographic_features, weather_features, soil_and_crop_features, and farm_management_features) were merged via SQLite joins and cleaned in Pandas (MD_agric_df).   2.Figure 3: Multi-variable aggregation showing crop performance across environmental variables.Key Finding: Highland plots at high elevation ($\sim 775\text{ m}$) with substantial annual rainfall ($\sim 1,535\text{ mm}$) and low pollution levels ($< 0.0001$) yield optimal conditions specifically for Tea.Version Control & Commit HistoryA clean, atomic commit history reflects disciplined project delivery and strict system hygiene:Figure 4: Terminal output of git log --oneline displaying structured commit tracking.
 ## 4. Strategic Impact
 1. Defensible Policy: The recommendation for Tea in the northern highlands is fully reproducible via auditable SQL joins and Pandas transformations.
 2. Fail-Safe Ingestion: Object-level validation rules guarantee zero silent failures or metric corruption in executive dashboards.
 3. Future-Proof Scale: $O(\log n)$ algorithmic lookups ensure the engine handles growth to a million records without requiring infrastructure re-engineering.