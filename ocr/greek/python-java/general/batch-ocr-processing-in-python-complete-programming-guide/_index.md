---
category: general
date: 2026-06-25
description: Η ομαδική επεξεργασία OCR σε Python γίνεται εύκολη. Μάθετε πώς να εξάγετε
  κείμενο από παρτίδα εικόνων και να κυριαρχήσετε στην εξαγωγή κειμένου από παρτίδα
  εικόνων με παράλληλα νήματα.
draft: false
keywords:
- batch OCR processing
- extract text from image batch
- batch image text extraction
language: el
og_description: Η επεξεργασία OCR σε παρτίδες με Python σας επιτρέπει να εξάγετε κείμενο
  από παρτίδα εικόνων γρήγορα. Αυτό το σεμινάριο σας καθοδηγεί στη παράλληλη OCR με
  σαφή παραδείγματα κώδικα.
og_title: Ομαδική επεξεργασία OCR σε Python – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Batch OCR processing in Python made easy. Learn how to extract text
    from image batch and master batch image text extraction with parallel threads.
  headline: Batch OCR Processing in Python – Complete Programming Guide
  type: TechArticle
- description: Batch OCR processing in Python made easy. Learn how to extract text
    from image batch and master batch image text extraction with parallel threads.
  name: Batch OCR Processing in Python – Complete Programming Guide
  steps:
  - name: Missing or Corrupt Images
    text: If an image can’t be opened, most OCR libraries raise an exception that
      aborts the whole batch. Wrap the call in a `try/except` inside the batch function
      or filter out problematic files beforehand (see the sanity check in Step 1).
  - name: Language & DPI Settings
    text: For multilingual documents, pass a `langs` parameter (e.g., `langs=['en',
      'de']`). If your scans are low‑resolution, consider pre‑processing with `Pillow`
      to upscale to 300 DPI before OCR—this often boosts accuracy.
  - name: Memory Constraints
    text: 'Eight threads can eat RAM, especially with large images. If you hit memory
      errors, lower `max_threads` or process the list in smaller chunks:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Επεξεργασία OCR κατά παρτίδες σε Python – Πλήρης οδηγός προγραμματισμού
url: /el/python-java/general/batch-ocr-processing-in-python-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Επεξεργασία OCR σε Παρτίδες με Python – Πλήρης Οδηγός Προγραμματισμού

Έχετε χρειαστεί ποτέ **επεξεργασία OCR σε παρτίδες** αλλά δεν ήσασταν σίγουροι πώς να την εκτελέσετε αποδοτικά σε δεκάδες σαρωμένες σελίδες; Δεν είστε μόνοι—οι προγραμματιστές συχνά συναντούν εμπόδια όταν προσπαθούν να εξάγουν κείμενο από παρτίδα εικόνων χωρίς να υπερφορτώνουν την CPU.  

Σε αυτόν τον οδηγό θα σας δείξουμε έναν απλό τρόπο για να **εξάγετε κείμενο από παρτίδα εικόνων** χρησιμοποιώντας τη μηχανή OCR της Python, να εκτελέσετε τη δουλειά σε έως και οκτώ νήματα, και τελικά να δείτε πόσους χαρακτήρες συνέβαλε κάθε εικόνα. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο script που διαχειρίζεται **εξαγωγή κειμένου από εικόνες σε παρτίδα** σαν επαγγελματίας.

## Τι Καλύπτει Αυτός ο Οδηγός

Θα περάσουμε από τρία πρακτικά βήματα:

1. Δημιουργήστε μια λίστα με τα αρχεία εικόνας που θέλετε να αναγνωρίσετε.  
2. Εκκινήστε τη μηχανή OCR παράλληλα με `max_threads=8`.  
3. Περάστε σε βρόχο τα αποτελέσματα και εκτυπώστε μια συνοπτική σύνοψη.

Χωρίς εξωτερικές υπηρεσίες, χωρίς σπάνιες βιβλιοθήκες—μόνο απλή Python και ένας τυπικός περιτύλιγμα OCR (για παράδειγμα, `ocr` από το `easyocr` ή ένα προσαρμοσμένο wrapper). Αν έχετε Python 3.8+ και ένα πακέτο OCR εγκατεστημένο, είστε έτοιμοι να αντιγράψετε‑επικολλήσετε και να τρέξετε.

