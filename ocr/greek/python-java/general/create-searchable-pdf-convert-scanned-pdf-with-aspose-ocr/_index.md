---
category: general
date: 2026-03-18
description: Δημιουργήστε PDF με δυνατότητα αναζήτησης από τα σαρωμένα αρχεία σας
  χρησιμοποιώντας το Aspose OCR. Μάθετε πώς να μετατρέπετε σαρωμένα PDF, να εξάγετε
  κείμενο από PDF και να αναγνωρίζετε γρήγορα κείμενο σε PDF.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- extract text from pdf
- recognize text pdf
- convert image pdf
language: el
og_description: Δημιουργήστε άμεσα PDF με δυνατότητα αναζήτησης. Ακολουθήστε αυτόν
  τον οδηγό για να μετατρέψετε σαρωμένο PDF, να εξάγετε κείμενο από PDF και να αναγνωρίσετε
  κείμενο PDF χρησιμοποιώντας το Aspose OCR.
og_title: Δημιουργήστε Αναζητήσιμο PDF – Βήμα‑βήμα με το Aspose OCR
tags:
- OCR
- PDF
- Aspose
- Python
title: Δημιουργία PDF με δυνατότητα αναζήτησης – Μετατροπή σαρωμένου PDF με Aspose
  OCR
url: /el/python-java/general/create-searchable-pdf-convert-scanned-pdf-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Αναζητήσιμου PDF – Οδηγός Βήμα‑βήμα  

Έχετε ποτέ χρειαστεί να **create searchable PDF** από μια στοίβα σαρωμένων σελίδων αλλά δεν ήξερατε από πού να ξεκινήσετε; Δεν είστε μόνοι—οι περισσότεροι προγραμματιστές αντιμετωπίζουν αυτό το εμπόδιο όταν το πρώτο σκανάρισμα φτάνει στον διακομιστή τους.  

Το καλό νέο είναι ότι με το Aspose OCR μπορείτε να **convert scanned pdf** με λίγες μόνο γραμμές κώδικα, **extract text from pdf** για επαλήθευση, και ακόμη **recognize text pdf** άμεσα. Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία, από την εγκατάσταση της βιβλιοθήκης μέχρι την αποθήκευση ενός πλήρως αναζητήσιμου εγγράφου, και θα προσθέσουμε μερικές συμβουλές για την αντιμετώπιση των edge cases του **convert image pdf**.

## What You’ll Achieve  

Στο τέλος αυτού του οδηγού θα μπορείτε να:

* Φορτώσετε ένα σαρωμένο PDF (ή ένα PDF μόνο με εικόνες) στο Aspose OCR.  
* Καθορίσετε στην μηχανή ποιες σελίδες θα επεξεργαστεί – χρήσιμο όταν χρειάζεστε μόνο ένα υποσύνολο.  
* Ενσωματώσετε τα αποτελέσματα OCR πίσω στο αρχικό αρχείο ώστε η έξοδος να είναι ένα αληθινό **searchable PDF**.  
* Επαληθεύσετε τη λειτουργία εκτυπώνοντας τον αριθμό σελίδων και, αν θέλετε, εξάγοντας το κείμενο που προέκυψε.  

Καμία εξωτερική υπηρεσία, καμία κρυφή μαγεία—μόνο καθαρή Python και το API του Aspose.

## Prerequisites  

* Python 3.8 ή νεότερη.  
* Πακέτο `aspose-ocr` – εγκαταστήστε το με `pip install aspose-ocr`.  
* Ένα σαρωμένο αρχείο PDF (ή PDF που περιέχει μόνο εικόνες).  
* Βασική εξοικείωση με scripting σε Python.  

Αν έχετε ήδη όλα αυτά, τέλεια—ας βουτήξουμε.

<img src="searchable-pdf-workflow.png" alt="Διαδικασία δημιουργίας αναζητήσιμου PDF">  

*(Εικονογράφηση της διαδικασίας OCR – δεν απαιτείται για τον κώδικα αλλά βοηθά τους οπτικούς μαθητές.)*

## Step 1 – Initialize the OCR Engine  

Πρώτο πράγμα: χρειάζεστε ένα στιγμιότυπο `OcrEngine`. Σκεφτείτε το ως το μυαλό που θα διαβάσει κάθε pixel και θα το μετατρέψει σε χαρακτήρες Unicode.

```python
# Step 1: Import the required classes and create the engine
from aspose.ocr import OcrEngine, PdfRecognitionOptions, ImageFormats

# Initialize the OCR engine – this object holds all settings
ocr_engine = OcrEngine()
```

**Γιατί είναι σημαντικό:** Χωρίς τη μηχανή δεν μπορείτε να ορίσετε επιλογές ή να εκτελέσετε αναγνώριση. Η προαρχική αρχικοποίηση σας δίνει επίσης ένα σημείο για να προσθέσετε τυχόν προσαρμοσμένα λεξικά αργότερα.

