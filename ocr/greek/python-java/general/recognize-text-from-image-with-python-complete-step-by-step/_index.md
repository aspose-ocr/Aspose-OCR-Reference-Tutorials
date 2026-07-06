---
category: general
date: 2026-06-16
description: Αναγνώριση κειμένου από εικόνα χρησιμοποιώντας Python OCR. Μάθετε πώς
  να φορτώνετε εικόνα για OCR, να ορίζετε λειτουργία υψηλής ακρίβειας και να εκτελείτε
  την αναγνώριση OCR για να μετατρέψετε την εικόνα σε κείμενο.
draft: false
keywords:
- recognize text from image
- convert image to text
- load image for ocr
- run ocr recognition
- set high accuracy mode
language: el
og_description: Αναγνώριση κειμένου από εικόνα σε Python. Αυτός ο οδηγός δείχνει πώς
  να φορτώσετε εικόνα για OCR, να ορίσετε λειτουργία υψηλής ακρίβειας και να εκτελέσετε
  την αναγνώριση OCR για να μετατρέψετε την εικόνα σε κείμενο.
og_title: Αναγνώριση κειμένου από εικόνα – Πλήρης Οδηγός OCR σε Python
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: recognize text from image using Python OCR. Learn how to load image
    for OCR, set high accuracy mode, and run OCR recognition to convert image to text.
  headline: recognize text from image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: recognize text from image using Python OCR. Learn how to load image
    for OCR, set high accuracy mode, and run OCR recognition to convert image to text.
  name: recognize text from image with Python – Complete Step‑by‑Step Guide
  steps:
  - name: 1. Empty Result
    text: 'Sometimes the engine returns an empty string. This usually means the image
      is too blurry or the text color blends with the background. Try:'
  - name: 2. Non‑Latin Scripts
    text: 'If your picture contains Cyrillic, Chinese, or Arabic characters, you’ll
      need to tell the OCR engine which language pack to use:'
  - name: 3. Large Batches
    text: Processing a folder of images? Wrap the core logic in a loop and reuse the
      same engine instance to avoid repeated initialization overhead.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Αναγνώριση κειμένου από εικόνα με Python – Πλήρης Οδηγός Βήμα‑βήμα
url: /el/python-java/general/recognize-text-from-image-with-python-complete-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# αναγνώριση κειμένου από εικόνα – Πλήρης Python OCR Tutorial

Έχετε αναρωτηθεί ποτέ πώς να **αναγνωρίσετε κείμενο από εικόνα** χωρίς να πληρώνετε για μια υπηρεσία cloud; Δεν είστε ο μόνος. Είτε ψηφιοποιείτε παλιές αποδείξεις είτε εξάγετε λεζάντες από στιγμιότυπα οθόνης, η μετατροπή μιας εικόνας σε επεξεργάσιμο κείμενο είναι μια χρήσιμη δεξιότητα.

Σε αυτό το tutorial θα περάσουμε από ένα **πλήρες, εκτελέσιμο παράδειγμα** που δείχνει πώς να **φορτώνετε εικόνα για OCR**, **ενεργοποιείτε τη λειτουργία υψηλής ακρίβειας**, και **εκτελείτε αναγνώριση OCR** ώστε να μπορείτε να **μετατρέψετε εικόνα σε κείμενο** με λίγες μόνο γραμμές Python. Χωρίς περιττές πληροφορίες, μόνο τα πρακτικά βήματα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε τώρα.

## Τι Θα Δημιουργήσετε

Στο τέλος αυτού του οδηγού θα έχετε ένα μικρό script που:

1. Δημιουργεί μια μηχανή OCR.
2. Ενεργοποιεί τη σημαία **set high accuracy mode** για καλύτερα αποτελέσματα σε εικόνες χαμηλής ανάλυσης.
3. **Φορτώνει μια εικόνα για OCR** από το δίσκο.
4. **Εκτελεί την αναγνώριση OCR** για **να αναγνωρίσει κείμενο από εικόνα**.
5. Εκτυπώνει τη εξαγόμενη συμβολοσειρά – ουσιαστικά **μετατρέποντας την εικόνα σε κείμενο**.

Αν έχετε Python 3.8+ και λίγη περιέργεια, είστε έτοιμοι να ξεκινήσετε.

## Προαπαιτήσεις

- **Python 3.8 ή νεότερο** – ο κώδικας χρησιμοποιεί type hints που οι παλαιότερες εκδόσεις δεν καταλαβαίνουν.
- Μια βιβλιοθήκη OCR που εκθέτει ένα module `ocr` (το παράδειγμα μιμείται έναν γενικό wrapper· αντικαταστήστε το με `pytesseract`, `easyocr`, ή οποιοδήποτε SDK συγκεκριμένου προμηθευτή που προτιμάτε).
- Ένα JPEG χαμηλής ανάλυσης με όνομα `low-res.jpg` σε φάκελο που ελέγχετε.
- (Προαιρετικό) Ένα εικονικό περιβάλλον για να διατηρείτε τις εξαρτήσεις τακτοποιημένες: `python -m venv venv && source venv/bin/activate`.

