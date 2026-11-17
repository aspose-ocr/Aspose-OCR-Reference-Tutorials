---
category: general
date: 2026-03-18
description: Πώς να χρησιμοποιήσετε OCR για την εξαγωγή κειμένου από εικόνες – ένας
  γρήγορος οδηγός για την αναγνώριση κειμένου από αρχεία PNG και τη φόρτωση εικόνων
  για OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from png
- how to extract text
- load image for OCR
language: el
og_description: Πώς να χρησιμοποιήσετε OCR για την εξαγωγή κειμένου από εικόνες –
  μάθετε να αναγνωρίζετε κείμενο από PNG, να φορτώνετε εικόνα για OCR και να εξάγετε
  κείμενο με ένα απλό script Python.
og_title: 'Πώς να χρησιμοποιήσετε OCR: Εξαγωγή κειμένου από εικόνες σε Python'
tags:
- OCR
- Python
- Image Processing
title: 'Πώς να χρησιμοποιήσετε OCR: Εξαγωγή κειμένου από εικόνες σε Python'
url: /el/python-java/general/how-to-use-ocr-extract-text-from-images-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε OCR: Εξαγωγή Κειμένου από Εικόνες σε Python

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε OCR** όταν έχετε ένα ακατάστατο στιγμιότυπο οθόνης ή μια σαρωμένη απόδειξη; Δεν είστε μόνοι—οι προγραμματιστές χρειάζεται συνεχώς να εξάγουν αναγνώσιμο κείμενο από εικόνες, ειδικά PNG που προέρχονται από κινητές εφαρμογές ή ανεβάσματα στο web. Σε αυτό το tutorial θα περάσουμε από ένα πλήρες, εκτελέσιμο παράδειγμα που σας δείχνει πώς να **εξάγετε κείμενο από εικόνα** αρχεία, **αναγνωρίσετε κείμενο από PNG** περιουσιακά στοιχεία, και ακόμη **φορτώσετε εικόνα για OCR** με λίγες μόνο γραμμές Python.

Θα καλύψουμε τα πάντα, από την εγκατάσταση της σωστής βιβλιοθήκης μέχρι τη διαχείριση πολυγλωσσικών εγγράφων, ώστε στο τέλος να ξέρετε ακριβώς *πώς να εξάγετε κείμενο* από οποιαδήποτε εικόνα που θα περάσετε στη μηχανή. Χωρίς ασαφείς αναφορές, μόνο μια σαφής, βήμα‑βήμα λύση που μπορείτε να αντιγράψετε‑επικολλήσετε και να εκτελέσετε.

## Τι Θα Μάθετε

1. Ρυθμίστε μια ελαφριά μηχανή OCR (χωρίς απαιτήσεις βαρέων εξαρτήσεων).  
2. Φορτώστε ένα αρχείο εικόνας—συγκεκριμένα ένα PNG—στη μηχανή.  
3. Ενεργοποιήστε την αυτόματη ανίχνευση γλώσσας ώστε η μηχανή να μπορεί να διαχειρίζεται πολυγλωσσικό περιεχόμενο.  
4. Εκτελέστε τη διαδικασία αναγνώρισης και λάβετε το αποτέλεσμα ως απλό κείμενο.  
5. Προσαρμόστε τη ροή εργασίας για ειδικές περιπτώσεις όπως ελλιπή αρχεία ή μη υποστηριζόμενες μορφές.

Αν είστε άνετοι με το βασικό Python, είστε έτοιμοι. Δεν απαιτείται προγενέστερη εμπειρία OCR, αν και μια γρήγορη ματιά στην τεκμηρίωση της βιβλιοθήκης δεν βλάπτει.

---

![Πώς να χρησιμοποιήσετε OCR σε εικόνα PNG](placeholder.png "Πώς να χρησιμοποιήσετε OCR σε εικόνα PNG – οδηγός βήμα-βήμα")

