---
category: general
date: 2026-01-02
description: Εξαγωγή πίνακα από έγγραφο χρησιμοποιώντας Python. Μάθετε πώς να διαβάζετε
  πίνακες από PDF και να επαναλαμβάνετε τις γραμμές του πίνακα με μια καθαρή, επαναχρησιμοποιήσιμη
  λύση.
draft: false
keywords:
- extract table from document
- how to read tables from pdf
- how to iterate table rows
- pdf table extraction python
- document layout detection
language: el
og_description: Εξαγωγή πίνακα από έγγραφο σε Python. Αυτός ο οδηγός δείχνει πώς να
  διαβάζετε πίνακες από PDF και να επαναλαμβάνετε τις γραμμές του πίνακα με αξιόπιστη
  μηχανή.
og_title: Εξαγωγή πίνακα από έγγραφο – Πλήρες σεμινάριο Python
tags:
- Python
- PDF
- Data Extraction
title: Εξαγωγή πίνακα από έγγραφο – Οδηγός Python βήμα‑προς‑βήμα
url: /el/python/general/extract-table-from-document-step-by-step-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή πίνακα από έγγραφο – Πλήρες Python Tutorial

Έχετε ποτέ χρειαστεί να **extract table from document** αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είστε οι μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν δουλεύουν με PDF που κρύβουν δεδομένα μέσα σε πίνακες. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από μια πρακτική, ολοκληρωμένη λύση που όχι μόνο δείχνει **how to read tables from pdf** αρχεία, αλλά επίσης επιδεικνύει **how to iterate table rows** ώστε να μπορείτε να μεταφέρετε τα δεδομένα όπου χρειάζεται.

Φανταστείτε ότι έχετε μια σειρά από τιμολόγια, το καθένα με έναν πίνακα σύνοψης των γραμμών. Θέλετε αυτές τις γραμμές σε CSV για ανάλυση downstream. Στο τέλος αυτού του οδηγού θα έχετε ένα επαναχρησιμοποιήσιμο snippet που κάνει ακριβώς αυτό, συν λίγες συμβουλές για να αποφύγετε κοινά προβλήματα.

## Τι Θα Μάθετε

- Εντοπίστε τη διάταξη ενός εγγράφου με μια μηχανή layout.  
- Βελτιώστε την ακατέργαστη ανίχνευση χρησιμοποιώντας έναν post‑processor για πιο καθαρές δομές πινάκων.  
- Επανάληψη σε κάθε γραμμή του εντοπισμένου πίνακα και εκτύπωση (ή αποθήκευση) του περιεχομένου των κελιών.  

Δεν απαιτούνται εξωτερικές υπηρεσίες, δεν υπάρχει μαγική μαύρη κουτί—απλώς καθαρό Python και μια δημοφιλής βιβλιοθήκη OCR/layout (π.χ., **pdfplumber**, **pdfminer.six**, ή ένα ιδιόκτητο `engine` που ήδη χρησιμοποιείτε). Αν έχετε ήδη ένα αντικείμενο `engine` που υλοποιεί `recognize_layout()` και `run_postprocessor()`, μπορείτε να ενσωματώσετε τον κώδικα αμέσως.

> **Pro tip:** Αν χρησιμοποιείτε εμπορικό SDK, βεβαιωθείτε ότι ενεργοποιείτε τη λειτουργία “table detection”; διαφορετικά η ακατέργαστη διάταξη μπορεί να παραλείψει συγχωνευμένα κελιά.

---

## Βήμα 1: Εντοπισμός της Δομής του Πίνακα – Extract table from document

Το πρώτο που χρειάζεστε είναι μια ακατέργαστη διάταξη που σας λέει πού βρίσκονται οι πίνακες στη σελίδα. Οι περισσότερες σύγχρονες βιβλιοθήκες PDF εκθέτουν μια μέθοδο όπως `recognize_layout()` που επιστρέφει μια ιεραρχική δομή από blocks, lines και cells.

```python
# Step 1 – Detect the document layout using the engine
# ---------------------------------------------------
# `engine` is assumed to be an instantiated object from your PDF library.
# It could be pdfplumber, a custom OCR SDK, or any tool that supports layout detection.
raw_layout = engine.recognize_layout()
```

**Why this matters:**  
Η ακατέργαστη διάταξη σας δίνει συντεταγμένες για κάθε στοιχείο κειμένου, αλλά συχνά περιλαμβάνει θόρυβο—κεφαλίδες, υποσέλιδα ή τυχαίους χαρακτήρες που δεν ανήκουν στον πίνακα. Γι' αυτό το επόμενο βήμα είναι κρίσιμο.

