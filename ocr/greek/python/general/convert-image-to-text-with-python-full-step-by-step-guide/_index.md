---
category: general
date: 2026-03-26
description: Μετατρέψτε την εικόνα σε κείμενο χρησιμοποιώντας το Aspose OCR και καθαρίστε
  το κείμενο OCR με Python. Μάθετε πώς να εξάγετε κείμενο από εικόνα και να το επεξεργαστείτε
  σε ένα ενιαίο script.
draft: false
keywords:
- convert image to text
- how to extract image text
- clean ocr text python
- Aspose OCR Python
- AI spell‑checker Python
- post‑process OCR output
language: el
og_description: Μετατρέψτε την εικόνα σε κείμενο γρήγορα. Αυτός ο οδηγός δείχνει πώς
  να εξάγετε το κείμενο από εικόνα και να καθαρίσετε το κείμενο OCR με στυλ Python,
  χρησιμοποιώντας το Aspose OCR και έναν AI ελεγκτή ορθογραφίας.
og_title: Μετατροπή εικόνας σε κείμενο με Python – Πλήρης οδηγός
tags:
- OCR
- Python
- Aspose
- AI
title: Μετατροπή εικόνας σε κείμενο με Python – Πλήρης οδηγός βήμα‑βήμα
url: /el/python/general/convert-image-to-text-with-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή Εικόνας σε Κείμενο – Πλήρης Οδηγός Python

Έχετε ποτέ χρειαστεί να **convert image to text** αλλά να λαμβάνετε ακατάστατα αποτελέσματα; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν προβλήματα όταν η έξοδος OCR είναι γεμάτη ορθογραφικά λάθη, περιττά σύμβολα ή λανθασμένα διαστήματα γραμμών. Τα καλά νέα; Με μερικές γραμμές Python και Aspose OCR, μπορείτε να εξάγετε απλό κείμενο από οποιαδήποτε εικόνα **and** να το καθαρίσετε αυτόματα.

Σε αυτόν τον οδηγό θα σας δείξουμε **how to extract image text**, έπειτα να εκτελέσετε έναν AI‑powered spell‑checker για να παράγετε επεξεργασμένο, ευανάγνωστο περιεχόμενο. Στο τέλος θα έχετε ένα ενιαίο script που μετατρέπει ένα αρχείο PNG σε ένα καθαρό αρχείο `.txt`—χωρίς να χρειάζεται χειροκίνητη αντιγραφή‑επικόλληση.  

> **Τι θα μάθετε**  
> * Εγκατάσταση και ρύθμιση του Aspose OCR.  
> * Αναγνώριση κειμένου από αρχείο εικόνας.  
> * Αρχικοποίηση μοντέλου Aspose AI για spell‑checking.  
> * Εφαρμογή του post‑processor για καθαρισμό της εξόδου OCR.  
> * Αποθήκευση του τελικού αποτελέσματος και απελευθέρωση πόρων.  

Όλα αυτά λειτουργούν με στυλ **clean OCR text python**—δηλαδή ο κώδικας είναι έτοιμος να ενσωματωθεί σε οποιοδήποτε έργο χωρίς πρόσθετες περιβλήσεις.

---

## Προαπαιτούμενα

Πριν προχωρήσουμε, βεβαιωθείτε ότι έχετε:

| Απαίτηση | Γιατί είναι σημαντικό |
|-------------|----------------|
| Python 3.9 or newer | Modern syntax & type hints |
| `asposeocr` package (`pip install asposeocr`) | Core OCR engine |
| Internet access (first run) | Model auto‑download from Hugging Face |
| A PNG/JPEG image you want to read | Input source |

Δεν απαιτείται GPU, αλλά αν έχετε ένα, το μοντέλο AI θα το χρησιμοποιήσει αυτόματα για ταχύτερο spell‑checking.

---

## Βήμα 1: Μετατροπή Εικόνας σε Κείμενο με Aspose OCR

Το πρώτο που χρειαζόμαστε είναι μια αξιόπιστη μηχανή OCR. Το Aspose OCR είναι εμπορική βιβλιοθήκη, αλλά προσφέρει γενναιόδωρο δωρεάν επίπεδο για ανάπτυξη. Παρακάτω αρχικοποιούμε τη μηχανή, ορίζουμε τα Αγγλικά ως γλώσσα και ενεργοποιούμε την auto‑skew correction για να διαχειριστούμε κλίσεις σκαναρίσματος.

```python
import asposeocr as ocr

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English   # English language pack
ocr_engine.auto_skew = True                  # Auto‑deskew images
```

> **Γιατί να ενεργοποιήσετε το `auto_skew`;**  
> Πολλά σαρωμένα έγγραφα δεν είναι τέλεια επίπεδα. Το Auto‑skew περιστρέφει την εικόνα ακριβώς όσο χρειάζεται για να βελτιώσει την αναγνώριση χαρακτήρων, μειώνοντας έτσι τον αριθμό των ακατάστατων λέξεων που θα πρέπει να καθαρίσετε αργότερα.

