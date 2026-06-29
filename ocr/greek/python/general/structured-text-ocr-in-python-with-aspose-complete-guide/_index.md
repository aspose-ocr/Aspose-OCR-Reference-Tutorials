---
category: general
date: 2026-06-28
description: Εκπαιδευτικό σεμινάριο OCR δομημένου κειμένου που δείχνει πώς να κάνετε
  OCR σε εικόνα, να φορτώσετε OCR εικόνας, να εκτελέσετε επεξεργασία μετά το OCR και
  να χρησιμοποιήσετε το Aspose OCR Python για ακριβή αποτελέσματα.
draft: false
keywords:
- structured text ocr
- how to ocr image
- ocr post processing
- aspose ocr python
- load image ocr
language: el
og_description: OCR δομημένου κειμένου με Aspose OCR Python. Μάθετε πώς να κάνετε
  OCR εικόνας, να φορτώνετε εικόνα για OCR και να εφαρμόζετε επεξεργασία μετά το OCR
  σε έναν οδηγό βήμα‑βήμα.
og_title: OCR δομημένου κειμένου σε Python – Πλήρες σεμινάριο Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Structured text OCR tutorial showing how to OCR image, load image OCR,
    perform OCR post processing, and use Aspose OCR Python for accurate results.
  headline: Structured Text OCR in Python with Aspose – Complete Guide
  type: TechArticle
- description: Structured text OCR tutorial showing how to OCR image, load image OCR,
    perform OCR post processing, and use Aspose OCR Python for accurate results.
  name: Structured Text OCR in Python with Aspose – Complete Guide
  steps:
  - name: '**Load image OCR** with auto‑rotate and preprocessing.'
    text: '**Load image OCR** with auto‑rotate and preprocessing.'
  - name: '**Run OCR** while preserving layout (`recognize_structured`).'
    text: '**Run OCR** while preserving layout (`recognize_structured`).'
  - name: '**Apply OCR post processing** via AI spell‑checking.'
    text: '**Apply OCR post processing** via AI spell‑checking.'
  - name: '**Save** the corrected result as JSON (and optionally CSV).'
    text: '**Save** the corrected result as JSON (and optionally CSV).'
  - name: '**Extend** the workflow into NLP or downstream analytics.'
    text: '**Extend** the workflow into NLP or downstream analytics.'
  type: HowTo
tags:
- OCR
- Python
- Aspose
title: OCR δομημένου κειμένου σε Python με το Aspose – Πλήρης οδηγός
url: /el/python/general/structured-text-ocr-in-python-with-aspose-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Δομημένου Κειμένου σε Python – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ πώς να κάνετε **OCR δομημένου κειμένου** σε ένα χειρόγραφο σημείωμα χωρίς να ξοδεύετε ώρες ρυθμίζοντας παραμέτρους; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν εμπόδια όταν προσπαθούν να **φορτώσουν εικόνα OCR** και να διατηρήσουν την αρχική διάταξη. Τα καλά νέα; Το Aspose OCR για Python το κάνει παιχνιδάκι, και μπορείτε ακόμη να προσθέσετε AI‑βασισμένο ορθογραφικό έλεγχο ως καθαρό βήμα **OCR post processing**.

Σε αυτό το tutorial θα περάσουμε από όλο το pipeline—από τη φόρτωση της εικόνας μέχρι τη δημιουργία ενός αρχείου JSON που διατηρεί τις αλλαγές γραμμής και τις στήλες. Στο τέλος, θα έχετε ένα έτοιμο‑για‑εκτέλεση script που δείχνει *ακριβώς* πώς να **OCR εικόνα**, να τρέξετε post‑processing και να εξάγετε καθαρό, δομημένο κείμενο.

---

## Τι Θα Χρειαστείτε

