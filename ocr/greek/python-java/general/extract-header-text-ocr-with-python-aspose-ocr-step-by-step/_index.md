---
category: general
date: 2026-04-26
description: Εξαγωγή κειμένου κεφαλίδας με OCR χρησιμοποιώντας Python Aspose OCR.
  Μάθετε πώς να εξάγετε κείμενο από συγκεκριμένη περιοχή σε εικόνες γρήγορα και αξιόπιστα.
draft: false
keywords:
- extract header text ocr
- extract specific area text
- python aspose ocr
- ocr region of interest python
- aspose ocr roi
language: el
og_description: Εξαγωγή κειμένου κεφαλίδας με OCR γρήγορα. Αυτός ο οδηγός δείχνει
  πώς να εξάγετε κείμενο από συγκεκριμένη περιοχή χρησιμοποιώντας το Python Aspose
  OCR σε λίγες μόνο γραμμές.
og_title: Εξαγωγή κειμένου κεφαλίδας OCR με Python Aspose OCR – Πλήρης οδηγός
tags:
- OCR
- Python
- Aspose
title: Εξαγωγή κειμένου κεφαλίδας OCR με Python Aspose OCR – Οδηγός βήμα‑βήμα
url: /el/python-java/general/extract-header-text-ocr-with-python-aspose-ocr-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου Κεφαλίδας OCR – Πλήρης Οδηγός Python Aspose OCR

Έχετε ποτέ χρειαστεί να **εξάγετε κείμενο κεφαλίδας OCR** από ένα σαρωμένο τιμολόγιο αλλά δεν θέλετε να επεξεργαστείτε ολόκληρη τη σελίδα; Δεν είστε ο μόνος. Σε πολλά πραγματικά pipelines, η κεφαλίδα περιέχει τις πιο κρίσιμες πληροφορίες—αριθμό τιμολογίου, ημερομηνία, όνομα προμηθευτή—οπότε η γρήγορη εξαγωγή της μπορεί να εξοικονομήσει πολύ δουλειά downstream.

Σε αυτό το tutorial θα σας δείξουμε μια έτοιμη προς εκτέλεση λύση που **εξάγει κείμενο συγκεκριμένης περιοχής** χρησιμοποιώντας τη βιβλιοθήκη **Python Aspose OCR**. Χωρίς ασαφείς αναφορές σε εξωτερικά έγγραφα, μόνο ένα πλήρες script, μια σαφής εξήγηση κάθε γραμμής, και συμβουλές που θα χρησιμοποιήσετε πραγματικά αύριο.

## Τι Θα Μάθετε

- Πώς να εγκαταστήσετε και να εισάγετε το πακέτο Aspose OCR για Python.  
- Πώς να φορτώσετε μια εικόνα και να ορίσετε μια **περιοχή ενδιαφέροντος (ROI)** που απομονώνει την κεφαλίδα.  
- Πώς να εκτελέσετε τη μηχανή OCR σε αυτήν την ROI και να ανακτήσετε καθαρό κείμενο.  
- Συνηθισμένα προβλήματα (π.χ., ασυμφωνίες DPI) και πώς να τα αποφύγετε.  
- Πώς φαίνεται το αναμενόμενο αποτέλεσμα ώστε να μπορείτε να επαληθεύσετε ότι όλα λειτουργούν.

Με το τέλος, θα μπορείτε να ενσωματώσετε αυτόν τον κώδικα σε οποιοδήποτε έργο χρειάζεται **εξαγωγή κειμένου κεφαλίδας OCR** από τιμολόγια, αποδείξεις ή οποιοδήποτε έγγραφο με προβλέψιμη διάταξη.

## Προαπαιτήσεις

- Python 3.8 ή νεότερη εγκατεστημένη στο μηχάνημά σας.  
- Ένα έγκυρο license Aspose OCR for Python (η δωρεάν δοκιμή λειτουργεί για αξιολόγηση).  
- Ένα αρχείο εικόνας (`invoice.png`) που περιέχει καθαρή περιοχή κεφαλίδας.  
- Βασική εξοικείωση με συναρτήσεις Python και διαδρομές αρχείων.

> **Pro tip:** Αν δοκιμάζετε σε σάρωση χαμηλής ανάλυσης, αυξήστε το DPI πριν το δώσετε στο Aspose OCR – βελτιώνει δραματικά την ακρίβεια.

---

## Βήμα 1: Εγκατάσταση του Πακέτου Aspose OCR

Πρώτα, προσθέστε τη βιβλιοθήκη στο περιβάλλον σας. Το επίσημο πακέτο είναι `aspose-ocr`. Εκτελέστε αυτό μία φορά:

```bash
pip install aspose-ocr
```

Αν χρησιμοποιείτε εικονικό περιβάλλον (συνιστάται έντονα), ενεργοποιήστε το πριν την εγκατάσταση. Αυτό εξασφαλίζει ότι το πακέτο δεν θα συγκρουστεί με άλλα έργα.

## Βήμα 2: Εισαγωγή Απαιτούμενων Κλάσεων και Φόρτωση της Εικόνας

