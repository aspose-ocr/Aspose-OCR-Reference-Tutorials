---
category: general
date: 2026-01-09
description: Αναγνωρίστε κείμενο σε JPG γρήγορα χρησιμοποιώντας το Aspose OCR σε C#.
  Μάθετε πώς να εξάγετε κείμενο από εικόνα, να μετατρέψετε την εικόνα σε JSON και
  EPUB σε ένα ενιαίο σεμινάριο.
draft: false
keywords:
- recognize text in jpg
- extract text from image
- convert image to json
- convert image to epub
- create epub from image
language: el
og_description: Αναγνώριση κειμένου σε jpg με το Aspose OCR. Αυτός ο οδηγός δείχνει
  πώς να εξάγετε κείμενο από εικόνα, να μετατρέψετε την εικόνα σε JSON και EPUB, και
  να δημιουργήσετε ένα ePub από μια εικόνα.
og_title: αναγνώριση κειμένου σε jpg – Πλήρης οδηγός C#
tags:
- Aspose OCR
- C#
- Image Processing
title: Αναγνώριση κειμένου σε jpg με το Aspose OCR – Πλήρης Οδηγός C#
url: /el/net/text-recognition/recognize-text-in-jpg-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# αναγνώριση κειμένου σε jpg – Πλήρης Οδηγός C#

Έχετε χρειαστεί ποτέ να **αναγνωρίσετε κείμενο σε jpg** αρχεία αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη να επιλέξετε; Δεν είστε μόνοι. Πολλοί προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν προσπαθούν για πρώτη φορά να εξάγουν λέξεις από μια φωτογραφία ή σαρωμένο έγγραφο.  

Τα καλά νέα; Με το Aspose OCR μπορείτε να **εξάγετε κείμενο από εικόνα** αρχεία με λίγες γραμμές κώδικα C#, και στη συνέχεια άμεσα **μετατρέψετε την εικόνα σε JSON** ή ακόμη και **μετατρέψετε την εικόνα σε EPUB**—όλα χωρίς να φύγετε από το IDE σας.

Σε αυτόν τον οδηγό θα περάσουμε από όλη τη ροή εργασίας: από την εγκατάσταση των σωστών πακέτων NuGet, μέσω της αναγνώρισης κειμένου σε JPG, μέχρι την αποθήκευση του αποτελέσματος ως δομημένο JSON και ως έγγραφο ePub. Στο τέλος θα μπορείτε να **δημιουργήσετε epub από εικόνα** προγραμματιστικά, ένα χρήσιμο κόλπο για πλατφόρμες e‑learning, ψηφιακές βιβλιοθήκες ή οποιαδήποτε εφαρμογή που χρειάζεται αναζητήσιμα e‑books.

---

## Τι Θα Χρειαστεί

- **.NET 6+** (ή .NET Framework 4.6+). Ο κώδικας λειτουργεί σε οποιοδήποτε πρόσφατο runtime.
- **Aspose.OCR** πακέτο NuGet – η κύρια μηχανή OCR.
- **Aspose.Publishing** πακέτο NuGet – απαιτείται για τη μορφή εξόδου ePub.
- Ένα αρχείο εικόνας με όνομα `input.jpg` τοποθετημένο κάπου στον δίσκο σας (αντικαταστήστε τη διαδρομή με τη δική σας).
- Ένα κειμενογράφο ή IDE (Visual Studio, VS Code, Rider—όπως προτιμάτε).

Αυτό είναι όλο. Χωρίς επιπλέον υπηρεσίες, χωρίς εξωτερικά APIs, μόνο μερικές βιβλιοθήκες και ένα αρχείο JPG.

## Βήμα 1: Ρυθμίστε το Έργο σας για **αναγνώριση κειμένου σε jpg**

