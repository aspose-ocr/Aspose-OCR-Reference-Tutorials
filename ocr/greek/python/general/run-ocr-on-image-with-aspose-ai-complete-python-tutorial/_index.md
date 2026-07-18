---
category: general
date: 2026-07-18
description: Εκτελέστε OCR σε εικόνα χρησιμοποιώντας το Aspose OCR στην Python. Μάθετε
  πώς να εξάγετε απλό κείμενο από την εικόνα, να εφαρμόζετε AI επεξεργασία μετά, και
  να λαμβάνετε καθαρά αποτελέσματα γρήγορα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- run OCR on image
- extract plain text from image
- Aspose OCR Python
- AI post‑processor OCR
- image text extraction
language: el
lastmod: 2026-07-18
og_description: Εκτελέστε OCR σε εικόνα με το Aspose OCR και την Python. Αυτό το σεμινάριο
  δείχνει πώς να εξάγετε απλό κείμενο από την εικόνα και να βελτιώσετε την ακρίβεια
  χρησιμοποιώντας έναν AI μετα-επεξεργαστή.
og_image_alt: Screenshot showing run OCR on image results in Python console
og_title: Εκτέλεση OCR σε εικόνα – Πλήρης οδηγός Python με Aspose AI
schemas:
- author: Aspose
  dateModified: '2026-07-18'
  description: Run OCR on image using Aspose OCR in Python. Learn to extract plain
    text from image, apply AI post‑processing, and get clean results fast.
  headline: Run OCR on Image with Aspose AI – Complete Python Tutorial
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- AI
title: Εκτέλεση OCR σε εικόνα με το Aspose AI – Πλήρης οδηγός Python
url: /el/python/general/run-ocr-on-image-with-aspose-ai-complete-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε εικόνα με Aspose AI – Πλήρες Python Tutorial

Έχετε ποτέ αναρωτηθεί πώς να **run OCR on image** αρχεία χωρίς να παλεύετε με χαμηλού επιπέδου APIs; Δεν είστε μόνοι. Σε πολλά έργα—επεξεργασία τιμολογίων, σάρωση αποδείξεων ή ψηφιοποίηση παλιών εγγράφων—η λήψη καθαρού, αναζητήσιμου κειμένου από μια εικόνα είναι το πρώτο, και συχνά το πιο δύσκολο, βήμα.

Σε αυτόν τον οδηγό θα περάσουμε από ένα πρακτικό παράδειγμα που όχι μόνο **run OCR on image** αλλά δείχνει επίσης πώς να **extract plain text from image** χρησιμοποιώντας τη μηχανή OCR της Aspose, και στη συνέχεια να βελτιώσουμε το αποτέλεσμα με έναν μικρό AI post‑processor. Στο τέλος θα έχετε ένα έτοιμο script, μια σαφή κατανόηση κάθε μέρους, και μερικές συμβουλές για να αποφύγετε κοινά προβλήματα.

![Run OCR on Image example](/images/run-ocr-on-image.png){: .align-center alt="Έξοδος κονσόλας Run OCR on image που δείχνει το αρχικό και το κείμενο βελτιωμένο από AI"}

## Τι θα χρειαστείτε

- Python 3.8+ εγκατεστημένο (ο κώδικας λειτουργεί σε Windows, macOS και Linux).
- Ένα ενεργό license Aspose OCR για Python ή μια δωρεάν δοκιμή (το πακέτο είναι `aspose-ocr` στο PyPI).
- Ένα δείγμα αρχείου εικόνας (π.χ., ένα σκαναρισμένο τιμολόγιο ή απόδειξη) αποθηκευμένο τοπικά.
- Προαιρετικά: ένα μηχάνημα με GPU αν σκοπεύετε να αλλάξετε τη ρύθμιση `gpu_layers` αργότερα.

Αυτό είναι όλο—χωρίς βαριές μηχανές OCR, χωρίς εξωτερικές κλήσεις σε cloud, μόνο μια εντολή pip install και μερικές γραμμές κώδικα.

## Βήμα 1: Εγκατάσταση του πακέτου Aspose OCR

Ανοίξτε ένα τερματικό και εκτελέστε:

```bash
pip install aspose-ocr
```

Το πακέτο φέρνει τη βασική μηχανή OCR μαζί με το ελαφρύ namespace `aspose.ocr` που θα χρησιμοποιούμε σε όλο τον οδηγό.

## Βήμα 2: Εισαγωγή των απαιτούμενων κλάσεων

Ξεκινάμε εισάγοντας τις δύο κύριες κλάσεις: `AsposeAI` για AI‑βελτιωμένη post‑processing και `OcrEngine` για την πραγματική εξαγωγή κειμένου.

```python
# Step 1: Import required classes
from aspose.ocr import AsposeAI, OcrEngine
```

*Γιατί είναι σημαντικό*: `OcrEngine` κάνει τη βαριά δουλειά της αναγνώρισης γλύφων, ενώ το `AsposeAI` μας επιτρέπει να ενσωματώσουμε προσαρμοσμένη λογική—όπως η κεφαλοποίηση κάθε λέξης—χωρίς να ξαναγράψουμε τον πυρήνα OCR.

