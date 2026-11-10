---
category: general
date: 2026-06-19
description: Μάθετε πώς να εκτελείτε OCR σε εικόνα χρησιμοποιώντας το Aspose OCR και
  τον AI post‑processor σε Python. Περιλαμβάνει αυτόματα ληφθέν μοντέλο, ορθογραφικό
  έλεγχο και επιτάχυνση GPU.
draft: false
keywords:
- perform OCR on image
- Aspose OCR Python
- AI post‑processor
- auto‑downloaded model
- spellcheck post‑processor
- GPU acceleration
language: el
og_description: εκτελέστε OCR σε εικόνα χρησιμοποιώντας το Aspose OCR και τον AI post‑processor.
  Οδηγός βήμα‑προς‑βήμα με αυτόματα ληφθέν μοντέλο, ορθογραφικό έλεγχο και επιτάχυνση
  GPU.
og_title: Εκτελέστε OCR σε εικόνα – Πλήρες Μάθημα Python
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to perform OCR on image using Aspose OCR and AI post‑processor
    in Python. Includes auto‑downloaded model, spellcheck, and GPU acceleration.
  headline: perform OCR on image with Aspose AI – Full Python Guide
  type: TechArticle
- description: Learn how to perform OCR on image using Aspose OCR and AI post‑processor
    in Python. Includes auto‑downloaded model, spellcheck, and GPU acceleration.
  name: perform OCR on image with Aspose AI – Full Python Guide
  steps:
  - name: Initializes the Aspose OCR engine and loads a sample invoice image.
    text: Initializes the Aspose OCR engine and loads a sample invoice image.
  - name: Runs a basic OCR pass and prints the raw text.
    text: Runs a basic OCR pass and prints the raw text.
  - name: Configures **Aspose AI** with an **auto‑downloaded model** from Hugging Face.
    text: Configures **Aspose AI** with an **auto‑downloaded model** from Hugging Face.
  - name: Executes the **AI post‑processor** (including a **spellcheck post‑processor**)
      to clean up the OCR output.
    text: Executes the **AI post‑processor** (including a **spellcheck post‑processor**)
      to clean up the OCR output.
  - name: Releases all resources cleanly.
    text: Releases all resources cleanly.
  type: HowTo
tags:
- OCR
- Python
- Aspose
- AI
title: Εκτελέστε OCR σε εικόνα με το Aspose AI – Πλήρης Οδηγός Python
url: /el/python/general/perform-ocr-on-image-with-aspose-ai-full-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# εκτέλεση OCR σε εικόνα – Πλήρης Οδηγός Python

Έχετε αναρωτηθεί ποτέ πώς να **εκτελέσετε OCR σε εικόνα** αρχεία χωρίς να παλεύετε με δεκάδες βιβλιοθήκες; Από την εμπειρία μου, το πρόβλημα είναι συνήθως η διαχείριση μιας ακατέργαστης μηχανής OCR, και στη συνέχεια η προσπάθεια καθαρισμού του θορυβώδους αποτελέσματος. Ευτυχώς, το Aspose OCR για Python σε συνδυασμό με τον AI post‑processor του κάνει όλη τη διαδικασία εύκολη.

Σε αυτόν τον οδηγό θα περάσουμε από ένα πρακτικό, ολοκληρωμένο παράδειγμα που σας δείχνει ακριβώς πώς να **εκτελέσετε OCR σε εικόνα** δεδομένα, να αυξήσετε την ακρίβεια με ένα αυτόματα ληφθέν μοντέλο, να ενεργοποιήσετε τον ορθογραφικό έλεγχο, και ακόμη να εκμεταλλευτείτε την επιτάχυνση GPU όταν είναι διαθέσιμη. Μέχρι να τελειώσετε, θα έχετε ένα επαναχρησιμοποιήσιμο script που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο τιμολόγησης, σάρωσης αποδείξεων ή ψηφιοποίησης εγγράφων.

