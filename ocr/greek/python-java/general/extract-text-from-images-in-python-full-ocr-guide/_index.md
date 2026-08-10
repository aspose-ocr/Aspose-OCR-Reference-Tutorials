---
category: general
date: 2026-06-19
description: Εξάγετε κείμενο από εικόνες χρησιμοποιώντας Python OCR. Μάθετε αυτόματη
  ανίχνευση γλώσσας, παράλληλη επεξεργασία και αναγνώριση σε παρτίδες σε ένα σύντομο
  σεμινάριο.
draft: false
keywords:
- extract text from images
- Python OCR library
- automatic language detection
- parallel processing OCR
- batch image recognition
- ocr.OcrEngine usage
language: el
og_description: Εξάγετε κείμενο από εικόνες με Python OCR. Αυτός ο οδηγός δείχνει
  αυτόματη ανίχνευση γλώσσας, παράλληλη επεξεργασία και αναγνώριση δέσμης σε ένα ενιαίο
  σεμινάριο.
og_title: Εξαγωγή κειμένου από εικόνες σε Python – Πλήρης Οδηγός OCR
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: extract text from images using Python OCR. Learn automatic language
    detection, parallel processing, and batch recognition in a concise tutorial.
  headline: extract text from images in Python – Full OCR Guide
  type: TechArticle
- description: extract text from images using Python OCR. Learn automatic language
    detection, parallel processing, and batch recognition in a concise tutorial.
  name: extract text from images in Python – Full OCR Guide
  steps:
  - name: Python 3.8 or newer installed.
    text: Python 3.8 or newer installed.
  - name: The `ocr` package (`pip install ocr`).
    text: The `ocr` package (`pip install ocr`).
  - name: A folder of PNG (or JPG) images you want to process.
    text: A folder of PNG (or JPG) images you want to process.
  - name: Basic familiarity with Python functions and loops.
    text: Basic familiarity with Python functions and loops.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Εξαγωγή κειμένου από εικόνες σε Python – Πλήρης Οδηγός OCR
url: /el/python-java/general/extract-text-from-images-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# εξαγωγή κειμένου από εικόνες σε Python – Πλήρης Οδηγός OCR

Έχετε αναρωτηθεί ποτέ πώς να **εξάγετε κείμενο από εικόνες** χωρίς να πληκτρολογείτε κάθε λέξη χειροκίνητα; Δεν είστε οι μόνοι. Είτε ψηφιοποιείτε παλιές αποδείξεις, είτε δημιουργείτε ένα αναζητήσιμο αρχείο εγγράφων, είτε απλώς πειραματίζεστε με εντυπωσιακές τεχνικές AI, η δυνατότητα εξαγωγής κειμένου από εικόνες είναι απαραίτητη για κάθε προγραμματιστή Python σήμερα.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, έτοιμο‑να‑τρέξει παράδειγμα που **εξάγει κείμενο από εικόνες** χρησιμοποιώντας μια δημοφιλή μηχανή OCR. Θα καλύψουμε αυτόματη ανίχνευση γλώσσας, παράλληλη επεξεργασία για ταχύτητα και επεξεργασία παρτίδας εικόνων ώστε να μπορείτε να διαχειριστείτε δεκάδες αρχεία σε δευτερόλεπτα. Σαφές ότι είναι αυτό που χρειάζεστε; Ας βουτήξουμε.

## Τι Θα Μάθετε

- Πώς να δημιουργήσετε μια μηχανή OCR με `ocr.OcrEngine`.
- Ενεργοποίηση **αυτόματης ανίχνευσης γλώσσας** ώστε η μηχανή να επιλέγει τη σωστή γλώσσα από μόνη της.
- Διαμόρφωση **παράλληλης επεξεργασίας OCR** με προσαρμοσμένο thread pool.
- Εκτέλεση **επεξεργασίας παρτίδας εικόνων** σε λίστα αρχείων.
- Εκτύπωση του αναγνωρισμένου κειμένου για κάθε εικόνα, έτοιμο για αποθήκευση ή ευρετηρίαση.

