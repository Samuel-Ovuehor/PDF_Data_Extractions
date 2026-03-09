# Brief Analysis Report

## Overview of the Data
The dataset contains four pages from anonymised planning decision notices. Each page was originally a scanned document and generally represents a different section of a planning decision notice. The goal was to identify the type of page and extract important information such as **Application numbers** and **Applicant names**.

From the sample results, four main types of pages were identified:

- Planning charges
- Application for planning permission notice of approval
- Grant of conditional planning permission
- Notice of approval of details

---

## Findings from the Results
The extracted results show that useful information can be identified from the pages of the files. Application numbers were successfully found on most pages. Some pages include more than one application number, which suggests that the document may refer to multiple related planning cases. For example, File Number 1 contains two application numbers, while File Number 4 also contains two. File Number 2 contains only one application number, and File Number 3 does not contain any visible application number.


- **Applicant Names** were also extracted in most cases. For example:
•	File number 1 identifies Mr. & Mrs. J.M Doe, showing joint applicants.
•	File number 2 extracts Mr M Dale, which might be a typical format used in planning documents.
•	File number 4 extracts Mrs AM Stephens, showing names with initials.
•	File number 3 contains the phrase “As named on the reverse”, which means the applicant name is likely written on another page rather than the current one.

These results show that planning decision notices usually follow a similar structure.

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
