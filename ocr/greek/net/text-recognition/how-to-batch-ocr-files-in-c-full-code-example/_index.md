---
category: general
date: 2026-02-17
description: Πώς να κάνετε μαζική OCR πολλαπλών PDF και εικόνων σε C# χρησιμοποιώντας
  το Aspose OCR. Μάθετε να εξάγετε κείμενο από PDF, να μετατρέπετε PDF σε κείμενο
  και να αναγνωρίζετε κείμενο από εικόνες.
draft: false
keywords:
- how to batch OCR
- extract text from pdf
- convert pdf to text
- recognize text from images
- extract text scanned pdf
language: el
og_description: Πώς να εκτελέσετε μαζική OCR σε πολλά έγγραφα με C# και Aspose OCR.
  Λάβετε κώδικα βήμα‑προς‑βήμα για την εξαγωγή κειμένου από PDF, τη μετατροπή PDF
  σε κείμενο και την αναγνώριση κειμένου από εικόνες.
og_title: Πώς να επεξεργαστείτε μαζικά αρχεία OCR σε C# – Πλήρης Οδηγός
tags:
- OCR
- C#
- Aspose
- PDF
- Text Extraction
title: Πώς να επεξεργαστείτε σε παρτίδες αρχεία OCR σε C# – Πλήρες παράδειγμα κώδικα
url: /el/net/text-recognition/how-to-batch-ocr-files-in-c-full-code-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να κάνετε batch OCR αρχεία σε C# – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να κάνετε batch OCR** σε μια στοίβα PDF και σαρωμένων εικόνων χωρίς να γράψετε ξεχωριστό βρόχο για κάθε αρχείο; Δεν είστε μόνοι. Οι περισσότεροι προγραμματιστές συναντούν αυτό το εμπόδιο όταν χρειάζεται να εξάγουν κείμενο από δεκάδες σελίδες με μία κίνηση. Τα καλά νέα; Με το Aspose OCR μπορείτε να τροφοδοτήσετε μια συλλογή αρχείων σε μία μηχανή και να αφήσετε αυτήν να κάνει το σκληρό έργο.

Σε αυτό το tutorial θα περάσουμε βήμα-βήμα μια πρακτική λύση που σας επιτρέπει να **εξάγετε κείμενο από pdf**, **μετατρέψετε pdf σε κείμενο**, και **αναγνωρίσετε κείμενο από εικόνες** όλα σε μία εκτέλεση batch. Στο τέλος θα έχετε μια έτοιμη για εκτέλεση εφαρμογή console που εκτυπώνει το αποτέλεσμα OCR για κάθε σελίδα, και θα κατανοήσετε το «γιατί» πίσω από κάθε βήμα ώστε να το προσαρμόσετε στα δικά σας έργα.

## Προαπαιτούμενα – Τι Χρειάζεστε Πριν Ξεκινήσετε

- **.NET 6.0 ή νεότερο** (ο κώδικας λειτουργεί και σε .NET Framework, αλλά συνιστάται .NET 6+)
- **Πακέτο NuGet Aspose.OCR** – εγκαταστήστε το με `dotnet add package Aspose.OCR`
- Μερικά δείγμα αρχεία: ένα πολυ-σελίδα PDF (`doc1.pdf`) και ένα σαρωμένο TIFF (`doc2.tif`). Τοποθετήστε τα σε έναν φάκελο που μπορείτε να αναφέρετε, π.χ., `C:\OCRSamples`.
- Βασικές γνώσεις C# – πρέπει να είστε άνετοι με τις δηλώσεις `using` και τις συλλογές.

> Συμβουλή: Αν δεν έχετε άδεια, η Aspose προσφέρει ένα δωρεάν προσωρινό κλειδί που αφαιρεί το όριο των 100 σελίδων κατά την ανάπτυξη.

## Βήμα 1: Ρύθμιση του Έργου και Εισαγωγή Namespaces

Πρώτα, δημιουργήστε ένα νέο έργο console (ή προσθέστε σε υπάρχον) και φέρετε τα απαιτούμενα namespaces.

```csharp
// Program.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;          // Aspose OCR core library
using Aspose.OCR.Image;   // ImageStream helper class
```

> **Γιατί είναι σημαντικό:** Η εισαγωγή του `Aspose.OCR.Image` σας παρέχει τη βολική μέθοδο `ImageStream.FromFile`, η οποία αυτόματα χωρίζει τις σελίδες PDF σε ξεχωριστά ρεύματα εικόνας. Αυτό είναι το μυστικό που κάνει την επεξεργασία batch άνετη.

## Βήμα 2: Αρχικοποίηση του OCR Engine

