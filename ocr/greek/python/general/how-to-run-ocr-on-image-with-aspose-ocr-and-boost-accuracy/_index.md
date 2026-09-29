---
category: general
date: 2026-09-22
description: Μάθετε πώς να εκτελείτε OCR σε εικόνα χρησιμοποιώντας το Aspose OCR,
  να διαμορφώσετε το μοντέλο OCR, να εξάγετε κείμενο από τιμολόγιο και να βελτιώσετε
  την ακρίβεια του OCR σε Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- run OCR on image
- extract text from invoice
- improve OCR accuracy
- configure OCR model
language: el
lastmod: 2026-09-22
og_description: Εκτελέστε OCR σε εικόνα με το Aspose OCR, διαμορφώστε το μοντέλο OCR,
  εξάγετε κείμενο από τιμολόγιο και βελτιώστε την ακρίβεια του OCR σε ένα πλήρες,
  βήμα‑προς‑βήμα οδηγό.
og_image_alt: Screenshot showing raw OCR and AI‑enhanced text extracted from an invoice
  image
og_title: Εκτελέστε OCR σε εικόνα με το Aspose OCR – πλήρης οδηγός Python
schemas:
- author: Aspose
  dateModified: '2026-09-22'
  description: Learn how to run OCR on image using Aspose OCR, configure the OCR model,
    extract text from invoice and improve OCR accuracy in Python.
  headline: How to run OCR on image with Aspose OCR and boost accuracy
  type: TechArticle
tags:
- Aspose OCR
- Python
- AI post‑processing
title: Πώς να εκτελέσετε OCR σε εικόνα με το Aspose OCR και να βελτιώσετε την ακρίβεια
url: /el/python/general/how-to-run-ocr-on-image-with-aspose-ocr-and-boost-accuracy/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εκτελέσετε OCR σε εικόνα με το Aspose OCR και να βελτιώσετε την ακρίβεια

Εάν χρειάζεται να **εκτελέσετε OCR σε εικόνα** σε Python, αυτός ο οδηγός σας παρουσιάζει μια πλήρη, έτοιμη για παραγωγή ροή εργασίας. Θα δείτε πώς να ρυθμίσετε το μοντέλο OCR, να εξάγετε κείμενο από φωτογραφίες τιμολογίων και να βελτιώσετε την ακρίβεια του OCR με τον AI post‑processor της Aspose.

Η επεξεργασία σαρωμένων τιμολογίων είναι ένα συχνό πρόβλημα—το ακατέργαστο OCR συχνά επιστρέφει λανθασμένες λέξεις ή σπασμένους αριθμούς. Στο τέλος αυτού του tutorial θα έχετε ένα έτοιμο script που παρέχει πιο καθαρή, αξιόπιστη εξαγωγή κειμένου, και θα κατανοήσετε γιατί κάθε βήμα ρύθμισης είναι σημαντικό.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* Python 3.8 ή νεότερη έκδοση εγκατεστημένη.
* Ένα ενεργό άδεια Aspose OCR (η δωρεάν δοκιμή λειτουργεί για αξιολόγηση).
* Ένα δείγμα εικόνας τιμολογίου (π.χ., `sample_invoice.png`) τοποθετημένο σε γνωστό φάκελο.
* Βασική εξοικείωση με την εγκατάσταση πακέτων Python.

Δεν απαιτούνται πρόσθετες εξαρτήσεις σε επίπεδο συστήματος· το SDK διαχειρίζεται αυτόματα τις λήψεις μοντέλων.

## Βήμα 1: Εγκατάσταση του πακέτου Aspose OCR

Το πρώτο που πρέπει να κάνετε είναι να προσθέσετε τη βιβλιοθήκη Aspose OCR στο περιβάλλον σας. Το πακέτο περιλαμβάνει το AI μοντέλο και τον post‑processor που θα χρειαστείτε αργότερα.

```bash
pip install aspose-ocr
```

Η εκτέλεση αυτής της εντολής εγκαθιστά το `asposeocr`, το οποίο παρέχει την κλάση `AsposeAI` που χρησιμοποιείται για **ρύθμιση παραμέτρων μοντέλου OCR** όπως αυτόματες λήψεις και εκτέλεση μόνο σε CPU.

