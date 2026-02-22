---
category: general
date: 2026-02-22
description: Πώς να κάνετε ομαδική OCR εικόνων JPEG σε C# με το Aspose.OCR. Μάθετε
  να εξάγετε κείμενο από jpg, να μετατρέπετε jpg σε txt και να επεξεργάζεστε εικόνες
  ομαδικά αποδοτικά.
draft: false
keywords:
- how to batch ocr
- extract text from jpg
- convert jpg to txt
- batch process images
- c# ocr example
language: el
og_description: Πώς να εκτελέσετε ομαδική OCR σε εικόνες JPEG με C# χρησιμοποιώντας
  το Aspose.OCR. Αυτό το σεμινάριο σας δείχνει πώς να εξάγετε κείμενο από jpg, να
  μετατρέψετε jpg σε txt και να επεξεργαστείτε εικόνες ομαδικά σε λίγα λεπτά.
og_title: Πώς να εκτελέσετε ομαδική OCR σε εικόνες JPEG με C# – Πλήρης οδηγός
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Πώς να κάνετε ομαδική OCR εικόνων JPEG σε C# – Πλήρης οδηγός
url: /el/net/text-recognition/how-to-batch-ocr-jpeg-images-in-c-complete-guide/
---

: none. Ensure code block placeholders remain unchanged.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εκτελέσετε OCR σε Παρτίδες σε Εικόνες JPEG σε C# – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να εκτελέσετε OCR σε παρτίδες** έναν φάκελο γεμάτο εικόνες χωρίς να γράψετε ξεχωριστό πρόγραμμα για κάθε αρχείο; Σε αυτόν τον οδηγό θα σας δείξουμε ακριβώς **πώς να εκτελέσετε OCR σε παρτίδες** αρχεία JPEG χρησιμοποιώντας το Aspose.OCR, ώστε να μπορείτε **να εξάγετε κείμενο από jpg** και **να μετατρέψετε jpg σε txt** με λίγες μόνο γραμμές κώδικα.  

Αν έχετε ποτέ κοίταξει σε έναν φάκελο με σαρωμένα τιμολόγια και σκεφτείτε, «Πρέπει να υπάρχει πιο γρήγορος τρόπος», βρίσκεστε στο σωστό μέρος. Θα περάσουμε από κάθε βήμα, θα εξηγήσουμε γιατί κάθε μέρος είναι σημαντικό, και θα προσθέσουμε μερικές επαγγελματικές συμβουλές για τη διαχείριση μεγάλων παρτίδων.

## Τι Θα Δημιουργήσετε

* Σαρώνει έναν δοσμένο φάκελο για αρχεία `*.jpg`.  
* Στέλνει κάθε εικόνα μέσω της μηχανής Aspose OCR (επιταχυνόμενη από GPU εάν έχετε κατάλληλη κάρτα).  
* Γράφει το αναγνωρισμένο κείμενο σε αρχείο `.txt` που βρίσκεται δίπλα στην αρχική εικόνα.  

Χωρίς εξωτερικές υπηρεσίες, χωρίς χειροκίνητο αντιγραφή‑επικόλληση—μόνο καθαρό C# και μια αξιόπιστη βιβλιοθήκη OCR.

### Προαπαιτούμενα

* .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.8).  
* Visual Studio 2022 ή οποιονδήποτε επεξεργαστή που υποστηρίζει C#.  
* Ένα πακέτο NuGet Aspose.OCR (η δωρεάν δοκιμή λειτουργεί για δοκιμές).  

Αν λείπει κάποιο από αυτά, κάντε παύση τώρα και εγκαταστήστε το· το υπόλοιπο του οδηγού υποθέτει ότι είναι ήδη στη θέση τους.

![How to batch OCR example](/images/how-to-batch-ocr.png "how to batch ocr diagram")

## Βήμα 1: Εγκατάσταση του Πακέτου NuGet Aspose.OCR

Πρώτα απ' όλα—το έργο σας χρειάζεται τη βιβλιοθήκη OCR. Ανοίξτε ένα τερματικό στον φάκελο της λύσης και εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

Ή χρησιμοποιήστε το UI του NuGet Package Manager στο Visual Studio. Αυτό θα κατεβάσει όλα όσα χρειάζεστε, συμπεριλαμβανομένων των δυαδικών αρχείων με υποστήριξη GPU εάν το μηχάνημά σας τα υποστηρίζει.

> **Συμβουλή επαγγελματία:** Εάν σκοπεύετε να το εκτελέσετε σε διακομιστή χωρίς GPU, ορίστε `UseGpu = false` αργότερα· η μηχανή θα επιστρέψει αυτόματα στην CPU.