## Βήμα 3: Δημιουργία ενός αντικειμένου AsposeAI (Προαιρετικός Logger)

Αν θέλετε λεπτομερή καταγραφή, μπορείτε να περάσετε έναν προσαρμοσμένο logger, αλλά η προεπιλογή λειτουργεί καλά στις περισσότερες περιπτώσεις.

```python
# Step 2: Create an AsposeAI instance (optional custom logger can be supplied)
ai = AsposeAI()
```

## Βήμα 4: Ρύθμιση του υποκείμενου μοντέλου (Προαιρετικό)

Το Aspose OCR έρχεται με ένα προεπιλεγμένο μοντέλο γλώσσας, αλλά μπορείτε να το κατευθύνετε σε ένα αποθετήριο HuggingFace ή να εξαναγκάσετε την εκτέλεση σε CPU. Παρακάτω ενεργοποιούμε αυτόματες λήψεις και επιλέγουμε το μικρό μοντέλο `gpt2`—απλώς για να δείξουμε τις ρυθμίσεις που μπορείτε να προσαρμόσετε.

```python
# Step 3: (Optional) Adjust the underlying model configuration
ai.config.allow_auto_download = "true"          # permit automatic model download
ai.config.hugging_face_repo_id = "openai/gpt2"   # specify the HuggingFace model
ai.config.gpu_layers = 0                        # force CPU execution
```

> **Συμβουλή:** Αν έχετε GPU με υποστήριξη CUDA, αυξήστε το `gpu_layers` σε `1` ή `2` για αξιοσημείωτη αύξηση ταχύτητας.

## Βήμα 5: Καταχώρηση ενός απλού Post‑Processor

Στόχος μας είναι να **extract plain text from image** και στη συνέχεια να το κάνουμε πιο ωραίο. Εδώ είναι μια μικρή συνάρτηση που κεφαλοποιεί κάθε λέξη. Μπορείτε να την αντικαταστήσετε με ορθογραφικό έλεγχο, ανίχνευση γλώσσας ή ακόμη και μια πλήρη κλήση LLM.

```python
# Step 4: Register a simple post‑processor that capitalizes each word
def capitalize_words(text, settings):
    """Capitalize every word in the OCR output."""
    return " ".join(word.capitalize() for word in text.split())

# Attach the processor to the AsposeAI instance
ai.set_post_processor(capitalize_words, custom_settings={})
```

Το λεξικό `custom_settings` σας επιτρέπει να περάσετε επιπλέον παραμέτρους αργότερα—χρήσιμο όταν εξελίσσετε τον επεξεργαστή.

## Βήμα 6: Φόρτωση εικόνας και εκτέλεση OCR

Τώρα τελικά **run OCR on image**. Θα λάβουμε δύο τύπους εξόδου:

1. **Plain text** – μια ακατέργαστη συμβολοσειρά χωρίς πληροφορίες διάταξης.
2. **Structured text** – διάταξη‑συνειδητή, διατηρώντας στήλες και πίνακες.

```python
# Step 5: Load an image and obtain OCR results (plain and layout‑aware)
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

plain_text = ocr_engine.recognize()                     # raw text
structured_text = ocr_engine.recognize_structured()    # layout‑aware text
```

> **Γιατί και τα δύο;** `plain_text` είναι τέλειο για γρήγορες αναζητήσεις, ενώ το `structured_text` ξεχωρίζει όταν χρειάζεται να ξαναδημιουργήσετε πίνακες ή να διατηρήσετε την ευθυγράμμιση των στηλών.

## Βήμα 7: Βελτίωση των αποτελεσμάτων OCR με τον AI Post‑Processor

Με τα αποτελέσματα OCR στα χέρια, τα περνάμε στο `AsposeAI.run_postprocessor`. Εδώ εκτελείται η προηγούμενη συνάρτηση `capitalize_words`.

```python
# Step 6: Enhance the OCR outputs using the AI post‑processor
enhanced_plain = ai.run_postprocessor(plain_text)
enhanced_structured = ai.run_postprocessor(structured_text)
```

Αν αποφασίσετε αργότερα να αντικαταστήσετε το post‑processor με κάτι πιο εξελιγμένο—π.χ. έναν διορθωτή γραμματικής—απλώς αντικαταστήστε τη συνάρτηση στο βήμα 5 και το υπόλοιπο του pipeline παραμένει το ίδιο.

## Βήμα 8: Προβολή των αποτελεσμάτων

Ας εκτυπώσουμε τα πάντα πλάι‑πλάι ώστε να μπορείτε να συγκρίνετε το ακατέργαστο OCR με την έκδοση βελτιωμένη από AI.

```python
# Step 7: Display original and enhanced texts
print("Original plain text:", plain_text)
print("AI‑enhanced plain text:", enhanced_plain)

print("\nOriginal structured text:", structured_text)
print("AI‑enhanced structured text:", enhanced_structured)
```

