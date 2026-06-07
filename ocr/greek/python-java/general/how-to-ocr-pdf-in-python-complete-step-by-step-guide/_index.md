---
category: general
date: 2026-06-06
description: Πώς να κάνετε OCR PDF με Python, να εξάγετε κείμενο από PDF, να μετατρέψετε
  το κείμενο σκαναρισμένου PDF και να αλλάξετε τη γλώσσα OCR με λίγες μόνο γραμμές
  κώδικα.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert scanned pdf text
- perform ocr on pdf
- change ocr language
language: el
og_description: 'Πώς να κάνετε OCR σε PDF με Python: ένας πρακτικός οδηγός που σας
  δείχνει πώς να εξάγετε κείμενο από PDF, να μετατρέψετε το κείμενο σαρωμένου PDF
  και να αλλάξετε τη γλώσσα OCR χωρίς κόπο.'
og_title: Πώς να κάνετε OCR PDF σε Python – Πλήρες Μάθημα Προγραμματισμού
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Python, extract text from PDF, convert scanned
    PDF text, and change OCR language in just a few lines of code.
  headline: How to OCR PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: Πώς να κάνετε OCR σε PDF με Python – Πλήρης Οδηγός Βήμα‑προς‑Βήμα
url: /el/python-java/general/how-to-ocr-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να κάνετε OCR PDF σε Python – Πλήρης Οδηγός Βήμα‑βήμα

Έχετε αναρωτηθεί ποτέ **πώς να κάνετε OCR PDF** χωρίς να πληρώνετε για ακριβά εργαλεία SaaS; Δεν είστε μόνοι. Είτε ψηφιοποιείτε παλιά βιβλία, εξάγετε δεδομένα από τιμολόγια, είτε χρειάζεστε απλώς αναζητήσιμο κείμενο από μια σαρωμένη αναφορά, η εξοικείωση με το PDF OCR σε Python μπορεί να σας εξοικονομήσει ώρες χειροκίνητης αντιγραφής.

Σε αυτό το tutorial θα περάσουμε από ένα σύντομο, λειτουργικό παράδειγμα που **εξάγει κείμενο από PDF**, σας δείχνει πώς να **μετατρέψετε το κείμενο σαρωμένου PDF** σε επεξεργάσιμες συμβολοσειρές, και ακόμη παρουσιάζει πώς να **αλλάξετε τη γλώσσα OCR** εάν το έγγραφό σας δεν είναι στα Αγγλικά. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο snippet που μπορείτε να ενσωματώσετε σε οποιοδήποτε project.

## Προαπαιτούμενα & Ρύθμιση

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

- Python 3.8+ εγκατεστημένο (ο κώδικας λειτουργεί σε 3.9, 3.10 και νεότερες εκδόσεις)
- Το πακέτο `ocr` που παρέχει την κλάση `OcrEngine` (μπορείτε να το εγκαταστήσετε μέσω `pip install ocr-lib` – αντικαταστήστε με το πραγματικό όνομα του πακέτου που χρησιμοποιείτε)
- Ένα αρχείο PDF που θέλετε να επεξεργαστείτε· για το demo θα χρησιμοποιήσουμε το `high_res_book.pdf` τοποθετημένο σε φάκελο που ονομάζεται `YOUR_DIRECTORY`

Αν χρησιμοποιείτε εικονικό περιβάλλον (συνιστάται έντονα), ενεργοποιήστε το πρώτα:

```bash
python -m venv .venv
source .venv/bin/activate   # on Windows: .venv\Scripts\activate
pip install ocr-lib
```

> **Pro tip:** Κρατήστε τα αρχεία PDF σας σε έναν αφιερωμένο φάκελο `data/` για να αποφύγετε προβλήματα σχετικού με διαδρομές αργότερα.

## Βήμα 1: Δημιουργία Παραδείγματος OCR Engine (How to OCR PDF – Initialization)

Το πρώτο πράγμα που πρέπει να κάνετε όταν θέλετε να **εκτελέσετε OCR σε PDF** είναι να δημιουργήσετε το engine. Σκεφτείτε το engine ως τον εγκέφαλο που θα διαβάσει κάθε σελίδα, θα ερμηνεύσει τα γλύφη και θα σας επιστρέψει απλό κείμενο.

```python
# Step 1: Create an OCR engine instance
engine = OcrEngine()
```

Γιατί είναι σημαντικό: χωρίς engine δεν έχετε πλαίσιο για ρυθμίσεις γλώσσας, επιλογές απόδοσης ή διαχείριση PDF. Το αντικείμενο `OcrEngine` κρατά όλα αυτά τα προεπιλεγμένα και σας επιτρέπει να τα τροποποιήσετε αργότερα.

## Βήμα 2: Ορισμός Γλώσσας Αναγνώρισης (Change OCR Language)

