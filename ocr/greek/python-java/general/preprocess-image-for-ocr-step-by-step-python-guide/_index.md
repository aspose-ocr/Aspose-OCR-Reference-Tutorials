---
category: general
date: 2026-06-22
description: Προεπεξεργασία εικόνας για OCR ώστε να εξάγετε κείμενο από την εικόνα
  και να βελτιώσετε την ακρίβεια του OCR χρησιμοποιώντας το Aspose OCR σε Python.
  Συμπεριλαμβάνεται πλήρες, εκτελέσιμο παράδειγμα.
draft: false
keywords:
- preprocess image for OCR
- extract text from image
- improve OCR accuracy
language: el
og_description: Προεπεξεργασία εικόνας για OCR, εξαγωγή κειμένου από εικόνα και βελτίωση
  της ακρίβειας του OCR με το Aspose OCR. Μάθετε τη πλήρη ροή εργασίας σε Python.
og_title: Προεπεξεργασία εικόνας για OCR – Πλήρης οδηγός Python
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Preprocess image for OCR to extract text from image and improve OCR
    accuracy using Aspose OCR in Python. Complete, runnable example included.
  headline: Preprocess Image for OCR – Step‑by‑Step Python Guide
  type: TechArticle
- description: Preprocess image for OCR to extract text from image and improve OCR
    accuracy using Aspose OCR in Python. Complete, runnable example included.
  name: Preprocess Image for OCR – Step‑by‑Step Python Guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Why it matters | |-------------|----------------| | Python
      3.8+ | Aspose OCR’s wheels target modern interpreters. | | `aspose-ocr` package
      (`pip install aspose-ocr`) | Provides the `OcrEngine`, `ImagePreprocessor`,
      and filter classes. | | A sample image (e.g., `noisy-document.jpg`) |'
  - name: – Initialise the OCR Engine and Load Your Source Image
    text: '```python import aspose.ocr as ocr'
  - name: – Build a Preprocessing Chain to Clean the Image
    text: '```python # Initialise the preprocessor – a container for a series of filters
      preprocessor = ocr.ImagePreprocessor()'
  - name: – Attach the Preprocessor to the Engine
    text: '```python # Hook the preprocessing pipeline into the OCR engine ocr_engine.set_preprocessor(preprocessor)
      ```'
  - name: – Run OCR and Extract Text from Image
    text: '```python # Perform the recognition on the pre‑processed image recognition_result
      = ocr_engine.recognize()'
  - name: – Verify the Output and Fine‑Tune for Better Accuracy
    text: '```python # Quick sanity check: print length and a sample snippet print(f"Detected
      {len(extracted_text)} characters.") print("First 200 chars:", extracted_text[:200])
      ```'
  type: HowTo
- questions:
  - answer: Yes. Convert each page to an image (e.g., using `pdf2image`) and feed
      it through the same pipeline in a loop. The same `preprocess image for OCR`
      steps apply per page.
    question: Does this work with multi‑page PDFs?
  - answer: 'Set the language before recognition: `engine.set_language(ocr.Language.FRENCH)`.
      The preprocessing filters stay the same; only the language model changes.'
    question: What if my document is in a language other than English?
  - answer: 'Absolutely. The `ImagePreprocessor` is extensible—just call `add_filter`
      again. For heavy‑dotted backgrounds, `ocr.Filters.MedianFilter(kernel=3)` can
      be useful. --- ## Wrap‑Up We’ve just **preprocess image for OCR**, run Aspose’s
      engine, and **extract text from image** while showcasing several tric'
    question: Can I chain more filters?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: Προεπεξεργασία εικόνας για OCR – Οδηγός Python βήμα‑βήμα
url: /el/python-java/general/preprocess-image-for-ocr-step-by-step-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προεπεξεργασία Εικόνας για OCR – Πλήρης Οδηγός Python

Αν χρειάζεστε **preprocess image for OCR**, πιθανότατα έχετε αντιμετωπίσει θορυβώδεις σκαναρισμένες εικόνες, λοξά σελίδες ή φωτογραφίες χαμηλής αντίθεσης που δεν συνεργάζονται. Έχετε προσπαθήσει ποτέ να εξάγετε κείμενο από εικόνα μόνο για να πάρετε ένα ακατάστατο μπερδεμένο κείμενο; Εκεί ακριβώς μια καλή αλυσίδα προεπεξεργασίας μπορεί να κάνει τη διαφορά μεταξύ μερικών αναγνώσιμων λέξεων και ενός πλήρους εφιάλτη μεταγραφής.

Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα από ένα πλήρες, end‑to‑end παράδειγμα που **extracts text from image** ενώ ταυτόχρονα δείχνει πώς να **improve OCR accuracy** χρησιμοποιώντας το Aspose OCR for Python. Χωρίς ασαφείς αναφορές—μόνο ο κώδικας που μπορείτε να αντιγράψετε‑επικολλήσετε, η λογική πίσω από κάθε γραμμή, και συμβουλές για πραγματικές περιπτώσεις.

## Τι Θα Μάθετε

- Ένα έτοιμο‑για‑εκτέλεση script Python που φορτώνει ένα θορυβώδες έγγραφο, το καθαρίζει και εκτυπώνει το αναγνωρισμένο κείμενο.  
- Κατανόηση του γιατί κάθε φίλτρο προεπεξεργασίας είναι σημαντικό και πώς να ρυθμίσετε τις παραμέτρους του.  
- Στρατηγικές για την αντιμετώπιση κοινών προβλημάτων όπως έντονος θόρυβος σπόρων, ακραία περιστροφή ή σκαναρισμένες εικόνες χαμηλής αντίθεσης.  

### Προαπαιτούμενα

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|-----------------------|
| Python 3.8+ | Τα wheels του Aspose OCR στοχεύουν σε σύγχρονους διερμηνείς. |
| `aspose-ocr` package (`pip install aspose-ocr`) | Παρέχει τις κλάσεις `OcrEngine`, `ImagePreprocessor` και τα φίλτρα. |
| A sample image (e.g., `noisy-document.jpg`) | Θα χρησιμοποιήσουμε μια σκόπιμα ακατάστατη εικόνα για να δείξουμε τα οφέλη της προεπεξεργασίας. |
| Basic familiarity with Python functions | Σας βοηθά να προσαρμόσετε το script στη δική σας ροή εργασίας. |

> **Pro tip:** Αν χρησιμοποιείτε Windows, εκτελέστε το script μέσα σε ένα virtual environment για να αποφύγετε συγκρούσεις εκδόσεων.

---

## Προεπεξεργασία Εικόνας για OCR με Aspose OCR (Python)

Παρακάτω είναι η καρδιά του tutorial—μια βήμα‑βήμα ανάλυση του κώδικα που θα χρειαστείτε. Κάθε ενότητα εξηγεί **τι** κάνουμε *και* **γιατί** το κάνουμε, ώστε να μπορείτε να προσαρμόσετε την αλυσίδα αργότερα χωρίς εικασίες.

![preprocess image for OCR example](ocr-preprocess.png){alt="προεπεξεργασία εικόνας για OCR"}

### Βήμα 1 – Initialise the OCR Engine and Load Your Source Image

```python
import aspose.ocr as ocr

