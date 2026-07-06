---
category: general
date: 2026-03-26
description: Μάθετε πώς να εκτελείτε OCR στην Python και να αναγνωρίζετε κείμενο από
  αρχεία εικόνας. Αυτός ο οδηγός δείχνει πώς να εξάγετε κείμενο από PNG και να μετατρέψετε
  την εικόνα σε κείμενο γρήγορα.
draft: false
keywords:
- how to perform ocr
- recognize text from image
- extract text from png
- ocr tutorial python
- convert image to text
language: el
og_description: Πώς να εκτελέσετε OCR στην Python; Ακολουθήστε αυτόν τον οδηγό για
  να αναγνωρίσετε κείμενο από εικόνα, να εξάγετε κείμενο από PNG και να μετατρέψετε
  την εικόνα σε κείμενο με δοκιμαστική άδεια.
og_title: Πώς να εκτελέσετε OCR σε Python – Πλήρης οδηγός
tags:
- OCR
- Python
- Image Processing
title: Πώς να εκτελέσετε OCR σε Python – Πλήρης βήμα‑βήμα οδηγός
url: /el/python-java/general/how-to-perform-ocr-in-python-complete-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εκτελέσετε OCR σε Python – Πλήρης Βήμα‑προς‑Βήμα Εκπαιδευτικό  

Έχετε αναρωτηθεί ποτέ **πώς να εκτελέσετε OCR** σε μια εικόνα που μόλις τραβήξατε με το τηλέφωνό σας; Δεν είστε μόνοι—προγραμματιστές παντού χρειάζονται έναν αξιόπιστο τρόπο για να αναγνωρίζουν κείμενο από αρχεία εικόνας χωρίς να παλεύουν με πολύπλοκες εγγενείς βιβλιοθήκες.  

Σε αυτό το εκπαιδευτικό θα περάσουμε από ένα πρακτικό παράδειγμα που δείχνει **πώς να εκτελέσετε OCR**, **να αναγνωρίσετε κείμενο από εικόνα**, και **να εξάγετε κείμενο από PNG** χρησιμοποιώντας ένα ελαφρύ Python wrapper. Στο τέλος θα μπορείτε να **μετατρέψετε εικόνα σε κείμενο** με λίγες μόνο γραμμές κώδικα, και δεν θα χρειαστεί να ανησυχείτε για προβλήματα αδειοδότησης επειδή θα χρησιμοποιήσουμε τη ενσωματωμένη λειτουργία δοκιμής.

## Τι Θα Μάθετε  

* Πώς να ρυθμίσετε μια δοκιμαστική άδεια για τη μηχανή OCR (χωρίς ανάγκη διαδρομής αρχείου).  
* Η ακριβής ακολουθία κλήσεων για αντικείμενα **recognize text from image**.  
* Τρόποι για **extract text from PNG** αρχεία και αντιμετώπιση κοινών προβλημάτων όπως η έλλειψη γραμματοσειρών.  
* Συμβουλές για κλιμάκωση της λύσης όταν μεταβαίνετε από δοκιμαστική σε άδεια παραγωγής.  

**Prerequisites** – χρειάζεστε Python 3.8+ και το πακέτο `ocr` (εγκαθίσταται μέσω `pip install ocr`). Δεν απαιτούνται άλλα εξωτερικά εργαλεία.

---  

