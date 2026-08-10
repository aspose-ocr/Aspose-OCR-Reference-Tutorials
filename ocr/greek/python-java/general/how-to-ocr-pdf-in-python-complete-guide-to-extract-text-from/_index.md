---
category: general
date: 2026-06-22
description: Μάθετε πώς να κάνετε OCR σε αρχεία PDF με Python, να εξάγετε κείμενο
  από PDF και να μετατρέπετε PDF σε κείμενο χρησιμοποιώντας μια προσέγγιση βασισμένη
  σε ροή. Απλά βήματα για την επεξεργασία σαρωμένων PDF.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf to text
- load pdf from stream
- process scanned pdf
language: el
og_description: Πώς να κάνετε OCR σε αρχεία PDF με Python; Ακολουθήστε αυτόν τον οδηγό
  για να εξάγετε κείμενο από PDF, να μετατρέψετε PDF σε κείμενο και να επεξεργαστείτε
  σκαναρισμένα PDF χρησιμοποιώντας ροή.
og_title: Πώς να κάνετε OCR PDF σε Python – Οδηγός βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to OCR PDF files in Python, extract text from PDF, and convert
    PDF to text using a stream‑based approach. Simple steps for processing scanned
    PDF.
  headline: How to OCR PDF in Python – Complete Guide to Extract Text from PDFs
  type: TechArticle
- description: Learn how to OCR PDF files in Python, extract text from PDF, and convert
    PDF to text using a stream‑based approach. Simple steps for processing scanned
    PDF.
  name: How to OCR PDF in Python – Complete Guide to Extract Text from PDFs
  steps:
  - name: Expected Output
    text: 'If `multipage.pdf` contains three scanned pages, you’ll see something like:'
  - name: 1. PDFs with Mixed Image and Text Layers
    text: 'Some PDFs already contain a hidden text layer (e.g., exported from Word).
      If you want the OCR engine to **ignore existing text** and re‑process the image,
      set:'
  - name: 2. Large Files Exceeding Memory Limits
    text: 'When working with gigabyte‑size PDFs, consider processing in chunks:'
  - name: 3. Language and Font Support
    text: 'If your scanned documents are in French or contain special characters,
      tell the engine which language model to use:'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: Πώς να κάνετε OCR PDF σε Python – Πλήρης οδηγός για την εξαγωγή κειμένου από
  PDF
url: /el/python-java/general/how-to-ocr-pdf-in-python-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να κάνετε OCR PDF σε Python – Πλήρης Οδηγός για την Εξαγωγή Κειμένου από PDF

Έχετε αναρωτηθεί ποτέ **πώς να κάνετε OCR PDF** αρχεία χωρίς να παλεύετε με βαριά εργαλεία επιφάνειας εργασίας; Δεν είστε μόνοι. Σε πολλά πραγματικά έργα—σκεφτείτε την αυτοματοποίηση τιμολογίων ή την ψηφιοποίηση αρχαίων σκαναρισμάτων—χρειάζεστε έναν αξιόπιστο τρόπο να μετατρέψετε ένα σκαναρισμένο PDF σε αναζητήσιμο, επεξεργάσιμο κείμενο.

Σε αυτό το tutorial θα περάσουμε από ένα καθαρό, ολοκληρωμένο παράδειγμα που **εξάγει κείμενο από PDF** σελίδες χρησιμοποιώντας μια ελαφριά μηχανή OCR σε Python. Στο τέλος θα γνωρίζετε ακριβώς πώς να **μετατρέψετε PDF σε κείμενο**, πώς να **φορτώσετε PDF από ροή**, και πώς να **επεξεργαστείτε σκαναρισμένο PDF** αποδοτικά. Χωρίς μαγεία, μόνο απλός κώδικας Python που μπορείτε να ενσωματώσετε στο πρότζεκτ σας σήμερα.

## Τι Θα Μάθετε

