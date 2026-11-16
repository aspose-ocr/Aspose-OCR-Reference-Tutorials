---
category: general
date: 2026-06-22
description: Αναγνωρίστε κείμενο από PNG χρησιμοποιώντας Aspose OCR Python – μάθετε
  πώς να φορτώνετε εικόνα για OCR, να μετατρέπετε την εικόνα σε κείμενο και να διαβάζετε
  κείμενο από την εικόνα γρήγορα.
draft: false
keywords:
- recognize text from png
- convert image to text
- read text from image
- aspose ocr python
- load image for ocr
language: el
og_description: αναγνωρίστε κείμενο από PNG χρησιμοποιώντας το Aspose OCR Python.
  Αυτό το σεμινάριο δείχνει πώς να φορτώσετε μια εικόνα για OCR, να μετατρέψετε την
  εικόνα σε κείμενο και να διαβάσετε το κείμενο από την εικόνα με λίγες γραμμές κώδικα.
og_title: Αναγνώριση κειμένου από PNG με Aspose OCR Python – Πλήρης Οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: recognize text from png using Aspose OCR Python – learn how to load
    image for OCR, convert image to text and read text from image quickly.
  headline: recognize text from png with Aspose OCR Python – Full Step‑by‑Step Guide
  type: TechArticle
- description: recognize text from png using Aspose OCR Python – learn how to load
    image for OCR, convert image to text and read text from image quickly.
  name: recognize text from png with Aspose OCR Python – Full Step‑by‑Step Guide
  steps:
  - name: 5.1 Set the Language
    text: 'Aspose OCR ships with multilingual support. If your PNG contains French
      text, tell the engine:'
  - name: 5.2 Adjust DPI (Dots Per Inch)
    text: 'Higher DPI often yields cleaner character shapes. You can manually set
      it before loading the image:'
  - name: 5.3 Enable Spell‑Check (Post‑Processing)
    text: 'After you **read text from image**, you might want to run a quick spell‑check
      to clean up OCR artifacts:'
  - name: 6.1 Empty Results
    text: 'If `ocr_result.text` is an empty string, the engine likely couldn’t detect
      any characters. Try:'
  - name: 6.2 Multi‑Page Images
    text: PNG doesn’t support multiple pages, but if you inadvertently feed a multi‑frame
      TIFF, Aspose OCR will only process the first frame. Loop over frames manually
      if you need to **read text from image** sequences.
  - name: 6.3 Memory Leaks in Long‑Running Scripts
    text: When processing thousands of images, reuse a single `OcrEngine` instance
      instead of creating a new one per file. This reuses native buffers and reduces
      GC pressure.
  type: HowTo
tags:
- Aspose
- OCR
- Python
- Image Processing
title: Αναγνώριση κειμένου από PNG με Aspose OCR Python – Πλήρης Οδηγός Βήμα‑προς‑Βήμα
url: /el/python/general/recognize-text-from-png-with-aspose-ocr-python-full-step-by/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση κειμένου από PNG με Aspose OCR Python – Πλήρης Οδηγός

Έχετε ποτέ χρειαστεί να **αναγνωρίσετε κείμενο από png** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη θα σας δώσει καθαρά αποτελέσματα χωρίς εκατοντάδες ρυθμίσεις; Δεν είστε μόνοι. Σε πολλά έργα αυτοματοποίησης το πρώτο βήμα είναι να *μετατρέψετε την εικόνα σε κείμενο* ώστε η λογική που ακολουθεί να δουλεύει με πραγματικές λέξεις αντί για εικονοστοιχεία.  

Σε αυτό το tutorial θα δείτε ακριβώς πώς να **φορτώσετε εικόνα για OCR**, να εκτελέσετε το Aspose OCR σε Python και τελικά να **διαβάσετε κείμενο από εικόνα** με μόνο λίγες γραμμές κώδικα. Χωρίς περιττές πληροφορίες, μόνο μια λειτουργική λύση που μπορείτε να ενσωματώσετε στα δικά σας scripts σήμερα.

## Τι θα μάθετε

