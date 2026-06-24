---
category: general
date: 2026-06-22
description: Εκπαιδευτικό σε Python για batch OCR που δείχνει πώς να εκτελείτε πολυνηματικό
  OCR σε φάκελο PNG εικόνων χρησιμοποιώντας Tesseract και pathlib. Μάθετε γρήγορο
  batch OCR εικόνων σε Python.
draft: false
keywords:
- python batch ocr tutorial
- multithreaded OCR in Python
- tesseract OCR batch processing
- pathlib image handling
- OCR thread count optimization
language: el
og_description: Το tutorial python batch OCR σας καθοδηγεί μέσα από ένα πλήρες, εκτελέσιμο
  script που επεξεργάζεται πολλά PNG με το Tesseract χρησιμοποιώντας πολλαπλά νήματα.
og_title: Οδηγός batch OCR σε Python – Γρήγορο πολυνηματικό OCR για εικόνες PNG
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: python batch ocr tutorial showing how to run multithreaded OCR on a
    folder of PNG images using Tesseract and pathlib. Learn fast batch image OCR in
    Python.
  headline: 'python batch ocr tutorial: Process Multiple PNGs Efficiently'
  type: TechArticle
- description: python batch ocr tutorial showing how to run multithreaded OCR on a
    folder of PNG images using Tesseract and pathlib. Learn fast batch image OCR in
    Python.
  name: 'python batch ocr tutorial: Process Multiple PNGs Efficiently'
  steps:
  - name: '**Collects** every PNG with **pathlib image handling**.'
    text: '**Collects** every PNG with **pathlib image handling**.'
  - name: '**Spins up** a **multithreaded OCR in Python** worker pool.'
    text: '**Spins up** a **multithreaded OCR in Python** worker pool.'
  - name: '**Optimizes** the number of threads for your hardware (**OCR thread count
      optimization**).'
    text: '**Optimizes** the number of threads for your hardware (**OCR thread count
      optimization**).'
  - name: '**Writes** each result to a dedicated folder (**tesseract OCR batch processing**).'
    text: '**Writes** each result to a dedicated folder (**tesseract OCR batch processing**).'
  type: HowTo
tags:
- OCR
- Python
- Batch Processing
title: 'Οδηγός batch OCR σε Python: Επεξεργασία πολλαπλών PNG αποδοτικά'
url: /el/python-java/general/python-batch-ocr-tutorial-process-multiple-pngs-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# python batch ocr tutorial – Γρήγορο Πολυνηματικό OCR για PNG Εικόνες

Έχετε αναρωτηθεί ποτέ πώς να **python batch ocr tutorial** μέσα από εκατοντάδες PNG στιγμιότυπα χωρίς να βλέπετε τον CPU σας να λιώνει; Δεν είστε ο μόνος. Είτε ψηφιοποιείτε σαρωμένες φόρμες, εξάγετε κείμενο από αποδείξεις, είτε δημιουργείτε ένα αναζητήσιμο αρχείο, μια αξιόπιστη παρτίδα OCR εξοικονομεί ώρες.

Σε αυτόν τον οδηγό θα δημιουργήσουμε ένα μικρό αλλά ισχυρό script που συλλέγει κάθε `*.png` σε έναν φάκελο, τα παραδίδει στο Tesseract μέσω ενός πολυνηματικού επεξεργαστή, και αποθηκεύει τα αποτελέσματα plain‑text σε έναν τακτοποιημένο φάκελο εξόδου. Χωρίς μυστικές βιβλιοθήκες—μόνο `pathlib`, `concurrent.futures` και το πάντα αξιόπιστο `pytesseract`. Στο τέλος θα έχετε ένα **python batch ocr tutorial** που μπορείτε να αντιγράψετε‑επικολλήσετε σε οποιοδήποτε έργο.

## Τι Θα Μάθετε

- Πώς να συλλέγετε αρχεία εικόνας με **pathlib image handling**  
- Ρύθμιση μιας **multithreaded OCR in Python** ομάδας εργασίας  
- Ρύθμιση **OCR thread count optimization** για τους πυρήνες του CPU σας  
- Αποθήκευση κάθε αποτελέσματος με ένα σαφές σύστημα ονοματοδοσίας για μελλοντική αναζήτηση  
- Εκτέλεση όλου του ως ένα ενιαίο, αυτόνομο script  

## Προαπαιτούμενα (Τι Χρειάζεστε Πρώτα)

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|------------------------|
| Python 3.9+ | Σύγχρονη σύνταξη (`pathlib`, f‑strings) |
| Tesseract 5.x installed and accessible in `PATH` | Η μηχανή OCR πίσω από το `pytesseract` |
| `pytesseract` (`pip install pytesseract`) | Python wrapper για το Tesseract |
| `Pillow` (`pip install pillow`) | Φόρτωση εικόνας για το Tesseract |
| A folder of PNG files you want to process | Ένας φάκελος PNG αρχείων που θέλετε να επεξεργαστείτε |
| Our **tesseract OCR batch processing** target | Ο στόχος μας **tesseract OCR batch processing** |