## Πώς να Χρησιμοποιήσετε OCR – Φόρτωση Εικόνας και Αναγνώριση Κειμένου {#how-to-use-ocr}

### Βήμα 1: Εγκαταστήστε τη βιβλιοθήκη OCR

Πρώτα απ' όλα, χρειάζεστε ένα πακέτο Python που παρέχει μια κλάση `OcrEngine`. Για το σκοπό αυτού του tutorial θα χρησιμοποιήσουμε το φανταστικό αλλά εικονοποιητικό πακέτο **SimpleOCR**, το οποίο μπορείτε να εγκαταστήσετε μέσω pip:

```bash
pip install simple-ocr
```

> **Pro tip:** Αν εργάζεστε σε ένα εικονικό περιβάλλον (συγκεκριμένα συνιστάται), ενεργοποιήστε το πριν τρέξετε την εντολή εγκατάστασης. Αυτό διατηρεί τις εξαρτήσεις του έργου σας τακτοποιημένες.

### Βήμα 2: Εισάγετε τη μηχανή και δημιουργήστε μια παρουσία

Η δημιουργία της μηχανής είναι τόσο απλή όσο η κλήση του κατασκευαστή της. Σκεφτείτε τη μηχανή ως το “εγκέφαλο” που θα επεξεργαστεί αργότερα την εικόνα που θα της δώσετε.

```python
# Step 2: Import and instantiate the OCR engine
from simple_ocr import OcrEngine

# Create a fresh engine instance – this allocates internal buffers
engine = OcrEngine()
```

Γιατί δημιουργούμε μια νέα παρουσία κάθε φορά; Απομόνωση. Μια φρέσκια μηχανή εγγυάται ότι δεν υπάρχει υπολειπόμενη κατάσταση από προηγούμενη εκτέλεση που να μολύνει την τρέχουσα αναγνώριση, κάτι που είναι κρίσιμο όταν επεξεργάζεστε πολλά αρχεία σε παρτίδα.

### Βήμα 3: Φορτώστε την εικόνα που θέλετε να επεξεργαστείτε

Τώρα στην πραγματικότητα **φορτώνουμε εικόνα για OCR**. Η μέθοδος `setImageFromFile` δέχεται μια διαδρομή προς οποιαδήποτε ραστερική εικόνα· θα την κατευθύνουμε σε ένα PNG που ονομάζεται `mixed_doc.png`.

```python
# Step 3: Load the PNG image you want to read
image_path = "YOUR_DIRECTORY/mixed_doc.png"
engine.setImageFromFile(image_path)
```

Αν το αρχείο δεν βρεθεί, το `SimpleOCR` ρίχνει ένα σαφές `FileNotFoundError`. Μπορείτε να το πιάσετε για να παρέχετε ένα φιλικό μήνυμα σφάλματος:

```python
try:
    engine.setImageFromFile(image_path)
except FileNotFoundError:
    print(f"❗️ Unable to locate '{image_path}'. Check the path and try again.")
    raise
```

### Βήμα 4: Ενεργοποιήστε την αυτόματη ανίχνευση γλώσσας

Οι περισσότερες σύγχρονες μηχανές OCR έρχονται με πακέτα γλώσσας. Με το να περάσουμε `"multilingual"` λέμε στη μηχανή να ανιχνεύσει το κείμενο και να επιλέξει αυτόματα το σωστό μοντέλο γλώσσας. Αυτό είναι ιδιαίτερα χρήσιμο όταν το PNG σας περιέχει ένα μείγμα αγγλικών και ισπανικών, για παράδειγμα.

```python
# Step 4: Turn on auto‑language detection (covers all installed packs)
engine.setLanguage("multilingual")
```

Αν γνωρίζετε τη γλώσσα εκ των προτέρων, μπορείτε να αντικαταστήσετε το `"multilingual"` με μια συγκεκριμένη τοπική ρύθμιση όπως `"eng"` ή `"spa"` για να επιταχύνετε την επεξεργασία.

### Βήμα 5: Εκτελέστε τη διαδικασία αναγνώρισης

