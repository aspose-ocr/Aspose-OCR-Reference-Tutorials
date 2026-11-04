---
category: general
date: 2026-05-03
description: Εξάγετε κείμενο από εικόνα με Python χρησιμοποιώντας το Aspose OCR. Μάθετε
  έναν βήμα‑βήμα οδηγό OCR σε Python με υποστήριξη μεικτών λατινικών‑κυριλλικών.
draft: false
keywords:
- extract text from image python
- Aspose OCR Python
- image to text conversion
- mixed language OCR
- Python OCR tutorial
language: el
og_description: Αποκτήστε κείμενο από εικόνα με Python γρήγορα. Αυτός ο οδηγός δείχνει
  πώς να χρησιμοποιήσετε το Aspose OCR σε Python για εικόνες με ανάμειξη λατινικών‑κυριλλικών.
og_title: Εξαγωγή κειμένου από εικόνα με Python – Πλήρης οδηγός Aspose OCR
tags:
- OCR
- Python
- Aspose
title: Εξαγωγή κειμένου από εικόνα με Python – Πλήρης οδηγός Aspose OCR
url: /el/python-java/general/extract-text-from-image-python-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extract Text from Image Python – Complete Aspose OCR Guide

Έχετε ποτέ χρειαστεί να **extract text from image python** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη μπορεί να διαχειριστεί ένα μίγμα λατινικών και κυριλλικών χαρακτήρων; Δεν είστε οι μόνοι—οι προγραμματιστές συχνά αντιμετωπίζουν αυτό το πρόβλημα όταν κάνουν OCR σε πολυγλωσσικά screenshots.  

Το καλό νέο είναι ότι το Aspose OCR for Python κάνει όλη τη διαδικασία σχεδόν άβολη. Σε αυτό το tutorial θα περάσουμε από την εγκατάσταση του πακέτου, την εφαρμογή της άδειας, τη φόρτωση μιας εικόνας με μίξη γλωσσών, και τέλος την εξαγωγή του αναγνωρισμένου κειμένου με λίγες γραμμές κώδικα. Στο τέλος θα έχετε ένα έτοιμο script που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο.

## What You’ll Learn

- Πώς να ρυθμίσετε το **Aspose OCR Python** σε ένα εικονικό περιβάλλον.  
- Γιατί η υπόδειξη γλωσσών (όπως Λατινικά και Κυριλλικά) επιταχύνει την ανίχνευση.  
- Ο ακριβής κώδικας που χρειάζεται για **extract text from image python** με μία κλήση συνάρτησης.  
- Συνηθισμένα προβλήματα όταν δουλεύετε με OCR πολλαπλών γλωσσών και πώς να τα αποφύγετε.  

### Prerequisites

- Python 3.8 ή νεότερη εγκατεστημένη στο σύστημά σας.  
- Ένα αρχείο άδειας Aspose OCR (`Aspose.OCR.Java.lic`). Η δωρεάν δοκιμή λειτουργεί για δοκιμές, αλλά ένα αδειοδοτημένο αρχείο αφαιρεί τα υδατογραφήματα.  
- Μια εικόνα PNG/JPEG που περιέχει τόσο λατινικούς όσο και κυριλλικούς χαρακτήρες (θα την ονομάσουμε `mixed_latin_cyrillic.png`).  

Αν έχετε ελέγξει όλα τα παραπάνω, είστε έτοιμοι—δεν απαιτούνται επιπλέον frameworks ή βαριές εξαρτήσεις.

---

## Step 1 – Extract Text from Image Python: Install Aspose OCR

First thing’s first: get the library from PyPI and make sure your environment can locate the license file.

```bash
# Create a clean virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the Aspose OCR package
pip install asposeocrcloud
```

> **Pro tip:** Αν αντιμετωπίσετε σφάλμα δικαιωμάτων, προσθέστε `--user` στην εντολή `pip install` ή τρέξτε το τερματικό ως διαχειριστής.

Τώρα που το πακέτο είναι στο σύστημά σας, θα το εισάγουμε και θα κατευθύνουμε τη μηχανή στην άδειά μας.

```python
import asposeocrcloud as ocr   # the library we just installed

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Apply your license – replace the path with the actual location of your .lic file
ocr_engine.license = ocr.License()
ocr_engine.license.set_license(r"YOUR_DIRECTORY/Aspose.OCR.Java.lic")
```

Γιατί χρειάζεται άδεια σε αυτό το στάδιο; Χωρίς αυτή η μηχανή λειτουργεί σε **λειτουργία αξιολόγησης**, η οποία περιορίζει τον αριθμό των σελίδων και προσθέτει υδατογράφημα στο αποτέλεσμα. Η παροχή της άδειας εκ των προτέρων εξασφαλίζει ότι η μετέπειτα κλήση `recognize` επιστρέφει καθαρό κείμενο.

---

## Step 2 – Load Your Image with Mixed Latin‑Cyrillic Content

Next, we bring the picture into memory. Aspose OCR works with its own `Image` class, which abstracts away the underlying file format.

```python
# Load the image that contains both Latin and Cyrillic characters
input_image = ocr.Image.from_file(r"YOUR_DIRECTORY/mixed_latin_cyrillic.png")
```