> **Pro tip:** Αν βρίσκεστε σε Windows, προσθέστε `C:\Program Files\Tesseract-OCR` στο σύστημα `PATH` ώστε το `pytesseract` να βρει το εκτελέσιμο αυτόματα.

---

## Βήμα 1 – Συλλογή Όλων των PNG Εικόνων (Χρήση pathlib)

Πρώτα απ' όλα: χρειαζόμαστε μια λίστα με κάθε εικόνα που σκοπεύουμε να τρέξουμε OCR. Το `pathlib` το κάνει αυτό με μία γραμμή και διατηρεί τον κώδικα ανεξάρτητο από το OS.

```python
import pathlib

# Adjust the path to point at your source folder
source_dir = pathlib.Path("YOUR_DIRECTORY/batch_images")
image_files = list(source_dir.glob("*.png"))

print(f"Found {len(image_files)} PNG files to process.")
```

*Γιατί `pathlib`?* Απομονώνει τις διαφορές μεταξύ των backslashes των Windows και των slash του Unix, επιτρέποντας στο ίδιο script να τρέχει παντού. Αυτό είναι το θεμέλιο της **pathlib image handling** στο tutorial μας.

---

## Βήμα 2 – Ορισμός Μιας Απλής Κλάσης Επεξεργαστή Batch OCR

Παρακάτω υπάρχει ένας ελαφρύς wrapper που κρύβει το boilerplate του threading. Αντιγράφει τον ψευδο‑κώδικα που είδατε νωρίτερα αλλά είναι πλήρως λειτουργικός.

```python
import concurrent.futures
import pytesseract
from PIL import Image
import os

class BatchOcrProcessor:
    """Encapsulates multithreaded OCR logic."""

    def __init__(self):
        self.thread_count = os.cpu_count() or 4  # sensible default
        self.output_folder = pathlib.Path("ocr_results")
        self.output_folder.mkdir(parents=True, exist_ok=True)

    def set_thread_count(self, count: int):
        """Adjust the number of worker threads (OCR thread count optimization)."""
        if count < 1:
            raise ValueError("Thread count must be at least 1")
        self.thread_count = count
        print(f"Thread pool size set to {self.thread_count}")

    def set_output_folder(self, folder: str):
        """Where each OCR result will be saved (tesseract OCR batch processing)."""
        self.output_folder = pathlib.Path(folder)
        self.output_folder.mkdir(parents=True, exist_ok=True)
        print(f"Output folder set to {self.output_folder}")

    def _process_single(self, image_path: pathlib.Path):
        """Run OCR on a single image and write the text file."""
        try:
            img = Image.open(image_path)
            text = pytesseract.image_to_string(img)
            out_file = self.output_folder / f"{image_path.stem}.txt"
            out_file.write_text(text, encoding="utf-8")
            return f"✅ {image_path.name} → {out_file.name}"
        except Exception as exc:
            return f"❌ {image_path.name} failed: {exc}"

    def process(self, image_paths):
        """Run OCR on the entire batch using a thread pool."""
        print("🚀 Starting batch OCR...")
        with concurrent.futures.ThreadPoolExecutor(max_workers=self.thread_count) as executor:
            results = list(executor.map(self._process_single, image_paths))
        for line in results:
            print(line)
        print("🏁 Batch OCR completed.")
```

**Εξήγηση των βασικών επιλογών**

- **ThreadPoolExecutor** μας παρέχει αληθινό πολυνηματισμό για εργασίες I/O‑bound όπως η ανάγνωση αρχείων και η κλήση του εξωτερικού δυαδικού Tesseract.  
- Η μέθοδος `set_thread_count` είναι το σημείο όπου μπορείτε να πειραματιστείτε με **OCR thread count optimization**· περισσότερα νήματα συχνά σημαίνουν μεγαλύτερη ταχύτητα μέχρι να κορεστούν οι πυρήνες του CPU σας.  
- Κάθε εικόνα παράγει ένα αρχείο `.txt` με όνομα το αρχικό PNG—τέλειο για μελλοντική ευρετηρίαση ή αναζήτηση.

---

## Βήμα 3 – Συνδέστε Όλα Μαζί

Τώρα δημιουργούμε ένα instance του επεξεργαστή, ρυθμίζουμε τον αριθμό των νημάτων, το κατευθύνουμε στον φάκελο εξόδου μας, και τέλος του δίνουμε τη λίστα των εικόνων.

```python
if __name__ == "__main__":
    # 1️⃣ Gather PNGs (already done above)
    # 2️⃣ Create processor instance
    ocr_processor = BatchOcrProcessor()

    # 3️⃣ Configure thread pool – feel free to change 8 → your core count
    ocr_processor.set_thread_count(8)   # multithreaded OCR in Python

    # 4️⃣ Choose where results land
    ocr_processor.set_output_folder("YOUR_DIRECTORY/ocr_results")

    # 5️⃣ Run the batch – this call blocks until everything is done
    ocr_processor.process(image_files)

    # 6️⃣ All done – a friendly console message
    print("✅ All images processed. Check the ocr_results folder.")
```

