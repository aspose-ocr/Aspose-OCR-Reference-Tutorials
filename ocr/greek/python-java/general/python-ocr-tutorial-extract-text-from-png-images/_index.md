---
category: general
date: 2026-06-25
description: Μάθημα OCR σε Python που δείχνει πώς να εξάγετε κείμενο από αρχεία PNG,
  να διαβάζετε κείμενο σε εικόνα και να αναγνωρίζετε κείμενο εικόνας χρησιμοποιώντας
  μια απλή, μηχανή χωρίς άδεια.
draft: false
keywords:
- python ocr tutorial
- extract text png
- read text image
- recognize image text
- load image for ocr
language: el
og_description: Το σεμινάριο Python OCR σας διδάσκει πώς να φορτώνετε εικόνα για OCR,
  να εξάγετε κείμενο από αρχεία PNG και να αναγνωρίζετε το κείμενο της εικόνας με
  λίγες μόνο γραμμές κώδικα.
og_title: Python OCR Οδηγός – Εξαγωγή κειμένου από PNG
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Python OCR tutorial that shows you how to extract text PNG files, read
    text image, and recognize image text using a simple, license‑free engine.
  headline: 'Python OCR Tutorial: Extract Text from PNG Images'
  type: TechArticle
- description: Python OCR tutorial that shows you how to extract text PNG files, read
    text image, and recognize image text using a simple, license‑free engine.
  name: 'Python OCR Tutorial: Extract Text from PNG Images'
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer (the library works with 3.7+ but 3.8+ is recommended).
      - Basic familiarity with pip and virtual environments. - An image file named
      `sample.png` (or any PNG you’d like to test) saved in a folder you can reference.'
  - name: 1. Low Contrast or Dark Backgrounds
    text: '```python # Increase contrast before recognition (optional step) image
      = image.adjust_contrast(1.5) # 1.0 = no change, >1 = higher contrast result
      = engine.recognize(image) ```'
  - name: 2. Skewed Text Lines
    text: '```python # Auto‑deskew the image image = image.deskew() result = engine.recognize(image)
      ```'
  - name: 3. Non‑English Characters
    text: 'If your PNG contains accented letters or non‑Latin scripts, initialise
      the engine with the appropriate language pack:'
  - name: 4. Very Large Images
    text: 'Processing a 4000×3000 PNG can be slow. Downscale it while preserving readability:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- Tutorial
title: 'Python OCR Tutorial: Εξαγωγή κειμένου από εικόνες PNG'
url: /el/python-java/general/python-ocr-tutorial-extract-text-from-png-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR Tutorial – Εξαγωγή Κειμένου από PNG Εικόνες

Έχετε αναρωτηθεί ποτέ πώς το **python ocr tutorial** μπορεί να μετατρέψει ένα στιγμιότυπο οθνης από απόδειξη σε επεξεργάσιμο κείμενο; Δεν είστε μόνοι. Σε πολλά πραγματικά έργα χρειάζεται να *read text image* αρχεία γρήγορα, και το να το κάνετε μόνοι σας είναι καλύτερο από το να αντιγράφετε‑επικολλάτε από ένα GUI κάθε φορά.  

Σε αυτόν τον οδηγό θα περάσουμε από ένα πρακτικό παράδειγμα που **extracts text PNG** αρχεία, σας δείχνει πώς να *load image for OCR*, και τελικά εκτυπώνει το αποτέλεσμα του *recognize image text* — όλα με μια δωρεάν, μόνο‑αξιολόγησης μηχανή OCR. Χωρίς κλειδιά άδειας, χωρίς βαριές εξαρτήσεις — μόνο απλό Python και μερικά μικρά πακέτα.

## Τι Θα Μάθετε

- Πώς να εγκαταστήσετε και να εισάγετε τη ελαφριά βιβλιοθήκη OCR.
- Τα ακριβή βήματα για **load image for OCR** και τη διαχείριση κοινών παγίδων.
- Τρόποι για **read text image** αρχεία διαφορετικής ποιότητας.
- Συμβουλές για βελτίωση της ακρίβειας όταν **extract text png** αρχεία.
- Πώς να εμφανίσετε τη αναγνωρισμένη συμβολοσειρά και προαιρετικά να την γράψετε στο δίσκο.

Στο τέλος αυτού του οδηγού θα έχετε ένα επαναχρησιμοποιήσιμο script που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο χρειάζεται **recognize image text** άμεσα. Χωρίς μαγεία, μόνο καθαρός κώδικας και εξηγήσεις.

### Προαπαιτούμενα

- Python 3.8 ή νεότερο (η βιβλιοθήκη λειτουργεί με 3.7+ αλλά συνιστάται 3.8+).
- Βασική εξοικείωση με pip και εικονικά περιβάλλοντα.
- Ένα αρχείο εικόνας με όνομα `sample.png` (ή οποιοδήποτε PNG θέλετε να δοκιμάσετε) αποθηκευμένο σε φάκελο που μπορείτε να αναφέρετε.

Αν κάτι από αυτά σας φαίνεται άγνωστο, κάντε ένα διάλειμμα για ένα λεπτό και ρυθμίστε τα — εμπιστευτείτε με, η ανταμοιβή αξίζει.

---

## Python OCR Tutorial – Ρύθμιση της Μηχανής

Πρώτα απ' όλα: χρειαζόμαστε ένα αντικείμενο μηχανής OCR. Η βιβλιοθήκη που θα χρησιμοποιήσουμε είναι ένας μικρός wrapper γύρω από μια εγγενή μηχανή OCR που λειτουργεί έτοιμη για αξιολόγηση. Δεν απαιτεί κλειδί άδειας, κάτι που κάνει το *python ocr tutorial* ιδανικό για γρήγορα πρωτότυπα.

```python
# Step 1: Install the OCR package (run once in your terminal)
# pip install simple-ocr-lib

