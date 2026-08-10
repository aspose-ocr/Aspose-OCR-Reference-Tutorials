---
category: general
date: 2026-06-16
description: Εξάγετε κείμενο από αρχεία TIFF χρησιμοποιώντας Python OCR. Μάθετε πώς
  να μετατρέπετε TIFF σε κείμενο βήμα‑βήμα, διαχειριζόμενοι έγγραφα πολλαπλών σελίδων
  με ευκολία.
draft: false
keywords:
- extract text from tiff
- convert tiff to text
- Python OCR multi‑page TIFF
- OCR language settings
- OCR engine Python
language: el
og_description: Εξάγετε κείμενο από αρχεία TIFF με Python OCR. Ακολουθήστε αυτόν τον
  οδηγό για να μετατρέψετε TIFF σε κείμενο, να διαχειριστείτε σαρώσεις πολλαπλών σελίδων
  και να έχετε καθαρά αποτελέσματα.
og_title: Εξαγωγή κειμένου από TIFF – Πλήρης οδηγός Python
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  headline: Extract Text from TIFF – Complete Python Guide
  type: TechArticle
- description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  name: Extract Text from TIFF – Complete Python Guide
  steps:
  - name: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
    text: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
  - name: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
    text: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
  - name: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
    text: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
  - name: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
    text: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Text extraction
title: Εξαγωγή κειμένου από TIFF – Πλήρης οδηγός Python
url: /el/python-java/general/extract-text-from-tiff-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από TIFF – Πλήρης Οδηγός Python

Έχετε χρειαστεί ποτέ να **εξάγετε κείμενο από εικόνες TIFF** αλλά δεν ήξερατε από πού να ξεκινήσετε; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν δουλεύουν με σκαναρισμένα αρχεία ή παλαιά έγγραφα. Το καλό νέο; Με λίγες γραμμές Python μπορείτε να **μετατρέψετε TIFF σε κείμενο** σε ελάχιστο χρόνο, ακόμα και όταν το αρχείο περιέχει δεκάδες σελίδες.

Σε αυτό το tutorial θα περάσουμε από ένα πραγματικό παράδειγμα: φόρτωση ενός πολυ-σελίδας TIFF, ορισμός της γλώσσας OCR στα Γαλλικά, και εξαγωγή του αναγνωρισμένου κειμένου από κάθε σελίδα. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση script, θα καταλάβετε γιατί κάθε βήμα είναι σημαντικό, και θα ξέρετε πώς να το προσαρμόσετε για άλλες γλώσσες ή μορφές εικόνας.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

- Python 3.8 ή νεότερη έκδοση εγκατεστημένη.
- Το πακέτο `ocr` (ή οποιαδήποτε συμβατή βιβλιοθήκη OCR που προσφέρει κλάση `OcrEngine`). Μπορείτε να το εγκαταστήσετε με `pip install ocr-lib`—αντικαταστήστε το με το πραγματικό όνομα του πακέτου που χρησιμοποιείτε.
- Ένα πολυ‑σελίδων TIFF αρχείο (π.χ. `french-scans.tif`) που θέλετε να επεξεργαστείτε.
- Βασική εξοικείωση με scripting σε Python.

Καμία βαριά εξάρτηση, καμία εξωτερική υπηρεσία—μόνο καθαρή Python και μια μηχανή OCR.

---

## Βήμα 1: Ρύθμιση της Μηχανής OCR για **Εξαγωγή Κειμένου από TIFF**

Πρώτα απ' όλα—χρειαζόμαστε ένα αντικείμενο OCR engine και πρέπει να του πούμε ποια γλώσσα θα χρησιμοποιήσει. Στην περίπτωσή μας το υλικό είναι στα Γαλλικά, οπότε θα ορίσουμε τη γλώσσα αναλόγως.

```python
import ocr  # Replace with the actual import if your OCR library uses a different name

# Create the OCR engine
engine = ocr.OcrEngine()

# Tell the engine to look for French characters
engine.language = ocr.Language.FRENCH
```

