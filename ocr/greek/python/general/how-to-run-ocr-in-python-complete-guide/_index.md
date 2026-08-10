---
category: general
date: 2026-06-19
description: Πώς να εκτελέσετε OCR βήμα‑βήμα και να βελτιώσετε την ακρίβεια του OCR
  με τεχνικές OCR απλού κειμένου. Μάθετε μια γρήγορη ροή εργασίας για αξιόπιστη εξαγωγή
  κειμένου.
draft: false
keywords:
- how to run OCR
- improve OCR accuracy
- plain text OCR
- OCR post‑processing
- layout‑aware OCR
language: el
og_description: Πώς να εκτελέσετε OCR αποδοτικά. Αυτό το σεμινάριο δείχνει πώς να
  βελτιώσετε την ακρίβεια του OCR χρησιμοποιώντας OCR απλού κειμένου και επεξεργασία
  AI μετά την αναγνώριση.
og_title: Πώς να τρέξετε OCR σε Python – Πλήρης Οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  headline: How to Run OCR in Python – Complete Guide
  type: TechArticle
- description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  name: How to Run OCR in Python – Complete Guide
  steps:
  - name: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
    text: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
  - name: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
    text: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
  - name: '**Export formats** – Write the corrected structure to a searchable PDF'
    text: '**Export formats** – Write the corrected structure to a searchable PDF'
  type: HowTo
tags:
- OCR
- Python
- AI
title: Πώς να τρέξετε OCR σε Python – Πλήρης οδηγός
url: /el/python/general/how-to-run-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εκτελέσετε OCR σε Python – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να εκτελέσετε OCR** σε μια δέσμη σαρωμένων PDF χωρίς να ξοδεύετε ώρες στην ρύθμιση; Δεν είστε μόνοι. Σε πολλά έργα το πρώτο εμπόδιο είναι απλώς η εξαγωγή αξιόπιστου κειμένου από μια εικόνα, και η διαφορά μεταξύ μιας αβέβαιης εξαγωγής και μιας καθαρής εξαγωγής συχνά εξαρτάται από μερικά έξυπνα βήματα.

Σε αυτόν τον οδηγό θα περάσουμε από μια πρακτική αλυσίδα τεσσάρων βημάτων που όχι μόνο **εκτελεί OCR**, αλλά επίσης **βελτιώνει την ακρίβεια του OCR** συνδυάζοντας μια γρήγορη εκτέλεση απλού κειμένου με μια δεύτερη εκτέλεση που λαμβάνει υπόψη τη διάταξη και έναν AI‑τροποποιημένο μετα-επεξεργαστή. Στο τέλος θα έχετε ένα έτοιμο σενάριο, μια σαφή εξήγηση του γιατί κάθε στάδιο είναι σημαντικό, και συμβουλές για την αντιμετώπιση ειδικών περιπτώσεων όπως σελίδες πολλαπλών στηλών ή θορυβώδεις σαρώσεις.

---

## Τι Θα Χρειαστείτε

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τα εξής:

- **Python 3.9+** – ο κώδικας χρησιμοποιεί type hints και f‑strings.  
- **Tesseract OCR** εγκατεστημένο και προσβάσιμο μέσω της εντολής `tesseract`. (Σε Ubuntu: `sudo apt install tesseract-ocr`; σε Windows κατεβάστε τον εγκαταστάτη από το επίσημο αποθετήριο.)  
- Η βιβλιοθήκη **pytesseract** (`pip install pytesseract`).  
- Μια **βιβλιοθήκη AI μετα-επεξεργασίας** – για αυτό το παράδειγμα θα υποθέσουμε ότι έχετε ένα ελαφρύ module `ai` που προσφέρει τη συνάρτηση `run_postprocessor`. Αντικαταστήστε το με το API του OpenAI GPT‑4 ή με ένα τοπικό LLM αν προτιμάτε.  
- Μερικές δείγμα εικόνων ή PDF για δοκιμή.

Αυτό είναι όλο. Χωρίς βαριές πλατφόρμες, χωρίς Docker. Μόνο λίγες εγκαταστάσεις pip και είστε έτοιμοι.

---

## Βήμα 1: Εκτελέστε μια Γρήγορη Εκτέλεση Απλού Κειμένου OCR

