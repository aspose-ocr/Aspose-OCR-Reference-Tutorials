---
category: general
date: 2026-06-19
description: Δημιουργήστε αναζητήσιμο PDF από μια εικόνα χρησιμοποιώντας Python OCR.
  Μάθετε πώς να μετατρέπετε το OCR σε PDF, να εξάγετε κείμενο από εικόνα και να εκτελείτε
  OCR σε εικόνα γρήγορα.
draft: false
keywords:
- create searchable pdf
- convert ocr to pdf
- extract text from image
- convert image to pdf
- perform ocr on image
language: el
og_description: Δημιουργήστε αναζητήσιμο PDF από μια εικόνα με Python OCR. Αυτός ο
  οδηγός δείχνει πώς να μετατρέψετε OCR σε PDF, να εξάγετε κείμενο από εικόνα και
  να εκτελέσετε OCR σε εικόνα.
og_title: Δημιουργία Αναζητήσιμου PDF σε Python – Πλήρης Οδηγός Προγραμματισμού
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  headline: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  name: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  steps:
  - name: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
    text: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
  - name: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
    text: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
  - name: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
    text: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
  type: HowTo
tags:
- OCR
- Python
- PDF
- ImageProcessing
title: Δημιουργία Αναζητήσιμου PDF σε Python – Πλήρης Οδηγός Βήμα‑βήμα
url: /el/python-java/general/create-searchable-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Αναζητήσιμου PDF σε Python – Πλήρης Οδηγός Βήμα‑βήμα

Έχετε ποτέ χρειαστεί να **δημιουργήσετε αναζητήσιμο PDF** από μια σαρωμένη απόδειξη αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν προσπαθούν για πρώτη φορά να μετατρέψουν μια εικόνα κειμένου σε PDF που μπορείτε πραγματικά να αναζητήσετε.  

Σε αυτό το tutorial θα περάσουμε βήμα-βήμα μια πρακτική λύση που σας επιτρέπει να **εφαρμόσετε OCR σε εικόνα**, να μετατρέψετε το αποτέλεσμα του OCR σε **αναζητήσιμο PDF**, και ακόμη να εξάγετε το ακατέργαστο κείμενο αν το χρειάζεστε για περαιτέρω επεξεργασία. Χωρίς περιττά, μόνο ένα λειτουργικό παράδειγμα που μπορείτε να αντιγράψετε‑επικολλήσετε στο πρόγραμμά σας σήμερα.

## Τι Θα Μάθετε

- Πώς να εγκαταστήσετε μια ελαφριά μηχανή OCR σε Python  
- Τα ακριβή βήματα για **convert OCR to PDF** και αποθήκευση ως αναζητήσιμο έγγραφο  
- Τρόπους για **extract text from image** για ανάλυση downstream  
- Συμβουλές για αντιμετώπιση κοινών προβλημάτων όπως προσανατολισμός εικόνας και μεγάλα αρχεία  
- Ένα πλήρες, εκτελέσιμο script που μπορείτε να προσαρμόσετε στη δική σας περίπτωση χρήσης

### Προαπαιτούμενα

- Python 3.8+ εγκατεστημένο στο μηχάνημά σας  
- Βασική εξοικείωση με pip και εικονικά περιβάλλοντα (προαιρετικό αλλά συνιστάται)  
- Ένα αρχείο εικόνας (PNG, JPEG, κ.λπ.) που περιέχει καθαρό, μηχανικά αναγνώσιμο κείμενο  

Αν τα έχετε αυτά, ας ξεκινήσουμε.

## Βήμα 1: Εγκατάσταση της Απαιτούμενης Βιβλιοθήκης

Το απόσπασμα κώδικα που είδατε νωρίτερα χρησιμοποιεί ένα φανταστικό πακέτο `ocr`, αλλά οι ίδιες ιδέες ισχύουν για πραγματικές βιβλιοθήκες όπως **EasyOCR**, **pytesseract**, ή **pdfminer.six**. Για αυτόν τον οδηγό θα χρησιμοποιήσουμε **EasyOCR** επειδή είναι καθαρά Python, υποστηρίζει πολλές γλώσσες, και επιστρέφει μια χρήσιμη μέθοδο μετατροπής PDF μέσω ενός βοηθητικού βοηθού.

