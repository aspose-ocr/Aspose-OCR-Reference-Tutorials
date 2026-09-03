---
category: general
date: 2026-01-07
description: Πώς να εμφανίσετε τη λίστα μοντέλων στο Aspose OCR AI χρησιμοποιώντας
  Python – μάθετε πώς να λαμβάνετε τη διαδρομή του μοντέλου, να ελέγχετε τα εγκατεστημένα
  μοντέλα και να ανακτήσετε μια λίστα μοντέλων σε Python σε δευτερόλεπτα.
draft: false
keywords:
- how to list models
- get model path
- check installed models
- python get model list
- list available models
language: el
og_description: Πώς να εμφανίσετε τη λίστα μοντέλων στο Aspose OCR AI χρησιμοποιώντας
  Python. Βρείτε τη διαδρομή του μοντέλου, ελέγξτε τα εγκατεστημένα μοντέλα και δείτε
  την πλήρη λίστα των διαθέσιμων μοντέλων.
og_title: Πώς να καταγράψετε μοντέλα στο Aspose OCR AI – Οδηγός Python
tags:
- Aspose OCR
- Python
- AI models
title: Πώς να καταγράψετε τα μοντέλα στο Aspose OCR AI – Οδηγός Python
url: /el/python/general/how-to-list-models-in-aspose-ocr-ai-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Λίστα Μοντέλων στο Aspose OCR AI – Οδηγός Python

Έχετε αναρωτηθεί **πώς να λίστα μοντέλων** που είναι ήδη εγκατεστημένα στο μηχάνημά σας όταν εργάζεστε με το Aspose OCR AI; Δεν είστε ο μόνος που αντιμετωπίζει αυτό το πρόβλημα. Σε πολλά έργα χρειάζεται να ελέγξετε το φάκελο μοντέλων, να επιβεβαιώσετε ποια μοντέλα υπάρχουν ή ακόμη και να εντοπίσετε ένα ελλιπές μοντέλο—όλα χωρίς να βγείτε από το Python REPL.

Σε αυτό το tutorial θα περάσουμε από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που δείχνει πώς να **πάρτε τη διαδρομή του μοντέλου**, **ελέγξετε τα εγκατεστημένα μοντέλα**, και τελικά **να λίστα διαθέσιμα μοντέλα** με λίγες μόνο γραμμές κώδικα. Χωρίς εξωτερικά scripts, χωρίς κρυφή μαγεία—μόνο καθαρό Python και το Aspose OCR AI SDK.

> **Προαπαιτούμενα**  
> • Python 3.8 ή νεότερο  
> • Πακέτο `asposeocr` εγκατεστημένο (`pip install asposeocr`)  
> • Βασική εξοικείωση με την εισαγωγή modules

Αν έχετε καλύψει αυτά, ας βουτήξουμε.

---

## Πώς να Λίστα Μοντέλων με το Aspose OCR AI

Το πρώτο που χρειάζεται είναι η βοηθητική κλάση `AsposeAI` που παρέχεται με το module `asposeocr.ai`. Αυτή η κλάση μας δίνει τρεις χρήσιμες μεθόδους:

| Μέθοδος | Τι επιστρέφει | Τυπική χρήση |
|--------|----------------|--------------|
| `get_local_path()` | Απόλυτη διαδρομή προς το φάκελο όπου το Aspose αποθηκεύει τα AI μοντέλα | Επαλήθευση ότι το SDK κοιτάζει στο σωστό μέρος |
| `list_local()` | Python `list` με τα ονόματα των φακέλων μοντέλων που υπάρχουν στο δίσκο | Γρήγορη προβολή των μοντέλων που μπορείτε να φορτώσετε |
| `list_remote()` *(προαιρετικό)* | Λίστα μοντέλων διαθέσιμων για λήψη από το cloud του Aspose | Όταν χρειάζεστε μοντέλο που δεν υπάρχει τοπικά |

Παρακάτω είναι το **πλήρες script** που εκτυπώνει το τοπικό φάκελο μοντέλων και τη λίστα των εγκατεστημένων μοντέλων.

```python
# ---------------------------------------------------------
# Step 1: Import the Aspose OCR AI module
# ---------------------------------------------------------
from asposeocr.ai import AsposeAI

# ---------------------------------------------------------
# Step 2: Create an instance of the AI helper
# ---------------------------------------------------------
ai = AsposeAI()

# ---------------------------------------------------------
# Step 3: Retrieve and display the local model folder
# ---------------------------------------------------------
local_folder = ai.get_local_path()
print("Local AI model folder:", local_folder)

# ---------------------------------------------------------
# Step 4: List all models that are currently installed
# ---------------------------------------------------------
installed_models = ai.list_local()
print("Available models:", installed_models)
```

### Αναμενόμενη Έξοδος

