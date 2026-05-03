---
category: general
date: 2026-05-03
description: Μάθημα Python OCR που δείχνει πώς να φορτώνετε αρχεία εικόνας PNG, να
  αναγνωρίζετε κείμενο από την εικόνα και δωρεάν πόρους AI για ομαδική επεξεργασία
  OCR.
draft: false
keywords:
- python ocr tutorial
- batch ocr processing
- free ai resources
- load png image
- recognize text from image
language: el
og_description: Το σεμινάριο Python OCR σας καθοδηγεί στη φόρτωση εικόνων PNG, στην
  αναγνώριση κειμένου από την εικόνα και στη διαχείριση δωρεάν πόρων AI για επεξεργασία
  OCR σε παρτίδες.
og_title: Python OCR Tutorial – Γρήγορη ομαδική OCR με δωρεάν πόρους AI
tags:
- OCR
- Python
- AI
title: Python OCR Tutorial – Εύκολη μαζική επεξεργασία OCR
url: /el/python/general/python-ocr-tutorial-batch-ocr-processing-made-easy/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Οδηγός Python OCR – Εύκολη Επεξεργασία OCR σε Παρτίδες

Κάποτε χρειάστηκε ένας **python ocr tutorial** που πραγματικά να σας επιτρέπει να τρέχετε OCR σε δεκάδες αρχεία PNG χωρίς να τρελαίνεστε; Δεν είστε μόνοι. Σε πολλά πραγματικά έργα πρέπει να **load png image** αρχεία, να τα δίνετε σε μια μηχανή, και μετά να καθαρίζετε τους πόρους AI όταν τελειώσετε.  

Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που δείχνει ακριβώς πώς να **recognize text from image** αρχεία, να τα επεξεργαστείτε σε παρτίδες, και να ελευθερώσετε τη μνήμη AI. Στο τέλος θα έχετε ένα αυτόνομο script που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο—χωρίς περιττά πρόσθετα, μόνο τα ουσιώδη.

## Τι Θα Χρειαστείτε

- Python 3.10 ή νεότερη (η σύνταξη που χρησιμοποιείται εδώ βασίζεται σε f‑strings και type hints)  
- Μια βιβλιοθήκη OCR που εκθέτει μέθοδο `engine.recognize` – για σκοπούς επίδειξης θα υποθέσουμε ένα φανταστικό πακέτο `aocr`, αλλά μπορείτε να το αντικαταστήσετε με Tesseract, EasyOCR κ.λπ.  
- Το βοηθητικό module `ai` που φαίνεται στο απόσπασμα κώδικα (διαχειρίζεται την αρχικοποίηση του μοντέλου και τον καθαρισμό πόρων)  
- Έναν φάκελο γεμάτο PNG αρχεία που θέλετε να επεξεργαστείτε  

Αν δεν έχετε εγκατεστημένα τα `aocr` ή `ai`, μπορείτε να τα μιμηθείτε με stubs – δείτε την ενότητα «Optional Stubs» στο τέλος.

## Βήμα 1: Αρχικοποίηση της Μηχανής AI (Free AI Resources)

Πριν δώσετε οποιαδήποτε εικόνα στη γραμμή OCR, το υποκείμενο μοντέλο πρέπει να είναι έτοιμο. Η αρχικοποίηση μόνο μία φορά εξοικονομεί μνήμη και επιταχύνει τις εργασίες παρτίδας.

```python
# step_1_initialize.py
import ai                # hypothetical helper that wraps the AI model
import aocr               # OCR library

def init_engine(config_path: str = "config.yaml"):
    """
    Initialize the AI engine if it hasn't been set up yet.
    This uses free AI resources – the engine will be released later.
    """
    if not ai.is_initialized():
        ai.initialize(config_path)   # auto‑initialize with the provided configuration
    else:
        print("Engine already initialized.")
```

**Γιατί είναι σημαντικό:**  
Η κλήση του `ai.initialize` επανειλημμένα για κάθε εικόνα θα κατανέμιζε μνήμη GPU ξανά‑ξανά, οδηγώντας τελικά σε κατάρρευση του script. Με τον έλεγχο `ai.is_initialized()` διασφαλίζουμε μία μόνο κατανομή – αυτό είναι η αρχή του «Free AI resources».

## Βήμα 2: Φόρτωση Αρχείων PNG για Επεξεργασία OCR σε Παρτίδες

Τώρα συγκεντρώνουμε όλα τα PNG αρχεία που θέλουμε να τρέξουμε μέσω OCR. Η χρήση του `pathlib` κρατά τον κώδικα ανεξάρτητο από το λειτουργικό σύστημα.

