---
category: general
date: 2026-09-13
description: Πώς να εκτελέσετε ομαδική OCR με το Aspose OCR GPU σε C# χρησιμοποιώντας
  .NET. Μάθετε πώς να αναγνωρίζετε κείμενο από εικόνες, να εξάγετε κείμενο από αρχεία
  TIFF και να επιταχύνετε την επεξεργασία με υποστήριξη GPU.
draft: false
keywords:
- aspose ocr gpu
- process multiple images
- how to batch ocr
- install aspose ocr
lastmod: 2026-09-13
og_description: Πώς να εκτελέσετε ομαδική OCR με το Aspose OCR GPU σε C# χρησιμοποιώντας
  .NET. Αυτός ο οδηγός σας δείχνει πώς να αναγνωρίζετε κείμενο από εικόνες, να εξάγετε
  κείμενο από αρχεία TIFF και να αξιοποιήσετε την επιτάχυνση GPU για επεξεργασία υψηλής
  απόδοσης.
og_image_alt: Screenshot of Aspose OCR GPU batch processing console output in C#
og_title: Πώς να εκτελέσετε ομαδική OCR με το Aspose OCR GPU σε C# χρησιμοποιώντας
  .NET
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: How to batch OCR with Aspose OCR GPU in C# using .NET. Learn to recognize
    text from images, extract text from TIFF files, and accelerate processing with
    GPU support.
  headline: How to batch OCR with Aspose OCR GPU in C# using .NET
  type: TechArticle
- questions:
  - answer: Yes, as long as the server has a CUDA‑compatible GPU and the appropriate
      driver libraries installed; no display is required.
    question: Can I run the GPU version on a headless Linux server?
  - answer: Absolutely. The engine treats each page as a separate image and returns
      concatenated text, preserving page order.
    question: Does Aspose OCR support multi‑page TIFF files out of the box?
  - answer: Benchmarks show Aspose OCR achieves ≥ 96 % character accuracy on clean
      printed documents and ≥ 90 % on low‑contrast scans, matching leading SaaS providers
      while keeping data on‑premises.
    question: How accurate is the OCR output compared with cloud services?
  - answer: The library imposes no hard limit; practical limits are driven by available
      disk space and GPU memory. Processing 10 000 pages on an RTX 3080 typically
      stays under 2 GB of GPU memory.
    question: Is there a limit to the number of files I can process in one run?
  - answer: Yes, set `ocrEngine.Language = OcrLanguage.Spanish` (or any supported
      language) before calling `Recognize`. The engine supports 30+ languages, including
      Arabic, Chinese, and Hindi.
    question: Can I customize the language model for non‑English scripts?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
- GPU
title: Πώς να εκτελέσετε ομαδική OCR με το Aspose OCR GPU σε C# χρησιμοποιώντας .NET
url: /el/net/ocr-optimization/how-to-batch-ocr-in-c-with-aspose-ocr-engine/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να κάνετε batch OCR με Aspose OCR GPU σε C# χρησιμοποιώντας .NET

Αν χρειάζεστε **batch OCR** για εκατοντάδες σαρωμένες σελίδες γρήγορα, η μηχανή Aspose OCR GPU σας προσφέρει έναν γρήγορο, αξιόπιστο τρόπο να αναγνωρίζετε κείμενο από εικόνες και αρχεία TIFF σε μία εκτέλεση. Σε αυτόν τον οδηγό θα δείτε πώς να ρυθμίσετε ένα έργο .NET, να ενεργοποιήσετε την επιτάχυνση GPU και να επεξεργαστείτε ολόκληρο φάκελο εικόνων χωρίς να γράψετε ούτε μια γραμμή κώδικα boiler‑plate.

## Γρήγορες απαντήσεις
- **Τι σημαίνει “batch OCR”;** Είναι η αυτοματοποιημένη επεξεργασία πολλών αρχείων εικόνας σε μία λειτουργία, επιστρέφοντας το εξαγόμενο κείμενο για κάθε αρχείο.  
- **Μπορώ να χρησιμοποιήσω την έκδοση GPU σε οποιονδήποτε υπολογιστή;** Ναι, εφόσον το σύστημα διαθέτει GPU συμβατό με CUDA και τον κατάλληλο οδηγό εγκατεστημένο.  
- **Χρειάζομαι άδεια για ανάπτυξη;** Μια δωρεάν δοκιμαστική άδεια λειτουργεί για δοκιμές· απαιτείται εμπορική άδεια για παραγωγή.  
- **Ποιες εκδόσεις .NET υποστηρίζονται;** .NET 6.0 και νεότερες υποστηρίζονται πλήρως· .NET 5 λειτουργεί επίσης με μικρές προσαρμογές.  
- **Είναι η μηχανή thread‑safe για παράλληλες εκτελέσεις;** Η μηχανή CPU είναι thread‑safe· η μηχανή GPU απαιτεί μία παρουσία ανά νήμα ή μια ελεγχόμενη στρατηγική παράλληλης εκτέλεσης.

