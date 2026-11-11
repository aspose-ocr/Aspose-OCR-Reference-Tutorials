---
category: general
date: 2026-09-13
description: Μάθετε πώς να μετατρέψετε μια σαρωμένη σελίδα σε PDF με C# χρησιμοποιώντας
  το Aspose OCR. Αυτός ο οδηγός δείχνει προεπεξεργασία, αναγνώριση κειμένου στα Κορεατικά
  και δημιουργία PDF με δυνατότητα αναζήτησης.
keywords:
- scanned page to pdf
- preprocess image for OCR
- generate pdf with text
- convert image to searchable pdf
- gpu accelerated OCR
- recognize Korean text image
lastmod: 2026-09-13
og_description: Μάθετε πώς να μετατρέψετε μια σαρωμένη σελίδα σε PDF με C# και Aspose
  OCR. Το σεμινάριο καλύπτει προεπεξεργασία εικόνας, GPU‑accelerated OCR για Κορεατικό
  κείμενο και δημιουργία PDF με δυνατότητα αναζήτησης σε λίγα λεπτά.
og_image_alt: Screenshot of C# console app converting a scanned Korean page to searchable
  PDF using Aspose OCR
og_title: Πώς να μετατρέψετε μια σαρωμένη σελίδα σε PDF με C# και OCR
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  headline: How to turn a scanned page to PDF in C# with OCR
  type: TechArticle
- description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  name: How to turn a scanned page to PDF in C# with OCR
  steps:
  - name: Initialise the OCR engine with GPU support.
    text: Initialise the OCR engine with GPU support.
  - name: Add **preprocess image for OCR** filters such as deskew and denoise.
    text: Add **preprocess image for OCR** filters such as deskew and denoise.
  - name: Download and load the Korean language model (handled automatically).
    text: Download and load the Korean language model (handled automatically).
  - name: Run the OCR on the image.
    text: Run the OCR on the image.
  - name: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
    text: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
  - name: (Optional) Serialize the OCR output to JSON for downstream pipelines.
    text: (Optional) Serialize the OCR output to JSON for downstream pipelines.
  - name: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
    text: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
  - name: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
    text: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
  - name: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
    text: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
  type: HowTo
- questions:
  - answer: 'The exporter embeds the original bitmap at its native resolution. If
      size is a concern, downscale the image *before* recognition:'
    question: My PDF is huge compared to the original image.
  - answer: Verify that the image path is correct and that the file is not corrupted.
      Also, make sure the GPU driver is up‑to‑date; older drivers can cause silent
      failures.
    question: The OCR returns empty strings.
  - answer: Absolutely. Wrap steps 4‑6 in a `foreach (var file in Directory.GetFiles("Resources",
      "*.jpg"))` loop and change the output PDF path accordingly.
    question: Can I process multiple pages in a loop?
  type: FAQPage
tags:
- scanned page to pdf
- OCR
- Aspose
- C#
title: Πώς να μετατρέψετε μια σαρωμένη σελίδα σε PDF με C# και OCR
url: /el/net/ocr-optimization/convert-image-to-pdf-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να μετατρέψετε μια σαρωμένη σελίδα σε PDF με C# και OCR

Αν χρειάζεστε **μετατροπή μιας σαρωμένης σελίδας σε PDF** διατηρώντας το κείμενο αναζητήσιμο, βρίσκεστε στο σωστό μέρος. Αυτό το tutorial σας καθοδηγεί στη χρήση του Aspose OCR για **προεπεξεργασία εικόνας για OCR**, **αναγνώριση εικόνας κειμένου Κορεάτικης**, και τελικά **δημιουργία αναζητήσιμης εικόνας PDF** – όλα από μια απλή εφαρμογή κονσόλας C#.

## Γρήγορες απαντήσεις
- **What library handles OCR?** Aspose.OCR for .NET  
- **Can I use the GPU?** Yes – enable GPU acceleration for up to 2× faster processing  
- **Do I need a Korean language pack?** It downloads automatically on first use  
- **Will the output be searchable?** The generated PDF contains an invisible text layer  
- **What .NET versions are supported?** .NET 6.0 and later (including .NET Core and .NET Framework)

## Απαιτήσεις

