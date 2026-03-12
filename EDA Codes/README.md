Judgment Court Notebooks
This repository contains two Jupyter notebooks used to explore and prepare judicial case data stored in a PostgreSQL database:

Judgment_Court_EDA.ipynb
Initializing_CaseOutcome_distribution_of_Courts.ipynb
Both notebooks are designed to run in Google Colab but can be adapted to any environment with access to the target PostgreSQL instances.

1. Judgment_Court_EDA.ipynb
Purpose

This notebook performs exploratory data analysis (EDA) on court case data stored in two PostgreSQL databases:

An original database containing raw judicial activity records (e.g., case_actions).
An updated database with a curated table business_suing_individuals, where businesses sue individual defendants.
It focuses on understanding the structure, size, and content of these tables to support downstream modeling and reporting.

Main Tasks

Database connection
Uses sqlalchemy.create_engine to connect to:
URL_ORIGINAL (original DS701 database).
URL_UPDATE (updated DS701 database with read user).
Table inspection
Inspects table metadata such as:
Number of rows and columns.
Column names and data types.
Previews a subset of records for:
case_actions (action history at the case level).
business_suing_individuals (plaintiff/defendant details, court, status).
Data profiling
Uses pandas to inspect:
Distribution of IDs (e.g., case_action_id, case_id).
Example values for categorical fields (actor, action, court_name, case_status).
Temporal fields (date_time, file_date, status_date).
Validation of update process
Compares original and updated tables to verify that the transformation pipeline for business-vs-individual cases has produced consistent and usable data.
Key Columns Explored

case_actions (original DB):
case_action_id, case_id, actor, action, description, date_time, file_reference_number, last_indexed.
business_suing_individuals (updated DB):
case_id, case_number, plaintiff_name, defendant_name, plaintiff_id, defendant_id, court_name, file_date, case_status, status_date.
How to Run

Open Judgment_Court_EDA.ipynb in Google Colab.
Ensure that the database URLs (URL_ORIGINAL and URL_UPDATE) are valid and reachable from your environment.
Run all cells in order:
The first cell installs required libraries if necessary.
Subsequent cells set up the engine connections and perform EDA.
2. Initializing_CaseOutcome_distribution_of_Courts.ipynb
Purpose

This notebook initializes and explores the distribution of case outcomes across different courts using the business_suing_individuals table. It is designed as a starting point for:

Statistical analysis of case outcomes by court.
Building visualizations or models that compare courts on metrics such as closure status and timing.
Main Tasks

Library and environment setup
Installs and imports:
sqlalchemy
psycopg2-binary
pandas
Database connection
Connects to the PostgreSQL instance containing the business_suing_individuals table.
Table discovery
Lists available tables and confirms the presence of:
business_suing_individuals
Initial data preview
Loads a sample of rows from business_suing_individuals into a pandas DataFrame.
Displays core fields such as:
case_id, case_number, plaintiff_name, defendant_name, plaintiff_id, defendant_id, court_name, file_date, case_status, status_date.
Confirms:
Number of unique courts.
Possible values of case_status (e.g., Closed, Disposed (Statistical Purposes)).
Although the notebook is primarily focused on initialization and inspection, it provides the foundation for:

Computing distributions of case outcomes for each court_name.
Analyzing temporal patterns via file_date and status_date.
How to Run

Open Initializing_CaseOutcome_distribution_of_Courts.ipynb in Google Colab.
Verify that the PostgreSQL connection details are correct for your environment.
Run the notebook cells sequentially:
First cell: install and import dependencies.
Next cells: connect to the DB, list tables, load and preview business_suing_individuals.
Extend the notebook to:
Group by court_name and case_status.
Compute counts or percentages for each outcome category.
Create visualizations of case outcome distributions across courts.
Dependencies
Both notebooks rely on the following Python packages:

pandas
sqlalchemy
psycopg2-binary
(Google Colab environment helpers such as google.colab for interactive usage)
To install them locally (outside Colab), run:

pip install pandas sqlalchemy psycopg2-binary
Notes
Security: The notebooks contain database connection strings. If you plan to publish or share this project, ensure that you remove or securely manage any credentials (e.g., via environment variables or secrets management).
Environment: The examples are written assuming a PostgreSQL backend and Google Colab. Adjust the connection URLs and installation commands as needed for your own environment or hosting.
