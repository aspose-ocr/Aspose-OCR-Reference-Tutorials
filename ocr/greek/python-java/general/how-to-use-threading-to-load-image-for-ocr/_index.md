---
category: general
date: 2026-04-26
description: Πώς να χρησιμοποιήσετε νήματα για τη φόρτωση εικόνας για OCR σε Python.
  Μάθετε την ασύγχρονη επεξεργασία OCR με callbacks, νήματα παρασκηνίου και φόρτωση
  εικόνας σε λίγα μόνο βήματα.
draft: false
keywords:
- how to use threading
- load image for OCR
- python threading OCR
- async OCR callback
- background thread image processing
language: el
og_description: Πώς να χρησιμοποιήσετε νήματα για τη φόρτωση εικόνας για OCR σε Python.
  Αυτός ο οδηγός παρουσιάζει ένα πλήρες, εκτελέσιμο παράδειγμα με κλήσεις επιστροφής
  και εκτέλεση στο παρασκήνιο.
og_title: Πώς να χρησιμοποιήσετε το threading για τη φόρτωση εικόνας για OCR
tags:
- Python
- Threading
- OCR
- Image Processing
title: Πώς να χρησιμοποιήσετε το threading για τη φόρτωση εικόνας για OCR
url: /el/python-java/general/how-to-use-threading-to-load-image-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε Threading για Φόρτωση Εικόνας για OCR

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε threading** για να φορτώσετε μια εικόνα για OCR χωρίς να παγώσει η εφαρμογή σας; Είναι ένα σενάριο που εμφανίζεται είτε χτίζετε έναν επιτραπέζιο σαρωτή, μια υπηρεσία web, ή ένα απλό script που επεξεργάζεται τεράστιες εικόνες. Τα καλά νέα; Μερικές γραμμές Python και το σωστό μοτίβο threading θα κρατήσουν το UI σας γρήγορο ενώ η μηχανή OCR κάνει τη μαγεία της.

Σε αυτό το tutorial θα περάσουμε από ένα πλήρες, end‑to‑end παράδειγμα: φόρτωση ενός μεγάλου PNG, εκκίνηση OCR σε νήμα background, και διαχείριση του αποτελέσματος με callback. Στο τέλος δεν θα ξέρετε μόνο **πώς να χρησιμοποιήσετε threading**, αλλά και **πώς να φορτώσετε εικόνα για OCR** με καθαρό, επαναχρησιμοποιήσιμο τρόπο.

## Τι Θα Χρειαστείτε

