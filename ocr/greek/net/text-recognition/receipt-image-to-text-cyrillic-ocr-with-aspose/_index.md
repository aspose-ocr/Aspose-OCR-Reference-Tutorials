---
category: general
date: 2026-04-01
description: Μάθετε πώς να μετατρέπετε μια εικόνα απόδειξης σε κείμενο χρησιμοποιώντας
  το Aspose OCR. Αυτός ο οδηγός δείχνει πώς να εξάγετε κυριλλικό κείμενο, να φορτώσετε
  την εικόνα για OCR και να αναγνωρίζετε αποτελεσματικά τους κυριλλικούς χαρακτήρες.
draft: false
keywords:
- receipt image to text
- extract cyrillic text
- load image for ocr
- recognize cyrillic characters
- create OCR engine
language: el
og_description: Μετατρέψτε μια εικόνα από απόδειξη σε κείμενο με το Aspose OCR. Μάθετε
  πώς να εξάγετε κυριλλικό κείμενο, να φορτώνετε εικόνα για OCR και να αναγνωρίζετε
  κυριλλικούς χαρακτήρες σε C#.
og_title: εικόνα απόδειξης σε κείμενο – OCR κυριλλικού με Aspose
tags:
- OCR
- C#
- Aspose
- Cyrillic
title: εικόνα απόδειξης σε κείμενο – Κυριλλικό OCR με Aspose
url: /el/net/text-recognition/receipt-image-to-text-cyrillic-ocr-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# εικόνα απόδειξης σε κείμενο – Cyrillic OCR with Aspose

Κάποτε χρειάστηκε να μετατρέψετε μια **receipt image to text** αλλά όλα τα γράμματα είναι Κυριλλικά; Δεν είστε ο μόνος που το σκέφτεται. Σε πολλές εφαρμογές λιανικής ή λογιστικής, οι αποδείξεις εμφανίζονται στα ρωσικά, βουλγαρικά ή σερβικά αλφάβητα, και εσείς θέλετε ένα καθαρό, αναζητήσιμο κείμενο.  

Σε αυτό το tutorial θα σας δείξουμε ακριβώς πώς να **εξάγετε Κυριλλικό κείμενο** από μια φωτογραφία απόδειξης, **φορτώσετε εικόνα για OCR**, και **αναγνωρίσετε Κυριλλικούς χαρακτήρες** χρησιμοποιώντας τη βιβλιοθήκη Aspose OCR. Στο τέλος θα έχετε ένα έτοιμο πρόγραμμα C# που γράφει το αποτέλεσμα του OCR σε αρχείο `.txt`.

## What You’ll Need

- **.NET 6** (ή οποιαδήποτε πρόσφατη έκδοση .NET) – ο κώδικας λειτουργεί επίσης σε .NET Framework 4.7+.  
- **Aspose.OCR for .NET** πακέτο NuGet – `Install-Package Aspose.OCR`.  
- Ένα δείγμα εικόνας απόδειξης που περιέχει Κυριλλικό κείμενο (π.χ., `cyrillic_receipt.jpg`).  
- Περιβάλλον ανάπτυξης – Visual Studio, VS Code ή Rider αρκούν.  

Δεν απαιτούνται πρόσθετες εγγενείς εξαρτήσεις· το Aspose παρέχει τα μοντέλα γλώσσας και διαχειρίζεται τη βαριά δουλειά εσωτερικά.

## receipt image to text – Setting up the OCR Engine

Το πρώτο βήμα είναι να **δημιουργήσετε ένα OCR engine** και να του πείτε ποια γλώσσα σας ενδιαφέρει. Το Aspose το κάνει αυτό πολύ εύκολα:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;   // language and resource handling
using System.Drawing;      // Image class
using System.IO;

