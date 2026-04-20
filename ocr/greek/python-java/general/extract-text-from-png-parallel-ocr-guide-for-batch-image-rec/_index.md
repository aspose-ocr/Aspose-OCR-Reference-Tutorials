---
category: general
date: 2026-03-18
description: Εξαγωγή κειμένου από PNG χρησιμοποιώντας Python και Aspose OCR. Μάθετε
  πώς να φορτώνετε εικόνα για OCR, να εκτελείτε OCR σε πολλαπλά αρχεία και να επιτυγχάνετε
  μαζική OCR εικόνων με παράλληλη αναγνώριση εικόνας.
draft: false
keywords:
- extract text from png
- ocr multiple files
- batch ocr images
- load image for OCR
- parallel image recognition
language: el
og_description: Εξαγωγή κειμένου από PNG με το Aspose OCR σε Python. Αυτό το σεμινάριο
  δείχνει πώς να φορτώσετε εικόνα για OCR, να επεξεργαστείτε OCR πολλαπλά αρχεία και
  να εκτελέσετε μαζικό OCR εικόνων χρησιμοποιώντας παράλληλη αναγνώριση εικόνας.
og_title: Εξαγωγή κειμένου από PNG – Οδηγός Παράλληλης OCR
tags:
- OCR
- Python
- threading
- Aspose
- image-processing
title: Εξαγωγή κειμένου από PNG – Οδηγός Παράλληλου OCR για Ομαδική Αναγνώριση Εικόνων
url: /el/python-java/general/extract-text-from-png-parallel-ocr-guide-for-batch-image-rec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή κειμένου από PNG – Οδηγός Παράλληλης OCR για Μαζική Αναγνώριση Εικόνων

Έχετε ποτέ χρειαστεί να **εξάγετε κείμενο από PNG** αρχεία αλλά να έχετε κολλήσει στο σημείο όπου μια μόνο εικόνα χρειάζεται αιώνιες για να επεξεργαστεί; Δεν είστε μόνοι. Σε πολλά πραγματικά έργα—σκεφτείτε σαρωτές τιμολογίων, ψηφιοποιητές αποδείξεων ή εργαλεία αρχειοθέτησης—η ταχύτητα μετράει, και η επεξεργασία κάθε PNG ένα‑ένα δεν αρκεί.

Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα μια πλήρη, έτοιμη‑για‑εκτέλεση λύση που **φορτώνει εικόνα για OCR**, εκτελεί **ocr multiple files** με τρόπο **batch OCR images**, και αξιοποιεί **παράλληλη αναγνώριση εικόνας** με το `threading` module της Python. Στο τέλος θα έχετε ένα script που εξάγει κείμενο από οποιονδήποτε αριθμό PNG σε δευτερόλεπτα, όχι λεπτά.

## Τι Θα Χρειαστεί

- Python 3.8 ή νεότερη (η σύνταξη που φαίνεται λειτουργεί και σε 3.10+).  
- Το πακέτο Aspose OCR για Java/​Python (`aspose-ocr`). Μπορείτε να το εγκαταστήσετε μέσω `pip`.  
- Ένας φάκελος με μερικά PNG αρχεία που θέλετε να επεξεργαστείτε.  
- Μια μέτρια ποσότητα RAM—κάθε νήμα κρατά ένα μικρό στιγμιότυπο του OCR engine, έτσι ακόμη και ένα laptop μπορεί να δημιουργήσει δεκάδες εργαζόμενους.

Καμία εξωτερική υπηρεσία, κανένα κλειδί cloud, και κανένα μυστηριώδες αρχείο ρυθμίσεων. Μόνο καθαρός κώδικας Python που μπορείτε να αντιγράψετε‑επικολλήσετε και να εκτελέσετε.

## Γιατί να εξάγετε κείμενο από PNG παράλληλα;

Η επεξεργασία ενός PNG είναι περιορισμένη από την CPU: η μηχανή OCR εκτελεί μια σειρά αλγορίθμων ανάλυσης εικόνας που καταναλώνουν τα δεδομένα pixel. Όταν έχετε δέκα, είκοσι ή εκατό εικόνες, ο συνολικός χρόνος εκτέλεσης είναι ουσιαστικά το άθροισμα κάθε μεμονωμένης εκτέλεσης.

Δημιουργώντας ένα νήμα για κάθε αρχείο, αφήνουμε το λειτουργικό σύστημα να προγραμματίσει αυτές τις εργασίες βαριές σε CPU ταυτόχρονα. Σε ένα πολυπύρηνο μηχάνημα αυτό συχνά μειώνει στο μισό—ή ακόμη και στο τέταρτο—το πραγματικό χρόνο εκτέλεσης. Η ανταλλαγή είναι μια ελαφρώς μεγαλύτερη κατανάλωση μνήμης, αλλά για τις περισσότερες μαζικές εργασίες το κέρδος στην ταχύτητα αξίζει.

