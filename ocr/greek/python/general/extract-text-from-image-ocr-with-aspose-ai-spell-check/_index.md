---
category: general
date: 2026-05-03
description: Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας το Aspose OCR και AI ορθογραφικό
  έλεγχο. Μάθετε πώς να κάνετε OCR σε εικόνα, να φορτώνετε εικόνα για OCR, να αναγνωρίζετε
  κείμενο από τιμολόγιο και να απελευθερώνετε τους πόρους GPU.
draft: false
keywords:
- extract text from image
- how to ocr image
- load image for ocr
- release gpu resources
- recognize text from invoice
language: el
og_description: Εξαγωγή κειμένου από εικόνα με Aspose OCR και AI ορθογραφικό έλεγχο.
  Οδηγός βήμα‑προς‑βήμα που καλύπτει πώς να κάνετε OCR σε εικόνα, να φορτώσετε την
  εικόνα για OCR και να απελευθερώσετε τους πόρους GPU.
og_title: Εξαγωγή κειμένου από εικόνα – Πλήρης οδηγός OCR & ελέγχου ορθογραφίας
tags:
- OCR
- Aspose
- AI
- Python
title: Εξαγωγή κειμένου από εικόνα – OCR με το Aspose AI Spell‑Check
url: /el/python/general/extract-text-from-image-ocr-with-aspose-ai-spell-check/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# εξαγωγή κειμένου από εικόνα – Οδηγός πλήρους OCR & Spell‑Check

Κάποτε χρειάστηκε να **εξάγετε κείμενο από εικόνα** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη θα σας προσφέρει ταχύτητα και ακρίβεια; Δεν είστε οι μόνοι. Σε πολλά πραγματικά έργα—όπως επεξεργασία τιμολογίων, ψηφιοποίηση αποδείξεων ή σάρωση συμβάσεων—η λήψη καθαρού, αναζητήσιμου κειμένου από μια φωτογραφία είναι το πρώτο εμπόδιο.

Το καλό νέο είναι ότι το Aspose OCR σε συνδυασμό με ένα ελαφρύ μοντέλο Aspose AI μπορεί να το κάνει αυτό με λίγες γραμμές Python. Σε αυτό το tutorial θα δούμε **πώς να κάνετε OCR σε εικόνα**, πώς να φορτώσετε σωστά την εικόνα, πώς να τρέξετε έναν ενσωματωμένο ελεγκτή ορθογραφίας και, τέλος, **πώς να απελευθερώσετε τους πόρους GPU** ώστε η εφαρμογή σας να παραμένει φιλική στη μνήμη.

Στο τέλος αυτού του οδηγού θα μπορείτε να **αναγνωρίσετε κείμενο από εικόνες τιμολογίων**, να διορθώνετε αυτόματα κοινά λάθη OCR και να διατηρείτε το GPU σας καθαρό για την επόμενη παρτίδα.

---

## Τι Θα Χρειαστείτε

- Python 3.9 ή νεότερο (ο κώδικας χρησιμοποιεί type hints αλλά λειτουργεί και σε παλαιότερες εκδόσεις 3.x)
- Πακέτα `aspose-ocr` και `aspose-ai` (εγκατάσταση μέσω `pip install aspose-ocr aspose-ai`)
- Ένα GPU με υποστήριξη CUDA είναι προαιρετικό· το script θα επανέλθει σε CPU αν δεν βρεθεί GPU.
- Μια εικόνα παραδείγματος, π.χ. `sample_invoice.png`, τοποθετημένη σε φάκελο που μπορείτε να αναφέρετε.

Χωρίς βαριές ML βιβλιοθήκες, χωρίς τεράστιες λήψεις μοντέλων—μόνο ένα μικρό μοντέλο Q4‑K‑M quantised που χωράει άνετα στα περισσότερα GPU.

---

## Βήμα 1: Αρχικοποίηση του OCR Engine – εξαγωγή κειμένου από εικόνα

Το πρώτο που κάνετε είναι να δημιουργήσετε μια παρουσία `OcrEngine` και να ορίσετε τη γλώσσα που αναμένετε. Εδώ επιλέγουμε τα Αγγλικά και ζητάμε έξοδο plain‑text, η οποία είναι ιδανική για επεξεργασία.

```python
import aocr  # Aspose OCR package
import aspose.ai as ai  # Aspose AI package

# Initialise the OCR engine
ocr_engine = aocr.OcrEngine()
ocr_engine.language = aocr.Language.English            # Choose any supported language
ocr_engine.recognize_mode = aocr.RecognitionMode.Plain  # Plain text makes post‑processing easier
```

