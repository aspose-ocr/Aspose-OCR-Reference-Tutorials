---
category: general
date: 2026-06-28
description: Μάθετε πώς να αναγνωρίζετε εικόνες κειμένου χρησιμοποιώντας Python OCR,
  να εξάγετε αρχεία PNG κειμένου και να εκτυπώνετε το αναγνωρισμένο κείμενο με ισχυρή
  διαχείριση σφαλμάτων.
draft: false
keywords:
- recognize text image
- extract text png
- load image ocr
- process image ocr
- print recognized text
language: el
og_description: Βήμα‑βήμα οδηγός για την αναγνώριση εικόνας κειμένου σε Python, την
  εξαγωγή κειμένου σε png και την ασφαλή εκτύπωση του αναγνωρισμένου κειμένου.
og_title: Αναγνώριση κειμένου σε εικόνα με Python OCR – Πλήρης Οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn how to recognize text image using Python OCR, extract text png
    files, and print recognized text with robust error handling.
  headline: recognize text image with Python OCR – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Αναγνώριση εικόνας κειμένου με Python OCR – Πλήρης Οδηγός
url: /el/python/general/recognize-text-image-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# αναγνώριση κειμένου σε εικόνα με Python OCR – Πλήρης Οδηγός

Έχετε σκεφτεί ποτέ πώς να **αναγνωρίσετε κείμενο σε εικόνα** σε ένα script Python χωρίς να προσθέσετε ένα βαρύ framework; Δεν είστε μόνοι. Πολλοί προγραμματιστές χρειάζονται έναν γρήγορο τρόπο για *load image OCR* ένα screenshot, μια σαρωμένη απόδειξη ή ένα απλό PNG και να πάρουν το κείμενο πίσω.  

Σε αυτό το tutorial θα συνδέσουμε μια ελάχιστη μηχανή OCR, θα προσθέσουμε έναν προσαρμοσμένο logger, **load image OCR**, θα τρέξουμε το **process image OCR**, και τέλος **print recognized text**. Στο τέλος θα έχετε ένα αυτόνομο script που μπορεί επίσης να **extract text png** αρχεία κατόπιν ανάγκης.

## What You’ll Walk Away With

- Ένα πλήρως λειτουργικό απόσπασμα κώδικα Python που δημιουργεί μια μηχανή OCR, καταγράφει κάθε βήμα, και διαχειρίζεται αποτυχίες με χάρη.  
- Καθαρές εξηγήσεις του *γιατί* κάθε γραμμή έχει σημασία—ώστε να προσαρμόσετε τον κώδικα σε Tesseract, EasyOCR, ή οποιοδήποτε άλλο backend.  
- Συμβουλές για κοινά προβλήματα (ελλιπείς γραμματοσειρές, κατεστραμμένα PNG) και πώς να τα εντοπίσετε.

### Prerequisites

- Python 3.8+ εγκατεστημένο  
- Μια βιβλιοθήκη OCR που εκθέτει μια κλάση `OcrEngine` (το παράδειγμα χρησιμοποιεί ένα φανταστικό αλλά τυπικό API· αντικαταστήστε το με `pytesseract`, `easyocr`, κ.λπ.).  
- Ένα PNG αρχείο που θέλετε να αναλύσετε, αποθηκευμένο ως `input.png` σε φάκελο που ελέγχετε.  

> **Pro tip:** Αν χρησιμοποιείτε `pytesseract`, εγκαταστήστε πρώτα το σύστημα Tesseract binary (`sudo apt install tesseract-ocr` σε Linux) και μετά `pip install pytesseract pillow`.

---

## ## Recognize Text Image: Setting Up the Logger

Ένας καλός logger είναι ο αθέατος ήρωας κάθε pipeline OCR. Σας λέει *πότε* η μηχανή ξεκίνησε, *ποιο* αρχείο άνοιξε, και *γιατί* μπορεί να απέτυχε.

```python
# Step 1: Define a simple logger for the OCR engine
def my_logger(level, message):
    """
    level: str – e.g., "INFO", "WARN", "ERROR"
    message: str – human‑readable description of the event
    """
    print(f"[{level}] {message}")
```

*Why this matters:*  
Ο logger αποσυνδέει την διαγνωστική έξοδο από τον πυρήνα OCR, καθιστώντας εύκολο το ανακατεύθυνση των logs σε αρχείο, υπηρεσία παρακολούθησης, ή ακόμη και UI αργότερα.  

---

## ## Load Image OCR: Feeding the Engine a PNG

Πριν η μηχανή μπορέσει να **process image OCR**, χρειάζεται ένα σωστό αντικείμενο εικόνας. Οι περισσότερες βιβλιοθήκες δέχονται ένα αντικείμενο Pillow `Image`.

```python
from PIL import Image

# Step 2: Create the OCR engine and attach the logger
ocr_engine = OcrEngine(logging=my_logger)

# Step 3: Load the image to be processed
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Image.from_file(image_path))
my_logger("INFO", f"Loaded image from {image_path}")
```

*Key points:*  

- **load image ocr** – `Image.from_file` αφαιρεί τις λεπτομέρειες αποκωδικοποίησης PNG.  
- Κρατήστε το μονοπάτι ρυθμιζόμενο· η σκληρή κωδικοποίηση κάνει το script ευάλωτο.  
- Η κλήση logger επιβεβαιώνει ότι η εικόνα διαβάστηκε επιτυχώς, κάτι χρήσιμο όταν το αρχείο λείπει ή είναι κατεστραμμένο.

---

## ## Process Image OCR: Recognizing the Text

