---
category: general
date: 2026-01-12
description: Πώς να εκτελέσετε OCR σε PDF χρησιμοποιώντας το Aspose OCR, να φορτώσετε
  το PDF OCR, να ενεργοποιήσετε τη λειτουργία OCR χειρόγραφου και να ενσωματώσετε
  ένα μοντέλο OCR Hugging Face για μεταεπεξεργασία.
draft: false
keywords:
- how to run OCR
- load pdf OCR
- handwritten OCR mode
- hugging face OCR model
language: el
og_description: Πώς να εκτελέσετε OCR σε PDF με το Aspose OCR, να ενεργοποιήσετε τη
  λειτουργία OCR χειρόγραφου και να βελτιώσετε την ακρίβεια χρησιμοποιώντας ένα μοντέλο
  OCR του Hugging Face.
og_title: Πώς να εκτελέσετε OCR σε PDF – Πλήρης οδηγός
tags:
- OCR
- Python
- Aspose
- Hugging Face
title: Πώς να εκτελέσετε OCR σε PDF – Οδηγός βήμα‑βήμα με λειτουργία χειρόγραφου
url: /el/python/general/how-to-run-ocr-on-pdfs-step-by-step-guide-with-handwritten-m/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εκτελέσετε OCR σε PDF – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να εκτελέσετε OCR** σε ένα PDF πολλαπλών γλωσσών που περιέχει ακατάστατη χειρόγραφη γραφή; Δεν είστε μόνοι. Σε πολλά πραγματικά έργα—σκεφτείτε την ψηφιοποίηση τιμολογίων ή την αρχειοθέτηση ιστορικών επιστολών—η εξαγωγή απλού κειμένου δεν αρκεί. Αυτός ο οδηγός σας δείχνει ακριβώς πώς να εκτελέσετε OCR σε PDF, να φορτώσετε PDF OCR, να μεταβείτε σε λειτουργία χειρόγραφου OCR, και στη συνέχεια να τελειοποιήσετε τα αποτελέσματα με ένα **μοντέλο OCR Hugging Face** για διορθώσεις ορθογραφίας και γραμματικής.

> **Προαπαιτούμενα**  
> • Python 3.9 ή νεότερη  
> • Άδεια Aspose OCR Cloud (ορίζεται ως μεταβλητή περιβάλλοντος)  
> • Προαιρετικά: GPU συμβατό με CUDA για ταχύτερη εκτέλεση  

---

## Τι Καλύπτει Αυτός ο Οδηγός

- Ενεργοποίηση της άδειας Aspose OCR από το περιβάλλον  
- Φόρτωση PDF με `load_pdf OCR` και ενεργοποίηση **λειτουργίας χειρόγραφου OCR**  
- Εκτέλεση δομημένου OCR για λήψη κειμένου σε επίπεδο μπλοκ και δεδομένων γλώσσας  
- Ρύθμιση ενός **μοντέλου OCR Hugging Face** (Qwen 2.5‑3B‑Instruct) για μετα‑επεξεργασία  
- Εφαρμογή ορθογραφικού ελέγχου και διόρθωσης γραμματικής μπλοκ προς μπλοκ  
- Καθαρισμός πόρων AI για αποφυγή διαρροών μνήμης  

Αν έχετε δοκιμάσει ποτέ μια βασική μηχανή OCR και έχετε λάβει ακατανόητο κείμενο σε χειρόγραφες σημειώσεις, η σημαία “λειτουργία χειρόγραφου OCR” είναι το στοιχείο που λείπει. Και χάρη στο μοντέλο Hugging Face, θα έχετε επίσης επαγγελματικό polish χωρίς να βγείτε από το περιβάλλον Python.

