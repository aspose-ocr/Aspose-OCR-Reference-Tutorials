---
category: general
date: 2025-12-27
description: Εξάγετε κείμενο από εικόνα χρησιμοποιώντας το Aspose OCR και διορθώστε
  τα σφάλματα OCR. Μάθετε πώς να φορτώνετε εικόνα για OCR και να διορθώνετε τα λάθη
  γρήγορα.
draft: false
keywords:
- extract text from image
- load image for ocr
- how to correct ocr errors
- Aspose OCR Python
- OCR post‑processing
language: el
og_description: Εξάγετε κείμενο από εικόνα με το Aspose OCR και διορθώστε αμέσως τα
  σφάλματα OCR. Ακολουθήστε αυτό το σεμινάριο για να φορτώσετε εικόνα για OCR και
  να καθαρίσετε τα αποτελέσματα.
og_title: Εξαγωγή κειμένου από εικόνα με το Aspose OCR – Πλήρης οδηγός
tags:
- OCR
- Python
- Aspose
- Text Extraction
title: Εξαγωγή κειμένου από εικόνα με το Aspose OCR – Οδηγός βήμα‑προς‑βήμα
url: /el/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Βήμα‑Βήμα

Έχετε ποτέ χρειαστεί να **εξάγετε κείμενο από εικόνα** αλλά μπλέξατε με ακατάστατο αποτέλεσμα OCR; Δεν είστε μόνοι. Σε πολλά έργα αυτοματοποίησης—σκεφτείτε την επεξεργασία τιμολογίων, τη σάρωση αποδείξεων ή την ψηφιοποίηση παλιών εγγράφων—το πρώτο εμπόδιο είναι η λήψη καθαρού, αναζητήσιμου κειμένου από μια εικόνα.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει πώς να **load image for OCR**, να εκτελέσετε την αναγνώριση και στη συνέχεια να **correct OCR errors** χρησιμοποιώντας το AI‑powered spell‑check post‑processor της Aspose. Στο τέλος θα έχετε ένα ενιαίο script που μετατρέπει ένα PNG τιμολογίου σε επεξεργασμένο, αναζητήσιμο κείμενο, έτοιμο για οποιαδήποτε επόμενη ροή εργασίας έχετε κατά νου.

## Τι Θα Μάθετε

- Πώς να εγκαταστήσετε και να εισάγετε τις βιβλιοθήκες Aspose OCR και AI σε Python.  
- Ο ακριβής κώδικας που απαιτείται για **load image for OCR** (χωρίς εικασίες).  
- Πώς να εκτελέσετε τη μηχανή OCR και να καταγράψετε το ακατέργαστο string.  
- Γιατί το OCR συχνά παράγει τυπογραφικά λάθη και πώς ο ενσωματωμένος spell‑check processor μπορεί να **correct OCR errors** αυτόματα.  
- Συμβουλές για τη διαχείριση edge cases όπως PDF πολλαπλών σελίδων ή σάρωση χαμηλής ανάλυσης.  

> **Προαπαιτούμενα:** Python 3.8+, έγκυρη άδεια Aspose OCR (ή δωρεάν δοκιμή) και αρχείο εικόνας (π.χ., `invoice.png`) που θέλετε να επεξεργαστείτε.

## Εξαγωγή Κειμένου από Εικόνα – Ρύθμιση Aspose OCR

Πριν μπορέσουμε να κάνουμε οτιδήποτε, χρειαζόμαστε τα σωστά πακέτα. Η Aspose διανέμει τη μηχανή OCR της ως pip‑installable module.

```bash
pip install aspose-ocr
```

Αν θέλετε επίσης το AI post‑processor, εγκαταστήστε το συνοδευτικό πακέτο:

```bash
pip install aspose-ocr-ai
```

> **Συμβουλή επαγγελματία:** Κρατήστε τα πακέτα σας ενημερωμένα. Κατά τη στιγμή της συγγραφής, οι τελευταίες εκδόσεις είναι `aspose-ocr 23.12` και `aspose-ocr-ai 23.12`.

Μόλις οι βιβλιοθήκες είναι στο σύστημά σας, εισάγετε τις κλάσεις που θα χρησιμοποιήσετε:

```python
# Step 1: Import the OCR and AI classes
from aspose.ocr import OcrEngine, AsposeAI
```

> **Γιατί είναι σημαντικό:** Η εισαγωγή των συγκεκριμένων κλάσεων διατηρεί το namespace καθαρό και καθιστά προφανές ποια στοιχεία είναι υπεύθυνα για την αναγνώριση σε σύγκριση με το post‑processing.