- **Python 3.8+** – οποιαδήποτε πρόσφατη έκδοση λειτουργεί.
- **Aspose.OCR for .NET** (διαθέσιμο σε Python μέσω `pythonnet`). Εγκαταστήστε το με `pip install pythonnet` και προσθέστε τα DLL του Aspose OCR στο έργο σας.
- Ένα δείγμα εικόνας (π.χ., `sample_handwritten.jpg`). Ιδανικά μια σκαναρισμένη σελίδα με σαφείς σειρές και στήλες.
- Προαιρετικά: πρόσβαση στο internet αν θέλετε ο AI ορθογραφικός ελεγκτής να καλέσει τις υπηρεσίες Aspose AI.

> **Pro tip:** Κρατήστε την εικόνα σας κάτω από 2 MB για να επιταχύνετε την προεπεξεργασία· μεγαλύτερα αρχεία μπορεί να κάνουν το βήμα αυτόματης περιστροφής να κολλήσει.

---

## Βήμα 1 – Φόρτωση της Εικόνας και Προετοιμασία για OCR

Το πρώτο πράγμα που κάνετε όταν **φορτώνετε εικόνα OCR** είναι να φέρετε το αρχείο στη μνήμη και να εφαρμόσετε μερικά χρήσιμα βοηθήματα: αυτόματη περιστροφή και μείωση θορύβου. Το Aspose OCR ενσωματώνει αυτά τα βοηθήματα στο `OcrUtil`.

```python
import clr
clr.AddReference("Aspose.OCR")
from Aspose.Ocr import Image, OcrUtil, OcrEngine, AsposeAI, AIProcessor

# Load the image from disk
image_path = "YOUR_DIRECTORY/sample_handwritten.jpg"
image = Image.from_file(image_path)

# Automatic rotation (detects portrait vs. landscape)
image = OcrUtil.auto_rotate(image)

# Pre‑process to improve contrast and remove background speckles
image = OcrUtil.preprocess(image)
```

**Γιατί είναι σημαντικό:**  
Αν η εικόνα είναι πλαγίως, η μηχανή OCR θα διαβάσει κάθε χαρακτήρα ανάποδα. Η κλήση `auto_rotate` σας σώζει από το χειροκίνητο περιστροφή των αρχείων. Το βήμα `preprocess` αυξάνει την ακρίβεια αναγνώρισης, ειδικά σε σκαναρισμένα σημειώματα όπου το φόντο δεν είναι καθαρά λευκό.

---

## Βήμα 2 – Εκτέλεση της Μηχανής OCR και Διατήρηση της Διάταξης

Τώρα που η εικόνα είναι τακτοποιημένη, την παραδίδουμε στην κεντρική μηχανή OCR. Η βασική μέθοδος εδώ είναι `recognize_structured()`, η οποία επιστρέφει ένα `StructuredResult` που διατηρεί σειρές, στήλες και εσοχές—ακριβώς ό,τι χρειάζεστε για **OCR δομημένου κειμένου**.

```python
# Initialise the OCR engine
engine = OcrEngine()
engine.set_image(image)

# Perform OCR while preserving the original layout
raw_result = engine.recognize_structured()
```

**Τι λαμβάνετε:**  
`raw_result` περιέχει μια ιεραρχία `Pages → Lines → Words`. Κάθε γραμμή γνωρίζει τις αρχικές της συντεταγμένες X/Y, ώστε να μπορείτε να αναδημιουργήσετε πίνακες ή φόρμες αργότερα αν το επιθυμείτε.

---

## Βήμα 3 – Εφαρμογή AI‑Βασισμένου Ορθογραφικού Ελέγχου (OCR Post Processing)

Η ακατέργαστη έξοδος OCR είναι συχνά γεμάτη λανθασμένες λέξεις, ειδικά με καλλιγραφικό χειρόγραφο. Το Aspose AI προσφέρει έναν βολικό post‑processor που συνδέεται απευθείας με το αντικείμενο αποτελέσματος.

```python
# Initialise Aspose AI for spell‑checking
ai = AsposeAI()
ai.set_post_processor(AIProcessor.SpellCheck, {})

# Run spell‑check on the structured OCR result
corrected_result = ai.run_postprocessor(raw_result)
```

