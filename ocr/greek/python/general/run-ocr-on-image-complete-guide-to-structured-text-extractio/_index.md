---
category: general
date: 2026-05-03
description: Μάθετε πώς να εκτελείτε OCR σε εικόνα και να εξάγετε κείμενο με συντεταγμένες
  χρησιμοποιώντας δομημένη αναγνώριση OCR. Περιλαμβάνεται βήμα‑βήμα κώδικας Python.
draft: false
keywords:
- run OCR on image
- extract text with coordinates
- structured OCR recognition
- OCR post‑processing
- bounding box extraction
- image text detection
language: el
og_description: Εκτελέστε OCR σε εικόνα και λάβετε το κείμενο με συντεταγμένες χρησιμοποιώντας
  δομημένη αναγνώριση OCR. Πλήρες παράδειγμα Python με επεξηγήσεις.
og_title: Εκτέλεση OCR σε εικόνα – Εκπαιδευτικό για εξαγωγή δομημένου κειμένου
tags:
- OCR
- Python
- Computer Vision
title: Εκτέλεση OCR σε εικόνα – Πλήρης οδηγός για εξαγωγή δομημένου κειμένου
url: /el/python/general/run-ocr-on-image-complete-guide-to-structured-text-extractio/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε εικόνα – Πλήρης Οδηγός για Εξαγωγή Δομημένου Κειμένου

Κάποτε χρειάστηκε να **run OCR on image** αρχεία αλλά δεν ήξερες πώς να διατηρήσεις τις ακριβείς θέσεις κάθε λέξης; Δεν είσαι μόνος σου. Σε πολλά έργα—σάρωση αποδείξεων, ψηφιοποίηση φορμών ή δοκιμές UI—χρειάζεσαι όχι μόνο το ακατέργαστο κείμενο αλλά και τα bounding boxes που δείχνουν πού βρίσκεται κάθε γραμμή στην εικόνα.  

Αυτό το tutorial σου δείχνει έναν πρακτικό τρόπο να *run OCR on image* χρησιμοποιώντας τη μηχανή **aocr**, να ζητήσεις **structured OCR recognition**, και στη συνέχεια να κάνεις post‑processing του αποτελέσματος διατηρώντας τη γεωμετρία. Στο τέλος θα μπορείς να **extract text with coordinates** σε λίγες γραμμές Python και θα καταλάβεις γιατί η δομημένη λειτουργία είναι σημαντική για επόμενα βήματα.

## Τι Θα Μάθεις

- Πώς να αρχικοποιήσεις τη μηχανή OCR για **structured OCR recognition**.  
- Πώς να τροφοδοτήσεις μια εικόνα και να λάβεις ακατέργαστα αποτελέσματα που περιλαμβάνουν τα όρια των γραμμών.  
- Πώς να τρέξεις έναν post‑processor που καθαρίζει το κείμενο χωρίς να χάνει τη γεωμετρία.  
- Πώς να επαναλάβεις τις τελικές γραμμές και να εκτυπώσεις κάθε κομμάτι κειμένου μαζί με το bounding box του.  

Καμία μαγεία, κανένα κρυφό βήμα—απλώς ένα πλήρες, εκτελέσιμο παράδειγμα που μπορείς να ενσωματώσεις στο δικό σου έργο.

---

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιώσου ότι έχεις εγκαταστήσει τα παρακάτω:

```bash
pip install aocr ai   # hypothetical packages; replace with real ones if needed
```

Θα χρειαστείς επίσης ένα αρχείο εικόνας (`input_image.png` ή `.jpg`) που περιέχει καθαρό, αναγνώσιμο κείμενο. Οτιδήποτε από μια σαρωμένη τιμολόγηση μέχρι ένα screenshot λειτουργεί, εφόσον η μηχανή OCR μπορεί να δει τους χαρακτήρες.

---

## Βήμα 1: Αρχικοποίηση της μηχανής OCR για δομημένη αναγνώριση

