---
category: general
date: 2026-06-06
description: αναγνωρίστε κείμενο από εικόνα με το Aspose OCR – μάθετε πώς να φορτώνετε
  εικόνα για OCR και να εκτελείτε OCR στην εικόνα χρησιμοποιώντας AI post‑processing
  σε Python.
draft: false
keywords:
- recognize text from image
- perform ocr on image
- load image for ocr
language: el
og_description: αναγνωρίστε κείμενο από εικόνα γρήγορα. Αυτός ο οδηγός δείχνει πώς
  να φορτώσετε εικόνα για OCR, να εκτελέσετε OCR στην εικόνα και να ενισχύσετε τα
  αποτελέσματα με AI post‑processing.
og_title: Αναγνώριση κειμένου από εικόνα χρησιμοποιώντας Aspose OCR & AI
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: recognize text from image with Aspose OCR – learn how to load image
    for OCR and perform OCR on image using AI post‑processing in Python.
  headline: recognize text from image using Aspose OCR & AI
  type: TechArticle
- description: recognize text from image with Aspose OCR – learn how to load image
    for OCR and perform OCR on image using AI post‑processing in Python.
  name: recognize text from image using Aspose OCR & AI
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer - `asposeocr` package (`pip install asposeocr`) -
      An image file (e.g., `doc.png`) that contains printed or handwritten text -
      Optional: a GPU for faster LLM inference (the script works on CPU too)'
  - name: Install and import the required modules
    text: '```python # Install the library (run once in your environment) # pip install
      asposeocr'
  - name: Create the OCR engine and enable handwritten text recognition
    text: '```python # Initialise the OCR engine ocr_engine = ocr.OcrEngine()'
  - name: Load the image for OCR
    text: '```python # Point the engine at the file you want to process ocr_engine.load_image("YOUR_DIRECTORY/doc.png")
      ```'
  - name: Run the raw OCR pass
    text: '```python # Execute the recognition pipeline and capture the raw result
      raw_result = ocr_engine.recognize() ```'
  - name: Configure the Aspose AI model for LLM post‑processing
    text: '```python ai_config = AsposeAIModelConfig( allow_auto_download="true",
      # Pull the model if missing hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
      hugging_face_quantization="int8", # Reduce RAM usage gpu_layers=20, # Use 20
      GPU layers if a GPU is present directory_model_path="YOUR_DIRECTORY/mo'
  - name: Initialise the AI processor and attach it as a post‑processor
    text: '```python # Instantiate the AI processor with the configuration above ai_processor
      = AsposeAI() ai_processor.initialize(ai_config)'
  - name: Run the post‑processor to enhance the OCR output
    text: '```python # Apply AI‑driven post‑processing enhanced_result = ocr_engine.run_postprocessor(raw_result)'
  - name: Release resources
    text: '```python # Free GPU/CPU memory held by the AI model ai_processor.free_resources()'
  type: HowTo
- questions:
  - answer: No. The script falls back to CPU, but inference will be slower.
    question: Do I need a GPU?
  - answer: Absolutely—just change `hugging_face_repo_id` and adjust `gpu_layers`
      accordingly.
    question: Can I use a different LLM?
  - answer: Resize it first (e.g., using Pillow) to keep memory usage reasonable.
    question: What if my image is huge?
  - answer: You can toggle `enable_handwritten_recognition` depending on your workload.
    question: Is handwritten recognition always on?
  type: FAQPage
tags:
- OCR
- Aspose
- Python
title: Αναγνώριση κειμένου από εικόνα χρησιμοποιώντας το Aspose OCR & AI
url: /el/python/general/recognize-text-from-image-using-aspose-ocr-ai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση κειμένου από εικόνα χρησιμοποιώντας Aspose OCR & AI

Ποτέ χρειάστηκε να αναγνωρίσετε κείμενο από εικόνα αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη θα σας προσφέρει ταυτόχρονα ταχύτητα και ακρίβεια; Δεν είστε μόνοι. Σε αυτόν τον οδηγό θα περάσουμε από ένα πλήρες, end‑to‑end παράδειγμα που δείχνει **πώς να φορτώσετε εικόνα για OCR**, **πώς να εκτελέσετε OCR σε εικόνα**, και στη συνέχεια θα τελειοποιήσουμε το αποτέλεσμα με τον AI post‑processor της Aspose. Στο τέλος θα έχετε ένα έτοιμο script που μετατρέπει ένα PNG σε καθαρό, αναζητήσιμο κείμενο.

## Τι θα μάθετε

Θα καλύψουμε τα πάντα, από την εγκατάσταση του πακέτου Aspose OCR μέχρι την απελευθέρωση πόρων στο τέλος της εκτέλεσης. Θα δείτε γιατί η ενεργοποίηση της αναγνώρισης χειρόγραφου κειμένου είναι σημαντική, πώς να ρυθμίσετε ένα Qwen 2.5 LLM για post‑processing, και πώς φαίνεται το τελικό αποτέλεσμα. Δεν απαιτούνται εξωτερικές αναφορές—απλώς αντιγράψτε, επικολλήστε και τρέξτε.

### Προαπαιτήσεις

- Python 3.8 ή νεότερη  
- πακέτο `asposeocr` (`pip install asposeocr`)  
- Ένα αρχείο εικόνας (π.χ., `doc.png`) που περιέχει τυπωμένο ή χειρόγραφο κείμενο  
- Προαιρετικά: μια GPU για ταχύτερη εκτέλεση LLM (το script λειτουργεί και σε CPU)

---

## Αναγνώριση κειμένου από εικόνα – Βήμα‑βήμα

Κάτω από κάθε μπλοκ κώδικα θα βρείτε μια σύντομη εξήγηση του **γιατί** κάνουμε αυτή τη συγκεκριμένη ενέργεια, όχι μόνο του **τι** κάνει η γραμμή.

### Βήμα 1: Εγκατάσταση και εισαγωγή των απαιτούμενων modules

```python
# Install the library (run once in your environment)
# pip install asposeocr

import asposeocr as ocr
from asposeocr.ai import AsposeAI, AsposeAIModelConfig
```

*Γιατί;* Η εισαγωγή του `asposeocr` μας δίνει την κλάση `OcrEngine`, ενώ το υπο-μοντέλο `ai` παρέχει τον LLM‑based post‑processor που βελτιώνει δραματικά το ακατέργαστο αποτέλεσμα OCR.

### Βήμα 2: Δημιουργία του OCR engine και ενεργοποίηση της αναγνώρισης χειρόγραφου κειμένου

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Turn on handwritten‑text support – useful for notes, signatures, etc.
ocr_engine.ocr_settings.enable_handwritten_recognition = True
```

Η ενεργοποίηση της αναγνώρισης χειρόγραφου επεκτείνει το σύνολο χαρακτήρων του engine, ώστε να μην χάσετε τις σημειώσεις όταν **εκτελείτε OCR σε εικόνα** που περιέχει μικτό τυπωμένο και καλλιγραφικό κείμενο.

### Βήμα 3: Φόρτωση της εικόνας για OCR

```python
# Point the engine at the file you want to process
ocr_engine.load_image("YOUR_DIRECTORY/doc.png")
```

Η κλήση `load_image` είναι η στιγμή που **φορτώνετε εικόνα για OCR**· αν η διαδρομή είναι λανθασμένη, το engine θα ρίξει μια ενημερωτική εξαίρεση, σώζοντάς σας από ασαφείς σφάλματα σε επόμενα βήματα.

### Βήμα 4: Εκτέλεση της ακατέργαστης διεργασίας OCR

```python
# Execute the recognition pipeline and capture the raw result
raw_result = ocr_engine.recognize()
```

Σε αυτό το στάδιο λαμβάνετε ένα αντικείμενο `RecognitionResult` που περιέχει το ακατέργαστο κείμενο, τις βαθμολογίες εμπιστοσύνης και τα μεταδεδομένα διάταξης. Συχνά είναι θορυβώδες—γι' αυτό χρειάζεται η καθαριότητα με AI.

### Βήμα 5: Διαμόρφωση του μοντέλου Aspose AI για LLM post‑processing

```python
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",                     # Pull the model if missing
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # Reduce RAM usage
    gpu_layers=20,                                  # Use 20 GPU layers if a GPU is present
    directory_model_path="YOUR_DIRECTORY/models/ocr_ai"
)
```

Γιατί να ασχοληθούμε με αυτές τις ρυθμίσεις;  
- **auto‑download** εγγυάται ότι το μοντέλο είναι διαθέσιμο στην πρώτη εκτέλεση.  
- **int8 quantization** μειώνει τη χρήση μνήμης χωρίς σημαντική απώλεια ακρίβειας.  
- **gpu_layers** σας επιτρέπει να αξιοποιήσετε μια συμβατή GPU για ταχύτερη εκτέλεση.

### Βήμα 6: Αρχικοποίηση του AI επεξεργαστή και σύνδεσή του ως post‑processor

```python
# Instantiate the AI processor with the configuration above
ai_processor = AsposeAI()
ai_processor.initialize(ai_config)