**Γιατί είναι σημαντικό:**  
Η ρύθμιση της γλώσσας βελτιώνει δραματικά την ακρίβεια. Γαλλικοί χαρακτήρες όπως “é” ή “ç” θα διαβαστούν λανθασμένα ως γενικά σύμβολα αν η μηχανή προεπιλέξει τα Αγγλικά. Επιλέγοντας ρητά τα Γαλλικά δίνουμε στη μηχανή τον σωστό χάρτη χαρακτήρων.

> **Συμβουλή:** Αν επεξεργάζεστε έγγραφα σε πολλές γλώσσες, μπορείτε να αλλάζετε το `engine.language` εν κινήσει πριν από κάθε κλήση `recognize()`.

---

## Βήμα 2: Φόρτωση του Πολυ‑Σελίδας TIFF που Θέλετε να **Μετατρέψετε TIFF σε Κείμενο**

Ένα TIFF μπορεί να περιέχει πολλά frames—σκεφτείτε κάθε frame ως ξεχωριστή σελίδα. Η βιβλιοθήκη OCR αφαιρεί αυτή τη δυσκολία για εμάς, οπότε απλώς δείχνουμε στο αρχείο.

```python
# Path to your multi‑page TIFF
tiff_path = "YOUR_DIRECTORY/french-scans.tif"

# Load the file; the engine now knows how many pages it contains
engine.load_from_file(tiff_path)
```

**Προειδοποίηση για ακραία περιπτώσεις:**  
Αν η διαδρομή του αρχείου είναι λανθασμένη ή το TIFF είναι κατεστραμμένο, η μέθοδος `load_from_file` θα ρίξει εξαίρεση. Τυλίξτε τη σε μπλοκ `try/except` για κώδικα παραγωγής:

```python
try:
    engine.load_from_file(tiff_path)
except Exception as e:
    print(f"Failed to load TIFF: {e}")
    raise
```

---

## Βήμα 3: Εκτέλεση OCR σε Ολόκληρο το Έγγραφο – Ο Πυρήνας της **Εξαγωγής Κειμένου από TIFF**

Τώρα αφήνουμε τη μηχανή να κάνει τη μαγεία της. Η κλήση `recognize()` επεξεργάζεται κάθε σελίδα σε μία φορά και επιστρέφει ένα πλούσιο αντικείμενο αποτελέσματος.

```python
# Perform OCR on all pages at once
multi_result = engine.recognize()
```

**Τι συμβαίνει στο παρασκήνιο;**  
Η μηχανή διασχίζει κάθε frame, εφαρμόζει προεπεξεργασία (ευθυγράμμιση, δυαδικοποίηση), τρέχει το νευρωνικό δίκτυο, και συγκεντρώνει το αποτέλεσμα. Επειδή κάλεσαμε το `recognize()` μόνο μία φορά, η βιβλιοθήκη μπορεί να μοιραστεί πόρους μεταξύ των σελίδων, κάτι που είναι γρηγορότερο από το χειροκίνητο βρόχο.

---

## Βήμα 4: Ανάκτηση του Αναγνωρισμένου Κειμένου από το JSON Αποτέλεσμα – **Μετατροπή TIFF σε Κείμενο** Σελίδα‑με‑Σελίδα

Το αντικείμενο αποτελέσματος μπορεί να σειριοποιηθεί σε JSON. Μέσα σε αυτό το JSON θα βρείτε έναν πίνακα `pages`, ο καθένας με ένα πεδίο `text`.

```python
# Convert the result to a Python dict (JSON-like)
result_dict = multi_result.to_json()

# Extract the list of pages
pages = result_dict["pages"]
```

Τώρα έχουμε μια καθαρή λίστα Python όπου κάθε στοιχείο αντιστοιχεί στην έξοδο OCR μιας σελίδας.

---

