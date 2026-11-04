---
category: general
date: 2026-01-09
description: c# OCR tutorial που δείχνει πώς να αναγνωρίζετε κείμενο από εικόνα και
  να προεπεξεργάζεστε την εικόνα για OCR χρησιμοποιώντας φίλτρα Aspose.OCR – βήμα‑βήμα
  οδηγός.
draft: false
keywords:
- c# ocr tutorial
- recognize text from image
- preprocess image for ocr
- Aspose OCR
- image preprocessing C#
language: el
og_description: c# OCR tutorial που σας καθοδηγεί στη αναγνώριση κειμένου από εικόνα
  και στην προεπεξεργασία εικόνας για OCR χρησιμοποιώντας φίλτρα Aspose.OCR. Συμπεριλαμβάνεται
  πλήρης κώδικας.
og_title: c# OCR tutorial – Αναγνώριση κειμένου από εικόνα με προεπεξεργασία
tags:
- OCR
- C#
- Image Processing
title: 'c# OCR οδηγός: Αναγνώριση κειμένου από εικόνα με προεπεξεργασία'
url: /el/net/ocr-optimization/c-ocr-tutorial-recognize-text-from-image-with-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Αναγνώριση κειμένου από εικόνα με προεπεξεργασία

Έχετε αναρωτηθεί ποτέ πώς να **αναγνωρίσετε κείμενο από εικόνα** σε μια εφαρμογή C# χωρίς να ξοδεύετε εβδομάδες στην ρύθμιση φίλτρων; Δεν είστε μόνοι. Σε αυτό το **c# ocr tutorial** θα περάσουμε από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που όχι μόνο διαβάζει το κείμενο αλλά επίσης **προετοιμάζει την εικόνα για OCR** ώστε να αυξήσει την ακρίβεια.

Θα χρησιμοποιήσουμε τη βιβλιοθήκη Aspose.OCR επειδή περιλαμβάνει μια βολική αλυσίδα φίλτρων που σας επιτρέπει να προσθέσετε βήματα ευθυγράμμισης, αποθορυβοποίησης και ενίσχυσης αντίθεσης με λίγες μόνο γραμμές κώδικα. Στο τέλος αυτού του οδηγού θα έχετε μια εφαρμογή κονσόλας που μπορεί να πάρει ένα λοξό, θορυβώδες PNG, να το καθαρίσει και να εμφανίσει το εξαγόμενο κείμενο—όλα με σαφείς εξηγήσεις για το γιατί κάθε βήμα είναι σημαντικό.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|------------------------|
| .NET 6 SDK (ή νεότερο) | Σύγχρονα χαρακτηριστικά C# και καλύτερη απόδοση |
| Visual Studio 2022 (ή VS Code) | Βολικό debugging και IntelliSense |
| Πακέτο NuGet **Aspose.OCR** | Παρέχει το `OcrEngine` και τις κλάσεις φίλτρων |
| Μια εικόνα εισόδου (π.χ., `skewed‑noisy.png`) | Δείχνει την ανάγκη προεπεξεργασίας |

Αν κάποιο από αυτά λείπει, εγκαταστήστε το πρώτα. Το βήμα NuGet καλύπτεται στην επόμενη ενότητα.

## Βήμα 1: Εγκατάσταση Aspose.OCR μέσω NuGet

Ανοίξτε το τερματικό σας (ή το Package Manager Console) και εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

> **Συμβουλή:** Χρησιμοποιήστε τη σημαία `--version` για να κλειδώσετε σε μια συγκεκριμένη έκδοση εάν χρειάζεστε αναπαραγώγιμα builds.

Το πακέτο περιλαμβάνει όλα τα φίλτρα που θα χρειαστούμε, οπότε δεν απαιτούνται επιπλέον DLLs.

## Βήμα 2: Αρχικοποίηση του OCR Engine – η καρδιά του c# ocr tutorial

