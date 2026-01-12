---
category: general
date: 2026-01-12
description: Πώς να εκτελέσετε OCR γρήγορα και με ακρίβεια. Μάθετε πώς να τρέχετε
  OCR σε έγγραφο, να εξάγετε κείμενο από tiff, να φορτώνετε εικόνα για OCR και να
  ορίζετε τη γλώσσα OCR στην Python.
draft: false
keywords:
- how to perform ocr
- run ocr on document
- extract text from tiff
- load image for ocr
- set OCR language
language: el
og_description: Πώς να εκτελέσετε OCR στην Python. Αυτό το σεμινάριο σας δείχνει πώς
  να εκτελείτε OCR σε έγγραφο, να εξάγετε κείμενο από tiff, να φορτώνετε εικόνα για
  OCR και να ορίζετε τη γλώσσα OCR.
og_title: Πώς να εκτελέσετε OCR σε έγγραφο TIFF – Πλήρης οδηγός
tags:
- OCR
- Python
- Image Processing
title: Πώς να εκτελέσετε OCR σε έγγραφο TIFF – Οδηγός βήμα‑προς‑βήμα
url: /el/python-java/general/how-to-perform-ocr-on-a-tiff-document-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εκτελέσετε OCR σε έγγραφο TIFF – Οδηγός πλήρους

Έχετε αναρωτηθεί ποτέ **πώς να εκτελέσετε OCR** σε ένα σαρωμένο αρχείο TIFF χωρίς να ξοδεύετε ώρες ψάχνοντας τη σωστή βιβλιοθήκη; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν πρόβλημα όταν χρειάζεται να εξάγουν κείμενο από εικόνες TIFF, ειδικά όταν η απόδοση και οι ρυθμίσεις γλώσσας έχουν σημασία.

Σε αυτό το tutorial θα περάσουμε από όλα όσα χρειάζεται να γνωρίζετε: από την εγκατάσταση του πακέτου OCR, τη φόρτωση της εικόνας για OCR, τον ορισμό της γλώσσας OCR, μέχρι τελικά **να τρέξετε OCR στο έγγραφο** και να εξάγετε καθαρό κείμενο. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση script που μπορείτε να ενσωματώσετε σε οποιοδήποτε project.

> **Pro tip:** Αν και το παράδειγμα χρησιμοποιεί ένα γενικό module `ocr`, οι ίδιες έννοιες ισχύουν για Tesseract, EasyOCR ή οποιοδήποτε σύγχρονο OCR engine που εκθέτει Python API.

---

## Τι θα χρειαστείτε

- Python 3.8+ (οποιαδήποτε πρόσφατη έκδοση λειτουργεί)
- Μια βιβλιοθήκη OCR που παρέχει κλάση `OcrEngine` (το δείγμα χρησιμοποιεί ένα φανταστικό πακέτο `ocr`; αντικαταστήστε το με το πραγματικό σας)
- Ένα πολυ‑σελίδων αρχείο TIFF που θέλετε να επεξεργαστείτε (θα το ονομάσουμε `big_document.tif`)
- Ένα μηχάνημα με τουλάχιστον 4 πυρήνες CPU αν σκοπεύετε να ορίσετε αριθμό νημάτων

Δεν απαιτούνται εξωτερικές υπηρεσίες, κλειδιά cloud — μόνο τοπικός κώδικας που τρέχει σε δευτερόλεπτα.

---

![how to perform ocr example](/images/ocr-example.png "how to perform OCR on a TIFF document")

*Image alt text: πώς να εκτελέσετε OCR σε έγγραφο TIFF – προεπισκόπηση του εξαγόμενου κειμένου.*

---

## Βήμα 1: Εγκατάσταση και Εισαγωγή της Βιβλιοθήκης OCR

Πρώτα απ' όλα: αποκτήστε τη βιβλιοθήκη στο μηχάνημά σας. Οι περισσότερες βιβλιοθήκες OCR είναι στο PyPI, οπότε μια απλή `pip install` κάνει τη δουλειά.

```bash
pip install ocr‑engine   # replace with the actual package name, e.g., pytesseract
```

Τώρα εισάγετε τις κλάσεις που θα χρειαστείτε. Αν χρησιμοποιείτε Tesseract, η γραμμή εισαγωγής θα είναι διαφορετική, αλλά το υπόλοιπο του κώδικα παραμένει το ίδιο.

