---
category: general
date: 2026-03-26
description: Μάθετε πώς να περιστρέφετε εικόνα και να εκτελείτε OCR σε Python. Αυτός
  ο οδηγός δείχνει επίσης πώς να προεπεξεργάζεστε την εικόνα για OCR και να εξάγετε
  κείμενο από την εικόνα αποδοτικά.
draft: false
keywords:
- how to rotate image
- how to perform ocr
- preprocess image for ocr
- recognize text from image
- how to extract text from image
language: el
og_description: Πώς να περιστρέψετε σωστά μια εικόνα και στη συνέχεια να αναγνωρίσετε
  κείμενο από την εικόνα χρησιμοποιώντας το Aspose OCR. Ακολουθήστε αυτό το βήμα‑βήμα
  οδηγό για την προεπεξεργασία της εικόνας για OCR και την εξαγωγή κειμένου από την
  εικόνα.
og_title: Πώς να περιστρέψετε μια εικόνα και να κάνετε OCR – Πλήρης οδηγός Python
tags:
- Aspose
- Python
- Image Processing
- OCR
title: Πώς να περιστρέψετε εικόνα και να εκτελέσετε OCR με το Aspose σε Python
url: /el/python-java/general/how-to-rotate-image-and-perform-ocr-with-aspose-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Περιστρέψετε Εικόνα και να Εκτελέσετε OCR με το Aspose σε Python

Έχετε αναρωτηθεί ποτέ **πώς να περιστρέψετε εικόνα** ώστε μια μηχανή OCR να μπορεί πραγματικά να διαβάσει το κείμενο; Ίσως να σαρώσατε μια φόρμα που βρέθηκε σε πλάγια θέση, ή μια λήψη κάμερας που στράφηκε 90° δεξιόστροφα. Σε αυτήν την περίπτωση το κείμενο φαίνεται σωστό στο ανθρώπινο μάτι, αλλά η μηχανή OCR βλέπει ένα χάος. Τα καλά νέα; Είναι παιχνιδάκι να διορθώσετε τον προσανατολισμό, να περικόψετε την περιοχή που σας ενδιαφέρει και, στη συνέχεια, να εξάγετε το κείμενο—όλα με λίγες γραμμές Python και τις βιβλιοθήκες Aspose.

Σε αυτό το tutorial θα περάσουμε από όλη τη ροή εργασίας: από τη φόρτωση ενός περιστραμμένου TIFF, τη διόρθωση του προσανατολισμού του, **προεπεξεργασία εικόνας για OCR**, και τέλος **αναγνώριση κειμένου από εικόνα**. Στο τέλος θα γνωρίζετε **πώς να εκτελέσετε OCR** σε οποιαδήποτε εικόνα και θα μπορείτε να **εξάγετε κείμενο από αρχεία εικόνας** με σιγουριά.

## Τι Θα Χρειαστεί

- Python 3.8+ (ο κώδικας λειτουργεί με οποιαδήποτε πρόσφατη έκδοση)
- `asposeocrjava` και `asposeimaging` πακέτα εγκατεστημένα μέσω `pip`
- Ένα δείγμα εικόνας που χρειάζεται περιστροφή (π.χ., `rotated_form.tif`)
- Λίγη περιέργεια για επεξεργασία εικόνας

Δεν απαιτούνται βαριά πλαίσια—μόνο τα δύο πακέτα Aspose και λίγη λογική Python.

---

## Βήμα 1: Εγκατάσταση Πακέτων Aspose (Πώς να Εκτελέσετε OCR)

Πριν μπορέσουμε να **περιστρέψουμε εικόνα** ή να **αναγνωρίσουμε κείμενο από εικόνα**, χρειαζόμαστε τις βιβλιοθήκες που πραγματικά κάνουν το σκληρό έργο.

```bash
pip install asposeocrjava asposeimaging
```

