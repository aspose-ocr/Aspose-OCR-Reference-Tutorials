---
category: general
date: 2026-06-25
description: Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας Aspose OCR και AI. Μάθετε
  πώς να φορτώνετε OCR εικόνας, να βελτιώνετε την ακρίβεια του OCR, να διορθώνετε
  τα σφάλματα του OCR και να ελευθερώνετε πόρους AI αποδοτικά.
draft: false
keywords:
- extract text image
- free ai resources
- improve ocr accuracy
- load image ocr
- correct OCR errors
language: el
og_description: Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας Aspose OCR και AI. Αυτό
  το σεμινάριο δείχνει πώς να φορτώσετε OCR εικόνας, να βελτιώσετε την ακρίβεια του
  OCR, να διορθώσετε τα σφάλματα του OCR και να ελευθερώσετε πόρους AI.
og_title: Εξαγωγή κειμένου από εικόνα με Aspose OCR & AI – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text image using Aspose OCR and AI. Learn to load image OCR,
    improve OCR accuracy, correct OCR errors, and free AI resources efficiently.
  headline: Extract Text Image with Aspose OCR & AI – Full Step‑by‑Step Guide
  type: TechArticle
- description: Extract text image using Aspose OCR and AI. Learn to load image OCR,
    improve OCR accuracy, correct OCR errors, and free AI resources efficiently.
  name: Extract Text Image with Aspose OCR & AI – Full Step‑by‑Step Guide
  steps:
  - name: Import Aspose OCR and AI Modules
    text: 'We start by pulling in the two namespaces we’ll need: the core OCR engine
      and the AI helper that hosts the LLM.'
  - name: Create and Configure the OCR Engine (Enable GPU)
    text: Turning on GPU accelerates the pixel‑analysis phase, which can shave seconds
      off large batches.
  - name: Load the Image That Contains the Text to Be Recognized
    text: This is where we **load image OCR**. The path can be absolute or relative;
      just make sure the file exists.
  - name: Perform OCR and Obtain the Raw Extracted Text
    text: Now we actually **extract text image** content. The `recognize()` call returns
      a raw string, often riddled with line breaks and mis‑read characters.
  - name: Set Up the AI Post‑Processor (Auto‑Download Qwen2.5‑3B Model)
    text: We instantiate `AsposeAI`, configure it to pull the Qwen model from Hugging
      Face, and allocate GPU layers for inference.
  - name: Define a Simple Correction Function
    text: The function receives the raw OCR string, builds a prompt, and asks the
      model to proof‑read it. Temperature `0.0` forces deterministic output, which
      is ideal for correction tasks.
  - name: Attach the Correction Function and Clean the Raw OCR Result
    text: We bind `fix` as a post‑processor, then let the AI run over the `raw_text`.
      The result lands in `cleaned_text`.
  - name: Display the Corrected Text
    text: A quick `print` lets you verify that the pipeline succeeded.
  - name: Release AI Resources When Done
    text: Finally, we **free AI resources**. This call unloads the model from GPU
      memory, preventing leaks in long‑running services.
  type: HowTo
tags:
- OCR
- AI
- Aspose
title: Εξαγωγή κειμένου από εικόνα με Aspose OCR & AI – Πλήρης οδηγός βήμα‑βήμα
url: /el/python/general/extract-text-image-with-aspose-ocr-ai-full-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή κειμένου από εικόνα με Aspose OCR & AI – Πλήρης Οδηγός Βήμα‑βήμα

Έχετε αναρωτηθεί ποτέ πώς να **εξάγετε κείμενο από εικόνα** χωρίς να ξοδέψετε μια περιουσία σε υπηρεσίες cloud; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν πρόβλημα όταν το ακατέργαστο αποτέλεσμα OCR μοιάζει με ακατάστατο μπερδεμένο κείμενο, ειδικά σε θορυβώδεις σκαναρίσματα.  

Σε αυτόν τον οδηγό θα περάσουμε από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που δείχνει πώς να **φορτώνετε εικόνα OCR**, να βελτιώσετε την ποιότητα για **βελτιώσετε την ακρίβεια του OCR**, να **διορθώσετε αυτόματα τα σφάλματα OCR**, και τέλος να **ελευθερώσετε πόρους AI** ώστε η εφαρμογή σας να παραμείνει ελαφριά.

