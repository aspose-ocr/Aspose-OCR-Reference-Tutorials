---
category: general
date: 2026-01-01
description: c# OCR οδηγός που δείχνει πώς να εξάγετε κείμενο, να φορτώσετε εικόνα
  για OCR και να γράψετε JSON σε αρχείο χρησιμοποιώντας το Aspose.OCR – οδηγός βήμα‑προς‑βήμα.
draft: false
keywords:
- c# OCR tutorial
- how to extract text
- write json to file
- load image for OCR
- OCR image to JSON
language: el
og_description: c# OCR tutorial που σας καθοδηγεί πώς να εξάγετε κείμενο από εικόνες,
  να φορτώσετε εικόνα για OCR και να γράψετε JSON σε αρχείο χρησιμοποιώντας το Aspose.OCR.
og_title: c# OCR οδηγός – Εξαγωγή κειμένου και εξαγωγή σε JSON
tags:
- Aspose.OCR
- C#
- Text Extraction
title: c# OCR tutorial – Εξαγωγή κειμένου από εικόνες και εξαγωγή σε JSON
url: /el/net/text-recognition/c-ocr-tutorial-extract-text-from-images-and-export-to-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR tutorial – Εξαγωγή κειμένου από εικόνες και εξαγωγή σε JSON

Έχετε ποτέ αναρωτηθεί πώς να εξάγετε κείμενο από ένα σαρωμένο τιμολόγιο χωρίς να περάσετε ώρες γράφοντας προσαρμοσμένους αναλυτές; Δεν είστε μόνοι. Σε αυτό το **c# OCR tutorial** θα σας δείξουμε ακριβώς πώς να φορτώσετε μια εικόνα για OCR, να εκτελέσετε τη μηχανή αναγνώρισης και, στη συνέχεια, **να γράψετε JSON σε αρχείο** ώστε να μπορείτε να τροφοδοτήσετε τα δεδομένα σε downstream συστήματα.

Φανταστείτε ότι έχετε έναν φάκελο με αποδείξεις, καθεμία με όνομα `receipt1.png`, `receipt2.png`, και χρειάζεστε έναν γρήγορο τρόπο να τις μετατρέψετε σε αναζητήσιμα JSON αρχεία. Αυτό είναι το πρόβλημα που θα λύσουμε, και στο τέλος θα έχετε μια έτοιμη για εκτέλεση εφαρμογή console που κάνει ακριβώς αυτό. Χωρίς επιπλέον εξαρτήσεις πέρα από το Aspose.OCR, και χωρίς μαγεία — μόνο σαφή, επαναλήψιμα βήματα.

> **Τι θα μάθετε**
> - Πώς να **φορτώσετε εικόνα για OCR** χρησιμοποιώντας το Aspose.OCR.
> - Τον καλύτερο τρόπο **πώς να εξάγετε κείμενο** και να λάβετε σκορ εμπιστοσύνης.
> - Μετατροπή του αποτελέσματος OCR σε καλά δομημένο **OCR image to JSON** payload.
> - Ασφαλή **εγγραφή JSON σε αρχείο** και επαλήθευση του αποτελέσματος.

## Προαπαιτούμενα

- .NET 6 SDK ή νεότερο (ο κώδικας λειτουργεί και σε .NET Core).  
- Visual Studio 2022 ή οποιονδήποτε επεξεργαστή προτιμάτε.  
- Πακέτο NuGet Aspose.OCR (`Install-Package Aspose.OCR`).  
- Ένα αρχείο εικόνας (PNG, JPG, BMP) που θέλετε να επεξεργαστείτε — για την επίδειξη θα χρησιμοποιήσουμε το `invoice.png`.

Αν λείπει κάτι από αυτά, κατεβάστε το SDK από τον ιστότοπο της Microsoft και προσθέστε το πακέτο NuGet μέσω του Package Manager Console:

```powershell
Install-Package Aspose.OCR
```

Τώρα που το υπόβαθρο είναι έτοιμο, ας βουτήξουμε στην υλοποίηση.

## Βήμα 1: c# OCR tutorial – Αρχικοποίηση της μηχανής OCR

