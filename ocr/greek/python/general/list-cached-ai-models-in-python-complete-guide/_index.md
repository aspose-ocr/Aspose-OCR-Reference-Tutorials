---
category: general
date: 2026-06-22
description: Μάθετε πώς να καταγράφετε τα αποθηκευμένα μοντέλα AI χρησιμοποιώντας
  το AI SDK σε Python. Περιλαμβάνει βήματα για την ανάκτηση του καταλόγου cache μοντέλων
  και τη διαχείριση των τοπικών μοντέλων AI αποδοτικά.
draft: false
keywords:
- list cached ai models
- retrieve model cache directory
- list local ai models
- ai sdk python
- manage ai model cache
language: el
og_description: Καταγράψτε τα αποθηκευμένα μοντέλα AI με Python χρησιμοποιώντας το
  AI SDK. Ακολουθήστε αυτόν τον βήμα‑βήμα οδηγό για να ανακτήσετε τον φάκελο cache
  μοντέλων και να διαχειριστείτε τα τοπικά μοντέλα AI.
og_title: Λίστα αποθηκευμένων μοντέλων AI σε Python – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to list cached AI models using the AI SDK in Python. Includes
    steps to retrieve model cache directory and manage local AI models efficiently.
  headline: List Cached AI Models in Python – Complete Guide
  type: TechArticle
