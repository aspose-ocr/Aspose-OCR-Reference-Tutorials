---
category: general
date: 2026-06-06
description: Πώς να προεπεξεργαστείτε εικόνες για OCR χρησιμοποιώντας Python. Μάθετε
  να δυαδικοποιήσετε την εικόνα με τη μέθοδο Otsu, πώς να διορθώσετε την κλίση των
  σαρωμένων εγγράφων και να βελτιώσετε την ακρίβεια του OCR για γερμανικό κείμενο.
draft: false
keywords:
- how to preprocess images for OCR
- binarize image using otsu
- how to deskew scanned documents
- how to improve OCR accuracy
- extract text from german image
language: el
og_description: Πώς να προεπεξεργαστείτε εικόνες για OCR σε Python. Αυτό το σεμινάριο
  δείχνει πώς να δυαδικοποιήσετε την εικόνα χρησιμοποιώντας τη μέθοδο Otsu, πώς να
  διορθώσετε την κλίση των σαρωμένων εγγράφων και πώς να βελτιώσετε την ακρίβεια του
  OCR για γερμανικές εικόνες.
og_title: Πώς να Προεπεξεργαστείτε Εικόνες για OCR – Πλήρης Οδηγός Python
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to preprocess images for OCR using Python. Learn to binarize image
    using Otsu, how to deskew scanned documents, and improve OCR accuracy for German
    text.
  headline: How to Preprocess Images for OCR – Complete Python Guide
  type: TechArticle
- description: How to preprocess images for OCR using Python. Learn to binarize image
    using Otsu, how to deskew scanned documents, and improve OCR accuracy for German
    text.
  name: How to Preprocess Images for OCR – Complete Python Guide
  steps:
  - name: How to Deskew Scanned Documents
    text: The `deskew` call above is the concrete answer to **how to deskew scanned
      documents**. Internally it estimates the dominant text line angle via Hough
      transform and rotates the image back. If your documents are rotated more than
      5°, bump `max_angle` up, but beware of over‑rotation artifacts.
  - name: Binarize Image Using Otsu
    text: The `binarize(method="otsu")` line directly answers the query **binarize
      image using otsu**. Otsu’s algorithm computes a threshold that minimizes intra‑class
      variance, which is perfect for documents with bimodal histograms (dark text
      vs. light background).
  - name: Expected Output
    text: 'Assuming the sample scan contains the sentence “Die schnelle braune Füchsin
      springt über den faulen Hund.” you should see something like:'
  type: HowTo
tags:
- OCR
- image preprocessing
- Python
- German language
title: Πώς να προεπεξεργαστείτε εικόνες για OCR – Πλήρης οδηγός Python
url: /el/python-java/general/how-to-preprocess-images-for-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Προεπεξεργαστείτε Εικόνες για OCR – Πλήρης Οδηγός Python

Έχετε αναρωτηθεί ποτέ **πώς να προεπεξεργαστείτε εικόνες για OCR** ώστε το κείμενο να βγαίνει κρυστάλλινα καθαρό; Δεν είστε οι μόνοι. Τα σαρωμένα έγγραφα—ιδιαίτερα οι θορυβώδεις γερμανικές σελίδες—μπορούν να γίνουν εφιάλτης για οποιαδήποτε μηχανή OCR. Το καλό νέο; Μερικά έξυπνα βήματα προεπεξεργασίας μπορούν να μετατρέψουν μια θολή, σπασμένη σάρωση σε μια καθαρή, μηχανικά αναγνώσιμη εικόνα.

Σε αυτό το tutorial θα περάσουμε από ένα πρακτικό παράδειγμα που δείχνει **πώς να προεπεξεργαστείτε εικόνες για OCR** χρησιμοποιώντας Python. Θα μάθετε να **δυαδικοποιείτε εικόνα με Otsu**, **πώς να διορθώνετε την κλίση σαρωμένων εγγράφων**, και γενικά **πώς να βελτιώσετε την ακρίβεια του OCR** όταν χρειάζεται να **εξάγετε κείμενο από γερμανική εικόνα**. Χωρίς περιττές πληροφορίες, μόνο ένα λειτουργικό script που μπορείτε να αντιγράψετε‑επικολλήσετε σήμερα.

## Τι Θα Χρειαστεί

