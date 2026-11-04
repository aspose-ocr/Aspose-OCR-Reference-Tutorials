---
category: general
date: 2026-06-19
description: Βελτιώστε την ακρίβεια OCR στην Python χρησιμοποιώντας το Aspose OCR.
  Μάθετε πώς να ορίσετε τη γλώσσα OCR, να φορτώσετε εικόνα για OCR και να εξάγετε
  κείμενο από την εικόνα με ένα προσαρμοσμένο λεξικό.
draft: false
keywords:
- improve OCR accuracy
- extract text from image
- perform OCR on image
- load image for OCR
- set OCR language
language: el
og_description: Βελτιώστε την ακρίβεια OCR στην Python ορίζοντας τη γλώσσα OCR, φορτώνοντας
  μια εικόνα για OCR και εξάγοντας κείμενο από την εικόνα με προσαρμοσμένο λεξικό.
og_title: Βελτιώστε την ακρίβεια OCR στην Python – Οδηγός βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Improve OCR accuracy in Python using Aspose OCR. Learn how to set OCR
    language, load image for OCR, and extract text from image with a custom dictionary.
  headline: Improve OCR Accuracy in Python – Complete Guide
  type: TechArticle
- description: Improve OCR accuracy in Python using Aspose OCR. Learn how to set OCR
    language, load image for OCR, and extract text from image with a custom dictionary.
  name: Improve OCR Accuracy in Python – Complete Guide
  steps:
  - name: '**Pre‑processing** – Apply contrast enhancement or binarization with Pillow
      before feeding the image to Aspose OCR.'
    text: '**Pre‑processing** – Apply contrast enhancement or binarization with Pillow
      before feeding the image to Aspose OCR.'
  - name: '**Multiple Languages** – Set `engine.language = ocr.Language.English |
      ocr.Language.French` to enable bilingual recognition.'
    text: '**Multiple Languages** – Set `engine.language = ocr.Language.English |
      ocr.Language.French` to enable bilingual recognition.'
  - name: '**Region‑Based OCR** – If you only need a specific area (e.g., a table),
      crop the image first to reduce noise.'
    text: '**Region‑Based OCR** – If you only need a specific area (e.g., a table),
      crop the image first to reduce noise.'
  - name: '**Confidence Filtering** – `result.confidence` gives a per‑character score;
      you can discard low‑confidence results programmatically.'
    text: '**Confidence Filtering** – `result.confidence` gives a per‑character score;
      you can discard low‑confidence results programmatically.'
  - name: '**Setting the OCR language** to match your document.'
    text: '**Setting the OCR language** to match your document.'
  - name: '**Loading the image correctly** so the engine sees the right pixels.'
    text: '**Loading the image correctly** so the engine sees the right pixels.'
  - name: '**Performing OCR on the image** with a single method call.'
    text: '**Performing OCR on the image** with a single method call.'
  - name: '**Extracting text from the image** and confirming the result.'
    text: '**Extracting text from the image** and confirming the result.'
  - name: '**Adding a custom dictionary** to lock in domain‑specific terms.'
    text: '**Adding a custom dictionary** to lock in domain‑specific terms.'
  type: HowTo
tags:
- OCR
- Python
- Aspose
title: Βελτιώστε την ακρίβεια OCR σε Python – Πλήρης οδηγός
url: /el/python-java/general/improve-ocr-accuracy-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Βελτιώστε την Ακρίβεια OCR σε Python – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ πώς να **βελτιώσετε την ακρίβεια OCR** όταν το κείμενο που σαρώνετε περιέχει παράξενα σύμβολα, κωδικούς προϊόντων ή ονόματα εμπορικών σημάτων; Δεν είστε μόνοι. Σε πολλά έργα η προεπιλεγμένη μηχανή παράγει ακατανόητο κείμενο, και αυτό είναι πραγματικός περιορισμός παραγωγικότητας.

Σε αυτό το tutorial θα περάσουμε από ένα πρακτικό, ολοκληρωμένο παράδειγμα που σας δείχνει πώς να **ορίσετε τη γλώσσα OCR**, **φορτώσετε εικόνα για OCR**, **εκτελέσετε OCR στην εικόνα**, και τέλος **εξάγετε κείμενο από την εικόνα** με ένα προσαρμοσμένο λεξικό που αυξάνει τα ποσοστά αναγνώρισης. Στο τέλος θα έχετε ένα έτοιμο προς εκτέλεση script που μπορείτε να ενσωματώσετε σε οποιαδήποτε βάση κώδικα Python.

## Τι Θα Αποκομίσετε

- Ένα πλήρως λειτουργικό script Python που χρησιμοποιεί το Aspose OCR για ανάγνωση αρχείου PNG.
- Τη δυνατότητα να **βελτιώσετε την ακρίβεια OCR** διαμορφώνοντας τη γλώσσα και μια προσαρμοσμένη λίστα λέξεων.
- Σαφείς εξηγήσεις για το γιατί κάθε ρύθμιση είναι σημαντική, καθώς και συμβουλές για την αντιμετώπιση ειδικών περιπτώσεων όπως μη‑λατινικοί χαρακτήρες.
- Μια γρήγορη λίστα ελέγχου για την αντιμετώπιση κοινών προβλημάτων OCR.

### Προαπαιτούμενα

- Python 3.8 ή νεότερο εγκατεστημένο στο μηχάνημά σας.  
- Πακέτο `aspose-ocr` (εγκατάσταση μέσω `pip install aspose-ocr`).  
- Ένα δείγμα εικόνας (`technical_doc.png`) που περιέχει το κείμενο που θέλετε να διαβάσετε.  
- Βασική εξοικείωση με την Python — δεν απαιτείται τίποτα περίπλοκο.

> **Pro tip:** Εάν εργάζεστε σε εικονικό περιβάλλον, ενεργοποιήστε το πριν εγκαταστήσετε το πακέτο. Διατηρεί τις εξαρτήσεις σας οργανωμένες και αποτρέπει συγκρούσεις εκδόσεων.

## Βήμα 1: Εγκατάσταση και Εισαγωγή του Aspose OCR

Πρώτα απ' όλα—ας προσθέσουμε τη βιβλιοθήκη στο περιβάλλον μας και να εισάγουμε τα στοιχεία που χρειαζόμαστε.

```python
# Install the package (run this once in your terminal)
# pip install aspose-ocr

