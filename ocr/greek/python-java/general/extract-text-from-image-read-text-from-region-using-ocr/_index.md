---
category: general
date: 2026-07-05
description: Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας Python OCR. Μάθετε πώς να
  φορτώνετε εικόνα για OCR, να διαβάζετε κείμενο από περιοχή και να εξάγετε κείμενο
  από τιμολόγιο με λίγες γραμμές κώδικα.
draft: false
keywords:
- extract text from image
- read text from region
- load image for ocr
- extract text from invoice
- ocr on region
language: el
og_description: Εξαγωγή κειμένου από εικόνα με Python OCR. Αυτός ο οδηγός δείχνει
  πώς να φορτώσετε εικόνα για OCR, να διαβάσετε κείμενο από περιοχή και να εξάγετε
  κείμενο από τιμολόγιο γρήγορα.
og_title: Εξαγωγή κειμένου από εικόνα – Ανάγνωση κειμένου από περιοχή χρησιμοποιώντας
  OCR
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, read text from region, and extract text from invoice with a few lines of
    code.
  headline: Extract Text from Image – Read Text from Region Using OCR
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Εξαγωγή κειμένου από εικόνα – Ανάγνωση κειμένου από περιοχή χρησιμοποιώντας
  OCR
url: /el/python-java/general/extract-text-from-image-read-text-from-region-using-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Εικόνα – Ανάγνωση Κειμένου από Περιοχή με OCR

Έχετε ποτέ χρειαστεί να **εξάγετε κείμενο από εικόνα** αλλά μόνο ένα συγκεκριμένο τμήμα έχει σημασία—όπως το συνολικό ποσό σε ένα τιμολόγιο; Δεν είστε οι μόνοι. Σε πολλά πραγματικά έργα θα βρείτε ότι χρειάζεται να **διαβάσετε κείμενο από περιοχή** αντί να επεξεργαστείτε ολόκληρη την εικόνα. Ευτυχώς, με λίγες γραμμές Python μπορείτε να φορτώσετε μια εικόνα για OCR, να ορίσετε μια περιοχή ενδιαφέροντος (ROI) και να εξάγετε ακριβώς τους χαρακτήρες που χρειάζεστε.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει πώς να **φορτώσετε εικόνα για OCR**, να ρυθμίσετε ένα ROI και τελικά να **εξάγετε κείμενο από τιμολόγιο**. Στο τέλος θα έχετε ένα έτοιμο κομμάτι κώδικα που λειτουργεί με οποιαδήποτε δημοφιλής βιβλιοθήκη OCR που υποστηρίζει αναγνώριση βάσει περιοχής.

---

## Τι Θα Χρειαστεί

- Python 3.8+ (ο κώδικας λειτουργεί και σε 3.10)  
- Ένα πακέτο OCR που εκθέτει μια κλάση `OcrEngine` (για την επίδειξη θα χρησιμοποιήσουμε ένα φανταστικό module `ocr`; αντικαταστήστε το με `pytesseract`, `easyocr`, ή οποιαδήποτε βιβλιοθήκη που προσφέρει υποστήριξη ROI)  
- Ένα δείγμα εικόνας—π.χ. `invoice.png`—που περιέχει καθαρό, τυπωμένο κείμενο  
- Βασική εξοικείωση με συναρτήσεις και κλάσεις Python (δεν απαιτείται βάθος στη μηχανική μάθηση)

Αν έχετε ήδη όλα αυτά, τέλεια—ας ξεκινήσουμε. Αν όχι, κατεβάστε την τελευταία έκδοση του Python από το python.org και εγκαταστήστε το πακέτο OCR με `pip install your-ocr-lib`.

---

![Εξαγωγή κειμένου από εικόνα παράδειγμα](extract-text-from-image.png "Εξαγωγή κειμένου από εικόνα – επίδειξη OCR βάσει περιοχής")

*Η παραπάνω εικόνα δείχνει την περιοχή (κόκκινο ορθογώνιο) που θα στοχεύσουμε για **εξαγωγή κειμένου από εικόνα**.*

---

## Βήμα 1: Εγκατάσταση και Εισαγωγή της Βιβλιοθήκης OCR

Πρώτα, βεβαιωθείτε ότι η βιβλιοθήκη OCR είναι διαθέσιμη στο περιβάλλον σας. Το πρότυπο εισαγωγής παρακάτω λειτουργεί για τις περισσότερες βιβλιοθήκες που εκθέτουν μια υψηλού επιπέδου κλάση `OcrEngine`.

```python
# Install the library (uncomment if you haven't yet)
# pip install your-ocr-lib

import ocr  # replace `ocr` with the actual module name, e.g., `import easyocr`
```

