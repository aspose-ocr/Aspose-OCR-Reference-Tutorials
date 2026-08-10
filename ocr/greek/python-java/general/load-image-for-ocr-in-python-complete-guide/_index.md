---
category: general
date: 2026-07-05
description: Μάθετε πώς να φορτώνετε εικόνα για OCR σε Python και να εξάγετε κείμενο
  από την εικόνα με στυλ Python. Αυτός ο οδηγός βήμα‑βήμα δείχνει πώς να χρησιμοποιείτε
  τη βιβλιοθήκη OCR αποδοτικά.
draft: false
keywords:
- load image for OCR
- extract text from image python
- how to use OCR library
- Python OCR tutorial
- OCR performance metrics
language: el
og_description: Φορτώστε εικόνα για OCR σε Python και εξάγετε κείμενο από την εικόνα
  με στυλ Python. Ακολουθήστε αυτόν τον οδηγό για να μάθετε πώς να χρησιμοποιείτε
  τη βιβλιοθήκη OCR με μετρικές απόδοσης.
og_title: Φόρτωση εικόνας για OCR σε Python – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Learn how to load image for OCR in Python and extract text from image
    python style. This step‑by‑step tutorial shows how to use OCR library efficiently.
  headline: Load Image for OCR in Python – Complete Guide
  type: TechArticle
tags:
- Python
- OCR
- Image Processing
title: Φόρτωση εικόνας για OCR σε Python – Πλήρης οδηγός
url: /el/python-java/general/load-image-for-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Φόρτωση Εικόνας για OCR σε Python – Πλήρης Οδηγός

Ποτέ χρειάστηκε να **φορτώσετε εικόνα για OCR** σε Python αλλά δεν ήξερατε από πού να ξεκινήσετε; Δεν είστε μόνοι· πολλοί προγραμματιστές συναντούν αυτό το εμπόδιο όταν προσπαθούν για πρώτη φορά να εξάγουν κείμενο από εικόνες. Σε αυτό το tutorial θα περάσουμε από ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει **πώς να χρησιμοποιήσετε τη βιβλιοθήκη OCR**, από την εγκατάσταση του πακέτου μέχρι την εξαγωγή κάθε χαρακτήρα και ακόμη τη μέτρηση της απόδοσης.

Φανταστείτε ότι δημιουργείτε μια εφαρμογή σάρωσης αποδείξεων ή έναν αυτοματοποιημένο επεξεργαστή φορμών. Μόλις μπορείτε αξιόπιστα να **φορτώσετε εικόνα για OCR** και να εξάγετε το κείμενο, το υπόλοιπο pipeline εντάσσεται αμέσως. Ας βουτήξουμε και ας το κάνουμε λειτουργικό σήμερα.

## Τι Θα Κερδίσετε

- Ένα καθαρό script Python που **φορτώνει εικόνα για OCR**, εκτελεί αναγνώριση και εκτυπώνει τόσο το εξαγόμενο κείμενο όσο και τα στατιστικά απόδοσης.  
- Κατανόηση του γιατί κάθε βήμα είναι σημαντικό, όχι μόνο του «τι».  
- Συμβουλές για την αντιμετώπιση κοινών παγίδων (λανθασμένη γλώσσα, μεγάλα αρχεία, αυξήσεις μνήμης).  
- Ένα γρήγορο roadmap για την επέκταση του παραδείγματος—προσθήκη προεπεξεργασίας, επεξεργασία παρτίδας ή αλλαγή σε διαφορετική μηχανή OCR.

### Προαπαιτούμενα

- Python 3.8+ εγκατεστημένο (ο κώδικας χρησιμοποιεί f‑strings).  
- Βασική εξοικείωση με pip και εικονικά περιβάλλοντα.  
- Ένα αρχείο εικόνας που θέλετε να επεξεργαστείτε (PNG, JPEG, TIFF λειτουργούν όλα).  

Καμία βαριά εξάρτηση εκτός από τη βιβλιοθήκη OCR, οπότε θα είστε έτοιμοι σε λίγα λεπτά.

---

## Step 1: Install and Import the OCR Library

Πρώτα, χρειαζόμαστε ένα πακέτο OCR για Python. Το απόσπασμα που δημοσιεύσατε χρησιμοποιεί ένα γενικό module `ocr`, οπότε ας υποθέσουμε ότι χρησιμοποιείτε το δημοφιλές **ocr** wrapper που εγκαθίσταται με `pip install ocr`. Αν προτιμάτε `pytesseract`, οι έννοιες παραμένουν ίδιες· απλώς αντικαταστήστε τις γραμμές εισαγωγής.

```bash
# Create a fresh virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # on Windows use `venv\Scripts\activate`

# Install the OCR library
pip install ocr
```

Τώρα εισάγετε τα στοιχεία που θα χρειαστείτε:

