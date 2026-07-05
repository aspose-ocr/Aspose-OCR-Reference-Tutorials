---
category: general
date: 2026-07-05
description: Πώς να ορίσετε τη γλώσσα στο Aspose OCR χρησιμοποιώντας Python. Μάθετε
  πώς να χρησιμοποιείτε OCR, πώς να εξάγετε κείμενο από εικόνες PNG και πώς να μετατρέψετε
  εικόνα σε κείμενο με Python σε λίγα λεπτά.
draft: false
keywords:
- how to set language
- how to use ocr
- how to extract text
- extract text png
- image to text python
language: el
og_description: Πώς να ορίσετε τη γλώσσα στο Aspose OCR χρησιμοποιώντας Python. Αυτός
  ο οδηγός δείχνει πώς να χρησιμοποιήσετε το OCR, να εξάγετε κείμενο από αρχεία PNG
  και να πραγματοποιήσετε μετατροπές εικόνας σε κείμενο με Python.
og_title: Πώς να ορίσετε τη γλώσσα στο Aspose OCR με Python – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to set language in Aspose OCR using Python. Learn how to use OCR,
    how to extract text from PNG images, and convert image to text python in minutes.
  headline: How to Set Language in Aspose OCR with Python – Full Guide
  type: TechArticle
- description: How to set language in Aspose OCR using Python. Learn how to use OCR,
    how to extract text from PNG images, and convert image to text python in minutes.
  name: How to Set Language in Aspose OCR with Python – Full Guide
  steps:
  - name: Alternative Language Options
    text: 'If your image contains **Cyrillic** or **Arabic**, just swap the enum:'
  - name: Expected Output
    text: 'Assuming `input.png` contains the phrase “Hello, World!” you’ll see:'
  - name: 1. Blurry Images Yield Garbage
    text: '- **Solution:** Pre‑process the image (increase contrast, sharpen). Aspose
      OCR offers built‑in filters, e.g., `engine.image_preprocessing = ocr.ImagePreprocessing.AUTO`.'
  - name: 2. Wrong Language Produces Missing Accents
    text: '- **Solution:** Double‑check that you called `engine.language = ocr.Language.LATIN_EXTENDED`
      **before** calling `recognize`. Changing the language after recognition has
      no effect.'
  - name: 3. License Not Found → Evaluation Watermark
    text: '- **Solution:** Verify the path to `Aspose.OCR.Java.lic`. Use an absolute
      path or `os.path.join(os.getcwd(), "license", "Aspose.OCR.Java.lic")` to avoid
      relative‑path surprises.'
  type: HowTo
tags:
- OCR
- Python
- Aspose
title: Πώς να ορίσετε τη γλώσσα στο Aspose OCR με Python – Πλήρης οδηγός
url: /el/python-java/general/how-to-set-language-in-aspose-ocr-with-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ορίσετε τη γλώσσα στο Aspose OCR με Python – Πλήρης Οδηγός

Η ρύθμιση της γλώσσας στο Aspose OCR χρησιμοποιώντας Python είναι συχνά το πρώτο βήμα για την απόκτηση ακριβών αποτελεσμάτων. Σε αυτό το tutorial θα σας καθοδηγήσουμε πώς να ορίσετε τη γλώσσα, πώς να χρησιμοποιήσετε το OCR και πώς να εξάγετε κείμενο από μια εικόνα PNG—όλα σε ένα ενιαίο, εκτελέσιμο script.

Αν έχετε ποτέ κοιτάξει ένα θολό screenshot και αναρωτηθείτε αν μπορείτε να το μετατρέψετε μαγικά σε επεξεργάσιμο κείμενο, βρίσκεστε στο σωστό μέρος. Θα καλύψουμε τα πάντα, από την άδεια της βιβλιοθήκης μέχρι την εκτύπωση του αναγνωρισμένου κειμένου, και θα προσθέσουμε πρακτικές συμβουλές ώστε να μην πέσετε στα συνήθη εμπόδια.