## Βήμα 2: Διαμόρφωση της Μηχανής OCR

Η δημιουργία και διαμόρφωση του `OcrEngine` είναι το σημείο όπου ξεκινά η μαγεία. Θα πείτε στη μηχανή ποια γλώσσα να περιμένει, αν θα χρησιμοποιήσει το GPU, και σε ποια μορφή πρέπει να είναι η έξοδος.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// ...

// Step 2: Initialize and configure the OCR engine
var ocrEngine = new OcrEngine
{
    // English works for most documents; change if you need another language.
    Language = Language.English,

    // Enable GPU for faster processing on supported hardware.
    UseGpu = true,

    // We only need plain text for our .txt files.
    OutputFormat = OutputFormat.Text
};
```

**Γιατί είναι σημαντικό:** Ο ορισμός του `Language` βελτιώνει την ακρίβεια επειδή η μηχανή μπορεί να περιορίσει τα σύνολα χαρακτήρων. Η ενεργοποίηση του `UseGpu` μπορεί να μειώσει τον χρόνο επεξεργασίας κατά το ήμισυ σε μια σύγχρονη κάρτα γραφικών, κάτι που είναι πραγματικό πλεονέκτημα όταν κάνετε **επεξεργασία εικόνων σε παρτίδες**.

## Βήμα 3: Αναγνώριση Όλων των Αρχείων JPEG σε Φάκελο

Τώρα αφήνουμε το Aspose να κάνει τη βαριά δουλειά. Η στατική μέθοδος `BatchProcessor.RecognizeFolder` περιηγείται στον φάκελο, εκτελεί OCR σε κάθε αντίστοιχο αρχείο και επιστρέφει μια συλλογή αποτελεσμάτων.

```csharp
using System.Collections.Generic;

// ...

// Step 3: Run OCR on every *.jpg in the target directory
IList<OcrResult> ocrResults = BatchProcessor.RecognizeFolder(
    ocrEngine,
    @"C:\Images\Invoices",   // <-- replace with your folder path
    searchPattern: "*.jpg"); // Only JPEG files are processed
```

**Διαχείριση ειδικών περιπτώσεων:** Εάν ο φάκελος περιέχει υποφακέλους, μπορείτε να προσθέσετε την υπερφόρτωση `SearchOption.AllDirectories` (ή να επαναλάβετε χειροκίνητα) ώστε να βεβαιωθείτε ότι δεν θα χάσετε κανένα αρχείο.

## Βήμα 4: Γράψτε Κάθε Αποτέλεσμα σε Αντίστοιχο Αρχείο `.txt`

Τα αντικείμενα `OcrResult` περιέχουν τη διαδρομή του αρχικού αρχείου και το αναγνωρισμένο κείμενο. Επανάλαβε τα, άλλαξε την επέκταση και γράψε την έξοδο.

```csharp
using System.IO;

// ...

// Step 4: Persist OCR results as .txt files next to the source images
foreach (var result in ocrResults)
{
    // Change "image.jpg" → "image.txt"
    string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");

    // Save the extracted text
    File.WriteAllText(txtFilePath, result.Text);
}
```

Αυτό είναι—κάθε JPEG έχει τώρα ένα αδελφό αρχείο κειμένου που μπορείτε να τροφοδοτήσετε σε επόμενες διαδικασίες, ευρετήρια αναζήτησης ή απλώς να το αρχειοθετήσετε.

## Βήμα 5: Εκτελέστε την Εφαρμογή και Επαληθεύστε την Έξοδο

Συγκεντρώστε και εκτελέστε το πρόγραμμα:

```bash
dotnet run
```

Υποθέτοντας ότι ο φάκελος περιέχει `invoice1.jpg` και `receipt2.jpg`, θα πρέπει να δείτε τα `invoice1.txt` και `receipt2.txt` να εμφανίζονται δίπλα τους. Ανοίξτε οποιοδήποτε από τα αρχεία `.txt`; θα βρείτε την ακατέργαστη έξοδο OCR, π.χ.:

```
Invoice #12345
Date: 02/15/2026
Total: $1,234.56
Thank you for your business!
```

Εάν το κείμενο φαίνεται ακατάστατο, ελέγξτε ξανά ότι οι πηγαίες εικόνες έχουν υψηλή αντίθεση και ότι η ιδιότητα `Language` ταιριάζει με τη γλώσσα του εγγράφου.

## Βήμα 6: Προχωρημένες Ρυθμίσεις (Προαιρετικό)

### α) Διαχείριση Σαρώσεων Χαμηλής Ποιότητας

Μερικές φορές τα JPEG είναι θορυβώδη. Μπορείτε να προεπεξεργαστείτε τις εικόνες με Aspose.Imaging ή οποιαδήποτε άλλη βιβλιοθήκη:

```csharp
using Aspose.Imaging;
using Aspose.Imaging.ImageOptions;

