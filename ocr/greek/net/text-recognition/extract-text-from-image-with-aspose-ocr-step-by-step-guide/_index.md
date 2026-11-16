---
category: general
date: 2026-03-17
description: Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας Aspose OCR σε C#. Μάθετε
  πώς να εφαρμόζετε φίλτρο διαμέσου, να φορτώνετε εικόνα για OCR, να δημιουργείτε
  μηχανή OCR και να εκτελείτε την αναγνώριση OCR αποδοτικά.
draft: false
keywords:
- extract text from image
- apply median filter
- load image for ocr
- run ocr recognition
- create ocr engine
language: el
og_description: Εξάγετε κείμενο από εικόνα γρήγορα. Αυτός ο οδηγός δείχνει πώς να
  δημιουργήσετε μηχανή OCR, να εφαρμόσετε φίλτρο διαμέσου, να φορτώσετε εικόνα για
  OCR και να εκτελέσετε αναγνώριση OCR σε C#.
og_title: Εξαγωγή κειμένου από εικόνα με Aspose OCR – Πλήρης οδηγός C#
tags:
- OCR
- C#
- Aspose
title: Εξαγωγή κειμένου από εικόνα με το Aspose OCR – Οδηγός βήμα‑προς‑βήμα
url: /el/net/text-recognition/extract-text-from-image-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Βήμα‑Βήμα

Έχετε ποτέ χρειαστεί να **εξάγετε κείμενο από εικόνα** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη να εμπιστευτείτε; Στο πρόσφατο έργο μου, χρειαζόμουν έναν αξιόπιστο τρόπο να εξάγω χειρόγραφες σημειώσεις από θορυβώδεις JPEGs, και το Aspose OCR αποδείχθηκε μια σταθερή επιλογή. Σε αυτό το tutorial θα δείτε ακριβώς πώς να **δημιουργήσετε OCR engine**, **φορτώσετε εικόνα για OCR**, **εφαρμόσετε median filter**, και τελικά **εκτελέσετε OCR recognition** για να λάβετε καθαρό κείμενο.

Θα περάσουμε από όλη τη διαδικασία—από την εγκατάσταση του πακέτου NuGet μέχρι την εκτύπωση του αποτελέσματος στην κονσόλα—ώστε να μπορείτε να αντιγράψετε‑επικολλήσετε ένα λειτουργικό παράδειγμα στη δική σας λύση. Χωρίς ασαφείς αναφορές, μόνο μια πλήρη, αυτόνομη λύση που μπορείτε να τρέξετε σήμερα.

> **Γρήγορη προεπισκόπηση:** Στο τέλος θα έχετε μια εφαρμογή κονσόλας C# που διαβάζει το `photo_noisy.jpg`, διορθώνει την κλίση, εξομαλύνει τον κόκκο με ένα median filter, και εκτυπώνει τη εξαγόμενη συμβολοσειρά.

---

## Τι Θα Χρειαστείτε

- **.NET 6+** (ή .NET Core 3.1 – το API είναι το ίδιο)
- **Aspose.OCR** πακέτο NuGet (`Install-Package Aspose.OCR`)
- Ένα δείγμα εικόνας, κατά προτίμηση ένας θορυβώδης σκαν (το `photo_noisy.jpg` λειτουργεί εξαιρετικά)
- Οποιοδήποτε IDE προτιμάτε—Visual Studio, Rider, ή VS Code

Αυτό είναι όλο. Χωρίς επιπλέον DLLs, χωρίς εξωτερικές υπηρεσίες, και χωρίς κρυφά αρχεία ρυθμίσεων. Αν έχετε ήδη ένα .NET project, απλώς προσθέστε το πακέτο και είστε έτοιμοι.

## Βήμα 1 – Δημιουργία OCR Engine (Πρωταρχική Ρύθμιση)

Το πρώτο πράγμα που πρέπει να κάνετε είναι **να δημιουργήσετε OCR engine**. Σκεφτείτε το engine ως τον εγκέφαλο που θα ερμηνεύσει τα pixel. Χωρίς αυτό, τίποτα άλλο δεν έχει σημασία.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

