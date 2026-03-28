---
category: general
date: 2026-03-28
description: Μάθετε πώς να εκτελείτε OCR σε εικόνα, να κατεβάζετε αυτόματα το μοντέλο
  Hugging Face, να καθαρίζετε το κείμενο OCR και να διαμορφώνετε το μοντέλο LLM σε
  Python χρησιμοποιώντας το Aspose OCR Cloud.
draft: false
keywords:
- run OCR on image
- download hugging face model
- clean OCR text
- configure LLM model
language: el
og_description: Εκτελέστε OCR σε εικόνα και καθαρίστε το αποτέλεσμα χρησιμοποιώντας
  ένα αυτόματα ληφθέν μοντέλο Hugging Face. Αυτός ο οδηγός δείχνει πώς να διαμορφώσετε
  το μοντέλο LLM στην Python.
og_title: Εκτέλεση OCR σε εικόνα – Πλήρης οδηγός Aspose OCR Cloud
tags:
- OCR
- Python
- LLM
- HuggingFace
title: Εκτελέστε OCR σε εικόνα με το Aspose OCR Cloud – Πλήρης οδηγός βήμα‑προς‑βήμα
url: /el/python/general/run-ocr-on-image-with-aspose-ocr-cloud-full-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε εικόνα – Πλήρης οδηγός Aspose OCR Cloud

Έχετε χρειαστεί ποτέ να τρέξετε OCR σε αρχεία εικόνας αλλά το ακατέργαστο αποτέλεσμα να φαίνεται σαν ακατάστατο μπέρδεμα; Από την εμπειρία μου το μεγαλύτερο πρόβλημα δεν είναι η αναγνώριση αυτή καθαυτή—είναι ο καθαρισμός. Ευτυχώς, το Aspose OCR Cloud σας επιτρέπει να συνδέσετε έναν LLM post‑processor που μπορεί να *καθαρίσει το κείμενο OCR* αυτόματα. Σε αυτό το tutorial θα περάσουμε από όλα όσα χρειάζεστε: από **τη λήψη ενός μοντέλου Hugging Face** μέχρι τη ρύθμιση του LLM, την εκτέλεση της μηχανής OCR και, τέλος, την τελική επεξεργασία του αποτελέσματος.

Στο τέλος αυτού του οδηγού θα έχετε ένα έτοιμο‑για‑εκτέλεση script που:

1. Κατεβάζει ένα συμπαγές μοντέλο Qwen 2.5 από το Hugging Face (αυτόματα για εσάς).  
2. Ρυθμίζει το μοντέλο ώστε να τρέχει μέρος του δικτύου στην GPU και το υπόλοιπο στην CPU.  
3. Εκτελεί τη μηχανή OCR σε μια εικόνα χειρόγραφης σημείωσης.  
4. Χρησιμοποιεί το LLM για να καθαρίσει το αναγνωρισμένο κείμενο, παρέχοντάς σας έξοδο αναγνώσιμη από άνθρωπο.

> **Προαπαιτούμενα** – Python 3.8+, πακέτο `asposeocrcloud`, GPU με τουλάχιστον 4 GB VRAM (προαιρετικό αλλά συνιστάται), και σύνδεση στο internet για την πρώτη λήψη του μοντέλου.

---

## Τι θα χρειαστείτε

- **Aspose OCR Cloud SDK** – εγκαταστήστε το με `pip install asposeocrcloud`.  
- **Ένα δείγμα εικόνας** – π.χ., `handwritten_note.jpg` τοποθετημένο σε τοπικό φάκελο.  
- **Υποστήριξη GPU** – αν διαθέτετε GPU με υποστήριξη CUDA, το script θα μεταφέρει 30 στρώματα· διαφορετικά θα επιστρέψει αυτόματα στην CPU.  
- **Δικαίωμα εγγραφής** – το script αποθηκεύει την cache του μοντέλου στο `YOUR_DIRECTORY`; βεβαιωθείτε ότι ο φάκελος υπάρχει.

---

## Βήμα 1 – Ρύθμιση του μοντέλου LLM (λήψη μοντέλου Hugging Face)

Το πρώτο που κάνουμε είναι να πούμε στο Aspose AI από πού να πάρει το μοντέλο. Η κλάση `AsposeAIModelConfig` διαχειρίζεται την αυτόματη λήψη, την ποσοτικοποίηση και την κατανομή των στρωμάτων στην GPU.

```python
import asposeocrcloud as ocr
from asposeocrcloud.ai import AsposeAI, AsposeAIModelConfig

# ----------------------------------------------------------------------
# Step 1: Model configuration – this will download the model if it’s missing
# ----------------------------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",                           # Enables auto‑download
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF", # Repo on Hugging Face
    hugging_face_quantization="int8",                     # Small footprint, fast inference
    gpu_layers=30,                                        # 30 layers on GPU, rest on CPU
    directory_model_path=r"YOUR_DIRECTORY"               # Cache folder (optional)
)
```