## Τι Θα Δημιουργήσετε

Θα δημιουργήσουμε ένα μικρό πρόγραμμα Python που:

1. Αρχικοποιεί τη μηχανή Aspose OCR και φορτώνει μια δείγμα εικόνας τιμολόγησης.  
2. Εκτελεί μια βασική διεργασία OCR και εκτυπώνει το ακατέργαστο κείμενο.  
3. Διαμορφώνει το **Aspose AI** με ένα **auto‑downloaded model** από το Hugging Face.  
4. Εκτελεί το **AI post‑processor** (συμπεριλαμβανομένου ενός **spellcheck post‑processor**) για να καθαρίσει το αποτέλεσμα OCR.  
5. Απελευθερώνει όλους τους πόρους καθαρά.

> **Συμβουλή:** Αν βρίσκεστε σε μηχάνημα με αξιοπρεπή GPU, ο ορισμός του `gpu_layers` μπορεί να μειώσει κατά δευτερόλεπτα το βήμα post‑processing.

## Προαπαιτούμενα

- Python 3.8 ή νεότερη (ο κώδικας χρησιμοποιεί type hints αλλά είναι προαιρετικά).  
- Πακέτα `aspose-ocr` και `aspose-ai` εγκατεστημένα μέσω `pip`.  
  ```bash
  pip install aspose-ocr aspose-ai
  ```  
- Μια δείγμα εικόνας (PNG, JPG ή TIFF) τοποθετημένη κάπου που μπορείτε να αναφέρετε, π.χ., `sample_invoice.png`.  
- (Προαιρετικό) Ένα GPU με υποστήριξη CUDA και οι κατάλληλοι οδηγοί αν θέλετε **GPU acceleration**.

Τώρα που η βάση είναι έτοιμη, ας βουτήξουμε στον κώδικα.

![perform OCR on image example](image.png)

## εκτέλεση OCR σε εικόνα – Βήμα 1: Αρχικοποίηση της μηχανής OCR και φόρτωση της εικόνας

Το πρώτο που χρειαζόμαστε είναι μια παρουσία της μηχανής OCR. Το Aspose OCR προσφέρει ένα καθαρό, αντικειμενοστραφές API που αφαιρεί την χαμηλού επιπέδου προεπεξεργασία εικόνας.

```python
from aspose.ocr import OcrEngine

# Initialise the OCR engine
ocr_engine = OcrEngine()
ocr_engine.Language = "en"                     # English; change as needed

# Load the image you want to analyse
ocr_engine.SetImageFromFile("YOUR_DIRECTORY/sample_invoice.png")
```

**Γιατί είναι σημαντικό:**  
Ο καθορισμός της γλώσσας νωρίς λέει στη μηχανή ποιο σύνολο χαρακτήρων να περιμένει, κάτι που μπορεί να βελτιώσει την ταχύτητα και την ακρίβεια της αναγνώρισης. Αν εργάζεστε με πολυγλωσσικά έγγραφα, απλώς αλλάξτε το `"en"` σε `"fr"` ή `"de"` όπως χρειάζεται.

## Βήμα 2: Εκτέλεση βασικού OCR και προβολή του ακατέργαστου κειμένου

Τώρα εκτελούμε πραγματικά την αναγνώριση. Το αντικείμενο αποτελέσματος περιέχει το ακατέργαστο κείμενο, τις βαθμολογίες εμπιστοσύνης, και ακόμη τα πλαίσια οριοθέτησης αν τα χρειαστείτε αργότερα.

```python
# Run OCR
ocr_result = ocr_engine.Recognize()

# Show the unprocessed output
print("Raw OCR output:")
print(ocr_result.Text)
```

Η τυπική έξοδος μπορεί να μοιάζει με αυτήν (σημειώστε τους περιστασιακούς λανθασμένους χαρακτήρες):

