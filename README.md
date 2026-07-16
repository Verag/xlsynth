# xlsynth

> Generate realistic, synthetic and intentionally imperfect Excel workbooks for testing, benchmarking and software validation.

`xlsynth` is an R package for generating synthetic Microsoft Excel workbooks.

Unlike traditional data generators, `xlsynth` focuses on the workbook itself rather than only the data. It can create realistic spreadsheets, simulate exports from business systems, and intentionally introduce common formatting and data quality issues found in real-world Excel files.

The package is designed for developers, data engineers, QA teams and researchers who need representative Excel files to test software.

---

## Why?

Most software is tested using clean, perfectly structured spreadsheets.

Real Excel files are rarely like that.

They often contain:

* hidden worksheets
* merged cells
* blank rows
* inconsistent date formats
* duplicated headers
* mixed data types
* formulas
* comments
* hyperlinks
* protected sheets
* inconsistent styling

Testing against ideal files gives a false sense of robustness.

`xlsynth` allows you to generate reproducible workbooks that better represent real-world conditions.

---

## MVP Goals

The first release focuses on four core capabilities.

### 1. Schema Generator

Describe the workbook instead of manually building it.

```r
schema <- workbook_schema(
  sheets = list(
    sheet(
      name = "Sales",
      rows = 5000,
      columns = list(
        date(),
        customer(),
        product(),
        currency()
      )
    )
  )
)
```

---

### 2. Workbook Generator

Generate a complete Excel workbook from a schema.

```r
generate_excel(
    schema,
    output = "sales.xlsx"
)
```

---

### 3. Chaos Engine

Introduce controlled imperfections into an existing workbook.

```r
chaos_excel(
    "sales.xlsx",
    level = 2,
    seed = 123
)
```

Examples include:

* random blank rows
* mixed date formats
* renamed worksheets
* hidden worksheets
* duplicated rows
* inconsistent number formats
* merged cells
* missing values

---

### 4. Test Suite Generator

Generate an entire collection of workbooks covering common scenarios.

```r
generate_excel_test_suite(
    output_dir = "tests/"
)
```

Example output:

```
tests/

minimal.xlsx

protected.xlsx

hidden_sheet.xlsx

merged_cells.xlsx

unicode.xlsx

mixed_dates.xlsx

comments.xlsx

hyperlinks.xlsx

large.xlsx

stress.xlsx
```

---

# Design Principles

* Reproducible
* Declarative
* Modular
* Extensible
* Realistic
* Domain agnostic

---

# Example

Generate a realistic workbook.

```r
schema <- workbook_schema(

    sheets = list(

        sheet(

            name = "Employees",

            rows = 1000,

            columns = list(

                employee_id(),

                person_name(),

                department(),

                hire_date(),

                salary()

            )

        )

    )

)

generate_excel(
    schema,
    output = "employees.xlsx"
)
```

---

# Example with Chaos

```r
chaos_excel(

    "employees.xlsx",

    actions = c(

        "blank_rows",

        "mixed_dates",

        "rename_sheet"

    ),

    seed = 42

)
```

---

# Target Users

* R package developers
* Data engineers
* QA engineers
* ETL developers
* Business Intelligence teams
* Researchers
* Software developers working with Excel

---

# Roadmap

## MVP

* Workbook schema
* Synthetic data generation
* Excel workbook generation
* Chaos Engine
* Test suite generator

## v0.2

* Industry templates
* Dashboard generation
* Conditional formatting
* Named ranges
* Charts
* Images

## v0.3

* SAP export simulation
* ERP exports
* Google Sheets profiles
* LibreOffice profiles

## v0.4

* Workbook fuzzing
* Property-based workbook generation
* Performance benchmarking
* Extreme Excel limit testing

---

# Motivation

`xlsynth` exists because testing software with perfect spreadsheets is easy.

Testing it with spreadsheets that resemble those created by real people is much harder.

This package aims to close that gap.

---

# Status

🚧 Early development (MVP)

