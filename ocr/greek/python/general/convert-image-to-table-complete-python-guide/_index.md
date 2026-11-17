---
category: general
date: 2026-03-26
description: Μετατρέψτε την εικόνα σε πίνακα με Python χρησιμοποιώντας OCR και AI.
  Μάθετε πώς να εξάγετε πίνακα από εικόνα, να βελτιώσετε την ακρίβεια του OCR και
  να λαμβάνετε δομημένα αποτελέσματα γρήγορα.
draft: false
keywords:
- convert image to table
- extract table from image
- extract tabular data image
- enhance OCR accuracy
language: el
og_description: Μετατροπή εικόνας σε πίνακα με Python. Αυτός ο οδηγός δείχνει πώς
  να εξάγετε πίνακα από εικόνα, να βελτιώσετε την ακρίβεια του OCR και να εργαστείτε
  με δομημένα δεδομένα.
og_title: Μετατροπή εικόνας σε πίνακα – Python οδηγός βήμα‑βήμα
tags:
- OCR
- Python
- AI post‑processing
title: Μετατροπή εικόνας σε πίνακα – Πλήρης οδηγός Python
url: /el/python/general/convert-image-to-table-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή εικόνας σε πίνακα – Πλήρης Οδηγός Python

Έχετε ποτέ χρειαστεί να **μετατρέψετε εικόνα σε πίνακα** αλλά να κολλήσετε μπροστά σε μια θολή λήψη οθόνης; Δεν είστε οι μόνοι. Σε πολλά έργα που βασίζονται σε δεδομένα, ο πιο γρήγορος τρόπος να πάρετε αριθμούς σε ένα dataframe είναι να τραβήξετε μια φωτογραφία ενός τυπωμένου πίνακα και να αφήσετε ένα script να κάνει τη βαριά δουλειά. Τα καλά νέα; Με μια σύγχρονη μηχανή OCR συνδυασμένη με έναν μικρό AI post‑processor, μπορείτε να εξάγετε έναν καθαρό, δομημένο πίνακα από σχεδόν οποιαδήποτε εικόνα.

Σε αυτό το tutorial θα περάσουμε από ένα **πραγματικό παράδειγμα που εξάγει δεδομένα από εικόνα πίνακα**, θα τα καθαρίσουμε και θα εκτυπώσουμε κάθε γραμμή ως απλό κείμενο. Στο τέλος θα καταλάβετε πώς να **βελτιώσετε την ακρίβεια του OCR**, να αντιμετωπίσετε κοινές παγίδες και να προσαρμόσετε τον κώδικα στις δικές σας ροές εργασίας. Χωρίς μαγεία, μόνο Python, μερικές βιβλιοθήκες και λίγη λογική.

> **Τι θα χρειαστείτε**  
> * Python 3.9+  
> * Μια βιβλιοθήκη OCR που υποστηρίζει `OutputFormat.Structured` (π.χ., `myocr`)  
> * Ένα προαιρετικό AI post‑processor (μπορεί να είναι ένας ελαφρύς transformer ή μια λειτουργία βασισμένη σε κανόνες)  
> * Ένα δείγμα αρχείου εικόνας (`table.png`) που περιέχει έναν απλό πίνακα

---

## Βήμα 1: Μετατροπή εικόνας σε πίνακα – Αναγνώριση της εικόνας με δομημένη έξοδο

Το πρώτο που κάνουμε είναι να τροφοδοτήσουμε την εικόνα στη μηχανή OCR και να ζητήσουμε ένα **δομημένο** αποτέλεσμα. Η δομημένη έξοδος σημαίνει ότι η μηχανή προσπαθεί να εντοπίσει γραμμές, στήλες και όρια κελιών αντί να επιστρέψει ένα επίπεδο κείμενο.

```python
import myocr as ocr          # Hypothetical OCR package
import myengine as engine    # Wrapper around the OCR engine
import myai as ai            # Simple AI post‑processor

def recognize_image(path: str):
    """
    Sends the image to the OCR engine and asks for a tabular
    (structured) representation.
    """
    # Step 1: Recognize the image and request a structured (tabular) result
    structured_result = engine.recognize_image(
        path,
        output_format=ocr.OutputFormat.Structured
    )
    return structured_result
```

