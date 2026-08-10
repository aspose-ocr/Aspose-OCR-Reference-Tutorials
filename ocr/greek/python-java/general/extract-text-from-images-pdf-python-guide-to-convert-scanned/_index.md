---
category: general
date: 2026-06-06
description: Εξάγετε κείμενο από εικόνες PDF χρησιμοποιώντας Python OCR. Μάθετε πώς
  να μετατρέπετε σαρωμένα έγγραφα σε κείμενο γρήγορα με ασύγχρονη ομαδική αναγνώριση.
draft: false
keywords:
- extract text from images pdf
- convert scanned documents to text
- python ocr batch processing
- asynchronous OCR python
- image to text conversion
language: el
og_description: Εξάγετε κείμενο από εικόνες PDF με Python. Αυτός ο οδηγός βήμα‑βήμα
  δείχνει πώς να μετατρέψετε σαρωμένα έγγραφα σε κείμενο χρησιμοποιώντας ασύγχρονη
  OCR.
og_title: Εξαγωγή κειμένου από εικόνες PDF – Python OCR Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from images pdf using Python OCR. Learn how to convert
    scanned documents to text quickly with async batch recognition.
  headline: Extract Text from Images PDF – Python Guide to Convert Scanned Documents
    to Text
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Εξαγωγή κειμένου από εικόνες PDF – Οδηγός Python για τη μετατροπή σαρωμένων
  εγγράφων σε κείμενο
url: /el/python-java/general/extract-text-from-images-pdf-python-guide-to-convert-scanned/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από PDF Εικόνων – Οδηγός Python για τη Μετατροπή Σαρωμένων Εγγράφων σε Κείμενο

Έχετε ποτέ χρειαστεί να **εξάγετε κείμενο από pdf εικόνων** χωρίς να ξοδεύετε ώρες ξαναπληκτρολόγηση; Σε αυτόν τον οδηγό θα σας δείξουμε πώς να **μετατρέψετε σαρωμένα έγγραφα σε κείμενο** χρησιμοποιώντας μια απλή ασύγχρονη ροή εργασίας OCR σε Python.  

Αν έχετε ποτέ κολλήσει μπροστά σε ένα σωρό σαρωμένων PDF και σκεφτείτε, “Πρέπει να υπάρχει πιο γρήγορος τρόπος,” βρίσκεστε στο σωστό μέρος. Θα περάσουμε από κάθε γραμμή κώδικα, θα εξηγήσουμε γιατί κάθε κομμάτι είναι σημαντικό και θα καλύψουμε μερικές περιπτώσεις που μπορεί να συναντήσετε.

## Τι Θα Μάθετε

- Πώς να δημιουργήσετε μια μηχανή OCR και να ορίσετε τη γλώσσα αναγνώρισης.  
- Τους μηχανισμούς τροφοδοσίας μιας μικτής λίστας PNG και PDF σε έναν batch recognizer.  
- Την εκτέλεση της εργασίας OCR ασύγχρονα ώστε η εφαρμογή σας να παραμένει ανταποκρινόμενη.  
- Την ανάκτηση των αποτελεσμάτων, τη συσχέτισή τους με τα αρχικά αρχεία και την εκτύπωση καθαρού αποτελέσματος.  

**Προαπαιτούμενα**: Python 3.8+, βασική κατανόηση του `asyncio` ή του `concurrent.futures`, και μια βιβλιοθήκη OCR που εκθέτει μια κλάση `OcrEngine` παρόμοια με το παράδειγμα (π.χ., Aspose.OCR, περιτύλιγμα Tesseract, ή προσαρμοσμένο wrapper). Δεν απαιτείται βαριά εγκατάσταση—απλώς εγκαταστήστε τη βιβλιοθήκη και είστε έτοιμοι.