## Βήμα 2: Ρύθμιση του μοντέλου OCR (προαιρετικό αλλά συνιστάται)

Η λεπτομερή ρύθμιση του μοντέλου βελτιώνει την ταχύτητα και την ακρίβεια, ειδικά όταν εκτελείτε OCR σε εικόνες τιμολογίων που περιέχουν πολλούς αριθμούς και ειδικούς χαρακτήρες. Ο παρακάτω κώδικας δείχνει τις πιο χρήσιμες ρυθμίσεις:

```python
import asposeocr as ocr   # import the Aspose OCR package

# Create an AsposeAI instance with default logging
ai = ocr.AsposeAI()

# Enable automatic model download, force CPU execution, and enlarge the context window
ai.allow_auto_download = "true"   # download missing model files automatically
ai.gpu_layers = 0                 # use CPU only – avoids GPU‑related errors on most machines
ai.context_size = 2048           # larger context improves correction quality
```

*Γιατί αυτές οι σημαίες;*  
* `allow_auto_download` διασφαλίζει ότι το μοντέλο OCR είναι διαθέσιμο ακόμη και σε νέο μηχάνημα.  
* `gpu_layers = 0` αφαιρεί την ανάγκη για GPU συμβατό με CUDA, το οποίο πολλοί προγραμματιστές δεν διαθέτουν.  
* `context_size` ελέγχει πόσες γύρω μονάδες (tokens) λαμβάνει υπόψη το AI κατά τη διόρθωση σφαλμάτων· ένα μεγαλύτερο παράθυρο συχνά **βελτιώνει την ακρίβεια του OCR** σε πυκνό κείμενο όπως τα τιμολόγια.

## Βήμα 3: Αρχικοποίηση της AI μηχανής

Η αρχικοποίηση επαληθεύει ότι τα αρχεία μοντέλου είναι έτοιμα και τα φορτώνει στη μνήμη. Η παράλειψη αυτού του βήματος μπορεί να οδηγήσει σε σφάλμα χρόνου εκτέλεσης όταν καλέσετε αργότερα τον post‑processor.

```python
# Initialise the AI engine – ensures the model is ready to use
if not ai.is_initialized():
    raise RuntimeError("AI engine failed to initialise")
```

Εάν η μηχανή αποτύχει, η εξαίρεση σας λέει ακριβώς πού συνέβη το πρόβλημα, εξοικονομώντας χρόνο εντοπισμού σφαλμάτων.

## Βήμα 4: Εκτέλεση του τυπικού OCR engine σε εικόνα

Τώρα μπορείτε να **εκτελέσετε OCR σε εικόνα**. Η κλάση `OcrEngine` πραγματοποιεί την ακατέργαστη εξαγωγή κειμένου χωρίς καμία AI‑βασισμένη διόρθωση.

```python
# Path to the invoice image you want to process
image_path = "YOUR_DIRECTORY/sample_invoice.png"

# Perform raw OCR
ocr_result = ocr.OcrEngine().recognize_image(image_path)
```

`ocr_result.text` περιέχει το απλό string που αναγνώρισε η μηχανή OCR. Σε ένα τυπικό τιμολόγιο, μπορεί να δείτε ελλιπείς ψηφία, λανθασμένη στίξη ή σπασμένες λέξεις.

## Βήμα 5: Εφαρμογή του AI post‑processor για βελτίωση της ακρίβειας OCR

Ο AI post‑processor της Aspose αναλύει το ακατέργαστο αποτέλεσμα και διορθώνει κοινά σφάλματα OCR (π.χ., “5um” → “Sum”). Η εκτέλεση αυτού του βήματος είναι το κλειδί για **βελτίωση της ακρίβειας OCR** σε οικονομικά έγγραφα.

```python
# Apply the AI post‑processor
cleaned_result = ai.run_postprocessor(ocr_result)
```

Ο post‑processor χρησιμοποιεί τη ρύθμιση που ορίσατε στο Βήμα 2, έτσι το μεγαλύτερο `context_size` συμβάλλει σε πιο αξιόπιστες διορθώσεις.

## Βήμα 6: Εξαγωγή κειμένου από το τιμολόγιο και εμφάνιση αποτελεσμάτων

