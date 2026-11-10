---
category: general
date: 2026-08-12
description: Πώς να χρησιμοποιήσετε OCR στην Python για να αναγνωρίσετε κείμενο από
  εικόνα, να εξάγετε κείμενο, να μετατρέψετε την εικόνα σε κείμενο και να καθαρίσετε
  το κείμενο OCR με επεξεργασία AI μετά την αναγνώριση.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use OCR
- recognize text from image
- extract text from image
- convert image to text
- clean up OCR text
language: el
lastmod: 2026-08-12
og_description: Πώς να χρησιμοποιήσετε OCR στην Python για να μετατρέψετε τις εικόνες
  σε επεξεργάσιμο κείμενο. Μάθετε να αναγνωρίζετε κείμενο από εικόνα, να εξάγετε κείμενο,
  να μετατρέπετε εικόνα σε κείμενο και να καθαρίζετε το κείμενο OCR με AI.
og_image_alt: Screenshot of Python code converting an image to clean text using OCR
  and AI post‑processing
og_title: Πώς να χρησιμοποιήσετε OCR στην Python – πλήρης οδηγός προγραμματισμού
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: How to use OCR in Python to recognize text from image, extract text,
    convert image to text, and clean up OCR text with AI post‑processing.
  headline: How to use OCR in Python – step‑by‑step guide
  type: TechArticle
- description: How to use OCR in Python to recognize text from image, extract text,
    convert image to text, and clean up OCR text with AI post‑processing.
  name: How to use OCR in Python – step‑by‑step guide
  steps:
  - name: Loads an image file (PNG, JPEG, or TIFF).
    text: Loads an image file (PNG, JPEG, or TIFF).
  - name: Recognizes text from the image using an OCR engine.
    text: Recognizes text from the image using an OCR engine.
  - name: Improves the raw output with an AI‑driven post‑processor.
    text: Improves the raw output with an AI‑driven post‑processor.
  - name: Prints the cleaned‑up text to the console.
    text: Prints the cleaned‑up text to the console.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- AI post‑processing
title: Πώς να χρησιμοποιήσετε OCR στην Python – βήμα‑βήμα οδηγός
url: /el/python/general/how-to-use-ocr-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να χρησιμοποιήσετε OCR σε Python – οδηγός βήμα‑βήμα

Αν χρειάζεστε **πώς να χρησιμοποιήσετε OCR** για να μετατρέψετε σαρωμένα έγγραφα ή στιγμιότυπα οθόνης σε επεξεργάσιμο κείμενο, αυτό το tutorial παρουσιάζει μια πλήρη λύση σε Python. Θα μάθετε να αναγνωρίζετε κείμενο από εικόνα, να εξάγετε κείμενο από εικόνα, να μετατρέπετε εικόνα σε κείμενο και να καθαρίζετε το κείμενο OCR με έναν ελαφρύ AI post‑processor.

Ο οδηγός καλύπτει τα πάντα, από την εγκατάσταση των απαιτούμενων βιβλιοθηκών μέχρι τη διαχείριση εικόνων χαμηλής ποιότητας, ώστε να μπορείτε να ενσωματώσετε OCR σε οποιοδήποτε pipeline αυτοματοποίησης χωρίς να αναρωτιέστε ποιο βήμα λείπει.

## Τι θα δημιουργήσετε

Στο τέλος αυτού του άρθρου θα έχετε ένα ενιαίο script Python που:

1. Φορτώνει ένα αρχείο εικόνας (PNG, JPEG ή TIFF).  
2. Αναγνωρίζει κείμενο από την εικόνα χρησιμοποιώντας μια μηχανή OCR.  
3. Βελτιώνει το ακατέργαστο αποτέλεσμα με έναν AI‑driven post‑processor.  
4. Εκτυπώνει το καθαρισμένο κείμενο στην κονσόλα.

Δεν απαιτούνται εξωτερικές υπηρεσίες — όλα εκτελούνται τοπικά, καθιστώντας τη λύση κατάλληλη για περιβάλλοντα εκτός σύνδεσης ή έργα με ευαίσθητα δεδομένα.

## Προαπαιτούμενα

- Python 3.9 ή νεότερη.  
- Βιβλιοθήκες `pytesseract` και `Pillow` (`pip install pytesseract pillow`).  
- Το εκτελέσιμο του Tesseract‑OCR εγκατεστημένο και διαθέσιμο στο `PATH` του συστήματός σας.  
- Βασική κατανόηση των συναρτήσεων σε Python.  

Αν έχετε ήδη αυτά τα στοιχεία, μπορείτε να περάσετε κατευθείαν στο πρώτο μπλοκ κώδικα.

## Πώς να χρησιμοποιήσετε OCR με Python

