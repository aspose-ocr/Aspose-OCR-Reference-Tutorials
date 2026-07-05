---
category: general
date: 2026-07-05
description: Πώς να εμφανίσετε τη λίστα μοντέλων με το Aspose AI, να ενεργοποιήσετε
  την αυτόματη λήψη και να κατεβάσετε μοντέλο Hugging Face σε Python. Ακολουθήστε
  αυτό το βήμα‑βήμα οδηγό για να ρυθμίσετε την προσωρινή μνήμη και να αρχίσετε να
  χρησιμοποιείτε το Aspose AI σήμερα.
draft: false
keywords:
- how to list models
- enable auto download
- download hugging face model
- how to use aspose
- how to set cache
language: el
og_description: Πώς να εμφανίσετε τα μοντέλα με το Aspose AI, να ενεργοποιήσετε την
  αυτόματη λήψη και να κατεβάσετε ένα μοντέλο Hugging Face. Μάθετε πώς να ρυθμίσετε
  την κρυφή μνήμη και να χρησιμοποιήσετε το Aspose AI σε λίγα λεπτά.
og_title: Πώς να καταγράψετε μοντέλα με το Aspose AI – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  headline: How to list models with Aspose AI – Complete Guide
  type: TechArticle
- description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  name: How to list models with Aspose AI – Complete Guide
  steps:
  - name: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
    text: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
  - name: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
    text: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
  - name: Initialise the AI, then call `list_local()` to see exactly what’s cached.
    text: Initialise the AI, then call `list_local()` to see exactly what’s cached.
  - name: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
    text: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
  type: HowTo
tags:
- Aspose
- Python
- LLM
- Model Management
title: Πώς να απαριθμήσετε μοντέλα με το Aspose AI – Πλήρης οδηγός
url: /el/python/general/how-to-list-models-with-aspose-ai-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να καταγράψετε μοντέλα με το Aspose AI – Πλήρης Οδηγός

Το πώς να καταγράψετε μοντέλα με το Aspose AI είναι μια ερώτηση που εμφανίζεται τη στιγμή που αρχίζετε να πειραματίζεστε με μεγάλα γλωσσικά μοντέλα σε Python. Σε αυτόν τον οδηγό θα περάσουμε από την ενεργοποίηση του **auto download**, τη διαμόρφωση μιας τοπικής κρυφής μνήμης (cache) και τη λήψη ενός μοντέλου απευθείας από το Hugging Face—ώστε να μπορείτε να ξεκινήσετε χωρίς να ψάχνετε χειροκίνητα για αρχεία.

Αν ποτέ αναρωτηθήκατε *«πώς να χρησιμοποιήσω το Aspose για AI με OCR;»* ή *«ποια είναι η πιο εύκολη μέθοδος για να ρυθμίσετε την κρυφή μνήμη (cache) για αρχεία μοντέλων;»* βρίσκεστε στο σωστό μέρος. Στο τέλος θα έχετε ένα πλήρως λειτουργικό script που καταγράφει κάθε μοντέλο που αποθηκεύεται τοπικά, κατεβάζει αυτόματα τα ελλιπή και σας δείχνει ακριβώς πού βρίσκονται τα αρχεία στο δίσκο.

---

## Τι Θα Χρειαστεί

- Python 3.9 ή νεότερη (η βιβλιοθήκη χρησιμοποιεί type hints που απαιτούν πρόσφατο interpreter)
- `pip` πρόσβαση για την εγκατάσταση του πακέτου **Aspose OCR** (`aocr`).  
  ```bash
  pip install aocr
  ```
- Σύνδεση στο διαδίκτυο για το πρώτο download από το Hugging Face.
- Ένας φάκελος όπου θέλετε να αποθηκεύσετε την κρυφή μνήμη μοντέλων (π.χ., `./model_cache`).

Αυτό είναι όλο—χωρίς επιπλέον Docker containers, χωρίς βαριά virtual environments πέρα από μια καθαρή εγκατάσταση Python.

## ## Πώς να καταγράψετε μοντέλα με το Aspose AI

