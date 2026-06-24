---
category: general
date: 2026-06-19
description: Εκτελέστε OCR σε εικόνα χρησιμοποιώντας τη βιβλιοθήκη OCR της Python.
  Μάθετε πώς να εντοπίζετε κείμενο από εικόνα, να αναγνωρίζετε κείμενο από JPEG και
  να εξάγετε κείμενο από σαρωμένη εικόνα αποδοτικά.
draft: false
keywords:
- perform OCR on image
- recognize text from jpeg
- detect text from image
- extract text from scanned image
- load image for OCR
language: el
og_description: Κάντε OCR σε εικόνα με Python και εξάγετε κείμενο από σαρωμένα αρχεία.
  Αυτός ο οδηγός σας καθοδηγεί βήμα‑βήμα στη φόρτωση εικόνων, την αποκλίση και την
  αναγνώριση κειμένου.
og_title: Εκτέλεση OCR σε εικόνα με Python – Οδηγός πλήρους εξαγωγής κειμένου
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  headline: Perform OCR on Image in Python – Full Text Extraction Guide
  type: TechArticle
- description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  name: Perform OCR on Image in Python – Full Text Extraction Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed (the example uses the `ocr` package available via
      `pip install ocr-lib` – replace with your actual library name). - Basic familiarity
      with Python functions and virtual environments. - An image file (JPEG, PNG,
      TIFF) you want to process; we’ll use `skewed_page.jpg` as a placeh'
  - name: Recognize Text from JPEG vs PNG
    text: 'Both formats are supported, but JPEG compression can introduce artifacts
      that confuse the engine. If you notice frequent mis‑recognitions, try converting
      the JPEG to PNG first:'
  - name: Detect Text from Image with Multiple Languages
    text: 'If your document mixes English and Spanish, set a multilingual mode:'
  - name: Extract Text from Scanned PDFs
    text: 'For PDFs, you need to rasterize each page into an image first. Libraries
      like `pdf2image` make this painless:'
  type: HowTo
