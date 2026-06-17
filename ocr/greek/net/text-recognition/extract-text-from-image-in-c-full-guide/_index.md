---
category: general
date: 2026-03-23
description: Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας το Aspose OCR σε C# και μάθετε
  πώς να προσθέσετε καταγραφέα κονσόλας για ανατροφοδότηση σε πραγματικό χρόνο.
draft: false
keywords:
- extract text from image
- add console logger
language: el
og_description: Εξαγωγή κειμένου από εικόνα με Aspose OCR και προσθήκη καταγραφέα
  κονσόλας για την παρακολούθηση της διαδικασίας. Βήμα‑βήμα οδηγός C#.
og_title: Εξαγωγή κειμένου από εικόνα σε C# – Πλήρης οδηγός προγραμματισμού
tags:
- OCR
- C#
- logging
title: Εξαγωγή κειμένου από εικόνα σε C# – Πλήρης οδηγός
url: /el/net/text-recognition/extract-text-from-image-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Εικόνα σε C# – Πλήρης Οδηγός

Χρειάζεστε **extract text from image** γρήγορα και αξιόπιστα; Με το Aspose OCR μπορείτε να το κάνετε ακριβώς αυτό με λίγες γραμμές C#.  
Θα σας δείξουμε επίσης πώς να **add console logger** ώστε να παρακολουθείτε το OCR engine να ψιθυρίζει την πρόοδό του απευθείας στο τερματικό σας.

Φανταστείτε ότι έχετε μια σαρωμένη απόδειξη, μια χειρόγραφη σημείωση ή μια σελίδα PDF αποθηκευμένη ως PNG. Θέλετε τους ακατέργαστους χαρακτήρες χωρίς να ανοίξετε ένα βαριά UI. Αυτό το tutorial σας καθοδηγεί βήμα‑βήμα με μια πλήρη, αντιγραφή‑και‑επικόλληση λύση που λειτουργεί σήμερα με .NET 6+ και τη νεότερη βιβλιοθήκη Aspose OCR.

Με το τέλος αυτού του οδηγού θα μπορείτε να:

* Φορτώσετε ένα αρχείο εικόνας και εκτελέσετε OCR για **extract text from image** δεδομένα.  
* Συνδέσετε έναν console logger στο Aspose AI ώστε να βλέπετε τι κάνει η βιβλιοθήκη στο παρασκήνιο.  
* Εφαρμόσετε τον ενσωματωμένο spell‑check post‑processor για να καθαρίσετε τα σφάλματα OCR.  

> **Προαπαιτούμενα** – Ένα λειτουργικό .NET περιβάλλον ανάπτυξης (Visual Studio 2022, VS Code ή Rider), .NET 6 SDK ή νεότερο, και άδεια Aspose OCR (ή δωρεάν δοκιμή). Δεν απαιτούνται άλλα πακέτα τρίτων.

## Τι Θα Χρειαστεί

| Στοιχείο | Γιατί είναι σημαντικό |
|------|----------------|
| **Aspose.OCR** NuGet package | Παρέχει την κλάση `OcrEngine` που διαβάζει πραγματικά την εικόνα. |
| **Aspose.OCR.AI** NuGet package | Σας παρέχει το πλαίσιο post‑processor `AsposeAI`, συμπεριλαμβανομένου του spell‑check. |
| **Microsoft.Extensions.Logging** (optional) | Παρέχει τη διεπαφή `ILogger` για το βήμα **add console logger**. |
| **An input image** (`input.png`) | Το αρχείο πηγής από το οποίο θα **extract text from image**. |

Μπορείτε να εγκαταστήσετε τα πακέτα μέσω του τερματικού:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.AI
dotnet add package Microsoft.Extensions.Logging.Abstractions
```

## Βήμα 1 – Εξαγωγή Κειμένου από Εικόνα με Aspose OCR

Το πρώτο που κάνουμε είναι να δώσουμε την εικόνα στον OCR engine. Αυτό το μπλοκ κάνει τη βαριά δουλειά και επιστρέφει μια ακατέργαστη συμβολοσειρά που μπορεί ακόμη να περιέχει ορθογραφικά λάθη.

```csharp
using Aspose.OCR;
using System;

