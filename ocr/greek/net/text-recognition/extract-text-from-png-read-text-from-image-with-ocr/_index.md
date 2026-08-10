---
category: general
date: 2026-03-17
description: Εξάγετε κείμενο από PNG χρησιμοποιώντας το Aspose OCR σε C#. Μάθετε πώς
  να διαβάζετε κείμενο από εικόνα, να επεξεργάζεστε OCR από απόδειξη και να δημιουργείτε
  μηχανή OCR με επιτάχυνση GPU.
draft: false
keywords:
- extract text from png
- read text from image
- ocr receipt image
- process receipt ocr
- create ocr engine
language: el
og_description: Εξαγωγή κειμένου από PNG με τη χρήση του Aspose OCR. Αυτός ο οδηγός
  δείχνει πώς να διαβάσετε κείμενο από εικόνα, να επεξεργαστείτε OCR από απόδειξη
  και να δημιουργήσετε αποδοτικά μηχανή OCR.
og_title: Εξαγωγή κειμένου από PNG – Ανάγνωση κειμένου από εικόνα με OCR
tags:
- OCR
- CSharp
- Aspose
title: Εξαγωγή κειμένου από PNG – Ανάγνωση κειμένου από εικόνα με OCR
url: /el/net/text-recognition/extract-text-from-png-read-text-from-image-with-ocr/
---

the table: translate content but keep pipe separators.

Let's craft.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από PNG – Ανάγνωση Κειμένου από Εικόνα με OCR

Έχετε χρειαστεί ποτέ να **εξάγετε κείμενο από PNG** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη θα σας δώσει αξιόπιστα αποτελέσματα; Δεν είστε οι μόνοι—οι προγραμματιστές ρωτούν συνεχώς: «Πώς διαβάζω κείμενο από αρχεία εικόνας όπως αποδείξεις χωρίς να γράψω ένα προσαρμοσμένο νευρωνικό δίκτυο;» Τα καλά νέα είναι ότι το Aspose OCR κάνει το σκληρό έργο για εσάς, και μπορείτε ακόμη να ενεργοποιήσετε την GPU για επιπλέον ταχύτητα.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από την εγκατάσταση του πακέτου NuGet μέχρι τη δημιουργία μιας μηχανής OCR που καταλαβαίνει το αρχείο PNG σας. Στο τέλος θα έχετε μια αυτόνομη εφαρμογή console που διαβάζει μια εικόνα απόδειξης, εκτυπώνει το αναγνωρισμένο κείμενο και δείχνει πώς να ρυθμίσετε τη μηχανή για διαφορετικά σενάρια. Χωρίς εξωτερική τεκμηρίωση, μόνο καθαρός κώδικας και σαφείς εξηγήσεις.

## Προαπαιτούμενα

- .NET 6.0 SDK (ή οποιαδήποτε πρόσφατη έκδοση .NET)  
- Visual Studio 2022 ή VS Code με επεκτάσεις C#  
- Υποστηριζόμενη κάρτα NVIDIA GPU με τους πιο πρόσφατους οδηγούς (προαιρετικό, αλλά συνιστάται για λειτουργία GPU)  
- Το πακέτο **Aspose.OCR** NuGet (`dotnet add package Aspose.OCR`)  

Αν δεν έχετε GPU, μπορείτε ακόμη να τρέξετε το παράδειγμα σε λειτουργία CPU—απλώς παραλείψτε τις γραμμές ρύθμισης GPU.

## Βήμα 1: Εγκατάσταση Aspose.OCR και Ρύθμιση του Έργου

Πρώτα, δημιουργήστε ένα νέο έργο console και προσθέστε τη βιβλιοθήκη Aspose OCR.

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

Γιατί είναι σημαντικό: το πακέτο `Aspose.OCR` περιλαμβάνει τη μηχανή OCR, τους φορτωτές εικόνας και την προαιρετική υποστήριξη GPU. Η προσθήκη του μέσω NuGet εξασφαλίζει ότι θα έχετε την πιο πρόσφατη σταθερή έκδοση (μέχρι Μάρτιο 2026 είναι η 23.10).

## Βήμα 2: Εισαγωγή Namespaces και Δημιουργία της Μηχανής OCR

Ανοίξτε το **Program.cs** και προσθέστε τις απαιτούμενες οδηγίες `using`. Στη συνέχεια δημιουργήστε τη μηχανή.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Optional: Enable GPU acceleration if a compatible GPU is present
            // This dramatically speeds up processing of high‑resolution PNGs
            ocrEngine.Config.EngineMode = EngineMode.Gpu;   // <-- primary way to "process receipt ocr" fast
            ocrEngine.Config.GpuDeviceId = 0; // selects the first GPU in the system

            // The rest of the code follows...