```bash
# Example installation for a hypothetical `ocr` package
pip install ocr-lib
```

> **Συμβουλή:** Αν χρησιμοποιείτε `pytesseract`, εγκαταστήστε ξεχωριστά τη μηχανή Tesseract (`sudo apt-get install tesseract-ocr` σε Linux, Homebrew σε macOS).

---

## Βήμα 1: Αναγνώριση Κειμένου από Εικόνα – Αρχικοποίηση της Μηχανής OCR

Πρώτα απ' όλα. Χρειαζόμαστε ένα νέο αντικείμενο μηχανής OCR που θα αναλάβει το βαριά δουλειά.

```python
# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Γιατί είναι σημαντικό:* Η κλάση `OcrEngine` είναι το σημείο εισόδου για όλες τις επόμενες λειτουργίες. Σκεφτείτε το ως τον εγκέφαλο που θα ερμηνεύσει τα pixel που του δίνετε. Η δημιουργία νέας παρουσίας σε κάθε εκτέλεση εξασφαλίζει καθαρή κατάσταση, ειδικά όταν αλλάζετε ρυθμίσεις όπως **set high accuracy mode** αργότερα.

---

## Βήμα 2: Ενεργοποίηση Λειτουργίας Υψηλής Ακρίβειας – Βελτιώστε τα Αποτελέσματα Χαμηλής Ανάλυσης

Οι εικόνες χαμηλής ανάλυσης είναι γνωστές για το ότι μπερδεύουν τις μηχανές OCR. Η ενεργοποίηση της σημαίας υψηλής ακρίβειας λέει στη μηχανή να εφαρμόσει επιπλέον προεπεξεργασία (αύξηση κλίμακας, μείωση θορύβου κ.λπ.) πριν διαβάσει τους χαρακτήρες.

```python
# Step 2: Enable high‑accuracy mode for better results
engine.high_accuracy = True   # <-- activates advanced preprocessing
```

> **Γιατί να την ενεργοποιήσετε;** Όταν η πηγή εικόνας είναι σπόρια ή μικρή, η προεπιλεγμένη λειτουργία μπορεί να χάσει γράμματα ή να συγχωνεύσει λέξεις. Η διαδρομή υψηλής ακρίβειας ανταλλάσσει λίγη ταχύτητα για αξιοσημείωτη βελτίωση στην ορθότητα — ιδανική για σενάρια που τρέχουν μία φορά όπου η καθυστέρηση δεν είναι κρίσιμη.

---

## Βήμα 3: Φόρτωση Εικόνας για OCR – Προετοιμασία του Αρχείου

Τώρα φορτώνουμε πραγματικά **την εικόνα για OCR**. Η βοηθητική μέθοδος `ocr.Image.load_from_file` αφαιρεί τα βήματα I/O και αποκωδικοποίησης εικόνας.

```python
# Step 3: Load the low‑resolution image to be processed
engine.image = ocr.Image.load_from_file("YOUR_DIRECTORY/low-res.jpg")
```

*Τι συμβαίνει στο παρασκήνιο;* Η βιβλιοθήκη διαβάζει το JPEG, το μετατρέπει σε bitmap, και το αποθηκεύει μέσα στην παρουσία της μηχανής. Αν χρειαστεί να δουλέψετε με εικόνα ήδη στη μνήμη (π.χ. από αίτημα web), οι περισσότερες βιβλιοθήκες προσφέρουν επίσης μέθοδο `from_bytes` — απλώς αντικαταστήστε την κλήση.

---

## Βήμα 4: Εκτέλεση Αναγνώρισης OCR – Η Κύρια Ενέργεια

Με τη μηχανή έτοιμη και την εικόνα στη θέση της, τελικά **εκτελούμε την αναγνώριση OCR**. Αυτό το βήμα πραγματοποιεί την πραγματική εξαγωγή κειμένου.

```python
# Step 4: Perform OCR recognition on the image
high_res_result = engine.recognize()
```

Η μέθοδος `recognize()` επιστρέφει ένα αντικείμενο αποτελέσματος που περιέχει τη ακατέργαστη συμβολοσειρά, βαθμούς εμπιστοσύνης, και μερικές φορές μεταδεδομένα bounding‑box. Για τον σκοπό του **convert image to text**, θα εστιάσουμε στο χαρακτηριστικό `text`.

---

## Βήμα 5: Εκτύπωση του Αναγνωρισμένου Κειμένου – Μετατροπή Εικόνας σε Κείμενο

Η κορύφωση της διαδικασίας: εκτύπωση της εξαγόμενης συμβολοσειράς. Εδώ η εικόνα γίνεται τελικά επεξεργάσιμο κείμενο.

```python
# Step 5: Output the recognized text
print(high_res_result.text)
```

**Αναμενόμενη έξοδος** (το πραγματικό κείμενό σας θα διαφέρει ανάλογα με την εικόνα):

```
Invoice #12345
Date: 2024‑03‑15
Total: $256.78
Thank you for your business!
```

Αν δείτε ακατάλληλους χαρακτήρες, ελέγξτε ξανά ότι η **set high accuracy mode** είναι πράγματι `True` και ότι η εικόνα δεν είναι υπερβολικά συμπιεσμένη.

---

## Διαχείριση Συνηθισμένων Περιπτώσεων

### 1. Κενό Αποτέλεσμα

Μερικές φορές η μηχανή επιστρέφει κενή συμβολοσειρά. Αυτό συνήθως σημαίνει ότι η εικόνα είναι πολύ θολή ή το χρώμα του κειμένου συγχωνεύεται με το φόντο. Δοκιμάστε:

- Αύξηση της ανάλυσης της εικόνας πριν τη φόρτωση (`PIL.Image.resize`).
- Ρύθμιση της αντίθεσης (`ImageEnhance.Contrast`).

### 2. Μη‑Λατινικά Σενάρια

Αν η εικόνα σας περιέχει κυριλλικούς, κινέζικους ή αραβικούς χαρακτήρες, θα πρέπει να ενημερώσετε τη μηχανή OCR ποιο πακέτο γλώσσας να χρησιμοποιήσει:

```python
engine.language = "eng+rus"   # Example for English + Russian
```

### 3. Μεγάλες Παρτίδες

Επεξεργάζεστε φάκελο εικόνων; Τυλίξτε τη λογική σε βρόχο και επαναχρησιμοποιήστε την ίδια παρουσία μηχανής για να αποφύγετε επαναλαμβανόμενη αρχικοποίηση.

```python
import pathlib

