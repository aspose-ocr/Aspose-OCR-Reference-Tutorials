---
category: general
date: 2026-06-25
description: Εξάγετε κείμενο από εικόνες με τη βιβλιοθήκη Python aocr – μάθετε ομαδική
  OCR, ορίστε τη λειτουργία αναγνώρισης σε έντυπο και προσθέστε έναν AI μετα-επεξεργαστή.
draft: false
keywords:
- extract text from images
- Python OCR batch
- aocr library
- recognition mode printed
- AI postprocessor
language: el
og_description: Εξάγετε κείμενο από εικόνες χρησιμοποιώντας τη βιβλιοθήκη Python aocr.
  Αυτό το σεμινάριο δείχνει την ομαδική OCR, τη λειτουργία αναγνώρισης εκτυπωμένου
  κειμένου και τον προαιρετικό επεξεργαστή AI.
og_title: Εξαγωγή κειμένου από εικόνες σε Python – Πλήρης οδηγός aocr batch
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  headline: Extract Text from Images in Python Using aocr OCR Batch
  type: TechArticle
- description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  name: Extract Text from Images in Python Using aocr OCR Batch
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer installed on your machine. - Basic familiarity with
      Python scripting (loops, imports, etc.). - Access to a folder of scanned images
      (PNG, JPG, TIFF, etc.).'
  - name: 1. Unsupported File Types
    text: '`aocr` silently skips files it can’t decode. If you suspect you have PDFs
      or BMPs mixed in, filter them beforehand:'
  - name: 2. Large Batches and Memory Consumption
    text: 'Running thousands of high‑resolution scans can balloon memory usage. Mitigate
      this by processing in chunks:'
  - name: 3. Empty or Low‑Contrast Pages
    text: 'If a page yields fewer than 10 characters, you might want to flag it for
      manual review:'
  type: HowTo
