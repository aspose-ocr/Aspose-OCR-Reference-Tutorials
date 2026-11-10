---
category: general
date: 2026-07-05
description: Πραγματοποιήστε OCR σε εικόνα χρησιμοποιώντας Python. Μάθετε πώς να μετατρέψετε
  εικόνα σε κείμενο με Python, να φορτώσετε εικόνα για OCR και να εξάγετε κυριλλικό
  κείμενο από την εικόνα σε λίγα λεπτά.
draft: false
keywords:
- perform OCR on image
- convert image to text python
- load image for OCR
- extract Cyrillic text from image
- recognize Cyrillic text
language: el
og_description: Κάντε OCR σε εικόνα με Python. Αυτός ο οδηγός σας δείχνει πώς να μετατρέψετε
  μια εικόνα σε κείμενο με Python, να φορτώσετε εικόνα για OCR και να εξάγετε κυριλλικό
  κείμενο από την εικόνα γρήγορα.
og_title: Εκτελέστε OCR σε εικόνα με Python – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Perform OCR on image using Python. Learn how to convert image to text
    python, load image for OCR and extract Cyrillic text from image in minutes.
  headline: Perform OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- Cyrillic
title: Εκτελέστε OCR σε εικόνα με Python – Πλήρης οδηγός βήμα‑βήμα
url: /el/python/general/perform-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Perform OCR on Image with Python – Complete Step‑by‑Step Guide

Έχετε αναρωτηθεί ποτέ πώς να **perform OCR on image** αρχεία χωρίς να τα παραδίδετε σε υπηρεσία τρίτου; Δεν είστε μόνοι. Σε πολλά έργα—σκανάρες διαβατηρίων, ψηφιοποιητές αποδείξεων ή εργαλεία αρχειοθέτησης—η λήψη ακατέργαστου κειμένου από μια εικόνα είναι το πρώτο εμπόδιο.  

Σε αυτόν τον οδηγό θα περάσουμε από ένα πρακτικό παράδειγμα που **converts image to text python** στυλ, θα σας δείξει πώς να **load image for OCR**, και τελικά **extract Cyrillic text from image** χρησιμοποιώντας τη βιβλιοθήκη ανοιχτού κώδικα `aocr`. Στο τέλος θα μπορείτε να **recognize Cyrillic text** σε οποιαδήποτε εικόνα τηςρίσετε.

> **Τι θα αποκομίσετε:** ένα έτοιμο‑για‑εκτέλεση script, σαφείς εξηγήσεις κάθε βήματος, και συμβουλές για την αντιμετώπιση κοινών προβλημάτων (όπως θολές σαρώσεις ή απρόσμενες γραμματοσειρές). Χωρίς εξωτερικά APIs, μόνο καθαρή Python.

---

## Απαιτούμενα

- Python 3.8 ή νεότερη εγκατεστημένη.
- Ένα τερματικό ή command prompt με το οποίο αισθάνεστε άνετα.
- Το πακέτο `aocr` (εγκαταστάσιμο μέσω `pip install aocr`).
- Ένα αρχείο εικόνας που περιέχει χαρακτήρες Κυριλλικού (π.χ., σαρωμένο ρωσικό διαβατήριο).  

Αν κάποιο από αυτά σας φαίνεται άγνωστο, μην πανικοβληθείτε—κάθε σημείο θα καλυφθεί σύντομα καθώς προχωράμε.

---

## Βήμα 1: Perform OCR on Image – Ρύθμιση του Περιβάλλοντος

Το πρώτο πράγμα που χρειαζόμαστε είναι ένα καθαρό περιβάλλον Python όπου ζει η βιβλιοθήκη OCR. Η χρήση εικονικού περιβάλλοντος απομονώνει τις εξαρτήσεις και αποτρέπει συγκρούσεις εκδόσεων.

```bash
# Create a virtual environment (optional but recommended)
python -m venv ocr-env
# Activate it (Windows)
ocr-env\Scripts\activate
# Activate it (macOS/Linux)
source ocr-env/bin/activate

# Install the aocr library
pip install aocr
```

**Γιατί;**  
Ένα αφιερωμένο περιβάλλον εξασφαλίζει ότι το πακέτο `aocr` και τα εγγενή του binaries δεν παρεμβαίνουν σε άλλα έργα. Επίσης κάνει την αναπαραγωγιμότητα παιχνιδάκι—κάποιος άλλος μπορεί να κλωνοποιήσει το αποθετήριό σας και να εκτελέσει την ίδια εντολή `pip install -r requirements.txt`.

> **Συμβουλή:** Παγώστε τις εξαρτήσεις σας με `pip freeze > requirements.txt` ώστε να γνωρίζετε πάντα ακριβώς ποιες εκδόσεις χρησιμοποιήθηκαν.

---

