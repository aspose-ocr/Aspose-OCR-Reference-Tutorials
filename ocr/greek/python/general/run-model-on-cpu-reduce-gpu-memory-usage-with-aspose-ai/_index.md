---
category: general
date: 2026-06-22
description: Τρέξτε το μοντέλο στην CPU και μάθετε πώς να μειώσετε τη χρήση μνήμης
  GPU ρυθμίζοντας τα επίπεδα GPU στο Aspose AI. Οδηγός βήμα‑βήμα με αποσπάσματα κώδικα.
draft: false
keywords:
- run model on cpu
- reduce gpu memory usage
- limit gpu layers
- configure gpu layers
language: el
og_description: Τρέξτε το μοντέλο στην CPU και μειώστε την κατανάλωση μνήμης GPU διαμορφώνοντας
  τα επίπεδα GPU. Πλήρης οδηγός για τη ρύθμιση του μοντέλου Aspose AI.
og_title: Εκτέλεση μοντέλου σε CPU – Μείωση χρήσης μνήμης GPU
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Run model on CPU and learn to reduce GPU memory usage by configuring
    GPU layers in Aspose AI. Step-by-step guide with code snippets.
  headline: Run Model on CPU – Reduce GPU Memory Usage with Aspose AI
  type: TechArticle
- description: Run model on CPU and learn to reduce GPU memory usage by configuring
    GPU layers in Aspose AI. Step-by-step guide with code snippets.
  name: Run Model on CPU – Reduce GPU Memory Usage with Aspose AI
  steps:
  - name: Attach any required post‑processors.
    text: Attach any required post‑processors.
  - name: Choose a configuration (`gpu_layers=0` for pure CPU, or a modest number
      for mixed mode).
    text: Choose a configuration (`gpu_layers=0` for pure CPU, or a modest number
      for mixed mode).
  - name: Initialize the model with that configuration.
    text: Initialize the model with that configuration.
  - name: Verify placement and run a test inference.
    text: Verify placement and run a test inference.
  type: HowTo
tags:
- AsposeAI
- CPU inference
- GPU optimization
title: Εκτέλεση μοντέλου σε CPU – Μείωση χρήσης μνήμης GPU με το Aspose AI
url: /el/python/general/run-model-on-cpu-reduce-gpu-memory-usage-with-aspose-ai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση Μοντέλου σε CPU – Μείωση Χρήσης Μνήμης GPU με Aspose AI

Έχετε αναρωτηθεί ποτέ πώς να **εκτελέσετε μοντέλο σε CPU** όταν ο διακομιστής σας δεν διαθέτει GPU; Ή ίσως αντιμετωπίζετε σφάλματα έλλειψης μνήμης σε ένα μέτριο GPU και χρειάζεστε **μείωση χρήσης μνήμης GPU** χωρίς να θυσιάσετε πολύ την ταχύτητα. Σε αυτόν τον οδηγό θα περάσουμε ακριβώς από αυτό: προσθήκη ενός post‑processor, εκκίνηση του Aspose AI στην CPU και ρύθμιση του αριθμού των επιπέδων GPU ώστε το αποτύπωμα μνήμης να παραμείνει μικρό.

Θα καλύψουμε τα πάντα, από την πρώτη γραμμή κώδικα μέχρι την επαλήθευση ότι το μοντέλο χρησιμοποιεί πραγματικά τη διαμόρφωση που ζητήσατε. Στο τέλος θα μπορείτε να **εκτελέσετε μοντέλο σε CPU**, **περιορίσετε τα επίπεδα GPU** και **ρυθμίσετε τα επίπεδα GPU** για οποιοδήποτε φορτίο εργασίας — χωρίς μαγεία, μόνο καθαρή Python.

## Προαπαιτούμενα

