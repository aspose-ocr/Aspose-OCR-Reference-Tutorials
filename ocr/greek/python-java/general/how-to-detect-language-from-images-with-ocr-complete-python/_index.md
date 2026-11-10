---
category: general
date: 2026-06-22
description: Μάθετε πώς να εντοπίζετε τη γλώσσα από εικόνα και να εξάγετε κείμενο
  χρησιμοποιώντας OCR στην Python. Αναλυτικός οδηγός βήμα‑βήμα που καλύπτει την αυτόματη
  ανίχνευση γλώσσας και την εξαγωγή κειμένου.
draft: false
keywords:
- how to detect language
- detect language from image
- extract text from image
- how to use ocr
- how to extract text
language: el
og_description: Πώς να εντοπίσετε τη γλώσσα από εικόνα χρησιμοποιώντας OCR; Αυτός
  ο οδηγός σας δείχνει βήμα‑βήμα πώς να χρησιμοποιήσετε το OCR στην Python για να
  εντοπίσετε τη γλώσσα και να εξάγετε κείμενο.
og_title: Πώς να εντοπίσετε τη γλώσσα από εικόνες με OCR – Πλήρης οδηγός Python
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to detect language from image and extract text using OCR
    in Python. Step‑by‑step tutorial covering automatic language detection and text
    extraction.
  headline: How to Detect Language from Images with OCR – Complete Python Guide
  type: TechArticle
- description: Learn how to detect language from image and extract text using OCR
    in Python. Step‑by‑step tutorial covering automatic language detection and text
    extraction.
  name: How to Detect Language from Images with OCR – Complete Python Guide
  steps:
  - name: Expected Output
    text: 'If `sample-multilang.png` contains French text, you might see something
      like:'
  - name: 1. Unsupported Image Formats
    text: 'If you try to load a TIFF file that the OCR library doesn’t recognise,
      `ocr.ImageStream.from_file()` will raise an `OcrUnsupportedFormatError`. Wrap
      the load call in a try/except block:'
  - name: 2. Low‑Resolution Images
    text: 'OCR accuracy drops sharply below ~300 dpi. If you notice poor detection,
      consider pre‑processing the image with Pillow:'
  - name: 3. Multiple Languages in One Image
    text: 'When an image contains text in more than one language, the auto‑detect
      feature will pick the dominant one. To capture all languages, you can disable
      auto‑detect and manually pass a list of languages to the engine:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Πώς να ανιχνεύσετε τη γλώσσα από εικόνες με OCR – Πλήρης οδηγός Python
url: /el/python-java/general/how-to-detect-language-from-images-with-ocr-complete-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ανιχνεύσετε τη γλώσσα από εικόνες με OCR – Πλήρης Οδηγός Python

Έχετε αναρωτηθεί ποτέ **πώς να ανιχνεύσετε τη γλώσσα** σε μια εικόνα χωρίς να την ανοίξετε χειροκίνητα; Δεν είστε ο μόνος. Σε πολλά έργα—σκεφτείτε σαρωτές αποδείξεων, πολύγλωσσα αρχεία εγγράφων ή μια απλή εφαρμογή φωτογραφίας‑σε‑κείμενο—πρέπει να γνωρίζετε *ποια* γλώσσα ανήκει το κείμενο πριν το επεξεργαστείτε περαιτέρω.  

Σε αυτό το σεμινάριο θα περάσουμε από ένα πρακτικό, ολοκληρωμένο παράδειγμα που δείχνει **πώς να ανιχνεύσετε τη γλώσσα** από μια εικόνα και στη συνέχεια να εξάγετε τους πραγματικούς χαρακτήρες. Στο τέλος θα μπορείτε να εκτελέσετε μερικές γραμμές Python, να στοχεύσετε το script σε οποιαδήποτε υποστηριζόμενη εικόνα και να λάβετε τόσο τη ανιχνευμένη γλώσσα *όσο* το εξαγόμενο κείμενο. Χωρίς περιττές πληροφορίες, μόνο μια σαφής λύση που μπορείτε να αντιγράψετε‑επικολλήσετε.

## Τι θα μάθετε

- Εγκατάσταση και ρύθμιση μιας ελαφριάς βιβλιοθήκης OCR σε Python.  
- Αρχικοποίηση της μηχανής OCR και ενεργοποίηση της αυτόματης ανίχνευσης γλώσσας.  
- Φόρτωση μιας εικόνας (οποιαδήποτε υποστηριζόμενη μορφή) και εκτέλεση OCR.  
- Ανάκτηση της ανιχνευμένης γλώσσας και του εξαγόμενου κειμένου.  
- Διαχείριση κοινών προβλημάτων όπως μη υποστηριζόμενες μορφές ή ασαφή αποτελέσματα γλώσσας.  

