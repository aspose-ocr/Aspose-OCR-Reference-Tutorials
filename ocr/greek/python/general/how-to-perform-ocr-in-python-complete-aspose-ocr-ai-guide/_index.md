---
category: general
date: 2026-06-25
description: Μάθετε πώς να εκτελείτε OCR σε Python και ανακαλύψτε τον καλύτερο τρόπο
  φόρτωσης εικόνας για OCR, στη συνέχεια ενισχύστε την ακρίβεια με την μετά‑επεξεργασία
  Aspose AI.
draft: false
keywords:
- how to perform OCR
- load image for OCR
- Aspose OCR Python
- AI post‑processor OCR
- OCR accuracy improvement
- Python image processing OCR
language: el
og_description: Πώς να εκτελέσετε OCR στην Python; Ακολουθήστε αυτόν τον οδηγό για
  να φορτώσετε εικόνα για OCR, να εκτελέσετε βασική αναγνώριση και να βελτιώσετε τα
  αποτελέσματα με την επεξεργασία μετά από Aspose AI.
og_title: Πώς να εκτελέσετε OCR σε Python – Πλήρης οδηγός Aspose OCR & AI
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Learn how to perform OCR in Python and discover the best way to load
    image for OCR, then boost accuracy with Aspose AI post‑processing.
  headline: How to Perform OCR in Python – Complete Aspose OCR & AI Guide
  type: TechArticle
- description: Learn how to perform OCR in Python and discover the best way to load
    image for OCR, then boost accuracy with Aspose AI post‑processing.
  name: How to Perform OCR in Python – Complete Aspose OCR & AI Guide
  steps:
  - name: Expected Output
    text: '``` === Raw OCR === Inv0ice #12345 Date: 2023-08-15 Total: $1,23O'
  - name: What if I don’t have a GPU?
    text: Set `model_config.gpu_layers = 0` and optionally increase `model_config.context_size`
      to 2048 for better CPU performance. The model will run slower, but you still
      get the same quality of correction.
  - name: My image is rotated—will `load_image` handle it?
    text: 'Aspose OCR automatically detects orientation, but for extremely skewed
      scans you may want to pre‑rotate using Pillow:'
  - name: How do I process multiple files in a folder?
    text: Wrap the whole pipeline in a `for` loop and store each `enhanced_text` in
      a list or write directly to a CSV. Remember to call `ocr_ai.free_resources()`
      **once** after the loop, not after each file—re‑initialising the model repeatedly
      is wasteful.
  - name: Can I swap the language model?
    text: Absolutely. Just change `model_config.hugging_face_repo_id` to any GGUF‑compatible
      model on Hugging Face (e.g., `Meta/Llama-3.2-1B-Instruct-GGUF`). Keep the quantization
      setting consistent with your hardware.
  type: HowTo
tags:
- OCR
- Python
- Aspose
- AI
title: Πώς να εκτελέσετε OCR σε Python – Πλήρης οδηγός Aspose OCR & AI
url: /el/python/general/how-to-perform-ocr-in-python-complete-aspose-ocr-ai-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εκτελέσετε OCR σε Python – Πλήρης Οδηγός Aspose OCR & AI

Έχετε αναρωτηθεί ποτέ **πώς να εκτελέσετε OCR** σε Python χωρίς να παλεύετε με χαμηλού επιπέδου τεχνικές εικόνας; Δεν είστε μόνοι. Σε αυτόν τον οδηγό θα περάσουμε από τη φόρτωση μιας εικόνας για OCR, την εκτέλεση εξαγωγής απλού κειμένου και, στη συνέχεια, την επεξεργασία του αποτελέσματος με τον AI post‑processor της Aspose. Στο τέλος θα έχετε ένα έτοιμο προς χρήση script που μετατρέπει θορυβώδεις σαρώσεις σε καθαρό, αναζητήσιμο κείμενο—χωρίς επιπλέον υπηρεσίες.