Η δημιουργία του engine είναι απλή, αλλά αξίζει να κατανοήσετε τι συμβαίνει στο παρασκήνιο. Το `OcrEngine` διατηρεί μια αλυσίδα **φίλτρων** που επεξεργάζονται το bitmap πριν τρέξει ο αλγόριθμος αναγνώρισης.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Initialize the OCR engine – this is the core object for the entire tutorial
var ocrEngine = new OcrEngine();
```

> **Γιατί να αρχικοποιήσετε πρώτα;** Το engine αποθηκεύει εσωτερικούς πόρους (όπως μοντέλα γλώσσας). Η επαναχρησιμοποίηση μιας μόνο παρουσίασης σε πολλές εικόνες εξοικονομεί μνήμη και επιταχύνει τις επόμενες αναγνώσεις.

## Βήμα 3: Προεπεξεργασία εικόνας για OCR – προσθήκη ευθυγράμμισης, αποθορυβοποίησης και ενίσχυσης αντίθεσης

Οι περισσότερες πραγματικές σαρώσεις δεν είναι τέλειες· είναι λοξές, σπιρτόζωτες ή πολύ σκοτεινές. Γι' αυτό το **preprocess image for OCR** είναι ένα κρίσιμο βήμα. Η Aspose παρέχει τρία φίλτρα που συνεργάζονται άψογα:

| Φίλτρο | Τι κάνει | Τυπική περίπτωση χρήσης |
|--------|----------|--------------------------|
| `DeskewFilter` | Περιστρέφει την εικόνα για να διορθώσει την κλίση | Σαρωμένα έγγραφα από σαρωτή |
| `DenoiseFilter` | Αφαιρεί απομονωμένα pixel (θόρυβος “αλάτι‑και‑πιπέρι”) | Φωτογραφίες χαμηλού φωτισμού |
| `ContrastBoostFilter` | Αυξάνει την αντίθεση για να ενισχύσει τις άκρες του κειμένου | Ασθενείς εκτυπώσεις ή λήψεις χαμηλής ανάλυσης |

Παρακάτω είναι ο κώδικας που προσθέτει κάθε φίλτρο στην αλυσίδα του engine:

```csharp
// 1️⃣ Deskew – automatically rotates the image to the proper orientation
ocrEngine.Filters.Add(new DeskewFilter());

// 2️⃣ Denoise – cleans up speckles that can confuse the OCR engine
ocrEngine.Filters.Add(new DenoiseFilter());

// 3️⃣ Contrast Boost – amplifies the difference between foreground text and background
ocrEngine.Filters.Add(new ContrastBoostFilter { Level = 1.5 });
```

> **Πώς λειτουργεί:** Όταν καλέσετε το `RecognizeImage` αργότερα, το engine θα εκτελέσει διαδοχικά αυτά τα τρία φίλτρα πριν περάσει το καθαρισμένο bitmap στον πυρήνα αναγνώρισης.

### Οπτική εικονογράφηση (προαιρετικό)

Αν ενσωματώσετε μια εικόνα, βεβαιωθείτε ότι το alt κείμενο περιέχει τη βασική λέξη-κλειδί:

```markdown
![c# ocr tutorial preprocessing example](/images/ocr-preprocess.png)
```

## Βήμα 4: Αναγνώριση κειμένου από εικόνα – η στιγμή της αλήθειας

Τώρα που η εικόνα έχει προεπεξεργαστεί, μπορούμε τελικά να εξάγουμε τους χαρακτήρες. Η μέθοδος επιστρέφει μια απλή συμβολοσειρά, την οποία μπορείτε να καταγράψετε, αποθηκεύσετε ή να τη δώσετε σε άλλο σύστημα.

```csharp
// Replace the path with the actual location of your test image
string imagePath = @"YOUR_DIRECTORY/skewed-noisy.png";

// Perform OCR – this call applies all the filters we added earlier
string recognizedText = ocrEngine.RecognizeImage(imagePath);
```

### Αναμενόμενη έξοδος

Η εκτέλεση του δείγματος σε μια τυπική σάρωση τιμολογίου δίνει κάτι σαν:

```
Invoice #12345
Date: 2025‑12‑31
Total: $1,234.56
Thank you for your business!
```

Αν η έξοδος φαίνεται ακατάληπτη, ελέγξτε ξανά την ποιότητα της εικόνας και σκεφτείτε να ρυθμίσετε το `ContrastBoostFilter.Level` (τιμές > 2.0 μπορεί να είναι πολύ επιθετικές).

## Βήμα 5: Εξαγωγή του αποτελέσματος και προαιρετική μετα-επεξεργασία

Μια εφαρμογή κονσόλας μπορεί απλώς να γράψει τη συμβολοσειρά, αλλά πολλά έργα χρειάζονται επιπλέον επεξεργασία—όπως αφαίρεση κενών, διαγραφή αλλαγών γραμμής ή αποθήκευση του κειμένου σε βάση δεδομένων.

```csharp
// Basic console output
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);

// Example of lightweight post‑processing
string cleaned = recognizedText
    .Replace("\r", "")
    .Replace("\n", " ")
    .Trim();

