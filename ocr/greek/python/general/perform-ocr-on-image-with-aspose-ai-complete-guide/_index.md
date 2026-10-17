---
category: general
date: 2026-06-28
description: Εκτελέστε OCR σε εικόνα χρησιμοποιώντας το Aspose AI και εξάγετε απλό
  κείμενο από την εικόνα με λίγες μόνο γραμμές Python. Αναλυτικός οδηγός βήμα‑βήμα
  για γρήγορη ενσωμάτωση.
draft: false
keywords:
- perform OCR on image
- extract plain text from image
- Aspose AI OCR
- Python OCR tutorial
- spell‑check post‑processor
- OCR result handling
language: el
og_description: Διενεργήστε OCR σε εικόνα με το Aspose AI και εξάγετε εύκολα το απλό
  κείμενο από την εικόνα. Μάθετε τη πλήρη ροή εργασίας σε αυτόν τον σύντομο οδηγό.
og_title: Εκτελέστε OCR σε εικόνα με το Aspose AI – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Perform OCR on image using Aspose AI and extract plain text from image
    in just a few lines of Python. Step‑by‑step tutorial for fast integration.
  headline: Perform OCR on Image with Aspose AI – Complete Guide
  type: TechArticle
- questions:
  - answer: Aspose’s OCR engine works best with 300 dpi or higher. If you’re dealing
      with lower quality scans, consider pre‑processing the image (e.g., sharpening,
      binarisation) before feeding it to `engine.set_image`.
    question: What if the image is low‑resolution?
  - answer: Yes. Loop over a list of image files, re‑using the same `engine` and `ai`
      instances. Just remember to call `engine.set_image` for each new file.
    question: Can I process multiple pages?
  - answer: Only on the first run, when the AI model is downloaded. After that, everything
      runs offline from the cached directory you specified.
    question: Do I need an internet connection?
  - answer: 'Pass a language code in the options dictionary, e.g., `ai.set_post_processor(AIProcessor.SpellCheck,
      {"lang": "fr"})` for French.'
    question: How do I change the language of the spell‑check?
  type: FAQPage
tags:
- OCR
- Python
- Aspose
- AI
title: Εκτελέστε OCR σε εικόνα με το Aspose AI – Πλήρης οδηγός
url: /el/python/general/perform-ocr-on-image-with-aspose-ai-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Διεξαγωγή OCR σε Εικόνα με Aspose AI – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ πώς να **perform OCR on image** αρχεία χωρίς να παλεύετε με βαριές βιβλιοθήκες; Σε πολλές πραγματικές εφαρμογές χρειάζεται μόνο να εξάγετε το κείμενο από ένα σαρωμένο τιμολόγιο ή μια απόδειξη, και μετά ίσως να το καθαρίσετε με έναν ορθογραφικό ελεγκτή. Τα καλά νέα είναι ότι το Aspose AI κάνει αυτό παιγνίδι, και μπορείτε επίσης να **extract plain text from image** σε ένα ενιαίο, ευανάγνωστο script.

Σε αυτό το tutorial θα περάσουμε από ολόκληρη τη διαδικασία: φόρτωση εικόνας, εκτέλεση OCR, λήψη τόσο ακατέργαστων όσο και δομημένων αποτελεσμάτων, εφαρμογή του ενσωματωμένου post‑processor ορθογραφικού ελέγχου, και τελικά εκκαθάριση πόρων. Στο τέλος θα έχετε ένα έτοιμο προς εκτέλεση παράδειγμα Python που μπορείτε να ενσωματώσετε στο δικό σας έργο.

## Τι Θα Μάθετε

- Πώς να αρχικοποιήσετε τη μηχανή Aspose OCR και να της δώσετε ένα αρχείο εικόνας.  
- Η διαφορά μεταξύ εξόδου απλής συμβολοσειράς και ενός δομημένου `OcrResult` που διατηρεί τη διάταξη.  
- Πώς να συνδέσετε τη γέφυρα Aspose AI, να κατεβάσετε το μοντέλο αυτόματα και να το κατευθύνετε σε έναν προσαρμοσμένο φάκελο cache.  
- Χρήση του post‑processor ορθογραφικού ελέγχου για **extract plain text from image** με διορθωμένη ορθογραφία ενώ διατηρεί τα bounding boxes.  
- Συμβουλές βέλτιστων πρακτικών για την απελευθέρωση πόρων AI και την αποφυγή διαρροών μνήμης.  

Δεν απαιτείται προηγούμενη εμπειρία με το Aspose — απλώς ένα λειτουργικό περιβάλλον Python 3 και μια εικόνα της επιλογής σας. Ας ξεκινήσουμε.

![Παράδειγμα διεξαγωγής OCR σε εικόνα](image.png "Διάγραμμα που δείχνει τη ροή OCR – perform OCR on image")

## Βήμα 1 – Αρχικοποίηση της Μηχανής OCR και Φόρτωση της Εικόνας Σας

Το πρώτο πράγμα που πρέπει να κάνετε είναι να εκκινήσετε τη μηχανή OCR και να την κατευθύνετε στην εικόνα που θέλετε να διαβάσετε. Σκεφτείτε τη μηχανή ως έναν σαρωτή που μετατρέπει τα pixel σε χαρακτήρες.

```python
# Step 1: Initialise the OCR engine and load the image
engine = OcrEngine()
engine.set_image(Image.from_file("YOUR_DIRECTORY/invoice.png"))
```

> **Γιατί αυτό είναι σημαντικό:** `OcrEngine()` δημιουργεί μια νέα συνεδρία, ενώ το `set_image` λέει στη μηχανή ακριβώς ποιο αρχείο να αναλύσει. Αν παραλείψετε αυτό το βήμα, οι επόμενες κλήσεις `recognize` θα προκαλέσουν εξαίρεση επειδή δεν υπάρχει τίποτα προς επεξεργασία.

## Βήμα 2 – Εκτέλεση OCR και Λήψη Και των Απλών Και των Δομημένων Αποτελεσμάτων

Τώρα πραγματικά **perform OCR on image**. Το Aspose σας παρέχει δύο τύπους εξόδου:

1. `plain_text` – μια απλή συμβολοσειρά, ιδανική όταν χρειάζεστε μόνο τις λέξεις.  
2. `structured` – ένα αντικείμενο `OcrResult` που διατηρεί τις αλλαγές γραμμής, τα bounding boxes και άλλα μεταδεδομένα διάταξης.

```python
# Step 2: Perform OCR – obtain plain text and structured result
plain_text = engine.recognize()                # plain string
structured = engine.recognize_structured()    # OcrResult with layout info
```

> **Συμβουλή επαγγελματία:** Χρησιμοποιήστε το `plain_text` όταν σας ενδιαφέρουν μόνο οι χαρακτήρες (π.χ., αναζήτηση σε έγγραφο). Χρησιμοποιήστε το `structured` όταν χρειάζεται να αντιστοιχίσετε το κείμενο στην αρχική του θέση, όπως η επισήμανση σφαλμάτων στο αρχικό σκανάρισμα.

## Βήμα 3 – Αρχικοποίηση της Γέφυρας Aspose AI (Λήψη Μοντέλου στην Πρώτη Χρήση)

Το Aspose AI είναι ο εγκέφαλος που τροφοδοτεί τον post‑processor ορθογραφικού ελέγχου. Την πρώτη φορά που το εκτελείτε, το μοντέλο θα ληφθεί αυτόματα. Μπορείτε επίσης να παρέχετε έναν προσαρμοσμένο φάκελο για την προσωρινή αποθήκευση του μοντέλου, κάτι που επιταχύνει τις επόμενες εκτελέσεις.

```python
# Step 3: Initialise the Aspose AI bridge (model will be downloaded on first use)
# Optional: specify a custom directory for the cached model
ai_config = AsposeAIModelConfig()
ai_config.directory_model_path = "YOUR_DIRECTORY/models"
ai = AsposeAI(ai_config)
```

> **Γιατί αυτό είναι σημαντικό:** Η προσωρινή αποθήκευση του μοντέλου αποτρέπει επαναλαμβανόμενες κλήσεις δικτύου και διατηρεί την εφαρμογή σας ανταποκρινόμενη, ειδικά σε περιβάλλοντα παραγωγής.

## Βήμα 4 – Καταχώριση του Ενσωματωμένου Post‑Processor Ορθογραφικού Ελέγχου

Το Aspose παρέχει έναν χρήσιμο επεξεργαστή ορθογραφικού ελέγχου που λειτουργεί τόσο σε απλές συμβολοσειρές όσο και σε δομημένα αποτελέσματα OCR. Καταχωρίστε το μία φορά και είστε έτοιμοι να διορθώσετε τυχόν τυπογραφικά λάθη που προέρχονται από το OCR.

```python
# Step 4: Register the built‑in spell‑check post‑processor
ai.set_post_processor(AIProcessor.SpellCheck, {})
```

> **Σημείωση:** Το κενό λεξικό `{}` είναι το σημείο όπου μπορείτε να περάσετε προσαρμοσμένα λεξικά ή ρυθμίσεις γλώσσας αν χρειάζεστε περισσότερο έλεγχο.

## Βήμα 5 – Εφαρμογή Ορθογραφικού Ελέγχου στο Απλό Κείμενο OCR

Εδώ είναι που **extract plain text from image** και ταυτόχρονα διορθώνουμε τα ορθογραφικά λάθη. Η μέθοδος `run_postprocessor` παίρνει τη ακατέργαστη συμβολοσειρά και επιστρέφει μια καθαρή έκδοση.

```python
# Step 5: Apply spell‑check to the plain OCR text
corrected_text = ai.run_postprocessor(plain_text)
print("Corrected:", corrected_text)
```

**Αναμενόμενη έξοδος (παράδειγμα):**

```
Corrected: Invoice Number 2023‑07‑15
Date: 07/15/2023
Total Amount: $1,250.00
```

> **Γιατί αυτό είναι σημαντικό:** Οι μηχανές OCR συχνά αναγνωρίζουν λανθασμένα χαρακτήρες όπως “0” vs “O” ή “1” vs “l”. Το βήμα του ορθογραφικού ελέγχου διορθώνει αυτά, παρέχοντάς σας πιο καθαρά δεδομένα για επεξεργασία downstream.

## Βήμα 6 – Εφαρμογή Ορθογραφικού Ελέγχου στο Δομημένο Αποτέλεσμα OCR (Διατηρεί τα Bounding Boxes)

Αν χρειάζεται να διατηρήσετε την αρχική διάταξη — π.χ., για να επισημάνετε τις διορθωμένες λέξεις στο σαρωμένο έγγραφο — μπορείτε να περάσετε το δομημένο αποτέλεσμα στον ίδιο post‑processor. Το επιστρεφόμενο αντικείμενο εξακολουθεί να περιέχει πληροφορίες γραμμών.

```python
# Step 6: Apply spell‑check to the structured OCR result (preserves bounding boxes)
corrected_struct = ai.run_postprocessor(structured)
for line in corrected_struct.Lines:
    print(line.Text)
