---
category: general
date: 2026-02-22
description: Μάθετε πώς να εμφανίζετε τη λίστα των αποθηκευμένων μοντέλων και να δείχνετε
  γρήγορα τον φάκελο cache στον υπολογιστή σας. Περιλαμβάνει βήματα για την προβολή
  του φακέλου cache και τη διαχείριση της τοπικής αποθήκευσης μοντέλων AI.
draft: false
keywords:
- list cached models
- show cache directory
- how to view cache folder
- AI model cache
- local model storage
language: el
og_description: Μάθετε πώς να καταγράψετε τα αποθηκευμένα μοντέλα, να εμφανίσετε τον
  κατάλογο cache και να προβάλετε το φάκελο cache σε λίγα εύκολα βήματα. Συμπεριλαμβάνεται
  πλήρες παράδειγμα Python.
og_title: Λίστα αποθηκευμένων μοντέλων – γρήγορος οδηγός για την προβολή του καταλόγου
  προσωρινής μνήμης
tags:
- AI
- caching
- Python
- development
title: Λίστα αποθηκευμένων μοντέλων – πώς να προβάλετε το φάκελο cache και να εμφανίσετε
  τον κατάλογο cache
url: /el/python/general/list-cached-models-how-to-view-cache-folder-and-show-cache-d/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# λίστα αποθηκευμένων μοντέλων – γρήγορος οδηγός για προβολή του καταλόγου cache

Έχετε αναρωτηθεί ποτέ πώς να **καταγράψετε τα αποθηκευμένα μοντέλα** στον υπολογιστή σας χωρίς να ψάχνετε σε άγνωστους φακέλους; Δεν είστε οι μόνοι. Πολλοί προγραμματιστές συναντούν πρόβλημα όταν πρέπει να επαληθεύσουν ποια μοντέλα AI είναι ήδη αποθηκευμένα τοπικά, ειδικά όταν ο χώρος στο δίσκο είναι περιορισμένος. Τα καλά νέα; Με λίγες μόνο γραμμές κώδικα μπορείτε να **καταγράψετε τα αποθηκευμένα μοντέλα** και να **εμφανίσετε τον φάκελο cache**, αποκτώντας πλήρη ορατότητα στο φάκελο cache.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα αυτόνομο script Python που κάνει ακριβώς αυτό. Στο τέλος θα ξέρετε πώς να δείτε το φάκελο cache, πού βρίσκεται το cache σε διαφορετικά λειτουργικά συστήματα, και θα έχετε μια τακτοποιημένη εκτύπωση λίστας όλων των μοντέλων που έχουν ληφθεί. Χωρίς εξωτερική τεκμηρίωση, χωρίς εικασίες—απλός κώδικας και εξηγήσεις που μπορείτε να αντιγράψετε‑και‑επικολλήσετε αμέσως.

## Τι Θα Μάθετε

- Πώς να αρχικοποιήσετε έναν πελάτη AI (ή ένα stub) που προσφέρει εργαλεία cache.  
- Οι ακριβείς εντολές για **list cached models** και **show cache directory**.  
- Πού βρίσκεται το cache στα Windows, macOS και Linux, ώστε να μπορείτε να το περιηγηθείτε χειροκίνητα αν το θέλετε.  
- Συμβουλές για την αντιμετώπιση ειδικών περιπτώσεων όπως κενό cache ή προσαρμοσμένη διαδρομή cache.  

**Προαπαιτούμενα** – χρειάζεστε Python 3.8+ και έναν πελάτη AI που μπορεί να εγκατασταθεί μέσω pip και υλοποιεί `list_local()`, `get_local_path()` και προαιρετικά `clear_local()`. Αν δεν έχετε ακόμη κάποιον, το παράδειγμα χρησιμοποιεί μια ψεύτικη κλάση `YourAIClient` που μπορείτε να αντικαταστήσετε με το πραγματικό SDK (π.χ., `openai`, `huggingface_hub`, κ.λπ.).  

Έτοιμοι; Ας ξεκινήσουμε.

## Βήμα 1: Ρύθμιση του Πελάτη AI (ή Mock)

Αν έχετε ήδη ένα αντικείμενο πελάτη, παραλείψτε αυτό το τμήμα. Διαφορετικά, δημιουργήστε ένα μικρό αντικαταστάτη που μιμείται τη διεπαφή cache. Αυτό κάνει το script εκτελέσιμο ακόμα και χωρίς πραγματικό SDK.