Αν έχετε ποτέ αναρωτηθεί **πώς να χρησιμοποιήσετε το OCR** για πολύγλωσσα έγγραφα, αυτός ο οδηγός σας καλύπτει.

---

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τα παρακάτω στον υπολογιστή σας:

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|------------------------|
| Python 3.9 ή νεότερο | Το πακέτο OCR που θα χρησιμοποιήσουμε στοχεύει σε σύγχρονους διερμηνείς. |
| `pip` (διαχειριστής πακέτων Python) | Απαιτείται για την εγκατάσταση της βιβλιοθήκης OCR. |
| Μια δείγμα εικόνας που περιέχει κείμενο τουλάχιστον σε μία γλώσσα (π.χ., `sample-multilang.png`) | Σας παρέχει κάτι συγκεκριμένο για δοκιμή. |
| Προαιρετικό: Εικονικό περιβάλλον (`venv` ή `conda`) | Διατηρεί τις εξαρτήσεις οργανωμένες και αποτρέπει συγκρούσεις εκδόσεων. |

> **Συμβουλή:** Αν εργάζεστε μέσα σε εικονικό περιβάλλον, ενεργοποιήστε το πριν εγκαταστήσετε το πακέτο OCR για να διατηρήσετε καθαρό το παγκόσμιο Python.

## Βήμα 1: Εγκατάσταση της βιβλιοθήκης OCR

Για αυτήν τη διαδρομή θα χρησιμοποιήσουμε το υποθετικό πακέτο `ocr` που αντικατοπτρίζει το API που φαίνεται στο απόσπασμα κώδικα. Σε πραγματικό σενάριο μπορείτε να το αντικαταστήσετε με `pytesseract`, `easyocr`, ή οποιαδήποτε άλλη βιβλιοθήκη που υποστηρίζει αυτόματη ανίχνευση γλώσσας.

```bash
pip install ocr
```

> **Σημείωση:** Το πακέτο είναι ελαφρύ (< 5 MB) και λειτουργεί σε Windows, macOS και Linux. Αν αντιμετωπίσετε σφάλματα δικαιωμάτων, προσθέστε `--user` στην εντολή.

## Βήμα 2: Αρχικοποίηση της μηχανής OCR – Πώς να ανιχνεύσετε τη γλώσσα

Τώρα που η βιβλιοθήκη είναι έτοιμη, μπορούμε να δημιουργήσουμε μια παρουσία της μηχανής OCR. Αυτό είναι το αντικείμενο που θα σαρώσει πραγματικά την εικόνα και θα προσδιορίσει τη γλώσσα.

```python
import ocr

# Initialise the OCR engine – this is where we start the language detection pipeline
engine = ocr.OcrEngine()
```

Γιατί ξεκινάμε με μια μηχανή; Σκεφτείτε τη μηχανή ως τον εγκέφαλο του συστήματος OCR· διατηρεί τις ρυθμίσεις, φορτώνει μοντέλα γλώσσας και διαχειρίζεται τις βαριές εργασίες στο παρασκήνιο. Η αρχικοποίησή της πρώτα εξασφαλίζει ότι τυχόν επόμενες κλήσεις (όπως η φόρτωση μιας εικόνας) έχουν ένα πλαίσιο λειτουργίας.

## Βήμα 3: Φόρτωση της εικόνας σας και ενεργοποίηση της αυτόματης ανίχνευσης γλώσσας

Το επόμενο βήμα είναι να περάσουμε την εικόνα στη μηχανή. Θα ενεργοποιήσουμε επίσης τη σημαία *auto‑detect language* ώστε η μηχανή OCR να προσπαθήσει να μαντέψει τη γλώσσα άμεσα.

```python
# Load the image (any supported format – PNG, JPEG, BMP, etc.)
image_path = "YOUR_DIRECTORY/sample-multilang.png"
image = ocr.ImageStream.from_file(image_path)

# Attach the image to the engine
engine.set_image(image)

# Enable automatic language detection – this is the key for detecting language from image
engine.get_settings().set_auto_detect_language(True)
```

> **Γιατί να ενεργοποιήσετε το auto‑detect;**  
> Οι περισσότερες βιβλιοθήκες OCR έρχονται με προεπιλεγμένη γλώσσα (συχνά Αγγλικά). Αν το έγγραφό σας περιέχει Γαλλικά, Ιαπωνικά ή οποιοδήποτε άλλο σύστημα γραφής, η μηχανή θα το χάσει χωρίς αυτή τη ρύθμιση. Με την εναλλαγή `set_auto_detect_language(True)`, επιτρέπουμε στη μηχανή να σαρώσει το bitmap, να συγκρίνει στατιστικά σχήματος χαρακτήρων και να επιλέξει το πιο πιθανό μοντέλο γλώσσας.

## Βήμα 4: Εκτέλεση OCR – Εξαγωγή κειμένου από την εικόνα

