---
category: general
date: 2026-06-06
description: Πώς να κάνετε OCR σε PDF χρησιμοποιώντας το Aspose OCR Cloud. Μάθετε
  να εξάγετε κείμενο από PDF, να μετατρέπετε σελίδα PDF σε PNG και να αποθηκεύετε
  εικόνες σελίδων PDF με Python.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf page png
- extract plain text pdf
- save pdf page images
language: el
og_description: Πώς να κάνετε OCR PDF με το Aspose OCR Cloud. Αυτός ο οδηγός δείχνει
  πώς να εξάγετε απλό κείμενο PDF, να μετατρέψετε σελίδα PDF σε PNG και να αποθηκεύσετε
  τις εικόνες των σελίδων PDF.
og_title: Πώς να κάνετε OCR PDF με το Aspose OCR Cloud – Βήμα προς βήμα
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Aspose OCR Cloud. Learn to extract text from PDF,
    convert PDF page PNG, and save PDF page images in Python.
  headline: How to OCR PDF with Aspose OCR Cloud – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: Πώς να κάνετε OCR PDF με το Aspose OCR Cloud – Πλήρης Οδηγός
url: /el/python-java/general/how-to-ocr-pdf-with-aspose-ocr-cloud-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να κάνετε OCR PDF με το Aspose OCR Cloud – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να κάνετε OCR PDF** αρχεία χωρίς να παλεύετε με βαριά εργαλεία επιφάνειας εργασίας; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν χρειάζονται έναν γρήγορο, προγραμματιστικό τρόπο να εξάγουν κείμενο από σαρωμένα έγγραφα. Τα καλά νέα; Με το Aspose OCR Cloud μπορείτε **να εξάγετε κείμενο από PDF**, να μετατρέψετε κάθε σελίδα σε PNG, και ακόμη **να αποθηκεύσετε εικόνες σελίδων PDF** για μελλοντική χρήση, όλα από ένα καθαρό script Python.

Σε αυτό το tutorial θα περάσουμε από όλα όσα χρειάζεται να γνωρίζετε: από την εγκατάσταση του SDK, την αδειοδότηση της μηχανής, και την αναγνώριση πολυ‑σελίδων PDF, μέχρι την εξαγωγή απλού κειμένου, τη μετατροπή σελίδων σε PNG, και την αποθήκευση αυτών των εικόνων στο δίσκο. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο snippet που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο χρειάζεται **how to OCR PDF** δυνατότητες.

## Τι Θα Χρειαστείτε

- **Python 3.8+** (ο κώδικας λειτουργεί επίσης σε 3.10 και νεότερες εκδόσεις)  
- Ένας λογαριασμός Aspose OCR Cloud – θα λάβετε ένα δωρεάν αρχείο άδειας δοκιμής (`Aspose.OCR.lic`)  
- Το πακέτο `asposeocrcloud` (`pip install asposeocrcloud`)  
- Ένα σαρωμένο, πολυ‑σελίδες PDF που θέλετε να επεξεργαστείτε  

Αυτό είναι όλο. Χωρίς επιπλέον δυαδικά αρχεία, χωρίς εγγενείς εξαρτήσεις, μόνο καθαρό Python.

## Πώς να κάνετε OCR PDF – Ρύθμιση και Άδεια

Πριν μπορέσετε να καλέσετε οποιεσδήποτε μεθόδους OCR, πρέπει να ενημερώσετε το SDK ποιος είστε. Η Aspose χρησιμοποιεί ένα ελαφρύ αρχείο άδειας που τοποθετείτε κάπου προσβάσιμο στο script σας.

```python
# Step 1: Import the OCR package and apply your license (optional but recommended)
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply the license – replace the path with your actual .lic file location
License().set_license("Aspose.OCR.lic")
```

*Συμβουλή:* Αν παραλείψετε το βήμα της άδειας, το SDK θα λειτουργήσει ακόμα αλλά θα ενσωματώσει ένα μικρό υδατογράφημα στις εικόνες εξόδου. Δεν είναι ιδανικό για παραγωγή.

## Βήμα 2: Εγκατάσταση του Aspose OCR Cloud Python SDK

Ανοίξτε ένα τερματικό και εκτελέστε:

```bash
pip install asposeocrcloud
```

Το πακέτο φέρνει όλες τις απαιτούμενες εξαρτήσεις (requests, pillow, κλπ.) ώστε να μην χρειάζεται να ψάχνετε για κάτι άλλο.

## Βήμα 3: Δημιουργία Μηχανής OCR και Επιλογή Γλώσσας

Η μηχανή είναι η καρδιά της λειτουργίας. Μπορείτε να καθορίσετε οποιαδήποτε γλώσσα υποστηρίζεται από την Aspose· η Αγγλική λειτουργεί στις περισσότερες περιπτώσεις.

