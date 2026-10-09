---
category: general
date: 2026-02-11
description: Μετατρέψτε μια εικόνα OCR σε JSON με C#. Μάθετε πώς να εξάγετε κείμενο
  από εικόνα, να διαβάζετε αρχείο εικόνας με C#, να μορφοποιείτε την έξοδο JSON και
  να κάνετε όμορφη εκτύπωση του JSON σε C# με το Aspose.OCR.
draft: false
keywords:
- ocr image to json
- extract text from image
- read image file c#
- format json output
- pretty print json c#
language: el
og_description: Μετατρέψτε μια εικόνα OCR σε JSON σε C#. Αυτός ο οδηγός δείχνει πώς
  να εξάγετε κείμενο από εικόνα, να διαβάσετε αρχείο εικόνας σε C#, να μορφοποιήσετε
  την έξοδο JSON και να εκτυπώσετε όμορφα το JSON σε C# χρησιμοποιώντας το Aspose.OCR.
og_title: OCR εικόνα σε JSON με C# – Πλήρης Οδηγός Βήμα‑βήμα
tags:
- OCR
- C#
- JSON
title: OCR εικόνα σε JSON με C# – Πλήρης Οδηγός Βήμα‑Βήμα
url: /el/net/text-recognition/ocr-image-to-json-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ocr εικόνας σε json σε C# – Πλήρης Οδηγός Βήμα‑βήμα

Έχετε ποτέ χρειαστεί να **ocr image to json** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη να επιλέξετε ή πώς να αποκτήσετε ένα ωραία μορφοποιημένο αποτέλεσμα; Δεν είστε μόνοι. Σε πολλές πραγματικές εφαρμογές—σάρωση αποδείξεων, επαλήθευση ταυτότητας ή απλή αρχειοθέτηση εγγράφων—θα θέλετε να εξάγετε κείμενο από μια εικόνα και να καταλήξετε με ένα καθαρό JSON payload που οι επόμενες υπηρεσίες μπορούν να καταναλώσουν.

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία: από την ανάγνωση ενός αρχείου εικόνας σε C# μέχρι την εξαγωγή του κειμένου με το Aspose.OCR, στη συνέχεια την αίτηση στην μηχανή για δομημένη έξοδο JSON, και τέλος την όμορφη εκτύπωση (pretty‑printing) του JSON ώστε να είναι αναγνώσιμο από άνθρωπο. Στο τέλος θα έχετε ένα αυτόνομο, έτοιμο για παραγωγή snippet που μπορείτε να ενσωματώσετε σε οποιοδήποτε .NET project.  

Θα αγγίξουμε επίσης κοινά προβλήματα (όπως η έλλειψη πακέτων γλώσσας) και θα δείξουμε μερικές γρήγορες παραλλαγές—π.χ., αλλαγή σε έξοδο XML ή διαχείριση PDF πολλαπλών σελίδων. Δεν απαιτείται εξωτερική τεκμηρίωση· όλα όσα χρειάζεστε είναι εδώ.

## Τι Θα Χρειαστείτε

- **.NET 6+** (ο κώδικας λειτουργεί επίσης με .NET Framework 4.7+)
- **Aspose.OCR for .NET** – εγκατάσταση μέσω NuGet (`Install-Package Aspose.OCR`)
- Ένα δείγμα εικόνας (π.χ., `receipt.png`) τοποθετημένο κάπου που μπορείτε να αναφέρετε
- Βασική εξοικείωση με τη σύνταξη C# (αν έχετε γράψει ένα “Hello World” πριν, είστε εντάξει)

> *Pro tip:* Αν βρίσκεστε σε CI server, ορίστε `AutomaticResourceDownload = true` ώστε το Aspose να κατεβάζει τα δεδομένα γλώσσας αυτόματα—χωρίς χειροκίνητη διαχείριση DLL.

## Βήμα 1: Ανάγνωση αρχείου εικόνας C# και δημιουργία της μηχανής OCR  

Το πρώτο που κάνουμε είναι να φορτώσουμε την εικόνα από το δίσκο. Η χρήση του `System.Drawing.Image` κρατά τον κώδικα σύντομο και λειτουργεί για PNG, JPEG, BMP, ακόμη και πολυ‑σελίδες TIFF (η μηχανή θα επιλέξει την πρώτη σελίδα εξ ορισμού).

```csharp
using System.Drawing;          // For Image
using Aspose.OCR;              // Core OCR classes
using Aspose.OCR.Models;       // Language and output enums
using System.Text.Json;        // JSON parsing & pretty‑print

// 1️⃣ Configure the OCR engine – this is where we tell Aspose what language we expect
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,          // extract text from image in English
    AutomaticResourceDownload = true,        // auto‑download language packs if missing
    OutputFormat = OcrOutputFormat.Json      // ask for JSON rather than plain text
};
```

