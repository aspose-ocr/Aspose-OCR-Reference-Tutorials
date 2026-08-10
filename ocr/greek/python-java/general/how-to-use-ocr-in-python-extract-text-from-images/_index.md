---
category: general
date: 2026-06-16
description: Πώς να χρησιμοποιήσετε OCR στην Python για την εξαγωγή κειμένου από αρχεία
  εικόνας όπως PNG. Μάθετε βήμα‑βήμα τη μετατροπή εικόνας σε κείμενο με το Aspose
  OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- read text from png
- convert image to text
- ocr image to text python
language: el
og_description: Πώς να χρησιμοποιήσετε OCR στην Python για την εξαγωγή κειμένου από
  εικόνες. Αυτός ο οδηγός σας καθοδηγεί στη μετατροπή αρχείων PNG σε κείμενο αναζητήσιμο
  με το Aspose OCR.
og_title: Πώς να χρησιμοποιήσετε OCR στην Python – Εξαγωγή κειμένου από εικόνες
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to use OCR in Python to extract text from image files like PNG.
    Learn step‑by‑step conversion of image to text with Aspose OCR.
  headline: How to Use OCR in Python – Extract Text from Images
  type: TechArticle
- description: How to use OCR in Python to extract text from image files like PNG.
    Learn step‑by‑step conversion of image to text with Aspose OCR.
  name: How to Use OCR in Python – Extract Text from Images
  steps:
  - name: Expected Output
    text: '``` Detected language: English Recognized text: Hello, world! This is a
      multi‑language test. こんにちは世界 ```'
  - name: 1. License Not Found
    text: If you see an error like `License file not found`, double‑check the path
      you passed to `set_license`. Using a raw string (`r"..."`) helps avoid escape‑character
      mishaps on Windows.
  - name: 2. Blank Output
    text: 'A blank `ocr_result.text` usually means the image is too noisy or the text
      is too faint. Try increasing the image contrast:'
  - name: 3. Wrong Language Detection
    text: 'If the auto‑detect picks the wrong language, you can force a specific one:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- Aspose
title: Πώς να χρησιμοποιήσετε OCR στην Python – Εξαγωγή κειμένου από εικόνες
url: /el/python-java/general/how-to-use-ocr-in-python-extract-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε OCR σε Python – Εξαγωγή Κειμένου από Εικόνες

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε OCR** σε ένα έργο Python; Δεν είστε ο μόνος. Είτε δημιουργείτε έναν σαρωτή αποδείξεων, έναν αρχειοθέτη εγγράφων, ή απλώς είστε περίεργοι για το πώς να μετατρέψετε ένα στιγμιότυπο οθόνης σε επεξεργάσιμο κείμενο, η δυνατότητα **εξαγωγής κειμένου από εικόνα** είναι ένας καθοριστικός παράγοντας.

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία — από την εγκατάσταση της βιβλιοθήκης Aspose OCR μέχρι την ανάγνωση κειμένου από αρχείο PNG — ώστε να μπορείτε να **μετατρέψετε εικόνα σε κείμενο** με λίγες μόνο γραμμές κώδικα. Στο τέλος, θα ξέρετε ακριβώς πώς να **διαβάσετε κείμενο από PNG** και ακόμη να διαχειριστείτε αυτόματα περιεχόμενο πολλαπλών γλωσσών.

> **Συμβουλή επαγγελματία:** Η αυτόματη ανίχνευση γλώσσας του Aspose OCR σημαίνει ότι δεν χρειάζεται να μαντέψετε τη γλώσσα εκ των προτέρων — ιδανικό για εφαρμογές που ταξιδεύουν παγκοσμίως.

## Τι Θα Χρειαστείτε

- Python 3.8+ (η τελευταία σταθερή έκδοση είναι εντάξει)
- Ένα έγκυρο αρχείο άδειας Aspose OCR (`Aspose.OCR.lic`). Η δωρεάν δοκιμή λειτουργεί για δοκιμές, αλλά μια σωστή άδεια αφαιρεί τους περιορισμούς αξιολόγησης.
- Το πακέτο Aspose OCR εγκατεστημένο μέσω `pip`:

```bash
pip install aspose-ocr
```

- Ένα αρχείο εικόνας που θέλετε να επεξεργαστείτε — ας χρησιμοποιήσουμε το `sample-multi-lang.png` ως παράδειγμα.

Η προετοιμασία αυτών των προαπαιτήσεων θα διατηρήσει τη ροή ομαλή και θα αποφύγετε εκπλήξεις τύπου “module not found” αργότερα.

![Διαδικασία χρήσης OCR σε Python](https://example.com/ocr-workflow.png "Πώς να χρησιμοποιήσετε OCR σε Python – εικονογραφική επεξήγηση βήμα‑βήμα")

*Κείμενο εναλλακτικής εικόνας: Διάγραμμα που δείχνει πώς να χρησιμοποιήσετε OCR σε Python για την εξαγωγή κειμένου από μια εικόνα.*

## Βήμα 1: Εφαρμόστε την Άδεια Aspose OCR (Απαιτείται Μία Φορά ανά Εφαρμογή)

Το πρώτο πράγμα που κάνει οποιοδήποτε σοβαρό έργο OCR είναι να φορτώσει μια άδεια. Χωρίς αυτήν, το Aspose θα εμφανίσει προειδοποίηση και θα περιορίσει τον αριθμό των σελίδων που μπορείτε να επεξεργαστείτε.

```python
# Import the license class
from aspose.ocr import License

