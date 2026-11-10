---
category: general
date: 2026-02-27
description: Μάθετε πώς να διορθώνετε σφάλματα OCR και να εξάγετε κείμενο από εικόνα
  χρησιμοποιώντας το Aspose OCR σε Python. Αυτός ο οδηγός δείχνει πώς να φορτώνετε
  εικόνα για OCR και να καθαρίζετε τα αποτελέσματα.
draft: false
keywords:
- extract text from image
- load image for ocr
- how to correct ocr errors
- Aspose OCR Python
- OCR post‑processing
og_description: Μάθετε πώς να διορθώνετε σφάλματα OCR και να εξάγετε κείμενο από εικόνα
  χρησιμοποιώντας το Aspose OCR σε Python. Ακολουθήστε αυτόν τον βήμα‑βήμα οδηγό.
og_title: Πώς να διορθώσετε σφάλματα OCR – Εξαγωγή κειμένου από εικόνα με το Aspose
  OCR
tags:
- OCR
- Python
- Aspose
- Text Extraction
title: Πώς να διορθώσετε σφάλματα OCR – Εξαγωγή κειμένου από εικόνα με Aspose OCR
  – Οδηγός βήμα‑προς‑βήμα
url: /el/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Διορθώσετε Σφάλματα OCR – Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Βήμα‑βήμα

Αν ποτέ χρειάστηκε να **εξάγετε κείμενο από εικόνα** σε ένα έργο Python και βρεθήκατε να παλεύετε με ακατάστατο αποτέλεσμα OCR, βρίσκεστε στο σωστό μέρος. Σε πολλά σενάρια αυτοματοποίησης—επεξεργασία τιμολογίων, σάρωση αποδείξεων ή ψηφιοποίηση ιστορικών εγγράφων—η πρώτη πρόκληση είναι η μετατροπή μιας φωτογραφίας σε καθαρό, αναζητήσιμο κείμενο. Αυτό το tutorial δείχνει **πώς να διορθώσετε σφάλματα OCR** χρησιμοποιώντας το AI‑powered spell‑check της Aspose, καλύπτοντας επίσης τα βασικά βήματα για **φόρτωση εικόνας για OCR** και λήψη αξιόπιστων αποτελεσμάτων.

## Γρήγορες Απαντήσεις
- **Ποια βιβλιοθήκη πρέπει να χρησιμοποιήσω;** Aspose OCR for Python
- **Μπορώ να διορθώσω τα ορθογραφικά λάθη αυτόματα;** Ναι, με τον ενσωματωμένο AI spell‑check processor
- **Χρειάζομαι άδεια;** Μια δοκιμαστική έκδοση λειτουργεί για δοκιμές· απαιτείται εμπορική άδεια για παραγωγή
- **Είναι συμβατό με Python‑3;** Λειτουργεί με Python 3.8 και νεότερες εκδόσεις
- **Μπορώ να επεξεργαστώ PDFs;** Μετατρέψτε πρώτα τις σελίδες PDF σε εικόνες (δείτε “convert pdf to images for ocr”)

## Τι σημαίνει «πώς να διορθώσετε σφάλματα OCR»;
Η διόρθωση σφαλμάτων OCR σημαίνει ότι παίρνετε τη ακατέργαστη συμβολοσειρά που παράγει η μηχανή OCR και διορθώνετε αυτόματα ορθογραφικά λάθη, λανθασμένους χαρακτήρες και προβλήματα μορφοποίησης ώστε το κείμενο να μπορεί να χρησιμοποιηθεί αξιόπιστα σε επόμενα στάδια (αναζήτηση, ανάλυση ή εισαγωγή δεδομένων).

## Γιατί να χρησιμοποιήσετε Aspose OCR για Python;
Το Aspose OCR συνδυάζει έναν γρήγορο, ακριβή μηχανισμό αναγνώρισης με έναν προαιρετικό AI post‑processor που διαχειρίζεται ορθογραφικό έλεγχο και βασικές διορθώσεις γραμματικής. Είναι ένα πλήρες **aspose ocr tutorial** σε ένα πακέτο, επιτρέποντάς σας να περάσετε από την εικόνα στο καθαρό κείμενο χωρίς εξωτερικά εργαλεία.

