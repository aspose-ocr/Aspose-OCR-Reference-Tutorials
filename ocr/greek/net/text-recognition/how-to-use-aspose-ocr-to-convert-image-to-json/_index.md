---
category: general
date: 2026-03-15
description: Πώς να χρησιμοποιήσετε το Aspose OCR για την εξαγωγή κειμένου από εικόνες
  και τη μετατροπή εικόνας σε JSON σε C#. Μάθετε να αναγνωρίζετε κείμενο από PNG και
  να λαμβάνετε δομημένη έξοδο γρήγορα.
draft: false
keywords:
- how to use aspose
- convert image to json
- extract text from image
- recognize text from png
- how to extract ocr
language: el
og_description: Πώς να χρησιμοποιήσετε το Aspose OCR για να εξάγετε κείμενο από εικόνες
  και να μετατρέψετε την εικόνα σε JSON σε C#. Αυτός ο οδηγός σας καθοδηγεί στην αναγνώριση
  κειμένου από PNG και στην απόκτηση δομημένης εξόδου.
og_title: Πώς να χρησιμοποιήσετε το Aspose OCR για τη μετατροπή εικόνας σε JSON
tags:
- Aspose
- OCR
- C#
- JSON
title: Πώς να χρησιμοποιήσετε το Aspose OCR για να μετατρέψετε εικόνα σε JSON
url: /el/net/text-recognition/how-to-use-aspose-ocr-to-convert-image-to-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε το Aspose OCR για τη Μετατροπή Εικόνας σε JSON

Το πώς να χρησιμοποιήσετε το Aspose OCR είναι μια συχνή ερώτηση όταν οι προγραμματιστές χρειάζονται να εξάγουν κείμενο από εικόνες. Αν θέλετε να **μετατρέψετε εικόνα σε JSON** ή **αναγνωρίσετε κείμενο από PNG**, αυτός ο οδηγός σας καλύπτει όλα — χωρίς περιττές πληροφορίες, μόνο μια πρακτική, ολοκληρωμένη λύση.

Σε λίγα λεπτά θα περάσουμε από όλα όσα χρειάζεστε: εγκατάσταση της βιβλιοθήκης, ρύθμιση της μηχανής για έξοδο JSON, φόρτωση ενός PNG από απόδειξη, εκτέλεση OCR και τελικά εγγραφή του αποτελέσματος σε αρχείο `.json`. Στο τέλος θα μπορείτε να **εξάγετε κείμενο από αρχείο εικόνας** με μία κλήση μεθόδου και θα καταλάβετε γιατί κάθε βήμα είναι σημαντικό.

> **Συμβουλή:** Το Aspose OCR λειτουργεί με μια ευρεία γκάμα μορφών εικόνας (PNG, JPEG, BMP, TIFF). Ο ίδιος κώδικας παρακάτω θα τις χειριστεί όλες, ώστε να μην χρειάζεται να γράψετε λογική ειδική για κάθε μορφή.

## Τι Θα Χρειαστείτε

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.6+)  
- Ένα έγκυρο πακέτο NuGet Aspose.OCR (δωρεάν δοκιμή ή με άδεια)  
- Ένα αρχείο εικόνας που θέλετε να επεξεργαστείτε (π.χ., `receipt.png`)  
- Visual Studio, VS Code ή οποιονδήποτε επεξεργαστή C# προτιμάτε  

Αυτό είναι όλο — χωρίς επιπλέον εξαρτήσεις, χωρίς εξωτερικές υπηρεσίες. Έτοιμοι; Ας ξεκινήσουμε.

![how to use aspose OCR engine](image-placeholder.png "how to use aspose OCR engine")

## Πώς να Χρησιμοποιήσετε το Aspose OCR – Ρύθμιση Εξόδου JSON

