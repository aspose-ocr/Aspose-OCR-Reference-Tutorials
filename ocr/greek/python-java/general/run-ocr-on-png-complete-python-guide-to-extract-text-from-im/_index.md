---
category: general
date: 2026-01-12
description: Εκτελέστε OCR σε αρχεία PNG γρήγορα με Python. Μάθετε πώς να εξάγετε
  κείμενο από εικόνα και τιμολόγιο και να φορτώνετε εικόνα για OCR χρησιμοποιώντας
  το Aspose.OCR.
draft: false
keywords:
- run OCR on PNG
- extract text from image
- extract text from invoice
- load image for OCR
- Aspose OCR Python
- JSON to CSV conversion
language: el
og_description: Εκτελέστε OCR σε PNG άμεσα. Αυτός ο οδηγός δείχνει πώς να εξάγετε
  κείμενο από εικόνα και τιμολόγιο, να φορτώσετε την εικόνα για OCR και να αποθηκεύσετε
  τα αποτελέσματα ως JSON και CSV.
og_title: Εκτέλεση OCR σε PNG – Πλήρης οδηγός Python
tags:
- OCR
- Python
- Image Processing
title: Εκτελέστε OCR σε PNG – Πλήρης Οδηγός Python για την Εξαγωγή Κειμένου από Εικόνες
url: /el/python-java/general/run-ocr-on-png-complete-python-guide-to-extract-text-from-im/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε PNG – Πλήρης Οδηγός Python για Εξαγωγή Κειμένου από Εικόνες

Έχετε ποτέ χρειαστεί να **run OCR on PNG** αρχεία αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη θα σας δώσει καθαρά, δομημένα αποτελέσματα; Δεν είστε μόνοι. Σε πολλά πραγματικά έργα—σκεφτείτε αυτοματοποίηση τιμολογίων ή σάρωση αποδείξεων—το πρώτο βήμα είναι να **extract text from image** αρχεία, και το PNG είναι μια κοινή μορφή επειδή διατηρεί την απώλεια ποιότητας.

Σε αυτό το tutorial θα περάσουμε από ένα πρακτικό παράδειγμα χρησιμοποιώντας το πακέτο Aspose.OCR για Python. Στο τέλος του οδηγού θα ξέρετε πώς να **load image for OCR**, να εξάγετε κάθε γραμμή κειμένου, να μετατρέψετε τα δεδομένα σε ένα τακτοποιημένο αντικείμενο JSON και ακόμη να τα αποθηκεύσετε σε CSV για επεξεργασία. Χωρίς περιττές πληροφορίες, μόνο μια πρακτική, έτοιμη προς εκτέλεση λύση.

## Τι Θα Μάθετε

- Πώς να εγκαταστήσετε και να εισάγετε τη βιβλιοθήκη Aspose.OCR.  
- Τα ακριβή βήματα για **run OCR on PNG** και τη διαχείριση του αντικειμένου αποτελέσματος.  
- Τρόπους **extract text from invoice** αρχείων και μορφοποίηση της εξόδου ως JSON ή CSV.  
- Συμβουλές για αντιμετώπιση εικόνων χαμηλής αντίθεσης, πολυγλωσσικών εγγράφων και βαθμολογιών εμπιστοσύνης.  
- Ένα πλήρες, αντιγραφή‑και‑επικόλληση δείγμα κώδικα που μπορείτε να εκτελέσετε σήμερα.

> **Prerequisite:** Python 3.8+ και βασική εξοικείωση με το pip. Αν δεν έχετε χρησιμοποιήσει ποτέ το Aspose, μην ανησυχείτε—αυτός ο οδηγός καλύπτει όλα όσα χρειάζεστε για να ξεκινήσετε.

---

## Βήμα 1 – Εγκατάσταση Aspose.OCR και Προετοιμασία Περιβάλλοντος

Πριν μπορέσουμε να **run OCR on PNG**, η βιβλιοθήκη πρέπει να είναι εγκατεστημένη στο σύστημά σας.

```bash
pip install aspose-ocr
```

> **Pro tip:** Χρησιμοποιήστε ένα εικονικό περιβάλλον (`python -m venv venv`) για να απομονώσετε τις εξαρτήσεις. Αποτρέπει συγκρούσεις εκδόσεων όταν διαχειρίζεστε πολλαπλά έργα.

Αφού εγκατασταθεί, εισάγετε τα modules που θα χρειαστούμε:

```python
# Step 1: Import the OCR and JSON modules
import asposeocr as ocr
import json
```

Εδώ φέρνουμε το `asposeocr` για το βαρέως βάρους έργο και τη ενσωματωμένη βιβλιοθήκη `json` για μετέπειτα σειριοποίηση.

---

## Βήμα 2 – Δημιουργία του OCR Engine και Ορισμός Γλώσσας

