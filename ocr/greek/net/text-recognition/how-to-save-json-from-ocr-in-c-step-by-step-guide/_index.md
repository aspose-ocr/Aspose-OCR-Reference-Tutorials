---
category: general
date: 2026-02-19
description: Πώς να αποθηκεύσετε JSON από την έξοδο OCR σε C# – μάθετε να εξάγετε
  κείμενο από εικόνα, να γράφετε αρχείο JSON σε C# και να μετατρέπετε εικόνα σε JSON
  με το Aspose OCR.
draft: false
keywords:
- how to save json
- extract text from image
- write json file c#
- convert image to json
- c# ocr tutorial
language: el
og_description: Το πώς να αποθηκεύσετε JSON από τα αποτελέσματα OCR σε C# είναι εύκολο.
  Ακολουθήστε αυτό το σεμινάριο για να εξάγετε κείμενο από εικόνα και να γράψετε αρχείο
  JSON σε στυλ C#.
og_title: Πώς να αποθηκεύσετε JSON από OCR σε C# – Πλήρης οδηγός
tags:
- C#
- OCR
- JSON
title: Πώς να αποθηκεύσετε JSON από OCR σε C# – Οδηγός βήμα‑βήμα
url: /el/net/text-recognition/how-to-save-json-from-ocr-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Αποθηκεύσετε JSON από OCR σε C# – Πλήρης Οδηγός

Το πώς να αποθηκεύσετε json από τα αποτελέσματα OCR σε C# είναι μια συχνή ανάγκη όταν μετατρέπετε σαρωμένα έγγραφα σε δομημένα δεδομένα. Σε αυτόν τον οδηγό θα δείτε ακριβώς πώς να εξάγετε κείμενο από εικόνα, να το μετατρέψετε σε json και τέλος να γράψετε το αρχείο json με στυλ C# — χωρίς περιττές πληροφορίες, μόνο μια λειτουργική λύση.

Έχετε προσπαθήσει ποτέ να διαβάσετε μια απόδειξη με σαρωτή, μόνο για να καταλήξετε με μια θολή εικόνα που δεν μπορείτε να αναζητήσετε; Αυτό είναι το πρόβλημα που αντιμετωπίζουν πολλοί προγραμματιστές όταν χρειάζεται να εξάγουν δεδομένα από εικόνες. Στο τέλος αυτού του άρθρου θα έχετε μια μικρή εφαρμογή console που διαβάζει μια εικόνα, εξάγει το κείμενο με Aspose OCR και αποθηκεύει ένα καθαρό αρχείο json που μπορείτε να τροφοδοτήσετε σε οποιαδήποτε επόμενη υπηρεσία.

Θα καλύψουμε τα πάντα: το πακέτο NuGet που χρειάζεστε, τον ακριβή κώδικα (πλήρης, εκτελέσιμος και με πολλές σχολιασμούς), κοινά προβλήματα και έναν γρήγορο τρόπο να επαληθεύσετε το αποτέλεσμα. Δεν απαιτείται προηγούμενη εμπειρία OCR — μόνο μια βασική κατανόηση του C# και του .NET.

## Προαπαιτούμενα

Πριν βουτήξουμε, βεβαιωθείτε ότι έχετε:

- .NET 6 SDK ή νεότερο (ο κώδικας στοχεύει στο .NET 6 αλλά λειτουργεί και σε .NET 5+)
- Visual Studio 2022, VS Code ή οποιονδήποτε επεξεργαστή προτιμάτε
- Ένα αρχείο εικόνας (`input.png`) που θέλετε να επεξεργαστείτε
- Πρόσβαση στο Internet για να κατεβάσετε το **Aspose.OCR** πακέτο NuGet

Αν λείπει κάτι από τα παραπάνω, αποκτήστε το τώρα· διαφορετικά θα χάσετε χρόνο αργότερα.  

> **Pro tip:** Το Aspose OCR προσφέρει ένα δωρεάν κλειδί δοκιμής — ιδανικό για πειραματισμό χωρίς άδεια.

## Βήμα 1: Εγκατάσταση του Πακέτου Aspose OCR NuGet

Πρώτα, προσθέστε τη βιβλιοθήκη που κάνει το βαρέως φορτίου έργο. Ανοίξτε ένα τερματικό στον φάκελο του έργου σας και τρέξτε:

```bash
dotnet add package Aspose.OCR
```

Αυτή η εντολή κατεβάζει τα πιο πρόσφατα binaries του Aspose OCR και προσθέτει μια αναφορά στο `.csproj` σας.  

> **Γιατί είναι σημαντικό αυτό το βήμα:** Χωρίς το πακέτο, η κλάση `OcrEngine` δεν υπάρχει, και θα λάβετε σφάλματα κατά τη μεταγλώττιση.  

