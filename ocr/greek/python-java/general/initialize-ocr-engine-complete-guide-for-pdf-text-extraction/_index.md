---
category: general
date: 2026-06-25
description: Αρχικοποιήστε τη μηχανή OCR στην Python για την εξαγωγή κειμένου από
  πολυσελιδικά PDF χρησιμοποιώντας προσαρμοσμένα λεξικά, ρυθμίσεις γλώσσας και στόχευση
  περιοχής.
draft: false
keywords:
- initialize OCR engine
- configure OCR language
- OCR image preprocessing
- OCR custom dictionary
- recognize multi-page PDF
language: el
og_description: Αρχικοποιήστε τη μηχανή OCR σε Python για αξιόπιστη ανάγνωση βιετναμέζικων
  PDF, ρυθμίστε τη γλώσσα, την προεπεξεργασία και το προσαρμοσμένο λεξικό για ακριβή
  αποτελέσματα.
og_title: Αρχικοποίηση Μηχανής OCR – Οδηγός Εξαγωγής PDF Βήμα‑Βήμα
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Initialize OCR engine in Python to extract text from multi‑page PDFs
    using custom dictionaries, language settings, and region targeting.
  headline: Initialize OCR Engine – Complete Guide for PDF Text Extraction
  type: TechArticle
- description: Initialize OCR engine in Python to extract text from multi‑page PDFs
    using custom dictionaries, language settings, and region targeting.
  name: Initialize OCR Engine – Complete Guide for PDF Text Extraction
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed. - An OCR library that exposes an `OcrEngine` class
      (the sample uses a hypothetical `ocr` package; replace with your actual SDK).
      - A sample multi‑page PDF (`sample.pdf`) placed in a known directory. - Basic
      familiarity with Python dictionaries and loops.'
  - name: Pro tip
    text: If you ever need to support multiple languages in the same run, you can
      switch `ocr_engine.language` on the fly before processing each page. Just remember
      to re‑initialize any heavy models if the SDK requires it.
  - name: Expected Output
    text: 'Running the script against a three‑page invoice PDF might produce:'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: Αρχικοποίηση Μηχανής OCR – Πλήρης Οδηγός για την Εξαγωγή Κειμένου από PDF
url: /el/python-java/general/initialize-ocr-engine-complete-guide-for-pdf-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αρχικοποίηση Μηχανής OCR – Πλήρης Οδηγός για Εξαγωγή Κειμένου από PDF

Έχετε χρειαστεί ποτέ να **initialize OCR engine** για μια δέσμη βιετναμέζικων τιμολογίων αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είστε οι μόνοι. Σε πολλά πραγματικά έργα το πρώτο εμπόδιο είναι να κάνετε τη βιβλιοθήκη OCR να «μιλήσει» με τα PDF σας, ειδικά όταν πρέπει να ρυθμίσετε τη γλώσσα, την προεπεξεργασία ή ένα προσαρμοσμένο λεξικό.  

Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα από ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει πώς να **initialize OCR engine**, να ρυθμίσετε τη γλώσσα, να ενεργοποιήσετε έξυπνη προεπεξεργασία εικόνας, να προσθέσετε προσαρμοσμένο λεξικό και, τέλος, να εξάγετε δομημένα δεδομένα από κάθε σελίδα ενός πολυ‑σελίδων PDF. Στο τέλος θα έχετε ένα αυτόνομο script που μπορείτε να ενσωματώσετε στο δικό σας έργο — χωρίς ελλείψεις, χωρίς συντομεύσεις «δείτε τα docs».

## Τι Θα Μάθετε

- Πώς να **initialize OCR engine** με υποστήριξη βιετναμέζικης γλώσσας.  
- Γιατί η **configure OCR language** είναι σημαντική για την ακρίβεια.  
- Χρήση επιλογών **OCR image preprocessing** όπως auto‑deskew και auto‑binarize.  
- Προσθήκη **OCR custom dictionary** για βελτίωση της αναγνώρισης όρων ειδικού τομέα.  
- **Recognize multi‑page PDF** αρχεία και εξαγωγή συγκεκριμένης περιοχής (π.χ. συνολικό ποσό).  
- Μετατροπή των ακατέργαστων αποτελεσμάτων σε καθαρή δομή τύπου JSON για επεξεργασία downstream.

### Προαπαιτούμενα