Με την εικόνα φορτωμένη και την ανίχνευση γλώσσας ενεργοποιημένη, το πραγματικό βήμα OCR είναι απλώς μια κλήση μεθόδου.

```python
# Run the OCR process – this both detects the language and extracts the text
result = engine.recognize()
```

Η μέθοδος `recognize()` κάνει δύο πράγματα στο παρασκήνιο:

1. **Ανίχνευση γλώσσας:** Εκτελεί έναν ελαφρύ ταξινομητή πάνω στην εικόνα για να επιλέξει έναν κωδικό γλώσσας (π.χ., `en`, `fr`, `es`).  
2. **Εξαγωγή κειμένου:** Στη συνέχεια εφαρμόζει το κατάλληλο μοντέλο συγκεκριμένης γλώσσας για να μεταγράψει τους χαρακτήρες σε συμβολοσειρές Unicode.

Επειδή και οι δύο ενέργειες συμβαίνουν ταυτόχρονα, λαμβάνετε ένα μοναδικό αντικείμενο `result` που περιέχει όλα όσα χρειάζεστε.

## Βήμα 5: Ανάκτηση και εμφάνιση της ανιχνευμένης γλώσσας και του εξαγόμενου κειμένου

Τέλος, εξάγουμε τον κωδικό γλώσσας και το ακατέργαστο κείμενο από το αντικείμενο `result` και τα εκτυπώνουμε στην κονσόλα.

```python
# Print the detected language and the extracted text
print("Detected language:", result.get_language())
print("Text:", result.get_text())
```

### Αναμενόμενο Αποτέλεσμα

Αν το `sample-multilang.png` περιέχει κείμενο στα Γαλλικά, μπορεί να δείτε κάτι όπως:

```
Detected language: fr
Text: Bonjour, ceci est un texte d'exemple.
```

Αν η εικόνα είναι ασαφής ή περιέχει πολλές γλώσσες, η μηχανή θα επιστρέψει τη γλώσσα στην οποία είναι πιο σίγουρη, και μπορείτε αργότερα να ελέγξετε το σκορ εμπιστοσύνης (οι περισσότερες βιβλιοθήκες εκθέτουν μια μέθοδο `get_confidence()` για προχωρημένες περιπτώσεις χρήσης).

## Διαχείριση Συνηθισμένων Ακραίων Περιπτώσεων

### 1. Μη υποστηριζόμενες μορφές εικόνας

Αν προσπαθήσετε να φορτώσετε ένα αρχείο TIFF που η βιβλιοθήκη OCR δεν αναγνωρίζει, το `ocr.ImageStream.from_file()` θα εγείρει ένα `OcrUnsupportedFormatError`. Τυλίξτε την κλήση φόρτωσης σε μπλοκ try/except:

```python
try:
    image = ocr.ImageStream.from_file(image_path)
except ocr.OcrUnsupportedFormatError as e:
    print(f"Unsupported format: {e}")
    raise
```

### 2. Εικόνες χαμηλής ανάλυσης

Η ακρίβεια του OCR μειώνεται απότομα κάτω από ~300 dpi. Αν παρατηρήσετε κακή ανίχνευση, σκεφτείτε την προεπεξεργασία της εικόνας με Pillow:

```python
from PIL import Image, ImageEnhance

pil_img = Image.open(image_path)
pil_img = pil_img.resize((pil_img.width * 2, pil_img.height * 2), Image.LANCZOS)
pil_img.save("resized.png")
image = ocr.ImageStream.from_file("resized.png")
```

### 3. Πολλαπλές γλώσσες σε μία εικόνα

Όταν μια εικόνα περιέχει κείμενο σε περισσότερες από μία γλώσσες, η λειτουργία auto‑detect θα επιλέξει τη κυρίαρχη. Για να καταγράψετε όλες τις γλώσσες, μπορείτε να απενεργοποιήσετε το auto‑detect και να περάσετε χειροκίνητα μια λίστα γλωσσών στη μηχανή:

```python
engine.get_settings().set_auto_detect_language(False)
engine.get_settings().set_languages(["en", "fr", "de"])
```

Τώρα το OCR θα προσπαθήσει να αναγνωρίσει χαρακτήρες χρησιμοποιώντας κάθε μοντέλο γλώσσας και θα επιστρέψει την καλύτερη αντιστοίχηση για κάθε μπλοκ κειμένου.

## Πλήρες Script – Όλα τα Βήματα Συνδυασμένα

Παρακάτω βρίσκεται το πλήρες, έτοιμο‑για‑εκτέλεση script Python που ενσωματώνει όλα όσα καλύψαμε. Αποθηκεύστε το ως `detect_language_ocr.py` και τρέξτε `python detect_language_ocr.py`.