Η ουσία αυτού του οδηγού είναι η δυνατότητα **list models** που το Aspose AI έχει αποθηκεύσει τοπικά στην κρυφή μνήμη. Μonce η κρυφή μνήμη ρυθμιστεί, η βιβλιοθήκη μπορεί να απαριθμήσει όλα όσα γνωρίζει, κάνοντας το debugging και τον έλεγχο εκδόσεων παιχνιδάκι.

```python
import aocr

# 1️⃣ Create an Aspose AI instance
ai = aocr.AsposeAI()

# 2️⃣ Configure the model cache and auto‑download behavior
cfg = aocr.AsposeAIModelConfig()
cfg.allow_auto_download = "true"                     # ← enable auto download
cfg.directory_model_path = r"./model_cache"          # ← how to set cache
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

# 3️⃣ Initialise the AI with the config we just built
ai.initialize(cfg)

# 4️⃣ List the models that are already cached locally
print("🗂️ Models cached at:", ai.get_local_path())
print("📦 Available models:", ai.list_local())
```

**Γιατί λειτουργεί αυτό:**

- `AsposeAI()` δημιουργεί το υψηλού επιπέδου entry point που επικοινωνεί με τη βασική μηχανή inference.  
- `AsposeAIModelConfig()` περιέχει όλες τις ρυθμίσεις που μπορείτε να προσαρμόσετε· ορίζοντας `allow_auto_download` σε `"true"` λέει στη βιβλιοθήκη να κατεβάζει αυτόματα τα ελλιπή αρχεία από το αποθετήριο που καθορίζετε.  
- `directory_model_path` είναι το *cache directory*—η θέση όπου ζουν όλα τα ληφθέντα binaries.  
- `initialize()` εφαρμόζει τη διαμόρφωση, εκτελώντας το πρώτο download αν η κρυφή μνήμη είναι κενή.  
- Τέλος, το `list_local()` σαρώει το φάκελο κρυφής μνήμης και επιστρέφει μια λίστα Python με τα αναγνωριστικά των μοντέλων, τα οποία εκτυπώνουμε.

### Αναμενόμενη έξοδος (πρώτη εκτέλεση)

```
🗂️ Models cached at: ./model_cache
📦 Available models: ['Qwen2.5-3B-Instruct-GGUF']
```

Αν εκτελέσετε ξανά το script, η βιβλιοθήκη θα παραλείψει το download και απλώς θα καταγράψει το ήδη υπάρχον μοντέλο, αποδεικνύοντας ότι το **how to set cache** πραγματικά αποδίδει σε επόμενες εκτελέσεις.

## ## Ενεργοποίηση auto download για ελλιπή μοντέλα

Συχνά θα δουλεύετε με πολλά μοντέλα σε διάφορα έργα. Η χειροκίνητη λήψη καθενός από το Hugging Face μπορεί να είναι κουραστική. Ενεργοποιώντας το auto download, το Aspose AI αναλαμβάνει το βαρέως φορτίου.

```python
cfg.allow_auto_download = "true"
```

> **Pro tip:** Κρατήστε το `allow_auto_download` ορισμένο σε `"true"` **μόνο** σε περιβάλλοντα ανάπτυξης ή CI. Σε παραγωγή ίσως θέλετε να κλειδώσετε την κρυφή μνήμη για να αποφύγετε απρόσμενη κίνηση δικτύου.

Αν αργότερα αποφασίσετε να το απενεργοποιήσετε, απλώς ορίστε τη σημαία σε `"false"` πριν καλέσετε ξανά το `initialize()`.

## ## Λήψη μοντέλου Hugging Face εν κινήσει

Η γραμμή

```python
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
```

ειδικοποιεί στο Aspose AI από ποιο απομακρυσμένο αποθετήριο να κάνει λήψη. Η βιβλιοθήκη υποστηρίζει οποιοδήποτε δημόσιο μοντέλο στο Hugging Face που παρέχει αρχείο GGUF. Θέλετε διαφορετικό μοντέλο; Αντικαταστήστε το repo ID:

```python
cfg.hugging_face_repo_id = "mistralai/Mistral-7B-Instruct-v0.2"
```

Όταν εκτελείτε το script, το Aspose AI ελέγχει την κρυφή μνήμη:

- **Αν το μοντέλο υπάρχει**, το φορτώνει αμέσως.  
- **Αν δεν υπάρχει**, η σημαία auto‑download ενεργοποιεί ένα download, αποθηκεύει το αρχείο στο `directory_model_path`, και στη συνέχεια το καταχωρεί για άμεση χρήση.

Αυτή η προσέγγιση εξαλείφει τη διαδικασία «download‑then‑run» δύο βημάτων που πολλές οδηγίες σας επιβάλλουν.

## ## Πώς να χρησιμοποιήσετε το Aspose AI μετά την καταγραφή του μοντέλου

Η καταγραφή μοντέλων είναι μόνο το ήμισυ της ιστορίας. Μόλις γνωρίζετε ότι ένα μοντέλο είναι παρόν, μπορείτε να ξεκινήσετε inference:

```python
# Assume the model we just listed is the one we want to use
model_name = ai.list_local()[0]

# Create a simple prompt
prompt = "Explain the difference between supervised and unsupervised learning."

# Run inference
response = ai.run_inference(model_name, prompt)

print("🤖 Model response:", response)
```

**Γιατί αυτό είναι σημαντικό:**

- `run_inference()` αφαιρεί την πολυπλοκότητα του tokenization, batching, και της διαχείρισης GPU.  
- Με τη μεταβίβαση του *model name* που λάβατε από το `list_local()`, εξασφαλίζετε ότι η κλήση inference ταιριάζει ακριβώς με το αρχείο στο δίσκο.

## ## Πώς να ορίσετε τη θέση της κρυφής μνήμης για πολλαπλά έργα

Αν διαχειρίζεστε πολλά έργα, ίσως θέλετε το καθένα να έχει το δικό του φάκελο κρυφής μνήμης. Το πεδίο `directory_model_path` είναι απλώς μια συμβολοσειρά, οπότε μπορείτε να το δημιουργήσετε δυναμικά:

```python
import os

project_name = "sentiment_analysis"
cache_root   = "./model_cache"
cfg.directory_model_path = os.path.join(cache_root, project_name)
```

Τώρα κάθε έργο λαμβάνει έναν απομονωμένο υπο‑φάκελο (`./model_cache/sentiment_analysis`), αποτρέποντας συγκρούσεις εκδόσεων και καθιστώντας την εκκαθάριση απλή.

## ## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Σύμπτωμα | Πιθανή αιτία | Διόρθωση |
|---------|--------------|-----|
| **`PermissionError` when accessing cache** | Ο φάκελος κρυφής μνήμης ανήκει σε άλλο χρήστη (συνηθισμένο σε κοινόχρηστους διακομιστές) | Δημιουργήστε τον φάκελο χειροκίνητα με τις κατάλληλες άδειες: `mkdir -p ./model_cache && chmod 775 ./model_cache` |
| **Model never appears in `list_local()`** | `allow_auto_download` ορισμένο σε `"false"` και το μοντέλο δεν είναι ακόμη στην κρυφή μνήμη | Ανεργοποιήστε προσωρινά τη σημαία, τρέξτε μία φορά, έπειτα απενεργοποιήστε την αν το επιθυμείτε |
| **Unexpected model version** | Δύο διαφορετικά αποθετήρια μοιράζονται το ίδιο όνομα αλλά διαφορετικά αρχεία | Καθορίστε ακριβώς το repo ID (συμπεριλαμβανομένου του tag/commit) ή κλειδώστε την κρυφή μνήμη απενεργοποιώντας το auto‑download μετά το πρώτο επιτυχές pull |
| **Out‑of‑memory errors** | Μεγάλα αρχεία GGUF σε μηχάνημα χωρίς αρκετή RAM/VRAM | Χρησιμοποιήστε μικρότερο μοντέλο (π.χ., `Qwen2.5-1.5B`) ή ορίστε `cfg.device = "cpu"` για να εξαναγκάσετε inference στην CPU |

