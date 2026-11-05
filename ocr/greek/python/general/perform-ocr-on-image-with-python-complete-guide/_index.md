---
category: general
date: 2026-04-29
description: Εκτελέστε OCR σε εικόνα χρησιμοποιώντας Python, αυτόματη λήψη μοντέλου
  HuggingFace και αποδέσμευση μνήμης GPU αποδοτικά ενώ καθαρίζετε το κείμενο OCR.
draft: false
keywords:
- perform OCR on image
- download HuggingFace model python
- release GPU memory python
- clean OCR text python
language: el
og_description: Μάθετε πώς να εκτελείτε OCR σε εικόνα με Python, να κατεβάζετε αυτόματα
  ένα μοντέλο HuggingFace, να καθαρίζετε το κείμενο και να ελευθερώνετε τη μνήμη GPU.
og_title: Εκτελέστε OCR σε εικόνα με Python – Οδηγός βήμα‑προς‑βήμα
tags:
- OCR
- Python
- Aspose
- HuggingFace
title: Εκτελέστε OCR σε εικόνα με Python – Πλήρης Οδηγός
url: /el/python/general/perform-ocr-on-image-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε εικόνα με Python – Πλήρης Οδηγός

Κάποτε χρειάστηκε να **εκτελέσετε OCR σε εικόνα** αρχεία αλλά κολλήσατε στο στάδιο λήψης μοντέλου ή εκκαθάρισης μνήμης GPU; Δεν είστε οι μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το εμπόδιο όταν προσπαθούν για πρώτη φορά να συνδυάσουν την οπτική αναγνώριση χαρακτήρων με μεγάλα μοντέλα γλώσσας.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από μια ολοκληρωμένη λύση που **κατεβάζει ένα μοντέλο HuggingFace σε Python**, εκτελεί Aspose OCR, καθαρίζει την ακατέργαστη έξοδο, και τελικά **απελευθερώνει τη μνήμη GPU** που η Python μπορεί να ανακτήσει. Στο τέλος θα έχετε ένα έτοιμο προς εκτέλεση script που μετατρέπει ένα σαρωμένο PNG σε επεξεργασμένο, αναζητήσιμο κείμενο.

> **Τι θα λάβετε:** ένα πλήρες, εκτελέσιμο δείγμα κώδικα, εξηγήσεις για το γιατί κάθε βήμα είναι σημαντικό, συμβουλές για την αποφυγή κοινών παγίδων, και μια ματιά στο πώς να προσαρμόσετε τη ροή εργασίας για τα δικά σας έργα.

---

## Τι Θα Χρειαστείτε

- Python 3.9 ή νεότερη (το παράδειγμα δοκιμάστηκε σε 3.11)  
- Πακέτο `aspose-ocr` (εγκατάσταση μέσω `pip install aspose-ocr`)  
- Σύνδεση στο διαδίκτυο για το βήμα **download HuggingFace model python**  
- GPU συμβατό με CUDA αν θέλετε την επιτάχυνση (προαιρετικό αλλά συνιστάται)  

Δεν απαιτούνται επιπλέον εξαρτήσεις σε επίπεδο συστήματος· η μηχανή OCR της Aspose περιλαμβάνει όλα όσα χρειάζεστε.

---

![παράδειγμα εκτέλεσης OCR σε εικόνα](image.png "Παράδειγμα εκτέλεσης OCR σε εικόνα με Aspose OCR και έναν επεξεργαστή LLM")

*Image alt text: “εκτέλεση OCR σε εικόνα – Έξοδος Aspose OCR πριν και μετά τον καθαρισμό AI”*

---

## Εκτέλεση OCR σε Εικόνα – Επισκόπηση Βήμα‑προς‑Βήμα

Παρακάτω χωρίζουμε τη ροή εργασίας σε λογικά τμήματα. Κάθε τμήμα έχει τη δική του επικεφαλίδα, ώστε οι βοηθοί AI να μπορούν γρήγορα να μεταβούν στο τμήμα που σας ενδιαφέρει, και οι μηχανές αναζήτησης να ευρετηριάσουν τις σχετικές λέξεις‑κλειδιά.

### 1. Download HuggingFace Model in Python

Το πρώτο που πρέπει να κάνουμε είναι να κατεβάσουμε ένα μοντέλο γλώσσας που θα λειτουργήσει ως post‑processor για την ακατέργαστη έξοδο OCR. Η Aspose OCR παρέχει μια βοηθητική κλάση που ονομάζεται `AsposeAI` η οποία μπορεί αυτόματα να τραβήξει ένα μοντέλο από το HuggingFace hub.

