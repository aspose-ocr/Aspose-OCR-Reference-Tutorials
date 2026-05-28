---
category: general
date: 2026-05-28
description: Μάθημα OCR για την κορεατική γλώσσα χρησιμοποιώντας το Aspose σε C#.
  Μάθετε πώς να φορτώνετε εικόνα από ροή, να εξάγετε απλό κείμενο, να μετατρέπετε
  την εικόνα σε PDF και να εξάγετε PDF με δυνατότητα αναζήτησης.
draft: false
keywords:
- korean language ocr
- convert image to pdf
- load image from stream
- extract plain text
- export searchable pdf
language: el
og_description: OCR κορεατικής γλώσσας σε C# με χρήση Aspose. Οδηγός βήμα‑βήμα για
  τη φόρτωση εικόνας από ροή, την εξαγωγή απλού κειμένου, τη μετατροπή της εικόνας
  σε PDF και την εξαγωγή PDF με δυνατότητα αναζήτησης.
og_title: OCR Κορεατικής γλώσσας – Μετατροπή εικόνας σε PDF & εξαγωγή κειμένου (Οδηγός
  C#)
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Korean Language OCR tutorial using Aspose in C#. Learn how to load
    image from stream, extract plain text, convert image to PDF and export searchable
    PDF.
  headline: 'Korean Language OCR with Aspose: Convert Image to PDF and Extract Text
    in C#'
  type: TechArticle
tags:
- Aspose OCR
- C#
- Image Processing
title: 'OCR της κορεατικής γλώσσας με το Aspose: Μετατροπή εικόνας σε PDF και εξαγωγή
  κειμένου σε C#'
url: /el/net/text-recognition/korean-language-ocr-with-aspose-convert-image-to-pdf-and-ext/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Κορεατικής Γλώσσας με Aspose: Μετατροπή Εικόνας σε PDF και Εξαγωγή Κειμένου σε C#

Σας έχει ποτέ προβληματίσει πώς να εκτελέσετε **Korean Language OCR** σε μια εικόνα χωρίς να στέλνετε τίποτα στο σύννεφο; Δεν είστε ο μόνος. Είτε ψηφιοποιείτε πινακίδες δρόμου, επεξεργάζεστε αποδείξεις, είτε δημιουργείτε ένα πολυγλωσσικό ευρετήριο αναζήτησης, η δυνατότητα αναγνώρισης κορεατικών χαρακτήρων τοπικά μπορεί να σας εξοικονομήσει χρόνο, χρήματα και προβλήματα ιδιωτικότητας.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει πώς να **φορτώσετε εικόνα από ροή**, **εξάγετε απλό κείμενο**, **μετατρέψετε την εικόνα σε PDF**, και τέλος **εξάγετε αναζητήσιμο PDF**—όλα με το Aspose.OCR και μερικές γραμμές C#. Χωρίς εξωτερικές υπηρεσίες, χωρίς κρυφή μαγεία—απλός κώδικας .NET που μπορείτε να ενσωματώσετε σε οποιαδήποτε εφαρμογή κονσόλας.

## Τι Θα Κερδίσετε

- Ένα λειτουργικό πρόγραμμα κονσόλας που διαβάζει ένα αρχείο JPEG μέσω ροής αρχείου.  
- Κορεατικό κείμενο εξαγόμενο ως απλές συμβολοσειρές Unicode.  
- Λεπτομερές αναφορά JSON της εκτέλεσης OCR για αποσφαλμάτωση ή ανάλυση.  
- Ένα αναζητήσιμο PDF που μπορείτε να ανοίξετε σε οποιονδήποτε αναγνώστη PDF και να επιλέξετε πραγματικά τις κορεατικές λέξεις.  

**Προαπαιτούμενα**  
- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.7+).  
- Πακέτο NuGet Aspose.OCR για .NET εγκατεστημένο (`Install-Package Aspose.OCR`).  
- Ένας φάκελος που περιέχει το `korean_sign.jpg` και μια εγγράψιμη τοποθεσία για τα αρχεία εξόδου.  

