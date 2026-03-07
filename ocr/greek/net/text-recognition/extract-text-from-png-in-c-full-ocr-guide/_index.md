---
category: general
date: 2026-03-07
description: Εξάγετε κείμενο από αρχεία PNG χρησιμοποιώντας C#. Μάθετε πώς να μετατρέπετε
  εικόνα σε κείμενο με C# και να διαβάζετε κείμενο από σαρωμένες εικόνες γρήγορα.
draft: false
keywords:
- extract text from png
- convert image to text c#
- read text from scanned images
- how to run ocr on images
language: el
og_description: Εξαγωγή κειμένου από αρχεία PNG χρησιμοποιώντας C#. Αυτός ο οδηγός
  δείχνει πώς να μετατρέψετε εικόνα σε κείμενο με C# και να διαβάσετε κείμενο από
  σαρωμένες εικόνες με το Aspose OCR.
og_title: Εξαγωγή κειμένου από PNG σε C# – Πλήρης οδηγός OCR
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Εξαγωγή κειμένου από PNG σε C# – Πλήρης οδηγός OCR
url: /el/net/text-recognition/extract-text-from-png-in-c-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από PNG σε C# – Πλήρης Οδηγός OCR

Έχετε χρειαστεί ποτέ να **εξάγετε κείμενο από PNG** αρχεία αλλά δεν ήξερατε από πού να ξεκινήσετε; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το εμπόδιο όταν αντιμετωπίζουν σαρωμένα γραφικά ή στιγμιότυπα οθόνης που πρέπει να γίνουν αναζητήσιμο κείμενο. Τα καλά νέα; Με λίγες γραμμές C# και Aspose OCR μπορείτε να μετατρέψετε οποιοδήποτε PNG σε επεξεργάσιμες συμβολοσειρές σε μια στιγμή.

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία: από τον εντοπισμό PNG στο δίσκο, την εκκίνηση OCR εργασιών παράλληλα, μέχρι την εμφάνιση μιας καθαρής προεπισκόπησης κάθε αποτελέσματος. Στο τέλος θα ξέρετε πώς να **μετατρέψετε εικόνα σε κείμενο C#**, θα μπορείτε να **διαβάζετε κείμενο από σαρωμένες εικόνες** αποδοτικά, και θα δείτε τον καλύτερο τρόπο να **τρέξετε OCR σε εικόνες** χωρίς να καταστρέψετε το UI thread.

## Τι Θα Χρειαστείτε

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Core και .NET Framework)  
- Πακέτο NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- Ένας φάκελος γεμάτος *.png* αρχεία που θέλετε να επεξεργαστείτε  
- Οποιοδήποτε IDE προτιμάτε (Visual Studio, VS Code, Rider…)

Δεν απαιτείται επιπλέον διαμόρφωση· η βιβλιοθήκη περιλαμβάνει όλα όσα χρειάζονται για την αποκωδικοποίηση PNG, JPEG, TIFF, ό,τι και αν είναι.

## Βήμα 1: Εντοπισμός Όλων των PNG Αρχείων – Η “Εξαγωγή Κειμένου από PNG” Ξεκινά

Πρώτα πρέπει να βρούμε κάθε PNG στο οποίο θέλουμε να τρέξουμε OCR. Η χρήση του `Directory.GetFiles` είναι γρήγορη και αξιόπιστη.

```csharp
// Step 1: Find all PNG images in the input folder
string[] imageFiles = Directory.GetFiles("YOUR_DIRECTORY", "*.png");

// Quick sanity check – throw if nothing was found
if (imageFiles.Length == 0)
    throw new FileNotFoundException("No PNG files found in the specified folder.");
```

*Γιατί είναι σημαντικό:* Η σάρωση του καταλόγου μία φορά κρατά το υπόλοιπο pipeline απλό, και ο πρώιμος έλεγχος αποτρέπει μια σιωπηλή κατάσταση “χωρίς έξοδο” που μπορεί να είναι δύσκολο να εντοπιστεί αργότερα.

## Βήμα 2: Εκκίνηση Παράλληλων OCR Εργασιών – Αποτελεσματικό **run OCR on images**

Η εκτέλεση OCR διαδοχικά είναι αποδεκτή για λίγα αρχεία, αλλά σε πραγματικά έργα συχνά αντιμετωπίζουμε δεκάδες ή εκατοντάδες. Με την εκκίνηση ενός `Task` ανά εικόνα κρατάμε την CPU απασχολημένη ενώ η βιβλιοθήκη κάνει το βαρέως τύπου έργο.

```csharp
// Step 2: Prepare a list to hold OCR tasks (one per image)
var ocrTasks = new List<Task<string>>();

// Step 3: Launch a parallel task for each image
foreach (var filePath in imageFiles)
{
    ocrTasks.Add(Task.Run(() =>
    {
        // Load the image and run OCR
        var engine = new OcrEngine();
        engine.Image = ImageStream.FromFile(filePath);
        engine.Recognize();
        return engine.Text;          // This is the extracted string
    }));
}
```

