---
category: general
date: 2026-03-28
description: Μάθετε πώς να κάνετε μαζική OCR σε C# και να μετατρέπετε εύκολα TIFF
  σε κείμενο. Αυτός ο οδηγός βήμα‑βήμα δείχνει την εξαγωγή κειμένου από αρχεία TIFF
  χρησιμοποιώντας το Aspose OCR.
draft: false
keywords:
- how to batch ocr
- convert tiff to text
- extract text from tiff
- c# ocr tutorial
language: el
og_description: Πώς να κάνετε ομαδική OCR σε C#; Ακολουθήστε αυτό το πλήρες σεμινάριο
  για να μετατρέψετε αρχεία TIFF πολλαπλών σελίδων σε αναζητήσιμο κείμενο χρησιμοποιώντας
  το Aspose OCR.
og_title: Πώς να εκτελέσετε ομαδική OCR σε C# – Μετατροπή πολυσελίδων TIFF σε κείμενο
tags:
- OCR
- C#
- Aspose
title: Πώς να κάνετε ομαδική OCR σε C# – Μετατροπή πολυ-σελίδων TIFF σε κείμενο
url: /el/net/text-recognition/how-to-batch-ocr-in-c-convert-multi-page-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να κάνετε Batch OCR σε C# – Μετατροπή Multi‑Page TIFF σε Κείμενο

Έχετε αναρωτηθεί ποτέ **πώς να κάνετε batch OCR** σε μια στοίβα σαρωμένων σελίδων χωρίς να γράψετε βρόχο για κάθε εικόνα; Δεν είστε οι μόνοι. Σε πολλά έργα—σκεφτείτε την επεξεργασία τιμολογίων ή την ψηφιοποίηση αρχείων—η ανάγκη για **μετατροπή TIFF σε κείμενο** εμφανίζεται καθημερινά, και η επεξεργασία μιας σελίδας τη φορά γίνεται γρήγορα εφιάλτης.

Τα καλά νέα; Με λίγες γραμμές C# και το Aspose OCR μπορείτε να τροφοδοτήσετε ολόκληρο ένα multi‑page TIFF στη μηχανή και να πάρετε ένα λεξικό με αριθμούς σελίδων που αντιστοιχούν στα εξαγόμενα κείμενα. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει ακριβώς **πώς να κάνετε batch OCR**, πώς να **εξάγετε κείμενο από TIFF**, και γιατί αυτή η προσέγγιση ξεπερνά την χειροκίνητη εναλλακτική.

## Τι Θα Μάθετε

- Πώς να ρυθμίσετε τη βιβλιοθήκη Aspose OCR σε ένα έργο .NET.  
- Πώς να φορτώσετε ένα multi‑page TIFF αρχείο χρησιμοποιώντας `Image.FromMultiPageFile`.  
- Πώς να εκτελέσετε `RecognizeBatch` για να λάβετε ένα `Dictionary<int,string>` με τα αποτελέσματα ανά σελίδα.  
- Πώς να εκτυπώσετε την έξοδο σε καθαρή, αναγνώσιμη μορφή.  

Στο τέλος θα έχετε μια έτοιμη για εκτέλεση εφαρμογή console που μετατρέπει οποιοδήποτε multi‑page TIFF σε απλό κείμενο—χωρίς επιπλέον εργαλεία.

### Προαπαιτούμενα

- .NET 6.0 SDK (ή οποιαδήποτε πρόσφατη έκδοση .NET).  
- Visual Studio 2022 ή VS Code—ο αγαπημένος σας IDE είναι εντάξει.  
- Ένα έγκυρο license Aspose OCR ή ένα δωρεάν κλειδί αξιολόγησης (το API λειτουργεί χωρίς license αλλά προσθέτει υδατογράφημα).  
- Ένα δείγμα multi‑page TIFF με όνομα `multipage.tif` τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε.

> **Pro tip:** Αν εργάζεστε σε Windows, ο προεπιλεγμένος φάκελος του έργου είναι ένα βολικό σημείο για να ρίξετε το TIFF· σε Linux/macOS απλώς προσαρμόστε τη διαδρομή ανάλογα.

## Βήμα 1: Εγκατάσταση του Πακέτου NuGet Aspose OCR

Πριν γράψουμε κώδικα, χρειαζόμαστε τη βιβλιοθήκη OCR. Ανοίξτε ένα τερματικό στον φάκελο του έργου σας και τρέξτε:

```bash
dotnet add package Aspose.OCR
```

Αυτό κατεβάζει την πιο πρόσφατη σταθερή έκδοση (από Μάρτιο 2026 v23.9) και προσθέτει τα απαραίτητα DLL στο έργο σας. Δεν απαιτείται επιπλέον ρύθμιση για μια απλή εφαρμογή console.

