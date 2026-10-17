---
category: general
date: 2026-07-05
description: Πώς να χρησιμοποιήσετε OCR στην Python για γρήγορη μετατροπή TIFF σε
  κείμενο. Μάθετε τα βήματα της βιβλιοθήκης OCR στην Python για την εξαγωγή κειμένου
  από εικόνες TIFF και τη δημιουργία μιας μηχανής OCR στην Python.
draft: false
keywords:
- how to use ocr
- ocr library python
- convert tiff to text
- extract text from tiff
- python ocr engine
language: el
og_description: Πώς να χρησιμοποιήσετε OCR στην Python; Αυτός ο οδηγός σας δείχνει
  βήμα‑βήμα πώς να μετατρέψετε TIFF σε κείμενο χρησιμοποιώντας μια μηχανή OCR σε Python
  και τη βιβλιοθήκη ocr python.
og_title: Πώς να χρησιμοποιήσετε OCR στην Python – Πλήρης εξαγωγή κειμένου από TIFF
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  headline: How to Use OCR in Python – Extract Text from TIFF
  type: TechArticle
- description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  name: How to Use OCR in Python – Extract Text from TIFF
  steps:
  - name: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
    text: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
  - name: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
    text: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
  - name: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
    text: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Image Processing
title: Πώς να χρησιμοποιήσετε OCR στην Python – Εξαγωγή κειμένου από TIFF
url: /el/python-java/general/how-to-use-ocr-in-python-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε OCR σε Python – Εξαγωγή Κειμένου από TIFF

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε OCR σε Python** για να μετατρέψετε ένα σαρωμένο βιβλίο σε επεξεργάσιμο κείμενο; Δεν είστε οι μόνοι—προγραμματιστές, ερευνητές και ερασιτέχνες αντιμετωπίζουν αυτό το εμπόδιο όταν δουλεύουν με εικόνες TIFF πολλαπλών σελίδων. Τα καλά νέα; Με το **ocr library python** μπορείτε να δημιουργήσετε μια μικρή μηχανή OCR, να την κατευθύνετε σε ένα αρχείο TIFF και να λάβετε καθαρό, αναζητήσιμο κείμενο σε δευτερόλεπτα.

Σε αυτό το tutorial θα περάσουμε από όλα όσα χρειάζεστε: την εγκατάσταση του σωστού πακέτου, τη φόρτωση ενός TIFF πολλαπλών σελίδων, την εκτέλεση της μηχανής OCR και, τέλος, την εκτύπωση του περιεχομένου κάθε σελίδας. Στο τέλος θα μπορείτε να **μετατρέψετε TIFF σε κείμενο** και να **εξάγετε κείμενο από TIFF** αρχεία χωρίς να φύγετε από το περιβάλλον Python.

## Προαπαιτήσεις

- Python 3.9 ή νεότερο (το παράδειγμα δοκιμάστηκε σε 3.11)
- Μια πρόσφατη έκδοση της βιβλιοθήκης `ocr` (ή οποιουδήποτε συμβατού `python ocr engine` προτιμάτε)
- Ένα αρχείο TIFF πολλαπλών σελίδων που θέλετε να επεξεργαστείτε (θα το ονομάσουμε `scanned_book.tif`)
- Βασική εξοικείωση με σενάρια Python και εικονικά περιβάλλοντα

Δεν απαιτούνται βαριά εξωτερικά εργαλεία—μόνο pip και μερικές γραμμές κώδικα.

## Εγκατάσταση της Βιβλιοθήκης OCR για Python

Πρώτα απ' όλα: χρειάζεστε ένα αξιόπιστο OCR backend. Για αυτόν τον οδηγό θα χρησιμοποιήσουμε το φανταστικό πακέτο `ocr` που παρέχει ένα απλό API υψηλού επιπέδου, αλλά το ίδιο μοτίβο λειτουργεί με wrappers βασισμένα στο Tesseract όπως το `pytesseract` ή εμπορικά SDKs.

