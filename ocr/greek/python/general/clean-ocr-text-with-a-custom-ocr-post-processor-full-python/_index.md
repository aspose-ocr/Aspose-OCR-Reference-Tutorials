---
category: general
date: 2026-06-22
description: Μάθετε πώς να καθαρίζετε κείμενο OCR χρησιμοποιώντας έναν επεξεργαστή
  μετά‑επεξεργασίας OCR σε Python. Κώδικας βήμα‑βήμα, εξηγήσεις και συμβουλές για
  αξιόπιστη δομημένη έξοδο JSON.
draft: false
keywords:
- clean OCR text
- OCR post processor
- Python OCR workflow
- structured JSON OCR
- OCR confidence averaging
language: el
og_description: Καθαρίστε αμέσως το κείμενο OCR προσθέτοντας έναν επεξεργαστή μετά
  την OCR. Αυτός ο οδηγός δείχνει την πλήρη υλοποίηση σε Python, γιατί λειτουργεί
  και πώς να την προσαρμόσετε.
og_title: Καθαρισμός κειμένου OCR με προσαρμοσμένο επεξεργαστή μετά-επεξεργασίας OCR
  – Οδηγός Python
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to clean OCR text using an OCR post processor in Python.
    Step‑by‑step code, explanations, and tips for reliable structured JSON output.
  headline: Clean OCR Text with a Custom OCR Post Processor – Full Python Guide
  type: TechArticle
tags:
- OCR
- Python
- post‑processing
title: Καθαρισμός κειμένου OCR με προσαρμοσμένο μετα-επεξεργαστή OCR – Πλήρης οδηγός
  Python
url: /el/python/general/clean-ocr-text-with-a-custom-ocr-post-processor-full-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Καθαρισμός Κειμένου OCR με Προσαρμοσμένο OCR Post Processor – Πλήρης Οδηγός Python

Έχετε ποτέ χρειαστεί να **καθαρίσετε κείμενο OCR** αλλά η ακατέργαστη έξοδος συνέχιζε να προκαλεί προβλήματα με αλλαγές γραμμής, περιττά κενά και χαρακτήρες χαμηλής εμπιστοσύνης; Δεν είστε ο μόνος. Σε πολλές πραγματικές ροές εργασίας η μηχανή OCR σας παρέχει ένα μπλοκ κειμένου μαζί με ένα σκορ εμπιστοσύνης, και εσείς πρέπει να βρείτε πώς να το μετατρέψετε σε κάτι χρήσιμο.  

Τα καλά νέα; Ένας μικρός **OCR post processor** μπορεί να τακτοποιήσει το αποτέλεσμα, να υπολογίσει μια μέση εμπιστοσύνη και ακόμη να συσκευάσει τα πάντα σε μια κομψή συμβολοσειρά JSON — χωρίς να αγγίξει τη βασική μηχανή. Σε αυτό το tutorial θα χτίσουμε αυτόν τον post‑processor, θα τον καταχωρήσουμε σε μια γενική AI/OCR μηχανή και θα περάσουμε γραμμή‑γραμμή τον κώδικα ώστε να τον ενσωματώσετε στο δικό σας project αύριο.

---

## Τι Καλύπτει Αυτό το Tutorial

- Πώς να δημιουργήσετε έναν **post‑processor καθαρού κειμένου OCR** που ομαλοποιεί τα κενά και αφαιρεί τις αλλαγές γραμμής.  
- Γιατί ο υπολογισμός μιας **μέσης εμπιστοσύνης** είναι χρήσιμος για επαλήθευση σε επόμενα στάδια.  
- Καταχώρηση του επεξεργαστή με μια μηχανή OCR (το μοτίβο `ai.set_post_processor`).  
- Εμφάνιση του δομημένου JSON και αντιμετώπιση κοινών περιπτώσεων άκρων.  

Δεν απαιτούνται εξωτερικές βιβλιοθήκες εκτός από την τυπική βιβλιοθήκη της Python, οπότε μπορείτε να ακολουθήσετε το tutorial σε οποιοδήποτε σύστημα με Python 3.8+.

---

## Προαπαιτούμενα

- Μια λειτουργική μηχανή OCR που εκθέτει ένα αντικείμενο `ocr_result` με `text`, `confidence` (λίστα float) και `bounding_boxes`.  
- Βασική εξοικείωση με συναρτήσεις Python και διαχείριση JSON.  
- Προαιρετικά: Ένα εικονικό περιβάλλον (virtual environment) για να διατηρήσετε τις εξαρτήσεις οργανωμένες.  