Οι περισσότερες βιβλιοθήκες OCR προεπιλογή είναι τα Αγγλικά, αλλά τι γίνεται αν το έγγραφό σας είναι στα Γαλλικά, Γερμανικά ή ακόμη και Ιαπωνικά; Η αλλαγή της γλώσσας είναι τόσο απλή όσο η κλήση του `set_recognition_language`. Αυτό ικανοποιεί την απαίτηση **change OCR language** και εξασφαλίζει μεγαλύτερη ακρίβεια.

```python
# Step 2: Set the recognition language to English (or any supported language)
engine.set_recognition_language(ocr.Language.ENGLISH)   # swap ENGLISH for FRANCAIS, etc.
```

> **Γιατί μπορεί να το χρειαστείτε:** Ένα πολύγλωσσο αρχείο συχνά περιέχει σελίδες με μεικτές γλώσσες. Η εναλλαγή γλωσσών εν κινήσει αποτρέπει την λανθασμένη αναγνώριση χαρακτήρων όπως “ß” ή “ñ”.

## Βήμα 3: Ρύθμιση Επιλογών Απόδοσης PDF (Convert Scanned PDF Text Effectively)

Κατά την επεξεργασία σαρωμένων PDF, η ανάλυση και η λειτουργία χρώματος επηρεάζουν δραστικά την ποιότητα του OCR. Η απόδοση σε 300 DPI σε κλίμακα του γκρι είναι το ιδανικό σημείο για τα περισσότερα έγγραφα—αρκετά υψηλή για να συλλάβει λεπτομέρειες, αλλά αρκετά χαμηλή για να διατηρήσει τη χρήση μνήμης σε λογικά επίπεδα.

```python
# Step 3: Configure PDF rendering options (300 DPI, grayscale)
engine.pdf_render_options() \
      .set_dpi(300) \
      .set_color_mode("grayscale")
```

Οι αλυσιδωτές κλήσεις μπορεί να φαίνονται εντυπωσιακές, αλλά είναι απλώς ένα fluent API που επιστρέφει το ίδιο αντικείμενο επιλογών κάθε φορά. Αν χρειάζεστε χρώμα (π.χ. για έγχρωμα διαγράμματα), αντικαταστήστε το `"grayscale"` με `"color"`.

## Βήμα 4: Αναγνώριση του PDF και Λήψη Κειμένου Πρώτης Σελίδας (Extract Text from PDF)

Τώρα έρχεται η ουσία του **πώς να κάνετε OCR PDF**: περάστε στο engine τη διαδρομή του αρχείου και εξάγετε το αναγνωρισμένο κείμενο. Η μέθοδος επιστρέφει μια λίστα αποτελεσμάτων ανά σελίδα· κάθε αποτέλεσμα περιέχει ένα χαρακτηριστικό `text`.

```python
# Step 4: Recognize the PDF and print the text of the first page
results = engine.recognize_pdf("YOUR_DIRECTORY/high_res_book.pdf")
print(results[0].text)   # Text from the first page
```

Αν χρειάζεστε ολόκληρο το έγγραφο, επαναλάβετε πάνω στο `results`:

```python
for i, page in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(page.text)
```

### Τι γίνεται αν το PDF είναι κρυπτογραφημένο;

Ορισμένα PDF είναι προστατευμένα με κωδικό. Σε αυτήν την περίπτωση μπορείτε να περάσετε τον κωδικό στο `recognize_pdf`:

```python
results = engine.recognize_pdf(
    "YOUR_DIRECTORY/secure_doc.pdf",
    password="mySecret123"
)
```

Το engine θα το αποκρυπτογραφήσει εν κινήσει πριν εκτελέσει το OCR—χωρίς επιπλέον βήματα.

## Βήμα 5: Μετα-επεξεργασία του Εξαγόμενου Κειμένου (Fine‑Tuning Extract Text from PDF)

Η ακατέργαστη έξοδος OCR συχνά περιέχει αλλαγές γραμμής, επιπλέον κενά ή περιστασιακούς λανθασμένους χαρακτήρες. Μια γρήγορη διαδικασία καθαρισμού κάνει τη συμβολοσειρά έτοιμη για επόμενη επεξεργασία (ευρετήριο αναζήτησης, αποθήκευση σε βάση δεδομένων κ.λπ.).

```python
import re

def clean_ocr_text(raw: str) -> str:
    # Remove multiple spaces and line breaks
    text = re.sub(r'\s+', ' ', raw)
    # Strip leading/trailing whitespace
    return text.strip()

clean_text = clean_ocr_text(results[0].text)
print(clean_text)
```

Τώρα μπορείτε με ασφάλεια να **εξάγετε κείμενο από PDF** και να το περάσετε σε οποιοδήποτε pipeline NLP, μηχανή αναζήτησης ή απλή λειτουργία `open(...).write()`.

## Bonus: Επεξεργασία Πολλαπλών PDF σε Batch (Scaling Perform OCR on PDF)

Αν έχετε έναν φάκελο γεμάτο σαρωμένα PDF, τυλίξτε τη λογική σε βρόχο:

```python
import pathlib

pdf_folder = pathlib.Path("YOUR_DIRECTORY")
for pdf_path in pdf_folder.glob("*.pdf"):
    print(f"Processing {pdf_path.name} …")
    pages = engine.recognize_pdf(str(pdf_path))
    full_text = "\n".join(page.text for page in pages)
    cleaned = clean_ocr_text(full_text)

    # Save the extracted text alongside the PDF
    txt_path = pdf_path.with_suffix(".txt")
    txt_path.write_text(cleaned, encoding="utf-8")
    print(f"Saved extracted text to {txt_path.name}")
```

Αυτό το snippet δείχνει πώς να **εκτελέσετε OCR σε PDF** αρχεία μαζικά, μια κοινή ανάγκη για έργα ψηφιοποίησης.

## Αναμενόμενο Αποτέλεσμα

Η εκτέλεση του παραδείγματος μίας σελίδας (Βήμα 4) θα πρέπει να εκτυπώσει κάτι σαν:

```
In the beginning God created the heavens and the earth. Now the earth was formless …
```

Αν επεξεργαστείτε ένα βιβλίο πολλαπλών σελίδων, η κονσόλα θα εμφανίσει το καθαρισμένο κείμενο κάθε σελίδας, και το batch script θα δημιουργήσει ένα αρχείο `.txt` δίπλα σε κάθε PDF.

## Συχνά Προβλήματα & Πώς να τα Αποφύγετε

| Πρόβλημα | Συμπτώματα | Διόρθωση |
|----------|------------|----------|
| PDF πηγής χαμηλής ανάλυσης | Παραμορφωμένοι χαρακτήρες, λείπουν λέξεις | Αυξήστε το DPI (`set_dpi(400)` ή περισσότερο) |
| Λάθος γλώσσα ορισμένη | Πολλά άγνωστα σύμβολα, ειδικά τονισμένα γράμματα | Χρησιμοποιήστε `engine.set_recognition_language(ocr.Language.FRENCH)` ή το αντίστοιχο enum |
| Μεγάλο PDF που προκαλεί σφάλμα μνήμης | `MemoryError` ή κατάρρευση μετά από λίγες σελίδες | Επεξεργαστείτε τις σελίδες σε τμήματα (`engine.recognize_pdf(..., max_pages=10)`) |
| Λείπουν γραμματοσειρές στο PDF | Κενό αποτέλεσμα για ορισμένες σελίδες | Βεβαιωθείτε ότι το PDF περιέχει πραγματικές ραστερ εικόνες· κάποια PDF είναι μόνο διανυσματικά και απαιτούν διαφορετική προσέγγιση |

## Εικονογραφική Παράσταση

Παρακάτω υπάρχει μια γρήγορη οπτική αναπαράσταση της ροής εργασίας. Το alt text είναι σκόπιμα φιλικό προς SEO.

![διαγράφημα ροής ocr pdf που δείχνει την αρχικοποίηση του engine, τη ρύθμιση γλώσσας, τις επιλογές απόδοσης, την αναγνώριση και την εξαγωγή κειμένου](/images/ocr-workflow.png)

*Το διάγραμμα δεν είναι απαραίτητο για την εκτέλεση του κώδικα, αλλά βοηθά τους οπτικούς μαθητές να καταλάβουν πού εντάσσεται κάθε βήμα.*

## Συμπέρασμα

Καλύψαμε **πώς να κάνετε OCR PDF** σε Python από την αρχή μέχρι το τέλος: δημιουργία OCR engine, **αλλαγή γλώσσας OCR**, ρύθμιση απόδοσης για **μετατροπή κειμένου σαρωμένου PDF**, και τέλος **εξαγωγή κειμένου από PDF** για περαιτέρω χρήση. Το πλήρες, εκτελέσιμο παράδειγμα είναι έτοιμο να ενσωματωθεί σε οποιοδήποτε project, και το προαιρετικό batch script δείχνει πώς να κλιμακώσετε τη λύση.

Επόμενα βήματα που ίσως θέλετε να εξερευνήσετε:

- Προσθήκη **perform OCR on PDF** για πολύγλωσσα αρχεία επαναλαμβάνοντας πάνω σε λίστα γλωσσών.
- Ενσωμάτωση του εξαγόμενου κειμένου με Elasticsearch για πλήρη αναζήτηση κειμένου.
- Χρήση OCR για δημιουργία αναζητήσιμων PDF ενσωματώνοντας το επίπεδο κειμένου πίσω στο αρχικό αρχείο (πολλές βιβλιοθήκες παρέχουν μέθοδο `save_as_searchable_pdf`).

Νιώστε ελεύθεροι να πειραματιστείτε, να τροποποιήσετε τις ρυθμίσεις DPI ή να αλλάξετε σε διαφορετικό backend OCR. Τα θεμέλια παραμένουν ίδια, και τώρα έχετε μια ισχυρή βάση για να χτίσετε πάνω της.

Καλός κώδικας και καλή επιτυχία με την αναζήτηση κειμένου στα σαρωμένα έγγραφά σας!

## Τι Πρέπει να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας projects.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}