import aspose.ocr as ocr
```

Το namespace `aspose.ocr` σας δίνει πρόσβαση στην κλάση `OcrEngine`, η οποία αποτελεί την καρδιά της διαδικασίας OCR. Η εισαγωγή της εδώ διατηρεί το υπόλοιπο script καθαρό και ευανάγνωστο.

## Βήμα 2: Δημιουργία Μηχανής OCR και **Ορισμός Γλώσσας OCR**

Γιατί είναι σημαντική η γλώσσα; Οι μηχανές OCR βασίζονται σε μοντέλα ειδικά για κάθε γλώσσα ώστε να αναγνωρίζουν τα σχήματα των χαρακτήρων και τα πρότυπα λέξεων. Εάν πείτε στη μηχανή ότι σαρώνετε αγγλικό κείμενο, θα αγνοήσει τα κυριλλικά σύμβολα και θα εστιάσει στο λατινικό αλφάβητο, βελτιώνοντας δραστικά την **ακρίβεια OCR**.

```python
# Step 2: Initialize the OCR engine
engine = ocr.OcrEngine()

# Set the recognition language to English (you can pick other languages too)
engine.language = ocr.Language.English
```

> **Note:** Το Aspose OCR υποστηρίζει πάνω από 50 γλώσσες. Αντικαταστήστε το `ocr.Language.English` με `ocr.Language.Spanish`, `ocr.Language.French`, κ.λπ., εάν το έγγραφό σας δεν είναι αγγλικό.

## Βήμα 3: Ορισμός **Προσαρμοσμένου Λεξικού** για Βελτίωση της Ακρίβειας

Φανταστείτε ότι σαρώνετε τιμολόγια που περιέχουν τη λέξη “AsposeOCR” ή κωδικούς προϊόντων όπως “SKU12345”. Η μηχανή δεν γνωρίζει αυτούς τους όρους, οπότε κάνει λανθασμένες εικασίες. Η παροχή μιας προσαρμοσμένης λίστας λέξεων λέει στη μηχανή, *«Εντάξει, αυτές οι ακολουθίες είναι έγκυρες—μην προσπαθήσετε να τις διορθώσετε»*. Αυτό είναι ένα γρήγορο κέρδος για **βελτίωση της ακρίβειας OCR**.

```python
# Step 3: Create a list of domain‑specific words
custom_word_list = [
    "AsposeOCR",   # brand name
    "InvoiceID",   # field label
    "SKU12345",    # product code
    "β‑cell"       # Greek character example
]

# Attach the custom dictionary to the engine
engine.text_processing.custom_dictionary = custom_word_list
```

Μπορείτε να φορτώσετε αυτή τη λίστα από αρχείο ή βάση δεδομένων εάν έχετε εκατοντάδες καταχωρήσεις—απλώς κρατήστε την σε μια λίστα Python για απλότητα.

## Βήμα 4: **Φόρτωση Εικόνας για OCR**

Τώρα χρειαζόμαστε μια εικόνα. Η μέθοδος `Image.load` δέχεται διαδρομή προς οποιαδήποτε υποστηριζόμενη μορφή raster (PNG, JPEG, BMP, κ.λπ.). Εάν το αρχείο δεν βρεθεί, η μηχανή ρίχνει εξαίρεση, οπότε θα το προστατεύσουμε.

```python
import os

