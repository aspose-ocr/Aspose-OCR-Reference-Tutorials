---
category: general
date: 2026-03-26
description: 'Python OCR tutorial: μάθετε πώς να εξάγετε κείμενο από εικόνα, να φορτώσετε
  εικόνα για OCR και να αναγνωρίσετε κείμενο από απόδειξη χρησιμοποιώντας το Aspose
  OCR σε λίγα μόνο βήματα.'
draft: false
keywords:
- python ocr tutorial
- extract text from image
- load image for ocr
- perform ocr in python
- recognize text from receipt
language: el
og_description: 'Python OCR tutorial: γρήγορα μάθετε να εξάγετε κείμενο από εικόνα,
  φορτώστε την εικόνα για OCR και αναγνωρίστε κείμενο από απόδειξη με το Aspise OCR.'
og_title: Python OCR tutorial – Εξαγωγή κειμένου από εικόνα
tags:
- OCR
- Aspose
- Python
title: Python OCR tutorial – Εξαγωγή κειμένου από εικόνα με Aspose
url: /el/python-java/general/python-ocr-tutorial-extract-text-from-image-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR tutorial – Extract Text from Image with Aspose

Έχετε αναρωτηθεί ποτέ πώς να εξάγετε το κείμενο από μια θολή απόδειξη ή μια σαρωμένη φόρμα χωρίς να περνάτε ώρες γράφοντας προσαρμοσμένα regex; Δεν είστε μόνοι. Σε αυτό το **python ocr tutorial** θα περάσουμε από τη φόρτωση μιας εικόνας για OCR, την εκτέλεση OCR σε Python και, τέλος, την αναγνώριση κειμένου από αρχεία απόδειξης χρησιμοποιώντας τη βιβλιοθήκη Aspose OCR.  

Στο τέλος αυτού του οδηγού θα έχετε ένα έτοιμο‑για‑εκτέλεση script που διαβάζει οποιαδήποτε υποστηριζόμενη μορφή εικόνας, εξάγει το κειμενικό περιεχόμενο και το εκτυπώνει στην κονσόλα. Χωρίς εξωτερικές υπηρεσίες, χωρίς κλειδιά API—απλώς καθαρό Python και μια ισχυρή μηχανή OCR.  

## What You’ll Need

- Python 3.8 ή νεότερη (ο κώδικας χρησιμοποιεί type hints, οπότε ένας πρόσφατος διερμηνέας είναι καλύτερος)
- Πακέτο `asposeocrjava` εγκατεστημένο μέσω `pip install aspose-ocr`
- Ένα δείγμα εικόνας – για παράδειγμα `receipt_noisy.jpg` που περιέχει μια τυπική απόδειξη καταστήματος
- (Προαιρετικά) Ένα εικονικό περιβάλλον για να διατηρήσετε τις εξαρτήσεις οργανωμένες

Αν έχετε τσεκάρει όλα τα παραπάνω, μπορούμε να περάσουμε κατευθείαν στον κώδικα.  

## Step 1: Install and Import Aspose OCR Classes

Πρώτα, βεβαιωθείτε ότι το πακέτο Aspose OCR είναι διαθέσιμο. Στη συνέχεια εισάγετε τις κλάσεις που θα χρειαστείτε.

```python
# Install the package (run once)
# pip install aspose-ocr

# Import the required Aspose OCR modules
import asposeocrjava as ocr
from asposeocrjava import OcrEngineMode, OcrEngine, OcrResult
```

**Why this matters:** Η εισαγωγή μόνο των απαραίτητων συμβόλων διατηρεί καθαρό το namespace και δείχνει στον διερμηνέα ποια μέρη της βιβλιοθήκης χρησιμοποιούμε πραγματικά. Επίσης συντομεύει τις επόμενες γραμμές κώδικα, κάνοντας τον οδηγό πιο εύκολο στην παρακολούθηση.

> **Pro tip:** Αν χρησιμοποιείτε Jupyter notebook, προσθέστε `!` στην αρχή της γραμμής εγκατάστασης για να την εκτελέσετε μέσα στο κελί.

## Step 2: Create the OCR Engine and Enable Deep‑Learning Mode