# Hook the AI processor into the OCR engine
ocr_engine.set_post_processor(ai_processor, None)
```

Η σύνδεση του επεξεργαστή σημαίνει ότι κάθε φορά που καλείτε `run_postprocessor`, το LLM θα διορθώσει ορθογραφικά, θα ενώσει σπασμένες λέξεις και ακόμη θα προτείνει ελλιπείς στίξη.

### Βήμα 7: Εκτέλεση του post‑processor για βελτίωση του OCR output

```python
# Apply AI‑driven post‑processing
enhanced_result = ocr_engine.run_postprocessor(raw_result)

# Print the polished text
print(enhanced_result.text)
```

Το `enhanced_result.text` είναι συνήθως πολύ πιο αναγνώσιμο από το ακατέργαστο string—σκεφτείτε το ως έναν ορθογραφικό ελεγκτή που καταλαβαίνει επίσης το συμφραζόμενο.

### Βήμα 8: Απελευθέρωση πόρων

```python
# Free GPU/CPU memory held by the AI model
ai_processor.free_resources()

# Dispose of the OCR engine to close file handles, etc.
ocr_engine.dispose()
```

Ο καθαρισμός είναι κρίσιμος σε υπηρεσίες που τρέχουν πολύ χρόνο· διαφορετικά θα διαρρεύσει μνήμη GPU και τελικά θα καταρρεύσει η εφαρμογή σας.

---

## Πλήρες script που μπορείτε να εκτελέσετε σήμερα

```python
import asposeocr as ocr
from asposeocr.ai import AsposeAI, AsposeAIModelConfig

