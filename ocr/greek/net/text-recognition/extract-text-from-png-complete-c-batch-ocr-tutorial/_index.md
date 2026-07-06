---
category: general
date: 2026-04-26
description: Εξάγετε κείμενο από αρχεία PNG γρήγορα με C#. Μάθετε πώς να μετατρέπετε
  εικόνες σε κείμενο, να διαβάζετε αρχεία PNG, να επαναλαμβάνετε τις εικόνες και να
  κάνετε μαζική OCR εικόνων σε λίγα λεπτά.
draft: false
keywords:
- extract text from png
- convert images to text
- read png files
- loop through images
- batch ocr images
language: el
og_description: Εξάγετε κείμενο από αρχεία PNG γρήγορα με C#. Αυτός ο οδηγός δείχνει
  πώς να μετατρέψετε εικόνες σε κείμενο, να διαβάσετε αρχεία PNG, να επαναλάβετε τις
  εικόνες και να κάνετε ομαδική OCR εικόνων.
og_title: Εξαγωγή κειμένου από PNG – Πλήρης οδηγός OCR σε παρτίδες C#
tags:
- C#
- OCR
- Aspose
title: Εξαγωγή κειμένου από PNG – Πλήρης οδηγός OCR σε παρτίδες με C#
url: /el/net/text-recognition/extract-text-from-png-complete-c-batch-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή κειμένου από PNG – Πλήρης οδηγός Batch OCR με C#

Κάποτε χρειάστηκε να **εξάγετε κείμενο από PNG** αρχεία αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είσαι μόνος—πολλοί προγραμματιστές συναντούν αυτό το εμπόδιο όταν προσπαθούν για πρώτη φορά OCR σε φάκελο με στιγμιότυπα. Τα καλά νέα είναι ότι με λίγες γραμμές C# και Aspose OCR μπορείς να μετατρέψεις εικόνες σε κείμενο, να διαβάσεις PNG αρχεία, να κάνεις βρόχο στις εικόνες και να επεξεργαστείς τα πάντα μαζικά σε ένα βήμα.

Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα από μια έτοιμη κονσόλα εφαρμογή που κάνει ακριβώς αυτό. Στο τέλος θα έχεις μια αυτόνομη λύση που εξάγει κείμενο από κάθε PNG σε έναν φάκελο και δημιουργεί ένα αντίστοιχο αρχείο `.txt` δίπλα σε κάθε εικόνα. Χωρίς επιπλέον σκριπτάκια, χωρίς χειροκίνητο copy‑paste—απλώς καθαρός κώδικας.

## Τι θα χρειαστείς

- **.NET 6 SDK** (ή οποιαδήποτε νεότερη έκδοση .NET). Είναι δωρεάν, γρήγορο και λειτουργεί παντού.  
- **Aspose.OCR for .NET** (το πακέτο NuGet). Η βιβλιοθήκη περιλαμβάνει επιτάχυνση GPU αν διαθέτεις συμβατό GPU, αλλά επιστρέφει αυτόματα σε CPU αν δεν υπάρχει.  
- Ένας φάκελος με μερικές **εικόνες PNG** που θέλεις να επεξεργαστείς.  
- Ένας επεξεργαστής κειμένου ή IDE—Visual Studio, VS Code, Rider—ό,τι προτιμάς.

Αυτό είναι όλο. Αν τα έχεις ήδη, είσαι έτοιμος να ξεκινήσεις.

![εξαγωγή κειμένου από png παράδειγμα](image.png "εξαγωγή κειμένου από png επίδειξη στιγμιότυπο")

*Κείμενο alt εικόνας: “εξαγωγή κειμένου από png χρησιμοποιώντας C# batch OCR”*

## Βήμα 1 – Δημιουργία έργου και εγκατάσταση Aspose.OCR

Πρώτα, δημιούργησε ένα νέο κονσόλα project και πρόσθεσε το πακέτο Aspose OCR.

```bash
dotnet new console -n PngOcrBatch
cd PngOcrBatch
dotnet add package Aspose.OCR
```

Γιατί χρησιμοποιούμε κονσόλα; Είναι ο πιο απλός τρόπος για batch εργασίες, μπορεί να τρέξει από τη γραμμή εντολών ή να προγραμματιστεί με task runner. Αν αργότερα χρειαστεί UI, μπορείς απλώς να μεταφέρεις τη λογική σε μια βιβλιοθήκη κλάσεων.