> **Γιατί είναι σημαντικό:** Το `OcrEngine` ενσωματώνει όλες τις προεπιλεγμένες ρυθμίσεις, συμπεριλαμβανομένης της ανίχνευσης γλώσσας και της προεπεξεργασίας εικόνας. Η δημιουργία του νωρίς σας δίνει ένα καθαρό ξεκίνημα για προσαρμογές αργότερα.

## Βήμα 2 – Εφαρμογή Median Filter (Μείωση Θορύβου)

Οι θορυβώδεις εικόνες κάνουν το OCR να δυσκολεύεται. Το βήμα **εφαρμογής median filter** εξομαλύνει τα στίγματα χωρίς να θολώνει τις άκρες, κάτι ιδανικό για κείμενο.

```csharp
// Clear any default filters that Aspose may have added
ocrEngine.Config.Filters.Clear();

// Add a deskew filter to correct any rotation
ocrEngine.Config.Filters.Add(new DeskewFilter());

// Add a median filter with a kernel size of 3
ocrEngine.Config.Filters.Add(new MedianFilter(3));
```

> **Συμβουλή επαγγελματία:** Ένα μέγεθος πυρήνα `3` λειτουργεί για τις περισσότερες σπόρια εικόνες. Αν η εικόνα σας είναι εξαιρετικά θορυβώδης, αυξήστε το σε `5`, αλλά προσέξτε να μην χάσετε λεπτές γραμμές.

## Βήμα 3 – Φόρτωση Εικόνας για OCR (Τροφοδοσία του Engine)

Τώρα **φορτώνουμε εικόνα για OCR**. Το Aspose παρέχει ένα βολικό βοηθητικό `ImageStream.FromFile` που διαβάζει το αρχείο σε μορφή που καταλαβαίνει το engine.

```csharp
// Point to your image file – adjust the path as needed
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/photo_noisy.jpg");
```

> **Ακραία περίπτωση:** Αν η εικόνα σας βρίσκεται σε ενσωματωμένο πόρο, χρησιμοποιήστε `ImageStream.FromStream(yourStream)` αντί αυτού. Το engine δέχεται οποιοδήποτε stream που μπορεί να αποκωδικοποιηθεί σε bitmap.

## Βήμα 4 – Εκτέλεση OCR Recognition (Λήψη του Κειμένου)

Με το engine έτοιμο και την εικόνα φορτωμένη, ήρθε η ώρα να **εκτελέσετε OCR recognition**. Αυτή η ενιαία κλήση κάνει όλη τη βαριά δουλειά—προεπεξεργασία, διαχωρισμό χαρακτήρων και μοντελοποίηση γλώσσας.

```csharp
// Perform the recognition
var ocrResult = ocrEngine.Recognize();

// The Text property holds the extracted string
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrResult.Text);
```

> **Τι θα δείτε:** Αν η εικόνα περιέχει “Hello World”, η κονσόλα θα εμφανίσει ακριβώς αυτό, χωρίς τυχόν άσχετα σύμβολα που αφαιρέθηκαν από το median filter.

