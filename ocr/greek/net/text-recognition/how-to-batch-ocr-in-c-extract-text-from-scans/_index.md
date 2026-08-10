---
category: general
date: 2026-05-06
description: Μάθετε πώς να εκτελείτε μαζική OCR σε C# και να εξάγετε κείμενο από σαρώσεις
  γρήγορα χρησιμοποιώντας το Aspose OCR Batch. Ακολουθήστε έναν πλήρη οδηγό βήμα‑προς‑βήμα
  με κώδικα, συμβουλές και διαχείριση ειδικών περιπτώσεων.
draft: false
keywords:
- how to batch OCR
- extract text from scans
- Aspose OCR batch processing
- C# OCR automation
- GPU accelerated OCR
language: el
og_description: Πώς να κάνετε ομαδική OCR σε C#; Αυτός ο οδηγός σας δείχνει πώς να
  εξάγετε κείμενο από σαρώσεις αποδοτικά με το Aspose OCR, υποστήριξη GPU και παράλληλη
  επεξεργασία.
og_title: Πώς να κάνετε μαζική OCR σε C# – Εξαγωγή κειμένου από σκαναρίσματα
tags:
- C#
- OCR
- Aspose
title: Πώς να κάνετε ομαδική OCR σε C# – Εξαγωγή κειμένου από σαρώσεις
url: /el/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-scans/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να κάνετε Batch OCR σε C# – Εξαγωγή κειμένου από σαρώσεις

Έχετε αναρωτηθεί ποτέ **πώς να κάνετε batch OCR** όταν έχετε έναν φάκελο γεμάτο σαρωμένα PDF ή JPEG; Δεν είστε ο μόνος που κοιτάζει ένα βουνό εικόνων και σκέφτεται, “Πρέπει να υπάρχει ένας πιο γρήγορος τρόπος να εξάγετε το κείμενο”. Σε αυτό το tutorial θα περάσουμε από μια πρακτική λύση που όχι μόνο σας επιτρέπει να **εξάγετε κείμενο από σαρώσεις**, αλλά επίσης επιταχύνει τη διαδικασία με επιτάχυνση GPU και παράλληλη εκτέλεση.

Το θέμα είναι: η εκτέλεση OCR ένα αρχείο τη φορά είναι ένας τεράστιος καταναλωτής χρόνου, ειδικά αν έχετε δεκάδες ή εκατοντάδες σελίδες. Στο τέλος αυτού του οδηγού θα έχετε μια έτοιμη προς εκτέλεση εφαρμογή C# console που επεξεργάζεται ολόκληρο τον φάκελο με μια μόνο εντολή, παρέχοντάς σας καθαρά αρχεία κειμένου έτοιμα για ευρετηρίαση, αναζήτηση ή ό,τι ακολουθεί.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

