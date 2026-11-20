---
category: general
date: 2026-11-20
description: Εκτελέστε OCR σε εικόνα με το Aspose OCR και, στη συνέχεια, εξάγετε κείμενο
  από την εικόνα χρησιμοποιώντας τον ενσωματωμένο AI επεξεργαστή. Μάθετε μια πλήρη
  ροή εργασίας Python σε λίγα λεπτά.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from image
language: el
lastmod: 2026-11-20
og_description: Εκτελέστε OCR σε εικόνα με το Aspose OCR, στη συνέχεια εξάγετε το
  κείμενο από την εικόνα μέσω AI επεξεργασίας μετά. Ακολουθήστε αυτόν τον βήμα‑βήμα
  οδηγό Python.
og_image_alt: Diagram showing how to perform OCR on image and extract text from image
  using Aspose
og_title: Εκτελέστε OCR σε εικόνα και εξάγετε κείμενο από την εικόνα χρησιμοποιώντας
  το Aspose
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: Perform OCR on image with Aspose OCR and then extract text from image
    using the built‑in AI post‑processor. Learn a complete Python workflow in minutes.
  headline: Perform OCR on image and extract text from image with Aspose
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- AI post‑processing
title: Διενεργήστε OCR σε εικόνα και εξάγετε κείμενο από την εικόνα με το Aspose
url: /el/python/general/perform-ocr-on-image-and-extract-text-from-image-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε εικόνα και εξαγωγή κειμένου από εικόνα με το Aspose

Αν χρειάζεστε να **εκτελέσετε OCR σε εικόνα** αρχεία σε Python, αυτός ο οδηγός σας παρουσιάζει μια πλήρη λύση από άκρη σε άκρη. Χρησιμοποιώντας το Aspose OCR μαζί με τον επεξεργαστή μετά‑επεξεργασίας Aspose AI, μπορείτε αξιόπιστα **να εξάγετε κείμενο από εικόνα** αρχεία και να βελτιώσετε την ακατέργαστη έξοδο OCR με ένα ελαφρύ μοντέλο γλώσσας.

Σε αυτό το tutorial θα:

* Ρυθμίσετε τη μηχανή Aspose OCR.
* Εκτελέσετε OCR για **εξαγωγή κειμένου από εικόνα**.
* Προαιρετικά διαμορφώσετε ένα μοντέλο AI για μετά‑επεξεργασία.
* Καταχωρήσετε μια προσαρμοσμένη συνάρτηση μετά‑επεξεργασίας.
* Παραγάγετε βελτιωμένο κείμενο και καθαρίσετε τους πόρους.

Τα βήματα λειτουργούν με οποιαδήποτε raster εικόνα (PNG, JPEG, BMP) και απαιτούν μόνο το πακέτο `aspose-ocr`.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|------------------------|
| Python 3.8+ | Απαιτείται από το Aspose SDK. |
| `aspose-ocr` pip package | Παρέχει `AsposeOCR`, `AsposeAI` και κλάσεις διαμόρφωσης μοντέλου. |
| Ένα αρχείο εικόνας (π.χ., `sample_image.png`) | Η πηγή στην οποία θα **εκτελέσετε OCR σε εικόνα**. |
| Προαιρετικά: υποστήριξη GPU | Αν σκοπεύετε να εκτελέσετε ένα μεγαλύτερο μοντέλο σε GPU, ορίστε το `gpu_layers` αναλόγως. |

Install the SDK with:

```bash
pip install aspose-ocr
```

## Βήμα 1: Εκτέλεση OCR σε εικόνα

Η πρώτη ενέργεια είναι η ανάγνωση της εικόνας και η λήψη ακατέργαστου κειμένου. Αυτό είναι το κύριο βήμα **εκτέλεσης OCR σε εικόνα**.

```python
from aspose.ocr import AsposeOCR

# Initialise the OCR engine
ocr_engine = AsposeOCR()

# Path to the image you want to process
image_path = "YOUR_DIRECTORY/sample_image.png"

# Execute OCR – this returns the plain text extracted from the image
raw_text = ocr_engine.recognize_image(image_path)

print("Raw OCR result:")
print(raw_text)
```

**Γιατί λειτουργεί:** `AsposeOCR.recognize_image` εκτελεί ένα προ‑εκπαιδευμένο μοντέλο οπτικής αναγνώρισης χαρακτήρων που είναι βελτιστοποιημένο για ταχύτητα και ακρίβεια σε κοινές γραμματοσειρές. Η μέθοδος επιστρέφει μια απλή συμβολοσειρά Unicode, η οποία αποτελεί τη βάση για οποιαδήποτε περαιτέρω επεξεργασία.

> **Συμβουλή:** Εάν η εικόνα περιέχει πολλαπλές γλώσσες, ορίστε `ocr_engine.language = "eng+spa"` (ή οποιονδήποτε υποστηριζόμενο κωδικό ISO‑639‑2) πριν καλέσετε το `recognize_image`.

## Βήμα 2: Αρχικοποίηση του AI post‑processor

