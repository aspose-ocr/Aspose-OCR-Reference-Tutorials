---
category: general
date: 2026-03-18
description: Εκτελέστε OCR σε εικόνα για να εξάγετε γρήγορα κείμενο από την εικόνα.
  Μάθετε πώς να φορτώνετε εικόνα για OCR, να δημιουργείτε μηχανή OCR και να βελτιώνετε
  την ακρίβεια του OCR με επιλογές γλώσσας.
draft: false
keywords:
- perform OCR on image
- extract text from image
- improve OCR accuracy
- load image for OCR
- create OCR engine
language: el
og_description: Εκτελέστε OCR σε εικόνα με αυτόν τον λεπτομερή οδηγό. Μάθετε πώς να
  φορτώνετε εικόνα για OCR, να δημιουργείτε μηχανή OCR και να βελτιώνετε την ακρίβεια
  του OCR για αξιόπιστη εξαγωγή κειμένου.
og_title: Εκτέλεση OCR σε εικόνα – Πλήρης οδηγός προγραμματισμού
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Διενέργεια OCR σε εικόνα – Οδηγός βήμα‑βήμα
url: /el/python-java/general/perform-ocr-on-image-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε Εικόνα – Πλήρης Προγραμματιστικό Εγχειρίδιο

Κάποτε χρειάστηκε να **perform OCR on image** αλλά δεν ήξερες ποια βιβλιοθήκη να επιλέξεις ή πώς να πάρεις αξιόπιστα αποτελέσματα; Δεν είσαι μόνος. Σε αυτόν τον οδηγό θα περάσουμε από όλα όσα χρειάζεσαι για **extract text from image**, από τη φόρτωση της εικόνας μέχρι τη ρύθμιση των επιλογών γλώσσας ώστε να **improve OCR accuracy** σε κάθε βήμα.

Θα καλύψουμε πώς να **load image for OCR**, πώς να **create OCR engine**, και γιατί κάθε ρύθμιση είναι σημαντική. Στο τέλος θα έχεις ένα έτοιμο‑για‑εκτέλεση script που εκτυπώνει το αναγνωρισμένο κείμενο, και θα κατανοήσεις το “γιατί” πίσω από κάθε γραμμή—χωρίς ασαφείς συντομεύσεις “δείτε τα docs”. Ας βουτήξουμε.

## Τι Θα Χρειαστείτε

- Python 3.8+ (ο κώδικας χρησιμοποιεί f‑strings και type hints)
- Το υποθετικό πακέτο `ocr_lib` – εγκαταστήστε το με `pip install ocr_lib`
- Ένα αρχείο εικόνας που περιέχει καθαρό, τυπωμένο κείμενο (π.χ., `lab_report.png`)
- Έναν βασικό επεξεργαστή κειμένου ή IDE (VS Code, PyCharm, ό,τι προτιμάτε)

Αν τα έχετε ήδη, τέλεια—είστε έτοιμοι. Αν όχι, κατεβάστε την Python από python.org και τρέξτε την εντολή pip· χρειάζεται μόνο ένα λεπτό.

![perform OCR on image example](/images/ocr-example.png)

*Alt text: εκτέλεση OCR σε εικόνα – δείγμα εξόδου που εμφανίζει το εξαγόμενο κείμενο.*

## Βήμα 1: Δημιουργία Μηχανής OCR – Πώς να **create OCR engine** σε Python

Πριν μπορέσει να γίνει οποιαδήποτε αναγνώριση, η βιβλιοθήκη χρειάζεται ένα αντικείμενο μηχανής που κρατά τις ρυθμίσεις και την κατάσταση εκτέλεσης. Σκεφτείτε τη μηχανή ως τον εγκέφαλο πίσω από τη λειτουργία.

```python
# step_1_create_engine.py
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    """
    Initialize and return a fresh OcrEngine instance.
    Creating the engine once and reusing it is more efficient than
    instantiating it inside a loop.
    """
    engine = OcrEngine()
    return engine
```