```bash
pip install easyocr pillow
```

> **Pro tip:** Εγκαταστήστε μέσα σε ένα εικονικό περιβάλλον (`python -m venv venv && source venv/bin/activate`) για να διατηρήσετε τις εξαρτήσεις σας οργανωμένες.

## Βήμα 2: Αρχικοποίηση της Μηχανής OCR – Perform OCR on Image

Τώρα που η βιβλιοθήκη είναι έτοιμη, δημιουργούμε μια μηχανή OCR και της λέμε να δουλεύει με αγγλικό κείμενο. Αυτό είναι το πρώτο σημείο όπου **perform OCR on image**.

```python
import easyocr
from PIL import Image
import io

# Create an EasyOCR reader for English
reader = easyocr.Reader(['en'])  # ← performs OCR on image
```

Γιατί χρειάζεται ένα αφιερωμένο αντικείμενο reader; Το EasyOCR προφορτώνει τα μοντέλα γλώσσας, έτσι η επαναχρησιμοποίηση του ίδιου `reader` για πολλαπλές εικόνες είναι πολύ πιο αποδοτική από το να το επανεκκινείτε κάθε φορά.

## Βήμα 3: Φόρτωση της Εικόνας – Extract Text from Image

Ας φορτώσουμε την εικόνα στη μνήμη. Αυτό το βήμα είναι όπου αργότερα **extract text from image**, αλλά πρώτα την φορτώνουμε.

```python
# Replace with the path to your receipt or scanned document
image_path = "YOUR_DIRECTORY/receipt.png"

# Open the image with Pillow (helps with format handling)
pil_image = Image.open(image_path).convert("RGB")
```

Αν η εικόνα σας είναι ανάποδα ή παραμορφωμένη, σκεφτείτε να χρησιμοποιήσετε τις μεθόδους `rotate` ή `transpose` του Pillow πριν τη δώσετε στη μηχανή OCR. Μια γρήγορη οπτική επιθεώρηση μπορεί να σας εξοικονομήσει ώρες εντοπισμού σφαλμάτων αργότερα.

## Βήμα 4: Εκτέλεση της Μηχανής OCR και Συλλογή Αποτελεσμάτων

Αυτή είναι η καρδιά της διαδικασίας—αποστολή της εικόνας στη μηχανή OCR και λήψη δομημένων δεδομένων.

```python
# EasyOCR returns a list of (bbox, text, confidence) tuples
ocr_result = reader.readtext(image_path, detail=1, paragraph=True)
```

Η σημαία `detail=1` μας δίνει τα πλαίσια περιγράμματος, τα οποία θα χρειαστούμε όταν αργότερα **convert OCR to PDF**. Αν σας ενδιαφέρουν μόνο οι ακατέργαστες συμβολοσειρές, ορίστε `detail=0`.

## Βήμα 5: Μετατροπή του Αποτελέσματος OCR σε Αναζητήσιμο PDF – Convert OCR to PDF

Το EasyOCR δεν παρέχει άμεσο γράφτη PDF, αλλά μπορούμε να δημιουργήσουμε το PDF μόνοι μας χρησιμοποιώντας το Pillow και τη βιβλιοθήκη `reportlab`. Για να κρατήσουμε το tutorial ελαφρύ, θα χρησιμοποιήσουμε το `fpdf2`, το οποίο μας επιτρέπει να ενσωματώσουμε την αρχική εικόνα και να επικάψουμε αόρατο κείμενο.

```bash
pip install fpdf2
```
```python
from fpdf import FPDF

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        # Set invisible text style
        self.set_text_color(255, 255, 255)   # white on white background
        self.set_font("Helvetica", size=12)

        for bbox, text, conf in ocr_data:
            # bbox = [(x1,y1), (x2,y2), (x3,y3), (x4,y4)]
            x_min = min(point[0] for point in bbox)
            y_min = min(point[1] for point in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

# Create PDF instance with the original image as background
pdf = SearchablePDF(image_path)

# Add invisible OCR text on top of the image
pdf.add_ocr_text(ocr_result)

# Save the searchable PDF
output_path = "YOUR_DIRECTORY/receipt_searchable.pdf"
pdf.output(output_path)
```