- Python 3.9+ (η σύνταξη που χρησιμοποιούμε λειτουργεί σε οποιαδήποτε πρόσφατη έκδοση)
- `pillow` για διαχείριση εικόνων (`pip install pillow`)
- `pytesseract` ως ελαφρύ wrapper γύρω από το Tesseract OCR (`pip install pytesseract`)
- Μηχανή Tesseract OCR εγκατεστημένη στο σύστημά σας (κατεβάστε από [tesseract‑ocr.org](https://github.com/tesseract-ocr/tesseract))
- Ένα μεγάλο αρχείο εικόνας που θέλετε να επεξεργαστείτε (`large_image.png` σε αυτόν τον οδηγό)

Καμία επιπλέον βιβλιοθήκη, χωρίς async/await—μόνο κλασικό `threading` και ένα callback.

## Βήμα 1: Εισαγωγή του Module Threading (Απαιτείται για Εκτέλεση στο Παρασκήνιο)

Το πρώτο που κάνουμε είναι να φέρουμε το module `threading`. Σας παρέχει την κλάση `Thread`, η οποία μας επιτρέπει να τρέξουμε οποιαδήποτε συνάρτηση σε ξεχωριστό νήμα του λειτουργικού συστήματος.

```python
import threading
```

*Γιατί είναι σημαντικό*: Αν τρέξετε OCR στο κύριο νήμα, το πρόγραμμά σας (ιδιαίτερα ένα GUI) θα παγώσει μέχρι να ολοκληρωθεί το OCR. Αναθέτοντας τη δουλειά σε νήμα background, το κύριο νήμα παραμένει ελεύθερο για ενημέρωση του UI, διαχείριση εισόδου χρήστη ή εκκίνηση άλλων εργασιών.

## Βήμα 2: Ορισμός Callback που Θα Κληθεί Όταν Το OCR Ολοκληρωθεί

Ένα callback είναι απλώς μια συνάρτηση που καλείται από άλλο κομμάτι κώδικα όταν ολοκληρωθεί. Εδώ θα τυπώσουμε το αναγνωρισμένο κείμενο, αλλά μπορείτε να το αποθηκεύσετε, να το στείλετε μέσω δικτύου ή να ενημερώσετε ένα widget UI.

```python
def ocr_done(result_text: str) -> None:
    """Called when the OCR thread finishes."""
    print("\n--- Async OCR finished ---")
    print(result_text)   # Display the recognized text
```

*Συμβουλή*: Κρατήστε το callback ελαφρύ. Η βαριά επεξεργασία μέσα στο callback αναιρεί το σκοπό του threading, επειδή θα μπλοκάρει ακόμα το νήμα που το κάλεσε (συχνά το κύριο νήμα).

## Βήμα 3: Φόρτωση της Εικόνας που Θέλετε να Επεξεργαστείτε

Η φόρτωση της εικόνας είναι ξεχωριστό ζήτημα από το OCR, αλλά αποτελεί μέρος της συνολικής ροής εργασίας. Η χρήση του Pillow το κάνει τελείως απλό.

```python
from PIL import Image

def load_image(path: str) -> Image.Image:
    """Loads an image from disk and returns a Pillow Image object."""
    try:
        img = Image.open(path)
        print(f"Image '{path}' loaded – size: {img.size}")
        return img
    except Exception as exc:
        raise RuntimeError(f"Failed to load image: {exc}") from exc
```

*Γιατί το κάνουμε εδώ*: Αν η εικόνα είναι τεράστια, η φόρτωση στο κύριο νήμα μπορεί ήδη να προκαλέσει καθυστέρηση. Σε πολλές πραγματικές εφαρμογές θα αποθέτατε και τη φόρτωση σε νήμα, αλλά για σαφήνεια τη διατηρούμε συγχρονισμένη.

## Βήμα 4: Δημιουργία Μικρού Wrapper για τη Μηχανή OCR

Το αρχικό απόσπασμα χρησιμοποίησε `engine.process_async`. Θα μιμηθούμε αυτό με μια μικρή κλάση που δημιουργεί εσωτερικά ένα νήμα και καλεί το παρεχόμενο callback όταν τελειώσει.

```python
import pytesseract

class SimpleOcrEngine:
    """A minimal OCR engine that runs pytesseract in a background thread."""

    def __init__(self, image: Image.Image):
        self.image = image

    def _run_ocr(self, callback):
        """Internal method executed in the worker thread."""
        try:
            # pytesseract returns the recognized text as a plain string
            text = pytesseract.image_to_string(self.image)
            callback(text)
        except Exception as exc:
            callback(f"OCR failed: {exc}")

    def process_async(self, callback):
        """Public method to start OCR on a new thread."""
        worker = threading.Thread(target=self._run_ocr, args=(callback,))
        worker.daemon = True          # Daemon so it won’t block program exit
        worker.start()
        print("OCR thread started…")
```

*Εξήγηση*:  
- `_run_ocr` κάνει τη βαριά δουλειά.  
- `process_async` δημιουργεί ένα αντικείμενο `Thread`, το ορίζει ως daemon (ώστε ο διερμηνέας να μπορεί να τερματιστεί ακόμη και αν το νήμα τρέχει) και το ξεκινά.  
- Το callback λαμβάνει είτε το κείμενο OCR είτε ένα μήνυμα σφάλματος.

## Βήμα 5: Συνδυάστε Όλα και Κάντε Άλλο Καθώς Το OCR Εκτελείται

Τώρα οργανώνουμε όλη τη ροή: φορτώνουμε την εικόνα, δημιουργούμε την μηχανή, ξεκινάμε το async OCR, και κρατάμε το κύριο νήμα απασχολημένο με κάτι άλλο (εδώ απλώς τυπώνουμε ένα μήνυμα).

```python
if __name__ == "__main__":
    # 1️⃣ Load the image you want to OCR
    img_path = "YOUR_DIRECTORY/large_image.png"
    image = load_image(img_path)

    # 2️⃣ Create the OCR engine instance
    engine = SimpleOcrEngine(image)

    # 3️⃣ Start OCR on a background thread, passing our callback
    engine.process_async(callback=ocr_done)

    # 4️⃣ Do other work while OCR runs (simulated with a loop)
    for i in range(5):
        print(f"Main thread doing other work… ({i+1}/5)")
        # In a real app you might update a progress bar, handle UI events, etc.
        threading.Event().wait(0.5)  # Sleep 0.5 s without blocking the OS thread

    # Give the OCR thread a moment to finish before the script exits
    threading.Event().wait(2)
    print("Script finished.")
```

**Αναμενόμενο αποτέλεσμα (κομμένο για συντομία):**

```
Image 'YOUR_DIRECTORY/large_image.png' loaded – size: (3840, 2160)
OCR thread started…
Main thread doing other work… (1/5)
Main thread doing other work… (2/5)
...
--- Async OCR finished ---
The quick brown fox jumps over the lazy dog.
Script finished.
```

Αν το OCR αποτύχει, το callback θα τυπώσει ένα μήνυμα σφάλματος αντί για το κείμενο.

---

## Γιατί Αυτή η Προσέγγιση Λειτουργεί Καλύτερα Από Έναν Απλό Βρόχο

- **Ανταπόκριση**: Το κύριο νήμα ποτέ δεν μπλοκάρει στην κλήση OCR, η οποία μπορεί να διαρκέσει δευτερόλεπτα για μεγάλες εικόνες.
- **Κλιμάκωση**: Μπορείτε να δημιουργήσετε πολλαπλά στιγμιότυπα `SimpleOcrEngine`, το καθένα σε δικό του νήμα, για επεξεργασία παρτίδας εικόνων ταυτόχρονα.
- **Διαχωρισμός Ευθυνών**: Η φόρτωση, η επεξεργασία και η διαχείριση αποτελεσμάτων είναι καθαρά διαχωρισμένες, καθιστώντας τον κώδικα πιο εύκολο στη δοκιμή και συντήρηση.

## Συνηθισμένα Παγίδες και Πώς να τις Αποφύγετε

| Παγίδα | Τι Συμβαίνει | Διόρθωση |
|--------|--------------|----------|
| Ξέχνατε να ορίσετε το νήμα ως *daemon* | Το script κολλάει μετά το τέλος της κύριας εργασίας επειδή το νήμα OCR είναι ακόμα ζωντανό. | Ορίστε `worker.daemon = True` **ή** καλέστε `join()` στο νήμα πριν την έξοδο. |
| Χρήση παγκόσμιας μεταβλητής για το αποτέλεσμα χωρίς κλειδώματα | Συνθήκες αγώνα μπορεί να καταστρέψουν τα δεδομένα όταν πολλά νήματα γράφουν ταυτόχρονα. | Περάστε το αποτέλεσμα μέσω callback (όπως κάνουμε) ή χρησιμοποιήστε δομές ασφαλείς για νήματα όπως `queue.Queue`. |
| Φόρτωση τεράστιας εικόνας στο κύριο νήμα | Το UI παγώνει πριν καν ξεκινήσει το OCR στο παρασκήνιο. | Αποθέστε τη φόρτωση της εικόνας σε νήμα επίσης, ή χρησιμοποιήστε τεχνικές lazy loading. |
| Μη διαχείριση εξαιρέσεων μέσα στο νήμα εργασίας | Απρόσμενες εξαιρέσεις σκοτώνουν σιωπηλά το νήμα, αφήνοντάς σας χωρίς αποτέλεσμα. | Τυλίξτε τη λογική OCR σε `try/except` και προωθήστε το σφάλμα στο callback. |

## Επέκταση Αυτού του Μοτίβου

- **Αναφορά Προόδου**: Χρησιμοποιήστε ένα κοινό `queue.Queue` για να στέλνετε ενδιάμεσες ποσοστιαίες προόδους από το νήμα OCR στο κύριο νήμα.
- **Thread Pool**: Για επεξεργασία παρτίδας, αντικαταστήστε τα μεμονωμένα αντικείμενα `Thread` με ένα `concurrent.futures.ThreadPoolExecutor`.
- **Ενσωμάτωση σε GUI**: Σε εφαρμογή Tkinter ή PyQt, προγραμματίστε το callback με `after()` (Tkinter) ή `QTimer.singleShot` (Qt) ώστε οι ενημερώσεις UI να γίνονται στο κύριο νήμα.

## Πλήρες Παράδειγμα Εργασίας (Ready για Copy‑Paste)

```python
import threading
from PIL import Image
import pytesseract

def ocr_done(result_text: str) -> None:
    """Callback invoked when OCR finishes."""
    print("\n--- Async OCR finished ---")
    print(result_text)

def load_image(path: str) -> Image.Image:
    """Load an image and report its size."""
    try:
        img = Image.open(path)
        print(f"Image '{path}' loaded – size: {img.size}")
        return img

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}