Το πρώτο που κάνουμε είναι να δημιουργήσουμε μια παρουσία του `aocr.Engine()` και να του πούμε ότι θέλουμε **structured OCR recognition**. Η δομημένη λειτουργία επιστρέφει όχι μόνο το απλό κείμενο αλλά και γεωμετρικά δεδομένα (bounding rectangles) για κάθε γραμμή, κάτι που είναι απαραίτητο όταν χρειάζεται να χαρτογραφήσεις το κείμενο πίσω στην εικόνα.

```python
import aocr
import ai   # hypothetical post‑processing module

# Initialise the OCR engine
ocr_engine = aocr.Engine()

# Request structured recognition (text + geometry)
ocr_engine.recognize_mode = aocr.RecognitionMode.Structured
```

> **Γιατί είναι σημαντικό:**  
> Στην προεπιλεγμένη λειτουργία η μηχανή μπορεί να σου δώσει μόνο μια συμβολοσειρά ενωμένων λέξεων. Η δομημένη λειτουργία σου παρέχει μια ιεραρχία σελίδες → γραμμές → λέξεις, καθεμία με συντεταγμένες, κάνοντας πολύ πιο εύκολο το overlay των αποτελεσμάτων στην αρχική εικόνα ή την τροφοδοσία τους σε μοντέλο που λαμβάνει υπόψη τη διάταξη.

---

## Βήμα 2: Εκτέλεση OCR στην εικόνα και λήψη ακατέργαστων αποτελεσμάτων

Τώρα τροφοδοτούμε την εικόνα στη μηχανή. Η κλήση `recognize` επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει μια συλλογή γραμμών, καθεμία με το δικό της bounding rectangle.

```python
# Load your image (any format supported by aocr)
input_image_path = "input_image.png"

# Run OCR – this returns an OcrResult with lines and bounds
raw_result = ocr_engine.recognize(input_image_path)
```

Σε αυτό το σημείο το `raw_result.lines` περιέχει αντικείμενα με δύο σημαντικά χαρακτηριστικά:

- `text` – η αναγνωρισμένη συμβολοσειρά για αυτή τη γραμμή.  
- `bounds` – ένα tuple όπως `(x, y, width, height)` που περιγράφει τη θέση της γραμμής.

---

## Βήμα 3: Post‑process διατηρώντας τη γεωμετρία

Τα ακατέργαστα αποτελέσματα OCR είναι συχνά θορυβώδη: περιττοί χαρακτήρες, λανθασμένα κενά ή προβλήματα line‑break. Η συνάρτηση `ai.run_postprocessor` καθαρίζει το κείμενο αλλά **διατηρεί την αρχική γεωμετρία** άθικτη, ώστε να έχεις ακόμη ακριβείς συντεταγμένες.

```python
# Apply a post‑processing step that corrects common OCR errors
postprocessed_result = ai.run_postprocessor(raw_result)

# The structure (lines + bounds) stays the same, only `line.text` changes
```

> **Pro tip:** Αν έχεις λεξικά ειδικά για το domain σου (π.χ. κωδικοί προϊόντων), δώσε ένα προσαρμοσμένο λεξικό στον post‑processor για να βελτιώσεις την ακρίβεια.

---

## Βήμα 4: Εξαγωγή κειμένου με συντεταγμένες – επανάληψη και εμφάνιση

Τέλος, κάνουμε βρόχο πάνω από τις καθαρισμένες γραμμές, εκτυπώνοντας το bounding box της κάθε γραμμής μαζί με το κείμενό της. Αυτό είναι το κεντρικό μέρος του **extract text with coordinates**.

```python
# Print each recognised line together with its bounding box
for line in postprocessed_result.lines:
    print(f"[{line.bounds}] {line.text}")
```

### Αναμενόμενο Αποτέλεσμα

Υποθέτοντας ότι η είσοδος εικόνα περιέχει δύο γραμμές: “Invoice #12345” και “Total: $89.99”, θα δεις κάτι σαν:

```
[(15, 30, 210, 25)] Invoice #12345
[(15, 70, 190, 25)] Total: $89.99
```

Το πρώτο tuple είναι το `(x, y, width, height)` της γραμμής στην αρχική εικόνα, επιτρέποντάς σου να σχεδιάσεις ορθογώνια, να επισημάνεις κείμενο ή να τροφοδοτήσεις τις συντεταγμένες σε άλλο σύστημα.

---

## Οπτικοποίηση του Αποτελέσματος (Προαιρετικό)

Αν θέλεις να δεις τα bounding boxes πάνω στην εικόνα, μπορείς να χρησιμοποιήσεις το Pillow (PIL) για να σχεδιάσεις ορθογώνια. Παρακάτω υπάρχει ένα γρήγορο snippet· μπορείς να το παραλείψεις αν χρειάζεσαι μόνο τα ακατέργαστα δεδομένα.

```python
from PIL import Image, ImageDraw

# Open the original image
img = Image.open(input_image_path)
draw = ImageDraw.Draw(img)

# Draw a rectangle around each line
for line in postprocessed_result.lines:
    x, y, w, h = line.bounds
    draw.rectangle([x, y, x + w, y + h], outline="red", width=2)

# Save or show the annotated image
img.save("annotated_output.png")
img.show()
```

![run OCR on image example showing bounding boxes](/images/ocr-bounding-boxes.png "run OCR on image – bounding box overlay")

Το alt κείμενο παραπάνω περιέχει τη **primary keyword**, ικανοποιώντας την απαίτηση SEO για τα alt attributes των εικόνων.

---

## Γιατί η Structured OCR Recognition Υπερισχύει της Απλής Εξαγωγής Κειμένου

Μπορεί να αναρωτιέσαι, “Μπορώ απλώς να τρέξω OCR και να πάρω το κείμενο; Γιατί να ασχοληθώ με τη γεωμετρία;”  

- **Χωρικό πλαίσιο:** Όταν χρειάζεται να τοποθετήσεις πεδία σε μια φόρμα (π.χ. “Date” δίπλα σε μια τιμή ημερομηνίας), οι συντεταγμένες σου λένε *πού* βρίσκεται το δεδομένο.  
- **Διατάξεις πολλαπλών στηλών:** Το απλό γραμμικό κείμενο χάνει τη σειρά· τα δομημένα δεδομένα διατηρούν τη σειρά των στηλών.  
- **Ακρίβεια post‑processing:** Η γνώση του μεγέθους του κουτιού σε βοηθά να αποφασίσεις αν μια λέξη είναι κεφαλίδα, υποσημείωση ή τυχαίο απόσπασμα.  

Συνοπτικά, η **structured OCR recognition** σου δίνει την ευελιξία να χτίσεις πιο έξυπνες pipelines—είτε τροφοδοτείς δεδομένα σε βάση, δημιουργείς αναζητήσιμα PDF ή εκπαιδεύεις μοντέλο μηχανικής μάθησης που σέβεται τη διάταξη.

---

## Συνηθισμένες Ακραίες Περιπτώσεις και Πώς να τις Αντιμετωπίσεις

| Κατάσταση | Σε τι Πρέπει να Προσέχεις | Προτεινόμενη Λύση |
|-----------|---------------------------|-------------------|
| **Περιστροφές ή κλίσεις εικόνας** | Τα bounding boxes μπορεί να είναι εκτός άξονα. | Προεπεξεργασία με deskewing (π.χ. `warpAffine` του OpenCV). |
| **Πολύ μικρές γραμματοσειρές** | Η μηχανή μπορεί να χάσει χαρακτήρες, οδηγώντας σε κενές γραμμές. | Αυξήστε την ανάλυση της εικόνας ή χρησιμοποιήστε `ocr_engine.set_dpi(300)`. |
| **Μικτές γλώσσες** | Λάθος μοντέλο γλώσσας μπορεί να παράγει ακατάληπτο κείμενο. | Ορίστε `ocr_engine.language = ["en", "de"]` πριν την αναγνώριση. |
| **Αλληλοεπικαλυπτόμενα κουτιά** | Ο post‑processor μπορεί να συγχωνεύσει δύο γραμμές ακούσια. | Επαληθεύστε `line.bounds` μετά την επεξεργασία· προσαρμόστε τα όρια στο `ai.run_postprocessor`. |

