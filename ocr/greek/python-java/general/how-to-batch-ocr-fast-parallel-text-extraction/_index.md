---
category: general
date: 2026-03-26
description: πώς να εκτελείτε μαζική OCR αποδοτικά με Python — μάθετε να εξάγετε κείμενο
  από εικόνες και μετατροπή PDF OCR με παράλληλη επεξεργασία.
draft: false
keywords:
- how to batch ocr
- extract text from images
- pdf ocr conversion
- batch ocr processing
- parallel ocr processing
language: el
og_description: πώς να εκτελείτε μαζική OCR αποδοτικά—βήμα‑βήμα οδηγός για εξαγωγή
  κειμένου από εικόνες, μετατροπή PDF σε OCR και μαζική επεξεργασία OCR χρησιμοποιώντας
  Python.
og_title: 'πώς να κάνετε ομαδική OCR: γρήγορη παράλληλη εξαγωγή κειμένου'
tags:
- OCR
- Python
- Parallel Computing
title: 'Πώς να κάνετε ομαδική OCR: γρήγορη παράλληλη εξαγωγή κειμένου'
url: /el/python-java/general/how-to-batch-ocr-fast-parallel-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# πώς να κάνετε batch ocr: γρήγορη παράλληλη εξαγωγή κειμένου

Έχετε αναρωτηθεί ποτέ **πώς να κάνετε batch ocr** όταν έχετε δεκάδες σαρωμένες σελίδες, στιγμιότυπα οθόνης και PDF που κρέμονται; Δεν είστε μόνοι—οι περισσότεροι προγραμματιστές συναντούν το ίδιο πρόβλημα: η επεξεργασία κάθε αρχείου ένα‑ένα γίνεται ένας επίπονος περιορισμός.  

Τα καλά νέα είναι ότι μπορείτε να δημιουργήσετε μια χούφτα νήματα εργατών, να τα τροφοδοτήσετε με όλα τα αρχεία σας και να δείτε τη μηχανή OCR να επεξεργάζεται το batch παράλληλα. Σε αυτό το tutorial θα περάσουμε από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που δείχνει **extract text from images**, εκτελεί **pdf ocr conversion**, και αξιοποιεί **parallel ocr processing** για ταχύτητα.

> **Τι θα αποκτήσετε**  
> * Ένα πλήρως λειτουργικό script Python που επεξεργάζεται μια μικτή λίστα αρχείων PNG, TIFF, PDF και JPG σε μία εκτέλεση.  
> * Κατανόηση του γιατί μια ομάδα νημάτων επιταχύνει εργασίες OCR που περιορίζονται από I/O.  
> * Συμβουλές για διαχείριση σφαλμάτων, μεγάλων PDF, και προσαρμοσμένου αριθμού νημάτων.  

## Προαπαιτούμενα

Πριν βουτήξουμε, βεβαιωθείτε ότι έχετε:

| Απαίτηση | Λόγος |
|-------------|--------|
| Python 3.8+ | Σύγχρονη σύνταξη & `concurrent.futures` |
| `ocr` library (or any compatible OCR wrapper) | Παρέχει `OcrBatchProcessor` και αντικείμενα αποτελεσμάτων |
| Μια χούφτα δείγματων αρχείων (PNG, TIFF, PDF, JPG) | Για να δείτε το **extract text from images** σε δράση |
| Βασική εξοικείωση με νήματα (προαιρετικό) | Χρήσιμο αλλά όχι υποχρεωτικό |

Αν δεν έχετε εγκαταστήσει ακόμα το πακέτο `ocr`, τρέξτε:

```bash
pip install ocr-lib   # replace with the actual package name
```

Τώρα που το περιβάλλον είναι έτοιμο, ας σπάσουμε το πρόβλημα σε βήματα.

## Βήμα 1: Εισαγωγή βοηθητικών συναρτήσεων και δημιουργία του batch processor

Το πρώτο που χρειαζόμαστε είναι ένας χώρος για τη συλλογή όλων των εργασιών OCR. Η κλάση `OcrBatchProcessor` κάνει ακριβώς αυτό—τοποθετεί τα αντικείμενα εργασίας σε ουρά και σας επιστρέφει μια λίστα από αντικείμενα `Future`.

```python
# Step 1 – set up imports and create the batch processor
from concurrent.futures import as_completed   # helps us retrieve results as they finish
import ocr                                      # the OCR library you installed

# Create a processor that will manage the whole batch
ocr_batch = ocr.OcrBatchProcessor()
```

*Γιατί είναι σημαντικό*: Η εισαγωγή του `as_completed` μας επιτρέπει να αντιδράμε αμέσως σε κάθε ολοκληρωμένη εργασία, αντί να περιμένουμε το πιο αργό αρχείο. Αυτό είναι η καρδιά του **batch ocr processing**.

## Βήμα 2: Ρύθμιση του pool εργατών για παράλληλη εκτέλεση

Από προεπιλογή ο επεξεργαστής μπορεί να χρησιμοποιεί ένα μόνο νήμα, κάτι που αναιρεί το σκοπό του batching. Ζητάμε ρητά τέσσερα εργατικά νήματα—αλλάξτε αυτόν τον αριθμό ανάλογα με τον αριθμό πυρήνων CPU που έχετε.