## Βήμα 2: Load Image for OCR – Εισαγωγή και Προετοιμασία του Αρχείου

Τώρα που η βιβλιοθήκη είναι έτοιμη, χρειάζεται να **load image for OCR**. Η μέθοδος `aocr.Image.from_file` διαχειρίζεται τις πιο κοινές μορφές (PNG, JPEG, TIFF). Να πώς το κάνετε:

```python
import aocr

# Path to the Cyrillic image – replace with your actual file location
image_path = "YOUR_DIRECTORY/rus_passport.png"

# Load the image into an aocr.Image object
cyrillic_image = aocr.Image.from_file(image_path)
```

**Τι συμβαίνει εδώ;**  
`aocr.Image.from_file` διαβάζει τα δυαδικά δεδομένα, τα αποκωδικοποιεί και τα αποθηκεύει σε ένα αντικείμενο που μπορεί να καταλάβει η μηχανή OCR. Αν το αρχείο δεν βρεθεί, η Python θα ρίξει ένα `FileNotFoundError`, το οποίο μπορείτε να πιάσετε αργότερα αν χρειάζεστε ευγενική διαχείριση σφαλμάτων.

> **Ειδική περίπτωση:** Κάποιοι σαρωτές παράγουν multi‑page TIFFs. Σε αυτήν την περίπτωση, θα χρειαστεί να χωρίσετε τις σελίδες πρώτα—`aocr` παρέχει `Image.from_tiff_pages()` γι' αυτό.

---

## Βήμα 3: Configure the OCR Engine – Εξαναγκασμός Αναγνώρισης Κυριλλικού

Από προεπιλογή, πολλές μηχανές OCR προσπαθούν να μαντέψουν τη γλώσσα, κάτι που μπορεί να οδηγήσει σε ακατάλληλο αποτέλεσμα για μη‑λατινικά σενάρια. Για να **recognize Cyrillic text** αξιόπιστα, ορίζουμε ρητά τη γλώσσα σε “cyrillic”.

```python
# Create an OCR engine instance
ocr_engine = aocr.OcrEngine()

# Force the engine to use the Cyrillic recognizer
ocr_engine.language = "cyrillic"
```

**Γιατί να εξαναγκάσουμε τη γλώσσα;**  
Οι χαρακτήρες Κυριλλικού μοιράζονται οπτικές ομοιότητες με τα λατινικά γράμματα (π.χ., “A” vs “Α”). Η ενημέρωση της μηχανής να περιμένει Κυριλλικό μειώνει δραστικά τις λανθασμένες αναγνώσεις, ειδικά σε σαρώσεις χαμηλής ανάλυσης.

---

## Βήμα 4: Perform OCR on Image – Εκτέλεση της Αναγνώρισης

Με την εικόνα φορτωμένη και τη μηχανή ρυθμισμένη, τελικά **perform OCR on image**. Η μέθοδος `recognize` επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει το εξαγόμενο κείμενο και τις βαθμολογίες εμπιστοσύνης.

```python
# Run the OCR process
ocr_result = ocr_engine.recognize(cyrillic_image)

# Print the raw text
print("Cyrillic text:")
print(ocr_result.text)
```

**Τι παρέχει το `ocr_result`;**  
- `text`: η απλή συμβολοσειρά των αναγνωρισμένων χαρακτήρων.  
- `confidence`: ένα float (0‑1) που υποδεικνύει τη συνολική βεβαιότητα.  
- `lines`: μια λίστα αντικειμένων γραμμής αν χρειάζεστε λεπτομερή έλεγχο.  

> **Συχνή ερώτηση:** *Τι γίνεται αν το κείμενο είναι ανάποδα;*  
> `aocr` μπορεί να περιστρέψει αυτόματα τις εικόνες· απλώς ορίστε `ocr_engine.auto_rotate = True` πριν καλέσετε το `recognize`.

---

## Βήμα 5: Convert Image to Text Python – Μετά‑επεξεργασία του Αποτελέσματος

Η ακατέργαστη συμβολοσειρά μπορεί να περιέχει περιττά κενά ή τεμάχια αλλαγής γραμμής. Για να **convert image to text python** στυλ, θα το καθαρίσουμε με μερικά απλά βήματα:

```python
import re

# Remove extra whitespace and normalize line breaks
clean_text = re.sub(r'\s+', ' ', ocr_result.text).strip()

print("\nCleaned Cyrillic text:")
print(clean_text)
```

**Γιατί να ασχοληθείτε;**  
Το καθαρισμένο αποτέλεσμα είναι πιο εύκολο να τροφοδοτηθεί σε επόμενες διαδικασίες—είτε το αποθηκεύετε σε βάση δεδομένων, το στέλνετε σε API μετάφρασης, ή εκτελείτε αναζητήσεις regex για αριθμούς διαβατηρίων.

