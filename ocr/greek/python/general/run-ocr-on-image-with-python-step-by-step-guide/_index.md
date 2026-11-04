---
category: general
date: 2026-08-12
description: Εκτελέστε OCR σε εικόνα χρησιμοποιώντας Python και Aspose AI για να εξάγετε
  κείμενο από την εικόνα και να βελτιώσετε την ακρίβεια του OCR με έναν επεξεργαστή
  ορθογραφικού ελέγχου μετά την επεξεργασία.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- run OCR on image
- extract text from image
- OCR text correction
- improve OCR accuracy
- load image for OCR
language: el
lastmod: 2026-08-12
og_description: Εκτελέστε OCR σε εικόνα με Python και εξάγετε αμέσως το κείμενο από
  την εικόνα, βελτιώνοντας ταυτόχρονα την ακρίβεια του OCR χρησιμοποιώντας την επεξεργασία
  μετά‑επεξεργασίας AI της Aspose.
og_image_alt: Diagram showing the run OCR on image workflow in Python
og_title: Εκτελέστε OCR σε εικόνα με Python – πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: Run OCR on image using Python and Aspose AI to extract text from image
    and improve OCR accuracy with a spell‑checking post‑processor.
  headline: Run OCR on image with Python – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- Image Processing
title: Εκτελέστε OCR σε εικόνα με Python – βήμα‑βήμα οδηγός
url: /el/python/general/run-ocr-on-image-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε εικόνα με Python – οδηγός βήμα‑βήμα

Αν χρειάζεστε **εκτέλεση OCR σε εικόνα** με Python, αυτός ο οδηγός σας καθοδηγεί σε όλη τη ροή εργασίας. Θα μάθετε πώς να **εξάγετε κείμενο από εικόνα**, να εφαρμόσετε **διόρθωση κειμένου OCR** και να **βελτιώσετε την ακρίβεια του OCR** με λίγες μόνο γραμμές κώδικα.

Η επεξεργασία σαρωμένων εγγράφων, αποδείξεων ή στιγμιότυπων συχνά παράγει θορυβώδες κείμενο. Προσθέτοντας έναν ελεγκτή ορθογραφίας ως post‑processor μπορείτε να μετατρέψετε το ακατέργαστο αποτέλεσμα του OCR σε καθαρό, αναζητήσιμο περιεχόμενο χωρίς να χρειάζεται να μεταβείτε σε ξεχωριστό εργαλείο. Αυτό το tutorial καλύπτει τα πάντα—από τη φόρτωση της εικόνας μέχρι την εμφάνιση του διορθωμένου αποτελέσματος.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* Python 3.9 ή νεότερη έκδοση εγκατεστημένη.
* Πρόσβαση στα πακέτα Aspose.OCR και Aspose.AI για Python (ή στα αντίστοιχα ανοιχτού κώδικα wrappers).
* Ένα δείγμα εικόνας (π.χ. `sample.png`) τοποθετημένο σε γνωστό φάκελο.
* Βασική εξοικείωση με συναρτήσεις Python και αντικειμενοστραφή κώδικα.

Μπορείτε να εγκαταστήσετε τις απαιτούμενες βιβλιοθήκες με pip:

```bash
pip install aspose-ocr aspose-ai
```

> **Συμβουλή:** Χρησιμοποιήστε ένα εικονικό περιβάλλον (`python -m venv .venv`) για να διατηρήσετε τις εξαρτήσεις απομονωμένες.

## Βήμα 1: Εκτέλεση OCR σε εικόνα – δημιουργία του αντικειμένου μηχανής

Το πρώτο βήμα είναι η δημιουργία ενός αντικειμένου `OcrEngine`. Αυτό το αντικείμενο περιλαμβάνει τη διαμόρφωση της μηχανής OCR και παρέχει μεθόδους για τη διαχείριση και την αναγνώριση εικόνων.

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine with default settings
ocr_engine = OcrEngine()
```

Δημιουργώντας τη μηχανή μία φορά και επαναχρησιμοποιώντας την για πολλές εικόνες μειώνετε το χρόνο εκκίνησης και εξασφαλίζετε συνεπείς ρυθμίσεις καθ' όλη τη διάρκεια της συνεδρίας.

## Βήμα 2: Φόρτωση εικόνας για OCR

Πριν μπορέσει να γίνει η αναγνώριση, η μηχανή πρέπει να γνωρίζει ποια εικόνα θα αναλύσει. Η μέθοδος `load_image` δέχεται διαδρομή αρχείου ή δυαδική ροή.

```python
# Provide the full path to your image file
image_path = "YOUR_DIRECTORY/sample.png"
ocr_engine.load_image(image_path)
```

> **Γιατί είναι σημαντικό:** Η σωστή φόρτωση της εικόνας αποτελεί τη βάση για ακριβές OCR. Η χρήση εικόνας υψηλής ανάλυσης (300 dpi ή περισσότερο) συνήθως **βελτιώνει την ακρίβεια του OCR** επειδή η μηχανή μπορεί να διακρίνει τους χαρακτήρες πιο καθαρά.

## Βήμα 3: Εξαγωγή κειμένου από εικόνα – βασική αναγνώριση

Με την εικόνα φορτωμένη, μπορείτε να καλέσετε `recognize()` για να λάβετε ένα αντικείμενο αποτελέσματος. Το αποτέλεσμα περιέχει το ακατέργαστο κείμενο, βαθμολογίες εμπιστοσύνης και, προαιρετικά, πλαίσια οριοθέτησης για κάθε λέξη.

```python
# Run the OCR process
plain_result = ocr_engine.recognize()   # returns a Result object

