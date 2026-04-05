---
category: general
date: 2026-04-04
description: Πώς να κάνετε παρτίδα OCR με το Aspose.OCR σε C#. Μάθετε να εξάγετε κείμενο
  από εικόνες, να εξάγετε σύνοψη CSV και να διαχειρίζεστε αποδοτικά το OCR μεγάλου
  όγκου εικόνων.
draft: false
keywords:
- how to batch ocr
- extract text images
- how to export csv
- bulk image ocr
- batch ocr images
language: el
og_description: Πώς να εκτελέσετε ομαδική OCR σε C# με το Aspose.OCR. Λάβετε τη πλήρη
  λύση για την εξαγωγή κειμένου από εικόνες και την εξαγωγή περιλήψεων CSV.
og_title: Πώς να κάνετε μαζική OCR σε C# – Πλήρης οδηγός βήμα‑προς‑βήμα
tags:
- OCR
- C#
- Aspose
- Automation
title: Πώς να κάνετε ομαδική OCR σε C# – Πλήρης οδηγός για εξαγωγή κειμένου από μαζικές
  εικόνες
url: /el/net/text-recognition/how-to-batch-ocr-in-c-complete-guide-for-bulk-image-text-ext/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εκτελέσετε Batch OCR – Ένας Πλήρης Οδηγός C#

Έχετε αναρωτηθεί ποτέ **πώς να κάνετε batch OCR** σε ολόκληρο φάκελο εικόνων χωρίς να γράψετε ξεχωριστή ρουτίνα για κάθε αρχείο; Δεν είστε ο μόνος. Σε πολλά πραγματικά έργα—σκεφτείτε την επεξεργασία τιμολογίων, την αρχειοθέτηση σαρωμένων βιβλίων ή τη μαζική ψηφιοποίηση αποδείξεων—οι προγραμματιστές χρειάζονται έναν γρήγορο, αξιόπιστο τρόπο για να εξάγουν κείμενο από δεκάδες ή ακόμη και χιλιάδες εικόνες.

Σε αυτόν τον οδηγό θα περάσουμε από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που δείχνει **πώς να κάνετε batch OCR**, **πώς να εξάγετε κείμενο από εικόνες**, και **πώς να εξάγετε μια σύνοψη CSV** χρησιμοποιώντας το Aspose.OCR. Στο τέλος θα έχετε ένα ενιαίο πρόγραμμα C# που μπορεί να πάρει οποιονδήποτε φάκελο εικόνων, να τα μετατρέψει σε αρχεία κειμένου αναζητήσιμα και να σας δώσει μια καθαρή αναφορά CSV της λειτουργίας. Καμία μυστήριο, μόνο καθαρός κώδικας και πρακτικές συμβουλές.

## Τι Θα Μάθετε

- Ρυθμίστε τη μηχανή Aspose.OCR για Αγγλικά (ή οποιαδήποτε υποστηριζόμενη γλώσσα).  
- Επεξεργαστείτε ολόκληρο φάκελο εικόνων σε μία φορά—ιδανικό για μαζική OCR εικόνων.  
- Αποθηκεύστε κάθε αποτέλεσμα OCR ως αρχείο `.txt` ενώ προαιρετικά δημιουργείτε ένα αρχείο CSV που καταγράφει το όνομα κάθε εικόνας και το μήκος του εξαγόμενου κειμένου.  
- Αντιμετωπίστε κοινές περιπτώσεις άκρων όπως μη υποστηριζόμενοι τύποι αρχείων, άδεια φάκελοι και χαρακτήρες Unicode.  

**Προαπαιτούμενα** – Χρειάζεστε .NET 6+ (ή .NET Framework 4.7.2+), Visual Studio 2022 ή οποιοδήποτε IDE προτιμάτε, και μια έγκυρη άδεια Aspose.OCR (η δωρεάν δοκιμή λειτουργεί για demos). Δεν απαιτούνται άλλες βιβλιοθήκες τρίτων.

