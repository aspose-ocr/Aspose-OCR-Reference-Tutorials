---
category: general
date: 2026-02-09
description: πώς να εκτελέσετε OCR χρησιμοποιώντας το Aspose AI και ένα μοντέλο Hugging
  Face – μάθετε πώς να κατεβάζετε το μοντέλο Hugging Face, να διορθώνετε τα σφάλματα
  OCR και να ελευθερώνετε τη μνήμη GPU.
draft: false
keywords:
- how to run OCR
- download hugging face model
- free gpu memory
- how to free gpu
- correct OCR errors
language: el
og_description: πώς να εκτελέσετε OCR με το Aspose AI εξηγείται στην πρώτη παράγραφο
  – ανακαλύψτε πώς να κατεβάσετε το μοντέλο Hugging Face, να διορθώσετε σφάλματα OCR
  και να ελευθερώσετε μνήμη GPU.
og_title: πώς να εκτελέσετε OCR με το Aspose AI – Πλήρης Οδηγός
tags:
- OCR
- Aspose
- AI
- HuggingFace
title: Πώς να εκτελέσετε OCR με το Aspose AI – Οδηγός βήμα‑βήμα
url: /el/python/general/how-to-run-ocr-with-aspose-ai-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# πώς να εκτελέσετε OCR με Aspose AI – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να εκτελέσετε OCR** σε μια σαρωμένη απόδειξη και να λάβετε τέλεια καθαρούς αριθμούς χωρίς να ξοδεύετε ώρες διορθώνοντας τυπογραφικά λάθη; Δεν είστε μόνοι. Σε πολλά πραγματικά έργα το ακατέργαστο κείμενο που προέρχεται από μια κλασική μηχανή OCR περιέχει ακόμη αχρείαστους χαρακτήρες, σπασμένα σύμβολα νομισμάτων ή παραμορφωμένους αριθμούς — ειδικά όταν η πηγή εικόνας είναι θορυβώδης.  

Τα καλά νέα είναι ότι μπορείτε να συνδέσετε ένα LLM με το Aspose OCR, να κατεβάσετε ένα μοντέλο Hugging Face εν κινήσει και να αφήσετε την AI να τελειοποιήσει το αποτέλεσμα για εσάς. Σε αυτό το tutorial θα περάσουμε από όλο το pipeline, από την λήψη του μοντέλου (ναι, θα σας δείξουμε πώς να **download hugging face model** αυτόματα) μέχρι την απελευθέρωση των πόρων GPU όταν τελειώσετε. Στο τέλος θα έχετε ένα επαναλήψιμο script που **corrects OCR errors**, τρέχει γρήγορα σε ένα μέτριο GPU και καθαρίζει μετά από τον εαυτό του ώστε να μην σπαταλάτε μνήμη.

## Τι Θα Μάθετε

- Διαμόρφωση του Aspose AI για λήψη ενός μοντέλου **Qwen2.5‑3B‑Instruct‑GGUF** από το Hugging Face.  
- Εκτέλεση του τυπικού κινητήρα Aspose OCR σε αρχείο εικόνας.  
- Χρήση προσαρμοσμένου prompt LLM που διατηρεί ακέραιους τους αριθμούς και τα σύμβολα νομισμάτων.  
- Απελευθέρωση μνήμης GPU με τη ενσωματωμένη ρουτίνα **free gpu memory**.  
- Προσαρμογή της ροής εργασίας για ειδικές περιπτώσεις όπως πολυ‑σελίδες PDF ή χαμηλής ισχύος GPUs.

> **Prerequisites** – Python 3.9+, πακέτο `aspose-ocr`, πρόσβαση στο internet για το πρώτο λήψη μοντέλου, και GPU με τουλάχιστον 4 GB VRAM (προαιρετικό αλλά συνιστάται). Αν δεν έχετε GPU, το script θα μεταβεί αυτόματα σε CPU για τα υπόλοιπα επίπεδα.

---

## Πώς να Εκτελέσετε OCR και να Βελτιώσετε τα Αποτελέσματα

Παρακάτω βρίσκεται το πλήρες, έτοιμο‑για‑εκτέλεση Python script. Αποθηκεύστε το ως `ocr_with_ai.py` και αντικαταστήστε τις διαδρομές placeholder με τα δικά σας αρχεία.

```python
# ocr_with_ai.py
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1 – Configure the AI engine (download hugging face model)
# -------------------------------------------------
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",                     # auto‑download if missing
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # tiny memory footprint
    gpu_layers=20,                                  # 20 layers on GPU, rest on CPU
    directory_model_path=r"YOUR_DIRECTORY/Models"  # optional custom folder
)
ai = AsposeAI(ai_config)

# -------------------------------------------------
# Step 2 – Load an image and run the classic OCR engine
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()   # returns plain‑text string

# -------------------------------------------------
# Step 3 – Register a custom LLM prompt (correct OCR errors)
# -------------------------------------------------
def financial_prompt():
    # Bias the model toward financial terminology
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# -------------------------------------------------
# Step 4 – Let the LLM polish the output
# -------------------------------------------------
corrected_text = ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Enhanced :", corrected_text)

# -------------------------------------------------
# Step 5 – Release resources (free gpu memory)
# -------------------------------------------------
ai.free_resources()
```