## Φόρτωση Εικόνας για OCR – Προετοιμασία του PNG Τιμολογίου σας

Το επόμενο λογικό βήμα είναι να δείξετε στη μηχανή το αρχείο που θέλετε να διαβάσετε. Εδώ η λέξη-κλειδί **load image for OCR** ξεχωρίζει.

```python
# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()

# Step 3: Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")
```

> **Επεξήγηση:** `OcrEngine()` δημιουργεί μια νέα μηχανή με προεπιλεγμένες ρυθμίσεις (γλώσσα Αγγλικά, αυτόματη περιστροφή κ.λπ.). Η μέθοδος `load_image()` δέχεται διαδρομή αρχείου, ροή ή ακόμη και byte array—ώστε να μπορείτε να τροφοδοτείτε εικόνες από δίσκο, το web ή μια ενδιάμεση μνήμη.

### Συνηθισμένα Προβλήματα κατά τη Φόρτωση Εικόνων

| Ζήτημα | Συμπτωμα | Διόρθωση |
|-------|----------|----------|
| Χαμηλό DPI (<300) | Ακατάστατοι χαρακτήρες, λείπουν αριθμοί | Επαναδειγματοληψία της εικόνας σε 300 dpi ή υψηλότερο πριν τη φόρτωση |
| Λανθασμένη λειτουργία χρώματος (CMYK) | Λανθασμένα σχήματα χαρακτήρων | Μετατροπή σε RGB χρησιμοποιώντας Pillow (`Image.convert("RGB")`) |
| PDF πολλαπλών σελίδων | Επεξεργάζεται μόνο η πρώτη σελίδα | Μετατρέψτε κάθε σελίδα σε εικόνα και επαναλάβετε τη διαδικασία |

## Εκτέλεση OCR και Λήψη Ακατέργαστου Κειμένου

Τώρα που η μηχανή γνωρίζει πού βρίσκεται η εικόνα, μπορούμε πραγματικά να τη διαβάσουμε.

```python
# Step 4: Perform OCR to extract raw text
raw_text = ocr_engine.recognize()
print("Raw OCR output:")
print(raw_text)
```

Η κλήση `recognize()` επιστρέφει μια απλή συμβολοσειρά Python. Σε πολλά πραγματικά σενάρια η έξοδος θα περιέχει περιττά κενά, λανθασμένα διαβασμένους χαρακτήρες ή σπασμένες αλλαγές γραμμής—ιδιαίτερα με αποδείξεις που χρησιμοποιούν συμπυκνωμένες γραμματοσειρές.

> **Γιατί καταγράφουμε πρώτα το raw_text:** Σας παρέχει μια βάση σύγκρισης με την καθαρισμένη έκδοση αργότερα, κάτι που είναι χρήσιμο για εντοπισμό σφαλμάτων ή έλεγχο.

## Πώς να Διορθώσετε Σφάλματα OCR – Χρησιμοποιώντας Aspose AI Spell‑Check

Η Aspose παρέχει ένα ελαφρύ AI wrapper που μπορεί να εκτελέσει ένα spell‑check post‑processor στο ακατέργαστο αποτέλεσμα. Αυτό αντιμετωπίζει άμεσα την ερώτηση **how to correct OCR errors**.

```python
# Step 5: Initialise the AI post‑processor and choose a spell‑check processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("spell_check")
```

Μπορείτε να αντικαταστήσετε το `"spell_check"` με άλλους επεξεργαστές όπως το `"grammar_check"` ή το `"named_entity_recognition"` εάν το σενάριό σας το απαιτεί.

```python
# Step 6: Clean the OCR output using the selected post‑processor
clean_text = ai_processor.run_postprocessor(raw_text)

# Step 7: Output the corrected text
print("\nCorrected OCR output:")
print(clean_text)
```

### Τι κάνει το Spell‑Check στο Παρασκήνιο

1. **Tokenisation** – Διαχωρίζει την ακατέργαστη συμβολοσειρά σε λέξεις και σημεία στίξης.  
2. **Dictionary Lookup** – Συγκρίνει κάθε token με ένα αγγλικό λεξικό (ή ένα προσαρμοσμένο που μπορείτε να παρέχετε).  
3. **Contextual Scoring** – Χρησιμοποιεί ένα μικρό μοντέλο γλώσσας για να αποφασίσει αν μια διόρθωση ταιριάζει με τις γύρω λέξεις.  
4. **Replacement** – Επιστρέφει μια νέα συμβολοσειρά με τις πιο πιθανές διορθώσεις εφαρμοσμένες.  