Ο πυρήνας του **πώς να χρησιμοποιήσετε OCR** είναι η αρχικοποίηση της μηχανής OCR και η παροχή μιας εικόνας σε αυτήν. Σε αυτό το tutorial χρησιμοποιούμε το `pytesseract`, ένα ελαφρύ wrapper γύρω από τη ανοιχτή μηχανή Tesseract.

```python
import pytesseract
from PIL import Image

def load_image(path: str) -> Image.Image:
    """
    Open an image file and return a Pillow Image object.
    Pillow handles many formats (PNG, JPEG, TIFF) and ensures
    the image is in a mode that Tesseract can read.
    """
    return Image.open(path)
```

> **Γιατί είναι σημαντικό αυτό το βήμα** – Το Tesseract απαιτεί καθαρή, σωστά προσανατολισμένη εικόνα. Η χρήση του Pillow εγγυάται ότι τα δεδομένα εικόνας είναι κανονικοποιημένα πριν τρέξει το OCR, βελτιώνοντας την ακρίβεια της επόμενης λειτουργίας **recognize text from image**.

## Recognize text from image

Τώρα καλούμε το `pytesseract.image_to_string` για να εξάγουμε το ακατέργαστο string. Αυτή είναι η κλασική κλήση **recognize text from image**.

```python
def ocr_recognize(image: Image.Image) -> str:
    """
    Run Tesseract OCR on the supplied image and return the raw text.
    """
    raw_text = pytesseract.image_to_string(image, lang='eng')
    return raw_text
```

> **Γιατί διαχωρίζουμε τη συνάρτηση** – Η απομόνωση του βήματος OCR σας επιτρέπει να αλλάξετε τη μηχανή αργότερα (π.χ., να μεταβείτε σε EasyOCR) χωρίς να επηρεάσετε το υπόλοιπο pipeline. Επίσης κάνει τις μονάδες ελέγχου πιο εύκολες.

## Extract text from image and improve quality

Το ακατέργαστο αποτέλεσμα OCR συχνά περιέχει αλλαγές γραμμής, τυχαίους χαρακτήρες ή λανθασμένα αναγνωρισμένες λέξεις. Ένας AI post‑processor μπορεί να καθαρίσει αυτά τα artefacts αυτόματα. Παρακάτω υπάρχει ένα ελάχιστο παράδειγμα που χρησιμοποιεί τη βιβλιοθήκη `transformers` για να τρέξει ένα μικρό μοντέλο γλώσσας τοπικά. Μπορείτε να το αντικαταστήσετε με οποιαδήποτε ιδιόκτητη υπηρεσία αν το προτιμάτε.

```python
from transformers import pipeline

# Initialize a zero‑shot text‑generation pipeline once (expensive operation)
_ai_postprocessor = pipeline("text2text-generation", model="google/flan-t5-small")

def clean_ocr_text(raw: str) -> str:
    """
    Send the raw OCR string to a lightweight AI model that rewrites
    the text, removing obvious errors and normalizing whitespace.
    """
    # The prompt guides the model to act as a post‑processor
    prompt = f"Clean up the following OCR output, fixing spelling mistakes and removing extra line breaks:\n\n{raw}"
    result = _ai_postprocessor(prompt, max_length=512, do_sample=False)
    # The pipeline returns a list of dicts; we take the generated text
    cleaned = result[0]["generated_text"]
    return cleaned.strip()
```

> **Γιατί ένας AI post‑processor βοηθά** – Τα παραδοσιακά OCR excelle στην αναγνώριση χαρακτήρων αλλά δυσκολεύονται με τη διάταξη και το θόρυβο. Ένα μοντέλο γλώσσας καταλαβαίνει το πλαίσιο, οπότε μπορεί να μετατρέψει το “Th1s 1s 4 test.” σε “This is a test.” Αυτό το βήμα αντιμετωπίζει άμεσα την απαίτηση **clean up OCR text**.

## Convert image to text – full script

Συνδυάζοντας τα πάντα παίρνουμε ένα σύντομο script που **convert image to text** από άκρη σε άκρη.

```python
import sys
from pathlib import Path

def main(image_path: str):
    """
    Complete pipeline:
    1. Load image.
    2. Recognize text from image.
    3. Clean up OCR text.
    4. Print the final result.
    """
    # 1️⃣ Load the image file
    img = load_image(image_path)

    # 2️⃣ Recognize text from image (raw OCR)
    raw_text = ocr_recognize(img)
    print("=== Raw OCR output ===")
    print(raw_text)
    print("\n---\n")

    # 3️⃣ Clean up OCR text with AI post‑processor
    cleaned_text = clean_ocr_text(raw_text)
    print("=== Cleaned‑up text ===")
    print(cleaned_text)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python ocr_pipeline.py <path-to-image>")
        sys.exit(1)

    image_file = Path(sys.argv[1])
    if not image_file.is_file():
        print(f"Error: file '{image_file}' does not exist.")
        sys.exit(1)

    main(str(image_file))
```

### Αναμενόμενο αποτέλεσμα

