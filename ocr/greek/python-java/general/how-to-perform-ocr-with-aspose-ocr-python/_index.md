---
category: general
date: 2026-06-25
description: Πώς να εκτελέσετε OCR με το Aspose OCR Python – μάθετε πώς να φορτώνετε
  εικόνα OCR, να επεξεργάζεστε εικόνα OCR και να εξάγετε αποτελέσματα JSON σε λίγα
  λεπτά.
draft: false
keywords:
- how to perform OCR
- aspose OCR python
- load image OCR
- process image OCR
language: el
og_description: Πώς να εκτελέσετε OCR με το Aspose OCR Python. Ακολουθήστε αυτόν τον
  οδηγό για να φορτώσετε OCR εικόνας, να επεξεργαστείτε OCR εικόνας και να αναλύσετε
  την έξοδο JSON εύκολα.
og_title: Πώς να εκτελέσετε OCR με το Aspose OCR Python
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: How to perform OCR with Aspose OCR Python – learn to load image OCR,
    process image OCR, and extract JSON results in minutes.
  headline: How to Perform OCR with Aspose OCR Python
  type: TechArticle
- description: How to perform OCR with Aspose OCR Python – learn to load image OCR,
    process image OCR, and extract JSON results in minutes.
  name: How to Perform OCR with Aspose OCR Python
  steps:
  - name: Creating an OCR engine instance.
    text: Creating an OCR engine instance.
  - name: Loading an image for OCR.
    text: Loading an image for OCR.
  - name: Processing the image OCR.
    text: Processing the image OCR.
  - name: Converting the result to JSON.
    text: Converting the result to JSON.
  - name: Parsing and printing useful information.
    text: Parsing and printing useful information.
  - name: '**File format matters** – While TIFF works great for scanned documents,
      PNG is often better for screenshots, and JPEG for photographs.'
    text: '**File format matters** – While TIFF works great for scanned documents,
      PNG is often better for screenshots, and JPEG for photographs.'
  - name: '**Resolution** – Aspose OCR performs best with 300 dpi or higher. If you
      see low confidence scores, consider up‑sampling the image before loading.'
    text: '**Resolution** – Aspose OCR performs best with 300 dpi or higher. If you
      see low confidence scores, consider up‑sampling the image before loading.'
  - name: '**Multi‑page files** – If your TIFF contains several pages, `image = ocr.Image.load(path)`
      will give you a stack; you can iterate with `for page in image.pages:` and call
      `engine.recognize(page)` for each.'
    text: '**Multi‑page files** – If your TIFF contains several pages, `image = ocr.Image.load(path)`
      will give you a stack; you can iterate with `for page in image.pages:` and call
      `engine.recognize(page)` for each.'
  type: HowTo
tags:
- OCR
- Python
- Aspose
title: Πώς να εκτελέσετε OCR με το Aspose OCR Python
url: /el/python-java/general/how-to-perform-ocr-with-aspose-ocr-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εκτελέσετε OCR με Aspose OCR Python

Έχετε αναρωτηθεί ποτέ **πώς να εκτελέσετε OCR** σε απόδειξη, τιμολόγιο ή οποιοδήποτε σαρωμένο έγγραφο χρησιμοποιώντας Python; Δεν είστε ο μόνος. Σε πολλά πραγματικά έργα, η εξαγωγή κειμένου από εικόνες είναι το πρώτο βήμα προς την αυτοματοποίηση, την ανάλυση ή την αρχειοθέτηση.  

Τα καλά νέα; Με **Aspose OCR Python** μπορείτε να φορτώσετε image OCR, να επεξεργαστείτε image OCR και να λάβετε ένα τακτοποιημένο JSON payload με λίγες μόνο γραμμές κώδικα. Παρακάτω θα δείτε ένα πλήρες, έτοιμο‑για‑εκτέλεση script, καθώς και τη λογική πίσω από κάθε βήμα ώστε να κατανοήσετε πραγματικά *γιατί* ο κώδικας φαίνεται όπως είναι.

## Τι Καλύπτει Αυτό το Tutorial

- Ρύθμιση της μηχανής Aspose OCR σε Python  
- **Load image OCR** σωστά, διαχειριζόμενοι κοινές μορφές όπως TIFF, PNG και JPEG  
- **Process image OCR** και μετατροπή του αποτελέσματος σε JSON  
- Ανάλυση του JSON για την ανάκτηση χρήσιμων πληροφοριών (λέξεις, βαθμοί εμπιστοσύνης κ.λπ.)  
- Συμβουλές για αντιμετώπιση προβλημάτων, διαχείριση edge‑case και ιδέες για τα επόμενα βήματα  

Δεν απαιτείται προηγούμενη εμπειρία με το Aspose· αρκεί ένα λειτουργικό περιβάλλον Python 3 και ένα αρχείο εικόνας που θέλετε να διαβάσετε.