```bash
# Create a clean virtual environment (optional but recommended)
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate

# Install the OCR package
pip install ocr
```

> **Συμβουλή επαγγελματία:** Αν χρησιμοποιείτε Windows και το πακέτο εξαρτάται από εγγενή binaries, βεβαιωθείτε ότι έχετε εγκατεστημένο το κατάλληλο Visual C++ redistributable. Ο εγκαταστάτης συνήθως θα σας προειδοποιήσει αν κάτι λείπει.

## Πώς να Χρησιμοποιήσετε τη Μηχανή OCR σε Python

Τώρα που η βιβλιοθήκη είναι έτοιμη, ας δημιουργήσουμε μια μηχανή OCR και να την κατευθύνουμε στο αρχείο TIFF. Το παρακάτω απόσπασμα κώδικα δημιουργεί μια παρουσία μηχανής, ορίζει τη γλώσσα στα Αγγλικά και την προετοιμάζει για επεξεργασία πολλαπλών σελίδων.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH   # You can switch to ocr.Language.FRENCH, etc.
```

**Γιατί να ορίσετε τη γλώσσα;**  
Οι περισσότερες μηχανές OCR χρησιμοποιούν μοντέλα γλώσσας για να βελτιώσουν την ακρίβεια. Αν παραλείψετε αυτό το βήμα, η μηχανή θα επιστρέψει σε ένα γενικό μοντέλο που μπορεί να αναγνωρίσει λανθασμένα σημεία στίξης ή ειδικούς χαρακτήρες.

## Φόρτωση της Εικόνας TIFF Πολλαπλών Σελίδων

Το επόμενο βήμα είναι η φόρτωση του σαρωμένου εγγράφου. Η βοηθητική συνάρτηση `ocr.Image.load` κατανοεί τις στοίβες TIFF αμέσως, επιστρέφοντας ένα αντικείμενο που αντιπροσωπεύει εσωτερικά κάθε σελίδα.

```python
# Step 2: Load the multi‑page TIFF image containing the scanned book
tiff_path = "YOUR_DIRECTORY/scanned_book.tif"
tiff_image = ocr.Image.load(tiff_path)
```

> **Ακραία περίπτωση:** Αν το TIFF σας χρησιμοποιεί συμπίεση (CCITT Group 4, LZW, κλπ.) και η βιβλιοθήκη ρίξει σφάλμα, δοκιμάστε να το μετατρέψετε σε μια ασυμπίεστη έκδοση με το ImageMagick πρώτα:
> ```bash
> convert scanned_book.tif -compress none scanned_book_uncompressed.tif
> ```

## Εκτέλεση OCR σε Όλες τις Σελίδες – Μετατροπή TIFF σε Κείμενο

Με το αντικείμενο εικόνας στα χέρια, η μηχανή μπορεί τώρα να επεξεργαστεί όλες τις σελίδες ταυτόχρονα. Αυτή η μέθοδος επιστρέφει μια λίστα όπου κάθε στοιχείο περιέχει το αποτέλεσμα OCR για μία σελίδα.

```python
# Step 3: Perform OCR on all pages of the image
page_results = engine.recognize_multi_page(tiff_image)
```

**Τι συμβαίνει στο παρασκήνιο;**  
Η συνάρτηση `recognize_multi_page` επαναλαμβάνει κάθε rasterized σελίδα, εκτελεί τον αναγνωριστή νευρωνικού δικτύου και συσκευάζει το κείμενο εξόδου μαζί με τις βαθμολογίες εμπιστοσύνης. Είναι ουσιαστικά μια λειτουργία batch που σας εξοικονομεί το γράψιμο ενός χειροκίνητου βρόχου.

## Επανάληψη Μέσω των Αποτελεσμάτων – Εξαγωγή Κειμένου από TIFF

Τέλος, εμφανίζουμε το αναγνωρισμένο κείμενο. Μπορείτε να γράψετε την έξοδο σε ξεχωριστά αρχεία `.txt`, να την σπρώξετε σε μια βάση δεδομένων ή να την τροφοδοτήσετε σε έναν δείκτη αναζήτησης—ό,τι ταιριάζει στη ροή εργασίας σας.

```python
# Step 4: Iterate through the results and display the recognized text for each page
for page_index, result in enumerate(page_results):
    print(f"Page {page_index + 1}:\n{result.text}\n")
