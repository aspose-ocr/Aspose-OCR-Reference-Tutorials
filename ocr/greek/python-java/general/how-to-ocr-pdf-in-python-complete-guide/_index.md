---
category: general
date: 2026-06-16
description: Πώς να κάνετε OCR PDF με Python σε λίγα λεπτά – μάθετε να εξάγετε κείμενο
  από PDF, να εκτελείτε OCR σε PDF και να μετατρέπετε αποτελεσματικά το κείμενο σαρωμένων
  PDF.
draft: false
keywords:
- how to OCR PDF
- extract text from PDF
- run OCR on PDF
- convert scanned PDF text
- load PDF for OCR
language: el
og_description: 'Πώς να κάνετε OCR PDF με Python: βήμα‑βήμα οδηγίες για την εξαγωγή
  κειμένου από PDF, την εκτέλεση OCR σε PDF και τη μετατροπή του κειμένου σκαναρισμένου
  PDF.'
og_title: Πώς να κάνετε OCR PDF σε Python – Πλήρης Οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to OCR PDF using Python in minutes – learn to extract text from
    PDF, run OCR on PDF, and convert scanned PDF text efficiently.
  headline: How to OCR PDF in Python – Complete Guide
  type: TechArticle
- description: How to OCR PDF using Python in minutes – learn to extract text from
    PDF, run OCR on PDF, and convert scanned PDF text efficiently.
  name: How to OCR PDF in Python – Complete Guide
  steps:
  - name: Initialized an OCR engine.
    text: Initialized an OCR engine.
  - name: Set the language (optional but recommended).
    text: Set the language (optional but recommended).
  - name: Limited the page range to speed things up.
    text: Limited the page range to speed things up.
  - name: Loaded the PDF file.
    text: Loaded the PDF file.
  - name: Ran OCR on the document.
    text: Ran OCR on the document.
  - name: '**Extracted text from PDF** for immediate use.'
    text: '**Extracted text from PDF** for immediate use.'
  - name: Exported detailed results to **convert scanned PDF text** into JSON.
    text: Exported detailed results to **convert scanned PDF text** into JSON.
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: Πώς να κάνετε OCR PDF σε Python – Πλήρης Οδηγός
url: /el/python-java/general/how-to-ocr-pdf-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να κάνετε OCR PDF σε Python – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να κάνετε OCR PDF** αρχεία χωρίς κόπο; Δεν είστε ο μόνος· αμέτρητοι προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν προσπαθούν να μετατρέψουν σαρωμένες σελίδες σε αναζητήσιμο κείμενο. Τα καλά νέα; Με μερικές γραμμές Python μπορείτε να φορτώσετε ένα PDF για OCR, να εκτελέσετε OCR σε σελίδες PDF και να εξάγετε καθαρά, επεξεργάσιμα strings σε δευτερόλεπτα.

Σε αυτό το tutorial θα περάσουμε από ένα πραγματικό παράδειγμα που σας δείχνει ακριβώς πώς να κάνετε OCR PDF έγγραφα, να εξάγετε κείμενο από σελίδες PDF και ακόμη να μετατρέψετε το σαρωμένο κείμενο PDF σε αποτελέσματα δομημένα σε JSON. Χωρίς περιττές πληροφορίες, μόνο ένα λειτουργικό script που μπορείτε να ενσωματώσετε στο πρόγραμμά σας σήμερα.

## Τι Θα Χρειαστεί

- Python 3.8+ (οποιαδήποτε πρόσφατη έκδοση λειτουργεί)
- Η βιβλιοθήκη `ocr` (ή ένα συμβατό wrapper – θα υποθέσουμε ένα γενικό πακέτο `ocr` που ακολουθεί το API που φαίνεται)
- Ένα πολυσελίδες σαρωμένο PDF που θέλετε να επεξεργαστείτε
- Ένα IDE ή επεξεργαστή της επιλογής σας (VS Code, PyCharm, ακόμη και ένας απλός επεξεργαστής κειμένου)

Αυτό είναι όλο. Αν τα έχετε, είστε έτοιμοι να αρχίσετε να εξάγετε κείμενο από αρχεία PDF σαν επαγγελματίας.

## Βήμα 1 – Ρύθμιση του OCR Engine (Πώς να κάνετε OCR PDF)

Πρώτα απ' όλα: δημιουργήστε μια παρουσία του OCR engine. Σκεφτείτε το engine ως τον εγκέφαλο που θα διαβάσει κάθε pixel του εγγράφου σας.

