---
category: general
date: 2026-06-19
description: Πώς να εκτελέσετε OCR σε αποδείξεις και να τρέξετε έναν ελεγκτή ορθογραφίας
  για καθαρή εξαγωγή κειμένου. Ακολουθήστε αυτόν τον βήμα‑βήμα οδηγό Python.
draft: false
keywords:
- how to perform ocr
- extract text from receipt
- run spell checker
- perform ocr on image
- load image for ocr
language: el
og_description: Πώς να εκτελέσετε OCR σε αποδείξεις και άμεσα να τρέξετε έναν ορθογραφικό
  έλεγχο. Μάθετε τη πλήρη ροή εργασίας σε Python με το Aspose AI.
og_title: Πώς να εκτελέσετε OCR σε αποδείξεις – Πλήρης οδηγός ελέγχου ορθογραφίας
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to perform OCR on receipts and run a spell checker for clean text
    extraction. Follow this step‑by‑step Python tutorial.
  headline: How to Perform OCR on Receipts – Spell Checker Guide
  type: TechArticle
- description: How to perform OCR on receipts and run a spell checker for clean text
    extraction. Follow this step‑by‑step Python tutorial.
  name: How to Perform OCR on Receipts – Spell Checker Guide
  steps:
  - name: '**Load the image** → the OCR engine knows *what* to read.'
    text: '**Load the image** → the OCR engine knows *what* to read.'
  - name: '**Perform OCR** → the engine spits out raw characters.'
    text: '**Perform OCR** → the engine spits out raw characters.'
  - name: '**Extract the text** → we pull the string out of the engine’s result object.'
    text: '**Extract the text** → we pull the string out of the engine’s result object.'
  - name: '**Run spell checker** → a smart post‑processor cleans up typos and OCR
      quirks.'
    text: '**Run spell checker** → a smart post‑processor cleans up typos and OCR
      quirks.'
  - name: '**Use the corrected text** → print, store, or pass it to another service.'
    text: '**Use the corrected text** → print, store, or pass it to another service.'
  type: HowTo
tags:
- OCR
- Python
- Aspose AI
- Text Extraction
title: Πώς να εκτελέσετε OCR σε αποδείξεις – Οδηγός ελέγχου ορθογραφίας
url: /el/python/general/how-to-perform-ocr-on-receipts-spell-checker-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εκτελέσετε OCR σε Αποδείξεις – Οδηγός Ελέγχου Ορθογραφίας

Έχετε αναρωτηθεί ποτέ **πώς να εκτελέσετε OCR** σε μια απόδειξη χωρίς να τσακίζετε τα μαλλιά σας; Δεν είστε ο μόνος. Σε πολλές πραγματικές εφαρμογές—εφαρμογές παρακολούθησης εξόδων, λογιστικά εργαλεία ή ακόμη και ένας απλός σαρωτής λίστας αγορών—πρέπει να **εξάγετε κείμενο από απόδειξη** εικόνες και να διασφαλίσετε ότι το κείμενο είναι αναγνώσιμο. Τα καλά νέα; Με λίγες γραμμές Python και Aspose AI μπορείτε να αποκτήσετε μια καθαρή, ορθογραφικά ελεγμένη συμβολοσειρά σε δευτερόλεπτα.

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία: φόρτωση της εικόνας της απόδειξης, εκτέλεση OCR και στη συνέχεια βελτίωση του αποτελέσματος με έναν post‑processor ελέγχου ορθογραφίας. Στο τέλος θα έχετε μια έτοιμη‑για‑χρήση συνάρτηση που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο χρειάζεται αξιόπιστη ψηφιοποίηση αποδείξεων.

## Τι Θα Μάθετε

