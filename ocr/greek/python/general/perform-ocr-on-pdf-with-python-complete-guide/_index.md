---
category: general
date: 2026-06-25
description: Εκτελέστε OCR σε PDF χρησιμοποιώντας Python—μάθετε πώς να φορτώνετε PDF
  για OCR, να εξάγετε κείμενο από τις σελίδες PDF και να προβάλλετε το αναγνωρισμένο
  κείμενο αποδοτικά.
draft: false
keywords:
- perform OCR on PDF
- extract text from PDF pages
- load PDF for OCR
- how to OCR large PDF
- preview recognized text
language: el
og_description: Εκτελέστε OCR σε PDF με Python. Αυτός ο οδηγός δείχνει πώς να φορτώσετε
  PDF για OCR, να εξάγετε κείμενο από τις σελίδες PDF και να προβάλετε γρήγορα το
  αναγνωρισμένο κείμενο.
og_title: Εκτελέστε OCR σε PDF με Python – Βήμα‑βήμα Εγχειρίδιο
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  headline: Perform OCR on PDF with Python – Complete Guide
  type: TechArticle
- description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  name: Perform OCR on PDF with Python – Complete Guide
  steps:
  - name: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
    text: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
  - name: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
    text: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
  - name: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
    text: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
  - name: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
    text: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: Διενέργεια OCR σε PDF με Python – Πλήρης Οδηγός
url: /el/python/general/perform-ocr-on-pdf-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτελέστε OCR σε PDF με Python – Πλήρης Οδηγός

Κάποτε χρειάστηκε να **εκτελέσετε OCR σε PDF** αρχεία αλλά δεν ήξερες από πού να ξεκινήσεις; Ίσως έχεις ένα βουνό σαρωμένων συμβάσεων, ή ένα μόνο τεράστιο εγχειρίδιο που αρνείται να συνεργαστεί με τον συνηθισμένο εξαγωγέα κειμένου. Συνοπτικά, θέλεις να **φορτώσεις PDF για OCR**, να εξάγεις το κείμενο και να πάρεις μια γρήγορη προεπισκόπηση—όλα χωρίς να εξαντλήσεις τη μνήμη του υπολογιστή σου.

Λοιπόν, βρίσκεσαι στο σωστό μέρος. Σε αυτό το tutorial θα περάσουμε από ένα πλήρως λειτουργικό script Python που **εξάγει κείμενο από σελίδες PDF**, δείχνει πώς να **προεπισκοπήσεις το αναγνωρισμένο κείμενο**, και ακόμη αντιμετωπίζει το κλασικό πρόβλημα του **πώς να κάνετε OCR σε μεγάλα PDF** αρχεία αποδοτικά.

Στο τέλος θα έχεις ένα έτοιμο προς εκτέλεση πρόγραμμα, μια σαφή κατανόηση κάθε ρυθμιστικού παραμέτρου, και μια σειρά συμβουλών για να αποφύγεις τα κοινά εμπόδια που παγιδεύουν τους αρχάριους.

---

## Τι Θα Μάθετε

- Πώς να **φορτώσετε PDF για OCR** χρησιμοποιώντας τη βιβλιοθήκη `aocr`.
- Τα ακριβή βήματα για **εκτέλεση OCR σε PDF** σελίδες μία‑μια.
- Τρόπους για **εξαγωγή κειμένου από σελίδες PDF** διατηρώντας τη χρήση μνήμης υπό έλεγχο.
- Πώς να **προεπισκοπήσετε το αναγνωρισμένο κείμενο** για έλεγχο των αποτελεσμάτων.
- Στρατηγικές για διαχείριση **μεγάλων PDF** χωρίς εξάντληση RAM.

> **Συμβουλή:** Αυτός ο οδηγός υποθέτει ότι έχετε εγκατεστημένο το Python 3.9+ και βασική εξοικείωση με εικονικά περιβάλλοντα. Αν είστε νέοι στο Python, δημιουργήστε πρώτα ένα virtualenv—σας εξοικονομεί πολλή κόπωση αργότερα.

---

## Προαπαιτήσεις

| Απαίτηση | Γιατί είναι σημαντική |
|-------------|----------------|
| Πακέτο Python `aocr` (ή οποιοδήποτε συμβατό OCR engine) | Παρέχει την κλάση `OcrEngine` που χρησιμοποιείται σε όλο το script. |
| `pip` και εικονικό περιβάλλον | Κρατά τις εξαρτήσεις απομονωμένες από το σύστημα Python. |
| Αρκετός ελεύθερος χώρος δίσκου για προσωρινές εξαγωγές εικόνας | Κάποια OCR engines γράφουν εικόνες σελίδας στο δίσκο πριν την επεξεργασία. |
| Προαιρετικό: `tqdm` για μπαρ προόδου | Βελτιώνει την εμπειρία χρήστη όταν αντιμετωπίζετε **πώς να κάνετε OCR σε μεγάλα PDF**. |