- description: Learn how to list cached AI models using the AI SDK in Python. Includes
    steps to retrieve model cache directory and manage local AI models efficiently.
  name: List Cached AI Models in Python – Complete Guide
  steps:
  - name: Import the AI SDK
    text: '```python # Step 1: Import the AI SDK (replace with the actual package
      name if different) import ai ```'
  - name: List All Cached Models
    text: '```python # Step 2: List all models that are cached locally cached_models
      = ai.list_local() print("Cached models:", cached_models) ```'
  - name: Retrieve the Model Cache Directory
    text: '```python # Step 3: Retrieve the directory where the model files are stored
      cache_dir = ai.get_local_path() print("Model cache directory:", cache_dir) ```'
  - name: Empty Cache
    text: If `ai.list_local()` returns an empty list, you might wonder whether the
      SDK is misconfigured. Double‑check the environment variable `AI_CACHE_DIR` (or
      the SDK’s config file) to ensure it points to a writable location.
  - name: Permissions Issues
    text: When accessing `ai.get_local_path()`, a `PermissionError` can surface on
      restrictive systems. The fix is usually to run the script with appropriate user
      rights or to adjust the directory’s ACLs.
  - name: Version Mismatches
    text: 'Sometimes the cache contains an older version of a model while your code
      requests a newer one. The SDK will automatically download the newer version,
      but you can pre‑empt this by inspecting the version tag in the list:'
  - name: Cleaning Up Old Models
    text: 'If you need to free up space, you can delete a specific model folder directly:'
  type: HowTo
- questions:
  - answer: Yes. The SDK abstracts away OS‑specific paths, so `ai.get_local_path()`
      returns a valid string on Linux, macOS, and Windows.
    question: Does this work on all operating systems?
  - answer: The built‑in `list_local()` only reports locally stored artifacts. For
      remote registries you’d use `ai.list_remote()` (if your SDK version provides
      it).
    question: Can I list models from a remote cache?
  - answer: 'Replace the import line with the actual package name, e.g., `import myai
      as ai`. All subsequent calls stay the same because the API contract is consistent
      across implementations. --- ## Conclusion You now have a solid, production‑ready
      method to **list cached AI models** using the **AI SDK Python** '
    question: What if the SDK name isn’t `ai`?
  type: FAQPage
tags:
- python
- ai
- sdk
title: Λίστα αποθηκευμένων μοντέλων AI σε Python – Πλήρης οδηγός
url: /el/python/general/list-cached-ai-models-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Λίστα Αποθηκευμένων Μοντέλων AI σε Python – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ πώς να **καταγράψετε τα αποθηκευμένα μοντέλα AI** στον υπολογιστή σας χωρίς να ψάχνετε σε ακαταστασίες φακέλους; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν πρόβλημα όταν πρέπει να επαληθεύσουν ποια μοντέλα είναι ήδη αποθηκευμένα τοπικά, ειδικά όταν εργάζονται με περιορισμένο εύρος ζώνης ή σε εκδόσεις εκτός σύνδεσης. Σε αυτό το tutorial θα δείτε έναν γρήγορο, χωρίς περιττές λεπτομέρειες τρόπο να ερωτήσετε το AI SDK, να εκτυπώσετε τα περιεχόμενα της κρυφής μνήμης (cache) και να ανακαλύψετε ακριβώς πού βρίσκονται αυτά τα αρχεία.

Θα αγγίξουμε επίσης σχετικές θεματικές όπως **ανάκτηση του καταλόγου κρυφής μνήμης μοντέλων**, διαχείριση κενών caches, και βέλτιστες πρακτικές για **διαχείριση κρυφής μνήμης μοντέλων AI** σε παραγωγικά σενάρια. Στο τέλος θα έχετε ένα αυτόνομο απόσπασμα κώδικα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Python.

## Προαπαιτούμενα

Πριν προχωρήσουμε, βεβαιωθείτε ότι έχετε:

- Python 3.8 ή νεότερο εγκατεστημένο.
- Το AI SDK (το πακέτο `ai`) εγκατεστημένο μέσω `pip install ai-sdk` ή από το εσωτερικό αποθετήριο της οργάνωσής σας.
- Βασική εξοικείωση με την εκτέλεση σεναρίων από τη γραμμή εντολών.

Δεν απαιτούνται πρόσθετες βιβλιοθήκες, ώστε το παράδειγμα να παραμένει ελαφρύ και φορητό.

---

## Λίστα Αποθηκευμένων Μοντέλων AI – Γρήγορη Επισκόπηση

Το πρώτο βήμα είναι η εισαγωγή του SDK και η κλήση των βοηθητικών του συναρτήσεων. Το SDK εκθέτει δύο χρήσιμες μεθόδους:

1. `ai.list_local()` – επιστρέφει μια λίστα Python με τα αναγνωριστικά μοντέλων που είναι ήδη αποθηκευμένα.
2. `ai.get_local_path()` – επιστρέφει τον απόλυτο φάκελο όπου βρίσκονται τα αρχεία των μοντέλων.

Και οι δύο κλήσεις είναι συγχρονισμένες και εγείρουν ένα σαφές `AIError` εάν κάτι πάει στραβά, κάτι που κάνει τη διαχείριση σφαλμάτων απλή.

> **Γιατί να χρησιμοποιήσετε αυτές τις συναρτήσεις;**  
> Η γνώση του ακριβούς συνόλου των αποθηκευμένων μοντέλων σας επιτρέπει να αποφύγετε περιττές λήψεις, να εντοπίσετε διαφορές εκδόσεων και να καθαρίσετε παλιά αρχεία αυτόματα. Είναι ένα μικρό κομμάτι της μεγαλύτερης ροής εργασίας **AI SDK Python**, αλλά μπορεί να σας εξοικονομήσει ώρες χειροκίνητης αναζήτησης στο σύστημα αρχείων.

### Βήμα 1: Εισαγωγή του AI SDK

```python
# Step 1: Import the AI SDK (replace with the actual package name if different)
import ai
```

*Γιατί είναι σημαντικό:* Η εισαγωγή του πακέτου καταχωρεί τις υποκείμενες C‑extensions και φορτώνει αρχεία ρυθμίσεων (όπως διαδρομές cache) από το περιβάλλον σας. Η παράλειψη αυτού του βήματος θα εγείρει `ModuleNotFoundError` τη στιγμή που θα καλέσετε οποιαδήποτε συνάρτηση του SDK.

### Βήμα 2: Λίστα Όλων των Αποθηκευμένων Μοντέλων

```python
# Step 2: List all models that are cached locally
cached_models = ai.list_local()
print("Cached models:", cached_models)
```

**Τι θα δείτε:** Εάν έχετε τρία μοντέλα αποθηκευμένα, η έξοδος μπορεί να μοιάζει με:

```
Cached models: ['gpt-4-mini', 'bert-base-uncased', 'stable-diffusion-v1']
```

Εάν η κρυφή μνήμη είναι κενή, θα λάβετε μια κενή λίστα:

```
Cached models: []
```

> **Συμβουλή επαγγελματία:** Τυλίξτε την κλήση σε μπλοκ try/except εάν υποψιάζεστε ότι το SDK μπορεί να μην έχει αρχικοποιηθεί σωστά.

```python
try:
    cached_models = ai.list_local()
