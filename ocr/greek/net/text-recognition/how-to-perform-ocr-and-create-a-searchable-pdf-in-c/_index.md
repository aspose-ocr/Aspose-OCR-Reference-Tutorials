---
category: general
date: 2026-02-14
description: Μάθετε πώς να εκτελείτε OCR σε αρχείο TIFF ή εικόνα και να μετατρέπετε
  PDF χρησιμοποιώντας OCR για να δημιουργήσετε ένα αναζητήσιμο PDF—βήμα‑βήμα οδηγός
  C#.
draft: false
keywords:
- how to perform OCR
- convert pdf using OCR
- make searchable pdf
- tiff to searchable pdf
- searchable pdf from image
language: el
og_description: Ανακαλύψτε πώς να εκτελείτε OCR σε εικόνες, να μετατρέπετε PDF με
  OCR και να δημιουργείτε αναζητήσιμο PDF με το Aspose OCR σε ένα σύντομο tutorial
  C#.
og_title: Πώς να κάνετε OCR και να δημιουργήσετε ένα αναζητήσιμο PDF σε C#
tags:
- OCR
- C#
- Aspose
- PDF conversion
title: Πώς να κάνετε OCR και να δημιουργήσετε ένα PDF με δυνατότητα αναζήτησης σε
  C#
url: /el/net/text-recognition/how-to-perform-ocr-and-create-a-searchable-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εκτελέσετε OCR και να Δημιουργήσετε ένα Αναζητήσιμο PDF σε C#

Κάποτε χρειάστηκε να **εκτελέσετε OCR** σε ένα σαρωμένο έγγραφο αλλά δεν ήξερες πώς να μετατρέψεις το αποτέλεσμα σε αναζητήσιμο PDF; Δεν είσαι μόνος—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το εμπόδιο όταν δουλεύουν με παλιά αρχεία TIFF ή PDF που περιέχουν μόνο εικόνες. Τα καλά νέα; Με λίγες γραμμές C# και τη βιβλιοθήκη Aspose.OCR, μπορείς να μετατρέψεις ένα TIFF ή οποιαδήποτε εικόνα σε πλήρως αναζητήσιμο PDF σε δευτερόλεπτα.

Σε αυτό το tutorial θα περάσουμε από όλα όσα χρειάζεσαι: από την εγκατάσταση της βιβλιοθήκης, τη φόρτωση ενός πολυ-σελιδικού TIFF, μέχρι την κλήση του `RecognizeToPdf` ώστε να **μετατρέψεις PDF χρησιμοποιώντας OCR** και **να δημιουργήσεις αναζητήσιμο PDF** που οι χρήστες σου μπορούν πραγματικά να ψάξουν. Στο τέλος, θα έχεις μια έτοιμη για εκτέλεση εφαρμογή console που παράγει ένα αναζητήσιμο PDF από πηγή εικόνας.

## Προαπαιτούμενα

- **.NET 6.0** ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.7+).
- Ένα έγκυρο **Aspose.OCR** license ή ένα προσωρινό κλειδί αξιολόγησης (η δωρεάν δοκιμή είναι επαρκής για δοκιμές).
- Visual Studio 2022 (ή οποιονδήποτε επεξεργαστή προτιμάς) με τον **NuGet** package manager.
- Ένα αρχείο εισόδου με όνομα `input.tif` τοποθετημένο σε φάκελο που ελέγχεις—πολυ-σελιδικά TIFF λειτουργούν αμέσως.

> **Συμβουλή:** Αν εργάζεσαι σε Windows, αντέγραψε το TIFF στον ίδιο φάκελο με το μεταγλωττισμένο `.exe` για να αποφύγεις προβλήματα διαδρομών.

## Βήμα 1: Εγκατάσταση του Πακέτου NuGet Aspose.OCR

Άνοιξε το φάκελο του έργου σου σε τερματικό και εκτέλεσε:

```bash
dotnet add package Aspose.OCR
```

Αυτό κατεβάζει την πιο πρόσφατη σταθερή έκδοση (από τον Φεβρουάριο 2026 είναι η 23.10) και προσθέτει όλες τις απαιτούμενες εξαρτήσεις. Μετά το τέλος της επαναφοράς, θα δεις το `Aspose.OCR` κάτω από **Dependencies** στον Solution Explorer.

