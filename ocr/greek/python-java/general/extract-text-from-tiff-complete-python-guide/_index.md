---
category: general
date: 2026-03-28
description: Εξάγετε κείμενο από αρχεία TIFF χρησιμοποιώντας το Aspose OCR σε Python.
  Μάθετε πώς να μετατρέπετε TIFF σε κείμενο γρήγορα και αξιόπιστα.
draft: false
keywords:
- extract text from tiff
- convert tiff to text
language: el
og_description: Εξάγετε κείμενο από αρχεία TIFF χρησιμοποιώντας το Aspose OCR σε Python.
  Αυτός ο οδηγός δείχνει πώς να μετατρέψετε το TIFF σε κείμενο βήμα‑βήμα.
og_title: Εξαγωγή κειμένου από TIFF – Πλήρης οδηγός Python
tags:
- OCR
- Python
- Aspose
title: Εξαγωγή κειμένου από TIFF – Πλήρης οδηγός Python
url: /el/python-java/general/extract-text-from-tiff-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από TIFF – Πλήρης Οδηγός Python

Χρειάζεστε **εξαγωγή κειμένου από TIFF** εικόνες στο Python project σας; Αυτός ο οδηγός σας δείχνει πώς να **μετατρέψετε TIFF σε κείμενο** χρησιμοποιώντας τη βιβλιοθήκη Aspose OCR, και το κάνει με τρόπο που μπορεί να ακολουθήσει ακόμη και ένας αρχάριος.

Αν έχετε ποτέ κοίταξει ένα multi‑page TIFF και αναρωτηθείτε πώς να εξάγετε τις λέξεις χωρίς να τις πληκτρολογήσετε χειροκίνητα, βρίσκεστε στο σωστό μέρος. Θα περάσουμε από όλη τη διαδικασία — από την εγκατάσταση του πακέτου μέχρι τη διαχείριση ειδικών περιπτώσεων όπως κρυπτογραφημένα αρχεία — ώστε να μπορείτε να εστιάσετε στην ανάπτυξη των λειτουργιών που έχουν σημασία.

## Τι Θα Μάθετε

Σε αυτό το tutorial θα ανακαλύψετε:

* Πώς να ρυθμίσετε το Aspose OCR για Python.
* Τον ακριβή κώδικα που χρειάζεται για να διαβάσετε κάθε σελίδα ενός multi‑page TIFF.
* Τρόπους για να αντιμετωπίσετε κοινά προβλήματα όπως ελλιπείς γραμματοσειρές ή κατεστραμμένες σελίδες.
* Συμβουλές για βελτίωση της ακρίβειας και της απόδοσης όταν **εξάγετε κείμενο από TIFF** αρχεία σε μεγάλη κλίμακα.

Στο τέλος, θα έχετε ένα έτοιμο‑για‑εκτέλεση script που μετατρέπει οποιοδήποτε TIFF σε απλό κείμενο, έτοιμο για ευρετηρίαση, αναζήτηση ή ενσωμάτωση σε downstream pipelines NLP.

### Προαπαιτούμενα

* Python 3.8 ή νεότερο (η βιβλιοθήκη υποστηρίζει 3.7+).
* Ένα έγκυρο license Aspose OCR — ή μπορείτε να ξεκινήσετε με τη δωρεάν δοκιμή (ο κώδικας λειτουργεί σε λειτουργία αξιολόγησης, μόνο με υδατογράφημα στην έξοδο).
* Βασική εξοικείωση με τα virtual environments του Python (προαιρετικό αλλά συνιστάται).

---

## Βήμα 1 – Εγκατάσταση του Πακέτου Aspose OCR

Πρώτα απ' όλα: χρειάζεστε το πακέτο `aspose-ocr`. Φιλοξενείται στο PyPI, έτσι μια απλή εντολή `pip` install κάνει τη δουλειά.

```bash
pip install aspose-ocr
```