image_path = "YOUR_DIRECTORY/technical_doc.png"

if not os.path.isfile(image_path):
    raise FileNotFoundError(f"Image not found: {image_path}")

# Step 4: Load the image into memory
image = ocr.Image.load(image_path)
```

> **Γιατί αυτό το βήμα είναι σημαντικό:** Η σωστή φόρτωση της εικόνας εξασφαλίζει ότι η μηχανή εργάζεται με τα ακριβή δεδομένα pixel που σκοπεύετε να αναλύσετε. Τα κατεστραμμένα αρχεία ή οι λανθασμένες διαδρομές είναι κοινή πηγή απογοήτευσης.

## Βήμα 5: **Εκτέλεση OCR στην Εικόνα** και Εξαγωγή Αποτελεσμάτων

Με τη μηχανή διαμορφωμένη και την εικόνα έτοιμη, η πραγματική αναγνώριση είναι μια κλήση μεθόδου. Το αντικείμενο αποτελέσματος περιέχει το ακατέργαστο κείμενο, τις βαθμολογίες εμπιστοσύνης και ακόμη πληροφορίες διάταξης εάν τις χρειαστείτε αργότερα.

```python
# Step 5: Run OCR
result = engine.recognize(image)

# The recognized text is stored in result.text
recognized_text = result.text
```

Εάν χρειάζεστε να **εξάγετε κείμενο από την εικόνα** γραμμή προς γραμμή, μπορείτε να χωρίσετε με χαρακτήρες νέας γραμμής:

```python
lines = recognized_text.splitlines()
for idx, line in enumerate(lines, start=1):
    print(f"{idx:02d}: {line}")
```

## Βήμα 6: Επαλήθευση του Αποτελέσματος – Βελτιώνει Πραγματικά την **Ακρίβεια OCR**;

Ας εκτυπώσουμε το αποτέλεσμα και να δούμε αν το προσαρμοσμένο λεξικό μας έκανε διαφορά.

```python
print("\n--- OCR Output ---")
print(recognized_text)
```

Η τυπική έξοδος για το δείγμα εικόνας μπορεί να φαίνεται ως εξής:

```
--- OCR Output ---
InvoiceID: 2023‑07‑15
Customer: AsposeOCR Ltd.
Product: β‑cell Therapy Kit
SKU: SKU12345
```

Παρατηρήστε πώς το όνομα της μάρκας, ο ελληνικός χαρακτήρας και ο κωδικός προϊόντος εμφανίζονται ακριβώς όπως τα ορίσαμε. Χωρίς το προσαρμοσμένο λεξικό, η μηχανή θα προσπαθούσε να τα «διορθώσει», συχνά παράγοντας κάτι όπως “Aspose OCR” ή “SKU 1234”.

## Συνηθισμένα Προβλήματα & Πώς να τα Αντιμετωπίσετε

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|-------|----------------|-----|
| **Χαρακτήρες σκουπίδας** | Λάθος γλώσσα ή εικόνα χαμηλής ανάλυσης | Βεβαιωθείτε ότι `engine.language` ταιριάζει με τη γλώσσα προέλευσης και χρησιμοποιήστε σάρωση υψηλής ανάλυσης (300 dpi ή περισσότερο). |
| **Παράβλεψη προσαρμοσμένων λέξεων** | Το λεξικό δεν έχει προσαρτηθεί ή υπάρχει τυπογραφικό λάθος στο όνομα ιδιότητας | Ελέγξτε ξανά `engine.text_processing.custom_dictionary = …`. |
| **Αρχείο δεν βρέθηκε** | Λάθος διαδρομή ή έλλειψη δικαιωμάτων αρχείου | Χρησιμοποιήστε `os.path.abspath()` για να επαληθεύσετε την απόλυτη διαδρομή· εκτελέστε το script με τα κατάλληλα δικαιώματα. |
| **Αργή επεξεργασία** | Μεγάλες εικόνες ή πολλές σελίδες | Προεπεξεργαστείτε την εικόνα (κόψιμο, αλλαγή μεγέθους) ή χρησιμοποιήστε `engine.recognize(image, max_threads=4)` για παράλληλη εκτέλεση. |

## Προχωρώντας Περαιτέρω: Προηγμένες Ρυθμίσεις για **Βελτίωση της Ακρίβειας OCR**

1. **Προεπεξεργασία** – Εφαρμόστε ενίσχυση αντίθεσης ή δυαδικοποίηση με το Pillow πριν περάσετε την εικόνα στο Aspose OCR.  
2. **Πολλαπλές Γλώσσες** – Ορίστε `engine.language = ocr.Language.English | ocr.Language.French` για ενεργοποίηση διγλωσσίας.  
3. **OCR βάσει Περιοχής** – Εάν χρειάζεστε μόνο μια συγκεκριμένη περιοχή (π.χ., έναν πίνακα), κόψτε πρώτα την εικόνα για να μειώσετε το θόρυβο.  
4. **Φιλτράρισμα Εμπιστοσύνης** – `result.confidence` παρέχει βαθμολογία ανά χαρακτήρα· μπορείτε να απορρίψετε αποτελέσματα χαμηλής εμπιστοσύνης προγραμματιστικά.

## Πλήρες Λειτουργικό Script

Παρακάτω βρίσκεται το πλήρες, έτοιμο για αντιγραφή script που ενσωματώνει κάθε βήμα που συζητήσαμε. Αποθηκεύστε το ως `improve_ocr_accuracy.py` και εκτελέστε το από τη γραμμή εντολών.

```python
# improve_ocr_accuracy.py
# Complete example that shows how to improve OCR accuracy with Aspose OCR in Python.