## Βήμα 2: Δημιουργία του Σκελετού της Εφαρμογής Console

Ας δημιουργήσουμε ένα ελάχιστο πρόγραμμα που αναφέρεται στη μηχανή OCR. Οι οδηγίες `using` είναι κρίσιμες—χωρίς αυτές ο μεταγλωττιστής θα παραπονιστεί για ελλιπείς τύπους.

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;   // Required for Image class
```

> **Γιατί είναι σημαντικό:** Η κλάση `Image` βρίσκεται σε υπο‑namespace, και η παράλειψη της εισαγωγής `ImageProcessing` θα προκαλέσει σφάλμα “type or namespace not found” που μπορεί να σας κοστίσει μια ώρα εντοπισμού σφαλμάτων.

Τώρα προσθέστε τη μέθοδο `Main` και ένα σύντομο σχόλιο που περιγράφει τον σκοπό:

```csharp
/// <summary>
/// Demonstrates how to batch OCR a multi‑page TIFF and output each page's text.
/// </summary>
class BatchOcrTutorial
{
    static void Main()
    {
        // Implementation will go here
    }
}
```

## Βήμα 3: Αρχικοποίηση της Μηχανής OCR

Η `OcrEngine` είναι ο κύριος μοχλός. Η δημιουργία μιας στιγμής της μία φορά και η επαναχρησιμοποίησή της για όλες τις σελίδες είναι τόσο αποδοτική μνήμης όσο και γρήγορη.

```csharp
// Step 3: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

> **Τι συμβαίνει στο παρασκήνιο;** Η μηχανή φορτώνει μοντέλα γλώσσας και προ‑ρυθμίζει τις προεπιλεγμένες ρυθμίσεις (π.χ., Αγγλικά, αυτόματη περιστροφή). Μπορείτε να τις τροποποιήσετε αργότερα, αλλά οι προεπιλογές είναι αξιόπιστες για τα περισσότερα έγγραφα.

## Βήμα 4: Φόρτωση του Multi‑Page TIFF

Το Aspose κάνει τη φόρτωση εικόνων πολλαπλών πλαισίων άνετη. Δώστε τη πλήρη διαδρομή ή μια σχετική από το τρέχον φάκελο του εκτελέσιμου.

```csharp
// Step 4: Load a multi‑page TIFF image
string tiffPath = "YOUR_DIRECTORY/multipage.tif";   // ← replace with your actual path
var multiPageImage = Image.FromMultiPageFile(tiffPath);
```

Αν το αρχείο δεν βρεθεί, το `FromMultiPageFile` ρίχνει `FileNotFoundException`. Τυλίξτε το σε `try/catch` αν χρειάζεστε ευγενική διαχείριση σφαλμάτων—κάτι που θα δείξουμε στο επόμενο βήμα.

## Βήμα 5: Εκτέλεση Batch OCR

Τώρα έρχεται το αστέρι της παράστασης: `RecognizeBatch`. Επιστρέφει ένα `Dictionary<int,string>` όπου το κλειδί είναι ο δείκτης σελίδας (ξεκινώντας από 0) και η τιμή το αναγνωρισμένο κείμενο.

```csharp
// Step 5: Perform batch OCR on all pages
Dictionary<int, string> ocrResults = ocrEngine.RecognizeBatch(multiPageImage);
```

> **Ακραία περίπτωση:** Κάποια TIFF περιέχουν κενές σελίδες. Το Aspose επιστρέφει κενή συμβολοσειρά για αυτές τις σελίδες, την οποία μπορείτε να φιλτράρετε αργότερα αν δεν θέλετε άσκοπο κείμενο στην έξοδο.

## Βήμα 6: Εμφάνιση των Αποτελεσμάτων

Τέλος, επαναλάβετε το λεξικό και εκτυπώστε το κείμενο κάθε σελίδας. Η χρήση interpolated strings κρατά τον κώδικα καθαρό.

```csharp
// Step 6: Output the recognized text for each page
foreach (var pageResult in ocrResults)
{
    Console.WriteLine($"--- Page {pageResult.Key + 1} ---"); // +1 for human‑friendly numbering
    Console.WriteLine(pageResult.Value);
    Console.WriteLine(); // Blank line for readability
}
```

Η εκτέλεση του προγράμματος θα πρέπει να παράγει κάτι σαν:

```
--- Page 1 ---
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
...

--- Page 2 ---
Terms and Conditions
...
```

Αν δείτε ακατανόητο κείμενο, ελέγξτε ξανά ότι το πηγαίο TIFF δεν είναι κατεστραμμένο και ότι η γλώσσα του κειμένου ταιριάζει με την προεπιλεγμένη γλώσσα της μηχανής (Αγγλικά). Μπορείτε επίσης να ορίσετε `ocrEngine.Language = OcrLanguage.Spanish;` για μη‑Αγγλικά έγγραφα.

## Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας όλα τα κομμάτια, εδώ είναι το ολοκληρωμένο πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε στο `Program.cs` και να τρέξετε:

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;   // Needed for Image class

/// <summary>
/// Demonstrates how to batch OCR a multi‑page TIFF and output each page's text.
/// </summary>
class BatchOcrTutorial
{
    static void Main()
    {
        try
        {
            // Step 1: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Step 2: Load a multi‑page TIFF image
            string tiffPath = "YOUR_DIRECTORY/multipage.tif";   // Change to your actual file location
            var multiPageImage = Image.FromMultiPageFile(tiffPath);

            // Step 3: Perform batch OCR on all pages
            Dictionary<int, string> ocrResults = ocrEngine.RecognizeBatch(multiPageImage);

            // Step 4: Output the recognized text for each page
            foreach (var pageResult in ocrResults)
            {
                Console.WriteLine($"--- Page {pageResult.Key + 1} ---");
                Console.WriteLine(pageResult.Value);
                Console.WriteLine(); // Extra line for visual separation
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
        }
    }
}
```

Αποθηκεύστε, κάντε build, και τρέξτε:

```bash
dotnet run
```

Θα πρέπει να δείτε το εξαγόμενο περιεχόμενο κάθε σελίδας να εκτυπώνεται στην κονσόλα. Αυτό είναι ολόκληρο το **c# ocr tutorial** που ζητήσατε.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν το TIFF μου περιέχει δεκάδες σελίδες;

Το `RecognizeBatch` επεξεργάζεται όλα τα πλαίσια σε μία κλήση, αλλά η χρήση μνήμης αυξάνεται γραμμικά με τον αριθμό των σελίδων. Για πολύ μεγάλα έγγραφα (εκατοντάδες σελίδες) σκεφτείτε την επεξεργασία σε τμήματα:

```csharp
for (int i = 0; i < multiPageImage.PageCount; i += 50)
{
    var subImage = multiPageImage.GetPages(i, Math.Min(50, multiPageImage.PageCount - i));
    var partialResults = ocrEngine.RecognizeBatch(subImage);
    // Merge partialResults into the main dictionary...
}
```

### Μπορώ να αποθηκεύσω το εξαγόμενο κείμενο σε αρχεία αντί για εκτύπωση;

Απολύτως. Αντικαταστήστε το τμήμα `Console.WriteLine` με λειτουργίες I/O αρχείων:

```csharp
string outputFolder = "ExtractedText";
Directory.CreateDirectory(outputFolder);

foreach (var pageResult in ocrResults)
{
    string filePath = Path.Combine(outputFolder, $"Page_{pageResult.Key + 1}.txt");
    File.WriteAllText(filePath, pageResult.Value);
}
```

Τώρα κάθε σελίδα θα έχει το δικό της αρχείο `.txt`—τέλεια για επόμενη ευρετηρίαση.

### Πώς αλλάζω τη γλώσσα εξόδου ή ενεργοποιώ την αυτόματη περιστροφή;

```csharp
ocrEngine.Language = OcrLanguage.French; // or any supported language
ocrEngine.AutoRotate = true;             // Detects rotated text automatically
```

Αυτές οι ρυθμίσεις πρέπει να εφαρμοστούν **πριν** καλέσετε το `RecognizeBatch`.

## Συμπέρασμα

Καλύψαμε **πώς να κάνετε batch OCR** σε ένα multi‑page TIFF χρησιμοποιώντας το Aspose OCR σε C#. Φορτώνοντας την εικόνα μία φορά, καλώντας το `RecognizeBatch` και επαναλαμβάνοντας το λεξικό που προκύπτει, μπορείτε να **μετατρέψετε TIFF σε κείμενο** σε δευτερόλεπτα. Το παράδειγμα δείχνει επίσης πώς να **εξάγετε κείμενο από TIFF**, να διαχειριστείτε σφάλματα, και προαιρετικά να γράψετε τα αποτελέσματα σε αρχεία—όλα μέσα σε μια καθαρή, αυτόνομη εφαρμογή console.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να συνδυάσετε αυτήν την προσέγγιση με μια βιβλιοθήκη δημιουργίας PDF για παραγωγή αναζητήσιμων PDF, ή συνδέστε την έξοδο με μια βάση δεδομένων για ευρετήρια αρχεία. Μπορείτε επίσης να πειραματιστείτε με άλλες μορφές εικόνας (PNG, JPEG) αντικαθιστώντας το `Image.FromMultiPageFile` με `Image.FromFile`.

Έχετε περισσότερες ερωτήσεις για OCR, licensing ή βελτιστοποίηση απόδοσης; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική διασκέδαση!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}