```python
# step_1_client_setup.py
import os
from pathlib import Path

class YourAIClient:
    """
    Minimal mock of an AI client that stores downloaded models in a
    directory called `.ai_cache` inside the user's home folder.
    """
    def __init__(self, cache_dir: Path | None = None):
        # Use a custom path if supplied, otherwise default to ~/.ai_cache
        self.cache_dir = Path(cache_dir) if cache_dir else Path.home() / ".ai_cache"
        self.cache_dir.mkdir(parents=True, exist_ok=True)

    def list_local(self):
        """Return a list of model folder names that exist in the cache."""
        return [p.name for p in self.cache_dir.iterdir() if p.is_dir()]

    def get_local_path(self):
        """Absolute path to the cache directory."""
        return str(self.cache_dir.resolve())

    # Optional helper for demonstration purposes
    def _populate_dummy_models(self, count=3):
        for i in range(1, count + 1):
            (self.cache_dir / f"model_{i}").mkdir(exist_ok=True)

# Initialize the client (replace with real client if you have one)
ai = YourAIClient()
# Populate with dummy data the first time you run the script
if not ai.list_local():
    ai._populate_dummy_models()
```

> **Pro tip:** Αν έχετε ήδη έναν πραγματικό πελάτη (π.χ., `from huggingface_hub import HfApi`), απλώς αντικαταστήστε την κλήση `YourAIClient()` με `HfApi()` και βεβαιωθείτε ότι οι μέθοδοι `list_local` και `get_local_path` υπάρχουν ή έχουν τυλιχθεί αναλόγως.

## Βήμα 2: **list cached models** – ανάκτηση και εμφάνιση

Τώρα που ο πελάτης είναι έτοιμος, μπορούμε να του ζητήσουμε να απαριθμήσει όλα όσα γνωρίζει τοπικά. Αυτό είναι το κεντρικό κομμάτι της λειτουργίας **list cached models**.

```python
# step_2_list_models.py
print("Cached models:")
for model_name in ai.list_local():
    print(" -", model_name)
```

**Αναμενόμενη έξοδος** (με τα ψεύτικα δεδομένα από το βήμα 1):

```
Cached models:
 - model_1
 - model_2
 - model_3
```

Αν το cache είναι κενό, θα δείτε απλώς:

```
Cached models:
```

Αυτή η μικρή κενή γραμμή σας λέει ότι δεν υπάρχει κάτι αποθηκευμένο ακόμη—χρήσιμο όταν γράφετε σενάρια καθαρισμού.

## Βήμα 3: **show cache directory** – πού βρίσκεται το cache;

Η γνώση της διαδρομής είναι συχνά το ήμισυ του αγώνα. Τα διαφορετικά λειτουργικά συστήματα τοποθετούν τα caches σε διαφορετικές προεπιλεγμένες θέσεις, και κάποια SDK επιτρέπουν την παράκαμψη μέσω μεταβλητών περιβάλλοντος. Το παρακάτω απόσπασμα τυπώνει τη απόλυτη διαδρομή ώστε να μπορείτε να κάνετε `cd` σε αυτή ή να τη ανοίξετε σε εξερευνητή αρχείων.

```python
# step_3_show_path.py
print("\nCache directory:", ai.get_local_path())
```

**Τυπική έξοδος** σε σύστημα τύπου Unix:

```
Cache directory: /home/youruser/.ai_cache
```

Στα Windows μπορεί να δείτε κάτι όπως:

```
Cache directory: C:\Users\YourUser\.ai_cache
```

Τώρα ξέρετε ακριβώς **πώς να δείτε το φάκελο cache** σε οποιαδήποτε πλατφόρμα.

## Βήμα 4: Συνδυάστε Όλα – ένα εκτελέσιμο script

Παρακάτω είναι το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα που συνδυάζει τα τρία βήματα. Αποθηκεύστε το ως `view_ai_cache.py` και τρέξτε `python view_ai_cache.py`.

```python
# view_ai_cache.py
import os
from pathlib import Path

class YourAIClient:
    """Simple mock client exposing cache‑related utilities."""
    def __init__(self, cache_dir: Path | None = None):
        self.cache_dir = Path(cache_dir) if cache_dir else Path.home() / ".ai_cache"
        self.cache_dir.mkdir(parents=True, exist_ok=True)

    def list_local(self):
        return [p.name for p in self.cache_dir.iterdir() if p.is_dir()]

    def get_local_path(self):
        return str(self.cache_dir.resolve())

    def _populate_dummy_models(self, count=3):
        for i in range(1, count + 1):
            (self.cache_dir / f"model_{i}").mkdir(exist_ok=True)

# ----------------------------------------------------------------------
# Main execution block
# ----------------------------------------------------------------------
if __name__ == "__main__":
    # Initialize (replace with real client if available)
    ai = YourAIClient()

    # Populate dummy data only on first run – remove this in production
    if not ai.list_local():
        ai._populate_dummy_models()

    # Step 1: list cached models
    print("Cached models:")
    for model_name in ai.list_local():
        print(" -", model_name)

    # Step 2: show cache directory
    print("\nCache directory:", ai.get_local_path())
```

