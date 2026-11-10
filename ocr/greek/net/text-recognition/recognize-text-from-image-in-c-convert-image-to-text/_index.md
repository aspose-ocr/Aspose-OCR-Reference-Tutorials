---
category: general
date: 2026-06-19
description: 'Αναγνώριση κειμένου από εικόνα χρησιμοποιώντας Aspose OCR σε C#: βήμα‑βήμα
  οδηγός για μετατροπή εικόνας σε κείμενο και εξαγωγή κειμένου από αρχεία jpg.'
draft: false
keywords:
- recognize text from image
- extract text from jpg
- convert image to text
- perform ocr on image
- set ocr language
language: el
og_description: αναγνωρίστε κείμενο από εικόνα με Aspose OCR σε C#. Μάθετε πώς να
  ορίσετε τη γλώσσα OCR, να εξάγετε κείμενο από jpg και να μετατρέψετε την εικόνα
  σε κείμενο σε λίγα λεπτά.
og_title: Αναγνώριση κειμένου από εικόνα σε C# – Μετατροπή εικόνας σε κείμενο
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: 'recognize text from image using Aspose OCR in C#: step‑by‑step guide
    to convert image to text and extract text from jpg files.'
  headline: recognize text from image in C# – Convert Image to Text
  type: TechArticle
- description: 'recognize text from image using Aspose OCR in C#: step‑by‑step guide
    to convert image to text and extract text from jpg files.'
  name: recognize text from image in C# – Convert Image to Text
  steps:
  - name: 5.1 Low‑Resolution Images
    text: OCR accuracy drops sharply below 100 dpi. If you notice garbled output,
      try pre‑processing the image (increase contrast, resize, or apply a sharpening
      filter) before feeding it to Aspose OCR.
  - name: 5.2 Multi‑Page Documents
    text: "Even though Community mode caps at 100 pages, you can still process PDFs
      or multi‑page TIFFs. The engine will return concatenated text, preserving page
      breaks with `\f`."
  - name: 5.3 Non‑English Languages
    text: 'Switch the `Language` enum to another supported value:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: Αναγνώριση κειμένου από εικόνα σε C# – Μετατροπή εικόνας σε κείμενο
url: /el/net/text-recognition/recognize-text-from-image-in-c-convert-image-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση κειμένου από εικόνα σε C# – Μετατροπή Εικόνας σε Κείμενο

Έχετε χρειαστεί ποτέ να **αναγνωρίσετε κείμενο από εικόνα** αλλά δεν ήξερατε ποια βιβλιοθήκη θα το έκανε χωρίς υψηλό κόστος άδειας; Δεν είστε μόνοι. Σε αυτό το tutorial θα περάσουμε από τη χρήση του Aspose OCR σε δωρεάν Community mode για **μετατροπή εικόνας σε κείμενο**, εξαγωγή κειμένου από αρχεία jpg και ακόμη **ρύθμιση γλώσσας OCR** για πολυγλωσσικά σενάρια.

Θα καλύψουμε τα πάντα, από την εγκατάσταση του πακέτου NuGet μέχρι την αντιμετώπιση ειδικών περιπτώσεων όπως πολυ-σελίδες PDF ή εικόνες χαμηλής ανάλυσης. Στο τέλος θα έχετε μια εκτελέσιμη εφαρμογή console που μπορεί να **εκτελέσει OCR σε εικόνες** σε δευτερόλεπτα.

## Τι Θα Χρειαστείτε

- .NET 6 SDK ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Core 3.1+)  
- Visual Studio 2022 ή οποιονδήποτε επεξεργαστή προτιμάτε  
- Ένα αρχείο εικόνας (JPG, PNG, BMP…) που περιέχει αναγνώσιμο κείμενο  
- Πρόσβαση στο Internet για λήψη του πακέτου NuGet `Aspose.OCR`  

Αυτό είναι όλο—χωρίς επιπλέον DLLs, χωρίς εξωτερικές υπηρεσίες, μόνο καθαρό C#.

