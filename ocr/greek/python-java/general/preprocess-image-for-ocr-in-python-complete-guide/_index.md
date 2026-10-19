---
category: general
date: 2026-06-25
description: Προεπεξεργασία εικόνας για OCR και αναγνώριση κειμένου από σαρωμένο έγγραφο
  με χρήση Python. Αναλυτικός οδηγός βήμα‑βήμα με πλήρη κώδικα.
draft: false
keywords:
- preprocess image for OCR
- recognize text from scanned document
- Python OCR tutorial
- image deskewing Python
- OCR preprocessing tips
language: el
og_description: Προεπεξεργασία εικόνας για OCR και αναγνώριση κειμένου από σαρωμένο
  έγγραφο με Python. Ακολουθήστε αυτόν τον λεπτομερή, εκτελέσιμο οδηγό.
og_title: Προεπεξεργασία εικόνας για OCR σε Python – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  headline: Preprocess Image for OCR in Python – Complete Guide
  type: TechArticle
- description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  name: Preprocess Image for OCR in Python – Complete Guide
  steps:
  - name: Create an OCR Engine Instance
    text: '```python import ocr # <-- make sure the OCR library is installed'
  - name: Enable Automatic Deskewing and Binarization
    text: '```python # Step 2: Enable automatic deskewing and binarization to improve
      recognition engine.image_preprocessing = ocr.ImagePreProcessingOptions( auto_deskew=True,
      auto_binarize=True ) ```'
  - name: Load the Skewed Image You Want to Process
    text: '```python # Step 3: Load the skewed image you want to process image_path
      = "YOUR_DIRECTORY/skewed_document.jpg" image = ocr.Image.load(image_path) ```'
  - name: Perform OCR on the Pre‑processed Image
    text: '```python # Step 4: Perform OCR on the pre‑processed image result = engine.recognize(image)
      ```'
  - name: Output the Recognized Text
    text: '```python # Step 5: Output the recognized text print("Deskewed & binarized
      text:", result.text) ```'
  - name: 1. Handling Multiple Languages
    text: 'If your document contains both English and French, configure the engine
      before step 1:'
  - name: 2. Fine‑Tuning Binarization Thresholds
    text: 'Automatic binarization works for most cases, but some old photocopies need
      a custom threshold:'
  - name: 3. Extracting Layout Information
    text: 'Sometimes you need more than raw text—you want to know where each paragraph
      lives on the page. Many engines expose a `result.blocks` collection:'
  - name: 4. Processing a Batch of Files
    text: 'If you have a folder full of scanned PDFs converted to JPEGs, wrap the
      whole flow in a loop:'
  - name: 5. Dealing with Low‑Resolution Scans
    text: 'Low‑resolution images (< 150 dpi) often produce fuzzy characters. A quick
      remedy is to upscale using a high‑quality algorithm before feeding the image
      to the OCR engine:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Προεπεξεργασία εικόνας για OCR σε Python – Πλήρης οδηγός
url: /el/python-java/general/preprocess-image-for-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προεπεξεργασία Εικόνας για OCR σε Python – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ πώς να **preprocess image for OCR** ώστε το κείμενο να βγαίνει καθαρό και αξιόπιστο; Δεν είστε μόνοι—οι περισσότεροι προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν η σαρωμένη σελίδα είναι στραβή ή η αντίθεση είναι ακανόνιστη. Τα καλά νέα είναι ότι με λίγες γραμμές Python μπορείτε να διορθώσετε αυτό το χάος, να δυαδικοποιήσετε την εικόνα και να λάβετε καθαρό, αναζητήσιμο κείμενο.

Σε αυτό το tutorial θα περάσουμε από τα ακριβή βήματα για **preprocess image for OCR** *και* **recognize text from scanned document** αρχεία, χρησιμοποιώντας μια δημοφιλής βιβλιοθήκη OCR. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση script, θα καταλάβετε γιατί κάθε ρύθμιση είναι σημαντική, και θα ξέρετε πώς να το προσαρμόσετε σε δύσκολες περιπτώσεις.

## Τι Θα Χρειαστείτε

