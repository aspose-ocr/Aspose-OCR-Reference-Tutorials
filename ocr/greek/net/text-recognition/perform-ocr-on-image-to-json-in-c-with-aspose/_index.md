---
category: general
date: 2026-04-08
description: Μάθετε πώς να εκτελείτε OCR σε εικόνα και να γράφετε αρχείο JSON με C#
  χρησιμοποιώντας το Aspose OCR. Αυτό το tutorial Aspose OCR C# δείχνει τη μετατροπή
  εικόνας OCR σε JSON με τιμές εμπιστοσύνης.
draft: false
keywords:
- perform OCR on image
- write JSON file C#
- OCR image to JSON
- Aspose OCR C# tutorial
language: el
og_description: Πραγματοποιήστε OCR σε εικόνα και εξάγετε τα αποτελέσματα σε αρχείο
  JSON με C#. Αυτό το σεμινάριο καλύπτει τη πλήρη ροή εργασίας Aspose OCR C#, συμπεριλαμβανομένων
  των βαθμών εμπιστοσύνης.
og_title: Διενέργεια OCR σε εικόνα σε JSON με C# – Οδηγός Aspose OCR
tags:
- Aspose
- OCR
- C#
- JSON
title: Εκτέλεση OCR σε εικόνα σε JSON με C# και Aspose
url: /el/net/text-recognition/perform-ocr-on-image-to-json-in-c-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε Εικόνα σε JSON με C# και Aspose

Έχετε χρειαστεί ποτέ να **εκτελέσετε OCR σε αρχεία εικόνας** αλλά δεν ήξερατε πώς να πάρετε τα αποτελέσματα σε δομημένη μορφή; Δεν είστε μόνοι—οι προγραμματιστές ρωτούν συνεχώς: «Πώς μετατρέπω μια σαρωμένη φωτογραφία σε χρήσιμα δεδομένα;» Τα καλά νέα είναι ότι το Aspose.OCR το κάνει παιχνιδάκι, και μπορείτε ακόμη και **να γράψετε αρχείο JSON σε C#**‑στυλ με συμπεριλαμβανόμενες βαθμολογίες εμπιστοσύνης.

Σε αυτόν τον οδηγό θα περάσουμε από ένα πλήρες **aspose OCR C# tutorial** που καλύπτει τα πάντα, από τη φόρτωση μιας εικόνας μέχρι την εξαγωγή του αναγνωρισμένου κειμένου ως JSON. Στο τέλος θα έχετε μια εκτελέσιμη εφαρμογή κονσόλας που **εκτελεί OCR σε εικόνα**, μετατρέπει την έξοδο σε JSON (συμπεριλαμβανομένων των τιμών εμπιστοσύνης) και την αποθηκεύει με μία μόνο γραμμή κώδικα. Χωρίς κρυφά βήματα, χωρίς εξωτερικά scripts—απλώς καθαρό C#.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

- .NET 6.0 SDK ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Core και .NET Framework)
- Visual Studio 2022 (ή οποιονδήποτε επεξεργαστή προτιμάτε)
- Ένα έγκυρο **Aspose.OCR for .NET** license ή μια δωρεάν προσωρινή άδεια (η δωρεάν δοκιμή λειτουργεί για δοκιμές)
- Ένα αρχείο εικόνας (`input.png`) που θέλετε να επεξεργαστείτε (οποιοδήποτε κοινό φορμά—PNG, JPG, BMP—θα κάνει)

Αυτό είναι όλο. Αν λείπει κάτι από τα παραπάνω, αποκτήστε το τώρα· το υπόλοιπο του οδηγού υποθέτει ότι όλα είναι ήδη στη θέση τους.

## Βήμα 1: Εγκατάσταση του πακέτου NuGet Aspose.OCR

Πρώτα απ’ όλα—προσθέστε τη βιβλιοθήκη στο έργο σας. Ανοίξτε ένα τερματικό στον φάκελο του έργου και εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

Αυτό κατεβάζει την πιο πρόσφατη έκδοση (από Απρίλιο 2026 είναι η 23.12) και προσθέτει τα απαραίτητα DLL στο φάκελο `bin`. Δεν απαιτείται επιπλέον διαμόρφωση.

