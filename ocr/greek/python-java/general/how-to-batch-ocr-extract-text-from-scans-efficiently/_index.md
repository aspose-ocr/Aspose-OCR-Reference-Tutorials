---
category: general
date: 2026-04-26
description: Πώς να κάνετε ομαδική OCR τα έγγραφά σας και να εξάγετε κείμενο από σαρώσεις
  σε Python. Μάθετε βήμα‑βήμα την ομαδική επεξεργασία με το OcrEngine για έξοδο JSON.
draft: false
keywords:
- how to batch OCR
- extract text from scans
- OCR batch processing
- Python OCR automation
- JSON OCR output
language: el
og_description: Πώς να κάνετε ομαδική OCR στα σαρωμένα αρχεία σας και να εξάγετε κείμενο
  από τις σαρώσεις σε ένα μόνο script. Πλήρης κώδικας, συμβουλές και διαχείριση ακραίων
  περιπτώσεων.
og_title: Πώς να κάνετε Batch OCR – Γρήγορος οδηγός Python
tags:
- OCR
- Python
- Automation
title: Πώς να κάνετε μαζική OCR – Εξαγωγή κειμένου από σαρώσεις αποδοτικά
url: /el/python-java/general/how-to-batch-ocr-extract-text-from-scans-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να κάνετε Batch OCR – Εξαγωγή Κειμένου από Σαρώσεις Αποτελεσματικά

Έχετε αναρωτηθεί ποτέ **πώς να κάνετε batch OCR** σε ένα βουνό σαρωμένων PDF χωρίς να χάσετε το μυαλό σας; Δεν είστε ο μόνος—οι προγραμματιστές ρωτούν συνεχώς, *«Πώς μπορώ να εξάγω κείμενο από σαρώσεις σε μία μόνο εκτέλεση;»* Τα καλά νέα είναι ότι με λίγες γραμμές Python μπορείτε να μετατρέψετε αυτή τη βαρετή εργασία σε μια ομαλή, αυτοματοποιημένη διαδικασία.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από μια πλήρη, έτοιμη‑για‑εκτέλεση λύση που **εξάγει κείμενο από σαρώσεις**, αποθηκεύει τα αποτελέσματα ως JSON, και σας παρέχει έναν γρήγορο έλεγχο στο τέλος. Χωρίς εξωτερικές υπηρεσίες, χωρίς μαγεία—απλώς καθαρό Python, η κλάση `OcrEngine`, και λίγη διαχείριση φακέλων.

## Τι Θα Κερδίσετε

- Ένα πλήρως λειτουργικό script που **κάνει batch OCR** σε οποιονδήποτε φάκελο εικόνων.
- Καθαρές εξηγήσεις του *γιατί* υπάρχει κάθε γραμμή, όχι μόνο του *τι* κάνει.
- Συμβουλές για τη διαχείριση κενών φακέλων, αρχείων που δεν είναι εικόνες, και μεγάλων batch.
- Ένας τρόπος για να επαληθεύσετε ότι η έξοδος JSON περιέχει πραγματικά το εξαγόμενο κείμενο.

### Προαπαιτούμενα (το ελάχιστο)

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|-----------------------|
| Python 3.8+ | Σύγχρονη σύνταξη & type hints |
| `OcrEngine` library (or a compatible wrapper) | Κύρια λειτουργικότητα OCR |
| Φάκελος με σαρωμένα αρχεία εικόνας (PNG, JPG, TIFF) | Δεδομένα εισόδου |
| Δικαιώματα εγγραφής για το φάκελο εξόδου | Αποθήκευση αποτελεσμάτων JSON |

Αν τα έχετε ήδη, υπέροχα—ας βουτήξουμε.

![διαδικασία batch OCR](image-placeholder.png){alt="διαδικασία batch OCR"}

## Βήμα 1 – Αρχικοποίηση του OCR Engine (πώς να κάνετε batch OCR)

Πριν μπορέσουμε να επεξεργαστούμε οτιδήποτε, χρειαζόμαστε μια παρουσία του OCR engine. Σκεφτείτε το ως το «εγκέφαλο» που θα διαβάζει κάθε εικόνα και θα παράγει κείμενο. Η αρχικοποίηση του μία φορά και η επαναχρησιμοποίησή του σε όλο το batch είναι το πιο αποδοτικό μοτίβο.

```python
# Step 1: Create an OCR engine instance
# The OcrEngine class abstracts the low‑level OCR library (Tesseract, EasyOCR, etc.)
ocr_engine = OcrEngine()
```

> **Γιατί να επαναχρησιμοποιήσετε την ίδια παρουσία;**  
> Η δημιουργία νέου engine για κάθε αρχείο θα φορτώνει επανειλημμένα βαριά μοντέλα στη μνήμη, επιβραδύνοντας δραματικά το batch. Μία παρουσία διατηρεί το μοντέλο στη RAM και σας επιτρέπει να επεξεργαστείτε χιλιάδες εικόνες χωρίς αισθητή καθυστέρηση.

## Βήμα 2 – Καθορίστε το Φάκελο Σαρώσεων (εξαγωγή κειμένου από σαρώσεις)