- Εγκαταστήστε το πακέτο Aspose OCR Python (`asposeocrpy`)
- Δημιουργήστε ένα αντικείμενο `OcrEngine` και ρυθμίστε το για αρχεία PNG
- Χρησιμοποιήστε τη μηχανή για **να αναγνωρίσετε κείμενο από png** και διαχειριστείτε το αποτέλεσμα
- Προαιρετικές ρυθμίσεις: ορίστε γλώσσα, προσαρμόστε DPI και αντιμετωπίστε κοινά προβλήματα  
- Ένα πλήρες, εκτελέσιμο script που μπορείτε να αντιγράψετε‑και‑επικολλήσετε

*Προαπαιτούμενα*: Python 3.7+, pip, και μια εικόνα PNG που θέλετε να επεξεργαστείτε. Δεν απαιτούνται άλλα εξωτερικά εργαλεία.

---

## Βήμα 1: Εγκατάσταση Aspose OCR για Python

Πριν μπορέσουμε να **μετατρέψουμε την εικόνα σε κείμενο**, χρειαζόμαστε τη βιβλιοθήκη. Ανοίξτε ένα τερματικό (ή την κονσόλα του αγαπημένου σας IDE) και εκτελέστε:

```bash
pip install asposeocrpy
```

Αυτή η εντολή κατεβάζει το πιο πρόσφατο πακέτο Aspose OCR και τις εγγενείς εξαρτήσεις του. Αν αντιμετωπίσετε σφάλμα δικαιωμάτων, προσθέστε `--user` ή χρησιμοποιήστε ένα εικονικό περιβάλλον — τίποτα εξειδικευμένο, μόνο καλή πρακτική Python.

> **Συμβουλή:** Κρατήστε τα πακέτα σας ενημερωμένα. `pip list --outdated` θα σας δείξει αν υπάρχει νεότερη έκδοση του Aspose OCR, η οποία συχνά προσφέρει βελτιώσεις απόδοσης για την επεξεργασία PNG.

---

## Βήμα 2: Εισαγωγή Aspose OCR και Δημιουργία Αντικειμένου OCR Engine

Τώρα που το πακέτο είναι έτοιμο, ας το εισάγουμε και να ξεκινήσουμε τη μηχανή. Αυτό είναι η καρδιά της ροής εργασίας **aspose ocr python**.

```python
# Step 2: Import Aspose OCR and create an OCR engine instance
import asposeocrpy as ocr

# The OcrEngine class provides all the methods we need.
ocr_engine = ocr.OcrEngine()
```

Γιατί δημιουργούμε ένα αντικείμενο `OcrEngine` αντί να καλέσουμε μια στατική συνάρτηση; Η μηχανή κρατά τις ρυθμίσεις (γλώσσα, DPI κλπ.) που μπορεί να θέλετε να προσαρμόσετε αργότερα, έτσι είναι επαναχρησιμοποιήσιμη για πολλές εικόνες.

---

## Βήμα 3: Φόρτωση Εικόνας για OCR

Εδώ συμβαίνει το μέρος **φόρτωσης εικόνας για ocr**. Το Aspose OCR δέχεται οποιαδήποτε μορφή υποστηρίζεται από το `System.Drawing` του .NET, που περιλαμβάνει PNG, JPEG, BMP και άλλα.

```python
# Step 3: Load the image you want to recognize (any format supported by System.Drawing)
image_file = r"YOUR_DIRECTORY/input.png"   # replace with your actual path
ocr_engine.load_image(image_file)
```

Μερικές λεπτομέρειες που αξίζει να σημειωθούν:

- **Raw string (`r"...`)** αποτρέπει τυχαία προβλήματα με ακολουθίες διαφυγής σε διαδρομές Windows.
- Αν η εικόνα είναι μεγάλη, ίσως θέλετε πρώτα να τη μειώσετε· η ακρίβεια του OCR συχνά κορυφώνεται γύρω στα 300 DPI.

---

## Βήμα 4: Εκτέλεση Απλού OCR και Ανάκτηση του Αναγνωρισμένου Κειμένου

Με τη φορτωμένη εικόνα, μπορούμε τελικά να **αναγνωρίσουμε κείμενο από png**. Η μέθοδος `recognize()` κάνει τη βαριά δουλειά και επιστρέφει ένα αντικείμενο `OcrResult`.

```python
# Step 4: Run plain OCR and retrieve the recognized text
ocr_result = ocr_engine.recognize()
print("Plain OCR:", ocr_result.text)
```

