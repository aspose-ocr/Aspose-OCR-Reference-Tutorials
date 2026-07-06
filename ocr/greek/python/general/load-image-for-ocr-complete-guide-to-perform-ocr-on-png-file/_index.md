---
category: general
date: 2026-06-25
description: Φορτώστε εικόνα για OCR και εκτελέστε OCR σε PNG με έναν βήμα‑βήμα οδηγό
  Python χρησιμοποιώντας aocr. Μάθετε εντοπισμό σφαλμάτων, καταγραφή και βέλτιστες
  πρακτικές.
draft: false
keywords:
- load image for OCR
- perform OCR on PNG
- aocr logging setup
- OCR debugging Python
- image preprocessing OCR
language: el
og_description: Φορτώστε εικόνα για OCR και εκτελέστε OCR σε PNG χρησιμοποιώντας το
  aocr. Αυτός ο οδηγός σας καθοδηγεί μέσω της καταγραφής, της φόρτωσης εικόνας και
  της αναγνώρισης με πλήρες κώδικα.
og_title: Φόρτωση εικόνας για OCR – Python οδηγός βήμα‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Load image for OCR and perform OCR on PNG with a step‑by‑step Python
    tutorial using aocr. Learn debugging, logging, and best practices.
  headline: Load Image for OCR – Complete Guide to Perform OCR on PNG Files
  type: TechArticle
- questions:
  - answer: Usually not. `aocr` handles PNG natively, but if the image is huge (>10
      MP) you might want to downscale first to speed up processing.
    question: Do I need to convert the PNG to another format?
  - answer: Rotate the log after each run or limit the level to `INFO` once you’re
      confident the pipeline works.
    question: What if the logger file grows too large?
  - answer: Absolutely. Just call `ocr_png` for each file; the function creates a
      fresh logger each time, keeping logs isolated.
    question: Can I process multiple images in a loop?
  - answer: Yes – `engine.result` also contains `boxes` and `confidences`. Explore
      the `aocr` docs for `result.boxes` if you need layout information.
    question: Is there a way to get bounding boxes instead of plain text?
  type: FAQPage
tags:
- OCR
- Python
- aocr
title: Φόρτωση εικόνας για OCR – Πλήρης οδηγός για την εκτέλεση OCR σε αρχεία PNG
url: /el/python/general/load-image-for-ocr-complete-guide-to-perform-ocr-on-png-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Φόρτωση Εικόνας για OCR – Πλήρης Οδηγός για Εκτέλεση OCR σε Αρχεία PNG

Κάποτε χρειάστηκε να **φορτώσετε εικόνα για OCR** αλλά δεν ήξερες πώς να ρυθμίσεις σωστά την αποσφαλμάτωση; Δεν είσαι μόνος. Σε πολλά έργα το πρώτο εμπόδιο είναι να φέρεις το PNG στη μηχανή ενώ ταυτόχρονα μπορείς να δεις τι συμβαίνει «κάτω από το καπό».

Σε αυτό το tutorial θα σε καθοδηγήσουμε βήμα‑βήμα σε ό,τι χρειάζεται για να **εκτελέσεις OCR σε PNG** αρχεία χρησιμοποιώντας τη βιβλιοθήκη `aocr` – από τη ρύθμιση ενός logger για λεπτομερή έξοδο μέχρι την πραγματική αναγνώριση κειμένου. Στο τέλος θα έχεις ένα επαναχρησιμοποιήσιμο script που μπορείς να ενσωματώσεις σε οποιοδήποτε έργο Python, και θα καταλάβεις γιατί κάθε κομμάτι είναι σημαντικό.

## Τι Θα Μάθεις

