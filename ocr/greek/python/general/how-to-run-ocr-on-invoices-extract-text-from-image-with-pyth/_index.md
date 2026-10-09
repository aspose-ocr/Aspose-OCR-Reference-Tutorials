---
category: general
date: 2026-01-07
description: Πώς να εκτελέσετε OCR και να εξάγετε κείμενο από εικόνα για επεξεργασία
  τιμολογίων. Μάθετε πώς να βελτιώσετε την ακρίβεια του OCR, να φορτώσετε εικόνα για
  OCR και να επεξεργαστείτε το OCR τιμολογίων αποδοτικά.
draft: false
keywords:
- how to run ocr
- extract text from image
- improve ocr accuracy
- load image for ocr
- process invoice ocr
language: el
og_description: Πώς να εκτελέσετε OCR σε τιμολόγια βήμα‑βήμα. Εξάγετε κείμενο από
  εικόνα, βελτιώστε την ακρίβεια του OCR και φορτώστε την εικόνα για OCR χρησιμοποιώντας
  το Aspose AI.
og_title: Πώς να Εκτελέσετε OCR σε Τιμολόγια – Πλήρης Οδηγός Python
tags:
- OCR
- Python
- Image Processing
title: Πώς να εκτελέσετε OCR σε τιμολόγια – Εξαγωγή κειμένου από εικόνα με Python
url: /el/python/general/how-to-run-ocr-on-invoices-extract-text-from-image-with-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εκτελέσετε OCR σε τιμολόγια – Εξαγωγή κειμένου από εικόνα με Python

Έχετε αναρωτηθεί ποτέ **πώς να εκτελέσετε OCR** σε ένα σαρωμένο τιμολόγιο και να λάβετε καθαρό, αναζητήσιμο κείμενο; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν προβλήματα όταν η ακατέργαστη έξοδος του OCR είναι γεμάτη ορθογραφικά λάθη, σπασμένες αλλαγές γραμμής και ελλιπές σημεία στίξης. Σε αυτό το tutorial θα περάσουμε από μια ολοκληρωμένη λύση που όχι μόνο **εξάγει κείμενο από εικόνα** αλλά επίσης **βελτιώνει την ακρίβεια του OCR** μέσω post‑processing με ένα μοντέλο Aspose AI.

Θα δείτε πώς να **φορτώσετε εικόνα για OCR**, να εκτελέσετε τη ενσωματωμένη μηχανή και στη συνέχεια να εφαρμόσετε έναν ελαφρύ έλεγχο ορθογραφίας που κάνει το αποτέλεσμα έτοιμο για downstream analytics. Στο τέλος, θα έχετε ένα επαναχρησιμοποιήσιμο script που μπορεί να ενσωματωθεί σε οποιοδήποτε pipeline επεξεργασίας τιμολογίων.

> **Τι θα χρειαστείτε**  
> * Python 3.9 ή νεότερο  
> * Πακέτα `aspose-ocr` και `aspose-ai` (εγκατεστημένα μέσω `pip`)  
> * Μια εικόνα τιμολογίου (PNG, JPEG ή TIFF) – θα χρησιμοποιήσουμε το `sample_invoice.png` ως παράδειγμα  
> * Προαιρετικά: GPU με τουλάχιστον 4 GB VRAM για ταχύτερη εκτέλεση μοντέλου (το script λειτουργεί και σε CPU)

## Βήμα 1: Εγκατάσταση Απαιτούμενων Πακέτων και Προετοιμασία του Περιβάλλοντος

Πριν μπορέσουμε να **φορτώσουμε εικόνα για OCR**, πρέπει να διασφαλίσουμε ότι οι απαραίτητες βιβλιοθήκες είναι διαθέσιμες. Η μηχανή Aspose OCR παρέχεται με ένα απλό Python wrapper, ενώ ο AI post‑processor βασίζεται σε ένα ποσοτικοποιημένο μοντέλο Hugging Face.

```bash
# Install Aspose OCR and AI packages
pip install aspose-ocr aspose-ai
```