> **Common question:** *What if my PDF has multiple pages?*  
> Η κλήση `recognize_layout()` συνήθως επιστρέφει μια λίστα αντικειμένων σελίδας. Κάντε βρόχο πάνω τους και εφαρμόστε την ίδια λογική post‑processing σε κάθε σελίδα.

---

## Βήμα 2: Βελτιώστε τον Εντοπισμό – How to read tables from pdf

Αφού έχετε το `raw_layout`, θα θέλετε να το καθαρίσετε. Οι περισσότερες μηχανές παρέχουν έναν post‑processor που συγχωνεύει κατακερματισμένα κελιά, αφαιρεί άσχετο κείμενο και δημιουργεί ένα σωστό αντικείμενο `Table`.

```python
# Step 2 – Refine the detected layout with the post‑processor
# ----------------------------------------------------------
# The post‑processor returns an enhanced layout where tables are
# represented as a list of rows, each row being a list of Cell objects.
enhanced_layout = engine.run_postprocessor(raw_layout)
```

**Why you need this:**  
Μια ακατέργαστη διάταξη μπορεί να αναφέρει μια μόνο γραμμή πίνακα ως δεκάδες μικρά κομμάτια. Ο post‑processor ομαδοποιεί αυτά τα κομμάτια σε λογικά κελιά, καθιστώντας την επανάληψη πολύ πιο απλή αργότερα.

> **Edge case:** Κάποια PDF χρησιμοποιούν αόρατα σύνορα. Αν παρατηρήσετε ελλιπείς γραμμές, ενεργοποιήστε τη σημαία “detect invisible lines” στη μηχανή σας (αν είναι διαθέσιμη).

---

## Βήμα 3: Επανάληψη Στις Γραμμές του Πίνακα – How to iterate table rows

Τώρα που έχετε μια καθαρή `enhanced_layout`, η εξαγωγή των δεδομένων είναι παιχνιδάκι. Παρακάτω κάνουμε βρόχο σε κάθε γραμμή, ενώσουμε τα κείμενα των κελιών με tabs (ώστε η έξοδος να ευθυγραμμίζεται ωραία) και εκτυπώνουμε το αποτέλεσμα. Μπορείτε να αντικαταστήσετε το `print` με οποιαδήποτε λογική αποθήκευσης—CSV writer, εισαγωγή σε βάση δεδομένων κ.λπ.

```python
# Step 3 – Print the table contents row by row
# --------------------------------------------
# `enhanced_layout.table` is expected to be an iterable of rows.
# Each `row` is a list of Cell objects with a `.text` attribute.
for row in enhanced_layout.table:
    # Join each cell's text with a tab to align columns
    print("\t".join(cell.text for cell in row))
```

**Expected output (example):**

```
Item	Qty	Price	Total
Widget A	2	$10.00	$20.00
Widget B	1	$15.00	$15.00
Service C	5	$8.00	$40.00
```

Αν χρειάζεστε CSV αντί για προβολή με tabs, απλώς αντικαταστήστε το `"\t".join(...)` με `",".join(...)` και γράψτε σε αρχείο.

---

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας τα παραπάνω, εδώ είναι ένα αυτόνομο script. Προσαρμόστε τις εισαγωγές και την αρχικοποίηση της μηχανής ώστε να ταιριάζει με τη βιβλιοθήκη που χρησιμοποιείτε.

```python
# --------------------------------------------------------------
# Full script: extract table from document and iterate rows
# --------------------------------------------------------------
import sys

# -----------------------------------------------------------------
# 1️⃣  Import or instantiate your PDF layout engine.
# Replace the placeholder with the actual library you use.
# -----------------------------------------------------------------
# Example with a fictional `pdf_engine` package:
# from pdf_engine import LayoutEngine
# engine = LayoutEngine(api_key="YOUR_KEY")
# -----------------------------------------------------------------
# For pdfplumber (open‑source) you could do:
# import pdfplumber
# engine = pdfplumber.open("sample.pdf")
# -----------------------------------------------------------------
# We'll keep it generic for the tutorial.
# -----------------------------------------------------------------

def extract_table(engine):
    """
    Detect, refine, and iterate over a table in a PDF document.
    Returns a list of rows, where each row is a list of cell strings.
    """
    # Detect layout
    raw_layout = engine.recognize_layout()

    # Refine layout
    enhanced_layout = engine.run_postprocessor(raw_layout)

    # Collect rows
    rows = []
    for row in enhanced_layout.table:
        rows.append([cell.text for cell in row])
    return rows

def main(pdf_path):
    # Initialise your engine – this will differ per library
    # Below is a stub; replace with real initialization.
    engine = initialize_engine(pdf_path)   # <-- implement this

    try:
        table_rows = extract_table(engine)
        for row in table_rows:
            print("\t".join(row))
    except Exception as e:
        print(f"❌ Extraction failed: {e}", file=sys.stderr)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python extract_table.py <path-to-pdf>")
    else:
        main(sys.argv[1])
```