- Πώς να **φορτώσετε εικόνα για OCR** χρησιμοποιώντας το OcrEngine της Aspose.
- Τα ακριβή βήματα για **εκτέλεση OCR σε εικόνα** αρχεία σε Python.
- Τρόπους **εξαγωγής κειμένου από απόδειξη** και γιατί ένας post‑processor είναι σημαντικός.
- Πώς να **εκτελέσετε έλεγχο ορθογραφίας** στο ακατέργαστο αποτέλεσμα OCR για διόρθωση κοινών λαθών.
- Συμβουλές για διαχείριση ακραίων περιπτώσεων όπως σάρωση χαμηλής αντίθεσης ή αποδείξεις πολλαπλών σελίδων.

### Προαπαιτούμενα

- Python 3.8 ή νεότερη έκδοση εγκατεστημένη στο σύστημά σας.
- Ένα ενεργό άδεια Aspose.OCR (η δωρεάν δοκιμή λειτουργεί για δοκιμές).
- Βασική εξοικείωση με συναρτήσεις Python και διαχείριση εξαιρέσεων.

Αν έχετε όλα αυτά, ας ξεκινήσουμε—χωρίς περιττές πληροφορίες, μόνο μια λειτουργική λύση που μπορείτε να αντιγράψετε‑και‑επικολλήσετε.

![διάγραμμα παραδείγματος εκτέλεσης OCR](ocr_flow.png)

## Πώς να Εκτελέσετε OCR σε Αποδείξεις – Επισκόπηση

Πριν αρχίσουμε τον κώδικα, φανταστείτε τη ροή ως μια απλή γραμμή συναρμολόγησης:

1. **Φορτώστε την εικόνα** → η μηχανή OCR ξέρει *τι* να διαβάσει.  
2. **Εκτελέστε OCR** → η μηχανή εκτυπώνει ακατέργαστους χαρακτήρες.  
3. **Εξάγετε το κείμενο** → παίρνουμε τη συμβολοσειρά από το αντικείμενο αποτελέσματος της μηχανής.  
4. **Εκτελέστε έλεγχο ορθογραφίας** → ένας έξυπνος post‑processor καθαρίζει τυπογραφικά λάθη και ιδιαιτερότητες OCR.  
5. **Χρησιμοποιήστε το διορθωμένο κείμενο** → εκτυπώστε, αποθηκεύστε ή περάστε το σε άλλη υπηρεσία.

Αυτό είναι όλο. Κάθε στάδιο είναι μια μόνο, καλά ονομασμένη γραμμή κώδικα, αλλά οι επεξηγήσεις γύρω από αυτό θα σας κρατήσουν από το να χαθείτε όταν κάτι πάει στραβά.

## Βήμα 1 – Φόρτωση Εικόνας για OCR

Το πρώτο πράγμα που πρέπει να κάνετε είναι να δείξετε στη μηχανή OCR το σωστό αρχείο. Το `OcrEngine` της Aspose περιμένει μια διαδρομή, οπότε βεβαιωθείτε ότι η εικόνα της απόδειξης βρίσκεται κάπου που το script μπορεί να την διαβάσει.

```python
# Import the necessary Aspose OCR classes
from aspose.ocr import OcrEngine

def load_image(image_path: str) -> OcrEngine:
    """
    Initializes an OcrEngine instance and loads the image.
    Returns the configured engine ready for recognition.
    """
    engine = OcrEngine()
    try:
        # This is the 'load image for ocr' step
        engine.set_image_from_file(image_path)
        return engine
    except Exception as e:
        # Provide a clear error if the file can't be opened
        raise FileNotFoundError(f"Unable to load image at {image_path}: {e}")
```

**Γιατί είναι σημαντικό:**  
Αν η διαδρομή της εικόνας είναι λανθασμένη, ολόκληρη η αλυσίδα καταρρέει. Τυλίγοντας τη φόρτωση σε ένα `try/except`, λαμβάνετε ένα χρήσιμο μήνυμα αντί για ένα ακατανόητο stack trace. Επίσης, σημειώστε το όνομα μεθόδου `set_image_from_file`—αυτή είναι η ακριβής κλήση που χρησιμοποιεί η Aspose για **φόρτωση εικόνας για OCR**.

## Βήμα 2 – Εκτέλεση OCR στην Εικόνα