# Create a License object and point it to your .lic file
ocr_license = License()
ocr_license.set_license(r"C:\Path\To\Your\Aspose.OCR.lic")
```

> **Γιατί είναι σημαντικό:** Η προφόρτωση της άδειας εξασφαλίζει ότι η μηχανή **ocr image to text python** λειτουργεί με πλήρη ταχύτητα και χωρίς υδατογραφήματα. Σκεφτείτε το ως ξεκλείδωμα των premium λειτουργιών πριν ξεκινήσετε τη μετατροπή.

## Βήμα 2: Δημιουργήστε Μηχανή OCR και Ενεργοποιήστε την Αυτόματη Ανίχνευση Γλώσσας

Τώρα δημιουργούμε την κύρια μηχανή. Η ενεργοποίηση του `language_auto_detect` είναι κρίσιμη όταν δεν γνωρίζετε αν η εικόνα περιέχει Αγγλικά, Ισπανικά, Κινέζικα ή ένα μείγμα γλωσσών.

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine
ocr_engine = OcrEngine()

# Turn on auto‑language detection – it works for over 60 languages
ocr_engine.language_auto_detect = True
```

Αν *γνωρίζετε* τη γλώσσα εκ των προτέρων, μπορείτε να ορίσετε `ocr_engine.language = "English"` (ή οποιονδήποτε υποστηριζόμενο κωδικό ISO) για να επιταχύνετε λίγο τη διαδικασία. Αλλά για ένα γενικό εργαλείο “read text from PNG”, η αυτόματη ανίχνευση είναι η πιο ασφαλής επιλογή.

## Βήμα 3: Φορτώστε την Εικόνα που Θέλετε να Επεξεργαστείτε

Το Aspose OCR λειτουργεί με μια ποικιλία μορφών — PNG, JPEG, BMP, TIFF, ό,τι θέλετε. Ας φορτώσουμε ένα αρχείο PNG που περιέχει πολλαπλές γλώσσες.

```python
from aspose.ocr import Image

# Load the image from disk (replace with your actual path)
ocr_image = Image.load_from_file(r"C:\Path\To\sample-multi-lang.png")

# Assign the image to the engine
ocr_engine.image = ocr_image
```

