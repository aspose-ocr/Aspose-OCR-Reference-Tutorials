---
category: general
date: 2026-02-14
description: Πώς να χρησιμοποιήσετε OCR σε C# για γρήγορη εξαγωγή κειμένου από αρχεία
  PNG. Μάθετε ομαδική επεξεργασία εικόνων OCR, επεξεργασία πολλαπλών εικόνων και χρήση
  του Aspose OCR C# σε έναν ενιαίο οδηγό.
draft: false
keywords:
- how to use OCR
- extract text png
- batch OCR images
- process multiple images
- aspose OCR c#
language: el
og_description: Πώς να χρησιμοποιήσετε OCR σε C# με το Aspose OCR C#. Αυτό το εκπαιδευτικό
  δείχνει πώς να εξάγετε κείμενο από αρχεία PNG, να κάνετε ομαδική επεξεργασία OCR
  εικόνων και να επεξεργάζεστε πολλαπλές εικόνες αποδοτικά.
og_title: Πώς να χρησιμοποιήσετε OCR σε C# – Μαζική εξαγωγή κειμένου από PNG
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Πώς να χρησιμοποιήσετε OCR σε C# – Μαζική επεξεργασία εικόνων PNG με το Aspose
  OCR
url: /el/net/text-recognition/how-to-use-ocr-in-c-batch-process-png-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε OCR σε C# – Μαζική Επεξεργασία PNG Εικόνων με Aspose OCR