**Why this matters:** Η δημιουργία της μηχανής νωρίς σας επιτρέπει να προσθέσετε επιλογές γλώσσας αργότερα, και επίσης αποθηκεύει εσωτερικά μοντέλα στην κρυφή μνήμη για ταχύτερες επόμενες κλήσεις.

## Βήμα 2: Φόρτωση Εικόνας για OCR – Ο σωστός τρόπος να **load image for OCR**

Τώρα που έχουμε μια μηχανή, πρέπει να της δώσουμε κάτι να διαβάσει. Η μέθοδος `setImageFromFile` δέχεται μια διαδρομή συστήματος αρχείων· η διαδρομή μπορεί να είναι απόλυτη ή σχετική με το φάκελο εργασίας του script.

```python
# step_2_load_image.py
def load_image(engine: OcrEngine, image_path: str) -> None:
    """
    Attach an image file to the engine.
    Raises FileNotFoundError if the file does not exist.
    """
    engine.setImageFromFile(image_path)
```

**Pro tip:** Χρησιμοποιήστε απόλυτη διαδρομή ή `os.path.join` για να αποφύγετε εκπλήξεις “file not found” όταν το script εκτελείται από διαφορετικό φάκελο.

```python
import os

image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
load_image(my_engine, image_file)
```

## Βήμα 3: Βελτίωση Ακρίβειας OCR – Ρύθμιση **language options** για **improve OCR accuracy**

Το OCR λειτουργεί κατευθείαν, αλλά λεξιλόγια ειδικών τομέων (όπως η ορολογία του εργαστηρίου) συχνά το μπλοκάρουν. Με την παροχή προσαρμοσμένου λεξικού και λίστας αποκλεισμού μειώνετε λανθασμένες αναγνώσεις, όπως η σύγχυση “0” με “O”.

```python
# step_3_language_options.py
def configure_language(engine: OcrEngine) -> None:
    """
    Set up language options to help the engine recognize domain‑specific terms
    and ignore characters that are frequently misread.
    """
    language_opts = LanguageOptions()
    # Add terms that appear often in laboratory reports
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    # Blacklist characters that cause confusion
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)
```

**Why this helps:** Το λεξικό λέει στο μοντέλο OCR ότι το “HPLC” είναι έγκυρο token, αποτρέποντας το να σπάσει τη λέξη σε άσχετα κομμάτια. Η λίστα αποκλεισμού λέει στο μοντέλο να θεωρεί ασαφή σύμβολα ως θόρυβο, κάτι που **improves OCR accuracy** άμεσα.

## Βήμα 4: Εκτέλεση OCR σε Εικόνα – Η κύρια κλήση **perform OCR on image**

Με τη μηχανή προετοιμασμένη και την εικόνα συνδεδεμένη, ήρθε η ώρα να αναγνωρίσουμε πραγματικά το κείμενο. Αυτό το βήμα επιστρέφει ένα αντικείμενο `OcrResult` που μπορείτε να ερωτήσετε για ακατέργαστο κείμενο, βαθμούς εμπιστοσύνης ή περιοχές (bounding boxes).

```python
# step_4_recognize.py
def recognize_text(engine: OcrEngine) -> OcrResult:
    """
    Run the OCR process. This may take a few seconds depending on image size.
    Returns an OcrResult that contains the extracted string and metadata.
    """
    result = engine.recognize()
    return result
```

Αν η εικόνα είναι θολή, θα δείτε χαμηλότερους αριθμούς εμπιστοσύνης στο αποτέλεσμα. Αυτό είναι ένδειξη να προεπεξεργαστείτε την εικόνα (π.χ., αύξηση αντίθεσης) πριν τη δώσετε στη μηχανή.

## Βήμα 5: Εξαγωγή Κειμένου από Εικόνα – Λήψη του τελικού κειμένου