> **Pro tip:** Αν χρησιμοποιείτε `pytesseract`, θα χρειαστεί να εγκαταστήσετε το εκτελέσιμο Tesseract ξεχωριστά και να ορίσετε το `pytesseract.pytesseract.tesseract_cmd` στη διαδρομή του.

---

## Βήμα 2: Δημιουργία του Μηχανήματος OCR και Ορισμός Γλώσσας

Η δημιουργία του μηχανήματος είναι απλή, αλλά ο καθορισμός της γλώσσας βελτιώνει δραματικά την ακρίβεια, ειδικά για τιμολόγια που περιέχουν αριθμούς και αγγλικές λέξεις.

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Set the language to English – this is crucial for invoice text
ocr_engine.language = ocr.Language.ENGLISH
```

Γιατί το κάνουμε αυτό; Η μηχανή OCR χρησιμοποιεί μοντέλα γλώσσας για την πρόβλεψη χαρακτήρων· λέγοντας της να περιμένει Αγγλικά μειώνουμε τα ψευδώς θετικά, όπως η λανθασμένη ανάγνωση του “0” ως “O”.

---

## Βήμα 3: Φόρτωση Εικόνας για OCR

Τώρα πραγματικά **φορτώνουμε εικόνα για OCR**. Οι περισσότερες βιβλιοθήκες δέχονται διαδρομή αρχείου ή αντικείμενο Pillow. Εδώ χρησιμοποιούμε τον ενσωματωμένο φορτωτή της βιβλιοθήκης για απλότητα.

```python
# Load the source image that contains the text
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)   # replace with cv2.imread or PIL.Image.open if needed
```

Βεβαιωθείτε ότι η διαδρομή δείχνει στον σωστό φάκελο· ένα συχνό λάθος είναι η παράλειψη της σχετικής διαδρομής όταν το script εκτελείται από διαφορετικό working directory.

---

## Βήμα 4: Ορισμός της Περιοχής Ενδιαφέροντος (ROI)

Ο ορισμός του ROI είναι η καρδιά του **read text from region**. Σκεφτείτε το σαν να σχεδιάζετε ένα ορθογώνιο γύρω από το τμήμα του τιμολογίου που περιέχει το συνολικό ποσό.

```python
# Define the ROI (left, top, width, height) in pixels
# Adjust these numbers to match your invoice layout
region_of_interest = ocr.Rectangle(100, 200, 400, 150)
```

- `left` και `top` αντιπροσωπεύουν τις συντεταγμένες X και Y της πάνω‑αριστερής γωνίας του ορθογωνίου.  
- `width` και `height` ορίζουν το μέγεθος του κουτιού.  
- Μπορείτε να πειραματιστείτε με διαφορετικές τιμές χρησιμοποιώντας έναν προβολέα εικόνας που δείχνει τις συντεταγμένες pixel.

> **Γιατί είναι σημαντικό το ROI:** Η εκτέλεση OCR σε ολόκληρη τη σελίδα σπαταλά CPU cycles και συχνά εισάγει θόρυβο από ανεξάρτητο κείμενο, πίνακες ή γραφικά. Εστιάζοντας σε μια περιοχή, παίρνετε πιο καθαρά αποτελέσματα και ταχύτερη επεξεργασία.

---

## Βήμα 5: Εκτέλεση OCR στην Καθορισμένη Περιοχή

Με όλα έτοιμα, τελικά **εξάγουμε κείμενο από εικόνα**—αλλά μόνο μέσα στο ROI που ορίσαμε.

```python
# Recognize text only within the defined ROI
ocr_result = ocr_engine.recognize(image, region_of_interest)
```

Η μέθοδος `recognize` επιστρέφει ένα αντικείμενο που συνήθως περιέχει το ακατέργαστο string, βαθμολογίες εμπιστοσύνης, και μερικές φορές bounding boxes για κάθε λέξη. Για τις ανάγκες μας χρειαζόμαστε μόνο το απλό κείμενο.

---

## Βήμα 6: Εμφάνιση του Εξαγόμενου Κειμένου

Ας τυπώσουμε το αποτέλεσμα και δούμε τι πήραμε. Αυτό το βήμα δείχνει **extract text from invoice** σε πραγματικό σενάριο.

```python
# Output the extracted text
print("Text inside ROI:")
print(ocr_result.text)
```

### Αναμενόμενο Αποτέλεσμα

```
Text inside ROI:
Total Amount: $1,245.67
```

Αν το τιμολόγιό σας έχει διαφορετική διάταξη, θα δείτε όποιο κείμενο βρίσκεται μέσα στο ορθογώνιο—ίσως αριθμό τιμολογίου, ημερομηνία ή αναφορά PO.

---

## Βήμα 7: Συσκευασία Όλων σε Επαναχρησιμοποιήσιμη Συνάρτηση (Προαιρετικό)

Για να κάνετε τη λύση επαναχρησιμοποιήσιμη σε πολλά τιμολόγια, ενσωματώστε τη λογική σε μια συνάρτηση. Αυτό επίσης δείχνει **ocr on region** ως γενική βοηθητική λειτουργία.

```python
def extract_text_from_region(image_path: str,
                             left: int,
                             top: int,
                             width: int,
                             height: int,
                             language: str = "ENGLISH") -> str:
    """
    Load an image, define a ROI, and return the OCR result as plain text.
    
    Parameters
    ----------
    image_path : str
        Path to the image file.
    left, top, width, height : int
        Coordinates defining the region of interest.
    language : str, optional
        Language code for the OCR engine (default is ENGLISH).
    
    Returns
    -------
    str
        Recognized text inside the ROI.
    """
    # Initialise engine
    engine = ocr.OcrEngine()
    engine.language = getattr(ocr.Language, language.upper(), ocr.Language.ENGLISH)

    # Load image
    img = ocr.Image.load(image_path)

    # Define ROI
    roi = ocr.Rectangle(left, top, width, height)

    # Recognise text
    result = engine.recognize(img, roi)

    return result.text.strip()