## Βήμα 2: Αρχικοποίηση του OCR Engine (Perform OCR on Image)

Τώρα δημιουργούμε ένα αντικείμενο `OcrEngine` και του λέμε ποια γλώσσα να χρησιμοποιήσει. Η αγγλική (`"en"`) είναι η πιο κοινή, αλλά μπορείτε να την αντικαταστήσετε με `"fr"`, `"de"` ή οποιαδήποτε υποστηριζόμενη γλώσσα.

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Path to your input image – change as needed
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        // Path where the JSON will be saved
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // Step 2: Initialize the OCR engine – this is where we **perform OCR on image**
        var ocrEngine = new OcrEngine
        {
            Language = "en"               // Set language; you can use ISO‑639‑1 codes
        };

        // Optional: tweak recognition options (speed vs. accuracy)
        // ocrEngine.RecognitionMode = RecognitionMode.LargeText; // Uncomment for large blocks
```

**Γιατί αρχικοποιούμε εδώ:** Το `OcrEngine` κρατά όλες τις ρυθμίσεις που χρειάζονται για τη διαδικασία αναγνώρισης. Ορίζοντας τη γλώσσα εκ των προτέρων εξασφαλίζει ότι η μηχανή θα χρησιμοποιήσει το σωστό σύνολο χαρακτήρων, βελτιώνοντας δραματικά την ακρίβεια.

## Βήμα 3: Αναγνώριση της Εικόνας και Καταγραφή Εμπιστοσύνης

Με τη μηχανή έτοιμη, τροφοδοτούμε το αρχείο εικόνας. Η μέθοδος `RecognizeImage` επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει τόσο το εξαγόμενο κείμενο όσο και μια βαθμολογία εμπιστοσύνης για κάθε λέξη.

```csharp
        // Step 3: Perform OCR on the image file
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        // Verify that the result is not null
        if (ocrResult == null)
        {
            Console.WriteLine("OCR failed – check the file path and format.");
            return;
        }

        // For debugging: print the plain text to the console
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
```

**Τι συμβαίνει στο παρασκήνιο;** Το Aspose εκτελεί έναν αναγνωριστή βασισμένο σε νευρωνικό δίκτυο που αναλύει κάθε μπλοκ pixel, το συγκρίνει με το μοντέλο γλώσσας και προσθέτει μια τιμή εμπιστοσύνης (0‑100) που δείχνει πόσο σίγουρος είναι για κάθε λέξη.

## Βήμα 4: Μετατροπή του Αποτελέσματος σε JSON (OCR Image to JSON)

Το Aspose κάνει τη μετατροπή απλή. Με το `includeConfidence: true` λαμβάνουμε ένα JSON payload που μοιάζει με αυτό:

```json
{
  "Text": "Hello world",
  "Words": [
    { "Value": "Hello", "Confidence": 97.3 },
    { "Value": "world", "Confidence": 95.8 }
  ]
}
```

Ακολουθεί ο κώδικας που παράγει το JSON string:

```csharp
        // Step 4: Convert OCR result to JSON, including confidence values
        string jsonResult = ocrResult.ToJson(includeConfidence: true);
```

**Γιατί να συμπεριλάβουμε την εμπιστοσύνη;** Αν σκοπεύετε να τροφοδοτήσετε τα δεδομένα σε επόμενες διαδικασίες (π.χ. έλεγχος, επισήμανση UI), το να γνωρίζετε ποιες λέξεις είναι αβέβαιες σας επιτρέπει να αποφασίσετε αν θα ζητήσετε επιβεβαίωση από τον χρήστη.

## Βήμα 5: Γράψιμο του Αρχείου JSON σε C#‑Στυλ

Τώρα πράγματι **γράφουμε αρχείο JSON σε C#**. Η μέθοδος `File.WriteAllText` είναι ατομική και λειτουργεί δια‑πλατφόρμα, καθιστώντας την ιδανική για εφαρμογές κονσόλας.

```csharp
        // Step 5: Save the JSON output to a file
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

