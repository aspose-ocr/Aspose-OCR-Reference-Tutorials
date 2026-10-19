---
category: general
date: 2026-07-05
description: Εξαγωγή πίνακα από εικόνα χρησιμοποιώντας Python OCR. Μάθετε πώς να εξάγετε
  πίνακα, να μετατρέψετε την εικόνα σε TSV και να κυριαρχήσετε στις τεχνικές OCR πίνακα
  εικόνας με Python.
draft: false
keywords:
- extract table from image
- how to extract table
- convert image to tsv
- ocr table image python
language: el
og_description: Εξαγωγή πίνακα από εικόνα με Python OCR. Αυτός ο οδηγός δείχνει πώς
  να εξάγετε πίνακα, να μετατρέψετε την εικόνα σε TSV και να χρησιμοποιήσετε εργαλεία
  OCR πίνακα εικόνας Python.
og_title: Εξαγωγή Πίνακα από Εικόνα – Μετατροπή Εικόνας σε TSV με Python
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  headline: Extract Table from Image – Convert Image to TSV in Python
  type: TechArticle
- description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  name: Extract Table from Image – Convert Image to TSV in Python
  steps:
  - name: Initialise the aocr OCR engine.
    text: Initialise the aocr OCR engine.
  - name: Attach the AI post‑processor.
    text: Attach the AI post‑processor.
  - name: Load a table image.
    text: Load a table image.
  - name: Perform structured OCR.
    text: Perform structured OCR.
  - name: Clean the results.
    text: Clean the results.
  - name: Export the table as a TSV file.
    text: Export the table as a TSV file.
  type: HowTo
tags:
- OCR
- Python
- Table Extraction
title: Εξαγωγή Πίνακα από Εικόνα – Μετατροπή Εικόνας σε TSV με Python
url: /el/python/general/extract-table-from-image-convert-image-to-tsv-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Πίνακα από Εικόνα – Μετατροπή Εικόνας σε TSV με Python

Έχετε αναρωτηθεί ποτέ πώς να εξάγετε έναν πίνακα από μια εικόνα χωρίς να τρελαίνεστε; Σε αυτό το σεμινάριο θα περάσουμε βήμα‑βήμα από το **πώς να εξάγετε δεδομένα πίνακα** από μια εικόνα χρησιμοποιώντας τη βιβλιοθήκη `aocr`, και στη συνέχεια θα μετατρέψουμε αυτά τα δεδομένα σε ένα τακτοποιημένο αρχείο TSV. Δεν υπάρχει μαγεία, μόνο μερικές γραμμές Python και λίγη επεξεργασία με τεχνητή νοημοσύνη.

Αν έχετε ποτέ προσπαθήσει να αντιγράψετε‑επικολλήσετε έναν πίνακα από ένα σαρωμένο τιμολόγιο ή ένα στιγμιότυπο οθόνης και καταλήξατε με ένα ακατάστατο μίγμα, θα εκτιμήσετε γιατί μια προσέγγιση βασισμένη σε OCR αξίζει να την κυριαρχήσετε. Στο τέλος, θα μπορείτε να τροφοδοτήσετε οποιαδήποτε εικόνα πίνακα στο Python και να λαμβάνετε καθαρές, διαχωρισμένες με καρτέλα τιμές, έτοιμες για λογιστικά φύλλα ή βάσεις δεδομένων.

---

## Τι Θα Χρειαστείτε

Πριν προχωρήσουμε, βεβαιωθείτε ότι έχετε τα παρακάτω στη μηχανή σας:

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|------------------------|
| Python 3.9+ | Το πακέτο `aocr` στοχεύει σε σύγχρονες εκδόσεις του Python. |
| `aocr` library (`pip install aocr`) | Παρέχει τη μηχανή OCR και τον AI post‑processor που θα χρησιμοποιήσουμε. |
| Αρχείο εικόνας που περιέχει πίνακα (PNG, JPG, κ.λπ.) | Τα δεδομένα πηγής που θα εξάγουμε. |
| Προαιρετικά: ένα εικονικό περιβάλλον | Κρατά τις εξαρτήσεις απομονωμένες — συνιστάται έντονα. |

Η προετοιμασία αυτών των στοιχείων σας εξοικονομεί διακοπές στη μέση του οδηγού.

---

## Εγκατάσταση των Εξαρτήσεων

Πρώτα, ας εγκαταστήσουμε τα εργαλεία OCR. Ανοίξτε ένα τερματικό και τρέξτε:

```bash
# Create and activate a virtual environment (optional but clean)
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate

# Install the aocr package
pip install aocr
```

> **Pro tip:** Αν αντιμετωπίσετε σφάλματα δικαιωμάτων, προσθέστε `--user` στην εντολή `pip install` ή χρησιμοποιήστε `pipx` για παγκόσμια εγκατάσταση.

