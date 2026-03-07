---
category: general
date: 2026-03-07
description: Πώς να δημιουργήσετε ePub από σαρωμένες εικόνες χρησιμοποιώντας το Aspose
  OCR – μάθετε πώς να μετατρέψετε εικόνα σε ePub, να εξάγετε κείμενο από την εικόνα,
  να προσθέσετε συγγραφέα στο ePub και να φορτώσετε την εικόνα για OCR.
draft: false
keywords:
- how to create epub
- convert image to epub
- extract text from image
- add author to epub
- load image for ocr
language: el
og_description: Πώς να δημιουργήσετε ePub από σαρωμένες εικόνες σε C#. Αυτό το σεμινάριο
  σας δείχνει πώς να μετατρέψετε εικόνα σε ePub, να εξάγετε κείμενο από την εικόνα,
  να προσθέσετε συγγραφέα στο ePub και να φορτώσετε εικόνα για OCR.
og_title: Πώς να δημιουργήσετε ePub από εικόνες σε C# – Πλήρης οδηγός
tags:
- C#
- Aspose OCR
- ePub
- Document Conversion
title: Πώς να δημιουργήσετε ePub από εικόνες σε C# – Οδηγός βήμα‑προς‑βήμα
url: /el/net/text-recognition/how-to-create-epub-from-images-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να δημιουργήσετε ePub από εικόνες σε C# – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να δημιουργήσετε ePub** από μια συλλογή σαρωμένων σελίδων; Ίσως έχετε μερικά PNG ενός κλασικού μυθιστορήματος και θέλετε να τα μετατρέψετε σε ένα τακτοποιημένο ePub που μπορείτε να διαβάσετε σε οποιαδήποτε συσκευή. Τα καλά νέα είναι ότι με το Aspose OCR μπορείτε **να φορτώσετε εικόνα για OCR**, να εξαγάγετε το κείμενο και στη συνέχεια **να μετατρέψετε την εικόνα σε ePub** με λίγες μόνο γραμμές C#.

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία: φόρτωση της εικόνας, εξαγωγή του κειμένου, προσθήκη κάποιων μεταδεδομένων (ναι, θα **προσθέσουμε συγγραφέα στο epub**), και τέλος εγγραφή ενός συμβατού με τα πρότυπα αρχείου ePub. Στο τέλος θα έχετε ένα έτοιμο προς δημοσίευση ePub και μια σαφή κατανόηση κάθε βήματος, ώστε να μπορείτε να προσαρμόσετε τον κώδικα για βιβλία πολλαπλών σελίδων, προσαρμοσμένες γραμματοσειρές ή ακόμη και διανομή χωρίς DRM.

## Τι θα χρειαστείτε

- **.NET 6** ή νεότερο (το API λειτουργεί επίσης με .NET Standard 2.0+)  
- **Aspose.OCR for .NET** – μπορείτε να κατεβάσετε μια δωρεάν δοκιμή από την ιστοσελίδα της Aspose.  
- Μια σαρωμένη εικόνα όπως `book_page.png` τοποθετημένη κάπου στον δίσκο.  
- Ένα αγαπημένο IDE (Visual Studio, Rider ή VS Code – θα χρησιμοποιήσω το Visual Studio στις στιγμιότυπες).

Δεν απαιτούνται επιπλέον πακέτα NuGet· το Aspose.OCR περιλαμβάνει όλα όσα χρειάζεστε για εξαγωγή ePub.

---

![Πώς να δημιουργήσετε ePub από σαρωμένη εικόνα](/images/how-to-create-epub.png "Πώς να δημιουργήσετε ePub από μια σαρωμένη εικόνα χρησιμοποιώντας Aspose OCR")

## Βήμα 1 – Ρύθμιση του έργου και εγκατάσταση του Aspose.OCR

Πρώτα απ' όλα. Δημιουργήστε μια νέα εφαρμογή console:

```bash
dotnet new console -n OcrToEpubDemo
cd OcrToEpubDemo
```

Προσθέστε το πακέτο Aspose.OCR:

```bash
dotnet add package Aspose.OCR
```

Αυτό είναι όλο – η βιβλιοθήκη περιλαμβάνει τόσο OCR όσο και δυνατότητες εξαγωγής ePub, οπότε δεν θα χρειαστείτε επιπλέον εξαρτήσεις.