Αν δεν είστε σίγουροι αν η μηχανή σας υποστηρίζει προσαρμοσμένους post‑processors, ελέγξτε την τεκμηρίωση για μια μέθοδο `set_post_processor` — οι περισσότερες σύγχρονες AI‑powered OCR SDKs το προσφέρουν.

---

## Βήμα 1: Ορισμός του OCR Post Processor που **Καθαρίζει Κείμενο OCR**

Πρώτα, γράφουμε μια συνάρτηση που λαμβάνει το ακατέργαστο αποτέλεσμα OCR, καθαρίζει το κείμενο, υπολογίζει ένα μέτρο εμπιστοσύνης και επιστρέφει μια συμβολοσειρά JSON. Παρατηρήστε πώς κάθε λειτουργία σχολιάζεται σκόπιμα· αυτά τα σχόλια είναι το “γιατί” που αγαπούν να αναφέρουν οι AI βοηθοί.

```python
import json

def create_structured_json(ocr_result, **kwargs):
    """
    Turn an OCR result into a clean, structured JSON payload.

    Parameters
    ----------
    ocr_result : object
        Must expose .text (raw string), .confidence (list of floats),
        and .bounding_boxes (list of box coordinates).

    Returns
    -------
    str
        JSON string with cleaned text, average confidence, and bounding boxes.
    """
    # 1️⃣ Clean the raw text: replace newlines with spaces and trim excess whitespace.
    clean_text = ocr_result.text.replace("\n", " ").strip()

    # 2️⃣ Compute the average confidence – useful for quality gating.
    # Guard against division by zero if the engine returns an empty list.
    if ocr_result.confidence:
        average_confidence = sum(ocr_result.confidence) / len(ocr_result.confidence)
    else:
        average_confidence = 0.0  # fallback when confidence data is missing

    # 3️⃣ Preserve the original bounding boxes for downstream layout analysis.
    boxes = ocr_result.bounding_boxes

    # 4️⃣ Assemble the dictionary and dump it as a JSON string.
    data = {
        "clean_text": clean_text,
        "average_confidence": average_confidence,
        "boxes": boxes
    }

    # ensure_ascii=False keeps Unicode characters intact (think accented letters, emojis, etc.)
    return json.dumps(data, ensure_ascii=False)
```

**Γιατί λειτουργεί αυτό:**  
- `replace("\n", " ")` μετατρέπει το πολυγραμμικό OCR σε μια ενιαία, αναζητήσιμη συμβολοσειρά — ακριβώς αυτό που σημαίνει “καθαρό κείμενο OCR” στις περισσότερες ροές εργασίας.  
- Η αφαίρεση των αρχικών/τελικών κενών αποτρέπει φανταστικά κενά tokens που θα μπορούσαν να σπάσουν tokenizers αργότερα.  
- Ο υπολογισμός της μέσης εμπιστοσύνης σας δίνει ένα ενιαίο μέτρο ποιότητας· μπορείτε να απορρίψετε αποτελέσματα κάτω από ένα όριο (π.χ. 0.85) πριν τα αποθηκεύσετε σε βάση δεδομένων.  
- Η διατήρηση των bounding boxes αμετάβλητη σημαίνει ότι μπορείτε ακόμη να αποδώσετε την αρχική διάταξη αν χρειαστεί να επισημάνετε περιοχές χαμηλής εμπιστοσύνης.

---

## Βήμα 2: Καταχώρηση του Προσαρμοσμένου **OCR Post Processor** στη Μηχανή Σας

Οι περισσότερες AI‑powered OCR SDKs εκθέτουν μια μέθοδο για να συνδέσετε μια callback επεξεργασίας. Παρακάτω υποθέτουμε ότι ένα αντικείμενο `ai` (η μηχανή) παρέχει `set_post_processor`. Αν η βιβλιοθήκη σας χρησιμοποιεί διαφορετικό όνομα, αντικαταστήστε το αναλόγως.

```python
# Register the post‑processor; the second argument can hold custom settings.
ai.set_post_processor(create_structured_json, custom_settings={})
```

**Συμβουλή:** Περάστε παραμετροποίηση μέσω `custom_settings` αν χρειαστεί ποτέ να εναλλάξετε συμπεριφορές (π.χ. ενεργοποίηση/απενεργοποίηση αφαίρεσης newline). Αυτό κάνει τον επεξεργαστή επαναχρησιμοποιήσιμο σε πολλά projects.

---

