---
category: general
date: 2026-01-12
description: Πώς να εκτελέσετε OCR και να μετατρέψετε γρήγορα μια εικόνα σε κείμενο.
  Μάθετε να αναγνωρίζετε ειδικούς χαρακτήρες, να εξάγετε κείμενο από εικόνα και να
  φορτώνετε εικόνα για OCR με ένα πλήρες παράδειγμα Python.
draft: false
keywords:
- how to perform OCR
- convert image to text
- recognize special characters
- extract text from image
- load image for OCR
language: el
og_description: Πώς να εκτελέσετε OCR στην Python, να μετατρέψετε εικόνα σε κείμενο
  και να αναγνωρίσετε ειδικούς χαρακτήρες. Ακολουθήστε αυτόν τον πρακτικό οδηγό για
  την εξαγωγή κειμένου από εικόνες.
og_title: Πώς να εκτελέσετε OCR σε Python – Πλήρης οδηγός
tags:
- OCR
- Python
- Image Processing
title: Πώς να εκτελέσετε OCR στην Python – Οδηγός βήμα‑προς‑βήμα
url: /el/python/general/how-to-perform-ocr-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εκτελέσετε OCR σε Python – Οδηγός Βήμα‑Βήμα

Έχετε χρειαστεί ποτέ να **εκτελέσετε OCR** σε ένα στιγμιότυπο οθόνης που περιέχει τόσο λατινικούς όσο και κυριλλικούς χαρακτήρες; Δεν είστε μόνοι. Σε πολλά έργα—είτε πρόκειται για ψηφιοποίηση αποδείξεων, ευρετηρίαση πολυγλωσσικών εγγράφων, ή δημιουργία ενός αναζητήσιμου αρχείου—**πώς να εκτελέσετε OCR** γρήγορα γίνεται μια ερώτηση που απασχολεί πολλούς.  

Σε αυτό το tutorial θα περάσουμε από ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει πώς να **μετατρέψετε εικόνα σε κείμενο**, **αναγνωρίσετε ειδικούς χαρακτήρες**, και **εξάγετε κείμενο από εικόνα** χρησιμοποιώντας μια απλή βιβλιοθήκη Python. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση script που φορτώνει μια εικόνα για OCR, διαχειρίζεται πολυγλωσσικό περιεχόμενο, και εκτυπώνει το αποτέλεσμα.

## Τι Θα Χρειαστείτε

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τα παρακάτω:

- Εγκατεστημένο Python 3.8+ στο σύστημά σας.  
- Το πακέτο `ocr` (ή οποιαδήποτε συμβατή βιβλιοθήκη OCR) εγκατεστημένο μέσω `pip install ocr`.  
- Ένα αρχείο εικόνας (`multilingual.png`) που περιέχει τόσο λατινικούς όσο και κυριλλικούς γλυφούς.  
- Έναν βασικό επεξεργαστή κειμένου ή IDE—VS Code, PyCharm, ή ακόμη και ένα απλό Notepad αρκούν.  

Αν δεν έχετε το πακέτο `ocr`, μπορείτε να το αντικαταστήσετε με το `pytesseract` με μερικές μικρές αλλαγές· οι βασικές έννοιες παραμένουν ίδιες.

## Βήμα 1: Εγκατάσταση και Εισαγωγή της Βιβλιοθήκης OCR

Πρώτα, ας ετοιμάσουμε τη μηχανή OCR. Θα εισάγουμε τη βιβλιοθήκη, θα δημιουργήσουμε μια παρουσία engine, και θα τη ρυθμίσουμε για πολυγλωσσική υποστήριξη.

```python
# Install the library (run this once in your terminal)
# pip install ocr

import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()

# Optional: Enable language packs for Latin and Cyrillic
engine.set_languages(['eng', 'rus'])  # 'eng' = English, 'rus' = Russian
```

**Γιατί είναι σημαντικό:**  
Η δημιουργία του engine είναι το θεμέλιο—χωρίς αυτό δεν μπορείτε να **φορτώσετε εικόνα για OCR** αργότερα. Η ενεργοποίηση των πακέτων γλώσσας εξασφαλίζει ότι η μηχανή μπορεί να αναγνωρίσει σωστά χαρακτήρες όπως “Ŀ”, “Ҕ”, και “Ǣ”. Αν παραλείψετε αυτό το βήμα, θα καταλήξετε με ακατάληπτο αποτέλεσμα για μη‑λατινικά σενάρια.

