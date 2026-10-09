---
category: general
date: 2026-09-25
description: Μάθετε πώς να εκτελείτε OCR σε εικόνα με το Aspose OCR, να φορτώνετε
  την εικόνα για OCR και να αναγνωρίζετε κείμενο από απόδειξη σε ένα πλήρες παράδειγμα
  Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- load image for OCR
- recognize text from receipt
- Aspose OCR Python
- AI post‑processor OCR
language: el
lastmod: 2026-09-25
og_description: Πραγματοποιήστε OCR σε εικόνα χρησιμοποιώντας το Aspose OCR στην Python.
  Αυτός ο οδηγός δείχνει πώς να φορτώσετε μια εικόνα για OCR και να αναγνωρίσετε κείμενο
  από απόδειξη με ενίσχυση AI.
og_image_alt: Screenshot of Python code performing OCR on an image and showing original
  vs AI‑enhanced text
og_title: Εκτελέστε OCR σε εικόνα με το Aspose OCR και τον AI μετα-επεξεργαστή – Οδηγός
  Python
schemas:
- author: Aspose
  dateModified: '2026-09-25'
  description: Learn how to perform OCR on image with Aspose OCR, load image for OCR,
    and recognize text from receipt in a complete Python example.
  headline: How to perform OCR on image using Aspose OCR and AI post‑processor in
    Python
  type: TechArticle
tags:
- OCR
- Python
- Aspose
title: Πώς να εκτελέσετε OCR σε εικόνα χρησιμοποιώντας το Aspose OCR και τον AI μεταεπεξεργαστή
  σε Python
url: /el/python/general/how-to-perform-ocr-on-image-using-aspose-ocr-and-ai-post-pro/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εκτελέσετε OCR σε εικόνα χρησιμοποιώντας το Aspose OCR και τον AI post‑processor σε Python

Αν χρειάζεστε να **perform OCR on image** αρχεία σε Python, αυτό το tutorial σας δείχνει μια πλήρη, έτοιμη‑για‑εκτέλεση λύση. Θα μάθετε πώς να **load image for OCR**, να εκτελέσετε τη μηχανή Aspose OCR, και να **recognize text from receipt** έγγραφα με προαιρετική AI‑βασισμένη επεξεργασία.

Θα περάσουμε από κάθε βήμα, από την εγκατάσταση του SDK μέχρι την απελευθέρωση πόρων, ώστε να μπορείτε να ενσωματώσετε αξιόπιστη εξαγωγή κειμένου στις δικές σας εφαρμογές χωρίς να χάσετε καμία λεπτομέρεια.

## Προαπαιτούμενα

- Python 3.8+ εγκατεστημένο  
- Aspose OCR για Python μέσω pip (`pip install aspose-ocr`)  
- Πρόσβαση στο Internet για τη λήψη του προαιρετικού μοντέλου AI  
- Ένα δείγμα εικόνας από απόδειξη (`receipt.png`) τοποθετημένο σε γνωστό φάκελο  

Δεν απαιτούνται πρόσθετες εξωτερικές υπηρεσίες· ο κώδικας εκτελείται τοπικά και χρησιμοποιεί το δωρεάν μοντέλο Qwen2‑3B‑Instruct όταν είναι διαθέσιμα τα GPU layers.

## Βήμα 1: Εγκατάσταση των απαιτούμενων πακέτων

```bash
pip install aspose-ocr
```

Το πακέτο `aspose-ocr` περιέχει τόσο την κλάση `OcrEngine` όσο και τον `AsposeAI` post‑processor που θα χρησιμοποιήσουμε για να **perform OCR on image** αρχεία.

## Βήμα 2: Δημιουργία και διαμόρφωση της μηχανής OCR – load image for OCR

```python
from aspose.ocr import OcrEngine

# Initialise the OCR engine
ocr_engine = OcrEngine()

# Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/receipt.png")   # <-- load image for OCR
```

Η κλήση του `load_image` ενημερώνει τη μηχανή ποιο αρχείο θα αναλύσει. Μπορείτε να αντικαταστήσετε τη διαδρομή με οποιοδήποτε αρχείο PNG, JPG ή TIFF που χρειάζεστε για να **perform OCR on image**.

