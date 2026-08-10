---
category: general
date: 2026-02-16
description: Μάθετε πώς να εκτελείτε OCR σε C# χρησιμοποιώντας το Aspose.OCR – αναγνωρίστε
  κείμενο από φωτογραφία, διαβάστε κείμενο από σάρωση και εξάγετε κείμενο από απόδειξη
  με υψηλή ακρίβεια.
draft: false
keywords:
- how to perform OCR
- recognize text from photo
- read text from scan
- extract text from receipt
- improve OCR accuracy
language: el
og_description: Μάθετε πώς να εκτελείτε OCR σε C# με το Aspose.OCR. Αυτός ο οδηγός
  σας δείχνει πώς να αναγνωρίζετε κείμενο από φωτογραφία, να διαβάζετε κείμενο από
  σάρωση και να εξάγετε κείμενο από απόδειξη.
og_title: Πώς να εκτελέσετε OCR σε C# – Πλήρης οδηγός Aspose
tags:
- C#
- Aspose.OCR
- Image Processing
title: Πώς να εκτελέσετε OCR σε C# – Πλήρης οδηγός Aspose
url: /el/net/text-recognition/how-to-perform-ocr-in-c-complete-aspose-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εκτελέσετε OCR σε C# – Πλήρης Οδηγός Aspose

Έχετε αναρωτηθεί ποτέ **πώς να εκτελέσετε OCR** σε μια θολή απόδειξη ή σε μια τυχαία φωτογραφία που τραβήξατε με το τηλέφωνό σας; Δεν είστε οι μόνοι. Σε πολλές πραγματικές εφαρμογές χρειάζεται να **αναγνωρίσουμε κείμενο από φωτογραφία**, **διαβάσουμε κείμενο από σαρωμένα** έγγραφα ή **εξάγουμε κείμενο από εικόνες αποδείξεων** χωρίς να στέλνουμε δεδομένα σε υπηρεσία cloud.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα αυτόνομο παράδειγμα που δείχνει **πώς να εκτελέσετε OCR** με το Aspose.OCR, και θα προσθέσουμε συμβουλές για **βελτίωση της ακρίβειας του OCR** καθ' όλη τη διάρκεια. Στο τέλος θα έχετε ένα έτοιμο πρόγραμμα C# console που εξάγει απλό κείμενο από οποιαδήποτε εικόνα του δείξετε.

> **Τι θα χρειαστείτε**  
> * .NET 6 SDK (ή οποιαδήποτε πρόσφατη έκδοση .NET)  
> * Πακέτο NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
> * Ένα δείγμα εικόνας – π.χ. μια φωτογραφία απόδειξης με όνομα `photo_receipt.jpg`  

Αν αυτά σας είναι γνωστά, τέλεια – ας βουτήξουμε.

![how to perform OCR example](image.png){alt="πώς να εκτελέσετε OCR"}

## Πώς να Εκτελέσετε OCR με Aspose.OCR σε C#

Το πρώτο βήμα είναι η ρύθμιση της μηχανής OCR και η φόρτωση ενός μοντέλου αγγλικής γλώσσας. Αυτό είναι ο πυρήνας του **πώς να εκτελέσετε OCR** με το Aspose· χωρίς μοντέλο γλώσσας η μηχανή δεν θα ξέρει ποιοι χαρακτήρες να ψάξει.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Load the English language model – change this if you need another language
ocrEngine.LoadLanguage(LanguageModel.English);
```

*Γιατί είναι σημαντικό*: Η φόρτωση του σωστού μοντέλου γλώσσας επηρεάζει άμεσα την ταχύτητα και την ακρίβεια της αναγνώρισης. Τα αγγλικά είναι η πιο κοινή περίπτωση, αλλά το Aspose παρέχει δεκάδες άλλα μοντέλα αν χρειαστεί ποτέ να **διαβάσετε κείμενο από σαρωμένα** έγγραφα στα γαλλικά, γερμανικά κ.λπ.

## Αναγνώριση Κειμένου από Φωτογραφία

Οι φωτογραφίες που τραβιούνται με το τηλέφωνο συχνά υποφέρουν από περιστροφή, θόρυβο ή χαμηλή αντίθεση. Πριν ζητήσουμε από τη μηχανή να **αναγνωρίσει κείμενο από φωτογραφία**, ρυθμίζουμε κάποιες επιλογές προεπεξεργασίας που καθαρίζουν την εικόνα.

```csharp
// Configure preprocessing to boost OCR results
PreprocessingOptions preprocessingOptions = new PreprocessingOptions
{
    Deskew = true,                     // Auto‑correct rotation (helps with tilted receipts)
    Denoise = DenoiseLevel.Medium,    // Reduce graininess
    Binarize = BinarizeMethod.Otsu,   // Convert to black‑and‑white for sharper edges
    ContrastEnhancement = true        // Boost contrast for faint characters
};