Τώρα φέρνουμε τις απαραίτητες κλάσεις στο script μας και φορτώνουμε την εικόνα του τιμολογίου. Παρατηρήστε τη χρήση **πλήρων διαδρομών**· οι σχετικές διαδρομές λειτουργούν επίσης, αλλά οι απόλυτες διαδρομές αφαιρούν την αμφιβολία όταν το script εκτελείται σε διακομιστή.

```python
# Step 2: Imports and image loading
from asposeocr import OcrEngine, Rectangle, Image

# Create an OCR engine instance – this object holds all settings.
ocr_engine = OcrEngine()

# Load the image that contains the invoice.
# Replace "YOUR_DIRECTORY/invoice.png" with your actual file location.
ocr_engine.image = Image.load(r"C:\Invoices\invoice.png")
```

> **Why this matters:** Η αρχικοποίηση του `OcrEngine` μία φορά και η επαναχρησιμοποίησή του για πολλαπλές εικόνες είναι πιο αποδοτική από το να δημιουργείτε νέα μηχανή κάθε φορά.

## Βήμα 3: Ορισμός της Περιοχής Κεφαλίδας (ROI)

Η κεφαλίδα συνήθως βρίσκεται στην κορυφή της σελίδας, αλλά οι ακριβείς συντεταγμένες της μπορεί να διαφέρουν. Εδώ ορίζουμε ένα ορθογώνιο (`x`, `y`, `width`, `height`) που καλύπτει την κεφαλίδα. Προσαρμόστε τους αριθμούς ώστε να ταιριάζουν με τη διάταξη του εγγράφου σας.

```python
# Step 3: Define the region of interest (ROI) that contains the header.
# Rectangle(x, y, width, height) – all values are in pixels.
header_region = Rectangle(50, 20, 500, 80)   # Example values; tweak as needed.
```

> **How it works:** Καλώντας το `set_roi`, η μηχανή OCR περιορίζει την ανάλυση της σε αυτό το ορθογώνιο, κάτι που επιταχύνει δραματικά την επεξεργασία και μειώνει τον θόρυβο από το υπόλοιπο της σελίδας.

## Βήμα 4: Εφαρμογή του ROI και Εκτέλεση OCR

Τώρα λέμε στη μηχανή να εστιάσει στην περιοχή κεφαλίδας και στη συνέχεια εκτελούμε τη διαδικασία OCR. Το αντικείμενο αποτελέσματος περιέχει το αναγνωρισμένο κείμενο και πρόσθετα μεταδεδομένα (βαθμοί εμπιστοσύνης, γλώσσα κ.λπ.).

```python
# Step 4: Apply the ROI to the OCR engine.
ocr_engine.set_roi(header_region)

# Step 5: Perform OCR on the defined ROI.
ocr_result = ocr_engine.process()
```

Αν το OCR αποτύχει (π.χ., μη υποστηριζόμενη μορφή εικόνας), το `ocr_result` θα είναι `None`. Μια γρήγορη συνθήκη προστασίας μπορεί να κάνει το script πιο ανθεκτικό:

```python
if ocr_result is None:
    raise RuntimeError("OCR processing failed – check image format and ROI.")
```

## Βήμα 5: Ανάκτηση και Εκτύπωση του Εξαγόμενου Κειμένου Κεφαλίδας

Τέλος, εξάγουμε το κείμενο από το αντικείμενο αποτελέσματος και το εμφανίζουμε. Μπορείτε επίσης να το γράψετε σε αρχείο ή να το περάσετε σε άλλη συνάρτηση για περαιτέρω ανάλυση.

```python
# Step 6: Print the extracted header text.
print("Header text:", ocr_result.text)
```

### Αναμενόμενο Αποτέλεσμα

Όταν όλα είναι σωστά ρυθμισμένα, θα πρέπει να δείτε κάτι όπως:

```
Header text: Acme Corp
Invoice #12345
Date: 2026‑04‑20
```

Αν το αποτέλεσμα φαίνεται παραμορφωμένο, ελέγξτε ξανά τις συντεταγμένες ROI και βεβαιωθείτε ότι η πηγή εικόνας είναι υψηλής αντίθεσης.

---

## Παραλλαγές & Ακραίες Περιπτώσεις

### 1. Πολλαπλές Κεφαλίδες σε Ένα Έγγραφο

Μερικές φορές ένα PDF περιέχει πολλές σελίδες, η καθεμία με τη δική της κεφαλίδα. Επανάληψη στις σελίδες και προσαρμογή του ROI ανά σελίδα:

```python
for page_number, img_path in enumerate(image_paths, start=1):
    ocr_engine.image = Image.load(img_path)
    # Adjust Y coordinate based on page height if needed.
    ocr_engine.set_roi(Rectangle(50, 20, 500, 80))
    result = ocr_engine.process()
    print(f"Page {page_number} header:", result.text)
```

### 2. Αντιμετώπιση Κεκλιμένων Σαρώσεων

