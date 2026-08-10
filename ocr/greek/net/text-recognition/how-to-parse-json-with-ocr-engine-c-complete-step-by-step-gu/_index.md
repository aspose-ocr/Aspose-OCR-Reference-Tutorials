---
category: general
date: 2026-03-17
description: Μάθετε πώς να αναλύετε JSON από τα αποτελέσματα OCR σε C#. Αυτό το σεμινάριο
  καλύπτει πώς να εξάγετε κείμενο, να φορτώνετε εικόνα για OCR, να εκτελείτε αναγνώριση
  OCR και να χρησιμοποιείτε αποτελεσματικά τη μηχανή OCR σε C#.
draft: false
keywords:
- how to parse json
- how to extract text
- load image for OCR
- run OCR recognition
- use OCR engine C#
language: el
og_description: Πώς να αναλύσετε JSON από την έξοδο OCR σε C#. Ακολουθήστε τον οδηγό
  μας για να εξάγετε κείμενο, να φορτώσετε εικόνα για OCR, να εκτελέσετε αναγνώριση
  OCR και να χρησιμοποιήσετε τη μηχανή OCR σε C#.
og_title: Πώς να Αναλύσετε JSON με τη Μηχανή OCR C# – Πλήρης Οδηγός
tags:
- C#
- OCR
- JSON
- Image Processing
title: Πώς να Αναλύσετε JSON με τη Μηχανή OCR C# – Πλήρης Οδηγός Βήμα‑βήμα
url: /el/net/text-recognition/how-to-parse-json-with-ocr-engine-c-complete-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Αναλύσετε JSON με τη Μηχανή OCR C# – Πλήρης Οδηγός Βήμα‑βήμα

Έχετε αναρωτηθεί ποτέ **πώς να αναλύσετε json** που προέρχεται κατευθείαν από μια μηχανή OCR; Δεν είστε μόνοι. Οι περισσότεροι προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα—παίρνουν ακατέργαστο JSON και πρέπει να βρουν τον καλύτερο τρόπο να εξάγουν τα χρήσιμα στοιχεία όπως τα confidence scores ή το πραγματικό κείμενο. Σε αυτόν τον οδηγό θα δούμε πώς να φορτώσουμε μια εικόνα για OCR, να εκτελέσουμε την αναγνώριση OCR και, τέλος, **πώς να αναλύσετε json** με καθαρό, συντηρήσιμο τρόπο.

Στο τέλος του tutorial θα μπορείτε να:

* Φορτώσετε μια εικόνα για OCR με λίγες μόνο γραμμές κώδικα.  
* Εκτελέσετε αναγνώριση OCR χρησιμοποιώντας μια μηχανή OCR σε C#.  
* **Πώς να εξάγετε κείμενο** και άλλα μεταδεδομένα από το JSON payload.  
* Αντιμετωπίσετε κοινές περιπτώσεις άκρων (ελλιπή πεδία, μη αναμενόμενες μορφές) χωρίς να καταρρεύσει η εφαρμογή.

Δεν χρειάζεται εξωτερική τεκμηρίωση—όλα όσα χρειάζεστε είναι εδώ.

## Προαπαιτούμενα

Πριν προχωρήσουμε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 ή νεότερο (ο κώδικας μεταγλωττίζεται επίσης σε .NET Framework 4.7+).  
* Μια αναφορά στη βιβλιοθήκη OCR που χρησιμοποιείτε (το παράδειγμα χρησιμοποιεί μια υποθετική κλάση `OcrEngine`).  
* Το πακέτο NuGet `Newtonsoft.Json` για διαχείριση JSON (`Install-Package Newtonsoft.Json`).  
* Ένα αρχείο εικόνας (π.χ. `passport.png`) τοποθετημένο κάπου που η εφαρμογή σας μπορεί να το διαβάσει.

> **Pro tip:** Αν χρησιμοποιείτε εμπορικό OCR SDK, ελέγξτε ότι η μορφή εξόδου JSON είναι ενεργοποιημένη—οι περισσότεροι προμηθευτές την εκθέτουν μέσω μιας ιδιότητας ρύθμισης όπως `ocrEngine.Config.OutputFormat`.

## Βήμα 1 – Δημιουργία και Διαμόρφωση της Μηχανής OCR (Κύρια Λέξη‑κλειδί σε Δράση)

Το πρώτο που πρέπει να κάνετε είναι να δημιουργήσετε ένα αντικείμενο της μηχανής OCR και να της πείτε να επιστρέφει JSON. Εδώ εμφανίζεται για πρώτη φορά η φράση **how to parse json** στον κώδικά μας, επειδή η μηχανή θα μας δώσει μια συμβολοσειρά JSON που θα αναλύσουμε αργότερα.

```csharp
using System;
using Newtonsoft.Json.Linq;   // For JSON parsing
// Assume OcrEngine, OutputFormat, and ImageStream live in the OCR SDK namespace
using OcrSdk;                  // <-- replace with the real namespace

// Step 1: Create an OCR engine instance and set JSON output
var ocrEngine = new OcrEngine();
ocrEngine.Config.OutputFormat = OutputFormat.Json;
```

