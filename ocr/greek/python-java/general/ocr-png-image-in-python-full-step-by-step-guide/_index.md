---
category: general
date: 2026-06-06
description: OCR PNG εικόνας με Python – μάθετε πώς να εξάγετε κείμενο από εικόνα,
  να τρέξετε ένα παράδειγμα OCR σε Python και ακόμη να διαβάζετε εύκολα αρχαίο ελληνικό
  κείμενο.
draft: false
keywords:
- ocr png image
- extract text from image
- python ocr example
- read ancient greek
- recognize image text
language: el
og_description: OCR PNG εικόνα σε Python εξηγείται. Αυτός ο οδηγός δείχνει πώς να
  εξάγετε κείμενο από εικόνα, να τρέξετε ένα παράδειγμα OCR σε Python και να διαβάσετε
  αρχαία ελληνικά με ευκολία.
og_title: OCR PNG Εικόνα σε Python – Πλήρης Οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  headline: OCR PNG Image in Python – Full Step‑by‑Step Guide
  type: TechArticle
- description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  name: OCR PNG Image in Python – Full Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Why it matters | |-------------|----------------| | Python
      3.8+ | Modern syntax and type hints | | `pytesseract` package | Thin wrapper
      around the Tesseract engine | | Tesseract OCR binaries (≥ 5.0) | The actual
      engine that does the heavy lifting | | Greek language data (`grc.trained'
  - name: How do I improve accuracy on a noisy PNG?
    text: '- Convert the image to grayscale: `img = img.convert(''L'')` - Apply a
      binary threshold: `img = img.point(lambda x: 0 if x < 128 else 255, ''1'')`
      - Upscale with `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`'
  - name: Can I process a whole folder of PNGs?
    text: Absolutely. Wrap the `recognize_image` call in a `for` loop over `Path.glob("*.png")`.
      Store each result in a dictionary or write to a CSV for later analysis.
  - name: What if I need to extract numbers only?
    text: 'Pass a custom **config** string to `image_to_string`:'
  - name: Is there a way to get confidence scores?
    text: Yes—use `pytesseract.image_to_data` which returns a TSV with confidence
      per word. You can filter out low‑confidence tokens before assembling the final
      string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR εικόνας PNG σε Python – Πλήρης οδηγός βήμα‑βήμα
url: /el/python-java/general/ocr-png-image-in-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR PNG Image σε Python – Πλήρης Οδηγός Βήμα‑βήμα

Έχετε ποτέ αναρωτηθεί πώς να **OCR PNG image** αρχεία απευθείας από ένα script Python; Ίσως έχετε έναν φάκελο γεμάτο σαρωμένα αρχαία χειρόγραφα και χρειάζεται να **extract text from image** αρχεία χωρίς να πληκτρολογείτε τα πάντα χειροκίνητα. Τα καλά νέα είναι ότι δεν χρειάζεστε διδακτορικό στην υπολογιστική όραση—απλώς μερικές γραμμές κώδικα και τη σωστή βιβλιοθήκη, και θα διαβάζετε αρχαία ελληνικά σε δευτερόλεπτα.

Σε αυτό το tutorial θα περάσουμε από ένα **python OCR example** που αναγνωρίζει κείμενο από ένα PNG, ορίζει τη γλώσσα σε Ελληνικά πολυτονικά και εκτυπώνει το αποτέλεσμα. Στο τέλος θα ξέρετε ακριβώς πώς να **recognize image text**, να αντιμετωπίσετε κοινά προβλήματα και να προσαρμόσετε το script για άλλες γλώσσες ή μορφές εικόνας.

## Τι Θα Μάθετε

- Εγκατάσταση και ρύθμιση μιας βιβλιοθήκης Python OCR (pytesseract + Tesseract OCR)
- Δημιουργία ενός OCR engine instance και φόρτωση αρχείου PNG
- Ορισμός της γλώσσας αναγνώρισης σε Ελληνικά πολυτονικά ώστε να μπορείτε να **read ancient greek**
- Έξοδος του αναγνωρισμένου κειμένου και αντιμετώπιση τυπικών προβλημάτων
- Επέκταση του script για batch‑process πολλαπλά PNG ή αλλαγή σε άλλη γλώσσα

### Προαπαιτούμενα

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|-----------------------|
| Python 3.8+ | Σύγχρονη σύνταξη και type hints |
| `pytesseract` package | Ελαφρύ wrapper γύρω από τη μηχανή Tesseract |
| Tesseract OCR binaries (≥ 5.0) | Η πραγματική μηχανή που κάνει τη βαριά δουλειά |
| Greek language data (`grc.traineddata`) | Απαιτείται για **read ancient greek** σωστά |
| A PNG image you want to analyse (e.g., `ancient_greek.png`) | Ο στόχος μας για την επίδειξη **ocr png image** |

Μπορείτε να εγκαταστήσετε το τμήμα Python με:

```bash
pip install pytesseract Pillow
```

Και σε Ubuntu/macOS θα προσθέσετε τη μηχανή:

```bash
# Ubuntu
sudo apt-get install tesseract-ocr libtesseract-dev

# macOS (Homebrew)
brew install tesseract
```

Μην ξεχάσετε να κατεβάσετε τα Greek polytonic trained data:

```bash
wget https://github.com/tesseract-ocr/tessdata/blob/main/greek.traineddata -P /usr/share/tesseract-ocr/4.00/tessdata/
```

*(Η διαδρομή μπορεί να διαφέρει· προσαρμόστε το `TESSDATA_PREFIX` αν χρειάζεται.)*

---

## OCR PNG Image: Δημιουργία του Engine Instance

Το πρώτο πράγμα που χρειαζόμαστε είναι ένα αντικείμενο που επικοινωνεί με το Tesseract. Στο `pytesseract` η μηχανή προσπελαύνεται μέσω συναρτήσεων επιπέδου module, αλλά για σαφήνεια θα το τυλίξουμε σε μια μικρή κλάση. Αυτό αντικατοπτρίζει την έννοια του “engine” που είδατε στο αρχικό snippet.

```python
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    """
    Simple wrapper around pytesseract to keep the API similar to the original example.
    """
    def __init__(self, tess_cmd: str = "tesseract"):
        # You can point pytesseract to a custom binary if you installed it somewhere unusual.
        pytesseract.pytesseract.tesseract_cmd = tess_cmd

    def set_recognition_language(self, language: str):
        """
        Store the language code for later calls.
        Example: 'grc' for Greek polytonic.
        """
        self.lang = language

    def recognize_image(self, image_path: str):
        """
        Open the PNG, run OCR, and return the raw result object.
        """
        img = Image.open(image_path)
        # pytesseract returns a string; we wrap it for consistency with the original code.
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text=text)

