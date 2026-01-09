---
category: general
date: 2026-01-09
description: Εξαγωγή κειμένου από αρχεία TIFF χρησιμοποιώντας το Aspose OCR σε C#.
  Μάθετε πώς να λαμβάνετε τους πρώτους 50 χαρακτήρες από κάθε αποτέλεσμα σε αυτόν
  τον οδηγό βήμα‑βήμα.
draft: false
keywords:
- extract text from tiff
- get first 50 characters
- aspose ocr c# tutorial
language: el
og_description: Εξαγωγή κειμένου από TIFF χρησιμοποιώντας το Aspose OCR σε C#. Αυτός
  ο οδηγός δείχνει πώς να λαμβάνετε τους πρώτους 50 χαρακτήρες από κάθε αποτέλεσμα
  OCR, βήμα προς βήμα.
og_title: Εξαγωγή κειμένου από TIFF με Aspose OCR – Πλήρης οδηγός C#
tags:
- Aspose OCR
- C#
- TIFF processing
title: Εξαγωγή κειμένου από TIFF με Aspose OCR C# – Πλήρης οδηγός
url: /el/net/text-recognition/extract-text-from-tiff-with-aspose-ocr-c-full-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από TIFF – Πλήρης Οδηγός Aspose OCR C#

Έχετε ποτέ χρειαστεί να **εξάγετε κείμενο από εικόνες TIFF** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη να εμπιστευτείτε; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν πρόβλημα όταν προσπαθούν να εξάγουν αναζητήσιμο κείμενο από πολυσελιδικές TIFF, ειδικά όταν η απόδοση είναι σημαντική.

Σε αυτόν τον **aspose ocr c# οδηγό** θα περάσουμε από ένα έτοιμο παράδειγμα που όχι μόνο εξάγει το πλήρες κείμενο αλλά και δείχνει πώς να **παίρετε τους πρώτους 50 χαρακτήρες** κάθε σελίδας για γρήγορες προεπισκοπήσεις. Στο τέλος θα έχετε ένα αυτόνομο πρόγραμμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET.

## Τι Θα Χρειαστείτε

- .NET 6 (ή οποιαδήποτε πρόσφατη έκδοση .NET) – ο κώδικας μεταγλωττίζεται τόσο με .NET Core όσο και με .NET Framework.  
- Μία ενεργή άδεια Aspose.OCR για .NET (μπορείτε να ξεκινήσετε με δωρεάν δοκιμή).  
- Ένας φάκελος που περιέχει ένα ή περισσότερα αρχεία `.tif` που θέλετε να επεξεργαστείτε.  
- Visual Studio, VS Code ή οποιοδήποτε IDE προτιμάτε – το παράδειγμα είναι απλό C# οπότε η επιλογή του επεξεργαστή δεν έχει σημασία.

> **Συμβουλή:** Εάν βρίσκεστε σε διακομιστή CI, προσθέστε το πακέτο NuGet Aspose.OCR (`Aspose.OCR`) στο αρχείο έργου σας· η βιβλιοθήκη είναι πλήρως διαχειριζόμενη και δεν έχει εγγενείς εξαρτήσεις.

## Βήμα 1: Εγκατάσταση του πακέτου NuGet Aspose OCR

Πρώτα απ' όλα, ας φέρουμε τη μηχανή OCR στο έργο. Ανοίξτε ένα τερματικό στον φάκελο της λύσης σας και εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

Αυτή η εντολή κατεβάζει την πιο πρόσφατη σταθερή έκδοση (από Ιαν 2026 είναι 23.9) και ενημερώνει αυτόματα το `.csproj` σας. Δεν απαιτείται χειροκίνητη διαχείριση DLL.

## Βήμα 2: Αρχικοποίηση της Μηχανής OCR

Τώρα δημιουργούμε μια παρουσία του `OcrEngine`. Σκεφτείτε το ως το “εγκέφαλο” που θα διαβάσει κάθε σελίδα TIFF.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Step 2: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: tweak recognition settings if you know the language
            // ocrEngine.Language = Language.English;
            // ocrEngine.Dpi = 300; // higher DPI can improve accuracy
```

Γιατί δημιουργούμε την μηχανή μόνο μία φορά; Επειδή το `RecognizeImages` μπορεί να δεχτεί μια συλλογή διαδρομών αρχείων, επιτρέποντας στη μηχανή να επαναχρησιμοποιεί εσωτερικές μνήμες και να επιταχύνει δραματικά την επεξεργασία δέσμης.

## Βήμα 3: Συλλογή Όλων των Αρχείων TIFF με Μία Κλήση

Αντί να κάνετε βρόχο στον κατάλογο εσείς, αφήνουμε το .NET να κάνει τη βαριά δουλειά. Η μέθοδος `Directory.GetFiles` επιστρέφει ένα `IEnumerable<string>` που μπορούμε να περάσουμε απευθείας στην κλήση OCR.

```csharp
            // Step 3: Collect all TIFF images from the batch folder
            IEnumerable<string> imageFiles = Directory.GetFiles(@"YOUR_DIRECTORY/Batch", "*.tif");

            if (!imageFiles.Any())
            {
                Console.WriteLine("No TIFF files found in the specified folder.");
                return;
            }
