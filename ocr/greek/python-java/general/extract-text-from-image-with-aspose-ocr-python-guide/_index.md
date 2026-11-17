---
category: general
date: 2026-03-28
description: Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας το Aspose OCR σε Python –
  μάθετε πώς να αναγνωρίζετε κείμενο από PNG, να μετατρέπετε εικόνα σε κείμενο με
  Python και να φορτώνετε εικόνα για OCR γρήγορα.
draft: false
keywords:
- extract text from image
- recognize text from png
- convert image to text python
- load image for ocr
- read text from scanned image
language: el
og_description: Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας το Aspose OCR σε Python.
  Αυτό το σεμινάριο δείχνει πώς να αναγνωρίζετε κείμενο από PNG, να μετατρέπετε εικόνα
  σε κείμενο με Python και να φορτώνετε εικόνα για OCR.
og_title: Εξαγωγή κειμένου από εικόνα με Aspose OCR – Οδηγός Python
tags:
- OCR
- Python
- Aspose
- Image Processing
title: Εξαγωγή κειμένου από εικόνα με το Aspose OCR – Οδηγός Python
url: /el/python-java/general/extract-text-from-image-with-aspose-ocr-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή κειμένου από εικόνα με Aspose OCR – Python guide

Έχετε ποτέ χρειαστεί να **εξάγετε κείμενο από εικόνα** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη θα σας δώσει αξιόπιστα αποτελέσματα σε σάρωση PNG; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν δουλεύουν με σαρωμένα PDF ή φωτογραφίες αποδείξεων. Τα καλά νέα; Με το Aspose OCR for Python μπορείτε να αναγνωρίσετε κείμενο από αρχεία PNG, να μετατρέψετε εικόνα σε κείμενο σε στυλ Python και να φορτώσετε εικόνα για OCR με λίγες μόνο γραμμές κώδικα.

Σε αυτό το tutorial θα περάσουμε βήμα-βήμα ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει ακριβώς πώς να **εξάγετε κείμενο από εικόνα** χρησιμοποιώντας το Aspose OCR. Θα δείτε πώς να φορτώσετε την εικόνα, να ενεργοποιήσετε την αυτόματη ανίχνευση γλώσσας, να εκτελέσετε τη μηχανή OCR και τελικά να διαβάσετε τη ανιχνευμένη γλώσσα και το εξαγόμενο κείμενο. Στο τέλος θα μπορείτε να ενσωματώσετε αυτόν τον κώδικα σε οποιοδήποτε έργο που χρειάζεται να διαβάσει κείμενο από σαρωμένα αρχεία εικόνας.

## Τι θα μάθετε

- Πώς να **φορτώσετε εικόνα για OCR** με Aspose Storage.
- Πώς να **αναγνωρίσετε κείμενο από PNG** και να ανιχνεύσετε αυτόματα τη γλώσσα του.
- Πώς να **μετατρέψετε εικόνα σε κείμενο python** χωρίς να ασχοληθείτε με χαμηλού επιπέδου byte buffers.
- Συμβουλές για τη διαχείριση PDF πολλαπλών σελίδων, κοινά εμπόδια και σενάρια άκρων.
- Αναμενόμενο αποτέλεσμα και γρήγοροι τρόποι επαλήθευσης ότι η εξαγωγή ήταν επιτυχής.

### Προαπαιτούμενα

- Python 3.8 + εγκατεστημένο στο σύστημά σας.
- Άδεια Aspose OCR for Python (ή κλειδί δωρεάν δοκιμής) – μπορείτε να το αποκτήσετε από την ιστοσελίδα Aspose.
- Τα πακέτα `aspose-ocr` και `aspose-storage` εγκατεστημένα μέσω `pip install aspose-ocr aspose-storage`.
- Ένα αρχείο PNG ή οποιοδήποτε άλλο υποστηριζόμενο αρχείο εικόνας που θέλετε να επεξεργαστείτε.

Τώρα, ας ξεκινήσουμε.

## Βήμα 1: Φόρτωση εικόνας για OCR

Πριν η μηχανή OCR μπορέσει να κάνει οτιδήποτε, χρειάζεται ένα αντικείμενο εικόνας. Το Aspose Storage το κάνει αυτό εύκολο.

```python
# Step 1: Import required Aspose modules
import aspose.ocr as aocr
import aspose.storage as storage

# Step 1.1: Define the path to your image file
input_image_path = "YOUR_DIRECTORY/input_image.png"

# Step 1.2: Load the image – Aspose supports PNG, JPEG, BMP, TIFF, etc.
# The Image class abstracts away file‑system handling.
image = storage.Image.load(input_image_path)
```

*Γιατί είναι σημαντικό:* Η χρήση του `storage.Image.load` αφαιρεί τις ιδιαιτερότητες του συγκεκριμένου φορμά, ώστε να μπορείτε να **αναγνωρίσετε κείμενο από png** ή JPEG χωρίς να γράψετε προσαρμοστικούς φορτωτές. Αν το αρχείο δεν βρεθεί, το Aspose ρίχνει ένα σαφές `FileNotFoundError`, το οποίο μπορείτε να πιάσετε για ευγενική εναλλακτική.

