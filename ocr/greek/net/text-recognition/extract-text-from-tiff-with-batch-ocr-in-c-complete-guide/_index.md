---
category: general
date: 2026-04-11
description: Εξάγετε κείμενο από αρχεία TIFF χρησιμοποιώντας την επεξεργασία παρτίδας
  OCR της Aspose σε C#. Μάθετε πώς να επεξεργάζεστε παρτίδες OCR αποδοτικά και να
  λαμβάνετε ανατροφοδότηση προόδου σε πραγματικό χρόνο.
draft: false
keywords:
- extract text from tiff
- process batch ocr
- OCR batch processing
- Aspose OCR C#
- TIFF image OCR
language: el
og_description: Εξάγετε κείμενο από αρχεία TIFF χρησιμοποιώντας την επεξεργασία παρτίδας
  OCR της Aspose σε C#. Αυτό το σεμινάριο δείχνει βήμα‑προς‑βήμα πώς να επεξεργαστείτε
  παρτίδα OCR και να διαβάσετε την πρόοδο.
og_title: Εξαγωγή κειμένου από TIFF με Batch OCR σε C# – Πλήρης οδηγός
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Εξαγωγή κειμένου από TIFF με Batch OCR σε C# – Πλήρης οδηγός
url: /el/net/text-recognition/extract-text-from-tiff-with-batch-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή κειμένου από TIFF – Ολοκληρωμένος οδηγός Batch OCR

Έχετε χρειαστεί ποτέ να **εξάγετε κείμενο από αρχεία TIFF** αλλά να κολλήσετε στο κομμάτι της επεξεργασίας σε batch; Δεν είστε οι μόνοι. Σε πολλά έργα αυτοματοποίησης εγγράφων, η διαχείριση δεκάδων εικόνων TIF υψηλής ανάλυσης μπορεί γρήγορα να γίνει bottleneck—ιδιαίτερα όταν θέλετε άμεση ανατροφοδότηση για την πρόοδο.  

Τα καλά νέα; Με το Aspose OCR μπορείτε να **επεξεργαστείτε batch OCR** με λίγες μόνο γραμμές, να λαμβάνετε γεγονότα προόδου σε πραγματικό χρόνο και να εξάγετε το αναγνωρισμένο κείμενο για κάθε εικόνα. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από μια έτοιμη εφαρμογή κονσόλας C# που κάνει ακριβώς αυτό.

Θα καλύψουμε τα πάντα που χρειάζεστε: τα απαιτούμενα πακέτα, γιατί κάθε γραμμή έχει σημασία, edge‑cases όπως ελλιπή αρχεία, και πώς να επαληθεύσετε τα αποτελέσματα. Στο τέλος θα μπορείτε να ενσωματώσετε το δείγμα στη δική σας λύση και να αρχίσετε να εξάγετε κείμενο από εικόνες TIFF αμέσως.

## Τι θα χρειαστείτε

- **.NET 6 ή νεότερο** (ο κώδικας μεταγλωττίζεται και με .NET Core)  
- **Aspose.OCR for .NET** πακέτο NuGet – `Install-Package Aspose.OCR`  
- Ένας φάκελος που περιέχει μερικές **TIFF** εικόνες που θέλετε να διαβάσετε (το demo χρησιμοποιεί `img1.tif`, `img2.tif`, `img3.tif`)  
- Οποιοδήποτε IDE προτιμάτε – Visual Studio, Rider ή VS Code αρκούν  

Δεν απαιτείται επιπλέον διαμόρφωση· η βιβλιοθήκη έρχεται με τη δική της μηχανή OCR, οπότε δεν χρειάζεται να εγκαταστήσετε εξωτερικά native binaries.

---

## Βήμα 1 – Δημιουργία του αντικειμένου OCR Engine  

Το πρώτο που κάνετε είναι να δημιουργήσετε ένα `OcrEngine`. Σκεφτείτε το ως τον εγκέφαλο που θα αναλύσει κάθε pixel και θα το μετατρέψει σε χαρακτήρες.

```csharp
using Aspose.OCR;

// Step 1: Initialise the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

> **Γιατί είναι σημαντικό:**  
> Η μηχανή κρατά εσωτερικά μοντέλα γλώσσας και ρυθμίσεις (π.χ., DPI, γλώσσα). Η δημιουργία της μία φορά και η επαναχρησιμοποίησή της για ένα batch είναι πολύ πιο αποδοτική από το να δημιουργείτε νέα μηχανή για κάθε εικόνα.

---

## Βήμα 2 – Σύνδεση των γεγονότων προόδου σε πραγματικό χρόνο  

Αν επεξεργάζεστε δεκάδες αρχεία TIFF, ένας δείκτης προόδου μπορεί να σας σώσει από το άγχος του «κολλήθηκε η εφαρμογή».

```csharp
using Aspose.OCR.Events;