- Python 3.8 ή νεότερο (ο κώδικας λειτουργεί επίσης σε 3.10+)
- Ένα πακέτο OCR που εκθέτει τις κλάσεις `OcrEngine`, `ImagePreProcessingOptions` και `Image` (π.χ., το φανταστικό module `ocr` που χρησιμοποιείται στο παράδειγμα)
- Ένα σαρωμένο ή φωτογραφημένο έγγραφο που είναι λίγο στραβό ή χαμηλής αντίθεσης
- Το αγαπημένο σας IDE ή ένα απλό τερματικό—χωρίς απαιτήσεις βαριάς διεπαφής GUI

Αυτό είναι όλο. Χωρίς επιπλέον binaries, χωρίς Docker. Ας βουτήξουμε.

## Προεπεξεργασία Εικόνας για OCR – Βήμα‑βήμα

Παρακάτω είναι η βασική ροή εργασίας χωρισμένη σε πέντε σαφή στάδια. Κάθε στάδιο περιλαμβάνει **γιατί** το κάνουμε, τον ακριβή **κώδικα**, και μια σύντομη **εξήγηση** του τι συμβαίνει στο παρασκήνιο.

### Βήμα 1: Δημιουργία μιας Περίπτωσης OCR Engine

```python
import ocr  # <-- make sure the OCR library is installed

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Γιατί είναι σημαντικό:*  
Το αντικείμενο `OcrEngine` είναι ο εγκέφαλος της λειτουργίας. Φυλάει ρυθμίσεις όπως πακέτα γλώσσας, όρια εμπιστοσύνης, και—το πιο σημαντικό για εμάς—σημαίες προεπεξεργασίας εικόνας. Η δημιουργία του πρώτα μας δίνει ένα καθαρό ξεκίνημα για να ενεργοποιήσουμε τα κόλπα που ακολουθούν.

### Βήμα 2: Ενεργοποίηση Αυτόματης Διόρθωσης Στρέψης και Δυαδικοποίησης

```python
# Step 2: Enable automatic deskewing and binarization to improve recognition
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=True
)
```

*Γιατί είναι σημαντικό:*  
- **Deskewing** περιστρέφει την εικόνα ώστε οι γραμμές κειμένου να γίνουν οριζόντιες. Οι μηχανές OCR δυσκολεύονται όταν η βάση κειμένου κλίνει περισσότερο από λίγους μοίρες.  
- **Binarization** μετατρέπει την εικόνα σε καθαρό μαύρο‑και‑λευκό, αφαιρώντας τον θόρυβο του φόντου που μπορεί να μπερδέψει τους ταξινομητές χαρακτήρων.  
Και οι δύο επιλογές είναι *automatic* σε πολλές σύγχρονες βιβλιοθήκες, αλλά πρέπει να τις ενεργοποιήσετε ρητά—από εδώ και η ρητή ανάθεση.

> **Συμβουλή:** Αν οι πηγές εικόνας είναι ήδη τέλεια ευθυγραμμισμένες, μπορείτε να θέσετε `auto_deskew=False` για να εξοικονομήσετε ένα χιλιοστό του χρόνου επεξεργασίας.

### Βήμα 3: Φόρτωση της Στραβής Εικόνας που Θέλετε να Επεξεργαστείτε

```python
# Step 3: Load the skewed image you want to process
image_path = "YOUR_DIRECTORY/skewed_document.jpg"
image = ocr.Image.load(image_path)
```

*Γιατί είναι σημαντικό:*  
Η μέθοδος `Image.load` διαβάζει το αρχείο στη μνήμη και το τυλίγει σε ένα αντικείμενο που καταλαβαίνει η μηχανή OCR. Εξάγει επίσης μεταδεδομένα όπως DPI, που μπορεί να επηρεάσει τον προεπιλεγμένο παράγοντα κλιμάκωσης για τη διόρθωση στροφής.

> **Edge case:** Αν η εικόνα είναι multi‑page TIFF, θα χρειαστεί να επαναλάβετε για κάθε σελίδα ή να χρησιμοποιήσετε ένα βοηθητικό εργαλείο όπως `ocr.MultiPageImage.load`. Οι ίδιες ρυθμίσεις προεπεξεργασίας εφαρμόζονται σε κάθε σελίδα.

### Βήμα 4: Εκτέλεση OCR στην Προεπεξεργασμένη Εικόνα

```python
# Step 4: Perform OCR on the pre‑processed image
result = engine.recognize(image)
```

*Γιατί είναι σημαντικό:*  
Σε αυτό το σημείο η μηχανή εφαρμόζει τα βήματα deskew και binarization που ενεργοποιήσαμε νωρίτερα, και στη συνέχεια τρέχει το νευρωνικό δίκτυό της (ή το κλασικό pipeline τύπου Tesseract) πάνω στο καθαρό bitmap. Το αντικείμενο `result` που επιστρέφεται περιέχει συνήθως το απλό κείμενο, τις βαθμολογίες εμπιστοσύνης, και μερικές φορές τα δεδομένα θέσης για κάθε λέξη.

> **Τι γίνεται αν το κείμενο παραμένει ακατάληπτο;**  
Ελέγξτε την ανάλυση της εικόνας: το OCR λειτουργεί καλύτερα στα 300 dpi ή περισσότερο. Αν η πηγή σας είναι χαμηλότερη, σκεφτείτε να κάνετε upscale πριν τη φόρτωση, ή ζητήστε το αρχικό scan από την πηγή του εγγράφου.

### Βήμα 5: Έξοδος του Αναγνωρισμένου Κειμένου

```python
# Step 5: Output the recognized text
print("Deskewed & binarized text:", result.text)
```

*Γιατί είναι σημαντικό:*  
`result.text` είναι μια απλή συμβολοσειρά που αντιπροσωπεύει ό,τι διάβασε η μηχανή. Η εκτύπωσή του είναι χρήσιμη για γρήγορο debugging· σε μια πραγματική εφαρμογή πιθανότατα θα το γράψετε σε αρχείο `.txt`, σε βάση δεδομένων, ή θα το περάσετε σε μια επόμενη NLP pipeline.

---

## Αναγνώριση Κειμένου από Σαρωμένο Έγγραφο – Πέρα από τα Βασικά

Τώρα που η βασική ροή λειτουργεί, ας εξερευνήσουμε μερικές κοινές παραλλαγές που μπορεί να συναντήσετε όταν προσπαθείτε να **recognize text from scanned document** εικόνες στο φυσικό περιβάλλον.

### 1. Διαχείριση Πολλαπλών Γλωσσών

Αν το έγγραφό σας περιέχει τόσο Αγγλικά όσο και Γαλλικά, ρυθμίστε τη μηχανή πριν το βήμα 1:

```python
engine = ocr.OcrEngine(languages=["eng", "fra"])
```

Οι περισσότερες μηχανές OCR δέχονται κωδικούς ISO‑639‑2· η φόρτωση επιπλέον πακέτων γλώσσας προσθέτει μικρό κόστος, αλλά βελτιώνει δραματικά την ακρίβεια σε πολύγλωσσες σελίδες.

### 2. Λεπτομερής Ρύθμιση Κατωφλίου Δυαδικοποίησης

Η αυτόματη δυαδικοποίηση λειτουργεί στις περισσότερες περιπτώσεις, αλλά μερικές παλιές φωτοαντιγραφές χρειάζονται προσαρμοσμένο κατώφλι:

```python
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=False,          # turn off auto
    binarization_threshold=180   # manual threshold (0‑255)
)
```

Δοκιμάστε τιμές μεταξύ 120 και 220 μέχρι το φόντο να εξαφανιστεί χωρίς να σβήνει τους αδύναμους χαρακτήρες.

### 3. Εξαγωγή Πληροφοριών Διάταξης

Μερικές φορές χρειάζεστε περισσότερα από το ακατέργαστο κείμενο—θέλετε να ξέρετε πού βρίσκεται κάθε παράγραφος στη σελίδα. Πολλές μηχανές εκθέτουν μια συλλογή `result.blocks`:

```python
for block in result.blocks:
    print(f"Block at ({block.x}, {block.y}) size {block.width}x{block.height}")
    print(block.text)