## Βήμα 2 – Φόρτωση εικόνας για OCR

Πριν μπορέσουμε **να εξάγουμε κείμενο από την εικόνα**, πρέπει να δώσουμε κάτι στον κινητήρα OCR για ανάγνωση. Η βοηθητική μέθοδος `ImageStream.FromFile` το κάνει αυτό εύκολα:

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Load the PNG (or JPG, TIFF, etc.) you want to process
// This is the “load image for OCR” step.
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/book_page.png");
```

> **Συμβουλή:** Αν η εικόνα σας βρίσκεται σε ενσωματωμένο πόρο, χρησιμοποιήστε `ImageStream.FromResource` αντί για `FromFile`.

## Βήμα 3 – Εξαγωγή κειμένου από την εικόνα

Τώρα ο κινητήρας διαβάζει τα pixel και τα μετατρέπει σε συμβολοσειρές Unicode. Η μέθοδος `Recognize` κάνει το σκληρό έργο.

```csharp
// Run the OCR process – this will fill ocrEngine.RecognitionResult
ocrEngine.Recognize();

// Optional: inspect the raw text
string rawText = ocrEngine.RecognitionResult.Text;
Console.WriteLine("Extracted text (first 200 chars):");
Console.WriteLine(rawText.Substring(0, Math.Min(200, rawText.Length)));
```

Γιατί να καλέσουμε το `Recognize` ξεχωριστά; Σας επιτρέπει να ελέγξετε την ακατέργαστη έξοδο OCR, να ρυθμίσετε τις γλώσσες ή ακόμη και να κάνετε ορθογραφικό έλεγχο πριν προχωρήσετε στη δημιουργία του ePub.

## Βήμα 4 – Προετοιμασία επιλογών εξαγωγής ePub (Προσθήκη συγγραφέα στο ePub)

Η δημιουργία ενός επαγγελματικού ePub δεν είναι μόνο η απόρριψη κειμένου· χρειάζεστε επίσης σωστά μεταδεδομένα. Η κλάση `EpubExportOptions` σας δίνει έναν καθαρό τρόπο να **προσθέσετε συγγραφέα στο ePub**, να ορίσετε τίτλο και να αποφασίσετε αν θα ενσωματώσετε τις αρχικές εικόνες.

```csharp
var epubExportOptions = new EpubExportOptions
{
    Title = "Scanned Book",          // Title shown in eReader libraries
    Author = "Unknown",              // This is where we “add author to epub”
    IncludeImages = true             // Embeds the original PNGs for visual fidelity
};
```

Αν έχετε πολλές σελίδες, μπορείτε να συνεχίσετε να καλείτε `ocrEngine.Image = …` και `ocrEngine.Recognize()` μέσα σε βρόχο· κάθε κλήση προσθέτει το περιεχόμενο της νέας σελίδας στο ίδιο έγγραφο ePub.

## Βήμα 5 – Μετατροπή εικόνας σε ePub και εξαγωγή

Με το κείμενο εξαγόμενο και τα μεταδεδομένα ορισμένα, το τελικό βήμα είναι μια γραμμή κώδικα που γράφει το αρχείο ePub στον δίσκο:

```csharp
// Export the recognized content to an ePub file
ocrEngine.ExportToEpub("YOUR_DIRECTORY/book.epub", epubExportOptions);

// Confirmation for the user
Console.WriteLine("ePub created.");
```

Το παραγόμενο `book.epub` μπορεί να ανοιχθεί στο Calibre, Apple Books ή σε οποιονδήποτε αναγνώστη συμβατό με EPUB. Επειδή ορίσαμε `IncludeImages = true`, το αρχικό PNG θα εμφανιστεί ως σελίδα‑εικόνα, διατηρώντας την εμφάνιση της σαρωμένης πηγής.

## Πλήρες λειτουργικό παράδειγμα

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι το πλήρες, έτοιμο‑να‑τρέξει πρόγραμμα:

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // This is the “load image for OCR” step.
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/book_page.png");

        // Step 3: Run the OCR recognition – we now “extract text from image”
        ocrEngine.Recognize();

        // (Optional) Print a snippet of the extracted text
        string snippet = ocrEngine.RecognitionResult.Text.Substring(0,
            Math.Min(200, ocrEngine.RecognitionResult.Text.Length));
        Console.WriteLine("Extracted text preview:");
        Console.WriteLine(snippet);
        Console.WriteLine();

        // Step 4: Set up ePub export options – we “add author to epub” here
        var epubExportOptions = new EpubExportOptions
        {
            Title = "Scanned Book",
            Author = "Unknown",
            IncludeImages = true   // embed the original images in the ePub
        };

        // Step 5: Export the recognized content – this is how we “convert image to epub”
        ocrEngine.ExportToEpub("YOUR_DIRECTORY/book.epub", epubExportOptions);

        // Step 6: Inform the user that the ePub has been created
        Console.WriteLine("ePub created.");
    }
}
```

