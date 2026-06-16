---
category: general
date: 2026-02-17
description: Πώς να εκτελέσετε OCR σε C# και να μετατρέψετε γρήγορα μια εικόνα σε
  JSON. Ακολουθήστε αυτό το σεμινάριο OCR σε C# για να εξάγετε κείμενο από εικόνες
  και να αποθηκεύσετε τη διάταξη ως JSON.
draft: false
keywords:
- how to perform OCR
- convert image to json
- c# ocr tutorial
- extract text image c#
- load image file c#
language: el
og_description: Πώς να εκτελέσετε OCR σε C#; Αυτός ο οδηγός σας δείχνει πώς να μετατρέψετε
  μια εικόνα σε JSON, να εξάγετε κείμενο από την εικόνα σε C# και να φορτώσετε αρχείο
  εικόνας για OCR.
og_title: Πώς να εκτελέσετε OCR σε C# – Μετατροπή εικόνας σε JSON
tags:
- OCR
- C#
- Aspose
title: Πώς να εκτελέσετε OCR σε C# – Οδηγός μετατροπής εικόνας σε JSON
url: /el/net/text-recognition/how-to-perform-ocr-in-c-convert-image-to-json-guide/
---

c#"*". Translate: "*Κείμενο alt εικόνας: "διάγραμμα ροής εργασίας εκτέλεσης OCR που απεικονίζει τη μετατροπή εικόνας σε JSON και την εξαγωγή κειμένου από εικόνα c#"*". Keep asterisks.

Then note about placeholder.

Then "## Conclusion" heading.

Paragraph.

Now final shortcodes.

Let's craft final output.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εκτελέσετε OCR σε C# – Οδηγός Μετατροπής Εικόνας σε JSON

Έχετε αναρωτηθεί ποτέ **πώς να εκτελέσετε OCR** σε απόδειξη, τιμολόγιο ή οποιοδήποτε σαρωμένο έγγραφο χρησιμοποιώντας C#; Δεν είστε οι μόνοι. Πολλοί προγραμματιστές αντιμετωπίζουν δυσκολίες όταν πρέπει να εξάγουν κείμενο *και* να διατηρήσουν τη διάταξη χωρίς να ξοδεύουν ώρες γράφοντας προσαρμοσμένους αναλυτές.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες **c# ocr tutorial** που δείχνει ακριβώς πώς να εκτελέσετε OCR, **να μετατρέψετε εικόνα σε json**, και να αποθηκεύσετε το αποτέλεσμα για μετέπειτα ανάλυση. Στο τέλος θα έχετε μια έτοιμη‑για‑εκτέλεση console εφαρμογή που φορτώνει ένα αρχείο εικόνας σε C#, εξάγει το κείμενο και γράφει ένα λεπτομερές αρχείο JSON που περιέχει συντεταγμένες, βαθμούς εμπιστοσύνης και το ακατέργαστο κείμενο.

## Προαπαιτούμενα — Τι Θα Χρειαστεί

- .NET 6 SDK ή νεότερο (ο κώδικας λειτουργεί και σε .NET Core)  
- Visual Studio 2022 ή οποιονδήποτε επεξεργαστή προτιμάτε  
- Άδεια Aspose OCR (μπορείτε να ξεκινήσετε με δωρεάν δοκιμή)  
- Ένα δείγμα εικόνας, π.χ. `receipt.png`, τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε  

Αυτό είναι όλο—δεν απαιτούνται επιπλέον πακέτα NuGet εκτός από `Aspose.OCR`. Αν έχετε αυτά τα στοιχεία, είστε έτοιμοι να ξεκινήσετε.

## Πώς να Εκτελέσετε OCR και να Λάβετε Έξοδο JSON

Ο πυρήνας του **πώς να εκτελέσετε OCR** με το Aspose είναι απλός: δημιουργείτε ένα `OcrEngine`, του παρέχετε ένα stream εικόνας, καλείτε το `Recognize`, και στη συνέχεια σειριοποιείτε το `OcrResult` σε JSON. Ας το αναλύσουμε βήμα‑βήμα.

### Step 1: Εγκατάσταση του Πακέτου Aspose OCR NuGet

Ανοίξτε το τερματικό σας στον φάκελο του έργου και εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Χρησιμοποιήστε τη σημαία `--version` για να κλειδώσετε στην πιο πρόσφατη σταθερή έκδοση (π.χ., `23.9.0`). Αυτό διασφαλίζει ότι η κατασκευή σας είναι αναπαραγώγιμη.

### Step 2: Δημιουργία του Σκελετού του Console Project

Αν δεν έχετε ήδη έργο, δημιουργήστε ένα:

```bash
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo
```

Τώρα έχετε ένα αρχείο `Program.cs` έτοιμο για τον κώδικα που θα **φορτώσει αρχείο εικόνας c#** και θα ξεκινήσει τη διαδικασία OCR.