- Εγκαταστήστε και ρυθμίστε μια βιβλιοθήκη OCR για Python που καταλαβαίνει είσοδο PDF.  
- Ενεργοποιήστε τη λειτουργία αναγνώρισης PDF και ορίστε τη μορφή εξόδου ως απλό κείμενο.  
- Φορτώστε ένα πολυ‑σελίδων PDF από ροή αρχείου (το κλασικό μοτίβο “load pdf from stream”).  
- Εκτελέστε OCR σε όλες τις σελίδες και ανακτήστε το κειμενικό περιεχόμενο.  
- Εκτυπώστε ή αποθηκεύστε τα αποτελέσματα για επεξεργασία downstream.  

**Προαπαιτούμενα**  
- Python 3.8+ εγκατεστημένο στο μηχάνημά σας.  
- Βασική εξοικείωση με pip και εικονικά περιβάλλοντα.  
- Ένα σκαναρισμένο αρχείο PDF (ονομαζόμενο `multipage.pdf` στο παράδειγμα) τοποθετημένο σε γνωστό φάκελο.  

Αν κάτι από αυτά σας φαίνεται άγνωστο, μην ανησυχείτε—κάθε βήμα εξηγείται με απλή γλώσσα, και θα παρέχουμε τις ακριβείς εντολές που χρειάζεστε.

---

## Βήμα 1: Εγκατάσταση της Μηχανής OCR (πώς να κάνετε OCR PDF)

Πρώτα απ' όλα—χρειάζεστε μια μηχανή OCR που μπορεί να διαχειριστεί είσοδο PDF. Για αυτόν τον οδηγό θα χρησιμοποιήσουμε το υποθετικό πακέτο `ocr` (το API αντικατοπτρίζει δημοφιλή εμπορικά SDK, αλλά το ίδιο μοτίβο λειτουργεί με Tesseract‑OCR, ABBYY ή Google Vision όταν ενσωματωθεί κατάλληλα).

```bash
# Create a virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR package
pip install ocr
```

> **Συμβουλή:** Αν χρησιμοποιείτε Windows και αντιμετωπίζετε σφάλματα δικαιωμάτων, δοκιμάστε `pip install --user ocr`.

Μόλις το πακέτο εγκατασταθεί, μπορείτε να το εισάγετε στο script σας και να δημιουργήσετε μια παρουσία μηχανής—αυτή είναι η καρδιά του **πώς να κάνετε OCR PDF**.

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

Το αντικείμενο `OcrEngine` περιέχει όλες τις ρυθμίσεις που θα προσαρμόσουμε αργότερα, όπως γλώσσα, DPI και—βασικά—λειτουργία PDF.

## Βήμα 2: Ενεργοποίηση Αναγνώρισης PDF και Επιλογή Εξόδου (εξαγωγή κειμένου από PDF)

Από προεπιλογή, πολλά SDK OCR υποθέτουν ότι τους παρέχετε εικόνες. Για να κάνουμε τη μηχανή να αντιμετωπίζει τη ροή εισόδου ως PDF, ενεργοποιούμε τη σημαία αναγνώρισης PDF και ζητάμε έξοδο απλού κειμένου.

```python
# Step 2: Turn on PDF mode and request plain text results
settings = engine.get_settings()
settings.set_recognize_pdf(True)                     # tells the engine to parse PDF containers
settings.set_output_format(ocr.OutputFormat.TEXT)   # we want raw text, not XML or PDF
```

Γιατί να ασχοληθούμε με τον καθορισμό της μορφής εξόδου; Επειδή ορισμένες μηχανές μπορούν να επιστρέψουν PDF με κρυφά επίπεδα κειμένου, αναζητήσιμα PDF ή JSON με πλαίσια οριοθέτησης. Για τις περισσότερες γραμμές εξαγωγής δεδομένων, η **εξαγωγή κειμένου από PDF** ως απλές συμβολοσειρές είναι η πιο καθαρή μορφή downstream.

## Βήμα 3: Φόρτωση του PDF από Ροή Αρχείου (load PDF from stream)

Η φόρτωση ενός PDF από ροή είναι ένα αποδοτικό σε μνήμη μοτίβο—αποφεύγετε τη φόρτωση ολόκληρου του αρχείου στη RAM ταυτόχρονα. Αυτό είναι ιδιαίτερα χρήσιμο όταν εργάζεστε με μεγάλα πολυ‑σελίδων έγγραφα.