---

## Βήμα 1: Προετοιμάστε μια Λίστα Αρχείων Εικόνας για Επεξεργασία OCR σε Παρτίδες

Το πρώτο που χρειάζεστε είναι μια συλλογή από διαδρομές εικόνων. Σκεφτείτε το ως λίστα αγορών για τη μηχανή OCR· κάθε καταχώρηση δείχνει σε ένα αρχείο PNG, JPEG ή TIFF που περιέχει το κείμενο που θέλετε να διαβάσετε.

```python
# Step 1: Prepare a list of image files to be recognized
image_files = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png",
    "YOUR_DIRECTORY/page4.png",
    "YOUR_DIRECTORY/page5.png"
]

# Quick sanity check – make sure the files exist
import os
missing = [p for p in image_files if not os.path.isfile(p)]
if missing:
    raise FileNotFoundError(f"These files are missing: {missing}")
```

**Γιατί αυτό είναι σημαντικό:**  
Η δημιουργία της λίστας εκ των προτέρων επιτρέπει στη μηχανή OCR να λειτουργεί σε πραγματική λειτουργία παρτίδας. Σας παρέχει επίσης ένα ενιαίο σημείο για προσθήκη ή αφαίρεση αρχείων χωρίς να επηρεάσετε τη λογική επεξεργασίας αργότερα. Ο έλεγχος εγκυρότητας αποτρέπει το ανεπιθύμητο σφάλμα “file not found” κατά τη διάρκεια μιας μακράς εκτέλεσης.

---

## Βήμα 2: Εκτελέστε OCR στην Παρτίδα με Παράλληλα Νήματα (Extract Text from Image Batch)

Τώρα δίνουμε τη λίστα στη μηχανή OCR. Οι περισσότερες σύγχρονες βιβλιοθήκες OCR εκθέτουν μια μέθοδο `recognize_batch` που δέχεται ένα όρισμα `max_threads`. Ορίζοντάς το σε `8` λέμε στη βιβλιοθήκη να δημιουργήσει οκτώ νήματα εργασίας, τα οποία σε έναν τετραπύρηνο CPU με hyper‑threading μπορούν να μειώσουν δραστικά το χρόνο επεξεργασίας.

```python
# Step 2: Run OCR on the batch, allowing up to 8 parallel threads
# Assuming `ocr` is a module that provides OcrEngine with recognize_batch()
import ocr

batch_results = ocr.OcrEngine.recognize_batch(image_files, max_threads=8)

# batch_results is a list of Result objects, each with a .text attribute
```

**Γιατί η παράλληλη εκτέλεση βοηθά:**  
Το OCR είναι εντατικό σε CPU· κάθε εικόνα περνάει από ένα νευρωνικό δίκτυο ή μια κληρονομική μηχανή. Η εκτέλεσή τους μία μετά την άλλη μπορεί να είναι εξαιρετικά αργή, ειδικά για σαρώσεις υψηλής ανάλυσης. Τα παράλληλα νήματα κρατούν όλους τους πυρήνες απασχολημένους, μετατρέποντας μια εργασία 5‑λεπτών σε 1‑λεπτη σε τυπικό υλικό.

**Συμβουλή:**  
Αν χρησιμοποιείτε το `easyocr`, η κλήση μοιάζει με `reader.readtext(image_path, detail=0)` μέσα σε βρόχο. Η αφαίρεση `recognize_batch` κρύβει αυτήν τη πολυπλοκότητα, αλλά μπορείτε πάντα να την αντικαταστήσετε με το δικό σας `ThreadPoolExecutor` εάν η βιβλιοθήκη δεν παρέχει υποστήριξη παρτίδας.

---

## Βήμα 3: Επανάληψη στα Αποτελέσματα και Σύνοψη Εξαγωγής Κειμένου από Εικόνες σε Παρτίδα

