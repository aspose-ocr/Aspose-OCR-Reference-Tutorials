---
category: general
date: 2026-02-09
description: Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας C# offline OCR. Ένα πλήρες
  παράδειγμα OCR σε C# δείχνει πώς να φορτώσετε εικόνα για OCR, να αναγνωρίσετε κυριλλικό
  κείμενο και να εξάγετε κείμενο από διαβατήριο.
draft: false
keywords:
- extract text from image
- c# ocr example
- load image for ocr
- recognize cyrillic text
- recognize text from passport
language: el
og_description: Εξάγετε κείμενο από εικόνα με C# offline OCR. Μάθετε ένα βήμα‑βήμα
  παράδειγμα C# OCR που φορτώνει μια εικόνα για OCR, αναγνωρίζει κυριλλικό κείμενο
  και εξάγει κείμενο από διαβατήριο.
og_title: Εξαγωγή κειμένου από εικόνα σε C# – Οδηγός OCR εκτός σύνδεσης
tags:
- OCR
- C#
- Aspose
title: Εξαγωγή κειμένου από εικόνα σε C# – Παράδειγμα offline OCR
url: /el/net/text-recognition/extract-text-from-image-in-c-offline-ocr-example/
---

didn't translate any code block placeholders.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Εικόνα σε C# – Παράδειγμα Offline OCR

Έχετε χρειαστεί ποτέ να **εξάγετε κείμενο από εικόνα** αλλά να έχετε κολλήσει σε APIs που εξαρτώνται από το δίκτυο; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν πρόβλημα όταν η υπηρεσία OCR προσπαθεί να κατεβάσει πακέτα γλωσσών κατά την εκτέλεση, ειδικά σε περιορισμένα περιβάλλοντα.

Σε αυτόν τον οδηγό θα περάσουμε από ένα **c# ocr example** που εκτελείται εξ ολοκλήρου offline, φορτώνει μια εικόνα για OCR και αναγνωρίζει κυριλλικό κείμενο από διαβατήριο. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση πρόγραμμα που εκτυπώνει το απλό‑κείμενο περιεχόμενο οποιασδήποτε υποστηριζόμενης εικόνας απευθείας στην κονσόλα.

## Τι Θα Μάθετε

- Πώς να ρυθμίσετε το Aspose.OCR για offline επεξεργασία.  
- Ο ακριβής κώδικας για **load image for OCR** από δίσκο.  
- Πώς να διαμορφώσετε τη μηχανή ώστε **recognize cyrillic text**.  
- Ένα πλήρες, έτοιμο για αντιγραφή‑επικόλληση **c# ocr example** που εξάγει κείμενο από φωτογραφία τύπου διαβατηρίου.  

Δεν απαιτείται προηγούμενη εμπειρία με το Aspose· αρκεί ένα .NET 6 (ή νεότερο) SDK και Visual Studio 2022 (ή VS Code).

---

![Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας Aspose OCR σε φωτογραφία διαβατηρίου](/images/ocr-passport.jpg "εξαγωγή κειμένου από εικόνα")

## Βήμα 1: Ρύθμιση του Έργου για Εξαγωγή Κειμένου από Εικόνα

Πριν γράψετε οποιονδήποτε κώδικα, βεβαιωθείτε ότι το πακέτο NuGet Aspose.OCR έχει προστεθεί στο έργο σας:

```bash
dotnet add package Aspose.OCR
```

> **Συμβουλή:** Χρησιμοποιήστε τη σημαία `--version` για να κλειδώσετε στην πιο πρόσφατη σταθερή έκδοση (π.χ., `13.9.0`). Αυτό εγγυάται τη συμβατότητα με το .NET 6.

Η δημιουργία μιας νέας εφαρμογής κονσόλας είναι τόσο απλή:

```bash
dotnet new console -n OfflineOcrDemo
cd OfflineOcrDemo
```

Τώρα έχετε ένα καθαρό ξεκίνημα όπου θα **extract text from image** χωρίς ποτέ να αγγίξετε το διαδίκτυο.

