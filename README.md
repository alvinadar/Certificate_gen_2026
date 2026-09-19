
# Cert Generator

This project aims to automate the generation of certificates from an Excel dataset. It involves data analysis for cleaning and formatting, enhancing Python concepts, and exploring third-party libraries, specifically `reportlab`, for PDF generation.

## Project Goals:
1.  **Data Analysis**: Clean and prepare the input data by handling missing values and formatting dates and text consistently.
2.  **Enhance Python Concepts**: Apply various Python programming concepts, especially with Pandas for data manipulation.
3.  **Explore 3rd Party Libraries**: Utilize the `reportlab` library to programmatically create and customize PDF certificates.

## Setup and Installation:
Before running the notebook, ensure you have the necessary libraries installed. `reportlab` is an external library and needs to be installed separately.

```bash
pip install reportlab pandas numpy
```

## Project Steps:

### 1. Download & Import Packages
The project starts by importing essential libraries:
-   `numpy` and `pandas` for data manipulation.
-   `reportlab` components (`canvas`, `pagesizes`, `units`, `pdfmetrics`, `ttfonts`) for PDF generation.

### 2. Reading and Exploring the Excel File
An Excel file (`dataset.xlsx`) is read into a pandas DataFrame. Initial exploration (`df.head()`, `df.info()`) helps to identify data quality issues like missing values and inconsistent formatting.

### 3. Data Cleaning (Data Analysis)
This crucial step addresses data inconsistencies:
-   **Missing Values**: Rows with any missing values are dropped using `df.dropna()`.
-   **Date Formatting**: The 'Date' column, initially in `datetime64[ns]` format, is converted to `dd/mm/yyyy` string format and stored in a new 'FormattedDate' column. The original 'Date' column is then dropped.
-   **Text Formatting**: 'Course' and 'CourseLevel' columns are standardized to have their first letter capitalized and the rest lowercase using `.str.capitalize()` to ensure consistency.

### 4. Registering Fonts
Custom fonts (`Lora-Bold.ttf`, `Lora-Regular.ttf`) are registered using `reportlab.pdfbase.pdfmetrics.registerFont()` to be used in the generated certificates. The font files are expected to be in a specified `fonts` directory.

### 5. Creating Certificate Logic Function
A Python function `certificate_generator(name, courseName, courseLevel, date)` is defined. This function takes the cleaned data for each individual and:
-   Creates a PDF file with a unique name based on the participant's details.
-   Draws a certificate template image onto the PDF canvas.
-   Places the participant's name, course details, date, and a unique certificate ID (generated using a timestamp) at specific positions on the certificate, using the registered fonts.
-   Saves the generated PDF.

### 6. Generating Certificates
The `certificate_generator` function is then iterated over each row of the cleaned DataFrame using `df.iterrows()`, generating a personalized certificate for every valid entry. A confirmation message is printed once all certificates are generated.

## Usage:
1.  Place your `dataset.xlsx` file, certificate template (`certificate_template.jpg`), and font files (`Lora-Bold.ttf`, `Lora-Regular.ttf`) in the specified Google Drive paths.
2.  Run through the notebook cells sequentially.
3.  Generated certificates will be saved in the `/content/drive/MyDrive/Certificate Generator/certificates/` directory.
```