// Apply the preprocessing configuration
ocrEngine.Preprocessing = preprocessingOptions;
```

*Συμβουλή*: Αν παρατηρήσετε ελλιπή χαρακτήρες, δοκιμάστε να αλλάξετε το `DenoiseLevel` σε `High` ή να χρησιμοποιήσετε το `BinarizeMethod.Sauvola`. Αυτές οι μικρές ρυθμίσεις είναι μέρος των στρατηγικών **βελτίωσης της ακρίβειας του OCR**.

## Διαβάστε Κείμενο από Σάρωση

Τώρα που η μηχανή είναι έτοιμη, φορτώνουμε την εικόνα. Είτε είναι μια σαρωμένη σελίδα PDF αποθηκευμένη ως JPEG είτε μια φωτογραφία μιας εκτυπωμένης φόρμας, ο κώδικας παραμένει ίδιος.

```csharp
// Load the image you want to process
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/photo_receipt.jpg");
```

Αν έχετε ένα `Stream` αντί για διαδρομή αρχείου, απλώς αντικαταστήστε το `FromFile` με `FromStream`. Αυτή η ευελιξία είναι χρήσιμη όταν **διαβάζετε κείμενο από σαρωμένες** εικόνες που προέρχονται από ανέβασμα στο web.

## Εξαγωγή Κειμένου από Απόδειξη

Με όλα έτοιμα, η πραγματική κλήση OCR είναι μια μόνο γραμμή. Η μέθοδος επιστρέφει το εξαγόμενο κείμενο ως συμβολοσειρά, το οποίο μπορούμε να εμφανίσουμε, αποθηκεύσουμε ή να το περάσουμε σε άλλο σύστημα.

```csharp
// Perform OCR and capture the result
string extractedText = ocrEngine.Recognize();

// Output the text to the console
Console.WriteLine("=== OCR RESULT ===");
Console.WriteLine(extractedText);
```

**Αναμενόμενο αποτέλεσμα** (παράδειγμα για απλή απόδειξη):

```
=== OCR RESULT ===
Store: CoffeeShop
Date: 2024-02-15
Item      Qty   Price
Latte      2    4.50
Bagel      1    2.75
Total            7.25
```

Αν το αποτέλεσμα φαίνεται παραμορφωμένο, επανεξετάστε το τμήμα προεπεξεργασίας – αυτό είναι το πιο συχνό σημείο για **βελτίωση της ακρίβειας του OCR**.

## Βελτίωση της Ακρίβειας του OCR – Προχωρημένες Ρυθμίσεις

Ενώ οι προεπιλεγμένες ρυθμίσεις λειτουργούν σε πολλές περιπτώσεις, οι παραγωγικές γραμμές συχνά απαιτούν επιπλέον φροντίδα:

| Κατάσταση | Προσαρμογή | Αιτιολογία |
|-----------|------------|------------|
| Πολύ σκούρο φόντο | `ContrastEnhancement = true` + `Binarize = BinarizeMethod.Sauvola` | Αυξάνει το διαχωρισμό μεταξύ κειμένου και φόντου |
| Χειρόγραφα σημειώματα | `ocrEngine.LoadLanguage(LanguageModel.EnglishHandwritten)` | Εξειδικευμένο μοντέλο για καμπυλωτές γραμμές |
| Πολυ‑σελίδες σάρωσης | Βρόχος πάνω σε κάθε εικόνα σελίδας και κλήση `Recognize()` ανά επανάληψη | Διατηρεί χαμηλό αποτύπωμα μνήμης |
| Μεγάλες εικόνες (> 2000 px) | Αλλαγή μεγέθους πριν την παροχή στο OCR (`Image.Resize(width, height)`) | Ταχύτερη επεξεργασία, λιγότερη χρήση μνήμης |

Θυμηθείτε, **πώς να εκτελέσετε OCR** δεν είναι μια συνταγή «ένα μέγεθος για όλους» – θα πειραματιστείτε με αυτές τις ρυθμίσεις μέχρι το αποτέλεσμα να ικανοποιεί τα πρότυπά σας.

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω είναι το πλήρες, έτοιμο για αντιγραφή‑και‑επικόλληση πρόγραμμα. Περιλαμβάνει όλα τα τμήματα που συζητήσαμε, καθώς και έναν μικρό βοηθό που ελέγχει αν το αρχείο υπάρχει πριν προσπαθήσει να το διαβάσει.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine and load language
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.LoadLanguage(LanguageModel.English);

        // 2️⃣ Set up preprocessing to improve OCR accuracy
        ocrEngine.Preprocessing = new PreprocessingOptions
        {
            Deskew = true,
            Denoise = DenoiseLevel.Medium,
            Binarize = BinarizeMethod.Otsu,
            ContrastEnhancement = true
        };

        // 3️⃣ Path to the image – change this to your own file
        string imagePath = Path.Combine("YOUR_DIRECTORY", "photo_receipt.jpg");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"⚠️  Image not found: {imagePath}");
            return;
        }

        // 4️⃣ Load the image (recognize text from photo / read text from scan)
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // 5️⃣ Perform OCR – this is the core of how to perform OCR
        string extractedText = ocrEngine.Recognize();

        // 6️⃣ Show the result – you can now extract text from receipt, invoice, etc.
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(extractedText);
    }
}
```

