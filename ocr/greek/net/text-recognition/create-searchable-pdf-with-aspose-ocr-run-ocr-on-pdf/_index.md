---
category: general
date: 2026-05-28
description: Δημιουργήστε αναζητήσιμο PDF χρησιμοποιώντας το Aspose OCR σε C#. Μάθετε
  πώς να εκτελείτε OCR σε PDF, να αναγνωρίζετε κείμενο PDF και να μετατρέπετε ένα
  PDF σκαναρισμένο με OCR σε αναζητήσιμο PDF.
draft: false
keywords:
- create searchable pdf
- run ocr on pdf
- recognize text pdf
- ocr scanned pdf
- aspose ocr pdf
language: el
og_description: Δημιουργήστε PDF με δυνατότητα αναζήτησης χρησιμοποιώντας το Aspose
  OCR σε C#. Ακολουθήστε αυτόν τον οδηγό βήμα‑προς‑βήμα για να εκτελέσετε OCR σε PDF,
  να αναγνωρίσετε κείμενο σε PDF και να διαχειριστείτε αρχεία PDF που έχουν σαρωθεί
  με OCR.
og_title: Δημιουργία PDF με δυνατότητα αναζήτησης με Aspose OCR – Εκτέλεση OCR σε
  PDF
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Create searchable PDF using Aspose OCR in C#. Learn how to run OCR
    on PDF, recognize text PDF, and turn an OCR scanned PDF into a searchable PDF.
  headline: Create Searchable PDF with Aspose OCR – Run OCR on PDF
  type: TechArticle
- description: Create searchable PDF using Aspose OCR in C#. Learn how to run OCR
    on PDF, recognize text PDF, and turn an OCR scanned PDF into a searchable PDF.
  name: Create Searchable PDF with Aspose OCR – Run OCR on PDF
  steps:
  - name: Multiple Languages (OCR Scanned PDF)
    text: 'If your source PDF contains both English and Spanish text, combine languages:'
  - name: Password‑Protected PDFs
    text: 'When dealing with secured PDFs, supply the password before calling `Recognize`:'
  - name: Controlling Image Quality
    text: 'Higher DPI yields better OCR results but consumes more memory. Adjust the
      DPI if you notice garbled characters:'
  - name: License vs. Evaluation Mode
    text: 'In evaluation mode a watermark appears on each page. To remove it, apply
      your license before any OCR call:'
  - name: What’s Next?
    text: '- Explore the **aspose ocr pdf** API further: extract plain text, export
      to DOCX, or generate searchable PDFs in bulk. - Combine the searchable PDF output
      with Aspose.PDF to add bookmarks or watermarks. - Experiment with different
      DPI settings or custom OCR dictionaries for niche fonts.'
  type: HowTo
tags:
- Aspose
- OCR
- PDF
- C#
title: Δημιουργία Αναζητήσιμου PDF με Aspose OCR – Εκτέλεση OCR σε PDF
url: /el/net/text-recognition/create-searchable-pdf-with-aspose-ocr-run-ocr-on-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Αναζητήσιμου PDF με Aspose OCR – Εκτέλεση OCR σε PDF

Ποτέ χρειάστηκε να **δημιουργήσετε αναζητήσιμα PDF** αρχεία από ένα σωρό σαρωμένων εγγράφων; Δεν είστε μόνοι. Σε πολλές εργασιακές ροές το μόνο που εμποδίζει ένα πλήρως αναζητήσιμο αρχείο είναι μερικές γραμμές κώδικα που εκτελούν OCR σε σελίδες PDF.  

Σε αυτό το tutorial θα περάσουμε από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που δείχνει ακριβώς πώς να **δημιουργήσετε αναζητήσιμα PDF** αρχεία χρησιμοποιώντας τη βιβλιοθήκη Aspose OCR για .NET. Στο τέλος θα ξέρετε πώς να *εκτελέσετε OCR σε PDF*, *αναγνωρίσετε κείμενο PDF* αρχεία, και να μετατρέψετε ένα *OCR scanned PDF* σε αναζητήσιμη έκδοση χωρίς καμία υπηρεσία τρίτου.

> **Prerequisites** – Μία πρόσφατη .NET SDK (συνιστάται 6.0+), μια έγκυρη άδεια Aspose.OCR για .NET (ή ένα προσωρινό κλειδί αξιολόγησης), και ένα PDF που θέλετε να επεξεργαστείτε.

