---
category: general
date: 2026-05-03
description: Πώς να επεξεργαστείτε μαζικά εικόνες με OCR χρησιμοποιώντας το Aspose
  OCR και τον AI ορθογραφικό έλεγχο. Μάθετε να εξάγετε κείμενο από εικόνες, να εφαρμόζετε
  ορθογραφικό έλεγχο, να χρησιμοποιείτε δωρεάν πόρους AI και να διορθώνετε σφάλματα
  OCR.
draft: false
keywords:
- how to batch ocr
- extract text from images
- free ai resources
- apply spell check
- correct ocr errors
language: el
og_description: Πώς να επεξεργαστείτε μαζικά εικόνες με OCR χρησιμοποιώντας το Aspose
  OCR και τον AI ορθογραφικό έλεγχο. Ακολουθήστε έναν βήμα‑προς‑βήμα οδηγό για την
  εξαγωγή κειμένου από εικόνες, την εφαρμογή ορθογραφικού ελέγχου, τη χρήση δωρεάν
  AI πόρων και τη διόρθωση σφαλμάτων OCR.
og_title: Πώς να κάνετε μαζική OCR με το Aspose OCR – Πλήρης οδηγός Python
tags:
- OCR
- Python
- AI
- Aspose
title: Πώς να κάνετε ομαδική OCR με το Aspose OCR – Πλήρης οδηγός Python
url: /el/python/general/how-to-batch-ocr-with-aspose-ocr-full-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εκτελέσετε OCR σε Παρτίδες με Aspose OCR – Πλήρης Οδηγός Python

Έχετε αναρωτηθεί ποτέ **πώς να εκτελέσετε OCR σε παρτίδες** σε ολόκληρο φάκελο σκαναρισμένων PDF ή φωτογραφιών χωρίς να γράψετε ξεχωριστό script για κάθε αρχείο; Δεν είστε μόνοι. Σε πολλές πραγματικές ροές εργασίας θα χρειαστείτε **εξαγωγή κειμένου από εικόνες**, καθαρισμό ορθογραφικών λαθών, και τελικά την απελευθέρωση των πόρων AI που έχετε δεσμεύσει. Αυτό το tutorial σας δείχνει ακριβώς πώς να το κάνετε αυτό με το Aspose OCR, έναν ελαφρύ AI post‑processor, και με λίγες γραμμές Python.

Θα περάσουμε από την αρχικοποίηση της μηχανής OCR, τη σύνδεση ενός AI ελεγκτή ορθογραφίας, την επανάληψη σε έναν κατάλογο εικόνων, και τον καθαρισμό του μοντέλου στο τέλος. Στο τέλος θα έχετε ένα έτοιμο script που **διορθώνει αυτόματα τα σφάλματα OCR** και απελευθερώνει **ελεύθερους πόρους AI** ώστε η GPU σας να παραμένει χαρούμενη.

## Τι Θα Χρειαστείτε

- Python 3.9+ (ο κώδικας χρησιμοποιεί type‑hints αλλά λειτουργεί και σε παλαιότερες εκδόσεις 3.x)
- Πακέτο `asposeocr` (`pip install asposeocr`) – παρέχει τη μηχανή OCR.
- Πρόσβαση στο μοντέλο Hugging Face `bartowski/Qwen2.5-3B-Instruct-GGUF` (κατεβάζεται αυτόματα).
- Μια GPU με τουλάχιστον λίγες GB VRAM (το script ορίζει `gpu_layers = 30`, μπορείτε να το μειώσετε αν χρειαστεί).

Καμία εξωτερική υπηρεσία, κανένα πληρωμένο API – όλα τρέχουν τοπικά.

---

## Βήμα 1: Ρύθμιση της Μηχανής OCR – **Πώς να Εκτελέσετε OCR σε Παρτίδες** Αποτελεσματικά

Πριν μπορέσουμε να επεξεργαστούμε χίλιες εικόνες, χρειαζόμαστε μια αξιόπιστη μηχανή OCR. Το Aspose OCR μας επιτρέπει να επιλέξουμε γλώσσα και λειτουργία αναγνώρισης με μία κλήση.

