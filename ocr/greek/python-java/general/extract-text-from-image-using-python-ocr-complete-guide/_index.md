---
category: general
date: 2026-06-06
description: Εξάγετε κείμενο από εικόνα με Python OCR σε λίγα λεπτά. Ανακαλύψτε πολυγλωσσικό
  OCR εικόνας, αυτόματη ανίχνευση γλώσσας OCR και πώς να εξάγετε κείμενο OCR με ακρίβεια.
draft: false
keywords:
- extract text from image
- how to extract OCR text
- multilingual image OCR
- detect language OCR
- auto detect language OCR
language: el
og_description: Εξάγετε κείμενο από εικόνα με Python OCR γρήγορα. Μάθετε πολυγλωσσικό
  OCR εικόνας, αυτόματη ανίχνευση γλώσσας OCR και πώς να εξάγετε κείμενο OCR βήμα
  προς βήμα.
og_title: Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας Python OCR – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from image with Python OCR in minutes. Discover multilingual
    image OCR, auto detect language OCR, and how to extract OCR text accurately.
  headline: Extract Text from Image Using Python OCR – Complete Guide
  type: TechArticle
- description: Extract text from image with Python OCR in minutes. Discover multilingual
    image OCR, auto detect language OCR, and how to extract OCR text accurately.
  name: Extract Text from Image Using Python OCR – Complete Guide
  steps:
  - name: '**Low‑resolution images** – OCR accuracy drops sharply below 150 dpi. Upscale
      or request a higher‑resolution scan.'
    text: '**Low‑resolution images** – OCR accuracy drops sharply below 150 dpi. Upscale
      or request a higher‑resolution scan.'
  - name: '**Noise and compression artifacts** – Apply a simple threshold filter (`opencv`
      or `Pillow`) before feeding the image to the engine.'
    text: '**Noise and compression artifacts** – Apply a simple threshold filter (`opencv`
      or `Pillow`) before feeding the image to the engine.'
  - name: '**Mixed scripts on one page** – Some engines struggle with simultaneous
      Latin and CJK characters. Split the page into regions and run separate recognitions
      if needed.'
    text: '**Mixed scripts on one page** – Some engines struggle with simultaneous
      Latin and CJK characters. Split the page into regions and run separate recognitions
      if needed.'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- Multilingual
title: Απόσπαση κειμένου από εικόνα με Python OCR – Πλήρης οδηγός
url: /el/python-java/general/extract-text-from-image-using-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Εικόνα με Python OCR – Πλήρης Οδηγός

Έχετε χρειαστεί ποτέ να **εξάγετε κείμενο από εικόνα** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη μπορεί να διαχειριστεί αυτόματα πολλές γλώσσες; Δεν είστε μόνοι—οι προγραμματιστές ρωτούν συνεχώς *πώς να εξάγουν κείμενο OCR* όταν εργάζονται με διεθνή έγγραφα, αποδείξεις ή σαρωμένα φυλλάδια. Σε αυτό το tutorial θα περάσουμε από ένα πρακτικό παράδειγμα Python που όχι μόνο εξάγει κείμενο από μια εικόνα αλλά επίσης **ανιχνεύει τη γλώσσα** αυτόματα, καθιστώντας το πολυγλωσσικό OCR εικόνας παιχνιδάκι.

Θα καλύψουμε τα πάντα, από την εγκατάσταση του πακέτου OCR μέχρι την ενεργοποίηση του **auto detect language OCR**, την εκτέλεση της μηχανής σε ένα δείγμα εικόνας, και τέλος την εκτύπωση τόσο της ανιχνευμένης γλώσσας όσο και του εξαγόμενου κειμένου. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο snippet που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο, είτε χτίζετε μια αλυσίδα μετάφρασης είτε μια υπηρεσία εισαγωγής δεδομένων.

## Εξαγωγή Κειμένου από Εικόνα – Ρύθμιση Περιβάλλοντος

Πριν βουτήξουμε στον κώδικα, βεβαιωθείτε ότι το περιβάλλον εργασίας σας πληροί τις ελάχιστες απαιτήσεις:

- Python 3.8 ή νεότερο (η βιβλιοθήκη χρησιμοποιεί type hints που οι παλαιότερες εκδόσεις αγνοούν)
- `pip` για διαχείριση πακέτων
- Ένα αρχείο εικόνας που περιέχει κείμενο τουλάχιστον σε δύο διαφορετικές γλώσσες (π.χ. Αγγλικά + Ισπανικά)

Θα χρειαστείτε επίσης τη βιβλιοθήκη OCR που τροφοδοτεί αυτή τη demo. Για το σκοπό αυτού του οδηγού θα χρησιμοποιήσουμε το φανταστικό πακέτο `ocr`, το οποίο αντικατοπτρίζει δημοφιλή πραγματικά εργαλεία όπως το Tesseract ή το EasyOCR αλλά προσφέρει ένα καθαρό Python API.

```bash
# Install the OCR package and its optional image dependencies
pip install ocr[image]
```