---

## Βήμα 1 – Αρχικοποίηση της Μηχανής OCR

Η μηχανή είναι η καρδιά της διαδικασίας. Σκεφτείτε την ως το «εγκέφαλο» που κοιτάζει κάθε pixel και αποφασίζει ποιος χαρακτήρας ανήκει πού.

```python
import aocr

# Create an OCR engine instance – this sets up the model and default settings
engine = aocr.OcrEngine()
```

Γιατί δημιουργούμε μια μηχανή αντί να καλέσουμε μια μοναδική συνάρτηση; Το αντικείμενο μηχανής μας επιτρέπει να προσθέσουμε προσαρμοσμένους post‑processors αργότερα, δίνοντάς μας λεπτομερή έλεγχο του αποτελέσματος — απαραίτητο όταν χρειάζεστε **ocr table image python** ακρίβεια.

---

## Βήμα 2 – Προσθήκη του AI Post‑Processor

`aocr` έρχεται με έναν ελαφρύ AI post‑processor που καθαρίζει τα ακατέργαστα αποτελέσματα OCR διατηρώντας τα όρια των κελιών. Δεν απαιτούνται επιπλέον ορίσματα, κάτι που κρατά τον κώδικα τακτοποιημένο.

```python
# Hook the AI post‑processor into the engine
engine.set_post_processor(ai.run_postprocessor, None)
```

Αν παραλείψετε αυτό το βήμα, θα λάβετε ακόμα ακατέργαστο κείμενο, αλλά η δομή του πίνακα θα είναι θορυβώδης — σκεφτείτε ένα λογιστικό φύλλο όπου κάθε κελί είναι αίνιγμα. Ο post‑processor κάνει το βαριά έργο της ευθυγράμμισης του κειμένου στο αρχικό πλέγμα.

---

## Βήμα 3 – Φόρτωση της Εικόνας του Πίνακα

Μπορείτε να φορτώσετε μια εικόνα από οποιοδήποτε μονοπάτι, αλλά για σαφήνεια θα αναφερθούμε σε έναν φάκελο placeholder. Αντικαταστήστε `"YOUR_DIRECTORY/invoice_table.png"` με το πραγματικό μονοπάτι του αρχείου σας.

```python
# Load the image that contains the table
image_path = "YOUR_DIRECTORY/invoice_table.png"
image = aocr.Image.from_file(image_path)
```

> **Note:** `aocr.Image` ανιχνεύει αυτόματα τη μορφή της εικόνας και κανονικοποιεί τα κανάλια χρώματος, οπότε δεν χρειάζεται να προεπεξεργαστείτε το αρχείο εκτός αν είναι σοβαρά κατεστραμμένο.

---

## Βήμα 4 – Εκτέλεση Structured OCR

Τώρα η μηχανή σαρώει την εικόνα και επιστρέφει ένα ακατέργαστο αντικείμενο πίνακα. Αυτό το αντικείμενο περιέχει γραμμές, στήλες και το ακατέργαστο κείμενο για κάθε κελί.

```python
# Recognise the table structure and extract raw cell data
raw_table = engine.recognize_structured(image)
```

Γιατί χρησιμοποιούμε το `recognize_structured` αντί για μια γενική κλήση `recognize`; Η δομημένη παραλλαγή προσπαθεί να ανιχνεύσει τα όρια γραμμών/στηλών, δίνοντάς σας ένα αποτέλεσμα τύπου πίνακα που είναι πολύ πιο εύκολο να μετατραπεί σε TSV αργότερα.

---

## Βήμα 5 – Καθαρισμός των Δεδομένων με τον AI Post‑Processor

Η εκτέλεση του post‑processor βελτιώνει το ακατέργαστο αποτέλεσμα: αφαιρεί τυχαίους χαρακτήρες, συγχωνεύει διασπασμένα τμήματα και εξασφαλίζει ότι το κείμενο κάθε κελιού είναι σωστά ευθυγραμμισμένο.

```python
# Apply the AI post‑processor to tidy up the table
processed_table = engine.run_postprocessor(raw_table)
```

Αν εξετάσετε το `processed_table.table`, θα δείτε μια λίστα γραμμών, όπου κάθε γραμμή είναι μια λίστα αντικειμένων `Cell`. Κάθε `Cell` έχει μια ιδιότητα `.text` που περιέχει το καθαρισμένο κείμενο.

---

## Βήμα 6 – Εξαγωγή του Πίνακα ως TSV

Το τελικό βήμα είναι να μετατρέψουμε τα επεξεργασμένα δεδομένα σε αρχείο τιμών διαχωρισμένων με καρτέλα (TSV) — ακριβώς ό,τι χρειάζεστε όταν θέλετε να **convert image to TSV** για Excel ή Google Sheets.

