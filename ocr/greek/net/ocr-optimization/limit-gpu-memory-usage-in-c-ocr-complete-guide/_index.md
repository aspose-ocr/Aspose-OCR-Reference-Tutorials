---
category: general
date: 2026-05-02
description: Περιορίστε τη χρήση μνήμης GPU κατά την εκτέλεση OCR σε εικόνα με C#.
  Μάθετε πώς να ενεργοποιήσετε την επιτάχυνση GPU, να εξάγετε κείμενο από απόδειξη
  και να κατακτήσετε έναν οδηγό OCR σε C#.
draft: false
keywords:
- limit gpu memory usage
- extract text from receipt
- how to enable gpu acceleration
- run OCR on image
- c# ocr tutorial
language: el
og_description: Περιορίστε τη χρήση μνήμης GPU κατά την εκτέλεση OCR σε εικόνα με
  C#. Αυτός ο οδηγός δείχνει πώς να ενεργοποιήσετε την επιτάχυνση GPU, να εξάγετε
  κείμενο από απόδειξη και να κατακτήσετε ένα tutorial OCR σε C#.
og_title: Περιορισμός χρήσης μνήμης GPU σε C# OCR – Πλήρης Οδηγός
tags:
- Aspose OCR
- C#
- GPU acceleration
title: Περιορισμός της χρήσης μνήμης GPU σε OCR C# – Πλήρης οδηγός
url: /el/net/ocr-optimization/limit-gpu-memory-usage-in-c-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Περιορισμός χρήσης μνήμης GPU σε C# OCR – Πλήρης Οδηγός

Σας έχει συμβεί ποτέ να χρειαστείτε **να περιορίσετε τη χρήση μνήμης GPU** όταν επεξεργάζεστε μια δέσμη αποδείξεων; Δεν είστε ο μόνος—οι προγραμματιστές συχνά αντιμετωπίζουν σφάλματα έλλειψης μνήμης όταν το GPU ζητείται να διαχειριστεί πάρα πολλές εικόνες ταυτόχρονα. Τα καλά νέα είναι ότι το Aspose.OCR σας επιτρέπει να περιορίσετε το αποτύπωμα μνήμης **και** να ενεργοποιήσετε την επιτάχυνση GPU με μια μόνο γραμμή κώδικα.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα μια πρακτική λύση που δείχνει **πώς να ενεργοποιήσετε την επιτάχυνση GPU**, να εξάγετε κείμενο από ένα δείγμα εικόνας απόδειξης, και να διατηρήσετε τη χρήση RAM του GPU κάτω από ένα τακτοποιημένο 1 GB. Στο τέλος θα έχετε μια έτοιμη για εκτέλεση εφαρμογή C# console, συν ένα σύνολο συμβουλών που μπορείτε να επαναχρησιμοποιήσετε σε οποιοδήποτε σενάριο **run OCR on image**.

## Τι Θα Χρειαστείτε

- .NET 6.0 SDK ή νεότερο (ο κώδικας συντάσσεται επίσης με .NET 5+)  
- Πακέτο NuGet Aspose.OCR για .NET (`Aspose.OCR`) – εγκαταστήστε το με `dotnet add package Aspose.OCR`  
- GPU που υποστηρίζει CUDA ή συσκευή Windows συμβατή με DirectML  
- Παράδειγμα εικόνας απόδειξης (`receipt.jpg`) τοποθετημένο σε φάκελο που μπορείτε να αναφερθείτε  

Αυτό είναι όλο—χωρίς επιπλέον εγγενείς βιβλιοθήκες, χωρίς περίπλοκες αντιγραφές DLL. Το Aspose αφαιρεί την πολυπλοκότητα του backend GPU, ώστε να μπορείτε να εστιάσετε στη λογική της επιχείρησής σας.

## Βήμα 1: Εγκατάσταση του Πακέτου NuGet Aspose.OCR

Πρώτα απ' όλα. Ανοίξτε ένα τερματικό στον φάκελο του έργου σας και εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

Αυτό κατεβάζει την πιο πρόσφατη σταθερή έκδοση (από τον Μάιο 2026 είναι η 23.11). Το πακέτο περιλαμβάνει τόσο τα binaries CPU όσο και GPU, οπότε δεν χρειάζεται να κατεβάσετε χειροκίνητα τα runtime CUDA ή DirectML—το Aspose ανιχνεύει τι είναι διαθέσιμο κατά την εκτέλεση.

> **Pro tip:** Αν στοχεύετε σε pipeline CI/CD, κλειδώστε την έκδοση στο `.csproj` σας για να αποφύγετε απρόσμενες αναβαθμίσεις.