![Create searchable PDF diagram](alt="Διάγραμμα που απεικονίζει τη ροή δημιουργίας αναζητήσιμου PDF χρησιμοποιώντας Aspose OCR")  

---

## Τι Καλύπτει Αυτός Ο Οδηγός

- Ρύθμιση της βιβλιοθήκης Aspose OCR σε ένα έργο C#.  
- Φόρτωση ενός πηγαίου PDF (οποιοσδήποτε αριθμός σελίδων).  
- Διαμόρφωση της μηχανής για έξοδο **αναζητήσιμου PDF**.  
- Εκτέλεση της διαδικασίας OCR και αποθήκευση του αποτελέσματος.  
- Συμβουλές για διαχείριση εγγράφων πολλαπλών σελίδων, επιλογή γλώσσας, και κοινές παγίδες.  

Αν ακολουθήσετε κάθε βήμα, θα καταλήξετε με ένα αρχείο που μπορείτε να ανοίξετε στο Adobe Reader, να πατήσετε **Ctrl + F**, και να αναζητήσετε αμέσως οποιαδήποτε λέξη εμφανίστηκε στην αρχική σάρωση.

---

## Βήμα 1: Εγκατάσταση Aspose OCR για .NET

Πριν γράψετε κώδικα, προσθέστε το πακέτο NuGet στο έργο σας:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Χρησιμοποιήστε τη σημαία `--version` για να κλειδώσετε στην πιο πρόσφατη σταθερή έκδοση (π.χ., `Aspose.OCR 23.10`). Αυτό εξασφαλίζει συμβατότητα με .NET 6 και νεότερες εκδόσεις.

---

## Βήμα 2: Δημιουργία Αντικειμένου OCR Engine

Η καρδιά της διαδικασίας είναι το `OcrEngine`. Σκεφτείτε το ως τον εγκέφαλο που διαβάζει εικόνες και εξάγει κείμενο. Η αρχικοποίησή του είναι απλή:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace PdfSearchableDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Instantiate the OCR engine
            var ocrEngine = new OcrEngine();
```

Το αντικείμενο `OcrEngine` θα κρατά τόσο το ρεύμα εισόδου εικόνας όσο και τη διαμόρφωση που λέει στην Aspose πώς θέλετε το αποτέλεσμα.

---

## Βήμα 3: Φόρτωση του Πηγαίου PDF (Run OCR on PDF)

Η Aspose OCR μπορεί να επεξεργαστεί ένα PDF απευθείας· εξάγει κάθε σελίδα ως εικόνα εσωτερικά. Αντικαταστήστε τη διαδρομή placeholder με τη θέση του σαρωμένου εγγράφου σας:

```csharp
            // Step 3: Load the source PDF – this is where we *run OCR on PDF*
            string inputPath = @"C:\Docs\handbook.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);
```

> **Why this works:** Η μέθοδος `ImageStream.FromFile` εντοπίζει αυτόματα τη μορφή PDF και προετοιμάζει μια ραστερική αναπαράσταση για OCR. Δεν απαιτείται επιπλέον βήμα μετατροπής.

---

## Βήμα 4: Διαμόρφωση Μορφής Εξόδου και Γλώσσας

Εδώ λέμε στην Aspose τι θέλουμε πίσω. Ορίζοντας το `OutputFormat` σε `SearchablePdf` η μηχανή ενσωματώνει το αναγνωρισμένο κείμενο πίσω από τις αρχικές εικόνες της σελίδας, δημιουργώντας ένα **αναζητήσιμο PDF**. Μπορείτε επίσης να επιλέξετε τη γλώσσα για βελτιωμένη ακρίβεια—η προεπιλογή είναι τα Αγγλικά, αλλά μπορείτε να αλλάξετε σε Γαλλικά, Γερμανικά κ.λπ.

```csharp
            // Step 4: Choose output format and language
            ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf; // creates searchable PDF
            ocrEngine.Configuration.Language = Language.English;               // *recognize text PDF* in English