---

## Βήμα 6: Extract Cyrillic Text from Image – Συνδυάζοντας Όλα

Ας ενσωματώσουμε τα πάντα σε μια ενιαία, επαναχρησιμοποιήσιμη συνάρτηση. Αυτό κάνει το **extract Cyrillic text from image** μια γραμμή κώδικα στα δικά σας έργα.

```python
def extract_cyrillic_text(image_path: str) -> str:
    """
    Loads an image, forces Cyrillic OCR, and returns cleaned text.
    """
    # Load image
    img = aocr.Image.from_file(image_path)

    # Configure OCR engine for Cyrillic
    engine = aocr.OcrEngine()
    engine.language = "cyrillic"

    # Recognize text
    result = engine.recognize(img)

    # Clean up the output
    cleaned = re.sub(r'\s+', ' ', result.text).strip()
    return cleaned

# Example usage
if __name__ == "__main__":
    path = "YOUR_DIRECTORY/rus_passport.png"
    print("Extracted text:", extract_cyrillic_text(path))
```

**Αποτέλεσμα που θα πρέπει να δείτε (παράδειγμα):**

```
Extracted text: ПАСПОРТ РФ № 1234567890 ИМЯ ФАМИЛИЯ ДАТА РОЖДЕНИЯ 01.01.1990
```

Αν η εικόνα είναι καθαρή και η γραμματοσειρά ταιριάζει με το μοντέλο OCR, θα έχετε σχεδόν τέλεια μεταγραφή.

---

## Αντιμετώπιση προβλημάτων & Συμβουλές

| Πρόβλημα | Πιθανή Αιτία | Διόρθωση |
|----------|--------------|----------|
| Ασυνεπές κείμενο | Λάθος ρύθμιση γλώσσας | Ensure `ocr_engine.language = "cyrillic"` |
| Κενό αποτέλεσμα | Η εικόνα είναι πολύ σκοτεινή ή χαμηλής ανάλυσης | Preprocess with `opencv` to increase contrast |
| Λάθος προσανατολισμός | Η εικόνα είναι περιστραμμένη 90° | Set `ocr_engine.auto_rotate = True` |
| Αργή απόδοση | Μεγάλη εικόνα ( >5 MP ) | Resize with `aocr.Image.resize(width=1024)` before recognition |

---

![παράδειγμα εκτέλεσης OCR σε εικόνα](ocr_example.png "παράδειγμα εκτέλεσης OCR σε εικόνα")

*Κείμενο alt: “παράδειγμα εκτέλεσης OCR σε εικόνα που δείχνει κώδικα Python που εξάγει Κυριλλικό κείμενο από σάρωση διαβατηρίου.”*

---

## Συμπέρασμα

Μόλις **performed OCR on image** αρχεία χρησιμοποιώντας καθαρή Python, μάθαμε πώς να **load image for OCR**, εξαναγκάσαμε τη μηχανή να **recognize Cyrillic text**, και τελικά **extract Cyrillic text from image** με μια τακτοποιημένη βοηθητική συνάρτηση. Ολόκληρη η αλυσίδα—από την εγκατάσταση του `aocr` μέχρι τον καθαρισμό του αποτελέσματος—χωρά σε μερικές δεκάδες γραμμές κώδικα και μπορεί να ενσωματωθεί σε οποιοδήποτε έργο που χρειάζεται **convert image to text python** στυλ.

---

## Τι Ακολουθεί;

- **Batch processing:** Επανάληψη πάνω σε φάκελο σαρώσεων και αποθήκευση αποτελεσμάτων σε SQLite.  
- **Language detection:** Συνδυάστε το `langdetect` με το `aocr` για αυτόματη εναλλαγή μεταξύ Κυριλλικού και Λατινικού.  
- **Advanced preprocessing:** Χρησιμοποιήστε το `opencv` για διόρθωση κλίσης, μείωση θορύβου ή δυαδικοποίηση εικόνων για μεγαλύτερη ακρίβεια.  
- **Integrate with FastAPI:** Εκθέστε τη συνάρτηση `extract_cyrillic_text` ως REST endpoint για web εφαρμογές.  

Μη διστάσετε να πειραματιστείτε—αλλάξτε τη γλώσσα σε “latin” για αγγλικά διαβατήρια, ή δοκιμάστε μια διαφορετική μηχανή OCR εντελώς. Οι έννοιες παραμένουν ίδιες, και ο κώδικας είναι αρκετά ευέλικτος για προσαρμογή.

Καλή προγραμματισμό, και εύχομαι οι εικόνες σας να είναι πάντα αναγνώσιμες!

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Βήμα‑βήμα](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Μετατροπή Εικόνας σε Κείμενο – Εκτέλεση OCR σε Εικόνα από URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}