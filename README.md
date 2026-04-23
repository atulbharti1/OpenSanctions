# OpenSanctions Entity Risk Profiling Pipeline
 
A Python-based pipeline for cleaning, structuring, and feature-engineering entity-level data from the [OpenSanctions](https://www.opensanctions.org/) dataset for sanction risk analysis.
 
---
 
## Overview
 
This project processes raw OpenSanctions data — structured around the [FollowTheMoney (FtM)](https://followthemoney.tech/) schema — to build a clean, analysis-ready dataset for entity-level risk profiling. It handles multi-schema entities (companies, ownership networks, directorships) and engineers features capturing governance patterns and identity signals relevant to sanction risk.
 
---
 
## Project Structure
 
```
opensanctions-pipeline/
│
├── data/
│   └── raw/                  # Raw FtM JSON input (not tracked in git)
│
├── notebooks/
│   └── exploration.ipynb     # Initial data exploration
│
├── src/
│   ├── cleaning.py           # Schema parsing and entity cleaning
│   ├── features.py           # Feature engineering (governance, identity)
│   └── pipeline.py           # End-to-end pipeline runner
│
├── outputs/
│   └── entity_features.csv   # Final processed dataset (not tracked in git)
│
├── requirements.txt
└── README.md
```
 
---
 
## Data Source
 
**OpenSanctions** aggregates global sanctions lists, politically exposed persons (PEPs), and corporate ownership data into a unified, open dataset. Data is structured using the **FollowTheMoney schema** — a graph-based JSON format where entities (companies, people, assets) are linked through typed relationships (ownership, directorship, family ties).
 
- Dataset: [opensanctions.org/datasets](https://www.opensanctions.org/datasets/)
- Schema reference: [followthemoney.tech](https://followthemoney.tech/)
> **Note:** Raw data files are not included in this repository due to size. Download instructions below.
 
---
 
## Pipeline Steps
 
### 1. Schema Parsing & Cleaning
- Ingests multi-schema FtM JSON entities
- Separates records by schema type: `Company`, `Ownership`, `Directorship`, `Person`
- Handles missing fields, nested properties, and multi-value attributes
- Normalizes country codes, date formats, and name variants
### 2. Network Construction
- Links entities across schemas using FtM's subject-object relationship structure
- Reconstructs ownership chains and directorship networks per entity
### 3. Feature Engineering
 
**Governance features:**
- Number of directorships held
- Ownership concentration (direct vs. indirect)
- Cross-border ownership flags
- Shell company indicators (minimal staff + high ownership links)
**Identity features:**
- Name alias count
- Jurisdiction diversity score
- Document inconsistency flags (mismatched nationality/registration)
### 4. Output
- Produces a flat, entity-level feature matrix ready for downstream risk modelling or classification
---
 
## Installation
 
```bash
git clone https://github.com/atulbharti1/opensanctions-pipeline.git
cd opensanctions-pipeline
pip install -r requirements.txt
```
 
---
 
## Usage
 
```bash
# Run the full pipeline
python src/pipeline.py --input data/raw/ --output outputs/entity_features.csv
```
 
---
 
## Requirements
 
```
pandas
numpy
scikit-learn
```
 
---
 
## Relevance
 
This pipeline was developed as part of broader work on structured data quality and reproducible analytical workflows. The FollowTheMoney schema presents challenges common to real-world knowledge graphs — variable entity completeness, multi-valued properties, and cross-schema joins — making it a useful testbed for robust data engineering practices.
 
---
 
## Author
 
**Atul Bharti**
MDS Student, Hertie School Berlin
[github.com/atulbharti1](https://github.com/atulbharti1) · [LinkedIn](https://linkedin.com/in/)
 
---
 
## License
 
MIT License
