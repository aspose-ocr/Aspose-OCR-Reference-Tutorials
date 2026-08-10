---
category: general
date: 2026-04-26
description: Αναγνωρίστε χειρόγραφο κείμενο χρησιμοποιώντας τη μηχανή OCR της Python.
  Μάθετε πώς να εξάγετε κείμενο από εικόνα, να ενεργοποιήσετε τη λειτουργία χειρογράφου
  και να διαβάζετε γρήγορα χειρόγραφες σημειώσεις.
draft: false
keywords:
- recognize handwritten text
- extract text from image
- read handwritten notes
- turn on handwritten mode
- create OCR engine python
language: el
og_description: Αναγνωρίστε χειρόγραφο κείμενο με την Python. Αυτός ο οδηγός δείχνει
  πώς να εξάγετε κείμενο από εικόνα, να ενεργοποιήσετε τη λειτουργία χειρογράφου και
  να διαβάσετε χειρόγραφες σημειώσεις χρησιμοποιώντας μια απλή μηχανή OCR.
og_title: Αναγνώριση χειρόγραφου κειμένου σε Python – Πλήρης Οδηγός OCR
tags:
- OCR
- Python
- Handwriting Recognition
title: Αναγνώριση χειρόγραφου κειμένου σε Python – Οδηγός Μηχανής OCR
url: /el/python/general/recognize-handwritten-text-in-python-ocr-engine-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση χειρόγραφου κειμένου σε Python – Οδηγός Μηχανής OCR

Έχετε ποτέ χρειαστεί να **αναγνωρίσετε χειρόγραφο κείμενο** αλλά νιώσατε κολλημένοι στο “πού ξεκινάω;”; Δεν είστε μόνοι. Είτε ψηφιοποιείτε σημειώσεις από συναντήσεις είτε εξάγετε δεδομένα από σαρωμένη φόρμα, η λήψη αξιόπιστου αποτελέσματος OCR μπορεί να μοιάζει με κυνήγι μονόκερου.  

Καλά νέα: με λίγες μόνο γραμμές Python μπορείτε να **εξάγετε κείμενο από εικόνα** αρχεία, **ενεργοποιήσετε τη λειτουργία χειρογράφου**, και τελικά **διαβάσετε χειρόγραφες σημειώσεις** χωρίς να ψάχνετε obscure βιβλιοθήκες. Σε αυτόν τον οδηγό θα περάσουμε από όλη τη διαδικασία, από τη ρύθμιση τύπου **create OCR engine python** μέχρι την εκτύπωση του αποτελέσματος στην οθόνη.

## Τι Θα Μάθετε

- Πώς να δημιουργήσετε ένα στιγμιότυπο **create OCR engine python** χρησιμοποιώντας το πακέτο `ocr`.  
- Ποια ρύθμιση γλώσσας σας παρέχει ενσωματωμένη υποστήριξη χειρογράφου.  
- Η ακριβής κλήση για **turn on handwritten mode** ώστε η μηχανή να γνωρίζει ότι αντιμετωπίζει πλάγιο κείμενο.  
- Πώς να τροφοδοτήσετε μια εικόνα σημείωσης και να **recognize handwritten text** από αυτήν.  
- Συμβουλές για διαχείριση διαφορετικών μορφών εικόνας, αντιμετώπιση κοινών προβλημάτων, και επέκταση της λύσης.

Χωρίς περιττά, χωρίς “δείτε την τεκμηρίωση” αδιέξοδα—απλώς ένα πλήρες, εκτελέσιμο script που μπορείτε να αντιγράψετε‑επικολλήσετε και να δοκιμάσετε σήμερα.

## Προαπαιτούμενα

Πριν βουτήξουμε, βεβαιωθείτε ότι έχετε:

1. Python 3.8+ εγκατεστημένο (ο κώδικας χρησιμοποιεί f‑strings).  
2. Τη θεωρητική βιβλιοθήκη `ocr` (`pip install ocr‑engine` – αντικαταστήστε με το πραγματικό όνομα πακέτου που χρησιμοποιείτε).  
3. Ένα καθαρό αρχείο εικόνας μιας χειρόγραφης σημείωσης (λειτουργούν JPEG, PNG ή TIFF).  
4. Μια μέτρια δόση περιέργειας—τα υπόλοιπα καλύπτονται παρακάτω.

> **Pro tip:** Αν η εικόνα σας είναι θορυβώδης, εκτελέστε ένα γρήγορο βήμα προεπεξεργασίας με το Pillow (π.χ., `Image.open(...).convert('L')`) πριν τη στείλετε στη μηχανή OCR. Συχνά βελτιώνει την ακρίβεια.

## Πώς να αναγνωρίσετε χειρόγραφο κείμενο με Python

