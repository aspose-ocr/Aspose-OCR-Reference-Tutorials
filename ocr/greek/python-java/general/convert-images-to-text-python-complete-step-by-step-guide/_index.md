---
category: general
date: 2026-05-31
description: Μάθετε πώς να μετατρέπετε εικόνες σε κείμενο με Python χρησιμοποιώντας
  ένα script μαζικής μετατροπής εικόνων σε κείμενο. Αναγνωρίστε κείμενο από σαρωμένες
  εικόνες με το Aspose.OCR σε λίγα λεπτά.
draft: false
keywords:
- convert images to text python
- bulk image to text conversion
- recognize text from scanned images
language: el
og_description: Μετατρέψτε εικόνες σε κείμενο με Python άμεσα. Αυτός ο οδηγός δείχνει
  τη μαζική μετατροπή εικόνων σε κείμενο και πώς να αναγνωρίζετε κείμενο από σαρωμένες
  εικόνες με το Aspose.OCR.
og_title: Μετατροπή Εικόνων σε Κείμενο με Python – Πλήρης Οδηγός
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to convert images to text python with a bulk image to text
    conversion script. Recognize text from scanned images using Aspose.OCR in minutes.
  headline: Convert Images to Text Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to convert images to text python with a bulk image to text
    conversion script. Recognize text from scanned images using Aspose.OCR in minutes.
  name: Convert Images to Text Python – Complete Step‑by‑Step Guide
  steps:
  - name: Imports the OCR engine classes.
    text: Imports the OCR engine classes.
  - name: Instantiates a `BatchOcrEngine`.
    text: Instantiates a `BatchOcrEngine`.
  - name: Points the engine at an input folder of images.
    text: Points the engine at an input folder of images.
  - name: Directs the engine to write each extracted text file into an output folder.
    text: Directs the engine to write each extracted text file into an output folder.
  - name: Fires the `recognize()` method, which **recognize text from scanned images**
      one by one.
    text: Fires the `recognize()` method, which **recognize text from scanned images**
      one by one.
  type: HowTo
tags:
- OCR
- Python
- Aspose
title: Μετατροπή Εικόνων σε Κείμενο με Python – Πλήρης Οδηγός Βήμα‑βήμα
url: /el/python-java/general/convert-images-to-text-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή Εικόνων σε Κείμενο με Python – Πλήρης Οδηγός Βήμα‑βήμα

Έχετε αναρωτηθεί ποτέ πώς να **convert images to text python** χωρίς να ψάχνετε σε δεκάδες βιβλιοθήκες; Δεν είστε οι μόνοι. Είτε ψηφιοποιείτε παλιές αποδείξεις, εξάγετε δεδομένα από σαρωμένα τιμολόγια, είτε δημιουργείτε ένα ευρετήριο PDF με δυνατότητα αναζήτησης, η μετατροπή εικόνων σε απλά αρχεία κειμένου είναι καθημερινή εργασία για πολλούς προγραμματιστές.

Σε αυτό το tutorial θα περάσουμε από μια **bulk image to text conversion** pipeline που αναγνωρίζει κείμενο από σαρωμένες εικόνες, αποθηκεύει κάθε αποτέλεσμα ως ξεχωριστό αρχείο `.txt`, και το κάνει όλο με μερικές μόνο γραμμές Python. Χωρίς να ψάχνετε για σπάνιες APIs—το Aspose.OCR κάνει το σκληρό κομμάτι, και θα σας δείξουμε ακριβώς πώς να το ενσωματώσετε.

## Τι Θα Μάθετε

- Πώς να εγκαταστήσετε και να ρυθμίσετε το πακέτο Aspose.OCR for Python.  
- Τον ακριβή κώδικα που απαιτείται για **convert images to text python** χρησιμοποιώντας το `BatchOcrEngine`.  
- Συμβουλές για την αντιμετώπιση κοινών προβλημάτων όπως μη υποστηριζόμενες μορφές ή κατεστραμμένα αρχεία.  
- Τρόπους επαλήθευσης ότι το βήμα **recognize text from scanned images** ολοκληρώθηκε επιτυχώς.  

