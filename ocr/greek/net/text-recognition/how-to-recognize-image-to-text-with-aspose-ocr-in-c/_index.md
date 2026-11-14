---
category: general
date: 2026-11-14
description: Μάθετε πώς να αναγνωρίζετε εικόνα σε κείμενο χρησιμοποιώντας το Aspose
  OCR σε C#. Αυτός ο οδηγός βήμα‑βήμα καλύπτει επίσης πώς να εξάγετε κείμενο από jpg
  και να μετατρέψετε την εικόνα σε κείμενο αποδοτικά.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize image to text
- extract text from jpg
- perform OCR on image
- convert image to text
- recognize text from image
language: el
lastmod: 2026-11-14
og_description: Αναγνωρίστε εικόνα σε κείμενο με το Aspose OCR σε C#. Ακολουθήστε
  αυτό το πλήρες σεμινάριο για να εξάγετε κείμενο από jpg, να εκτελέσετε OCR στην
  εικόνα και να μετατρέψετε την εικόνα σε κείμενο.
og_image_alt: Screenshot of C# code that recognize image to text using Aspose OCR
og_title: Αναγνώριση εικόνας σε κείμενο με Aspose OCR – Οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-11-14'
  description: Learn how to recognize image to text using Aspose OCR in C#. This step‑by‑step
    guide also covers how to extract text from jpg and convert image to text efficiently.
  headline: How to recognize image to text with Aspose OCR in C#
  type: TechArticle
- description: Learn how to recognize image to text using Aspose OCR in C#. This step‑by‑step
    guide also covers how to extract text from jpg and convert image to text efficiently.
  name: How to recognize image to text with Aspose OCR in C#
  steps:
  - name: Large images
    text: Large files increase memory usage and processing time. Resize the image
      to a maximum of 2000 px on the longest side before calling `RecognizeImage`.
  - name: Missing language model
    text: If the required language pack cannot be downloaded (e.g., offline environment),
      the engine throws `IOException`. Wrap the call in a try‑catch block and provide
      a fallback language.
  - name: Asynchronous processing
    text: For UI applications, avoid blocking the UI thread. Wrap the recognition
      call in `Task.Run`.
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Πώς να αναγνωρίσετε εικόνα σε κείμενο με το Aspose OCR σε C#
url: /el/net/text-recognition/how-to-recognize-image-to-text-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αναγνωρίσετε εικόνα σε κείμενο με το Aspose OCR σε C#

Αν χρειάζεστε να αναγνωρίσετε εικόνα σε κείμενο σε μια εφαρμογή .NET, αυτός ο οδηγός δείχνει τα ακριβή βήματα που απαιτούνται. Θα δείτε πώς να εξάγετε κείμενο από αρχεία jpg, να εκτελέσετε OCR σε δεδομένα εικόνας και να μετατρέψετε την εικόνα σε κείμενο με ελάχιστο κώδικα.

Το tutorial καλύπτει τα πάντα, από την εγκατάσταση του πακέτου NuGet Aspose.OCR μέχρι τη ασφαλή διαχείριση του αποτελέσματος OCR. Δεν απαιτούνται εξωτερικές υπηρεσίες και ο κώδικας εκτελείται σε .NET 6 ή νεότερο.

## Εγκατάσταση του πακέτου Aspose OCR

Πριν γράψετε οποιονδήποτε κώδικα, προσθέστε τη βιβλιοθήκη Aspose.OCR στο έργο σας. Το πακέτο περιλαμβάνει όλα τα μοντέλα γλώσσας και κατεβάζει αυτόματα τα απαιτούμενα αρχεία κατά την εκτέλεση.

```bash
dotnet add package Aspose.OCR
```

Η εντολή προσθέτει την πιο πρόσφατη σταθερή έκδοση του **Aspose.OCR** στο `csproj` σας. Αυτό το βήμα εξασφαλίζει ότι μπορείτε να καλέσετε το `OcrEngine` χωρίς χειροκίνητη διαχείριση DLL.

## Δημιουργία και διαμόρφωση της μηχανής OCR

Η δημιουργία της μηχανής OCR είναι η πρώτη προγραμματιστική ενέργεια που πρέπει να κάνετε. Η μηχανή διαχειρίζεται τη φόρτωση εικόνας, την επιλογή γλώσσας και την αναγνώριση.

```csharp
using Aspose.OCR;

// Step 1: Instantiate the OCR engine (required modules are downloaded automatically)
OcrEngine ocrEngine = new OcrEngine();
```

`OcrEngine` είναι η βασική κλάση που εκτελεί το βαρέως φορτίου έργο. Η δημιουργία μιας στιγμής της ενεργοποιεί μια ελαφριά αρχικοποίηση· η βιβλιοθήκη κατεβάζει τα πακέτα γλώσσας μόνο όταν επιλέγετε μια γλώσσα.

## Επιλογή του μοντέλου γλώσσας (εξαγωγή κειμένου από jpg)