> **Pro tip:** Η παράμετρος `gpu_layers` σας επιτρέπει να αποφασίσετε πόσα επίπεδα transformer θα παραμείνουν στο GPU. Αν αντιμετωπίζετε σφάλματα «out‑of‑memory», μειώστε αυτόν τον αριθμό και το υπόλοιπο θα τρέξει σε CPU – θα μπορείτε ακόμη να **free gpu memory** αργότερα με `ai.free_resources()`.

### Αναμενόμενο Αποτέλεσμα

Η εκτέλεση του script σε ένα δείγμα απόδειξης δίνει κάτι σαν:

```
Original : Invoic # 12345 \n Total: $1O0.00\n Date: 2023-07-15
Enhanced : Invoice # 12345
Total: $100.00
Date: 2023-07-15
```

Δείτε πώς η AI διόρθωσε το “O” στο `$1O0.00` σε μηδέν, διατηρώντας το σύμβολο δολαρίου. Αυτή είναι η ουσία του **correct OCR errors** για οικονομικά έγγραφα.

---

## Λήψη Μοντέλου Hugging Face – Τι Συμβαίνει Πίσω από τις Σκηνές;

Όταν ορίσετε `allow_auto_download="true"` το wrapper του Aspose AI ελέγχει το `directory_model_path`. Αν τα αρχεία μοντέλου δεν υπάρχουν, επικοινωνεί με το Hugging Face Hub, κατεβάζει την **int8‑quantized** έκδοση του `Qwen2.5‑3B‑Instruct‑GGUF` και τα αποθηκεύει τοπικά. Αυτή η εφάπαξ λήψη είναι συνήθως κάτω από 2 GB, καθιστώντας την εφικτή ακόμη και σε μέτριους SSD.

> **Γιατί int8;** Η ποσοτικοποίηση σε 8‑bit μειώνει δραστικά τη χρήση μνήμης — κρίσιμο όταν θέλετε επίσης να **free gpu memory** μετά την επεξεργασία. Η ανταλλαγή είναι μια μικρή απώλεια ακρίβειας, αλλά για post‑processing κειμένου OCR η επίδραση είναι αμελητέα.

Αν προτιμάτε να φιλοξενήσετε το μοντέλο εσείς, απλώς τοποθετήστε τα αρχεία `.gguf` στο `YOUR_DIRECTORY/Models` και το Aspose θα τα εντοπίσει χωρίς να χρειαστεί ξανά internet.

---

## Πώς να Απελευθερώσετε GPU – Καλύτερες Πρακτικές

Οι πόροι GPU είναι κοινόχρηστο αγαθό σε πολλά εργαστήρια. Η διατήρηση tensors ζωντανών μετά το τέλος του script μπορεί να προκαλέσει σφάλματα «CUDA out of memory» για επόμενες εργασίες. Η κλήση `ai.free_resources()` κάνει τρία πράγματα:

1. **Καταστρέφει τον υποκείμενο transformer** – όλες οι βάρη που βρίσκονται στο GPU απελευθερώνονται.  
2. **Καθαρίζει την κρυφή μνήμη PyTorch** – καλείται εσωτερικά το `torch.cuda.empty_cache()`.  
3. **Διαγράφει προσωρινά αρχεία** – οποιεσδήποτε κρυφές μνήμες στο δίσκο που δημιουργήθηκαν κατά τη λήψη αφαιρούνται.

Μπορείτε επίσης να καλέσετε χειροκίνητα το `torch.cuda.empty_cache()` αν συνδυάζετε το Aspose AI με άλλες εργασίες PyTorch, αλλά η ενσωματωμένη μέθοδος συνήθως αρκεί.

---

## Βήμα‑βήμα Οδηγός (H2s με Δευτερεύουσες Λέξεις‑Κλειδιά)

### Λήψη Μοντέλου Hugging Face Αυτόματα

Ο κατασκευαστής `AsposeAIModelConfig` κρύβει την πολυπλοκότητα της αλληλεπίδρασης με το Hugging Face API. Απλώς βεβαιωθείτε ότι έχετε πρόσβαση στο internet την πρώτη φορά που τρέχετε το script. Μετά από αυτό, το μοντέλο ζει στο `YOUR_DIRECTORY/Models` και οι επόμενες εκτελέσεις ξεκινούν αμέσως.

### Απελευθέρωση Μνήμης GPU Μετά την Πρόβλεψη

Αν τρέχετε αυτό μέσα σε μια μακροχρόνια υπηρεσία (π.χ. Flask API), καλέστε `ai.free_resources()` μετά από κάθε αίτημα. Αυτό αποτρέπει διαρροές μνήμης και εξασφαλίζει ότι το επόμενο αίτημα μπορεί να χρησιμοποιήσει το ίδιο GPU χωρίς προβλήματα.