Θα καλύψουμε τα πάντα, από την εγκατάσταση του SDK μέχρι την απελευθέρωση πόρων σε εφαρμογές που τρέχουν για μεγάλο χρονικό διάστημα. Αν έχετε προσπαθήσει ποτέ να **φορτώσετε εικόνα για OCR** και έχετε πάρει ένα ακατάστατο μπερδεμένο κείμενο, αυτός ο οδηγός είναι το αντίδοτο. Θα δείτε γιατί ο συνδυασμός παραδοσιακού OCR με ένα μοντέλο γλώσσας αποδίδει αποτελέσματα που μοιάζουν με κείμενο που έχει πληκτρολογηθεί από άνθρωπο.

## Προαπαιτήσεις

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

- Python 3.9 ή νεότερο (ο κώδικας χρησιμοποιεί type hints που δεν αρέσουν στους παλαιότερους διερμηνείς)
- Ένα ενεργό άδεια Aspose OCR ή μια δωρεάν δοκιμή (η έκδοση community λειτουργεί για αξιολόγηση)
- Μια GPU με τουλάχιστον 4 GB VRAM αν θέλετε να επιταχύνετε το AI μοντέλο (προαιρετικό αλλά ωραίο)
- Μια δείγμα εικόνας, π.χ., `sample_invoice.png`, τοποθετημένη κάπου που μπορείτε να αναφερθείτε

Αν κάποιο από αυτά σας φαίνεται άγνωστο, μην πανικοβληθείτε—η εγκατάσταση του SDK είναι μια γραμμή εντολής, και οι ρυθμίσεις GPU μπορούν να απενεργοποιηθούν αργότερα.

## Βήμα 1: Εγκατάσταση Aspose OCR και Εξαρτήσεων

Ανοίξτε ένα τερματικό και εκτελέστε:

```bash
pip install aspose-ocr
pip install aspose-ocr-ai
```

Το πρώτο πακέτο σας παρέχει το `aspose.ocr`, το δεύτερο προσθέτει τις βοηθητικές λειτουργίες του AI post‑processor. Και τα δύο είναι καθαρά Python wheels, οπότε δεν χρειάζεται να μεταγλωττίσετε τίποτα μόνοι σας.

## Βήμα 2: Φόρτωση Εικόνας για OCR και Αρχικοποίηση της Μηχανής

Τώρα θα **φορτώσουμε εικόνα για OCR** χρησιμοποιώντας το `OcrEngine` της Aspose. Σκεφτείτε το σαν να δίνετε ένα φύλλο χαρτιού σε έναν πολύ επιμελή υπάλληλο που διαβάζει κάθε χαρακτήρα.

```python
import aspose.ocr as aocr
import aspose.ocr.ai as aocr_ai

# Initialise the basic OCR engine
ocr_engine = aocr.OcrEngine()

# Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

# Perform a plain OCR scan – this returns a raw string
raw_text = ocr_engine.recognize()
print("=== Raw OCR ===")
print(raw_text)
```

> **Γιατί είναι σημαντικό:** Η κλήση `load_image` είναι η γέφυρα μεταξύ του συστήματος αρχείων σας και της μηχανής OCR. Αν η διαδρομή είναι λανθασμένη, θα λάβετε `FileNotFoundError` πριν ξεκινήσει η αναγνώριση. Ελέγξτε πάντα διπλά τους διαχωριστές καταλόγου, ειδικά σε Windows vs. macOS/Linux.

## Βήμα 3: Ρύθμιση του Aspose AI Post‑Processor

Το Aspose AI μπορεί να κατεβάσει ένα μοντέλο γλώσσας από το Hugging Face, να το αποθηκεύσει τοπικά και να τρέξει inference στην GPU (ή CPU). Παρακάτω διαμορφώνουμε ένα ελαφρύ μοντέλο 3 δισεκατομμυρίων παραμέτρων που χωράει στα περισσότερα σύγχρονα laptops.

```python
# Initialise the AI post‑processor
ocr_ai = aocr_ai.AsposeAI()
model_config = aocr_ai.AsposeAIModelConfig()

# Allow the SDK to fetch the model automatically
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"

# Use half of the GPU layers – balances speed and VRAM usage
model_config.gpu_layers = 20
model_config.context_size = 1024

# Load (or download) the model now
ocr_ai.initialize(model_config)
```

> **Συμβουλή:** Αν χρησιμοποιείτε μηχάνημα μόνο με CPU, ορίστε `gpu_layers = 0`. Το μοντέλο θα τρέξει ακόμα, απλώς λίγο πιο αργά. Η ποσοτικοποίηση `int8` διατηρεί το αποτύπωμα μνήμης μικρό ενώ διατηρεί την πλειονότητα της ακρίβειας του μοντέλου.