## Βήμα 2: Δημιουργία Ελάχιστης Εφαρμογής Console

Δημιούργησε ένα νέο έργο console αν δεν έχεις ήδη:

```bash
dotnet new console -n OcrSearchablePdfDemo
cd OcrSearchablePdfDemo
```

Αντικατέστησε το αυτόματα δημιουργημένο `Program.cs` με τον πλήρη κώδικα που φαίνεται στο **Βήμα 3**. Το πρόγραμμα θα:

1. Δημιουργήσει μια παρουσία του OCR engine.
2. Φορτώσει την πηγή εικόνας (ή πολυ‑σελιδικό TIFF).
3. Εκτελέσει OCR και γράψει το αποτέλεσμα απευθείας σε αναζητήσιμο PDF.
4. Ειδοποιήσει τον χρήστη ότι η διαδικασία ολοκληρώθηκε με επιτυχία.

## Βήμα 3: Πλήρης Λειτουργικός Κώδικας – Από Εικόνα σε Αναζητήσιμο PDF

Παρακάτω είναι το **ολόκληρο** αρχείο πηγαίου κώδικα. Αντέγραψε‑επικόλλησέ το στο `Program.cs`. Τα σχόλια εξηγούν τα μη‑προφανή μέρη.

```csharp
using System;
using Aspose.OCR;          // Core OCR namespace
using Aspose.OCR.Image;   // Provides ImageStream helpers

namespace OcrSearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Initialise the OCR engine.
            // -------------------------------------------------
            // The Engine class is the entry point for all OCR operations.
            // You can optionally pass a license object here if you have one.
            var ocrEngine = new Engine();

            // -------------------------------------------------
            // 2️⃣ Load the source image.
            // -------------------------------------------------
            // ImageStream.FromFile supports TIFF, PDF, JPEG, PNG, etc.
            // For multi‑page TIFFs the stream automatically contains all pages.
            string inputPath = "YOUR_DIRECTORY/input.tif";
            var imageStream = ImageStream.FromFile(inputPath);

            // -------------------------------------------------
            // 3️⃣ Perform OCR and write a searchable PDF.
            // -------------------------------------------------
            // RecognizeToPdf does the heavy lifting:
            // • It runs the OCR engine on every page.
            // • It embeds the extracted text as an invisible layer.
            // • The visual appearance of the original image is preserved.
            string outputPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.RecognizeToPdf(imageStream, outputPath);

            // -------------------------------------------------
            // 4️⃣ Inform the user.
            // -------------------------------------------------
            Console.WriteLine("Searchable PDF created at: " + outputPath);
        }
    }
}
```

**Τι θα δεις:** Μετά την εκτέλεση του προγράμματος, ένα αρχείο με όνομα `searchable.pdf` εμφανίζεται στον φάκελο προορισμού. Άνοιξέ το σε Adobe Reader ή οποιονδήποτε προβολέα PDF και δοκίμασε την αναζήτηση μιας λέξης που υπάρχει στο αρχικό TIFF. Το κείμενο θα βρεθεί αμέσως, αποδεικνύοντας ότι **δημιούργησες αναζητήσιμο PDF** από εικόνα.

### Εκτέλεση της Εφαρμογής

```bash
dotnet run
```

Αν όλα είναι ρυθμισμένα σωστά, θα δεις:

```
Searchable PDF created at: YOUR_DIRECTORY/searchable.pdf
```

Άνοιξε το PDF, πάτησε `Ctrl+F`, πληκτρολόγησε μια λέξη από την πηγή και παρατήρησε την επισήμανση να πηδά στη σωστή θέση.

## Βήμα 4: Συχνές Παραλλαγές και Ακραίες Περιπτώσεις

### Μετατροπή Κανονικού PDF (μόνο‑εικόνα) σε Αναζητήσιμο PDF

Αν η πηγή σου είναι PDF που περιέχει σαρωμένες εικόνες αντί για κείμενο, μπορείς ακόμα να χρησιμοποιήσεις την ίδια μέθοδο—απλώς άλλαξε την πηγή του `ImageStream`:

```csharp
var pdfStream = ImageStream.FromFile("YOUR_DIRECTORY/input.pdf");
ocrEngine.RecognizeToPdf(pdfStream, "YOUR_DIRECTORY/searchable_from_pdf.pdf");
```

Αυτό καλύπτει το σενάριο **convert pdf using OCR** χωρίς επιπλέον κώδικα.

### Διαχείριση Μεγάλων Πολυ‑Σελιδικών Εγγράφων

Για έγγραφα που υπερβαίνουν μερικές εκατοντάδες σελίδες, σκέψου:

- **Αύξηση ορίων μνήμης** (`Engine.MemoryLimit = 2_000; // MB`).
- **Επεξεργασία σε τμήματα**: φόρτωσε ένα υποσύνολο σελίδων, γράψε ενδιάμεσα PDFs, έπειτα συγχέσου τα χρησιμοποιώντας μια βιβλιοθήκη PDF (π.χ., Aspose.PDF).

### Διαχείριση Γλωσσών Εκτός Αγγλικών

Το Aspose.OCR υποστηρίζει πολλές γλώσσες αμέσως. Όρισε τη γλώσσα πριν από την αναγνώριση:

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

Αν χρειάζεσαι **tiff to searchable pdf** σε μη‑λατινικό αλφάβητο, βεβαιώσου ότι το αντίστοιχο language pack είναι εγκατεστημένο.

### Τι Να Κάνεις Αν Το PDF Εξόδου Είναι Κενό;

- Επαλήθευσε ότι το αρχείο εισόδου δεν είναι κατεστραμμένο.
- Σιγουρέψου ότι ο OCR engine έχει έγκυρη άδεια—η λειτουργία αξιολόγησης μπορεί να επιβάλλει όρια σελίδων.
- Έλεγξε ότι η ανάλυση της εικόνας είναι τουλάχιστον 300 dpi· χαμηλότερες αναλύσεις μπορούν να προκαλέσουν κακή αναγνώριση.

## Βήμα 5: Επαλήθευση του Αποτελέσματος Προγραμματιστικά (Προαιρετικό)

Μερικές φορές θέλεις να επιβεβαιώσεις ότι το PDF περιέχει πραγματικά μια στρώση κειμένου. Μπορείς να χρησιμοποιήσεις το Aspose.PDF για εξαγωγή κειμένου:

```csharp
using Aspose.Pdf;

var pdfDoc = new Document("YOUR_DIRECTORY/searchable.pdf");
string extracted = pdfDoc.Pages[1].ExtractText();
Console.WriteLine("First page text snippet: " + extracted.Substring(0, 100));
```

Αν το `extracted` δεν είναι κενό, έχεις **δημιουργήσει αναζητήσιμο pdf** με επιτυχία.

## Συμπέρασμα

Καλύψαμε **πώς να εκτελέσετε OCR** σε TIFF (ή οποιαδήποτε εικόνα) και πώς να **μετατρέψετε PDF χρησιμοποιώντας OCR** για να δημιουργήσετε ένα **αναζητήσιμο PDF** που συμπεριφέρεται σαν εγγενές έγγραφο. Τα βασικά βήματα είναι:

1. Εγκατάσταση Aspose.OCR.  
2. Αρχικοποίηση `Engine`.  
3. Φόρτωση της εικόνας μέσω `ImageStream`.  
4. Κλήση `RecognizeToPdf`.  

Από εκεί μπορείς να πειραματιστείς με ρυθμίσεις γλώσσας, μαζική επεξεργασία μεγάλων αρχείων, ή να συνδυάσεις το αποτέλεσμα με άλλες εργασίες διαχείρισης PDF. Το ίδιο μοτίβο λειτουργεί για **tiff to searchable pdf**, **searchable pdf from image**, και ακόμη για σαρωμένα PDF.

Έτοιμος για την επόμενη πρόκληση; Δοκίμασε να ενσωματώσεις OCR σε ένα web API ώστε οι χρήστες να ανεβάζουν σαρώσεις και να λαμβάνουν άμεσα αναζητήσιμα PDFs, ή εξερεύνησε OCR σε χειρόγραφες σημειώσεις χρησιμοποιώντας τις προχωρημένες ρυθμίσεις του `OcrEngine`. Οι δυνατότητες είναι απεριόριστες—καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}