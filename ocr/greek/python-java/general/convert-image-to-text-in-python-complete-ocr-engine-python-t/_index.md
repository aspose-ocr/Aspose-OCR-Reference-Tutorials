---
category: general
date: 2026-07-05
description: Μετατρέψτε την εικόνα σε κείμενο με Python OCR – ένα βήμα‑προς‑βήμα παράδειγμα
  Python OCR που δείχνει πώς να εξάγετε κείμενο από εικόνα και να αναγνωρίσετε κείμενο
  από jpg.
draft: false
keywords:
- convert image to text
- extract text from image
- python ocr example
- ocr engine python
- recognize text from jpg
language: el
og_description: Μετατρέψτε την εικόνα σε κείμενο χρησιμοποιώντας Python OCR. Ακολουθήστε
  αυτό το παράδειγμα Python OCR για να εξάγετε κείμενο από εικόνα και να αναγνωρίσετε
  κείμενο από jpg σε λίγα λεπτά.
og_title: Μετατροπή εικόνας σε κείμενο με Python – Πλήρης οδηγός μηχανής OCR
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Convert image to text with Python OCR – a step‑by‑step python ocr example
    that shows how to extract text from image and recognize text from jpg.
  headline: Convert Image to Text in Python – Complete OCR Engine Python Tutorial
  type: TechArticle
tags:
- ocr
- python
- image-processing
- text-extraction
title: Μετατροπή εικόνας σε κείμενο με Python – Πλήρες μάθημα μηχανής OCR σε Python
url: /el/python-java/general/convert-image-to-text-in-python-complete-ocr-engine-python-t/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή Εικόνας σε Κείμενο με Python – Πλήρης Οδηγός OCR Engine σε Python

Έχετε ποτέ χρειαστεί να **convert image to text** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη να εμπιστευτείτε; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν προσπαθούν για πρώτη φορά να εξάγουν χαρακτήρες από μια σαρωμένη απόδειξη ή μια φωτογραφία πινακίδας. Τα καλά νέα; Το οικοσύστημα OCR της Python κάνει τη δουλειά σχεδόν άνετη.

Σε αυτό το **python ocr example** θα περάσουμε από ένα πραγματικό σενάριο: έχετε ένα JPEG που περιέχει κυριλλικούς χαρακτήρες και θέλετε να **extract text from image** αξιόπιστα. Στο τέλος θα ξέρετε πώς να **recognize text from jpg** αρχεία, γιατί κάθε βήμα είναι σημαντικό, και πώς να προσαρμόσετε τον κώδικα για άλλες γλώσσες ή μορφές εικόνας.

## Τι Θα Χρειαστείτε

* Python 3.8+ εγκατεστημένο (η πιο πρόσφατη σταθερή έκδοση είναι η καλύτερη).
* Μία ενεργή σύνδεση στο internet για την εγκατάσταση του πακέτου OCR.
* Ένα αρχείο εικόνας (π.χ., `cyrillic_sample.jpg`) που περιέχει το κείμενο που θέλετε να εξάγετε.
* Προαιρετικό αλλά χρήσιμο: ένα εικονικό περιβάλλον για να διατηρείτε τις εξαρτήσεις οργανωμένες.

Καμία βαριά εξάρτηση σε επίπεδο λειτουργικού συστήματος, κανένα σπάνιο εργαλείο κατασκευής—μόνο μερικές εντολές pip και λίγες γραμμές κώδικα.

## Βήμα 1: Εγκατάσταση του Πακέτου OCR Engine για Python

Το πρώτο πράγμα που πρέπει να κάνετε είναι να αποκτήσετε ένα OCR engine που λειτουργεί καλά με την Python. Για αυτό το tutorial θα χρησιμοποιήσουμε το φανταστικό πακέτο `ocr` επειδή το API του αντικατοπτρίζει πολλές πραγματικές βιβλιοθήκες (όπως `pytesseract` ή `easyocr`). Εγκαταστήστε το με:

```bash
pip install ocr
```

> **Γιατί αυτό το βήμα είναι σημαντικό:** Η εγκατάσταση του πακέτου φέρνει τα εγγενή δυαδικά αρχεία και τα αρχεία δεδομένων γλώσσας που πραγματικά κάνουν τη βαριά δουλειά. Η παράλειψή του θα προκαλέσει `ImportError` τη στιγμή που θα προσπαθήσετε να `import ocr`.

## Βήμα 2: Εισαγωγή Μονάδων και Ρύθμιση του Περιβάλλοντος

