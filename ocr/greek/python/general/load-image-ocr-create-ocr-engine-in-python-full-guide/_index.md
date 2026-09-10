---
category: general
date: 2026-01-12
description: Φορτώστε γρήγορα OCR εικόνας με Python. Μάθετε πώς να δημιουργήσετε μηχανή
  OCR, να διαχειριστείτε σφάλματα και να εξάγετε κείμενο σε έναν βήμα‑βήμα οδηγό.
draft: false
keywords:
- load image OCR
- create OCR engine
- OCR error handling
- Python OCR tutorial
- image preprocessing OCR
language: el
og_description: Φορτώστε OCR εικόνας με Python χρησιμοποιώντας μια απλή μηχανή OCR.
  Αυτός ο οδηγός δείχνει τη διαχείριση σφαλμάτων, τις βέλτιστες πρακτικές και τον
  πλήρη κώδικα.
og_title: Φόρτωση εικόνας OCR – Δημιουργία μηχανής OCR σε Python
tags:
- OCR
- Python
- Image Processing
title: Φόρτωση εικόνας OCR – Δημιουργία μηχανής OCR σε Python – Πλήρης οδηγός
url: /el/python/general/load-image-ocr-create-ocr-engine-in-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Φόρτωση OCR Εικόνας – Δημιουργία Μηχανής OCR σε Python

Έχετε ποτέ χρειαστεί να **φορτώσετε OCR εικόνας** αλλά δεν ήξερες πώς να ξεκινήσεις; Ίσως δοκιμάσατε μια βιβλιοθήκη, λάβατε μια ακατανόητη εξαίρεση, και σκεφτήκατε «Τι τώρα;». Δεν είστε μόνοι. Σε αυτό το tutorial θα περάσουμε από τη δημιουργία μιας μηχανής OCR από το μηδέν, τη ασφαλή φόρτωση εικόνων, και τη διαχείριση των αναπόφευκτων προβλημάτων που εμφανίζονται όταν ένα αρχείο λείπει ή είναι κατεστραμμένο.

Στο τέλος αυτού του οδηγού θα έχετε ένα πλήρως λειτουργικό script που **δημιουργεί μηχανή OCR**, φορτώνει εικόνες, ελέγχει για σφάλματα, και ακόμη εκτυπώνει το εξαγόμενο κείμενο. Χωρίς ασαφείς αναφορές σε εξωτερικά έγγραφα—απλώς ένα ολοκληρωμένο, εκτελέσιμο παράδειγμα που μπορείτε να ενσωματώσετε στο πρότζεκτ σας σήμερα.

## Τι Θα Χρειαστεί

- Python 3.9 ή νεότερο (η σύνταξη που χρησιμοποιούμε είναι τυπική σε όλες τις εκδόσεις 3.x)  
- Η υποθετική βιβλιοθήκη `ocr` (εγκαταστήστε με `pip install ocr‑lib` – αντικαταστήστε με τη δική σας βιβλιοθήκη)  
- Ένας φάκελος με μερικές δοκιμαστικές εικόνες (μία που υπάρχει, μία που σκόπιμα δεν υπάρχει)  

Αυτό είναι όλο. Χωρίς βαριές εξαρτήσεις, χωρίς πολύπλοκα βήματα κατασκευής. Ας βουτήξουμε.

## Βήμα 1: Δημιουργία Μηχανής OCR – Ρύθμιση του Κεντρικού Αντικειμένου

Πριν μπορέσετε να **φορτώσετε OCR εικόνας**, χρειάζεστε μια παρουσία μηχανής που ξέρει πώς να επικοινωνεί με τη βασική μηχανή OCR. Σκεφτείτε το ως το τηλεχειριστήριο μιας τηλεόρασης· χωρίς αυτό δεν μπορείτε να αλλάξετε κανάλι.