## Βήμα 4: Καταχώρηση Προσαρμοσμένου Post‑Processor

Το AI μοντέλο χρειάζεται ένα prompt που του λέει τι να κάνει. Εδώ του ζητάμε να λειτουργήσει σαν διορθωτής OCR, διορθώνοντας ορθογραφικά λάθη, συγχωνεύοντας σπασμένες λέξεις και αφαιρώντας artefacts.

```python
def correction_processor(text, settings):
    prompt = (
        "You are an OCR post‑processor. Fix any spelling or OCR errors in the following "
        "text and return ONLY the cleaned version:\n\n"
        f"{text}"
    )
    # Temperature 0.0 makes the output deterministic
    return ocr_ai.run_inference(prompt, temperature=0.0, max_new_tokens=512)

# Hook the custom processor into the AI pipeline
ocr_ai.set_post_processor(correction_processor, custom_settings=None)
```

> **Γιατί ένας προσαρμοσμένος επεξεργαστής;** Ο προεπιλεγμένος post‑processor μπορεί να προσθέσει επιπλέον εξηγήσεις ή μορφοποίηση που δεν χρειάζεστε. Παρέχοντας τη δική μας συνάρτηση, διατηρούμε την έξοδο αυστηρά ως καθαρό κείμενο, κάτι τέλειο για downstream indexing ή αποθήκευση σε βάση δεδομένων.

## Βήμα 5: Εκτέλεση του AI‑Enhanced OCR Pipeline

Τώρα τροφοδοτούμε την ακατέργαστη έξοδο OCR στο AI επίπεδο. Η μηχανή θα καλέσει το `correction_processor`, το οποίο με τη σειρά του επικοινωνεί με το μοντέλο γλώσσας.

```python
# Apply the AI post‑processor to the raw OCR result
enhanced_text = ocr_ai.run_postprocessor(raw_text)

print("\n=== AI‑enhanced OCR ===")
print(enhanced_text)
```

Θα πρέπει να δείτε μια αξιοσημείωτη βελτίωση: οι ελλιπείς χαρακτήρες αποκαθίστανται, κοινά OCR λάθη όπως “0” vs “O” διορθώνονται, και οι αλλαγές γραμμής γίνονται πιο λογικές.

## Βήμα 6: Καθαρισμός – Απελευθέρωση Πόρων

Αν σκοπεύετε να τρέξετε αυτό το script μέσα σε web service ή σε daemon που λειτουργεί για μεγάλο χρονικό διάστημα, η απελευθέρωση μνήμης GPU είναι κρίσιμη. Η παράλειψη κλήσης `free_resources` μπορεί να οδηγήσει σε σφάλματα “out‑of‑memory” μετά από μερικές εκατοντάδες αιτήσεις.

```python
ocr_ai.free_resources()
```

Αυτό ήταν—η πλήρης pipeline OCR είναι τώρα έτοιμη για παραγωγή.

## Ανασκόπηση Πλήρους Script

Παρακάτω βρίσκεται το πλήρες, εκτελέσιμο παράδειγμα. Αντιγράψτε‑και‑επικολλήστε το σε ένα αρχείο με όνομα `ocr_with_ai.py`, προσαρμόστε τη διαδρομή της εικόνας και τρέξτε `python ocr_with_ai.py`.

```python
import aspose.ocr as aocr
import aspose.ocr.ai as aocr_ai

# Step 1: Load image for OCR and perform basic recognition
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
raw_text = ocr_engine.recognize()
print("=== Raw OCR ===")
print(raw_text)

# Step 2: Initialise the Aspose AI post‑processor
ocr_ai = aocr_ai.AsposeAI()
model_config = aocr_ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"
model_config.gpu_layers = 20          # half of GPU layers
model_config.context_size = 1024
ocr_ai.initialize(model_config)

# Step 3: Register custom correction processor
def correction_processor(text, settings):
    prompt = (
        "You are an OCR post‑processor. Fix any spelling or OCR errors in the following "
        "text and return ONLY the cleaned version:\n\n"
        f"{text}"
    )
    return ocr_ai.run_inference(prompt, temperature=0.0, max_new_tokens=512)

ocr_ai.set_post_processor(correction_processor, custom_settings=None)

# Step 4: Run AI post‑processor on raw OCR output
enhanced_text = ocr_ai.run_postprocessor(raw_text)
print("\n=== AI‑enhanced OCR ===")
print(enhanced_text)

# Step 5: Release resources (important for long‑running apps)
ocr_ai.free_resources()
```