**Γιατί είναι σημαντικό:**  
Αν ζητήσετε από το OCR απλό κείμενο, θα λάβετε ένα μπερδεμένο σύνολο χαρακτήρων χωρίς έννοια γραμμών ή στηλών. Ζητώντας δομημένη μορφή, η μηχανή κάνει τη βαριά δουλειά της εντοπισμού γραμμών, στοίχισης στηλών και ακόμη βασικής συγχώνευσης κελιών. Αυτό μειώνει δραστικά την ποσότητα χειροκίνητης ανάλυσης που θα χρειαστείτε αργότερα.

> **Συμβουλή επαγγελματία:** Βεβαιωθείτε ότι η εικόνα έχει καλό αντίθεση και ελάχιστη κλίση. Σάρωση 300 dpi συνήθως δίνει τα καλύτερα αποτελέσματα.

---

## Βήμα 2: Βελτίωση ακρίβειας OCR – Post‑process η ακατέργαστη δομή

Το OCR δεν είναι τέλειο—ιδιαίτερα όταν η πηγή περιέχει αχνές γραμμές ή ασυνήθιστα fonts. Εδώ μπαίνει ένας ελαφρύς AI (ή ακόμη και ένα script βασισμένο σε κανόνες) που καθαρίζει την έξοδο, διορθώνει κοινές λανθασμένες αναγνώσεις και προσθέτει το χαμένο περιεχόμενο.

```python
def enhance_structure(structured_result):
    """
    Runs a post‑processor that fixes typical OCR errors
    (e.g., 'O' vs '0', merged cells) and adds semantic context.
    """
    # Step 2: Enhance the raw OCR structure with AI (adds context, corrects errors)
    enhanced_structure = ai.run_postprocessor(structured_result)
    return enhanced_structure
```

**Γιατί είναι σημαντικό:**  
Ένας ακατέργαστος OCR πίνακας μπορεί να ετικετοποιήσει μια κεφαλίδα ως “Q1 2022” αλλά να διαβάσει το “1” ως “l”. Η AI στρώση μπορεί να μάθει αυτά τα μοτίβα από ένα μικρό σύνολο εκπαίδευσης και να παραγάγει έναν πιο καθαρό πίνακα. Ακόμη και μια απλή ευρετική (αντικατάσταση απομονωμένου “l” με “1” όταν περιβάλλεται από ψηφία) μπορεί να αυξήσει **την ακρίβεια του OCR** δραματικά.

> **Κοινή περίπτωση άκρης:** Αν ο πίνακας περιέχει συγχωνευμένα κελιά, το OCR μπορεί να διπλασιάσει το περιεχόμενο σε πολλές στήλες. Ο post‑processor πρέπει να εντοπίζει τα ίδια γειτονικά κελιά και να τα συγχωνεύει.

---

## Βήμα 3: Εξαγωγή δεδομένων από εικόνα πίνακα – Επανάληψη πάνω στις γραμμές και εμφάνιση κειμένου κελιών

Τώρα που έχουμε μια τακτοποιημένη δομή, η εξαγωγή των δεδομένων είναι απλή. Θα κάνουμε βρόχο πάνω στον πρώτο εντοπισμένο πίνακα και θα εκτυπώσουμε κάθε γραμμή ως λίστα τιμών κελιών.

```python
def print_table(enhanced_structure):
    """
    Prints each row of the first detected table.
    """
    # Step 3: Iterate over the rows of the first detected table and display cell text
    for row in enhanced_structure.tables[0].rows:
        print([cell.text for cell in row.cells])

if __name__ == "__main__":
    # Path to your image file
    image_path = "YOUR_DIRECTORY/table.png"

    # Run the pipeline
    raw = recognize_image(image_path)
    cleaned = enhance_structure(raw)
    print_table(cleaned)
```

**Τι θα δείτε:**  
Αν υποθέσουμε ότι το `table.png` περιέχει ένα απλό πλέγμα 3 × 2, η έξοδος μπορεί να είναι:

```
['Product', 'Price']
['Apple', '$1.20']
['Banana', '$0.80']
```

Αν το OCR χάσει μια κεφαλίδα, ο AI post‑processor πιθανότατα θα την προσθέσει βάσει του περιβάλλοντος, ώστε ο τελικός πίνακας να είναι έτοιμος για pandas ή οποιαδήποτε επόμενη ανάλυση.

> **Προσοχή σε:** Κενές γραμμές στο τέλος του πίνακα. Μερικές μηχανές OCR προσθέτουν μια κενή γραμμή όταν συναντούν λευκό χώρο. Ένας γρήγορος έλεγχος `if any(cell.text for cell in row.cells):` μπορεί να τις φιλτράρει.