Αυτή είναι η πλήρης ροή εργασίας—πέντε σύντομα βήματα που **εκτελούν OCR σε εικόνα**, μετατρέπουν την έξοδο σε JSON και την αποθηκεύουν.

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω βρίσκεται το ολοκληρωμένο πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε στο `Program.cs`. Βεβαιωθείτε ότι το `input.png` βρίσκεται στον ίδιο φάκελο με το εκτελέσιμο ή προσαρμόστε τις διαδρομές ανάλογα.

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------------
        // 1️⃣ Set up file locations (feel free to change paths)
        // -------------------------------------------------------
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // -------------------------------------------------------
        // 2️⃣ Initialize the OCR engine – this is where we **perform OCR on image**
        // -------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Language = "en" // English – replace with "fr", "es", etc. as needed
        };

        // -------------------------------------------------------
        // 3️⃣ Recognize the image and obtain confidence values
        // -------------------------------------------------------
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        if (ocrResult == null)
        {
            Console.WriteLine("❌ OCR failed – verify the image path and format.");
            return;
        }

        // Show plain text (optional)
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine();

        // -------------------------------------------------------
        // 4️⃣ Convert the result to JSON – **OCR image to JSON**
        // -------------------------------------------------------
        string jsonResult = ocrResult.ToJson(includeConfidence: true);

        // -------------------------------------------------------
        // 5️⃣ Write the JSON file – **write JSON file C#** style
        // -------------------------------------------------------
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

### Αναμενόμενη Έξοδος

Όταν εκτελέσετε το πρόγραμμα (`dotnet run`), θα δείτε κάτι σαν:

```
=== Extracted Text ===
Hello world

✅ JSON with confidence saved to: C:\YourProject\output.json
```

Και το `output.json` θα περιέχει το δομημένο JSON που εμφανίστηκε νωρίτερα, με πλήρη ποσοστά εμπιστοσύνης για κάθε λέξη.

## Pro Tips & Edge Cases

- **Διαχείριση ελλιπούς αρχείου:** Τυλίξτε την κλήση `RecognizeImage` σε `try/catch` για `FileNotFoundException` αν αναμένετε δυναμικές διαδρομές.
- **Διάφορες γλώσσες:** Ορίστε `ocrEngine.Language = "fr"` για γαλλικά, ή φορτώστε ένα προσαρμοσμένο πακέτο γλώσσας μέσω `ocrEngine.LoadLanguage("custom.lang")`.
- **Μεγάλα έγγραφα:** Για πολυ‑σελίδες PDF, μετατρέψτε πρώτα κάθε σελίδα σε εικόνα (π.χ. με `Aspose.PDF`) και επαναλάβετε τα βήματα OCR.
- **Βελτιστοποίηση απόδοσης:** Αν χρειάζεστε γρήγορα αποτελέσματα, αλλάξτε σε `RecognitionMode.Fast`—χάνετε λίγο στην ακρίβεια αλλά κερδίζετε ταχύτητα.
- **Μορφοποίηση JSON:** Θέλετε όμορφα μορφοποιημένο JSON; Χρησιμοποιήστε `JsonConvert.SerializeObject` από το Newtonsoft με `Formatting.Indented` μετά την αποσυμπίεση του JSON string του Aspose.

## Συχνές Ερωτήσεις

**Ε: Λειτουργεί αυτό με .NET Framework;**  
Α: Απόλυτα. Το ίδιο πακέτο NuGet στοχεύει στο .NET Standard 2.0, οπότε μπορείτε να το αναφέρετε από .NET Framework 4.6.1 και νεότερα.

**Ε: Τι γίνεται αν χρειάζομαι την εμπιστοσύνη για ολόκληρο το έγγραφο, όχι ανά λέξη;**  
Α: Το `OcrResult` εκθέτει επίσης `OverallConfidence`. Μπορείτε να το προσθέσετε χειροκίνητα στο JSON:

```csharp
var customObj = new
{
    Text = ocrResult.Text,
    OverallConfidence = ocrResult.OverallConfidence,
    Words = ocrResult.Words
};
string json = JsonConvert.SerializeObject(customObj, Formatting.Indented);
```

**Ε: Μπορώ να στέλνω το JSON απευθείας σε web API;**  
Α: Ναι. Αντικαταστήστε το `File.WriteAllText` με ένα `HttpClient` POST που στέλνει το `jsonResult

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}