Θα καταλήξετε με μια καθαρή συμβολοσειρά που μπορείτε να τροφοδοτήσετε απευθείας σε μια βάση δεδομένων, έναν δείκτη αναζήτησης ή οποιοδήποτε downstream pipeline NLP. Καμία μυστική σύνδεση σε εξωτερικά έγγραφα — όλα όσα χρειάζεστε είναι εδώ.

## Τι θα δημιουργήσετε

- Φόρτωση αρχείου εικόνας και εκτέλεση Aspose OCR για λήψη ακατέργαστου κειμένου.  
- Ενσωμάτωση ενός LLM on‑device (μοντέλο Qwen2.5‑3B) στην αλυσίδα OCR ως post‑processor.  
- Χρήση ενός μικρού prompt για διόρθωση και proof‑reading του αποτελέσματος OCR.  
- Απελευθέρωση του μοντέλου και της μνήμης GPU με μία κλήση.  

Στο τέλος θα έχετε ένα σταθερό πρότυπο που μπορείτε να επαναχρησιμοποιήσετε για τιμολόγια, αποδείξεις, σαρωμένα συμβόλαια ή οποιοδήποτε bitmap που περιέχει αναγνώσιμους χαρακτήρες.

---

## Προαπαιτούμενα

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|------------------------|
| Python 3.9+ | Σύγχρονη σύνταξη και type hints. |
| `aspose-ocr` package | Παρέχει την κλάση `OcrEngine`. |
| GPU με CUDA (προαιρετικό) | Ενεργοποιεί `ocr_engine.use_gpu = True` για ταχύτερη αναγνώριση. |
| Σύνδεση στο Internet (πρώτη εκτέλεση) | Επιτρέπει στο μοντέλο Qwen να κατεβάσει αυτόματα. |
| Βασική εξοικείωση με συναρτήσεις | Απαραίτητη για την προσθήκη της callback διόρθωσης. |

Εγκαταστήστε τις βιβλιοθήκες με:

```bash
pip install aspose-ocr
pip install aspose-ocr-ai
```

> **Pro tip:** Αν εργάζεστε σε μηχάνημα μόνο με CPU, απλώς παραλείψτε τη γραμμή `use_gpu`; ο κώδικας θα επιστρέψει ομαλά.

---

## Εξαγωγή κειμένου από εικόνα με Aspose OCR και AI

Παρακάτω βρίσκεται το πλήρες script, χωρισμένο σε εννέα λογικά βήματα. Κάθε βήμα εισάγεται με σύντομη εξήγηση, ακολουθούμενο από τον ακριβή κώδικα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε.

### Βήμα 1: Εισαγωγή των μονάδων Aspose OCR και AI

Ξεκινάμε φορτώνοντας τα δύο namespaces που χρειαζόμαστε: τον πυρήνα του OCR engine και τον βοηθό AI που φιλοξενεί το LLM.

```python
# Step 1: Import Aspose OCR and AI modules
import aspose.ocr as aocr
import aspose.ocr.ai as aocr_ai
```

> **Γιατί;** Η συγκέντρωση των imports σε ένα μέρος κάνει το script πιο εύκολο στην επιθεώρηση και αποφεύγει κρυφές εξαρτήσεις αργότερα.

### Βήμα 2: Δημιουργία και ρύθμιση του OCR Engine (Ενεργοποίηση GPU)

Η ενεργοποίηση του GPU επιταχύνει τη φάση ανάλυσης εικονοστοιχείων, κάτι που μπορεί να εξοικονομήσει δευτερόλεπτα σε μεγάλες παρτίδες.

```python
# Step 2: Create and configure the OCR engine (enable GPU for faster processing)
ocr_engine = aocr.OcrEngine()
ocr_engine.use_gpu = True   # Set to False if you lack a compatible GPU
```

> **Σημείωση:** Η σημαία `use_gpu` είναι ασφαλής για εναλλαγή· η μηχανή θα εντοπίσει αυτόματα τη διαθεσιμότητα CUDA.

### Βήμα 3: Φόρτωση της εικόνας που περιέχει το κείμενο προς αναγνώριση

