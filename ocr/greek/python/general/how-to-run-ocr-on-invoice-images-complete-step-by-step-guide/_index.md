---
category: general
date: 2026-01-12
description: Πώς να εκτελέσετε OCR και να εξάγετε κείμενο από εικόνες τιμολογίων χρησιμοποιώντας
  το Aspose OCR και ένα ελαφρύ μοντέλο Hugging Face. Μάθετε πώς να κατεβάσετε το μοντέλο,
  να διορθώσετε τα σφάλματα OCR και να εκτελέσετε OCR στην εικόνα.
draft: false
keywords:
- how to run OCR
- extract text from invoice
- download hugging face model
- correct OCR errors
- perform OCR on image
language: el
og_description: Πώς να εκτελέσετε OCR σε εικόνες τιμολογίων, να εξάγετε κείμενο και
  να διορθώσετε σφάλματα με ένα LLM της Hugging Face. Ακολουθήστε αυτόν τον πλήρη
  οδηγό για άψογα αποτελέσματα.
og_title: Πώς να εκτελέσετε OCR σε εικόνες τιμολογίων – Πλήρης οδηγός
tags:
- OCR
- Python
- AI post‑processing
- Hugging Face
title: Πώς να εκτελέσετε OCR σε εικόνες τιμολογίων – Πλήρης οδηγός βήμα‑προς‑βήμα
url: /el/python/general/how-to-run-ocr-on-invoice-images-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εκτελέσετε OCR σε Εικόνες Τιμολογίων – Ολοκληρωμένος Οδηγός Βήμα‑Βήμα

Έχετε αναρωτηθεί ποτέ **πώς να εκτελέσετε OCR** σε ένα σαρωμένο τιμολόγιο και να πάρετε καθαρό, αναζητήσιμο κείμενο χωρίς να ξοδέψετε ώρες στην επεξεργασία του; Δεν είστε μόνοι. Σε πολλά πραγματικά έργα η ακατέργαστη έξοδος του OCR είναι γεμάτη λανθασμένες αναγνώσεις—π.χ. “O” αντί για “0”, “l” αντί για “1”, ή ακόμη και ολόκληρες λέξεις παραμορφωμένες. Τα καλά νέα; Με λίγες γραμμές Python μπορείτε όχι μόνο να **εκτελέσετε OCR σε εικόνα** αλλά και αυτόματα να **διορθώσετε σφάλματα OCR** χρησιμοποιώντας ένα ελαφρύ μοντέλο από το Hugging Face.

Σε αυτό το tutorial θα περάσουμε από όλα όσα χρειάζεστε: από τη φόρτωση μιας εικόνας τιμολογίου, την εξαγωγή ακατέργαστου κειμένου, τη λήψη ενός ποσοτικοποιημένου μοντέλου, μέχρι την τελειοποίηση του αποτελέσματος ώστε να έχετε μια τέλεια μεταγραφή έτοιμη για επεξεργασία. Στο τέλος θα μπορείτε να **εξάγετε κείμενο από τιμολόγια** σε PDF ή PNG με ένα ενιαίο, επαναλήψιμο script.

## Προαπαιτήσεις & Ρύθμιση

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|------------------------|
| Python 3.9+ | Σύγχρονη σύνταξη και type hints |
| `aspose-ocr` package | Παρέχει το `ocr.OcrEngine` που χρησιμοποιείται στο παράδειγμα |
| `aspose-ai` package | Προσφέρει το post‑processor `AsposeAI` |
| Πρόσβαση σε GPU (προαιρετικό) | Επιταχύνει τα επίπεδα LLM· διαφορετικά λειτουργεί καλά και με CPU |
| Σύνδεση στο Internet (πρώτη εκτέλεση) | Απαιτείται για **λήψη μοντέλου Hugging Face** αυτόματα |

Μπορείτε να εγκαταστήσετε τις απαιτούμενες βιβλιοθήκες με:

```bash
pip install aspose-ocr aspose-ai
```

