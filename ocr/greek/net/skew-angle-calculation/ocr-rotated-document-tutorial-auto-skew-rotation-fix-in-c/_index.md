---
category: general
date: 2026-06-03
description: Οδηγός OCR για περιστραμμένο έγγραφο που δείχνει πώς να διορθώσετε αυτόματα
  την κλίση και να εντοπίσετε την περιστροφή χρησιμοποιώντας το Aspose OCR σε C#.
  Μάθετε βήμα‑βήμα με πλήρη κώδικα.
draft: false
keywords:
- ocr rotated document tutorial
- Aspose OCR
- automatic skew correction
- auto detect rotation
- C# image processing
language: el
og_description: Το σεμινάριο OCR για περιστραμμένο έγγραφο σας διδάσκει πώς να διορθώνετε
  αυτόματα την κλίση και να ανιχνεύετε την περιστροφή χρησιμοποιώντας το Aspose OCR
  σε C#. Ακολουθήστε τον πλήρη οδηγό.
og_title: Οδηγός OCR για Περιστραμμένο Έγγραφο – Αυτόματη Διόρθωση Στρέψης & Περιστροφής
  σε C#
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: OCR rotated document tutorial that shows how to auto-correct skew and
    detect rotation using Aspose OCR in C#. Learn step‑by‑step with full code.
  headline: OCR Rotated Document Tutorial – Auto Skew & Rotation Fix in C#
  type: TechArticle
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Οδηγός OCR για Περιστρεφόμενα Έγγραφα – Αυτόματη Διόρθωση Κλίσης & Περιστροφής
  σε C#
url: /el/net/skew-angle-calculation/ocr-rotated-document-tutorial-auto-skew-rotation-fix-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Οδηγός OCR για Περιστρεφόμενα Έγγραφα – Πλήρης Εγχειρίδιο για Προγραμματιστές C#

Έχετε ποτέ βρεθεί αντιμέτωποι με ένα **ocr rotated document tutorial** όταν μια σαρωμένη φόρμα ήρθε πλαγίως ή λοξά; Δεν είστε μόνοι. Αυτές οι παραμορφωμένες εικόνες μπορούν να χαλάσουν την καθαρή εξαγωγή κειμένου, αλλά το καλό νέο είναι ότι το Aspose OCR μπορεί να τα διορθώσει αυτόματα.

Σε αυτόν τον οδηγό βήμα‑βήμα θα δημιουργήσουμε ένα `OcrEngine`, θα ενεργοποιήσουμε την **automatic skew correction** και την **auto detect rotation**, θα τρέξουμε τη μηχανή σε μια περιστρεφόμενη εικόνα και θα εκτυπώσουμε το καθαρό κείμενο. Στο τέλος θα γνωρίζετε ακριβώς γιατί κάθε ρύθμιση είναι σημαντική, πώς να την προσαρμόσετε για ειδικές περιπτώσεις, και θα έχετε ένα έτοιμο προς εκτέλεση πρόγραμμα C#.

## Τι Θα Μάθετε

* Πώς να εγκαταστήσετε και να αναφέρετε το **Aspose OCR** σε ένα έργο .NET.  
* Γιατί η ενεργοποίηση των `AutoCorrectSkew` και `AutoDetectRotation` είναι το κλειδί για ένα αξιόπιστο **ocr rotated document tutorial**.  
* Πώς να φορτώσετε οποιαδήποτε εικόνα (JPG, PNG, TIFF) και να αφήσετε τη μηχανή να κάνει τη βαριά δουλειά.  
* Συμβουλές για τη διαχείριση πολυσελίδων PDF, σαρώσεων χαμηλής ανάλυσης και προσαρμοσμένων πακέτων γλώσσας.