class OcrResult:
    """Container for OCR output – mimics the .text attribute used in the example."""
    def __init__(self, text: str):
        self.text = text
```

**Γιατί να το τυλίξουμε;**  
- Διατηρεί το δημόσιο API ίδιο με το snippet που ξεκινήσατε, κάνοντας τη μετανάστευση απρόσκοπτη.  
- Επιτρέπει την προσθήκη logging ή error handling αργότερα χωρίς να επηρεάσουμε τη βασική ροή.  
- Δείχνει καλή πρακτική OOP—κάτι που εκτιμούν οι senior developers.

## Εξαγωγή Κειμένου από Εικόνα: Ορισμός Γλώσσας σε Ελληνικά Πολυτονικά

Τώρα που έχουμε μια μηχανή, πρέπει να της πούμε ποια γλώσσα να περιμένει. Τα Ελληνικά πολυτονικά χρησιμοποιούν διακριτικά που δεν καλύπτονται από τα τυπικά δεδομένα “greek”, έτσι δείχνουμε στο Tesseract το αρχείο `grc` trainedfile.

```python
# Step 2: Set the recognition language to Greek polytonic
engine = OcrEngine()
engine.set_recognition_language("grc")   # 'grc' is the ISO‑639‑2 code for ancient Greek
```

Αν ποτέ θέλετε να **extract text from image** αρχεία σε άλλη γλώσσα, απλώς αντικαταστήστε το `"grc"` με `"eng"` για Αγγλικά, `"fra"` για Γαλλικά κ.λπ. Η ίδια γραμμή λειτουργεί για οποιαδήποτε γλώσσα έχετε εγκατεστημένη.

## Αναγνώριση Κειμένου Εικόνας: Εκτέλεση OCR σε PNG

Με τη γλώσσα ορισμένη, τροφοδοτούμε το PNG στη μηχανή. Το αρχικό παράδειγμα χρησιμοποίησε σκληρά κωδικοποιημένη διαδρομή· θα το κάνουμε λίγο πιο ευέλικτο χρησιμοποιώντας αντικείμενα `Path`.

```python
# Step 3: Recognize text from the image file
image_path = Path("YOUR_DIRECTORY/ancient_greek.png")
ocr_result = engine.recognize_image(str(image_path))
```

**Συμβουλές & Ακραίες Περιπτώσεις**

- **File not found** – τυλίξτε την κλήση σε `try/except FileNotFoundError` για να δώσετε ένα φιλικό μήνυμα.  
- **Low‑resolution PNG** – σκεφτείτε προεπεξεργασία (π.χ., αλλαγή μεγέθους, δυαδικοποίηση) με Pillow πριν το OCR.  
- **Non‑Greek text** – το Tesseract θα προσπαθήσει ακόμη να το αποκωδικοποιήσει, αλλά η ακρίβεια μειώνεται δραστικά. Πάντα ταιριάξτε τη γλώσσα.

## Έξοδος του Αναγνωρισμένου Κειμένου

Τέλος, εκτυπώνουμε το αποτέλεσμα. Σε ένα πραγματικό πρότζεκτ μπορεί να γράψετε σε βάση δεδομένων, CSV, ή ακόμη να το περάσετε σε pipeline μετάφρασης.

```python
# Step 4: Output the recognized text
print("=== OCR Result ===")
print(ocr_result.text)
```

Όταν εκτελέσετε το script σε σαφή σάρωση μιας αρχαίας ελληνικής επιγραφής, θα πρέπει να δείτε κάτι όπως:

```
=== OCR Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος...
```

Αν η έξοδος φαίνεται ακαταλαβίστικη, ελέγξτε ξανά ότι το αρχείο **greek.traineddata** βρίσκεται στο σωστό φάκελο και ότι το PNG δεν είναι πολύ θορυβώδες.

## Πλήρες Παράδειγμα Εργασίας (Όλα τα Βήματα σε Ένα Script)

Παρακάτω είναι το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα. Αποθηκεύστε το ως `ocr_greek.py` και εκτελέστε `python ocr_greek.py`.

```python
# ocr_greek.py
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    def __init__(self, tess_cmd: str = "tesseract"):
        pytesseract.pytesseract.tesseract_cmd = tess_cmd
        self.lang = "eng"  # default fallback

    def set_recognition_language(self, language: str):
        self.lang = language

    def recognize_image(self, image_path: str):
        img = Image.open(image_path)
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text)