Τώρα που η μηχανή ξέρει ποιο αρχείο να διαβάσει, της ζητάμε να αναγνωρίσει τους χαρακτήρες. Αυτό το βήμα είναι όπου γίνεται η βαριά δουλειά.

```python
def perform_ocr(engine: OcrEngine):
    """
    Executes OCR on the previously loaded image.
    Returns the raw recognition result object.
    """
    # This line actually runs the OCR algorithm
    raw_result = engine.recognize()
    return raw_result
```

**Πίσω από τη σκηνή:**  
Η `recognize()` σαρώνει το bitmap, εφαρμόζει τμηματοποίηση και στη συνέχεια τρέχει έναν αναγνώστη βασισμένο σε νευρωνικό δίκτυο. Το αποτέλεσμα περιέχει περισσότερα από απλό κείμενο—περιλαμβάνει βαθμολογίες εμπιστοσύνης, περιοριστικά πλαίσια και πληροφορίες γλώσσας. Για τις περισσότερες περιπτώσεις σάρωσης αποδείξεων, θα χρειαστείτε μόνο την ιδιότητα `text` αργότερα.

## Βήμα 3 – Εξαγωγή Κειμένου από την Απόδειξη

Το ακατέργαστο αποτέλεσμα είναι ένα πλούσιο αντικείμενο, αλλά μας ενδιαφέρει μόνο η ανθρώπινα αναγνώσιμη συμβολοσειρά. Αυτό είναι το σημείο όπου **εξάγουμε κείμενο από απόδειξη**.

```python
def get_raw_text(raw_result) -> str:
    """
    Pulls the plain text out of the OCR result.
    """
    # The Text attribute holds the recognized characters
    return raw_result.text
```

**Συνηθισμένα προβλήματα:**  
Μερικές φορές οι αποδείξεις περιέχουν πολύ μικρές γραμματοσειρές ή αχνή εκτύπωση, προκαλώντας τη μηχανή OCR να επιστρέψει κενές συμβολοσειρές ή παραμορφωμένα σύμβολα. Αν παρατηρήσετε πολλούς χαρακτήρες `�`, σκεφτείτε προεπεξεργασία της εικόνας (αύξηση αντίθεσης, ευθυγράμμιση κ.λπ.) πριν τη φόρτωση.

## Βήμα 4 – Εκτέλεση Ελέγχου Ορθογραφίας

Το OCR δεν είναι τέλειο—ειδικά σε αποδείξεις χαμηλής ανάλυσης. Η Aspose AI προσφέρει έναν post‑processor που λειτουργεί σαν έλεγχο ορθογραφίας, διορθώνοντας τυπικά σφάλματα OCR όπως “0” αντί για “O” ή “l” αντί για “1”.

```python
from aspose.ai import AsposeAI

def spell_check(raw_text: str) -> str:
    """
    Sends the raw OCR text through Aspose AI's spell‑checking post‑processor.
    Returns the corrected string.
    """
    # Initialize the AI helper
    spellchecker = AsposeAI()
    try:
        # The 'run_postprocessor' method expects the raw OCR result object,
        # but we can also feed just the text if the API allows.
        corrected = spellchecker.run_postprocessor(raw_text)
        return corrected.text
    finally:
        # Always free resources to avoid memory leaks
        spellchecker.free_resources()
```

**Γιατί το χρειάζεστε:**  
Ακόμη και ένα OCR με 95 % ακρίβεια μπορεί να παράγει λίγες λανθασμένες λέξεις που διακόπτουν την επεξεργασία downstream (π.χ., εξαγωγή ημερομηνίας). Ο ελεγκτής ορθογραφίας μαθαίνει από μοντέλα γλώσσας και διορθώνει αυτά τα σφάλματα αυτόματα. Στην πράξη, θα δείτε μια εμφανή βελτίωση από “Total: $1O.00” σε “Total: $10.00”.

## Βήμα 5 – Χρήση του Διορθωμένου Κειμένου

