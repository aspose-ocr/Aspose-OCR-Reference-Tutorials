---
category: general
date: 2025-12-30
description: Μετατρέψτε εικόνα σε PDF χρησιμοποιώντας το Aspose OCR σε C#. Μάθετε
  πώς να προεπεξεργαστείτε την εικόνα για OCR, να αναγνωρίσετε εικόνα με κορεατικό
  κείμενο και να δημιουργήσετε γρήγορα ένα αναζητήσιμο PDF εικόνας.
draft: false
keywords:
- convert image to pdf
- preprocess image for ocr
- recognize korean text image
- create searchable pdf image
language: el
og_description: Μετατρέψτε την εικόνα σε PDF με το Aspose OCR. Αυτό το σεμινάριο δείχνει
  πώς να προετοιμάσετε την εικόνα για OCR, να αναγνωρίσετε εικόνα κειμένου στα κορεατικά
  και να δημιουργήσετε ένα αναζητήσιμο PDF εικόνας.
og_title: Μετατροπή εικόνας σε PDF με C# – Πλήρης οδηγός OCR
tags:
- C#
- OCR
- Aspose
- PDF
title: Μετατροπή εικόνας σε PDF σε C# – Πλήρης οδηγός OCR
url: /el/net/ocr-optimization/convert-image-to-pdf-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή Εικόνας σε PDF σε C# – Πλήρης Οδηγός OCR

Έχετε ποτέ χρειαστεί να **convert image to PDF** αλλά επίσης θέλετε το κείμενο μέσα να είναι αναζητήσιμο; Δεν είστε μόνοι. Πολλοί προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν δουλεύουν με σαρωμένες σελίδες, ειδικά αυτές που είναι γραμμένες στα Κορεατικά. Τα καλά νέα είναι ότι με το Aspose OCR μπορείτε να **preprocess image for OCR**, **recognize Korean text image**, και τελικά **create searchable PDF image** με λίγες μόνο γραμμές.

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία — από τη φόρτωση ενός ακατέργαστου JPEG μιας σελίδας κορεατικού βιβλίου, τον καθαρισμό του, την εξαγωγή του κειμένου, και την συσκευασία του ως PDF με δυνατότητα αναζήτησης. Στο τέλος θα έχετε μια έτοιμη εφαρμογή κονσόλας C# που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET.

## Τι Θα Χρειαστείτε

- **.NET 6.0 ή νεότερο** (ο κώδικας λειτουργεί τόσο σε .NET Core όσο και σε .NET Framework)  
- **Aspose.OCR for .NET** πακέτο NuGet (`Aspose.OCR`) – δωρεάν κλειδιά δοκιμής διατίθενται στην ιστοσελίδα της Aspose.  
- Ένα δείγμα εικόνας που περιέχει κορεατικό κείμενο (π.χ. `korean_book_page.jpg`).  
- Ένα περιβάλλον ανάπτυξης της επιλογής σας (Visual Studio, VS Code, Rider – εγώ χρησιμοποιώ VS 2022).

> **Pro tip:** Κρατήστε τα αρχεία εικόνας σε έναν αφιερωμένο φάκελο όπως `Resources/` ώστε η διαδρομή να παραμένει συνεπής σε όλα τα μηχανήματα.

## Επισκόπηση της Διαδικασίας

1. **Αρχικοποίηση του OCR engine** με υποστήριξη GPU για ταχύτητα.  
2. **Προσθήκη φίλτρων προεπεξεργασίας** (deskew, denoise) για βελτίωση της ακρίβειας αναγνώρισης.  
3. **Λήψη και φόρτωση του μοντέλου γλώσσας Κορεατικά** – το Aspose το κάνει αυτόματα αν χρειαστεί.  
4. **Εκτέλεση της αναγνώρισης** στην είσοδο εικόνας.  
5. **Εξαγωγή του αποτελέσματος ως searchable PDF** χρησιμοποιώντας τον ενσωματωμένο εξαγωγέα.  
6. **Προαιρετικά, σειριοποίηση του αποτελέσματος σε JSON** για περαιτέρω ανάλυση ή καταγραφή.

Παρακάτω θα αναλύσουμε κάθε βήμα, θα εξηγήσουμε *γιατί* είναι σημαντικό, και θα σας δώσουμε τον ακριβή κώδικα που μπορείτε να αντιγράψετε‑επικολλήσετε.

---

## ## Μετατροπή Εικόνας σε PDF – Πλήρης Ροή Εργασίας