```
Raw OCR output:
Inv0ice N0: 12345
Date: 2023/09/15
Total Am0unt: $1,2O0.00
```

Μπορείτε να δείτε τα μηδενικά (`0`) όπου η μηχανή νόμιζε ότι είδε ένα “O”. Εκεί είναι που το **AI post‑processor** ξεχωρίζει.

## Διαμόρφωση Aspose AI – auto‑downloaded model και ορθογραφικός έλεγχος

Πριν περάσουμε το ακατέργαστο αποτέλεσμα OCR στο επίπεδο AI, πρέπει να πούμε στο Aspose AI ποιο μοντέλο να χρησιμοποιήσει. Η βιβλιοθήκη μπορεί να κατεβάσει αυτόματα ένα μοντέλο από το Hugging Face, ώστε να μην χρειάζεται να διαχειρίζεστε μεγάλα αρχεία `.bin`.

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

# Create a model configuration that auto‑downloads the Qwen2.5‑3B‑Instruct model
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"   # reduces RAM usage
model_config.gpu_layers = 20                      # use GPU if available

# Initialise the AI engine with the config
ai_engine = AsposeAI(model_config)

# Enable the built‑in spellcheck post‑processor
ai_engine.set_post_processor("spellcheck", None)
```

**Επεξήγηση των ρυθμίσεων**

| Ρύθμιση | Τι κάνει | Πότε να προσαρμόσετε |
|---------|----------|----------------------|
| `allow_auto_download` | Επιτρέπει στο Aspose να κατεβάσει το μοντέλο αυτόματα στην πρώτη εκτέλεση. | Διατηρήστε `true` εκτός αν έχετε προ‑κατεβάσει για χρήση εκτός σύνδεσης. |
| `hugging_face_repo_id` | Αναγνωριστικό του μοντέλου στο Hugging Face. | Αλλάξτε για διαφορετικό μοντέλο αν χρειάζεστε ένα ειδικό για το πεδίο. |
| `hugging_face_quantization` | Επιλέγει το επίπεδο κβαντισμού (`int8`, `float16`, κ.λπ.). | Χρησιμοποιήστε `int8` για περιβάλλοντα με χαμηλή μνήμη· `float16` για μεγαλύτερη ακρίβεια. |
| `gpu_layers` | Αριθμός επιπέδων transformer που εκτελούνται στο GPU. | Ορίστε σε `0` για μόνο CPU, ή μια τιμή έως τα συνολικά επίπεδα του μοντέλου (20 για Qwen2.5‑3B). |

## Εκτέλεση του AI post‑processor στο αποτέλεσμα OCR

Με τη μηχανή έτοιμη, απλώς τροφοδοτούμε το ακατέργαστο αποτέλεσμα OCR στην AI pipeline. Ο ενσωματωμένος **spellcheck post‑processor** θα διορθώσει προφανή τυπογραφικά λάθη, ενώ το μοντέλο γλώσσας μπορεί να επαναδιατυπώσει ή να συμπληρώσει ελλιπείς πληροφορίες αν ενεργοποιήσετε πρόσθετους επεξεργαστές αργότερα.

```python
# Enhance the OCR result using the AI post‑processor
enhanced_result = ai_engine.run_postprocessor(ocr_result)

