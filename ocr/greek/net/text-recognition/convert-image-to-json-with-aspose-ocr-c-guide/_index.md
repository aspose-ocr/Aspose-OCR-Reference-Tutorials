---
category: general
date: 2026-01-15
description: Μετατρέψτε την εικόνα σε JSON χρησιμοποιώντας το Aspose OCR σε C#. Μάθετε
  πώς να εξάγετε κείμενο από την εικόνα, να λαμβάνετε τα πλαίσια περιορισμού σε JSON
  και να αναγνωρίζετε εικόνα απόδειξης.
draft: false
keywords:
- convert image to json
- extract text from image
- aspose ocr c# example
- recognize receipt image
- json bounding boxes
language: el
og_description: Μετατρέψτε την εικόνα σε JSON χρησιμοποιώντας το Aspose OCR σε C#.
  Οδηγός βήμα‑προς‑βήμα για την εξαγωγή κειμένου από εικόνα, την αναγνώριση εικόνας
  απόδειξης και την λήψη των πλαίσια οριοθέτησης JSON.
og_title: Μετατροπή εικόνας σε JSON με τον οδηγό Aspose OCR C#
tags:
- Aspose OCR
- C#
- JSON
- Image Processing
title: Μετατροπή εικόνας σε JSON με τον οδηγό Aspose OCR C#
url: /el/net/text-recognition/convert-image-to-json-with-aspose-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή Εικόνας σε JSON με το Aspose OCR C# Οδηγός

Έχετε ποτέ χρειαστεί να **μετατρέψετε εικόνα σε JSON** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη μπορεί να σας δώσει τόσο το ακατέργαστο κείμενο όσο και τις ακριβείς συντεταγμένες των λέξεων; Δεν είστε μόνοι. Πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν προσπαθούν να εξάγουν κείμενο από αρχεία εικόνας — ιδιαίτερα αποδείξεις — ενώ χρειάζονται επίσης ένα μηχανικά αναγνώσιμο JSON payload για επεξεργασία downstream.

Σε αυτό το tutorial θα περάσουμε από ένα πλήρες **Aspose OCR C# example** που δείχνει πώς να εξάγετε κείμενο από εικόνα, να αναγνωρίσετε εικόνα απόδειξης και να εξάγετε **JSON bounding boxes** για κάθε λέξη. Στο τέλος θα έχετε μια έτοιμη για εκτέλεση εφαρμογή κονσόλας που εκτυπώνει μια ωραία μορφοποιημένη συμβολοσειρά JSON που μπορείτε να τροφοδοτήσετε σε οποιοδήποτε API, βάση δεδομένων ή pipeline ανάλυσης.

> **Τι θα αποκομίσετε**  
> • Ένα πλήρως λειτουργικό έργο C# που **μετατρέπει εικόνα σε JSON**  
> • Κατανόηση του γιατί ενεργοποιούμε το `IncludeBoundingBoxes` (είναι το κλειδί για τα `json bounding boxes`)  
> • Συμβουλές για τη διαχείριση διαφορετικών μορφών εικόνας και γλωσσών  

Ας ξεκινήσουμε.

---

## Τι Θα Χρειαστείτε

Πριν βουτήξουμε στον κώδικα, βεβαιωθείτε ότι έχετε εγκαταστήσει τις παρακάτω προαπαιτήσεις:

- **.NET 6.0 SDK** (ή οποιαδήποτε μεταγενέστερη έκδοση) – ο κώδικας στοχεύει στο .NET 6 αλλά λειτουργεί επίσης σε .NET Framework 4.7+.  
- **Aspose.OCR for .NET** πακέτο NuGet – μπορείτε να το προσθέσετε μέσω `dotnet add package Aspose.OCR`.  
- Ένα δείγμα εικόνας απόδειξης (`receipt.jpg`) τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε από το έργο σας.  
- Visual Studio 2022, VS Code, ή οποιοδήποτε IDE προτιμάτε.

Δεν απαιτούνται άλλες εξωτερικές υπηρεσίες· όλα εκτελούνται τοπικά.

## Μετατροπή Εικόνας σε JSON – Επισκόπηση

Η βασική ιδέα είναι απλή: φορτώστε μια εικόνα, πείτε στο Aspose OCR να αναγνωρίσει τα Αγγλικά (ή οποιαδήποτε υποστηριζόμενη γλώσσα), ζητήστε του να συμπεριλάβει τα bounding boxes, και τελικά ζητήστε το αποτέλεσμα σε μορφή **JSON**. Η βιβλιοθήκη κάνει όλη τη βαριά δουλειά — OCR, ανάλυση διάταξης και σειριοποίηση JSON.