Η μηχανή OCR είναι το κύριο στοιχείο που διαβάζει τα pixel. Για τα περισσότερα αγγλικά τιμολόγια, θα θέλετε το πακέτο αγγλικής γλώσσας:

```python
# Step 2: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

> **Why this matters:** Ο καθορισμός της γλώσσας περιορίζει το σύνολο χαρακτήρων, βελτιώνοντας την ακρίβεια και την ταχύτητα επεξεργασίας. Αν χρειαστεί ποτέ να διαχειριστείτε πολυγλωσσικά τιμολόγια, απλώς αντικαταστήστε το `ocr.Language.ENGLISH` με το κατάλληλο enum.

---

## Βήμα 3 – Φόρτωση της Εικόνας για OCR

Τώρα θα **load image for OCR**. Η μέθοδος `Image.load` δέχεται διαδρομή αρχείου και λειτουργεί με PNG, JPEG, BMP και άλλα.

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

> **Edge case:** Αν το PNG είναι ασυνήθιστα μεγάλο (πάνω από 5 MB), σκεφτείτε να το αλλάξετε σε μικρότερο μέγεθος πρώτα για να διατηρήσετε τη χρήση μνήμης σε λογικά επίπεδα. Το Pillow μπορεί να το κάνει αυτό σε μία γραμμή:

```python
# Optional: Resize large PNGs
from PIL import Image as PilImage
pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000), PilImage.ANTIALIAS)
pil_img.save("temp_resized.png")
image = ocr.Image.load("temp_resized.png")
```

---

## Βήμα 4 – Εκτέλεση OCR σε PNG και Λήψη του Αποτελέσματος

Με τη μηχανή έτοιμη και την εικόνα φορτωμένη, ήρθε η ώρα να **run OCR on PNG** και να ανακτήσετε το δομημένο αποτέλεσμα.

```python
# Step 4: Run the OCR process on the loaded image
ocr_result = ocr_engine.process(image)
```

Το αντικείμενο `ocr_result` περιέχει μια συλλογή αντικειμένων `OcrRegion`, το καθένα με το αναγνωρισμένο κείμενο και μια βαθμολογία εμπιστοσύνης (0‑100). Εδώ παίρνετε τα λεπτομερή δεδομένα που χρειάζεστε για **extract text from invoice** γραμμές.

---

## Βήμα 5 – Μετατροπή του Αποτελέσματος σε JSON και Καλαίσθητη Εκτύπωση

Τα περισσότερα downstream συστήματα αγαπούν το JSON, οπότε θα μετατρέψουμε την έξοδο OCR σε μια ωραία μορφοποιημένη συμβολοσειρά.

```python
# Step 5: Convert the OCR result to a formatted JSON string and display it
json_str = ocr_result.to_json()
ocr_data = json.loads(json_str)

# Pretty‑print with indentation
print(json.dumps(ocr_data, indent=2))
```

### Δείγμα Εξόδου

```json
{
  "pages": [
    {
      "regions": [
        {
          "text": "Invoice #12345",
          "confidence": 98.7,
          "bounds": { "x": 50, "y": 20, "width": 200, "height": 30 }
        },
        {
          "text": "Date: 2025‑12‑01",
          "confidence": 96.4,
          "bounds": { "x": 50, "y": 60, "width": 180, "height": 25 }
        },
        {
          "text": "Total Amount: $1,250.00",
          "confidence": 99.1,
          "bounds": { "x": 50, "y": 300, "width": 250, "height": 30 }
        }
      ]
    }
  ]
}
```

Παρατηρήστε πώς κάθε γραμμή περιλαμβάνει ένα μετρικό εμπιστοσύνης—τέλειο για φιλτράρισμα χαμηλής εμπιστοσύνης αν σκοπεύετε να **extract text from invoice** αυτόματα.

---

## Βήμα 6 – Αποθήκευση των Δεδομένων OCR ως CSV (Μία Γραμμή ανά Κείμενο + Εμπιστοσύνη)

Το CSV είναι ιδανικό για υπολογιστικά φύλλα ή γρήγορες εισαγωγές δεδομένων. Το Aspose προσφέρει μια εντολή μίας γραμμής για να αποθηκεύσετε τα πάντα σε αρχείο CSV.

```python
# Step 6: Save the OCR result as a CSV file (each line → text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
ocr_result.save_as_csv(csv_path)
```

Το παραγόμενο CSV θα μοιάζει με αυτό:

```
"Invoice #12345",98.7
"Date: 2025-12-01",96.4
"Total Amount: $1,250.00",99.1
```

Τώρα μπορείτε να το ανοίξετε στο Excel, Google Sheets ή να το φορτώσετε σε βάση δεδομένων.

---

## Bonus – Διαχείριση Κειμένου Χαμηλής Εμπιστοσύνης και Πολυσελίδων PDF

### Φιλτράρισμα κατά Εμπιστοσύνη

Αν θέλετε μόνο γραμμές υψηλής βεβαιότητας, φιλτράρετε το JSON πριν το γράψετε:

```python
high_confidence = [
    region for page in ocr_data["pages"]
    for region in page["regions"]
    if region["confidence"] >= 95
]
print(json.dumps(high_confidence, indent=2))
```

### Πολυσελίδες Έγγραφα

Το Aspose.OCR δημιουργεί αυτόματα μια νέα καταχώρηση `page` για κάθε σελίδα σε PNG ή PDF πολλαπλών σελίδων. Επανάληψη μέσω `ocr_data["pages"]` για επεξεργασία όλων—χωρίς επιπλέον κώδικα.

---

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω είναι το **complete script** που μπορείτε να αντιγράψετε, επικολλήσετε και να τρέξετε αμέσως. Αντικαταστήστε το `YOUR_DIRECTORY` με το φάκελο που περιέχει το PNG αρχείο σας.

```python
import asposeocr as ocr
import json

