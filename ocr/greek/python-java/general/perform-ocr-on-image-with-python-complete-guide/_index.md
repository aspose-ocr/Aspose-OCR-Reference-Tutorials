---
category: general
date: 2026-07-05
description: Κάντε OCR σε εικόνα με Python γρήγορα. Μάθετε πώς να φορτώνετε εικόνα
  για OCR, να εξάγετε κείμενο από σαρωμένη φόρμα και να χρησιμοποιήσετε το OCR για
  αναγνώριση εικόνας με Python.
draft: false
keywords:
- perform OCR on image
- load image for OCR
- how to use OCR Python
- extract text from scanned form
- OCR recognize image Python
language: el
og_description: Εκτελέστε OCR σε εικόνα με Python. Αυτό το σεμινάριο δείχνει πώς να
  φορτώσετε εικόνα για OCR, να εξάγετε κείμενο από σαρωμένη φόρμα και να χρησιμοποιήσετε
  το OCR για αναγνώριση εικόνας με Python.
og_title: Εκτελέστε OCR σε εικόνα με Python – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Perform OCR on image in Python quickly. Learn how to load image for
    OCR, extract text from scanned form, and use OCR recognize image Python.
  headline: Perform OCR on Image with Python – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Εκτελέστε OCR σε εικόνα με Python – Πλήρης οδηγός
url: /el/python-java/general/perform-ocr-on-image-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε Εικόνα με Python – Πλήρης Οδηγός

Έχετε ποτέ χρειαστεί να **εκτελέσετε OCR σε εικόνα** αρχεία αλλά δεν ήξερες από πού να ξεκινήσεις με την Python; Δεν είστε μόνοι. Είτε ψηφιοποιείτε αποδείξεις, εξάγετε δεδομένα από μια θορυβώδη φόρμα έρευνας, είτε απλώς μετατρέπετε ένα σαρωμένο PDF σε αναζητήσιμο κείμενο, η δυνατότητα εξαγωγής κειμένου από μια σαρωμένη φόρμα αποτελεί καθημερινό πρόβλημα για πολλούς προγραμματιστές.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα **πώς να χρησιμοποιήσετε βιβλιοθήκες OCR Python**, από τη φόρτωση της εικόνας μέχρι την εμφάνιση ενός φιλτραρισμένου αποτελέσματος. Στο τέλος θα ξέρετε ακριβώς πώς να **φορτώσετε εικόνα για OCR**, να ρυθμίσετε τα όρια εμπιστοσύνης και να καλέσετε τη μέθοδο **OCR recognize image Python** που κάνει το πραγματικό βάρος.

> **Τι θα λάβετε:** ένα έτοιμο‑για‑εκτέλεση script που φορτώνει μια εικόνα, εκτελεί OCR και εκτυπώνει καθαρό, φιλτραρισμένο κείμενο με βάση την εμπιστοσύνη. Χωρίς ασαφείς αναφορές, χωρίς ελλιπείς εισαγωγές—απλώς μια πλήρης, αντιγραφή‑επικόλληση λύση.

---

## Τι Θα Χρειαστείτε

Πριν βουτήξουμε, βεβαιωθείτε ότι έχετε:

* Python 3.9 ή νεότερη εγκατεστημένη (ο κώδικας λειτουργεί επίσης σε 3.10+).  
* Ένα πακέτο OCR που ακολουθεί το API `ocr` που χρησιμοποιείται παρακάτω – για παράδειγμα, η φανταστική βιβλιοθήκη `simple-ocr` ή οποιοδήποτε wrapper που εκθέτει `OcrEngine`, `Language`, και `Image`.  
* Ένα αρχείο εικόνας (`.png`, `.jpg`, κλπ.) που περιέχει το κείμενο που θέλετε να εξάγετε.  
* Ένα τερματικό ή IDE όπου μπορείτε να εκτελέσετε ένα μόνο script Python.

Αν τα έχετε ήδη, υπέροχα—ας ξεκινήσουμε.

---

## Εκτέλεση OCR σε Εικόνα – Ρύθμιση του Μηχανήματος

Το πρώτο πράγμα που πρέπει να κάνετε είναι να δημιουργήσετε μια παρουσία του OCR engine. Σκεφτείτε τον engine ως τον εγκέφαλο πίσω από τη λειτουργία· γνωρίζει πώς να ερμηνεύει τα pixel και να τα μετατρέπει σε χαρακτήρες.