## Προαπαιτούμενα

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|------------------------|
| Python 3.8+ | Aspose OCR’s wheels target modern interpreters |
| `aspose-ocr` package (`pip install aspose-ocr`) | Πακέτο `aspose-ocr` που εκτελεί την κύρια λειτουργία |
| A sample image (e.g., `receipt.tif`) | Δείγμα εικόνας (π.χ., `receipt.tif`) |
| Basic `json` knowledge | Βασικές γνώσεις `json` |

> **Συμβουλή:** Αν χρησιμοποιείτε Windows, εκτελέστε τη γραμμή εντολών ως Διαχειριστής όταν εγκαθιστάτε το πακέτο για να αποφύγετε προβλήματα δικαιωμάτων.

---

## Πώς να Εκτελέσετε OCR με Aspose OCR Python

Παρακάτω βρίσκεται το **πλήρες script** που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα αρχείο με όνομα `ocr_demo.py`. Περιέχει τα πάντα—από τις εισαγωγές μέχρι την τελική έξοδο—ώστε να το εκτελέσετε αμέσως.

```python
#!/usr/bin/env python3
"""
How to Perform OCR with Aspose OCR Python

This script demonstrates:
1. Creating an OCR engine instance.
2. Loading an image for OCR.
3. Processing the image OCR.
4. Converting the result to JSON.
5. Parsing and printing useful information.
"""

import json
import aspose.ocr as ocr
import os
import sys

# ----------------------------------------------------------------------
# Step 1: Create an OCR engine instance
# ----------------------------------------------------------------------
# The engine holds configuration (language, recognition mode, etc.).
# For most cases the defaults work fine, but you can tweak them later.
engine = ocr.OcrEngine()

# ----------------------------------------------------------------------
# Step 2: Load image OCR
# ----------------------------------------------------------------------
# Aspose can read many formats; here we use a TIFF because receipts often
# come as multi‑page scans. Adjust the path to point at your own file.
image_path = os.path.join("YOUR_DIRECTORY", "receipt.tif")
if not os.path.isfile(image_path):
    sys.stderr.write(f"❌ Image not found: {image_path}\n")
    sys.exit(1)

# The Image.load method decodes the file into an in‑memory object.
image = ocr.Image.load(image_path)

# ----------------------------------------------------------------------
# Step 3: Process image OCR
# ----------------------------------------------------------------------
# The recognize() call runs the OCR engine on the supplied image.
# It returns an OcrResult object that we can later serialize.
result = engine.recognize(image)

# ----------------------------------------------------------------------
# Step 4: Convert the recognition result to JSON
# ----------------------------------------------------------------------
# Aspose gives us a handy to_json() method; we then feed the string
# into Python's json module for a native dict.
json_payload = result.to_json()
parsed = json.loads(json_payload)

# ----------------------------------------------------------------------
# Step 5: Inspect the parsed data
# ----------------------------------------------------------------------
# The structure contains keys like "words", "lines", and "pages".
# We'll print a few samples to prove it works.
print("\n🔎 JSON keys:", list(parsed.keys()))
if parsed.get("words"):
    print("First word entry:", parsed["words"][0])
else:
    print("⚠️ No words detected – check image quality or language settings.")
```

### Αναμενόμενη Έξοδος

Όταν εκτελέσετε `python ocr_demo.py` (υποθέτοντας ότι η εικόνα υπάρχει και είναι αναγνώσιμη), θα πρέπει να δείτε κάτι παρόμοιο με:

```
🔎 JSON keys: ['pages', 'lines', 'words', 'language', 'confidence']
First word entry: {'text': 'Total', 'confidence': 0.98, 'rectangle': {...}}
```

Το ακριβές περιεχόμενο διαφέρει ανάλογα με την πηγή εικόνας, αλλά η παρουσία του πίνακα `"words"` επιβεβαιώνει ότι το **process image OCR** πέτυχε.

---

## Φόρτωση Image OCR – Συμβουλές & Συνηθισμένα Πιθανά Σφάλματα

1. **File format matters** – Ενώ το TIFF λειτουργεί εξαιρετικά για σαρωμένα έγγραφα, το PNG είναι συχνά καλύτερο για στιγμιότυπα οθόνης, και το JPEG για φωτογραφίες.  
2. **Resolution** – Το Aspose OCR αποδίδει καλύτερα με 300 dpi ή περισσότερο. Αν δείτε χαμηλούς βαθμούς εμπιστοσύνης, σκεφτείτε την αύξηση της ανάλυσης της εικόνας πριν τη φόρτωση.  
3. **Multi‑page files** – Αν το TIFF σας περιέχει πολλές σελίδες, η εντολή `image = ocr.Image.load(path)` θα σας δώσει μια στοίβα· μπορείτε να επαναλάβετε με `for page in image.pages:` και να καλέσετε `engine.recognize(page)` για κάθε μία.

> **Γιατί αυτό το βήμα είναι κρίσιμο:** Η σωστή φόρτωση της εικόνας εξασφαλίζει ότι η μηχανή OCR λαμβάνει καθαρά δεδομένα pixel. Ένα κατεστραμμένο ή μη υποστηριζόμενο φορμά θα προκαλέσει εξαίρεση `engine.recognize`, διακόπτοντας τη διαδικασία σας.

---

## Επεξεργασία Image OCR – Προχωρημένες Επιλογές