## Βήμα 3: Ρύθμιση του προαιρετικού AsposeAI post‑processor

Ο AI post‑processor μπορεί να διορθώσει ορθογραφικά λάθη, να βελτιώσει τη μορφοποίηση ή να εφαρμόσει προσαρμοσμένη λογική μετά την επιστροφή του ακατέργαστου αποτελέσματος OCR.

```python
from aspose.ocr import AsposeAI, AsposeAIModelConfig

# Initialise the AI processor (logging is optional)
ai_processor = AsposeAI()   # AsposeAI(logging=my_logger)

# Define which model to use – it will auto‑download if missing
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20                     # use GPU layers when available
)

# Load the model configuration into the processor
ai_processor.initialize(model_config)   # implicit in many examples
```

Η διαμόρφωση οδηγεί τον επεξεργαστή να κατεβάσει το προεπιλεγμένο μοντέλο Qwen2, επιτρέποντάς σας να **perform OCR on image** με υψηλότερη κατανόηση της γλώσσας.

## Βήμα 4: Προσθήκη μιας απλής συνάρτησης post‑processing

Μπορείτε να συνδέσετε οποιοδήποτε callable που λαμβάνει το ακατέργαστο κείμενο και επιστρέφει μια διορθωμένη έκδοση. Ακολουθεί ένα ελάχιστο παράδειγμα που διορθώνει ένα κοινό τυπογραφικό λάθος:

```python
def simple_spell_check(text, **kwargs):
    """Correct a frequent misspelling in receipt OCR results."""
    return text.replace("reciept", "receipt")

# Register the function with the AI processor
ai_processor.set_post_processor(simple_spell_check, {})
```

Επειδή η συνάρτηση είναι καταχωρημένη, κάθε φορά που καλείτε το `run_postprocessor`, η έξοδος OCR θα περνάει από αυτό το βήμα.

## Βήμα 5: Εκτέλεση OCR και βελτίωση του αποτελέσματος – recognize text from receipt

```python
# Perform the core OCR operation
raw_result = ocr_engine.recognize()          # <-- recognize text from receipt

# Let the AI processor improve the raw output
enhanced_result = ai_processor.run_postprocessor(raw_result)

# Display both versions
print("Original OCR :", raw_result.text)
print("AI‑enhanced  :", enhanced_result.text)
```

Η κλήση `recognize` επιστρέφει ένα αντικείμενο του οποίου το χαρακτηριστικό `text` περιέχει τους ακατέργαστους χαρακτήρες που εξήχθησαν από την εικόνα της απόδειξης. Η επακόλουθη κλήση `run_postprocessor` επιστρέφει ένα νέο αποτέλεσμα όπου έχει εφαρμοστεί ο έλεγχος ορθογραφίας (και τυχόν βελτιώσεις βάσει μοντέλου).

### Αναμενόμενο αποτέλεσμα

```
Original OCR : Total: $23.45\nSubtotl: $20.00\nTax: $3.45\nThank you for your reciept
AI‑enhanced  : Total: $23.45
Subtotal: $20.00
Tax: $3.45
Thank you for your receipt
```

Παρατηρήστε πώς το κείμενο με βελτιώσεις AI διορθώνει το τυπογραφικό λάθος και εισάγει αλλαγές γραμμής για ευανάγνωστη παρουσίαση — ακριβώς αυτό που θέλετε όταν **recognize text from receipt** αρχεία.

## Βήμα 6: Εκκαθάριση πόρων

```python
# Release memory held by the AI processor
ai_processor.free_resources()

# Dispose of the OCR engine
ocr_engine.dispose()
```

Η απελευθέρωση πόρων είναι ιδιαίτερα σημαντική όταν επεξεργάζεστε πολλές εικόνες σε μια μακροχρόνια υπηρεσία.

## Πλήρες εκτελέσιμο script