## Βήμα 2: Φόρτωση Εικόνας για OCR – Ανάγνωση της Φωτογραφίας Διαβατηρίου

Το πρώτο που χρειάζεται η μηχανή OCR είναι ένα bitmap ή stream που αντιπροσωπεύει την εικόνα. Στο σενάριό μας θα **load image for OCR** από ένα τοπικό αρχείο που ονομάζεται `cyrillic_passport.jpg`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

// Step 2: Load the image file (this is the “load image for ocr” part)
var imagePath = @"YOUR_DIRECTORY\cyrillic_passport.jpg";

// Validate the file exists – helpful when the path is wrong.
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// ImageStream abstracts the underlying format; it works with JPEG, PNG, etc.
var image = ImageStream.FromFile(imagePath);
```

> **Γιατί είναι σημαντικό:** Η παροχή ενός stream αντί για ένα ακατέργαστο `Bitmap` επιτρέπει στο Aspose να διαχειρίζεται την ανίχνευση μορφής εσωτερικά, μειώνοντας το boilerplate και πιθανά σφάλματα.

## Βήμα 3: Διαμόρφωση Offline Λειτουργίας και Επιλογή Κυριλλικής Γλώσσας

Το Aspose.OCR μπορεί να κατεβάσει μοντέλα γλώσσας εν κινήσει, αλλά αυτό αναιρεί τον σκοπό μιας offline λύσης. Απενεργοποιήστε τις κλήσεις δικτύου και δηλώστε ρητά στη μηχανή ποια γλώσσα να χρησιμοποιήσει.

```csharp
// Step 3: Create the OCR engine and switch to offline mode
var ocrEngine = new OcrEngine
{
    Configuration =
    {
        OfflineMode = true,               // No network traffic – perfect for secure environments
        Language = new[] { OcrLanguage.Cyrillic } // We want to **recognize cyrillic text**
    }
};
```

> **Περίπτωση άκρης:** Αν αργότερα χρειαστεί να **recognize** λατινικούς χαρακτήρες στο ίδιο έγγραφο, απλώς προσθέστε `OcrLanguage.English` στον πίνακα. Η μηχανή θα διαχειριστεί αυτόματα την ανίχνευση πολλαπλών γλωσσών.

## Βήμα 4: Εκτέλεση της Μηχανής OCR και Αναγνώριση Κυριλλικού Κειμένου

Τώρα πραγματικά **recognize text from passport**‑style εικόνες. Η μέθοδος `Recognize` επιστρέφει ένα πλούσιο αντικείμενο αποτελέσματος που περιέχει το plain text, τα confidence scores και τα bounding boxes.

```csharp
// Step 4: Perform the OCR operation
OcrResult result = ocrEngine.Recognize(image);

// Step 5: Output the plain text – this is where we finally **extract text from image**
Console.WriteLine("📝 Extracted Text:");
Console.WriteLine("-------------------");
Console.WriteLine(result.PlainText);
```

### Αναμενόμενη Έξοδος Κονσόλας

```
📝 Extracted Text:
-------------------
ПАСПОРТ РФ
Иванов Иван Иванович
01.01.1990
...
```

Αν το αποτέλεσμα φαίνεται χαοτικό, ελέγξτε ξανά ότι η πηγή εικόνας είναι καθαρή και ότι το πακέτο γλώσσας `OfflineMode` για Κυριλλικά υπάρχει στον φάκελο εγκατάστασης του Aspose (συνήθως `\Aspose.OCR\resources\languages`).

## Πλήρες Παράδειγμα C# OCR – Ολόκληρος Κώδικας

Παρακάτω βρίσκεται το **c# ocr example** στο σύνολό του. Αντιγράψτε‑επικολλήστε το στο `Program.cs` και εκτελέστε `dotnet run`. Ό,τι χρειάζεστε για **extract text from image** είναι εδώ.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

class OfflineExample
{
    static void Main()
    {
        // --------------------------------------------------------------
        // Step 1: Create the OCR engine (offline mode)
        // --------------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Configuration =
            {
                OfflineMode = true,                     // No network calls
                Language = new[] { OcrLanguage.Cyrillic } // Recognize Cyrillic text
            }
        };

        // --------------------------------------------------------------
        // Step 2: Load the image for OCR (passport photo)
        // --------------------------------------------------------------
        var imagePath = @"YOUR_DIRECTORY\cyrillic_passport.jpg";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"❌ Image not found at {imagePath}");
            return;
        }

        var image = ImageStream.FromFile(imagePath);

        // --------------------------------------------------------------
        // Step 3: Recognize the text
        // --------------------------------------------------------------
        var result = ocrEngine.Recognize(image);

        // --------------------------------------------------------------
        // Step 4: Output the plain text (the final extraction)
        // --------------------------------------------------------------
        Console.WriteLine("📝 Extracted Text:");
        Console.WriteLine("-------------------");
        Console.WriteLine(result.PlainText);
    }
}
```

