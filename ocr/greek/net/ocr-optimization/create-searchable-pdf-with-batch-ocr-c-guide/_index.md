---
category: general
date: 2025-12-29
description: Δημιουργήστε αναζητήσιμο PDF από σαρωμένες εικόνες χρησιμοποιώντας την
  επεξεργασία παρτίδας Aspose OCR. Μάθετε πώς να μετατρέπετε εικόνες σε PDF, να προεπεξεργάζεστε
  εικόνες για OCR και να διορθώνετε την κλίση των σαρωμένων εγγράφων.
draft: false
keywords:
- create searchable pdf
- batch ocr processing
- convert images to pdf
- preprocess images for ocr
- deskew scanned documents
language: el
og_description: Δημιουργήστε αναζητήσιμο PDF από σαρωμένες εικόνες χρησιμοποιώντας
  την επεξεργασία παρτίδας Aspose OCR. Μάθετε πώς να μετατρέπετε εικόνες σε PDF, να
  προεπεξεργάζεστε εικόνες για OCR και να διορθώνετε την κλίση των σαρωμένων εγγράφων.
og_title: Δημιουργία αναζητήσιμου PDF με ομαδικό OCR – Οδηγός C#
tags:
- OCR
- C#
- PDF/A
- Aspose
title: Δημιουργία αναζητήσιμου PDF με μαζική OCR – Οδηγός C#
url: /el/net/ocr-optimization/create-searchable-pdf-with-batch-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία αναζητήσιμου pdf με batch OCR – Οδηγός C#

Έχετε ποτέ χρειαστεί να **δημιουργήσετε αναζητήσιμο pdf** αρχεία από ένα βουνό σαρωμένων εικόνων αλλά να έχετε κολλήσει στο πρώτο βήμα; Δεν είστε μόνοι—οι περισσότεροι προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν ασχολούνται με ακατάστατες σαρώσεις, άνισες σελίδες ή απλώς μαζική μετατροπή.  

Τα καλά νέα; Με το Aspose OCR μπορείτε να δημιουργήσετε μια **batch OCR processing** γραμμή εργασίας που όχι μόνο **μετατρέπει εικόνες σε pdf**, αλλά επίσης **προεπεξεργάζεται εικόνες για OCR** και ακόμη **ευθυγραμμίζει σαρωμένα έγγραφα** αυτόματα. Σε αυτόν τον οδηγό θα περάσουμε από όλα τα βήματα, από τη ρύθμιση της μηχανής μέχρι την τελειοποίηση του αποτελέσματος, ώστε να μπορείτε να το τρέξετε σε έναν φάκελο αρχείων και να αποκτήσετε αναζητήσιμα PDF/A‑2b διαμάντια.

> **Τι θα πάρετε:** μια ενιαία, εκτελέσιμη εφαρμογή κονσόλας C# που παίρνει έναν κατάλογο εικόνων (ή PDF), καθαρίζει κάθε σελίδα, εκτελεί OCR και αποθηκεύει ένα αναζητήσιμο αρχείο PDF/A‑2b δίπλα στην πηγή. Χωρίς αποσπασματικά αποσπάσματα, μόνο μια συνεκτική λύση.

---

## Προαπαιτούμενα

- .NET 6 SDK ή νεότερο (ο κώδικας μεταγλωττίζεται επίσης με .NET Core).  
- Ένα πακέτο NuGet Aspose OCR (`Aspose.OCR`).  
- Ένας φάκελος με σαρωμένες εικόνες (TIFF, JPEG, PNG) ή PDF που θέλετε να μετατρέψετε σε αναζητήσιμα PDF.  
- (Προαιρετικό) Ένα πραγματικό κλειδί άδειας—διαφορετικά η δοκιμαστική λειτουργία θα προσθέσει υδατογράφημα, αλλά λειτουργεί για δοκιμές.

Αν έχετε όλα αυτά, ας βουτήξουμε.

