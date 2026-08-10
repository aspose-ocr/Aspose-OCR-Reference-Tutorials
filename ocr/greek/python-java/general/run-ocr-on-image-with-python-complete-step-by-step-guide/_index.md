---
category: general
date: 2026-06-06
description: Εκτελέστε OCR σε εικόνα χρησιμοποιώντας Python και δείτε τις βαθμολογίες
  εμπιστοσύνης. Μάθετε πώς να φιλτράρετε λέξεις χαμηλής εμπιστοσύνης, να ορίζετε όρια
  και να αντιμετωπίζετε ειδικές περιπτώσεις.
draft: false
keywords:
- run OCR on image
- Python OCR tutorial
- OCR confidence threshold
- low‑confidence word detection
- image text extraction
language: el
og_description: Εκτελέστε OCR σε εικόνα με Python, ελέγξτε τα επίπεδα εμπιστοσύνης
  και φιλτράρετε τις λέξεις χαμηλής εμπιστοσύνης. Αυτό το σεμινάριο σας καθοδηγεί
  βήμα-βήμα μέσα από ένα πλήρες, εκτελέσιμο παράδειγμα.
og_title: Εκτελέστε OCR σε εικόνα με Python – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  headline: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  name: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  steps:
  - name: Install and Import the OCR Engine
    text: First, make sure the OCR library is available. **EasyOCR** works out‑of‑the‑box
      for many languages and gives you a confidence score per word.
  - name: Run OCR on the Image
    text: Now we actually **run OCR on image**. The `recognize_image` method from
      the original example is replaced with EasyOCR’s `readtext` call, which returns
      a list of `(bbox, text, confidence)` tuples.
  - name: Summarize Overall Confidence
    text: 'Unlike the earlier snippet that printed a single `confidence` attribute,
      EasyOCR gives a confidence per word. To get an overall sense, we’ll average
      them:'
  - name: List Low‑Confidence Words
    text: Now comes the part that directly answers the “list words whose confidence
      is below the desired threshold” requirement. We’ll set a **OCR confidence threshold**
      of 0.80 (80 %) by default, but you can adjust it.
  - name: Edge Cases & Variations
    text: 1. **Batch Processing** – If you need to **run OCR on image** files in bulk,
      wrap the above logic in a loop that iterates over a directory. 2. **Multiple
      Languages** – Pass a list like `['en', 'fr']` to `easyocr.Reader` and the engine
      will detect both. 3. **Alternative Engines** – Want to try **pyte
  type: HowTo
