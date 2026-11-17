---
category: general
date: 2026-03-26
description: Εξάγετε πίνακες από εικόνα και μετατρέψτε την εικόνα σε λογιστικό φύλλο
  χρησιμοποιώντας Python OCR. Μάθετε πώς να φορτώνετε εικόνα για OCR, να διαβάζετε
  πίνακες και να εξάγετε τα δεδομένα των πινάκων.
draft: false
keywords:
- extract tables from image
- convert image to spreadsheet
- load image for ocr
- ocr read tables
- ocr extract table data
language: el
og_description: Εξαγωγή πινάκων από εικόνα με Python OCR. Αυτός ο οδηγός δείχνει πώς
  να φορτώσετε την εικόνα για OCR, να διαβάσετε τους πίνακες και να τους μετατρέψετε
  σε λογιστικό φύλλο.
og_title: Εξαγωγή Πινάκων από Εικόνα – Πλήρες Μάθημα OCR
tags:
- OCR
- Python
- Data Extraction
title: Εξαγωγή πινάκων από εικόνα – Οδηγός OCR βήμα‑βήμα
url: /el/python-java/general/extract-tables-from-image-step-by-step-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Πινάκων από Εικόνα – Πλήρες Μάθημα OCR

Έχετε χρειαστεί ποτέ να **extract tables from image** αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν δυσκολίες όταν ένα PDF ή ένα στιγμιότυπο οθόνης περιέχει δεδομένα σε μορφή πίνακα που πρέπει να μετατραπούν σε επεξεργάσιμες γραμμές και στήλες. Τα καλά νέα; Μερικές γραμμές κώδικα Python, σε συνδυασμό με μια αξιόπιστη μηχανή OCR, μπορούν να μετατρέψουν αυτήν την εικόνα σε ένα χρήσιμο υπολογιστικό φύλλο σε δευτερόλεπτα.

Σε αυτό το μάθημα θα περάσουμε από τη φόρτωση μιας εικόνας για OCR, την εκτέλεση της μηχανής αναγνώρισης και την εξαγωγή κάθε πίνακα γραμμή‑με‑γραμμή. Στο τέλος θα μπορείτε να **convert image to spreadsheet**, και θα δείτε επίσης πώς να **ocr read tables** και **ocr extract table data** για επεξεργασία downstream. Χωρίς κρυφή μαγεία, μόνο σαφής, εκτελέσιμος κώδικας που μπορείτε να ενσωματώσετε στο πρότζεκτ σας σήμερα.

---

## What You’ll Need

Πριν βουτήξουμε, βεβαιωθείτε ότι έχετε τα εξής:

- **Python 3.9+** – η πιο πρόσφατη σταθερή έκδοση λειτουργεί καλύτερα.  
- Η βιβλιοθήκη **`ocr`** (ή οποιοδήποτε συμβατό OCR SDK που εκθέτει `OcrEngine`, `Image` και μεθόδους σχετικές με πίνακες). Εγκαταστήστε την με `pip install ocr‑sdk` (αντικαταστήστε με το πραγματικό όνομα πακέτου).  
- Ένα αρχείο εικόνας (`.png`, `.jpg`, κ.λπ.) που περιέχει έναν καθαρά τυπωμένο πίνακα.  
- Προαιρετικά: **pandas** αν θέλετε να γράψετε τα εξαγόμενα δεδομένα απευθείας σε αρχείο CSV ή Excel (`pip install pandas`).

Τα έχετε όλα; Τέλεια—ας ξεκινήσουμε.

---

## Step 1: Import the OCR SDK and Prepare Your Environment

Πρώτα απ’ όλα: πρέπει να εισάγουμε τις κλάσεις OCR στο script μας και να δημιουργήσουμε έναν μικρό βοηθό που αργότερα θα μετατρέπει τα ακατέργαστα δεδομένα του πίνακα σε DataFrame.

```python
# Step 1 – Imports and basic setup
import ocr                     # The OCR SDK
from pathlib import Path      # Handy for file paths
import pandas as pd           # For converting tables to spreadsheets

# Optional: configure logging to see what the engine is doing
import logging
logging.basicConfig(level=logging.INFO)
```

