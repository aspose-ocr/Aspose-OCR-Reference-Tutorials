---
category: general
date: 2026-03-20
description: Μάθετε πώς να αφαιρέσετε την κλίση της εικόνας και να εξαλείψετε τον
  θόρυβο της εικόνας με το Aspose OCR. Αυτός ο οδηγός βήμα προς βήμα δείχνει επίσης
  πώς να προεπεξεργαστείτε την εικόνα για OCR και να βελτιώσετε την ακρίβεια του OCR.
draft: false
keywords:
- how to deskew image
- remove image noise
- preprocess image for OCR
- recognize text from image
- improve OCR accuracy
language: el
og_description: Μάθετε πώς να διορθώσετε την κλίση μιας εικόνας και να αφαιρέσετε
  τον θόρυβο με το Aspose OCR. Αυξήστε την ακρίβεια του OCR σας σε λίγα λεπτά.
og_title: Πώς να ευθυγραμμίσετε την εικόνα – Πλήρης οδηγός C# για την προεπεξεργασία
  OCR
tags:
- OCR
- C#
- Image Processing
title: Πώς να διορθώσετε την κλίση της εικόνας – Πλήρης οδηγός C# για την προεπεξεργασία
  OCR
url: /el/net/ocr-optimization/how-to-deskew-image-complete-c-guide-for-ocr-pre-processing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Διορθώσετε την Κλίση μιας Εικόνας – Πλήρης Οδηγός C# για Προεπεξεργασία OCR

Έχετε αναρωτηθεί ποτέ **πώς να διορθώσετε την κλίση μιας εικόνας** που βγήκε από σαρωτή με παράξενη γωνία; Δεν είστε οι μόνοι· πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν προσπαθούν να τροφοδοτήσουν μια φωτογραφία σε μηχανή OCR. Τα καλά νέα είναι ότι με λίγες γραμμές C# και Aspose OCR μπορείτε να ευθυγραμμίσετε, να αφαιρέσετε θόρυβο και να ενισχύσετε την αντίθεση σε μια καθαρή αλυσίδα—χωρίς Photoshop.

Σε αυτό το tutorial θα περάσουμε από όλα όσα χρειάζεστε: από τη φόρτωση μιας κεκλιμένης εικόνας, μέχρι την **αφαίρεση θορύβου εικόνας**, την **προεπεξεργασία εικόνας για OCR**, και τελικά την **αναγνώριση κειμένου από εικόνα** με υψηλό **βαθμό βελτίωσης ακρίβειας OCR**. Στο τέλος θα έχετε μια έτοιμη για εκτέλεση εφαρμογή console που μετατρέπει ένα ακατάστατο σκανάρισμα σε καθαρό, αναζητήσιμο κείμενο.

## Τι Θα Χρειαστείτε