except ai.AIError as e:
    print("Failed to list cached models:", e)
    cached_models = []
```

### Βήμα 3: Ανάκτηση του Καταλόγου Κρυφής Μνήμης Μοντέλων

```python
# Step 3: Retrieve the directory where the model files are stored
cache_dir = ai.get_local_path()
print("Model cache directory:", cache_dir)
```

Τυπική έξοδος σε σύστημα τύπου Unix:

```
Model cache directory: /home/you/.cache/ai/models
```

Σε Windows μπορεί να δείτε κάτι όπως `C:\Users\you\AppData\Local\ai\models`. Η γνώση αυτής της διαδρομής είναι ουσιώδης όταν χρειάζεται να **διαχειριστείτε την κρυφή μνήμη μοντέλων AI** χειροκίνητα—π.χ. για να διαγράψετε παλιές εκδόσεις ή να αντιγράψετε αρχεία σε κοινόχρηστο δίσκο.

---

## Οπτική Σύνοψη

![Διάγραμμα που δείχνει πώς να καταγράψετε αποθηκευμένα μοντέλα AI, να ανακτήσετε τα ονόματά τους και να εντοπίσετε τον φάκελο cache](https://example.com/images/list-cached-ai-models.png)

*Κείμενο εναλλακτικής περιγραφής:* Διάγραμμα που απεικονίζει τη διαδικασία **καταγραφής αποθηκευμένων μοντέλων AI** χρησιμοποιώντας το AI SDK σε Python.

---

## Διαχείριση Ακραίων Περιπτώσεων και Συνηθισμένων Παγίδων

### Κενή Κρυφή Μνήμη

Εάν το `ai.list_local()` επιστρέφει κενή λίστα, μπορεί να αναρωτηθείτε αν το SDK είναι λανθασμένα ρυθμισμένο. Ελέγξτε τη μεταβλητή περιβάλλοντος `AI_CACHE_DIR` (ή το αρχείο ρυθμίσεων του SDK) ώστε να δείχνει σε μια εγγράψιμη θέση.

```python
if not cached_models:
    print("No models are cached. Consider downloading a model first.")
```

### Προβλήματα Δικαιωμάτων

Κατά την πρόσβαση στο `ai.get_local_path()`, μπορεί να εμφανιστεί `PermissionError` σε περιορισμένα συστήματα. Η λύση είναι συνήθως η εκτέλεση του σεναρίου με τα κατάλληλα δικαιώματα χρήστη ή η ρύθμιση των ACL του φακέλου.

### Ασυμφωνίες Εκδόσεων

Μερικές φορές η κρυφή μνήμη περιέχει παλαιότερη έκδοση μοντέλου ενώ ο κώδικάς σας ζητά νεότερη. Το SDK θα κατεβάσει αυτόματα τη νεότερη έκδοση, αλλά μπορείτε να το προλάβετε ελέγχοντας την ετικέτα έκδοσης στη λίστα:

```python
for model in cached_models:
    if "v2" not in model:
        print(f"Model {model} may be outdated.")
```

### Καθαρισμός Παλαιών Μοντέλων

Εάν χρειάζεται να ελευθερώσετε χώρο, μπορείτε να διαγράψετε απευθείας έναν συγκεκριμένο φάκελο μοντέλου:

```python
import shutil, os

def purge_model(model_name):
    path = os.path.join(cache_dir, model_name)
    if os.path.isdir(path):
        shutil.rmtree(path)
        print(f"Purged {model_name} from cache.")
    else:
        print(f"{model_name} not found in cache.")
```

Η εκτέλεση `purge_model('bert-base-uncased')` θα αφαιρέσει εκείνο το μοντέλο και θα ελευθερώσει χώρο στο δίσκο.

---

## Πλήρες Σενάριο που Μπορείτε να Αντιγράψετε‑Κολλήσετε

Παρακάτω υπάρχει ένα έτοιμο‑για‑εκτέλεση σενάριο που συνδυάζει όλα τα βήματα, προσθέτει βασική διαχείριση σφαλμάτων και εκτυπώνει μια φιλική σύνοψη.

```python
#!/usr/bin/env python3
"""
Complete example: list cached AI models and show cache directory.
"""

