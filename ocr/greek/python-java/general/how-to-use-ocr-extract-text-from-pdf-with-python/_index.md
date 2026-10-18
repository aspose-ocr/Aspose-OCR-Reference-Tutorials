---
category: general
date: 2026-04-26
description: πώς να χρησιμοποιήσετε OCR σε σαρωμένα PDF, να εξάγετε κείμενο από PDF,
  να εκτελέσετε OCR σε PDF και να μετατρέψετε το σαρωμένο PDF σε αναζητήσιμα αρχεία
  σε λίγα βήματα.
draft: false
keywords:
- how to use OCR
- extract text from pdf
- run OCR on pdf
- convert scanned pdf
- load pdf as image
language: el
og_description: 'πώς να χρησιμοποιήσετε OCR στην Python: μάθετε πώς να εξάγετε κείμενο
  από PDF, να εκτελείτε OCR σε PDF και να μετατρέπετε σαρωμένα PDF σε έγγραφα με δυνατότητα
  αναζήτησης.'
og_title: πώς να χρησιμοποιήσετε OCR – Σύντομος οδηγός για την εξαγωγή κειμένου από
  PDF
tags:
- OCR
- Python
- PDF
- Text Extraction
title: πώς να χρησιμοποιήσετε OCR – Εξαγωγή κειμένου από PDF με Python
url: /el/python-java/general/how-to-use-ocr-extract-text-from-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# πώς να χρησιμοποιήσετε OCR – Εξαγωγή κειμένου από PDF με Python

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε OCR** για να εξάγετε κείμενο από ένα σαρωμένο συμβόλαιο, απόδειξη ή ebook; Δεν είστε μόνοι. Σε πολλά πραγματικά έργα το PDF που λαμβάνετε είναι απλώς μια εικόνα, και χωρίς OCR δεν μπορείτε να αναζητήσετε, να ευρετηριάσετε ή να αναλύσετε το περιεχόμενό του.  

Σε αυτό το tutorial θα περάσουμε από ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει **πώς να χρησιμοποιήσετε OCR**, πώς να **εξάγετε κείμενο από PDF**, και γιατί ίσως θέλετε να **μετατρέψετε σαρωμένα PDF** σε έγγραφα που μπορούν να αναζητηθούν. Θα καλύψουμε επίσης τη λεπτή τέχνη του **φόρτωμα PDF ως εικόνα** ώστε η μηχανή OCR να μπορεί να δει κάθε σελίδα καθαρά.

> **Γρήγορη προεπισκόπηση:** Στο τέλος θα έχετε ένα script που φορτώνει ένα πολυ-σελίδων PDF, εκτελεί OCR σε κάθε σελίδα, και εκτυπώνει το αναγνωρισμένο κείμενο – χωρίς εξωτερικές υπηρεσίες.

## Τι Θα Χρειαστεί

- Python 3.9+ (οποιαδήποτε πρόσφατη έκδοση λειτουργεί)
- `aocr` package (ή οποιαδήποτε συμβατή βιβλιοθήκη OCR που παρέχει `OcrEngine` και `Image.load`)
- Ένα σαρωμένο αρχείο PDF που θέλετε να επεξεργαστείτε (π.χ., `contract.pdf`)
- Μια μέτρια ποσότητα RAM (≈ 200 MB ανά 100‑σελίδων PDF συνήθως είναι επαρκής)

Αν δεν έχετε εγκαταστήσει ακόμη τη βιβλιοθήκη OCR, εκτελέστε:

```bash
pip install aocr
```

> **Συμβουλή επαγγελματία:** Χρησιμοποιήστε ένα εικονικό περιβάλλον για να διατηρήσετε τις εξαρτήσεις σας οργανωμένες.

## Βήμα 1: Φόρτωση PDF ως Εικόνα – Το Πρώτο Κομμάτι του Παζλ

Πριν μπορέσει να γίνει οποιοδήποτε OCR, το PDF πρέπει να αναπαρασταθεί ως εικόνα. Εδώ έρχεται σε δράση η δευτερεύουσα λέξη-κλειδί **load pdf as image**.

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()