- **.NET 6.0 ή νεότερο** (ο κώδικας χρησιμοποιεί σύγχρονα χαρακτηριστικά C#).
- **Άδεια για Aspose.OCR** (η δωρεάν δοκιμή λειτουργεί για δοκιμές).
- Μηχάνημα συμβατό με GPU **αν θέλετε να ενεργοποιήσετε `UseGpu`**· διαφορετικά η βιβλιοθήκη θα επιστρέψει στην CPU.
- Βασική εξοικείωση με **εφαρμογές console C#**.

Καμία εξωτερική υπηρεσία, κανένα κρυφό αρχείο ρυθμίσεων — μόνο το SDK και ένας φάκελος εικόνων.

## Βήμα 1: Εγκατάσταση του πακέτου NuGet Aspose.OCR

Πρώτα, προσθέστε τη βιβλιοθήκη Aspose OCR στο έργο σας. Ανοίξτε ένα τερματικό στο φάκελο της λύσης και εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

Αυτό θα κατεβάσει το `Aspose.OCR` και το namespace batch, που θα χρησιμοποιήσουμε για **batch OCR** αργότερα.

> **Pro tip:** Αν χρησιμοποιείτε Visual Studio, μπορείτε επίσης να προσθέσετε το πακέτο μέσω του UI του NuGet Package Manager.

## Βήμα 2: Δημιουργία του σκελετού της εφαρμογής Console

Ας δημιουργήσουμε μια ελάχιστη εφαρμογή console που θα φιλοξενήσει τον batch επεξεργαστή μας. Δημιουργήστε ένα νέο αρχείο με όνομα `Program.cs` και επικολλήστε το παρακάτω σκελετό:

```csharp
using System;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll configure and run the OCR batch processor here.
        }
    }
}
```

Γιατί να τοποθετήσουμε τη λογική μέσα στο `Main`; Επειδή μια εφαρμογή console μας δίνει άμεση ανάδραση μέσω `Console.WriteLine`, ιδανική για γρήγορη επαλήθευση ότι η εργασία **batch OCR** ολοκληρώθηκε.

## Βήμα 3: Διαμόρφωση του OcrBatchProcessor

Τώρα το κεντρικό μέρος της λύσης. Θα δημιουργήσουμε ένα `OcrBatchProcessor`, θα το κατευθύνουμε στον φάκελο εισόδου, θα ορίσουμε πού θα αποθηκεύονται τα αποτελέσματα και θα ρυθμίσουμε μερικές παραμέτρους απόδοσης.

```csharp
// Step 3: Configure the OCR batch processor
var batch = new OcrBatchProcessor
{
    // Folder that contains the source images to be processed
    InputFolder = @"YOUR_DIRECTORY/Scans",

    // Folder where the OCR results will be saved
    OutputFolder = @"YOUR_DIRECTORY/OcrResults",

    // Specify the language of the documents (Spanish in this example)
    Language = OcrLanguage.Spanish,

    // Enable GPU acceleration for faster processing (if available)
    UseGpu = true,

    // Limit the number of concurrent OCR operations
    MaxDegreeOfParallelism = 4
};
```

### Γιατί είναι σημαντικές αυτές οι ρυθμίσεις

| Setting | Τι κάνει | Πότε μπορεί να το αλλάξετε |
|---------|----------|----------------------------|
| `InputFolder` | Διαδρομή προς τις σαρώσεις που θέλετε να επεξεργαστείτε. | Χρησιμοποιήστε σχετική διαδρομή για φορητότητα. |
| `OutputFolder` | Πού θα αποθηκευτεί το εξαγόμενο κείμενο κάθε εικόνας ως αρχείο `.txt`. | Κατευθύνετε σε κοινόχρηστο δίκτυο αν χρειάζεστε κεντρική αποθήκευση. |
| `Language` | Μοντέλο γλώσσας OCR· επιλέξαμε Ισπανικά για να δείξουμε πολυγλωσσική υποστήριξη. | Αλλάξτε σε `OcrLanguage.English` ή οποιαδήποτε υποστηριζόμενη γλώσσα. |
| `UseGpu` | Μεταφέρει βαριές υπολογιστικές πράξεις στην GPU. | Ορίστε `false` σε διακομιστές χωρίς GPU. |
| `MaxDegreeOfParallelism` | Ελέγχει πόσες εικόνες επεξεργάζονται ταυτόχρονα. | Μειώστε σε μηχανή με χαμηλή CPU για να αποφύγετε υπερφόρτωση. |

## Βήμα 4: Εκτέλεση της Batch λειτουργίας με διαχείριση σφαλμάτων

Η εκτέλεση του batch είναι τόσο απλή όσο η κλήση του `Execute()`, αλλά θα το τυλίξουμε σε μπλοκ try‑catch ώστε να λαμβάνετε ένα φιλικό μήνυμα αν κάτι πάει στραβά (π.χ. λείπει φάκελος, μη υποστηριζόμενη μορφή εικόνας).

```csharp
try
{
    // Step 4: Run the batch OCR operation
    batch.Execute();

    // Step 5: Inform the user that processing has finished
    Console.WriteLine("Batch completed.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during batch OCR: {ex.Message}");
}
```

Όταν ο επεξεργαστής ολοκληρωθεί, θα δείτε **Batch completed.** στην κονσόλα, και κάθε αρχική εικόνα θα έχει ένα αντίστοιχο αρχείο `.txt` στο `OcrResults`. Τα ονόματα αρχείων αντικατοπτρίζουν τα αρχικά, κάνοντας εύκολο το αντιστοίχισμα στην αρχική σάρωση.

## Βήμα 5: Επαλήθευση του αποτελέσματος – Τι να περιμένετε

Μετά την εκτέλεση του προγράμματος, ανοίξτε οποιοδήποτε αρχείο μέσα στο `YOUR_DIRECTORY/OcrResults`. Θα πρέπει να δείτε απλό κείμενο που εξήχθη από την αντίστοιχη εικόνα, για παράδειγμα:

```
Este es un documento de prueba.
Contiene varias líneas de texto.
```

Αν το αποτέλεσμα φαίνεται παραμορφωμένο, ελέγξτε ξανά ότι το `Language` ταιριάζει με τη γλώσσα των σαρώσεών σας. Το Aspose OCR υποστηρίζει πάνω από 100 γλώσσες, οπότε μπορείτε να αντικαταστήσετε το `OcrLanguage.Spanish` με όποια χρειάζεστε.

## Διαχείριση Ακραίων Περιπτώσεων και Συνηθισμένων Παγίδων

### 1. GPU Μη Διαθέσιμο

Αν το μηχάνημά σας δεν διαθέτει συμβατή GPU, το `UseGpu = true` θα επιστρέψει σιωπηλά σε λειτουργία CPU, αλλά θα χάσετε την επιτάχυνση. Για να είστε σαφείς, μπορείτε να εντοπίσετε την ικανότητα GPU:

```csharp
if (!OcrBatchProcessor.IsGpuSupported)
{
    batch.UseGpu = false;
    Console.WriteLine("GPU not detected – falling back to CPU processing.");
}
```

### 2. Μεγάλα Αρχεία που Υπερβαίνουν τη Μνήμη

Όταν δουλεύετε με τεράστιες TIFF ή PDF, σκεφτείτε να τις χωρίσετε σε μικρότερες εικόνες εκ των προτέρων. Το Aspose OCR μπορεί να χειριστεί πολυ‑σελίδες PDF, αλλά η κατανάλωση μνήμης αυξάνεται με τον αριθμό των σελίδων. Ένα απλό βήμα προεπεξεργασίας με `Aspose.Imaging` μπορεί να κόψει το έγγραφο σε διαχειρίσιμα κομμάτια.

### 3. Μη‑εικόνες στον Φάκελο Εισόδου

Ο batch επεξεργαστής αγνοεί αρχεία που δεν μπορεί να αναλύσει, αλλά είναι καλή πρακτική να διατηρείτε τον φάκελο καθαρό. Μπορείτε να φιλτράρετε κατά επέκταση:

```csharp
batch.InputFolder = @"YOUR_DIRECTORY/Scans";
batch.FileFilter = file => file.EndsWith(".png", StringComparison.OrdinalIgnoreCase)
                         || file.EndsWith(".jpg", StringComparison.OrdinalIgnoreCase);
```

*(Σημείωση: το `FileFilter` είναι υποθετική ιδιότητα· αντικαταστήστε το με το πραγματικό API αν υπάρχει.)*

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω είναι το πλήρες, έτοιμο για αντιγραφή‑επικόλληση πρόγραμμα. Αντικαταστήστε το `YOUR_DIRECTORY` με την απόλυτη διαδρομή στο σύστημά σας.

```csharp
using System;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Configure the batch processor
            var batch = new OcrBatchProcessor
            {
                InputFolder = @"C:\MyScans",          // <-- change this
                OutputFolder = @"C:\OcrResults",     // <-- change this
                Language = OcrLanguage.Spanish,
                UseGpu = true,
                MaxDegreeOfParallelism = 4
            };

            // Optional: fall back to CPU if no GPU is found
            if (!OcrBatchProcessor.IsGpuSupported)
            {
                batch.UseGpu = false;
                Console.WriteLine("GPU not detected – using CPU.");
            }

            try
            {
                // Run the batch job
                batch.Execute();

                Console.WriteLine("Batch completed.");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Error during batch OCR: {ex.Message}");
            }
        }
    }
}
```

### Αναμενόμενη έξοδος στην κονσόλα

```
Batch completed.
```

Και στο `C:\OcrResults` θα βρείτε ένα αρχείο `.txt` για κάθε εικόνα στο `C:\MyScans`.

## Συμπέρασμα

Τώρα έχετε έναν στιβαρό, έτοιμο για παραγωγή τρόπο **πώς να κάνετε batch OCR** σε C# και **να εξάγετε κείμενο από σαρώσεις** χωρίς να ανοίγετε κάθε αρχείο χειροκίνητα. Εκμεταλλευόμενοι το batch API της Aspose, την επιτάχυνση GPU και την παραμετροποιήσιμη παράλληλη εκτέλεση, η λύση κλιμακώνεται από μερικές σελίδες έως χιλιάδες.

Τι ακολουθεί; Δοκιμάστε τις παρακάτω ιδέες:

- **Ενσωμάτωση με ευρετήριο αναζήτησης** (π.χ., Elasticsearch) για να κάνετε το εξαγόμενο κείμενο αναζητήσιμο.
- **Προσθήκη μετα‑επεξεργασίας** όπως ορθογραφικός έλεγχος ή ανίχνευση γλώσσας.
- **Μετατροπή της εφαρμογής console σε Windows Service** για συνεχή παρακολούθηση ενός φακέλου εισόδου.

Νιώστε ελεύθεροι να πειραματιστείτε, να ρυθμίσετε το επίπεδο παράλληλης εκτέλεσης ή να αλλάξετε το μοντέλο γλώσσας. Αν αντιμετωπίσετε προβλήματα, αφήστε ένα σχόλιο παρακάτω — καλή OCR εμπειρία!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}