- **Python 3.9+** (οποιαδήποτε πρόσφατη έκδοση)
- Μια βιβλιοθήκη OCR που εκθέτει μια κλάση `OcrEngine` – για το demo θα υποθέσουμε ένα γενικό πακέτο `ocr`. Εγκαταστήστε το με `pip install ocr-lib`.
- Μια θορυβώδη γερμανική σάρωση (`noisy_german_scan.tif`) που θέλετε να δοκιμάσετε.
- Μια βασική κατανόηση των συναρτήσεων Python (αν έχετε γράψει ποτέ ένα `def`, είστε εντάξει).

> **Pro tip:** Αν χρησιμοποιείτε διαφορετικό OCR SDK (π.χ., Tesseract μέσω `pytesseract`), οι έννοιες παραμένουν ίδιες—απλώς προσαρμόστε τα ονόματα μεθόδων.

## Επισκόπηση της Λύσης

1. **Δημιουργήστε ένα στιγμιότυπο μηχανής OCR.**  
2. **Ορίστε τη γλώσσα αναγνώρισης σε Γερμανικά.**  
3. **Κατασκευάστε μια προσαρμοσμένη αλυσίδα προεπεξεργασίας** που περιλαμβάνει διόρθωση κλίσης, αποθορυβοποίηση, δυαδικοποίηση (Otsu) και τέντωμα αντίθεσης.  
4. **Συνδέστε την αλυσίδα στη μηχανή** ώστε κάθε εικόνα να περνάει αυτόματα από αυτήν.  
5. **Εκτελέστε το OCR** σε μια θορυβώδη γερμανική σάρωση.  
6. **Εκτυπώστε το εξαγόμενο κείμενο** για να επαληθεύσετε το αποτέλεσμα.

Παρακάτω διασπάμε κάθε βήμα, εξηγούμε **γιατί** είναι σημαντικό, και δείχνουμε τον ακριβή κώδικα που χρειάζεστε.

![πώς να προεπεξεργαστείτε εικόνες για OCR παράδειγμα](image.png "πώς να προεπεξεργαστείτε εικόνες για OCR παράδειγμα")

## Βήμα 1: Δημιουργία Στιγμιότυπου Μηχανής OCR

Πρώτα απ' όλα—χωρίς μηχανή, δεν συμβαίνει τίποτα. Το αντικείμενο `OcrEngine` είναι το σημείο εισόδου που συντονίζει όλη τη μεταγενέστερη επεξεργασία.

```python
# Step 1: Initialize the OCR engine
from ocr import OcrEngine, Language

ocr_engine = OcrEngine()
```

*Γιατί είναι σημαντικό:* Η αρχικοποίηση της μηχανής ρυθμίζει εσωτερικούς πόρους (όπως μοντέλα γλώσσας) και σας δίνει ένα καθαρό καμβά για να συνδέσετε μια προσαρμοσμένη αλυσίδα αργότερα.

## Βήμα 2: Ορισμός Γλώσσας Αναγνώρισης σε Γερμανικά

Η ακρίβεια του OCR εξαρτάται σε μεγάλο βαθμό από τη γλώσσα. Αναγγέλλοντας στη μηχανή ότι πρέπει να περιμένει Γερμανικά, ενεργοποιείτε το σωστό σύνολο χαρακτήρων και το μοντέλο γλώσσας.

```python
# Step 2: Tell the engine we’re working with German text
ocr_engine.set_recognition_language(Language.GERMAN)
```

Αν παραλείψετε αυτό το βήμα, η μηχανή μπορεί να προεπιλέξει τα Αγγλικά, παραγνωρίζοντας τα umlauts (ä, ö, ü) και το χαρακτήρα ß—συνηθισμένα προβλήματα σε γερμανικές σάρωσες.

## Βήμα 3: Κατασκευή Προσαρμοσμένης Αλυσίδας Προεπεξεργασίας

Αυτή είναι η καρδιά του **πώς να προεπεξεργαστείτε εικόνες για OCR**. Θα αλυσίδουμε τέσσερις μετασχηματισμούς:

| Μετασχηματισμός | Τι κάνει | Γιατί βοηθά |
|------------------|----------|--------------|
| **Deskew** | Περιστρέφει την εικόνα πίσω σε οριζόντια (μέγιστο 5°) | Οι σάρωσες σπάνια είναι τέλεια ευθυγραμμισμένες· η διόρθωση κλίσης αφαιρεί την κλίση που μπερδεύει τη διαχωριστική λειτουργία χαρακτήρων. |
| **Denoise** | Μειώνει τυχαίες κηλίδες (ισχύς 0.7) | Ο θόρυβος δημιουργεί ψευδείς άκρες που η μηχανή OCR μπορεί να ερμηνεύσει ως χαρακτήρες. |
| **Binarize (Otsu)** | Μετατρέπει σε ασπρόμαυρο χρησιμοποιώντας τη μέθοδο Otsu | Μια καθαρή δυαδική εικόνα δίνει στην μηχανή έντονη αντίθεση μεταξύ προσκηνίου (κειμένου) και φόντου. |
| **Contrast Stretch** | Επεκτείνει το δυναμικό εύρος | Βελτιώνει την αναγνωσιμότητα αδύναμων γραμμών, ειδικά σε παλιά έγγραφα. |