// Example: increase contrast before OCR
using (var image = Image.Load(result.SourceFilePath))
{
    image.Contrast = 30; // boost contrast
    image.Save(result.SourceFilePath); // overwrite or save to temp file
}
```

### β) Παράλληλη Επεξεργασία της Παρτίδας

Εάν έχετε πολλά αρχεία και CPU πολλαπλών πυρήνων, τυλίξτε το βρόχο σε `Parallel.ForEach`:

```csharp
Parallel.ForEach(ocrResults, result =>
{
    string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");
    File.WriteAllText(txtFilePath, result.Text);
});
```

Απλώς να γνωρίζετε ότι η μηχανή Aspose OCR δεν είναι ασφαλής για νήματα· θα χρειαστείτε ξεχωριστό αντικείμενο `OcrEngine` ανά νήμα ή να χρησιμοποιήσετε μια ταυτόχρονη ουρά.

### γ) Καταγραφή και Διαχείριση Σφαλμάτων

Μια αξιόπιστη λύση καταγράφει αποτυχίες ώστε να μπορείτε να τις δοκιμάσετε ξανά αργότερα:

```csharp
try
{
    // OCR and write logic here
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed on {result.SourceFilePath}: {ex.Message}");
    // Optionally write to a log file
}
```

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα, εδώ είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε μια νέα Console App:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;
using System.Collections.Generic;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create and configure the OCR engine
        var ocrEngine = new OcrEngine
        {
            Language = Language.English,
            UseGpu = true,
            OutputFormat = OutputFormat.Text
        };

        // 2️⃣ Recognize all JPEG images in the target folder
        IList<OcrResult> ocrResults = BatchProcessor.RecognizeFolder(
            ocrEngine,
            @"C:\Images\Invoices",   // <-- change to your directory
            searchPattern: "*.jpg");

        // 3️⃣ Write each OCR result to a matching .txt file
        foreach (var result in ocrResults)
        {
            string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");
            File.WriteAllText(txtFilePath, result.Text);
        }

        Console.WriteLine("Batch OCR complete. Check the folder for .txt files.");
    }
}
```

Τρέξτε το, παρακολουθήστε την έξοδο της κονσόλας, και στη συνέχεια ανοίξτε μερικά αρχεία `.txt` για να επιβεβαιώσετε ότι το βήμα **εξαγωγής κειμένου από jpg** πέτυχε.  

---

## Συμπέρασμα

Μόλις καλύψαμε **πώς να εκτελέσετε OCR σε παρτίδες** μια συλλογή εικόνων JPEG σε C# χρησιμοποιώντας το Aspose.OCR, μετατρέποντας κάθε εικόνα σε ένα αναζητήσιμο αρχείο `.txt`. Η λύση είναι συμπαγής, ευαίσθητη στο GPU, και εύκολη στην επέκταση για διαχείριση σφαλμάτων, προεπεξεργασία εικόνας ή παράλληλη εκτέλεση.  

Αν είστε έτοιμοι να προχωρήσετε παραπέρα, σκεφτείτε τα επόμενα βήματα:

* **Επεξεργασία εικόνων σε παρτίδες** άλλων μορφών (`*.png`, `*.tif`) τροποποιώντας το `searchPattern`.  
* Συνδυάστε την έξοδο με μια μηχανή πλήρους κειμένου όπως το Lucene.NET για άμεση αναζήτηση εγγράφων.  
* Εξερευνήστε τις δυνατότητες μετατροπής PDF του Aspose για να δημιουργήσετε αναζητήσιμα PDF απευθείας από τα αποτελέσματα OCR.  

Νιώστε ελεύθεροι να πειραματιστείτε—αλλάξτε τη γλώσσα, απενεργοποιήστε το GPU, ή διοχετεύστε το κείμενο σε μια βάση δεδομένων. Το βασικό μοτίβο παραμένει το ίδιο, και τώρα έχετε μια σταθερή βάση για να χτίσετε πάνω της.

Καλή κωδικοποίηση, και εύχομαι οι OCR αγωγοί σας να είναι πάντα γρήγοροι και ακριβείς!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}