```python
# step_1_create_engine.py
import ocr

def init_engine():
    """
    Initializes and returns an OCR engine instance.
    This is where we 'create OCR engine' for the rest of the tutorial.
    """
    try:
        engine = ocr.OcrEngine()
        print("✅ OCR engine created successfully.")
        return engine
    except ocr.OcrException as e:
        # If the library itself fails to initialise, we bail out early.
        print(f"❌ Failed to create OCR engine (code {e.code}): {e.message}")
        raise
```

**Γιατί είναι σημαντικό:**  
Η δημιουργία της μηχανής μία φορά και η επαναχρησιμοποίησή της αποφεύγει το κόστος φόρτωσης των εγγενών βιβλιοθηκών σε κάθε εικόνα. Επίσης κεντράρει τη διαμόρφωση (πακέτα γλώσσας, ρυθμίσεις DPI κ.λπ.) ώστε να μπορείτε να τις ρυθμίσετε από ένα σημείο.

## Βήμα 2: Φόρτωση OCR Εικόνας – Ασφαλής Φόρτωση με Εξαιρέσεις

Τώρα που έχουμε μια μηχανή, το επόμενο λογικό βήμα είναι να της δώσουμε μια εικόνα. Ο πιο απλός τρόπος είναι να καλέσετε `engine.load_image(path)`. Ωστόσο, ο κώδικας στην πραγματική ζωή πρέπει να προβλέπει ελλιπή αρχεία, μη υποστηριζόμενες μορφές ή προβλήματα δικαιωμάτων.

```python
# step_2_load_with_exception.py
def load_image_with_exception(engine, path):
    """
    Attempts to load an image using a try/except block.
    Demonstrates the classic 'load image OCR' pattern with Python exceptions.
    """
    try:
        engine.load_image(path)
        print(f"✅ Image loaded: {path}")
    except ocr.OcrException as ex:
        # The OCR library packages its own error codes.
        print(f"❌ Failed to load image (code {ex.code}): {ex.message}")
        # Optionally re‑raise or handle gracefully.
```

**Συμβουλή:** Αν αναμένετε πολλές εικόνες, τυλίξτε την κλήση σε βρόχο και καταγράψτε τις αποτυχίες σε ένα CSV για μεταγενέστερη ανάλυση. Αυτό διατηρεί την αλυσίδα σας ανθεκτική ακόμη και όταν ένα αρχείο αποτύχει.

## Βήμα 3: Φόρτωση OCR Εικόνας – Χρήση του Ενσωματωμένου API Σφαλμάτων της Μηχανής

Κάποιες βιβλιοθήκες OCR εκθέτουν μια μέθοδο ανάκτησης σφαλμάτων χωρίς εξαιρέσεις. Αυτό είναι χρήσιμο όταν θέλετε να αποφύγετε το κόστος απόδοσης των εξαιρέσεων Python σε σφιχτούς βρόχους.

```python
# step_3_load_with_error_api.py
def load_image_with_error_api(engine, path):
    """
    Loads an image and then checks the engine's internal error state.
    This pattern complements the exception approach and shows another way
    to 'load image OCR' safely.
    """
    engine.load_image(path)           # No try/except here.
    load_error = engine.get_last_error()
    if load_error:
        print(f"❌ Load error: {load_error.message} (code {load_error.code})")
    else:
        print(f"✅ Image loaded without error: {path}")
```

**Πότε να το προτιμήσετε:**  
Αν επεξεργάζεστε χιλιάδες εικόνες ανά λεπτό, η αποφυγή εξαιρέσεων μπορεί να εξοικονομήσει πολύτιμα χιλιοστά του δευτερολέπτου. Το API σφαλμάτων σας παρέχει έναν ελαφρύ έλεγχο κατάστασης μετά από κάθε κλήση.

## Βήμα 4: Εξαγωγή Κειμένου – Ο Πραγματικός Λόγος που Είστε Εδώ

