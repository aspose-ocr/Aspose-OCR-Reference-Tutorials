---
category: general
date: 2026-09-19
description: Το μάθημα Python OCR δείχνει πώς να μετατρέψετε PNG σε κείμενο χρησιμοποιώντας
  το Aspose OCR. Μάθετε εξαγωγή κειμένου OCR με Python και εξάγετε κείμενο από σαρωμένες
  εικόνες.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- python OCR tutorial
- convert PNG to text
- OCR text extraction python
- extract text image python
- extract text scanned image
language: el
lastmod: 2026-09-19
og_description: Το μάθημα OCR σε Python σας καθοδηγεί στη μετατροπή PNG σε κείμενο
  χρησιμοποιώντας το Aspose OCR. Κατακτήστε την εξαγωγή κειμένου OCR με Python και
  εξάγετε κείμενο από σαρωμένες εικόνες.
og_image_alt: Screenshot of Python OCR code extracting text from a PNG image
og_title: Python OCR tutorial – μετατροπή PNG σε κείμενο με το Aspose
schemas:
- author: Aspose
  dateModified: '2026-09-19'
  description: Python OCR tutorial shows how to convert PNG to text using Aspose OCR.
    Learn OCR text extraction python and extract text from scanned images.
  headline: 'Python OCR tutorial: convert PNG to text with Aspose'
  type: TechArticle
- description: Python OCR tutorial shows how to convert PNG to text using Aspose OCR.
    Learn OCR text extraction python and extract text from scanned images.
  name: 'Python OCR tutorial: convert PNG to text with Aspose'
  steps:
  - name: Expected output
    text: 'If `sample.png` contains the sentence “Hello, world!”, the console will
      show:'
  - name: 1. Non‑PNG formats
    text: Even though this tutorial focuses on **convert PNG to text**, you might
      receive JPEG or TIFF files. The same code works; just change the file extension
      in `load_image`.
  - name: 2. Low‑resolution images
    text: 'OCR accuracy drops below 150 dpi. If you encounter poor results, upscale
      the image first using Pillow:'
  - name: 3. Extracting text from a scanned image with multiple languages
    text: 'Set a comma‑separated list of language codes:'
  - name: 4. Large documents
    text: 'Processing many pages in a single run can exhaust memory. Process each
      page individually:'
  type: HowTo
tags:
- python
- OCR
- image processing
title: 'Python OCR tutorial: μετατροπή PNG σε κείμενο με το Aspose'
url: /el/python/general/python-ocr-tutorial-convert-png-to-text-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR tutorial: μετατροπή PNG σε κείμενο με Aspose

Αν χρειάζεστε ένα **python OCR tutorial** που μετατρέπει μια εικόνα PNG σε επεξεργάσιμο κείμενο, αυτός ο οδηγός σας παρέχει μια πλήρη, έτοιμη προς εκτέλεση λύση. Θα δείτε πώς να εγκαταστήσετε τη βιβλιοθήκη Aspose OCR, να φορτώσετε μια εικόνα, να εκτελέσετε τη μηχανή αναγνώρισης και να εκτυπώσετε τα αποτελέσματα — όλα σε λίγα σύντομα βήματα.

Η σάρωση ενός εγγράφου και η εξαγωγή του κειμένου μπορεί να φαίνεται επίπονη, ειδικά όταν διαχειρίζεστε διαφορετικές μορφές εικόνας και ρυθμίσεις γλώσσας. Αυτό το tutorial αφαιρεί τις εικασίες δείχνοντάς σας ακριβώς ποιες μεθόδους να καλέσετε και γιατί έχουν σημασία, ώστε να μπορείτε να εστιάσετε στην ενσωμάτωση του OCR στις δικές σας εφαρμογές.

Θα μάθετε επίσης πώς να **convert PNG to text**, να αντιμετωπίζετε κοινές παγίδες και να προσαρμόζετε τον κώδικα για άλλους τύπους εικόνας όπως JPEG ή TIFF. Στο τέλος, θα μπορείτε να εξάγετε κείμενο από οποιαδήποτε σαρωμένη εικόνα με σιγουριά.

## Prerequisites

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* Python 3.8 ή νεότερη έκδοση εγκατεστημένη.
* Σύνδεση στο internet για λήψη του πακέτου Aspose OCR.
* Μια εικόνα PNG (ή οποιαδήποτε υποστηριζόμενη μορφή) που περιέχει αναγνώσιμο κείμενο.