Η βαριά δουλειά γίνεται εδώ. Η `recognize()` σαρώνει την εικόνα, εφαρμόζει τμηματοποίηση, τρέχει το νευρωνικό δίκτυο και δημιουργεί εσωτερικά ένα buffer κειμένου.

```python
# Step 5: Execute OCR – this may take a moment for large images
engine.recognize()
```

Πίσω από τη σκηνή η μηχανή εκτελεί:

- **Προεπεξεργασία** (ευθυγράμμιση, δυαδικοποίηση)  
- **Ανάλυση διάταξης** (ανίχνευση στηλών, πινάκων)  
- **Κατηγοριοποίηση χαρακτήρων** (χρησιμοποιώντας μοντέλο deep‑learning)  

Όλα αυτά είναι αφαιρεμένα, γι' αυτό χρειάζεστε μόνο μία γραμμή.

### Βήμα 6: Ανακτήστε και εκτυπώστε το αναγνωρισμένο κείμενο

Τέλος, παίρνουμε το αντικείμενο αποτελέσματος και εξάγουμε τη απλή συμβολοσειρά. Αυτό είναι το τμήμα όπου πραγματικά **εξάγετε κείμενο από εικόνα**.

```python
# Step 6: Get the OCR result and display the plain text
result = engine.getResult()
text = result.getText()
print("📝 Recognized Text:\n")
print(text)
```

**Αναμενόμενη έξοδος** (κομμένη για συντομία):

```
📝 Recognized Text:

Invoice #12345
Date: 2026‑03‑15
Total: $89.99
Thank you for your purchase!
```

Αν η εικόνα δεν περιέχει αναγνωρίσιμους χαρακτήρες, το `text` θα είναι μια κενή συμβολοσειρά. Μπορείτε να προστατέψετε ενάντια σε αυτό:

```python
if not text.strip():
    print("⚠️ No text detected – try a higher‑resolution image or adjust preprocessing.")
```

---

## Εξαγωγή Κειμένου από Εικόνα – Διαχείριση Συνηθισμένων Περιπτώσεων Άκρων

### Πολλαπλές γλώσσες σε ένα αρχείο

Όταν ένα έγγραφο αναμιγνύει γλώσσες, η ρύθμιση `"multilingual"` συνήθως κάνει το σωστό. Ωστόσο, αν παρατηρήσετε λανθασμένες αναγνώσεις, μπορείτε να καθορίσετε χειροκίνητα μια εναλλακτική λίστα:

```python
engine.setLanguage(["eng", "spa", "fra"])  # English, Spanish, French
```

### Μη‑PNG μορφές

Ακόμα και αν η εστίασή μας είναι **αναγνώριση κειμένου από PNG**, το `SimpleOCR` δέχεται επίσης JPEG, BMP και TIFF. Απλώς αλλάξτε την επέκταση αρχείου στη `setImageFromFile`. Για στοίβες TIFF, ίσως χρειαστεί να επιλέξετε μια συγκεκριμένη σελίδα:

```python
engine.setImageFromFile("scanned.tif", page=0)  # first page only
```

### Μεγάλα αρχεία και χρήση μνήμης

Αν επεξεργάζεστε σαρώσεις gigapixel, σκεφτείτε την αλλαγή μεγέθους πριν το OCR:

```python
from PIL import Image

with Image.open(image_path) as img:
    img.thumbnail((2000, 2000))  # keep aspect ratio, max 2000px
    img.save("temp_resized.png")
engine.setImageFromFile("temp_resized.png")
```

Η αλλαγή μεγέθους μειώνει την πίεση στη μνήμη ενώ διατηρεί αρκετές λεπτομέρειες για ακριβή αναγνώριση.

### Εντοπισμός σφαλμάτων αποτυχημένων φορτώσεων

Μερικές φορές μια εικόνα φαίνεται εντάξει στο μάτι αλλά είναι κατεστραμμένη εσωτερικά. Ενεργοποιήστε την εκτενή καταγραφή για να δείτε τι βλέπει η μηχανή:

```python
engine.enableDebug(True)   # prints internal steps to stdout
engine.recognize()
```

---

## Πλήρες, Έτοιμο‑για‑Εκτέλεση Σενάριο

Παρακάτω είναι το πλήρες πρόγραμμα που ενώνει όλα τα κομμάτια. Αντιγράψτε το σε ένα αρχείο με όνομα `ocr_demo.py`, προσαρμόστε το placeholder `YOUR_DIRECTORY`, και τρέξτε `python ocr_demo.py`.

```python
# ocr_demo.py
# Full example showing how to use OCR to extract text from a PNG image.
# Requires: pip install simple-ocr pillow

from simple_ocr import OcrEngine
import os
from PIL import Image

def main():
    # 1️⃣ Create the OCR engine
    engine = OcrEngine()

    # 2️⃣ Define the image path – change this to your actual file location
    image_path = os.path.join("YOUR_DIRECTORY", "mixed_doc.png")

    # 3️⃣ Load the image (with a safety net for missing files)
    try:
        engine.setImageFromFile(image_path)
    except FileNotFoundError:
        print(f"❗️ Cannot find image at '{image_path}'. Exiting.")
        return

    # Optional: resize large images to keep memory usage low
    # (uncomment if you deal with huge scans)
    # with Image.open(image_path) as img:
    #     img.thumbnail((2000, 2000))
    #     resized_path = "temp_resized.png"
    #     img.save(resized_path)
    #     engine.setImageFromFile(resized_path)

    # 4️⃣ Enable automatic language detection (covers all installed packs)
    engine.setLanguage("multilingual")

    # 5️⃣ Run the OCR engine
    engine.recognize()

    # 6️⃣ Retrieve and print the recognized text
    result = engine.getResult()
    text = result.getText()

    if text.strip():
        print("\n📝 Recognized Text:\n")
        print(text)
    else:
        print("⚠️ No recognizable text found. Try a clearer image or adjust preprocessing.")

if __name__ == "__main__":
    main()
```

Η εκτέλεση αυτού του σεναρίου θα πρέπει να εμφανίσει την απλή‑κείμενη έκδοση ό,τι βρίσκεται μέσα στο `mixed_doc.png`. Μη διστάσετε να αντικαταστήσετε το αρχείο με οποιαδήποτε άλλη εικόνα—**πώς να εξάγετε κείμενο** λειτουργεί με τον ίδιο τρόπο.

---

## Συμπέρασμα

Μόλις περάσαμε από το **πώς να χρησιμοποιήσετε OCR** σε Python για **εξαγωγή κειμένου από εικόνα** αρχεία, εστιάζοντας ειδικά στην **αναγνώριση κειμένου από PNG** περιουσιακά στοιχεία και τα πρακτικά βήματα για **φόρτωση εικόνας για OCR**. Το παραπάνω απόσπασμα είναι μια αυτόνομη λύση: εγκαταστήστε το πακέτο, δώστε του ένα αρχείο, ενεργοποιήστε την πολυγλωσσική ανίχνευση, εκτελέστε τη μηχανή και πάρτε το αποτέλεσμα.

Από εδώ μπορείτε να:

- Ενσωματώσετε το σενάριο σε μια υπηρεσία web που δέχεται μεταφορτώσεις χρηστών.  
- Επεξεργαστείτε κατά παρτίδες έναν φάκελο PDF που έχουν μετατραπεί σε PNG.  
- Προσθέσετε μετα-επεξεργασία (π.χ., καθαρισμό με regex, ορθογραφικό έλεγχο) για να βελτιώσετε την ακρίβεια.

Θυμηθείτε, η ποιότητα του OCR εξαρτάται από την καθαρότητα της εικόνας, τα κατάλληλα πακέτα γλώσσας, και μερικές φορές λίγη προ‑επεξεργασία—οπότε πειραματιστείτε

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}