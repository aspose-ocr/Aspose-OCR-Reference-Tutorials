---
category: general
date: 2026-03-21
description: Πώς να κάνετε παρτίδα OCR σε C# με απλότητα—μάθετε να εξάγετε κείμενο
  από εικόνες, να μετατρέπετε εικόνες σε κείμενο και να αποθηκεύετε το OCR ως κείμενο
  με ρυθμίσεις γλώσσας.
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert images to text
- save OCR as text
- set OCR language
language: el
og_description: Πώς να εκτελείτε OCR σε παρτίδες σε C# σας επιτρέπει να εξάγετε κείμενο
  από εικόνες, να μετατρέπετε εικόνες σε κείμενο και να αποθηκεύετε το OCR ως κείμενο,
  ενώ ρυθμίζετε εύκολα τη γλώσσα του OCR.
og_title: Πώς να κάνετε μαζική OCR σε C# – Σύντομος οδηγός
tags:
- OCR
- C#
- Aspose
title: Πώς να κάνετε μαζική OCR σε C# – Εξαγωγή κειμένου από εικόνες γρήγορα
url: /el/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-images-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να κάνετε Batch OCR σε C# – Εξαγωγή Κειμένου από Εικόνες Γρήγορα

Έχετε αναρωτηθεί ποτέ **πώς να κάνετε batch OCR** όταν έχετε εκατοντάδες εικόνες σε έναν φάκελο; Δεν είστε μόνοι—οι προγραμματιστές ρωτούν συνεχώς πώς να εξάγουν κείμενο από εικόνες χωρίς να γράφουν βρόχο για κάθε αρχείο. Τα καλά νέα είναι ότι το Aspose.OCR σας παρέχει έναν καθαρό, έτοιμο για παράλληλη εκτέλεση τρόπο να **μετατρέψετε εικόνες σε κείμενο** με λίγες μόνο γραμμές C#.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που δείχνει πώς να **αποθηκεύσετε OCR ως κείμενο**, να επιλέξετε τη σωστή γλώσσα και να ενισχύσετε την παράλληλη επεξεργασία για ταχύτητα. Στο τέλος θα έχετε μια αυτόνομη λύση που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET.

## Τι Θα Χρειαστείτε

- .NET 6 ή νεότερο (το API λειτουργεί με .NET Core και .NET Framework)
- Aspose.OCR για .NET (πακέτο NuGet `Aspose.OCR`)
- Έναν φάκελο με τις εικόνες που θέλετε να επεξεργαστείτε (PNG, JPEG, TIFF, κ.λπ.)
- Λίγη περιέργεια για παράλληλο προγραμματισμό (προαιρετικό, αλλά χρήσιμο)

Δεν χρειάζονται επιπλέον υπηρεσίες, κλειδιά cloud—απλώς καθαρός κώδικας C# που εκτελείται τοπικά.

---

![διαδικασία batch OCR](placeholder.png){alt="διάγραμμα διαδικασίας batch OCR"}

## Βήμα 1: Ρυθμίστε το Έργο και Εγκαταστήστε το Aspose.OCR

Πρώτα απ' όλα, δημιουργήστε μια εφαρμογή console (ή χρησιμοποιήστε μια υπάρχουσα) και προσθέστε το πακέτο Aspose.OCR:

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** Αν χρησιμοποιείτε Visual Studio, κάντε δεξί‑κλικ στο έργο → *Manage NuGet Packages* → αναζητήστε το *Aspose.OCR* και εγκαταστήστε την πιο πρόσφατη σταθερή έκδοση.

Αυτό σας δίνει πρόσβαση στα `OcrBatchProcessor`, `OcrEngineSettings` και το enum `Language`.

## Βήμα 2: Ορίστε Φακέλους Εισόδου και Εξόδου

Ο επεξεργαστής batch πρέπει να ξέρει πού βρίσκονται οι πηγαίες εικόνες και πού πρέπει να γραφτούν τα εξαγόμενα αρχεία κειμένου. Κρατήστε τις διαδρομές απόλυτες ή σχετικές με τη ρίζα του έργου—απλώς βεβαιωθείτε ότι οι φάκελοι υπάρχουν πριν τρέξετε τον κώδικα.

```csharp
var inputPath  = @"C:\MyImages\BatchInput";
var outputPath = @"C:\MyImages\BatchResults";

// Ensure the output directory exists
if (!Directory.Exists(outputPath))
    Directory.CreateDirectory(outputPath);
```

> **Why this matters:** Αν λείπει ο φάκελος εξόδου, ο επεξεργαστής θα πετάξει εξαίρεση, διακόπτοντας όλο το batch. Η προημιουργία του εξασφαλίζει ομαλή εκτέλεση.

## Βήμα 3: Διαμορφώστε τις Ρυθμίσεις OCR (συμπεριλαμβανομένης της γλώσσας)