- Πώς να αρχικοποιήσεις το logger του `aocr` ώστε να παρακολουθείς κάθε βήμα.  
- Τον ακριβή κώδικα για **φόρτωση εικόνας για OCR** με `aocr.OcrEngine`.  
- Πώς να ρυθμίσεις το επίπεδο logging για λεπτομερείς πληροφορίες debug.  
- Εκτέλεση της μηχανής για **εκτέλεση OCR σε PNG** και λήψη των αποτελεσμάτων.  
- Συμβουλές για την αντιμετώπιση κοινών προβλημάτων όπως ελλιπή αρχεία ή μη υποστηριζόμενες μορφές.

Δεν απαιτείται προγενέστερη εμπειρία με το `aocr`; αρκεί μια λειτουργική εγκατάσταση Python 3 και μια εικόνα που θέλεις να διαβάσεις. Ας ξεκινήσουμε.

![load image for OCR example](assets/load-image-ocr.png "Εικονογράφηση της φόρτωσης μιας εικόνας για OCR σε Python")

## Προαπαιτούμενα

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|-----------------------|
| Python 3.8+ | Το `aocr` στοχεύει σε σύγχρονους διερμηνείς και χρησιμοποιεί type hints. |
| Βιβλιοθήκη `aocr` εγκατεστημένη (`pip install aocr`) | Χωρίς το πακέτο οι κλάσεις που χρησιμοποιούμε δεν θα υπάρχουν. |
| Ένα PNG αρχείο που θέλεις να διαβάσεις | Το tutorial εστιάζει στην **εκτέλεση OCR σε PNG**, οπότε ένα PNG είναι απαραίτητο. |
| Δικαίωμα εγγραφής σε φάκελο καταγραφής | Ο logger χρειάζεται να δημιουργήσει το `ocr_debug.log`. |

Αν λείπει κάτι από τα παραπάνω, εγκατέστησέ το τώρα – παίρνει μόνο ένα λεπτό.

```bash
pip install aocr
```

## Βήμα 1: Φόρτωση Εικόνας για OCR – Αρχικοποίηση Logging

Πριν αγγίξεις την εικόνα, ρύθμισε έναν logger. Η αποσφαλμάτωση του OCR μπορεί να γίνει εφιάλτης αν δεν βλέπεις τι κάνει η μηχανή. Η κλάση `aocr.Logging` γράφει τα πάντα σε αρχείο, και ορίζοντας το επίπεδο σε `DEBUG` θα δεις κάθε εσωτερική κλήση.

```python
import aocr

# Create a logger instance
ocr_logger = aocr.Logging()
# Choose where the log file will live – adjust the path to suit your project
ocr_logger.set_output_file("logs/ocr_debug.log")

# DEBUG gives you the most detail; you can switch to INFO for less noise
ocr_logger.set_level(aocr.LoggingLevel.DEBUG)
```

**Γιατί είναι σημαντικό:**  
Αν η μηχανή OCR δεν βρει το αρχείο ή η μορφή της εικόνας δεν υποστηρίζεται, ο logger θα καταγράψει το stack trace της εξαίρεσης. Αυτό σε σώζει από ατελείωτες εικασίες αργότερα.

## Βήμα 2: Εκτέλεση OCR σε PNG – Διαμόρφωση της Μηχανής

Τώρα που ο logger είναι έτοιμος, σύνδεσέ τον με τη μηχανή OCR. Αυτό το βήμα ενώνει τα δύο ώστε κάθε ενέργεια της μηχανής να καταγράφεται.

```python
# Initialise the OCR engine
ocr_engine = aocr.OcrEngine()
# Plug the logger into the engine
ocr_engine.logging = ocr_logger
```

**Pro tip:**  
Μπορείς να επαναχρησιμοποιήσεις το ίδιο αντικείμενο `ocr_engine` για πολλαπλές εικόνες. Απλώς θυμήσου να καθαρίσεις τυχόν προηγούμενη κατάσταση αν επεξεργάζεσαι παρτίδα.

## Βήμα 3: Φόρτωση Εικόνας για OCR – Φόρτωση του Αρχείου PNG