## Τι είναι το Aspose OCR GPU;
Η μηχανή `Aspose.OCR` GPU είναι μια υψηλών επιδόσεων βιβλιοθήκη OCR που μεταφέρει την ανάλυση εικόνας σε κάρτα γραφικών με ενεργοποιημένο CUDA, προσφέροντας έως και 4× μεγαλύτερη ταχύτητα σε σχέση με την καθαρή επεξεργασία CPU. Υποστηρίζει ευρύ φάσμα μορφών εικόνας, παρέχει ενσωματωμένα μοντέλα γλώσσας και μπορεί να ενσωματωθεί σε οποιαδήποτε εφαρμογή .NET με ελάχιστες αλλαγές κώδικα.

## Γιατί να χρησιμοποιήσετε Aspose OCR GPU για batch επεξεργασία;
Το Aspose OCR υποστηρίζει **30+ μορφές εικόνας** (συμπεριλαμβανομένων PNG, JPEG, BMP και multi‑page TIFF) και μπορεί να διαχειριστεί αρχεία έως **2 GB** το καθένα χωρίς να φορτώνει ολόκληρο το έγγραφο στη μνήμη. Όταν ενεργοποιήσετε την επιτάχυνση GPU, τυπικές σελίδες TIFF 300 dpi επεξεργάζονται σε λιγότερο από 0,2 δευτερόλεπτα ανά σελίδα σε μια σύγχρονη κάρτα RTX 3080.

## Προαπαιτούμενα
- .NET 6.0 SDK (ή νεότερο) εγκατεστημένο στο μηχάνημά σας.  
- Πακέτο NuGet Aspose.OCR για .NET – επιλέξτε το πακέτο `Aspose.OCR.Gpu` αν έχετε συμβατό GPU, διαφορετικά εγκαταστήστε το `Aspose.OCR`.  
- Ένας φάκελος που περιέχει τις εικόνες που θέλετε να επεξεργαστείτε (TIFF, PNG, JPEG κ.λπ.).  
- Visual Studio 2022, Rider ή οποιονδήποτε επεξεργαστή που μπορεί να δημιουργήσει εφαρμογές κονσόλας .NET.

> **Pro tip:** Επαληθεύστε ότι είναι εγκατεστημένο το CUDA 11+ και ότι το `nvidia-smi` αναφέρει το GPU σας ως “compatible”. Η βιβλιοθήκη θα επιστρέψει αυτόματα σε CPU αν δεν βρει κατάλληλο GPU.

## Πώς να ρυθμίσετε το έργο και να εγκαταστήσετε το Aspose OCR
Δημιουργήστε μια νέα εφαρμογή κονσόλας .NET, προσθέστε το πακέτο NuGet Aspose OCR και επαναφέρετε τις εξαρτήσεις. Αυτό προετοιμάζει ένα ελαφρύ έργο που μπορεί να μεταγλωττιστεί και να εκτελεστεί σε οποιαδήποτε πλατφόρμα που υποστηρίζει .NET 6 ή νεότερο. Αφού εγκατασταθεί το πακέτο, μπορείτε να αναφερθείτε στις κλάσεις OCR απευθείας στον κώδικά σας, ενεργοποιώντας batch επεξεργασία χωρίς πρόσθετη διαμόρφωση.

```bash
dotnet new console -n GpuBatchDemo
cd GpuBatchDemo
dotnet add package Aspose.OCR --version 23.12
```

Αν διαθέτετε άδεια με υποστήριξη GPU, εγκαταστήστε το πακέτο ειδικό για GPU. Αυτή η έκδοση περιλαμβάνει εγγενείς δεσμεύσεις CUDA που επιτρέπουν στη μηχανή να τρέχει στην κάρτα γραφικών, παρέχοντας την απόδοση που περιγράφηκε παραπάνω.

```bash
dotnet add package Aspose.OCR.GPU --version 23.12
```

