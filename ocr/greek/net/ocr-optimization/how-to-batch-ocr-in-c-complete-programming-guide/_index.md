---
category: general
date: 2026-05-31
description: Πώς να κάνετε ομαδική OCR σε C# με το Aspose OCR. Μάθετε να μετατρέπετε
  εικόνες σε κείμενο, να εξάγετε κείμενο από εικόνες και να επεξεργάζεστε πολλαπλά
  αρχεία αποδοτικά.
draft: false
keywords:
- how to batch OCR
- convert images to text
- extract text from images
- OCR multiple files
- batch OCR processing
language: el
og_description: Πώς να κάνετε παρτίδα OCR σε C# χρησιμοποιώντας το Aspose OCR. Μετατρέψτε
  εικόνες σε κείμενο, εξάγετε κείμενο από εικόνες και διαχειριστείτε πολλαπλά αρχεία
  OCR με ευκολία.
og_title: Πώς να εκτελέσετε ομαδική OCR σε C# – Πλήρης Οδηγός Προγραμματισμού
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: How to batch OCR in C# with Aspose OCR. Learn to convert images to
    text, extract text from images, and process multiple files efficiently.
  headline: How to Batch OCR in C# – Complete Programming Guide
  type: TechArticle
- description: How to batch OCR in C# with Aspose OCR. Learn to convert images to
    text, extract text from images, and process multiple files efficiently.
  name: How to Batch OCR in C# – Complete Programming Guide
  steps:
  - name: '**.NET 6 SDK** (or later) installed – the latest runtime gives you better
      performance and native support for async I/O.'
    text: '**.NET 6 SDK** (or later) installed – the latest runtime gives you better
      performance and native support for async I/O.'
  - name: '**Visual Studio 2022** (Community Edition works fine) or any editor you
      like.'
    text: '**Visual Studio 2022** (Community Edition works fine) or any editor you
      like.'
  - name: 'The **Aspose.OCR** NuGet package. Install it via the Package Manager Console:'
    text: 'The **Aspose.OCR** NuGet package. Install it via the Package Manager Console:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- batch-processing
title: Πώς να κάνετε ομαδική OCR σε C# – Πλήρης οδηγός προγραμματισμού
url: /el/net/ocr-optimization/how-to-batch-ocr-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εκτελέσετε Batch OCR σε C# – Πλήρης Οδηγός Προγραμματισμού

Έχετε αναρωτηθεί ποτέ **πώς να κάνετε batch OCR** σε ολόκληρο φάκελο σαρωμένων εικόνων χωρίς να ανοίγετε κάθε αρχείο χειροκίνητα; Δεν είστε οι μόνοι. Σε πολλά πραγματικά έργα—σκεφτείτε αυτοματοποίηση τιμολογίων ή αρχειοθέτηση ιστορικών φωτογραφιών—χρειάζεται **να μετατρέψετε εικόνες σε κείμενο** μαζικά, και η επεξεργασία μία‑ προς‑ μία είναι ένας τεράστιος χρόνος.

Σε αυτό το tutorial θα περάσουμε από μια έτοιμη εφαρμογή κονσόλας C# που παίρνει κάθε PNG, JPG ή TIFF σε έναν φάκελο προέλευσης, εκτελεί Aspose OCR σε κάθε μία, και αποθηκεύει ένα αντίστοιχο αρχείο *.txt* σε φάκελο εξόδου. Στο τέλος θα είστε άνετοι με **την εξαγωγή κειμένου από εικόνες**, τη **διαχείριση OCR πολλαπλών αρχείων**, και θα έχετε μια σταθερή βάση για οποιαδήποτε **επεξεργασία batch OCR** χρειαστείτε αργότερα.

## Τι Θα Μάθετε

- Ρύθμιση ενός έργου .NET με το πακέτο NuGet Aspose OCR.  
- Ορισμός φακέλων προέλευσης και προορισμού για μια **batch OCR** εκτέλεση.  
- Καταγραφή των υποστηριζόμενων τύπων εικόνας και παροχή τους στη μηχανή OCR.  
- Εγγραφή του αναγνωρισμένου κειμένου σε ξεχωριστά αρχεία *.txt*, μετατρέποντας **εικόνες σε κείμενο**.  
- Αντιμετώπιση κοινών προβλημάτων όπως ελλιπείς φάκελοι, μη υποστηριζόμενες μορφές και βελτιστοποιήσεις απόδοσης.

Δεν απαιτείται προηγούμενη εμπειρία με το Aspose· μόνο βασική γνώση C# και Visual Studio αρκεί.

---

![Diagram showing the flow of batch OCR processing from image folder to text output – how to batch OCR](/images/batch-ocr-flow.png){alt="διάγραμμα ροής batch OCR"}

## Πώς να κάνετε Batch OCR – Ρύθμιση του Έργου

Πριν βουτήξουμε στον κώδικα, βεβαιωθείτε ότι έχετε:

1. **.NET 6 SDK** (ή νεότερο) εγκατεστημένο – η πιο πρόσφατη έκδοση προσφέρει καλύτερη απόδοση και εγγενή υποστήριξη για async I/O.  
2. **Visual Studio 2022** (η έκδοση Community λειτουργεί άψογα) ή οποιονδήποτε επεξεργαστή προτιμάτε.  
3. Το πακέτο **Aspose.OCR** NuGet. Εγκαταστήστε το μέσω του Package Manager Console:

   ```powershell
   Install-Package Aspose.OCR
   ```

Αυτό είναι όλο. Το υπόλοιπο του tutorial υποθέτει ότι το πακέτο έχει αναφερθεί σωστά.

## Βήμα 2: Προετοιμασία Φακέλων Προέλευσης και Προορισμού (convert images to text)

Πρώτα, χρειαζόμαστε δύο φακέλους: έναν που περιέχει τις ακατέργαστες εικόνες και έναν όπου θα τοποθετηθούν τα παραγόμενα αρχεία *.txt*. Ο κώδικας παρακάτω δημιουργεί τον φάκελο προορισμού αν δεν υπάρχει ήδη—χωρίς χειροκίνητα βήματα.

```csharp
// Define where the images live and where the text files will go
string sourceFolder = @"C:\OCR\Batch";
string outputFolder = @"C:\OCR\BatchTxt";

// Ensure the output directory exists; CreateDirectory is idempotent
Directory.CreateDirectory(outputFolder);
```

> **Γιατί είναι σημαντικό:** Αν παραλείψετε την κλήση `CreateDirectory`, το πρόγραμμα θα ρίξει `DirectoryNotFoundException` τη στιγμή που θα προσπαθήσει να γράψει το πρώτο αρχείο κειμένου. Με το χειρισμό αυτό εκ των προτέρων, κάνετε τη διαδικασία batch OCR πιο αξιόπιστη.

## Βήμα 3: Καταγραφή Αρχείων Εικόνας για OCR Multiple Files

Στη συνέχεια, συγκεντρώνουμε κάθε αρχείο που ταιριάζει στις μορφές που υποστηρίζουμε. Η χρήση LINQ κρατά τον κώδικα σύντομο ενώ παραμένει αναγνώσιμος.

```csharp
// Grab all PNG, JPG, and TIFF files from the source folder (non‑recursive)
var imageFiles = Directory.EnumerateFiles(sourceFolder, "*.*", SearchOption.TopDirectoryOnly)
    .Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase) ||
                f.EndsWith(".jpg", StringComparison.OrdinalIgnoreCase) ||
                f.EndsWith(".tif", StringComparison.OrdinalIgnoreCase));
```

> **Συμβουλή:** Αν αργότερα χρειαστεί να υποστηρίξετε PDF ή BMP, απλώς επεκτείνετε την πρόταση `Where`. Η συγκέντρωση του φίλτρου σε ένα σημείο κάνει τις μελλοντικές τροποποιήσεις άνετες.

## Βήμα 4: Εκτέλεση της Μηχανής OCR σε Κάθε Εικόνα (how to batch OCR)

Τώρα το κύριο μέρος: τροφοδοτώντας κάθε εικόνα στο Aspose OCR και εξάγοντας το αναγνωρισμένο κείμενο. Ο βρόχος παρακάτω δημιουργεί μια νέα παρουσία `OcrEngine` για κάθε αρχείο—αυτό εξασφαλίζει ότι η μνήμη από την προηγούμενη εικόνα απελευθερώνεται πριν ξεκινήσει η επόμενη.

```csharp
foreach (var imagePath in imageFiles)
{
    // Initialize the OCR engine with the current image
    OcrEngine ocrEngine = new OcrEngine
    {
        Image = ImageStream.FromFile(imagePath)
    };

    // Perform recognition; Recognize() returns an OcrResult object
    OcrResult ocrResult = ocrEngine.Recognize();

    // Build the output .txt file path (same base name, .txt extension)
    string textFilePath = Path.Combine(outputFolder,
        Path.GetFileNameWithoutExtension(imagePath) + ".txt");

    // Persist the extracted text
    File.WriteAllText(textFilePath, ocrResult.Text);

    Console.WriteLine($"Processed {Path.GetFileName(imagePath)} → {Path.GetFileName(textFilePath)}");
}
```

**Τι συμβαίνει;**  

- `ImageStream.FromFile` φορτώνει την εικόνα σε ροή που μπορεί να διαβάσει το Aspose.  
- `ocrEngine.Recognize()` εκτελεί τον αλγόριθμο OCR, επιστρέφοντας μια συμβολοσειρά στο `ocrResult.Text`.  
- `File.WriteAllText` γράφει αυτή τη συμβολοσειρά στο δίσκο, ουσιαστικά **εξάγοντας κείμενο από εικόνες**.

### Διαχείριση Περιπτώσεων Άκρων

- **Κατεστραμμένες εικόνες** – τυλίξτε την κλήση αναγνώρισης σε `try/catch` και καταγράψτε την αποτυχία, συνεχίζοντας με το επόμενο αρχείο.  
- **Μεγάλες παρτίδες** – σκεφτείτε την ασύγχρονη επεξεργασία με `Parallel.ForEach` αν διαθέτετε πολυπύρημο σύστημα.  
- **Διάφορες γλώσσες** – ορίστε `ocrEngine.Language = Language.English;` ή οποιαδήποτε άλλη υποστηριζόμενη γλώσσα πριν καλέσετε `Recognize()`.

