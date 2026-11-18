---
category: general
date: 2026-06-28
description: Πώς να κάνετε ομαδική OCR με τη χρήση της Python. Μάθετε πώς να κάνετε
  OCR σε πολλαπλές εικόνες, να εξάγετε κείμενο από PNG και να μετατρέψετε εικόνα σε
  κείμενο με ένα πλήρες σεμινάριο OCR σε Python.
draft: false
keywords:
- how to batch OCR
- ocr multiple images
- extract text from png
- convert image to text
- python ocr tutorial
language: el
og_description: Πώς να εκτελέσετε ομαδική OCR σε Python εξηγείται στην πρώτη πρόταση.
  Ακολουθήστε αυτό το σεμινάριο OCR σε Python για να εξάγετε κείμενο από αρχεία PNG
  αποδοτικά.
og_title: Πώς να εκτελέσετε μαζική OCR σε Python – Πλήρης οδηγός προγραμματισμού
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  headline: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  name: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  steps:
  - name: '**Why set the language?**'
    text: '**Why set the language?**'
  - name: '**Why use a batch operation?**'
    text: '**Why use a batch operation?**'
  - name: '**Why a ThreadPoolExecutor?**'
    text: '**Why a ThreadPoolExecutor?**'
  - name: '**Why enumerate the results?**'
    text: '**Why enumerate the results?**'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Πώς να κάνετε μαζική OCR σε Python – Πλήρης οδηγός βήμα‑βήμα
url: /el/python-java/general/how-to-batch-ocr-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να κάνετε Batch OCR σε Python – Πλήρης Οδηγός Βήμα‑βήμα

Έχετε αναρωτηθεί ποτέ **πώς να κάνετε batch OCR** σε μια στοίβα σαρωμένων σελίδων χωρίς να γράψετε έναν βρόχο που μπλοκάρει το UI σας; Δεν είστε ο μόνος. Η επεξεργασία δεκάδων αρχείων PNG ένα‑ένα μπορεί να μοιάζει με το να παρακολουθείτε το χρώμα να στεγνώνει, ειδικά όταν κάθε εικόνα χρειάζεται ένα ή δύο δευτερόλεπτα για αποκωδικοποίηση.  

Σε αυτό το tutorial θα σας δείξουμε έναν καθαρό, μη‑μπλοκαριστικό τρόπο για **OCR πολλαπλών εικόνων** ταυτόχρονα, **εξαγωγή κειμένου από PNG** αρχεία, και **μετατροπή εικόνας σε κείμενο** χρησιμοποιώντας μια σύγχρονη μηχανή OCR σε Python. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση script που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο – ιδανικό για ένα γρήγορο *python ocr tutorial* ή μια παραγωγική εργασία batch.

## Τι Θα Δημιουργήσετε

- Αρχικοποιήστε μια μηχανή OCR και ορίστε τη γλώσσα της σε Latin (ή οποιαδήποτε γλώσσα χρειάζεστε).  
- Παρέχετε μια λίστα διαδρομών εικόνων (PNG στο παράδειγμά μας) στη μηχανή.  
- Ξεκινήστε μια batch λειτουργία που επιστρέφει ένα αντικείμενο τύπου Future.  
- Ανακτήστε όλα τα αποτελέσματα ταυτόχρονα με ένα thread pool, διατηρώντας ελεύθερο το κύριο νήμα.  
- Εκτυπώστε το αναγνωρισμένο κείμενο για κάθε σελίδα, με ωραίο διαχωρισμό.

Δεν υπάρχει κρυφή μαγεία, μόνο απλή Python και μια τρίτη‑μεριά βιβλιοθήκη OCR (θα χρησιμοποιήσουμε το φανταστικό πακέτο `pyocr` για παράδειγμα).

**Προαπαιτούμενα**  
- Εγκατεστημένο Python 3.8+.  
- Βασική εξοικείωση με συναρτήσεις Python και `concurrent.futures`.  
- Πρόσβαση σε βιβλιοθήκη OCR που εκθέτει μια κλάση `OcrEngine` (π.χ., `pip install pyocr`).  

Αν λείπει κάποιο από αυτά, αποκτήστε το τώρα – είναι πιο εύκολο απ' ό,τι νομίζετε.

---