Καμία εξωτερική τεκμηρίωση δεν απαιτείται — όλα όσα χρειάζεστε είναι εδώ, και ο κώδικας λειτουργεί αμέσως με το πακέτο `ocr` (εγκαταστήστε το μέσω `pip install ocr`).

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

1. Python 3.8 ή νεότερη έκδοση εγκατεστημένη.
2. Το πακέτο `ocr` (`pip install ocr`).
3. Έναν φάκελο με εικόνες PNG (ή JPG) που θέλετε να επεξεργαστείτε.
4. Βασική εξοικείωση με συναρτήσεις και βρόχους της Python.

Αυτό είναι όλο — χωρίς βαριές εξαρτήσεις, χωρίς μαγικά GPU, μόνο καθαρή Python.

![extract text from images example](https://example.com/ocr-demo.png "Στιγμιότυπο που δείχνει το αποτέλεσμα εξαγωγής κειμένου από εικόνες")

*Alt text: στιγμιότυπο επίδειξης εξαγωγής κειμένου από εικόνες*

## Βήμα 1 – Ρύθμιση της Μηχανής OCR (Κύρια Λέξη‑Κλειδί σε Δράση)

Πρώτο πράγμα: δημιουργήστε ένα αντικείμενο μηχανής OCR. Σκεφτείτε το `ocr.OcrEngine()` ως τον εγκέφαλο της λειτουργίας· ξέρει πώς να διαβάζει χαρακτήρες, γραμμές και παραγράφους.

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

Γιατί χρειάζεται μια ρητή μηχανή; Επειδή η **χρήση του ocr.OcrEngine** σας δίνει λεπτομερή έλεγχο πάνω στις ρυθμίσεις γλώσσας, threading και άλλα. Είναι ο πιο ευέλικτος τρόπος για **εξαγωγή κειμένου από εικόνες** σε σύγκριση με τις βοηθητικές συναρτήσεις μίας γραμμής.

## Βήμα 2 – Αφήστε τη Μηχανή να Ανιχνεύει Αυτόματα τις Γλώσσες

Οι περισσότερες βιβλιοθήκες OCR απαιτούν να τους πείτε ποια γλώσσα να ψάξουν. Αυτό είναι εντάξει για ένα έργο μίας γλώσσας, αλλά ενοχλητικό για παρτίδα με μικτές γλώσσες. Ευτυχώς, το πακέτο `ocr` υποστηρίζει **αυτόματη ανίχνευση γλώσσας**.

```python
# Step 2: Enable automatic language detection
engine.language = ocr.Language.Auto
```

Ορίζοντας `engine.language` σε `ocr.Language.Auto` λέτε στη μηχανή να «ανιχνεύει» κάθε εικόνα και να επιλέγει το κατάλληλο μοντέλο γλώσσας. Αυτή η μικρή γραμμή σας εξοικονομεί ώρες χειροκίνητης ρύθμισης όταν δουλεύετε με διεθνή έγγραφα.

## Βήμα 3 – Επιταχύνετε με Παράλληλη Επεξεργασία OCR

Αν έχετε τέσσερις ή περισσότερους πυρήνες CPU, γιατί να μην τους χρησιμοποιήσετε; Η μηχανή μπορεί να δημιουργήσει ένα thread pool, επιτρέποντας την ταυτόχρονη επεξεργασία πολλαπλών εικόνων. Εδώ η **παράλληλη επεξεργασία OCR** δείχνει την αξία της.

```python
# Step 3: Enable parallel processing with four worker threads
engine.set_thread_pool_size(4)
```

Απλώς προσαρμόστε τον αριθμό `4` ανάλογα με το σύστημά σας. Περισσότερα νήματα → ταχύτερες εκτελέσεις παρτίδας, αλλά θυμηθείτε ότι κάθε νήμα καταναλώνει μνήμη, οπότε βρείτε το «sweet spot» για το περιβάλλον σας.

## Βήμα 4 – Συλλογή των Εικόνων που Θέλετε να Επεξεργαστείτε

Τώρα χρειαζόμαστε μια λίστα διαδρομών αρχείων. Μπορείτε να τη δημιουργήσετε χειροκίνητα, να τη διαβάσετε από CSV ή να χρησιμοποιήσετε `glob`. Για σαφήνεια, θα κωδικοποιήσουμε μια σύντομη λίστα:

```python
# Step 4: Prepare a list of image files to be recognized
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png",
    "YOUR_DIRECTORY/doc4.png"
]
```

Αντικαταστήστε το `YOUR_DIRECTORY` με την πραγματική διαδρομή στο σύστημά σας. Αν έχετε δεκάδες αρχεία, ένα γρήγορο `glob.glob("*.png")` θα κάνει τη δουλειά.

## Βήμα 5 – Εκτέλεση Επεξεργασίας Παρτίδας Εικόνων

Αυτή είναι η καρδιά του tutorial: μία κλήση που επεξεργάζεται κάθε εικόνα στη λίστα `files` και επιστρέφει μια λίστα αντικειμένων αποτελεσμάτων. Αυτή είναι η λειτουργία **επεξεργασίας παρτίδας εικόνων** που κάνει το OCR σε μεγάλη κλίμακα πρακτικό.

```python
# Step 5: Perform batch recognition on all images
results = engine.recognize_batch(files)
```

Στο παρασκήνιο, η μηχανή διανέμει κάθε αρχείο στα τέσσερα νήματα εργασίας που ρυθμίσαμε νωρίτερα, ενώ αυτόματα ανιχνεύει τη γλώσσα για κάθε εικόνα. Η μέθοδος επιστρέφει μια λίστα όπου κάθε στοιχείο περιέχει το αναγνωρισμένο κείμενο και μεταδεδομένα.

## Βήμα 6 – Εκτύπωση (ή Αποθήκευση) του Εξαγόμενου Κειμένου

Τέλος, διατρέχουμε τα αποτελέσματα και εκτυπώνουμε το κείμενο. Σε πραγματικό έργο πιθανότατα θα γράψετε τα δεδομένα σε βάση ή CSV, αλλά η εκτύπωση κρατά το παράδειγμα απλό.

```python
# Step 6: Output the recognized text for each image
for result in results:
    print("---")
    print(f"File: {result.file_path}")
    print("Extracted Text:")
    print(result.text.strip())
    print("---\n")
```

**Αναμενόμενο αποτέλεσμα** (κομμένο για συντομία):

```
---
File: YOUR_DIRECTORY/doc1.png
Extracted Text:
Invoice #12345
Date: 2024‑03‑15
Total: $250.00
---
```

Κάθε μπλοκ δείχνει το όνομα αρχείου ακολουθούμενο από το κείμενο που προέκυψε από το OCR. Αν μια εικόνα περιέχει πολλαπλές γλώσσες, θα δείτε τους αντίστοιχους χαρακτήρες χάρη στο προηγούμενο βήμα **αυτόματης ανίχνευσης γλώσσας**.

## Pro Tips & Συνηθισμένα Πιθανά Προβλήματα

- **Η ποιότητα της εικόνας μετρά** – θολές ή χαμηλής αντίθεσης εικόνες θα δώσουν άσχημα αποτελέσματα. Προεπεξεργαστείτε με OpenCV (`cv2.threshold`, `cv2.resize`) αν χρειάζεται.
- **Αριθμός νημάτων vs. I/O** – Αν οι εικόνες βρίσκονται σε αργό δίκτυο, περισσότερα νήματα ίσως δεν βοηθήσουν. Παρακολουθήστε τη χρήση CPU με `top` ή `Task Manager`.
- **Διαχείριση Unicode** – Το `result.text` είναι συμβολοσειρά Unicode. Όταν γράφετε σε αρχεία, ανοίξτε τα με `encoding="utf‑8"` για να αποφύγετε `UnicodeEncodeError`.
- **Κατανάλωση μνήμης** – Μεγάλα PDF μπορούν να καταναλώσουν πολύ RAM. Αν αντιμετωπίσετε `MemoryError`, μειώστε το μέγεθος του thread pool ή επεξεργαστείτε τις εικόνες σε μικρότερα τμήματα.

## Πλήρες Εργαζόμενο Script

Ακολουθεί το πλήρες, έτοιμο‑για‑αντιγραφή script που ενσωματώνει όλα τα βήματα που συζητήσαμε. Αποθηκεύστε το ως `batch_ocr.py` και τρέξτε `python batch_ocr.py`.

```python
#!/usr/bin/env python3
"""
Batch OCR script to extract text from images using the ocr package.
Features:
- Automatic language detection
- Parallel processing with configurable thread pool
- Simple batch API for multiple files
"""

import ocr
import os
import sys

def main(image_dir: str, workers: int = 4):
    # Verify directory exists
    if not os.path.isdir(image_dir):
        print(f"Error: Directory '{image_dir}' does not exist.", file=sys.stderr)
        sys.exit(1)

    # Build list of PNG/JPG files
    supported_ext = (".png", ".jpg", ".jpeg", ".tif", ".tiff")
    files = [
        os.path.join(image_dir, f)
        for f in os.listdir(image_dir)
        if f.lower().endswith(supported_ext)
    ]

    if not files:
        print("No supported image files found in the directory.", file=sys.stderr)
        sys.exit(1)

    # Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto          # automatic language detection
    engine.set_thread_pool_size(workers)         # parallel processing OCR

    # Perform batch recognition
    print(f"Processing {len(files)} files with {workers} workers...")
    results = engine.recognize_batch(files)

    # Output results
    for result in results:
        print("---")
        print(f"File: {result.file_path}")
        print("Extracted Text:")
        print(result.text.strip())
        print("---\n")

if __name__ == "__main__":
    # Example usage: python batch_ocr.py ./my_images 4
    if len(sys.argv) < 2:
        print("Usage: python batch_ocr.py <image_directory> [worker_count]")
        sys.exit(1)

    directory = sys.argv[1]
    worker_count = int(sys.argv[2]) if len(sys.argv) > 2 else 4
    main(directory, worker_count)
```

Τρέξτε το έτσι:

```bash
python batch_ocr.py ./my_images 4
```

Θα δείτε ένα ωραία μορφοποιημένο μπλοκ κειμένου για κάθε εικόνα, αποδεικνύοντας ότι μπορείτε να **εξάγετε κείμενο από εικόνες** σε κλίμακα.

## Τι Ακολουθεί;

Τώρα που έχετε κατακτήσει τα βασικά της **εξαγωγής κειμένου από εικόνες** με Python, σκεφτείτε να εξερευνήσετε:

- **Post‑processing**: καθαρίστε το αποτέλεσμα OCR με regex ή βιβλιοθήκες φυσικής γλώσσας.
- **Μετατροπή σε PDF**: τροφοδοτήστε τις εξαγόμενες συμβολοσειρές σε δημιουργό PDF για αναζητήσιμα PDFs.
- **Υπηρεσίες Cloud OCR**: συγκρίνετε τα αποτελέσματα του τοπικού `ocr` με Google Vision ή Azure OCR για ακραίες περιπτώσεις ακρίβειας.
- **GUI front‑end**: χτίστε μια μικρή εφαρμογή Flask ή FastAPI που επιτρέπει στους χρήστες να ανεβάζουν εικόνες και να βλέπουν αμέσως το εξαγόμενο κείμενο.

Κάθε ένα από αυτά τα θέματα βασίζεται στο **Python OCR library** που μόλις στήσατε, και όλα ωφελούνται από τις ίδιες **παράλληλες επεξεργασίες OCR** που χρησιμοποιήσαμε εδώ.

---

*Καλό κώδικα! Αν αντιμετωπίσετε δυσκολίες, αφήστε ένα σχόλιο παρακάτω — είμαι πάντα διαθέσιμος για troubleshooting OCR.*


## Τι Πρέπει να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές του παρόντος οδηγού. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κυριαρχήσετε σε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}