```python
# step_2_load_images.py
from pathlib import Path
from typing import List

def collect_png_paths(directory: str) -> List[Path]:
    """
    Scan `directory` and return a list of Path objects pointing to PNG files.
    """
    base_path = Path(directory)
    if not base_path.is_dir():
        raise NotADirectoryError(f"'{directory}' is not a valid folder.")
    
    png_files = sorted(base_path.glob("*.png"))
    if not png_files:
        raise FileNotFoundError("No PNG images found in the specified directory.")
    
    print(f"Found {len(png_files)} PNG image(s) to process.")
    return png_files
```

**Ακρόαση περιπτώσεων:**  
Αν ο φάκελος περιέχει αρχεία που δεν είναι PNG (π.χ. JPEG), θα αγνοηθούν, αποτρέποντας το `engine.recognize` από το να «πνίγει» σε μη υποστηριζόμενη μορφή.

## Βήμα 3: Εκτέλεση OCR σε Κάθε Εικόνα και Εφαρμογή Μετα‑επεξεργασίας

Με τη μηχανή έτοιμη και τη λίστα αρχείων προετοιμασμένη, μπορούμε να διασχίσουμε τις εικόνες, να εξάγουμε ακατέργαστο κείμενο, και να το περάσουμε σε μετα‑επεξεργαστή που καθαρίζει κοινά artefacts OCR (όπως ανεπιθύμητες αλλαγές γραμμής).

```python
# step_3_ocr_batch.py
import aocr
import ai
from pathlib import Path
from typing import List

def ocr_batch(image_paths: List[Path]) -> List[str]:
    """
    Perform OCR on each PNG image and return a list of cleaned strings.
    """
    results = []
    for image_path in image_paths:
        # Load the image – aocr.Image.load abstracts away Pillow/OpenCV details
        img = aocr.Image.load(str(image_path))
        
        # Recognize raw text
        raw_text = engine.recognize(img)
        
        # Refine the raw OCR output using the AI post‑processor
        cleaned_text = ai.run_postprocessor(raw_text)
        results.append(cleaned_text)
        
        print(f"Processed {image_path.name}: {len(cleaned_text)} characters extracted.")
    
    return results
```

**Γιατί χωρίζουμε τη φόρτωση από την αναγνώριση:**  
Η `aocr.Image.load` μπορεί να κάνει lazy decoding, κάτι που είναι γρηγορότερο για μεγάλες παρτίδες. Η ρητή φάση φόρτωσης κάνει επίσης εύκολο το swap σε διαφορετική βιβλιοθήκη εικόνας αν αργότερα χρειαστεί να υποστηρίξετε JPEG ή TIFF.

## Βήμα 4: Καθαρισμός – Ελευθέρωση Πόρων AI μετά την Παρτίδα

Μόλις ολοκληρωθεί η παρτίδα, πρέπει να απελευθερώσουμε το μοντέλο για να αποφύγουμε διαρροές μνήμης, ειδικά σε μηχανές με GPU.

```python
# step_4_cleanup.py
import ai

def release_resources():
    """
    Free any allocated AI resources. Safe to call multiple times.
    """
    if ai.is_initialized():
        ai.free_resources()
        print("AI resources have been released.")
    else:
        print("No AI resources were allocated.")
```

## Συνδυασμός Όλων – Το Πλήρες Script

Παρακάτω υπάρχει ένα μοναδικό αρχείο που ενώνει τα τέσσερα βήματα σε μια συνεκτική ροή εργασίας. Αποθηκεύστε το ως `batch_ocr.py` και τρέξτε το από τη γραμμή εντολών.

```python
# batch_ocr.py
"""
Python OCR tutorial – end‑to‑end batch OCR processing.
Loads PNG images, runs OCR, post‑processes results, and frees AI resources.
"""

import sys
from pathlib import Path
import ai
import aocr

# ----------------------------------------------------------------------
# Helper functions (copied from the steps above)
# ----------------------------------------------------------------------
def init_engine(cfg: str = "config.yaml"):
    if not ai.is_initialized():
        ai.initialize(cfg)
    else:
        print("Engine already initialized.")

def collect_png_paths(directory: str):
    base_path = Path(directory)
    if not base_path.is_dir():
        raise NotADirectoryError(f"'{directory}' is not a valid folder.")
    png_files = sorted(base_path.glob("*.png"))
    if not png_files:
        raise FileNotFoundError("No PNG images found in the specified directory.")
    print(f"Found {len(png_files)} PNG image(s) to process.")
    return png_files

def ocr_batch(image_paths):
    results = []
    for image_path in image_paths:
        img = aocr.Image.load(str(image_path))
        raw_text = engine.recognize(img)
        cleaned_text = ai.run_postprocessor(raw_text)
        results.append(cleaned_text)
        print(f"Processed {image_path.name}: {len(cleaned_text)} characters.")
    return results

def release_resources():
    if ai.is_initialized():
        ai.free_resources()
        print("AI resources released.")
    else:
        print("No resources to release.")

# ----------------------------------------------------------------------
# Main execution block
# ----------------------------------------------------------------------
if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <directory-with-png>")
        sys.exit(1)

    image_dir = sys.argv[1]

    try:
        init_engine()
        png_paths = collect_png_paths(image_dir)
        texts = ocr_batch(png_paths)

        # Optional: write results to a single text file
        output_file = Path("ocr_results.txt")
        with output_file.open("w", encoding="utf-8") as f:
            for path, txt in zip(png_paths, texts):
                f.write(f"--- {path.name} ---\n")
                f.write(txt + "\n\n")
        print(f"All results saved to {output_file.resolve()}")
    finally:
        release_resources()
```