**Γιατί είναι σημαντικό:** Η ρύθμιση της γλώσσας περιορίζει το σύνολο χαρακτήρων, βελτιώνοντας την ακρίβεια. Η λειτουργία plain‑text αφαιρεί πληροφορίες διάταξης που συνήθως δεν χρειάζεστε όταν θέλετε απλώς να εξάγετε κείμενο από εικόνα.

---

## Βήμα 2: Φόρτωση εικόνας για OCR – πώς να κάνετε OCR σε εικόνα

Τώρα τροφοδοτούμε τον κινητήρα με μια πραγματική εικόνα. Η βοηθητική μέθοδος `Image.load` καταλαβαίνει κοινές μορφές (PNG, JPEG, TIFF) και αφαιρεί τις ιδιαιτερότητες του file‑IO.

```python
# Load the input image – this is the "load image for OCR" step
input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
raw_text = ocr_engine.recognize(input_image)  # Returns the recognised text as a string
```

**Συμβουλή:** Αν οι εικόνες προέλευσης είναι μεγάλες, σκεφτείτε να τις αλλάξετε σε μικρότερο μέγεθος πριν τις στείλετε στον κινητήρα· μικρότερες διαστάσεις μπορούν να μειώσουν τη χρήση μνήμης GPU χωρίς να επηρεάσουν την ποιότητα αναγνώρισης.

---

## Βήμα 3: Διαμόρφωση του Aspose AI Model – αναγνώριση κειμένου από τιμολόγιο

Το Aspose AI έρχεται με ένα μικρό μοντέλο GGUF που μπορείτε να κατεβάσετε αυτόματα. Το παράδειγμα χρησιμοποιεί το αποθετήριο `Qwen2.5‑3B‑Instruct‑GGUF`, quantised σε `q4_k_m`. Επίσης, ορίζουμε στο runtime να εκχωρήσει 20 στρώματα στο GPU, κάτι που εξισορροπεί την ταχύτητα και τη χρήση VRAM.

```python
# Model configuration – auto‑download a small Q4‑K‑M quantised model
model_config = ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "q4_k_m"
model_config.gpu_layers = 20  # Use 20 GPU layers when a GPU is available
```

**Πίσω από τη σκηνή:** Το quantised μοντέλο είναι περίπου 1,5 GB στο δίσκο, ένα κλάσμα ενός μοντέλου πλήρους ακρίβειας, αλλά εξακολουθεί να καταγράφει αρκετή γλωσσική λεπτότητα για να εντοπίζει τυπικά ορθογραφικά λάθη OCR.

---

## Βήμα 4: Αρχικοποίηση AsposeAI και προσθήκη του post‑processor ελέγχου ορθογραφίας

Το Aspose AI περιλαμβάνει έναν έτοιμο post‑processor ελέγχου ορθογραφίας. Με την προσθήκη του, κάθε αποτέλεσμα OCR θα καθαρίζεται αυτόματα.

```python
# Initialise AsposeAI and attach the built‑in spell‑check post‑processor
ocr_ai = ai.AsposeAI(model_config)  # Pass the config we just built
ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})  # Empty dict → default settings
```

**Γιατί να χρησιμοποιήσετε τον post‑processor;** Οι μηχανές OCR συχνά διαβάζουν “Invoice” ως “Invo1ce” ή “Total” ως “T0tal”. Ο έλεγχος ορθογραφίας τρέχει ένα ελαφρύ μοντέλο γλώσσας πάνω στο ακατέργαστο κείμενο και διορθώνει αυτά τα σφάλματα χωρίς να χρειάζεται να γράψετε προσαρμοσμένο λεξικό.

---

## Βήμα 5: Εκτέλεση του post‑processor ελέγχου ορθογραφίας στο αποτέλεσμα OCR

Με όλα συνδεδεμένα, μια κλήση δίνει το διορθωμένο κείμενο. Εκτυπώνουμε επίσης τόσο την αρχική όσο και την καθαρισμένη έκδοση ώστε να δείτε τη βελτίωση.

```python
# Run the spell‑check post‑processor on the OCR result
corrected_text = ocr_ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Corrected:", corrected_text)
```

Τυπική έξοδος για ένα τιμολόγιο μπορεί να είναι η εξής:

```
Original : Invo1ce #12345
Date: 2023/07/15
Total: $1,250.00
...
Corrected: Invoice #12345
Date: 2023/07/15
Total: $1,250.00
...
```

Παρατηρήστε πώς το “Invo1ce” μετατράπηκε στη σωστή λέξη “Invoice”. Αυτή είναι η δύναμη του ενσωματωμένου AI ελέγχου ορθογραφίας.

---

## Βήμα 6: Απελευθέρωση πόρων GPU – ασφαλής απελευθέρωση πόρων GPU

