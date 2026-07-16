# xlsynth

> Generate realistic and reproducible Excel workbooks for automated testing.

`xlsynth` is an R package for generating synthetic Microsoft Excel workbooks.

It was originally developed to support testing of **xlversion**, an R package for comparing and fingerprinting Excel workbooks. During development it became clear that creating representative test files manually was slow, repetitive and difficult to automate.

`xlsynth` provides a declarative way to generate realistic Excel workbooks that can be used to develop, test and benchmark software that reads or processes `.xlsx` files.

---

## Why?

Most software that processes Excel files is tested using clean, perfectly structured spreadsheets.

Real-world workbooks are rarely like that.

They often contain:

- blank rows
- hidden worksheets
- merged cells
- inconsistent date formats
- duplicated values
- mixed data types
- missing values
- inconsistent formatting

Testing only against ideal workbooks gives a false sense of robustness.

`xlsynth` helps developers generate reproducible workbooks that better represent the spreadsheets encountered in production.

---

# Features

- Declarative workbook schema
- Synthetic but realistic datasets
- Multi-sheet workbook generation
- Reproducible output using random seeds
- Optional workbook mutations for testing edge cases
- Designed for automated testing and CI pipelines

---

# MVP

The first release focuses on three core capabilities.

## 1. Workbook Schema

Describe a workbook instead of manually creating it.

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

## 2. Workbook Generation

Generate a complete Excel workbook from the schema.

```r
generate_excel(

    schema,

    output = "sales.xlsx"

)
```

---

## 3. Workbook Mutations

Introduce controlled imperfections into an existing workbook.

```r
mutate_workbook(

    "sales.xlsx",

    actions = c(

        "blank_rows",

        "mixed_dates",

        "missing_values"

    ),

    seed = 42

)
```

Available mutations include:

- blank rows
- duplicated rows
- missing values
- mixed date formats
- merged cells
- hidden worksheets
- renamed worksheets
- inconsistent number formats

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

# Relationship with xlversion

`xlsynth` and **xlversion** are complementary.

- **xlsynth** generates realistic Excel workbooks for testing.
- **xlversion** analyses, fingerprints and compares those workbooks.

Together they provide a reproducible workflow for developing and testing software that processes Excel files.

---

# Target Users

- Data engineers
- ETL developers
- QA engineers
- Software developers
- R package developers
- Anyone building software that reads Excel workbooks

---

# Design Principles

- Reproducible
- Declarative
- Modular
- Extensible

---

# Roadmap

## v0.1

- Workbook schema
- Workbook generation
- Basic synthetic data generators
- Workbook mutations

## Future

Potential future extensions include:

- Industry-specific templates
- Additional mutation strategies
- Large workbook generation
- Performance benchmarking
- Workbook fuzz testing

---

# Motivation

`xlsynth` started as an internal tool while developing **xlversion**.

Creating realistic Excel files by hand quickly became one of the biggest bottlenecks when writing automated tests.

Rather than maintaining dozens of manually crafted spreadsheets, `xlsynth` generates reproducible workbooks on demand, making automated testing simpler and more representative of real-world scenarios.

---

# Status

🚧 Early development (MVP)

Contributions, suggestions and feedback are welcome.