Εδώ είναι που **ορίζετε τη γλώσσα OCR** για ολόκληρο το batch. Το Aspose.OCR υποστηρίζει δεκάδες γλώσσες· η προεπιλογή είναι τα Αγγλικά, αλλά μπορείτε να αλλάξετε σε Γαλλικά, Ισπανικά κ.λπ., αλλάζοντας την τιμή του enum `Language`.

```csharp
var ocrSettings = new OcrEngineSettings
{
    Language = Language.English   // Change to Language.French, Language.Spanish, etc.
};
```

Αν χρειαστεί ποτέ να επεξεργαστείτε διαφορετικές γλώσσες ανά εικόνα, μπορείτε αργότερα να παρακάμψετε αυτή τη ρύθμιση ανά αρχείο—περισσότερα αργότερα.

## Βήμα 4: Δημιουργήστε το Αντικείμενο `OcrBatchProcessor`

Τώρα συνδέουμε όλα μαζί. Ο `OcrBatchProcessor` σας επιτρέπει να καθορίσετε το φάκελο εισόδου, φάκελο εξόδου, μορφή εξόδου, επιλογές παράλληλης εκτέλεσης και τις κοινές ρυθμίσεις που μόλις δημιουργήσαμε.

```csharp
using Aspose.OCR.Batch;
using Aspose.OCR.Settings;
using System.Threading.Tasks;

var batch = new OcrBatchProcessor
{
    InputFolder   = inputPath,
    OutputFolder  = outputPath,
    OutputFormat  = OcrOutputFormat.PlainText, // **save OCR as text** in .txt files
    ParallelOptions = new ParallelOptions { MaxDegreeOfParallelism = 4 }, // up to 4 threads
    Settings = ocrSettings
};
```

> **Why parallelism?** Όταν έχετε δεκάδες ή εκατοντάδες εικόνες, η επεξεργασία τους μία‑με‑μία μπορεί να είναι εξαιρετικά αργή. Ορίζοντας το `MaxDegreeOfParallelism` σε 4, το runtime χρησιμοποιεί τέσσερις πυρήνες CPU ταυτόχρονα, μειώνοντας δραστικά το συνολικό χρόνο σε ένα τυπικό workstation.

## Βήμα 5: Εκτελέστε τη Λειτουργία Batch

Με τον επεξεργαστή διαμορφωμένο, η εκτέλεση είναι μια μόνο κλήση μεθόδου. Η βιβλιοθήκη διαχειρίζεται την απαρίθμηση αρχείων, το OCR και τη γραφή των αποτελεσμάτων αυτόματα.

```csharp
batch.Execute();
Console.WriteLine("Batch OCR completed.");
```

Όταν η κονσόλα εκτυπώσει *“Batch OCR completed.”* θα βρείτε ένα αρχείο `.txt` δίπλα σε κάθε αρχική εικόνα μέσα στο `BatchResults`. Κάθε αρχείο κειμένου περιέχει τους ακατέργαστους χαρακτήρες που εξήχθησαν από την πηγή του—ακριβώς ό,τι χρειάζεστε για **εξαγωγή κειμένου από εικόνες** για επόμενη επεξεργασία.

### Αναμενόμενη Έξοδος

```
C:\MyImages\BatchResults\image1.txt
C:\MyImages\BatchResults\image2.txt
...
```

Ανοίξτε οποιοδήποτε από αυτά τα αρχεία και θα δείτε την απλή κειμενική αναπαράσταση του περιεχομένου της εικόνας.

## Βήμα 6: Επαληθεύστε τα Αποτελέσματα (Προαιρετικό)

Είναι καλή συνήθεια να ελέγχετε μερικά αρχεία για να βεβαιωθείτε ότι το OCR λειτούργησε όπως αναμενόταν. Ένας γρήγορος τρόπος είναι να διαβάσετε την πρώτη γραμμή κάθε παραγόμενου αρχείου και να την εκτυπώσετε στην κονσόλα:

```csharp
foreach (var txtFile in Directory.GetFiles(outputPath, "*.txt"))
{
    var firstLine = File.ReadLines(txtFile).FirstOrDefault();
    Console.WriteLine($"{Path.GetFileName(txtFile)} → {firstLine}");
}
```

Αν παρατηρήσετε ακατάλληλους χαρακτήρες, σκεφτείτε να αλλάξετε τη ρύθμιση `Language` ή να βελτιώσετε την ποιότητα της εικόνας (π.χ., αυξήστε DPI, μετατρέψτε σε γκρι κλίμακα).

## Προχωρημένες Παραλλαγές & Ακραίες Περιπτώσεις

### 1. Παράκαμψη Γλώσσας ανά Αρχείο
Μερικές φορές ένα batch περιέχει πολύγλωσσα έγγραφα. Μπορείτε να ελέγξετε το όνομα κάθε εικόνας και να εκχωρήσετε γλώσσα επί τόπου:

```csharp
batch.Settings = new OcrEngineSettings(); // default settings

batch.FileProcessing += (sender, args) =>
{
    if (args.FileName.Contains("_fr"))
        args.Settings.Language = Language.French;
    else if (args.FileName.Contains("_es"))
        args.Settings.Language = Language.Spanish;
    // otherwise keep the default (English)
};
```

