---
category: general
date: 2026-02-22
description: αναγνωρίστε κείμενο από εικόνα χρησιμοποιώντας το Aspose OCR σε C#. Μάθετε
  πώς να φορτώνετε εικόνα TIFF, να δημιουργείτε μηχανή OCR και να εξάγετε κείμενο
  από την εικόνα αποδοτικά.
draft: false
keywords:
- recognize text from image
- load tiff image
- extract text from image
- create OCR engine
language: el
og_description: Αναγνωρίστε κείμενο από εικόνα βήμα‑βήμα. Μάθετε πώς να φορτώνετε
  εικόνα tiff, να δημιουργείτε μηχανή OCR και να εξάγετε κείμενο από την εικόνα με
  το Aspose OCR σε C#.
og_title: Αναγνώριση κειμένου από εικόνα – Πλήρης οδηγός C# Aspose OCR
tags:
- C#
- Aspose OCR
- Image Processing
title: Αναγνώριση κειμένου από εικόνα με το Aspose OCR – Πλήρης οδηγός C#
url: /el/net/text-recognition/recognize-text-from-image-with-aspose-ocr-complete-c-guide/
---

Also keep markdown links unchanged (none present). Images none.

Let's craft.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# αναγνώριση κειμένου από εικόνα – Πλήρες C# Aspose OCR Tutorial

Έχετε χρειαστεί ποτέ να **αναγνωρίσετε κείμενο από εικόνα** αλλά να κολλήσετε στην πρώτη γραμμή κώδικα; Δεν είστε μόνοι. Σε πολλά έργα—σάρωση τιμολογίων, ψηφιοποίηση αρχείων, ή δημιουργία βιβλιοθήκης PDF με δυνατότητα αναζήτησης—η εξαγωγή καθαρού κειμένου από μια εικόνα είναι το πρώτο εμπόδιο.  

Καλή είδηση: με το Aspose OCR μπορείτε να φορτώσετε μια εικόνα TIFF, να δημιουργήσετε μια μηχανή OCR και **να εξάγετε κείμενο από εικόνα** με λίγες μόνο γραμμές κώδικα. Σε αυτό το tutorial θα περάσουμε από όλη τη ροή, από τη φόρτωση ενός αρχείου TIFF υψηλής ανάλυσης μέχρι την εκτύπωση του αναγνωρισμένου κειμένου και του χρόνου επεξεργασίας.

Θα καλύψουμε επίσης μερικά σενάρια “τι γίνεται αν…”, όπως η απενεργοποίηση της επιτάχυνσης GPU ή η διαχείριση πολυσελίδων TIFF, ώστε να μην εκπλαγείτε όταν τα πραγματικά σας δεδομένα διαφέρουν ελαφρώς. Στο τέλος, θα έχετε μια έτοιμη εφαρμογή κονσόλας που **αναγνωρίζει κείμενο από εικόνα** αξιόπιστα.

## Προαπαιτούμενα

- .NET 6.0 SDK ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Core και .NET Framework)
- Πακέτο NuGet Aspose.OCR (`dotnet add package Aspose.OCR`)
- Ένα αρχείο TIFF που θέλετε να επεξεργαστείτε (το παράδειγμα χρησιμοποιεί `high_res_page.tif`)
- Οποιοδήποτε IDE προτιμάτε—Visual Studio, Rider ή VS Code αρκεί

Δεν απαιτούνται πρόσθετες εγγενείς βιβλιοθήκες· το Aspose διαχειρίζεται τα πάντα εσωτερικά, συμπεριλαμβανομένης της προαιρετικής υποστήριξης GPU.

## Βήμα 1: Φόρτωση εικόνας TIFF

