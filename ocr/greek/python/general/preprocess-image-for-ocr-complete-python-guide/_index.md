---
category: general
date: 2026-06-28
description: Προεπεξεργασία εικόνας για OCR με αυτόματη περιστροφή, δυαδικοποίηση
  και αποθορυβοποίηση σε Python. Λάβετε δομημένη έξοδο JSON χρησιμοποιώντας μηχανή
  OCR.
draft: false
keywords:
- preprocess image for OCR
- auto rotate image OCR
- OCR engine Python
- OCR structured JSON output
- image binarization for OCR
- denoise OCR image
language: el
og_description: Προεπεξεργασία εικόνας για OCR με αυτόματη περιστροφή, δυαδικοποίηση
  και αποθορυβοποίηση σε Python. Μάθετε πώς να εξάγετε δομημένο JSON χρησιμοποιώντας
  μια μηχανή OCR.
og_title: Προεπεξεργασία εικόνας για OCR – Πλήρης οδηγός Python
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Preprocess image for OCR with auto‑rotate, binarization and denoising
    in Python. Get structured JSON output using an OCR engine.
  headline: Preprocess Image for OCR – Complete Python Guide
  type: TechArticle
- description: Preprocess image for OCR with auto‑rotate, binarization and denoising
    in Python. Get structured JSON output using an OCR engine.
  name: Preprocess Image for OCR – Complete Python Guide
  steps:
  - name: '**Binarization** – converting the picture to pure black‑and‑white, which
      sharpens character edges.'
    text: '**Binarization** – converting the picture to pure black‑and‑white, which
      sharpens character edges.'
  - name: '**Denoising** – removing speckles that the OCR engine might mistake for
      glyphs.'
    text: '**Denoising** – removing speckles that the OCR engine might mistake for
      glyphs.'
  - name: '**Add language packs** (`engine.set_language(''eng+spa'')`) for multilingual
      documents.'
    text: '**Add language packs** (`engine.set_language(''eng+spa'')`) for multilingual
      documents.'
  - name: '**Integrate with Pandas** to turn the JSON tables into DataFrames for analytics.'
    text: '**Integrate with Pandas** to turn the JSON tables into DataFrames for analytics.'
  - name: '**Run batch processing** by looping over a folder of images and appending
      results to a master JSON file.'
    text: '**Run batch processing** by looping over a folder of images and appending
      results to a master JSON file.'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Προεπεξεργασία εικόνας για OCR – Πλήρης οδηγός Python
url: /el/python/general/preprocess-image-for-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προεπεξεργασία Εικόνας για OCR – Πλήρης Οδηγός Python

Έχετε αναρωτηθεί ποτέ πώς να **preprocess image for OCR** ώστε η μηχανή να διαβάζει πραγματικά ό,τι βλέπετε; Δεν είστε μόνοι—οι περισσότεροι προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν τα σαρωμένα έγγραφά τους εμφανίζονται ακατάληπτα. Τα καλά νέα; Μερικά καλά τοποθετημένα βήματα—auto‑rotate, binarization και denoising—μπορούν να μετατρέψουν μια ακατάστατη φωτογραφία σε καθαρό, μηχανικά αναγνώσιμο κείμενο.

Σε αυτό το tutorial θα περάσουμε βήμα-βήμα από μια ροή εργασίας **Python** που όχι μόνο καθαρίζει την εικόνα, αλλά και σας επιστρέφει ένα καλά δομημένο αρχείο JSON. Στο τέλος θα γνωρίζετε πώς να auto‑rotate μια εικόνα για OCR, να εφαρμόσετε image binarization για OCR, και ακόμη να denoise δεδομένα εικόνας OCR πριν τα δώσετε σε μια **OCR engine Python** παρουσία.

## Τι Θα Χρειαστείτε

- Python 3.9+ (οποιαδήποτε πρόσφατη έκδοση λειτουργεί)
- `Pillow` για διαχείριση εικόνας (`pip install pillow`)
- `ocrutil` – μια φανταστική βιβλιοθήκη βοηθητικών λειτουργιών που περιβάλλει τη μηχανή OCR (εγκατάσταση μέσω `pip install ocrutil`)
- Ένα δείγμα κεκλιμένης εικόνας (`skewed.jpg`) τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε

Αυτό είναι όλο—χωρίς βαριά frameworks, χωρίς μαγεία GPU. Μόνο plain‑vanilla Python και μερικές χρήσιμες βιβλιοθήκες.

## Βήμα 1: Φόρτωση της Εικόνας σας – Προετοιμασία για OCR

Πρώτα απ' όλα: χρειαζόμαστε ένα αντικείμενο εικόνας που η υπόλοιπη αλυσίδα επεξεργασίας μπορεί να επεξεργαστεί.

```python
from PIL import Image
import ocrutil

# Load the image you want to process
img_path = "YOUR_DIRECTORY/skewed.jpg"
img = Image.open(img_path)          # Pillow gives us a convenient Image object
print(f"Loaded image size: {img.size}")
```

