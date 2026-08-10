---
category: general
date: 2026-04-26
description: Καλύψτε γρήγορα τους αριθμούς πιστωτικών καρτών χρησιμοποιώντας την επεξεργασία
  μετά‑από‑OCR του AsposeAI. Μάθετε για τη συμμόρφωση PCI, τη μάσκα με κανονικές εκφράσεις
  και τον καθαρισμό δεδομένων σε έναν βήμα‑βήμα οδηγό.
draft: false
keywords:
- mask credit card numbers
- PCI compliance
- OCR post‑processing
- AsposeAI
- regular expression masking
- data sanitization
language: el
og_description: Απόκρυψη αριθμών πιστωτικών καρτών στα αποτελέσματα OCR με το AsposeAI.
  Αυτό το σεμινάριο καλύπτει τη συμμόρφωση με το PCI, την απόκρυψη με κανονικές εκφράσεις
  και την απολύμανση δεδομένων.
og_title: Απόκρυψη αριθμών πιστωτικών καρτών – Πλήρης οδηγός επεξεργασίας μετά την
  OCR με Python
tags:
- OCR
- Python
- security
title: Απόκρυψη αριθμών πιστωτικών καρτών στην έξοδο OCR – Πλήρης οδηγός Python
url: /el/python/general/mask-credit-card-numbers-in-ocr-output-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Απόκρυψη Αριθμών Πιστωτικών Καρτών – Πλήρης Οδηγός Python

Έχετε ποτέ χρειαστεί να **αποκρύψετε αριθμούς πιστωτικών καρτών** σε κείμενο που προέρχεται απευθείας από μια μηχανή OCR; Δεν είστε μόνοι. Σε ρυθμιζόμενους κλάδους, η αποκάλυψη ενός πλήρους PAN (Primary Account Number) μπορεί να σας βάλει σε πρόβλημα με τους ελεγκτές συμμόρφωσης PCI. Τα καλά νέα; Με λίγες γραμμές Python και το hook post‑processing του AsposeAI, μπορείτε αυτόματα να κρύψετε τα μεσαία οκτώ ψηφία και να παραμείνετε ασφαλείς.

Σε αυτό το tutorial θα περάσουμε από ένα πραγματικό σενάριο: εκτέλεση OCR σε εικόνα απόδειξης, έπειτα εφαρμογή μιας προσαρμοσμένης λειτουργίας **OCR post‑processing** που εξαλείφει τυχόν δεδομένα PCI. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο snippet που μπορείτε να ενσωματώσετε σε οποιαδήποτε ροή εργασίας AsposeAI, καθώς και μια σειρά πρακτικών συμβουλών για τη διαχείριση edge cases και την κλιμάκωση της λύσης.

## Τι Θα Μάθετε

- Πώς να καταχωρίσετε έναν προσαρμοσμένο post‑processor με **AsposeAI**.  
- Γιατί η προσέγγιση **regular expression masking** είναι γρήγορη και αξιόπιστη.  
- Τα βασικά της **PCI compliance** που σχετίζονται με την εξάλειψη δεδομένων.  
- Τρόποι επέκτασης του μοτίβου για πολλαπλές μορφές καρτών ή διεθνείς αριθμούς.  
- Αναμενόμενο αποτέλεσμα και πώς να επαληθεύσετε ότι η απόκρυψη λειτούργησε.

> **Prerequisites** – Θα πρέπει να έχετε ένα λειτουργικό περιβάλλον Python 3, το πακέτο Aspose.AI for OCR εγκατεστημένο (`pip install aspose-ocr`), και ένα δείγμα εικόνας (π.χ., `receipt.png`) που περιέχει αριθμό πιστωτικής κάρτας. Δεν απαιτούνται άλλες εξωτερικές υπηρεσίες.

---

## Step 1: Define a Post‑Processor that Masks Credit Card Numbers

Η καρδιά της λύσης βρίσκεται σε μια μικρή συνάρτηση που λαμβάνει το αποτέλεσμα του OCR, εκτελεί μια ρουτίνα **regular expression masking**, και επιστρέφει το εξαγορευμένο κείμενο.

