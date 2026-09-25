---
category: general
date: 2026-01-12
description: Μάθετε πώς να κάνετε OCR σε PDF με Python και να κάνετε το PDF αναζητήσιμο
  γρήγορα. Μετατρέψτε σκαναρισμένα PDF, εξάγετε κείμενο από PDF και κάντε OCR σε σκαναρισμένα
  PDF με Python χρησιμοποιώντας το Aspose OCR.
draft: false
keywords:
- how to ocr pdf
- make pdf searchable
- convert scanned pdf
- extract text pdf
- ocr scanned pdf python
language: el
og_description: Πώς να κάνετε OCR PDF σε Python; Αυτό το βήμα‑βήμα tutorial σας δείχνει
  πώς να μετατρέψετε σαρωμένα αρχεία PDF σε αναζητήσιμα PDF και να εξάγετε κείμενο
  με το Aspose OCR.
og_title: Πώς να κάνετε OCR σε PDF και να το κάνετε αναζητήσιμο – Οδηγός Python
tags:
- OCR
- Python
- PDF processing
title: Πώς να κάνετε OCR σε PDF και να το κάνετε αναζητήσιμο – Οδηγός Python
url: /el/python-java/general/how-to-ocr-pdf-and-make-it-searchable-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να κάνετε OCR PDF και να το κάνετε Αναζητήσιμο – Οδηγός Python

Έχετε αναρωτηθεί ποτέ **πώς να κάνετε OCR PDF** αρχεία χωρίς να ξοδέψετε μια περιουσία σε εμπορικό λογισμικό; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν δυσκολίες όταν πρέπει να μετατρέψουν ένα σαρωμένο συμβόλαιο, ένα τιμολόγιο ή οποιοδήποτε PDF βασισμένο σε εικόνα σε ένα αναζητήσιμο έγγραφο. Τα καλά νέα; Με μερικές γραμμές Python και Aspose OCR μπορείτε να μετατρέψετε σαρωμένα PDF, να εξάγετε κείμενο PDF και τελικά να κάνετε το PDF αναζητήσιμο σε λίγα λεπτά.

Σε αυτό το εκπαιδευτικό υλικό θα περάσουμε από όλα όσα χρειάζεστε: από την εγκατάσταση της βιβλιοθήκης, τη ρύθμιση της γλώσσας, την επεξεργασία ενός σαρωμένου PDF, μέχρι την αποθήκευση του αποτελέσματος ως αναζητήσιμο PDF που περιέχει τόσο την αρχική εικόνα όσο και ένα κρυφό στρώμα κειμένου. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο script που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο—χωρίς να χρειάζεται χειροκίνητη αντιγραφή‑επικόλληση.

---

## Τι Θα Χρειαστείτε

- **Python 3.8+** (ο κώδικας λειτουργεί σε 3.9, 3.10 και νεότερες εκδόσεις)
- Μία ενεργή άδεια **Aspose OCR for Python** (μια δωρεάν δοκιμή λειτουργεί για πειραματισμό)
- Ένα σαρωμένο αρχείο PDF (π.χ., `scanned_contract.pdf`) που θέλετε να κάνετε αναζητήσιμο
- Βασική εξοικείωση με τη γραμμή εντολών και τα εικονικά περιβάλλοντα (προαιρετικό αλλά συνιστάται)

> **Συμβουλή:** Αν δεν έχετε ακόμη άδεια, εγγραφείτε για δοκιμαστική περίοδο 30 ημερών στην ιστοσελίδα της Aspose· η δοκιμαστική έκδοση είναι πλήρως λειτουργική για σκοπούς ανάπτυξης.

## Πώς να κάνετε OCR PDF με Aspose OCR (Κύρια Λέξη-Κλειδί σε H2)

Το πρώτο βήμα είναι να αποκτήσετε το σωστό πακέτο. Το Aspose OCR παρέχει ένα καθαρό, υψηλού επιπέδου API που αφαιρεί τις λεπτομέρειες της χαμηλού επιπέδου επεξεργασίας εικόνας.

```bash
# Create a virtual environment (optional but tidy)
python -m venv venv
source venv/bin/activate   # On Windows use `venv\Scripts\activate`

# Install the Aspose OCR package
pip install aspose-ocr
```

Μόλις εγκατασταθεί το πακέτο, μπορείτε να ξεκινήσετε να γράφετε το script.

