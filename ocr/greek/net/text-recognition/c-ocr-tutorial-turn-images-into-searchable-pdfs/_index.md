---
category: general
date: 2026-01-12
description: c# OCR tutorial που δείχνει πώς να αναγνωρίζετε εικόνα κειμένου, να εξάγετε
  κείμενο από εικόνα με c# και να δημιουργήσετε αρχείο OCR εικόνας σε PDF με βαθμολογίες
  εμπιστοσύνης.
draft: false
keywords:
- c# ocr tutorial
- image to pdf ocr
- recognize text image
- ocr confidence scores
- extract text image c#
language: el
og_description: Μάθετε ένα πλήρες tutorial C# OCR για την αναγνώριση εικόνας κειμένου,
  την εξαγωγή κειμένου από εικόνα C# και τη δημιουργία εγγράφου OCR εικόνας σε PDF
  με βαθμολογίες εμπιστοσύνης.
og_title: c# OCR tutorial – Μετατροπή εικόνων σε PDF με δυνατότητα αναζήτησης
tags:
- OCR
- C#
- PDF
title: c# OCR οδηγός – Μετατροπή εικόνων σε αναζητήσιμα PDF
url: /el/net/text-recognition/c-ocr-tutorial-turn-images-into-searchable-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Μετατροπή Εικόνων σε Αναζητήσιμα PDF

Έχετε αναρωτηθεί ποτέ πώς να **αναγνωρίσετε εικόνες κειμένου** σε ένα έργο C# χωρίς να ψάχνετε για υπηρεσίες τρίτων; Δεν είστε μόνοι. Σε πολλές πραγματικές εφαρμογές—σκεφτείτε σαρωτές τιμολογίων, παρακολούθηση αποδείξεων ή αρχεία πολυγλωσσικών εγγράφων—οι προγραμματιστές χρειάζονται μια αξιόπιστη, τοπική μηχανή OCR που επίσης παρέχει βαθμούς εμπιστοσύνης.

Αυτό το **c# ocr tutorial** θα σας καθοδηγήσει σε όλα όσα χρειάζεστε: από τη φόρτωση μιας εικόνας, την επιλογή μοντέλων γλώσσας, την ενεργοποίηση της επιτάχυνσης GPU, έως την αποθήκευση του αποτελέσματος ως αναζητήσιμο PDF. Στο τέλος θα έχετε ένα έτοιμο προς εκτέλεση δείγμα κώδικα που εξάγει κείμενο, αναφέρει την εμπιστοσύνη OCR, και προαιρετικά δημιουργεί ένα αρχείο *image to pdf ocr*—όλα σε λιγότερο από ένα λεπτό κώδικα.

## Τι Θα Κατασκευάσετε

- Φορτώστε μια πολυγλωσσική εικόνα (`sample_multi_lang.jpg` χρησιμοποιείται ως υπόδειγμα).  
- Επιλέξτε τα μοντέλα γλώσσας Αραβικά, Χίντι και Ρωσικά (μπορείτε να προσθέσετε περισσότερα).  
- Ενεργοποιήστε την επεξεργασία GPU εάν το μηχάνημά σας το υποστηρίζει.  
- Λάβετε το ακατέργαστο αποτέλεσμα OCR **με βαθμούς εμπιστοσύνης**.  
- Σειριοποιήστε το αποτέλεσμα σε μορφοποιημένο JSON **ή** γράψτε ένα αναζητήσιμο PDF.  

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας μεταγλωττίζεται σε .NET Core και .NET Framework).  
- Visual Studio 2022 (ή οποιοδήποτε IDE προτιμάτε).  
- Άδεια Aspose.OCR για .NET (η δωρεάν δοκιμή λειτουργεί για δοκιμές).  
- Προαιρετικά: μια GPU συμβατή με CUDA εάν θέλετε να επιταχύνετε την αναγνώριση.

> **Συμβουλή:** Αν δεν έχετε GPU, απλώς ορίστε `UseGpu = false` και η μηχανή θα επιστρέψει στην CPU χωρίς καμία αλλαγή κώδικα.

## Βήμα 1: Εγκατάσταση των Απαιτούμενων Πακέτων NuGet

