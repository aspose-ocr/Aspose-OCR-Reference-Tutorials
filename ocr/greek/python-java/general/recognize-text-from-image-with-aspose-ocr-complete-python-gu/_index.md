---
category: general
date: 2026-06-28
description: Μάθετε πώς να αναγνωρίζετε κείμενο από εικόνα και να εκτελείτε OCR σε
  εικόνα χρησιμοποιώντας το Aspose OCR για Python. Περιλαμβάνει βήματα για τον καθορισμό
  της γλώσσας OCR και την εξαγωγή των βαθμών εμπιστοσύνης.
draft: false
keywords:
- recognize text from image
- perform ocr on image
- how to set OCR language
language: el
og_description: Αναγνωρίστε κείμενο από εικόνα χρησιμοποιώντας το Aspose OCR σε Python.
  Αυτός ο οδηγός δείχνει πώς να ορίσετε τη γλώσσα OCR, να εκτελέσετε OCR σε εικόνα
  και να διαβάσετε τα επίπεδα εμπιστοσύνης.
og_title: Αναγνώριση κειμένου από εικόνα – Πλήρες σεμινάριο OCR με Python
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn how to recognize text from image and perform OCR on image using
    Aspose OCR for Python. Includes steps to set OCR language and extract confidence
    scores.
  headline: recognize text from image with Aspose OCR – Complete Python Guide
  type: TechArticle
- description: Learn how to recognize text from image and perform OCR on image using
    Aspose OCR for Python. Includes steps to set OCR language and extract confidence
    scores.
  name: recognize text from image with Aspose OCR – Complete Python Guide
  steps:
  - name: What if my image contains multiple languages?
    text: 'Aspose OCR supports multi‑language detection, but you need to pass a **combined
      language flag**. For example, to handle both Latin and Cyrillic:'
  - name: How do I improve accuracy on low‑resolution images?
    text: '- **Pre‑process** the image: increase contrast, apply binarization, or
      upscale using a library like Pillow. - **Set the correct DPI** if you know it;
      Aspose respects the image metadata. - **Choose the right language**—the more
      specific you are, the better the model performs.'
  - name: Can I extract only certain regions of the image?
    text: Yes. Use the `recognizeRegion` method (not shown in the basic example) and
      pass a rectangle object defining the area of interest. This is handy when you
      only need a table or a specific block of text.
  type: HowTo
tags:
- OCR
- Python
- Aspose
title: Αναγνώριση κειμένου από εικόνα με το Aspose OCR – Πλήρης Οδηγός Python
url: /el/python-java/general/recognize-text-from-image-with-aspose-ocr-complete-python-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση κειμένου από εικόνα με Aspose OCR – Πλήρης Οδηγός Python

Έχετε ποτέ χρειαστεί να **αναγνωρίσετε κείμενο από εικόνα** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη θα σας προσφέρει ταυτόχρονα ταχύτητα και ακρίβεια; Δεν είστε μόνοι. Στον κόσμο του αυτοματισμού εγγράφων, η δυνατότητα **να εκτελείτε OCR σε εικόνες** αποτελεί καθημερινή απαίτηση — είτε ψηφιοποιείτε αποδείξεις, σαρώνετε διαβατήρια ή εξάγετε δεδομένα από πολυγλωσσικές πινακίδες.

Σε αυτό το tutorial θα περάσουμε από ένα πρακτικό παράδειγμα που δείχνει ακριβώς πώς να **αναγνωρίσετε κείμενο από εικόνα** χρησιμοποιώντας το Aspose OCR για Python, και θα καλύψουμε επίσης **πώς να ορίσετε τη γλώσσα OCR** ώστε η μηχανή να γνωρίζει αν αντιμετωπίζει Λατινικό, Κυριλλικό ή οποιοδήποτε άλλο σύστημα γραφής. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση script που εκτυπώνει το πλήρες κείμενο, την εμπιστοσύνη γραμμή‑προς‑γραμμή, και ακόμη τα περιγράμματα (bounding boxes) για κάθε λέξη.

