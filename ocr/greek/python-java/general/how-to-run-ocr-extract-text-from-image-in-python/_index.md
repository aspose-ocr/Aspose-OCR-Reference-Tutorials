---
category: general
date: 2026-03-26
description: Πώς να εκτελέσετε OCR σε αρχείο PNG και να εξάγετε κείμενο από εικόνα
  με προσαρμοσμένο λεξικό για βελτιωμένη ακρίβεια OCR. Μάθετε πώς να φορτώνετε εικόνα
  για OCR γρήγορα.
draft: false
keywords:
- how to run OCR
- extract text from image
- recognize text from png
- improve OCR accuracy
- load image for OCR
language: el
og_description: Πώς να εκτελέσετε OCR σε αρχείο PNG και να εξάγετε κείμενο από εικόνα
  με προσαρμοσμένο λεξικό για βελτιωμένη ακρίβεια OCR. Οδηγός βήμα‑προς‑βήμα.
og_title: Πώς να εκτελέσετε OCR – Εξαγωγή κειμένου από εικόνα σε Python
tags:
- OCR
- Python
- Image Processing
title: Πώς να εκτελέσετε OCR – Εξαγωγή κειμένου από εικόνα σε Python
url: /el/python-java/general/how-to-run-ocr-extract-text-from-image-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εκτελέσετε OCR – Εξαγωγή Κειμένου από Εικόνα σε Python

Έχετε αναρωτηθεί ποτέ **πώς να εκτελέσετε OCR** σε μια σαρωμένη τιμολόγηση ή ένα στιγμιότυπο οθόνης και να πάρετε καθαρό, αναζητήσιμο κείμενο; Δεν είστε μόνοι. Σε πολλά έργα το σημείο συμφόρησης είναι απλώς η φόρτωση της εικόνας για OCR και η προσαρμογή της μηχανής ώστε να καταλαβαίνει λέξεις ειδικές για το πεδίο.

Σε αυτό το tutorial θα περάσουμε από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που **εξάγει κείμενο από εικόνα** αρχείων, σας δείχνει πώς να **αναγνωρίζετε κείμενο από PNG** πόρους, και ακόμη παρουσιάζει τεχνάσματα για **βελτίωση της ακρίβειας του OCR** με προσαρμοσμένα λεξικά και ειδικούς χαρακτήρες. Στο τέλος θα έχετε ένα αυτόνομο script που μπορείτε να ενσωματώσετε σε οποιοδήποτε Python codebase.

## Τι Θα Χρειαστεί

- Python 3.8+ (ο κώδικας χρησιμοποιεί type hints αλλά λειτουργεί και σε παλαιότερες εκδόσεις 3.x)
- Η βιβλιοθήκη `ocr` που συνοδεύει τη μηχανή OCR που στοχεύετε (εγκαταστήστε με `pip install ocr‑engine` – αντικαταστήστε με το πραγματικό όνομα πακέτου)
- Ένα αρχείο εικόνας (`input.png`) που θέλετε να επεξεργαστείτε
- Προαιρετικά: ένα αρχείο plain‑text (`invoice_terms.txt`) με λέξεις ειδικές για το πεδίο, μία ανά γραμμή

Χωρίς βαριές εξωτερικές εξαρτήσεις, χωρίς κλειδιά cloud API, μόνο μια τοπική μηχανή OCR.

---

## Βήμα 1: Εγκατάσταση και Εισαγωγή της Βιβλιοθήκης OCR

Πρώτα, βεβαιωθείτε ότι το πακέτο OCR είναι εγκατεστημένο. Αν χρησιμοποιείτε το υποθετικό πακέτο `ocr-engine`, τρέξτε:

```bash
pip install ocr-engine
```

Τώρα εισάγετε τις κλάσεις που θα χρειαστείτε:

```python
# Step 1: Import the OCR SDK
import ocr
from ocr import Imaging
```

> **Pro tip:** Αν εργάζεστε σε εικονικό περιβάλλον, ενεργοποιήστε το πριν την εγκατάσταση για να διατηρήσετε καθαρό το global Python σας.

## Βήμα 2: Δημιουργία Αντικειμένου OCR Engine

Η δημιουργία ενός αντικειμένου engine είναι το σημείο εισόδου για κάθε εργασία OCR. Σκεφτείτε το ως ενεργοποίηση του υλικού σαρωτή μέσω λογισμικού.

```python
# Step 2: Initialise the OCR engine
ocr_engine = ocr.OcrEngine()
```

Γιατί είναι σημαντικό: το engine κρατάει ρυθμίσεις όπως language packs, modes αναγνώρισης, και τυχόν προσαρμοσμένους πόρους που θα προσθέσετε αργότερα. Χωρίς αυτό, δεν μπορείτε να **φορτώσετε εικόνα για OCR** ή να εκτελέσετε τη διαδικασία αναγνώρισης.

