---
category: general
date: 2026-06-28
description: Πώς να κάνετε ομαδική OCR σε Python—εξαγωγή κειμένου από εικόνες και
  μετατροπή σαρωμένων σελίδων σε κείμενο χρησιμοποιώντας ομαδική επεξεργασία OCR.
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert scanned pages to text
- batch OCR processing
language: el
og_description: Μάθετε πώς να κάνετε ομαδική OCR σε Python, να εξάγετε κείμενο από
  εικόνες και να μετατρέπετε σαρωμένες σελίδες σε κείμενο με αποδοτική ομαδική επεξεργασία
  OCR.
og_title: Πώς να κάνετε ομαδική OCR σε Python – Οδηγός βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR in Python—extract text from images and convert scanned
    pages to text using batch OCR processing.
  headline: How to Batch OCR in Python – Complete Guide to Extract Text from Images
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Πώς να κάνετε μαζική OCR σε Python – Πλήρης οδηγός για την εξαγωγή κειμένου
  από εικόνες
url: /el/python/general/how-to-batch-ocr-in-python-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να κάνετε Batch OCR σε Python – Πλήρης Οδηγός για την Εξαγωγή Κειμένου από Εικόνες

Αν αναρωτιέστε **πώς να κάνετε batch OCR σε Python**, βρίσκεστε στο σωστό μέρος. Αυτό το tutorial σας δείχνει έναν γρήγορο τρόπο για **να εξάγετε κείμενο από εικόνες** και **να μετατρέψετε σαρωμένες σελίδες σε κείμενο** χρησιμοποιώντας μια μόνο παρουσία του OCR engine. Τέλος με την αντιγραφή‑επικόλληση ενός αρχείου μετά το άλλο—αφήστε τον κώδικα να κάνει το βαρέως έργο.

Θα περάσουμε από όλα όσα χρειάζεστε: την εγκατάσταση της βιβλιοθήκης, τη φόρτωση ενός ολόκληρου φακέλου σαρώσεων, την εκτέλεση batch OCR επεξεργασίας και τη διαχείριση των αποτελεσμάτων με χάρη. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο script που μετατρέπει μια στοίβα PNG ή JPEG σε αρχεία κειμένου με δυνατότητα αναζήτησης σε δευτερόλεπτα.

## Τι Θα Χρειαστεί

* Εγκατεστημένο Python 3.9+ (ο κώδικας λειτουργεί και σε 3.8, αλλά το 3.9+ προσφέρει τις πιο πρόσφατες δυνατότητες typing).
* Μια σύγχρονη βιβλιοθήκη OCR—εδώ χρησιμοποιούμε **Aspose.OCR for Python via .NET**, η οποία εκθέτει την κλάση `OcrEngine` που φαίνεται στο αρχικό απόσπασμα.  
  ```bash
  pip install aspose-ocr
  ```
* Ένα φάκελο με σαρωμένες σελίδες (`page1.png`, `page2.png`, …). Οποιοδήποτε αρχείο μπορεί να ανοίξει το Pillow θα λειτουργήσει, έτσι και PDFs, TIFFs ή BMPs είναι εντάξει.
* Μια μικρή δόση περιέργειας—αν δεν έχετε ποτέ αυτοματοποιήσει τη μετατροπή εικόνας‑σε‑κείμενο, πρόκειται να δείτε γιατί το batch OCR είναι μια αλλαγή παιχνιδιού.

> **Pro tip:** Αν προτιμάτε μια καθαρά‑Python βιβλιοθήκη, αντικαταστήστε το `OcrEngine` με το `pytesseract.image_to_string`. Η υπόλοιπη λογική παραμένει ίδια.

## Πώς να κάνετε Batch OCR σε Python – Οδηγός Βήμα‑βήμα

Παρακάτω βρίσκεται το πλήρες, εκτελέσιμο script. Κάθε γραμμή είναι σχολιασμένη ώστε να βλέπετε *γιατί* κάθε κομμάτι είναι σημαντικό, όχι μόνο *τι* κάνει.

