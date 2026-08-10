---
category: general
date: 2026-06-25
description: 'αναγνώριση κειμένου από png με Python: βήμα‑βήμα οδηγός για δημιουργία
  μηχανής OCR με Python, εκτέλεση OCR σε τεχνικό έγγραφο και εξαγωγή κειμένου από
  εικόνα τεχνικού εγγράφου.'
draft: false
keywords:
- recognize text from png
- ocr image to text python
- create OCR engine python
- extract text from technical document image
- run OCR on technical document
language: el
og_description: Αναγνωρίστε κείμενο από PNG χρησιμοποιώντας Python. Μάθετε πώς να
  δημιουργήσετε μηχανή OCR με Python, να εκτελέσετε OCR σε τεχνικό έγγραφο και να
  εξάγετε κείμενο από εικόνα τεχνικού εγγράφου.
og_title: Αναγνώριση κειμένου από PNG σε Python – Πλήρης οδηγός μηχανής OCR
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: 'recognize text from png with Python: step‑by‑step guide to create
    OCR engine python, run OCR on technical document and extract text from technical
    document image.'
  headline: Recognize Text from PNG in Python – Complete OCR Engine Guide
  type: TechArticle
- description: 'recognize text from png with Python: step‑by‑step guide to create
    OCR engine python, run OCR on technical document and extract text from technical
    document image.'
  name: Recognize Text from PNG in Python – Complete OCR Engine Guide
  steps:
  - name: Low‑Resolution Images
    text: 'If the PNG originates from a scanned fax, you might be dealing with 72
      dpi. OCR accuracy drops dramatically below 150 dpi. A quick fix is to upscale
      the image using a bicubic algorithm before recognition:'
  - name: Rotated Pages
    text: 'Technical manuals sometimes come scanned at an angle. The engine can auto‑deskew,
      but you can also pre‑rotate:'
  - name: Multi‑Page Documents
    text: 'When you need to **run OCR on technical document** PDFs that have been
      exported to PNG per page, wrap the logic in a loop:'
  - name: Language Selection
    text: 'Aspose OCR defaults to English, but you can switch to other languages (e.g.,
      German) by loading the appropriate language pack:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Αναγνώριση κειμένου από PNG σε Python – Πλήρης οδηγός μηχανής OCR
url: /el/python-java/general/recognize-text-from-png-in-python-complete-ocr-engine-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση Κειμένου από PNG σε Python – Οδηγός Πλήρους Μηχανής OCR

Ποτέ χρειάστηκε να **recognize text from PNG** αρχεία αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη Python να επιλέξετε; Δεν είστε οι μόνοι. Είτε ψηφιοποιείτε σαρωμένα εγχειρίδια, είτε εξάγετε σειριακούς αριθμούς από ετικέτες προϊόντων, είτε εξάγετε δεδομένα από εικόνα τεχνικού εγγράφου, μια αξιόπιστη αλυσίδα OCR μπορεί να σας εξοικονομήσει ώρες χειροκίνητης αντιγραφής‑επικόλλησης.

Σε αυτό το tutorial θα περάσουμε από ένα πρακτικό παράδειγμα που δείχνει πώς να **create OCR engine python**, να του δώσουμε ένα PNG και να **extract text from technical document image** με λίγες μόνο γραμμές κώδικα. Στο τέλος θα ξέρετε επίσης πώς να **run OCR on technical document** αρχεία διαφορετικής ποιότητας και θα έχετε ένα επαναχρησιμοποιήσιμο script έτοιμο για το επόμενο project σας.

## Τι Θα Μάθετε

- Εγκαταστήστε και ρυθμίστε μια βιβλιοθήκη OCR για Python (χρησιμοποιείται η Aspose OCR, αλλά τα βήματα ισχύουν για τις περισσότερες σύγχρονες πακέτα OCR).  
- **Create OCR engine python** instance και διαμορφώστε ένα προσαρμοσμένο λεξικό για ορολογία ειδικού τομέα.  
- Φορτώστε μια εικόνα PNG, εκτελέστε το OCR, και **recognize text from png** αποδοτικά.  
- Αντιμετωπίστε κοινά προβλήματα όπως χαμηλή ανάλυση, περιστρεφόμενες σελίδες και θορυβώδη υπόβαθρα.  
- Επεκτείνετε το script για batch‑process πολλαπλά τεχνικά έγγραφα.