Το παρακάτω απόσπασμα είναι το *complete* πρόγραμμα. Μπορείτε να δημιουργήσετε ένα νέο έργο κονσόλας (`dotnet new console -n OcrPdfDemo`) και να αντικαταστήσετε το αυτόματα δημιουργημένο `Program.cs` με αυτόν τον κώδικα.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;
using Aspose.OCR.Export;
using Aspose.OCR.Result;   // for JsonResult

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Initialise the OCR engine (GPU enabled, offline mode off)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                UseGpu = true,          // leverages your graphics card for faster inference
                OfflineMode = false    // allows on‑the‑fly language model download
            };

            // --------------------------------------------------------------
            // Step 2: Add preprocessing filters to improve accuracy
            // --------------------------------------------------------------
            // Deskew corrects slight rotations; MaxAngle = 12° is a safe default.
            ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 12 });

            // Denoise removes isolated speckles that often appear in scanned books.
            ocrEngine.Filters.Add(new DenoiseFilter());

            // --------------------------------------------------------------
            // Step 3: Load the Korean language model
            // --------------------------------------------------------------
            // Aspose will download the model the first time you run this on a new machine.
            ocrEngine.LoadLanguage(LanguageModel.Korean);

            // --------------------------------------------------------------
            // Step 4: Recognise text from the input image
            // --------------------------------------------------------------
            // Replace the path with your actual image location.
            string imagePath = "Resources/korean_book_page.jpg";
            var recognitionResult = ocrEngine.Recognize(imagePath);

            // --------------------------------------------------------------
            // Step 5: Export the recognised page as a searchable PDF
            // --------------------------------------------------------------
            string pdfPath = "Resources/korean_page.pdf";
            var exporter = new SearchablePdfExporter { OutputPath = pdfPath };
            exporter.Export(ocrEngine, imagePath);

            // --------------------------------------------------------------
            // Step 6: Obtain a structured JSON representation of the result
            // --------------------------------------------------------------
            string json = JsonResult.FromRecognitionResult(recognitionResult).ToString(true);
            Console.WriteLine("=== OCR JSON Result ===");
            Console.WriteLine(json);

            Console.WriteLine("\n✅ Conversion complete!");
            Console.WriteLine($"PDF saved to: {pdfPath}");
        }
    }
}
```

### Γιατί Λειτουργεί Αυτό

- **GPU acceleration** μειώνει το χρόνο αναγνώρισης περίπου στο μισό σε σχέση με τη λειτουργία μόνο CPU.  
- **Deskew** και **Denoise** είναι κλασικές τεχνικές *preprocess image for OCR*· διορθώνουν κοινά ελαττώματα σάρωσης που διαφορετικά θα έκαναν το engine να χάσει χαρακτήρες.  
- **Η φόρτωση του μοντέλου γλώσσας** είναι απαραίτητη για **recognize Korean text image** – χωρίς το μοντέλο Κορεατικά το engine θα επανέλθει σε ένα γενικό λατινικό αλφάβητο και θα παράγει άσχημο κείμενο.  
- Ο **SearchablePdfExporter** συνδυάζει το αρχικό bitmap με ένα αόρατο στρώμα κειμένου, δίνοντάς σας ένα αποτέλεσμα **create searchable pdf image** που μπορείτε να ευρετηριάσετε σε οποιονδήποτε PDF viewer.

---

## ## Προεπεξεργασία Εικόνας για OCR – Συμβουλές & Τεχνικές

Αν και τα δύο φίλτρα που προσθέσαμε συνήθως αρκούν, μπορεί να συναντήσετε επίμονες εικόνες. Εδώ είναι μερικά επιπλέον βήματα που μπορείτε να δοκιμάσετε:

| Πρόβλημα | Πρόσθετο Φίλτρο | Πώς να Προσθέσετε |
|----------|----------------|-------------------|
| Χαμηλή αντίθεση | `ContrastFilter { Level = 30 }` | `ocrEngine.Filters.Add(new ContrastFilter { Level = 30 });` |
| Ισχυρός θόρυβος φόντου | `BinarizationFilter { Threshold = 128 }` | `ocrEngine.Filters.Add(new BinarizationFilter { Threshold = 128 });` |
| Μικτή προσανατολισμός (πορτραίτο & τοπίο) | `OrientationFilter()` | `ocrEngine.Filters.Add(new OrientationFilter());` |

> **Σημείωση:** Η προσθήκη πάρα πολλών φίλτρων μπορεί να επιβραδύνει την επεξεργασία. Δοκιμάστε κάθε αλλαγή σε μία σελίδα πριν την εφαρμόσετε σε όλο το σύνολο.

---

## ## Αναγνώριση Κορεατικού Κειμένου σε Εικόνα – Συνηθισμένα Πιθανά Σφάλματα

Τα κορεατικά σενάρια περιέχουν συλλαβές Hangul που είναι οπτικά πυκνές. Αν παρατηρήσετε ακατάλληλο (garbled) αποτέλεσμα:

1. **Βεβαιωθείτε ότι το μοντέλο γλώσσας έχει ληφθεί πλήρως** – ελέγξτε την κονσόλα για μήνυμα όπως “Downloading Korean model…”.  
2. **Αυξήστε το `MaxAngle`** στο `DeskewFilter` αν οι σαρώσεις σας είναι περιστραμμένες πάνω από 12°.  
3. **Αυξήστε τη μνήμη GPU** ορίζοντας `ocrEngine.GpuMemoryLimit = 2048;` (τιμή σε MB).  

Αυτές οι ρυθμίσεις επηρεάζουν άμεσα την επιτυχία του **recognize Korean text image**.

---

## ## Δημιουργία Searchable PDF Image – Επαλήθευση του Αποτελέσματος

Μετά το τέλος του προγράμματος, ανοίξτε το `korean_page.pdf` σε οποιονδήποτε PDF reader (Adobe Acrobat Reader, Foxit, ακόμη και Chrome). Θα πρέπει να μπορείτε να:

- **Επιλέξετε κείμενο** με το ποντίκι όπως σε ένα φυσικό PDF.  
- **Αναζητήσετε** κορεατικές λέξεις χρησιμοποιώντας το ενσωματωμένο πεδίο αναζήτησης.  

Αν το στρώμα κειμένου εμφανίζεται κενό, ελέγξτε ξανά ότι η μέθοδος `Export` έλαβε τη σωστή διαδρομή εικόνας και ότι το OCR αποτέλεσμα περιέχει μη‑κενό `RecognitionResult.Text`.

---

## ## Πλήρης Έξοδος JSON – Τι να Περιμένετε

Η κονσόλα εκτυπώνει ένα ωραία μορφοποιημένο JSON payload. Ένα περικομμένο παράδειγμα φαίνεται παρακάτω:

```json
{
  "Text": "첫 번째 페이지의 내용...",
  "Blocks": [
    {
      "Text": "첫 번째 페이지의 내용...",
      "BoundingBox": { "X": 12, "Y": 34, "Width": 560, "Height": 780 },
      "Confidence": 0.98
    }
  ],
  "Language": "Korean",
  "ProcessingTimeMs": 842
}
```

Μπορείτε να τροφοδοτήσετε αυτό το JSON σε downstream services (π.χ. pipelines ευρετηρίασης, APIs μετάφρασης) χωρίς να χρειάζεται να τρέξετε ξανά το OCR.

---

## ## Troubleshooting & FAQ

**Ε: Το PDF μου είναι τεράστιο σε σύγκριση με την αρχική εικόνα.**  
Α: Ο εξαγωγέας ενσωματώνει το αρχικό bitmap στην εγγενή του ανάλυση. Αν το μέγεθος είναι πρόβλημα, μειώστε την ανάλυση της εικόνας *πριν* την αναγνώριση:

```csharp
ocrEngine.Filters.Add(new ResizeFilter { MaxWidth = 1240, MaxHeight = 1754 });
```

**Ε: Το OCR επιστρέφει κενές συμβολοσειρές.**  
Α: Επαληθεύστε ότι η διαδρομή της εικόνας είναι σωστή και ότι το αρχείο δεν είναι κατεστραμμένο. Επίσης, βεβαιωθείτε ότι ο οδηγός GPU είναι ενημερωμένος· παλαιότεροι οδηγοί μπορούν να προκαλέσουν σιωπηλές αποτυχίες.

**Ε: Μπορώ να επεξεργαστώ πολλές σελίδες σε βρόχο;**  
Α: Φυσικά. Τυλίξτε τα βήματα 4‑6 μέσα σε έναν βρόχο `foreach (var file in Directory.GetFiles("Resources", "*.jpg"))` και αλλάξτε τη διαδρομή εξόδου PDF αναλόγως.

---

## ## Συμπέρασμα

Μόλις **convert image to PDF** διατηρώντας το αναζητήσιμο κείμενο, όλα χάρη στην ισχυρή αλυσίδα του Aspose OCR. Με το **preprocess image for OCR** βελτιώνετε την ακρίβεια· με το **recognize Korean text image** χειρίζεστε σύνθετα σενάρια· και με το **create searchable pdf image** αποκτάτε ένα φορητό, ευρετηριάσιμο έγγραφο.

Πάρτε τον κώδικα, δείξτε τον στα δικά σας scans, και πειραματιστείτε με πρόσθετα φίλτρα ή μοντέλα γλώσσας. Το ίδιο μοτίβο λειτουργεί για Κινέζικα, Ιαπωνικά ή οποιαδήποτε γλώσσα βασισμένη σε λατινικό αλφάβητο — απλώς αντικαταστήστε το `LanguageModel.Korean` με το κατάλληλο enum.

Έχετε περισσότερες ερωτήσεις; Αφήστε ένα σχόλιο, και καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}