- Python 3.8+ εγκατεστημένο (ο κώδικας χρησιμοποιεί type hints αλλά λειτουργεί και σε παλαιότερες εκδόσεις)
- Πακέτο `asposeai` (εγκατάσταση μέσω `pip install asposeai`)
- Βασική εξοικείωση με έννοιες inference νευρωνικών δικτύων (δεν χρειάζεται διδακτορικό, μόνο περιέργεια)
- Προαιρετικά: μηχάνημα με ενεργό GPU για δοκιμή της αντίθεσης μεταξύ εκτελέσεων CPU και GPU

Αν λείπει κάτι από τα παραπάνω, εγκαταστήστε πρώτα το SDK· το υπόλοιπο tutorial υποθέτει ότι η εισαγωγή λειτουργεί.

![Διάγραμμα που δείχνει πώς να εκτελέσετε μοντέλο σε cpu αντί για gpu](run-model-on-cpu-diagram.png)

## Βήμα 1: Προσθήκη του Post‑Processor Ελέγχου Ορθογραφίας (Δεν Απαιτούνται Προσαρμοσμένες Ρυθμίσεις)

Πριν σκεφτούμε CPU ή GPU, ας συνδέσουμε τον post‑processor ελέγχου ορθογραφίας που παρέχει το Aspose AI. Είναι καλή πρακτική να προσθέτετε post‑processors νωρίς ώστε να αποτελούν μέρος κάθε κλήσης inference.

```python
from asposeai import AI, spell_check_processor

# Create the AI client
ai = AI()

# Attach the built‑in spell‑check processor; no custom settings required
ai.set_post_processor(spell_check_processor, custom_settings={})
```

*Γιατί είναι σημαντικό:* Οι post‑processors εκτελούνται **μετά** το μοντέλο να παράγει ακατέργαστα tokens. Συνδέοντάς τους τώρα, εξασφαλίζετε ότι οποιοδήποτε κείμενο δημιουργείτε—είτε σε CPU είτε σε GPU—καθαρίζεται αυτόματα. Είναι ένα μικρό βήμα που αποτρέπει σφάλματα σε επόμενα στάδια.

## Βήμα 2: Εκτέλεση Μοντέλου σε CPU – Εκκίνηση Aspose AI Χωρίς GPU

Τώρα έρχεται η ουσία του tutorial: να πείτε στο Aspose AI να **εκτελέσει μοντέλο σε CPU**. Το SDK εκθέτει το `AsposeAIModelConfig`, όπου η παράμετρος `gpu_layers` ελέγχει πόσα επίπεδα παραμένουν στο GPU. Ορίζοντάς το σε `0` εξαναγκάζει όλο το δίκτυο στην CPU.

```python
from asposeai import AsposeAIModelConfig

# Initialize the model configuration to use zero GPU layers (i.e., CPU only)
cpu_config = AsposeAIModelConfig(gpu_layers=0)

# Apply the configuration; this will load the model onto the CPU
ai.initialize(cpu_config)

print("✅ Model initialized on CPU – ready for inference.")
```

*Τι συμβαίνει στο παρασκήνιο;* Όταν `gpu_layers=0`, το runtime εκχωρεί όλα τα tensors στη μνήμη του κεντρικού υπολογιστή. Αυτό εξαλείφει την ανάγκη για οδηγούς CUDA, καθιστώντας το script εκτελέσιμο σε σχεδόν οποιονδήποτε διακομιστή. Η ανταλλαγή είναι η πιο αργή απόδοση, αλλά για batch jobs ή πρωτότυπα χαμηλής καθυστέρησης η απλότητα συχνά υπερτερεί της ακατέργαστης ταχύτητας.

## Βήμα 3: Περιορισμός Επιπέδων GPU για Μείωση Χρήσης Μνήμης GPU

Αν έχετε GPU αλλά η μνήμη του είναι περιορισμένη, μπορείτε να **περιορίσετε τα επίπεδα GPU** αντί να μεταφέρετε τα πάντα στην CPU. Κρατώντας μόνο μερικά πρώτα επίπεδα στο GPU, εξακολουθείτε να επωφελείστε από την επιτάχυνση του hardware ενώ μειώνετε δραστικά την κατανάλωση μνήμης.