Αν έχετε ήδη όλα αυτά έτοιμα, τέλεια—ας βάλουμε τα χέρια μας στη δουλειά.

## Βήμα 1: Αρχικοποίηση του OCR Engine για Korean Language OCR

Το πρώτο που χρειάζεστε είναι μια παρουσία `OcrEngine`. Η ενεργοποίηση του GPU (αν έχετε) επιταχύνει την αναγνώριση δραματικά, και η απενεργοποίηση της αυτόματης λήψης πόρων αναγκάζει τη βιβλιοθήκη να χρησιμοποιήσει τα offline language packs που παρέχετε.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Enable GPU acceleration – optional but fast
ocrEngine.Configuration.EnableGpu = true;

// We’ll supply the Korean language pack ourselves
ocrEngine.Configuration.AutomaticResourceDownload = false;
ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";
```

> **Γιατί είναι σημαντικό:**  
> *GPU acceleration* μπορεί να μειώσει το χρόνο επεξεργασίας από δευτερόλεπτα σε χιλιοστά του δευτερολέπτου για μεγάλες παρτίδες. Ο ορισμός του `AutomaticResourceDownload` σε `false` εξασφαλίζει ότι η επίδειξη λειτουργεί offline—μια κρίσιμη απαίτηση για πολλά επιχειρηματικά περιβάλλοντα.

## Βήμα 2: Φόρτωση Εικόνας από Ροή

Η ανάγνωση της εικόνας μέσω ροής σας δίνει ευελιξία: μπορείτε να αντλήσετε αρχεία από δίσκο, κοινόχρηστους δικτυακούς πόρους ή ακόμη και από blobs που είναι αποθηκευμένα στη μνήμη. Εδώ ανοίγουμε ένα τοπικό αρχείο JPEG, αλλά το ίδιο μοτίβο λειτουργεί για οποιοδήποτε `Stream`.

```csharp
using System.IO;

// Open the image file as a read‑only stream
using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");

// Feed the stream to the OCR engine
ocrEngine.Image = ImageStream.FromStream(imageStream);
```

> **Συμβουλή:** Αν χρειαστεί ποτέ να επεξεργαστείτε εικόνες που ανεβαίνουν μέσω web API, απλώς αντικαταστήστε το `File.OpenRead` με το εισερχόμενο `IFormFile.OpenReadStream()`—το υπόλοιπο παραμένει ίδιο.

## Βήμα 3: Επιλογή Κορεατικής Γλώσσας και Εφαρμογή Φίλτρων Προεπεξεργασίας

Το Aspose.OCR υποστηρίζει μια σειρά από βήματα προεπεξεργασίας που καθαρίζουν την εικόνα πριν την αναγνώριση. Για κορεατικές πινακίδες, η διόρθωση κλίσης (deskew) και η αποθορυβοποίηση (denoise) συνήθως αρκούν.

```csharp
using Aspose.OCR.Enums;

// Tell the engine we’re dealing with Korean text
ocrEngine.Configuration.Language = Language.Korean;

