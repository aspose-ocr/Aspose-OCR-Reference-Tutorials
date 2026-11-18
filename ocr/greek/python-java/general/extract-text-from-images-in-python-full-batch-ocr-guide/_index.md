---
category: general
date: 2026-06-19
description: Εξάγετε κείμενο από εικόνες σε Python με μια απλή μηχανή OCR. Μάθετε
  πώς να μετατρέπετε σαρωμένες εικόνες σε κείμενο, να αναγνωρίζετε κείμενο από φωτογραφίες
  και να καταγράφετε αρχεία εικόνας σε Python αποδοτικά.
draft: false
keywords:
- extract text from images
- convert scanned images to text
- recognize text from pictures
- list image files python
language: el
og_description: Εξάγετε κείμενο από εικόνες σε Python χρησιμοποιώντας μια ελαφριά
  μηχανή OCR. Αυτός ο οδηγός σας δείχνει πώς να μετατρέψετε σαρωμένες εικόνες σε κείμενο,
  να αναγνωρίσετε κείμενο από φωτογραφίες και να καταγράψετε αρχεία εικόνας σε Python
  σε λίγα βήματα.
og_title: Εξαγωγή κειμένου από εικόνες σε Python – Πλήρης οδηγός OCR σε παρτίδα
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Extract text from images in Python with a simple OCR engine. Learn
    how to convert scanned images to text, recognize text from pictures, and list
    image files python efficiently.
  headline: Extract Text from Images in Python – Full Batch OCR Guide
  type: TechArticle
tags:
- Python
- OCR
- Image Processing
title: Εξαγωγή κειμένου από εικόνες με Python – Οδηγός πλήρους OCR σε παρτίδες
url: /el/python-java/general/extract-text-from-images-in-python-full-batch-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Εικόνες σε Python – Οδηγός Πλήρους Batch OCR

Κάποτε χρειάστηκε να **εξάγετε κείμενο από εικόνες** αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είσαι μόνος—οι προγραμματιστές αντιμετωπίζουν συνεχώς την πρόκληση του να μετατρέπουν σαρωμένα PDF, φωτογραφημένα αποδείξεις ή στιγμιότυπα οθόνης σε αναζητήσιμο κείμενο. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που δείχνει πώς να **μετατρέψετε σαρωμένες εικόνες σε κείμενο**, να αναγνωρίζετε κείμενο από φωτογραφίες, και ακόμη να **καταγράψετε αρχεία εικόνας python‑style**. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο script που επεξεργάζεται ολόκληρο φάκελο με μια κλήση.

Θα καλύψουμε όλα όσα χρειάζεστε: απαιτούμενες βιβλιοθήκες, γιατί κάθε βήμα είναι σημαντικό, διαχείριση edge‑case, και λίγη αντιμετώπιση προβλημάτων. Δεν χρειάζεται να ψάχνετε σε εξωτερική τεκμηρίωση· ο κώδικας παρακάτω είναι αυτόνομος, και οι εξηγήσεις απαντούν στο “πώς” *και* στο “γιατί”. Πάρτε το αγαπημένο σας IDE και ας ξεκινήσουμε.

---

## Τι Θα Δημιουργήσετε

- Αρχικοποίηση μηχανής OCR (θα χρησιμοποιήσουμε το πακέτο `ocr` για παράδειγμα).
- Σάρωση ενός καταλόγου και **καταγραφή αρχείων εικόνας python‑style**, φιλτράροντας PNG, JPG και TIFF.
- Εκτέλεση λειτουργίας **batch OCR** σε όλες τις εικόνες που βρέθηκαν.
- Εκτύπωση του εξαγόμενου κειμένου για κάθε αρχείο, με σαφή ετικέτα.

> **Pro tip:** Αν δεν έχετε εγκαταστήσει τη βιβλιοθήκη `ocr`, μπορείτε να την αντικαταστήσετε με `pytesseract` με μερικές μικρές αλλαγές—η βασική λογική παραμένει η ίδια.

---

## Προαπαιτούμενα

- Python 3.8+ (το script χρησιμοποιεί f‑strings και type hints).
- Μια βιβλιοθήκη OCR που εκθέτει ένα `OcrEngine` με `recognize_batch`. Για αυτόν τον οδηγό υποθέτουμε ένα φανταστικό πακέτο `ocr`, αλλά το μοτίβο λειτουργεί με πραγματικές βιβλιοθήκες.
- Ένας φάκελος που περιέχει αρχεία εικόνας που θέλετε να επεξεργαστείτε (`.png`, `.jpg`, `.tif`).

---

## Βήμα 1 – Εγκατάσταση & Εισαγωγή Απαιτούμενων Μονάδων

Πρώτα, βεβαιωθείτε ότι το πακέτο OCR είναι διαθέσιμο. Αν χρησιμοποιείτε πραγματική βιβλιοθήκη όπως `pytesseract`, αντικαταστήστε την εισαγωγή αναλόγως.

```python
# Install the fictional OCR package (skip if using pytesseract)
# pip install ocr-package

import os
import ocr  # <-- replace with your actual OCR library
from typing import List
```