## Τι Θα Χρειαστεί

- **Python 3.8+** (ο κώδικας λειτουργεί σε οποιαδήποτε πρόσφατη έκδοση)
- Πακέτο **Aspose.OCR for Python via Java** – εγκαταστήστε το με `pip install aspose-ocr`
- Ένα αρχείο εικόνας (π.χ., `mixed_script.png`) που περιέχει το κείμενο που θέλετε να εξάγετε
- Ένα βασικό IDE ή επεξεργαστή — VS Code, PyCharm, ή ακόμη και ένας απλός επεξεργαστής κειμένου αρκούν

Καμία βαριά εξάρτηση, κανένα native binary για μεταγλώττιση. Μόνο μια εντολή pip και είστε έτοιμοι.

## Βήμα 1: Εγκατάσταση και Εισαγωγή της Μηχανής OCR

Πρώτα απ’ όλα, ας φέρουμε τη βιβλιοθήκη στο μηχάνημά σας και ας εισάγουμε τις κλάσεις που θα χρειαστείτε.

```python
# Install the package (run this once in your terminal)
# pip install aspose-ocr

# Import the OCR engine and the language enumeration
from asposeocrjava import OcrEngine, Language
```

> **Pro tip:** Αν βρίσκεστε πίσω από εταιρικό proxy, προσθέστε τη σημαία `--proxy` στην εντολή pip. Σας εξοικονομεί πολύ κόπο αργότερα.

## Βήμα 2: Δημιουργία της Μηχανής και **πώς να ορίσετε τη γλώσσα OCR**

Η δημιουργία ενός αντικειμένου `OcrEngine` είναι τόσο απλή όσο η κλήση του κατασκευαστή του, αλλά η πραγματική δύναμη έρχεται όταν λέτε στη μηχανή ποια γλώσσα να περιμένει. Αυτό είναι το τμήμα που απαντά στην ερώτηση “**πώς να ορίσετε τη γλώσσα OCR**”.

```python
# Instantiate the OCR engine
ocr_engine = OcrEngine()

# Tell the engine we’re dealing with Latin script (you can pick others like Language.Cyrillic)
ocr_engine.setLanguage(Language.Latin)
```

Γιατί είναι σημαντικό; Οι αλγόριθμοι OCR χρησιμοποιούν μοντέλα χαρακτήρων ειδικά για κάθε γλώσσα· η σωστή ρύθμιση της γλώσσας αυξάνει δραστικά την ακρίβεια, ειδικά για συστήματα γραφής με παρόμοια σύμβολα (σκεφτείτε το “0” vs “O” στα Λατινικά vs το “О” στα Κυριλλικά).

## Βήμα 3: **εκτέλεση OCR σε εικόνα** – Αναγνώριση του Κειμένου

Τώρα δίνουμε στη μηχανή τη διαδρομή της εικόνας και την αφήνουμε να κάνει τη μαγεία της. Η μέθοδος επιστρέφει ένα αντικείμενο `RecognitionResult` που περιέχει όλα όσα μπορεί να χρειαστείτε.

```python
# Path to the image you want to process
image_path = "YOUR_DIRECTORY/mixed_script.png"

# Run the OCR operation
recognition_result = ocr_engine.recognizeImage(image_path)
```

Αν το αρχείο δεν βρεθεί, το Aspose θα ρίξει ένα `FileNotFoundError`. Τυλίξτε την κλήση σε μπλοκ `try/except` για κώδικα παραγωγής — τίποτα δεν είναι χειρότερο από μια μη διαχειριζόμενη εξαίρεση που καταρρέει την υπηρεσία σας.

## Βήμα 4: Εκτύπωση του Πλήρους Αναγνωρισμένου Κειμένου

