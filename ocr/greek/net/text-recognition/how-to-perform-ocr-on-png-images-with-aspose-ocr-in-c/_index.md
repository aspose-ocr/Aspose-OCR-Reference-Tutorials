---
category: general
date: 2026-11-26
description: Μάθετε πώς να εκτελείτε OCR σε αρχεία PNG, να μετατρέπετε PNG σε κείμενο
  και να εξάγετε κυριλλικό κείμενο χρησιμοποιώντας το Aspose.OCR – βήμα‑βήμα οδηγός
  για προγραμματιστές.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- convert PNG to text
- recognize text from PNG
- extract Cyrillic text
- load image for OCR
language: el
lastmod: 2026-11-26
og_description: Πώς να εκτελέσετε OCR σε αρχεία PNG και να εξάγετε κυριλλικό κείμενο
  χρησιμοποιώντας το Aspose.OCR σε C#. Ακολουθήστε αυτόν τον πλήρη οδηγό για να μετατρέψετε
  PNG σε κείμενο.
og_image_alt: how to perform OCR on a PNG image using Aspose.OCR
og_title: Πώς να εκτελέσετε OCR σε εικόνες PNG με το Aspose.OCR – Οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-11-26'
  description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  headline: How to perform OCR on PNG images with Aspose.OCR in C#
  type: TechArticle
- description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  name: How to perform OCR on PNG images with Aspose.OCR in C#
  steps:
  - name: Handling large images
    text: 'If the PNG is larger than 2 MB, consider down‑scaling it before recognition
      to speed up processing:'
  - name: 'Edge case: Missing language module'
    text: 'If the download fails (e.g., offline environment), the engine throws an
      `OcrException`. Catch it to provide a graceful fallback:'
  - name: Expected output
    text: 'If `sample_image.png` contains the Cyrillic phrase “Привет мир”, the console
      will display:'
  - name: How it works
    text: 1. **Engine creation** – prepares the OCR pipeline. 2. **Image loading**
      – supports both raw PNG and down‑scaled versions for performance. 3. **Language
      selection** – demonstrates **extract Cyrillic text** while handling missing
      modules. 4. **Recognition** – the core **recognize text from PNG** call
  type: HowTo
tags:
- OCR
- C#
- Aspose.OCR
title: Πώς να εκτελέσετε OCR σε εικόνες PNG με το Aspose.OCR σε C#
url: /el/net/text-recognition/how-to-perform-ocr-on-png-images-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εκτελέσετε OCR σε εικόνες PNG με το Aspose.OCR σε C#

Αν χρειάζεστε **πώς να εκτελέσετε OCR** σε αρχείο PNG, αυτός ο οδηγός σας δείχνει τα ακριβή βήματα για να μετατρέψετε PNG σε κείμενο χρησιμοποιώντας το Aspose.OCR. Είτε εξάγετε κυριλλικό κείμενο από σαρωμένα έγγραφα είτε απλώς αναγνωρίζετε κείμενο από στιγμιότυπα PNG, η λύση λειτουργεί αμέσως και απαιτεί μόνο λίγες γραμμές κώδικα C#.

Σε αυτό το tutorial θα μάθετε πώς να:

* **φορτώνετε εικόνα για OCR** από τοπικό φάκελο,
* ρυθμίζετε τη μηχανή ώστε **να εξάγει κυριλλικό κείμενο**,
* **αναγνωρίζετε κείμενο από PNG** και λαμβάνετε μια καθαρή συμβολοσειρά,
* αντιμετωπίζετε κοινά προβλήματα όπως η έλλειψη γλωσσικών μονάδων και μεγάλες εικόνες.

Δεν απαιτείται προηγούμενη εμπειρία με το Aspose.OCR — μόνο ένα .NET περιβάλλον ανάπτυξης και μια εικόνα PNG που θέλετε να επεξεργαστείτε.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 (ή νεότερη) εγκατεστημένη.
* Άδεια ή δοκιμαστική έκδοση του **Aspose.OCR for .NET**. Μπορείτε να αποκτήσετε δωρεάν δοκιμή από την ιστοσελίδα της Aspose.
* Visual Studio 2022 (ή οποιοδήποτε IDE που υποστηρίζει .NET).
* Ένα αρχείο PNG που περιέχει το κείμενο που θέλετε να εξάγετε (το παράδειγμα χρησιμοποιεί `sample_image.png`).