```python
# Step 1: Import the Aspose OCR module
import asposeocr as ocr

# Step 2: Create an OCR engine instance and set the recognition language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

> **Γιατί να ορίσετε τη γλώσσα;**  
> Η ακρίβεια του OCR εξαρτάται σε μεγάλο βαθμό από το μοντέλο γλώσσας. Ενημερώνοντας ρητά τη μηχανή ότι αναμένει κείμενο στα Αγγλικά, μειώνετε τα ψευδώς θετικά και επιταχύνετε την επεξεργασία.

## Βήμα 2: Μετατροπή Σαρωμένου PDF σε Αναζητήσιμο PDF

Τώρα που η μηχανή είναι έτοιμη, κατευθύνετέ την στο σαρωμένο έγγραφό σας. Η μέθοδος `process_pdf` επιστρέφει ένα αντικείμενο `PdfResult` που περιέχει τόσο τα αρχικά δεδομένα εικόνας όσο και το αναγνωρισμένο κείμενο.

```python
# Step 3: Process the scanned PDF to extract text
input_pdf_path = "YOUR_DIRECTORY/scanned_contract.pdf"
pdf_result = ocr_engine.process_pdf(input_pdf_path)
```

Αν χρειάζεται να **μετατρέψετε σαρωμένα PDF** αρχεία μαζικά, απλώς κάντε βρόχο σε έναν φάκελο και καλέστε `process_pdf` για κάθε αρχείο. Η μηχανή διαχειρίζεται PDF πολλαπλών σελίδων αμέσως.

## Βήμα 3: Αποθήκευση του Αποτελέσματος ως Αναζητήσιμο PDF (Κάντε το PDF Αναζητήσιμο)

Το τελευταίο κομμάτι του παζλ είναι η αποθήκευση της αναζητήσιμης έκδοσης. Το Aspose OCR το κάνει αυτό με μία γραμμή κώδικα:

```python
# Step 4: Define the output path for the searchable PDF
searchable_pdf_path = "YOUR_DIRECTORY/contract_searchable.pdf"

# Step 5: Save the result as a searchable PDF (image + hidden text layer)
pdf_result.save_as_searchable_pdf(searchable_pdf_path)
```

Όταν ανοίξετε το `contract_searchable.pdf` σε οποιονδήποτε προβολέα PDF, θα δείτε την αρχική σαρωμένη εικόνα, αλλά τώρα μπορείτε **να αναζητήσετε οποιαδήποτε λέξη** που η μηχανή OCR αναγνώρισε. Το κρυφό στρώμα κειμένου είναι αόρατο στο μάτι αλλά πλήρως ευρετηριάσιμο.

### Πλήρες Script – Έτοιμο για Εκτέλεση

Παρακάτω είναι το πλήρες, εκτελέσιμο παράδειγμα. Αντιγράψτε‑επικολλήστε το σε ένα αρχείο με όνομα `make_searchable.py` και προσαρμόστε τις διαδρομές ώστε να ταιριάζουν με το περιβάλλον σας.

```python
# make_searchable.py
# -------------------------------------------------
# Complete script to OCR a scanned PDF and make it searchable
# -------------------------------------------------

import os
import asposeocr as ocr

def ocr_to_searchable(input_path: str, output_path: str, language=ocr.Language.ENGLISH):
    """
    Convert a scanned PDF into a searchable PDF.
    
    Parameters
    ----------
    input_path : str
        Path to the scanned PDF file.
    output_path : str
        Destination path for the searchable PDF.
    language : ocr.Language, optional
        OCR language model (default is English).
    """
    if not os.path.isfile(input_path):
        raise FileNotFoundError(f"Input file not found: {input_path}")

    # Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = language

    # Process the PDF (extracts images + hidden text)
    result = engine.process_pdf(input_path)

    # Save as searchable PDF
    result.save_as_searchable_pdf(output_path)
    print(f"✅ Searchable PDF saved to: {output_path}")

if __name__ == "__main__":
    # Example usage – replace with your actual file locations
    INPUT_PDF = "YOUR_DIRECTORY/scanned_contract.pdf"
    OUTPUT_PDF = "YOUR_DIRECTORY/contract_searchable.pdf"
    ocr_to_searchable(INPUT_PDF, OUTPUT_PDF)