Η πιο συνηθισμένη αίτηση είναι απλώς “δώσε μου το κείμενο”. Η μέθοδος `getText()` ενώνει όλες τις ανιχνευμένες γραμμές σε μία συμβολοσειρά.

```python
# Print the complete text extracted from the image
print("Full text:", recognition_result.getText())
```

Θα δείτε κάτι σαν:

```
Full text: Hello World!
This is a sample mixed‑script image.
```

Αυτό είναι το βασικό κομμάτι της **αναγνώρισης κειμένου από εικόνα** — μια μιά‑γραμμή που επιστρέφει ό,τι η μηχανή κατάφερε να αποκρυπτογραφήσει.

## Βήμα 5: (Προαιρετικό) Εμφάνιση Εμπιστοσύνης για Κάθε Ανιχνευμένη Γραμμή

Οι βαθμοί εμπιστοσύνης σας επιτρέπουν να εκτιμήσετε την αξιοπιστία. Γραμμές με βαθμό κάτω από, π.χ., 0.70 μπορεί να χρειάζονται ανθρώπινη επανεξέταση.

```python
print("\n--- Line‑by‑Line Confidence ---")
for line in recognition_result.getLines():
    # Each line object provides its text and a confidence value between 0 and 1
    print(f"Line: '{line.getText()}'  Confidence: {line.getConfidence():.2f}")
```

Τυπική έξοδος:

```
Line: 'Hello World!'  Confidence: 0.98
Line: 'This is a sample mixed‑script image.'  Confidence: 0.85
```

## Βήμα 6: (Προαιρετικό) Ανάκτηση Περιγραμμάτων για Κάθε Λέξη – Ιδανικό για Επισήμανση UI

Αν δημιουργείτε έναν προβολέα που επιτρέπει στους χρήστες να κάνουν κλικ σε μια λέξη για να δουν τα δεδομένα OCR, οι συντεταγμένες του περιγράμματος είναι πολύτιμες.

```python
print("\n--- Word Bounding Boxes ---")
for word in recognition_result.getWords():
    bbox = word.getBoundingBox()   # Returns (x, y, width, height)
    print(f"Word '{word.getText()}' at {bbox}")
```

Παράδειγμα εξόδου:

```
Word 'Hello' at (12, 34, 58, 20)
Word 'World' at (78, 34, 60, 20)
```

Αυτές οι συντεταγμένες είναι σε εικονοστοιχεία (pixels) σε σχέση με την αρχική εικόνα, ώστε να μπορείτε να τις τοποθετήσετε απευθείας πάνω σε έναν καμβά.

## Πλήρες Λειτουργικό Script

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι ένα έτοιμο‑για‑εκτέλεση script που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο. Απλώς αντικαταστήστε το `YOUR_DIRECTORY/mixed_script.png` με την πραγματική διαδρομή της εικόνας σας.

```python
# ocr_demo.py
from asposeocrjava import OcrEngine, Language

def main(image_path: str, language: Language = Language.Latin):
    """
    Recognize text from an image using Aspose OCR.
    Parameters:
        image_path (str): Full path to the image file.
        language (Language): OCR language to use (default: Latin).
    """
    # Create the OCR engine and set the desired language
    ocr_engine = OcrEngine()
    ocr_engine.setLanguage(language)

    try:
        # Perform OCR
        result = ocr_engine.recognizeImage(image_path)

        # Full text output
        print("Full text:", result.getText())

        # Optional: line confidence
        print("\n--- Line‑by‑Line Confidence ---")
        for line in result.getLines():
            print(f"Line: '{line.getText()}'  Confidence: {line.getConfidence():.2f}")

        # Optional: word bounding boxes
        print("\n--- Word Bounding Boxes ---")
        for word in result.getWords():
            bbox = word.getBoundingBox()
            print(f"Word '{word.getText()}' at {bbox}")

    except FileNotFoundError:
        print(f"Error: Image file not found at {image_path}")
    except Exception as e:
        print(f"An unexpected error occurred: {e}")

if __name__ == "__main__":
    # Change the path below to point at your own test image
    IMAGE_PATH = "YOUR_DIRECTORY/mixed_script.png"
    main(IMAGE_PATH, Language.Latin)
```