import os
import aspose.ocr as ocr

def main():
    # ---------- Step 1: Initialize engine and set language ----------
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English          # set OCR language

    # ---------- Step 2: Attach custom dictionary ----------
    custom_word_list = [
        "AsposeOCR",
        "InvoiceID",
        "SKU12345",
        "β‑cell"
    ]
    engine.text_processing.custom_dictionary = custom_word_list

    # ---------- Step 3: Load the image ----------
    image_path = "YOUR_DIRECTORY/technical_doc.png"
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    image = ocr.Image.load(image_path)               # load image for OCR

    # ---------- Step 4: Perform OCR ----------
    result = engine.recognize(image)                 # perform OCR on image
    recognized_text = result.text

    # ---------- Step 5: Output the recognized text ----------
    print("\n--- OCR Output ---")
    print(recognized_text)

    # Optional: print line numbers for easier debugging
    print("\n--- Line‑by‑Line View ---")
    for idx, line in enumerate(recognized_text.splitlines(), start=1):
        print(f"{idx:02d}: {line}")

if __name__ == "__main__":
    main()
```

Τρέξτε το:

```bash
python improve_ocr_accuracy.py
```

Θα πρέπει να δείτε την ωραία μορφοποιημένη έξοδο που εμφανίσαμε νωρίτερα.

## Συμπέρασμα

Μόλις καλύψαμε έναν απλό τρόπο για **βελτίωση της ακρίβειας OCR** σε Python μέσω:

1. **Ορισμός της γλώσσας OCR** ώστε να ταιριάζει με το έγγραφό σας.  
2. **Σωστή φόρτωση της εικόνας** ώστε η μηχανή να βλέπει τα σωστά pixel.  
3. **Εκτέλεση OCR στην εικόνα** με μία κλήση μεθόδου.  
4. **Εξαγωγή κειμένου από την εικόνα** και επιβεβαίωση του αποτελέσματος.  
5. **Προσθήκη προσαρμοσμένου λεξικού** για να κλειδώσετε όρους ειδικού τομέα.

Αυτή είναι η πλήρης ροή εργασίας—από ακατέργαστη εικόνα σε καθαρό, αναζητήσιμο κείμενο—συσκευασμένη σε ένα τακτοποιημένο, επαναχρησιμοποιήσιμο script.

Εάν είστε έτοιμοι για την επόμενη πρόκληση, δοκιμάστε πειραματισμό με προεπεξεργασία εικόνας (αντίθεση, διόρθωση κλίσης) ή μεταβείτε σε πολυγλωσσική ρύθμιση χρησιμοποιώντας `ocr.Language.English | ocr.Language.German`. Οι ίδιες αρχές ισχύουν, και θα συνεχίσετε να **βελτιώνετε την ακρίβεια OCR** σε ένα ευρύτερο σύνολο εγγράφων.

Έχετε ερωτήσεις ή κάποιο περίεργο σενάριο; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

![improve OCR accuracy


## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή Κειμένου από Εικόνα – Βελτιστοποίηση OCR με Aspose.OCR για .NET](/ocr/english/net/ocr-optimization/)
- [αναγνώριση κειμένου εικόνας με Aspose OCR για πολλές γλώσσες](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Πώς να Ορίσετε Τιμή Κατωφλίου στην Αναγνώριση Εικόνας OCR](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}