# The raw OCR output is accessible via the .text attribute
print("Raw OCR output:")
print(plain_result.text)
```

Σε αυτό το σημείο έχετε εκτελέσει επιτυχώς **OCR σε εικόνα** και έχετε εξάγει τους ακατέργαστους χαρακτήρες. Ωστόσο, το κείμενο μπορεί να περιέχει ορθογραφικά λάθη, ειδικά σε χαμηλής ποιότητας σκαναρίσματα.

## Βήμα 4: Διόρθωση κειμένου OCR – προσθήκη ελεγκτή ορθογραφίας post‑processing

Το Aspose AI παρέχει ένα ευέλικτο pipeline post‑processing. Συνδέοντας έναν προσαρμοσμένο ελεγκτή ορθογραφίας μπορείτε να διορθώσετε τυπικά σφάλματα OCR (π.χ. “l” vs. “1”, “O” vs. “0”).

```python
from aspose.ai import AsposeAI
from my_spellchecker import MySpellChecker   # your own implementation

# Initialize the AI engine and set the post‑processor
ai_engine = AsposeAI()
ai_engine.set_post_processor(MySpellChecker())

# Run the post‑processor on the plain OCR result
corrected_result = ai_engine.run_postprocessor(plain_result)
```

**Πώς λειτουργεί ο ελεγκτής ορθογραφίας:** Το `MySpellChecker` πρέπει να υλοποιεί μια μέθοδο `process(text: str) -> str`. Μέσα σε αυτήν, μπορείτε να χρησιμοποιήσετε βιβλιοθήκες όπως `pyspellchecker` ή `symspellpy` για να αντικαταστήσετε ακατάλληλες ακολουθίες λέξεων με εναλλακτικές που έχουν επαληθευτεί από λεξικό.

```python
# Example implementation (very simple)
from spellchecker import SpellChecker

class MySpellChecker:
    def __init__(self):
        self.spell = SpellChecker()

    def process(self, text: str) -> str:
        corrected = []
        for word in text.split():
            corrected.append(self.spell.correction(word))
        return " ".join(corrected)
```

## Βήμα 5: Εμφάνιση αρχικού και διορθωμένου κειμένου OCR

Τέλος, συγκρίνετε τα ακατέργαστα και τα διορθωμένα αποτελέσματα. Αυτό σας βοηθά να επαληθεύσετε ότι η **διόρθωση κειμένου OCR** πραγματικά **βελτίωσε την ακρίβεια του OCR** για την περίπτωσή σας.

```python
print("\nOriginal :", plain_result.text)
print("Corrected:", corrected_result.text)
```

### Αναμενόμενο αποτέλεσμα

```
Original : Th1s is a s4mpl3 rec3pt with som3 err0rs.
Corrected: This is a simple receipt with some errors.
```

Η διορθωμένη γραμμή δείχνει ότι ο ελεγκτής ορθογραφίας αντικατέστησε κοινές λανθασμένες αναγνώσεις OCR (`Th1s` → `This`, `s4mpl3` → `simple`, `rec3pt` → `receipt`, `som3` → `some`, `err0rs` → `errors`).

## Βήμα 6: Βελτίωση ακρίβειας OCR – λίστα ελέγχου βέλτιστων πρακτικών

Ακόμη και με post‑processing, μπορείτε να αυξήσετε την αρχική ποιότητα της μηχανής OCR:

| Στοιχείο λίστας ελέγχου | Γιατί βοηθά |
|--------------------------|--------------|
| **Χρήση εικόνων υψηλής ανάλυσης (≥300 dpi)** | Περισσότερα δεδομένα pixel μειώνουν την ασάφεια χαρακτήρων. |
| **Μετατροπή έγχρωμων εικόνων σε γκρι κλίμακα** | Απομακρύνει τον θόρυβο χρωμάτων που μπορεί να μπερδέψει τη μηχανή. |
| **Εφαρμογή διόρθωσης κλίσης εικόνας** | Ευθυγραμμίζει κεκλιμένο κείμενο, αποτρέποντας σφάλματα διακοπής γραμμής. |
| **Ορισμός γλώσσας/τοπικής ρύθμισης ρητά** | Κατευθύνει τον αναγνωριστή προς το σωστό σύνολο χαρακτήρων. |
| **Ενεργοποίηση μοντέλου γλώσσας** (αν η βιβλιοθήκη το υποστηρίζει) | Παρέχει προβλέψεις με βάση το συμφραζόμενο, βελτιώνοντας περαιτέρω **την ακρίβεια του OCR**. |

Μπορείτε να υλοποιήσετε αυτά τα βήματα προεπεξεργασίας με Pillow ή OpenCV πριν περάσετε την εικόνα στο `ocr_engine`.

```python
from PIL import Image, ImageOps
import cv2
import numpy as np