![πώς να εκτελέσετε OCR παράδειγμα](https://example.com/ocr-demo.png "πώς να εκτελέσετε OCR σε Python – εμφανιζόμενο αναγνωρισμένο κείμενο")  

*Image alt text: πώς να εκτελέσετε OCR σε Python – δείγμα εξόδου*  

## Βήμα 1 – Ενεργοποίηση Δοκιμαστικής Άδειας (Χωρίς Διαδρομή Αρχείου)  

Πριν η μηχανή μπορέσει να διαβάσει οτιδήποτε, χρειάζεται μια έγκυρη άδεια. Η λειτουργία δοκιμής είναι ιδανική για πειράματα και μικρά έργα.

```python
# Step 1: Activate a trial license (no file path needed for trial mode)
import ocr

trial_license = ocr.TrialLicense()
trial_license.apply()
```

*Why this matters:* Το αντικείμενο άδειας ενημερώνει τη βιβλιοθήκη OCR ότι λειτουργείτε σε sandbox. Αν παραλείψετε αυτό το βήμα, η μηχανή θα εγείρει ένα `LicenseError` τη στιγμή που καλέσετε `recognize()`.

**Pro tip:** Όταν μεταβείτε σε πληρωμένη άδεια, αντικαταστήστε τις δύο παραπάνω γραμμές με `ocr.License("path/to/your/license.key").apply()`.

## Βήμα 2 – Δημιουργία του Αντικειμένου OCR Engine  

Τώρα που η δοκιμαστική άδεια είναι ενεργή, δημιουργούμε το κύριο engine. Σκεφτείτε το ως το “εγκέφαλο” που θα κοιτάξει την εικόνα και θα αποφασίσει ποιοι χαρακτήρες βρίσκονται πού.

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

*Why this matters:* Το `OcrEngine` περιέχει ρυθμίσεις όπως πακέτα γλώσσας και ρυθμίσεις DPI. Μπορείτε να τα προσαρμόσετε αργότερα, αλλά η προεπιλογή λειτουργεί για τις περισσότερες PNG μόνο στα Αγγλικά.

## Βήμα 3 – Φόρτωση του PNG που Θέλετε να Επεξεργαστείτε  

Εδώ είναι που **recognize text from image**. Η μέθοδος `ocr.Imaging.Image.load()` υποστηρίζει PNG, JPEG, BMP, και μερικές άλλες μορφές.

```python
# Step 3: Load the image you want to recognize
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/sample1.png")
ocr_engine.set_image(input_image)
```

*Edge case:* Αν το PNG σας χρησιμοποιεί παλέτα ευρετηρίου (συνηθισμένο για στιγμιότυπα οθόνης), ο φορτωτής θα το μετατρέψει αυτόματα σε buffer 24‑bit RGB. Αυτή η μετατροπή μπορεί να είναι μικρή επιβάρυνση στην απόδοση, αλλά εγγυάται ακριβή αποτελέσματα OCR.

## Βήμα 4 – Εκτέλεση του OCR και Λήψη του Κειμένου  

Τέλος, ζητάμε από το engine να κάνει τη δουλειά του και στη συνέχεια να πάρουμε το αποτέλεσμα ως απλό κείμενο.

```python
# Step 4: Perform OCR and print the recognized text
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

**Expected output** (παράδειγμα για μια απλή εικόνα που περιέχει “Hello World”):

```
Hello World
```

Αν η εικόνα περιέχει πολλαπλές γραμμές, η έξοδος θα διατηρήσει τις αλλαγές γραμμής, καθιστώντας εύκολο το περαιτέρω επεξεργαστικό στάδιο όπως αναλυτές CSV ή pipelines NLP.

## Προαιρετικό: Ρύθμιση για Καλύτερη Ακρίβεια  

* **Language packs:** `ocr_engine.set_language("eng")` (default) ή `"fra"` για Γαλλικά.  
* **DPI scaling:** `ocr_engine.set_dpi(300)` μπορεί να βελτιώσει τα αποτελέσματα σε σαρώσεις χαμηλής ανάλυσης.  
* **Pre‑processing:** Η εφαρμογή ενός δυαδικού κατωφλίου (`ocr.Imaging.Image.threshold()`) πριν από `set_image` συχνά δίνει πιο καθαρό κείμενο σε θορυβώδεις φόντους.  

Αυτές οι ρυθμίσεις είναι χρήσιμες όταν μεταβαίνετε από μια γρήγορη επίδειξη σε μια παραγωγική **ocr tutorial python** που επεξεργάζεται εκατοντάδες αρχεία την ημέρα.

## Πλήρες Script – Έτοιμο για Αντιγραφή & Επικόλληση  

Παρακάτω είναι το πλήρες, εκτελέσιμο script που συνδυάζει όλα τα παραπάνω βήματα. Αποθηκεύστε το ως `run_ocr.py` και αντικαταστήστε το `YOUR_DIRECTORY/sample1.png` με τη διαδρομή του δικού σας PNG.

```python
# run_ocr.py
# Complete example showing how to perform OCR, recognize text from image,
# and extract text from PNG using the ocr Python package.

import ocr

def main():
    # Activate trial license
    trial_license = ocr.TrialLicense()
    trial_license.apply()

    # Create engine
    ocr_engine = ocr.OcrEngine()

    # Load image (PNG, JPEG, etc.)
    image_path = "YOUR_DIRECTORY/sample1.png"
    input_image = ocr.Imaging.Image.load(image_path)
    ocr_engine.set_image(input_image)

    # Run OCR
    result = ocr_engine.recognize().get_text()
    print("=== Recognized Text ===")
    print(result)

if __name__ == "__main__":
    main()
```

Τρέξτε το από τη γραμμή εντολών:

```bash
python run_ocr.py
```

Θα πρέπει να δείτε το εξαγόμενο κείμενο να εκτυπώνεται στην κονσόλα. Αν λάβετε μια κενή συμβολοσειρά, ελέγξτε ξανά ότι η εικόνα περιέχει σαφές, υψηλής αντίθεσης κείμενο και ότι η δοκιμαστική άδεια εφαρμόστηκε χωρίς σφάλματα.

## Συχνές Ερωτήσεις & Παγίδες  

* **“Does this work with JPEG?”** – Απόλυτα. Η μέθοδος `load()` ανιχνεύει αυτόματα τη μορφή, έτσι μπορείτε να αντικαταστήσετε το PNG με JPEG χωρίς αλλαγές κώδικα.  
* **“What if the image is rotated?”** – Η μηχανή μπορεί να ανιχνεύσει αυτόματα τον προσανατολισμό, αλλά για καλύτερα αποτελέσματα μπορείτε να προ‑στρέψετε με `input_image.rotate(90)` πριν από `set_image`.  
* **“Can I process multiple images in a loop?”** – Ναι. Απλώς μετακινήστε τις κλήσεις φόρτωσης και `recognize()` μέσα σε έναν βρόχο `for`; το ίδιο αντικείμενο `ocr_engine` μπορεί να επαναχρησιμοποιηθεί, εξοικονομώντας λίγο χρόνο.  

## Επόμενα Βήματα – Από Επίδειξη σε Παραγωγή  

Τώρα που ξέρετε **πώς να εκτελέσετε OCR**, σκεφτείτε τα παρακάτω θέματα:

* **Batch processing** – Συνδυάστε αυτό το script με `os.listdir()` για **extract text from PNG** αρχεία μαζικά.  
* **Integrate with PDF** – Χρησιμοποιήστε `pdf2image` για να μετατρέψετε σελίδες PDF σε PNG, και στη συνέχεια τροφοδοτήστε τα στην ίδια pipeline.  
* **Post‑processing** – Εφαρμόστε regex ή fuzzy matching για να καθαρίσετε κοινές λανθασμένες αναγνώσεις OCR (π.χ., “0” vs “O”).  

Κάθε ένα από αυτά βασίζεται στην κεντρική ιδέα του **convert image to text** και επεκτείνει τη χρησιμότητα της ροής εργασίας OCR.

---  

### TL;DR  

Συζητήσαμε όλα όσα χρειάζεστε για να **πώς να εκτελέσετε OCR** σε Python: ενεργοποιήστε μια δοκιμαστική άδεια, δημιουργήστε ένα engine, φορτώστε ένα PNG, εκτελέστε την αναγνώριση και εκτυπώστε το αποτέλεσμα. Με λίγες μόνο γραμμές μπορείτε να **recognize text from image**, **extract text from PNG**, και **convert image to text** για οποιαδήποτε επόμενη εφαρμογή.  

Δοκιμάστε το, προσαρμόστε τις ρυθμίσεις DPI ή γλώσσας, και αφήστε το engine να κάνει το σκληρό έργο. Καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}