> **Προαπαιτούμενα:** Visual Studio 2022 (ή οποιοδήποτε IDE C#), .NET 6+ runtime, και μια έγκυρη άδεια Aspose OCR (ή η δωρεάν δοκιμή). Δεν απαιτείται προηγούμενη εμπειρία OCR.

---

## Βήμα 1 – Εγκατάσταση Aspose OCR και Ρύθμιση του Έργου

Πρώτα απ' όλα. Κατεβάστε το πακέτο NuGet:

```bash
dotnet add package Aspose.OCR
```

> **Συμβουλή:** Εάν χρησιμοποιείτε δοκιμαστική άδεια, τοποθετήστε το αρχείο `Aspose.OCR.lic` στον ίδιο φάκελο με το εκτελέσιμο σας, ή καταχωρίστε το προγραμματιστικά με `License license = new License(); license.SetLicense("Aspose.OCR.lic");`.

Δημιουργήστε μια νέα εφαρμογή κονσόλας:

```bash
dotnet new console -n OcrRotatedDemo
cd OcrRotatedDemo
```

Τώρα έχετε ένα καθαρό περιβάλλον για το **ocr rotated document tutorial** μας.

## Βήμα 2 – Αρχικοποίηση του OCR Engine

Η μηχανή είναι η καρδιά της διαδικασίας. Σκεφτείτε την ως ένα πολυεργαλείο για εξαγωγή κειμένου· χρειάζεται μόνο να της πείτε ποιες λειτουργίες να ενεργοποιήσετε.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

class SkewDemo
{
    static void Main()
    {
        // Step 2.1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2.2: Enable automatic skew correction
        ocrEngine.Settings.AutoCorrectSkew = true;   // <-- fixes slanted lines

        // Step 2.3: Enable automatic rotation detection
        ocrEngine.Settings.AutoDetectRotation = true; // <-- turns the page upright
```

**Γιατί αυτές οι ρυθμίσεις;**

* `AutoCorrectSkew` αναλύει τη βάση των χαρακτήρων και περιστρέφει την εικόνα ακριβώς όσο χρειάζεται ώστε οι γραμμές να είναι οριζόντιες.  
* `AutoDetectRotation` εξετάζει τη συνολική προσανατολισμό (0°, 90°, 180°, 270°) και αναστρέφει τη σελίδα αν είναι ανάποδη. Χωρίς αυτές, η μηχανή θα διάβαζε “pɹᴉʍ” αντί για “word”.

## Βήμα 3 – Φόρτωση της Εικόνας που Θέλετε να Επεξεργαστείτε

Το Aspose OCR λειτουργεί με οποιαδήποτε κοινή μορφή raster. Αντικαταστήστε τη διαδρομή placeholder με την πραγματική θέση της περιστρεφόμενης φόρμας σας.

```csharp
        // Step 3: Load the image that may be rotated or skewed
        var imagePath = @"C:\Scans\rotated_form.jpg"; // adjust as needed
        var image = OcrImage.FromFile(imagePath);
```

> **Ειδική περίπτωση:** Εάν λάβετε ένα πολυσελίδων TIFF, χρησιμοποιήστε `OcrImage.FromMultiPageTiff(filePath)` και κάντε βρόχο μέσω `image.Pages`.

## Βήμα 4 – Εκτέλεση της Αναγνώρισης

Τώρα η μηχανή κάνει τη μαγεία. Θα διορθώσει πρώτα την εικόνα (ευχαριστώντας τις σημαίες skew/rotation) και στη συνέχεια θα εξάγει τους χαρακτήρες.

```csharp
        // Step 4: Perform OCR recognition on the image
        var ocrResult = ocrEngine.Recognize(image);
```

Εάν χρειάζεστε υποστήριξη γλώσσας πέρα από τα Αγγλικά, ορίστε την πριν καλέσετε το `Recognize`:

```csharp
        ocrEngine.Settings.Language = Language.Spanish; // example
```

## Βήμα 5 – Έξοδος του Αναγνωρισμένου Κειμένου

Τέλος, εκτυπώστε το καθαρό κείμενο στην κονσόλα—ή το δρομολογήστε σε αρχείο, βάση δεδομένων, ό,τι ταιριάζει στη ροή εργασίας σας.

```csharp
        // Step 5: Output the recognized text
        System.Console.WriteLine("=== OCR Result ===");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

**Αναμενόμενη έξοδος** (υποθέτοντας ότι η δείγμα εικόνας περιέχει “Invoice #1234”):

```
=== OCR Result ===
Invoice #1234
Date: 2026-05-30
Total: $1,250.00
```

Παρατηρήστε πώς το κείμενο εμφανίζεται σωστά παρόλο που η αρχική εικόνα ήταν περιστραμμένη 90° και ελαφρώς λοξή.

---

## Διαχείριση Συνηθισμένων Προβλημάτων

| Πρόβλημα | Γιατί Συμβαίνει | Διόρθωση |
|------|----------------|-----|
| **Κενή έξοδος** | Η διόρθωση skew είναι απενεργοποιημένη ή η εικόνα είναι πολύ σκοτεινή. | Ενεργοποιήστε το `AutoCorrectSkew` (ήδη ενεργό) και αυξήστε την αντίθεση της εικόνας μέσω `image.AdjustContrast(1.2)`. |
| **Ασυνήθιστοι χαρακτήρες** | Λάθος ρύθμιση γλώσσας. | Ορίστε το `ocrEngine.Settings.Language` ώστε να ταιριάζει με τη γλώσσα του εγγράφου. |
| **Καθυστέρηση απόδοσης σε μεγάλα PDFs** | Η μηχανή επεξεργάζεται κάθε σελίδα διαδοχικά. | Χρησιμοποιήστε `Parallel.ForEach` στο `image.Pages` για να αξιοποιήσετε πολυπύρηνους επεξεργαστές. |
| **Αδυναμία άδειας** | Η δοκιμαστική άδεια έληξε. | Αποκτήστε μόνιμη άδεια ή παραμείνετε εντός των περιορισμών της δοκιμής (5 σελίδες ανά εκτέλεση). |

## Συμβουλές για Ένα Αξιόπιστο OCR Rotated Document Tutorial

* **Επεξεργασία παρτίδας:** Τυλίξτε όλη τη ροή σε μια μέθοδο που δέχεται διαδρομή φακέλου, διασχίζει κάθε εικόνα και γράφει κάθε αποτέλεσμα σε αρχείο `.txt`.  
* **Προεπεξεργασία:** Μερικές φορές μια θορυβώδης σάρωση ωφελείται από `image.Denoise()` πριν την αναγνώριση.  
* **Μεταεπεξεργασία:** Χρησιμοποιήστε κανονικές εκφράσεις για να καθαρίσετε κοινά σφάλματα OCR, π.χ., αντικαταστήστε το “0” με “O” μόνο όταν περιβάλλεται από γράμματα.  
* **Καταγραφή:** Το Aspose OCR παρέχει το `ocrEngine.Logger` – συνδέστε το με έναν καταγραφέα αρχείων για να συλλάβετε προειδοποιήσεις σχετικά με χαμηλές βαθμολογίες εμπιστοσύνης.

## Πλήρης, Έτοιμος‑για‑Εκτέλεση Κώδικας

Αποθηκεύστε το παρακάτω ως `Program.cs` μέσα στο κονσόλα έργο σας. Περιλαμβάνει όλα τα βήματα, σχόλια, και έναν μικρό βοηθό για επεξεργασία παρτίδας.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace OcrRotatedDemo
{
    class Program
    {
        static void Main()
        {
            // OPTIONAL: Register your license here
            // var license = new License();
            // license.SetLicense("Aspose.OCR.lic");

            // Path to a single image – change as needed
            string imagePath = @"C:\Scans\rotated_form.jpg";

            // Run OCR on one file
            string result = ProcessImage(imagePath);
            Console.WriteLine("=== OCR Result for Single File ===");
            Console.WriteLine(result);

            // OPTIONAL: Process an entire folder
            // string folder = @"C:\Scans\Batch";
            // ProcessFolder(folder);
        }

        /// <summary>
        /// Recognizes text from a possibly rotated or skewed image.
        /// </summary>
        static string ProcessImage(string filePath)
        {
            var engine = new OcrEngine();

            // Enable automatic corrections – core of our OCR rotated document tutorial
            engine.Settings.AutoCorrectSkew = true;
            engine.Settings.AutoDetectRotation = true;

            // If you know the language, set it here (default is English)
            // engine.Settings.Language = Language.French;

            var image = OcrImage.FromFile(filePath);
            var result = engine.Recognize(image);
            return result.Text;
        }

        /// <summary>
        /// Processes every image in a folder and writes a .txt per file.
        /// </summary>
        static void ProcessFolder(string folderPath)
        {
            foreach (var file in Directory.GetFiles(folderPath, "*.*", SearchOption.TopDirectoryOnly))
            {
                if (!file.EndsWith(".jpg", StringComparison.OrdinalIgnoreCase) &&
                    !file.EndsWith(".png", StringComparison.OrdinalIgnoreCase) &&
                    !file.EndsWith(".tif", StringComparison.OrdinalIgnoreCase))
                    continue; // skip unsupported files

                string text = ProcessImage(file);
                string outPath = Path.ChangeExtension(file, ".txt");
                File.WriteAllText(outPath, text);
                Console.WriteLine($"Processed {Path.GetFileName(file)} → {Path.GetFileName(outPath)}");
            }
        }
    }
}
```

Τρέξτε το:

```bash
dotnet run
```

Θα πρέπει να δείτε το καθαρισμένο κείμενο να εκτυπώνεται στην κονσόλα, αποδεικνύοντας ότι το **ocr rotated document tutorial** μας λειτουργεί από άκρη σε άκρη.

## Συμπέρασμα

Τώρα έχετε ένα πλήρες **ocr rotated document tutorial** που διορθώνει αυτόματα το skew, εντοπίζει την περιστροφή και εξάγει καθαρό κείμενο χρησιμοποιώντας το Aspose OCR σε C#. Το βασικό συμπέρασμα; Η ενεργοποίηση του `AutoCorrectSkew` **και** του `AutoDetectRotation` μετατρέπει μια πολύ κεκλιμένη σάρωση σε τέλεια αναγνώσιμη έξοδο με λίγες μόνο γραμμές κώδικα.

Από εδώ, μπορείτε να επεκτείνετε σε εργασίες παρτίδας, να ενσωματώσετε πακέτα γλώσσας, ή να τροφοδοτήσετε τα αποτελέσματα σε downstream pipelines ανάλυσης. Θέλετε να εξερευνήσετε περαιτέρω το **automatic skew correction**; Ρίξτε μια ματιά στο API προεπεξεργασίας εικόνας του Aspose, ή πειραματιστείτε με προσαρμοσμένα όρια για θορυβώδεις σαρώσεις.

Έχετε ερωτήσεις σχετικά με τη διαχείριση PDF, πολυσελίδων TIFF, ή την ενσωμάτωση με Azure Functions; Αφήστε ένα σχόλιο, και καλή κωδικοποίηση!

## Τι Θα Μάθετε Στη Σύντομη Μελλοντική Περίοδο;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετα χαρακτηριστικά του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην δική σας υλοποίηση.

- [ocr document mode – Detect Areas Mode in OCR Image Recognition](/ocr/english/net/text-recognition/ocr-detect-areas-mode/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Aspose OCR Tutorial – Optical Character Recognition](/ocr/english/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}