```python
# Import the OCR library – replace `ocr` with your actual package name
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Γιατί είναι σημαντικό:* χωρίς engine δεν υπάρχει τίποτα προς επεξεργασία. Το αντικείμενο `OcrEngine` κρατά όλες τις ρυθμίσεις που θα προσαρμόσετε αργότερα, όπως η γλώσσα και το όριο εμπιστοσύνης.

---

## Φόρτωση Εικόνας για OCR – Προετοιμασία της Σαρωμένης Φόρμας

Τώρα που υπάρχει ο engine, πρέπει να **φορτώσουμε εικόνα για OCR**. Η μέθοδος `Image.load()` της βιβλιοθήκης διαβάζει το αρχείο από το δίσκο και το μετατρέπει σε εσωτερική αναπαράσταση που μπορεί να καταλάβει ο engine.

```python
# Step 2: Load the image you want to process
# Replace the path with the actual location of your noisy form
image_path = "YOUR_DIRECTORY/noisy_form.png"
image = ocr.Image.load(image_path)
```

> **Συμβουλή:** Αν εργάζεστε με PDFs, μετατρέψτε πρώτα κάθε σελίδα σε εικόνα (π.χ., χρησιμοποιώντας `pdf2image`). Ο OCR engine δέχεται μόνο raster εικόνες.

---

## Πώς να Χρησιμοποιήσετε OCR Python – Ρύθμιση Γλώσσας και Εμπιστοσύνης

Οι περισσότεροι OCR engines υποστηρίζουν πολλαπλές γλώσσες και σας επιτρέπουν να φιλτράρετε χαρακτήρες χαμηλής εμπιστοσύνης. Η ρύθμιση αυτών των παραμέτρων νωρίς εξασφαλίζει ότι θα λάβετε μόνο αξιόπιστο κείμενο.

```python
# Step 3: Choose language and set a confidence threshold
engine.language = ocr.Language.ENGLISH          # you can switch to FR, DE, etc.
engine.min_confidence = 85                     # accept only characters >85 % confidence
```

*Γιατί 85 %?* Στην πράξη, ένα όριο γύρω στο 80‑90 % εξαλείφει τα περισσότερα ακατανόητα ενώ διατηρεί το καλό υλικό. Μπορείτε να το προσαρμόσετε ανάλογα με την ποιότητα των σαρώσεων σας.

---

## Εξαγωγή Κειμένου από Σαρωμένη Φόρμα – Αναγνώριση της Εικόνας

Με τον engine έτοιμο και την εικόνα φορτωμένη, ήρθε η ώρα να **εκτελέσετε OCR σε εικόνα**. Η μέθοδος `recognize()` επιστρέφει ένα αντικείμενο αποτελέσματος που περιέχει το εξαγόμενο κείμενο και, προαιρετικά, δεδομένα περιοριστικού πλαισίου.

```python
# Step 4: Perform OCR recognition on the image
result = engine.recognize(image)
```

Αν η βιβλιοθήκη το υποστηρίζει, το `result` μπορεί επίσης να εκθέτει `result.confidences` (μια λίστα με βαθμολογίες εμπιστοσύνης ανά χαρακτήρα) και `result.words` (δομημένα αντικείμενα λέξεων). Για αυτόν τον οδηγό θα εστιάσουμε στην έξοδο απλού κειμένου.

---

## OCR Recognize Image Python – Εμφάνιση Φιλτραρισμένων Αποτελεσμάτων

Τέλος, ας εκτυπώσουμε το φιλτραρισμένο κείμενο. Τα σύμβολα χαμηλής εμπιστοσύνης εμφανίζονται ως ερωτηματικό (`?`) επειδή ορίσαμε `min_confidence` στο 85 %.

```python
# Step 5: Show the filtered text
print("Filtered text:")
print(result.text)
```

### Αναμενόμενο Αποτέλεσμα

```
Filtered text:
Name: John Doe
Date: 2023‑04‑15
Amount: $123.45
Signature: ?
```

Παρατηρήστε πώς η μη αναγνώσιμη υπογραφή μετατράπηκε σε `?`. Αυτό είναι ακριβώς το αποτέλεσμα του φίλτρου εμπιστοσύνης—διατηρεί το αποτέλεσμα καθαρό για επεξεργασία σε επόμενα στάδια.

---

## Συνηθισμένα Προβλήματα και Επαγγελματικές Συμβουλές

| Πρόβλημα | Γιατί Συμβαίνει | Γρήγορη Λύση |
|----------|----------------|--------------|
| **Κενό αποτέλεσμα** | Η εικόνα είναι πολύ σκοτεινή ή χαμηλής ανάλυσης. | Προεπεξεργασία με OpenCV: αυξήστε την αντίθεση, αλλάξτε το μέγεθος σε ≥300 dpi. |
| **Χαλασμένοι χαρακτήρες** | Επιλέχθηκε λανθασμένη γλώσσα. | Ορίστε `engine.language` ώστε να ταιριάζει με το έγγραφο (π.χ., `ocr.Language.FRENCH`). |
| **Πάρα πολλά σύμβολα `?`** | Το όριο εμπιστοσύνης είναι πολύ υψηλό. | Μειώστε το `engine.min_confidence` στο 70‑80 % για θορυβώδεις σαρώσεις. |
| **Σφάλματα Unicode** | Η έξοδος περιέχει μη‑ASCII χαρακτήρες αλλά η κωδικοποίηση του τερματικού είναι λανθασμένη. | Εκτελέστε `python -X utf8` ή ορίστε `PYTHONIOENCODING=utf-8`. |

**Συμβουλή:** Αν χρειάζεται να εξάγετε πίνακες, εκτελέστε δεύτερο πέρασμα με έναν OCR engine που λαμβάνει υπόψη τη διάταξη (όπως το `--psm 6` του Tesseract) μετά το φιλτράρισμα του ακατέργαστου κειμένου.

---

## Πλήρες Script – Έτοιμο για Εκτέλεση

Παρακάτω βρίσκεται το πλήρες, αυτόνομο script που ενσωματώνει κάθε βήμα που συζητήθηκε. Αποθηκεύστε το ως `perform_ocr.py`, προσαρμόστε τη διαδρομή της εικόνας και εκτελέστε `python perform_ocr.py`.

```python
# perform_ocr.py
# -------------------------------------------------
# Complete Python script to perform OCR on image,
# load image for OCR, configure engine, and display
# filtered results. Works with any OCR library that
# follows the simple `ocr` API shown here.
# -------------------------------------------------