```python
# Step 3: Load the multi‑page PDF from a file stream
pdf_path = "YOUR_DIRECTORY/multipage.pdf"
pdf_stream = ocr.ImageStream.from_file(pdf_path)   # wraps the file handle in an OCR‑friendly object
engine.set_image(pdf_stream)
```

> **Τι γίνεται αν το αρχείο βρίσκεται σε S3 ή άλλο cloud bucket;**  
> Απλώς αντικαταστήστε το `from_file` με μια μέθοδο που δέχεται ένα byte buffer (π.χ., `ImageStream.from_bytes(s3_object.read())`). Το υπόλοιπο του pipeline παραμένει ίδιο.

## Βήμα 4: Εκτέλεση OCR σε Όλες τις Σελίδες (process scanned PDF)

Τώρα ξεκινά η βαριά δουλειά. Η μηχανή θα επαναλάβει κάθε σελίδα, θα τρέξει τη μηχανή αναγνώρισης και θα επιστρέψει μια λίστα αντικειμένων σελίδας—κάθε ένα εκθέτει το κειμενικό του περιεχόμενο.

```python
# Step 4: Perform OCR on all pages of the PDF
pages = engine.recognize_pdf()
```

Πίσω από τις σκηνές, η βιβλιοθήκη OCR αποσυμπιέζει κάθε σελίδα PDF, την rasterizes στο ρυθμισμένο DPI και τροφοδοτεί το bitmap μέσω του νευρωνικού μοντέλου της. Το αποτέλεσμα; Μια συλλογή από αντικείμενα `Page` έτοιμα για εξαγωγή.

## Βήμα 5: Ανάκτηση και Εμφάνιση του Αναγνωρισμένου Κειμένου (convert PDF to text)

Τέλος, επαναλαμβάνουμε τις επιστρεφόμενες σελίδες και εκτυπώνουμε το αναγνωρισμένο κείμενο. Αυτή είναι η στιγμή που η **μετατροπή PDF σε κείμενο** συμβαίνει πραγματικά.

```python
# Step 5: Iterate through the recognized pages and display their text
for index, page in enumerate(pages):
    print(f"--- Page {index + 1} ---")
    print(page.get_text())
```

### Αναμενόμενη Έξοδος

Αν το `multipage.pdf` περιέχει τρεις σκαναρισμένες σελίδες, θα δείτε κάτι όπως:

```
--- Page 1 ---
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

--- Page 2 ---
Item Description   Qty   Price
Widget A           10    $50.00
Widget B            5    $30.00
...

--- Page 3 ---
Thank you for your business!
```

Παρατηρήστε τον καθαρό διαχωρισμό μεταξύ των σελίδων—χρήσιμο αν χρειάζεται να αποθηκεύσετε το κείμενο κάθε σελίδας σε βάση δεδομένων ή να το δώσετε σε downstream μοντέλο NLP.

## Διαχείριση Συνηθισμένων Περιπτώσεων Ορίων

### 1. PDF με Μικτά Επίπεδα Εικόνας και Κειμένου

Ορισμένα PDF περιέχουν ήδη ένα κρυφό επίπεδο κειμένου (π.χ., εξαγόμενο από Word). Αν θέλετε η μηχανή OCR να **αγνοήσει το υπάρχον κείμενο** και να επεξεργαστεί ξανά την εικόνα, ορίστε:

```python
settings.set_force_ocr(True)   # forces rasterization and OCR even if text exists
```

### 2. Μεγάλα Αρχεία που Υπερβαίνουν τα Όρια Μνήμης

Όταν εργάζεστε με PDF μεγέθους gigabyte, σκεφτείτε την επεξεργασία σε τμήματα:

```python
for page_number in range(1, engine.get_page_count() + 1):
    single_page_stream = engine.get_page_stream(page_number)
    engine.set_image(single_page_stream)
    page = engine.recognize_pdf()[0]   # only one page at a time
    print(f"--- Page {page_number} ---")
    print(page.get_text())
```

