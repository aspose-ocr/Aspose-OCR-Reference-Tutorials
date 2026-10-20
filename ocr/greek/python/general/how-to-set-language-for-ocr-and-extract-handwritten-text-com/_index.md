---
category: general
date: 2026-03-26
description: Πώς να ορίσετε τη γλώσσα σε μια μηχανή OCR και να εξάγετε χειρόγραφο
  κείμενο από εικόνες – βήμα‑βήμα οδηγός για τη μετατροπή εικόνας σε κείμενο.
draft: false
keywords:
- how to set language
- extract handwritten text
- convert image to text
- how to extract handwritten
- recognize handwritten notes
language: el
og_description: Πώς να ορίσετε τη γλώσσα σε μια μηχανή OCR και να εξάγετε χειρόγραφα
  σημειώματα από εικόνες. Μάθετε πώς να μετατρέπετε εικόνα σε κείμενο σε λίγα λεπτά.
og_title: Πώς να ορίσετε τη γλώσσα για OCR – Εξαγωγή χειρόγραφου κειμένου εύκολα
tags:
- OCR
- Python
- Image Processing
title: Πώς να ορίσετε τη γλώσσα για OCR και να εξάγετε χειρόγραφο κείμενο – Πλήρης
  οδηγός
url: /el/python/general/how-to-set-language-for-ocr-and-extract-handwritten-text-com/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Ορίσετε τη Γλώσσα για OCR και να Εξάγετε Χειρόγραφο Κείμενο – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να ορίσετε τη γλώσσα** στο OCR engine σας ώστε να καταλαβαίνει πραγματικά τους χαρακτήρες που χρειάζεστε; Ίσως έχετε μια φωτογραφία λίστας αγορών, μια σημείωση συνάντησης ή ένα σκίτσο διαγράμματος και δεν μπορείτε να εξάγετε το κείμενο. Τα καλά νέα; Δεν χρειάζεστε διδακτορικό στην υπολογιστική όραση—μόνο μερικές γραμμές Python και τις σωστές επιλογές.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα τις ακριβείς ενέργειες για **εξάγετε χειρόγραφο κείμενο** από ένα PNG, να μετατρέψετε αυτήν την εικόνα σε απλό κείμενο, και να εξηγήσουμε το “γιατί” πίσω από κάθε ρύθμιση. Στο τέλος θα μπορείτε να αναγνωρίζετε χειρόγραφες σημειώσεις σε οποιοδήποτε έργο, είτε πρόκειται για εφαρμογή λήψης σημειώσεων είτε για pipeline μαζικής επεξεργασίας.

> **Τι θα χρειαστείτε**  
> • Python 3.8+ (ο κώδικας λειτουργεί και με 3.10)  
> • Η βιβλιοθήκη `ocr` (ή οποιοδήποτε συμβατό wrapper που εκθέτει `OcrEngine`)  
> • Ένα δείγμα εικόνας όπως `note_handwritten.png` – οποιαδήποτε εικόνα με εκτεταμένους λατινικούς χαρακτήρες αρκεί.

Ας ξεκινήσουμε.

---

## Πώς να Ορίσετε τη Γλώσσα και να Ενεργοποιήσετε την Αναγνώριση Χειρόγραφου

Το πρώτο πράγμα που πρέπει να κάνετε είναι να πείτε στο OCR engine ποιο αλφάβητο πρέπει να περιμένει. Αν παραλείψετε αυτό το βήμα, η μηχανή χρησιμοποιεί ένα γενικό σύνολο που συχνά αναγνωρίζει λανθασμένα τους τονισμένους χαρακτήρες ή ειδικά σύμβολα.

```python
import ocr  # Assuming the library is named `ocr`

# Step 1: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Step 2: Choose the language that includes extended Latin characters
ocr_engine.language = ocr.Language.ExtendedLatin

# Step 3: Turn on the handwritten‑text flag
ocr_engine.recognize_handwritten = True
```

**Γιατί αυτό είναι σημαντικό:**  
- **ExtendedLatin** καλύπτει χαρακτήρες όπως “ñ”, “ø”, και “ç”, που είναι συνηθισμένοι σε πολλές ευρωπαϊκές σημειώσεις.  
- Το flag `recognize_handwritten` αλλάζει το υποκείμενο μοντέλο από OCR τυπωμένου κειμένου σε νευρωνικό δίκτυο εκπαιδευμένο σε καμπυλωτές γραμμές. Χωρίς αυτό, η μηχανή αντιμετωπίζει τις γραφές σας ως θόρυβο.

> **Συμβουλή:** Αν επεξεργάζεστε έγγραφα σε πολλαπλές γλώσσες, δημιουργήστε ξεχωριστό engine ανά γλώσσα ή αλλάξτε δυναμικά το `ocr_engine.language` πριν από κάθε κλήση. Αυτό αποφεύγει το κόστος φόρτωσης αχρησιμοποίητων συνόλων χαρακτήρων.

