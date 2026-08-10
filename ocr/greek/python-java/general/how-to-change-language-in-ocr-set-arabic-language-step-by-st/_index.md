---
category: general
date: 2026-06-22
description: Πώς να αλλάξετε γρήγορα τη γλώσσα στις μηχανές OCR. Μάθετε πώς να ορίσετε
  τη γλώσσα OCR στα Αραβικά (ar) χρησιμοποιώντας απλό κώδικα και αποφύγετε τις συνηθισμένες
  παγίδες.
draft: false
keywords:
- how to change language
- ocr language arabic
- how to set OCR
- change OCR language
- set language OCR
language: el
og_description: Πώς να αλλάξετε τη γλώσσα στις μηχανές OCR εξηγείται στην πρώτη πρόταση.
  Ακολουθήστε αυτό το σεμινάριο για να ορίσετε γρήγορα τη γλώσσα OCR στα Αραβικά.
og_title: Πώς να αλλάξετε τη γλώσσα στο OCR – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: How to change language in OCR engines quickly. Learn to set Arabic
    (ar) OCR language using simple code and avoid common pitfalls.
  headline: How to Change Language in OCR – Set Arabic Language Step‑by‑Step
  type: TechArticle
- description: How to change language in OCR engines quickly. Learn to set Arabic
    (ar) OCR language using simple code and avoid common pitfalls.
  name: How to Change Language in OCR – Set Arabic Language Step‑by‑Step
  steps:
  - name: '**Grab the OCR engine instance** – this is usually a singleton or a factory‑created
      object.'
    text: '**Grab the OCR engine instance** – this is usually a singleton or a factory‑created
      object.'
  - name: '**Pull the settings object** – most libraries keep language, DPI, and other
      options in a separate config container.'
    text: '**Pull the settings object** – most libraries keep language, DPI, and other
      options in a separate config container.'
  - name: '**Set the language code** – for Arabic the ISO‑639‑2 code is `"ar"`.'
    text: '**Set the language code** – for Arabic the ISO‑639‑2 code is `"ar"`.'
  type: HowTo
tags:
- OCR
- multilingual
- programming
title: Πώς να αλλάξετε τη γλώσσα στο OCR – Ορίστε την αραβική γλώσσα βήμα‑βήμα
url: /el/python-java/general/how-to-change-language-in-ocr-set-arabic-language-step-by-st/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Αλλάξετε τη Γλώσσα στο OCR – Πλήρης Οδηγός Προγραμματισμού

Το πώς να αλλάξετε τη γλώσσα σε μηχανές OCR είναι ένα συχνό εμπόδιο όταν αρχίζετε να ασχολείστε με πολυγλωσσικά έγγραφα. Σε αυτό το tutorial θα σας καθοδηγήσουμε βήμα‑βήμα για να ορίσετε τη γλώσσα OCR στα Αραβικά, με ένα εκτελέσιμο παράδειγμα κώδικα και εξηγήσεις για κάθε γραμμή. Αν ποτέ αναρωτηθήκατε *«πώς να ορίσετε το OCR* σε διαφορετικό σύστημα γραφής χωρίς να διακόψετε τη ροή*, βρίσκεστε στο σωστό μέρος*.

Θα καλύψουμε όλα όσα χρειάζεστε: τις απαιτούμενες βιβλιοθήκες, πώς να αποκτήσετε το στιγμιότυπο της μηχανής OCR, πώς να προσπελάσετε τις ρυθμίσεις της και, τέλος, πώς να αλλάξετε τη γλώσσα OCR με ασφάλεια. Στο τέλος θα μπορείτε να μεταβείτε από τα Αγγλικά στα Αραβικά (ή σε οποιαδήποτε άλλη υποστηριζόμενη γλώσσα) με μία μόνο κλήση μεθόδου. Χωρίς μαγεία, μόνο καθαρός κώδικας και μερικές πρακτικές συμβουλές.

## Προαπαιτούμενα

