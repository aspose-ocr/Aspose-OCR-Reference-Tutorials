---
category: general
date: 2026-06-25
description: Εξαγωγή κειμένου PDF με OCR χρησιμοποιώντας Python. Μάθετε πώς να μετατρέπετε
  PDF σε κείμενο με ένα σαφές παράδειγμα OCR σε Python και να λαμβάνετε αξιόπιστα
  αποτελέσματα γρήγορα.
draft: false
keywords:
- extract pdf text OCR
- convert pdf to text
- python ocr example
- Aspose OCR Python
- multi‑page PDF OCR
language: el
og_description: Εξαγωγή κειμένου PDF με OCR σε Python. Αυτός ο οδηγός δείχνει ένα
  παράδειγμα OCR σε Python που μετατρέπει PDF σε κείμενο, διαχειριζόμενο έγγραφα πολλαπλών
  σελίδων άψογα.
og_title: Εξαγωγή κειμένου PDF με OCR σε Python – Πλήρης προγραμματιστικός οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract PDF text OCR using Python. Learn how to convert PDF to text
    with a clear python OCR example and get reliable results fast.
  headline: Extract PDF Text OCR in Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: Εξαγωγή κειμένου PDF με OCR σε Python – Πλήρης οδηγός βήμα‑προς‑βήμα
url: /el/python-java/general/extract-pdf-text-ocr-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή κειμένου PDF OCR σε Python – Πλήρης Οδηγός Βήμα‑βήμα

Έχετε χρειαστεί ποτέ να **εξάγετε κείμενο pdf OCR** αλλά δεν ήξερες ποια βιβλιοθήκη μπορεί να διαχειριστεί PDF πολλαπλών σελίδων χωρίς προβλήματα; Δεν είστε μόνοι. Σε πολλά πραγματικά έργα — σκεφτείτε νομικά συμβόλαια, σαρωμένα τιμολόγια ή αρχειοθετημένες αναφορές — η λήψη καθαρού, αναζητήσιμου κειμένου από ένα PDF είναι απαραίτητη δεξιότητα.

Σε αυτό το tutorial θα περάσουμε από ένα **python ocr example** που **convert pdf to text** χρησιμοποιώντας το Aspose.OCR. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση script που εξάγει το κείμενο από κάθε σελίδα, εμφανίζει προεπισκόπηση και ακόμη αποθηκεύει ολόκληρο το έγγραφο ως ένα ενιαίο αρχείο `.txt`. Χωρίς περιττές πληροφορίες, μόνο μια πρακτική λύση που μπορείτε να ενσωματώσετε στον κώδικά σας σήμερα.

## Τι Θα Μάθετε

- Πώς να εγκαταστήσετε και να εισάγετε το module Aspose OCR για Python.  
- Πώς να δημιουργήσετε μια παρουσία OCR engine και να εκτελέσετε **extract pdf text OCR** σε PDF πολλαπλών σελίδων.  
- Τρόπους για να επαναλάβετε το αποτέλεσμα κάθε σελίδας, να εμφανίσετε προεπισκόπηση και να γράψετε το πλήρες αποτέλεσμα στο δίσκο.  
- Συμβουλές για την αντιμετώπιση κοινών προβλημάτων όπως κενές σελίδες ή χαρακτήρες Unicode.  

> **Προαπαιτούμενα:** Python 3.8+ εγκατεστημένο, βασική εξοικείωση με pip, και ένα αρχείο PDF που θέλετε να επεξεργαστείτε. Δεν απαιτείται προηγούμενη εμπειρία OCR.

---

![Extract PDF Text OCR workflow diagram](extract-pdf-text-ocr.png "Diagram of extract pdf text OCR process")

*Alt text: Διάγραμμα που απεικονίζει τη ροή εργασίας extract pdf text OCR σε Python.*

## Βήμα 1: Εγκατάσταση Aspose OCR για Python

Πριν τρέξει οποιοσδήποτε κώδικας, χρειάζεστε το πακέτο Aspose.OCR. Διανέμεται μέσω PyPI, οπότε μια εντολή pip αρκεί.

```bash
pip install aspose-ocr
```

> **Pro tip:** Αν εργάζεστε μέσα σε εικονικό περιβάλλον (συνετά προτεινόμενο), ενεργοποιήστε το πρώτα για να διατηρήσετε τις εξαρτήσεις απομονωμένες.

## Βήμα 2: Εισαγωγή του Module και Δημιουργία του OCR Engine

Τώρα που η βιβλιοθήκη είναι διαθέσιμη, εισάγετε την και δημιουργήστε ένα `OcrEngine`. Σκεφτείτε το engine ως τον εγκέφαλο που κάνει όλη τη βαριά δουλειά — αναγνώριση χαρακτήρων, διαχείριση διατάξεων σελίδας και επιστροφή καθαρών συμβολοσειρών Unicode.

