---
category: general
date: 2026-07-05
description: Εξάγετε κείμενο από εικόνα χρησιμοποιώντας Python OCR. Μάθετε πώς να
  αναγνωρίζετε κείμενο από εικόνα, να φορτώνετε εικόνα για OCR και να ορίζετε τη γλώσσα
  OCR με λίγες μόνο γραμμές.
draft: false
keywords:
- extract text from image
- how to recognize text from image
- load image for ocr
- create ocr engine python
- set ocr language
language: el
og_description: Εξαγωγή κειμένου από εικόνα με Python OCR. Αυτός ο οδηγός δείχνει
  πώς να αναγνωρίζετε κείμενο από εικόνα, να φορτώνετε εικόνα για OCR, να δημιουργείτε
  μηχανή OCR σε στυλ Python και να ορίζετε τη γλώσσα του OCR.
og_title: Εξαγωγή κειμένου από εικόνα σε Python – Γρήγορη αναγνώριση κειμένου
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to recognize text
    from image, load image for OCR, and set OCR language in just a few lines.
  headline: Extract Text from Image in Python – Recognize Text Fast
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Εξαγωγή κειμένου από εικόνα σε Python – Γρήγορη αναγνώριση κειμένου
url: /el/python-java/general/extract-text-from-image-in-python-recognize-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Εικόνα σε Python – Αναγνώριση Κειμένου Γρήγορα

Κάποτε χρειάστηκε να **εξάγετε κείμενο από εικόνα** αλλά δεν ήξερατε ποια βιβλιοθήκη να επιλέξετε; Αν έχετε σκεφτεί *πώς να αναγνωρίσετε κείμενο από εικόνα* χωρίς να χρησιμοποιήσετε εξωτερικά εργαλεία, βρίσκεστε στο σωστό μέρος. Σε αυτό το tutorial θα δημιουργήσουμε μια μικρή μηχανή OCR, θα την κατευθύνουμε σε μια εικόνα και θα εξάγουμε το κείμενο — τίποτα παραπάνω, τίποτα παρακάτω.

Θα περάσουμε από κάθε βήμα: **δημιουργία OCR engine python**, **ρύθμιση γλώσσας OCR**, **φόρτωση εικόνας για OCR**, εκκίνηση της αναγνώρισης ασύγχρονα, και τέλος ανάγνωση του αποτελέσματος. Στο τέλος θα έχετε ένα αυτόνομο script που μπορείτε να ενσωματώσετε σε οποιοδήποτε project, είτε είναι ένας ψηφιοποιητής εγγράφων είτε ένα chatbot που διαβάζει memes.

## Τι Θα Χρειαστείτε

- Python 3.8+ (ο κώδικας λειτουργεί και σε 3.10 και νεότερες εκδόσεις)  
- Το πακέτο `ocr` (μια ελαφριά επικάλυψη γύρω από το Tesseract – εγκαταστήστε το με `pip install ocr` ή το προτιμώμενο fork σας)  
- Ένα αρχείο εικόνας (`.jpg`, `.png`, κ.λπ.) που περιέχει αναγνώσιμο κείμενο  
- Μια μικρή δόση υπομονής για το async μέρος (είναι γρήγορο, υπόσχομαι)

Αυτό είναι όλο — χωρίς βαριές εξαρτήσεις, χωρίς native builds. Αν έχετε ήδη το Tesseract στο σύστημά σας, η επικάλυψη `ocr` θα το βρει αυτόματα.

## Βήμα 1: Δημιουργία του OCR Engine – η Καρδιά της Εξαγωγής

Πρώτα απ’ όλα: χρειάζεστε ένα αντικείμενο engine που ξέρει πώς να επικοινωνεί με τη βασική μηχανή OCR. Σκεφτείτε το ως το «εγκέφαλο» που θα επεξεργαστεί αργότερα την εικόνα.