Η μηχανή είναι το βασικό στοιχείο που επικοινωνεί με τον υποκείμενο OCR engine. Χρειάζεστε μόνο μία παρουσία για ολόκληρο το batch.

```csharp
// Step 2: Create a single OcrEngine instance
OcrEngine ocrEngine = new OcrEngine();
```

> **Εξήγηση:** Η επαναχρησιμοποίηση του ίδιου `OcrEngine` μειώνει την κατανάλωση μνήμης και επιταχύνει την επεξεργασία επειδή οι εγγενείς βιβλιοθήκες παραμένουν φορτωμένες μεταξύ των σελίδων.

## Βήμα 3: Δημιουργία Λίστας Image Streams

Εδώ συγκεντρώνουμε κάθε έγγραφο που θέλουμε να επεξεργαστούμε. Η `ImageStream.FromFile` είναι αρκετά έξυπνη ώστε να διασπά ένα PDF σε μεμονωμένες σελίδες, έτσι ένα τρι-σελίδα PDF γίνεται τρία ξεχωριστά ρεύματα στο παρασκήνιο.

```csharp
// Step 3: Assemble the collection of image streams
List<ImageStream> imageStreams = new List<ImageStream>
{
    ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
    ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
};
```

> **Ακραία περίπτωση:** Αν έχετε ένα μείγμα PDF, TIFF, JPEG ή PNG, απλώς προσθέστε τα στην ίδια λίστα – το Aspose διαχειρίζεται αυτόματα την ανίχνευση μορφής.

## Βήμα 4: Εκτέλεση της Λειτουργίας Batch OCR

Τώρα παραδίδουμε τη λίστα στη μηχανή. Η `RecognizeBatch` επιστρέφει μια συλλογή αντικειμένων `OcrResult`, ένα ανά σελίδα.

```csharp
// Step 4: Perform batch OCR on the supplied streams
IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

> **Γιατί batch;** Η εκτέλεση OCR σελίδα‑με‑σελίδα σε έναν χειροκίνητο βρόχο αναγκάζει τη μηχανή να επανεκκινείται κάθε φορά, κάτι που μπορεί να διπλασιάσει το χρόνο επεξεργασίας. Η `RecognizeBatch` διατηρεί τη μηχανή ενεργή και στέλνει τα αποτελέσματα καθώς είναι διαθέσιμα.

## Βήμα 5: Έξοδος του Αναγνωρισμένου Κειμένου

Τέλος, διασχίζουμε τα αποτελέσματα και γράφουμε το κείμενο κάθε σελίδας στην κονσόλα. Εδώ μπορείτε να αντικαταστήσετε το `Console.WriteLine` με εγγραφές σε αρχείο, εισαγωγές σε βάση δεδομένων ή οποιαδήποτε άλλη ενέργεια downstream.

```csharp
// Step 5: Display the OCR output for each page
for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
{
    Console.WriteLine($"--- Page {pageIndex + 1} ---");
    Console.WriteLine(ocrResults[pageIndex].Text);
}
```

### Αναμενόμενη Έξοδος Κονσόλας

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore...
--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

Αν εκτελέσετε το πρόγραμμα με τα δείγμα αρχεία, θα δείτε ένα μπλοκ κειμένου για κάθε σελίδα, αποδεικνύοντας ότι έχετε εξάγει επιτυχώς **κείμενο από σαρωμένο pdf** σε μία μόνο εκτέλεση.

## Διαχείριση Συνηθισμένων Προβλημάτων

| Πρόβλημα | Γιατί Συμβαίνει | Γρήγορη Διόρθωση |
|----------|----------------|-------------------|
| **Σφάλματα έλλειψης μνήμης** | Τα μεγάλα PDF δημιουργούν πολλές εικόνες υψηλής ανάλυσης. | Περιορίστε το DPI κατά τη φόρτωση PDF: `ocrEngine.Settings.ImageDpi = 200;` |
| **Ασυνήθιστοι χαρακτήρες** | Η πηγή σάρωσης είναι χαμηλής ποιότητας ή χρησιμοποιεί μη υποστηριζόμενη γλώσσα. | Ορίστε ρητά τη γλώσσα: `ocrEngine.Language = Language.English;` |
| **Μερικά αποτελέσματα** | Η λίστα batch περιέχει κατεστραμμένο αρχείο. | Τυλίξτε τη `RecognizeBatch` σε try/catch και καταγράψτε το `e.Message` για το προβληματικό αρχείο. |
| **Σ bottleneck απόδοσης** | Εκτέλεση σε ένα νήμα σε πολυπύρημη μηχανή. | Χρησιμοποιήστε `Parallel.ForEach` με ξεχωριστές παρουσίες `OcrEngine` ανά νήμα (προχωρημένο). |

## Μπόνους: Αποθήκευση Αποτελεσμάτων OCR σε Αρχεία Κειμένου

Αν προτιμάτε να διατηρείτε ξεχωριστό αρχείο `.txt` ανά σελίδα, απλώς προσθέστε ένα μικρό τμήμα εγγραφής μέσα στον βρόχο:

```csharp
string outputPath = @"C:\OCRResults";
System.IO.Directory.CreateDirectory(outputPath);