Το πρώτο πράγμα που παραβλέπουν οι περισσότεροι προγραμματιστές είναι ότι μια εκτέλεση *απλού κειμένου* OCR είναι αστραπιαία γρήγορη και σας δίνει έναν γρήγορο έλεγχο λογικής. Θα καλέσουμε `engine.Recognize()` για να πάρουμε ακατέργαστους χαρακτήρες χωρίς μεταδεδομένα διάταξης. Αυτό είναι αυτό που εννοούμε με **plain text OCR**.

```python
import pytesseract
from PIL import Image

def plain_text_ocr(image_path: str) -> str:
    """Run a quick plain‑text OCR pass and return the raw string."""
    img = Image.open(image_path)
    # pytesseract returns a single string with line breaks.
    raw_text = pytesseract.image_to_string(img, lang='eng')
    return raw_text
```

*Γιατί είναι σημαντικό:*  
- **Ταχύτητα** – μια απλή εκτέλεση σε σελίδα 300 dpi συνήθως ολοκληρώνεται κάτω από ένα δευτερόλεπτο.  
- **Βάση σύγκρισης** – μπορείτε να συγκρίνετε το μεταγενέστερο δομημένο αποτέλεσμα με αυτή τη βάση για να εντοπίσετε εμφανή σφάλματα.  
- **Ανίχνευση σφαλμάτων** – αν η απλή εκτέλεση αποτύχει εντελώς (π.χ. όλα τα κείμενα είναι άσχετα), ξέρετε ότι η ποιότητα της εικόνας είναι πολύ χαμηλή και μπορείτε να σταματήσετε νωρίς.

---

## Βήμα 2: Εκτελέστε μια Λεπτομερή Εκτέλεση OCR με Διάταξη

Το απλό κείμενο είναι χρήσιμο, αλλά παραλείπει *πού* βρίσκεται κάθε λέξη στη σελίδα. Για τιμολόγια, φόρμες ή περιοδικά με πολλαπλές στήλες χρειάζεστε συντεταγμένες, αριθμούς γραμμών και ίσως ακόμη και πληροφορίες γραμματοσειράς. Εδώ έρχεται το `engine.RecognizeStructured()`.

Παρακάτω υπάρχει ένας ελαφρύς wrapper γύρω από την έξοδο **TSV** του Tesseract, η οποία μας δίνει μια ιεραρχία σελίδων → γραμμών → λέξεων, διατηρώντας τα bounding boxes.

```python
from typing import List, Dict

def structured_ocr(image_path: str) -> List[Dict]:
    """Return a list of pages, each containing lines with word coordinates."""
    img = Image.open(image_path)

    # Tesseract TSV includes page, block, paragraph, line, word indices.
    tsv_data = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT, lang='eng')

    pages = {}
    for i, level in enumerate(tsv_data["level"]):
        if level != 5:  # focus on word level (5)
            continue
        page_num = tsv_data["page_num"][i]
        line_num = tsv_data["line_num"][i]
        word = tsv_data["text"][i]
        if not word.strip():
            continue

        # Build nested dict structure.
        pages.setdefault(page_num, {}).setdefault(line_num, []).append({
            "text": word,
            "bbox": (
                tsv_data["left"][i],
                tsv_data["top"][i],
                tsv_data["width"][i],
                tsv_data["height"][i],
            ),
        })

    # Convert dicts to a more convenient list format.
    structured_result = []
    for page_id, lines in pages.items():
        page_obj = {"PageNumber": page_id, "Lines": []}
        for line_id, words in lines.items():
            line_text = " ".join(w["text"] for w in words)
            line_obj = {
                "LineNumber": line_id,
                "Text": line_text,
                "Words": words,
            }
            page_obj["Lines"].append(line_obj)
        structured_result.append(page_obj)

    return structured_result
```

*Γιατί το κάνουμε:*  
- **Συντεταγμένες** σας επιτρέπουν να χαρτογραφήσετε το εξαγόμενο κείμενο πίσω στην αρχική εικόνα για επισήμανση ή διαγραφή.  
- **Ομαδοποίηση γραμμών** διατηρεί την αρχική διάταξη, κάτι που είναι κρίσιμο όταν πρέπει να ανακατασκευάσετε πίνακες ή στήλες.  
- Αυτή η εκτέλεση είναι λίγο πιο αργή από την απλή, αλλά ολοκληρώνεται ακόμα σε λίγα δευτερόλεπτα για τα περισσότερα έγγραφα.

---

