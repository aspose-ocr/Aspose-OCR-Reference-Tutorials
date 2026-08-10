---
category: general
date: 2026-06-22
description: Αναγνωρίστε κείμενο από αρχεία PNG χρησιμοποιώντας το Aspose OCR στην
  Python. Μάθετε την ομαδική OCR εικόνων και ορίστε επίπεδα GPU για γρήγορη επεξεργασία.
draft: false
keywords:
- recognize text from png
- batch ocr images
- set gpu layers
- Aspose OCR Python
- GPU acceleration OCR
language: el
og_description: αναγνωρίστε κείμενο από αρχεία PNG με το Aspose OCR σε Python. Αυτός
  ο οδηγός δείχνει πώς να κάνετε ομαδική αναγνώριση OCR εικόνων και να ορίσετε επίπεδα
  GPU για ταχύτητα.
og_title: Αναγνώριση κειμένου από PNG – Βήμα‑βήμα οδηγός Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: recognize text from png files using Aspose OCR in Python. Learn batch
    OCR images and set GPU layers for fast processing.
  headline: recognize text from png – Complete Guide with Aspose OCR & AI
  type: TechArticle
- description: recognize text from png files using Aspose OCR in Python. Learn batch
    OCR images and set GPU layers for fast processing.
  name: recognize text from png – Complete Guide with Aspose OCR & AI
  steps:
  - name: '**Model download fails** – Ensure your environment can reach `https://huggingface.co`.
      A corporate proxy may need configuration (`https_proxy` env var).'
    text: '**Model download fails** – Ensure your environment can reach `https://huggingface.co`.
      A corporate proxy may need configuration (`https_proxy` env var).'
  - name: '**GPU not detected** – Verify that the `torch` library (installed as a
      dependency) sees the GPU: `import torch; print(torch.cuda.is_available())`.
      If it returns `False`, install the CUDA‑compatible PyTorch wheel.'
    text: '**GPU not detected** – Verify that the `torch` library (installed as a
      dependency) sees the GPU: `import torch; print(torch.cuda.is_available())`.
      If it returns `False`, install the CUDA‑compatible PyTorch wheel.'
  - name: '**Incorrect image path** – `Path.glob("*.png")` is case‑sensitive on Linux.
      Use `*.PNG` or `*.png` accordingly, or add `pathlib.Path(...).rglob("*.[pP][nN][gG]")`
      for safety.'
    text: '**Incorrect image path** – `Path.glob("*.png")` is case‑sensitive on Linux.
      Use `*.PNG` or `*.png` accordingly, or add `pathlib.Path(...).rglob("*.[pP][nN][gG]")`
      for safety.'
  - name: '**Post‑processor over‑corrects** – The simple replace may turn legitimate
      “0” characters into “o”. Test on a representative sample and adjust the logic
      as needed.'
    text: '**Post‑processor over‑corrects** – The simple replace may turn legitimate
      “0” characters into “o”. Test on a representative sample and adjust the logic
      as needed.'
  type: HowTo
tags:
- OCR
- Python
- AsposeAI
title: Αναγνώριση κειμένου από PNG – Πλήρης Οδηγός με Aspose OCR & AI
url: /el/python/general/recognize-text-from-png-complete-guide-with-aspose-ocr-ai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# αναγνώριση κειμένου από png – Πλήρης Οδηγός Aspose OCR & AI

Έχετε ποτέ χρειαστεί να **αναγνωρίσετε κείμενο από png** αρχεία αλλά να μπλέξετε με τις λεπτομέρειες της εγκατάστασης; Δεν είστε μόνοι. Είτε ψηφιοποιείτε αποδείξεις, σκανάρετε φόρμες, είτε μετατρέπετε στιγμιότυπα οθόνης σε αναζητήσιμο κείμενο, η εξοικείωση με την επεξεργασία batch OCR εικόνων σε Python μπορεί να σας εξοικονομήσει ώρες.

Σε αυτόν τον οδηγό θα περάσουμε από ένα έτοιμο παράδειγμα που όχι μόνο **αναγνωρίζει κείμενο από png**, αλλά δείχνει επίσης πώς να **ρυθμίσετε τις GPU layers** για αισθητή αύξηση ταχύτητας. Στο τέλος θα έχετε ένα αυτόνομο script, μια σαφή εξήγηση κάθε βήματος, και μια σειρά πρακτικών συμβουλών που μπορείτε να αντιγράψετε‑επικολλήσετε στα δικά σας έργα.