for (int i = 0; i < ocrResults.Count; i++)
{
    string fileName = System.IO.Path.Combine(outputPath, $"Page_{i + 1}.txt");
    System.IO.File.WriteAllText(fileName, ocrResults[i].Text);
}
```

Τώρα έχετε μετατρέψει **convert pdf to text** σε έναν τακτοποιημένο φάκελο απλών αρχείων κειμένου—ιδανικό για downstream ευρετηρίαση ή αναζήτηση.

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω βρίσκεται το πλήρες πρόγραμμα, έτοιμο για αντιγραφή‑και‑επικόλληση. Χωρίς κρυφές εξαρτήσεις, χωρίς εξωτερικά scripts.

```csharp
// FullProgram.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Initialise OCR engine (reuse for the whole batch)
        OcrEngine ocrEngine = new OcrEngine();

        // Optional: tweak settings for speed or accuracy
        ocrEngine.Settings.ImageDpi = 200;          // lower memory usage
        ocrEngine.Language = Language.English;     // set language explicitly

        // Build the list of image streams (PDF pages auto‑split)
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
            ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
        };

        // Perform batch OCR
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Output each page's text to console
        for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
        {
            Console.WriteLine($"--- Page {pageIndex + 1} ---");
            Console.WriteLine(ocrResults[pageIndex].Text);
        }

        // (Optional) Save each page to a .txt file
        string outputFolder = @"C:\OCRResults";
        System.IO.Directory.CreateDirectory(outputFolder);
        for (int i = 0; i < ocrResults.Count; i++)
        {
            string txtPath = System.IO.Path.Combine(outputFolder, $"Page_{i + 1}.txt");
            System.IO.File.WriteAllText(txtPath, ocrResults[i].Text);
        }
    }
}
```

Εκτελέστε `dotnet run` από το φάκελο του έργου και παρακολουθήστε την κονσόλα να γεμίζει με το εξαγόμενο κείμενο. Αυτό είναι **πώς να κάνετε batch OCR** μια συλλογή εγγράφων με λίγες μόνο γραμμές C#.

## Τι Καλύψαμε – Σύντομη Ανακεφαλαίωση

- Ρύθμιση εφαρμογής .NET console και εγκατάσταση του Aspose.OCR.
- Δημιουργία μιας μοναδικής παρουσίασης `OcrEngine` για αποδοτική διαδικασία.
- Δημιουργία λίστας αντικειμένων `ImageStream` που αυτόματα χωρίζουν τα PDF σε σελίδες.
- Εκτέλεση `RecognizeBatch` για **εξαγωγή κειμένου από pdf** και άλλες μορφές εικόνας σε μία κίνηση.
- Εκτύπωση των αποτελεσμάτων και προαιρετική αποθήκευση ως ξεχωριστά αρχεία `.txt`, ολοκληρώνοντας τη ροή εργασίας **convert pdf to text**.

## Επόμενα Βήματα και Σχετικά Θέματα

- **Κλιμάκωση**: Χρησιμοποιήστε `Parallel.ForEach` με μια ομάδα αντικειμένων `OcrEngine` για επεξεργασία εκατοντάδων αρχείων ταυτόχρονα.
- **Πακέτα γλώσσας**: Αντικαταστήστε το `Language.English` με `Language.French` ή φορτώστε ένα προσαρμοσμένο λεξικό όταν χρειάζεται να **αναγνωρίσετε κείμενο από εικόνες** σε άλλες γλώσσες.
- **Μετα-επεξεργασία**: Διέλθετε το αποτέλεσμα OCR μέσω ελεγκτή ορθογραφίας ή parser φυσικής γλώσσας για βελτίωση της ακρίβειας σε σαρωμένα συμβόλαια.
- **Εναλλακτικές βιβλιοθήκες**: Συγκρίνετε το Aspose OCR με το Tesseract.NET αν ψάχνετε για ανοιχτή λύση—και τα δύο μπορούν να **εξάγουν κείμενο από σαρωμένο pdf** αλλά διαφέρουν σε άδεια χρήσης και ακρίβεια εκτός κουτιού.

![πώς να κάνετε batch OCR παράδειγμα](alt="πώς να κάνετε batch OCR παράδειγμα")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}