![διάγραμμα batch OCR](https://example.com/ocr-flow.png "διάγραμμα ροής batch OCR")

## Βήμα 1: Εγκατάσταση Aspose.OCR και Δημιουργία Νέου Console Project

Για να ξεκινήσετε, προσθέστε το πακέτο NuGet Aspose.OCR στο πρόγραμμά σας:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Αν χρησιμοποιείτε Visual Studio, μπορείτε επίσης να κάνετε δεξί‑κλικ στο project → *Manage NuGet Packages* → αναζητήστε *Aspose.OCR* → εγκαταστήστε.

Δημιουργήστε μια νέα εφαρμογή console (`dotnet new console -n BulkOcrDemo`) και ανοίξτε το `Program.cs`. Αυτό θα είναι το σπίτι για όλο τον κώδικά μας.

## Βήμα 2: Αρχικοποίηση της Μηχανής OCR – Επιλέξτε τη Σωστή Γλώσσα

Η μηχανή OCR πρέπει να γνωρίζει ποια γλώσσα θα αναζητήσει. Τα Αγγλικά είναι τα πιο κοινά, αλλά μπορείτε να τα αντικαταστήσετε με Ισπανικά, Γαλλικά κ.λπ., αλλάζοντας το `Language.English`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;

// Step 2: Set up the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    // You can switch to Language.Spanish, Language.French, etc.
    Language = Language.English
};
```

**Γιατί είναι σημαντικό:** Η καθορισμένη γλώσσα βελτιώνει την ακρίβεια επειδή η μηχανή μπορεί να εφαρμόσει λεξικά και σύνολα χαρακτήρων ειδικά για τη γλώσσα. Αν το παραλείψετε, θα λάβετε ένα γενικό μοντέλο που μπορεί να ερμηνεύσει λανθασμένα χαρακτήρες.

## Βήμα 3: Ορισμός Διαδρομών Πηγής, Εξόδου και Προαιρετικού CSV

Χρειαζόμαστε τρεις φακέλους:

| Διαδρομή | Σκοπός |
|------|---------|
| `sourceFolder` | Όπου βρίσκονται οι αρχικές εικόνες. |
| `outputFolder` | Όπου θα αποθηκευτεί το αποτέλεσμα OCR (`.txt`) για κάθε εικόνα. |
| `csvSummaryPath` | (Προαιρετικό) Ένα αρχείο CSV που καταγράφει το όνομα κάθε εικόνας και το μήκος του εξαγόμενου κειμένου. |

```csharp
// Step 3: Folder locations – update these to match your environment
string sourceFolder = @"C:\OcrDemo\Images\Bulk";
string outputFolder = @"C:\OcrDemo\Output\BulkResults";
string csvSummaryPath = Path.Combine(outputFolder, "summary.csv"); // optional
```

> **Tip:** Χρησιμοποιήστε `Path.Combine` για συμβατότητα μεταξύ πλατφορμών· εισάγει αυτόματα το σωστό διαχωριστικό καταλόγου.

## Βήμα 4: Εκτέλεση του Batch Processor

Το Aspose.OCR παρέχει ένα χρήσιμο `BatchProcessor` που κάνει το σκληρό έργο. Διασχίζει κάθε υποστηριζόμενη εικόνα (`.png`, `.jpg`, `.tif`, κ.λπ.), εκτελεί OCR και γράφει το αποτέλεσμα.

```csharp
// Step 4: Process the entire folder
BatchProcessor.ProcessFolder(
    sourceFolder: sourceFolder,
    outputFolder: outputFolder,
    engine: ocrEngine,
    csvSummaryPath: csvSummaryPath);