Τρέξτε το και θα δείτε αμέσως τόσο τη λίστα των αποθηκευμένων μοντέλων **όσο** τη θέση του φακέλου cache.

## Ειδικές Περιπτώσεις & Παραλλαγές

| Κατάσταση | Τι να Κάνετε |
|-----------|--------------|
| **Κενό cache** | Το script θα εκτυπώσει “Cached models:” χωρίς καταχωρήσεις. Μπορείτε να προσθέσετε μια προειδοποίηση: `if not models: print("⚠️ No models cached yet.")` |
| **Προσαρμοσμένη διαδρομή cache** | Περνάτε μια διαδρομή κατά τη δημιουργία του πελάτη: `YourAIClient(cache_dir=Path("/tmp/my_ai_cache"))`. Η κλήση `get_local_path()` θα αντανακλά αυτή τη θέση. |
| **Σφάλματα δικαιωμάτων** | Σε περιορισμένα μηχανήματα, ο πελάτης μπορεί να ρίξει `PermissionError`. Τυλίξτε την αρχικοποίηση σε `try/except` και πέστε σε φάκελο εγγράψιμο από τον χρήστη. |
| **Χρήση πραγματικού SDK** | Αντικαταστήστε το `YourAIClient` με την πραγματική κλάση πελάτη και βεβαιωθείτε ότι τα ονόματα μεθόδων ταιριάζουν. Πολλά SDK εκθέτουν μια ιδιότητα `cache_dir` που μπορείτε να διαβάσετε απευθείας. |

## Pro Tips για Διαχείριση του Cache

- **Τακτικός καθαρισμός:** Αν κατεβάζετε συχνά μεγάλα μοντέλα, προγραμματίστε ένα cron job που καλεί `shutil.rmtree(ai.get_local_path())` αφού επιβεβαιώσετε ότι δεν τα χρειάζεστε πια.  
- **Παρακολούθηση χρήσης δίσκου:** Χρησιμοποιήστε `du -sh $(ai.get_local_path())` σε Linux/macOS ή `Get-ChildItem -Recurse | Measure-Object -Property Length -Sum` στο PowerShell για να παρακολουθείτε το μέγεθος.  
- **Φάκελοι με εκδόσεις:** Κάποιοι πελάτες δημιουργούν υποφακέλους ανά έκδοση μοντέλου. Όταν **list cached models**, θα δείτε κάθε έκδοση ως ξεχωριστή καταχώρηση—χρησιμοποιήστε το για να αφαιρέσετε παλαιότερες εκδόσεις.  

## Οπτική Επισκόπηση

![list cached models screenshot](https://example.com/images/list-cached-models.png "list cached models – console output showing models and cache path")

*Alt text:* *list cached models – console output displaying cached model names and the cache directory path.*

## Συμπέρασμα

Καλύψαμε όλα όσα χρειάζεστε για **list cached models**, **show cache directory**, και γενικά **πώς να δείτε το φάκελο cache** σε οποιοδήποτε σύστημα. Το σύντομο script παρουσιάζει μια πλήρη, εκτελέσιμη λύση, εξηγεί **γιατί** κάθε βήμα είναι σημαντικό, και προσφέρει πρακτικές συμβουλές για πραγματική χρήση.  

Στη συνέχεια, μπορείτε να εξερευνήσετε **πώς να καθαρίσετε το cache** προγραμματιστικά, ή να ενσωματώσετε αυτές τις κλήσεις σε μεγαλύτερο pipeline ανάπτυξης που επαληθεύει τη διαθεσιμότητα μοντέλων πριν την εκκίνηση εργασιών inference. Όπως και να έχει, έχετε τώρα τη βάση για να διαχειρίζεστε την τοπική αποθήκευση μοντέλων AI με σιγουριά.

Έχετε ερωτήσεις για κάποιο συγκεκριμένο SDK AI; Αφήστε ένα σχόλιο παρακάτω, και καλή διαχείριση του cache!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}