import ocr  # Replace with your actual OCR package name

def main():
    # 1️⃣ Create the engine
    engine = ocr.OcrEngine()

    # 2️⃣ Configure language and confidence
    engine.language = ocr.Language.ENGLISH
    engine.min_confidence = 85  # Only keep chars >85 % confidence

    # 3️⃣ Load the image (adjust the path)
    image_path = "YOUR_DIRECTORY/noisy_form.png"
    image = ocr.Image.load(image_path)

    # 4️⃣ Recognize the text
    result = engine.recognize(image)

    # 5️⃣ Print the filtered output
    print("Filtered text:")
    print(result.text)

if __name__ == "__main__":
    main()
```

Τρέξτε το, και θα δείτε το φιλτραρισμένο κείμενο να εκτυπώνεται στην κονσόλα—ακριβώς αυτό που υπόσχεται το βήμα **extract text from scanned form**.

---

## Τι Ακολουθεί;

Τώρα που ξέρετε πώς να **εκτελέσετε OCR σε εικόνα** και **εξάγετε κείμενο από σαρωμένη φόρμα**, ίσως θέλετε να εξερευνήσετε:

* **Batch processing** – επανάληψη σε έναν φάκελο εικόνων για δημιουργία CSV με τα αποτελέσματα.  
* **Post‑processing** – χρησιμοποιήστε regex ή spaCy για εξαγωγή πεδίων όπως ημερομηνίες, ποσά ή IDs.  
* **Integrations** – ενσωματώστε την έξοδο OCR σε βάση δεδομένων, Google Sheets ή REST API.  

Όλες αυτές οι ιδέες περιλαμβάνουν φυσικά τις ίδιες βασικές λειτουργίες που καλύψαμε: φόρτωση της εικόνας, ρύθμιση του engine και κλήση της μεθόδου **OCR recognize image Python**.

---

## Συμπέρασμα

Διασχίσαμε ένα πλήρες, έτοιμο για παραγωγή παράδειγμα για το πώς να **εκτελέσετε OCR σε εικόνα** χρησιμοποιώντας Python. Από το **φόρτωση εικόνας για OCR** μέχρι τη ρύθμιση γλώσσας, τον καθορισμό ορίου εμπιστοσύνης και τελικά την **εξαγωγή κειμένου από σαρωμένη φόρμα**, κάθε βήμα παρουσιάστηκε με σαφή κώδικα και εξηγήσεις. Τώρα έχετε μια σταθερή βάση για να αντιμετωπίσετε πιο σύνθετα σενάρια—είτε πρόκειται για batch εργασίες, υποστήριξη πολλαπλών γλωσσών ή εξαγωγή πινάκων.

Δοκιμάστε το script, προσαρμόστε τα όρια, και παρακολουθήστε τα έγγραφά σας να γίνονται αναζητήσιμα σε λίγα λεπτά. Έχετε ερωτήσεις ή μια δύσκολη φόρμα που δεν συνεργάζεται; Αφήστε ένα σχόλιο παρακάτω και ας το αντιμετωπίσουμε μαζί. Καλή προγραμματιστική!

![Παράδειγμα εκτέλεσης OCR σε εικόνα](example.png "Εκτέλεση OCR σε εικόνα")

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε σε πρόσθετα χαρακτηριστικά API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Βήμα‑βήμα](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Πώς να Χρησιμοποιήσετε AspOCR: Προεπεξεργασία Φίλτρων OCR Εικόνας για .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}