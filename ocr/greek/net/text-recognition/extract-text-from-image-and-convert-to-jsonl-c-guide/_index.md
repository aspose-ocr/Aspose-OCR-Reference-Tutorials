---
category: general
date: 2026-01-02
description: Εξάγετε κείμενο από εικόνα χρησιμοποιώντας το Aspose OCR σε C#. Μάθετε
  πώς να μετατρέψετε την εικόνα σε μορφή JSONL γρήγορα και αξιόπιστα.
draft: false
keywords:
- extract text from image
- convert image to jsonl
language: el
og_description: Εξάγετε κείμενο από εικόνα με το Aspose OCR και μετατρέψτε το σε μορφή
  JSONL. Πλήρης βήμα‑βήμα οδηγός C# για προγραμματιστές.
og_title: Εξαγωγή κειμένου από εικόνα – Μετατροπή σε JSONL σε C#
tags:
- C#
- OCR
- Aspose
- JSONL
title: Εξαγωγή κειμένου από εικόνα και μετατροπή σε JSONL – Οδηγός C#
url: /el/net/text-recognition/extract-text-from-image-and-convert-to-jsonl-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή κειμένου από εικόνα και μετατροπή σε JSONL – Πλήρες C# Tutorial

Έχετε ποτέ χρειαστεί να **εξάγετε κείμενο από εικόνα** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη θα σας δώσει καθαρό, δομημένο αποτέλεσμα; Δεν είστε μόνοι. Σε πολλά έργα επεξεργασίας αποδείξεων ή ψηφιοποίησης εγγράφων το στενό λαιμό είναι η μετατροπή ενός bitmap σε αναζητήσιμο κείμενο *και* σε μορφή που μπορεί να διαβαστεί από μηχανή.

Τα καλά νέα; Με το Aspose OCR μπορείτε να **εξάγετε κείμενο από εικόνα** και, με λίγες γραμμές κώδικα, **μετατρέψετε την εικόνα σε JSONL** για downstream analytics. Αυτός ο οδηγός σας καθοδηγεί βήμα‑βήμα σε όλη τη διαδικασία, από τη φόρτωση ενός PNG μέχρι τη δημιουργία ενός αρχείου JSON‑Lines που μπορεί να ροήσει σε ένα data pipeline.

> **Συμβουλή:** Αν ήδη χρησιμοποιείτε .NET 6 ή νεότερο, ο ίδιος κώδικας λειτουργεί χωρίς πρόσθετη διαμόρφωση.

## Προαπαιτούμενα — Τι θα χρειαστείτε

- **.NET 6 SDK** (ή οποιαδήποτε πρόσφατη έκδοση .NET)
- **Aspose.OCR** NuGet package  
  ```bash
  dotnet add package Aspose.OCR
  ```
- **Newtonsoft.Json** for serialization  
  ```bash
  dotnet add package Newtonsoft.Json
  ```
- Ένα δείγμα εικόνας (π.χ., `receipt.png`) τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε.
- Ένα IDE ή επεξεργαστή της επιλογής σας—Visual Studio, VS Code, Rider, κ.λπ.

Καμία βαριά εγκατάσταση, χωρίς εξωτερικές υπηρεσίες, μόνο μερικά NuGet packages.