**Why this matters:** Η εισαγωγή του `ocr` μας δίνει πρόσβαση στα `OcrEngine`, `Imaging.Image` και στα αντικείμενα πίνακα που θα διατρέχουμε. Το `pandas` δεν είναι απαραίτητο για την εξαγωγή, αλλά κάνει το κομμάτι **convert image to spreadsheet** τελείως απλό.

---

## Step 2: Load the Image You Want to Process

Τώρα φορτώνουμε πραγματικά την **image for OCR**. Το SDK αναμένει ένα αντικείμενο `Image`, γι’ αυτό θα τυλίξουμε τη διαδρομή του αρχείου με τη βοηθητική μέθοδο `Image.load()`.

```python
# Step 2 – Load the image that contains a table
image_path = Path("YOUR_DIRECTORY/table_image.png")

# Verify the file exists early to avoid cryptic SDK errors
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Attach the image to the engine
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))
```

**Pro tip:** Κρατήστε τα αρχεία εικόνας σε έναν αφιερωμένο φάκελο (`assets/` ή `data/`) και χρησιμοποιήστε σχετικές διαδρομές. Έτσι το script παραμένει φορητό μεταξύ διαφορετικών μηχανών.

---

## Step 3: Run the Recognition Process

Με την εικόνα συνδεδεμένη, μπορούμε τελικά να πούμε στη μηχανή να **ocr read tables**. Η κλήση `recognize()` επιστρέφει ένα αντικείμενο αποτελέσματος που περιέχει ό,τι ανακάλυψε η μηχανή—μπλοκ κειμένου, γραμμές και, το πιο σημαντικό για εμάς, πίνακες.

```python
# Step 3 – Perform OCR and obtain results
ocr_result = ocr_engine.recognize()

# Quick sanity check: did the engine find any tables?
if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
else:
    logging.info(f"Found {len(ocr_result.get_tables())} table(s).")
```

**Why we check:** Κάποιες εικόνες μπορεί να είναι θορυβώδεις ή τα όρια του πίνακα αχνά, με αποτέλεσμα η μηχανή να τα χάσει. Η καταγραφή μιας προειδοποίησης σας δίνει άμεση ανάδραση χωρίς να διακόπτει το script.

---

## Step 4: Extract Each Table’s Rows and Cells

Εδώ συμβαίνει η πραγματική μαγεία. Θα διατρέξουμε κάθε ανιχνευμένο πίνακα, θα εξάγουμε κάθε γραμμή και, στη συνέχεια, το κείμενο κάθε κελιού. Η εσωτερική list comprehension κάνει τον κώδικα σύντομο, αλλά θα εξηγήσουμε τη ροή.

```python
# Step 4 – Iterate over detected tables and collect data
all_tables = []   # Will hold a list of pandas DataFrames

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")

    rows_data = []   # Temporary storage for this table's rows

    for row_obj in table_obj.get_rows():
        # Extract text from each cell in the current row
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    # Convert the raw list of rows into a DataFrame
    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    # Print a human‑readable version to the console
    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))
```

**What’s going on?**  

- `enumerate(..., start=1)` παρέχει έναν φιλικό αριθμό πίνακα για το logging.  
- `row_obj.get_cells()` επιστρέφει κάθε αντικείμενο κελιού· `cell.get_text()` παίρνει τη συμβολοσειρά που αποκωδικοποίησε το OCR.  
- Αποθηκεύουμε τις γραμμές στο `rows_data`, έπειτα τις περνάμε στο `pandas.DataFrame` που ευθυγραμμίζει αυτόματα τις στήλες.  
- Το τμήμα `print` αντικατοπτρίζει το **essential output** του αρχικού αποσπάσματος, ώστε να μπορείτε να επαληθεύσετε τα αποτελέσματα αμέσως.

**Edge case handling:** Αν μια γραμμή έχει διαφορετικό αριθμό κελιών από τις άλλες, το `pandas` θα γεμίσει τα κενά με `NaN`. Μπορείτε αργότερα να καθαρίσετε το DataFrame με `df.fillna('')` αν προτιμάτε κενές συμβολοσειρές.

---

## Step 5: Save the Extracted Tables to a Spreadsheet