## Βήμα 2: Δημιουργία του OCR Engine και **περιορισμός χρήσης μνήμης GPU**

Τώρα θα δημιουργήσουμε ένα αντικείμενο `OcrEngine` και θα του πούμε ρητά να μην υπερβεί 1 GB μνήμης GPU. Αυτό είναι ο πυρήνας της απαίτησης **περιορισμού χρήσης μνήμης GPU**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

public class GpuExample
{
    public static void Run()
    {
        // Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // Enable GPU mode – Aspose auto‑detects CUDA or DirectML
        ocrEngine.Settings.Engine = EngineMode.Gpu;

        // 👉 Limit GPU memory usage to 1024 MB (1 GB)
        ocrEngine.Settings.GpuMemoryLimitMb = 1024;

        // Load the receipt image and run OCR
        var result = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/receipt.jpg");

        // Output the plain‑text result
        Console.WriteLine(result.Text);
    }
}
```

Παρατηρήστε το σχόλιο `// 👉 Limit GPU memory usage…`—αυτή η γραμμή είναι η απάντηση στη βασική λέξη‑κλειδί. Ορίζοντας το `GpuMemoryLimitMb` λέτε στη βασική μηχανή inference να δεσμεύσει το πολύ το καθορισμένο ποσό, επιτρέποντας σε πολλαπλές ταυτόχρονες εργασίες να συνυπάρχουν χωρίς να υπερφορτώνουν το GPU.

## Βήμα 3: **Πώς να ενεργοποιήσετε την επιτάχυνση GPU** (και γιατί έχει σημασία)

Μπορεί να αναρωτιέστε, “Γιατί να μην μείνουμε μόνο στη CPU;” Η απάντηση είναι η ταχύτητα. Σε μια σύγχρονη RTX 3080, η ίδια απόδειξη επεξεργάζεται σε κάτω από 200 ms σε αντίθεση με 1,2 δευτερόλεπτα σε CPU 4‑πυρήνων.  

Η ενεργοποίηση της επιτάχυνσης GPU είναι τόσο απλή όσο η αλλαγή του enum `EngineMode`:

```csharp
ocrEngine.Settings.Engine = EngineMode.Gpu;
```

Aspose αυτόματα επιλέγει το καλύτερο backend:

| Ανιχνευμένο Backend | Τι Κάνει |
|---------------------|----------|
| CUDA (NVIDIA)       | Χρησιμοποιεί πυρήνες cuDNN για OCR, ιδανικό για Windows/Linux με κάρτες NVIDIA |
| DirectML (Windows)  | Εκμεταλλεύεται DirectX 12, λειτουργεί σε GPU AMD/Intel χωρίς επιπλέον οδηγούς |
| None (fallback)     | Επιστρέφει στην βελτιστοποιημένη διαδρομή CPU |

Αν δεν υπάρχει ούτε CUDA ούτε DirectML, η μηχανή επιστρέφει σιωπηλά στην CPU—χωρίς κατάρρευση, μόνο πιο αργή απόδοση.

## Βήμα 4: **Run OCR on image** και **extract text from receipt**

Με τη μηχανή ρυθμισμένη, η τροφοδοσία μιας εικόνας είναι απλή. Η μέθοδος `RecognizeImage` δέχεται διαδρομή αρχείου, `Stream`, ή ακόμη και `Bitmap`. Εδώ είναι η ελάχιστη κλήση:

```csharp
var result = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/receipt.jpg");
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(result.Text);
```

Υποθέτοντας ότι η απόδειξη περιέχει:

```
Store XYZ
Date: 2026-04-30
Total: $23.45
```

Θα πρέπει να δείτε έξοδο παρόμοια με:

```
=== OCR Output ===
Store XYZ
Date: 2026-04-30
Total: $23.45
```

Αν το κείμενο φαίνεται παραμορφωμένο, ελέγξτε ότι η εικόνα έχει υψηλή αντίθεση και είναι σωστά προσανατολισμένη—το OCR αγαπά τις καθαρές σκαναρίσματα.

## Βήμα 5: Επαλήθευση Ορίων Μνήμης και Διαχείριση Ακραίων Περιπτώσεων

Μετά την πρώτη εκτέλεση, μπορείτε να ερωτήσετε πόση μνήμη GPU χρησιμοποίησε πραγματικά η μηχανή:

```csharp
Console.WriteLine($"GPU memory used: {ocrEngine.Settings.GpuMemoryUsedMb} MB");
```

Αν σκοπεύετε να επεξεργαστείτε δεκάδες αποδείξεις παράλληλα, ίσως θέλετε να μειώσετε το όριο σε 512 MB και να εκτελέσετε πολλές στιγμές του engine. Απλώς θυμηθείτε ότι κάθε στιγμιότυπο σέβεται το ίδιο παγκόσμιο όριο· η βιβλιοθήκη θα ρυθμίσει αυτόματα τις δεσμεύσεις.

