---
category: general
date: 2026-03-28
description: Εκτελέστε OCR σε εικόνα και λάβετε καθαρό κείμενο με συντεταγμένες περιοριστικού
  πλαισίου. Μάθετε πώς να εξάγετε OCR, να καθαρίζετε OCR και να εμφανίζετε τα αποτελέσματα
  βήμα‑βήμα.
draft: false
keywords:
- perform OCR on image
- how to extract OCR
- how to clean OCR
- display bounding box coordinates
- OCR post‑processing
- OCR bounding boxes
language: el
og_description: Εκτελέστε OCR σε εικόνα, καθαρίστε το αποτέλεσμα και εμφανίστε τις
  συντεταγμένες του πλαισίου σε ένα σύντομο οδηγό.
og_title: Πραγματοποιήστε OCR σε εικόνα – Καθαρά αποτελέσματα και πλαίσια οριοθέτησης
tags:
- OCR
- Computer Vision
- Python
title: Εκτέλεση OCR σε εικόνα – Καθαρά αποτελέσματα και εμφάνιση συντεταγμένων πλαισίου
  περιορισμού
url: /el/python/general/perform-ocr-on-image-clean-results-and-show-bounding-box-coo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε Εικόνα – Καθαρά Αποτελέσματα και Εμφάνιση Συντεταγμένων Πλαισίου Περιγράμματος

Έχετε ποτέ χρειαστεί να **εκτελέσετε OCR σε εικόνα** αλλά να λαμβάνετε ακατάστατο κείμενο και να μην ξέρετε πού βρίσκεται κάθε λέξη στην εικόνα; Δεν είστε μόνοι. Σε πολλά έργα—ψηφιοποίηση τιμολογίων, σάρωση αποδείξεων ή απλή εξαγωγή κειμένου—η λήψη του ακατέργαστου αποτελέσματος OCR είναι μόνο το πρώτο εμπόδιο. Τα καλά νέα; Μπορείτε να καθαρίσετε αυτό το αποτέλεσμα και να δείτε αμέσως τις συντεταγμένες του πλαισίου περιγράμματος κάθε περιοχής χωρίς να γράψετε πολύ κώδικα boilerplate.

Σε αυτόν τον οδηγό θα περάσουμε από το **πώς να εξάγετε OCR**, θα τρέξουμε έναν **πώς να καθαρίσετε OCR** μετα‑επεξεργαστή, και τελικά **να εμφανίσουμε τις συντεταγμένες του πλαισίου περιγράμματος** για κάθε καθαρή περιοχή. Στο τέλος θα έχετε ένα ενιαίο, εκτελέσιμο σενάριο που μετατρέπει μια θολή φωτογραφία σε τακτικό, δομημένο κείμενο έτοιμο για επεξεργασία downstream.

## Τι Θα Χρειαστείτε

- Python 3.9+ (η σύνταξη παρακάτω λειτουργεί σε 3.8 και νεότερες εκδόσεις)
- Μια μηχανή OCR που υποστηρίζει `recognize(..., return_structured=True)` – για παράδειγμα, μια φανταστική βιβλιοθήκη `engine` που χρησιμοποιείται στο απόσπασμα. Αντικαταστήστε την με Tesseract, EasyOCR ή οποιοδήποτε SDK που επιστρέφει δεδομένα περιοχής.
- Βασική εξοικείωση με συναρτήσεις και βρόχους της Python
- Ένα αρχείο εικόνας που θέλετε να σαρώσετε (PNG, JPG κ.λπ.)

> **Pro tip:** Αν χρησιμοποιείτε Tesseract, η συνάρτηση `pytesseract.image_to_data` παρέχει ήδη πλαίσια περιγράμματος. Μπορείτε να τυλίξετε το αποτέλεσμα της σε έναν μικρό προσαρμογέα που μιμείται το API `engine.recognize` που φαίνεται παρακάτω.

---

![παράδειγμα εκτέλεσης OCR σε εικόνα](image-placeholder.png "παράδειγμα εκτέλεσης OCR σε εικόνα")

*Alt text: diagram showing how to perform OCR on image and visualize bounding box coordinates*

## Βήμα 1 – Εκτέλεση OCR σε Εικόνα και Λήψη Δομημένων Περιοχών

