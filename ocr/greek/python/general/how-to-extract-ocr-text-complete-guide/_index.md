---
category: general
date: 2026-02-22
description: Μάθετε πώς να εξάγετε κείμενο OCR και να βελτιώσετε την ακρίβεια του
  OCR με επεξεργασία AI. Καθαρίστε εύκολα το κείμενο OCR σε Python με ένα βήμα‑προς‑βήμα
  παράδειγμα.
draft: false
keywords:
- how to extract OCR
- improve OCR accuracy
- clean OCR text
- OCR post‑processing
- AI OCR enhancement
language: el
og_description: Ανακαλύψτε πώς να εξάγετε κείμενο OCR, να βελτιώσετε την ακρίβεια
  του OCR και να καθαρίσετε το κείμενο OCR χρησιμοποιώντας μια απλή ροή εργασίας Python
  με επεξεργασία AI μετά‑εξαγωγής.
og_title: Πώς να εξάγετε κείμενο OCR – Οδηγός βήμα‑προς‑βήμα
tags:
- OCR
- AI
- Python
title: Πώς να εξάγετε κείμενο OCR – Πλήρης οδηγός
url: /el/python/general/how-to-extract-ocr-text-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εξάγετε Κείμενο OCR – Πλήρης Προγραμματιστική Εκμάθηση

Έχετε αναρωτηθεί ποτέ **πώς να εξάγετε OCR** από ένα σαρωμένο έγγραφο χωρίς να καταλήξετε σε ένα χάος ορθογραφικών λαθών και σπασμένων γραμμών; Δεν είστε μόνοι. Σε πολλά πραγματικά έργα η ακατέργαστη έξοδος από μια μηχανή OCR μοιάζει με ένα ακατάστατο παράγραφο, και ο καθαρισμός του μοιάζει με κουραστική εργασία.  

Τα καλά νέα; Ακολουθώντας αυτόν τον οδηγό θα δείτε έναν πρακτικό τρόπο να εξάγετε δομημένα δεδομένα OCR, να τρέξετε έναν AI post‑processor, και να καταλήξετε με **καθαρό κείμενο OCR** έτοιμο για ανάλυση downstream. Θα αγγίξουμε επίσης τεχνικές για **βελτίωση της ακρίβειας του OCR** ώστε τα αποτελέσματα να είναι αξιόπιστα από την πρώτη φορά.

Στα επόμενα λεπτά θα καλύψουμε όλα όσα χρειάζεστε: τις απαιτούμενες βιβλιοθήκες, ένα πλήρες εκτελέσιμο σενάριο, και συμβουλές για αποφυγή κοινών παγίδων. Χωρίς ασαφείς «δείτε την τεκμηρίωση» συντομεύσεις—απλώς μια ολοκληρωμένη, αυτόνομη λύση που μπορείτε να αντιγράψετε‑επικολλήσετε και να τρέξετε.

## Τι Θα Χρειαστεί

- Python 3.9+ (ο κώδικας χρησιμοποιεί type hints αλλά λειτουργεί και σε παλαιότερες εκδόσεις 3.x)
- Μηχανή OCR που μπορεί να επιστρέψει δομημένο αποτέλεσμα (π.χ., Tesseract μέσω `pytesseract` με τη σημαία `--psm 1`, ή εμπορικό API που προσφέρει μεταδεδομένα block/line)
- Μοντέλο AI post‑processing – για αυτό το παράδειγμα θα το προσομοιώσουμε με μια απλή συνάρτηση, αλλά μπορείτε να το αντικαταστήσετε με το `gpt‑4o-mini` της OpenAI, Claude, ή οποιοδήποτε LLM που δέχεται κείμενο και επιστρέφει καθαρισμένο αποτέλεσμα
- Μερικές γραμμές δείγματος εικόνας (PNG/JPG) για δοκιμή

Αν έχετε όλα αυτά έτοιμα, ας βουτήξουμε.

## Πώς να Εξάγετε OCR – Αρχική Ανάκτηση

Το πρώτο βήμα είναι να καλέσετε τη μηχανή OCR και να της ζητήσετε μια **δομημένη αναπαράσταση** αντί για απλό string. Τα δομημένα αποτελέσματα διατηρούν τα όρια block, line και word, κάτι που κάνει τον επόμενο καθαρισμό πολύ πιο εύκολο.