# 1️⃣ Initialise OCR engine with handwritten support
ocr_engine = ocr.OcrEngine()
ocr_engine.ocr_settings.enable_handwritten_recognition = True

# 2️⃣ Load the image you want to analyse
ocr_engine.load_image("YOUR_DIRECTORY/doc.png")   # <-- replace with your path

# 3️⃣ Perform the basic OCR pass
raw_result = ocr_engine.recognize()

# 4️⃣ Set up the AI model for smarter output
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,
    directory_model_path="YOUR_DIRECTORY/models/ocr_ai"
)

# 5️⃣ Initialise and attach the AI post‑processor
ai_processor = AsposeAI()
ai_processor.initialize(ai_config)
ocr_engine.set_post_processor(ai_processor, None)

# 6️⃣ Enhance the OCR result with the LLM
enhanced_result = ocr_engine.run_postprocessor(raw_result)

# 7️⃣ Show the final, cleaned‑up text
print("=== Enhanced OCR Output ===")
print(enhanced_result.text)

# 8️⃣ Clean up
ai_processor.free_resources()
ocr_engine.dispose()
```

**Αναμενόμενο αποτέλεσμα** (παράδειγμα για μια απλή εικόνα τιμολόγησης):

```
=== Enhanced OCR Output ===
Invoice #12345
Date: 2024‑04‑01
Total Amount: $1,250.00
Thank you for your business!
```

Παρατηρήστε πώς το AI layer διόρθωσε το “Inv0ice” → “Invoice” και πρόσθεσε την ελλιπή στίξη.

---

## Συχνές ερωτήσεις (και σύντομες απαντήσεις)

- **Χρειάζομαι GPU;** Όχι. Το script επιστρέφει σε CPU, αλλά η εκτέλεση θα είναι πιο αργή.  
- **Μπορώ να χρησιμοποιήσω διαφορετικό LLM;** Απόλυτα—απλώς αλλάξτε το `hugging_face_repo_id` και προσαρμόστε το `gpu_layers` ανάλογα.  
- **Τι γίνεται αν η εικόνα μου είναι τεράστια;** Αλλάξτε το μέγεθός της πρώτα (π.χ., με το Pillow) για να διατηρήσετε λογική χρήση μνήμης.  
- **Είναι πάντα ενεργή η αναγνώριση χειρόγραφου;** Μπορείτε να ενεργοποιήσετε/απενεργοποιήσετε το `enable_handwritten_recognition` ανάλογα με το φορτίο εργασίας.

---

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **αναγνωρίζετε κείμενο από εικόνα** χρησιμοποιώντας Aspose OCR, πώς να **φορτώνετε εικόνα για OCR**, και πώς να **εκτελείτε OCR σε εικόνα** με AI‑βελτιωμένο post‑processing. Το πλήρες, εκτελέσιμο παράδειγμα παραπάνω σας δίνει μια σταθερή βάση για να ενσωματώσετε OCR σε οποιοδήποτε έργο Python—είτε πρόκειται για σάρωση αποδείξεων, ψηφιοποίηση συμβάσεων, ή εξαγωγή δεδομένων από χειρόγραφες φόρμες.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να αντικαταστήσετε το μοντέλο Qwen με ένα μεγαλύτερο, πειραματιστείτε με διαφορετικά σχήματα ποσοτικοποίησης, ή συνδέστε πολλαπλές εικόνες για επεξεργασία σε batch. Οι δυνατότητες είναι ατελείωτες, και ο κώδικας που μόλις δημιουργήσατε θα τις διαχειριστεί άψογα.

Καλή προγραμματιστική δουλειά, και εύχομαι τα OCR αποτελέσματά σας να είναι πάντα κρυστάλλινα!  

![Screenshot of Python console showing enhanced OCR output](/images/ocr_output.png){alt="Στιγμιότυπο οθόνης που δείχνει πώς να αναγνωρίζετε κείμενο από εικόνα χρησιμοποιώντας Aspose OCR"}

## Τι Θα Μάθετε Στη Σειρά;

Οι παρακάτω οδηγίες καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Βήμα‑βήμα](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Μετατροπή Εικόνας σε Κείμενο – Εκτέλεση OCR σε Εικόνα από URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}