### Αναμενόμενο Αποτέλεσμα

Η εκτέλεση του script σε φάκελο με τρία PNG μπορεί να εμφανίσει:

```
Engine already initialized.
Found 3 PNG image(s) to process.
Processed invoice1.png: 452 characters.
Processed receipt2.png: 317 characters.
Processed flyer3.png: 689 characters.
All results saved to /home/user/ocr_results.txt
AI resources released.
```

Το αρχείο `ocr_results.txt` θα περιέχει έναν σαφή διαχωριστή για κάθε εικόνα, ακολουθούμενο από το καθαρισμένο κείμενο OCR.

## Optional Stubs για aocr & ai (Αν Δεν Έχετε Πραγματικά Πακέτα)

Αν θέλετε απλώς να δοκιμάσετε τη ροή χωρίς βαριές βιβλιοθήκες OCR, μπορείτε να δημιουργήσετε ελάχιστα mock modules:

```python
# aocr/__init__.py
class Image:
    @staticmethod
    def load(path):
        return f"ImageObject({path})"

def dummy_recognize(image):
    return "Raw OCR output for " + str(image)

engine = type("Engine", (), {"recognize": dummy_recognize})()
```

```python
# ai/__init__.py
_state = {"initialized": False}

def is_initialized():
    return _state["initialized"]

def initialize(cfg):
    print(f"Initializing AI engine with {cfg}")
    _state["initialized"] = True

def run_postprocessor(text):
    # Very naive cleanup: strip extra spaces
    return " ".join(text.split())

def free_resources():
    print("Freeing AI resources")
    _state["initialized"] = False
```

Τοποθετήστε αυτούς τους φακέλους δίπλα στο `batch_ocr.py` και το script θα τρέξει, εκτυπώνοντας ψεύτικα αποτελέσματα.

## Pro Tips & Συνηθισμένα Πιθανά Σφάλματα

- **Αιχμές μνήμης:** Αν επεξεργάζεστε χιλιάδες PNG υψηλής ανάλυσης, σκεφτείτε να τα μειώσετε πριν το OCR. Η `aocr.Image.load` συχνά δέχεται όρισμα `max_size`.  
- **Διαχείριση Unicode:** Πάντα ανοίγετε το αρχείο εξόδου με `encoding="utf-8"`· οι μηχανές OCR μπορούν να εκπονήσουν μη‑ASCII χαρακτήρες.  
- **Παράλληλη εκτέλεση:** Για OCR που περιορίζεται από CPU, μπορείτε να τυλίξετε το `ocr_batch` σε `concurrent.futures.ThreadPoolExecutor`. Θυμηθείτε όμως να διατηρείτε μία μόνο παρουσία `ai` – η δημιουργία πολλών νημάτων που καλούν `ai.initialize` αντιστέκεται στον στόχο «Free AI resources».  
- **Ανθεκτικότητα σε σφάλματα:** Τυλίξτε τον βρόχο ανά‑εικόνα σε `try/except` ώστε ένα κατεστραμμένο PNG να μην διακόψει όλη τη παρτίδα.

## Συμπέρασμα

Τώρα έχετε έναν **python ocr tutorial** που δείχνει πώς να **load png image** αρχεία, να εκτελείτε **batch OCR processing**, και να διαχειρίζεστε υπεύθυνα **free AI resources**. Το πλήρες, εκτελέσιμο παράδειγμα δείχνει ακριβώς πώς να **recognize text from image** αντικείμενα και να καθαρίζετε μετά, ώστε να το αντιγράψετε‑επικολλήσετε στα δικά σας έργα χωρίς να ψάχνετε για ελλείποντα κομμάτια.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να αντικαταστήσετε τα stub `aocr` και `ai` με πραγματικές βιβλιοθήκες όπως `pytesseract` και `torchvision`. Μπορείτε επίσης να επεκτείνετε το script ώστε να εξάγει JSON, να στέλνει αποτελέσματα σε βάση δεδομένων, ή να ενσωματώνεται με cloud storage bucket. Ο ουρανός είναι το όριο—καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}