Το πρώτο πράγμα που πρέπει να κάνετε όταν **πώς να χρησιμοποιήσετε aspose** για OCR είναι να δημιουργήσετε μια παρουσία `OcrEngine` και να της πείτε να εκδώσει JSON. Αυτό το μικρό διακόπτη ρύθμισης σας εξοικονομεί την ανάγκη χειροκίνητης σειριοποίησης του αποτελέσματος αργότερα.

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this is the core object that does the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Tell Aspose to give us JSON instead of plain text.
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Load the image you want to recognize.
        var inputImage = Image.FromFile(@"YOUR_DIRECTORY/receipt.png");

        // 4️⃣ Run the OCR process.
        var ocrResult = ocrEngine.Recognize(inputImage);

        // 5️⃣ Save the JSON payload to disk.
        File.WriteAllText(@"YOUR_DIRECTORY/receipt.json", ocrResult.Text);

        // 6️⃣ Let the developer know we’re done.
        Console.WriteLine("JSON saved.");
    }
}
```

**Γιατί είναι σημαντικό:** Ορίζοντας το `OutputFormat` σε `Json` σημαίνει ότι η μηχανή OCR ήδη δομεί το κείμενο σε ιεραρχία σελίδων, γραμμών και λέξεων. Δεν χρειάζεται να αναλύσετε ακατέργαστες συμβολοσειρές αργότερα, κάτι που καθιστά την επεξεργασία downstream — όπως η τροφοδοσία δεδομένων σε βάση δεδομένων — πολύ πιο καθαρή.

## Μετατροπή Εικόνας σε JSON με Aspose OCR

Τώρα που η μηχανή είναι ρυθμισμένη, ας μιλήσουμε πιο αναλυτικά για το **convert image to JSON**.

1. **Φόρτωση της εικόνας** – `Image.FromFile` λειτουργεί για οποιαδήποτε υποστηριζόμενη μορφή. Αν δουλεύετε με ροή (π.χ., ένα ανεβασμένο αρχείο), μπορείτε να χρησιμοποιήσετε `Image.FromStream` αντί αυτού.  
2. **Εκτέλεση `Recognize`** – αυτή η μέθοδος επιστρέφει ένα αντικείμενο `OcrResult`. Επειδή ορίσαμε την έξοδο σε JSON, το `ocrResult.Text` περιέχει ήδη μια συμβολοσειρά JSON.  
3. **Εγγραφή του αρχείου** – `File.WriteAllText` είναι ο πιο απλός τρόπος για να αποθηκεύσετε το JSON. Αν χρειάζεται να το αποθηκεύσετε σε cloud bucket, απλώς αντικαταστήστε αυτή τη γραμμή με την κατάλληλη κλήση SDK.

### Αναμενόμενη Έξοδος JSON

Ένα τυπικό payload JSON φαίνεται ως εξής (συνοπτικό για συντομία):

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Words": [
            { "Text": "Total", "Confidence": 0.99 },
            { "Text": "$12.34", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

Τώρα μπορείτε να τροφοδοτήσετε αυτή τη δομή σε οποιοδήποτε σύστημα downstream — είτε είναι εργαλείο αναφοράς, μοντέλο μηχανικής μάθησης ή απλό αρχείο καταγραφής.

## Εξαγωγή Κειμένου από Εικόνα Χρησιμοποιώντας Aspose OCR

Αν χρειάζεστε μόνο την ακατέργαστη συμβολοσειρά (δηλαδή δεν σας ενδιαφέρει το JSON), απλώς αλλάξτε την μορφή εξόδου σε απλό κείμενο:

```csharp
ocrEngine.Configuration.OutputFormat = OutputFormat.PlainText;
var plainResult = ocrEngine.Recognize(inputImage);
Console.WriteLine(plainResult.Text);
```

**Πότε να επιλέξετε απλό κείμενο;**  
- Γρήγορη αποσφαλμάτωση ή έξοδος στην κονσόλα.  
- Σενάρια όπου θα εφαρμόσετε προσαρμοσμένη μετα-επεξεργασία (π.χ., εξαγωγή με regex).  

Αλλά θυμηθείτε, η **extract text from image** χρησιμοποιώντας JSON σας παρέχει δεδομένα θέσης — χρήσιμα για επισήμανση κειμένου σε UI ή ευθυγράμμιση με πεδία φόρμας.

## Αναγνώριση Κειμένου από Αρχεία PNG

Το PNG είναι μορφή χωρίς απώλειες, η οποία συχνά προσφέρει καλύτερη ακρίβεια OCR σε σύγκριση με τα έντονα συμπιεσμένα JPEG. Ακολουθεί μια γρήγορη λίστα ελέγχου για να εξασφαλίσετε τα καλύτερα αποτελέσματα όταν **recognize text from PNG**:

| Στοιχείο Λίστας | Γιατί Βοηθά |
|----------------|--------------|
| Χρησιμοποιήστε DPI 300+ | Υψηλότερη ανάλυση δίνει στη μηχανή περισσότερα pixel για επεξεργασία. |
| Κρατήστε την εικόνα σε κλίμακα του γκρι | Μειώνει το θόρυβο· το Aspose OCR μετατρέπει αυτόματα, αλλά η προεπεξεργασία μπορεί να επιταχύνει. |
| Αφαιρέστε το φόντο που αποσπά την προσοχή | Καθαρά φόντα βελτιώνουν τις βαθμολογίες εμπιστοσύνης. |

Αν αντιμετωπίσετε χαμηλές βαθμολογίες εμπιστοσύνης, δοκιμάστε να αυξήσετε το DPI ή να εφαρμόσετε ένα απλό φίλτρο κατωφλίου πριν τροφοδοτήσετε την εικόνα στο Aspose.

## Πώς να Εξάγετε Προγραμματιστικά τα Αποτελέσματα OCR

Πέρα από την αποθήκευση του JSON, ίσως θέλετε να διαβάσετε προγραμματιστικά συγκεκριμένα πεδία — π.χ., το συνολικό ποσό σε μια απόδειξη. Επειδή το JSON περιέχει ιεραρχία, μπορείτε να το αποσειριοποιήσετε σε αντικείμενο C#:

```csharp
using System.Text.Json;

