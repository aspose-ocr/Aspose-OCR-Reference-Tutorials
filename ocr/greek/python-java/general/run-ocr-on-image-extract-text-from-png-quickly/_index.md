---
category: general
date: 2026-03-18
description: Εκτελέστε OCR σε εικόνα για να εξάγετε κείμενο από PNG και να δημιουργήσετε
  αναζητήσιμο PDF. Μάθετε πώς να αναγνωρίζετε κείμενο σε εικόνα και να μετατρέπετε
  PNG σε PDF σε λίγα λεπτά.
draft: false
keywords:
- run OCR on image
- extract text from png
- recognize text image
- generate searchable pdf
- convert png to pdf
language: el
og_description: Εκτελέστε OCR στην εικόνα για να εξάγετε κείμενο από PNG, αναγνωρίστε
  το κείμενο της εικόνας και δημιουργήστε ένα αναζητήσιμο PDF. Ακολουθήστε αυτόν τον
  οδηγό βήμα‑βήμα.
og_title: Εκτελέστε OCR σε εικόνα – Εξαγάγετε κείμενο από PNG γρήγορα
tags:
- OCR
- Python
- Image Processing
title: Εκτέλεση OCR σε εικόνα – Γρήγορη εξαγωγή κειμένου από PNG
url: /el/python-java/general/run-ocr-on-image-extract-text-from-png-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε εικόνα – Εξαγωγή κειμένου από PNG γρήγορα

Έχετε ποτέ χρειαστεί να **run OCR on image** αρχεία αλλά δεν ήξερες από πού να ξεκινήσεις; Ίσως έχετε ένα σαρωμένο άρθρο αποθηκευμένο ως `article.png` και θέλετε απλώς το ακατέργαστο κείμενο, ή χρειάζεστε ένα αναζητήσιμο PDF για αρχειοθέτηση. Σε κάθε περίπτωση, βρίσκεστε στο σωστό μέρος. Σε αυτό το tutorial θα περάσουμε από την εξαγωγή κειμένου από PNG, την αναγνώριση της εικόνας κειμένου, και ακόμη τη μετατροπή του PNG σε αναζητήσιμο PDF—όλα με λίγες γραμμές κώδικα.

> **Τι θα λάβετε:** ένα πλήρες, εκτελέσιμο script που φορτώνει ένα PNG, εκτελεί OCR, αποθηκεύει το hOCR output, και προαιρετικά δημιουργεί ένα αναζητήσιμο PDF. Χωρίς ελλιπείς εισαγωγές, χωρίς “δείτε τα docs” αδιέξοδα—απλώς μια αυτόνομη λύση που μπορείτε να ενσωματώσετε στο πρότζεκτ σας σήμερα.

## Προαπαιτήσεις

- **Python 3.8+** (η σύνταξη που χρησιμοποιείται εδώ λειτουργεί σε οποιαδήποτε πρόσφατη έκδοση)
- Η βιβλιοθήκη **`ocr_engine`** που χρησιμοποιείτε (το παράδειγμα υποθέτει μια κλάση που ονομάζεται `OcrEngine`; αντικαταστήστε με Tesseract, EasyOCR κ.λπ., αν χρειάζεται)
- Μια εικόνα PNG που θέλετε να επεξεργαστείτε (π.χ. `article.png` τοποθετημένη σε φάκελο που μπορείτε να αναφέρετε)
- Δικαιώματα εγγραφής στον φάκελο εξόδου

Αν χρησιμοποιείτε το Tesseract στο παρασκήνιο, εγκαταστήστε το με:

```bash
# Ubuntu/Debian
sudo apt-get install tesseract-ocr

# macOS (Homebrew)
brew install tesseract
```

Και στη συνέχεια εγκαταστήστε το Python wrapper:

```bash
pip install pytesseract Pillow
```

*Συμβουλή:* διατηρήστε τη βιβλιοθήκη OCR ενημερωμένη—νέα πακέτα γλωσσών και βελτιώσεις απόδοσης κυκλοφορούν συχνά.

## Εκτέλεση OCR σε εικόνα – Οδηγός βήμα‑βήμα

Παρακάτω είναι το **πλήρες script**. Μπορείτε να το αντιγράψετε‑και‑επικολλήσετε σε ένα αρχείο με όνομα `run_ocr.py` και να το εκτελέσετε με `python run_ocr.py`.

