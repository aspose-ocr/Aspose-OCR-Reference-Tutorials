---
category: general
date: 2026-07-05
description: Δημιουργήστε αναζητήσιμο PDF με Python. Μάθετε πώς να κάνετε OCR σε σκαναρισμένο
  PNG, να μετατρέψετε σκαναρισμένο PDF εικόνας και να αποκτήσετε ένα αναζητήσιμο PDF
  σε λίγα λεπτά.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- how to ocr pdf
- ocr recognition example
- convert png searchable pdf
language: el
og_description: Δημιουργήστε γρήγορα PDF με δυνατότητα αναζήτησης. Αυτός ο οδηγός
  δείχνει πώς να κάνετε OCR σε PNG, να μετατρέψετε σκαναρισμένο PDF εικόνας και να
  παράγετε PDF με δυνατότητα αναζήτησης χρησιμοποιώντας Python.
og_title: Δημιουργία PDF με δυνατότητα αναζήτησης από σαρωμένη εικόνα – Εγχειρίδιο
  Python OCR
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF with Python. Learn how to OCR a scanned PNG,
    convert scanned image PDF, and get a searchable PDF in minutes.
  headline: Create Searchable PDF from Scanned Image – Full Python OCR Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF
- Automation
title: Δημιουργία Αναζητήσιμου PDF από Σαρωμένη Εικόνα – Πλήρης Οδηγός OCR με Python
url: /el/python-java/general/create-searchable-pdf-from-scanned-image-full-python-ocr-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Αναζητήσιμου PDF από Σαρωμένη Εικόνα – Πλήρης Οδηγός Python OCR

Έχετε αναρωτηθεί ποτέ πώς να **δημιουργήσετε αναζητήσιμο PDF** από μια σαρωμένη εικόνα χωρίς να πληρώσετε για ακριβά λογισμικά; Δεν είστε μόνοι. Σε πολλά γραφεία, τα PDF εμφανίζονται ως επίπεδες εικόνες — δύσκολες στην αναζήτηση, αδύνατο το αντιγραφή‑επικόλληση, και εφιάλτης για ελέγχους συμμόρφωσης. Τα καλά νέα; Με λίγες γραμμές Python μπορείτε να μετατρέψετε αυτό το στατικό PNG σε πλήρως αναζητήσιμο PDF, και η διαδικασία είναι πιο εύκολη απ' ό,τι νομίζετε.

Σε αυτό το tutorial θα περάσουμε από ένα πλήρες **παράδειγμα αναγνώρισης OCR**, καλύπτοντας τα πάντα από την εγκατάσταση της σωστής βιβλιοθήκης μέχρι τη δημιουργία του τελικού αρχείου PDF. Στο τέλος θα ξέρετε ακριβώς πώς να **μετατρέψετε αρχεία PDF με σαρωμένη εικόνα**, πώς να **ocr pdf** προγραμματιστικά, και θα έχετε ένα επαναχρησιμοποιήσιμο script που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο.

## Τι Θα Μάθετε

- Εγκατάσταση και ρύθμιση μιας βιβλιοθήκης OCR για Python (θα χρησιμοποιήσουμε `pytesseract` και `pdf2image`).
- Αρχικοποίηση της μηχανής OCR και ορισμός της γλώσσας.
- Φόρτωση μιας σαρωμένης PNG (ή οποιασδήποτε εικόνας) και εκτέλεση OCR.
- Μετατροπή του αποτελέσματος OCR σε **αναζητήσιμο PDF** (byte array) και αποθήκευση.
- Συμβουλές για διαχείριση εγγράφων πολλαπλών σελίδων, διαφορετικών γλωσσών και κοινών προβλημάτων.

Δεν απαιτείται προηγούμενη εμπειρία με OCR — μόνο ένα λειτουργικό περιβάλλον Python 3 και λίγη περιέργεια.

---

## Δημιουργία Αναζητήσιμου PDF – Επισκόπηση

