---
category: general
date: 2026-04-06
description: Αυξήστε την αντίθεση της εικόνας και αφαιρέστε τον θόρυβο της εικόνας
  για να βελτιώσετε την ακρίβεια του OCR σε C#. Μάθετε πώς να φορτώνετε εικόνα OCR
  και πώς να κάνετε OCR σε C# με τα φίλτρα Aspose OCR.
draft: false
keywords:
- boost image contrast
- remove image noise
- improve ocr accuracy
- load image ocr
- how to ocr c#
language: el
og_description: Αυξήστε την αντίθεση της εικόνας και αφαιρέστε τον θόρυβο της εικόνας
  για να βελτιώσετε την ακρίβεια του OCR σε C#. Αυτό το σεμινάριο δείχνει πώς να φορτώσετε
  εικόνα για OCR και πώς να κάνετε OCR σε C# χρησιμοποιώντας το Aspose.
og_title: Αύξηση της αντίθεσης εικόνας σε C# OCR – Οδηγός βήμα‑βήμα
tags:
- OCR
- C#
- Image Processing
title: Αύξηση της Αντίθεσης Εικόνας σε C# OCR – Πλήρης Οδηγός
url: /el/net/ocr-optimization/boost-image-contrast-in-c-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ενίσχυση της Αντίθεσης Εικόνας σε C# OCR – Πλήρης Οδηγός

Έχετε προσπαθήσει ποτέ να **boost image contrast** σε μια τρεμάμενη σάρωση και να λάβατε ακατάληπτο κείμενο; Δεν είστε μόνοι. Σε πολλά πραγματικά έργα η εικόνα είναι περιστραμμένη, θορυβώδης και απλώς θαμπή, κάτι που κάνει το OCR να δυσκολεύεται. Τα καλά νέα; Μερικά καλά τοποθετημένα φίλτρα μπορούν να μετατρέψουν αυτό το χάος σε καθαρό, αναγνώσιμο κείμενο. Σε αυτό το tutorial θα δούμε ακριβώς πώς να **boost image contrast**, **remove image noise**, και **improve OCR accuracy** χρησιμοποιώντας το Aspose OCR σε C#. Στο τέλος θα ξέρετε πώς να **load image OCR**, να εκτελέσετε τη γραμμή εργασιών και τελικά να απαντήσετε στην παλιά ερώτηση «**how to OCR C#**;» χωρίς κόπο.

Θα καλύψουμε όλα όσα χρειάζεστε:

* Ρύθμιση της μηχανής Aspose OCR
* Δημιουργία μιας αλυσίδας φίλτρων (deskew, denoise, contrast boost)
* Φόρτωση μιας εικόνας για OCR
* Εξαγωγή και εκτύπωση του αναγνωρισμένου κειμένου
* Συμβουλές, παγίδες και παραλλαγές που μπορεί να συναντήσετε

Καμία εξωτερική σύνδεση τεκμηρίωσης — μόνο ένα αυτόνομο, εκτελέσιμο παράδειγμα που μπορείτε να επικολλήσετε στο Visual Studio και να δείτε να λειτουργεί.

## Προαπαιτούμενα – Τι Θα Χρειαστείτε Πριν Ξεκινήσετε

| Απαίτηση | Γιατί Είναι Σημαντικό |
|-------------|----------------|
| .NET 6+ (ή .NET Framework 4.6+) | Το Aspose.OCR στοχεύει σε αυτά τα runtime |
| Πακέτο NuGet Aspose.OCR (`Aspose.OCR`) | Παρέχει `OcrEngine` και κλάσεις φίλτρων |
| Δείγμα εικόνας (`noisy_rotated.jpg`) | Επιδεικνύει deskew, denoise και contrast boost |
| Βασικές γνώσεις C# | Για να μπορείτε να τροποποιήσετε τον κώδικα αργότερα |

Αν έχετε ήδη ένα έργο, απλώς προσθέστε το πακέτο NuGet:

```bash
dotnet add package Aspose.OCR
```

Αυτό είναι όλο — χωρίς επιπλέον DLLs, χωρίς εγγενείς εξαρτήσεις.

## Βήμα 1: Αρχικοποίηση της Μηχανής OCR (Η Ενίσχυση της Αντίθεσης Εικόνας Ξεκινά Εδώ)

Η δημιουργία της μηχανής είναι η βάση. Σκεφτείτε το `OcrEngine` ως τον εγκέφαλο που θα διαβάσει αργότερα τους χαρακτήρες αφού καθαρίσουμε την εικόνα.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Filters;

// Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

> **Why?** Η μηχανή κρατά τη διαμόρφωση, τις ρυθμίσεις γλώσσας και την αλυσίδα φίλτρων που θα δημιουργήσουμε στη συνέχεια. Χωρίς αυτήν, τίποτα άλλο δεν λειτουργεί.