> **Pro tip:** Κρατήστε τις εικόνες σας κάτω από 5 MB για καλύτερη απόδοση. Μεγαλύτερα αρχεία μπορούν να υποβληθούν σε down‑sampling με `image.resize()` πριν το OCR.

## Βήμα 2: Αρχικοποίηση της μηχανής OCR και ενεργοποίηση ανίχνευσης γλώσσας

Το Aspose OCR περιλαμβάνει μια ισχυρή `OcrEngine` που μπορεί να ανιχνεύσει αυτόματα τη γλώσσα του κειμένου που βλέπει. Η ενεργοποίηση αυτής της λειτουργίας συχνά αυξάνει την ακρίβεια για πολύγλωσσα έγγραφα.

```python
# Step 2: Initialise the OCR engine
ocr_engine = aocr.OcrEngine()

# Step 2.1: Enable automatic language detection (AUTO mode)
ocr_engine.language_detection = aocr.LanguageDetectionMode.AUTO
```

*Γιατί είναι σημαντικό:* Όταν **μετατρέπετε εικόνα σε κείμενο python** σε στυλ, συνήθως σας ενδιαφέρει η γλώσσα επειδή επηρεάζει το σύνολο χαρακτήρων και το λεξικό που χρησιμοποιείται κατά την αναγνώριση. Η λειτουργία AUTO επιτρέπει στη μηχανή να επιλέξει την καλύτερη αντιστοιχία, είτε είναι Αγγλικά, Ισπανικά ή Κινέζικα.

## Βήμα 3: Αναγνώριση κειμένου από PNG και εξαγωγή του αποτελέσματος

Τώρα γίνεται η βαριά δουλειά. Η μέθοδος `recognize` εκτελεί την αλυσίδα OCR και επιστρέφει ένα πλούσιο αντικείμενο αποτελέσματος.

```python
# Step 3: Run OCR on the loaded image
ocr_result = ocr_engine.recognize(image)

# Step 3.1: Pull out the detected language and the plain text
detected_lang = ocr_result.detected_language
extracted_text = ocr_result.text
```

Αν χρειάζεστε μόνο το ακατέργαστο κείμενο, το `ocr_result.text` είναι έτοιμο για χρήση. Η ιδιότητα `detected_language` σας δίνει έναν κωδικό ISO‑639‑1 (π.χ., `"en"` για Αγγλικά).

> **Edge case:** Για πολύ κατεστραμμένες σαρώσεις, η μηχανή μπορεί να επιστρέψει κενή συμβολοσειρά. Σε αυτήν την περίπτωση, σκεφτείτε την προεπεξεργασία της εικόνας (αύξηση αντίθεσης, διόρθωση κλίσης) χρησιμοποιώντας βιβλιοθήκες όπως το Pillow πριν τη δώσετε στο Aspose.

## Βήμα 4: Εμφάνιση του αποτελέσματος – τι να περιμένετε

Ας εκτυπώσουμε τα αποτελέσματα ώστε να μπορείτε να επαληθεύσετε ότι όλα λειτούργησαν.

```python
# Step 4: Show the detection results
print(f"Detected language: {detected_lang}")
print("Extracted text:")
print(extracted_text)
```

### Παράδειγμα εξόδου

```
Detected language: en
Extracted text:
Invoice #12345
Date: 2026‑03‑01
Total: $1,250.00
Thank you for your business!
```

Αν δείτε κάτι παρόμοιο, συγχαρητήρια—έχετε εξαγάγει με επιτυχία **κείμενο από εικόνα** χρησιμοποιώντας το Aspose OCR! Αν η έξοδος φαίνεται χαοτική, ελέγξτε ξανά ότι η ποιότητα της εικόνας είναι επαρκής (τουλάχιστον 300 dpi για τυπωμένο κείμενο).

## Βήμα 5: Προχωρημένες συμβουλές – διαχείριση PDF πολλαπλών σελίδων και σαρωμένων εγγράφων

Ενώ η βασική ροή λειτουργεί για ένα μόνο PNG, οι πραγματικές περιπτώσεις συχνά περιλαμβάνουν PDF πολλαπλών σελίδων ή στοίβες TIFF.

1. **Μετατροπή σελίδων PDF σε εικόνες** – Το Aspose PDF μπορεί να αποδώσει κάθε σελίδα ως PNG, την οποία στη συνέχεια τροφοδοτείτε στον βρόχο OCR.
2. **Επεξεργασία σε παρτίδες** – Επανάληψη πάνω σε έναν φάκελο σαρωμένων εικόνων, συγκεντρώνοντας τα αποτελέσματα σε λίστα ή γράφοντάς τα σε CSV.
3. **Προσαρμοσμένη επιλογή γλώσσας** – Αν γνωρίζετε ότι το έγγραφο είναι πάντα Γαλλικό, ορίστε `ocr_engine.language_detection = aocr.LanguageDetectionMode.FRENCH` για αύξηση ταχύτητας.