## Βήμα 5: Εκτύπωση ή Αποθήκευση του Κειμένου για Κάθε Σελίδα – Το Τελευταίο Κομμάτι της **Εξαγωγής Κειμένου από TIFF**

Ας περάσουμε από τις σελίδες και να εμφανίσουμε το εξαγόμενο κείμενο. Μπορείτε επίσης να γράψετε κάθε σελίδα σε ξεχωριστό αρχείο `.txt` αν προτιμάτε.

```python
for i, page in enumerate(pages, start=1):
    print(f"--- Page {i} ---")
    print(page["text"])
    print()  # Blank line for readability
```

### Αναμενόμενο Αποτέλεσμα (παράδειγμα)

```
--- Page 1 ---
Bonjour, ceci est un exemple de texte extrait d'une image TIFF.

--- Page 2 ---
Le deuxième page contient davantage d'informations en français.
```

Αν το OCR πέτυχε, θα δείτε ένα καθαρό μπλοκ γαλλικών προτάσεων για κάθε σελίδα. Αν παρατηρήσετε ακατάστατους χαρακτήρες, ελέγξτε ξανά τη ρύθμιση γλώσσας ή σκεφτείτε να αυξήσετε την ανάλυση της εικόνας πριν το OCR.

---

## Αντιμετώπιση Συνηθισμένων Προβλημάτων Κατά τη **Μετατροπή TIFF σε Κείμενο**

| Πρόβλημα | Γιατί Συμβαίνει | Γρήγορη Λύση |
|----------|----------------|--------------|
| **Κενός πίνακας `pages`** | Το TIFF δεν φορτώθηκε σωστά ή δεν έχει frames. | Επαληθεύστε τη διαδρομή του αρχείου και βεβαιωθείτε ότι το TIFF δεν είναι PNG μονής σελίδας με κατάληξη TIFF. |
| **Ασυνεπείς χαρακτήρες** | Ασυμφωνία γλώσσας ή χαμηλή ποιότητα εικόνας. | Ορίστε το σωστό `engine.language` και προεπεξεργαστείτε την εικόνα (π.χ. αυξήστε DPI). |
| **Κατανάλωση μνήμης σε μεγάλα TIFF** | Η φόρτωση όλων των σελίδων ταυτόχρονα καταναλώνει RAM. | Επεξεργαστείτε σε τμήματα: φορτώστε ένα frame, αναγνωρίστε, απορρίψτε πριν προχωρήσετε στο επόμενο. |
| **Σφάλματα Unicode κατά την εκτύπωση** | Η κωδικοποίηση του τερματικού δεν υποστηρίζει διακριτικούς χαρακτήρες. | Χρησιμοποιήστε `print(page["text"].encode('utf-8').decode('utf-8'))` ή ρυθμίστε το τερματικό σας σε UTF‑8. |

---

## Επέκταση του Script: Από την **Εξαγωγή Κειμένου από TIFF** στην Επεξεργασία Πολλαπλών Αρχείων

Τώρα που έχετε μια σταθερή βάση, σκεφτείτε τα παρακάτω βήματα:

1. **Μαζική μετατροπή** – Τυλίξτε όλη τη ροή σε μια συνάρτηση `def ocr_tiff(path):` και επαναλάβετε τη για έναν φάκελο TIFF αρχείων.
2. **Αποθήκευση σε αρχεία** – Αντί για εκτύπωση, γράψτε το κείμενο κάθε σελίδας σε `page_{i}.txt` ή ενώστε τα όλα σε ένα ενιαίο έγγραφο.
3. **Εναλλακτικές μηχανές OCR** – Αν χρειάζεστε μεγαλύτερη ακρίβεια, αντικαταστήστε το `ocr.OcrEngine()` με Tesseract (`pytesseract`) ή Azure Cognitive Services—διατηρώντας την ίδια λογική “εξαγωγής κειμένου από TIFF”.
4. **Μετα-επεξεργασία** – Εκτελέστε ορθογραφικό έλεγχο, ανίχνευση γλώσσας ή καθαρισμό με regex για να βελτιώσετε το ακατέργαστο OCR output.