```python
# Step 2 – configure parallelism (four threads in this example)
ocr_batch.set_thread_count(4)   # Adjust based on your machine’s capabilities
```

*Pro tip*: Για εργασίες I/O‑bound όπως το OCR, συνήθως οι αποδόσεις μειώνονται μετά από `CPU cores * 2`. Δοκιμάστε μερικές τιμές και βρείτε το βέλτιστο σημείο.

## Βήμα 3: Προσθήκη κάθε αρχείου που θέλετε να OCR

Εδώ προσθέτουμε ένα μίγμα εικόνων και PDF. Η μέθοδος `add` απλώς καταγράφει τη διαδρομή· η πραγματική εργασία δεν ξεκινά μέχρι να υποβάλουμε το batch.

```python
# Step 3 – add files to the batch (feel free to glob a directory instead)
ocr_batch.add("YOUR_DIRECTORY/page1.png")
ocr_batch.add("YOUR_DIRECTORY/page2.tif")
ocr_batch.add("YOUR_DIRECTORY/page3.pdf")
ocr_batch.add("YOUR_DIRECTORY/page4.jpg")
```

Αν χρειάζεται να επεξεργαστείτε ολόκληρο φάκελο, ένας γρήγορος βρόχος `glob` κάνει τη δουλειά:

```python
import pathlib, fnmatch
for path in pathlib.Path("YOUR_DIRECTORY").rglob("*"):
    if fnmatch.fnmatch(path.suffix.lower(), ".png") or \
       fnmatch.fnmatch(path.suffix.lower(), ".tif") or \
       fnmatch.fnmatch(path.suffix.lower(), ".pdf") or \
       fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
        ocr_batch.add(str(path))
```

## Βήμα 4: Εκκίνηση των εργασιών και συλλογή των futures

Καλώντας το `submit_all` δίνετε στο επεξεργαστή το πράσινο φως. Επιστρέφει μια λίστα από αντικείμενα `Future`—σκεφτείτε τα ως placeholders για αποτελέσματα που θα εμφανιστούν αργότερα.

```python
# Step 4 – submit all jobs at once; get back a list of futures
ocr_futures = ocr_batch.submit_all()
```

Σε αυτό το σημείο η μηχανή OCR είναι απασχολημένη στο παρασκήνιο, κάθε νήμα τρώγοντας ένα αρχείο.

## Βήμα 5: Συλλογή αποτελεσμάτων μόλις ολοκληρωθούν

Χρησιμοποιώντας το `as_completed` διατρέχουμε τα futures με τη σειρά που τελειώνουν, όχι με τη σειρά που τα υποβάλαμε. Αυτό κρατά το script σας ανταποκρινόμενο, ειδικά όταν κάποια PDF διαρκούν περισσότερο από απλά PNG.

```python
# Step 5 – retrieve each result as it completes
for future in as_completed(ocr_futures):
    try:
        ocr_result = future.result()          # May raise if the job failed
        print("Batch result:\n", ocr_result.get_text())
    except Exception as exc:
        # Graceful error handling – you can log or retry here
        print(f"An OCR job failed: {exc}")
```

**Αναμενόμενη έξοδος** (συνοπτική για συντομία):

```
Batch result:
 The quick brown fox jumps over the lazy dog.
...
Batch result:
 Invoice #12345
 Date: 2026-03-01
 Total: $1,234.56
...
```

Κάθε μπλοκ αντιστοιχεί στην αναπαράσταση plain‑text του αρχικού αρχείου. Αν κάνετε **pdf ocr conversion**, το κείμενο θα περιλαμβάνει όλα όσα η μηχανή OCR μπόρεσε να διαβάσει από κάθε σελίδα.

## Διαχείριση Edge Cases & Συνηθισμένων Παγίδων

| Κατάσταση | Σε τι να προσέξετε | Γρήγορη λύση |
|-----------|-------------------|-----------|
| Κατεστραμμένη εικόνα | `future.result()` ρίχνει `OSError` | Τυλίξτε σε `try/except` (δείτε τον κώδικα παραπάνω) |
| Πολύ μεγάλα PDFs ( > 100 MB ) | Πίεση μνήμης, πιο αργά νήματα | Αυξήστε ελαφρώς το `thread_count` ή χωρίστε το PDF σε κεφάλαια πρώτα |
| Έγγραφα πολλαπλών γλωσσών | Το προεπιλεγμένο μοντέλο OCR μπορεί να μπερδέσει | Περάστε υποδείξεις γλώσσας στο `OcrBatchProcessor` αν η βιβλιοθήκη το υποστηρίζει |
| Απαίτηση διατήρησης διάταξης | Το απλό `get_text()` χάνει στήλες | Χρησιμοποιήστε `ocr_result.get_hocr()` ή παρόμοια μέθοδο που διατηρεί τη διάταξη |

### Pro tip: Προσαρμοσμένος αριθμός νημάτων βάσει τύπου αρχείου