Το πρώτο που πρέπει να κάνετε είναι να ζητήσετε από τη μηχανή OCR να επιστρέψει όχι μόνο απλό κείμενο, αλλά μια δομημένη λίστα περιοχών κειμένου. Αυτή η λίστα περιέχει τη ακατέργαστη συμβολοσειρά και το ορθογώνιο που την περιβάλλει.

```python
import engine   # replace with your actual OCR library
from pathlib import Path

# Load the image you want to process
image_path = Path("sample_invoice.jpg")
image = engine.load_image(image_path)

# Step 1: Perform OCR and request a structured list of text regions
raw_result = engine.recognize(image, return_structured=True)
```

**Γιατί αυτό είναι σημαντικό:**  
Όταν ζητάτε μόνο απλό κείμενο χάνετε το χωρικό πλαίσιο. Τα δομημένα δεδομένα σας επιτρέπουν να **εμφανίσετε τις συντεταγμένες του πλαισίου περιγράμματος**, να ευθυγραμμίσετε το κείμενο με πίνακες ή να δώσετε ακριβείς θέσεις σε ένα downstream μοντέλο.

## Βήμα 2 – Πώς να Καθαρίσετε το Αποτέλεσμα OCR με έναν Μετα‑Επεξεργαστή

Οι μηχανές OCR είναι εξαιρετικές στο να εντοπίζουν χαρακτήρες, αλλά συχνά αφήνουν περιττά κενά, τεχνάσματα αλλαγής γραμμής ή λανθασμένα αναγνωρισμένα σύμβολα. Ένας μετα‑επεξεργαστής κανονικοποιεί το κείμενο, διορθώνει κοινά σφάλματα OCR και αφαιρεί λευκούς χαρακτήρες.

```python
# Step 2: Clean the plain‑text of each region using the post‑processor
processed_result = engine.run_postprocessor(raw_result)
```

Αν δημιουργείτε τον δικό σας καθαριστή, σκεφτείτε:

- Αφαίρεση μη‑ASCII χαρακτήρων (`re.sub(r'[^\x00-\x7F]+',' ', text)`)
- Συμπίεση πολλαπλών κενών σε ένα ενιαίο κενό
- Εφαρμογή ελεγκτή ορθογραφίας όπως `pyspellchecker` για προφανή τυπογραφικά λάθη

**Γιατί πρέπει να σας ενδιαφέρει:**  
Μια τακτική συμβολοσειρά κάνει την αναζήτηση, την ευρετηρίαση και τις downstream pipelines NLP πολύ πιο αξιόπιστες. Με άλλα λόγια, το **πώς να καθαρίσετε OCR** είναι συχνά η διαφορά μεταξύ ενός χρήσιμου συνόλου δεδομένων και ενός κεφαλαλγίας.

## Βήμα 3 – Εμφάνιση Συντεταγμένων Πλαισίου Περιγράμματος για Κάθε Καθαρή Περιοχή

Τώρα που το κείμενο είναι τακτοποιημένο, επαναλαμβάνουμε πάνω από κάθε περιοχή, εκτυπώνοντας το ορθογώνιο της και τη καθαρή συμβολοσειρά. Αυτό είναι το τμήμα όπου τελικά **εμφανίζουμε τις συντεταγμένες του πλαισίου περιγράμματος**.

```python
# Step 3 – Iterate over the cleaned regions and display their bounding box and text
for text_region in processed_result.regions:
    # Each region has a .bounding_box attribute (x, y, width, height)
    bbox = text_region.bounding_box
    print(f"[{bbox}] {text_region.text}")
```

**Δείγμα εξόδου**

```
[(34, 120, 210, 30)] Invoice #12345
[(34, 160, 420, 28)] Date: 2026‑03‑01
[(34, 200, 380, 28)] Total Amount: $1,254.00
```

Μπορείτε τώρα να περάσετε αυτές τις συντεταγμένες σε μια βιβλιοθήκη σχεδίασης (π.χ., OpenCV) για να επικάλυψετε πλαίσια στην αρχική εικόνα, ή να τις αποθηκεύσετε σε μια βάση δεδομένων για μελλοντικά ερωτήματα.

## Πλήρες, Έτοιμο‑για‑Εκτέλεση Σενάριο

Παρακάτω είναι το πλήρες πρόγραμμα που ενώνει τα τρία βήματα. Αντικαταστήστε τις κλήσεις placeholder `engine` με το πραγματικό σας OCR SDK.

