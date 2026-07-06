---
category: general
date: 2026-06-19
description: Πώς να εξάγετε PDF χρησιμοποιώντας OCR σε Python – βήμα‑βήμα tutorial
  που καλύπτει την εξαγωγή κειμένου από PDF, την αναγνώριση κειμένου από εικόνα και
  ένα παράδειγμα OCR σε Python.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize text from image
- ocr python example
- read pdf with ocr
language: el
og_description: Πώς να εξάγετε PDF χρησιμοποιώντας OCR σε Python. Μάθετε πώς να εξάγετε
  κείμενο από PDF, να αναγνωρίζετε κείμενο από εικόνα και δείτε ένα πλήρες παράδειγμα
  OCR σε Python.
og_title: Πώς να εξάγετε κείμενο PDF με OCR στην Python – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  headline: How to Extract PDF Text with OCR in Python – Complete Guide
  type: TechArticle
- description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  name: How to Extract PDF Text with OCR in Python – Complete Guide
  steps:
  - name: – Install the Required Packages
    text: First, we need an OCR engine. The example below uses the popular **ocr**
      package (a thin wrapper around Tesseract). If you prefer a different backend,
      the concepts stay the same.
  - name: – Initialize the OCR Engine and Set Language
    text: Now we spin up the engine and tell it to look for English characters. You
      can swap `ocr.Language.English` for any supported language code.
  - name: – Load a PDF Page as an Image
    text: OCR works on raster images, not PDF objects. The `ocr.Image.from_pdf` helper
      renders the chosen page to a bitmap. Adjust `page_number` for other pages (0‑based
      indexing).
  - name: – Recognize Text from the Rendered Image
    text: Here’s the heart of the **ocr python example**. The engine processes the
      bitmap and returns an object containing the extracted string.
  - name: – Print or Store the Extracted Text
    text: Finally, we output the result. In a real application you’d probably write
      to a file or a database.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Πώς να εξάγετε κείμενο PDF με OCR σε Python – Πλήρης οδηγός
url: /el/python-java/general/how-to-extract-pdf-text-with-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εξάγετε κείμενο PDF με OCR στην Python – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να εξάγετε PDF** περιεχόμενο όταν το αρχείο είναι απλώς μια σαρωμένη εικόνα; Δεν είστε μόνοι. Σε πολλά πραγματικά έργα—συμβόλαια, τιμολόγια ή ιστορικά αρχεία—το PDF που λαμβάνετε δεν έχει επιλέξιμο κείμενο. Το καλό νέο; Μερικές γραμμές Python μπορούν να μετατρέψουν αυτές τις σελίδες μόνο με εικόνα σε αναζητήσιμο, επεξεργάσιμο κείμενο.

Σε αυτό το tutorial θα περάσουμε από ένα πρακτικό **OCR Python example** που διαβάζει ένα PDF, αποδίδει την πρώτη του σελίδα ως εικόνα και στη συνέχεια **εξάγει κείμενο από PDF** χρησιμοποιώντας μια μηχανή OCR. Στο τέλος θα ξέρετε ακριβώς πώς να **διαβάσετε PDF με OCR**, γιατί κάθε βήμα είναι σημαντικό και πώς να προσαρμόσετε τον κώδικα για έγγραφα πολλαπλών σελίδων ή διαφορετικές γλώσσες.

## Τι Θα Μάθετε

- Εγκατάσταση και ρύθμιση μιας αξιόπιστης βιβλιοθήκης OCR για Python.  
- Μετατροπή σελίδων PDF σε εικόνες κατάλληλες για OCR.  
- **Αναγνώριση κειμένου από εικόνα** και λήψη καθαρών συμβολοσειρών Unicode.  
- Συνηθισμένα προβλήματα (PDF χαμηλής ανάλυσης, περιστρεφόμενες σελίδες) και πώς να τα αποφύγετε.  
- Επέκταση του script για διαχείριση πολλαπλών σελίδων ή μαζική επεξεργασία.

**Προαπαιτούμενα**: Python 3.8+, pip, και βασική κατανόηση εικονικών περιβαλλόντων. Δεν απαιτείται προηγούμενη εμπειρία OCR—απλώς ακολουθήστε τα βήματα.

---

## ## Πώς να εξάγετε κείμενο PDF με OCR στην Python

Αυτή η επικεφαλίδα H2 περιέχει τη βασική μας λέξη‑κλειδί ακριβώς εκεί που τις αγαπούν οι μηχανές αναζήτησης. Ας βουτήξουμε κατευθείαν στον κώδικα.

### Βήμα 1 – Εγκατάσταση των Απαιτούμενων Πακέτων

Πρώτα, χρειαζόμαστε μια μηχανή OCR. Το παρακάτω παράδειγμα χρησιμοποιεί το δημοφιλές πακέτο **ocr** (μια ελαφριά επικάλυψη γύρω από το Tesseract). Αν προτιμάτε διαφορετικό backend, οι έννοιες παραμένουν οι ίδιες.