## Βήμα 2: Δημιουργία Αλυσίδας Φίλτρων – Deskew, Denoise, **Boost Image Contrast**

Τα φίλτρα εφαρμόζονται με τη σειρά που τα προσθέτετε. Εδώ πρώτα ευθυγραμμίζουμε την εικόνα (deskew), μετά εξαλείφουμε τις σπόρια θορύβου (denoise) και τέλος αυξάνουμε την αντίθεση ώστε οι χαρακτήρες να ξεχωρίζουν.

```csharp
// DeskewFilter – corrects rotation up to 5 degrees
ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 5 });

// DenoiseFilter – reduces noise with moderate strength
ocrEngine.Filters.Add(new DenoiseFilter { Strength = 2 });

// ContrastBoostFilter – enhances contrast for better character detection
ocrEngine.Filters.Add(new ContrastBoostFilter { Level = 1.5f });
```

### Τι Κάνει Κάθε Φίλτρο

* **DeskewFilter**: Οι περιστρεφόμενες σάρωσες είναι συχνές όταν οι χρήστες τραβούν φωτογραφίες με τα τηλέφωνά τους. Ένα μέγιστο γωνία 5° καταγράφει τις περισσότερες τυχαίες κλίσεις.
* **DenoiseFilter**: Σάρωσες από φθηνά κάμερα συχνά περιέχουν κόκκο. Η ισχύς = 2 είναι το ιδανικό σημείο — αρκετό για εξομάλυνση χωρίς να θολώνει τις άκρες.
* **ContrastBoostFilter**: Εδώ είναι που **boost image contrast**. Αυξάνοντας το `Level` σε `1.5f`, το σκοτεινό μελάνι γίνεται πιο σκοτεινό και το φόντο πιο ανοιχτό, κάτι που βελτιώνει δραστικά την **improve OCR accuracy**.

> **Pro tip:** Αν οι πηγαίες εικόνες σας είναι ήδη υψηλής αντίθεσης, μειώστε το `Level` για να αποφύγετε την κοπή.

## Βήμα 3: Φόρτωση της Εικόνας για OCR – **Load Image OCR** Εύκολη

Τώρα φέρνουμε πραγματικά την εικόνα στη μνήμη. Η χρήση του `System.Drawing.Image.FromFile` λειτουργεί για τις περισσότερες κοινές μορφές (JPG, PNG, BMP).

```csharp
// Replace with the path to your own image
string imagePath = @"YOUR_DIRECTORY/noisy_rotated.jpg";

using (var inputImage = Image.FromFile(imagePath))
{
    // The rest of the steps go inside this block
}
```

> **Γιατί να χρησιμοποιήσετε ένα μπλοκ `using`;** Εξασφαλίζει ότι ο χειριστής της εικόνας απελευθερώνεται άμεσα, αποτρέποντας προβλήματα κλειδώματος αρχείων στα Windows.

## Βήμα 4: Εκτέλεση Αναγνώρισης – Η Καρδιά του **How to OCR C#**

Μέσα στο μπλοκ `using` καλούμε το `Recognize`. Η μηχανή εκτελεί αυτόματα την αλυσίδα φίλτρων που διαμορφώσαμε προηγουμένως.

```csharp
    // Recognize text from the image
    var ocrResult = ocrEngine.Recognize(inputImage);

    // Output the recognized text to the console
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(ocrResult.Text);
```

### Αναμενόμενη Έξοδος

Αν η πηγή εικόνας περιέχει τη φράση «Hello World», η κονσόλα θα εκτυπώσει κάτι όπως:

```
=== OCR Output ===
Hello World
```

Αν το κείμενο φαίνεται ακατάληπτο, ελέγξτε ξανά τις ρυθμίσεις των φίλτρων — ίσως η εικόνα χρειάζεται πιο ισχυρό denoise ή υψηλότερο επίπεδο αντίθεσης.

