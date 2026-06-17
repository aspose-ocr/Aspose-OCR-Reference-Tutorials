---
category: general
date: 2026-05-06
description: Δημιουργήστε αναζητήσιμο PDF από μια εικόνα χρησιμοποιώντας το Aspose
  OCR σε C#. Μάθετε πώς να μετατρέψετε PNG σε PDF, να εξάγετε κείμενο από την εικόνα
  και να δημιουργήσετε ένα αναζητήσιμο PDF.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- convert png to pdf
- ocr image to pdf
language: el
og_description: Δημιουργήστε αναζητήσιμο PDF από μια εικόνα χρησιμοποιώντας το Aspose
  OCR σε C#. Αυτό το βήμα‑βήμα tutorial δείχνει πώς να μετατρέψετε PNG σε PDF, να
  εξάγετε κείμενο από την εικόνα και να παραγάγετε ένα αναζητήσιμο PDF.
og_title: Δημιουργία PDF με δυνατότητα αναζήτησης από εικόνα – Οδηγός OCR με C# Aspose
tags:
- Aspose
- C#
- OCR
- PDF
title: Δημιουργία PDF με δυνατότητα αναζήτησης από εικόνα – Οδηγός C# Aspose OCR
url: /el/net/text-recognition/create-searchable-pdf-from-image-c-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία PDF με δυνατότητα αναζήτησης από εικόνα – Οδηγός C# Aspose OCR

Έχετε ποτέ χρειαστεί να **δημιουργήσετε PDF με δυνατότητα αναζήτησης** από μια σαρωμένη εικόνα αλλά δεν ήξερες από πού να ξεκινήσεις; Ίσως έχετε μια απόδειξη σε PNG, ένα JPEG μιας σύμβασης ή οποιοδήποτε bitmap που θέλετε να μετατρέψετε σε PDF που μπορείτε πραγματικά να αναζητήσετε. Αυτό είναι ένα κοινό πρόβλημα, ειδικά όταν ασχολείστε με παλιές σαρώσεις που μένουν αχρησιμοποίητες σε έναν φάκελο.

Τα καλά νέα είναι ότι με το Aspose OCR μπορείτε **να μετατρέψετε εικόνα σε PDF**, να εξάγετε το κρυφό κείμενο και να καταλήξετε με ένα πλήρως αναζητήσιμο έγγραφο—όλα σε λίγες γραμμές C#. Σε αυτόν τον οδηγό θα σας δείξουμε επίσης πώς να **μετατρέψετε png σε PDF**, **να εξάγετε κείμενο από εικόνα**, και ακόμη θα καλύψουμε την περίπτωση διαχείρισης πολυ‑σελίδων TIFF. Στο τέλος, θα έχετε μια αυτόνομη λύση που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET.

## Τι θα χρειαστείτε

- **.NET 6+** (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.6+)
- **Visual Studio 2022** ή οποιοδήποτε IDE προτιμάτε
- **Aspose.OCR** πακέτο NuGet (φέρνει αυτόματα το Aspose.PDF)
- Ένα αρχείο εικόνας (PNG, JPEG, BMP, TIFF) που θέλετε να μετατρέψετε σε PDF με δυνατότητα αναζήτησης

Καμία επιπλέον άδεια, καμία εξωτερική υπηρεσία—μόνο μια αναφορά NuGet και λίγα λεπτά κώδικα.

## Βήμα 1: Εγκατάσταση του πακέτου NuGet Aspose.OCR

Πρώτα απ' όλα, προσθέστε τη βιβλιοθήκη στο έργο σας. Ανοίξτε το Package Manager Console και εκτελέστε:

```powershell
Install-Package Aspose.OCR
```

Αυτή η εντολή κατεβάζει τόσο το **Aspose.OCR** όσο και το **Aspose.Pdf** assembly από το οποίο εξαρτάται, ώστε να είστε έτοιμοι να διαβάσετε την εικόνα και να γράψετε το PDF.

> **Pro tip:** Αν χρησιμοποιείτε το .NET CLI, το ισοδύναμο είναι `dotnet add package Aspose.OCR`.

## Βήμα 2: Αρχικοποίηση της μηχανής OCR

Δημιουργώντας μια παρουσία του `OcrEngine` ανοίγετε την πύλη για όλη τη δουλειά OCR. Σκεφτείτε το ως το μυαλό που θα κοιτάξει την εικόνα σας και θα αρχίσει να «διαβάζει» τους χαρακτήρες.

```csharp
using Aspose.OCR;
using Aspose.Pdf;   // pulled in by the OCR package

// Create an OCR engine instance – this object holds configuration and state
var ocrEngine = new OcrEngine();
```

Μπορεί να αναρωτιέστε, *γιατί να μην καλέσουμε απλώς μια στατική μέθοδο;* Η αντικειμενοστραφής προσέγγιση σας επιτρέπει να ρυθμίσετε παραμέτρους αργότερα (γλώσσα, ανάλυση κ.λπ.) χωρίς να αλλάξετε τη ροή.

