---
category: general
date: 2026-05-31
description: Μάθετε πώς να λαμβάνετε βαθμολογίες εμπιστοσύνης OCR σε C# ενώ εξάγετε
  κείμενο από εικόνα και διαβάζετε την εικόνα απόδειξης με το Aspose OCR.
draft: false
keywords:
- ocr confidence scores
- extract text from image
- ocr bounding boxes
- perform ocr on jpg
- read receipt image
language: el
og_description: Οι βαθμοί εμπιστοσύνης OCR σάς επιτρέπουν να αξιολογήσετε την ακρίβεια·
  αυτός ο οδηγός δείχνει πώς να εξάγετε κείμενο από εικόνα, να λάβετε τα πλαίσια περιγράμματος
  και να διαβάσετε την εικόνα απόδειξης χρησιμοποιώντας το Aspose OCR.
og_title: Βαθμολογίες εμπιστοσύνης OCR σε C# – Πλήρης Οδηγός
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get OCR confidence scores in C# while extract text from
    image and read receipt image with Aspose OCR.
  headline: OCR confidence scores in C# – Complete Guide
  type: TechArticle
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Βαθμοί εμπιστοσύνης OCR σε C# – Πλήρης οδηγός
url: /el/net/ocr-optimization/ocr-confidence-scores-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Βαθμοί εμπιστοσύνης OCR σε C# – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ πώς να **βάλετε βαθμούς εμπιστοσύνης OCR** όταν χρειάζεται να *εξάγετε κείμενο από εικόνα*; Ίσως προσπαθείτε να **διαβάσετε εικόνα από απόδειξη** για παρακολούθηση εξόδων και θέλετε να ξέρετε ποιοι χαρακτήρες είναι αβέβαιοι για τη μηχανή. Τα καλά νέα; Με το Aspose.OCR μπορείτε να εξάγετε ποσοστά εμπιστοσύνης, περιοριστικά πλαίσια (bounding boxes) και απλό κείμενο από ένα JPG με λίγες μόνο γραμμές C#.

Σε αυτό το tutorial θα περάσουμε από όλα όσα χρειάζεστε: εγκατάσταση της βιβλιοθήκης, ρύθμιση της μηχανής για **εκτέλεση OCR σε JPG**, εξαγωγή βαθμών εμπιστοσύνης και ερμηνεία των **OCR bounding boxes** που δείχνουν πού βρίσκεται κάθε χαρακτήρας στη σελίδα. Στο τέλος θα έχετε μια έτοιμη εφαρμογή κονσόλας που εκτυπώνει κάθε χαρακτήρα, την εμπιστοσύνη του και τη θέση του — ιδανική για επαλήθευση αποδείξεων ή οποιουδήποτε σαρωμένου εγγράφου.

## Τι Θα Μάθετε

- Εγκατάσταση του Aspose.OCR μέσω NuGet και δημιουργία μιας βασικής μηχανής OCR.  
- Ρύθμιση του `OcrOptions` για αίτηση εξόδου απλού κειμένου **με βαθμούς εμπιστοσύνης** και **με περιοριστικά πλαίσια**.  
- Επανάληψη μέσω του `OcrResult` για **εξαγωγή κειμένου από εικόνα** γραμμή‑με‑γραμμή και σύμβολο‑με‑σύμβολο.  
- Διαχείριση κοινών προβλημάτων όπως ελλιπή αρχεία, χαρακτήρες χαμηλής εμπιστοσύνης και μορφές μη‑JPG.  
- Επέκταση του παραδείγματος για επεξεργασία πολλαπλών εικόνων αποδείξεων σε φάκελο.

Δεν απαιτείται προγενέστερη εμπειρία με το Aspose· αρκεί ένα λειτουργικό περιβάλλον .NET και μια εικόνα από απόδειξη (JPG) που θέλετε να δοκιμάσετε.

---

## Βήμα 1 – Εγκατάσταση Aspose.OCR και Προετοιμασία του Έργου

Πρώτα απ’ όλα: χρειάζεστε το πακέτο NuGet Aspose.OCR. Ανοίξτε ένα τερματικό στον φάκελο του έργου σας και εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

> **Συμβουλή:** Η δωρεάν δοκιμή λειτουργεί για έως 200 σελίδες, κάτι που είναι περισσότερο από αρκετό για δοκιμές σάρωσης αποδείξεων.

Αφού εγκατασταθεί το πακέτο, δημιουργήστε ένα νέο έργο κονσόλας (αν δεν έχετε ήδη ένα):

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
```

Τώρα μπορείτε να ανοίξετε το παραγόμενο `Program.cs` και να προσθέσετε τις οδηγίες using:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
```