Μετά το OCR, θα έχετε μια λίστα αντικειμένων αποτελεσμάτων. Ας συνδυάσουμε τις αρχικές διαδρομές αρχείων με το αντίστοιχο αποτέλεσμα OCR και να εκτυπώσουμε μια καθαρή γραμμή για κάθε εικόνα που δείχνει πόσοι χαρακτήρες αναγνωρίστηκαν.

```python
# Step 3: Iterate through the results and display character counts
for file_path, result in zip(image_files, batch_results):
    # result.text holds the raw extracted string
    char_count = len(result.text)
    print(f"{file_path} → {char_count} characters recognized")
```

**Τι θα δείτε:**  

```
YOUR_DIRECTORY/page1.png → 1245 characters recognized
YOUR_DIRECTORY/page2.png → 987 characters recognized
YOUR_DIRECTORY/page3.png → 1103 characters recognized
YOUR_DIRECTORY/page4.png → 1320 characters recognized
YOUR_DIRECTORY/page5.png → 845 characters recognized
```

**Γιατί αυτό το βήμα είναι χρήσιμο:**  
Μια γρήγορη καταμέτρηση χαρακτήρων σας λέει με μια ματιά αν μια εικόνα επεξεργάστηκε σωστά. Ένας απροσδόκητα χαμηλός αριθμός μπορεί να υποδεικνύει θολή σάρωση, λανθασμένη ρύθμιση γλώσσας ή κατεστραμμένο αρχείο—προβλήματα που μπορείτε να αντιμετωπίσετε πριν προχωρήσετε στην ανάλυση downstream.

---

## Μπόνους: Διαχείριση Ακραίων Περιπτώσεων και Συνηθισμένων Παγίδων

### Ελλιπείς ή Κατεστραμμένες Εικόνες  
Αν μια εικόνα δεν μπορεί να ανοιχτεί, οι περισσότερες βιβλιοθήκες OCR ρίχνουν μια εξαίρεση που διακόπτει ολόκληρη την παρτίδα. Τυλίξτε την κλήση σε `try/except` μέσα στη συνάρτηση παρτίδας ή φιλτράρετε τα προβληματικά αρχεία εκ των προτέρων (δείτε τον έλεγχο εγκυρότητας στο Βήμα 1).

### Ρυθμίσεις Γλώσσας & DPI  
Για πολυγλωσσικά έγγραφα, περάστε μια παράμετρο `langs` (π.χ., `langs=['en', 'de']`). Αν οι σαρώσεις σας είναι χαμηλής ανάλυσης, σκεφτείτε προεπεξεργασία με `Pillow` για αύξηση σε 300 DPI πριν το OCR—αυτό συχνά βελτιώνει την ακρίβεια.

### Περιορισμοί Μνήμης  
Οκτώ νήματα μπορούν να καταναλώσουν RAM, ειδικά με μεγάλες εικόνες. Αν αντιμετωπίσετε σφάλματα μνήμης, μειώστε το `max_threads` ή επεξεργαστείτε τη λίστα σε μικρότερα τμήματα:

```python
from itertools import islice

def chunked(iterable, size):
    it = iter(iterable)
    while True:
        chunk = list(islice(it, size))
        if not chunk:
            break
        yield chunk

for chunk in chunked(image_files, 3):  # process three images at a time
    results = ocr.OcrEngine.recognize_batch(chunk, max_threads=3)
    # handle results...
```

---

## Πλήρες Λειτουργικό Script

Συνδυάζοντας όλα, εδώ είναι ένα πλήρες, έτοιμο‑να‑τρέξει παράδειγμα. Αντικαταστήστε το `"YOUR_DIRECTORY"` με τη διαδρομή που περιέχει τα αρχεία PNG σας και βεβαιωθείτε ότι το module `ocr` είναι εγκατεστημένο.