### 2. Διαφορετικές Μορφές Εξόδου
Αν χρειάζεστε αναζητήσιμα PDF αντί για απλό κείμενο, αλλάξτε το `OutputFormat`:

```csharp
batch.OutputFormat = OcrOutputFormat.SearchablePdf;
```

Αυτό θα **μετατρέψει εικόνες σε κείμενο** μέσα σε ένα PDF container, διατηρώντας την αρχική διάταξη.

### 3. Διαχείριση Μεγάλων Εικόνων
Πολύ υψηλής ανάλυσης εικόνες μπορούν να εξαντλήσουν τη μνήμη. Για να κρατήσετε τη διαδικασία ελαφριά, ενεργοποιήστε τη μείωση ανάλυσης εικόνας:

```csharp
batch.Settings.Dpi = 300; // lowers internal processing DPI
```

### 4. Καταγραφή Σφαλμάτων
Ο επεξεργαστής πετάει εξαιρέσεις για μη αναγνώσιμα αρχεία. Τυλίξτε το `Execute` σε try/catch και καταγράψτε τα προβληματικά ονόματα αρχείων:

```csharp
try
{
    batch.Execute();
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed on {ex.Data["FileName"]}: {ex.Message}");
}
```

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας τα παραπάνω, εδώ είναι το πλήρες, έτοιμο‑για‑αντιγραφή‑και‑επικόλληση πρόγραμμα:

```csharp
using Aspose.OCR.Batch;
using Aspose.OCR.Settings;
using System;
using System.IO;
using System.Linq;
using System.Threading.Tasks;

class Program
{
    static void Main()
    {
        // 1️⃣ Input & output locations
        var inputFolder  = @"C:\MyImages\BatchInput";
        var outputFolder = @"C:\MyImages\BatchResults";

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ OCR settings – set OCR language
        var ocrSettings = new OcrEngineSettings
        {
            Language = Language.English // change as needed
        };

        // 3️⃣ Configure the batch processor
        var batch = new OcrBatchProcessor
        {
            InputFolder    = inputFolder,
            OutputFolder   = outputFolder,
            OutputFormat   = OcrOutputFormat.PlainText, // **save OCR as text**
            ParallelOptions = new ParallelOptions { MaxDegreeOfParallelism = 4 },
            Settings       = ocrSettings
        };

        // 4️⃣ Run the batch job
        batch.Execute();

        // 5️⃣ Confirmation message
        Console.WriteLine("Batch OCR completed.");

        // 6️⃣ (Optional) Quick verification of a few results
        foreach (var txtFile in Directory.GetFiles(outputFolder, "*.txt").Take(5))
        {
            var firstLine = File.ReadLines(txtFile).FirstOrDefault();
            Console.WriteLine($"{Path.GetFileName(txtFile)} → {firstLine}");
        }
    }
}
```

Αποθηκεύστε το ως `Program.cs`, δημιουργήστε το έργο και τρέξτε `dotnet run`. Θα δείτε την έξοδο της κονσόλας που επιβεβαιώνει την ολοκλήρωση, ακολουθούμενη από μια σύντομη προεπισκόπηση του εξαγόμενου κειμένου.

---

## Συμπέρασμα

Μόλις καλύψαμε **πώς να κάνετε batch OCR** σε C# χρησιμοποιώντας το Aspose.OCR, δείχνοντάς σας πώς να **εξάγετε κείμενο από εικόνες**, **μετατρέψετε εικόνες σε κείμενο**, και **αποθηκεύσετε OCR ως κείμενο** ενώ **ρυθμίζετε τη γλώσσα OCR** ώστε να ταιριάζει στο περιεχόμενό σας. Το παράδειγμα είναι πλήρως λειτουργικό, περιλαμβάνει παράλληλη επεξεργασία για ταχύτητα, και προσφέρει σημεία επέκτασης για προχωρημένα σενάρια όπως παρακάμψεις γλώσσας ανά αρχείο ή έξοδο PDF.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να αντικαταστήσετε το `OcrOutputFormat.PlainText` με `SearchablePdf` και δείτε πόσο εύκολο είναι να δημιουργήσετε αναζητήσιμα PDF. Ή πειραματιστείτε με διαφορετικές τιμές `MaxDegreeOfParallelism` για να εξαγάγετε κάθε τελευταίο χιλιοστό του δευτερολέπτου σε ένα πολυπύρηνο μηχάνημα.

Αν αντιμετωπίσετε προβλήματα, ελέγξτε ξανά τις διαδρομές των φακέλων, βεβαιωθείτε ότι οι εικόνες είναι αναγνώσιμες, και επαληθεύστε ότι το enum γλώσσας ταιριάζει με το κείμενο στις εικόνες σας. Καλό κώδικα, και εύχομαι τα batch OCR σας να είναι γρήγορα και ακριβή!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}