```python
# Step 3: Create an OCR engine and set the recognition language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)
```

Γιατί να ορίσετε τη γλώσσα; Επειδή η μηχανή OCR χρησιμοποιεί λεξικά ειδικά για τη γλώσσα ώστε να βελτιώσει την ακρίβεια. Αν επεξεργάζεστε PDF στα Γαλλικά, απλώς αντικαταστήστε το `ENGLISH` με `FRENCH`.

## Βήμα 4: Καθορίστε το Πολυ‑Σελίδες PDF Σας

Δώστε στη μηχανή τη πλήρη διαδρομή του αρχείου που θέλετε να επεξεργαστείτε. Οι σχετικές διαδρομές είναι εντάξει εφόσον λύνουν από τον τρέχοντα φάκελο του script.

```python
# Step 4: Specify the path to the multi‑page PDF you want to process
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"
```

Βεβαιωθείτε ότι το αρχείο είναι αναγνώσιμο· διαφορετικά θα δείτε ένα `FileNotFoundError`.

## Βήμα 5: Εκτέλεση OCR – Λαμβάνετε μια Λίστα Αποτελεσμάτων

Η κλήση του `recognize_pdf` επιστρέφει μια λίστα όπου κάθε στοιχείο αντιστοιχεί σε μία σελίδα του αρχικού PDF.

```python
# Step 5: Run OCR on the PDF – a list of OcrResult objects is returned (one per page)
results = engine.recognize_pdf(pdf_path)
```

Κάθε `OcrResult` περιέχει δύο χρήσιμες ιδιότητες:

* `text` – η αναπαράσταση plain‑text της σελίδας (ιδανικό για **extract plain text pdf**)
* `image` – ένα αντικείμενο Pillow `Image` της αποδομένης σελίδας (τέλειο για **convert pdf page png**)

## Βήμα 6: Εξαγωγή Κειμένου από PDF και Μετατροπή Σελίδων σε PNG

Τώρα επαναλαμβάνουμε τα αποτελέσματα, εκτυπώνουμε το εξαγόμενο κείμενο και αποθηκεύουμε μια έκδοση PNG κάθε σελίδας.

```python
# Step 6: Iterate through each page, output the extracted text and optionally save the page image
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    # Extract plain text for this page
    print(res.text)                     # <-- this is the "extract plain text pdf" part
    # Convert the page to PNG and save it
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # <-- this does the "convert pdf page png"
```

### Αναμενόμενη Εξαγωγή στην Κονσόλα

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Θα βρείτε επίσης τα `page_1.png`, `page_2.png`, … στον φάκελο `YOUR_DIRECTORY`. Αυτές είναι οι rasterized εικόνες σελίδων που μπορείτε να τροφοδοτήσετε σε επόμενες pipelines επεξεργασίας εικόνας.

## Βήμα 7: Αποθήκευση Εικόνων Σελίδων PDF (Προαιρετική Μετα-Επεξεργασία)

Αν χρειάζεστε μόνο τις εικόνες και όχι το κείμενο, μπορείτε να παραλείψετε τη γραμμή `print(res.text)`. Αντίστροφα, αν θέλετε να αποθηκεύσετε το κείμενο σε ξεχωριστά αρχεία `.txt`, απλώς προσθέστε μια μικρή εγγραφή:

```python
# Optional: Save each page's text to a .txt file
for i, res in enumerate(results, start=1):
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)
```

Αυτή η μικρή προσθήκη δείχνει πόσο εύκολο είναι να **save PDF page images** ενώ ταυτόχρονα αποθηκεύετε το εξαγόμενο περιεχόμενο.

## Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας όλα, εδώ είναι το πλήρες script που μπορείτε να αντιγράψετε‑επικολλήσετε στο `ocr_pdf.py`:

```python
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply your license – optional but removes watermarks
License().set_license("Aspose.OCR.lic")

# Initialize the OCR engine and set language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)

# Path to the source PDF
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"

# Run OCR – get a list of results (one per page)
results = engine.recognize_pdf(pdf_path)

# Process each page
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(res.text)  # extract plain text PDF
    # Save the rendered page as PNG
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # convert PDF page PNG
    # Optional: also save the text to a .txt file
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)  # save PDF page images + text
```

Τρέξτε το με:

```bash
python ocr_pdf.py
```

Θα πρέπει να δείτε την εκτύπωση στην κονσόλα του κειμένου κάθε σελίδας και μια σειρά από αρχεία PNG

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να κάνετε OCR PDF σε .NET με το Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Αναγνώριση Κειμένου PDF – Λειτουργίες OCR με το Aspose.OCR για Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Μετατροπή Εικόνων σε PDF C# – Αποθήκευση Πολυσελίδας OCR Αποτελέσματος](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}