## Βήμα 2: Φόρτωση της Εικόνας που Περιέχει Πολυγλωσσικό Κείμενο

Τώρα κατευθύνουμε τη μηχανή στο αρχείο που θέλουμε να επεξεργαστούμε. Η διαδρομή μπορεί να είναι απόλυτη ή σχετική· απλώς βεβαιωθείτε ότι δείχνει σε μια αναγνώσιμη εικόνα.

```python
# Step 2: Load the image containing multilingual text
image_path = "YOUR_DIRECTORY/multilingual.png"  # replace with your actual path
engine.load_image(image_path)
```

> ![παράδειγμα εκτέλεσης OCR](/images/ocr-example.png "πώς να εκτελέσετε OCR σε μια πολυγλωσσική εικόνα")

**Γιατί είναι σημαντικό:**  
Η κλήση `load_image` διαβάζει τα δεδομένα pixel στη μνήμη, προετοιμάζοντάς τα για τον αλγόριθμο OCR. Αν η εικόνα είναι μεγάλη, η μηχανή μπορεί αυτόματα να τη μειώσει· μπορείτε να το ρυθμίσετε αργότερα με `engine.set_max_resolution(3000)` για σαρώσεις υψηλής ανάλυσης.

## Βήμα 3: Εκτέλεση της Διαδικασίας Αναγνώρισης

Με τη μηχανή έτοιμη και την εικόνα φορτωμένη, μπορούμε τελικά να εξάγουμε το κειμενικό περιεχόμενο.

```python
# Step 3: Perform OCR recognition on the loaded image
result = engine.recognize()
```

**Γιατί είναι σημαντικό:**  
Η `recognize()` εκτελεί το βαρέως βάρους νευρωνικό δίκτυο στο παρασκήνιο. Επιστρέφει ένα αντικείμενο που περιέχει το ακατέργαστο κείμενο, βαθμολογίες εμπιστοσύνης, και ακόμη και πλαίσια περιορισμού αν τα χρειάζεστε για οπτικό debugging.

## Βήμα 4: Εξαγωγή του Αναγνωρισμένου Κειμένου

Ας δούμε τι βρήκε η μηχανή. Θα εκτυπώσουμε το κείμενο στην κονσόλα, αλλά μπορείτε επίσης να το γράψετε σε αρχείο ή βάση δεδομένων.

```python
# Step 4: Output the recognized text, which should include characters like “Ŀ”, “Ҕ”, “Ǣ”
print("=== OCR Result ===")
print(result.text)
```

### Αναμενόμενο Αποτέλεσμα

```
=== OCR Result ===
Hello, world! Ŀ is a Latin‑extended character.
Привет, мир! Ҕ is a Cyrillic character.
Special combo: Ǣ is a ligature.
```

Αν δείτε κάτι παρόμοιο, συγχαρητήρια—έχετε επιτυχώς **μετατρέψει εικόνα σε κείμενο** και **αναγνωρίσει ειδικούς χαρακτήρες**.

## Διαχείριση Συνηθισμένων Προκλήσεων

Ακόμη και με ένα απλό script, μπορεί να συναντήσετε μερικά εμπόδια. Παρακάτω μερικές πρακτικές συμβουλές από τη δική μου εμπειρία.

### 1. Έλλειψη Πακέτων Γλώσσας

Αν βλέπετε ερωτηματικά (`?`) αντί για κυριλλικά γράμματα, ελέγξτε ξανά ότι τα πακέτα γλώσσας είναι εγκατεστημένα. Για πολλές μηχανές OCR πρέπει να κατεβάσετε τα αντίστοιχα αρχεία `.traineddata` και να τα τοποθετήσετε στο φάκελο `tessdata` της μηχανής.

```python
# Example for pytesseract
import pytesseract
pytesseract.pytesseract.tesseract_cmd = r"C:\Program Files\Tesseract-OCR\tesseract.exe"
# Ensure 'eng' and 'rus' data files exist in tessdata
```

### 2. Χαμηλή Ποιότητα Εικόνας

Θολές ή χαμηλής αντίθεσης εικόνες παράγουν χαμηλές βαθμολογίες εμπιστοσύνης. Προεπεξεργαστείτε την εικόνα με OpenCV:

```python
import cv2

# Load, convert to grayscale, and apply thresholding
raw = cv2.imread(image_path)
gray = cv2.cvtColor(raw, cv2.COLOR_BGR2GRAY)
_, thresh = cv2.threshold(gray, 150, 255, cv2.THRESH_BINARY)

# Save a temporary cleaned image and feed it to the OCR engine
cv2.imwrite("cleaned.png", thresh)
engine.load_image("cleaned.png")
```