- Python 3.8+ εγκατεστημένο.  
- Μια βιβλιοθήκη OCR που εκθέτει κλάση `OcrEngine` (το παράδειγμα χρησιμοποιεί ένα υποθετικό πακέτο `ocr`; αντικαταστήστε το με το πραγματικό SDK σας).  
- Ένα δείγμα πολυ‑σελίδων PDF (`sample.pdf`) τοποθετημένο σε γνωστό φάκελο.  
- Βασική εξοικείωση με λεξικά Python και βρόχους.

Αν έχετε όλα αυτά, ας βουτήξουμε.

---

## Βήμα 1: Πώς να Initialize OCR Engine σε Python

Το πρώτο πράγμα που πρέπει να κάνετε είναι **initialize OCR engine**. Σκεφτείτε το ως το άναμμα μιας μηχανής και την καθοδήγηση της για τη γλώσσα που θα τροφοδοτήσετε.

```python
import ocr  # Replace with your actual OCR package

# Create the engine instance
ocr_engine = ocr.OcrEngine()

# Set the language to Vietnamese – this tells the engine which character set to expect
ocr_engine.language = ocr.Language.Vietnamese
```

> **Γιατί είναι σημαντικό:**  
> Οι περισσότερες μηχανές OCR έρχονται με γενικά πακέτα γλώσσας. Ορίζοντας ρητά το `ocr_engine.language` αποφεύγετε την εσφαλμένη εικασία χαρακτήρων, κάτι που μειώνει δραματικά τις λανθασμένες αναγνώσεις για τα διακριτικά που είναι κοινά στα βιετναμέζικα.

### Pro tip
Αν χρειαστεί ποτέ να υποστηρίξετε πολλαπλές γλώσσες στην ίδια εκτέλεση, μπορείτε να αλλάξετε το `ocr_engine.language` εν κινήσει πριν επεξεργαστείτε κάθε σελίδα. Απλώς θυμηθείτε να επανεκκινήσετε τυχόν βαριά μοντέλα αν το SDK το απαιτεί.

---

## Βήμα 2: Ενεργοποίηση Επιλογών OCR Image Preprocessing

Οι ακατέργαστες σαρώσεις σπάνια είναι τέλειες. Σελίδες με κλίση, άνιση φωτισμό ή χαμηλή αντίθεση μπορούν να «μπλοκάρουν» ακόμη και τους καλύτερους αναγνωριστές. Γι' αυτό **configure OCR image preprocessing** αμέσως μετά την αρχικοποίηση.

```python
ocr_engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,      # Auto‑rotate to correct tilt
    auto_binarize=True    # Convert to black‑and‑white for sharper edges
)
```

Αυτές οι δύο σημαίες συνήθως αρκούν για να καθαρίσουν τις περισσότερες σαρωμένες τιμολόγια. Αν τα PDF πηγής σας είναι ήδη υψηλής ποιότητας, μπορείτε να τις απενεργοποιήσετε για να εξοικονομήσετε μερικά χιλιοστά του δευτερολέπτου ανά σελίδα.

---

## Βήμα 3: Προσθήκη OCR Custom Dictionary

Όροι ειδικού τομέα — όπως κωδικοί παραγγελιών, IDs προϊόντων ή νομικές συντομογραφίες — σπάνια εμφανίζονται σε γενικά μοντέλα γλώσσας. Με την προσθήκη **OCR custom dictionary**, δίνετε στη μηχανή ένα «σχεδιάγραμμα».

```python
ocr_engine.custom_dictionary = ["MãĐơnHàng", "KháchHàng", "SốTiền"]
```

> **Τι συμβαίνει στο παρασκήνιο;**  
> Η μηχανή αυξάνει τις βαθμολογίες εμπιστοσύνης για κάθε λέξη που ταιριάζει με μια καταχώρηση σε αυτή τη λίστα, καθιστώντας πολύ λιγότερο πιθανό να διαβαστεί λανθασμένα ως κάτι άλλο.

---

## Βήμα 4: Recognize Multi‑Page PDF – Εξαγωγή Όλου του Κειμένου Μιας Στιγμής

Τώρα που η μηχανή είναι πλήρως ρυθμισμένη, μπορούμε να **recognize multi‑page PDF** αρχεία. Η μέθοδος `recognize_multi_page` επιστρέφει μια λίστα όπου κάθε στοιχείο αντιπροσωπεύει μία σελίδα, ήδη επεξεργασμένη από OCR.