## Βήμα 1: Εγκατάσταση του πακέτου NuGet Aspose.OCR

Ανοίξτε ένα τερματικό στον φάκελο του έργου σας και εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

Το πακέτο περιλαμβάνει τον πυρήνα της μηχανής OCR και όλες τις γλωσσικές μονάδες. Όταν ζητήσετε μια γλώσσα που δεν υπάρχει τοπικά, το Aspose.OCR θα κατεβάσει αυτόματα τη απαιτούμενη μονάδα.

## Βήμα 2: Δημιουργία μιας παρουσίας της μηχανής OCR (πώς να εκτελέσετε OCR)

Το πρώτο πρακτικό βήμα σε οποιαδήποτε ροή εργασίας OCR είναι η δημιουργία της μηχανής. Αυτό το αντικείμενο διαχειρίζεται όλες τις επόμενες λειτουργίες, όπως η φόρτωση της εικόνας και η εκτέλεση της αναγνώρισης.

```csharp
using Aspose.OCR;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

**Γιατί είναι σημαντικό:** Η κλάση `OcrEngine` ενσωματώνει την αλυσίδα επεξεργασίας OCR. Η δημιουργία μιας μόνο παρουσίας και η επαναχρησιμοποίησή της σε πολλαπλές εικόνες μειώνει το φορτίο μνήμης και βελτιώνει την απόδοση.

## Βήμα 3: Φόρτωση εικόνας για OCR – καθορίστε το αρχείο PNG προέλευσης

Η φόρτωση της εικόνας είναι το σημείο όπου **φορτώνετε εικόνα για OCR**. Το Aspose.OCR δέχεται πολλούς τύπους εισόδου· ο πιο απλός είναι `ImageStream.FromFile`.

```csharp
// Load the PNG image from disk
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_image.png");
```

> **Συμβουλή:** Χρησιμοποιήστε απόλυτη διαδρομή ή `Path.Combine` για να αποφύγετε σφάλματα χρόνου εκτέλεσης σε διαφορετικά περιβάλλοντα.

### Διαχείριση μεγάλων εικόνων

Αν το PNG είναι μεγαλύτερο από 2 MB, εξετάστε το ενδεχόμενο να το μειώσετε πριν από την αναγνώριση για να επιταχύνετε την επεξεργασία:

```csharp
using System.Drawing;

// Downscale large images to a maximum width of 1200 pixels
Bitmap original = new Bitmap(@"YOUR_DIRECTORY/sample_image.png");
int maxWidth = 1200;
int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

using (var ms = new MemoryStream())
{
    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
    ocrEngine.Image = ImageStream.FromStream(ms);
}
```

## Βήμα 4: Ρύθμιση γλώσσας – εξαγωγή κυριλλικού κειμένου

Από προεπιλογή, το Aspose.OCR υποθέτει Αγγλικά. Για να **εξάγετε κυριλλικό κείμενο**, ορίστε την ιδιότητα `Language` σε `Language.Cyrillic`. Η απαιτούμενη μονάδα θα κατέβει αυτόματα την πρώτη φορά που θα τρέξετε τον κώδικα.

```csharp
// Set the OCR language to Cyrillic
ocrEngine.Language = Language.Cyrillic;
```

Αν χρειάζεται να αναγνωρίσετε πολλαπλές γλώσσες (π.χ. Αγγλικά και Κυριλλικά), μπορείτε να τις συνδυάσετε:

```csharp
ocrEngine.Language = Language.English | Language.Cyrillic;
```

### Ακραία περίπτωση: Έλλειψη γλωσσικής μονάδας

Αν η λήψη αποτύχει (π.χ. σε περιβάλλον χωρίς σύνδεση), η μηχανή θα ρίξει ένα `OcrException`. Πιάστε το για να παρέχετε μια ευγενική εναλλακτική:

```csharp
try
{
    ocrEngine.Language = Language.Cyrillic;
}
catch (OcrException ex)
{
    Console.WriteLine($"Language module could not be loaded: {ex.Message}");
    // Optionally, fall back to English or abort the process
}
```

## Βήμα 5: Εκτέλεση της λειτουργίας αναγνώρισης (αναγνώριση κειμένου από PNG)

Τώρα που η εικόνα και η γλώσσα έχουν οριστεί, μπορείτε να **αναγνωρίσετε κείμενο από PNG**. Η μέθοδος `Recognize` εκτελεί την αλυσίδα OCR συγχρονισμένα.

```csharp
// Run OCR
ocrEngine.Recognize();
```

**Γιατί λειτουργεί:** Εσωτερικά, το Aspose.OCR εφαρμόζει προεπεξεργασία (δυαδικοποίηση, αφαίρεση θορύβου) πριν περάσει την εικόνα σε έναν νευρωνικό αναγνωριστή που είναι βελτιστοποιημένος για την επιλεγμένη γλώσσα.

## Βήμα 6: Ανάκτηση και εμφάνιση του αναγνωρισμένου κειμένου (μετατροπή PNG σε κείμενο)

Μετά την αναγνώριση, η εξαγόμενη συμβολοσειρά είναι διαθέσιμη μέσω της ιδιότητας `Text`. Αυτό είναι το τελικό βήμα στο **μετατροπή PNG σε κείμενο**.

```csharp
// Get the recognized text
string recognizedText = ocrEngine.Text;

