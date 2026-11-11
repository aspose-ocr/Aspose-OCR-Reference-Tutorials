---
category: general
date: 2026-08-12
description: Αναγνωρίστε κείμενο από εικόνα χρησιμοποιώντας το Aspose OCR για C#.
  Μάθετε πώς να εξάγετε κείμενο από PNG, να μετατρέψετε την εικόνα σε κείμενο και
  να διαχειριστείτε τη κυριλλική γλώσσα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from image
- extract text from png
- convert image to text
- c# image ocr
- aspose ocr c#
language: el
lastmod: 2026-08-12
og_description: Αναγνωρίστε κείμενο από εικόνα με Aspose OCR σε C#. Αυτός ο οδηγός
  σας δείχνει πώς να εξάγετε κείμενο από PNG, να μετατρέψετε την εικόνα σε κείμενο
  και να εργαστείτε με τη κυριλλική γλώσσα.
og_image_alt: Diagram showing the OCR processing flow from image file to recognized
  text output
og_title: Αναγνώριση κειμένου από εικόνα σε C# – πλήρες σεμινάριο Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: recognize text from image using Aspose OCR for C#. Learn how to extract
    text from PNG, convert image to text, and handle Cyrillic language.
  headline: recognize text from image in C# – step‑by‑step Aspose OCR guide
  type: TechArticle
- description: recognize text from image using Aspose OCR for C#. Learn how to extract
    text from PNG, convert image to text, and handle Cyrillic language.
  name: recognize text from image in C# – step‑by‑step Aspose OCR guide
  steps:
  - name: Expected console output
    text: '``` === Recognized Text === Привет мир! Это пример текста на кириллице.
      ```'
  - name: Recognize text from JPEG or BMP
    text: Replace the PNG file path with a JPEG or BMP file; the same `engine.Image`
      assignment works because Aspose.OCR auto‑detects the format.
  - name: Extract text from multiple pages
    text: 'If you need to **extract text from png** files that represent scanned pages,
      loop over the file list and concatenate the results:'
  - name: Convert image to text in an ASP.NET API
    text: 'Expose the OCR logic through a controller action:'
  type: HowTo
tags:
- Aspose OCR
- C#
- OCR
- Image processing
title: Αναγνώριση κειμένου από εικόνα σε C# – βήμα‑βήμα οδηγός Aspose OCR
url: /el/net/text-recognition/recognize-text-from-image-in-c-step-by-step-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση κειμένου από εικόνα σε C# – βήμα‑βήμα οδηγός Aspose OCR

Αν χρειάζεστε **αναγνώριση κειμένου από εικόνα** σε μια εφαρμογή .NET, αυτό το tutorial σας παρέχει μια πλήρη, έτοιμη προς εκτέλεση λύση. Θα δείτε πώς να εξάγετε κείμενο από αρχεία PNG, να μετατρέψετε εικόνα σε κείμενο και να διαχειριστείτε κυριλλικούς χαρακτήρες—όλα με τη βιβλιοθήκη Aspose.OCR για C#.

Ο οδηγός καλύπτει όλα όσα χρειάζεστε για να ξεκινήσετε να χρησιμοποιείτε OCR σήμερα: τα απαιτούμενα πακέτα NuGet, τη ρύθμιση γλώσσας, τη φόρτωση εικόνας και τη διαχείριση σφαλμάτων. Στο τέλος θα έχετε ένα πρόγραμμα κονσόλας που εκτυπώνει τη αναγνωρισμένη συμβολοσειρά στην κονσόλα, και θα καταλάβετε πώς να προσαρμόσετε τον κώδικα για άλλες μορφές εικόνας ή γλώσσες.

## Προαπαιτούμενα

- .NET 6 SDK ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.7.2)
- Visual Studio 2022 ή οποιονδήποτε επεξεργαστή C# προτιμάτε
- Πρόσβαση στο Internet την πρώτη φορά που εκτελείτε το πρόγραμμα (Aspose.OCR κατεβάζει αυτόματα τα γλωσσικά modules)
- Μια εικόνα PNG που περιέχει αναγνώσιμο κείμενο (το παράδειγμα χρησιμοποιεί *cyrillic_sample.png*)

> **Συμβουλή:** Κρατήστε τα αρχεία PNG σας κάτω από 2 MB για ταχύτερη επεξεργασία. Μεγαλύτερες εικόνες μπορούν να κλιμακωθούν πριν το OCR για βελτίωση της ακρίβειας.

## Βήμα 1: Εγκατάσταση του πακέτου NuGet Aspose.OCR

Ανοίξτε ένα τερματικό στο φάκελο του έργου σας και εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

Το πακέτο περιλαμβάνει τον πυρήνα του OCR engine και τα προεπιλεγμένα γλωσσικά modules. Όταν ζητάτε μια γλώσσα που δεν υπάρχει τοπικά, το Aspose την κατεβάζει αυτόματα.

## Βήμα 2: Δημιουργία του OCR engine και επιλογή της γλώσσας

Το OCR engine είναι το κεντρικό αντικείμενο που εκτελεί τη μετατροπή από εικόνα σε κείμενο. Για κυριλλικό κείμενο ορίζετε την ιδιότητα `Language` σε `Language.Cyrillic`. Η ίδια ιδιότητα λειτουργεί για άλλες γλώσσες όπως `Language.English`.

```csharp
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 2.1: Instantiate the OCR engine
        OcrEngine engine = new OcrEngine();

        // Step 2.2: Choose the language module – Cyrillic in this example
        engine.Language = Language.Cyrillic;
