---
category: general
date: 2026-04-26
description: Πώς να κάνετε μαζική OCR εικόνων PNG γρήγορα. Μάθετε να εξάγετε κείμενο
  από PNG, να μετατρέπετε εικόνες σε κείμενο, να γράφετε το αναγνωρισμένο κείμενο
  και να διαβάζετε τον φάκελο PNG με το Aspose OCR.
draft: false
keywords:
- how to batch OCR
- extract text from png
- convert images to text
- write recognized text
- read png directory
language: el
og_description: Πώς να επεξεργαστείτε μαζικά εικόνες PNG με OCR σε C# χρησιμοποιώντας
  το Aspose OCR. Αυτός ο οδηγός δείχνει πώς να εξάγετε κείμενο από PNG, να μετατρέψετε
  τις εικόνες σε κείμενο και να γράψετε το αναγνωρισμένο κείμενο αποδοτικά.
og_title: Πώς να κάνετε ομαδική OCR εικόνων PNG σε C# – Βήμα‑προς‑βήμα
tags:
- OCR
- C#
- Aspose
title: Πώς να κάνετε ομαδική OCR εικόνων PNG σε C# – Πλήρης Οδηγός
url: /el/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εκτελέσετε Batch OCR σε PNG Εικόνες με C# – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να κάνετε batch OCR** σε ολόκληρο φάκελο αρχείων PNG χωρίς να γράψετε ξεχωριστό πρόγραμμα για κάθε εικόνα; Δεν είστε μόνοι που διαχειρίζεστε δεκάδες στιγμιότυπα, σαρωμένες αποδείξεις ή γραφικά που πρέπει να μετατραπούν σε αναζητήσιμο κείμενο. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από μια πρακτική λύση που **εξάγει κείμενο από PNG**, **μετατρέπει εικόνες σε κείμενο**, και **γράφει το αναγνωρισμένο κείμενο** σε ξεχωριστά αρχεία — όλα ενώ διαβάζει αυτόματα το φάκελο PNG.

Στο τέλος αυτού του οδηγού θα έχετε μια έτοιμη προς εκτέλεση εφαρμογή C# console που επεξεργάζεται όποιον αριθμό εικόνων σε μία μόνο εκτέλεση. Χωρίς επιπλέον scripts, χωρίς χειροκίνητο copy‑paste — μόνο καθαρός κώδικας που κάνει τη βαριά δουλειά για εσάς.

## Τι Θα Χρειαστείτε

- **.NET 6.0** ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework).  
- **Aspose.OCR for .NET** πακέτο NuGet (η δωρεάν δοκιμή λειτουργεί για δοκιμές).  
- Ένας φάκελος με μερικά *.png* αρχεία που θέλετε να OCR‑άτε.  
- Visual Studio 2022 ή οποιοδήποτε IDE C# προτιμάτε.

Αν έχετε όλα αυτά, μπορούμε να περάσουμε κατευθείαν στην υλοποίηση.

## Βήμα 1 – Προετοιμάστε τους Φακέλους Εισόδου και Εξόδου *(Read PNG Directory)*

Το πρώτο που κάνουμε είναι να δείξουμε στο πρόγραμμα ποιος φάκελος περιέχει τις εικόνες και πού θα αποθηκευτούν τα παραγόμενα *.txt* αρχεία. Η χρήση του `Directory.GetFiles` μας δίνει μια καθαρή συλλογή όλων των PNG στο φάκελο.

```csharp
using System;
using System.Collections.Generic;
using System.IO;

// Define where the source PNGs are and where the OCR results will be saved
string inputFolder = @"C:\MyProject\BatchImages";   // <-- change to your path
string outputFolder = @"C:\MyProject\BatchOutput";

// Ensure the output folder exists; create it if it doesn’t
if (!Directory.Exists(outputFolder))
{
    Directory.CreateDirectory(outputFolder);
}

// Grab every *.png* file – this is the “read png directory” part
IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
```

**Γιατί είναι σημαντικό:**  
- Η χρήση μπαλαντέρ (`*.png`) εγγυάται ότι επεξεργαζόμαστε μόνο αρχεία εικόνας, αγνοώντας τυχόν τυχαία έγγραφα.  
- Η δημιουργία του φακέλου εξόδου «on the fly» αποτρέπει ένα `DirectoryNotFoundException` αργότερα.

> **Pro tip:** Αν χρειάζεται να υποστηρίξετε και άλλες μορφές (JPEG, BMP), απλώς επεκτείνετε το πρότυπο αναζήτησης ή καλέστε `Directory.EnumerateFiles` με πολλαπλές επεκτάσεις.

