---
category: general
date: 2026-10-18
description: Εκτελέστε OCR σε μια εικόνα σε C# γρήγορα. Μάθετε να εξάγετε κείμενο
  από JPG, να μετατρέπετε την εικόνα σε κείμενο και να διαβάζετε κείμενο από εικόνα
  χρησιμοποιώντας το Aspose.OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- convert image to text
- read text from image
- load image for OCR
language: el
lastmod: 2026-10-18
og_description: Πραγματοποιήστε OCR σε εικόνα με C# και Aspose.OCR. Αυτό το σεμινάριο
  δείχνει πώς να εξάγετε κείμενο από JPG, να μετατρέψετε την εικόνα σε κείμενο και
  να διαβάσετε κείμενο από την εικόνα σε λίγα λεπτά.
og_image_alt: Console output displaying recognized Cyrillic text after performing
  OCR on an image
og_title: Εκτελέστε OCR σε εικόνα με C# – πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-10-18'
  description: Perform OCR on an image in C# quickly. Learn to extract text from JPG,
    convert image to text and read text from image using Aspose.OCR.
  headline: How to perform OCR on an image in C# with Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose.OCR
title: Πώς να εκτελέσετε OCR σε μια εικόνα σε C# με το Aspose.OCR
url: /el/net/text-recognition/how-to-perform-ocr-on-an-image-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εκτελέσετε OCR σε εικόνα σε C# με Aspose.OCR

Αν χρειάζεστε **εκτέλεση OCR σε εικόνα** σε μια εφαρμογή .NET, αυτός ο οδηγός σας παρουσιάζει μια πλήρη, έτοιμη‑για‑εκτέλεση λύση. Θα δείτε πώς να **φορτώσετε εικόνα για OCR**, να αναγνωρίσετε κυριλλικούς χαρακτήρες και να **εξάγετε κείμενο από αρχεία JPG** χωρίς να γράψετε κώδικα χαμηλού επιπέδου επεξεργασίας εικόνας.

Σε αυτό το tutorial θα:

* Εγκαταστήσετε το πακέτο NuGet Aspose.OCR.  
* Φορτώσετε ένα αρχείο εικόνας (JPG, PNG, BMP, κ.λπ.).  
* Εκτελέσετε τη μηχανή OCR για **μετατροπή εικόνας σε κείμενο**.  
* **Διαβάσετε το κείμενο από την εικόνα** στην κονσόλα.  

Τα βήματα λειτουργούν με οποιαδήποτε εικόνα συμβατή με .NET, ώστε να μπορείτε να τα προσαρμόσετε σε PDF, σαρωμένες αποδείξεις ή στιγμιότυπα οθόνης.

## Προαπαιτούμενα

* .NET 6.0 SDK ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.7+).  
* Visual Studio 2022 ή οποιονδήποτε επεξεργαστή C# προτιμάτε.  
* Πρόσβαση στο Internet για την πρώτη εκτέλεση – το Aspose.OCR κατεβάζει αυτόματα το πακέτο γλώσσας κυριλλικών.

> **Pro tip:** Κρατήστε το πακέτο NuGet ενημερωμένο· οι νεότερες εκδόσεις βελτιώνουν την ακρίβεια αναγνώρισης και προσθέτουν γλωσσικά πακέτα.

## Βήμα 1: Εγκατάσταση Aspose.OCR

Ανοίξτε ένα τερματικό στον φάκελο του έργου σας και εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

Το πακέτο περιλαμβάνει την κλάση `OcrEngine` που χρησιμοποιείται για **εκτέλεση OCR σε αρχεία εικόνας**. Μετά την ολοκλήρωση της εντολής, η αναφορά του πακέτου εμφανίζεται στο αρχείο *.csproj* σας.

## Βήμα 2: Δημιουργία σκελετού προγράμματος κονσόλας

Δημιουργήστε ένα νέο έργο κονσόλας αν δεν έχετε ήδη:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Αντικαταστήστε το παραγόμενο *Program.cs* με τον κώδικα που φαίνεται στις επόμενες ενότητες. Ο σκελετός περιλαμβάνει τις απαιτούμενες οδηγίες `using` και μια μέθοδο `Main` που οδηγεί τη διαδικασία OCR.