## Βήμα 5: Αποθήκευση Εξαγόμενου Κειμένου (extract text from images)

Το προηγούμενο απόσπασμα ήδη αποθηκεύει το αποτέλεσμα OCR, αλλά ας απομονώσουμε αυτή τη λογική σε μια βοηθητική μέθοδο. Αυτό καθαρίζει τον κύριο βρόχο και ενθαρρύνει την επαναχρησιμοποίηση.

```csharp
static void SaveOcrResult(string outputFolder, string imagePath, string recognizedText)
{
    string textFilePath = Path.Combine(outputFolder,
        Path.GetFileNameWithoutExtension(imagePath) + ".txt");

    File.WriteAllText(textFilePath, recognizedText);
}
```

Στη συνέχεια αντικαθιστάτε την ενσωματωμένη κλήση `File.WriteAllText` με:

```csharp
SaveOcrResult(outputFolder, imagePath, ocrResult.Text);
```

> **Γιατί να το εξάγετε σε μέθοδο;** Διαχωρίζει τις ανησυχίες—αναγνώριση vs. αποθήκευση—και σας δίνει ένα ενιαίο σημείο για προσθήκη επεξεργασίας μετά (π.χ. αφαίρεση κενών ή προσθήκη χρονικών σημάνσεων).

## Πλήρες Παράδειγμα – Επεξεργασία Batch OCR σε C#

Συνδυάζοντας όλα τα κομμάτια, εδώ είναι ένα αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα νέο έργο Console App και να τρέξετε αμέσως.

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Linq;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Define source & destination folders
            string sourceFolder = @"C:\OCR\Batch";
            string outputFolder = @"C:\OCR\BatchTxt";

            // 2️⃣ Make sure the output folder exists
            Directory.CreateDirectory(outputFolder);

            // 3️⃣ Get all supported image files (convert images to text)
            var imageFiles = Directory.EnumerateFiles(sourceFolder, "*.*", SearchOption.TopDirectoryOnly)
                .Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase) ||
                            f.EndsWith(".jpg", StringComparison.OrdinalIgnoreCase) ||
                            f.EndsWith(".tif", StringComparison.OrdinalIgnoreCase));

            // 4️⃣ Process each image (how to batch OCR)
            foreach (var imagePath in imageFiles)
            {
                try
                {
                    // Initialise OCR engine for the current file
                    OcrEngine ocrEngine = new OcrEngine
                    {
                        Image = ImageStream.FromFile(imagePath)
                    };

                    // Run OCR – this extracts text from images
                    OcrResult result = ocrEngine.Recognize();

                    // 5️⃣ Save the result (extract text from images)
                    SaveOcrResult(outputFolder, imagePath, result.Text);

                    Console.WriteLine($"✅ {Path.GetFileName(imagePath)} processed.");
                }
                catch (Exception ex)
                {
                    // Gracefully handle problematic files
                    Console.WriteLine($"⚠️ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
                }
            }

            Console.WriteLine("🎉 Batch OCR processing complete!");
        }

        // Helper to write the OCR output to a .txt file
        static void SaveOcrResult(string outputFolder, string imagePath, string recognizedText)
        {
            string textFilePath = Path.Combine(outputFolder,
                Path.GetFileNameWithoutExtension(imagePath) + ".txt");

            File.WriteAllText(textFilePath, recognizedText);
        }
    }
}
```

### Αναμενόμενη Εξαγωγή

Όταν τρέξετε το πρόγραμμα, η κονσόλα θα εμφανίσει γραμμές παρόμοιες με:

```
✅ invoice001.png processed.
✅ receipt123.jpg processed.
✅ map.tif processed.
🎉 Batch OCR processing complete!
```

Την ίδια στιγμή, ο φάκελος `C:\OCR\BatchTxt` θα περιέχει:

- `invoice001.txt`
- `receipt123.txt`
- `map.txt`

Κάθε αρχείο περιέχει την απλή κειμενική αναπαράσταση της πηγαίας εικόνας, έτοιμο για ευρετηρίαση, αναζήτηση ή επόμενη ανάλυση.

## Pro Tips & Common Pitfalls (batch OCR processing)

- **Διαχείριση μνήμης:** Το Aspose OCR απελευθερώνει τις εικόνες μετά από κάθε κλήση `Recognize()`, αλλά αν επεξεργάζεστε χιλιάδες αρχεία, σκεφτείτε να καλέσετε `GC.Collect()` περιοδικά για να κρατήσετε το αποτύπωμα μνήμης χαμηλό.  
- **Επιτάχυνση:** Χρησιμοποιήστε `OcrEngine.RecognizeAsync()` σε .NET 6+ και εκκινήστε πολλαπλές εργασίες με `Task

## Τι Θα Μάθετε Στη Σύντομη Μελλοντική Σας

- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Perform OCR on Archive Images with Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}