> **Συμβουλή:** Αν βρίσκεστε πίσω από εταιρικό proxy, προσθέστε `--proxy http://proxy:port` στην εντολή. Τα πακέτα είναι καθαρά Python wrappers γύρω από τον πυρήνα Aspose .NET/Java, έτσι η εγκατάσταση είναι συνήθως άμεση.

---

## Βήμα 2: Φόρτωση του Πηγαίου Αρχείου και Περιστροφή του – Το Κεντρικό Βήμα “Πώς να Περιστρέψετε Εικόνα”

```python
from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

# Load the original, incorrectly oriented image
source_image = Image.load("YOUR_DIRECTORY/rotated_form.tif")

# Rotate 90° clockwise – this fixes the orientation for OCR
rotated_image = source_image.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)
```

> **Γιατί να περιστρέψετε;** Οι περισσότερες μηχανές OCR υποθέτουν ότι το κείμενο τρέχει από αριστερά προς δεξιά και από πάνω προς τα κάτω. Αν το bitmap είναι στραμμένο πλάγια, η μηχανή είτε θα επιστρέψει ακατανόητο κείμενο είτε τίποτα. Η περιστροφή ευθυγραμμίζει το πλέγμα εικονοστοιχείων με τη αναμενόμενη σειρά ανάγνωσης, βελτιώνοντας δραματικά την ακρίβεια.
> 
> **Περίπτωση άκρης:** Αν δεν είστε σίγουροι αν η εικόνα χρειάζεται περιστροφή 90°, 180° ή 270°, μπορείτε να ελέγξετε `source_image.width` έναντι `source_image.height` ή να χρησιμοποιήσετε ετικέτες προσανατολισμού `exif`. Η μέθοδος `rotate_flip` του Aspose υποστηρίζει επίσης `ROTATE_180` και `ROTATE_270_CLOCKWISE`.
> 
> **Προεπισκόπηση εικόνας (προαιρετικό):**  
> ![παράδειγμα περιστροφής εικόνας](/assets/rotate-demo.png "Πώς να περιστρέψετε εικόνα – πριν και μετά τη περιστροφή")

---

## Βήμα 3: Περικοπή της Περιοχής Ενδιαφέροντος – Προεπεξεργασία Εικόνας για OCR

Συχνά χρειάζεστε μόνο ένα μικρό τμήμα της σελίδας—π.χ., ένα πεδίο υπογραφής ή ένα μπλοκ αριθμών. Η περικοπή αφαιρεί θόρυβο και επιταχύνει **πώς να εκτελέσετε OCR**.

```python
# Define the rectangle that encloses the text you care about
# (x=100, y=200, width=800, height=300) – adjust to your form
roi = Rectangle(100, 200, 800, 300)

# Crop the rotated image to that rectangle
roi_image = rotated_image.crop(roi)
```

> **Γιατί να περικόψετε;** Η μείωση του μεγέθους της εικόνας περιορίζει το χώρο αναζήτησης της μηχανής OCR, μειώνοντας τα ψευδώς θετικά και μειώνοντας τον χρόνο επεξεργασίας. Βοηθά επίσης αν το πηγαίο αρχείο περιέχει υδατογραφήματα ή άλλα γραφικά που θα μπορούσαν να μπερδέψουν τη μηχανή.
> 
> **Συμβουλή:** Αν χειρίζεστε πολλαπλά πεδία, επαναλάβετε το βήμα περικοπής με διαφορετικά ορθογώνια και εκτελέστε OCR σε κάθε τμήμα ξεχωριστά.

---

## Βήμα 4: Αρχικοποίηση της Μηχανής OCR – Ο Πυρήνας “Πώς να Εκτελέσετε OCR”

