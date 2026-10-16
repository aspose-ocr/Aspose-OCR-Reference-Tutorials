---
category: general
date: 2026-06-06
description: Πραγματοποιήστε OCR σε εικόνα χρησιμοποιώντας το Aspose OCR και ένα μοντέλο
  Hugging Face. Μάθετε πώς να κατεβάσετε το μοντέλο Hugging Face, να εξάγετε κείμενο
  από τιμολόγιο και να ελευθερώσετε τους πόρους GPU.
draft: false
keywords:
- perform OCR on image
- download Hugging Face model
- extract text from invoice
- free GPU resources
- load image for OCR
language: el
og_description: Πραγματοποιήστε OCR σε εικόνα χρησιμοποιώντας το Aspose OCR και ένα
  μοντέλο Hugging Face. Αυτό το σεμινάριο δείχνει πώς να κατεβάσετε το μοντέλο, να
  εξάγετε κείμενο από τιμολόγιο και να ελευθερώσετε τους πόρους GPU.
og_title: Εκτελέστε OCR σε εικόνα με το Aspose OCR & LLM – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Perform OCR on image using Aspose OCR and a Hugging Face model. Learn
    how to download Hugging Face model, extract text from invoice, and free GPU resources.
  headline: Perform OCR on Image with Aspose OCR & LLM – Complete Guide
  type: TechArticle
tags:
- OCR
- Aspose
- Python
- AI
- HuggingFace
title: Εκτελέστε OCR σε εικόνα με το Aspose OCR & LLM – Πλήρης οδηγός
url: /el/python/general/perform-ocr-on-image-with-aspose-ocr-llm-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε Εικόνα με Aspose OCR & LLM – Πλήρης Οδηγός

Έχετε ποτέ θέλει να **εκτελέσετε OCR σε εικόνα** αρχεία αλλά νιώσατε κολλημένοι στην ερώτηση «πού να ξεκινήσω;»; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το εμπόδιο όταν ασχολούνται για πρώτη φορά με την αυτοματοποίηση εγγράφων. Τα καλά νέα είναι ότι με το Aspose OCR και ένα ελαφρύ LLM από το Hugging Face, μπορείτε να μετατρέψετε μια ακατέργαστη σάρωση ενός τιμολογίου σε καθαρό, αναζητήσιμο κείμενο με λίγες γραμμές Python.

Σε αυτό το tutorial θα περάσουμε από όλα όσα χρειάζεστε: από **φόρτωση εικόνας για OCR**, μέχρι **λήψη του μοντέλου Hugging Face**, μέχρι **εξαγωγή κειμένου από τιμολόγιο** δεδομένα, και τέλος **απελευθέρωση πόρων GPU** ώστε η εφαρμογή σας να παραμένει ελαφριά. Στο τέλος θα έχετε ένα αυτόνομο script που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο.

---

## Τι Θα Μάθετε

- Πώς να **εκτελέσετε OCR σε εικόνα** χρησιμοποιώντας το `OcrEngine` της Aspose.
- Τα ακριβή βήματα για **λήψη αρχείων μοντέλου Hugging Face** αυτόματα.
- Τεχνικές για **εξαγωγή κειμένου από τιμολόγιο** PDFs ή PNGs με AI‑βελτιωμένη μετα‑επεξεργασία.
- Καλές πρακτικές για **απελευθέρωση πόρων GPU** μετά την εκτίμηση.
- Συμβουλές για **φόρτωση εικόνας για OCR** αποδοτικά και αποφυγή κοινών παγίδων.

Δεν απαιτείται εξωτερική τεκμηρίωση—όλα όσα χρειάζεστε είναι εδώ, με πλήρη κώδικα, εξηγήσεις και αναμενόμενα αποτελέσματα.

## Προαπαιτούμενα

| Απαίτηση | Αιτία |
|-------------|--------|
| Python 3.9+ | Σύγχρονη σύνταξη και type hints |
| `asposeocr` package (`pip install asposeocr`) | Κύρια μηχανή OCR |
| Access to a GPU (optional but recommended) | Επιταχύνει τον LLM post‑processor |
| An invoice image (`sample_invoice.png`) | Πραγματικό παράδειγμα |

Αν σας λείπει κάποιο από αυτά, εγκαταστήστε το τώρα· το script θα **κατεβάσει αυτόματα το μοντέλο Hugging Face**, ώστε να μην χρειάζεται να ψάχνετε τα αρχεία μόνοι σας.

## Βήμα 1: Εκτέλεση OCR σε Εικόνα – Δημιουργία της Μηχανής