class OcrDemo
{
    static string PerformOcr(string imagePath)
    {
        // Initialise the OCR engine
        using (OcrEngine ocr = new OcrEngine())
        {
            // Load the image – replace with your own path if needed
            ocr.Image = ImageStream.FromFile(imagePath);

            // Run recognition; if it fails we return an empty string
            if (!ocr.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return string.Empty;
            }

            // The engine populates the Text property with the recognised characters
            string rawText = ocr.Text;
            Console.WriteLine("Raw OCR output:\n" + rawText);
            return rawText;
        }
    }
}
```

**Γιατί λειτουργεί:** `OcrEngine` αφαιρεί όλη την χαμηλού επιπέδου προεπεξεργασία εικόνας (δυαδικοποίηση, διόρθωση κλίσης κ.λπ.). Όταν το `Recognize()` επιστρέφει `true`, η ιδιότητα `Text` περιέχει ήδη τους καλύτερους εικαστικούς χαρακτήρες.  

> **Συμβουλή:** Αν η εικόνα σας είναι μεγάλη, σκεφτείτε να την αλλάξετε μέγεθος σε ≤ 2000 px στην μεγαλύτερη πλευρά πριν τη δώσετε στον engine. Αυτό επιταχύνει την επεξεργασία χωρίς να επηρεάσει την ακρίβεια.

## Βήμα 2 – Προσθήκη Console Logger για Ενσυναίσθηση σε Πραγματικό Χρόνο

Τώρα φέρνουμε το τμήμα **add console logger**. Η καταγραφή δεν είναι μόνο για εντοπισμό σφαλμάτων· σας δίνει ορατότητα στις λήψεις μοντέλων, στα βήματα του AI‑processor και σε τυχόν προειδοποιήσεις που μπορεί να εκδώσει η βιβλιοθήκη.

```csharp
using Microsoft.Extensions.Logging;
using System;

public class ConsoleLogger : ILogger
{
    // Minimal ILogger implementation that writes to the console.
    public IDisposable BeginScope<TState>(TState state) => null;
    public bool IsEnabled(LogLevel logLevel) => true;

    public void Log<TState>(LogLevel logLevel, EventId eventId,
        TState state, Exception exception, Func<TState, Exception, string> formatter)
    {
        Console.WriteLine($"[{logLevel}] {formatter(state, exception)}");
    }
}
```

Τώρα μπορείτε να συνδέσετε αυτόν τον logger στο Aspose AI:

```csharp
using Aspose.OCR.AI;
using Aspose.OCR.AI.PostProcessors;

// ...

ILogger consoleLogger = new ConsoleLogger();   // Implements ILogger
AsposeAI ai = new AsposeAI(consoleLogger);
```

**Τι θα δείτε:** Όταν το μοντέλο spell‑check ληφθεί αυτόματα, η κονσόλα θα εκτυπώσει μια γραμμή όπως:

```
[Information] Downloading model to YOUR_DIRECTORY/Models/spellcheck.onnx …
```

Αυτό είναι το πλεονέκτημα του **add console logger** – δεν θα αναρωτιέστε ποτέ αν μια λειτουργία στο παρασκήνιο ολοκληρώθηκε επιτυχώς.

## Βήμα 3 – Διαμόρφωση και Καταχώριση του Spell‑Check Post‑Processor

Το Aspose AI περιλαμβάνει έναν χρήσιμο spell‑check post‑processor που καθαρίζει τα κοινά σφάλματα OCR (π.χ., “rec0gn1ze” → “recognize”). Θα το διαμορφώσουμε, προαιρετικά θα πούμε στη βιβλιοθήκη πού να αποθηκεύσει το μοντέλο, και στη συνέχεια θα το καταχωρίσουμε.

```csharp
// Create the built‑in spell‑check processor
SpellCheckAIProcessor spellProcessor = new SpellCheckAIProcessor();

// Optional: tell AsposeAI where to keep downloaded models
AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
{
    AllowAutoDownload = true,
    DirectoryModelPath = "YOUR_DIRECTORY/Models"
};

// Register the processor with the AI engine
ai.SetPostProcessor(spellProcessor, modelConfig);
```

**Γιατί μπορεί να θέλετε προσαρμοσμένη διαδρομή:** Σε CI/CD pipelines συχνά θέλετε να αποθηκεύετε μοντέλα σε γνωστό φάκελο για να αποφύγετε επαναλαμβανόμενες λήψεις. Η σημαία `AllowAutoDownload` εξασφαλίζει ότι το μοντέλο θα ληφθεί την πρώτη φορά που τρέχετε τον κώδικα.

## Βήμα 4 – Εκτέλεση του Post‑Processor στο Αποτέλεσμα OCR

Με το κείμενο OCR στα χέρια και τον spell‑check processor έτοιμο, δίνουμε τη ακατέργαστη συμβολοσειρά στο `AsposeAI`. Ο engine εκτελεί το μοντέλο, και ο processor αποθηκεύει το διορθωμένο κείμενο εσωτερικά.

```csharp
// Assume ocrResult contains the raw OCR output from Step 1
string ocrResult = PerformOcr("YOUR_DIRECTORY/input.png");

