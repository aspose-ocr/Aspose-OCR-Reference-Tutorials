---
category: general
date: 2026-06-16
description: Η επεξεργασία OCR σε παρτίδες σε C# σας επιτρέπει να μετατρέπετε εικόνες
  σε κείμενο γρήγορα. Μάθετε πώς να εξάγετε κείμενο από εικόνες χρησιμοποιώντας το
  Aspose.OCR με βήμα‑βήμα κώδικα.
draft: false
keywords:
- batch OCR processing
- extract text from images
- convert images to text
language: el
og_description: Η επεξεργασία OCR σε παρτίδες σε C# μετατρέπει εικόνες σε κείμενο.
  Ακολουθήστε αυτόν τον οδηγό για να εξάγετε κείμενο από εικόνες χρησιμοποιώντας το
  Aspose.OCR.
og_title: Ομαδική επεξεργασία OCR σε C# – Εξαγωγή κειμένου από εικόνες
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Batch OCR processing in C# lets you convert images to text quickly.
    Learn how to extract text from images using Aspose.OCR with step‑by‑step code.
  headline: Batch OCR Processing in C# – Complete Guide to Extract Text from Images
  type: TechArticle
- description: Batch OCR processing in C# lets you convert images to text quickly.
    Learn how to extract text from images using Aspose.OCR with step‑by‑step code.
  name: Batch OCR Processing in C# – Complete Guide to Extract Text from Images
  steps:
  - name: Expected Output
    text: 'Assuming you have three images (`invoice1.png`, `receipt2.jpg`, `form3.tif`)
      in the input folder, the output folder will contain:'
  - name: What if some images fail to process?
    text: '`OcrBatchProcessor` logs errors to the console by default and continues
      with the next file. For production use, you can subscribe to the `OnError` event
      to collect failed filenames and retry later.'
  - name: Can I process PDFs directly?
    text: Yes. Aspose.OCR treats each page of a PDF as an image internally. Just point
      `InputFolder` to a directory containing PDFs, and the processor will extract
      text from every page—effectively **convert images to text** even when the source
      is a PDF.
  - name: How do I handle multi‑language documents?
    text: Set `Language` to `OcrLanguage.Multilingual` or specify a list of languages
      if the library version supports it. The engine will attempt to recognize characters
      from all provided languages, which is handy for international invoices.
  - name: What about memory consumption?
    text: The batch processor streams each image, so memory usage stays low even with
      thousands of files. However, enabling a high `MaxDegreeOfParallelism` on a memory‑constrained
      machine could cause spikes. Monitor your RAM and adjust the thread count accordingly.
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: Ομαδική επεξεργασία OCR σε C# – Πλήρης οδηγός για την εξαγωγή κειμένου από
  εικόνες
url: /el/net/text-recognition/batch-ocr-processing-in-c-complete-guide-to-extract-text-fro/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Επεξεργασία OCR σε Παρτίδες με C# – Πλήρης Οδηγός για την Εξαγωγή Κειμένου από Εικόνες

Έχετε αναρωτηθεί ποτέ πώς να κάνετε **επεξεργασία OCR σε παρτίδες** με C# χωρίς να γράφετε ξεχωριστό βρόχο για κάθε εικόνα; Δεν είστε οι μόνοι. Όταν έχετε δεκάδες—ή και εκατοντάδες—σαρωμένες αποδείξεις, τιμολόγια ή χειρόγραφα σημειώματα, η χειροκίνητη τροφοδότηση κάθε αρχείου σε μια μηχανή OCR γίνεται γρήγορα εφιάλτης.  

Τα καλά νέα; Με το Aspose.OCR μπορείτε να *μετατρέψετε εικόνες σε κείμενο* με μια ενιαία, καθαρή ενέργεια. Σε αυτό το tutorial θα περάσουμε από όλη τη ροή εργασίας, από την εγκατάσταση της βιβλιοθήκης μέχρι την εκτέλεση μιας παραγωγικής, έτοιμης για χρήση παρτίδας που **εξάγει κείμενο από εικόνες** και αποθηκεύει τα αποτελέσματα στη μορφή που χρειάζεστε.

> **Τι θα πάρετε:** Μια έτοιμη προς εκτέλεση εφαρμογή κονσόλας που επεξεργάζεται ολόκληρο φάκελο, γράφει αρχεία plain‑text (ή JSON, XML, HTML, PDF) δίπλα στα αρχικά αρχεία, και σας δείχνει πώς να ρυθμίσετε το parallelism για μέγιστη απόδοση.

## Προαπαιτούμενα