Τρέξτε το πρόγραμμα με `dotnet run`. Αν όλα είναι σωστά ρυθμισμένα, θα δείτε το εξαγόμενο κείμενο να εμφανίζεται στην κονσόλα.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

**Ε: Τι γίνεται αν η εικόνα είναι PDF;**  
Α: Μετατρέψτε πρώτα κάθε σελίδα PDF σε εικόνα (π.χ., χρησιμοποιώντας `Aspose.Pdf` ή `PdfSharp`) και στη συνέχεια δώστε το παραγόμενο bitmap στο `ocrEngine.Image`.

**Ε: Μπορώ να επεξεργάζομαι εικόνες παράλληλα;**  
Α: Ναι, αλλά δημιουργήστε ξεχωριστό `OcrEngine` ανά νήμα. Η μηχανή δεν είναι thread‑safe, οπότε η κοινή χρήση μιας μόνο παρουσίας μπορεί να προκαλέσει συνθήκες αγώνα.

**Ε: Λειτουργεί αυτό σε Linux;**  
Α: Απόλυτα. Το Aspose.OCR είναι cross‑platform· απλώς βεβαιωθείτε ότι οι εγγενείς εξαρτήσεις είναι εγκατεστημένες (`libgdiplus` για .NET Core σε Linux).

**Ε: Πώς διαχειρίζομαι πολυγλωσσικές αποδείξεις;**  
Α: Φορτώστε πολλαπλά μοντέλα γλώσσας πριν την αναγνώριση:  
```csharp
ocrEngine.LoadLanguage(LanguageModel.English);
ocrEngine.LoadLanguage(LanguageModel.Spanish);
```  
Η μηχανή θα δοκιμάσει κάθε μοντέλο με τη σειρά.

## Συμπέρασμα

Τώρα έχετε μια στέρεη, ολοκληρωμένη λύση για **πώς να εκτελέσετε OCR** σε C# με το Aspose.OCR. Το tutorial κάλυψε τα πάντα, από την αρχικοποίηση της μηχανής, **αναγνώριση κειμένου από φωτογραφία**, **διάβασμα κειμένου από σάρωση**, μέχρι **εξαγωγή κειμένου από απόδειξη**, και σας έδωσε πρακτικούς τρόπους **βελτίωσης της ακρίβειας του OCR**.  

Τι θα κάνετε στη συνέχεια; Δοκιμάστε να αντικαταστήσετε το αγγλικό μοντέλο με ένα χειρόγραφου, πειραματιστείτε με διαφορετικές τιμές `BinarizeMethod`, ή ενσωματώστε την κλήση OCR σε ένα API ASP.NET που επεξεργάζεται ανέβασμα αρχείων σε πραγματικό χρόνο. Οι δυνατότητες είναι τόσο ευρείες όσο οι εικόνες που θα τροφοδοτήσετε.

Έχετε περισσότερες ερωτήσεις για OCR, προεπεξεργασία εικόνας ή βιβλιοθήκες Aspose; Αφήστε ένα σχόλιο ή εξερευνήστε την επίσημη τεκμηρίωση Aspose.OCR για πιο βαθιές πληροφορίες. Καλό κώδικα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}