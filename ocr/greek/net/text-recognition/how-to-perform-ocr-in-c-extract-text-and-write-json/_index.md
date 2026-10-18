---
category: general
date: 2026-02-09
description: Μάθετε πώς να εκτελείτε OCR σε C# για να εξάγετε κείμενο από εικόνα,
  να αναγνωρίζετε κείμενο από PNG και να γράφετε γρήγορα αρχείο JSON σε C#.
draft: false
keywords:
- how to perform OCR
- extract text from image
- recognize text from png
- write json file c#
language: el
og_description: Πώς να εκτελέσετε OCR σε C#; Ακολουθήστε αυτόν τον βήμα‑βήμα οδηγό
  για να εξάγετε κείμενο από εικόνα, να αναγνωρίσετε κείμενο από PNG και να γράψετε
  αρχείο JSON σε C# αποδοτικά.
og_title: Πώς να εκτελέσετε OCR σε C# – Εξαγωγή κειμένου και δημιουργία JSON
tags:
- OCR
- C#
- Aspose
- JSON
title: Πώς να εκτελέσετε OCR σε C# – Εξαγωγή κειμένου και δημιουργία JSON
url: /el/net/text-recognition/how-to-perform-ocr-in-c-extract-text-and-write-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εκτελέσετε OCR σε C# – Πλήρης Οδηγός

Το πώς να εκτελέσετε OCR σε C# είναι ένα συχνό εμπόδιο όταν χρειάζεται να **εξάγετε κείμενο από αρχείο εικόνας**. Σε αυτόν τον οδηγό θα περάσουμε από την αναγνώριση κειμένου από PNG, την εξαγωγή του λεπτομερούς αποτελέσματος σε συμβολοσειρά JSON, και τέλος **να γράψετε αρχείο JSON C#**. Έχετε κολλήσει ποτέ σε μια σαρωμένη φόρμα και αναρωτηθείτε πώς να μετατρέψετε αυτά τα σκαλίσματα σε αναζητήσιμο κείμενο; Δεν είστε μόνοι· πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα νωρίς.

Θα χρησιμοποιήσουμε τη βιβλιοθήκη Aspose.OCR επειδή παρέχει εμπιστοσύνη ανά σύμβολο έτοιμη προς χρήση και συνεργάζεται άψογα με έργα .NET 6+. Στο τέλος αυτού του σεμινάριου θα έχετε μια έτοιμη για εκτέλεση εφαρμογή κονσόλας που φορτώνει ένα PNG, εξάγει κάθε χαρακτήρα και αποθηκεύει ένα καθαρό αρχείο JSON που μπορείτε να τροφοδοτήσετε σε βάση δεδομένων ή μοντέλο AI. Χωρίς μυστικά “δείτε τα docs” συντομεύσεις—απλώς μια αυτόνομη λύση.

## Τι Θα Χρειαστεί

- **.NET 6 SDK** (ή νεότερο) – η τρέχουσα έκδοση LTS τη στιγμή της συγγραφής.
- **Aspose.OCR for .NET** πακέτο NuGet – `Install-Package Aspose.OCR`.
- Μια εικόνα PNG που θέλετε να σαρώσετε (π.χ., `form.png`).  
- Ένα IDE ή επεξεργαστής – Visual Studio, VS Code, Rider – ό,τι σας βολεύει.

Αυτό είναι όλο. Αν έχετε αυτά τα στοιχεία, είστε έτοιμοι να ξεκινήσετε.

![Πώς να εκτελέσετε OCR παράδειγμα](ocr-example.png "Πώς να εκτελέσετε OCR σε C#")

*Κείμενο alt εικόνας: εικονογράφηση του πώς να εκτελέσετε OCR που δείχνει μια εφαρμογή κονσόλας C# που επεξεργάζεται ένα PNG.*

## Βήμα 1: Ρύθμιση του Έργου και Προσθήκη Εξαρτήσεων

Πρώτα, δημιουργήστε ένα νέο έργο κονσόλας και προσθέστε τη βιβλιοθήκη Aspose OCR.

```csharp
// Create a new console app (run in terminal)
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo

// Add Aspose.OCR NuGet package
dotnet add package Aspose.OCR
```

> **Pro tip:** Χρησιμοποιήστε τη σημαία `--framework net6.0` αν θέλετε να κλειδώσετε ρητά το στοχευόμενο framework.

