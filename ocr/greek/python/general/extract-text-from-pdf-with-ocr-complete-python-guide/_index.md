---
category: general
date: 2026-02-09
description: Εξαγωγή κειμένου από PDF με OCR χρησιμοποιώντας το Aspose σε Python.
  Μάθετε πώς να διαβάζετε PDF με OCR, να φορτώνετε PDF για OCR και να κατακτήσετε
  την αποδοτική εξαγωγή κειμένου από PDF.
draft: false
keywords:
- extract text from pdf
- read pdf with ocr
- load pdf for ocr
- how to extract pdf text
language: el
og_description: Εξαγωγή κειμένου από PDF με OCR χρησιμοποιώντας το Aspose. Αυτός ο
  οδηγός δείχνει πώς να διαβάσετε PDF με OCR, να φορτώσετε PDF για OCR και απαντά
  στο πώς να εξάγετε κείμενο από PDF.
og_title: Εξαγωγή κειμένου από PDF με OCR – Εγχειρίδιο Python
tags:
- OCR
- Python
- PDF processing
title: Εξαγωγή κειμένου από PDF με OCR – Πλήρης οδηγός Python
url: /el/python/general/extract-text-from-pdf-with-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από PDF με OCR – Πλήρης Οδηγός Python

Έχετε χρειαστεί ποτέ να **εξάγετε κείμενο από PDF** αλλά το αρχείο είναι μόνο μια σαρωμένη εικόνα; Δεν είστε μόνοι που αντιμετωπίζετε αυτό το πρόβλημα. Σε πολλά πραγματικά έργα τα PDF που λαμβάνετε είναι μόνο εικόνες, έτσι μια απλή κλήση «read PDF» δεν επιστρέφει τίποτα. Εδώ έρχεται το OCR, και σήμερα θα σας δείξουμε ακριβώς **πώς να εξάγετε κείμενο από PDF** χρησιμοποιώντας το Aspose OCR για Python.

Σε αυτό το tutorial θα μάθετε να **διαβάζετε PDF με OCR**, θα δείτε τον καλύτερο τρόπο να **φορτώσετε PDF για OCR**, και θα περάσετε από ένα πλήρες παράδειγμα που επιστρέφει κάθε λέξη μαζί με το σκορ εμπιστοσύνης της. Χωρίς ασαφείς αναφορές—απλώς ένα εκτελέσιμο script, εξηγήσεις για το γιατί κάθε γραμμή είναι σημαντική, και συμβουλές που μπορείτε να εφαρμόσετε αμέσως.

## Τι Καλύπτει Αυτός ο Οδηγός

Θα ξεκινήσουμε εγκαθιστώντας το πακέτο Aspose OCR, στη συνέχεια θα δημιουργήσουμε ένα `OcrEngine`, θα φορτώσουμε ένα PDF, θα εκτελέσουμε δομημένη αναγνώριση, και τέλος θα εξάγουμε κάθε λέξη και την εμπιστοσύνη της. Στο τέλος θα μπορείτε να απαντήσετε στην ερώτηση “**πώς να εξάγετε κείμενο από PDF**?” για οποιοδήποτε σαρωμένο έγγραφο, και θα κατανοήσετε τις διαφορές μεταξύ δομημένου και απλού OCR.  

Οι προαπαιτήσεις είναι ελάχιστες: Python 3.8+, μια βιβλιοθήκη Aspose OCR που μπορεί να εγκατασταθεί με pip, και ένα PDF που θέλετε να επεξεργαστείτε. Αν είστε άνετοι με βασικούς βρόχους Python, είστε έτοιμοι.  

Γιατί είναι σημαντικό; Επειδή τα σκορ εμπιστοσύνης σας επιτρέπουν να φιλτράρετε αυτόματα αποτελέσματα χαμηλής ποιότητας, και το δομημένο κείμενο σας δίνει ιεραρχία σελίδας, μπλοκ, γραμμής και λέξης—τέλεια για downstream analytics ή ευρετήρια αναζήτησης.

---