```python
def mask_pci(data, settings):
    """
    Replace the middle 8 digits of any 16‑digit card number with asterisks.
    Keeps the first and last four digits visible for reference.
    """
    import re
    # Pattern captures groups: first 4 digits, middle 8, last 4
    pattern = r'(\d{4})\d{8}(\d{4})'
    # Replace middle portion with ****
    return re.sub(pattern, r'\1****\2', data.text)
```

**Why this works:**  
- Η κανονική έκφραση `(\d{4})\d{8}(\d{4})` ταιριάζει ακριβώς με 16 διαδοχικά ψηφία, τη συνήθη μορφή για Visa, MasterCard και πολλές άλλες.  
- Καταγράφοντας τα πρώτα και τα τελευταία τέσσερα ψηφία (`\1` και `\2`) διατηρούμε αρκετές πληροφορίες για debugging, ενώ συμμορφωνόμαστε με τους κανόνες **PCI compliance** που απαγορεύουν την αποθήκευση του πλήρους PAN.  
- Η αντικατάσταση `\1****\2` κρύβει τα ευαίσθητα μεσαία οκτώ ψηφία, μετατρέποντας το `1234567812345678` σε `1234****5678`.

> **Pro tip:** Αν χρειάζεται να υποστηρίξετε 15‑ψηφιακούς αριθμούς American Express, προσθέστε ένα δεύτερο μοτίβο όπως `r'(\d{4})\d{6}(\d{5})'` και εκτελέστε και τις δύο αντικαταστάσεις διαδοχικά.

---

## Step 2: Initialise the AsposeAI Engine

Πριν μπορέσουμε να συνδέσουμε τον post‑processor, χρειαζόμαστε μια παρουσία του OCR engine. Το AsposeAI περιλαμβάνει το μοντέλο OCR και ένα απλό API για προσαρμοσμένη επεξεργασία.

```python
from aspose.ocr import AsposeAI

# Initialise the AI engine – it will handle image loading, recognition, and post‑processing
ai = AsposeAI()
```

**Why initialise here?**  
Δημιουργώντας το αντικείμενο `AsposeAI` μία φορά και επαναχρησιμοποιώντας το για πολλές εικόνες μειώνουμε το κόστος. Η μηχανή επίσης αποθηκεύει στην κρυφή μνήμη (cache) τα μοντέλα γλώσσας, κάτι που επιταχύνει τις επόμενες κλήσεις — χρήσιμο όταν σαρώνετε δέσμες αποδείξεων.

---

## Step 3: Register the Custom Masking Function

Το AsposeAI εκθέτει τη μέθοδο `set_post_processor` που σας επιτρέπει να συνδέσετε οποιοδήποτε callable. Περνάμε τη συνάρτηση `mask_pci` μαζί με ένα προαιρετικό λεξικό ρυθμίσεων (αρχικά κενό).

```python
# Register our masking routine; custom_settings can hold flags like "log_masked" if you expand later
ai.set_post_processor(mask_pci, custom_settings={})
```

**What’s happening behind the scenes?**  
Όταν αργότερα καλέσετε `run_postprocessor`, το AsposeAI θα παραδώσει το ακατέργαστο αποτέλεσμα OCR στη `mask_pci`. Η συνάρτηση λαμβάνει ένα ελαφρύ αντικείμενο (`data`) που περιέχει το αναγνωρισμένο κείμενο, και επιστρέφετε μια νέα συμβολοσειρά. Αυτός ο σχεδιασμός διατηρεί το βασικό OCR αμετάβλητο, ενώ σας επιτρέπει να επιβάλετε πολιτικές **data sanitization** σε ένα μόνο σημείο.

---

## Step 4: Run OCR on the Receipt Image

Τώρα που η μηχανή ξέρει πώς να καθαρίζει το αποτέλεσμα, της παρέχουμε μια εικόνα. Για το σκοπό του tutorial υποθέτουμε ότι έχετε ήδη ένα αντικείμενο `engine` ρυθμισμένο με τη σωστή γλώσσα και ανάλυση.