```

**Γιατί είναι σημαντικό:** Η επιλογή της σωστής γλώσσας βελτιώνει την αναγνώριση χαρακτήρων επειδή το engine φορτώνει λεξικά και γραμματοσειρές ειδικές για τη γλώσσα. Αν παραλείψετε αυτό το βήμα, το engine επιστρέφει στην αγγλική και οι κυριλλικοί χαρακτήρες γίνονται ακατανόητοι.

## Βήμα 3: Φόρτωση της εικόνας που θέλετε να επεξεργαστείτε

Το Aspose.OCR υποστηρίζει πολλές μορφές εικόνας, αλλά το PNG είναι μια κοινή ακαταστροφική επιλογή που διατηρεί τις άκρες του κειμένου. Χρησιμοποιήστε `ImageStream.FromFile` για να διαβάσετε το αρχείο στο engine.

```csharp
        // Step 3: Load the PNG image that contains the text
        engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/cyrillic_sample.png");
```

Αντικαταστήστε το `YOUR_DIRECTORY` με την πραγματική διαδρομή προς το αρχείο PNG σας. Αν χρειάζεστε **εξαγωγή κειμένου από png** αρχεία που βρίσκονται σε διαφορετικό φάκελο, απλώς προσαρμόστε τη διαδρομή ανάλογα.

## Βήμα 4: Εκτέλεση της λειτουργίας OCR

Η κλήση του `engine.Recognize()` εκτελεί την αλυσίδα OCR και επιστρέφει μια απλή συμβολοσειρά. Αυτό είναι ο πυρήνας της λειτουργίας **μετατροπής εικόνας σε κείμενο**.

```csharp
        // Step 4: Run OCR and get the recognized string
        string recognizedText = engine.Recognize();
```

Η μέθοδος ρίχνει εξαίρεση εάν η εικόνα δεν μπορεί να φορτωθεί ή εάν το γλωσσικό module αποτύχει να κατέβει. Τυλίξτε την κλήση σε μπλοκ try‑catch για κώδικα παραγωγής.

## Βήμα 5: Εμφάνιση ή αποθήκευση του αναγνωρισμένου αποτελέσματος

Για μια γρήγορη επίδειξη μπορείτε να γράψετε το αποτέλεσμα στην κονσόλα. Σε πραγματικές εφαρμογές μπορεί να το αποθηκεύσετε σε βάση δεδομένων, σε αρχείο κειμένου ή να το περάσετε σε άλλη υπηρεσία.

```csharp
        // Step 5: Output the recognized text
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
}
```

### Αναμενόμενη έξοδος κονσόλας

```
=== Recognized Text ===
Привет мир! Это пример текста на кириллице.
```

Αν η εικόνα περιέχει αγγλικό κείμενο, η έξοδος θα είναι η αντίστοιχη αγγλική πρόταση. Ο ίδιος κώδικας λειτουργεί για εργασίες **c# image ocr** σε πολλές γλώσσες.

## Πλήρης κώδικας – έτοιμος για αντιγραφή

Παρακάτω βρίσκεται το πλήρες πρόγραμμα, συμπεριλαμβανομένης της οδηγίας `using` και όλων των βημάτων σε ένα μόνο αρχείο. Αντιγράψτε το στο `Program.cs` και εκτελέστε `dotnet run`.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        try
        {
            // Create an OCR engine instance
            OcrEngine engine = new OcrEngine();

            // Select the Cyrillic language module (downloaded automatically if missing)
            engine.Language = Language.Cyrillic;

            // Load the image that contains Cyrillic text
            engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/cyrillic_sample.png");

            // Perform the OCR recognition
            string recognizedText = engine.Recognize();

            // Display the recognized text
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"OCR failed: {ex.Message}");
        }
    }
}
```

## Διαχείριση κοινών παραλλαγών