```python
import pytesseract
from PIL import Image
from dataclasses import dataclass, field
from typing import List

# Simple data classes mirroring a typical structured OCR response
@dataclass
class Line:
    text: str

@dataclass
class Block:
    lines: List[Line] = field(default_factory=list)

@dataclass
class StructuredResult:
    blocks: List[Block] = field(default_factory=list)

def recognize_structured(image_path: str) -> StructuredResult:
    """
    Run Tesseract with the `--psm 1` layout mode to get block/line info.
    In a real engine you would get JSON directly; here we simulate it.
    """
    img = Image.open(image_path)

    # Tesseract's TSV output includes level, page_num, block_num, par_num, line_num, word_num, text…
    tsv = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT)

    result = StructuredResult()
    current_block_idx = -1
    current_line_idx = -1

    for i, level in enumerate(tsv["level"]):
        if level == 3:  # block level
            result.blocks.append(Block())
            current_block_idx += 1
            current_line_idx = -1
        elif level == 4:  # line level
            result.blocks[current_block_idx].lines.append(Line(text=""))
            current_line_idx += 1

        # level 5 is word; concatenate words into the current line
        if level == 5:
            word = tsv["text"][i]
            if word.strip():
                line_obj = result.blocks[current_block_idx].lines[current_line_idx]
                line_obj.text += (word + " ")

    # Trim trailing spaces
    for block in result.blocks:
        for line in block.lines:
            line.text = line.text.strip()
    return result
```

> **Γιατί είναι σημαντικό:** Διατηρώντας τα blocks και τις lines αποφεύγουμε να μαντέψουμε πού αρχίζουν οι παράγραφοι. Η συνάρτηση `recognize_structured` μας δίνει μια καθαρή ιεραρχία που μπορούμε αργότερα να περάσουμε σε ένα μοντέλο AI.

```python
# Demo call – replace with your own image path
structured_result = recognize_structured("sample_scan.png")
print("Before AI:", structured_result.blocks[0].lines[0].text)
```

Η εκτέλεση του αποσπάσματος εκτυπώνει την πρώτη γραμμή ακριβώς όπως την είδε η μηχανή OCR, η οποία συχνά περιέχει λανθασμένες αναγνώσεις όπως “0cr” αντί για “OCR”.

## Βελτιώστε την Ακρίβεια του OCR με AI Post‑Processing

Τώρα που έχουμε το ακατέργαστο δομημένο αποτέλεσμα, ας το περάσουμε σε έναν AI post‑processor. Ο στόχος είναι να **βελτιώσουμε την ακρίβεια του OCR** διορθώνοντας κοινά λάθη, κανονικοποιώντας την στίξη, και ακόμη επανακαθορίζοντας τις γραμμές όταν χρειάζεται.

```python
import openai  # Example: using OpenAI's API; replace with your provider

def run_postprocessor(structured: StructuredResult) -> StructuredResult:
    """
    Sends each line to an LLM that returns a cleaned version.
    This simple loop can be parallelized for large documents.
    """
    api_key = "YOUR_OPENAI_API_KEY"
    openai.api_key = api_key

    for block in structured.blocks:
        for line in block.lines:
            prompt = (
                "You are an OCR cleanup assistant. Fix any spelling, spacing, "
                "or punctuation errors in the following line while preserving the original meaning:\n\n"
                f"\"{line.text}\""
            )
            response = openai.ChatCompletion.create(
                model="gpt-4o-mini",
                messages=[{"role": "user", "content": prompt}],
                temperature=0.0,
                max_tokens=200,
            )
            cleaned = response.choices[0].message.content.strip()
            line.text = cleaned
    return structured
```

> **Pro tip:** Αν δεν έχετε συνδρομή σε LLM, μπορείτε να αντικαταστήσετε την κλήση με έναν τοπικό transformer (π.χ., `sentence‑transformers` + ένα προσαρμοσμένο μοντέλο διόρθωσης) ή ακόμη και με μια προσέγγιση βασισμένη σε κανόνες. Η βασική ιδέα είναι ότι το AI βλέπει κάθε γραμμή ξεχωριστά, κάτι που συνήθως αρκεί για **καθαρισμό του κειμένου OCR**.

```python
# Apply the AI post‑processor
structured_result = run_postprocessor(structured_result)
print("After AI:", structured_result.blocks[0].lines[0].text)
```

Τώρα θα πρέπει να δείτε μια πολύ πιο καθαρή πρόταση—τα τυπογραφικά λάθη έχουν αντικατασταθεί, τα επιπλέον κενά έχουν αφαιρεθεί, και η στίξη έχει διορθωθεί.

## Καθαρισμός Κειμένου OCR για Καλύτερα Αποτελέσματα

Ακόμη και μετά τη διόρθωση από το AI, ίσως θελήσετε να εφαρμόσετε ένα τελικό βήμα εξαγωγής: αφαίρεση μη‑ASCII χαρακτήρων, ενοποίηση αλλαγών γραμμής, και συμπίεση πολλαπλών κενών. Αυτό το επιπλέον πέρασμα εξασφαλίζει ότι η έξοδος είναι έτοιμη για downstream εργασίες όπως NLP ή εισαγωγή σε βάση δεδομένων.