> **Pro tip:** Χρησιμοποιήστε ένα virtual environment (`python -m venv venv`) για να διατηρήσετε τις εξαρτήσεις απομονωμένες. Αποτρέπει συγκρούσεις εκδόσεων με άλλα έργα που μπορεί να διαχειρίζεστε.

> **Why this matters:** Η εγκατάσταση του πακέτου φέρνει τα εγγενή binaries της μηχανής OCR που πραγματικά εκτελούν τη βαριά δουλειά. Χωρίς αυτά, η μέθοδος `recognize_from_tiff` δεν θα υπάρχει, και θα αντιμετωπίσετε ένα `ImportError`.

## Βήμα 2 – Εισαγωγή της Βιβλιοθήκης και Δημιουργία OCR Engine

Τώρα που η βιβλιοθήκη είναι στον υπολογιστή σας, εισάγετέ την και δημιουργήστε ένα `OcrEngine`. Αυτό το αντικείμενο είναι το εργαλείο που θα επεξεργαστεί τα δεδομένα της εικόνας.

```python
# Step 2: Import the Aspose OCR library and create an engine instance
import aspose.ocr as aocr

# Initialize the OCR engine – you can optionally pass a license file here
ocr_engine = aocr.OcrEngine()
```

*Η κλάση `OcrEngine` περιλαμβάνει όλες τις ρυθμίσεις OCR, όπως γλώσσα, ανάλυση και επιλογές προεπεξεργασίας. Θα ρυθμίσουμε μερικές από αυτές αργότερα για να αυξήσουμε την ακρίβεια.*

## Βήμα 3 – Δείξτε στο Multi‑Page TIFF Αρχείο Σας

Χρειάζεστε μια διαδρομή προς το TIFF που θέλετε να διαβάσετε. Η βιβλιοθήκη λειτουργεί με απόλυτες ή σχετικές διαδρομές, αλλά οι απόλυτες διαδρομές αποφεύγουν εκπλήξεις όταν το script εκτελείται από διαφορετικό φάκελο εργασίας.

```python
# Step 3: Define the path to the TIFF file
tiff_file_path = "YOUR_DIRECTORY/input.tif"
```

> **Common mistake:** Ξεχάνοντας να διαφύγετε τις ανάστροφες κάθετες (backslashes) στα Windows (`C:\\Images\\file.tif`). Η χρήση raw strings (`r\"C:\\Images\\file.tif\"`) ή μπροστινών καθέτων (forward slashes) αποφεύγει αυτό το πρόβλημα.

## Βήμα 4 – Αναγνώριση Κειμένου από Όλες τις Σελίδες

Αυτή είναι η καρδιά του tutorial: η κλήση του `recognize_from_tiff`. Η μέθοδος επιστρέφει μια λίστα από αντικείμενα `OcrResult` — ένα για κάθε σελίδα — ώστε να μπορείτε να τα επεξεργαστείτε ξεχωριστά.

```python
# Step 4: Extract text from every page of the TIFF
ocr_pages = ocr_engine.recognize_from_tiff(tiff_file_path)

# Verify we got results
if not ocr_pages:
    raise RuntimeError("No pages were recognized. Check the file path and format.")
```

**Why this works:** Το Aspose OCR εσωτερικά χωρίζει το TIFF στα επιμέρους πλαίσια του, τρέχει τη μηχανή OCR σε κάθε ένα, και ομαδοποιεί τα αποτελέσματα. Αυτό είναι πολύ πιο αξιόπιστο από το να προσπαθήσετε να διαχωρίσετε τις σελίδες χειροκίνητα με Pillow ή ImageMagick.

## Βήμα 5 – Επανάληψη στα Αποτελέσματα και Εξαγωγή του Κειμένου

Τέλος, επαναλάβετε τη λίστα `OcrResult` και εκτυπώστε (ή αποθηκεύστε) το εξαγόμενο κείμενο. Μπορείτε επίσης να γράψετε κάθε σελίδα σε ξεχωριστό αρχείο `.txt` αν αυτό ταιριάζει στη ροή εργασίας σας.