- **.NET 6.0 ή νεότερη** – λειτουργεί σε .NET Core, .NET Framework, και .NET 5/6+  
- **Aspose.OCR for .NET** πακέτο NuGet (`Aspose.OCR`) – τα κλειδιά δοκιμής είναι δωρεάν στον ιστότοπο της Aspose  
- Μια δείγμα εικόνας με κορεατικούς χαρακτήρες, π.χ. `korean_book_page.jpg`  
- Το αγαπημένο σας IDE (Visual Studio 2022, VS Code, Rider, κ.λπ.)

> **Συμβουλή επαγγελματία:** Αποθηκεύστε τις εικόνες σε φάκελο `Resources/` ώστε οι διαδρομές να παραμένουν συνεπείς μεταξύ των μηχανών.

## Επισκόπηση της διαδικασίας

1. Αρχικοποιήστε τη μηχανή OCR με υποστήριξη GPU.  
2. Προσθέστε φίλτρα **προεπεξεργασία εικόνας για OCR** όπως deskew και denoise.  
3. Κατεβάστε και φορτώστε το μοντέλο γλώσσας Κορεάτικης (χειρίζεται αυτόματα).  
4. Εκτελέστε το OCR στην εικόνα.  
5. Εξάγετε το αποτέλεσμα με **SearchablePdfExporter** για **δημιουργία αναζητήσιμης εικόνας PDF**.  
6. (Προαιρετικά) Σειριοποιήστε την έξοδο OCR σε JSON για επόμενες διαδικασίες.

Παρακάτω επεκτείνουμε κάθε βήμα, εξηγούμε *γιατί* είναι σημαντικό, και σας δίνουμε τον ακριβή κώδικα που μπορείτε να αντιγράψετε‑επικολλήσετε.

## Πώς λειτουργεί η μετατροπή σαρωμένης σελίδας σε PDF;

`OcrEngine` είναι η κύρια κλάση στο Aspose.OCR που εκτελεί οπτική αναγνώριση χαρακτήρων σε εικόνες.  
`SearchablePdfExporter` δημιουργεί ένα PDF που περιέχει την αρχική εικόνα και ένα αόρατο στρώμα κειμένου για αναζήτηση.  
`RecognitionResult` κρατά το κείμενο και τα δεδομένα εμπιστοσύνης που επιστρέφει η μηχανή OCR.

Φορτώστε την εικόνα με `new OcrEngine()` και καλέστε `engine.Recognize("korean_book_page.jpg")`, στη συνέχεια περάστε το `RecognitionResult` στο `SearchablePdfExporter.Export`. Αυτή η ροή δύο βημάτων διαβάζει το bitmap, εξάγει κείμενο Unicode, και ενσωματώνει και τα δύο σε ένα μόνο PDF όπου το στρώμα κειμένου είναι αόρατο αλλά αναζητήσιμο. Η επιτάχυνση GPU μειώνει τον χρόνο αναγνώρισης περίπου στο μισό, ενώ τα φίλτρα deskew και denoise αυξάνουν την ακρίβεια έως και 15 % σε θορυβώδεις σαρώσεις.

## Μετατροπή εικόνας σε PDF – πλήρης ροή εργασίας

Το παρακάτω απόσπασμα είναι το *πλήρες* πρόγραμμα. Δημιουργήστε ένα νέο έργο κονσόλας (`dotnet new console -n OcrPdfDemo`) και αντικαταστήστε το αυτόματα δημιουργημένο `Program.cs` με τον κώδικα που φαίνεται στην θέση κράτησης.

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

### Γιατί λειτουργεί αυτό

- **GPU acceleration** μειώνει τον χρόνο αναγνώρισης περίπου στο μισό σε σύγκριση με τη λειτουργία μόνο CPU.  
- **Deskew** και **Denoise** είναι κλασικές τεχνικές *προεπεξεργασία εικόνας για OCR*· διορθώνουν κοινά ελαττώματα σάρωσης που διαφορετικά κάνουν τη μηχανή να χάσει χαρακτήρες.  
- **Language model loading** είναι απαραίτητο για **recognize Korean text image** – χωρίς το μοντέλο Κορεάτικης η μηχανή θα επανέλθει σε ένα γενικό λατινικό αλφάβητο και θα παράγει άχρηστο κείμενο.  
- Το **SearchablePdfExporter** συνδυάζει το αρχικό bitmap και μια αόρατη επικάλυψη κειμένου, δίνοντάς σας ένα αποτέλεσμα **create searchable pdf image** που μπορείτε να ευρετηριάσετε σε οποιονδήποτε προβολέα PDF.