```python
import aspose.ocr as aocr
from aspose.ocr import AsposeAI, AsposeAIModelConfig, OcrEngine

# Configure the model – it will auto‑download the first time you run it
model_config = AsposeAIModelConfig(
    allow_auto_download="true",                     # <-- enables auto‑download
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # smaller footprint on GPU
    gpu_layers=20,                                  # how many layers stay on GPU
    directory_model_path=r"YOUR_DIRECTORY"         # where the model files live
)
```

**Γιατί είναι σημαντικό:**  
- **download HuggingFace model python** – αποφεύγετε τη χειροκίνητη διαχείριση αρχείων zip ή την αυθεντικοποίηση με token.  
- Η χρήση ποσοτικοποίησης `int8` μειώνει το μέγεθος του μοντέλου περίπου στο ένα τέταρτο του αρχικού, κάτι κρίσιμο όταν αργότερα χρειαστεί να **release GPU memory python**.

> **Pro tip:** Κρατήστε το `directory_model_path` σε SSD για ταχύτερους χρόνους φόρτωσης.  

---

### 2. Initialise the AI Helper and Enable Spell‑Checking

Τώρα δημιουργούμε ένα στιγμιότυπο `AsposeAI` και προσθέτουμε έναν post‑processor ελέγχου ορθογραφίας. Εδώ αρχίζει η μαγεία του **clean OCR text python**.

```python
# Initialise the AI helper
ai_helper = AsposeAI()
ai_helper.set_post_processor(
    processor="spell_corrector",
    custom_settings={"max_edits": 2}   # allows up to two character edits per word
)
```

**Εξήγηση:**  
Ο ελεγκτής ορθογραφίας εξετάζει κάθε token από τη μηχανή OCR και προτείνει διορθώσεις περιορισμένες από το `max_edits`. Αυτή η μικρή βελτίωση μπορεί να μετατρέψει το “rec0gn1tion” σε “recognition” χωρίς τη χρήση βαρύ μοντέλου γλώσσας.

---

### 3. Hook the AI Helper into the OCR Engine

Η Aspose εισήγαγε μια νέα μέθοδο στην έκδοση 23.4 που επιτρέπει την ενσωμάτωση μιας AI μηχανής απευθείας στην αλυσίδα OCR.

```python
# Initialise the OCR engine and attach the AI helper
ocr_engine = OcrEngine()
ocr_engine.set_ai_engine(ai_helper)   # new in v23.4
```

**Γιατί το κάνουμε:**  
Συνδέοντας τον AI helper νωρίς, η μηχανή OCR μπορεί προαιρετικά να χρησιμοποιήσει το μοντέλο για βελτιώσεις σε πραγματικό χρόνο (π.χ., ανίχνευση διάταξης). Επιπλέον, διατηρεί τον κώδικα καθαρό—δεν χρειάζονται ξεχωριστοί βρόχοι post‑processing αργότερα.

---

### 4. Perform OCR on the Scanned Image

Αυτό είναι το κεντρικό βήμα που πραγματικά **perform OCR on image** αρχεία. Αντικαταστήστε το `YOUR_DIRECTORY/input.png` με τη διαδρομή του δικού σας σαρωμένου αρχείου.

```python
image_path = r"YOUR_DIRECTORY/input.png"
ocr_result = ocr_engine.recognize(image_path)

print("Raw OCR text:")
print(ocr_result.text)
```

Η τυπική ακατέργαστη έξοδος μπορεί να περιέχει αλλαγές γραμμής σε περίεργα σημεία, λανθασμένους χαρακτήρες ή άσχετα σύμβολα. Γι’ αυτό χρειάζεται το επόμενο βήμα.

**Αναμενόμενη ακατέργαστη έξοδος (παράδειγμα):**

```
Th1s 1s 4n ex4mpl3 0f r4w OCR t3xt.
It c0ntains numb3rs 123 and s0me m1stakes.
```

---

### 5. Clean OCR Text in Python with the AI Post‑Processor

Τώρα αφήνουμε το AI να καθαρίσει το χάος. Αυτό είναι η καρδιά της διαδικασίας **clean OCR text python**.

```python
cleaned_result = ocr_engine.run_postprocessor(ocr_result)

print("\nAI‑enhanced text:")
print(cleaned_result.text)
```

**Αποτέλεσμα που θα δείτε:**

