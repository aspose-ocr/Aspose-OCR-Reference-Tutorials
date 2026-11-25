---
category: general
date: 2026-10-11
description: Μάθετε πώς να εκτελείτε OCR σε εικόνα σε C# με το Aspose.OCR, συμπεριλαμβανομένης
  της εγκατάστασης του System.Drawing.Common και της εξαγωγής κειμένου από αρχεία
  JPG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- recognize text from picture
- load image for OCR
- install System.Drawing.Common package
language: el
lastmod: 2026-10-11
og_description: Εκτελέστε OCR σε εικόνα σε C# χρησιμοποιώντας το Aspose.OCR. Αυτός
  ο οδηγός σας δείχνει πώς να εγκαταστήσετε το System.Drawing.Common, να φορτώσετε
  μια εικόνα για OCR και να εξάγετε κείμενο από JPG.
og_image_alt: Screenshot of C# console output displaying recognized text after performing
  OCR on image
og_title: Εκτέλεση OCR σε εικόνα με C# – οδηγός βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on image in C# with Aspose.OCR, including
    installing System.Drawing.Common and extracting text from JPG files.
  headline: How to perform OCR on image in C# using Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: Πώς να εκτελέσετε OCR σε εικόνα σε C# χρησιμοποιώντας το Aspose.OCR
url: /el/net/text-recognition/how-to-perform-ocr-on-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εκτελέσετε OCR σε εικόνα σε C# χρησιμοποιώντας το Aspose.OCR

Αν χρειάζεστε **να εκτελέσετε OCR σε εικόνα** σε αρχεία σε μια εφαρμογή .NET, αυτός ο οδηγός σας δείχνει μια πλήρη λύση. Χρησιμοποιώντας το Aspose.OCR μπορείτε γρήγορα **να αναγνωρίσετε κείμενο από εικόνα** αρχεία όπως JPG και να εμφανίσετε το αποτέλεσμα σε ένα παράθυρο κονσόλας.

Θα μάθετε πώς να:

* **install System.Drawing.Common package** – η βιβλιοθήκη που παρέχει την κλάση `Image`,
* **load image for OCR** – ανάγνωση ενός JPEG ή PNG στη μνήμη,
* ρυθμίστε το μοντέλο γλώσσας,
* **perform OCR on image** και τέλος,
* **extract text from JPG** και εμφάνιση του.

Τα βήματα είναι γραμμένα για .NET 6+, αλλά λειτουργούν επίσης με .NET Framework 4.6.1 ή νεότερο.

---

## Prerequisites

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6 SDK (or .NET Framework 4.6.1+) | Παρέχει το runtime για την κονσόλα C#. |
| Visual Studio 2022 (or any IDE) | Διευκολύνει την προσθήκη πακέτων NuGet και την εκτέλεση του προγράμματος. |
| Internet connection (first run only) | Το Aspose.OCR κατεβάζει αυτόματα το μοντέλο γλώσσας. |
| A sample image containing Cyrillic or Latin text (e.g., `sample_cyrillic.jpg`) | Χρησιμοποιείται για την επίδειξη του **extract text from JPG**. |

---

## Step 1: Install System.Drawing.Common package

Το πακέτο NuGet `System.Drawing.Common` παρέχει την κλάση `Image` που θα **load image for OCR**. Ανοίξτε το Package Manager Console και εκτελέστε:

```powershell
Install-Package System.Drawing.Common
```

> **Pro tip:** Στοχεύστε `net6.0-windows` ή προσθέστε `<UseWindowsForms>true</UseWindowsForms>` στο αρχείο έργου αν αντιμετωπίσετε προειδοποιήσεις ειδικές για πλατφόρμα σε Linux/macOS.

---

## Step 2: Add the Aspose.OCR NuGet package

Το Aspose.OCR περιέχει τη μηχανή OCR και τα μοντέλα γλώσσας. Εγκαταστήστε το με:

```powershell
Install-Package Aspose.OCR
```

Το πακέτο είναι ελαφρύ· τα απαιτούμενα δεδομένα γλώσσας (π.χ. Cyrillic) κατεβάζονται την πρώτη φορά που ορίζετε `OcrEngine.Language`.

---

## Step 3: How to load image for OCR

Η φόρτωση της εικόνας είναι το πρώτο συγκεκριμένο βήμα πριν μπορείτε **perform OCR on image**. Η μέθοδος `Image.FromFile` διαβάζει οποιαδήποτε μορφή υποστηρίζεται από το GDI+, συμπεριλαμβανομένων JPG, PNG, BMP και TIFF.

```csharp
using System.Drawing; // Requires System.Drawing.Common

// Replace the path with the location of your test picture.
string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
Image ocrImage = Image.FromFile(imagePath);
```

*Αν το αρχείο δεν υπάρχει, ρίχνεται `FileNotFoundException` – τυλίξτε την κλήση σε μπλοκ try/catch για κώδικα παραγωγής.*

---

## Step 4: Configure the engine and **perform OCR on image**

Δημιουργήστε μια παρουσία `OcrEngine`, επιλέξτε το μοντέλο γλώσσας, αντιστοιχίστε την φορτωμένη εικόνα και καλέστε `Recognize()`.

```csharp
using Aspose.OCR;

// Step 4: Initialize OCR engine and set language
var ocrEngine = new OcrEngine
{
    // Choose the language you need; Cyrillic is used in this example.
    Language = OcrLanguage.Cyrillic,
    Image = ocrImage
};

// Execute the OCR operation
OcrResult ocrResult = ocrEngine.Recognize();
```