```python
# batch_ocr.py
import os
from aspose.ocr import OcrEngine, Image  # Aspose OCR library
from typing import List

def load_images(folder: str) -> List[Image]:
    """
    Scan a directory and return a list of Aspose.Image objects.
    Supports PNG, JPEG, BMP, and TIFF out of the box.
    """
    supported_ext = {".png", ".jpg", ".jpeg", ".bmp", ".tif", ".tiff"}
    images = []
    for filename in sorted(os.listdir(folder)):
        _, ext = os.path.splitext(filename)
        if ext.lower() in supported_ext:
            path = os.path.join(folder, filename)
            try:
                img = Image.from_file(path)
                images.append(img)
            except Exception as e:
                print(f"⚠️  Could not load {filename}: {e}")
    return images

def batch_ocr_process(images: List[Image]) -> List[str]:
    """
    Perform OCR on the whole batch at once.
    Returns a list of recognized strings, one per image.
    """
    engine = OcrEngine()          # Step 1: create an OCR engine instance
    # The recognize_batch method is optimized for bulk work.
    return engine.recognize_batch(images)

def save_results(texts: List[str], output_folder: str):
    """
    Write each page's text to a separate .txt file.
    """
    os.makedirs(output_folder, exist_ok=True)
    for idx, page_text in enumerate(texts, start=1):
        out_path = os.path.join(output_folder, f"page_{idx}.txt")
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(page_text)
        print(f"✅  Saved page {idx} → {out_path}")

def main():
    # -----------------------------------------------------------------
    # 1️⃣ Load the images you want to process
    # -----------------------------------------------------------------
    image_folder = "YOUR_DIRECTORY"          # <-- replace with your path
    images = load_images(image_folder)

    if not images:
        print("❌  No supported images found. Exiting.")
        return

    # -----------------------------------------------------------------
    # 2️⃣ Perform OCR on the whole batch at once
    # -----------------------------------------------------------------
    print(f"🔎  Running batch OCR on {len(images)} images...")
    page_texts = batch_ocr_process(images)

    # -----------------------------------------------------------------
    # 3️⃣ Output the recognized text for each page
    # -----------------------------------------------------------------
    for i, txt in enumerate(page_texts, start=1):
        print(f"\n--- Page {i} ---")
        print(txt[:200] + ("…" if len(txt) > 200 else ""))  # preview first 200 chars

    # -----------------------------------------------------------------
    # 4️⃣ (Optional) Save each page's text to a file
    # -----------------------------------------------------------------
    save_results(page_texts, "ocr_output")

if __name__ == "__main__":
    main()
```

### Αναμενόμενη Έξοδος

Η εκτέλεση του script σε έναν φάκελο με τρεις PNG σαρώσεις παράγει κάτι όπως:

```
🔎  Running batch OCR on 3 images...

--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit…

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore…

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco…
✅  Saved page 1 → ocr_output/page_1.txt
✅  Saved page 2 → ocr_output/page_2.txt
✅  Saved page 3 → ocr_output/page_3.txt
```

Η προεπισκόπηση δείχνει τους πρώτους 200 χαρακτήρες κάθε σελίδας, και το πλήρες κείμενο βρίσκεται στον φάκελο `ocr_output`.

## Εξαγωγή Κειμένου από Εικόνες Χρησιμοποιώντας Έναν Μοναδικό Engine

Γιατί δημιουργούμε **ένα** `OcrEngine` και το επαναχρησιμοποιούμε; Η δημιουργία του engine μπορεί να είναι δαπανηρή επειδή φορτώνει πακέτα γλώσσας και εγγενή DLLs. Με το να μοιράζεστε την ίδια παρουσία σε όλο το batch, εσείς:

* **Εξοικονομείτε μνήμη** – μόνο ένα σύνολο πόρων ζει στη RAM.
* **Αυξάνετε την ταχύτητα** – το engine παραμένει ζεστό, αποφεύγοντας επαναλαμβανόμενη αρχικοποίηση.
* **Διατηρείτε τη συνέπεια** – οι ίδιες ρυθμίσεις αναγνώρισης εφαρμόζονται σε κάθε σελίδα, κάτι που είναι ουσιώδες όταν θέλετε να **εξάγετε κείμενο από εικόνες** που έχουν την ίδια διάταξη.

Αν χρειάζεται να προσαρμόσετε την αναγνώριση (π.χ., να ενεργοποιήσετε τον ορθογραφικό έλεγχο ή να αλλάξετε τη γλώσσα), κάντε το *πριν* καλέσετε το `recognize_batch`. Όλες οι επόμενες σελίδες θα κληρονομήσουν αυτές τις ρυθμίσεις αυτόματα.

