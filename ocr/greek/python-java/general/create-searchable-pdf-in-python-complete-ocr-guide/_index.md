---
category: general
date: 2026-06-22
description: Δημιουργήστε αναζητήσιμο PDF σε Python χρησιμοποιώντας OCR – μάθετε πώς
  να μετατρέπετε εικόνα σε PDF, να αναγνωρίζετε κείμενο σε PDF και να αυτοματοποιείτε
  τη ροή εργασίας σας.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- ocr image to pdf
- recognize text pdf
- python ocr pdf
language: el
og_description: Δημιουργήστε PDF με δυνατότητα αναζήτησης στην Python χρησιμοποιώντας
  OCR. Ακολουθήστε αυτόν τον βήμα‑βήμα οδηγό για να μετατρέψετε εικόνα σε PDF, να
  αναγνωρίσετε κείμενο PDF και να αυτοματοποιήσετε την επεξεργασία εγγράφων.
og_title: Δημιουργήστε αναζητήσιμο PDF σε Python – Πλήρης Οδηγός OCR
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create searchable PDF in Python using OCR – learn how to convert image
    to PDF, recognize text PDF, and automate your workflow.
  headline: Create searchable PDF in Python – Complete OCR Guide
  type: TechArticle
- description: Create searchable PDF in Python using OCR – learn how to convert image
    to PDF, recognize text PDF, and automate your workflow.
  name: Create searchable PDF in Python – Complete OCR Guide
  steps:
  - name: Initialise the OCR engine
    text: The first thing you do is spin up an `OcrEngine` object. Think of it as
      turning on a scanner that’s ready to read your image.
  - name: Load the image you want to convert
    text: Next we feed the engine with an image stream. The `ImageStream.from_file`
      helper reads the file and wraps it in a format the OCR engine understands.
  - name: Tell the engine to output a searchable PDF
    text: By default many OCR SDKs output plain text. We need to switch the output
      format to PDF so the resulting file is both visual and searchable.
  - name: Prepare an in‑memory stream for the PDF data
    text: Instead of writing directly to disk, we capture the PDF in a `MemoryStream`.
      This keeps I/O fast and lets you pipe the bytes elsewhere (e.g., upload to S3)
      if you wish.
  - name: Run the recognition and write the PDF
    text: Now the heavy lifting happens. The `recognize` call reads the image, runs
      OCR, and streams the searchable PDF into `pdf_stream`.
  - name: Save the generated PDF to a file
    text: Finally, we dump the bytes from the memory stream onto disk. The resulting
      file can be opened in Adobe Reader, Preview, or any PDF viewer with full‑text
      search.
  type: HowTo
tags:
- OCR
- Python
- PDF
title: Δημιουργία PDF με δυνατότητα αναζήτησης σε Python – Πλήρης οδηγός OCR
url: /el/python-java/general/create-searchable-pdf-in-python-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία αναζητήσιμου PDF σε Python – Πλήρης Οδηγός OCR

Έχετε ποτέ χρειαστεί να **δημιουργήσετε αναζητήσιμο PDF** από ένα σαρωμένο συμβόλαιο αλλά δεν ήξερατε από πού να ξεκινήσετε; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν προσπαθούν για πρώτη φορά να μετατρέψουν μια bitmap εικόνα σε έγγραφο με δυνατότητα αναζήτησης κειμένου. Τα καλά νέα είναι ότι με ένα μικρό script Python μπορείτε να **convert image to PDF**, να αφήσετε τη μηχανή OCR να αναγνωρίσει κάθε λέξη, και να καταλήξετε σε ένα τέλεια αναζητήσιμο αρχείο.

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία, από την εγκατάσταση της κατάλληλης βιβλιοθήκης μέχρι τη διαχείριση ειδικών περιπτώσεων όπως έγγραφα πολλαπλών σελίδων. Στο τέλος θα μπορείτε να **ocr image to pdf**, **recognize text pdf**, και να ενσωματώσετε τη ροή εργασίας σε μεγαλύτερα pipelines αυτοματισμού.

## Τι θα χρειαστείτε

Πριν βουτήξουμε, βεβαιωθείτε ότι έχετε τα παρακάτω στον υπολογιστή σας:

| Απαίτηση | Γιατί είναι σημαντικό |
|-------------|----------------|
| Python 3.8 or newer | Σύγχρονη σύνταξη και καλύτερες υποδείξεις τύπων |
| `ocr` Python package (or any compatible OCR SDK) | Παρέχει `OcrEngine`, `ImageStream` και έξοδο PDF |
| Μια σαρωμένη εικόνα (JPEG, PNG ή TIFF) | Η πηγή που θα μετατρέψετε |
| Δικαίωμα εγγραφής σε φάκελο για το PDF εξόδου | Για να μπορείτε να αποθηκεύσετε το παραγόμενο αρχείο |

Αν δεν έχετε εγκαταστήσει ακόμη το SDK, εκτελέστε:

```bash
pip install ocr-sdk   # replace with the actual package name
```

> **Pro tip:** Χρησιμοποιήστε ένα εικονικό περιβάλλον (`python -m venv .venv`) για να διατηρήσετε τις εξαρτήσεις οργανωμένες.

## Επισκόπηση της ροής εργασίας

1. **Create an OCR engine instance** – ο εγκέφαλος πίσω από την αναγνώριση.  
2. **Load the image** που θέλετε να επεξεργαστείτε.  
3. **Configure the engine** ώστε να εκδίδει αναζητήσιμο PDF αντί για απλό κείμενο.  
4. **Prepare an in‑memory stream** που θα κρατά τα bytes του PDF.  
5. **Run the recognition** – η μηχανή διαβάζει την εικόνα, εξάγει κείμενο και γράφει το PDF.  
6. **Persist the PDF to disk** ώστε να μπορείτε να το ανοίξετε σε οποιονδήποτε προβολέα.

Αυτή είναι η πλήρης ιστορία σε έξι γραμμές κώδικα. Ας αναλύσουμε κάθε βήμα.

---

## Δημιουργία αναζητήσιμου PDF – Βήμα‑βήμα Python OCR Tutorial

### Βήμα 1: Αρχικοποίηση της μηχανής OCR

Το πρώτο πράγμα που κάνετε είναι να δημιουργήσετε ένα αντικείμενο `OcrEngine`. Σκεφτείτε το ως το άνοιγμα ενός σαρωτή που είναι έτοιμος να διαβάσει την εικόνα σας.

```python
import ocr

# Initialise the OCR engine – this is where all the magic begins
engine = ocr.OcrEngine()
```

> **Why this matters:** Η δημιουργία της μηχανής εκχωρεί εσωτερικές μνήμες και φορτώνει δεδομένα γλώσσας. Η παράλειψη αυτού του βήματος θα προκαλέσει σφάλμα `NoneType` αργότερα όταν προσπαθήσετε να ορίσετε την εικόνα.

### Βήμα 2: Φόρτωση της εικόνας που θέλετε να μετατρέψετε

Στη συνέχεια τροφοδοτούμε τη μηχανή με ένα ρεύμα εικόνας. Η βοηθητική συνάρτηση `ImageStream.from_file` διαβάζει το αρχείο και το τυλίγει σε μορφή που καταλαβαίνει η μηχανή OCR.

```python
# Load the source image – replace the path with your own file
image_path = "YOUR_DIRECTORY/contract.jpg"
engine.set_image(ocr.ImageStream.from_file(image_path))
```

> **Edge case:** Αν η πηγή σας είναι ένα multi‑page TIFF, χρησιμοποιήστε `ocr.MultiPageImageStream.from_file` αντί αυτού. Η μηχανή θα αντιμετωπίσει κάθε σελίδα ως ξεχωριστή σελίδα PDF αυτόματα.

### Βήμα 3: Εντοπίστε στη μηχανή να εξάγει αναζητήσιμο PDF

Από προεπιλογή, πολλά OCR SDK εξάγουν απλό κείμενο. Πρέπει να αλλάξουμε τη μορφή εξόδου σε PDF ώστε το παραγόμενο αρχείο να είναι τόσο οπτικό όσο και αναζητήσιμο.

```python
# Configure the engine to produce a searchable PDF
engine.get_settings().set_output_format(ocr.OutputFormat.PDF)
```

> **What’s happening under the hood?** Η μηχανή τώρα ενσωματώνει ένα αόρατο στρώμα κειμένου πίσω από το bitmap, επιτρέποντάς σας να αναζητήσετε λέξεις όπως σε ένα φυσικό PDF.

### Βήμα 4: Προετοιμασία ρεύματος μνήμης για τα δεδομένα PDF

