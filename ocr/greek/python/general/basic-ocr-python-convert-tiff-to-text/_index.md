---
category: general
date: 2026-03-18
description: Βασικός οδηγός OCR σε Python δείχνει πώς να μετατρέψετε TIFF σε κείμενο,
  να φορτώσετε OCR εικόνας, να ορίσετε επίπεδα GPU και να διορθώσετε τα αρχικά μηδενικά
  με το Aspose AI.
draft: false
keywords:
- basic ocr python
- convert tiff to text
- load image ocr
- set gpu layers
- fix leading zeroes
language: el
og_description: Βασικό σεμινάριο OCR σε Python σας καθοδηγεί στη μετατροπή αρχείων
  TIFF σε καθαρό κείμενο, τη φόρτωση εικόνων, τη ρύθμιση επιπέδων GPU και τη διόρθωση
  αρχικών μηδενικών.
og_title: Βασικό OCR Python – μετατροπή TIFF σε κείμενο
tags:
- OCR
- Python
- AI
- Aspose
title: βασικό OCR Python – μετατροπή TIFF σε κείμενο
url: /el/python/general/basic-ocr-python-convert-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# basic ocr python – Μετατροπή TIFF σε Κείμενο με AI Post‑Processing

Ψάχνετε έναν τρόπο να κάνετε **basic ocr python** στα σαρωμένα έγγραφά σας; Σε αυτόν τον οδηγό θα περάσουμε από τη μετατροπή ενός αρχείου TIFF σε καθαρό, αναζητήσιμο κείμενο χρησιμοποιώντας το Aspose OCR και έναν AI post‑processor.  

Αν έχετε ποτέ δυσκολευτεί να **convert TIFF to text** επειδή το ακατέργαστο αποτέλεσμα είναι γεμάτο τυπογραφικά λάθη ή περίεργα σύμβολα, δεν είστε μόνοι. Θα σας δείξουμε επίσης πώς να **load image OCR**, να ρυθμίσετε τη μηχανή με **set GPU layers**, και ακόμη να **fix leading zeroes** που εμφανίζονται συχνά σε αριθμούς τιμολογίων.

## Τι Θα Μάθετε

- Πώς να αρχικοποιήσετε τη μηχανή Aspose OCR για έντυπα έγγραφα.  
- Τα ακριβή βήματα για **load image OCR** από αρχείο TIFF και λήψη ακατέργαστου κειμένου.  
- Διαμόρφωση μοντέλου AI, αυτόματη λήψη του και **set GPU layers** για ταχύτερη πρόβλεψη.  
- Προσθήκη ενσωματωμένου ελέγχου ορθογραφίας μαζί με μια προσαρμοσμένη λειτουργία που **fixes leading zeroes**.  
- Καθαρισμός του αποτελέσματος OCR και σωστή απελευθέρωση πόρων.  

Στο τέλος αυτού του tutorial θα έχετε ένα ενιαίο, επαναχρησιμοποιήσιμο script Python που μετατρέπει οποιοδήποτε TIFF σε γυαλισμένο, αναζητήσιμο κείμενο — χωρίς ανάγκη χειροκίνητης αντιγραφής‑επικόλλησης.  

### Προαπαιτήσεις

- Python 3.8+ εγκατεστημένο στον υπολογιστή σας.  
- `aspose-ocr` package (`pip install aspose-ocr`).  
- Προαιρετικά: μια GPU με τουλάχιστον 4 GB VRAM αν θέλετε να **set GPU layers**· διαφορετικά ο κώδικας επιστρέφει αυτόματα στην CPU.  

---

## basic ocr python – φόρτωση εικόνας και αναγνώριση κειμένου

Το πρώτο πράγμα που πρέπει να κάνουμε είναι **load image OCR** ώστε η μηχανή να μπορεί να διαβάσει τα pixel. Η `OcrEngine` της Aspose υποστηρίζει πολλές μορφές, αλλά εδώ εστιάζουμε στο TIFF επειδή είναι το πιο κοινό για σαρωμένα τιμολόγια.