- questions:
  - answer: Not out‑of‑the‑box. `aocr` only handles raster images. Convert PDFs to
      PNG/TIFF first (e.g., using `pdf2image`).
    question: Does this work on PDFs?
  - answer: Absolutely—just replace `aocr.RecognitionMode.PRINTED` with `aocr.RecognitionMode.HANDWRITTEN`.
      Expect a slower run time but better results on cursive notes.
    question: Can I change the recognition mode to handwritten?
  - answer: 'The library ships with language packs. Install the desired language module
      (`pip install aocr-lang-fr` for French, etc.) and set `ocr_batch.language =
      "fr"` before running. ## Next Steps and Related Topics - **Parallel processing:**
      Wrap the batch execution in a `concurrent.futures.ThreadPoolExecuto'
    question: What if I need multilingual support?
  type: FAQPage
tags:
- OCR
- Python
- image processing
title: Εξαγωγή κειμένου από εικόνες σε Python χρησιμοποιώντας aocr OCR Batch
url: /el/python/general/extract-text-from-images-in-python-using-aocr-ocr-batch/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Εικόνες σε Python Χρησιμοποιώντας aocr OCR Batch

Ποτέ χρειάστηκε να **εξάγετε κείμενο από εικόνες** και νιώσατε καταβεβλημένοι από δεκάδες μικρά βήματα; Δεν είστε οι μόνοι. Είτε ψηφιοποιείτε σαρωμένες φόρμες, εξάγετε δεδομένα από αποδείξεις, είτε δημιουργείτε ένα αναζητήσιμο αρχείο, η απόκτηση αξιόπιστων αποτελεσμάτων OCR σε μεγάλη κλίμακα μπορεί να μοιάζει με ανάβαση σε απότομο λόφο.

Τα καλά νέα; Με τη **βιβλιοθήκη aocr** μπορείτε να δημιουργήσετε ένα πλήρες **Python OCR batch** με λίγες μόνο γραμμές κώδικα. Σε αυτόν τον οδηγό θα περάσουμε από τη δημιουργία ενός OCR batch, τη φόρτωση κάθε υποστηριζόμενης εικόνας από φάκελο, την επιλογή της σωστής **λειτουργίας αναγνώρισης printed**, και ακόμη την προσθήκη ενός **AI postprocessor** για επιπλέον ακρίβεια. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση script που εξάγει κείμενο από εικόνες και σας λέει πόσο κείμενο καταγράφηκε ανά αρχείο.

## Τι Θα Μάθετε

- Πώς να εγκαταστήσετε και να εισάγετε το πακέτο `aocr`.
- Ρύθμιση ενός `OcrBatch` για αυτόματη διαχείριση χιλιάδων αρχείων.
- Επιλογή της βέλτιστης λειτουργίας αναγνώρισης για τυπωμένα έγγραφα.
- (Προαιρετικό) Σύνδεση ενός AI post‑processor για καθαρισμό θορυβωδών αποτελεσμάτων.
- Εμφάνιση κάθε διαδρομής αρχείου μαζί με το μήκος του εξαγόμενου κειμένου.
- Συμβουλές για την αντιμετώπιση ειδικών περιπτώσεων όπως μη υποστηριζόμενες μορφές ή κενές σελίδες.

### Προαπαιτούμενα

- Python 3.8 ή νεότερο εγκατεστημένο στο σύστημά σας.  
- Βασική εξοικείωση με scripting σε Python (βρόχοι, εισαγωγές κ.λπ.).  
- Πρόσβαση σε φάκελο με σαρωμένες εικόνες (PNG, JPG, TIFF κ.λπ.).  

Αν τα έχετε, ας ξεκινήσουμε—χωρίς εξωτερικές υπηρεσίες.

## Βήμα 1: Εγκατάσταση της Βιβλιοθήκης aocr

Πρώτα απ' όλα. Το πακέτο `aocr` δεν είναι μέρος της τυπικής βιβλιοθήκης, οπότε πρέπει να το κατεβάσετε από το PyPI.

```bash
pip install aocr
```

> **Pro tip:** Χρησιμοποιήστε ένα εικονικό περιβάλλον (`python -m venv .venv`) για να διατηρήσετε τις εξαρτήσεις απομονωμένες.  

Μόλις εγκατασταθεί, μπορείτε να εισάγετε τις βασικές κλάσεις.

```python
# core imports
import aocr
```

## Βήμα 2: Δημιουργία ενός OCR Batch Instance

Ένα `OcrBatch` είναι η «μηχανή» που θα περιηγηθεί τον κατάλογό σας και θα παρακολουθεί κάθε αρχείο εικόνας. Σκεφτείτε το ως έναν κυλιόμενο ιμάντα που τροφοδοτεί τις εικόνες στον OCR κινητήρα.

```python
# Step 2: Initialize the batch
ocr_batch = aocr.OcrBatch()
```

Σε αυτό το σημείο το batch είναι κενό, αλλά θα το γεμίσουμε στο επόμενο βήμα.

## Βήμα 3: Προσθήκη Όλων των Υποστηριζόμενων Εικόνων από Φάκελο (Αναδρομικά)

Πιθανώς έχετε μια δομή φακέλων με υποφακέλους—ίσως ένας υπο‑φάκελος ανά πελάτη ή ανά μήνα. Η μέθοδος `add_folder` διασχίζει το δέντρο για εσάς, προσθέτοντας κάθε εικόνα που μπορεί να διαβάσει.

```python
# Step 3: Load images from a directory
ocr_batch.add_folder("YOUR_DIRECTORY/scanned_forms/", recursive=True)
```

Αντικαταστήστε το `"YOUR_DIRECTORY/scanned_forms/"` με την πραγματική διαδρομή στο σύστημά σας. Μετά από αυτήν την κλήση, το `ocr_batch.file_paths` περιέχει μια λίστα από απόλυτα ονόματα αρχείων, και το batch γνωρίζει ακριβώς πόσα στοιχεία θα επεξεργαστεί.

## Βήμα 4: Επιλογή της Λειτουργίας Αναγνώρισης για Τυπωμένο Κείμενο

Η μηχανή `aocr` υποστηρίζει διάφορες λειτουργίες (χειρόγραφο, τυπωμένο, μικτό). Επειδή δουλεύουμε με καθαρές, τυπωμένες φόρμες, ορίστε τη λειτουργία αναλόγως. Αυτή η μικρή σημαία μπορεί να βελτιώσει δραματικά την ακρίβεια, επειδή η μηχανή παραλείπει τις βαριές ευρετικές που απαιτούνται για καλλιγραφικά σενάρια.

```python
# Step 4: Tell the engine we have printed text
ocr_batch.recognition_mode = aocr.RecognitionMode.PRINTED
```

> **Why it matters:** Το τυπωμένο κείμενο έχει συνεπείς βάσεις και σχήματα χαρακτήρων, επιτρέποντας στο μοντέλο OCR να εφαρμόσει πιο στενά λεξικά χαρακτήρων. Αν αφήσετε τη λειτουργία σε “auto”, μπορεί να εμφανιστεί επιπλέον θόρυβος σε σαρώσεις χαμηλής ανάλυσης.

## Βήμα 5: (Προαιρετικό) Σύνδεση AI Post‑Processor

Αν οι σαρώσεις σας έχουν θολότητα, χαμηλή αντίθεση ή ασυνήθιστα γραμματοσειρές, ένας AI post‑processor μπορεί να καθαρίσει το ακατέργαστο αποτέλεσμα OCR πριν το περάσετε σε επόμενα συστήματα. Η μέθοδος `set_ai_postprocessor` αναμένει ένα αντικείμενο που υλοποιεί τη διεπαφή `process(text: str) -> str`.

Παρακάτω υπάρχει ένα ελάχιστο παράδειγμα με τη φανταστική κλάση `SimpleCleaner`. Στην πράξη, μπορείτε να ενσωματώσετε έναν μετασχηματιστή HuggingFace, ένα προσαρμοσμένο μοντέλο γλώσσας, ή ακόμη και έναν κανόνα‑βασισμένο ορθογραφικό ελεγκτή.

```python
# Optional Step 5: Define a tiny post‑processor
class SimpleCleaner:
    def process(self, text: str) -> str:
        # Strip extra whitespace and fix common OCR quirks
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")  # replace em‑dash with hyphen