## Προαπαιτούμενα — Τι Θα Χρειαστείτε Πριν Ξεκινήσετε

- **Python 3.8+** (οποιαδήποτε πρόσφατη έκδοση λειτουργεί)
- **pip** για την εγκατάσταση του πακέτου `aspose-ocr`
- Ένα **αρχείο άδειας Aspose OCR** (προαιρετικό αλλά συνιστάται για παραγωγή)
- Μια **εικόνα PNG** που περιέχει το κείμενο που θέλετε να διαβάσετε  
  (θα την αναφέρουμε ως `input.png` σε όλο το κείμενο)

Δεν απαιτούνται βαριές πλατφόρμες, ούτε Docker gymnastics—απλώς καθαρή Python και η βιβλιοθήκη Aspose OCR.

## Βήμα 1: Εγκατάσταση και Άδεια του Aspose OCR

Πρώτα απ' όλα, χρειάζεστε τη βιβλιοθήκη στο μηχάνημά σας. Ανοίξτε ένα τερματικό και εκτελέστε:

```bash
pip install aspose-ocr
```

Αν έχετε άδεια, τοποθετήστε το `Aspose.OCR.Java.lic` (ναι, η άδεια Java λειτουργεί και για Python) σε ασφαλές μέρος και φορτώστε την ως εξής:

```python
import asposeocr as ocr

# Load your Aspose OCR license (optional but removes evaluation limits)
ocr.License().set_license("YOUR_DIRECTORY/Aspose.OCR.Java.lic")
```

> **Pro tip:** Κρατήστε το αρχείο άδειας εκτός του φακέλου ελέγχου πηγαίου κώδικα για να αποφύγετε τυχαίες δεσμεύσεις.

## Βήμα 2: Δημιουργία του Αντικειμένου OCR Engine

Τώρα δημιουργούμε τη μηχανή που θα κάνει όλη τη βαριά δουλειά.

```python
# Create an OCR engine instance
engine = ocr.OcrEngine()
```

Το αντικείμενο `engine` είναι η πύλη σας σε κάθε δυνατότητα OCR που παρέχει η Aspose—αναγνώριση, επιλογή γλώσσας, προεπεξεργασία εικόνας, ό,τι χρειαστείτε.

## Βήμα 3: Πώς να Ορίσετε τη Γλώσσα — Διαμόρφωση Latin Extended

Εδώ λάμπει η κύρια λέξη-κλειδί. Για να πετύχετε τη μέγιστη ακρίβεια πρέπει να πείτε στη μηχανή ποιο σύνολο γλώσσας να περιμένει. Η Aspose OCR υποστηρίζει δεκάδες, αλλά για πολλά δυτικά ευρωπαϊκά κείμενα θα θέλετε **Latin Extended**.

```python
# How to set language: configure the engine to recognize Latin Extended characters
engine.language = ocr.Language.LATIN_EXTENDED
```

Γιατί είναι σημαντικό; Η ρύθμιση της γλώσσας περιορίζει το σύνολο χαρακτήρων που ψάχνει η μηχανή, μειώνοντας δραστικά τα ψευδή θετικά. Αν παραλείψετε αυτό το βήμα, μπορεί να λάβετε ακατάληπτο αποτέλεσμα, ειδικά με τόνους.

### Εναλλακτικές Επιλογές Γλώσσας

Αν η εικόνα σας περιέχει **Cyrillic** ή **Arabic**, απλώς αλλάξτε το enum:

```python
engine.language = ocr.Language.CYRILLIC      # For Russian, Bulgarian, etc.
engine.language = ocr.Language.ARABIC        # For Arabic script
```

Μπορείτε ακόμη και να συνδυάσετε πολλές γλώσσες περνώντας μια λίστα, αλλά θυμηθείτε ότι κάθε επιπλέον γλώσσα επιβραδύνει ελαφρώς την επεξεργασία.