```python
# Step 3: Assemble the preprocessing pipeline
preprocessing_pipeline = (
    ocr_engine.preprocessing()
               .deskew(max_angle=5)          # auto‑deskew up to 5°
               .denoise(strength=0.7)       # medium denoise
               .binarize(method="otsu")      # **binarize image using Otsu**
               .contrast(stretch=True)      # auto contrast stretch
)

# Explanation:
# - `deskew` corrects rotation; 5° is a safe ceiling for most scans.
# - `denoise` with 0.7 balances smoothing without erasing thin characters.
# - `binarize` with method "otsu" automatically selects the optimal threshold.
# - `contrast` stretch brightens faint ink while keeping dark ink dark.
```

### Πώς να Διορθώσετε την Κλίση Σαρωμένων Εγγράφων

Η κλήση `deskew` παραπάνω είναι η συγκεκριμένη απάντηση στο **πώς να διορθώσετε την κλίση σαρωμένων εγγράφων**. Εσωτερικά εκτιμά τη κυρίαρχη γωνία γραμμής κειμένου μέσω μετασχηματισμού Hough και περιστρέφει την εικόνα πίσω. Αν τα έγγραφά σας είναι περιστραμμένα περισσότερο από 5°, αυξήστε το `max_angle`, αλλά προσέξτε τα τεχνητά σφάλματα υπερ‑περιστροφής.

### Δυαδικοποίηση Εικόνας με Otsu

Η γραμμή `binarize(method="otsu")` απαντά άμεσα στο ερώτημα **δυαδικοποιήστε εικόνα με otsu**. Ο αλγόριθμος του Otsu υπολογίζει ένα κατώφλι που ελαχιστοποιεί τη διακύμανση εντός κλάσεων, ιδανικό για έγγραφα με δισκοειδείς ιστογράμματα (σκοτεινό κείμενο vs. ανοιχτό φόντο).

## Βήμα 4: Σύνδεση της Αλυσίδας στη Μηχανή

Τώρα λέμε στη μηχανή OCR να εκτελεί κάθε εισερχόμενη εικόνα μέσω της αλυσίδας που μόλις δημιουργήσαμε.

```python
# Step 4: Register the custom pipeline
ocr_engine.set_preprocessing(preprocessing_pipeline)
```

*Γιατί είναι σημαντικό:* Χωρίς την εγγραφή, η μηχανή θα επεξεργαστεί την ακατέργαστη σάρωση, αγνοώντας όλη την καθαριότητα που μόλις διαμορφώσαμε. Αυτό το βήμα εξασφαλίζει **πώς να βελτιώσετε την ακρίβεια του OCR** εφαρμόζοντας την ίδια προεπεξεργασία σταθερά.

## Βήμα 5: Αναγνώριση Κειμένου από Θορυβώδη Γερμανική Σάρωση

Ώρα να ενώσουμε τα πάντα. Τροφοδοτούμε τη μηχανή με μια θορυβώδη γερμανική εικόνα και αφήνουμε αυτήν να κάνει το σκληρό έργο.

```python
# Step 5: Run OCR on the target file
image_path = "YOUR_DIRECTORY/noisy_german_scan.tif"
recognition_result = ocr_engine.recognize_image(image_path)
```

Αν σας ενδιαφέρει η απόδοση, μπορείτε να μετρήσετε το χρόνο εκτέλεσης:

```python
import time
start = time.time()
result = ocr_engine.recognize_image(image_path)
print(f"OCR took {time.time() - start:.2f}s")
```

## Βήμα 6: Εκτύπωση του Αναγνωρισμένου Κειμένου

Τέλος, εκτυπώνουμε το εξαγόμενο string. Αυτή είναι η άμεση απάντηση στο **εξάγετε κείμενο από γερμανική εικόνα**.

```python
# Step 6: Display the OCR output
print("=== Recognized German Text ===")
print(recognition_result.text)
```