engine = ocr.OcrEngine()
engine.high_accuracy = True
engine.language = "eng"

for img_path in pathlib.Path("batch/").glob("*.jpg"):
    engine.image = ocr.Image.load_from_file(str(img_path))
    result = engine.recognize()
    print(f"{img_path.name}: {result.text[:50]}...")
```

---

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας τα πάντα, εδώ είναι ένα script που μπορείτε να αποθηκεύσετε σε αρχείο `ocr_demo.py` και να τρέξετε αμέσως.

```python
#!/usr/bin/env python3
"""
ocr_demo.py – Recognize text from image using a generic OCR library.
"""

import ocr  # Replace with the actual OCR package you installed

def main():
    # Initialize engine
    engine = ocr.OcrEngine()
    engine.high_accuracy = True          # set high accuracy mode
    engine.language = "eng"              # optional: specify language pack

    # Load image – change the path to your own file
    image_path = "YOUR_DIRECTORY/low-res.jpg"
    engine.image = ocr.Image.load_from_file(image_path)

    # Perform recognition
    result = engine.recognize()

    # Output the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

Αποθηκεύστε, κάντε το εκτελέσιμο (`chmod +x ocr_demo.py`), και τρέξτε:

```bash
./ocr_demo.py
```

Θα πρέπει να δείτε την έξοδο **convert image to text** να εμφανίζεται στην κονσόλα.

---

## Συμβουλές & Τεχνάσματα από το Πεδίο

- **Cache τη μηχανή** αν επεξεργάζεστε πολλές εικόνες· η δημιουργία νέας παρουσίας για κάθε αρχείο μπορεί να διπλασιάσει τον χρόνο εκτέλεσης.
- **Προεπεξεργαστείτε μόνοι σας** όταν η ενσωματωμένη λειτουργία υψηλής ακρίβειας δεν αρκεί: χρησιμοποιήστε OpenCV για μείωση θορύβου (`cv2.fastNlMeansDenoisingColored`) ή δυαδικοποίηση (`cv2.threshold`).
- **Καταγράψτε την εμπιστοσύνη** (`result.confidence`) αν χρειάζεται να φιλτράρετε αυτόματα χαμηλής ποιότητας αποτελέσματα.
- **Αποφύγετε το σκληρό κωδικοποίηση διαδρομών**· χρησιμοποιήστε `pathlib.Path` για συμβατότητα μεταξύ πλατφορμών.

---

## Συμπέρασμα

Μόλις **αναγνωρίσαμε κείμενο από εικόνα** χρησιμοποιώντας μια απλή ροή εργασίας Python: **φορτώνουμε εικόνα για OCR**, **ενεργοποιούμε τη λειτουργία υψηλής ακρίβειας**, **εκτελούμε αναγνώριση OCR**, και τελικά **μετατρέπουμε την εικόνα σε κείμενο**. Ολόκληρη η αλυσίδα χωράει σε λιγότερο από είκοσι γραμμές, αλλά είναι αρκετά ευέλικτη για παρτίδες, πολυγλωσσικά έγγραφα και θορυβώδεις εισόδους.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να αντικαταστήσετε τη γενική βιβλιοθήκη `ocr` με `pytesseract` ή `easyocr`, πειραματιστείτε με επιπλέον βήματα προεπεξεργασίας, ή ενσωματώστε το script σε API Flask ώστε να μπορείτε να ανεβάζετε εικόνες από μια ιστοσελίδα και να λαμβάνετε ζωντανές μεταγραφές.

Έχετε ερωτήσεις ή ένα ενδιαφέρον σενάριο χρήσης; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

## Τι Θα Πρέπει Να Μάθετε Στη Συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}