> **Pro tip:** Αν αντιμετωπίσετε σφάλματα δικαιωμάτων, προσθέστε `python -m` στην αρχή της εντολής ή χρησιμοποιήστε ένα virtual environment—διατηρεί τα global site‑packages σας καθαρά.

## Δημιουργία Αντικειμένου OCR Engine

Τώρα που η βιβλιοθήκη είναι έτοιμη, το πρώτο λογικό βήμα είναι να **δημιουργήσετε ένα αντικείμενο OCR engine**. Σκεφτείτε τη μηχανή ως έναν έξυπνο σαρωτή που μπορείτε να διαμορφώσετε πριν της δώσετε εικόνες.

```python
import ocr

# Step 1: Initialize the OCR engine
engine = ocr.OcrEngine()
```

Γιατί δημιουργούμε το αντικείμενο ξεχωριστά αντί να καλέσουμε μια static μέθοδο; Το αντικείμενο engine κρατάει την κατάσταση διαμόρφωσης (όπως προτιμήσεις γλώσσας) που μπορεί να θέλετε να επαναχρησιμοποιήσετε σε πολλές εικόνες, εξοικονομώντας το κόστος επανεκκίνησής του κάθε φορά.

## Ενεργοποίηση Auto Detect Language OCR

Οι περισσότερες εργαλεία OCR απαιτούν να καθορίσετε έναν κωδικό γλώσσας—`eng` για Αγγλικά, `spa` για Ισπανικά, κ.λπ. Η χειροκίνητη εικασία της γλώσσας αντιτίθεται στον σκοπό μιας **πολυγλωσσικής OCR εικόνας**. Ευτυχώς, το πακέτο `ocr` προσφέρει λειτουργία *auto detect language OCR* που εξετάζει την εικόνα και επιλέγει το καλύτερο μοντέλο γλώσσας στο παρασκήνιο.

```python
# Step 2: Turn on automatic language detection
engine.set_recognition_language(ocr.Language.AUTO_DETECT)
```

Η ενεργοποίηση του **detect language OCR** με αυτόν τον τρόπο σημαίνει ότι δεν θα χρειαστεί να διατηρείτε μια μακριά λίστα κωδικών γλώσσας. Η μηχανή θα προσπαθήσει να ταιριάξει το script που βλέπει—Latin, Cyrillic, Han κ.λπ.—και θα φορτώσει το κατάλληλο μοντέλο αυτόματα.

## Εκτέλεση Πολυγλωσσικού OCR Εικόνας

Με τη μηχανή έτοιμη, ήρθε η ώρα να **εξάγετε κείμενο από εικόνα**. Η μέθοδος `recognize_image` δέχεται μια διαδρομή αρχείου και επιστρέφει ένα αντικείμενο αποτελέσματος που περιέχει τόσο το ακατέργαστο κείμενο όσο και τη γλώσσα που ανιχνεύθηκε.

```python
# Step 3: Run OCR on a multilingual image
image_path = "YOUR_DIRECTORY/multilang_page.png"
result = engine.recognize_image(image_path)
```

Αν αναρωτιέστε *πώς να εξάγετε OCR κείμενο* από PDF αντί για PNG, η ίδια μηχανή προσφέρει `recognize_pdf`—απλώς αλλάξτε το όνομα της μεθόδου. Η λογική ανίχνευσης παραμένει η ίδια, οπότε επωφελείστε από την ίδια λειτουργία **auto detect language OCR**.

## Εμφάνιση Ανιχνευμένης Γλώσσας και Εξαγόμενου Κειμένου

Τέλος, εμφανίζουμε ό,τι ανακάλυψε η μηχανή. Το αντικείμενο αποτελέσματος εκθέτει `detected_language` (μια ετικέτα BCP‑47 όπως `en` ή `es`) και `text`, που περιέχει το ακατέργαστο OCR output.

```python
# Step 4: Show the language and the extracted string
print(f"Detected language: {result.detected_language}")
print("Extracted text:")
print(result.text)
```

Η εκτέλεση του script στην δείγμα εικόνα μας θα πρέπει να παράγει κάτι παρόμοιο με:

```
Detected language: en
Extracted text:
Welcome to our multilingual brochure.
¡Bienvenidos a nuestro folleto multilingüe!
```

Παρατηρήστε πώς η μηχανή αναγνώρισε σωστά τα Αγγλικά ως κύρια γλώσσα, αλλά κατέγραψε και τη γραμμή στα Ισπανικά—ακριβώς αυτό που περιμένετε από μια αξιόπιστη **πολυγλωσσική OCR εικόνας** λύση.

### Τι γίνεται αν η ανίχνευση αποτύχει;

Μερικές φορές η μηχανή OCR μπορεί να επιστρέψει μια προεπιλεγμένη γλώσσα (συνήθως Αγγλικά) αν η εικόνα είναι θολή ή το script είναι πολύ εξωτικό. Σε αυτές τις περιπτώσεις μπορείτε να επιβάλετε μια λίστα γλωσσών:

```python
engine.set_recognition_language([ocr.Language.ENGLISH, ocr.Language.SPANISH])
```

Αλλά θυμηθείτε, η επιβολή γλωσσών μειώνει την ευκολία του **auto detect language OCR**, οπότε χρησιμοποιήστε το μόνο όταν γνωρίζετε ένα υποσύνολο γλωσσών.

## Συνηθισμένα Πιθανά Προβλήματα και Πώς να Εξάγετε OCR Κείμενο Αξιόπιστα

Ακόμη και με auto‑detection, μερικά μικρά προβλήματα μπορεί να σας εμποδίσουν:

1. **Εικόνες χαμηλής ανάλυσης** – Η ακρίβεια του OCR πέφτει δραστικά κάτω από 150 dpi. Ανεβάστε την ανάλυση ή ζητήστε σάρωση υψηλότερης ανάλυσης.
2. **Θόρυβος και τεχνουργήματα συμπίεσης** – Εφαρμόστε ένα απλό φίλτρο κατωφλίου (`opencv` ή `Pillow`) πριν δώσετε την εικόνα στη μηχανή.
3. **Μικτά scripts σε μία σελίδα** – Κάποιες μηχανές δυσκολεύονται με ταυτόχρονα Latin και CJK χαρακτήρες. Χωρίστε τη σελίδα σε περιοχές και τρέξτε ξεχωριστές αναγνωρίσεις αν χρειαστεί.

Η αντιμετώπιση αυτών των ζητημάτων βελτιώνει δραματικά την ποιότητα της διαδικασίας **extract text from image**, ειδικά όταν δουλεύετε με πραγματικά, πολυγλωσσικά έγγραφα.

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω βρίσκεται το πλήρες, έτοιμο‑για‑εκτέλεση script που συνδυάζει όλα τα βήματα που συζητήσαμε. Αποθηκεύστε το ως `multilingual_ocr.py` και τρέξτε το από τη γραμμή εντολών.

```python
import ocr

def main():
    # Initialize engine with auto language detection
    engine = ocr.OcrEngine()
    engine.set_recognition_language(ocr.Language.AUTO_DETECT)

    # Path to your multilingual image
    image_path = "YOUR_DIRECTORY/multilang_page.png"

    # Perform OCR
    result = engine.recognize_image(image_path)

    # Output results
    print(f"Detected language: {result.detected_language}")
    print("Extracted text:")
    print(result.text)

if __name__ == "__main__":
    main()
```

**Αναμενόμενο αποτέλεσμα** (υπόθεση ότι η δείγμα εικόνα περιέχει κείμενο στα Αγγλικά και Ισπανικά):

```
Detected language: en
Extracted text:
Welcome to our multilingual brochure.
¡Bienvenidos a nuestro folleto multilingüe!
```

Αντικαταστήστε το `multilang_page.png` με οποιαδήποτε εικόνα περιέχει κείμενο σε άλλες γλώσσες—χάρη στο **auto detect language OCR**, το script θα δώσει ακόμα μια λογική ετικέτα γλώσσας και το αντίστοιχο κείμενο.

![Εξαγωγή κειμένου από εικόνα παράδειγμα](https://example.com/ocr-sample.png "Εξαγωγή κειμένου από εικόνα")

## Συμπέρασμα

Τώρα ξέρετε ακριβώς **πώς να εξάγετε OCR κείμενο** από μια εικόνα, πώς να ενεργοποιήσετε το **auto detect language OCR**, και πώς να διαχειριστείτε σενάρια **πολυγλωσσικού OCR εικόνας** με ελάχιστο κώδικα. Δημιουργώντας ένα OCR engine instance, ενεργοποιώντας την αυτόματη ανίχνευση γλώσσας, και καλώντας το `recognize_image`, μπορείτε αξιόπιστα να εξάγετε τόσο τον αναγνωριστικό γλώσσας όσο και το ακατέργαστο κείμενο.

Τι ακολουθεί; Δοκιμάστε να τροφοδοτήσετε τα εξαγόμενα strings σε ένα API μετάφρασης, αποθηκεύστε τα σε μια αναζητήσιμη βάση δεδομένων, ή συνδυάστε πολλές σελίδες σε ένα ενιαίο PDF report. Μπορείτε επίσης να πειραματιστείτε με διαφορετικά OCR back‑ends (Tesseract, EasyOCR, Google Vision) διατηρώντας το ίδιο υψηλού επιπέδου workflow—ευχαριστώντας τη συνεπή **detect language OCR** διεπαφή.

Αν αντιμετωπίσετε οποιεσδήποτε ιδιαιτερότητες, επιστρέψτε στην ενότητα “Συνηθισμένα Πιθανά Προβλήματα” ή προσαρμόστε τα βήματα προεπεξεργασίας εικόνας. Καλή κωδικοποίηση, και εύχομαι το επόμενο έργο σας να είναι γεμάτο σωστά ανιχνευμένο, τέλεια εξαγόμενο κείμενο!

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει ολοκληρωμένα παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην δική σας υλοποίηση.

- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}