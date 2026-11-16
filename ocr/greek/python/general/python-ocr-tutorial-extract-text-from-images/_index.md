---
category: general
date: 2026-03-28
description: Μάθημα Python OCR που δείχνει πώς να εξάγετε κείμενο από εικόνα με το
  Aspose OCR Cloud. Μάθετε πώς να φορτώνετε εικόνα για OCR και να μετατρέπετε την
  εικόνα σε απλό κείμενο σε λίγα λεπτά.
draft: false
keywords:
- python ocr tutorial
- extract text image python
- ocr image to text
- load image for ocr
- convert image plain text
language: el
og_description: Το σεμινάριο Python OCR εξηγεί πώς να φορτώσετε εικόνα για OCR και
  να μετατρέψετε το απλό κείμενο της εικόνας χρησιμοποιώντας το Aspose OCR Cloud.
  Λάβετε τον πλήρη κώδικα και συμβουλές.
og_title: Python OCR Tutorial – Εξαγωγή κειμένου από εικόνες
tags:
- OCR
- Python
- Image Processing
title: Python OCR Tutorial – Εξαγωγή κειμένου από εικόνες
url: /el/python/general/python-ocr-tutorial-extract-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR Tutorial – Εξαγωγή κειμένου από εικόνες

Έχετε αναρωτηθεί ποτέ πώς να μετατρέψετε μια ακατάστατη φωτογραφία από απόδειξη σε καθαρό, αναζητήσιμο κείμενο; Δεν είστε ο μόνος. Κατά την εμπειρία μου, το μεγαλύτερο εμπόδιο δεν είναι η μηχανή OCR, αλλά η μετατροπή της εικόνας στη σωστή μορφή και η εξαγωγή του απλού κειμένου χωρίς προβλήματα.  

Αυτό το **python ocr tutorial** σας καθοδηγεί βήμα προς βήμα—φόρτωση εικόνας για OCR, εκτέλεση της αναγνώρισης, και τελικά μετατροπή του απλού κειμένου της εικόνας σε μια συμβολοσειρά Python που μπορείτε να αποθηκεύσετε ή να αναλύσετε. Στο τέλος θα μπορείτε να **extract text image python** με στυλ, και δεν θα χρειαστείτε καμία επί πληρωμή άδεια για να ξεκινήσετε.

## Τι θα μάθετε

- Πώς να εγκαταστήσετε και να εισάγετε το Aspose OCR Cloud SDK για Python.  
- Ο ακριβής κώδικας για **load image for OCR** (PNG, JPEG, TIFF, PDF, κλπ).  
- Πώς να καλέσετε τη μηχανή για να εκτελέσετε τη μετατροπή **ocr image to text**.  
- Συμβουλές για τη διαχείριση κοινών edge‑cases όπως PDF πολλαπλών σελίδων ή σάρωση χαμηλής ανάλυσης.  
- Τρόποι επαλήθευσης του αποτελέσματος και τι να κάνετε αν το κείμενο εμφανίζεται παραμορφωμένο.

### Προαπαιτούμενα

- Python 3.8+ εγκατεστημένο στο μηχάνημά σας.  
- Δωρεάν λογαριασμός Aspose Cloud (η δοκιμή λειτουργεί χωρίς άδεια).  
- Βασική εξοικείωση με pip και εικονικά περιβάλλοντα—τίποτα περίπλοκο.

> **Pro tip:** Αν ήδη χρησιμοποιείτε virtualenv, ενεργοποιήστε το τώρα. Διατηρεί τις εξαρτήσεις σας οργανωμένες και αποτρέπει συγκρούσεις εκδόσεων.

![Στιγμιότυπο οθόνης του Python OCR tutorial που δείχνει το αναγνωρισμένο κείμενο](path/to/ocr_example.png "Python OCR tutorial – εμφάνιση εξαγόμενου απλού κειμένου")

## Step 1 – Εγκατάσταση του Aspose OCR Cloud SDK

Πρώτα απ' όλα, χρειαζόμαστε τη βιβλιοθήκη που επικοινωνεί με την υπηρεσία OCR της Aspose. Ανοίξτε ένα τερματικό και εκτελέστε:

```bash
pip install asposeocrcloud
```

Αυτή η εντολή κατεβάζει το πιο πρόσφατο SDK (επί του παρόντος έκδοση 23.12). Το πακέτο περιλαμβάνει όλα όσα χρειάζεστε—δεν απαιτούνται πρόσθετες βιβλιοθήκες επεξεργασίας εικόνας.