## Βήμα 3: Εκτέλεση της Μηχανής OCR – Το Αποτέλεσμα Είναι Τώρα μια Συμβολοσειρά JSON

Με τον post‑processor συνδεδεμένο, η κλήση `engine.recognize()` (ή ό,τι χρησιμοποιεί το SDK σας) θα ενεργοποιήσει αυτόματα τη `create_structured_json`. Η μηχανή επιστρέφει τότε ένα αντικείμενο του οποίου το χαρακτηριστικό `.text` περιέχει ήδη το JSON payload.

```python
# The engine runs OCR, then our post‑processor formats the output.
structured_result = engine.recognize()
```

> **Σημείωση:** Κάποια SDKs μπορεί να επιστρέψουν μια απλή συμβολοσειρά αντί για αντικείμενο με χαρακτηριστικό `.text`. Προσαρμόστε το επόμενο βήμα αναλόγως.

---

## Βήμα 4: Εμφάνιση (ή Αποθήκευση) του Δομημένου JSON

Τέλος, τυπώνουμε το JSON στην κονσόλα. Σε παραγωγικό περιβάλλον πιθανότατα θα το γράψετε σε αρχείο, σε μήνυμα σε ουρά ή σε βάση δεδομένων.

```python
# Show the clean OCR text and additional metadata.
print("Structured JSON:", structured_result.text)
```

**Αναμενόμενη έξοδος στην κονσόλα** (μορφοποιημένη για ευανάγνωστη παρουσίαση):

```json
{
  "clean_text": "The quick brown fox jumps over the lazy dog.",
  "average_confidence": 0.9375,
  "boxes": [
    [0, 0, 120, 30],
    [0, 35, 115, 30],
    ...
  ]
}
```

Αν δείτε περιττούς χαρακτήρες newline ή μια εμπιστοσύνη `0.0`, ελέγξτε ότι η μηχανή OCR σας γεμίζει πραγματικά το `ocr_result.confidence`. Η προφυλακτική δήλωση στον post‑processor θα σας προστατεύσει από `ZeroDivisionError`, αλλά θα θέλετε να καταλάβετε γιατί λείπουν τα δεδομένα εμπιστοσύνης.

---

## Αντιμετώπιση Συνηθισμένων Περιπτώσεων Άκρων

| Κατάσταση | Τι να προσέξετε | Γρήγορη Διόρθωση |
|-----------|-------------------|-----------|
| **Κενό αποτέλεσμα OCR** | `ocr_result.text` είναι `""` και η λίστα `confidence` κενή | Ο επεξεργαστής επιστρέφει ήδη `clean_text` κενό και `average_confidence` = 0.0. Μπορείτε να προσθέσετε μια προηγόντως‑επιστροφή αν προτιμάτε να παραλείψετε τη δημιουργία JSON εντελώς. |
| **Μη‑ASCII χαρακτήρες** | Το Unicode γίνεται escaped (`\u00e9`) | Χρησιμοποιήστε `ensure_ascii=False` (ήδη στον κώδικα) για να διατηρήσετε χαρακτήρες όπως το “é” αναγνώσιμους. |
| **Πολύ μεγάλα έγγραφα** | Το μέγεθος του JSON μπορεί να υπερβεί όρια API | Σκεφτείτε streaming της εξόδου ή εγγραφή σε αρχείο αντί για επιστροφή μιας ενιαίας συμβολοσειράς. |
| **Απουσία bounding boxes** | Κάποιες μηχανές OCR παραλείπουν δεδομένα διάταξης | Ορίστε `boxes` σε `None` ή σε κενή λίστα· οι καταναλωτές downstream θα πρέπει να χειρίζονται την απουσία με χάρη. |

---

## Pro Tips & Best Practices

- **Επεξεργασία σε παρτίδες:** Αν χρειάζεται να OCR-άρετε εκατοντάδες σελίδες, τυλίξτε την κλήση αναγνώρισης σε βρόχο και συλλέξτε κάθε JSON payload σε λίστα. Στη συνέχεια αποθηκεύστε ολόκληρη τη λίστα σε ένα αρχείο για ευκολότερη παρτίδα ανάλυσης.  
- **Κατώφλια εμπιστοσύνης:** Πριν αποθηκεύσετε, ελέγξτε το `average_confidence`. Ένας κανόνας: απορρίψτε ό,τι κάτω από `0.80` για κρίσιμες εργασίες εισαγωγής δεδομένων.  
- **Καταγραφή αντί για εκτύπωση:** Σε παραγωγή, αντικαταστήστε το `print()` με έναν δομημένο logger (`logging.info(...)`) ώστε να μπορείτε να εντοπίσετε ποιες εικόνες παρήγαγαν χαμηλή εμπιστοσύνη.  
- **Δοκιμές:** Γράψτε μια μονάδα ελέγχου (unit test) που τροφοδοτεί ένα mock `ocr_result` με γνωστό κείμενο και τιμές εμπιστοσύνης, και στη συνέχεια ελέγχει ότι η δομή JSON ταιριάζει με τις προσδοκίες.  

