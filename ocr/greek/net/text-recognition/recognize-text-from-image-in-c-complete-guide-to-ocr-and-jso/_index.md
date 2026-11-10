---
category: general
date: 2026-01-10
description: Μάθετε πώς να αναγνωρίζετε κείμενο από εικόνα, να εξάγετε τις συντεταγμένες
  του κειμένου και να μετατρέπετε την απόδειξη σε JSON χρησιμοποιώντας το Aspose OCR
  σε C#. Οδηγός βήμα‑βήμα.
draft: false
keywords:
- recognize text from image
- how to extract text
- extract text coordinates
- convert receipt to json
language: el
og_description: Αναγνώριση κειμένου από εικόνα σε C# χρησιμοποιώντας Aspose OCR. Αυτός
  ο οδηγός δείχνει πώς να εξάγετε κείμενο, να λάβετε συντεταγμένες και να μετατρέψετε
  την απόδειξη σε JSON.
og_title: Αναγνώριση κειμένου από εικόνα – Πλήρης οδηγός OCR σε C#
tags:
- OCR
- C#
- Aspose
title: αναγνώριση κειμένου από εικόνα σε C# – Πλήρης οδηγός για OCR και JSON
url: /el/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# αναγνώριση κειμένου από εικόνα – Πλήρες Tutorial C# OCR

Έχετε χρειαστεί ποτέ να αναγνωρίσετε κείμενο από εικόνα αλλά δεν ήξερατε ποια βιβλιοθήκη να επιλέξετε; Δεν είστε μόνοι. Σε πολλές πραγματικές εφαρμογές—διαχειριστές εξόδων, σαρωτές αποδείξεων ή αρχειοθέτες εγγράφων—η αξιόπιστη εξαγωγή κειμένου είναι το πρώτο εμπόδιο.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα **πώς να εξάγουμε κείμενο**, πώς να πάρουμε τα πλαίσια οριοθέτησής του και τελικά **πώς να μετατρέψουμε την απόδειξη σε JSON** χρησιμοποιώντας το Aspose.OCR για .NET. Στο τέλος θα έχετε ένα αυτόνομο έργο C# που παίρνει μια φωτογραφία απόδειξης και δημιουργεί ένα καθαρό αρχείο JSON με βαθμούς εμπιστοσύνης και συντεταγμένες.

## Τι Θα Χρειαστείτε

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τα εξής στο μηχάνημά σας:

- **.NET 6.0 SDK** (ή οποιαδήποτε νεότερη έκδοση). Παλαιότερα frameworks λειτουργούν επίσης, αλλά το .NET 6 είναι η ιδανική επιλογή για σύγχρονες βιβλιοθήκες.
- **Visual Studio 2022** ή VS Code με την επέκταση C#.
- **Aspose.OCR for .NET** πακέτο NuGet (`Aspose.OCR` και `Aspose.OCR.Output`). Μπορείτε να το εγκαταστήσετε μέσω του Package Manager Console:

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Output
```

- Ένα δείγμα εικόνας απόδειξης (π.χ. `receipt.jpg`) τοποθετημένο σε φάκελο που θα αναφέρετε αργότερα.

Αυτό είναι όλο—χωρίς επιπλέον SDKs, χωρίς εγγενή binaries, μόνο καθαρός διαχειριζόμενος κώδικας.

## Βήμα 1: Δημιουργία Νέου Console Project

Πρώτα απ’ όλα, δημιουργήστε μια console εφαρμογή. Είναι ο πιο γρήγορος τρόπος για να δοκιμάσετε OCR χωρίς επιπλέον UI.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in later.
        }
    }
}
```

> **Συμβουλή:** Κρατήστε τον φάκελο του έργου οργανωμένο· δημιουργήστε έναν υπο‑φάκελο με όνομα `Resources` και τοποθετήστε εκεί το `receipt.jpg`. Έτσι η διαχείριση διαδρομών γίνεται πιο απλή.

## Βήμα 2: Φόρτωση της Εικόνας Απόδειξης

Τώρα θα **αναγνωρίσουμε κείμενο από εικόνα**. Το πρώτο βήμα είναι να κατευθύνουμε τη μηχανή OCR στο αρχείο.

```csharp
// Inside Main()
string imagePath = @"Resources/receipt.jpg";
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// Initialise the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    Image = ImageStream.FromFile(imagePath)
};

Console.WriteLine("✅ Image loaded successfully.");
```

Γιατί τυλίγουμε τη φόρτωση σε έναν απλό έλεγχο ύπαρξης; Επειδή σε παραγωγή συχνά αντιμετωπίζετε ανεβάσματα χρηστών που μπορεί να λείπουν ή να είναι κατεστραμμένα. Η έγκαιρη ανίχνευση του προβλήματος αποτρέπει cryptic exceptions αργότερα.

## Βήμα 3: Εκτέλεση OCR – **αναγνώριση κειμένου από εικόνα**

