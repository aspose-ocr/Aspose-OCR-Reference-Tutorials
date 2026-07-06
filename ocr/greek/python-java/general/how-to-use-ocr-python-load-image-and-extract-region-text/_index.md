---
category: general
date: 2026-06-25
description: Πώς να χρησιμοποιήσετε OCR στην Python – μάθετε πώς να φορτώνετε εικόνα
  για OCR, να αναγνωρίζετε κείμενο σε περιοχή και να εξάγετε γρήγορα το κείμενο της
  περιοχής.
draft: false
keywords:
- how to use ocr
- load image for ocr
- recognize text in region
- how to extract region text
language: el
og_description: Πώς να χρησιμοποιήσετε OCR στην Python – βήμα‑βήμα οδηγός για τη φόρτωση
  μιας εικόνας, την αναγνώριση κειμένου σε συγκεκριμένη περιοχή και την εξαγωγή του
  αριθμού τιμολογίου.
og_title: 'Πώς να χρησιμοποιήσετε το OCR με Python: Φόρτωση εικόνας και εξαγωγή κειμένου
  περιοχής'
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: How to use OCR in Python – learn how to load image for OCR, recognize
    text in region, and extract region text quickly.
  headline: 'How to Use OCR Python: Load Image and Extract Region Text'
  type: TechArticle
- questions:
  - answer: Most modern OCR engines handle a wide range of fonts, but you can boost
      accuracy by training a custom language model or pre‑processing the image (e.g.,
      applying a threshold filter).
    question: What if the invoice number is printed in a fancy font?
  - answer: Absolutely. Define a list of `Rectangle` objects—one per field—and loop
      over them, storing each result in a dictionary.
    question: Can I extract multiple fields at once?
  - answer: 'Convert each page to an image first (using `pdf2image` or similar), then
      apply the same region‑based extraction per page. --- ## Wrapping Up In this
      tutorial we covered **how to use OCR** in Python to load an image, recognize
      text in a specific region, and extract that region’s text—perfect for pull'
    question: Does this work on multi‑page PDFs?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: 'Πώς να χρησιμοποιήσετε το OCR Python: Φόρτωση εικόνας και εξαγωγή κειμένου
  περιοχής'
url: /el/python-java/general/how-to-use-ocr-python-load-image-and-extract-region-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε OCR Python: Φόρτωση Εικόνας και Εξαγωγή Κειμένου Περιοχής

**How to use OCR in Python** είναι πιο απλό απ' ό,τι νομίζετε. Έχετε ποτέ κολλήσει σε μια σαρωμένη απόδειξη και αναρωτηθείτε πώς να εξάγετε μόνο τον αριθμό της απόδειξης χωρίς να αναλύσετε ολόκληρη τη σελίδα; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν αρχίζουν να πειραματίζονται με την οπτική αναγνώριση χαρακτήρων. Σε αυτόν τον οδηγό θα περάσουμε από τη φόρτωση μιας εικόνας για OCR, τον ορισμό ενός ορθογωνίου, την αναγνώριση κειμένου σε εκείνη την περιοχή και, τέλος, την εξαγωγή του κειμένου της περιοχής. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση script που απομονώνει οποιοδήποτε κομμάτι κειμένου χρειάζεστε.

> *Pro tip:* Αν εργάζεστε με PDFs, μετατρέψτε πρώτα κάθε σελίδα σε εικόνα—οι περισσότερες βιβλιοθήκες OCR χειρίζονται καλύτερα PNG/JPEG.

## Τι Θα Χρειαστείτε

- Python 3.8+ (συνιστάται η τελευταία σταθερή έκδοση)  
- Μια βιβλιοθήκη OCR που εκθέτει μια κλάση `OcrEngine` (π.χ., **ocr** από `pip install ocr-lib`)  
- Ένα δείγμα εικόνας—εδώ θα χρησιμοποιήσουμε το `invoice.png` τοποθετημένο σε φάκελο που ελέγχετε  
- Βασική εξοικείωση με ορθογώνια (x, y, πλάτος, ύψος)  

Χωρίς βαριές εξαρτήσεις, χωρίς ανάγκη GPU—μόνο απλή εργασία CPU, που διατηρεί την φορητότητα.

---

## Πώς να Χρησιμοποιήσετε OCR: Αρχικοποίηση της Μηχανής (Βήμα 1)

Πριν μπορέσει να διαβαστεί οποιοδήποτε κείμενο, χρειάζεστε μια παρουσία της μηχανής OCR. Σκεφτείτε το ως τον εγκέφαλο που θα αναλύει τα μοτίβα των pixel.