## Βήμα 3: Φόρτωση εικόνας για OCR

Η πρώτη λειτουργική γραμμή κώδικα **φορτώνει την εικόνα** που θέλετε να αναλύσετε. Το Aspose.OCR δέχεται οποιοδήποτε stream, ώστε να μπορείτε να φορτώσετε ένα αρχείο από δίσκο, URL ή ενσωματωμένο πόρο.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Step 3: Load the image containing Cyrillic text
        // Replace the path with the location of your JPG file.
        string imagePath = @"YOUR_DIRECTORY\cyrillic-sample.jpg";
        using var image = ImageStream.FromFile(imagePath);
```

*Γιατί είναι σημαντικό*: Η χρήση του `ImageStream.FromFile` αφαιρεί την ανάγκη χειρισμού μορφής, διασφαλίζοντας ότι η μηχανή OCR λαμβάνει ένα συνεπές bitmap ανεξαρτήτως του αρχικού τύπου αρχείου. Επιπλέον, το `using` διαχειρίζεται αυτόματα την απελευθέρωση του stream.

## Βήμα 4: Αρχικοποίηση της μηχανής OCR και ορισμός γλώσσας (προαιρετικό)

Από προεπιλογή το Aspose.OCR προσπαθεί να εντοπίσει τη γλώσσα αυτόματα. Για κυριλλικό κείμενο μπορείτε ρητά να ζητήσετε το module `Language.Cyrillic`, το οποίο επιταχύνει τη λήψη του για πρώτη φορά.

```csharp
        // Step 4: Initialize the OCR engine
        var engine = new OcrEngine();

        // Optional: force Cyrillic language to avoid auto‑detection overhead
        engine.Language = Language.Cyrillic;
```

Αν παραλείψετε τον ορισμό της γλώσσας, η μηχανή θα κατεβάσει το απαραίτητο module την πρώτη φορά που θα καλέσετε το `Recognize`. Η λήψη γίνεται μέσω HTTPS και αποθηκεύεται στην τοπική cache για επόμενες εκτελέσεις.

## Βήμα 5: Εκτέλεση OCR και μετατροπή εικόνας σε κείμενο

Τώρα πραγματικά **εκτελείτε OCR σε εικόνα** και λαμβάνετε μια συμβολοσειρά απλού κειμένου. Η μέθοδος `Recognize` κάνει όλη τη βαριά δουλειά: προεπεξεργασία, ανάλυση διάταξης και ταξινόμηση χαρακτήρων.

```csharp
        // Step 5: Perform OCR – convert image to text
        engine.Image = image;
        string recognizedText = engine.Recognize();
```

Το επιστρεφόμενο `recognizedText` περιέχει αλλαγές γραμμής που ταιριάζουν με την αρχική διάταξη, καθιστώντας εύκολη την περαιτέρω επεξεργασία ή αποθήκευση σε βάση δεδομένων.

## Βήμα 6: Εμφάνιση του αποτελέσματος – ανάγνωση κειμένου από την εικόνα

Τέλος, **διαβάζετε το κείμενο από την εικόνα** γράφοντας το αποτέλεσμα στην κονσόλα. Αυτό το βήμα επαληθεύει ότι το OCR πέτυχε και σας δείχνει ακριβώς τι εξήχθη.

```csharp
        // Step 6: Display the recognized text – read text from image
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

Όταν εκτελέσετε το πρόγραμμα (`dotnet run`), θα πρέπει να δείτε έξοδο παρόμοια με:

```
=== OCR Result ===
Пример текста на кириллице
```

> **Σημείωση:** Η ακριβής έξοδος εξαρτάται από την ποιότητα του πηγαίου JPG. Καθαρές, υψηλής ανάλυσης εικόνες δίνουν τα καλύτερα αποτελέσματα.

## Πλήρης, εκτελέσιμος κώδικας

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε στο *Program.cs* και να εκτελέσετε χωρίς τροποποιήσεις (εκτός από τη διαδρομή της εικόνας).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Load the image containing Cyrillic text
        string imagePath = @"YOUR_DIRECTORY\cyrillic-sample.jpg";
        using var image = ImageStream.FromFile(imagePath);

        // Initialize the OCR engine
        var engine = new OcrEngine
        {
            // Force Cyrillic language; optional but speeds up first run
            Language = Language.Cyrillic,
            Image = image
        };

        // Recognize the text – this converts the image to text
        string recognizedText = engine.Recognize();

        // Display the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