Αναρωτηθήκατε ποτέ **πώς να χρησιμοποιήσετε OCR** για να εξάγετε κείμενο από μια σειρά αρχείων PNG χωρίς να γράψετε ξεχωριστή ρουτίνα για το καθένα; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν δυσκολίες όταν πρέπει να **εξάγουν κείμενο PNG** σε μεγάλη κλίμακα, ειδικά όταν οι εικόνες βρίσκονται σε έναν φάκελο και πρέπει να ενεργοποιήσετε τη μηχανή OCR για κάθε αρχείο.  

Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα από μια πλήρη, έτοιμη προς εκτέλεση λύση που **μαζικά OCR εικόνες**, **επεξεργάζεται πολλαπλές εικόνες** παράλληλα και αξιοποιεί τη δυναμική βιβλιοθήκη **Aspose OCR C#**. Στο τέλος θα έχετε ένα εκτελέσιμο αρχείο που διαβάζει όποιο αριθμό PNG, εξάγει το κείμενό τους και εμφανίζει τα αποτελέσματα στην κονσόλα—όλα με λίγες μόνο γραμμές κώδικα.

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Core και .NET Framework)  
- Ένα έγκυρο license του Aspose.OCR for .NET (ή η δωρεάν δοκιμαστική έκδοση) – μπορείτε να το αποκτήσετε από την ιστοσελίδα της Aspose.  
- Ένας φάκελος που περιέχει τα PNG αρχεία που θέλετε να διαβάσετε.  
- Visual Studio 2022 (ή οποιοδήποτε IDE συμβατό με C#).  

Δεν απαιτούνται επιπλέον πακέτα NuGet εκτός από `Aspose.OCR`.

## Βήμα 1: Πώς να Χρησιμοποιήσετε OCR – Αρχικοποίηση της Μηχανής Aspose OCR

Το πρώτο που χρειάζεστε είναι μια παρουσία της κλάσης `Engine`. Αυτό το αντικείμενο αφαιρεί την πολυπλοκότητα της υποκείμενης τεχνολογίας OCR και μπορεί να τρέξει σε CPU ή GPU, ανάλογα με το υλικό και το license σας.

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

// Create an OCR engine (CPU by default; GPU can be enabled via EngineSettings if licensed)
var ocrEngine = new Engine();
```

*Γιατί είναι σημαντικό:* Η αρχικοποίηση της μηχανής μία φορά και η επαναχρησιμοποίησή της σε πολλαπλά νήματα εξοικονομεί μνήμη και αποφεύγει το κόστος φόρτωσης των μοντέλων OCR επανειλημμένα. Επίσης εξασφαλίζει συνεπείς ρυθμίσεις για όλες τις εικόνες.

## Βήμα 2: Εξαγωγή Κειμένου PNG – Συλλογή Διαδρομών Αρχείων

Στη συνέχεια, χρειαζόμαστε μια συλλογή διαδρομών αρχείων. Σε ένα πραγματικό έργο μπορεί να διαβάζετε τον φάκελο δυναμικά, αλλά για σαφήνεια θα παραθέσουμε μερικά δείγματα αρχείων.

```csharp
// List the PNG files you want to process
var imagePaths = new List<string>
{
    "YOUR_DIRECTORY/img1.png",
    "YOUR_DIRECTORY/img2.png",
    "YOUR_DIRECTORY/img3.png"
};
```

*Συμβουλή:* Αντικαταστήστε το `YOUR_DIRECTORY` με την απόλυτη ή σχετική διαδρομή προς τις εικόνες σας. Αν έχετε δεκάδες αρχεία, μπορείτε να αντικαταστήσετε τη χειροκίνητη λίστα με `Directory.GetFiles("YOUR_DIRECTORY", "*.png")`.

## Βήμα 3: Μαζική OCR Εικόνων – Εκτέλεση Αναγνώρισης Παράλληλα

Η επεξεργασία των εικόνων μία προς μία είναι απλή αλλά αργή. Χρησιμοποιώντας το `Parallel.ForEach` μπορούμε να **επεξεργαστούμε πολλαπλές εικόνες** ταυτόχρονα, εκμεταλλευόμενοι τους πολυπύρηνους επεξεργαστές.

```csharp
// Helper method that performs the parallel recognition
static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
{
    var resultsBag = new ConcurrentBag<OcrResult>();

    Parallel.ForEach(paths, path =>
    {
        // Load the image stream (Aspose handles various formats)
        var image = ImageStream.FromFile(path);
        // Perform OCR
        OcrResult result = engine.Recognize(image);
        // Store the result safely for later use
        resultsBag.Add(result);
    });

    return resultsBag.ToArray();
}

// Execute the parallel OCR
var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);
```

*Γιατί παράλληλα;* Κάθε κλήση OCR είναι απαιτητική για την CPU αλλά ανεξάρτητη, οπότε η ταυτόχρονη εκτέλεση μπορεί να μειώσει δραστικά το συνολικό χρόνο, ειδικά σε μηχανή με 4 πυρήνες ή περισσότερο.

## Βήμα 4: Επεξεργασία Πολλαπλών Εικόνων – Εμφάνιση του Εξαγόμενου Κειμένου

Τώρα που έχουμε μια συλλογή αντικειμένων `OcrResult`, μπορούμε να τα διατρέξουμε και να εκτυπώσουμε το αναγνωρισμένο κείμενο. Εδώ θα αποθηκεύατε κανονικά το αποτέλεσμα σε βάση δεδομένων ή σε αρχεία, αλλά η έξοδος στην κονσόλα κρατά το παράδειγμα σύντομο.

```csharp
int index = 1;
foreach (var result in ocrResults)
{
    Console.WriteLine($"--- Image {index++} ---");
    Console.WriteLine(result.Text);
}
```

**Αναμενόμενη έξοδος στην κονσόλα (δείγμα):**

```
--- Image 1 ---
Hello world! This is the first image.
--- Image 2 ---
Invoice #12345
Total: $250.00
--- Image 3 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
```

Αν κάποια εικόνα αποτύχει να φορτωθεί, το Aspose ρίχνει εξαίρεση· μπορείτε να τυλίξετε την κλήση `engine.Recognize` σε μπλοκ try/catch για να καταγράψετε τα σφάλματα χωρίς να διακόψετε ολόκληρη τη δέσμη.

## Βήμα 5: Πλήρες Παράδειγμα – Όλα τα Τμήματα Μαζί

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα νέο C# console project. Περιλαμβάνει όλα τα `using` statements μέχρι τον τελικό βρόχο εξόδου.

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new Engine();

        // Step 2: Define the PNG files to process
        var imagePaths = new List<string>
        {
            "YOUR_DIRECTORY/img1.png",
            "YOUR_DIRECTORY/img2.png",
            "YOUR_DIRECTORY/img3.png"
        };

        // Step 3: Run OCR in parallel
        var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);

        // Step 4: Output the recognized text
        int index = 1;
        foreach (var result in ocrResults)
        {
            Console.WriteLine($"--- Image {index++} ---");
            Console.WriteLine(result.Text);
        }
    }

    // Helper method for parallel OCR
    static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
    {
        var resultsBag = new ConcurrentBag<OcrResult>();

        Parallel.ForEach(paths, path =>
        {
            try
            {
                var image = ImageStream.FromFile(path);
                OcrResult result = engine.Recognize(image);
                resultsBag.Add(result);
            }
            catch (Exception ex)
            {
                // Log the error but keep the batch running
                Console.Error.WriteLine($"Error processing {path}: {ex.Message}");
            }
        });

        return resultsBag.ToArray();
    }
}
```