```python
import csv

# Define the output TSV path
tsv_path = "extracted_table.tsv"

# Open the file and write rows as tab‑separated values
with open(tsv_path, "w", newline="", encoding="utf-8") as tsv_file:
    writer = csv.writer(tsv_file, delimiter="\t")
    for row in processed_table.table:
        # Extract text from each cell and write the row
        writer.writerow([cell.text for cell in row])

print(f"✅ Table successfully saved to {tsv_path}")
```

Η εκτέλεση του script εκτυπώνει κάθε γραμμή στην κονσόλα (αν προτιμάτε) και γράφει ένα καθαρό αρχείο TSV που μπορείτε να ανοίξετε σε οποιοδήποτε πρόγραμμα λογιστικού φύλλου.

### Γρήγορη επαλήθευση

```python
# Print the TSV to the console for a sanity check
for row in processed_table.table:
    print("\t".join(cell.text for cell in row))
```

Θα πρέπει να δείτε ευθυγραμμισμένες στήλες, όπως:

```
Item	Qty	Price	Total
Apple	10	0.50	5.00
Banana	5	0.30	1.50
```

Αν το αποτέλεσμα φαίνεται ακατάστατο, ελέγξτε ξανά την ποιότητα της εικόνας (ευκρίνεια, αντίθεση) και σκεφτείτε να ρυθμίσετε τις παραμέτρους της μηχανής OCR — το `engine.set_config(...)` σας επιτρέπει να προσαρμόσετε μοντέλα γλώσσας και όρια εμπιστοσύνης.

---

## Διαχείριση Συνηθισμένων Περιπτώσεων

| Κατάσταση | Προτεινόμενη Διόρθωση |
|-----------|-----------------------|
| **Καμπυλωμένη εικόνα** | Προ-περιστροφή χρησιμοποιώντας `Pillow` (`Image.rotate`) πριν τη δώσετε στο `aocr`. |
| **Χαμηλή αντίθεση** | Εφαρμόστε εξίσωση ιστογράμματος (`cv2.equalizeHist`) για να βελτιώσετε την αναγνωσιμότητα. |
| **Συγχωνευμένα κελιά** | Μετά-επεξεργασία του TSV για διαχωρισμό των κελιών βάσει γνωστών οριοθετήσεων ή χρήση της επιλογής `merge_cells=False` αν είναι διαθέσιμη. |
| **PDF πολλαπλών σελίδων** | Μετατρέψτε κάθε σελίδα σε εικόνα πρώτα (`pdf2image`) και τρέξτε τη διαδικασία σε βρόχο. |

Αυτές οι προσαρμογές διατηρούν τη ροή εργασίας **ocr table image python** ανθεκτική σε διαφορετικό υλικό προέλευσης.

---

## Πλήρες Script – Ολοκληρωμένη Λύση

Παρακάτω βρίσκεται το πλήρες, έτοιμο προς εκτέλεση script που ενσωματώνει κάθε βήμα που συζητήθηκε. Αποθηκεύστε το ως `extract_table.py` και εκτελέστε `python extract_table.py`.

```python
#!/usr/bin/env python3
"""
Extract Table from Image – Convert Image to TSV (Python)

This script demonstrates how to:
1. Initialise the aocr OCR engine.
22. Attach the AI post‑processor.
3. Load a table image.
4. Perform structured OCR.
5. Clean the results.
6. Export the table as a TSV file.

Author: Your Name
Date: 2026-07-05
"""

import aocr
import csv
import sys
from pathlib import Path

def main(image_path: str, output_tsv: str = "extracted_table.tsv"):
    # Step 1 – Initialise engine
    engine = aocr.OcrEngine()

    # Step 2 – Attach AI post‑processor
    engine.set_post_processor(ai.run_postprocessor, None)

    # Step 3 – Load image
    if not Path(image_path).is_file():
        sys.exit(f"❌ Image not found: {image_path}")
    image = aocr.Image.from_file(image_path)

    # Step 4 – Structured OCR
    raw_table = engine.recognize_structured(image)

    # Step 5 – Clean with post‑processor
    processed_table = engine.run_postprocessor(raw_table)

    # Step 6 – Write TSV
    with open(output_tsv, "w", newline="", encoding="utf-8") as tsv_file:
        writer = csv.writer(tsv_file, delimiter="\


## Τι Θα Μάθετε Στη Σειρά;

Οι παρακάτω οδηγίες καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Βήμα‑βήμα](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Πώς να εξάγετε πίνακα από εικόνα χρησιμοποιώντας Aspose.OCR για .NET](/ocr/english/net/text-recognition/recognize-table/)
- [Πώς να Εξάγετε Κείμενο από Εικόνα Προετοιμάζοντας Ορθογώνια στο OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}