Η εκτέλεση του προγράμματος εκτυπώνει τους εξαγόμενους χαρακτήρες στην κονσόλα, αποδεικνύοντας ότι έχετε **εξάγει κείμενο από JPG** και **μετατρέψει εικόνα σε κείμενο**.

## Διαχείριση κοινών παραλλαγών

| Σενάριο | Προσαρμογή |
|----------|------------|
| **Διαφορετική γλώσσα** | Ορίστε `engine.Language = Language.English;` ή άλλο υποστηριζόμενο enum. |
| **PDF πολλαπλών σελίδων** | Μετατρέψτε κάθε σελίδα σε εικόνα (π.χ., χρησιμοποιώντας `Aspose.PDF`) και καλέστε τον βρόχο OCR για κάθε εικόνα. |
| **Μεγάλο batch** | Τυλίξτε την κλήση OCR σε βρόχο `Parallel.ForEach`; επαναχρησιμοποιήστε ένα μόνο αντικείμενο `OcrEngine` για μείωση του φορτίου μνήμης. |
| **Χαμηλής ανάλυσης εικόνα** | Προεπεξεργαστείτε με `engine.Image = ImageProcessing.Filters.GaussianBlur(image, 1.5);` για μείωση θορύβου πριν την αναγνώριση. |

Αυτές οι παραλλαγές σας επιτρέπουν να **εξάγετε κείμενο από JPG** αρχείο οποιασδήποτε γλώσσας, μεγέθους ή ποιότητας.

## Συμβουλές απόδοσης

* **Cache γλωσσικών modules** – η πρώτη λήψη μπορεί να διαρκέσει μερικά δευτερόλεπτα· οι επόμενες εκτελέσεις είναι στιγμιαίες. |
* **Επαναχρησιμοποίηση του αντικειμένου `OcrEngine`** για πολλαπλές εικόνες ώστε να αποφύγετε επαναλαμβανόμενα κόστη αρχικοποίησης. |
* **Περιορισμός μεγέθους εικόνας** – εξαιρετικά μεγάλες φωτογραφίες αυξάνουν τη χρήση μνήμης. Αλλάξτε το μέγεθος σε μέγιστο 2000 px σε πλάτος πριν τις περάσετε στη μηχανή.

## Συμπέρασμα

Τώρα ξέρετε πώς να **εκτελείτε OCR σε αρχεία εικόνας** σε C# χρησιμοποιώντας το Aspose.OCR. Φορτώνοντας μια εικόνα, ρυθμίζοντας τη μηχανή και καλώντας το `Recognize`, μπορείτε να **εξάγετε κείμενο από JPG**, **μετατρέψετε εικόνα σε κείμενο** και **διαβάσετε κείμενο από την εικόνα** με λίγες μόνο γραμμές κώδικα.  

Από εδώ μπορείτε να εξερευνήσετε:

* Αποθήκευση των αποτελεσμάτων OCR σε βάση δεδομένων για αναζητήσιμα αρχεία.  
* Ενσωμάτωση της ροής εργασίας σε web API που δέχεται ανεβασμένες εικόνες.  
* Χρήση άλλων γλωσσικών modules (Arabic, Hindi, κ.λπ.) για να επεκτείνετε την εμβέλεια της εφαρμογής σας.

Μη διστάσετε να πειραματιστείτε με διαφορετικές μορφές εικόνας, γλώσσες και στρατηγικές επεξεργασίας batch. Το βασικό μοτίβο—**φόρτωση εικόνας για OCR → αναγνώριση → διαχείριση του κειμένου εξόδου**—παραμένει το ίδιο, παρέχοντάς σας μια ισχυρή βάση για οποιοδήποτε έργο εξαγωγής κειμένου.


## Τι θα μάθετε στη συνέχεια;


Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε πρόσθετα χαρακτηριστικά του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση των δικών σας έργων.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [How to extract text from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}