class CyrillicDemo
{
    static void Main()
    {
        // Step 1: Instantiate the OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Tell Aspose we want Cyrillic support
        ocrEngine.Language = Language.Cyrillic;

        // Optional: Pre‑load the model if you’ll run offline later
        // ResourceManager.Preload(Language.Cyrillic);
```

> **Pro tip:** Η προφόρτωση του μοντέλου αποφεύγει μια κλήση δικτύου την πρώτη φορά που τρέχετε το πρόγραμμα, κάτι που είναι χρήσιμο για επιτραπέζιες ή ενσωματωμένες εφαρμογές.

## How to extract Cyrillic text – Loading the receipt image

Τώρα που το engine είναι έτοιμο, πρέπει να **φορτώσετε την εικόνα για OCR**. Η κλάση `System.Drawing.Image` λειτουργεί τέλεια για τις περισσότερες μορφές bitmap.

```csharp
        // Step 3: Point to your receipt image
        string imagePath = @"YOUR_DIRECTORY\cyrillic_receipt.jpg";

        // Step 4: Load the image inside a using block (ensures disposal)
        using (var image = Image.FromFile(imagePath))
        {
            // Step 5: Run the OCR process
            var recognitionResult = ocrEngine.Recognize(image);
```

Αν το αρχείο δεν βρεθεί, το `Image.FromFile` ρίχνει `FileNotFoundException`. Στην παραγωγική έκδοση ίσως θέλετε να τυλίξετε όλο το κομμάτι σε μπλοκ `try…catch`.

## Recognize Cyrillic characters – Getting the text out

Το αντικείμενο `recognitionResult` περιέχει το ακατέργαστο κείμενο, τους δείκτες εμπιστοσύνης, και ακόμη και τα πλαίσια οριοθέτησης αν τα χρειαστείτε αργότερα. Για μια απλή μετατροπή “receipt image to text” αρκεί να γράψετε την ιδιότητα `Text` σε αρχείο:

```csharp
            // Step 6: Write the extracted text to a .txt file
            string outputPath = @"YOUR_DIRECTORY\cyrillic.txt";
            File.WriteAllText(outputPath, recognitionResult.Text);

            // Quick verification: print to console
            Console.WriteLine("OCR completed. Extracted text:");
            Console.WriteLine(recognitionResult.Text);
        }
    }
}
```

Όταν τρέξετε το πρόγραμμα, θα δείτε κάτι σαν:

```
OCR completed. Extracted text:
СЧЕТ № 12345
Дата: 01/04/2026
Товар      Кол-во   Цена
Хлеб       2        30,00
Молоко     1        45,00
Итого:               105,00
```

Αυτό είναι το **receipt image to text** αποτέλεσμα που ζητούσατε.

![receipt image to text example](receipt-ocr-example.png "Example of a receipt image being converted to text")

*Image alt text: μετατροπή εικόνας απόδειξης σε κείμενο με εξαγόμενους Κυριλλικούς χαρακτήρες από το Aspose OCR.*

## Edge Cases & Common Questions

### What if the language model isn’t downloaded yet?

Το Aspose κατεβάζει αυτόματα το απαιτούμενο μοντέλο την πρώτη φορά που ορίζετε `ocrEngine.Language = Language.Cyrillic;`. Αν η μηχανή δεν έχει πρόσβαση στο internet, το προαιρετικό βήμα προφόρτωσης θα αποτύχει. Σε αυτή την περίπτωση, είτε παρέχετε το μοντέλο χειροκίνητα (δείτε την τεκμηρίωση του Aspose) είτε εξασφαλίζετε ότι η συσκευή μπορεί να φτάσει στο `download.aspose.com`.

### How do I handle multiple languages in the same receipt?

Μπορείτε να περάσετε μια λίστα χωρισμένη με κόμμα:

```csharp
ocrEngine.Language = Language.Cyrillic | Language.English;
```

Το Aspose θα προσπαθήσει να αναγνωρίσει χαρακτήρες και από τα δύο σύνολα.

### My receipt is blurry – can I improve accuracy?

Το Aspose OCR προσφέρει βασική προεπεξεργασία εικόνας:

```csharp
ocrEngine.ImagePreprocessor = new ImagePreprocessor
{
    Sharpen = true,
    Binarize = true,
    Denoise = true
};
```

Εφαρμόστε το αυτό πριν καλέσετε το `Recognize`.

### What about large batch processing?

Τυλίξτε τον βρόχο αναγνώρισης σε ένα `Parallel.ForEach` και επαναχρησιμοποιήστε το ίδιο αντικείμενο `OcrEngine` (είναι thread‑safe αφού φορτωθεί το μοντέλο). Απλώς θυμηθείτε να κλειδώσετε το engine αν αντιμετωπίσετε προβλήματα ασφαλείας νήματος.

## Full Working Example (All Steps Combined)

Ακολουθεί το πλήρες, έτοιμο‑για‑αντιγραφή πρόγραμμα που ενσωματώνει την προαιρετική προφόρτωση και βασικό χειρισμό σφαλμάτων:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;
using System.Drawing;
using System.IO;

class CyrillicDemo
{
    static void Main()
    {
        try
        {
            // Create OCR engine and select Cyrillic language
            var ocrEngine = new OcrEngine();
            ocrEngine.Language = Language.Cyrillic;

            // Optional: preload model for offline use
            // ResourceManager.Preload(Language.Cyrillic);

            // Path to the receipt image
            string imagePath = @"YOUR_DIRECTORY\cyrillic_receipt.jpg";

            // Verify the file exists
            if (!File.Exists(imagePath))
                throw new FileNotFoundException("Receipt image not found.", imagePath);

            using (var image = Image.FromFile(imagePath))
            {
                // Perform OCR
                var result = ocrEngine.Recognize(image);

                // Output path for extracted text
                string outputPath = @"YOUR_DIRECTORY\cyrillic.txt";
                File.WriteAllText(outputPath, result.Text);

                Console.WriteLine("✅ receipt image to text conversion succeeded.");
                Console.WriteLine("Extracted text saved to: " + outputPath);
                Console.WriteLine("\n--- Extracted Text ---\n");
                Console.WriteLine(result.Text);
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine("❌ An error occurred: " + ex.Message);
        }
    }
}
```

Τρέξτε το πρόγραμμα (`dotnet run` από το φάκελο του έργου) και θα λάβετε ένα αρχείο `.txt` με το **receipt image to text** αποτέλεσμα.

## Conclusion

Τώρα έχετε μια σταθερή, end‑to‑end λύση για τη μετατροπή μιας **receipt image to text**—συγκεκριμένα για Κυριλλικά σενάρια—χρησιμοποιώντας το Aspose OCR. Καλύψαμε πώς να **δημιουργήσετε OCR engine**, **φορτώσετε εικόνα για OCR**, **εξάγετε Κυριλλικό κείμενο**, και **αναγνωρίσετε Κυριλλικούς χαρακτήρες** σε λίγες μόνο γραμμές C#.  

Τι θα κάνετε στη συνέχεια; Δοκιμάστε την επεξεργασία φακέλου αποδείξεων, πειραματιστείτε με το `ImagePreprocessor` για βελτιωμένη ακρίβεια, ή συνδυάστε το αποτέλεσμα OCR με μια βάση δεδομένων για αυτοματοποιημένη λογιστική. Αν χρειαστεί να υποστηρίξετε άλλα αλφάβητα, απλώς αντικαταστήστε `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}