Αυτή είναι η καρδιά του tutorial: η πραγματική **φόρτωση εικόνας για OCR**. Η μέθοδος `load_image` δέχεται διαδρομή αρχείου· εσωτερικά αποκωδικοποιεί το PNG σε bitmap που η μηχανή μπορεί να καταλάβει.

```python
# Path to the PNG you want to read
image_path = "samples/invoice.png"

# Load the image – this is where we “load image for OCR”
ocr_engine.load_image(image_path)
```

### Περιπτώσεις Ακρόασης

1. **Αρχείο Δεν Βρέθηκε** – Αν η διαδρομή είναι λανθασμένη, το `aocr` ρίχνει `FileNotFoundError`. Ο logger θα το σημειώσει, αλλά μπορείς επίσης να το πιάσεις:

   ```python
   try:
       ocr_engine.load_image(image_path)
   except FileNotFoundError as e:
       print(f"❌ Could not locate {image_path}: {e}")
       raise
   ```

2. **Μη Υποστηριζόμενη Μορφή** – Αν και το PNG υποστηρίζεται ευρέως, ένα κατεστραμμένο αρχείο μπορεί να προκαλέσει `UnsupportedFormatError`. Σε αυτήν την περίπτωση, σκέψου να μετατρέψεις την εικόνα σε καθαρό PNG με το Pillow πριν τη φόρτωση.

## Βήμα 4: Εκτέλεση OCR σε PNG – Εκτέλεση Αναγνώρισης

Τώρα που η εικόνα είναι στη μνήμη, μπορείς τελικά να **εκτελέσεις OCR σε PNG**. Η μέθοδος `recognize` εκκινεί τις pipelines της μηχανής (προεπεξεργασία, τμηματοποίηση, ταξινόμηση) και γεμίζει το αντικείμενο αποτελέσματος.

```python
# Execute the OCR process
ocr_engine.recognize()
```

Μετά από αυτήν την κλήση, η μηχανή κρατά το αναγνωρισμένο κείμενο. Μπορείς να το προσπελάσεις μέσω του χαρακτηριστικού `result`:

```python
# Retrieve the plain text output
recognized_text = ocr_engine.result.text
print("📝 OCR Result:")
print(recognized_text)
```

**Γιατί πρέπει να ελέγχεις το αποτέλεσμα:**  
Κάποιες μηχανές OCR επιστρέφουν κενές συμβολοσειρές για εικόνες χαμηλής αντίθεσης. Η άμεση προβολή του αποτελέσματος σε επιτρέπει να αποφασίσεις αν χρειάζεται προεπεξεργασία (π.χ. αύξηση αντίθεσης) πριν επανεκτελέσεις.

## Βήμα 5: Συνοψίζοντας – Μία Επαναχρησιμοποιήσιμη Συνάρτηση

Η συνένωση των κομματιών σε μία μόνο συνάρτηση κάνει εύκολη την κλήση από άλλα scripts ή web service. Αυτό επίσης δείχνει πώς να **φορτώνεις εικόνα για OCR** και να **εκτελείς OCR σε PNG** σε ένα καθαρό πακέτο.

```python
def ocr_png(image_path: str, log_dir: str = "logs") -> str:
    """
    Load a PNG image, run aocr OCR, and return the extracted text.
    
    Parameters
    ----------
    image_path : str
        Full path to the PNG file.
    log_dir : str, optional
        Directory where the debug log will be written.
    
    Returns
    -------
    str
        The plain‑text OCR result.
    """
    import os
    import aocr

    # Ensure the log directory exists
    os.makedirs(log_dir, exist_ok=True)

    # ---------- Logging ----------
    logger = aocr.Logging()
    logger.set_output_file(os.path.join(log_dir, "ocr_debug.log"))
    logger.set_level(aocr.LoggingLevel.DEBUG)

    # ---------- Engine ----------
    engine = aocr.OcrEngine()
    engine.logging = logger

    # ---------- Load Image ----------
    try:
        engine.load_image(image_path)
    except Exception as exc:
        logger.error(f"Failed to load image {image_path}: {exc}")
        raise

    # ---------- Recognize ----------
    engine.recognize()
    return engine.result.text

# Example usage
if __name__ == "__main__":
    txt = ocr_png("samples/invoice.png")
    print("\n--- Extracted Text ---\n")
    print(txt)
```