Η φόρτωση της εικόνας είναι μόνο το ήμισυ της ιστορίας. Μετά από μια επιτυχημένη φόρτωση, συνήθως θέλετε το κείμενο OCR. Εδώ είναι ένας σύντομος βοηθός που εξάγει το κείμενο και το εκτυπώνει.

```python
# step_4_extract_text.py
def extract_text(engine):
    """
    Retrieves OCR results from the previously loaded image.
    Returns a string; empty string indicates no text found.
    """
    try:
        result = engine.recognize()
        text = result.text
        if text:
            print("📝 Extracted Text:")
            print(text)
        else:
            print("⚠️ No text detected in the image.")
        return text
    except ocr.OcrException as e:
        print(f"❌ OCR failed (code {e.code}): {e.message}")
        return ""
```

**Γιατί λειτουργεί:**  
`engine.recognize()` είναι η τυπική κλήση στα περισσότερα OCR SDKs. Επιστρέφει ένα αντικείμενο αποτελέσματος που περιέχει τη ακατέργαστη συμβολοσειρά, τις βαθμολογίες εμπιστοσύνης και τα πλαίσια οριοθέτησης. Σε αυτό το tutorial το κρατάμε απλό και εμφανίζουμε μόνο το απλό κείμενο.

## Βήμα 5: Συνδυάζοντας Όλα – Ένα Πλήρες, Εκτελέσιμο Script

Παρακάτω είναι το τελικό script που ενώνει όλα τα κομμάτια. Αποθηκεύστε το ως `load_image_ocr_demo.py` και τρέξτε το από τη γραμμή εντολών.

```python
# load_image_ocr_demo.py
import os
import ocr

def init_engine():
    try:
        engine = ocr.OcrEngine()
        print("✅ OCR engine created.")
        return engine
    except ocr.OcrException as e:
        print(f"❌ Could not create OCR engine (code {e.code}): {e.message}")
        raise

def load_image_with_exception(engine, path):
    try:
        engine.load_image(path)
        print(f"✅ Loaded image via exception method: {path}")
    except ocr.OcrException as ex:
        print(f"❌ Exception while loading '{path}': {ex.message}")

def load_image_with_error_api(engine, path):
    engine.load_image(path)
    err = engine.get_last_error()
    if err:
        print(f"❌ Error API reported for '{path}': {err.message}")
    else:
        print(f"✅ Loaded image via error API: {path}")

def extract_text(engine):
    try:
        result = engine.recognize()
        txt = result.text
        if txt:
            print("📝 OCR Result:")
            print(txt)
        else:
            print("⚠️ No recognizable text.")
        return txt
    except ocr.OcrException as e:
        print(f"❌ Recognition error: {e.message}")
        return ""

def main():
    # 1️⃣ Create the OCR engine
    engine = init_engine()

    # Paths – adjust to your environment
    existing_img = os.path.join("samples", "document.png")
    missing_img = os.path.join("samples", "nonexistent.png")

    # 2️⃣ Load a valid image using exception handling
    load_image_with_exception(engine, existing_img)
    extract_text(engine)

    # 3️⃣ Attempt to load a missing image using the error API
    load_image_with_error_api(engine, missing_img)

if __name__ == "__main__":
    main()
```

**Αναμενόμενη έξοδος (όταν το `document.png` υπάρχει):**

```
✅ OCR engine created.
✅ Loaded image via exception method: samples/document.png
📝 OCR Result:
[Here you’ll see the extracted text from the image]

✅ Loaded image via error API: samples/nonexistent.png
❌ Error API reported for 'samples/nonexistent.png': File not found
```

Αν η εικόνα λείπει, το script αναφέρει το πρόβλημα με χάρη αντί να καταρρεύσει—ακριβώς αυτό που θέλετε σε παραγωγή.

## Συνηθισμένα Πιθανά Προβλήματα & Συμβουλές