# Create the OCR engine – the central object that drives recognition
ocr_engine = ocr.OcrEngine()

# Load the raw image file. Using ImageStream lets Aspose handle various formats.
ocr_engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/noisy-document.jpg"))
```

- **Why** an `OcrEngine`? Encapsulates the recognizer, language settings, and (later) the preprocessor.  
- **Why** `ImageStream.from_file`? Abstracts away file‑type handling, so you can swap JPEG for PNG without code changes.

### Βήμα 2 – Build a Preprocessing Chain to Clean the Image

```python
# Initialise the preprocessor – a container for a series of filters
preprocessor = ocr.ImagePreprocessor()

# 1️⃣ Deskew – corrects any rotation so text lines become horizontal.
preprocessor.add_filter(ocr.Filters.Deskew())

# 2️⃣ Despeckle – removes isolated noise pixels; strength=2 is a good middle ground.
preprocessor.add_filter(ocr.Filters.Despeckle(strength=2))

# 3️⃣ ContrastBoost – lifts faint characters; level=1.5 amplifies contrast without blowing out highlights.
preprocessor.add_filter(ocr.Filters.ContrastBoost(level=1.5))
```

**Πώς αυτά τα φίλτρα βελτιώνουν την ακρίβεια του OCR:**  
- **Deskew** εξαλείφει το κοινό πρόβλημα “λίγης σελίδας” που μπερδεύει τη διαίρεση χαρακτήρων.  
- **Despeckle** στοχεύει στα σπαστά που παράγονται από χαμηλής ποιότητας σαρωτές· μεγαλύτερη ισχύς αφαιρεί περισσότερο θόρυβο αλλά μπορεί να φθείρει λεπτομέρειες.  
- **ContrastBoost** κάνει το σκοτεινό κείμενο να ξεχωρίζει από το φωτεινό φόντο, κλασική νίκη για τις περισσότερες μηχανές OCR.

> **Edge case:** Αν το έγγραφό σας είναι ήδη τέλεια ευθεία, μπορείτε να παραλείψετε το `Deskew()` για να κερδίσετε μερικά χιλιοστά του δευτερολέπτου.

### Βήμα 3 – Attach the Preprocessor to the Engine

```python
# Hook the preprocessing pipeline into the OCR engine
ocr_engine.set_preprocessor(preprocessor)
```

Τώρα κάθε φορά που εκτελείται `ocr_engine.recognize()`, θα τρέχει πρώτα τα τρία φίλτρα με τη σειρά που τα ορίσαμε. Η σειρά μετρά: θέλετε **deskew before despeckling**, διαφορετικά το φίλτρο σπόρων μπορεί να ερμηνεύσει λανθασμένα τις περιστρεφόμενες άκρες ως θόρυβο.

### Βήμα 4 – Run OCR and Extract Text from Image

```python
# Perform the recognition on the pre‑processed image
recognition_result = ocr_engine.recognize()