Αυτοί οι χώροι ονομάτων σας δίνουν πρόσβαση στα `OcrEngine`, `OcrOptions` και στους τύπους αποτελεσμάτων που θα χρειαστούμε αργότερα.

## Βήμα 2 – Λήψη βαθμών εμπιστοσύνης OCR και OCR bounding boxes

Αυτή είναι η καρδιά του tutorial. Θα ρυθμίσουμε τη μηχανή ώστε κάθε αναγνωρισμένος χαρακτήρας να συνοδεύεται από **βαθμό εμπιστοσύνης** και **περιοριστικό πλαίσιο** (το ορθογώνιο που περικλείει το glyph). Ο τίτλος H2 περιέχει τη βασική λέξη‑κλειδί, ικανοποιώντας τον κανόνα SEO.

```csharp
// Step 2: Initialize the OCR engine and request detailed output
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process – here we assume a JPEG receipt
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Tell Aspose we want plain text, confidence percentages, and bounding boxes
ocrEngine.Options = new OcrOptions
{
    OutputFormat = OcrOutputFormat.PlainText,
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};
```

**Γιατί να συμπεριλάβετε βαθμούς εμπιστοσύνης;**  
Ένας βαθμός εμπιστοσύνης (0‑100%) σας λέει πόσο σίγουρη είναι η μηχανή για κάθε χαρακτήρα. Αν τροφοδοτείτε το αποτέλεσμα σε επόμενη λογική — π.χ. σε ροή έγκρισης εξόδων — μπορείτε αυτόματα να απορρίψετε ή να σημαδέψετε σύμβολα χαμηλής εμπιστοσύνης.

**Γιατί να ζητήσετε περιοριστικά πλαίσια;**  
Τα bounding boxes είναι απαραίτητα όταν χρειάζεται να επισημάνετε κείμενο στην αρχική εικόνα, να εξάγετε υπο‑περιοχές ή να ευθυγραμμίσετε τα αποτελέσματα OCR με μια επικάλυψη UI. Κάθε `character.Bounds` παρέχει τις συντεταγμένες X, Y, πλάτος και ύψος σε pixel.

## Βήμα 3 – Εκτέλεση OCR σε JPG και εξαγωγή κειμένου από εικόνα

Τώρα τρέχουμε τη μηχανή. Η κλήση στο `Recognize()` εκτελεί όλη τη βαριά δουλειά και επιστρέφει ένα αντικείμενο `OcrResult`.

```csharp
// Step 3: Run the OCR process
OcrResult ocrResult = ocrEngine.Recognize();
```

Αν η διαδρομή της εικόνας είναι λανθασμένη ή το αρχείο δεν είναι υποστηριζόμενη μορφή, το Aspose ρίχνει `FileNotFoundException` ή `UnsupportedImageFormatException`. Στο παραγωγικό κώδικα τυλίξτε την κλήση σε μπλοκ try/catch για να χειριστείτε αυτές τις περιπτώσεις με χάρη.

### Λήψη του απλού κειμένου

Αν χρειάζεστε μόνο το ενωμένο κείμενο, μπορείτε να διαβάσετε `ocrResult.Text`:

```csharp
Console.WriteLine("Full extracted text:");
Console.WriteLine(ocrResult.Text);
```

Αλλά επειδή ζητήσαμε και βαθμούς εμπιστοσύνης και bounding boxes, θα διασχίσουμε τη δομή για να δούμε τις λεπτομέρειες κάθε χαρακτήρα.

## Βήμα 4 – Επανάληψη μέσω γραμμών, συμβόλων και εμφάνιση βαθμών εμπιστοσύνης OCR

Ακολουθεί ο βρόχος που εκτυπώνει κάθε χαρακτήρα, την εμπιστοσύνη του και το πλαίσιο του. Εδώ το παράδειγμα **read receipt image** δείχνει την αξία του.

```csharp
// Step 4: Walk through each line and each symbol (character)
foreach (var textLine in ocrResult.Lines)
{
    foreach (var character in textLine.Symbols)
    {
        Console.WriteLine(
            $"Char: '{character.Text}'  Confidence: {character.Confidence}%  Box: {character.Bounds}");
    }
}
```

Παράδειγμα εξόδου μπορεί να είναι:

```
Char: 'R'  Confidence: 98%  Box: {X=12,Y=34,Width=15,Height=20}
Char: 'e'  Confidence: 95%  Box: {X=28,Y=34,Width=12,Height=20}
Char: 'c'  Confidence: 92%  Box: {X=41,Y=34,Width=13,Height=20}
...
```

**Ερμηνεία των αριθμών:**  
- **Εμπιστοσύνη ≥ 90%** – συνήθως ασφαλές για αποδοχή.  
- **Εμπιστοσύνη 70‑89%** – ίσως θέλετε να ελέγξετε ξανά, ειδικά για ψηφία σε ποσά.  
- **Εμπιστοσύνη < 70%** – σκεφτείτε να το σημαδέψετε για χειροκίνητη ανασκόπηση.