### Διόρθωση Σφαλμάτων OCR με Προσαρμοσμένο Prompt

Η συνάρτηση `financial_prompt` επιστρέφει ένα dictionary με ένα μόνο κλειδί `prompt`. Μπορείτε να το προσαρμόσετε σε οποιονδήποτε τομέα:

```python
def medical_prompt():
    return {"prompt": "Fix OCR mistakes, keep dosage numbers and units unchanged"}
```

Αλλάξτε το όνομα της συνάρτησης στο `ai.set_post_processor(...)` και έχετε μια **correct OCR errors** ροή εργασίας για ιατρικά αρχεία.

### Πώς να Εκτελέσετε OCR σε Πολυ‑σελίδες PDF

Το Aspose OCR μπορεί να χειριστεί PDF απευθείας:

```python
ocr_engine.load_document(r"YOUR_DIRECTORY/multi_page.pdf")
raw_text = ocr_engine.recognize()  # concatenates pages automatically
```

Αφού λάβετε το ακατέργαστο κείμενο, ο ίδιος LLM post‑processor θα καθαρίσει το κείμενο κάθε σελίδας. Δεν χρειάζεται επιπλέον κώδικας.

### Όταν Δεν Έχετε GPU – Πώς να Απελευθερώσετε GPU (Ακόμη και Χωρίς Ένα)

Ακόμη και σε μηχανήματα μόνο με CPU, η κλήση `ai.free_resources()` δεν προκαλεί προβλήματα. Απλώς καθαρίζει εσωτερικές κρυφές μνήμες, που μπορεί ακόμη να ελευθερώσει RAM. Έτσι η συμβουλή **how to free gpu** ισχύει παντού: πάντα καθαρίζετε μετά τη χρήση.

---

## Συνηθισμένα Προβλήματα & Πώς Τα Επιλύσαμε

| Πρόβλημα | Γιατί Συμβαίνει | Λύση |
|----------|----------------|------|
| **Out‑of‑Memory στο GPU** | `gpu_layers` ορίστηκε πολύ υψηλό για την κάρτα σας | Μειώστε το `gpu_layers` σε 10 ή 5, αφήνοντας το υπόλοιπο να τρέξει σε CPU |
| **Το μοντέλο δεν κατεβάζεται ποτέ** | Το εταιρικό firewall μπλοκάρει HTTPS προς huggingface.co | Κατεβάστε το μοντέλο χειροκίνητα από άλλο δίκτυο, μετά κατευθύνετε το `directory_model_path` στο τοπικό φάκελο |
| **Οι αριθμοί καταστρέφονται** | Το prompt δεν είναι αρκετά σαφές για διατήρηση ψηφίων | Προσθέστε “preserve all numeric values and currency symbols exactly as they appear” στο prompt |
| **`free_resources` προκαλεί εξαίρεση** | Χρήση παλαιότερης έκδοσης Aspose OCR | Αναβαθμίστε στην τελευταία έκδοση του πακέτου `aspose-ocr` (pip install --upgrade aspose-ocr) |

---

## Πλήρης Παράδειγμα Ανακεφαλαίωση

Εδώ είναι ξανά το script, αυτή τη φορά με ενσωματωμένα σχόλια που εξηγούν κάθε γραμμή για μελλοντική αναφορά:

```python
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# 1️⃣ Configure AI – will auto‑download the model if needed
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,                     # adjust based on your GPU size
    directory_model_path=r"YOUR_DIRECTORY/Models"
)
ai = AsposeAI(ai_config)               # initialise the engine

# 2️⃣ Run classic OCR on an image (or PDF)
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()      # plain‑text result

# 3️⃣ Define a prompt that tells the LLM to keep numbers intact
def financial_prompt():
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# 4️⃣ Let the LLM clean the text
corrected_text = ai.run_postprocessor(raw_text)

# 5️⃣ Show before/after
print("Original :", raw_text)
print("Enhanced :", corrected_text)

# 6️⃣ Clean up – this frees GPU memory for the next run
ai.free_resources()
```

---

## Συμπέρασμα

Καλύψαμε **πώς να εκτελέσετε OCR** με το Aspose, να κατεβάσετε ένα μοντέλο Hugging Face κατ’ απαίτηση, να δημιουργήσετε ένα prompt που **corrects OCR errors**, και τέλος να **free gpu memory** ώστε ο σταθμός εργασίας σας να παραμένει ανταποκρινόμενος. Ολόκληρη η ροή εργασίας χωράει σε ένα μόνο, αυτόνομο αρχείο Python — χωρίς εξωτερικά scripts, χωρίς χειροκίνητη διαχείριση μοντέλων, και χωρίς εναπομείναντες πόροι GPU.

Επόμενα βήματα; Δοκιμάστε να αντικαταστήσετε το `financial_prompt` με ένα

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}