Τι συνέβη μόλις; Τοποθετήσαμε την σαρωμένη εικόνα ως ορατό στρώμα, έπειτα γράψαμε τις αναγνωρισμένες λέξεις από πάνω χρησιμοποιώντας λευκό κείμενο που ενσωματώνεται στο λευκό φόντο. Τα εργαλεία αναζήτησης εξακολουθούν να διαβάζουν το κρυφό στρώμα, έτσι το PDF γίνεται **searchable** χωρίς να αλλάζει η οπτική εμφάνιση.

## Βήμα 6: Αποθήκευση των Bytes του PDF – Convert Image to PDF

Αν προτιμάτε να χειριστείτε το PDF στη μνήμη (π.χ., αποστέλλοντάς το μέσω API), μπορείτε να συλλάβετε τα bytes αντί να γράψετε απευθείας στο δίσκο.

```python
pdf_bytes = pdf.output(dest='S').encode('latin1')  # returns a byte string

# Example: write bytes to a file (same as Step 5 but shows the conversion)
with open(output_path, "wb") as f:
    f.write(pdf_bytes)
```

Αυτή η γραμμή δείχνει τη κλασική ροή εργασίας **convert image to PDF**: ξεκινάτε με μια εικόνα, εκτελείτε OCR, επικάθετε κείμενο, και τελικά παράγετε ένα ρεύμα PDF.

## Βήμα 7: Επαλήθευση του Αποτελέσματος – Γρήγοροι Έλεγχοι

Αφού εκτελέσετε το script, ανοίξτε το `receipt_searchable.pdf` σε οποιονδήποτε προβολέα PDF και δοκιμάστε το πεδίο αναζήτησης (Ctrl + F). Πληκτρολογήστε μια λέξη που γνωρίζετε ότι εμφανίζεται στην απόδειξη—αν μεταβεί στη σωστή θέση, έχετε δημιουργήσει επιτυχώς **create searchable pdf**!

Αν η αναζήτηση αποτύχει, ελέγξτε ξανά:

1. Τα σκορ εμπιστοσύνης του OCR (`conf` values). Χαμηλή εμπιστοσύνη μπορεί να σημαίνει ότι η εικόνα είναι θολή.  
2. Συντεταγμένες πλαισίων περιγράμματος—μερικές φορές το EasyOCR τις αναφέρει σε διαφορετικό προσανατολισμό.  
3. Ότι ο προβολέας PDF δεν είναι σε λειτουργία «μόνο‑εικόνα» (σπάνια, αλλά ορισμένοι προβολείς έχουν αυτή την επιλογή).

## Πλήρες Λειτουργικό Script

Συνδυάζοντας όλα, εδώ είναι το πλήρες, έτοιμο‑για‑εκτέλεση αρχείο Python:

```python
# searchable_pdf.py
import easyocr
from PIL import Image
from fpdf import FPDF

# ---------- Configuration ----------
IMAGE_PATH = "YOUR_DIRECTORY/receipt.png"
OUTPUT_PDF = "YOUR_DIRECTORY/receipt_searchable.pdf"
# ----------------------------------

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        # Fit the image to the page size
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        self.set_text_color(255, 255, 255)   # invisible white text
        self.set_font("Helvetica", size=12)
        for bbox, text, conf in ocr_data:
            x_min = min(p[0] for p in bbox)
            y_min = min(p[1] for p in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

def main():
    # 1️⃣ Initialize OCR engine – perform OCR on image
    reader = easyocr.Reader(['en'])

    # 2️⃣ Load the image – extract text from image later
    pil_image = Image.open(IMAGE_PATH).convert("RGB")

    # 3️⃣ Run OCR and capture results
    ocr_result = reader.readtext(IMAGE_PATH, detail=1, paragraph=True)

    # 4️⃣ Convert OCR result to searchable PDF – convert OCR to PDF
    pdf = SearchablePDF(IMAGE_PATH)
    pdf.add_ocr_text(ocr_result)

    # 5️⃣ Save the PDF – convert image to PDF (or keep bytes in memory)
    pdf.output(OUTPUT_PDF)
    print(f"✅ Searchable PDF saved to {OUTPUT_PDF}")

if __name__ == "__main__":
    main()
```