- .NET 6 ή νεότερο (ο κώδικας χρησιμοποιεί σύνταξη `using var`, η οποία υποστηρίζεται από C# 8)
- Ένα πακέτο NuGet Aspose OCR (`Aspose.OCR`) – εγκαταστήστε το με `dotnet add package Aspose.OCR`
- Μια δείγμα εικόνας που είναι τόσο κεκλιμένη όσο και θορυβώδης (π.χ., `skewed_noisy.png`)
- Ένα IDE ή επεξεργαστή της επιλογής σας (Visual Studio, VS Code, Rider… εσείς διαλέγετε)

> **Pro tip:** Αν δεν έχετε αρχείο δείγμα, απλώς περιστρέψτε ένα καθαρό screenshot με μερικές μοίρες και προσθέστε λίγο “αλάτι‑και‑πίπερο” θόρυβο με έναν επεξεργαστή εικόνας. Η αλυσίδα λειτουργεί με τον ίδιο τρόπο.

## Βήμα 1: Πώς να Διορθώσετε την Κλίση μιας Εικόνας με Φίλτρο Deskew

Το πρώτο που κάνουμε είναι η διόρθωση της περιστροφής. Η Aspose παρέχει ένα `DeskewFilter` που μπορεί αυτόματα να ανιχνεύσει γωνίες μέχρι ένα ρυθμιζόμενο `MaxAngle`. Ορίζοντάς το σε **5°** είναι μια ασφαλής προεπιλογή για τα περισσότερα σαρωμένα έγγραφα.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System.Drawing;   // For Image class

// Initialize the OCR engine – English is the most common language
using var ocrEngine = new OcrEngine
{
    Language = Language.English
};

// Build the preprocessing pipeline
var preprocessPipeline = new PreprocessPipeline()
    .Add(new DeskewFilter { MaxAngle = 5 })          // This is where we answer “how to deskew image”
    .Add(new DespeckleFilter { Strength = 2 })      // Next we’ll remove image noise
    .Add(new ContrastFilter { Level = 1.5 });        // Finally we boost contrast for OCR
```

**Γιατί είναι σημαντικό:**  
Αν το κείμενο είναι κεκλιμένο, ο αλγόριθμος OCR μπορεί να ερμηνεύσει λανθασμένα χαρακτήρες—π.χ. το “l” να γίνει “i”. Με το **deskew** πρώτα, δίνετε στη μηχανή έναν ορθό, ευθύ καμβά για επεξεργασία.

## Βήμα 2: Αφαίρεση Θορύβου Εικόνας με Despeckle

Σκάνια από φθηνά τηλέφωνα ή παλιούς σαρωτές συχνά περιέχουν στίγματα που μοιάζουν με τυχαίες κουκκίδες. Αυτά τα στίγματα μπερδεύουν τον αναγνωστικό χαρακτήρων. Το `DespeckleFilter` εξομαλύνει την εικόνα διατηρώντας τα άκρα.

```csharp
// The DespeckleFilter is already part of the pipeline (see Step 1)
// Strength = 2 is a balanced setting; increase for very noisy pics
```

Αν χρειαστεί να **αφαιρέσετε θόρυβο εικόνας** πιο επιθετικά, αυξήστε το `Strength` σε 3 ή 4—αλλά προσέξτε την απώλεια λεπτών γραμμών.

## Βήμα 3: Προεπεξεργασία Εικόνας για OCR – Ενίσχυση Αντίθεσης

Σκάνια χαμηλής αντίθεσης (ανοιχτό γκρι σε λευκό χαρτί) μπορούν να κάνουν το OCR να χάσει αδύνατα γράμματα. Το `ContrastFilter` τεντώνει το τόνικό εύρος, κάνοντας τα σκοτεινά pixel πιο σκοτεινά και τα φωτεινά πιο φωτεινά.

```csharp
// Contrast level of 1.5 is a good starting point.
// You can experiment with values between 1.0 (no change) and 2.0 (strong boost).
```

**Ακραία περίπτωση:** Αν η πηγή σας είναι ήδη υψηλής αντίθεσης, η εφαρμογή αυτού του φίλτρου μπορεί να ξεθωριάσει τις λεπτομέρειες. Σε αυτήν την περίπτωση, ορίστε το `Level` σε `1.0` (απενεργοποιώντας το ουσιαστικά).

## Βήμα 4: Φόρτωση και Καθαρισμός της Πηγαίας Εικόνας

Τώρα φορτώνουμε πραγματικά την εικόνα και την περνάμε από την αλυσίδα που μόλις συναρτήσαμε.

```csharp
// Load the source image – replace the path with your own file location
var sourceImage = Image.FromFile("YOUR_DIRECTORY/skewed_noisy.png");

// Apply the entire preprocessing pipeline
var cleanedImage = preprocessPipeline.Apply(sourceImage);
```

> **Σημείωση:** Η μέθοδος `Apply` επιστρέφει ένα νέο αντικείμενο `Image`; το αρχικό παραμένει αμετάβλητο. Αυτό διευκολύνει τη σύγκριση “πριν” και “μετά” αν θέλετε να εντοπίσετε σφάλματα.

## Βήμα 5: Αναγνώριση Κειμένου από Εικόνα Χρησιμοποιώντας Aspose OCR

Με μια ευθεία, χωρίς θόρυβο, υψηλής αντίθεσης εικόνα στα χέρια, την παραδίδουμε τελικά στη μηχανή OCR.

```csharp
// Perform OCR on the cleaned image
var ocrResult = ocrEngine.Recognize(cleanedImage);

// Output the recognized text to the console
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

**Τι θα δείτε:** Η κονσόλα εκτυπώνει το κειμενικό περιεχόμενο του αρχικού σκαναρίσματος, συνήθως με πολύ λιγότερα λάθη αναγνώρισης σε σύγκριση με το ακατέργαστο αρχείο.

## Βήμα 6: Επαλήθευση και Βελτίωση της Ακρίβειας OCR

Ακόμη και με μια στιβαρή αλυσίδα, κάποιοι χαρακτήρες μπορεί να παραμείνουν λανθασμένοι—ιδιαίτερα αν η αρχική γραμματοσειρά είναι ασυνήθιστη. Εδώ είναι μερικά γρήγορα κόλπα για **βελτίωση της ακρίβειας OCR**:

| Πρόβλημα | Γρήγορη Λύση |
|----------|--------------|
| Λείπουν μικρά σημεία στίξης | Προσθέστε ένα `BinaryThresholdFilter` πριν το βήμα αντίθεσης |
| Μικτή γλώσσα (π.χ., Αγγλικά + Ισπανικά) | Ορίστε `ocrEngine.Language = Language.English \| Language.Spanish;` |
| Πολύ σκοτεινό φόντο | Αντιστρέψτε την εικόνα (`new InvertFilter()`) πριν το deskew |
| Μεγάλα έγγραφα | Επεξεργαστείτε τις σελίδες παράλληλα (`Parallel.ForEach`) για ταχύτητα |

Πειραματιστείτε με τη σειρά των φίλτρων· μερικές φορές η εφαρμογή **αντίθεσης** πριν το **despeckle** δίνει καλύτερα αποτελέσματα σε χαμηλής ποιότητας σκανάρια.

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα νέο project console. Περιλαμβάνει όλα τα τμήματα που συζητήσαμε, καθώς και μερικούς ελέγχους ασφαλείας.

```csharp
// File: Program.cs
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine (English language)
        // -------------------------------------------------
        using var ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // -------------------------------------------------
        // 2️⃣ Build preprocessing pipeline:
        //    Deskew → Despeckle → Contrast Boost
        // -------------------------------------------------
        var preprocessPipeline = new PreprocessPipeline()
            .Add(new DeskewFilter { MaxAngle = 5 })          // how to deskew image
            .Add(new DespeckleFilter { Strength = 2 })      // remove image noise
            .Add(new ContrastFilter { Level = 1.5 });        // preprocess image for OCR

        // -------------------------------------------------
        // 3️⃣ Load the source image (adjust path as needed)
        // -------------------------------------------------
        const string imagePath = "YOUR_DIRECTORY/skewed_noisy.png";
        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"❌ File not found: {imagePath}");
            return;
        }

        var sourceImage = Image.FromFile(imagePath);

        // -------------------------------------------------
        // 4️⃣ Apply the pipeline → cleaned image
        // -------------------------------------------------
        var cleanedImage = preprocessPipeline.Apply(sourceImage);

        // -------------------------------------------------
        // 5️⃣ Recognize text (this is the “recognize text from image” step)
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(cleanedImage);

        // -------------------------------------------------
        // 6️⃣ Output the result
        // -------------------------------------------------
        Console.WriteLine("\n=== OCR Output ===\n");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Αναμενόμενο αποτέλεσμα** (υποθέτοντας ότι η δείγμα εικόνα περιέχει “Hello World!”):

```
=== OCR Output ===

Hello World!
```

Αν δείτε ακατανόητους χαρακτήρες, ελέγξτε ξανά τη σειρά των φίλτρων ή αυξήστε το `DespeckleFilter.Strength`.

## Συμπέρασμα

Καλύψαμε **πώς να διορθώσετε την κλίση μιας εικόνας**, **πώς να αφαιρέσετε θόρυβο εικόνας**, **πώς να προεπεξεργαστείτε εικόνα για OCR**, και τέλος **πώς να αναγνωρίσετε κείμενο από εικόνα** χρησιμοποιώντας Aspose OCR—όλα ενώ διατηρούμε επίκεντρο τη **βελτίωση της ακρίβειας OCR**. Το πλήρες, εκτελέσιμο παράδειγμα δείχνει κάθε βήμα σε συμφραζόμενα, ώστε να το ενσωματώσετε σε οποιοδήποτε έργο .NET και να αρχίσετε αμέσως την εξαγωγή κειμένου.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να επεκτείνετε την αλυσίδα για να χειρίζεται πολυ‑σελίδες PDF, ή πειραματιστείτε με πακέτα γλώσσας για πολυγλωσσικά έγγραφα. Οι ίδιες έννοιες ισχύουν—απλώς αλλάξτε τη σημαία `Language` και ίσως προσθέστε ένα `RotateFilter` για σελίδες που είναι ανάποδα.

Έχετε ερωτήσεις ή μια επίμονη εικόνα που δεν συνεργάζεται; Αφήστε ένα σχόλιο παρακάτω και θα το αντιμετωπίσουμε μαζί. Καλό coding! 

![πώς να διορθώσετε την κλίση μιας εικόνας παράδειγμα](/images/deskew-example.png "Εικονογράφηση του πώς να διορθώσετε την κλίση μιας εικόνας χρησιμοποιώντας Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}