## Βήμα 5: Πλήρες, Εκτελέσιμο Παράδειγμα (Όλα τα Βήματα Συνδυασμένα)

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε μια νέα εφαρμογή κονσόλας (`dotnet new console`). Βεβαιωθείτε ότι η διαδρομή της εικόνας δείχνει σε ένα πραγματικό αρχείο στον δίσκο σας.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Build a filter pipeline to improve image quality
        //   • DeskewFilter – corrects rotation up to 5 degrees
        //   • DenoiseFilter – reduces noise with moderate strength
        //   • ContrastBoostFilter – enhances contrast for better character detection
        ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 5 });
        ocrEngine.Filters.Add(new DenoiseFilter { Strength = 2 });
        ocrEngine.Filters.Add(new ContrastBoostFilter { Level = 1.5f });

        // Step 3: Load the image that needs OCR processing
        string imagePath = @"YOUR_DIRECTORY/noisy_rotated.jpg";
        using (var inputImage = Image.FromFile(imagePath))
        {
            // Step 4: Recognize text from the image
            var ocrResult = ocrEngine.Recognize(inputImage);

            // Step 5: Output the recognized text to the console
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

Εκτελέστε `dotnet run` και δείτε τη μαγεία. Μόλις **boosted image contrast**, **removed image noise**, και **improved OCR accuracy** — όλα σε λίγες γραμμές C#.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### 1. Τι γίνεται αν η εικόνα μου είναι σε μορφή PNG;

`Image.FromFile` υποστηρίζει PNG από την αρχή. Δεν απαιτείται αλλαγή κώδικα — απλώς δείξτε το `imagePath` στο αρχείο PNG.

### 2. Το κείμενό μου είναι ακόμα θολό μετά τα φίλτρα. Κάποιες ιδέες;

* Αυξήστε το `ContrastBoostFilter.Level` σε `2.0f` ή περισσότερο.
* Αυξήστε το `DenoiseFilter.Strength` σε `3` για πολύ θορυβώδεις σάρωσες.
* Αν η περιστροφή υπερβαίνει τα 5°, αυξήστε το `DeskewFilter.MaxAngle` σε `10`.

### 3. Μπορώ να επεξεργαστώ πολλές εικόνες σε παρτίδα;

Απόλυτα. Τυλίξτε τη λογική αναγνώρισης μέσα σε έναν βρόχο:

```csharp
foreach (var file in Directory.GetFiles(@"C:\Images", "*.jpg"))
{
    using var img = Image.FromFile(file);
    var result = ocrEngine.Recognize(img);
    Console.WriteLine($"{Path.GetFileName(file)}: {result.Text}");
}
```

### 4. Υποστηρίζει το Aspose OCR γλώσσες εκτός της Αγγλικής;

Ναι. Ορίστε τη γλώσσα πριν από την αναγνώριση:

```csharp
ocrEngine.Language = Language.Spanish; // or Language.French, etc.
```

Βεβαιωθείτε ότι το κατάλληλο πακέτο γλώσσας είναι εγκατεστημένο (συνήθως περιλαμβάνεται με το πακέτο NuGet).

## Συμβουλές Απόδοσης – Πώς να Αποκομίσετε το Μέγιστο από το OCR

* **Επαναχρησιμοποίηση του `OcrEngine`**: Η δημιουργία του μία φορά και η επαναχρησιμοποίησή του για πολλές εικόνες μειώνει το κόστος.
* **Αλλαγή μεγέθους μεγάλων εικόνων**: Αν η πηγή σας είναι > 2000 px πλάτος, μειώστε την σε ~ 1200 px πριν τη δώσετε στη μηχανή. Οι μικρότερες εικόνες επεξεργάζονται πιο γρήγορα και συχνά δίνουν την ίδια ακρίβεια μετά την ενίσχυση της αντίθεσης.
* **Παράλληλη εκτέλεση με ασφάλεια**: Το `OcrEngine` δεν είναι thread‑safe, αλλά μπορείτε να δημιουργήσετε μια δεξαμενή μηχανών και να αναθέσετε καθεμία σε ξεχωριστό νήμα.

## Συμπέρασμα – Τι Καταφέραμε

Ξεκινήσαμε με ένα θολό, περιστρεφόμενο JPEG και, μέσω μιας σύντομης αλυσίδας φίλτρων, **boosted image contrast**, **removed image noise**, και **improved OCR accuracy**. Ο τελικός κώδικας δείχνει έναν καθαρό τρόπο να **load image OCR**, να εκτελέσετε την αναγνώριση και να εκτυπώσετε το αποτέλεσμα — απαντώντας στην κλασική ερώτηση «**how to OCR C#**» μια για πάντα.

Επόμενα βήματα; Δοκιμάστε να αντικαταστήσετε το `ContrastBoostFilter` με το `GammaCorrectionFilter` αν χρειάζεστε πιο ακριβή έλεγχο, ή πειραματιστείτε με **γλωσσικά‑συγκεκριμένα λεξικά** για να αυξήσετε ακόμη περισσότερο την ακρίβεια. Μπορείτε επίσης να εξετάσετε την αποθήκευση της καθαρισμένης εικόνας στο δίσκο (`inputImage.Save("cleaned.png")`) πριν την αναγνώριση — χρήσιμο για εντοπισμό σφαλμάτων.

Αισθανθείτε ελεύθεροι να προσαρμόσετε την αλυσίδα στα δικά σας δεδομένα, και καλή προγραμματιστική! Αν αντιμετωπίσετε οποιεσδήποτε ιδιομορφίες, αφήστε ένα σχόλιο παρακάτω — ας τα λύσουμε μαζί.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}