Παρακάτω είναι το πλήρες script που **creates OCR engine python** αντικείμενα, τα ρυθμίζει για χειρόγραφο και εκτυπώνει το εξαγόμενο κείμενο. Αποθηκεύστε το ως `handwriting_ocr.py` και εκτελέστε το από το τερματικό σας.

```python
# handwriting_ocr.py
import ocr                     # The OCR library that provides OcrEngine
import os

def main():
    # Step 1: Create an OCR engine instance
    # This is the core object that will do all the heavy lifting.
    ocr_engine = ocr.OcrEngine()

    # Step 2: Choose a language that includes handwritten support.
    # EXTENDED_LATIN covers most Western alphabets and knows how to
    # handle cursive strokes.
    ocr_engine.set_language(ocr.Language.EXTENDED_LATIN)

    # Step 3: Turn on handwritten mode.
    # Without this flag the engine assumes printed text and will miss
    # most of the nuances in a scribble.
    ocr_engine.enable_handwritten_mode(True)

    # Step 4: Define the path to your handwritten image.
    # Replace the placeholder with the actual location of your file.
    image_path = os.path.join("YOUR_DIRECTORY", "handwritten_note.jpg")

    # Basic validation – makes debugging easier.
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Step 5: Recognize text from the image.
    # The recognize_image method returns a result object that holds
    # both the raw text and confidence scores.
    handwritten_result = ocr_engine.recognize_image(image_path)

    # Step 6: Display the extracted text.
    # This is where you finally **read handwritten notes** programmatically.
    print("=== Extracted Text ===")
    print(handwritten_result.text)

if __name__ == "__main__":
    main()
```

### Αναμενόμενο Αποτέλεσμα

Όταν το script εκτελεστεί επιτυχώς, θα δείτε κάτι όπως:

```
=== Extracted Text ===
Meeting notes:
- Discuss quarterly targets
- Assign tasks to Alice & Bob
- Follow‑up email by Friday
```

Αν η μηχανή OCR δεν μπορεί να εντοπίσει χαρακτήρες, το πεδίο `text` θα είναι μια κενή συμβολοσειρά. Σε αυτήν την περίπτωση, ελέγξτε ξανά την ποιότητα της εικόνας ή δοκιμάστε σάρωση υψηλότερης ανάλυσης.

## Εξήγηση Βήμα‑προς‑Βήμα

### Βήμα 1 – **create OCR engine python** στιγμιότυπο

Η κλάση `OcrEngine` είναι το σημείο εισόδου. Σκεφτείτε το σαν ένα κενό σημειωματάριο—δεν συμβαίνει τίποτα μέχρι να του πείτε ποια γλώσσα να περιμένει και αν αντιμετωπίζει χειρόγραφο.

### Βήμα 2 – Επιλέξτε γλώσσα που υποστηρίζει χειρόγραφο

`ocr.Language.EXTENDED_LATIN` δεν είναι μόνο “English”. Συμπεριλαμβάνει ένα σύνολο λατινικών γραφών και, κρίσιμα, μοντέλα εκπαιδευμένα σε δείγματα πλάγιου κειμένου. Η παράλειψη αυτού του βήματος συχνά οδηγεί σε ακατανόητο αποτέλεσμα επειδή η μηχανή προεπιλέγει μοντέλο τυπωμένου κειμένου.

### Βήμα 3 – **turn on handwritten mode**

Καλώντας `enable_handwritten_mode(True)` ενεργοποιείται μια εσωτερική σημαία. Η μηχανή τότε μεταβαίνει στο νευρωνικό δίκτυό της που είναι ρυθμισμένο για την ακανόνιστη απόσταση και τις μεταβλητές πλάτους γραμμής που βλέπετε σε πραγματικές σημειώσεις. Η παράλειψη αυτής της γραμμής είναι κοινό λάθος· η μηχανή θα θεωρήσει τις σημειώσεις σας ως θόρυβο.

### Βήμα 4 – Τροφοδοτήστε την εικόνα και **recognize handwritten text**

`recognize_image` κάνει τη βαριά δουλειά: προεπεξεργάζεται το bitmap, το τρέχει μέσω του μοντέλου χειρογράφου, και επιστρέφει ένα αντικείμενο με το χαρακτηριστικό `text`. Μπορείτε επίσης να ελέγξετε το `handwritten_result.confidence` αν χρειάζεστε μέτρο ποιότητας.

### Βήμα 5 – Εκτυπώστε το αποτέλεσμα και **read handwritten notes**

`print(handwritten_result.text)` είναι ο πιο απλός τρόπος να επαληθεύσετε ότι έχετε επιτυχώς **extract text from image**. Σε παραγωγή πιθανότατα θα αποθηκεύσετε τη συμβολοσειρά σε βάση δεδομένων ή θα τη μεταβιβάσετε σε άλλη υπηρεσία.