```python
# Step 1: Initialize the OCR engine for English plain‑text output
def init_ocr() -> aocr.OcrEngine:
    ocr_engine = aocr.OcrEngine()
    ocr_engine.language = aocr.Language.English          # English language pack
    ocr_engine.recognize_mode = aocr.RecognitionMode.Plain  # Returns raw string, no layout
    return ocr_engine
```

**Γιατί είναι σημαντικό:** Ορίζοντας το `recognize_mode` σε `Plain` διατηρεί το αποτέλεσμα ελαφρύ, κάτι ιδανικό όταν σκοπεύετε να εκτελέσετε έλεγχο ορθογραφίας αργότερα. Αν χρειάζεστε πληροφορίες διάταξης, θα πρέπει να αλλάξετε σε `Layout`, αλλά αυτό προσθέτει επιπλέον φόρτο που πιθανότατα δεν θέλετε σε μια εργασία παρτίδας.

> **Συμβουλή:** Αν αντιμετωπίζετε πολυγλωσσικά σκαναρίσματα, μπορείτε να περάσετε μια λίστα όπως `ocr_engine.language = [aocr.Language.English, aocr.Language.Spanish]`.

---

## Βήμα 2: Αρχικοποίηση του AI Post‑Processor – **Εφαρμογή Ελέγχου Ορθογραφίας** στο Αποτέλεσμα OCR

Το Aspose AI έρχεται με ενσωματωμένο post‑processor που μπορεί να τρέξει οποιοδήποτε μοντέλο θέλετε. Εδώ κατεβάζουμε ένα ποσοτικοποιημένο μοντέλο Qwen 2.5 από το Hugging Face και το συνδέουμε με τη ρουτίνα ελέγχου ορθογραφίας.

```python
# Step 2: Configure and start the AI post‑processor
def init_ai() -> aocr.ai.AsposeAI:
    model_cfg = AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "q4_k_m"
    model_cfg.gpu_layers = 30          # Adjust based on your GPU memory
    ai_processor = AsposeAI()
    ai_processor.initialize(model_cfg)

    # Attach the built‑in spell‑check post‑processor
    ai_processor.set_post_processor(ai_processor.postprocessor_spell_check, {})
    return ai_processor
```

**Γιατί είναι σημαντικό:** Το μοντέλο είναι ποσοτικοποιημένο (`q4_k_m`), κάτι που μειώνει τη χρήση μνήμης ενώ εξακολουθεί να παρέχει αξιοπρεπή κατανόηση της γλώσσας. Καλώντας το `set_post_processor` λέμε στο Aspose AI να εκτελεί αυτόματα το βήμα **εφαρμογής ελέγχου ορθογραφίας** σε κάθε συμβολοσειρά που του δίνουμε.

> **Προσοχή:** Αν η GPU σας δεν μπορεί να διαχειριστεί 30 επίπεδα, μειώστε τον αριθμό σε 15 ή ακόμη και 5 – το script θα λειτουργήσει, απλώς πιο αργά.

---

## Βήμα 3: Εκτέλεση OCR και **Διόρθωση Σφαλμάτων OCR** σε Μία Μοναδική Εικόνα

Τώρα που η μηχανή OCR και ο AI ελεγκτής ορθογραφίας είναι έτοιμα, τα συνδυάζουμε. Αυτή η συνάρτηση φορτώνει μια εικόνα, εξάγει το ακατέργαστο κείμενο, και στη συνέχεια τρέχει τον AI post‑processor για να το καθαρίσει.

```python
# Step 3: OCR an image and run the spell‑check post‑processor
def ocr_and_correct(image_path: str,
                    ocr_engine: aocr.OcrEngine,
                    ai_processor: aocr.ai.AsposeAI) -> str:
    image = aocr.Image.load(image_path)               # Load any supported format
    raw_text = ocr_engine.recognize(image)           # Plain string from OCR
    corrected_text = ai_processor.run_postprocessor(raw_text)
    return corrected_text
```