```

### Αναμενόμενη Έξοδος

```
Page 1:
Chapter 1
In the beginning...

Page 2:
The quick brown fox jumps over the lazy dog.

Page 3:
...

```

Κάθε συμβολοσειρά `result.text` περιέχει την ακατέργαστη έξοδο OCR για αυτή τη σελίδα. Αν χρειάζεστε διατήρηση των αλλαγών γραμμής, οι περισσότερες μηχανές εκθέτουν `result.lines` ως λίστα συμβολοσειρών.

## Διαχείριση Μεγάλων Αρχείων TIFF – Συμβουλές & Τεχνικές

Η επεξεργασία ενός TIFF 500 σελίδων μπορεί να απαιτεί πολύ μνήμη. Εδώ είναι μερικές στρατηγικές για να διατηρήσετε τα πράγματα ομαλά:

1. **Διαχωρίστε τις σελίδες** – Αντί για `recognize_multi_page`, καλέστε `engine.recognize(page)` μέσα σε έναν γεννήτρια που αποδίδει μία σελίδα τη φορά.
2. **Ρυθμίστε το DPI** – Η μείωση της ανάλυσης της εικόνας (π.χ., από 300 DPI σε 200 DPI) μειώνει το φορτίο CPU ενώ σχεδόν δεν επηρεάζει την ακρίβεια για το περισσότερο τυπωμένο κείμενο.
3. **Παραλληλοποίηση** – Αν η μηχανή OCR είναι thread‑safe, δημιουργήστε έναν `concurrent.futures.ThreadPoolExecutor` για να εκτελέσετε την αναγνώριση σε πολλαπλές σελίδες ταυτόχρονα.

```python
import concurrent.futures

def ocr_page(page):
    return engine.recognize(page).text

with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    texts = list(executor.map(ocr_page, tiff_image.pages))
```

## Αποθήκευση του Εξαγόμενου Κειμένου σε Αρχεία

Οι περισσότερες πραγματικές ροές εργασίας χρειάζονται μόνιμη αποθήκευση. Παρακάτω υπάρχει ένας σύντομος τρόπος για να αποθηκεύσετε το κείμενο κάθε σελίδας σε ξεχωριστό αρχείο, διατηρώντας τη σειρά των σελίδων.

```python
import pathlib

output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for i, result in enumerate(page_results, start=1):
    file_path = output_dir / f"page_{i:03}.txt"
    file_path.write_text(result.text, encoding="utf-8")
    print(f"Saved page {i} to {file_path}")
```

Τώρα έχετε έναν καθαρό φάκελο με αρχεία `.txt` έτοιμα για ευρετηρίαση ή περαιτέρω επεξεργασία NLP.

## Προεπισκόπηση Εικόνας – Πώς να Χρησιμοποιήσετε τα Αποτελέσματα OCR Οπτικά

Αν θέλετε να δείτε το overlay OCR στην αρχική εικόνα (χρήσιμο για εντοπισμό σφαλμάτων), πολλές βιβλιοθήκες σας επιτρέπουν να σχεδιάσετε πλαίσια. Εδώ είναι ένα γρήγορο παράδειγμα με χρήση του Pillow:

```python
from PIL import ImageDraw

for page, result in zip(tiff_image.pages, page_results):
    draw = ImageDraw.Draw(page)
    for word in result.words:          # Assume `result.words` gives bounding boxes
        draw.rectangle(word.box, outline="red")
    page.show()   # Opens the annotated page