Ακολουθεί ένα διαγραμματικό υψηλού επιπέδου της ροής (φανταστείτε μια μικρή εικόνα):

```
[Image File] → Aspose OCR Engine → Recognition Options (JSON + Bounding Boxes) → JSON Output
```

Αυτό το μικρό διάγραμμα αποτυπώνει ολόκληρο το pipeline που θα υλοποιήσουμε.

## Βήμα 1: Ρύθμιση του Έργου και Εγκατάσταση του Aspose OCR

Πρώτα, δημιουργήστε ένα νέο έργο κονσόλας και προσθέστε το πακέτο Aspose OCR.

```bash
dotnet new console -n JsonOutputDemo
cd JsonOutputDemo
dotnet add package Aspose.OCR
```

> **Συμβουλή:** Αν χρησιμοποιείτε το Visual Studio, κάντε δεξί‑κλικ στο έργο → *Manage NuGet Packages* → αναζητήστε το **Aspose.OCR** και εγκαταστήστε την πιο πρόσφατη σταθερή έκδοση (τώρα 23.12).

## Βήμα 2: Φόρτωση της Εικόνας που Θέλετε να Αναγνωρίσετε

Θα χρησιμοποιήσουμε τη μέθοδο `OcrImage.FromFile` για να διαβάσουμε την εικόνα της απόδειξης. Βεβαιωθείτε ότι η διαδρομή δείχνει σε πραγματικό αρχείο· διαφορετικά θα αντιμετωπίσετε `FileNotFoundException`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // Step 2: Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

Αν η εικόνα σας βρίσκεται δίπλα στο `.csproj`, μπορείτε απλώς να χρησιμοποιήσετε `"receipt.jpg"`.

## Βήμα 3: Διαμόρφωση των OCR Options για JSON Bounding Boxes

Η μαγεία συμβαίνει όταν ενεργοποιούμε το `OutputFormat = OutputFormat.Json` **και** το `IncludeBoundingBoxes = true`. Το πρώτο λέει στο Aspose να σειριοποιήσει το αποτέλεσμα ως JSON, ενώ το δεύτερο προσθέτει `x`, `y`, `width` και `height` για κάθε λέξη — ακριβώς ό,τι χρειάζεστε για τα `json bounding boxes`.

```csharp
        // Step 3: Configure OCR options
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };
```

Μπορείτε επίσης να ρυθμίσετε το `ocrOptions.Dpi` ή το `ocrOptions.Language` αν χρειάζεστε υψηλότερη ανάλυση ή διαφορετική γλώσσα.

## Βήμα 4: Εκτέλεση της Αναγνώρισης – Εξαγωγή Κειμένου από την Εικόνα

Τώρα καλούμε το `Recognize`. Η μέθοδος επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει τη συμβολοσειρά JSON, το ακατέργαστο κείμενο και άλλα.

```csharp
        // Step 4: Perform recognition using English language and the configured options
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);
```

Αν χρειάζεται να διαχειριστείτε άλλες γλώσσες, αντικαταστήστε το `Language.English` με `Language.Spanish`, `Language.French`, κ.λπ. Το Aspose υποστηρίζει πάνω από 30 γλώσσες από το κουτί.

## Βήμα 5: Έξοδος του Αποτελέσματος – Το JSON Payload Σας

Τέλος, εκτυπώνουμε το JSON στην κονσόλα. Σε μια πραγματική εφαρμογή, πιθανότατα θα το γράφατε σε αρχείο ή θα το στέλνατε σε μια υπηρεσία.

