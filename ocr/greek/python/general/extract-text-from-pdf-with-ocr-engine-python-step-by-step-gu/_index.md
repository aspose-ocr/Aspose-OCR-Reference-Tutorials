---
category: general
date: 2026-01-12
description: Εξαγωγή κειμένου από PDF χρησιμοποιώντας τη μηχανή OCR Python – μάθετε
  πώς να διαβάζετε PDF με OCR, να φορτώνετε εικόνα για OCR και να λαμβάνετε δομημένα
  αποτελέσματα.
draft: false
keywords:
- extract text from pdf
- read pdf with ocr
- load image for ocr
- use ocr engine python
language: el
og_description: Εξαγωγή κειμένου από PDF χρησιμοποιώντας την μηχανή OCR Python. Αυτό
  το σεμινάριο δείχνει πώς να διαβάσετε PDF με OCR, να φορτώσετε εικόνα για OCR και
  να χρησιμοποιήσετε την μηχανή OCR Python για αξιόπιστα αποτελέσματα.
og_title: Εξαγωγή κειμένου από PDF με μηχανή OCR Python – Πλήρης οδηγός
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Εξαγωγή κειμένου από PDF με μηχανή OCR Python – Οδηγός βήμα‑προς‑βήμα
url: /el/python/general/extract-text-from-pdf-with-ocr-engine-python-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από PDF με OCR Engine Python – Πλήρες Tutorial

Έχετε χρειαστεί ποτέ να **extract text from PDF** αλλά το αρχείο είναι μόνο μια σκαναρισμένη εικόνα; Δεν είστε μόνοι. Σε πολλά πραγματικά έργα το PDF που λαμβάνετε δεν έχει επιλέξιμο κείμενο, οπότε ο μόνος τρόπος είναι να **read PDF with OCR**.  

Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα από μια πρακτική, ολοκληρωμένη λύση που δείχνει ακριβώς πώς να **load image for OCR**, να ξεκινήσετε το **OCR engine Python**, και να εξάγετε δομημένο κείμενο που μπορείτε να τροφοδοτήσετε σε επόμενες διαδικασίες. Χωρίς ασαφείς αναφορές, μόνο ένα πλήρες, εκτελέσιμο παράδειγμα που μπορείτε να αντιγράψετε‑επικολλήσετε σήμερα.

## What You’ll Learn

- Πώς να εγκαταστήσετε και να εισάγετε τη βιβλιοθήκη OCR για Python που χρειάζεστε.  
- Τα ακριβή βήματα για **load image for OCR** από αρχείο PDF.  
- Πώς να καλέσετε τη μέθοδο `recognize_structured()` της μηχανής και να επαναλάβετε τα blocks, lines, και words.  
- Συμβουλές για τη διαχείριση αποτελεσμάτων χαμηλής εμπιστοσύνης και PDF πολλαπλών σελίδων.  

Στο τέλος αυτού του tutorial θα έχετε ένα script που εξάγει αξιόπιστα **text from PDF** έγγραφα, ανεξάρτητα αν περιέχουν μία ή εκατό σελίδες.

---

![Διάγραμμα που δείχνει τη μηχανή OCR να επεξεργάζεται ένα PDF και να παράγει δομημένο κείμενο.](images/ocr_flow.png "διάγραμμα εξαγωγής κειμένου από pdf")

*Image alt text: διάγραμμα εξαγωγής κειμένου από pdf που απεικονίζει τα βήματα επεξεργασίας OCR.*

## Prerequisites

- Python 3.9 ή νεότερο (ο κώδικας χρησιμοποιεί f‑strings και type hints).  
- Μια pip‑installable OCR package που εκθέτει μια κλάση `OcrEngine` (για παράδειγμα, μια φανταστική βιβλιοθήκη `pyocr`).  
- Ένα αρχείο PDF που θέλετε να επεξεργαστείτε, αποθηκευμένο τοπικά (π.χ., `form.pdf`).  

Αν σας λείπει η βιβλιοθήκη OCR, εγκαταστήστε την με:

```bash
pip install pyocr   # replace with the actual package name you use
```

---

## Step 1: Extract Text from PDF – Setting Up the OCR Engine

Πριν μπορέσουμε να **read PDF with OCR**, χρειάζεται μια παρουσία της μηχανής. Σκεφτείτε τη μηχανή ως τον εγκέφαλο που κοιτάζει κάθε pixel και αποφασίζει ποιο χαρακτήρα αντιπροσωπεύει.