Το Aspose OCR εκθέτει πολλές ιδιότητες στο αντικείμενο `OcrEngine`:

| Ιδιότητα | Περίπτωση χρήσης |
|----------|-------------------|
| `engine.language = ocr.Language.English` | Εξαναγκασμός Αγγλικών όταν η εικόνα περιέχει μικτές γραφές |
| `engine.recognition_mode = ocr.RecognitionMode.TextDetection` | Γρηγορότερο, αλλά λιγότερο ακριβές· καλό για γρήγορες προεπισκοπήσεις |
| `engine.auto_rotate = True` | Αυτόματη διόρθωση περιστρεφόμενων σελίδων (χρήσιμο για αποδείξεις) |

Μπορείτε να ορίσετε αυτές τις ρυθμίσεις πριν από το βήμα 3 για να βελτιώσετε τη φάση **process image OCR**. Για παράδειγμα:

```python
engine.language = ocr.Language.English
engine.auto_rotate = True
```

---

## Κατανόηση της Εξόδου Aspose OCR Python

Το JSON payload ακολουθεί ένα προβλέψιμο σχήμα:

- **pages** – Λίστα αντικειμένων σελίδας, το καθένα με διαστάσεις και πληροφορίες περιστροφής.  
- **lines** – Ομαδοποιημένες λέξεις που μοιράζονται την ίδια βάση. Χρήσιμο για την ανασύνθεση παραγράφων.  
- **words** – Ατομικά αντικείμενα λέξεων που περιέχουν `text`, `confidence` και ένα `rectangle` με συντεταγμένες.  
- **language** – Κωδικός ανιχνευμένης γλώσσας (π.χ., "en").  
- **confidence** – Συνολική εμπιστοσύνη για ολόκληρο το έγγραφο.

Γνωρίζοντας αυτή τη δομή μπορείτε να εξάγετε ακριβώς ό,τι χρειάζεστε. Για παράδειγμα, για να πάρετε όλες τις λέξεις με confidence < 0.9 (πιθανά σφάλματα OCR), μπορείτε να προσθέσετε:

```python
low_confidence = [w for w in parsed["words"] if w["confidence"] < 0.9]
print("Potentially mis‑read words:", low_confidence)
```

---

## Edge Cases & Πώς να τα Διαχειριστείτε

| Κατάσταση | Προτεινόμενη αντιμετώπιση |
|-----------|---------------------------|
| **Empty result** (χωρίς λέξεις) | Επαληθεύστε την ποιότητα της εικόνας, βεβαιωθείτε ότι η σωστή γλώσσα είναι ορισμένη, και ίσως αυξήστε το DPI. |
| **Multi‑page PDFs** | Μετατρέψτε τις σελίδες PDF σε εικόνες πρώτα (π.χ., χρησιμοποιώντας `pdf2image`) και στη συνέχεια τροφοδοτήστε κάθε σελίδα στη μηχανή OCR. |
| **Non‑Latin scripts** | Εγκαταστήστε πρόσθετα πακέτα γλώσσας μέσω `engine.add_language(ocr.Language.ChineseSimplified)`. |
| **Large files** | Επεξεργαστείτε σε τμήματα· επαναχρησιμοποιήστε το ίδιο αντικείμενο `OcrEngine` για να αποφύγετε υπερβολική χρήση μνήμης. |

---

## Πλήρες Παράδειγμα Εργασίας (Όλα τα Βήματα Συνδυασμένα)

Παρακάτω είναι μια συμπαγής έκδοση που μπορείτε να ενσωματώσετε σε ένα Jupyter notebook ή σε ένα script. Περιλαμβάνει διαχείριση σφαλμάτων, προαιρετικές ρυθμίσεις και εκτυπώνει μια τακτοποιημένη σύνοψη.

```python
import json, os, sys, aspose.ocr as ocr

def perform_ocr(image_path: str):
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Create engine and tweak settings (optional)
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English   # ensures English detection
    engine.auto_rotate = True                # correct rotated scans

    # Load and recognize
    image = ocr.Image.load(image_path)
    result = engine.recognize(image)

    # Convert to JSON and parse
    parsed = json.loads(result.to_json())
    return parsed

if __name__ == "__main__":
    img = os.path.join("YOUR_DIRECTORY", "receipt.tif")
    try:
        data = perform_ocr(img)
        print("\n🔎 JSON keys:", list(data.keys()))
        print("First word:", data["words"][0] if data.get("words") else "No words")
    except Exception as exc:
        sys.stderr.write(f"❗ OCR failed: {exc}\n")
```

Η εκτέλεση αυτού σας δίνει την ίδια συνοπτική έξοδο όπως προηγουμένως,

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε σε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Βήμα‑Βήμα](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Πώς να Χρησιμοποιήσετε Aspose OCR για Αποτέλεσμα JSON στην Αναγνώριση Εικόνας](/ocr/english/net/text-recognition/get-result-as-json/)
- [Πώς να Εκτελέσετε Εξαγωγή Κειμένου από Εικόνα από Ροή Χρησιμοποιώντας Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}