Οι σαρώσεις σας βρίσκονται κάπου στο δίσκο. Ας πούμε στο script πού να τις βρει. Η χρήση απόλυτων διαδρομών αποφεύγει εκπλήξεις «αρχείο δεν βρέθηκε» όταν το script εκτελείται από διαφορετικό τρέχον φάκελο.

```python
import os

# Step 2: Specify the folder that contains scanned images
# Replace YOUR_DIRECTORY with the actual base path on your machine.
input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
```

> **Συμβουλή:**  
> Αν είστε σε Windows, οι μπροστιές κάθετες (`/`) λειτουργούν καλά με `os.path.abspath`, έτσι δεν χρειάζεται να διαφύγετε τις ανάστροφες κάθετες (`\`).

## Βήμα 3 – Επιλέξτε Πού Θα Μεταφερθούν τα Αποτελέσματα JSON

Πιθανώς θέλετε έναν τακτοποιημένο φάκελο για τα αποτελέσματα OCR. Η διατήρηση της εξόδου χωριστά από την πηγή διευκολύνει τον καθαρισμό αργότερα ή την τροφοδοσία του JSON σε άλλη pipeline.

```python
# Step 3: Specify where the JSON results should be saved
output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
os.makedirs(output_dir, exist_ok=True)   # Ensure the folder exists
```

> **Γιατί να δημιουργήσετε το φάκελο προγραμματιστικά;**  
> Εγγυάται ότι το script δεν θα καταρρεύσει αν ο φάκελος λείπει, και το `exist_ok=True` κάνει τη λειτουργία επαναληπτική—εκτελέστε το script πολλές φορές χωρίς σφάλματα.

## Βήμα 4 – Εκτέλεση της Batch Διαδικασίας (πώς να κάνετε batch OCR)

Τώρα η ουσία: να πείτε στο `ocr_engine` να περάσει από κάθε αρχείο στο `input_dir`, να εκτελέσει OCR, και να αποθηκεύσει JSON στο `output_dir`. Η σημαία `format="json"` λέει στο engine να σειριοποιήσει το αποτέλεσμα με δομημένο τρόπο που αγαπούν τα downstream εργαλεία.

```python
# Step 4: Run batch processing to convert all scans to JSON format
ocr_engine.batch_process(
    input_folder=input_dir,
    output_folder=output_dir,
    format="json"
)
```

### Τι συμβαίνει υπό το καπό;

1. **Ανακάλυψη αρχείων** – Το engine σαρώει το `input_folder` αναδρομικά, αγνοώντας κρυφά αρχεία.  
2. **Επικύρωση αρχείων** – Μόνο υποστηριζόμενες επεκτάσεις εικόνας (`.png`, `.jpg`, `.tif`, κλπ.) τροφοδοτούνται στο μοντέλο OCR.  
3. **Εκτέλεση OCR** – Κάθε εικόνα αποστέλλεται στο OCR engine· κείμενο, βαθμοί εμπιστοσύνης και δεδομένα διάταξης καταγράφονται.  
4. **Σειριοποίηση JSON** – Το αποτέλεσμα γράφεται σε αρχείο με το ίδιο βασικό όνομα αλλά με επέκταση `.json` στο `output_folder`.

> **Διαχείριση ειδικών περιπτώσεων:**  
> - **Κενός φάκελος:** Το engine καταγράφει “No files found” και επιστρέφει ομαλά.  
> - **Κατεστραμμένη εικόνα:** Παραλείπει το αρχείο, καταγράφει ένα σφάλμα στο `batch_errors.log`, και συνεχίζει.  
> - **Μεγάλο batch (10k+ αρχεία):** Η χρήση μνήμης παραμένει χαμηλή επειδή κάθε εικόνα επεξεργάζεται ανεξάρτητα.

## Βήμα 5 – Επιβεβαίωση Ολοκλήρωσης Μετατροπής

Μια απλή εντολή `print` παρέχει άμεση ανατροφοδότηση στην κονσόλα. Για pipelines παραγωγής μπορείτε να την αντικαταστήσετε με κλήση logging ή ειδοποίηση email.

```python
# Step 5: Inform the user that the batch conversion has finished
print("Batch conversion complete.")
```

Όταν δείτε αυτή τη γραμμή, μπορείτε με ασφάλεια να ελέγξετε το φάκελο `json_output`. Κάθε αρχείο JSON θα μοιάζει περίπου έτσι:

```json
{
  "file_name": "invoice_001.png",
  "text": "Invoice #001\nDate: 2024‑12‑01\nTotal: $1,234.56",
  "confidence": 0.97,
  "layout": [
    {"line": 1, "bbox": [10, 20, 200, 40]},
    {"line": 2, "bbox": [10, 50, 180, 70]},
    {"line": 3, "bbox": [10, 80, 150, 100]}
  ]
}
```

Τώρα μπορείτε να τροφοδοτήσετε αυτά τα αρχεία JSON σε μια βάση δεδομένων, έναν δείκτη αναζήτησης, ή οποιοδήποτε downstream εργαλείο ανάλυσης.

## Συχνές Ερωτήσεις (και γρήγορες απαντήσεις)

**Q: Τι γίνεται αν χρειαστεί να επεξεργαστώ PDF αντί για εικόνες;**  
A: Μετατρέψτε κάθε σελίδα PDF σε εικόνα πρώτα (π.χ., χρησιμοποιώντας `pdf2image`) και τοποθετήστε τα παραγόμενα αρχεία PNG/JPG στο `input_dir`. Η λογική του batch OCR παραμένει αμετάβλητη.

**Q: Μπορώ να αλλάξω τη μορφή εξόδου σε απλό κείμενο;**  
A: Απόλυτα. Αντικαταστήστε το `format="json"` με `format="txt"` και το engine θα γράψει ένα αρχείο `.txt` που περιέχει μόνο το εξαγόμενο κείμενο.

**Q: Οι σαρώσεις μου βρίσκονται σε πολλαπλούς υπο‑φακέλους—θα κάνει το script αναδρομή;**  
A: Ναι. Το `batch_process` περιηγείται στο δέντρο καταλόγων εξ ορισμού. Αν θέλετε επίπεδη έξοδο, ορίστε `flatten=True` (αν η βιβλιοθήκη το υποστηρίζει) ή επεξεργαστείτε τα ονόματα αρχείων JSON μετά.

**Q: Πώς να διαχειριστώ μη‑λατινικά scripts;**  
A: Αρχικοποιήστε το `OcrEngine` με παράμετρο γλώσσας, π.χ., `OcrEngine(lang="spa+eng")`. Η βρόχος batch δεν χρειάζεται αλλαγές.

## Επαγγελματικές Συμβουλές & Συνηθισμένα Πιθανά Σφάλματα

- **Το μέγεθος batch μετράει:** Αν παρατηρήσετε αυξήσεις CPU, περιορίστε τη διαδικασία με ένα απλό `time.sleep(0.1)` μεταξύ των αρχείων.  
- **Logging:** Αντικαταστήστε την κλήση `print` με το module `logging` του Python για καταγραφή χρονικών σημείων και επιπέδων σφάλματος.  
- **Σύγκρουση ονομάτων αρχείων:** Αν δύο σαρώσεις έχουν το ίδιο βασικό όνομα αλλά βρίσκονται σε διαφορετικούς υπο‑φακέλους, τα αρχεία JSON θα αντικαταστήσουν το ένα το άλλο. Προσθέστε ένα hash της σχετικής διαδρομής στο όνομα εξόδου για να το αποφύγετε.  
- **Διαρροές μνήμης:** Κάποια OCR back‑ends κρατούν εγγενείς πόρους. Καλέστε `ocr_engine.close()` στο τέλος του script αν η βιβλιοθήκη παρέχει μέθοδο καθαρισμού.

## Πλήρες Script – Έτοιμο για Αντιγραφή & Επικόλληση

```python
import os
from ocr_engine import OcrEngine   # Replace with the actual import path

def main():
    # Step 1: Initialize the OCR engine (how to batch OCR)
    ocr_engine = OcrEngine()

    # Step 2: Directory with scanned images (extract text from scans)
    input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
    if not os.path.isdir(input_dir):
        raise FileNotFoundError(f"Input folder not found: {input_dir}")

    # Step 3: Destination for JSON results
    output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
    os.makedirs(output_dir, exist_ok=True)

    # Step 4: Run the batch OCR process
    ocr_engine.batch_process(
        input_folder=input_dir,
        output_folder=output_dir,
        format="json"
    )

    # Step 5: Confirmation message
    print("Batch conversion complete.")

if __name__ == "__main__":
    main()
```

**Αναμενόμενη έξοδος κονσόλας**

```
Scanning folder: /home/user/YOUR_DIRECTORY/scans/
Found 42 image files.
Processing file 1/42: invoice_001.png … done.
Processing file 2/42: receipt_2024-03.jpg … done.
…
Batch conversion complete.
```

Μπορείτε να επαληθεύσετε το JSON ανοίγοντας οποιοδήποτε αρχείο στο `json_output` με έναν επεξεργαστή κειμένου ή φορτώνοντάς το σε Python:

```python
import json, pathlib

sample = pathlib.Path(output_dir) / "invoice_001.json"
data = json.loads(sample.read_text())
print(data["text"])
```

Θα πρέπει να δείτε το ακατέργαστο κείμενο που εξήχθη από OCR να τυπώνεται στην κονσόλα.

## Συμπερασματικά

Μόλις καλύψαμε **πώς να κάνετε batch OCR** σε ολόκληρο φάκελο σαρωμένων εικόνων και **να εξάγετε κείμενο από σαρώσεις** σε καθαρά, μηχανικά αναγνώσιμα αρχεία JSON. Η προσέγγιση είναι σκόπιμα απλή: ρυθμίστε το engine μία φορά, δείξτε το σε έναν φάκελο, και αφήστε τη βιβλιοθήκη να κάνει το βαρέως έργο. Από εδώ μπορείτε:

- Συνδέστε το JSON

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}