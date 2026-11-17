---
category: general
date: 2026-05-31
description: Βελτιώστε την ακρίβεια του OCR με Python, προεπεξεργάζοντας εικόνες για
  OCR. Μάθετε πώς να εξάγετε κείμενο από αρχεία εικόνας, να αναγνωρίζετε κείμενο από
  PNG και να ενισχύετε τα αποτελέσματα.
draft: false
keywords:
- improve OCR accuracy
- preprocess image for OCR
- extract text from image
- recognize text from PNG
- image preprocessing for text
language: el
og_description: Βελτιώστε την ακρίβεια OCR στην Python εφαρμόζοντας προεπεξεργασία
  εικόνας για κείμενο. Ακολουθήστε αυτόν τον οδηγό για να εξάγετε κείμενο από αρχεία
  εικόνας και να αναγνωρίζετε κείμενο από PNG χωρίς κόπο.
og_title: Βελτιώστε την ακρίβεια OCR στην Python – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Improve OCR accuracy with Python by preprocessing images for OCR. Learn
    how to extract text from image files, recognize text from PNG, and boost results.
  headline: Improve OCR Accuracy in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Improve OCR accuracy with Python by preprocessing images for OCR. Learn
    how to extract text from image files, recognize text from PNG, and boost results.
  name: Improve OCR Accuracy in Python – Complete Step‑by‑Step Guide
  steps:
  - name: Loads the PNG into memory
    text: Loads the PNG into memory
  - name: Applies denoise and deskew based on our settings
    text: Applies denoise and deskew based on our settings
  - name: Runs the neural‑network or classic pattern matcher
    text: Runs the neural‑network or classic pattern matcher
  - name: Packages the output into `recognition_result`
    text: Packages the output into `recognition_result`
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Βελτιώστε την ακρίβεια του OCR στην Python – Πλήρης οδηγός βήμα‑βήμα
url: /el/python-java/general/improve-ocr-accuracy-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Βελτιώστε την Ακρίβεια OCR σε Python – Πλήρης Οδηγός Βήμα‑βήμα

Προσπαθήσατε ποτέ να **βελτιώσετε την ακρίβεια OCR** και να λάβετε ακατάστατο αποτέλεσμα; Δεν είστε οι μόνοι. Οι περισσότεροι προγραμματιστές συναντούν προβλήματα όταν η ακατέργαστη εικόνα είναι θορυβώδης, λοξή ή απλώς χαμηλής αντίθεσης. Τα καλά νέα; Μερικές τεχνικές προεπεξεργασίας μπορούν να μετατρέψουν ένα θολό στιγμιότυπο σε καθαρό, μηχανικά αναγνώσιμο κείμενο.

Σε αυτό το tutorial θα περάσουμε από ένα πραγματικό παράδειγμα που **προετοιμάζει μια εικόνα για OCR**, εκτελεί τη μηχανή αναγνώρισης και τελικά **εξάγει κείμενο από αρχεία εικόνας**—συγκεκριμένα PNG. Στο τέλος θα ξέρετε ακριβώς πώς να **αναγνωρίσετε κείμενο από PNG** με υψηλότερο ποσοστό επιτυχίας και θα έχετε ένα επαναχρησιμοποιήσιμο απόσπασμα κώδικα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο.

## Τι Θα Μάθετε

- Γιατί η προεπεξεργασία εικόνας είναι σημαντική για τις μηχανές OCR  
- Ποιες λειτουργίες προεπεξεργασίας (denoise, deskew) προσφέρουν τη μεγαλύτερη βελτίωση  
- Πώς να διαμορφώσετε μια παρουσία `OcrEngine` σε Python  
- Το πλήρες, εκτελέσιμο script που **εξάγει κείμενο από αρχεία εικόνας**  
- Συμβουλές για την αντιμετώπιση ειδικών περιπτώσεων όπως περιστρεφόμενες σαρώσεις ή εικόνες χαμηλής ανάλυσης  