## Βήμα 2 – Αρχικοποιήστε τη Μηχανή OCR *(Convert Images to Text)*

Το Aspose.OCR παρέχει δύο τύπους μηχανών: μια CPU‑βασισμένη `OcrEngine` και μια GPU‑επιταχυμένη `GpuOcrEngine`. Για τις περισσότερες εργασίες batch η CPU μηχανή είναι απολύτως επαρκής, αλλά μπορείτε να αλλάξετε το όνομα της κλάσης αν διαθέτετε ισχυρή GPU.

```csharp
using Aspose.OCR;

// Initialise the OCR engine – CPU version
OcrEngine ocrEngine = new OcrEngine();   // Use new GpuOcrEngine() for GPU acceleration

// Set the language to Latin (covers English, French, Spanish, etc.)
ocrEngine.Language = Language.Latin;
```

**Γιατί είναι σημαντικό:**  
- Η καθορισμένη γλώσσα βελτιώνει δραματικά την ακρίβεια, επειδή η μηχανή ξέρει ποιο σύνολο χαρακτήρων να περιμένει.  
- Η αλλαγή σε `GpuOcrEngine` είναι μια γραμμή κώδικα αν αντιμετωπίσετε προβλήματα απόδοσης σε μεγάλα batch.

## Βήμα 3 – Δημιουργήστε έναν Batch Recogniser

Το Aspose παρέχει ένα βολικό `BatchRecognizer` που δέχεται μια συλλογή διαδρομών αρχείων και επιστρέφει τα αποτελέσματα ένα‑ένα. Αυτό αποφεύγει τη φόρτωση όλων των εικόνων στη μνήμη ταυτόχρονα — μια κρίσιμη λεπτομέρεια για μεγάλους φακέλους.

```csharp
// Build a batch recogniser that will use the previously configured engine
BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);
```

**Γιατί είναι σημαντικό:**  
- Ο batch recogniser ενσωματώνει τη λογική του βρόχου, επιτρέποντάς μας να εστιάσουμε στο τι κάνουμε με κάθε αποτέλεσμα αντί στο πώς να το επαναλάβουμε με ασφάλεια.

## Βήμα 4 – Εκτελέστε OCR σε Όλες τις Εικόνες και Γράψτε το Αποτέλεσμα *(Write Recognized Text)*

Τώρα εκτελούμε το OCR. Η μέθοδος `Recognize` επιστρέφει ένα `IEnumerable<RecognitionResult>` όπου κάθε αποτέλεσμα περιέχει το εξαγόμενο κείμενο και άλλα μεταδεδομένα.

```csharp
// Perform OCR on the entire collection of PNG files
IEnumerable<RecognitionResult> recognitionResults = batchRecognizer.Recognize(inputImageFiles);

// Write each recognised text to a separate *.txt* file
int fileIndex = 0;
foreach (RecognitionResult result in recognitionResults)
{
    // Build a unique output filename – out_0.txt, out_1.txt, …
    string outputPath = Path.Combine(outputFolder, $"out_{fileIndex++}.txt");

    // Save the plain text to disk
    File.WriteAllText(outputPath, result.Text);
}
```

**Γιατί είναι σημαντικό:**  
- Η χρήση του `File.WriteAllText` εξασφαλίζει ότι το κείμενο αποθηκεύεται με κωδικοποίηση UTF‑8 από προεπιλογή, διατηρώντας ειδικούς χαρακτήρες.  
- Η διαδοχική ονομασία (`out_0.txt`, `out_1.txt`) ταιριάζει με τη σειρά επεξεργασίας, κάτι χρήσιμο για εντοπισμό σφαλμάτων.

> **Edge case:** Αν κάποια εικόνα αποτύχει στο OCR (π.χ. κατεστραμμένο αρχείο), το `RecognitionResult.Text` θα είναι κενό. Μπορείτε να προσθέσετε έναν απλό έλεγχο μέσα στον βρόχο για να καταγράψετε τις αποτυχίες:

```csharp
if (string.IsNullOrWhiteSpace(result.Text))
{
    Console.WriteLine($"Warning: No text extracted from {inputImageFiles.ElementAt(fileIndex - 1)}");
}
```

## Βήμα 5 – Συνδυάστε Όλα – Πλήρες Παράδειγμα Εργασίας

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα νέο console project. Περιλαμβάνει τις οδηγίες `using`, την επικύρωση των φακέλων, και ένα μικρό UI στην κονσόλα ώστε να ξέρετε πότε ολοκληρώθηκε το batch.