**Γιατί είναι σημαντικό** – Η ποσοτικοποίηση σε `int8` μειώνει δραστικά τη χρήση μνήμης (≈ 4 GB vs 12 GB). Ο διαχωρισμός του μοντέλου μεταξύ GPU και CPU σας επιτρέπει να τρέξετε ένα LLM 3 δισεκατομμυρίων παραμέτρων ακόμα και σε μια μέτρια RTX 3060. Αν δεν έχετε GPU, ορίστε `gpu_layers=0` και το SDK θα κρατήσει τα πάντα στην CPU.

> **Συμβουλή:** Η πρώτη εκτέλεση θα κατεβάσει ~ 1.5 GB, οπότε δώστε του λίγα λεπτά και μια σταθερή σύνδεση.

---

## Βήμα 2 – Αρχικοποίηση της AI Μηχανής με τη Ρύθμιση του Μοντέλου

Τώρα ξεκινάμε τη μηχανή Aspose AI και της δίνουμε τη ρύθμιση που μόλις δημιουργήσαμε.

```python
# ----------------------------------------------------------------------
# Step 2: Initialise the AI engine – pulls the model if needed
# ----------------------------------------------------------------------
ocr_ai = AsposeAI()
ocr_ai.initialize(model_config)  # This call blocks until the model is ready
```

**Τι συμβαίνει στο παρασκήνιο;** Το SDK ελέγχει το `directory_model_path` για υπάρχον μοντέλο. Αν βρει μια αντίστοιχη έκδοση, το φορτώνει αμέσως· διαφορετικά, κατεβάζει το αρχείο GGUF από το Hugging Face, το αποσυμπιέζει και προετοιμάζει τη γραμμή επεξεργασίας.

---

## Βήμα 3 – Δημιουργία της Μηχανής OCR και Σύνδεση του AI Post‑Processor

Η μηχανή OCR κάνει το βαρέως βάρους έργο της αναγνώρισης χαρακτήρων. Συνδέοντας το `ocr_ai.run_postprocessor` ενεργοποιούμε την **καθαριότητα του κειμένου OCR** αυτόματα μετά την αναγνώριση.

```python
# ----------------------------------------------------------------------
# Step 3: Build the OCR engine and bind the LLM post‑processor
# ----------------------------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_post_processor(ocr_ai.run_postprocessor, custom_settings=None)
```

**Γιατί να χρησιμοποιήσετε post‑processor;** Το ακατέργαστο OCR συχνά περιλαμβάνει αλλαγές γραμμής στα λάθος σημεία, λανθασμένη στίξη ή τυχαία σύμβολα. Το LLM μπορεί να ξαναγράψει το αποτέλεσμα σε σωστές προτάσεις, να διορθώσει ορθογραφικά λάθη και ακόμη να συμπληρώσει ελλιπή λέξεις—με άλλα λόγια, μετατρέπει ένα ακατέργαστο αρχείο σε γυαλιστερό κείμενο.

---

## Βήμα 4 – Εκτέλεση OCR σε Αρχείο Εικόνας

Με όλα συνδεδεμένα, ήρθε η ώρα να τροφοδοτήσουμε μια εικόνα στη μηχανή.

```python
# ----------------------------------------------------------------------
# Step 4: Load the image and run OCR
# ----------------------------------------------------------------------
input_image = ocr.Image.load(r"YOUR_DIRECTORY/handwritten_note.jpg")
raw_result = ocr_engine.recognize(input_image)   # Returns an OcrResult object
```

**Ακραία περίπτωση:** Αν η εικόνα είναι μεγάλη (> 5 MP), ίσως θελήσετε να την μειώσετε πρώτα για να επιταχύνετε την επεξεργασία. Το SDK δέχεται αντικείμενο Pillow `Image`, οπότε μπορείτε να προεπεξεργαστείτε με `PIL.Image.thumbnail()` αν χρειαστεί.

---

## Βήμα 5 – Αφήστε το AI να Καθαρίσει το Αναγνωρισμένο Κείμενο και Εμφανίστε Και τις Δύο Εκδόσεις

Τέλος, καλούμε τον post‑processor που συνδέσαμε νωρίτερα. Αυτό το βήμα δείχνει τη διαφορά μεταξύ *πριν* και *μετά* τον καθαρισμό.

```python
# ----------------------------------------------------------------------
# Step 5: Clean the OCR output using the LLM and display both results
# ----------------------------------------------------------------------
cleaned_result = ocr_engine.run_postprocessor(raw_result)

print("=== Before AI ===")
print(raw_result.text)

print("\n=== After AI ===")
print(cleaned_result.text)
```

### Αναμενόμενο Αποτέλεσμα