# Instantiate and attach
ai = SimpleCleaner()
ocr_batch.set_ai_postprocessor(ai)
```

Αν παραλείψετε αυτό το βήμα, το batch θα επιστρέψει απλώς τις ακατέργαστες συμβολοσειρές OCR.

## Βήμα 6: Εκτέλεση OCR σε Ολόκληρο το Batch και Συλλογή Αποτελεσμάτων

Τώρα αρχίζει η βαριά δουλειά. Η μέθοδος `run` επαναλαμβάνει για κάθε αρχείο, τρέχει τον OCR κινητήρα, περνά το αποτέλεσμα μέσω του προαιρετικού AI post‑processor, και επιστρέφει μια λίστα συμβολοσειρών—μία ανά εικόνα.

```python
# Step 6: Execute the batch
ocr_results = ocr_batch.run()   # list of extracted texts
```

Επειδή η μέθοδος επιστρέφει μια απλή λίστα Python, μπορείτε να τη χειριστείτε όπως οποιαδήποτε άλλη συλλογή—να την αποθηκεύσετε, να τη γράψετε σε CSV, ή να τη στείλετε σε βάση δεδομένων.

## Βήμα 7: Εμφάνιση Κάθε Διαδρομής Αρχείου με το Μήκος του Εξαγόμενου Κειμένου

Μια γρήγορη επιβεβαίωση είναι να τυπώσετε πόσοι χαρακτήρες εξήχθησαν από κάθε αρχείο. Αν μια σελίδα είναι κενή ή το OCR απέτυχε, θα δείτε μήκος `0`.

```python
# Step 7: Show results summary
for file_path, text in zip(ocr_batch.file_paths, ocr_results):
    print(f"{file_path} -> {len(text)} chars")
```

Τυπική έξοδος μοιάζει με:

```
/data/forms/invoice_001.png -> 1245 chars
/data/forms/invoice_002.jpg -> 0 chars
/data/forms/receipt_2023-04-15.tif -> 876 chars
```

Η εμφάνιση μιας σημαίας `0` σας λέει αμέσως ποια αρχεία χρειάζονται δεύτερη ματιά (ίσως είναι κατεστραμμένα ή δεν είναι καθόλου εικόνα).

## Διαχείριση Συνηθισμένων Ειδικών Περιπτώσεων

### 1. Μη Υποστηριζόμενοι Τύποι Αρχείων

Το `aocr` παραλείπει σιωπηλά αρχεία που δεν μπορεί να αποκωδικοποιήσει. Αν υποψιάζεστε ότι έχετε PDFs ή BMPs ανάμεικτα, φιλτράρετε τα εκ των προτέρων:

```python
supported_ext = {".png", ".jpg", ".jpeg", ".tif", ".tiff"}
ocr_batch.file_paths = [
    p for p in ocr_batch.file_paths if p.lower().endswith(tuple(supported_ext))
]
```

### 2. Μεγάλα Batches και Κατανάλωση Μνήμης

Η εκτέλεση χιλιάδων σαρώσεων υψηλής ανάλυσης μπορεί να αυξήσει τη χρήση μνήμης. Μετριάστε το πρόβλημα επεξεργάζοντας σε τμήματα:

```python
batch_size = 200
for i in range(0, len(ocr_batch.file_paths), batch_size):
    sub_batch = aocr.OcrBatch()
    sub_batch.file_paths = ocr_batch.file_paths[i:i+batch_size]
    sub_batch.recognition_mode = aocr.RecognitionMode.PRINTED
    if 'ai' in locals():
        sub_batch.set_ai_postprocessor(ai)
    results = sub_batch.run()
    # handle results (e.g., write to file) before next chunk