```python
# Example: keep only the first 10 layers on the GPU; the rest run on CPU
limited_gpu_config = AsposeAIModelConfig(gpu_layers=10)

ai.initialize(limited_gpu_config)

print("✅ Model initialized with 10 GPU layers – memory usage trimmed.")
```

*Γιατί ο περιορισμός των επιπέδων GPU βοηθά:* Τα σύγχρονα μοντέλα transformer κατανέμουν την πλειονότητα της μνήμης τους ανά επίπεδο. Η αφαίρεση ακόμη και λίγων επιπέδων από το GPU μπορεί να ελευθερώσει εκατοντάδες megabytes. Αυτή η προσέγγιση είναι ιδανική για “εργασίες με περιορισμένη μνήμη” όπου θέλετε ακόμα μια αύξηση ταχύτητας για τις πιο βαριές υπολογιστικές διεργασίες.

## Βήμα 4: Ρύθμιση Επιπέδων GPU για Ευέλικτη Διαχείριση Μνήμης

Μερικές φορές χρειάζεται πιο λεπτομερής προσέγγιση — ίσως θέλετε **να ρυθμίσετε τα επίπεδα GPU** ανάλογα με το μέγεθος της συγκεκριμένης εργασίας. Το SDK σας επιτρέπει να διαβάσετε τον συνολικό αριθμό επιπέδων του μοντέλου και να υπολογίσετε έναν ασφαλή αριθμό επιπέδων GPU κατά το runtime.

```python
# Determine total number of layers (this is model‑specific; assume 36 for illustration)
total_layers = ai.model_info.total_layers  

# Choose a safe percentage, e.g., 25% of layers on GPU
gpu_layer_fraction = 0.25
desired_gpu_layers = int(total_layers * gpu_layer_fraction)

# Build the config dynamically
dynamic_config = AsposeAIModelConfig(gpu_layers=desired_gpu_layers)

ai.initialize(dynamic_config)

print(f"✅ Configured {desired_gpu_layers}/{total_layers} layers on GPU.")
```

*Συμβουλή:* Όταν τρέχετε σε κοινόχρηστο διακομιστή, ελέγξτε πρώτα τη διαθέσιμη μνήμη GPU (`torch.cuda.get_device_properties(0).total_memory`) και προσαρμόστε το `desired_gpu_layers` αναλόγως. Αυτό το επιπλέον βήμα εξασφαλίζει ότι δεν θα υπερφορτώσετε το GPU, κάτι που διαφορετικά θα προκαλούσε σφάλματα OOM.

## Βήμα 5: Επαλήθευση της Διαμόρφωσης και Δοκιμή Inference

Αφού ρυθμίσετε τη διαμόρφωση, είναι σοφό να ελέγξετε ξανά πού βρίσκεται κάθε επίπεδο. Το Aspose AI παρέχει μια διαγνωστική μέθοδο που επιστρέφει έναν χάρτη επιπέδων προς συσκευές.

```python
# Retrieve the device placement map
placement = ai.get_layer_placement()

cpu_layers = [l for l, dev in placement.items() if dev == "cpu"]
gpu_layers = [l for l, dev in placement.items() if dev == "gpu"]

print(f"Layers on CPU: {len(cpu_layers)}")
print(f"Layers on GPU: {len(gpu_layers)}")
```

Μόλις είστε ικανοποιημένοι, τρέξτε μια γρήγορη inference για να δείτε όλα σε δράση:

```python
input_text = "The quick brown fox jumps over the lazy dog."
output = ai.process(input_text)

print("Model output:", output)
```

Αν το script εκτυπώσει το αναμενόμενο κείμενο και η αναφορά τοποθέτησης ταιριάζει με τη διαμόρφωσή σας, έχετε ολοκληρώσει με επιτυχία την **εκτέλεση μοντέλου σε CPU**, τη **μείωση χρήσης μνήμης GPU** και τη **ρύθμιση επιπέδων GPU** για το σενάριό σας.