Το πρώτο που πρέπει να κάνετε είναι να φέρετε τα δεδομένα της εικόνας στη μνήμη. Το Aspose παρέχει τη στατική μέθοδο `Image.Load` που λειτουργεί με τις περισσότερες κοινές μορφές, συμπεριλαμβανομένου του TIFF.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Load the TIFF file – replace the path with your own image location
var inputImage = Image.Load(@"YOUR_DIRECTORY/high_res_page.tif");
```

**Γιατί είναι σημαντικό:** Τα αρχεία TIFF συχνά περιέχουν πολλαπλές σελίδες ή δεδομένα υψηλής ανάλυσης που άλλες βιβλιοθήκες δεν διαχειρίζονται καλά. Ο φορτωτής του Aspose διαβάζει το αρχείο σωστά και διατηρεί το βάθος εικονοστοιχείων, κάτι κρίσιμο για ακριβή OCR αργότερα.

*Συμβουλή:* Αν εργάζεστε με πολυσελίδα TIFF, μπορείτε να κάνετε βρόχο μέσω του `inputImage.Frames` και να επεξεργαστείτε κάθε καρέ ξεχωριστά. Έτσι δεν θα χάσετε κείμενο που κρύβεται σε μεταγενέστερες σελίδες.

## Βήμα 2: Δημιουργία μηχανής OCR

Τώρα που η εικόνα βρίσκεται στη μνήμη, χρειάζεστε μια μηχανή που ξέρει πώς να διαβάζει χαρακτήρες. Η κλάση `OcrEngine` είναι εκεί όπου ρυθμίζετε τη γλώσσα, τη χρήση GPU και άλλες επιλογές.

```csharp
// Initialize the OCR engine with desired settings
var ocrEngine = new OcrEngine
{
    // Enable GPU acceleration for faster processing (optional, requires compatible hardware)
    UseGpu = true,
    // Set the language to English – you can change this to Language.French, etc.
    Language = Language.English
};
```

**Γιατί είναι σημαντικό:** Η ενεργοποίηση της GPU (`UseGpu = true`) μπορεί να μειώσει δραστικά τον χρόνο επεξεργασίας σε υποστηριζόμενες μηχανές, αλλά είναι απολύτως ασφαλές να την αφήσετε απενεργοποιημένη αν τρέχετε σε CI server ή σε χαμηλής ισχύος laptop. Επίσης, η επιλογή της σωστής γλώσσας βελτιώνει την αναγνώριση χαρακτήρων επειδή η μηχανή φορτώνει γλωσσικά λεξικά.

*Προσοχή:* Αν ξεχάσετε να ορίσετε το `Language`, η μηχανή προεπιλέγει τα Αγγλικά, κάτι που μπορεί να δώσει παράξενα αποτελέσματα σε μη‑λατινικά αλφάβητα.

## Βήμα 3: Αναγνώριση κειμένου από εικόνα

Με τη μηχανή έτοιμη, η πραγματική κλήση OCR είναι μια μόνο μέθοδος: `Recognize`. Επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει το εξαγόμενο κείμενο και μετρικές απόδοσης.

```csharp
// Perform OCR on the loaded image
var ocrResult = ocrEngine.Recognize(inputImage);
```

Το `OcrResult` παρέχει δύο χρήσιμες ιδιότητες:

- `Text` – η απλή κειμενική αναπαράσταση όλων όσων η μηχανή μπόρεσε να διαβάσει.
- `ProcessingTime` – πόσο χρόνο πήρε το OCR, μετρημένο σε χιλιοστά του δευτερολέπτου.

## Βήμα 4: Επισκόπηση των αποτελεσμάτων

Τέλος, ας εμφανίσουμε ό,τι λάβαμε. Σε μια πραγματική εφαρμογή ίσως γράψετε το κείμενο σε βάση δεδομένων, αλλά για σκοπούς επίδειξης η έξοδος στην κονσόλα αρκεί.

```csharp
// Show how long the OCR took and the recognized text
Console.WriteLine($"Recognized in {ocrResult.ProcessingTime} ms");
Console.WriteLine("=== Extracted Text Start ===");
Console.WriteLine(ocrResult.Text);
Console.WriteLine("=== Extracted Text End ===");
```

**Αναμενόμενη έξοδος** (το κείμενό σας θα διαφέρει, φυσικά):

```
Recognized in 842 ms
=== Extracted Text Start ===
Invoice #12345
Date: 2024‑01‑15
Total: $1,250.00
...
=== Extracted Text End ===
```

Αν η έξοδος φαίνεται παραμορφωμένη, ελέγξτε ξανά ότι η εικόνα είναι καθαρή και ότι έχετε επιλέξει τη σωστή γλώσσα. Μπορείτε επίσης να ρυθμίσετε ιδιότητες του `ocrEngine` όπως `PreprocessOptions` για μείωση θορύβου.

## Διαχείριση Ακραίων Περιπτώσεων

### 1. Χωρίς GPU; Κανένα πρόβλημα.

```csharp
ocrEngine.UseGpu = false; // fallback to CPU‑only processing
```

Η επεξεργασία από CPU είναι πιο αργή (συχνά 2‑3×), αλλά λειτουργεί σε κάθε μηχάνημα Windows, Linux ή macOS.

### 2. Πολυσελίδα TIFF

```csharp
foreach (var frame in inputImage.Frames)
{
    var pageResult = ocrEngine.Recognize(frame);
    Console.WriteLine(pageResult.Text);
}
```

Κάθε καρέ αντιμετωπίζεται ως ξεχωριστή εικόνα, οπότε θα λάβετε ένα τμήμα κειμένου ανά σελίδα.

### 3. Διαφορετικές γλώσσες

```csharp
ocrEngine.Language = Language.Spanish; // or Language.French, Language.German, etc.
```

Η αλλαγή γλώσσας φορτώνει το αντίστοιχο σύνολο χαρακτήρων και λεξικό, βελτιώνοντας δραματικά την ακρίβεια για έγγραφα μη‑Αγγλικά.

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα νέο έργο κονσόλας (`dotnet new console`). Περιλαμβάνει όλα τα τμήματα που συζητήσαμε, καθώς και μερικούς ελέγχους ασφαλείας.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the TIFF image you want to process
        // -------------------------------------------------
        const string imagePath = @"YOUR_DIRECTORY/high_res_page.tif";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"Error: File not found at {imagePath}");
            return;
        }

        var inputImage = Image.Load(imagePath);

        // -------------------------------------------------
        // Step 2: Create and configure the OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true,                 // optional – set to false if GPU not available
            Language = Language.English    // change if you need another language
        };

        // -------------------------------------------------
        // Step 3: Perform OCR on the loaded image
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(inputImage);

        // -------------------------------------------------
        // Step 4: Display processing time and extracted text
        // -------------------------------------------------
        Console.WriteLine($"Recognized in {ocrResult.ProcessingTime} ms");
        Console.WriteLine("=== Extracted Text Start ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("=== Extracted Text End ===");

        // Keep console window open when debugging
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

Αποθηκεύστε το αρχείο, τρέξτε `dotnet run` και παρακολουθήστε την κονσόλα να εμφανίζει το αναγνωρισμένο κείμενο. Αυτό είναι—η **αναγνώριση κειμένου από εικόνα** σας είναι έτοιμη και λειτουργεί.

## Συχνές Ερωτήσεις

**Ε: Λειτουργεί αυτό με PNG ή JPEG;**  
Α: Απόλυτα. Η `Image.Load` ανιχνεύει αυτόματα τη μορφή, οπότε μπορείτε να αντικαταστήσετε την επέκταση `.tif` με `.png`, `.jpg` ή ακόμη και `.bmp`. Η μηχανή OCR τις αντιμετωπίζει με τον ίδιο τρόπο.

**Ε: Η έξοδός μου περιέχει πολλά άσχετα σύμβολα.**  
Α: Δοκιμάστε να ενεργοποιήσετε την προεπεξεργασία: `ocrEngine.PreprocessOptions = new PreprocessOptions { RemoveNoise = true, Deskew = true };`. Αυτό καθαρίζει την εικόνα πριν την αναγνώριση.

**Ε: Μπορώ να λάβω τα πλαίσια περιθώρια (bounding boxes) για κάθε λέξη;**  
Α: Ναι. Το `ocrResult.Regions` περιέχει αντικείμενα `OcrRegion` με συντεταγμένες. Περάστε τα σε βρόχο αν χρειάζεστε να επισημάνετε λέξεις σε UI.

## Συμπέρασμα

Σας δείξαμε πώς να **αναγνωρίζετε κείμενο από εικόνα** χρησιμοποιώντας το Aspose OCR σε C#. Ξεκινώντας από τη φόρτωση ενός αρχείου TIFF, στη **δημιουργία μηχανής OCR**, την εκτέλεση της αναγνώρισης και τέλος την εμφάνιση των αποτελεσμάτων—κάθε βήμα είναι σύντομο, πλήρως εξηγημένο και έτοιμο για αντιγραφή στο δικό σας έργο.  

Από εδώ μπορείτε να εξερευνήσετε επεξεργασία δέσμης φακέλων, αποθήκευση αποτελεσμάτων σε ευρετήριο αναζήτησης ή συνδυασμό OCR με APIs μετάφρασης. Ό,τι και αν επιλέξετε, το βασικό μοτίβο παραμένει το ίδιο: φορτώστε την εικόνα, ρυθμίστε τη μηχανή, αναγνωρίστε και διαχειριστείτε την έξοδο.

Έχετε περισσότερες ερωτήσεις σχετικά με τη φόρτωση εικόνων TIFF, την εξαγωγή κειμένου από εικόνα ή τη ρύθμιση της μηχανής OCR; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική διασκέδαση!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}