```

Αυτό είναι ανεκτίμητο για την ανασύνθεση πινάκων ή τη διατήρηση της σειράς των στηλών.

### 4. Επεξεργασία Παρτίδας Αρχείων

Αν έχετε έναν φάκελο γεμάτο σαρωμένα PDF μετατρεπόμενα σε JPEG, τυλίξτε όλη τη ροή σε έναν βρόχο:

```python
import pathlib

folder = pathlib.Path("YOUR_DIRECTORY")
for img_file in folder.glob("*.jpg"):
    img = ocr.Image.load(str(img_file))
    txt = engine.recognize(img).text
    (folder / f"{img_file.stem}.txt").write_text(txt, encoding="utf-8")
    print(f"Processed {img_file.name}")
```

Ο βρόχος επαναχρησιμοποιεί την ίδια παρουσία `engine`, κάτι που είναι πιο αποδοτικό από το να τη δημιουργείτε ξανά για κάθε αρχείο.

### 5. Αντιμετώπιση Χαμηλής Ανάλυσης Σαρώσεων

Οι εικόνες χαμηλής ανάλυσης (< 150 dpi) συχνά παράγουν θολούς χαρακτήρες. Μια γρήγορη λύση είναι το upscale χρησιμοποιώντας αλγόριθμο υψηλής ποιότητας πριν τροφοδοτήσετε την εικόνα στη μηχανή OCR:

```python
from PIL import Image as PilImage