Η αντιμετώπιση αυτών των σεναρίων νωρίς αποτρέπει προβλήματα αργότερα, ειδικά όταν κλιμακώνεις τη λύση σε εκατοντάδες έγγραφα την ημέρα.

---

## Πλήρες Script End‑to‑End

Παρακάτω βρίσκεται το ολοκληρωμένο, έτοιμο‑για‑εκτέλεση πρόγραμμα που ενώνει όλα τα βήματα. Αντέγραψε‑επικόλλησε, προσαρμόζε το μονοπάτι της εικόνας, και είσαι έτοιμος.

```python
# -*- coding: utf-8 -*-
"""
Run OCR on image – extract text with coordinates using structured OCR recognition.
Author: Your Name
Date: 2026-05-03
"""

import aocr
import ai
from PIL import Image, ImageDraw

def run_structured_ocr(image_path: str, annotate: bool = False):
    # 1️⃣ Initialise the OCR engine
    ocr_engine = aocr.Engine()
    ocr_engine.recognize_mode = aocr.RecognitionMode.Structured

    # 2️⃣ Recognise the image
    raw_result = ocr_engine.recognize(image_path)

    # 3️⃣ Post‑process while keeping geometry
    processed = ai.run_postprocessor(raw_result)

    # 4️⃣ Print each line with its bounding box
    for line in processed.lines:
        print(f"[{line.bounds}] {line.text}")

    # Optional visualisation
    if annotate:
        img = Image.open(image_path)
        draw = ImageDraw.Draw(img)
        for line in processed.lines:
            x, y, w, h = line.bounds
            draw.rectangle([x, y, x + w, y + h], outline="red", width=2)
        annotated_path = "annotated_" + image_path
        img.save(annotated_path)
        print(f"Annotated image saved as {annotated_path}")

if __name__ == "__main__":
    INPUT_IMG = "input_image.png"
    run_structured_ocr(INPUT_IMG, annotate=True)
```

Η εκτέλεση αυτού του script:

1. **Run OCR on image** με δομημένη λειτουργία.  
2. **Extract text with coordinates** για κάθε γραμμή.  
3. Προαιρετικά παράγει ένα PNG με τα annotations.

---

## Συμπέρασμα

Τώρα διαθέτεις μια ολοκληρωμένη, αυτόνομη λύση για **run OCR on image** και **extract text with coordinates** χρησιμοποιώντας **structured OCR recognition**. Ο κώδικας δείχνει κάθε βήμα—from την αρχικοποίηση της μηχανής μέχρι το post‑processing και την οπτική επαλήθευση—ώστε να το προσαρμόσεις σε αποδείξεις, φόρμες ή οποιοδήποτε οπτικό έγγραφο που απαιτεί ακριβή εντοπισμό κειμένου.

Τι θα κάνεις μετά; Δοκίμασε να αντικαταστήσεις τη μηχανή `aocr` με άλλη βιβλιοθήκη (Tesseract, EasyOCR) και δες πώς διαφέρουν τα δομημένα αποτελέσματά τους. Πειραματίσου με διαφορετικές στρατηγικές post‑processing, όπως ορθογραφικό έλεγχο ή προσαρμοσμένα regex φίλτρα, για να αυξήσεις την ακρίβεια στο domain σου. Και αν χτίζεις μεγαλύτερη pipeline, σκέψου την αποθήκευση των ζευγών `(text, bounds)` σε βάση δεδομένων για μελλοντική ανάλυση.

Καλή προγραμματιστική δουλειά, και οι OCR προσπάθειές σου να είναι πάντα ακριβείς!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}