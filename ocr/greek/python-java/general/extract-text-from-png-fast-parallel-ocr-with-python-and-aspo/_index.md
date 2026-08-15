---
category: general
date: 2026-03-28
description: Εξάγετε κείμενο από PNG γρήγορα χρησιμοποιώντας το Aspose OCR σε Python.
  Μάθετε πώς να μετατρέπετε το κείμενο των σαρωμένων σελίδων με παράλληλη αναγνώριση
  εικόνας σε Python για αποτελέσματα υψηλής απόδοσης.
draft: false
keywords:
- extract text from png
- convert scanned pages text
- parallel image recognition python
- recognize image text python
- async OCR batch processing
- Aspose OCR Python
language: el
og_description: Εξάγετε κείμενο από PNG γρήγορα χρησιμοποιώντας το Aspose OCR σε Python.
  Αυτός ο οδηγός δείχνει πώς να μετατρέψετε το κείμενο σαρωμένων σελίδων με παράλληλη
  αναγνώριση εικόνας σε Python, προσφέροντας αποτελέσματα υψηλής ταχύτητας.
og_title: Εξαγωγή κειμένου από PNG – Γρήγορο παράλληλο OCR με Python
tags:
- OCR
- Python
- Image Processing
- Concurrency
title: Εξαγωγή κειμένου από PNG – Γρήγορο παράλληλο OCR με Python και Aspose
url: /el/python-java/general/extract-text-from-png-fast-parallel-ocr-with-python-and-aspo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από PNG – Γρήγορο Παράλληλο OCR με Python

Κάποτε χρειάστηκε να **εξάγετε κείμενο από αρχεία PNG** αλλά το μονονηματικό OCR ήταν εξαιρετικά αργό; Δεν είστε μόνοι. Είτε ψηφιοποιείτε μια στοίβα σαρωμένων αποδείξεων είτε μετατρέπετε διαφάνειες διαλέξεων σε αναζητήσιμα PDF, το στενό σημείο είναι συνήθως το βήμα του OCR.  

Σε αυτό το tutorial θα σας δείξουμε μια πλήρη, έτοιμη προς εκτέλεση λύση που **μετατρέπει το κείμενο σαρωμένων σελίδων** παράλληλα, χρησιμοποιώντας τη λειτουργία async batch του Aspose OCR σε συνδυασμό με το `ThreadPoolExecutor` της Python. Στο τέλος θα μπορείτε να **recognize image text python**‑style, επεξεργαζόμενοι δεκάδες εικόνες σε κλάσμα του χρόνου που θα απαιτούσε ένας απλός βρόχος.

> **Τι θα αποκτήσετε**  
> * Ένα πλήρως λειτουργικό script που εξάγει κείμενο από εικόνες PNG ταυτόχρονα.  
> * Κατανόηση του γιατί η async batch mode επιταχύνει τη διαδικασία.  
> * Συμβουλές για κλιμάκωση της λύσης σε μεγαλύτερα φορτία εργασίας.

## Τι Θα Χρειαστείτε

| Προαπαιτούμενο | Λόγος |
|----------------|-------|
| Python 3.9+ | Σύγχρονη σύνταξη και type hints. |
| Πακέτα `aspose-ocr` και `aspose-storage` | Παρέχουν τη μηχανή OCR και το φορτωτή εικόνων. |
| Ένας φάκελος με αρχεία PNG (π.χ. σαρωμένες σελίδες) | Το υλικό που θέλετε να επεξεργαστείτε. |
| Βασικές γνώσεις σύγχυσης (concurrency) στην Python | Χρήσιμες αλλά όχι υποχρεωτικές· θα εξηγήσουμε τα πάντα. |

Μπορείτε να εγκαταστήσετε τις βιβλιοθήκες Aspose με:

```bash
pip install aspose-ocr aspose-storage
```

> **Pro tip:** Κρατήστε τα πακέτα σας ενημερωμένα (`pip list --outdated`) για να επωφεληθείτε από τις τελευταίες βελτιώσεις απόδοσης.

## Βήμα 1: Αρχικοποίηση του Aspose OCR Engine σε Async Batch Mode