Το χαρακτηριστικό `text` περιέχει μια απλή συμβολοσειρά με όλα όσα η μηχανή μπόρεσε να διαβάσει. Αν χρειάζεστε περιοριστικά πλαίσια ή βαθμολογίες εμπιστοσύνης, είναι επίσης διαθέσιμα (`ocr_result.regions`, `ocr_result.confidence`), αλλά για τις περισσότερες περιπτώσεις “μετατροπής εικόνας σε κείμενο” η απλή συμβολοσειρά είναι αρκετή.

**Αναμενόμενη έξοδος** (υποθέτοντας ότι το `input.png` περιέχει “Hello World”):

```
Plain OCR: Hello World
```

Αν δείτε ακατανόητο κείμενο, ελέγξτε ξανά την ποιότητα της εικόνας και σκεφτείτε τις προαιρετικές ρυθμίσεις στην επόμενη ενότητα.

---

## Βήμα 5: Προαιρετικό – Λεπτομερής Ρύθμιση της Μηχανής για Καλύτερη Ακρίβεια

### 5.1 Ορισμός Γλώσσας

Το Aspose OCR προσφέρει πολυγλωσσική υποστήριξη. Αν το PNG σας περιέχει κείμενο στα Γαλλικά, ενημερώστε τη μηχανή:

```python
ocr_engine.language = ocr.Language.French
```

### 5.2 Προσαρμογή DPI (Dots Per Inch)

Υψηλότερο DPI συχνά δίνει καθαρότερα σχήματα χαρακτήρων. Μπορείτε να το ορίσετε χειροκίνητα πριν φορτώσετε την εικόνα:

```python
ocr_engine.dpi = 300   # 300 DPI is a sweet spot for most prints
```

### 5.3 Ενεργοποίηση Ελέγχου Ορθογραφίας (Μετά‑Επεξεργασία)

Αφού **διαβάσετε κείμενο από εικόνα**, ίσως θέλετε να εκτελέσετε έναν γρήγορο έλεγχο ορθογραφίας για να καθαρίσετε τα artefacts του OCR:

```python
import difflib

def simple_spell_check(text):
    # Very naive example – replace common OCR misreads
    corrections = {"0": "O", "1": "I", "5": "S"}
    for wrong, right in corrections.items():
        text = text.replace(wrong, right)
    return text

clean_text = simple_spell_check(ocr_result.text)
print("Cleaned OCR:", clean_text)
```

Αυτές οι ρυθμίσεις είναι προαιρετικές αλλά μπορούν να βελτιώσουν δραματικά την αξιοπιστία της **μετατροπής εικόνας σε κείμενο** διαδικασίας, ειδικά όταν εργάζεστε με σαρωμένα έγγραφα ή PNG με χαμηλή αντίθεση.

---

## Βήμα 6: Διαχείριση Ακραίων Περιπτώσεων και Κοινών Προβλημάτων

### 6.1 Κενά Αποτελέσματα

Αν το `ocr_result.text` είναι κενή συμβολοσειρά, η μηχανή πιθανότατα δεν μπόρεσε να εντοπίσει χαρακτήρες. Δοκιμάστε:

- Αύξηση DPI (`ocr_engine.dpi = 400`)
- Μετατροπή του PNG σε κλίμακα του γκρι πρώτα (εξωτερικές βιβλιοθήκες όπως το Pillow μπορούν να βοηθήσουν)
- Βεβαιωθείτε ότι η εικόνα δεν είναι υπερβολικά συμπιεσμένη (υψηλή συμπίεση μπορεί να διαγράψει λεπτομέρειες)

### 6.2 Πολυσελίδες Εικόνες

Το PNG δεν υποστηρίζει πολλαπλές σελίδες, αλλά αν κατά λάθος δώσετε ένα multi‑frame TIFF, το Aspose OCR θα επεξεργαστεί μόνο το πρώτο πλαίσιο. Επανάληψη πάνω στα πλαίσια χειροκίνητα αν χρειάζεται να **διαβάσετε κείμενο από εικόνα** ακολουθίες.

### 6.3 Διαρροές Μνήμης σε Μακροχρόνια Scripts