```

![Πώς να χρησιμοποιήσετε OCR σε Python – Επικάλυψη OCR σε σελίδα TIFF](ocr_overlay_example.png)

*Κείμενο alt:* Πώς να χρησιμοποιήσετε OCR σε Python – οπτική επικάλυψη του αναγνωρισμένου κειμένου σε σελίδα TIFF.

## Συνηθισμένα Παράπλευρα Προβλήματα και Πώς να τα Αποφύγετε

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| Ασυνεπείς χαρακτήρες | Λάθος μοντέλο γλώσσας | Ορίστε `engine.language` στο σωστό enum |
| Αγνοούμενες σελίδες | Συμπίεση TIFF δεν υποστηρίζεται | Μετατρέψτε πρώτα σε ασυμπίεστο TIFF |
| Αργή απόδοση | Υψηλό DPI + επεξεργασία μονόνημα | Μειώστε DPI ή ενεργοποιήστε πολυνηματική επεξεργασία |
| Κενή έξοδος | Η εικόνα είναι πολύ σκοτεινή/χαμηλής αντίθεσης | Προεπεξεργασία με τέντωμα αντίθεσης (`opencv` ή `Pillow`) |

Η αντιμετώπιση αυτών νωρίς σας εξοικονομεί ώρες εντοπισμού σφαλμάτων αργότερα.

## Επόμενα Βήματα – Πέρα από τη Βασική Εξαγωγή

Τώρα που έχετε κατακτήσει τα βασικά του **πώς να χρησιμοποιήσετε OCR σε Python**, σκεφτείτε να εξερευνήσετε:

- **Δημιουργία PDF** – Συνδυάστε το εξαγόμενο κείμενο με το `reportlab` για να ξαναδημιουργήσετε PDF με δυνατότητα αναζήτησης.
- **Ανίχνευση γλώσσας** – Αυτόματη εναλλαγή του `engine.language` χρησιμοποιώντας το `langdetect`.
- **Εξαγωγή δομημένων δεδομένων** – Χρησιμοποιήστε κανονικές εκφράσεις ή το spaCy για να εξάγετε ημερομηνίες, ονόματα ή πίνακες από το ακατέργαστο κείμενο.
- **Εναλλακτικά OCR backends** – Αντικαταστήστε το `ocr` με `pytesseract` ή `easyocr` αν χρειάζεστε πολυγλωσσική υποστήριξη.

Κάθε ένα από αυτά τα θέματα συνδέεται φυσικά με τις δευτερεύουσες λέξεις-κλειδιά **ocr library python**, **convert tiff to text**, **extract text from tiff**, και **python ocr engine**, παρέχοντάς σας μια ισχυρή βάση για πιο προχωρημένα έργα.

---

### Συμπέρασμα

Καλύψαμε **πώς να χρησιμοποιήσετε OCR σε Python** από την εγκατάσταση έως την επεξεργασία πολλαπλών σελίδων, δείχνοντάς σας ακριβώς πώς να **μετατρέψετε TIFF σε κείμενο** και να **εξάγετε κείμενο από TIFF** χρησιμοποιώντας μια απλή **python OCR engine**. Το πλήρες, εκτελέσιμο παράδειγμα παραπάνω θα πρέπει να λειτουργεί αμέσως για τα περισσότερα τυπικά αρχεία TIFF, και οι συμβουλές που δόθηκαν θα σας βοηθήσουν να κλιμακώσετε σε μεγαλύτερα έγγραφα ή να ενσωματώσετε OCR σε μεγαλύτερες ροές εργασίας.

Δοκιμάστε το με τα δικά σας σαρωμένα βιβλία, αποδείξεις ή αρχειακές εικόνες—στη συνέχεια πειραματιστείτε με τις ιδέες επόμενου επιπέδου που αναφέρονται στην ενότητα “Επόμενα Βήματα”. Καλή προγραμματιστική δουλειά, και εύχομαι τα αποτελέσματα OCR σας να είναι πάντα ακριβή!

## Τι Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Βήμα‑Βήμα](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Πώς να εξάγετε κείμενο από tiff με Aspose.OCR για Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [Πώς να Εκτελέσετε Εξαγωγή Κειμένου από Εικόνα από Ροή Χρησιμοποιώντας Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}