---
category: general
date: 2026-06-22
description: Λάβετε τις συντεταγμένες του πλαισίου περιβάλλοντος από εικόνες χρησιμοποιώντας
  Python. Μάθετε πώς να εξάγετε κείμενο από εικόνα με Python, χρησιμοποιώντας Aspose
  OCR και ανάλυση JSON σε λίγα λεπτά.
draft: false
keywords:
- get bounding box coordinates
- extract text from image python
- Aspose OCR Python
- OCR layout data JSON
- Python image processing OCR
language: el
og_description: Λάβετε τις συντεταγμένες του πλαισίου περιορισμού από εικόνες χρησιμοποιώντας
  Python. Αυτός ο οδηγός δείχνει πώς να εξάγετε κείμενο από εικόνα με Python χρησιμοποιώντας
  Aspose OCR και να αναλύσετε τα δεδομένα διάταξης.
og_title: Λάβετε Συντεταγμένες Πλαισίου από OCR σε Python – Πλήρης Εκπαιδευτικό Σεμινάριο
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  headline: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  type: TechArticle
- description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  name: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - An active Aspose.OCR for Python
      license or a free trial (the library works without a license but adds a watermark).
      - `pip install aspose-ocr` (the package name on PyPI). - A sample image called
      `invoice.png` placed in a folder you can reference.'
  - name: 1. Convert Bounding Boxes to Simple Rectangles
    text: 'If your downstream tool expects `(x, y, width, height)` instead of eight
      points, add a helper:'
  - name: 2. Handle Multi‑Page PDFs
    text: 'Aspose OCR can accept PDF streams. Replace the image loading line with:'
  - name: 3. Visualize Bounding Boxes
    text: 'If you want to see the boxes drawn on the original image, use Pillow:'
  type: HowTo
- questions:
  - answer: For large documents, consider streaming the JSON or processing page‑by‑page
      to keep memory usage low.
    question: What if the JSON is huge?
  - answer: Low contrast or handwritten text often trips OCR engines. Pre‑process
      the image (increase contrast, binarize) before feeding it to Aspose.
    question: Why are some words missing?
  - answer: Yes—set `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)`
      to receive a `"characters"` array with its own `boundingBox`.
    question: Can I get character‑level coordinates?
  - answer: Absolutely. (0, 0) is the top‑left corner of the image.
    question: Is the coordinate system zero‑based?
  type: FAQPage
tags:
- OCR
- Python
- JSON
- Image Processing
title: Λάβετε Συντεταγμένες Πλαισίου Περιγράμματος από OCR σε Python – Πλήρης Οδηγός
url: /el/python-java/general/get-bounding-box-coordinates-from-ocr-in-python-complete-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Λήψη Συντεταγμένων Πλαισίου Περιγράμματος από OCR σε Python – Πλήρης Οδηγός

Έχετε χρειαστεί ποτέ να **λάβετε τις συντεταγμένες του πλαισίου περιγράμματος** για κάθε λέξη σε ένα σαρωμένο τιμολόγιο, αλλά δεν ήξερατε από πού να ξεκινήσετε; Δεν είστε μόνοι. Σε πολλά έργα αυτοματοποίησης, πρέπει να εντοπίσετε το κείμενο σε μια εικόνα για να το επισημάνετε, να το διαγράψετε ή να το τροφοδοτήσετε σε επόμενες αναλύσεις. Τα καλά νέα; Με λίγες γραμμές Python και Aspose.OCR μπορείτε να εξάγετε τόσο το κείμενο **όσο και** τη ακριβή θέση του σε μία μόνο εκτέλεση.

Σε αυτό το tutorial θα περάσουμε από ένα πρακτικό παράδειγμα που δείχνει πώς να **εξάγετε κείμενο από εικόνα σε στυλ Python**, έπειτα να εμβαθύνουμε στα δεδομένα διάταξης JSON για να εξάγουμε τα πλαίσια περιγράμματος. Χωρίς περιττές πληροφορίες, μόνο ένα λειτουργικό script, εξηγήσεις για το γιατί κάθε βήμα είναι σημαντικό, και συμβουλές για την αποφυγή κοινών παγίδων.