```python
import ocr

# Step 1: Instantiate the OCR engine
engine = ocr.OcrEngine()
```

*Γιατί είναι σημαντικό*: χωρίς engine δεν υπάρχει πλαίσιο για ρυθμίσεις γλώσσας ή δυνατότητες async. Η κλάση `OcrEngine` αφαιρεί τις χαμηλού επιπέδου κλήσεις γραμμής εντολών στο Tesseract, παρέχοντάς σας ένα καθαρό Python API.

## Βήμα 2: Ρύθμιση Γλώσσας OCR – πείτε στο engine τι να περιμένει

Αν το έγγραφό σας είναι στα Αγγλικά, μπορείτε να αφήσετε την προεπιλογή, αλλά είναι καλή πρακτική να το ορίσετε ρητά. Αυτό δείχνει επίσης πώς να **ρυθμίσετε τη γλώσσα OCR** για άλλες περιοχές.

```python
# Step 2: Explicitly set the language to English
engine.language = ocr.Language.ENGLISH
```

> **Pro tip**: Για πολυγλωσσικά PDF, μπορείτε να περάσετε μια λίστα όπως `[ocr.Language.ENGLISH, ocr.Language.FRENCH]`. Το engine θα προσπαθήσει και τις δύο γλώσσες αυτόματα.

## Βήμα 3: Φόρτωση Εικόνας για OCR – φέρτε την εικόνα στη μνήμη

Τώρα πραγματικά **φορτώνουμε την εικόνα για OCR**. Η επικάλυψη υποστηρίζει lazy loading, έτσι το αρχείο δεν διαβάζεται μέχρι να το χρειαστεί το engine.

```python
# Step 3: Load the image you want to process
image_path = "YOUR_DIRECTORY/large_document.jpg"
image = ocr.Image.load(image_path)
```

*Edge case*: Αν η εικόνα είναι τεράστια (πάνω από 5 MB), σκεφτείτε να την μειώσετε πρώτα για να επιταχύνετε την αναγνώριση. Μπορείτε να το κάνετε αυτό με το Pillow:

```python
from PIL import Image as PilImage

pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000))          # keep aspect ratio, max 2000px
pil_img.save("resized.jpg")
image = ocr.Image.load("resized.jpg")
```

## Βήμα 4: Έναρξη Ασύγχρονης Αναγνώρισης – μην μπλοκάρετε την εφαρμογή σας

Η εκτέλεση OCR μπορεί να διαρκέσει ένα δευτερόλεπτο ή δύο, ειδικά σε μεγάλες σαρώσεις. Η μέθοδος `recognize_async` επιστρέφει ένα future που μπορείτε να ελέγχετε αργότερα, επιτρέποντάς σας να **εκτελείτε άλλες εργασίες ενώ το OCR τρέχει στο παρασκήνιο**.

```python
# Step 4: Start the recognition asynchronously
future = engine.recognize_async(image)

# While OCR works, we can do something else
print("Processing other tasks while OCR runs...")
# Example placeholder work
for i in range(3):
    print(f"Task {i+1} done.")
```

Γιατί async; Σε έναν web server δεν θέλετε ένα μόνο αίτημα να «κολλάει» όλο το pool εργατών. Το αντικείμενο future σας δίνει έλεγχο: μπορείτε να το `await` σε async κώδικα ή να μπλοκάρετε μόνο όταν χρειάζεστε πραγματικά το αποτέλεσμα.

## Βήμα 5: Ανάκτηση του Αποτελέσματος – μπλοκάρετε μόνο όταν είναι απαραίτητο

Όταν τελικά χρειαστείτε το κείμενο, καλέστε `future.get()`. Αυτή η κλήση **μπλοκάρει μόνο εδώ**, πράγμα που σημαίνει ότι το υπόλοιπο πρόγραμμα παραμένει ανταποκρινόμενο μέχρι να ολοκληρωθεί το OCR.