```python
# Step 2: Import the Aspose OCR module and create an engine
import aspose.ocr as ocr

engine = ocr.OcrEngine()
```

> **Why this matters:** Η δημιουργία μιας μόνο παρουσίας του engine και η επαναχρησιμοποίησή του σε όλες τις σελίδες είναι πολύ πιο αποδοτική από το να δημιουργείτε νέο engine ανά σελίδα. Επίσης εξασφαλίζει συνεπείς ρυθμίσεις σε όλο το έγγραφο.

## Βήμα 3: Αναγνώριση Όλων των Σελίδων ενός PDF (Multi‑Page OCR)

Η μέθοδος `recognize_multi_page` του Aspose.OCR δέχεται διαδρομή αρχείου και επιστρέφει μια λίστα αντικειμένων `OcrResult` — ένα ανά σελίδα. Αυτό αποτελεί τον πυρήνα της λειτουργίας **convert pdf to text**.

```python
# Step 3: Run OCR on every page of the PDF
pdf_path = "YOUR_DIRECTORY/contract.pdf"   # replace with your actual file
pdf_pages = engine.recognize_multi_page(pdf_path)  # returns List[OcrResult]
```

> **Edge case:** Αν το PDF είναι προστατευμένο με κωδικό, πρέπει να περάσετε τον κωδικό μέσω `engine.set_password("your_password")` πριν καλέσετε το `recognize_multi_page`.

## Βήμα 4: Επανάληψη στα Αποτελέσματα και Εμφάνιση Προεπισκόπησης

Μια γρήγορη προεπισκόπηση σας βοηθά να επαληθεύσετε ότι το OCR εντοπίζει πραγματικά κείμενο. Θα εκτυπώσουμε τους πρώτους 200 χαρακτήρες κάθε σελίδας, αλλά μπορείτε να προσαρμόσετε το τμήμα όπως χρειάζεται.

```python
# Step 4: Display a short preview of each page’s extracted text
for page_number, page_result in enumerate(pdf_pages, start=1):
    print(f"--- Page {page_number} ---")
    # Show the first 200 characters of the page's OCR text
    print(page_result.text[:200])
    print()  # blank line for readability
```

**Δείγμα εξόδου**

```
--- Page 1 ---
This Agreement is made on the 1st day of January 2025 between ...

--- Page 2 ---
WHEREAS, the Parties desire to enter into a collaborative ...

--- Page 3 ---
IN WITNESS WHEREOF, the Parties have executed this Agreement ...
```

Το παραπάνω δείχνει μόνο ένα απόσπασμα, αλλά το πλήρες κείμενο βρίσκεται μέσα στο `page_result.text`.

## Βήμα 5: Συγχώνευση Όλων των Σελίδων σε Ένα Αρχείο Κειμένου (Προαιρετικό)

Οι περισσότερες επακόλουθες ροές εργασίας — ευρετηρίαση αναζήτησης, ανάλυση δεδομένων ή απλή αρχειοθέτηση — προτιμούν ένα ενιαίο αρχείο `.txt`. Ας ενωσουμε τις σελίδες και ας το γράψουμε στο δίσκο.

```python
# Step 5: Save the complete OCR output to a .txt file
output_path = "YOUR_DIRECTORY/contract_extracted.txt"

with open(output_path, "w", encoding="utf-8") as out_file:
    for page_result in pdf_pages:
        out_file.write(page_result.text)
        out_file.write("\n\n")  # separate pages with a blank line
print(f"All pages saved to {output_path}")
```

> **Why this works:** Η χρήση UTF‑8 εξασφαλίζει ότι δεν θα χάσετε ειδικούς χαρακτήρες όπως τονισμένα γράμματα ή σύμβολα που εμφανίζονται συχνά σε νομικά έγγραφα.

## Βήμα 6: Αντιμετώπιση Συνηθισμένων Προβλημάτων

| Πρόβλημα | Συμπτωμα | Διόρθωση |
|----------|----------|----------|
| Κενές σελίδες στο αποτέλεσμα | `page_result.text` είναι κενό | Επαληθεύστε ότι το PDF πηγαίο περιέχει σαρωμένες εικόνες· κάποια PDFs είναι ήδη κειμενικά και μπορεί να χρειάζονται διαφορετική προσέγγιση (π.χ. βιβλιοθήκες εξαγωγής κειμένου PDF). |
| Κατεστραμμένοι χαρακτήρες | Παράξενες συμβολοσειρές αντί για γράμματα | Βεβαιωθείτε ότι η γλώσσα του OCR engine είναι σωστή: `engine.language = ocr.Language.English` (ή άλλη γλώσσα). |
| Μεγάλα PDFs που παίρνουν πολύ χρόνο | Το script φαίνεται να κολλάει σε μια σελίδα | Ενεργοποιήστε πολυνηματική εκτέλεση: `engine.recognize_multi_page(pdf_path, ocr.RecognizeOptions(parallel=True))`. |
| Σφάλματα μνήμης σε τεράστια αρχεία | Σφάλμα `MemoryError` | Επεξεργαστείτε το PDF σε τμήματα (π.χ. 50 σελίδες τη φορά) ή αυξήστε το όριο μνήμης του Python. |