Με την εικόνα στη μνήμη, ζητάμε από το Aspose να **αναγνωρίσει κείμενο από εικόνα**. Η λειτουργία αυτή είναι συγχρονική και επιστρέφει ένα πλούσιο σύνολο αποτελεσμάτων.

```csharp
// Still inside Main()
try
{
    ocrEngine.Recognize();
    Console.WriteLine("🧠 OCR completed.");
}
catch (Exception ex)
{
    Console.WriteLine($"❗ OCR failed: {ex.Message}");
    return;
}
```

Στο παρασκήνιο το Aspose τρέχει ένα νευρωνικό δίκτυο εκπαιδευμένο σε εκατομμύρια χαρακτήρες. Η μηχανή γεμίζει τα `ocrEngine.Text`, `ocrEngine.RecognitionResult` και μια συλλογή αντικειμένων `OcrRegion` που περιέχουν συντεταγμένες. Αυτό είναι ακριβώς ό,τι χρειαζόμαστε για το επόμενο βήμα.

## Βήμα 4: **πώς να εξάγετε κείμενο** – Λήψη της ακατέργαστης συμβολοσειράς

Αν σας ενδιαφέρει μόνο το απλό κείμενο (π.χ. για γρήγορη αναζήτηση), μπορείτε να το πάρετε κατευθείαν από τη μηχανή:

```csharp
string plainText = ocrEngine.Text;
Console.WriteLine("\n--- Extracted Text ---");
Console.WriteLine(plainText);
```

Θα παρατηρήσετε αλλαγές γραμμής όπου το OCR ανίχνευσε όρια παραγράφων. Σε πολλές περιπτώσεις σάρωσης αποδείξεων η ακατέργαστη συμβολοσειρά αρκεί για να εξαχθούν τα σύνολα, οι ημερομηνίες ή τα ονόματα προμηθευτών με απλά regex.

## Βήμα 5: **συντεταγμένες κειμένου** – Πλαίσια οριοθέτησης για κάθε λέξη

Συχνά χρειάζεται να ξέρετε *πού* στην εικόνα βρίσκεται ένα συγκεκριμένο κομμάτι κειμένου—π.χ. για να επισημάνετε το συνολικό ποσό σε UI. Το Aspose μας παρέχει αυτό μέσω των αντικειμένων `OcrRegion`.

```csharp
Console.WriteLine("\n--- Text Coordinates (extract text coordinates) ---");
foreach (var region in ocrEngine.RecognitionResult.Regions)
{
    // Each region represents a word or a line depending on the engine settings.
    string word = region.Text;
    var bounds = region.BoundingBox; // X, Y, Width, Height
    Console.WriteLine($"Word: \"{word}\" | Box: X={bounds.X}, Y={bounds.Y}, W={bounds.Width}, H={bounds.Height}");
}
```

Παρατηρήστε ότι κάνουμε βρόχο πάνω στις **συντεταγμένες κειμένου** για κάθε αναγνωρισμένο τμήμα. Οι συντεταγμένες είναι σχετικές με την αρχική εικόνα, ώστε να μπορείτε να τις τοποθετήσετε σε ένα graphics canvas ή σε στοιχείο HTML `<canvas>`.

## Βήμα 6: **μετατροπή απόδειξης σε JSON** – Αποθήκευση λεπτομερών αποτελεσμάτων

Τώρα έρχεται το κομμάτι που ενώνει τα πάντα: θέλουμε μια δομή μηχανής‑αναγνώσιμη που να περιλαμβάνει το κείμενο, τους βαθμούς εμπιστοσύνης και τα πλαίσια οριοθέτησης. Το Aspose παρέχει την κλάση `JsonSaveOptions` που κάνει αυτή τη δουλειά παιχνιδάκι.

```csharp
// Define where the JSON will be saved
string jsonPath = @"Resources/receipt.json";

// Configure JSON options to keep confidence and bounding boxes
JsonSaveOptions jsonOptions = new JsonSaveOptions
{
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};

// Save the OCR result
ocrEngine.Save(jsonPath, jsonOptions);
Console.WriteLine($"\n💾 Detailed OCR results saved to {jsonPath}");
```

Το παραγόμενο αρχείο μοιάζει κάπως έτσι (συνοπτικό για συντομία):

```json
{
  "Regions": [
    {
      "Text": "Store",
      "Confidence": 0.99,
      "BoundingBox": { "X": 45, "Y": 120, "Width": 80, "Height": 20 }
    },
    {
      "Text": "Total",
      "Confidence": 0.97,
      "BoundingBox": { "X": 300, "Y": 560, "Width": 70, "Height": 22 }
    }
    // ... more regions ...
  ]
}
```