Σε αυτό το σημείο έχετε δύο εκδόσεις του εξαγόμενου κειμένου: το ακατέργαστο OCR αποτέλεσμα και την έκδοση που βελτιώθηκε από το AI. Η εκτύπωση και των δύο σας επιτρέπει να επαληθεύσετε τη βελτίωση και επίσης να καταγράψετε τα αρχικά δεδομένα για σκοπούς ελέγχου.

```python
# Display both the raw and the AI‑enhanced text
print("=== Raw OCR ===")
print(ocr_result.text)

print("\n=== AI‑enhanced ===")
print(cleaned_result.text)
```

**Τυπική έξοδος**

```
=== Raw OCR ===
Inv0ice No: 12345
Date: 2023/09/15
Total Am0unt: $1,2O0.00

=== AI‑enhanced ===
Invoice No: 12345
Date: 2023/09/15
Total Amount: $1,200.00
```

Δείτε πώς το βήμα AI διόρθωσε τις εσφαλμένες εναλλαγές μηδέν‑ένα και διόρθωσε τη μορφοποίηση του ποσού—ακριβώς το είδος βελτίωσης που χρειάζεστε όταν **εξάγετε κείμενο από τιμολόγιο**.

## Βήμα 7: Απελευθέρωση πόρων

Τέλος, ελευθερώστε τους εγγενείς πόρους που χρησιμοποιεί η AI μηχανή. Αυτό είναι ιδιαίτερα σημαντικό σε υπηρεσίες που τρέχουν για μεγάλο χρονικό διάστημα ή σε batch jobs.

```python
# Release resources when finished
ai.free_resources()
```

Η παράλειψη αυτού του κλήσης μπορεί να οδηγήσει σε διαρροές μνήμης επειδή το υποκείμενο μοντέλο εκτελείται σε εγγενή κώδικα.

## Πλήρες script που μπορείτε να αντιγράψετε‑επικολλήσετε

Παρακάτω βρίσκεται το πλήρες, εκτελέσιμο πρόγραμμα που ενσωματώνει κάθε βήμα που περιγράφηκε παραπάνω. Αντικαταστήστε το `YOUR_DIRECTORY` με το πραγματικό μονοπάτι προς το αρχείο εικόνας σας.

```python
import asposeocr as ocr   # import the Aspose OCR package

# Step 1: Create an AsposeAI instance (default logging)
ai = ocr.AsposeAI()

# Step 2: (Optional) Tune the model configuration for this demo
#   • Enable automatic download of the model if missing
#   • Use CPU only (no GPU layers)
#   • Increase context size for better correction quality
ai.allow_auto_download = "true"
ai.gpu_layers = 0
ai.context_size = 2048

# Step 3: Initialise the AI engine – ensures the model is ready to use
if not ai.is_initialized():
    raise RuntimeError("AI engine failed to initialise")

# Step 4: Run the standard OCR engine on an image
image_path = "YOUR_DIRECTORY/sample_invoice.png"
ocr_result = ocr.OcrEngine().recognize_image(image_path)

# Step 5: Apply the AI post‑processor to improve the raw OCR output
cleaned_result = ai.run_postprocessor(ocr_result)

# Step 6: Display both the raw and the AI‑enhanced text
print("=== Raw OCR ===")
print(ocr_result.text)
print("\n=== AI‑enhanced ===")
print(cleaned_result.text)

# Step 7: Release resources when finished
ai.free_resources()
```

Αποθηκεύστε το ως `process_invoice.py` και τρέξτε:

```bash
python process_invoice.py
```

Θα πρέπει να δείτε το ακατέργαστο και το διορθωμένο κείμενο να εκτυπώνονται στην κονσόλα, επιβεβαιώνοντας ότι έχετε **εκτελέσει OCR σε εικόνα**, **ρυθμίσει το μοντέλο OCR** και **βελτιώσει την ακρίβεια OCR** για την εργασία εξαγωγής κειμένου από τιμολόγια.

## Συχνές ερωτήσεις και ειδικές περιπτώσεις