## Γιατί λειτουργεί αυτό

- **GPU acceleration** μειώνει τον χρόνο αναγνώρισης περίπου στο μισό σε σύγκριση με τη λειτουργία μόνο CPU.  
- **Deskew** και **Denoise** είναι κλασικές τεχνικές *προεπεξεργασία εικόνας για OCR*· διορθώνουν κοινά ελαττώματα σάρωσης που διαφορετικά κάνουν τη μηχανή να χάσει χαρακτήρες.  
- **Language model loading** είναι απαραίτητο για **recognize Korean text image** – χωρίς το μοντέλο Κορεάτικης η μηχανή θα επανέλθει σε ένα γενικό λατινικό αλφάβητο και θα παράγει άχρηστο κείμενο.  
- Το **SearchablePdfExporter** συνδυάζει το αρχικό bitmap και μια αόρατη επικάλυψη κειμένου, δίνοντάς σας ένα αποτέλεσμα **create searchable pdf image** που μπορείτε να ευρετηριάσετε σε οποιονδήποτε προβολέα PDF.

## Προεπεξεργασία εικόνας για OCR – συμβουλές & κόλπα

`DeskewFilter` διορθώνει την περιστροφή των σαρωμένων σελίδων.  
`ContrastFilter` ρυθμίζει την αντίθεση της εικόνας για βελτίωση της ακρίβειας OCR.  
`BinarizationFilter` μετατρέπει την εικόνα σε ασπρόμαυρη βάση ενός κατωφλίου, μειώνοντας τον θόρυβο του φόντου.  
`OrientationFilter` εντοπίζει και διορθώνει μικτές σελίδες πορτραίτου/τοπίου.  

| Πρόβλημα | Πρόσθετο φίλτρο | Πώς να προσθέσετε |
|----------|----------------|-------------------|
| Χαμηλή αντίθεση | `ContrastFilter { Level = 30 }` | `ocrEngine.Filters.Add(new ContrastFilter { Level = 30 });` |
| Έντονος θόρυβος φόντου | `BinarizationFilter { Threshold = 128 }` | `ocrEngine.Filters.Add(new BinarizationFilter { Threshold = 128 });` |
| Μικτή προσανατολισμός (πορτραίτο & τοπίο) | `OrientationFilter()` | `ocrEngine.Filters.Add(new OrientationFilter());` |

> **Σημείωση:** Η προσθήκη πάρα πολλών φίλτρων μπορεί να επιβραδύνει την επεξεργασία. Δοκιμάστε κάθε αλλαγή σε μία σελίδα πριν την κλιμακώσετε.

## Αναγνώριση εικόνας κειμένου Κορεάτικης – κοινά προβλήματα

Τα κορεατικά σενάρια περιέχουν συλλαβές Hangul που είναι οπτικά πυκνές. Αν παρατηρήσετε ακατάλληλο αποτέλεσμα:

1. **Βεβαιωθείτε ότι το μοντέλο γλώσσας έχει κατεβεί πλήρως** – ελέγξτε την κονσόλα για μήνυμα όπως “Downloading Korean model…”.  
2. **Αυξήστε το `MaxAngle`** στο `DeskewFilter` αν οι σαρώσεις σας είναι περιστραμμένες πέρα από 12°.  
3. **Αυξήστε τη μνήμη GPU** ορίζοντας `ocrEngine.GpuMemoryLimit = 2048;` (τιμή σε MB).  

`LanguageModel.Korean` φορτώνει τα δεδομένα γλώσσας Κορεάτικης για OCR, επιτρέποντας ακριβή αναγνώριση Hangul.  

Αυτές οι προσαρμογές επηρεάζουν άμεσα την επιτυχία του **recognize Korean text image**.

## Δημιουργία αναζητήσιμης εικόνας PDF – επαλήθευση του αποτελέσματος

Μετά το τέλος του προγράμματος, ανοίξτε το `korean_page.pdf` σε οποιονδήποτε αναγνώστη PDF (Adobe Acrobat Reader, Foxit, ακόμη και Chrome). Θα πρέπει να μπορείτε:

- **Να επιλέξετε κείμενο** με το ποντίκι όπως σε ένα φυσικό PDF.  
- **Να κάνετε αναζήτηση** για κορεατικές λέξεις χρησιμοποιώντας το ενσωματωμένο πλαίσιο αναζήτησης.  

Αν το στρώμα κειμένου εμφανίζεται κενό, ελέγξτε ξανά ότι η μέθοδος `Export` έλαβε τη σωστή διαδρομή εικόνας και ότι το αποτέλεσμα OCR περιέχει μη‑κενό `RecognitionResult.Text`.

## Πλήρης έξοδος JSON – τι να περιμένετε

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

Μπορείτε να τροφοδοτήσετε αυτό το JSON σε downstream υπηρεσίες (π.χ. pipelines ευρετηρίασης, APIs μετάφρασης) χωρίς να χρειάζεται να τρέξετε ξανά το OCR.

## Αντιμετώπιση προβλημάτων & Συχνές ερωτήσεις

**Ε: Το PDF μου είναι τεράστιο σε σύγκριση με την αρχική εικόνα.**  
Α: Ο εξαγωγέας ενσωματώνει το αρχικό bitmap στην εγγενή του ανάλυση. Αν το μέγεθος αποτελεί πρόβλημα, μειώστε την εικόνα *πριν* την αναγνώριση:

```csharp
ocrEngine.Filters.Add(new ResizeFilter { MaxWidth = 1240, MaxHeight = 1754 });
```

**Ε: Το OCR επιστρέφει κενές συμβολοσειρές.**  
Α: Επαληθεύστε ότι η διαδρομή της εικόνας είναι σωστή και ότι το αρχείο δεν είναι κατεστραμμένο. Επίσης, βεβαιωθείτε ότι ο οδηγός GPU είναι ενημερωμένος· παλαιότεροι οδηγοί μπορούν να προκαλέσουν σιωπηλές αποτυχίες.

**Ε: Μπορώ να επεξεργαστώ πολλές σελίδες σε βρόχο;**  
Α: Φυσικά. Τυλίξτε τα βήματα 4‑6 σε έναν βρόχο `foreach (var file in Directory.GetFiles("Resources", "*.jpg"))` και αλλάξτε τη διαδρομή εξόδου PDF ανάλογα.

## Συμπέρασμα

Μόλις **μετατρέψαμε εικόνα σε PDF** διατηρώντας το αναζητήσιμο κείμενο, όλα χάρη στην ισχυρή αλυσίδα του Aspose OCR. Με την **προεπεξεργασία εικόνας για OCR**, αυξάνετε την ακρίβεια· με την **αναγνώριση εικόνας κειμένου Κορεάτικης**, χειρίζεστε σύνθετα σενάρια· και με τη **δημιουργία αναζητήσιμης εικόνας PDF**, αποκτάτε ένα φορητό, ευρετηριάσιμο έγγραφο.

Πάρτε τον κώδικα, δείξτε τον στις δικές σας σαρώσεις, και πειραματιστείτε με πρόσθετα φίλτρα ή μοντέλα γλώσσας. Το ίδιο μοτίβο λειτουργεί για Κινέζικα, Ιαπωνικά ή οποιαδήποτε γλώσσα βασισμένη σε λατινικό αλφάβητο—απλώς αντικαταστήστε το `LanguageModel.Korean` με το αντίστοιχο enum.

Έχετε περισσότερες ερωτήσεις; Αφήστε ένα σχόλιο, και καλή προγραμματιστική!

---

**Τελευταία ενημέρωση:** 2026-09-13  
**Δοκιμή με:** Aspose.OCR 24.11 for .NET  
**Συγγραφέας:** Aspose

## Σχετικά Μαθήματα

- [Δημιουργία Αναζητήσιμου PDF από Σαρωμένα Αρχεία Χρησιμοποιώντας Aspose Ocr](/ocr/net/ocr-optimization/create-searchable-pdf-from-scanned-files-using-aspose-ocr/)
- [Pipeline Προεπεξεργασίας OCR – Πώς να Αναγνωρίσετε Κείμενο από Εικόνα](/ocr/net/ocr-optimization/ocr-preprocessing-pipeline-how-to-recognize-text-from-image/)
- [Αναγνώριση Κειμένου από Εικόνα με Aspose Ocr – Πλήρης Οδηγός C](/ocr/net/ocr-configuration/recognize-text-from-image-with-aspose-ocr-complete-c-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}