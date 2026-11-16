---
category: general
date: 2026-03-18
description: Διορθώστε γρήγορα τα σφάλματα OCR στην Python. Μάθετε πώς να καθαρίζετε
  το OCR, πώς να καθαρίζετε το κείμενο OCR, να αντικαθιστάτε το μηδέν με το O και
  να εφαρμόζετε επεξεργασία μετά το OCR με Python.
draft: false
keywords:
- fix OCR errors
- how to clean OCR
- clean OCR text python
- replace zero with O
- python OCR post processing
language: el
og_description: Διορθώστε γρήγορα τα σφάλματα OCR στην Python. Μάθετε πώς να καθαρίζετε
  το OCR, να αντικαθιστάτε το μηδέν με O και να χρησιμοποιείτε την επεξεργασία OCR
  στην Python σε ένα ενιαίο σεμινάριο.
og_title: Διορθώστε τα σφάλματα OCR στην Python – Οδηγός καθαρισμού κειμένου OCR
tags:
- OCR
- Python
- Text Cleaning
title: Διορθώστε τα σφάλματα OCR στην Python – Οδηγός καθαρισμού κειμένου OCR
url: /el/python/general/fix-ocr-errors-in-python-clean-ocr-text-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Διόρθωση Σφαλμάτων OCR σε Python – Οδηγός Καθαρισμού Κειμένου OCR

Έχετε ποτέ κολλήσει σε ένα σαρωμένο τιμολόγιο και σκεφτείτε, *«Πώς διορθώνω τα σφάλματα OCR πριν το εισάγω στη βάση δεδομένων μου;»* Δεν είστε μόνοι. Στον κόσμο της αυτοματοποίησης εγγράφων, ένας μόνο λανθασμένος χαρακτήρας μπορεί να διακόψει ολόκληρη τη ροή, γι' αυτό η εκμάθηση **πώς να καθαρίζετε το OCR** είναι απαραίτητη.  

Σε αυτό το tutorial θα δείτε έναν πρακτικό, end‑to‑end τρόπο για **να διορθώσετε σφάλματα OCR** χρησιμοποιώντας έναν μικρό post‑processor που αντικαθιστά το ψηφίο “0” με το γράμμα “O” — ένα κοινό πρόβλημα σε κωδικούς προϊόντων. Στο τέλος, θα μπορείτε να ενσωματώσετε τη λύση σε οποιοδήποτε Python OCR workflow και να έχετε πιο καθαρό, αξιόπιστο κείμενο.

> **Τι θα πάρετε:** ένα πλήρες, εκτελέσιμο script Python, εξηγήσεις για το γιατί κάθε γραμμή είναι σημαντική, συμβουλές για την επέκταση της λογικής, και έναν γρήγορο έλεγχο λογικής του αναμενόμενου αποτελέσματος.

## Προαπαιτούμενα — Τι Χρειάζεστε Πριν Ξεκινήσετε

- Python 3.8 ή νεότερο (η σύνταξη λειτουργεί σε όλες τις πρόσφατες εκδόσεις).  
- Μια βασική βιβλιοθήκη OCR (π.χ., Tesseract μέσω `pytesseract`) που επιστρέφει ακατέργαστες συμβολοσειρές.  
- Ελάχιστη εξοικείωση με συναρτήσεις και αντικείμενα στην Python.  

Αν ήδη έχετε ένα βήμα OCR που παράγει μια συμβολοσειρά, είστε έτοιμοι — δεν απαιτούνται επιπλέον εγκαταστάσεις για το τμήμα post‑processing.

## Βήμα 1: Ρύθμιση ενός Ελάχιστου Wrapper Στυλ AI (Γιατί Το Χρειαζόμαστε)

Σε πολλά έργα η μηχανή OCR ζει μέσα σε μια μεγαλύτερη κλάση “AI” που διαχειρίζεται προεπεξεργασία, inference και post‑processing. Για να κρατήσουμε το παράδειγμα αυτό ανεξάρτητο, θα δημιουργήσουμε μια μικρή κλάση `AIProcessor` που μιμείται αυτό το μοτίβο. Αυτό το καθιστά εύκολο να ενσωματώσετε τον κώδικα σε υπάρχον κώδικα χωρίς να ξαναγράψετε τίποτα.

```python
# ai_wrapper.py
class AIProcessor:
    """
    Simple wrapper that stores a post‑processing callable.
    In real projects this could be a full‑fledged model class.
    """
    def __init__(self):
        self._post_processor = None

    def set_post_processor(self, func):
        """Register a function that will clean OCR output."""
        if not callable(func):
            raise TypeError("Post‑processor must be callable")
        self._post_processor = func

    def run_postprocessor(self, text):
        """Apply the registered post‑processor to raw OCR text."""
        if self._post_processor is None:
            raise RuntimeError("No post‑processor has been set")
        return self._post_processor(text)
```

