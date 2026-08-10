---
category: general
date: 2026-04-29
description: Εξαγωγή κειμένου από PDF χρησιμοποιώντας το Aspose OCR σε Python. Μάθετε
  την επεξεργασία PDF με batch OCR, μετατρέψτε το κείμενο σκαναρισμένων PDF και διαχειριστείτε
  σελίδες χαμηλής εμπιστοσύνης.
draft: false
keywords:
- extract text from pdf
- ocr pdf with python
- convert scanned pdf text
- batch ocr pdf processing
language: el
og_description: Εξαγωγή κειμένου από PDF με το Aspose OCR σε Python. Αυτός ο οδηγός
  δείχνει επεξεργασία PDF με OCR σε παρτίδες, μετατροπή κειμένου από σαρωμένα PDF
  και διαχείριση αποτελεσμάτων χαμηλής εμπιστοσύνης.
og_title: Εξαγωγή κειμένου από PDF – OCR PDF με Python
tags:
- OCR
- Python
- PDF processing
title: Εξαγωγή κειμένου από PDF – OCR PDF με Python
url: /el/python/general/extract-text-from-pdf-ocr-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από PDF – OCR PDF με Python

Έχετε ποτέ χρειαστεί να **εξάγετε κείμενο από PDF** αλλά το αρχείο είναι μόνο μια σαρωμένη εικόνα; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν προσπαθούν να μετατρέψουν τα PDF σε αναζητήσιμα δεδομένα. Τα καλά νέα; Με το Aspose OCR for Python μπορείτε να μετατρέψετε το κείμενο από σαρωμένα PDF με λίγες γραμμές κώδικα, και ακόμη να εκτελέσετε **batch OCR PDF processing** όταν έχετε δεκάδες αρχεία προς επεξεργασία.

Σε αυτό το tutorial θα περάσουμε από όλη τη ροή εργασίας: τη ρύθμιση της βιβλιοθήκης, την εκτέλεση OCR σε ένα μόνο PDF, την κλιμάκωση σε batch, και τη διαχείριση σελίδων με χαμηλή εμπιστοσύνη ώστε να ξέρετε πότε απαιτείται χειροκίνητη ανασκόπηση. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση script που εξάγει κείμενο από οποιοδήποτε σαρωμένο PDF, και θα κατανοήσετε το «γιατί» κάθε βήματος.

## Τι Θα Χρειαστεί

Πριν προχωρήσουμε, βεβαιωθείτε ότι έχετε:

- Python 3.8 ή νεότερη (ο κώδικας χρησιμοποιεί f‑strings, επομένως η 3.6+ λειτουργεί, αλλά συνιστάται η 3.8+).
- Άδεια Aspose OCR for Python ή κλειδί δωρεάν δοκιμής (μπορείτε να αποκτήσετε ένα από την ιστοσελίδα Aspose).
- Έναν φάκελο με ένα ή περισσότερα σαρωμένα PDF που θέλετε να επεξεργαστείτε.
- Μια μέτρια ποσότητα χώρου στο δίσκο για τις παραγόμενες αναφορές *.txt*.

Αυτό είναι όλο—χωρίς βαριές εξωτερικές εξαρτήσεις, χωρίς τρικαλό OpenCV. Η μηχανή Aspose OCR κάνει το σκληρό έργο για εσάς.

## Ρύθμιση του Περιβάλλοντος

Πρώτα, εγκαταστήστε το πακέτο Aspose OCR από το PyPI:

```bash
pip install aspose-ocr
```

Αν έχετε αρχείο άδειας (`Aspose.OCR.lic`), τοποθετήστε το στη ρίζα του έργου σας και ενεργοποιήστε το ως εξής:

```python
# Activate Aspose OCR license (optional but removes trial watermark)
from aspose.ocr import License

license = License()
license.set_license("Aspose.OCR.lic")
```

> **Pro tip:** Κρατήστε το αρχείο άδειας εκτός ελέγχου εκδόσεων· προσθέστε το στο `.gitignore` για να αποφύγετε τυχαία αποκάλυψη.

## Εκτέλεση OCR σε Ένα PDF

Τώρα ας εξάγουμε κείμενο από ένα μόνο σαρωμένο PDF. Τα βασικά βήματα είναι:

1. Δημιουργήστε μια παρουσία `OcrEngine`.
2. Κατευθύνετέ το στο αρχείο PDF.
3. Ανακτήστε ένα `OcrResult` για κάθε σελίδα.
4. Γράψτε την έξοδο plain‑text στο δίσκο.
5. Αποδεσμεύστε τη μηχανή για να ελευθερώσετε τους εγγενείς πόρους.