*Συμβουλή:* Το `Task.Run` εκχωρεί τη δουλειά στο thread pool, πράγμα που σημαίνει ότι το UI σας (αν υπάρχει) παραμένει αντιδραστικό. Αν τρέχετε σε διακομιστή, το ίδιο μοτίβο κλιμακώνεται ωραία σε πολλούς πυρήνες.

## Βήμα 3: Αναμονή Όλων των Εργασιών – Συλλογή των Αποτελεσμάτων

Τώρα περιμένουμε να ολοκληρωθεί κάθε λειτουργία OCR. Το `Task.WhenAll` επιστρέφει έναν πίνακα που ευθυγραμμίζεται με τη σειρά των αρχικών αρχείων, κάνοντας εύκολο το ζευγάρισμα αποτελεσμάτων με ονόματα αρχείων.

```csharp
// Step 4: Await all tasks and gather the recognized texts
string[] ocrResults = await Task.WhenAll(ocrTasks);
```

*Σημείωση για ειδικές περιπτώσεις:* Αν κάποιο μόνο εικόνα προκαλέσει εξαίρεση (κατεστραμμένο αρχείο, μη υποστηριζόμενη μορφή) ολόκληρο το `WhenAll` θα προωθήσει την εξαίρεση. Μπορείτε να τυλίξετε το εσωτερικό `Task.Run` σε try/catch και να επιστρέψετε κενή συμβολοσειρά ή διαγνωστικό μήνυμα αν χρειάζεστε ανθεκτικότητα σε σφάλματα.

## Βήμα 4: Εμφάνιση Προεπισκόπησης – Επαλήθευση του **convert image to text C#** αποτελέσματος

Μια γρήγορη προεπισκόπηση σας βοηθά να επιβεβαιώσετε ότι το OCR λειτούργησε πριν αρχίσετε να αποθηκεύετε τα δεδομένα κάπου αλλού.

```csharp
// Step 5: Show a short preview of each result
for (int i = 0; i < ocrResults.Length; i++)
{
    string fileName = Path.GetFileName(imageFiles[i]);
    string preview = ocrResults[i].Length > 100
        ? ocrResults[i][..100] + "..."
        : ocrResults[i];
    Console.WriteLine($"{fileName}: {preview}");
}
```

Τυπική έξοδος κονσόλας μοιάζει με:

```
invoice-001.png: Invoice Number: 2025-07-14   Date: 07/14/2025   Total: $1,250.00...
receipt-202.png: Thank you for your purchase!   Order #12345   Amount: $89.99...
```

Αν η προεπισκόπηση εμφανίζει ακαταλαβίστικο κείμενο, ελέγξτε ξανά την ποιότητα της εικόνας ή σκεφτείτε προεπεξεργασία (π.χ., δυαδικοποίηση) – αλλά για τις περισσότερες καθαρές PNG, το Aspose OCR το κάνει σωστά στην πρώτη προσπάθεια.

## Προαιρετικό: Αποθήκευση Αποτελεσμάτων σε CSV – Πραγματική Χρήση

Τα περισσότερα έργα χρειάζονται το εξαγόμενο κείμενο σε δομημένη μορφή. Παρακάτω υπάρχει ένας μικρός βοηθός που γράφει το όνομα αρχείου και το πλήρες OCR κείμενο σε αρχείο CSV.

```csharp
string csvPath = Path.Combine("YOUR_DIRECTORY", "ocr-results.csv");
using var writer = new StreamWriter(csvPath);
writer.WriteLine("FileName,ExtractedText");

for (int i = 0; i < imageFiles.Length; i++)
{
    string escaped = ocrResults[i].Replace("\"", "\"\"");
    writer.WriteLine($"\"{Path.GetFileName(imageFiles[i])}\",\"{escaped}\"");
}
Console.WriteLine($"All results saved to {csvPath}");
```

Τώρα μπορείτε να εισάγετε το CSV στο Excel, Power BI, ή σε οποιοδήποτε σύστημα που περιμένει **read text from scanned images**.

## Συχνές Ερωτήσεις

**Τι γίνεται αν τα PNG μου είναι τεράστια (πάνω από 5 MB);**  
Το Aspose OCR αυτόματα μειώνει το μέγεθος των μεγάλων εικόνων για να διατηρήσει τη χρήση μνήμης λογική, αλλά μπορείτε να αλλάξετε το μέγεθος χειροκίνητα με `engine.Image = ImageStream.FromFile(filePath).Resize(2000, 0);` ώστε να περιορίσετε το πλάτος στα 2000 px διατηρώντας την αναλογία.

**Μπορώ να το τρέξω σε Linux;**  
Ναι. Το Aspose OCR είναι cross‑platform· απλώς βεβαιωθείτε ότι οι εγγενείς εξαρτήσεις (`libgdiplus` σε ορισμένες διανομές) είναι εγκατεστημένες.