```python
# Step 5: Print or save the extracted text
for page_index, page_result in enumerate(ocr_pages):
    print(f"--- TIFF Page {page_index + 1} ---")
    print(page_result.text)
    # Optional: write each page to a separate file
    with open(f"page_{page_index + 1}.txt", "w", encoding="utf-8") as f:
        f.write(page_result.text)
```

**Αναμενόμενη έξοδος** (truncated for brevity):

```
--- TIFF Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
--- TIFF Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore...
```

> **Edge case handling:** Αν μια σελίδα δεν περιέχει αναγνωρίσιμο κείμενο, το `page_result.text` θα είναι μια κενή συμβολοσειρά. Ίσως θέλετε να καταγράψετε αυτές τις σελίδες για μετέπειτα χειροκίνητη ανασκόπηση.

## Bonus – Ρύθμιση Ρυθμίσεων OCR για Καλύτερη Ακρίβεια

Μερικές φορές η προεπιλεγμένη διαμόρφωση δεν είναι επαρκής, ειδικά με σαρώσεις χαμηλής ανάλυσης ή ασυνήθιστες γραμματοσειρές. Παρακάτω είναι μερικές ρυθμίσεις που μπορείτε να προσαρμόσετε:

```python
# Set language (default is English)
ocr_engine.language = aocr.Language.English

# Increase image resolution before OCR (helps with blurry scans)
ocr_engine.image_preprocessing = aocr.ImagePreprocessingOptions(
    sharpen=True,
    contrast=1.2
)

# Enable deskew to straighten rotated pages
ocr_engine.deskew = True
```

*Αυτές οι επιλογές είναι προαιρετικές, αλλά συχνά κάνουν τη διαφορά μεταξύ ενός ακατάστατου αποτελέσματος και ενός καθαρού, αναζητήσιμου αποσπάσματος.*

## Συχνά Προβλήματα & Πώς να τα Αποφύγετε

| Συμπτωμα | Πιθανή Αιτία | Διόρθωση |
|----------|--------------|----------|
| Κενή έξοδος για όλες τις σελίδες | Λάθος διαδρομή αρχείου ή μη υποστηριζόμενη συμπίεση TIFF | Επαληθεύστε τη διαδρομή, βεβαιωθείτε ότι το TIFF χρησιμοποιεί υποστηριζόμενη συμπίεση (π.χ., LZW, PackBits). |
| Παραμορφωμένοι χαρακτήρες (π.χ., �) | Λανθασμένη ρύθμιση γλώσσας ή ελλιπείς γραμματοσειρές | Ορίστε `ocr_engine.language` στη σωστή τοπική ρύθμιση· εγκαταστήστε τις απαιτούμενες γραμματοσειρές στο λειτουργικό σύστημα. |
| Αργή επεξεργασία σε μεγάλα TIFF | Προεπιλεγμένη λειτουργία μονονηματική | Χρησιμοποιήστε `ocr_engine.recognize_from_tiff(..., parallel=True)` εάν η έκδοση της βιβλιοθήκης το υποστηρίζει. |
| Προειδοποίηση άδειας | Χρήση της δοκιμής χωρίς αρχείο άδειας | Παρέχετε κλειδί άδειας μέσω `aocr.License().set_license("Aspose.OCR.lic")`. |

## Πλήρες Script – Έτοιμο για Εκτέλεση

Παρακάτω είναι το πλήρες, αυτόνομο script που ενσωματώνει όλα τα βήματα και τις προαιρετικές ρυθμίσεις που συζητήθηκαν παραπάνω. Αντιγράψτε‑και‑επικολλήστε το σε ένα αρχείο με όνομα `extract_tiff_text.py` και τρέξτε `python extract_tiff_text.py`.

