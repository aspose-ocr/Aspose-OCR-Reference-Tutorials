---
category: general
date: 2026-01-09
description: c# οδηγός OCR για ανάγνωση κειμένου από PNG, μετατροπή εικόνας σε κείμενο
  και αναγνώριση κειμένου στα Χίντι σε απόδειξη χρησιμοποιώντας το Aspose OCR.
draft: false
keywords:
- c# ocr tutorial
- read text from png
- convert image to text
- recognize hindi text
- extract text from receipt
language: el
og_description: c# OCR tutorial που σας διδάσκει πώς να διαβάζετε κείμενο από PNG,
  να μετατρέπετε την εικόνα σε κείμενο και να αναγνωρίζετε κείμενο στα Χίντι σε απόδειξη
  με το Aspose OCR.
og_title: c# OCR tutorial – Εξαγωγή κειμένου Χίντι από αποδείξεις PNG
tags:
- OCR
- C#
- Aspose
- Image Processing
title: c# OCR οδηγός – Εξαγωγή κειμένου στα Χίντι από αποδείξεις PNG
url: /el/net/text-recognition/c-ocr-tutorial-extract-hindi-text-from-png-receipts/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Εξαγωγή κειμένου Hindi από αποδείξεις PNG

Έχετε ποτέ αναρωτηθεί πώς να **διαβάσετε κείμενο από PNG** αρχεία σε μια εφαρμογή C#; Ίσως έχετε μια σειρά από αποδείξεις Hindi και χρειάζεται να εξάγετε τα ποσά αυτόματα. Αυτό ακριβώς αντιμετωπίζει αυτό το c# ocr tutorial—μετατρέποντας μια εικόνα σε αναζητήσιμο κείμενο με λίγες μόνο γραμμές κώδικα.

Σε αυτόν τον οδηγό θα περάσουμε από την εγκατάσταση του Aspose OCR, τη φόρτωση μιας απόδειξης PNG, την αναγνώριση χαρακτήρων Hindi, και τελικά την εκτύπωση της εξαγόμενης συμβολοσειράς στην κονσόλα. Στο τέλος θα μπορείτε να **μετατρέψετε εικόνα σε κείμενο**, **αναγνωρίσετε κείμενο Hindi**, και ακόμη **εξάγετε κείμενο από εικόνες αποδείξεων** χωρίς να αφήσετε το IDE σας.

> **Σημείωση προαπαιτούμενου:** Χρειάζεστε μια έγκυρη άδεια Aspose OCR (ή μπορείτε να χρησιμοποιήσετε τη δωρεάν δοκιμή) και .NET 6+ εγκατεστημένο. Αν είστε νέοι στο NuGet, μην ανησυχείτε—θα καλύψουμε και αυτό.

## Τι Θα Χρειαστείτε

