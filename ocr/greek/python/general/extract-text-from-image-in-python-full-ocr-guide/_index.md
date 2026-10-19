---
category: general
date: 2026-06-25
description: Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας Python OCR. Μάθετε πώς να
  φορτώνετε εικόνα για OCR, να εκτελείτε OCR σε Python και να μετατρέπετε την απόδειξη
  σε JSON σε λίγα απλά βήματα.
draft: false
keywords:
- extract text from image
- load image for OCR
- perform OCR in Python
- convert receipt to JSON
language: el
og_description: Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας Python OCR. Αυτό το σεμινάριο
  σας καθοδηγεί στη φόρτωση μιας εικόνας για OCR, στην εκτέλεση OCR με Python και
  στη μετατροπή μιας απόδειξης σε JSON.
og_title: Εξαγωγή κειμένου από εικόνα σε Python – Πλήρης οδηγός OCR
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  headline: Extract Text from Image in Python – Full OCR Guide
  type: TechArticle
- description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  name: Extract Text from Image in Python – Full OCR Guide
  steps:
  - name: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
    text: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
  - name: '**Load an image for OCR** – tell the engine which file to read.'
    text: '**Load an image for OCR** – tell the engine which file to read.'
  - name: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
    text: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
  - name: '**Run the recognition** – actually perform OCR in Python.'
    text: '**Run the recognition** – actually perform OCR in Python.'
  - name: '**Print or store the result** – convert receipt to JSON and see the output.'
    text: '**Print or store the result** – convert receipt to JSON and see the output.'
  - name: Sends the image through a pre‑trained convolutional network.
    text: Sends the image through a pre‑trained convolutional network.
  - name: Decodes the network output into readable characters.
    text: Decodes the network output into readable characters.
  - name: Packages everything into the selected format (JSON in our case).
    text: Packages everything into the selected format (JSON in our case).
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- JSON
title: Εξαγωγή κειμένου από εικόνα σε Python – Πλήρης οδηγός OCR
url: /el/python/general/extract-text-from-image-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Εικόνα με Python – Πλήρης Οδηγός OCR

Έχετε ποτέ χρειαστεί να **εξάγετε κείμενο από εικόνα** αλλά δεν ήξερες από πού να ξεκινήσεις; Σε αυτό το σεμινάριο θα σας δείξουμε πώς να **φορτώσετε εικόνα για OCR**, **εκτελέσετε OCR με Python**, και **μετατρέψετε απόδειξη σε JSON**—όλα με λίγες μόνο γραμμές κώδικα.

Αν έχετε ποτέ δημιουργήσει μια εφαρμογή σάρωσης αποδείξεων, έναν παρακολουθητή εξόδων, ή απλώς θέλετε να αυτοματοποιήσετε την εισαγωγή δεδομένων, θα δείτε γιατί η εξοικείωση με αυτή τη ροή είναι καθοριστική. Στο τέλος θα έχετε ένα λειτουργικό script που διαβάζει μια φωτογραφία απόδειξης και παράγει ένα καθαρό JSON payload έτοιμο για downstream services.

## Τι Θα Μάθετε

Θα καλύψουμε κάθε βήμα από την εγκατάσταση της βιβλιοθήκης `aocr` μέχρι τη διαχείριση του ακατέργαστου αποτελέσματος. Συγκεκριμένα, θα μάθετε πώς να:

1. **Δημιουργήστε μια παρουσίαση του OCR engine** – το σημείο εισόδου για όλη τη δουλειά αναγνώρισης.  
2. **Φορτώστε μια εικόνα για OCR** – ενημερώστε το engine ποιο αρχείο να διαβάσει.  
3. **Επιλέξτε τη μορφή εξαγωγής** – JSON ή XML, θα επιλέξουμε JSON επειδή είναι πιο εύκολο να χρησιμοποιηθεί.  
4. **Εκτελέστε την αναγνώριση** – πραγματικά εκτελέστε OCR με Python.  
5. **Εκτυπώστε ή αποθηκεύστε το αποτέλεσμα** – μετατρέψτε την απόδειξη σε JSON και δείτε το αποτέλεσμα.

Δεν απαιτείται προηγούμενη εμπειρία με OCR· αρκεί μια βασική εγκατάσταση Python και ένα αρχείο εικόνας (απόδειξη, φυλλάδιο, ό,τι χρειάζεστε).  

---

![Diagram showing the flow of extracting text from image using Python OCR](extract-text-from-image-python-ocr.png){alt="Διάγραμμα που δείχνει τη ροή εξαγωγής κειμένου από εικόνα χρησιμοποιώντας Python OCR"}