```

### Τι Συμβαίνει Πίσω από τις Σκηνές;

1. **Ανακάλυψη αρχείων** – Ο επεξεργαστής σαρώει το `sourceFolder` για αρχεία εικόνας.  
2. **Εκτέλεση OCR** – Κάθε εικόνα τροφοδοτείται στη `ocrEngine`.  
3. **Αποθήκευση κειμένου** – Το αναγνωρισμένο κείμενο γράφεται σε αρχείο `.txt` με το ίδιο βασικό όνομα στο `outputFolder`.  
4. **Καταγραφή CSV** – Αν παρέχεται `csvSummaryPath`, ο επεξεργαστής προσθέτει μια γραμμή: `ImageName,CharactersExtracted,ProcessingTimeMs`.  

## Βήμα 5: Προσθήκη Διαχείρισης Σφαλμάτων και Υποστήριξης Περιπτώσεων Άκρων

Μια αξιόπιστη εργασία batch πρέπει να αντέχει σε ελλιπή αρχεία, μη υποστηριζόμενες μορφές και άδεια καταλόγους. Τυλίξτε την κλήση επεξεργασίας σε μπλοκ `try/catch` και επικυρώστε πρώτα τις εισόδους.

```csharp
try
{
    // Validate folders
    if (!Directory.Exists(sourceFolder))
        throw new DirectoryNotFoundException($"Source folder not found: {sourceFolder}");

    Directory.CreateDirectory(outputFolder); // ensures output exists

    // Optional: clean previous CSV
    if (File.Exists(csvSummaryPath))
        File.Delete(csvSummaryPath);

    // Run the batch
    BatchProcessor.ProcessFolder(
        sourceFolder: sourceFolder,
        outputFolder: outputFolder,
        engine: ocrEngine,
        csvSummaryPath: csvSummaryPath);

    Console.WriteLine("✅ Batch OCR completed successfully!");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"❌ An error occurred: {ex.Message}");
}
```

**Γιατί να το προσθέσετε;** Χωρίς επικύρωση, το πρόγραμμα μπορεί να αποτύχει σιωπηρά, αφήνοντάς σας με έναν άδειο φάκελο εξόδου και χωρίς να ξέρετε το γιατί. Τα σαφή μηνύματα κάνουν την αποσφαλμάτωση άνετη.

## Βήμα 6: Επαλήθευση των Αποτελεσμάτων – Τι Να Περιμένετε

Μετά το τέλος της εκτέλεσης, ανοίξτε το `outputFolder`. Θα πρέπει να δείτε ένα αρχείο `.txt` για κάθε εικόνα:

```
C:\OcrDemo\Output\BulkResults\invoice_001.txt
C:\OcrDemo\Output\BulkResults\receipt_2023-03-15.txt
...
```

Κάθε αρχείο περιέχει την ακατέργαστη έξοδο OCR—απλό κείμενο που μπορείτε να τροφοδοτήσετε σε ευρετήρια αναζήτησης, βάσεις δεδομένων ή περαιτέρω pipelines NLP.

Αν παρείχατε `csvSummaryPath`, ανοίξτε το `summary.csv`. Θα μοιάζει κάπως έτσι:

```
ImageName,CharactersExtracted,ProcessingTimeMs
invoice_001.png,1245,312
receipt_2023-03-15.jpg,378,98
...
```

Το CSV κάνει εξαιρετικά εύκολη τη δημιουργία αναφορών, τον εντοπισμό ασυνήθιστα σύντομων αποτελεσμάτων (πιθανές αποτυχίες σάρωσης) ή την τροφοδοσία μετρικών σε πίνακες παρακολούθησης.

## Βήμα 7: Επέκταση της Λύσης – Συνηθισμένες Παραλλαγές

### 7.1 Αλλαγή Μορφής Εξόδου

Αντί για απλό `.txt`, ίσως θέλετε PDF ή JSON. Ο `BatchProcessor` σας επιτρέπει να παρέχετε μια προσαρμοσμένη callback:

```csharp
BatchProcessor.ProcessFolder(
    sourceFolder,
    outputFolder,
    ocrEngine,
    csvSummaryPath,
    (imagePath, ocrResult) =>
    {
        // Example: save as JSON
        var json = System.Text.Json.JsonSerializer.Serialize(new { Text = ocrResult.Text });
        string jsonPath = Path.ChangeExtension(Path.Combine(outputFolder,
                              Path.GetFileNameWithoutExtension(imagePath)), ".json");
        File.WriteAllText(jsonPath, json);
    });
```

### 7.2 Επεξεργασία Πολλαπλών Γλωσσών

Αν ο φάκελός σας περιέχει έγγραφα με μεικτές γλώσσες, μπορείτε να ανιχνεύσετε τη γλώσσα ανά εικόνα ή να εκτελέσετε δύο περάσματα:

```csharp
ocrEngine.Language = Language.Spanish; // first pass
BatchProcessor.ProcessFolder(...);
ocrEngine.Language = Language.English; // second pass
BatchProcessor.ProcessFolder(...);
```

### 7.3 Παράλειψη Κατεστραμμένων Αρχείων με Ευγένεια

Προσθέστε ένα φίλτρο μέσα στον βρόχο (ή χρησιμοποιήστε την υπερφόρτωση που δέχεται πρόβλεψη) για να αγνοήσετε αρχεία που προκαλούν εξαίρεση:

```csharp
BatchProcessor.ProcessFolder(
    sourceFolder,
    outputFolder,
    ocrEngine,
    csvSummaryPath,
    filter: path => !Path.GetFileName(path).StartsWith("ignore_"));