Η εκτέλεση του script θα παράγει έξοδο παρόμοια με:

```
Found 42 PNG files to process.
Thread pool size set to 8
Output folder set to YOUR_DIRECTORY/ocr_results
🚀 Starting batch OCR...
✅ invoice_001.png → invoice_001.txt
✅ receipt_2023-04-15.png → receipt_2023-04-15.txt
...
🏁 Batch OCR completed.
✅ All images processed. Check the ocr_results folder.
```

Κάθε `.txt` περιέχει το ακατέργαστο αποτέλεσμα του OCR. Ανοίξτε οποιοδήποτε αρχείο και θα δείτε το εξαγόμενο κείμενο έτοιμο για ευρετηρίαση, ανάλυση συναισθήματος ή ό,τι ακολουθεί.

---

## Βήμα 4 – Συνηθισμένα Προβλήματα & Πώς να τα Αποφύγετε

| Σύμπτωμα | Πιθανή Αιτία | Διόρθωση |
|----------|--------------|----------|
| Κενά αρχεία `.txt` | Το Tesseract δεν βρίσκει τα δεδομένα γλώσσας ή η εικόνα είναι πολύ σκοτεινή | Εγκαταστήστε τα πακέτα γλώσσας (`tesseract-ocr-eng`) και προεπεξεργαστείτε τις εικόνες (αυξήστε την αντίθεση). |
| `UnicodeDecodeError` κατά την ανάγνωση των αποτελεσμάτων | Η έξοδος περιέχει χαρακτήρες που δεν είναι UTF‑8 | Γράψτε τα αρχεία με `encoding="utf-8"` (ήδη στον κώδικα) ή χρησιμοποιήστε `errors="ignore"` για γρήγορη λύση. |
| Αιχμές CPU, χωρίς κέρδος στην ταχύτητα | Ο αριθμός νημάτων υπερβαίνει τους φυσικούς πυρήνες | Μειώστε το `set_thread_count` στο `os.cpu_count()` ή λιγότερο. |
| `FileNotFoundError` κατά το άνοιγμα της εικόνας | Η διαδρομή περιέχει μη‑ASCII χαρακτήρες στα Windows | Προσθέστε πρόθεμα `r` στη συμβολοσειρά ή χρησιμοποιήστε απευθείας αντικείμενα `pathlib` (όπως κάνουμε). |

---

## Βήμα 5 – Επέκταση του Tutorial (Επόμενα Βήματα)

- **Add image preprocessing** με OpenCV (`cv2`) για βελτίωση της ακρίβειας του OCR (π.χ., διόρθωση κλίσης, κατώφλι).  
- **Parallelize across machines** χρησιμοποιώντας `multiprocessing` ή μια απλή ουρά εργασιών όπως το RabbitMQ για τεράστιες φορτώσεις.  
- **Integrate with a search engine** (Elasticsearch) ώστε το εξαγόμενο κείμενο να είναι αναζητήσιμο σε πραγματικό χρόνο.  
- **Swap Tesseract for a cloud OCR API** (Google Vision, Azure Computer Vision) αν χρειάζεστε μεγαλύτερη ακρίβεια σε χειρόγραφο κείμενο.

Όλες αυτές οι ιδέες βασίζονται στο θεμέλιο που έχετε τώρα: ένα καθαρό, **python batch ocr tutorial** που λειτουργεί αμέσως.

---

## Συμπέρασμα

Έχετε μόλις χτίσει ένα πλήρες **python batch ocr tutorial** που:

1. **Collects** κάθε PNG με **pathlib image handling**.  
2. **Spins up** μια **multithreaded OCR in Python** ομάδα εργασίας.  
3. **Optimizes** τον αριθμό των νημάτων για το υλικό σας (**OCR thread count optimization**).  
4. **Writes** κάθε αποτέλεσμα σε έναν αφιερωμένο φάκελο (**tesseract OCR batch processing**).  

Το script είναι έτοιμο να ενσωματωθεί σε οποιοδήποτε pipeline, είτε επεξεργάζεστε αποδείξεις, νομικά έγγραφα, είτε ένα βουνό από στιγμιότυπα. Πειραματιστείτε με τον αριθμό των νημάτων, προσθέστε προεπεξεργασία εικόνας, ή συνδέστε την έξοδο με μια βάση δεδομένων—η επιλογή είναι δική σας.

Έχετε ερωτήσεις; Μη διστάσετε να σχολιάσετε παρακάτω, και καλή προγραμματιστική!

![Διάγραμμα ροής του python batch ocr tutorial που επεξεργάζεται πολλαπλά PNG αρχεία παράλληλα](/images/python-batch-ocr-workflow.png){.center width=600 alt="διαγράμματα ροής python batch ocr tutorial"}

---

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Aspose OCR Tutorial – Οπτική Αναγνώριση Χαρακτήρων](/ocr/english/)
- [Πώς να Batch OCR Εικόνες με Λίστα στο Aspose.OCR για .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}