## Step 2 – Load Your Source PDF  

Το Aspose OCR μπορεί να διαβάσει PDF απευθείας, πράγμα που σημαίνει ότι δεν χρειάζεται να rasterize κάθε σελίδα μόνοι σας. Απλώς δείξτε στη μηχανή το αρχείο.

```python
# Step 2: Load the scanned PDF (replace with your actual path)
input_path = "YOUR_DIRECTORY/input.pdf"
ocr_engine.setImageFromFile(input_path)
```

*Pro tip:* Αν το PDF είναι τεράστιο, σκεφτείτε να το φορτώσετε από stream ώστε να αποφύγετε το κλείδωμα του αρχείου στο δίσκο.

## Step 3 – Configure PDF Recognition Options  

Εδώ αρχίζουν να λάμπουν οι δευτερεύουσες λέξεις-κλειδιά. Μπορείτε να πείτε στη μηχανή να **convert scanned pdf** μόνο σε συγκεκριμένες σελίδες, να ενσωματώσει το αναγνωρισμένο κείμενο, ή ακόμη να διατηρήσει τις αρχικές εικόνες ανέπαφες.

```python
# Step 3: Create and configure PDF recognition options
pdf_options = PdfRecognitionOptions()
pdf_options.setEmbedRecognisedText(True)          # Makes the PDF searchable
pdf_options.setPageRange(1, 3)                    # Process only pages 1‑3 (optional)
pdf_options.setTextExtractionMode(True)          # Enables text extraction for verification
```

**Γιατί είναι σημαντικό:**  
* `setEmbedRecognisedText(True)` είναι το κλειδί για τη μετατροπή ενός raster PDF σε **searchable PDF**.  
* `setPageRange` σας βοηθά να **convert image pdf** επιλεκτικά—χρήσιμο για μεγάλα έγγραφα όπου χρειάζεστε OCR μόνο σε λίγες σελίδες.  
* Η ενεργοποίηση της εξαγωγής κειμένου σας επιτρέπει αργότερα να **extract text from pdf** χωρίς να ανοίξετε προβολέα.

## Step 4 – Attach Options to the Engine  

Τώρα συνδέστε τις επιλογές με τη μηχανή. Αυτό το βήμα συχνά παραβλέπεται, αλλά η παράλειψή του σημαίνει ότι η μηχανή τρέχει με τις προεπιλεγμένες ρυθμίσεις (χωρίς αναζητήσιμο κείμενο).

```python
# Step 4: Attach the options to the OCR engine
ocr_engine.setPdfRecognitionOptions(pdf_options)
```

## Step 5 – Run OCR on the Selected Pages  

Με όλα συνδεδεμένα, η πραγματική αναγνώριση είναι μια κλήση μεθόδου.

```python
# Step 5: Perform OCR – this may take a few seconds per page
ocr_result = ocr_engine.recognize()
```

Αν επεξεργάζεστε ένα πολυμεγαβυτιούχο έγγραφο, ίσως θελήσετε να το τυλίξετε σε `try/except` για να πιάσετε `OcrException` και να καταγράψετε τη προβληματική σελίδα.

## Step 6 – Verify the Result  

Μια γρήγορη επιβεβαίωση είναι να εκτυπώσετε πόσες σελίδες η μηχανή θεωρεί ότι επεξεργάστηκε. Μπορείτε επίσης να εξάγετε το ακατέργαστο κείμενο αν χρειάζεστε **extract text from pdf** για περαιτέρω ανάλυση.

```python
# Step 6: Show how many pages were processed
print("Pages processed:", ocr_result.getPageCount())

# Optional: dump extracted text for the first page (helps debugging)
first_page_text = ocr_result.getPageText(0)   # 0‑based index
print("\n--- Extracted Text (Page 1) ---\n", first_page_text[:500])  # show first 500 chars
```

**Γιατί σας ενδιαφέρει:** Η εμφάνιση του αριθμού σελίδων επιβεβαιώνει ότι το `setPageRange` λειτούργησε, και το απόσπασμα του εξαγόμενου κειμένου αποδεικνύει ότι το OCR αναγνώρισε χαρακτήρες.

## Step 7 – Save the Searchable PDF  

Τέλος, γράψτε το αποτέλεσμα πίσω στο δίσκο. Η σταθερά `ImageFormats.PDF` λέει στο Aspose να κρατήσει το αρχείο ως PDF, τώρα εμπλουτισμένο με αναζητήσιμο κείμενο.

```python
# Step 7: Save the searchable PDF
output_path = "YOUR_DIRECTORY/output.pdf"
ocr_engine.save(output_path, ImageFormats.PDF)

print(f"Searchable PDF saved to: {output_path}")
```

Ανοίξτε το παραγόμενο αρχείο σε οποιονδήποτε PDF reader και δοκιμάστε μια αναζήτηση κειμένου—voilà, έχετε **created searchable pdf**!