## Επισκόπηση – Πώς η πλήρης γραμμή εργασίας δημιουργεί ένα αναζητήσιμο pdf

1. **Ενεργοποίηση δοκιμαστικής λειτουργίας** (ή φόρτωση της άδειας).  
2. **Διαμόρφωση `OcrBatchProcessor`** – υποδείξτε του πού να διαβάζει αρχεία, πού να γράφει PDF, ποια μορφή να χρησιμοποιεί και πόσα νήματα να εκτελεί παράλληλα.  
3. **Προ‑επεξεργασία κάθε εικόνας** – ευθυγράμμιση, αφαίρεση θορύβου και αφαίρεση φόντου ώστε η μηχανή OCR να βλέπει μια καθαρή σελίδα.  
4. **Εκτέλεση της παρτίδας** – το Aspose επεξεργάζεται κάθε αρχείο, εκτελεί OCR και γράφει ένα αναζητήσιμο PDF/A‑2b.  
5. **Ειδοποίηση ολοκλήρωσης** – ένα απλό μήνυμα κονσόλας, αλλά μπορείτε να συνδέσετε έναν καταγραφέα ή webhook.

Αυτή είναι η υψηλού επιπέδου ροή. Ο κώδικας παρακάτω υλοποιεί κάθε βήμα με πολλές σχολιαστικές σημειώσεις, ώστε να μπορείτε να τροποποιήσετε οποιοδήποτε μέρος χωρίς να σπάσετε ολόκληρη τη διαδικασία.

## Βήμα 1 – Ενεργοποίηση δοκιμαστικής λειτουργίας (ή φόρτωση της άδειας)

Πριν καλέσετε οποιαδήποτε κλάση του Aspose, πρέπει να ενημερώσετε τη βιβλιοθήκη ότι έχετε άδεια. Για γρήγορα πειράματα η δοκιμαστική λειτουργία είναι αρκετή.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using Aspose.OCR.Batch;

// Activate trial mode – replace with OcrEngine.SetLicense("YourLicenseFile.lic") for production
OcrEngine.EnableTrialMode();
```

**Συμβουλή επαγγελματία:** διατηρήστε την ενεργοποίηση της άδειας στην κορυφή του `Program.cs`. Αν το ξεχάσετε, η μηχανή θα πετάξει εξαίρεση την πρώτη φορά που καλέσετε το `Process()`.

## Βήμα 2 – Διαμόρφωση της μηχανής επεξεργασίας batch OCR

Εδώ ρυθμίζουμε το αντικείμενο **batch OCR processing**. Παρατηρήστε ότι το `InputFolder` και το `OutputFolder` είναι τα ίδια σε αυτό το παράδειγμα, αλλά μπορείτε να τα χωρίσετε αν προτιμάτε.

```csharp
// Define where your source images live and where the searchable PDFs should be saved
var ocrBatch = new OcrBatchProcessor
{
    // Folder that contains the images or PDFs to be processed
    InputFolder = @"C:\Scans\Incoming",

    // Folder where searchable PDF/A‑2b files will be saved
    OutputFolder = @"C:\Scans\Processed",

    // Choose the output format – searchable PDF/A‑2b (perfect for archiving)
    OutputFormat = SaveFormat.SearchablePdf,

    // Limit the number of concurrent OCR operations to avoid CPU spikes
    MaxDegreeOfParallelism = 3,

    // Pre‑process each image: deskew, denoise, and remove background
    Preprocess = img => ImageFilters
                            .Deskew(img)          // fixes rotated pages
                            .Denoise()            // reduces speckles
                            .RemoveBackground()   // clears colored backgrounds
};
```

### Γιατί αυτές οι ρυθμίσεις έχουν σημασία

- **`MaxDegreeOfParallelism`**: Η εκτέλεση πάρα πολλών νημάτων OCR μπορεί να κορεσθεί η CPU, ειδικά σε ένα μέτριο σταθμό εργασίας. Τρία νήματα είναι το ιδανικό για τα περισσότερα φορητά quad‑core.  
- **`Preprocess` pipeline**: Τα τρία φίλτρα μαζί βελτιώνουν δραματικά την ακρίβεια του OCR. Η ευθυγράμμιση διορθώνει το κοινό πρόβλημα “κλινής σάρωσης”, η αφαίρεση θορύβου αφαιρεί τυχαίο θόρυβο, και η αφαίρεση φόντου εξασφαλίζει ότι η μηχανή βλέπει μόνο κείμενο μαύρο‑σε‑λευκό.  
- **`SaveFormat.SearchablePdf`**: Αυτό δημιουργεί αρχεία PDF/A‑2b που είναι τόσο έτοιμα για αρχειοθέτηση όσο και αναζητήσιμα—απαιτούμενο για πολλά πρότυπα συμμόρφωσης.

## Βήμα 3 – Εκτέλεση της παρτίδας και παρακολούθηση της μαγείας

Η εκτέλεση της παρτίδας είναι τόσο απλή όσο η κλήση του `Process()`. Η μέθοδος μπλοκάρει μέχρι να ολοκληρωθεί κάθε αρχείο, μετά επιστρέφει. Αν χρειάζεστε αναφορά προόδου, μπορείτε να συνδέσετε το συμβάν `ProgressChanged` (δεν εμφανίζεται εδώ).

```csharp
// Start processing – this will walk through every file in InputFolder
ocrBatch.Process();