// Output the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

### Αναμενόμενο αποτέλεσμα

Αν το `sample_image.png` περιέχει τη κυριλλική φράση “Привет мир”, η κονσόλα θα εμφανίσει:

```
=== OCR Result ===
Привет мир
```

Η έξοδος μπορεί να περιλαμβάνει αλλαγές γραμμής και στίξη ακριβώς όπως εμφανίζονται στην εικόνα. Μπορείτε να επεξεργαστείτε τη συμβολοσειρά με `String.Trim()`, `Regex` ή άλλα εργαλεία καθαρισμού κειμένου αν χρειάζεται.

## Βήμα 7: Προαιρετικό – Αποθήκευση του αποτελέσματος σε αρχείο

Η αποθήκευση του αποτελέσματος OCR επιτρέπει επόμενη επεξεργασία (π.χ. ευρετηρίαση, μετάφραση). Εδώ είναι ένας γρήγορος τρόπος για να γράψετε το κείμενο σε αρχείο UTF‑8:

```csharp
File.WriteAllText(@"YOUR_DIRECTORY/ocr_output.txt", recognizedText, Encoding.UTF8);
Console.WriteLine("OCR text saved to ocr_output.txt");
```

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Πρόβλημα | Συμπτωμα | Διόρθωση |
|----------|----------|----------|
| **Έλλειψη γλωσσικής μονάδας** | `OcrException` στο `Language = Language.Cyrillic` | Διασφαλίστε σύνδεση στο διαδίκτυο στην πρώτη εκτέλεση ή προ‑κατεβάστε τις μονάδες μέσω του offline πακέτου της Aspose. |
| **Θολή ή χαμηλής αντίθεσης εικόνα** | Χαμηλή ακρίβεια, πολλοί χαρακτήρες “?” | Προεπεξεργασία εικόνας: αυξήστε την αντίθεση, εφαρμόστε όξυνση ή μετατρέψτε σε γκρι κλίμακα πριν τη δώσετε στη μηχανή. |
| **Πολύ μεγάλο PNG** | Μεγάλος χρόνος επεξεργασίας, πιθανό `OutOfMemoryException` | Μειώστε το μέγεθος όπως φαίνεται στο Βήμα 3 ή χωρίστε μια πολυσελίδα εικόνα σε ξεχωριστά τμήματα. |
| **Χαρακτήρες μη‑UTF‑8** | Κατεστραμμένη έξοδος | Βεβαιωθείτε ότι η κονσόλα ή ο συγγραφέας αρχείου χρησιμοποιεί κωδικοποίηση UTF‑8 (`Encoding.UTF8`). |

## Πλήρες, εκτελέσιμο παράδειγμα

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που ενσωματώνει όλα τα παραπάνω βήματα. Αντιγράψτε το σε ένα νέο έργο κονσόλας και τρέξτε το αφού προσαρμόσετε τις διαδρομές αρχείων.