```python
# Step 5: Get the recognized text (blocks here)
result = future.get()   # blocks only at this point
```

Αν βρίσκεστε μέσα σε βρόχο `asyncio`, μπορείτε αντί αυτού να `await future` — η επικάλυψη υποστηρίζει και τις δύο προσεγγίσεις.

## Βήμα 6: Χρήση του Αναγνωρισμένου Κειμένου – τα δεδομένα σας είναι έτοιμα

Τώρα που έχετε ένα αντικείμενο `result`, η λήψη του απλού string είναι τριπλή. Ας το εκτυπώσουμε και επίσης ας δούμε πώς μπορείτε να το γράψετε σε αρχείο.

```python
# Step 6: Output the OCR result
print("OCR completed:")
print(result.text)

# Optional: save to a .txt file
with open("extracted.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

**Αναμενόμενη έξοδος** (κομμένη για συντομία):

```
OCR completed:
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

Αν η εικόνα δεν περιέχει κείμενο, το `result.text` θα είναι κενή συμβολοσειρά — χειριστείτε αυτήν την περίπτωση με χάρη.

## Πλήρες Παράδειγμα Λειτουργίας – Όλα τα Βήματα σε Ένα Script

Παρακάτω είναι το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα. Αντιγράψτε‑και‑επικολλήστε, προσαρμόστε το `image_path`, και είστε έτοιμοι.

```python
import ocr
from PIL import Image as PilImage

# -------------------------------------------------
# 1️⃣ Create OCR engine
engine = ocr.OcrEngine()

# 2️⃣ Set language (English)
engine.language = ocr.Language.ENGLISH

# 3️⃣ Load image (optional resize for large files)
original_path = "YOUR_DIRECTORY/large_document.jpg"
pil_img = PilImage.open(original_path)
pil_img.thumbnail((2000, 2000))          # keep aspect ratio
pil_img.save("resized.jpg")
image = ocr.Image.load("resized.jpg")

# 4️⃣ Start async recognition
future = engine.recognize_async(image)
print("Processing other tasks while OCR runs...")
for i in range(3):
    print(f"Task {i+1} done.")

# 5️⃣ Wait for result
result = future.get()

# 6️⃣ Use the text
print("OCR completed:")
print(result.text)
with open("extracted.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

> **Note**: Αντικαταστήστε το `"YOUR_DIRECTORY/large_document.jpg"` με το πραγματικό μονοπάτι στην εικόνα σας. Το script λειτουργεί σε Windows, macOS και Linux, εφόσον το Tesseract είναι εγκατεστημένο και προσβάσιμο στο `PATH`.

## Συνηθισμένα Προβλήματα & Πώς να τα Αποφύγετε

| Πρόβλημα | Γιατί Συμβαίνει | Διόρθωση |
|----------|-----------------|----------|
| **Αχρείαστοι χαρακτήρες** | Λάθος γλώσσα ή έλλειψη αρχείων δεδομένων γλώσσας. | Βεβαιωθείτε ότι το `engine.language` ταιριάζει με το κείμενο και ότι το αντίστοιχο αρχείο `.traineddata` υπάρχει στο φάκελο `tessdata` του Tesseract. |
| **Αργή απόδοση σε μεγάλες εικόνες** | Το OCR κλιμακώνεται περίπου με τον αριθμό των pixel. | Αλλάξτε μέγεθος ή κάντε down‑sample πριν το περάσετε στο engine (δείτε το snippet Pillow). |
| **Το future δεν λυγίζει ποτέ** | Κατεστραμμένο ή μη αναγνώσιμο αρχείο εικόνας. | Τυλίξτε το `future.get()` σε try/except block και ελέγξτε `image.is_valid()` πριν την αναγνώριση. |
| **Unicode loss** |


## Τι Θα Μάθετε Στη Σειρά Επόμενη;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Extract Text from Image – OCR Optimization with Aspose OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}