**Γιατί είναι σημαντικό:** Η άμεση τροφοδοσία της ακατέργαστης συμβολοσειράς OCR στο μοντέλο AI μας δίνει μια **διόρθωση σφαλμάτων OCR** χωρίς να χρειάζεται να γράψουμε regex ή προσαρμοσμένα λεξικά. Το μοντέλο καταλαβαίνει το πλαίσιο, οπότε μπορεί να διορθώσει “recieve” → “receive” και ακόμη πιο λεπτές ατέλειες.

---

## Βήμα 4: **Εξαγωγή Κειμένου από Εικόνες** Μαζικά – Ο Πραγματικός Βρόχος Παρτίδας

Εδώ φαίνεται η μαγεία του **πώς να εκτελέσετε OCR σε παρτίδες**. Διατρέχουμε έναν φάκελο, παραλείπουμε μη υποστηριζόμενα αρχεία, και γράφουμε κάθε διορθωμένο αποτέλεσμα σε αρχείο `.txt`.

```python
# Step 4: Process an entire folder of images
if __name__ == "__main__":
    # Initialize once – reuse for every file
    ocr_engine = init_ocr()
    ai_processor = init_ai()

    input_dir = "YOUR_DIRECTORY/input_images"
    output_dir = "YOUR_DIRECTORY/output_text"
    os.makedirs(output_dir, exist_ok=True)

    for file_name in os.listdir(input_dir):
        # Only handle common image extensions
        if not file_name.lower().endswith(('.png', '.jpg', '.jpeg', '.tif', '.tiff')):
            continue

        image_path = os.path.join(input_dir, file_name)
        corrected = ocr_and_correct(image_path, ocr_engine, ai_processor)

        txt_path = os.path.join(output_dir,
                                os.path.splitext(file_name)[0] + ".txt")
        with open(txt_path, "w", encoding="utf-8") as txt_file:
            txt_file.write(corrected)

        print(f"Processed {file_name}")

    # Step 5: Release **free AI resources** after the batch finishes
    ai_processor.free_resources()
```

### Αναμενόμενο αποτέλεσμα

Για μια εικόνα που περιέχει τη φράση *«The quick brown fox jumps over the lazzy dog.»* θα δείτε ένα αρχείο κειμένου με:

```
The quick brown fox jumps over the lazy dog.
```

Παρατηρήστε ότι το διπλό “z” διορθώθηκε αυτόματα – αυτό είναι το AI ελέγχου ορθογραφίας σε δράση.

**Γιατί είναι σημαντικό:** Δημιουργώντας τα αντικείμενα OCR και AI **μία φορά** και επαναχρησιμοποιώντας τα, αποφεύγουμε το κόστος φόρτωσης του μοντέλου για κάθε αρχείο. Αυτή είναι η πιο αποδοτική μέθοδος για **πώς να εκτελέσετε OCR σε παρτίδες** σε κλίμακα.

---

## Βήμα 5: Καθαρισμός – **Απελευθέρωση Πόρων AI** Κατάλληλα

Όταν τελειώσετε, η κλήση `free_resources()` απελευθερώνει τη μνήμη GPU, τα context CUDA, και τυχόν προσωρινά αρχεία που δημιούργησε το μοντέλο.

```python
# Step 5: Explicitly free GPU and model memory
ai_processor.free_resources()
```

Η παράλειψη αυτού του βήματος μπορεί να αφήσει «κολλημένες» κατανομές GPU, κάτι που μπορεί να καταρρεύσει επόμενες διεργασίες Python ή να καταναλώσει VRAM. Σκεφτείτε το ως το «σβήσιμο των φώτων» στο τέλος μιας εργασίας παρτίδας.

---

## Συνηθισμένα Προβλήματα & Επιπλέον Συμβουλές