Η επιλογή του σωστού μοντέλου γλώσσας επηρεάζει την ακρίβεια. Για κυριλλικό κείμενο, ορίστε `OcrLanguage.Cyrillic`. Την πρώτη φορά που ορίζετε μια γλώσσα που δεν είναι αποθηκευμένη τοπικά, το Aspose κατεβάζει το μοντέλο στο παρασκήνιο.

```csharp
// Step 2: Choose the language model – triggers download if needed
ocrEngine.Language = OcrLanguage.Cyrillic;
```

Αν εργάζεστε με λατινικά σενάρια, αντικαταστήστε το `Cyrillic` με `English` ή άλλη τιμή του enum. Η ίδια διαδρομή κώδικα **εκτελέσετε OCR σε εικόνα** ανεξαρτήτως γλώσσας.

## Αναγνώριση κειμένου από αρχείο JPG (μετατροπή εικόνας σε κείμενο)

Τώρα μπορείτε να τροφοδοτήσετε το μηχάνημα με ένα αρχείο εικόνας. Η μέθοδος `RecognizeImage` δέχεται διαδρομή αρχείου, ροή ή ένα `Bitmap`. Εδώ χρησιμοποιούμε JPEG επειδή είναι κοινή μορφή για σαρωμένα έγγραφα.

```csharp
// Step 3: Recognize text from the image file
OcrResult ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/cyrillic-sample.jpg");
```

Η μέθοδος επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει το ακατέργαστο κείμενο, τις βαθμολογίες εμπιστοσύνης και προαιρετικές πληροφορίες διάταξης. Αυτή η κλήση **αναγνωρίζει κείμενο από εικόνα** σε μία γραμμή.

## Εμφάνιση του αποτελέσματος OCR (εξαγωγή κειμένου από jpg)

Μετά την αναγνώριση, εμφανίστε το ανιχνευμένο κείμενο στην κονσόλα ή περάστε το σε άλλο στοιχείο.

```csharp
// Step 4: Display the recognized text
Console.WriteLine(ocrResult.Text);
```

Η τυπική έξοδος της κονσόλας φαίνεται ως εξής:

```
Пример текста на кириллице
```

Αν η εικόνα δεν περιέχει αναγνώσιμους χαρακτήρες, το `ocrResult.Text` θα είναι κενή συμβολοσειρά. Πάντα ελέγχετε αυτήν την κατάσταση πριν από περαιτέρω επεξεργασία.

## Διαχείριση κοινών περιπτώσεων άκρων

### Μεγάλες εικόνες

Τα μεγάλα αρχεία αυξάνουν τη χρήση μνήμης και τον χρόνο επεξεργασίας. Αλλάξτε το μέγεθος της εικόνας σε μέγιστο 2000 px στην μεγαλύτερη πλευρά πριν καλέσετε το `RecognizeImage`.

```csharp
using System.Drawing;

// Load, resize, then recognize
using (Bitmap original = new Bitmap("YOUR_DIRECTORY/large-sample.jpg"))
{
    int maxDim = 2000;
    int width = original.Width;
    int height = original.Height;

    if (width > maxDim || height > maxDim)
    {
        float scale = Math.Min((float)maxDim / width, (float)maxDim / height);
        int newWidth = (int)(width * scale);
        int newHeight = (int)(height * scale);
        using (Bitmap resized = new Bitmap(original, newWidth, newHeight))
        {
            OcrResult result = ocrEngine.RecognizeImage(resized);
            Console.WriteLine(result.Text);
        }
    }
    else
    {
        OcrResult result = ocrEngine.RecognizeImage(original);
        Console.WriteLine(result.Text);
    }
}
```

### Έλλειψη μοντέλου γλώσσας

Αν το απαιτούμενο πακέτο γλώσσας δεν μπορεί να ληφθεί (π.χ., σε περιβάλλον εκτός σύνδεσης), η μηχανή ρίχνει `IOException`. Τυλίξτε την κλήση σε μπλοκ try‑catch και παρέχετε εναλλακτική γλώσσα.

```csharp
try
{
    ocrEngine.Language = OcrLanguage.Cyrillic;
    OcrResult result = ocrEngine.RecognizeImage("sample.jpg");
    Console.WriteLine(result.Text);
}
catch (IOException ex)
{
    Console.WriteLine($"Language model download failed: {ex.Message}");
    // Fallback to English
    ocrEngine.Language = OcrLanguage.English;
    OcrResult fallback = ocrEngine.RecognizeImage("sample.jpg");
    Console.WriteLine(fallback.Text);
}
```

### Ασύγχρονη επεξεργασία

Για εφαρμογές UI, αποφύγετε το μπλοκάρισμα του νήματος UI. Τυλίξτε την κλήση αναγνώρισης σε `Task.Run`.

```csharp
await Task.Run(() =>
{
    OcrResult asyncResult = ocrEngine.RecognizeImage("sample.jpg");
    Console.WriteLine(asyncResult.Text);
});
```

