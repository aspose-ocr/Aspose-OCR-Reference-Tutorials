---
category: general
date: 2026-06-22
description: Κάντε OCR σε εικόνα χρησιμοποιώντας Python σε λίγες μόνο γραμμές. Μάθετε
  πώς να φορτώνετε εικόνα για OCR, να αναγνωρίζετε κείμενο από PNG και να χρησιμοποιείτε
  τον κινητήρα OCR αποδοτικά.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- load image for OCR
- use OCR engine
language: el
og_description: Εκτελέστε OCR σε εικόνα γρήγορα με την Python. Αυτό το σεμινάριο δείχνει
  πώς να φορτώσετε εικόνα για OCR, να αναγνωρίσετε κείμενο από PNG και να χρησιμοποιήσετε
  τη μηχανή OCR με εμπιστοσύνη.
og_title: Εκτελέστε OCR σε εικόνα με Python – Οδηγός βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Perform OCR on image using Python in just a few lines. Learn how to
    load image for OCR, recognize text from PNG, and use OCR engine efficiently.
  headline: Perform OCR on Image in Python – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Εκτέλεση OCR σε εικόνα με Python – Πλήρης οδηγός
url: /el/python-java/general/perform-ocr-on-image-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε Εικόνα με Python – Πλήρης Οδηγός

Έχετε ποτέ χρειαστεί να **εκτελέσετε OCR σε εικόνα** αρχεία αλλά να νιώσατε κολλημένοι στην πρώτη γραμμή κώδικα; Δεν είστε μόνοι. Σε αυτόν τον οδηγό θα σας δείξουμε ακριβώς πώς να **φορτώσετε εικόνα για OCR**, να ρυθμίσετε μια ελαφριά **μηχανή OCR**, και τελικά να **αναγνωρίσετε κείμενο από PNG** με λίγες μόνο εντολές.

Θα καλύψουμε τα πάντα, από την εγκατάσταση της βιβλιοθήκης μέχρι τη ρύθμιση της λίστας επιτρεπόμενων χαρακτήρων ώστε μόνο τα ψηφία και τα κεφαλαία γράμματα να παραμένουν στην ανίχνευση. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση script που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο—χωρίς μυστήριο, χωρίς περιττά στοιχεία.

## Τι Θα Μάθετε

- Πώς να **χρησιμοποιήσετε τη μηχανή OCR** προγραμματιστικά σε Python.  
- Τα ακριβή βήματα για **φόρτωση εικόνας για OCR** από τοπικό φάκελο.  
- Γιατί και πώς να περιορίσετε την αναγνώριση σε προσαρμοσμένο σύνολο χαρακτήρων.  
- Πώς να **αναγνωρίσετε κείμενο από PNG** και να διαχειριστείτε το αποτέλεσμα με ασφάλεια.  

**Προαπαιτούμενα:** Εγκατεστημένο Python 3.7+, ένα τερματικό με το οποίο αισθάνεστε άνετα, και μια εικόνα (π.χ. `serial-number.png`) που θέλετε να διαβάσετε. Δεν απαιτείται προηγούμενη εμπειρία με OCR.

---

## Εκτέλεση OCR σε Εικόνα – Αρχικοποίηση της Μηχανής OCR

Το πρώτο πράγμα που πρέπει να κάνετε είναι να δημιουργήσετε μια παρουσία της μηχανής OCR. Σκεφτείτε τη μηχανή ως τον εγκέφαλο που θα αναλύει τα pixel και θα τα μετατρέπει σε χαρακτήρες.