// Step 2: Subscribe to progress updates
ocrEngine.ProgressChanged += Ocr_ProgressChanged;

// Event handler definition (placed later in the file)
```

Το γεγονός `ProgressChanged` ενεργοποιείται μετά το τέλος κάθε εικόνας, παρέχοντάς σας `Current`, `Total` και `Percentage`. Αυτός είναι ο βρόχος ανατροφοδότησης **process batch OCR** που οι περισσότεροι προγραμματιστές ξεχνούν να υλοποιήσουν.

---

## Βήμα 3 – Δημιουργία λίστας ροών εικόνας  

Το Aspose.OCR δουλεύει με αντικείμενα `ImageStream`. Ο πιο εύκολος τρόπος είναι να φορτώσετε κάθε TIFF από το δίσκο.

```csharp
using Aspose.OCR;
using System.Collections.Generic;

// Step 3: Prepare the batch of TIFF images
List<ImageStream> imageFiles = new List<ImageStream>
{
    ImageStream.FromFile(@"YOUR_DIRECTORY/img1.tif"),
    ImageStream.FromFile(@"YOUR_DIRECTORY/img2.tif"),
    ImageStream.FromFile(@"YOUR_DIRECTORY/img3.tif")
};
```

> **Συμβουλή:**  
> Αν έχετε έναν δυναμικό φάκελο, αντικαταστήστε τη σκληρά κωδικοποιημένη λίστα με `Directory.GetFiles(path, "*.tif")` και `Select(ImageStream.FromFile)` – έτσι θα **process batch OCR** χωρίς χειροκίνητες ενημερώσεις.

---

## Βήμα 4 – Εκτέλεση της διαδικασίας Batch OCR  

Τώρα γίνεται η βαριά δουλειά. Η `ProcessBatch` επιστρέφει μια read‑only λίστα αντικειμένων `OcrResult`, το καθένα με το εξαγόμενο κείμενο και τα confidence scores.

```csharp
// Step 4: Execute batch OCR and collect results
IReadOnlyList<OcrResult> ocrResults = ocrEngine.ProcessBatch(imageFiles);
```

> **Γιατί είναι αποδοτικό:**  
> Η μηχανή επαναχρησιμοποιεί το ίδιο μοντέλο γλώσσας για όλες τις εικόνες, μειώνοντας δραστικά την κατανάλωση μνήμης σε σύγκριση με κλήσεις μονής εικόνας.

---

## Βήμα 5 – Εμφάνιση ή αποθήκευση του αναγνωρισμένου κειμένου  

Τέλος, επαναλάβετε τα αποτελέσματα. Σε ένα πραγματικό έργο ίσως τα γράψετε σε βάση δεδομένων ή σε αρχείο JSON, αλλά για αυτό το demo θα τα τυπώσουμε στην κονσόλα.

```csharp
// Step 5: Output the recognised text for each TIFF
foreach (var result in ocrResults)
{
    Console.WriteLine("=== OCR Result ===");
    Console.WriteLine(result.Text);
    Console.WriteLine();
}
```

**Αναμενόμενη έξοδος κονσόλας** (συντομευμένη για ευκρίνεια):

```
=== OCR Result ===
Invoice #12345
Date: 03/15/2026
Total: $1,250.00

=== OCR Result ===
Meeting Minutes
1. Project kickoff...
```

Αν κάποια εικόνα αποτύχει, το `result.Text` θα είναι κενό string, και το γεγονός `ProgressChanged` θα αναφέρει το στοιχείο ως επεξεργασμένο—έτσι μπορείτε να καταγράψετε τις αποτυχίες ξεχωριστά.

---

## Ο Διαχειριστής του Γεγονότος Προόδου (Πλήρης Κώδικας)

Τοποθετήστε αυτή τη μέθοδο οπουδήποτε μέσα στην κλάση `BatchDemo`—κατά προτίμηση μετά το `Main`.

```csharp
private static void Ocr_ProgressChanged(object sender, ProgressChangedEventArgs e)
{
    // Gives you a live view of how many files have been processed
    Console.WriteLine($"Processed {e.Current}/{e.Total} – {e.Percentage}%");
}
```

> **Pro tip:**  
> Ανακατευθύνετε αυτή την έξοδο σε μια progress bar UI αν χτίζετε desktop εφαρμογή· το ίδιο γεγονός λειτουργεί για WinForms, WPF ή ακόμη και για ASP.NET Core SignalR notifications.

---

## Πλήρες, Έτοιμο‑για‑Εκτέλεση Δείγμα  

Συνδυάζοντας τα παραπάνω, εδώ είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε νέο project κονσόλας.

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Events;

class BatchDemo
{
    static void Main()
    {
        // 1️⃣ Initialise OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Subscribe to progress events
        ocrEngine.ProgressChanged += Ocr_ProgressChanged;

        // 3️⃣ Load TIFF images into a list
        List<ImageStream> imageFiles = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/img1.tif"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/img2.tif"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/img3.tif")
        };

        // 4️⃣ Run batch OCR
        IReadOnlyList<OcrResult> ocrResults = ocrEngine.ProcessBatch(imageFiles);

        // 5️⃣ Print results
        foreach (var result in ocrResults)
        {
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(result.Text);
            Console.WriteLine();
        }
    }

    // Progress event handler
    private static void Ocr_ProgressChanged(object sender, ProgressChangedEventArgs e)
    {
        Console.WriteLine($"Processed {e.Current}/{e.Total} – {e.Percentage}%");
    }
}
```