Δεν απαιτούνται εξωτερικές βιβλιοθήκες πέρα από το OCR SDK, αλλά θα χρειαστείτε Python 3.8+ και μια εικόνα PNG που θέλετε να διαβάσετε.

---

![Διάγραμμα που δείχνει τα βήματα για βελτίωση της ακρίβειας OCR σε Python](image.png "Ροή εργασίας βελτίωσης ακρίβειας OCR")

*Alt text: διάγραμμα ροής βελτίωσης ακρίβειας OCR που απεικονίζει τα βήματα προεπεξεργασίας και αναγνώρισης.*

## Προαπαιτούμενα

- Python 3.8 ή νεότερη έκδοση εγκατεστημένη  
- Πρόσβαση στο OCR SDK που παρέχει `OcrEngine`, `OcrEngineSettings` και `ImagePreprocessMode` (ο κώδικας παρακάτω χρησιμοποιεί μια γενική API· αντικαταστήστε το με τις κλάσεις του προμηθευτή σας αν χρειάζεται)  
- Μια εικόνα PNG (`input.png`) τοποθετημένη σε φάκελο που μπορείτε να αναφέρετε  

Αν χρησιμοποιείτε εικονικό περιβάλλον, ενεργοποιήστε το τώρα—δεν χρειάζεται κάτι περίπλοκο, απλώς `python -m venv venv && source venv/bin/activate`.

---

## Βήμα 1: Δημιουργία της Παρουσίας του OCR Engine – Έναρξη Βελτίωσης της Ακρίβειας OCR

Το πρώτο που χρειάζεστε είναι ένα αντικείμενο OCR engine. Σκεφτείτε το ως τον εγκέφαλο που θα διαβάσει τα pixel και θα εκτυπώσει χαρακτήρες.

```python
# Step 1: Initialise the OCR engine
ocr_engine = OcrEngine()
```

Γιατί είναι σημαντικό: χωρίς engine δεν μπορείτε να εφαρμόσετε προεπεξεργασία, και η ακατέργαστη εικόνα θα τροφοδοτηθεί απευθείας στον αναγνώστη—συνήθως η χειρότερη περίπτωση για την ακρίβεια.

---

## Βήμα 2: Φόρτωση του Στόχου PNG – Προετοιμασία για Αναγνώριση Κειμένου από PNG

Τώρα λέμε στο engine ποιο αρχείο θα επεξεργαστεί. Το PNG είναι lossless, κάτι που μας δίνει μικρό πλεονέκτημα έναντι του JPEG.

```python
# Step 2: Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/input.png")
```

Αν η εικόνα βρίσκεται κάπου αλλού, απλώς προσαρμόστε τη διαδρομή. Το engine δέχεται οποιαδήποτε υποστηριζόμενη μορφή, αλλά το PNG συχνά διατηρεί τις λεπτές λεπτομέρειες που χρειάζονται για καθαρά άκρα χαρακτήρων.

---

## Βήμα 3: Διαμόρφωση Προεπεξεργασίας – Preprocess Image for OCR

Εδώ συμβαίνει η μαγεία. Δημιουργούμε ένα αντικείμενο ρυθμίσεων, ενεργοποιούμε το denoise για να αφαιρέσουμε τις κηλίδες και ενεργοποιούμε το deskew ώστε το κεκλιμένο κείμενο να ευθυγραμμιστεί αυτόματα.

```python
# Step 3: Prepare preprocessing settings to improve accuracy
preprocess_settings = OcrEngineSettings()
preprocess_settings.preprocess_mode = (
    ImagePreprocessMode.DENOISE | ImagePreprocessMode.DESKEW
)
```

### Γιατί Denoise + Deskew;

- **Denoise**: Ο τυχαίος θόρυβος pixel μπερδεύει τους αλγόριθμους αντιστοίχισης προτύπων. Η αφαίρεσή του καθαρίζει τα γράμματα.  
- **Deskew**: Ακόμη και μια κλίση 2 μπορεί να μειώσει δραματικά τις βαθμολογίες εμπιστοσύνης. Το deskew ευθυγραμμίζει τη βάση γραμμής, επιτρέποντας στον αναγνώστη να ταιριάξει τις γραμματοσειρές πιο αξιόπιστα.