// Run the post‑processor – it expects an IEnumerable<string>
ai.RunPostprocessor(new[] { ocrResult });
```

Μετά από αυτήν την κλήση, το `spellProcessor` περιέχει μια συλλογή από αντικείμενα `RecognitionResult`, καθένα με ιδιότητα `RecognitionText` που περιέχει την καθαρισμένη έκδοση.

## Βήμα 5 – Ανάκτηση και Εμφάνιση του Διορθωμένου Κειμένου

Τέλος, εξάγουμε τη διορθωμένη συμβολοσειρά από τον processor και την εκτυπώνουμε. Αυτή είναι η στιγμή που βλέπετε πραγματικά το όφελος τόσο του OCR όσο και της ροής εργασίας **add console logger**.

```csharp
// Grab the first (and only) result
string correctedText = spellProcessor.GetResult()[0].RecognitionText;
Console.WriteLine("\nCorrected OCR output:\n" + correctedText);
```

**Αναμενόμενη έξοδος** (υποθέτοντας ότι η εικόνα περιέχει τη φράση “Aspose OCR demo” με λίγα σφάλματα OCR):

```
Raw OCR output:
Asp0se OCR d3mo

[Information] Model downloaded successfully.
[Information] Spell‑check completed.

Corrected OCR output:
Aspose OCR demo
```

Παρατηρήστε πώς ο logger μας ενημέρωσε ότι το μοντέλο ήταν έτοιμο, και η διορθωμένη γραμμή εμφανίζεται καθαρά.

## Βήμα 6 – Καθαρισμός Πόρων

Τanto `AsposeAI` όσο και το `OcrEngine` υλοποιούν το `IDisposable`. Η απελευθέρωση τους αποδεσμεύει τη φυσική μνήμη και τους χειριστές αρχείων, κάτι που είναι ιδιαίτερα σημαντικό σε υπηρεσίες που τρέχουν για μεγάλο χρονικό διάστημα.

```csharp
// At the end of Main()
ai.Dispose();   // Releases AI resources
// OcrEngine is already disposed via the using‑statement in PerformOcr()
```

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω βρίσκεται ολόκληρο το πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε ένα νέο console project (`dotnet new console`). Αντικαταστήστε το `"YOUR_DIRECTORY"` με έναν πραγματικό φάκελο στο μηχάνημά σας.

```csharp
using Aspose.OCR;
using Aspose.OCR.AI;
using Aspose.OCR.AI.PostProcessors;
using Microsoft.Extensions.Logging; // optional logger
using System;

class SpellCheckDemo
{
    static void Main()
    {
        // ---------- Step 1: OCR ----------
        string ocrResult = PerformOcr("YOUR_DIRECTORY/input.png");
        if (string.IsNullOrEmpty(ocrResult)) return;

        // ---------- Step 2: Initialise AI with console logger ----------
        ILogger consoleLogger = new ConsoleLogger(); // implements ILogger
        AsposeAI ai = new AsposeAI(consoleLogger);

        // ---------- Step 3: Spell‑check processor ----------
        SpellCheckAIProcessor spellProcessor = new SpellCheckAIProcessor();

        // ---------- Step 4: Model configuration (optional) ----------
        AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
        {
            AllowAutoDownload = true,
            DirectoryModelPath = "YOUR_DIRECTORY/Models"
        };

        // ---------- Step 5: Register and run ----------
        ai.SetPostProcessor(spellProcessor, modelConfig);
        ai.RunPostprocessor(new[] { ocrResult });

        // ---------- Step 6: Show corrected text ----------
        string correctedText = spellProcessor.GetResult()[0].RecognitionText;
        Console.WriteLine("\nCorrected OCR output:\n" + correctedText);

        // ---------- Clean up ----------
        ai.Dispose();
    }

    static string PerformOcr(string imagePath)
    {
        using (OcrEngine ocr = new OcrEngine())
        {
            ocr.Image = ImageStream.FromFile(imagePath);
            if (!ocr.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return string.Empty;
            }
            string raw = ocr.Text;
            Console.WriteLine("Raw OCR output:\n" + raw);
            return raw;
        }
    }
}

// Minimal console logger implementation
public class ConsoleLogger : ILogger
{
    public IDisposable BeginScope<TState>(TState state) => null;
    public bool

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}