```python
# Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

> **Πίσω από τη σκηνή:** Το Aspose OCR χρησιμοποιεί συνδυασμό Tesseract και ιδιόκτητης ανάλυσης εικόνας. Η δημιουργία μιας στιγμής της μηχανής μία φορά και η επαναχρησιμοποίησή της για πολλαπλές εικόνες είναι πιο αποδοτική από το να δημιουργείτε νέο αντικείμενο κάθε φορά.

---

## Βήμα 5: Παροχή της Περικομμένης Εικόνας και Αναγνώριση Κειμένου – Πώς να Εξάγετε Κείμενο από Εικόνα

```python
# Set the cropped image as the input for OCR
ocr_engine.set_image(roi_image)

# Run the recognition process
result = ocr_engine.recognize()

# Extract the plain text
extracted_text = result.get_text()
print(extracted_text)
```

### Αναμενόμενη Έξοδος

Αν η ROI περιέχει τη φράση “Invoice #12345 – Paid”, θα δείτε κάτι όπως:

```
Invoice #12345 – Paid
```

Αν το OCR δυσκολεύεται, μπορεί να εμφανίσει επιπλέον κενά ή λανθασμένους χαρακτήρες (π.χ., “Invo1ce #I2345 – Pa1d”). Εκεί έρχονται σε δράση τα κόλπα **προεπεξεργασίας εικόνας για OCR**—όπως η ρύθμιση αντίθεσης ή η εφαρμογή δυαδικοποίησης. Το Aspose προσφέρει πρόσθετα φίλτρα που μπορείτε να συνδυάσετε πριν το βήμα 5, αλλά η βασική ροή παραπάνω λειτουργεί για τις περισσότερες καθαρές σάρωση.

---

## Βήμα 6: Προαιρετικό – Λεπτομερής Ρύθμιση των Ρυθμίσεων OCR (Προχωρημένο “Πώς να Εκτελέσετε OCR”)

Αν χρειάζεστε μεγαλύτερη ακρίβεια για μια συγκεκριμένη γλώσσα ή θέλετε να αγνοήσετε ορισμένους χαρακτήρες, μπορείτε να ρυθμίσετε τη μηχανή:

```python
# Example: Restrict recognition to English alphanumerics only
ocr_engine.get_recognition_settings().set_recognition_language("en")
ocr_engine.get_recognition_settings().set_characters_blacklist("!@#$%^&*()")
```

> **Πότε να χρησιμοποιήσετε:** Χρησιμοποιήστε το όταν το έγγραφο περιέχει πολλά διακοσμητικά σύμβολα που δεν σας ενδιαφέρουν. Η μαύρη λίστα μειώνει τις ψευδείς ανιχνεύσεις.

---

## Πλήρες Script Από Αρχή έως Τέλος

Συνδυάζοντας όλα, εδώ είναι ένα έτοιμο‑να‑τρέξει script που **πώς να περιστρέψετε εικόνα**, **προεπεξεργασία εικόνας για OCR**, και τελικά **αναγνωρίζει κείμενο από εικόνα**:

```python
# -*- coding: utf-8 -*-
"""
Complete example: rotate, crop, and OCR an image with Aspose.
Author: Your Name
Date: 2026-03-26
"""

from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

def ocr_rotated_image(
    input_path: str,
    output_path: str = None,
    crop_rect: Rectangle = Rectangle(100, 200, 800, 300)
) -> str:
    """
    Loads an image, rotates it 90° clockwise, crops the region of interest,
    runs OCR, and returns the extracted text.

    Parameters
    ----------
    input_path : str
        Path to the original (possibly rotated) image file.
    output_path : str, optional
        If provided, saves the processed (rotated + cropped) image for inspection.
    crop_rect : Rectangle, optional
        Rectangle defining the ROI. Adjust to match your document layout.

    Returns
    -------
    str
        The plain text extracted from the ROI.
    """
    # Load and rotate
    src = Image.load(input_path)
    rotated = src.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)

    # Crop to region of interest
    roi = rotated.crop(crop_rect)

    # Optionally save the processed image for debugging
    if output_path:
        roi.save(output_path)

    # OCR
    engine = OcrEngine()
    engine.set_image(roi)
    result = engine.recognize()
    return result.get_text()