Τώρα τροφοδοτούμε ένα αρχείο εικόνας στη μηχανή:

```python
# Recognise text from the input image (replace with your own path)
ocr_result = ocr_engine.recognize_image("YOUR_DIRECTORY/input_image.png")
print("Raw OCR output:")
print(ocr_result.text[:200])  # Show first 200 characters for sanity check
```

Η ιδιότητα `ocr_result.text` περιέχει τη ακατέργαστη συμβολοσειρά που εξήχθη από την εικόνα. Σε αυτό το στάδιο πιθανότατα θα παρατηρήσετε περιττά σημεία στίξης, ιδιαιτερότητες στις αλλαγές γραμμής ή ακόμη και μερικές λανθασμένες λέξεις—ακριβώς το πρόβλημα που θέλαμε να λύσουμε.

![convert image to text workflow](image.png){alt="convert image to text workflow diagram"}

---

## Βήμα 2: Ρύθμιση του AI Spell‑Checker (Clean OCR Text Python)

Ο καθαρισμός της εξόδου OCR μπορεί να είναι τόσο απλός όσο μια αντικατάσταση regex, αλλά για πραγματικά ευανάγνωστο κείμενο θα χρησιμοποιήσουμε το Aspose AI με ένα ελαφρύ LLM που ειδικεύεται στο spell‑checking. Το μοντέλο λαμβάνεται από το Hugging Face την πρώτη φορά που εκτελείτε το script, ώστε να μην χρειάζεται να κατεβάσετε τίποτα χειροκίνητα.

```python
from asposeocr import AsposeAI, AsposeAIModelConfig

# Model configuration – auto‑download enabled
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="bartowski/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=30                # Use GPU if available, otherwise CPU fallback
)

# Initialise the AI spell‑checker
spell_checker = AsposeAI()
spell_checker.initialize(model_cfg)
spell_checker.set_post_processor("spell_check")
```

**Γιατί αυτό το συγκεκριμένο μοντέλο;**  
`Qwen2.5‑3B‑Instruct‑GGUF` είναι ένα συμπαγές μοντέλο 3‑δισεκατομμυρίων παραμέτρων, βελτιστοποιημένο για εντολές, που τρέχει άνετα σε GPU laptop (ή ακόμη και CPU με int8 quantisation). Είναι αρκετά γρήγορο για spell‑checking γραμμή‑γραμμή χωρίς να καταναλώνει μνήμη.

---

## Βήμα 3: Εφαρμογή Spell‑Checking στην Έξοδο OCR

Με το κείμενο OCR στα χέρια και το μοντέλο AI έτοιμο, απλώς τροφοδοτούμε τη ακατέργαστη συμβολοσειρά στον post‑processor. Η μέθοδος επιστρέφει μια καθαρισμένη έκδοση που μπορείτε να γράψετε απευθείας στο δίσκο.

```python
# Run the spell‑checking post‑processor
corrected_text = spell_checker.run_postprocessor(ocr_result.text)

print("\nCleaned OCR output (first 200 chars):")
print(corrected_text[:200])
```

Τυπικές βελτιώσεις που θα δείτε:

* “teh” → “the”  
* “recieve” → “receive”  
* Έλλειψη κενών μετά την στίξη – διορθώνεται αυτόματα  
* Παράξενες αλλαγές γραμμής μετατρέπονται σε σωστές προτάσεις  

Αν χρειάζεστε περισσότερο έλεγχο, μπορείτε να περάσετε ένα προσαρμοσμένο prompt στο `run_postprocessor`, αλλά η προεπιλογή “spell_check” λειτουργεί για τις περισσότερες περιπτώσεις.

---

## Βήμα 4: Αποθήκευση του Καθαρισμένου Κειμένου σε Αρχείο

Τώρα που το κείμενο είναι τακτοποιημένο, το αποθηκεύουμε. Η χρήση UTF‑8 εξασφαλίζει ότι τυχόν ειδικοί χαρακτήρες (π.χ., τονισμένα γράμματα) παραμένουν.

```python
output_path = "YOUR_DIRECTORY/output_text.txt"

with open(output_path, "w", encoding="utf-8") as out_file:
    out_file.write(corrected_text)

print(f"\n✅ Processing complete: input_image.png → {output_path}")
```

Μπορείτε να ανοίξετε το αρχείο σε οποιονδήποτε επεξεργαστή και θα δείτε ένα ανθρώπινα αναγνώσιμο έγγραφο έτοιμο για επεξεργασία downstream—είτε τροφοδοτώντας ένα μοντέλο γλώσσας, είτε δημιουργώντας ευρετήριο για αναζήτηση, είτε απλώς αρχειοθετώντας.

---

## Βήμα 5: Απελευθέρωση Πόρων AI (Καλή Διαχείριση)