Αντί να γράψουμε απευθείας στο δίσκο, καταγράφουμε το PDF σε ένα `MemoryStream`. Αυτό διατηρεί το I/O γρήγορο και σας επιτρέπει να μεταφέρετε τα bytes αλλού (π.χ., ανέβασμα σε S3) αν το επιθυμείτε.

```python
# Create a memory buffer that will receive the PDF bytes
pdf_stream = ocr.MemoryStream()
```

### Βήμα 5: Εκτέλεση της αναγνώρισης και εγγραφή του PDF

Τώρα γίνεται η βαριά δουλειά. Η κλήση `recognize` διαβάζει την εικόνα, εκτελεί OCR, και ρέει το αναζητήσιμο PDF στο `pdf_stream`.

```python
# Perform OCR and write the searchable PDF into the memory stream
engine.recognize(pdf_stream)
```

> **Common pitfall:** Η παράλειψη κλήσης του `engine.recognize` θα αφήσει το `pdf_stream` κενό, και η προσπάθεια αποθήκευσης θα προκαλέσει `ValueError`. Πάντα ελέγξτε το `pdf_stream.length` αν χρειάζεται να επαληθεύσετε ότι δημιουργήθηκαν δεδομένα.

### Βήμα 6: Αποθήκευση του παραγόμενου PDF σε αρχείο

Τέλος, αποθηκεύουμε τα bytes από το ρεύμα μνήμης στο δίσκο. Το παραγόμενο αρχείο μπορεί να ανοιχθεί σε Adobe Reader, Preview ή οποιονδήποτε προβολέα PDF με πλήρη αναζήτηση κειμένου.

```python
output_path = "YOUR_DIRECTORY/contract_searchable.pdf"

# Write the PDF bytes to a file
with open(output_path, "wb") as f:
    f.write(pdf_stream.to_bytes())
print(f"✅ Searchable PDF saved to {output_path}")
```

> **Result you’ll see:** Ανοίξτε το PDF, πατήστε `Ctrl+F`, πληκτρολογήστε μια λέξη που εμφανίζεται στην αρχική σάρωση, και δείτε τον προβολέα να την επισημαίνει αμέσως. Αυτό είναι το χαρακτηριστικό ενός **searchable PDF**.

## Μετατροπή εικόνας σε PDF – Ρύθμιση παραμέτρων για βέλτιστα αποτελέσματα

Αν ο κύριος στόχος σας είναι απλώς να **convert image to PDF** χωρίς OCR, μπορείτε να παραλείψετε το βήμα 3 και να ορίσετε τη μορφή εξόδου σε `ocr.OutputFormat.IMAGE_PDF`. Η μηχανή θα ενσωματώσει το bitmap ως σελίδα PDF χωρίς κρυφό στρώμα κειμένου.

```python
engine.get_settings().set_output_format(ocr.OutputFormat.IMAGE_PDF)
```

Χρησιμοποιήστε αυτή τη λειτουργία όταν χρειάζεστε μια πιστή οπτική αναπαράσταση αλλά δεν σας ενδιαφέρει η δυνατότητα αναζήτησης—ίσως για αρχειοθετικούς σκοπούς όπου δεν απαιτείται OCR.

## Αναγνώριση κειμένου PDF – Προσθήκη πακέτων γλώσσας και έλεγχος DPI

Για μια αξιόπιστη εμπειρία **recognize text PDF**, εξετάστε τις παρακάτω προαιρετικές ρυθμίσεις:

```python
settings = engine.get_settings()
settings.set_language("eng+spa")          # English + Spanish support
settings.set_dpi(300)                     # Higher DPI improves accuracy
settings.enable_auto_rotate(True)         # Auto‑rotate skewed scans
```

> **Why adjust DPI?** Μια υψηλότερη ανάλυση παρέχει στη μηχανή OCR περισσότερα pixel για ανάλυση, μειώνοντας τις λανθασμένες αναγνώσεις σε σαρώσεις χαμηλής ποιότητας.

## Python OCR PDF – Ενσωμάτωση σε μεγαλύτερα pipelines

Τώρα που μπορείτε να **python ocr pdf** σε λίγες γραμμές, φανταστείτε την ενσωμάτωση αυτής της λογικής σε ένα Flask API:

```python
from flask import Flask, request, send_file
import io, ocr

app = Flask(__name__)

@app.route("/upload", methods=["POST"])
def upload():
    file = request.files["image"]
    engine = ocr.OcrEngine()
    engine.set_image(ocr.ImageStream.from_bytes(file.read()))
    engine.get_settings().set_output_format(ocr.OutputFormat.PDF)
    pdf_stream = ocr.MemoryStream()
    engine.recognize(pdf_stream)

    return send_file(
        io.BytesIO(pdf_stream.to_bytes()),
        mimetype="application/pdf",
        as_attachment=True,
        download_name="searchable.pdf"
    )
```

Αυτό το μικρό endpoint επιτρέπει σε έναν πελάτη να στείλει (POST) μια εικόνα και να λάβει αμέσως ένα **searchable PDF**—ιδανικό για υπηρεσίες SaaS επεξεργασίας εγγράφων.

## Συνηθισμένα προβλήματα όταν **ocr image to pdf**

| Σύμπτωμα | Πιθανή αιτία | Διόρθωση |
|---------|--------------|-----|
| Κενές σελίδες PDF | Η εικόνα δεν φορτώθηκε (`engine.set_image` κλήθηκε με λάθος διαδρομή) | Επαληθεύστε τη διαδρομή και χρησιμοποιήστε `os.path.abspath` |
| Δεν υπάρχει αναζητήσιμο κείμενο | Η μορφή εξόδου παραμένει σε `IMAGE_PDF` | Καλέστε ρητά `set_output_format(ocr.OutputFormat.PDF)` |
| Παραμορφωμένοι χαρακτήρες | Λανθασμένο πακέτο γλώσσας | Φορτώστε τη σωστή γλώσσα με `settings.set_language("eng")` |
| Αργή επεξεργασία σε μεγάλα αρχεία | Χρήση προεπιλεγμένου DPI (72) σε εικόνες υψηλής ανάλυσης | Αυξήστε το DPI σε 300 ή επεξεργαστείτε τις σελίδες παρτίδες ξεχωριστά |

## Πλήρες, εκτελέσιμο παράδειγμα (έτοιμο για αντιγραφή‑επικόλληση)

```python
import ocr

def create_searchable_pdf(image_path: str, output_path: str) -> None:
    """
    Convert a scanned image to a searchable PDF using the ocr SDK.
    """
    # 1️⃣ Initialise engine
    engine = ocr.OcrEngine()

    # 2️⃣ Load image
    engine.set_image(ocr.ImageStream.from_file(image_path))

    # 3️⃣ Set output to searchable PDF
    engine.get_settings().set_output_format(ocr.OutputFormat.PDF)

    # Optional: improve accuracy
    settings = engine.get_settings()
    settings.set_language("eng")   # adjust as needed
    settings.set_dpi(300)

    # 4️⃣ Prepare in‑memory stream
    pdf_stream = ocr.MemoryStream()

    # 5️⃣ Run OCR
    engine.recognize(pdf_stream)

    # 6️⃣ Persist PDF
    with open(output_path, "wb") as f:
        f.write(pdf_stream.to_bytes())
    print(f"✅ Searchable PDF created at: {output_path}")

if __name__ == "__main__":
    create_searchable_pdf(
        image_path="YOUR_DIRECTORY/contract.jpg",
        output_path="YOUR_DIRECTORY/contract_searchable.pdf"
    )
```

Εκτελέστε το script, ανοίξτε το παραγόμενο PDF, και δοκιμάστε να αναζητήσετε μια λέξη που γνωρίζετε ότι εμφανίζεται στην αρχική σάρωση. Αν όλα πήγαν ομαλά, μόλις κατακτήσατε το **create searchable pdf** με Python.

## Συμπέρασμα

Καλύψαμε όλα όσα χρειάζεστε για να **create searchable PDF** αρχεία χρησιμοποιώντας μια βιβλιοθήκη OCR Python: αρχικοποίηση της μηχανής, φόρτωση εικόνας, ρύθμιση εξόδου PDF, ροή του αποτελέσματος, και τελικά αποθήκευση στο δίσκο. Επίσης, είδατε πώς να **convert image to PDF**, να ρυθμίσετε λεπτομερώς **

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε σε πρόσθετα χαρακτηριστικά API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Αναγνώριση κειμένου PDF – Λειτουργίες OCR με Aspose.OCR για Java](/ocr/english/java/ocr-operations/)
- [Πώς να κάνετε OCR PDF σε .NET με Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Μετατροπή εικόνων σε PDF C# – Αποθήκευση αποτελέσματος OCR πολλαπλών σελίδων](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}