---
category: general
date: 2026-04-29
description: Μάθετε πώς να εκτελείτε OCR στις σαρώσεις σας, να χρησιμοποιείτε αυτόματα
  το μοντέλο Hugging Face και να αναγνωρίζετε κείμενο από σαρώσεις με το Aspose OCR
  σε λίγα λεπτά.
draft: false
keywords:
- how to run OCR
- use hugging face model
- recognize text from scans
- download model automatically
language: el
og_description: Πώς να εκτελέσετε OCR σε σαρώσεις χρησιμοποιώντας το Aspose OCR, να
  κατεβάσετε αυτόματα ένα μοντέλο Hugging Face και να λάβετε καθαρό, με στίξη κείμενο.
og_title: Πώς να εκτελέσετε OCR με το Aspose & το Hugging Face – Πλήρης Οδηγός
tags:
- OCR
- Aspose
- Hugging Face
- Python
title: Πώς να εκτελέσετε OCR με το Aspose & το Hugging Face – Πλήρης Οδηγός
url: /el/python/general/how-to-run-ocr-with-aspose-hugging-face-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εκτελέσετε OCR με Aspose & Hugging Face – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να εκτελέσετε OCR** σε μια στοίβα σαρωμένων εγγράφων χωρίς να ξοδεύετε ώρες ρυθμίζοντας παραμέτρους; Δεν είστε μόνοι. Σε πολλά έργα, οι προγραμματιστές χρειάζονται **να αναγνωρίσουν κείμενο από σαρώσεις** γρήγορα, αλλά συναντούν δυσκολίες με τη λήψη μοντέλων και την επεξεργασία των αποτελεσμάτων.  

Καλή είδηση: αυτό το tutorial σας δείχνει μια έτοιμη λύση που **χρησιμοποιεί ένα μοντέλο Hugging Face**, το κατεβάζει αυτόματα και προσθέτει στίξη ώστε η έξοδος να διαβάζεται σαν να την έγραψε άνθρωπος. Στο τέλος, θα έχετε ένα script που επεξεργάζεται κάθε εικόνα σε έναν φάκελο και δημιουργεί ένα καθαρό αρχείο `.txt` δίπλα σε κάθε σάρωση.

## Τι Θα Χρειαστείτε

- Python 3.8+ (ο κώδικας χρησιμοποιεί f‑strings, οπότε παλαιότερες εκδόσεις δεν θα λειτουργήσουν)
- Πακέτο `aspose-ocr` (εγκατάσταση μέσω `pip install aspose-ocr`)
- Πρόσβαση στο Internet για τη λήψη του μοντέλου την πρώτη φορά  
- Ένας φάκελος με εικόνες σαρώσεων (`.png`, `.jpg`, ή `.tif`)

Αυτό είναι όλο—χωρίς επιπλέον δυαδικά αρχεία, χωρίς χειροκίνητη ρύθμιση μοντέλου. Ας βουτήξουμε.