```

**Συμβουλή:** Αν αντιμετωπίσετε `System.DllNotFoundException` σε μηχανήματα χωρίς GPU, απλώς σχολιάστε τις δύο γραμμές που ορίζουν `EngineMode` και `GpuDeviceId`. Η μηχανή θα επιστρέψει αυτόματα στη λειτουργία CPU.

## Βήμα 3: Φόρτωση της Εικόνας PNG από την Που Θέλετε να Εξάγετε Κείμενο

Το Aspose OCR μπορεί να διαβάσει εικόνες απευθείας από διαδρομή αρχείου, ροή ή ακόμη και πίνακα byte. Για αυτή τη demo θα φορτώσουμε μια τοπική εικόνα απόδειξης.

```csharp
            // Step 3: Load the image (replace the path with your own PNG file)
            string imagePath = @"C:\Images\receipt.png";

            // Validate the file exists to avoid runtime surprises
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }

            // Load the image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);
```

Παρατηρήστε πώς προστατεύουμε τον κώδικα από έλλειψη αρχείου. Σε πραγματικές εφαρμογές θα εμφανίζατε πιθανώς ένα φιλικό μήνυμα UI αντί να τερματίζετε απλώς.

## Βήμα 4: Εκτέλεση της Αναγνώρισης OCR

Η πραγματική εξαγωγή κειμένου γίνεται με μία κλήση μεθόδου. Η μηχανή επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει το ακατέργαστο string, βαθμολογίες εμπιστοσύνης και πληροφορίες διάταξης.

```csharp
            // Step 4: Run the OCR process
            OcrResult ocrResult = ocrEngine.Recognize();

            // Check if the engine succeeded
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }
```

Γιατί ελέγχουμε το `ocrResult.Text`: μερικές φορές ένα PNG χαμηλής ποιότητας επιστρέφει κενό string, και είναι καλύτερο να ενημερώσετε τον χρήστη παρά να μην εμφανιστεί τίποτα σιωπηρά.

## Βήμα 5: Εμφάνιση του Αναγνωρισμένου Κειμένου

Τέλος, εκτυπώστε το εξαγόμενο κείμενο στην κονσόλα. Μπορείτε επίσης να το γράψετε σε αρχείο, βάση δεδομένων ή να το περάσετε σε άλλη υπηρεσία.

```csharp
            // Step 5: Display the recognized text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

Όταν τρέξετε το πρόγραμμα (`dotnet run`), θα δείτε κάτι σαν:

```
=== Extracted Text from PNG ===
Store: Coffee Corner
Date: 03/15/2026
Item      Qty   Price
Latte      2    $5.40
Muffin     1    $2.30
Total            $7.70
=== End of Output ===
```

Αυτή είναι η **πλήρης λύση για εξαγωγή κειμένου από αρχεία PNG** με Aspose OCR, και μόλις μάθατε πώς να **διαβάζετε κείμενο από εικόνες** που μοιάζουν με αποδείξεις.

## Προαιρετικό: Λεπτομερής Ρύθμιση της Μηχανής OCR (Για Προχωρημένους)

Αν χρειάζεστε μεγαλύτερη ακρίβεια για συγκεκριμένες γραμματοσειρές ή θορυβώδεις φόντους, σκεφτείτε να προσαρμόσετε τις παρακάτω ρυθμίσεις:

```csharp
// Enable language detection (default is English)
ocrEngine.Config.Language = Language.English;

// Turn on automatic image preprocessing (deskew, binarization)
ocrEngine.Config.EnableImagePreprocessing = true;

// Set a confidence threshold if you only want high‑certainty results
ocrEngine.Config.ConfidenceThreshold = 0.75f;
```

Αυτές οι μικρορυθμίσεις είναι ιδιαίτερα χρήσιμες όταν **επεξεργάζεστε OCR αποδείξεων** σε παρτίδες όπου κάποιες σάρωση δεν είναι τέλεια.

## Συνηθισμένα Προβλήματα & Πώς να τα Αποφύγετε