## Εξαγωγή Κειμένου από Εικόνα – Βήμα‑βήμα Python OCR

Παρακάτω είναι το πλήρες, έτοιμο‑για‑εκτέλεση script. Μπορείτε να το αντιγράψετε‑και‑επικολλήσετε σε ένα αρχείο με όνομα `receipt_ocr.py` και να το τρέξετε με `python receipt_ocr.py`.

```python
# receipt_ocr.py

# 1️⃣ Import the aocr package (make sure it's installed via `pip install aocr`)
import aocr

# 2️⃣ Create an OCR engine instance – this object orchestrates the whole process
engine = aocr.OcrEngine()

# 3️⃣ Load the image you want to process.
#    Replace the path with the location of your receipt or any image.
engine.load_image("YOUR_DIRECTORY/receipt.png")

# 4️⃣ Choose the output format. JSON is handy for APIs and downstream services.
engine.export_format = aocr.ExportFormat.JSON

# 5️⃣ Run the recognition and obtain the raw result.
json_result = engine.recognize()

# 6️⃣ Output the raw JSON string – you can also write it to a file if you prefer.
print(json_result)
```

### Γιατί Λειτουργεί Αυτό

- **Engine instance** – `aocr.OcrEngine()` περιλαμβάνει όλη τη βαριά δουλειά (φόρτωση μοντέλου, προεπεξεργασία κ.λπ.).  
- **Loading the image** – `engine.load_image()` λέει στη βιβλιοθήκη ακριβώς ποιο bitmap να αναλύσει· μπορείτε να δώσετε JPEG, PNG ή ακόμη και πολυ‑σελίδες PDF.  
- **Export format** – Ορίζοντας `engine.export_format` σε `aocr.ExportFormat.JSON` το αποτέλεσμα γίνεται μια δομημένη συμβολοσειρά, ιδανική για APIs που αναμένουν JSON.  
- **Recognition call** – `engine.recognize()` εκτελεί την εκτίμηση του νευρωνικού δικτύου στο παρασκήνιο· επιστρέφει μια συμβολοσειρά JSON που περιέχει τα εντοπισμένα μπλοκ κειμένου, βαθμολογίες εμπιστοσύνης και πληροφορίες διάταξης.  

---

## Φόρτωση Εικόνας για OCR με aocr

Αν αναρωτιέστε αν η εικόνα χρειάζεται κάποια ειδική προεπεξεργασία, η σύντομη απάντηση είναι **όχι**—`aocr` διαχειρίζεται τις περισσότερες κοινές περιπτώσεις (ρύθμιση αντίθεσης, ευθυγράμμιση) αυτόματα. Ωστόσο, μπορείτε να βελτιώσετε την ακρίβεια με:

- Διασφαλίζοντας ότι η εικόνα έχει τουλάχιστον 300 dpi.  
- Κόβοντας τα άσχετα περιθώρια.  
- Μετατρέποντας σε κλίμακα του γκρι πριν τη φορτώσετε (προαιρετικό, το `engine.load_image()` το κάνει αυτό για εσάς).

```python
# Optional preprocessing example using Pillow
from PIL import Image, ImageOps

original = Image.open("YOUR_DIRECTORY/receipt.png")
# Convert to grayscale and increase contrast
processed = ImageOps.autocontrast(original.convert("L"))
processed.save("processed_receipt.png")
engine.load_image("processed_receipt.png")
```

*Συμβουλή:* Αν η απόδειξη περιέχει πολύ θόρυβο, το επιπλέον βήμα παραπάνω μπορεί να ενισχύσει την ακρίβεια του **perform OCR in Python** με αξιοσημείωτο περιθώριο.

---

## Επιλέξτε Μορφή Εξαγωγής και Μετατρέψτε την Απόδειξη σε JSON

Μπορεί να αναρωτιέστε, “Γιατί να μην πάρουμε απλό κείμενο;” Επειδή το JSON διατηρεί τη ιεραρχική δομή (γραμμές, λέξεις, πλαίσια). Αυτό καθιστά πολύ πιο εύκολο τον χάρτη πεδίων όπως *συνολικό ποσό* ή *ημερομηνία* αργότερα.

```python
engine.export_format = aocr.ExportFormat.JSON   # Switch to XML with aocr.ExportFormat.XML if needed
```

Όταν τρέξετε το script, το `json_result` θα μοιάζει κάπως έτσι (συνοπτικά για συντομία):

