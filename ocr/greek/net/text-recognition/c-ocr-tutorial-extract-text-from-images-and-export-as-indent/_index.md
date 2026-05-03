---
category: general
date: 2026-05-02
description: c# OCR tutorial που δείχνει πώς να εξάγετε κείμενο από εικόνα c# και
  να αναγνωρίσετε κείμενο PNG, και στη συνέχεια να γράψετε μορφοποιημένο JSON χρησιμοποιώντας
  το JsonSerializer c#. Οδηγός βήμα‑βήμα για προγραμματιστές.
draft: false
keywords:
- c# ocr tutorial
- extract text image c#
- recognize png text
- write indented json
- use jsonserializer c#
language: el
og_description: c# OCR tutorial που δείχνει πώς να εξάγετε κείμενο από εικόνα c# και
  να αναγνωρίσετε κείμενο PNG, και στη συνέχεια να γράψετε μορφοποιημένο JSON με το
  JsonSerializer c#. Πλήρες, εκτελέσιμο παράδειγμα.
og_title: c# OCR οδηγός – Εξαγωγή κειμένου και εξαγωγή ως JSON με εσοχές
tags:
- OCR
- C#
- Aspose
- JSON
title: c# OCR tutorial – Εξαγωγή κειμένου από εικόνες και εξαγωγή ως JSON με εσοχές
url: /el/net/text-recognition/c-ocr-tutorial-extract-text-from-images-and-export-as-indent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Εξαγωγή Κειμένου από Εικόνες και Εξαγωγή ως Εσοδιασμένο JSON

Έχετε ποτέ χρειαστεί ένα **c# ocr tutorial** που περνάει από μια φωτογραφία κειμένου κατευθείαν σε ένα ωραία μορφοποιημένο αρχείο JSON; Δεν είστε ο μόνος. Σε πολλά έργα – σκεφτείτε σάρωση τιμολογίων, ανάλυση αποδείξεων ή ακόμη και εξαγωγή κειμένου από meme – καταλήγετε με ένα αρχείο PNG και αναρωτιέστε πώς να εξάγετε τις λέξεις χωρίς να γράψετε έναν προσαρμοσμένο αναγνωριστή.  

Αυτός ο οδηγός σας παρέχει μια πρακτική λύση: θα **extract text image c#** χρησιμοποιώντας το Aspose.OCR, **recognize png text**, και στη συνέχεια **write indented json** με το `JsonSerializer` σε C#. Στο τέλος θα έχετε μια αυτόνομη εφαρμογή κονσόλας που μπορείτε να ενσωματώσετε σε οποιαδήποτε λύση .NET. Χωρίς ασαφείς συνδέσμους “δείτε την τεκμηρίωση”, μόνο ένα πλήρες παράδειγμα έτοιμο για αντιγραφή‑και‑επικόλληση.

## Τι Θα Χρειαστείτε

- **.NET 6** (ή οποιαδήποτε πρόσφατη έκδοση .NET). Τα παλαιότερα πλαίσια λειτουργούν, αλλά η σύνταξη που εμφανίζεται στοχεύει στο .NET 6+.
- **Aspose.OCR for .NET** – εγκαταστήστε μέσω NuGet: `dotnet add package Aspose.OCR`.
- Ένα δείγμα PNG εικόνας (`text.png`) που περιέχει καθαρό, μηχανικά αναγνώσιμο κείμενο.
- Ένα IDE ή επεξεργαστή της επιλογής σας – Visual Studio, VS Code, Rider, κλπ.

> **Pro tip:** Αν σκοπεύετε να επεξεργαστείτε πολλές εικόνες, σκεφτείτε να επαναχρησιμοποιήσετε ένα μόνο αντικείμενο `OcrEngine` αντί να δημιουργείτε νέο για κάθε αρχείο. Αυτό μειώνει το κόστος και βελτιώνει τη ροή δεδομένων.

## Βήμα 1: Ρύθμιση Έργου c# ocr tutorial

Αρχικά, δημιουργήστε ένα έργο κονσόλας. Οι παρακάτω εντολές δημιουργούν τη δομή και προσθέτουν τη βιβλιοθήκη OCR:

```bash
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo
dotnet add package Aspose.OCR
```

Τώρα ανοίξτε το παραγόμενο `Program.cs`. Θα αντικαταστήσουμε το περιεχόμενό του με το πλήρες παράδειγμα αργότερα, αλλά προς το παρόν βεβαιωθείτε ότι το έργο κατασκευάζεται:

```bash
dotnet build
```

Αν δεν δείτε σφάλματα, είστε έτοιμοι να προχωρήσετε.

## Βήμα 2: Αναγνώριση Κειμένου PNG από Εικόνα

Η καρδιά κάθε **c# ocr tutorial** είναι η ίδια η μηχανή OCR. Το Aspose.OCR αφαιρεί τις λεπτομέρειες χαμηλού επιπέδου και σας παρέχει μια καθαρή κλάση `OcrEngine`. Παρακάτω δημιουργούμε τη μηχανή, την κατευθύνουμε σε ένα αρχείο PNG και της ζητάμε να αναγνωρίσει το κείμενο.

```csharp
using Aspose.OCR;
using System;
using System.Text.Json;

class JsonExportExample
{
    public static void Run()
    {
        // 1️⃣ Create an OCR engine instance – this is the entry point for all OCR work.
        var ocrEngine = new OcrEngine();

        // 2️⃣ Recognize text from the input image. 
        //    The method automatically detects the language (default is English) and returns an OcrResult.
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/text.png");

        // If the image couldn't be read, handle it gracefully.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No text detected – double‑check the file path and image quality.");
            return;
        }

        // Continue to serialization...
```

### Γιατί Αυτό Λειτουργεί

- **`RecognizeImage`** δέχεται πολλές μορφές (PNG, JPEG, BMP). Αναγνωρίζουμε ειδικά **recognize png text** επειδή το PNG διατηρεί λεπτομέρειες χωρίς απώλειες, κάτι που είναι ιδανικό για OCR.
- Το επιστρεφόμενο `OcrResult` περιέχει όχι μόνο το απλό κείμενο αλλά και βαθμολογία εμπιστοσύνης ανά γλύφο, χρήσιμη αν χρειαστεί να φιλτράρετε χαρακτήρες χαμηλής εμπιστοσύνης αργότερα.

## Βήμα 3: Γράψτε Εσοδιασμένο JSON με JsonSerializer c#

Τώρα που έχουμε το `ocrResult`, το επόμενο λογικό βήμα στο **c# ocr tutorial** μας είναι να μετατρέψουμε αυτό το αντικείμενο σε αναγνώσιμο από άνθρωπο JSON. Ο ενσωματωμένος σειριοποιητής `System.Text.Json` κάνει τη δουλειά, και θα το ρυθμίσουμε ώστε να **write indented json** για σαφήνεια.

```csharp
        // 3️⃣ Serialize the OCR result (including confidence per glyph) to indented JSON.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // This makes the output pretty‑printed.
        };

        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 4️⃣ Display the JSON result – you could also write it to a file if you prefer.
        Console.WriteLine(jsonOutput);
    }
}
```

### Χρήση του `JsonSerializer` Σωστά

- Η σημαία `WriteIndented` είναι ο πιο απλός τρόπος να **write indented json** χωρίς να προσθέτετε βιβλιοθήκες τρίτων.
- Αν χρειαστείτε ποτέ ονόματα ιδιοτήτων σε camel‑case, προσθέστε `PropertyNamingPolicy = JsonNamingPolicy.CamelCase` στις επιλογές.
- Η συμβολοσειρά `jsonOutput` μπορεί να αποθηκευτεί με `File.WriteAllText("result.json", jsonOutput);` – μια χρήσιμη προσαρμογή για πραγματικές ροές εργασίας.

## Βήμα 4: Εκτελέστε και Επαληθεύστε το Αποτέλεσμα

Συγκεντρώστε και εκτελέστε το πρόγραμμα:

```bash
dotnet run
```

Υποθέτοντας ότι το `text.png` περιέχει τη φράση *“Hello, OCR World!”*, θα πρέπει να δείτε κάτι όπως:

```json
{
  "Text": "Hello, OCR World!",
  "Confidence": 0.9875,
  "Lines": [
    {
      "Text": "Hello, OCR World!",
      "Confidence": 0.9875,
      "Words": [
        {
          "Text": "Hello,",
          "Confidence": 0.9921,
          "BoundingBox": { "X": 12, "Y": 34, "Width": 58, "Height": 20 }
        },
        {
          "Text": "OCR",
          "Confidence": 0.9812,
          "BoundingBox": { "X": 78, "Y": 34, "Width": 34, "Height": 20 }
        },
        {
          "Text": "World!",
          "Confidence": 0.9890,
          "BoundingBox": { "X": 118, "Y": 34, "Width": 62, "Height": 20 }
        }
      ]
    }
  ]
}
```