**Γιατί είναι σημαντικό:** Ορίζοντας το `OutputFormat` σε `Json` εξασφαλίζετε ότι η απόκριση περιέχει τόσο το αναγνωρισμένο κείμενο **όσο και** τα χρήσιμα μεταδεδομένα όπως τα confidence scores. Αν παραλείψετε αυτό το βήμα, θα λάβετε απλό κείμενο και το **how to parse json** θα γίνει άσχετο.

## Βήμα 2 – Φόρτωση Εικόνας για OCR

Τώρα φορτώνουμε την εικόνα που θέλουμε να αναλύσουμε. Εδώ εμφανίζεται η δευτερεύουσα λέξη‑κλειδί **load image for OCR**.

```csharp
// Step 2: Load the image you want to recognize
// Make sure the path points to a real file; otherwise an exception is thrown.
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY\passport.png");
```

> **Τι γίνεται αν το αρχείο δεν υπάρχει;** Τυλίξτε την κλήση σε ένα `try/catch` και εμφανίστε ένα φιλικό μήνυμα—η εφαρμογή σας δεν θα καταρρεύσει και οι χρήστες θα ξέρουν τι πήγε στραβά.

## Βήμα 3 – Εκτέλεση Αναγνώρισης OCR

Με τη μηχανή έτοιμη και την εικόνα φορτωμένη, το επόμενο λογικό βήμα είναι να τρέξετε τη διαδικασία αναγνώρισης. Αυτό ικανοποιεί τη δευτερεύουσα λέξη‑κλειδί **run OCR recognition**.

```csharp
// Step 3: Execute OCR and get the raw result object
var ocrResult = ocrEngine.Recognize();
```

Η ιδιότητα `ocrResult.Text` περιέχει τώρα μια συμβολοσειρά JSON. Αν την εκτυπώσετε στην κονσόλα, θα δείτε κάτι σαν:

```json
{
  "OverallConfidence": 0.92,
  "Pages": [
    {
      "Text": "John Doe\nPassport No: 123456789",
      "Confidence": 0.95
    }
  ]
}
```

## Βήμα 4 – Πώς να Εξάγετε Κείμενο (και Άλλα Πεδία) από το JSON

Εδώ είναι η καρδιά του tutorial: **how to parse json** και **how to extract text** από το payload OCR. Θα χρησιμοποιήσουμε το `Newtonsoft.Json.Linq.JObject` για την ευελιξία του.

```csharp
// Step 4: Output the raw JSON (optional, helps debugging)
Console.WriteLine("Raw OCR JSON:");
Console.WriteLine(ocrResult.Text);
Console.WriteLine();

// Step 5: Parse the JSON into a JObject
JObject jsonObject = JObject.Parse(ocrResult.Text);

// Extract the overall confidence score
var overallConfidence = jsonObject["OverallConfidence"]?.Value<double>() ?? 0.0;
Console.WriteLine($"Overall confidence: {overallConfidence:P0}");

// Extract the text from the first page (how to extract text)
string pageText = jsonObject["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;
Console.WriteLine("Extracted text:");
Console.WriteLine(pageText);
```

**Γιατί να χρησιμοποιήσετε `JObject`;** Σας επιτρέπει να περιηγηθείτε με ασφάλεια στο δέντρο JSON χωρίς να ορίσετε μια πλήρη κλάση μοντέλου C#. Οι τελεστές `?.` προστατεύουν από `NullReferenceException` αν η μηχανή OCR παραλείψει κάποιο πεδίο.

### Διαχείριση Περιπτώσεων Άκρων

* **Ελλιπή πεδία:** Το μοτίβο `?.Value<T>() ?? default` επιστρέφει μια λογική εναλλακτική τιμή.  
* **Πολλές σελίδες:** Κάντε βρόχο πάνω στο `jsonObject["Pages"]` αν περιμένετε περισσότερες από μία σελίδες.  
* **Μη αριθμητικό confidence:** Χρησιμοποιήστε `double.TryParse` αν το SDK μερικές φορές επιστρέφει συμβολοσειρά.

## Βήμα 5 – Συσκευασία Όλων σε Μία Επαναχρησιμοποιήσιμη Μέθοδο

Για να αποφύγετε την επαναλαμβανόμενη αντιγραφή του ίδιου κώδικα, ενσωματώστε όλη τη ροή σε μια βοηθητική μέθοδο. Αυτό επίσης δείχνει **use OCR engine C#** με καθαρό, επαναχρησιμοποιήσιμο τρόπο.

```csharp
public static void RunOcrAndParseJson(string imagePath)
{
    // 1️⃣ Create engine & set JSON output
    var engine = new OcrEngine();
    engine.Config.OutputFormat = OutputFormat.Json;

    // 2️⃣ Load image (load image for OCR)
    engine.Image = ImageStream.FromFile(imagePath);

    // 3️⃣ Run OCR (run OCR recognition)
    var result = engine.Recognize();

    // 4️⃣ Show raw JSON (optional)
    Console.WriteLine("=== Raw JSON ===");
    Console.WriteLine(result.Text);
    Console.WriteLine();

    // 5️⃣ Parse JSON (how to parse json)
    JObject obj = JObject.Parse(result.Text);

    // 6️⃣ Extract useful data (how to extract text)
    double confidence = obj["OverallConfidence"]?.Value<double>() ?? 0.0;
    string text = obj["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;

    Console.WriteLine($"Overall confidence: {confidence:P0}");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(text);
}
```