```python
#!/usr/bin/env python3
"""
Perform OCR on image → clean results → display bounding box coordinates.
Author: Your Name
Date: 2026‑03‑28
"""

import engine               # <-- replace with your OCR library
from pathlib import Path
import sys

def main(image_path: str):
    # Load image
    image = engine.load_image(Path(image_path))

    # 1️⃣ Perform OCR and ask for structured output
    raw_result = engine.recognize(image, return_structured=True)

    # 2️⃣ Clean the raw text using the built‑in post‑processor
    processed_result = engine.run_postprocessor(raw_result)

    # 3️⃣ Show each region's bounding box and cleaned text
    print("\n=== Cleaned OCR Regions ===")
    for region in processed_result.regions:
        bbox = region.bounding_box  # (x, y, w, h)
        print(f"[{bbox}] {region.text}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python perform_ocr.py <image_file>")
        sys.exit(1)
    main(sys.argv[1])
```

### Πώς να Εκτελέσετε

```bash
python perform_ocr.py sample_invoice.jpg
```

Θα πρέπει να δείτε μια λίστα πλαισίων περιγράμματος συνδεδεμένων με καθαρό κείμενο, ακριβώς όπως το δείγμα εξόδου παραπάνω.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

| Ερώτηση | Απάντηση |
|----------|--------|
| **Τι γίνεται αν η μηχανή OCR δεν υποστηρίζει `return_structured`;** | Γράψτε έναν ελαφρύ wrapper που μετατρέπει το ακατέργαστο αποτέλεσμα της μηχανής (συνήθως μια λίστα λέξεων με συντεταγμένες) σε αντικείμενα με ιδιότητες `text` και `bounding_box`. |
| **Μπορώ να λάβω βαθμολογίες εμπιστοσύνης;** | Πολλά SDK εκθέτουν ένα μέτρο εμπιστοσύνης ανά περιοχή. Προσθέστε το στη δήλωση εκτύπωσης: `print(f"[{bbox}] {region.text} (conf: {region.confidence:.2f})")`. |
| **Πώς να διαχειριστείτε κείμενο με περιστροφή;** | Προεπεξεργαστείτε την εικόνα με το `cv2.minAreaRect` του OpenCV για διόρθωση κλίσης πριν καλέσετε το `recognize`. |
| **Τι γίνεται αν χρειάζομαι το αποτέλεσμα σε JSON;** | Σειριοποιήστε το `processed_result.regions` με `json.dumps([r.__dict__ for r in processed_result.regions], indent=2)`. |
| **Υπάρχει τρόπος να οπτικοποιήσετε τα πλαίσια;** | Χρησιμοποιήστε το OpenCV: `cv2.rectangle(img, (x, y), (x+w, y+h), (0,255,0), 2)` μέσα στον βρόχο, μετά `cv2.imwrite("annotated.jpg", img)`. |

## Συμπερασματικά

Μόλις μάθατε **πώς να εκτελέσετε OCR σε εικόνα**, να καθαρίσετε το ακατέργαστο αποτέλεσμα, και **να εμφανίσετε τις συντεταγμένες του πλαισίου περιγράμματος** για κάθε περιοχή. Η τριπλή ροή—recognize → post‑process → iterate—είναι ένα επαναχρησιμοποιήσιμο μοτίβο που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Python που χρειάζεται αξιόπιστη εξαγωγή κειμένου.

### Τι Ακολουθεί;

- **Εξερευνήστε διαφορετικά OCR back‑ends** (Tesseract, EasyOCR, Google Vision) και συγκρίνετε την ακρίβεια.
- **Ενσωματώστε με μια βάση δεδομένων** για αποθήκευση δεδομένων περιοχής για αναζητήσιμα αρχεία.
- **Προσθέστε ανίχνευση γλώσσας** για να κατευθύνετε κάθε περιοχή μέσω του κατάλληλου ελεγκτή ορθογραφίας.
- **Επικάλυψη πλαισίων στην αρχική εικόνα** για οπτική επαλήθευση (δείτε το απόσπασμα OpenCV παραπάνω).

Αν αντιμετωπίσετε ιδιομορφίες, θυμηθείτε ότι η μεγαλύτερη νίκη προέρχεται από ένα ισχυρό βήμα μετα‑επεξεργασίας· μια καθαρή συμβολοσειρά είναι πολύ πιο εύκολο να δουλέψει από μια ακατέργαστη ροή χαρακτήρων.

Καλό προγραμματισμό, και εύχομαι οι OCR pipelines σας να είναι πάντα τακτικοί!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}