Το έργο σας τώρα αναφέρει τη βιβλιοθήκη OCR που απαιτείται για **batch OCR**.

## Πώς να αρχικοποιήσετε τη μηχανή OCR (CPU ή GPU)
Η κλάση `OcrEngine` είναι το κύριο σημείο εισόδου για εκτέλεση λειτουργιών OCR. Απομονώνει το υποκείμενο υλικό και παρέχει ένα απλό API για εκτέλεση τόσο σε CPU όσο και σε GPU. Φορτώστε τη μηχανή OCR και καθορίστε αν θα χρησιμοποιηθεί το GPU:

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class GpuBatchDemo
{
    static void Main()
    {
        // Create the OCR engine. It works with both CPU and GPU builds.
        var ocrEngine = new OcrEngine();

        // OPTIONAL: Force GPU usage if a compatible device is present.
        // Setting this to true won’t break on CPU‑only machines—it simply tries GPU first.
        ocrEngine.Settings.UseGpu = true;
```

**Γιατί είναι σημαντικό:** Ορίζοντας το `UseGpu` επιτρέπει στο Aspose να επιλέξει τη γρηγορότερη διαδρομή εκτέλεσης. Όταν υπάρχει συμβατό GPU, η μηχανή τρέχει στην κάρτα γραφικών· διαφορετικά επιστρέφει σε CPU χωρίς να πετάξει σφάλμα, διασφαλίζοντας ότι η batch εργασία σας δεν θα καταρρεύσει λόγω έλλειψης υλικού.

## Πώς να συγκεντρώσετε τα αρχεία που θέλετε να επεξεργαστείτε
Η συλλογή των εικόνων-στόχων είναι το πρώτο βήμα σε κάθε batch ροή εργασίας. Δημιουργήστε μια λίστα διαδρομών αρχείων που ταιριάζουν στις υποστηριζόμενες επεκτάσεις, έπειτα περάστε αυτή τη λίστα στον βρόχο OCR. Αυτή η προσέγγιση διατηρεί τον κώδικα απλό και διευκολύνει την προσθήκη φιλτραρίσματος αργότερα.

```csharp
        // Prepare a list of image files (TIFF, PNG, JPEG, etc.).
        var imageFiles = new List<string>
        {
            @"C:\OCR\Input\doc1.tif",
            @"C:\OCR\Input\doc2.tif",
            @"C:\OCR\Input\doc3.tif"
        };

        // You could also populate the list dynamically:
        // var imageFiles = Directory.GetFiles(@"C:\OCR\Input", "*.tif").ToList();
```

**Σημείωση edge‑case:** Αν ο φάκελός σας περιέχει μικτές μορφές, αντικαταστήστε το μοτίβο αναζήτησης με `"*.*"` και φιλτράρετε κατά επέκταση μέσα στον βρόχο. Αυτό κρατά το batch ευέλικτο και αποτρέπει την παράλειψη αρχείων.

## Πώς να επεξεργαστείτε κάθε εικόνα και να εμφανίσετε προεπισκόπηση
Για κάθε αρχείο, καλέστε τη μηχανή OCR, ανακτήστε το αναγνωρισμένο κείμενο και εμφανίστε ένα σύντομο απόσπασμα στην κονσόλα. Η προεπισκόπηση βοηθά να επαληθευτεί ότι το batch λειτουργεί σωστά χωρίς να ανοίγετε κάθε αρχείο εξόδου.

```csharp
        // Loop through each file, run OCR, and print a short preview.
        foreach (var filePath in imageFiles)
        {
            // Load the image into Aspose's OcrImage object.
            var ocrImage = OcrImage.FromFile(filePath);

            // Run recognition.
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // Display the first 50 characters of the recognized text.
            Console.WriteLine($"{filePath}: {ocrResult.Text.Substring(0, Math.Min(50, ocrResult.Text.Length))}...");
        }
    }
}
```

**Τι θα δείτε:** Για κάθε εικόνα η κονσόλα εκτυπώνει τους πρώτους 100 χαρακτήρες του αναγνωρισμένου κειμένου, επιβεβαιώνοντας ότι το batch ολοκληρώθηκε χωρίς να χρειαστεί να ανοίξετε κάθε αρχείο χειροκίνητα.

## Πώς να αποθηκεύσετε τα αποτελέσματα OCR (προαιρετικό αλλά χρήσιμο)
Η διατήρηση της πλήρους εξόδου OCR επιτρέπει επακόλουθη ευρετηρίαση, ανάλυση AI ή μετατροπή σε αναζητήσιμα PDF. Γράψτε το κείμενο σε αρχείο `.txt` που βρίσκεται δίπλα στην πηγαία εικόνα, χρησιμοποιώντας το ίδιο βασικό όνομα για εύκολη αντιστοίχιση.

```csharp
            // Define an output path based on the source file name.
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
```

Τώρα κάθε εικόνα έχει ένα συνοδευτικό αρχείο κειμένου που περιέχει την πλήρη έξοδο OCR, έτοιμο για μηχανές αναζήτησης, μοντέλα γλώσσας ή προσαρμοσμένους αγωγούς ανάλυσης.

## Πώς να εκτελέσετε τη demo και να επαληθεύσετε την έξοδο
Κατασκευάστε και εκτελέστε την εφαρμογή κονσόλας για να δείτε το batch σε δράση. Το βήμα build μεταγλωττίζει τον κώδικα, ενώ το βήμα run επεξεργάζεται κάθε εικόνα στον φάκελο-στόχο και γράφει γραμμές προεπισκόπησης στην κονσόλα. Αν ενεργοποιήσατε το προαιρετικό βήμα αποθήκευσης, θα βρείτε επίσης ένα αρχείο `.txt` για κάθε πηγαία εικόνα.

1. Κατασκευάστε το έργο: `dotnet build`.  
2. Εκτελέστε το πρόγραμμα: `dotnet run --project GpuBatchDemo.csproj`.

Θα πρέπει να δείτε γραμμές προεπισκόπησης στην κονσόλα και, εάν προσθέσατε το προαιρετικό βήμα, μια σειρά από αρχεία `.txt` δίπλα στις πηγαίες εικόνες.

## Συνηθισμένα προβλήματα & πώς να τα διορθώσετε
| Συμπτωμα | Πιθανή αιτία | Διόρθωση |
|----------|--------------|----------|
| **Empty `ocrResult.Text`** | Η εικόνα είναι πολύ σκοτεινή ή χαμηλής DPI | Προεπεξεργασία εικόνων (αύξηση αντίθεσης, upscale) ή ενεργοποίηση `ocrEngine.Settings.PreprocessImage = true`. |
| **GPU error “CUDA driver version is insufficient”** | Παλιός οδηγός | Ενημέρωση του οδηγού GPU, ή ορισμός `UseGpu = false` για εξαναγκαστική επεξεργασία σε CPU. |
| **Exception “File not found”** | Λάθος διαχωριστικό διαδρομής σε Linux/macOS | Χρήση `Path.Combine` ή διαγώνιων καθέτων (`/`). |

## Πώς να κλιμακώσετε πέρα από λίγα αρχεία
Όταν μεταβείτε από δεκάδες σε χιλιάδες εικόνες, σκεφτείτε τις εξής στρατηγικές: χρήση παράλληλης επεξεργασίας με ξεχωριστές παρουσίες μηχανής ανά νήμα, φόρτωση εικόνων σε διαχειρίσιμα batch και καταγραφή προόδου σε αρχείο για εύκολη ανάκτηση. Αυτές οι τεχνικές κρατούν τη χρήση μνήμης χαμηλή και διατηρούν υψηλή απόδοση.

```csharp
Parallel.ForEach(imageFiles, filePath =>
{
    // Same OCR logic as before, but each thread gets its own engine.
    var engine = new OcrEngine { Settings = { UseGpu = true } };
    // ... rest of the code
});
```

> **Remember:** Η μνήμη GPU μοιράζεται μεταξύ της διεργασίας. Η εκκίνηση πάρα πολλών παράλληλων εργασιών GPU μπορεί να κορεστεί τη μνήμη και να επιβραδύνει το batch. Ξεκινήστε με 2‑4 νήματα και παρακολουθήστε τη χρήση GPU.

## Συχνές ερωτήσεις

**Ε: Μπορώ να τρέξω την έκδοση GPU σε έναν headless Linux server;**  
Α: Ναι, εφόσον ο διακομιστής διαθέτει GPU συμβατό με CUDA και τις κατάλληλες βιβλιοθήκες οδηγού εγκατεστημένες· δεν απαιτείται οθόνη.

**Ε: Υποστηρίζει το Aspose OCR αρχεία multi‑page TIFF από προεπιλογή;**  
Α: Απόλυτα. Η μηχανή αντιμετωπίζει κάθε σελίδα ως ξεχωριστή εικόνα και επιστρέφει ενωμένο κείμενο, διατηρώντας τη σειρά των σελίδων.

**Ε: Πόσο ακριβής είναι η έξοδος OCR σε σύγκριση με υπηρεσίες cloud;**  
Α: Τα benchmarks δείχνουν ότι το Aspose OCR επιτυγχάνει ≥ 96 % ακρίβεια χαρακτήρων σε καθαρά τυπωμένα έγγραφα και ≥ 90 % σε σάρωση χαμηλής αντίθεσης, ταιριάζοντας με κορυφαίους παρόχους SaaS ενώ διατηρεί τα δεδομένα on‑premises.

**Ε: Υπάρχει όριο στον αριθμό αρχείων που μπορώ να επεξεργαστώ σε μία εκτέλεση;**  
Α: Η βιβλιοθήκη δεν επιβάλλει σκληρό όριο· τα πρακτικά όρια καθορίζονται από τον διαθέσιμο χώρο στο δίσκο και τη μνήμη GPU. Η επεξεργασία 10 000 σελίδων σε RTX 3080 συνήθως παραμένει κάτω από 2 GB μνήμης GPU.

**Ε: Μπορώ να προσαρμόσω το μοντέλο γλώσσας για μη‑Αγγλικές γραφές;**  
Α: Ναι, ορίστε `ocrEngine.Language = OcrLanguage.Spanish` (ή οποιαδήποτε υποστηριζόμενη γλώσσα) πριν καλέσετε `Recognize`. Η μηχανή υποστηρίζει 30+ γλώσσες, συμπεριλαμβανομένων Arabic, Chinese και Hindi.

## Συμπέρασμα
Τώρα έχετε μια πλήρη, end‑to‑end λύση για **batch OCR με Aspose OCR GPU σε C#**. Ο οδηγός κάλυψε τη ρύθμιση του έργου, την ενεργοποίηση GPU, την απαρίθμηση αρχείων, την επεξεργασία ανά εικόνα, την προαιρετική αποθήκευση αποτελεσμάτων και τεχνικές κλιμάκωσης για τεράστιες εργασίες. Με αυτή τη βάση μπορείτε να τροφοδοτήσετε την έξοδο OCR σε ευρετήρια αναζήτησης, σε μεγάλα μοντέλα γλώσσας ή να δημιουργήσετε προσαρμοσμένους αγωγούς επεξεργασίας εγγράφων.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να συνδυάσετε το κείμενο OCR με το Aspose .PDF για δημιουργία αναζητήσιμων PDF, ή ενσωματώστε την έξοδο με Azure Cognitive Search για άμεση πλήρη αναζήτηση κειμένου σε χιλιάδες σαρωμένα έγγραφα.

---

**Τελευταία ενημέρωση:** 2026-09-13  
**Δοκιμάστηκε με:** Aspose.OCR 24.5 for .NET (CPU & GPU packages)  
**Συγγραφέας:** Aspose  

```
C:\OCR\Input\doc1.tif: The quick brown fox jumps over the laz...
C:\OCR\Input\doc2.tif: Invoice #12345
Date: 2023-11-01
Total: $1,250.00
...
```
```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1 – Create OCR engine (CPU or GPU)
        var ocrEngine = new OcrEngine();
        ocrEngine.Settings.UseGpu = true; // Try GPU, fallback to CPU automatically

        // Step 2 – List of TIFF files to process
        var imageFiles = new List<string>
        {
            @"C:\OCR\Input\doc1.tif",
            @"C:\OCR\Input\doc2.tif",
            @"C:\OCR\Input\doc3.tif"
        };

        // Step 3 – Process each file
        foreach (var filePath in imageFiles)
        {
            var ocrImage = OcrImage.FromFile(filePath);
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // Show a short preview
            Console.WriteLine($"{filePath}: {ocrResult.Text.Substring(0, Math.Min(50, ocrResult.Text.Length))}...");

            // Optional: Save full text to a .txt file
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
        }
    }
}
```

## Σχετικά Tutorials

- [Πώς να χρησιμοποιήσετε OCR σε C για εξαγωγή κειμένου από εικόνες με επιτάχυνση GPU](/ocr/net/ocr-optimization/how-to-use-ocr-in-c-extract-text-from-images-with-gpu-accele/)
- [Αναγνώριση κειμένου από εικόνα με Aspose OCR GPU επιταχυμένη C](/ocr/net/ocr-optimization/recognize-text-from-image-with-aspose-ocr-gpu-accelerated-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}