![παράδειγμα αναγνώρισης κειμένου από εικόνα](https://example.com/ocr-screenshot.png "παράδειγμα αναγνώρισης κειμένου από εικόνα")

*(Το στιγμιότυπο δείχνει την έξοδο της κονσόλας μετά την αναγνώριση ενός δείγματος JPG.)*

## Βήμα 1: Εγκατάσταση Aspose OCR μέσω NuGet

Πρώτα, προσθέστε τη βιβλιοθήκη Aspose OCR στο έργο σας. Ανοίξτε ένα τερματικό στο φάκελο του έργου και εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

Το πακέτο περιλαμβάνει **Community mode** που περιορίζει την επεξεργασία σε 100 σελίδες ανά εκτέλεση, ιδανικό για μικρές δοκιμές. Αν χρειαστείτε υψηλότερα όρια, μπορείτε να αναβαθμίσετε σε πληρωμένη άδεια αργότερα—χωρίς αλλαγές κώδικα.

## Βήμα 2: Διαμόρφωση του Μηχανήματος OCR (Ρύθμιση Γλώσσας OCR)

Πριν μπορέσετε να **εκτελέσετε OCR σε εικόνα**, πρέπει να πείτε στη μηχανή ποια γλώσσα θα περιμένετε. Η προεπιλογή είναι τα Αγγλικά, αλλά μπορείτε να μεταβείτε σε Ισπανικά, Γαλλικά ή ακόμη και Κινέζικα με μια μόνο γραμμή.

```csharp
using Aspose.OCR;
using Aspose.OCR.Configuration;

// Choose the language you need – here we stick with English.
var ocrConfig = new OcrEngineConfig
{
    Language = Language.English,      // set ocr language
    MaxPagesPerRun = 100              // enforced limit in Community mode
};
```

Γιατί είναι σημαντική η γλώσσα; Τα μοντέλα OCR εκπαιδεύονται σε συγκεκριμένα σύνολα χαρακτήρων· η παροχή γαλλικού εγγράφου σε αγγλικό μοντέλο θα χάσει τόνους και συνδέσμους. Η σωστή γλώσσα βελτιώνει δραματικά την ακρίβεια.

## Βήμα 3: Δημιουργία του Μηχανήματος OCR και Αναγνώριση της Εικόνας

Με τη διαμόρφωση έτοιμη, δημιουργήστε το μηχάνημα μέσα σε ένα `using` block ώστε οι πόροι να απελευθερώνονται αυτόματα. Στη συνέχεια καλέστε `RecognizeImage` με τη διαδρομή του JPG (ή οποιασδήποτε υποστηριζόμενης μορφής).

```csharp
// Step 3: Create the OCR engine and recognize the image
using var ocrEngine = new OcrEngine(ocrConfig);

// Replace with the actual path to your image file.
string imagePath = @"YOUR_DIRECTORY/sample.jpg";

// Perform OCR – this will **recognize text from image**.
var ocrResult = ocrEngine.RecognizeImage(imagePath);
```

Μερικά σημεία που πρέπει να σημειώσετε:

- **Ασφάλεια νήματος:** Η παρουσία `OcrEngine` δεν είναι thread‑safe. Αν σκοπεύετε να επεξεργάζεστε πολλές εικόνες ταυτόχρονα, δημιουργήστε ξεχωριστό engine ανά νήμα.  
- **Υποστηριζόμενες μορφές:** Εκτός από JPG, μπορείτε να δώσετε PNG, BMP, TIFF και ακόμη PDF. Η ίδια μέθοδος λειτουργεί, ώστε να μπορείτε να **εξάγετε κείμενο από jpg** ή οποιαδήποτε άλλη raster εικόνα.

## Βήμα 4: Έξοδος του Αναγνωρισμένου Κειμένου (Μετατροπή Εικόνας σε Κείμενο)

Τώρα που η μηχανή OCR ολοκλήρωσε τη δουλειά της, το αποτέλεσμα αποθηκεύεται σε ένα αντικείμενο `OcrResult`. Η ιδιότητα `Text` περιέχει την απλή κειμενική αναπαράσταση όλων όσων η μηχανή μπόρεσε να διαβάσει.

```csharp
// Step 4: Write the recognized text to the console
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

Αν τρέξετε το πρόγραμμα με μια καθαρή λήψη από απόδειξη, θα δείτε κάτι όπως:

```
=== OCR Output ===
Item        Qty   Price
Apple       2     $1.20
Banana      5     $0.75
Total               $5.55
```

Αυτή είναι η ουσία του **μετατροπής εικόνας σε κείμενο**—η εικόνα γίνεται τώρα μια συμβολοσειρά που μπορείτε να αποθηκεύσετε, να αναζητήσετε ή να περάσετε σε άλλο σύστημα.

## Βήμα 5: Διαχείριση Συνηθισμένων Edge Cases

### 5.1 Εικόνες Χαμηλής Ανάλυσης

Η ακρίβεια OCR πέφτει απότομα κάτω από 100 dpi. Αν παρατηρήσετε ακατάστατο κείμενο, δοκιμάστε προεπεξεργασία της εικόνας (αύξηση αντίθεσης, αλλαγή μεγέθους ή εφαρμογή φίλτρου ακονισμού) πριν τη δώσετε στο Aspose OCR.

```csharp
// Example: Resize a low‑dpi image to improve accuracy
using var bitmap = new Bitmap(imagePath);
var highRes = new Bitmap(bitmap, new Size(bitmap.Width * 2, bitmap.Height * 2));
highRes.Save("highres_sample.jpg");
var highResResult = ocrEngine.RecognizeImage("highres_sample.jpg");
```

### 5.2 Πολυ‑σελίδες Έγγραφα

Αν και το Community mode περιορίζει τις 100 σελίδες, μπορείτε ακόμη να επεξεργαστείτε PDF ή πολυ‑σελίδες TIFF. Η μηχανή θα επιστρέψει ενωμένο κείμενο, διατηρώντας τις αλλαγές σελίδας με `\f`.

```csharp
var multiPageResult = ocrEngine.RecognizeImage("multi_page.pdf");
Console.WriteLine(multiPageResult.Text); // contains form‑feed characters between pages
```

### 5.3 Μη‑Αγγλικές Γλώσσες

Αλλάξτε το enum `Language` σε άλλη υποστηριζόμενη τιμή:

```csharp
ocrConfig.Language = Language.French; // now the engine expects French characters
```

Θυμηθείτε να εγκαταστήσετε τα αντίστοιχα language packs αν ξεπεράσετε το προεπιλεγμένο σύνολο· το Aspose τα παρέχει ως ξεχωριστά πακέτα NuGet.

## Βήμα 6: Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας τα παραπάνω, εδώ είναι μια πλήρης, έτοιμη για αντιγραφή και επικόλληση εφαρμογή console που **αναγνωρίζει κείμενο από εικόνα**, **εξάγει κείμενο από jpg** και **ρυθμίζει τη γλώσσα OCR** όπως απαιτείται.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Configuration;

class OcrDemo
{
    static void Main()
    {
        // 1️⃣ Configure OCR – change Language to match your source.
        var ocrConfig = new OcrEngineConfig
        {
            Language = Language.English,   // set ocr language
            MaxPagesPerRun = 100
        };

        // 2️⃣ Create the engine inside a using block.
        using var ocrEngine = new OcrEngine(ocrConfig);

        // 3️⃣ Path to the image you want to process.
        string imagePath = @"YOUR_DIRECTORY/sample.jpg";

        // 4️⃣ Perform OCR – this **recognize text from image**.
        var ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 5️⃣ Output – now you have **convert image to text** results.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Αναμενόμενη έξοδος** (υποθέτοντας ότι η δείγμα εικόνα περιέχει το κείμενο “Hello World!”):

```
=== OCR Output ===
Hello World!
```

Τρέξτε το πρόγραμμα με `dotnet run` και θα δείτε την κονσόλα να εμφανίζει τη εξαγόμενη συμβολοσειρά.

## Pro Tips & Συνηθισμένα Πιθανά Σφάλματα

- **Pro tip:** Τυλίξτε την κλήση OCR σε `try/catch` block για να διαχειριστείτε κατεστραμμένα αρχεία με χάρη.  
- **Προσοχή σε:** Εικόνες με υδατογραφήματα ή έντονο θόρυβο φόντου· συχνά μπερδεύουν τη μηχανή.  
- **Συμβουλή:** Αν χρειάζεται να επεξεργαστείτε μια δέσμη αρχείων, κάντε βρόχο πάνω στις καταχωρήσεις του καταλόγου και επαναχρησιμοποιήστε το ίδιο αντικείμενο `OcrEngine`—απλώς θυμηθείτε να επαναφέρετε τυχόν ρυθμίσεις ανά εικόνα.  
- **Θυμηθείτε:** Το όριο των 100 σελίδων του Community mode ισχύει ανά εκτέλεση, όχι ανά αρχείο. Χωρίστε μεγάλα PDF αν φτάσετε το όριο.

## Συμπέρασμα

Τώρα έχετε ένα στιβαρό, έτοιμο για παραγωγή snippet που **αναγνωρίζει κείμενο από εικόνα** χρησιμοποιώντας το Aspose OCR σε C#. Από την εγκατάσταση του πακέτου NuGet μέχρι τη **ρύθμιση γλώσσας OCR**, τη διαχείριση εικόνων χαμηλής ανάλυσης και τέλος τη **μετατροπή εικόνας σε κείμενο**, καλύφθηκαν όλα τα βήματα. Μη διστάσετε να πειραματιστείτε—αλλάξτε τη γλώσσα, δοκιμάστε PNGs ή συνδέστε την έξοδο με έναν downstream δείκτη αναζήτησης.

Στη συνέχεια, μπορείτε να εξερευνήσετε **εξαγωγή κειμένου από jpg** σε κλίμακα ενσωματώνοντας αυτόν τον κώδικα σε Azure Function, ή να εμβαθύνετε στις προχωρημένες δυνατότητες του Aspose OCR όπως ανάλυση διάταξης και αναγνώριση χειρόγραφου. Οι δυνατότητες είναι ατελείωτες, και η βάση που χτίσατε σήμερα θα κάνει αυτές τις επεκτάσεις απρόσκοπτες.

Καλό coding, και οι εικόνες σας να είναι πάντα αναγνώσιμες!

## Τι Θα Μάθετε Στη Σύντομη Μελλοντική Σας

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}