**Γιατί είναι σημαντικό:** το διαχωρισμό του post‑processor από τη μηχανή OCR σέβεται την αρχή της μοναδικής ευθύνης και σας επιτρέπει να αλλάζετε τη λογική καθαρισμού χωρίς να αγγίζετε τον κώδικα OCR.

## Βήμα 2: Γράψτε τη Συνάρτηση που **Διορθώνει Σφάλματα OCR**

Τώρα δημιουργούμε την καρδιά του tutorial: μια συνάρτηση που **διορθώνει σφάλματα OCR** αντικαθιστώντας το ψηφίο “0” με το γράμμα “O”. Αυτό το μοτίβο καλύπτει κωδικούς προϊόντων, σειριακούς αριθμούς και οποιονδήποτε αλφαριθμητικό αναγνωριστικό όπου η μηχανή OCR συχνά μπερδεύει τους δύο χαρακτήρες.

```python
# post_processors.py
def correct_ocr_errors(text: str) -> str:
    """
    Replace common OCR mis‑reads.
    Example: change digit "0" to letter "O" in product codes.
    """
    # You could add more rules here, e.g.:
    # text = text.replace('1', 'I')
    # text = text.replace('5', 'S')
    return text.replace("0", "O")
```

**Γιατί αντικαθιστούμε το 0 με O:** Σε πολλές γραμματοσειρές το μηδέν και το κεφαλαίο O φαίνονται πανομοιότυπα, οπότε το OCR συχνά μπερδεύει το ένα με το άλλο. Διορθώνοντάς το νωρίς, η επακόλουθη επικύρωση (όπως έλεγχοι regex) λειτουργεί όπως πρέπει.

## Βήμα 3: Συνδέστε τον Post‑Processor με το Αντικείμενο AI

Με το wrapper και τη συνάρτηση καθαρισμού έτοιμα, τα ενώνουμε. Αυτό αντικατοπτρίζει το πώς θα καταχωρίσετε έναν προσαρμοσμένο post‑processor σε μια παραγωγική γραμμή.

```python
# main.py
from ai_wrapper import AIProcessor
from post_processors import correct_ocr_errors

# Create the AI‑like object
ai = AIProcessor()

# Register our OCR‑fixing function
ai.set_post_processor(correct_ocr_errors)
```

Αν ποτέ χρειαστείτε **πώς να καθαρίζετε OCR** για διαφορετική γλώσσα ή μορφή δεδομένων, απλώς γράψτε μια άλλη συνάρτηση και καλέστε ξανά το `set_post_processor` — χωρίς να χρειαστεί να αγγίξετε το υπόλοιπο pipeline.

## Βήμα 4: Εισάγετε Ακατέργαστο Κείμενο OCR και Λάβετε το Καθαρισμένο Αποτέλεσμα

Ας προσομοιώσουμε μια ακατέργαστη συμβολοσειρά OCR που περιέχει το ανεπιθύμητο “0” σε έναν κωδικό προϊόντος. Σε πραγματικό σενάριο θα αντικαταστήσετε το placeholder με `pytesseract.image_to_string(image)` ή παρόμοια κλήση.

```python
# Simulated OCR output (replace with your own OCR call)
raw_text = "Product code: 10A0B"

# Run the post‑processor to obtain cleaned text
cleaned_text = ai.run_postprocessor(raw_text)

print("Before cleaning :", raw_text)
print("After cleaning  :", cleaned_text)
```

**Αναμενόμενο αποτέλεσμα**

```
Before cleaning : Product code: 10A0B
After cleaning  : Product code: 1OAOB
```

Παρατηρήστε πώς τα μηδενικά έχουν μετατραπεί σε κεφαλαία O, δίνοντάς μας μια συμβολοσειρά που ταιριάζει με το αναμενόμενο φορμάτ για τις περισσότερες συστήματα αποθεμάτων.

## Βήμα 5: Επέκταση της Λογικής – Πραγματικές Παραλλαγές

Η απλή αντικατάσταση παραπάνω λύνει μια στενή περίπτωση, αλλά στην παραγωγή θα συναντήσετε και άλλα ιδιόμορφα:

| Κοινό σφάλμα | Παράδειγμα OCR | Επιθυμητή διόρθωση | Πώς να προσθέσετε |
|--------------|----------------|-------------------|-------------------|
| «1» διαβάζεται ως «I» | `I23` | `123` | `text = text.replace('I', '1')` |
| «5» διαβάζεται ως «S» | `S9` | `59` | `text = text.replace('S', '5')` |
| Πρόσθετα κενά | `  ABC  ` | `ABC` | `text = text.strip()` |
| Σύγχυση μικρών‑κεφαλαίων | `oRder` | `Order` | `text = text.title()` |