> **Prerequisites** – Πρέπει να έχετε εγκατεστημένο το Python 3.8+ , βασική εξοικείωση με το pip, και μια εικόνα PNG που περιέχει κείμενο αναγνώσιμο από μηχανή. Δεν απαιτείται προηγούμενη εμπειρία OCR.

---

## Βήμα 1: Εγκατάσταση της Βιβλιοθήκης OCR (Create OCR Engine Python)

Πρώτα απ’ όλα: χρειαζόμαστε μια βιβλιοθήκη που πραγματικά κάνει το σκληρό έργο. Η Aspose OCR for Python via .NET είναι εμπορική επιλογή που προσφέρει υψηλή ακρίβεια έτοιμη για χρήση, αλλά το ίδιο μοτίβο λειτουργεί και με ανοιχτού κώδικα εναλλακτικές όπως το `pytesseract`. Για να κρατήσουμε το παράδειγμα αυτό‑συνεπές, θα χρησιμοποιήσουμε την Aspose OCR.

```bash
pip install aspose-ocr
```

> **Pro tip:** Αν αντιμετωπίσετε σφάλματα δικαιωμάτων στα Windows, εκτελέστε την εντολή από PowerShell με δικαιώματα διαχειριστή ή προσθέστε `--user` στο τέλος.

Μόλις εγκατασταθεί, μπορείτε να εισάγετε το module και να δημιουργήσετε μια μηχανή:

```python
import aspose.ocr as ocr
```

Αυτή η μοναδική γραμμή εισαγωγής σας δίνει πρόσβαση στην κλάση `OcrEngine`, η οποία αποτελεί τη βάση του **creating an OCR engine python**.

## Βήμα 2: Αρχικοποίηση της Μηχανής OCR και Ρύθμιση (Run OCR on Technical Document)

Τώρα θα δημιουργήσουμε την μηχανή και προαιρετικά θα της δώσουμε ένα προσαρμοσμένο λεξικό. Ένα προσαρμοσμένο λεξικό είναι μια λίστα λέξεων που το OCR πρέπει να θεωρεί έγκυρες — ιδανικό για τεχνική ορολογία, κωδικούς προϊόντων ή εσωτερικά ακρωνύμια.

```python
# Step 2: Create an OCR engine instance
engine = ocr.OcrEngine()

# Optional: define a custom dictionary for domain‑specific terms
engine.custom_dictionary = [
    "AsposeOCR", "OCRSDK", "Invoice#2026", "SKU-12345"
]
```

Γιατί να ασχοληθούμε με λεξικό; Σκεφτείτε ότι σαρώνετε ένα εγχειρίδιο συντήρησης που αναφέρει επανειλημμένα το “SKU‑12345”. Χωρίς λεξικό το OCR μπορεί να το διαβάσει ως “SKU‑12345” ή ακόμη και “S K U‑12345”. Προσθέτοντας τον όρο στο `custom_dictionary`, βελτιώνετε δραστικά την ακρίβεια του **ocr image to text python** για εκείνο το συγκεκριμένο έγγραφο.

## Βήμα 3: Φόρτωση της Εικόνας PNG (Extract Text from Technical Document Image)

Στη συνέχεια, φορτώνουμε το PNG που περιέχει το κείμενο που θέλουμε να **recognize text from png**. Η Aspose OCR υποστηρίζει ποικίλες μορφές εικόνας, αλλά το PNG είναι καλή επιλογή επειδή διατηρεί την απώλεια‑απώλειας ποιότητα.

```python
# Step 3: Load the image file
image_path = "YOUR_DIRECTORY/technical_doc.png"
image = ocr.Image.load(image_path)
```

Αν το PNG σας είναι ασυνήθιστα μεγάλο (π.χ. ένα σαρωμένο σχέδιο), ίσως θελήσετε να το μειώσετε πριν το OCR ώστε η χρήση μνήμης να παραμείνει λογική:

```python
# Optional downscale for huge images
max_dim = 2000  # pixels
if max(image.width, image.height) > max_dim:
    scale = max_dim / max(image.width, image.height)
    image = image.resize(int(image.width * scale), int(image.height * scale))
```

## Βήμα 4: Εκτέλεση του OCR (OCR Image to Text Python)

Με τη μηχανή έτοιμη και την εικόνα φορτωμένη, η πραγματική αναγνώριση είναι μια κλήση μεθόδου:

```python
# Step 4: Run OCR on the loaded image
result = engine.recognize(image)
```

Στο παρασκήνιο, το `engine.recognize` εκτελεί μια αλυσίδα βημάτων προεπεξεργασίας — δυαδικοποίηση, διόρθωση κλίσης, ανάλυση διάταξης — πριν περάσει το καθαρισμένο bitmap στο νευρωνικό δίκτυο. Γι’ αυτό μια μόνο γραμμή μπορεί να **run OCR on technical document** αρχεία που διαφορετικά θα μπέρδευαν αφελή scripts.

## Βήμα 5: Έξοδος του Αναγνωρισμένου Κειμένου (Recognize Text from PNG)

Τέλος, εκτυπώνουμε το εξαγόμενο κείμενο. Μπορείτε επίσης να το γράψετε σε αρχείο, να το εισάγετε σε βάση δεδομένων ή να το περάσετε σε επόμενες pipelines NLP.

```python
# Step 5: Output the recognized text
print("=== OCR Result ===")
print(result.text)
```

Αν τρέξετε το script με ένα έγκυρο PNG, θα δείτε κάτι σαν:

```
=== OCR Result ===
Invoice #2026
Product: AsposeOCR SDK
SKU-12345
Total: $1,299.00
```

> **Image Example**  
> ![recognize text from png output](images/ocr_result.png)  
> *Alt text:* *recognize text from png – δείγμα αποτελέσματος OCR που εμφανίζεται στην κονσόλα.*

Αυτή η λήψη οθόνης δείχνει μια καθαρή εξαγωγή όπου το προσαρμοσμένο λεξικό μας διατήρησε αμετάβλητο τον κωδικό προϊόντος.

---

## Βαθύτερη Εξέταση: Διαχείριση Συνηθισμένων Ακραίων Περιπτώσεων

### Εικόνες Χαμηλής Ανάλυσης

Αν το PNG προέρχεται από fax σαρωμένο, μπορεί να έχετε 72 dpi. Η ακρίβεια του OCR πέφτει δραματικά κάτω από 150 dpi. Μια γρήγορη λύση είναι η αύξηση της ανάλυσης της εικόνας με αλγόριθμο bicubic πριν την αναγνώριση:

```python
if image.dpi < 150:
    image = image.resize(image.width * 2, image.height * 2, interpolation=ocr.InterpolationMode.BICUBIC)
```

### Περιστρεφόμενες Σελίδες

Τα τεχνικά εγχειρίδια μερικές φορές σαρώνουν υπό γωνία. Η μηχανή μπορεί να διορθώσει αυτόματα την κλίση, αλλά μπορείτε επίσης να προ-στρέψετε:

```python
# Detect and correct rotation
angle = engine.auto_rotate(image)
if angle != 0:
    image = image.rotate(-angle)
```

### Πολυσελιδή Έγγραφα

Όταν χρειάζεται να **run OCR on technical document** PDF που έχουν εξαχθεί σε PNG ανά σελίδα, τυλίξτε τη λογική σε βρόχο:

```python
import glob

for png_path in sorted(glob.glob("pages/*.png")):
    img = ocr.Image.load(png_path)
    txt = engine.recognize(img).text
    with open("output.txt", "a", encoding="utf-8") as f:
        f.write(f"--- Page {png_path} ---\n{txt}\n\n")
```

### Επιλογή Γλώσσας

Η Aspose OCR προεπιλογή είναι τα Αγγλικά, αλλά μπορείτε να μεταβείτε σε άλλες γλώσσες (π.χ. Γερμανικά) φορτώνοντας το αντίστοιχο language pack:

```python
engine.language = ocr.Language.German
```

Αυτό είναι χρήσιμο όταν το **extract text from technical document image** περιλαμβάνει πολυγλωσσικούς πίνακες ή προδιαγραφές.

---

## Πλήρες Λειτουργικό Script

Παρακάτω βρίσκεται το πλήρες, έτοιμο‑για‑εκτέλεση script που ενώνει όλα τα παραπάνω. Αποθηκεύστε το ως `ocr_technical_doc.py` και αντικαταστήστε το `YOUR_DIRECTORY/technical_doc.png` με τη διαδρομή του PNG σας.



## Τι Θα Μάθετε Στη Στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετα χαρακτηριστικά του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}