> **Περίπτωση άκρης:** Αν η εικόνα είναι τεράστια (πάνω από μερικά megabytes), ίσως θελήσετε να τη μειώσετε πρώτα για να βελτιώσετε την απόδοση. Το Aspose παρέχει `ocr_image.resize(width, height)` για αυτόν τον σκοπό.

## Βήμα 4: Εκτελέστε Αναγνώριση OCR

Με όλα συνδεδεμένα, η πραγματική εξαγωγή κειμένου είναι μια κλήση μεθόδου. Το αντικείμενο αποτελέσματος σας δίνει τόσο το αναγνωρισμένο κείμενο όσο και τη γλώσσα που ανιχνεύθηκε.

```python
# Run the recognition process
ocr_result = ocr_engine.recognize()
```

Πίσω από τη σκηνή, το Aspose εκτελεί εξελιγμένα νευρωνικά δίκτυα και αλγόριθμους αντιστοίχισης προτύπων για να μετατρέψει κάθε σύμπλεγμα εικονοστοιχείων σε χαρακτήρες. Η βαριά δουλειά γίνεται όλο σε εγγενή κώδικα, έτσι λαμβάνετε **γρήγορο, ακριβές OCR** ακόμη και σε μέτριο υλικό.

## Βήμα 5: Εμφανίστε τη Ανιχνευμένη Γλώσσα και το Αναγνωρισμένο Κείμενο

Τέλος, ας εκτυπώσουμε ό,τι λάβαμε. Η ιδιότητα `detected_language` σας λέει ποια γλώσσα μαντέψε το Aspose, και το `text` περιέχει τη πλήρη μεταγραφή.

```python
print("Detected language:", ocr_result.detected_language)
print("Recognized text:\n", ocr_result.text)
```

### Αναμενόμενη Έξοδος

```
Detected language: English
Recognized text:
 Hello, world!
 This is a multi‑language test.
 こんにちは世界
```

Αν εκτελέσετε το script σε μια εικόνα που περιλαμβάνει τόσο Αγγλικά όσο και Ιαπωνικά, θα δείτε τη γλώσσα να αλλάζει αυτόματα — χάρη στη λειτουργία αυτόματης ανίχνευσης που ενεργοποιήσαμε νωρίτερα.

## Διαχείριση Κοινών Προβλημάτων

### 1. Άδεια Δεν Βρέθηκε

Αν δείτε σφάλμα όπως `License file not found`, ελέγξτε ξανά τη διαδρομή που περάσατε στο `set_license`. Η χρήση ακατέργαστης συμβολοσειράς (`r"..."`) βοηθά στην αποφυγή προβλημάτων με χαρακτήρες διαφυγής στα Windows.

### 2. Κενή Έξοδος

Ένα κενό `ocr_result.text` συνήθως σημαίνει ότι η εικόνα είναι πολύ θορυβώδης ή το κείμενο είναι πολύ αχνό. Δοκιμάστε να αυξήσετε την αντίθεση της εικόνας:

```python
ocr_image = Image.load_from_file("sample.png")
ocr_image = ocr_image.adjust_contrast(1.5)  # Boost contrast by 50%
ocr_engine.image = ocr_image
```

### 3. Λάθος Ανίχνευση Γλώσσας

Αν η αυτόματη ανίχνευση επιλέξει τη λάθος γλώσσα, μπορείτε να επιβάλετε μια συγκεκριμένη:

```python
ocr_engine.language = "Japanese"  # ISO code or language name
```

## Επέκταση του Παραδείγματος: Επεξεργασία Πολλαπλών Αρχείων PNG σε Παρτίδες

Συχνά θέλετε να **μετατρέψετε εικόνα σε κείμενο** για ολόκληρο φάκελο, όχι μόνο για ένα αρχείο. Εδώ είναι ένας γρήγορος βρόχος που επεξεργάζεται κάθε PNG σε έναν κατάλογο:

```python
import os
from pathlib import Path

input_folder = Path(r"C:\Images")
output_folder = Path(r"C:\OCR_Output")
output_folder.mkdir(exist_ok=True)

for png_path in input_folder.glob("*.png"):
    # Load and assign image
    ocr_image = Image.load_from_file(str(png_path))
    ocr_engine.image = ocr_image

    # Recognize
    result = ocr_engine.recognize()

    # Write result to a .txt file with the same base name
    txt_path = output_folder / (png_path.stem + ".txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(f"Detected language: {result.detected_language}\n")
        f.write(result.text)

    print(f"Processed {png_path.name} → {txt_path.name}")
```

Αυτό το απόσπασμα δείχνει έναν πρακτικό τρόπο για **εξαγωγή κειμένου από εικόνα** αρχείων μαζικά, μια κοινή απαίτηση για αγωγούς ψηφιοποίησης εγγράφων.

## Πλήρες Λειτουργικό Script

Συνδυάζοντας όλα, εδώ είναι ένα μοναδικό αρχείο που μπορείτε να εκτελέσετε από αρχή μέχρι το τέλος:

```python
# ocr_demo.py
import os
from aspose.ocr import License, OcrEngine, Image

# -------------------------------------------------
# 1️⃣ Apply license (replace with your own path)
# -------------------------------------------------
license_path = r"C:\Path\To\Aspose.OCR.lic"
ocr_license = License()
ocr_license.set_license(license_path)

# -------------------------------------------------
# 2️⃣ Create engine and enable auto‑detect
# -------------------------------------------------
ocr_engine = OcrEngine()
ocr_engine.language_auto_detect = True

# -------------------------------------------------
# 3️⃣ Load image (change to your PNG file)
# -------------------------------------------------
image_path = r"C:\Path\To\sample-multi-lang.png"
ocr_image = Image.load_from_file(image_path)
ocr_engine.image = ocr_image

# -------------------------------------------------
# 4️⃣ Recognize and output results
# -------------------------------------------------
ocr_result = ocr_engine.recognize()
print("Detected language:", ocr_result.detected_language)
print("Recognized text:\n", ocr_result.text)
```

Αποθηκεύστε το ως `ocr_demo.py`, εκτελέστε `python ocr_demo.py`, και θα δείτε τη γλώσσα και το κείμενο να εκτυπώνονται στην κονσόλα.

## Συμπέρασμα

Καλύψαμε **πώς να χρησιμοποιήσετε OCR** σε Python από την αρχή μέχρι το τέλος, δείχνοντάς σας πώς να **εξάγετε κείμενο από εικόνα**, **διαβάσετε κείμενο από PNG**, και γενικά **μετατρέψετε εικόνα σε κείμενο** χρησιμοποιώντας τη δυνατή μηχανή του Aspose. Φορτώνοντας μια άδεια, ενεργοποιώντας την αυτόματη ανίχνευση γλώσσας, και τροφοδοτώντας μια εικόνα στο `OcrEngine`, λαμβάνετε καθαρό, αναζητήσιμο κείμενο σε δευτερόλεπτα.

Τι ακολουθεί; Δοκιμάστε να αντικαταστήσετε το Aspose με μια ανοιχτού κώδικα εναλλακτική όπως το Tesseract για να συγκρίνετε την ακρίβεια, πειραματιστείτε με εισόδους PDF, ή ενσωματώστε το βήμα OCR σε ένα Flask API για επεξεργασία εικόνας σε πραγματικό χρόνο. Ο ουρανός είναι το όριο όταν κατακτήσετε τα βασικά του **ocr image to text python**.

Έχετε ερωτήσεις σχετικά με τη διαχείριση δύσκολων γραμματοσειρών, την κλιμάκωση της απόδοσης ή τις άδειες; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετα χαρακτηριστικά του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Βήμα‑Βήμα](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Εξαγωγή Κειμένου από Εικόνα – Βελτιστοποίηση OCR με Aspose.OCR για .NET](/ocr/english/net/ocr-optimization/)
- [Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}