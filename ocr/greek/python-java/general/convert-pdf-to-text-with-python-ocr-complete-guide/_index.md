---
category: general
date: 2026-07-05
description: Μετατρέψτε το PDF σε κείμενο χρησιμοποιώντας Python OCR. Μάθετε πώς να
  εξάγετε κείμενο από PDF, να εκτελείτε ομαδική επεξεργασία OCR και να φορτώνετε PDF
  για OCR σε λίγα εύκολα βήματα.
draft: false
keywords:
- convert pdf to text
- extract text from pdf
- batch ocr processing
- load pdf for ocr
- recognize scanned pdf
language: el
og_description: Μετατρέψτε το PDF σε κείμενο γρήγορα. Αυτό το σεμινάριο δείχνει πώς
  να εξάγετε κείμενο από PDF, να εκτελέσετε επεξεργασία OCR σε παρτίδες και να αναγνωρίσετε
  σαρωμένα αρχεία PDF χρησιμοποιώντας Python.
og_title: Μετατροπή PDF σε Κείμενο με Python OCR – Οδηγός Βήμα‑προς‑Βήμα
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Convert PDF to text using Python OCR. Learn how to extract text from
    PDF, perform batch OCR processing, and load PDF for OCR in a few easy steps.
  headline: Convert PDF to Text with Python OCR – Complete Guide
  type: TechArticle
- description: Convert PDF to text using Python OCR. Learn how to extract text from
    PDF, perform batch OCR processing, and load PDF for OCR in a few easy steps.
  name: Convert PDF to Text with Python OCR – Complete Guide
  steps:
  - name: '**Chunked Loading** – Some libraries let you load a range of pages:'
    text: '**Chunked Loading** – Some libraries let you load a range of pages:'
  - name: '**Streaming to Disk** – Write each page’s text directly to a file instead
      of keeping the entire list in memory.'
    text: '**Streaming to Disk** – Write each page’s text directly to a file instead
      of keeping the entire list in memory.'
  - name: '**Sanity Check** – Open a generated `.txt` file and verify that the first
      few lines match the original document’s header.'
    text: '**Sanity Check** – Open a generated `.txt` file and verify that the first
      few lines match the original document’s header.'
  - name: '**Performance Test** – Time the script on a 100‑page PDF using the `time`
      command. If it takes longer than expected, consider enabling the library’s multi‑threading
      flag (often `engine.set_threads(4)`).'
    text: '**Performance Test** – Time the script on a 100‑page PDF using the `time`
      command. If it takes longer than expected, consider enabling the library’s multi‑threading
      flag (often `engine.set_threads(4)`).'
  - name: '**Quality Assurance** – Compare the OCR output against a manually typed
      excerpt using a diff tool. Aim for >95 % character accuracy for clean scans.'
    text: '**Quality Assurance** – Compare the OCR output against a manually typed
      excerpt using a diff tool. Aim for >95 % character accuracy for clean scans.'
  type: HowTo
tags:
- OCR
- Python
- PDF
title: Μετατροπή PDF σε Κείμενο με Python OCR – Πλήρης Οδηγός
url: /el/python-java/general/convert-pdf-to-text-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή PDF σε Κείμενο με Python OCR – Πλήρης Οδηγός

Έχετε ποτέ αναρωτηθεί πώς να **convert PDF to text** χωρίς κόπο; Ίσως έχετε ένα σωρό σαρωμένων συμβάσεων, τιμολογίων ή ερευνητικών εργασιών και χρειάζεστε την απλή έκδοση κειμένου για ευρετηρίαση ή ανάλυση. Τα καλά νέα είναι ότι με λίγες γραμμές Python μπορείτε να κάνετε τη σκληρή δουλειά.

Σε αυτό το tutorial θα περάσουμε από μια πρακτική λύση που όχι μόνο **convert pdf to text**, αλλά επίσης σας δείχνει πώς να **extract text from pdf**, να ρυθμίσετε **batch OCR processing**, και να **load pdf for OCR** σωστά. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση script που μπορεί να **recognize scanned pdf** σε μία κλήση.

## What You’ll Learn

- Εγκατάσταση και διαμόρφωση μιας βιβλιοθήκης Python OCR (θα χρησιμοποιήσουμε ένα γενικό πακέτο `ocr` για παράδειγμα).  
- Φόρτωση ενός πολυ‑σελίδων PDF και παροχή του στην μηχανή OCR.  
- Επανάληψη στα αποτελέσματα για εκτύπωση ή αποθήκευση του εξαγόμενου κειμένου.  
- Διαχείριση κοινών περιπτώσεων όπως μεγάλα αρχεία, κρυπτογραφημένα PDF και έγγραφα πολλαπλών γλωσσών.  