Πρώτα, δημιουργήστε μια νέα εφαρμογή κονσόλας (ή προσθέστε σε υπάρχον έργο). Στη συνέχεια προσθέστε τα δύο πακέτα Aspose μέσω του NuGet Package Manager:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.Publishing
```

> **Συμβουλή:** Αν χρησιμοποιείτε Visual Studio, κάντε δεξί‑κλικ στο έργο → *Manage NuGet Packages* → αναζητήστε *Aspose.OCR* και *Aspose.Publishing*, στη συνέχεια κάντε κλικ στο **Install**.

Αυτά τα πακέτα φέρνουν όλα όσα χρειάζεστε για να **εξάγετε κείμενο από εικόνα** και για να δημιουργήσετε αργότερα ένα αρχείο ePub.

## Βήμα 2: **Εξαγωγή κειμένου από εικόνα** Χρησιμοποιώντας Aspose OCR

Τώρα θα γράψουμε τον κώδικα που διαβάζει το JPG και εξάγει τους χαρακτήρες από αυτό.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ImageToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // 2️⃣ Recognize text from the JPG file
            // Replace the path with the location of your own image
            string inputPath = @"YOUR_DIRECTORY\input.jpg";
            var ocrResult = ocrEngine.RecognizeImage(inputPath);

            // 3️⃣ Show the recognized text in the console
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**Γιατί λειτουργεί:** Το `OcrEngine` αφαιρεί όλες τις χαμηλού επιπέδου προεπεξεργασίες εικόνας, την ανίχνευση γλώσσας και τη διαχωρισμό χαρακτήρων. Απλώς το δείχνετε σε ένα αρχείο και επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει τη συμβολοσειρά απλού κειμένου (`ocrResult.Text`) και ένα πλούσιο σύνολο μεταδεδομένων.

## Βήμα 3: **Μετατροπή εικόνας σε JSON** – Εξαγωγή του Αποτελέσματος OCR

Αν χρειάζεται να αποθηκεύσετε το αποτέλεσμα OCR σε δομημένη μορφή (για APIs, βάσεις δεδομένων ή επεξεργασία downstream), το Aspose το κάνει εύκολο να σειριοποιήσετε το αποτέλεσμα σε JSON.

```csharp
// 4️⃣ Convert the OCR result to JSON
string jsonContent = ocrResult.ToJson();

// 5️⃣ Save the JSON to disk
string jsonPath = @"YOUR_DIRECTORY\output.json";
File.WriteAllText(jsonPath, jsonContent);

Console.WriteLine($"JSON saved to: {jsonPath}");
```

Το παραγόμενο JSON φαίνεται περίπου έτσι (περιορισμένο για συντομία):

```json
{
  "Text": "Hello world!",
  "Confidence": 0.98,
  "PageCount": 1,
  "Words": [
    { "Value": "Hello", "Confidence": 0.99 },
    { "Value": "world!", "Confidence": 0.97 }
  ]
}
```

**Πότε να το χρησιμοποιήσετε:** Το JSON είναι τέλειο αν τροφοδοτείτε τα δεδομένα OCR σε μια υπηρεσία web, τα αποθηκεύετε σε αποθήκη NoSQL, ή απλώς χρειάζεστε μια φορητή αναπαράσταση που μπορεί να αναλυθεί από οποιαδήποτε γλώσσα.

## Βήμα 4: **Μετατροπή εικόνας σε EPUB** – Αποθήκευση ως eBook

Το Aspose Publishing προσθέτει υποστήριξη για διάφορες μορφές e‑book, συμπεριλαμβανομένου του EPUB. Καλώντας το `Save` στο `OcrResult` μπορείτε να δημιουργήσετε ένα πλήρως συμβατό αρχείο ePub που περιέχει το αναγνωρισμένο κείμενο και, προαιρετικά, την αρχική εικόνα.

```csharp
// 6️⃣ Save the OCR result as an ePub document
string epubPath = @"YOUR_DIRECTORY\output.epub";
ocrResult.Save(epubPath, OcrOutputFormat.Epub);

Console.WriteLine($"EPUB created at: {epubPath}");
```

**Τι λαμβάνετε:** Ένα ePub που μπορείτε να ανοίξετε σε οποιονδήποτε αναγνώστη (Calibre, Apple Books, Adobe Digital Editions). Το αρχείο περιλαμβάνει το εξαγόμενο κείμενο ως αναζητήσιμο περιεχόμενο, καθώς και την πηγή εικόνας ως στρώση φόντου—ιδανικό για τη δημιουργία **δημιουργίας epub από εικόνα** pipelines.

## Βήμα 5: Πλήρες Παράδειγμα Εργασίας – Από JPG σε JSON & EPUB

Συνδυάζοντας όλα, εδώ είναι το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα. Αντιγράψτε‑και‑επικολλήστε το στο `Program.cs`, προσαρμόστε τις διαδρομές αρχείων και πατήστε **F5**.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ImageToEpubDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize OCR engine
            var ocrEngine = new OcrEngine();

            // Path to the input JPG
            string inputPath = @"YOUR_DIRECTORY\input.jpg";

            // Recognize text
            var ocrResult = ocrEngine.RecognizeImage(inputPath);

            // Output recognized text to console
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine();

            // Export to JSON
            string jsonPath = @"YOUR_DIRECTORY\output.json";
            File.WriteAllText(jsonPath, ocrResult.ToJson());
            Console.WriteLine($"JSON saved to: {jsonPath}");

            // Export to EPUB
            string epubPath = @"YOUR_DIRECTORY\output.epub";
            ocrResult.Save(epubPath, OcrOutputFormat.Epub);
            Console.WriteLine($"EPUB created at: {epubPath}");
        }
    }
}
```