# Step 2: Import the library and create an engine instance
import ocr

# No license needed for evaluation mode – the engine is ready to go
engine = ocr.OcrEngine()
```

**Why this matters:** Η δημιουργία της μηχανής απομονώνει το runtime OCR από το υπόλοιπο κώδικα, επιτρέποντάς σας να το επαναχρησιμοποιήσετε για πολλές εικόνες χωρίς επανεκκίνηση βαρέων πόρων κάθε φορά.

---

## Load Image for OCR – Ανάγνωση Αρχείου PNG

Τώρα που η μηχανή υπάρχει, πρέπει να *load image for OCR*. Η μέθοδος `Image.load` της βιβλιοθήκης δέχεται μια διαδρομή και αυτόματα αποκωδικοποιεί PNG, JPEG, BMP και μερικές άλλες μορφές.

```python
# Step 3: Load the PNG you want to process
image_path = "YOUR_DIRECTORY/sample.png"   # replace with your actual path
image = ocr.Image.load(image_path)
```

> **Pro tip:** Αν το PNG σας περιέχει κανάλι άλφα, η βιβλιοθήκη θα το αφαιρέσει αυτόματα. Ωστόσο, για τα καλύτερα αποτελέσματα σε εργασίες *read text image*, κρατήστε την εικόνα σε γκρι κλίμακα — αυτό μειώνει τον θόρυβο και επιταχύνει την αναγνώριση.

---

## Recognize Image Text – Εκτέλεση της Μηχανής OCR

Με το αντικείμενο εικόνας έτοιμο, μπορούμε τελικά να **recognize image text**. Αυτό είναι ο πυρήνας του *python ocr tutorial* και απαιτεί μόνο μία γραμμή κώδικα.

```python
# Step 4: Perform OCR on the loaded image
result = engine.recognize(image)
```

**What happens under the hood?** Η μηχανή εκτελεί μια σειρά από φίλτρα προεπεξεργασίας (deskew, binarization) πριν τροφοδοτήσει το bitmap σε ένα νευρωνικό δίκτυο εκπαιδευμένο σε εκατομμύρια χαρακτήρες. Γι' αυτό συχνά λαμβάνετε εκπληκτικά ακριβή αποτελέσματα ακόμη και σε PNG χαμηλής ανάλυσης.

---

## Εμφάνιση και Αποθήκευση του Εξαγόμενου Κειμένου

Το να έχετε το αποτέλεσμα είναι υπέροχο, αλλά πιθανότατα θέλετε να το δείτε ή να το αποθηκεύσετε κάπου. Το αντικείμενο `result` εκθέτει ένα χαρακτηριστικό `text` που περιέχει την απλή συμβολοσειρά εξόδου.

```python
# Step 5: Print the recognized text to the console
print("Eval-mode result:", result.text)

# Optional: Save the text to a .txt file for later use
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

**Expected output** (υπόθεση ότι το `sample.png` περιέχει “Hello, OCR!”):

```
Eval-mode result: Hello, OCR!
```

Αν λάβετε ακατάλληλο κείμενο αντί για αναγνώσιμους χαρακτήρες, ελέγξτε την επόμενη ενότητα για κοινές διορθώσεις.

---

## Διαχείριση Συνηθισμένων Προβλημάτων Κατά την Εξαγωγή Κειμένου PNG

Ακόμη και οι καλύτερες μηχανές OCR αντιμετωπίζουν προβλήματα με ορισμένες εικόνες. Παρακάτω είναι τυπικά εμπόδια και πώς να τα ξεπεράσετε.

### 1. Χαμηλή Αντίθεση ή Σκούρο Φόντο

```python
# Increase contrast before recognition (optional step)
image = image.adjust_contrast(1.5)   # 1.0 = no change, >1 = higher contrast
result = engine.recognize(image)
```

### 2. Λοξές Γραμμές Κειμένου

```python
# Auto‑deskew the image
image = image.deskew()
result = engine.recognize(image)
```

### 3. Μη‑Αγγλικοί Χαρακτήρες

Αν το PNG σας περιέχει τονισμένα γράμματα ή μη‑λατινικά σενάρια, αρχικοποιήστε τη μηχανή με το κατάλληλο πακέτο γλώσσας:

```python
engine = ocr.OcrEngine(languages=["eng", "spa"])   # English + Spanish
```

### 4. Πολύ Μεγάλες Εικόνες

Η επεξεργασία ενός PNG 4000×3000 μπορεί να είναι αργή. Μειώστε το μέγεθός του διατηρώντας την αναγνωσιμότητα:

```python
image = image.resize(width=1024)   # keep aspect ratio
result = engine.recognize(image)
```

Αυτές οι προσαρμογές αποτελούν μέρος ενός στιβαρού *python ocr tutorial* που λειτουργεί πέρα από το ευνοϊκό σενάριο.

---

## Πλήρες Script – Λύση σε Ένα Αρχείο

Παρακάτω είναι το πλήρες, έτοιμο‑για‑εκτέλεση script που ενσωματώνει όλα τα βήματα και τις προαιρετικές βελτιώσεις που συζητήθηκαν. Αντιγράψτε‑και‑επικολλήστε το στο `ocr_extract.py` και εκτελέστε `python ocr_extract.py`.

```python
# ocr_extract.py
# Complete Python OCR tutorial – extract text from PNG images

import ocr
import sys
import os

def main(image_path):
    # Verify the file exists
    if not os.path.isfile(image_path):
        print(f"Error: File not found → {image_path}")
        sys.exit(1)

    # 1️⃣ Create the OCR engine (evaluation mode, no license needed)
    engine = ocr.OcrEngine()

    # 2️⃣ Load the image – this is the "load image for OCR" step
    image = ocr.Image.load(image_path)

    # Optional preprocessing for better accuracy
    # Uncomment any of the following lines as needed:
    # image = image.adjust_contrast(1.5)   # boost contrast
    # image = image.deskew()               # correct skew
    # image = image.resize(width=1024)     # downscale large images

    # 3️⃣ Recognize the text
    result = engine.recognize(image)

    # 4️⃣ Output the result
    print("Eval-mode result:", result.text)

    # 5️⃣ Save to a .txt file (useful for batch processing)
    txt_path = os.path.splitext(image_path)[0] + "_extracted.txt"
    with open(txt_path, "w", encoding="utf-8") as out_file:
        out_file.write(result.text)
    print(f"Extracted text saved to {txt_path}")

if __name__ == "__main__":
    # Pass the image path as a command‑line argument, e.g.:
    # python ocr_extract.py ./samples/sample.png
    if len(sys.argv) < 2:
        print("Usage: python ocr_extract.py <path_to_png>")
        sys.exit(1)
    main(sys.argv[1])
```

**Run it:**  
```bash
python ocr_extract.py ./sample.png
```

Θα πρέπει να δείτε τη αναγνωρισμένη συμβολοσειρά εκτυπωμένη και ένα αρχείο `sample_extracted.txt` να δημιουργηθεί δίπλα στην εικόνα.

---

## Οπτική Επισκόπηση

![Python OCR tutorial – load image for OCR and extract text from PNG](/images/python-ocr-flow.png)

*Alt text:* *Διάγραμμα Python OCR tutorial που δείχνει τη ροή από τη φόρτωση μιας εικόνας για OCR έως την εξαγωγή κειμένου PNG.*

Το διάγραμμα απεικονίζει την γραμμική πρόοδο από **load image for OCR** → **recognize image text** → **extract text PNG** και επισημαίνει πού μπορείτε να ενσωματώσετε βήματα προεπεξεργασίας.

---

## Συμπέρασμα

Μόλις ολοκληρώσαμε ένα **python ocr tutorial** που δείχνει πώς να *load image for OCR*, *recognize image text*, και τελικά **extract text png** αρχεία με μόνο μερικές εντολές Python. Το script είναι πλήρως λειτουργικό, διαχειρίζεται κοινές ακραίες περιπτώσεις, και μπορεί να επεκταθεί για επεξεργασία παρτίδων ή πολυγλωσσική υποστήριξη.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να τροφοδοτήσετε τη μηχανή με PDF που έχουν μετατραπεί σε εικόνες, πειραματιστείτε με διαφορετικά πακέτα γλώσσας, ή ενσωματώστε το βήμα OCR σε ένα Flask API ώστε η web εφαρμογή σας να διαβάζει ανεβασμένα στιγμιότυπα άμεσα. Οι δυνατότητες αυτοματοποίησης *read text image* είναι πρακτικά ατελείωτες.

Έχετε ερωτήσεις ή μια δύσκολη εικόνα που δεν μπορείτε να λύσετε; Αφήστε ένα σχόλιο παρακάτω και ας το αντιμετωπίσουμε μαζί. Καλό κώδικα!

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε σε πρόσθετα χαρακτηριστικά API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Βήμα‑Βήμα](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Εξαγωγή Κειμένου από Εικόνα – Βελτιστοποίηση OCR με Aspose.OCR για .NET](/ocr/english/net/ocr-optimization/)
- [Πώς να OCR Κείμενο Εικόνας με Γλώσσα Χρησιμοποιώντας Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}