Το πρώτο που κάνουμε είναι να δημιουργήσουμε ένα αντικείμενο `OcrEngine` και να το μεταβάλουμε σε **asynchronous batch mode**. Αυτή η λειτουργία ουράζει εσωτερικά αιτήματα αναγνώρισης, επιτρέποντας στη μηχανή να επεξεργάζεται πολλαπλές εικόνες χωρίς να μπλοκάρει το νήμα της Python.

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the OCR engine
ocr_engine = aocr.OcrEngine()
# Enable async batch processing – crucial for parallel speed‑up
ocr_engine.batch_mode = aocr.BatchMode.ASYNC
```

*Γιατί async;*  
Όταν καλείτε το `recognize` σε συγχρονική λειτουργία, η κλήση μπλοκάρει μέχρι να ολοκληρωθεί η επεξεργασία της εικόνας. Στην async λειτουργία, η μηχανή μπορεί να αρχίσει να δουλεύει στην επόμενη εικόνα ενώ η τρέχουσα εξακολουθεί να αποκωδικοποιείται, επικαλύπτοντας έτσι I/O και CPU.

## Βήμα 2: Καταγραφή των Αρχείων PNG που Θέλετε να Επεξεργαστείτε

Εδώ ορίζουμε τη συλλογή των εικόνων. Σε ένα πραγματικό έργο μπορεί να δημιουργήσετε αυτή τη λίστα δυναμικά (π.χ. `glob.glob("*.png")`), αλλά η ρητή δήλωση την κάνει πιο εύκολη στην κατανόηση.

```python
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]
```

> **Σημείωση:** Αντικαταστήστε το `YOUR_DIRECTORY` με την πραγματική διαδρομή όπου βρίσκονται οι PNG σαρώσεις σας. Αν έχετε εκατοντάδες αρχεία, σκεφτείτε να χρησιμοποιήσετε το `os.listdir` και να φιλτράρετε για `.png`.

## Βήμα 3: Γράψτε μια Βοηθητική Συνάρτηση που Φορτώνει μια Εικόνα και Επιστρέφει το Κείμενό της

Η βοηθητική συνάρτηση αφαιρεί τη διαδικασία δύο βημάτων: τη φόρτωση του αρχείου μέσω **Aspose Storage** και την επεξεργασία του από τη μηχανή OCR. Η προσθήκη ενός μικρού docstring κάνει τη συνάρτηση αυτο‑εξηγητική—χρήσιμη για μελλοντική συντήρηση.

```python
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the recognized text.
    """
    # Load the image using Aspose Storage (handles many formats)
    img = storage.Image.load(path)
    # Perform OCR; the result object contains the extracted text
    result = ocr_engine.recognize(img)
    return result.text
```

*Γιατί ξεχωριστή συνάρτηση;*  
Κρατά τον κώδικα του thread‑pool καθαρό και μας επιτρέπει να επαναχρησιμοποιήσουμε τη λογική αλλού (π.χ. σε ένα endpoint Flask). Επίσης, η απομόνωση του I/O διευκολύνει τον εντοπισμό σφαλμάτων—αν αποτύχει κάποιο αρχείο, θα δείτε το όνομα του αρχείου στο trace της εξαίρεσης.

## Βήμα 4: Εκτέλεση Παράλληλης Αναγνώρισης Εικόνας Python με Thread Pool

Τώρα φέρνουμε το `ThreadPoolExecutor`. Από προεπιλογή δημιουργούμε τέσσερις εργαζόμενους, αλλά μπορείτε να ρυθμίσετε το `max_workers` ανάλογα με τους πυρήνες του CPU και το μέγεθος του συνόλου εικόνων.

```python
from concurrent.futures import ThreadPoolExecutor, as_completed

with ThreadPoolExecutor(max_workers=4) as pool:
    # Submit each image to the pool; map futures back to filenames
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    
    # Process results as they finish (order may differ from input order)
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)
```

### Πώς Αυτό Παρέχει Παράλληλη Αναγνώριση Εικόνας Python

* **ThreadPoolExecutor** δημιουργεί μια δεξαμενή εργαζόμενων νημάτων που κάθε ένα καλεί το `recognize_image`.  
* Επειδή η μηχανή OCR βρίσκεται σε async batch mode, κάθε νήμα μπορεί να παραδώσει δουλειά στη μηχανή ενώ παραμένει ενεργό.  
* Το `as_completed` επιστρέφει τα futures με τη σειρά που ολοκληρώνονται, ώστε να λαμβάνετε τα αποτελέσματα αμέσως—ιδανικό για ροή μεγάλων batch.

> **Κοινό λάθος:** Η χρήση `max_workers=1` αναιρεί το σκοπό του parallelism. Σε μηχάνημα με 8 πυρήνες, `max_workers=8` συχνά δίνει την καλύτερη απόδοση, αλλά δοκιμάστε μερικές τιμές για να βρείτε το βέλτιστο για το hardware σας.

## Βήμα 5: Επαλήθευση του Αποτελέσματος και Διαχείριση Ακραίων Περιπτώσεων

Όταν τρέξετε το script, θα πρέπει να δείτε ένα μπλοκ κειμένου για κάθε PNG, προαχθέν από το όνομα του αρχείου:

```
--- YOUR_DIRECTORY/page1.png ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- YOUR_DIRECTORY/page2.png ---
Sed do eiusmod tempor incididunt ut labore et dolore...

--- YOUR_DIRECTORY/page3.png ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

Αν κάποια εικόνα αποτύχει (κατεστραμμένο αρχείο, μη υποστηριζόμενη μορφή), το block `except` εκτυπώνει ένα χρήσιμο μήνυμα σφάλματος αντί να καταρρεύσει ολόκληρο το batch.

### Επέκταση της Λύσης

| Σενάριο | Προτεινόμενη τροποποίηση |
|----------|---------------------------|
| **Χιλιάδες σελίδες** | Μεταβείτε σε `ProcessPoolExecutor` για αξιοποίηση πολλαπλών διεργασιών CPU, ή χωρίστε τη λίστα σε τμήματα και επεξεργαστείτε τα batch διαδοχικά. |
| **Διάφορες μορφές εικόνας (JPG, TIFF)** | Η μέθοδος `storage.Image.load` ανιχνεύει αυτόματα τη μορφή, οπότε απλώς προσθέστε τα αρχεία στο `input_images`. |
| **Ανάγκη αποθήκευσης αποτελεσμάτων** | Γράψτε το `text` σε αρχείο `.txt` ή εισάγετε το σε βάση δεδομένων μέσα στο block `else`. |
| **Παρακολούθηση απόδοσης** | Τυλίξτε το `recognize_image` με χρονομετρητή (`time.perf_counter`) και καταγράψτε τη διάρκεια ανά αρχείο. |

## Πλήρες Παράδειγμα Εργασίας (Ready‑to‑Copy)

Παρακάτω είναι το ολοκληρωμένο script, έτοιμο να το τοποθετήσετε σε ένα αρχείο με όνομα `parallel_ocr.py`. Δεν λείπει τίποτα—όλα όσα χρειάζεστε είναι εδώ.

```python
# parallel_ocr.py
import aspose.ocr as aocr
import aspose.storage as storage
from concurrent.futures import ThreadPoolExecutor, as_completed

# -------------------------------------------------
# Step 1: Initialize OCR engine in async batch mode
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.batch_mode = aocr.BatchMode.ASYNC   # enable asynchronous batch processing

# -------------------------------------------------
# Step 2: Define the PNG files you want to recognize
# -------------------------------------------------
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]

# -------------------------------------------------
# Step 3: Helper that loads an image and returns the recognized text
# -------------------------------------------------
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the OCR‑extracted text.
    """
    img = storage.Image.load(path)
    result = ocr_engine.recognize(img)
    return result.text

