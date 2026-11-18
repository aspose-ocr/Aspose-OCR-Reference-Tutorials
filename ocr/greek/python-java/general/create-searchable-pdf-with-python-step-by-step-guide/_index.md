---
category: general
date: 2026-05-31
description: Δημιουργήστε αναζητήσιμο PDF από σαρωμένες εικόνες χρησιμοποιώντας Python
  OCR. Μάθετε πώς να μετατρέψετε PDF από σαρωμένες εικόνες, να μετατρέψετε TIFF σε
  PDF και να προσθέσετε στρώση κειμένου OCR σε λίγα λεπτά.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- convert tiff to pdf
- how to run OCR
- add OCR text layer
language: el
og_description: Δημιουργήστε άμεσα PDF με δυνατότητα αναζήτησης. Αυτός ο οδηγός δείχνει
  πώς να εκτελέσετε OCR, να μετατρέψετε PDF σαρωμένης εικόνας και να προσθέσετε στρώση
  κειμένου OCR χρησιμοποιώντας ένα μόνο script Python.
og_title: Δημιουργία Αναζητήσιμου PDF με Python – Πλήρης Οδηγός
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  headline: Create Searchable PDF with Python – Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  name: Create Searchable PDF with Python – Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'Running the script prints:'
  - name: 1️⃣ Can I process multi‑page PDFs?
    text: Yes. Use `ocr_engine.load_image("file.pdf")` and then loop over each page
      with `ocr_engine.recognize(pdf_save_options, page_number)`. The library will
      automatically generate a multi‑page searchable PDF.
  - name: 2️⃣ What if my source file is a high‑resolution TIFF (300 dpi+)?
    text: 'Higher DPI yields better OCR accuracy but also larger memory usage. If
      you hit a `MemoryError`, downscale the image first:'
  - name: 3️⃣ How do I change the language of the OCR?
    text: 'Set the `language` property on the engine before loading the image:'
  - name: 4️⃣ What if I need to keep the original image quality?
    text: The `PdfSaveOptions` class has a `compression` property. Set it to `PdfCompression.None`
      to preserve the raster data exactly as it was.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Document Automation
title: Δημιουργία Αναζητήσιμου PDF με Python – Οδηγός Βήμα‑βήμα
url: /el/python-java/general/create-searchable-pdf-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Αναζητήσιμου PDF με Python – Οδηγός Βήμα‑Βήμα

Έχετε αναρωτηθεί ποτέ πώς να **δημιουργήσετε αναζητήσιμο PDF** από μια σαρωμένη σελίδα χωρίς να χρειάζεται να χειρίζεστε δεκάδες εργαλεία; Δεν είστε μόνοι. Σε πολλές εργασιακές ροές, ένα σαρωμένο TIFF ή JPEG αποθηκεύεται σε κοινόχρηστο δίσκο, και το επόμενο άτομο πρέπει να αντιγράψει‑επικολλήσει το κείμενο χειροκίνητα—πρόσφορο, επιρρεπές σε σφάλματα και χρονοβόρο.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα μια καθαρή, προγραμματιστική λύση που σας επιτρέπει να **μετατρέψετε σαρωμένο PDF εικόνας**, **μετατρέψετε TIFF σε PDF**, και **προσθέσετε στρώση κειμένου OCR** σε μία ενέργεια. Στο τέλος θα έχετε ένα έτοιμο‑για‑χρήση script που εκτελεί OCR, ενσωματώνει το κρυφό κείμενο, και παράγει ένα αναζητήσιμο PDF που μπορείτε να ευρετήσετε, να αναζητήσετε ή να μοιραστείτε με σιγουριά.

## Τι Θα Χρειαστεί

- Python 3.9+ (οποιαδήποτε πρόσφατη έκδοση λειτουργεί)
- `aspose-ocr` and `aspose-pdf` packages (εγκαθίστανται μέσω `pip install aspose-ocr aspose-pdf`)
- Ένα αρχείο σαρωμένης εικόνας (`.tif`, `.png`, `.jpg`, ή ακόμη και μια σελίδα PDF που είναι μόνο εικόνα)
- Μέτρια ποσότητα RAM (η μηχανή OCR είναι ελαφριά· ακόμη και ένα laptop το διαχειρίζεται)

> **Συμβουλή:** Αν χρησιμοποιείτε Windows, ο πιο εύκολος τρόπος για να αποκτήσετε τα πακέτα είναι να εκτελέσετε την εντολή σε ένα ανυψωμένο παράθυρο PowerShell.

```bash
pip install aspose-ocr aspose-pdf
```

Τώρα που οι προαπαιτήσεις έχουν καλυφθεί, ας βουτήξουμε στον κώδικα.

## Βήμα 1: Δημιουργία Παραδείγματος Μηχανής OCR – *create searchable pdf*