```bash
# Create a fresh virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR wrapper and Pillow for image handling
pip install ocr pillow
```

> **Pro tip:** Σε Linux, θα χρειαστείτε επίσης το εκτελέσιμο Tesseract: `sudo apt-get install tesseract-ocr`. Οι χρήστες macOS μπορούν να το εγκαταστήσουν μέσω Homebrew: `brew install tesseract`.

### Βήμα 2 – Αρχικοποίηση της Μηχανής OCR και Ορισμός Γλώσσας

Τώρα ξεκινάμε τη μηχανή και της λέμε να ψάξει για αγγλικούς χαρακτήρες. Μπορείτε να αντικαταστήσετε το `ocr.Language.English` με οποιονδήποτε υποστηριζόμενο κωδικό γλώσσας.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English
```

**Γιατί είναι σημαντικό:** Η καθορισμένη γλώσσα βελτιώνει δραστικά την ακρίβεια, επειδή η μηχανή μπορεί να εφαρμόσει λεξικά και μοντέλα χαρακτήρων ειδικά για τη γλώσσα.

### Βήμα 3 – Φόρτωση μιας Σελίδας PDF ως Εικόνα

Το OCR λειτουργεί σε raster εικόνες, όχι σε αντικείμενα PDF. Η βοηθητική συνάρτηση `ocr.Image.from_pdf` αποδίδει την επιλεγμένη σελίδα σε bitmap. Προσαρμόστε το `page_number` για άλλες σελίδες (αρίθμηση από το 0).

```python
# Step 2: Load the first page of the PDF as an image
pdf_file_path = "YOUR_DIRECTORY/contract.pdf"
page_image = ocr.Image.from_pdf(pdf_file_path, page_number=1)
```

> **Edge case:** Αν το PDF περιέχει διανυσματικά γραφικά αντί για σαρωμένες εικόνες, μπορεί να λάβετε μια καθαρή απόδοση. Για σαρώσεις χαμηλής ανάλυσης, σκεφτείτε να αυξήσετε το DPI: `ocr.Image.from_pdf(..., dpi=300)`.

### Βήμα 4 – Αναγνώριση Κειμένου από την Αποδοθείσα Εικόνα

Αυτή είναι η καρδιά του **ocr python example**. Η μηχανή επεξεργάζεται το bitmap και επιστρέφει ένα αντικείμενο που περιέχει την εξαγόμενη συμβολοσειρά.

```python
# Step 3: Recognize text from the rendered page image
ocr_result = ocr_engine.recognize(page_image)
```

Το χαρακτηριστικό `ocr_result.text` περιέχει το απλό‑κείμενο αποτέλεσμα, διατηρώντας τις αλλαγές γραμμής όπου είναι δυνατόν.

### Βήμα 5 – Εκτύπωση ή Αποθήκευση του Εξαγόμενου Κειμένου

Τέλος, εμφανίζουμε το αποτέλεσμα. Σε μια πραγματική εφαρμογή πιθανότατα θα γράψετε σε αρχείο ή βάση δεδομένων.

```python
# Step 4: Print the extracted text
print(ocr_result.text)
```

Η εκτέλεση του script θα πρέπει να εμφανίσει κάτι όπως:

```
THIS AGREEMENT is made on the 1st day of January 2024...
```

Αυτό είναι ένα πλήρες workflow **extract text from pdf** χρησιμοποιώντας OCR.

---

## ## Αναγνώριση Κειμένου από Εικόνα – Βελτιστοποίηση Ακρίβειας

Αν σας ενδιαφέρει μόνο η **αναγνώριση κειμένου από εικόνα** (π.χ. ένα JPEG από απόδειξη), μπορείτε να παραλείψετε το βήμα μετατροπής PDF:

```python
image_path = "receipt.jpg"
page_image = ocr.Image.from_file(image_path)   # Directly load an image
ocr_result = ocr_engine.recognize(page_image)
print(ocr_result.text)
```

**Συμβουλές για καλύτερα αποτελέσματα:**

- **Προ‑επεξεργασία** της εικόνας: μετατροπή σε γκρι, εφαρμογή κατωφλίου ή διόρθωση κλίσης. Η Pillow το κάνει εύκολα.  
- **Αύξηση DPI** κατά την απόδοση PDF: υψηλότερη ανάλυση δίνει στη μηχανή OCR περισσότερες λεπτομέρειες.  
- **Ενεργοποίηση ρυθμίσεων OCR** για τμηματοποίηση σελίδας (`ocr_engine.config = "--psm 6"` για ομοιόμορφα μπλοκ).

---

## ## Διαβάστε PDF με OCR – Διαχείριση Πολλαπλών Σελίδων

Τα περισσότερα συμβόλαια εκτείνονται σε πολλές σελίδες. Η επανάληψη πάνω σε κάθε σελίδα είναι απλή:

```python
def extract_all_pages(pdf_path):
    all_text = []
    for i in range(ocr.Image.pdf_page_count(pdf_path)):
        img = ocr.Image.from_pdf(pdf_path, page_number=i)
        result = ocr_engine.recognize(img)
        all_text.append(result.text)
    return "\n--- PAGE BREAK ---\n".join(all_text)