// Assuming ocrResult.Text contains the JSON string
var ocrData = JsonSerializer.Deserialize<OcrResponse>(ocrResult.Text);

// Example class definitions (simplified)
public class OcrResponse
{
    public Page[] Pages { get; set; }
}
public class Page
{
    public int PageNumber { get; set; }
    public Line[] Lines { get; set; }
}
public class Line
{
    public Word[] Words { get; set; }
}
public class Word
{
    public string Text { get; set; }
    public double Confidence { get; set; }
}
```

Τώρα μπορείτε να ερωτήσετε το `ocrData` με LINQ:

```csharp
var totalLine = ocrData.Pages
    .SelectMany(p => p.Lines)
    .FirstOrDefault(l => l.Words.Any(w => w.Text.Equals("Total", StringComparison.OrdinalIgnoreCase)));

if (totalLine != null)
{
    var amount = totalLine.Words
        .FirstOrDefault(w => w.Text.StartsWith("$"))
        ?.Text;
    Console.WriteLine($"Extracted amount: {amount}");
}
```

**Γιατί λειτουργεί:** Το JSON ήδη σας λέει πού βρίσκεται κάθε λέξη στη σελίδα, ώστε να μπορείτε αξιόπιστα να εντοπίζετε πεδία ακόμη και αν η διάταξη αλλάξει ελαφρώς.

## Ακραίες Περιπτώσεις & Συνηθισμένα Πιθανά Σφάλματα

- **Null Result:** Αν το `ocrEngine.Recognize` επιστρέψει `null`, η εικόνα μπορεί να μην υποστηρίζεται ή να είναι κατεστραμμένη. Πάντα να το ελέγχετε:

  ```csharp
  var ocrResult = ocrEngine.Recognize(inputImage);
  if (ocrResult == null) throw new InvalidOperationException("OCR failed – check the image path.");
  ```

- **Μεγάλα Αρχεία:** Για εικόνες πολλαπλών megabytes, σκεφτείτε τη ροή της εικόνας ή τη μείωση του μεγέθους πριν το OCR για να αποφύγετε υπερβολική χρήση μνήμης.

- **Θέματα Άδειας:** Η δοκιμαστική έκδοση προσθέτει υδατογράφημα στην έξοδο. Βεβαιωθείτε ότι φορτώνετε την άδειά σας νωρίς στο πρόγραμμα:

  ```csharp
  Aspose.OCR.License license = new Aspose.OCR.License();
  license.SetLicense("Aspose.OCR.lic");
  ```

- **Μη‑Λατινικά Σενάρια:** Το Aspose OCR υποστηρίζει πολλές γλώσσες, αλλά πρέπει να ορίσετε την ιδιότητα `Language` αναλόγως (π.χ., `ocrEngine.Configuration.Language = Language.English;`).

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // Load your Aspose license (optional for trial)
        // var license = new Aspose.OCR.License();
        // license.SetLicense("Aspose.OCR.lic");

        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Set output to JSON – this is the key step for convert image to JSON
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Optional: improve accuracy for PNG files
        ocrEngine.Configuration.Dpi = 300; // higher DPI = better results

        // 4️⃣ Load the image you want to process
        var inputImagePath = @"YOUR_DIRECTORY/receipt.png";
        if (!File.Exists(inputImagePath))
            throw new FileNotFoundException($"Image not found: {inputImagePath}");

        var inputImage = Image.FromFile(inputImagePath);

        // 5️⃣ Run OCR – this is where we actually extract text from image
        var ocrResult = ocrEngine.Recognize(inputImage);
        if (ocrResult == null)
            throw new InvalidOperationException("OCR

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}