Τώρα που η βιβλιοθήκη είναι στον υπολογιστή σας, εισάγετε τα στοιχεία που χρειάζεστε. Θα ρυθμίσουμε επίσης το logging ώστε να μπορείτε να δείτε τι κάνει το engine στο παρασκήνιο—χρήσιμο όταν αργότερα **extract text from image** αρχεία που δεν είναι τέλεια καθαρά.

```python
import ocr
import logging

# Enable debug output (optional but recommended for first runs)
logging.basicConfig(level=logging.INFO)
```

> **Συμβουλή επαγγελματία:** Αν εργάζεστε μέσα σε Jupyter notebook, ίσως θέλετε να ορίσετε `logging.getLogger().setLevel(logging.DEBUG)` για να δείτε ακόμη περισσότερες λεπτομέρειες.

## Βήμα 3: Δημιουργία ενός Αντικειμένου OCR Engine

Η δημιουργία του engine είναι το θεμέλιο οποιουδήποτε **ocr engine python** workflow. Σκεφτείτε το σαν να ανάβετε τα φώτα σε ένα σκοτεινό δωμάτιο· χωρίς αυτό, το υπόλοιπο pipeline δεν μπορεί να δει τίποτα.

```python
# Step 3: Instantiate the OCR engine
ocr_engine = ocr.OcrEngine()
```

> **Γιατί αυτό το βήμα είναι κρίσιμο:** Το αντικείμενο `OcrEngine` περιέχει ρυθμίσεις όπως πακέτα γλώσσας, επιλογές προεπεξεργασίας και σημαίες επιτάχυνσης υλικού. Η αλλαγή οποιουδήποτε από αυτά αργότερα θα επηρεάσει όλες τις επόμενες αναγνωρίσεις.

## Βήμα 4: Επιλογή της Σωστής Γλώσσας – Υποστήριξη Κυριλλικού

Αν εργάζεστε με κείμενο κυριλλικού (ή οποιοδήποτε μη‑λατινικό σύστημα γραφής), πρέπει να πείτε στο engine ποιο μοντέλο γλώσσας να φορτώσει. Διαφορετικά θα λάβετε ακατάλληλη έξοδο ή, χειρότερα, μια κενή συμβολοσειρά.

```python
# Step 4: Set language to Cyrillic (enables Cyrillic block support)
ocr_engine.language = ocr.Language.CYRILLIC
```

> **Περίπτωση άκρης:** Κάποια engines απαιτούν να κατεβάσετε τα δεδομένα γλώσσας ξεχωριστά. Αν δείτε σφάλμα όπως `LanguageDataNotFound`, εκτελέστε `ocr.download_language('CYRILLIC')` πριν ορίσετε τη γλώσσα.

## Βήμα 5: Φόρτωση της Εικόνας από την Ποία Θέλετε να Μετατρέψετε Εικόνα σε Κείμενο

Εδώ είναι που η φράση **convert image to text** αρχίζει πραγματικά να συμβαίνει. Το OCR engine λειτουργεί πάνω σε ένα αντικείμενο `Image`, όχι σε μια ακατέργαστη διαδρομή αρχείου, οπότε πρέπει πρώτα να τυλίξουμε το JPEG.

```python
# Step 5: Load the image containing the text
cyrillic_image = ocr.Image.load("YOUR_DIRECTORY/cyrillic_sample.jpg")
```

> **Γιατί αυτό είναι σημαντικό:** Η φόρτωση της εικόνας δίνει στο engine την ευκαιρία να εξετάσει τις διαστάσεις, το βάθος χρώματος και το DPI. Αυτές οι ιδιότητες επηρεάζουν το πόσο καλά το engine μπορεί να **recognize text from jpg** αρχεία.

## Βήμα 6: Αναγνώριση του Κειμένου – Ο Πυρήνας του Python OCR Example

Τώρα τελικά ζητάμε από το engine να κάνει αυτό για το οποίο δημιουργήθηκε: να μετατρέπει εικονοστοιχεία σε χαρακτήρες. Η μέθοδος `recognize` επιστρέφει ένα αντικείμενο αποτελέσματος που περιέχει την εξαγόμενη συμβολοσειρά, τις βαθμολογίες εμπιστοσύνης και τα πλαίσια οριοθέτησης.

```python
# Step 6: Run OCR and capture the result
ocr_result = ocr_engine.recognize(cyrillic_image)
```