![διάγραμμα ροής εκτέλεσης OCR](https://example.com/ocr-workflow.png "πώς να εκτελέσετε OCR")

*Image alt text: διάγραμμα ροής εκτέλεσης OCR*

## Βήμα 1: Εγκατάσταση Απαιτούμενων Πακέτων

Πρώτα, βεβαιωθείτε ότι το Aspose OCR Cloud SDK και η βιβλιοθήκη `transformers` είναι εγκατεστημένα. Εκτελέστε το παρακάτω στο τερματικό σας:

```bash
pip install aspose-ocr-cloud transformers huggingface-hub
```

> **Pro tip:** Εάν σκοπεύετε να χρησιμοποιήσετε επιτάχυνση GPU, εγκαταστήστε επίσης το `torch` με υποστήριξη CUDA (`pip install torch==2.2.0+cu121 -f https://download.pytorch.org/whl/torch_stable.html`).

## Βήμα 2: Ενεργοποίηση της Άδειας Aspose OCR

Η ενεργοποίηση της άδειας από μια μεταβλητή περιβάλλοντος κρατά το κλειδί σας μακριά από τον έλεγχο έκδοσης. Ορίστε το `ASPOSE_OCR_LICENSE` στο κέλυφος σας, μετά καλέστε το `activate_from_env()`:

```python
import asposeocrcloud as ocr

# Pull the license string from the ASPOSE_OCR_LICENSE environment variable
ocr.activate_from_env()
```

> **Γιατί είναι σημαντικό:** Χωρίς έγκυρη άδεια το SDK επιστρέφει σε λειτουργία δοκιμής που περιορίζει τον αριθμό σελίδων και απενεργοποιεί τη χρήση GPU.

## Βήμα 3: Αρχικοποίηση του Μηχανήματος OCR σε Λειτουργία Χειρόγραφου

Δημιουργούμε ένα `OcrEngine`, ενεργοποιούμε το GPU (αν υπάρχει) και ζητάμε ρητά **λειτουργία χειρόγραφου OCR**. Αυτή η λειτουργία τροποποιεί το υποκείμενο νευρωνικό δίκτυο ώστε να χειρίζεται καλύτερα τις καμπυλωτές γραμμές.

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Enable GPU acceleration – optional but speeds up large PDFs dramatically
ocr_engine.set_use_gpu(True)

# Switch to handwritten recognition mode for better accuracy on cursive text
ocr_engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)
```

> **Σημείωση:** Εάν δεν έχετε GPU, το `set_use_gpu(False)` λειτουργεί κανονικά· η μηχανή θα επιστρέψει σε CPU.

## Βήμα 4: Φορτώστε το PDF σας και Εκτελέστε Δομημένο OCR

Τώρα φορτώνουμε πραγματικά **PDF OCR**. Η μέθοδος `load_image` δέχεται PDF, TIFF, JPG κ.λπ. Το δομημένο OCR επιστρέφει μπλοκ που περιέχουν τόσο το ακατέργαστο κείμενο όσο και τη γλώσσα που εντοπίστηκε.

```python
# Replace the path with your own PDF location
pdf_path = "YOUR_DIRECTORY/multilingual_handwritten.pdf"
ocr_engine.load_image(pdf_path)

# Perform structured OCR – returns a hierarchy of blocks
structured_result = ocr_engine.recognize_structured()
```

Η λίστα `structured_result.blocks` μπορεί να φαίνεται ως εξής (συνοπτικά):

```python
[
    Block(text="Bonjour le monde", language="fr"),
    Block(text="Hello world", language="en"),
    Block(text="こんにちは世界", language="ja")
]
```

## Βήμα 5: Διαμόρφωση Μοντέλου OCR Hugging Face για Μετα‑Επεξεργασία

Θα χρησιμοποιήσουμε το μοντέλο **Qwen 2.5‑3B‑Instruct** από το Hugging Face, ποσοτικοποιημένο σε `int8` για μικρό αποτύπωμα μνήμης. Η περιτύλιξη `AsposeAIModelConfig` ενημερώνει τον AI μετα‑επεξεργαστή Aspose πώς να κατεβάσει και να τρέξει το μοντέλο.

```python
from asposeocrcloud import AsposeAI, AsposeAIModelConfig

model_cfg = AsposeAIModelConfig(
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=25,                # Number of transformer layers to keep on GPU
    allow_auto_download="true"   # Auto‑download the model if not cached
)

spell_corrector = AsposeAI()
spell_corrector.set_post_processor("spell_corrector", model_cfg)
```

> **Γιατί αυτό το μοντέλο;** Το Qwen 2.5‑3B‑Instruct ισορροπεί ταχύτητα και ποιότητα. Η ποσοτικοποίηση `int8` μειώνει τη χρήση RAM σε ~4 GB, καθιστώντας το εφικτό στα περισσότερα σύγχρονα laptops.

## Βήμα 6: Εφαρμογή Ορθογραφικού Ελέγχου Μπλοκ προς Μπλοκ

Διατρέχουμε κάθε μπλοκ OCR, το περνάμε στον AI μετα‑επεξεργαστή και εκτυπώνουμε το διορθωμένο κείμενο μαζί με τη γλώσσα που εντοπίστηκε. Αυτό είναι η καρδιά της **pipeline load PDF OCR → post‑process**.

```python
for block in structured_result.blocks:
    # Run the correction; `run_postprocessor` returns an object with a .text attribute
    corrected = spell_corrector.run_postprocessor(block)
    print(f"[{block.language}] {corrected.text}")