# Pull out the plain text string
extracted_text = recognition_result.get_text()
print(extracted_text)
```

- Η κλήση `recognize()` επιστρέφει ένα αντικείμενο `RecognitionResult` που περιέχει όχι μόνο το ακατέργαστο κείμενο αλλά και βαθμολογίες εμπιστοσύνης, περιοχές (bounding boxes) και λεπτομέρειες γλώσσας.  
- Εδώ χρειαζόμαστε μόνο το απλό string, αλλά μπορείτε να εξερευνήσετε το `recognition_result.get_confidence()` για έναν γρήγορο έλεγχο **improve OCR accuracy**.

### Βήμα 5 – Verify the Output and Fine‑Tune for Better Accuracy

```python
# Quick sanity check: print length and a sample snippet
print(f"Detected {len(extracted_text)} characters.")
print("First 200 chars:", extracted_text[:200])
```

Αν το αποτέλεσμα εξακολουθεί να περιέχει ακατάστατα σύμβολα, σκεφτείτε τις παρακάτω προσαρμογές:

| Πρόβλημα | Προτεινόμενη Διόρθωση |
|----------|----------------------|
| Ακόμα θολό κείμενο | Increase `ContrastBoost(level)` to 2.0 or add `ocr.Filters.GaussianBlur(radius=1)` before despeckling. |
| Πάρα πολλοί ανεπιθύμητοι χαρακτήρες | Raise `Despeckle(strength)` to 3, or insert `ocr.Filters.RemoveLines()` to strip horizontal rules. |
| Η κλίση παραμένει | Call `ocr.Filters.Deskew(max_angle=5)` to limit correction to mild rotations. |

---

## Πλήρες, Εκτελέσιμο Script

Αντιγράψτε το παρακάτω μπλοκ σε ένα αρχείο με όνομα `ocr_preprocess.py`. Αντικαταστήστε το `YOUR_DIRECTORY/noisy-document.jpg` με την πραγματική διαδρομή της εικόνας σας, μετά τρέξτε `python ocr_preprocess.py`.

```python
import aspose.ocr as ocr