// Let the user (or calling script) know we’re finished
Console.WriteLine("All files processed. Searchable PDFs are ready.");
```

Όταν η κονσόλα εκτυπώσει την τελική γραμμή, θα βρείτε ένα αναζητήσιμο PDF για κάθε εικόνα εισόδου στο `C:\Scans\Processed`. Ανοίξτε οποιοδήποτε από αυτά στο Adobe Reader, πατήστε **Ctrl+F**, και μπορείτε να αναζητήσετε το κείμενο που μόλις εξήχθη από τη σάρωση.

## Βήμα 4 – Πλήρες εκτελέσιμο πρόγραμμα (έτοιμο για αντιγραφή‑επικόλληση)

Παρακάτω βρίσκεται το **πλήρες, αυτόνομο** πρόγραμμα που μπορείτε να προσθέσετε σε ένα νέο έργο κονσόλας (`dotnet new console`). Βεβαιωθείτε ότι έχετε προσθέσει πρώτα το πακέτο NuGet Aspose.OCR (`dotnet add package Aspose.OCR`).

```csharp
// Program.cs
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using Aspose.OCR.Batch;

namespace CreateSearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Activate trial mode (replace with real license for production)
            OcrEngine.EnableTrialMode();

            // 2️⃣ Configure batch OCR processing
            var ocrBatch = new OcrBatchProcessor
            {
                InputFolder = @"C:\Scans\Incoming",   // 👉 change to your source folder
                OutputFolder = @"C:\Scans\Processed", // 👉 change to your target folder
                OutputFormat = SaveFormat.SearchablePdf,
                MaxDegreeOfParallelism = 3,
                Preprocess = img => ImageFilters
                                        .Deskew(img)          // fixes rotated pages
                                        .Denoise()            // cleans up noise
                                        .RemoveBackground()   // strips colored backgrounds
            };

            // 3️⃣ Run the batch
            ocrBatch.Process();

            // 4️⃣ Notify completion
            Console.WriteLine("All files processed. Searchable PDFs are ready.");
        }
    }
}
```

### Αναμενόμενη έξοδος

```
All files processed. Searchable PDFs are ready.
```

Μετά την εκτέλεση, πλοηγώντας στο `C:\Scans\Processed` θα εμφανιστεί ένα σύνολο αρχείων `.pdf`—κάθε ένα αναζητήσιμο, κάθε ένα σύμφωνο με PDF/A‑2b. Ανοίξτε οποιοδήποτε αρχείο, πληκτρολογήστε μια λέξη που γνωρίζετε ότι εμφανίζεται στην αρχική σάρωση, και voilà, το κείμενο θα επισημανθεί.

## Συχνές ερωτήσεις & διαχείριση ειδικών περιπτώσεων

### Τι γίνεται αν ο φάκελος προέλευσης περιέχει ήδη PDF;

Το Aspose OCR μπορεί να επεξεργαστεί PDF απευθείας· θα ραστεροποιήσει κάθε σελίδα, θα εφαρμόσει τα ίδια φίλτρα **preprocess**, και θα ενσωματώσει το στρώμα OCR. Δεν απαιτείται επιπλέον κώδικας.

### Πώς αλλάζω τη μορφή εξόδου σε απλό PDF (μη αναζητήσιμο);

Αντικαταστήστε το `SaveFormat.SearchablePdf` με `SaveFormat.Pdf`. Θα χάσετε το στρώμα αναζητήσιμου κειμένου, αλλά η οπτική πιστότητα παραμένει η ίδια.

### Οι σαρώσεις μου είναι έγχρωμες—επηρεάζει η αφαίρεση φόντου αυτό;

`RemoveBackground()` στοχεύει σε μη‑λευκά φόντα διατηρώντας το κύριο κείμενο. Αν χρειάζεται να διατηρήσετε χρωματικά γραφικά, μπορείτε να παραλείψετε αυτό το φίλτρο:

```csharp
.Preprocess = img => ImageFilters.Deskew(img).Denoise()
```

### Εκτελώ σε διακομιστή με περιορισμένη μνήμη RAM—μπορώ να μειώσω τον αριθμό των νημάτων;

Απόλυτα. Ορίστε το `MaxDegreeOfParallelism` σε `1` ή `2`. Η παρτίδα θα διαρκέσει περισσότερο, αλλά η χρήση μνήμης θα παραμείνει χαμηλή.

## Οπτική σύνοψη (προαιρετικό)

Αν σας αρέσει ένα γρήγορο διάγραμμα, φανταστείτε αυτή τη ροή:

![Δημιουργία αναζητήσιμου pdf ροής εργασίας – δείχνει φάκελο εισόδου → προεπεξεργασία → OCR → έξοδο αναζητήσιμου PDF](/images/ocr-workflow.png)

*Κείμενο alt εικόνας:* **Διάγραμμα ροής δημιουργίας αναζητήσιμου pdf** – απεικονίζει την επεξεργασία batch OCR, τη μετατροπή και τα βήματα ευθυγράμμισης.

## Συμπέρασμα

Τώρα έχετε μια **πλήρη, έτοιμη για παραγωγή** λύση για **δημιουργία αναζητήσιμων pdf** αρχείων από οποιαδήποτε παρτίδα σαρωμένων εικόνων. Εκμεταλλευόμενοι την **batch OCR processing**, μπορείτε να **μετατρέψετε εικόνες σε pdf**, να **προεπεξεργαστείτε εικόνες για OCR**, και αυτόματα να **ευθυγραμμίσετε σαρωμένα έγγραφα**—όλα με μερικές μόνο γραμμές C#.

Επόμενα βήματα; Δοκιμάστε να προσθέσετε ένα προσαρμοσμένο σχήμα ονομασίας, να συνδέσετε ένα πλαίσιο καταγραφής για τη λήψη βαθμών εμπιστοσύνης OCR, ή να πειραματιστείτε με άλλα `ImageFilters` όπως το `Sharpen()` για αχνό κείμενο. Το API του Aspose OCR είναι αρκετά ευέλικτο ώστε να εξελίσσεται με τις ανάγκες σας.

Καλή προγραμματιστική δουλειά, και εύχομαι τα PDF σας να είναι πάντα αναζητήσιμα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}