```

### Αναμενόμενο Αποτέλεσμα

```
[fr] Bonjour le monde
[en] Hello world
[ja] こんにちは世界
```

Εάν το αρχικό OCR είχε ορθογραφικά λάθη όπως “Helllo wrold”, το μοντέλο θα παράγει τη διορθωμένη έκδοση.

## Βήμα 7: Καθαρισμός Πόρων AI

Πάντα ελευθερώστε τη μνήμη GPU όταν τελειώσετε. Η κλήση `free_resources()` αποφορτώνει το μοντέλο και καθαρίζει την κρυφή μνήμη CUDA.

```python
spell_corrector.free_resources()
```

## Συνηθισμένα Πιθανά Προβλήματα & Πώς να τα Αποφύγετε

| Πρόβλημα | Συμπτωμα | Διόρθωση |
|----------|----------|----------|
| **GPU δεν εντοπίστηκε** | `set_use_gpu(True)` πέφτει σιωπηλά σε CPU | Επαληθεύστε τους οδηγούς CUDA (`nvidia-smi`) και εγκαταστήστε το σωστό `torch` wheel |
| **Αποτυχία λήψης μοντέλου** | `allow_auto_download` προκαλεί σφάλμα δικτύου | Βεβαιωθείτε ότι επιτρέπεται η εξερχόμενη κίνηση HTTPS, ή κατεβάστε χειροκίνητα το αρχείο GGUF και ορίστε το `hugging_face_repo_id` στην τοπική διαδρομή |
| **Η χειρόγραφη κείμενο εξακολουθεί να είναι ακατάληπτο** | Χαμηλές βαθμολογίες εμπιστοσύνης στο `structured_result` | Αυξήστε το `set_recognition_mode` σε `HANDWRITTEN` (ήδη γίνει) και εξετάστε την προεπεξεργασία του PDF με ενίσχυση εικόνας (`opencv`) πριν το OCR |
| **Έλλειψη μνήμης στο GPU** | `RuntimeError: CUDA out of memory` | Μειώστε το `gpu_layers` (π.χ., σε 10) ή μεταβείτε σε CPU inference (`set_use_gpu(False)`) |

## Επέκταση της Ροής Εργασίας

- **Επεξεργασία παρτίδας:** Τυλίξτε ολόκληρο το script σε μια συνάρτηση που δέχεται λίστα διαδρομών PDF και γράφει το διορθωμένο αποτέλεσμα σε ξεχωριστά αρχεία `.txt`.  
- **Προσαρμοστικά λεξιλόγια:** Εάν ο τομέας σας χρησιμοποιεί εξειδικευμένη ορολογία (π.χ., ιατρικά ακρωνύμια), κάντε fine‑tune το μοντέλο Hugging Face με ένα μικρό σύνολο δεδομένων.  
- **Εναλλακτικά μοντέλα:** Αντικαταστήστε το `Qwen/Qwen2.5-3B-Instruct-GGUF` με το `mistralai/Mistral-7B-Instruct-v0.2` εάν χρειάζεστε μεγαλύτερο παράθυρο συμφραζομένων.  

## Συμπέρασμα

Τώρα ξέρετε **πώς να εκτελέσετε OCR** σε PDF, να φορτώσετε PDF OCR, να ενεργοποιήσετε **λειτουργία χειρόγραφου OCR**, και να βελτιώσετε την ακρίβεια με ένα **μοντέλο OCR Hugging Face**. Το πλήρες script—ενεργοποίηση άδειας, μηχανή με υποστήριξη GPU, δομημένο OCR, AI μετα‑επεξεργασία και καθαρισμό—καλύπτει κάθε βήμα που ένας προγραμματιστής συνήθως ρωτά, από το “τι γίνεται αν δεν έχω GPU?” μέχρι το “πώς ελευθερώνω τους πόρους;”.  

Δοκιμάστε το με τα δικά σας έγγραφα, πειραματιστείτε με διαφορετικά μοντέλα, ή ενσωματώστε τη διαδικασία σε μια μεγαλύτερη υπηρεσία επεξεργασίας εγγράφων. Ο ουρανός είναι το όριο μόλις κυριαρχήσετε αυτόν τον συνδυασμό Aspose OCR και Hugging Face AI.

**Επόμενα Βήματα**

- Δοκιμάστε την ίδια ροή εργασίας σε σαρωμένες εικόνες (`.png`, `.jpg`) για να δείτε πώς προσαρμόζεται η μηχανή.  
- Εξερευνήστε τις δυνατότητες **layout analysis** του Aspose OCR για εξαγωγή πινάκων.  
- Βυθιστείτε περισσότερο στις τεχνικές ποσοτικοποίησης του Hugging Face για να μειώσετε ακόμη περισσότερο το μέγεθος του μοντέλου.  

Καλή επιτυχία με το OCR!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}