### Αναμενόμενο Αποτέλεσμα

```
=== Raw OCR ===
Inv0ice #12345
Date: 2023-08-15
Total: $1,23O

=== AI‑enhanced OCR ===
Invoice #12345
Date: 2023-08-15
Total: $1,230
```

Παρατηρήστε πώς το “Inv0ice” γίνεται “Invoice” και το περιττό “O” μετά το ποσό εξαφανίζεται. Αυτό είναι το AI που κάνει τη μαγεία του.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν δεν έχω GPU;

Ορίστε `model_config.gpu_layers = 0` και προαιρετικά αυξήστε το `model_config.context_size` σε 2048 για καλύτερη απόδοση CPU. Το μοντέλο θα τρέξει πιο αργά, αλλά θα έχετε την ίδια ποιότητα διόρθωσης.

### Η εικόνα μου είναι περιστραμμένη—θα διαχειριστεί το `load_image`;

Το Aspose OCR ανιχνεύει αυτόματα την προσανατολισμό, αλλά για εξαιρετικά λοξές σαρώσεις μπορεί να θέλετε να προ‑στρέψετε την εικόνα χρησιμοποιώντας το Pillow:

```python
from PIL import Image
img = Image.open("sample.png")
rotated = img.rotate(90, expand=True)
rotated.save("rotated.png")
ocr_engine.load_image("rotated.png")
```

### Πώς επεξεργάζομαι πολλαπλά αρχεία σε φάκελο;

Τυλίξτε ολόκληρη τη pipeline μέσα σε έναν βρόχο `for` και αποθηκεύστε κάθε `enhanced_text` σε μια λίστα ή γράψτε απευθείας σε CSV. Θυμηθείτε να καλέσετε `ocr_ai.free_resources()` **μία φορά** μετά το βρόχο, όχι μετά από κάθε αρχείο—η επανεκκίνηση του μοντέλου επανειλημμένα είναι σπατάλη.

```python
import os

for filename in os.listdir("invoices"):
    if filename.lower().endswith(".png"):
        ocr_engine.load_image(os.path.join("invoices", filename))
        raw = ocr_engine.recognize()
        clean = ocr_ai.run_postprocessor(raw)
        # Save or index `clean`
```

### Μπορώ να αλλάξω το μοντέλο γλώσσας;

Απολύτως. Απλώς αλλάξτε το `model_config.hugging_face_repo_id` σε οποιοδήποτε μοντέλο συμβατό με GGUF στο Hugging Face (π.χ., `Meta/Llama-3.2-1B-Instruct-GGUF`). Διατηρήστε τη ρύθμιση ποσοτικοποίησης σύμφωνη με το υλικό σας.

## Επαγγελματικές Συμβουλές & Πιθανά Προβλήματα

- **Pro tip:** Ορίστε `temperature=0.0` για ντετερμινιστικές διορθώσεις. Υψηλότερες θερμοκρασίες μπορούν να εισάγουν δημιουργικές αλλά λανθασμένες αλλαγές.
- **Watch out for:** Εξαιρετικά μεγάλα έγγραφα (> 5000 χαρακτήρες). Το παράθυρο συμφραζομένων του μοντέλου περιορίζεται σε 1024 tokens στο παράδειγμα· χωρίστε το κείμενο σε παραγράφους πριν το στείλετε στο AI.
- **Security note:** Αν τρέχετε αυτό το script σε ρυθμιζόμενο περιβάλλον, βεβαιωθείτε ότι το URL λήψης του μοντέλου είναι στη λευκή λίστα. Η σημαία `allow_auto_download` μπορεί

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετα χαρακτηριστικά API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Βήμα‑βήμα](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Πώς να Χρησιμοποιήσετε AspOCR: Φίλτρα Προεπεξεργασίας Εικόνας OCR για .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}