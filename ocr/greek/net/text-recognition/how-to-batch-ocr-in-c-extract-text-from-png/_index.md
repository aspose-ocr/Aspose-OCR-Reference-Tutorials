---
category: general
date: 2026-03-26
description: Πώς η μαζική OCR σε C# καθιστά εύκολη την εξαγωγή κειμένου από αρχεία
  PNG. Ακολουθήστε αυτό το βήμα‑βήμα tutorial C# OCR για μαζική εξαγωγή κειμένου με
  το Aspose OCR.
draft: false
keywords:
- how to batch OCR
- extract text from png
- c# ocr tutorial
- how to create OCR
- batch text extraction
language: el
og_description: Πώς να κάνετε ομαδική OCR σε C# σας επιτρέπει να εξάγετε γρήγορα κείμενο
  από αρχεία PNG. Αυτός ο οδηγός σας καθοδηγεί μέσα από ένα πλήρες μάθημα OCR σε C#
  με ομαδική εξαγωγή κειμένου.
og_title: Πώς να κάνετε ομαδική OCR σε C# – Εξαγωγή κειμένου από PNG
tags:
- OCR
- C#
- Aspose
title: Πώς να κάνετε ομαδική OCR σε C# – Εξαγωγή κειμένου από PNG
url: /el/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να κάνετε batch OCR σε C# – Εξαγωγή κειμένου από PNG

Έχετε αναρωτηθεί ποτέ **πώς να κάνετε batch OCR** μια σειρά από στιγμιότυπα οθόνης χωρίς να γράψετε ξεχωριστό πρόγραμμα για κάθε αρχείο; Δεν είστε μόνοι. Σε πολλά έργα καταλήγουμε με δεκάδες PNG που χρειάζονται εξαγωγή κειμένου, και η επεξεργασία τους ένα‑ένα είναι ενοχλητική.  

Τα καλά νέα; Με το Aspose OCR μπορείτε να δημιουργήσετε μια μικρή εφαρμογή κονσόλας C# που επεξεργάζεται όλες αυτές τις εικόνες παράλληλα, παρέχοντάς σας γρήγορη **batch text extraction** και ένα καθαρό σύνολο αποτελεσμάτων. Σε αυτόν τον οδηγό θα περάσουμε από ένα πλήρες **c# ocr tutorial**, θα εξηγήσουμε γιατί κάθε μέρος είναι σημαντικό, και θα σας δείξουμε ακριβώς πώς φαίνεται η έξοδος.

Με το τέλος αυτού του άρθρου θα μπορείτε να:

* Φορτώσετε μια λίστα αρχείων PNG (ή οποιαδήποτε υποστηριζόμενη εικόνα) με μία κίνηση.  
* Διαμορφώσετε ένα κοινόχρηστο `OcrEngine` ώστε οι ρυθμίσεις να παραμένουν συνεπείς σε όλο το batch.  
* Εκτελέσετε την ουρά αναγνώρισης με έως και τέσσερις παράλληλους εργαζόμενους.  
* Αποκτήσετε το αναγνωρισμένο κείμενο για κάθε σελίδα και το εκτυπώσετε στην κονσόλα.

Κανένα μαγικό, μόνο σταθερός κώδικας που μπορείτε να ενσωματώσετε στη λύση σας σήμερα.

## Τι θα χρειαστείτε

Πριν βουτήξουμε, βεβαιωθείτε ότι έχετε:

* .NET 6 SDK (ή οποιαδήποτε πρόσφατη έκδοση .NET).  
* Ένα έγκυρο άδεια Aspose OCR ή ένα προσωρινό κλειδί αξιολόγησης.  
* Έναν φάκελο που περιέχει τα αρχεία PNG που θέλετε να επεξεργαστείτε.  
* Visual Studio 2022 ή τον αγαπημένο σας επεξεργαστή.

Αυτό είναι όλο—χωρίς επιπλέον πακέτα NuGet πέρα από το `Aspose.OCR` και το τυπικό `System.Collections.Generic`.

## Πώς να κάνετε batch OCR – Ρύθμιση του έργου

Πρώτα απ' όλα, δημιουργήστε ένα νέο έργο κονσόλας και προσθέστε τη βιβλιοθήκη Aspose OCR.

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