### Αναμενόμενο Αποτέλεσμα

Υποθέτοντας ότι η δείγμα σάρωση περιέχει την πρόταση «Die schnelle braune Füchsin springt über den faulen Hund.» θα πρέπει να δείτε κάτι παρόμοιο με:

```
=== Recognized German Text ===
Die schnelle braune Füchsin springt über den faulen Hund.
```

Αν το αποτέλεσμα εξακολουθεί να περιέχει ακατανόητους χαρακτήρες, σκεφτείτε να ρυθμίσετε τη δύναμη `denoise` ή να αυξήσετε το `max_angle` για τη διόρθωση κλίσης.

## Συχνές Παγίδες & Πώς να τις Αντιμετωπίσετε

- **Λείπει το μοντέλο γλώσσας:** Η παράλειψη του `set_recognition_language(Language.GERMAN)` συχνά οδηγεί σε έλλειψη umlauts. Ελέγξτε ξανά την κλήση.
- **Υπερ‑αποθορυβοποίηση:** Μια ισχύς πάνω από 0.9 μπορεί να σβήσει λεπτές γραμμές, ειδικά σε παλαιά γραμματοσειρά. Κρατήστε το στο 0.5‑0.7 για τις περισσότερες περιπτώσεις.
- **Λανθασμένη μορφή αρχείου:** Κάποιες μηχανές OCR δυσκολεύονται με πολυσελίδες TIFF. Αν έχετε πολυσελιδικό έγγραφο, χωρίστε το σε μονοσέλιδα αρχεία πρώτα.
- **Σειρά αλυσίδας:** Η σειρά που φαίνεται (deskew → denoise → binarize → contrast) είναι σκόπιμη. Η δυαδικοποίηση πριν την αποθορυβοποίηση μπορεί να «κλειδώσει» τον θόρυβο· πάντα αποθορυβώστε πρώτα.

## Επέκταση της Αλυσίδας (Τι Ακολουθεί;)

Τώρα που έχετε μια σταθερή βάση, ίσως θέλετε να:

- **Προσθέσετε ένα μορφολογικό άνοιγμα** για καθαρισμό μικρών σφαιριδίων (`.morph_open(kernel=3)`).
- **Ενσωματώσετε μοντέλο γλώσσας** για διόρθωση μετά την επεξεργασία (`ocr_engine.apply_spellcheck()`).
- **Παραλληλοποιήσετε την επεξεργασία παρτίδας** για μεγάλα σύνολα δεδομένων χρησιμοποιώντας `concurrent.futures`.

Όλα αυτά είναι φυσικές επεκτάσεις που διατηρούν την κεντρική ιδέα του **πώς να προεπεξεργαστείτε εικόνες για OCR** ενώ ενισχύουν περαιτέρω το **πώς να βελτιώσετε την ακρίβεια του OCR**.

## Συμπέρασμα

Καλύψαμε το **πώς να προεπεξεργαστείτε εικόνες για OCR** από την αρχή μέχρι το τέλος: δημιουργία μηχανής, ορισμός γερμανικής γλώσσας, κατασκευή αλυσίδας που **δυαδικοποιεί εικόνα με Otsu**, **πώς να διορθώσετε την κλίση σαρωμένων εγγράφων**, και τελικά **εξάγετε κείμενο από γερμανική εικόνα** με μεγαλύτερη εμπιστοσύνη. Ακολουθώντας τα έξι βήματα παραπάνω θα δείτε μια αισθητή βελτίωση στην ποιότητα αναγνώρισης—χωρίς ατέλειωτες χειροκίνητες διορθώσεις.

Δοκιμάστε το script με τις δικές σας σάρωσες, πειραματιστείτε με τις παραμέτρους, και αφήστε τα αποτελέσματα να μιλήσουν από μόνα τους. Έχετε ερωτήσεις για κάποια συγκεκριμένη ρύθμιση προεπεξεργασίας; Αφήστε ένα σχόλιο και θα εμβαθύνουμε μαζί.

Καλό προγραμματισμό, και να είναι το OCR σας πάντα ακριβές!

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή κειμένου από εικόνα C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Πώς να Ορίσετε Τιμή Κατωφλίου στην Αναγνώριση Εικόνας OCR](/ocr/english/net/ocr-settings/set-threshold-value/)
- [Πώς να Κάνετε OCR σε Εικόνα – Εκτέλεση OCR σε Εικόνα στην Αναγνώριση Εικόνας OCR](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}