- Python 3.8+ (ή οποιαδήποτε πρόσφατη έκδοση)
- Μια βιβλιοθήκη OCR που εκθέτει αντικείμενο ρυθμίσεων – το παράδειγμα χρησιμοποιεί **pytesseract** τυλιγμένο σε μια μικρή βοηθητική κλάση, αλλά το ίδιο μοτίβο λειτουργεί και για άλλες μηχανές όπως EasyOCR ή το Microsoft Computer Vision SDK.
- Δεδομένα γλώσσας Αραβικών εγκατεστημένα για τη μηχανή OCR (`ara.traineddata` για το Tesseract).  
  *Pro tip:* σε Ubuntu μπορείτε να τα εγκαταστήσετε με `sudo apt-get install tesseract-ocr-ara`.

## Πώς να Αλλάξετε τη Γλώσσα στο OCR – Επισκόπηση

Η αλλαγή της γλώσσας είναι ουσιαστικά ένας χορός τριών βημάτων:

1. **Πάρτε το στιγμιότυπο της μηχανής OCR** – συνήθως είναι ένα singleton ή ένα αντικείμενο που δημιουργείται από factory.
2. **Αποκτήστε το αντικείμενο ρυθμίσεων** – οι περισσότερες βιβλιοθήκες διατηρούν τη γλώσσα, DPI και άλλες επιλογές σε ξεχωριστό container ρυθμίσεων.
3. **Ορίστε τον κωδικό γλώσσας** – για τα Αραβικά ο κωδικός ISO‑639‑2 είναι `"ar"`.

Παρακάτω υπάρχει ένα ελάχιστο, πλήρως εκτελέσιμο script που δείχνει αυτά τα βήματα.

![How to change language in OCR screenshot](image-placeholder.png "How to change language in OCR example")

## Βήμα 1: Δημιουργία ή Απόκτηση του Στιγμιότυπου της Μηχανής OCR

Πρώτα χρειαζόμαστε μια μηχανή. Σε πραγματικά έργα η μηχανή μπορεί να δημιουργείται αλλού και να περνιέται γύρω· για σαφήνεια θα την δημιουργήσουμε εδώ.

```python
# step1_engine.py
import pytesseract
from PIL import Image

class SimpleOCREngine:
    """A thin wrapper around pytesseract to expose a settings object."""
    def __init__(self):
        # pytesseract itself doesn't expose a mutable settings object,
        # so we store options in a dict that we later pass to image_to_string().
        self._options = {"lang": "eng"}  # default to English

    def get_settings(self):
        """Return a Settings object that can modify OCR options."""
        return OcrSettings(self)

    def recognize(self, image_path: str) -> str:
        """Run OCR on the given image using current options."""
        img = Image.open(image_path)
        return pytesseract.image_to_string(img, config=self._build_config())

    def _build_config(self) -> str:
        """Convert the internal options dict to a Tesseract command line."""
        # Example: '-l eng' or '-l ar+eng' for multiple languages
        lang_option = self._options.get("lang", "eng")
        return f"-l {lang_option}"
```

**Γιατί τυλίγουμε τη μηχανή** – πολλές SDK OCR (συμπεριλαμβανομένου του Tesseract) απαιτούν τη γλώσσα ως συμβολοσειρά σε κάθε κλήση. Ενσωματώνοντας τις επιλογές σε αντικείμενο ρυθμίσεων παίρνουμε ένα καθαρό, *how to set OCR*‑στυλ API που αντικατοπτρίζει το αρχικό απόσπασμα κώδικα που δώσατε.

## Βήμα 2: Πρόσβαση στο Αντικείμενο Ρυθμίσεων της Μηχανής

Τώρα που έχουμε τη μηχανή, ανακτούμε τις ρυθμίσεις της. Αυτό αντικατοπτρίζει τη δεύτερη γραμμή του αρχικού παραδείγματος (`settings = engine.get_settings()`).