**Γιατί είναι σημαντικό:**  
- `AutomaticResourceDownload` αποτρέπει σφάλματα χρόνου εκτέλεσης όταν το αρχείο γλώσσας Αγγλικών δεν είναι τοπικά διαθέσιμο.  
- Ορίζοντας `OutputFormat` σε `Json` σημαίνει ότι η μηχανή ήδη κάνει το βαρέως βάρους μετασχηματισμό των ακατέργαστων αποτελεσμάτων OCR σε δομημένο αντικείμενο—χωρίς ανάγκη χειροκίνητης ανάλυσης συμβολοσειρών.

## Βήμα 2: Εκτέλεση OCR και λήψη εξόδου JSON  

Τώρα τροφοδοτούμε το φορτωμένο bitmap στη μηχανή. Η μέθοδος `Recognize` επιστρέφει ένα `OcrResult` που περιέχει μια ιδιότητα `Text` με το JSON string.

```csharp
// 2️⃣ Load the image you want to process
using (var receiptImage = Image.FromFile(@"C:\Images\receipt.png"))
{
    // 3️⃣ Perform OCR – this call blocks until the engine finishes
    var ocrResult = ocrEngine.Recognize(receiptImage);

    // 4️⃣ The OCR engine gave us JSON straight away
    string rawJson = ocrResult.Text;
    
    // Optional: write the raw JSON to a file for debugging
    System.IO.File.WriteAllText(@"C:\Temp\ocr_raw.json", rawJson);
}
```

**Περίπτωση άκρης:** Αν η εικόνα είναι κατεστραμμένη ή η διαδρομή είναι λανθασμένη, το `Image.FromFile` ρίχνει `FileNotFoundException`. Τυλίξτε το μπλοκ σε `try/catch` αν αναμένετε ασταθείς εισόδους.

## Βήμα 3: Ανάλυση και μορφοποίηση του JSON – pretty‑print JSON C#  

Το ακατέργαστο JSON από τη μηχανή OCR είναι συμπαγές και δύσκολο στην ανάγνωση. Χρησιμοποιώντας το `System.Text.Json` μπορούμε να το αποσαφηνίσουμε (deserialize) σε ένα `JsonDocument`, μετά να το ξανα‑σειράσουμε (re‑serialize) με εσοχές.

```csharp
// 5️⃣ Parse the JSON string into a DOM-like structure
using var jsonDoc = JsonDocument.Parse(rawJson);

// 6️⃣ Pretty‑print with indentation (2 spaces by default)
string prettyJson = JsonSerializer.Serialize(
    jsonDoc.RootElement,
    new JsonSerializerOptions { WriteIndented = true });

// 7️⃣ Output to console – you could also send this to an API or a file
Console.WriteLine(prettyJson);

// 8️⃣ Save the pretty JSON for later use
System.IO.File.WriteAllText(@"C:\Temp\ocr_pretty.json", prettyJson);
```

**Τι θα δείτε:**  

```json
{
  "Lines": [
    {
      "Text": "Store Name",
      "BoundingBox": { "X": 12, "Y": 5, "Width": 150, "Height": 20 }
    },
    {
      "Text": "Total: $23.45",
      "BoundingBox": { "X": 12, "Y": 200, "Width": 100, "Height": 20 }
    }
  ],
  "Language": "English",
  "Confidence": 0.96
}
```

Το JSON τώρα περιλαμβάνει κείμενο γραμμή‑με‑γραμμή, περιοριστικά πλαίσια (bounding boxes), ανιχνευμένη γλώσσα και βαθμό εμπιστοσύνης—τέλειο για τροφοδοσία σε downstream analytics ή σε UI component.

## Βήμα 4: Bonus – Αλλαγή μορφής εξόδου ή γλώσσας  

Αν ποτέ χρειαστείτε **format json output** ως XML ή θέλετε να κάνετε OCR σε ισπανική απόδειξη, απλώς προσαρμόστε τη ρύθμιση της μηχανής:

```csharp
ocrEngine.Language = OcrLanguage.Spanish;          // extract text from image in Spanish
ocrEngine.OutputFormat = OcrOutputFormat.Xml;     // ask for XML instead of JSON
```

Το υπόλοιπο του κώδικα παραμένει ίδιο· αλλάζετε μόνο το βήμα αποσαφήνισης (deserialize) (χρησιμοποιήστε `XmlDocument` για XML).