![παράδειγμα εκτέλεσης OCR](https://example.com/ocr-demo.png "παράδειγμα εκτέλεσης OCR")

## Βήμα 1: Εισαγωγή Κλάσεων Aspose OCR & Ρύθμιση Περιβάλλοντος

Ξεκινάμε φορτώνοντας τις απαραίτητες κλάσεις από τη βιβλιοθήκη Aspose OCR. Η εισαγωγή όλων των απαραίτητων στοιχείων στην αρχή κρατά το script τακτοποιημένο και διευκολύνει την ανίχνευση ελλιπών εξαρτήσεων.

```python
# Step 1: Import Aspose OCR classes
import os
from aspose.ocr import OcrEngine, AsposeAI, AsposeAIModelConfig
```

*Γιατί είναι σημαντικό*: Η `OcrEngine` κάνει το βαριά δουλειά, ενώ η `AsposeAI` μας επιτρέπει να συνδέσουμε ένα μεγάλο μοντέλο γλώσσας για πιο έξυπνη μετα‑επεξεργασία. Αν παραλείψετε την εισαγωγή, ο υπόλοιπος κώδικας δεν θα συνταχθεί—οπότε μην το ξεχάσετε.

## Βήμα 2: Διαμόρφωση Μοντέλου Hugging Face με Υποστήριξη GPU  

Τώρα λέμε στην Aspose πού να κατεβάσει το μοντέλο και πόσα επίπεδα πρέπει να τρέξουν στο GPU. Η σημαία `allow_auto_download="true"` κάνει αυτόματα τη **λήψη του μοντέλου** για εσάς.

```python
# Step 2: Configure a GPU‑aware AI model (replace with your own model folder)
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=40,                     # use GPU for faster inference
    directory_model_path=r"YOUR_DIRECTORY/models"
)
```

> **Συμβουλή**: Αν δεν έχετε GPU, ορίστε `gpu_layers=0`. Το μοντέλο θα πέσει στην CPU, που είναι πιο αργό αλλά λειτουργεί.

### Γιατί να Επιλέξετε ένα Μοντέλο Hugging Face;

Το Hugging Face φιλοξενεί μια τεράστια συλλογή έτοιμων LLM. Δείχνοντας στο `Qwen/Qwen2.5-3B-Instruct-GGUF`, παίρνετε ένα συμπαγές, προσαρμοσμένο σε εντολές μοντέλο που μπορεί να προσθέσει στίξη, να διορθώσει κενά και ακόμη να διορθώσει μικρά σφάλματα OCR. Αυτό είναι το νόημα της **χρήσης μοντέλου hugging face** στην πράξη.

## Βήμα 3: Αρχικοποίηση του AI Engine και Ενεργοποίηση Μετά‑Επεξεργασίας Στίξης  

Η μηχανή AI δεν είναι μόνο για κομψές συνομιλίες—εδώ προσθέτουμε έναν *προσθέτη στίξης* που καθαρίζει το ακατέργαστο OCR αποτέλεσμα.

```python
# Step 3: Initialise the AI engine and enable punctuation post‑processing
ai_engine = AsposeAI()
ai_engine.set_post_processor("punctuation_adder", {})
```

*Τι συμβαίνει;* Η κλήση `set_post_processor` καταχωρεί έναν ενσωματωμένο μετα‑επεξεργαστή που εκτελείται μετά το τέλος της μηχανής OCR. Παίρνει το ακατέργαστο κείμενο και εισάγει κόμματα, τελείες και κεφαλαία γράμματα όπου χρειάζεται, κάνοντας το τελικό κείμενο πολύ πιο αναγνώσιμο.

## Βήμα 4: Δημιουργία του OCR Engine και Σύνδεση με το AI Engine  

Η σύνδεση του AI engine με το OCR engine μας δίνει ένα ενιαίο αντικείμενο που μπορεί τόσο να διαβάζει χαρακτήρες όσο και να τελειοποιεί το αποτέλεσμα.

```python
# Step 4: Create the OCR engine and attach the AI engine
ocr_engine = OcrEngine()
ocr_engine.set_ai_engine(ai_engine)
```

Αν παραλείψετε αυτό το βήμα, το OCR θα λειτουργήσει ακόμα, αλλά θα χάσετε το πλεονέκτημα της στίξης—οπότε η έξοδος θα μοιάζει με αλυσίδα λέξεων.

## Βήμα 5: Επεξεργασία Κάθε Εικόνας σε Φάκελο  

Αυτή είναι η καρδιά του tutorial. Διατρέχουμε κάθε εικόνα, τρέχουμε OCR, εφαρμόζουμε τον μετα‑επεξεργαστή και γράφουμε το καθαρισμένο κείμενο σε ένα παράπλευρο αρχείο `.txt`.

```python
# Step 5: Run OCR on each image in a folder, post‑process the result, and save the text
scans_folder = r"YOUR_DIRECTORY/scans"
for image_file in os.listdir(scans_folder):
    # Filter only supported image types
    if not image_file.lower().endswith(('.png', '.jpg', '.tif')):
        continue

    image_path = os.path.join(scans_folder, image_file)

    # Recognise text from the image
    ocr_result = ocr_engine.recognize(image_path)

    # Apply the punctuation post‑processor
    ocr_result = ocr_engine.run_postprocessor(ocr_result)

    # Show a brief confidence summary
    print(f"{image_file} – confidence {ocr_result.confidence:.2%}")

    # Save the cleaned text next to the source image
    txt_path = image_path + ".txt"
    with open(txt_path, "w", encoding="utf-8") as txt_file:
        txt_file.write(ocr_result.text)
```

### Τι να Περιμένετε

Η εκτέλεση του script εκτυπώνει κάτι σαν:

```
invoice_001.png – confidence 96.73%
receipt_2024.tif – confidence 94.12%
```

Κάθε γραμμή σας δείχνει το σκορ εμπιστοσύνης (γρήγορος έλεγχος υγείας) και δημιουργεί τα αρχεία `invoice_001.png.txt`, `receipt_2024.tif.txt`, κ.λπ., που περιέχουν στίξη και ανθρώπινα αναγνώσιμο κείμενο.

### Ακραίες Περιπτώσεις & Παραλλαγές

- **Σαρώσεις μη‑Αγγλικών**: Αλλάξτε το `hugging_face_repo_id` σε ένα πολυγλωσσικό μοντέλο (π.χ., `microsoft/Multilingual-LLM-GGUF`).
- **Μεγάλες παρτίδες**: Τυλίξτε το βρόχο σε ένα `concurrent.futures.ThreadPoolExecutor` για παράλληλη επεξεργασία, αλλά προσέξτε τα όρια μνήμης GPU.
- **Προσαρμοσμένη μετά‑επεξεργασία**: Αντικαταστήστε το `"punctuation_adder"` με το δικό σας script αν χρειάζεστε εξειδικευμένο καθαρισμό (π.χ., αφαίρεση αριθμών τιμολογίων).

## Βήμα 6: Καθαρισμός Πόρων  

Όταν η εργασία ολοκληρωθεί, η απελευθέρωση πόρων αποτρέπει διαρροές μνήμης, κάτι ιδιαίτερα σημαντικό αν τρέχετε αυτό μέσα σε μια μακροχρόνια υπηρεσία.

```python
# Step 6: Release resources
ai_engine.free_resources()
ocr_engine.dispose()
```

Η παράλειψη αυτού του βήματος μπορεί να αφήσει μνήμη GPU κλειδωμένη, κάτι που θα εμποδίσει επόμενες εκτελέσεις.

## Ανακεφαλαίωση: Πώς να Εκτελέσετε OCR Από‑Αρχή‑Τέλος  

Σε λίγες μόνο γραμμές, δείξαμε **πώς να εκτελέσετε OCR** σε έναν φάκελο σαρώσεων, **να χρησιμοποιήσετε ένα μοντέλο Hugging Face** που κατεβαίνει αυτόματα την πρώτη φορά, και **να αναγνωρίσετε κείμενο από σαρώσεις** με αυτόματη προσθήκη στίξης. Το πλήρες script είναι έτοιμο για αντιγραφή‑επικόλληση, προσαρμογή των διαδρομών σας και εκτέλεση.

## Επόμενα Βήματα & Σχετικά Θέματα  

- **Μαζική μετά‑επεξεργασία**: Εξερευνήστε το `ocr_engine.run_batch_postprocessor` για ακόμη πιο γρήγορη μαζική διαχείριση.  
- **Εναλλακτικά μοντέλα**: Δοκιμάστε την οικογένεια `openai/whisper` αν χρειάζεστε μετατροπή ομιλίας‑σε‑κείμενο μαζί με OCR.  
- **Ενσωμάτωση με βάσεις δεδομένων**: Αποθηκεύστε το εξαγόμενο κείμενο σε SQLite ή Elasticsearch για αρχεία με δυνατότητα αναζήτησης.  

Νιώστε ελεύθεροι να πειραματιστείτε—αλλάξτε το μοντέλο, ρυθμίστε το `gpu_layers`, ή προσθέστε τον δικό σας μετα‑επεξεργαστή. Η ευελιξία του Aspose OCR σε συνδυασμό με το μοντέλο hub του Hugging Face κάνει αυτή τη λύση μια πολύπλευρη βάση για οποιοδήποτε έργο ψηφιοποίησης εγγράφων.

---

*Καλή προγραμματιστική! Αν συναντήσετε κάποιο πρόβλημα, αφήστε ένα σχόλιο παρακάτω ή ελέγξτε τα έγγραφα Aspose OCR για πιο προχωρημένες επιλογές διαμόρφωσης.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}