# -------------------------------------------------
# Step 4: Run OCR on all images concurrently using a thread pool
# -------------------------------------------------
with ThreadPoolExecutor(max_workers=4) as pool:
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)

# -------------------------------------------------
# Step 5: Output is printed to the console.
# -------------------------------------------------
```

Αποθηκεύστε το αρχείο, προσαρμόστε το placeholder `YOUR_DIRECTORY`, και τρέξτε:

```bash
python parallel_ocr.py
```

Θα πρέπει να δείτε το εξαγόμενο κείμενο για κάθε PNG να εμφανίζεται στην κονσόλα, όπως φαίνεται παραπάνω.

## Συμπέρασμα

Δείξαμε πώς να **εξάγετε κείμενο από PNG** αρχεία αποδοτικά, συνδυάζοντας το async batch mode του Aspose OCR με το `ThreadPoolExecutor` της Python. Το script μετατρέπει το κείμενο σαρωμένων σελίδων παράλληλα, παρέχοντάς σας μια κλιμακώσιμη μέθοδο για **recognize image text python**‑style χωρίς να χρειάζεται να γράψετε δικό σας thread‑pool από την αρχή.  

Αν θέλετε να προχωρήσετε παραπέρα, δοκιμάστε:

* Αποθήκευση των αποτελεσμάτων σε μια αναζητήσιμη βάση SQLite.  
* Προεπεξεργασία εικόνας (deskew, denoise) με OpenCV πριν το OCR.  
* Ανάπτυξη του script ως μικροϋπηρεσία πίσω από ένα endpoint Flask ή FastAPI.

Θυμηθείτε, το κλειδί για υψηλής απόδοσης OCR δεν είναι μόνο μια γρηγορότερη μηχανή—αφορά επίσης το πώς τροφοδοτείτε τη μηχανή με δουλειά ώστε να μεγιστοποιήσετε τη σύγκρουση. Με το μοτίβο που παρουσιάστηκε εδώ, μπορείτε να διαχειριστείτε δεκάδες ή ακόμη και εκατοντάδες PNG σαρώσεις με ελάχιστες αλλαγές κώδικα.

Καλή κωδικοποίηση, και οι PDF σας να είναι πάντα αναζητήσιμοι!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}