---
category: general
date: 2026-05-31
description: Μάθετε πώς να χρησιμοποιείτε την περιοχή ενδιαφέροντος OCR για να φορτώνετε
  εικόνα για OCR και να εξάγετε κείμενο από το ορθογώνιο, ιδανικό για την αναγνώριση
  του ποσού σε τιμολόγιο.
draft: false
keywords:
- ocr region of interest
- extract text from rectangle
- load image for ocr
- how to extract amount
- recognize text from invoice
language: el
og_description: Κατακτήστε την περιοχή ενδιαφέροντος OCR για τη φόρτωση εικόνας, εξαγωγή
  κειμένου από το ορθογώνιο και αναγνώριση κειμένου από τιμολόγιο σε ένα ενιαίο σεμινάριο.
og_title: OCR Περιοχή Ενδιαφέροντος – Οδηγός Python βήμα‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  headline: OCR Region of Interest – Extract Text from Rectangle in Python
  type: TechArticle
- description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  name: OCR Region of Interest – Extract Text from Rectangle in Python
  steps:
  - name: Loads an invoice image from disk.
    text: Loads an invoice image from disk.
  - name: Marks a rectangular ROI where the total amount lives.
    text: Marks a rectangular ROI where the total amount lives.
  - name: Runs OCR only inside that ROI.
    text: Runs OCR only inside that ROI.
  - name: Prints the cleaned‑up amount string.
    text: Prints the cleaned‑up amount string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR Περιοχή Ενδιαφέροντος – Εξαγωγή Κειμένου από Ορθογώνιο σε Python
url: /el/python-java/general/ocr-region-of-interest-extract-text-from-rectangle-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Περιοχή Ενδιαφέροντος – Εξαγωγή Κειμένου από Ορθογώνιο σε Python

Έχετε αναρωτηθεί ποτέ πώς να **ocr region of interest** ένα συγκεκριμένο τμήμα μιας σαρωμένης απόδειξης χωρίς να τροφοδοτείτε ολόκληρη τη σελίδα στη μηχανή; Δεν είστε ο πρώτος που κοιτάζει ένα θολό απόδειξη και σκέφτεται, “Πώς μπορώ να εξάγω το ποσό που βρίσκεται κάπου κάτω δεξιά;” Τα καλά νέα είναι ότι μπορείτε να πείτε στη βιβλιοθήκη OCR ακριβώς πού να κοιτάξει, βελτιώνοντας δραματικά τόσο την ταχύτητα όσο και την ακρίβεια.

Σε αυτόν τον οδηγό θα περάσουμε από ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει πώς να **load image for OCR**, να ορίσετε μια **region of interest**, και στη συνέχεια να **extract text from rectangle** για να **recognize text from invoice** και να απαντήσετε στην κλασική ερώτηση “πώς να εξάγετε το ποσό”. Χωρίς ασαφείς αναφορές—μόνο συγκεκριμένος κώδικας, σαφείς εξηγήσεις, και μερικές συμβουλές που θα θέλατε να γνωρίζατε νωρίτερα.

---

## Τι Θα Δημιουργήσετε

Στο τέλος αυτού του tutorial θα έχετε ένα μικρό script Python που:

1. Φορτώνει μια εικόνα απόδειξης από το δίσκο.  
2. Σημαδεύει ένα ορθογώνιο ROI όπου βρίσκεται το συνολικό ποσό.  
3. Εκτελεί OCR μόνο μέσα σε αυτό το ROI.  
4. Εκτυπώνει το καθαρισμένο string του ποσού.  

Όλα αυτά λειτουργούν με οποιαδήποτε βιβλιοθήκη OCR που υποστηρίζει ROI—εδώ θα χρησιμοποιήσουμε ένα φανταστικό αλλά αντιπροσωπευτικό πακέτο `SimpleOCR` που μιμείται δημοφιλή εργαλεία όπως το Tesseract ή το EasyOCR. Μπορείτε να το αντικαταστήσετε ελεύθερα· οι έννοιες παραμένουν ίδιες.