Τώρα έχετε ένα **αποτέλεσμα μετατροπής απόδειξης σε JSON** που μπορεί να τροφοδοτηθεί σε downstream υπηρεσίες—π.χ. APIs αναφοράς εξόδων, pipelines analytics ή ακόμη και ένα απλό UI που σχεδιάζει ορθογώνια γύρω από κάθε λέξη.

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα τα κομμάτια, εδώ είναι το πλήρες `Program.cs` που μπορείτε να αντιγράψετε‑επικολλήσετε στο έργο σας:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image
            // -------------------------------------------------
            string imagePath = @"Resources/receipt.jpg";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found at {imagePath}");
                return;
            }

            OcrEngine ocrEngine = new OcrEngine
            {
                Image = ImageStream.FromFile(imagePath)
            };
            Console.WriteLine("✅ Image loaded.");

            // -------------------------------------------------
            // 2️⃣ Run OCR – recognize text from image
            // -------------------------------------------------
            try
            {
                ocrEngine.Recognize();
                Console.WriteLine("🧠 OCR completed.");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❗ OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 3️⃣ Extract plain text (how to extract text)
            // -------------------------------------------------
            Console.WriteLine("\n--- Extracted Text ---");
            Console.WriteLine(ocrEngine.Text);

            // -------------------------------------------------
            // 4️⃣ Get coordinates (extract text coordinates)
            // -------------------------------------------------
            Console.WriteLine("\n--- Text Coordinates ---");
            foreach (var region in ocrEngine.RecognitionResult.Regions)
            {
                var box = region.BoundingBox;
                Console.WriteLine($"Word: \"{region.Text}\" | Box: X={box.X}, Y={box.Y}, W={box.Width}, H={box.Height}");
            }

            // -------------------------------------------------
            // 5️⃣ Save detailed JSON (convert receipt to json)
            // -------------------------------------------------
            string jsonPath = @"Resources/receipt.json";
            JsonSaveOptions jsonOptions = new JsonSaveOptions
            {
                IncludeConfidence = true,
                IncludeBoundingBoxes = true
            };
            ocrEngine.Save(jsonPath, jsonOptions);
            Console.WriteLine($"\n💾 JSON saved at {jsonPath}");
        }
    }
}
```

Τρέξτε το πρόγραμμα (`dotnet run`) και παρακολουθήστε την έξοδο στην κονσόλα. Ανοίξτε το `Resources/receipt.json` για να επαληθεύσετε τη δομή.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

- **Τι γίνεται αν η εικόνα είναι θολή;**  
  Το Aspose OCR αποδίδει καλύτερα με 300 dpi ή περισσότερο. Αν λάβετε χαμηλούς βαθμούς εμπιστοσύνης, σκεφτείτε να εφαρμόσετε φίλτρο sharpening πριν περάσετε την εικόνα στη μηχανή.

- **Μπορώ να αναγνωρίσω πολλαπλές γλώσσες;**  
  Ναι. Ορίστε `ocrEngine.Language = Language.English | Language.Spanish;` πριν καλέσετε το `Recognize()`.

- **Πώς περιορίζω την έξοδο μόνο σε αριθμούς (π.χ. σύνολα);**  
  Αφού έχετε το απλό κείμενο, τρέξτε ένα regex όπως `\d+\.\d{2}` στο `ocrEngine.Text`. Επειδή ήδη έχουμε τις συντεταγμένες, μπορείτε να αντιστοιχίσετε το ταιριασμένο string στην περιοχή του για οπτική επισήμανση.

- **Μπορεί να προσαρμοστεί η μορφή JSON;**  
  Η κλάση `JsonSaveOptions` εκθέτει μια σειρά σημαιών. Αν χρειάζεστε εντελώς προσαρμοσμένο σχήμα, μπορείτε να διασχίσετε τα `ocrEngine.RecognitionResult.Regions` και να σειριοποιήσετε τα αντικείμενα μόνοι σας με `System.Text.Json`.

## Συμπέρασμα

Δείξαμε πώς να **αναγνωρίσετε κείμενο από εικόνα** σε C# χρησιμοποιώντας το Aspose.OCR, **πώς να εξάγετε κείμενο**, να πάρετε **συντεταγμένες κειμένου**, και τέλος να **μετατρέψετε την απόδειξη σε JSON**. Η όλη ροή βρίσκεται σε μια μόνο, εύκολη στην εκτέλεση console εφαρμογή, καθιστώντας την ιδανική για πρωτότυπα ή ως δομικό στοιχείο σε μεγαλύτερα συστήματα.

Τι επόμενα βήματα; Δοκιμάστε να τροφοδοτήσετε το JSON σε ένα front‑end που σχεδιάζει τα πλαίσια, ή ενσωματώστε το αποτέλεσμα σε υπηρεσία αναφοράς εξόδων. Μπορείτε επίσης να πειραματιστείτε με διαφορετικές μορφές εικόνας (PNG, TIFF) ή να επεξεργαστείτε μαζικά έναν φάκελο αποδείξεων.

Έχετε περισσότερες ερωτήσεις για OCR, Aspose ή διαχείριση JSON; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική δουλειά!

![Παράδειγμα εικόνας απόδειξης για αναγνώριση κειμένου από εικόνα](receipt.jpg "Παράδειγμα εικόνας απόδειξης")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}