*Γιατί είναι σημαντικό:* Η φόρτωση της εικόνας με Pillow εξασφαλίζει ότι διατηρούμε όλα τα αρχικά δεδομένα pixel, κάτι που είναι κρίσιμο όταν αργότερα εφαρμόζουμε binarization. Η παράλειψη αυτού του βήματος ή η χρήση ενός φορτωτή χαμηλής ποιότητας μπορεί ήδη να υπονομεύσει την ακρίβεια του OCR.

## Βήμα 2: Auto‑rotate της Εικόνας για OCR (auto rotate image OCR)

Μια φωτογραφία που τραβήχτηκε με το τηλέφωνο συχνά είναι κλινή ή ακόμη και ανάποδη. Η βοηθητική συνάρτηση `ocrutil.auto_rotate` εντοπίζει τη βάση του κειμένου και περιστρέφει την εικόνα αναλόγως.

```python
# Automatically correct 90°/180° rotation
img = ocrutil.auto_rotate(img)
print("Auto‑rotation applied.")
```

*Συμβουλή:* Αν ξέρετε ότι τα έγγραφά σας είναι πάντα όρθια, μπορείτε να παραλείψετε αυτό το βήμα, αλλά στην πράξη το “auto rotate image OCR” σας εξοικονομεί πολύ χειροκίνητο καθαρισμό.

## Βήμα 3: Προεπεξεργασία Εικόνας για OCR – Binarization + Denoising

Τώρα φτάνουμε στην ουσία: **preprocess image for OCR**. Τα δύο πιο αποτελεσματικά κόλπα είναι:

1. **Binarization** – μετατροπή της εικόνας σε καθαρό μαύρο‑και‑άσπρο, που ενισχύει τις άκρες των χαρακτήρων.
2. **Denoising** – αφαίρεση σκόνης που η μηχανή OCR μπορεί να συγχέει με γλύφους.

```python
# Apply preprocessing: binarization + denoising
img = ocrutil.preprocess(img)   # Under the hood: thresholding + median filter
print("Preprocessing completed.")
```

Αν ρίξετε μια ματιά στην εικόνα μετά από αυτό το βήμα (π.χ., `img.show()`), θα παρατηρήσετε έντονη αντίθεση με το φόντο—ακριβώς αυτό που απαιτεί μια καλή μηχανή OCR.

## Βήμα 4: Ρύθμιση της Μηχανής OCR (OCR engine Python)

Με μια καθαρή εικόνα στα χέρια, δημιουργούμε μια παρουσία της μηχανής OCR. Η κλάση `ocrutil.OcrEngine` περιβάλλει ένα δημοφιλές ανοιχτού κώδικα OCR backend (σκεφτείτε το Tesseract) ενώ εκθέτει ένα φιλικό Python API.

```python
# Create and configure the OCR engine
engine = ocrutil.OcrEngine()
engine.set_image(img)           # Feed the preprocessed image
print("Engine ready for recognition.")
```

*Γιατί το κάνουμε:* Η παροχή της προεπεξεργασμένης εικόνας στο αντικείμενο **OCR engine Python** εγγυάται ότι η μηχανή λειτουργεί με τα υψηλότερης ποιότητας δεδομένα που μπορείτε να προσφέρετε, κάτι που μεταφράζεται άμεσα σε μεγαλύτερη ακρίβεια.

## Βήμα 5: Αναγνώριση Απλού Κειμένου (Προαιρετικό αλλά Χρήσιμο)

Μερικές φορές χρειάζεστε μόνο το ακατέργαστο κείμενο. Αυτό το βήμα είναι προαιρετικό επειδή ο κύριος στόχος του tutorial είναι η δομημένη έξοδος, αλλά είναι χρήσιμο για γρήγορους ελέγχους.

```python
# Get plain text (useful for debugging)
plain_text = engine.recognize()
print("Plain‑text output:\n", plain_text[:200])   # Print first 200 chars
```

Θα δείτε μια συμβολοσειρά που μοιάζει με το αρχικό έγγραφο, αν και χωρίς πληροφορίες διάταξης. Αν το κείμενο φαίνεται ακατάληπτο, επιστρέψτε και προσαρμόστε τις παραμέτρους προεπεξεργασίας.

## Βήμα 6: Εξαγωγή Δομημένων Δεδομένων και Αποθήκευση ως JSON (OCR structured JSON output)

Η πραγματική δύναμη των σύγχρονων μηχανών OCR είναι η ικανότητά τους να επιστρέφουν πληροφορίες διάταξης—πίνακες, στήλες και ακόμη πεδία φόρμας. Η μέθοδος `engine.recognize_structured()` κάνει ακριβώς αυτό, και θα αποθηκεύσουμε το αποτέλεσμα σε ένα τακτοποιημένο αρχείο JSON.

```python
# Recognize structured data (tables, layout) and export to JSON
structured_result = engine.recognize_structured()
output_path = "YOUR_DIRECTORY/out.json"
ocrutil.save_result(structured_result, output_path)
print(f"Structured OCR result saved to {output_path}")
```