![Εξαγωγή κειμένου από PDF χρησιμοποιώντας Aspose OCR](https://example.com/placeholder-image.jpg "εξαγωγή κειμένου από pdf")

*Κείμενο εναλλακτικής εικόνας: “εξαγωγή κειμένου από pdf χρησιμοποιώντας τη μηχανή Aspose OCR σε Python”*

## Βήμα 1 – Εγκατάσταση και Εισαγωγή του Aspose OCR

Πριν τρέξει οποιοσδήποτε κώδικας, χρειάζεστε τη βιβλιοθήκη. Το Aspose OCR διανέμεται ως pure‑Python wheel, οπότε μια εντολή `pip` κάνει τη δουλειά.

```bash
pip install aspose-ocr
```

Τώρα εισάγουμε το module. Η γραμμή εισαγωγής μπορεί να φαίνεται παράξενη (`aspose.ocr as aocr`) αλλά κρατά το namespace καθαρό.

```python
# Step 1: Import the Aspose OCR module
import aspose.ocr as aocr
```

*Γιατί είναι σημαντικό:* Η εισαγωγή του `aspose.ocr` σας δίνει πρόσβαση στο `OcrEngine`, την κεντρική κλάση που διαχειρίζεται τα πάντα—from loading files to returning structured results.

## Βήμα 2 – Δημιουργία του Αντικειμένου OCR Engine

Ένα αντικείμενο `OcrEngine` περιλαμβάνει ρυθμίσεις όπως γλώσσα, mode αναγνώρισης, και παραμέτρους απόδοσης. Στις περισσότερες περιπτώσεις οι προεπιλογές λειτουργούν καλά, αλλά μπορείτε να τις τροποποιήσετε αργότερα.

```python
# Step 2: Create an OCR engine instance
ocr_engine = aocr.OcrEngine()
```

> **Pro tip:** Αν ξέρετε ότι το PDF περιέχει μόνο αγγλικό κείμενο, ορίστε `ocr_engine.language = aocr.Language.English` για να επιταχύνετε τη διαδικασία.

## Βήμα 3 – Φόρτωση PDF για OCR

Τώρα **φορτώνουμε PDF για OCR**. Η μέθοδος `load_image` δέχεται πολλές μορφές—PDF, JPG, PNG, TIFF—οπότε μπορείτε να επαναχρησιμοποιήσετε τον ίδιο κώδικα για άλλες πηγές.

```python
# Step 3: Load the document you want to process
ocr_engine.load_image("YOUR_DIRECTORY/input.pdf")
```

*Τι συμβαίνει “κάτω από το καπό”;* Το Aspose αναλύει κάθε σελίδα σε raster images, τα οποία η μηχανή OCR μεταχειρίζεται όπως κανονικές εικόνες. Γι' αυτό μπορείτε να δώσετε απευθείας ένα πολυ‑σελίδες PDF· η μηχανή θα το επεξεργαστεί εσωτερικά.

## Βήμα 4 – Εκτέλεση Δομημένης Αναγνώρισης

Η δομημένη αναγνώριση επιστρέφει ένα αντικείμενο `OcrResult` που διατηρεί την ιεραρχία διάταξης (pages → blocks → lines → words). Αυτό είναι πολύ πιο πλούσιο από την απλή έξοδο κειμένου.

```python
# Step 4: Perform structured recognition to obtain detailed results
ocr_result = ocr_engine.recognize_structured()   # returns an OcrResult object
```

Αν χρειάζεστε μόνο ακατέργαστο κείμενο, μπορείτε να καλέσετε `ocr_engine.recognize()` αντί αυτού, αλλά θα χάσετε τα σκορ εμπιστοσύνης και τα δεδομένα θέσης—πληροφορίες που συχνά είναι κρίσιμες για pipelines επικύρωσης.

## Βήμα 5 – Εξαγωγή Λέξεων και Βαθμών Εμπιστοσύνης

Εδώ είναι η καρδιά του **πώς να εξάγετε κείμενο από PDF** ενώ παίρνετε και τις τιμές εμπιστοσύνης. Οι ένθετοι βρόχοι διασχίζουν την ιεραρχία και συλλέγουν πλειάδες `(word, confidence)`.

```python
# Step 5: Extract recognized words and their confidence scores
recognized_words = []
for page in ocr_result.structured_text.pages:
    for block in page.blocks:
        for line in block.lines:
            for word in line.words:
                recognized_words.append((word.text, word.confidence))
```

*Γιατί να βρόχο αυτόν τον τρόπο;* Κάθε επίπεδο (page → block → line → word) σας δίνει συμφραζόμενα. Για παράδειγμα, μπορείτε αργότερα να ομαδοποιήσετε λέξεις ξανά σε προτάσεις ή να αγνοήσετε λέξεις από ένα block κεφαλίδας που τυπικά έχει χαμηλότερη εμπιστοσύνη.

### Διαχείριση Ακραίων Περιστατικών

- **Κενά PDFs:** Αν `ocr_result.structured_text.pages` είναι κενό, το `recognized_words` παραμένει κενό—χειριστείτε το με χάρη.
- **Χαμηλή εμπιστοσύνη:** Μπορεί να θέλετε να φιλτράρετε λέξεις με `confidence < 0.6`. Παράδειγμα:

```python
high_confidence = [(t, c) for t, c in recognized_words if c >= 0.6]
```

## Βήμα 6 – Εμφάνιση Δείγματος Λέξης με την Εμπιστοσύνη της

Μια γρήγορη δοκιμή είναι να τυπώσετε την πρώτη λέξη και την εμπιστοσύνη της. Αυτό επιβεβαιώνει ότι η μηχανή διάβασε κάτι.

```python
# Step 6: Show a sample word with its confidence
if recognized_words:
    sample_text, sample_conf = recognized_words[0]
    print(f"{sample_text} (conf: {sample_conf:.2f})")
```

Η τυπική έξοδος φαίνεται ως εξής:

```
Invoice (conf: 0.98)
```

Αν δείτε εμπιστοσύνη κάτω από 0.5, σκεφτείτε να προεπεξεργαστείτε την εικόνα (π.χ., διόρθωση κλίσης) πριν το OCR.

## Βήμα 7 – Σύνοψη του Συνολικού Αριθμού Αναγνωρισμένων Λέξεων

Τέλος, δώστε στον χρήστη μια γρήγορη σύνοψη. Αυτό είναι χρήσιμο για logging ή UI feedback.

```python
# Step 7: Summarize the total number of words recognized
print(f"Total words recognized: {len(recognized_words)}")
```

Δείγμα εξόδου κονσόλας:

```
Total words recognized: 1,342
```

## Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι το πλήρες script που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα αρχείο με όνομα `extract_ocr.py`. Αντικαταστήστε `"YOUR_DIRECTORY/input.pdf"` με τη διαδρομή του PDF σας.

```python
# extract_ocr.py – Complete example to extract text from PDF with OCR

import aspose.ocr as aocr

def extract_words(pdf_path):
    # Initialize OCR engine
    ocr_engine = aocr.OcrEngine()
    
    # Load PDF (this is the step where we **load PDF for OCR**)
    ocr_engine.load_image(pdf_path)
    
    # Run structured recognition
    ocr_result = ocr_engine.recognize_structured()
    
    # Collect words + confidence
    words = []
    for page in ocr_result.structured_text.pages:
        for block in page.blocks:
            for line in block.lines:
                for word in line.words:
                    words.append((word.text, word.confidence))
    return words

if __name__ == "__main__":
    pdf_file = "YOUR_DIRECTORY/input.pdf"
    recognized = extract_words(pdf_file)
    
    # Show first word as a quick sanity check
    if recognized:
        txt, conf = recognized[0]
        print(f"{txt} (conf: {conf:.2f})")
    
    # Summary
    print(f"Total words recognized: {len(recognized)}")
```

Η εκτέλεση αυτού του script τυπώνει μια δείγμα λέξης με την εμπιστοσύνη της και τον συνολικό αριθμό—ακριβώς ό,τι χρειάζεστε για να επαληθεύσετε ότι **read PDF with OCR** λειτούργησε όπως αναμενόταν.

## Συχνές Ερωτήσεις & Προβλήματα

| Ερώτηση | Απάντηση |
|----------|--------|
| *Τι γίνεται αν το PDF μου είναι προστατευμένο με κωδικό;* | Καλέστε `ocr_engine.load_image("file.pdf", password="secret")`. Η μηχανή θα αποκρυπτογραφήσει πριν το rasterize. |
| *Μπορώ να επεξεργαστώ πολλά PDFs σε batch;* | Απολύτως. Τυλίξτε την κλήση `extract_words` σε έναν βρόχο πάνω σε μια λίστα διαδρομών αρχείων. |
| *Πρέπει να εγκαταστήσω επιπλέον language packs;* | Για PDFs που δεν είναι αγγλικά, εγκαταστήστε το αντίστοιχο language pack (`pip install aspose-ocr‑lang‑<lang>`). |
| *Πώς βελτιώνω σκορ χαμηλής εμπιστοσύνης;* | Προεπεξεργαστείτε τις σελίδες PDF (αυξήστε DPI, εφαρμόστε binarization) πριν τη φόρτωση, ή ενεργοποιήστε `ocr_engine.image_preprocessing = True`. |

## Επόμενα Βήματα – Πέρα από τη Βασική Εξαγωγή

Τώρα που ξέρετε **πώς να εξάγετε κείμενο από PDF** με σκορ εμπιστοσύνης, μπορείτε να εξερευνήσετε:

- **Indexing** των λέξεων σε Elasticsearch για full‑text αναζήτηση.  
- **Exporting** της δομημένης ιεραρχίας σε JSON για downstream analytics.  
- **Combining** το Aspose OCR με εργαλεία PDF‑to‑image για ακριβή ρύθμιση DPI.  
- **Integrating** το pipeline σε endpoint Flask ή FastAPI για παροχή OCR ως υπηρεσία.

Κάθε μία από αυτές τις επεκτάσεις βασίζεται στον ίδιο πυρήνα κώδικα που καλύψαμε, ώστε να μπορείτε να προχωρήσετε γρήγορα.

### Συμπέρασμα

Διασχίσαμε μια πλήρη, end‑to‑end λύση που σας επιτρέπει να **εξάγετε κείμενο από PDF** χρησιμοποιώντας το Aspose OCR σε Python. Φορτώνοντας το PDF για OCR, εκτελώντας δομημένη αναγνώριση, και διασχίζοντας σελίδες, blocks, lines και words, λαμβάνετε όχι μόνο το ακατέργαστο κείμενο αλλά και την εμπιστοσύνη ανά λέξη—κρίσιμη για ποιοτικό έλεγχο.  

Αισθανθείτε ελεύθεροι να τροποποιήσετε το script, να προσθέσετε προεπεξεργασία, ή να το ενσωματώσετε σε μεγαλύτερο workflow επεξεργασίας εγγράφων. Αν συναντήσετε δυσκολίες, αφήστε ένα σχόλιο παρακάτω· καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}