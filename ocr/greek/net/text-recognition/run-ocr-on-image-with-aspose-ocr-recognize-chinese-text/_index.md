---
category: general
date: 2026-03-04
description: Εκτελέστε OCR σε εικόνα χρησιμοποιώντας το Aspose OCR σε C#. Μάθετε πώς
  να αναγνωρίζετε κινέζικο κείμενο, να εξάγετε κείμενο από εικόνα και να φορτώνετε
  την εικόνα για OCR σε λίγα μόνο βήματα.
draft: false
keywords:
- run OCR on image
- recognize chinese text
- extract text from image
- load image for OCR
- recognize simplified chinese
language: el
og_description: Εκτελέστε OCR σε εικόνα με το Aspose OCR σε C#. Αυτός ο οδηγός σας
  δείχνει πώς να αναγνωρίζετε κινεζικό κείμενο, να εξάγετε κείμενο από εικόνα και
  να φορτώνετε εικόνα για OCR αποδοτικά.
og_title: Εκτέλεση OCR σε εικόνα με το Aspose OCR – Γρήγορη αναγνώριση κινεζικού κειμένου
tags:
- Aspose OCR
- C#
- Chinese OCR
title: Εκτέλεση OCR σε εικόνα με το Aspose OCR – Αναγνώριση Κινέζικου κειμένου
url: /el/net/text-recognition/run-ocr-on-image-with-aspose-ocr-recognize-chinese-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε Εικόνα – Πλήρης Οδηγός C# για Κινεζικό Κείμενο

Έχετε ποτέ χρειαστεί να **run OCR on image** αρχεία αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη θα διαχειριστεί τα Απλοποιημένα Κινεζικά χωρίς προβλήματα; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν εμπόδια όταν προσπαθούν να **recognize Chinese text** και καταλήγουν να τσακίζουν τα μαλλιά τους λόγω προβλημάτων κωδικοποίησης.

Σε αυτόν τον οδηγό θα κόψουμε το θόρυβο και θα σας δείξουμε, βήμα‑βήμα, πώς να **run OCR on image** πόρους χρησιμοποιώντας το Aspose OCR, να κατεβάσετε το απαραίτητο μοντέλο γλώσσας μόνο μία φορά, και τελικά να **extract text from image** αρχεία που περιέχουν Απλοποιημένους Κινεζικούς χαρακτήρες. Στο τέλος θα έχετε μια έτοιμη για εκτέλεση εφαρμογή κονσόλας που εκτυπώνει το αναγνωρισμένο κείμενο στην κονσόλα.

> **Τι θα λάβετε:** ένα πλήρες, μεταγλωττιζόμενο πρόγραμμα C#, εξηγήσεις του *why* κάθε γραμμής, και συμβουλές για την αντιμετώπιση κοινών παγίδων όπως ελλιπείς πόροι ή λανθασμένες μορφές εικόνας.

## Τι Θα Χρειαστείτε

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε εγκαταστήσει τις παρακάτω προαπαιτήσεις στο μηχάνημα ανάπτυξής σας:

| Προαπαιτούμενο | Γιατί είναι σημαντικό |
|----------------|------------------------|
| .NET 6.0 SDK or later | Παρέχει το runtime και τον μεταγλωττιστή για έργα C#. |
| Visual Studio 2022 (or VS Code with C# extension) | Σας παρέχει IntelliSense και εύκολη αποσφαλμάτωση. |
| Aspose.OCR NuGet package | Η βασική βιβλιοθήκη που ενισχύει τις δυνατότητες OCR. |
| An image containing Simplified Chinese characters (e.g., `chinese_sample.png`) | Η πηγή που θα **load image for OCR**. |

Μπορείτε να κατεβάσετε το πακέτο NuGet με:

```bash
dotnet add package Aspose.OCR
```

Τώρα που η βάση είναι καλυμμένη, ας ξεκινήσουμε τη μηχανή.

## Βήμα 1 – Επιλογή του Μοντέλου Γλώσσας (Recognize Simplified Chinese)

Το Aspose OCR διαχωρίζει τα δεδομένα γλώσσας από τη βασική μηχανή, πράγμα που σημαίνει ότι πρέπει να πείτε στο SDK ποιο μοντέλο χρειάζεστε. Δεδομένου ότι δουλεύουμε με χαρακτήρες της ηπειρωτικής Κίνας, επιλέγουμε το μοντέλο **Simplified Chinese**.

```csharp
using Aspose.OCR;
using Aspose.OCR.ResourceManagement;

// Select the Simplified Chinese language model
LanguageModel languageModel = LanguageModel.ChineseSimplified;
```

*Γιατί είναι σημαντικό:* Η μηχανή OCR χρησιμοποιεί λεξικά ειδικά για τη γλώσσα και σχήματα χαρακτήρων. Η επιλογή του σωστού μοντέλου βελτιώνει δραματικά την ακρίβεια, ειδικά για πυκνά γραπτά όπως τα Κινεζικά.

## Βήμα 2 – Λήψη του Μοντέλου Μία Φορά (Extract Text from Image)

Την πρώτη φορά που εκτελείτε τον κώδικα θα χρειαστεί να κατεβάσετε τα αρχεία μοντέλου από τους διακομιστές της Aspose. Η `ResourceDownloader` το διαχειρίζεται για εσάς. Σε μια παραγωγική εφαρμογή πιθανόν να το κάνετε ασύγχρονα, αλλά για τη σαφήνεια του οδηγού θα μπλοκάρουμε με `.Wait()`.

```csharp
// Initialise the downloader and fetch the model (runs once)
ResourceDownloader resourceDownloader = new ResourceDownloader();
resourceDownloader.DownloadModelAsync(languageModel).Wait();
```

> **Pro tip:** Αποθηκεύστε τους ληφθέντες πόρους σε φάκελο που είναι μέρος του έργου σας (π.χ., `OcrResources`). Με αυτόν τον τρόπο οι επόμενες εκτελέσεις παραλείπουν την κλήση δικτύου, επιταχύνοντας τη διαδικασία.

## Βήμα 3 – Καθορίστε τη Μηχανή στα Τοπικά Σας Πόρους (Load Image for OCR)

Τώρα δημιουργούμε τη μηχανή OCR και της λέμε πού βρίσκονται τα αρχεία μοντέλου. Η `LocalResourceProvider` διαβάζει τα αρχεία από το δίσκο, εξαλείφοντας τυχόν περαιτέρω κίνηση δικτύου.

```csharp
// Create the OCR engine and link it to the local resources folder
OcrEngine ocrEngine = new OcrEngine
{
    ResourceProvider = new LocalResourceProvider(@"YOUR_DIRECTORY/OcrResources")
};
```

Αντικαταστήστε το `YOUR_DIRECTORY` με την απόλυτη ή σχετική διαδρομή που δείχνει στο φάκελο όπου αποθηκεύσατε τα αρχεία μοντέλου.

*Γιατί είναι σημαντικό:* Αν η μηχανή δεν μπορεί να εντοπίσει τους πόρους γλώσσας, θα ρίξει ένα `FileNotFoundException` και δεν θα μπορείτε να **run OCR on image** καθόλου.

## Βήμα 4 – Ορίστε τη Γλώσσα για Αναγνώριση (Recognize Chinese Text)

Ακόμα και αν κατεβάσαμε το μοντέλο Simplified Chinese, πρέπει ακόμη να ενημερώσουμε τη μηχανή ποια γλώσσα θα εφαρμόσει κατά την αναγνώριση.

```csharp
// Tell the engine to use Simplified Chinese for this session
ocrEngine.Language = Language.ChineseSimplified;
```

Αν χρειαστεί ποτέ να αλλάξετε γλώσσες εν κινήσει (π.χ., από Κινεζικά σε Αγγλικά), μπορείτε απλώς να αλλάξετε αυτήν την ιδιότητα πριν καλέσετε το `Recognize`.

## Βήμα 5 – Φορτώστε την Εικόνα και Εκτελέστε OCR (Run OCR on Image)

Αυτή είναι η ουσία του οδηγού: φόρτωση αρχείου εικόνας και εξαγωγή του κειμένου του. Η μέθοδος `ImageInfo.Load` διαβάζει το αρχείο σε μορφή που καταλαβαίνει η μηχανή OCR.

```csharp
// Load the image that contains Chinese characters
var imageInfo = ImageInfo.Load(@"YOUR_DIRECTORY/chinese_sample.png");

// Perform OCR – this is where we actually run OCR on image
OcrResult ocrResult = ocrEngine.Recognize(imageInfo);
```

Αν η εικόνα είναι μεγάλη ή θορυβώδης, σκεφτείτε προεπεξεργασία (π.χ., δυαδικοποίηση) πριν από αυτό το βήμα. Το Aspose OCR προσφέρει επίσης φίλτρα, αλλά αυτό υπερβαίνει το πεδίο του αρχαρίου οδηγού.

## Βήμα 6 – Εξαγωγή του Αναγνωρισμένου Κειμένου (Extract Text from Image)

Τέλος, εκτυπώνουμε το εξαγόμενο κείμενο στην κονσόλα. Σε πραγματικό σενάριο μπορεί να το γράψετε σε βάση δεδομένων, αρχείο ή να το περάσετε σε άλλη υπηρεσία.

```csharp
// Show the OCR result in the console
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(ocrResult.Text);
```

Η εκτέλεση του προγράμματος θα πρέπει να εμφανίσει κάτι όπως:

```
=== Recognized Text ===
你好，世界！这是一个测试。
```

Αυτό ήταν—το πρώτο σας **run OCR on image** που **recognize Chinese text**.

## Πλήρες, Έτοιμο‑για‑Εκτέλεση Παράδειγμα

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε ένα νέο έργο κονσόλας (`dotnet new console`). Θυμηθείτε να αντικαταστήσετε το `YOUR_DIRECTORY` με την πραγματική διαδρομή στο μηχάνημά σας.

```csharp
// ------------------------------------------------------------
// Complete C# example: Run OCR on Image and Recognize Simplified Chinese
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.ResourceManagement;

class Program
{
    static void Main()
    {
        // 1️⃣ Choose the language model (Simplified Chinese)
        LanguageModel languageModel = LanguageModel.ChineseSimplified;

        // 2️⃣ Download the model (only the first time)
        var downloader = new ResourceDownloader();
        downloader.DownloadModelAsync(languageModel).Wait();   // Blocking for tutorial simplicity

        // 3️⃣ Initialise OCR engine with local resources folder
        var ocrEngine = new OcrEngine
        {
            ResourceProvider = new LocalResourceProvider(@"YOUR_DIRECTORY/OcrResources")
        };

        // 4️⃣ Set the language for this session
        ocrEngine.Language = Language.ChineseSimplified;

        // 5️⃣ Load the image that contains Chinese text
        var imageInfo = ImageInfo.Load(@"YOUR_DIRECTORY/chinese_sample.png");

        // 6️⃣ Run OCR on the image and capture the result
        OcrResult result = ocrEngine.Recognize(imageInfo);

        // 7️⃣ Output the extracted text
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);
    }
}
```

> **Expected output:** Η κονσόλα εκτυπώνει τους Κινεζικούς χαρακτήρες που βρέθηκαν στο `chinese_sample.png`. Αν η εικόνα είναι καθαρή, η ακρίβεια συχνά υπερβαίνει το 95 %.

## Συνηθισμένα Προβλήματα & Πώς να τα Αποφύγετε

| Σύμπτωμα | Πιθανή Αιτία | Διόρθωση |
|----------|--------------|----------|
| `FileNotFoundException` κατά την εκκίνηση | Λάθος διαδρομή φακέλου πόρων | Ελέγξτε ξανά τη διαδρομή στο `LocalResourceProvider`. Χρησιμοποιήστε το `Path.Combine` για ασφάλεια μεταξύ πλατφορμών. |
| Κενή έξοδος (`ocrResult.Text` κενό) | Η εικόνα είναι πολύ θορυβώδης ή σε μη υποστηριζόμενη μορφή | Μετατρέψτε την εικόνα σε PNG υψηλής αντίθεσης, ή χρησιμοποιήστε το `ocrEngine.PreprocessImage(imageInfo)` πριν το `Recognize`. |
| Exception: `Unsupported language` | Το μοντέλο γλώσσας δεν έχει ληφθεί | Εκτελέστε ξανά το βήμα λήψης, ή διαγράψτε το κατεστραμμένο φάκελο και αφήστε το να κατεβάσει ξανά. |
| Αργή πρώτη εκτέλεση | Λήψη μοντέλου μέσω αργής σύνδεσης | Αποθηκεύστε το μοντέλο σε κοινόχρηστη τοποθεσία δικτύου ή ενσωματώστε το εκ των προτέρων με τον εγκαταστάτη σας. |

## Επέκταση της Λύσης (Επόμενα Βήματα)

- **Batch processing:** Επανάληψη πάνω σε έναν φάκελο εικόνων, καλώντας την ίδια μέθοδο `Recognize` για κάθε αρχείο. Αυτό σας επιτρέπει να **extract text from image** συλλογές χωρίς χειροκίνητη προσπάθεια.  
- **Post‑processing:** Χρησιμοποιήστε κανονικές εκφράσεις για να καθαρίσετε τα υπολείμματα OCR (π.χ., τυχαία σημεία στίξης).  
- **Language detection:** Αν χρειάζεται να διαχειριστείτε πολυγλωσσικά έγγραφα, ελέγξτε το `ocrResult.DetectedLanguage` (διαθέσιμο σε νεότερες εκδόσεις Aspose) και αλλάξτε το `ocrEngine.Language` αναλόγως.  

## Συμπέρασμα

Σας παρουσιάσαμε όλα όσα χρειάζεστε για να **run OCR on image** αρχεία χρησιμοποιώντας το Aspose OCR σε C#. Από την επιλογή του σωστού μοντέλου **recognize simplified Chinese**, μέχρι τη λήψη πόρων, τη ρύθμιση της μηχανής, και τέλος το **extracting text from image**, ο οδηγός σας παρέχει μια αυτόνομη, αντιγραφή‑και‑επικόλληση λύση.  

Τώρα μπορείτε με σιγουριά να **recognize Chinese text** σε οποιοδήποτε PNG ή JPEG περάσετε στη μηχανή, και έχετε μια ισχυρή βάση για επέκταση σε εργασίες batch, υποστήριξη πολλαπλών γλωσσών, ή ενσωμάτωση με downstream pipelines ανάλυσης.

Έχετε ερωτήσεις σχετικά με τη ρύθμιση του OCR ή τη διαχείριση άλλων γραφών; Αφήστε ένα σχόλιο, και καλή προγραμματιστική! 

![Run OCR on image example](image.png "Run OCR on image example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}