Γιατί είναι σημαντικό αυτό το βήμα: το πακέτο NuGet περιέχει τις κλάσεις `OcrEngine`, `ImageStream` και `JsonExporter` στις οποίες θα βασιστούμε. Χωρίς αυτό, ο μεταγλωττιστής δεν θα ξέρει τι σημαίνει “OCR”.

## Βήμα 2: Γράψτε τη Βασική Λογική OCR

Ανοίξτε το `Program.cs` (ή δημιουργήστε νέο αρχείο) και αντικαταστήστε το περιεχόμενό του με το ακόλουθο. Κάθε τμήμα είναι σχολιασμένο ώστε να καταλάβετε γιατί υπάρχει.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Export;
using System;

namespace OcrJsonDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Initialize the OCR engine – this prepares the
            //    internal models and allocates native resources.
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // 2️⃣ Load the image you want to process.
            //    Replace the path with your own PNG file.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/form.png";
            ImageStream image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // 3️⃣ Perform OCR recognition – the heavy lifting.
            //    The result includes text, per‑symbol confidence,
            //    and layout information.
            // -------------------------------------------------
            RecognitionResult ocrResult = ocrEngine.Recognize(image);

            // -------------------------------------------------
            // 4️⃣ Export the result to a JSON string.
            //    JsonExporter respects the confidence values.
            // -------------------------------------------------
            JsonExporter jsonExporter = new JsonExporter();
            string jsonContent = jsonExporter.ExportToString(ocrResult);

            // -------------------------------------------------
            // 5️⃣ Write the JSON to disk – this is how we
            //    **write JSON file C#** style.
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/form.json";
            System.IO.File.WriteAllText(jsonPath, jsonContent);

            // -------------------------------------------------
            // 6️⃣ Let the user know we succeeded.
            // -------------------------------------------------
            Console.WriteLine($"JSON file saved successfully at {jsonPath}");
        }
    }
}
```

### Γιατί Κάθε Τμήμα Είναι Σημαντικό

- **OcrEngine**: Σκεφτείτε το ως τον εγκέφαλο της λειτουργίας. Φορτώνει μοντέλα γλώσσας και ρυθμίζει τη γραμμή επεξεργασίας.
- **ImageStream.FromFile**: Διαχειρίζεται οποιοδήποτε PNG, JPEG, BMP κ.λπ. Απομονώνει τις ιδιαιτερότητες του I/O αρχείων.
- **RecognitionResult**: Περιέχει το ακατέργαστο κείμενο μαζί με τις βαθμολογίες εμπιστοσύνης. Εδώ παίρνετε τα λεπτομερή δεδομένα που χρειάζεστε για επακόλουθη επικύρωση.
- **JsonExporter**: Μετατρέπει το πλούσιο `RecognitionResult` σε καθαρό payload JSON, ιδανικό για APIs.
- **File.WriteAllText**: Ο απλός τρόπος .NET για **να γράψετε αρχείο JSON C#** χωρίς πρόσθετες εξαρτήσεις.

## Βήμα 3: Εκτελέστε την Εφαρμογή και Επαληθεύστε το Αποτέλεσμα

Συγκεντρώστε και εκτελέστε το πρόγραμμα:

```bash
dotnet run
```

Θα πρέπει να δείτε ένα μήνυμα κονσόλας παρόμοιο με:

```
JSON file saved successfully at YOUR_DIRECTORY/form.json
```

Ανοίξτε το `form.json` – θα βρείτε κάτι σαν:

```json
{
  "Text": "Sample Form\nName: John Doe\nDate: 2026-02-09",
  "Symbols": [
    { "Char": "S", "Confidence": 0.99, "X": 12, "Y": 8 },
    { "Char": "a", "Confidence": 0.98, "X": 22, "Y": 8 },
    // … more symbols …
  ]
}
```

Το βήμα **εξαγωγής κειμένου από εικόνα** ολοκληρώθηκε επιτυχώς, και τώρα έχετε μια μηχανικά αναγνώσιμη αναπαράσταση JSON κάθε χαρακτήρα.

## Βήμα 4: Διαχείριση Συνηθισμένων Περιπτώσεων Άκρων

### Ελλιπή ή Κατεστραμμένα Αρχεία

Αν η διαδρομή του PNG είναι λανθασμένη, το `ImageStream.FromFile` ρίχνει `FileNotFoundException`. Τυλίξτε τον κώδικα φόρτωσης σε μπλοκ try‑catch:

```csharp
try
{
    ImageStream image = ImageStream.FromFile(imagePath);
}
catch (FileNotFoundException ex)
{
    Console.Error.WriteLine($"Could not find image: {ex.Message}");
    return;
}
```

### Χαμηλές Βαθμολογίες Εμπιστοσύνης

Μερικές φορές το OCR επιστρέφει χαμηλή εμπιστοσύνη για θορυβώδεις σαρώσεις. Μπορείτε να φιλτράρετε σύμβολα πριν την εξαγωγή:

```csharp
ocrResult.Symbols.RemoveAll(s => s.Confidence < 0.6);
```

Αυτό εξασφαλίζει ότι το JSON περιέχει μόνο χαρακτήρες με λογικά αξιόπιστες βαθμολογίες—χρήσιμο όταν τροφοδοτείτε τα δεδομένα σε επακόλουπες pipelines επικύρωσης.

### Μεγάλα Αρχεία & Μνήμη

Η επεξεργασία ενός PNG πολλαπλών megabytes μπορεί να αυξήσει τη χρήση μνήμης. Σκεφτείτε να κάνετε streaming της εικόνας σε τμήματα ή να χρησιμοποιήσετε `OcrEngine.RecognizeAsync` (διαθέσιμο σε νεότερες εκδόσεις Aspose) για να διατηρήσετε την UI ανταποκρινόμενη.

## Βήμα 5: Επέκταση της Λύσης (Προαιρετικό)

- **Batch processing**: Επανάληψη σε έναν φάκελο PNG και δημιουργία αντίστοιχου JSON για κάθε αρχείο.
- **Αποθήκευση σε βάση δεδομένων**: Εισαγωγή του JSON σε στήλη SQL `NVARCHAR(MAX)` για μελλοντική ανάλυση.
- **Επιλογή γλώσσας**: Ορίστε `ocrEngine.Language = OcrLanguage.Spanish;` αν χρειάζεστε υποστήριξη μη‑αγγλικών.

Όλες αυτές οι επεκτάσεις ακολουθούν το ίδιο **πώς να εκτελέσετε OCR** μοτίβο που καθιερώσαμε—αρχικοποίηση, αναγνώριση, εξαγωγή και αποθήκευση.

## Συχνές Ερωτήσεις

**Q: Λειτουργεί αυτό με JPG ή TIFF;**  
A: Απόλυτα. Το `ImageStream.FromFile` ανιχνεύει αυτόματα τη μορφή, οπότε μπορείτε να αντικαταστήσετε το PNG με οποιαδήποτε υποστηριζόμενη ραστερική εικόνα.

**Q: Τι γίνεται αν χρειαστεί να εξάγω κείμενο από PDF;**  
A: Μετατρέψτε πρώτα κάθε σελίδα PDF σε εικόνα (π.χ., χρησιμοποιώντας `Aspose.PDF`) και μετά τροφοδοτήστε το PNG στη ροή OCR που περιγράφηκε εδώ.

**Q: Μπορώ να λάβω το αποτέλεσμα OCR ως XML αντί για JSON;**  
A: Ναι. Το Aspose.OCR παρέχει επίσης `XmlExporter`. Αντικαταστήστε το `JsonExporter` με `XmlExporter` και προσαρμόστε την επέκταση αρχείου.

## Συμπέρασμα

Διασχίσαμε **πώς να εκτελέσετε OCR** σε C# από την αρχή μέχρι το τέλος, δείχνοντας πώς να **εξάγετε κείμενο από εικόνα**, **να αναγνωρίζετε κείμενο από PNG**, και **να γράψετε αρχείο JSON C#** χωρίς προβλήματα. Το πλήρες, εκτελέσιμο παράδειγμα βρίσκεται στα αποσπάσματα κώδικα παραπάνω, και τώρα κατανοείτε το «γιατί» πίσω από κάθε βήμα—την αρχικοποίηση του κινητήρα, τη διαχείριση περιπτώσεων άκρων, και την αποθήκευση των αποτελεσμάτων.

Στη συνέχεια, μπορείτε να εξερευνήσετε pipelines batch OCR, να ενσωματώσετε την έξοδο JSON με Azure Cognitive Search, ή να πειραματιστείτε με προσαρμοσμένα μοντέλα γλώσσας. Ο ουρανός είναι το όριο μόλις κυριαρχήσετε τα βασικά του OCR σε C#.

Αν αντιμετωπίσατε δυσκολίες ή έχετε ιδέες για περαιτέρω επεκτάσεις, αφήστε ένα σχόλιο παρακάτω. Καλό κώδικα και απολαύστε τη μετατροπή των pixelated σαρώσεων σε καθαρά, αναζητήσιμα δεδομένα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}