Ανοίξτε το **Package Manager Console** και εκτελέστε:

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Gpu
Install-Package Newtonsoft.Json
```

## Βήμα 2: Ρύθμιση της Δομής του Έργου

Δημιουργήστε ένα νέο έργο κονσόλας (`dotnet new console -n AsposeOcrDemo`) και αντικαταστήστε το παραγόμενο `Program.cs` με τον κώδικα παρακάτω.  
Όλη η λογική βρίσκεται μέσα στην κλάση `Program`; ο μόνος επιπλέον τύπος είναι μια μικρή μέθοδος επέκτασης που μορφοποιεί το αποτέλεσμα OCR για JSON.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.Models;
using Newtonsoft.Json;

namespace AsposeOcrDemo
{
    class Program
    {
        // Step 1: Input image and language models
        private const string InputImagePath = @"YOUR_DIRECTORY/sample_multi_lang.jpg";
        private static readonly string[] Languages = { LanguageModel.Arabic, LanguageModel.Hindi, LanguageModel.Russian };

        // Step 2: Processing options (GPU toggle & output format)
        private const bool UseGpu = true;               // set false if no GPU
        private const string OutputFormat = "Json";     // change to "Pdf" for PDF output

        static void Main()
        {
            // Step 3: Initialise the appropriate OCR engine
            IOcrEngine engine = UseGpu ? (IOcrEngine)new GpuOcrEngine() : new OcrEngine();

            // Step 4: Run OCR – language models are auto‑downloaded if missing
            OcrResult result = engine.Recognize(
                InputImagePath,
                new OcrOptions { LanguageModels = Languages, AutoDownloadResources = true });

            // Step 5: Emit the result in the chosen format
            if (OutputFormat.Equals("json", StringComparison.OrdinalIgnoreCase))
            {
                string json = JsonConvert.SerializeObject(
                    result.GetWordsWithConfidence(),
                    Formatting.Indented);
                Console.WriteLine(json);
            }
            else if (OutputFormat.Equals("pdf", StringComparison.OrdinalIgnoreCase))
            {
                string pdfPath = Path.ChangeExtension(InputImagePath, ".pdf");
                File.WriteAllBytes(pdfPath, result.Pdf);
                Console.WriteLine($"PDF saved to: {pdfPath}");
            }
        }
    }

    // Helper that flattens OcrResult into a JSON‑friendly structure
    internal static class OcrResultExtensions
    {
        public static object GetWordsWithConfidence(this OcrResult result)
        {
            var words = new System.Collections.Generic.List<object>();
            foreach (var w in result.Words)
                words.Add(new
                {
                    Text = w.Text,
                    Confidence = w.Confidence,
                    BoundingBox = new { w.Bounds.X, w.Bounds.Y, w.Bounds.Width, w.Bounds.Height }
                });

            return new
            {
                RecognizedText = result.Text,
                LanguageModels = result.UsedLanguageModels,
                Words = words,
                ProcessingTimeMs = result.ProcessingTime.TotalMilliseconds
            };
        }
    }
}
```

### Γιατί Λειτουργεί Αυτός ο Κώδικας

1. **GPU toggle** – Το `GpuOcrEngine` αξιοποιεί πυρήνες CUDA· ο τελεστής τριπλού ελέγχου κάνει την εναλλαγή απρόσκοπτη.  
2. **Automatic language download** – Το `AutoDownloadResources = true` εξασφαλίζει ότι τα μοντέλα Αραβικών, Χίντι και Ρωσικών θα ληφθούν την πρώτη φορά που εκτελείτε την εφαρμογή.  
3. **Confidence scores** – Το `result.Words` περιέχει ένα `Confidence` για κάθε αναγνωρισμένη λέξη· η μέθοδος επέκτασης τις μορφοποιεί σε ένα καθαρό αντικείμενο JSON.  
4. **Searchable PDF** – Το `result.Pdf` είναι ήδη ένα πλήρως αναζητήσιμο PDF, οπότε απλώς γράφουμε τον πίνακα byte στο δίσκο. Δεν χρειάζονται επιπλέον βιβλιοθήκες.

## Βήμα 6: Εκτέλεση του Παραδείγματος

Ανοίξτε ένα τερματικό, μεταβείτε στο φάκελο του έργου και εκτελέστε:

```bash
dotnet run
```

Αν επιλέξατε έξοδο **JSON**, θα δείτε κάτι όπως:

```json
{
  "RecognizedText": "مرحبا Hello Привет",
  "LanguageModels": [
    "Arabic",
    "Hindi",
    "Russian"
  ],
  "Words": [
    {
      "Text": "مرحبا",
      "Confidence": 0.98,
      "BoundingBox": { "X": 45, "Y": 12, "Width": 120, "Height": 30 }
    },
    {
      "Text": "Hello",
      "Confidence": 0.99,
      "BoundingBox": { "X": 180, "Y": 12, "Width": 80, "Height": 30 }
    },
    {
      "Text": "Привет",
      "Confidence": 0.97,
      "BoundingBox": { "X": 280, "Y": 12, "Width": 110, "Height": 30 }
    }
  ],
  "ProcessingTimeMs": 312
}
```

Αν μεταβείτε σε **PDF**, η κονσόλα εμφανίζει τη διαδρομή και θα βρείτε ένα αναζητήσιμο PDF ακριβώς δίπλα στην αρχική εικόνα.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

- **Τι γίνεται αν ένα μοντέλο γλώσσας δεν είναι διαθέσιμο;**  
  Η μηχανή OCR ρίχνει ένα σαφές `ResourceNotFoundException`. Επειδή έχουμε ορίσει `AutoDownloadResources = true`, το ελλιπές μοντέλο λήγεται αυτόματα την πρώτη φορά, οπότε η εξαίρεση σπάνια εμφανίζεται σε παραγωγή.

- **Μπορώ να επεξεργαστώ μια δέσμη εικόνων;**  
  Απόλυτα. Τυλίξτε την κλήση `engine.Recognize` μέσα σε έναν βρόχο `foreach` πάνω σε έναν φάκελο αρχείων. Η ίδια `OcrResultExtensions` λειτουργεί για κάθε εικόνα.

- **Χρειάζομαι άδεια για GPU;**  
  Όχι. Η δωρεάν δοκιμή λειτουργεί τόσο για CPU όσο και για GPU. Μια πλήρης άδεια αφαιρεί το υδατογράφημα δοκιμής και αφαιρεί τους περιορισμούς σελίδας.

- **Πόσο ακριβείς είναι οι βαθμοί εμπιστοσύνης;**  
  Οι βαθμοί κυμαίνονται από 0.0 (χωρίς εμπιστοσύνη) έως 1.0 (τέλεια εμπιστοσύνη). Στην πράξη, οτιδήποτε πάνω από 0.90 είναι αξιόπιστο για επεξεργασία downstream· μπορείτε να φιλτράρετε λέξεις με χαμηλότερη εμπιστοσύνη αν χρειάζεστε αυστηρότερη επικύρωση.

## Βήμα 7: Επόμενα Βήματα (Επέκταση του OCR Toolkit σας)

1. **Προσθήκη περισσότερων γλωσσών** – απλώς προσθέστε `LanguageModel.French` (ή οποιοδήποτε υποστηριζόμενο μοντέλο) στον πίνακα `Languages`.  
2. **Συνδυασμός OCR με μετατροπή PDF/A** – Το Aspose.PDF μπορεί να ενσωματώσει το στρώμα OCR σε ένα συμβατό με PDF/A‑2b έγγραφο για αρχειοθέτηση.  
3. **Ενσωμάτωση με Azure Functions** – τυλίξτε τη λογική σε ένα serverless endpoint για επεξεργασία ανεβάσματος σε πραγματικό χρόνο.  
4. **Ρύθμιση των ορίων εμπιστοσύνης** – χρησιμοποιήστε `result.Words.Where(w => w.Confidence < 0.85)` για να επισημάνετε αβέβαιες λέξεις για χειροκίνητη ανασκόπηση.

### TL;DR

Αυτό το **c# ocr tutorial** σας δείχνει πώς να:

- Φορτώσετε μια εικόνα και να επιλέξετε πολλαπλά μοντέλα γλώσσας.  
- Ενεργοποιήσετε την επιτάχυνση GPU με μια μόνο λογική σημαία.  
- Ανακτήσετε αποτελέσματα OCR **με βαθμούς εμπιστοσύνης** και να τα σειριοποιήσετε σε JSON.  
- Προαιρετικά να γράψετε ένα αναζητήσιμο PDF (**image to pdf ocr**).  

Όλα αυτά είναι εφικτά με λίγες γραμμές κώδικα, μια δωρεάν δοκιμή του Aspose.OCR και τον παραπάνω κώδικα. Δοκιμάστε το, προσαρμόστε τη λίστα γλωσσών και θα έχετε μια παραγωγική γραμμή OCR σε λίγα λεπτά.

![c# ocr tutorial example image](https://example.com/placeholder-image.jpg "c# ocr tutorial example image")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}