## Βήμα 3: Φόρτωση της Εικόνας που Θέλετε να Αναγνωρίσετε

Εδώ πραγματικά **φορτώνουμε εικόνα για OCR**. Η μέθοδος `Imaging.Image.load()` διαβάζει το αρχείο και το μετατρέπει στη εσωτερική μορφή bitmap που περιμένει το engine.

```python
# Step 3: Load the PNG image you want to process
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Imaging.Image.load(image_path))
```

Αν έχετε JPEG ή TIFF, η ίδια μέθοδος λειτουργεί—απλώς αλλάξτε την επέκταση. Το engine ανιχνεύει αυτόματα τη μορφή.

> **Edge case:** Πολύ μεγάλες εικόνες (πάνω από 5 MP) μπορούν να προκαλέσουν αιχμές μνήμης. Σκεφτείτε να μειώσετε την ανάλυση με το Pillow πριν τη φόρτωση αν αντιμετωπίσετε προβλήματα απόδοσης.

## Βήμα 4: Παροχή Προσαρμοσμένου Λεξικού για Αύξηση Ακρίβειας

Οι περισσότερες μηχανές OCR έρχονται με γενικά μοντέλα γλώσσας. Για τιμολόγια, αποδείξεις ή νομικά έγγραφα συχνά λείπουν λέξεις. Η παροχή μιας προσαρμοσμένης λίστας λέξεων λέει στο engine «αυτοί οι όροι είναι έγκυροι, αντιμετωπίστε τους ως σωστούς».

```python
# Step 4: Attach a custom dictionary (one word per line)
custom_dict_path = "YOUR_DIRECTORY/invoice_terms.txt"
ocr_engine.set_custom_dictionary(custom_dict_path)
```

Τυπικές καταχωρήσεις μπορεί να είναι:

```
VAT
InvoiceNumber
Øre
ß
Ħ
```

Η προσθήκη αυτών βελτιώνει δραματικά το μέτρο **βελτίωση ακρίβειας OCR**—ιδιαίτερα για σύμβολα μη‑ASCII.

## Βήμα 5: Προσθήκη Ειδικών Χαρακτήρων που Δεν Καλύπτονται από το Προεπιλεγμένο Σύνολο

Αν το πεδίο σας χρησιμοποιεί σύμβολα όπως το σύμβολο του Ευρώ (€) ή το σκανδιναβικό Ø, μπορείτε να τα προσθέσετε ρητά:

```python
# Step 5: Register additional characters
ocr_engine.add_custom_characters("ØßĦ")
```

Το engine τώρα θα θεωρεί αυτά τα glyphs έγκυρα κατά τη φάση αναγνώρισης, μειώνοντας την πιθανότητα «σκουπιδόχρηστων» αποτελεσμάτων.

## Βήμα 6: Εκτέλεση της Διαδικασίας OCR και Ανάκτηση Κειμένου

Τέλος, καλέστε τον αναγνωριστή και εξάγετε το plain‑text αποτέλεσμα. Η κλήση `recognize()` επιστρέφει ένα πλούσιο αντικείμενο· για τις περισσότερες περιπτώσεις χρειαζόμαστε μόνο τη ακατέργαστη συμβολοσειρά.

```python
# Step 6: Execute OCR and print the result
result = ocr_engine.recognize()
print("=== Recognized Text ===")
print(result.get_text())
```

**Αναμενόμενο αποτέλεσμα** (συντομευμένο για συντομία):

```
=== Recognized Text ===
Invoice #12345
Date: 2026-03-01
Total: €1,250.00
VAT: 25%
...
```

Αν το αποτέλεσμα φαίνεται παραμορφωμένο, ελέγξτε ξανά ότι το προσαρμοσμένο λεξικό και οι ειδικοί χαρακτήρες έχουν φορτωθεί σωστά.

---

## Οπτική Επισκόπηση

![διάγραμμα πώς να εκτελέσετε OCR](ocr-workflow.png){alt="διάγραμμα πώς να εκτελέσετε OCR"}

Το παραπάνω διάγραμμα απεικονίζει τη ροή από τη φόρτωση μιας εικόνας μέχρι την απόκτηση καθαρού κειμένου, επισημαίνοντας πού μπορείτε να ενσωματώσετε προσαρμοσμένα λεξικά και σύνολα χαρακτήρων.

---

## Συχνές Ερωτήσεις & Παγίδες

### Λειτουργεί αυτό με PDF πολλαπλών σελίδων;