class OcrResult:
    def __init__(self, text: str):
        self.text = text

def main():
    # 1️⃣ Create an OCR engine instance
    engine = OcrEngine()

    # 2️⃣ Set the language to Greek polytonic (read ancient greek)
    engine.set_recognition_language("grc")

    # 3️⃣ Path to the PNG you want to analyse
    png_path = Path("YOUR_DIRECTORY/ancient_greek.png")
    if not png_path.is_file():
        raise FileNotFoundError(f"Cannot find image at {png_path}")

    # 4️⃣ Recognize and retrieve the text
    result = engine.recognize_image(str(png_path))

    # 5️⃣ Print the extracted text
    print("=== OCR PNG Image Result ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

**Αναμενόμενη έξοδος** (περιορισμένη για συντομία):

```
=== OCR PNG Image Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος·
Καὶ ὁ ἥλιος ἀνατέλλει·
```

Αν δείτε τους σωστούς ελληνικούς χαρακτήρες, συγχαρητήρια—έχετε ολοκληρώσει με επιτυχία μια λειτουργία **ocr png image** σε Python!

## Συχνές Ερωτήσεις & Pro Συμβουλές

### Πώς βελτιώνω την ακρίβεια σε θορυβώδες PNG;

- Μετατρέψτε την εικόνα σε κλίμακα του γκρι: `img = img.convert('L')`
- Εφαρμόστε δυαδικό κατώφλι: `img = img.point(lambda x: 0 if x < 128 else 255, '1')`
- Αυξήστε την ανάλυση με `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`

Αυτά τα βήματα συχνά μετατρέπουν έναν εφιάλτη **recognize image text** σε καθαρό αποτέλεσμα.

### Μπορώ να επεξεργαστώ ολόκληρο φάκελο PNG;

Απολύτως. Τυλίξτε την κλήση `recognize_image` σε ένα `for` loop πάνω από `Path.glob("*.png")`. Αποθηκεύστε κάθε αποτέλεσμα σε ένα dictionary ή γράψτε σε CSV για μεταγενέστερη ανάλυση.

```python
for png in Path("my_folder").glob("*.png"):
    res = engine.recognize_image(str(png))
    print(f"{png.name}: {res.text[:50]}...")
```

### Τι γίνεται αν χρειάζομαι να εξάγω μόνο αριθμούς;

Περάστε μια προσαρμοσμένη συμβολοσειρά **config** στο `image_to_string`:

```python
digits = pytesseract.image_to_string(img, lang=self.lang, config='outputbase digits')
```

Με αυτόν τον τρόπο μπορείτε να **extract text from image** αρχεία που περιέχουν πίνακες, σειριακούς αριθμούς ή χρονικές σφραγίδες.

### Υπάρχει τρόπος να λάβετε βαθμούς εμπιστοσύνης;

Ναι—χρησιμοποιήστε `pytesseract.image_to_data` που επιστρέφει ένα TSV με confidence ανά λέξη. Μπορείτε να φιλτράρετε τα tokens χαμηλής εμπιστοσύνης πριν συναρτήσετε το τελικό string.

## Επέκταση του Tutorial

Τώρα που έχετε κατακτήσει τα βασικά, σκεφτείτε να εξερευνήσετε τα παρακάτω συναφή θέματα:

- **Batch OCR with multiprocessing** – επιταχύνετε μεγάλα corpora PNG.  
- **Hybrid OCR + NLP pipelines** – αυτόματη μετάφραση του εξαγόμενου αρχαίου ελληνικού σε σύγχρονα Αγγλικά.  
- **Alternative engines** – δοκιμάστε `easyocr` ή μεθόδους βασισμένες σε `opencv` για συγκεκριμένες περιπτώσεις.  
- **Cloud OCR services** – Google Vision, Azure Computer Vision, ή AWS Textract για serverless scaling.

Κάθε ένα από αυτά βασίζεται στο κεντρικό **python ocr example** που καλύψαμε, έτσι θα νιώσετε άνετα να εμβαθύνετε περαιτέρω.

## Συμπέρασμα

Μετατρέψαμε ένα απλό snippet σε μια ισχυρή ροή εργασίας **ocr png image** σε Python. Δημιουργώντας ένα `OcrEngine`, ορίζοντας τη γλώσσα σε Ελληνικά πολυτονικά, τροφοδοτώντας ένα PNG και εκτυπώνοντας το αποτέλεσμα, τώρα ξέρετε πώς να **extract text from image** αρχεία, **recognize image text**, και ακόμη **read ancient greek**.

## Τι Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}