```python
pdf_path = "YOUR_DIRECTORY/sample.pdf"
pages = ocr_engine.recognize_multi_page(pdf_path)
```

Αν εργάζεστε με τεράστια PDF (εκατοντάδες σελίδες), σκεφτείτε την επεξεργασία σε τμήματα για να κρατήσετε τη χρήση μνήμης χαμηλή. Το SDK συνήθως προσφέρει streaming API για αυτή την περίπτωση.

---

## Βήμα 5: Εξαγωγή Συγκεκριμένης Περιοχής από Κάθε Σελίδα

Τα περισσότερα τιμολόγια έχουν πεδίο «Συνολικό Ποσό» που βρίσκεται στην ίδια θέση σε κάθε σελίδα. Αντί να αναλύουμε όλο το κείμενο της σελίδας, μπορούμε να πούμε στη μηχανή να εστιάσει σε ένα ορθογώνιο.

```python
from ocr import Rectangle  # Adjust import based on your SDK

for page_index, page in enumerate(pages, start=1):
    # Define the rectangle (x, y, width, height) that encloses the total amount
    total_region = Rectangle(400, 650, 200, 50)

    # Run OCR only on that region
    region_result = ocr_engine.recognize_region(page.image, total_region)
```

> **Γιατί να στοχεύσουμε μια περιοχή;**  
> Ο περιορισμός του OCR σε μικρότερο χώρο επιταχύνει την επεξεργασία και μειώνει τα ψευδώς θετικά, ειδικά όταν το υπόλοιπο της σελίδας είναι θορυβώδες.

---

## Βήμα 6: Δημιουργία Λεξικού Στυλ JSON για Κάθε Σελίδα

Το ακατέργαστο κείμενο είναι χρήσιμο, αλλά τα downstream συστήματα συνήθως απαιτούν δομημένα δεδομένα. Παρακάτω δημιουργούμε ένα καθαρό λεξικό που περιλαμβάνει τον αριθμό σελίδας, το πλήρες κείμενο της σελίδας, το εξαγόμενο σύνολο και μια λίστα με όλες τις αναγνωρισμένες λέξεις και τις βαθμολογίες εμπιστοσύνης.

```python
    page_output = {
        "page": page_index,
        "full_text": page.text,
        "total_amount": region_result.text,
        "words": [
            {"text": word.text, "conf": word.confidence}
            for word in page.words
        ]
    }

    # Step 7: Output the result for the current page
    print(page_output)
```

Η εκτέλεση του script θα εκτυπώσει μια σειρά λεξικών — ένα ανά σελίδα — που μοιάζουν κάπως έτσι:

```json
{
  "page": 1,
  "full_text": "....",
  "total_amount": "1,250,000 VND",
  "words": [
    {"text": "MãĐơnHàng", "conf": 0.98},
    {"text": "KháchHàng", "conf": 0.96},
    ...
  ]
}
```

Μπορείτε εύκολα να κατευθύνετε την έξοδο σε αρχείο (`> results.jsonl`) για επεξεργασία batch αργότερα.

---

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι το πλήρες script που μπορείτε να αντιγράψετε‑επικολλήσετε και να τρέξετε:

```python
import ocr
from ocr import Rectangle

# -------------------------------------------------
# 1️⃣ Initialize the OCR engine and configure it
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.Vietnamese
ocr_engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=True
)
ocr_engine.custom_dictionary = ["MãĐơnHàng", "KháchHàng", "SốTiền"]

# -------------------------------------------------
# 2️⃣ Recognize all pages of a multi‑page PDF
# -------------------------------------------------
pdf_path = "YOUR_DIRECTORY/sample.pdf"
pages = ocr_engine.recognize_multi_page(pdf_path)

# -------------------------------------------------
# 3️⃣ Iterate through each page, extract region, and build output
# -------------------------------------------------
for page_index, page in enumerate(pages, start=1):
    total_region = Rectangle(400, 650, 200, 50)          # region of interest
    region_result = ocr_engine.recognize_region(page.image, total_region)

    page_output = {
        "page": page_index,
        "full_text": page.text,
        "total_amount": region_result.text,
        "words": [
            {"text": word.text, "conf": word.confidence}
            for word in page.words
        ]
    }

    print(page_output)   # Replace with logging or file write as needed
```