Ακολουθεί το πλήρες, εκτελέσιμο script:

```python
# Step 1: Import the OCR engine and create an instance
from aspose.ocr import OcrEngine

# Optional: activate license (see previous section)
# from aspose.ocr import License
# License().set_license("Aspose.OCR.lic")

ocr_engine = OcrEngine()

# Step 2: Specify the PDF file to be processed
pdf_file_path = r"YOUR_DIRECTORY/input.pdf"

# Step 3: Extract OCR results – one OcrResult object per page
ocr_pages = ocr_engine.extract_from_pdf(pdf_file_path)

# Step 4: Iterate through the results, show confidence, flag low‑confidence pages, and save the plain text
for ocr_page in ocr_pages:
    print(f"Page {ocr_page.page_number}: confidence {ocr_page.confidence:.2%}")

    # If confidence is below 80 %, flag it for manual review
    if ocr_page.confidence < 0.80:
        print("  Low confidence – consider manual review")

    # Build the output filename
    output_txt = f"YOUR_DIRECTORY/Report_page{ocr_page.page_number}.txt"
    with open(output_txt, "w", encoding="utf-8") as f:
        f.write(ocr_page.text)

# Step 5: Release resources used by the engine
ocr_engine.dispose()
```

**What you’ll see:** Για κάθε σελίδα το script εκτυπώνει κάτι όπως `Page 1: confidence 97.45%`. Αν μια σελίδα πέσει κάτω από το όριο 80 %, εμφανίζεται μια προειδοποίηση, ενημερώνοντάς σας ότι το OCR μπορεί να έχει χάσει χαρακτήρες.

### Γιατί Λειτουργεί Αυτό

- `OcrEngine` είναι η πύλη προς τη φυσική βιβλιοθήκη Aspose OCR· διαχειρίζεται τα πάντα από την προεπεξεργασία εικόνας μέχρι την αναγνώριση χαρακτήρων.
- `extract_from_pdf` ραστεροποιεί αυτόματα κάθε σελίδα PDF, έτσι δεν χρειάζεται να μετατρέψετε το PDF σε εικόνες εσείς.
- Οι βαθμολογίες εμπιστοσύνης σας επιτρέπουν να αυτοματοποιήσετε ελέγχους ποιότητας—κρίσιμα όταν επεξεργάζεστε νομικά ή ιατρικά έγγραφα όπου η ακρίβεια έχει σημασία.

## Batch OCR Επεξεργασία PDF με Python

Τα περισσότερα πραγματικά έργα περιλαμβάνουν περισσότερα από ένα αρχεία. Ας επεκτείνουμε το script ενός αρχείου σε μια **batch OCR PDF processing** pipeline που διασχίζει έναν φάκελο, επεξεργάζεται κάθε PDF και αποθηκεύει τα αποτελέσματα σε έναν αντίστοιχο υπο‑φάκελο.

```python
import os
from pathlib import Path
from aspose.ocr import OcrEngine

def ocr_pdf_file(pdf_path: Path, output_dir: Path, engine: OcrEngine, confidence_threshold: float = 0.80):
    """Extract text from a single PDF and write per‑page .txt files."""
    ocr_pages = engine.extract_from_pdf(str(pdf_path))
    for page in ocr_pages:
        print(f"{pdf_path.name} – Page {page.page_number}: {page.confidence:.2%}")
        if page.confidence < confidence_threshold:
            print("  ⚠️ Low confidence – manual review may be needed")

        out_file = output_dir / f"{pdf_path.stem}_page{page.page_number}.txt"
        out_file.write_text(page.text, encoding="utf-8")

def batch_ocr_pdf(input_folder: str, output_folder: str):
    """Iterate over all PDFs in input_folder and run OCR."""
    engine = OcrEngine()
    input_path = Path(input_folder)
    output_path = Path(output_folder)
    output_path.mkdir(parents=True, exist_ok=True)

    pdf_files = list(input_path.glob("*.pdf"))
    if not pdf_files:
        print("🚫 No PDF files found in the specified folder.")
        return

    for pdf_file in pdf_files:
        # Create a sub‑folder for each PDF to keep pages organized
        pdf_out_dir = output_path / pdf_file.stem
        pdf_out_dir.mkdir(exist_ok=True)
        ocr_pdf_file(pdf_file, pdf_out_dir, engine)

    # Clean up native resources
    engine.dispose()
    print("✅ Batch OCR completed.")

# Example usage:
if __name__ == "__main__":
    batch_ocr_pdf("YOUR_DIRECTORY/input_pdfs", "YOUR_DIRECTORY/ocr_output")
```