**What to replace:**  

- `initialize_engine(pdf_path)`: Δημιουργήστε το αντικείμενο engine για την επιλεγμένη βιβλιοθήκη.  
- `engine.recognize_layout()` / `engine.run_postprocessor()`: Χρησιμοποιήστε τα σωστά ονόματα μεθόδων αν διαφέρουν.

Η εκτέλεση του script με `python extract_table.py invoice.pdf` θα εκτυπώσει έναν όμορφα μορφοποιημένο πίνακα με tabs, έτοιμο για downstream επεξεργασία.

---

## Εικονογραφική Παράσταση

Below is a quick schematic of what the detection pipeline looks

![extract table from document diagram showing raw layout → post‑processor → clean table]  

*Alt text:* *Διάγραμμα ροής εξαγωγής πίνακα από έγγραφο*  

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

| Ερώτηση | Απάντηση |
|----------|--------|
| **What if the PDF has multiple tables?** | Το `enhanced_layout.table` μπορεί να περιέχει μόνο τον πρώτο εντοπισμένο πίνακα. Κάντε βρόχο στο `enhanced_layout.tables` (σημειώστε το πληθυντικό) αν η βιβλιοθήκη το υποστηρίζει, και εφαρμόστε την ίδια λογική επανάληψης γραμμών σε κάθε έναν. |
| **How do I handle merged cells?** | Ο post‑processor συνήθως επεκτείνει τα συγχωνευμένα κελιά σε ξεχωριστές εγγραφές. Αν δεν το κάνει, ελέγξτε τη σημαία `merge_cells` της μηχανής ή συνδυάστε χειροκίνητα τα γειτονικά κελιά βάσει των συντεταγμένων τους. |
| **Can I extract tables from scanned PDFs?** | Ναι, αλλά θα χρειαστεί ένα βήμα OCR πριν από την ανίχνευση διάταξης. Πολλά SDK συνδυάζουν OCR + layout detection σε μία κλήση (`recognize_layout()` σε σκαναρισμένο έγγραφο). |
| **Performance concerns for large batches?** | Επεξεργαστείτε τις σελίδες παράλληλα (π.χ., με `concurrent.futures`). Το βαρύ μέρος είναι το OCR· κρατήστε το αντικείμενο engine ενεργό μεταξύ αρχείων για να αποφύγετε την επανεκκίνηση βαρέων μοντέλων. |
| **Do I need to install extra dependencies?** | Αν χρησιμοποιείτε `pdfplumber`, εγκαταστήστε το με `pip install pdfplumber`. Για εμπορικά SDK, ακολουθήστε τον οδηγό εγκατάστασης του προμηθευτή. |

---

## Συμπέρασμα

Μόλις δείξαμε πώς να **extract table from document** εντοπίζοντας τη διάταξη, βελτιώνοντάς την, και στη συνέχεια **iterating table rows** για να αποκτήσουμε καθαρά, χρήσιμα δεδομένα. Είτε τροφοδοτείτε ένα data‑warehouse, δημιουργείτε αναφορές, είτε απλώς μετατρέπετε PDF σε CSV, το μοτίβο παραμένει το ίδιο: εντοπισμός → καθαρισμός → επανάληψη.

Επόμενα βήματα που μπορείτε να εξερευνήσετε:

- **How to read tables from pdf** με πρόσθετες πληροφορίες στυλ (γραμματοσειρές, χρώματα).  
- Εξαγωγή απευθείας σε **pandas DataFrames** για ανάλυση.  
- Χρήση του ίδιου pipeline για **write tables back** σε νέο PDF (αντίστροφη ροή).  

Δοκιμάστε το script με μερικά από τα δικά σας PDF και δείτε πόσο γρήγορα μπορείτε να μετατρέψετε στατικούς πίνακες σε ενεργά δεδομένα. Καλή εξαγωγή!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}