## Προαπαιτούμενα
- Python 3.8+ εγκατεστημένο
- Έγκυρη άδεια Aspose OCR (ή δωρεάν δοκιμή)
- Ένα αρχείο εικόνας όπως `invoice.png` που θέλετε να επεξεργαστείτε
- Προαιρετικά: `pdf2image` αν χρειάζεται **convert pdf to images for OCR**

## Οδηγός Βήμα‑βήμα

### Βήμα 1: Εγκατάσταση Aspose OCR και του AI post‑processor
```bash
pip install aspose-ocr
```

```bash
pip install aspose-ocr-ai
```

> **Pro tip:** Κρατήστε τα πακέτα ενημερωμένα. Κατά τη στιγμή της συγγραφής, οι τελευταίες εκδόσεις είναι `aspose-ocr 23.12` και `aspose-ocr-ai 23.12`.

### Βήμα 2: Εισαγωγή των απαιτούμενων κλάσεων
```python
# Step 1: Import the OCR and AI classes
from aspose.ocr import OcrEngine, AsposeAI
```

### Βήμα 3: Δημιουργία του μηχανισμού και **φόρτωση εικόνας για OCR**
```python
# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()

# Step 3: Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")
```

> **Explanation:** Η `load_image()` δέχεται διαδρομή, ροή ή πίνακα byte, ώστε να μπορείτε να τροφοδοτείτε εικόνες από δίσκο, το web ή ένα buffer στη μνήμη.

#### Συνηθισμένα προβλήματα κατά τη φόρτωση εικόνων
| Πρόβλημα | Συμπτωμα | Διόρθωση |
|----------|----------|----------|
| Χαμηλό DPI (<300) | Κατεστραμμένοι χαρακτήρες, λείπουν αριθμοί | Επαναδειγματοληψία σε ≥ 300 dpi πριν τη φόρτωση |
| Κατάσταση χρώματος CMYK | Λάθος σχήματα χαρακτήρων | Μετατροπή σε RGB με Pillow (`Image.convert("RGB")`) |
| PDF πολλαπλών σελίδων | Επεξεργάζεται μόνο την πρώτη σελίδα | **Convert PDF to images for OCR** χρησιμοποιώντας `pdf2image` και βρόχο για κάθε σελίδα |

### Βήμα 4: Εκτέλεση OCR για λήψη της ακατέργαστης συμβολοσειράς
```python
# Step 4: Perform OCR to extract raw text
raw_text = ocr_engine.recognize()
print("Raw OCR output:")
print(raw_text)
```

### Βήμα 5: Αρχικοποίηση του AI spell‑check επεξεργαστή (ο πυρήνας του **πώς να διορθώσετε σφάλματα OCR**)
```python
# Step 5: Initialise the AI post‑processor and choose a spell‑check processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("spell_check")
```

Μπορείτε να αντικαταστήσετε το `"spell_check"` με `"grammar_check"` ή `"named_entity_recognition"` για άλλες περιπτώσεις χρήσης.

### Βήμα 6: Καθαρισμός της εξόδου OCR
```python
# Step 6: Clean the OCR output using the selected post‑processor
clean_text = ai_processor.run_postprocessor(raw_text)

# Step 7: Output the corrected text
print("\nCorrected OCR output:")
print(clean_text)
```

**Τι κάνει ο spell‑check:** Τokenizes το κείμενο, ελέγχει κάθε token σε αγγλικό λεξικό (ή σε προσαρμοσμένο που παρέχετε), βαθμολογεί εναλλακτικές λύσεις με ένα ελαφρύ μοντέλο γλώσσας και επιστρέφει τη πιο πιθανή διόρθωση.

#### Μη‑Αγγλικές γλώσσες
Περάστε τον κωδικό γλώσσας όταν δημιουργείτε το `AsposeAI`, π.χ., `AsposeAI(language="fr")` για γαλλικά.

### Βήμα 7: Αποθήκευση του καθαρισμένου αποτελέσματος
```python
# Example: Save the cleaned text to a .txt file for later indexing
with open("invoice_extracted.txt", "w", encoding="utf-8") as f:
    f.write(clean_text)

print("\n✅ Cleaned text saved to invoice_extracted.txt")
```

### Πλήρες Παράδειγμα Λειτουργίας
Παρακάτω είναι το πλήρες script που μπορείτε να αντιγράψετε‑επικολλήσετε στο `extract_invoice.py`. Υποθέτει ότι τα δύο πακέτα Aspose είναι εγκατεστημένα και η εικόνα βρίσκεται στο `YOUR_DIRECTORY/invoice.png`.