def main():
    # Initialise engine and load image
    engine = ocr.OcrEngine()
    engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/noisy-document.jpg"))

    # Build preprocessing pipeline
    preproc = ocr.ImagePreprocessor()
    preproc.add_filter(ocr.Filters.Deskew())
    preproc.add_filter(ocr.Filters.Despeckle(strength=2))
    preproc.add_filter(ocr.Filters.ContrastBoost(level=1.5))

    # Attach pipeline
    engine.set_preprocessor(preproc)

    # Recognise and extract text
    result = engine.recognize()
    text = result.get_text()

    # Display results
    print("\n--- OCR Output ---")
    print(text)
    print("\n--- Summary ---")
    print(f"Characters detected: {len(text)}")
    print("Snippet:", text[:200].replace("\n", " "))

if __name__ == "__main__":
    main()
```

Η εκτέλεση αυτού του script σε μια θορυβώδη, ελαφρώς περιστραμμένη JPEG θα πρέπει να αποδώσει καθαρό, αναγνώσιμο κείμενο—δείχνοντας πώς μια καλά σχεδιασμένη αλυσίδα προεπεξεργασίας **improves OCR accuracy** δραματικά.

---

## Συχνές Ερωτήσεις & Απαντήσεις

**Ε: Λειτουργεί αυτό με PDF πολλαπλών σελίδων;**  
Α: Ναι. Μετατρέψτε κάθε σελίδα σε εικόνα (π.χ., χρησιμοποιώντας `pdf2image`) και τροφοδοτήστε την μέσω της ίδιας pipeline σε βρόχο. Τα ίδια βήματα `preprocess image for OCR` εφαρμόζονται ανά σελίδα.

**Ε: Τι γίνεται αν το έγγραφό μου είναι σε γλώσσα διαφορετική από τα Αγγλικά;**  
Α: Ορίστε τη γλώσσα πριν την αναγνώριση: `engine.set_language(ocr.Language.FRENCH)`. Τα φίλτρα προεπεξεργασίας παραμένουν τα ίδια· μόνο το μοντέλο γλώσσας αλλάζει.

**Ε: Μπορώ να προσθέσω περισσότερα φίλτρα;**  
Α: Απόλυτα. Το `ImagePreprocessor` είναι επεκτάσιμο—απλώς καλέστε ξανά `add_filter`. Για βαριά φόντα με κουκκίδες, το `ocr.Filters.MedianFilter(kernel=3)` μπορεί να είναι χρήσιμο.

---

## Συμπεράσματα

Μόλις **preprocess image for OCR**, τρέξαμε τη μηχανή του Aspose και **extract text from image** παρουσιάζοντας αρκετές τεχνικές για **improve OCR accuracy**. Το πλήρες παράδειγμα είναι έτοιμο να ενσωματωθεί σε οποιοδήποτε έργο, και ο μοντέλο φίλτρων σημαίνει ότι μπορείτε να προσθέσετε, αφαιρέσετε ή αλλάξετε βήματα ανάλογα με τις ανάγκες των δεδομένων σας.

Επόμενα βήματα:

- **Batch processing** εκατοντάδων σαρώσεων με `concurrent.futures`.  
- **Post‑processing** με βιβλιοθήκες ελέγχου ορθογραφίας (π.χ., `pyspellchecker`) για να καθαρίσετε τα τυπογραφικά λάθη που εισάγει το OCR.  
- **Integrating** το script σε μια web υπηρεσία χρησιμοποιώντας Flask ή FastAPI, μετατρέποντάς το σε micro‑service OCR κατόπιν ζήτησης.

Δοκιμάστε το, ρυθμίστε τις εντάσεις των φίλτρων, και παρακολουθήστε τις αναλογίες αναγνώρισης να ανεβαίνουν. Αν συναντήσετε πρόβλημα, αφήστε ένα σχόλιο—καλή προγραμματιστική!

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Βήμα‑βήμα](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Πώς να Χρησιμοποιήσετε AspOCR: Φίλτρα Προεπεξεργασίας Εικόνας OCR για .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Εξαγωγή Κειμένου από Εικόνα – Βελτιστοποίηση OCR με Aspose.OCR για .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}