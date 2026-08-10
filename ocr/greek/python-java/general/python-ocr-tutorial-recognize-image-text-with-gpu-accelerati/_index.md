---
category: general
date: 2026-06-06
description: Εκπαιδευτικό σε Python OCR που δείχνει πώς να αναγνωρίζετε κείμενο εικόνας,
  να εκτελείτε OCR υψηλής ανάλυσης και να εξάγετε ισπανικό κείμενο χρησιμοποιώντας
  OCR επιταχυμένο με GPU.
draft: false
keywords:
- python ocr tutorial
- recognize image text
- high resolution ocr
- gpu accelerated ocr
- extract spanish text
language: el
og_description: Μάθημα Python OCR που σας καθοδηγεί στη αναγνώριση κειμένου σε εικόνες,
  OCR υψηλής ανάλυσης και εξαγωγή ισπανικού κειμένου με επιτάχυνση GPU.
og_title: Μάθημα OCR με Python – Αναγνώριση κειμένου με επιτάχυνση GPU
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Python OCR tutorial showing how to recognize image text, perform high
    resolution OCR and extract Spanish text using GPU accelerated OCR.
  headline: Python OCR Tutorial – Recognize Image Text with GPU Acceleration
  type: TechArticle
- description: Python OCR tutorial showing how to recognize image text, perform high
    resolution OCR and extract Spanish text using GPU accelerated OCR.
  name: Python OCR Tutorial – Recognize Image Text with GPU Acceleration
  steps:
  - name: Prerequisites
    text: '- Python 3.9+ (the code works on 3.10 and newer as well). - A CUDA‑compatible
      GPU (optional but highly recommended). - Basic familiarity with pip and virtual
      environments.'
  - name: 6.1 Fallback When No GPU Is Present
    text: "```python if not torch.cuda.is_available(): # Re‑initialize the reader
      without GPU to avoid hidden errors reader = Reader(lang_list=[\"es\"], gpu=False)
      print(\"\U0001F504 Re‑initialized reader for CPU execution.\") ```"
  - name: 6.2 Down‑sampling Very Large Images
    text: 'If your image is larger than 4000 × 4000 px, you might run out of GPU memory.
      Down‑sample proportionally while preserving DPI:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- GPU
- Spanish
title: Python OCR Tutorial – Αναγνώριση κειμένου εικόνας με επιτάχυνση GPU
url: /el/python-java/general/python-ocr-tutorial-recognize-image-text-with-gpu-accelerati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR Tutorial – Αναγνώριση Κειμένου σε Εικόνα με Επιτάχυνση GPU

Έχετε αναρωτηθεί ποτέ πώς να **αναγνωρίσετε κείμενο σε εικόνα** σε ένα script Python χωρίς να ξοδεύετε ώρες ρυθμίζοντας παραμέτρους; Δεν είστε ο μόνος. Σε αυτό το **python ocr tutorial** θα σας δείξουμε έναν καθαρό, ολοκληρωμένο τρόπο να εξάγετε ισπανικό κείμενο από μια εικόνα υψηλής ανάλυσης, και θα προσθέσουμε επιτάχυνση GPU ώστε η διαδικασία να τρέχει αστραπιαία.

Σκεφτείτε το ως μια γρήγορη επίδειξη κατά τη διάρκεια του καφέ, που μπορείτε να επεκτείνετε σε μια παραγωγική γραμμή εργασίας αργότερα. Στο τέλος αυτού του οδηγού θα έχετε ένα εκτελέσιμο πρόγραμμα που εκτελεί **OCR υψηλής ανάλυσης**, αξιοποιεί μια GPU με υποστήριξη CUDA, και παράγει τους ακριβείς ισπανικούς χαρακτήρες που χρειάζεστε.

## Τι Θα Μάθετε

- Πώς να εγκαταστήσετε και να εισάγετε μια σύγχρονη βιβλιοθήκη OCR που υποστηρίζει επιτάχυνση GPU.  
- Πώς να δημιουργήσετε μια παρουσία (instance) του μηχανήματος OCR και να το ρυθμίσετε να **αναγνωρίζει κείμενο σε εικόνα** στα Ισπανικά.  
- Πώς να ενεργοποιήσετε **GPU επιταχυνόμενο OCR** για τεράστια κέρδη ταχύτητας σε αρχεία υψηλής ανάλυσης.  
- Πώς να αντιμετωπίσετε ειδικές περιπτώσεις όπως η έλλειψη οδηγών CUDA ή η επιστροφή στην CPU.  
- Συμβουλές για τη βελτίωση της ακρίβειας όταν χρειάζεται να **εξάγετε ισπανικό κείμενο** από θορυβώδεις σάρωση.

### Προαπαιτούμενα

- Python 3.9+ (ο κώδικας λειτουργεί επίσης σε 3.10 και νεότερες εκδόσεις).  
- Μια GPU συμβατή με CUDA (προαιρετική αλλά ιδιαίτερα συνιστώμενη).  
- Βασική εξοικείωση με pip και εικονικά περιβάλλοντα.  

Αν λείπει κάποιο από αυτά, το tutorial λειτουργεί ακόμη—απλώς παραλείψτε το βήμα GPU και η βιβλιοθήκη θα επιστρέψει αυτόματα στην CPU.

---

## Python OCR Tutorial: Εγκατάσταση των Απαιτούμενων Πακέτων

Πρώτα απ' όλα, χρειαζόμαστε μια αξιόπιστη μηχανή OCR. Για αυτό το tutorial θα χρησιμοποιήσουμε το ανοιχτού κώδικα πακέτο **`easyocr`**, το οποίο περιλαμβάνει ενσωματωμένη υποστήριξη GPU όταν εντοπιστεί συμβατή συσκευή.

```bash
# Create a fresh virtual environment (optional but tidy)
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows use `ocr-env\Scripts\activate`

# Install EasyOCR and its optional torch dependencies
pip install easyocr[torch]   # Installs both CPU and GPU builds of PyTorch
```

> **Pro tip:** Αν έχετε ήδη εγκατεστημένο το PyTorch, βεβαιωθείτε ότι ταιριάζει με την έκδοση CUDA σας (`pip install torch==2.2.0+cu121 -f https://download.pytorch.org/whl/torch_stable.html`). Οι ασυμφωνίες εκδόσεων είναι κοινή πηγή σφαλμάτων “GPU not found”.

---

## Βήμα 1: Δημιουργία μιας Παρουσίας (Instance) του Μηχανήματος OCR

Τώρα ξεκινάμε τη μηχανή. Το EasyOCR ονομάζει την κύρια κλάση του `Reader`. Ο κατασκευαστής δέχεται μια λίστα κωδικών γλώσσας· θα περάσουμε `"es"` για Ισπανικά.

```python
# Step 1: Initialize the OCR reader for Spanish
from easyocr import Reader

# The `gpu` flag tells EasyOCR to try using CUDA if it’s available.
reader = Reader(lang_list=["es"], gpu=True)
```

*Γιατί είναι σημαντικό:* Με την προκήρυξη της γλώσσας εκ των προτέρων, η μηχανή φορτώνει μόνο τα απαραίτητα βάρη νευρωνικού δικτύου, εξοικονομώντας μνήμη και επιταχύνοντας την εκτίμηση—ιδιαίτερα χρήσιμο όταν ασχολείστε με **OCR υψηλής ανάλυσης** αργότερα.

---

## Βήμα 2: Προετοιμασία μιας Εικόνας Υψηλής Ανάλυσης

Οι εικόνες υψηλής ανάλυσης παρέχουν στο μοντέλο περισσότερα pixel για επεξεργασία, κάτι που συνήθως μεταφράζεται σε καλύτερη αναγνώριση χαρακτήρων. Ας υποθέσουμε ότι έχετε ένα αρχείο με όνομα `high_res_spanish.png` σε φάκελο που ονομάζεται `samples`.

```python
import os

# Construct an absolute path – keeps the script portable
image_path = os.path.join("samples", "high_res_spanish.png")

# Quick sanity check – raise a clear error if the file is missing
if not os.path.isfile(image_path):
    raise FileNotFoundError(f"Image not found at {image_path}")
```

Αν δεν έχετε διαθέσιμο δείγμα υψηλής ανάλυσης, μπορείτε να κατεβάσετε ένα δωρεάν από το Unsplash ή να δημιουργήσετε μια συνθετική εικόνα με το Pillow. Το κλειδί είναι να διατηρήσετε το DPI πάνω από 300 για τα καλύτερα αποτελέσματα.

---

## Βήμα 3: Ενεργοποίηση Επιτάχυνσης GPU (Προαιρετικό αλλά Συνιστώμενο)

Το EasyOCR προσπαθεί ήδη να χρησιμοποιήσει την GPU όταν ορίσετε `gpu=True`. Ωστόσο, είναι καλή πρακτική να επαληθεύσετε ότι η συσκευή χρησιμοποιείται πραγματικά, ειδικά σε συστήματα με πολλαπλές GPU.

```python
import torch

# Verify CUDA availability – helpful for debugging
if torch.cuda.is_available():
    print(f"✅ CUDA device detected: {torch.cuda.get_device_name(0)}")
else:
    print("⚠️ No CUDA device found – falling back to CPU. Performance will be slower.")
```

*Γιατί να το ελέγξετε;* Αν το script επιστρέψει σιωπηλά στην CPU, μπορεί να αναρωτηθείτε γιατί μια λειτουργία 5 δευτερολέπτων ξαφνικά διαρκεί 30 δευτερόλεπτα. Αυτός ο μικρός έλεγχος κάνει τη συμπεριφορά διαφανή και διατηρεί την **GPU επιταχυνόμενη OCR** γραμμή εργασίας προβλέψιμη.

---

## Βήμα 4: Εκτέλεση OCR Υψηλής Ανάλυσης και Αναγνώριση Κειμένου σε Εικόνα

Τώρα το διασκεδαστικό μέρος—να διαβάσουμε πραγματικά το κείμενο. Η μέθοδος `readtext` του EasyOCR επιστρέφει μια λίστα από πλειάδες που περιέχουν το πλαίσιο, τη αναγνωρισμένη συμβολοσειρά και ένα σκορ εμπιστοσύνης.

```python
# Step 4: Run OCR on the high‑resolution image
results = reader.readtext(image_path, detail=1, paragraph=False)

# `results` looks like:
# [
#   ([(x1, y1), (x2, y2), (x3, y3), (x4, y4)], 'Texto reconocido', 0.98),
#   ...
# ]
```

Αν χρειάζεστε τη ακατέργαστη συμβολοσειρά χωρίς συντεταγμένες, ορίστε `detail=0`. Για τις περισσότερες περιπτώσεις χρήσης **αναγνώρισης κειμένου σε εικόνα**, η προεπιλογή (`detail=1`) σας παρέχει αρκετό πλαίσιο για επεξεργασία αργότερα.

---

## Βήμα 5: Εξαγωγή Ισπανικού Κειμένου και Καθαρισμός του Αποτελέσματος

Επειδή ζητήσαμε από το EasyOCR Ισπανικά, οι επιστρεφόμενες συμβολοσειρές είναι ήδη σε αυτή τη γλώσσα. Παρόλα αυτά, ίσως θέλετε να τις συνενώσετε, να αφαιρέσετε κενά ή να φιλτράρετε ανιχνεύσεις χαμηλής εμπιστοσύνης.

```python
# Step 5: Consolidate high‑confidence Spanish strings
extracted_text = []
for bbox, text, conf in results:
    if conf > 0.85:                # Drop anything below 85 % confidence
        extracted_text.append(text)

# Join everything into a single block – perfect for further NLP tasks
final_text = "\n".join(extracted_text)

print("📝 Extracted Spanish text:")
print(final_text)
```

**Τι γίνεται αν η εμπιστοσύνη είναι χαμηλή;** Μπορείτε είτε να μειώσετε το όριο (κινδυνεύοντας θόρυβο) είτε να προεπεξεργαστείτε την εικόνα (αυξήστε την αντίθεση, δυαδικοποιήστε ή διορθώστε την κλίση). Αυτά τα κόλπα είναι κοινά όταν αντιμετωπίζετε **OCR υψηλής ανάλυσης** σε σαρωμένα έγγραφα.

---

## Βήμα 6: Διαχείριση Ειδικών Περιπτώσεων και Ρυθμίσεις Απόδοσης

Ακόμη και τα καλύτερα εκπαιδευμένα μοντέλα αντιμετωπίζουν προβλήματα σε ορισμένα σενάρια. Παρακάτω υπάρχουν μερικές γρήγορες διορθώσεις που μπορείτε να επικολλήσετε στο script.

### 6.1 Εναλλακτική Λύση όταν δεν υπάρχει GPU

```python
if not torch.cuda.is_available():
    # Re‑initialize the reader without GPU to avoid hidden errors
    reader = Reader(lang_list=["es"], gpu=False)
    print("🔄 Re‑initialized reader for CPU execution.")
```

### 6.2 Μείωση Δειγματοληψίας Πολύ Μεγάλων Εικόνων

Αν η εικόνα σας είναι μεγαλύτερη από 4000 × 4000 px, μπορεί να εξαντλήσετε τη μνήμη GPU. Μειώστε τη δειγματοληψία αναλογικά διατηρώντας το DPI:

```python
from PIL import Image

def resize_if_needed(path, max_dim=3000):
    img = Image.open(path)
    if max(img.size) > max_dim:
        scale = max_dim / max(img.size)
        new_size = (int(img.width * scale), int(img.height * scale))
        img = img.resize(new_size, Image.LANCZOS)
        resized_path = path.replace(".png", "_resized.png")
        img.save(resized_path)
        return resized_path
    return path

image_path = resize_if_needed(image_path)
```

Αυτά τα αποσπάσματα διατηρούν το script ανθεκτικό, είτε τρέχετε σε workstation είτε σε ένα μέτριο laptop.

---

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα, εδώ είναι το πλήρες script που μπορείτε να αντιγράψετε‑επικολλήσετε και να τρέξετε αμέσως:

```python
# python_ocr_tutorial.py
import os
import torch
from PIL import Image
from easyocr import Reader

# ----------------------------------------------------------------------
# Helper: Resize very large images to avoid GPU OOM errors
def resize_if_needed(path, max_dim=3000):
    img = Image.open(path)
    if max(img.size) > max_dim:
        scale = max_dim / max(img.size)
        new_size = (int(img.width * scale), int(img.height * scale))
        img = img.resize(new_size, Image.LANCZOS)
        resized_path = path.replace(".png", "_resized.png")
        img.save(resized_path)
        return resized_path
    return path
# ----------------------------------------------------------------------

# 1️⃣ Verify CUDA availability (optional)
if torch.cuda.is_available():
    print(f"✅ CUDA device detected: {torch.cuda.get_device_name(0)}")
else:
    print("⚠️ No CUDA device – using CPU (expect slower performance).")

# 2️⃣ Initialize the OCR engine for Spanish (GPU if possible)
reader = Reader(lang_list=["es"], gpu=torch.cuda.is_available())

# 3️⃣ Path to the high‑resolution image
image_path = os.path.join("samples", "high_res_spanish.png")
if not os.path.isfile(image_path):
    raise FileNotFoundError(f"Image not found at {image_path}")

# 4️⃣ Resize if the image is gigantic
image_path = resize_if_needed(image_path)

# 5️⃣ Run OCR – this is the core **recognize image text** step
results = reader.readtext(image_path, detail=1, paragraph=False)

# 6️⃣ Filter and concatenate high‑confidence Spanish strings
extracted = []
for bbox, txt, conf in results:
    if conf > 0.85:
        extracted.append(txt)

final_text = "\n".join(extracted)

# 7️⃣ Output the result – **extract spanish text** ready for downstream processing
print("\n📝 Extracted Spanish text:")
print(final_text)
```

**Αναμενόμενο αποτέλεσμα (παράδειγμα):**



## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε σε πρόσθετα χαρακτηριστικά API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Βήμα‑Βήμα](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Πώς να Κάνετε OCR Κειμένου σε Εικόνα με Γλώσσα Χρησιμοποιώντας Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Πώς να Αναγνωρίσετε Ορθογώνια Σελίδας για Αναγνώριση Κειμένου OCR στο Aspose.OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}