```python
# extract_invoice.py
# -------------------------------------------------------------
# Complete example: extract text from image and correct OCR errors
# -------------------------------------------------------------

# 1️⃣ Import required classes
from aspose.ocr import OcrEngine, AsposeAI

# 2️⃣ Create OCR engine and load the target image
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")

# 3️⃣ Run OCR – get raw text
raw_text = ocr_engine.recognize()
print("Raw OCR output:")
print(raw_text)

# 4️⃣ Initialise AI spell‑check post‑processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("spell_check")

# 5️⃣ Clean the OCR output
clean_text = ai_processor.run_postprocessor(raw_text)

# 6️⃣ Show the corrected result
print("\nCorrected OCR output:")
print(clean_text)

# 7️⃣ Persist the cleaned text for later use
with open("invoice_extracted.txt", "w", encoding="utf-8") as out_file:
    out_file.write(clean_text)

print("\n✅ Cleaned text saved to invoice_extracted.txt")
```

Τρέξτε το με:

```bash
python extract_invoice.py
```

Θα δείτε το ακατέργαστο dump, την τακτοποιημένη έκδοση και ένα αρχείο με όνομα `invoice_extracted.txt` στον ίδιο φάκελο.

## Πώς να διορθώσετε σφάλματα OCR σε άλλα σενάρια;
- **Επεξεργασία παρτίδας:** Τυλίξτε τη βασική λογική σε μια συνάρτηση και χρησιμοποιήστε `concurrent.futures.ThreadPoolExecutor` για παράλληλη επεξεργασία πολλών εικόνων.
- **Έγγραφα PDF:** Χρησιμοποιήστε `pdf2image` για να μετατρέψετε κάθε σελίδα σε PNG, έπειτα τροφοδοτήστε κάθε PNG μέσω του script. Αυτό υλοποιεί τη ροή εργασίας “convert pdf to images for ocr”.
- **Προσαρμοσμένα λεξικά:** Περάστε μια λίστα με όρους ειδικού τομέα στο `AsposeAI` μέσω `set_custom_dictionary()` για βελτίωση της ακρίβειας του spell‑check σε τιμολόγια, ιατρικές αναφορές κ.λπ.

## Συχνές Ερωτήσεις

**Ε: Λειτουργεί αυτό απευθείας με PDFs;**  
Α: Όχι απευθείας. Μετατρέψτε πρώτα κάθε σελίδα PDF σε εικόνα (π.χ., με `pdf2image`) και έπειτα τρέξτε το script OCR σε κάθε PNG.

**Ε: Η πηγαία μου γλώσσα δεν είναι τα Αγγλικά—μπορώ ακόμα να χρησιμοποιήσω το spell‑check;**  
Α: Ναι. Αρχικοποιήστε `AsposeAI(language="de")` για γερμανικά, `"es"` για ισπανικά κ.ά.

**Ε: Τι γίνεται αν η μηχανή OCR δεν ανιχνεύει σωστά τις δομές πινάκων;**  
Α: Ενεργοποιήστε την ανάλυση διάταξης με `ocr_engine.set_layout_analysis(True)`. Αυτό βελτιώνει την ανίχνευση πινάκων με μικρό επιπλέον κόστος επεξεργασίας.

**Ε: Πώς μπορώ να διαχειριστώ πολύ μεγάλες παρτίδες αποδοτικά;**  
Α: Επεξεργαστείτε τις εικόνες σε τμήματα, γράψτε κάθε αποτέλεσμα σε βάση δεδομένων ή σε μήνυμα ουράς, και εξετάστε τη χρήση async I/O ή multiprocessing για μέγιστη αξιοποίηση του CPU.

**Ε: Υπάρχει τρόπος να προσαρμόσω το λεξικό του spell‑check;**  
Α: Ναι. Χρησιμοποιήστε `ai_processor.set_custom_dictionary(["Invoice", "VAT", "Subtotal"])` πριν τρέξετε τον post‑processor.

---

![Extract text from image example](extract_text_image.png "Extract text from image with Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}

---

**Τελευταία ενημέρωση:** 2026-02-27  
**Δοκιμάστηκε με:** Aspose OCR 23.12, Aspose OCR AI 23.12  
**Συγγραφέας:** Aspose