```python
import ocr  # Assuming the OCR library is named `ocr`

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Γιατί είναι σημαντικό:* Χωρίς μηχανή δεν υπάρχει τίποτα για να επεξεργαστεί την εικόνα. Η κλάση `OcrEngine` συγκεντρώνει όλη τη βαριά δουλειά—προεπεξεργασία, τμηματοποίηση και ταξινόμηση χαρακτήρων—σε ένα ενιαίο αντικείμενο που μπορείτε να επαναχρησιμοποιήσετε.

---

## Φόρτωση Εικόνας για OCR – Παροχή του Αρχείου PNG

Τώρα που η μηχανή υπάρχει, πρέπει να της δώσετε την εικόνα που θέλετε να διαβάσετε. Η βιβλιοθήκη αναμένει ένα αντικείμενο `ImageStream`, το οποίο μπορείτε να δημιουργήσετε απευθείας από μια διαδρομή αρχείου.

```python
# Step 2: Load the image to be processed
image_path = "YOUR_DIRECTORY/serial-number.png"
engine.set_image(ocr.ImageStream.from_file(image_path))
```

*Συμβουλή:* Διατηρήστε την εικόνα σε μορφή υψηλής αντίθεσης (μαύρο κείμενο σε λευκό φόντο) και αποφύγετε τα συμπιεστικά τεχνουργήματα· μπορούν να μπλοκάρουν τον αλγόριθμο OCR.

---

## Περιορισμός Χαρακτήρων – Λίστα Επιτρεπόμενων Ψηφίων και Κεφαλαίων Γραμμάτων

Συχνά σας ενδιαφέρει μόνο ένα υποσύνολο χαρακτήρων—π.χ. ένας σειριακός αριθμός που περιέχει μόνο A‑Z και 0‑9. Ορίζοντας μια whitelist, λέτε στη μηχανή να αγνοεί όλα τα άλλα, κάτι που βελτιώνει δραστικά την ακρίβεια.

```python
# Step 3: Restrict recognition to digits and uppercase letters
whitelist = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"
engine.get_settings().set_whitelist(whitelist)
```

*Τι συμβαίνει στο παρασκήνιο;* Η μηχανή δημιουργεί ένα φίλτρο που απορρίπτει οποιοδήποτε γλύφο δεν υπάρχει στη whitelist πριν από το τελικό στάδιο ταξινόμησης. Αυτό είναι ιδιαίτερα χρήσιμο όταν η εικόνα περιέχει θόρυβο ή διακοσμητικό κείμενο που δεν χρειάζεστε.

---

## Αναγνώριση Κειμένου από PNG – Εκτέλεση της Διαδικασίας OCR

Με τη μηχανή προετοιμασμένη και την εικόνα φορτωμένη, μπορείτε τελικά να **εκτελέσετε OCR σε εικόνα**. Η κλήση `recognize()` εκτελεί ολόκληρη τη διαδικασία και επιστρέφει ένα αντικείμενο αποτελέσματος.

```python
# Step 4: Perform OCR on the image
result = engine.recognize()
```

Αν σας ενδιαφέρει η απόδοση, η μέθοδος ολοκληρώνεται συνήθως μέσα σε μερικές εκατοντάδες χιλιοστά του δευτερολέπτου για ένα PNG 300 × 200 px σε ένα σύγχρονο laptop.

---

## Έξοδος και Επαλήθευση – Λήψη του Αναγνωρισμένου Κειμένου

Το τελευταίο βήμα είναι η εξαγωγή του απλού κειμένου από το αντικείμενο αποτελέσματος. Οτιδήποτε δεν ταιριάζει με τη whitelist απορρίπτεται αυτόματα, έτσι λαμβάνετε μια καθαρή συμβολοσειρά έτοιμη για περαιτέρω επεξεργασία.

```python
# Step 5: Output the recognized text (characters outside the whitelist are ignored)
recognized_text = result.get_text()
print(recognized_text)
```

*Τυπική έξοδος:* `AB12C3D4E5` (υποθέτοντας ότι η εικόνα περιείχε ακριβώς αυτόν τον σειριακό αριθμό).  

Αν η έξοδος είναι κενή ή παραμορφωμένη, ελέγξτε ξανά την ποιότητα της εικόνας και τη whitelist· ένα συνηθισμένο λάθος είναι η τυχαία παράλειψη απαιτούμενων χαρακτήρων.

---

## Ακραίες Περιπτώσεις & Συνηθισμένα Προβλήματα

| Κατάσταση | Τι να Ελέγξετε | Προτεινόμενη Διόρθωση |
|-----------|----------------|----------------------|
| **File not found** | Λάθος διαδρομή ή λείπει το αρχείο | Χρησιμοποιήστε `os.path.abspath` για να επαληθεύσετε την πλήρη διαδρομή πριν καλέσετε `set_image`. |
| **Low contrast image** | Το κείμενο αναμειγνύεται με το φόντο | Εφαρμόστε ένα απλό κατώφλι (`Pillow` ή `OpenCV`) πριν δώσετε την εικόνα στη μηχανή. |
| **Unexpected characters** | Η whitelist είναι πολύ περιοριστική | Προσθέστε τους ελλιπείς χαρακτήρες στη συμβολοσειρά της whitelist. |
| **Large images** | Αργή αναγνώριση | Αλλάξτε το μέγεθος της εικόνας σε μέγιστο πλάτος 1024 px· η ποιότητα OCR συνήθως παραμένει υψηλή. |

---

## Πλήρες Script – Έτοιμο για Εκτέλεση

Παρακάτω είναι το πλήρες, αυτόνομο script που ενώνει όλα τα κομμάτια. Αποθηκεύστε το ως `ocr_demo.py`, αντικαταστήστε το `YOUR_DIRECTORY` με τον πραγματικό φάκελο, και τρέξτε `python ocr_demo.py`.

```python
import ocr
import os

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a PNG image and return the recognized text.
    Only uppercase letters and digits are allowed.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()

    # Load the PNG image
    engine.set_image(ocr.ImageStream.from_file(image_path))

    # Whitelist: A-Z and 0-9
    engine.get_settings().set_whitelist("ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789")

    # Run recognition
    result = engine.recognize()

    # Return clean text
    return result.get_text()