Αφού ολοκληρωθεί η επαναφορά, ανοίξτε το **Program.cs** (ή δημιουργήστε ένα νέο αρχείο) και προσθέστε τις συνήθεις οδηγίες `using`:

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
```

Αυτή η απλή δομή μας δίνει πρόσβαση στο `OcrEngine`, το `RecognitionQueue` και τις βοηθητικές κλάσεις που θα χρειαστούμε αργότερα.

## Εξαγωγή κειμένου από PNG – Προετοιμασία λίστας εικόνων

Τώρα πρέπει να πούμε στο πρόγραμμα **ποια PNG** θα περάσει από OCR. Ο πιο απλός τρόπος είναι να δημιουργήσετε μια `List<string>` που περιέχει απόλυτες ή σχετικές διαδρομές.

```csharp
// Step 1: Define the image files to be processed
var imagePaths = new List<string>
{
    @"YOUR_DIRECTORY/page1.png",
    @"YOUR_DIRECTORY/page2.png",
    @"YOUR_DIRECTORY/page3.png",
    @"YOUR_DIRECTORY/page4.png"
};
```

Αντικαταστήστε το `YOUR_DIRECTORY` με την πραγματική διαδρομή του φακέλου. Αν έχετε ένα δυναμικό σύνολο, μπορείτε επίσης να χρησιμοποιήσετε `Directory.GetFiles(@"YOUR_DIRECTORY", "*.png")` και να τροφοδοτήσετε το αποτέλεσμα στη λίστα. Το βασικό σημείο είναι ότι **extract text from PNG** είναι απλώς θέμα τροφοδότησης των σωστών ονομάτων αρχείων στην ουρά.

![Πώς να κάνετε batch OCR workflow](https://example.com/placeholder.png "Διάγραμμα που απεικονίζει πώς να κάνετε batch OCR μια συλλογή αρχείων PNG")

*Image alt text: how to batch OCR workflow diagram* → *Κείμενο εναλλακτικής εικόνας: διάγραμμα workflow batch OCR*

## C# OCR tutorial – Διαμόρφωση της ουράς αναγνώρισης

Η καρδιά της λειτουργίας batch είναι το `RecognitionQueue`. Σκεφτείτε το ως έναν ιμάντα μεταφοράς που παραδίδει κάθε εικόνα σε ένα κοινόχρηστο `OcrEngine`. Με το κοινόχρηστο engine κρατάμε τη χρήση μνήμης χαμηλή και εγγυόμαστε ταυτόσιμες ρυθμίσεις για κάθε σελίδα.

```csharp
// Step 2: Create a recognition queue with shared OCR engine and parallelism
var recognitionQueue = new RecognitionQueue
{
    MaxDegreeOfParallelism = 4,          // run up to 4 images at the same time
    Engine = new OcrEngine()            // shared configuration for all images
};
```

Γιατί να ορίσετε το `MaxDegreeOfParallelism` σε 4; Σε ένα τυπικό quad‑core laptop αυτό προσφέρει τη βέλτιστη απόδοση χωρίς να «πνίγει» το λειτουργικό σύστημα. Αν τρέχετε σε διακομιστή με περισσότερους πυρήνες, αυξήστε τον αριθμό ανάλογα.

### Συμβουλή

Αν χρειάζεστε προσαρμοσμένα πακέτα γλώσσας, ρυθμίσεις DPI ή περικοπή περιοχής‑ενδιαφέροντος, κάντε το **μια φορά** στο κοινόχρηστο `Engine` πριν προσθέσετε εικόνες στην ουρά. Για παράδειγμα:

```csharp
recognitionQueue.Engine.Language = Language.English;
recognitionQueue.Engine.Dpi = 300;
```

Όλες οι επόμενες αναγνωρίσεις κληρονομούν αυτές τις επιλογές αυτόματα—αυτή είναι η ουσία του **how to create OCR** pipelines που παραμένουν συνεπή.

## Batch εξαγωγή κειμένου – Προσθήκη εικόνων στην ουρά και εκτέλεση της ουράς

Με την ουρά έτοιμη, το επόμενο βήμα είναι να προσθέσετε κάθε εικόνα σε αυτήν. Η μέθοδος `Enqueue` δέχεται ένα αντικείμενο `OcrImage`, το οποίο δημιουργούμε από μια διαδρομή αρχείου.

```csharp
// Step 3: Enqueue each image for OCR processing
foreach (var path in imagePaths)
    recognitionQueue.Enqueue(OcrImage.FromFile(path));