### Αναμενόμενη Έξοδος

Η εκτέλεση του script σε ένα PDF τριών σελίδων μπορεί να παράγει:

```
{'page': 1, 'full_text': '...', 'total_amount': '1,250,000 VND', 'words': [{'text': 'MãĐơnHàng', 'conf': 0.99}, ...]}
{'page': 2, 'full_text': '...', 'total_amount': '1,250,000 VND', 'words': [{'text': 'MãĐơnHàng', 'conf': 0.98}, ...]}
{'page': 3, 'full_text': '...', 'total_amount': '1,250,000 VND', 'words': [{'text': 'MãĐơnHàng', 'conf': 0.97}, ...]}
```

Αισθανθείτε ελεύθεροι να το διοχετεύσετε σε `jq` ή οποιονδήποτε JSON parser για να επαληθεύσετε τη δομή.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

| Ερώτηση | Απάντηση |
|----------|--------|
| **Τι γίνεται αν το PDF είναι προστατευμένο με κωδικό;** | Τα περισσότερα SDK επιτρέπουν να περάσετε ένα όρισμα `password` στη `recognize_multi_page`. Απλώς προσθέστε `password="mySecret"` στην κλήση. |
| **Οι σαρώσεις μου είναι σε γκρι κλίμακα, όχι ασπρόμαυρες.** | Η επιλογή `auto_binarize` θα το διαχειριστεί, αλλά μπορείτε επίσης να μετατρέψετε χειροκίνητα με `Pillow` πριν περάσετε την εικόνα στη `recognize_region`. |
| **Το συνολικό ποσό εμφανίζεται μερικές φορές σε διαφορετικό συντεταγμένο.** | Υπολογίστε το ορθογώνιο δυναμικά (π.χ. μέσω template matching) ή εκτελέστε OCR ολόκληρης της σελίδας και στη συνέχεια ψάξτε το κείμενο με regex όπως `r'\d{1,3}(,\d{3})* VND'`. |
| **Η απόδοση είναι αργή σε PDF 500 σελίδων.** | Ομαδοποιήστε τις σελίδες: επεξεργαστείτε 50 σελίδες, γράψτε τα αποτελέσματα, μετά καθαρίστε τη λίστα `pages` για να ελευθερώσετε μνήμη. Επίσης, απενεργοποιήστε το `auto_deskew` αν οι σαρώσεις είναι ήδη ευθείες. |
| **Πώς να διαχειριστώ άλλες γλώσσες αργότερα;** | Απλώς αλλάξτε `ocr_engine.language = ocr.Language.English` (ή οποιοδήποτε υποστηριζόμενο enum) πριν καλέσετε `recognize_multi_page`. Το υπόλοιπο του pipeline παραμένει το ίδιο. |

---

## Συμβουλές για Παραγωγικές Αναπτύξεις

1. **Διαχείριση σφαλμάτων** – Τυλίξτε τις κλήσεις OCR σε `try/except` blocks· καταγράψτε το index της σελίδας σε περίπτωση αποτυχίας ώστε να μπορείτε να ξαναπροσπαθήσετε.  
2. **Καταγραφή (Logging)** – Χρησιμοποιήστε το module `logging` της Python αντί για `print` για ευέλικτη ρύθμιση επιπέδου verbosity.  
3. **Παράλληλη εκτέλεση** – Αν η βιβλιοθήκη OCR είναι thread‑safe, δημιουργήστε έναν `ThreadPoolExecutor` για ταυτόχρονη επεξεργασία σελίδων.  
4. **Αρχείο ρυθμίσεων** – Αποθηκεύστε τη γλώσσα, το λεξικό και τις συντεταγμένες του ορθογωνίου σε αρχείο JSON/YAML· κάνει το script επαναχρησιμοποιήσιμο σε πολλά έργα.  
5. **Testing** – Δημιουργήστε μικρό σύνολο δοκιμών με γνωστά PDF και ελέγξτε ότι το εξαγόμενο `total_amount` ταιριάζει με τις αναμενόμενες τιμές.  

---

## Συμπέρασμα

Μόλις μάθατε **


## Τι Θα Μάθετε Στη Σύντομη Επόμενη Στιγμή;


Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}