// Apply deskew and denoise filters
ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                            PreprocessFilter.Denoise;
```

> **Τι συμβαίνει στο παρασκήνιο;**  
> Το φίλτρο `Deskew` ευθυγραμμίζει το κείμενο που είναι περιστραμμένο, ενώ το `Denoise` αφαιρεί τον θόρυβο που μπορεί να μπερδέψει τον ταξινομητή χαρακτήρων. Η παράλειψη αυτών των βημάτων συχνά οδηγεί σε ακατανόητο αποτέλεσμα, ειδικά σε φωτογραφίες χαμηλής ανάλυσης.

## Βήμα 4: Ασύγχρονη Εξαγωγή Απλού Κειμένου

Τώρα έρχεται η στιγμή της αλήθειας—να ζητήσουμε από τη μηχανή να αναγνωρίσει τους χαρακτήρες και να μας δώσει μια καθαρή συμβολοσειρά. Η χρήση του `RecognizeAsync` διατηρεί το UI ανταποκρινόμενο αν ενσωματώσετε αυτό σε εφαρμογή desktop ή web.

```csharp
// Run OCR and get the plain text result
string plainText = await ocrEngine.RecognizeAsync();
```

Όταν εκτελέσετε το πρόγραμμα, θα πρέπει να δείτε κάτι σαν:

```
OCR complete. Extracted text:
서울시청
```

> **Γιατί async;**  
> Το OCR μπορεί να είναι εντατικό σε CPU. Η ασύγχρονη εκτέλεση αποτρέπει το μπλοκάρισμα του νήματος σας, κάτι που είναι ιδιαίτερα χρήσιμο στο ASP.NET Core όπου η έλλειψη νημάτων είναι πραγματικό πρόβλημα.

## Βήμα 5: Λήψη Λεπτομερούς Αποτελέσματος Αναγνώρισης και Αποθήκευση ως JSON

Μερικές φορές χρειάζεστε περισσότερα από την ακατέργαστη συμβολοσειρά—ίσως θέλετε βαθμολογίες εμπιστοσύνης, περιοριστικά πλαίσια (bounding boxes) ή τα αρχικά δεδομένα εικόνας. Η μέθοδος `RecognizeDetailed` επιστρέφει ένα αντικείμενο `RecognitionResult` που μπορεί να σειριοποιηθεί σε JSON για μεταγενέστερη ανάλυση.

```csharp
// Detailed result includes confidence, coordinates, etc.
RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();

// Convert to nicely indented JSON
string jsonResult = detailedResult.ToJson(indent: true);

// Persist the JSON to disk
File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);
```

Ανοίγοντας το `korean_ocr.json` θα αποκαλύψει μια δομή παρόμοια με:

```json
{
  "Pages": [
    {
      "Text": "서울시청",
      "Confidence": 0.98,
      "Words": [
        {
          "Text": "서울시청",
          "BoundingBox": [12,34,56,78],
          "Confidence": 0.98
        }
      ]
    }
  ]
}
```

> **Πότε να το χρησιμοποιήσετε;**  
> Αν δημιουργείτε ένα ευρετήριο αναζήτησης, οι τιμές εμπιστοσύνης σας επιτρέπουν να φιλτράρετε τα χαμηλής ποιότητας αποτελέσματα. Αν χρειάζεστε να επισημάνετε κείμενο σε UI, τα bounding boxes είναι ο χάρτης σας.

## Βήμα 6: Μετατροπή Εικόνας σε PDF και Εξαγωγή Αναζητήσιμου PDF

Το Aspose κάνει τη μετάβαση από raster σε vector χωρίς κόπο. Ορίζοντας το `OutputFormat` σε `SearchablePdf`, η βιβλιοθήκη ενσωματώνει την αρχική εικόνα και προσθέτει ένα αόρατο στρώμα κειμένου που περιέχει το αποτέλεσμα OCR. Το παραγόμενο PDF μπορεί να αναζητηθεί, να αντιγραφεί και να ευρετηριαστεί όπως οποιοδήποτε εγγενές PDF.

```csharp
using Aspose.OCR.Enums;

// Tell the engine to produce a searchable PDF
ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;

// Save the PDF to the target folder
ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");
```

Ανοίξτε το `korean_searchable.pdf` σε Adobe Reader ή οποιονδήποτε προβολέα PDF, πατήστε **Ctrl+F**, πληκτρολογήστε μια κορεατική λέξη και δείτε το να μεταβαίνει στην ακριβή θέση στη σελίδα. Αυτή είναι η δύναμη ενός αναζητήσιμου PDF.

> **Επιπλέον συμβουλή:** Αν χρειάζεστε μόνο ένα οπτικό PDF χωρίς το κρυφό στρώμα κειμένου, αλλάξτε το `OutputFormat` σε `Pdf`.

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω είναι το πλήρες πρόγραμμα—αντιγράψτε, επικολλήστε, αντικαταστήστε το `YOUR_DIRECTORY` με μια πραγματική διαδρομή, και πατήστε **F5**.

```csharp
using System;
using System.IO;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