- questions:
  - answer: Not directly. Convert each PDF page to an image first (e.g., with `pdf2image`)
      and then feed the PNG/JPEG into the script.
    question: Does this work with PDFs?
  - answer: 'Try image preprocessing: increase contrast, remove background noise,
      or rotate the image to a horizontal baseline. EasyOCR also accepts a `contrast_ths`
      parameter you can tweak.'
    question: My confidence numbers are all low—what can I do?
  - answer: Absolutely. After the low‑confidence loop, write `ocr_results` to a `csv.DictWriter`
      where each row contains `text`, `confidence`, and bounding‑box coordinates.
    question: Can I export the results to CSV?
  - answer: 'EasyOCR automatically uses CUDA if a compatible GPU and PyTorch are installed.
      Verify with `torch.cuda.is_available()` before running the script. --- ## Conclusion
      We’ve just **run OCR on image** using Python, inspected the overall confidence,
      and isolated any low‑confidence words that need a {{< /b'
    question: Is there a GPU‑accelerated version?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: Εκτελέστε OCR σε εικόνα με Python – Πλήρης οδηγός βήμα‑βήμα
url: /el/python-java/general/run-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε Εικόνα με Python – Πλήρης Οδηγός Βήμα‑βήμα

Κάποτε χρειάστηκε να **εκτελέσετε OCR σε εικόνα** αλλά δεν ήξερες πώς να εξάγεις αξιόπιστο κείμενο; Δεν είσαι μόνος σου—πολλοί προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν οι εξαγόμενες λέξεις φαίνονται ασαφείς και η βαθμολογία εμπιστοσύνης είναι ακατανόητη.  

Σε αυτόν τον οδηγό θα βουτήξουμε κατευθείαν σε μια λειτουργική λύση: θα δεις πώς να εκτελέσεις OCR σε εικόνα, να διαβάσεις τη συνολική εμπιστοσύνη και να εντοπίσεις τυχόν λέξεις χαμηλής εμπιστοσύνης που ίσως χρειάζονται χειροκίνητη επανεξέταση. Στο τέλος θα έχεις ένα επαναχρησιμοποιήσιμο script, θα καταλάβεις γιατί κάθε γραμμή είναι σημαντική και θα ξέρεις πώς να ρυθμίσεις το όριο εμπιστοσύνης για τα δικά σου έργα.

## Τι Καλύπτει Αυτό το Tutorial

Θα περάσουμε από όλη τη ροή εργασίας—από τη φόρτωση μιας εικόνας μέχρι την εκτύπωση μιας τακτοποιημένης αναφοράς λέξεων που έπεσαν κάτω από το όριο 80 % εμπιστοσύνης. Καθ' όλη τη διάρκεια θα συζητήσουμε:

* Επιλογή αξιόπιστης μηχανής OCR (θα χρησιμοποιήσουμε **EasyOCR**, μια δημοφιλής βιβλιοθήκη OCR για Python)  
* Ερμηνεία του χαρακτηριστικού `confidence` που επιστρέφει κάθε αποτέλεσμα OCR  
* Φιλτράρισμα λέξεων με προσαρμοσμένο **όριο εμπιστοσύνης OCR**  
* Επέκταση του script για επεξεργασία παρτίδας ή εναλλακτικές μηχανές όπως **pytesseract**  

Δεν απαιτείται προηγούμενη εμπειρία OCR, μόνο βασική εξοικείωση με την Python και ένα λειτουργικό περιβάλλον (συνιστάται Python 3.9+).  

Έτοιμος/η να μετατρέψεις θολές λήψεις οθόνης σε καθαρό, αναζητήσιμο κείμενο; Ας ξεκινήσουμε.

---

## ## Πώς να Εκτελέσετε OCR σε Εικόνα με Python

Η καρδιά του tutorial είναι ένα τρι‑βήμα snippet που αντικατοπτρίζει τον κώδικα που είδες ήδη. Παρακάτω θα αναλύσουμε κάθε γραμμή, θα εξηγήσουμε το «γιατί» και θα σου δώσουμε ένα πλήρες, έτοιμο για αντιγραφή‑επικόλληση script.

### Βήμα 1: Εγκατάσταση και Εισαγωγή της Μηχανής OCR

Πρώτα, βεβαιώσου ότι η βιβλιοθήκη OCR είναι διαθέσιμη. **EasyOCR** λειτουργεί αμέσως για πολλές γλώσσες και παρέχει βαθμολογία εμπιστοσύνης ανά λέξη.

```bash
pip install easyocr
```

```python
import easyocr  # The engine that will run OCR on image files
import os
```

*Γιατί EasyOCR;* Συμπεριλαμβάνει ένα μοντέλο deep‑learning που έχει εκπαιδευτεί σε ποικίλα σύνολα δεδομένων, οπότε συνήθως λαμβάνεις υψηλότερες τιμές εμπιστοσύνης από την παλαιότερη μηχανή Tesseract, ειδικά σε εικόνες μεικτής ποιότητας.

> **Pro tip:** Αν εργάζεσαι σε περιορισμένο περιβάλλον (π.χ. μικρό Docker container), το `pytesseract` μπορεί να είναι ελαφρύτερο, αλλά θα χάσεις μέρος της σύγχρονης ακρίβειας που προσφέρει το EasyOCR.

### Βήμα 2: Εκτέλεση OCR στην Εικόνα

Τώρα εκτελούμε πραγματικά **OCR σε εικόνα**. Η μέθοδος `recognize_image` από το αρχικό παράδειγμα αντικαθίσταται με την κλήση `readtext` του EasyOCR, η οποία επιστρέφει μια λίστα από πλειάδες `(bbox, text, confidence)`.

```python
# Initialize the OCR reader for English (you can add more languages as needed)
reader = easyocr.Reader(['en'])

# Path to the image you want to process
image_path = os.path.join("YOUR_DIRECTORY", "mixed_quality.png")

# Perform OCR – this is the step where we run OCR on image
ocr_results = reader.readtext(image_path, detail=1, paragraph=False)
```

Κάθε καταχώρηση στο `ocr_results` έχει την εξής μορφή:

```python
[
    ((x1, y1, x2, y2, x3, y3, x4, y4), "Detected text", 0.92),
    ...
]
```

Το τρίτο στοιχείο (`0.92` στο παράδειγμα) είναι η βαθμολογία εμπιστοσύνης, η οποία κυμαίνεται από 0 ως 1.

### Βήμα 3: Σύνοψη Συνολικής Εμπιστοσύνης

Σε αντίθεση με το προηγούμενο snippet που εκτύπωνε ένα μόνο χαρακτηριστικό `confidence`, το EasyOCR δίνει εμπιστοσύνη ανά λέξη. Για να πάρουμε μια γενική εικόνα, θα υπολογίσουμε τον μέσο όρο τους:

```python
# Extract just the confidence numbers
confidences = [item[2] for item in ocr_results]

# Compute the mean confidence (overall confidence)
overall_confidence = sum(confidences) / len(confidences) if confidences else 0

print(f"Overall confidence: {overall_confidence:.2%}")
```

*Γιατί ο μέσος όρος;* Σου δίνει έναν γρήγορο έλεγχο υγείας—αν η συνολική εμπιστοσύνη είναι κάτω από, π.χ., 70 %, πιθανότατα χρειάζεται να βελτιώσεις την εικόνα (καλύτερο φωτισμό, προεπεξεργασία κλπ.).

### Βήμα 4: Λίστα Λέξεων Χαμηλής Εμπιστοσύνης

Τώρα έρχεται το τμήμα που απαντά άμεσα στην απαίτηση «λίστα λέξεων των οποίων η εμπιστοσύνη είναι κάτω από το επιθυμητό όριο». Θα ορίσουμε ένα **όριο εμπιστοσύνης OCR** στο 0.80 (80 %) από προεπιλογή, αλλά μπορείς να το προσαρμόσεις.

```python
# Define the confidence threshold – tweak as needed
THRESHOLD = 0.80

print("\nLow‑confidence words:")
low_confidence_found = False
for bbox, text, conf in ocr_results:
    if conf < THRESHOLD:
        low_confidence_found = True
        print(f"  • '{text}' ({conf:.2%})")
if not low_confidence_found:
    print("  All words meet the confidence threshold.")
```

Ο βρόχος εκτυπώνει κάθε λέξη που δεν πέρασε το όριο, μαζί με το ποσοστό εμπιστοσύνης της. Αυτό είναι το ακριβές ισοδύναμο του αρχικού βρόχου `for recognized_word in recognition_result.words`, αλλά τώρα λειτουργεί με τη μορφή εξόδου του EasyOCR.

---

## ## Κατανόηση Βαθμών Εμπιστοσύνης OCR

Η εμπιστοσύνη δεν είναι ένας μαγικός αριθμός· είναι η εκτίμηση του μοντέλου για το πόσο σίγουρο είναι σχετικά με μια συγκεκριμένη μεταγραφή. Λάβε υπόψη τα εξής:

| Κατάσταση | Τυπική Εμπιστοσύνη | Τι να Κάνεις |
|-----------|-------------------|--------------|
| Καθαρή, υψηλής ανάλυσης σάρωση | 0.95 – 1.00 | Δεν απαιτείται επιπλέον εργασία |
| Ελαφριά θολότητα ή άνισος φωτισμός | 0.80 – 0.94 | Σκέψου ελαφριά προεπεξεργασία (αύξηση αντίθεσης) |
| Πολύ θόρυβος, κείμενο με κλίση | < 0.70 | Εφάρμοσε προεπεξεργασία εικόνας (απλοποίηση, αποθόρυβο) ή άλλαξε μηχανή OCR |

> **Προσοχή:** Ορισμένες γλώσσες (π.χ. καλλιγραφική γραφή) παράγουν φυσικά χαμηλότερες βαθμολογίες. Ρύθμισε το όριο ανάλογα.

### Ακραίες Περιπτώσεις & Παραλλαγές

1. **Επεξεργασία Παρτίδας** – Αν χρειάζεται να **εκτελέσετε OCR σε εικόνα** σε μεγάλες ποσότητες, τυλίξτε τη λογική σε βρόχο που διατρέχει έναν φάκελο.  
2. **Πολλαπλές Γλώσσες** – Περνάτε μια λίστα όπως `['en', 'fr']` στο `easyocr.Reader` και η μηχανή θα εντοπίσει και τις δύο.  
3. **Εναλλακτικές Μηχανές** – Θέλετε να δοκιμάσετε **pytesseract**; Αντικαταστήστε το τμήμα reader με:

   ```python
   import pytesseract
   from PIL import Image

   img = Image.open(image_path)
   raw_text = pytesseract.image_to_string(img, output_type=pytesseract.Output.DICT)
   # raw_text['text'] contains the full string,
   # raw_text['conf'] holds per‑character confidence.
   ```

   Θα χρειαστεί να συγκεντρώσετε τις εμπιστοσύνες ανά χαρακτήρα σε επίπεδο λέξης—λίγο πιο πολύπλοκο, αλλά εφικτό.

4. **Τεχνάσματα Προ‑επεξεργασίας** – Η εφαρμογή φίλτρων OpenCV (`cv2.threshold`, `cv2.GaussianBlur`) μπορεί να αυξήσει την εμπιστοσύνη για θορυβώδεις σάρωσες.  

---

## ## Πλήρες, Έτοιμο‑για‑Εκτέλεση Script

Παρακάτω είναι το ολοκληρωμένο αρχείο Python που μπορείς να προσθέσεις στο πρότζεκτ σου. Αποθήκευσε το ως `ocr_report.py` και τρέξε `python ocr_report.py`. Βεβαιώσου ότι η διαδρομή της εικόνας δείχνει σε πραγματικό αρχείο.

```python
#!/usr/bin/env python3
"""
run_ocr_on_image.py

A self‑contained script that:
  1. Runs OCR on an image using EasyOCR.
  2. Prints the overall confidence.
  3. Lists any words whose confidence falls below a configurable threshold.

Author: Your Name
Date: 2026‑06‑06
"""

import os
import easyocr

# --------------------------- Configuration --------------------------- #
IMAGE_DIR = "YOUR_DIRECTORY"          # <-- Change to your folder
IMAGE_NAME = "mixed_quality.png"      # <-- Change to your file name
THRESHOLD = 0.80                       # Confidence threshold (0‑1)

# --------------------------- Helper Functions ----------------------- #
def load_image_path():
    """Construct the absolute path to the target image."""
    return os.path.join(IMAGE_DIR, IMAGE_NAME)

def run_ocr(image_path):
    """Run OCR on the image and return detailed results."""
    reader = easyocr.Reader(['en'])
    return reader.readtext(image_path, detail=1, paragraph=False)

def compute_overall_confidence(results):
    """Return the mean confidence across all detected words."""
    if not results:
        return 0.0
    confidences = [item[2] for item in results]
    return sum(confidences) / len(confidences)

def report_low_confidence_words(results, threshold):
    """Print words whose confidence is below the given threshold."""
    low_conf = [(text, conf) for _, text, conf in results if conf < threshold]
    if not low_conf:
        print("All words meet the confidence threshold.")
    else:
        for text, conf in low_conf:
            print(f"Low‑confidence word: '{text}' ({conf:.2%})")

# --------------------------- Main Execution ------------------------ #
def main():
    image_path = load_image_path()
    if not os.path.isfile(image_path):
        print(f"❌ Image not found: {image_path}")
        return

    # Step 1: Run OCR on image
    ocr_results = run_ocr(image_path)

    # Step 2: Show overall confidence
    overall = compute_overall_confidence(ocr_results)
    print(f"Overall confidence: {overall:.2%}")

    # Step 3: List low‑confidence words
    print("\n--- Low‑confidence words (threshold: {0:.0%}) ---".format(THRESHOLD))
    report_low_confidence_words(ocr_results, THRESHOLD)

if __name__ == "__main__":
    main()
```

**Αναμενόμενη έξοδος** (τα νούμερα θα διαφέρουν):

```
Overall confidence: 78.45%

--- Low‑confidence words (threshold: 80%) ---
Low‑confidence word: 'recgnition' (62.13%)
Low‑confidence word: 'imgae' (57.90%)
```

Αν κάθε λέξη ξεπεράσει το όριο 80 % θα δεις το φιλικό μήνυμα «All words meet the confidence threshold.» αντί για τη λίστα χαμηλής εμπιστοσύνης.

---

## ## Συχνές Ερωτήσεις (FAQ)

**Ε: Λειτουργεί αυτό με PDF;**  
Α: Όχι άμεσα. Μετέτρεψε κάθε σελίδα PDF σε εικόνα πρώτα (π.χ. με `pdf2image`) και μετά δώσε το PNG/JPEG στο script.

**Ε: Οι αριθμοί εμπιστοσύνης μου είναι όλοι χαμηλοί—τι μπορώ να κάνω;**  
Α: Δοκίμασε προεπεξεργασία εικόνας: αύξησε την αντίθεση, αφαίρεσε τον θόρυβο ή περιστρέψτε την εικόνα ώστε να είναι οριζόντια. Το EasyOCR δέχεται επίσης παράμετρο `contrast_ths` που μπορείς να ρυθμίσεις.

**Ε: Μπορώ να εξάγω τα αποτελέσματα σε CSV;**  
Α: Φυσικά. Μετά τον βρόχο χαμηλής εμπιστοσύνης, γράψε το `ocr_results` σε έναν `csv.DictWriter` όπου κάθε γραμμή περιέχει `text`, `confidence` και συντεταγμένες του bounding‑box.

**Ε: Υπάρχει έκδοση με επιτάχυνση GPU;**  
Α: Το EasyOCR χρησιμοποιεί αυτόματα CUDA αν υπάρχει συμβατό GPU και εγκατεστημένο PyTorch. Επαλήθευσε με `torch.cuda.is_available()` πριν τρέξεις το script.

---

## Συμπέρασμα

Μόλις **εκτελέσαμε OCR σε εικόνα** χρησιμοποιώντας Python, εξετάσαμε τη συνολική εμπιστοσύνη και απομονώσαμε τυχόν λέξεις χαμηλής εμπιστοσύνης που χρειάζονται χειροκίνητη επανεξέταση.

## Τι Θα Πρέπει Να Μάθεις Στη Σύντομη Μελλοντική Σου

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσεις επιπλέον δυνατότητες API και να εξερευνήσεις εναλλακτικές προσεγγίσεις στα δικά σου έργα.

- [Πώς να Ορίσετε Τιμή Κατωφλίου στην Αναγνώριση OCR Εικόνας](/ocr/english/net/ocr-settings/set-threshold-value/)
- [Πώς να Χρησιμοποιήσετε το Aspose OCR για Αποτέλεσμα JSON στην Αναγνώριση Εικόνας](/ocr/english/net/text-recognition/get-result-as-json/)
- [Εξαγωγή Κειμένου από Εικόνα – Βελτιστοποίηση OCR με Aspose.OCR για .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}