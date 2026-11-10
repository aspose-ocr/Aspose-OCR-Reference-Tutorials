---
category: general
date: 2026-01-12
description: Python OCR tutorial που δείχνει πώς να εξάγετε κείμενο πίνακα από μια
  εικόνα. Μάθετε πώς να διαβάζετε πίνακα από εικόνα και να εξάγετε επιλεγμένο κείμενο
  με το Aspose OCR.
draft: false
keywords:
- python ocr tutorial
- extract table text
- read table from image
- extract selected text
- how to extract table
language: el
og_description: Μάθημα Python OCR που σας διδάσκει πώς να εξάγετε κείμενο πίνακα από
  μια εικόνα, να διαβάσετε πίνακα από εικόνα και να εξάγετε επιλεγμένο κείμενο χρησιμοποιώντας
  το Aspose OCR.
og_title: 'Python OCR Tutorial: Εξαγωγή κειμένου πίνακα από εικόνες'
tags:
- OCR
- Python
- AsposeOCR
title: 'Python OCR Tutorial: Εξαγωγή κειμένου πίνακα από εικόνες'
url: /el/python-java/general/python-ocr-tutorial-extract-table-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR Tutorial: Εξαγωγή Κειμένου Πίνακα από Εικόνες

Ποτέ χρειάστηκε ένα **python ocr tutorial** που πραγματικά δείχνει πώς να εξάγετε έναν πίνακα από μια σαρωμένη φόρμα; Δεν είστε οι μόνοι. Οι περισσότερες οδηγίες σταματούν στην γενική εξαγωγή κειμένου, αφήνοντάς σας να μαντεύετε πώς να απομονώσετε το καθαρό πλέγμα δεδομένων που σας ενδιαφέρει.  

Σε αυτόν τον οδηγό θα περάσουμε από ένα πραγματικό σενάριο: ανάγνωση ενός πίνακα από μια εικόνα, εξαγωγή μόνο του κειμένου που χρειάζεστε, και τελικά εκτύπωση των αποτελεσμάτων. Καθ' όλη τη διάρκεια θα προσθέσουμε συμβουλές για **πώς να εξάγετε πίνακα** δεδομένα αξιόπιστα, ώστε να μην χρειάζεται να ξαναεφευρίσετε τον τροχό κάθε φορά.

## Τι Θα Μάθετε

- Πώς να ρυθμίσετε το Aspose OCR για Python.  
- Πώς να ορίσετε μια ορθογώνια περιοχή που περιέχει έναν πίνακα.  
- Τα ακριβή βήματα για **extract table text** και **read table from image**.  
- Συμβουλές για διαχείριση πολλαπλών γλωσσών ή ακανόνιστων διατάξεων πινάκων.  
- Ένα πλήρες, εκτελέσιμο σενάριο που μπορείτε να ενσωματώσετε στο πρότζεκτ σας σήμερα.

**Προαπαιτούμενα**  
- Python 3.8 ή νεότερη.  
- Βασική εξοικείωση με τις έννοιες του OCR (χωρίς ανάγκη για βαθιά εξειδίκευση).  
- Μια εικόνα PNG ή JPEG που περιέχει έναν καθαρό πίνακα (θα την ονομάσουμε `form_with_table.png`).  

Αν έχετε όλα αυτά, ας ξεκινήσουμε—χωρίς περιττές πληροφορίες, μόνο πρακτικός κώδικας.

![python ocr tutorial example of table region](table_region_example.png){alt="παράδειγμα python ocr tutorial που δείχνει την περιοχή του πίνακα"}

## Βήμα 1: Εγκατάσταση και Εισαγωγή του Aspose OCR

Πρώτα απ' όλα: χρειάζεστε τη βιβλιοθήκη Aspose OCR. Το πακέτο είναι στο PyPI, οπότε μια εντολή `pip` αρκεί.

```bash
pip install aspose-ocr
```

Τώρα εισάγετε το module και τυχόν βοηθητικά εργαλεία που θα χρειαστείτε.

```python
# Step 1: Import the Aspose OCR package
import asposeocr as ocr
```

*Pro tip:* Κρατήστε τις εξαρτήσεις σας σε ένα αρχείο `requirements.txt`. Έτσι η αναπαραγωγή του περιβάλλοντος γίνεται παιχνιδάκι.

## Βήμα 2: Αρχικοποίηση του OCR Engine (Python OCR Tutorial Core)

Η δημιουργία του engine είναι η καρδιά κάθε **python ocr tutorial**. Εδώ ορίζουμε επίσης τη προεπιλεγμένη γλώσσα σε English—μπορείτε να την αλλάξετε αργότερα.