Μπορείτε να επεκτείνετε το `correct_ocr_errors` με οποιονδήποτε από αυτούς τους κανόνες. Απλώς κρατήστε κάθε μετασχηματισμό **ιδεομετρικό** (να μην αλλάζει το αποτέλεσμα αν εκτελεστεί δύο φορές) ώστε να αποφύγετε τυχαία αλλοίωση δεδομένων.

```python
def correct_ocr_errors(text: str) -> str:
    text = text.replace("0", "O")
    text = text.replace("I", "1")
    text = text.replace("S", "5")
    return text.strip()
```

**Pro tip:** Αν έχετε έναν γνωστό κατάλογο έγκυρων κωδίκων, σκεφτείτε να επικυρώνετε τη καθαρισμένη συμβολοσειρά έναντι ενός regex ή πίνακα αναζήτησης. Αυτό το επιπλέον βήμα εντοπίζει τυχόν υπόλοιπα σφάλματα OCR που δεν καλύπτονται από απλές αντικαταστάσεις χαρακτήρων.

## Βήμα 6: Ενσωμάτωση με Πραγματική Μηχανή OCR (Προαιρετικό)

Παρακάτω υπάρχει μια γρήγορη εικονογράφηση του πώς θα συνδέσετε τον post‑processor σε μια πραγματική ροή OCR χρησιμοποιώντας `pytesseract`. Αυτό το τμήμα είναι προαιρετικό αλλά δείχνει το end‑to‑end pipeline.

```python
import pytesseract
from PIL import Image
from ai_wrapper import AIProcessor
from post_processors import correct_ocr_errors

# Initialize AI wrapper and register the cleaner
ai = AIProcessor()
ai.set_post_processor(correct_ocr_errors)

# Load an image containing a product label
image = Image.open("sample_label.png")

# Perform OCR (this returns raw text)
raw_ocr = pytesseract.image_to_string(image)

# Clean the OCR output
cleaned = ai.run_postprocessor(raw_ocr)

print("Raw OCR   :", raw_ocr)
print("Cleaned   :", cleaned)
```

> **Σημείωση:** το `pytesseract` απαιτεί την εγκατάσταση του Tesseract OCR στο σύστημά σας. Το παραπάνω snippet λειτουργεί σε Windows, macOS και Linux, εφόσον το εκτελέσιμο βρίσκεται στο PATH.

## Βήμα 7: Επαλήθευση των Αποτελεσμάτων Προγραμματιστικά

Όταν αυτοματοποιείτε μεγάλες παρτίδες, είναι χρήσιμο να ελέγχετε ότι το βήμα καθαρισμού συμπεριφέρθηκε όπως αναμενόταν. Ένα γρήγορο unit test μπορεί να εξοικονομήσει ώρες debugging αργότερα.

```python
def test_correct_ocr_errors():
    assert correct_ocr_errors("0O0") == "OOO"
    assert correct_ocr_errors(" 10A0B ") == "1OAOB"
    print("All tests passed!")

test_correct_ocr_errors()
```

Η εκτέλεση αυτού του τεστ επιβεβαιώνει ότι η συνάρτηση **διορθώνει σφάλματα OCR** σταθερά, ακόμη και όταν εμφανίζονται επιπλέον κενά.

## Εικονογραφική Παράσταση

Παρακάτω υπάρχει ένα οπτικό σκίτσο του pipeline (η κύρια λέξη‑κλειδί εμφανίζεται στο alt text για SEO).

![Διάγραμμα ροής διόρθωσης σφαλμάτων OCR – δείχνει το ακατέργαστο OCR που τροφοδοτείται σε έναν post‑processor που αντικαθιστά το μηδέν με O]()

## Συμπέρασμα – Τι Καταφέραμε

Διασχίσαμε ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει **πώς να καθαρίζετε OCR** στην Python, συγκεκριμένα **πώς να αντικαθιστάτε το μηδέν με O** και **να διορθώνετε σφάλματα OCR** χρησιμοποιώντας έναν modular post‑processor. Διαχωρίζοντας τη λογική καθαρισμού από τη μηχανή OCR, κερδίζετε ευελιξία, δυνατότητα δοκιμών και ένα σαφές σημείο για προσθήκη μελλοντικών κανόνων όπως *πώς να καθαρίζετε OCR* για άλλες συγχύσεις χαρακτήρων.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να προσθέσετε έναν validator regex για κωδικούς προϊόντων, πειραματιστείτε με fuzzy matching για θορυβώδες κείμενο, ή εξερευνήστε μια πλήρη βιβλιοθήκη όπως το `ocrmypdf` που ήδη ενσωματώνει hooks post‑processing. Το μοτίβο που καλύψαμε κλιμακώνεται άψογα, είτε διαχειρίζεστε μερικά τιμολόγια είτε εκατομμύρια σαρωμένα έγγραφα.

---

*Καλή προγραμματιστική, και οι OCR pipelines σας να παραμείνουν χωρίς σφάλματα!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}