## Πλήρες Script – Έτοιμο για Εκτέλεση

Συνδυάζοντας τα παραπάνω, εδώ είναι το ολοκληρωμένο, αυτόνομο script που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα αρχείο με όνομα `extract_pdf_text_ocr.py`.

```python
# extract_pdf_text_ocr.py
# Complete python ocr example that extracts PDF text using Aspose OCR.

import aspose.ocr as ocr

def main():
    # 1️⃣ Install the library via `pip install aspose-ocr` before running.
    # 2️⃣ Set the path to your PDF.
    pdf_path = "YOUR_DIRECTORY/contract.pdf"
    output_path = "YOUR_DIRECTORY/contract_extracted.txt"

    # 3️⃣ Create the OCR engine.
    engine = ocr.OcrEngine()
    # Optional: set language for better accuracy.
    # engine.language = ocr.Language.English

    # 4️⃣ Perform multi‑page OCR.
    pdf_pages = engine.recognize_multi_page(pdf_path)

    # 5️⃣ Show a preview of each page.
    for page_number, page_result in enumerate(pdf_pages, start=1):
        print(f"--- Page {page_number} ---")
        print(page_result.text[:200])
        print()

    # 6️⃣ Write the full text to a file.
    with open(output_path, "w", encoding="utf-8") as out_file:
        for page_result in pdf_pages:
            out_file.write(page_result.text)
            out_file.write("\n\n")
    print(f"✅ All pages saved to {output_path}")

if __name__ == "__main__":
    main()
```

Τρέξτε το από το τερματικό σας:

```bash
python extract_pdf_text_ocr.py
```

Θα πρέπει να δείτε τις προεπισκοπήσεις των σελίδων στην κονσόλα, ακολουθούμενες από επιβεβαίωση ότι το πλήρες κείμενο αποθηκεύτηκε.

## Ανακεφαλαίωση & Επόμενα Βήματα

Δείξαμε πώς να **extract pdf text OCR** χρησιμοποιώντας ένα σύντομο **python ocr example** που **convert pdf to text** αποδοτικά. Τα βασικά βήματα — εγκατάσταση, εισαγωγή, δημιουργία engine, εκτέλεση `recognize_multi_page`, προεπισκόπηση και αποθήκευση — καλύπτουν τη πιο κοινή ροή εργασίας για σαρωμένα PDFs.

**Τι ακολουθεί;**  

- **Βελτιστοποίηση ακρίβειας**: Πειραματιστείτε με `engine.recognize_multi_page(..., RecognizeOptions(...))` για να ρυθμίσετε DPI ή να χρησιμοποιήσετε πακέτα γλώσσας.  
- **Μετα-επεξεργασία**: Αφαιρέστε περιττά κενά, τρέξτε ορθογραφικό έλεγχο ή τροφοδοτήστε το κείμενο σε pipeline φυσικής γλώσσας.  
- **Επεξεργασία παρτίδας**: Επανάληψη σε φάκελο PDFs για δημιουργία αναζητήσιμου αρχείου.  

Αν αντιμετωπίσετε προβλήματα, ελέγξτε ξανά ότι το PDF περιέχει ραστερ εικόνες (το OCR λειτουργεί σε εικόνες, όχι σε ενσωματωμένο κείμενο). Για PDFs που ήδη περιέχουν κείμενο, σκεφτείτε βιβλιοθήκες όπως `pdfminer.six` ή `PyMuPDF`.

---

**Καλή προγραμματιστική!** Αν αυτός ο οδηγός σας βοήθησε να **extract pdf text OCR** για το έργο σας, μοιραστείτε τα αποτελέσματά σας στα σχόλια ή ανοίξτε ένα issue στη σελίδα του Aspose OCR στο GitHub για αιτήματα χαρακτηριστικών. Συνεχίστε να πειραματίζεστε και σύντομα θα έχετε μια ισχυρή αλυσίδα που μετατρέπει οποιοδήποτε σαρωμένο PDF σε αναζητήσιμο, επεξεργάσιμο κείμενο.

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}