---

## Προαπαιτούμενα

- Python 3.8+ εγκατεστημένο (`python --version` πρέπει να δείχνει ≥3.8).  
- Ένα πακέτο OCR που μπορεί να εγκατασταθεί μέσω pip (π.χ., `pip install simpleocr`).  
- Μια εικόνα απόδειξης (PNG ή JPEG) τοποθετημένη σε φάκελο που μπορείτε να αναφέρετε.  
- Βασική εξοικείωση με συναρτήσεις και κλάσεις Python (τίποτα περίπλοκο).

Αν έχετε ήδη όλα αυτά, τέλεια—ας βουτήξουμε. Αν όχι, πάρτε πρώτα την εικόνα· τα υπόλοιπα βήματα είναι ανεξάρτητα από το περιεχόμενο του αρχείου.

---

## Βήμα 1: Φόρτωση Εικόνας για OCR

Το πρώτο πράγμα που χρειάζεται οποιαδήποτε ροή εργασίας OCR είναι ένα bitmap για ανάγνωση. Οι περισσότερες βιβλιοθήκες εκθέτουν μια απλή μέθοδο `load_image` που δέχεται διαδρομή αρχείου. Να πώς το κάνετε με τη μηχανή `SimpleOCR` μας:

```python
# Step 1: Create an OCR engine instance and load the invoice image
from simpleocr import OcrEngine

# Initialize the engine (you can pass language settings here if needed)
ocr_engine = OcrEngine()

# Load the image – replace the path with yours
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")
```

> **Pro tip:** Χρησιμοποιήστε απόλυτες διαδρομές ή `os.path.join` για να αποφύγετε εκπλήξεις τύπου “file not found” όταν τρέχετε το script από διαφορετικό φάκελο εργασίας.

---

## Βήμα 2: Ορισμός Περιοχής Ενδιαφέροντος OCR

Αντί να αφήσουμε τη μηχανή να σαρώσει ολόκληρη τη σελίδα, της λέμε *ακριβώς* πού βρίσκεται το ποσό. Αυτό είναι το βήμα **ocr region of interest** και είναι το κλειδί για αξιόπιστη εξαγωγή, ειδικά όταν το έγγραφο περιέχει θορυβώδεις κεφαλίδες ή υποσέλιδα.

```python
# Step 2: Define the region of interest (ROI) where the amount appears
# Rectangle(x, y, width, height) – adjust these values for your layout
from simpleocr import Rectangle

amount_region = Rectangle(120, 340, 200, 40)   # x=120, y=340, w=200, h=40
ocr_engine.add_roi(amount_region)
```

Γιατί αυτά τα νούμερα; `x` και `y` είναι μετατοπίσεις εικονοστοιχείων από την πάνω‑αριστερή γωνία, ενώ `width` και `height` περιγράφουν το μέγεθος του κουτιού. Αν δεν είστε σίγουροι, ανοίξτε την εικόνα σε οποιονδήποτε επεξεργαστή, ενεργοποιήστε το χάρακα και σημειώστε τις συντεταγμένες. Πολλά IDE επιτρέπουν ακόμη να εκτυπώνετε τη θέση του κέρσορα ενώ αιωρείται.

---

## Βήμα 3: Εξαγωγή Κειμένου από Ορθογώνιο

Τώρα που το ROI είναι ορισμένο, ζητάμε από τη μηχανή να **recognize text from invoice** αλλά περιορισμένα στο ορθογώνιο που μόλις προσθέσαμε. Η κλήση επιστρέφει ένα αντικείμενο αποτελέσματος που συνήθως περιέχει το ακατέργαστο string, βαθμολογίες εμπιστοσύνης, και μερικές φορές τα πλαίσια περιγράμματος.