---

## Τι Θα Δημιουργήσετε

Στο τέλος αυτού του οδηγού θα έχετε ένα έτοιμο‑για‑εκτέλεση script Python που:

1. Φορτώνει μια εικόνα (π.χ. ένα PNG τιμολόγιο) στο Aspose OCR.  
2. Διαμορφώνει το engine ώστε να εκδίδει πληροφορίες διάταξης σε JSON.  
3. Αναλύει το JSON σε ένα λεξικό Python.  
4. Επαναλαμβάνει πάνω από κάθε αναγνωρισμένη λέξη, εκτυπώνοντας το κείμενο **και** τις συντεταγμένες του πλαισίου περιγράμματος.

Θα δείτε επίσης πώς να προσαρμόσετε τον κώδικα για πολυσελίδες PDF, διαφορετικές μορφές εικόνας και προσαρμοσμένα συστήματα συντεταγμένων.

### Προαπαιτήσεις

- Python 3.8+ εγκατεστημένο στο σύστημά σας.  
- Ένα ενεργό license Aspose.OCR για Python ή μια δωρεάν δοκιμή (η βιβλιοθήκη λειτουργεί χωρίς άδεια αλλά προσθέτει υδατογράφημα).  
- `pip install aspose-ocr` (το όνομα του πακέτου στο PyPI).  
- Μια δείγμα εικόνας με όνομα `invoice.png` τοποθετημένη σε φάκελο που μπορείτε να αναφέρετε.

Αυτό είναι όλο—χωρίς βαριά frameworks, χωρίς εξωτερικές υπηρεσίες. Ας βουτήξουμε.

---

## Βήμα 1: Εγκατάσταση και Εισαγωγή των Απαιτούμενων Βιβλιοθηκών

Πρώτα, βεβαιωθείτε ότι το πακέτο Aspose OCR και το ενσωματωμένο module `json` είναι διαθέσιμα. Το module `json` περιλαμβάνεται στο Python, οπότε χρειάζεται μόνο η εγκατάσταση του Aspose.

```bash
pip install aspose-ocr
```

Τώρα εισάγετε τα στο script σας:

```python
# Step 1: Import the OCR library and the JSON module
import aspose.ocr as ocr
import json
```

> **Γιατί είναι σημαντικό:** Η εισαγωγή του `aspose.ocr` σας δίνει πρόσβαση στη υψηλής απόδοσης μηχανή OCR, ενώ το `json` σας επιτρέπει να μετατρέψετε το ακατέργαστο string διάταξης σε ένα εγγενές λεξικό Python για εύκολη περιήγηση.

---

## Βήμα 2: Δημιουργία του OCR Engine και Φόρτωση της Εικόνας Σας

Το engine είναι η καρδιά της διαδικασίας. Το δημιουργείτε, έπειτα το κατευθύνετε στην εικόνα που θέλετε να σαρώσετε.

```python
# Step 2: Create an OCR engine instance and load the image to be processed
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))
```

> **Pro tip:** Αντικαταστήστε το `"YOUR_DIRECTORY/invoice.png"` με μια απόλυτη ή σχετική διαδρομή που δείχνει στο πραγματικό σας αρχείο. Αν το αρχείο δεν βρεθεί, το Aspose θα ρίξει `FileNotFoundError`, οπότε ελέγξτε προσεκτικά την ορθογραφία.

---

## Βήμα 3: Διαμόρφωση του Engine για Έξοδο Δεδομένων Διάταξης JSON

Το Aspose OCR μπορεί να επιστρέψει απλό κείμενο, OCR‑μόνο JSON, ή ένα πλήρες JSON διάταξης που περιλαμβάνει συντεταγμένες για λέξεις, γραμμές και ακόμη και μεμονωμένους χαρακτήρες. Για **λήψη συντεταγμένων πλαισίου περιγράμματος**, χρειαζόμαστε το JSON διάταξης.

```python
# Step 3: Configure the engine to output results in JSON format (includes layout data)
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)
```