```python
# step2_settings.py
class OcrSettings:
    """Provides getters and setters for OCR configuration."""
    def __init__(self, engine: SimpleOCREngine):
        self._engine = engine

    def set_language(self, lang_code: str):
        """
        Change OCR language.
        :param lang_code: ISO‑639‑2 language code, e.g., 'ar' for Arabic.
        """
        # Validate the language code – a tiny safety net.
        if not isinstance(lang_code, str) or len(lang_code) < 2:
            raise ValueError("Language code must be a non‑empty string.")
        self._engine._options["lang"] = lang_code

    def get_language(self) -> str:
        """Return the currently configured language code."""
        return self._engine._options.get("lang", "eng")
```

Εδώ εκθέτουμε τη **how to set OCR** γλώσσα μέσω `set_language`. Η μέθοδος εκτελεί επίσης έναν βασικό έλεγχο λογικής, κάτι που αποτελεί καλή πρακτική αμυντικού προγραμματισμού.

## Βήμα 3: Ορισμός της Γλώσσας OCR στα Αραβικά (ocr language arabic)

Τέλος, καλούμε τη μέθοδο με τον κωδικό Αραβικών `"ar"`. Αυτό είναι η καρδιά της λειτουργίας *change OCR language*.

```python
# step3_change_language.py
from step1_engine import SimpleOCREngine

# Obtain the OCR engine instance (could be a singleton in a larger app)
engine = SimpleOCREngine()

# Access the settings object
settings = engine.get_settings()

# Set the OCR language to Arabic – this is the "how to change language" line.
settings.set_language("ar")

# Optional: verify the change
print("Current OCR language:", settings.get_language())

# Run OCR on a sample Arabic image (replace with your own path)
# result = engine.recognize("sample_arabic.png")
# print("OCR Output:", result)
```

**Αναμενόμενη έξοδος**

```
Current OCR language: ar
```

Αν ξεσχολιάσετε την κλήση `recognize` και την κατευθύνετε σε μια πραγματική εικόνα Αραβικών, θα πρέπει να δείτε χαρακτήρες Αραβικών στην κονσόλα (εφόσον τα δεδομένα γλώσσας είναι εγκατεστημένα).

## Πώς να Ορίσετε OCR για Πολλές Γλώσσες

Μερικές φορές χρειάζεστε *ocr language arabic* **και** Αγγλικά, ειδικά για μικτά έγγραφα. Η μέθοδος `set_language` μπορεί να δεχτεί λίστα χωρισμένη με `+`:

```python
settings.set_language("ar+eng")
print("Now recognizing both Arabic and English:", settings.get_language())
```

*Edge case*: Αν το ζητούμενο πακέτο γλώσσας δεν είναι εγκατεστημένο, το Tesseract θα πετάξει σφάλμα όπως `Error opening language file`. Για να αποφύγετε την κατάρρευση, μπορείτε να πιάσετε την εξαίρεση και να επιστρέψετε σε προεπιλεγμένη γλώσσα.

```python
try:
    settings.set_language("ar")
except Exception as e:
    print("Failed to set Arabic language:", e)
    settings.set_language("eng")  # fallback
```

## Δυναμική Αλλαγή Γλώσσας OCR Κατά τη Λειτουργία

Σε πολλές εφαρμογές ο χρήστης επιλέγει γλώσσα από ένα dropdown. Επειδή οι ρυθμίσεις ζουν μέσα στο αντικείμενο της μηχανής, μπορείτε να αλλάζετε γλώσσες «on‑the‑fly» χωρίς να επαναδημιουργήσετε τη μηχανή.

```python
def switch_language(lang_code: str):
    settings.set_language(lang_code)
    print(f"OCR language switched to {lang_code}")

# Example usage:
switch_language("fr")   # switch to French
switch_language("ar")   # back to Arabic
```

Αυτό το μοτίβο ικανοποιεί την απαίτηση *set language OCR* ενώ διατηρεί τον κώδικα τακτοποιημένο.

## Συνηθισμένα Προβλήματα και Pro Tips