![Extract text from image using C#](https://example.com/assets/ocr-sample.png)

*Κείμενο alt: εξαγωγή κειμένου από εικόνα χρησιμοποιώντας C# με Aspose OCR*

## Βήμα 1: Φορτώστε την εικόνα που θέλετε να επεξεργαστείτε  

Το πρώτο πράγμα που κάνετε όταν θέλετε να **εξάγετε κείμενο από εικόνα** είναι να δώσετε στο OCR engine ένα bitmap. Η χρήση του `System.Drawing.Bitmap` είναι απλή και λειτουργεί για τις περισσότερες μορφές raster.

```csharp
using System.Drawing;

// Adjust the path to where your receipt.png lives
string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
Bitmap receiptImage = new Bitmap(imagePath);
```

> **Γιατί είναι σημαντικό:** Η φόρτωση της εικόνας ως `Bitmap` δίνει στο OCR engine άμεση πρόσβαση στα pixel, βελτιώνοντας την ταχύτητα και την ακρίβεια της αναγνώρισης σε σχέση με τη ροή ακατέργαστων bytes.

## Βήμα 2: Διαμορφώστε το Aspose OCR για έξοδο JSON‑Lines  

Το Aspose OCR σας επιτρέπει να ορίσετε γλώσσα, μορφή εξόδου και μερικές ρυθμίσεις απόδοσης. Εδώ ζητάμε **JSON‑Lines** (ένα JSON αντικείμενο ανά γραμμή) επειδή είναι ιδανικό για επεξεργασία γραμμή‑με‑γραμμή αργότερα.

```csharp
using Aspose.OCR;

// Create the engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine we’re dealing with English text
RecognitionOptions options = new RecognitionOptions
{
    Language = Language.English,
    OutputFormat = OutputFormat.JsonLines   // This is the key for converting image to JSONL
};
```

> **Pro tip:** Αν χρειάζεστε πολυγλωσσικές αποδείξεις, ορίστε `Language = Language.Multilingual` ή περάστε έναν πίνακα τιμών `Language`.

## Βήμα 3: Εκτελέστε το OCR και καταγράψτε το αποτέλεσμα  

Τώρα πραγματικά **εξάγουμε κείμενο από εικόνα**. Η μέθοδος `Recognize` επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει μια συλλογή από αντικείμενα `OcrLine`, το καθένα αντιπροσωπεύει μια γραμμή αναγνωρισμένου κειμένου μαζί με το bounding box της.

```csharp
// Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);
```

Σε αυτό το σημείο το `ocrResult.Lines` περιέχει όλα όσα χρειάζεστε—ακατέργαστο κείμενο, βαθμολογίες εμπιστοσύνης και συντεταγμένες.

## Βήμα 4: Σειριοποιήστε τις γραμμές σε JSON‑Lines  

Θα μετατρέψουμε τη συλλογή σε ένα ωραία εσοχή JSON string. Παρόλο που τα JSON‑Lines είναι συνήθως συμπαγή, η προσθήκη εσοχής κάνει το αρχείο πιο εύκολο στην επιθεώρηση κατά την ανάπτυξη.

```csharp
using Newtonsoft.Json;

// Serialize each line as a separate JSON object
string jsonLines = JsonConvert.SerializeObject(
    ocrResult.Lines,
    Formatting.Indented
);
```

Το παραγόμενο μεταβλητό `jsonLines` φαίνεται κάπως έτσι (προσαρμοσμένο για συντομία):

```json
{
  "Text": "Store XYZ",
  "Confidence": 0.98,
  "BoundingBox": { "X": 10, "Y": 15, "Width": 120, "Height": 20 }
}
{
  "Text": "Date: 01/01/2026",
  "Confidence": 0.95,
  "BoundingBox": { "X": 10, "Y": 45, "Width": 180, "Height": 20 }
}
```

Κάθε γραμμή λήγει με χαρακτήρα newline, δίνοντάς σας ένα αληθινό **JSONL** (JSON‑Lines) αρχείο.

## Βήμα 5: Γράψτε τα JSON‑Lines στο δίσκο  

Τέλος, αποθηκεύουμε το αποτέλεσμα ώστε άλλες υπηρεσίες—όπως Spark, Logstash ή ένα απλό Bash script—να το καταναλώνουν γραμμή‑με‑γραμμή.

```csharp
using System.IO;

// Choose a destination file
string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
File.WriteAllText(outputPath, jsonLines);
```

Όταν ανοίξετε το `receipt.jsonl` θα δείτε ένα JSON αντικείμενο ανά γραμμή, έτοιμο για streaming.

## Βήμα 6: Επαληθεύστε την εξαγωγή  

Μια γρήγορη έλεγχος λογικής σας εξοικονομεί ώρες debugging αργότερα. Ας διαβάσουμε τις πρώτες λίγες γραμμές ξανά και να τις εκτυπώσουμε στην κονσόλα.

```csharp
Console.WriteLine("First three lines of the JSONL output:");
foreach (var line in File.ReadLines(outputPath).Take(3))
{
    Console.WriteLine(line);
}
```

Τυπική έξοδος κονσόλας:

```
First three lines of the JSONL output:
{"Text":"Store XYZ","Confidence":0.98,"BoundingBox":{"X":10,"Y":15,"Width":120,"Height":20}}
{"Text":"Date: 01/01/2026","Confidence":0.95,"BoundingBox":{"X":10,"Y":45,"Width":180,"Height":20}}
{"Text":"Total   $23.45","Confidence":0.97,"BoundingBox":{"X":10,"Y":75,"Width":150,"Height":20}}
```

Αν δείτε κάτι παρόμοιο, συγχαρητήρια—έχετε επιτυχώς **εξάγει κείμενο από εικόνα** και **μετέτρεψα την εικόνα σε JSONL**.

## Συνηθισμένα προβλήματα & Πώς να τα αποφύγετε  

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|------------------|----------|
| **Κενό αποτέλεσμα** | Λάθος διαδρομή εικόνας ή το αρχείο δεν είναι αναγνώσιμο. | Χρησιμοποιήστε `File.Exists(imagePath)` πριν δημιουργήσετε το bitmap. |
| **Χαμηλές βαθμολογίες εμπιστοσύνης** | Η εικόνα είναι θολή ή έχει χαμηλή αντίθεση. | Προ‑επεξεργαστείτε την εικόνα (π.χ., `Bitmap.RotateFlip`, `Graphics.Clear`) ή αυξήστε το DPI. |
| **Λανθασμένη γλώσσα** | Το OCR προεπιλογή είναι Αγγλικά αλλά η απόδειξη είναι σε άλλη γλώσσα. | Ορίστε `options.Language = Language.Spanish` (ή το κατάλληλο enum). |
| **Το JSONL εμφανίζεται ως ένας ενιαίος JSON πίνακας** | Χρησιμοποιήσατε `Formatting.None` χωρίς διαχείριση newline. | Βεβαιωθείτε ότι κάθε σειριοποιημένο αντικείμενο λήγει με `Environment.NewLine`. |

## Πλήρες Παράδειγμα Εργασίας  

Παρακάτω είναι το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα. Επικολλήστε το σε ένα console project και πατήστε **F5**.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Linq;
using Newtonsoft.Json;

namespace OcrToJsonlDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the image
            string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found at {imagePath}");
                return;
            }
            Bitmap receiptImage = new Bitmap(imagePath);

            // 2️⃣ Set up OCR options for JSON‑Lines output
            OcrEngine ocrEngine = new OcrEngine();
            RecognitionOptions options = new RecognitionOptions
            {
                Language = Language.English,
                OutputFormat = OutputFormat.JsonLines
            };

            // 3️⃣ Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);

            // 4️⃣ Serialize to JSON‑Lines
            string jsonLines = JsonConvert.SerializeObject(
                ocrResult.Lines,
                Formatting.Indented
            );

            // 5️⃣ Write to file
            string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
            File.WriteAllText(outputPath, jsonLines);
            Console.WriteLine($"✅ JSONL saved to {outputPath}");

            // 6️⃣ Quick verification
            Console.WriteLine("\nFirst three lines of output:");
            foreach (var line in File.ReadLines(outputPath).Take(3))
            {
                Console.WriteLine(line);
            }
        }
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Ένα αρχείο `receipt.jsonl` που περιέχει ένα JSON αντικείμενο ανά γραμμή, το καθένα με πεδία `Text`, `Confidence` και `BoundingBox`. Τώρα μπορείτε να τροφοδοτήσετε αυτό το αρχείο σε οποιοδήποτε pipeline analytics που καταναλώνει JSONL.