## Τι Καλύπτει Αυτός ο Οδηγός

- Εγκατάσταση των πακέτων Aspose OCR και Aspose AI για Python  
- Διαμόρφωση ενός μοντέλου AI με αυτόματη λήψη από το Hugging Face  
- Δημιουργία ενός μικρού post‑processor που διορθώνει τα πιο συχνά OCR τυπογραφικά λάθη  
- Εκτέλεση βρόχου **batch OCR images** σε ολόκληρο φάκελο PNG  
- Χρήση της επιλογής **set GPU layers** για αξιοποίηση της κάρτας γραφικών σας  
- Ασφαλής εκκαθάριση πόρων μετά την επεξεργασία  

Καμία εξωτερική υπηρεσία, καμία κρυφή μαγεία—απλώς καθαρός κώδικας Python που μπορείτε να τοποθετήσετε σε ένα αρχείο `.py` και να τρέξετε.

![Diagram of recognize text from png workflow](workflow.png){alt="recognize text from png workflow diagram"}

## Προαπαιτούμενα

| Απαίτηση | Γιατί είναι σημαντική |
|----------|-----------------------|
| Python 3.8+ | Τα wheels του Aspose AI στοχεύουν πρόσφατους διερμηνείς |
| GPU συμβατό με CUDA (προαιρετικό) | Απαιτείται αν θέλετε να **ρυθμίσετε GPU layers** για επιτάχυνση |
| Πρόσβαση στο Internet στην πρώτη εκτέλεση | Το μοντέλο θα ληφθεί αυτόματα από το Hugging Face |
| `pip` εγκατεστημένο | Για λήψη των πακέτων Aspose |

Αν έχετε ήδη όλα αυτά, τέλεια—είστε έτοιμοι να ξεκινήσετε. Αν όχι, τα βήματα εγκατάστασης παρακάτω θα σας καθοδηγήσουν στα ελλιπή στοιχεία.

---

## Βήμα 1: Εγκατάσταση Πακέτων Aspose OCR και Aspose AI

Πρώτα, κατεβάστε τις βιβλιοθήκες από το PyPI. Η παρακάτω εντολή εγκαθιστά τόσο τη μηχανή OCR όσο και τον βοηθό AI με μία κίνηση.

```bash
pip install aspose-ocr aspose-ai
```

*Συμβουλή:* Χρησιμοποιήστε ένα εικονικό περιβάλλον (`python -m venv .venv`) ώστε τα πακέτα να παραμείνουν απομονωμένα από την παγκόσμια εγκατάσταση του Python.

---

## Βήμα 2: Δημιουργία και Διαμόρφωση του Aspose AI Instance

Το στοιχείο AI τροφοδοτεί τη λειτουργία “intelligent” της μηχανής OCR. Θα το κατευθύνουμε προς το μοντέλο `Qwen/Qwen2.5-3B-Instruct-GGUF`, θα ζητήσουμε αυτόματη λήψη αν λείπει, και θα **ρυθμίσουμε GPU layers** σε 30 (μπορείτε να το προσαρμόσετε αργότερα).

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Initialize the AI wrapper
ai = AsposeAI()

# Build a model configuration
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",                     # Grab the model automatically
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # Smaller footprint, still accurate
    directory_model_path="YOUR_DIRECTORY/ai_models", # Where the model will live
    gpu_layers=30                                   # <-- set gpu layers for GPU acceleration
)

