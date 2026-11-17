---
category: general
date: 2026-08-22
description: Μάθετε να αναγνωρίζετε κείμενο από εικόνα χρησιμοποιώντας το Aspose.OCR.
  Αυτός ο οδηγός καλύπτει επίσης την OCR εικόνας σε κείμενο και την εξαγωγή κειμένου
  από jpg σε λίγα βήματα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from image
- ocr image to text
- extract text from jpg
- convert image to text
- read cyrillic text image
language: el
lastmod: 2026-08-22
og_description: Αναγνωρίστε κείμενο από εικόνα χρησιμοποιώντας το Aspose.OCR σε C#.
  Ακολουθήστε αυτό το σεμινάριο για OCR εικόνας σε κείμενο, εξαγωγή κειμένου από jpg
  και ανάγνωση εικόνας με κυριλλικό κείμενο.
og_image_alt: Screenshot of C# console output showing recognized Cyrillic text from
  a JPG image
og_title: Αναγνώριση κειμένου από εικόνα με το Aspose.OCR – βήμα‑βήμα οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-08-22'
  description: Learn to recognize text from image using Aspose.OCR. This guide also
    covers OCR image to text and extract text from jpg in a few steps.
  headline: How to recognize text from image with Aspose.OCR in C#
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: Πώς να αναγνωρίσετε κείμενο από εικόνα με το Aspose.OCR σε C#
url: /el/net/text-recognition/how-to-recognize-text-from-image-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση κειμένου από εικόνα με Aspose.OCR – πλήρες C# tutorial

Αν χρειάζεστε να αναγνωρίσετε κείμενο από εικόνα σε ένα έργο .NET, αυτό το tutorial σας παρουσιάζει μια έτοιμη‑για‑εκτέλεση λύση. Θα δείτε πώς να ρυθμίσετε τη μηχανή OCR, να επιλέξετε το σωστό module γλώσσας και να εξάγετε τους χαρακτήρες που εντοπίστηκαν. Το παράδειγμα δείχνει επίσης πώς να μετατρέψετε εικόνα σε κείμενο για μια κυριλλική εικόνα, καλύπτοντας την κοινή περίπτωση ανάγνωσης αρχείων εικόνας με κυριλλικό κείμενο.

Πέρα από τα βασικά βήματα, θα μάθετε πώς να εξάγετε κείμενο από αρχεία jpg, να μετατρέψετε εικόνα σε κείμενο για άλλες μορφές και να διαχειριστείτε καταστάσεις όπου το module γλώσσας πρέπει να ληφθεί αυτόματα. Δεν απαιτούνται εξωτερικές υπηρεσίες πέρα από το πακέτο NuGet Aspose.OCR.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