Console.WriteLine("\n=== Cleaned Text ===");
Console.WriteLine(cleaned);
```

### Γιατί μετα-επεξεργασία;

Ακόμη και με καλή προεπεξεργασία, το OCR συχνά εισάγει ανεπιθύμητες αλλαγές γραμμής ή αόρατους χαρακτήρες. Μια γρήγορη αλυσίδα `Replace` μπορεί να κάνει τα δεδομένα πολύ πιο χρήσιμα στο επόμενο στάδιο.

## Βήμα 6: Πλήρες λειτουργικό παράδειγμα – έτοιμο για αντιγραφή‑επικόλληση

Παρακάτω είναι το **πλήρες** πρόγραμμα που μπορείτε να μεταγλωττίσετε και να εκτελέσετε αμέσως. Περιλαμβάνει όλες τις δηλώσεις `using`, τη ρύθμιση φίλτρων, την κλήση OCR και τη διαχείριση εξόδου.

```csharp
// ---------------------------------------------------------------
// Complete c# ocr tutorial – Recognize Text from Image
// ---------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Add preprocessing filters
        ocrEngine.Filters.Add(new DeskewFilter());                     // Fix rotation
        ocrEngine.Filters.Add(new DenoiseFilter());                    // Remove speckles
        ocrEngine.Filters.Add(new ContrastBoostFilter { Level = 1.5 }); // Boost contrast

        // 3️⃣ Path to the image you want to process
        string imagePath = @"YOUR_DIRECTORY/skewed-noisy.png";

        // 4️⃣ Perform OCR – this also runs the filters we added
        string recognizedText = ocrEngine.RecognizeImage(imagePath);

        // 5️⃣ Show raw OCR result
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);

        // 6️⃣ Optional: simple cleanup for downstream use
        string cleaned = recognizedText
            .Replace("\r", "")
            .Replace("\n", " ")
            .Trim();

        Console.WriteLine("\n=== Cleaned Text ===");
        Console.WriteLine(cleaned);
    }
}
```

**Πώς να το εκτελέσετε**

1. Αποθηκεύστε το αρχείο ως `Program.cs` μέσα σε ένα νέο έργο κονσόλας (`dotnet new console`).
2. Αντικαταστήστε το `YOUR_DIRECTORY/skewed-noisy.png` με την πραγματική διαδρομή προς την εικόνα δοκιμής σας.
3. Εκτελέστε `dotnet run`. Θα πρέπει να δείτε την έξοδο OCR να εμφανίζεται στην κονσόλα.

## Συνηθισμένα προβλήματα & Συμβουλές (αναγνώριση κειμένου από εικόνα αξιόπιστα)

| Πρόβλημα | Τι να ελέγξετε | Διόρθωση |
|----------|----------------|----------|
| **Ακατάληπτοι χαρακτήρες** | Η εικόνα είναι πολύ σκοτεινή ή χαμηλής ανάλυσης | Αυξήστε το `ContrastBoostFilter.Level` ή χρησιμοποιήστε πηγή υψηλότερης ανάλυσης |
| **Απουσία γραμμών** | Το Deskew δεν διόρθωσε πλήρως τη γωνία | Περιστρέψτε χειροκίνητα την εικόνα πρώτα ή προσαρμόστε την ανοχή του `DeskewFilter` |
| **Αργή απόδοση** | Επεξεργασία πολλών μεγάλων εικόνων σε βρόχο | Επαναχρησιμοποιήστε την ίδια παρουσίαση `OcrEngine` και καλέστε `ocrEngine.Clear()` μετά από κάθε εκτέλεση |
| **Μη υποστηριζόμενη γλώσσα** | Το κείμενο δεν είναι Αγγλικά | Ορίστε `ocrEngine.Language = OcrLanguage.French` (ή άλλη υποστηριζόμενη γλώσσα) πριν από την αναγνώριση |

### Ειδική περίπτωση: διαχείριση PDF πολλαπλών σελίδων

Αν χρειάζεται να κάνετε OCR σε PDF, μετατρέψτε κάθε σελίδα σε εικόνα (π.χ., χρησιμοποιώντας το `Aspose.PDF`) και δώστε τις μία‑μία στο ίδιο engine. Η αλυσίδα προεπεξεργασίας παραμένει η ίδια, εξασφαλίζοντας συνεπή αποτελέσματα σε όλες τις σελίδες.

## Συμπέρασμα

Σε αυτό το **c# ocr tutorial** καλύψαμε όλα όσα χρειάζεστε για να **αναγνωρίσετε κείμενο από εικόνα** και να **προετοιμάσετε την εικόνα για OCR** χρησιμοποιώντας τα ενσωματωμένα φίλτρα του Aspose.OCR. Αρχικοποιώντας το engine, προσθέτοντας βήματα ευθυγράμμισης, αποθορυβοποίησης και ενίσχυσης αντίθεσης, και τέλος καλώντας το `RecognizeImage`, λαμβάνετε καθαρή, αξιόπιστη εξαγωγή κειμένου με μόνο λίγες γραμμές κώδικα.

Μη διστάσετε να πειραματιστείτε—αντικαταστήστε ένα φίλτρο, ρυθμίστε το επίπεδο αντίθεσης, ή ενσωματώστε το αποτέλεσμα σε μια μεγαλύτερη ροή δεδομένων. Οι έννοιες εδώ ισχύουν για οποιαδήποτε βιβλιοθήκη OCR: η προεπεξεργασία συχνά αποτελεί τη διαφορά μεταξύ μισής ανάγνωσης ενός τιμολογίου και ενός τέλεια καταγεγραμμένου εγγράφου.

Έχετε περισσότερες ερωτήσεις; Ίσως να θέλετε να μάθετε πώς να διαχειριστείτε χειρόγραφα κείμενα ή μαζική επεξεργασία χιλιάδων αρχείων. Αφήστε ένα σχόλιο και θα εξερευνήσουμε αυτά τα σενάρια μαζί. Καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}