## Πρακτικές συμβουλές για αξιόπιστο OCR

- **Προεπεξεργασία εικόνων**: Εφαρμόστε μετατροπή σε κλίμακα του γκρι και ενίσχυση αντίθεσης για βελτίωση της ακρίβειας όταν **εκτελέσετε OCR σε εικόνα** με φτωχή φωτισμό.
- **Επιλέξτε τη σωστή γλώσσα**: Πάντα ορίστε το `ocrEngine.Language` πριν από την αναγνώριση. Η προεπιλογή είναι τα Αγγλικά, που οδηγούν σε χαμηλή ακρίβεια για κυριλλικά ή ασιατικά σενάρια.
- **Επικυρώστε την έξοδο**: Χρησιμοποιήστε κανονικές εκφράσεις για να επαληθεύσετε ότι το αναγνωρισμένο κείμενο ταιριάζει με τα αναμενόμενα πρότυπα (π.χ., ημερομηνίες, IDs) πριν το αποθηκεύσετε.
- **Αποθηκεύστε στην κρυφή μνήμη τα πακέτα γλώσσας**: Η πρώτη λήψη μπορεί να διαρκέσει αρκετά δευτερόλεπτα. Αναπτύξτε τα απαιτούμενα πακέτα με την εφαρμογή σας αν χρειάζεστε άμεση εκκίνηση.

## Πλήρες παράδειγμα

Παρακάτω υπάρχει ένα αυτόνομο πρόγραμμα που δείχνει ολόκληρη τη ροή εργασίας—από την εγκατάσταση του πακέτου μέχρι την εμφάνιση του αποτελέσματος OCR.

```csharp
// -----------------------------------------------------------
// Recognize image to text with Aspose OCR – complete example
// -----------------------------------------------------------
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1. Create the OCR engine (modules are downloaded automatically)
        OcrEngine ocrEngine = new OcrEngine();

        // 2. Select the language model – triggers download if missing
        ocrEngine.Language = OcrLanguage.Cyrillic;

        // 3. Recognize text from a JPG file (convert image to text)
        OcrResult ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/cyrillic-sample.jpg");

        // 4. Output the recognized string (extract text from jpg)
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Αναμενόμενη έξοδος κονσόλας**

```
Recognized text:
Пример текста на кириллице
```

Η εκτέλεση του προγράμματος με διαφορετική εικόνα (π.χ., ένα αγγλικό τιμολόγιο) απαιτεί μόνο την αλλαγή του enum `Language` και της διαδρομής αρχείου. Ο ίδιος κώδικας **αναγνωρίζει κείμενο από εικόνα** χωρίς τροποποίηση.

## Συμπέρασμα

Τώρα ξέρετε πώς να αναγνωρίζετε εικόνα σε κείμενο με το Aspose OCR σε C#. Το tutorial κάλυψε την εγκατάσταση της βιβλιοθήκης, τη δημιουργία και διαμόρφωση της μηχανής OCR, τη μετατροπή εικόνας σε κείμενο και τη διαχείριση τυπικών περιπτώσεων άκρων. Με αυτή τη βάση μπορείτε να **εξάγετε κείμενο από jpg**, **εκτελέσετε OCR σε εικόνα** δεδομένων οποιουδήποτε μεγέθους και να ενσωματώσετε το αποτέλεσμα σε μεγαλύτερες ροές εργασίας .NET.

Στη συνέχεια, εξερευνήστε προχωρημένα χαρακτηριστικά όπως:

- **OCR πολλαπλών σελίδων PDF** (χρησιμοποιήστε `PdfInput` αντί για JPG)
- **Προσαρμοσμένη λευκή λίστα χαρακτήρων** για βελτίωση της ακρίβειας των αριθμητικών κωδίκων
- **Αποθήκευση αποτελεσμάτων OCR ως PDF με δυνατότητα αναζήτησης** με `OcrEngine.Save`.

Πειραματιστείτε με διαφορετικά μοντέλα γλώσσας και τεχνικές προεπεξεργασίας εικόνας για να επιτύχετε το καλύτερο δυνατό ποσοστό αναγνώρισης για τον συγκεκριμένο τομέα σας. Καλή προγραμματιστική!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [αναγνωρίστε κείμενο από εικόνα σε C# – βήμα‑βήμα οδηγός Aspose OCR](/ocr/english/net/text-recognition/recognize-text-from-image-in-c-step-by-step-aspose-ocr-guide/)
- [αναγνωρίστε κείμενο από εικόνα με Aspose OCR – Πλήρης οδηγός C# Async](/ocr/english/net/text-recognition/recognize-text-from-image-with-aspose-ocr-complete-c-async-g/)
- [αναγνωρίστε κείμενο από εικόνα σε C# – Πλήρες tutorial Aspose OCR](/ocr/english/net/text-recognition/recognize-text-from-image-in-c-complete-aspose-ocr-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}