- questions:
  - answer: Absolutely. The library works without a GUI; just ensure the necessary
      native binaries (e.g., Tesseract) are installed on the server.
    question: Can I run this on a headless server?
  - answer: Consider adding a sharpening filter before `engine.recognize`. Many OCR
      libraries expose `image_preprocessing.sharpen = True` or you can use OpenCV’s
      `cv2.GaussianBlur` in reverse.
    question: What if the image is blurry?
  - answer: 'Yes. Wrap `perform_ocr` in a loop over a list of file paths, ## What
      Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
      - [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
      - [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

      {{< /blocks/products/pf/tutorial-page-section >}} {{< /blocks/products/pf/main-container
      >}} {{< /blocks/products/pf/main-wrap-class >}} {{< blocks/products/products-backtop-button
      >}}'
    question: Does the script support batch processing?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Εκτέλεση OCR σε εικόνα με Python – Οδηγός πλήρους εξαγωγής κειμένου
url: /el/python-java/general/perform-ocr-on-image-in-python-full-text-extraction-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε Εικόνα με Python – Οδηγός Πλήρους Εξαγωγής Κειμένου

Κάποτε χρειάστηκε να **εκτελέσετε OCR σε εικόνα** αλλά αντιμετωπίζατε δυσκολίες επειδή ο κώδικας φαινόταν κρυπτογραφημένος; Δεν είστε ο μόνος. Είτε μετατρέπετε μια στοίβα σαρωμένων αποδείξεων σε αναζητήσιμα PDF, είτε εξάγετε λεζάντες από ένα JPEG για ένα έργο επιστήμης δεδομένων, η ικανότητα να αναγνωρίζετε κείμενο από JPEG και άλλες μορφές είναι απαραίτητη δεξιότητα για κάθε προγραμματιστή σήμερα.

Σε αυτό το tutorial θα περάσουμε από ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει πώς να **ανιχνεύσετε κείμενο από εικόνα**, **εξάγετε κείμενο από σαρωμένο έγγραφο** και ακόμη **φορτώσετε εικόνα για OCR** σε λίγες μόνο γραμμές κώδικα. Στο τέλος, θα έχετε ένα σταθερό, έτοιμο για παραγωγή snippet που μπορείτε να ενσωματώσετε στα δικά σας έργα — χωρίς ελλιπείς εισαγωγές, χωρίς ασαφείς συντομεύσεις «δείτε τα docs».

## Τι Θα Δημιουργήσετε

- Ένα μικρό script Python που δημιουργεί μια μηχανή OCR, ενεργοποιεί το auto‑deskew, φορτώνει ένα JPEG (ή οποιαδήποτε υποστηριζόμενη μορφή) και εκτυπώνει το αναγνωρισμένο κείμενο.  
- Επεξηγήσεις του **γιατί** κάθε ρύθμιση είναι σημαντική, όχι μόνο του **πώς** να την γράψετε.  
- Συμβουλές για διαχείριση πολυ‑σελίδων PDF, μη‑αγγλικών γλωσσών και κοινών παγίδων όπως θολές σάρωση.

### Προαπαιτούμενα

- Python 3.8+ εγκατεστημένο (το παράδειγμα χρησιμοποιεί το πακέτο `ocr` διαθέσιμο μέσω `pip install ocr-lib` – αντικαταστήστε το με το πραγματικό όνομα της βιβλιοθήκης σας).  
- Βασική εξοικείωση με συναρτήσεις Python και εικονικά περιβάλλοντα.  
- Ένα αρχείο εικόνας (JPEG, PNG, TIFF) που θέλετε να επεξεργαστείτε· θα χρησιμοποιήσουμε το `skewed_page.jpg` ως παράδειγμα.

> **Pro tip:** Αν χρησιμοποιείτε Windows, εκτελέστε το τερματικό σας ως Administrator όταν εγκαθιστάτε τη βιβλιοθήκη OCR για να αποφύγετε προβλήματα δικαιωμάτων.

---

## Εκτέλεση OCR σε Εικόνα – Ρύθμιση και Διαμόρφωση

Το πρώτο που χρειάζεστε είναι μια καθαρή παρουσία μηχανής OCR. Σκεφτείτε το ως τον εγκέφαλο πίσω από τη λειτουργία· χωρίς σωστή διαμόρφωση, ακόμη και η πιο καθαρή εικόνα θα επιστρέψει ακατανόητο κείμενο.

```python
# Step 1: Import the OCR library and create an engine
import ocr

engine = ocr.OcrEngine()
# Set the recognition language – English works for most cases
engine.language = ocr.Language.English
```

**Γιατί είναι σημαντικό:**  
Η ρύθμιση `engine.language` περιορίζει το σύνολο χαρακτήρων που αναμένει η μηχανή OCR, αυξάνοντας δραματικά την ακρίβεια. Αν το παραλείψετε, η μηχανή θα προσπαθήσει να μαντέψει, συχνά διαβάζοντας λανθασμένα απλές λέξεις.

---

## Ενεργοποίηση Αυτόματου Deskew – Διόρθωση Κεκλιμένων Σαρώσεων

Οι σαρωμένες σελίδες σπάνια είναι τέλεια επίπεδες. Μία μικρή κλίση μπορεί να διαταράξει τη διαχωριστική διαδικασία χαρακτήρων, μετατρέποντας το “Hello” σε “H3llo”. Η σημαία `auto_deskew` κάνει το σκληρό έργο για εσάς.

```python
# Step 2: Turn on automatic deskew to straighten tilted images
engine.image_preprocessing.auto_deskew = True
```

**Ακραία περίπτωση:** Αν γνωρίζετε ότι οι εικόνες σας είναι ήδη ευθείες, η απενεργοποίηση του deskew μπορεί να εξοικονομήσει μερικά χιλιοστά του δευτερολέπτου χρόνο επεξεργασίας — χρήσιμο όταν διαχειρίζεστε χιλιάδες σελίδες σε batch job.

---

## Φόρτωση Εικόνας για OCR – Υποστήριξη JPEG, PNG, TIFF

Τώρα φορτώνουμε πραγματικά **εικόνα για OCR**. Η μέθοδος `ocr.Image.load` είναι ευέλικτη· δέχεται διαδρομή προς οποιαδήποτε υποστηριζόμενη μορφή raster.

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/skewed_page.jpg"
image = ocr.Image.load(image_path)
```

> **Γιατί αυτό το βήμα είναι κρίσιμο:** Η βιβλιοθήκη διαβάζει το αρχείο σε ένα εσωτερικό bitmap, εφαρμόζοντας τυχόν απαραίτητη μετατροπή χρωματικού χώρου. Η παράλειψη αυτού και η μετάδοση ενός ακατέργαστου ρεύματος bytes θα προκαλούσε `FileNotFoundError` ή, χειρότερα, θα παρήγαγε σιωπηλά κενά αποτελέσματα.

Αν χρειάζεται να **αναγνωρίσετε κείμενο από JPEG** αρχεία συγκεκριμένα, απλώς βεβαιωθείτε ότι η επέκταση του αρχείου είναι `.jpeg` ή `.jpg`. Η ίδια κλήση λειτουργεί για PNG (`.png`) ή TIFF (`.tif`) χωρίς τροποποίηση.

---

## Εκτέλεση OCR σε Εικόνα – Εκτέλεση της Μηχανής

Με τη μηχανή έτοιμη και την εικόνα στη μνήμη, ήρθε η ώρα να **εκτελέσετε OCR σε εικόνα**. Αυτή η μοναδική γραμμή κάνει το σκληρό έργο: προεπεξεργασία, διαχωρισμό, ταξινόμηση και συναρμολόγηση κειμένου.

```python
# Step 4: Run OCR and capture the result object
result = engine.recognize(image)
```

**Τι συμβαίνει στο παρασκήνιο;**  
- Η μηχανή εφαρμόζει τη μεταστροφή deskew (αν είναι ενεργοποιημένη).  
- Εκτελεί ένα νευρωνικό δίκτυο ή backend Tesseract για την ταυτοποίηση χαρακτήρων.  
- Τέλος, ενώνει τους χαρακτήρες σε λέξεις και γραμμές, επιστρέφοντας ένα πλούσιο αντικείμενο `result`.

---

## Εξαγωγή Κειμένου από Σαρωμένη Εικόνα – Εμφάνιση Αποτελεσμάτων

Το τελευταίο βήμα είναι να **εξάγετε κείμενο από σαρωμένη εικόνα** και να το εμφανίσετε. Το χαρακτηριστικό `result.text` περιέχει την αναπαράσταση plain‑text.

```python
# Step 5: Print the detected text to the console
print("Detected text:")
print(result.text)
```

Τυπική έξοδος μοιάζει με:

```
Detected text:
Invoice #12345
Date: 2023‑09‑01
Total: $1,234.56
Thank you for your business!
```

Αν η μηχανή OCR δεν βρει κανέναν χαρακτήρα, το `result.text` θα είναι κενή συμβολοσειρά. Σε αυτήν την περίπτωση, ελέγξτε ξανά την ποιότητα της εικόνας ή σκεφτείτε να προσαρμόσετε την ιδιότητα `engine.confidence_threshold` (αν η βιβλιοθήκη σας το υποστηρίζει).

---

## Διαχείριση Συνηθισμένων Παραλλαγών

### Αναγνώριση Κειμένου από JPEG vs PNG

Και οι δύο μορφές υποστηρίζονται, αλλά η συμπίεση JPEG μπορεί να εισάγει τεχνουργήματα που μπερδεύουν τη μηχανή. Αν παρατηρήσετε συχνές λανθασμένες αναγνώσεις, δοκιμάστε πρώτα να μετατρέψετε το JPEG σε PNG:

```python
from PIL import Image
Image.open(image_path).save("temp.png", format="PNG")
image = ocr.Image.load("temp.png")
```

### Ανίχνευση Κειμένου από Εικόνα με Πολλαπλές Γλώσσες

Αν το έγγραφό σας συνδυάζει Αγγλικά και Ισπανικά, ορίστε λειτουργία πολυγλωσσίας:

```python
engine.language = ocr.Language.English | ocr.Language.Spanish
```

Η μηχανή θα λάβει υπόψη και τα δύο αλφάβητα κατά την αναγνώριση.

### Εξαγωγή Κειμένου από Σαρωμένα PDFs

Για PDFs, πρέπει πρώτα να rasterize κάθε σελίδα σε εικόνα. Βιβλιοθήκες όπως η `pdf2image` κάνουν αυτή τη διαδικασία απλή:

```python
from pdf2image import convert_from_path

pages = convert_from_path("document.pdf", dpi=300)
for i, page_image in enumerate(pages):
    image = ocr.Image.from_pil(page_image)   # assuming the library accepts a PIL image
    result = engine.recognize(image)
    print(f"Page {i+1} text:")
    print(result.text)
```

---

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω βρίσκεται το πλήρες script που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα αρχείο `ocr_demo.py`. Περιλαμβάνει διαχείριση σφαλμάτων και έναν μικρό βοηθό για μέτρηση χρόνου εκτέλεσης.

```python
import ocr
import time
import sys
from pathlib import Path

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a given image file and return the extracted text.
    Handles auto‑deskew and basic error reporting.
    """
    if not Path(image_path).exists():
        sys.exit(f"❌ Error: File not found – {image_path}")

    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.image_preprocessing.auto_deskew = True

    try:
        image = ocr.Image.load(image_path)
    except Exception as e:
        sys.exit(f"❌ Failed to load image: {e}")

    start = time.time()
    result = engine.recognize(image)
    elapsed = time.time() - start

    if not result.text.strip():
        print("⚠️ No text detected. Try a higher‑resolution image or adjust preprocessing.")
    else:
        print(f"✅ OCR completed in {elapsed:.2f}s")
        print("Detected text:")
        print(result.text)

    return result.text

if __name__ == "__main__":
    # Replace with the path to your JPEG/PNG/TIFF file
    perform_ocr("YOUR_DIRECTORY/skewed_page.jpg")
```

**Αναμενόμενη έξοδος** (υπόθεση καθαρού σκαναρίσματος):

```
✅ OCR completed in 0.87s
Detected text:
Lorem ipsum dolor sit amet,
consectetur adipiscing elit.
```

---

## Συχνές Ερωτήσεις

**Ε: Μπορώ να τρέξω αυτό σε headless server;**  
Α: Απόλυτα. Η βιβλιοθήκη λειτουργεί χωρίς GUI· απλώς βεβαιωθείτε ότι τα απαραίτητα εγγενή binaries (π.χ., Tesseract) είναι εγκατεστημένα στον server.

**Ε: Τι γίνεται αν η εικόνα είναι θολή;**  
Α: Σκεφτείτε να προσθέσετε φίλτρο sharpening πριν από το `engine.recognize`. Πολλές βιβλιοθήκες OCR εκθέτουν `image_preprocessing.sharpen = True` ή μπορείτε να χρησιμοποιήσετε το `cv2.GaussianBlur` του OpenCV αντίστροφα.

**Ε: Υποστηρίζει το script επεξεργασία παρτίδας;**  
Α: Ναι. Τυλίξτε το `perform_ocr` σε βρόχο πάνω σε μια λίστα διαδρομών αρχείων,

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}