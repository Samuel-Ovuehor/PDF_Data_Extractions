**System Overview**
The pipeline uses a "consensus" model between two extraction strategies to maximize accuracy. While Engine A relies on strict pattern matching (Regex), Engine B uses positional logic to capture edge cases where patterns may fail due to Optical Character Recognition (OCR) noise.

#1. Environment Setup
System Dependencies
The code requires the Tesseract OCR engine and Poppler (for PDF rendering) to be installed on the host operating system:
•	Tesseract-OCR: The primary engine for Optical Character Recognition.
•	Poppler-utils: Required by pdf2image to convert PDF pages into image objects.

Python Libraries
Pytesseract: Python wrapper for Tesseract OCR.
pdf2image: Converts PDF files into PIL Image objects.
Spacy: Natural Language Processing for entity filtering.
Pandas: Data manipulation and CSV export.
Re: Regular expression engine for pattern matching.


#2. Implementation Logic
A. Document Classification (NLPClassifier)
The classifier identifies the document type by scanning the OCR output for specific legal phrases.
•	Mechanism: Case-insensitive keyword matching.
•	Categories: * Grant of conditional planning permission
o	Notice of approval of details
o	Application for planning permission
o	Planning charges

B. Extraction Engine A (Regex-Driven)
This engine is optimized for high-precision extraction of structured strings.
•	Application Numbers: Uses a non-capturing group regex to find patterns like 2024/0123 or DC/22/500.
•	Applicant Names: Searches for honorifics (Mr, Mrs, Dr) and uses a "sliding window" to check the three lines following the "Applicant" keyword.

C. Extraction Engine B (Positional-Driven)
Acts as a fallback for Engine A.
•	Logic: It looks for the "Applicant" label and extracts text either immediately following a colon (:) or on the subsequent line, regardless of whether a title (Mr/Mrs) is present.
•	Validation: Implements a "Blacklist" (e.g., Council, London, Road) to ensure address lines aren't misidentified as people.

**3. Execution Workflow**
1.	Conversion: The PDF is converted to images at 300 DPI to ensure high OCR legibility.
2.	OCR Processing: Tesseract is configured with --psm 6 (Assume a single uniform block of text) to maintain the layout of form-based documents.
3.	Parallel Execution: * run_pipeline_A extracts category, application numbers, and names.
o	run_pipeline_B focuses specifically on capturing names via positional logic.
4.	Data Merging: The results are merged using a Left Join on the Page Number.
5.	Coalescing: If Engine A returns "N/A" or "None" for an applicant, the system automatically fills that cell with the result from Engine B.

4. Usage
To run the code, ensure your PDF is uploaded to the specified path and execute the main block:
Python
# Update this path to your local file
FILE_PATH = "your_document.pdf"

# Run the unified process
df_A = run_pipeline_A(FILE_PATH)
df_B = run_pipeline_B(FILE_PATH)
final_df = merge_results(df_A, df_B)

# View and Save
print(final_df)
final_df.to_csv("extracted_data.csv")