> **Common pitfall:** Ορισμός του ορίου πολύ χαμηλού (π.χ., 100 MB) μπορεί να κάνει τη μηχανή να επιστρέψει στην CPU κατά τη διάρκεια εκτέλεσης, οδηγώντας σε ασυνεπή απόδοση. Δοκιμάστε με ρεαλιστικό φορτίο πριν κλειδώσετε την τιμή.

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω υπάρχει ένα πλήρες, έτοιμο για αντιγραφή πρόγραμμα console. Αντικαταστήστε το `YOUR_DIRECTORY` με την πραγματική διαδρομή προς την εικόνα της απόδειξής σας.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace AsposeOcrGpuDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step‑by‑step demo
            GpuExample.Run();

            // Keep console window open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }

    class GpuExample
    {
        public static void Run()
        {
            // 1️⃣ Create OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Enable GPU acceleration (auto‑detects CUDA or DirectML)
            ocrEngine.Settings.Engine = EngineMode.Gpu;

            // 3️⃣ Limit GPU memory usage to 1 GB for concurrent jobs
            ocrEngine.Settings.GpuMemoryLimitMb = 1024;

            // 4️⃣ Load the image and run OCR
            var recognitionResult = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/receipt.jpg");

            // 5️⃣ Output the recognized plain‑text
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognitionResult.Text);

            // 6️⃣ Optional: Show how much GPU memory was actually used
            Console.WriteLine($"\nGPU memory used: {ocrEngine.Settings.GpuMemoryUsedMb} MB");
        }
    }
}
```

Αποθηκεύστε το αρχείο, εκτελέστε `dotnet run`, και θα πρέπει να δείτε το εξαγόμενο κείμενο της απόδειξης να εμφανίζεται στην κονσόλα, μαζί με μια μικρή αναφορά της κατανάλωσης μνήμης GPU.

## Επίλυση Προβλημάτων & Συχνές Ερωτήσεις

**Ε: Η GPU μου δεν ανιχνεύεται—γιατί;**  
Α: Βεβαιωθείτε ότι έχετε εγκαταστήσει τον πιο πρόσφατο οδηγό NVIDIA (για CUDA) ή Windows 10 1809+ (για DirectML). Επίσης ελέγξτε ότι τα DLL `Aspose.OCR` ταιριάζουν με την αρχιτεκτονική της διεργασίας σας (συνιστάται x64).

**Ε: Η έξοδος είναι κενή.**  
Α: Ελέγξτε την ποιότητα της εικόνας—θολές ή περιστρεφόμενες αποδείξεις συχνά χρειάζονται προεπεξεργασία (απλοποίηση κλίσης, δυαδικοποίηση). Το Aspose παρέχει `ImagePreprocessor` που μπορείτε να ενσωματώσετε πριν το `RecognizeImage`.

**Ε: Μπορώ να το τρέξω σε Linux;**  
Α: Ναι, εφόσον έχετε μια GPU NVIDIA με εγκατεστημένο CUDA 11+. Ο ίδιος κώδικας λειτουργεί αμετάβλητος.

## Συμπέρασμα

Συζητήσαμε όλα όσα χρειάζεστε για **να περιορίσετε τη χρήση μνήμης GPU** ενώ **τρέχετε OCR σε εικόνα** χρησιμοποιώντας το Aspose.OCR σε C#. Από την εγκατάσταση του πακέτου NuGet μέχρι τη διαμόρφωση του engine, την ενεργοποίηση της επιτάχυνσης GPU, και τελικά **την εξαγωγή κειμένου από απόδειξη**, ο οδηγός σας παρέχει μια έτοιμη λύση που είναι φιλική στη μνήμη και εξαιρετικά γρήγορη.

Στη συνέχεια, μπορείτε να εξερευνήσετε πιο προχωρημένα θέματα **c# OCR tutorial**—όπως επεξεργασία σε δέσμες, προσαρμοσμένα πακέτα γλωσσών, ή ενσωμάτωση των αποτελεσμάτων σε βάση δεδομένων. Πειραματιστείτε με διαφορετικές τιμές `GpuMemoryLimitMb` για να βρείτε το ιδανικό σημείο για το φορτίο εργασίας σας, και παρακολουθείτε τη διάγνωση χρήσης μνήμης για να αποφύγετε εκπλήξεις.

Καλή προγραμματιστική, και εύχομαι η GPU σας να παραμένει ψυχρή ενώ το OCR σας παραμένει ακονισμένο!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}