```python
import ocr               # The OCR library
from ocr import Rectangle  # Helper for defining regions

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Γιατί είναι σημαντικό:* Η αρχικοποίηση της μηχανής φορτώνει μοντέλα γλώσσας και ορίζει προεπιλεγμένες ρυθμίσεις. Η παράλειψη αυτού του βήματος θα προκαλέσει εξαίρεση τη στιγμή που θα καλέσετε `recognize_region`.

## Φόρτωση Εικόνας για OCR (Βήμα 2)

Τώρα που η μηχανή είναι έτοιμη, της παρέχουμε μια εικόνα. Η μέθοδος `Image.load` της βιβλιοθήκης διαχειρίζεται κοινές μορφές και κανονικοποιεί το bitmap.

```python
# Step 2: Load the image containing the invoice
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

Αν το αρχείο δεν βρεθεί, η Python θα ρίξει ένα `FileNotFoundError`. Βεβαιωθείτε ότι η διαδρομή είναι απόλυτη ή σχετική με τον τρέχοντα φάκελο του script σας.  

*Περίπτωση άκρης:* Κάποιες μηχανές OCR αναμένουν εικόνα σε κλίμακα του γκρι. Αν παρατηρήσετε χαμηλή ακρίβεια, μετατρέψτε πρώτα την εικόνα:

```python
image = image.convert("L")  # L = 8‑bit pixels, black and white
```

## Αναγνώριση Κειμένου στην Περιοχή (Βήμα 3)

Ο ορισμός της περιοχής είναι το σημείο όπου λέτε στη μηχανή *πού* να κοιτάξει. Η `Rectangle` δέχεται τιμές κινητής υποδιαστολής για υπο‑pixel ακρίβεια, κάτι που μπορεί να φανεί χρήσιμο όταν δουλεύετε με σαρώσεις υψηλής ανάλυσης.

```python
# Step 3: Define the rectangle that encloses the invoice number
invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
```

- **x, y** – επάνω‑αριστερή γωνία του ορθογωνίου (σε pixel)  
- **width, height** – μέγεθος του κουτιού  

Μπορεί να αναρωτιέστε πώς να βρείτε αυτούς τους αριθμούς. Ένας γρήγορος τρόπος είναι να ανοίξετε την εικόνα σε οποιονδήποτε επεξεργαστή (π.χ., GIMP ή Paint.NET) και να χρησιμοποιήσετε το εργαλείο επιλογής για να διαβάσετε τις συντεταγμένες.  

*Γιατί να μην κάνετε OCR όλης της σελίδας;* Ο περιορισμός της περιοχής μειώνει τον θόρυβο, επιταχύνει την επεξεργασία και βελτιώνει δραματικά την ακρίβεια για μικρά πεδία όπως οι αριθμοί τιμολογίων.

## Πώς να Εξάγετε Κείμενο Περιοχής (Βήμα 4)

Με την περιοχή ορισμένη, ζητήστε από τη μηχανή να αναγνωρίσει μόνο αυτό το τμήμα. Το αντικείμενο αποτελέσματος περιέχει το ακατέργαστο κείμενο και τις βαθμολογίες εμπιστοσύνης.

```python
# Step 4: Recognize text only within the specified region
region_result = engine.recognize_region(image, invoice_rect)
```

Αν η μηχανή OCR υποστηρίζει πολλαπλές γλώσσες, μπορείτε να περάσετε έναν προαιρετικό κωδικό γλώσσας:

```python
region_result = engine.recognize_region(image, invoice_rect, lang="eng")
```

*Κοινό λάθος:* Κάποιες μηχανές επιστρέφουν λίστα λέξεων αντί για μία συμβολοσειρά. Σε τέτοιες περιπτώσεις, συνενώστε τις:

```python
text = " ".join(region_result.words)
```

## Εξαγωγή του Εξαγόμενου Αριθμού Τιμολογίου (Βήμα 5)

Τέλος, εκτυπώστε—ή αποθηκεύστε—το εξαγόμενο κείμενο. Μπορείτε επίσης να επεξεργαστείτε τη συμβολοσειρά για να αφαιρέσετε περιττά κενά ή μη‑αριθμητικούς χαρακτήρες.

```python
# Step 5: Output the extracted invoice number
raw_text = region_result.text.strip()
# Optional: keep only digits (most invoice numbers are numeric)
invoice_number = "".join(filter(str.isdigit, raw_text))

print("Invoice number:", invoice_number)
```

Η εκτέλεση του script με σωστά ευθυγραμμισμένο ορθογώνιο θα πρέπει να δώσει κάτι όπως:

```
Invoice number: 20231578
```

Αν εμφανιστούν άχρηστοι χαρακτήρες, ελέγξτε ξανά τις συντεταγμένες του ορθογωνίου ή σκεφτείτε να αυξήσετε την ανάλυση της εικόνας.

## Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι ένα αυτόνομο script που μπορείτε να αντιγράψετε‑και‑επικολλήσετε και να τρέξετε:

```python
import ocr
from ocr import Rectangle

def extract_invoice_number(image_path: str,
                          rect: Rectangle,
                          lang: str = "eng") -> str:
    """
    Loads an image, runs OCR on the specified rectangle, and returns
    a cleaned invoice number string.
    """
    engine = ocr.OcrEngine()
    image = ocr.Image.load(image_path)

    # Optional: force grayscale for better accuracy
    image = image.convert("L")

    result = engine.recognize_region(image, rect, lang=lang)
    raw = result.text.strip()
    cleaned = "".join(filter(str.isdigit, raw))
    return cleaned

if __name__ == "__main__":
    # Adjust these values to match your invoice layout
    invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
    invoice_path = "YOUR_DIRECTORY/invoice.png"

    number = extract_invoice_number(invoice_path, invoice_rect)
    print("Invoice number:", number)
```

Αποθηκεύστε το αρχείο ως `extract_invoice.py`, αντικαταστήστε το `YOUR_DIRECTORY` με τον πραγματικό φάκελο, και τρέξτε:

```bash
python extract_invoice.py
```

Θα πρέπει να δείτε τον αριθμό του τιμολογίου να εκτυπώνεται στην κονσόλα.

## Συχνές Ερωτήσεις

**Q: Τι γίνεται αν ο αριθμός του τιμολογίου είναι τυπωμένος με περίπλοκη γραμματοσειρά;**  
A: Οι περισσότερες σύγχρονες μηχανές OCR διαχειρίζονται ευρύ φάσμα γραμματοσειρών, αλλά μπορείτε να βελτιώσετε την ακρίβεια εκπαιδεύοντας ένα προσαρμοσμένο μοντέλο γλώσσας ή προεπεξεργάζοντας την εικόνα (π.χ., εφαρμόζοντας φίλτρο κατωφλίου).

**Q: Μπορώ να εξάγω πολλαπλά πεδία ταυτόχρονα;**  
A: Απόλυτα. Ορίστε μια λίστα από αντικείμενα `Rectangle`—ένα ανά πεδίο—και κάντε βρόχο πάνω τους, αποθηκεύοντας κάθε αποτέλεσμα σε ένα λεξικό.

**Q: Λειτουργεί αυτό σε PDF πολλαπλών σελίδων;**  
A: Μετατρέψτε πρώτα κάθε σελίδα σε εικόνα (χρησιμοποιώντας `pdf2image` ή παρόμοιο), και στη συνέχεια εφαρμόστε την ίδια εξαγωγή βάσει περιοχής ανά σελίδα.

## Συμπεράσματα

Σε αυτόν τον οδηγό καλύψαμε **πώς να χρησιμοποιήσετε OCR** σε Python για να φορτώσετε μια εικόνα, να αναγνωρίσετε κείμενο σε συγκεκριμένη περιοχή και να εξάγετε το κείμενο αυτής της περιοχής—ιδανικό για την εξαγωγή αριθμών τιμολογίων, IDs παραγγελιών ή οποιουδήποτε μικρού τμήματος δεδομένων από σαρωμένα έγγραφα. Με την απομόνωση της περιοχής ενδιαφέροντος κερδίζετε ταχύτητα, ακρίβεια και λιγότερο κόπο στην επεξεργασία.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να επεκτείνετε το script ώστε να διαχειρίζεται **load image for OCR** από φάκελο με δέσμες τιμολογίων, ή πειραματιστείτε με **recognize text in region** για διαφορετικά πεδία όπως ημερομηνίες και σύνολα. Το ίδιο μοτίβο ισχύει—απλώς αλλάξτε τις συντεταγμένες του ορθογωνίου.

Αν αντιμετωπίσατε προβλήματα ή έχετε ιδέες για βελτίωση, αφήστε ένα σχόλιο παρακάτω. Καλό κώδικα, και εύχομαι οι OCR αγωγοί σας να είναι πάντα ακριβείς!

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε σε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Βήμα‑βήμα](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Πώς να Εξάγετε Κείμενο από Εικόνα Προετοιμάζοντας Ορθογώνια σε OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Πώς να Χρησιμοποιήσετε AspOCR: Προεπεξεργασία Φίλτρων OCR Εικόνας για .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}