Αν αναρωτιέστε αν λειτουργούν και άλλες μορφές—ναι, JPEG, BMP, TIFF, και ακόμη PDF υποστηρίζονται. Απλώς αλλάξτε την επέκταση του αρχείου και η μέθοδος `from_file` θα χειριστεί τα υπόλοιπα.

---

## Step 3 – Hint Languages for Faster Detection (Optional but Helpful)

When you know the languages present in the image, you can give the engine a heads‑up. This isn’t mandatory, but it **significantly reduces processing time** and improves accuracy for mixed‑language OCR.

```python
# Provide language hints: Latin and Cyrillic
ocr_engine.config.language_hints = ["Latin", "Cyrillic"]
```

Η λίστα `language_hints` δέχεται οποιαδήποτε γλώσσα υποστηρίζεται από το Aspose OCR (π.χ., `"Arabic"`, `"Japanese"`). Αν παραλείψετε αυτό το βήμα, η μηχανή θα δοκιμάσει κάθε ενσωματωμένη γλώσσα, κάτι που μπορεί να είναι πιο αργό σε μεγάλες δέσμες.

---

## Step 4 – Run the OCR Engine and Extract Text

Now the moment of truth: actually recognise the characters. The `recognize` method returns an `OcrResult` object that holds the plain text, confidence scores, and even bounding boxes if you need them later.

```python
# Perform OCR on the loaded image
ocr_result = ocr_engine.recognize(input_image)

# The recognised text is available via the .text attribute
extracted_text = ocr_result.text
```

> **Why this works:** Στο παρασκήνιο το Aspose OCR συνδυάζει έναν νευρωνικό ανιχνευτή κειμένου με ταξινομητές ειδικών γλωσσών. Με το να του δώσετε ένα αντικείμενο `Image`, παρακάμπτετε την ανάγκη για χειροκίνητη προεπεξεργασία όπως η δυαδικοποίηση.

---

## Step 5 – View the Extracted Text

Finally, let’s print the result to the console. In a real application you might write it to a file, push it to a database, or feed it into a translation API.

```python
print("Recognised text:")
print(extracted_text)
```

When you run the script, you should see something like:

```
Recognised text:
Hello мир! This is a test.
```

That output confirms we successfully **extract text from image python**, handling both Latin and Cyrillic characters in a single pass.

---

## Full Working Example

Below is the complete script you can copy‑paste into a file called `extract_ocr.py`. Just replace the placeholder paths with your actual directories.

```python
import asposeocrcloud as ocr   # package installed via pip

# ------------------------------------------------------------
# Step 1 – Initialise engine and apply license
# ------------------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.license = ocr.License()
ocr_engine.license.set_license(r"YOUR_DIRECTORY/Aspose.OCR.Java.lic")   # path to your license file

# ------------------------------------------------------------
# Step 2 – Load the image (mixed Latin‑Cyrillic)
# ------------------------------------------------------------
input_image = ocr.Image.from_file(r"YOUR_DIRECTORY/mixed_latin_cyrillic.png")

# ------------------------------------------------------------
# Step 3 – (Optional) Hint the languages present
# ------------------------------------------------------------
ocr_engine.config.language_hints = ["Latin", "Cyrillic"]

# ------------------------------------------------------------
# Step 4 – Run OCR
# ------------------------------------------------------------
ocr_result = ocr_engine.recognize(input_image)

# ------------------------------------------------------------
# Step 5 – Display the recognised text
# ------------------------------------------------------------
print("Recognised text:")
print(ocr_result.text)
```

Save the file, activate your virtual environment, and run:

```bash
python extract_ocr.py
```

You should see the recognised text printed, confirming the script works end‑to‑end.

---

## Frequently Asked Questions & Edge Cases

**What if the image is blurry?**  
Aspose OCR includes built‑in de‑skewing and noise reduction, but for heavily degraded photos you might want to pre‑process with OpenCV (e.g., apply a Gaussian blur and threshold). The `Image` class can also accept a NumPy array, so you can chain custom filters before calling `recognize`.

**Can I process a whole folder of images?**  
Absolutely. Wrap the logic in a `for` loop, change `from_file` to read each filename, and store the results in a dictionary. Remember to respect API rate limits if you’re using the cloud version.

**Do I need a separate license for each language?**  
No, a single Aspose OCR license covers all supported languages. The `language_hints` list is just a performance hint.

**What about PDF input?**  
Replace `Image.from_file` with `ocr.Image.from_file("document.pdf")`. The OCR engine will automatically rasterise each page and return concatenated text.

---

## Conclusion

We’ve just shown a concise, production‑ready way to **extract text from image python** using Aspose OCR. The steps—install, license, load, hint languages, recognise, and display—cover everything you need to get reliable results for mixed Latin‑Cyrillic content.  

From here you could explore advanced topics like **image to text conversion** for batch processing, integrate the output with a **Python OCR tutorial** on natural‑language processing, or experiment with other language hints for multilingual documents. The sky’s the limit, and the code is already in your hands.

Got a different use case or ran into an issue? Drop a comment, share your experience, and let’s keep the conversation going. Happy coding!  

![Extract text from image python example](/images/extract-text-from-image-python.png "Screenshot showing OCR output – extract text from image python")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}