```python
import re

def final_cleanup(structured: StructuredResult) -> str:
    """
    Flattens the hierarchy into a single string and performs
    additional regex‑based cleaning.
    """
    lines = []
    for block in structured.blocks:
        for line in block.lines:
            # Remove any lingering non‑printable characters
            cleaned = re.sub(r"[^\x20-\x7E]", "", line.text)
            # Collapse multiple spaces
            cleaned = re.sub(r"\s+", " ", cleaned).strip()
            lines.append(cleaned)
    # Join blocks with double newline to preserve paragraph breaks
    return "\n\n".join(lines)

clean_text = final_cleanup(structured_result)
print("\n=== Cleaned OCR Text ===\n")
print(clean_text)
```

Η συνάρτηση `final_cleanup` σας δίνει ένα απλό string που μπορείτε να περάσετε απευθείας σε ευρετήριο αναζήτησης, μοντέλο γλώσσας, ή εξαγωγή CSV. Επειδή διατηρήσαμε τα όρια block, η δομή των παραγράφων παραμένει αμετάβλητη.

## Ακραίες Περιπτώσεις & Σενάρια “Τι‑Αν”

- **Διατάξεις πολλαπλών στηλών:** Αν η πηγή σας έχει στήλες, η μηχανή OCR μπορεί να αναμιγνύει γραμμές. Μπορείτε να εντοπίσετε τις συντεταγμένες των στηλών από το TSV output και να επαναδιατάξετε τις γραμμές πριν τις στείλετε στο AI.
- **Μη‑λατινικά αλφάβητα:** Για γλώσσες όπως τα Κινέζικα ή τα Αραβικά, αλλάξτε το prompt του LLM ώστε να ζητά διόρθωση ειδικά για τη γλώσσα, ή χρησιμοποιήστε μοντέλο που έχει εκπαιδευτεί σε αυτό το σενάριο.
- **Μεγάλα έγγραφα:** Η αποστολή κάθε γραμμής ξεχωριστά μπορεί να είναι αργή. Ομαδοποιήστε γραμμές (π.χ., 10 ανά αίτηση) και αφήστε το LLM να επιστρέψει μια λίστα καθαρισμένων γραμμών. Θυμηθείτε να σεβαστείτε τα όρια token.
- **Απουσία blocks:** Κάποιες μηχανές OCR επιστρέφουν μόνο μια επίπεδη λίστα λέξεων. Σε αυτήν την περίπτωση, μπορείτε να ανακατασκευάσετε τις γραμμές ομαδοποιώντας λέξεις με παρόμοιες τιμές `line_num`.

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι ένα ενιαίο αρχείο που μπορείτε να τρέξετε από άκρη σε άκρη. Αντικαταστήστε τα placeholders με το δικό σας κλειδί API και τη διαδρομή της εικόνας.

```python
# ocr_cleanup.py
import re
import pytesseract
from PIL import Image
from dataclasses import dataclass, field
from typing import List
import openai

# ---------- Data structures ----------
@dataclass
class Line:
    text: str

@dataclass
class Block:
    lines: List[Line] = field(default_factory=list)

@dataclass
class StructuredResult:
    blocks: List[Block] = field(default_factory=list)

# ---------- Step 1: Extract OCR ----------
def recognize_structured(image_path: str) -> StructuredResult:
    img = Image.open(image_path)
    tsv = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT)

    result = StructuredResult()
    cur_block = -1
    cur_line = -1

    for i, lvl in enumerate(tsv["level"]):
        if lvl == 3:                # block
            result.blocks.append(Block())
            cur_block += 1
            cur_line = -1
        elif lvl == 4:              # line
            result.blocks[cur_block].lines.append(Line(text=""))
            cur_line += 1
        elif lvl == 5:              # word
            word = tsv["text"][i]
            if word.strip():
                result.blocks[cur_block].lines[cur_line].text += word + " "

    # Trim spaces
    for blk in result.blocks:
        for ln in blk.lines:
            ln.text = ln.text.strip()
    return result

# ---------- Step 2: AI post‑processor ----------
def run_postprocessor(structured: StructuredResult) -> StructuredResult:
    openai.api_key = "YOUR_OPENAI_API_KEY"
    for block in structured.blocks:
        for line in block.lines:
            prompt = (
                "Correct OCR errors (spelling, spacing, punctuation) in this line:\n"
                f"\"{line.text}\""
            )
            resp = openai.ChatCompletion.create(
                model="gpt-4o-mini",
                messages=[{"role": "user", "content": prompt}],
                temperature=0.0,
                max_tokens=150,
            )
            line.text = resp.choices[0].message.content.strip()
    return structured

# ---------- Step 3: Final cleanup ----------
def final_cleanup(structured: StructuredResult) -> str:
    out = []
    for block in structured.blocks:
        for line in block.lines:
            txt = re.sub(r"[^\x20-\x7E]", "", line.text)   # strip non‑ASCII
            txt = re.sub(r"\s+", " ", txt).strip

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}