- **Visual Studio 2022** (ή οποιονδήποτε επεξεργαστή συμβατό με C#)
- **.NET 6 SDK** (ή νεότερο)
- **Aspose.OCR** πακέτο NuGet  
  ```bash
  dotnet add package Aspose.OCR
  ```
- Ένα δείγμα εικόνας απόδειξης, π.χ., `hindi-receipt.png`, αποθηκευμένο στον φάκελο του έργου σας.

Αν έχετε αυτά έτοιμα, μπορείτε να αντιγράψετε‑επικολλήσετε τον τελικό κώδικα και να πατήσετε **F5** αμέσως.

## Βήμα 1: Ρύθμιση του Έργου και Εισαγωγή Namespaces

Πρώτα, δημιουργήστε ένα έργο console αν δεν έχετε ήδη ένα:

```bash
dotnet new console -n HindiReceiptOcr
cd HindiReceiptOcr
dotnet add package Aspose.OCR
```

Τώρα ανοίξτε το `Program.cs`. Στην κορυφή, εισάγετε τα namespaces του Aspose OCR ώστε ο μεταγλωττιστής να ξέρει πού βρίσκονται οι κλάσεις:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;
```

> **Γιατί είναι σημαντικό:** Το `OcrEngine` βρίσκεται στο `Aspose.OCR`, ενώ τα enums σχετιζόμενα με τη γλώσσα είναι στο `Aspose.OCR.Settings`. Η παράλειψη οποιουδήποτε θα προκαλέσει σφάλμα κατά τη μεταγλώττιση.

## Βήμα 2: Αρχικοποίηση του OCR Engine και Επιλογή του Μοντέλου Γλώσσας

Το OCR engine πρέπει να γνωρίζει **ποια γλώσσα** θα αναζητήσει. Η Aspose παρέχει πολλά πακέτα γλωσσών· η καθορισμός του `OcrLanguage.Hindi` λέει στο engine να κατεβάσει (αν λείπει) και να χρησιμοποιήσει το μοντέλο Hindi.

```csharp
// Step 2: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    // The library will auto‑download the model the first time it runs.
    Language = OcrLanguage.Hindi
};
```

> **Συμβουλή επαγγελματία:** Αν σκοπεύετε να επεξεργάζεστε αποδείξεις σε πολλές γλώσσες, μπορείτε να αλλάξετε το `Language` κατά την εκτέλεση ή ακόμη και να ενεργοποιήσετε τη λειτουργία `MultiLanguage`.

## Βήμα 3: Παροχή της Απόδειξης PNG στο Engine

Εδώ είναι που **διαβάζουμε κείμενο από PNG**. Παρέχετε τη πλήρη διαδρομή (η σχετική προς το εκτελέσιμο λειτουργεί καλά). Η μέθοδος επιστρέφει μια απλή συμβολοσειρά που περιέχει ό,τι κατάφερε να αποκρυπτογραφήσει το engine.

```csharp
// Step 3: Perform OCR on the target image file
string imagePath = @"hindi-receipt.png";   // adjust if your file lives elsewhere
string recognizedText = ocrEngine.RecognizeImage(imagePath);
```

Αν η εικόνα είναι υψηλής ανάλυσης και το κείμενο είναι καθαρό, θα έχετε σχεδόν τέλεια αποτελέσματα. Για θορυβώδεις σαρώσεις, σκεφτείτε προεπεξεργασία (π.χ., δυαδικοποίηση) – η Aspose προσφέρει μεθόδους `PreprocessImage` που μπορείτε να εξερευνήσετε αργότερα.

## Βήμα 4: Εμφάνιση ή Αποθήκευση του Εξαγόμενου Κειμένου

Οι περισσότεροι προγραμματιστές απλώς εκτυπώνουν το αποτέλεσμα στην κονσόλα κατά τη δοκιμή. Σε παραγωγικό σενάριο μπορεί να γράψετε σε βάση δεδομένων ή αρχείο CSV.

```csharp
// Step 4: Show the OCR result
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(recognizedText);
```

Η εκτέλεση του προγράμματος με το δείγμα απόδειξης εκτυπώνει κάτι όπως:

```
=== OCR Output ===
दिनांक: 09/01/2026
बिल no: 12345
रक्कम: ₹ 1,250.00
धन्यवाद!
```

Αυτό είναι το τμήμα **μετατροπής εικόνας σε κείμενο** σε δράση—χωρίς ανάγκη χειροκίνητης μεταγραφής.

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω είναι το πλήρες, αυτόνομο πρόγραμμα. Επικολλήστε το στο `Program.cs`, τοποθετήστε το `hindi-receipt.png` δίπλα στο μεταγλωττισμένο `.exe`, και πατήστε **Ctrl + F5**.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace HindiReceiptOcr
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine with Hindi language
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.Hindi
            };

            // 2️⃣ Path to the PNG receipt (adjust if needed)
            string imagePath = @"hindi-receipt.png";

            // 3️⃣ Run OCR – this will download the Hindi model on first run
            string recognizedText = ocrEngine.RecognizeImage(imagePath);

            // 4️⃣ Output the result – you can also write to a file or DB
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

### Αναμενόμενη Έξοδος

Όταν η εικόνα της απόδειξης περιέχει καθαρούς χαρακτήρες Hindi, η κονσόλα θα εμφανίσει τις εξαγόμενες γραμμές, διατηρώντας τις αλλαγές γραμμής. Αν το OCR δεν αναγνωρίσει μια λέξη, θα δείτε ένα ακατάστατο τμήμα—ένα σήμα να βελτιώσετε την ποιότητα της εικόνας ή να προσαρμόσετε την προεπεξεργασία.

## Βήμα 5: Πέρα από το Βασικό – Εξαγωγή Κειμένου από Απόδειξη Προγραμματιστικά

Αν ο στόχος σας είναι να **εξάγετε κείμενο από πεδία απόδειξης** (ημερομηνία, σύνολο, αριθμός τιμολογίου), μπορείτε να επεξεργαστείτε το OCR string με κανονικές εκφράσεις:

```csharp
using System.Text.RegularExpressions;