- **Παράξενες συμπεριφορές διαδρομών αρχείων:** Τα Windows χρησιμοποιούν ανάστροφες καθέτους (`\`) που μπορούν να ερμηνευτούν ως χαρακτήρες διαφυγής. Χρησιμοποιήστε ακατέργαστες συμβολοσειρές (`r\"C:\\path\\file.png\"`) ή `os.path.join` όπως φαίνεται.  
- **Μη υποστηριζόμενες μορφές:** Οι περισσότερες μηχανές OCR όπως το Tesseract δέχονται PNG, JPEG, TIFF. Αν δώσετε ένα BMP, θα λάβετε κωδικό σφάλματος. Μετατρέψτε με το Pillow (`Image.save(..., format=\"PNG\")`) πριν τη φόρτωση.  
- **Διαρροές μνήμης:** Η επαναχρησιμοποίηση της ίδιας μηχανής είναι αποδοτική, αλλά μην ξεχάσετε να καλέσετε `engine.close()` (ή το ισοδύναμο της βιβλιοθήκης) όταν τελειώσετε, ειδικά σε υπηρεσίες που τρέχουν πολύ χρόνο.  
- **Επεξεργασία παρτίδας:** Τυλίξτε τα βήματα φόρτωσης‑εξαγωγής σε έναν βρόχο `for` πάνω σε έναν φάκελο. Καταγράψτε κάθε σφάλμα σε ξεχωριστό αρχείο· αυτό κάνει τον εντοπισμό σφαλμάτων σε τεράστιες συλλογές δεδομένων εύκολο.

## Οπτική Επισκόπηση

![Διάγραμμα OCR εικόνας που απεικονίζει τα βήματα δημιουργίας μηχανής OCR, φόρτωσης εικόνας, διαχείρισης σφαλμάτων και εξαγωγής κειμένου](load_image_ocr_diagram.png "Ροή εργασίας OCR εικόνας")

*Alt text: διάγραμμα OCR εικόνας που απεικονίζει τα βήματα δημιουργίας μηχανής OCR, φόρτωσης εικόνας, διαχείρισης σφαλμάτων και εξαγωγής κειμένου.*

## Συμπέρασμα

Μόλις καλύψαμε όλα όσα χρειάζεστε για να **φορτώσετε OCR εικόνας** αξιόπιστα ενώ **δημιουργείτε μηχανή OCR** σε Python. Από την αρχικοποίηση της μηχανής, τη διαχείριση ελλιπών αρχείων με εξαιρέσεις και το API σφαλμάτων της βιβλιοθήκης, μέχρι την εξαγωγή του αναγνωρισμένου κειμένου, το πλήρες script είναι έτοιμο να ενσωματωθεί σε οποιοδήποτε πρότζεκτ.

Θυμηθείτε: η αξιόπιστη OCR δεν εξαρτάται μόνο από τη βιβλιοθήκη που επιλέγετε· αφορά τη χαριτωμένη διαχείριση σφαλμάτων, τη λογική διαχείριση πόρων και την καθαρή καταγραφή. Με τα πρότυπα που παρουσιάστηκαν εδώ μπορείτε να κλιμακώσετε από μια επίδειξη μίας εικόνας σε μια παραγωγική παρτίδα χωρίς να ξαναεφευρίσετε το τροχό.

### Τι Ακολουθεί;

- Πειραματιστείτε με **προεπεξεργασία εικόνας** (αύξηση αντίθεσης, ευθυγράμμιση) για βελτίωση της ακρίβειας.  
- Αντικαταστήστε τη βιβλιοθήκη `ocr` με Tesseract, EasyOCR ή μια υπηρεσία cloud και προσαρμόστε τη συνάρτηση `init_engine` ανάλογα.  
- Ενσωματώστε το αποτέλεσμα OCR σε μια βάση δεδομένων ή έναν δείκτη αναζήτησης για περιπτώσεις ανάκτησης εγγράφων.

Έχετε ερωτήσεις ή κάποιο παράξενο edge case που αντιμετωπίσατε; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}