- .NET 6.0 SDK ή νεότερο εγκατεστημένο  
- Visual Studio 2022 (ή οποιοσδήποτε επεξεργαστής που υποστηρίζει C#)  
- Πρόσβαση στο Internet για την πρώτη εκτέλεση (το module γλώσσας Κυριλλικού λήγεται κατ' απαίτηση)  
- Το πακέτο NuGet Aspose.OCR (`dotnet add package Aspose.OCR`)  

Αυτά τα στοιχεία σας επιτρέπουν να μεταγλωττίσετε και να εκτελέσετε τον κώδικα χωρίς πρόσθετη διαμόρφωση.

## Βήμα 1: Δημιουργία νέου έργου console

Ανοίξτε ένα τερματικό και εκτελέστε τις παρακάτω εντολές για να δημιουργήσετε μια ελάχιστη εφαρμογή console:

```bash
dotnet new console -n ImageOcrDemo
cd ImageOcrDemo
dotnet add package Aspose.OCR
```

Η εντολή `dotnet new console` δημιουργεί ένα αρχείο `Program.cs` και ένα αρχείο έργου που αναφέρει τη βιβλιοθήκη Aspose.OCR. Η προσθήκη του πακέτου επιλύει όλες τις απαιτούμενες συναρτήσεις.

## Βήμα 2: Εισαγωγή του namespace Aspose.OCR

Επεξεργαστείτε το **Program.cs** και προσθέστε τη δήλωση `using Aspose.OCR;` στην κορυφή του αρχείου. Αυτό καθιστά τις κλάσεις OCR διαθέσιμες χωρίς πλήρως προσδιορισμένα ονόματα.

```csharp
using System;
using Aspose.OCR;
```

Η δήλωση `using` βελτιώνει την αναγνωσιμότητα και διατηρεί τον κώδικα εστιασμένο στη ροή εργασίας OCR.

## Βήμα 3: Αρχικοποίηση της μηχανής OCR

Δημιουργήστε ένα αντικείμενο `OcrEngine`. Η μηχανή διατηρεί ρυθμίσεις όπως το module γλώσσας και τις παραμέτρους αναγνώρισης.

```csharp
// Initialise the OCR engine
var ocrEngine = new OcrEngine();
```

Η δημιουργία της μηχανής μία φορά ανά εφαρμογή είναι αποδοτική, επειδή οι υποκείμενες βιβλιοθήκες native φορτώνονται μόνο μία φορά.

## Βήμα 4: Επιλογή του module γλώσσας

Για κυριλλικό κείμενο, ορίστε την ιδιότητα `Language` σε `Language.Cyrillic`. Το Aspose.OCR κατεβάζει αυτόματα το module εάν λείπει, έτσι η πρώτη εκτέλεση μπορεί να διαρκέσει μερικά δευτερόλεπτα.

```csharp
// Choose Cyrillic language module – it will be downloaded if absent
ocrEngine.Language = Language.Cyrillic;
```

Αν αργότερα χρειαστεί να μετατρέψετε εικόνα σε κείμενο σε άλλη γλώσσα (π.χ., Αγγλικά ή Αραβικά), αντικαταστήστε το `Language.Cyrillic` με την αντίστοιχη τιμή enum. Αυτή η ευελιξία σας επιτρέπει να μετατρέψετε εικόνα σε κείμενο για οποιοδήποτε υποστηριζόμενο σύστημα γραφής.

## Βήμα 5: Αναγνώριση κειμένου από αρχείο JPG

Καλέστε το `RecognizeImage` με τη πλήρη διαδρομή προς την εικόνα. Η μέθοδος επιστρέφει ένα `OcrResult` που περιέχει το εξαγόμενο κείμενο.

```csharp
// Path to the source image – replace with your own file
string imagePath = @"YOUR_DIRECTORY/sample_image.jpg";

// Perform OCR – this extracts text from the JPG file
OcrResult result = ocrEngine.RecognizeImage(imagePath);
```

Η κλήση λειτουργεί με οποιαδήποτε μορφή raster εικόνας υποστηρίζεται από το Aspose.OCR (JPG, PNG, BMP, TIFF). Η χρήση JPG εξασφαλίζει ότι μπορείτε να εξάγετε κείμενο από αρχεία jpg χωρίς επιπλέον βήματα μετατροπής.

## Βήμα 6: Εξαγωγή του αναγνωρισμένου κειμένου

Τέλος, γράψτε το αναγνωρισμένο κείμενο στην κονσόλα. Αυτό δείχνει έναν απλό τρόπο ανάγνωσης εικόνας με κυριλλικό κείμενο και εμφάνισής του.

```csharp
// Show the recognised text in the console
Console.WriteLine("Recognised text:");
Console.WriteLine(result.Text);
```

Όταν εκτελέσετε το πρόγραμμα, θα πρέπει να δείτε τους κυριλλικούς χαρακτήρες να εκτυπώνονται ακριβώς όπως εμφανίζονται στην αρχική εικόνα.

## Πλήρες λειτουργικό παράδειγμα

Παρακάτω βρίσκεται το πλήρες αρχείο **Program.cs** που μπορείτε να αντιγράψετε, επικολλήσετε και να τρέξετε αμέσως.

```csharp
using System;
using Aspose.OCR;

namespace ImageOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Step 2: Choose the language module required for recognition (Cyrillic in this case)
            // The language module will be downloaded automatically if not present
            ocrEngine.Language = Language.Cyrillic;

            // Step 3: Provide the path to the image you want to process
            // You can replace the file name with any JPG, PNG, BMP, or TIFF image
            string imagePath = @"YOUR_DIRECTORY/sample_image.jpg";

            // Step 4: Recognise text from the image file
            OcrResult result = ocrEngine.RecognizeImage(imagePath);

            // Step 5: Output the recognised text
            Console.WriteLine("Recognised text:");
            Console.WriteLine(result.Text);
        }
    }
}
```

### Αναμενόμενο αποτέλεσμα

```
Recognised text:
Пример текста на кириллице
```

Το ακριβές αποτέλεσμα εξαρτάται από το περιεχόμενο του `sample_image.jpg`. Αν η εικόνα περιέχει αγγλικό κείμενο, ο ίδιος κώδικας θα επιστρέψει το αγγλικό κείμενο εφόσον ορίσετε `ocrEngine.Language = Language.English;`.

## Διαχείριση κοινών προβλημάτων

| Πρόβλημα | Γιατί συμβαίνει | Πώς να το επιλύσετε |
|----------|----------------|----------------------|
| Language module not found | Η πρώτη εκτέλεση προσπαθεί να κατεβάσει το module αλλά η διαδικασία αποτυγχάνει λόγω περιορισμών firewall. | Βεβαιωθείτε ότι το μηχάνημα μπορεί να προσεγγίσει το `https://downloads.aspose.com/ocr` ή κατεβάστε χειροκίνητα το module από το portal της Aspose και τοποθετήστε το στον προεπιλεγμένο φάκελο (`%APPDATA%\Aspose\OCR\`). |
| Low accuracy on noisy images | Οι μηχανές OCR εξαρτώνται από καθαρή αντίθεση μεταξύ κειμένου και φόντου. | Προεπεξεργαστείτε την εικόνα (π.χ., αυξήστε την αντίθεση, μετατρέψτε σε γκρι) πριν καλέσετε το `RecognizeImage`. Το Aspose.OCR παρέχει επιλογές `ImagePreprocessing` που μπορείτε να εξερευνήσετε. |
| Non‑JPG formats | Κάποιοι προγραμματιστές υποθέτουν ότι ο κώδικας λειτουργεί μόνο με αρχεία JPG. | Το API δέχεται επίσης PNG, BMP και TIFF. Αλλάξτε την επέκταση αρχείου στο `imagePath` ανάλογα. |
| Large files cause long processing time | Μεγαλύτερες εικόνες απαιτούν περισσότερη μνήμη και κύκλους CPU. | Αλλάξτε το μέγεθος της εικόνας σε λογική ανάλυση (π.χ., 1500 × 1500) πριν από την αναγνώριση. |

Αυτές οι συμβουλές σας βοηθούν να μετατρέψετε εικόνα σε κείμενο αξιόπιστα σε διαφορετικά σενάρια.

## Επέκταση της λύσης

Μόλις μπορείτε να αναγνωρίσετε κείμενο από εικόνα, ίσως θέλετε να:

- **Αποθήκευση του αποτελέσματος σε αρχείο** – γράψτε `result.Text` σε αρχείο `.txt` ή `.docx`.  
- **Επεξεργασία παρτίδας φακέλου** – επαναλάβετε για όλα τα αρχεία σε έναν κατάλογο και εφαρμόστε την ίδια λογική OCR.  
- **Συνδυασμός με κανονικές εκφράσεις** – εξάγετε αριθμούς τηλεφώνου, ημερομηνίες ή άλλα μοτίβα από το αναγνωρισμένο κείμενο.  

Όλες αυτές οι επεκτάσεις χρησιμοποιούν τον ίδιο βασικό κώδικα, διατηρώντας την υλοποίηση σύντομη.

## Συμπέρασμα

Τώρα έχετε έναν πλήρη οδηγό για την αναγνώριση κειμένου από εικόνα χρησιμοποιώντας το Aspose.OCR σε C#. Το tutorial κάλυψε πώς να ρυθμίσετε το έργο, να αρχικοποιήσετε τη μηχανή OCR, να επιλέξετε το κυριλλικό module γλώσσας και να εξάγετε κείμενο από αρχείο JPG. Ακολουθώντας αυτά τα βήματα μπορείτε επίσης να μετατρέψετε εικόνα σε κείμενο για άλλες γλώσσες, να εξάγετε κείμενο από αρχεία jpg και να μετατρέψετε εικόνα σε κείμενο σε οποιαδήποτε εφαρμογή .NET.

Νιώστε ελεύθεροι να πειραματιστείτε με πρόσθετες γλώσσες, μεγαλύτερες παρτίδες ή λογική μετα-επεξεργασίας. Αν χρειαστεί να διαβάσετε εικόνα με κυριλλικό κείμενο σε διαφορετικό περιβάλλον—όπως ένα web API ή μια υπηρεσία Windows—το ίδιο μοτίβο ισχύει. Καλή κωδικοποίηση!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Αναγνώριση κειμένου εικόνας με Aspose OCR για πολλαπλές γλώσσες](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [pipeline προεπεξεργασίας OCR – Πώς να αναγνωρίσετε κείμενο από εικόνα σε C#](/ocr/english/net/ocr-optimization/ocr-preprocessing-pipeline-how-to-recognize-text-from-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}