## Handling Common Edge Cases  

### When the source is an *image‑only* PDF  

Αν το εισαγόμενο PDF περιέχει μόνο εικόνες (χωρίς στρώση κειμένου), ο ίδιος κώδικας λειτουργεί—απλώς βεβαιωθείτε ότι το `setEmbedRecognisedText(True)` παραμένει ενεργό. Μπορεί επίσης να θέλετε να αυξήσετε το DPI για καλύτερη ακρίβεια:

```python
pdf_options.setResolution(300)  # 300 DPI gives sharper OCR results
```

### Dealing with Multiple Languages  

Το Aspose OCR υποστηρίζει language packs. Φορτώστε μια γλώσσα πριν καλέσετε `recognize()`:

```python
ocr_engine.setLanguage("spa")   # Spanish language pack
```

### Large Documents  

Η επεξεργασία ενός 500‑σελιδικού σαρωμένου PDF μπορεί να καταναλώσει πολύ μνήμη. Διαχωρίστε τη δουλειά:

1. Επανάληψη σε εύρη σελίδων (`setPageRange(start, end)`).  
2. Αποθήκευση κάθε τμήματος ως προσωρινό searchable PDF.  
3. Συγχώνευση των τμημάτων με `PdfMerger` (άλλο στοιχείο του Aspose).

## Full Working Example (All Steps Together)

```python
# Full script – create searchable PDF from a scanned document
from aspose.ocr import OcrEngine, PdfRecognitionOptions, ImageFormats

def create_searchable_pdf(input_file: str, output_file: str, start_page: int = 1, end_page: int = 0):
    """
    Convert a scanned or image‑only PDF into a searchable PDF.
    :param input_file: Path to the source PDF.
    :param output_file: Destination path for the searchable PDF.
    :param start_page: First page to process (1‑based). Default = 1.
    :param end_page: Last page to process. 0 means “till the end”.
    """
    # Initialize engine
    ocr_engine = OcrEngine()
    ocr_engine.setImageFromFile(input_file)

    # Set options
    pdf_opts = PdfRecognitionOptions()
    pdf_opts.setEmbedRecognisedText(True)          # embed searchable text
    pdf_opts.setTextExtractionMode(True)           # allow text extraction
    if end_page > 0:
        pdf_opts.setPageRange(start_page, end_page)  # selective processing
    else:
        pdf_opts.setPageRange(start_page, start_page)  # process from start_page onward

    # Attach options
    ocr_engine.setPdfRecognitionOptions(pdf_opts)

    # Run OCR
    result = ocr_engine.recognize()
    print("Pages processed:", result.getPageCount())

    # Optional verification
    print("\nSample extracted text (first page):")
    print(result.getPageText(0)[:300])

    # Save searchable PDF
    ocr_engine.save(output_file, ImageFormats.PDF)
    print(f"Searchable PDF saved to: {output_file}")

if __name__ == "__main__":
    create_searchable_pdf(
        input_file="YOUR_DIRECTORY/input.pdf",
        output_file="YOUR_DIRECTORY/output.pdf",
        start_page=1,
        end_page=3   # change or set to 0 to process the whole file
    )
```

Η εκτέλεση αυτού του script θα σας δώσει ένα **searchable PDF** που μπορείτε να ανοίξετε σε Adobe Reader, Chrome ή οποιονδήποτε PDF viewer και να κάνετε άμεση αναζήτηση λέξεων.

## Conclusion  

Τώρα έχετε μια πλήρη, end‑to‑end λύση για **create searchable PDF** χρησιμοποιώντας το Aspose OCR. Από τη φόρτωση της πηγής, τη ρύθμιση επιλογών που **convert scanned pdf**, την εξαγωγή και επαλήθευση κειμένου, μέχρι την τελική αποθήκευση του αναζητήσιμου αποτελέσματος, κάθε βήμα καλύπτεται.  

Στη συνέχεια, ίσως θελήσετε να εξερευνήσετε σενάρια **convert image pdf** όπου η πηγή είναι μια σειρά JPEG που έχουν συσκευαστεί σε PDF, ή να εμβαθύνετε στην OCR ειδικά για γλώσσες ώστε να βελτιώσετε την ακρίβεια σε πολυγλωσσικά έγγραφα. Σε κάθε περίπτωση, το μοτίβο παραμένει το ίδιο: ορίστε τις επιλογές, τρέξτε `recognize()`, και αποθηκεύστε.

Πειραματιστείτε ελεύθερα—αλλάξτε το εύρος σελίδων, ρυθμίστε το DPI, ή προσθέστε ένα προσαρμοσμένο λεξικό. Αν αντιμετωπίσετε προβλήματα, αφήστε ένα σχόλιο παρακάτω ή ελέγξτε τα επίσημα docs του Aspose για τις πιο πρόσφατες λεπτομέρειες του API. Καλή OCR

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}