Δεν χρειάζεστε **όχι** ξεχωριστή μηχανή OCR ή εξωτερικά binaries — το Aspose OCR περιλαμβάνει όλα όσα χρειάζεστε.

## Step 1: Install the Aspose OCR package

Το πρώτο βήμα είναι η προσθήκη της βιβλιοθήκης στο περιβάλλον σας. Η Aspose παρέχει ένα καθαρά Python πακέτο που μπορεί να εγκατασταθεί μέσω pip.

```bash
pip install aspose-ocr
```

> **Pro tip:** Χρησιμοποιήστε ένα εικονικό περιβάλλον (`python -m venv venv`) για να διατηρήσετε τις εξαρτήσεις απομονωμένες από άλλα έργα.

Η εγκατάσταση του πακέτου καθιστά διαθέσιμο το module `aspose.ocr`, το οποίο περιέχει την κλάση `OcrEngine` που χρησιμοποιείται σε όλο το tutorial.

## Step 2: Import the OCR engine class

Τώρα που το πακέτο είναι διαθέσιμο, εισάγετε την κλάση που οδηγεί τη διαδικασία αναγνώρισης.

```python
# Step 2: Import the OCR engine class
from aspose.ocr import OcrEngine
```

Η `OcrEngine` περιλαμβάνει όλη τη λογική για φόρτωση εικόνων, ρύθμιση γλώσσας και εξαγωγή κειμένου. Η εισαγωγή της στην αρχή ακολουθεί την τυπική πρακτική της Python και διατηρεί το script οργανωμένο.

## Step 3: Create an instance of the OCR engine

Η δημιουργία ενός αντικειμένου δίνει μια νέα μηχανή με προεπιλεγμένες ρυθμίσεις. Μπορείτε αργότερα να προσαρμόσετε ιδιότητες όπως η γλώσσα ή η προεπεξεργασία εικόνας.

```python
# Step 3: Create an instance of the OCR engine
engine = OcrEngine()
```

Ένα νέο αντικείμενο `engine` αντιπροσωπεύει μια μοναδική συνεδρία OCR. Η επαναχρησιμοποίηση του ίδιου αντικειμένου για πολλές εικόνες μπορεί να βελτιώσει την απόδοση επειδή οι εσωτερικοί πόροι είναι cached.

## Step 4: Load the image you want to process

Καθορίστε τη διαδρομή του αρχείου PNG που θέλετε να μετατρέψετε. Η μέθοδος `load_image` δέχεται οποιαδήποτε μορφή υποστηρίζεται από το Aspose OCR, ώστε μπορείτε επίσης να περάσετε αρχεία JPEG, BMP ή TIFF.

```python
# Step 4: Load the image you want to process
engine.load_image("YOUR_DIRECTORY/sample.png")
```

Αν το αρχείο δεν βρεθεί, η `load_image` ρίχνει ένα `FileNotFoundError`. Τυλίξτε την κλήση σε block try/except για κώδικα παραγωγής ώστε να παρέχετε φιλικό μήνυμα σφάλματος.

## Step 5: Perform OCR to extract text from the image

Καλώντας τη `recognize` εκτελείται η αλυσίδα αναγνώρισης και επιστρέφει το εξαγόμενο string. Η μέθοδος χειρίζεται αυτόματα την ανάλυση διάταξης, τον διαχωρισμό χαρακτήρων και την ανίχνευση γλώσσας (η προεπιλογή είναι Αγγλικά).

```python
# Step 5: Perform OCR to extract text from the image
text = engine.recognize()
```

Μπορείτε να αλλάξετε τη γλώσσα πριν καλέσετε τη `recognize`:

```python
engine.language = "fr"   # for French text
```

Αυτή η ευελιξία είναι χρήσιμη όταν χρειάζεστε **OCR text extraction python** για πολυγλωσσικά έγγραφα.

## Step 6: Output the recognized text

Τέλος, εκτυπώστε ή αποθηκεύστε το αποτέλεσμα. Για έναν γρήγορο έλεγχο, η `print` εμφανίζει το ακατέργαστο string στην κονσόλα.

```python
# Step 6: Output the recognized text
print(text)
```

### Expected output

Αν το `sample.png` περιέχει την πρόταση “Hello, world!”, η κονσόλα θα εμφανίσει:

```
Hello, world!
```

Η έξοδος μπορεί να περιλαμβάνει αλλαγές γραμμής ή επιπλέον κενά ανάλογα με την αρχική διάταξη. Μπορείτε να επεξεργαστείτε το string με `str.strip()` ή κανονικές εκφράσεις για να το καθαρίσετε.