> **Why this matters:** Η εισαγωγή του `os` μας δίνει διαχείριση διαδρομών ανεξαρτήτως πλατφόρμας, ενώ το `typing.List` βοηθά στην αυτόματη συμπλήρωση του IDE και στην προετοιμασία για το μέλλον.

---

## Βήμα 2 – **Extract Text from Images**: Αρχικοποίηση της Μηχανής OCR

Η δημιουργία της μηχανής είναι το πρώτο βήμα για οποιαδήποτε εργασία OCR. Ορίζουμε επίσης τη γλώσσα σε auto‑detect ώστε η μηχανή να μπορεί να διαχειριστεί έγγραφα με πολλαπλές γλώσσες.

```python
def create_engine() -> ocr.OcrEngine:
    """
    Initializes the OCR engine with automatic language detection.
    Returns:
        An instance of ocr.OcrEngine ready for batch processing.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto  # Auto‑detect language
    return engine
```

> **Explanation:** Με το να ενσωματώνουμε τη δημιουργία της μηχανής σε μια συνάρτηση κρατάμε τον κώδικα modular. Αν αργότερα χρειαστεί να ρυθμίσετε DPI ή OCR mode, θα το κάνετε μόνο σε αυτό το σημείο.

---

## Βήμα 3 – **List Image Files Python**: Συλλογή Αρχείων από Κατάλογο

Τώρα πρέπει να εντοπίσουμε κάθε εικόνα που θέλουμε να επεξεργαστούμε. Η list comprehension παρακάτω αντικατοπτρίζει ένα κοινό μοτίβο “list image files python”.

```python
def get_image_files(input_dir: str) -> List[str]:
    """
    Scans `input_dir` and returns a list of absolute paths
    for files ending with .png, .jpg, or .tif (case‑insensitive).
    """
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]
```

> **Edge case handling:** Η συνάρτηση αγνοεί υπο‑φακέλους (μπορείτε να προσθέσετε επανάληψη αργότερα) και φιλτράρει αυτόματα κρυφά αρχεία επειδή συνήθως δεν τελειώνουν με υποστηριζόμενες επεκτάσεις.

---

## Βήμα 4 – **Convert Scanned Images to Text**: Εκτέλεση Batch OCR

Οι περισσότερες βιβλιοθήκες OCR παρέχουν μέθοδο batch που είναι πολύ πιο γρήγορη από την επεξεργασία μιας εικόνας τη φορά. Δείτε πώς την καλούμε.

```python
def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    """
    Sends a list of image file paths to the OCR engine for batch recognition.
    Returns a list of OcrResult objects, preserving order.
    """
    # The fictional `recognize_batch` returns a list of results matching input order
    return engine.recognize_batch(image_paths)
```

> **Why batch?** Η αποστολή όλων των εικόνων ταυτόχρονα μειώνει το overhead (π.χ. την επανειλημμένη φόρτωση του μοντέλου OCR) και συχνά προσφέρει καλύτερη αξιοποίηση CPU/GPU.

---

## Βήμα 5 – **Recognize Text from Pictures**: Εμφάνιση Αποτελεσμάτων

Τέλος, διατρέχουμε τα ζευγάρια ονομάτων αρχείων και αποτελεσμάτων OCR, εκτυπώνοντας μια καθαρή κεφαλίδα για κάθε εικόνα.

```python
def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    """
    Prints the extracted text for each image, prefixed with the file name.
    """
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        # Some OCR engines store the plain text in a `.text` attribute
        print(result.text.strip())
        print()  # Blank line for readability
```

> **Tip:** Η `strip()` αφαιρεί κενά στην αρχή/τέλος που συχνά προσθέτει το OCR.

---

## Πλήρες Script – Συνδυάστε Όλα Μαζί

Παρακάτω είναι το πλήρες, εκτελέσιμο πρόγραμμα. Αποθηκεύστε το ως `batch_ocr.py` και τρέξτε `python batch_ocr.py <your_folder>`.

```python
#!/usr/bin/env python3
"""
Batch OCR script – extracts text from images in a given folder.
Usage: python batch_ocr.py /path/to/images
"""

import sys
import os
import ocr  # Replace with your OCR library if different
from typing import List

def create_engine() -> ocr.OcrEngine:
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto
    return engine

def get_image_files(input_dir: str) -> List[str]:
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]

def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    return engine.recognize_batch(image_paths)

def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        print(result.text.strip())
        print()

def main() -> None:
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <input_directory>")
        sys.exit(1)

    input_dir = sys.argv[1]

    if not os.path.isdir(input_dir):
        print(f"Error: '{input_dir}' is not a valid directory.")
        sys.exit(1)

    engine = create_engine()
    image_files = get_image_files(input_dir)

    if not image_files:
        print("No supported image files found in the directory.")
        sys.exit(0)

    ocr_results = run_batch_ocr(engine, image_files)
    display_results(image_files, ocr_results)

if __name__ == "__main__":
    main()
```

### Αναμενόμενη Έξοδος

Αν ο φάκελος περιέχει `invoice1.png` και `receipt.jpg`, μπορεί να δείτε:

```
--- invoice1.png ---
Invoice #12345
Date: 2024‑04‑01
Total: $256.78

--- receipt.jpg ---
Store: Coffee Corner
Item: Latte
Price: $4.50
```

Κάθε μπλοκ είναι σαφώς επισημασμένο, κάνοντας την επεξεργασία downstream (π.χ. αποθήκευση σε βάση δεδομένων) απλή.

---

## Διαχείριση Συνηθισμένων Προβλημάτων

| Πρόβλημα | Γιατί Συμβαίνει | Γρήγορη Λύση |
|----------|----------------|--------------|
| **Δεν εμφανίζεται κείμενο** | Η γλώσσα OCR δεν εντοπίστηκε ή η εικόνα είναι πολύ χαμηλής αντίθεσης. | Εξαναγκάστε μια γλώσσα (`engine.language = ocr.Language.English`) ή προεπεξεργαστείτε τις εικόνες (αυξήστε την αντίθεση). |
| **Σφάλμα μνήμης σε μεγάλα batch** | Η μηχανή προσπαθεί να φορτώσει όλες τις εικόνες ταυτόχρονα. | Χωρίστε το `image_files` σε τμήματα (`batch_size = 20`) και καλέστε επανειλημμένα το `recognize_batch`. |
| **Μη υποστηριζόμενη μορφή αρχείου** | Προσθέσατε ένα `.gif` ή `.bmp`. | Επεκτείνετε το tuple `supported_exts` ή μετατρέψτε τις εικόνες σε PNG/JPG εκ των προτέρων. |
| **Κατάρρευση Unicode** | Το OCR επιστρέφει bytes αντί για strings. | Βεβαιωθείτε ότι η βιβλιοθήκη OCR επιστρέφει Unicode (`result.text.decode('utf‑8')` αν χρειάζεται). |

---

## Επέκταση της Ροής Εργασίας

Τώρα που μπορείτε να **εξάγετε κείμενο από εικόνες**, σκεφτείτε τα επόμενα βήματα:

- **Εξαγωγή σε CSV** – Γράψτε κάθε όνομα αρχείου και το εξαγόμενο κείμενο σε ένα φύλλο εργασίας για αναλύσεις.
- **Παράλληλη επεξεργασία** – Χρησιμοποιήστε `concurrent.futures.ThreadPoolExecutor` για να διαχειριστείτε πολλαπλά batch ταυτόχρονα.
- **Ενσωμάτωση με cloud OCR** – Αντικαταστήστε τη τοπική μηχανή με Google Vision ή Azure OCR για μεγαλύτερη ακρίβεια σε σύνθετες διατάξεις.
- **Προσθήκη προεπεξεργασίας εικόνας** – Βιβλιοθήκες όπως Pillow ή OpenCV μπορούν να διορθώσουν κλίση, θόρυβο ή να εφαρμόσουν κατώφλι πριν το OCR, βελτιώνοντας τα αποτελέσματα.

Όλες αυτές οι ιδέες χρησιμοποιούν τις ίδιες βασικές συναρτήσεις που δημιουργήσαμε, οπότε δεν χρειάζεται να ξεκινήσετε από το μηδέν.

---

## Συμπέρασμα

Διασχίσαμε μια πλήρη λύση για **εξαγωγή κειμένου από εικόνες** σε Python, καλύπτοντας τα πάντα από το **list image files python** έως το **recognize text from pictures** και τελικά το **convert scanned images to text** σε ένα οργανωμένο batch. Το script είναι σκόπιμα απλό αλλά αρκετά ευέλικτο ώστε να λειτουργήσει ως βάση για μεγαλύτερα έργα—είτε ψηφιοποιείτε αποδείξεις, χτίζετε ένα αναζητήσιμο αρχείο, ή τροφοδοτείτε μια γραμμή εξαγωγής δεδομένων.

Δοκιμάστε το, προσαρμόστε τα βήματα προεπεξεργασίας, και παρακολουθήστε την ακρίβεια του OCR να ανεβαίνει. Αν αντιμετωπίσετε δυσκολίες, επιστρέψτε στον πίνακα “Διαχείριση Συνηθισμένων Προβλημάτων”· τα περισσότερα ζητήματα λύνουν με μια μικρή αλλαγή ρυθμίσεων.

Έτοιμοι για την επόμενη πρόκληση; Προσθέστε ένα βήμα μετατροπής PDF‑σε‑εικόνα χρησιμοποιώντας `pdf2image`, και τροφοδοτήστε αυτές τις εικόνες απευθείας στην ίδια ροή. Ο ουρανός είναι το όριο όταν συνδυάζετε OCR με το πλούσιο οικοσύστημα της Python.

Καλή προγραμματιστική, και εύχομαι το κείμενό σας να είναι πάντα ευανάγνωστο!

## Τι Θα Μάθετε Στη Σειρά Επόμενη;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Βήμα‑Βήμα](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Εξαγωγή Κειμένου από Εικόνες – Βασικά OCR με Aspose.OCR για Java](/ocr/english/java/ocr-basics/)
- [Πώς να εξάγετε κείμενο από εικόνα από URL χρησιμοποιώντας Aspose.OCR για Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}