Το πρώτο που κάνουμε είναι να εκκινήσουμε τη μηχανή OCR. Σκεφτείτε τη ως τον εγκέφαλο που θα διαβάσει κάθε pixel και θα το μετατρέψει σε χαρακτήρες.

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine – this is the core of the create searchable pdf process
ocr_engine = OcrEngine()
```

> **Γιατί είναι σημαντικό:** Η αρχικοποίηση της μηχανής μόνο μία φορά διατηρεί τη χρήση μνήμης χαμηλή. Αν καλούσατε `OcrEngine()` μέσα σε βρόχο για κάθε σελίδα, θα εξαντλούσατε γρήγορα τους πόρους.

## Βήμα 2: Φόρτωση Σαρωμένης Εικόνας – *convert tiff to pdf* & *convert scanned image pdf*

Στη συνέχεια, δείξτε τη μηχανή στο αρχείο που θέλετε να επεξεργαστείτε. Το API δέχεται οποιαδήποτε raster εικόνα, έτσι ένα TIFF λειτουργεί εξίσου καλά με ένα JPEG.

```python
# Load the image you want to OCR. Replace the path with your own file location.
ocr_engine.load_image("YOUR_DIRECTORY/scanned_page.tif")
```

Αν έχετε ένα PDF που περιέχει μόνο μια σαρωμένη εικόνα, μπορείτε ακόμη να χρησιμοποιήσετε το `load_image` επειδή το Aspose θα εξάγει αυτόματα την πρώτη σελίδα.

## Βήμα 3: Προετοιμασία Επιλογών Αποθήκευσης PDF – *add OCR text layer*

Εδώ διαμορφώνουμε πώς θα πρέπει να φαίνεται το τελικό PDF. Η κρίσιμη σημαία είναι `create_searchable_pdf`; ορίζοντάς την σε `True` λέμε στη βιβλιοθήκη να ενσωματώσει μια αόρατη στρώση κειμένου που αντικατοπτρίζει το οπτικό περιεχόμενο.

```python
from aspose.pdf import PdfSaveOptions

pdf_save_options = PdfSaveOptions()
pdf_save_options.create_searchable_pdf = True   # embed OCR text layer
pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"
```

> **Τι κάνει η στρώση κειμένου:** Όταν ανοίξετε το παραγόμενο αρχείο στο Adobe Reader και προσπαθήσετε να επιλέξετε κείμενο, θα δείτε τους κρυφούς χαρακτήρες. Οι μηχανές αναζήτησης μπορούν επίσης να τα ευρετηριάσουν—τέλειο για συμμόρφωση ή αρχειοθέτηση.

## Βήμα 4: Εκτέλεση OCR και Αποθήκευση – *how to run OCR* σε μία κλήση

Τώρα συμβαίνει η μαγεία. Μία κλήση μεθόδου εκτελεί τη μηχανή αναγνώρισης και γράφει το αναζητήσιμο PDF στο δίσκο.

```python
# Run OCR and generate the searchable PDF in one go
ocr_engine.recognize(pdf_save_options)

print("PDF saved as searchable PDF.")
```

Η μέθοδος `recognize` επιστρέφει ένα αντικείμενο κατάστασης που μπορείτε να ελέγξετε για σφάλματα, αλλά για τις περισσότερες απλές περιπτώσεις η απλή κλήση παραπάνω είναι επαρκής.

### Αναμενόμενο Αποτέλεσμα

Η εκτέλεση του script εμφανίζει:

```
PDF saved as searchable PDF.
```

Αν ανοίξετε το `scanned_page_searchable.pdf` θα παρατηρήσετε ότι μπορείτε να επιλέξετε κείμενο, να το αντιγράψετε‑επικολλήσετε, και ακόμη να εκτελέσετε αναζήτηση `Ctrl+F`. Αυτό είναι το χαρακτηριστικό μιας ροής εργασίας **create searchable pdf**.

## Πλήρες Λειτουργικό Script

Παρακάτω είναι το πλήρες, έτοιμο‑για‑εκτέλεση script. Απλώς αντικαταστήστε τις διαδρομές placeholder με τις πραγματικές τοποθεσίες των αρχείων σας.

```python
# ------------------------------------------------------------
# create_searchable_pdf.py – Convert scanned image to searchable PDF
# ------------------------------------------------------------

from aspose.ocr import OcrEngine
from aspose.pdf import PdfSaveOptions

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load image (TIFF, JPEG, PNG, or scanned PDF page)
    image_path = "YOUR_DIRECTORY/scanned_page.tif"
    ocr_engine.load_image(image_path)

    # 3️⃣ Configure PDF output – embed OCR text layer
    pdf_save_options = PdfSaveOptions()
    pdf_save_options.create_searchable_pdf = True
    pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"

    # 4️⃣ Run OCR and write searchable PDF
    ocr_engine.recognize(pdf_save_options)

    print("PDF saved as searchable PDF.")