## Step 2 – Αρχικοποίηση της μηχανής OCR (Primary Keyword in Action)

Τώρα που το SDK είναι έτοιμο, μπορούμε να εκκινήσουμε τη μηχανή **python ocr tutorial**. Ο κατασκευαστής δεν χρειάζεται κανένα κλειδί άδειας για τη δοκιμή, κάτι που απλοποιεί τη διαδικασία.

```python
import asposeocrcloud as ocr

# Initialise the OCR engine – no licence needed for trial use
ocr_engine = ocr.OcrEngine()
```

> **Why this matters:** Η αρχικοποίηση της μηχανής μόνο μία φορά διατηρεί τις επόμενες κλήσεις γρήγορες. Αν δημιουργείτε ξανά το αντικείμενο για κάθε εικόνα, θα σπαταλήσετε δικτυακές κλήσεις.

## Step 3 – Φόρτωση εικόνας για OCR

Εδώ όπου η λέξη-κλειδί **load image for OCR** λάμπει. Η μέθοδος `Image.load` του SDK δέχεται διαδρομή αρχείου ή URL, και ανιχνεύει αυτόματα τη μορφή (PNG, JPEG, TIFF, PDF, κλπ). Ας φορτώσουμε ένα δείγμα απόδειξης:

```python
# Step 3: Load the input image (PNG, JPEG, TIFF, PDF …)
input_image = ocr.Image.load(r"YOUR_DIRECTORY/receipt.png")
```

Αν εργάζεστε με PDF πολλαπλών σελίδων, απλώς δείξτε στο αρχείο PDF· το SDK θα αντιμετωπίσει κάθε σελίδα ως ξεχωριστή εικόνα εσωτερικά.

## Step 4 – Εκτέλεση μετατροπής OCR εικόνας σε κείμενο

Με την εικόνα στη μνήμη, η πραγματική OCR εκτελείται σε μία γραμμή. Η μέθοδος `recognize` επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει το απλό κείμενο, τις βαθμολογίες εμπιστοσύνης, και ακόμη και τα πλαίσια περιορισμού εάν τα χρειαστείτε αργότερα.

```python
# Step 4: Perform OCR on the loaded image
ocr_result = ocr_engine.recognize(input_image)
```

> **Edge case:** Για εικόνες χαμηλής ανάλυσης (κάτω από 300 dpi) ίσως θέλετε πρώτα να αυξήσετε το μέγεθος της εικόνας. Το SDK προσφέρει βοηθητικό `Resize`, αλλά για τις περισσότερες αποδείξεις η προεπιλογή λειτουργεί καλά.

## Step 5 – Μετατροπή του απλού κειμένου εικόνας σε χρήσιμη συμβολοσειρά

Το τελευταίο κομμάτι του παζλ είναι η εξαγωγή του απλού κειμένου από το αντικείμενο αποτελέσματος. Αυτό είναι το βήμα **convert image plain text** που μετατρέπει το blob OCR σε κάτι που μπορείτε να εκτυπώσετε, αποθηκεύσετε ή να το δώσετε σε άλλο σύστημα.

```python
# Step 5: Output the recognised plain text
print("Plain OCR:")
print(ocr_result.text)
```

Όταν εκτελέσετε το script, θα πρέπει να δείτε κάτι όπως:

```
Plain OCR:
Starbucks Coffee
Date: 2026/03/27
Total: $4.75
Thank you!
```

Αυτή η έξοδος είναι τώρα μια κανονική συμβολοσειρά Python, έτοιμη για εξαγωγή CSV, εισαγωγή σε βάση δεδομένων ή επεξεργασία φυσικής γλώσσας.

## Διαχείριση κοινών προβλημάτων

### 1. Κενές ή θορυβώδεις εικόνες

Αν το `ocr_result.text` επιστρέφει κενό, ελέγξτε ξανά την ποιότητα της εικόνας. Μια γρήγορη λύση είναι να προσθέσετε ένα βήμα προεπεξεργασίας:

```python
# Simple preprocessing – convert to grayscale and increase contrast
processed = input_image.to_grayscale().adjust_contrast(1.2)
ocr_result = ocr_engine.recognize(processed)
```

### 2. PDF πολλαπλών σελίδων

Όταν δίνετε ένα PDF, το `recognize` επιστρέφει αποτελέσματα για κάθε σελίδα. Επανάληψη μέσω αυτών ως εξής:

```python
pdf_image = ocr.Image.load("document.pdf")
pages = pdf_image.pages  # collection of page images

for i, page in enumerate(pages, start=1):
    result = ocr_engine.recognize(page)
    print(f"--- Page {i} ---")
    print(result.text)
```

### 3. Υποστήριξη γλώσσας

Το Aspose OCR υποστηρίζει πάνω από 60 γλώσσες. Για να αλλάξετε τη γλώσσα, ορίστε την ιδιότητα `language` πριν καλέσετε το `recognize`:

```python
ocr_engine.language = "fr"  # French
ocr_result = ocr_engine.recognize(input_image)
```

## Πλήρες λειτουργικό παράδειγμα

Συνδυάζοντας τα πάντα, εδώ είναι ένα πλήρες script έτοιμο για αντιγραφή‑επικόλληση που καλύπτει τα πάντα από την εγκατάσταση μέχρι τη διαχείριση edge‑case:

```python
# -*- coding: utf-8 -*-
"""
Python OCR tutorial – complete example using Aspose OCR Cloud.
Demonstrates loading an image, performing OCR, and handling multi‑page PDFs.
"""

import asposeocrcloud as ocr
import os

def ocr_file(filepath: str, language: str = "en"):
    """
    Perform OCR on a given file (image or PDF) and return plain text.
    """
    # Initialise engine (trial licence)
    engine = ocr.OcrEngine()
    engine.language = language

    # Load the file – SDK auto‑detects format
    image = ocr.Image.load(filepath)

    # If it's a PDF, iterate over pages
    if image.is_pdf:
        all_text = []
        for page in image.pages:
            result = engine.recognize(page)
            all_text.append(result.text)
        return "\n".join(all_text)

    # Single‑image case
    result = engine.recognize(image)
    return result.text


if __name__ == "__main__":
    # Example usage – replace with your own path
    sample_path = os.path.join("YOUR_DIRECTORY", "receipt.png")

    if not os.path.exists(sample_path):
        raise FileNotFoundError(f"File not found: {sample_path}")

    extracted = ocr_file(sample_path)
    print("=== Extracted Text ===")
    print(extracted)
```

Εκτελέστε το script (`python ocr_demo.py`) και θα δείτε την έξοδο **ocr image to text** απευθείας στην κονσόλα σας.

## Ανακεφαλαίωση – Τι καλύψαμε

- Εγκαταστήσαμε το SDK **Aspose OCR Cloud** (`pip install asposeocrcloud`).  
- **Initialised the OCR engine** χωρίς άδεια (τέλειο για δοκιμή).  
- Δείξαμε πώς να **load image for OCR**, είτε πρόκειται για PNG, JPEG ή PDF.  
- Εκτελέσαμε τη μετατροπή **ocr image to text** και **converted image plain text** σε μια χρήσιμη συμβολοσειρά Python.  
- Αντιμετωπίσαμε κοινά προβλήματα όπως σάρωση χαμηλής ανάλυσης, PDF πολλαπλών σελίδων και επιλογή γλώσσας.

## Επόμενα βήματα & Σχετικά θέματα

Τώρα που έχετε κατακτήσει το **python ocr tutorial**, σκεφτείτε να εξερευνήσετε:

- **Extract text image python** για επεξεργασία παρτίδας μεγάλων φακέλων αποδείξεων.  
- Ενσωμάτωση της εξόδου OCR με **pandas** για ανάλυση δεδομένων (`df = pd.read_csv(StringIO(extracted))`).  
- Χρήση του **Tesseract OCR** ως εναλλακτική όταν η σύνδεση στο διαδίκτυο είναι περιορισμένη.  
- Προσθήκη post‑processing με **spaCy** για αναγνώριση οντοτήτων όπως ημερομηνίες, ποσά και ονόματα εμπόρων.  

Μη διστάσετε να πειραματιστείτε: δοκιμάστε διαφορετικές μορφές εικόνας, ρυθμίστε την αντίθεση ή αλλάξτε γλώσσες. Το πεδίο του OCR είναι ευρύ, και οι δεξιότητες που μόλις αποκτήσατε αποτελούν μια ισχυρή βάση για οποιοδήποτε έργο αυτοματοποίησης εγγράφων.

Καλό προγραμματισμό, και εύχομαι το κείμενό σας πάντα να είναι αναγνώσιμο!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}