## Διαχείριση Περιπτώσεων Άκρων & Κοινών Παραλλαγών

| Κατάσταση | Τι να κάνετε |
|-----------|--------------|
| **Η εικόνα είναι περιστραμμένη** | Χρησιμοποιήστε το Pillow για περιστροφή (`Image.rotate(angle)`) πριν καλέσετε το `recognize_image`. |
| **Χαμηλή αντίθεση** | Μετατρέψτε σε κλίμακα του γκρι και εφαρμόστε προσαρμοστική διόρθωση κατωφλίου (`Image.point(lambda p: p > 128 and 255)`). |
| **Πολλές σελίδες** | Κάντε βρόχο πάνω σε μια λίστα διαδρομών αρχείων και συνενώστε τα αποτελέσματα. |
| **Μη‑λατινικά σενάρια** | Αντικαταστήστε το `EXTENDED_LATIN` με `ocr.Language.CHINESE` (ή κατάλληλο) και διατηρήστε το `enable_handwritten_mode(True)`. |
| **Ανησυχίες απόδοσης** | Επαναχρησιμοποιήστε το ίδιο στιγμιότυπο `ocr_engine` για πολλές εικόνες· η εκκίνηση του κάθε φορά προσθέτει επιβάρυνση. |

### Συμβουλή για χρήση μνήμης

Αν επεξεργάζεστε εκατοντάδες σημειώσεις σε παρτίδα, καλέστε `ocr_engine.dispose()` μετά το τέλος. Απελευθερώνει τους εγγενείς πόρους που μπορεί να κρατά το Python wrapper.

## Σύντομη Οπτική Ανασκόπηση

![recognize handwritten text example](https://example.com/handwritten-note.png "recognize handwritten text example")

*Η παραπάνω εικόνα δείχνει μια τυπική χειρόγραφη σημείωση που το script μας μπορεί να μετατρέψει σε απλό κείμενο.*

## Πλήρες Παράδειγμα Εργασίας (Script ενός Αρχείου)

Για όσους αγαπούν την απλότητα του copy‑paste, εδώ είναι ολόκληρο το script ξανά χωρίς τα επεξηγηματικά σχόλια:

```python
import ocr, os

ocr_engine = ocr.OcrEngine()
ocr_engine.set_language(ocr.Language.EXTENDED_LATIN)
ocr_engine.enable_handwritten_mode(True)

img = os.path.join("YOUR_DIRECTORY", "handwritten_note.jpg")
if not os.path.isfile(img):
    raise FileNotFoundError(f"Image not found: {img}")

result = ocr_engine.recognize_image(img)
print("=== Extracted Text ===")
print(result.text)
```

Τρέξτε το με:

```bash
python handwriting_ocr.py
```

Τώρα θα πρέπει να δείτε το αποτέλεσμα **recognize handwritten text** στην κονσόλα σας.

## Συμπέρασμα

Μόλις καλύψαμε όλα όσα χρειάζεστε για να **recognize handwritten text** σε Python—από μια φρέσκια κλήση **create OCR engine python**, επιλογή της σωστής γλώσσας, **turn on handwritten mode**, και τελικά **extract text from image** για **read handwritten notes**.  

Σε ένα ενιαίο, αυτόνομο script μπορείτε να μετατρέψετε μια θολή φωτογραφία μιας σημείωσης συνάντησης σε καθαρό, αναζητήσιμο κείμενο. Στη συνέχεια, σκεφτείτε να τροφοδοτήσετε το αποτέλεσμα σε μια αλυσίδα επεξεργασίας φυσικής γλώσσας, να το αποθηκεύσετε σε ευρετήριο αναζήτησης, ή ακόμη να το στείλετε πίσω σε υπηρεσία μεταγραφής για δημιουργία φωνητικού overlay.

### Πού να Πηγαίνετε Από Εδώ;

- **Batch processing:** Τυλίξτε το script σε βρόχο για να διαχειριστείτε έναν φάκελο σκαναρισμάτων.  
- **Confidence filtering:** Χρησιμοποιήστε το `result.confidence` για να απορρίψετε αναγνώσεις χαμηλής ποιότητας.  
- **Alternative libraries:** Αν το `ocr` δεν είναι τέλειο, εξερευνήστε το `pytesseract` με `--psm 13` για λειτουργία χειρογράφου.  
- **UI integration:** Συνδυάστε με Flask ή FastAPI για να προσφέρετε μια υπηρεσία ανεβάσματος μέσω web.

Έχετε ερωτήσεις σχετικά με συγκεκριμένη μορφή εικόνας ή χρειάζεστε βοήθεια στη ρύθμιση του μοντέλου; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}