### Αναμενόμενη έξοδος

```
Extracted text preview:
Chapter 1
It was a bright cold day in April, and the...
 
ePub created.
```

Ανοίξτε το `book.epub` στον αγαπημένο σας αναγνώστη και θα δείτε μια σελίδα τίτλου, τη γραμμή συγγραφέα (ακόμα και αν γράφει “Unknown”) και την σαρωμένη εικόνα να εμφανίζεται δίπλα σε επιλέξιμο κείμενο.

## Συχνές ερωτήσεις & Ακραίες περιπτώσεις

### Τι γίνεται αν η γλώσσα OCR δεν είναι Αγγλικά;

Το Aspose.OCR υποστηρίζει πάνω από 70 γλώσσες. Απλώς ορίστε την ιδιότητα `Language` πριν καλέσετε το `Recognize`:

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

### Πώς να διαχειριστώ βιβλία πολλαπλών σελίδων;

Τυλίξτε τη λογική φόρτωσης/αναγνώρισης σε έναν βρόχο `foreach`:

```csharp
string[] pages = Directory.GetFiles("YOUR_DIRECTORY", "*.png");
foreach (var pagePath in pages)
{
    ocrEngine.Image = ImageStream.FromFile(pagePath);
    ocrEngine.Recognize();
}
ocrEngine.ExportToEpub("YOUR_DIRECTORY/full_book.epub", epubExportOptions);
```

Κάθε επανάληψη προσθέτει το νέο αναγνωρισμένο κείμενο στο ίδιο ePub, διατηρώντας τη σειρά των σελίδων.

### Μπορώ να εξαιρέσω τις αρχικές εικόνες;

Βεβαίως – ορίστε `IncludeImages = false` στο `EpubExportOptions`. Το παραγόμενο ePub θα είναι καθαρό κείμενο ρεφλουο, μειώνοντας δραστικά το μέγεθος του αρχείου.

### Τι γίνεται με προσαρμοσμένες γραμματοσειρές ή στυλ;

Ο εξαγωγέας ePub του Aspose.OCR σας επιτρέπει να παρέχετε ένα CSS stylesheet μέσω της ιδιότητας `Css` στο `EpubExportOptions`. Με αυτόν τον τρόπο μπορείτε να επιβάλετε συγκεκριμένη οικογένεια γραμματοσειράς, διάστιχο ή περιθώρια.

## Συμπέρασμα

Τώρα ξέρετε **πώς να δημιουργήσετε ePub** από μια σαρωμένη εικόνα χρησιμοποιώντας το Aspose OCR σε C#. Το tutorial κάλυψε τα πάντα από **φόρτωση εικόνας για OCR**, μέσω **εξαγωγής κειμένου από εικόνα**, μέχρι **προσθήκη συγγραφέα στο epub**, και τελικά **μετατροπή εικόνας σε epub** με μία κλήση εξαγωγής. Με το πλήρες δείγμα κώδικα στα χέρια σας, μπορείτε να επεκτείνετε τη λύση για μαζική επεξεργασία ολόκληρων βιβλιοθηκών, προσθήκη προσαρμοσμένου εξώφυλλου ή ακόμη και ενσωμάτωση της ροής εργασίας σε ένα web API.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε τη μετατροπή PDF σε ePub ή πειραματιστείτε με τα όρια εμπιστοσύνης του OCR για να βελτιώσετε την ακρίβεια σε θορυβώδεις σαρώσεις. Ο ουρανός είναι το όριο όταν συνδυάζετε ισχυρό OCR με ευέλικτη δημιουργία ePub.

Καλή προγραμματιστική και απολαύστε την ανάγνωση του νεοδημιουργημένου ePub σας!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}