```python
# Step 1: Import the OCR engine and image helper
import ocr                       # fictional package – swap with your real one
from ocr import OcrEngine, Image
```

*Γιατί είναι σημαντικό:* Η έγκαιρη εισαγωγή των σωστών συμβόλων αποτρέπει συγκρούσεις ονομάτων αργότερα και κάνει το script πιο ευανάγνωστο.

---

## Βήμα 2: Δημιουργία και Διαμόρφωση του OCR Engine (Ορισμός Γλώσσας OCR)

Η διαμόρφωση του engine είναι το σημείο όπου **ορίζετε τη γλώσσα OCR** για ακριβή αναγνώριση. Η αγγλική είναι η προεπιλογή, αλλά μπορείτε να μεταβείτε σε γαλλικά, γερμανικά ή ακόμη και σε πολυγλωσσική λειτουργία με μια μόνο γραμμή.

```python
# Step 2: Initialize the engine and set language
ocr_engine = OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # set OCR language to English
ocr_engine.set_thread_count(4)               # limit processing to 4 CPU cores
ocr_engine.set_memory_limit(512 * 1024 * 1024)  # 512 MB internal buffer
```

> **Γιατί 4 νήματα;** Τα περισσότερα σύγχρονα laptops έχουν τουλάχιστον τέσσερις πυρήνες, και ο περιορισμός του αριθμού νημάτων αποτρέπει το OCR από το να καταναλώνει όλη τη μηχανή — ιδιαίτερα χρήσιμο όταν το script τρέχει σε κοινόχρηστο server.

Αν χρειάζεστε άλλη γλώσσα, απλώς αντικαταστήστε το `ocr.Language.ENGLISH` με `ocr.Language.FRENCH`, `ocr.Language.SPANISH`, κ.λπ.

---

## Βήμα 3: Φόρτωση Εικόνας για OCR (Load Image for OCR)

Τώρα **φορτώνουμε την εικόνα για OCR**. Η μέθοδος `Image.load` διαβάζει το αρχείο TIFF στη μνήμη, χειριζόμενη αυτόματα πολυ‑σελίδες έγγραφα.

```python
# Step 3: Load the TIFF image you want to process
image_path = "YOUR_DIRECTORY/big_document.tif"
image = Image.load(image_path)   # load image for OCR
```

*Edge case:* Αν το αρχείο είναι τεράστιο, μπορεί να εξαντλήσει τη RAM. Σε αυτή την περίπτωση, σκεφτείτε να φορτώνετε μία σελίδα τη φορά με `Image.load_page(page_number)` (αν η βιβλιοθήκη το υποστηρίζει).

---

## Βήμα 4: Εκτέλεση OCR στο Έγγραφο

Με το engine έτοιμο και την εικόνα φορτωμένη, ήρθε η ώρα να **τρέξετε OCR στο έγγραφο**. Η μέθοδος `process` κάνει το βαρέως βάρους έργο και επιστρέφει ένα αντικείμενο αποτελέσματος.

```python
# Step 4: Execute OCR
ocr_result = ocr_engine.process(image)
```

Στο παρασκήνιο, το engine χωρίζει την εικόνα σε μπλοκ κειμένου, τρέχει το μοντέλο αναγνώρισης και ενώνει τα αποτελέσματα. Η κλήση είναι blocking, δηλαδή το script περιμένει μέχρι να επεξεργαστεί ολόκληρο το TIFF — ιδανικό για batch jobs.

---

## Βήμα 5: Εξαγωγή Κειμένου από TIFF και Επαλήθευση Αποτελέσματος

Τέλος, **εξάγουμε το κείμενο από το TIFF** προσπερνώντας το χαρακτηριστικό `text` του αποτελέσματος. Ας εκτυπώσουμε τους πρώτους 200 χαρακτήρες ως γρήγορο έλεγχο.

```python
# Step 5: Show a preview of the recognized text
preview = ocr_result.text[:200]   # first 200 characters
print("Preview of OCR output:\n", preview)
```

**Αναμενόμενο αποτέλεσμα (παράδειγμα):**

```
Preview of OCR output:
 In the United States, the Constitution guarantees the ...
```

Αν χρειάζεστε ολόκληρο το κείμενο, απλώς χρησιμοποιήστε `ocr_result.text`. Για επεξεργασία downstream, ίσως θελήσετε να το γράψετε σε αρχείο `.txt`:

```python
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(ocr_result.text)
```

---

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι ένα έτοιμο‑για‑εκτέλεση script. Αντικαταστήστε το όνομα του placeholder πακέτου με αυτό που έχετε εγκαταστήσει.

```python
# -*- coding: utf-8 -*-
"""
How to Perform OCR on a TIFF Document – Complete Example
"""

# Install the OCR library first:
# pip install ocr-engine   # adjust to your actual package

import ocr
from ocr import OcrEngine, Image

def main():
    # 1️⃣ Initialize and configure the engine
    engine = OcrEngine()
    engine.language = ocr.Language.ENGLISH
    engine.set_thread_count(4)
    engine.set_memory_limit(512 * 1024 * 1024)

    # 2️⃣ Load the TIFF image
    img_path = "YOUR_DIRECTORY/big_document.tif"
    img = Image.load(img_path)

    # 3️⃣ Run OCR on the loaded image
    result = engine.process(img)

    # 4️⃣ Show a short preview and save the full text
    print("First 200 chars of OCR output:")
    print(result.text[:200])

    with open("extracted_text.txt", "w", encoding="utf-8") as out_file:
        out_file.write(result.text)

    print("\n✅ Extraction complete – see 'extracted_text.txt' for full output.")

if __name__ == "__main__":
    main()
```

Τρέξτε το script με:

```bash
python ocr_tiff_example.py
```

Θα δείτε μια προεπισκόπηση στην κονσόλα και ένα αρχείο με όνομα `extracted_text.txt` που περιέχει τη πλήρη απομαγνητοφώνηση.

---

## Συχνές Ερωτήσεις & Edge Cases

- **Τι γίνεται αν το TIFF περιέχει πολλαπλές σελίδες;**  
  Οι περισσότερες μηχανές OCR αντιμετωπίζουν κάθε σελίδα ως ξεχωριστή εικόνα εσωτερικά. Το `ocr_result.text` θα περιέχει μια αλλαγή γραμμής μεταξύ των σελίδων. Αν χρειάζεστε χειρισμό ανά σελίδα, επαναλάβετε με `Image.load_page(page_number)`.

- **Μπορώ να επεξεργαστώ PNG ή JPEG αντί για TIFF;**  
  Απόλυτα. Η μέθοδος `Image.load` συνήθως δέχεται οποιαδήποτε μορφή υποστηρίζεται από Pillow ή τη βασική βιβλιοθήκη. Απλώς αλλάξτε την επέκταση του αρχείου.

- **Το κείμενό μου είναι ακατάληπτο — πρέπει να αλλάξω τη γλώσσα;**  
  Ναι. Το βήμα **ορισμού γλώσσας OCR** είναι κρίσιμο για μη‑αγγλικά έγγραφα. Βεβαιωθείτε ότι το πακέτο γλώσσας είναι εγκατεστημένο (π.χ., `tesseract‑lang‑fra` για γαλλικά).

- **Τρέχει η μνήμη;**  
  Μειώστε το `set_memory_limit` ή επεξεργαστείτε τις σελίδες μία‑μία. Κάποιες μηχανές επιτρέπουν επίσης τη μείωση της ανάλυσης της εικόνας πριν από την αναγνώριση.

---

## Συμπέρασμα

Αυτά είναι — ένας σύντομος, πλήρως λειτουργικός οδηγός για **πώς να εκτελέσετε OCR** σε αρχείο TIFF χρησιμοποιώντας Python. Καλύψαμε τα πάντα, από την εγκατάσταση της βιβλιοθήκης, τη διαμόρφωση του engine (συμπεριλαμβανομένου του **ορισμού γλώσσας OCR**), **φόρτωση εικόνας για OCR**, **εκτέλεση OCR στο έγγραφο**, και τέλος **εξαγωγή κειμένου από TIFF**.  

Μη διστάσετε να πειραματιστείτε: αλλάξτε τον αριθμό νημάτων, εναλλάξτε γλώσσες, ή τροφοδοτήστε το αποτέλεσμα OCR σε pipeline φυσικής γλώσσας. Ο ουρανός είναι το όριο μόλις κυριαρχήσετε τα βασικά.

Έχετε περισσότερες ερωτήσεις; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}