Το Aspose AI παρέχει ένα ελαφρύ επίπεδο μετά‑επεξεργασίας που μπορεί να καθαρίσει τα σφάλματα OCR, να διορθώσει την στίξη ή να εφαρμόσει προσαρμοσμένη επιχειρηματική λογική.

```python
from aspose.ocr import AsposeAI

# Initialise the AI post‑processor with default logging
ai_processor = AsposeAI()
```

**Γιατί το χρειάζεστε:** Η ακατέργαστη έξοδος OCR συχνά αναγνωρίζει λανθασμένα χαρακτήρες (π.χ., “0” vs “O”). Το βήμα AI βελτιώνει την έξοδο, καθιστώντας το αποτέλεσμα **εξαγωγής κειμένου από εικόνα** πιο αξιόπιστο για επόμενες εργασίες όπως η ευρετηρίαση ή η ανάλυση.

## Βήμα 3: (Προαιρετικό) Διαμόρφωση του AI μοντέλου

Μπορείτε να κατευθύνετε τον επεξεργαστή σε ένα συγκεκριμένο μοντέλο Hugging Face, να ενεργοποιήσετε αυτόματες λήψεις ή να εξαναγκάσετε εκτέλεση σε CPU. Αυτό το βήμα είναι προαιρετικό αλλά χρήσιμο όταν θέλετε ντετερμινιστική συμπεριφορά.

```python
from aspose.ocr import AsposeAIModelConfig

# Create a configuration object
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"          # Download model if missing
model_config.hugging_face_repo_id = "openai/gpt2"   # Small, fast model
model_config.gpu_layers = 0                        # Use CPU; set >0 for GPU

# Apply the configuration to the AI processor
ai_processor.configure(model_config)
```

**Εξήγηση:**  
* `allow_auto_download` σας εξοικονομεί τη διαχείριση μοντέλων με το χέρι.  
* `hugging_face_repo_id` επιλέγει ένα μοντέλο· `gpt2` είναι μια καλή ισορροπία μεταξύ μεγέθους και ποιότητας για διόρθωση σύντομου κειμένου.  
* `gpu_layers` ελέγχει πόσες στρώσεις transformer εκτελούνται στο GPU· `0` εξαναγκάζει καθαρή εκτέλεση σε CPU, η οποία είναι ασφαλής σε όλα τα μηχανήματα.

## Βήμα 4: Καταχώρηση προσαρμοσμένης συνάρτησης μετά‑επεξεργασίας

Το Aspose AI σας επιτρέπει να ενσωματώσετε οποιοδήποτε callable που λαμβάνει τη ακατέργαστη συμβολοσειρά OCR και επιστρέφει μια μετασχηματισμένη έκδοση. Παρακάτω είναι ένα απλό παράδειγμα που μετατρέπει όλα σε κεφαλαία.

```python
def my_post_processor(text):
    """
    Custom post‑processor that transforms the OCR result.
    Replace this logic with your own business rules.
    """
    return text.upper()

# Register the function with the AI processor
ai_processor.set_post_processor(my_post_processor, custom_settings=None)
```

**Πότε να προσαρμόσετε:** Χρησιμοποιήστε μια προσαρμοσμένη συνάρτηση όταν χρειάζεστε καθαρισμό ειδικό για το πεδίο, όπως αφαίρεση εμπιστευτικών αναγνωριστικών, κανονικοποίηση ημερομηνιών ή εφαρμογή διορθώσεων βάσει regex. Το μοντέλο AI θα εκτελεστεί *μετά* από αυτή τη συνάρτηση, επιτρέποντάς σας να συνδυάσετε ντετερμινιστικούς κανόνες με πιθανοκρατικές βελτιώσεις.

## Βήμα 5: Βελτίωση του αποτελέσματος OCR χρησιμοποιώντας τον AI post‑processor

Τώρα εκτελέστε ολόκληρη τη διαδικασία: το ακατέργαστο κείμενο OCR περνά πρώτα από τη δική σας προσαρμοσμένη συνάρτηση, μετά από το μοντέλο AI, και τελικά λαμβάνετε την βελτιωμένη έξοδο.

```python
# Run the AI post‑processor on the raw OCR text
enhanced_text = ai_processor.run_postprocessor(raw_text)

print("\nOriginal OCR :")
print(raw_text)
print("\nAI‑enhanced   :")
print(enhanced_text)
```

**Τι θα πρέπει να δείτε:**  
Αν η αρχική εικόνα περιείχε “Hello world”, η κονσόλα μπορεί να εμφανίσει:

```
Original OCR :
Hello world

AI‑enhanced   :
HELLO WORLD
```

Σε πραγματικό σενάριο, το μοντέλο AI θα διορθώσει ορθογραφικά λάθη, θα προσθέσει ελλείπουσες σημεία στίξης ή θα επαναμορφοποιήσει τις αλλαγές γραμμής, παρέχοντάς σας ένα πιο καθαρό αποτέλεσμα **εξαγωγής κειμένου από εικόνα** έτοιμο για αποθήκευση ή ανάλυση.

## Βήμα 6: Απελευθέρωση πόρων όταν ολοκληρωθεί