pil_img = PilImage.open("low_res.jpg")
upscaled = pil_img.resize((pil_img.width * 2, pil_img.height * 2), PilImage.LANCZOS)
upscaled.save("upscaled.jpg")
image = ocr.Image.load("upscaled.jpg")
```

Το upscale δεν δημιουργεί μαγικά λεπτομέρειες, αλλά το βήμα δυαδικοποίησης μπορεί να δουλέψει με πιο καθαρά άκρα, προσφέροντας μια ήπια βελτίωση.

## Αναμενόμενη Έξοδος

Η εκτέλεση του αρχικού πενταβήματου script σε μια μέτρια στραβή σάρωση 300 dpi θα πρέπει να εκτυπώσει κάτι όπως:

```
Deskewed & binarized text: 
Dear Customer,

Thank you for your recent purchase. Please find your receipt attached.

Best regards,
Acme Corp.
```

Αν δείτε ακατάληπτους χαρακτήρες, ελέγξτε ξανά τις σημαίες προεπεξεργασίας, την ανάλυση της εικόνας και τη ρύθμιση γλώσσας.

## Συμπέρασμα

Καλύψαμε όλα όσα χρειάζεστε για **preprocess image for OCR** και **recognize text from scanned document** αρχεία χρησιμοποιώντας Python. Ξεκινώντας από μια φρέσκια παρουσία engine, ενεργοποιήσαμε αυτόματη διόρθωση στροφής και δυαδικοποίηση, φορτώσαμε μια στραβή εικόνα, τρέξαμε την αναγνώριση, και εκτυπώσαμε το καθαρό κείμενο. Στο δρόμο εξερευνήσαμε υποστήριξη πολλαπλών γλωσσών, χειροκίνητες ρυθμίσεις κατωφλίου, εξαγωγή διάταξης, επεξεργασία παρτίδας, και λύσεις για χαμηλή ανάλυση.

Δοκιμάστε το script στις δικές σας σαρώσεις—ίσως μια στοίβα αποδείξεων, μια χειρόγραφη φόρμα, ή ένα παλιό αποσπασματικό άρθρο εφημερίδας. Μόλις νιώσετε άνετα, προσθέστε δημιουργία PDF ή τροφοδοτήστε το αποτέλεσμα σε ευρετήριο αναζήτησης. Ο ουρανός είναι το όριο.

**Έτοιμοι για την επόμενη πρόκληση;** Ρίξτε μια ματιά στα tutorials μας για *«Extract Tables from Scanned PDFs with Python»* και *«Train Custom OCR Models with TensorFlow»* ώστε να συνεχίσετε να επεκτείνετε το εργαλείο αυτοματοποίησης εγγράφων σας.

Καλή προγραμματιστική, και το OCR σας πάντα να είναι καθαρό!

## Τι Θα Πρέπει να Μάθετε Στη Σύντομη Επόμενη

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Βήμα‑βήμα](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Εξαγωγή Κειμένου από Εικόνα – Βελτιστοποίηση OCR με Aspose.OCR για .NET](/ocr/english/net/ocr-optimization/)
- [Πώς να Χρησιμοποιήσετε AspOCR: Φίλτρα Προεπεξεργασίας Εικόνας OCR για .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}