| Πρόβλημα | Τι να Αναζητήσετε | Διόρθωση |
|----------|-------------------|----------|
| **Σφάλματα έλλειψης μνήμης** | Η GPU εξαντλείται μετά από μερικές δεκάδες εικόνες | Μειώστε το `gpu_layers` ή μεταβείτε σε CPU (`model_cfg.gpu_layers = 0`). |
| **Λείπει το πακέτο γλώσσας** | Το OCR επιστρέφει κενές συμβολοσειρές | Βεβαιωθείτε ότι η έκδοση `asposeocr` περιλαμβάνει τα δεδομένα γλώσσας Αγγλικών· επανεγκαταστήστε αν χρειάζεται. |
| **Μη‑εικόνα αρχεία** | Το script καταρρέει σε ένα τυχαίο `.pdf` | Η προϋπόθεση `if not file_name.lower().endswith(...)` ήδη τα παραλείπει. |
| **Ο έλεγχος ορθογραφίας δεν εφαρμόζεται** | Το αποτέλεσμα είναι πανομοιότυπο με το ακατέργαστο OCR | Επαληθεύστε ότι κλήθηκε το `ai_processor.set_post_processor` πριν από τον βρόχο. |
| **Αργός ρυθμός παρτίδας** | Παίρνει >5 δευτερόλεπτα ανά εικόνα | Ενεργοποιήστε `model_cfg.allow_auto_download = "false"` μετά την πρώτη εκτέλεση, ώστε το μοντέλο να μην ξανακατεβάζεται κάθε φορά. |

**Συμβουλή:** Αν χρειάζεται να **εξάγετε κείμενο από εικόνες** σε γλώσσα διαφορετική από τα Αγγλικά, απλώς αλλάξτε το `ocr_engine.language` στο αντίστοιχο enum (π.χ., `aocr.Language.French`). Ο ίδιος AI post‑processor θα εφαρμόσει ακόμη και έλεγχο ορθογραφίας, αλλά ίσως θέλετε ένα μοντέλο ειδικά για τη γλώσσα για βέλτιστα αποτελέσματα.

---

## Ανακεφαλαίωση & Επόμενα Βήματα

Καλύψαμε ολόκληρη τη ροή για **πώς να εκτελέσετε OCR σε παρτίδες**:

1. **Αρχικοποίηση** μιας μηχανής OCR απλού κειμένου για τα Αγγλικά.  
2. **Διαμόρφωση** μοντέλου ελέγχου ορθογραφίας AI και σύνδεσή του ως post‑processor.  
3. **Εκτέλεση** OCR σε κάθε εικόνα και αφήστε το AI να **διορθώσει αυτόματα τα σφάλματα OCR**.  
4. **Βρόχος** σε έναν φάκελο για **μαζική εξαγωγή κειμένου από εικόνες**.  
5. **Απελευθέρωση** των πόρων AI μόλις ολοκληρωθεί η εργασία.

Από εδώ μπορείτε:

- Να διοχετεύσετε το διορθωμένο κείμενο σε μια επόμενη pipeline NLP (ανάλυση συναισθήματος, εξαγωγή οντοτήτων κ.λπ.).
- Να αντικαταστήσετε το post‑processor ελέγχου ορθογραφίας με έναν προσαρμοσμένο summarizer καλώντας `ai_processor.set_post_processor(your_custom_func, {})`.
- Να παραλληλοποιήσετε τον βρόχο φακέλου με `concurrent.futures.ThreadPoolExecutor` αν η GPU σας μπορεί να διαχειριστεί πολλαπλές ροές.

---

## Τελευταίες Σκέψεις

Η παρτίδα OCR δεν χρειάζεται να είναι κουραστική. Εκμεταλλευόμενοι το Aspose OCR μαζί με ένα ελαφρύ μοντέλο AI, αποκτάτε μια **ολοκληρωμένη λύση** που **εξάγει κείμενο από εικόνες**, **εφαρμόζει έλεγχο ορθογραφίας**, **διορθώνει σφάλματα OCR**, και **απελευθερώνει πόρους AI** με καθαρό τρόπο. Δοκιμάστε το script σε έναν δοκιμαστικό φάκελο, ρυθμίστε τον αριθμό επιπέδων GPU ώστε να ταιριάζει στο υλικό σας, και θα έχετε μια παραγωγική pipeline σε λίγα λεπτά.

Έχετε ερωτήσεις για την προσαρμογή του μοντέλου, τη διαχείριση PDF, ή την ενσωμάτωση σε web service; Αφήστε ένα σχόλιο παρακάτω ή επικοινωνήστε μαζί μου στο GitHub. Καλό κώδικα, και να είναι το OCR σας πάντα ακριβές!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}