Συνδυάζοντας όλα τα κομμάτια μαζί λαμβάνετε ένα ενιαίο script που μπορείτε να αντιγράψετε, επικολλήσετε και εκτελέσετε:

```python
# ocr_receipt.py
from aspose.ocr import AsposeAI, AsposeAIModelConfig, OcrEngine

# 1️⃣ Initialise OCR engine and load the image
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/receipt.png")   # load image for OCR

# 2️⃣ Set up optional AI post‑processor
ai_processor = AsposeAI()
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20
)
ai_processor.initialize(model_config)

# 3️⃣ Register a simple spell‑check function
def simple_spell_check(text, **kwargs):
    return text.replace("reciept", "receipt")
ai_processor.set_post_processor(simple_spell_check, {})

# 4️⃣ Perform OCR and enhance the result
raw_result = ocr_engine.recognize()                # recognize text from receipt
enhanced_result = ai_processor.run_postprocessor(raw_result)

print("Original OCR :", raw_result.text)
print("AI‑enhanced  :", enhanced_result.text)

# 5️⃣ Release resources
ai_processor.free_resources()
ocr_engine.dispose()
```

Εκτελέστε το script με:

```bash
python ocr_receipt.py
```

Θα πρέπει να δείτε τις αρχικές και τις AI‑βελτιωμένες εξόδους να εμφανίζονται στην κονσόλα.

## Επαγγελματικές συμβουλές και κοινά προβλήματα

- **Image quality matters** – βεβαιωθείτε ότι η εικόνα της απόδειξης είναι καλά φωτισμένη και δεν είναι υπερβολικά συμπιεσμένη· διαφορετικά η μηχανή OCR μπορεί να χάσει χαρακτήρες, μειώνοντας το όφελος της post‑processing.  
- **GPU availability** – εάν το μηχάνημά σας δεν διαθέτει συμβατό GPU, ορίστε `gpu_layers=0` για να εξαναγκάσετε την εκτέλεση σε CPU· το μοντέλο θα λειτουργήσει ακόμα, αν και πιο αργά.  
- **Custom post‑processors** – μπορείτε να συνδέσετε πολλαπλές συναρτήσεις ή να χρησιμοποιήσετε ένα πιο εξελιγμένο μοντέλο γλώσσας για να επαναμορφοποιήσετε ημερομηνίες, ποσά ή ονόματα προμηθευτών.  
- **Batch processing** – δημιουργήστε ένα μόνο αντικείμενο `AsposeAI` και επαναχρησιμοποιήστε το σε πολλές περιπτώσεις `OcrEngine` για να αποφύγετε επαναλαμβανόμενες λήψεις μοντέλου.  

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **perform OCR on image** αρχεία χρησιμοποιώντας το Aspose OCR, πώς να **load image for OCR**, και πώς να **recognize text from receipt** με βελτιώσεις που βασίζονται σε AI. Ακολουθώντας τα παραπάνω βήματα, μπορείτε να ενσωματώσετε ακριβή, υψηλής απόδοσης επεξεργασία αποδείξεων σε οποιαδήποτε εφαρμογή Python.

**Next steps**: εξερευνήστε πρόσθετες τεχνικές post‑processing όπως η κανονικοποίηση νομισμάτων, ενσωματώστε το αποτέλεσμα σε βάση δεδομένων, ή μεταβείτε σε μεγαλύτερο μοντέλο για πολυγλωσσικές αποδείξεις. Για πιο βαθιά προσαρμογή, δείτε την τεκμηρίωση του Aspose OCR σχετικά με προσαρμοσμένα language packs και προχωρημένη προ‑επεξεργασία εικόνας.

Καλό κώδικα!

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Μετατροπή Εικόνας σε Κείμενο: Εξαγωγή Κειμένου από Εικόνα Χρησιμοποιώντας το Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Πώς να κάνετε OCR Κειμένου Εικόνας με Γλώσσα Χρησιμοποιώντας το Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Πώς να Εκτελέσετε OCR σε C# – Εξαγωγή Κειμένου από Εικόνα Χρησιμοποιώντας το Aspose OCR](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image-using-aspose/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}