## Βήμα 4: Φόρτωση της Εικόνας που Θέλετε να Μετατρέψετε (Εξαγωγή Κειμένου PNG)

Το επόμενο κομμάτι του παζλ είναι η τροφοδοσία της μηχανής με ένα bitmap. Η Aspose OCR μπορεί να διαβάσει πολλές μορφές, αλλά θα εστιάσουμε στο **PNG** επειδή είναι lossless και ευρέως χρησιμοποιούμενο.

```python
# Load the image that contains the text you want to recognize
image = ocr.Image.load("YOUR_DIRECTORY/input.png")
```

Αν αναρωτιέστε πώς να εξάγετε κείμενο από ένα **PNG** που βρίσκεται στο διαδίκτυο, μπορείτε πρώτα να το κατεβάσετε χρησιμοποιώντας `requests` και στη συνέχεια να περάσετε το byte array στο `ocr.Image.from_bytes()`.

```python
import requests
response = requests.get("https://example.com/sample.png")
image = ocr.Image.from_bytes(response.content)
```

## Βήμα 5: Εκτέλεση OCR και Εκτύπωση του Αποτελέσματος (Πώς να Χρησιμοποιήσετε το OCR)

Τώρα έρχεται η στιγμή της αλήθειας—εκτελέστε τη μηχανή και πάρτε το κείμενο.

```python
# Perform OCR and output the recognised text
result = engine.recognize(image)

print("Recognised text:")
print(result.text)
```

Η ιδιότητα `result.text` περιέχει το αποτέλεσμα της μετατροπής **image to text python**. Είναι μια απλή συμβολοσειρά, οπότε μπορείτε να τη γράψετε σε αρχείο, να τη δώσετε σε chatbot ή ακόμη και να κάνετε ανάλυση συναισθήματος.

### Αναμενόμενο Αποτέλεσμα

Υποθέτοντας ότι το `input.png` περιέχει τη φράση “Hello, World!” θα δείτε:

```
Recognised text:
Hello, World!
```

Αν η εικόνα περιλαμβάνει πολλαπλές γραμμές, θα διαχωρίζονται με χαρακτήρες νέας γραμμής (`\n`). Μπορείτε να τις χωρίσετε με `result.text.splitlines()` για περαιτέρω επεξεργασία.

## Βήμα 6: Συνηθισμένα Προβλήματα και Πώς να τα Διορθώσετε

### 1. Θολές Εικόνες Παράγουν Ακαταλαβίστικο Κείμενο

- **Solution:** Προ‑επεξεργαστείτε την εικόνα (αυξήστε την αντίθεση, ευκρινίστε). Η Aspose OCR προσφέρει ενσωματωμένα φίλτρα, π.χ. `engine.image_preprocessing = ocr.ImagePreprocessing.AUTO`.

### 2. Λάθος Γλώσσα Παράγει Ελλιπείς Τόνοι

- **Solution:** Επαληθεύστε ότι κάλεσατε `engine.language = ocr.Language.LATIN_EXTENDED` **πριν** καλέσετε `recognize`. Η αλλαγή της γλώσσας μετά την αναγνώριση δεν έχει καμία επίδραση.

### 3. Η Άδεια Δεν Βρέθηκε → Υδατογράφημα Αξιολόγησης

- **Solution:** Επαληθεύστε τη διαδρομή προς το `Aspose.OCR.Java.lic`. Χρησιμοποιήστε απόλυτη διαδρομή ή `os.path.join(os.getcwd(), "license", "Aspose.OCR.Java.lic")` για να αποφύγετε εκπλήξεις σχετικών διαδρομών.

## Πλήρες Παράδειγμα Εργασίας (Όλα τα Βήματα Συνδυασμένα)

Παρακάτω είναι το πλήρες script που μπορείτε να αντιγράψετε‑και‑επικολλήσετε στο `ocr_demo.py` και να τρέξετε:

```python
import asposeocr as ocr
import os

# -------------------------------------------------
# 1️⃣ Load license (optional)
# -------------------------------------------------
license_path = os.path.join("YOUR_DIRECTORY", "Aspose.OCR.Java.lic")
if os.path.exists(license_path):
    ocr.License().set_license(license_path)
    print("License loaded successfully.")
else:
    print("License not found – running in evaluation mode.")

# -------------------------------------------------
# 2️⃣ Create OCR engine
# -------------------------------------------------
engine = ocr.OcrEngine()

# -------------------------------------------------
# 3️⃣ How to set language – Latin Extended for accented chars
# -------------------------------------------------
engine.language = ocr.Language.LATIN_EXTENDED

# -------------------------------------------------
# 4️⃣ Load PNG image (extract text png)
# -------------------------------------------------
image_path = os.path.join("YOUR_DIRECTORY", "input.png")
image = ocr.Image.load(image_path)

# -------------------------------------------------
# 5️⃣ Perform OCR – how to use OCR
# -------------------------------------------------
result = engine.recognize(image)

# -------------------------------------------------
# 6️⃣ Output – how to extract text / image to text python
# -------------------------------------------------
print("\n--- Recognised text ---")
print(result.text)
```

Αποθηκεύστε το αρχείο, αντικαταστήστε το `YOUR_DIRECTORY` με τον πραγματικό φάκελο, και τρέξτε:

```bash
python ocr_demo.py
```

Θα πρέπει να δείτε το αναγνωρισμένο κείμενο εκτυπωμένο στην κονσόλα.

## Μπόνους: Αποθήκευση του Αποτελέσματος σε Αρχείο Κειμένου

Αν προτιμάτε ένα μόνιμο αρχείο αντί για έξοδο στην κονσόλα:

```python
output_path = os.path.join("YOUR_DIRECTORY", "output.txt")
with open(output_path, "w", encoding="utf-8") as f:
    f.write(result.text)
print(f"Text saved to {output_path}")
```

Τώρα έχετε ολοκληρώσει **πώς να ορίσετε τη γλώσσα**, **πώς να χρησιμοποιήσετε το OCR**, και **πώς να εξάγετε κείμενο** από ένα PNG—all in Python.

---

## Συμπέρασμα

Μόλις δείξαμε **πώς να ορίσετε τη γλώσσα** στο Aspose OCR με Python, παρουσιάσαμε **πώς να χρησιμοποιήσετε το OCR** για ανάγνωση εικόνων, και εξηγήσαμε **πώς να εξάγετε κείμενο** από ένα αρχείο PNG—ουσιαστικά μετατρέποντας μια εικόνα σε επεξεργάσιμο κείμενο χρησιμοποιώντας τεχνικές **image to text python**. Το πλήρες script είναι έτοιμο για εκτέλεση, και μπορείτε να το προσαρμόσετε για άλλες γλώσσες ή μορφές εικόνας με μια μόνο αλλαγή γραμμής.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να τροφοδοτήσετε μια δέσμη εικόνων μέσα από βρόχο, πειραματιστείτε με διαφορετικές ρυθμίσεις γλώσσας, ή ενσωματώστε το αποτέλεσμα σε μια μεγαλύτερη pipeline επεξεργασίας εγγράφων. Ο ουρανός είναι το όριο μόλις κυριαρχήσετε τα βασικά.

Έχετε ερωτήσεις για συγκεκριμένη γλώσσα ή χρειάζεστε βοήθεια με την αποσφαλμάτωση μιας δύσκολης εικόνας; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

## Τι Θα Πρέπει να Μάθετε Στη Στη συνέχεια;

Οι παρακάτω οδηγίες καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Βήμα‑βήμα](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Πώς να Κάνετε OCR σε Κείμενο Εικόνας με Γλώσσα Χρησιμοποιώντας Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}