Ναι—απλώς μετατρέψτε κάθε σελίδα σε PNG (χρησιμοποιώντας `pdf2image` ή παρόμοιο) και τροφοδοτήστε τις διαδοχικά στην ίδια παρουσία `ocr_engine`. Το engine επεξεργάζεται κάθε εικόνα ανεξάρτητα, οπότε θα λάβετε μια λίστα συμβολοσειρών που μπορείτε να ενώσετε.

### Τι γίνεται αν η εικόνα είναι περιστραμμένη;

Οι περισσότερες σύγχρονες μηχανές OCR ανιχνεύουν αυτόματα την προσανατολισμό, αλλά μπορείτε να εξαναγκάσετε περιστροφή με:

```python
ocr_engine.set_image(Imaging.Image.load(image_path).rotate(90))
```

### Πώς να διαχειριστείτε γλώσσες εκτός της Αγγλικής;

Αλλάξτε το μοντέλο γλώσσας πριν φορτώσετε την εικόνα:

```python
ocr_engine.set_language("de")  # German
```

Βεβαιωθείτε ότι το αντίστοιχο language pack είναι εγκατεστημένο.

---

## Πλήρες Script – Έτοιμο για Αντιγραφή & Επικόλληση

Παρακάτω βρίσκεται ολόκληρο το πρόγραμμα, έτοιμο να τρέξει αφού αντικαταστήσετε τις διαδρομές placeholder.

```python
#!/usr/bin/env python3
"""
How to Run OCR – Complete example that extracts text from a PNG,
uses a custom dictionary, and adds special characters for better accuracy.
"""

# Install the OCR package first:
# pip install ocr-engine

import ocr
from ocr import Imaging

def main():
    # 1️⃣ Initialise the OCR engine
    ocr_engine = ocr.OcrEngine()

    # 2️⃣ Load the image you want to recognize
    image_path = "YOUR_DIRECTORY/input.png"      # <-- change this
    ocr_engine.set_image(Imaging.Image.load(image_path))

    # 3️⃣ Provide a custom dictionary (optional but recommended)
    dict_path = "YOUR_DIRECTORY/invoice_terms.txt"   # one word per line
    ocr_engine.set_custom_dictionary(dict_path)

    # 4️⃣ Add any special characters not covered by the default set
    ocr_engine.add_custom_characters("ØßĦ")   # e.g., currency symbols

    # 5️⃣ Run the OCR process
    result = ocr_engine.recognize()

    # 6️⃣ Output the recognized text
    print("=== Recognized Text ===")
    print(result.get_text())

if __name__ == "__main__":
    main()
```

Τρέξτε το με:

```bash
python run_ocr.py
```

Θα πρέπει να δείτε το εξαγόμενο κείμενο να εμφανίζεται στην κονσόλα. Από εκεί μπορείτε να το γράψετε σε αρχείο, να το τροφοδοτήσετε σε βάση δεδομένων, ή να το περάσετε σε downstream pipelines NLP.

---

## Ανακεφαλαίωση & Επόμενα Βήματα

Καλύψαμε **πώς να εκτελέσετε OCR** σε PNG, πώς να **εξάγετε κείμενο από εικόνα**, και παρουσιάσαμε πρακτικούς τρόπους για **αναγνώριση κειμένου από PNG** ενώ **βελτιώνουμε την ακρίβεια OCR** με λεξικά και προσαρμοσμένους χαρακτήρες.

Επόμενα, σκεφτείτε:

- **Batch processing:** Επανάληψη πάνω σε έναν φάκελο εικόνων.
- **Post‑processing:** Χρήση regex για εξαγωγή αριθμών τιμολογίων ή ημερομηνιών.
- **Integration:** Σύνδεση του script με ένα Flask API για υπηρεσίες OCR κατ' απαίτηση.

Αν σας ενδιαφέρουν πιο προχωρημένα θέματα, ρίξτε μια ματιά σε tutorials για **φόρτωση εικόνας για OCR** με προεπεξεργασία OpenCV, ή εμβαθύνετε σε deep‑learning μοντέλα OCR όπως το Tesseract 4+ με LSTM layers.

---

### Συνεχίστε να Πειραματίζεστε!

Δοκιμάστε να αντικαταστήσετε το `invoice_terms.txt` με μια λίστα ιατρικής ορολογίας, προσθέστε ελληνικούς χαρακτήρες, ή τροφοδοτήστε το engine με μια χαμηλής ανάλυσης φωτογραφία για να δείτε πόσο μακριά μπορεί να φτάσει η ακρίβεια. Όσο περισσότερο πειραματίζεστε, τόσο καλύτερα θα κατανοήσετε τις ανταλλαγές μεταξύ προεπεξεργασίας, προσαρμοσμένων λεξιλογίων και ρυθμίσεων του engine.

Καλό κώδικα, και εύχομαι τα αποτελέσματα OCR σας να είναι πάντα καθαρά!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}