### Εκτέλεση του Παραδείγματος

1. Δημιουργήστε ένα νέο έργο **Console App** στο Visual Studio.  
2. Προσθέστε το πακέτο **Aspose.OCR** μέσω NuGet (`Install-Package Aspose.OCR`).  
3. Αντικαταστήστε το `YOUR_DIRECTORY` με τη διαδρομή που περιέχει τα PNG αρχεία σας.  
4. Κατασκευάστε και τρέξτε – θα πρέπει να δείτε το εξαγόμενο κείμενο στην κονσόλα.

## Pro Tips & Edge Cases

- **GPU acceleration:** Αν διαθέτετε συμβατό GPU και έχετε license Aspose OCR, ενεργοποιήστε το μέσω `EngineSettings` πριν δημιουργήσετε τη μηχανή. Αυτό μπορεί να μειώσει δευτερόλεπτα ανά εικόνα.  
- **Μεγάλα αρχεία:** Για εικόνες μεγαλύτερες από 10 MB, σκεφτείτε να τις μειώσετε πρώτα ώστε να μειώσετε την πίεση μνήμης.  
- **Υποστήριξη γλώσσας:** Από προεπιλογή η μηχανή υποθέτει Αγγλικά. Ορίστε `engine.Language = Language.French;` (ή οποιαδήποτε υποστηριζόμενη γλώσσα) για καλύτερη ακρίβεια σε μη‑Αγγλικό κείμενο.  
- **Διαχείριση σφαλμάτων:** Το `try/catch` μέσα στον παράλληλο βρόχο εξασφαλίζει ότι ένα κατεστραμμένο αρχείο δεν διακόπτει ολόκληρη τη δέσμη. Μπορείτε επίσης να καταγράφετε αποτυχίες σε αρχείο για μελλοντική ανασκόπηση.  
- **Αποθήκευση αποτελεσμάτων:** Αντί για εκτύπωση, μπορείτε να γράψετε το `result.Text` σε αρχείο `.txt` χρησιμοποιώντας `File.WriteAllText(Path.ChangeExtension(path, ".txt"))`.

## Συμπέρασμα

Τώρα γνωρίζετε **πώς να χρησιμοποιήσετε OCR** σε C# για να **εξάγετε κείμενο PNG** αρχείων, να **μαζικά OCR εικόνες** και να **επεξεργαστείτε πολλαπλές εικόνες** αποδοτικά με το Aspose OCR C#. Η λύση είναι πλήρως αυτόνομη, τρέχει παράλληλα και μπορεί να επεκταθεί για να διαχειριστεί εκατοντάδες ή χιλιάδες αρχεία με ελάχιστες αλλαγές.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να αντικαταστήσετε την έξοδο στην κονσόλα με μια αναφορά CSV, πειραματιστείτε με την επιτάχυνση GPU ή τροφοδοτήστε το κείμενο OCR σε έναν δείκτη αναζήτησης. Οι δυνατότητες είναι ατελείωτες, και το βασικό μοτίβο—αρχικοποίηση μία φορά, εκτέλεση παράλληλα, διαχείριση σφαλμάτων με χάρη—θα σας εξυπηρετήσει σε οποιοδήποτε pipeline επεξεργασίας εικόνας.

Καλή προγραμματιστική, και να είναι οι εργασίες OCR γρήγορες και χωρίς σφάλματα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}