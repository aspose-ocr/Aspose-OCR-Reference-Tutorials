---
category: general
date: 2026-03-26
description: Πώς να εξάγετε κείμενο PDF χρησιμοποιώντας OCR. Μάθετε πώς να φορτώνετε
  το PDF ως εικόνα, να αναγνωρίζετε το κείμενο του PDF και να εξάγετε το κείμενο από
  το PDF με ένα απλό παράδειγμα σε Python.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize pdf text
- load pdf as image
- how to use OCR
language: el
og_description: Πώς να εξάγετε κείμενο PDF χρησιμοποιώντας OCR. Αυτός ο οδηγός σας
  δείχνει πώς να φορτώσετε το PDF ως εικόνα, να αναγνωρίσετε το κείμενο του PDF και
  να εξάγετε κείμενο από το PDF σε Python.
og_title: Πώς να εξάγετε κείμενο PDF με OCR – Πλήρης οδηγός
tags:
- OCR
- Python
- PDF processing
title: Πώς να εξάγετε κείμενο PDF με OCR – Πλήρης οδηγός βήμα‑προς‑βήμα
url: /el/python-java/general/how-to-extract-pdf-text-with-ocr-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εξάγετε Κείμενο από PDF με OCR – Πλήρης Οδηγός Βήμα‑Βήμα

Έχετε αναρωτηθεί ποτέ **πώς να εξάγετε PDF** αρχεία που στην πραγματικότητα είναι μόνο σαρωμένες εικόνες; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν χρειάζονται αναζητήσιμο περιεχόμενο αλλά έχουν μόνο PDF που περιέχουν εικόνες. Τα καλά νέα; Μερικές γραμμές κώδικα και μια αξιόπιστη βιβλιοθήκη OCR μπορούν να μετατρέψουν αυτά τα PDF‑εικόνα σε απλό κείμενο σε μια στιγμή.  

Σε αυτό το tutorial θα δούμε **πώς να χρησιμοποιήσετε OCR** για να φορτώσετε ένα PDF ως εικόνα, να αναγνωρίσετε κείμενο PDF, και τελικά **να εξάγετε κείμενο από PDF** έγγραφα οποιουδήποτε μήκους. Στο τέλος θα έχετε ένα εκτελέσιμο script, μια σαφή εξήγηση κάθε βήματος, και μερικές συμβουλές για να αποφύγετε τα συνηθισμένα προβλήματα.

## Τι Θα Χρειαστεί

- Python 3.9 ή νεότερο (ο κώδικας λειτουργεί επίσης σε 3.10+)  
- Το πακέτο Python `ocr` (ή οποιαδήποτε συμβατή βιβλιοθήκη OCR που εκθέτει `OcrEngine`, `OcrEngineMode` και `Imaging.Image`)  
- Ένα PDF πολλαπλών σελίδων που θέλετε να επεξεργαστείτε (για την επίδειξη θα το ονομάσουμε `multi_page.pdf`)  
- Βασική εξοικείωση με εικονικά περιβάλλοντα (προαιρετικό αλλά συνιστάται)

> **Συμβουλή επαγγελματία:** Αν χρησιμοποιείτε Windows, σκεφτείτε να χρησιμοποιήσετε το Anaconda Prompt· σε macOS/Linux, μια απλή εντολή `python -m venv venv && source venv/bin/activate` κάνει τη δουλειά.

## Βήμα 1: Εγκατάσταση της Βιβλιοθήκης OCR

Πρώτα, κατεβάστε το πακέτο OCR από το PyPI. Το παρακάτω παράδειγμα χρησιμοποιεί ένα φανταστικό πακέτο `ocr` που αντικατοπτρίζει το API που φαίνεται στο απόσπασμα κώδικα, αλλά οι περισσότερες πραγματικές βιβλιοθήκες (όπως `pytesseract` + `pdf2image`) ακολουθούν το ίδιο μοτίβο.

```bash
pip install ocr
```

Αν χρησιμοποιείτε διαφορετική μηχανή, αντικαταστήστε το `ocr` με το κατάλληλο όνομα (π.χ., `pip install pytesseract pdf2image`).

## Βήμα 2: Αρχικοποίηση του Μηχανήματος OCR

Η δημιουργία ενός αντικειμένου μηχανής είναι το θεμέλιο του **πώς να εξάγετε PDF** κείμενο. Σκεφτείτε τη μηχανή ως τον εγκέφαλο που θα ερμηνεύσει τα pixel σε κάθε σελίδα PDF.