Τώρα που έχουμε μια λίστα DataFrames, η μετατροπή τους σε βιβλίο Excel (ή CSV) είναι παιχνιδάκι. Αυτό ικανοποιεί τον στόχο **convert image to spreadsheet**.

```python
# Step 5 – Export tables to Excel (one sheet per table)
output_path = Path("extracted_tables.xlsx")
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        sheet_name = f"Table_{idx}"
        df.to_excel(writer, sheet_name=sheet_name, index=False)

logging.info(f"All tables saved to {output_path}")
```

**Why Excel?** Οι περισσότεροι επαγγελματίες προτιμούν `.xlsx`. Αν προτιμάτε CSV, αντικαταστήστε το βρόχο με `df.to_csv(f"table_{idx}.csv", index=False)`.

---

## Full, Ready‑to‑Run Script

Συνδυάζοντας τα παραπάνω, εδώ είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε για εκτέλεση.

```python
import ocr
from pathlib import Path
import pandas as pd
import logging

logging.basicConfig(level=logging.INFO)

# ---------- Configuration ----------
image_path = Path("YOUR_DIRECTORY/table_image.png")
output_path = Path("extracted_tables.xlsx")
# ----------------------------------

# Verify image exists
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Initialize OCR engine
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))

# Run recognition
ocr_result = ocr_engine.recognize()

if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
    exit(0)

all_tables = []

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")
    rows_data = []

    for row_obj in table_obj.get_rows():
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))

# Save to Excel
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        df.to_excel(writer, sheet_name=f"Table_{idx}", index=False)

logging.info(f"All tables saved to {output_path}")
```

**Expected console output** (assuming a simple 2×3 table):

```
=== New Table ===
Header1    Header2    Header3
Row1Col1   Row1Col2   Row1Col3
Row2Col1   Row2Col2   Row2Col3
```

Και θα βρείτε το `extracted_tables.xlsx` στον φάκελο του script, με κάθε πίνακα σε ξεχωριστό φύλλο.

---

## Frequently Asked Questions & Tips

| Question | Answer |
|----------|--------|
| **Can I use a different OCR library?** | Absolutely. The pattern stays the same: load image → recognize → iterate over `get_tables()`. Just replace the import and object names. |
| **What if my image is noisy?** | Pre‑process with OpenCV (thresholding, deskew) before feeding it to the OCR engine. Noise reduction often improves **ocr extract table data** accuracy. |
| **Do I need to install `openpyxl`?** | Yes, `pandas` uses it under the hood for Excel output. Install with `pip install openpyxl`. |
| **How do I handle merged cells?** | Some SDKs expose `cell.is_merged()`; you can detect and propagate the value across the merged range manually. |
| **Is there a way to extract only specific tables?** | Filter by `table_obj.get_confidence()` or by checking header keywords before processing. |

---

## Wrapping Up

Τώρα έχετε μια πλήρη, end‑to‑end λύση για **extract tables from image**, μετατρέποντας το αποτέλεσμα σε τακτικό υπολογιστικό φύλλο, και ακόμη διαχειρίζεστε πολλαπλούς πίνακες σε μία εικόνα. Το script δείχνει πώς να **load image for OCR**, **ocr read tables**, και **ocr extract table data** παραμένοντας ευέλικτο για πραγματικές συνθήκες.

Τι θα κάνετε μετά; Δοκιμάστε να τροφοδοτήσετε τη μηχανή OCR με μια σελίδα PDF που έχει μετατραπεί σε εικόνα, ή πειραματιστείτε με διαφορετικές γλώσσες και γραμματοσειρές. Μπορείτε επίσης να στέλνετε τα DataFrames κατευθείαν σε μια βάση δεδομένων ή σε εργαλείο αναφορών—η φαντασία σας είναι το όριο.

Αν βρήκατε αυτόν τον οδηγό χρήσιμο, μοιραστείτε τον, δώστε αστέρι στο αποθετήριο που φιλοξενεί το SDK, ή αφήστε ένα σχόλιο με τις δικές σας συμβουλές. Καλό coding, και εύχομαι οι πίνακές σας να είναι πάντα τέλεια αναγνωρισμένοι!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}