```

### 3. Κενές ή Χαμηλής Αντίθεσης Σελίδες

Αν μια σελίδα αποδίδει λιγότερους από 10 χαρακτήρες, ίσως θέλετε να την σημαδέψετε για χειροκίνητη ανασκόπηση:

```python
for fp, txt in zip(ocr_batch.file_paths, ocr_results):
    if len(txt.strip()) < 10:
        print(f"⚠️  Low‑confidence result for {fp}")
```

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι ένα script που μπορείτε να αντιγράψετε‑επικολλήσετε και να τρέξετε αμέσως. Αποθηκεύστε το ως `batch_ocr.py`.

```python
#!/usr/bin/env python3
"""
Batch OCR script using aocr to extract text from images.
"""

import aocr

# ----------------------------------------------------------------------
# Optional: a tiny AI post‑processor to clean up OCR output
# ----------------------------------------------------------------------
class SimpleCleaner:
    def process(self, text: str) -> str:
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_ROOT = "YOUR_DIRECTORY/scanned_forms/"   # ← change this!
RECOGNITION_MODE = aocr.RecognitionMode.PRINTED

# ----------------------------------------------------------------------
# Build and run the OCR batch
# ----------------------------------------------------------------------
def main():
    # 1️⃣ Create batch
    batch = aocr.OcrBatch()

    # 2️⃣ Load images recursively
    batch.add_folder(IMAGE_ROOT, recursive=True)

    # 3️⃣ Set mode for printed text
    batch.recognition_mode = RECOGNITION_MODE

    # 4️⃣ Attach AI post‑processor (comment out if not needed)
    ai = SimpleCleaner()
    batch.set_ai_postprocessor(ai)

    # 5️⃣ Run OCR
    results = batch.run()

    # 6️⃣ Summarize
    for path, text in zip(batch.file_paths, results):
        print(f"{path} -> {len(text)} chars")

if __name__ == "__main__":
    main()
```

**Αναμενόμενη έξοδος** (περιορισμένη για συντομία):

```
/home/me/scanned_forms/formA.png -> 1342 chars
/home/me/scanned_forms/subfolder/formB.tif -> 0 chars
/home/me/scanned_forms/invoice_2024-01.jpg -> 987 chars
```

Τρέξτε το με:

```bash
python batch_ocr.py
```

Αν όλα έχουν ρυθμιστεί σωστά, θα δείτε μια γραμμή για κάθε εικόνα, η οποία αναφέρει τον αριθμό χαρακτήρων του εξαγόμενου κειμένου.

## Συχνές Ερωτήσεις

**Q: Does this work on PDFs?**  
A: Not out‑of‑the‑box. `aocr` only handles raster images. Convert PDFs to PNG/TIFF first (e.g., using `pdf2image`).  

**Q: Can I change the recognition mode to handwritten?**  
A: Absolutely—just replace `aocr.RecognitionMode.PRINTED` with `aocr.RecognitionMode.HANDWRITTEN`. Expect a slower run time but better results on cursive notes.  

**Q: What if I need multilingual support?**  
A: The library ships with language packs. Install the desired language module (`pip install aocr-lang-fr` for French, etc.) and set `ocr_batch.language = "fr"` before running.  

## Επόμενα Βήματα και Σχετικά Θέματα

- **Parallel processing:** Τυλίξτε την εκτέλεση του batch σε ένα `concurrent.futures.ThreadPoolExecutor` για να αξιοποιήσετε πολλαπλούς πυρήνες CPU.  
- **Storing results:** Γράψτε τα `ocr_results` σε CSV ή βάση δεδομένων SQLite για downstream analytics.  
- **Integrating with cloud AI:** Αντικαταστήστε το `SimpleCleaner` με ένα μοντέλο transformer από HuggingFace για state‑of‑the‑art διόρθωση ορθογραφίας.  
- **Fine‑tuning aocr:** Αν έχετε ένα προσαρμοσμένο σύνολο γραμματοσειρών, εξερευνήστε το `aocr.Trainer` για βελτίωση της ακρίβειας σε λειτουργία printed.  

---

That’s it—you now have a solid

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Βήμα‑βήμα](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Εξαγωγή Κειμένου από Εικόνες Χρησιμοποιώντας OCR Λειτουργία σε Φακέλους](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Πώς να Batch OCR Εικόνες με Λίστα στο Aspose.OCR για .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}