![Screenshot of OCR engine configuration showing how to set language](/images/ocr-set-language.png "How to set language on OCR engine")

*Image alt text: “Πώς να ορίσετε τη γλώσσα στην οθόνη ρύθμισης του OCR engine.”*

---

## Εξάγετε Χειρόγραφο Κείμενο από Μία Εικόνα PNG

Τώρα που η μηχανή ξέρει τι πρέπει να ψάξει, ήρθε η ώρα να της δώσετε μια εικόνα. Η μέθοδος `recognize_image` επιστρέφει ένα πλούσιο αντικείμενο αποτελέσματος· το χαρακτηριστικό `text` περιέχει το απλό κείμενο που σας ενδιαφέρει.

```python
# Step 4: Perform OCR on the input image
handwritten_result = ocr_engine.recognize_image("YOUR_DIRECTORY/note_handwritten.png")

# Step 5: Print the extracted text
print(handwritten_result.text)
```

Όταν εκτελέσετε το script, θα δείτε κάτι σαν:

```
Buy milk
Call Dr. García at 5 pm
Pick up résumé
```

Αυτή η έξοδος αποδεικνύει ότι μετατρέψατε επιτυχώς **εικόνα σε κείμενο** και ότι η μηχανή τήρησε τη ρύθμιση γλώσσας που δώσατε.

**Συνηθισμένα προβλήματα**  
- **Incorrect path** – Ελέγξτε ξανά τη θέση του αρχείου· ένα αρχείο που λείπει προκαλεί `FileNotFoundError`.  
- **Low‑resolution image** – Η αναγνώριση χειρόγραφου δυσκολεύεται κάτω από 300 dpi. Αυξήστε την ανάλυση ή σκανάρετε ξανά αν η έξοδος φαίνεται χαοτική.  
- **Color inversion** – Αν το φόντο είναι σκοτεινό και το μελάνι ανοιχτό, αντιστρέψτε πρώτα τα χρώματα (`Pillow` μπορεί να βοηθήσει).

---

## Μετατρέψτε Εικόνα σε Κείμενο Χρησιμοποιώντας μια Βοηθητική Συνάρτηση

Αν σκοπεύετε να τρέχετε OCR σε δεκάδες αρχεία, τυλίξτε τη λογική σε μια επαναχρησιμοποιήσιμη συνάρτηση. Αυτό κάνει επίσης τον κώδικα πιο εύκολο στη δοκιμή και στην ενσωμάτωση με άλλα pipelines.

```python
def extract_handwritten_text(image_path: str) -> str:
    """
    Loads an image, sets the OCR engine to ExtendedLatin,
    enables handwritten recognition, and returns the plain text.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ExtendedLatin
    engine.recognize_handwritten = True

    result = engine.recognize_image(image_path)
    return result.text.strip()   # Remove leading/trailing whitespace


# Example usage
if __name__ == "__main__":
    txt = extract_handwritten_text("YOUR_DIRECTORY/note_handwritten.png")
    print("📝 Handwritten notes:\n", txt)
```

Η βοηθητική συνάρτηση απομονώνει τη λογική **πώς να εξάγετε χειρόγραφο** ώστε να τη καλέσετε από ένα endpoint Flask, ένα εργαλείο CLI ή μια εργασία batch χωρίς να ξαναγράψετε τη ρύθμιση κάθε φορά.

---

## Αναγνωρίστε Χειρόγραφες Σημειώσεις σε Πραγματικές Καταστάσεις

Παρακάτω παρουσιάζονται μερικές καταστάσεις όπου πιθανότατα θα χρειαστείτε **αναγνώριση χειρόγραφων σημειώσεων** και πώς αυτή η ρύθμιση προσαρμόζεται:

| Σενάριο | Γιατί η γλώσσα είναι σημαντική | Προτεινόμενη προσαρμογή |
|----------|-------------------------------|------------------------|
| **Multilingual grocery lists** | Τα είδη μπορεί να περιέχουν τόνους (π.χ., “crème”) | Αλλάξτε `ocr_engine.language` ανά λίστα ή χρησιμοποιήστε `ocr.Language.AutoDetect` αν υποστηρίζεται |
| **Classroom whiteboard photos** | Η κιμωλία μπορεί να παράγει αχνές γραμμές | Αυξήστε την αντίθεση της εικόνας πριν τη δώσετε στη μηχανή |
| **Medical prescriptions** | Η γραφή είναι συχνά ακατάστατη | Συνδυάστε OCR με λεξικό διόρθωσης ορθογραφίας για ονόματα φαρμάκων |

Σε κάθε περίπτωση, τα βασικά βήματα—**πώς να ορίσετε τη γλώσσα**, ενεργοποίηση της λειτουργίας χειρόγραφου, και κλήση του `recognize_image`—παραμένουν τα ίδια. Αυτή η συνέπεια κάνει την προσέγγιση αξιόπιστη και εύκολη στη συντήρηση.