> **Pro tip:** Αν σκοπεύετε να τρέξετε το LLM σε GPU, εγκαταστήστε το `torch` με υποστήριξη CUDA (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu118`).

Τώρα που το περιβάλλον είναι έτοιμο, ας περάσουμε στον κώδικα.

---

## Βήμα 1 – Αρχικοποίηση του OCR Engine και Φόρτωση της Εικόνας Τιμολογίου

Το πρώτο που πρέπει να κάνετε είναι να δημιουργήσετε μια παρουσία του OCR engine της Aspose και να την κατευθύνετε στο αρχείο που θέλετε να επεξεργαστείτε. Αυτό το βήμα αποτελεί τη βάση του **πώς να εκτελέσετε OCR** σε οποιαδήποτε εικόνα.

```python
import ocr  # Aspose OCR package

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Load the invoice you want to read
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
```

> **Γιατί είναι σημαντικό:** Η `load_image` δέχεται PNG, JPEG, TIFF, και ακόμη και σελίδες PDF, επιτρέποντάς σας να **εκτελέσετε OCR σε εικόνα** ανεξαρτήτως μορφής.

---

## Βήμα 2 – Εκτέλεση Βασικού OCR για Λήψη Ακατέργαστου Κειμένου

Μόλις η εικόνα φορτωθεί, η μηχανή μπορεί να παράγει μια ακατέργαστη μεταγραφή. Αυτή η έξοδος είναι συχνά θορυβώδης, γι' αυτό αργότερα θα τρέξουμε ένα βήμα διόρθωσης.

```python
# Perform the OCR scan
raw_result = ocr_engine.recognize()

# Show what the engine saw
print("Raw OCR:", raw_result.text)
```

Τυπική ακατέργαστη έξοδος μπορεί να μοιάζει με:

```
Raw OCR: Inv0ice No: 12345
Date: 2023/07/15
Total Am0unt: $1,200.00
```

Παρατηρήσατε τα μηδενικά (`0`) όπου θα έπρεπε να είναι το γράμμα “O”; Αυτό είναι ακριβώς το είδος του λάθους που θα διορθώσουμε αργότερα.

---

## Βήμα 3 – Διαμόρφωση του AI Post‑Processor με Ελαφρύ LLM

Τώρα φέρνουμε ένα **λήψη μοντέλου Hugging Face** που είναι αρκετά μικρό για να τρέξει σε μέτριο υλικό, αλλά αρκετά ισχυρό για να κατανοήσει τη γλώσσα των τιμολογίων. Το παράδειγμα χρησιμοποιεί το μοντέλο Qwen 2.5 3B‑Instruct GGUF, ποσοτικοποιημένο σε `int8` για ελάχιστη μνήμη.

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Define model configuration
model_config = AsposeAIModelConfig(
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",          # reduces size dramatically
    gpu_layers=20,                             # use GPU for the first 20 layers if available
    allow_auto_download="true"                # pulls the model on first run
)

# Initialise the AI processor and attach the post‑processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("llm_correction", model_config)
```

> **Γιατί αυτό το μοντέλο;** Η ποσοτικοποίηση `int8` μειώνει το αρχείο σε ~1,2 GB, καθιστώντας το εφικτό στα περισσότερα laptops. Τα επίπεδα GPU επιταχύνουν την πρόβλεψη, αλλά ο κώδικας επιστρέφει αυτόματα σε CPU αν δεν βρεθεί GPU.

---

## Βήμα 4 – Εκτέλεση Διόρθωσης με Βάση το LLM στο Ακατέργαστο OCR Αποτέλεσμα

Με το μοντέλο έτοιμο, τροφοδοτούμε το ακατέργαστο κείμενο στο post‑processor. Το LLM θα ξαναγράψει τη μεταγραφή, διορθώνοντας κοινά σφάλματα OCR και ομαλοποιώντας τους αριθμούς.

```python
# Apply AI correction
corrected_result = ai_processor.run_postprocessor(raw_result)

# Display the cleaned output
print("AI‑corrected:", corrected_result.text)
```

Αναμενόμενη καθαρή έξοδος:

```
AI‑corrected: Invoice No: 12345
Date: 2023/07/15
Total Amount: $1,200.00
```

Βλέπετε ότι τα μηδενικά έχουν μετατραπεί ξανά σε γράμμα “O”, και το “Am0unt” είναι τώρα “Amount”. Αυτό αποτελεί τον πυρήνα του **αυτόματου διορθώματος σφαλμάτων OCR**.

---

## Βήμα 5 – Απελευθέρωση Πόρων και Καθαρισμός

Τα μεγάλα γλωσσικά μοντέλα μπορούν να κρατήσουν μνήμη GPU, γι' αυτό είναι καλή πρακτική να ελευθερώνονται οι πόροι όταν τελειώσετε.

```python
# Free the model and any GPU buffers
ai_processor.free_resources()
```

Αν σκοπεύετε να επεξεργαστείτε πολλά τιμολόγια σε batch, μπορείτε να κρατήσετε το μοντέλο φορτωμένο και να το ελευθερώσετε μόνο στο τέλος του script.

---

## Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας τα παραπάνω, εδώ είναι ένα ενιαίο script που μπορείτε να αποθηκεύσετε σε αρχείο `.py` και να τρέξετε:

```python
# ------------------------------------------------------------
# How to Run OCR on Invoice Images – End‑to‑End Example
# ------------------------------------------------------------
import ocr
from aspose_ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = ocr.OcrEngine()
    ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Capture raw OCR text
    raw_result = ocr_engine.recognize()
    print("Raw OCR:", raw_result.text)

    # 3️⃣ Configure lightweight LLM from Hugging Face
    model_cfg = AsposeAIModelConfig(
        hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
        hugging_face_quantization="int8",
        gpu_layers=20,
        allow_auto_download="true"
    )
    ai = AsposeAI()
    ai.set_post_processor("llm_correction", model_cfg)

    # 4️⃣ Run AI correction
    corrected = ai.run_postprocessor(raw_result)
    print("AI‑corrected:", corrected.text)

    # 5️⃣ Clean up
    ai.free_resources()

if __name__ == "__main__":
    main()
```

Η εκτέλεση του script θα πρέπει να παράγει έξοδο παρόμοια με το μπλοκ “AI‑corrected” που εμφανίστηκε νωρίτερα. Αλλάξτε το μονοπάτι της εικόνας με οποιοδήποτε άλλο τιμολόγιο ή απόδειξη για να **εξάγετε κείμενο από τιμολόγια** μαζικά.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν δεν έχω GPU;

Η παράμετρος `gpu_layers` είναι προαιρετική. Ορίστε την σε `0` ή παραλείψτε την, και το μοντέλο θα τρέξει εξ ολοκλήρου σε CPU. Αναμένετε πιο αργή πρόβλεψη—περίπου 2–3 δευτερόλεπτα ανά σελίδα σε σύγχρονο laptop.

### Τα τιμολόγιά μου είναι PDF πολλαπλών σελίδων. Πώς τα διαχειρίζομαι;

Μετατρέψτε κάθε σελίδα σε ξεχωριστή εικόνα (π.χ., με `pdf2image`) και κάντε βρόχο στις σελίδες με το ίδιο script. Το OCR engine μπορεί να επεξεργαστεί κάθε εικόνα ανεξάρτητα, και το LLM θα διορθώσει κάθε μπλοκ κειμένου.

```python
from pdf2image import convert_from_path

pages = convert_from_path("invoice.pdf", dpi=300)
for i, page_img in enumerate(pages):
    ocr_engine.load_image(page_img)
    # …run steps 2‑4…
```

### Η λήψη του μοντέλου αποτυγχάνει πίσω από τείχος προστασίας;

Κατεβάστε το μοντέλο χειροκίνητα από το Hugging Face model hub, αποσυμπιέστε το σε τοπικό φάκελο, και ορίστε το `hugging_face_repo_id` στη διαδρομή του τοπικού φακέλου:

```python
model_cfg = AsposeAIModelConfig(
    hugging_face_repo_id="/local/path/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,
    allow_auto_download="false"
)
```

### Πόσο ακριβής είναι η διόρθωση;

Για τυπικά τιμολόγια στα αγγλικά, το LLM διορθώνει >95 % των κοινών σφαλμάτων OCR. Πολύπλοκες χειρόγραφες σημειώσεις μπορεί να χρειάζονται ακόμη χειροκίνητη επανεξέταση.

---

## Συμβουλές & Τεχνάσματα για Παραγωγική Χρήση

- **Batch processing:** Τυλίξτε τα βήματα 2‑4 σε μια συνάρτηση και περάστε μια λίστα διαδρομών αρχείων. Επαναχρησιμοποιήστε την ίδια παρουσία `AsposeAI` για να αποφύγετε την επαναφόρτωση του μοντέλου.
- **Logging:** Αντικαταστήστε το `print` με το module `logging` της Python για να καταγράφετε τόσο το ακατέργαστο όσο και το διορθωμένο κείμενο για σκοπούς ελέγχου.
- **Error handling:** Περιβάλλετε την κλήση OCR με `try/except`. Αν μια εικόνα αποτύχει, καταγράψτε το όνομα αρχείου και συνεχίστε.
- **Performance tuning:** Πειραματιστείτε με το `gpu_layers`. Περισσότερα επίπεδα στο GPU επιταχύνουν την πρόβλεψη αλλά αυξάνουν τη χρήση VRAM.

---

## Συμπέρασμα

Καλύψαμε **πώς να εκτελέσετε OCR** σε εικόνες τιμολογίων από την αρχή μέχρι το τέλος, δείχνοντας πώς να **εκτελέσετε OCR σε εικόνα**, **λήψη μοντέλου Hugging Face**, και **αυτόματη διόρθωση σφαλμάτων OCR**. Το πλήρες script παρουσιάζει μια πρακτική ροή εργασίας που μπορείτε να ενσωματώσετε σε οποιοδήποτε pipeline αυτοματοποίησης με Python.

Τι θα ακολουθήσει; Δοκιμάστε να επεκτείνετε το pipeline για **εξαγωγή βασικών πεδίων** (αριθμός τιμολογίου, ημερομηνία, σύνολο) χρησιμοποιώντας κανονικές εκφράσεις στο διορθωμένο κείμενο, ή στείλτε το καθαρό αποτέλεσμα σε βάση δεδομένων για αναζητήσιμα αρχεία. Μπορείτε επίσης να πειραματιστείτε με άλλα ελαφριά LLMs από το Hugging Face αν χρειάζεστε διαφορετική γλώσσα ή εξειδικευμένη γνώση.

Καλή προγραμματιστική δουλειά, και εύχομαι τα αποτελέσματα OCR σας να είναι πάντα kristalliká! 

![πώς να εκτελέσετε OCR σε εικόνα τιμολογίου](ocr_invoice_example.png "πώς να εκτελέσετε OCR σε τιμολόγιο")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}