Η εκτέλεση του script θα δημιουργήσει ένα λεπτομερές `ocr_debug.log` στον φάκελο `logs`, και στη συνέχεια θα εκτυπώσει το αναγνωρισμένο κείμενο στην κονσόλα. Έχεις πλέον ένα εργαλείο **εκτέλεσης OCR σε PNG** που μπορείς να εισάγεις οπουδήποτε.

## Συχνές Ερωτήσεις & Παγίδες

- **Πρέπει να μετατρέψω το PNG σε άλλη μορφή;**  
  Συνήθως όχι. Το `aocr` διαχειρίζεται το PNG εγγενώς, αλλά αν η εικόνα είναι τεράστια (>10 MP) ίσως θελήσεις να την μειώσεις πρώτα για να επιταχύνεις την επεξεργασία.

- **Τι γίνεται αν το αρχείο καταγραφής μεγαλώσει πολύ;**  
  Περιστρέψτε το log μετά από κάθε εκτέλεση ή περιορίστε το επίπεδο σε `INFO` όταν είστε σίγουροι ότι η αλυσίδα λειτουργεί.

- **Μπορώ να επεξεργαστώ πολλαπλές εικόνες σε βρόχο;**  
  Απόλυτα. Απλώς κάλεσε `ocr_png` για κάθε αρχείο· η συνάρτηση δημιουργεί νέο logger κάθε φορά, κρατώντας τα logs ξεχωριστά.

- **Υπάρχει τρόπος να λάβω τα bounding boxes αντί για απλό κείμενο;**  
  Ναι – το `engine.result` περιέχει επίσης `boxes` και `confidences`. Εξερεύνησε την τεκμηρίωση του `aocr` για `result.boxes` αν χρειάζεσαι πληροφορίες διάταξης.

## Συμπέρασμα

Τώρα ξέρεις πώς να **φορτώνεις εικόνα για OCR** και να **εκτελείς OCR σε PNG** χρησιμοποιώντας τη βιβλιοθήκη `aocr`, με μια στιβαρή ρύθμιση logging που κάνει την αποσφαλμάτωση αβίαστη. Η παράδειγμα συνάρτηση ενσωματώνει όλη τη ροή εργασίας, ώστε να την ενσωματώσεις σε οποιοδήποτε έργο και να αρχίσεις να εξάγεις κείμενο αμέσως.

Τι θα κάνεις μετά; Δοκίμασε να τροφοδοτήσεις τη μηχανή με διαφορετικούς τύπους εικόνας (JPEG, TIFF) για να δεις πώς αλλάζει η ακρίβεια, ή πειραματίσου με τεχνικές προεπεξεργασίας όπως thresholding για να βελτιώσεις τα αποτελέσματα σε θορυβώδεις σκαναρίσματα. Και αν σε ενδιαφέρει η εξαγωγή δομημένων δεδομένων (πίνακες, φόρμες), ρίξε μια ματιά στις ενότητες `aocr` για ανάλυση διάταξης – ταιριάζουν τέλεια με ό,τι έφτιαξες.

Καλό coding, και οι OCR pipelines σου να είναι πάντα χωρίς σφάλματα!

## Τι Πρέπει Να Μάθεις Στη Σύντομη Μελλοντική

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κυριαρχήσεις επιπλέον δυνατότητες του API και να εξερευνήσεις εναλλακτικές προσεγγίσεις στα δικά σου έργα.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}