# Display the cleaned‑up text
print("\nAI‑enhanced OCR output:")
print(enhanced_result.Text)
```

Αναμενόμενη έξοδος μετά το βήμα ορθογραφικού ελέγχου:

```
AI‑enhanced OCR output:
Invoice No: 12345
Date: 2023/09/15
Total Amount: $1,200.00
```

Παρατηρήστε πώς τα μηδενικά έχουν διορθωθεί σε σωστά γράμματα, και η λανθασμένη λέξη “Am0unt” μετατράπηκε σε “Amount”. Το **AI post‑processor** λειτουργεί στέλνοντας το ακατέργαστο κείμενο μέσω του επιλεγμένου μοντέλου, το οποίο επιστρέφει μια βελτιωμένη έκδοση βάσει της εκπαίδευσής του.

### Περιπτώσεις Άκρων & Συμβουλές

- **Low‑resolution images**: Αν η μηχανή OCR δυσκολεύεται, σκεφτείτε να αυξήσετε την ανάλυση της εικόνας πρώτα (`Pillow` μπορεί να βοηθήσει) ή να αυξήσετε το `ocr_engine.ImagePreprocessingOptions`.  
- **Non‑Latin scripts**: Αλλάξτε το `ocr_engine.Language` στον κατάλληλο κωδικό ISO (`"zh"` για Κινέζικα, `"ar"` για Αραβικά).  
- **GPU not detected**: Η ρύθμιση `gpu_layers` επιστρέφει σιωπηλά σε CPU αν δεν βρεθεί συμβατό GPU, οπότε δεν χρειάζεται επιπλέον διαχείριση σφαλμάτων.  
- **Model size limits**: Το μοντέλο Qwen2.5‑3B είναι ~4 GB συμπιεσμένο· βεβαιωθείτε ότι ο δίσκος σας έχει αρκετό χώρο για το αυτόματο κατέβασμα.

## Απελευθέρωση πόρων – καθαρό κλείσιμο

Τα αντικείμενα Aspose κρατούν εγγενείς δείκτες, επομένως είναι καλή πρακτική να τα ελευθερώνετε όταν τελειώσετε. Αυτό αποτρέπει διαρροές μνήμης, ειδικά σε υπηρεσίες που τρέχουν για μεγάλο χρονικό διάστημα.

```python
# Free AI resources
ai_engine.free_resources()

# Dispose of the OCR engine
ocr_engine.Dispose()
```

Μπορείτε να τυλίξετε ολόκληρο το script σε ένα μπλοκ `try…finally` αν προτιμάτε ρητή εκκαθάριση.

## Πλήρες Script – έτοιμο για αντιγραφή‑επικόλληση

Παρακάτω βρίσκεται ολόκληρο το πρόγραμμα, έτοιμο να εκτελεστεί αφού αντικαταστήσετε το `YOUR_DIRECTORY` με τη διαδρομή προς την εικόνα σας.

```python
# -*- coding: utf-8 -*-
"""
Full example: perform OCR on image using Aspose OCR + AI post‑processor.
Author: Your Name
Date: 2026‑06‑19
"""

from aspose.ocr import OcrEngine
from aspose.ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = OcrEngine()
    ocr_engine.Language = "en"
    ocr_engine.SetImageFromFile("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Basic OCR
    ocr_result = ocr_engine.Recognize()
    print("Raw OCR output:")
    print(ocr_result.Text)

    # 3️⃣ Configure Aspose AI with auto‑downloaded model
    model_cfg = AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "int8"
    model_cfg.gpu_layers = 20   # GPU acceleration if available

    ai_engine = AsposeAI(model_cfg)
    ai_engine.set_post_processor("spellcheck", None)   # enable spellcheck

    # 4️⃣ AI post‑processing
    enhanced = ai_engine.run_postprocessor(ocr_result)
    print("\nAI‑enhanced OCR output:")
    print(enhanced.Text)

    # 5️⃣ Clean up
    ai_engine.free_resources()
    ocr_engine.Dispose()

if __name__ == "__main__":
    main()
```

Τρέξτε το με:

```bash
python perform_ocr_on_image.py
```

Θα πρέπει να δείτε τα ακατέργαστα και τα καθαρισμένα αποτελέσματα να εκτυπώνονται στην κονσόλα.

## Συμπέρασμα


## Τι Θα Μάθετε Στη Σειρά;

- [Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Βήμα‑βήμα](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Μετατροπή Εικόνας σε Κείμενο – Εκτέλεση OCR σε Εικόνα από URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}