## Αποδοτική Μετατροπή Σαρωμένων Σελίδων σε Κείμενο

Η καρδιά του προβλήματος—**μετατροπή σαρωμένων σελίδων σε κείμενο**—λύνεται με το `engine.recognize_batch(images)`. Στο παρασκήνιο η βιβλιοθήκη επεξεργάζεται κάθε εικόνα σε μια ομάδα background threads, έτσι λαμβάνετε σχεδόν γραμμική κλιμάκωση σε πολυπύρηνους υπολογιστές. Μερικά πράγματα που πρέπει να θυμάστε:

* **Η ποιότητα της εικόνας μετρά** – 300 dpi ή περισσότερο δίνει τα καλύτερα αποτελέσματα. Αν οι σαρώσεις σας είναι χαμηλής ανάλυσης, σκεφτείτε up‑sampling με το Pillow πριν τις δώσετε στο engine.
* **Χρώμα vs. κλίμακα του γκρι** – Τα OCR engines συνήθως λειτουργούν πιο γρήγορα σε 8‑bit grayscale. Μπορείτε να προσθέσετε ένα βήμα προεπεξεργασίας:  
  ```python
  img = Image.from_file(path).convert_to_grayscale()
  ```
* **Υποστήριξη γλώσσας** – Το Aspose.OCR υποστηρίζει πάνω από 40 γλώσσες. Ορίστε `engine.language = "eng"` ή `"fra"` πριν την κλήση batch αν δεν εργάζεστε με αγγλικά.

## Καλές Πρακτικές για Batch OCR Επεξεργασία

Ακόμα και αν ο κώδικας παραπάνω είναι ήδη συνοπτικός, το batch OCR σε παραγωγικό επίπεδο συχνά απαιτεί μερικά επιπλέον μέτρα ασφαλείας:

| Πρόβλημα | Συνιστώμενη Προσέγγιση |
|----------|------------------------|
| **Μεγάλες παρτίδες (> 500 αρχεία)** | Διαχωρίστε σε τμήματα των 100–200 εικόνων για να διατηρήσετε το αποτύπωμα μνήμης μέτριο. |
| **Κατεστραμμένα ή μη υποστηριζόμενα αρχεία** | Η βοηθητική συνάρτηση `load_images` ήδη συλλαμβάνει εξαιρέσεις και καταγράφει προειδοποίηση· μπορείτε επίσης να γράψετε fallback για να παραλείψετε ή να μετακινήσετε τα κακά αρχεία. |
| **Παρακολούθηση προόδου** | Τυλίξτε το `recognize_batch` σε βρόχο που αποδίδει (yield) μετά από κάθε εικόνα αν η βιβλιοθήκη εκθέτει callbacks ανά‑εικόνα. |
| **Μετα‑επεξεργασία** | Εκτελέστε ορθογραφικό έλεγχο ή καθαρισμό με regex στα αποτελέσματα για να βελτιώσετε την αναζητησιμότητα. |
| **Παραλληλισμός** | Αν έχετε ένα multi‑node setup, διανείμετε φακέλους σε workers και συγχωνεύστε τα `.txt` αρχεία στο τέλος. |

Αυτές οι συμβουλές σας βοηθούν να κλιμακώσετε το **batch OCR processing** από μερικές σελίδες σε χιλιάδες χωρίς να καταρρεύσει το script σας.

## Συχνές Ερωτήσεις

**Q: Μπορώ να το χρησιμοποιήσω απευθείας με PDFs;**  
A: Απόλυτα. Μετατρέψτε κάθε σελίδα PDF σε εικόνα πρώτα (π.χ., χρησιμοποιώντας το `pdf2image`) και δώστε τη λίστα που προκύπτει στο `recognize_batch`. Το υπόλοιπο pipeline παραμένει αμετάβλητο


## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε σε πρόσθετα χαρακτηριστικά του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Βήμα‑βήμα](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Εξαγωγή Κειμένου από Εικόνες Χρησιμοποιώντας OCR Λειτουργία σε Φακέλους](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Πώς να Εξάγετε Κείμενο από Αρχεία ZIP Χρησιμοποιώντας Aspose.OCR για .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}