```python
# Step 2: Create an OCR engine and set the default language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

Γιατί να ορίσετε τη γλώσσα; Η ακρίβεια του OCR μπορεί να αυξηθεί δραματικά όταν η μηχανή ξέρει ποιοι χαρακτήρες να περιμένει. Αν δουλεύετε με πολυγλωσσικές φόρμες, μπορείτε είτε να ορίσετε μια λίστα γλωσσών είτε να παρακάμψετε ανά περιοχή (δείτε παρακάτω).

## Βήμα 3: Φόρτωση της Εικόνας Σας

Το Aspose OCR λειτουργεί με τις πιο κοινές μορφές εικόνας. Απλώς δείξτε το μονοπάτι του αρχείου και θα έχετε ένα αντικείμενο `Image` έτοιμο για επεξεργασία.

```python
# Step 3: Load the image that contains the form with the table
image_page = ocr.Image.load("YOUR_DIRECTORY/form_with_table.png")
```

*Edge case:* Μεγάλες εικόνες (πάνω από 5 MB) μπορούν να επιβραδύνουν την επεξεργασία. Σκεφτείτε να τις αλλάξετε σε μέγεθος ή να τις συμπιέσετε πριν το OCR αν η απόδοση γίνει πρόβλημα.

## Βήμα 4: Ορισμός της Περιοχής Πίνακα (Read Table from Image)

Τώρα έρχεται το διασκεδαστικό μέρος: να πείτε στη μηχανή *πού* βρίσκεται ο πίνακας. Παρέχετε ένα `OcrRegion` με ένα `Rectangle` (x, y, width, height). Οι συντεταγμένες είναι σε pixel, οπότε ίσως χρειαστεί λίγη δοκιμή.

```python
# Step 4: Define the rectangular area where the table is located
# (x, y, width, height) – adjust these values for your image
table_region = ocr.OcrRegion(
    image_page,
    ocr.Rectangle(120, 340, 800, 450)
)

# Optional: override language for this specific region
table_region.language = ocr.Language.ENGLISH
```

Γιατί να χρησιμοποιήσετε περιοχή; Περιορίζοντας το OCR στην περιοχή του πίνακα **εξάγουμε επιλεγμένο κείμενο** πιο γρήγορα και αποφεύγουμε θόρυβο από ετικέτες ή γραφικά γύρω του. Επίσης βελτιώνει την ακρίβεια επειδή η μηχανή μπορεί να εστιάσει σε μια ομοιόμορφη διάταξη.

## Βήμα 5: Εκτέλεση OCR στην Ορισμένη Περιοχή

Με τη περιοχή ορισμένη, καλούμε το `process_region`. Η μέθοδος επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει το ακατέργαστο κείμενο, βαθμούς εμπιστοσύνης, και ακόμη κουτιά περιορισμού αν τα χρειάζεστε αργότερα.

```python
# Step 5: Run OCR only on the defined region
region_result = ocr_engine.process_region(table_region)
```

Αν χρειάζεται να εξάγετε πολλαπλούς πίνακες, απλώς επαναλάβετε τα Βήματα 4‑5 με διαφορετικά rectangles.

## Βήμα 6: Εξαγωγή του Κειμένου του Πίνακα

Τέλος, εκτυπώστε—ή αποθηκεύστε—την κειμενική αναπαράσταση του πίνακα. Το Aspose OCR επιστρέφει απλό κείμενο με αλλαγές γραμμής που συνήθως ευθυγραμμίζονται με τις σειρές, κάνοντας την επεξεργασία εύκολη.

```python
# Step 6: Output the extracted table text
print("Table text:\n", region_result.text)
```

**Αναμενόμενη έξοδος** (παράδειγμα):

```
Table text:
 Item        Qty   Price
 Apple       10    $1.20
 Banana      5     $0.80
 Orange      8     $1.00
```

Τώρα μπορείτε να δώσετε αυτή τη συμβολοσειρά σε `csv` parser, pandas DataFrames, ή οποιοδήποτε pipeline ανάλυσης δεδομένων.

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι το πλήρες σενάριο που μπορείτε να τρέξετε αμέσως. Αντικαταστήστε το `YOUR_DIRECTORY/form_with_table.png` με το πραγματικό μονοπάτι της εικόνας σας.

```python
# -*- coding: utf-8 -*-
"""
Python OCR Tutorial: Extract Table Text from Images
---------------------------------------------------
A self‑contained example that demonstrates how to read a table from an image
using Aspose OCR for Python.
"""

# Install the library first:
# pip install aspose-ocr

import asposeocr as ocr

