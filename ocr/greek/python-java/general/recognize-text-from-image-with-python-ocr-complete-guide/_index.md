---
category: general
date: 2026-06-16
description: Αναγνωρίστε κείμενο από εικόνα χρησιμοποιώντας μια μηχανή OCR σε Python
  – μάθετε πώς να εξάγετε κείμενο από απόδειξη και να βελτιώσετε την ακρίβεια του
  OCR σε λίγα λεπτά.
draft: false
keywords:
- recognize text from image
- extract text from receipt
- improve ocr accuracy
- python ocr tutorial
- image preprocessing for OCR
language: el
og_description: Αναγνωρίστε γρήγορα κείμενο από εικόνα. Αυτός ο οδηγός δείχνει πώς
  να εξάγετε κείμενο από απόδειξη και να βελτιώσετε την ακρίβεια OCR χρησιμοποιώντας
  Python.
og_title: Αναγνώριση κειμένου από εικόνα με Python OCR – Πλήρης Οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: recognize text from image using a Python OCR engine – learn how to
    extract text from receipt and improve OCR accuracy in minutes.
  headline: recognize text from image with Python OCR – Complete Guide
  type: TechArticle
- description: recognize text from image using a Python OCR engine – learn how to
    extract text from receipt and improve OCR accuracy in minutes.
  name: recognize text from image with Python OCR – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - Basic familiarity with pip and
      virtual environments. - A sample receipt image (JPEG or PNG) that you want to
      process. - The `ocr` package (the example uses a fictional `ocr` module for
      illustration; replace it with `pytesseract`, `easyocr`, or any library t'
  - name: Expected Output
    text: 'Running the script on a typical grocery receipt yields something like:'
  - name: H3 – Crop to the Receipt Region
    text: 'If your image contains a lot of background (e.g., a photo of a desk), crop
      it first:'
  - name: H3 – Use a Custom Language Pack
    text: 'For receipts that contain foreign characters (e.g., “€” or “¥”), load the
      appropriate language data:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Αναγνώριση κειμένου από εικόνα με Python OCR – Πλήρης Οδηγός
url: /el/python-java/general/recognize-text-from-image-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση Κειμένου από Εικόνα με Python OCR – Πλήρης Οδηγός

Έχετε ποτέ χρειαστεί να **αναγνωρίσετε κείμενο από εικόνα** αλλά τα αποτελέσματα έδειχναν ακατανόητο κείμενο; Δεν είστε ο μόνος. Σε πολλές μικρές επιχειρηματικές περιπτώσεις—σκεφτείτε τη σάρωση αποδείξεων, την ψηφιοποίηση τιμολογίων ή την εξαγωγή δεδομένων από ταυτότητες—η λήψη καθαρού, αξιόπιστου αποτελέσματος είναι η διαφορά μεταξύ μιας ομαλής ροής εργασίας και ενός κεφαλαίου.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από έναν πρακτικό τρόπο για **αναγνωρίσετε κείμενο από εικόνα** χρησιμοποιώντας μια ελαφριά βιβλιοθήκη Python OCR. Θα σας δείξουμε επίσης ακριβώς πώς να **εξάγετε κείμενο από απόδειξη** και θα μοιραστούμε κόλπα για **να βελτιώσετε την ακρίβεια του OCR** χωρίς να αγοράσετε ακριβές λογισμικό. Έτοιμοι; Ας βουτήξουμε.

## Τι Θα Δημιουργήσετε

Στο τέλος αυτού του οδηγού θα έχετε ένα έτοιμο‑για‑εκτέλεση script που:

1. Δημιουργεί μια μηχανή OCR.  
2. Ενεργοποιεί έξυπνη προεπεξεργασία (ευθυγράμμιση, απομάκρυνση θορύβου, δυαδικοποίηση).  
3. Φορτώνει μια θορυβώδη εικόνα απόδειξης.  
4. Εκτελεί αυτόματα τη διαδικασία αναγνώρισης.  
5. Εκτυπώνει καθαρό, αναζητήσιμο κείμενο στην κονσόλα.

Χωρίς εξωτερικές υπηρεσίες, χωρίς κρυφά API keys—απλώς καθαρός κώδικας Python που μπορείτε να προσαρμόσετε σε οποιοδήποτε έργο.

### Προαπαιτούμενα

- Python 3.8+ εγκατεστημένο στο μηχάνημά σας.  
- Βασική εξοικείωση με pip και εικονικά περιβάλλοντα.  
- Μια δείγμα εικόνας απόδειξης (JPEG ή PNG) που θέλετε να επεξεργαστείτε.  
- Το πακέτο `ocr` (το παράδειγμα χρησιμοποιεί ένα φανταστικό module `ocr` για επεξήγηση· αντικαταστήστε το με `pytesseract`, `easyocr`, ή οποιαδήποτε βιβλιοθήκη προσφέρει παρόμοιο API).

> **Pro tip:** Αν αντιμετωπίσετε ελλείψεις εξαρτήσεων, εγκαταστήστε τες με `pip install ocr` (ή το πραγματικό όνομα του πακέτου) πριν προχωρήσετε.

## Βήμα 1 – Αναγνώριση Κειμένου από Εικόνα: Ρύθμιση της Μηχανής

Πρώτα απ’ όλα. Χρειαζόμαστε ένα αντικείμενο που ξέρει πώς να διαβάζει δεδομένα pixel και να τα μετατρέπει σε χαρακτήρες. Σκεφτείτε τη μηχανή ως τον εγκέφαλο της λειτουργίας· όλα τα άλλα της παρέχουν πληροφορίες.

```python
import ocr  # Replace with your actual OCR library import

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

Γιατί να δημιουργήσουμε τη μηχανή χειροκίνητα; Κάποιες βιβλιοθήκες σας επιτρέπουν να καλέσετε μια μοναδική συνάρτηση, αλλά μια ρητή δημιουργία αντικειμένου σας δίνει λεπτομερή έλεγχο της προεπεξεργασίας—ακριβώς αυτό που χρειαζόμαστε για **να βελτιώσουμε την ακρίβεια του OCR** αργότερα.

## Βήμα 2 – Εξαγωγή Κειμένου από Απόδειξη: Ενεργοποίηση Προεπεξεργασίας

Μια απόδειξη που έχει σαρωθεί με τη φωτογραφική μηχανή του τηλεφώνου σπάνια είναι τέλεια. Μπορεί να είναι ελαφρώς κεκλιμένη, να έχει σκόνη ή να υποφέρει από ανισοκατανομή φωτισμού. Η ενεργοποίηση της προεπεξεργασίας κάνει το σκληρό έργο πριν η μηχανή ακόμη και κοιτάξει τα γράμματα.

```python
# Step 2: Enable preprocessing to improve recognition quality
preprocess = engine.preprocessing
preprocess.deskew = True        # Auto‑rotate slightly tilted pages
preprocess.despeckle = True     # Remove isolated noise pixels
preprocess.binarization = True  # Convert image to pure black‑white
```

*Deskew* ευθυγραμμίζει τη σελίδα, *despeckle* αφαιρεί ανεπιθύμητα στίγματα, και *binarization* μετατρέπει κάθε pixel σε μαύρο ή λευκό. Αυτές οι τρεις επιλογές μπορούν **να βελτιώσουν την ακρίβεια του OCR** κατά 20‑30 % σε θορυβώδεις αποδείξεις.

## Βήμα 3 – Φόρτωση της Εικόνας που Θέλετε να Αναγνωρίσετε

Τώρα κατευθύνουμε τη μηχανή στο πραγματικό αρχείο. Η διαδρομή μπορεί να είναι απόλυτη ή σχετική· απλώς βεβαιωθείτε ότι η εικόνα υπάρχει.

```python
# Step 3: Load the scanned receipt image
engine.image = ocr.Image.load_from_file("YOUR_DIRECTORY/receipt-noisy.jpg")
```

Αν αναρωτιέστε αν η μηχανή υποστηρίζει PDFs ή πολυ‑σελίδες TIFF, οι περισσότερες σύγχρονες βιβλιοθήκες το κάνουν—απλώς ελέγξτε την τεκμηρίωση. Για ένα μονοσέλιδο JPEG, η παραπάνω γραμμή είναι ό,τι χρειάζεστε.

## Βήμα 4 – Εκτέλεση OCR – Η Μηχανή Κάνει τα Υπόλοιπα

Με τη προεπεξεργασία ρυθμισμένη και την εικόνα φορτωμένη, η επόμενη κλήση κάνει τα πάντα: προεπεξεργάζεται, τρέχει τον αλγόριθμο αναγνώρισης και επιστρέφει ένα αντικείμενο αποτελέσματος.

```python
# Step 4: Run OCR – the configured preprocessing is applied automatically
ocr_result = engine.recognize()
```

Πίσω από τις σκηνές η μηχανή μπορεί να χρησιμοποιεί Tesseract, ένα νευρωνικό δίκτυο ή μια ιδιόκτητη μηχανή. Δεν χρειάζεται να γνωρίζετε τα εσωτερικά· λαμβάνετε απλώς ένα καθαρό αποτέλεσμα.

## Βήμα 5 – Έξοδος του Αναγνωρισμένου Κειμένου

Τέλος, εξάγουμε το απλό κείμενο από το αποτέλεσμα και το εκτυπώνουμε. Σε μια πραγματική εφαρμογή θα μπορούσατε να το γράψετε σε βάση δεδομένων, αρχείο CSV ή ακόμη και να το τροφοδοτήσετε σε μια downstream pipeline ανάλυσης.

```python
# Step 5: Output the recognized text
print(ocr_result.text)
```

### Αναμενόμενη Έξοδος

Η εκτέλεση του script σε μια τυπική απόδειξη παντοπωλείου δίνει κάτι σαν:

```
WALMART STORE #1234
123 Main St.
Anytown, USA

Date: 06/15/2026   Time: 14:32
Cashier: J. Doe

Item                Qty   Price
---------------------------------
Milk                1     2.99
Bread               2     5.48
Eggs                1     3.20
---------------------------------
Subtotal                    11.67
Tax                         0.93
Total                       12.60
```

Αν η έξοδος φαίνεται ακατάληπτη, ελέγξτε ξανά ότι οι σημαίες προεπεξεργασίας είναι ενεργές και ότι η εικόνα δεν είναι πολύ σκοτεινή. Η ρύθμιση του κατωφλίου δυαδικοποίησης (κάποιες βιβλιοθήκες επιτρέπουν προσαρμοσμένη τιμή) μπορεί **να βελτιώσει την ακρίβεια του OCR** περαιτέρω.

## Προχωρημένο: Λεπτομερής Ρύθμιση για Ταχύτερη Εξαγωγή Κειμένου από Απόδειξη

Αν και η ροή πέντε βημάτων λειτουργεί στις περισσότερες περιπτώσεις, ίσως θέλετε να επιταχύνετε την επεξεργασία εκατοντάδων αποδείξεων κάθε βράδυ. Εδώ είναι μερικές προαιρετικές βελτιώσεις:

### H3 – Κόψιμο στην Περιοχή της Απόδειξης

Αν η εικόνα σας περιέχει πολύ φόντο (π.χ., φωτογραφία ενός γραφείου), κόψτε την πρώτα:

```python
engine.image = engine.image.crop((50, 200, 800, 1200))  # left, top, right, bottom
```

### H3 – Χρήση Προσαρμοσμένου Πακέτου Γλώσσας

Για αποδείξεις που περιέχουν ξένους χαρακτήρες (π.χ., “€” ή “¥”), φορτώστε τα αντίστοιχα δεδομένα γλώσσας:

```python
engine.set_language('eng+deu+fra')  # English, German, French
```

Και τα δύο κόλπα βοηθούν τη μηχανή **να αναγνωρίσει κείμενο από εικόνα** πιο αξιόπιστα, ειδικά όταν το υλικό προέρχεται από διαφορετικές πηγές.

## Συνηθισμένα Πίνακες και Πώς να τους Αποφύγετε

- **Λείπουν Γραμματοσειρές:** Κάποιες μηχανές OCR χρειάζονται τα αρχεία γραμματοσειράς για εξειδικευμένες γραμματοσειρές αποδείξεων. Εγκαταστήστε τα κατάλληλα πακέτα γλώσσας.  
- **Πάρα πολύ Θόρυβος:** Ακόμη και με `despeckle=True`, εξαιρετικά σπογγώδεις σάρωση μπορεί να μπερδέψει τη μηχανή. Ένα γρήγορο χειροκίνητο φίλτρο στο Pillow (`Image.filter(ImageFilter.MedianFilter)`) μπορεί να βοηθήσει.  
- **Λάθος DPI:** Οι μηχανές OCR υποθέτουν περίπου 300 dpi. Αν η εικόνα σας είναι χαμηλότερη, αλλάξτε το μέγεθος πρώτα: `engine.image = engine.image.resize((width*2, height*2))`.

Η αντιμετώπιση αυτών των ζητημάτων **βελτιώνει την ακρίβεια του OCR** χωρίς να χρειάζεται να στραφείτε σε ακριβές τρίτα μέρη.

## Πλήρες Script – Έτοιμο για Εκτέλεση

Παρακάτω είναι το πλήρες, εκτελέσιμο πρόγραμμα Python που ενσωματώνει όλα όσα συζητήσαμε. Αποθηκεύστε το ως `receipt_ocr.py` και εκτελέστε `python receipt_ocr.py`.

```python
import ocr  # Replace with the actual library you use

def main():
    # Initialize the OCR engine
    engine = ocr.OcrEngine()

    # Enable preprocessing steps
    preprocess = engine.preprocessing
    preprocess.deskew = True
    preprocess.despeckle = True
    preprocess.binarization = True

    # Load the receipt image (change the path to your file)
    engine.image = ocr.Image.load_from_file("YOUR_DIRECTORY/receipt-noisy.jpg")

    # Optional: crop out unnecessary background
    # engine.image = engine.image.crop((50, 200, 800, 1200))

    # Run the recognition pipeline
    result = engine.recognize()

    # Print the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

Η εκτέλεση αυτού του script **αναγνωρίζει κείμενο από εικόνα** και εκτυπώνει ένα ωραία μορφοποιημένο μπλοκ δεδομένων απόδειξης. Μη διστάσετε να προσαρμόσετε τις συντεταγμένες κοπής, τις ρυθμίσεις γλώσσας ή τις σημαίες προεπεξεργασίας ώστε να ταιριάζουν στα δικά σας σχέδια αποδείξεων.

## Συμπέρασμα

Καλύψαμε έναν απλό τρόπο για **να αναγνωρίσετε κείμενο από εικόνα** χρησιμοποιώντας Python, δείξαμε πώς να **εξάγετε κείμενο από απόδειξη** και εξετάσαμε αρκετές πρακτικές συμβουλές για **να βελτιώσετε την ακρίβεια του OCR**. Η βασική ιδέα είναι απλή: ρυθμίστε μια μηχανή OCR, ενεργοποιήστε έξυπνη προεπεξεργασία, δώστε της μια καθαρή εικόνα και αφήστε τη βιβλιοθήκη να κάνει το σκληρό έργο.

Τι θα κάνετε στη συνέχεια; Δοκιμάστε να τροφοδοτήσετε μια δέσμη αποδείξεων μέσω βρόχου, αποθηκεύστε κάθε αποτέλεσμα σε CSV ή συνδέστε την έξοδο με ένα σύστημα λογιστικής. Μπορείτε επίσης να πειραματιστείτε με βιβλιοθήκες OCR βάσει deep‑learning όπως `easyocr` για ακόμη μεγαλύτερη ακρίβεια σε σύνθετες γραμματοσειρές.

Έχετε ερωτήσεις για κάποιο συγκεκριμένο φορμά απόδειξης ή θέλετε να δείτε πώς να διαχειριστείτε πολυ‑σελίδες PDF; Αφήστε ένα σχόλιο παρακάτω, και καλή κωδικοποίηση!

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική;

Οι παρακάτω οδηγίες καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες λειτουργίες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Βήμα‑Βήμα](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Πώς να Εξάγετε Κείμενο από Εικόνα Προετοιμάζοντας Ορθογώνια στο OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Εξαγωγή Κειμένου από Εικόνα – Βελτιστοποίηση OCR με Aspose.OCR για .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}