```python
# Step 3: Perform OCR on the specified ROI
ocr_result = ocr_engine.recognize()
```

Στο παρασκήνιο, η `recognize()` διατρέχει κάθε ROI, κόβει το αντίστοιχο τμήμα, τρέχει το μοντέλο OCR, και ενώνει τα αποτελέσματα. Γι' αυτό ο ορισμός μιας στενής **extract text from rectangle** περιοχής μπορεί να μειώσει δευτερόλεπτα από τον χρόνο επεξεργασίας για παρτίδες εργασιών.

---

## Βήμα 4: Πώς να Εξάγετε το Ποσό – Καθαρισμός της Εξόδου

Το OCR δεν είναι τέλειο· συχνά παίρνετε περιττά κενά, αλλαγές γραμμής, ή ακόμη και λανθασμένους χαρακτήρες (π.χ., “S” αντί για “5”). Ένα γρήγορο `strip()` και μια μικρή regex συνήθως λύνουν το πρόβλημα για χρηματικές τιμές.

```python
# Step 4: Clean and display the recognized amount
import re

raw_amount = ocr_result.text.strip()
# Simple regex to keep digits, commas, periods, and optional currency symbols
clean_amount = re.search(r'[\d,.]+', raw_amount)
if clean_amount:
    print("Amount:", clean_amount.group())
else:
    print("Could not locate a numeric amount in the ROI.")
```

> **Γιατί είναι σημαντικό:** Αν σκοπεύετε να στείλετε το ποσό σε βάση δεδομένων ή σε gateway πληρωμών, χρειάζεστε προβλέψιμη μορφή. Η αφαίρεση κενών και η φιλτράρισμα μη‑αριθμητικών χαρακτήρων αποτρέπει σφάλματα σε επόμενα βήματα.

---

## Βήμα 5: Αναγνώριση Κειμένου από Απόδειξη – Πλήρες Script

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι το πλήρες, έτοιμο‑για‑εκτέλεση script. Αποθηκεύστε το ως `extract_amount.py` και τρέξτε `python extract_amount.py`.

```python
# extract_amount.py
import re
from simpleocr import OcrEngine, Rectangle

def main():
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load the invoice image (adjust the path)
    ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")

    # Define ROI where the amount is located
    amount_region = Rectangle(120, 340, 200, 40)
    ocr_engine.add_roi(amount_region)

    # Run OCR on the ROI
    ocr_result = ocr_engine.recognize()

    # Clean and print the amount
    raw_amount = ocr_result.text.strip()
    match = re.search(r'[\d,.]+', raw_amount)
    if match:
        print("Amount:", match.group())
    else:
        print("Could not locate a numeric amount in the ROI.")

if __name__ == "__main__":
    main()
```

### Αναμενόμενη Έξοδος

```
Amount: 1,245.67
```

Αν το ROI είναι λανθασμένα ευθυγραμμισμένο, μπορεί να δείτε κάτι σαν `Amount: 1245.6S`—σημειώστε το περιττό “S”. Ρυθμίστε τις συντεταγμένες του ορθογωνίου και ξανατρέξτε μέχρι η έξοδος να φαίνεται καθαρή.

---

## Κοινά Προβλήματα & Ακραίες Περιπτώσεις