Εκτελέστε το πρόγραμμα και θα πρέπει να δείτε τρία πράγματα:

1. Το αναγνωρισμένο κείμενο εκτυπωμένο στην κονσόλα.
2. Ένα αρχείο `output.json` που περιέχει τα δομημένα δεδομένα OCR.
3. Ένα αρχείο `output.epub` που μπορείτε να ανοίξετε με οποιονδήποτε αναγνώστη e‑book.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

- **Τι γίνεται αν η εικόνα είναι PNG ή BMP;**  
  Το Aspose OCR υποστηρίζει τις περισσότερες μορφές raster (PNG, BMP, TIFF, GIF). Απλώς αλλάξτε την επέκταση αρχείου στο `inputPath`; ο ίδιος κώδικας λειτουργεί.

- **Μπορώ να ορίσω γλώσσα διαφορετική από τα Αγγλικά;**  
  Ναι. Ορίστε `ocrEngine.Language = OcrLanguage.French;` (ή οποιαδήποτε υποστηριζόμενη γλώσσα) πριν καλέσετε το `RecognizeImage`.

- **Τι γίνεται με PDF πολλαπλών σελίδων;**  
  Για PDF, πρώτα θα μετατρέψετε κάθε σελίδα σε εικόνα (το Aspose.PDF μπορεί να το κάνει) και στη συνέχεια θα δώσετε κάθε εικόνα στο `RecognizeImage`. Τα προκύπτοντα αντικείμενα `OcrResult` μπορούν να συγχωνευτούν πριν την εξαγωγή σε JSON ή EPUB.

- **Λαμβάνω χαμηλές βαθμολογίες εμπιστοσύνης. Πώς μπορώ να βελτιώσω την ακρίβεια;**  
  Προεπεξεργαστείτε την εικόνα: αυξήστε την αντίθεση, διορθώστε την κλίση ή μετατρέψτε την σε γκρι κλίμακα. Το Aspose OCR προσφέρει επίσης `PreprocessOptions` που μπορείτε να ρυθμίσετε.

## Συμπέρασμα

Τώρα έχετε μια σταθερή, ολοκληρωμένη συνταγή για **αναγνώριση κειμένου σε jpg** αρχεία χρησιμοποιώντας Aspose OCR, στη συνέχεια **μετατροπή εικόνας σε JSON** για pipelines δεδομένων και **μετατροπή εικόνας σε EPUB** για τη δημιουργία αναζητήσιμων e‑books. Η προσέγγιση είναι ελαφριά, απαιτεί μόνο δύο πακέτα NuGet και λειτουργεί σε όλα τα σύγχρονα runtime .NET.

Από εδώ μπορείτε:

- Να ενσωματώσετε το JSON αποτέλεσμα σε ευρετήριο αναζήτησης (Azure Cognitive Search, Elastic).
- Να επεξεργαστείτε κατά παρτίδες έναν φάκελο εικόνων και να δημιουργήσετε μια βιβλιοθήκη βιβλίων ePub.
- Να επεκτείνετε τη ροή εργασίας με APIs μετάφρασης για αυτόματη δημιουργία πολύγλωσσων e‑books.

Δοκιμάστε το, πειραματιστείτε με διαφορετικές ποιότητες εικόνας και αφήστε τη μηχανή OCR να κάνει το δύσκολο έργο. Καλό κώδικα!

![αναγνώριση κειμένου σε jpg εξαγωγή στιγμιότυπο](placeholder-image.png "παράδειγμα αναγνώρισης κειμένου σε jpg")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}