---
category: general
date: 2026-10-08
description: Μάθετε πώς να εκτελείτε OCR σε C# χρησιμοποιώντας το Aspose.OCR για να
  εξάγετε κείμενο από αρχεία εικόνας. Αυτός ο οδηγός σας δείχνει πώς να μετατρέπετε
  εικόνα σε κείμενο και να αναγνωρίζετε κείμενο από JPEG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- recognize text from jpeg
- c# ocr example
language: el
lastmod: 2026-10-08
og_description: Πώς να εκτελέσετε OCR σε C# με το Aspose.OCR. Ακολουθήστε αυτόν τον
  οδηγό βήμα‑προς‑βήμα για να εξάγετε κείμενο από αρχεία εικόνας, να μετατρέψετε την
  εικόνα σε κείμενο και να αναγνωρίσετε κείμενο από JPEG.
og_image_alt: Console output displaying Cyrillic text recognized from a JPEG image
  by a C# OCR program
og_title: Πώς να εκτελέσετε OCR σε C# – εξαγωγή κειμένου από εικόνες
schemas:
- author: Aspose
  dateModified: '2026-10-08'
  description: Learn how to perform OCR in C# using Aspose.OCR to extract text from
    image files. This guide shows you how to convert image to text and recognize text
    from JPEG.
  headline: How to perform OCR in C# – extract text from images
  type: TechArticle
- description: Learn how to perform OCR in C# using Aspose.OCR to extract text from
    image files. This guide shows you how to convert image to text and recognize text
    from JPEG.
  name: How to perform OCR in C# – extract text from images
  steps:
  - name: Why each line matters
    text: '* **`OcrEngine ocrEngine = new OcrEngine();`** – Instantiates the engine
      that orchestrates the whole OCR pipeline. * **`ocrEngine.Language = Language.Cyrillic;`**
      – Selects the language model. Choosing the correct language dramatically improves
      accuracy when you **extract text from image** files tha'
  - name: 4.1 Recognizing English or multilingual text
    text: 'Replace the language assignment with the appropriate enum:'
  - name: 4.2 Processing images from a stream instead of a file
    text: 'If your image arrives via an HTTP response or a database blob, use a `MemoryStream`:'
  - name: 4.3 Handling large or low‑resolution images
    text: 'Large images increase memory consumption. You can downscale before OCR:'
  - name: 4.4 Error handling
    text: 'Wrap the recognition call in a try‑catch block to catch network or file‑access
      errors:'
  type: HowTo
tags:
- OCR
- C#
- Aspose.OCR
- Image Processing
title: Πώς να εκτελέσετε OCR σε C# – εξαγωγή κειμένου από εικόνες
url: /el/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εκτελέσετε OCR σε C# – εξαγωγή κειμένου από εικόνες

Αν χρειάζεστε **how to perform OCR** σε μια εφαρμογή .NET, αυτό το tutorial σας παρέχει μια πλήρη, έτοιμη‑για‑εκτέλεση λύση. Χρησιμοποιώντας το Aspose.OCR μπορείτε να **extract text from image** αρχεία, **convert image to text**, και **recognize text from JPEG** με μόνο μερικές γραμμές κώδικα.

Θα δείτε ολόκληρη τη ροή εργασίας—από την εγκατάσταση της βιβλιοθήκης μέχρι την εκτύπωση της αναγνωρισμένης συμβολοσειράς—ώστε να μπορείτε να αντιγράψετε το παράδειγμα στο δικό σας έργο και να αρχίσετε να επεξεργάζεστε εικόνες αμέσως.

## Τι θα μάθετε

* Πώς να ρυθμίσετε ένα έργο C# για εργασίες OCR.  
* Πώς να φορτώσετε ένα JPEG (ή οποιαδήποτε υποστηριζόμενη εικόνα) και να εκτελέσετε την αναγνώριση.  
* Πώς να ανακτήσετε το προκύπτον κείμενο και να το χρησιμοποιήσετε στην εφαρμογή σας.  

Η μόνη προαπαιτούμενη προϋπόθεση είναι ένα πρόσφατο .NET SDK (≥ .NET 6) και σύνδεση στο διαδίκτυο για τη λήψη του πρώτου μοντέλου γλώσσας.