## Πώς να κάνετε Batch OCR σε Python – Βασικές Έννοιες

Πριν βουτήξουμε στον κώδικα, ας απαντήσουμε στο «γιατί» πίσω από κάθε βήμα.

1. **Γιατί να ορίσετε τη γλώσσα;**  
   Η ακρίβεια του OCR αυξάνεται εκθετικά όταν η μηχανή γνωρίζει ποιοι χαρακτήρες να περιμένει. Τα Latin λειτουργούν για Αγγλικά, Γαλλικά, Ισπανικά κ.λπ. Αλλάξτε σε `Language.Japanese` ή `Language.Arabic` αν χρειάζεται.

2. **Γιατί να χρησιμοποιήσετε μια batch λειτουργία;**  
   Μια κλήση batch επιτρέπει στη μηχανή να προγραμματίσει την εργασία εσωτερικά, συχνά αξιοποιώντας νήματα ή επιτάχυνση GPU. Επιστρέφει ένα χειριστή που μπορείτε να ερωτήσετε αργότερα, πράγμα που σημαίνει ότι δεν μπλοκάρετε ενώ κάθε εικόνα επεξεργάζεται.

3. **Γιατί ThreadPoolExecutor;**  
   Το αντικείμενο Future που λαμβάνουμε είναι *lazy* – ξεκινά να αντλεί αποτελέσματα μόνο όταν το ζητήσουμε. Με τη μεταβίβαση ενός thread pool στη `getAll`, επιτρέπουμε στην Python να ανακτά το κείμενο κάθε σελίδας παράλληλα, μειώνοντας δραστικά το συνολικό χρόνο εκτέλεσης.

4. **Γιατί να αριθμήσουμε (enumerate) τα αποτελέσματα;**  
   Η σειρά των αποτελεσμάτων ταιριάζει με τη σειρά των εισαγόμενων διαδρομών, ώστε να μπορούμε με ασφάλεια να ετικετοποιήσουμε κάθε αριθμό σελίδας.

Κατανοώντας αυτά τα «γιατί» σας βοηθά να προσαρμόσετε το μοτίβο σε άλλες βιβλιοθήκες ή σε μεγαλύτερα σύνολα δεδομένων.

## Βήμα 1: Εγκατάσταση και Εισαγωγή Απαιτούμενων Πακέτων

Πρώτα, βεβαιωθείτε ότι η βιβλιοθήκη OCR είναι εγκατεστημένη. Το παράδειγμα χρησιμοποιεί ένα γενικό πακέτο `pyocr`; αντικαταστήστε το με τη βιβλιοθήκη που προτιμάτε (π.χ., `pytesseract`, `easyocr`).

```bash
pip install pyocr
```

Τώρα εισάγουμε όλα όσα χρειαζόμαστε.

```python
# Standard library imports
import concurrent.futures
from pathlib import Path

# Third‑party OCR library (hypothetical)
from pyocr import OcrEngine, Language
```

> **Συμβουλή:** Η χρήση του `Path` από το `pathlib` κάνει το script σας ανεξάρτητο από το λειτουργικό σύστημα και πιο ευανάγνωστο.

## Βήμα 2: Δημιουργία Μηχανής OCR και Ορισμός Γλώσσας

Η δημιουργία της μηχανής είναι απλή. Θα την κλειδώσουμε σε Latin για αυτή τη demo.

```python
# Step 2: Initialise the OCR engine
engine = OcrEngine()
engine.setLanguage(Language.Latin)   # Change to Language.YourChoice if needed
```

Η κλήση `setLanguage` είναι προαιρετική για ορισμένες μηχανές, αλλά αποτελεί καλή πρακτική. Ενημερώνει το μοντέλο OCR να εστιάσει στο σύνολο χαρακτήρων που σας ενδιαφέρει, βελτιώνοντας τόσο την ταχύτητα όσο και την ακρίβεια.

## Βήμα 3: Καταγραφή Αρχείων Εικόνας για Επεξεργασία (Εξαγωγή Κειμένου από PNG)

Συλλέξτε όλα τα αρχεία PNG που θέλετε να μετατρέψετε. Η χρήση του `Path.glob` σημαίνει ότι μπορείτε να ρίξετε ολόκληρο φάκελο χωρίς να επεξεργαστείτε το script.