```
=== Before AI ===
Th1s 1s a h@ndwr1tt3n n0te.  It c0nta1ns m1st@k3s, l1n3 br3aks, & sp3c!@l ch@r@ct3rs.

=== After AI ===
This is a handwritten note. It contains mistakes, line breaks, and special characters.
```

Δείτε πώς το LLM:

- Διόρθωσε κοινές λανθασμένες αναγνώσεις OCR (`Th1s` → `This`).  
- Αφαίρεσε τυχαία σύμβολα (`&` → `and`).  
- Κανονικοποίησε τις αλλαγές γραμμής σε σωστές προτάσεις.

---

## 🎨 Οπτική Επισκόπηση (Ροή εργασίας Εκτέλεσης OCR σε εικόνα)

![Ροή εργασίας εκτέλεσης OCR σε εικόνα](run_ocr_on_image_workflow.png "Διάγραμμα που δείχνει τη διαδικασία εκτέλεσης OCR σε εικόνα από τη λήψη του μοντέλου μέχρι το καθαρισμένο αποτέλεσμα")

Το παραπάνω διάγραμμα συνοψίζει ολόκληρη τη διαδικασία: **λήψη μοντέλου Hugging Face → ρύθμιση LLM → αρχικοποίηση AI → μηχανή OCR → AI post‑processor → καθαρό κείμενο OCR**.

---

## Συχνές Ερωτήσεις & Επαγγελματικές Συμβουλές

### Τι κάνω αν δεν έχω GPU;

Ορίστε `gpu_layers=0` στο `AsposeAIModelConfig`. Το μοντέλο θα τρέξει εξ ολοκλήρου στην CPU, κάτι που είναι πιο αργό αλλά λειτουργικό. Μπορείτε επίσης να μεταβείτε σε μικρότερο μοντέλο (π.χ., `Qwen/Qwen2.5-1.5B‑Instruct‑GGUF`) για να διατηρήσετε λογικό χρόνο εκτέλεσης.

### Πώς αλλάζω το μοντέλο αργότερα;

Απλώς ενημερώστε το `hugging_face_repo_id` και ξανατρέξτε `ocr_ai.initialize(model_config)`. Το SDK θα εντοπίσει την αλλαγή έκδοσης, θα κατεβάσει το νέο μοντέλο και θα αντικαταστήσει τα αρχεία cache.

### Μπορώ να προσαρμόσω το prompt του post‑processor;

Ναι. Περνάτε ένα λεξικό στο `custom_settings` με κλειδί `prompt_template`. Για παράδειγμα:

```python
custom_prompt = {
    "prompt_template": "Correct the following OCR text and keep line breaks:\n{ocr_text}"
}
ocr_engine.set_post_processor(ocr_ai.run_postprocessor, custom_settings=custom_prompt)
```

### Πρέπει να αποθηκεύσω το καθαρισμένο κείμενο σε αρχείο;

Απολύτως. Μετά τον καθαρισμό μπορείτε να γράψετε το αποτέλεσμα σε αρχείο `.txt` ή `.json` για περαιτέρω επεξεργασία:

```python
with open("cleaned_note.txt", "w", encoding="utf-8") as f:
    f.write(cleaned_result.text)
```

---

## Συμπέρασμα

Σας δείξαμε πώς να **εκτελέσετε OCR σε αρχεία εικόνας** με το Aspose OCR Cloud, να **κατεβάσετε αυτόματα ένα μοντέλο Hugging Face**, να **ρυθμίσετε τις παραμέτρους του μοντέλου LLM** και, τέλος, να **καθαρίσετε το κείμενο OCR** χρησιμοποιώντας έναν ισχυρό LLM post‑processor. Η όλη διαδικασία χωράει σε ένα μόνο, εύκολο‑να‑τρέξει script Python και λειτουργεί τόσο σε μηχανές με GPU όσο και σε μηχανές μόνο με CPU.

Αν αισθάνεστε άνετα με αυτή τη ροή, δοκιμάστε:

- **Διάφορα LLM** – δοκιμάστε το `meta-llama/Meta-Llama-3-8B‑Instruct‑GGUF` για μεγαλύτερο παράθυρο συμφραζομένων.  
- **Επεξεργασία παρτίδας** – κάντε βρόχο πάνω από έναν φάκελο εικόνων και συγκεντρώστε τα καθαρισμένα αποτελέσματα σε CSV.  
- **Προσαρμοσμένα prompts** – προσαρμόστε το AI στον τομέα σας (νομικά έγγραφα, ιατρικές σημειώσεις κ.λπ.).

Αλλάξτε την τιμή `gpu_layers`, αντικαταστήστε το μοντέλο ή προσθέστε το δικό σας prompt. Ο ουρανός είναι το όριο, και ο κώδικας που έχετε τώρα είναι η πλατφόρμα εκτόξευσης.

Καλό προγραμματισμό, και οι έξοδοι OCR σας να είναι πάντα καθαροί! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}