---

## Πλήρες, Έτοιμο‑για‑Εκτέλεση Script

Παρακάτω βρίσκεται ο πλήρης κώδικας, έτοιμος για αντιγραφή‑επικόλληση. Περιλαμβάνει βασική διαχείριση σφαλμάτων και προαιρετική αποθήκευση του κειμένου κάθε σελίδας σε ξεχωριστά αρχεία.

```python
import ocr  # Adjust import based on your OCR library
import os

def extract_text_from_tiff(tiff_path: str, output_dir: str = None) -> list:
    """
    Loads a multi‑page TIFF, runs OCR, and returns a list of strings,
    one per page. Optionally saves each page to a .txt file.
    """
    # Initialize engine and set language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.FRENCH

    # Load the TIFF file
    try:
        engine.load_from_file(tiff_path)
    except Exception as e:
        raise RuntimeError(f"Unable to load {tiff_path}: {e}")

    # Run OCR on all pages
    multi_result = engine.recognize()

    # Parse JSON result
    pages = multi_result.to_json()["pages"]
    texts = [page["text"] for page in pages]

    # If an output directory is provided, write each page to a file
    if output_dir:
        os.makedirs(output_dir, exist_ok=True)
        for i, text in enumerate(texts, start=1):
            file_path = os.path.join(output_dir, f"page_{i}.txt")
            with open(file_path, "w", encoding="utf-8") as f:
                f.write(text)

    return texts

if __name__ == "__main__":
    # Example usage – replace with your actual TIFF path
    tiff_file = "YOUR_DIRECTORY/french-scans.tif"
    # Optional: where to store per‑page text files
    out_folder = "extracted_pages"

    page_texts = extract_text_from_tiff(tiff_file, out_folder)

    for i, txt in enumerate(page_texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()
```

Τρέξτε αυτό το script, ορίστε το `tiff_file` στο έγγραφό σας, και παρακολουθήστε την κονσόλα να γεμίζει με καθαρές γαλλικές προτάσεις. Αν δώσετε τιμή στο `out_folder`, θα βρείτε επίσης μια σειρά από αρχεία `page_#.txt` έτοιμα για επόμενη επεξεργασία.

---

## Συμπέρασμα

Μόλις **εξάγαμε κείμενο από αρχεία TIFF** χρησιμοποιώντας μια απλή ροή OCR σε Python, και τώρα ξέρετε πώς να **μετατρέψετε TIFF σε κείμενο** αξιόπιστα. Από την αρχικοποίηση της μηχανής με τη σωστή γλώσσα μέχρι την επανάληψη πάνω στο JSON αποτέλεσμα κάθε σελίδας, εξηγήσαμε κάθε βήμα με το «γιατί», ώστε να μπορείτε να προσαρμόσετε το μοτίβο σε άλλες γλώσσες, μορφές εικόνας ή μεγαλύτερα batch jobs.

Τι θα κάνετε στη συνέχεια; Δοκιμάστε να αντικαταστήσετε το backend OCR με Tesseract, πειραματιστείτε με διαφορετικά language packs, ή ενσωματώστε το αποτέλεσμα σε μια αναζητήσιμη βάση δεδομένων. Ο ουρανός είναι το όριο όταν μπορείτε να μετατρέψετε αξιόπιστα σκαναρισμένες εικόνες σε αναζητήσιμο κείμενο.

Μη διστάσετε να αφήσετε ένα σχόλιο αν αντιμετωπίσετε δυσκολίες ή έχετε ιδέες για περαιτέρω βελτιώσεις. Καλή προγραμματιστική διασκέδαση!

## Τι Θα Μάθετε Στη Σειρά Επόμενη;

Οι παρακάτω οδηγίες καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}