```python
# detect_language_ocr.py
# -------------------------------------------------
# How to detect language from image and extract text using OCR
# -------------------------------------------------

import ocr

def main():
    # 1️⃣ Initialise the OCR engine
    engine = ocr.OcrEngine()

    # 2️⃣ Load the image (any supported format)
    image_path = "YOUR_DIRECTORY/sample-multilang.png"
    try:
        image = ocr.ImageStream.from_file(image_path)
    except ocr.OcrUnsupportedFormatError as err:
        print(f"Error loading image: {err}")
        return

    engine.set_image(image)

    # 3️⃣ Enable automatic language detection
    engine.get_settings().set_auto_detect_language(True)

    # 4️⃣ Perform OCR – this both detects language and extracts text
    try:
        result = engine.recognize()
    except ocr.OcrRecognitionError as err:
        print(f"OCR failed: {err}")
        return

    # 5️⃣ Retrieve and display the detected language and extracted text
    print("Detected language:", result.get_language())
    print("Text:", result.get_text())

if __name__ == "__main__":
    main()
```

**Τρέξτε το** και θα δείτε αμέσως τον κωδικό γλώσσας ακολουθούμενο από το εξαγόμενο κείμενο. Αυτή είναι η πλήρης απάντηση στο **πώς να ανιχνεύσετε τη γλώσσα** και **πώς να εξάγετε κείμενο** από μια εικόνα χρησιμοποιώντας OCR.

## Περαιτέρω – Επόμενα Βήματα & Σχετικά Θέματα

- **Βελτιώστε την ακρίβεια**: Πειραματιστείτε με την προεπεξεργασία εικόνας (κατώφλι, αποθορυβοποίηση) χρησιμοποιώντας `opencv-python`.  
- **Επεξεργασία σε παρτίδες**: Τυλίξτε το script σε βρόχο για να διαχειριστείτε έναν φάκελο γεμάτο εικόνες.  
- **Ενσωμάτωση με NLP**: Περάστε το εξαγόμενο κείμενο σε μια βιβλιοθήκη αναγνώρισης γλώσσας όπως `langdetect` για δεύτερη γνώμη.  
- **Εξερευνήστε άλλες μηχανές OCR**: Το `pytesseract` προσφέρει λεπτομερή έλεγχο, ενώ το `easyocr` υποστηρίζει πάνω από 80 γλώσσες έτοιμες προς χρήση.  

Όλα αυτά τα θέματα συνδέονται με τις δευτερεύουσες λέξεις‑κλειδιά μας—*detect language from image*, *extract text from image*, *how to use OCR*, και *how to extract text*—ώστε να μπορείτε να επεκτείνετε το σύνολο εργαλείων σας χωρίς να ξεκινάτε από το μηδέν.

## Συμπέρασμα

Μόλις καλύψαμε **πώς να ανιχνεύσετε τη γλώσσα** από μια εικόνα, περάσαμε από τον ακριβή κώδικα που απαιτείται και εξηγήσαμε γιατί κάθε βήμα είναι σημαντικό. Αρχικοποιώντας τη μηχανή OCR, φορτώνοντας την εικόνα, ενεργοποιώντας την αυτόματη ανίχνευση γλώσσας και τελικά καλώντας το `recognize()`, λαμβάνετε τόσο τον αναγνωριστικό γλώσσας όσο και το εξαγόμενο κείμενο σε μια καθαρή λειτουργία.

Τώρα μπορείτε να ενσωματώσετε αυτή τη λογική σε μεγαλύτερες εφαρμογές—είτε πρόκειται για υπηρεσία σάρωσης αποδείξεων, πολύγλωσσο chatbot, ή μια απλή επιτραπέζια βοηθητική εφαρμογή. Η βασική ιδέα παραμένει η ίδια: αφήστε τη μηχανή OCR να κάνει το σκληρό έργο, και στη συνέχεια χρησιμοποιήστε τα αποτελέσματα όπως θέλετε.

Έχετε ερωτήσεις σχετικά με ακραίες περιπτώσεις ή θέλετε να μοιραστείτε μια ενδιαφέρουσα χρήση; Αφήστε ένα σχόλιο παρακάτω. Καλή προγραμματιστική, και απολαύστε τη μετατροπή εικόνων σε αναζητήσιμο κείμενο!  

![πώς να ανιχνεύσετε τη γλώσσα από εικόνα](ocr-demo.png "Στιγμιότυπο οθόνης που δείχνει πώς να ανιχνεύσετε τη γλώσσα από εικόνα χρησιμοποιώντας Python OCR")

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω σεμινάρια καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή κειμένου από εικόνα με Aspose OCR – Οδηγός βήμα‑βήμα](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Πώς να χρησιμοποιήσετε το AspOCR: Φίλτρα προεπεξεργασίας εικόνας OCR για .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}