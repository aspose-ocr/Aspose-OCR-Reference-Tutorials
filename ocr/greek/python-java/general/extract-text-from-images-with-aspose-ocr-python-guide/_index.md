---
category: general
date: 2026-03-18
description: Μάθετε πώς να εξάγετε κείμενο από εικόνες και να μετατρέπετε το κείμενο
  σαρωμένων εικόνων σε επεξεργάσιμες συμβολοσειρές χρησιμοποιώντας το Aspose OCR σε
  Python. Περιλαμβάνεται κώδικας βήμα‑βήμα.
draft: false
keywords:
- extract text from images
- convert scanned images text
- Aspose OCR Python
- batch OCR processing
- image to text conversion
language: el
og_description: Εξάγετε κείμενο από εικόνες χρησιμοποιώντας το Aspose OCR σε Python.
  Αυτό το σεμινάριο δείχνει πώς να μετατρέψετε το κείμενο σαρωμένων εικόνων με λίγες
  μόνο γραμμές κώδικα.
og_title: Εξαγωγή κειμένου από εικόνες με το Aspose OCR – Οδηγός Python
tags:
- OCR
- Python
- Aspose
- Image Processing
title: Εξαγωγή κειμένου από εικόνες με το Aspose OCR – Οδηγός Python
url: /el/python-java/general/extract-text-from-images-with-aspose-ocr-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Εικόνες με Aspose OCR – Οδηγός Python

Έχετε ποτέ χρειαστεί να **εξάγετε κείμενο από εικόνες** αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είστε ο μόνος—οι προγραμματιστές αντιμετωπίζουν συνεχώς το πρόβλημα του να μετατρέπουν σαρωμένα PDF, θορυβώδεις στιγμιότυπα οθόνης ή φωτογραφημένα αποδείξεις σε αναζητήσιμες, επεξεργάσιμες συμβολοσειρές.  

Τα καλά νέα; Με το Aspose OCR για Python μπορείτε να **μετατρέψετε κείμενο από σαρωμένες εικόνες** μαζικά, χωρίς να βγείτε από το IDE σας. Σε αυτόν τον οδηγό θα περάσουμε από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που δείχνει ακριβώς πώς να το κάνετε, γιατί κάθε βήμα είναι σημαντικό και τι πρέπει να προσέξετε.

## Τι Θα Μάθετε

- Ρυθμίστε τη βιβλιοθήκη Aspose OCR σε περιβάλλον Python.  
- Προετοιμάστε μια λίστα αρχείων εικόνας (PNG, JPG, TIFF κ.λπ.).  
- Εκτελέστε batch OCR με μία κλήση μεθόδου.  
- Πρόσβαση και εμφάνιση του εξαγόμενου κειμένου για κάθε αρχείο.  
- Διαχείριση κοινών προβλημάτων όπως μη υποστηριζόμενες μορφές και χρήση μνήμης για μεγάλα αρχεία.  

Στο τέλος, θα έχετε ένα επαναχρησιμοποιήσιμο script που μπορεί να **εξάγει κείμενο από εικόνες** κατ' απαίτηση—ιδανικό για αυτοματοποίηση εισαγωγής δεδομένων, ευρετηρίαση εγγράφων ή τροφοδοσία επόμενων pipelines NLP.

![Παράδειγμα εξαγωγής κειμένου από εικόνες](/images/ocr-extract-text.png "εξαγωγή κειμένου από εικόνες")

*Κείμενο εναλλακτικής εικόνας: “εξαγωγή κείμενου από εικόνες χρησιμοποιώντας Aspose OCR σε Python”*

## Προαπαιτούμενα

- Python 3.8 ή νεότερο (ο κώδικας χρησιμοποιεί f‑strings).  
- Ένα έγκυρο άδεια χρήσης Aspose OCR για Python ή κλειδί δοκιμής δωρεάν.  
- Οι εικόνες που θέλετε να επεξεργαστείτε αποθηκευμένες τοπικά (οποιοσδήποτε συνδυασμός PNG, JPG ή TIFF).  