Αν ξέρετε ότι το μεγαλύτερο μέρος του φόρτου εργασίας είναι PDFs, μπορείτε να διαθέσετε περισσότερα νήματα για αυτά και λιγότερα για μικρά PNG. Κάποιες βιβλιοθήκες επιτρέπουν να περάσετε `priority` ανά εργασία· αλλιώς, μπορείτε να δημιουργήσετε δύο ξεχωριστά batches—ένα για εικόνες, ένα για PDFs—και να τα τρέξετε ταυτόχρονα.

## Οπτική Επισκόπηση (προαιρετικό)

![how to batch ocr workflow diagram](https://example.com/ocr-workflow.png "how to batch ocr workflow")

*Το διάγραμμα απεικονίζει τη ροή από την ανακάλυψη αρχείων → δημιουργία batch → παράλληλη εκτέλεση → συγκέντρωση αποτελεσμάτων.*

## Πλήρες Script που Μπορείτε να Αντιγράψετε‑Κολλήσετε

Παρακάτω είναι ολόκληρο το πρόγραμμα, έτοιμο να τοποθετηθεί σε ένα αρχείο `.py`. Περιλαμβάνει όλα τα αποσπάσματα παραπάνω, καθώς και έναν μικρό βοηθό που ανακαλύπτει αυτόματα υποστηριζόμενα αρχεία σε έναν φάκελο.

```python
#!/usr/bin/env python3
"""
How to Batch OCR – Complete Example
-----------------------------------
This script demonstrates parallel OCR processing of mixed image and PDF files.
It shows how to extract text from images, perform pdf ocr conversion, and
handle errors gracefully.
"""

from concurrent.futures import as_completed
import pathlib, fnmatch, sys
import ocr  # replace with your actual OCR library import

def discover_files(root_dir):
    """Yield paths of supported OCR files under *root_dir*."""
    for path in pathlib.Path(root_dir).rglob("*"):
        if fnmatch.fnmatch(path.suffix.lower(), ".png") \
           or fnmatch.fnmatch(path.suffix.lower(), ".tif") \
           or fnmatch.fnmatch(path.suffix.lower(), ".pdf") \
           or fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
            yield str(path)

def main(directory, workers=4):
    # 1️⃣ Initialise batch processor
    ocr_batch = ocr.OcrBatchProcessor()
    ocr_batch.set_thread_count(workers)

    # 2️⃣ Queue every discovered file
    for file_path in discover_files(directory):
        ocr_batch.add(file_path)

    # 3️⃣ Submit all jobs
    futures = ocr_batch.submit_all()

    # 4️⃣ Process results as they arrive
    for fut in as_completed(futures):
        try:
            result = fut.result()
            print("=== OCR RESULT ===")
            print(result.get_text())
            print("\n---\n")
        except Exception as e:
            print(f"[ERROR] OCR failed for a job: {e}", file=sys.stderr)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <directory-with-files>")
        sys.exit(1)
    main(sys.argv[1])
```

Αποθηκεύστε το ως `batch_ocr.py`, δείξτε το σε έναν φάκελο που περιέχει τις σαρώσεις σας, και παρακολουθήστε την κονσόλα να γεμίζει με εξαγόμενο κείμενο.  

### Γιατί λειτουργεί αυτό

* **Thread pool** – Το OCR περιμένει κυρίως I/O δίσκου και κλήσεις σε εξωτερικές μηχανές, οπότε πολλά νήματα κρατούν την CPU απασχολημένη.  
* **`as_completed`** – Λαμβάνετε τα αποτελέσματα αμέσως μόλις είναι έτοιμα, ιδανικό για UI feedback ή streaming pipelines.  
* **Απομόνωση σφαλμάτων** – Ένα κακό αρχείο δεν θα καταρρεύσει όλο το batch· το block `try/except` απομονώνει τις αποτυχίες.

## Συμπέρασμα

Συνοπτικά, τώρα ξέρετε **πώς να κάνετε batch ocr** χρησιμοποιώντας το `concurrent.futures` της Python μαζί με μια βιβλιοθήκη OCR που υποστηρίζει batch processing. Ρυθμίζοντας ένα μέτριο pool νημάτων, προσθέτοντας κάθε υποστηριζόμενο αρχείο, και συλλέγοντας τα αποτελέσματα καθώς ολοκληρώνονται, επιτυγχάνετε γρήγορη **parallel ocr processing** χωρίς να θυσιάζετε την αξιοπιστία.  

Από εδώ μπορείτε:

* Να ενσωματώσετε την έξοδο σε έναν δείκτη αναζήτησης για γρήγορη ανάκτηση εγγράφων.  
* Να επεκτείνετε το script ώστε να γράφει κάθε αποτέλεσμα σε αρχείο `.txt` δίπλα στο αρχικό.  
* Να αντικαταστήσετε το ενσωματωμένο thread pool με `asyncio` αν η βιβλιοθήκη OCR προσφέρει async APIs.  

Συνεχίστε να πειραματίζεστε—αντικαταστήστε το Tesseract, Azure Cognitive Services, ή Google Vision, και θα δείτε ότι το ίδιο μοτίβο ισχύει. Καλή OCR‑εξαγωγή!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}