## Βήμα 2 – Αρχικοποίηση OCR Engine με επιτάχυνση GPU (ή fallback σε CPU)

Η Aspose προσφέρει ένα `GpuOcrEngine` που ανιχνεύει αυτόματα υποστηριζόμενο GPU. Αν δεν βρεθεί, επιστρέφει στον κανονικό CPU engine—χωρίς επιπλέον κώδικα.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Create the OCR engine – GPU if available, otherwise CPU
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;   // Latin covers most Western alphabets

        // The rest of the code lives in a separate method for clarity
        ProcessFolder(ocrEngine, @"C:\MyPngFolder");
    }

    // …
}
```

**Συμβουλή:** Αν τρέχεις σε headless server χωρίς GPU, μπορείς να αντικαταστήσεις το `GpuOcrEngine` με `OcrEngine` και ο κώδικας θα λειτουργεί ακριβώς το ίδιο.

## Βήμα 3 – Βρόχος μέσω εικόνων στον προορισμό φάκελο

Πρέπει να **βρόχομε μέσω εικόνων** και να επιλέγουμε μόνο αρχεία PNG. Η μέθοδος `Directory.GetFiles` κάνει το δύσκολο μέρος, και θα ελέγξουμε αν ο φάκελος είναι κενός.

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    if (!Directory.Exists(folderPath))
    {
        Console.WriteLine($"❌ Folder not found: {folderPath}");
        return;
    }

    // Grab every *.png file – this is the “read png files” part
    string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

    if (pngFiles.Length == 0)
    {
        Console.WriteLine("⚠️ No PNG files found. Make sure the folder contains .png images.");
        return;
    }

    foreach (var pngPath in pngFiles)
    {
        Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
        ExtractAndSave(engine, pngPath);
    }
}
```

Παρατήρησε τη χρήση του `SearchOption.TopDirectoryOnly`. Αν αργότερα χρειαστεί να επεξεργαστείς υποφακέλους, άλλαξε σε `AllDirectories`. Αυτή η μικρή αλλαγή σου επιτρέπει να **μετατρέπεις εικόνες σε κείμενο** σε ολόκληρο δέντρο με μία γραμμή.

## Βήμα 4 – Εκτέλεση OCR και αποθήκευση αποτελέσματος

Τώρα έρχεται η καρδιά της ροής **batch OCR εικόνων**. Φορτώνουμε κάθε PNG, καλούμε `Recognize()` και γράφουμε το εξαγόμενο κείμενο σε αρχείο `.txt` με το ίδιο όνομα.

```csharp
static void ExtractAndSave(OcrEngine engine, string imagePath)
{
    try
    {
        // Load the PNG into the engine
        engine.Image = ImageStream.FromFile(imagePath);

        // Run recognition – this returns a RecognitionResult object
        RecognitionResult result = engine.Recognize();

        // Build the output path (same name, .txt extension)
        string txtPath = Path.ChangeExtension(imagePath, ".txt");

        // Write the OCR text to disk
        File.WriteAllText(txtPath, result.Text);

        Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
    }
    catch (Exception ex)
    {
        // Edge case: corrupted PNG or unsupported format
        Console.WriteLine($"❗ Error processing {Path.GetFileName(imagePath)}: {ex.Message}");
    }
}
```

**Γιατί το τυλίγουμε σε try/catch;** Σε πραγματικές παρτίδες εικόνων συχνά υπάρχει κάποιο κατεστραμμένο αρχείο ή PNG με ασυνήθιστο χρωματικό προφίλ. Το catch αποτρέπει το σπάσιμο ολόκληρης της εκτέλεσης και επιτρέπει τη συνέχιση με τα υπόλοιπα αρχεία.

## Βήμα 5 – Εκτέλεση εφαρμογής και επαλήθευση εξόδου

Δοκίμασε και τρέξε την εφαρμογή:

```bash
dotnet run
```

Θα πρέπει να δεις κάτι σαν:

```
🔎 Processing: invoice1.png
✅ Saved: invoice1.txt
🔎 Processing: screenshot_2024.png
✅ Saved: screenshot_2024.txt
...
```