- .NET 6.0 SDK ή νεότερο (ο κώδικας λειτουργεί τόσο με .NET Core όσο και με .NET Framework)
- Visual Studio 2022, VS Code ή οποιονδήποτε επεξεργαστή C# προτιμάτε
- Άδεια Aspose.OCR NuGet (μια δωρεάν δοκιμή λειτουργεί για αξιολόγηση)
- Ένας φάκελος με αρχεία εικόνας (`.png`, `.jpg`, `.tif`, κλπ.) που θέλετε να **μετατρέψετε εικόνες σε κείμενο**

Αν έχετε τσεκάρει όλα τα παραπάνω, ας βουτήξουμε.

![Diagram illustrating batch OCR processing flow](batch-ocr-workflow.png "Batch OCR processing flow")

## Βήμα 1: Εγκατάσταση Aspose.OCR μέσω NuGet

Πρώτα, προσθέστε το πακέτο Aspose.OCR στο project σας. Ανοίξτε ένα τερματικό στον φάκελο του project και εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

Ή, αν βρίσκεστε μέσα στο Visual Studio, κάντε δεξί‑κλικ στο *Dependencies → Manage NuGet Packages*, ψάξτε για **Aspose.OCR** και κάντε κλικ στο *Install*. Αυτή η εντολή φέρνει όλα όσα χρειάζεστε για **επεξεργασία OCR σε παρτίδες**.

> **Pro tip:** Κρατήστε την έκδοση του πακέτου ενημερωμένη· η τελευταία έκδοση (από τον Ιούνιο 2026) προσθέτει υποστήριξη για νέες μορφές εικόνας και βελτιώνει την πολυγλωσσική ακρίβεια.

## Βήμα 2: Δημιουργία του Σκελετού της Κονσόλας

Δημιουργήστε μια νέα εφαρμογή κονσόλας C# (αν δεν το έχετε κάνει ήδη) και αντικαταστήστε το παραγόμενο `Program.cs` με το παρακάτω σκελετό. Παρατηρήστε την οδηγία `using Aspose.OCR;` στην κορυφή – αυτό είναι το namespace που μας δίνει την κλάση `OcrBatchProcessor`.

```csharp
using Aspose.OCR;
using System;

class BatchDemo
{
    static void Main()
    {
        // We'll fill this in later.
    }
}
```

Σε αυτό το σημείο το αρχείο είναι μόνο ένας placeholder, αλλά αποτελεί καθαρό σημείο εκκίνησης για τη λογική **επεξεργασίας OCR σε παρτίδες**.

## Βήμα 3: Αρχικοποίηση του OcrBatchProcessor

Το `OcrBatchProcessor` είναι η μηχανή που σαρώει έναν φάκελο, τρέχει OCR σε κάθε υποστηριζόμενη εικόνα και γράφει το αποτέλεσμα. Η δημιουργία του είναι τόσο απλή όσο:

```csharp
// Step 3: Create an OCR batch processor instance
var ocrBatchProcessor = new OcrBatchProcessor();
```

Γιατί να χρησιμοποιήσετε έναν batch processor αντί για ένα API μονής εικόνας; Η κλάση batch διαχειρίζεται αυτόματα την απαρίθμηση αρχείων, την καταγραφή σφαλμάτων και ακόμη και την παράλληλη εκτέλεση, πράγμα που σημαίνει ότι ξοδεύετε λιγότερο χρόνο σε βρόχους και περισσότερο σε βελτιστοποίηση της ακρίβειας.

## Βήμα 4: Ορισμός Φακέλων Εισόδου και Εξόδου

Πείτε στον επεξεργαστή από πού να διαβάσει τις εικόνες και πού να αποθηκεύσει τα αποτελέσματα. Αντικαταστήστε τις διαδρομές placeholder με πραγματικούς καταλόγους στο σύστημά σας.

```csharp
// Step 4: Configure the input folder containing images to process
ocrBatchProcessor.InputFolder = @"C:\MyProjects\OCRDemo\Images\Batch";

// Step 5: Set the folder where OCR results will be saved
ocrBatchProcessor.OutputFolder = @"C:\MyProjects\OCRDemo\Results\Batch";
```

Και οι δύο φάκελοι πρέπει να υπάρχουν πριν τρέξετε την εφαρμογή· διαφορετικά θα λάβετε `DirectoryNotFoundException`. Η δημιουργία τους προγραμματιστικά είναι εύκολη, αλλά για σαφήνεια κρατάμε το παράδειγμα απλό.

## Βήμα 5: Επιλογή Μορφής Εξόδου