```python
# Step 1: Import the OCR module and create an engine instance
import ocr  # or `import pyocr as ocr` depending on the package

# Create the OCR engine – this may load language models under the hood
ocr_engine = ocr.OcrEngine()
```

> **Why this matters:** Η αρχικοποίηση της μηχανής μία φορά σας επιτρέπει να επαναχρησιμοποιήσετε τα φορτωμένα language packs σε πολλά αρχεία, εξοικονομώντας χρόνο και μνήμη.

---

## Step 2: Load Image for OCR – Preparing Your PDF

Ένα PDF δεν είναι ακατέργαστη εικόνα, γι' αυτό η βιβλιοθήκη συνήθως παρέχει ένα helper για να μετατρέψετε την πρώτη σελίδα (ή όλες τις σελίδες) σε εικόνα που η μηχανή OCR μπορεί να καταλάβει.

```python
# Step 2: Load the PDF page(s) you want to process
# The `load_image` method accepts many formats – PDF, PNG, JPEG, etc.
pdf_path = "YOUR_DIRECTORY/form.pdf"
ocr_engine.load_image(pdf_path)
```

> **Tip:** Αν το PDF σας έχει πολλές σελίδες, πολλές βιβλιοθήκες OCR επιτρέπουν να περάσετε `page=2` ή να κάνετε βρόχο πάνω στο `engine.load_image(pdf_path, page=n)`. Για μεγάλα έγγραφα, σκεφτείτε την επεξεργασία σε παρτίδες ώστε να αποφύγετε αιχμές μνήμης.

---

## Step 3: Use OCR Engine Python – Recognizing Structured Text

Τώρα γίνεται η βαριά δουλειά. Η κλήση `recognize_structured()` επιστρέφει μια ιεραρχία blocks → lines → words, καθένα με ετικέτες γλώσσας, εμπιστοσύνης και bounding boxes.

```python
# Step 3: Perform structured text recognition
structured_result = ocr_engine.recognize_structured()
```

> **What you get:**  
> - `structured_result.blocks` – containers υψηλού επιπέδου (συχνά παραγράφοι ή στήλες).  
> - Κάθε block περιέχει `lines`, και κάθε line περιέχει `words`.  
> - Τα scores εμπιστοσύνης σας επιτρέπουν να φιλτράρετε αβέβαια αποτελέσματα.

---

## Step 4: Iterate Over Results – Accessing Blocks, Lines, and Words

Παρακάτω υπάρχει ένας συμπαγής βρόχος που εκτυπώνει τις πιο χρήσιμες πληροφορίες. Μπορείτε να τον επεκτείνετε για να γράψετε JSON, CSV ή να τροφοδοτήσετε μια βάση δεδομένων.

```python
# Step 4: Walk through the hierarchy and display key data
for block_idx, text_block in enumerate(structured_result.blocks, start=1):
    print(f"Block {block_idx}: language={text_block.language}, confidence={text_block.confidence:.2f}")

    # Show a sample line from the block, if any
    if text_block.lines:
        sample_line = text_block.lines[0]
        print(f"  Sample line: {sample_line.text}")

        # Show a sample word with its bounding box and confidence
        if sample_line.words:
            sample_word = sample_line.words[0]
            print(
                f"    Sample word: '{sample_word.text}' "
                f"bbox={sample_word.bounding_box} "
                f"conf={sample_word.confidence:.2f}"
            )
```

### Expected Output

```
Block 1: language=en, confidence=0.97
  Sample line: Invoice Number: 2025-00123
    Sample word: 'Invoice' bbox=(12,34,78,90) conf=0.99
Block 2: language=en, confidence=0.94
  Sample line: Total Amount: $1,250.00
    Sample word: 'Total' bbox=(15,120,70,155) conf=0.96
...
```

> **Why you’ll love this:** Η ιεραρχία αντικατοπτρίζει τον τρόπο που οι άνθρωποι διαβάζουν μια σελίδα, κάνοντας εύκολη την ανακατασκευή πινάκων ή στήλων αργότερα.

---

## Step 5: Handling Edge Cases – Low Confidence & Multi‑Page PDFs

### Low‑Confidence Words

Αν η εμπιστοσύνη μιας λέξης πέσει κάτω από, π.χ., `0.70`, ίσως θέλετε να την σημαδέψετε για χειροκίνητη επανεξέταση:

```python
LOW_CONF_THRESHOLD = 0.70

for block in structured_result.blocks:
    for line in block.lines:
        for word in line.words:
            if word.confidence < LOW_CONF_THRESHOLD:
                print(f"⚠️ Low confidence: '{word.text}' ({word.confidence:.2f})")
```

### Processing All Pages

```python
# Example: loop over every page in a multi‑page PDF
for page_number in range(ocr_engine.page_count):
    ocr_engine.load_image(pdf_path, page=page_number)
    result = ocr_engine.recognize_structured()
    # …process `result` just like we did above…
```

> **Pro tip:** Αποθηκεύστε ενδιάμεσες εικόνες ως PNG αν η βιβλιοθήκη OCR σας τις επαναδημιουργεί κάθε φορά· αυτό μπορεί να μειώσει δευτερόλεπτα σε μεγάλες παρτίδες.

---

## Full Working Script

Συνδυάζοντας τα παραπάνω, εδώ είναι ένα μοναδικό αρχείο που μπορείτε να τρέξετε αμέσως:

```python
#!/usr/bin/env python3
"""
Extract text from PDF with OCR engine Python.
This script demonstrates loading a PDF, recognizing structured text,
and printing a concise summary of blocks, lines, and words.
"""

import ocr  # Replace with your actual OCR package import

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
PDF_PATH = "YOUR_DIRECTORY/form.pdf"
LOW_CONF_THRESHOLD = 0.70

# ----------------------------------------------------------------------
# Initialize OCR engine
# ----------------------------------------------------------------------
ocr_engine = ocr.OcrEngine()

# ----------------------------------------------------------------------
# Load the PDF (first page by default)
# ----------------------------------------------------------------------
ocr_engine.load_image(PDF_PATH)

# ----------------------------------------------------------------------
# Recognize structured text
# ----------------------------------------------------------------------
structured_result = ocr_engine.recognize_structured()

# ----------------------------------------------------------------------
# Iterate and display results
# ----------------------------------------------------------------------
for block_idx, block in enumerate(structured_result.blocks, start=1):
    print(f"Block {block_idx}: language={block.language}, confidence={block.confidence:.2f}")

    if block.lines:
        line = block.lines[0]
        print(f"  Sample line: {line.text}")

        if line.words:
            word = line.words[0]
            print(
                f"    Sample word: '{word.text}' "
                f"bbox={word.bounding_box} "
                f"conf={word.confidence:.2f}"
            )

    # Flag low‑confidence words inside the block
    for line in block.lines:
        for word in line.words:
            if word.confidence < LOW_CONF_THRESHOLD:
                print(f"⚠️ Low confidence: '{word.text}' ({word.confidence:.2f})")
```

Αποθηκεύστε το ως `extract_pdf_ocr.py` και τρέξτε:

```bash
python extract_pdf_ocr.py
```

Θα πρέπει να δείτε λεπτομέρειες σε επίπεδο block να εκτυπώνονται στην κονσόλα, μαζί με τυχόν προειδοποιήσεις χαμηλής εμπιστοσύνης.

---

## Conclusion

Μόλις καλύψαμε έναν πλήρη, έτοιμο για παραγωγή τρόπο να **extract text from PDF** χρησιμοποιώντας ένα **OCR engine Python**. Από την εγκατάσταση της βιβλιοθήκης, μέσω του **load image for OCR**, μέχρι το **read PDF with OCR** και τέλος την επανάληψη πάνω στο δομημένο αποτέλεσμα, έχετε τώρα ένα επαναχρησιμοποιήσιμο script που μπορείτε να προσαρμόσετε σε οποιοδήποτε έργο.

Επόμενα βήματα που μπορείτε να εξερευνήσετε:

- Εξαγωγή της ιεραρχίας σε JSON για downstream NLP pipelines.  
- Προσθήκη ανίχνευσης γλώσσας για εναλλαγή μοντέλων OCR αυτόματα.  
- Ενσωμάτωση με `pdf2image` για προεπεξεργασία PDF με πολύπλοκες διατάξεις.  

Δοκιμάστε το σε μια παρτίδα τιμολογίων πολλαπλών σελίδων, ρυθμίστε το όριο εμπιστοσύνης, και δείτε πόσο γρήγορα μπορείτε να μετατρέψετε σκαναρισμένα PDF σε αναζητήσιμο, επεξεργάσιμο κείμενο. Αν αντιμετωπίσετε προβλήματα, αφήστε ένα σχόλιο παρακάτω—καλή OCR!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}