Εγκαταστήστε τα απαραίτητα με:

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate
pip install aocr tqdm
```

Αν το PDF σας είναι προστατευμένο με κωδικό, θα χρειαστεί να δώσετε τον κωδικό αργότερα—δείτε την ενότητα «Edge Cases».

---

## Βήμα 1: Εκτέλεση OCR σε PDF – Ρύθμιση του Engine

Πρώτα απ’ όλα, χρειαζόμαστε μια παρουσία OCR engine. Σκεφτείτε το ως τον εγκέφαλο που θα διαβάσει την εικόνα κάθε σελίδας και θα εκτυπώσει απλό κείμενο.

```python
import aocr                     # The OCR library
from tqdm import tqdm           # Optional, for a nice progress bar

def create_engine():
    """
    Initialise the OcrEngine with sensible defaults.
    Returns the configured engine ready for processing.
    """
    engine = aocr.OcrEngine()
    # Limit memory usage – crucial when tackling how to OCR large PDF files
    engine.max_memory_mb = 200               # 200 MB cap, adjust if needed
    # Choose a recognition mode that matches your source material
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine
```

> **Γιατί να ορίσετε `max_memory_mb`;**  
> Τα OCR engines συχνά αποθηκεύουν εικόνες σελίδων στη RAM. Με το όριο μνήμης αποτρέπετε το σενάριό σας από κατάρρευση σε ένα συμβόλαιο 500 σελίδων.

---

## Βήμα 2: Φόρτωση PDF για OCR και Διαμόρφωση Ρυθμίσεων

Τώρα φορτώνουμε πραγματικά το **PDF για OCR**. Η διαδρομή μπορεί να είναι απόλυτη ή σχετική· απλώς βεβαιωθείτε ότι το αρχείο υπάρχει.

```python
def load_pdf(engine, pdf_path):
    """
    Loads the PDF into the OCR engine.
    Raises FileNotFoundError if the file does not exist.
    """
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages ready.")
    except Exception as e:
        raise RuntimeError(f"Failed to load PDF: {e}")
```

Αν το PDF είναι κρυπτογραφημένο, το `engine.load_pdf` συνήθως θα ρίξει εξαίρεση. Σε αυτήν την περίπτωση μπορείτε να καλέσετε `engine.load_pdf(pdf_path, password="secret")`—περισσότερα αργότερα.

---

## Βήμα 3: Εξαγωγή Κειμένου από Σελίδες PDF – Ο Κύριος Βρόχος

Εδώ είναι που **εκτελούμε OCR σε PDF** σελίδα προς σελίδα. Θα **προεπισκοπήσουμε το αναγνωρισμένο κείμενο** για τους πρώτους μερικούς εκατοντάδες χαρακτήρες ώστε να επαληθεύσετε ότι όλα λειτουργούν.

```python
def ocr_pages(engine, preview_len=200):
    """
    Iterates over each page, runs OCR, and yields the recognized text.
    Also prints a short preview for each page.
    """
    for page_index in tqdm(range(engine.page_count), desc="Processing pages"):
        # Select the current page – essential for multi‑page PDFs
        engine.select_page(page_index)

        # Perform the actual OCR
        page_text = engine.recognize()

        # Preview the first `preview_len` characters (helps with debugging)
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))

        yield page_text
```

> **Pro tip:** Η μπάρα προόδου `tqdm` σας δίνει οπτική ένδειξη, ιδιαίτερα χρήσιμη όταν επεξεργάζεστε **πώς να κάνετε OCR σε μεγάλα PDF** έγγραφα που απαιτούν λεπτά για επεξεργασία.

---

## Βήμα 4: Όλα Μαζί – Ένα Έτοιμο‑για‑Εκτέλεση Script

Παρακάτω είναι το πλήρες, εκτελέσιμο παράδειγμα. Αποθηκεύστε το ως `pdf_ocr.py` και τρέξτε το με `python pdf_ocr.py path/to/your/file.pdf`.

```python
#!/usr/bin/env python3
"""
Complete script to perform OCR on PDF, extract text from PDF pages,
and preview recognized text. Works for both small and large PDFs.
"""

import sys
import aocr
from tqdm import tqdm

def create_engine():
    engine = aocr.OcrEngine()
    engine.max_memory_mb = 200
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine

def load_pdf(engine, pdf_path):
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages.")
    except Exception as exc:
        raise RuntimeError(f"Unable to load PDF: {exc}")

def ocr_pages(engine, preview_len=200):
    for page_index in tqdm(range(engine.page_count), desc="OCR progress"):
        engine.select_page(page_index)
        page_text = engine.recognize()
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))
        yield page_text

def main(pdf_path):
    engine = create_engine()
    load_pdf(engine, pdf_path)

    all_text = []
    for txt in ocr_pages(engine):
        all_text.append(txt)

    # Optional: write the combined output to a .txt file
    out_path = pdf_path.rsplit(".", 1)[0] + "_ocr.txt"
    with open(out_path, "w", encoding="utf-8") as f:
        f.write("\n\n".join(all_text))
    print(f"\n✅ OCR complete. Full text saved to: {out_path}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python pdf_ocr.py <path_to_pdf>")
        sys.exit(1)
    pdf_file = sys.argv[1]
    main(pdf_file)
