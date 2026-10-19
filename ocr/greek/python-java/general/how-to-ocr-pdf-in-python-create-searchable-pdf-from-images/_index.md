---
category: general
date: 2026-06-06
description: Πώς να κάνετε OCR σε PDF και να δημιουργήσετε αναζητήσιμα αρχεία PDF
  από εικόνες χρησιμοποιώντας Python. Μάθετε να προσθέτετε αναζητήσιμο κείμενο και
  να μετατρέπετε εικόνα σε PDF/A σε λίγα λεπτά.
draft: false
keywords:
- how to ocr pdf
- create searchable pdf
- add searchable text
- ocr image to pdf
- convert image to pdf/a
language: el
og_description: Πώς να κάνετε OCR σε PDF βήμα‑βήμα. Μάθετε πώς να προσθέτετε αναζητήσιμο
  κείμενο και να μετατρέπετε εικόνα σε PDF/A χρησιμοποιώντας ένα απλό script Python.
og_title: Πώς να κάνετε OCR PDF – Σύντομος οδηγός για τη δημιουργία PDF με δυνατότητα
  αναζήτησης
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  headline: How to OCR PDF in Python – Create Searchable PDF from Images
  type: TechArticle
- description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  name: How to OCR PDF in Python – Create Searchable PDF from Images
  steps:
  - name: Why this matters
    text: '- **Preserving graphics** means the visual layout (tables, logos, stamps)
      stays exactly as the scanner captured it. - The `result` object typically contains
      a hidden text layer that we’ll later embed into the PDF. - Using `recognize_image`
      instead of `recognize_pdf` avoids an extra conversion step, '
  - name: Why this matters
    text: '- **Searchable PDF**: The output file contains a hidden, selectable text
      layer. You can now Ctrl + F through the document. - **PDF/A compliance**: Some
      organizations (legal, finance) require PDF/A for audit trails; this step satisfies
      that rule automatically. - The method also **adds searchable text'
  - name: Expected output
    text: 'When you run the script, the console prints:'
  type: HowTo
tags:
- OCR
- PDF
- Python
- Automation
title: Πώς να κάνετε OCR PDF σε Python – Δημιουργήστε Αναζητήσιμο PDF από Εικόνες
url: /el/python-java/general/how-to-ocr-pdf-in-python-create-searchable-pdf-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να OCR PDF – Μετατρέψτε Σαρωμένες Εικόνες σε Αναζητήσιμα PDF

Έχετε αναρωτηθεί ποτέ **πώς να OCR PDF** όταν το μόνο που έχετε είναι μια σαρωμένη εικόνα από τιμολόγιο ή απόδειξη; Δεν είστε οι μόνοι. Σε πολλά γραφεία τα εισερχόμενα έγγραφα φτάνουν ως επίπεδα PNG ή JPEG, και το επόμενο βήμα — η μετατροπή του περιεχομένου σε αναζητήσιμο — φαίνεται σαν μαύρο κουτί.

Τα καλά νέα; Με λίγες γραμμές Python μπορείτε να **δημιουργήσετε αναζητήσιμα PDF**, **προσθέσετε αναζητήσιμο κείμενο**, και ακόμη **μετατρέψετε εικόνα σε PDF/A** για μακροπρόθεσμη αρχειοθέτηση. Σε αυτό το tutorial θα περάσουμε από κάθε βήμα, θα εξηγήσουμε γιατί είναι σημαντικό, και θα σας δώσουμε ένα έτοιμο script που μπορείτε να ενσωματώσετε σε οποιοδήποτε project.

> **Pro tip:** Η ίδια προσέγγιση λειτουργεί για σαρώσεις πολλαπλών σελίδων· απλώς κάντε βρόχο πάνω στα αρχεία και η μηχανή θα κάνει το σκληρό κομμάτι.

---

## Τι Θα Χρειαστείτε

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τα παρακάτω στον υπολογιστή σας:

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|------------------------|
| Python 3.9 or newer | Σύγχρονη σύνταξη και καλύτερη υποστήριξη βιβλιοθηκών |
| `pdfium`‑based OCR engine (e.g., `pdfocr` or a commercial SDK) | Διαχειρίζεται τόσο την αναγνώριση εικόνας όσο και τη δημιουργία PDF/A |
| An image file (PNG, JPEG, TIFF) you want to turn into a searchable PDF | Η πηγή του κειμένου |
| Write permission to the output folder | Για να μπορεί το script να αποθηκεύσει το νέο PDF |

Αν δεν έχετε εγκαταστήσει ακόμη το OCR SDK, τρέξτε:

```bash
pip install pdfocr   # replace with your vendor's package name
```

Αυτό είναι όλο — χωρίς πολύπλοκες εξαρτήσεις συστήματος, μόνο μια εγκατάσταση pip.

---

## Πώς να OCR PDF – Επισκόπηση

Σε υψηλό επίπεδο η διαδικασία αποτελείται από τρεις απλές ενέργειες:

1. **Αναγνώριση** του κειμένου μέσα στην εικόνα διατηρώντας τα αρχικά γραφικά.  
2. **Εξαγωγή** του αποτελέσματος OCR μαζί με την αρχική εικόνα ως **αναζητήσιμο PDF/A** (η έκδοση PDF φιλική προς την αρχειοθέτηση).  
3. **Επικύρωση** ότι το παραγόμενο αρχείο περιέχει επιλέξιμο, αναζητήσιμο κείμενο επάνω από την αρχική εικόνα.

Παρακάτω θα δείτε κάθε βήμα σε κώδικα, με εξηγήσεις του *γιατί* πίσω από τις εντολές.

---

## Βήμα 1: Αναγνώριση Κειμένου από την Εικόνα

Πρώτα ζητάμε από τη μηχανή OCR να διαβάσει τα pixel και να επιστρέψει ένα αντικείμενο αποτελέσματος που περιέχει τόσο την ακατέργαστη εικόνα όσο και το εξαγόμενο κείμενο. Σκεφτείτε το σαν η μηχανή “διαβάζει” το τιμολόγιο για εσάς.

```python
# Step 1: Recognize text from the image and keep the original graphics
result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

### Γιατί είναι σημαντικό

- **Διατήρηση γραφικών** σημαίνει ότι η οπτική διάταξη (πίνακες, λογότυπα, σφραγίδες) παραμένει ακριβώς όπως την κατέγραψε ο σαρωτής.  
- Το αντικείμενο `result` συνήθως περιέχει ένα κρυφό στρώμα κειμένου που θα ενσωματώσουμε αργότερα στο PDF.  
- Η χρήση του `recognize_image` αντί του `recognize_pdf` αποφεύγει ένα επιπλέον βήμα μετατροπής, κάτι που επιταχύνει την επεξεργασία για εικόνες μονής σελίδας.

#### Συνηθισμένες παραλλαγές

- Αν έχετε ένα **πολυσελιδικό TIFF**, περάστε τη διαδρομή του αρχείου απευθείας· οι περισσότερες μηχανές θα αντιμετωπίσουν κάθε σελίδα ως ξεχωριστή εικόνα.  
- Για PDF που ήδη περιέχουν εικόνες, μπορείτε να καλέσετε `engine.recognize_pdf("file.pdf")` και να παραλείψετε εντελώς αυτό το βήμα.

---

## Βήμα 2: Εξαγωγή Αποτελέσματος OCR ως Αναζητήσιμο PDF/A

Τώρα παίρνουμε το `result` από το βήμα 1 και λέμε στη μηχανή να γράψει ένα νέο αρχείο. Η βασική σημαία εδώ είναι *PDF/A* — η έκδοση του PDF σύμφωνα με το πρότυπο ISO για μακροπρόθεσμη διατήρηση.

```python
# Step 2: Export the OCR result together with the original image as a searchable PDF/A
result.save_as_pdfa("YOUR_DIRECTORY/invoice_searchable.pdf")
```

### Γιατί είναι σημαντικό

- **Αναζητήσιμο PDF**: Το αρχείο εξόδου περιέχει ένα κρυφό, επιλέξιμο στρώμα κειμένου. Μπορείτε τώρα να κάνετε Ctrl + F στο έγγραφο.  
- **Συμμόρφωση PDF/A**: Ορισμένοι οργανισμοί (νομικοί, χρηματοοικονομικοί) απαιτούν PDF/A για αρχειακά ίχνη· αυτό το βήμα ικανοποιεί αυτόν τον κανόνα αυτόματα.  
- Η μέθοδος επίσης **προσθέτει αναζητήσιμο κείμενο** χωρίς να επίπεδωση της εικόνας, έτσι η οπτική πιστότητα παραμένει τέλεια.

#### Ειδική περίπτωση: Χρειάζεστε κανονικό PDF;

Αν δεν σας ενδιαφέρει το PDF/A, αντικαταστήστε το `save_as_pdfa` με `save_as_pdf`. Το υπόλοιπο της ροής παραμένει το ίδιο.

---

## Βήμα 3: Επαλήθευση του Αναζητήσιμου PDF

Μια γρήγορη επιβεβαίωση σας σώζει από μυστηριώδη σφάλματα αργότερα. Ανοίξτε το παραγόμενο αρχείο σε οποιονδήποτε προβολέα PDF, δοκιμάστε να επιλέξετε μια λέξη και χρησιμοποιήστε τη λειτουργία αναζήτησης.

```python
# Step 3: The file "invoice_searchable.pdf" now contains selectable text layered over the original invoice image
import subprocess, os