```python
#!/usr/bin/env python3
"""
Batch OCR Processing Script
Extracts text from an image batch using parallel threads and prints character counts.
"""

import os
import ocr  # Replace with your OCR library import, e.g., from easyocr import Reader

# -------------------------------------------------
# Step 1: Define the list of image files
# -------------------------------------------------
image_dir = "YOUR_DIRECTORY"
image_files = [
    os.path.join(image_dir, f"page{i}.png") for i in range(1, 6)
]

# Verify that all files exist
missing = [p for p in image_files if not os.path.isfile(p)]
if missing:
    raise FileNotFoundError(f"Missing image files: {missing}")

# -------------------------------------------------
# Step 2: Run OCR in parallel (max 8 threads)
# -------------------------------------------------
# The OcrEngine is a placeholder – adapt to your library's API
batch_results = ocr.OcrEngine.recognize_batch(image_files, max_threads=8)

# -------------------------------------------------
# Step 3: Report how many characters each image yielded
# -------------------------------------------------
for file_path, result in zip(image_files, batch_results):
    char_count = len(result.text)
    print(f"{file_path} → {char_count} characters recognized")
```

**Αναμενόμενη έξοδος** (οι αριθμοί σας θα διαφέρουν):

```
YOUR_DIRECTORY/page1.png → 1245 characters recognized
YOUR_DIRECTORY/page2.png → 987 characters recognized
YOUR_DIRECTORY/page3.png → 1103 characters recognized
YOUR_DIRECTORY/page4.png → 1320 characters recognized
YOUR_DIRECTORY/page5.png → 845 characters recognized
```

Τρέξτε το script με `python batch_ocr.py` και παρακολουθήστε το τερματικό να γεμίζει με συνοπτικά στατιστικά.

---

## Οπτική Επισκόπηση

![Διάγραμμα ροής επεξεργασίας OCR σε παρτίδες](image-placeholder.png "Διάγραμμα που απεικονίζει τα βήματα επεξεργασίας OCR σε παρτίδες")

*Κείμενο alt εικόνας:* *Διάγραμμα ροής επεξεργασίας OCR σε παρτίδες που δείχνει τη δημιουργία λίστας αρχείων, την παράλληλη εκτέλεση OCR και τη σύνοψη των αποτελεσμάτων.*

---

## Συμπέρασμα

Τώρα έχετε μια ισχυρή βάση για **επεξεργασία OCR σε παρτίδες** με Python. Με την προετοιμασία μιας καθαρής λίστας εικόνων, την αξιοποίηση παράλληλων νημάτων για **extract text from image batch**, και τη σύνοψη των αποτελεσμάτων, μπορείτε να μετατρέψετε μια επίπονη χειροκίνητη εργασία σε μια γρήγορη, επαναλαμβανόμενη ροή.

Από εδώ μπορείτε:

- Αποθηκεύστε κάθε `result.text` σε αρχείο `.txt` για downstream NLP.  
- Συνδυάστε τις καταμετρήσεις χαρακτήρων με τις βαθμολογίες εμπιστοσύνης για φιλτράρισμα σελίδων χαμηλής ποιότητας.  
- Ενσωματώστε το script σε μια μεγαλύτερη ροή εισαγωγής εγγράφων, ίσως τροφοδοτώντας ένα ευρετήριο αναζήτησης.

Είτε ψηφιοποιείτε αρχεία, είτε δημιουργείτε μια εφαρμογή σάρωσης αποδείξεων, είτε προετοιμάζετε δεδομένα εκπαίδευσης για μοντέλο γλώσσας, οι έννοιες που καλύφθηκαν εδώ κλιμακώνονται σε εκατοντάδες ή χιλιάδες αρχεία με ελάχιστες προσαρμογές.

Έχετε ερωτήσεις σχετικά με τις ρυθμίσεις γλώσσας, την προεπεξεργασία εικόνας ή την ανάπτυξη αυτού στο cloud; Αφήστε ένα σχόλιο ή δείτε σχετικούς οδηγούς για *Python image preprocessing* και *asynchronous OCR with asyncio*. Καλή προγραμματιστική!

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικό θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε σε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Βήμα‑βήμα](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Πώς να Επεξεργαστείτε OCR Εικόνες σε Παρτίδα με Λίστα στο Aspose.OCR για .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Εξαγωγή Κειμένου από Εικόνα – Βελτιστοποίηση OCR με Aspose.OCR για .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}