```python
#!/usr/bin/env python3
"""
extract_tiff_text.py

A complete example that extracts text from a multi‑page TIFF using Aspose OCR.
It demonstrates how to:
- Install and import the library
- Initialize the OCR engine
- Configure optional preprocessing
- Iterate over each page and save the results

Author: Your Name
Date: 2026‑03‑28
"""

import aspose.ocr as aocr
import os
import sys

def main(tiff_path: str, output_dir: str = "output"):
    # Ensure output directory exists
    os.makedirs(output_dir, exist_ok=True)

    # Initialize the OCR engine
    ocr_engine = aocr.OcrEngine()

    # Optional: fine‑tune OCR settings for better accuracy
    ocr_engine.language = aocr.Language.English
    ocr_engine.image_preprocessing = aocr.ImagePreprocessingOptions(
        sharpen=True,
        contrast=1.2
    )
    ocr_engine.deskew = True

    # Perform OCR on the TIFF
    try:
        ocr_pages = ocr_engine.recognize_from_tiff(tiff_path)
    except Exception as e:
        sys.exit(f"Failed to process {tiff_path}: {e}")

    if not ocr_pages:
        sys.exit("No pages were recognized. Check the file path and format.")

    # Iterate over results
    for idx, result in enumerate(ocr_pages, start=1):
        page_text = result.text or "[No recognizable text]"
        print(f"--- TIFF Page {idx} ---")
        print(page_text[:200] + ("..." if len(page_text) > 200 else ""))  # preview

        # Save each page's text
        out_file = os.path.join(output_dir, f"page_{idx}.txt")
        with open(out_file, "w", encoding="utf-8") as f:
            f.write(page_text)

    print(f"\nAll pages processed. Text files saved in '{output_dir}'.")

if __name__ == "__main__":
    if len(sys.argv) < 2:
        sys.exit("Usage: python extract_tiff_text.py <path_to_tiff>")
    tiff_file = sys.argv[1]
    main(tiff_file)
```

**Εκτέλεση του script**

```bash
python extract_tiff_text.py /path/to/your/input.tif
```

Θα δείτε μια προεπισκόπηση στην κονσόλα για κάθε σελίδα και έναν φάκελο με όνομα `output` που περιέχει `page_1.txt`, `page_2.txt`, κ.λπ.

## Συμπέρασμα

Μόλις καλύψαμε όλα όσα χρειάζεστε για **εξαγωγή κειμένου από TIFF** αρχεία χρησιμοποιώντας Python και Aspose OCR. Από την εγκατάσταση του πακέτου μέχρι τη διαχείριση multi‑page εγγράφων, τη ρύθμιση παραμέτρων για ακρίβεια και την αποθήκευση των αποτελεσμάτων, ολόκληρη η ροή εργασίας είναι τώρα στα χέρια σας.

Αν θέλετε να **μετατρέψετε TIFF σε κείμενο** σε παραγωγική pipeline, σκεφτείτε την ομαδοποίηση αρχείων, την παράλληλη εκτέλεση κλήσεων OCR, και την αποθήκευση της εξόδου σε ευρετήριο αναζήτησης όπως το Elasticsearch. Για τους τολμηρούς, πειραματιστείτε με άλλες γλώσσες (`aocr.Language.Spanish`) ή τροφοδοτήστε τα ακατέργαστα αποτελέσματα OCR σε βιβλιοθήκη ελέγχου ορθογραφίας για να καθαρίσετε το θόρυβο OCR.

Έχετε ερωτήσεις σχετικά με την κλιμάκωση, τις άδειες ή την ενσωμάτωση με αποθήκευση στο cloud; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

![Διάγραμμα που δείχνει τη ροή OCR από αρχείο TIFF σε εξαγόμενο κείμενο](https://example.com/placeholder-image.png "Εξαγωγή κειμένου από TIFF χρησιμοποιώντας Python")

*Κείμενο alt εικόνας: Εξαγωγή κειμένου από TIFF χρησιμοποιώντας Python*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}