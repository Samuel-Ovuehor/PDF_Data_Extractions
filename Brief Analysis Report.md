# Brief Analysis Report

## Overview of the Data
The dataset contains several pages from anonymised planning decision notices. Each page was originally a scanned document and generally represents a different section of a planning decision notice. The goal of this analysis was to identify the type of page and extract important information such as:

- **Application numbers**
- **Applicant names**

From the sample results, four main types of pages were identified:

- Planning charges
- Application for planning permission notice of approval
- Grant of conditional planning permission
- Notice of approval of details

---

## Findings from the Results
The extracted results demonstrate that useful information can be identified from the pages.

- **Application Numbers:**  
  Application numbers were successfully found in most pages. Some pages include more than one application number, indicating multiple related planning cases. For example:
  - Page 1: three application numbers
  - Page 4: two application numbers
  - Page 2: one application number
  - Page 3: no visible application number

- **Applicant Names:**  
  Applicant names were extracted in most cases. Examples include:
  - Page 1: `Mr. & Mrs. J.M Doe` (joint applicants)
  - Page 2: `Mr M Dale` (typical planning document format)
  - Page 4: `Mrs AM Stephens` (names with initials)
  - Page 3: `"As named on the reverse"` (applicant name appears on another page)

These results indicate that planning decision notices generally follow a **consistent structure**.

---

## Limitations
- **Scanned Document Quality:**  
  Older documents may contain faded text, marks, or unusual formatting, which can lead to OCR mistakes affecting extracted information.
  
- **Page Type Classification:**  
  Page type is determined using specific keyword phrases. Documents with different wording or formatting may not be correctly categorized.
  
- **Applicant Name Extraction:**  
  Extraction works best when a person’s title (e.g., Mr, Mrs) precedes the name. Names without titles or organisational names may not be detected accurately.
  
- **Sample Size:**  
  The dataset is small, limiting the ability to fully evaluate accuracy on larger document sets.

---

## Alternate Methods / Future Improvements
- **Advanced Text Analysis:**  
  Use more sophisticated NLP techniques to understand the content of each page, instead of relying solely on specific phrases.

- **Improved Name Recognition:**  
  Incorporate tools that better detect individual and organisational names for more accurate extraction.

- **Layout-Aware Processing:**  
  Consider document layout (text positions, columns, forms) to improve reliability, especially for structured planning notices.