Ένα απόσπασμα του JSON μπορεί να μοιάζει ως εξής:

```json
{
  "pages": [
    {
      "blocks": [
        {
          "type": "text",
          "bbox": [12, 34, 560, 120],
          "text": "Invoice #12345"
        },
        {
          "type": "table",
          "bbox": [15, 130, 580, 400],
          "rows": [
            ["Item", "Qty", "Price"],
            ["Widget A", "2", "$19.99"]
          ]
        }
      ]
    }
  ]
}
```

*Τι σας προσφέρει αυτό:* Μια μηχανικά αναγνώσιμη αναπαράσταση που μπορείτε να τροφοδοτήσετε απευθείας σε μια βάση δεδομένων, ένα API ή ένα εργαλείο αναφοράς—χωρίς περαιτέρω χειροκίνητο copy‑paste.

## Bonus: Οπτική Επιβεβαίωση (Image with Alt Text)

Παρακάτω υπάρχει ένα στιγμιότυπο πριν‑και‑μετά της αλυσίδας προεπεξεργασίας. Παρατηρήστε πώς η αντίθεση αυξάνεται και ο θόρυβος εξαφανίζεται.

![Προεπεξεργασία εικόνας για OCR – αρχική vs καθαρισμένη](/images/ocr_preprocess_example.png){: .align-center alt="παράδειγμα προεπεξεργασίας εικόνας για OCR"}

*Αν είστε περίεργοι:* Αντικαταστήστε το `ocrutil.preprocess` με τη δική σας ρουτίνα OpenCV και θα συνεχίσετε να ακολουθείτε την ίδια φιλοσοφία **preprocess image for OCR**—threshold, filter, then feed.

## Συχνά Πιθανά Σφάλματα & Πώς να τα Αποφύγετε

- **Over‑binarizing:** Ο καθορισμός του κατωφλίου πολύ υψηλό μπορεί να διαγράψει αδύνατους χαρακτήρες. Αν δείτε ελλείπουσες γράμματα, μειώστε το κατώφλι στο `ocrutil.preprocess`.
- **Wrong DPI:** Οι μηχανές OCR υποθέτουν ~300 dpi για έντυπο υλικό. Αν η εικόνα σας είναι χαμηλής ανάλυσης, σκεφτείτε upscale πριν από την προεπεξεργασία.
- **Skipping auto‑rotate:** Ακόμη και μια κλίση 5 μοιρών μπορεί να διαταράξει την ανίχνευση γραμμών. Το βήμα “auto rotate image OCR” είναι φθηνό και εξοικονομεί ώρες εντοπισμού σφαλμάτων αργότερα.

## Επέκταση της Ροής Εργασίας

Τώρα που έχετε μια σταθερή βάση, ίσως θέλετε να:

1. **Add language packs** (`engine.set_language('eng+spa')`) για πολυγλωσσικά έγγραφα.  
2. **Integrate with Pandas** για μετατροπή των πινάκων JSON σε DataFrames για αναλύσεις.  
3. **Run batch processing** κάνοντας βρόχο πάνω σε φάκελο εικόνων και προσθέτοντας τα αποτελέσματα σε ένα κύριο αρχείο JSON.

Όλες αυτές οι επεκτάσεις βασίζονται ακόμα στην κεντρική ιδέα: **preprocess image for OCR** πριν καλέσετε τη μηχανή.

## Συμπέρασμα

Μόλις μάθατε πώς να **preprocess image for OCR** σε Python—auto‑rotate, binarize, denoise, και τέλος να δώσετε την καθαρή εικόνα σε μια **OCR engine Python** που παράγει τόσο απλό κείμενο όσο και ένα πλούσιο **OCR structured JSON output**. Ακολουθώντας αυτά τα βήματα, θα βελτιώσετε δραματικά τα ποσοστά αναγνώρισης και θα έχετε δεδομένα έτοιμα για επεξεργασία downstream.

Έτοιμοι να ανεβάσετε το επίπεδο; Δοκιμάστε να αντικαταστήσετε το ενσωματωμένο `ocrutil.preprocess` με μια προσαρμοσμένη αλυσίδα OpenCV, πειραματιστείτε με διαφορετικές τεχνικές binarization, ή τροφοδοτήστε το JSON σε έναν πίνακα ελέγχου αναφορών. Ο ουρανός είναι το όριο, και η βάση που μόλις δημιουργήσατε θα σας προστατεύει από τα ίδια προβλήματα ποιότητας εικόνας ξανά.

Καλό κώδικα, και οι OCR αποτελέσματά σας να είναι πάντα καθαρά!

## Τι Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Βήμα‑βήμα](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Εξαγωγή Κειμένου από Εικόνα – Βελτιστοποίηση OCR με Aspose.OCR για .NET](/ocr/english/net/ocr-optimization/)
- [Πώς να Ορίσετε Τιμή Κατωφλίου στην Αναγνώριση Εικόνας OCR](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}