# 1️⃣ Initialize OCR engine
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH

# 2️⃣ Load the PNG image
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)

# 3️⃣ Perform OCR
result = engine.process(image)

# 4️⃣ Convert to JSON and pretty‑print
json_str = result.to_json()
data = json.loads(json_str)
print("=== OCR JSON Output ===")
print(json.dumps(data, indent=2))

# 5️⃣ Save as CSV (text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
result.save_as_csv(csv_path)
print(f"\n✅ CSV saved to {csv_path}")

# 6️⃣ (Optional) Filter high‑confidence lines
high_conf = [
    r for page in data["pages"]
    for r in page["regions"]
    if r["confidence"] >= 95
]
print("\n=== High‑Confidence Regions ===")
print(json.dumps(high_conf, indent=2))
```

Τρέξτε το script με `python run_ocr.py` και θα δείτε το JSON dump στην κονσόλα, ένα αρχείο CSV στο δίσκο, και μια φιλτραρισμένη λίστα εγγραφών υψηλής εμπιστοσύνης.

---

## Συχνές Ερωτήσεις

**Q: Μπορώ να το χρησιμοποιήσω για να εξάγω κείμενο από μια σαρωμένη απόδειξη αντί για τιμολόγιο;**  
A: Απόλυτα. Η ίδια ροή εργασίας ισχύει—απλώς δείξτε το `image_path` στην απόδειξη PNG. Αν η απόδειξη χρησιμοποιεί διαφορετική γλώσσα, αλλάξτε το `engine.language` αναλόγως.

**Q: Τι γίνεται αν το PNG περιέχει κείμενο περιστρεφόμενο;**  
A: Το Aspose.OCR ανιχνεύει αυτόματα τον προσανατολισμό, αλλά για επίμονες περιπτώσεις μπορείτε να περιστρέψετε την εικόνα χειροκίνητα με το Pillow πριν τη δώσετε στη μηχανή.

**Q: Χρειάζομαι πληρωμένη άδεια για το Aspose.OCR;**  
A: Η βιβλιοθήκη προσφέρει δωρεάν λειτουργία αξιολόγησης με υδατογράφημα στην έξοδο. Για παραγωγική χρήση θα χρειαστείτε άδεια, την οποία μπορείτε να αποκτήσετε από την ιστοσελίδα του Aspose.

---

## Συμπέρασμα

Καλύψαμε όλα όσα χρειάζεστε για να **run OCR on PNG** αρχεία χρησιμοποιώντας Python: εγκατάσταση του SDK, φόρτωση εικόνας, εξαγωγή δομημένου κειμένου και αποθήκευση του αποτελέσματος ως JSON ή CSV. Είτε θέλετε να **extract text from image** για ένα απλό script είτε να **extract text from invoice** για μια αυτοματοποιημένη γραμμή λογιστικής, τα παραπάνω βήματα σας δίνουν μια σταθερή, έτοιμη για παραγωγή βάση.

Επόμενα βήματα που μπορείτε να εξερευνήσετε:

- Ενσωμάτωση της εξόδου CSV με βάση δεδομένων για μαζική αποθήκευση τιμολογίων.  
- Προσθήκη post‑processing με κανονικές εκφράσεις για εξαγωγή ημερομηνιών, ποσών ή αριθμών φορολογικού μητρώου.  
- Χρήση της λειτουργίας `ocr_engine.recognize_barcode` αν τα τιμολόγια σας περιλαμβάνουν QR codes.

Δοκιμάστε το, προσαρμόστε τα όρια εμπιστοσύνης, και δείτε τη ροή επεξεργασίας εγγράφων σας να γίνεται παιχνιδάκι. Έχετε περισσότερες ερωτήσεις ή ένα ενδιαφέρον use‑case να μοιραστείτε; Αφήστε ένα σχόλιο παρακάτω—καλή OCR εμπειρία!

![run OCR on PNG example](run-ocr-on-png.png "run OCR on PNG – visual example of OCR result")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}