full_text = extract_all_pages("YOUR_DIRECTORY/contract.pdf")
print(full_text)
```

Αυτή η συνάρτηση **reads PDF with OCR**, ενώνει το αποτέλεσμα και προσθέτει έναν σαφή διαχωριστή σελίδας. Στη συνέχεια μπορείτε να τροφοδοτήσετε το `full_text` σε έναν δείκτη αναζήτησης ή να το αποθηκεύσετε ως αρχείο `.txt`.

---

## ## Συνηθισμένα Προβλήματα και Πώς να Τα Διορθώσετε

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Κατεστραμμένοι χαρακτήρες, πολλά `?` | Λάθος γλώσσα ή έλλειψη αρχείων δεδομένων γλώσσας | Εγκαταστήστε το σωστό πακέτο γλώσσας Tesseract (`tesseract-ocr-<lang>`) και ορίστε `ocr_engine.language`. |
| Λείπουν γραμμές ή κομμένες λέξεις | Χαμηλό DPI (κάτω από 150) | Αποδώστε το PDF σε 300 DPI ή περισσότερο (`dpi=300`). |
| Το κείμενο είναι περιστρεφόμενο ή ανάποδο | Η σαρωμένη σελίδα δεν είναι ευθεία | Χρησιμοποιήστε `ocr.Image.deskew(page_image)` πριν την αναγνώριση. |
| Αργή επεξεργασία σε μεγάλα PDFs | Επεξεργασία σελίδων διαδοχικά σε ένα νήμα | Παράλληλη εκτέλεση με `concurrent.futures.ThreadPoolExecutor`. |

---

## ## Επέκταση του OCR Python Example

- **Εξαγωγή σε PDF/A**: Μετά την εξαγωγή, μπορείτε να ενσωματώσετε το κείμενο πίσω σε ένα αναζητήσιμο PDF χρησιμοποιώντας `reportlab` ή `pypdf2`.  
- **Ανίχνευση γλώσσας**: Χρησιμοποιήστε `langdetect` στο αποτέλεσμα OCR για να αλλάζετε δυναμικά το `ocr_engine.language`.  
- **Μαζική επεξεργασία**: Περιηγηθείτε σε έναν φάκελο με `os.listdir` και εφαρμόστε `extract_all_pages` σε κάθε αρχείο.

---

## ## Αναμενόμενο Αποτέλεσμα και Επαλήθευση

Όταν εκτελέσετε το script σε μια καθαρή σάρωση αγγλικής γλώσσας, θα πρέπει να δείτε ένα καθαρό μπλοκ κειμένου με σωστή στίξη. Επαληθεύστε:

1. Συγκρίνοντας μερικές γραμμές με την αρχική σαρωμένη εικόνα.  
2. Εκτελώντας έναν απλό υπολογισμό λέξεων (`len(ocr_result.text.split())`) για να βεβαιωθείτε ότι το αποτέλεσμα δεν είναι κενό.  
3. Προαιρετικά, τροφοδοτώντας το αποτέλεσμα σε έναν ορθογραφικό ελεγκτή όπως `pyspellchecker` για να εντοπίσετε σφάλματα OCR.

---

## Συμπέρασμα

Καλύψαμε **πώς να εξάγετε PDF** περιεχόμενο όταν η παραδοσιακή ανάλυση αποτυγχάνει, παρουσιάσαμε ένα πλήρες **ocr python example**, και εξηγήσαμε πώς να **αναγνωρίσετε κείμενο από εικόνα** και να **διαβάσετε PDF με OCR** για σενάρια μονής ή πολλαπλών σελίδων. Με τα παραπάνω αποσπάσματα κώδικα μπορείτε τώρα να μετατρέψετε οποιοδήποτε σαρωμένο PDF σε αναζητήσιμο, επεξεργάσιμο κείμενο—χωρίς να χρειάζεται να πληκτρολογείτε χειροκίνητα.

Τι θα κάνετε στη συνέχεια; Δοκιμάστε να αλλάξετε τη γλώσσα σε Ισπανικά (`ocr.Language.Spanish`) ή πειραματιστείτε με τεχνικές προ‑επεξεργασίας εικόνας για να αυξήσετε την ακρίβεια. Αν χτίζετε σύστημα διαχείρισης εγγράφων, σκεφτείτε να ευρετηριάσετε το εξαγόμενο κείμενο με Elasticsearch για αστραπιαία αναζήτηση.

Έχετε ερωτήσεις ή αντιμετωπίζετε κάποιο ιδιότροπο PDF; Αφήστε ένα σχόλιο, και καλή προγραμματιστική δουλειά!  

![How to extract PDF using OCR in Python](image.png "How to extract PDF using OCR in Python")


## Τι Θα Μάθετε Στη Σειρά Επόμενη;

Οι παρακάτω οδηγίες καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση των δικών σας έργων.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}