Αυτό το JSON είναι **indented**, καθιστώντας το εύκολο στην ανάγνωση στα αρχεία καταγραφής ή για μεταβίβαση σε downstream υπηρεσίες.

### Περιπτώσεις Ορίων & Συμβουλές

| Situation | What to Do |
|-----------|------------|
| **Η εικόνα είναι θολή** | Αυξήστε το `ocrEngine.Config.Dpi` (π.χ., `ocrEngine.Config.Dpi = 300`) πριν καλέσετε το `RecognizeImage`. |
| **Μη‑Αγγλική γλώσσα** | Ορίστε `ocrEngine.Config.Language = OcrLanguage.German` (ή οποιαδήποτε υποστηριζόμενη γλώσσα). |
| **Μεγάλο σύνολο αρχείων** | Κάντε βρόχο πάνω σε έναν φάκελο, επαναχρησιμοποιώντας το ίδιο αντικείμενο `OcrEngine`; αποθηκεύστε κάθε αποτέλεσμα JSON με μοναδικό όνομα αρχείου. |
| **Απαιτείται μόνο κείμενο υψηλής εμπιστοσύνης** | Φιλτράρετε τα `ocrResult.Lines` όπου `Confidence` ≥ 0.95 πριν τη σειριοποίηση. |

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω είναι το *ολόκληρο* πρόγραμμα, έτοιμο να τοποθετηθεί στο `Program.cs`. Περιλαμβάνει όλα τα βήματα, διαχείριση σφαλμάτων και σχόλια που κάνουν τον κώδικα αυτοεξηγηματικό.

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    public static void Main()
    {
        // 👉 Step 1: Initialize the OCR engine.
        var ocrEngine = new OcrEngine();

        // 👉 Step 2: Path to the PNG image you want to process.
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "text.png");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found at {imagePath}");
            return;
        }

        // 👉 Step 3: Perform OCR – this is where we **recognize png text**.
        var ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 👉 Step 4: Validate the result.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No recognizable text found. Try a clearer image or adjust DPI settings.");
            return;
        }

        // 👉 Step 5: Configure JsonSerializer to **write indented json**.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // Pretty‑print the JSON.
        };

        // 👉 Step 6: Serialize the OCR result – this demonstrates **use jsonserializer c#**.
        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 👉 Step 7: Output to console (or write to a file).
        Console.WriteLine(jsonOutput);

        // Optional: Save to disk.
        string outputPath = Path.ChangeExtension(imagePath, ".json");
        File.WriteAllText(outputPath, jsonOutput);
        Console.WriteLine($"JSON saved to {outputPath}");
    }
}
```

Εκτελέστε τον κώδικα, ελέγξτε την κονσόλα ή το παραγόμενο αρχείο `.json`, και θα δείτε το εξαγόμενο κείμενο μαζί με τις βαθμολογίες εμπιστοσύνης, όλα τακτοποιημένα **indented**.

## Συμπέρασμα

Τώρα έχετε ένα ολοκληρωμένο **c# ocr tutorial** που δείχνει πώς να **extract text image c#**, **recognize png text**, και **write indented json** χρησιμοποιώντας το `JsonSerializer`. Το παράδειγμα είναι πλήρες, εκτελέσιμο, και περιλαμβάνει πρακτικές συμβουλές για πραγματικά σενάρια.  

Επόμενα βήματα; Δοκιμάστε να αντικαταστήσετε το Aspose.OCR με άλλη μηχανή (π.χ., Tesseract) και δείτε πώς αλλάζει η δομή του `OcrResult`, ή στείλτε το JSON σε ένα downstream API που αποθηκεύει τα δεδομένα OCR σε βάση δεδομένων. Μπορείτε επίσης να πειραματιστείτε με τις επιλογές **use jsonserializer c#** όπως προσαρμοσμένοι μετατροπείς για μορφοποίηση ημερομηνιών ή διαχείριση enum.  

Καλό κώδικα, και εύχομαι οι OCR αγωγοί σας να είναι πάντα ακριβείς!  

---  

![Διάγραμμα c# ocr tutorial](image.png "Διάγραμμα που απεικονίζει τη ροή OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}