Αν τρέχετε αυτόν τον κώδικα σε μια υπηρεσία μακράς διάρκειας (π.χ. ένα web API που επεξεργάζεται δεκάδες τιμολόγια ανά λεπτό), πρέπει να ελευθερώνετε το context του GPU μετά από κάθε παρτίδα. Διαφορετικά θα αντιμετωπίσετε διαρροές μνήμης και τελικά σφάλματα “CUDA out of memory”.

```python
# Release GPU resources – crucial to avoid memory leaks
ocr_ai.free_resources()
```

**Pro tip:** Καλέστε `free_resources()` μέσα σε ένα `finally` block ή σε έναν context manager ώστε να εκτελείται πάντα, ακόμη και αν προκύψει εξαίρεση.

---

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα τα κομμάτια παίρνετε ένα αυτόνομο script που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο.

```python
# extract_text_from_image.py
import aocr
import aspose.ai as ai

def main():
    # Step 1: Initialise OCR engine
    ocr_engine = aocr.OcrEngine()
    ocr_engine.language = aocr.Language.English
    ocr_engine.recognize_mode = aocr.RecognitionMode.Plain

    # Step 2: Load image for OCR
    input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
    raw_text = ocr_engine.recognize(input_image)

    # Step 3: Configure Aspose AI model
    model_cfg = ai.AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "q4_k_m"
    model_cfg.gpu_layers = 20

    # Step 4: Initialise AI and attach spell‑check
    ocr_ai = ai.AsposeAI(model_cfg)
    ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})

    # Step 5: Run spell‑check
    corrected_text = ocr_ai.run_postprocessor(raw_text)

    print("Original :", raw_text)
    print("Corrected:", corrected_text)

    # Step 6: Release GPU resources
    ocr_ai.free_resources()

if __name__ == "__main__":
    main()
```

Αποθηκεύστε το αρχείο, προσαρμόστε τη διαδρομή στην εικόνα σας και τρέξτε `python extract_text_from_image.py`. Θα πρέπει να δείτε το καθαρισμένο κείμενο του τιμολογίου να εμφανίζεται στην κονσόλα.

---

## Συχνές Ερωτήσεις (FAQ)

**Ε: Λειτουργεί αυτό σε μηχανήματα μόνο με CPU;**  
Α: Απόλυτα. Αν δεν εντοπιστεί GPU, το Aspose AI επιστρέφει στην εκτέλεση σε CPU, αν και θα είναι πιο αργό. Μπορείτε να εξαναγκάσετε τη χρήση CPU ορίζοντας `model_cfg.gpu_layers = 0`.

**Ε: Τι γίνεται αν τα τιμολόγια μου είναι σε άλλη γλώσσα εκτός των Αγγλικών;**  
Α: Αλλάξτε το `ocr_engine.language` στην αντίστοιχη τιμή enum (π.χ., `aocr.Language.Spanish`). Το μοντέλο ελέγχου ορθογραφίας είναι πολυγλωσσικό, αλλά μπορεί να έχετε καλύτερα αποτελέσματα με μοντέλο ειδικά για τη γλώσσα.

**Ε: Μπορώ να επεξεργαστώ πολλαπλές εικόνες σε βρόχο;**  
Α: Ναι. Απλώς μετακινήστε τα βήματα φόρτωσης, αναγνώρισης και post‑processing μέσα σε έναν `for` βρόχο. Θυμηθείτε να καλέσετε `ocr_ai.free_resources()` μετά τον βρόχο ή μετά από κάθε παρτίδα αν επαναχρησιμοποιείτε την ίδια παρουσία AI.

**Ε: Πόσο μεγάλο είναι το κατέβασμα του μοντέλου;**  
Α: Περίπου 1,5 GB για την έκδοση `q4_k_m`. Αποθηκεύεται στην cache μετά την πρώτη εκτέλεση, οπότε οι επόμενες εκτελέσεις είναι άμεσες.

---

## Συμπέρασμα

Σε αυτό το tutorial δείξαμε πώς να **εξάγετε κείμενο από εικόνα** χρησιμοποιώντας το Aspose OCR, να διαμορφώσουμε ένα μικρό μοντέλο AI, να εφαρμόσουμε έναν post‑processor ελέγχου ορθογραφίας και να **απελευθερώσουμε με ασφάλεια τους πόρους GPU**. Η ροή εργασίας καλύπτει όλα, από τη φόρτωση της εικόνας μέχρι τον καθαρισμό μετά την ολοκλήρωση, παρέχοντάς σας μια αξιόπιστη pipeline για σενάρια **αναγνώρισης κειμένου από τιμολόγιο**.

Τι θα κάνετε στη συνέχεια; Δοκιμάστε να αντικαταστήσετε τον έλεγχο ορθογραφίας με ένα προσαρμοσμένο μοντέλο εξαγωγής οντοτήτων.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}