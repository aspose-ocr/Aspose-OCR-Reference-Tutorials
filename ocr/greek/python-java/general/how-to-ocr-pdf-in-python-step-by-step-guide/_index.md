---
category: general
date: 2026-03-28
description: Μάθετε πώς να κάνετε OCR σε PDF με Python γρήγορα. Αυτός ο οδηγός σας
  δείχνει πώς να εξάγετε κείμενο από PDF, να αναγνωρίζετε κείμενο από PDF και να μετατρέπετε
  σαρωμένα PDF σε κείμενο χρησιμοποιώντας το Aspose OCR.
draft: false
keywords:
- how to ocr pdf
- ocr pdf with python
- extract text from pdf
- recognize text from pdf
- convert scanned pdf to text
language: el
og_description: Μάθετε πώς να κάνετε OCR σε PDF με Python. Εξάγετε κείμενο από PDF,
  αναγνωρίστε κείμενο από PDF και μετατρέψτε σαρωμένα PDF σε κείμενο σε λίγα λεπτά.
og_title: Πώς να κάνετε OCR PDF σε Python – Πλήρης Οδηγός
tags:
- PDF
- OCR
- Python
- Aspose
title: Πώς να κάνετε OCR PDF σε Python – Οδηγός βήμα‑βήμα
url: /el/python-java/general/how-to-ocr-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να κάνετε OCR PDF σε Python – Οδηγός βήμα‑βήμα

Έχετε αναρωτηθεί ποτέ **πώς να κάνετε OCR PDF** όταν το αρχείο είναι απλώς μια εικόνα μιας σελίδας; Δεν είστε μόνοι. Σε αυτό το tutorial θα περάσουμε από τα ακριβή βήματα για OCR αρχείων PDF, εξαγωγή κειμένου από PDF, και μετατροπή ενός σαρωμένου PDF σε αναζητήσιμο κείμενο—όλα με απλό κώδικα Python.

Θα καλύψουμε τα πάντα, από την εγκατάσταση της βιβλιοθήκης Aspose OCR μέχρι την εξαγωγή του αναγνωρισμένου κειμένου από κάθε σελίδα. Στο τέλος θα μπορείτε να **OCR PDF με Python**, **εξάγετε κείμενο από PDF**, και **μετατρέψετε σαρωμένο PDF σε κείμενο** χωρίς να ψάχνετε σε διάσπαρτη τεκμηρίωση. Χωρίς περιττές πληροφορίες, μόνο ένα πρακτικό, εκτελέσιμο παράδειγμα που μπορείτε να αντιγράψετε‑επικολλήσετε.

## Τι Θα Χρειαστεί

* Python 3.8+ (η πιο πρόσφατη σταθερή έκδοση λειτουργεί καλύτερα)  
* Μια άδεια Aspose OCR for Python ή ένα δωρεάν κλειδί δοκιμής – μπορείτε να το αποκτήσετε από τον ιστότοπο της Aspose.  
* Ένα σαρωμένο PDF που θέλετε να επεξεργαστείτε (θα το ονομάσουμε `input.pdf`).  

Αν τα έχετε ήδη, υπέροχα—ας ξεκινήσουμε. Αν όχι, η εγκατάσταση του πακέτου είναι πανεύκολη και θα σας δείξουμε πώς.

## Πώς να κάνετε OCR PDF – Ρύθμιση του Περιβάλλοντος

Το πρώτο πράγμα που πρέπει να κάνετε είναι να αποκτήσετε το module Aspose OCR στον υπολογιστή σας. Το πακέτο ονομάζεται `aspose-ocr`, και μπορείτε να το εγκαταστήσετε μέσω pip:

```bash
pip install aspose-ocr
```

> **Συμβουλή:** Χρησιμοποιήστε ένα εικονικό περιβάλλον (`python -m venv venv`) ώστε οι εξαρτήσεις σας να παραμένουν οργανωμένες.