---

## Πλήρες Παράδειγμα Λειτουργίας (Όλα τα Βήματα Συνδυασμένα)

Παρακάτω βρίσκεται το πλήρες script που μπορείτε να αντιγράψετε σε ένα αρχείο με όνομα `ocr_cleanup.py`. Φροντίστε να αντικαταστήσετε τα placeholders `engine` και `ai` με τις πραγματικές παρουσίες από το OCR SDK σας.

```python
import json

# ----------------------------------------------------------------------
# Step 1: Define the post‑processor that cleans OCR text and builds JSON.
# ----------------------------------------------------------------------
def create_structured_json(ocr_result, **kwargs):
    """
    Convert raw OCR output into a clean JSON string.
    """
    # Clean the raw text: collapse newlines, trim whitespace.
    clean_text = ocr_result.text.replace("\n", " ").strip()

    # Safely compute average confidence.
    if ocr_result.confidence:
        average_confidence = sum(ocr_result.confidence) / len(ocr_result.confidence)
    else:
        average_confidence = 0.0

    # Keep bounding boxes for layout work.
    boxes = ocr_result.bounding_boxes

    payload = {
        "clean_text": clean_text,
        "average_confidence": average_confidence,
        "boxes": boxes
    }
    return json.dumps(payload, ensure_ascii=False)

# ----------------------------------------------------------------------
# Step 2: Register the post‑processor with the OCR engine.
# ----------------------------------------------------------------------
# Replace `ai` with your actual engine/controller instance.
ai.set_post_processor(create_structured_json, custom_settings={})

# ----------------------------------------------------------------------
# Step 3: Run OCR – the result is automatically transformed.
# ----------------------------------------------------------------------
structured_result = engine.recognize()

# ----------------------------------------------------------------------
# Step 4: Output the structured JSON.
# ----------------------------------------------------------------------
print("Structured JSON:", structured_result.text)
```

Αποθηκεύστε το αρχείο, τρέξτε `python ocr_cleanup.py`, και θα δείτε μια ωραία μορφοποιημένη συμβολοσειρά JSON που περιέχει **καθαρό κείμενο OCR**, έναν μέσο δείκτη εμπιστοσύνης και τα αρχικά bounding boxes.

---

## Συμπέρασμα

Τώρα έχετε έναν πλήρη, έτοιμο για παραγωγή τρόπο να **καθαρίσετε κείμενο OCR** χρησιμοποιώντας έναν προσαρμοσμένο **OCR post processor** στην Python. Η λύση ομαλοποιεί τα κενά, προστατεύει από ελλιπή δεδομένα εμπιστοσύνης και επιστρέφει ένα αυτοπεριγραφικό JSON payload που οι επόμενες υπηρεσίες μπορούν να καταναλώσουν χωρίς επιπλέον parsing.  

Από εδώ μπορείτε:

- Να επεκτείνετε τον επεξεργαστή ώστε να **φιλτράρει λέξεις χαμηλής εμπιστοσύνης** πριν δημιουργηθεί το `clean_text`.  
- Να προσθέσετε **ανίχνευση γλώσσας** για να δρομολογήσετε το JSON σε pipelines ανά τοπική γλώσσα.  
- Να συνδυάσετε αυτόν τον post‑processor με **βιβλιοθήκες ορθογραφικού ελέγχου** για ένα επιπλέον επίπεδο ποιότητας.  

Νιώστε ελεύθεροι να τροποποιήσετε τον κώδικα, να πειραματιστείτε με διαφορετικά όρια εμπιστοσύνης ή να μοιραστείτε τις δικές σας βελτιώσεις στα σχόλια. Καλό coding!

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικούς τομείς που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας projects.

- [Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Βήμα‑Βήμα](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Πώς να Εκτελέσετε OCR Κειμένου Εικόνας με Γλώσσα Χρησιμοποιώντας Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Πώς να Αναγνωρίσετε Ορθογώνια Σελίδας για OCR Αναγνώριση Κειμένου σε Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}