## Βήμα 3: Φόρτωση της εικόνας που θέλετε να μετατρέψετε

Εδώ είναι που **μετατρέπουμε εικόνα σε PDF** κατά την ουσία—τροφοδοτώντας το bitmap στη μηχανή OCR. Αντικαταστήστε `"YOUR_DIRECTORY/input.png"` με το πραγματικό μονοπάτι του αρχείου σας.

```csharp
// Load the source image (PNG, JPEG, BMP, or multi‑page TIFF)
ocrEngine.SetImage("YOUR_DIRECTORY/input.png");
```

Αν έχετε μια περίπτωση **μετατροπής png σε pdf**, απλώς δείξτε στο PNG. Για πολυ‑σελίδες TIFF, το Aspose.OCR θα αντιμετωπίσει αυτόματα κάθε καρέ ως ξεχωριστή σελίδα.

## Βήμα 4: Εκτέλεση OCR και προαιρετική λήψη του κειμένου

Η κλήση `Recognize()` κάνει το σκληρό κομμάτι: αναλύει την εικόνα, εντοπίζει χαρακτήρες και επιστρέφει ένα δομημένο αποτέλεσμα. Μπορείτε να κρατήσετε το κείμενο για logging, ευρετηρίαση αναζήτησης ή εμφάνιση.

```csharp
// Perform OCR – this extracts the textual content from the image
var ocrResult = ocrEngine.Recognize();

// Optional: show the extracted text in the console
Console.WriteLine("Extracted text:");
Console.WriteLine(ocrResult.Text);
```

> **Γιατί να εξάγουμε το κείμενο;** Παρόλο που θα το ενσωματώσουμε στο τελικό PDF, η ακατέργαστη συμβολοσειρά μπορεί να φανεί χρήσιμη για επικύρωση ή ανάλυση.

## Βήμα 5: Διαμόρφωση επιλογών PDF για έγγραφο με δυνατότητα αναζήτησης

Το Aspose.PDF μας παρέχει μια ειδική λειτουργία `PdfSaveOptions` που ονομάζεται **CreateSearchablePdf**. Λέει στη βιβλιοθήκη να ενσωματώσει το κείμενο OCR ως αόρατο στρώμα πίσω από την εικόνα, καθιστώντας το PDF αναζητήσιμο.

```csharp
// Prepare PDF save options – this tells Aspose to embed OCR text
var pdfOptions = PdfSaveOptions.CreateSearchablePdf();
```

Αν ποτέ χρειαστείτε ένα απλό PDF μόνο με εικόνα (χωρίς κρυφό κείμενο), μπορείτε να αλλάξετε σε `PdfSaveOptions.CreatePdf()`. Αλλά για τον στόχο μας—**δημιουργία PDF με δυνατότητα αναζήτησης**—η λειτουργία αναζητήσιμου PDF είναι το αστέρι.

## Βήμα 6: Αποθήκευση του PDF με δυνατότητα αναζήτησης στο δίσκο

Τώρα ενώνουμε όλα τα κομμάτια. Η μέθοδος `SavePdf` γράφει την εικόνα και το κρυφό κείμενο σε ένα μόνο αρχείο.

```csharp
// Save the searchable PDF file
ocrEngine.SavePdf("YOUR_DIRECTORY/output.pdf", pdfOptions);

Console.WriteLine("Searchable PDF created successfully.");
```

Σε αυτό το σημείο έχετε ένα **PDF με δυνατότητα αναζήτησης** που μπορείτε να ανοίξετε στο Adobe Reader, να πληκτρολογήσετε μια λέξη στο πεδίο αναζήτησης και να μεταβείτε αμέσως στη θέση που ταιριάζει—παρόλο που η ορατή σελίδα είναι ακόμα η αρχική εικόνα.

## Πλήρες λειτουργικό παράδειγμα

Συνδυάζοντας όλα τα κομμάτια, εδώ είναι μια έτοιμη για εκτέλεση κονσολική εφαρμογή. Αντιγράψτε‑και‑επικολλήστε την σε ένα νέο έργο C#, προσαρμόστε τα μονοπάτια αρχείων και πατήστε **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.Pdf; // included automatically with Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image that contains the scanned document
        // Replace with your actual image path
        ocrEngine.SetImage("YOUR_DIRECTORY/input.png");

        // Step 3: Run the OCR process to extract text (optional but useful)
        var ocrResult = ocrEngine.Recognize();

        // Show extracted text – helpful for debugging
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("======================");

        // Step 4: Prepare to export the recognized content as a searchable PDF
        var pdfOptions = PdfSaveOptions.CreateSearchablePdf();

        // Step 5: Save the searchable PDF to disk
        // Replace with your desired output path
        ocrEngine.SavePdf("YOUR_DIRECTORY/output.pdf", pdfOptions);

        // Step 6: Inform the user that the PDF has been created
        Console.WriteLine("Searchable PDF created successfully.");
    }
}
```

### Αναμενόμενο αποτέλεσμα

Όταν εκτελέσετε το πρόγραμμα, η κονσόλα θα εμφανίσει κάτι όπως:

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑04‑30
Total: $1,250.00
...
======================
Searchable PDF created successfully.
```

