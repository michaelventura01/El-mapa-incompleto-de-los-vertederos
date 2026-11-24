# The Incomplete Map of Landfills

## Repository Analysis and Technical Documentation

**Repository:**
[michaelventura01/El-mapa-incompleto-de-los-vertederos](https://github.com/michaelventura01/El-mapa-incompleto-de-los-vertederos)\
**Primary domain:** Municipal solid waste management and data mining\
**Geographic context:** Santiago de los Caballeros and Moca, Dominican
Republic\
**Academic context:** Data Mining -- MACDIA, Universidad Autónoma de
Santo Domingo (UASD)\
**Documentation language:** English

------------------------------------------------------------------------

## 1. Executive Summary

*The Incomplete Map of Landfills* is a data-mining project focused on
the analysis of municipal solid-waste weighing and collection records.
Its central context is the evaluation of the municipal solid-waste
management system of Santiago de los Caballeros, with supporting
material and records also referring to Moca.

The repository brings together heterogeneous source material---including
CSV files, Excel workbooks, PDF documents, images, and Jupyter
notebooks---and uses Python-based data processing to consolidate,
inspect, clean, and prepare waste-management data for analysis.

The project is valuable because it addresses a real public-sector and
environmental-management problem. Its current repository artifacts are
best understood as a data preparation and exploratory analysis workflow.
The repository title suggests a geospatial inventory or map of disposal
sites; however, the available weighing dataset and notebooks should not
be interpreted as a complete, verified geographic inventory unless
authoritative landfill locations and coordinates are added and
validated.

### Main objectives

-   Consolidate waste collection and weighing information from different
    source formats.
-   Extract structured information from spreadsheets, CSV files, and PDF
    documents.
-   Standardize and inspect the resulting datasets.
-   Identify missing values, duplicates, temporal inconsistencies, and
    unusual observations.
-   Create analytical variables that support descriptive and temporal
    analysis.
-   Prepare data for subsequent data-mining and
    environmental-intelligence work.

------------------------------------------------------------------------

## 2. Repository Overview

The public repository currently exposes the following principal folders
and files:

  ----------------------------------------------------------------------------------------------------------------------------------------------------
  Path                                                                                                             Purpose inferred from the
                                                                                                                   repository contents
  ---------------------------------------------------------------------------------------------------------------- -----------------------------------
  `csv_file/`                                                                                                      CSV source files used during data
                                                                                                                   ingestion and consolidation.

  `pdf_file/`                                                                                                      PDF source documents and supporting
                                                                                                                   material.

  `picture_file/`                                                                                                  Image resources associated with the
                                                                                                                   project.

  `procesed/`                                                                                                      Processed or intermediate data
                                                                                                                   artifacts. The original spelling is
                                                                                                                   retained here to match the
                                                                                                                   repository.

  `RETO02_El_mapa_incompleto_de_los_vertederos.ipynb`                                                              Notebook for source extraction,
                                                                                                                   consolidation, and initial
                                                                                                                   processing.

  `RETO02_Mapa_Vertederos.ipynb`                                                                                   Notebook for data exploration,
                                                                                                                   quality assessment, and analytical
                                                                                                                   preparation.

  `desechos_csv_unificado.csv`                                                                                     Consolidated waste-related CSV
                                                                                                                   dataset.

  `recoleccion_residuos.xlsx`                                                                                      Excel workbook containing waste
                                                                                                                   collection/weighing records.

  `residuos_limpio.csv`                                                                                            Cleaned waste dataset produced by
                                                                                                                   the workflow.

  `Explicación del Reto 5 - Pesaje de Residuos Santiago y Moca - Grupo Marrón - Data Mining - MACDIA - UASD.pdf`   Academic challenge description and
                                                                                                                   source context for the weighing
                                                                                                                   analysis.
  ----------------------------------------------------------------------------------------------------------------------------------------------------

The repository page identifies the municipal evaluation of Santiago de
los Caballeros' urban solid-waste management system as its subject. The
repository is public and its default branch is `main`.

------------------------------------------------------------------------

## 3. Business and Environmental Context

Municipal solid-waste management depends on reliable information about
collection activity, quantities, service providers, time periods, and
final disposal destinations.

Weighing records can help answer operational questions such as:

-   How much waste is collected during a given day, month, or year?
-   How does collection volume vary by weekday or season?
-   What proportion of recorded waste is associated with municipal or
    other collection operations?
-   Are there unusual changes in daily tonnage?
-   Are collection records complete and internally consistent?
-   What additional information is required to connect collected waste
    to its final disposal location?

The project provides a starting point for answering data-oriented
questions. It should not, by itself, be treated as proof of landfill
capacity, environmental impact, illegal dumping locations, or the
geographic destination of every recorded load. Those questions require
additional validated sources.

------------------------------------------------------------------------

## 4. Data Sources and Ingestion

The repository contains multiple data formats, which introduces common
data-engineering challenges:

1.  Different schemas and column names.
2.  Different date and number formats.
3.  Tables embedded in PDF documents.
4.  Multiple sheets in Excel workbooks.
5.  Potentially inconsistent encodings and delimiters in CSV files.
6.  Different levels of detail and geographic coverage.
7.  Unclear or incomplete provenance for some records.

### 4.1 CSV sources

CSV files are used as source and intermediate datasets. Ingestion should
explicitly control:

-   Character encoding.
-   Delimiter and quote handling.
-   Decimal and thousands separators.
-   Date parsing.
-   Column data types.
-   Source file identification.
-   Row counts before and after processing.

A key implementation risk identified in the extraction workflow is the
use of a row limit such as `nrows=1000` when reading a CSV. If this
limit remains enabled for production processing, records beyond the
first 1,000 rows will not be ingested. It should be removed unless
sampling is intentional and clearly documented.

### 4.2 Excel source

The repository includes `recoleccion_residuos.xlsx`. The analysis
notebook documents a workbook structure with 13 sheets: one annual
summary and 12 monthly sheets. The monthly consolidation is documented
as producing 362 records and 18 columns.

These figures are reported notebook results, not a fresh execution
performed as part of this documentation. They should be revalidated
whenever the source workbook changes.

### 4.3 PDF extraction

The repository's first notebook references tools for extracting tables
and text from PDF documents. PDF extraction is inherently less reliable
than reading structured files because document layout, scanned pages,
merged cells, and OCR errors can affect the output.

Extracted PDF records should therefore be treated as provisional until
they pass validation against the original pages.

### 4.4 Images and OCR

Image processing and OCR can help recover information from scanned
documents. OCR output must be reviewed for:

-   Incorrectly recognized digits.
-   Decimal separator errors.
-   Missing minus signs.
-   Confused date characters.
-   Shifted table columns.
-   Incomplete rows.

A robust pipeline should preserve the original image or PDF reference
and record the extraction method used for each resulting row.

------------------------------------------------------------------------

## 5. Notebook Analysis

### 5.1 `RETO02_El_mapa_incompleto_de_los_vertederos.ipynb`

This notebook is associated with the source extraction and initial
processing stage.

The technologies referenced in the workflow include:

  Technology    Typical role in the project
  ------------- -------------------------------------------------------
  Python        Main programming language.
  Pandas        Tabular ingestion, transformation, and consolidation.
  NumPy         Numerical operations and data preparation.
  Tabula        Extraction of tables from PDF documents.
  Camelot       PDF table extraction.
  PyTesseract   Optical character recognition (OCR).
  OpenCV        Image preprocessing for extraction workflows.
  Matplotlib    Static data visualization.
  Plotly        Interactive visualizations.

The notebook's role is to bring information from different source
formats into a form that can be analyzed consistently.

**Engineering considerations**

-   Avoid hard-coded local paths where possible.
-   Separate extraction logic from transformation logic.
-   Capture source filename and source sheet/page.
-   Record row counts at each processing stage.
-   Avoid silently skipping files when an exception occurs.
-   Make ingestion repeatable and safe to rerun.
-   Do not impose row limits unintentionally.
-   Preserve raw source values before applying cleaning rules.

### 5.2 `RETO02_Mapa_Vertederos.ipynb`

This notebook focuses on exploratory analysis and data-quality
assessment of the waste collection/weighing dataset.

The documented workflow includes:

-   Consolidation of monthly Excel sheets.
-   Inspection of date and operational fields.
-   Duplicate checks.
-   Missing-value analysis.
-   Weekday/date consistency checks.
-   Outlier detection using the interquartile range (IQR).
-   Creation of temporal and analytical features.
-   Preparation of data for further mining and visualization.

The notebook is especially relevant because it moves the project from
file consolidation toward analytical interpretation.

------------------------------------------------------------------------

## 6. Data Quality Assessment

The notebook outputs previously documented the following results for the
consolidated workbook:

  Quality check                             Reported result
  --------------------------------------- -----------------
  Consolidated records                                  362
  Columns                                                18
  Monthly sheets consolidated                            12
  Duplicate records detected                              0
  Missing values in `AMS_TON`                             1
  Missing values in `TOTAL_GENERAL_TON`                   0
  Weekday/date inconsistencies                            6
  Outlier observations flagged                           54

**Important:** These are reported results from the notebook artifacts.
They have not been independently recomputed for this Markdown document.
Re-run the notebooks against the current repository files before using
these figures in an official report.

### 6.1 Duplicate records

The notebook reports no duplicate records in the consolidated dataset. A
stronger production-quality check should define the business key
explicitly. For example, a candidate key could combine date, collection
entity, vehicle or ticket identifier, and weighing event---provided
those fields exist and are reliable.

A row-level duplicate check alone may fail to identify duplicate
business events whose metadata differs slightly.

### 6.2 Missing values versus zero

A missing value and a numeric zero have different meanings:

-   **Zero:** a measured or explicitly recorded quantity of zero.
-   **Null:** the value is unknown, missing, or unavailable.
-   **No operation:** an independently confirmed absence of collection
    activity.

Replacing missing values with zero is only valid when the source
documentation or business process confirms that the missing value means
no activity. Otherwise, the replacement can bias totals and averages.

Recommended treatment:

-   Preserve the original value.
-   Add a data-quality status or missing-value flag.
-   Apply imputation only in a separate analytical field.
-   Document the business rule used for each replacement.

### 6.3 Date and weekday consistency

Six inconsistencies were reported between the weekday recorded in the
source and the weekday calculated from the date.

Recommended validation:

1.  Parse the source date using an explicit format.
2.  Calculate the weekday from the parsed date.
3.  Compare calculated and source weekday values.
4.  Flag mismatches.
5.  Correct only when the date or weekday can be verified from
    authoritative evidence.

The calculated weekday should not automatically overwrite the source
value without retaining the original.

### 6.4 Outlier detection

The notebook reports 54 observations flagged as outliers using the IQR
method. It also documents winsorization/capping as a treatment.

An outlier is not necessarily an error. High daily tonnage may
represent:

-   Special collection operations.
-   Accumulated waste collected after a service interruption.
-   Seasonal or event-driven activity.
-   A change in collection frequency.
-   A legitimate operational peak.
-   A data-entry or measurement error.

**Recommendation:** preserve raw measurements and create separate
adjusted values only when the adjustment is justified.

Suggested fields:

-   `TOTAL_GENERAL_TON_RAW`
-   `TOTAL_GENERAL_TON_ADJUSTED`
-   `IS_OUTLIER`
-   `OUTLIER_REASON`
-   `ADJUSTMENT_METHOD`

This makes the analytical process traceable and prevents irreversible
alteration of source measurements.

------------------------------------------------------------------------

## 7. Feature Engineering

The notebook documents the creation of temporal and analytical
variables, including:

  -----------------------------------------------------------------------
  Feature                             Analytical purpose
  ----------------------------------- -----------------------------------
  `PROP_AYUNTAMIENTO`                 Represents a municipal proportion
                                      or share; its exact formula and
                                      denominator should be documented in
                                      the notebook.

  `ES_FIN_DE_SEMANA`                  Identifies weekend records.

  `DIA_MES`                           Day of the month.

  `TRIMESTRE`                         Calendar quarter.

  `SEMANA_ANIO`                       Week of the year.

  `CAT_VOLUMEN`                       Categorical grouping of recorded
                                      volume.
  -----------------------------------------------------------------------

These features support segmentation and descriptive analysis.

### Volume categories

The notebook's reported category distribution is:

  Category      Records
  ----------- ---------
  Very Low            0
  Low                 0
  Medium             70
  High              256
  Very High          36
  **Total**     **362**

The category thresholds should be documented explicitly. If thresholds
are based on IQR, quantiles, or fixed business rules, the method should
be stated and versioned. If categories are calculated from the entire
dataset, be aware that new data may change the thresholds and historical
classifications.

------------------------------------------------------------------------

## 8. Temporal Coverage and Interpretation Limitations

The available records have been described as covering periods between
April 2022 and December 2023, but the source sheets do not represent
every consecutive month in that interval.

The notebook's analysis should therefore distinguish among:

-   Months with complete data.
-   Months with partial data.
-   Months with no source records.
-   Months not included in the available source material.

A missing month must not be interpreted as zero waste generation.

### Recommended coverage table

Create a calendar-based coverage dataset with fields such as:

  Field               Description
  ------------------- -----------------------------------------
  `YEAR`              Calendar year.
  `MONTH`             Calendar month.
  `EXPECTED_DAYS`     Expected days in the reporting period.
  `OBSERVED_DAYS`     Number of days with source records.
  `COVERAGE_RATE`     Observed days divided by expected days.
  `COVERAGE_STATUS`   Complete, partial, or unavailable.

Do not compare monthly totals without considering coverage. Where
appropriate, report both the observed total and a clearly labeled
normalized metric. Do not extrapolate missing periods without an
explicit statistical method.

------------------------------------------------------------------------

## 9. Geospatial Gap: Why the Map Is Still Incomplete

The repository's title emphasizes an incomplete map of landfills.
However, weighing and collection records do not automatically provide
the geographic information needed to create a reliable landfill map.

A geospatial inventory requires verified location data, such as:

-   Facility or landfill name.
-   Facility type and operational status.
-   Latitude and longitude.
-   Municipality and province.
-   Address or geographic description.
-   Facility operator or responsible authority.
-   Data source and verification date.
-   Environmental or regulatory status, where available.

The weighing dataset also needs a reliable relationship between each
weighing event and its destination facility. Without this relationship,
it is not possible to infer where each load was ultimately disposed of.

### Recommended geospatial data model

A future implementation could introduce:

**`DIM_LOCATION`** - `LOCATION_ID` - `LOCATION_NAME` - `LOCATION_TYPE` -
`MUNICIPALITY` - `PROVINCE` - `LATITUDE` - `LONGITUDE` - `GEOMETRY` -
`SOURCE_REFERENCE` - `VERIFICATION_DATE`

**`DIM_LANDFILL`** - `LANDFILL_ID` - `LANDFILL_NAME` - `LANDFILL_TYPE` -
`OPERATIONAL_STATUS` - `LOCATION_ID` - `OPERATOR` - `VALID_FROM` -
`VALID_TO`

**`FACT_WASTE_WEIGHT`** - `WEIGHT_EVENT_ID` - `DATE_KEY` -
`LOCATION_ID` - `LANDFILL_ID`, when verified - `COLLECTOR_ID`, when
available - `WASTE_TYPE_ID`, when available - `WEIGHT_TONS` -
`SOURCE_FILE` - `DATA_QUALITY_STATUS`

A map should only display facilities whose location and status are
supported by a traceable source.

------------------------------------------------------------------------

## 10. Recommended Target Data Architecture

The current notebook-oriented workflow can be evolved into a
maintainable data pipeline.

``` text
SOURCE SYSTEMS
  |-- Excel workbooks
  |-- CSV files
  |-- PDF documents
  |-- Scanned images
  |-- Municipal / GIS datasets
          |
          v
RAW LAYER
  |-- Preserve original files and values
  |-- Record ingestion metadata
  |-- Retain source lineage
          |
          v
STAGING LAYER
  |-- Standardize column names and types
  |-- Parse dates and numeric fields
  |-- Validate records
  |-- Identify duplicates and missing values
  |-- Apply documented business rules
          |
          v
ANALYTICAL / DATA WAREHOUSE LAYER
  |-- DIM_DATE
  |-- DIM_LOCATION
  |-- DIM_LANDFILL
  |-- DIM_COLLECTOR
  |-- DIM_WASTE_TYPE
  |-- FACT_WASTE_WEIGHT
  |-- FACT_COLLECTION
          |
          v
CONSUMPTION
  |-- Power BI dashboards
  |-- GIS maps
  |-- Statistical analysis
  |-- Machine learning
```

### Suggested technology stack

  -----------------------------------------------------------------------
  Layer / capability                  Suggested technology
  ----------------------------------- -----------------------------------
  Data ingestion                      Python, Pandas

  File and table storage              Microsoft Fabric Lakehouse or
                                      PostgreSQL

  Transformations                     Python or Spark; dbt where
                                      supported by the target platform

  Data quality                        Pandera, Great Expectations, or
                                      custom validation tests

  Geospatial storage                  PostgreSQL with PostGIS

  Spatial processing                  GeoPandas

  Visualization                       Power BI, Plotly, GeoPandas

  Machine learning                    Scikit-learn

  Version control                     Git and GitHub
  -----------------------------------------------------------------------

This is a proposed target architecture, not a description of
infrastructure already implemented in the repository.

------------------------------------------------------------------------

## 11. Potential Analytical Use Cases

### 11.1 Operational monitoring

-   Daily and monthly recorded tonnage.
-   Collection volume by operator or entity, if the source supports it.
-   Weekday and weekend patterns.
-   Changes in recorded collection activity.
-   Identification of unusually high or low observations.

### 11.2 Geographic analysis

Once verified coordinates and destination relationships are available:

-   Map of authorized disposal facilities.
-   Distribution of facilities by municipality.
-   Distance between collection zones and disposal facilities.
-   Geographic service coverage.
-   Identification of areas requiring further investigation.

### 11.3 Forecasting

With a sufficiently long, consistent, and representative time series:

-   Daily or weekly waste-volume forecasting.
-   Seasonal pattern analysis.
-   Collection-demand estimation.
-   Detection of unusual operational changes.

The currently documented 362-record dataset and incomplete temporal
coverage may be insufficient for reliable forecasting. More complete
historical data and a careful validation strategy are recommended before
training predictive models.

### 11.4 Public-sector performance indicators

Possible indicators include:

-   Total recorded tons by reporting period.
-   Average tons per observed collection day.
-   Percentage of days with complete records.
-   Number of records failing validation.
-   Share of records with a verified destination.
-   Collection volume by operator, where supported by source data.

Every KPI should define its numerator, denominator, reporting period,
and coverage limitations.

------------------------------------------------------------------------

## 12. Technical Risks and Recommended Improvements

  -----------------------------------------------------------------------
  Finding / risk    Potential impact  Recommended       Priority
                                      action            
  ----------------- ----------------- ----------------- -----------------
  CSV ingestion may Records may be    Remove the limit  Critical
  use a 1,000-row   omitted           or make sampling  
  limit                               explicit          

  Incomplete        Misleading        Build a coverage  Critical
  monthly coverage  time-series       calendar          
                    comparisons                         

  No verified       Cannot reliably   Obtain            Critical
  geospatial        map disposal      authoritative     
  inventory in the  facilities        coordinates and   
  weighing dataset                    facility metadata 

  Null values may   Biased totals and Preserve nulls    High
  be converted to   averages          and document      
  zero                                imputation rules  

  Outliers may be   Real events may   Retain raw values High
  capped without    be distorted      and flag adjusted 
  operational                         values            
  review                                                

  PDF/OCR           Incorrect weights Validate          High
  extraction can    or dates          extracted values  
  introduce errors                    against source    
                                      documents         

  Hard-coded file   Workflow may fail Use configuration Medium
  paths             outside the       and relative      
                    original          paths             
                    environment                         

  Limited automated Regressions may   Add schema,       Medium
  testing           go unnoticed      quality, and      
                                      transformation    
                                      tests             

  Unclear source    Difficult to      Capture file,     High
  lineage           audit results     sheet, page, and  
                                      ingestion         
                                      timestamp         

  Limited data      Business meaning  Document each     Medium
  dictionary        may be            field and formula 
                    misinterpreted                      
  -----------------------------------------------------------------------

------------------------------------------------------------------------

## 13. Recommended Development Roadmap

### Phase 1 --- Reproducible ingestion

-   Inventory all source files.
-   Document schemas and source provenance.
-   Remove unintended row limits.
-   Standardize file reading and error handling.
-   Produce ingestion logs and row-count reconciliation.

### Phase 2 --- Data quality and standardization

-   Define business keys.
-   Validate date and numeric fields.
-   Separate missing, zero, and no-activity conditions.
-   Preserve raw values.
-   Document outlier rules.
-   Add automated tests.

### Phase 3 --- Analytical model

-   Define a data dictionary.
-   Build a calendar dimension.
-   Build location, collector, and waste-type dimensions where source
    data supports them.
-   Define the waste-weight fact table.
-   Reconcile analytical totals against source files.

### Phase 4 --- Geospatial enrichment

-   Obtain authoritative landfill and transfer-station data.
-   Validate coordinates and facility status.
-   Link weighing events to destinations only when supported by
    evidence.
-   Store geographic data in PostGIS or another suitable spatial
    platform.
-   Build a map with source attribution and verification dates.

### Phase 5 --- BI and advanced analytics

-   Create operational dashboards.
-   Add data-coverage and quality indicators.
-   Evaluate forecasting feasibility.
-   Document model assumptions and limitations.
-   Publish reproducible analytical outputs.

------------------------------------------------------------------------

## 14. Suggested Repository Improvements

A more maintainable structure could look like this:

``` text
El-mapa-incompleto-de-los-vertederos/
|
|-- data/
|   |-- raw/
|   |   |-- csv/
|   |   |-- excel/
|   |   |-- pdf/
|   |   |-- images/
|   |
|   |-- processed/
|   |-- curated/
|
|-- notebooks/
|   |-- 01_source_inventory.ipynb
|   |-- 02_data_extraction.ipynb
|   |-- 03_data_consolidation.ipynb
|   |-- 04_data_quality_assessment.ipynb
|   |-- 05_exploratory_analysis.ipynb
|   |-- 06_geospatial_analysis.ipynb
|
|-- src/
|   |-- ingestion/
|   |-- transformations/
|   |-- validation/
|   |-- geospatial/
|
|-- tests/
|   |-- test_schema.py
|   |-- test_dates.py
|   |-- test_duplicates.py
|   |-- test_business_rules.py
|
|-- docs/
|   |-- data_dictionary.md
|   |-- methodology.md
|   |-- architecture.md
|   |-- data_sources.md
|
|-- reports/
|
|-- requirements.txt
|-- .gitignore
|-- README.md
```

This is a suggested future structure. It does not imply that these
directories or tests currently exist.

------------------------------------------------------------------------

## 15. Reproducibility and Execution

The repository contains Jupyter notebooks, but a complete execution
guide should be added with:

-   Supported Python version.
-   Dependency installation instructions.
-   Input-file locations.
-   Expected output locations.
-   Notebook execution order.
-   Environment variables or configuration files, if required.
-   Expected row counts and validation results.
-   Known limitations.

A starter environment can be created with:

``` bash
python -m venv .venv

# Linux / macOS
source .venv/bin/activate

# Windows PowerShell
# .venv\Scripts\Activate.ps1

pip install pandas numpy matplotlib plotly openpyxl jupyter
```

Additional packages for PDF extraction and OCR should be installed only
when the corresponding notebook cells require them. Some tools, such as
OCR engines, may also require operating-system dependencies.

The notebook execution order should be confirmed from the actual file
dependencies before it is documented as definitive.

------------------------------------------------------------------------

## 16. Final Assessment

The repository establishes a useful foundation for analyzing municipal
waste collection and weighing information. Its strongest contribution is
the consolidation of heterogeneous source material and the initial
assessment of data quality.

Its main limitation is the gap between the repository's geospatial
framing and the evidence available in the weighing records. A reliable
landfill map requires a separately validated geographic inventory and a
traceable relationship between collection events and disposal
destinations.

The most important next steps are:

1.  Make ingestion complete and reproducible.
2.  Establish temporal coverage and data-quality controls.
3.  Preserve raw values and document every adjustment.
4.  Build a documented analytical data model.
5.  Add verified geospatial data.
6.  Develop dashboards and predictive analysis only after the underlying
    data is sufficiently complete.

**Overall conclusion:** This is a promising academic data-mining project
with a clear path toward a broader environmental data-intelligence
solution. Its evolution should prioritize data traceability, geographic
validation, and reproducible engineering over adding visualizations
before the source data is reliable.

------------------------------------------------------------------------

## 17. References

-   **GitHub repository:**
    [El-mapa-incompleto-de-los-vertederos](https://github.com/michaelventura01/El-mapa-incompleto-de-los-vertederos)
-   **Source notebook:**
    [`RETO02_El_mapa_incompleto_de_los_vertederos.ipynb`](https://github.com/michaelventura01/El-mapa-incompleto-de-los-vertederos/blob/main/RETO02_El_mapa_incompleto_de_los_vertederos.ipynb)
-   **Analysis notebook:**
    [`RETO02_Mapa_Vertederos.ipynb`](https://github.com/michaelventura01/El-mapa-incompleto-de-los-vertederos/blob/main/RETO02_Mapa_Vertederos.ipynb)
-   **Excel source:**
    [`recoleccion_residuos.xlsx`](https://github.com/michaelventura01/El-mapa-incompleto-de-los-vertederos/blob/main/recoleccion_residuos.xlsx)
-   **Consolidated dataset:**
    [`desechos_csv_unificado.csv`](https://github.com/michaelventura01/El-mapa-incompleto-de-los-vertederos/blob/main/desechos_csv_unificado.csv)
-   **Cleaned dataset:**
    [`residuos_limpio.csv`](https://github.com/michaelventura01/El-mapa-incompleto-de-los-vertederos/blob/main/residuos_limpio.csv)
-   **Academic challenge description:**
    [`Explicación del Reto 5 - Pesaje de Residuos Santiago y Moca - Grupo Marrón - Data Mining - MACDIA - UASD.pdf`](https://github.com/michaelventura01/El-mapa-incompleto-de-los-vertederos/blob/main/Explicaci%C3%B3n%20del%20Reto%205%20-%20Pesaje%20de%20Residuos%20Santiago%20y%20Moca%20-%20Grupo%20Marr%C3%B3n%20-%20Data%20Mining%20-%20MACDIA%20-%20UASD.pdf)

------------------------------------------------------------------------

*Documentation note: This document combines repository-level inspection
with the analysis findings previously reported from the notebooks.
Metrics and implementation details should be revalidated by executing
the current notebooks against the current source files before being used
as formal or operational evidence.*