![εξαγωγή κειμένου από pdf εικόνων](https://example.com/placeholder.png "Στιγμιότυπο εξόδου OCR – εξαγωγή κειμένου από pdf εικόνων")

## Εξαγωγή Κειμένου από PDF Εικόνων – Ρύθμιση της Μηχανής OCR

Το πρώτο που χρειάζεστε είναι μια παρουσία της μηχανής OCR ρυθμισμένη για τη γλώσσα των εγγράφων σας. Στην περίπτωση μας θα χρησιμοποιήσουμε τα Γαλλικά, αλλά μπορείτε να την αλλάξετε σε οποιαδήποτε υποστηριζόμενη γλώσσα.

```python
# Import the OCR library – replace with your actual import
from ocr import OcrEngine, Language

# Step 1: Create and configure the OCR engine
engine = OcrEngine()
engine.set_recognition_language(Language.FRENCH)   # Change to Language.ENGLISH, etc.
```

**Γιατί αυτό είναι σημαντικό**: Η προ-ρύθμιση της γλώσσας βελτιώνει δραστικά την ακρίβεια. Η μηχανή χρησιμοποιεί λεξικά και μοντέλα χαρακτήρων ειδικά για τη γλώσσα· η τροφοδοσία με λανθασμένη γλώσσα είναι κοινή πηγή ακατανόητης εξόδου.

## Προετοιμασία Λίστας Αρχείων – Εικόνες και PDF Μαζί

Ο batch recognizer μας μπορεί να διαχειριστεί τόσο raster εικόνες (`.png`, `.jpg`) όσο και PDF containers. Απλώς δώστε μια απλή λίστα Python με διαδρομές αρχείων.

```python
# Step 2: Define the files to be processed (use your own directory)
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.pdf"
]
```

**Συμβουλή**: Κρατήστε τη λίστα επίπεδη· η μηχανή θα αποσυμπιέσει εσωτερικά κάθε σελίδα PDF σε εικόνες πριν την αναγνώριση. Αν έχετε χιλιάδες αρχεία, σκεφτείτε να χωρίσετε τη λίστα σε μικρότερα batch για να αποφύγετε αυξήσεις μνήμης.

## Εκκίνηση Ασύγχρονης Batch Αναγνώρισης

Αντί να μπλοκάρετε το κύριο νήμα, εκκινούμε την εργασία OCR στο παρασκήνιο. Η μέθοδος επιστρέφει ένα `Future` που τελικά θα περιέχει μια λίστα αντικειμένων `OcrResult`.

```python
# Step 3: Start asynchronous batch recognition
future = engine.recognize_batch_async(files)   # returns a Future[List[OcrResult]]
```

**Πώς λειτουργεί**: Στο παρασκήνιο η μηχανή δημιουργεί μια ομάδα νημάτων (ή μια ασύγχρονη εργασία, ανάλογα με την υλοποίηση). Αυτό σας επιτρέπει να συνεχίσετε άλλες εργασίες—όπως ενημέρωση UI, λήψη περισσότερων αρχείων ή καταγραφή προόδου—ενώ η βαριά επεξεργασία γίνεται αλλού.

## Κάντε Κάτι Χρήσιμο Καθώς Εκτελείται το OCR

Ένα κοινό λάθος είναι να μένετε αδρανείς και να ελέγχετε το future σε σφιχτό βρόχο. Αντί αυτού, μπορείτε να εκτελείτε οποιαδήποτε ανεξάρτητη εργασία. Για επίδειξη, θα εκτυπώσουμε μια γραμμή κατάστασης.

```python
# Step 4: Perform other work while OCR runs
print("Batch started – doing other work...")
# Imagine you could be uploading files, sending heartbeats, etc.
```

## Συλλογή Αποτελεσμάτων Μόλις Το Future Ολοκληρωθεί

Όταν είστε έτοιμοι να συγκεντρώσετε την έξοδο OCR, χρησιμοποιήστε `as_completed` από το `concurrent.futures`. Αυτό το μοτίβο λειτουργεί είτε έχετε ένα είτε πολλά futures.

```python
from concurrent.futures import as_completed

# Step 5: Wait for the batch to finish and retrieve the results
for completed in as_completed([future]):
    ocr_results = completed.result()   # List[OcrResult] in the same order as `files`
    for path, result in zip(files, ocr_results):
        print(f"{path} →\n{result.text}\n")
```

**Τι θα δείτε**: Κάθε διαδρομή αρχείου ακολουθείται από την εξαγόμενη αναπαράσταση plain‑text. Για PDF, το `result.text` περιέχει το ενωμένο κείμενο όλων των σελίδων.

### Αναμενόμενη Έξοδος (παράδειγμα)

```
YOUR_DIRECTORY/doc1.png →
Bonjour, ceci est un test d’OCR.

YOUR_DIRECTORY/doc2.png →
Le texte de la deuxième image apparaît ici.

YOUR_DIRECTORY/doc3.pdf →
Page 1 du PDF : Lorem ipsum dolor sit amet…
Page 2 du PDF : Consectetur adipiscing elit…
```

Αν παρατηρήσετε ελλιπή χαρακτήρες, ελέγξτε ξανά ότι η γλώσσα που ορίσατε ταιριάζει με τη γλώσσα του εγγράφου, και σκεφτείτε προ‑επεξεργασία των εικόνων (ευθυγράμμιση, αύξηση αντίθεσης) πριν τις τροφοδοτήσετε στη μηχανή.

## Διαχείριση Περιπτώσεων Άκρων και Συνηθισμένων Παγίδων

| Κατάσταση | Τι να κάνετε |
|-----------|--------------|
| **Μικτές γλώσσες** | Εκτελέστε πρώτα μια φάση ανίχνευσης γλώσσας, έπειτα δημιουργήστε ξεχωριστές μηχανές ανά γλώσσα. |
| **Μεγάλα PDF (> 100 MB)** | Χωρίστε το PDF σε μεμονωμένες σελίδες στο δίσκο (π.χ., με `PyPDF2`) και τροφοδοτήστε τις ως ξεχωριστές καταχωρήσεις. |
| **Μη‑λατινικά scripts** | Βεβαιωθείτε ότι η βιβλιοθήκη OCR περιλαμβάνει το απαιτούμενο language pack· ορισμένες βιβλιοθήκες απαιτούν λήψη επιπλέον αρχείων δεδομένων. |
| **Προβλήματα απόδοσης** | Αυξήστε το μέγεθος του thread pool (`engine.set_thread_pool_size(8)`) ή μεταβείτε σε backend επιταχυμένο από GPU αν είναι διαθέσιμο. |
| **Απουσία κειμένου σε εικόνες χαμηλής ανάλυσης** | Προ‑επεξεργαστείτε με OpenCV: `cv2.resize`, `cv2.threshold`, και `cv2.medianBlur` για βελτίωση της αναγνωσιμότητας. |

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

```python
# ------------------------------------------------------------
# Full script: extract text from images pdf – async OCR batch
# ------------------------------------------------------------
import os
from concurrent.futures import as_completed
# Replace the import below with the actual OCR library you use
from ocr import OcrEngine, Language, OcrResult

def main():
    # 1️⃣ Initialize OCR engine
    engine = OcrEngine()
    engine.set_recognition_language(Language.FRENCH)   # Change as needed

    # 2️⃣ Build list of files (images + PDFs)
    base_dir = "YOUR_DIRECTORY"
    files = [
        os.path.join(base_dir, "doc1.png"),
        os.path.join(base_dir, "doc2.png"),
        os.path.join(base_dir, "doc3.pdf")
    ]

    # 3️⃣ Launch async batch recognition
    future = engine.recognize_batch_async(files)

    # 4️⃣ Do other work – here we just print a placeholder
    print("Batch started – doing other work...")

    # 5️⃣ Retrieve results when ready
    for completed in as_completed([future]):
        ocr_results = completed.result()   # List[OcrResult]
        for path, result in zip(files, ocr_results):
            print(f"{path} →\n{result.text}\n")

if __name__ == "__main__":
    main()
```

Αποθηκεύστε το ως `extract_text_async.py`, αντικαταστήστε το `YOUR_DIRECTORY` με τη διαδρομή προς τα αρχεία σας, εγκαταστήστε το πακέτο OCR (`pip install your-ocr-lib`), και τρέξτε `python extract_text_async.py`. Θα πρέπει να δείτε την έξοδο κονσόλας όπως περιγράφηκε νωρίτερα.

## Επόμενα Βήματα – Πέρα από τη Βασική Εξαγωγή

- **Post‑processing**: Αφαιρέστε περιττά κενά, κανονικοποιήστε Unicode (`unicodedata.normalize`), ή τρέξτε έναν ορθογραφικό ελεγκτή για να καθαρίσετε τον θόρυβο OCR.  
- **Structured output**: Εξάγετε τα αποτελέσματα σε CSV, JSON, ή απευθείας σε βάση δεδομένων για επόμενη αναζήτηση.  
- **Parallel batches**: Αν έχετε εκατοντάδες αρχεία, δημιουργήστε πολλαπλά futures και χρησιμοποιήστε μια ουρά για να κρατήσετε την CPU απασχολημένη χωρίς να υπερφορτώσετε τη μνήμη.  
- **Integrate with web frameworks**: Συνδέστε αυτό το script με ένα endpoint Flask ή FastAPI για να παρέχετε OCR on‑demand ως υπηρεσία.

---

### TL;DR

Τώρα ξέρετε πώς να **εξάγετε κείμενο από pdf εικόνων** με ένα ελάχιστο script Python που εκτελεί OCR ασύγχρονα, επιτρέποντάς σας να **μετατρέψετε σαρωμένα έγγραφα σε κείμενο** ενώ το πρόγραμμα σας παραμένει ανταποκρινόμενο. Παίξτε με τις ρυθμίσεις γλώσσας, τα μεγέθη batch, και τις τεχνικές προ‑επεξεργασίας για να εξάγετε την μέγιστη ακρίβεια χαρακτήρων.

Έχετε κάποιο ιδιαίτερο σενάριο που θέλετε να μοιραστείτε—ίσως OCR σε χειρόγραφες σημειώσεις ή υπηρεσία cloud; Αφήστε ένα σχόλιο, και καλή προγραμματιστική διασκέδαση!

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Βήμα‑βήμα](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Εξαγωγή Κειμένου από Εικόνες Χρησιμοποιώντας Λειτουργία OCR σε Φακέλους](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Εξαγωγή Κειμένου από Εικόνες Χρησιμοποιώντας Aspose.OCR – Επιτρεπόμενοι Χαρακτήρες](/ocr/english/java/advanced-ocr-techniques/specify-allowed-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}