Σε αυτό το στάδιο έχετε μια καθαρή συμβολοσειρά έτοιμη για ό,τι χρειάζεστε—εκτύπωση στην κονσόλα, αποθήκευση σε βάση δεδομένων ή τροφοδότηση σε parser φυσικής γλώσσας.

```python
def main(image_path: str):
    # Load the image
    engine = load_image(image_path)

    # Perform OCR
    raw_result = perform_ocr(engine)

    # Extract raw text
    raw_text = get_raw_text(raw_result)

    # Run spell checker
    corrected_text = spell_check(raw_text)

    # Release OCR resources
    engine.dispose()

    # Show the final, cleaned‑up receipt text
    print("=== Corrected Receipt Text ===")
    print(corrected_text)

# Example usage
if __name__ == "__main__":
    main("YOUR_DIRECTORY/receipt.png")
```

**Αναμενόμενη έξοδος** (υποθέτοντας μια τυπική απόδειξη παντοπωλείου):

```
=== Corrected Receipt Text ===
Walmart Supercenter
Date: 06/15/2026   Time: 14:32
Item          Qty   Price
Milk          2     $3.20
Bread         1     $2.50
Eggs          1     $2.99
Subtotal               $8.69
Tax                    $0.69
Total                 $9.38
Thank you for shopping!
```

Παρατηρήστε πώς οι αριθμοί εμφανίζονται σωστά και η λέξη “Thank” δεν διαβάζεται λανθασμένα ως “Thankk”.

## Διαχείριση Ακραίων Περιπτώσεων & Συμβουλές

- **Σάρωση χαμηλής αντίθεσης:** Προεπεξεργαστείτε την εικόνα με Pillow (`ImageEnhance.Contrast`) πριν τη φόρτωση.  
- **Αποδείξεις πολλαπλών σελίδων:** Επαναλάβετε τη διαδικασία για κάθε αρχείο σελίδας και συνενώστε τα αποτελέσματα.  
- **Διαφορετικές γλώσσες:** Ορίστε `engine.language = "eng"` ή άλλο κωδικό ISO αν δουλεύετε με μη‑Αγγλικές αποδείξεις.  
- **Καθαρισμός πόρων:** Πάντα καλέστε `engine.dispose()` και `spellchecker.free_resources()`· η παράλειψη μπορεί να προκαλέσει διαρροή μνήμης σε υπηρεσίες που τρέχουν πολύ χρόνο.  
- **Επεξεργασία σε παρτίδες:** Τυλίξτε τη λογική `main` σε μια ουρά εργασιών (Celery, RQ) για σενάρια υψηλής απόδοσης.

## Συμπέρασμα

Απαντήσαμε πώς να **εκτελέσετε OCR** σε αποδείξεις και αβίαστα **να εκτελέσετε έλεγχο ορθογραφίας** για να λάβετε καθαρό, αναζητήσιμο κείμενο. Από τη φόρτωση της εικόνας, την εκτέλεση OCR στην εικόνα, την εξαγωγή κειμένου από την απόδειξη, μέχρι την εκτέλεση του post‑processor ελέγχου ορθογραφίας—κάθε βήμα είναι σύντομο, καλά τεκμηριωμένο και έτοιμο για παραγωγική χρήση.

Αν θέλετε να **εξάγετε κείμενο από απόδειξη** σε κλίμακα, σκεφτείτε την προσθήκη παράλληλης επεξεργασίας και caching των αποτελεσμάτων OCR. Θέλετε να εξερευνήσετε περισσότερο; Δοκιμάστε ενσωμάτωση ενός PDF parser για χειρισμό σαρωμένων PDF, ή πειραματιστείτε με την ανάλυση διάταξης της Aspose για αυτόματη σύλληψη δεδομένων σε στήλες.

Καλό coding, και εύχομαι οι αποδείξεις σας να είναι πάντα αναγνώσιμες!

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Βήμα‑βήμα](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Πώς να Χρησιμοποιήσετε AspOCR: Φίλτρα Προεπεξεργασίας Εικόνας OCR για .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}