---
category: general
date: 2026-01-02
description: Μάθετε πώς να διορθώνετε την κλίση της εικόνας και να ενισχύετε την αντίθεση
  της εικόνας για να λαμβάνετε γρήγορα απλό κείμενο. Περιλαμβάνει βήμα‑βήμα κώδικα
  Python και συμβουλές για την εξαγωγή κειμένου.
draft: false
keywords:
- how to deskew image
- boost image contrast
- get plain text
- how to boost contrast
- how to extract text
language: el
og_description: Πώς να διορθώσετε την κλίση μιας εικόνας και να ενισχύσετε την αντίθεση
  για να αποκτήσετε απλό κείμενο. Πλήρες παράδειγμα Python με εξαγωγή πινάκων και
  επιτάχυνση GPU.
og_title: Πώς να διορθώσετε την κλίση εικόνας – Πλήρης οδηγός OCR με GPU
tags:
- OCR
- Python
- Image Processing
title: Πώς να διορθώσετε την κλίση της εικόνας – Οδηγός OCR με επιτάχυνση GPU
url: /el/python-java/general/how-to-deskew-image-gpu-accelerated-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Διορθώσετε την Κλίση μιας Εικόνας – Οδηγός OCR με Επιτάχυνση GPU

Έχετε αναρωτηθεί ποτέ **πώς να διορθώσετε την κλίση μιας εικόνας** όταν οι αποδείξεις σας έρχονται με αστεία γωνία; Δεν είστε μόνοι· μια κεκλιμένη φωτογραφία μπορεί να μετατρέψει μια τέλεια αναγνώσιμη απόδειξη σε ακατάστατο μπερδεμένο κείμενο. Τα καλά νέα είναι ότι με λίγες γραμμές Python μπορείτε να αυτο‑διορθώσετε την κλίση, να ενισχύσετε την αντίθεση και να εξάγετε καθαρό απλό κείμενο—χωρίς χειροκίνητο Photoshop.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, εκτελέσιμο παράδειγμα που όχι μόνο **πώς να διορθώσετε την κλίση μιας εικόνας** αλλά και δείχνει **πώς να ενισχύσετε την αντίθεση**, **πώς να λάβετε απλό κείμενο**, και ακόμη **πώς να εξάγετε κείμενο** από πίνακες που εντοπίζει η μηχανή OCR. Στο τέλος θα έχετε ένα αυτόνομο script που μπορείτε να ενσωματώσετε σε οποιοδήποτε project.

## Τι Θα Χρειαστείτε

- Python 3.9+ εγκατεστημένο (ο κώδικας χρησιμοποιεί type hints, οπότε ένας πρόσφατος διερμηνέας βοηθά)
- Η βιβλιοθήκη `ocr` που παρέχει `OcrEngine`, `EngineMode`, `ImageProcessingOptions` και `OcrResult` (εγκαταστήστε τη με `pip install ocr‑sdk` – αντικαταστήστε με το πραγματικό όνομα πακέτου που χρησιμοποιείτε)
- Μια GPU με συμβατούς οδηγούς αν θέλετε την επιτάχυνση ταχύτητας (προαιρετικό αλλά συνιστάται)
- Ένα αρχείο εικόνας που είναι ελαφρώς περιστραμμένο ή χαμηλής αντίθεσης, π.χ. `receipt_skewed.jpg`

> **Pro tip:** Αν δεν έχετε GPU, απλώς αλλάξτε το `EngineMode.GPU` σε `EngineMode.CPU` και το script θα λειτουργήσει—απλώς λίγο πιο αργά.

## Υλοποίηση Βήμα‑Βήμα

Παρακάτω χωρίζουμε τη λύση σε λογικά τμήματα. Κάθε τμήμα έχει ένα περιγραφικό **H2** που περιέχει είτε την κύρια λέξη‑κλειδί *πώς να διορθώσετε την κλίση μιας εικόνας* είτε μία από τις δευτερεύουσες λέξεις‑κλειδιά. Ο κώδικας είναι πλήρης, σχολιασμένος και έτοιμος για εκτέλεση.

### Πώς να Διορθώσετε την Κλίση μιας Εικόνας με OCR Επιταχυνόμενο από GPU