| Πρόβλημα | Τι Συμβαίνει | Διόρθωση |
|----------|--------------|----------|
| Λείπει το πακέτο γλώσσας | Το Tesseract επιστρέφει “Failed loading language ‘ar’” | Εγκαταστήστε τα δεδομένα γλώσσας (`sudo apt-get install tesseract-ocr-ara` ή κατεβάστε τα από το αποθετήριο). |
| Χρήση λανθασμένου κώδικα ISO | Δεν υπάρχει έξοδος ή εμφανίζονται ακατανόητοι χαρακτήρες | Επαληθεύστε τον κώδικα (`ar` για Αραβική, `eng` για Αγγλικά, `chi_sim` για Απλοποιημένα Κινέζικα). |
| Ξεχάτε να ξαναχτίσετε τη διαμόρφωση | Η μηχανή εξακολουθεί να χρησιμοποιεί την παλιά γλώσσα | Πάντα καλέστε `engine._build_config()` (χειρίζεται εσωτερικά όταν καλείτε `recognize`). |
| Περνώντας λίστα αντί για συμβολοσειρά | TypeError | Χρησιμοποιήστε `"ar+eng"` ως μία ενιαία συμβολοσειρά, όχι `["ar", "eng"]`. |

## Πλήρες Παράδειγμα Εργασίας (Όλα τα Τμήματα Μαζί)

```python
# full_example.py
import pytesseract
from PIL import Image

class SimpleOCREngine:
    def __init__(self):
        self._options = {"lang": "eng"}

    def get_settings(self):
        return OcrSettings(self)

    def recognize(self, image_path: str) -> str:
        img = Image.open(image_path)
        return pytesseract.image_to_string(img, config=self._build_config())

    def _build_config(self) -> str:
        return f"-l {self._options.get('lang', 'eng')}"

class OcrSettings:
    def __init__(self, engine: SimpleOCREngine):
        self._engine = engine

    def set_language(self, lang_code: str):
        if not isinstance(lang_code, str) or len(lang_code) < 2:
            raise ValueError("Language code must be a non‑empty string.")
        self._engine._options["lang"] = lang_code

    def get_language(self) -> str:
        return self._engine._options.get("lang", "eng")

# ---------- Usage ----------
engine = SimpleOCREngine()
settings = engine.get_settings()

# Change to Arabic (how to change language)
settings.set_language("ar")
print("Current OCR language:", settings.get_language())

# Uncomment and point to a real Arabic image to test OCR
# output = engine.recognize("sample_arabic.png")
# print("OCR result:", output)
```

Τρέξτε το script με `python full_example.py`. Αν όλα είναι ρυθμισμένα, θα δείτε:

```
Current OCR language: ar
```

…και την έξοδο OCR για την εικόνα Αραβικών αν ενεργοποιήσετε τις τελευταίες δύο γραμμές.

## Συμπέρασμα

Τώρα ξέρετε **πώς να αλλάξετε τη γλώσσα σε μηχανές OCR**, συγκεκριμένα πώς να ορίσετε τη γλώσσα OCR στα Αραβικά χρησιμοποιώντας ένα καθαρό, επαναχρησιμοποιήσιμο μοτίβο. Ο οδηγός διέσχισε την απόκτηση της μηχανής, την πρόσβαση στις ρυθμίσεις της και, τέλος, την εφαρμογή της αλλαγής γλώσσας—καλύπτοντας τόσο το σενάριο *ocr language arabic* όσο και το ευρύτερο *change OCR language*.  

Τι θα κάνετε στη συνέχεια; Δοκιμάστε να προσθέσετε υποστήριξη για περισσότερες γλώσσες, πειραματιστείτε με πολυγλωσσικές συμβολοσειρές (`"ar+eng"`), ή ενσωματώστε αυτή τη λογική σε μια υπηρεσία web που επιτρέπει στους χρήστες να ανεβάζουν έγγραφα σε οποιοδήποτε σύστημα γραφής. Αν σας ενδιαφέρει το *set language OCR* σε άλλες βιβλιοθήκες (EasyOCR, Google Vision...

## Τι Θα Μάθετε Στη Σύντομη Επόμενη Στιγμή;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Extract OCR – OCR Configuration](/ocr/english/net/ocr-configuration/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}