class OcrDemo
{
    static async Task Main()
    {
        // Step 1: Create the OCR engine and enable GPU with offline resources
        var ocrEngine = new OcrEngine();
        ocrEngine.Configuration.EnableGpu = true;
        ocrEngine.Configuration.AutomaticResourceDownload = false;
        ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";

        // Step 2: Select the language and apply preprocessing filters
        ocrEngine.Configuration.Language = Language.Korean;
        ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                                    PreprocessFilter.Denoise;

        // Step 3: Load the image to be recognized from a file stream
        using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");
        ocrEngine.Image = ImageStream.FromStream(imageStream);

        // Step 4: Run OCR asynchronously and obtain the plain text result
        string plainText = await ocrEngine.RecognizeAsync();

        // Step 5: Get a detailed recognition result, convert it to JSON, and save it
        RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();
        string jsonResult = detailedResult.ToJson(indent: true);
        File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);

        // Step 6: Export the recognized page as a searchable PDF
        ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
        ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");

        Console.WriteLine("OCR complete. Extracted text:");
        Console.WriteLine(plainText);
    }
}
```

### Αναμενόμενη Εξαγωγή Κονσόλας

```
OCR complete. Extracted text:
서울시청
```

Και θα βρείτε τρία νέα αρχεία δίπλα στην πηγαία εικόνα σας:

- `korean_ocr.json` – πλήρη δεδομένα αναγνώρισης.  
- `korean_searchable.pdf` – PDF που μπορείτε να αναζητήσετε.  
- (προαιρετικό) τυχόν ενδιάμεσα αρχεία καταγραφής που επιλέγετε να προσθέσετε.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

**Τι γίνεται αν δεν έχω GPU;**  
Ορίστε `EnableGpu = false`; η εναλλακτική χρήση CPU είναι απολύτως επαρκής για μικρές παρτίδες.

**Μπορώ να επεξεργαστώ πολλές εικόνες σε μία εκτέλεση;**  
Απόλυτα. Τυλίξτε τη βασική λογική σε έναν βρόχο `foreach (var file in Directory.GetFiles(...))` και επανα‑αναθέστε το `ocrEngine.Image` σε κάθε επανάληψη.

**Πώς να διαχειριστώ άλλες γλώσσες μαζί με την κορεατική;**  
Το Aspose.OCR επιτρέπει να ορίσετε `Language = Language.AutoDetect` ή να συνδυάσετε γλώσσες με τον τελεστή bitwise OR (π.χ., `Language.Korean | Language.English`).

**Τι γίνεται αν η εμπιστοσύνη του OCR είναι χαμηλή;**  
Εξετάστε το `detailedResult.Pages[0].Words` και φιλτράρετε τις καταχωρήσεις με `Confidence < 0.7`. Μπορείτε επίσης να προσαρμόσετε τα φίλτρα προεπεξεργασίας—δοκιμάστε να προσθέσετε το `PreprocessFilter.ContrastEnhancement`.

## Συμπεράσματα

Μόλις είδατε πώς να εκτελέσετε **Korean Language OCR** από την αρχή μέχρι το τέλος, από το **φόρτωμα εικόνας από ροή** μέχρι το **εξαγωγή απλού κειμένου**, στη συνέχεια **μετατροπή εικόνας σε PDF** και τέλος **εξαγωγή αναζητήσιμου PDF**. Η προσέγγιση είναι μοντέλο, ώστε να μπορείτε να αντικαταστήσετε την πηγή εικόνας, να αλλάξετε τη μορφή εξόδου ή να ενσωματώσετε το JSON σε οποιοδήποτε επόμενο pipeline.

Τι ακολουθεί

## Σχετικά Tutorials

- [Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Αναγνώριση κειμένου εικόνας με Aspose OCR για πολλαπλές γλώσσες](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Εξαγωγή Κειμένου από Εικόνα – Βελτιστοποίηση OCR με Aspose.OCR για .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}