Παρακάτω φαίνεται ένα υψηλού επιπέδου διάγραμμα ροής των βημάτων που θα υλοποιήσουμε.  

![Create searchable PDF workflow diagram](https://example.com/flowchart.png "Create searchable PDF workflow diagram")

*Alt text: Διάγραμμα ροής δημιουργίας αναζητήσιμου PDF που δείχνει την αρχικοποίηση της μηχανής, τη φόρτωση εικόνας, την αναγνώριση OCR, τη μετατροπή σε PDF και την εγγραφή του αρχείου.*

---

## Βήμα 1: Αρχικοποίηση της Μηχανής OCR (how to ocr pdf)

Γιατί χρειάζεται να αρχικοποιήσουμε κάτι; Η μηχανή OCR είναι ο εγκέφαλος που ερμηνεύει τα μοτίβα εικονοστοιχείων ως χαρακτήρες. Δημιουργώντας μια παρουσία της μηχανής και ορίζοντας ρητά τη γλώσσα, λέμε στη βιβλιοθήκη ποιο αλφάβητο να περιμένει, κάτι που βελτιώνει δραστικά την ακρίβεια.

```python
import pytesseract
from pdf2image import convert_from_path
from PIL import Image
import io

# Ensure Tesseract is on your PATH or provide the executable location
pytesseract.pytesseract.tesseract_cmd = r"/usr/local/bin/tesseract"  # adjust as needed

# Define the language – ENGLISH is the default, but you can add more (e.g., 'fra' for French)
ocr_language = "eng"
```

**Συμβουλή:** Αν χρειάζεται να κάνετε OCR σε έγγραφα πολλαπλών γλωσσών, εγκαταστήστε τα αντίστοιχα πακέτα γλώσσας για το Tesseract και περάστε μια λίστα όπως `"eng+spa"` στο `ocr_language`.

---

## Βήμα 2: Φόρτωση της Σαρωμένης Εικόνας (convert scanned image pdf)

Το επόμενο κομμάτι του παζλ είναι η λήψη των δεδομένων εικόνας στο Python. Είτε έχετε ένα μόνο PNG είτε ένα πολυ‑σελίδων TIFF, η κλάση `PIL.Image` μπορεί να το ανοίξει. Αν ξεκινάτε από ένα PDF που ήδη περιέχει σαρωμένες εικόνες, το `pdf2image` θα μετατρέψει κάθε σελίδα σε εικόνα για εμάς.

```python
# Path to the scanned image (PNG, JPG, TIFF, etc.)
image_path = "YOUR_DIRECTORY/scanned_agreement.png"

# Open the image using Pillow
image = Image.open(image_path)

# If you were starting from a scanned PDF, you could do:
# pages = convert_from_path("scanned.pdf", dpi=300)
# image = pages[0]  # just take the first page for this example
```

**Γιατί είναι σημαντικό:** Η φόρτωση της εικόνας ως αντικείμενο Pillow μας δίνει πρόσβαση στα ακατέργαστα εικονοστοιχεία, τα οποία χρειάζεται η μηχανή OCR. Η παράλειψη αυτού του βήματος και η άμεση παροχή ακατέργαστων bytes θα προκαλούσαν σφάλματα.

---

## Βήμα 3: Εκτέλεση Αναγνώρισης OCR στην Εικόνα (ocr recognition example)

Τώρα το διασκεδαστικό μέρος — αφήνουμε τη μηχανή να διαβάσει το κείμενο. Η `pytesseract.image_to_pdf_or_hocr` επιστρέφει ένα byte stream PDF που ήδη περιέχει ένα αόρατο στρώμα κειμένου, ακριβώς ό,τι χρειαζόμαστε για ένα **αναζητήσιμο PDF**.

```python
# Run OCR and ask for a PDF output (includes the hidden text layer)
pdf_bytes = pytesseract.image_to_pdf_or_hocr(
    image,
    lang=ocr_language,
    extension='pdf'  # returns PDF bytes
)

# pdf_bytes is a binary blob that can be saved directly to disk
```

**Περίπτωση άκρου:** Αν η εικόνα σας έχει χαμηλή αντίθεση, σκεφτείτε να εφαρμόσετε ένα απλό κατώφλι πριν το OCR:

```python
# Convert to grayscale and increase contrast
gray = image.convert('L')
threshold = gray.point(lambda x: 0 if x < 128 else 255, '1')
pdf_bytes = pytesseract.image_to_pdf_or_hocr(threshold, lang=ocr_language, extension='pdf')
```

Αυτό το μικρό βήμα προεπεξεργασίας μπορεί να αυξήσει δραστικά την ακρίβεια.

---

## Βήμα 4: Εγγραφή των Bytes PDF σε Αρχείο (convert png searchable pdf)

Η βιβλιοθήκη OCR μας δίνει ένα byte array — σκεφτείτε το ως το ακατέργαστο περιεχόμενο ενός αρχείου PDF. Το μόνο που χρειάζεται τώρα είναι να γράψουμε αυτά τα bytes στο δίσκο.

```python
output_path = "YOUR_DIRECTORY/agreement_searchable.pdf"

with open(output_path, "wb") as f:
    f.write(pdf_bytes)

print(f"✅ Searchable PDF created at: {output_path}")
```

**Τι θα δείτε:** Ανοίξτε το παραγόμενο αρχείο σε οποιονδήποτε προβολέα PDF και δοκιμάστε να αναζητήσετε μια λέξη που γνωρίζετε ότι υπάρχει στην αρχική εικόνα. Η επισήμανση θα μεταβεί αμέσως στην τοποθεσία, αποδεικνύοντας ότι το αόρατο στρώμα κειμένου λειτουργεί.

---

## Βήμα 5: Επέκταση σε Έγγραφα Πολλαπλών Σελίδων (convert scanned image pdf)

Στην πραγματικότητα, συμβόλαια συχνά καλύπτουν πολλές σελίδες. Για να **convert scanned image pdf** αρχεία που περιέχουν πολλές σελίδες, κάντε βρόχο σε κάθε σελίδα, εφαρμόστε OCR και συνδέστε τα παραγόμενα PDFs.

```python
def ocr_image_to_pdf(image_obj, lang="eng"):
    """Helper that returns PDF bytes for a single image."""
    return pytesseract.image_to_pdf_or_hocr(image_obj, lang=lang, extension='pdf')

def merge_pdfs(pdf_bytes_list):
    """Combine multiple PDF byte streams into one."""
    from PyPDF2 import PdfMerger
    merger = PdfMerger()
    for i, pdf_bytes in enumerate(pdf_bytes_list):
        merger.append(io.BytesIO(pdf_bytes))
    output = io.BytesIO()
    merger.write(output)
    merger.close()
    return output.getvalue()

# Example: convert a multi‑page scanned PDF to searchable PDF
pages = convert_from_path("YOUR_DIRECTORY/scanned_contract.pdf", dpi=300)
pdf_parts = [ocr_image_to_pdf(p, lang=ocr_language) for p in pages]
final_pdf = merge_pdfs(pdf_parts)

with open("YOUR_DIRECTORY/contract_searchable.pdf", "wb") as f:
    f.write(final_pdf)

print("✅ Multi‑page searchable PDF created.")
```

**Γιατί συγχώνευση;** Κάθε κλήση στο `image_to_pdf_or_hocr` παράγει ένα αυτόνομο PDF. Η συγχώνευσή τους εξασφαλίζει ότι το τελικό έγγραφο διατηρεί τη σωστή σειρά σελίδων.

---

## Συνηθισμένα Προβλήματα & Πώς να Τα Διορθώσετε

| Σύμπτωμα | Πιθανή Αιτία | Διόρθωση |
|----------|--------------|----------|
| Δεν είναι δυνατόν να αναζητηθεί κείμενο μετά το άνοιγμα του PDF | Το Tesseract δεν βρίσκει χαρακτήρες (κενό αποτέλεσμα) | Ελέγξτε την ποιότητα της εικόνας, αυξήστε το DPI ή εφαρμόστε προεπεξεργασία (αντίθεση, δυαδικοποίηση). |
| Κατεστραμμένοι χαρακτήρες (π.χ., �) | Λανθασμένο πακέτο γλώσσας ή έλλειψη γραμματοσειρών | Εγκαταστήστε τα σωστά δεδομένα γλώσσας (`tesseract‑lang‑eng`) και βεβαιωθείτε ότι το `ocr_language` ταιριάζει. |
| Το μέγεθος του αρχείου PDF είναι τεράστιο (>10 MB για μια σελίδα) | Χρήση lossless PNG ως πηγή· το OCR προσθέτει εικόνα πλήρους ανάλυσης | Μειώστε την ανάλυση της εικόνας πριν το OCR (`image.thumbnail((1240, 1754))` για A4). |
| Το script καταρρέει στα Windows με το μήνυμα “tesseract.exe not found” | Το εκτελέσιμο του Tesseract δεν είναι στο PATH | Προσθέστε `pytesseract.pytesseract.tesseract_cmd = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"` (προσαρμόστε τη διαδρομή). |

---

## Πλήρες, Έτοιμο‑για‑Εκτέλεση Script

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι ένα αρχείο που μπορείτε να αντιγράψετε‑επικολλήσετε και να τρέξετε:

```python
#!/usr/bin/env python3
"""
create_searchable_pdf.py
A complete example that converts a scanned PNG (or PDF) into a searchable PDF using Tesseract OCR.
"""

import io
import sys
from pathlib import Path

import pytesseract
from pdf2image import convert_from_path
from PIL import Image
from PyPDF2 import PdfMerger

# -------------------- Configuration --------------------
# Adjust these paths for your environment
TESSERACT_CMD = r"/usr/local/bin/tesseract"   # macOS/Linux
# TESSERACT_CMD = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"  # Windows
OCR_LANGUAGE = "eng"                         # Add '+spa' for Spanish, etc.
INPUT_PATH = Path("YOUR_DIRECTORY/scanned_agreement.png")
OUTPUT_PATH = Path("YOUR_DIRECTORY/agreement_searchable.pdf")
# -------------------------------------------------------

# Point pytesseract at the executable
pytesseract.pytesseract.tesseract_cmd = TESSERACT_CMD

def load_image(path: Path) -> Image.Image:
    """Load an image from disk; supports PNG, JPG, TIFF."""
    if not path.is_file():
        sys.exit(f"❌ File not found: {path}")
    return Image.open(path)

def ocr_to_pdf_bytes(img: Image.Image, lang: str = OCR_LANGUAGE) -> bytes:
    """Run OCR on a Pillow image and return PDF bytes with hidden text."""
    return pytesseract.image_to_pdf_or_hocr(img, lang=lang, extension='pdf')

def write_pdf(data: bytes, dest: Path):
    """Write PDF byte stream to a file."""
    dest.parent.mkdir(parents=True, exist_ok=True)
    with open(dest, "wb") as f:
        f.write(data)
    print(f"✅ Searchable PDF saved to {dest}")

def main():
    # Load the scanned image
    image = load_image(INPUT_PATH)

    # Optional: improve contrast for low‑quality scans
    # image = image.convert('L').point(lambda x: 0 if x < 128 else 255, '1')

    # OCR → PDF bytes
    pdf_bytes = ocr_to_pdf_bytes(image)

    # Save the result
    write_pdf(pdf_bytes, OUTPUT_PATH)

if __name__ == "__main__":
    main()
```

Αποθηκεύστε το ως `create_searchable_pdf.py`, αντικαταστήστε τα placeholders με πραγματικές διαδρομές, και τρέξτε:

```bash
python create_searchable_pdf.py
```

Θα πρέπει να δείτε ένα


## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην δική σας ανάπτυξη.

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [OCR Recognizing PDF Documents in Aspose.OCR for Java](/ocr/hongkong/java/ocr-operations/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}