Στο τέλος αυτού του οδηγού θα έχετε ένα έτοιμο‑να‑τρέξει script που μπορεί να επεξεργαστεί χιλιάδες εικόνες σε μία φορά—ιδανικό για οποιοδήποτε σενάριο επεξεργασίας παρτίδας.

## Προαπαιτούμενα

- Python 3.8+ εγκατεστημένο στο σύστημά σας.  
- Ένας φάκελος με αρχεία εικόνας (PNG, JPEG, TIFF, κ.λπ.) που θέλετε να μετατρέψετε σε κείμενο.  
- Ένας ενεργός λογαριασμός Aspose Cloud ή μια δωρεάν δοκιμαστική άδεια (το δωρεάν επίπεδο αρκεί για δοκιμές).  

Αν έχετε όλα αυτά, ας βουτήξουμε.

---

## Step 1 – Set Up Your Python Environment

Πριν αρχίσουμε να γράφουμε κώδικα OCR, βεβαιωθείτε ότι εργάζεστε μέσα σε ένα καθαρό virtual environment. Αυτό απομονώνει τις εξαρτήσεις και αποτρέπει συγκρούσεις εκδόσεων.

```bash
# Create a new virtual environment named venv
python -m venv venv

# Activate the environment (Windows)
venv\Scripts\activate

# Activate the environment (macOS / Linux)
source venv/bin/activate
```

> **Pro tip:** Κρατήστε τον φάκελο του έργου σας τακτοποιημένο—δημιουργήστε ένα υποφάκελο που ονομάζεται `ocr_project` και τοποθετήστε το script εκεί. Έτσι η διαχείριση διαδρομών γίνεται παιχνιδάκι αργότερα.

## Step 2 – Install Aspose.OCR for Python

Το Aspose.OCR είναι εμπορική βιβλιοθήκη, αλλά διανέμεται με ένα δωρεάν wheel τύπου NuGet που μπορείτε να κατεβάσετε από το PyPI. Εκτελέστε την παρακάτω εντολή μέσα στο ενεργοποιημένο virtual environment:

```bash
pip install aspose-ocr
```

Αν αντιμετωπίσετε σφάλμα δικαιωμάτων, προσθέστε τη σημαία `--user` ή τρέξτε την εντολή με `sudo` (μόνο Linux/macOS). Μετά την εγκατάσταση θα πρέπει να δείτε κάτι σαν:

```
Successfully installed aspose-ocr-23.9.0
```

> **Why Aspose?** Σε αντίθεση με πολλά ανοιχτού κώδικα OCR εργαλεία, το Aspose.OCR υποστηρίζει **bulk image to text conversion** έτοιμο από την αρχή και διαχειρίζεται ένα ευρύ φάσμα μορφών εικόνας χωρίς επιπλέον ρυθμίσεις. Επιπλέον προσφέρει την κλάση `BatchOcrEngine` που κάνει το έργο **convert images to text python** μια εντολή‑μια‑γραμμή.

## Step 3 – Convert Images to Text Python with Batch OCR

Τώρα για την καρδιά του tutorial. Παρακάτω υπάρχει ένα πλήρως εκτελέσιμο script που:

1. Εισάγει τις κλάσεις του OCR engine.  
2. Δημιουργεί ένα αντικείμενο `BatchOcrEngine`.  
3. Κατευθύνει το engine σε έναν φάκελο εισόδου με εικόνες.  
4. Οδηγεί το engine να γράψει κάθε εξαγόμενο αρχείο κειμένου σε έναν φάκελο εξόδου.  
5. Εκκινεί τη μέθοδο `recognize()`, η οποία **recognize text from scanned images** μία-μία.  