**Γιατί ο ορθογραφικός έλεγχος αλλάζει το παιχνίδι:**  
Ακόμη και μια μέτρια ακρίβεια 85 % μπορεί να ανέβει σε 95 %+ με μια διέλευση που γνωρίζει λεξικό. Ο επεξεργαστής `SpellCheck` σέβεται τη διάταξη, έτσι οι αλλαγές γραμμής παραμένουν αμετάβλητες ενώ οι μεμονωμένες λέξεις διορθώνονται.

---

## Βήμα 4 – Αποθήκευση του Δομημένου, Διορθωμένου Αποτελέσματος

Τα περισσότερα downstream συστήματα προτιμούν JSON, CSV ή απλό κείμενο. Η βοηθητική λειτουργία `save_result` του Aspose OCR γράφει ολόκληρο το `StructuredResult` σε αρχείο διατηρώντας την ιεραρχία.

```python
# Persist the corrected result as JSON
output_path = "YOUR_DIRECTORY/result.json"
OcrUtil.save_result(corrected_result, output_path)

# Print each line to the console for quick verification
for line in corrected_result.Lines:
    print(line.Text)
```

**Αναμενόμενη έξοδος κονσόλας (παράδειγμα):**

```
Dear John,
Please find the attached invoice for March.
Total amount: $1,250.00
Thank you,
Acme Corp.
```

Παρατηρήστε πώς οι αλλαγές γραμμής ταιριάζουν με το αρχικό σκανάρισμα, και κοινά σφάλματα OCR όπως “March” → “Marrh” διορθώνονται αυτόματα.

---

## Βήμα 5 – (Προαιρετικό) Εξαγωγή σε CSV για Εργασίες Φύλλων Εργασίας

Αν χρειάζεστε δεδομένα σε μορφή πίνακα, η μετατροπή του δομημένου αποτελέσματος σε CSV είναι απλή. Παρακάτω υπάρχει μια βοηθητική συνάρτηση που μπορείτε να ενσωματώσετε στο script σας.

```python
import csv

def export_to_csv(structured_result, csv_path):
    """
    Writes each line of the OCR result to a CSV row.
    Columns are inferred from whitespace gaps.
    """
    with open(csv_path, mode="w", newline="", encoding="utf-8") as file:
        writer = csv.writer(file)
        for line in structured_result.Lines:
            # Split on multiple spaces to guess column boundaries
            columns = [col.strip() for col in line.Text.split("  ") if col]
            writer.writerow(columns)

csv_output = "YOUR_DIRECTORY/result.csv"
export_to_csv(corrected_result, csv_output)
print(f"CSV exported to {csv_output}")
```

Τώρα έχετε ένα CSV έτοιμο για εισαγωγή που αντικατοπτρίζει την αρχική διάταξη της σελίδας—ιδανικό για λογιστικές ή διαδικασίες εισαγωγής δεδομένων.

---

## Συνηθισμένα Πιθανά Σφάλματα & Πώς να τα Αποφύγετε

| Πρόβλημα | Γιατί Συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| **Κενή έξοδος** | Η εικόνα δεν φορτώθηκε σωστά (λάθος διαδρομή) | Επαληθεύστε το `image_path` και βεβαιωθείτε ότι το αρχείο υπάρχει. |
| **Ασυνήθιστοι χαρακτήρες** | Παράλειψη `preprocess` σε εικόνες χαμηλής αντίθεσης | Πάντα καλέστε `OcrUtil.preprocess`. |
| **Απώλεια διάταξης** | Χρήση `engine.recognize()` αντί για `recognize_structured()` | Χρησιμοποιήστε τη δομημένη μέθοδο για διατήρηση διάταξης. |
| **Αποτυχία ορθογραφικού ελέγχου** | Χωρίς internet ή μη έγκυρα διαπιστευτήρια Aspose AI | Βεβαιωθείτε ότι το περιβάλλον σας μπορεί να προσεγγίσει τις υπηρεσίες Aspose AI ή χρησιμοποιήστε λεξικά offline. |