## ## Πλήρες script που μπορείτε να αντιγράψετε‑και‑επικολλήσετε

Παρακάτω βρίσκεται το πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που ενσωματώνει όλες τις παραπάνω έννοιες. Αποθηκεύστε το ως `list_models_demo.py` και εκτελέστε το με `python list_models_demo.py`.

```python
# list_models_demo.py
import os
import aocr

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Create the Aspose AI instance
    # ------------------------------------------------------------------
    ai = aocr.AsposeAI()

    # ------------------------------------------------------------------
    # 2️⃣ Build configuration: enable auto download, set cache path,
    #    and point at a Hugging Face repo
    # ------------------------------------------------------------------
    cfg = aocr.AsposeAIModelConfig()
    cfg.allow_auto_download = "true"                               # enable auto download
    cfg.directory_model_path = os.path.abspath("./model_cache")   # how to set cache
    cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

    # ------------------------------------------------------------------
    # 3️⃣ Initialise the AI with the configuration
    # ------------------------------------------------------------------
    ai.initialize(cfg)

    # ------------------------------------------------------------------
    # 4️⃣ Verify cache location and list all locally available models
    # ------------------------------------------------------------------
    print("🗂️ Models cached at:", ai.get_local_path())
    print("📦 Available models:", ai.list_local())

    # ------------------------------------------------------------------
    # 5️⃣ (Optional) Run a quick inference using the first listed model
    # ------------------------------------------------------------------
    if ai.list_local():
        model_name = ai.list_local()[0]
        prompt = "Give a short summary of the Python GIL."
        response = ai.run_inference(model_name, prompt)
        print("\n🤖 Model response:", response)

if __name__ == "__main__":
    main()
```

**Η εκτέλεσή του** θα παράγει έξοδο παρόμοια με το προηγούμενο παράδειγμα, ακολουθούμενη από μια σύντομη απάντηση από το μοντέλο. Μη διστάσετε να αντικαταστήσετε το prompt με ό,τι θέλετε—αυτή είναι η πιο γρήγορη μέθοδος για να δοκιμάσετε ότι το μοντέλο είναι πραγματικά χρησιμοποιήσιμο μετά το **how to list models**.

## ## Σύνοψη

Καλύψαμε όλα όσα χρειάζεστε για **how to list models** χρησιμοποιώντας το Aspose AI, από την ενεργοποίηση του **auto download** μέχρι τη διαμόρφωση μιας μόνιμης **cache** και τη λήψη ενός **μοντέλου Hugging Face** κατ' απαίτηση. Τα βασικά σημεία:

1. Δημιουργήστε ένα αντικείμενο `AsposeAI` και ένα `AsposeAIModelConfig`.  
2. Ορίστε `allow_auto_download = "true"` και δείξτε το `directory_model_path` σε έναν φάκελο που ελέγχετε.  
3. Αρχικοποιήστε το AI, έπειτα καλέστε `list_local()` για να δείτε ακριβώς τι είναι στην κρυφή μνήμη.  
4. Χρησιμοποιήστε το όνομα του καταγεγραμμένου μοντέλου για inference, και είστε έτοιμοι να δημιουργήσετε εφαρμογές πραγματικού κόσμου.

## Τι Ακολουθεί;

- **Πειραματιστείτε με διαφορετικά μοντέλα** – αντικαταστήστε το `cfg.hugging_face_repo_id` με άλλο αποθετήριο και δείτε πώς αλλάζει η λίστα.  
- **Ρύθμιση της cache**

## Τι Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικά θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετα χαρακτηριστικά του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Επεξεργαστείτε Μαζικά Εικόνες OCR με Λίστα στο Aspose.OCR για .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Πώς να Ορίσετε Άδεια Aspose OCR και να την Επαληθεύσετε σε Java](/ocr/english/java/ocr-basics/set-license/)
- [Πώς να Εξάγετε Κείμενο από Εικόνα Χρησιμοποιώντας Aspose.OCR για .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}