---

## Ακραίες Περιπτώσεις & Προχωρημένες Ρυθμίσεις

1. **Batch processing** – Φορτώστε το engine μία φορά, κάντε βρόχο στα αρχεία, και αλλάξτε το χαρακτηριστικό `language` μόνο όταν χρειάζεται. Αυτό μειώνει το κόστος εκκίνησης.  
2. **Non‑Latin scripts** – Αν χρειάζεται να επεξεργαστείτε κυριλλικά ή αραβικά, αντικαταστήστε το `ExtendedLatin` με το αντίστοιχο enum (π.χ., `ocr.Language.Cyrillic`). Το ίδιο μοτίβο ισχύει.  
3. **Partial recognition** – Μερικές φορές η μηχανή επιστρέφει κενές συμβολοσειρές για πολύ σύντομες γραμμές. Μια γρήγορη έλεγχος (`if not result.text.strip(): …`) σας επιτρέπει να περάσετε σε δευτερεύον μοντέλο ή να ζητήσετε από τον χρήστη να σκανάρει ξανά.  
4. **Performance profiling** – Για μεγάλα σύνολα δεδομένων, χρονομετρήστε την κλήση `recognize_image`. Αν γίνει bottleneck, σκεφτείτε παραλληλοποίηση με `concurrent.futures.ThreadPoolExecutor`.

---

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω βρίσκεται το πλήρες script που μπορείτε να αντιγράψετε σε ένα αρχείο με όνομα `handwritten_ocr.py`. Περιλαμβάνει ανάλυση ορισμάτων ώστε να μπορείτε να το κατευθύνετε σε οποιαδήποτε εικόνα από τη γραμμή εντολών.

```python
#!/usr/bin/env python3
"""
handwritten_ocr.py – Convert an image containing handwritten notes
to plain text using the OCR library.

Usage:
    python handwritten_ocr.py path/to/image.png
"""

import sys
import argparse
import ocr  # Replace with the actual import if the library name differs


def extract_handwritten_text(image_path: str) -> str:
    """Extracts handwritten text from the given image."""
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ExtendedLatin
    engine.recognize_handwritten = True

    result = engine.recognize_image(image_path)
    return result.text.strip()


def main():
    parser = argparse.ArgumentParser(
        description="Convert handwritten image to text (how to set language, extract handwritten text)."
    )
    parser.add_argument("image", help="Path to the PNG/JPG image containing handwritten notes")
    args = parser.parse_args()

    try:
        text = extract_handwritten_text(args.image)
        if text:
            print("✅ Extracted text:\n", text)
        else:
            print("⚠️ No text detected – try a higher‑resolution image.")
    except Exception as e:
        print(f"❌ Error processing {args.image}: {e}", file=sys.stderr)
        sys.exit(1)


if __name__ == "__main__":
    main()
```

Τρέξτε το έτσι:

```bash
python handwritten_ocr.py YOUR_DIRECTORY/note_handwritten.png
```

Θα δείτε την ίδια έξοδο όπως στο προηγούμενο απόσπασμα, επιβεβαιώνοντας ότι μετατρέψατε επιτυχώς **εικόνα σε κείμενο** και **αναγνωρίσατε χειρόγραφες σημειώσεις**.

---

## Συμπέρασμα

Καλύψαμε **πώς να ορίσετε τη γλώσσα** σε ένα OCR engine, ενεργοποιήσαμε τη σημαία χειρόγραφου κειμένου, και δημιουργήσαμε μια επαναχρησιμοποιήσιμη συνάρτηση που **εξάγει χειρόγραφο κείμενο** από οποιαδήποτε εικόνα. Ακολουθώντας τα παραπάνω βήματα μπορείτε αξιόπιστα **να μετατρέψετε εικόνα σε κείμενο**, είτε διαχειρίζεστε μια μοναδική σημείωση είτε ένα τεράστιο αρχείο σαρωμένων εγγράφων.

Στη συνέχεια, δοκιμάστε διαφορετικά πακέτα γλώσσας, επεξεργαστείτε μαζικά έναν φάκελο εικόνων, ή ενσωματώστε αυτή τη λογική σε μια web υπηρεσία που επιστρέφει αποτελέσματα JSON. Τα θεμέλια παραμένουν τα ίδια, και η ευελιξία της βιβλιοθήκης `ocr` σημαίνει ότι μπορείτε να προσαρμοστείτε σε σχεδόν οποιαδήποτε περίπτωση χρήσης.

Έχετε ερωτήσεις για ακραίες περιπτώσεις, απόδοση ή επέκταση του script σε άλλες γλώσσες; Αφήστε ένα σχόλιο ή στείλτε μου μήνυμα στο GitHub – καλή κωδικοποίηση!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}