| Πρόβλημα | Γιατί Συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| **Λείπει ο οδηγός GPU** | Η μηχανή προσπαθεί να φορτώσει CUDA αλλά δεν βρίσκει το DLL. | Εγκαταστήστε τον πιο πρόσφατο οδηγό NVIDIA ή μεταβείτε σε λειτουργία CPU αφαιρώντας τη γραμμή `EngineMode.Gpu`. |
| **Λανθασμένη διαδρομή εικόνας** | Το `ImageStream.FromFile` πετάει εξαίρεση αν το αρχείο δεν βρεθεί. | Πάντα να επικυρώνετε τη διαδρομή (δείτε το Βήμα 3) ή χρησιμοποιήστε `Path.Combine` για ασφαλή διασυστημική χρήση. |
| **Χαμηλή εμπιστοσύνη σε θολές αποδείξεις** | Η μηχανή OCR δεν μπορεί να διακρίνει χαρακτήρες. | Ενεργοποιήστε `EnableImagePreprocessing` και προαιρετικά αυξήστε το DPI της εικόνας πριν τη δώσετε στη μηχανή. |
| **Διαρροή μνήμης σε υπηρεσίες μεγάλης διάρκειας** | Κάθε `OcrEngine` κρατά μη διαχειριζόμενους πόρους. | Αποδεσμεύστε τη μηχανή μετά τη χρήση: `using var ocrEngine = new OcrEngine();` |

## Πλήρες Παράδειγμα (Αντιγραφή‑Επικόλληση)

Παρακάτω είναι το **ολόκληρο πρόγραμμα** που μπορείτε να τοποθετήσετε στο `Program.cs`. Περιλαμβάνει όλα τα προαιρετικά tweaks σχολιασμένα για εύκολη ενεργοποίηση.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create OCR engine
            using var ocrEngine = new OcrEngine();

            // Enable GPU acceleration if you have a supported card
            ocrEngine.Config.EngineMode = EngineMode.Gpu;
            ocrEngine.Config.GpuDeviceId = 0;

            // Optional fine‑tuning (uncomment as needed)
            //ocrEngine.Config.Language = Language.English;
            //ocrEngine.Config.EnableImagePreprocessing = true;
            //ocrEngine.Config.ConfidenceThreshold = 0.75f;

            // Load PNG image
            string imagePath = @"C:\Images\receipt.png";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize();

            // Verify result
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }

            // Output the extracted text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

Αποθηκεύστε, τρέξτε `dotnet run`, και θα δείτε το περιεχόμενο της απόδειξης να εκτυπώνεται στην κονσόλα.

![εξαγωγή κειμένου από png παράδειγμα](receipt.png "εξαγωγή κειμένου από png παράδειγμα")

*Η παραπάνω εικόνα δείχνει μια δείγμα PNG απόδειξης που μπορεί να επεξεργαστεί ο κώδικας.*

## Ανακεφαλαίωση

Καλύψαμε πώς να **εξάγετε κείμενο από PNG** χρησιμοποιώντας Aspose OCR, δείξαμε πώς να **διαβάζετε κείμενο από εικόνα**, και περάσαμε από μια πλήρη **διαδικασία OCR αποδείξεων** που περιλαμβάνει προαιρετική επιτάχυνση GPU. Δημιουργώντας τη δική σας μηχανή OCR, αποκτάτε πλήρη έλεγχο πάνω στη διαμόρφωση, την απόδοση και τη διαχείριση σφαλμάτων.

## Τι Να Εξερευνήσετε Στη Σύντομη Μελλοντική?

- **Επεξεργασία παρτίδας**: Επανάληψη πάνω σε έναν φάκελο PNG αποδείξεων και εγγραφή κάθε αποτελέσματος σε αρχείο CSV.  
- **Ενσωμάτωση με Azure Functions**: Μετατρέψτε αυτή την εφαρμογή console σε serverless endpoint που δέχεται μεταφορτώσεις εικόνας.  
- **Υποστήριξη πολλαπλών γλωσσών**: Αντικαταστήστε το `Language.English` με `Language.Spanish` ή προσθέστε προσαρμοσμένα λεξικά.  
- **Μετα-επεξεργασία**: Χρησιμοποιήστε κανονικές εκφράσεις για εξαγωγή πεδίων όπως το συνολικό ποσό, η ημερομηνία ή ο ΑΦΜ από το ακατέργαστο OCR string.

Πειραματιστείτε ελεύθερα—το OCR είναι ένα απρόσμενα ευέλικτο εργαλείο μόλις γνωρίζετε τα σωστά κουμπιά. Αν συναντήσετε δυσκολίες, αφήστε ένα σχόλιο παρακάτω ή ελέγξτε την αναφορά API του Aspose OCR για πιο βαθιές πληροφορίες.

Καλό coding, και απολαύστε τη μετατροπή εκείνων των επίμονων PNG αποδείξεων σε αναζητήσιμο κείμενο!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}