if __name__ == "__main__":
    # Adjust the path to point to your PNG file
    png_path = "YOUR_DIRECTORY/serial-number.png"
    try:
        text = perform_ocr(png_path)
        print("Recognized text:", text)
    except Exception as e:
        print("Error during OCR:", e)
```

*Αναμενόμενη έξοδος κονσόλας* (όταν το PNG περιέχει `SN12345`):

```
Recognized text: SN12345
```

---

## Συμπέρασμα

Τώρα γνωρίζετε ακριβώς πώς να **εκτελέσετε OCR σε εικόνα** αρχεία σε Python, από το **φόρτωμα εικόνας για OCR** μέχρι την **αναγνώριση κειμένου από PNG** και τελικά την εξαγωγή ενός καθαρού αποτελέσματος χρησιμοποιώντας μια προσαρμόσιμη **μηχανή OCR**. Η προσέγγιση είναι απλή, επεκτάσιμη και λειτουργεί έτοιμη για χρήση σε περισσότερες σαρώσεις τύπου σειριακού αριθμού.

Τι θα κάνετε στη συνέχεια; Δοκιμάστε να αλλάξετε τη whitelist σε πεζά γράμματα, πειραματιστείτε με διαφορετικές μορφές εικόνας (JPEG, BMP), ή ενσωματώστε το script σε μια γραμμή επεξεργασίας δέσμης. Το ίδιο μοτίβο—μηχανή → εικόνα → ρυθμίσεις → αναγνώριση → έξοδος—ισχύει για σχεδόν κάθε εργασία OCR που θα συναντήσετε.

Έχετε ερωτήσεις ή μια ιδιόρρυθμη εικόνα που αρνείται να συνεργαστεί; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

![Διάγραμμα που απεικονίζει τα βήματα για την εκτέλεση OCR σε εικόνα χρησιμοποιώντας Python](https://example.com/ocr-flow.png "Διάγραμμα που δείχνει πώς να εκτελέσετε OCR σε εικόνα με μια μηχανή OCR Python")

## Τι Θα Μάθετε Στη Σύντομη Επόμενη

Τα παρακάτω tutorials καλύπτουν στενά σχετικά θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Μετατροπή Εικόνας σε Κείμενο – Εκτέλεση OCR σε Εικόνα από URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Πώς να Χρησιμοποιήσετε το AspOCR: Φίλτρα Προεπεξεργασίας Εικόνας OCR για .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Πώς να Εξάγετε Κείμενο από Εικόνα Προετοιμάζοντας Ορθογώνια στο OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}