Αποθηκεύστε το παρακάτω ως `batch_ocr.py` μέσα στον φάκελο του έργου σας:

```python
# batch_ocr.py
# -------------------------------------------------
# Bulk Image to Text Conversion using Aspose.OCR
# -------------------------------------------------

# Step 1: Import the OCR engine classes
from asposeocr import BatchOcrEngine, OcrEngine

# Step 2: Create a batch OCR engine instance
batch_engine = BatchOcrEngine()

# Step 3: Set the folder that contains the images to be processed
# Replace 'YOUR_DIRECTORY' with the absolute path to your images folder
batch_engine.input_folder = "YOUR_DIRECTORY/input_images"

# Step 4: Set the folder where the extracted text files will be saved
# Make sure this folder exists or Aspose will raise an error
batch_engine.output_folder = "YOUR_DIRECTORY/output_texts"

# Optional: Adjust OCR settings if you need higher accuracy
# For example, enable language detection for multilingual documents
# batch_engine.ocr_engine.language = "eng+spa"  # English + Spanish

# Step 5: Run the batch recognition – each supported image in the input folder is processed
batch_engine.recognize()

# Step 6: Notify that the batch operation has finished
print("Batch processing complete. Text files saved to YOUR_DIRECTORY/output_texts.")
```

### How It Works

- **`BatchOcrEngine`** περιβάλλει το κανονικό `OcrEngine` αλλά προσθέτει ορχήστρωση επι επίπεδο φακέλου, κάτι που είναι ακριβώς αυτό που χρειάζεστε όταν θέλετε να **convert images to text python** μαζικά.  
- Η ιδιότητα `input_folder` λέει στο engine πού να ψάξει για τις πηγαίες εικόνες. Σαρώνει αυτόματα τον κατάλογο και προσθέτει σε ουρά κάθε υποστηριζόμενο τύπο αρχείου.  
- Η ιδιότητα `output_folder` καθορίζει πού θα τοποθετηθεί κάθε αρχείο `.txt`. Το engine διατηρεί το αρχικό όνομα αρχείου, έτσι το `receipt1.png` γίνεται `receipt1.txt`.  
- Η κλήση `recognize()` ενεργοποιεί τον εσωτερικό βρόχο που φορτώνει κάθε εικόνα, εκτελεί OCR και γράφει το αποτέλεσμα. Η μέθοδος μπλοκάρει μέχρι να επεξεργαστούν όλα τα αρχεία, καθιστώντας εύκολο το συνδυασμό με περαιτέρω ενέργειες (π.χ., συμπίεση του φακέλου εξόδου).

#### Expected Output

Όταν τρέξετε το script:

```bash
python batch_ocr.py
```

Θα πρέπει να δείτε:

```
Batch processing complete. Text files saved to YOUR_DIRECTORY/output_texts.
```

Στο `output_texts` θα βρείτε ένα αρχείο κειμένου για κάθε εικόνα. Ανοίξτε οποιοδήποτε με έναν επεξεργαστή κειμένου και θα δείτε το ακατέργαστο αποτέλεσμα OCR—συνήθως μια κοντινή προσέγγιση του αρχικού τυπωμένου κειμένου.

## Step 4 – Verify the Results and Handle Errors

Ακόμη και οι καλύτεροι OCR engines μπορούν να δυσκολευτούν με χαμηλής ανάλυσης σάρωση ή πολύ κεκλιμένες σελίδες. Εδώ είναι ένας γρήγορος τρόπος για να ελέγξετε την έξοδο και να καταγράψετε τυχόν αποτυχίες.

```python
import os

def verify_output(output_dir):
    txt_files = [f for f in os.listdir(output_dir) if f.lower().endswith('.txt')]
    empty_files = [f for f in txt_files if os.path.getsize(os.path.join(output_dir, f)) == 0]

    if empty_files:
        print("Warning: The following files are empty – OCR may have failed:")
        for f in empty_files:
            print(f"  • {f}")
    else:
        print("All text files contain data. OCR succeeded for every image.")

# Run verification after batch processing
verify_output(batch_engine.output_folder)
```