Εδώ **φορτώνουμε εικόνα OCR**. Η διαδρομή μπορεί να είναι απόλυτη ή σχετική· βεβαιωθείτε μόνο ότι το αρχείο υπάρχει.

```python
# Step 3: Load the image that contains the text to be recognized
ocr_engine.load_image("YOUR_DIRECTORY/input.png")
```

> **Κοινό λάθος:** Η παροχή λανθασμένης διαδρομής προκαλεί `FileNotFoundError`. Ελέγξτε προσεκτικά την ορθογραφία, ειδικά σε συστήματα αρχείων με ευαισθησία σε πεζά‑κεφαλαία.

### Βήμα 4: Εκτέλεση OCR και λήψη του ακατέργαστου εξαγόμενου κειμένου

Τώρα πραγματικά **εξάγουμε κείμενο από εικόνα**. Η κλήση `recognize()` επιστρέφει μια ακατέργαστη συμβολοσειρά, συχνά γεμάτη αλλαγές γραμμής και λανθασμένους χαρακτήρες.

```python
# Step 4: Perform OCR and obtain the raw extracted text
raw_text = ocr_engine.recognize()
```

Αν εκτυπώσετε το `raw_text` αυτή τη στιγμή, θα δείτε κάτι όπως:

```
Th1s is a s4mple test.
```

Παρατηρήστε το “1” αντί για “i” και το “4” αντί για “e”. Εδώ έρχεται σε δράση ο AI post‑processor.

### Βήμα 5: Ρύθμιση του AI Post‑Processor (Αυτόματη λήψη μοντέλου Qwen2.5‑3B)

Δημιουργούμε ένα αντικείμενο `AsposeAI`, το ρυθμίζουμε ώστε να κατεβάσει το μοντέλο Qwen από το Hugging Face και να κατανείμει τα GPU layers για inference.

```python
# Step 5: Set up the AI post‑processor (auto‑download Qwen2.5‑3B model)
ai_processor = aocr_ai.AsposeAI()
model_cfg = aocr_ai.AsposeAIModelConfig()
model_cfg.allow_auto_download = "true"
model_cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_cfg.gpu_layers = 20               # Adjust based on your GPU VRAM
ai_processor.initialize(model_cfg)
```

> **Γιατί αυτό το μοντέλο;** Το Qwen2.5‑3B‑Instruct είναι αρκετά μικρό για να τρέξει σε GPU μεσαίας κατηγορίας, ενώ είναι αρκετά ισχυρό για να κατανοήσει prompts proof‑reading, καθιστώντας το ιδανικό για **βελτιώσετε την ακρίβεια του OCR** χωρίς να αυξήσει τη μνήμη.

### Βήμα 6: Ορισμός μιας απλής συνάρτησης διόρθωσης

Η συνάρτηση λαμβάνει τη ακατέργαστη συμβολοσειρά OCR, δημιουργεί ένα prompt και ζητά από το μοντέλο να το proof‑read. Η θερμοκρασία `0.0` εξασφαλίζει ντετερμινιστικό αποτέλεσμα, ιδανικό για εργασίες διόρθωσης.

```python
# Step 6: Define a simple correction function that asks the model to proof‑read the OCR output
def fix(text, _):
    prompt = f"Proof‑read and correct the OCR text:\n\n{text}"
    return ai_processor.run_inference(prompt, temperature=0.0, max_new_tokens=512)
```

> **Πώς λειτουργεί:** Το LLM βλέπει το ακριβές κείμενο και επιστρέφει μια καθαρή έκδοση, λειτουργώντας ουσιαστικά ως έξυπνος ορθογράφος που διορθώνει επίσης ανωμαλίες στις αλλαγές γραμμής.

### Βήμα 7: Σύνδεση της συνάρτησης διόρθωσης και καθαρισμός του ακατέργαστου OCR

Δεσμεύουμε τη `fix` ως post‑processor, έπειτα αφήνουμε το AI να επεξεργαστεί το `raw_text`. Το αποτέλεσμα αποθηκεύεται στο `cleaned_text`.

```python
# Step 7: Attach the correction function as a post‑processor and clean the raw OCR result
ai_processor.set_post_processor(fix, None)
cleaned_text = ai_processor.run_postprocessor(raw_text)
```