Αν έχετε ήδη ένα εικονικό περιβάλλον, τέλεια—αν όχι, δημιουργήστε ένα με:

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate
```

Τώρα είστε έτοιμοι να εγκαταστήσετε το SDK.

## Βήμα 1: Εγκατάσταση του Aspose OCR SDK

Η Aspose διανέμει τη μηχανή OCR μέσω PyPI, έτσι μια εντολή `pip` κάνει τη δουλειά:

```bash
pip install aspose-ocr
```

> **Συμβουλή:** Καθορίστε την έκδοση (π.χ., `aspose-ocr==22.12`) για να αποφύγετε απρόσμενες αλλαγές που σπάζουν τη λειτουργία αργότερα.

## Βήμα 2: Εισαγωγή της Κλάσης OCR Engine

Η βασική κλάση με την οποία θα αλληλεπιδράτε είναι `OcrEngine`. Εισάγετέ την στην αρχή του script σας:

```python
# Step 2: Import the OCR engine class
from asposeocr import OcrEngine
```

> *Γιατί είναι σημαντικό:* Η εισαγωγή μόνο των απαραίτητων κρατάει το χρόνο εκκίνησης χαμηλό, ειδικά όταν αργότερα ενσωματώσετε το script σε μεγαλύτερη εφαρμογή.

## Βήμα 3: Ορισμός των Αρχείων Εικόνας για Επεξεργασία

Δημιουργήστε μια λίστα Python που περιέχει τις πλήρεις διαδρομές σε κάθε εικόνα που θέλετε να σαρώσετε. Αντικαταστήστε το `YOUR_DIRECTORY` με την πραγματική διαδρομή φακέλου.

```python
# Step 3: Define the image files to be processed
image_files = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.jpg",
    "YOUR_DIRECTORY/page3.tif"
]
```

> **Ακραία περίπτωση:** Αν έχετε εκατοντάδες αρχεία, σκεφτείτε να δημιουργήσετε αυτή τη λίστα προγραμματιστικά με `glob.glob('*.png')` για να αποφύγετε χειροκίνητες επεμβάσεις.

## Βήμα 4: Εκτέλεση OCR σε Όλες τις Εικόνες Μαζί

Το Aspose OCR παρέχει μια βολική μέθοδο `processMultiple` που επιστρέφει μια λίστα αντικειμένων `OcrResult`—ένα για κάθε αρχείο εισόδου.

```python
# Step 4: Run OCR on all images at once
ocr_engine = OcrEngine()               # instantiate the engine
ocr_results = ocr_engine.processMultiple(image_files)
```

> *Γιατί η επεξεργασία παρτίδας;* Η αποστολή κάθε εικόνας ξεχωριστά προκαλεί επιπλέον επιβάρυνση (αρχικοποίηση της μηχανής, φόρτωση εγγενών βιβλιοθηκών). Η κλήση παρτίδας μειώνει το φορτίο CPU και επιταχύνει τη συνολική εργασία.

### Διαχείριση Σφαλμάτων με Ευγένεια

Αν μια εικόνα δεν μπορεί να διαβαστεί (κατεστραμμένο αρχείο, μη υποστηριζόμενη μορφή), το `processMultiple` θα ρίξει μια εξαίρεση. Τυλίξτε την κλήση σε ένα μπλοκ `try/except` για να κρατήσετε το script ζωντανό:

```python
try:
    ocr_results = ocr_engine.processMultiple(image_files)
except Exception as e:
    print(f"⚠️ OCR failed: {e}")
    ocr_results = []   # fallback to empty list
```

## Βήμα 5: Εξαγωγή του Εξαχθέντος Κειμένου για Κάθε Αρχείο

Επανάληψη πάνω στα αποτελέσματα, συνδυάζοντας κάθε `OcrResult` με το αρχικό όνομα αρχείου. Η μέθοδος `getText()` επιστρέφει τη αναγνωρισμένη συμβολοσειρά.

```python
# Step 5: Output the extracted text for each file
for index, result in enumerate(ocr_results, start=1):
    file_path = image_files[index - 1]
    print(f"--- Text from file {file_path} ---")
    print(result.getText())
    print("\n")   # add a blank line for readability
```

### Αναμενόμενη Έξοδος

Η εκτέλεση του πλήρους script σε τρία απλά στιγμιότυπα οθόνης μπορεί να παράγει κάτι όπως:

```
--- Text from file YOUR_DIRECTORY/page1.png ---
Invoice #12345
Date: 2024‑07‑01
Total: $256.78

--- Text from file YOUR_DIRECTORY/page2.jpg ---
Welcome to the Annual Report
Prepared by: Finance Dept.