Τέλος, ζητάμε από το `OcrResult` την κειμενική του αναπαράσταση. Η μέθοδος `getText()` επιστρέφει μια συμβολοσειρά plain‑text έτοιμη για επεξεργασία (αποθήκευση σε αρχείο, εισαγωγή σε βάση δεδομένων κ.λπ.).

```python
# step_5_output.py
def print_result(result: OcrResult) -> None:
    """
    Output the recognized text to the console.
    You could also write it to a file with open('output.txt', 'w') …
    """
    extracted = result.getText()
    print("=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===")
```

**Expected output:** Υποθέτοντας ότι το `lab_report.png` περιέχει έναν απλό πίνακα, μπορεί να δείτε κάτι όπως:

```
=== OCR Output Start ===
Sample ID: 00123
Method: HPLC
Result: 5.67 mg/L
=== OCR Output End ===
```

Αυτό ολοκληρώνει το τμήμα **extract text from image**.

## Πλήρες Παράδειγμα Λειτουργίας – Συνδυάστε Όλα Μαζί

Παρακάτω υπάρχει ένα ενιαίο script που ενώνει τα κομμάτια από τις προηγούμενες ενότητες. Μπορείτε να το αντιγράψετε στο `run_ocr.py` και να το εκτελέσετε με `python run_ocr.py`.

```python
# run_ocr.py
import os
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    engine = OcrEngine()
    return engine

def load_image(engine: OcrEngine, image_path: str) -> None:
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")
    engine.setImageFromFile(image_path)

def configure_language(engine: OcrEngine) -> None:
    language_opts = LanguageOptions()
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)

def recognize_text(engine: OcrEngine) -> OcrResult:
    return engine.recognize()

def print_result(result: OcrResult) -> None:
    extracted = result.getText()
    print("\n=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===\n")

def main() -> None:
    # 1️⃣ Create the OCR engine
    ocr_engine = build_engine()

    # 2️⃣ Load the image you want to process
    image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
    load_image(ocr_engine, image_file)

    # 3️⃣ Apply language tweaks to **improve OCR accuracy**
    configure_language(ocr_engine)

    # 4️⃣ **Perform OCR on image** – this is the heavy lifting
    ocr_result = recognize_text(ocr_engine)

    # 5️⃣ **Extract text from image** and show it
    print_result(ocr_result)

if __name__ == "__main__":
    main()
```

### Γρήγορη λίστα ελέγχου επαλήθευσης

| ✅ | Στοιχείο |
|---|----------|
| ✔️ | Η μηχανή δημιουργήθηκε (`create OCR engine`) |
| ✔️ | Η εικόνα φορτώθηκε (`load image for OCR`) |
| ✔️ | Οι επιλογές γλώσσας ορίστηκαν (`improve OCR accuracy`) |
| ✔️ | Εκτελέστηκε OCR (`perform OCR on image`) |
| ✔️ | Το κείμενο εξήχθη (`extract text from image`) |

Τρέξτε το script και παρακολουθήστε την κονσόλα. Αν δείτε το μπλοκ “OCR Output” με το περιεχόμενο της αναφοράς σας, έχετε ολοκληρώσει με επιτυχία την **performed OCR on image**.

## Συνηθισμένα Προβλήματα & Πώς να τα Αποφύγετε

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|------------------|----------|
| **Θολή είσοδος** | Το μοντέλο OCR δεν μπορεί να διακρίνει χαρακτήρες | Προεπεξεργασία με OpenCV: `cv2.GaussianBlur` ή αύξηση DPI |
| **Λάθος γλώσσα** | Η προεπιλεγμένη γλώσσα μπορεί να είναι κάτι διαφορετικό από τα Αγγλικά | Κλήση `engine.setLanguage("eng")` πριν από `recognize()` |
| **Λείπουν όροι λεξικού** | Οι ειδικοί όροι του τομέα γίνονται ακατανόητοι | Προσθέστε τους μέσω `setDictionary` όπως φαίνεται στο Βήμα 3 |
| **Οι αποκλεισμένοι χαρακτήρες προκαλούν** |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}