```

> **Τι γίνεται αν οι εικόνες μου είναι JPEG ή PNG;** Απλώς αλλάξτε το πρότυπο αναζήτησης (`"*.jpg"` ή `"*.*"`). Το Aspose OCR λειτουργεί με όλες τις κοινές μορφές raster.

## Βήμα 4: Εκτέλεση OCR στην Ολόκληρη Συλλογή

Αυτή είναι η μαγική γραμμή που επεξεργάζεται κάθε αρχείο σε μία μόνο αίτηση. Η μέθοδος επιστρέφει ένα λεξικό όπου το κλειδί είναι η διαδρομή του αρχείου και η τιμή είναι ένα αντικείμενο `OcrResult` που περιέχει το αναγνωρισμένο κείμενο.

```csharp
            // Step 4: Perform OCR on the entire collection in one call
            var ocrResults = ocrEngine.RecognizeImages(imageFiles);
```

Γιατί η επεξεργασία δέσμης; Μειώνει το κόστος φόρτωσης της μηχανής OCR επανειλημμένα, και σε πολυπύρηνες μηχανές το Aspose παράλληλοποιεί εσωτερικά τη δουλειά, προσφέροντας αισθητή αύξηση ταχύτητας.

## Βήμα 5: Εμφάνιση Προεπισκόπησης – Λήψη Πρώτων 50 Χαρακτήρων

Οι περισσότερες περιπτώσεις UI χρειάζονται μόνο ένα απόσπασμα, όχι ολόκληρο το έγγραφο. Θα εξάγουμε τους πρώτους 50 χαρακτήρες (ή λιγότερους αν η σελίδα είναι σύντομη) και θα τους εκτυπώσουμε μαζί με το όνομα του αρχείου.

```csharp
            // Step 5: Display each file name with a preview of the recognized text
            foreach (var entry in ocrResults) // entry.Key = file path, entry.Value = OcrResult
            {
                string fileName = Path.GetFileName(entry.Key);
                string fullText = entry.Value.Text ?? string.Empty;
                string preview = fullText.Substring(0, Math.Min(50, fullText.Length));

                Console.WriteLine($"{fileName} → {preview}...");
            }
        }
    }
}
```

Η γραμμή `Math.Min(50, fullText.Length)` εγγυάται ότι δεν υπερβαίνουμε τα όρια της συμβολοσειράς – ένα μικρό μέτρο ασφαλείας που αποτρέπει το `ArgumentOutOfRangeException` όταν το αποτέλεσμα OCR είναι μικρότερο από 50 χαρακτήρες.

### Αναμενόμενη Εξαγωγή στην Κονσόλα

Υποθέτοντας ότι έχετε δύο αρχεία TIFF (`invoice1.tif` και `receipt2.tif`) η κονσόλα μπορεί να εμφανίσει:

```
invoice1.tif → Invoice Number: 2025-07-14 Date: 07/14/...
receipt2.tif → Store: QuickMart Total: $23.45 Date: ...
```

Κάθε γραμμή τελειώνει με αποσιωπητικά (`...`) για να υποδείξει ότι η προεπισκόπηση είναι μόνο η αρχή ενός μεγαλύτερου κειμένου.

## Βήμα 6: Διαχείριση Ακραίων Περιπτώσεων και Συνηθισμένων Παγίδων

### Κενά ή Κατεστραμμένα Αρχεία

Αν ένα αρχείο δεν μπορεί να διαβαστεί, το `RecognizeImages` εξακολουθεί να επιστρέφει μια καταχώρηση με κενή ιδιότητα `Text`. Μπορείτε να τις φιλτράρετε:

```csharp
if (string.IsNullOrWhiteSpace(fullText))
{
    Console.WriteLine($"{fileName} → (No recognizable text)");
    continue;
}
```

### Μεγάλες Δέσμες

Η επεξεργασία χιλιάδων TIFF μπορεί να καταναλώσει πολύ μνήμη. Σε τέτοιες περιπτώσεις, χρησιμοποιήστε την υπερφόρτωση που δέχεται ένα `Stream` ανά εικόνα, ή επεξεργαστείτε τη λίστα σε μικρότερα τμήματα:

```csharp
var batches = imageFiles.Chunk(100); // .NET 6+ extension
foreach (var batch in batches)
{
    var batchResults = ocrEngine.RecognizeImages(batch);
    // handle batchResults...
}
```

### Υποστήριξη Γλώσσας και Γραμματοσειράς

Αν τα έγγραφά σας περιέχουν μη λατινικούς χαρακτήρες, ορίστε τη γλώσσα πριν καλέσετε το `RecognizeImages`:

```csharp
ocrEngine.Language = Language.Spanish; // or Language.MultiLanguage
```

Αυτή η μικρή ρύθμιση μπορεί να αυξήσει δραματικά την ακρίβεια.

## Βήμα 7: Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να επικολλήσετε σε ένα νέο έργο κονσόλας (`dotnet new console`) και να το τρέξετε όπως είναι (απλώς αντικαταστήστε το `YOUR_DIRECTORY/Batch` με την πραγματική διαδρομή).

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: set language or DPI for better accuracy
            // ocrEngine.Language = Language.English;
            // ocrEngine.Dpi = 300;

            // Collect all TIFF files from the batch folder
            IEnumerable<string> imageFiles = Directory.GetFiles(@"YOUR_DIRECTORY/Batch", "*.tif");

            if (!imageFiles.Any())
            {
                Console.WriteLine("No TIFF files found in the specified folder.");
                return;
            }

            // Perform OCR on the entire collection
            var ocrResults = ocrEngine.RecognizeImages(imageFiles);

            // Show a preview – get first 50 characters of each result
            foreach (var entry in ocrResults)
            {
                string fileName = Path.GetFileName(entry.Key);
                string fullText = entry.Value.Text ?? string.Empty;

                if (string.IsNullOrWhiteSpace(fullText))
                {
                    Console.WriteLine($"{fileName} → (No recognizable text)");
                    continue;
                }

                string preview = fullText.Substring(0, Math.Min(50, fullText.Length));
                Console.WriteLine($"{fileName} → {preview}...");
            }
        }
    }
}
```

