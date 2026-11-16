---
category: general
date: 2026-03-13
description: Πώς να χρησιμοποιήσετε OCR σε C# για την εξαγωγή κειμένου από σαρώσεις.
  Μάθετε πώς να μετατρέπετε TIFF σε κείμενο με το Aspose OCR, επιτάχυνση GPU και κώδικα
  βήμα‑βήμα.
draft: false
keywords:
- how to use OCR
- extract text from scans
- convert tiff to text
- c# ocr tutorial
language: el
og_description: Πώς να χρησιμοποιήσετε OCR σε C# για την εξαγωγή κειμένου από σαρώσεις.
  Αυτός ο οδηγός σας δείχνει πώς να μετατρέψετε TIFF σε κείμενο με το Aspose OCR και
  επιτάχυνση GPU.
og_title: Πώς να χρησιμοποιήσετε OCR σε C# – Εξαγωγή κειμένου από σαρώσεις γρήγορα
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Πώς να χρησιμοποιήσετε OCR σε C# – Γρήγορη εξαγωγή κειμένου από σαρώσεις
url: /el/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-scans-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε OCR σε C# – Εξαγωγή Κειμένου από Σαρώσεις Γρήγορα

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε OCR** για να εξάγετε αναγνώσιμο κείμενο από μια στοίβα σαρωμένων αρχείων TIFF; Δεν είστε οι μόνοι. Σε πολλά πραγματικά έργα—σκεφτείτε την ψηφιοποίηση τιμολογίων, την αρχειοθέτηση ιστορικών εγγράφων ή απλώς το να κάνετε τα PDF αναζητήσιμα—οι προγραμματιστές χρειάζονται έναν αξιόπιστο τρόπο για **να εξάγουν κείμενο από σαρώσεις** χωρίς κόπο.

Το καλό νέο; Με το Aspose OCR και μερικές γραμμές C# μπορείτε να μετατρέψετε TIFF σε κείμενο σε δευτερόλεπτα, ακόμη και σε έναν μέτριο υπολογιστή. Παρακάτω θα βρείτε ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα, μαζί με τη λογική πίσω από κάθε επιλογή, ώστε να το προσαρμόσετε στη δική σας ροή εργασίας.

## Τι Θα Χρειαστείτε

Πριν προχωρήσουμε, βεβαιωθείτε ότι έχετε τα παρακάτω:

| Προαπαιτούμενο | Γιατί είναι σημαντικό |
|----------------|-----------------------|
| .NET 6+ (ή .NET Framework 4.7+) | Το πακέτο NuGet Aspose OCR στοχεύει σε σύγχρονες εκδόσεις .NET. |
| Visual Studio 2022 (ή οποιοδήποτε IDE προτιμάτε) | Παρέχει IntelliSense και εύκολη αποσφαλμάτωση. |
| GPU συμβατό με CUDA & driver (προαιρετικό) | Ενεργοποιεί `ocrEngine.UseGpu = true` για αξιοσημείωτη επιτάχυνση σε μεγάλες παρτίδες. |
| Ένας φάκελος με εικόνες TIFF που θέλετε να επεξεργαστείτε | Το tutorial αυτό χρησιμοποιεί αρχεία `*.tif`, αλλά μπορείτε να προσαρμόσετε το μοτίβο. |
| Πακέτο NuGet Aspose.OCR (`Install-Package Aspose.OCR`) | Η κύρια βιβλιοθήκη που κάνει το σκληρό έργο. |

Αν λείπει κάποιο από αυτά, αποκτήστε το τώρα—δεν έχει νόημα να συνεχίσετε μόνο και μόνο για να αντιμετωπίσετε έλλειψη εξαρτήματος αργότερα.

## Επισκόπηση της Λύσης

Σε υψηλό επίπεδο το πρόγραμμα κάνει τρία πράγματα:

1. **Δημιουργεί έναν OCR engine** και προαιρετικά ενεργοποιεί την επιτάχυνση GPU.  
2. **Διασχίζει κάθε αρχείο TIFF** σε έναν φάκελο, εκτελεί αναγνώριση και αποθηκεύει το κείμενο.  
3. **Γράφει το κείμενο** σε αρχείο `.txt` δίπλα στην αρχική εικόνα.

Αυτό είναι όλο. Ο κώδικας είναι σκόπιμα μικρός, αλλά δείχνει βέλτιστες πρακτικές όπως η ρητή επιλογή γλώσσας, η σωστή διαχείριση πόρων και η διαχείριση σφαλμάτων για τις πιο κοινές εξαιρέσεις.