```

**Αναμενόμενη έξοδος:**  
Η εκτέλεση του script εκτυπώνει μια γραμμή επιβεβαίωσης και δημιουργεί το `contract_searchable.pdf`. Ανοίξτε το αρχείο, πατήστε `Ctrl + F` και πληκτρολογήστε οποιαδήποτε λέξη εμφανίζεται στην αρχική σαρωμένη εικόνα—θα δείτε τα αποτελέσματα αμέσως.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### 1. Τι γίνεται αν το PDF περιέχει πολλαπλές γλώσσες;

Μπορείτε να περάσετε μια λίστα γλωσσών στη μηχανή:

```python
engine.language = [ocr.Language.ENGLISH, ocr.Language.SPANISH]
```

Το Aspose OCR θα προσπαθήσει να αναγνωρίσει κείμενο και στις δύο γλώσσες στην ίδια σελίδα.

### 2. Πώς να διαχειριστώ σαρώσεις χαμηλής ανάλυσης;

Αν οι εικόνες προέλευσης είναι κάτω από 150 dpi, η ακρίβεια του OCR μπορεί να υποφέρει. Προεπεξεργαστείτε το PDF με ένα εργαλείο όπως το `pdfimages` για να εξάγετε τις σελίδες, αυξήστε την ανάλυση τους με το Pillow και τροφοδοτήστε τις εικόνες υψηλότερης ανάλυσης ξανά στο `process_pdf`.

### 3. Μπορώ να εξάγω το ακατέργαστο κείμενο χωρίς να δημιουργήσω αναζητήσιμο PDF;

Απολύτως. Το αντικείμενο `PdfResult` εκθέτει μια ιδιότητα `text`:

```python
plain_text = pdf_result.text
print(plain_text[:500])  # preview first 500 characters
```

Αυτό καλύπτει τη χρήση **extract text pdf** όταν χρειάζεστε μόνο τους ακατέργαστους χαρακτήρες.

### 4. Υπάρχει τρόπος να επεξεργαστείτε μαζικά ένα φάκελο PDF;

Ναι—τυλίξτε τη λειτουργία `ocr_to_searchable` σε έναν απλό βρόχο:

```python
import glob

for src in glob.glob("scans/*.pdf"):
    dst = src.replace("scans/", "searchable/").replace(".pdf", "_searchable.pdf")
    ocr_to_searchable(src, dst)
```

Τώρα μπορείτε να **μετατρέψετε σαρωμένα pdf** αρχεία μαζικά με μία μόνο εντολή.

## Συμβουλές Απόδοσης

- **Επαναχρησιμοποίηση της μηχανής**: Η δημιουργία ενός νέου `OcrEngine` για κάθε αρχείο προσθέτει επιπλέον φόρτο. Δημιουργήστε το μία φορά και επαναχρησιμοποιήστε το σε πολλαπλές κλήσεις.
- **Παράλληλη επεξεργασία**: Για μεγάλες παρτίδες, σκεφτείτε το `concurrent.futures.ThreadPoolExecutor` της Python—το Aspose OCR είναι ασφαλές για νήματα σε λειτουργίες μόνο ανάγνωσης.
- **Διαχείριση μνήμης**: Αν επεξεργάζεστε πολύ μεγάλα PDF (εκατοντάδες σελίδες), καλέστε `gc.collect()` μετά από κάθε αρχείο για να ελευθερώσετε μνήμη.

## Συμπέρασμα

Καλύψαμε **πώς να κάνετε OCR PDF** αρχεία σε Python, μετατρέψαμε αυτές τις σαρώσεις σε **αναζητήσιμα PDFs**, και ακόμη σας δείξαμε πώς να **εξάγετε κείμενο PDF** απευθείας. Με το Aspose OCR έχετε μια αξιόπιστη μηχανή που διαχειρίζεται έγγραφα πολλαπλών σελίδων, πολλαπλές γλώσσες και υψηλής ακρίβειας αναγνώριση—όλα με λίγες μόνο γραμμές κώδικα.

Δοκιμάστε το στα δικά σας συμβόλαια, τιμολόγια ή αρχειοθετημένα ερευνητικά έγγραφα. Μόλις κατακτήσετε τα βασικά, πειραματιστείτε με τις προχωρημένες λειτουργίες—όπως προσαρμοσμένα λεξικά, προεπεξεργασία εικόνας ή ενσωμάτωση του αποτελέσματος σε ευρετήριο πλήρους κειμένου όπως το Elasticsearch.

Έχετε περισσότερες ερωτήσεις σχετικά με **ocr scanned pdf python** ή χρειάζεστε βοήθεια για την αντιμετώπιση μιας δύσκολης σάρωσης; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

--- 

![how to ocr pdf example](image-placeholder.png){alt="πώς να κάνετε OCR PDF παράδειγμα"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}