> **Συμβουλή επαγγελματία:** Εάν σκοπεύετε να χρησιμοποιήσετε επιτάχυνση GPU, εγκαταστήστε το `torch` με υποστήριξη CUDA (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu121`).

## Βήμα 2: Φόρτωση της Εικόνας του Τιμολογίου

Η φόρτωση της εικόνας είναι απλή, αλλά αξίζει να αναφέρουμε γιατί ορίζουμε ρητά τη διαδρομή ως raw string (`r"..."`). Αυτό αποτρέπει τυχαία προβλήματα με χαρακτήρες διαφυγής σε διαδρομές Windows.

```python
import aspose.ocr as ocr

# Define the path to your invoice image
image_path = r"YOUR_DIRECTORY/sample_invoice.png"

# Initialize the OCR engine and attach the image
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)
```

*Γιατί είναι σημαντικό:* Η χρήση του `ocr.Image.load` εγγυάται ότι η εικόνα προεπεξεργάζεται (δυαδικοποίηση, διόρθωση κλίσης) σύμφωνα με τις βέλτιστες προεπιλογές της Aspose, οι οποίες ήδη **βελτιώνουν την ακρίβεια του OCR** πριν συμβεί οποιοδήποτε AI μαγικό.

## Βήμα 3: Εκτέλεση της Ενσωματωμένης Μηχανής OCR

Τώρα πραγματικά **εκτελούμε OCR** και καταγράφουμε το ακατέργαστο κείμενο. Αυτό το βήμα δείχνει την τυπική έξοδο που θα λάβετε από μια απλή εκτέλεση OCR—συχνά ένα χάος αλλαγών γραμμής και περιστασιακών ορθογραφικών λαθών.

```python
# Perform OCR
engine.recognize()
raw_text = engine.recognized_text

print("Raw OCR output:")
print(raw_text)
```

**Τυπική ακατέργαστη έξοδος** (συμπιεσμένη για συντομία):

```
INVOICE NO: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

Μπορείτε να παρατηρήσετε ότι το “Invoice” εμφανInvo1ce” ή ότι λείπουν σημεία στίξης. Εδώ έρχεται σε δράση ο AI post‑processor.

## Βήμα 4: Διαμόρφωση του Μοντέλου Aspose AI

Το μοντέλο AI που θα χρησιμοποιήσουμε είναι το **Qwen2.5‑3B‑Instruct‑GGUF**, ένα ελαφρύ LLM προσαρμοσμένο σε οδηγίες που τρέχει άνετα σε GPU μεσαίας κατηγορίας. Η παρακάτω διαμόρφωση ενημερώνει την Aspose πού να κατεβάσει το μοντέλο, πόσες στρώσεις να διατηρήσει στο GPU και το μέγεθος του context για την επεξεργασία μεγάλων παραγράφων.

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,               # 30 layers on GPU, remainder on CPU
    context_size=4096            # larger context for long paragraphs
)

ai = AsposeAI()
ai.initialize(model_config)   # you could also pass `model_config` to the constructor
```

> **Γιατί αυτή η διαμόρφωση;**  
> * `gpu_layers=30` ισορροπεί την ταχύτητα και τη μνήμη—η περισσότερη επεξεργασία γίνεται στο GPU, ενώ οι υπόλοιπες στρώσεις παραμένουν στο CPU για να αποφευχθούν σφάλματα OOM.  
> * `context_size=4096` διασφαλίζει ότι το μοντέλο μπορεί να δει ολόκληρο το τιμολόγιο ταυτόχρονα, αποτρέποντας την περικοπή σημαντικών πεδίων.

## Βήμα 5: Δημιουργία ενός Απλού Post‑Processor Ελέγχου Ορθογραφίας

Θα τυλίξουμε την κλήση AI σε μια μικρή συνάρτηση που ονομάζεται `simple_spell_check`. Το prompt είναι σκόπιμα σύντομο: “Correct spelling and punctuation:” ακολουθούμενο από το ακατέργαστο κείμενο OCR. Το μοντέλο επιστρέφει μια καθαρισμένη έκδοση.

```python
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