### Step 3: Γράψτε τον Πλήρη Κώδικα OCR‑to‑JSON

Παρακάτω είναι το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα. Αντιγράψτε‑και‑επικολλήστε το στο `Program.cs`. Κάθε γραμμή είναι σχολιασμένη ώστε να βλέπετε *γιατί* κάθε μέρος είναι σημαντικό.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonOutput
{
    static void Main()
    {
        // ---------------------------------------------------------
        // 1️⃣  Initialize the OCR engine – this object holds
        //     language settings, recognition options, etc.
        // ---------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---------------------------------------------------------
        // 2️⃣  Load the image you want to analyze.
        //     This demonstrates **load image file c#** in a clean way.
        // ---------------------------------------------------------
        // Replace the path with the actual location of your receipt.png
        string imagePath = Path.Combine(
            Environment.CurrentDirectory, "receipt.png");
        ImageStream image = ImageStream.FromFile(imagePath);

        // ---------------------------------------------------------
        // 3️⃣  Perform the recognition.
        //     The engine returns an OcrResult containing text,
        //     confidence scores, and layout information.
        // ---------------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // ---------------------------------------------------------
        // 4️⃣  Convert the result to a detailed JSON string.
        //     This is the heart of **convert image to json**.
        // ---------------------------------------------------------
        string jsonResult = ocrResult.ToJson();

        // ---------------------------------------------------------
        // 5️⃣  Save the JSON to disk – you can later import this into
        //     databases, analytics pipelines, or UI components.
        // ---------------------------------------------------------
        string jsonPath = Path.Combine(
            Environment.CurrentDirectory, "receipt.json");
        File.WriteAllText(jsonPath, jsonResult);

        // ---------------------------------------------------------
        // 6️⃣  Let the user know we’re done.
        // ---------------------------------------------------------
        Console.WriteLine("JSON with layout saved to " + jsonPath);
    }
}
```

#### Τι Κάνει ο Κώδικας

| Βήμα | Γιατί Είναι Σημαντικό |
|------|-----------------------|
| **Initialize OcrEngine** | Ρυθμίζει τη προεπιλεγμένη γλώσσα (Αγγλικά) και προετοιμάζει τα εσωτερικά μοντέλα. |
| **Load image file** | Η χρήση του `ImageStream.FromFile` διασφαλίζει ότι η εικόνα διαβάζεται σε μορφή που περιμένει το Aspose. |
| **Recognize** | Η βαριά δουλειά—ανάλυση εικονοστοιχείων, διαχωρισμός χαρακτήρων και αναζήτηση σε λεξικό. |
| **ToJson** | Παράγει δομημένη έξοδο που περιλαμβάνει πλαίσια οριοθέτησης, βαθμούς εμπιστοσύνης και ακατέργαστο κείμενο. |
| **WriteAllText** | Αποθηκεύει το JSON ώστε να μπορείτε να το μοιραστείτε με άλλες υπηρεσίες. |
| **Console.WriteLine** | Παρέχει άμεση ανατροφοδότηση—χρήσιμο όταν τρέχετε από τερματικό. |

> **Watch out:** Αν η εικόνα σας είναι μεγάλη, σκεφτείτε να την αλλάξετε σε μικρότερο μέγεθος πρώτα για να βελτιώσετε την ταχύτητα και τη χρήση μνήμης. Το Aspose παρέχει μεθόδους `Resize` που μπορείτε να καλέσετε στο `ImageStream`.

### Step 4: Εκτελέστε την Εφαρμογή και Επαληθεύστε το Αποτέλεσμα

Από το τερματικό:

```bash
dotnet run
```

Θα πρέπει να δείτε:

```
JSON with layout saved to C:\Path\To\OcrJsonDemo\receipt.json
```

Ανοίξτε το `receipt.json` σε οποιονδήποτε επεξεργαστή· θα βρείτε κάτι σαν:

```json
{
  "Pages": [
    {
      "Blocks": [
        {
          "Text": "Total: $12.34",
          "Confidence": 0.98,
          "BoundingBox": { "X": 120, "Y": 340, "Width": 150, "Height": 30 }
        }
      ]
    }
  ]
}
```

Αυτό το JSON καταγράφει **extract text image c#** μαζί με μεταδεδομένα διάταξης, ιδανικό για επεξεργασία σε επόμενα στάδια.

## Convert Image to JSON – Πέρα από τα Βασικά

Τώρα που ξέρετε **πώς να εκτελέσετε OCR**, ας εξερευνήσουμε μερικές παραλλαγές που μπορεί να χρειαστείτε σε πραγματικά έργα.

### Διαχείριση Πολλαπλών Σελίδων

Αν η πηγή σας είναι PDF ή TIFF πολλαπλών σελίδων, απλώς κάντε βρόχο σε κάθε σελίδα:

```csharp
foreach (var pageStream in multiPageImageStreams)
{
    OcrResult result = ocrEngine.Recognize(pageStream);
    // Append each page's JSON to a master list
}
```

### Προσαρμογή Γλώσσας και Ακρίβειας

Το Aspose υποστηρίζει πάνω από 40 γλώσσες. Για να μεταβείτε στα Ισπανικά:

```csharp
ocrEngine.Language = Language.Spanish;
```

Μπορείτε επίσης να ρυθμίσετε το `ocrEngine.Settings` ώστε να ενεργοποιήσετε **αυτόματη περιστροφή**, **αφαίρεση θορύβου**, ή **διόρθωση βάσει λεξικού**—όλα αυτά βελτιώνουν την ποιότητα του JSON που λαμβάνετε.

### Αποθήκευση JSON σε Μορφή Pretty‑Printed

Αν προτιμάτε μορφοποιημένο JSON για ευκολότερη ανάγνωση:

```csharp
string prettyJson = ocrResult.ToJson(true); // true = formatted
File.WriteAllText(jsonPath, prettyJson);
```

## Load Image File C# – Συνηθισμένα Προβλήματα και Συμβουλές

Όταν **φορτώνετε αρχείο εικόνας c#**, μπορεί να αντιμετωπίσετε:

- **File not found** – Βεβαιωθείτε ότι το μονοπάτι είναι απόλυτο ή χρησιμοποιήστε `Path.Combine` με `Environment.CurrentDirectory`.  
- **Unsupported format** – Το Aspose διαχειρίζεται PNG, JPEG, BMP, TIFF και PDF. Για μορφές RAW, μετατρέψτε τις πρώτα.  
- **Large file memory pressure** – Χρησιμοποιήστε `ImageStream.FromFile(path, maxSizeInKB)` για να μειώσετε το μέγεθος κατά τη φόρτωση.

Η αντιμετώπιση αυτών των ζητημάτων νωρίς αποτρέπει cryptic exceptions αργότερα στην αλυσίδα OCR.

## Extract Text Image C# – Επαλήθευση Αποτελεσμάτων

Αφού έχετε το JSON, ίσως θέλετε μόνο το απλό κείμενο:

```csharp
var ocrResult = ocrEngine.Recognize(image);
string plainText = ocrResult.Text; // Simple string with line breaks
Console.WriteLine(plainText);
```

Αυτό το απόσπασμα δείχνει **extract text image c#** χωρίς τις λεπτομέρειες διάταξης—χρήσιμο για γρήγορες αναζητήσεις ή καταγραφή.

---

![Διάγραμμα που δείχνει τη ροή εργασίας OCR – πώς να εκτελέσετε OCR, μετατροπή εικόνας σε JSON, και εξαγωγή κειμένου από εικόνα c#](/images/ocr-workflow.png "ροή εργασίας εκτέλεσης OCR")

*Κείμενο alt εικόνας: "διάγραμμα ροής εργασίας εκτέλεσης OCR που απεικονίζει τη μετατροπή εικόνας σε JSON και την εξαγωγή κειμένου από εικόνα c#"*  

*(Η εικόνα είναι placeholder· αντικαταστήστε την με πραγματικό διάγραμμα όταν δημοσιεύετε.)*

---

## Συμπέρασμα

Καλύψαμε **πώς να εκτελέσετε OCR** σε C# από την αρχή μέχρι το τέλος, σας δείξαμε πώς να **μετατρέψετε εικόνα σε JSON**, και εξηγήσαμε τις λεπτομέρειες του **load image file c#** και του **extract text image c#**. Το πλήρες παράδειγμα κώδικα είναι έτοιμο να ενσωματωθεί σε οποιοδήποτε .NET έργο, και η έξοδος JSON σας παρέχει τόσο ακατέργαστο κείμενο όσο και ακριβή δεδομένα διάταξης για επόμενη ανάλυση.

Τι ακολουθεί; Δοκιμάστε να τροφοδοτήσετε το JSON σε μια βάση δεδομένων, να οπτικοποιήσετε τα πλαίσια οριοθέτησης σε UI, ή να συνδέσετε πολλαπλές εκτελέσεις OCR για επεξεργασία παρτίδας. Μπορείτε επίσης να πειραματιστείτε με άλλες δυνατότητες του Aspose όπως η αναγνώριση χειρόγραφου ή η ανίχνευση barcode—και τα δύο εντάσσονται φυσικά στην ίδια ροή εργασίας.

Αν αντιμετωπίσετε προβλήματα, επιστρέψτε στις συμβουλές αντιμετώπισης προβλημάτων στην ενότητα “Load Image File C#”, ή εξερευνήστε την εκτενή τεκμηρίωση του Aspose για προχωρημένες ρυθμίσεις. Καλό κώδικα και καλή διασκέδαση με τη μετατροπή εικόνων σε δομημένα δεδομένα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}