```

Τώρα μπορείτε να καλέσετε τη συνάρτηση με οποιοδήποτε τιμολόγιο:

```python
total_text = extract_text_from_region(
    "invoices/2024-03-15.png",
    left=100, top=200, width=400, height=150
)
print("Extracted total:", total_text)
```

---

## Συνηθισμένα Προβλήματα & Πώς να τα Αποφύγετε

| Πρόβλημα | Γιατί Συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| **Κενό αποτέλεσμα** | Το ROI δεν καλύπτει πραγματικό κείμενο (λάθος συντεταγμένες). | Ελέγξτε ξανά τις τιμές pixel με έναν επεξεργαστή εικόνας· προσθέστε οπτική επικάλυψη εντοπισμού σφαλμάτων. |
| **Ασχημοί χαρακτήρες** | Χαμηλή ανάλυση εικόνας ή κακή αντίθεση. | Προεπεξεργασία εικόνας: μετατροπή σε grayscale, εφαρμογή κατωφλίου (`cv2.threshold`). |
| **Λάθος γλώσσα** | Η μηχανή προεπιλέγει γλώσσα χωρίς το απαιτούμενο σύνολο χαρακτήρων. | Ορίστε ρητά `ocr_engine.language` σε `ENGLISH` ή τη σχετική τοπική ρύθμιση. |
| **Καθυστέρηση απόδοσης** | Εκτέλεση OCR σε μεγάλες εικόνες επανειλημμένα. | Αλλάξτε το μέγεθος της εικόνας πριν τη φόρτωση, ή επεξεργαστείτε μόνο το ROI κόβοντας πρώτα. |

---

## Επέκταση του Παραδείγματος: Πολλαπλά ROI

Μερικές φορές ένα τιμολόγιο περιέχει πολλά πεδία που χρειάζεστε—όπως **extract text from invoice** για το συνολικό ποσό και την ημερομηνία τιμολογίου. Μπορείτε να κάνετε βρόχο πάνω σε μια λίστα ορθογωνίων:

```python
fields = {
    "total": ocr.Rectangle(100, 200, 400, 150),
    "date":  ocr.Rectangle(500, 200, 200, 80)
}

for name, rect in fields.items():
    txt = ocr_engine.recognize(image, rect).text.strip()
    print(f"{name.title()} → {txt}")
```

Αυτό το μοτίβο διατηρεί τον κώδικά σας καθαρό και διευκολύνει την προσθήκη περισσότερων περιοχών αργότερα.

---

## Συμπέρασμα

Μόλις καλύψαμε μια πλήρη, end‑to‑end ροή εργασίας για **extract text from image** χρησιμοποιώντας Python OCR, εστιάζοντας σε μια συγκεκριμένη περιοχή. Με το **loading image for OCR**, ορίζοντας μια **region of interest**, και καλώντας τη μηχανή, μπορείτε αξιόπιστα να **read text from region**—ιδανικό για εξαγωγή συνολικών ποσών από τιμολόγια, ημερομηνιών από αποδείξεις, ή οποιοδήποτε άλλο τοπικοποιημένο δεδομένο.

Αισθανθείτε ελεύθεροι να πειραματιστείτε

## Τι Πρέπει να Μάθετε Στη Σύντομη Επόμενη

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετα χαρακτηριστικά API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}