// Example: pull the amount (₹) from the OCR result
var amountMatch = Regex.Match(recognizedText, @"रक्कम:\s*₹\s*([\d,]+\.\d{2})");
if (amountMatch.Success)
{
    Console.WriteLine($"Detected amount: {amountMatch.Groups[1].Value}");
}
```

## Συνηθισμένα Προβλήματα & Πώς να τα Αποφύγετε

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|------------------|-----------|
| **Κενή έξοδος** | Λάθος διαδρομή εικόνας ή το αρχείο δεν αντιγράφηκε στο φάκελο εξόδου. | Χρησιμοποιήστε `Path.GetFullPath` και επαληθεύστε ότι το αρχείο υπάρχει (`File.Exists`). |
| **Ακατάστατοι χαρακτήρες** | PNG χαμηλής ανάλυσης ή συμπιεσμένα χρώματα. | Αυξήστε την ανάλυση της εικόνας, ορίστε DPI σε 300+, ή χρησιμοποιήστε `ocrEngine.ImagePreprocessor`. |
| **Το μοντέλο γλώσσας δεν έχει ληφθεί** | Δεν υπάρχει σύνδεση στο internet κατά την πρώτη εκτέλεση. | Κατεβάστε εκ των προτέρων το μοντέλο Hindi μέσω του portal της Aspose ή φιλοξενήστε το τοπικά. |
| **Καθυστέρηση απόδοσης** | Επεξεργασία πολλών σελίδων σε βρόχο χωρίς απελευθέρωση πόρων. | Τοποθετήστε το `OcrEngine` μέσα σε μπλοκ `using` ή επαναχρησιμοποιήστε μια μόνο παρουσία. |

## Εικονογράφηση

![c# ocr tutorial reading Hindi text from PNG receipt](https://example.com/placeholder-image.png "c# ocr tutorial – read text from png receipt")

*Το στιγμιότυπο δείχνει μια απόδειξη Hindi πριν και μετά τη μετατροπή OCR.*

## Ανακεφαλαίωση: Τι Καλύψαμε

- Ρύθμιση μιας εφαρμογής console C# και προσθήκη του πακέτου NuGet Aspose OCR.  
- Αρχικοποίηση του `OcrEngine` με το μοντέλο γλώσσας **recognize hindi text**.  
- **Διαβάστε κείμενο από PNG** χρησιμοποιώντας το `RecognizeImage`.  
- **Μετατρέψτε εικόνα σε κείμενο** και εκτυπώσατε το αποτέλεσμα.  
- Επιδειχθεί ένα απλό μοτίβο για **εξαγωγή κειμένου από πεδία απόδειξης**.  

Όλα αυτά παρασχέθηκαν σε ένα ενιαίο, εκτελέσιμο αρχείο—ακριβώς αυτό που πρέπει να παρέχει ένα **c# ocr tutorial**.

## Επόμενα Βήματα & Σχετικά Θέματα

1. **Batch processing** – επανάληψη μέσω φακέλου εικόνων αποδείξεων και αποθήκευση των αποτελεσμάτων σε CSV.  
2. **Pre‑processing** – εξερευνήστε το `ocrEngine.ImagePreprocessor` για αφαίρεση θορύβου, διόρθωση κλίσης ή βελτίωση αντίθεσης.  
3. **Multi‑language OCR** – ενεργοποιήστε το `OcrLanguage.Multilingual` για διαχείριση αποδείξεων που συνδυάζουν Hindi και English.  
4. **Integration** – μεταφέρετε τα εξαγόμενα δεδομένα σε μοντέλο Entity Framework Core για μόνιμη αποθήκευση.  

Αν σας ενδιαφέρει κάποιο από αυτά, δείτε τα tutorials μας για **convert image to text in C#** και **extract structured data from OCR results**.

### Καλό Κώδικα!

Μη διστάσετε να αφήσετε ένα σχόλιο αν αντιμετωπίσετε προβλήματα, ή να μοιραστείτε πώς έχετε επεκτείνει αυτό το **c# ocr tutorial** στα δικά σας έργα. Θυμηθείτε, το OCR είναι μόνο το πρώτο βήμα—τα καθαρά δεδομένα είναι όπου συμβαίνει η πραγματική μαγεία. 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}