Το πρώτο που κάνουμε είναι να πούμε στη μηχανή OCR να τρέξει στην GPU και να ενεργοποιήσουμε τη λειτουργία auto‑deskew. Η auto‑deskew αναλύει τη γεωμετρία της εικόνας και την περιστρέφει πίσω στην όρθια θέση.

```python
# Import the required classes from the OCR SDK
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

# Step 1: Initialize the OCR engine with GPU acceleration
ocr_engine = OcrEngine()
ocr_engine.set_engine_mode(EngineMode.GPU)  # Enables GPU backend for faster processing
```

> **Why this matters:** Η επιτάχυνση GPU μπορεί να μειώσει το χρόνο επεξεργασίας από δευτερόλεπτα σε χιλιοστά του δευτερολέπτου, κάτι κρίσιμο όταν διαχειρίζεστε δεκάδες αποδείξεις ανά λεπτό.

### Ενίσχυση της Αντίθεσης της Εικόνας για Καλύτερη Αναγνώριση

Μια απόδειξη χαμηλής αντίθεσης είναι εφιάλτης για οποιοδήποτε σύστημα OCR. Με την ενίσχυση της αντίθεσης δίνουμε στη μηχανή πιο καθαρές άκρες για επεξεργασία.

```python
# Step 2: Configure image preprocessing (auto‑deskew and contrast boost)
processing_options = ImageProcessingOptions()
processing_options.set_auto_deskew(True)          # Corrects slight rotation
processing_options.set_contrast_boost(30)         # Improves readability
ocr_engine.set_image_processing_options(processing_options)
```

> **How to boost contrast:** Η μέθοδος `set_contrast_boost` δέχεται ένα ποσοστό· 30 % είναι μια ασφαλής προεπιλογή που λειτουργεί για τις περισσότερες σαρωμένες αποδείξεις. Αν οι εικόνες σας είναι εξαιρετικά σκοτεινές, αυξήστε το σε 50 % ή πειραματιστείτε.

### Λήψη Απλού Κειμένου από την Επεξεργασμένη Εικόνα

Τώρα που η εικόνα είναι ευθεία και φωτεινή, τη δίνουμε στη μηχανή και ζητάμε το αποτέλεσμα ως απλό κείμενο.

```python
# Step 3: Load the target image and perform OCR
image_path = "YOUR_DIRECTORY/receipt_skewed.jpg"
ocr_result: OcrResult = ocr_engine.recognize_image(image_path)

# Step 4: Output the recognized plain text
print("Detected text:")
print(ocr_result.get_text())
```

**Expected output** (truncated for brevity):

```
Detected text:
Store: Coffee Corner
Date: 2025-12-31
Item          Qty   Price
Latte          1    $3.50
Muffin         2    $5.00
Total                $8.50
```

> **How to get plain text:** Η μέθοδος `get_text()` αφαιρεί οποιαδήποτε πληροφορία διάταξης και επιστρέφει μια καθαρή συμβολοσειρά, την οποία μπορείτε να αποθηκεύσετε σε βάση δεδομένων, να στείλετε σε API ή να τροφοδοτήσετε σε επόμενες αναλύσεις.

### Πώς να Εξάγετε Κείμενο από Ανιχνευμένους Πίνακες

Συχνά οι αποδείξεις περιέχουν δεδομένα σε πίνακες (είδη, ποσότητες, τιμές). Το SDK OCR μπορεί να εντοπίσει πίνακες και να σας επιτρέψει να διατρέξετε γραμμές και κελιά.

```python
# Step 5: If tables are detected, print their contents
if ocr_result.get_tables():
    for idx, table in enumerate(ocr_result.get_tables()):
        print(f"\nTable {idx + 1}:")
        for row in table.get_rows():
            # Join each cell's text with a tab for easy copy‑paste
            print("\t".join(cell.get_text() for cell in row.get_cells()))
```

**Sample table output**:

```
Table 1:
Item	Qty	Price
Latte	1	$3.50
Muffin	2	$5.00
Total		$8.50
```

> **Why extract tables:** Τα δομημένα δεδομένα κάνουν την εκτίμηση συνολικών, τη δημιουργία αναφορών ή την ενσωμάτωση σε λογισμικό λογιστικής εξαιρετικά απλή.

### Πλήρες Λειτουργικό Script

Συνδυάζοντας τα πάντα, εδώ είναι το script που μπορείτε να αντιγράψετε‑επικολλήσετε στο `deskew_and_ocr.py`:

```python
# deskew_and_ocr.py
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

def main(image_path: str) -> None:
    # Initialize OCR engine with GPU acceleration
    ocr_engine = OcrEngine()
    ocr_engine.set_engine_mode(EngineMode.GPU)

    # Configure preprocessing: auto‑deskew + contrast boost
    opts = ImageProcessingOptions()
    opts.set_auto_deskew(True)
    opts.set_contrast_boost(30)  # Adjust if needed
    ocr_engine.set_image_processing_options(opts)

    # Perform OCR
    result: OcrResult = ocr_engine.recognize_image(image_path)

    # Print plain text
    print("Detected text:")
    print(result.get_text())

    # Print tables, if any
    if result.get_tables():
        for i, tbl in enumerate(result.get_tables(), start=1):
            print(f"\nTable {i}:")
            for row in tbl.get_rows():
                print("\t".join(cell.get_text() for cell in row.get_cells()))

if __name__ == "__main__":
    # Replace with your actual image location
    main("YOUR_DIRECTORY/receipt_skewed.jpg")
```

Τρέξτε το με:

```bash
python deskew_and_ocr.py
```

Θα πρέπει να δείτε το καθαρισμένο κείμενο και τυχόν ανιχνευμένους πίνακες να εκτυπώνονται στην κονσόλα.

## Συνηθισμένες Ακραίες Περιπτώσεις & Πώς να τις Διαχειριστείτε

| Situation | What to Do |
|-----------|------------|
| **Image is upside‑down** | Increase `set_auto_deskew(True)` confidence by also calling `set_rotation_correction(True)` if the SDK offers it. |
| **Contrast boost makes the image too bright** | Reduce the percentage passed to `set_contrast_boost` (e.g., 15 %). |
| **GPU not available** | Switch `EngineMode.GPU` to `EngineMode.CPU`; the rest of the pipeline remains unchanged. |
| **Tables are missed** | Try a higher resolution scan or enable `set_table_detection(True)` if the library provides it. |

## Επόμενα Βήματα: Από Απλό Κείμενο σε Δομημένα Δεδομένα

Τώρα που ξέρετε **πώς να διορθώσετε την κλίση μιας εικόνας**, **πώς να ενισχύσετε την αντίθεση** και **πώς να λάβετε απλό κείμενο**, μπορείτε να:

- Αναλύσετε το απλό κείμενο με κανονικές εκφράσεις για εξαγωγή ζευγών κλειδί‑τιμή (π.χ. `total`, `date`).
- Αποθηκεύσετε τα αποτελέσματα σε βάση δεδομένων SQLite ή PostgreSQL για μελλοντική αναφορά.
- Συνδέσετε το script σε serverless function (AWS Lambda, Azure Functions) για αυτόματη επεξεργασία ανεβάσματος.

Όλες αυτές οι επεκτάσεις βασίζονται στο ίδιο θεμέλιο που καλύψαμε εδώ.

## Συμπέρασμα

Διασχίσαμε **πώς να διορθώσετε την κλίση μιας εικόνας** χρησιμοποιώντας μια μηχανή OCR επιταχυνόμενη από GPU, δείξαμε **πώς να ενισχύσετε την αντίθεση** για πιο οξεία αναγνώριση, σας παρουσιάσαμε ακριβώς **πώς να λάβετε απλό κείμενο**, και ακόμη καλύψαμε **πώς να εξάγετε κείμενο** από πίνακες. Το πλήρες, εκτελέσιμο script ενώνει όλα τα παραπάνω, ώστε να το ενσωματώσετε σε οποιοδήποτε έργο Python και να αρχίσετε να εξάγετε καθαρά δεδομένα από κεκλιμένες, χαμηλής αντίθεσης φωτογραφίες αμέσως.

Δοκιμάστε το με μερικές από τις δικές σας αποδείξεις, ρυθμίστε το επίπεδο αντίθεσης, και αφήστε το OCR να κάνει το σκληρό έργο. Αν συναντήσετε δυσκολίες, επιστρέψτε στον πίνακα ακραίων περιπτώσεων παραπάνω—τα περισσότερα προβλήματα λύνουν με μια μικρή προσαρμογή.

Καλή προγραμματιστική δουλειά, και ας είναι οι εικόνες σας πάντα ευθείες και φωτεινές!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}