> **Συμβουλή:** Αν διαχειρίζεστε εκατοντάδες megabytes εικόνων, σκεφτείτε να χρησιμοποιήσετε το `concurrent.futures.ProcessPoolExecutor` αντί για το `threading`. Οι διεργασίες σας προσφέρουν πραγματικό παράλληλο επεξεργαστικό ισχύ στο GIL‑bound CPython interpreter, με κόστος λίγο μεγαλύτερης επιβάρυνσης.

## Βήμα 1: Εγκατάσταση Aspose OCR για Python

Πρώτα απ’ όλα—ας εγκαταστήσουμε τη βιβλιοθήκη OCR στο σύστημά σας.

```bash
pip install aspose-ocr
```

Αυτή η μοναδική γραμμή κατεβάζει τα πιο πρόσφατα δυαδικά αρχεία Aspose OCR και τις Python bindings του. Αν αντιμετωπίσετε σφάλμα δικαιωμάτων, δοκιμάστε να προσθέσετε `--user` ή να χρησιμοποιήσετε ένα εικονικό περιβάλλον.

## Βήμα 2: Φόρτωση εικόνας για OCR – η λειτουργία εργαζόμενου

Τώρα ορίζουμε τη βασική ρουτίνα που θα εκτελείται σε κάθε νήμα. Αυτή **φορτώνει εικόνα για OCR**, εκτελεί την αναγνώριση και εκτυπώνει μια προεπισκόπηση του εξαγόμενου κειμένου.

```python
import threading
from asposeocrjava import OcrEngine, OcrResult

def ocr_task(image_path: str):
    """
    Loads a PNG, runs OCR, and prints the first 100 characters of the result.
    Each thread creates its own OcrEngine instance to avoid state clashes.
    """
    # Initialise a fresh engine – this is cheap and thread‑safe.
    engine = OcrEngine()
    # Load image for OCR
    engine.setImageFromFile(image_path)

    # Perform the recognition – this is the CPU‑intensive part.
    result: OcrResult = engine.recognize()

    # Show a preview of the recognized text (first 100 characters)
    preview = result.getText()[:100].replace("\n", " ")
    print(f"[{image_path}] -> {preview}...")
```

- **Γιατί ένα νέο `OcrEngine` ανά νήμα;** Η μηχανή κρατά εσωτερικές προσωρινές μνήμες· η κοινή χρήση ενός αντικειμένου θα προκαλούσε συνθήκες αγώνα και ακατάστατο αποτέλεσμα.  
- **Γιατί αφαιρούνται τα newline;** Όταν καταγράφουμε στην κονσόλα διατηρεί τη γραμμή καθαρή.  
- **Διαχείριση σφαλμάτων;** Σε παραγωγή θα τυλίγατε το σώμα σε `try/except` και ίσως να καταγράφετε σε αρχείο—κάτι που θα καλύψουμε αργότερα.

## Βήμα 3: Καταγραφή των PNG αρχείων που θέλετε να επεξεργαστείτε

Θα μπορούσατε να κωδικοποιήσετε τη λίστα, αλλά μια πιο ευέλικτη προσέγγιση είναι η σάρωση ενός καταλόγου. Παρακάτω παραθέτουμε χειροκίνητα τρία αρχεία για σαφήνεια· αντικαταστήστε τις διαδρομές με το δικό σας φάκελο.

```python
image_files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png"
]
```

Αν προτιμάτε αυτόματη ανακάλυψη:

```python
import pathlib

image_dir = pathlib.Path("YOUR_DIRECTORY")
image_files = sorted(str(p) for p in image_dir.glob("*.png"))
```

Αυτή η μικρή τροποποίηση σας επιτρέπει να **εξάγετε κείμενο από PNG** αρχεία μαζικά χωρίς να τροποποιείτε τον πηγαίο κώδικα κάθε φορά.

## Βήμα 4: Ρύθμιση ocr multiple files με batch OCR images

Τώρα δημιουργούμε ένα νήμα για κάθε εικόνα. Αυτό είναι η καρδιά του προτύπου **batch OCR images**.

```python
# Create a thread for each image to run OCR concurrently
thread_list = [
    threading.Thread(target=ocr_task, args=(path,))
    for path in image_files
]
```

Η λίστα κατανόησης (list comprehension) διατηρεί τον κώδικα σύντομο, και κάθε αντικείμενο `Thread` αποθηκεύει τη λειτουργία-στόχο και το όρισμά του (`image_path`).

> **Σημείωση:** Το `threading` module της Python χρησιμοποιεί εγγενή νήματα του λειτουργικού συστήματος, έτσι σε ένα 4‑πυρήνων laptop συνήθως θα δείτε μέχρι τέσσερα νήματα να εκτελούνται πραγματικά ταυτόχρονα· τα υπόλοιπα θα προγραμματιστούν καθώς οι πυρήνες γίνονται ελεύθεροι.

## Βήμα 5: Εκτέλεση παράλληλης αναγνώρισης εικόνας