```json
{
  "pages": [
    {
      "blocks": [
        {
          "text": "Store Name",
          "confidence": 0.98,
          "bbox": [12, 34, 210, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.96,
          "bbox": [15, 400, 190, 420]
        }
      ]
    }
  ]
}
```

Τώρα έχετε ένα **convert receipt to JSON** payload που μπορείτε να τροφοδοτήσετε απευθείας σε μια βάση δεδομένων, ένα REST endpoint, ή ένα μοντέλο μηχανικής μάθησης.

---

## Εκτελέστε την Αναγνώριση και Ανακτήστε τα Αποτελέσματα

Το τελευταίο βήμα—η πραγματική εκτέλεση του OCR—είναι τόσο απλό όσο η κλήση του `recognize()`. Στο παρασκήνιο η βιβλιοθήκη:

1. Στέλνει την εικόνα μέσω ενός προ‑εκπαιδευμένου συνελικτικού δικτύου.  
2. Αποκωδικοποιεί την έξοδο του δικτύου σε αναγνώσιμους χαρακτήρες.  
3. Συσκευάζει τα πάντα στη επιλεγμένη μορφή (JSON στην περίπτωσή μας).

```python
json_result = engine.recognize()
print(json_result)   # <-- This prints the JSON string to stdout
```

Αν χρειάζεται να αποθηκεύσετε το αποτέλεσμα αντί να το εκτυπώσετε, απλώς γράψτε το σε αρχείο:

```python
with open("receipt_output.json", "w", encoding="utf-8") as f:
    f.write(json_result)
```

*Edge case:* Ορισμένες αποδείξεις περιέχουν μη‑ASCII χαρακτήρες (π.χ., “€” ). Βεβαιωθείτε ότι ανοίγετε το αρχείο με κωδικοποίηση UTF‑8, όπως φαίνεται παραπάνω, για να αποφύγετε παραμορφωμένο κείμενο.

---

## Πλήρες Παράδειγμα Λειτουργίας (Όλα τα Βήματα σε Ένα Script)

Συνδυάζοντας τα πάντα, εδώ είναι το τελικό script που μπορείτε να τρέξετε από άκρη σε άκρη:

```python
import aocr
from PIL import Image, ImageOps

# Create engine
engine = aocr.OcrEngine()

# Optional: preprocess image for better accuracy
raw = Image.open("YOUR_DIRECTORY/receipt.png")
processed = ImageOps.autocontrast(raw.convert("L"))
processed.save("processed_receipt.png")

# Load the (processed) image
engine.load_image("processed_receipt.png")

# Choose JSON output
engine.export_format = aocr.ExportFormat.JSON

# Run OCR
json_result = engine.recognize()

# Save result
with open("receipt_output.json", "w", encoding="utf-8") as out_file:
    out_file.write(json_result)

print("OCR complete! JSON saved to receipt_output.json")
```

Τρέξτε το με:

```bash
python receipt_ocr.py
```

Θα πρέπει να δείτε μια γραμμή επιβεβαίωσης και, στον ίδιο φάκελο, ένα αρχείο `receipt_output.json` που περιέχει τα δομημένα δεδομένα.

---

## Συμπέρασμα

Τώρα γνωρίζετε **πώς να εξάγετε κείμενο από εικόνα** χρησιμοποιώντας Python, **πώς να φορτώσετε εικόνα για OCR**, **πώς να εκτελέσετε OCR με Python**, και **πώς να μετατρέψετε απόδειξη σε JSON** για downstream κατανάλωση. Αυτή η end‑to‑end ροή είναι ελαφριά, απαιτεί μόνο το πακέτο `aocr`, και μπορεί να ενσωματωθεί σε οποιοδήποτε pipeline αυτοματοποίησης.

Τι έπεται; Δοκιμάστε να αλλάξετε τη μορφή εξαγωγής σε XML, πειραματιστείτε με διαφορετικές τεχνικές προεπεξεργασίας εικόνας, ή δημιουργήστε ένα μικρό Flask API που δέχεται μια ανεβασμένη απόδειξη και επιστρέφει αμέσως το JSON payload. Ο ουρανός είναι το όριο μόλις έχετε κατακτήσει τα βασικά.

Έχετε ερωτήσεις ή αντιμετωπίζετε πρόβλημα; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

## Τι Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Βήμα‑βήμα](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Εξαγωγή Κειμένου από Εικόνα – Βελτιστοποίηση OCR με Aspose.OCR για .NET](/ocr/english/net/ocr-optimization/)
- [Πώς να εξάγετε πίνακα από εικόνα χρησιμοποιώντας Aspose.OCR για .NET](/ocr/english/net/text-recognition/recognize-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}