Κατά την επεξεργασία χιλιάδων εικόνων, επαναχρησιμοποιήστε ένα μόνο αντικείμενο `OcrEngine` αντί να δημιουργείτε νέο για κάθε αρχείο. Αυτό επαναχρησιμοποιεί τους εγγενείς buffers και μειώνει την πίεση του GC.

```python
for path in png_paths:
    ocr_engine.load_image(path)
    result = ocr_engine.recognize()
    # process result...
```

---

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω υπάρχει ένα αυτόνομο script που ενώνει όλα τα παραπάνω. Αποθηκεύστε το ως `ocr_png_demo.py` και εκτελέστε το με `python ocr_png_demo.py`.

```python
import asposeocrpy as ocr
import os

def main():
    # ==== Configuration ====
    # Folder containing PNG files
    img_dir = r"YOUR_DIRECTORY"
    # Optional: set language and DPI for the engine
    language = ocr.Language.English
    dpi = 300

    # ==== Initialize OCR Engine ====
    engine = ocr.OcrEngine()
    engine.language = language
    engine.dpi = dpi

    # ==== Process each PNG ====
    for filename in os.listdir(img_dir):
        if not filename.lower().endswith('.png'):
            continue   # skip non‑PNG files

        img_path = os.path.join(img_dir, filename)
        engine.load_image(img_path)          # load image for OCR
        result = engine.recognize()          # recognize text from png
        print(f"\nFile: {filename}")
        print("Plain OCR:", result.text)

        # Optional cleaning step
        cleaned = result.text.replace('0', 'O').replace('1', 'I')
        print("Cleaned OCR:", cleaned)

if __name__ == "__main__":
    main()
```

**Τι κάνει αυτό το script**:

1. Ρυθμίζει τη μηχανή με αγγλική γλώσσα και 300 DPI.
2. Διασχίζει έναν φάκελο, **φορτώνει εικόνα για OCR**, και εκτελεί την αναγνώριση.
3. Εκτυπώνει τόσο το ακατέργαστο όσο και μια πολύ απλή καθαρισμένη έκδοση του κειμένου.

Εκτελέστε το script και θα δείτε τη συμβολοσειρά που εξήχθη από κάθε PNG να εκτυπώνεται στην κονσόλα — ακριβώς η ροή εργασίας **μετατροπής εικόνας σε κείμενο** που χρειάζονται πολλοί προγραμματιστές.

---

## Συμπέρασμα

Τώρα έχετε μια ισχυρή, ολοκληρωμένη μέθοδο για **αναγνώριση κειμένου από png** χρησιμοποιώντας το Aspose OCR σε Python. Από την εγκατάσταση του πακέτου μέχρι τη λεπτομερή ρύθμιση DPI και γλώσσας, το tutorial κάλυψε κάθε βήμα που θα περιμένατε όταν θέλετε να **φορτώσετε εικόνα για OCR**, **μετατρέψετε εικόνα σε κείμενο**, και τελικά **διαβάσετε κείμενο από εικόνα** στις δικές σας εφαρμογές.

Τι ακολουθεί; Δοκιμάστε να τροφοδοτήσετε την έξοδο του OCR σε μια αλυσίδα επεξεργασίας φυσικής γλώσσας, να την αποθηκεύσετε σε μια αναζητήσιμη βάση δεδομένων ή να δημιουργήσετε PDF άμεσα. Αν σας ενδιαφέρουν άλλες μορφές εικόνας, αντικαταστήστε την επέκταση `.png` με `.jpg` ή `.bmp` — ο ίδιος κώδικας λειτουργεί επειδή το Aspose OCR τα υποστηρίζει από προεπιλογή.

Έχετε ερωτήσεις σχετικά με τη διαχείριση χρωματιστών φόντων ή πολυγλωσσικών εγγράφων; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

![παράδειγμα αναγνώρισης κειμένου από png](https://example.com/ocr-png-screenshot.png "αναγνώριση κειμένου από png")

*Η εικόνα δείχνει ένα παράθυρο τερματικού όπου το script εκτυπώνει το εξαγόμενο κείμενο από ένα αρχείο PNG.*

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Βήμα‑Βήμα](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Πώς να Κάνετε OCR Κειμένου Εικόνας με Γλώσσα Χρησιμοποιώντας Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Πώς να εξάγετε κείμενο από εικόνα από URL χρησιμοποιώντας Aspose.OCR για Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}