---

## Επέκταση του Pipeline: Από Δομημένο OCR σε NLP

Μόλις έχετε καθαρό, δομημένο κείμενο, το επόμενο λογικό βήμα είναι η ενσωμάτωση σε μοντέλο NLP (π.χ., spaCy) για εξαγωγή οντοτήτων. Επειδή η διάταξη διατηρείται, μπορείτε να αντιστοιχίσετε τις εντοπισμένες οντότητες στις αρχικές τους θέσεις—ένα μεγάλο πλεονέκτημα για AI κεντρικό στα έγγραφα.

```python
import spacy

nlp = spacy.load("en_core_web_sm")
doc = nlp("\n".join([line.Text for line in corrected_result.Lines]))

for ent in doc.ents:
    print(ent.text, ent.label_)
```

Αυτό το απόσπασμα κώδικα εξάγει ημερομηνίες, χρηματικά ποσά και ονόματα ατόμων, μετατρέποντας μια σκαναρισμένη απόδειξη σε χρήσιμα δεδομένα.

---

## Συνοπτική Επισκόπηση

Καλύψαμε κάθε πτυχή του **OCR δομημένου κειμένου** με το Aspose OCR για Python:

1. **Φορτώστε εικόνα OCR** με αυτόματη περιστροφή και προεπεξεργασία.  
2. **Τρέξτε OCR** διατηρώντας τη διάταξη (`recognize_structured`).  
3. **Εφαρμόστε OCR post processing** μέσω AI ορθογραφικού ελέγχου.  
4. **Αποθηκεύστε** το διορθωμένο αποτέλεσμα ως JSON (και προαιρετικά CSV).  
5. **Επεκτείνετε** τη ροή εργασίας σε NLP ή downstream analytics.

Όλα αυτά τυλίγονται σε ένα ενιαίο, αυτόνομο script που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Python.

---

## Τι Ακολουθεί;

- **Δοκιμάστε διαφορετικές γλώσσες** – το Aspose OCR υποστηρίζει πάνω από 60 γλώσσες· απλώς ορίστε `engine.Language = "fra"` για τα Γαλλικά.  
- **Βελτιώστε την προεπεξεργασία** – προσαρμόστε τις παραμέτρους του `OcrUtil.preprocess` για θορυβώδεις αποδείξεις.  
- **Ενσωματώστε με Azure Functions** – μετατρέψτε το script σε serverless API που επεξεργάζεται ανεβάσματα σε πραγματικό χρόνο.  

Αν σας ενδιαφέρει **πώς να OCR εικόνες** μαζικά, σκεφτείτε έναν βρόχο που διατρέχει έναν φάκελο και προσθέτει κάθε JSON αποτέλεσμα σε ένα κύριο αρχείο. Το ίδιο μοτίβο λειτουργεί και για PDFs—απλώς μετατρέψτε κάθε σελίδα σε εικόνα πρώτα.

---

![Διάγραμμα του Pipeline OCR Δομημένου Κειμένου – δείχνει φόρτωση εικόνας OCR, προεπεξεργασία, μηχανή OCR, AI post‑processing και έξοδο](/images/structured_ocr_pipeline.png "pipeline OCR δομημένου κειμένου")

*Κείμενο alt: εικονογράφηση του pipeline OCR δομημένου κειμένου*  

---

### Καλό κώδικα!

Αν αντιμετωπίσετε κάποιο πρόβλημα, αφήστε ένα σχόλιο παρακάτω ή ελέγξτε τα επίσημα docs του Aspose για τις τελευταίες ενημερώσεις API. Θυμηθείτε, το κλειδί για αξιόπιστο OCR είναι καθαρή είσοδος και έξυπνη post‑επεξεργασία—μια φορά που τα κυριαρχήσετε, το υπόλοιπο είναι απλώς glue code.

---


## Τι Θα Μάθετε Στη Σειρά Επόμενη;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}