# Register the post‑processor with the AI instance
ai.set_post_processor(simple_spell_check, None)
```

**Πώς λειτουργεί:** `ai.run_prompt` στέλνει το prompt στο τοπικά φορτωμένο LLM, το οποίο επιστρέφει μια ενιαία συμβολοσειρά με διορθωμένη ορθογραφία, σωστή στίξη και πιο φυσική διάταξη αλλαγών γραμμής.

## Βήμα 6: Εφαρμογή του Post‑Processor στο Ακατέργαστο Κείμενο OCR

Τώρα συμβαίνει η μαγεία. Τροφοδοτούμε την ακατέργαστη έξοδο OCR στον post‑processor μας και εκτυπώνουμε το βελτιωμένο αποτέλεσμα.

```python
enhanced_text = ai.run_postprocessor(raw_text)

print("\nAI‑enhanced OCR output:")
print(enhanced_text)
```

**Δείγμα βελτιωμένης εξόδου**:

```
Invoice No: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

Παρατηρήστε τη διορθωμένη ορθογραφία του “Invoice”, τη σωστή χρήση των άνω‑κάτω τελειών και τις συνεπείς αλλαγές γραμμής—ακριβώς αυτό που χρειάζεστε για αξιόπιστη downstream ανάλυση.

## Βήμα 7: Καθαρισμός Πόρων

Τanto η μηχανή OCR όσο και το μοντέλο AI εκχωρούν εγγενείς πόρους. Είναι καλή πρακτική να τους ελευθερώνετε όταν τελειώσετε, ειδικά σε υπηρεσίες που τρέχουν για μεγάλο χρονικό διάστημα.

```python
ai.free_resources()
engine.dispose()
```

## Πλήρες Script – Έτοιμο για Επικόλληση

Παρακάτω βρίσκεται το πλήρες, εκτελέσιμο script που ενώνει όλα τα βήματα. Αποθηκεύστε το ως `invoice_ocr.py`, αντικαταστήστε το `YOUR_DIRECTORY` με το φάκελο που περιέχει την εικόνα του τιμολογίου σας, και εκτελέστε το με `python invoice_ocr.py`.

```python
# invoice_ocr.py
import aspose.ocr as ocr
from aspose.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1: Load the image to be processed
# -------------------------------------------------
image_path = r"YOUR_DIRECTORY/sample_invoice.png"
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)

# -------------------------------------------------
# Step 2: Run the built‑in OCR engine and obtain raw text
# -------------------------------------------------
engine.recognize()
raw_text = engine.recognized_text
print("Raw OCR output:")
print(raw_text)

# -------------------------------------------------
# Step 3: Configure the Aspose AI model for post‑processing
# -------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,
    context_size=4096
)

ai = AsposeAI()
ai.initialize(model_config)   # alternatively, pass config to the constructor

# -------------------------------------------------
# Step 4: Define a simple spell‑check post‑processor
# -------------------------------------------------
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

ai.set_post_processor(simple_spell_check, None)

# -------------------------------------------------
# Step 5: Apply the post‑processor to the raw OCR text
# -------------------------------------------------
enhanced_text = ai.run_postprocessor(raw_text)
print("\nAI‑enhanced OCR output:")
print(enhanced_text)

# -------------------------------------------------
# Step 6: Release resources
# -------------------------------------------------
ai.free_resources()
engine.dispose()
```

Εκτελέστε το script και θα δείτε τόσο την θορυβώδη ακατέργαστη εξαγωγή OCR όσο και την επεξεργασμένη, **βελτιωμένη ακρίβεια OCR** έκδοση δίπλα‑δίπλα.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### 1. Τι γίνεται αν η εικόνα του τιμολογίου μου είναι PDF πολλαπλών σελίδων;

Η Aspose OCR μπορεί να φορτώσει απευθείας σελίδες PDF. Αντικαταστήστε τη γραμμή φόρτωσης εικόνας με:

```python
engine.image = ocr.Image.load("invoice.pdf", page_index=0)  # 0‑based page number
```

### 2. Η GPU μου εξαντλεί τη μνήμη—μπορώ να χρησιμοποιήσω μόνο CPU;