pdf_path = "YOUR_DIRECTORY/invoice_searchable.pdf"
if os.path.exists(pdf_path):
    print(f"✅ PDF created successfully: {pdf_path}")
    # Optionally open the file (works on macOS, Windows, Linux with appropriate commands)
    subprocess.run(["open", pdf_path] if os.name == "posix" else ["start", pdf_path], shell=True)
else:
    print("❌ Something went wrong – PDF not found.")
```

### Αναμενόμενη έξοδος

Όταν τρέξετε το script, η κονσόλα εκτυπώνει:

```
✅ PDF created successfully: YOUR_DIRECTORY/invoice_searchable.pdf
```

Ανοίγοντας το αρχείο, θα δείτε την αρχική εικόνα του τιμολογίου με ένα αχνό, αόρατο στρώμα κειμένου. Επισημάνετε οποιαδήποτε λέξη και θα παρατηρήσετε ότι είναι επιλέξιμη — **αυτό είναι το αναζητήσιμο κείμενο** που μόλις προσθέσατε.

---

## Προσθήκη Αναζητήσιμου Κειμένου σε Υπάρχοντα PDF (Bonus)

Μερικές φορές έχετε ήδη ένα PDF αλλά χρειάζεται να **προσθέσετε αναζητήσιμο κείμενο** σε αυτό. Η ίδια μηχανή μπορεί να επικάλυψει τα αποτελέσματα OCR πάνω σε ένα υπάρχον PDF:

```python
# Bonus: Add searchable text to an existing PDF file
existing_pdf = engine.load_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result = engine.recognize_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result.apply_to(existing_pdf).save_as_pdfa("YOUR_DIRECTORY/old_scanned_searchable.pdf")
```

Εδώ το `apply_to` συγχωνεύει το κρυφό στρώμα με τις αρχικές σελίδες, επιτρέποντάς σας να **δημιουργήσετε αναζητήσιμο PDF** χωρίς επανασάρωση.

---

## Συνηθισμένα Προβλήματα και Συμβουλές

| Πρόβλημα | Πώς να το αποφύγετε |
|----------|----------------------|
| **Πηγές εικόνας χαμηλής ανάλυσης** (< 150 dpi) | Μεγαλώστε ή ζητήστε σαρωτικό υψηλότερης ανάλυσης· η ακρίβεια OCR πέφτει δραματικά κάτω από 150 dpi. |
| **Απουσία δεδομένων γλώσσας** | Εγκαταστήστε τα κατάλληλα πακέτα γλώσσας για τη μηχανή OCR (`pip install pdfocr[eng,spa]`). |
| **Ο φάκελος εξόδου δεν είναι εγγράψιμος** | Εκτελέστε το script με επαρκή δικαιώματα ή επιλέξτε διαφορετικό κατάλογο. |
| **Αποτυχία επικύρωσης PDF/A** | Βεβαιωθείτε ότι δεν ενσωματώνετε μη υποστηριζόμενες γραμματοσειρές ή JavaScript· οι περισσότερες SDK το διαχειρίζονται αυτόματα όταν χρησιμοποιείτε `save_as_pdfa`. |

---

## Πλήρες Script – Λύση Μίας-Αρχείου

Παρακάτω είναι ένα αυτόνομο script που ενώνει όλα τα παραπάνω. Αντιγράψτε‑και‑επικολλήστε, αντικαταστήστε τις διαδρομές placeholder, και είστε έτοιμοι να **μετατρέψετε εικόνα σε PDF/A** σε δευτερόλεπτα.

```python
#!/usr/bin/env python3
"""
How to OCR PDF – Complete script to create a searchable PDF/A from an image.
Works with any OCR engine exposing `recognize_image` and `save_as_pdfa`.
"""

import os
import subprocess

# ----------------------------------------------------------------------
# CONFIGURATION – change these paths to match your environment
# ----------------------------------------------------------------------
INPUT_IMAGE = "YOUR_DIRECTORY/invoice.png"
OUTPUT_PDF  = "YOUR_DIRECTORY/invoice_searchable.pdf"