```

### Αναμενόμενο Αποτέλεσμα (απόσπασμα)

```
✅ Loaded 'large_contract.pdf' – 342 pages.

--- Page 1 Preview ---
Contract Agreement between Party A and Party B ... 

--- Page 2 Preview ---
Recitals: Whereas, the parties desire to ...

...
✅ OCR complete. Full text saved to: large_contract_ocr.txt
```

Θα δείτε μια σύντομη προεπισκόπηση για κάθε σελίδα, ακολουθούμενη από τελική επιβεβαίωση ότι το συγκεντρωτικό αρχείο κειμένου έχει γραφτεί.

---

## Edge Cases & Practical Tips

| Κατάσταση | Τι να Κάνετε |
|-----------|------------|
| **Κρυπτογραφημένο PDF** | Δώστε τον κωδικό: `engine.load_pdf(pdf_path, password="mySecret")`. |
| **Πολύ μεγάλο PDF (> 1000 σελίδες)** | Αυξήστε το `max_memory_mb` με προσοχή, ή επεξεργαστείτε σε τμήματα (π.χ., 200 σελίδες τη φορά). |
| **Μικτό περιεχόμενο (εκτυπωμένο + χειρόγραφο)** | Αλλάξτε το `engine.recognition_mode` σε `aocr.RecognitionMode.MIXED` αν η βιβλιοθήκη το υποστηρίζει. |
| **Λείπουν γραμματοσειρές ή χαμηλή ποιότητα σάρωσης** | Προεπεξεργαστείτε τις σελίδες με βιβλιοθήκη βελτίωσης εικόνας (π.χ., Pillow) πριν καλέσετε `recognize()`. |
| **Καταρρεύσεις εξαιτίας έλλειψης μνήμης** | Μειώστε το `preview_len` ή γράψτε το κείμενο κάθε σελίδας απευθείας στο δίσκο αντί να το κρατάτε όλα σε λίστα. |

---

## Πώς να Κάνετε OCR σε Μεγάλα PDF Αποδοτικά – Προχωρημένες Στρατηγικές

Όταν αντιμετωπίζετε **πώς να κάνετε OCR σε μεγάλα PDF**, η ταχύτητα και η σταθερότητα γίνονται κρίσιμες. Εδώ είναι μερικά κόλπα που μπορείτε να ενσωματώσετε στο script:

1. **Παράλληλη επεξεργασία ανά σελίδα** – Χρησιμοποιήστε `concurrent.futures.ThreadPoolExecutor` αν το OCR engine είναι thread‑safe.
2. **Αποθήκευση ενδιάμεσων εικόνων** – Κάποια engines επιτρέπουν την αποθήκευση ραστερισμένων σελίδων σε SSD, μειώνοντας δραστικά το φορτίο CPU σε επανεκτελέσεις.
3. **Ομαδική εγγραφή εξόδου** – Αντί να προσθέτετε σε λίστα Python, ανοίξτε το αρχείο εξόδου μία φορά και γράψτε το κείμενο κάθε σελίδας μόλις είναι έτοιμο.
4. **Ρύθμιση DPI** – Η μείωση του DPI κατά τη ραστεροποίηση μειώνει τη μνήμη αλλά μπορεί να επηρεάσει την ακρίβεια· βρείτε το «sweet spot» (συνήθως 200‑300 DPI).

Παρακάτω ένα γρήγορο απόσπασμα που δείχνει πώς μπορείτε να παραλληλοποιήσετε το βήμα OCR (προαιρετικό, αποσχολιάστε για χρήση):

```python
# from concurrent.futures import ThreadPoolExecutor

# def ocr_page(engine, idx):
#     engine.select_page(idx)
#     return engine.recognize()

# with ThreadPoolExecutor(max_workers=4) as executor:
#     results = list(tqdm(executor.map(lambda i: ocr_page(engine, i),
#                                    range(engine.page_count)),
#                     total=engine.page_count,
#                     desc="Parallel OCR"))
```

Θυμηθείτε: η παραλληλοποίηση μπορεί να αυξήσει τη χρήση CPU, επομένως παρακολουθείτε τη θερμοκρασία του συστήματός σας σε μεγάλες εκτελέσεις.

---

## Συχνές Ερωτήσεις

**Ε: Μπορώ να χρησιμοποιήσω αυτό το script με άλλες βιβλιοθήκες OCR όπως το Tesseract;**  
Α: Απόλυτα. Αντικαταστήστε τις κλήσεις `aocr` με `pytesseract.image_to

## Τι Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κυριαρχήσετε επιπλέον χαρακτηριστικά API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να κάνετε OCR PDF σε .NET με Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Πώς να Εκτελέσετε Εξαγωγή Κειμένου από Εικόνα από Stream Χρησιμοποιώντας Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Πώς να εξάγετε κείμενο από εικόνα από URL χρησιμοποιώντας Aspose.OCR για Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}