--- Text from file YOUR_DIRECTORY/page3.tif ---
© 2025 Acme Corp. All rights reserved.
```

Αν μια εικόνα δεν περιέχει αναγνωρίσιμους χαρακτήρες, θα δείτε μια κενή συμβολοσειρά—δεν σπάει τίποτα, και μπορείτε να αποφασίσετε αν θα σημαδέψετε το αρχείο για χειροκίνητη ανασκόπηση.

## Bonus: Βελτιστοποίηση της Ακρίβειας OCR

Το Aspose OCR προσφέρει αρκετές προαιρετικές ρυθμίσεις που ίσως θέλετε να δοκιμάσετε:

| Ρύθμιση | Τι Κάνει | Πότε να Χρησιμοποιηθεί |
|---------|----------|------------------------|
| `ocr_engine.setLanguage('eng')` | Εξαναγκάζει το μοντέλο αγγλικής γλώσσας (μειώνει ψευδείς θετικές). | Κυρίως αγγλικά έγγραφα. |
| `ocr_engine.setResolution(300)` | Βελτιώνει την ακρίβεια σε σαρώσεις χαμηλής ανάλυσης (dpi). | Σαρώσεις κάτω από 200 dpi. |
| `ocr_engine.setPageSegMode('single_block')` | Θεωρεί όλη την εικόνα ως ένα μπλοκ κειμένου. | Απλές αποδείξεις ή ταυτότητες. |

Μπορείτε να προσθέσετε αυτές τις γραμμές αμέσως μετά τη δημιουργία του `ocr_engine`:

```python
ocr_engine.setLanguage('eng')
ocr_engine.setResolution(300)
ocr_engine.setPageSegMode('single_block')
```

## Συνηθισμένα Προβλήματα & Πώς να τα Αποφύγετε

1. **Μεγάλα TIFF στοίβες** – Ένα πολυ-σελίδων TIFF μπορεί να καταναλώσει gigabytes μνήμης RAM όταν φορτώνεται ολόκληρο. Διαχωρίστε το αρχείο σε εικόνες μονής σελίδας πριν το δώσετε στο `processMultiple`.  
2. **Μη λατινικά αλφάβητα** – Αν χρειάζεται να **εξάγετε κείμενο από εικόνες** που περιέχουν κυριλλικούς, αραβικούς ή κινέζικους χαρακτήρες, αλλάξτε τον κωδικό γλώσσας ανάλογα (`'rus'`, `'ara'`, `'chi_sim'`).  
3. **Κενά στα μονοπάτια αρχείων** – Τα μονοπάτια των Windows με κενά μπορεί να προκαλέσουν `FileNotFoundError`. Τυλίξτε κάθε διαδρομή σε raw strings (`r"C:\\My Folder\\image.png"`) ή χρησιμοποιήστε `os.path.abspath`.  

Η αντιμετώπιση αυτών των ζητημάτων εκ των προτέρων σας εξοικονομεί ασαφείς σφάλματα χρόνου εκτέλεσης αργότερα.

---

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω είναι το πλήρες script που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε ένα αρχείο με όνομα `batch_ocr.py`. Περιλαμβάνει όλες τις βελτιώσεις βέλτιστων πρακτικών που συζητήθηκαν παραπάνω.

```python
# batch_ocr.py
# -------------------------------------------------
# Complete example: extract text from images using Aspose OCR (Python)
# -------------------------------------------------

from asposeocr import OcrEngine
import os

# -------------------------------------------------
# Configuration – adjust these values for your environment
# -------------------------------------------------
IMAGE_DIR = "YOUR_DIRECTORY"   # <-- replace with your folder path
SUPPORTED_EXT = (".png", ".jpg", ".jpeg", ".tif", ".tiff")

# Build a list of image file paths automatically
image_files = [
    os.path.join(IMAGE_DIR, f)
    for f in os.listdir(IMAGE_DIR)
    if f.lower().endswith(SUPPORTED_EXT)
]

if not image_files:
    print("⚠️ No supported image files found in the specified directory.")
    exit(1)

# -------------------------------------------------
# Initialize OCR engine with optional tweaks
# -------------------------------------------------
ocr_engine = OcrEngine()
ocr_engine.setLanguage('eng')          # English language model
ocr_engine.setResolution(300)          # Boost low‑dpi accuracy
ocr_engine.setPageSegMode('single_block')  # Treat whole image as one block

# -------------------------------------------------
# Run batch OCR and handle potential errors
# -------------------------------------------------
try:
    ocr_results = ocr_engine.processMultiple(image_files)
except Exception as exc:
    print(f"❌ OCR processing failed: {exc}")
    ocr_results = []

# -------------------------------------------------
# Display extracted text
# -------------------------------------------------
for idx, result in enumerate(ocr_results, start=1):
    file_path = image_files[idx - 1]
    print(f"--- Text from file {file_path} ---")
    print(result.getText())
    print("\n")
```

Αποθηκεύστε, ενεργοποιήστε το εικονικό σας περιβάλλον, και τρέξτε:

```bash
python batch_ocr.py
```

Θα πρέπει να δείτε τις εξαγόμενες συμβολοσειρές να εκτυπώνονται στην κονσόλα, έτοιμες για περαιτέρω επεξεργασία (π.χ., αποθήκευση σε βάση δεδομένων ή τροφοδοσία μοντέλου φυσικής γλώσσας).

---

## Συμπέρασμα

Σε αυτόν τον οδηγό δείξαμε πώς να **εξάγετε κείμενο από εικόνες** χρησιμοποιώντας Aspose OCR για Python, καλύπτοντας τα πάντα από την εγκατάσταση μέχρι την επεξεργασία παρτίδας και τη διαχείριση σφαλμάτων. Το script είναι συμπαγές, πλήρως λειτουργικό και εύκολο στην επέκταση—είτε χρειάζεστε να **μετατρέψετε κείμενο από σαρωμένες εικόνες** σε αρχεία CSV, να τροφοδοτήσετε έναν δείκτη αναζήτησης, ή απλώς να αυτοματοποιήσετε την εισαγωγή δεδομένων.

Έτοιμοι για το επόμενο βήμα; Σκεφτείτε να συνδυάσετε αυτή τη ροή OCR με έναν συγχωνευτή PDF για να δημιουργήσετε αναζητήσιμα PDF, ή να το ενσωματώσετε σε ένα trigger αποθήκευσης στο cloud ώστε κάθε ανεβασμένη σάρωση να επεξεργάζεται άμεσα. Ο ουρανός είναι το όριο, και τώρα έχετε μια σταθερή βάση για να χτίσετε.

Έχετε ερωτήσεις ή ιδέες για βελτίωση; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}