## Βήμα 5 – Πλήρες εκτελέσιμο παράδειγμα (με διαχείριση σφαλμάτων)

Συνδυάζοντας τα παραπάνω, εδώ είναι ένα πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε στο `Program.cs`. Περιλαμβάνει έναν απλό έλεγχο για ελλιπή αρχεία και εκτυπώνει φιλικό μήνυμα αν το OCR αποτύχει.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the receipt image – adjust to your environment
            const string imagePath = "YOUR_DIRECTORY/receipt.jpg";

            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found -> {imagePath}");
                return;
            }

            try
            {
                // Initialize engine
                OcrEngine ocrEngine = new OcrEngine
                {
                    Image = ImageStream.FromFile(imagePath),
                    Options = new OcrOptions
                    {
                        OutputFormat = OcrOutputFormat.PlainText,
                        IncludeConfidence = true,
                        IncludeBoundingBoxes = true
                    }
                };

                // Perform OCR
                OcrResult ocrResult = ocrEngine.Recognize();

                // Show full plain text (optional)
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
                Console.WriteLine();

                // Show each character with confidence and bounding box
                Console.WriteLine("=== Detailed Character Data ===");
                foreach (var line in ocrResult.Lines)
                {
                    foreach (var symbol in line.Symbols)
                    {
                        Console.WriteLine(
                            $"Char: '{symbol.Text}'  Confidence: {symbol.Confidence}%  Box: {symbol.Bounds}");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

### Αναμενόμενη έξοδος

Όταν τρέξετε `dotnet run`, η κονσόλα θα εμφανίσει πρώτα το ενωμένο κείμενο της απόδειξης, έπειτα μια λίστα με κάθε χαρακτήρα, τον βαθμό εμπιστοσύνης του και το bounding box. Αν η εμπιστοσύνη ενός χαρακτήρα είναι χαμηλή, θα δείτε ποσοστό κάτω από 80, που αποτελεί ένδειξη για χειροκίνητη επαλήθευση του τμήματος της απόδειξης.

## Bonus: Επεξεργασία Πολλαπλών Αποδείξεων σε Φάκελο

Αν έχετε μια δέσμη εικόνων αποδείξεων JPG, τυλίξτε τη λογική σε βρόχο `foreach (var file in Directory.GetFiles(folder, "*.jpg"))`. Θυμηθείτε να επαναρυθμίσετε το `OcrEngine` για κάθε αρχείο ή να δημιουργήσετε νέο αντικείμενο μέσα στον βρόχο ώστε να αποφύγετε διαρροή κατάστασης.

```csharp
string folder = "YOUR_DIRECTORY/Receipts";
foreach (var file in System.IO.Directory.GetFiles(folder, "*.jpg"))
{
    // reuse the same code block, just replace imagePath with 'file'
}
```

Η επεξεργασία μαζικά είναι χρήσιμη για νυχτερινές εισαγωγές εξόδων.

---

## Συμπέρασμα

Τώρα έχετε μια ολοκληρωμένη λύση για την απόκτηση **βαθμών εμπιστοσύνης OCR** σε C#, **εξαγωγή κειμένου από εικόνα**, και ανάκτηση **OCR bounding boxes** ενώ **εκτελείτε OCR σε JPG** αρχεία όπως μια **read receipt image**. Ο κώδικας είναι πλήρως αυτόνομος, λειτουργεί με την πιο πρόσφατη έκδοση του Aspose.OCR (ως 31‑05‑2026) και σας παρέχει τα λεπτομερή δεδομένα που χρειάζεστε για αξιόπιστες γραμμές επεξεργασίας εγγράφων.

Τι ακολουθεί; Δοκιμάστε να οπτικοποιήσετε τα bounding boxes στην αρχική απόδειξη χρησιμοποιώντας `System.Drawing` ή μια βιβλιοθήκη UI, ή να στείλετε χαρακτήρες χαμηλής εμπιστοσύνης σε δευτερεύουσα υπηρεσία επαλήθευσης. Μπορείτε επίσης να πειραματιστείτε με διαφορετικές γλώσσες ορίζοντας `ocrEngine.Options.Language = OcrLanguage.French;` – το API υποστηρίζει πολλές τοπικές ρυθμίσεις.

Καλή προγραμματιστική δουλειά, και οι βαθμοί εμπιστοσύνης σας να παραμένουν πάντα υψηλοί! 

![Console output showing OCR confidence scores and bounding boxes for a receipt


## Τι Θα Μάθετε Στη Σειρά Επόμενη;

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Get OCR Character Choices for Recognized Characters in Image Recognition](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}