```python
# Assume `engine` is a pre‑configured OCR object (e.g., with language='en')
ocr_engine = engine
raw_result = ocr_engine.recognize_image("receipt.png")
```

**Tip:** Αν δεν έχετε προ‑ρυθμισμένο αντικείμενο, μπορείτε να δημιουργήσετε ένα με:

```python
from aspose.ocr import OcrEngine
ocr_engine = OcrEngine(language='en')
```

Η κλήση `recognize_image` επιστρέφει ένα αντικείμενο του οποίου η ιδιότητα `text` περιέχει τη ακατέργαστη, μη αποκρυπτογραφημένη συμβολοσειρά.

---

## Step 5: Apply the Registered Post‑Processor

Με τα ακατέργαστα δεδομένα OCR στα χέρια, τα παραδίδουμε στην παρουσία AI. Η μηχανή εκτελεί αυτόματα τη συνάρτηση `mask_pci` που καταχωρήσαμε νωρίτερα.

```python
# This triggers the post‑processor and returns a new result object
final_result = ai.run_postprocessor(raw_result)
```

**Why use `run_postprocessor` instead of calling the function manually?**  
Κάνοντας έτσι διατηρείται η ροή εργασίας συνεπής, ειδικά όταν έχετε πολλαπλούς post‑processors (π.χ., spell‑checking, language detection). Το AsposeAI τα τοποθετεί στη σειρά που τα καταχωρίσατε, εξασφαλίζοντας ντετερμινιστικό αποτέλεσμα.

---

## Step 6: Verify the Sanitized Output

Τέλος, ας εκτυπώσουμε το εξαγορευμένο κείμενο και ας επιβεβαιώσουμε ότι τυχόν αριθμοί πιστωτικών καρτών έχουν αποκρυφτεί σωστά.

```python
print(final_result.text)
```

**Expected output** (excerpt):

```
Purchase at Café Latte – Total: $4.75
Card: 1234****5678
Date: 2026-04-25
Thank you!
```

Αν η απόδειξη δεν περιείχε αριθμό κάρτας, το κείμενο παραμένει αμετάβλητο — τίποτα προς απόκρυψη, τίποτα για ανησυχία.

---

## Handling Edge Cases and Common Variations

### Multiple Card Numbers in One Document
Αν μια απόδειξη περιλαμβάνει περισσότερα από ένα PAN (π.χ., κάρτα πιστότητας συν αριθμό πληρωμής), η κανονική έκφραση εκτελείται παγκοσμίως, αποκρύπτοντας αυτόματα όλα τα ταιριάσματα. Δεν απαιτείται επιπλέον κώδικας.

### Non‑Standard Formatting
Μερικές φορές το OCR εισάγει κενά ή παύλες (`1234 5678 1234 5678` ή `1234-5678-1234-5678`). Επεκτείνετε το μοτίβο ώστε να αγνοεί αυτούς τους χαρακτήρες:

```python
pattern = r'(\d{4})[ -]?\d{4}[ -]?\d{4}[ -]?\d{4}'
```

Η προσθήκη `[ -]?` επιτρέπει προαιρετικά κενά ή παύλες μεταξύ των ομάδων ψηφίων.

### International Cards
Για PAN 19‑ψηφίων που χρησιμοποιούνται σε ορισμένες περιοχές, μπορείτε να διευρύνετε το μοτίβο:

```python
pattern = r'(\d{4})\d{11,15}(\d{4})'
```

Απλώς θυμηθείτε ότι η **PCI compliance** εξακολουθεί να απαιτεί την απόκρυψη των μεσαίων ψηφίων, ανεξάρτητα από το μήκος.

### Logging Masked Values (Optional)
Αν χρειάζεστε ίχνη ελέγχου, περάστε μια σημαία μέσω `custom_settings` και προσαρμόστε τη συνάρτηση:

```python
def mask_pci(data, settings):
    import re, logging
    pattern = r'(\d{4})\d{8}(\d{4})'
    def repl(match):
        masked = f"{match.group(1)}****{match.group(2)}"
        if settings.get('log'):
            logging.info(f"Masked PAN: {masked}")
        return masked
    return re.sub(pattern, repl, data.text)
```

Στη συνέχεια καταχωρίστε με:

```python
ai.set_post_processor(mask_pci, custom_settings={'log': True})
```

---

## Full Working Example (Copy‑Paste Ready)

```python
# ------------------------------------------------------------
# Mask Credit Card Numbers in OCR Output – Complete Example
# ------------------------------------------------------------
import re
from aspose.ocr import AsposeAI, OcrEngine

# 1️⃣ Define the post‑processor
def mask_pci(data, settings):
    """
    Hide the middle eight digits of any 16‑digit credit‑card number.
    """
    pattern = r'(\d{4})\d{8}(\d{4})'          # keep first & last 4 digits
    return re.sub(pattern, r'\1****\2', data.text)

# 2️⃣ Initialise the OCR engine and AsposeAI wrapper
ocr_engine = OcrEngine(language='en')       # configure as needed
ai = AsposeAI()

# 3️⃣ Register the masking function
ai.set_post_processor(mask_pci, custom_settings={})

# 4️⃣ Run OCR on a sample receipt
raw_result = ocr_engine.recognize_image("receipt.png")

# 5️⃣ Apply post‑processing (masking)
final_result = ai.run_postprocessor(raw_result)

# 6️⃣ Display sanitized text
print("Sanitized OCR output:")
print(final_result.text)
```

Εκτελώντας αυτό το script σε μια απόδειξη που περιέχει `4111111111111111` θα παραχθεί:

```
Sanitized OCR output:
Purchase at Bookstore – $12.99
Card: 4111****1111
Date: 2026-04-26
```

Αυτή είναι η πλήρης αλυσίδα — από ακατέργαστο OCR μέχρι **data sanitization** — τυλιγμένη σε λίγες καθαρές γραμμές Python.

---

## Conclusion

Σας δείξαμε πώς να **αποκρύψετε αριθμούς πιστωτικών καρτών** σε αποτελέσματα OCR χρησιμοποιώντας το hook post‑processing του AsposeAI, μια σύντομη ρουτίνα regular‑expression, και μια σειρά βέλτιστων πρακτικών για **PCI compliance**. Η λύση είναι πλήρως αυτοσυντηρούμενη, λειτουργεί με οποιαδήποτε εικόνα μπορεί να διαβάσει η μηχανή OCR, και μπορεί να επεκταθεί για πιο σύνθετες μορφές καρτών ή απαιτήσεις καταγραφής.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να συνδυάσετε αυτήν την απόκρυψη με μια διαδικασία **database insertion** που αποθηκεύει μόνο τα τελευταία τέσσερα ψηφία για αναφορά, ή ενσωματώστε έναν **batch processor** που σαρώνει ολόκληρο φάκελο αποδείξεων κατά τη νύχτα. Μπορείτε επίσης να εξερευνήσετε άλλες εργασίες **OCR post‑processing** όπως τυποποίηση διευθύνσεων ή ανίχνευση γλώσσας — κάθε μία ακολουθεί το ίδιο μοτίβο που χρησιμοποιήσαμε εδώ.

Έχετε ερωτήσεις σχετικά με edge cases, απόδοση ή πώς να προσαρμόσετε τον κώδικα για διαφορετική βιβλιοθήκη OCR; Αφήστε ένα σχόλιο παρακάτω και ας συνεχίσουμε τη συζήτηση. Καλό coding και παραμείνετε ασφαλείς!  

![Διάγραμμα που απεικονίζει πώς λειτουργεί η απόκρυψη αριθμών πιστωτικών καρτών σε μια διαδικασία OCR](https://example.com/images/ocr-mask-flow.png "Διάγραμμα της ροής απόκρυψης στην επεξεργασία μετά το OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}