Μόλις εγκατασταθεί το πακέτο, είστε έτοιμοι να το εισάγετε και να ξεκινήσετε τη μηχανή OCR. Αυτό αποτελεί τη βάση για κάθε ροή εργασίας **ocr pdf with python** που θα δημιουργήσετε αργότερα.

## OCR PDF με Python – Εισαγωγή του Aspose OCR

Τώρα που η βιβλιοθήκη είναι διαθέσιμη, ας την φέρουμε στο script μας. Θα ορίσουμε επίσης τη μηχανή να λειτουργεί σε *direct PDF mode*, το οποίο λέει στο Aspose να διαβάζει τα bytes του PDF απευθείας από το αρχείο αντί να μετατρέπει κάθε σελίδα σε εικόνα πρώτα.

```python
# Step 1: Import the Aspose OCR module
import aspose.ocr as aocr

# Step 2: Create an OCR engine instance and enable direct PDF processing
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
```

Γιατί να χρησιμοποιήσετε το `PdfMode.DIRECT`; Επειδή παραλείπει ένα επιπλέον βήμα rasterization, κάνοντας τη διαδικασία πιο γρήγορη και διατηρώντας την αρχική διάταξη—ιδιαίτερα χρήσιμο όταν χρειάζεται να **recognize text from PDF** με ακρίβεια.

## Αναγνώριση Κειμένου από PDF – Εκτέλεση της Μηχανής

Με τη μηχανή έτοιμη, στοχεύστε τη στο σαρωμένο αρχείο σας. Η μέθοδος `recognize_from_pdf` κάνει όλη τη βαριά δουλειά: αναλύει κάθε σελίδα, εκτελεί τον αλγόριθμο OCR, και επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει μια συλλογή από αντικείμενα `Page`.

```python
# Step 3: Define the path to the PDF you want to process
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# Step 4: Perform OCR on the PDF and obtain the result object
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)
```

Αν αναρωτιέστε αν αυτό λειτουργεί με κρυπτογραφημένα PDF—ναι, εφόσον παρέχετε τον κωδικό μέσω `ocr_engine.password = "secret"` πριν καλέσετε το `recognize_from_pdf`. Αυτό είναι μια ειδική περίπτωση που παραλείπουν πολλά tutorials, αλλά είναι χρήσιμη σε πραγματικές γραμμές επεξεργασίας.

## Εξαγωγή Κειμένου από PDF – Πρόσβαση στα Αποτελέσματα Σελίδας

Η λίστα `ocr_result.pages` περιέχει μία εγγραφή ανά σελίδα. Κάθε αντικείμενο `Page` έχει μια ιδιότητα `.text` που περιέχει την απλή κειμενική αναπαράσταση της σαρωμένης σελίδας. Ας κάνουμε βρόχο και να εκτυπώσουμε τα αποτελέσματα ώστε να δείτε ακριβώς τι εξήχθη.

```python
# Step 5: Iterate through each page and display the recognized text
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)
```

Η εκτέλεση του script θα εμφανίσει κάτι όπως:

```
PDF OCR complete. Text per page:
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Αυτή η έξοδος αποδεικνύει ότι έχετε εξάγει με επιτυχία **extract text from PDF** και **recognize text from PDF** χρησιμοποιώντας το Aspose OCR. Τώρα μπορείτε να μεταφέρετε τις συμβολοσειρές σε μια βάση δεδομένων, έναν δείκτη αναζήτησης ή οποιοδήποτε επόμενο pipeline NLP.

![παράδειγμα ocr pdf](placeholder-image.png "παράδειγμα ocr pdf")

*Κείμενο εναλλακτικής εικόνας:* **παράδειγμα ocr pdf** – εμφανίζει την έξοδο της κονσόλας με το αναγνωρισμένο κείμενο ανά σελίδα.

## Μετατροπή Σαρωμένου PDF σε Κείμενο – Αποθήκευση του Αποτελέσματος

Οι περισσότεροι προγραμματιστές δεν θέλουν μόνο να βλέπουν το κείμενο στην κονσόλα· χρειάζονται ένα μόνιμο αρχείο. Παρακάτω υπάρχει ένας μικρός βοηθός που γράφει το κείμενο κάθε σελίδας σε ξεχωριστό αρχείο `.txt`, μετατρέποντας ουσιαστικά **convert scanned PDF to text** σε έναν φάκελο που ονομάζεται `output`.

```python
import os