```csharp
// ---------------------------------------------------------------
// Batch OCR for PNG files using Aspose.OCR
// ---------------------------------------------------------------
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Define input & output directories
        string inputFolder = @"C:\MyProject\BatchImages";   // <-- adjust
        string outputFolder = @"C:\MyProject\BatchOutput";

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"Error: Input folder does not exist -> {inputFolder}");
            return;
        }

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ Gather all PNG files
        IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
        Console.WriteLine($"Found {inputImageFiles?.Count() ?? 0} PNG files to process.");

        // 3️⃣ Initialise OCR engine (CPU) and set language
        OcrEngine ocrEngine = new OcrEngine();   // Swap with GpuOcrEngine() if needed
        ocrEngine.Language = Language.Latin;

        // 4️⃣ Create batch recogniser
        BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);

        // 5️⃣ Run OCR and write results
        IEnumerable<RecognitionResult> results = batchRecognizer.Recognize(inputImageFiles);
        int index = 0;
        foreach (RecognitionResult result in results)
        {
            string outPath = Path.Combine(outputFolder, $"out_{index++}.txt");
            File.WriteAllText(outPath, result.Text);
        }

        Console.WriteLine($"✅ OCR complete! Text files saved to {outputFolder}");
    }
}
```

**Αναμενόμενη έξοδος:**  
Η εκτέλεση του προγράμματος εκτυπώνει κάτι σαν:

```
Found 12 PNG files to process.
✅ OCR complete! Text files saved to C:\MyProject\BatchOutput
```

Και θα δείτε τα `out_0.txt` … `out_11.txt` μέσα στο φάκελο εξόδου, το καθένα με την απλή‑κείμενη έκδοση της αντίστοιχης εικόνας.

## Συχνές Ερωτήσεις & Συμβουλές

| Ερώτηση | Απάντηση |
|----------|--------|
| *Μπορώ να κάνω OCR και σε υπο‑φακέλους;* | Ναι — αντικαταστήστε το `Directory.GetFiles` με `Directory.EnumerateFiles(inputFolder, "*.png", SearchOption.AllDirectories)`. |
| *Τι γίνεται αν χρειαστώ διαφορετική γλώσσα;* | Ορίστε `ocrEngine.Language = Language.Spanish;` (ή οποιοδήποτε υποστηριζόμενο enum). |
| *Πώς να διαχειριστώ τεράστια batch (χίλια αρχεία);* | Σκεφτείτε την επεξεργασία σε τμήματα ή τη χρήση `Parallel.ForEach` με περιορισμένο βαθμό παραλληλισμού για να μην εξαντλήσετε τη μνήμη. |
| *Η έξοδος είναι πάντα UTF‑8;* | Το `File.WriteAllText` προεπιλογή είναι UTF‑8 χωρίς BOM, που λειτουργεί για τις περισσότερες γλώσσες με λατινικό αλφάβητο. Για ασιατικές γραφές ίσως χρειαστεί να ορίσετε ρητά `Encoding.UTF8`. |
| *Μπορώ να λάβω βαθμολογίες εμπιστοσύνης;* | Το `RecognitionResult` εκθέτει το `Confidence` — μπορείτε να το καταγράψετε μαζί με το κείμενο για έλεγχο ποιότητας. |

## Οπτική Επισκόπηση *(How to Batch OCR – Diagram)*

![Διάγραμμα ροής batch OCR που δείχνει φάκελο εισόδου → μηχανή OCR → batch recogniser → αρχεία txt εξόδου](https://example.com/diagram-how-to-batch-ocr.png "Διάγραμμα batch OCR")

*Το alt κείμενο περιέχει τη βασική λέξη‑κλειδί, ικανοποιώντας τις απαιτήσεις SEO για εικόνες.*

## Συμπεράσματα

Μόλις καλύψαμε **πώς να κάνετε batch OCR** σε έναν φάκελο PNG αρχείων χρησιμοποιώντας το Aspose.OCR, από την ανάγνωση του φακέλου PNG μέχρι τη δημιουργία κάθε αρχείου κειμένου. Η λύση είναι πλήρως αυτόνομη, λειτουργεί σε οποιοδήποτε σύγχρονο .NET runtime, και μπορεί να επεκταθεί για επιτάχυνση GPU, υποστήριξη πολλαπλών γλωσσών ή παράλληλη επεξεργασία.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να αντικαταστήσετε το `Language.Latin` με άλλη γλώσσα, ή ενσωματώστε την έξοδο σε έναν δείκτη αναζήτησης ώστε τα έγγραφά σας να γίνουν άμεσα αναζητήσιμα. Ο ουρανός είναι το όριο μόλις κυριαρχήσετε το batch OCR.

Καλή προγραμματιστική, και πείτε μας στα σχόλια αν αντιμετωπίσετε κάποιο πρόβλημα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}