Η Aspose προσφέρει διάφορες λειτουργίες μηχανής. Για τις περισσότερες πραγματικές αποδείξεις, το μοντέλο deep‑learning παρέχει την υψηλότερη ακρίβεια, ειδικά σε θορυβώδεις σαρώσεις.

```python
# Initialise the OCR engine
ocr_engine = OcrEngine()

# Switch to deep‑learning mode for better accuracy on complex images
ocr_engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)
```

**Why deep‑learning?** Η παραδοσιακή OCR με κανόνες μπορεί να δυσκολευτεί με χαρακτήρες χαμηλής αντίθεσης ή παραμορφωμένους. Το μοντέλο deep‑learning, εκπαιδευμένο σε εκατομμύρια γλύφους, προσαρμόζεται καλύτερα στις παραλλαγές—ακριβώς αυτό που χρειάζεστε όταν *perform OCR in Python* σε αποδείξεις τραβηγμένες με τη συσκευή σας.

## Step 3: Load Image for OCR

Τώρα φορτώνουμε **image for OCR**. Η Aspose.Imaging υποστηρίζει PNG, JPEG, BMP, TIFF και άλλα, ώστε να μπορείτε να την δείξετε σε σχεδόν οποιαδήποτε φωτογραφία εγγράφου.

```python
# Load the image (replace the path with your own file)
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/receipt_noisy.jpg")

# Attach the image to the OCR engine
ocr_engine.set_image(input_image)
```

**Common pitfall:** Η παράλειψη του `set_image` στο engine οδηγεί σε `NullReferenceException` κατά την εκτέλεση. Πάντα καλέστε `set_image` μετά τη φόρτωση του αρχείου.

## Step 4: Perform OCR and Extract Text

Με το engine έτοιμο και την εικόνα συνδεδεμένη, μπορούμε τελικά **perform OCR in Python** και να ανακτήσουμε το κειμενικό αποτέλεσμα.

```python
# Run the recognition process
ocr_result: OcrResult = ocr_engine.recognize()

# Extract plain text from the result object
recognized_text = ocr_result.get_text()
```

Η μέθοδος `recognize()` επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει όχι μόνο το ακατέργαστο κείμενο, αλλά και βαθμολογίες εμπιστοσύνης, περιοριστικά πλαίσια και πληροφορίες γλώσσας. Για μια γρήγορη περίπτωση **extract text from image** χρειαζόμαστε μόνο το `get_text()`.

## Step 5: Display the Recognized Text

Ας δούμε τι διάβασε το engine από την απόδειξη.

```python
print("Recognized text:\n", recognized_text)
```

Τυπική έξοδος μοιάζει με:

```
Recognized text:
   Store XYZ
   04/26/2026  14:32
   Item A   2.99
   Item B   5.49
   TOTAL    8.48
   THANK YOU!
```

Αν η έξοδος περιέχει ακατάλληλους χαρακτήρες, σκεφτείτε προεπεξεργασία της εικόνας (π.χ. αύξηση αντίθεσης ή εφαρμογή φίλτρου deskew) πριν τη φορτώσετε στο OCR engine. Η Aspose.Imaging προσφέρει πλήρη σειρά εργαλείων βελτίωσης εικόνας που μπορείτε να συνδυάσετε.

## Handling Edge Cases & Tips for Better Accuracy

### 1. Dealing with Extremely Noisy Receipts
Αν η απόδειξη είναι πολύ λασπωμένη, μπορείτε να αλλάξετε σε λειτουργία `OcrEngineMode.HIGH_SPEED` για πιο γρήγορη, αν και λιγότερο ακριβή, επεξεργασία, και στη συνέχεια να τρέξετε δεύτερο πέρασμα σε `DEEP_LEARNING` στην καθαρισμένη εικόνα.

```python
ocr_engine.set_engine_mode(OcrEngineMode.HIGH_SPEED)
# ... run first pass, then...
ocr_engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)
# ... run second pass on the same image
```

### 2. Specifying Language
Από προεπιλογή η Aspose προσπαθεί να εντοπίσει αυτόματα τη γλώσσα. Για αγγλικές αποδείξεις μπορείτε να την κλειδώσετε:

```python
ocr_engine.set_language("eng")
```

### 3. Memory Management
Όταν επεξεργάζεστε πολλές εικόνες σε βρόχο, απελευθερώστε ρητά τους πόρους:

```python
input_image.dispose()
ocr_engine.dispose()
```

### 4. Saving OCR Results to a File
Μερικές φορές χρειάζεται το εξαγόμενο κείμενο να αποθηκευτεί για μετέπειτα ανάλυση.

```python
with open("receipt_output.txt", "w", encoding="utf-8") as f:
    f.write(recognized_text)
```

## Full Working Example

Παρακάτω βρίσκεται το πλήρες script που ενώνει όλα τα παραπάνω. Αντιγράψτε‑και‑επικολλήστε το σε ένα αρχείο με όνομα `receipt_ocr.py`, προσαρμόστε τη διαδρομή της εικόνας και τρέξτε `python receipt_ocr.py`.

```python
# receipt_ocr.py
# -------------------------------------------------
# Complete Python OCR tutorial using Aspose OCR
# -------------------------------------------------

# 1️⃣ Install the package (run once):
# pip install aspose-ocr

import asposeocrjava as ocr
from asposeocrjava import OcrEngineMode, OcrEngine, OcrResult

def main():
    # 2️⃣ Initialise engine in deep‑learning mode
    engine = OcrEngine()
    engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)

    # 3️⃣ Load your receipt image
    image_path = "YOUR_DIRECTORY/receipt_noisy.jpg"   # <-- change this
    img = ocr.Imaging.Image.load(image_path)
    engine.set_image(img)

    # 4️⃣ Recognise text
    result: OcrResult = engine.recognize()
    text = result.get_text()

    # 5️⃣ Output the result
    print("=== Recognized text from receipt ===")
    print(text)

    # Optional: write to a file
    with open("receipt_output.txt", "w", encoding="utf-8") as out_file:
        out_file.write(text)

    # Clean up resources
    img.dispose()
    engine.dispose()

if __name__ == "__main__":
    main()
```

Η εκτέλεση του script θα πρέπει να εμφανίσει το περιεχόμενο της απόδειξης στην κονσόλα και επίσης να δημιουργήσει το `receipt_output.txt` με τα ίδια δεδομένα.

![Python OCR tutorial – sample receipt output](https://example.com/receipt_output.png "python ocr tutorial example")

*Κείμενο alt εικόνας:* **python ocr tutorial – sample receipt output**

## Recap & Next Steps

Μόλις περάσαμε από ένα **python ocr tutorial** που δείχνει πώς να **load image for OCR**, **perform OCR in Python**, και τέλος **recognize text from receipt** χρησιμοποιώντας την Aspose. Τα κύρια σημεία είναι:

- Επιλέξτε τη σωστή λειτουργία engine (deep‑learning για ακρίβεια)
- Πάντα συνδέετε την εικόνα πριν καλέσετε `recognize()`
- Χρησιμοποιήστε το αντικείμενο `OcrResult` για να εξάγετε καθαρό κείμενο, έπειτα αποθηκεύστε ή επεξεργαστείτε το όπως χρειάζεται

Τι ακολουθεί; Σκεφτείτε να συνδυάσετε φίλτρα Aspose Imaging για βελτίωση χαμηλής αντίθεσης σαρώσεων, ή να ενσωματώσετε το script σε ένα Flask API ώστε να μπορείτε να ανεβάζετε αποδείξεις μέσω web φόρμας. Μπορείτε επίσης να εξερευνήσετε την εξαγωγή των δεδομένων OCR σε CSV για αυτοματοποίηση λογιστικής.

Έχετε ερωτήσεις για επεξεργασία πολυ‑σελίδων PDF ή μη‑λατινικών γραφών; Αφήστε ένα σχόλιο—χάρηκα να βοηθήσω!  

**Ready to level up your document automation?** Πάρτε τον κώδικα, πειραματιστείτε με διαφορετικές εικόνες, και αφήστε το OCR engine να κάνει τη βαριά δουλειά. Καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}