```csharp
        // Step 5: Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

Η εκτέλεση του προγράμματος θα πρέπει να παράγει ένα έγγραφο JSON παρόμοιο με το παρακάτω απόσπασμα.

```json
{
  "Text": "Total $12.34\nDate 01/01/2024",
  "Words": [
    {
      "Text": "Total",
      "BoundingBox": { "X": 45, "Y": 112, "Width": 60, "Height": 20 }
    },
    {
      "Text": "$12.34",
      "BoundingBox": { "X": 110, "Y": 112, "Width": 70, "Height": 20 }
    },
    {
      "Text": "Date",
      "BoundingBox": { "X": 45, "Y": 140, "Width": 50, "Height": 20 }
    },
    {
      "Text": "01/01/2024",
      "BoundingBox": { "X": 100, "Y": 140, "Width": 120, "Height": 20 }
    }
  ]
}
```

Παρατηρήστε πώς κάθε λέξη τώρα φέρει το **JSON bounding box** — ιδανικό για τροφοδοσία σε UI overlay ή downstream parser.

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω βρίσκεται το πλήρες, έτοιμο για αντιγραφή πρόγραμμα. Χωρίς κρυφά μέρη, χωρίς εξωτερικές κλήσεις — μόνο καθαρό C#.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");

        // 3️⃣ Configure OCR options to get detailed JSON output with word positions
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };

        // 4️⃣ Perform recognition using English language and the configured options
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);

        // 5️⃣ Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

> **Προσοχή:**  
> • **Σφάλματα διαδρομής αρχείου** – ελέγξτε ξανά τη θέση της εικόνας.  
> • **Λείπει το πακέτο NuGet** – βεβαιωθείτε ότι το `Aspose.OCR` είναι αναφορά.  
> • **Μη υποστηριζόμενες μορφές εικόνας** – χρησιμοποιήστε JPEG, PNG, BMP ή TIFF για τα καλύτερα αποτελέσματα.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Μπορώ να μετατρέψω μια **σελίδα PDF** σε JSON αντί για JPEG;

Ναι. Μετατρέψτε πρώτα τη σελίδα PDF σε εικόνα (π.χ., χρησιμοποιώντας `Aspose.PDF`), έπειτα τροφοδοτήστε αυτή την εικόνα στο ίδιο OCR pipeline. Η έξοδος JSON θα είναι ίδια επειδή το βήμα OCR ενδιαφέρεται μόνο για τα raster δεδομένα.

### Τι γίνεται αν η απόδειξη είναι θολή;

Αυξήστε το DPI στο `ocrOptions`. Για παράδειγμα:

```csharp
ocrOptions.Dpi = 300; // higher DPI improves accuracy on low‑quality scans
```

Υψηλότερο DPI μπορεί να αυξήσει τη χρήση μνήμης, οπότε ισορροπήστε την ποιότητα με την απόδοση.

### Χρειάζομαι **πολλαπλές γλώσσες** στην ίδια απόδειξη (π.χ., Αγγλικά + Ισπανικά).

Μπορείτε να περάσετε έναν πίνακα γλωσσών:

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, new[] { Language.English, Language.Spanish }, ocrOptions);
```

Το Aspose θα προσπαθήσει να αναγνωρίσει κάθε γλώσσα με τη συγκεκριμένη σειρά.

### Πώς μπορώ να γράψω το JSON σε αρχείο;

Απλώς αντικαταστήστε τη γραμμή `Console.WriteLine` με:

```csharp
System.IO.File.WriteAllText("receipt.json", ocrResult.Json);
```

Τώρα έχετε ένα μόνιμο αρχείο που μπορείτε να στείλετε σε άλλες υπηρεσίες.

## Οπτική Σύνοψη

![παράδειγμα μετατροπής εικόνας σε json](convert-image-to-json.png "παράδειγμα μετατροπής εικόνας σε json")

*Το στιγμιότυπο δείχνει την έξοδο της κονσόλας του JSON payload μετά την εκτέλεση της επίδειξης.*

## Συμπέρασμα

Μόλις σας δείξαμε πώς να **μετατρέψετε εικόνα σε JSON** χρησιμοποιώντας το Aspose OCR σε C#. Με τη διαμόρφωση του `OutputFormat` και του `IncludeBoundingBoxes`, μπορείτε να **εξάγετε κείμενο από εικόνα**, να **αναγνωρίσετε εικόνα απόδειξης**, και να αποκτήσετε ακριβή **JSON bounding boxes** για κάθε λέξη. Ο πλήρης, εκτελέσιμος κώδικας βρίσκεται στο απόσπασμα παραπάνω, ώστε να τον ενσωματώσετε σε οποιοδήποτε έργο .NET τώρα.

Τι ακολουθεί; Δοκιμάστε να τροφοδοτήσετε το JSON σε έναν front‑end viewer που επισημαίνει κάθε λέξη, ή στείλτε τα δεδομένα σε μοντέλο μηχανικής μάθησης που ταξινομεί τα στοιχεία γραμμής στις αποδείξεις. Μπορείτε επίσης να πειραματιστείτε με άλλες γλώσσες, υψηλότερες ρυθμίσεις DPI, ή επεξεργασία πολλαπλών εικόνων σε batch σε βρόχο.

Αν αντιμετωπίσετε προβλήματα, θυμηθείτε τις συμβουλές για τις διαδρομές αρχείων, το DPI και τις σειρές γλωσσών. Μη διστάσετε να αφήσετε ένα σχόλιο ή να ανοίξετε ένα ζήτημα στο GitHub repo που θα δημιουργήσετε για αυτήν την επίδειξη. Καλή προγραμματιστική δουλειά, και απολαύστε τη μετατροπή εικόνων σε δομημένο JSON!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}