```

Αν χρειάζεται να επεξεργαστείτε ένα δίγλωσσο έγγραφο, μπορείτε να συνδυάσετε γλώσσες χρησιμοποιώντας τις σημαίες του enum `Language`.

---

## Βήμα 5: Εκτέλεση της Διαδικασίας OCR – Recognize Text PDF

Τώρα γίνεται η βαριά δουλειά. Η μέθοδος `Recognize` σαρώνει κάθε σελίδα, εξάγει γλύφους, και δημιουργεί ένα εσωτερικό ρεύμα PDF που περιέχει τόσο την αρχική εικόνα όσο και ένα αόρατο στρώμα κειμένου. Αυτό είναι το βήμα όπου *αναγνωρίζουμε κείμενο PDF*.

```csharp
            // Step 5: Execute OCR – this *recognizes text PDF* and builds the searchable stream
            ocrEngine.Recognize();
```

> **Common question:** *Τι γίνεται αν το PDF έχει 200 σελίδες;*  
> Η μηχανή επεξεργάζεται τις σελίδες διαδοχικά και ρέει τα αποτελέσματα, έτσι η κατανάλωση μνήμης παραμένει μέτρια. Ωστόσο, για εξαιρετικά μεγάλα αρχεία ίσως θελήσετε να αυξήσετε τη ρύθμιση `MemoryLimit` στο `ocrEngine.Configuration`.

---

## Βήμα 6: Αποθήκευση του Αναζητήσιμου PDF

Τέλος, γράψτε το αποτέλεσμα στο δίσκο. Η μέθοδος `Save` αποθηκεύει το εσωτερικό ρεύμα σε ένα νέο αρχείο που μπορείτε να ανοίξετε με οποιονδήποτε προβολέα PDF.

```csharp
            // Step 6: Save the searchable PDF to disk
            string outputPath = @"C:\Docs\handbook_searchable.pdf";
            ocrEngine.Save(outputPath);

            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

Τρέξτε το πρόγραμμα (`dotnet run`) και παρακολουθήστε την κονσόλα να επιβεβαιώνει τη δημιουργία του αρχείου. Ανοίξτε το `handbook_searchable.pdf` και δοκιμάστε να αναζητήσετε μια λέξη που ξέρετε ότι υπάρχει στην αρχική σάρωση – θα δείτε τα αποτελέσματα αμέσως.

---

## Διαχείριση Ειδικών Περιπτώσεων και Προχωρημένα Σενάρια

### Πολλαπλές Γλώσσες (OCR Scanned PDF)

Αν το πηγαίο PDF περιέχει κείμενο τόσο στα Αγγλικά όσο και στα Ισπανικά, συνδυάστε τις γλώσσες:

```csharp
ocrEngine.Configuration.Language = Language.English | Language.Spanish;
```

Η Aspose OCR θα αλλάξει λεξικά εν κινήσει, βελτιώνοντας την ακρίβεια για έγγραφα μικτής γλώσσας.

### PDF με Κωδικό Πρόσβασης

Όταν εργάζεστε με ασφαλισμένα PDF, παρέχετε τον κωδικό πριν καλέσετε το `Recognize`:

```csharp
ocrEngine.Image = ImageStream.FromFile(inputPath, "MySecretPassword");
```

Αν ο κωδικός είναι λανθασμένος, το `Recognize` ρίχνει `InvalidPasswordException`; το χειρισμό του σφάλματος σας επιτρέπει να ζητήσετε από τον χρήστη τον σωστό κωδικό.

### Έλεγχος Ποιότητας Εικόνας

Υψηλότερο DPI προσφέρει καλύτερα αποτελέσματα OCR αλλά καταναλώνει περισσότερη μνήμη. Ρυθμίστε το DPI αν παρατηρήσετε παραμορφωμένους χαρακτήρες:

```csharp
ocrEngine.Configuration.Dpi = 300; // default is 200
```

### Άδεια vs. Λειτουργία Αξιολόγησης

Σε λειτουργία αξιολόγησης εμφανίζεται υδατογράφημα σε κάθε σελίδα. Για να το αφαιρέσετε, εφαρμόστε την άδειά σας πριν από οποιαδήποτε κλήση OCR:

```csharp
var license = new License();
license.SetLicense(@"C:\Aspose\Aspose.OCR.lic");
```

---

## Pro Tips για Παραγωγική Χρήση