Το Aspose.OCR μπορεί να αποδώσει plain text, JSON, XML, HTML ή ακόμη και PDF. Για τις περισσότερες περιπτώσεις **εξαγωγής κειμένου από εικόνες**, το plain text αρκεί, αλλά μπορείτε να το αλλάξετε όπως θέλετε.

```csharp
// Step 6: Choose the desired output format (e.g., plain text)
ocrBatchProcessor.OutputFormat = ResultFormat.Text;   // alternatives: Json, Xml, Html, Pdf, etc.
```

Αν χρειάζεστε δομημένα δεδομένα για επεξεργασία downstream, το `ResultFormat.Json` είναι μια καλή επιλογή. Η βιβλιοθήκη θα τυλίξει αυτόματα το κείμενο κάθε σελίδας σε ένα JSON αντικείμενο, διατηρώντας πληροφορίες διάταξης.

## Βήμα 6: Ορισμός Γλώσσας και Parallelism

Η ακρίβεια του OCR εξαρτάται από το σωστό μοντέλο γλώσσας. Τα Αγγλικά λειτουργούν για τα περισσότερα Δυτικά έγγραφα, αλλά μπορείτε να επιλέξετε οποιαδήποτε υποστηριζόμενη γλώσσα (Αραβικά, Κινέζικα κλπ.). Επιπλέον, μπορείτε να ορίσετε πόσα νήματα θα χρησιμοποιήσει ο επεξεργαστής—μέχρι τέσσερα από προεπιλογή.

```csharp
// Step 7: Specify the language for OCR recognition
ocrBatchProcessor.Language = OcrLanguage.English;

// Step 8: Define the level of parallelism (up to 4 concurrent threads)
ocrBatchProcessor.MaxDegreeOfParallelism = 4;
```

**Γιατί το parallelism είναι σημαντικό:** Αν έχετε CPU quad‑core, ορίζοντας `MaxDegreeOfParallelism` σε `4` μπορεί να μειώσει τον χρόνο επεξεργασίας περίπου κατά 75 %. Σε laptop με δύο πυρήνες, το `2` είναι πιο ασφαλές. Πειραματιστείτε για να βρείτε το ιδανικό σημείο για το υλικό σας.

## Βήμα 7: Εκτέλεση της Παρτίδας

Τώρα γίνεται η βαριά δουλειά. Μία γραμμή εκκινεί ολόκληρο το pipeline, επεξεργαζόμενη κάθε εικόνα στον φάκελο εισόδου και γράφοντας τα αποτελέσματα στον φάκελο εξόδου.

```csharp
// Step 9: Execute the batch processing of all supported image files
ocrBatchProcessor.Execute();

Console.WriteLine("Batch OCR completed.");
```

Όταν η κονσόλα εμφανίσει *Batch OCR completed.*, θα βρείτε ένα αρχείο `.txt` (ή όποια μορφή έχετε επιλέξει) δίπλα σε κάθε αρχική εικόνα. Τα ονόματα αρχείων ταιριάζουν με την πηγή, καθιστώντας την αντιστοίχηση OCR‑output με την αρχική εικόνα τελείως απλή.

## Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε στο `Program.cs` και να τρέξετε αμέσως:

```csharp
using Aspose.OCR;
using System;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create an OCR batch processor instance
        var ocrBatchProcessor = new OcrBatchProcessor();

        // Step 2: Configure the input folder containing images to process
        ocrBatchProcessor.InputFolder = @"C:\MyProjects\OCRDemo\Images\Batch";

        // Step 3: Set the folder where OCR results will be saved
        ocrBatchProcessor.OutputFolder = @"C:\MyProjects\OCRDemo\Results\Batch";

        // Step 4: Choose the desired output format (plain text is default)
        ocrBatchProcessor.OutputFormat = ResultFormat.Text; // alternatives: Json, Xml, Html, Pdf, etc.

        // Step 5: Specify the language for OCR recognition
        ocrBatchProcessor.Language = OcrLanguage.English;

        // Step 6: Define the level of parallelism (up to 4 concurrent threads)
        ocrBatchProcessor.MaxDegreeOfParallelism = 4;

        // Step 7: Execute the batch processing of all supported image files
        ocrBatchProcessor.Execute();

        Console.WriteLine("Batch OCR completed.");
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Υποθέτοντας ότι έχετε τρεις εικόνες (`invoice1.png`, `receipt2.jpg`, `form3.tif`) στον φάκελο εισόδου, ο φάκελος εξόδου θα περιέχει:

```
invoice1.txt
receipt2.txt
form3.txt
```

Κάθε αρχείο `.txt` περιέχει τους ακατέργαστους χαρακτήρες που εξήχθησαν από την αντίστοιχη εικόνα. Ανοίξτε οποιοδήποτε αρχείο με το Notepad και θα δείτε την plain‑text αναπαράσταση του αρχικού scan.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν κάποιες εικόνες αποτύχουν να επεξεργαστούν;

Το `OcrBatchProcessor` καταγράφει σφάλματα στην κονσόλα από προεπιλογή και συνεχίζει με το επόμενο αρχείο. Για παραγωγική χρήση, μπορείτε να εγγραφείτε στο γεγονός `OnError` ώστε να συλλέγετε τα ονόματα των αποτυχημένων αρχείων και να τα ξαναπροσπαθήσετε αργότερα.

```csharp
ocrBatchProcessor.OnError += (sender, args) =>
{
    Console.WriteLine($"Failed on {args.FileName}: {args.Exception.Message}");
};
```

### Μπορώ να επεξεργαστώ PDF απευθείας;

Ναι. Το Aspose.OCR αντιμετωπίζει κάθε σελίδα ενός PDF ως εικόνα εσωτερικά. Απλώς δείξτε το `InputFolder` σε έναν κατάλογο που περιέχει PDF και ο επεξεργαστής θα εξάγει κείμενο από κάθε σελίδα—ενσωματώνοντας ουσιαστικά **μετατροπή εικόνων σε κείμενο** ακόμη και όταν η πηγή είναι PDF.

### Πώς να διαχειριστώ έγγραφα πολλαπλών γλωσσών;

Ορίστε το `Language` σε `OcrLanguage.Multilingual` ή καθορίστε μια λίστα γλωσσών αν η έκδοση της βιβλιοθήκης το υποστηρίζει. Η μηχανή θα προσπαθήσει να αναγνωρίσει χαρακτήρες από όλες τις παρεχόμενες γλώσσες, κάτι πολύ χρήσιμο για διεθνή τιμολόγια.

### Τι γίνεται με την κατανάλωση μνήμης;

Ο batch processor κάνει streaming κάθε εικόνα, έτσι η χρήση μνήμης παραμένει χαμηλή ακόμη και με χιλιάδες αρχεία. Ωστόσο, η ενεργοποίηση υψηλού `MaxDegreeOfParallelism` σε μηχάνημα με περιορισμένη μνήμη μπορεί να προκαλέσει αιχμές. Παρακολουθήστε το RAM σας και προσαρμόστε τον αριθμό των νημάτων ανάλογα.

## Συμβουλές για Καλύτερη Ακρίβεια

- **Pre‑process images**: Καθαρίστε τον θόρυβο, διορθώστε την κλίση και μετατρέψτε σε γκρι κλίμακα πριν το OCR. Το Aspose.OCR προσφέρει `ImagePreprocessOptions` που μπορείτε να συνδέσετε στο `ocrBatchProcessor`.
- **Choose the right format**: Αν χρειάζεστε διατήρηση της διάταξης, τα `ResultFormat.Html` ή `Pdf` κρατούν τις αλλαγές γραμμής και βασικό στυλ.
- **Validate results**: Υλοποιήστε ένα απλό βήμα post‑processing που ελέγχει για κενά αρχεία εξόδου—συνήθως υποδεικνύουν αποτυχία αναγνώρισης.

## Επόμενα Βήματα

Τώρα που έχετε κατακτήσει **επεξεργασία OCR σε παρτίδες** για **εξαγωγή κειμένου από εικόνες**, ίσως θέλετε να:

- **Integrate with a database** – αποθηκεύσετε κάθε αποτέλεσμα OCR μαζί με μεταδεδομένα για αναζήτηση.
- **Add a UI** – δημιουργήσετε μια μικρή διεπαφή WPF ή WinForms που να επιτρέπει στους χρήστες να σύρουν‑και‑αποθέτουν φακέλους.
- **Scale out** – τρέξετε την παρτίδα σε Azure Functions ή AWS Lambda για cloud‑native επεξεργασία.

Κάθε ένα από αυτά τα θέματα βασίζεται στις ίδιες βασικές έννοιες που καλύψαμε, οπότε είστε έτοιμοι να επεκτείνετε τη λύση σας.

---

**Καλή προγραμματιστική!** Αν αντιμετωπίσετε κάποιο πρόβλημα ή έχετε ιδέες για βελτιώσεις, αφήστε ένα σχόλιο παρακάτω. Ας συνεχίσουμε τη συζήτηση και ας κάνουμε την αυτοματοποίηση OCR ακόμη πιο ομαλή.

## Τι Πρέπει να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση των δικών σας έργων.

- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}