---

## Bonus: Πέρα από το βασικό – Αποθήκευση του πίνακα σε CSV ή DataFrame

Οι περισσότερες πραγματικές ροές εργασίας χρειάζονται τα δεδομένα σε αρχείο CSV ή pandas DataFrame. Εδώ είναι ένα μικρό απόσπασμα που μετατρέπει τις εκτυπωμένες γραμμές σε CSV χωρίς να βγείτε από τη διαδικασία Python.

```python
import csv
import pandas as pd

def save_to_csv(enhanced_structure, output_path="output.csv"):
    rows = [
        [cell.text for cell in row.cells]
        for row in enhanced_structure.tables[0].rows
        if any(cell.text for cell in row.cells)  # Skip empty rows
    ]
    # Write CSV
    with open(output_path, "w", newline="", encoding="utf-8") as f:
        writer = csv.writer(f)
        writer.writerows(rows)

    # Also return a DataFrame for immediate use
    return pd.DataFrame(rows[1:], columns=rows[0])  # Assume first row is header

# Example usage:
df = save_to_csv(cleaned, "my_table.csv")
print(df.head())
```

Τώρα έχετε ένα έτοιμο DataFrame, τέλειο για analytics, visualisation ή για τροφοδοσία σε μοντέλο μηχανικής μάθησης.

---

## Συχνές Ερωτήσεις (FAQ)

**Ε: Λειτουργεί αυτό με PDF που περιέχουν σαρωμένους πίνακες;**  
Α: Απόλυτα—απλώς μετατρέψτε κάθε σελίδα PDF σε εικόνα (π.χ., με `pdf2image`) και τροφοδοτήστε τα PNG στην ίδια pipeline.

**Ε: Ο πίνακάς μου έχει συγχωνευμένα κελιά κεφαλίδας· θα το διορθώσει η AI;**  
Α: Ένας καλά εκπαιδευμένος post‑processor μπορεί να εντοπίσει συγχωνευμένα κελιά ελέγχοντας τα spans των κελιών. Αν χρησιμοποιείτε προσέγγιση βασισμένη σε κανόνες, ψάξτε για ίδιο κείμενο σε γειτονικά κελιά και συγχωνεύστε τα.

**Ε: Τι γίνεται αν το OCR επιστρέψει πολλαπλούς πίνακες;**  
Α: `enhanced_structure.tables` είναι μια λίστα. Μπορείτε να κάνετε βρόχο πάνω της ή να επιλέξετε αυτόν με τις περισσότερες γραμμές/στήλες—όπως ταιριάζει στις ανάγκες σας.

**Ε: Μπορώ να αντικαταστήσω τον AI post‑processor με μια απλή καθαριότητα regex;**  
Α: Ναι. Για πολλά έργα αρκούν μερικές αντικαταστάσεις regex (π.χ., διόρθωση “O” → “0”). Το κλειδί είναι να τρέχετε *κάτι* μετά το OCR για να βελτιώσετε **την ακρίβεια του OCR**.

---

## Συμπέρασμα

Δείξαμε πώς να **μετατρέψετε εικόνα σε πίνακα** με Python, από την ακατέργαστη αναγνώριση OCR μέχρι μια AI‑βελτιωμένη, έτοιμη δομή δεδομένων. Η τριπλή αλυσίδα—αναγνώριση, βελτίωση, εξαγωγή—καλύπτει τις κύριες προκλήσεις της **εξαγωγής πίνακα από εικόνα** και παρουσιάζει πρακτικούς τρόπους για **βελτίωση της ακρίβειας του OCR**.

Πάρτε ένα στιγμιότυπο οθόνης οποιουδήποτε spreadsheet, δείξτε το script σε αυτό και θα έχετε CSV ή DataFrame σε δευτερόλεπτα. Από εδώ μπορείτε να εξερευνήσετε πιο προχωρημένα κόλπα: πολυσελιδικά PDF, χειρόγραφους πίνακες ή ακόμη ζωντανές ροές κάμερας.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να τροφοδοτήσετε την pipeline με ζωντανά πλαίσια βίντεο ή πειραματιστείτε με post‑processors βασισμένους σε μοντέλα γλώσσας που μπορούν να εικάσουν λείποντα ονόματα στηλών. Ο ουρανός είναι το όριο, και τώρα έχετε μια σταθερή βάση για να χτίσετε πάνω της.

Καλή προγραμματιστική! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}