| Πρόβλημα | Γιατί Συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| **ROI πολύ μικρό** | Το κείμενο του ποσού περικόπτεται, οδηγώντας σε μερική αναγνώριση. | Αυξήστε το `width`/`height` κατά ~10‑20 % και δοκιμάστε ξανά. |
| **Λανθασμένο DPI** | Σαρώσεις χαμηλής ανάλυσης (≤150 dpi) μειώνουν την ακρίβεια του OCR. | Επαναδειγματοληπτήστε την εικόνα στα 300 dpi πριν τη φόρτωση, ή ζητήστε από το scanner υψηλότερο DPI. |
| **Πολλαπλά νομίσματα** | Η regex παίρνει την πρώτη αριθμητική ομάδα, η οποία μπορεί να είναι αριθμός απόδειξης. | Βελτιώστε τη regex ώστε να ψάχνει για σύμβολα νομισμάτων (`$`, `€`, `£`) πριν από τα ψηφία. |
| **Περιστροφές στις αποδείξεις** | Οι μηχανές OCR υποθέτουν ευθεία γραφή· οι περιστρεφόμενες σελίδες διακόπτουν την αναγνώριση. | Εφαρμόστε διόρθωση περιστροφής (`ocr_engine.rotate(90)`) πριν προσθέσετε ROI. |
| **Θόρυβος στο φόντο** | Σκιές ή σφραγίδες μπερδεύουν το μοντέλο. | Προεπεξεργαστείτε με απλό κατώφλι (`cv2.threshold`) ή χρησιμοποιήστε φίλτρο αποθορυβοποίησης. |

Η αντιμετώπιση αυτών των ακραίων περιπτώσεων νωρίς σας εξοικονομεί ώρες εντοπισμού σφαλμάτων αργότερα.

---

## Συμβουλές για Πραγματικά Έργα

- **Επεξεργασία σε Παρτίδες:** Επανάληψη πάνω σε φάκελο αποδείξεων, υπολογισμός ROI δυναμικά (π.χ., βάσει ανίχνευσης προτύπου), και αποθήκευση αποτελεσμάτων σε CSV.  
- **Ανίχνευση Προτύπου:** Αν διαχειρίζεστε πολλαπλά layout αποδείξεων, διατηρήστε έναν χάρτη JSON `template_id → ROI coordinates`. Αλλάξτε ROI βάσει γρήγορου ταξινομητή layout.  
- **Παράλληλη Εκτέλεση:** Χρησιμοποιήστε `concurrent.futures.ThreadPoolExecutor` για να τρέξετε πολλαπλές περιπτώσεις OCR ταυτόχρονα—ιδανικό για υψηλού όγκου pipelines back‑office.  
- **Φίλτρο Εμπιστοσύνης:** Τα περισσότερα αποτελέσματα OCR περιλαμβάνουν βαθμό εμπιστοσύνης. Απορρίψτε αποτελέσματα κάτω από ένα όριο (π.χ., 85 %) και σημαδέψτε τα για χειροκίνητη επανεξέταση.

---

## Συμπέρασμα

Καλύψαμε τα πάντα που χρειάζεστε για **ocr region of interest**, **load image for OCR**, **extract text from rectangle**, και τελικά **recognize text from invoice** ώστε να απαντήσετε στην κλασική ερώτηση **how to extract amount**. Το script είναι σύντομο, αλλά αρκετά ευέλικτο ώστε να προσαρμοστεί σε διαφορετικές μορφές εγγράφων, γλώσσες, και OCR back‑ends.

Τώρα που έχετε κατακτήσει τα βασικά, σκεφτείτε να επεκτείνετε τη ροή: προσθέστε σάρωση barcode, ενσωματώστε έναν parser PDF, ή στείλτε το εξαγόμενο ποσό σε API λογισμικού. Ο ουρανός είναι το όριο, και με καλά ορισμένο ROI θα έχετε πάντα πιο γρήγορα και καθαρά αποτελέσματα.

Αν αντιμετωπίσετε κάποιο πρόβλημα, αφήστε ένα σχόλιο παρακάτω—καλή OCR εμπειρία!

![ocr region of interest example](https://example.com/ocr_roi_example.png "ocr region of interest example")


## Τι Θα Πρέπει να Μάθετε Στη Σειρά;

- [Πώς να Εξάγετε Κείμενο από Εικόνα Προετοιμάζοντας Ορθογώνια στο OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Εξαγωγή Κειμένου από Εικόνα Java με Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Εξαγωγή Κειμένου από Εικόνα – Βελτιστοποίηση OCR με Aspose.OCR για .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}