Απόλυτα. Ορίστε `gpu_layers=0` στο `AsposeAIModelConfig`. Το μοντέλο θα τρέξει εξ ολοκλήρου στο CPU, κάτι που είναι πιο αργό αλλά ασφαλές για υλικό χαμηλής κατηγορίας.

### 3. Πώς να διαχειριστώ τιμολόγια μη‑Αγγλικής γλώσσας;

Αντικαταστήστε το ID του αποθετηρίου μοντέλου με ένα μοντέλο ειδικό για τη γλώσσα, π.χ., `"mistralai/Mistral-7B-Instruct-v0.2"` για πολυγλωσσική υποστήριξη. Το υπόλοιπο του pipeline παραμένει αμετάβλητο.

### 4. Μπορώ να συνδυάσω πολλαπλούς post‑processors (π.χ., μορφοποίηση ημερομηνιών, εξαγωγή συνολικών);

Ναι. Η `ai.set_post_processor` δέχεται λίστα από κλήσιμες συναρτήσεις. Για παράδειγμα:

```python
def extract_totals(text):
    # simple regex to pull monetary values
    import re
    totals = re.findall(r"\$\d+(?:,\d{3})*(?:\.\d{2})?", text)
    return "\n".join(totals)

ai.set_post_processor([simple_spell_check, extract_totals], None)
```

## Συμβουλές Απόδοσης & Καλές Πρακτικές

| Συμβουλή | Γιατί βοηθά |
|-----|---------------|
| **Ομαδοποίηση πολλαπλών τιμολογίων** – φορτώστε τα σε λίστα και επεξεργαστείτε τα σε βρόχο. | Μειώνει το φορτίο του διερμηνέα Python και διατηρεί το μοντέλο AI ζεστό στη μνήμη. |
| **Cache του μοντέλου** – αποφύγετε την επαναλαμβανόμενη κλήση `initialize` σε web service. | Η φόρτωση του μοντέλου μπορεί να διαρκέσει ~30 δευτερόλεπτα· η cache προσφέρει άμεσες απαντήσεις. |
| **Αλλαγή μεγέθους μεγάλων εικόνων** σε πλάτος 1500 px πριν το OCR. | Οι μικρότερες εικόνες επιταχύνουν τόσο το OCR όσο και την AI inference χωρίς να θυσιάζεται η ακρίβεια. |
| **Ορίστε `allow_auto_download="false"` σε παραγωγή** – συμπεριλάβετε το μοντέλο στην ανάπτυξη. | Εξασφαλίζει προβλέψιμο χρόνο εκκίνησης και αποφεύγει προβλήματα δικτύου. |

## Συμπέρασμα

Καλύψαμε **πώς να εκτελέσετε OCR** σε τιμολόγια, από τη φόρτωση της εικόνας μέχρι την τελειοποίηση του αποτελέσματος με έναν AI‑βασισμένο έλεγχο ορθογραφίας. Ακολουθώντας αυτά τα βήματα μπορείτε αξιόπιστα **να εξάγετε κείμενο από εικόνα**, **να βελτιώσετε την ακρίβεια του OCR**, και να επεξεργαστείτε απρόσκοπτα **OCR τιμολογίων** σε οποιαδήποτε ροή εργασίας βασισμένη σε Python.

Δοκιμάστε το με διάφορες διατάξεις τιμολογίων—ίσως μια χειρόγραφη απόδειξη ή ένα σαρωμένο συμβόλαιο. Η ίδια pipeline προσαρμόζεται με ελάχιστες αλλαγές, αποδεικνύοντας ότι ένας καλά δομημένος συνδυασμός OCR + AI είναι ένα ευέλικτο εργαλείο για οποιοδήποτε έργο αυτοματοποίησης εγγράφων.

Αν βρήκατε αυτόν τον οδηγό χρήσιμο, σκεφτείτε να τον μοιραστείτε με συναδέλφους ή να δώσετε αστέρι στο αποθετήριο που φιλοξενεί τα πακέτα Aspose

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}