Τώρα που το πακέτο είναι στη θέση του, ας δημιουργήσουμε το σκελετό της εφαρμογής console.

## Βήμα 2: Ρύθμιση της Δομής του Έργου

Δημιουργήστε ένα νέο έργο console αν δεν το έχετε κάνει ήδη:

```bash
dotnet new console -n JsonExportOcr
cd JsonExportOcr
```

Στο `Program.cs` αντικαταστήστε το προεπιλεγμένο περιεχόμενο με το πλήρες παράδειγμα παρακάτω. Θα περάσουμε από κάθε γραμμή αργότερα, αλλά το να έχετε το αρχείο έτοιμο βοηθά στο copy‑paste χωρίς να λείπει κάποια αγκύλη.

## Βήμα 3: Αρχικοποίηση του OCR Engine (Εξαγωγή Κειμένου από Εικόνα)

Η πρώτη πραγματική γραμμή κώδικα δημιουργεί ένα OCR engine και του λέει να ψάχνει για αγγλικούς χαρακτήρες. Μπορείτε να το αλλάξετε σε `Language.Spanish` ή οποιαδήποτε άλλη υποστηριζόμενη γλώσσα, αλλά τα αγγλικά είναι η πιο κοινή περίπτωση.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;
using System;
using System.IO;

class JsonExport
{
    static void Main()
    {
        // Step 3.1: Create an OCR engine and set the language to English
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };

        // Step 3.2: Recognize text from the input image
        // Replace the path with where your image actually lives
        string inputPath = @"YOUR_DIRECTORY/input.png";
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);
```

**Τι συμβαίνει;**  
- Η `OcrEngine` είναι το σημείο εισόδου για το Aspose OCR.  
- Η ρύθμιση του `Language` βελτιώνει την ακρίβεια επειδή η μηχανή μπορεί να εφαρμόσει γλωσσικές ευρετικές.  
- Η `RecognizeImage` επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει όλες τις αναγνωρισμένες λέξεις, τα ποσοστά εμπιστοσύνης και τα πλαίσια περιορισμού.

Αν η εικόνα λείπει ή είναι κατεστραμμένη, η προειδοποιητική εντολή εκτυπώνει ένα φιλικό μήνυμα και τερματίζει — αυτή η μικρή έλεγχος σας σώζει από ένα συγκεχυμένο σφάλμα null‑reference αργότερα.

## Βήμα 4: Μετατροπή του OCR Result σε JSON (Μετατροπή Εικόνας σε JSON)

Το Aspose OCR περιλαμβάνει έναν βοηθό που ονομάζεται `JsonResultWriter`. Αυτός σειριοποιεί το `OcrResult` σε μια καθαρή συμβολοσειρά JSON που αντικατοπτρίζει τη δομή που θα περιμένατε από ένα REST API.

```csharp
        // Step 4: Convert the OCR result to a JSON string
        string jsonResult = JsonResultWriter.Write(ocrResult);
```

**Γιατί να χρησιμοποιήσετε το `JsonResultWriter`;**  
- Διαχειρίζεται αυτόματα πολύπλοκα αντικείμενα (όπως ενσωματωμένες συλλογές `Word`).  
- Αποφεύγετε το να γράψετε τον δικό σας σειριακοποιητή, ο οποίος μπορεί να παραλείψει λεπτομερή πεδία όπως τα ποσοστά εμπιστοσύνης.

Σε αυτό το σημείο το `jsonResult` φαίνεται περίπου έτσι (μορφοποιημένο για ευανάγνωστη παρουσία):

```json
{
  "PageCount": 1,
  "Pages": [
    {
      "PageNumber": 1,
      "Words": [
        {
          "Text": "Hello",
          "Confidence": 0.98,
          "BoundingBox": { "X": 10, "Y": 20, "Width": 50, "Height": 15 }
        },
        // … more words …
      ]
    }
  ]
}
```

Μπορείτε να αντιγράψετε αυτό το απόσπασμα σε έναν προβολέα JSON για να εξερευνήσετε τη δομή.  

> **Edge case:** Αν η εικόνα σας περιέχει πολλαπλές σελίδες, το JSON θα περιλαμβάνει έναν πίνακα `Pages` — βεβαιωθείτε ότι οι καταναλωτές downstream μπορούν να το διαχειριστούν.

## Βήμα 5: Εγγραφή του JSON στο Δίσκο (Πώς να Αποθηκεύσετε JSON)

Τώρα έρχεται η καρδιά του οδηγού: **πώς να αποθηκεύσετε json** σε αρχείο στο δίσκο. Η κλάση .NET `File` το κάνει με μία γραμμή κώδικα, αλλά θα προσθέσουμε μια μικρή διαχείριση σφαλμάτων για μεγαλύτερη ανθεκτικότητα.

```csharp
        // Step 5: Write the JSON string to an output file
        string outputPath = @"YOUR_DIRECTORY/output.json";
        try
        {
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"JSON saved to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to write JSON: {ex.Message}");
        }