if __name__ == "__main__":
    main()
```

Αποθηκεύστε το ως `create_searchable_pdf.py` και εκτελέστε:

```bash
python create_searchable_pdf.py
```

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### 1️⃣ Μπορώ να επεξεργαστώ PDF πολλαπλών σελίδων;

Ναι. Χρησιμοποιήστε `ocr_engine.load_image("file.pdf")` και στη συνέχεια κάντε βρόχο σε κάθε σελίδα με `ocr_engine.recognize(pdf_save_options, page_number)`. Η βιβλιοθήκη θα δημιουργήσει αυτόματα ένα PDF πολλαπλών σελίδων αναζητήσιμο.

### 2️⃣ Τι γίνεται αν το αρχείο προέλευσης είναι TIFF υψηλής ανάλυσης (300 dpi+)?

Υψηλότερο DPI προσφέρει καλύτερη ακρίβεια OCR αλλά και μεγαλύτερη χρήση μνήμης. Αν αντιμετωπίσετε `MemoryError`, μειώστε πρώτα την ανάλυση της εικόνας:

```python
from PIL import Image
img = Image.open(image_path)
img = img.resize((int(img.width * 0.5), int(img.height * 0.5)), Image.ANTIALIAS)
img.save("temp.tif")
ocr_engine.load_image("temp.tif")
```

### 3️⃣ Πώς αλλάζω τη γλώσσα του OCR;

Ορίστε την ιδιότητα `language` στη μηχανή πριν φορτώσετε την εικόνα:

```python
ocr_engine.language = "fra"   # French
```

Μια πλήρης λίστα των υποστηριζόμενων κωδικών γλώσσας βρίσκεται στην τεκμηρίωση του Aspose.

### 4️⃣ Τι κάνω αν χρειάζεται να διατηρήσω την αρχική ποιότητα εικόνας;

Η κλάση `PdfSaveOptions` έχει ιδιότητα `compression`. Ορίστε την σε `PdfCompression.None` για να διατηρήσετε τα raster δεδομένα ακριβώς όπως ήταν.

```python
pdf_save_options.compression = "None"
```

## Συμβουλές για Παραγωγικές Αναπτύξεις

- **Batch processing:** Τυλίξτε τη βασική λογική σε μια συνάρτηση που δέχεται μια λίστα διαδρομών αρχείων. Καταγράψτε κάθε επιτυχία/αποτυχία σε CSV για γραμμές ελέγχου.
- **Parallelism:** Χρησιμοποιήστε `concurrent.futures.ThreadPoolExecutor` για να εκτελέσετε OCR σε πολλούς πυρήνες. Απλώς θυμηθείτε ότι κάθε νήμα χρειάζεται το δικό του παράδειγμα `OcrEngine`.
- **Security:** Αν χειρίζεστε ευαίσθητα έγγραφα, εκτελέστε το script σε περιβάλλον sandbox και διαγράψτε τα προσωρινά αρχεία αμέσως μετά την επεξεργασία.

## Συμπέρασμα

Τώρα ξέρετε πώς να **δημιουργήσετε αναζητήσιμα PDF** αρχεία από σαρωμένες εικόνες χρησιμοποιώντας ένα σύντομο script Python. Αρχικοποιώντας μια μηχανή OCR, φορτώνοντας ένα TIFF (ή οποιοδήποτε raster), διαμορφώνοντας το `PdfSaveOptions` για **add OCR text layer**, και τελικά καλώντας το `recognize`, ολόκληρη η αλυσίδα **convert scanned image pdf** και **convert TIFF to PDF** γίνεται μια ενιαία, επαναλαμβανόμενη εντολή.

Επόμενα βήματα; Δοκιμάστε να συνδέσετε αυτό το script με έναν παρατηρητή αρχείων ώστε κάθε νέα σάρωση που τοποθετείται σε φάκελο να γίνεται αυτόματα αναζητήσιμη. Ή πειραματιστείτε με διαφορετικές γλώσσες OCR για να υποστηρίξετε πολύγλωσσικά αρχεία. Ο ουρανός είναι το όριο όταν συνδυάζετε OCR με δημιουργία PDF.

Έχετε περισσότερες ερωτήσεις σχετικά με το **how to run OCR** σε άλλες γλώσσες ή πλαίσια; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

![Διάγραμμα που δείχνει τη ροή από σαρωμένη εικόνα → μηχανή OCR → αναζητήσιμο PDF (create searchable pdf)](searchable-pdf-flow.png "Create searchable pdf flow diagram")


## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

- [Πώς να κάνετε OCR PDF σε .NET με Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Μετατροπή Εικόνων σε PDF C# – Αποθήκευση Αποτελέσματος OCR Πολλαπλών Σελίδων](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [Πώς να κάνετε OCR Κειμένου Εικόνας με Γλώσσα Χρησιμοποιώντας Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}