Τρέξτε το με:

```bash
python ocr_demo.py
```

Θα πρέπει να δείτε το πλήρες εξαγόμενο κείμενο, τις βαθμολογίες εμπιστοσύνης και τα περιγράμματα εκτυπωμένα στην κονσόλα.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν η εικόνα μου περιέχει πολλαπλές γλώσσες;

Το Aspose OCR υποστηρίζει ανίχνευση πολλαπλών γλωσσών, αλλά πρέπει να περάσετε μια **συνδυασμένη σημαία γλώσσας**. Για παράδειγμα, για να χειριστείτε τόσο Λατινικά όσο και Κυριλλικά:

```python
ocr_engine.setLanguage(Language.Latin | Language.Cyrillic)
```

Ο τελεστής pipe (`|`) συγχωνεύει τα enums. Αυτό απαντά στην απαίτηση “**εκτέλεση OCR σε εικόνα**” για πολυγλωσσικά σενάρια.

### Πώς μπορώ να βελτιώσω την ακρίβεια σε εικόνες χαμηλής ανάλυσης;

- **Προεπεξεργασία** της εικόνας: αυξήστε την αντίθεση, εφαρμόστε δυαδικοποίηση ή upscale χρησιμοποιώντας βιβλιοθήκη όπως το Pillow.
- **Ορίστε το σωστό DPI** αν το γνωρίζετε· το Aspose σέβεται τα μεταδεδομένα της εικόνας.
- **Επιλέξτε τη σωστή γλώσσα** — όσο πιο συγκεκριμένη είστε, τόσο καλύτερο είναι το μοντέλο.

### Μπορώ να εξάγω μόνο συγκεκριμένες περιοχές της εικόνας;

Ναι. Χρησιμοποιήστε τη μέθοδο `recognizeRegion` (δεν εμφανίζεται στο βασικό παράδειγμα) και περάστε ένα αντικείμενο rectangle που ορίζει την περιοχή ενδιαφέροντος. Αυτό είναι χρήσιμο όταν χρειάζεστε μόνο έναν πίνακα ή ένα συγκεκριμένο μπλοκ κειμένου.

## Συμπέρασμα

Μόλις περάσαμε από ένα πλήρες, end‑to‑end παράδειγμα για το πώς να **αναγνωρίσετε κείμενο από εικόνα** χρησιμοποιώντας το Aspose OCR για Python. Τώρα ξέρετε πώς να **εκτελείτε OCR σε εικόνα**, να ορίζετε σωστά τη **γλώσσα OCR**, και να ανακτάτε τόσο βαθμούς εμπιστοσύνης όσο και περιγράμματα λέξεων για επόμενη επεξεργασία UI.

Από εδώ μπορείτε:

- Να πειραματιστείτε με άλλες γλώσσες (`Language.Arabic`, `Language.Japanese`, κ.λπ.)
- Να ενσωματώσετε το script σε μια web υπηρεσία (Flask/Django) για να παρέχετε OCR ως API
- Να συνδυάσετε τα δεδομένα περιγράμματος με ένα frontend καμβά ώστε οι χρήστες να μπορούν να επισημαίνουν κείμενο

Οι δυνατότητες είναι τόσο ευρείες όσο τα έγγραφα που χρειάζεται να ψηφιοποιήσετε. Έχετε μια δύσκολη εικόνα που δεν συνεργάζεται; Αφήστε ένα σχόλιο και θα το αντιμετωπίσουμε μαζί. Καλή προγραμματιστική!

![recognize text from image example](/images/ocr_example.png "recognize text from image – Aspose OCR output")


## Τι Θα Μάθετε Στη Σειρά Επόμενη;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κυριαρχήσετε σε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση των δικών σας έργων.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}