output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

Μετά το τέλος του script θα έχετε έναν τακτοποιημένο φάκελο:

```
output_text/
│─ page_1.txt
│─ page_2.txt
└─ …
```

Τώρα έχετε ολοκληρώσει πλήρως το **convert scanned PDF to text** και μπορείτε να τροφοδοτήσετε αυτά τα αρχεία σε οποιαδήποτε επόμενη διαδικασία—αναζήτηση, ανάλυση, ή ακόμη και ένα απλό `grep`.

## Συχνές Ερωτήσεις & Ειδικές Περιπτώσεις

**Τι γίνεται αν το PDF μου περιέχει εικόνες αναμεμειγμένες με πραγματικό κείμενο;**  
Το Aspose OCR θα προσπαθήσει να αναγνωρίσει τα πάντα, αλλά μπορείτε να επιταχύνετε τη διαδικασία απενεργοποιώντας το OCR για σελίδες που ήδη περιέχουν επιλέξιμο κείμενο. Ορίστε `ocr_engine.auto_detect_page_orientation = True` και στη συνέχεια καλέστε `ocr_engine.recognize_from_pdf(..., detect_text=False)` για τις σελίδες που είναι γνωστές ως καλές.

**Μπορώ να ελέγξω το μοντέλο γλώσσας;**  
Απόλυτα. Ορίστε `ocr_engine.language = aocr.Language.English` (ή οποιαδήποτε υποστηριζόμενη γλώσσα) πριν καλέσετε το `recognize_from_pdf`. Αυτό βελτιώνει την ακρίβεια για έγγραφα μη‑Αγγλικής γλώσσας.

**Πώς να διαχειριστώ πολύ μεγάλα PDF (100+ σελίδες);**  
Επεξεργαστείτε τα σε τμήματα. Η μέθοδος `recognize_from_pdf` δέχεται ένα όρισμα `page_range`, π.χ., `ocr_engine.recognize_from_pdf(path, page_range=(1, 20))`. Κάντε βρόχο πάνω από τα εύρη για να διατηρήσετε τη χρήση μνήμης χαμηλή.

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι ένα ενιαίο script που μπορείτε να αποθηκεύσετε σε ένα αρχείο με όνομα `ocr_pdf.py` και να το εκτελέσετε:

```python
import os
import aspose.ocr as aocr

# -------------------------------------------------
# 1️⃣  Initialize the OCR engine (direct PDF mode)
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
# Optional: set language for better accuracy
ocr_engine.language = aocr.Language.English

# -------------------------------------------------
# 2️⃣  Path to the scanned PDF you want to process
# -------------------------------------------------
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# -------------------------------------------------
# 3️⃣  Run OCR – this is where we actually recognize text from PDF
# -------------------------------------------------
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)

# -------------------------------------------------
# 4️⃣  Print the extracted text (shows how to extract text from PDF)
# -------------------------------------------------
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)

# -------------------------------------------------
# 5️⃣  Save each page as a .txt file (convert scanned PDF to text)
# -------------------------------------------------
output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

Τρέξτε το με:

```bash
python ocr_pdf.py
```

Θα πρέπει να δείτε την έξοδο της κονσόλας που επιβεβαιώνει το κείμενο κάθε σελίδας και τη θέση των αποθηκευμένων αρχείων `.txt`.

## Συμπέρασμα

Καλύψαμε **πώς να κάνετε OCR PDF** χρησιμοποιώντας Python, παρουσιάσαμε έναν καθαρό τρόπο **ocr pdf with python**, σας δείξαμε πώς να **extract text from PDF**, εξηγήσαμε τη λειτουργία του **recognize text from PDF**, και τελικά δώσαμε ένα έτοιμο προς χρήση snippet που **convert scanned PDF to text**. Η όλη διαδικασία είναι ολοκληρωμένη

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}