| Ερώτηση | Απάντηση |
|----------|--------|
| *Τι γίνεται αν το μοντέλο αποτύχει να κατέβει;* | Βεβαιωθείτε ότι το μηχάνημά σας έχει πρόσβαση στο διαδίκτυο και ότι η σημαία `allow_auto_download` είναι ορισμένη σε `"true"`. Μπορείτε επίσης να κατεβάσετε το μοντέλο χειροκίνητα από το portal της Aspose και να κατευθύνετε το `AsposeAI` στον τοπικό φάκελο μέσω `ai.model_path = "path/to/model"` |
| *Μπορώ να τρέξω αυτό σε GPU;* | Ναι. Ορίστε `ai.gpu_layers` σε θετικό ακέραιο (π.χ., `2`) και εγκαταστήστε τις κατάλληλες βιβλιοθήκες CUDA. Η εκτέλεση σε GPU επιταχύνει μεγάλες παρτίδες αλλά απαιτεί συμβατό GPU. |
| *Πώς επεξεργάζομαι πολλά τιμολόγια σε έναν φάκελο;* | Τυλίξτε τη βασική λογική σε βρόχο που διατρέχει το `os.listdir(folder)`. Θυμηθείτε να καλέσετε `ai.free_resources()` μόνο μετά το τέλος του βρόχου, όχι μετά από κάθε αρχείο, ώστε το μοντέλο να παραμείνει φορτωμένο. |
| *Είναι ο post‑processor ασφαλής για τιμολόγια μη‑Αγγλικών;* | Το προεπιλεγμένο μοντέλο είναι εκπαιδευμένο σε αγγλικό κείμενο. Για άλλες γλώσσες, κατεβάστε το αντίστοιχο language pack και ορίστε `ai.language = "fr"` (ή τον κατάλληλο κωδικό ISO). |
| *Τι γίνεται αν το αποτέλεσμα OCR είναι κενό;* | Επαληθεύστε ότι το `image_path` δείχνει σε μια αναγνώσιμη εικόνα και ότι το αρχείο δεν είναι κατεστραμμένο. Μπορείτε επίσης να αυξήσετε το `ai.context_size` για να δώσετε στο μοντέλο περισσότερο πλαίσιο σε χαμηλής ποιότητας σκαναρίσματα. |

## Επόμενα βήματα

Τώρα που μπορείτε να **εκτελέσετε OCR σε εικόνα** και αξιόπιστα **εξάγετε κείμενο από τιμολόγιο**, σκεφτείτε τις εξής επεκτάσεις:

* **Batch processing** – συνδυάστε το script με `multiprocessing` για να διαχειριστείτε χιλιάδες τιμολόγια παράλληλα.  
* **Επαλήθευση δεδομένων** – χρησιμοποιήστε κανονικές εκφράσεις για να ελέγξετε αριθμούς τιμολογίων, ημερομηνίες και χρηματικά ποσά μετά την εξαγωγή.  
* **Ενσωμάτωση με βάσεις δεδομένων** – αποθηκεύστε το καθαρό κείμενο απευθείας σε PostgreSQL ή MongoDB για επακόλουθη ανάλυση.  
* **Προσαρμοσμένη βελτιστοποίηση μοντέλου** – εάν διαθέτετε μεγάλο ιδιόκτητο σύνολο δεδομένων, εκπαιδεύστε ένα domain‑specific μοντέλο και κατευθύνετε το `ai.model_path` σε αυτό για ακόμη μεγαλύτερη ακρίβεια.

Δοκιμάζοντας αυτές τις ιδέες, θα μετατρέψετε ένα απλό demo OCR σε μια στιβαρή pipeline επεξεργασίας εγγράφων που πληροί τις απαιτήσεις παραγωγής.

---

*Τώρα γνωρίζετε πώς να εκτελείτε OCR σε εικόνες με το Aspose OCR, να ρυθμίζετε το μοντέλο OCR για βέλτιστη απόδοση και να βελτιώνετε την ακρίβεια OCR χρησιμοποιώντας τον AI post‑processor. Εφαρμόστε αυτά τα βήματα στις δικές σας ροές επεξεργασίας τιμολογίων και απολαύστε πιο καθαρή, αξιόπιστη εξαγωγή κειμένου.*


## Τι πρέπει να μάθετε στη συνέχεια;


Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας projects.

- [How to Run OCR on Invoices – Extract Text from Image with Python](/ocr/english/python/general/how-to-run-ocr-on-invoices-extract-text-from-image-with-pyth/)
- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Convert Image to Text: Extract Text from Image Using Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}