```python
import ocr

# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Set the engine to the default mode (fast enough for most PDFs)
ocr_engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)
```

> **Γιατί είναι σημαντικό:** Η `set_engine_mode` σας επιτρέπει να ανταλλάξετε ταχύτητα με ακρίβεια. Η `DEFAULT` είναι μια ισορροπημένη επιλογή· αν χρειάζεστε μεγαλύτερη ακρίβεια, μεταβείτε σε `HIGH_ACCURACY` (αν η βιβλιοθήκη το υποστηρίζει).

## Βήμα 3: Φόρτωση του PDF ως Αντικείμενο Εικόνας

Το OCR λειτουργεί σε εικόνες, όχι σε containers PDF, επομένως πρέπει πρώτα να μετατρέψουμε το PDF σε αναπαράσταση εικόνας. Η μέθοδος `Imaging.Image.load` διαχειρίζεται αυτόματα PDF πολλαπλών σελίδων.

```python
# Step 3: Load the multi‑page PDF as an image object
pdf_path = "YOUR_DIRECTORY/multi_page.pdf"
pdf_image = ocr.Imaging.Image.load(pdf_path)
```

> **Ακραία περίπτωση:** Κάποιες βιβλιοθήκες δέχονται μόνο εικόνα μίας σελίδας. Σε αυτήν την περίπτωση, θα επαναλαμβάνατε κάθε σελίδα χρησιμοποιώντας `pdf2image.convert_from_path`. Η κλήση `load` μας αφαιρεί αυτή τη δυσκολία, κάνοντας το **load pdf as image** μια εντολή μίας γραμμής.

## Βήμα 4: Αναγνώριση Κειμένου σε Όλες τις Σελίδες

Τώρα έρχεται ο πυρήνας του **recognize PDF text**. Η μηχανή σαρώνει κάθε σελίδα, επιστρέφοντας μια λίστα αντικειμένων αποτελεσμάτων—ένα ανά σελίδα.

```python
# Step 4: Recognize text on all pages of the PDF
page_results = ocr_engine.recognize_multi_page(pdf_image)
```

Κάθε `page_result` περιέχει μεθόδους όπως `get_text()` (απλό κείμενο) και `get_confidence()` (προαιρετικό μέτρο ποιότητας).  

> **Συμβουλή:** Αν χρειάζεστε μόνο την πρώτη σελίδα, καλέστε `recognize(pdf_image[0])` αντί για τη βοηθητική λειτουργία πολλαπλών σελίδων.

## Βήμα 5: Επανάληψη στα Αποτελέσματα και Εξαγωγή του Κειμένου

Τέλος, επαναλαμβάνουμε τα αποτελέσματα, εκτυπώνοντας το κείμενο κάθε σελίδας. Αυτό ολοκληρώνει τη ροή εργασίας **extract text from PDF**.

```python
# Step 5: Print extracted text page by page
for index, page_result in enumerate(page_results):
    print(f"--- Page {index + 1} ---")
    print(page_result.get_text())
    # Optional: show confidence score
    # print(f"Confidence: {page_result.get_confidence():.2f}%")
```

### Αναμενόμενο Αποτέλεσμα

Αν το `multi_page.pdf` περιέχει τρεις σελίδες με τις λέξεις “Hello”, “World” και “Python”, θα δείτε:

```
--- Page 1 ---
Hello
--- Page 2 ---
World
--- Page 3 ---
Python
```

Αυτό ήταν—το PDF σας είναι τώρα πλήρως αναζητήσιμο και το κείμενο είναι έτοιμο για επεξεργασία (αποθήκευση, ανάλυση συναισθήματος, ό,τι χρειάζεστε).

## Βήμα 6: Διαχείριση Συνηθισμένων Προβλημάτων

| Πρόβλημα | Γιατί Συμβαίνει | Γρήγορη Διόρθωση |
|----------|----------------|-------------------|
| **Κενή έξοδος** | Οι σελίδες PDF είναι σαρωμένες σε χαμηλό DPI, κάνοντας τους χαρακτήρες ακατανόητους. | Αυξήστε την ανάλυση της εικόνας πριν το OCR: `pdf_image = pdf_image.resize(300)` (300 DPI είναι το ιδανικό). |
| **Αχρείαστα σύμβολα** | Τα μη λατινικά αλφάβητα χρειάζονται πακέτα γλώσσας. | Φορτώστε το κατάλληλο μοντέλο γλώσσας: `ocr_engine.load_language('spa')` για Ισπανικά, κ.λπ. |
| **Κατανάλωση μνήμης σε τεράστια PDF** | Η φόρτωση όλων των σελίδων ταυτόχρονα καταναλώνει RAM. | Επεξεργαστείτε τις σελίδες σε τμήματα: `for img in pdf_image.split(batch=10): …` (ψευδο‑κώδικας). |
| **Αργή απόδοση** | Η χρήση του `DEFAULT` σε τεράστιο έγγραφο μπορεί να είναι αργή. | Μεταβείτε σε λειτουργία `FAST` ή εκτελέστε OCR παράλληλα χρησιμοποιώντας `concurrent.futures`. |