```python
# run_ocr.py
import os
from pathlib import Path

# Import the OCR engine – replace with your actual import if different
# For Tesseract via pytesseract you would use: import pytesseract
# Here we assume a generic OcrEngine class that matches the example
from ocr_engine import OcrEngine  # <-- adjust as needed

def main():
    # ------------------------------------------------------------------
    # Step 1: Create an OCR engine instance
    # ------------------------------------------------------------------
    ocr_engine = OcrEngine()
    # Why this matters: the engine holds configuration (language, DPI, etc.)
    # You can tweak ocr_engine.setLanguage('eng') or similar before proceeding.

    # ------------------------------------------------------------------
    # Step 2: Load the image you want to process
    # ------------------------------------------------------------------
    image_path = Path("YOUR_DIRECTORY/article.png")
    if not image_path.is_file():
        raise FileNotFoundError(f"Image not found: {image_path}")
    ocr_engine.setImageFromFile(str(image_path))

    # ------------------------------------------------------------------
    # Step 3: Choose the export format
    # ------------------------------------------------------------------
    # hOCR preserves layout (bounding boxes, fonts) – perfect for searchable PDFs.
    # Other options: "txt", "pdf", "pdfa"
    ocr_engine.setExportFormat("hocr")

    # ------------------------------------------------------------------
    # Step 4: Run the recognition process
    # ------------------------------------------------------------------
    ocr_result = ocr_engine.recognize()
    # The result object gives us access to the raw OCR text, hOCR, etc.

    # ------------------------------------------------------------------
    # Step 5: Write the HOCR output to a file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/article.hocr")
    with open(output_path, "w", encoding="utf-8") as output_file:
        output_file.write(ocr_result.getExportedContent())
    print(f"✅ HOCR saved to {output_path}")

    # ------------------------------------------------------------------
    # Optional: Generate a searchable PDF from the HOCR
    # ------------------------------------------------------------------
    # Many OCR engines can bundle the original image with the hOCR to produce
    # a PDF that you can search. If your engine supports it, uncomment:
    # ocr_engine.setExportFormat("pdf")
    # pdf_result = ocr_engine.recognize()
    # pdf_path = Path("YOUR_DIRECTORY/article_searchable.pdf")
    # with open(pdf_path, "wb") as pdf_file:
    #     pdf_file.write(pdf_result.getExportedContent())
    # print(f"📄 Searchable PDF created at {pdf_path}")

if __name__ == "__main__":
    main()
```

### Τι κάνει το script, με απλά λόγια

1. **Instantiate** τη μηχανή OCR ώστε να μπορείτε να ελέγχετε τις ρυθμίσεις της.
2. **Load** το αρχείο PNG (`article.png`). Το script τερματίζει νωρίς αν το αρχείο δεν υπάρχει—χωρίς μυστηριώδεις σφάλματα `NoneType` αργότερα.
3. **Select** `hocr` ως μορφή εξαγωγής. Αυτή η μορφή διατηρεί τη αρχική διάταξη, η οποία είναι ουσιώδης για τη μετατροπή της εικόνας σε αναζητήσιμο PDF αργότερα.
4. **Run** τη μηχανή αναγνώρισης· εδώ γίνεται η βαριά δουλειά.
5. **Write** το hOCR XML στο `article.hocr`. Έχετε τώρα μια μηχανικά αναγνώσιμη αναπαράσταση του κειμένου και των συντεταγμένων του.
6. *(Optional)* Αλλάξτε σε `"pdf"` και δημιουργήστε ένα αναζητήσιμο PDF σε ένα επιπλέον βήμα.

Το **expected output** είναι ένα αρχείο `.hocr` κωδικοποιημένο σε UTF‑8 που φαίνεται κάπως έτσι (περιορισμένο για συντομία):

```xml
<div class='ocr_page' id='page_1' title='image "article.png"; bbox 0 0 2480 3508; ppageno 0'>
  <div class='ocr_carea' id='block_1_1' title="bbox 100 100 2400 3400">
    <p class='ocr_par' id='par_1' title="bbox 100 100 2400 200">
      <span class='ocr_line' id='line_1' title="bbox 100 100 2400 150; baseline 0 -5">
        <span class='ocrx_word' id='word_1' title="bbox 100 100 300 150; x_wconf 96">This</span>
        <span class='ocrx_word' id='word_2' title="bbox 310 100 500 150; x_wconf 92">is</span>
        …
```

Αν αφαιρέσετε το σχόλιο από το τμήμα PDF, θα έχετε επίσης το `article_searchable.pdf`, το οποίο μπορείτε να ανοίξετε σε οποιονδήποτε προβολέα PDF και να χρησιμοποιήσετε το πλαίσιο αναζήτησης **Ctrl + F** για να εντοπίσετε λέξεις αμέσως.

![Παράδειγμα εξόδου OCR σε εικόνα](example.png "Εκτέλεση OCR σε εικόνα – αποτελέσματα hOCR και PDF")

## Πώς να εξάγετε κείμενο από PNG χρησιμοποιώντας OcrEngine

Αν το μόνο που χρειάζεστε είναι το ακατέργαστο κείμενο (χωρίς διάταξη, χωρίς PDF), μπορείτε να παραλείψετε εντελώς το βήμα hOCR:

```python
ocr_engine.setExportFormat("txt")
text_result = ocr_engine.recognize()
plain_text = text_result.getExportedContent()
print("📝 Extracted text:\n", plain_text)
```

*Γιατί να επιλέξετε plain text;* Είναι ελαφρύ, ιδανικό για ευρετηρίαση, και λειτουργεί άψογα με downstream NLP pipelines.

## Αναγνώριση εικόνας κειμένου και δημιουργία αναζητήσιμου PDF

Η δημιουργία ενός αναζητήσιμου PDF είναι μια διαδικασία δύο βημάτων:

1. **Run OCR** με `hocr` (όπως κάναμε παραπάνω) για να λάβετε τις πληροφορίες διάταξης.
2. **Combine** το αρχικό PNG με το hOCR σε PDF χρησιμοποιώντας τον PDF exporter της μηχανής.

Οι περισσότερες σύγχρονες βιβλιοθήκες OCR (Tesseract, ABBYY, Google Vision) προσφέρουν μια εξαγωγή `pdf` που κάνει ακριβώς αυτό. Το απόσπασμα στο *Optional* τμήμα του κύριου script δείχνει το μοτίβο. Αν η βιβλιοθήκη σας δεν διαθέτει ενσωματωμένο PDF exporter, μπορείτε να χρησιμοποιήσετε **`pdf2image`** + **`reportlab`** για να συνδυάσετε την εικόνα και το hOCR—απλώς ενημερώστε με, και θα μοιραστώ ένα γρήγορο επιπλέον παράδειγμα.

## Μετατροπή PNG σε PDF με έξοδο OCR

Μερικές φορές θέλετε απλώς ένα **plain PDF** που περιέχει την εικόνα (χωρίς αναζητήσιμη στρώση). Αυτό είναι ακόμη πιο απλό:

```python
from PIL import Image

png_path = Path("YOUR_DIRECTORY/article.png")
pdf_path = Path("YOUR_DIRECTORY/article.pdf")

# Pillow can convert directly:
Image.open(png_path).convert("RGB").save(pdf_path, "PDF", resolution=100.0)
print(f"📄 PNG converted to PDF at {pdf_path}")
```

Συνδυάστε αυτό με το βήμα OCR αν χρειάζεστε μια αναζητήσιμη έκδοση, ή κρατήστε το ως πιστή οπτική αναπαράσταση για αρχειοθετικούς σκοπούς.

## Συνηθισμένα προβλήματα & Συμβουλές

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **Blurry or low‑resolution PNG** | Η ακρίβεια του OCR μειώνεται δραματικά κάτω από ~300 DPI. | Ανεβάστε την ανάλυση με `Image.resize((width*2, height*2), Image.LANCZOS)` πριν τη δώσετε στη μηχανή. |
| **Wrong language** | Η μηχανή προεπιλέγει τα Αγγλικά· οι μη‑Αγγλικοί χαρακτήρες γίνονται ακατανόητοι. | Κλήση `ocr_engine.setLanguage('deu')` (ή κατάλληλος κωδικός ISO) πριν το `recognize()`. |
| **Missing hOCR output** | Κάποιες μηχανές προεπιλέγουν plain text όταν δεν κληθεί `setExportFormat`. | Ελέγξτε ότι `setExportFormat("hocr")` εκτελείται **πριν** το `recognize()`. |
| **File permission errors** | Προσπάθεια εγγραφής σε φάκελο μόνο για ανάγνωση. | Χρησιμοποιήστε διαδρομή μέσα στο πρότζεκτ σας ή `os.makedirs(..., exist_ok=True)` πρώτα. |
| **Large PDFs cause memory spikes** | Ο PDF exporter κρατά όλη την εικόνα στη μνήμη RAM. | Επεξεργαστείτε τις σελίδες σε τμήματα ή χρησιμοποιήστε έναν streaming PDF writer. |

*Συμβουλή:* δοκιμάστε πάντα σε μια μικρή δείγμα εικόνας πριν επεκταθείτε σε χιλιάδες. Εξοικονομεί ώρες εντοπισμού σφαλμάτων.

## Συνοψίζοντας

Τώρα ξέρετε **how to run OCR on image** αρχεία, **extract text from PNG**, **recognize text image** για downstream εργασίες, **generate a searchable PDF**, και **convert PNG to PDF** όταν χρειάζεστε ένα απλό αρχείο. Το παρεχόμενο script είναι μια πλήρης, copy‑and‑paste λύση που λειτουργεί αμέσως, και τα προαιρετικά τμήματα σας επιτρέπουν να προσαρμόσετε την έξοδο ακριβώς στη ροή εργασίας σας.

### Τι έπεται;

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}