Τώρα μπορείτε να καλέσετε `RunOcrAndParseJson(@"C:\Images\passport.png");` από το `Main` ή από οποιοδήποτε άλλο τμήμα της εφαρμογής σας.

## Πλήρες Παράδειγμα Εφαρμογής

Παρακάτω υπάρχει ένα πλήρες, αυτόνομο πρόγραμμα κονσόλας που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα νέο `.csproj`. Περιλαμβάνει όλα τα κομμάτια που συζητήσαμε, καθώς και λίγη διαχείριση σφαλμάτων.

```csharp
// File: Program.cs
using System;
using Newtonsoft.Json.Linq;
using OcrSdk;               // Replace with the actual namespace of your OCR library

class Program
{
    static void Main()
    {
        try
        {
            // Adjust the path to point at a real image on your machine
            string imagePath = @"YOUR_DIRECTORY\passport.png";

            RunOcrAndParseJson(imagePath);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Unexpected error: {ex.Message}");
        }
    }

    /// <summary>
    /// Demonstrates how to parse JSON returned by an OCR engine,
    /// and how to extract text, confidence, and other metadata.
    /// </summary>
    /// <param name="imagePath">Full path to the image file.</param>
    public static void RunOcrAndParseJson(string imagePath)
    {
        // 1️⃣ Initialize OCR engine (use OCR engine C#)
        var engine = new OcrEngine();
        engine.Config.OutputFormat = OutputFormat.Json;

        // 2️⃣ Load image for OCR
        engine.Image = ImageStream.FromFile(imagePath);

        // 3️⃣ Run OCR recognition
        var result = engine.Recognize();

        // 4️⃣ Print raw JSON (helps debugging)
        Console.WriteLine("=== Raw OCR JSON ===");
        Console.WriteLine(result.Text);
        Console.WriteLine();

        // 5️⃣ Parse JSON (how to parse json)
        JObject json = JObject.Parse(result.Text);

        // 6️⃣ Extract overall confidence
        double overallConf = json["OverallConfidence"]?.Value<double>() ?? 0.0;
        Console.WriteLine($"Overall confidence: {overallConf:P0}");

        // 7️⃣ Extract text from first page (how to extract text)
        string firstPageText = json["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(firstPageText);
    }
}
```

**Αναμενόμενη έξοδος** (υπό την προϋπόθεση ότι η OCR ολοκληρώθηκε επιτυχώς):

```
=== Raw OCR JSON ===
{
  "OverallConfidence": 0.92,
  "Pages": [
    {
      "Text": "John Doe\nPassport No: 123456789",
      "Confidence": 0.95
    }
  ]
}

Overall confidence: 92%
=== Extracted Text ===
John Doe
Passport No: 123456789
```

Αν η εικόνα δεν μπορεί να διαβαστεί, το SDK θα ρίξει εξαίρεση που παγιδεύουμε στο `Main`, εκτυπώνοντας ένα φιλικό σφάλμα αντί για κατάρρευση.

## Συχνές Ερωτήσεις (FAQs)

**Ε: Τι γίνεται αν η μηχανή OCR επιστρέψει έναν πίνακα σελίδων;**  
Α: Κάντε βρόχο πάνω στο `json["Pages"]` και συνενώστε κάθε τιμή `["Text"]`, ή επεξεργαστείτε τις ξεχωριστά ανάλογα με την περίπτωση χρήσης σας.

**Ε: Μπορώ να αποσυσχετίσω το JSON σε μια τυποποιημένη κλάση C#;**  
Α: Φυσικά. Ορίστε μια δομή κλάσεων που ταιριάζει στο σχήμα του JSON και χρησιμοποιήστε `JsonConvert.DeserializeObject<YourRootClass>(result.Text)`. Αυτό προσφέρει ασφάλεια χρόνου μεταγλώττισης, αλλά απαιτεί να διατηρείτε το μοντέλο συγχρονισμένο με την έξοδο του SDK.

**Ε: Λειτουργεί αυτό με ασύγχρονα OCR APIs;**  
Α: Ναι. Αντικαταστήστε το `engine.Recognize()` με `await engine.RecognizeAsync()` και κάντε τη μέθοδο `RunOcrAndParseJson` `async Task`. Το τμήμα ανάλυσης JSON παραμένει το ίδιο.

**Ε: Πώς αποθηκεύω το JSON σε αρχείο για μελλοντική ανάλυση;**  
Α: Αφού ληφθεί το `result.Text`, καλέστε `File.WriteAllText(@"output.json", result.Text);`. Στη συνέχεια μπορείτε να το φορτώσετε ξανά με `JObject.Parse(File.ReadAllText(...))`.

## Επόμενα Βήματα

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}