Τρέξτε το πρόγραμμα με `dotnet run`. Θα πρέπει να δείτε μια σύντομη προεπισκόπηση για κάθε αρχείο TIFF, επιβεβαιώνοντας ότι έχετε εξαγάγει επιτυχώς **κείμενο από TIFF** εικόνες χρησιμοποιώντας το Aspose OCR.

## Συχνές Ερωτήσεις (FAQ)

**Ε: Λειτουργεί αυτό με πολυσελιδικά TIFF;**  
Α: Ναι. Το Aspose OCR αντιμετωπίζει κάθε σελίδα ως ξεχωριστή εικόνα εσωτερικά, έτσι ένα πολυσελιδικό TIFF παράγει μία ενιαία συνενωμένη συμβολοσειρά ανά αρχείο. Μπορείτε να τη χωρίσετε αργότερα αν χρειαστεί.

**Ε: Πόσο ακριβές είναι το OCR έτοιμο προς χρήση;**  
Α: Για καθαρές, υψηλής ανάλυσης σαρώσεις (300 DPI ή περισσότερο) μπορείτε να περιμένετε >95 % ακρίβεια στο αγγλικό κείμενο. Η προεπεξεργασία (ευθυγράμμιση, δυαδικοποίηση) μπορεί να το αυξήσει ακόμη περισσότερο.

**Ε: Μπορώ να εξάγω τα αποτελέσματα σε αρχείο CSV;**  
Α: Απόλυτα. Αντικαταστήστε το `Console.WriteLine` με ένα `StreamWriter` και γράψτε γραμμές `fileName,preview`. Θυμηθείτε να διαφύγετε τα κόμματα στο κείμενο προεπισκόπησης.

## Επόμενα Βήματα και Σχετικά Θέματα

- **Αποθήκευση αποτελεσμάτων OCR** – Αποθηκεύστε το πλήρες κείμενο σε βάση δεδομένων για αρχεία με δυνατότητα αναζήτησης.  
- **Συνδυασμός με μετατροπή PDF** – Χρησιμοποιήστε το Aspose.PDF για να ενσωματώσετε το εξαγόμενο κείμενο πίσω σε PDF με δυνατότητα αναζήτησης.  
- **Επεξεργασία δέσμης σε Azure Functions** – Κλιμακώστε την εργασία OCR χωρίς διαχείριση διακομιστών.  

Όλες αυτές οι επεκτάσεις συνδέονται με την κεντρική ιδέα της **εξαγωγής κειμένου από TIFF** αποδοτικά, ενώ εξακολουθείτε να μπορείτε να **παίρετε τους πρώτους 50 χαρακτήρες** για γρήγορες προεπισκοπήσεις UI.

*Καλό κώδικα! Αν συναντήσετε προβλήματα, αφήστε ένα σχόλιο παρακάτω – θα κάνω ό,τι μπορώ για να σας βοηθήσω να βελτιώσετε τη ροή OCR.*

![Εξαγωγή κειμένου από TIFF χρησιμοποιώντας Aspose OCR](https://example.com/images/extract-text-from-tiff.png "Εξαγωγή κειμένου από TIFF χρησιμοποιώντας Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}