## Μπόνους: Αποθήκευση του Εξαγόμενου Κειμένου σε Αρχείο

Οι περισσότερες πραγματικές ροές εργασίας χρειάζονται το κείμενο αποθηκευμένο. Εδώ είναι ένας μικρός βοηθός που γράφει τα πάντα στο `output.txt`.

```python
output_path = "YOUR_DIRECTORY/output.txt"

with open(output_path, "w", encoding="utf-8") as f:
    for idx, result in enumerate(page_results):
        f.write(f"--- Page {idx + 1} ---\n")
        f.write(result.get_text() + "\n\n")
print(f"All text saved to {output_path}")
```

## Συνδυάζοντας Όλα – Πλήρες Script

Παρακάτω είναι το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα. Αντιγράψτε‑και‑επικολλήστε, προσαρμόστε τις διαδρομές αρχείων, και είστε έτοιμοι.

```python
# -*- coding: utf-8 -*-
"""
How to extract PDF text with OCR – end‑to‑end example.

Prerequisites:
    pip install ocr
"""

import ocr

def extract_text_from_pdf(pdf_path: str):
    """
    Load a PDF, run OCR on every page, and return a list of strings.
    """
    # Initialize engine
    engine = ocr.OcrEngine()
    engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)

    # Load PDF as image (multi‑page support)
    pdf_image = ocr.Imaging.Image.load(pdf_path)

    # Recognize text on all pages
    results = engine.recognize_multi_page(pdf_image)

    # Collect plain text
    texts = [res.get_text() for res in results]
    return texts

def main():
    pdf_file = "YOUR_DIRECTORY/multi_page.pdf"
    texts = extract_text_from_pdf(pdf_file)

    # Print and optionally save
    for i, txt in enumerate(texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()

    # Save to file
    out_path = "YOUR_DIRECTORY/extracted_text.txt"
    with open(out_path, "w", encoding="utf-8") as out_f:
        for i, txt in enumerate(texts, start=1):
            out_f.write(f"--- Page {i} ---\n{txt}\n\n")
    print(f"Extracted text stored in {out_path}")

if __name__ == "__main__":
    main()
```

Τρέξτε το:

```bash
python extract_pdf_ocr.py
```

Θα πρέπει να δείτε το περιεχόμενο κάθε σελίδας να εκτυπώνεται στην κονσόλα, ακολουθούμενο από επιβεβαίωση ότι το αρχείο `extracted_text.txt` δημιουργήθηκε.

## Συμπέρασμα

Καλύψαμε **πώς να εξάγετε PDF** κείμενο από έγγραφα μόνο με εικόνες χρησιμοποιώντας μια μηχανή OCR, από την εγκατάσταση της βιβλιοθήκης μέχρι τη διαχείριση αποτελεσμάτων πολλαπλών σελίδων και την αποθήκευση του αποτελέσματος. Τώρα ξέρετε **πώς να χρησιμοποιήσετε OCR**, πώς να **φορτώσετε PDF ως εικόνα**, και πώς να **αναγνωρίσετε κείμενο PDF** αξιόπιστα.  

Επόμενα βήματα; Δοκιμάστε να αλλάξετε τη προεπιλεγμένη λειτουργία της μηχανής σε ρύθμιση υψηλής ακρίβειας, πειραματιστείτε με πακέτα γλώσσας για πολυγλωσσικά PDF, ή στείλτε το εξαγόμενο κείμενο σε έναν πλήρη δείκτη αναζήτησης όπως το Elasticsearch. Ο ουρανός είναι το όριο μόλις έχετε κατακτήσει τα βασικά της εξαγωγής κειμένου από αρχεία PDF.

---

![how to extract pdf example](images/ocr_flowchart.png){alt="διάγραμμα ροής εξαγωγής pdf"}

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}