if __name__ == "__main__":
    text = ocr_rotated_image(
        "YOUR_DIRECTORY/rotated_form.tif",
        output_path="processed_roi.png"
    )
    print("=== Extracted Text ===")
    print(text)
```

Η εκτέλεση αυτού του script εκτυπώνει το αναγνωρισμένο κείμενο στην κονσόλα και αποθηκεύει μια οπτική του επεξεργασμένου ROI ως `processed_roi.png`. Μπορείτε να ανοίξετε αυτό το PNG για να επαληθεύσετε ότι η περιστροφή και η περικοπή λειτούργησαν όπως αναμενόταν.

---

## Συχνές Ερωτήσεις & Προβλήματα

| Ερώτηση | Απάντηση |
|----------|--------|
| **Τι γίνεται αν η εικόνα είναι ήδη όρθια;** | Το βήμα περιστροφής είναι ιδεομετρικό—η περιστροφή μιας σωστά προσανατολισμένης εικόνας κατά 90° θα την χαλάσει προφανώς, επομένως πρέπει να ελέγξετε `source_image.width` έναντι `height` ή να χρησιμοποιήσετε δεδομένα προσανατολισμού EXIF πριν καλέσετε `rotate_flip`. |
| **Η έξοδος OCR περιέχει επιπλέον αλλαγές γραμμής.** | Χρησιμοποιήστε `result.get_text().replace("\n", " ").strip()` για καθαρισμό, ή ενεργοποιήστε `ocr_engine.get_recognition_settings().set_remove_line_breaks(True)`. |
| **Μπορώ να επεξεργαστώ PDF απευθείας;** | Ναι—το Aspose Imaging μπορεί να φορτώσει σελίδες PDF ως εικόνες (`Image.load("file.pdf")`), μετά από αυτό ακολουθείτε τα ίδια βήματα περιστροφής και OCR. |
| **Υπάρχει τρόπος να επεξεργαστώ μαζικά πολλά αρχεία;** | Τυλίξτε το `ocr_rotated_image` σε βρόχο πάνω σε έναν φάκελο, ή χρησιμοποιήστε το `concurrent.futures` της Python για παράλληλη εκτέλεση. |
| **Πώς να διαχειριστώ γλώσσες εκτός της Αγγλικής;** | Ορίστε τη γλώσσα αναγνώρισης μέσω `ocr_engine.get_recognition_settings().set_recognition_language("fr")` για τα Γαλλικά κ.λπ. |

---

## Συμπέρασμα

Καλύψαμε **πώς να περιστρέψετε εικόνα** σωστά, **προεπεξεργασία εικόνας για OCR** με περικοπή, και τελικά **πώς να εκτελέσετε OCR** για **αναγνώριση κειμένου από εικόνα** και **εξαγωγή κειμένου από εικόνα** χρησιμοποιώντας τις βιβλιοθήκες Python του Aspose. Το πλήρες script παρουσιάζει μια πρακτική, έτοιμη για παραγωγή ροή εργασίας που μπορείτε να ενσωματώσετε σε οποιοδήποτε pipeline αυτοματοποίησης.

Αν είστε έτοιμοι να προχωρήσετε, δοκιμάστε να πειραματιστείτε με:

- **Βελτίωση εικόνας** (αντίθεση, δυαδικοποίηση) πριν το OCR
- **Εξαγωγή πολλαπλών ROI** για φόρμες με πολλά πεδία
- **Μαζική επεξεργασία** ολόκληρων φακέλων σαρωμένων εγγράφων
- **Ενσωμάτωση** με downstream συστήματα (π.χ., τροφοδοσία των εξαγόμενων δεδομένων σε βάση δεδομένων)

Μη διστάσετε να προσαρμόσετε τον κώδικα στη δική σας περίπτωση χρήσης, και καλή προγραμματιστική! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}