### 3. Μεγάλα Αρχεία και Χρήση Μνήμης

Η επεξεργασία μιας φωτογραφίας 10 MB μπορεί να αυξήσει τη μνήμη. Χρησιμοποιήστε `engine.set_max_image_size(2000)` για να περιορίσετε την ανάλυση, ή χωρίστε την εικόνα σε πλακίδια και κάντε OCR σε κάθε πλακίδιο ξεχωριστά.

### 4. Λήψη Πλαισίων Περιορισμού (Bounding Boxes)

Αν χρειάζεστε να επισημάνετε πού εμφανίζεται κάθε λέξη (χρήσιμο για UI overlays), προσπελάστε το `result.boxes`:

```python
for box in result.boxes:
    print(f"Word: {box.text} – Coordinates: {box.x0},{box.y0},{box.x1},{box.y1}")
```

## Πλήρες Script – Εκτέλεση με Ένα Κλικ

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι ένα μοναδικό αρχείο που μπορείτε να τρέξετε ως `python ocr_demo.py`. Περιλαμβάνει διαχείριση σφαλμάτων, προαιρετική προεπεξεργασία, και σχόλια για σαφήνεια.

```python
#!/usr/bin/env python3
"""
Complete OCR demo: load image, recognize multilingual text,
and print results. Works with the generic 'ocr' library.
"""

import os
import sys
import ocr

def main(image_path: str):
    # Verify the image exists
    if not os.path.isfile(image_path):
        sys.exit(f"Error: File not found – {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()
    engine.set_languages(['eng', 'rus'])          # load language packs
    engine.set_max_image_size(2500)               # limit memory usage

    # Load the image
    try:
        engine.load_image(image_path)
    except Exception as e:
        sys.exit(f"Failed to load image: {e}")

    # Perform recognition
    try:
        result = engine.recognize()
    except Exception as e:
        sys.exit(f"OCR failed: {e}")

    # Output the text
    print("\n=== OCR Result ===")
    print(result.text)

    # Optional: display confidence scores
    if hasattr(result, "confidence"):
        avg_conf = sum(result.confidence) / len(result.confidence)
        print(f"\nAverage confidence: {avg_conf:.1%}")

if __name__ == "__main__":
    # Replace with your actual image path or pass as CLI argument
    img = sys.argv[1] if len(sys.argv) > 1 else "YOUR_DIRECTORY/multilingual.png"
    main(img)
```

Τρέξτε το με:

```bash
python ocr_demo.py path/to/multilingual.png
```

Θα πρέπει να δείτε το ίδιο αποτέλεσμα που εμφανίστηκε νωρίτερα, επιβεβαιώνοντας ότι έχετε **εξάγει κείμενο από εικόνα** με επιτυχία.

## Συμπέρασμα

Καλύψαμε **πώς να εκτελέσετε OCR** σε Python από την αρχή μέχρι το τέλος: εγκατάσταση της βιβλιοθήκης, φόρτωση εικόνας, αναγνώριση πολυγλωσσικού περιεχομένου, και διαχείριση των πιο συχνών edge cases. Ακολουθώντας αυτόν τον οδηγό μπορείτε τώρα να **μετατρέψετε εικόνα σε κείμενο**, **αναγνωρίσετε ειδικούς χαρακτήρες**, και **εξάγετε κείμενο από εικόνα** στα δικά σας έργα—χωρίς περισσότερη χειροκίνητη μεταγραφή.

Τι ακολουθεί; Δοκιμάστε:

- Προσθήκη περισσότερων πακέτων γλώσσας (π.χ., `spa` για Ισπανικά).  
- Εξαγωγή αποτελεσμάτων σε JSON για επεξεργασία downstream.  
- Ενσωμάτωση του βήματος OCR σε Flask API ώστε άλλες υπηρεσίες να το καλούν.  

Αν αντιμετωπίσετε οποιοδήποτε πρόβλημα, η κοινότητα γύρω από τις περισσότερες βιβλιοθήκες OCR είναι ενεργή—αναζητήστε “ocr library language pack installation” ή αφήστε ένα σχόλιο παρακάτω. Καλή προγραμματιστική δουλειά, και απολαύστε τη μετατροπή εικόνων σε αναζητήσιμο κείμενο!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}