```

**Δειγματική έξοδος κονσόλας:**

```
Invoice Number 2023‑07‑15
Date: 07/15/2023
Total Amount: $1,250.00
```

> **Συμβουλή επαγγελματία:** Επειδή η συλλογή `Lines` διατηρεί τις συντεταγμένες `BoundingBox`, μπορείτε τώρα να επικάνατε το διορθωμένο κείμενο πάνω στην αρχική εικόνα χρησιμοποιώντας οποιαδήποτε βιβλιοθήκη γραφικών (Pillow, OpenCV, κλπ.).

## Βήμα 7 – Απελευθέρωση Πόρων AI Όταν Τελειώσετε

Οι διαρροές μνήμης είναι οι σιωπηλοί δολοφόνοι των μακροχρόνιων υπηρεσιών. Πάντα ελευθερώστε τους πόρους AI μόλις ολοκληρωθεί η εργασία.

```python
# Step 7: Release AI resources when done
ai.free_resources()
```

> **Γιατί αυτό είναι σημαντικό:** Η `free_resources()` κλείνει τα νήματα στο παρασκήνιο και καθαρίζει το μοντέλο από τη μνήμη, διατηρώντας την εφαρμογή σας ελαφριά.

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι το πλήρες script που μπορείτε να αντιγράψετε‑επικολλήσετε και να εκτελέσετε (απλώς αντικαταστήστε το `YOUR_DIRECTORY` με πραγματικές διαδρομές):

```python
from aspose.ocr import OcrEngine, Image
from aspose.ai import AsposeAI, AsposeAIModelConfig, AIProcessor