Μπορείτε να πειραματιστείτε με πρόσθετες σημαίες (π.χ., `ImagePreprocessMode.CONTRAST_ENHANCE`) αν οι εικόνες σας είναι ιδιαίτερα σκοτεινές. Η τεκμηρίωση του SDK συνήθως παραθέτει όλες τις διαθέσιμες λειτουργίες.

---

## Βήμα 4: Εφαρμογή των Ρυθμίσεων στο Engine – Σύνδεση Προεπεξεργασίας με OCR

Αναθέστε το αντικείμενο ρυθμίσεων στο engine ώστε η επόμενη εκτέλεση αναγνώρισης να χρησιμοποιεί τις μετασχηματισμούς που ορίσαμε.

```python
# Step 4: Apply the settings to the engine
ocr_engine.settings = preprocess_settings
```

Αν παραλείψετε αυτό το βήμα, το engine θα επιστρέψει στις προεπιλογές του (συχνά «χωρίς προεπεξεργασία») και θα δείτε **χαμηλότερη ακρίβεια OCR**.

---

## Βήμα 5: Εκτέλεση της Διαδικασίας Αναγνώρισης – Extract Text from Image

Με όλα συνδεδεμένα, ζητάμε τελικά από το engine να κάνει τη δουλειά του. Η κλήση είναι συγχρονική, επιστρέφοντας ένα αντικείμενο αποτελέσματος που περιέχει το αναγνωρισμένο κείμενο.

```python
# Step 5: Run the recognition process
recognition_result = ocr_engine.recognize()
```

Πίσω από τις σκηνές το engine:

1. Φορτώνει το PNG στη μνήμη  
2. Εφαρμόζει denoise και deskew βάσει των ρυθμίσεών μας  
3. Εκτελεί το νευρωνικό δίκτυο ή τον κλασικό αλγόριθμο αντιστοίχισης προτύπων  
4. Συσκευάζει το αποτέλεσμα στο `recognition_result`

---

## Βήμα 6: Εμφάνιση του Αναγνωρισμένου Κειμένου – Επαλήθευση της Βελτίωσης

Ας τυπώσουμε το εξαγόμενο κείμενο. Σε μια πραγματική εφαρμογή μπορεί να το γράψετε σε αρχείο, βάση δεδομένων ή να το περάσετε σε άλλη υπηρεσία.

```python
# Step 6: Output the recognized text
print(recognition_result.text)
```

### Αναμενόμενο Αποτέλεσμα

Αν η εικόνα περιέχει τη φράση «Hello, OCR World!», θα πρέπει να δείτε:

```
Hello, OCR World!
```

Παρατηρήστε πόσο καθαρό είναι το κείμενο—χωρίς τυχαία σύμβολα ή σπασμένους χαρακτήρες. Αυτό είναι το αποτέλεσμα της σωστής **προεπεξεργασίας εικόνας για κείμενο**.

---

## Pro Tips & Edge Cases

| Κατάσταση | Τι να Ρυθμίσετε | Γιατί |
|-----------|----------------|------|
| Πολύ χαμηλή ανάλυση PNG (≤ 72 dpi) | Προσθέστε `ImagePreprocessMode.SUPER_RESOLUTION` αν είναι διαθέσιμο | Η ανύψωση μπορεί να δώσει στον αναγνώστη περισσότερα pixel για επεξεργασία |
| Το κείμενο είναι περιστραμμένο > 5° | Αυξήστε την ανοχή του deskew ή περιστρέψτε χειροκίνητα με `Pillow` πριν το δώσετε στο engine | Οι ακραίες γωνίες μερικές φορές παρακάμπτουν το αυτόματο deskew |
| Έντονα μοτίβα φόντου | Ενεργοποιήστε `ImagePreprocessMode.BACKGROUND_REMOVAL` | Αφαιρεί το μη‑κείμενο που θα μπορούσε να διαβαστεί λανθασμένα |
| Έγγραφο πολλαπλών γλωσσών | Ορίστε `ocr_engine.language = "eng+spa"` (ή παρόμοιο) | Το engine επιλέγει το σωστό σύνολο χαρακτήρων, βελτιώνοντας τη συνολική ακρίβεια |