**Η γλώσσα OCR είναι προεπιλεγμένα στα Αγγλικά;**  
Σωστά. Αν χρειάζεστε άλλη γλώσσα, ορίστε `engine.Language = OcrLanguage.French;` (ή οποιοδήποτε υποστηριζόμενο enum) πριν καλέσετε το `Recognize()`.

**Πώς διαχειρίζομαι PDF με κωδικό πρόσβασης που περιέχουν PNG;**  
Μετατρέψτε πρώτα τις σελίδες PDF σε εικόνες (χρησιμοποιώντας Aspose PDF ή άλλη βιβλιοθήκη), μετά τροφοδοτήστε τα PNG στην ίδια pipeline. Η αρχή του **how to run OCR on images** παραμένει αμετάβλητη.

## Πλήρες Παράδειγμα (Async Main)

Ακολουθεί ένα αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα console project. Περιλαμβάνει όλα τα παραπάνω κομμάτια, καθώς και έναν μικρό βοηθό για την επικύρωση του φακέλου εισόδου.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        // -------------------------------------------------
        // 1️⃣ Locate PNGs – the heart of “extract text from png”
        // -------------------------------------------------
        const string folder = @"YOUR_DIRECTORY";   // <-- change this
        if (!Directory.Exists(folder))
        {
            Console.WriteLine($"Folder not found: {folder}");
            return;
        }

        string[] imageFiles = Directory.GetFiles(folder, "*.png");
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to do.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Fire off OCR tasks – best way to “run OCR on images”
        // -------------------------------------------------
        var ocrTasks = new List<Task<string>>();
        foreach (var filePath in imageFiles)
        {
            ocrTasks.Add(Task.Run(() =>
            {
                var engine = new OcrEngine();
                engine.Image = ImageStream.FromFile(filePath);
                engine.Recognize();
                return engine.Text;
            }));
        }

        // -------------------------------------------------
        // 3️⃣ Await results
        // -------------------------------------------------
        string[] ocrResults = await Task.WhenAll(ocrTasks);

        // -------------------------------------------------
        // 4️⃣ Show previews
        // -------------------------------------------------
        for (int i = 0; i < ocrResults.Length; i++)
        {
            string fileName = Path.GetFileName(imageFiles[i]);
            string preview = ocrResults[i].Length > 100
                ? ocrResults[i][..100] + "..."
                : ocrResults[i];
            Console.WriteLine($"{fileName}: {preview}");
        }

        // -------------------------------------------------
        // 5️⃣ Optional: write CSV – perfect for “read text from scanned images”
        // -------------------------------------------------
        string csvPath = Path.Combine(folder, "ocr-results.csv");
        using var writer = new StreamWriter(csvPath);
        writer.WriteLine("FileName,ExtractedText");
        for (int i = 0; i < imageFiles.Length; i++)
        {
            string escaped = ocrResults[i].Replace("\"", "\"\"");
            writer.WriteLine($"\"{Path.GetFileName(imageFiles[i])}\",\"{escaped}\"");
        }

        Console.WriteLine($"✅ OCR complete – results saved to {csvPath}");
    }
}
```

**Αναμενόμενη έξοδος** (παράδειγμα για δύο PNG):

```
invoice-001.png: Invoice Number: 2025-07-14   Date: 07/14/2025   Total: $1,250.00...
receipt-202.png: Thank you for your purchase!   Order #12345   Amount: $89.99...
✅ OCR complete – results saved to C:\MyImages\ocr-results.csv
```

## Συμπέρασμα

Καλύψαμε όλα όσα χρειάζεστε για να **εξάγετε κείμενο από PNG** αρχεία χρησιμοποιώντας C#. Από τον εντοπισμό των αρχείων, την εκκίνηση παράλληλων εργασιών OCR, την προεπισκόπηση των συμβολοσειρών, μέχρι την αποθήκευσή τους σε CSV—αυτός ο οδηγός παρέχει ένα έτοιμο για παραγωγή πρότυπο για σενάρια **convert image to text C#**.  

Αν είστε έτοιμοι για το επόμενο βήμα, δοκιμάστε να τροφοδοτήσετε την ίδια pipeline με JPEG ή TIFF αρχεία, πειραματιστείτε με διαφορετικές γλώσσες OCR, ή συνδέστε τα αποτελέσματα με έναν δείκτη αναζήτησης ώστε να μπορείτε άμεσα να **read text from scanned images**.  

Έχετε ερωτήσεις για ειδικές περιπτώσεις, βελτιστοποίηση απόδοσης ή άδειες; Αφήστε ένα σχόλιο ή επικοινωνήστε με την κοινότητα Aspose—καλή προγραμματιστική!

![Παράδειγμα εξαγωγής κειμένου από PNG](extract-text-png.png "Εξαγωγή κειμένου από PNG χρησιμοποιώντας Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}