> **Εξαίρεση:** Εάν η γλώσσα προέλευσης δεν είναι Αγγλικά, περάστε τον κατάλληλο κωδικό γλώσσας κατά τη δημιουργία του `AsposeAI()` (π.χ., `AsposeAI(language="fr")`).

## Επαλήθευση και Χρήση του Καθαρισμένου Κειμένου

Σε αυτό το σημείο έχετε δύο μεταβλητές: `raw_text` (η άμεση εξαγωγή OCR) και `clean_text` (η έκδοση με spell‑check). Η επιλογή εξαρτάται από τις ανάγκες του επόμενου βήματος.

```python
# Example: Save the cleaned text to a .txt file for later indexing
with open("invoice_extracted.txt", "w", encoding="utf-8") as f:
    f.write(clean_text)

print("\n✅ Cleaned text saved to invoice_extracted.txt")
```

Αν τροφοδοτείτε το αποτέλεσμα σε μηχανή αναζήτησης, βάση δεδομένων ή μοντέλο machine‑learning, προτιμήστε πάντα την **cleaned** έκδοση—διαφορετικά θα διαδώσετε τον θόρυβο OCR σε όλη τη διαδικασία.

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω είναι το πλήρες script που μπορείτε να αντιγράψετε σε ένα αρχείο με όνομα `extract_invoice.py`. Υποθέτει ότι έχετε ήδη εγκαταστήσει τα δύο πακέτα Aspose και έχετε μια εικόνα στο `YOUR_DIRECTORY/invoice.png`.

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

Θα πρέπει να δείτε το ακατέργαστο dump ακολουθούμενο από μια πιο καθαρή έκδοση, και ένα αρχείο με όνομα `invoice_extracted.txt` θα εμφανιστεί στον ίδιο φάκελο.

## Συχνές Ερωτήσεις (FAQ)

**Q: Λειτουργεί αυτό με PDFs;**  
A: Όχι άμεσα. Μετατρέψτε κάθε σελίδα PDF σε εικόνα (π.χ., χρησιμοποιώντας `pdf2image`) και επαναλάβετε το script για τα παραγόμενα PNG.

**Q: Η γλώσσα μου δεν είναι Αγγλικά—μπορώ ακόμα να χρησιμοποιήσω το spell‑check;**  
A: Ναι. Περάστε τον επιθυμητό κωδικό γλώσσας στο `AsposeAI(language="de")` για Γερμανικά, `"es"` για Ισπανικά κ.λπ.

**Q: Τι γίνεται αν η μηχανή OCR εντοπίσει λανθασμένα τη διάταξη ενός πίνακα;**  
A: Η Aspose OCR προσφέρει τη σημαία `set_layout_analysis(True)`. Η ενεργοποίησή της βελτιώνει την ανίχνευση πινάκων αλλά μπορεί να αυξήσει τον χρόνο επεξεργασίας.

**Q: Πώς να διαχειριστώ εξαιρετικά μεγάλες παρτίδες;**  
A: Τυλίξτε τη βασική λογική σε μια συνάρτηση και χρησιμοποιήστε thread pool ή async IO για παράλληλη εκτέλεση σε πολλούς πυρήνες ή μηχανές.

## Συμπεράσματα

Σας δείξαμε πώς να **extract text from image** χρησιμοποιώντας Aspose OCR, πώς να **load image for OCR**, και τον πιο απλό τρόπο να **correct OCR errors** με το ενσωματωμένο AI spell‑check. Το πλήρες, εκτελέσιμο script παρουσιάζει τη ροή από την αρχή μέχρι το τέλος—από τη φόρτωση του PNG του τιμολογίου μέχρι την αποθήκευση ενός καθαρού, αναζητήσιμου αρχείου `.txt`.

Μη διστάσετε να πειραματιστείτε: αντικαταστήστε το spell‑check με διόρθωση γραμματικής, τροφοδοτήστε το αποτέλεσμα σε έναν ταξινομητή NLP, ή ενσωματώστε τη διαδικασία σε ένα μεγαλύτερο σύστημα διαχείρισης εγγράφων. Οι δυνατότητες είναι απεριόριστες μόλις έχετε αξιόπιστο, διορθωμένο κείμενο.

Έχετε περισσότερες ερωτήσεις σχετικά με OCR, Aspose ή αυτοματοποίηση με Python; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

![Παράδειγμα εξαγωγής κειμένου από εικόνα](extract_text_image.png "Εξαγωγή κειμένου από εικόνα με Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}