```

Μόλις όλες οι εικόνες προστεθούν στην ουρά, ξεκινάμε την επεξεργασία:

```csharp
// Step 4: Run the queue and collect OCR results
List<OcrResult> ocrResults = recognitionQueue.ExecuteAll();
```

Το `ExecuteAll` μπλοκάρει μέχρι να ολοκληρωθεί κάθε εικόνα, στη συνέχεια επιστρέφει μια λίστα όπου κάθε στοιχείο αντιστοιχεί στη σειρά εισόδου. Αυτό εγγυάται ότι το αποτέλεσμα της σελίδας 1 βρίσκεται στο δείκτη 0, της σελίδας 2 στο δείκτη 1, κ.ο.κ.—χρήσιμο όταν χρειάζεται να αντιστοιχίσετε τα αποτελέσματα στα αρχικά αρχεία.

## Πώς να δημιουργήσετε OCR – Εμφάνιση των αποτελεσμάτων

Τέλος, ας εκτυπώσουμε το αναγνωρισμένο κείμενο στην κονσόλα. Εδώ βλέπετε πραγματικά την **batch text extraction** σε δράση.

```csharp
// Step 5: Output the recognized text for each page
for (int i = 0; i < ocrResults.Count; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

Όταν εκτελέσετε το πρόγραμμα (`dotnet run`), θα πρέπει να δείτε κάτι σαν:

```
--- Page 1 ---
Welcome to the quarterly report.
--- Page 2 ---
Revenue increased by 12% YoY.
--- Page 3 ---
All figures are provisional.
--- Page 4 ---
Contact finance@example.com for details.
```

Αν κάποια εικόνα αποτύχει (π.χ., κατεστραμμένο αρχείο), το αντίστοιχο `OcrResult` θα έχει κενή ιδιότητα `Text` και μπορείτε να ελέγξετε το `ocrResults[i].Exception` για διαγνωστικά.

## Πώς να δημιουργήσετε OCR – Συμβουλές, ειδικές περιπτώσεις και βέλτιστες πρακτικές

### Διαχείριση μεγάλων batch

Η επεξεργασία εκατοντάδων PNG μπορεί ακόμα να καταναλώνει μνήμη αν κρατάτε όλα τα αντικείμενα `OcrResult` ενεργά. Σε τέτοιες περιπτώσεις, ρέξτε την έξοδο σε αρχείο ή βάση δεδομένων αμέσως μόλις φτάσει κάθε αποτέλεσμα:

```csharp
recognitionQueue.OnResultReady += (sender, args) =>
{
    File.AppendAllText("OcrOutput.txt",
        $"--- {args.Image.Path} ---{Environment.NewLine}{args.Result.Text}{Environment.NewLine}");
};
```

### Αντιμετώπιση μη‑PNG μορφών

Το Aspose OCR υποστηρίζει επίσης JPEG, BMP και TIFF έτοιμα. Απλώς αλλάξτε την επέκταση αρχείου στη λίστα σας ή χρησιμοποιήστε αναζήτηση με μπαλαντέρ. Τα ίδια βήματα του **c# ocr tutorial** ισχύουν—χωρίς ανάγκη αλλαγής κώδικα.

### Παράλειψη κενών σελίδων

Αν έχετε σαρωμένα PDF που μερικές φορές περιέχουν κενές σελίδες, μπορείτε να φιλτράρετε τα αποτελέσματα:

```csharp
if (!string.IsNullOrWhiteSpace(result.Text))
    // process non‑empty text
```

### Σκέψεις για την άδεια

Η έκδοση αξιολόγησης τοποθετεί υδατογράφημα σε κάθε σελίδα. Για παραγωγική χρήση, βεβαιωθείτε ότι ενσωματώνετε το αρχείο άδειας στην αρχή του `Main`:

```csharp
License lic = new License();
lic.SetLicense("Aspose.OCR.lic");
```

### Ρύθμιση παραλληλισμού

Το `MaxDegreeOfParallelism` προεπιλογή είναι το `Environment.ProcessorCount`. Αν παρατηρήσετε υψηλή χρήση CPU ή πίεση μνήμης, μειώστε την τιμή. Αντίστροφα, σε ένα cloud VM με πολλούς πυρήνες, αυξήστε το για να εκμεταλλευτείτε πλήρως το υλικό.

## Σύνοψη

Τώρα έχετε μια πλήρη λύση **how to batch OCR** σε C# που μπορεί να **extract text from PNG** αρχεία, να τα εκτελεί παράλληλα και να σας δίνει καθαρά, διατεταγμένα αποτελέσματα. Με το κοινόχρηστο `OcrEngine` έχετε μάθει **how to create OCR** pipelines που είναι τόσο αποδοτικά στη μνήμη όσο και εύκολα στη συντήρηση. Αυτό το **c# ocr tutorial** δείχνει επίσης πώς να κλιμακώσετε σε **batch text extraction** για εκατοντάδες εικόνες με λίγες επιπλέον γραμμές κώδικα.

---

### Τι θα ακολουθήσει;

* Δοκιμάστε να προσθέσετε αυτόματη ανίχνευση γλώσσας (`Engine.Language = Language.AutoDetect`).  
* Πειραματιστείτε με μορφές εξόδου—γράψτε τα αποτελέσματα σε JSON ή CSV για επακόλουθη ανάλυση.  
* Συνδυάστε αυτό το batch OCR με βήμα μετατροπής PDF‑σε‑εικόνα για επεξεργασία ολόκληρων σαρωμένων εγγράφων.

Νιώστε ελεύθεροι να ρυθμίσετε τον παραλληλισμό, να αντικαταστήσετε τις πηγές εικόνων ή να ενσωματώσετε τα αποτελέσματα σε ευρετήριο αναζήτησης. Ο ουρανός είναι το όριο όταν κυριαρχήσετε στο **how to batch OCR** σε C#.

Καλή προγραμματιστική, και οι εκτελέσεις OCR σας να είναι γρήγορες και χωρίς σφάλματα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}