Η εκκίνηση των εργατών είναι απλή: επαναλάβετε τη λίστα και καλέστε `start()`. Στη συνέχεια περιμένουμε κάθε νήμα να ολοκληρωθεί χρησιμοποιώντας `join()`.

```python
# Step 5: Start all threads
for thread in thread_list:
    thread.start()

# Step 6: Wait for every thread to finish before exiting
for thread in thread_list:
    thread.join()
```

Όταν το script ολοκληρωθεί, θα δείτε μια σειρά γραμμών όπως:

```
[YOUR_DIRECTORY/doc1.png] -> Invoice #12345 Date: 2024-07-01 Total: $...
[YOUR_DIRECTORY/doc2.png] -> Receipt from Store XYZ Items: 3 Subtotal: $...
[YOUR_DIRECTORY/doc3.png] -> ...
```

Αυτή η έξοδος επιβεβαιώνει ότι κάθε PNG επεξεργάστηκε και το εξαγόμενο κείμενο είναι διαθέσιμο για περαιτέρω επεξεργασία (π.χ., αποθήκευση σε βάση δεδομένων ή τροφοδοσία σε pipeline NLP).

## Βήμα 6: Επαλήθευση των αποτελεσμάτων και διαχείριση ειδικών περιπτώσεων

### Έλεγχος για κενά αποτελέσματα

Μερικές φορές μια εικόνα είναι πολύ θορυβώδης, ή η μηχανή OCR δεν εντοπίζει κανέναν χαρακτήρα. Μια γρήγορη επαλήθευση μπορεί να σας προστατεύσει από σφάλματα σε επόμενα βήματα.

```python
def ocr_task(image_path: str):
    engine = OcrEngine()
    engine.setImageFromFile(image_path)

    result: OcrResult = engine.recognize()
    text = result.getText().strip()

    if not text:
        print(f"[{image_path}] -> No text detected.")
    else:
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")
```

### Περιορισμός του αριθμού ταυτόχρονων νημάτων

Αν το τρέξετε σε ένα μέτριο VM, η δημιουργία εκατοντάδων νημάτων μπορεί να υπερφορτώσει το scheduler. Μπορείτε να περιορίσετε τη σύγχρονη εκτέλεση με ένα semaphore:

```python
max_workers = 8
sema = threading.Semaphore(max_workers)

def ocr_task(image_path: str):
    with sema:
        # ... same body as before ...
```

### Αποθήκευση αποτελεσμάτων σε αρχείο

Αντί για εκτύπωση, ίσως θέλετε ένα CSV με το όνομα αρχείου και το εξαγόμενο κείμενο:

```python
import csv
output_path = "ocr_results.csv"

with open(output_path, "w", newline="", encoding="utf-8") as csvfile:
    writer = csv.writer(csvfile)
    writer.writerow(["filename", "extracted_text"])

    def ocr_task(image_path: str):
        engine = OcrEngine()
        engine.setImageFromFile(image_path)
        text = engine.recognize().getText().strip()
        writer.writerow([image_path, text])
```

Βεβαιωθείτε ότι ανοίγετε το CSV **μία φορά** εκτός της λειτουργίας του νήματος για να αποφύγετε συνθήκες αγώνα· ο writer του `csv` module είναι thread‑safe για απλές εγγραφές.

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα, εδώ είναι ένα ενιαίο script που μπορείτε να αποθηκεύσετε σε αρχείο με όνομα `batch_ocr.py` και να το εκτελέσετε:

```python
import threading
import pathlib
import csv
from asposeocrjava import OcrEngine, OcrResult

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_DIR = pathlib.Path("YOUR_DIRECTORY")   # <-- change this
OUTPUT_CSV = "ocr_results.csv"
MAX_WORKERS = 8                               # adjust based on your CPU

# ----------------------------------------------------------------------
# Helper: OCR worker
# ----------------------------------------------------------------------
sema = threading.Semaphore(MAX_WORKERS)

def ocr_task(image_path: str, writer):
    """
    Extract text from a single PNG using Aspose OCR.
    This function is designed to run inside a thread.
    """
    with sema:                     # limit concurrent threads
        engine = OcrEngine()
        engine.setImageFromFile(image_path)

        result: OcrResult = engine.recognize()
        text = result.getText().strip()

        # Write to CSV (thread‑safe because writer is shared)
        writer.writerow([image_path, text])

        # Also print a short preview for quick debugging
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")

# ----------------------------------------------------------------------
# Main routine
# ----------------------------------------------------------------------
def main():
    # Discover all PNG files
    image_files = sorted(str(p) for p in IMAGE_DIR.glob("*.png"))
    if not image_files:
        print("No PNG files found in", IMAGE_DIR)
        return

    # Open CSV once, share the writer with all threads
    with open(OUTPUT_CSV, "w", newline="", encoding="utf-8") as csvfile:
        writer = csv.writer(csvfile)
        writer.writerow(["filename", "extracted_text"])

        # Create a thread for each image
        threads = [
            threading.Thread(target=ocr_task, args=(path, writer))
            for path in image_files

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}