def extract_table(image_path, rect):
    """
    Extracts text from a rectangular region that contains a table.

    :param image_path: Path to the PNG/JPEG image.
    :param rect: Tuple (x, y, width, height) defining the table region.
    :return: Plain‑text representation of the table.
    """
    # Initialise OCR engine with English language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Load the image
    img = ocr.Image.load(image_path)

    # Define the region (override language if needed)
    region = ocr.OcrRegion(img, ocr.Rectangle(*rect))
    region.language = ocr.Language.ENGLISH  # optional per‑region override

    # Process only this region
    result = engine.process_region(region)

    return result.text

if __name__ == "__main__":
    # Adjust these coordinates to match your table location
    table_rect = (120, 340, 800, 450)   # x, y, width, height

    # Path to your image file
    img_file = "YOUR_DIRECTORY/form_with_table.png"

    extracted_text = extract_table(img_file, table_rect)
    print("=== Extracted Table Text ===")
    print(extracted_text)
```

Τρέξτε το σενάριο με `python extract_table.py`. Αν όλα ευθυγραμμιστούν, θα δείτε τον πίνακα να εκτυπώνεται στην κονσόλα.

## Συχνές Ερωτήσεις & Διαχείριση Edge‑Case

**Τι γίνεται αν ο πίνακας δεν είναι τέλεια ορθογώνιος;**  
Μποτε να χωρίσετε τον πίνακα σε πολλαπλές επικαλυπτόμενες περιοχές ή να χρησιμοποιήσετε ένα μεγαλύτερο rectangle που καλύπτει όλη την περιοχή και μετά να επεξεργαστείτε το κείμενο (π.χ., διαχωρισμός με αλλαγές γραμμής).

**Μπορώ να εξάγω μόνο συγκεκριμένες στήλες;**  
Αφού έχετε το πλήρες κείμενο του πίνακα, χρησιμοποιήστε το `csv` ή το `pandas` της Python για να αποκόψετε τις στήλες που σας ενδιαφέρουν. Το βήμα OCR επιστρέφει όλα όσα βρίσκονται μέσα στο rectangle.

**Πώςλεύω με πίνακες μη‑Αγγλικών;**  
Ορίστε `ocr_engine.language` (ή `region.language`) στην κατάλληλη enum, όπως `ocr.Language.FRENCH` ή συνδυάστε πολλές γλώσσες με `ocr.Language.ENGLISH | ocr.Language.SPANISH`.

**Υπάρχει τρόπος να λάβω κουτιά περιορισμού για κάθε κελί;**  
Το Aspose OCR μπορεί να επιστρέψει `region_result.words` όπου κάθε λέξη περιλαμβάνει ένα bounding box. Θα χρειαστεί να χαρτογραφήσετε αυτά τα κουτιά σε ένα πλέγμα—χρήσιμο για προχωρημένη ανάλυση διάταξης.

## Συμβουλές για Καλύτερη Ακρίβεια

- **Καθαρίστε την εικόνα**: Δυαδικοποιήστε ή αυξήστε την αντίθεση πριν τη δώσετε στο OCR. Βιβλιοθήκες όπως η Pillow μπορούν να βοηθήσουν.  
- **Αποφύγετε τα artifacts συμπίεσης**: Αποθηκεύετε τις σάρωση ως PNG όποτε είναι δυνατόν.  
- **Προσοχή στο DPI**: 300 dpi είναι το ιδανικό σημείο· χαμηλότερες τιμές μπορεί να προκαλέσουν χαμένα χαρακτήρες.  
- **Δοκιμάστε διαφορετικά μεγέθη rectangle**: Λίγο μεγαλύτερα rectangles συχνά συλλαμβάνουν χαρακτήρες που ανήκουν στον πίνακα αλλά βγαίνουν εκτός μικρότερου πλαισίου.

## Επόμενα Βήματα

Τώρα που έχετε κατακτήσει **πώς να εξάγετε πίνακα** δεδομένα με το Aspose OCR, μπορείτε να εξερευνήσετε:

- Μετατροπή του εξαγόμενου κειμένου σε αρχείο CSV με το module `csv` της Python.  
- Φόρτωση των δεδομένων σε **pandas** DataFrame για ανάλυση.  
- Χρήση OCR για ανάγνωση χειρόγραφων φορμών (απαιτεί διαφορετικό engine ή πρόσθετη εκπαίδευση).  
- Αυτοματοποίηση επεξεργασίας δεκάδων σαρωμένων φορμών με έναν απλό βρόχο `for`.

Κάθε μία από αυτές τις επεκτάσεις βασίζεται στις βασικές έννοιες που καλύφθηκαν σε αυτό το **python ocr tutorial**, οπότε είστε έτοιμοι να κλιμακώσετε το έργο σας.

---

*Καλή προγραμματιστική! Αν αντιμετωπίσετε προβλήματα, αφήστε ένα σχόλιο παρακάτω—θα χαρώ να σας βοηθήσω να βελτιώσετε την εξαγωγή.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}