```python
import ocr               # The main OCR package
import os                # For path handling and optional file checks
```

> **Pro tip:** Κρατήστε το `requirements.txt` τακτοποιημένο—απλώς προσθέστε `ocr==<latest>` ώστε οι μελλοντικές κατασκευές να είναι αναπαραγώγιμες.

---

## Step 2: Initialize the OCR Engine and Set the Language

Γιατί να ασχοληθείτε με ένα ρητό αντικείμενο μηχανής; Οι περισσότερες μηχανές OCR (Tesseract, EasyOCR κ.λπ.) απαιτούν φάση διαμόρφωσης όπου λέτε στη μηχανή ποιο μοντέλο γλώσσας να φορτώσει. Η παράλειψη αυτού του βήματος μπορεί να οδηγήσει σε ακατάλληλη έξοδο ή σημαντικά πιο αργή επεξεργασία.

```python
# Step 2: Initialize the OCR engine and set the language
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH   # Switch to 'ocr.Language.SPANISH' for Spanish text
```

Αν χρειαστεί ποτέ να επεξεργαστείτε πολυγλωσσικά έγγραφα, απλώς αλλάξτε το χαρακτηριστικό `language` ή περάστε μια λίστα—οι περισσότερες βιβλιοθήκες δέχονται μια συμβολοσειρά διαχωρισμένη με κόμμα.

---

## Step 3: Load Image for OCR

Εδώ είναι η καρδιά του tutorial: **load image for OCR**. Η μέθοδος `ocr.Image.load` διαβάζει το αρχείο σε μια εσωτερική μορφή που καταλαβαίνει η μηχανή. Επίσης εκτελεί μια μικρή επικύρωση (π.χ., επιβεβαιώνει ότι το αρχείο υπάρχει).

```python
# Step 3: Load the image you want to process
image_path = os.path.join("YOUR_DIRECTORY", "performance_test.png")

# Guard against missing files – a small but often‑overlooked edge case
if not os.path.isfile(image_path):
    raise FileNotFoundError(f"Cannot find image at {image_path}")

image = ocr.Image.load(image_path)
```

> **Why this matters:** Η φόρτωση της εικόνας νωρίς σας επιτρέπει να ελέγξετε τις διαστάσεις της, το DPI ή τη χρωματική λειτουργία—πληροφορίες που μπορεί να χρειαστείτε για προεπεξεργασία αργότερα (π.χ., μετατροπή σε γκρι κλίμακα).

---

## Step 4: Perform OCR Recognition

Τώρα τελικά **extract text from image python** style. Η κλήση `engine.recognize` κάνει το βαρέως κόστους έργο: τρέχει το νευρωνικό δίκτυο ή τον κλασικό αλγόριθμο αντιστοίχισης, και επιστρέφει ένα αντικείμενο αποτελέσματος που περιέχει το ακατέργαστο κείμενο, τις βαθμολογίες εμπιστοσύνης και τα χρονικά μετρικά.

```python
# Step 4: Perform OCR recognition on the image
result = engine.recognize(image)
```

Το αντικείμενο `result` συνήθως έχει τα εξής χαρακτηριστικά:

- `text` – η απλή συμβολοσειρά των αναγνωρισμένων χαρακτήρων.  
- `confidence` – αριθμός κινητής υποδιαστολής μεταξύ 0 και 1 που υποδεικνύει τη συνολική βεβαιότητα.  
- `processing_time` – χιλιοστά του δευτερολέπτου που η μηχανή δαπάνησε για αυτήν την εικόνα.  
- `memory_used` – kilobytes που διατέθηκαν κατά τη λειτουργία.

---

## Step 5: Output Extracted Text and Performance Metrics

Ας εκτυπώσουμε τα πάντα σε μια τακτοποιημένη μορφή. Αυτό όχι μόνο ικανοποιεί την περιέργεια «πώς να χρησιμοποιήσετε τη βιβλιοθήκη OCR», αλλά σας δίνει επίσης γρήγορη ανάδραση για profiling αργότερα.

```python
# Step 5: Output the recognized text and performance metrics
print("=== OCR RESULT ===")
print(result.text)                         # The extracted text
print(f"Confidence: {result.confidence:.2%}")  # Convert to percentage
print(f"Time taken: {result.processing_time} ms")
print(f"Memory used: {result.memory_used} KB")
```

**Expected output** (το πραγματικό κείμενο σας θα διαφέρει ανάλογα με την εικόνα):

```
=== OCR RESULT ===
Performance Test
Confidence: 98.73%
Time taken: 124 ms
Memory used: 58 KB
```

Αν η εμπιστοσύνη είναι χαμηλή, σκεφτείτε βήματα προεπεξεργασίας όπως η δυαδικοποίηση ή η διόρθωση κλίσης—αυτά καλύπτονται στην ενότητα «επόμενα βήματα».

---