```
This is an example of raw OCR text.
It contains numbers 123 and some mistakes.
```

Παρατηρήστε πώς ο ελεγκτής ορθογραφίας διόρθωσε το “Th1s” → “This” και αφαίρεσε το άσχετο “4n”. Το μοντέλο επίσης ομαλοποιεί τα κενά, κάτι που συχνά αποτελεί πρόβλημα όταν αργότερα τροφοδοτείτε το κείμενο σε downstream pipelines NLP.

---

### 6. Release GPU Memory in Python – Clean‑up Steps

Όταν τελειώσετε, είναι καλή πρακτική να ελευθερώσετε τους πόρους GPU, ειδικά αν τρέχετε πολλαπλές εργασίες OCR σε μια μακροχρόνια υπηρεσία.

```python
# Release resources – crucial for GPU memory
ai_helper.free_resources()
ocr_engine.dispose()
```

**Τι συμβαίνει στο παρασκήνιο:**  
Η `free_resources()` αποφορτώνει το μοντέλο από το GPU, επιστρέφοντας τη μνήμη στον οδηγό CUDA. Η `dispose()` κλείνει τις εσωτερικές μνήμες της μηχανής OCR. Η παράλειψη αυτών των κλήσεων μπορεί να οδηγήσει σε σφάλματα έλλειψης μνήμης μετά από λίγες μόνο εικόνες.

> **Θυμηθείτε:** Αν σκοπεύετε να επεξεργαστείτε παρτίδες σε βρόχο, καλέστε το clean‑up μετά από κάθε παρτίδα ή επαναχρησιμοποιήστε το ίδιο `ai_helper` χωρίς ελευθέρωση μέχρι το πολύ τέλος.

---

## Bonus: Προσαρμογή της Ροής Εργασίας για Διαφορετικά Σενάρια

### Ρύθμιση Ποσοτικοποίησης Μοντέλου

Αν διαθέτετε ισχυρό GPU (π.χ., RTX 4090) και θέλετε μεγαλύτερη ακρίβεια, αλλάξτε το `hugging_face_quantization` σε `"fp16"` και αυξήστε το `gpu_layers` σε `30`. Αυτό θα καταναλώσει περισσότερη μνήμη, οπότε θα χρειαστεί να **release GPU memory python** πιο επιθετικά μετά από κάθε παρτίδα.

### Χρήση Προσαρμοσμένου Ελεγκτή Ορθογραφίας

Μπορείτε να αντικαταστήσετε το ενσωματωμένο `spell_corrector` με έναν προσαρμοσμένο post‑processor που κάνει διορθώσεις ειδικές για το πεδίο σας (π.χ., ιατρική ορολογία). Απλώς υλοποιήστε τη απαιτούμενη διεπαφή και περάστε το όνομά του στο `set_post_processor`.

### Επεξεργασία Πολλών Εικόνων σε Παρτίδες

Τυλίξτε τα βήματα OCR μέσα σε έναν βρόχο `for`, συγκεντρώστε τα `cleaned_result.text` σε λίστα, και καλέστε το `ai_helper.free_resources()` μόνο μετά το βρόχο αν έχετε αρκετή μνήμη GPU. Αυτό μειώνει το κόστος φόρτωσης του μοντέλου επανειλημμένα.

---

## Συμπέρασμα

Σας δείξαμε πώς να **perform OCR on image** αρχεία σε Python, να **κατεβάσετε αυτόματα ένα μοντέλο HuggingFace**, να **καθαρίσετε το OCR κείμενο**, και να **απελευθερώσετε τη μνήμη GPU** με ασφάλεια όταν τελειώσετε. Το πλήρες script είναι έτοιμο για αντιγραφή‑επικόλληση, και οι εξηγήσεις σας δίνουν την αυτοπεποίθηση να το προσαρμόσετε σε μεγαλύτερα έργα.

Τι ακολουθεί; Δοκιμάστε να αντικαταστήσετε το μοντέλο Qwen 2.5 με μια μεγαλύτερη παραλλαγή LLaMA, πειραματιστείτε με διαφορετικούς post‑processors, ή ενσωματώστε την καθαρισμένη έξοδο σε έναν αναζητήσιμο δείκτη Elasticsearch. Οι δυνατότητες είναι ατελείωτες, και τώρα έχετε μια σταθερή βάση για να χτίσετε πάνω της.

Καλό coding, και εύχομαι οι OCR αλυσίδες σας να είναι πάντα καθαρές και φιλικές προς τη μνήμη!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}