# Step 2: Load the PDF file as a multi‑page image
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/contract.pdf")
```

*Γιατί είναι σημαντικό:* `aocr.Image.load` εσωτερικά rasterizes (μετατρέπει) κάθε σελίδα PDF σε bitmap που η μηχανή OCR μπορεί να καταλάβει. Αν παραλείψετε αυτό το βήμα και δώσετε το ακατέργαστο PDF, η μηχανή θα εμφανίσει σφάλμα επειδή αναμένει δεδομένα pixel, όχι διανυσματικά δεδομένα.

> **Σημείωση:** Η διαδρομή μπορεί να είναι απόλυτη ή σχετική. Βεβαιωθείτε ότι το αρχείο είναι αναγνώσιμο· διαφορετικά θα αντιμετωπίσετε `FileNotFoundError`.

## Βήμα 2: Εκτέλεση OCR σε PDF – Μετατροπή Pixels σε Χαρακτήρες

Τώρα που το PDF υπάρχει ως εικόνα, μπορούμε τελικά να **εκτελέσουμε OCR σε PDF**. Το παρακάτω απόσπασμα επεξεργάζεται κάθε σελίδα με τη μία:

```python
# Step 3: Run OCR on every page of the document
page_results = ocr_engine.process_all_pages()
```

*Τι συμβαίνει στο παρασκήνιο;* `process_all_pages` διασχίζει τις rasterized σελίδες, εφαρμόζει το μοντέλο OCR, και επιστρέφει μια λίστα αντικειμένων αποτελεσμάτων — ένα ανά σελίδα. Κάθε αποτέλεσμα περιέχει το αναγνωρισμένο κείμενο, τις βαθμολογίες εμπιστοσύνης, και τα bounding boxes (αν τα χρειαστείτε αργότερα).

## Βήμα 3: Εξαγωγή Κειμένου από PDF – Αποκόλληση των Συμβολοσειρών

Με τα αποτελέσματα OCR στα χέρια, η εξαγωγή του απλού κειμένου γίνεται τετριμμένο. Θα διατρέξουμε τις σελίδες και θα εκτυπώσουμε το αποτέλεσμα, δείχνοντας τη δευτερεύουσα λέξη-κλειδί **extract text from pdf**.

```python
# Step 4: Iterate through the results and output the recognized text
for page_number, page_result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(page_result.text)
```

**Αναμενόμενο αποτέλεσμα** (περιορισμένο για συντομία):

```
--- Page 1 ---
This Agreement is made on the 1st day of January...
--- Page 2 ---
Section 2.1: Definitions...
```

Αν χρειάζεστε το κείμενο σε μια ενιαία συμβολοσειρά, απλώς συνενώστε:

```python
full_text = "\n".join(r.text for r in page_results)
```

Τώρα έχετε εξάγει επιτυχώς **κείμενο από PDF** χρησιμοποιώντας OCR.

## Βήμα 4: Μετατροπή Σαρωμένου PDF – Δημιουργία Αναζητήσιμου

Πολλά downstream εργαλεία (όπως Elasticsearch ή SharePoint) αναμένουν ένα αναζητήσιμο PDF αντί για ένα αρχείο απλού κειμένου. Μπορείτε να ενσωματώσετε την έξοδο OCR πίσω στο αρχικό PDF, μετατρέποντας αποτελεσματικά **scanned PDF** σε μια αναζητήσιμη έκδοση.

```python
# Optional: Create a searchable PDF
searchable_pdf_path = "YOUR_DIRECTORY/contract_searchable.pdf"
ocr_engine.save_searchable_pdf(searchable_pdf_path)
print(f"Searchable PDF saved to {searchable_pdf_path}")
```

*Γιατί να ασχοληθείτε;* Ένα αναζητήσιμο PDF διατηρεί την αρχική διάταξη και τις εικόνες ενώ επιτρέπει την επιλογή κειμένου και την ευρετηρίαση — κέρδος για ανθρώπους και μηχανές.

## Συνηθισμένα Πιθανά Προβλήματα & Ακραίες Περιπτώσεις

### Πολυ‑σελίδες PDFs Μεγαλύτερα από τη Μνήμη

Αν το PDF σας έχει εκατοντάδες σελίδες, η φόρτωση όλων ταυτόχρονα μπορεί να εξαντλήσει τη RAM. Η βιβλιοθήκη `aocr` υποστηρίζει lazy loading:

```python
ocr_engine.image = aocr.Image.load("bigfile.pdf", lazy=True)
```

Στη συνέχεια επεξεργαστείτε τις σελίδες μία-μία:

```python
for page in ocr_engine.image.iter_pages():
    result = ocr_engine.process_page(page)
    print(result.text)
```

### Σαρώσεις Χαμηλής Ποιότητας

Η ακρίβεια του OCR μειώνεται δραστικά σε θολές ή χαμηλής αντίθεσης σαρώσεις. Πριν τροφοδοτήσετε την εικόνα στη μηχανή, σκεφτείτε προεπεξεργασία:

```python
from aocr import preprocess