Τanto η μηχανή OCR όσο και ο AI post‑processor εκχωρούν εγγενείς πόρους. Η ρητή απελευθέρωσή τους αποτρέπει διαρροές μνήμης, ειδικά σε υπηρεσίες που τρέχουν για μεγάλο χρονικό διάστημα.

```python
# Clean up native resources
ai_processor.free_resources()
```

Αν επίσης δημιουργήσατε το `ocr_engine` με ένα βαρύ backend, θα μπορούσατε να καλέσετε `ocr_engine.dispose()` (αν είναι διαθέσιμο) με τον ίδιο τρόπο.

## Συνηθισμένες παραλλαγές και ακραίες περιπτώσεις

| Κατάσταση | Συνιστώμενη προσαρμογή |
|-----------|------------------------|
| **Μεγάλα PDF με πολλές σελίδες** | Επανάληψη σε κάθε σελίδα, κλήση του `recognize_image` για κάθε rasterized σελίδα, και συγκέντρωση των αποτελεσμάτων. |
| **Περιβάλλον με ενεργοποιημένο GPU** | Ορίστε `model_config.gpu_layers` στον αριθμό των στρώσεων που θέλετε στο GPU (π.χ., `4`). Βεβαιωθείτε ότι οι οδηγοί CUDA είναι εγκατεστημένοι. |
| **Μη‑Αγγλικό κείμενο** | Αλλάξτε `ocr_engine.language` στον κατάλληλο κωδικό γλώσσας και, αν χρειάζεται, επιλέξτε ένα μοντέλο Hugging Face ειδικό για τη γλώσσα. |
| **Πολύ θορυβώδεις σκαναρίσματα** | Προεπεξεργαστείτε την εικόνα με OpenCV (αφαίρεση θορύβου, κατώφλι) πριν καλέσετε το `recognize_image`. |
| **Απαιτείται διατήρηση της αρχικής κεφαλαιοποίησης** | Αντικαταστήστε τη συνάρτηση `my_post_processor` με μια λειτουργία no‑op ή έναν πιο λεπτομερή κανόνα αντί για `text.upper()`. |

## Πλήρες λειτουργικό παράδειγμα

Συνδυάζοντας όλα, εδώ είναι ένα ενιαίο script που μπορείτε να εκτελέσετε όπως είναι (αντικαταστήστε το `YOUR_DIRECTORY/sample_image.png` με το πραγματικό σας μονοπάτι αρχείου):

```python
from aspose.ocr import AsposeOCR, AsposeAI, AsposeAIModelConfig

# 1️⃣ Perform OCR on image
ocr_engine = AsposeOCR()
image_path = "YOUR_DIRECTORY/sample_image.png"
raw_text = ocr_engine.recognize_image(image_path)

# 2️⃣ Initialise the AI post‑processor
ai_processor = AsposeAI()

# 3️⃣ (Optional) Configure the AI model
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "openai/gpt2"
model_config.gpu_layers = 0            # CPU execution
ai_processor.configure(model_config)

# 4️⃣ Register a custom post‑processor (example: uppercase)
def my_post_processor(text):
    return text.upper()

ai_processor.set_post_processor(my_post_processor, custom_settings=None)

# 5️⃣ Enhance the OCR result
enhanced_text = ai_processor.run_postprocessor(raw_text)

print("Original OCR :", raw_text)
print("AI‑enhanced   :", enhanced_text)

# 6️⃣ Release resources
ai_processor.free_resources()
```

Η εκτέλεση αυτού του script εκτυπώνει τόσο την ακατέργαστη έξοδο OCR όσο και την έκδοση βελτιωμένη με AI, δείχνοντας πώς μπορείτε να **εκτελέσετε OCR σε εικόνα** αρχεία και αξιόπιστα **εξάγετε κείμενο από εικόνα** σε μια ενιαία, επαναλήψιμη ροή εργασίας.

## Συμπέρασμα

Τώρα ξέρετε πώς να **εκτελέσετε OCR σε εικόνα** αρχεία με το Aspose OCR, και στη συνέχεια **να εξάγετε κείμενο από εικόνα** χρησιμοποιώντας τον ενσωματωμένο AI post‑processor. Ο οδηγός κάλυψε:

* Αρχικοποίηση της μηχανής OCR.
* Εκτέλεση OCR για λήψη ακατέργαστου κειμένου.
* (Προαιρετικά) διαμόρφωση ενός ελαφρού μοντέλου Hugging Face.
* Προσθήκη ενός

## Τι Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετα χαρακτηριστικά API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή Κειμένου από Εικόνα με Aspose OCR & AI – Πλήρης Οδηγός Βήμα‑βήμα](/ocr/english/python/general/extract-text-image-with-aspose-ocr-ai-full-step-by-step-guid/)
- [Πώς να Διορθώσετε Σφάλματα OCR – Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Βήμα‑βήμα](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Εξαγωγή Κειμένου από Εικόνα Python – Πλήρης Οδηγός Aspose OCR](/ocr/english/python-java/general/extract-text-from-image-python-complete-aspose-ocr-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}