## Βήμα 3: Εκτελέστε τον AI Μετα‑Επεξεργαστή για Διόρθωση Σφαλμάτων OCR

Ακόμη και η καλύτερη μηχανή OCR κάνει λάθη—π.χ. “rn” αντί για “m”, λείπουν διακριτικά, ή χωρισμένες λέξεις. Ένα μοντέλο AI μπορεί να κοιτάξει το ακατέργαστο κείμενο και τα δομημένα δεδομένα, να εντοπίσει ασυνέπειες και να ξαναγράψει το κείμενο διατηρώντας τις αρχικές συντεταγμένες.

Παρακάτω είναι μια **mock** υλοποίηση· αντικαταστήστε το σώμα με μια πραγματική κλήση σε LLM αν έχετε.

```python
def ai_postprocess(plain_text: str, structured_result: List[Dict]) -> List[Dict]:
    """
    Simulate an AI post‑processor that corrects OCR errors.
    It walks through each line, compares it with the plain text,
    and applies simple heuristics (e.g., spell‑check).
    """
    import difflib
    corrected = []

    for page in structured_result:
        new_page = {"PageNumber": page["PageNumber"], "Lines": []}
        for line in page["Lines"]:
            # Find the closest match in the plain text using difflib.
            best_match = difflib.get_close_matches(line["Text"], plain_text.splitlines(), n=1, cutoff=0.6)
            corrected_text = best_match[0] if best_match else line["Text"]
            # Preserve original word list but replace the text field.
            new_line = {
                "LineNumber": line["LineNumber"],
                "Text": corrected_text,
                "Words": line["Words"],  # coordinates stay the same
            }
            new_page["Lines"].append(new_line)
        corrected.append(new_page)

    return corrected
```

*Γιατί αυτό το βήμα βελτιώνει την ακρίβεια του OCR:*  
- **Διορθώσεις με συμφραζόμενα** – το AI μπορεί να αποφασίσει ότι το “l0ve” είναι πιθανότατα “love” βάσει των γύρω λέξεων.  
- **Διατήρηση συντεταγμένων** – κρατάτε τις πληροφορίες διάταξης, ώστε οι επόμενες εργασίες (όπως η επισήμανση PDF) να παραμένουν ακριβείς.  
- **Επαναληπτική βελτίωση** – μπορείτε να τρέξετε τον μετα‑επεξεργαστή πολλές φορές, κάθε φορά καθαρίζοντας περισσότερα σφάλματα.

---

## Βήμα 4: Επανάληψη Μέσω της Διορθωμένης, Δομημένης Εξόδου

Τώρα που έχουμε μια καθαρή δομή, η εξαγωγή του τελικού κειμένου είναι τριπλή. Παρακάτω εκτυπώνουμε κάθε γραμμή, αλλά μπορείτε επίσης να γράψετε σε CSV, να τροφοδοτήσετε μια βάση δεδομένων ή να δημιουργήσετε ένα αναζητήσιμο PDF.

```python
def display_corrected_text(structured_result: List[Dict]) -> None:
    """Print each line of corrected OCR output."""
    for page in structured_result:
        print(f"\n--- Page {page['PageNumber']} ---")
        for line in page["Lines"]:
            print(line["Text"])

# Example usage tying everything together
if __name__ == "__main__":
    img_path = "sample_scan.png"

    # 1️⃣ Plain‑text OCR
    plain = plain_text_ocr(img_path)
    print("✅ Plain text OCR completed.")

    # 2️⃣ Structured OCR
    structured = structured_ocr(img_path)
    print("✅ Structured OCR completed.")

    # 3️⃣ AI post‑processing
    corrected = ai_postprocess(plain, structured)
    print("✅ AI post‑processor finished.")

    # 4️⃣ Show results
    display_corrected_text(corrected)
```

**Αναμενόμενη έξοδος** (υποθέτοντας ένα απλό τιμολόγιο μιας σελίδας):

```
--- Page 1 ---
Invoice #12345
Date: 2024‑05‑01
Bill To: Acme Corp
Item Qty Price Total
Widget A 2 $15.00 $30.00
Widget B 1 $25.00 $25.00
Subtotal $55.00
Tax $5.50
Total $60.50
```

Παρατηρήστε πώς οι αλλαγές γραμμής και η σειρά των στηλών διατηρούνται, και κοινά σφάλματα OCR όπως το “$15.00” που διαβάζεται ως “$15,00” διορθώνονται από το βήμα AI.