## Βήμα 1: Ρύθμιση του έργου και εγκατάσταση του Aspose.OCR

1. Δημιουργήστε ένα νέο έργο κονσόλας:

   ```bash
   dotnet new console -n OcrDemo
   cd OcrDemo
   ```

2. Προσθέστε το πακέτο NuGet Aspose.OCR:

   ```bash
   dotnet add package Aspose.OCR
   ```

Το πακέτο περιέχει τη μηχανή OCR, τα μοντέλα γλώσσας και τα εργαλεία διαχείρισης εικόνας που απαιτούνται για **convert image to text**.

> **Pro tip:** Εάν σκοπεύετε να εκτελείτε OCR σε πολλαπλές εικόνες, σκεφτείτε να προσθέσετε το πακέτο σε μια κοινόχρηστη βιβλιοθήκη ώστε να μπορείτε να επαναχρησιμοποιήσετε την ίδια παρουσία της μηχανής.

## Βήμα 2: Γράψτε το παράδειγμα OCR σε C#

Δημιουργήστε ή αντικαταστήστε το `Program.cs` με τον παρακάτω κώδικα. Δείχνει ένα **c# ocr example** που λειτουργεί για οποιαδήποτε μορφή εικόνας υποστηρίζεται από το Aspose.OCR (JPEG, PNG, BMP, κλπ).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // ---------------------------------------------------------
        // Step 2.1: Create an OCR engine instance
        // ---------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---------------------------------------------------------
        // Step 2.2: Choose the language model.
        // The example uses Cyrillic; replace with Language.English,
        // Language.French, etc., to match your source image.
        // ---------------------------------------------------------
        ocrEngine.Language = Language.Cyrillic; // <-- change as needed

        // ---------------------------------------------------------
        // Step 2.3: Load the image you want to process.
        // ImageStream.FromFile automatically reads JPEG, PNG, BMP…
        // ---------------------------------------------------------
        ocrEngine.Image = ImageStream.FromFile("sample_cyrillic.jpg");

        // ---------------------------------------------------------
        // Step 2.4: Run the recognition process.
        // This call downloads the required language model the first
        // time it is used, then performs the OCR.
        // ---------------------------------------------------------
        ocrEngine.Recognize();

        // ---------------------------------------------------------
        // Step 2.5: Retrieve the recognized text.
        // The Text property holds the result of the OCR engine.
        // ---------------------------------------------------------
        string recognizedText = ocrEngine.Text;

        // ---------------------------------------------------------
        // Step 2.6: Display the output.
        // This is where you can further process the string,
        // e.g., save to a database, feed to a search index, etc.
        // ---------------------------------------------------------
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
}
```

### Γιατί κάθε γραμμή είναι σημαντική

* **`OcrEngine ocrEngine = new OcrEngine();`** – Δημιουργεί την μηχανή που οργανώνει ολόκληρη τη διαδικασία OCR.  
* **`ocrEngine.Language = Language.Cyrillic;`** – Επιλέγει το μοντέλο γλώσσας. Η επιλογή της σωστής γλώσσας βελτιώνει δραματικά την ακρίβεια όταν **extract text from image** αρχεία που περιέχουν μη‑λατινικούς χαρακτήρες.  
* **`ocrEngine.Image = ImageStream.FromFile(...);`** – Φορτώνει το αρχικό JPEG (ή οποιαδήποτε άλλη υποστηριζόμενη εικόνα). Αυτό το βήμα είναι απαραίτητο για **recognize text from jpeg**.  
* **`ocrEngine.Recognize();`** – Εκτελεί τον κύριο αλγόριθμο OCR. Η μέθοδος μπλοκάρει μέχρι η μηχανή να ολοκληρώσει την επεξεργασία.  
* **`ocrEngine.Text;`** – Επιστρέφει το αποτέλεσμα ως απλό κείμενο, το οποίο μπορείτε τώρα να **convert image to text** για περαιτέρω λογική.

## Βήμα 3: Εκτελέστε το πρόγραμμα και επαληθεύστε το αποτέλεσμα

Συγκεντρώστε και εκτελέστε:

```bash
dotnet run
```

Αν η εικόνα `sample_cyrillic.jpg` περιέχει τη κυριλλική φράση “Привет мир”, η κονσόλα θα εμφανίσει:

```
=== Recognized Text ===
Привет мир
```

Αυτό το αποτέλεσμα αποδεικνύει ότι έχετε μάθει με επιτυχία **how to perform OCR** και **extract text from image** χρησιμοποιώντας C#.

## Βήμα 4: Συνηθισμένες παραλλαγές και ειδικές περιπτώσεις

### 4.1 Αναγνώριση Αγγλικού ή πολυγλωσσικού κειμένου

Αντικαταστήστε την ανάθεση γλώσσας με το κατάλληλο enum:

```csharp
ocrEngine.Language = Language.English;           // English only
ocrEngine.Language = Language.Multilingual;      // Detects many languages automatically
```

### 4.2 Επεξεργασία εικόνων από ροή αντί για αρχείο

Εάν η εικόνα σας φθάνει μέσω απάντησης HTTP ή blob βάσης δεδομένων, χρησιμοποιήστε ένα `MemoryStream`:

```csharp
using (var ms = new MemoryStream(imageBytes))
{
    ocrEngine.Image = ImageStream.FromStream(ms);
    ocrEngine.Recognize();
}
```

### 4.3 Διαχείριση μεγάλων ή χαμηλής ανάλυσης εικόνων

Οι μεγάλες εικόνες αυξάνουν την κατανάλωση μνήμης. Μπορείτε να μειώσετε την ανάλυση πριν το OCR:

```csharp
ocrEngine.Config.ImagePreprocessOptions.ScaleFactor = 0.5; // Reduce size by 50%
```

### 4.4 Διαχείριση σφαλμάτων

Τυλίξτε την κλήση αναγνώρισης σε μπλοκ try‑catch για να πιάσετε σφάλματα δικτύου ή πρόσβασης σε αρχείο:

```csharp
try
{
    ocrEngine.Recognize();
}
catch (Exception ex)
{
    Console.Error.WriteLine($"OCR failed: {ex.Message}");
}
```

## Βήμα 5: Επόμενα βήματα – επέκταση της ροής εργασίας OCR

* **Batch processing:** Επανάληψη σε αρχεία σε έναν φάκελο για **convert image to text** για κάθε JPEG.  
* **Post‑processing:** Εφαρμόστε κανονικές εκφράσεις για να καθαρίσετε τη αναγνωρισμένη συμβολοσειρά, χρήσιμο όταν χρειάζεται να **extract text from image** από φόρμες ή τιμολόγια.  
* **Integration with Azure Cognitive Services:** Συγκρίνετε τα αποτελέσματα του Aspose.OCR με OCR βασισμένο στο cloud για υψηλότερη ακρίβεια σε σύνθετες διατάξεις.  
* **Storing results:** Εισάγετε το εξαγόμενο κείμενο σε μια βάση δεδομένων SQL ή σε ευρετήριο ElasticSearch για έγγραφα με δυνατότητα αναζήτησης.

---

## Συμπέρασμα

Τώρα γνωρίζετε **how to perform OCR** σε C# με το Aspose.OCR, από την εγκατάσταση του πακέτου μέχρι την εμφάνιση της αναγνωρισμένης συμβολοσειράς. Αυτό το πλήρες **c# ocr example** σας επιτρέπει να **extract text from image**, **convert image to text**, και **recognize text from JPEG** με μόνο μερικές γραμμές κώδικα. Πειραματιστείτε με διαφορετικά μοντέλα γλώσσας, πηγές εικόνας και τεχνικές post‑processing για να ταιριάζουν στην ειδική σας περίπτωση χρήσης.

---

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε σε πρόσθετα χαρακτηριστικά API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να χρησιμοποιήσετε OCR σε C# – Εξαγωγή κειμένου από αρχεία εικόνας](/ocr/english/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-files/)
- [Μετατροπή εικόνας σε κείμενο σε C# με Aspose OCR – Οδηγός βήμα‑βήμα](/ocr/english/net/text-recognition/convert-image-to-text-in-c-with-aspose-ocr-step-by-step-guid/)
- [Πώς να εκτελέσετε OCR σε C# – Εξαγωγή κειμένου και εγγραφή JSON](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-extract-text-and-write-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}