## Step 6: Handling Edge Cases and Common Pitfalls

Ακόμη και ένα τέλειο script μπορεί να κολλήσει σε πραγματικά δεδομένα. Παρακάτω είναι μερικά σενάρια που μπορεί να συναντήσετε και πώς να τα προστατέψετε.

| Situation | What to Check | Quick Fix |
|-----------|---------------|-----------|
| **Wrong language** | `engine.language` not matching the text | Set `engine.language = ocr.Language.FRENCH` or use `engine.languages = ["ENGLISH", "SPANISH"]`. |
| **Huge image ( > 5 MB )** | Memory spikes, longer `processing_time` | Downscale with `PIL.Image.thumbnail` before loading. |
| **No text found** | `result.text` empty, confidence 0 | Verify image contrast; try adaptive thresholding. |
| **Library not found** | ImportError on `ocr` | Ensure you installed the correct package (`pip install ocr`) and activated your virtual env. |

```python
# Example: simple preprocessing with Pillow
from PIL import Image as PilImage

def preprocess(path):
    img = PilImage.open(path)
    # Convert to grayscale and resize to a max of 1024px width
    img = img.convert("L")
    img.thumbnail((1024, 1024))
    # Save to a temporary file that OCR can read
    tmp_path = "temp_preprocessed.png"
    img.save(tmp_path)
    return ocr.Image.load(tmp_path)

# Use the helper
image = preprocess(image_path)
result = engine.recognize(image)
```

---

## Step 7: Putting It All Together – Full Script

Παρακάτω είναι το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα που **loads image for OCR**, εξάγει το κείμενο και εκτυπώνει αριθμούς απόδοσης. Αντιγράψτε‑και‑επικολλήστε το στο `ocr_demo.py` και τρέξτε `python ocr_demo.py`.

```python
#!/usr/bin/env python3
"""
Load Image for OCR in Python – Full Example
Demonstrates how to use OCR library, extract text from image python, and measure performance.
"""

import os
import ocr
from PIL import Image as PilImage   # Optional, for preprocessing

def preprocess(image_path: str) -> ocr.Image:
    """Resize and grayscale the image to improve OCR accuracy."""
    img = PilImage.open(image_path)
    img = img.convert("L")
    img.thumbnail((1024, 1024))
    tmp_path = "temp_preprocessed.png"
    img.save(tmp_path)
    return ocr.Image.load(tmp_path)

def main():
    # 1️⃣ Initialize engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # 2️⃣ Locate image
    image_path = os.path.join("YOUR_DIRECTORY", "performance_test.png")
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # 3️⃣ Load image for OCR (with optional preprocessing)
    image = preprocess(image_path)          # Swap with ocr.Image.load(image_path) if you skip preprocessing

    # 4️⃣ Recognize text
    result = engine.recognize(image)

    # 5️⃣ Show results
    print("=== OCR RESULT ===")
    print(result.text)
    print(f"Confidence: {result.confidence:.2%}")
    print(f"Time taken: {result.processing_time} ms")
    print(f"Memory used: {result.memory_used} KB")

if __name__ == "__main__":
    main()
```

**Run it**:

```bash
python ocr_demo.py
```

Θα πρέπει να δείτε το κείμενο από το `performance_test.png` μαζί με το χρόνο επεξεργασίας και τη χρήση μνήμης. Αν οι αριθμοί φαίνονται περίεργοι, ελέγξτε ξανά τη λειτουργία προεπεξεργασίας ή επαληθεύστε τη ρύθμιση γλώσσας.

---

## Conclusion

Μόλις καλύψαμε πώς να **load image for OCR** σε Python, **extract text from image python** style, και να μετρήσουμε την ταχύτητα της λειτουργίας—βασικές δεξιότητες για όποιον ρωτά *how to use OCR library* σε πραγματικό έργο. Το script είναι αρκετά μικρό ώστε να το καταλάβετε με μια ματιά, αλλά αρκετά ευέλικτο ώστε να επεκταθεί σε batch jobs, cloud functions ή ακόμη και mobile back‑ends.

Τι είναι το επόμενο; Δοκιμάστε να αντικαταστήσετε το `ocr` με `pytesseract` και δείτε πώς αλλάζει το API, πειραματιστείτε με διαφορετικά language packs, ή ενσωματώστε το αποτέλεσμα σε μια βάση δεδομένων για αναζητήσιμα PDFs. Η βάση είναι τώρα σταθερή και μπορείτε να χτίσετε πάνω της χωρίς να ξαναεφευρίσετε τον τροχό.

Έχετε ερωτήσεις για συγκεκριμένο τύπο εικόνας, ή θέλετε να μάθετε πώς να διαχειριστείτε PDFs άμεσα; Αφήστε ένα σχόλιο.

## What Should You Learn Next?

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε πρόσθετα χαρακτηριστικά του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση των δικών σας έργων.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}