```python
# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

> **Pro tip:** Η αρχικοποίηση του engine είναι φθηνή, αλλά αν σκοπεύετε να επεξεργαστείτε δεκάδες PDF σε μια παρτίδα, επαναχρησιμοποιήστε το ίδιο αντικείμενο `engine` για να εξοικονομήσετε μνήμη.

![Διάγραμμα της ροής OCR που απεικονίζει πώς να κάνετε OCR PDF](/images/ocr-pdf-workflow.png "Ροή OCR PDF")

## Βήμα 2 – Επιλογή της σωστής γλώσσας (Εκτέλεση OCR σε PDF)

Αν οι σαρώσεις σας είναι στα Αγγλικά, ορίστε τη γλώσσα ρητά. Παραλείποντας αυτό το βήμα, το engine θα προσπαθήσει να μαντέψει, κάτι που μπορεί να είναι πιο αργό και μερικές φορές λιγότερο ακριβές.

```python
# Step 2 (optional): Set language to English
engine.language = ocr.Language.ENGLISH
```

Γιατί να το κάνετε; Επειδή λέγοντας στο engine να **εκτελέσει OCR σε PDF** με γνωστή γλώσσα βελτιώνει δραστικά τα ποσοστά αναγνώρισης — ειδικά για έγγραφα με τεχνική ορολογία.

## Βήμα 3 – Εστίαση σε συγκεκριμένες σελίδες (Φόρτωση PDF για OCR)

Η επεξεργασία ενός τεράστιου αρχείου 500‑σελίδων μπορεί να είναι υπερβολική αν χρειάζεστε μόνο τα πρώτα κεφάλαια. Μπορείτε να περιορίσετε το εύρος σελίδων ως εξής:

```python
# Step 3 (optional): Process only pages 1‑5
engine.pdf_page_range = (1, 5)
```

Αυτή η μικρή ρύθμιση λέει στο engine να **φορτώσει PDF για OCR** αλλά να αγγίξει μόνο τις σελίδες που σας ενδιαφέρουν, εξοικονομώντας χρόνο και κύκλους CPU.

## Βήμα 4 – Φόρτωση του εγγράφου σας (Φόρτωση PDF για OCR)

Τώρα δείξτε το engine στο πραγματικό αρχείο. Βεβαιωθείτε ότι η διαδρομή είναι σωστή· διαφορετικά θα αντιμετωπίσετε `FileNotFoundError`.

```python
# Step 4: Load the multi‑page PDF file
engine.load_from_file("YOUR_DIRECTORY/multipage-document.pdf")
```

Σε αυτό το σημείο το engine έχει **φορτώσει το PDF για OCR**, έχει αναλύσει τη δομή του και είναι έτοιμο να ξεκινήσει τη βαριά δουλειά.

## Βήμα 5 – Εκκίνηση της αναγνώρισης (Εκτέλεση OCR σε PDF)

Αυτή είναι η στιγμή που συμβαίνει η μαγεία. Η κλήση `recognize()` σαρώει κάθε pixel, εφαρμόζει μοντέλα γλώσσας και επιστρέφει ένα πλούσιο αντικείμενο αποτελέσματος.

```python
# Step 5: Run OCR on the loaded document
pdf_result = engine.recognize()
```

Πίσω από τις σκηνές, το engine **εκτελεί OCR σε PDF** σελίδες, δημιουργεί στρώματα κειμένου και ακόμη διατηρεί βαθμολογίες εμπιστοσύνης για κάθε λέξη.

## Βήμα 6 – Εξαγωγή ολόκληρου του κειμένου (Εξαγωγή κειμένου από PDF)

Οι περισσότερες περιπτώσεις χρήσης χρειάζονται μόνο το απλό κείμενο. Το χαρακτηριστικό `text` σας δίνει μια ενωμένη συμβολοσειρά με ό,τι είδε το engine.

```python
# Step 6: Retrieve the combined text of the entire PDF
print("Full PDF text:\n", pdf_result.text)
```

Τώρα έχετε εξάγει επιτυχώς **κείμενο από PDF** — έτοιμο να το τροφοδοτήσετε σε ευρετήριο αναζήτησης, βάση δεδομένων ή ένα απλό `print()`.

## Βήμα 7 – Επισκόπηση λεπτομερών αποτελεσμάτων (Μετατροπή σαρωμένου κειμένου PDF)

Αν χρειάζεστε κάτι περισσότερο από ακατέργαστες συμβολοσειρές — π.χ. τα πλαίσια οριοθέτησης ή τις βαθμολογίες εμπιστοσύνης — χρησιμοποιήστε την εξαγωγή JSON. Αυτό ουσιαστικά **μετατρέπει το σαρωμένο κείμενο PDF** σε μορφή αναγνώσιμη από μηχανή.

```python
# Step 7: View detailed OCR results for each page in JSON
print(pdf_result.to_json(indent=2))
```

Το JSON περιλαμβάνει πίνακες ανά σελίδα, κάθε καταχώρηση περιέχει το αναγνωρισμένο κείμενο, τη θέση του στη σελίδα και ένα μέτρο εμπιστοσύνης. Ιδανικό για επεξεργασία downstream όπως εξαγωγή οντοτήτων ή προσαρμοσμένο επισήμανση.

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Πρόβλημα | Γιατί συμβαίνει | Γρήγορη λύση |
|----------|-----------------|--------------|
| **Αχρείαστοι χαρακτήρες** | Λάθος γλώσσα ή ελλιπείς γραμματοσειρές | Ορίστε ρητά `engine.language` στη σωστή γλώσσα. |
| **Λείπουν σελίδες** | `pdf_page_range` πολύ στενό | Ελέγξτε ξανά ότι η πλειάδα `(start, end)` ταιριάζει με το έγγραφό σας. |
| **Καθυστέρηση απόδοσης** | Μεγάλα PDF επεξεργάζονται σε μία φορά | Διαχωρίστε το PDF σε τμήματα ή επεξεργαστείτε τις σελίδες παράλληλα χρησιμοποιώντας `concurrent.futures`. |
| **Κενό αποτέλεσμα** | Λάθος διαδρομή αρχείου ή μη αναγνώσιμο PDF | Επιβεβαιώστε ότι το αρχείο υπάρχει και δεν είναι προστατευμένο με κωδικό. |

Η αντιμετώπιση αυτών των προβλημάτων νωρίς σας εξοικονομεί ώρες εντοπισμού σφαλμάτων αργότερα.

## Επέκταση του παραδείγματος

- **Batch processing:** Επανάληψη σε έναν φάκελο PDF, επαναχρησιμοποιώντας την ίδια παρουσία `engine`.
- **Custom output:** Γράψτε `pdf_result.text` σε αρχείο `.txt`, ή τροφοδοτήστε το απευθείας σε μηχανή αναζήτησης όπως το Elasticsearch.
- **Image extraction:** Ορισμένες βιβλιοθήκες OCR εκθέτουν εικόνες ανά σελίδα· μπορείτε να τις εξάγετε για οπτική επαλήθευση.

Ακολουθεί ένα μικρό απόσπασμα που δείχνει πώς μπορείτε να επεξεργαστείτε κατά παρτίδες έναν φάκελο:

```python
import pathlib, json