```python
import aspose.ocr as ocr

# Initialise the OCR engine for printed documents
ocr_engine = ocr.OcrEngine()
ocr_engine.set_recognition_mode(ocr.RecognitionMode.PRINTED)   # use HANDWRITTEN for handwritten docs

# Load the TIFF file – replace with your own path
ocr_engine.load_image("YOUR_DIRECTORY/input.tif")
```

> **Pro tip:** Αν εργάζεστε με multi‑page TIFFs, η Aspose επεξεργάζεται αυτόματα κάθε σελίδα διαδοχικά, οπότε δεν χρειάζονται επιπλέον βρόχοι.

Τώρα που η εικόνα έχει φορτωθεί, ας τρέξουμε μια βασική αναγνώριση.

```python
# Perform basic OCR and capture the raw string
raw_text = ocr_engine.recognize()
print("Raw OCR:", raw_text)
```

Θα δείτε κάτι όπως:

```
Raw OCR: Inv0ce N0: 0123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

Παρατηρήσατε τα *μηδενικά* πριν από τα γράμματα; Αυτό είναι ένα κλασικό artefact OCR που θα καθαρίσουμε αργότερα.

![ροή εργασίας basic ocr python](/images/ocr-workflow.png "διάγραμμα ροής εργασίας basic ocr python")

---

## Βήμα 2: Μετατροπή TIFF σε κείμενο – προετοιμασία του AI post‑processor

Το ακατέργαστο OCR είναι χρήσιμο, αλλά οι περισσότερες παραγωγικές pipelines χρειάζονται μια γυαλισμένη έκδοση. Η Aspose παρέχει ένα wrapper `AsposeAI` που μπορεί να κατεβάσει ένα μοντέλο από το Hugging Face, να το τρέξει στην GPU, και να εφαρμόσει αυτόματα ορθογραφικό έλεγχο.

```python
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# Configure the AI model – we’ll download Qwen2.5‑3B‑Instruct automatically
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    directory_model_path="YOUR_DIRECTORY/ocr_ai_models",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=25          # <-- this is where we **set GPU layers**
)

ocr_ai = AsposeAI(ai_config)
```

### Γιατί το `set GPU layers` είναι σημαντικό

Η παράμετρος `gpu_layers` λέει στο υποκείμενο μοντέλο GGUF πόσα transformer layers να διατηρηθούν στην GPU. Περισσότερα layers = ταχύτερη πρόβλεψη αλλά μεγαλύτερη χρήση VRAM. Αν χρησιμοποιείτε ένα μέτριο laptop, μειώστε την τιμή σε `10` ή παραλείψτε την εντελώς για να παραμείνει στην CPU.

---

## Βήμα 3: Εφαρμογή ελέγχου ορθογραφίας και **fix leading zeroes**

Η Aspose AI έρχεται με ενσωματωμένο spell‑checker, που εντοπίζει τα περισσότερα αγγλικά ορθογραφικά λάθη. Ωστόσο, διορθώσεις ειδικές για το domain — όπως η μετατροπή ενός αρχικού `0` σε `O` για κωδικούς τιμολογίων — απαιτούν προσαρμοσμένο post‑processor.

```python
# Enable the built‑in spell‑check
ocr_ai.set_post_processor("spellcheck")

# Custom function to replace a leading zero before three capital letters
def invoice_fix(txt: str) -> str:
    import re
    # Example: "0ABC" -> "OABC"
    return re.sub(r"\b0([A-Z]{3})\b", r"O\1", txt)

# Register the custom fix – it runs after spellcheck
ocr_ai.set_post_processor(invoice_fix)
```

> **Why this works:** Η κανονική έκφραση ψάχνει για ένα όριο λέξης (`\b`), ένα μηδέν, και μετά ακριβώς τρία κεφαλαία γράμματα. Στη συνέχεια αντικαθιστά το μηδέν με το γράμμα “O”. Μπορείτε να επεκτείνετε το μοτίβο για άλλες ιδιομορφίες (π.χ., `0[0-9]{2}` για λανθασμένα διαβασμένους αριθμούς).

---

## Βήμα 4: Καθαρισμός του αποτελέσματος OCR με το AI post‑processor

Τώρα συνδυάζουμε τα πάντα: το ακατέργαστο string από **basic ocr python**, τον έλεγχο ορθογραφίας, και τη διόρθωση μηδενικών. Η μέθοδος `run_postprocessor` επιστρέφει μια καθαρή έκδοση έτοιμη για downstream συστήματα.

```python
cleaned_text = ocr_ai.run_postprocessor(raw_text)
print("\nCleaned OCR:", cleaned_text)
```

Τυπική έξοδος μετά το post‑processor:

```
Cleaned OCR: Invoice No: O123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