- **Batch processing:** Τυλίξτε τη βασική λογική σε έναν βρόχο `foreach` που διατρέχει μια λίστα PDF. Αποδεσμεύστε το `OcrEngine` μετά από κάθε αρχείο για να ελευθερώσετε τους εγγενείς πόρους.  
- **Logging:** Χρησιμοποιήστε το `ocrEngine.Configuration.Logger` για να καταγράψετε λεπτομερείς στατιστικές OCR (π.χ., αναγνωρισμένοι χαρακτήρες ανά δευτερόλεπτο). Αυτό είναι ανεκτίμητο όταν αντιμετωπίζετε χαμηλή ακρίβεια.  
- **Performance tuning:** Για διακομιστές πολλαπλών πυρήνων, δημιουργήστε ξεχωριστά αντικείμενα `OcrEngine` ανά νήμα· η βιβλιοθήκη είναι thread‑safe όταν κάθε instance είναι απομονωμένο.  
- **Error handling:** Πάντα τυλίξτε τα `Recognize` και `Save` σε `try/catch`. Συνηθισμένες εξαιρέσεις περιλαμβάνουν `FileNotFoundException`, `OutOfMemoryException`, και `UnsupportedFormatException`.

---

## Πλήρες Παράδειγμα Εργασίας (Copy‑Paste Ready)

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace PdfSearchableDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Apply license (optional – removes evaluation watermark)
            // var license = new License();
            // license.SetLicense(@"C:\Aspose\Aspose.OCR.lic");

            // 1️⃣ Create OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Load PDF – this is where we *run OCR on PDF*
            string inputPath = @"C:\Docs\handbook.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Configure output as searchable PDF and set language
            ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
            ocrEngine.Configuration.Language = Language.English;

            // 4️⃣ Run OCR – *recognize text PDF*
            ocrEngine.Recognize();

            // 5️⃣ Save the searchable PDF
            string outputPath = @"C:\Docs\handbook_searchable.pdf";
            ocrEngine.Save(outputPath);

            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**Expected output** (console):

```
Searchable PDF created at: C:\Docs\handbook_searchable.pdf
```

Ανοίξτε το παραγόμενο αρχείο, πατήστε **Ctrl + F**, και θα μπορείτε να εντοπίσετε οποιαδήποτε λέξη εμφανίστηκε στις αρχικές σαρωμένες σελίδες. Αυτή είναι η μαγεία του να μετατρέπετε ένα *OCR scanned PDF* σε **αναζητήσιμο PDF**.

---

## Συμπέρασμα

Δείξαμε πώς να **δημιουργήσετε αναζητήσιμα PDF** αρχεία με Aspose OCR για .NET, καλύπτοντας όλα από την εγκατάσταση του πακέτου μέχρι τη διαχείριση πολυγλωσσικών και κωδικοποιημένων PDF. Ακολουθώντας αυτά τα βήματα μπορείτε αξιόπιστα να *εκτελέσετε OCR σε PDF* έγγραφα, να *αναγνωρίσετε κείμενο PDF* και να μετατρέψετε οποιοδήποτε *OCR scanned PDF* σε πλήρως αναζητήσιμο περιουσιακό στοιχείο.

### Τι Ακολουθεί;

- Εξερευνήστε περαιτέρω το **aspose ocr pdf** API: εξαγωγή απλού κειμένου, εξαγωγή σε DOCX, ή δημιουργία αναζητήσιμων PDF μαζικά.  
- Συνδυάστε την έξοδο αναζητήσιμου PDF με Aspose.PDF για προσθήκη σελιδοδεικτών ή υδατογραφημάτων.  
- Πειραματιστείτε με διαφορετικές ρυθμίσεις DPI ή προσαρμοσμένα λεξικά OCR για εξειδικευμένες γραμματοσειρές.

Μη διστάσετε να τροποποιήσετε το δείγμα, να το ενσωματώσετε στη ροή διαχείρισης εγγράφων σας, ή να θέσετε ερωτήσεις στα σχόλια. Καλή προγραμματιστική δουλειά, και απολαύστε τη μετατροπή των αδιάβαστων σαρώσεων σε χρυσό αναζητήσιμο!

## Σχετικά Tutorials

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Cómo hacer OCR a PDF en .NET con Aspose.OCR](/ocr/spanish/net/text-recognition/recognize-pdf/)
- [كيفية إجراء OCR لملف PDF في .NET باستخدام Aspose.OCR](/ocr/arabic/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}