Η μέθοδος `Recognize()` επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει το εξαγόμενο κείμενο, τις βαθμολογίες εμπιστοσύνης και τα πλαίσια οριοθέτησης. Το μοντέλο γλώσσας κατεβαίνει αυτόματα στην πρώτη χρήση, οπότε δεν απαιτούνται επιπλέον αρχεία.

---

## Step 5: **Extract text from JPG** and display it

Τώρα μπορείτε **recognize text from picture** και να εμφανίσετε το αποτέλεσμα. Η ιδιότητα `Text` του `OcrResult` περιέχει το απλό string.

```csharp
// Step 5: Output recognized text
Console.WriteLine("Recognized text:");
Console.WriteLine(ocrResult.Text);
```

### Expected console output

```
Recognized text:
Пример текста на кириллице
```

Αν η πηγαία εικόνα περιέχει αγγλικό κείμενο, η έξοδος θα είναι η αγγλική πρόταση που τοποθετήσατε στην εικόνα.

---

## Edge cases and best‑practice tips

| Situation | Recommendation |
|-----------|----------------|
| **Large images ( > 5 MB )** | Αλλάξτε το μέγεθος της εικόνας σε ≤ 2000 px στην μεγαλύτερη διάσταση πριν το OCR για μείωση της χρήσης μνήμης και βελτίωση της ταχύτητας. |
| **Multiple languages in one picture** | Κλήστε `ocrEngine.AddLanguage(OcrLanguage.English)` εκτός από το Cyrillic, στη συνέχεια ορίστε `ocrEngine.Language = OcrLanguage.Multilingual`. |
| **Low‑contrast scans** | Αυξήστε την αντίθεση με `System.Drawing.Graphics` πριν περάσετε το bitmap στη μηχανή. |
| **Running on Linux/macOS** | Βεβαιωθείτε ότι η εγγενής εξάρτηση `libgdiplus` είναι εγκατεστημένη (`sudo apt-get install -y libgdiplus`). |
| **Repeated OCR calls** | Επαναχρησιμοποιήστε το ίδιο αντικείμενο `OcrEngine` και αντικαταστήστε μόνο το `ocrEngine.Image` για να αποφύγετε επαναλαμβανόμενη φόρτωση του μοντέλου. |

---

## Full, runnable program

Παρακάτω βρίσκεται η πλήρης εφαρμογή κονσόλας που ενσωματώνει όλα τα προηγούμενα βήματα. Αντιγράψτε τον κώδικα σε ένα νέο έργο C# console, αντικαταστήστε τη διαδρομή της εικόνας και τρέξτε το.

```csharp
using System;
using System.Drawing;                 // Install System.Drawing.Common if needed
using Aspose.OCR;                     // NuGet package: Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Install System.Drawing.Common (handled via NuGet)
        // Step 2: Install Aspose.OCR (handled via NuGet)

        // Step 3: Load the image that contains the text to be recognized
        // Replace the placeholder with the actual path to your JPG or PNG file.
        string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
        Image ocrImage;
        try
        {
            ocrImage = Image.FromFile(imagePath);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load image: {ex.Message}");
            return;
        }

        // Step 4: Create the OCR engine and choose the language model
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Cyrillic, // Change to OcrLanguage.English for Latin scripts
            Image = ocrImage
        };

        // Step 5: Perform OCR on the loaded picture
        OcrResult ocrResult = ocrEngine.Recognize();

        // Step 6: Display the extracted text
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Running the program** εκτυπώνει το αναγνωρισμένο κείμενο στην κονσόλα, επιβεβαιώνοντας ότι έχετε ολοκληρώσει με επιτυχία **performed OCR on image** και **extracted text from JPG**.

---

## Conclusion

Τώρα ξέρετε πώς να **perform OCR on image** αρχεία σε C# χρησιμοποιώντας το Aspose.OCR, από την εγκατάσταση του απαιτούμενου **System.Drawing.Common package** μέχρι το **loading image for OCR**, την επιλογή της κατάλληλης γλώσσας και τέλος το **extracting text from JPG**. Αυτό το end‑to‑end παράδειγμα σας παρέχει μια σταθερή βάση για την κατασκευή πιο προχωρημένων pipelines επεξεργασίας εγγράφων, όπως η επεξεργασία φακέλων εικόνων κατά παρτίδες ή η ενσωμάτωση OCR σε web API.

### What’s next?

* Εξερευνήστε το **recognize text from picture** σε PDF μετατρέποντας πρώτα κάθε σελίδα σε εικόνα.
* Πειραματιστείτε με τις ιδιότητες του `OcrEngine` `Resolution`, `Threshold` και `MaxProcessingTime` για να βελτιώσετε την ακρίβεια σε θορυβώδεις σκαναρίσματα.
* Συνδυάστε το αποτέλεσμα του OCR με μια βιβλιοθήκη επεξεργασίας φυσικής γλώσσας για αυτόματη κατηγοριοποίηση του εξαγόμενου περιεχομένου.

Νιώστε ελεύθεροι να προσαρμόσετε τον κώδικα για άλλες μορφές εικόνας, να προσθέσετε διαχείριση σφαλμάτων ή να τον ενσωματώσετε σε μεγαλύτερες εφαρμογές. Καλή προγραμματιστική!

## What Should You Learn Next?

Οι παρακάτω οδηγίες καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Extract Text from Image in C# – Complete Aspose OCR Guide](/ocr/english/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}