![How to use OCR in C# example](/images/how-to-use-ocr-csharp.png "Illustration of how to use OCR in C# to extract text from scans")

## Βήμα 1: Αρχικοποίηση του OCR Engine (Πώς να Χρησιμοποιήσετε OCR)

Το πρώτο που χρειάζεστε είναι μια παρουσία του `OcrEngine`. Αυτό το αντικείμενο είναι η πύλη σε όλη τη λειτουργικότητα του Aspose OCR. Από προεπιλογή λειτουργεί στην CPU, αλλά ορίζοντας `UseGpu = true` λέτε στη βιβλιοθήκη να μεταφέρει τους βαριούς υπολογισμούς στο γραφικό σας καρτέλα—εφόσον έχετε εγκατεστημένο driver συμβατό με CUDA.

```csharp
using Aspose.OCR;
using System.IO;

// Initialise the engine ----------------------------------------------------
OcrEngine ocrEngine = new OcrEngine
{
    // Enable GPU acceleration if a compatible card is present.
    // If you don’t have a GPU, just leave this as false – the code will still run.
    UseGpu = true,

    // Choose English as the recognition language. Change this if you need
    // another language pack (e.g., Language.French, Language.Spanish, etc.).
    Language = Language.English
};
```

**Γιατί είναι σημαντικό:**  
- **Η επιτάχυνση GPU** μπορεί να μειώσει τον χρόνο επεξεργασίας έως και 70 % για σαρώσεις υψηλής ανάλυσης.  
- **Η ρητή επιλογή γλώσσας** αποτρέπει την εικασία της μηχανής και βελτιώνει την ακρίβεια, ειδικά για μη‑λατινικά αλφάβητα.

## Βήμα 2: Καθορίστε τον Engine στα Σαρωμένα Αρχεία (Μετατροπή TIFF σε Κείμενο)

Στη συνέχεια λέμε στο πρόγραμμα πού να ψάξει τις εικόνες. Η χρήση του `Directory.GetFiles` με φίλτρο `*.tif` κρατά τη λογική απλή και αποφεύγει την ανάκτηση άσχετων αρχείων όπως `.jpg` ή `.png`.

```csharp
// Define the folder that contains the scanned TIFF images -----------------
string inputFolder = @"C:\ScannedDocs"; // <-- replace with your actual path

// Verify the folder exists before we start looping
if (!Directory.Exists(inputFolder))
{
    Console.WriteLine($"❌ Folder not found: {inputFolder}");
    return;
}
```

**Σημείωση για ειδική περίπτωση:** Αν ο φάκελος είναι κενός, η βρόχος παρακάτω απλώς δεν εκτελείται, κάτι που είναι απολύτως εντάξει. Θα δείτε ένα φιλικό μήνυμα “No files found” αργότερα.

## Βήμα 3: Επεξεργασία Κάθε Αρχείου TIFF (Εξαγωγή Κειμένου από Σαρώσεις)

Τώρα η καρδιά του προγράμματος: φόρτωση κάθε εικόνας, εκτέλεση OCR και αποθήκευση του αποτελέσματος. Η βοηθητική μέθοδος `ImageStream.FromFile` μεταφέρει το αρχείο απευθείας στη μνήμη, κάτι πιο αποδοτικό από το να φορτώνετε πρώτα ένα `Bitmap`.

```csharp
// Step 3: Iterate over every .tif file in the folder --------------------
string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

if (tiffFiles.Length == 0)
{
    Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
}
else
{
    foreach (var imagePath in tiffFiles)
    {
        try
        {
            // Load the current image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR on the image
            ocrEngine.Recognize();

            // Build the output .txt file path (same name, different extension)
            string textPath = Path.ChangeExtension(imagePath, ".txt");

            // Save the extracted text
            File.WriteAllText(textPath, ocrEngine.Text);

            Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
        }
        catch (Exception ex)
        {
            // Log the error but continue with the next file
            Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

**Γιατί τυλίγουμε κάθε επανάληψη σε `try/catch`:**  
Η επεξεργασία μιας παρτίδας εγγράφων είναι ακατάστατη· ένα κατεστραμμένο TIFF ή ένα σφάλμα μνήμης δεν πρέπει να διακόπτει όλη τη διαδικασία. Το μπλοκ catch καταγράφει το πρόβλημα και συνεχίζει, διατηρώντας την αλυσίδα αξιόπιστη.

### Αναμενόμενο Αποτέλεσμα

Για κάθε `example.tif` θα βρείτε ένα αδελφό `example.txt` που περιέχει κάτι όπως:

```
Invoice #12345
Date: 2024‑01‑15
Total: $1,250.00
Thank you for your business!
```

Αν ο OCR engine δεν μπορεί να διαβάσει μια γραμμή, θα αφήσει απλώς μια κενή γραμμή ή έναν ακατάλληλο χαρακτήρα—δεν θα καταρρεύσει η εφαρμογή.

## Βήμα 4: Καθαρισμός και Διακοπή (Καλύτερη Πρακτική)

Το `OcrEngine` υλοποιεί το `IDisposable`, οπότε είναι ευγενικό να ελευθερώσετε τους εγγενείς πόρους όταν τελειώσετε. Σε μια μικρή εφαρμογή κονσόλας μπορείτε να βασιστείτε στον GC, αλλά η ρητή διακοπή είναι συνήθεια που αξίζει να καλλιεργηθεί.

```csharp
// Dispose the engine when everything is finished -------------------------
ocrEngine.Dispose();
Console.WriteLine("🎉 All done! OCR engine released.");
```

## Πλήρες Παράδειγμα (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να επικολλήσετε σε ένα νέο έργο Console App. Συγκεντώνεται όπως είναι, εφόσον έχετε προσθέσει το πακέτο NuGet Aspose.OCR.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // --------------------------------------------------------------------
        // Step 1: Initialise the OCR engine (how to use OCR)
        // --------------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            UseGpu = true,               // Enable GPU if available
            Language = Language.English  // Set language for recognition
        };

        // --------------------------------------------------------------------
        // Step 2: Define the folder containing TIFF scans (convert TIFF to text)
        // --------------------------------------------------------------------
        string inputFolder = @"C:\ScannedDocs"; // <-- adjust this path

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"❌ Folder not found: {inputFolder}");
            return;
        }

        // --------------------------------------------------------------------
        // Step 3: Process each TIFF file (extract text from scans)
        // --------------------------------------------------------------------
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

        if (tiffFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
        }
        else
        {
            foreach (var imagePath in tiffFiles)
            {
                try
                {
                    // Load image
                    ocrEngine.Image = ImageStream.FromFile(imagePath);

                    // Run OCR
                    ocrEngine.Recognize();

                    // Save result next to source image
                    string textPath = Path.ChangeExtension(imagePath, ".txt");
                    File.WriteAllText(textPath, ocrEngine.Text);

                    Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
                }
            }
        }

        // --------------------------------------------------------------------
        // Step 4: Clean‑up (c# OCR tutorial best practice)
        // --------------------------------------------------------------------
        ocrEngine.Dispose();
        Console.WriteLine("🎉 All done! OCR engine released.");
    }
}
```

### Γρήγορη Λίστα Ελέγχου

- **Σημαία GPU** – αφαιρέστε ή θέστε σε `false` αν δεν έχετε driver CUDA.  
- **Γλώσσα** – αντικαταστήστε το `Language.English` με οποιαδήποτε άλλη υποστηριζόμενη γλώσσα.  
- **Μοτίβο αρχείου** – αλλάξτε το `"*.tif"` σε `"*.png"` ή `"*.*"` αν οι σαρώσεις σας είναι σε άλλη μορφή.  

## Συνηθισμένα Προβλήματα & Προτάσεις (c# OCR tutorial)

| Πρόβλημα | Πώς να το αποφύγετε |
|----------|----------------------|
| **Σφάλματα μνήμης** σε τεράστιες παρτίδες | Επεξεργαστείτε τα αρχεία σε μικρότερα τμήματα ή καλέστε `GC.Collect()` μετά από κάθε 50 αρχεία (σπάνια χρειάζεται). |
| **GPU δεν εντοπίστηκε** αλλά `UseGpu = true` | Ο engine επιστρέφει σιωπηλά στην CPU, αλλά μπορείτε να ελέγξετε `ocrEngine.IsGpuAvailable` μετά τη δημιουργία. |
| **Λανθασμένο πακέτο γλώσσας** οδηγεί σε ακατάλληλο κείμενο | Πάντα ορίζετε ρητά `ocrEngine.Language`. Η προεπιλογή μπορεί να είναι `Language.Unknown`. |
| **Διαδρομή αρχείου περιέχει Unicode χαρακτήρες** | Χρησιμοποιήστε `Path.GetFullPath` για κανονικοποίηση, ή προσθέστε το πρόθεμα `@"\\?\"` στα Windows αν οι διαδρομές υπερβαίνουν |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}