# ----------------------------------------------------------------------
# INITIALIZE THE OCR ENGINE (replace with your SDK's init call)
# ----------------------------------------------------------------------
# Example for a fictional `pdfocr` package:
# from pdfocr import Engine
# engine = Engine(api_key="YOUR_API_KEY")
# If you use a different library, adjust the import and init accordingly.
engine = Engine()  # placeholder – insert real initialization here

def main():
    # Step 1 – Recognize the image
    print(f"🔎 Recognizing text from {INPUT_IMAGE} …")
    result = engine.recognize_image(INPUT_IMAGE)

    # Step 2 – Save as searchable PDF/A
    print(f"💾 Saving searchable PDF/A to {OUTPUT_PDF} …")
    result.save_as_pdfa(OUTPUT_PDF)

    # Step 3 – Verify the file exists
    if os.path.isfile(OUTPUT_PDF):
        print("✅ Success! Searchable PDF/A created.")
        # Open the file for a quick visual check (optional)
        try:
            if os.name == "posix":
                subprocess.run(["open", OUTPUT_PDF])
            else:
                subprocess.run(["start", OUTPUT_PDF], shell=True)
        except Exception:
            pass
    else:
        print("❌ Error: PDF not created.")

if __name__ == "__main__":
    main()
```

**Τι κάνει αυτό το script:**  
1. Φορτώνει τη μηχανή OCR.  
2. Διαβάζει την επιλεγμένη εικόνα και εξάγει το κείμενο.  
3. Γράφει ένα **αναζητήσιμο PDF/A** που μπορείτε άμεσα να διανείμετε ή να αρχειοθετήσετε.  

Μπορείτε ελεύθερα να τυλίξετε τη λογική `main` σε μια συνάρτηση που επεξεργάζεται ολόκληρο φάκελο — απλώς επαναλάβετε `os.listdir()` και εκτελέστε τα τρία βήματα για κάθε αρχείο.

---

## Επόμενα Βήματα & Σχετικά Θέματα

Τώρα που έχετε κατακτήσει **πώς να OCR PDF**, σκεφτείτε τις παρακάτω ιδέες για επέκταση:

- **Επεξεργασία παρτίδας:** Χρησιμοποιήστε `concurrent.futures` για OCR δεκάδων τιμολογίων παράλληλα.  
- **Ένθεση μεταδεδομένων:** Προσθέστε ημερομηνίες δημιουργίας ή αριθμούς τιμολογίων στα μεταδεδομένα του PDF για ευκολότερη ευρετηρίαση.  
- **Υβριδικά PDF:** Συνδυάστε αναζητήσιμο κείμενο με ενσωματωμένες αρχικές εικόνες για ένα “ψηφιακό δίδυμο” του έντυπου εγγράφου.  
- **Εναλλακτικές εξόδους:** Εξάγετε σε **DOCX** ή **HTML** αν τα επόμενα συστήματα απαιτούν επεξεργάσιμες μορφές.

Κάθε μία από αυτές τις προσεγγίσεις βασίζεται στις βασικές έννοιες που μόλις μάθατε — αναγνώριση, εξαγωγή, επαλήθευση.

---

## Συμπέρασμα

Με λίγες μόνο γραμμές Python, τώρα ξέρετε **πώς να OCR PDF** μετατρέποντας μια απλή εικόνα σε **αναζητήσιμο PDF/A**. Το script αναλαμβάνει το δύσκολο κομμάτι, διατηρεί τα αρχικά γραφικά και σας δίνει ένα σύμφωνο πρότυπο έγγραφο που μπορείτε να αναζητήσετε, να αρχειοθετήσετε ή να μοιραστείτε.

Δοκιμάστε το με τα δικά σας τιμολόγια, αποδείξεις ή σαρωμένα συμβόλαια. Αν συναντήσετε δυσκολίες, αφήστε ένα σχόλιο παρακάτω ή ελέγξτε την επίσημη τεκμηρίωση του SDK — συνήθως περιέχει επιπλέον παραδείγματα. Καλή κωδικοποίηση, και απολαύστε τη νέα δυνατότητα να κάνετε οποιαδήποτε εικόνα άμεσα αναζητήσιμη!

![Παράδειγμα OCR PDF που δείχνει την αρχική εικόνα και το επικάλυμμα του αναζητήσιμου PDF](placeholder.png "Παράδειγμα OCR PDF")

## Τι Πρέπει να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας projects.

- [Πώς να OCR PDF σε .NET με Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Αναγνώριση Κειμένου PDF – Λειτουργίες OCR με Aspose.OCR για Java](/ocr/english/java/ocr-operations/)
- [Μετατροπή Εικόνων σε PDF C# – Αποθήκευση Πολυσελιδικού Αποτελέσματος OCR](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}