Μπορείτε να δείτε ότι το αρχικό μηδέν έχει μετατραπεί σε `O`, και τα κοινά ορθογραφικά λάθη έχουν διορθωθεί. Το κείμενο είναι πλέον κατάλληλο για ευρετηρίαση σε μηχανή αναζήτησης ή για τροφοδοσία σε pipeline εξαγωγής δεδομένων.

---

## Βήμα 5: Απελευθέρωση πόρων AI – κρατήστε την GPU σας ευχαριστημένη

Αν τρέχετε πολλαπλές εργασίες OCR σε μια μακροχρόνια υπηρεσία, είναι καλή πρακτική να ελευθερώνετε τη μνήμη GPU του μοντέλου όταν τελειώσετε.

```python
ocr_ai.free_resources()
```

Η παράλειψη αυτού του βήματος μπορεί να οδηγήσει σε σφάλματα “out‑of‑memory” σε επόμενες κλήσεις, ειδικά όταν **set GPU layers** σε υψηλή τιμή.

---

## Προαιρετικές Παραλλαγές & Ακραίες Περιπτώσεις

| Situation | What to change |
|-----------|----------------|
| **Χειρόγραφα έγγραφα** | Use `ocr_engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)` instead of `PRINTED`. |
| **Δεν υπάρχει GPU** | Set `gpu_layers=0` or omit the argument; the model will run on CPU (slower but safe). |
| **Διαφορετική γλώσσα** | Swap the Hugging Face repo ID to a language‑specific model, e.g., `microsoft/Florence-2-base`. |
| **Επεξεργασία παρτίδας** | Wrap the steps in a `for file in glob("*.tif"):` loop and accumulate results in a list or CSV. |
| **Πιο σύνθετα μοτίβα μηδενικών** | Extend `invoice_fix` with additional regexes, such as `r"\b0+([A-Z]{2,})\b"` for multiple leading zeroes. |

---

## Συμπέρασμα

Μόλις ολοκληρώσαμε μια **basic ocr python** pipeline που φορτώνει ένα TIFF, εξάγει ακατέργαστο κείμενο, και στη συνέχεια το καθαρίζει χρησιμοποιώντας ένα μοντέλο AI ενώ **sets GPU layers** για απόδοση. Ο προσαρμοσμένος post‑processor δείχνει πώς να **fix leading zeroes**, μια μικρή αλλά συχνά παραβλεπόμενη λεπτομέρεια που μπορεί να διακόψει downstream analytics.

Νιώστε ελεύθεροι να πειραματιστείτε: δοκιμάστε διαφορετική ποσοτικοποίηση (`float16` για υψηλότερη ακρίβεια), αντικαταστήστε τον έλεγχο ορθογραφίας με ένα domain‑specific λεξικό, ή συνδέστε πολλαπλές προσαρμοσμένες διορθώσεις μαζί. Το μοτίβο παραμένει το ίδιο — φόρτωση, αναγνώριση, διαμόρφωση AI, post‑process, και καθαρισμός.

**Επόμενα βήματα** που μπορείτε να εξερευνήσετε περιλαμβάνουν:

- Ενσωμάτωση του καθαρισμένου αποτελέσματος σε βάση δεδομένων ή ευρετήριο Elasticsearch.  
- Χρήση της ίδιας προσέγγισης για **convert TIFF to text** σε πολυγλωσσικά PDF.  
- Προσθήκη UI με Flask ή FastAPI ώστε μη‑τεχνικοί χρήστες να μπορούν να ανεβάζουν αρχεία και να λαμβάνουν καθαρό κείμενο άμεσα.  

Καλή προγραμματιστική εργασία, και εύχομαι τα OCR αποτελέσματά σας να είναι πάντα καθαρά και χωρίς μηδενικά!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}