import ai
import os
import sys
import shutil

def main():
    try:
        # Retrieve cached model list
        cached = ai.list_local()
        print("Cached models:", cached)

        # Retrieve cache directory
        cache_dir = ai.get_local_path()
        print("Model cache directory:", cache_dir)

        # Summarize status
        if not cached:
            print("\n⚠️  No models are currently cached.")
        else:
            print("\n✅  Found {} model(s) in cache.".format(len(cached)))

        # Optional: ask user if they want to purge an old model
        if cached:
            to_purge = input("\nEnter a model name to purge (or press Enter to skip): ").strip()
            if to_purge:
                purge_path = os.path.join(cache_dir, to_purge)
                if os.path.isdir(purge_path):
                    shutil.rmtree(purge_path)
                    print(f"🗑️  Purged {to_purge} from cache.")
                else:
                    print(f"❌  Model {to_purge} not found in cache.")
    except ai.AIError as err:
        print("AI SDK error:", err, file=sys.stderr)
        sys.exit(1)
    except Exception as exc:
        print("Unexpected error:", exc, file=sys.stderr)
        sys.exit(1)

if __name__ == "__main__":
    main()
```

**Αναμενόμενη έξοδος (όταν η κρυφή μνήμη είναι γεμάτη):**

```
Cached models: ['gpt-4-mini', 'bert-base-uncased', 'stable-diffusion-v1']
Model cache directory: /home/you/.cache/ai/models

✅  Found 3 model(s) in cache.

Enter a model name to purge (or press Enter to skip):
```

Τρέξτε το σενάριο με `python list_models.py` και θα γνωρίζετε αμέσως τι βρίσκεται στο δίσκο.

---

## Συχνές Ερωτήσεις

**Ε: Λειτουργεί αυτό σε όλα τα λειτουργικά συστήματα;**  
Α: Ναι. Το SDK αφαιρεί τις διαφορές μεταξύ OS, έτσι το `ai.get_local_path()` επιστρέφει έγκυρη συμβολοσειρά σε Linux, macOS και Windows.

**Ε: Μπορώ να καταγράψω μοντέλα από απομακρυσμένη κρυφή μνήμη;**  
Α: Η ενσωματωμένη `list_local()` αναφέρει μόνο τοπικά αποθηκευμένα αρχεία. Για απομακρυσμένα αποθετήρια θα χρησιμοποιήσετε `ai.list_remote()` (εφόσον η έκδοση του SDK το υποστηρίζει).

**Ε: Τι γίνεται αν το όνομα του SDK δεν είναι `ai`;**  
Α: Αντικαταστήστε τη γραμμή εισαγωγής με το πραγματικό όνομα του πακέτου, π.χ., `import myai as ai`. Όλες οι επόμενες κλήσεις παραμένουν ίδιες επειδή η σύμβαση API είναι συνεπής μεταξύ των υλοποιήσεων.

---

## Συμπέρασμα

Τώρα διαθέτετε μια σταθερή, έτοιμη για παραγωγή μέθοδο για **καταγραφή αποθηκευμένων μοντέλων AI** χρησιμοποιώντας τη βιβλιοθήκη **AI SDK Python**, ανάκτηση του **καταλόγου κρυφής μνήμης μοντέλων**, και ακόμη καθαρισμό παλιών αρχείων. Αυτή η γνώση σας βοηθά να διατηρείτε το περιβάλλον σας τακτοποιημένο, να αποφεύγετε περιττές λήψεις και να εντοπίζετε προβλήματα εκδόσεων με ευκολία.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να επεκτείνετε το σενάριο ώστε να κατεβάζει αυτόματα τα ελλείποντα μοντέλα, ή ενσωματώστε το σε pipeline CI που ελέγχει την υγεία της κρυφής μνήμης πριν από κάθε build. Η εξερεύνηση στρατηγικών **διαχείρισης κρυφής μνήμης μοντέλων AI** θα κάνει τις εφαρμογές σας πιο γρήγορες και αξιόπιστες.

Καλή προγραμματιστική, και να παραμείνουν οι κρυφές μνήμες σας ελαφριές!

## Τι Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}