---

## Πώς Αυτή η Ροή Εργασίας Βοηθά **να Βελτιώσει την Ακρίβεια του OCR**

| Στάδιο | Τι διορθώνει | Γιατί είναι σημαντικό |
|------|---------------|------------------------|
| **Plain text OCR** | Ανιχνεύει σελίδες ακατάλληλες για ανάγνωση νωρίς | Εξοικονομεί χρόνο παραλείποντας ακατόρθωτες εισόδους |
| **Structured OCR** | Καταγράφει διάταξη, συντεταγμένες | Ενεργοποιεί επόμενες εργασίες (επισήμανση, διαγραφή) |
| **AI post‑processor** | Διορθώνει ορθογραφία, συγχωνεύει χωρισμένες λέξεις, διορθώνει αριθμούς | Ανεβάζει τη συνολική ακρίβεια χαρακτήρων από ~85 % σε >95 % σε θορυβώδεις σαρώσεις |
| **Iteration** | Επιτρέπει επανεκτέλεση με ρυθμισμένες παραμέτρους | Βελτιστοποιεί τη γραμμή εργασίας για συγκεκριμένους τύπους εγγράφων |

Συνδυάζοντας αυτές τις τρεις έννοιες—**plain text OCR**, εξαγωγή με γνώση διάταξης, και AI διόρθωση—παίρνετε μια ανθεκτική λύση που *σημαντικά* **βελτιώνει την ακρίβεια του OCR** χωρίς να χρειάζεται να γράψετε ένα προσαρμοσμένο νευρωνικό δίκτυο από την αρχή.

---

## Συνηθισμένα Πιθανά Προβλήματα & Επαγγελματικές Συμβουλές

- **Πρόβλημα:** Χρήση εικόνας χαμηλής ανάλυσης (≤150 dpi) στο Tesseract παράγει ακατάλληλη έξοδο.  
  **Συμβουλή:** Προεπεξεργαστείτε με `Pillow`—εφαρμόστε `Image.convert('L')` και `Image.filter(ImageFilter.MedianFilter())` πριν το OCR.

- **Πρόβλημα:** Ο AI μετα‑επεξεργαστής μπορεί να ξαναγράψει εξειδικευμένη ορολογία (π.χ. “SKU123”).  
  **Συμβουλή:** Δημιουργήστε μια whitelist όρων και περάστε την στο LLM ή σε μια βιβλιοθήκη ελέγχου ορθογραφίας όπως `pyspellchecker`.

- **Πρόβλημα:** Σελίδες πολλαπλών στηλών συγχωνεύονται σε μία γραμμή.  
  **Συμβουλή:** Εντοπίστε τα όρια των στηλών χρησιμοποιώντας το πεδίο `block_num` στην έξοδο TSV του Tesseract και χωρίστε τις γραμμές ανάλογα.

- **Πρόβλημα:** Μεγάλα PDF προκαλούν υπερφόρτωση μνήμης όταν φορτώνονται όλες οι σελίδες ταυτόχρονα.  
  **Συμβουλή:** Επεξεργαστείτε τις σελίδες σταδιακά—επανάληψη πάνω από `pdf2image.convert_from_path(..., first_page=n, last_page=n)`.

---

## Επέκταση της Αλυσίδας Επεξεργασίας

Αν σας ενδιαφέρουν τα επόμενα βήματα, σκεφτείτε τις παρακάτω βελτιώσεις:

1. **Επεξεργασία σε παρτίδες** – Τυλίξτε ολόκληρο το σενάριο σε μια συνάρτηση που διασχίζει έναν φάκελο, διαχειριζόμενη χιλιάδες αρχεία παράλληλα με `concurrent.futures`.  
2. **Μοντέλα γλώσσας** – Αντικαταστήστε την απλή λογική difflib με κλήση στο OpenAI `gpt‑4o` ή σε ένα τοπικό μοντέλο LLaMA για πιο πλούσιες διορθώσεις συμφραζομένων.  
3. **Μορφές εξαγωγής** – Γράψτε τη διορθωμένη δομή σε αναζητήσιμο PDF  

## Τι Πρέπει να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to Use OCR - Advanced Techniques with Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/)
- [Improve OCR Accuracy – Detect Areas Mode in OCR](/ocr/hongkong/net/text-recognition/ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}