```

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω είναι το πλήρες `Program.cs` που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε ένα νέο project console. Αντικαταστήστε τις διαδρομές φακέλων με τις δικές σας.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Batch;

namespace BulkOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine – set language to English
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Define folders – adjust these for your environment
            string sourceFolder = @"C:\OcrDemo\Images\Bulk";
            string outputFolder = @"C:\OcrDemo\Output\BulkResults";
            string csvSummaryPath = Path.Combine(outputFolder, "summary.csv"); // optional

            try
            {
                // 3️⃣ Validate folders
                if (!Directory.Exists(sourceFolder))
                    throw new DirectoryNotFoundException($"Source folder not found: {sourceFolder}");

                Directory.CreateDirectory(outputFolder); // creates if missing

                // 4️⃣ Clean previous CSV (optional)
                if (File.Exists(csvSummaryPath))
                    File.Delete(csvSummaryPath);

                // 5️⃣ Run the batch OCR
                BatchProcessor.ProcessFolder(
                    sourceFolder: sourceFolder,
                    outputFolder: outputFolder,
                    engine: ocrEngine,
                    csvSummaryPath: csvSummaryPath);

                Console.WriteLine("✅ Batch OCR completed successfully!");
                Console.WriteLine($"📂 Text files are in: {outputFolder}");
                Console.WriteLine($"📄 CSV summary (if requested) at: {csvSummaryPath}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ An error occurred during batch OCR: {ex.Message}");
            }
        }
    }
}
```

### Αναμενόμενη Έξοδος Console

```
✅ Batch OCR completed successfully!
📂 Text files are in: C:\OcrDemo\Output\BulkResults
📄 CSV summary (if requested) at: C:\OcrDemo\Output\BulkResults\summary.csv
```

Ανοίξτε ένα από τα παραγόμενα αρχεία `.txt` και θα δείτε το εξαγόμενο κείμενο, έτοιμο για περαιτέρω επεξεργασία.

## Συχνές Ερωτήσεις

**Λειτουργεί αυτό με εισόδους PDF;**  
Το Aspose.OCR μπορεί να διαχειριστεί σελίδες PDF αν πρώτα τις μετατρέψετε σε εικόνες (π.χ., χρησιμοποιώντας Aspose.PDF). Ο batch processor μόνο ψάχνει για μορφές raster εικόνας.

**Τι γίνεται αν χρειαστεί να επεξεργαστώ 10.000 εικόνες;**  
Ο ενσωματωμένος `BatchProcessor` μεταδίδει κάθε αρχείο ένα προς ένα, έτσι η χρήση μνήμης παραμένει χαμηλή. Για τεράστιες εργασίες μπορείτε να επεξεργαστείτε παράλληλα υποφακέλους, αλλά θυμηθείτε ότι το OCR είναι εντατικά CPU—παρακολουθήστε τον αριθμό πυρήνων του μηχανήματός σας.

**Μπορώ να αλλάξω τις ρυθμίσεις ακρίβειας OCR;**  
Ναι. Η `ocrEngine` εκθέτει ιδιότητες όπως `Resolution` και `PreprocessOptions`. Η ρύθμιση τους μπορεί να βελτιώσει τα αποτελέσματα σε χαμηλής ποιότητας σάρωση, με κόστος την ταχύτητα.

**Πώς αδειοδοτώ το Aspose.OCR για παραγωγή;**  
Τοποθετήστε το αρχείο άδειας (`Aspose.OCR.lic`) στον φάκελο εκτελέσιμου και φορτώστε το κατά την εκκίνηση:

```csharp
var license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

## Συμπέρασμα

Τώρα έχετε μια **πλήρη, έτοιμη για παραγωγή λύση για batch OCR** χρησιμοποιώντας C#. Ο οδηγός κάλυψε τα πάντα, από την εγκατάσταση του Aspose.OCR, την αρχικοποίηση της μηχανής, την επεξεργασία ολόκληρου φακέλου, μέχρι την εξαγωγή μιας σύνοψης CSV

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}