# Initialise OCR engine
engine = OcrEngine()
engine.set_image(Image.from_file("YOUR_DIRECTORY/invoice.png"))

# Perform OCR
plain_text = engine.recognize()
structured = engine.recognize_structured()

# Initialise Aspose AI bridge
ai_config = AsposeAIModelConfig()
ai_config.directory_model_path = "YOUR_DIRECTORY/models"
ai = AsposeAI(ai_config)

# Register spell‑check post‑processor
ai.set_post_processor(AIProcessor.SpellCheck, {})

# Correct plain text
corrected_text = ai.run_postprocessor(plain_text)
print("Corrected:", corrected_text)

# Correct structured result
corrected_struct = ai.run_postprocessor(structured)
for line in corrected_struct.Lines:
    print(line.Text)

# Clean up
ai.free_resources()
```

Εκτελέστε το script και θα δείτε την διορθωμένη έξοδο να εμφανίζεται στην κονσόλα. Αυτή είναι η πλήρης ροή εργασίας **perform OCR on image** από την αρχή μέχρι το τέλος.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

- **Τι γίνεται αν η εικόνα είναι χαμηλής ανάλυσης;**  
  Η μηχανή OCR του Aspose λειτουργεί καλύτερα με 300 dpi ή περισσότερο. Αν εργάζεστε με σαρώσεις χαμηλότερης ποιότητας, σκεφτείτε την προεπεξεργασία της εικόνας (π.χ., ενίσχυση, δυαδικοποίηση) πριν τη δώσετε στο `engine.set_image`.

- **Μπορώ να επεξεργαστώ πολλαπλές σελίδες;**  
  Ναι. Επανάληψη πάνω σε λίστα αρχείων εικόνας, επαναχρησιμοποιώντας τις ίδιες παρουσίες `engine` και `ai`. Απλώς θυμηθείτε να καλέσετε `engine.set_image` για κάθε νέο αρχείο.

- **Χρειάζομαι σύνδεση στο διαδίκτυο;**  
  Μόνο στην πρώτη εκτέλεση, όταν το μοντέλο AI κατεβαίνει. Μετά από αυτό, όλα τρέχουν offline από τον φάκελο cache που καθορίσατε.

- **Πώς αλλάζω τη γλώσσα του ορθογραφικού ελέγχου;**  
  Περάστε έναν κωδικό γλώσσας στο λεξικό επιλογών, π.χ., `ai.set_post_processor(AIProcessor.SpellCheck, {"lang": "fr"})` για τα Γαλλικά.

## Συμπέρασμα

Τώρα ξέρετε ακριβώς πώς να **perform OCR on image** αρχεία με το Aspose AI και πώς να **extract plain text from image** ενώ διορθώνετε αυτόματα τα κοινά σφάλματα OCR. Το tutorial κάλυψε την αρχικοποίηση της μηχανής, τα απλά vs δομημένα αποτελέσματα, την προσωρινή αποθήκευση του μοντέλου, την ενσωμάτωση του ορθογραφικού ελέγχου και τη σωστή εκκαθάριση πόρων.  

Από εδώ μπορείτε να εξερευνήσετε την προσθήκη προσαρμοσμένων λεξικών, την τροφοδοσία του διορθωμένου κειμένου σε μια downstream NLP pipeline, ή την απόδοση των bounding boxes πίσω στην αρχική σάρωση για οπτική επαλήθευση. Οι δυνατότητες είναι πολλές, και η βάση κώδικα που μόλις δημιουργήσατε είναι ένα σταθερό θεμέλιο.

Μη διστάσετε να πειραματιστείτε — αντικαταστήστε την εικόνα, τροποποιήστε τις ρυθμίσεις του post‑processor, ή συνδέστε επιπλέον μονάδες AI. Αν αντιμετωπίσετε πρόβλημα, αφήστε ένα σχόλιο παρακάτω· καλή κωδικοποίηση!

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Βήμα‑βήμα](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Πώς να Χρησιμοποιήσετε το Aspose OCR για Αποτέλεσμα JSON στην Αναγνώριση Εικόνας](/ocr/english/net/text-recognition/get-result-as-json/)
- [Αναγνώριση κειμένου εικόνας με Aspose OCR για πολλαπλές γλώσσες](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}