Το πρώτο πράγμα που πρέπει να κάνετε είναι να εκκινήσετε τη μηχανή OCR της Aspose. Σκεφτείτε το ως το άνοιγμα ενός κεννού καμβά όπου η εικόνα θα μετατραπεί αργότερα σε κείμενο.

```python
import asposeocr as ocr
from asposeocr.ai import AsposeAI, AsposeAIModelConfig

# Step 1: Initialize the OCR engine
engine = ocr.OcrEngine()
```

> **Γιατί είναι σημαντικό:** Το `OcrEngine` αφαιρεί όλες τις χαμηλού επιπέδου προεπεξεργασίες εικόνας, ώστε να μπορείτε να εστιάσετε στη ροή εργασίας υψηλότερου επιπέδου. Επίσης εκθέτει τη μέθοδο `set_post_processor` που αργότερα θα μας επιτρέψει να συνδέσουμε ένα LLM για πιο έξυπνη έξοδο.

## Βήμα 2: Φόρτωση Εικόνας για OCR – Επιλογή του Κατάλληλου Αρχείου

Τώρα που υπάρχει η μηχανή, πρέπει να **φορτώσουμε εικόνα για OCR**. Η Aspose υποστηρίζει PNG, JPG, TIFF και μερικές άλλες μορφές. Βεβαιωθείτε ότι η διαδρομή είναι απόλυτη ή σχετική με τη θέση του script σας.

```python
# Step 2: Load the image you want to process
engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
```

> **Συμβουλή:** Αν η εικόνα σας είναι μεγάλη, σκεφτείτε να την αλλάξετε μέγεθος εκ των προτέρων για να μειώσετε την πίεση μνήμης. Η μηχανή OCR μπορεί να διαχειριστεί σαρώσεις υψηλής ανάλυσης, αλλά μια εικόνα 300 DPI είναι συνήθως το ιδανικό σημείο για τιμολόγια.

## Βήμα 3: Εκτέλεση Ακατέργαστου OCR και Προβολή του Εξαγόμενου Κειμένου

Με την εικόνα φορτωμένη, μπορούμε τελικά να **εκτελέσουμε OCR σε εικόνα** και να δούμε τι εξάγει η ακατέργαστη μηχανή. Αυτό το βήμα μας δίνει μια βάση πριν προσθέσουμε τη μαγεία AI.

```python
# Step 3: Run the built‑in OCR and capture raw results
raw_result = engine.recognize()
print("Raw text:")
print(raw_result.text)
```

**Αναμενόμενο αποτέλεσμα (κομμένο):**

```
Raw text:
Invoice #12345
Date: 2024‑04‑01
Total: $1,250.00
...
```

Η ακατέργαστη έξοδος συχνά περιέχει αλλαγές γραμμής, λανθασμένα αναγνωρισμένους χαρακτήρες ή ελλιπή πεδία—ακριβώς ο λόγος που θα φέρουμε ένα μοντέλο γλώσσας στη συνέχεια.

## Βήμα 4: Λήψη Μοντέλου Hugging Face – Διαμόρφωση του LLM Post‑Processor

Εδώ είναι που το βήμα **λήψη μοντέλου Hugging Face** ξεχωρίζει. Το Aspose AI μπορεί αυτόματα να κατεβάσει ένα μοντέλο από το κέντρο Hugging Face αν δεν υπάρχει ήδη στον δίσκο. Θα χρησιμοποιήσουμε το μοντέλο Qwen2.5‑3B‑Instruct‑GGUF, το οποίο ισορροπεί την ακρίβεια και το αποτύπωμα μνήμης.

```python
# Step 4: Set up the AI model configuration
ai_cfg = AsposeAIModelConfig(
    allow_auto_download="true",               # automatically fetch model if missing
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",         # int8 quantization cuts RAM usage dramatically
    gpu_layers=20,                            # first 20 layers run on GPU, rest on CPU
    directory_model_path="YOUR_DIRECTORY/asp_ocr_models"
)
```

> **Γιατί λειτουργεί:** Η `allow_auto_download` σας εξοικονομεί το χειροκίνητο κατέβασμα του αρχείου `.gguf`. Η ποσοτικοποίηση (`int8`) μειώνει το μέγεθος του μοντέλου σε περίπου 3 GB, καθιστώντας το εφικτό στα περισσότερα καταναλωτικά GPU. Ρυθμίστε το `gpu_layers` ανάλογα με το υλικό σας—περισσότερα στρώματα στο GPU = ταχύτερη εκτίμηση.

## Βήμα 5: Εξαγωγή Κειμένου από Τιμολόγιο Χρησιμοποιώντας AI‑Βελτιωμένη Μετα‑Επεξεργασία