#### Πώς Αυτό Βοηθά

- **Scalability:** Η συνάρτηση διασχίζει το φάκελο μία φορά, δημιουργώντας έναν αφιερωμένο υπο‑φάκελο εξόδου για κάθε PDF. Αυτό διατηρεί τα πράγματα οργανωμένα όταν έχετε δεκάδες έγγραφα.
- **Reusability:** Η `ocr_pdf_file` μπορεί να κληθεί από άλλα scripts (π.χ., μια web υπηρεσία) επειδή είναι καθαρή συνάρτηση.
- **Error handling:** Το script εκτυπώνει ένα φιλικό μήνυμα αν ο φάκελος εισόδου είναι κενός, αποφεύγοντας μια σιωπηλή αποτυχία.

## Μετατροπή Κειμένου από Σαρωμένα PDF – Διαχείριση Ακραίων Περιπτώσεων

Αν και ο παραπάνω κώδικας λειτουργεί για τα περισσότερα PDF, μπορεί να αντιμετωπίσετε μερικές ιδιαιτερότητες:

| Κατάσταση | Γιατί Συμβαίνει | Πώς να Μετριάσετε |
|-----------|----------------|-------------------|
| **Encrypted PDFs** | Το PDF είναι προστατευμένο με κωδικό. | Περάστε τον κωδικό στο `extract_from_pdf(pdf_path, password="yourPwd")`. |
| **Multi‑language documents** | Το Aspose OCR προεπιλογή είναι η Αγγλική. | Ορίστε `ocr_engine.language = "spa"` για Ισπανικά, ή δώστε μια λίστα για μεικτές γλώσσες. |
| **Very large PDFs (>500 pages)** | Η χρήση μνήμης αυξάνεται επειδή κάθε σελίδα φορτώνεται στη RAM. | Επεξεργαστείτε το PDF σε τμήματα χρησιμοποιώντας `engine.extract_from_pdf(pdf_path, start_page=1, end_page=100)` και επαναλάβετε. |
| **Poor scan quality** | Χαμηλό DPI ή πολύ θόρυβος μειώνει την εμπιστοσύνη. | Προ‑επεξεργαστείτε το PDF με `engine.image_preprocessing = True` ή αυξήστε το DPI μέσω `engine.dpi = 300`. |

> **Watch out:** Η ενεργοποίηση της προεπεξεργασίας εικόνας μπορεί να αυξήσει σημαντικά το χρόνο CPU. Αν εκτελείτε ένα νυχτερινό batch, προγραμματίστε αρκετό χρόνο ή ξεκινήστε έναν ξεχωριστό worker.

## Επαλήθευση του Αποτελέσματος

Μετά το τέλος του script, θα βρείτε μια δομή φακέλων όπως:

```
ocr_output/
├─ invoice_2023/
│  ├─ invoice_2023_page1.txt
│  ├─ invoice_2023_page2.txt
│  └─ …
└─ contract_A/
   ├─ contract_A_page1.txt
   └─ …
```

Ανοίξτε οποιοδήποτε αρχείο `.txt`; θα πρέπει να δείτε καθαρό κείμενο κωδικοποιημένο σε UTF‑8 που αντικατοπτρίζει το αρχικό σαρωμένο περιεχόμενο. Αν παρατηρήσετε παραμορφωμένους χαρακτήρες, ελέγξτε ξανά τις ρυθμίσεις γλώσσας του PDF και βεβαιωθείτε ότι τα σωστά πακέτα γραμματοσειρών είναι εγκατεστημένα στο μηχάνημα.

## Καθαρισμός Πόρων

Το Aspose OCR βασίζεται σε εγγενείς DLL, επομένως είναι απαραίτητο να καλέσετε `engine.dispose()` μόλις τελειώσετε. Η παράλειψη αυτού του βήματος μπορεί να οδηγήσει σε διαρροές μνήμης, ειδικά σε μακροχρόνιες batch εργασίες.

```python
# Always the last line of your script
engine.dispose()
```

## Πλήρες Παράδειγμα Από Αρχή έως Τέλος

Συνδυάζοντας όλα, εδώ είναι ένα μόνο

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}