Άνοιξε οποιοδήποτε από τα δημιουργημένα `.txt` αρχεία—εκεί είναι το εξαγόμενο κείμενο. Αν κάποιο αρχείο είναι κενό, έλεγξε την ποιότητα της εικόνας· το OCR αποδίδει καλύτερα με καθαρό, υψηλής αντίθεσης κείμενο.

### Γρήγορο σκριπτάκι επαλήθευσης (προαιρετικό)

Αν θέλεις να βεβαιωθείς ότι κάθε PNG έχει το αντίστοιχο αρχείο κειμένου, τρέξε αυτό το μικρό PowerShell one‑liner:

```powershell
Get-ChildItem -Path "C:\MyPngFolder" -Filter *.png |
  ForEach-Object { 
    $txt = $_.BaseName + ".txt"
    if (-Not (Test-Path $txt)) { Write-Host "Missing: $txt" }
  }
```

## Συνηθισμένες παραλλαγές & Ακραίες περιπτώσεις

| Κατάσταση | Τι να αλλάξετε |
|-----------|----------------|
| **Μη‑λατινικά γλώσσες** (π.χ., Κυριλλικά) | Ορίστε `ocrEngine.Language = Language.Cyrillic;` |
| **Μεγάλο σύνολο εικόνων (>10 000 αρχεία)** | Χρησιμοποιήστε `Parallel.ForEach` για ταχύτερη επεξεργασία, αλλά παρακολουθήστε τη χρήση μνήμης GPU. |
| **Διατήρηση αρχικής σειράς εικόνων** | Ταξινομήστε το `pngFiles` πριν το `foreach` (`Array.Sort(pngFiles);`). |
| **Εκτέλεση σε CI server χωρίς GPU** | Αντικαταστήστε το `GpuOcrEngine` με `OcrEngine` για να αποφύγετε σφάλματα αρχικοποίησης GPU. |
| **Θέλετε να επεξεργαστείτε μόνο αρχεία που περιέχουν συγκεκριμένη λέξη-κλειδί** | Μετά την ανάκτηση του `result.Text`, ελέγξτε `result.Text.Contains("Invoice")` πριν γράψετε το αρχείο. |

Αυτές οι προσαρμογές σου επιτρέπουν να προσαρμόσεις τη **μετατροπή εικόνων σε κείμενο** σε σχεδόν οποιοδήποτε σενάριο.

## Πλήρης κώδικας (έτοιμος για copy‑paste)

```csharp
// ------------------------------------------------------------
// Extract Text from PNG – Batch OCR using Aspose.OCR (C#)
// ------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine (GPU if possible)
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;

        // 2️⃣ Define the folder that holds your PNG files
        string targetFolder = @"C:\MyPngFolder";   // <-- change to your path

        // 3️⃣ Process every PNG in the folder
        ProcessFolder(ocrEngine, targetFolder);
    }

    static void ProcessFolder(OcrEngine engine, string folderPath)
    {
        if (!Directory.Exists(folderPath))
        {
            Console.WriteLine($"❌ Folder not found: {folderPath}");
            return;
        }

        string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

        if (pngFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No PNG files found.");
            return;
        }

        foreach (var pngPath in pngFiles)
        {
            Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
            ExtractAndSave(engine, pngPath);
        }
    }

    static void ExtractAndSave(OcrEngine engine, string imagePath)
    {
        try
        {
            engine.Image = ImageStream.FromFile(imagePath);
            RecognitionResult result = engine.Recognize();

            string txtPath = Path.ChangeExtension(imagePath, ".txt");
            File.WriteAllText(txtPath, result.Text);

            Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❗ Error on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

Αποθήκευσε το ως `Program.cs`, τρέξε `dotnet run` και παρακολούθησε τη μαγεία.

## Συμπέρασμα

Τώρα διαθέτεις έναν **πλήρη, έτοιμο για παραγωγή τρόπο εξαγωγής κειμένου από PNG** αρχεία χρησιμοποιώντας C#. Ο οδηγός κάλυψε τα πάντα—from τη δημιουργία του project, την αρχικοποίηση ενός OCR engine με επιτάχυνση GPU, **βρόχο μέσω εικόνων**, μέχρι **batch OCR εικόνων** και αποθήκευση των αποτελεσμάτων ως απλό κείμενο.

Αν θέλεις να προχωρήσεις, δοκίμασε:

- **Μετατροπή εικόνων σε κείμενο** για άλλες μορφές (JPG, BMP

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}