```python
# Step 3: Gather PNG images – this is the “extract text from png” part
image_dir = Path("YOUR_DIRECTORY")   # Replace with your actual folder
image_paths = sorted(image_dir.glob("*.png"))   # Returns a list of Path objects

# Convert Path objects to strings for the OCR library (if required)
image_paths = [str(p) for p in image_paths]

if not image_paths:
    raise FileNotFoundError("No PNG files found in the specified directory.")
```

> **Γιατί είναι σημαντικό:** Με την ταξινόμηση της λίστας εγγυόμαστε μια ντετερμινιστική σειρά, η οποία αργότερα ευθυγραμμίζει κάθε αποτέλεσμα με τον σωστό αριθμό σελίδας.

## Βήμα 4: Εκκίνηση Batch Λειτουργίας OCR (Μετατροπή Εικόνας σε Κείμενο)

Τώρα δίνουμε τη λίστα στη μηχανή. Η μέθοδος επιστρέφει ένα κοντέινερ τύπου Future που θα ελέγξουμε αργότερα.

```python
# Step 4: Start batch OCR – returns a Future‑like object
batch_future = engine.ocrBatch(image_paths)
```

Στο παρασκήνιο η μηχανή μπορεί να δημιουργήσει τα δικά της νήματα εργασίας ή ακόμη και μια γραμμή επεξεργασίας GPU. Το μόνο που μας ενδιαφέρει είναι ότι έχουμε ένα χειριστή (`batch_future`) που ξέρει πώς να ανακτά τα μεμονωμένα αποτελέσματα.

## Βήμα 5: Ανάκτηση Όλων των Αποτελεσμάτων Συγχρόνως (OCR Πολλαπλών Εικόνων)

Εδώ είναι που πραγματικά *batch* τη δουλειά. Δίνοντας ένα `ThreadPoolExecutor` στη `getAll`, το κείμενο κάθε σελίδας ανακτάται στο δικό του νήμα.

```python
# Step 5: Pull results using a thread pool – this speeds up OCR multiple images
with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    # getAll returns a list of Result objects in the same order as image_paths
    results = batch_future.getAll(executor)
```

Μπορείτε να ρυθμίσετε το `max_workers` βάσει των πυρήνων της CPU ή των συστάσεων της βιβλιοθήκης OCR. Περισσότεροι εργαζόμενοι ≠ πάντα πιο γρήγορο – παρακολουθήστε τη χρήση της CPU.

## Βήμα 6: Εμφάνιση του Αναγνωρισμένου Κειμένου (Τελευταίο Μέρος του Python OCR Tutorial)

Τέλος, εκτυπώστε το κείμενο κάθε σελίδας. Το αντικείμενο `Result` εκθέτει τη μέθοδο `getText()` – προσαρμόστε αν η βιβλιοθήκη σας χρησιμοποιεί διαφορετικό όνομα μεθόδου.

```python
# Step 6: Display the recognised text for each page
for i, result in enumerate(results):
    print(f"--- Page {i + 1} ---")
    print(result.getText())
    print()   # Blank line for readability
```

**Αναμενόμενη έξοδος (παράδειγμα)**

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna...

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco...
```

Αν κάποια εικόνα αποτύχει, οι περισσότερες μηχανές ενσωματώνουν μια κενή συμβολοσειρά ή ρίχνουν εξαίρεση – μπορείτε να τυλίξετε το βρόχο σε ένα μπλοκ `try/except` για να διαχειριστείτε τις ακραίες περιπτώσεις με χάρη.

## Πλήρες Script – Έτοιμο για Εκτέλεση

Παρακάτω βρίσκεται το πλήρες, αυτόνομο script. Αντιγράψτε‑και‑επικολλήστε το σε ένα αρχείο με όνομα `batch_ocr.py`, προσαρμόστε το `YOUR_DIRECTORY` και εκτελέστε `python batch_ocr.py`.

```python
#!/usr/bin/env python3
"""
Batch OCR script – processes all PNG files in a directory.
Demonstrates how to batch OCR, OCR multiple images, extract text from PNG,
and convert image to text using a Python OCR engine.
"""

import concurrent.futures
from pathlib import Path

# Replace with your actual OCR library import
from pyocr import OcrEngine, Language