Η εκτέλεση του script με ένα δείγμα εικόνας (`sample.png`) μπορεί να παράγει:

```
=== Raw OCR output ===
Th1s 1s 4 sampl3
text from an im4ge.

--- 

=== Cleaned‑up text ===
This is a sample text from an image.
```

Παρατηρήστε πώς ο AI post‑processor διόρθωσε τους λανθασμένους χαρακτήρες και αφαίρεσε την τυχαία αλλαγή γραμμής. Αυτό δείχνει το πλήρες workflow **extract text from image** και αποδεικνύει το όφελος του καθαρισμού του OCR κειμένου.

## Διαχείριση κοινών edge cases

| Κατάσταση                               | Προτεινόμενη προσαρμογή                                                          |
|----------------------------------------|---------------------------------------------------------------------------------|
| Εικόνα χαμηλής αντίθεσης               | Μετατρέψτε σε κλίμακα του γκρι και αυξήστε την αντίθεση με `ImageEnhance` πριν το OCR. |
| Έγγραφο πολλαπλών γλωσσών               | Περνάτε λίστα χωρισμένη με κόμμα στο `lang` (π.χ., `lang='eng+fra'`).          |
| Πολύ μεγάλες εικόνες ( > 2000 px )      | Μειώστε την ανάλυση με `img.thumbnail((2000, 2000))` για να επιταχύνετε το Tesseract. |
| Λείπει το εκτελέσιμο του Tesseract      | Επαληθεύστε ότι το `pytesseract.pytesseract.tesseract_cmd` δείχνει στο εκτελέσιμο. |
| Ο AI post‑processor είναι αργός        | Χρησιμοποιήστε μικρότερο μοντέλο (`t5-small`) ή τρέξτε τον post‑processor σε GPU. |

> **Pro tip:** Κρατήστε το αντικείμενο του AI μοντέλου (`_ai_postprocessor`) στην εισαγωγή του module, όπως φαίνεται, ώστε να μην φορτώνεται ξανά σε κάθε κλήση. Αυτό μειώνει δραματικά την καθυστέρηση όταν επεξεργάζεστε πολλές εικόνες.

## Εναλλακτικές προσεγγίσεις

- **EasyOCR**: Μια καθαρά‑Python βιβλιοθήκη OCR που υποστηρίζει πάνω από 80 γλώσσες χωρίς εξωτερικό εκτελέσιμο. Αντικαταστήστε το `ocr_recognize` με `EasyOCR.Reader` αν προτιμάτε λύση μόνο με pip.
- **Cloud OCR APIs**: Google Cloud Vision, Azure Computer Vision ή Amazon Textract προσφέρουν υψηλότερη ακρίβεια για σύνθετες διατάξεις, αλλά απαιτούν πρόσβαση στο διαδίκτυο και χρέωση.
- **Custom post‑processing**: Για καθορισμένο καθαρισμό, εκφράσεις κανονικού τύπου (`re.sub`) μπορούν να διορθώσουν κοινά μοτίβα (π.χ., αφαίρεση ενωμένων διασπάσεων γραμμής) χωρίς μοντέλο AI.

## Σύνοψη

Τώρα ξέρετε **πώς να χρησιμοποιήσετε OCR** σε Python για να αναγνωρίσετε κείμενο από εικόνα, να εξάγετε κείμενο από εικόνα, να μετατρέψετε εικόνα σε κείμενο και να καθαρίσετε το OCR κείμενο με έναν AI post‑processor. Το πλήρες script παρουσιάζει ένα pipeline έτοιμο για παραγωγή, το οποίο μπορείτε να επεκτείνετε με πρόσθετη προεπεξεργασία (μείωση θορύβου, διόρθωση κλίσης) ή επόμενες ενέργειες (αποθήκευση σε βάση δεδομένων, τροφοδότηση ευρετηρίου αναζήτησης).

### Επόμενα βήματα

- Πειραματιστείτε με διαφορετικά AI μοντέλα (π.χ., `gpt‑2`, `flan‑ul2`) για να δείτε ποιο προσφέρει τον καλύτερο καθαρισμό για το πεδίο σας.  
- Ενσωματώστε το pipeline σε μια web υπηρεσία χρησιμοποιώντας Flask ή FastAPI, μετατρέποντας το script σε endpoint OCR κατ’ απαίτηση.  
- Εξερευνήστε επεξεργασία batch: κάντε βρόχο σε έναν φάκελο εικόνων και γράψτε κάθε καθαρισμένο αποτέλεσμα σε αντίστοιχο αρχείο `.txt`.

Αισθανθείτε ελεύθεροι να προσαρμόσετε τον κώδικα στη δική σας ροή εργασίας και αφήστε το καθαρό, αναζητήσιμο κείμενο να ενδυναμώσει το επόμενο στάδιο της εφαρμογής σας. Καλό κώδικα!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Convert Image to Text: Extract Text from Image Using Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}