Το Aspose AI κρατά τα βάρη του μοντέλου στη μνήμη. Η απελευθέρωσή τους όταν τελειώσετε αποτρέπει διαρροές μνήμης, ειδικά σε υπηρεσίες που τρέχουν για μεγάλο χρονικό διάστημα.

```python
spell_checker.free_resources()
```

Αυτό είναι! Ολόκληρη η αλυσίδα—από εικόνα σε καθαρό κείμενο—ταιριάζει σε λιγότερο από 30 γραμμές Python.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν η εικόνα δεν είναι στα Αγγλικά;

Ορίστε `ocr_engine.language` στην κατάλληλη enum, π.χ., `ocr.Language.French`. Το μοντέλο spell‑checker είναι γλωσσικά ανεξάρτητο για βασική ορθογραφία, αλλά ίσως θέλετε ένα πολυγλωσσικό μοντέλο για καλύτερα αποτελέσματα.

### Η GPU μου έχει μόνο 20 layers—μπορώ ακόμα να χρησιμοποιήσω το μοντέλο;

Απόλυτα. Απλώς μειώστε το `gpu_layers` σε `20` (ή `0` για καθαρό CPU). Η βιβλιοθήκη θα επιστρέψει αυτόματα στο CPU για τα υπόλοιπα layers.

### Αποτυγχάνει η λήψη του μοντέλου πίσω από εταιρικό proxy;

Περάστε τη ρύθμιση του proxy μέσω μεταβλητών περιβάλλοντος (`HTTP_PROXY`, `HTTPS_PROXY`) πριν τρέξετε το script. Η διαδικασία λήψης σέβεται αυτές τις ρυθμίσεις.

### Χρειάζομαι μόνο έναν γρήγορο καθαρισμό regex, όχι AI;

Μπορείτε να παραλείψετε το βήμα AI και να εκτελέσετε έναν απλό καθαρισμό:

```python
import re
clean = re.sub(r'\s+', ' ', ocr_result.text).strip()
```

Αλλά θυμηθείτε, το regex δεν θα διορθώσει πραγματικά ορθογραφικά λάθη—το AI το κάνει για εσάς.

---

## Πλήρες Λειτουργικό Script

Παρακάτω είναι το πλήρες, έτοιμο‑για‑εκτέλεση script. Αντικαταστήστε το `YOUR_DIRECTORY` με το φάκελο που περιέχει την εικόνα σας και όπου θέλετε να αποθηκευτεί το αρχείο εξόδου.

```python
import asposeocr as ocr
from asposeocr import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1 – Initialise OCR engine
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English
ocr_engine.auto_skew = True

# -------------------------------------------------
# Step 2 – Recognise text from image
# -------------------------------------------------
ocr_result = ocr_engine.recognize_image("YOUR_DIRECTORY/input_image.png")
print("Raw OCR (first 200 chars):")
print(ocr_result.text[:200])

# -------------------------------------------------
# Step 3 – Configure AI spell‑checker
# -------------------------------------------------
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="bartowski/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=30
)

spell_checker = AsposeAI()
spell_checker.initialize(model_cfg)
spell_checker.set_post_processor("spell_check")

# -------------------------------------------------
# Step 4 – Clean the OCR output
# -------------------------------------------------
corrected_text = spell_checker.run_postprocessor(ocr_result.text)
print("\nCleaned OCR (first 200 chars):")
print(corrected_text[:200])

# -------------------------------------------------
# Step 5 – Write to file
# -------------------------------------------------
output_path = "YOUR_DIRECTORY/output_text.txt"
with open(output_path, "w", encoding="utf-8") as out_file:
    out_file.write(corrected_text)

print(f"\nProcessing complete: input_image.png → {output_path}")

# -------------------------------------------------
# Step 6 – Free AI resources
# -------------------------------------------------
spell_checker.free_resources()
```

Η εκτέλεση αυτού του script θα δημιουργήσει το `output_text.txt` που περιέχει την επεξεργασμένη μεταγραφή της εικόνας σας.

---

## Συμπέρασμα

Μόλις περάσαμε από έναν πρακτικό τρόπο για **convert image to text** χρησιμοποιώντας Aspose OCR, έπειτα **clean OCR text python**‑style με έναν AI spell‑checker. Η λύση είναι αυτόνομη, απαιτεί μόνο ένα αρχείο Python και λειτουργεί σε Windows, macOS ή Linux.

Αν ψάχνετε το επόμενο βήμα, σκεφτείτε:

* **How to extract image text** από PDFs μετατρέποντας πρώτα τις σελίδες σε εικόνες.  
* Τροφοδοσία του καθαρισμένου κειμένου σε μοντέλο summarisation για αυτόματη δημιουργία αναφορών.  
* Αποθήκευση των αποτελεσμάτων σε βάση δεδομένων vector για semantic search.

Δοκιμάστε το, πειραματιστείτε με τις παραμέτρους του μοντέλου, και αφήστε την αλυσίδα OCR‑to‑text να γίνει βασικό εργαλείο στην εργαλειοθήκη εισαγωγής δεδομένων σας. Καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}