Αν το τιμολόγιο είναι ελαφρώς περιστραμμένο, προεπεξεργαστείτε την εικόνα με OpenCV πριν τη δώσετε στο Aspose OCR:

```python
import cv2
import numpy as np

# Load with OpenCV, correct rotation, then convert back to Aspose Image.
cv_img = cv2.imread(r"C:\Invoices\invoice.png")
# Assume we have a function `deskew` that returns a corrected image.
deskewed = deskew(cv_img)
# Convert back to Aspose Image:
aspose_img = Image.from_array(deskewed)   # Pseudo‑code; actual conversion may vary.
ocr_engine.image = aspose_img
```

### 3. Αλλαγή Ρυθμίσεων Γλώσσας

Το Aspose OCR μπορεί να ανιχνεύσει αυτόματα τη γλώσσα, αλλά μπορείτε να επιβάλετε τα Αγγλικά για ταχύτερα αποτελέσματα:

```python
ocr_engine.language = "en"
```

---

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω είναι το πλήρες script που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα αρχείο με όνομα `extract_header.py`. Θυμηθείτε να αντικαταστήσετε τη διαδρομή εικόνας με τη δική σας.

```python
# extract_header.py
# Complete example: extract header text OCR using Python Aspose OCR

from asposeocr import OcrEngine, Rectangle, Image

def extract_header(image_path: str,
                   roi: Rectangle = Rectangle(50, 20, 500, 80),
                   language: str = "en") -> str:
    """
    Extracts text from the header region of an invoice image.

    :param image_path: Full path to the invoice image (PNG, JPG, etc.).
    :param roi: Rectangle defining the header area (default works for most A4 invoices).
    :param language: OCR language code; default is English.
    :return: Recognized header text.
    :raises RuntimeError: If OCR processing fails.
    """
    engine = OcrEngine()
    engine.language = language
    engine.image = Image.load(image_path)
    engine.set_roi(roi)

    result = engine.process()
    if result is None:
        raise RuntimeError("OCR processing failed – verify image and ROI.")
    return result.text.strip()

if __name__ == "__main__":
    # Example usage
    invoice_path = r"C:\Invoices\invoice.png"
    header_text = extract_header(invoice_path)
    print("Header text:", header_text)
```

Η εκτέλεση αυτού του script πρέπει να εμφανίσει τις γραμμές κεφαλίδας ακριβώς όπως φαίνονται παραπάνω. Μη διστάσετε να τροποποιήσετε τις τιμές `roi` ώστε να ταιριάζουν με το συγκεκριμένο πρότυπο τιμολογίου σας.

---

## Συχνές Ερωτήσεις Απαντημένες

**Q: Λειτουργεί αυτό απευθείας με PDF;**  
A: Δεν είναι έτοιμο εκτός κουτιού. Μετατρέψτε κάθε σελίδα PDF σε εικόνα (π.χ., χρησιμοποιώντας `pdf2image`) και στη συνέχεια δώστε το PNG/JPG στο script.

**Q: Τι γίνεται αν η κεφαλίδα μου περιέχει λογότυπο και κείμενο μαζί;**  
A: Το Aspose OCR εστιάζει στο κειμενικό περιεχόμενο. Για λογότυπα, σκεφτείτε να χρησιμοποιήσετε μια ξεχωριστή βιβλιοθήκη αναγνώρισης εικόνας όπως `opencv` ή `tesseract` με προσαρμοσμένο μοντέλο.

**Q: Είναι περιορισμένη η δωρεάν δοκιμή;**  
A: Η δοκιμή επιτρέπει έως 10 σελίδες ανά μήνα. Για παραγωγή, αγοράστε άδεια ώστε να αφαιρεθεί το όριο και να ξεκλειδώσετε ρυθμίσεις υψηλότερης ακρίβειας.

---

## Συμπέρασμα

Τώρα έχετε έναν **πλήρη, αξιόπιστο** οδηγό για **εξαγωγή κειμένου κεφαλίδας OCR** χρησιμοποιώντας **Python Aspose OCR**. Το tutorial κάλυψε τα πάντα, από την εγκατάσταση μέχρι την αντιμετώπιση ακραίων περιπτώσεων, και σας έδωσε μια επαναχρησιμοποιήσιμη συνάρτηση που μπορείτε να ενσωματώσετε σε μεγαλύτερες ροές εργασίας.

Στη συνέχεια, μπορείτε να εξερευνήσετε **εξαγωγή κειμένου συγκεκριμένης περιοχής** για άλλες ζώνες όπως υποσέλιδα ή γραμμές‑ειδών, ή να συνδυάσετε αυτήν την προσέγγιση με έναν μετατροπέα PDF‑σε‑εικόνα για αυτοματοποίηση πλήρων pipelines εγγράφων. Οι δυνατότητες είναι ατελείωτες—απλώς θυμηθείτε να διατηρείτε ακριβείς συντεταγμένες ROI και εικόνες υψηλής ανάλυσης.

Έχετε δύσκολη διάταξη; Μοιραστείτε τη στα σχόλια και θα προσαρμόσουμε το ROI μαζί. Καλή κωδικοποίηση!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}