## Handling common edge cases

### 1. Non‑PNG formats

Αν και αυτό το tutorial εστιάζει στη **convert PNG to text**, μπορεί να λάβετε αρχεία JPEG ή TIFF. Ο ίδιος κώδικας λειτουργεί· απλώς αλλάξτε την επέκταση του αρχείου στη `load_image`.

```python
engine.load_image("scanned_page.tiff")
```

### 2. Low‑resolution images

Η ακρίβεια του OCR μειώνεται κάτω από 150 dpi. Αν αντιμετωπίσετε φτωχά αποτελέσματα, αυξήστε την ανάλυση της εικόνας πρώτα χρησιμοποιώντας το Pillow:

```python
from PIL import Image

img = Image.open("sample.png")
high_res = img.resize((img.width * 2, img.height * 2), Image.LANCZOS)
high_res.save("sample_high_res.png")
engine.load_image("sample_high_res.png")
```

### 3. Extracting text from a scanned image with multiple languages

Ορίστε μια λίστα γλωσσικών κωδίκων χωρισμένων με κόμμα:

```python
engine.language = "en,es,de"
```

Το Aspose OCR θα προσπαθήσει να αναγνωρίσει χαρακτήρες από όλες τις αναφερθείσες γλώσσες.

### 4. Large documents

Η επεξεργασία πολλών σελίδων σε μία εκτέλεση μπορεί να εξαντλήσει τη μνήμη. Επεξεργαστείτε κάθε σελίδα ξεχωριστά:

```python
for page_path in ["page1.png", "page2.png", "page3.png"]:
    engine.load_image(page_path)
    print(engine.recognize())
```

## Full, runnable script

Συνδυάζοντας όλα τα βήματα δημιουργείται ένα αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε, επικολλήσετε και εκτελέσετε.

```python
# python_ocr_tutorial.py
# Complete script for extracting text from a PNG image using Aspose OCR

# Install the library first:
# pip install aspose-ocr

from aspose.ocr import OcrEngine

def extract_text(image_path: str) -> str:
    """
    Loads an image and returns the recognized text.
    Parameters:
        image_path: Path to the PNG (or other supported) image.
    Returns:
        Recognized text as a string.
    """
    engine = OcrEngine()          # Create OCR engine instance
    engine.load_image(image_path) # Load the target image
    return engine.recognize()     # Perform OCR and return result

if __name__ == "__main__":
    # Replace with the actual path to your image
    path = "YOUR_DIRECTORY/sample.png"
    try:
        result = extract_text(path)
        print("=== Recognized Text ===")
        print(result)
    except Exception as e:
        print(f"Error during OCR processing: {e}")
```

Τρέξτε το script με:

```bash
python python_ocr_tutorial.py
```

Θα πρέπει να δείτε το εξαγόμενο κείμενο να εμφανίζεται στην κονσόλα.

## Conclusion

Αυτό το **python OCR tutorial** έδειξε πώς να **convert PNG to text** χρησιμοποιώντας το Aspose OCR, καλύπτοντας εγκατάσταση, φόρτωση εικόνας, αναγνώριση και διαχείριση εξόδου. Τώρα έχετε ένα αξιόπιστο πρότυπο για **OCR text extraction python**, και μπορείτε να προσαρμόσετε τον κώδικα για **extract text image python** από οποιοδήποτε σαρωμένο έγγραφο.

Από εδώ, σκεφτείτε:

* Ενσωμάτωση του script σε μια web υπηρεσία (π.χ., Flask) για παροχή OCR ως API.
* Αποθήκευση του εξαγόμενου κειμένου σε βάση δεδομένων για αναζητήσιμα αρχεία.
* Πειραματισμό με διαφορετικές ρυθμίσεις γλώσσας για την επεξεργασία πολυγλωσσικών σαρώσεων.

Καλή προγραμματιστική δουλειά και απολαύστε τη μετατροπή εικόνων σε αναζητήσιμο, επεξεργάσιμο κείμενο!

## What Should You Learn Next?

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Μετατροπή Εικόνας σε Κείμενο: Εξαγωγή Κειμένου από Εικόνα Χρησιμοποιώντας Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Python OCR Tutorial: Εξαγωγή Κειμένου Πίνακα από Εικόνες](/ocr/english/python-java/general/python-ocr-tutorial-extract-table-text-from-images/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}