## Βήμα 5 – Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω είναι το πλήρες πρόγραμμα, έτοιμο για μεταγλώττιση. Αποθηκεύστε το ως `Program.cs` μέσα σε ένα έργο κονσόλας, αντικαταστήστε το `YOUR_DIRECTORY` με το πραγματικό φάκελο, και τρέξτε `dotnet run`.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create OCR engine
            var ocrEngine = new OcrEngine();

            // Step 2: Apply filters – deskew + median
            ocrEngine.Config.Filters.Clear();
            ocrEngine.Config.Filters.Add(new DeskewFilter());
            ocrEngine.Config.Filters.Add(new MedianFilter(3));

            // Step 3: Load the image you want to process
            // Make sure the path points to a valid JPEG/PNG/TIFF file
            ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/photo_noisy.jpg");

            // Step 4: Run OCR recognition
            var ocrResult = ocrEngine.Recognize();

            // Step 5: Output the extracted text
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**Αναμενόμενη έξοδος (παράδειγμα):**

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
```

Αν η εικόνα είναι εντελώς κενή, το `ocrResult.Text` θα είναι μια κενή συμβολοσειρά—δεν υπάρχει πρόβλημα, απλώς ένα σήμα να ελέγξετε τη διαδρομή της εικόνας ή τις ρυθμίσεις του φίλτρου.

## Συχνές Ερωτήσεις & Πιθανά Προβλήματα

| Ερώτηση | Απάντηση |
|----------|--------|
| *Τι γίνεται αν η εικόνα είναι περιστραμμένη 90°;* | Το `DeskewFilter` ανιχνεύει και διορθώνει αυτόματα μικρές περιστροφές. Για ακραίες γωνίες, σκεφτείτε να προσθέσετε ένα προσαρμοσμένο φίλτρο περιστροφής πριν το deskew. |
| *Μπορώ να αλλάξω τη γλώσσα;* | Ναι—ορίστε `ocrEngine.Config.Language = Language.English;` (ή οποιαδήποτε υποστηριζόμενη γλώσσα) πριν καλέσετε `Recognize()`. |
| *Είναι το median filter ο μόνος μειωτής θορύβου;* | Καθόλου. Το Aspose προσφέρει επίσης `GaussianFilter` και `BilateralFilter`. Επιλέξτε ανάλογα με τον τύπο θορύβου που αντιμετωπίζετε. |
| *Πώς διαχειρίζομαι PDF με πολλές σελίδες;* | Επαναλάβετε για κάθε σελίδα, μετατρέψτε την σε εικόνα (π.χ., χρησιμοποιώντας Aspose.PDF), και τροφοδοτήστε κάθε εικόνα στο ίδιο OCR engine. |
| *Τι γίνεται αν χρειάζομαι το σκορ εμπιστοσύνης;* | Το `ocrResult.Confidence` επιστρέφει ένα float μεταξύ 0 και 1 που υποδεικνύει τη συνολική αξιοπιστία. |

## Οπτική Επισκόπηση

![Διάγραμμα ροής εξαγωγής κειμένου από εικόνα](ocr_flow.png "Εξαγωγή κειμένου από εικόνα")

Το παραπάνω διάγραμμα απεικονίζει τη ροή εργασίας: **create OCR engine → apply median filter → load image for OCR → run OCR recognition → get text**. Είναι μια γρήγορη αναφορά που μπορείτε να καρφιτσώσετε στο γραφείο σας.

## Συμπεράσματα

Μόλις περάσαμε από το πώς να **εξάγετε κείμενο από εικόνα** χρησιμοποιώντας Aspose OCR σε C#. Με το **δημιουργία OCR engine**, **εφαρμογή median filter**, **φόρτωση εικόνας για OCR**, και τελικά **εκτέλεση OCR recognition**, έχετε τώρα μια αξιόπιστη λύση που λειτουργεί σε θορυβώδεις σκαναρίσματα, αποδείξεις ή χειρόγραφες σημειώσεις.

Αν θέλετε να προχωρήσετε παραπέρα, δοκιμάστε:

- Αλλάζοντας σε `OcrEngine.Config.Language = Language.Spanish;` για πολυγλωσσικά έργα.
- Εξάγοντας το `ocrResult.Text` σε αρχείο JSON για επεξεργασία downstream.
- Συνδυάζοντας με το `Tesseract` για υβριδική προσέγγιση όταν το Aspose αντιμετωπίζει δυσκολίες με ορισμένες γραμματοσειρές.

Νιώστε ελεύθεροι να πειραματιστείτε, να ρυθμίσετε τις παραμέτρους του φίλτρου, και να μοιραστείτε τα αποτελέσματά σας στα σχόλια. Καλή προγραμματιστική, και εύχομαι οι εικόνες σας να είναι πάντα αναγνώσιμες!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}