def main():
    # Initialise OCR engine
    engine = OcrEngine()
    engine.setLanguage(Language.Latin)

    # Locate PNG files
    image_dir = Path("YOUR_DIRECTORY")          # <‑‑ change this
    image_paths = sorted(image_dir.glob("*.png"))
    image_paths = [str(p) for p in image_paths]

    if not image_paths:
        raise FileNotFoundError("No PNG files found in the specified directory.")

    # Start batch OCR
    batch_future = engine.ocrBatch(image_paths)

    # Retrieve results concurrently
    with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
        results = batch_future.getAll(executor)

    # Print each page's recognised text
    for i, result in enumerate(results):
        print(f"--- Page {i + 1} ---")
        print(result.getText())
        print()

if __name__ == "__main__":
    main()
```

Αποθηκεύστε, τρέξτε, και παρακολουθήστε την κονσόλα να γεμίζει με το εξαγόμενο κείμενο. Απλό, γρήγορο και πλήρως ασύγχρονο.

## Συνηθισμένα Προβλήματα & Πώς να τα Αποφύγετε

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Καμία έξοδος** – κενές συμβολοσειρές | Η μηχανή OCR δεν μπόρεσε να βρει κείμενο (εικόνα πολύ θορυβώδης) | Προεπεξεργασία εικόνων: δυαδικοποίηση, διόρθωση κλίσης ή αύξηση DPI |
| **FileNotFoundError** | Λάθος διαδρομή φακέλου ή ελλείποντα αρχεία PNG | Ελέγξτε ξανά το `YOUR_DIRECTORY` και βεβαιωθείτε ότι τα αρχεία λήγουν σε `.png` |
| **Υψηλή χρήση CPU** | `max_workers` ορισμένο πολύ υψηλά για το μηχάνημά σας | Μειώστε το `max_workers` ή ενεργοποιήστε επιτάχυνση GPU αν υποστηρίζεται |
| **Κακή κωδικοποίηση Unicode** | Η μηχανή προεπιλογή σε διαφορετική γλώσσα | Καλέστε `engine.setLanguage(Language.Latin)` (ή την κατάλληλη) πριν το batch OCR |

## Επέκταση του Tutorial – Επόμενα Βήματα

- **OCR πολλαπλών εικόνων** σε άλλες μορφές (JPEG, TIFF) – απλώς αλλάξτε το πρότυπο glob.  
- **Εξαγωγή κειμένου από PNG** και ενσωμάτωσή του σε ευρετήριο αναζήτησης (π.χ., Elasticsearch).  
- **Μετατροπή εικόνας σε κείμενο** για δημιουργία PDF χρησιμοποιώντας `reportlab` ή `PyPDF2`.  
- **Παραλληλοποίηση σε πολλαπλές μηχανές** με `multiprocessing` ή ουρά εργασιών όπως Celery για τεράστια σύνολα δεδομένων.  

## Συμπέρασμα

Διασχίσαμε πώς **να κάνετε batch OCR** σε μια συλλογή αρχείων PNG, δείξαμε τη δύναμη ενός API προσανατολισμένου σε batch, και σας δείξαμε πώς να **εξάγετε κείμενο από PNG** με προσέγγιση thread‑pool. Το πλήρες script παραπάνω είναι έτοιμο για παραγωγή, και τώρα έχετε μια σταθερή βάση για οποιοδήποτε έργο Python με έντονη χρήση OCR.

Δοκιμάστε το, προσαρμόστε τις ρυθμίσεις γλώσσας, και ίσως ακόμη αντικαταστήσετε το `pyocr` με `pytesseract` – το μοτίβο παραμένει το ίδιο. Έχετε ερωτήσεις ή θέλετε να μοιραστείτε μια ενδιαφέρουσα περίπτωση χρήσης; Αφήστε ένα σχόλιο και ας συνεχίσουμε τη συζήτηση.

*Καλό κώδικα!*

## Τι Θα Μάθετε Στη Σύντομη Μελλοντική;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε σε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Βήμα‑βήμα](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Εξαγωγή Κειμένου από Εικόνες Χρησιμοποιώντας Λειτουργία OCR σε Φακέλους](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Πώς να Κάνετε Batch OCR Εικόνων με Λίστα στο Aspose.OCR για .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}