> **Γιατί JSON;** Το JSON είναι ανεξάρτητο από γλώσσα, αναγνώσιμο από άνθρωπο, και μεταφράζεται άψογα σε λεξικά Python. Το JSON διάταξης περιέχει έναν πίνακα `"words"` όπου κάθε στοιχείο κρατά το κείμενο και έναν πίνακα `boundingBox` με οκτώ αριθμούς (τα τέσσερα σημεία των γωνιών).

---

## Βήμα 4: Εκτέλεση Αναγνώρισης και Λήψη του Ακατέργαστου JSON String

Τώρα τρέχουμε πραγματικά το OCR. Η μέθοδος `recognize()` επιστρέφει ένα αντικείμενο `OcrResult`, από το οποίο μπορούμε να εξάγουμε το JSON string.

```python
# Step 4: Perform recognition and obtain the raw JSON string with words, lines, and bounding boxes
result = engine.recognize()
layout_json = result.get_json()
```

Αν εκτυπώσετε το `layout_json` θα δείτε κάτι σαν:

```json
{
  "words": [
    {
      "text": "Invoice",
      "boundingBox": [12, 34, 112, 34, 112, 58, 12, 58]
    },
    {
      "text": "#12345",
      "boundingBox": [130, 34, 210, 34, 210, 58, 130, 58]
    }
    // ... more words ...
  ]
}
```

> **Edge case:** Κάποιες εικόνες μπορεί να παράγουν κενά arrays `"words"` αν η μηχανή OCR δεν εντοπίσει κείμενο. Σε αυτήν την περίπτωση, ελέγξτε την ποιότητα της εικόνας (αντίθεση, ανάλυση) πριν προχωρήσετε.

---

## Βήμα 5: Ανάλυση του JSON σε Λεξικό Python

Η εργασία με εγγενείς δομές Python είναι πολύ πιο εύκολη από το χειρισμό συμβολοσειρών. Χρησιμοποιήστε τη συνάρτηση `json.loads()` για να μετατρέψετε το string.

```python
# Step 5: Parse the JSON string into a Python dictionary for easy access
layout_data = json.loads(layout_json)
```

Τώρα το `layout_data["words"]` είναι μια λίστα λεξικών, το καθένα αντιπροσωπεύει μια λέξη και το πλαίσιο περιγράμματός της.

---

## Βήμα 6: Επανάληψη πάνω από τις Λέξεις και **Λήψη Συντεταγμένων Πλαισίου Περιγράμματος**

Αυτή είναι η καρδιά του tutorial μας: βρόχος πάνω από κάθε λέξη, εξαγωγή του κειμένου και εκτύπωση των συντεταγμένων. Αυτό είναι το ακριβές σημείο όπου **λαμβάνουμε τις συντεταγμένες του πλαισίου περιγράμματος**.

```python
# Step 6: Iterate through each recognized word and display its text and bounding box coordinates
for word in layout_data["words"]:
    text = word["text"]
    box = word["boundingBox"]  # Format: [x1, y1, x2, y2, x3, y3, x4, y4]
    print(f"'{text}' at {box}")
```

**Δειγματική έξοδος** (οι αριθμοί σας θα διαφέρουν ανάλογα με την εικόνα):

```
'Invoice' at [12, 34, 112, 34, 112, 58, 12, 58]
'#12345' at [130, 34, 210, 34, 210, 58, 130, 58]
'Date' at [12, 70, 60, 70, 60, 94, 12, 94]
'01/01/2024' at [70, 70, 150, 70, 150, 94, 70, 94]
```

> **Γιατί η μορφή οκτώ σημείων;** Οι τέσσερις γωνίες (πάνω‑αριστερά, πάνω‑δεξιά, κάτω‑δεξιά, κάτω‑αριστερά) σας επιτρέπουν να σχεδιάσετε ένα πολύγωνο γύρω από τη λέξη, ακόμη και αν το κείμενο είναι κεκλιμένο. Αν χρειάζεστε μόνο ένα απλό ορθογώνιο, μπορείτε να υπολογίσετε `x_min = min(x1, x2, x3, x4)`, `y_min = min(y1, y2, y3, y4)`, `width = max(x…) - x_min`, και `height = max(y…) - y_min`.

---