### 3. Υποστήριξη Γλώσσας και Γραμματοσειράς

Αν τα σκαναρισμένα έγγραφά σας είναι στα Γαλλικά ή περιέχουν ειδικούς χαρακτήρες, ενημερώστε τη μηχανή ποιο μοντέλο γλώσσας να χρησιμοποιήσει:

```python
settings.set_language("fr")   # or "en", "de", etc.
```

## Πλήρες Script – Έτοιμο για Εκτέλεση

Παρακάτω βρίσκεται το πλήρες, εκτελέσιμο παράδειγμα που ενώνει όλα τα κομμάτια. Αποθηκεύστε το ως `ocr_pdf.py` και εκτελέστε `python ocr_pdf.py`.

```python
import ocr

def main():
    # Initialize engine
    engine = ocr.OcrEngine()

    # Configure for PDF recognition and plain‑text output
    settings = engine.get_settings()
    settings.set_recognize_pdf(True)
    settings.set_output_format(ocr.OutputFormat.TEXT)

    # Optional: force OCR even if PDF already has text
    # settings.set_force_ocr(True)

    # Load PDF from a stream
    pdf_path = "YOUR_DIRECTORY/multipage.pdf"
    pdf_stream = ocr.ImageStream.from_file(pdf_path)
    engine.set_image(pdf_stream)

    # Perform OCR on every page
    pages = engine.recognize_pdf()

    # Output the results
    for idx, page in enumerate(pages):
        print(f"--- Page {idx + 1} ---")
        print(page.get_text())

if __name__ == "__main__":
    main()
```

**Η εκτέλεση του script** θα εκτυπώσει το κείμενο κάθε σελίδας στην κονσόλα, ακριβώς όπως φαίνεται στην ενότητα “Αναμενόμενη Έξοδος”. Από εδώ μπορείτε να ανακατευθύνετε την έξοδο σε αρχείο:

```bash
python ocr_pdf.py > extracted_text.txt
```

## Συμπέρασμα

Μόλις καλύψαμε **πώς να κάνετε OCR PDF** αρχεία σε Python από την αρχή μέχρι το τέλος. Με τη ρύθμιση της μηχανής, τη φόρτωση του εγγράφου μέσω ροής, και την επανάληψη σε κάθε αναγνωρισμένη σελίδα, μπορείτε να **εξάγετε κείμενο από PDF**, **μετατρέψετε PDF σε κείμενο**, και **επεξεργαστείτε σκαναρισμένο PDF** με μόνο λίγες γραμμές κώδικα. Η προσέγγιση κλιμακώνεται από μικρά τιμολόγια δύο σελίδων μέχρι τεράστια αρχεία εκατοντάδων σελίδων.

Τι ακολουθεί; Δοκιμάστε να τροφοδοτήσετε τις εξαγόμενες συμβολοσειρές σε ευρετήριο αναζήτησης, σε σύνοψη μοντέλου γλώσσας ή σε pipeline επικύρωσης δεδομένων. Μπορείτε επίσης να πειραματιστείτε με μορφές εξόδου όπως JSON για να διατηρήσετε μεταδεδομένα θέσης για προχωρημένη ανάλυση εγγράφων.

Έχετε ερωτήσεις σχετικά με τη διαχείριση κρυπτογραφημένων PDF ή την ενσωμάτωση με αποθήκευση στο cloud; Αφήστε ένα σχόλιο παρακάτω—καλή κωδικοποίηση! 

![Διάγραμμα που δείχνει τη ροή εργασίας OCR PDF – πώς να κάνετε OCR PDF, φόρτωση PDF από ροή, αναγνώριση σελίδων, και εξαγωγή κειμένου](ocr-pdf-workflow.png "how to OCR PDF workflow diagram")

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να κάνετε OCR PDF σε .NET με Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Πώς να Εξάγετε Κείμενο από Εικόνα Χρησιμοποιώντας Aspose.OCR για .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Πώς να Εξάγετε Κείμενο από Αρχεία ZIP Χρησιμοποιώντας Aspose.OCR για .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}