Θυμηθείτε, **βελτιώστε την ακρίβεια OCR** δεν είναι μια λύση «ένα μέγεθος για όλους»· ίσως χρειαστεί να επαναλάβετε τις σημαίες προεπεξεργασίας για το συγκεκριμένο σας σύνολο δεδομένων.

---

## Πλήρες Script – Έτοιμο για Αντιγραφή & Επικόλληση

Παρακάτω βρίσκεται το πλήρες, εκτελέσιμο παράδειγμα που ενσωματώνει κάθε βήμα που συζητήσαμε. Αποθηκεύστε το ως `improve_ocr_accuracy.py` και τρέξτε το με `python improve_ocr_accuracy.py`.

```python
"""
Improve OCR Accuracy in Python – Full Example
Author: Your Name (2026)
Requires: OCR SDK providing OcrEngine, OcrEngineSettings, ImagePreprocessMode
"""

# Import the necessary classes from the OCR SDK
from ocr_sdk import OcrEngine, OcrEngineSettings, ImagePreprocessMode

def main():
    # 1️⃣ Initialise the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the PNG you want to read
    image_path = "YOUR_DIRECTORY/input.png"
    ocr_engine.load_image(image_path)

    # 3️⃣ Configure preprocessing: denoise + deskew
    preprocess_settings = OcrEngineSettings()
    preprocess_settings.preprocess_mode = (
        ImagePreprocessMode.DENOISE | ImagePreprocessMode.DESKEW
    )

    # 4️⃣ Apply the settings
    ocr_engine.settings = preprocess_settings

    # 5️⃣ Run recognition
    recognition_result = ocr_engine.recognize()

    # 6️⃣ Print the extracted text
    print("=== Recognized Text ===")
    print(recognition_result.text)

if __name__ == "__main__":
    main()
```

Τρέξτε το, παρακολουθήστε την κονσόλα, και θα δείτε αμέσως το αποτέλεσμα **extract text from image**. Αν το αποτέλεσμα φαίνεται λανθασμένο, προσαρμόστε τις σημαίες `preprocess_mode` όπως περιγράφεται στον πίνακα «Pro Tips».

---

## Συμπέρασμα

Μόλις περάσαμε από μια πρακτική συνταγή για **βελτίωση της ακρίβειας OCR** χρησιμοποιώντας Python. Δημιουργώντας ένα `OcrEngine`, φορτώνοντας ένα PNG, **προετοιμάζοντας την εικόνα για OCR**, και τελικά **αναγνωρίζοντας κείμενο από PNG**, μπορείτε αξιόπιστα **να εξάγετε κείμενο από αρχεία εικόνας** ακόμη και όταν η πηγή δεν είναι τέλεια.  

Τι θα κάνετε στη συνέχεια; Δοκιμάστε να επεξεργαστείτε μια δέσμη εικόνων μέσα σε βρόχο, αποθηκεύστε κάθε αποτέλεσμα σε CSV, ή πειραματιστείτε με πρόσθετες λειτουργίες προεπεξεργασίας όπως η ενίσχυση αντίθεσης. Το ίδιο μοτίβο λειτουργεί για PDF, σαρωμένα αποδείξεις ή χειρόγραφες σημειώσεις—απλώς αλλάξτε την είσοδο και προσαρμόστε τις ρυθμίσεις.

Έχετε ερωτήσεις για συγκεκριμένο τύπο εικόνας ή θέλετε να μάθετε πώς να το ενσωματώσετε σε μια web υπηρεσία; Αφήστε ένα σχόλιο και θα εξερευνήσουμε αυτά τα σενάρια μαζί. Καλό κώδικα, και εύχομαι τα αποτελέσματα OCR σας να είναι πάντα kristall‑καθαρά!

## Τι Να Μάθετε Στη Σύντομη Μελλοντική

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}