### Αναγνώριση κειμένου από JPEG ή BMP

Αντικαταστήστε τη διαδρομή του αρχείου PNG με ένα αρχείο JPEG ή BMP· η ίδια ανάθεση `engine.Image` λειτουργεί επειδή το Aspose.OCR ανιχνεύει αυτόματα τη μορφή.

```csharp
engine.Image = ImageStream.FromFile("photo.jpg");
```

### Εξαγωγή κειμένου από πολλαπλές σελίδες

Αν χρειάζεστε **εξαγωγή κειμένου από png** αρχεία που αντιπροσωπεύουν σαρωμένες σελίδες, κάντε επανάληψη στη λίστα αρχείων και συνενώστε τα αποτελέσματα:

```csharp
string[] files = Directory.GetFiles("scans", "*.png");
var allText = new StringBuilder();

foreach (var file in files)
{
    engine.Image = ImageStream.FromFile(file);
    allText.AppendLine(engine.Recognize());
}
Console.WriteLine(allText.ToString());
```

### Μετατροπή εικόνας σε κείμενο σε ASP.NET API

Αποκτήστε τη λογική OCR μέσω μιας ενέργειας ελεγκτή:

```csharp
[HttpPost("api/ocr")]
public async Task<IActionResult> Ocr(IFormFile image)
{
    using var stream = image.OpenReadStream();
    OcrEngine engine = new OcrEngine { Language = Language.English };
    engine.Image = ImageStream.FromStream(stream);
    string text = engine.Recognize();
    return Ok(new { text });
}
```

Αυτό δείχνει **c# image ocr** μέσα σε μια υπηρεσία web, επιτρέποντας στους πελάτες να ανεβάσουν οποιαδήποτε raster εικόνα και να λάβουν το εξαγόμενο κείμενο ως JSON.

## Συμβουλές απόδοσης και ειδικές περιπτώσεις

- **Ποιότητα εικόνας:** Η ακρίβεια του OCR μειώνεται απότομα όταν η εικόνα είναι θολή ή έχει χαμηλή αντίθεση. Χρησιμοποιήστε προεπεξεργασία εικόνας (π.χ., ενίσχυση, δυαδικοποίηση) πριν τη δώσετε στο engine.
- **Μεγάλα αρχεία:** Για εικόνες μεγαλύτερες από 5 MP, αλλάξτε το μέγεθός τους σε μέγιστο 2000 px στην μεγαλύτερη πλευρά. Αυτό μειώνει τη χρήση μνήμης χωρίς να επηρεάζει την αναγνώριση.
- **Fallback γλώσσας:** Εάν ορίσετε μια γλώσσα που δεν υποστηρίζεται, το engine επιστρέφει στην αγγλική. Πάντα επαληθεύετε το `engine.Language` μετά την αρχικοποίηση εάν φορτώνετε γλωσσικά modules δυναμικά.
- **Ασφάλεια νήματος:** Οι παρουσίες `OcrEngine` δεν είναι thread‑safe. Δημιουργήστε ένα νέο engine ανά αίτημα σε πολυνηματικά περιβάλλοντα (π.χ., ASP.NET Core).

## Συμπέρασμα

Τώρα ξέρετε πώς να **αναγνωρίζετε κείμενο από εικόνα** σε C# χρησιμοποιώντας το Aspose.OCR. Το tutorial σας οδήγησε στη εγκατάσταση του πακέτου, τη ρύθμιση της γλώσσας, τη φόρτωση ενός PNG, την εκτέλεση OCR και τη διαχείριση του αποτελέσματος. Με αυτά τα δομικά στοιχεία μπορείτε επίσης να **εξάγετε κείμενο από png**, **μετατρέψετε εικόνα σε κείμενο**, και να δημιουργήσετε αξιόπιστες λύσεις **c# image ocr** για επιτραπέζιες, web ή cloud εφαρμογές.

Στη συνέχεια, εξερευνήστε άλλα γλωσσικά modules (π.χ., `Language.Spanish`) ή ενσωματώστε τα αποτελέσματα OCR με βιβλιοθήκες επεξεργασίας φυσικής γλώσσας. Για πιο προχωρημένη βελτιστοποίηση απόδοσης, διαβάστε την τεκμηρίωση του Aspose.OCR σχετικά με την προεπεξεργασία εικόνας και τα προσαρμοσμένα λεξικά.

Καλή προγραμματιστική!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετικούς θεματικούς τομείς που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Εξαγωγή κειμένου από εικόνα – Βελτιστοποίηση OCR με Aspose.OCR για .NET](/ocr/english/net/ocr-optimization/)
- [Πώς να εξάγετε κείμενο από εικόνα χρησιμοποιώντας Aspose.OCR για .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}