pdf_folder = pathlib.Path("YOUR_DIRECTORY")
for pdf_path in pdf_folder.glob("*.pdf"):
    engine.load_from_file(str(pdf_path))
    result = engine.recognize()
    (pdf_folder / f"{pdf_path.stem}.txt").write_text(result.text)
    (pdf_folder / f"{pdf_path.stem}.json").write_text(result.to_json(indent=2))
    print(f"Processed {pdf_path.name}")
```

## Ανακεφαλαίωση – Τι καλύψαμε

Ξεκινήσαμε με την ερώτηση **πώς να κάνετε OCR PDF** σε Python, μετά:

1. Αρχικοποιήσαμε ένα OCR engine.
2. Ορίσαμε τη γλώσσα (προαιρετικό αλλά συνιστάται).
3. Περιορίσαμε το εύρος σελίδων για να επιταχύνουμε.
4. Φορτώσαμε το αρχείο PDF.
5. Εκτελέσαμε OCR στο έγγραφο.
6. **Εξάγαμε κείμενο από PDF** για άμεση χρήση.
7. Εξάγαμε λεπτομερή αποτελέσματα για **μετατροπή σαρωμένου κειμένου PDF** σε JSON.

Όλα αυτά τα βήματα μαζί σας παρέχουν μια ισχυρή βάση για τη μετατροπή οποιουδήποτε σαρωμένου PDF σε αναζητήσιμο, επεξεργάσιμο περιεχόμενο.

## Επόμενα βήματα

- Δοκιμάστε διαφορετικές γλώσσες (`ocr.Language.SPANISH`, `ocr.Language.FRENCH`) για να δείτε πώς το engine διαχειρίζεται πολυγλωσσικά έγγραφα.
- Πειραματιστείτε με τη ρύθμιση `engine.dpi` αν οι σαρώσεις σας είναι χαμηλής ανάλυσης — υψηλότερο DPI μπορεί να βελτιώσει την ακρίβεια.
- Συνδυάστε το αποτέλεσμα OCR με βιβλιοθήκες επεξεργασίας φυσικής γλώσσας όπως το spaCy για αυτόματη εξαγωγή οντοτήτων, ημερομηνιών ή βασικών φράσεων.

Έχετε ερωτήσεις σχετικά με **φόρτωση PDF για OCR** ή αντιμετωπίζετε πρόβλημα κατά την **εκτέλεση OCR σε PDF**; Αφήστε ένα σχόλιο παρακάτω και θα το επιλύσουμε μαζί. Καλή προγραμματιστική, και απολαύστε τη μετατροπή αυτών των επίμονων σαρώσεων σε αναζητήσιμο χρυσό!

## Τι πρέπει να μάθετε μετά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να κάνετε OCR PDF σε .NET με Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Αναγνώριση κειμένου PDF – Λειτουργίες OCR με Aspose.OCR για Java](/ocr/english/java/ocr-operations/)
- [Μετατροπή εικόνων σε PDF C# – Αποθήκευση αποτελέσματος OCR πολλαπλών σελίδων](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}