Αποθηκεύστε το ως `searchable_pdf.py`, αντικαταστήστε τα placeholders `YOUR_DIRECTORY` με πραγματικές διαδρομές, και εκτελέστε:

```bash
python searchable_pdf.py
```

Θα πρέπει να δείτε ένα μήνυμα επιβεβαίωσης και ένα ολοκαίνουργιο αναζητήσιμο PDF στον φάκελό σας.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

**Τι γίνεται αν η εικόνα είναι έγχρωμη;**  
Το EasyOCR λειτουργεί τόσο με εικόνες σε κλίμακα του γκρι όσο και με έγχρωμες, αλλά η μετατροπή σε κλίμακα του γκρι (`pil_image.convert("L")`) μπορεί μερικές φορές να βελτιώσει την ακρίβεια σε θορυβώδεις σαρώσεις.

**Μπορώ να χειριστώ PDF πολλαπλών σελίδων;**  
Ναι—επανάληψη πάνω σε κάθε εικόνα σελίδας, εκτέλεση των βημάτων OCR, και προσθήκη κάθε σελίδας στο ίδιο αντικείμενο `FPDF`. Απλώς θυμηθείτε να επαναφέρετε τον κέρσορα (`self.add_page()`) για κάθε νέα εικόνα.

**Υπάρχει τρόπος να διατηρήσετε το αρχικό στρώμα κειμένου αντί για αόρατο λευκό κείμενο;**  
Αν χρειάζεστε ένα πραγματικό PDF «κείμενο‑κάτω‑από‑εικόνα» (π.χ., για προσβασιμότητα), σκεφτείτε να χρησιμοποιήσετε το `pdfminer` ή το `pikepdf` για να ενσωματώσετε ένα κρυφό στρώμα κειμένου με σωστές ετικέτες PDF. Είναι πιο προχωρημένο, αλλά η αρχή παραμένει η ίδια: εικόνα φόντου + επικάλυψη κειμένου.

**Τι γίνεται αν η εμπιστοσύνη του OCR είναι χαμηλή;**  
Μπορείτε να φιλτράρετε τις λέξεις χαμηλής εμπιστοσύνης:

```python
filtered = [item for item in ocr_result if item[2] > 0.8]  # keep >80% confidence
pdf.add_ocr_text(filtered)
```

## Συμπέρασμα – Τι Καταφέραμε

Ξεκινήσαμε με μια απλή εικόνα απόδειξης, **performed OCR on image**, εξάγαμε τις αναγνωρισμένες συμβολοσειρές, και τελικά **create searchable pdf** που συμπεριφέρεται όπως οποιοδήποτε επαγγελματικά σαρωμένο έγγραφο. Η διαδικασία κάλυψε όλες τις δευτερεύουσες λέξεις‑κλειδιά—**convert OCR to PDF**, **extract text from image**, **convert image to PDF**, και **perform OCR on image**—οπότε τώρα έχετε ένα επαναχρησιμοποιήσιμο κουτί εργαλείων για οποιοδήποτε παρόμοιο έργο.

### Επόμενα Βήματα

- Πειραματιστείτε με άλλες γλώσσες περνώντας τους κωδικούς ISO στο `easyocr.Reader(['en', 'es'])`.  
- Αντικαταστήστε το EasyOCR με το Tesseract αν χρειάζεστε μια πλήρως offline λύση· το υπόλοιπο pipeline παραμένει το ίδιο.  
- Προσθέστε οπτικοποίηση εμπιστοσύνης OCR (σχεδίαση πλαισίων περιγράμματος στην εικόνα) για εντοπισμό προβληματικών σαρώσεων.  

Έχετε μια παραλλαγή που θέλετε να μοιραστείτε; Αφήστε ένα σχόλιο, κάντε fork

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε σε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}