# Improve contrast and denoise
clean_image = preprocess.enhance(ocr_engine.image, contrast=1.5, denoise=True)
ocr_engine.image = clean_image
```

### Υποστήριξη Γλώσσας

Από προεπιλογή η μηχανή υποθέτει Αγγλικά. Για να **run OCR on PDF** σε άλλη γλώσσα, ορίστε τον κωδικό γλώσσας:

```python
ocr_engine.language = "spa"  # Spanish
```

Βεβαιωθείτε ότι το αντίστοιχο μοντέλο γλώσσας είναι εγκατεστημένο.

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα, εδώ είναι ένα αυτόνομο script που μπορείτε να αποθηκεύσετε σε αρχείο με όνομα `ocr_pdf.py` και να το εκτελέσετε αμέσως:

```python
# ocr_pdf.py
from aocr import OcrEngine, Image, preprocess

def main(pdf_path: str, output_path: str = None):
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load PDF as image (lazy loading for large files)
    ocr_engine.image = Image.load(pdf_path, lazy=False)

    # Optional preprocessing – improves accuracy on noisy scans
    ocr_engine.image = preprocess.enhance(ocr_engine.image, contrast=1.4, denoise=True)

    # Run OCR on all pages
    page_results = ocr_engine.process_all_pages()

    # Print extracted text
    for i, result in enumerate(page_results, start=1):
        print(f"--- Page {i} ---")
        print(result.text)

    # If a searchable PDF is desired
    if output_path:
        ocr_engine.save_searchable_pdf(output_path)
        print(f"Searchable PDF saved to {output_path}")

if __name__ == "__main__":
    import argparse
    parser = argparse.ArgumentParser(description="Extract text from a scanned PDF using OCR.")
    parser.add_argument("pdf", help="Path to the input scanned PDF")
    parser.add_argument("-o", "--output", help="Path to save searchable PDF (optional)")
    args = parser.parse_args()
    main(args.pdf, args.output)
```

Τρέξτε το ως εξής:

```bash
python ocr_pdf.py YOUR_DIRECTORY/contract.pdf -o YOUR_DIRECTORY/contract_searchable.pdf
```

Θα δείτε το κείμενο να εκτυπώνεται στην κονσόλα, και αν παρείχατε `-o`, ένα αναζητήσιμο PDF θα εμφανιστεί δίπλα στο αρχικό αρχείο.

## Συμβουλές Επαγγελματία & Καλές Πρακτικές

- **Batch processing:** Όταν διαχειρίζεστε δεκάδες PDFs, τυλίξτε τη λογική σε έναν βρόχο και καταγράψτε την επιτυχία/αποτυχία κάθε αρχείου.
- **Confidence filtering:** Κάθε `page_result` περιλαμβάνει ένα μέτρο εμπιστοσύνης. Απορρίψτε ή σημαδέψτε σελίδες με χαμηλή εμπιστοσύνη για χειροκίνητη ανασκόπηση.
- **Parallelism:** Αν η CPU σας έχει πολλούς πυρήνες, σκεφτείτε να χρησιμοποιήσετε `concurrent.futures` για επεξεργασία σελίδων παράλληλα — απλώς προσέξτε τη χρήση μνήμης.
- **Version lock:** Το API του `aocr` μπορεί να εξελιχθεί. Καθορίστε την έκδοση στο `requirements.txt` (π.χ., `aocr==2.3.1`) για να αποφύγετε αλλαγές που σπάζουν.

## Συμπέρασμα

Διασχίσαμε **πώς να χρησιμοποιήσετε OCR** για **εξαγωγή κειμένου από PDF**, **εκτέλεση OCR σε PDF**, **φόρτωση PDF ως εικόνα**, και ακόμη **μετατροπή σαρωμένου PDF** σε αναζητήσιμο φορμάτ. Ο κώδικας είναι πλήρης, οι εξηγήσεις καλύπτουν τόσο το *τι* όσο και το *γιατί*, και τώρα έχετε ένα επαναχρησιμοποιήσιμο πρότυπο για οποιοδήποτε έργο που ασχολείται με PDFs βασισμένα σε εικόνες.

Τι ακολουθεί; Δοκιμάστε να τροφοδοτήσετε το εξαγόμενο κείμενο σε μια αλυσίδα επεξεργασίας φυσικής γλώσσας, ευρετηριάστε τα αναζητήσιμα PDFs με Elasticsearch, ή πειραματιστείτε με διαφορετικά OCR back‑ends όπως Tesserent ή Azure Computer Vision. Ο ουρανός είναι το όριο, και τα εργαλεία είναι στα χέρια σας.

Καλή προγραμματιστική δουλειά, και ας είναι πάντα τα PDFs σας αναζητήσιμα! 

![παράδειγμα χρήσης OCR](/images/ocr_workflow.png "χρήση OCR")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}