Τώρα συνδέουμε το LLM στη μηχανή OCR και τρέχουμε έναν **post‑processor** που καθαρίζει την ακατέργαστη έξοδο, διορθώνει λάθη OCR και μορφοποιεί τα πεδία του τιμολογίου όμορφα.

```python
# Step 5: Initialize the AI engine and bind it to the OCR engine
ai_engine = AsposeAI()
ai_engine.initialize(ai_cfg)                 # implicit when using set_post_processor in newer versions
engine.set_post_processor(ai_engine)

# Run the AI‑enhanced post‑processor
enhanced_result = engine.run_postprocessor(raw_result)
print("\nEnhanced text:")
print(enhanced_result.text)
```

**Δείγμα βελτιωμένης εξόδου:**

```
Enhanced text:
Invoice Number: 12345
Date: 2024-04-01
Bill To: Acme Corp.
Amount Due: $1,250.00
Status: Paid
```

> **Τι συνέβη;** Το LLM αναγνώρισε ότι το “Invoice #12345” πρέπει να είναι “Invoice Number: 12345”, διόρθωσε τη μορφή της ημερομηνίας και ακόμη συνέλαβε το πεδίο “Bill To” που η ακατέργαστη μηχανή παρέλειψε. Αυτό είναι το βασικό στοιχείο της αυτοματοποίησης **εξαγωγής κειμένου από τιμολόγιο**.

## Βήμα 6: Απελευθέρωση Πόρων GPU – Καθαρισμός μετά την Επεξεργασία

Αν εκτελείτε αυτό σε μια μακροχρόνια υπηρεσία (π.χ., ένα Flask API), πρέπει να **απελευθερώσετε πόρους GPU** μετά από κάθε εκτίμηση για να αποφύγετε καταρρεύσεις λόγω έλλειψης μνήμης. Το Aspose AI παρέχει μια απλή μέθοδο γι' αυτό.

```python
# Step 6: Release GPU memory and dispose of the engine
ai_engine.free_resources()   # frees GPU layers and model tensors
engine.dispose()             # cleans up internal buffers
```

> **Επαγγελματική συμβουλή:** Καλέστε το `free_resources()` μέσα σε ένα μπλοκ `finally:` αν τυλίγετε την κλήση OCR σε try/except. Αυτό εγγυάται τον καθαρισμό ακόμη και όταν προκύψει εξαίρεση.

## Βήμα 7: Πλήρες Script – Συνδυάστε Όλα Μαζί

Παρακάτω είναι το πλήρες, έτοιμο‑να‑τρέξει script. Αντιγράψτε‑και‑επικολλήστε το, προσαρμόστε τις διαδρομές, και είστε έτοιμοι.

```python
import asposeocr as ocr
from asposeocr.ai import AsposeAI, AsposeAIModelConfig

# 1️⃣ Create OCR engine
engine = ocr.OcrEngine()

# 2️⃣ Load image for OCR
engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

# 3️⃣ Raw OCR
raw_result = engine.recognize()
print("Raw text:")
print(raw_result.text)

# 4️⃣ Download Hugging Face model (auto‑download enabled)
ai_cfg = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,
    directory_model_path="YOUR_DIRECTORY/asp_ocr_models"
)

# 5️⃣ Attach AI post‑processor and enhance text
ai_engine = AsposeAI()
ai_engine.initialize(ai_cfg)          # optional in newer versions
engine.set_post_processor(ai_engine)

enhanced_result = engine.run_postprocessor(raw_result)
print("\nEnhanced text:")
print(enhanced_result.text)

# 6️⃣ Free GPU resources
ai_engine.free_resources()
engine.dispose()
```

Τρέξτε το script και παρακολουθήστε τη μεταμόρφωση από θορυβώδη OCR σε καθαρά, δομημένα δεδομένα τιμολογίου. 🎉

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

| Ερώτηση | Απάντηση |
|----------|--------|
| **Τι γίνεται αν το μοντέλο δεν κατέβει;** | Βεβαιωθείτε ότι ο υπολογιστής σας έχει πρόσβαση στο internet και ότι το `hugging_face_repo_id` είναι σωστό. Μπορείτε επίσης να κατεβάσετε χειροκίνητα το |

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Εξαγωγή Κειμένου από Εικόνα – Βελτιστοποίηση OCR με Aspose.OCR για .NET](/ocr/english/net/ocr-optimization/)
- [Μετατροπή Εικόνας σε Κείμενο – Εκτέλεση OCR σε Εικόνα από URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}