```csharp
using System;
using System.Drawing;
using System.IO;
using System.Text;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1. Create OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 2. Load PNG image (with optional down‑scaling for large files)
            string imagePath = @"YOUR_DIRECTORY/sample_image.png";
            Bitmap original = new Bitmap(imagePath);
            const int maxWidth = 1200;

            if (original.Width > maxWidth)
            {
                int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
                Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

                using (var ms = new MemoryStream())
                {
                    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    ocrEngine.Image = ImageStream.FromStream(ms);
                }
            }
            else
            {
                ocrEngine.Image = ImageStream.FromFile(imagePath);
            }

            // 3. Set language to Cyrillic (fallback to English if needed)
            try
            {
                ocrEngine.Language = Language.Cyrillic;
            }
            catch (OcrException ex)
            {
                Console.WriteLine($"Failed to load Cyrillic module: {ex.Message}");
                Console.WriteLine("Falling back to English.");
                ocrEngine.Language = Language.English;
            }

            // 4. Recognize text
            ocrEngine.Recognize();

            // 5. Retrieve and display the text (convert PNG to text)
            string recognizedText = ocrEngine.Text;
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(recognizedText);

            // 6. Save result to a UTF‑8 file
            string outputPath = @"YOUR_DIRECTORY/ocr_output.txt";
            File.WriteAllText(outputPath, recognizedText, Encoding.UTF8);
            Console.WriteLine($"OCR text saved to {outputPath}");
        }
    }
}
```

### Πώς λειτουργεί

1. **Δημιουργία μηχανής** – προετοιμάζει την αλυσίδα OCR.  
2. **Φόρτωση εικόνας** – υποστηρίζει τόσο το ακατέργαστο PNG όσο και τις μειωμένες εκδόσεις για απόδοση.  
3. **Επιλογή γλώσσας** – δείχνει **εξαγωγή κυριλλικού κειμένου** ενώ διαχειρίζεται τις ελλείψεις μονάδων.  
4. **Αναγνώριση** – η κύρια κλήση **αναγνώριση κειμένου από PNG**.  
5. **Διαχείριση αποτελέσματος** – παρουσιάζει **μετατροπή PNG σε κείμενο** και γράφει την έξοδο σε αρχείο.

Τρέξτε το πρόγραμμα με `dotnet run`. Αν όλα είναι ρυθμισμένα σωστά, θα δείτε το αναγνωρισμένο κείμενο στην κονσόλα και θα αποθηκευτεί στο `ocr_output.txt`.

## Συμπέρασμα

Σε αυτό το tutorial μάθατε **πώς να εκτελέσετε OCR** σε αρχεία PNG χρησιμοποιώντας το Aspose.OCR για .NET, καλύπτοντας όλα από το **φόρτωση εικόνας για OCR** μέχρι την **εξαγωγή κυριλλικού κειμένου** και τη **μετατροπή PNG σε κείμενο**. Το πλήρες, εκτελέσιμο παράδειγμα παρουσιάζει τη στάνταρ ροή εργασίας, τις κοινές ακραίες περιπτώσεις και πρακτικές συμβουλές για αξιόπιστο OCR.

**Επόμενα βήματα**

* Εξερευνήστε το **αναγνώριση κειμένου από PNG** με πρόσθετες γλώσσες (Αραβικά, Κινέζικα) συνδυάζοντας τις σημαίες `Language`.  
* Ενσωματώστε το αποτέλεσμα OCR με το Azure Cognitive Search για ευρετήρια εγγράφων.  
* Πειραματιστείτε με τις ρυθμίσεις του `OcrEngine` του Aspose.OCR, όπως `Resolution


## Τι πρέπει να μάθετε στη συνέχεια;


Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση των δικών σας έργων.

- [How to Download Aspose.OCR Model and Extract Text from PNG in C#](/ocr/english/net/text-recognition/how-to-download-ocr-model-and-extract-text-from-png-using-as/)
- [How to Perform OCR in C# – Recognize Cyrillic Text with Aspose](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-recognize-cyrillic-text-with-aspose/)
- [How to Batch OCR in C# – Fast Way to Extract Text PNG Files](/ocr/english/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}