def preprocess_image(path: str) -> str:
    # Load with Pillow, convert to grayscale, and increase contrast
    img = Image.open(path).convert("L")
    img = ImageOps.autocontrast(img, cutoff=2)

    # Save a temporary preprocessed file
    temp_path = "temp_preprocessed.png"
    img.save(temp_path)
    return temp_path

# Use the preprocessor
preprocessed_path = preprocess_image(image_path)
ocr_engine.load_image(preprocessed_path)
```

## Πλήρες εκτελέσιμο σενάριο

Συνδυάζοντας όλα τα παραπάνω, το παρακάτω σενάριο είναι έτοιμο για αντιγραφή‑επικόλληση σε αρχείο με όνομα `run_ocr.py` και εκτέλεση.

```python
# run_ocr.py
from aspose.ocr import OcrEngine
from aspose.ai import AsposeAI
from my_spellchecker import MySpellChecker
from PIL import Image, ImageOps

def preprocess_image(path: str) -> str:
    img = Image.open(path).convert("L")
    img = ImageOps.autocontrast(img, cutoff=2)
    temp_path = "temp_preprocessed.png"
    img.save(temp_path)
    return temp_path

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load and preprocess the image
    raw_path = "YOUR_DIRECTORY/sample.png"
    processed_path = preprocess_image(raw_path)
    ocr_engine.load_image(processed_path)

    # 3️⃣ Perform basic OCR
    plain_result = ocr_engine.recognize()

    # 4️⃣ Run OCR text correction
    ai_engine = AsposeAI()
    ai_engine.set_post_processor(MySpellChecker())
    corrected_result = ai_engine.run_postprocessor(plain_result)

    # 5️⃣ Show both results
    print("\nOriginal :", plain_result.text)
    print("Corrected:", corrected_result.text)

if __name__ == "__main__":
    main()
```

Η εκτέλεση του σεναρίου εκτυπώνει το αρχικό και το διορθωμένο κείμενο, επιβεβαιώνοντας ότι έχετε επιτυχώς **εκτελέσει OCR σε εικόνα**, **εξάγει κείμενο από εικόνα** και **βελτιώσει την ακρίβεια του OCR** μέσω **διόρθωσης κειμένου OCR**.

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **εκτελείτε OCR σε εικόνα** με Python, να εξάγετε το ακατέργαστο κείμενο και να εφαρμόζετε έναν ελεγκτή ορθογραφίας post‑processing για πιο καθαρά αποτελέσματα. Ακολουθώντας τη λίστα ελέγχου για **βελτίωση ακρίβειας OCR**, μπορείτε να προσαρμόσετε αυτή τη ροή εργασίας σε αποδείξεις, τιμολόγια, ταυτότητες ή οποιοδήποτε σαρωμένο έγγραφο.

### Τι θα ακολουθήσει;

* Εξερευνήστε **λεξικά ειδικών γλωσσών** για πολυγλωσσικό OCR.
* Ενσωματώστε τη ροή εργασίας με μια βάση δεδομένων ή έναν δείκτη αναζήτησης (π.χ. Elasticsearch) για να κάνετε το εξαγόμενο κείμενο αναζητήσιμο.
* Αντικαταστήστε τον απλό ελεγκτή ορθογραφίας με ένα νευρωνικό μοντέλο γλώσσας (π.χ. διόρθωση βασισμένη σε GPT) για ακόμη μεγαλύτερη ακρίβεια.

Νιώστε ελεύθεροι να πειραματιστείτε με διαφορετικές τεχνικές προεπεξεργασίας εικόνας, διαφορετικούς post‑processors ή εναλλακτικές μηχανές OCR. Το βασικό μοτίβο—**run OCR on image → extract text from image → OCR text correction → improve OCR accuracy**—παραμένει το ίδιο, παρέχοντάς σας μια στιβαρή βάση για οποιοδήποτε έργο ψηφιοποίησης εγγράφων.

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση σας.

- [Convert Image to Text: Extract Text from Image Using Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}