Αποθηκεύστε το αρχείο ως `Program.cs`, τρέξτε `dotnet add package Aspose.OCR`, αντικαταστήστε το `YOUR_DIRECTORY` με την πραγματική διαδρομή, και πατήστε **Ctrl+F5**. Θα πρέπει να δείτε αριθμούς προόδου ακολουθούμενους από το εξαγόμενο κείμενο για κάθε TIFF.

---

## Διαχείριση Συνηθισμένων Edge Cases  

| Κατάσταση | Τι να προσέξετε | Γρήγορη Διόρθωση |
|-----------|-------------------|-----------|
| **Απουσία ή κατεστραμμένο TIFF** | `ImageStream.FromFile` ρίχνει `FileNotFoundException` ή `ArgumentException`. | Τυλίξτε τη δημιουργία λίστας σε `try/catch` και παραλείψτε τα μη έγκυρα αρχεία, καταγράφοντας το πρόβλημα. |
| **Πολύ μεγάλες εικόνες ( >10 MP )** | Το OCR μπορεί να καταναλώσει πολύ RAM και να επιβραδύνει. | Μειώστε το DPI πριν την επεξεργασία: `ocrEngine.ImagePreprocessing.Dpi = 300;` |
| **Μη‑Αγγλικό κείμενο** | Το προεπιλεγμένο μοντέλο γλώσσας είναι Αγγλικά. | Ορίστε `ocrEngine.Language = Language.Spanish;` (ή οποιαδήποτε υποστηριζόμενη γλώσσα). |
| **Ανάγκη αποθήκευσης αποτελεσμάτων** | Η έξοδος στην κονσόλα δεν είναι μόνιμη. | Γράψτε `result.Text` σε αρχείο `.txt` με `File.WriteAllText`. |

Η αντιμετώπιση αυτών των σεναρίων κάνει τη λύση σας ανθεκτική και δείχνει ότι έχετε σκεφτεί πέρα από το «happy path».

---

## Επόμενα Βήματα & Σχετικά Θέματα  

- **Εξαγωγή κειμένου από PDF** – παρόμοιο API, απλώς αντικαταστήστε το `ImageStream` με `PdfDocument`.  
- **Parallel batch OCR** – για τεράστιες εργασίες, δημιουργήστε πολλαπλά `OcrEngine` σε ξεχωριστά νήματα· θυμηθείτε να σεβαστείτε τα όρια της άδειας χρήσης.  
- **Post‑processing** – τρέξτε το OCR output από spell‑checker ή regex για να καθαρίσετε κοινά OCR artefacts.  

Όλες αυτές οι επεκτάσεις βασίζονται στην κεντρική ιδέα του **process batch OCR** και μπορούν να προστεθούν σταδιακά.

---

## Συμπέρασμα  

Δείξαμε πώς να **εξάγετε κείμενο από αρχεία TIFF** αποδοτικά με **process batch OCR** χρησιμοποιώντας το Aspose OCR σε C#. Το δείγμα δημιουργεί μία μηχανή, εγγράφεται σε γεγονότα προόδου, φορτώνει μια λίστα ροών εικόνας, εκτελεί το batch και τυπώνει κάθε αποτέλεσμα.  

Από εδώ μπορείτε να ενσωματώσετε το αποτέλεσμα σε βάσεις δεδομένων, να δημιουργήσετε searchable PDFs, ή να τροφοδοτήσετε το κείμενο σε downstream NLP pipelines. Ο ουρανός είναι το όριο—πειραματιστείτε με ρυθμίσεις γλώσσας, DPI, και παράλληλη εκτέλεση ώστε να ταιριάζει στο workload σας.

Έχετε ερωτήσεις ή θέλετε να μοιραστείτε πώς προσαρμόσατε το batch; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}