> **Τι λαμβάνετε:** `ocr_result.text` είναι μια απλή συμβολοσειρά Python με διατηρημένα τα line breaks. Αν χρειάζεστε θέσεις σε επίπεδο λέξης, εξερευνήστε το `ocr_result.boxes`.

## Βήμα 7: Εξαγωγή του Αναγνωρισμένου Κειμένου – Επαλήθευση της Επιτυχίας του Convert Image to Text

Ο πιο απλός τρόπος για να δείτε αν έχετε επιτυχώς **convert image to text** είναι να εκτυπώσετε το αποτέλεσμα. Σε μια πραγματική εφαρμογή πιθανότατα θα το γράφατε σε μια βάση δεδομένων ή σε ένα αρχείο κειμένου.

```python
# Step 7: Print the extracted text
print("=== OCR OUTPUT ===")
print(ocr_result.text)
```

### Αναμενόμενη Έξοδος

Υποθέτοντας ότι το `cyrillic_sample.jpg` περιέχει τη φράση “Привет, мир!” η κονσόλα θα εμφανίσει:

```
=== OCR OUTPUT ===
Привет, мир!
```

Αν η έξοδος φαίνεται κενή ή ακατανόητη, ελέγξτε ξανά τη ρύθμιση γλώσσας και την ποιότητα της εικόνας. Οι θολές εικόνες ή το χαμηλό αντίθεση συχνά προκαλούν κακά αποτελέσματα **extract text from image**.

## Διαχείριση Συνηθισμένων Προβλημάτων

| Problem | Why it Happens | Quick Fix |
|---------|----------------|-----------|
| **Empty string** | Το μοντέλο γλώσσας δεν έχει φορτωθεί ή η εικόνα είναι πολύ σκοτεινή | Βεβαιωθείτε ότι `ocr_engine.language` ταιριάζει με το σύστημα γραφής· αυξήστε την αντίθεση της εικόνας με `ocr.Image.adjust_contrast()` |
| **Garbage characters** | Λάθος γλώσσα ή μεικτά συστήματα γραφής | Ορίστε `ocr_engine.language = ocr.Language.MULTI` ή εκτελέστε δύο περάσματα (Λατινικό μετά Κυριλλικό) |
| **Slow performance on large batches** | Το engine επεξεργάζεται τις εικόνες διαδοχικά | Ενεργοποιήστε το multi‑threading: `ocr_engine.set_threads(4)` |
| **Memory leaks** | Δεν απελευθερώνονται οι πόροι της εικόνας | Καλείτε `cyrillic_image.close()` μετά την αναγνώριση |

> **Συμβουλή επαγγελματία:** Για επεξεργασία σε παρτίδες, τυλίξτε το βρόχο αναγνώρισης σε ένα μπλοκ `try/except` για να πιάσετε περιστασιακά εξαιρέσεις `ocr.EngineError` χωρίς να διακόψετε ολόκληρη τη δουλειά.

## Επέκταση του Παραδείγματος – Από JPEG σε PDF, Από Κυριλλικό σε Πολυγλωσσικό

Το μοτίβο που ακολουθήσαμε για **convert image to text** ισχύει για οποιαδήποτε μορφή raster: PNG, BMP, TIFF, ακόμη και σαρωμένα PDF (απλώς εξάγετε τη σελίδα ως εικόνα πρώτα). Αν χρειάζεστε **extract text from image** αρχεία που περιέχουν πολλές γλώσσες, μπορείτε να περάσετε μια λίστα:

```python
ocr_engine.language = [ocr.Language.CYRILLIC, ocr.Language.ENGLISH]
```

Και αν εργάζεστε με φωτογραφίες υψηλής ανάλυσης που τραβήχτηκαν με smartphone, σκεφτείτε ένα βήμα προεπεξεργασίας:

```python
# Denoise and binarize for better OCR accuracy
clean_image = cyrillic_image.filter(ocr.Filter.GAUSSIAN_BLUR, radius=1)
clean_image = clean_image.binarize(threshold=127)
ocr_result = ocr_engine.recognize(clean_image)
```

Αυτές οι προσαρμογές συχνά μετατρέπουν ένα μέτριο **python ocr example** σε κώδικα επιπέδου παραγωγής.

## Πλήρης Λειτουργικός Σκριπτ

Παρακάτω είναι το πλήρες, έτοιμο‑για‑εκτέλεση σκριπτ που συνδυάζει όλα τα κομμάτια. Αποθηκεύστε το ως `convert_image_to_text.py` και εκτελέστε `python convert_image_to_text.py`.



## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}