### Εκτέλεση του Παραδείγματος

```bash
dotnet run
```

Θα πρέπει να δείτε την κονσόλα να εκτυπώνει τα στοιχεία του διαβατηρίου στα Κυριλλικά. Αυτή είναι η στιγμή που ξέρετε ότι η **extract text from image** pipeline λειτουργεί.

## Συνηθισμένα Προβλήματα & Πώς να Τα Διορθώσετε

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Κενό `PlainText` | Λάθος μοντέλο γλώσσας ή εικόνα πολύ σκοτεινή | Βεβαιωθείτε ότι η γλώσσα `OfflineMode` περιλαμβάνει `Cyrillic` και αυξήστε την αντίθεση της εικόνας |
| `System.DllNotFoundException` | Λείπουν τα εγγενή δυαδικά αρχεία Aspose OCR | Επανεγκαταστήστε το πακέτο NuGet ή αντιγράψτε το `Aspose.OCR.Native.dll` στο φάκελο εξόδου |
| Αργή απόδοση σε μεγάλες εικόνες | Η μηχανή επεξεργάζεται πλήρη ανάλυση | Μειώστε την εικόνα σε πλάτος ≤ 1500 px πριν τη δώσετε στο `ImageStream` |
| Ακατάστατοι χαρακτήρες | Η εικόνα είναι περιστραμμένη λανθασμένα | Χρησιμοποιήστε `Image.RotateFlip(RotateFlipType.Rotate90FlipNone)` πριν δημιουργήσετε το stream |

## Επόμενα Βήματα – Επέκταση του Offline OCR Workflow

- **Load image for OCR** από ένα `MemoryStream` όταν χειρίζεστε ανεβασμένα αρχεία σε ASP.NET Core.  
- Μεταβείτε σε **recognize text from passport** σε λειτουργία batch επαναλαμβάνοντας έναν φάκελο με σάρωση διαβατηρίων.  
- Συνδυάστε το αποτέλεσμα με **regular expressions** για να εξάγετε πεδία όπως αριθμός διαβατηρίου ή ημερομηνία γέννησης.  
- Δοκιμάστε το `ocrEngine.Configuration.UseParallelProcessing = true` για επιταχύνσεις πολλαπλών πυρήνων.

---

### Συμπέρασμα

Μόλις σας δείξαμε πώς να **extract text from image** χρησιμοποιώντας μια πλήρως offline C# OCR pipeline. Το σύντομο, αυτόνομο **c# ocr example** φορτώνει μια εικόνα, διαμορφώνει τη μηχανή για **recognize cyrillic text**, και εκτυπώνει τα εξαγόμενα δεδομένα διαβατηρίου—όλα χωρίς καμία αίτηση στο δίκτυο.

Μη διστάσετε να τροποποιήσετε τον κώδικα, να προσθέσετε περισσότερες γλώσσες ή να συνδέσετε το αποτέλεσμα σε μια βάση δεδομένων. Ο ουρανός είναι το όριο μόλις κατακτήσετε τα βασικά της φόρτωσης εικόνας για OCR και της αναγνώρισης κειμένου από φωτογραφία τύπου διαβατηρίου.

Έχετε ερωτήσεις ή θέλετε να μοιραστείτε τις δικές σας προσαρμογές; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}