Σε αυτό το σημείο το `cleaned_text` θα πρέπει να εμφανίζει:

```
This is a simple test.
```

### Βήμα 8: Εμφάνιση του διορθωμένου κειμένου

Μια γρήγορη `print` σας επιτρέπει να επαληθεύσετε ότι η αλυσίδα λειτούργησε.

```python
# Step 8: Display the corrected text
print("Cleaned text:\n", cleaned_text)
```

Η έξοδος στην κονσόλα θα είναι κάτι όπως:

```
Cleaned text:
 This is a simple test.
```

### Βήμα 9: Απελευθέρωση πόρων AI όταν ολοκληρωθεί

Τέλος, **ελευθερώνουμε πόρους AI**. Αυτή η κλήση αποφορτώνει το μοντέλο από τη μνήμη GPU, αποτρέποντας διαρροές σε υπηρεσίες που τρέχουν για μεγάλο χρονικό διάστημα.

```python
# Step 9: Release AI resources when done
ai_processor.free_resources()
```

> **Γιατί είναι σημαντικό:** Η παράλειψη της απελευθέρωσης πόρων μπορεί να προκαλέσει καταρρεύσεις εξαιτίας έλλειψης μνήμης, ειδικά σε περιβάλλοντα serverless όπου κάθε κλήση πρέπει να καθαρίζει μετά τον εαυτό της.

---

## Πώς να φορτώνετε εικόνα OCR αποδοτικά

Αν χρειάζεται να επεξεργαστείτε δεκάδες αρχεία, τυλίξτε τη φόρτωση και την αναγνώριση μέσα σε βρόχο:

```python
def ocr_one(path):
    ocr_engine.load_image(path)
    return ocr_engine.recognize()
```

Θυμηθείτε να επαναχρησιμοποιείτε το ίδιο αντικείμενο `ocr_engine`; η δημιουργία νέου για κάθε εικόνα προσθέτει περιττό κόστος και αναιρεί το σκοπό της βελτιστοποίησης **φορτώνετε εικόνα OCR**.

---

## Τεχνικές για βελτίωση της ακρίβειας του OCR

1. **Προεπεξεργασία της εικόνας** – Μετατροπή σε γκρι, αύξηση αντίθεσης και διόρθωση κλίσης πριν την τροφοδοσία του engine.  
2. **Ενεργοποίηση GPU** – Όπως φαίνεται στο Βήμα 2, η διαδρομή GPU συχνά προσφέρει υψηλότερα confidence scores.  
3. **Post‑process με AI** – Το βήμα **διορθώστε σφάλματα OCR** είναι η πιο ισχυρή μοχλός· μπορεί να αντιμετωπίσει γλωσσικές ιδιαιτερότητες που οι κανόνες ορθογραφίας δεν εντοπίζουν.  

Ο συνδυασμός αυτών των τριών τακτικών συνήθως μειώνει το word‑error‑rate κατά 30‑40 % σε πραγματικές σαρώσεις.

---

## Διόρθωση σφαλμάτων OCR χρησιμοποιώντας AI Post‑Processor

Η συνάρτηση `fix` που ορίσαμε νωρίτερα είναι σκόπιμα ελάχιστη. Μπορείτε να την εμπλουτίσετε με πρόσθετες οδηγίες, για παράδειγμα:

```python
def fix_with_formatting(text, _):
    prompt = (
        "You are a proofreading assistant. Return ONLY the corrected text, "
        "preserving line breaks and punctuation. Do not add explanations.\n\n"
        f"{text}"
    )
    return ai_processor.run_inference(prompt, temperature=0.0, max_new_tokens=1024)
```

Η αλλαγή σε `ai_processor.set_post_processor(fix_with_formatting, None)` αποδίδει πιο καθαρά, διατηρώντας τη μορφοποίηση — ένας ακόμη τρόπος για **βελτιώσετε**.

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Εξαγωγή κειμένου από εικόνα – Βελτιστοποίηση OCR με Aspose.OCR για .NET](/ocr/english/net/ocr-optimization/)
- [Εξαγωγή κειμένου από εικόνα C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Μετατροπή εικόνας σε κείμενο – Εκτέλεση OCR σε εικόνα από URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}