```python
# Example: Batch processing a folder of PNGs
import os

folder = "scans/"
texts = []
for file_name in os.listdir(folder):
    if file_name.lower().endswith(".png"):
        img = storage.Image.load(os.path.join(folder, file_name))
        result = ocr_engine.recognize(img)
        texts.append({"file": file_name,
                      "lang": result.detected_language,
                      "text": result.text})
```

Τώρα έχετε μια χρήσιμη συλλογή που μπορείτε να εξάγετε με `json` ή `pandas`.

## Βήμα 6: Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|-------|----------------|-----|
| Κενή έξοδος | Η εικόνα έχει πολύ χαμηλή ανάλυση ή είναι υπερβολικά συμπιεσμένη | Αυξήστε την ανάλυση σε ≥300 dpi, χρησιμοποιήστε Pillow για όξυνση |
| Λάθος ανίχνευση γλώσσας | Σελίδες με ανάμειξη γλωσσών | Ορίστε χειροκίνητα `language_detection` σε συγκεκριμένη γλώσσα ή επεξεργαστείτε κάθε σελίδα ξεχωριστά |
| Σφάλμα μνήμης σε μεγάλες παρτίδες | Φόρτωση πολλών εικόνων υψηλής ανάλυσης ταυτόχρονα | Επεξεργαστείτε τις εικόνες μία-μία, ή χρησιμοποιήστε `gc.collect()` μετά από κάθε επανάληψη |
| Απρόσμενοι χαρακτήρες | Η γραμματοσειρά δεν υποστηρίζεται από το λεξικό OCR | Ενεργοποιήστε `ocr_engine.enable_complex_script` εάν εργάζεστε με Αραβικά ή Χίντι |

## Πλήρες εκτελέσιμο σενάριο

Ακολουθεί το πλήρες σενάριο που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα αρχείο με όνομα `extract_text.py`. Αντικαταστήστε το `YOUR_DIRECTORY/input_image.png` με την πραγματική διαδρομή προς την εικόνα σας.

```python
# extract_text.py
# Complete example: extract text from image with Aspose OCR (Python)

import aspose.ocr as aocr
import aspose.storage as storage

def main():
    # 1️⃣ Load the image
    input_image_path = "YOUR_DIRECTORY/input_image.png"
    try:
        image = storage.Image.load(input_image_path)
    except Exception as e:
        print(f"❗ Unable to load image: {e}")
        return

    # 2️⃣ Initialise OCR engine and enable auto language detection
    ocr_engine = aocr.OcrEngine()
    ocr_engine.language_detection = aocr.LanguageDetectionMode.AUTO

    # 3️⃣ Run OCR
    try:
        ocr_result = ocr_engine.recognize(image)
    except Exception as e:
        print(f"❗ OCR failed: {e}")
        return

    # 4️⃣ Output results
    print(f"Detected language: {ocr_result.detected_language}")
    print("Extracted text:")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

Τρέξτε το με:

```bash
python extract_text.py
```

Θα πρέπει να δείτε τη ανιχνευμένη γλώσσα ακολουθούμενη από το εξαγόμενο κείμενο να εκτυπώνονται στην κονσόλα.

## Συμπέρασμα

Τώρα ξέρετε πώς να **εξάγετε κείμενο από εικόνα** χρησιμοποιώντας το Aspose OCR σε Python, από τη φόρτωση του αρχείου μέχρι την εμφάνιση του αναγνωρισμένου κειμένου. Αυτή η ολοκληρωμένη λύση σας επιτρέπει να **αναγνωρίζετε κείμενο από png**, να **μετατρέπετε εικόνα σε κείμενο python** σε στυλ, και άνετα να **φορτώνετε εικόνα για OCR** σε οποιοδήποτε pipeline αυτοματοποίησης.

Επόμενα βήματα; Δοκιμάστε να τροφοδοτήσετε ένα σύνολο σαρωμένων αποδείξεων στο σενάριο, εξάγετε τα αποτελέσματα σε CSV, ή ενσωματώστε το βήμα OCR σε μια μεγαλύτερη ροή επεξεργασίας εγγράφων (π.χ., αυτόματη συμπλήρωση βάσης δεδομένων). Μπορείτε επίσης να εξερευνήσετε τη βιβλιοθήκη Aspose PDF για να μετατρέψετε σαρωμένα PDF σε έγγραφα με δυνατότητα αναζήτησης—μια προφανής επέκταση εάν εργάζεστε με **read text from scanned image** PDF.

Καλή προγραμματιστική, και μη διστάσετε να πειραματιστείτε με διαφορετικές ρυθμίσεις γλώσσας, τεχνικές προεπεξεργασίας εικόνας, ή ακόμη και συνδυάζοντας το Aspose OCR με το Tesseract για μια υβριδική προσέγγιση. Αν αντιμετωπίσετε οποιοδήποτε πρόβλημα, αφήστε ένα σχόλιο παρακάτω—ας το λύσουμε μαζί!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}