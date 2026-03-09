## System Overview
This pipeline uses a **"consensus" model** between two extraction strategies to maximize accuracy.  
- **Engine A**: Regex-driven, high-precision pattern matching.  
- **Engine B**: Positional logic fallback, designed to capture edge cases caused by Optical Character Recognition (OCR) noise.  

The system merges outputs from both engines to provide the most accurate applicant and application number extraction.

---

## 1. Environment Setup

### System Dependencies
The following software must be installed on the host system:

- **Tesseract-OCR**: Primary OCR engine for extracting text from images.  
- **Poppler-utils**: Required by `pdf2image` to convert PDF pages into image objects.

### Python Libraries
Install via pip:

- **pytesseract**: Python wrapper for Tesseract OCR.  
- **pdf2image**: Converts PDF files into PIL Image objects.  
- **spacy**: NLP library for entity extraction and filtering.  
- **pandas**: Data manipulation and CSV export.  
- **re**: Regular expressions for pattern matching.

---

## 2. Implementation Logic

### A. Document Classification (NLPClassifier)
The classifier identifies the document type from OCR text using keyword scanning.

- **Mechanism**: Case-insensitive keyword matching.  
- **Supported Categories**:
  - Grant of conditional planning permission
  - Notice of approval of details
  - Application for planning permission
  - Planning charges

---

### B. Extraction Engine A (Regex-Driven)
Optimized for **high-precision extraction**.

- **Application Numbers**: Uses regex with non-capturing groups to detect patterns like `2024/0123` or `DC/22/500`.  
- **Applicant Names**: Searches for honorifics (`Mr`, `Mrs`, `Dr`) and checks the **three lines following the "Applicant" keyword** to locate valid names.

---

### C. Extraction Engine B (Positional-Driven)
Fallback for Engine A, targeting edge cases.

- **Logic**: Looks for the "Applicant" label and extracts text either:
  - Immediately following a colon (`:`)  
  - On the subsequent line, regardless of titles
- **Validation**: Uses a **blacklist** (e.g., Council, London, Road) to avoid capturing addresses or organization names as people.

---

## 3. Execution Workflow

1. **PDF Conversion**: Convert PDF pages to images for optimal OCR quality.  
2. **OCR Processing**: Tesseract runs (single uniform text block) to preserve layout of forms.  
3. **Parallel Extraction**:
   - `run_pipeline_A` → Extracts category, application numbers, and applicant names.  
   - `run_pipeline_B` → Captures applicant names using positional logic as a fallback.  
4. **Data Merging**: Merge both pipelines on **File Number** (Left Join).  
5. **Coalescing**: If Engine A returns `"N/A"` or `"None"` for an applicant, replace it with Engine B's result.

---

## 4. Usage

### Step 1: Set File Path
```python
# Update this path to your local PDF
FILE_PATH = "your_document.pdf"