Και στον φάκελο `YOUR_DIRECTORY` θα βρείτε το `output.pdf`. Ανοίξτε το, πατήστε **Ctrl F**, πληκτρολογήστε “Invoice” και θα μεταβείτε αμέσως στη λέξη—παρόλο που η σελίδα φαίνεται σαν επίπεδη σάρωση.

## Διαχείριση κοινών παραλλαγών

### Μετατροπή πολλαπλών εικόνων ταυτόχρονα

Αν έχετε έναν φάκελο γεμάτο PNG και θέλετε ένα ενιαίο PDF με δυνατότητα αναζήτησης, κάντε βρόχο στα αρχεία και προσθέστε το καθένα ως ξεχωριστή σελίδα:

```csharp
var allImages = Directory.GetFiles("YOUR_DIRECTORY", "*.png");
var ocrEngine = new OcrEngine();
var pdfOptions = PdfSaveOptions.CreateSearchablePdf();

foreach (var imgPath in allImages)
{
    ocrEngine.SetImage(imgPath);
    ocrEngine.Recognize(); // extracts text for the current page
    ocrEngine.SavePdf("temp_page.pdf", pdfOptions);

    // Merge temp_page.pdf into the final document (omitted for brevity)
}
```

Μπορείτε επίσης να χρησιμοποιήσετε το `PdfFileEditor` από το Aspose.PDF για να συγχωνεύσετε τα προσωρινά PDFs σε ένα τελικό αρχείο.

### Αντιμετώπιση σαρώσεων χαμηλής ανάλυσης

Η ακρίβεια του OCR μειώνεται όταν το DPI της εικόνας είναι κάτω από 150. Πριν τροφοδοτήσετε την εικόνα, μπορείτε να την αυξήσετε:

```csharp
ocrEngine.ImageProcessingOptions.Dpi = 300; // forces 300 DPI for better recognition
```

### Επιλογή συγκεκριμένης γλώσσας

Αν το έγγραφό σας δεν είναι στα Αγγλικά, ορίστε τη γλώσσα πριν το `Recognize()`:

```csharp
ocrEngine.Language = Language.Spanish; // or Language.French, etc.
```

Αυτές οι ρυθμίσεις εξασφαλίζουν ότι η **εξαγωγή κειμένου από εικόνα** λειτουργεί αξιόπιστα σε διαφορετικά σενάρια.

## Οπτικό αποτέλεσμα

![PDF με δυνατότητα αναζήτησης δημιουργημένο με Aspose OCR – δημιουργία PDF με δυνατότητα αναζήτησης](https://example.com/images/searchable-pdf.png)

*Το παραπάνω στιγμιότυπο δείχνει ένα PDF όπου η εικόνα είναι ορατή, αλλά το στρώμα κειμένου μπορεί να αναζητηθεί.*

## Συμπέρασμα

Τώρα έχετε μια πλήρη, έτοιμη για παραγωγή συνταγή για **δημιουργία PDF με δυνατότητα αναζήτησης** από οποιαδήποτε εικόνα χρησιμοποιώντας Aspose OCR και C#. Καλύψαμε πώς να **μετατρέψετε εικόνα σε PDF**, **να εξάγετε κείμενο από εικόνα**, και ακόμη αγγίξαμε τις περιπτώσεις **μετατροπής png σε pdf** και **ocr image to pdf**. Ο κώδικας είναι πλήρως αυτόνομος, τρέχει σε οποιοδήποτε .NET runtime, και μπορεί να επεκταθεί για επεξεργασία δέσμης ή προσαρμοσμένη υποστήριξη γλώσσας.

Τι ακολουθεί; Δοκιμάστε να προσθέσετε υδατογράφημα, να κρυπτογραφήσετε το PDF, ή να τροφοδοτήσετε το εξαγόμενο κείμενο σε έναν ευρετήριο αναζήτησης όπως το Elasticsearch. Οι δυνατότητες είναι ατελείωτες, και το ίδιο μοτίβο—φόρτωση → αναγνώριση → αποθήκευση—θα σας εξυπηρετήσει σε κάθε ροή εργασίας που βασίζεται σε OCR.

Αν αντιμετωπίσετε δυσκολίες ή έχετε κάποιο ενδιαφέρον use‑case να μοιραστείτε, αφήστε ένα σχόλιο παρακάτω. Καλό κώδικα και απολαύστε τη μετατροπή αυτών των επίμονων σαρώσεων σε χρυσό με δυνατότητα αναζήτησης!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}