Χωρίς βαριά εργαλεία GUI, χωρίς χειροκίνητη αντιγραφή—απλώς καθαρός κώδικας που μπορείτε να ενσωματώσετε σε μια CI pipeline ή σε μια επιτραπέζια εφαρμογή.

![Μετατροπή PDF σε Κείμενο χρησιμοποιώντας Python OCR](https://example.com/images/convert-pdf-to-text.png "Μετατροπή PDF σε Κείμενο χρησιμοποιώντας Python OCR")

## Prerequisites

Before we dive in, make sure you have:

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|-----------------------|
| Python 3.9+ | Σύγχρονη σύνταξη, type hints, και καλύτερη απόδοση. |
| `ocr` library (ή ένα wrapper γύρω από το Tesseract) | Παρέχει τις κλάσεις `OcrEngine`, `Language`, και `Image` που χρησιμοποιούνται στο παράδειγμα. |
| A multi‑page scanned PDF (e.g., `contract.pdf`) | Αυτή είναι η πηγή που θα **load pdf for OCR**. |
| Basic command‑line familiarity | Για την εγκατάσταση πακέτων και την εκτέλεση του script. |

Αν χρησιμοποιείτε το Tesseract στο παρασκήνιο, εγκαταστήστε το μέσω του διαχειριστή πακέτων του λειτουργικού σας (`apt-get install tesseract-ocr` σε Linux, `brew install tesseract` σε macOS). Στη συνέχεια προσθέστε το Python wrapper:

```bash
pip install ocr  # replace with the actual package name, e.g., pytesseract-wrapper
```

## Step 1: Create the OCR Engine and Set the Recognition Language

First, we need an OCR engine instance. Setting the language to English is a common default, but you can switch to other supported languages later.

```python
import ocr  # hypothetical import; replace with your actual OCR package

# Initialize the OCR engine
engine = ocr.OcrEngine()

# Choose the language for recognition – ENGLISH works for most contracts
engine.language = ocr.Language.ENGLISH
```

**Γιατί είναι σημαντικό:** Η μηχανή είναι ο εγκέφαλος που ερμηνεύει τα pixel δεδομένα. Ορίζοντας ρητά το `engine.language`, αποφεύγετε το κόστος ανίχνευσης γλώσσας σε κάθε σελίδα, κάτι που επιταχύνει σημαντικά το **batch OCR processing**.

## Step 2: Load the PDF Document for OCR

Now we bring the PDF into memory. The `ocr.Image.load` method can accept a file path and returns an object that the engine understands.

```python
# Path to your scanned PDF; adjust as needed
pdf_path = "YOUR_DIRECTORY/contract.pdf"

# Load the PDF – this step **load pdf for OCR**
pdf_document = ocr.Image.load(pdf_path)
```

**Συμβουλή:** Αν το PDF σας είναι προστατευμένο με κωδικό, οι περισσότερες βιβλιοθήκες επιτρέπουν να περάσετε ένα όρισμα `password`. Η διαχείριση του νωρίς αποτρέπει ένα ασαφές σφάλμα “cannot open file” αργότερα.

## Step 3: Run OCR on All Pages – Recognize Scanned PDF in One Call

Running OCR page‑by‑page can be slow, especially for large documents. The `recognize_multi_page` method performs **batch OCR processing** internally, using multiple threads when possible.

```python
# Execute OCR across every page; returns a list of OcrResult objects
page_results = engine.recognize_multi_page(pdf_document)  # List<OcrResult>
```

**Τι συμβαίνει στο παρασκήνιο;** Η μηχανή στέλνει κάθε σελίδα στην υποκείμενη μηχανή OCR (όπως το Tesseract), συλλέγει το κείμενο και το τυλίγει σε ένα `OcrResult`. Αυτή η προσέγγιση μειώνει το κόστος I/O και σας παρέχει έναν καθαρό τρόπο για **extract text from pdf** αργότερα.

## Step 4: Iterate Through Results and Output the Recognized Text

Finally, we loop over each `OcrResult` and print the text. You could also write each page to a separate `.txt` file or concatenate them into a single document.

```python
for page_number, result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(result.text)
    # Optional: save to a file
    # with open(f"page_{page_number}.txt", "w", encoding="utf-8") as f:
    #     f.write(result.text)
```

**Γιατί η χρήση του enumerate;** Η χρήση του `enumerate(..., start=1)` σας δίνει έναν αριθμό σελίδας που είναι ευανάγνωστος, χρήσιμο όταν χρειαστεί να αναφερθείτε σε συγκεκριμένο τμήμα του αρχικού PDF.

### Expected Output

Running the script against a 3‑page contract might produce:

```
--- Page 1 ---
THIS AGREEMENT is made on the 1st day of January 2024...
--- Page 2 ---
WHEREAS, the Parties desire to...
--- Page 3 ---
IN WITNESS WHEREOF, the Parties have executed...
```

Αν μια σελίδα δεν περιέχει αναγνωρίσιμο κείμενο, το αντίστοιχο `result.text` θα είναι μια κενή συμβολοσειρά—ιδανικό για εντοπισμό κενών ή μόνο‑εικόνας σελίδων.

## Handling Large PDFs and Memory Constraints

Processing a 500‑page PDF can exhaust RAM if you load everything at once. Here are two strategies:

1. **Chunked Loading** – Some libraries let you load a range of pages:

   ```python
   for start in range(0, total_pages, 50):  # process 50 pages at a time
       chunk = pdf_document.select_pages(start, start + 49)
       chunk_results = engine.recognize_multi_page(chunk)
       # handle chunk_results as before
   ```

2. **Streaming to Disk** – Write each page’s text directly to a file instead of keeping the entire list in memory.

Both techniques keep your **convert pdf to text** workflow scalable.

## Dealing with Errors and Edge Cases

- **Encrypted PDFs** – Pass the password to `Image.load`:

  ```python
  pdf_document = ocr.Image.load(pdf_path, password="mySecret")
  ```

- **Mixed Languages** – Switch language per page if you detect a different script:

  ```python
  if detect_spanish(result.text):
      engine.language = ocr.Language.SPANISH
  ```

- **Low‑Resolution Scans** – Pre‑process images with a library like `Pillow` to increase contrast before OCR. This can dramatically improve the quality of the **recognize scanned pdf** step.

## Full Script: Convert PDF to Text in One Run

Below is the complete, ready‑to‑execute script that ties everything together. Save it as `pdf_to_text.py` and run `python pdf_to_text.py`.

```python
#!/usr/bin/env python3
"""
convert_pdf_to_text.py

A self‑contained script that demonstrates how to convert PDF to text using
Python OCR. It covers loading the PDF, batch processing, and handling common
edge cases.
"""

import os
import ocr  # Replace with your actual OCR package

def convert_pdf_to_text(pdf_path: str, output_dir: str = "output"):
    """Convert a scanned PDF into plain‑text files, one per page."""
    if not os.path.isfile(pdf_path):
        raise FileNotFoundError(f"PDF not found: {pdf_path}")

    os.makedirs(output_dir, exist_ok=True)

    # Step 1 – create engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Step 2 – load PDF (supports password argument if needed)
    pdf_document = ocr.Image.load(pdf_path)

    # Step 3 – run batch OCR
    page_results = engine.recognize_multi_page(pdf_document)

    # Step 4 – write each page's text to a file
    for page_number, result in enumerate(page_results, start=1):
        page_text = result.text.strip()
        out_file = os.path.join(output_dir, f"page_{page_number}.txt")
        with open(out_file, "w", encoding="utf-8") as f:
            f.write(page_text)

        # Also echo to console for quick sanity check
        print(f"--- Page {page_number} ---")
        print(page_text[:200] + ("…" if len(page_text) > 200 else ""))

if __name__ == "__main__":
    # Example usage – adjust the path to your PDF file
    PDF_PATH = "YOUR_DIRECTORY/contract.pdf"
    convert_pdf_to_text(PDF_PATH)
```

**Running the script** will create an `output` folder containing `page_1.txt`, `page_2.txt`, etc., effectively **extract text from pdf** in a structured way.

## Testing the Solution

1. **Sanity Check** – Open a generated `.txt` file and verify that the first few lines match the original document’s header.  
2. **Performance Test** – Time the script on a 100‑page PDF using the `time` command. If it takes longer than expected, consider enabling the library’s multi‑threading flag (often `engine.set_threads(4)`).  
3. **Quality Assurance** – Compare the OCR output against a manually typed excerpt using a diff tool. Aim for >95 % character accuracy for clean scans.

## Next Steps and Related Topics

- **Improve Accuracy**: Experiment with `engine.dpi = 300` or apply image preprocessing (deskew, denoise) before OCR.  
- **Searchable PDFs**: Use a PDF library (like `PyPDF2` ή `pdfplumber`) to embed the extracted text back into the original PDF, making it searchable.  
- **Natural Language Processing**: Feed the extracted text into spaCy ή NLTK for entity extraction, sentiment analysis, or keyword tagging.  
- **Automation Pipelines**: Combine this script with `watchdog` to monitor a folder and automatically **convert pdf to text** whenever a new file appears.

Με την εξάσκηση αυτών των προτύπων, θα μπορείτε να

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Αναγνώριση Κειμένου PDF – Λειτουργίες OCR με Aspose.OCR για Java](/ocr/english/java/ocr-operations/)
- [Πώς να κάνετε OCR PDF σε .NET με Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Πώς να Εξάγετε Κείμενο από Αρχεία ZIP Χρησιμοποιώντας Aspose.OCR για .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}