```

Αυτή είναι η στιγμή που τελικά απαντάτε στην ερώτηση *πώς να αποθηκεύσετε json* — το αρχείο δημιουργείται, αντικαθίσταται αν υπήρχε ήδη, και λαμβάνετε ένα σαφές μήνυμα στην κονσόλα που επιβεβαιώνει την επιτυχία.

## Βήμα 6: Επαλήθευση του Αποτελέσματος

Αφού το πρόγραμμα ολοκληρωθεί, ανοίξτε το `output.json` σε οποιονδήποτε επεξεργαστή (VS Code, Notepad++, ή ακόμη και σε έναν φυλλομετρητή). Θα πρέπει να δείτε μια ωραία μορφοποιημένη αναπαράσταση JSON της εξόδου OCR. Αν δείτε κενά arrays `"Words": []`, ελέγξτε ξανά την ποιότητα της εικόνας — το OCR δυσκολεύεται με χαμηλή αντίθεση ή πολύ θόρυβο.

Μπορείτε επίσης να τρέξετε έναν γρήγορο έλεγχο από τη γραμμή εντολών:

```bash
dotnet run
```

Θα πρέπει να δείτε:

```
JSON saved to YOUR_DIRECTORY/output.json
```

Αν εμφανιστεί σφάλμα, η κονσόλα θα σας πει αν λείπει το αρχείο εισόδου ή αν η εγγραφή απέτυχε.

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω είναι το **πλήρες** πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε στο `Program.cs`. Αντικαταστήστε το `YOUR_DIRECTORY` με το φάκελο που περιέχει το `input.png`. Δεν χρειάζονται άλλα αρχεία.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;
using System;
using System.IO;

class JsonExport
{
    static void Main()
    {
        // Step 3: Initialize OCR engine (extract text from image)
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };

        // Define file paths
        string inputPath = @"YOUR_DIRECTORY/input.png";
        string outputPath = @"YOUR_DIRECTORY/output.json";

        // Validate input image exists
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        // Recognize text
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        // Convert OCR result to JSON (convert image to json)
        string jsonResult = JsonResultWriter.Write(ocrResult);

        // Write JSON to disk (how to save json)
        try
        {
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"JSON saved to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to write JSON: {ex.Message}");
        }
    }
}
```

Τρέξτε το πρόγραμμα, ανοίξτε το παραγόμενο αρχείο, και έχετε ολοκληρώσει επιτυχώς ένα **c# ocr tutorial** που δείχνει **πώς να αποθηκεύσετε json** από μια εικόνα.

## Συνηθισμένα Προβλήματα & Συμβουλές (Write JSON File C#)

| Πρόβλημα | Γιατί Συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| **Κενός πίνακας `Words`** | Η εικόνα είναι πολύ σκοτεινή ή χαμηλής ανάλυσης | Προεπεξεργαστείτε την εικόνα (αυξήστε την αντίθεση, χρησιμοποιήστε υψηλότερο DPI) |
| **`File.WriteAllText` ρίχνει UnauthorizedAccessException** | Προσπάθεια εγγραφής σε φάκελο μόνο για ανάγνωση | Επιλέξτε έναν φάκελο με δικαιώματα εγγραφής (π.χ., `%TEMP%` ή το φάκελο του έργου) |
| **Λείπει το πακέτο NuGet** | Ξέχασα να τρέξω `dotnet add package Aspose.OCR` | Εκτελέστε ξανά την εντολή και κάντε rebuild |
| **Το JSON είναι σε μία γραμμή** | Η `WriteAllText` γράφει την ακατέργαστη συμβολοσειρά χωρίς μορφοποίηση | Χρησιμοποιήστε `JsonResultWriter.Write(ocrResult, true)` αν υπάρχει το overload, ή περάστε το αποτέλεσμα από `JsonSerializer` με `WriteIndented = true` |

Αυτοί οι γρήγοροι έλεγχοι κρατούν τη ροή **write json file c#** ομαλή και αποτρέπουν τα ανεπιθύμητα «δεν συνέβη τίποτα» στιγμιότυπα.

## Επόμενα Βήματα (Extract Text from Image & More)

Τώρα που ξέρετε **πώς να αποθηκεύσετε json**, ίσως θέλετε να:

- **Store the

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}