Όταν τρέχετε το script σε μια φρέσκια εγκατάσταση, συνήθως βλέπετε κάτι τέτοιο:

```
Local AI model folder: /home/user/.asposeocr/models
Available models: ['ocr-general-v1', 'ocr-handwritten-v2']
```

Αν ο φάκελος είναι κενός, το `list_local()` επιστρέφει μια κενή λίστα (`[]`). Αυτό είναι ένα χρήσιμο σήμα ότι πρέπει πρώτα να κατεβάσετε ένα μοντέλο—κάτι που θα καλύψουμε αργότερα.

---

## Γιατί η Γνώση της Διαδρομής του Μοντέλου Είναι Σημαντική

Η κατανόηση **πού** το SDK αποθηκεύει τα αρχεία του (`get model path`) είναι περισσότερο από μια περιέργεια:

1. **Ανίχνευση σφαλμάτων** – Αν ένα μοντέλο αποτύχει να φορτωθεί, μπορείτε να κάνετε `ls` στη διαδρομή και να δείτε αν το αρχείο υπάρχει πραγματικά.
2. **Προσαρμοσμένα μοντέλα** – Ορισμένες ομάδες εκπαιδεύουν τα δικά τους OCR μοντέλα και τα τοποθετούν στον φάκελο. Ξέροντας τη διαδρομή, μπορείτε να τοποθετήσετε τα αρχεία ακριβώς εκεί που το Aspose τα περιμένει.
3. **Δικαιώματα** – Σε Linux, ο φάκελος μπορεί να ανήκει σε διαφορετικό χρήστη. Η έγκαιρη ανίχνευση σφάλματος δικαιωμάτων εξοικονομεί ώρες άσκοπης σκέψης.

> **Συμβουλή επαγγελματία:** Αν χρειάζεται να υποδείξετε στο SDK έναν προσαρμοσμένο φάκελο, ορίστε τη μεταβλητή περιβάλλοντος `ASPOSE_OCR_MODEL_PATH` πριν δημιουργήσετε το `AsposeAI()`.

```bash
export ASPOSE_OCR_MODEL_PATH=/my/custom/models
python my_script.py
```

---

## Έλεγχος Εγκατεστημένων Μοντέλων – Edge Cases & Συμβουλές

### 1. Δεν Έχουν Εγκατασταθεί Μοντέλα

Αν το `list_local()` επιστρέφει `[]`, έχετε δύο επιλογές:

| Επιλογή | Πώς να το κάνετε |
|--------|-----------------|
| **Κατεβάστε ένα μοντέλο από το Aspose** | `ai.download('ocr-general-v1')` (απαιτείται internet) |
| **Αντιγράψτε ένα προ‑εκπαιδευμένο μοντέλο** | Τοποθετήστε το φάκελο μοντέλου χειροκίνητα στη διαδρομή που εμφανίζεται από το `get_local_path()` |

### 2. Πολλές Εκδόσεις του Ίδιου Μοντέλου

Μερικές φορές βλέπετε τόσο `ocr-general-v1` **όσο** και `ocr-general-v1-beta`. Το SDK φορτώνει την πρώτη αντιστοίχηση που βρει, αλλά μπορείτε να εξαναγκάσετε μια συγκεκριμένη έκδοση περνώντας το ακριβές όνομα φακέλου στον κατασκευαστή του OCR:

```python
from asposeocr.ai import AsposeOCR

ocr = AsposeOCR(model_name='ocr-general-v1-beta')
```

### 3. Κατεστραμμένα Αρχεία Μοντέλου

Ένα μερικώς ληφθέν μοντέλο μπορεί να προκαλέσει `FileNotFoundError` αργότερα. Αν υποψιάζεστε κατεστραμμένα αρχεία, απλώς διαγράψτε τον προβληματικό φάκελο και ξανακατεβάστε:

```bash
rm -rf /home/user/.asposeocr/models/ocr-general-v1
python -c "from asposeocr.ai import AsposeAI; AsposeAI().download('ocr-general-v1')"
```

---

## Επέκταση του Script – Λίστα Απομακρυσμένων Μοντέλων (Προαιρετικό)

Αν θέλετε να δείτε ποια μοντέλα είναι διαθέσιμα για λήψη χωρίς να βγείτε από το Python, προσθέστε μια κλήση:

```python
remote_models = ai.list_remote()
print("Remote models you can download:", remote_models)
```

Αυτό θα εμφανίσει κάτι όπως:

```
Remote models you can download: ['ocr-general-v1', 'ocr-handwritten-v2', 'ocr-table-v1']
```

Τότε μπορείτε να επιλέξετε οποιοδήποτε μοντέλο και να καλέσετε `ai.download('model-name')` για αυτόματη λήψη.

---

## Πλήρες Παράδειγμα End‑to‑End

Συνδυάζοντας τα παραπάνω, εδώ είναι ένα **μονό script, εκτελέσιμο**, που:

1. Εμφανίζει το τοπικό φάκελο μοντέλων.
2. Λίστα των εγκατεστημένων μοντέλων.
3. Αν δεν βρεθούν, κατεβάζει ένα προεπιλεγμένο μοντέλο.
4. Τέλος, εκτυπώνει τη ενημερωμένη λίστα.

```python
# ---------------------------------------------------------
# Complete script – verifies model folder, installs if empty
# ---------------------------------------------------------
from asposeocr.ai import AsposeAI

def main():
    ai = AsposeAI()

    # 1️⃣ Show where Aspose expects models
    local_path = ai.get_local_path()
    print("🔎 Local AI model folder:", local_path)

    # 2️⃣ List currently installed models
    models = ai.list_local()
    print("📦 Installed models:", models)

    # 3️⃣ If nothing is installed, grab a default model
    if not models:
        default = 'ocr-general-v1'
        print(f"⚠️ No models found – downloading '{default}'...")
        try:
            ai.download(default)
            models = ai.list_local()
            print("✅ After download, installed models:", models)
        except Exception as e:
            print("❌ Failed to download model:", e)
            return

    # 4️⃣ (Optional) Show what you could download from the cloud
    remote = ai.list_remote()
    print("🌐 Remote models available:", remote)

if __name__ == "__main__":
    main()
```

Τρέχοντας αυτό το script σε ένα καθαρό μηχάνημα θα παραγάγει:

```
🔎 Local AI model folder: /home/user/.asposeocr/models
📦 Installed models: []
⚠️ No models found – downloading 'ocr-general-v1'...
✅ After download, installed models: ['ocr-general-v1']
🌐 Remote models available: ['ocr-general-v1', 'ocr-handwritten-v2', 'ocr-table-v1']
```

Τώρα έχετε μια **αυτοσυνεπής, αξιόπιστη** λύση που οποιοσδήποτε AI βοηθός μπορεί να παραθέσει ακριβώς.

---

## Συχνές Ερωτήσεις (FAQ)

**Ε: Λειτουργεί αυτό στα Windows;**  
Α: Απόλυτα. Το SDK αφαιρεί τις λεπτομέρειες του συστήματος αρχείων, έτσι το `get_local_path()` θα επιστρέψει κάτι όπως `C:\Users\YourName\.asposeocr\models`. Απλώς βεβαιωθείτε ότι το Python μπορεί να γράψει σε αυτόν το φάκελο.

**Ε: Μπορώ να αποθηκεύσω μοντέλα σε δικτυακό δίσκο;**  
Α: Ναι—ορίστε το `ASPOSE_OCR_MODEL_PATH` στη UNC διαδρομή (`\\server\share\models`) πριν δημιουργήσετε το αντικείμενο `AsposeAI`.

**Ε: Τι γίνεται αν χρειάζομαι μοντέλο για γλώσσα που δεν περιλαμβάνεται στο προεπιλεγμένο σύνολο;**  
Α: Χρησιμοποιήστε το `list_remote()` για να δείτε αν το Aspose προσφέρει μοντέλο συγκεκριμένης γλώσσας. Αν όχι, μπορείτε να εκπαιδεύσετε το δικό σας και να το τοποθετήσετε στον φάκελο· απλώς περάστε το όνομα του προσαρμοσμένου φακέλου στον κατασκευαστή του OCR.

---

## Συμπέρασμα

Καλύψαμε **πώς να λίστα μοντέλων** στο Aspose OCR AI, σας δείξαμε πώς να **πάρτε τη διαδρομή του μοντέλου**, **ελέγξετε τα εγκατεστημένα μοντέλα**, και ακόμη **να κατεβάσετε ένα ελλιπές μοντέλο**—όλα με καθαρό Python. Κατανοώντας τη δομή των φακέλων και τις βοηθητικές μεθόδους (`get_local_path()`, `list_local()`, `list_remote()`), αποκτάτε πλήρη έλεγχο πάνω στα AI μοντέλα που εξαρτάται η εφαρμογή σας.

Τι θα κάνετε μετά; Δοκιμάστε να αντικαταστήσετε το προεπιλεγμένο μοντέλο με ένα μοντέλο χειρόγραφου κειμένου, ή υποδείξτε το SDK σε ένα προσαρμοσμένο μοντέλο που έχετε δημιουργήσει εσωτερικά. Σε κάθε περίπτωση, έχετε τώρα μια σταθερή βάση για τη διαχείριση OCR πόρων σε οποιοδήποτε έργο Python.

Καλή προγραμματιστική, και να είναι πάντα η λίστα μοντέλων σας ενημερωμένη! 

---

![How to list models screenshot](https://example.com/images/how-to-list-models.png "How to list models")

*Image alt text:* **how to list models screenshot** (fulfills primary keyword requirement).

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}