## Πλήρες Παράδειγμα Λειτουργίας  

Συνδυάζοντας όλα, εδώ είναι ένα μόνο αρχείο που μπορείτε να αντιγράψετε‑επικολλήσετε σε μια console app:

```csharp
// ---------------------------------------------------------------
// ocr_image_to_json_demo.cs
// ---------------------------------------------------------------
using System;
using System.Drawing;
using System.Text.Json;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Configure OCR engine
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            AutomaticResourceDownload = true,
            OutputFormat = OcrOutputFormat.Json
        };

        // Path to your image – adjust as needed
        string imagePath = @"C:\Images\receipt.png";

        try
        {
            using (var receiptImage = Image.FromFile(imagePath))
            {
                var ocrResult = ocrEngine.Recognize(receiptImage);
                string rawJson = ocrResult.Text;

                // Parse & pretty‑print
                using var jsonDoc = JsonDocument.Parse(rawJson);
                string prettyJson = JsonSerializer.Serialize(
                    jsonDoc.RootElement,
                    new JsonSerializerOptions { WriteIndented = true });

                Console.WriteLine("=== Pretty‑Printed OCR JSON ===");
                Console.WriteLine(prettyJson);

                // Optional: write to file
                System.IO.File.WriteAllText(@"C:\Temp\ocr_pretty.json", prettyJson);
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Error processing image: {ex.Message}");
        }
    }
}
```

Η εκτέλεση αυτού του προγράμματος εκτυπώνει ένα ωραία εσοδιασμένο JSON payload στην κονσόλα και το αποθηκεύει στο `C:\Temp\ocr_pretty.json`. Το μπλοκ `try/catch` εξασφαλίζει ότι ακόμη και αν η εικόνα δεν μπορεί να διαβαστεί, θα λάβετε ένα σαφές μήνυμα σφάλματος αντί για σιωπηλή κατάρρευση.

## Συχνές Ερωτήσεις & Παγίδες  

- **Τι γίνεται αν το OCR επιστρέψει κενό κείμενο;**  
  Συνήθως σημαίνει ότι η εικόνα είναι πολύ θορυβώδης ή η γλώσσα δεν ταιριάζει. Δοκιμάστε να αυξήσετε την αντίθεση της εικόνας ή να αλλάξετε το `Language` σε `AutoDetect`.  

- **Μπορώ να επεξεργαστώ πολλαπλές εικόνες σε βρόχο;**  
  Απόλυτα. Τυλίξτε το μπλοκ `using (var img = Image.FromFile(...))` μέσα σε έναν βρόχο `foreach (var file in Directory.GetFiles(...))` και συλλέξτε κάθε `prettyJson` σε μια λίστα ή γράψτε τα σε ξεχωριστά αρχεία.

- **Είναι σταθερό το σχήμα (schema) του JSON;**  
  Το Aspose εγγυάται συμβατότητα προς τα πίσω για τη μορφή εξόδου `Json`, αλλά ελέγχετε πάντα το χαρακτηριστικό `Version` στην απάντηση αν στοχεύετε σε συγκεκριμένη έκδοση API.

- **Χρειάζομαι άδεια για το Aspose.OCR;**  
  Ένα δωρεάν κλειδί αξιολόγησης λειτουργεί για έως 100 σελίδες. Για παραγωγή, αγοράστε άδεια και ορίστε την με `License license = new License(); license.SetLicense("Aspose.OCR.lic");`.

## Συμπέρασμα  

Τώρα έχετε μια **πλήρη, αυτόνομη λύση για ocr image to json** σε C#. Διαβάζοντας το αρχείο εικόνας, ρυθμίζοντας τη μηχανή OCR, ζητώντας έξοδο JSON και κάνοντας pretty‑print, μπορείτε να ενσωματώσετε την εξαγωγή κειμένου σε οποιαδήποτε υπηρεσία .NET χωρίς να παλεύετε με χειροκίνητες επεμβάσεις σε συμβολοσειρές.  

Από εδώ μπορείτε να εξερευνήσετε **extract text from image** για άλλους τύπους αρχείων (PDF, πολυ‑σελίδες TIFF), να πειραματιστείτε με διαφορετικές γλώσσες ή να διοχετεύσετε το JSON σε αποθήκη NoSQL για αναλύσεις. Ο ουρανός είναι το όριο—απλώς θυμηθείτε να διαχειρίζεστε τα σφάλματα με χάρη και να παρακολουθείτε τις άδειες αν κλιμακώσετε.  

Καλή προγραμματιστική, και οι OCR pipelines σας να είναι πάντα ακριβείς!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}