## Προαιρετικές Βελτιώσεις

### 1. Μετατροπή Πλαισίων Περιγράμματος σε Απλά Ορθογώνια

Αν το επόμενο εργαλείο σας αναμένει `(x, y, width, height)` αντί για οκτώ σημεία, προσθέστε έναν βοηθό:

```python
def box_to_rect(box):
    xs = box[0::2]  # extract x coordinates
    ys = box[1::2]  # extract y coordinates
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min, x_max - x_min, y_max - y_min)

for word in layout_data["words"]:
    rect = box_to_rect(word["boundingBox"])
    print(f"'{word['text']}' rectangle {rect}")
```

### 2. Διαχείριση Πολυσελίδων PDF

Το Aspose OCR μπορεί να δεχτεί ροές PDF. Αντικαταστήστε τη γραμμή φόρτωσης εικόνας με:

```python
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/document.pdf"))
engine.get_settings().set_page_number(1)  # change for each page in a loop
```

Επαναλάβετε `set_page_number` για κάθε σελίδα, συλλέγοντας τις συντεταγμένες ανά σελίδα.

### 3. Οπτικοποίηση Πλαισίων Περιγράμματος

Αν θέλετε να δείτε τα πλαίσια σχεδιασμένα πάνω στην αρχική εικόνα, χρησιμοποιήστε το Pillow:

```python
from PIL import Image, ImageDraw

img = Image.open("YOUR_DIRECTORY/invoice.png")
draw = ImageDraw.Draw(img)

for word in layout_data["words"]:
    box = word["boundingBox"]
    # Pillow expects a list of tuples [(x1,y1), (x2,y2), ...]
    polygon = [(box[i], box[i+1]) for i in range(0, len(box), 2)]
    draw.line(polygon + [polygon[0]], fill="red", width=2)

img.show()
```

Τώρα θα δείτε κόκκινες γραμμές γύρω από κάθε αναγνωρισμένη λέξη—τέλεια για debugging ή UI overlays.

---

## Συχνές Ερωτήσεις & Προβλήματα

- **Τι γίνεται αν το JSON είναι τεράστιο;** Για μεγάλα έγγραφα, σκεφτείτε τη ροή (streaming) του JSON ή την επεξεργασία σελίδα‑με‑σελίδα για να κρατήσετε τη χρήση μνήμης χαμηλή.  
- **Γιατί λείπουν κάποιες λέξεις;** Χαμηλή αντίθεση ή χειρόγραφο κείμενο συχνά αποτυγχάνουν τις μηχανές OCR. Προεπεξεργαστείτε την εικόνα (αυξήστε την αντίθεση, δυαδικοποιήστε) πριν τη δώσετε στο Aspose.  
- **Μπορώ να λάβω συντεταγμένες επιπέδου χαρακτήρα;** Ναι—ορίστε `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)` για να λάβετε έναν πίνακα `"characters"` με το δικό του `boundingBox`.  
- **Το σύστημα συντεταγμένων είναι μηδενικής βάσης;** Απόλυτα. (0, 0) είναι η πάνω‑αριστερή γωνία της εικόνας.

---

## Πλήρες Script – Έτοιμο για Αντιγραφή & Εκτέλεση

Παρακάτω είναι το πλήρες, εκτελέσιμο παράδειγμα που συνδυάζει όλα τα βήματα. Αποθηκεύστε το ως `extract_bboxes.py` και εκτελέστε `python extract_bboxes.py`.

```python
import aspose.ocr as ocr
import json

# -------------------------
# 1️⃣ Initialize OCR engine
# -------------------------
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))

# -------------------------------------------------
# 2️⃣ Ask for JSON layout output (contains bounding boxes)
# -------------------------------------------------
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)

# -------------------------
# 3️⃣ Run recognition
# -------------------------
result = engine.recognize()
layout_json = result.get_json()

# -------------------------
# 4️⃣ Parse JSON
# -------------------------
layout_data = json.loads(layout_json)

# -------------------------
# 5️⃣ Helper to turn 8‑point box into rectangle (optional)
# -------------------------
def box_to_rect(box):
    xs = box[0::2]
    ys = box[1::2]
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}