**Why add this?**  
- Συλλαμβάνει περιπτώσεις όπου το engine παράγει σιωπηλά μια κενή συμβολοσειρά (συνηθισμένο με μη αναγνώσιμες εικόνες).  
- Σας δίνει μια λίστα προβληματικών αρχείων ώστε να τα ελέγξετε χειροκίνητα ή να τρέξετε ξανά με διαφορετικές ρυθμίσεις (π.χ., αυξήστε τις επιλογές `OcrEngine.preprocess`).  

### Edge Cases & Tweaks

| Situation | Suggested Fix |
|-----------|----------------|
| Images are rotated 90° | Set `batch_engine.ocr_engine.rotation_correction = True`. |
| Mixed languages (English + French) | Use `batch_engine.ocr_engine.language = "eng+fra"` before `recognize()`. |
| Huge PDFs converted to images first | Split PDFs into single‑page images, then feed the folder to the batch engine. |
| Memory errors on very large batches | Process smaller sub‑folders sequentially, or increase `batch_engine.max_memory_usage`. |

## Step 5 – Automate the Whole Workflow (Optional)

Αν χρειάζεται να τρέχετε αυτή τη μετατροπή καθημερινά, τυλίξτε το script σε ένα απλό shell ή Windows batch αρχείο, και προγραμματίστε το με `cron` (Linux/macOS) ή Task Scheduler (Windows). Εδώ είναι ένα ελάχιστο `run_ocr.sh` για Unix‑like συστήματα:

```bash
#!/usr/bin/env bash
# run_ocr.sh – Automate bulk image to text conversion

# Activate virtual environment
source /path/to/venv/bin/activate

# Execute the OCR script
python /path/to/ocr_project/batch_ocr.py

# Deactivate after completion
deactivate
```

Κάντε το εκτελέσιμο (`chmod +x run_ocr.sh`) και προσθέστε μια καταχώρηση cron:

```cron
0 2 * * * /path/to/run_ocr.sh >> /var/log/ocr_batch.log 2>&1
```

Αυτό τρέχει τη μετατροπή κάθε μέρα στις 2 π.μ. και καταγράφει τυχόν έξοδο για μεταγενέστερη ανασκόπηση.

---

## Conclusion

Τώρα έχετε μια αποδεδειγμένη, έτοιμη για παραγωγή μέθοδο να **convert images to text python** χρησιμοποιώντας το `BatchOcrEngine` του Aspose.OCR. Το script διαχειρίζεται **bulk image to text conversion**, γράφει κάθε αποτέλεσμα σε ξεχωριστό αρχείο, και περιλαμβάνει βήματα επαλήθευσης ώστε να βεβαιωθείτε ότι πραγματικά **recognize text from scanned images** σωστά.

Από εδώ μπορείτε:

- Να πειραματιστείτε με διαφορετικές ρυθμίσεις OCR (πακέτα γλώσσας, deskew, μείωση θορύβου).  
- Να διοχετεύσετε το παραγόμενο κείμενο σε έναν δείκτη αναζήτησης όπως το Elasticsearch για άμεση πλήρη αναζήτηση κειμένου.  
- Να συνδυάσετε αυτή τη γραμμή παραγωγής με εργαλεία μετατροπής PDF για επεξεργασία σαρωμένων PDF σε μία ενέργεια.  

Έχετε ερωτήσεις ή εντοπίσατε κάποιο πρόβλημα με συγκεκριμένο τύπο αρχείου; Αφήστε ένα σχόλιο παρακάτω και ας το λύσουμε μαζί. Καλό κώδικα, και εύχομαι οι OCR εκτελέσεις σας να είναι γρήγορες και χωρίς σφάλματα!

## What Should You Learn Next?

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}