## Συνηθισμένα Προβλήματα & Πώς να τα Αποφύγετε

| Σύμπτωμα | Πιθανή Αιτία | Διόρθωση |
|----------|--------------|----------|
| Σφάλμα `CUDA out of memory` | Πάρα πολλά επίπεδα GPU | Μειώστε το `gpu_layers` ή αλλάξτε σε `gpu_layers=0` |
| Καμία έξοδος από `ai.process` | Μη αρχικοποιημένο μοντέλο | Βεβαιωθείτε ότι το `ai.initialize` καλείται **μετά** την προσθήκη των post‑processors |
| Αργή inference σε GPU | Όλα τα επίπεδα παραμένουν στην CPU | Επαληθεύστε ότι `gpu_layers` > 0 και ότι ο χάρτης συσκευών δείχνει χρήση GPU |
| Απρόσμενα ορθογραφικά λάθη | Post‑processor δεν είναι συνδεδεμένος | Καλέστε `set_post_processor` πριν το `initialize` |

## Bonus: Εναλλαγή μεταξύ CPU και GPU εν Πραγματικό χρόνο

Επειδή το SDK επανεκκινεί το μοντέλο κάθε φορά που καλείτε `initialize`, μπορείτε να εναλλάσσετε μεταξύ CPU και GPU χωρίς επανεκκίνηση του script.

```python
def switch_to_cpu():
    ai.initialize(AsposeAIModelConfig(gpu_layers=0))
    print("🔄 Switched to CPU mode.")

def switch_to_gpu(layers=12):
    ai.initialize(AsposeAIModelConfig(gpu_layers=layers))
    print(f"🔄 Switched to GPU mode with {layers} layers.")
```

Απλώς καλέστε `switch_to_cpu()` όταν χρειάζεστε εκτέλεση με χαμηλή μνήμη, και `switch_to_gpu(12)` όταν είστε έτοιμοι για αύξηση ταχύτητας.

## Συμπέρασμα

Διασχίσαμε ένα πλήρες, πρακτικό παράδειγμα για το πώς να **εκτελέσετε μοντέλο σε CPU**, **να μειώσετε τη χρήση μνήμης GPU**, **να περιορίσετε τα επίπεδα GPU**, και **να ρυθμίσετε τα επίπεδα GPU** με το Aspose AI. Τα βήματα είναι απλά:

1. Προσθέστε τυχόν απαιτούμενους post‑processors.  
2. Επιλέξτε μια διαμόρφωση (`gpu_layers=0` για καθαρή CPU, ή έναν μέτριο αριθμό για μεικτό τρόπο).  
3. Αρχικοποιήστε το μοντέλο με αυτή τη διαμόρφωση.  
4. Επαληθεύστε την τοποθέτηση και τρέξτε μια δοκιμαστική inference.  

Με αυτά τα εργαλεία μπορείτε να διατηρήσετε τις pipelines inference ελαφριές, να αποφύγετε δαπανηρά σφάλματα OOM, και να εξαχθεί απόδοση ακόμη και από ένα μέτριο GPU όταν είναι διαθέσιμο. Στο επόμενο βήμα, μπορείτε να εξερευνήσετε στρατηγικές batching, ποσοτικοποίηση, ή ακόμη και την εκχώρηση τμημάτων του μοντέλου στην CPU ενώ διατηρείτε τα attention heads στο GPU — κάθε ένα από αυτά τα θέματα στηρίζεται άμεσα στη **ρύθμιση επιπέδων GPU** που μόλις μάθατε.

Έχετε ερωτήσεις για συγκεκριμένη αρχιτεκτονική μοντέλου ή χρειάζεστε βοήθεια στην προσαρμογή του αριθμού επιπέδων για ένα

## Τι Πρέπει να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Aspose OCR Tutorial – Optical Character Recognition](/ocr/english/)
- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}