## Επόμενα βήματα – Πέρα από το βασικό OCR  

- **Batch processing:** Τυλίξτε τη λογική σε έναν βρόχο `foreach` για επεξεργασία ολόκληρων φακέλων αποδείξεων.  
- **Parallelism:** Χρησιμοποιήστε `Parallel.ForEach` για επιταχύνσεις πολλαπλών πυρήνων όταν επεξεργάζεστε χιλιάδες εικόνες.  
- **Post‑processing:** Αφαιρέστε γραμμές χαμηλής εμπιστοσύνης (`Confidence < 0.9`) πριν αποθηκεύσετε.  
- **Integration:** Σπρώξτε το JSONL απευθείας στο Azure Blob Storage ή AWS S3 με τα αντίστοιχα SDKs.  
- **Alternative formats:** Αλλάξτε το `OutputFormat` σε `PlainText` ή `Xml` αν το downstream σύστημα προτιμά αυτές τις μορφές.  

## Συμπέρασμα  

Τώρα έχετε μια σταθερή, end‑to‑end λύση για **εξαγωγή κειμένου από εικόνα** και **μετατροπή εικόνας σε JSONL** χρησιμοποιώντας το Aspose OCR σε C#. Το tutorial κάλυψε τα πάντα—from τη φόρτωση του bitmap μέχρι την επαλήθευση του αποτελέσματος, μαζί με πρακτικές συμβουλές για να κρατήσετε το pipeline σας αξιόπιστο.

Δοκιμάστε το με τις δικές σας αποδείξεις, τιμολόγια ή σαρωμένες φόρμες—παρακολουθήστε το OCR engine να μετατρέπει pixel σε αναζητήσιμο, δομημένο κατά γραμμή δεδομένο σε δευτερόλεπτα. Αν αντιμετωπίσετε edge cases (π.χ., παραμορφωμένες σκαναρίσματα ή πολυγλωσσικό κείμενο), επιστρέψτε στην ενότητα *RecognitionOptions* και ρυθμίστε τη γλώσσα ή τα βήματα προεπεξεργασίας.

Καλή προγραμματιστική, και οι pipelines δεδομένων σας να είναι πάντα καθαροί!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}