Πριν μπορέσουμε να **φορτώσουμε εικόνα για OCR**, χρειαζόμαστε μια παρουσία της μηχανής που θα οδηγήσει τη διαδικασία αναγνώρισης. Η κλάση `OcrEngine` είναι ελαφριά, αλλά είναι καλή πρακτική να την τυλίγουμε σε ένα μπλοκ `using` ώστε οι πόροι να απελευθερώνονται άμεσα.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonExportDemo
{
    static void Main()
    {
        // Step 1: Create the OCR engine – this is the heart of the c# OCR tutorial
        var ocrEngine = new OcrEngine();

        // The rest of the steps follow…
```

*Pro tip:* Αν σκοπεύετε να επεξεργαστείτε πολλές εικόνες σε batch, επαναχρησιμοποιήστε την ίδια παρουσία `OcrEngine` αντί να δημιουργείτε νέα κάθε φορά. Μειώνει την κατανάλωση μνήμης και επιταχύνει τη διαδικασία.

## Βήμα 2: Φόρτωση εικόνας για OCR

Τώρα φορτώνουμε πραγματικά την **εικόνα για OCR**. Το Aspose.OCR υποστηρίζει ποικίλες μορφές, ώστε να μπορείτε να το κατευθύνετε σε PNG, JPEG ή ακόμη και σε πολυ‑σελίδα TIFF. Η μέθοδος `OcrImage.FromFile` διαβάζει το αρχείο και το προετοιμάζει για αναγνώριση.

```csharp
        // Step 2: Load the image you want to recognize
        // Replace YOUR_DIRECTORY with the folder that holds your invoice.png
        var imagePath = @"YOUR_DIRECTORY/invoice.png";
        var ocrImage = OcrImage.FromFile(imagePath);
```

> **Γιατί είναι σημαντικό:** Η ξεχωριστή φόρτωση της εικόνας σας επιτρέπει να ελέγξετε τις διαστάσεις, το DPI ή ακόμη και να την προεπεξεργαστείτε (π.χ., δυαδικοποίηση) πριν τη στείλετε στη μηχανή. Αν η εικόνα είναι κατεστραμμένη, το `FromFile` θα ρίξει μια σαφή εξαίρεση, την οποία μπορείτε να πιάσετε και να καταγράψετε.

## Βήμα 3: Πώς να εξάγετε κείμενο – Εκτέλεση της αναγνώρισης

Με την εικόνα στα χέρια, μπορούμε τελικά να **εξάγουμε κείμενο** από αυτήν. Η μέθοδος `Recognize` επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει όχι μόνο το απλό κείμενο, αλλά και δεδομένα θέσης και σκορ εμπιστοσύνης για κάθε λέξη.

```csharp
        // Step 3: Perform OCR – this is the core of how to extract text
        var ocrResult = ocrEngine.Recognize(ocrImage);
```

*Edge case:* Ορισμένα PDF περιέχουν αόρατα στρώματα κειμένου. Αν τροφοδοτήσετε μια σελίδα PDF που έχει αποδοθεί ως εικόνα, η μηχανή μπορεί να μην δει τίποτα. Σε αυτές τις περιπτώσεις, σκεφτείτε να χρησιμοποιήσετε το Aspose.PDF για να εξάγετε το κρυφό στρώμα πρώτα, και μετά να καταφύγετε στο OCR μόνο όταν χρειάζεται.

## Βήμα 4: OCR image to JSON – Μετατροπή του αποτελέσματος

Η κλάση `OcrResult` προσφέρει ένα βολικό βοηθητικό μέθοδο `ToJson()` που σειριοποιεί ολόκληρο το σύνολο αποτελεσμάτων — συμπεριλαμβανομένου του bounding box και του confidence κάθε λέξης — σε μια συμβολοσειρά JSON. Αυτός είναι ο πιο καθαρός τρόπος για να πετύχετε **OCR image to JSON** χωρίς να γράψετε δικό σας serializer.

```csharp
        // Step 4: Convert the OCR result to JSON (includes words, confidence, locations)
        string jsonResult = ocrResult.ToJson();
```

Αν προτιμάτε ένα προσαρμοσμένο σχήμα, μπορείτε να επαναλάβετε το `ocrResult.Words` και να δημιουργήσετε το δικό σας αντικείμενο, αλλά για τις περισσότερες περιπτώσεις το ενσωματωμένο JSON είναι επαρκές και ήδη καλά δομημένο.

## Βήμα 5: Εγγραφή JSON σε αρχείο

Τώρα έρχεται το τελευταίο κομμάτι του παζλ: η αποθήκευση του JSON payload. Η μέθοδος `File.WriteAllText` εξασφαλίζει ότι το αρχείο δημιουργείται (ή αντικαθίσταται) ατομικά. Βεβαιωθείτε ότι ο προορισμός υπάρχει, διαφορετικά θα αντιμετωπίσετε `DirectoryNotFoundException`.

```csharp
        // Step 5: Save the JSON output – this demonstrates write JSON to file
        var jsonPath = @"YOUR_DIRECTORY/invoice.json";
        File.WriteAllText(jsonPath, jsonResult);
```

*Tip:* Αν χρειάζεστε UTF‑8 με BOM ή διαφορετική κωδικοποίηση, χρησιμοποιήστε την υπερφόρτωση που δέχεται ένα όρισμα `Encoding`.

## Βήμα 6: Επαλήθευση του αποτελέσματος

Ένα γρήγορο `Console.WriteLine` μας λέει ότι η διαδικασία ολοκληρώθηκε επιτυχώς. Μπορείτε επίσης να ανοίξετε το αρχείο JSON σε έναν προβολέα για να επιβεβαιώσετε τη δομή.

```csharp
        // Step 6: Inform the user that the JSON file has been saved
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

### Αναμενόμενο απόσπασμα JSON

```json
{
  "Text": "Invoice #12345\nDate: 2025-12-31\nTotal: $250.00",
  "Words": [
    { "Text": "Invoice", "Confidence": 0.98, "Location": { "X": 10, "Y": 15, "Width": 80, "Height": 20 } },
    { "Text": "#12345", "Confidence": 0.96, "Location": { "X": 95, "Y": 15, "Width": 60, "Height": 20 } }
    // … more words …
  ]
}
```

Το JSON περιλαμβάνει τη θέση κάθε λέξης, κάτι που είναι χρήσιμο αν αργότερα θέλετε να επισημάνετε το κείμενο σε UI.

## Πλήρες Παράδειγμα Λειτουργίας

Ακολουθεί το πλήρες, έτοιμο για αντιγραφή‑και‑επικόλληση πρόγραμμα. Αντικαταστήστε το `YOUR_DIRECTORY` με την πραγματική διαδρομή όπου βρίσκεται η εικόνα σας.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonExportDemo
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to recognize
        var imagePath = @"YOUR_DIRECTORY/invoice.png";
        var ocrImage = OcrImage.FromFile(imagePath);

        // Step 3: Perform OCR – how to extract text
        var ocrResult = ocrEngine.Recognize(ocrImage);

        // Step 4: Convert the result to JSON (OCR image to JSON)
        string jsonResult = ocrResult.ToJson();

        // Step 5: Write JSON to file – write JSON to file
        var jsonPath = @"YOUR_DIRECTORY/invoice.json";
        File.WriteAllText(jsonPath, jsonResult);

        // Step 6: Verify
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

Τρέξτε το πρόγραμμα (`dotnet run` από το φάκελο του έργου) και θα βρείτε το `invoice.json` δίπλα στο αρχικό PNG.

## Συνηθισμένα Προβλήματα & Πώς να τα Αποφύγετε

| Πρόβλημα | Γιατί Συμβαίνει | Λύση |
|----------|----------------|------|
| **FileNotFoundException** κατά τη φόρτωση της εικόνας | Λάθος διαδρομή ή λείπει το αρχείο | Χρησιμοποιήστε `Path.Combine` και ελέγξτε `File.Exists` πριν καλέσετε `FromFile`. |
| **Χαμηλά σκορ εμπιστοσύνης** | Κακή ποιότητα εικόνας, χαμηλό DPI | Προεπεξεργασία με `ocrImage.AdjustContrast` ή αύξηση DPI σε 300. |
| **Κενό αρχείο JSON** | `ocrResult` επιστράφηκε null (η μηχανή απέτυχε) | Επαληθεύστε ότι η μορφή εικόνας υποστηρίζεται και ότι η άδεια (αν υπάρχει) έχει εφαρμοστεί σωστά. |
| **Σ bottleneck απόδοσης σε μεγάλα batch** | Δημιουργία νέου `OcrEngine` σε κάθε επανάληψη | Επαναχρησιμοποιήστε μία ενιαία παρουσία `OcrEngine` για όλο το batch, απελευθερώνοντας τη μόνο στο τέλος. |

## Επόμενα Βήματα

Τώρα που έχετε κατακτήσει το **c# OCR tutorial**, ίσως θέλετε να:

- **Επεξεργαστείτε batch** ολόκληρου φακέλου και να συγκεντρώσετε τα JSON αρχεία σε μια ενιαία βάση δεδομένων.
- **Ενσωματώσετε** το αποτέλεσμα με το Azure Cognitive Search για αναζητήσιμα PDF.
- **Προσθέσετε υποστήριξη γλώσσας** ορίζοντας `ocrEngine.Language = OcrLanguage.Spanish` (ή οποιαδήποτε υποστηριζόμενη γλώσσα).
- **Μετα-επεξεργασία** του JSON για εξαγωγή πινάκων ή ζευγών κλειδί‑τιμή με χρήση regular expressions.

Κάθε μία από αυτές τις επεκτάσεις βασίζεται στις βασικές έννοιες που καλύψαμε: φόρτωση εικόνων για OCR, εξαγωγή κειμένου, μετατροπή σε JSON και αποθήκευση του JSON στο δίσκο.

---

### Συμπέρασμα

Σε αυτό το **c# OCR tutorial** περάσαμε από κάθε βήμα που απαιτείται για να **φορτώσουμε εικόνα για OCR**, **να εξάγουμε κείμενο**, να μετατρέψουμε το αποτέλεσμα σε **OCR image to JSON** payload, και τελικά να **γράψουμε JSON σε αρχείο**. Το πλήρες παράδειγμα κώδικα είναι έτοιμο να ενσωματωθεί σε οποιοδήποτε .NET project, και οι εξηγήσεις σας δίνουν το πλαίσιο που χρειάζεστε για να προσαρμόσετε τη λύση σε πραγματικά σενάρια.

Δοκιμάστε το με το δικό σας σύνολο αποδείξεων ή τιμολογίων — πειραματιστείτε με την προεπεξεργασία εικόνας, δοκιμάστε διαφορετικές γλώσσες, και παρακολουθήστε το JSON να μεγαλώνει. Αν αντιμετωπίσετε δυσκολίες, επιστρέψτε στον πίνακα προβλημάτων ή αφήστε ένα σχόλιο παρακάτω. Καλό προγραμματισμό!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}