# Apply the configuration and spin up the model
ai.initialize(model_cfg)
```

**Γιατί είναι σημαντικό:**  
- `allow_auto_download` αφαιρεί το χειροκίνητο βήμα λήψης ενός μοντέλου ~2 GB.  
- `gpu_layers=30` λέει στον υποκείμενο transformer να τρέξει τις πρώτες 30 στρώσεις στην GPU, μειώνοντας δραστικά το χρόνο εκτέλεσης όταν υπάρχει συμβατή GPU.  
- Η ποσοτικοποίηση `int8` διατηρεί τη χρήση μνήμης χαμηλή χωρίς μεγάλη απώλεια ακρίβειας.

---

## Βήμα 3: Ορισμός Απλού Post‑Processor για Διόρθωση Σφαλμάτων OCR

Το OCR δεν είναι τέλειο—ιδιαίτερα σε PNG χαμηλής ανάλυσης. Μια γρήγορη λύση είναι η αντικατάσταση χαρακτήρων που διαβάζονται λανθασμένα. Η παρακάτω συνάρτηση αντικαθιστά το “0” με “o” και το “1” με “l”, ένα μοτίβο που βλέπουμε συχνά σε σαρωμένα τιμολόγια.

```python
def fix_common_errors(text, **_):
    """
    Post‑processor that corrects typical OCR mis‑recognitions.
    Feel free to extend this with regexes or custom dictionaries.
    """
    return text.replace("0", "o").replace("1", "l")
```

Θα το συνδέσουμε με το AI instance στο επόμενο βήμα ώστε κάθε αποτέλεσμα αναγνώρισης να περνάει αυτόματα από αυτόν.

---

## Βήμα 4: Σύνδεση του Post‑Processor με τη Μηχανή OCR

Τώρα ενώνουμε τα πάντα: τη μηχανή OCR, το μοντέλο AI, και τον post‑processor.

```python
import ocr  # Aspose OCR module

# Attach the post‑processor
ai.set_post_processor(fix_common_errors, {})

# Spin up the OCR engine and bind the AI
engine = ocr.OcrEngine()
engine.set_ai(ai)
```

**Τι συμβαίνει στο παρασκήνιο;**  
Η `OcrEngine` αναθέτει το βαρέως φορτίου έργο στο μοντέλο AI που διαμορφώσατε. Αφού το μοντέλο επιστρέψει το ακατέργαστο κείμενο, το Aspose καλεί τη `fix_common_errors` για να καθαρίσει το αποτέλεσμα πριν το δείτε.

---

## Βήμα 5: Batch OCR Images – Επεξεργασία Όλων των PNG σε Φάκελο

Αυτή είναι η καρδιά του οδηγού: ένας βρόχος που διασχίζει έναν κατάλογο, φορτώνει κάθε `.png`, τρέχει OCR, και εκτυπώνει το καθαρισμένο αποτέλεσμα. Αυτό το μοτίβο είναι ο κανονικός τρόπος για **batch OCR images** αποδοτικά.

```python
from pathlib import Path

# Replace with the folder that holds your PNG files
image_folder = Path("YOUR_DIRECTORY")

# Iterate over every PNG file in the folder
for img_path in image_folder.glob("*.png"):
    # Load the image into the engine
    engine.load_image(str(img_path))

    # Perform recognition
    result = engine.recognize()

    # Output the filename and the extracted text
    print(f"[{img_path.name}] → {result.text}")
```

**Αναμενόμενο αποτέλεσμα** (παράδειγμα για απόδειξη):

```
[receipt_001.png] → Total amount: $23.45
[receipt_002.png] → Item: Coffee, Price: $3.50
```

Αν έχετε δεκάδες ή εκατοντάδες αρχεία, αυτός ο βρόχος θα τα διαχειριστεί διαδοχικά, επαναχρησιμοποιώντας το ίδιο AI instance για να αποφύγετε το κόστος επαναφόρτωσης του μοντέλου.

---

## Βήμα 6: Εκκαθάριση – Απελευθέρωση Πόρων και Καταστροφή της Μηχανής

Όταν τελειώσετε, είναι καλή πρακτική να απελευθερώσετε τη μνήμη GPU και άλλους εγγενείς πόρους. Το Aspose παρέχει ρητές μεθόδους γι’ αυτό.

```python
# Release the AI model and any GPU buffers
ai.free_resources()