### Αναμενόμενη έξοδος

```
Original plain text: invoice #12345 date 01/02/2024 total $123.45
AI‑enhanced plain text: Invoice #12345 Date 01/02/2024 Total $123.45

Original structured text: invoice #12345
date 01/02/2024
total $123.45
AI‑enhanced structured text: Invoice #12345
Date 01/02/2024
Total $123.45
```

Παρατηρήστε πώς ο AI post‑processor μετατρέπει τις λέξεις με όλα τα γράμματα μικρά σε κεφαλαίες, κάνοντας το κείμενο πολύ πιο ευανάγνωστο. Μπορείτε να εφαρμόσετε οποιαδήποτε μετατροπή θέλετε—αυτό είναι μόνο μια απόδειξη της ιδέας.

## Βήμα 9: Εκκαθάριση πόρων

Το Aspose φορτώνει βαριά αρχεία μοντέλων στη μνήμη. Όταν τελειώσετε, ελευθερώστε τα για να αποφύγετε διαρροές μνήμης, ειδικά σε υπηρεσίες που τρέχουν για μεγάλο χρονικό διάστημα.

```python
# Step 8: Release model resources when done
ai.free_resources()
```

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

| Ερώτηση | Απάντηση |
|----------|--------|
| **Μπορώ να εκτελέσω OCR σε πολλαπλές εικόνες σε βρόχο;** | Απόλυτα. Απλώς δημιουργήστε μια φορά το `OcrEngine`, καλέστε `load_image` μέσα στον βρόχο, και επαναχρησιμοποιήστε το ίδιο αντικείμενο `AsposeAI` για post‑processing. |
| **Τι γίνεται αν η εικόνα είναι χαμηλής ανάλυσης;** | Προεπεξεργαστείτε με OpenCV (π.χ., `cv2.resize` και `cv2.threshold`) πριν τη δώσετε στο `OcrEngine`. |
| **Χρειάζομαι GPU;** | Δεν είναι απαραίτητο. Η προεπιλεγμένη λειτουργία CPU λειτουργεί καλά για τα περισσότερα έγγραφα. Ορίστε `ai.config.gpu_layers` > 0 μόνο αν έχετε συμβατό GPU και χρειάζεστε ταχύτητα. |
| **Πώς να εξάγετε plain text from image σε άλλες γλώσσες;** | Αλλάξτε `ocr_engine.language = "fr"` (ή οποιονδήποτε κωδικό ISO‑639‑1) πριν καλέσετε `recognize`. Ο ίδιος post‑processor θα λειτουργεί ακόμα, αλλά ίσως χρειαστεί λογική ειδική για τη γλώσσα. |

## Πλήρες Λειτουργικό Script

Συνδυάζοντας όλα, εδώ είναι το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα:

```python
# Full script: run OCR on image, extract plain text, and apply AI post‑processing

from aspose.ocr import AsposeAI, OcrEngine

# 1️⃣ Initialize AsposeAI
ai = AsposeAI()
ai.config.allow_auto_download = "true"
ai.config.hugging_face_repo_id = "openai/gpt2"
ai.config.gpu_layers = 0   # set >0 for GPU

# 2️⃣ Register post‑processor (capitalizes each word)
def capitalize_words(text, settings):
    return " ".join(word.capitalize() for word in text.split())

ai.set_post_processor(capitalize_words, custom_settings={})

# 3️⃣ Load image and run OCR
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

plain_text = ocr_engine.recognize()
structured_text = ocr_engine.recognize_structured()

# 4️⃣ Enhance outputs
enhanced_plain = ai.run_postprocessor(plain_text)
enhanced_structured = ai.run_postprocessor(structured_text)

# 5️⃣ Print results
print("Original plain text:", plain_text)
print("AI‑enhanced plain text:", enhanced_plain)

print("\nOriginal structured text:", structured_text)
print("AI‑enhanced structured text:", enhanced_structured)

# 6️⃣ Clean up
ai.free_resources()
```

Αποθηκεύστε το ως `run_ocr_on_image.py`, αντικαταστήστε τη διαδρομή placeholder με την πραγματική εικόνα σας, και εκτελέστε `python run_ocr_on_image.py`. Θα πρέπει να δείτε την έξοδο πριν/μετά όπως στο παραπάνω παράδειγμα.

## Συμπέρασμα

Έχουμε εκτελέσει με επιτυχία **run OCR on image** αρχεία χρησιμοποιώντας το Aspose OCR, δείξαμε πώς να **extract plain text from image**, και παρουσιάσαμε έναν ελαφρύ τρόπο να βελτιώσετε την αναγνωσιμότητα με έναν AI post‑processor. Το βασικό μοτίβο—OCR

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετικό θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή κειμένου από εικόνα με Aspose OCR – Οδηγός βήμα‑βήμα](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Εξαγωγή κειμένου από εικόνα – Βελτιστοποίηση OCR με Aspose.OCR για .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}