Τώρα αρχίζει η βαριά δουλειά. Η μηχανή σαρώνει το bitmap, εφαρμόζει τα νευρωνικά δίκτυα ή τις ευρετικές μεθόδους της, και επιστρέφει μια συμβολοσειρά Unicode.

```python
# Step 4: Recognize text from the image
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:
    # Step 5: Handle OCR errors gracefully
    my_logger("ERROR", f"OCR failed with code {e.code}: {e.message}")
    extracted_text = None
```

*Why we wrap it in `try/except`:*  
Το OCR μπορεί να «σκάσει» σε PNG χαμηλής ανάλυσης, μη υποστηριζόμενους χρωματικούς χώρους, ή όταν λείπουν δεδομένα γλώσσας. Το `catch OcrException` σας επιτρέπει να **print recognized text** μόνο όταν υπάρχει πραγματικά, αποφεύγοντας ασαφείς stack traces για τους τελικούς χρήστες.

---

## ## Print Recognized Text & Extract Text PNG

Αν η αναγνώριση πέτυχε, εμφανίζουμε το αποτέλεσμα και προαιρετικά το γράφουμε σε αρχείο `.txt` που αντανακλά το αρχικό όνομα PNG.

```python
if extracted_text:
    # Step 6: Print the recognized text
    print("Recognized text:", extracted_text)
    my_logger("INFO", "Printed recognized text to console")

    # Optional: Save extracted text for later use
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
```

*What you get:*  

- **print recognized text** – άμεση οπτική ανάδραση στο τερματικό.  
- Ένα παράπλευρο αρχείο `.txt` που ουσιαστικά **extract text png** για επεξεργασία downstream (ευρετήριο αναζήτησης, εισαγωγή δεδομένων, κ.λπ.).

---

## ## Common Edge Cases & How to Tackle Them

| Situation | Symptom | Fix |
|-----------|---------|-----|
| PNG is grayscale only | OCR returns empty string | Convert to RGB (`Image.convert("RGB")`) before feeding the engine. |
| Language not supported | `OcrException` with code `LANG_NOT_FOUND` | Install the language pack (e.g., `tesseract‑lang‑fra` for French) and set `ocr_engine.language = "fra"`. |
| Very large image ( > 5 MB ) | Slow recognition or memory error | Downscale with `image.thumbnail((2000, 2000))` before `set_image`. |
| Unexpected characters | Garbled output | Ensure the image is truly PNG; some files masquerade as PNG but are actually JPEGs. Use `Image.verify()` to validate. |

---

## ## Full Working Example (Copy‑Paste Ready)

```python
# -*- coding: utf-8 -*-
"""
Complete script to recognize text image using a generic OCR engine.
Replace OcrEngine, OcrException with the concrete classes from your library.
"""

from PIL import Image

# ----------------------------------------------------------------------
# 1️⃣  Logger definition
# ----------------------------------------------------------------------
def my_logger(level: str, message: str) -> None:
    """Simple console logger."""
    print(f"[{level}] {message}")

# ----------------------------------------------------------------------
# 2️⃣  Engine creation & image loading
# ----------------------------------------------------------------------
ocr_engine = OcrEngine(logging=my_logger)   # <- adapt to your library

image_path = "YOUR_DIRECTORY/input.png"
try:
    img = Image.open(image_path)
    img.verify()                     # sanity check the PNG
    img = Image.open(image_path)     # reopen after verify
    ocr_engine.set_image(img)
    my_logger("INFO", f"Loaded image from {image_path}")
except Exception as load_err:
    my_logger("ERROR", f"Failed to load image: {load_err}")
    raise SystemExit(1)

# ----------------------------------------------------------------------
# 3️⃣  Text recognition
# ----------------------------------------------------------------------
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:            # replace with actual exception class
    my_logger("ERROR", f"OCR failed ({e.code}): {e.message}")
    extracted_text = None

# ----------------------------------------------------------------------
# 4️⃣  Output handling
# ----------------------------------------------------------------------
if extracted_text:
    print("Recognized text:", extracted_text)          # ✅ print recognized text
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
else:
    my_logger("WARN", "No text extracted; check image quality.")
```

**Expected console output (happy path):**

```
[INFO] Loaded image from YOUR_DIRECTORY/input.png
[INFO] OCR succeeded
Recognized text: Invoice #12345
Total Amount: $1,250.00
Date: 2026‑06‑01
[INFO] Saved extracted text to YOUR_DIRECTORY/input.txt
```

If something goes wrong, you’ll see a clear `[ERROR]` line with the reason, thanks to the custom logger.

---

## ## Next Steps & Related Topics

- **extract text png** from batches: wrap the script in a `for` loop that walks a directory tree.  
- **process image ocr** with preprocessing (deskew, contrast boost) using OpenCV before feeding the engine.  
- Switch to a cloud OCR service (Google Vision, Azure Read) by swapping the `OcrEngine` implementation—your surrounding code stays the same.  
- Learn how to **print recognized text** into PDFs using `reportlab` for automated report generation.  

---

## Conclusion

We just walked through a compact, production‑ready way to **recognize text image** in Python, from loading the PNG to **print recognized text** and saving the result. By injecting a tiny logger, handling exceptions, and optionally persisting the output, the script is ready for both quick experiments and integration into larger pipelines.

Give it a spin with your own screenshots, tinker with image preprocessing, and you’ll soon be extracting text from any PNG you throw at it. Got questions? Drop a comment—happy OCRing!  

![παράδειγμα αναγνώρισης κειμένου σε εικόνα](placeholder.png)


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}