# Dispose of the OCR engine to close native handles
engine.dispose()
```

Η παράλειψη αυτού του βήματος μπορεί να αφήσει μνήμη GPU δεσμευμένη, προκαλώντας σφάλματα out‑of‑memory στην επόμενη εκτέλεση του script.

---

## Bonus: Ρύθμιση GPU Layers για Διάφορο Υλικό

Η τιμή `gpu_layers` που ορίσατε νωρίτερα είναι ένα καλό σημείο εκκίνησης για πολλές σύγχρονες GPU, αλλά ίσως χρειαστεί να την προσαρμόσετε:

| Μνήμη GPU (GB) | Προτεινόμενη `gpu_layers` |
|----------------|---------------------------|
| 4 GB ή λιγότερο | 10‑15 |
| 6‑8 GB | 20‑30 |
| 12 GB+ | 35‑45 (ή περισσότερο) |

Αν υπερβείτε τη μνήμη της GPU, η μηχανή θα επιστρέψει αυτόματα σε CPU για τις υπόλοιπες στρώσεις, οπότε δεν θα καταρρεύσει—απλώς θα είναι πιο αργή. Πειραματιστείτε και παρακολουθήστε τη χρήση με `nvidia‑smi`.

---

## Συνηθισμένα Πιθανά Σφάλματα & Πώς να τα Αποφύγετε

1. **Αποτυχία λήψης μοντέλου** – Βεβαιωθείτε ότι το περιβάλλον σας μπορεί να προσεγγίσει το `https://huggingface.co`. Ένας εταιρικός proxy μπορεί να απαιτεί ρύθμιση (`https_proxy` μεταβλητή).  
2. **Δεν εντοπίζεται η GPU** – Επαληθεύστε ότι η βιβλιοθήκη `torch` (εγκατεστημένη ως εξάρτηση) βλέπει την GPU: `import torch; print(torch.cuda.is_available())`. Αν επιστρέψει `False`, εγκαταστήστε το wheel του PyTorch συμβατό με CUDA.  
3. **Λάθος διαδρομή εικόνας** – `Path.glob("*.png")` είναι case‑sensitive σε Linux. Χρησιμοποιήστε `*.PNG` ή `*.png` ανάλογα, ή προσθέστε `pathlib.Path(...).rglob("*.[pP][nN][gG]")` για ασφάλεια.  
4. **Ο post‑processor διορθώνει υπερβολικά** – Η απλή αντικατάσταση μπορεί να μετατρέψει έγκυρους χαρακτήρες “0” σε “o”. Δοκιμάστε σε αντιπροσωπευτικό δείγμα και προσαρμόστε τη λογική όπως χρειάζεται.

---

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Copy‑Paste)

```python
# recognize_text_from_png_batch.py
# -------------------------------------------------
# Author: Your Name
# Date:   2026‑06‑22
# -------------------------------------------------
from pathlib import Path
import ocr                      # Aspose OCR module
from aspose_ai import AsposeAI, AsposeAIModelConfig

# ----- Step 1: AI configuration -----
ai = AsposeAI()
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    directory_model_path="YOUR_DIRECTORY/ai_models",
    gpu_layers=30               # <-- set gpu layers
)
ai.initialize(model_cfg)

# ----- Step 2: Post‑processor -----
def fix_common_errors(text, **_):
    """Replace typical OCR mis‑reads."""
    return text.replace("0", "o").replace("1", "l")

ai.set_post_processor(fix_common_errors, {})

# ----- Step 3: OCR engine -----
engine = ocr.OcrEngine()
engine.set_ai(ai)

# ----- Step 4: Batch processing -----
image_folder = Path("YOUR_DIRECTORY")
for img_path in image_folder.glob("*.png"):
    engine.load_image(str(img_path))
    result = engine.recognize()
    print(f"[{img_path.name}] → {result.text}")

# ----- Step 5: Cleanup -----
ai.free_resources()
engine.dispose()
```

Τρέξτε το με:

```bash
python recognize_text_from_png_batch.py
```

Θα πρέπει να δείτε κάθε όνομα αρχείου PNG ακολουθούμενο από το εξαγόμενο κείμενο, ακριβώς όπως παρουσιάστηκε νωρίτερα.

---

## Συμπέρασμα

Μόλις διασχίσαμε μια πλήρη, έτοιμη για παραγωγή ροή εργασίας για **αναγνώριση κειμένου από png** αρχεία χρησιμοποιώντας Aspose OCR και Aspose AI σε Python. Συγκεντρώνοντας τα βήματα σε ένα καθαρό script, μπορείτε εύκολα να **batch OCR images**, και χάρη στην επιλογή `set gpu layers`


## Τι Πρέπει να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}