---
category: general
date: 2026-04-06
description: Αναγνωρίστε το κείμενο εικόνας χρησιμοποιώντας το Aspose OCR σε C#. Μάθετε
  πώς να εξάγετε κείμενο, να φορτώνετε αρχείο εικόνας σε C# και να γράφετε JSON σε
  C# με ένα απλό βήμα‑βήμα παράδειγμα.
draft: false
keywords:
- recognize image text
- how to extract text
- write json in c#
- load image file c#
language: el
og_description: Αναγνωρίστε το κείμενο εικόνας με Aspose OCR σε C#. Αυτός ο οδηγός
  δείχνει πώς να εξάγετε κείμενο, να φορτώσετε αρχείο εικόνας σε C# και να γράψετε
  JSON σε C# γρήγορα.
og_title: Αναγνώριση κειμένου εικόνας σε C# – Πλήρης Οδηγός Βήμα‑Βήμα
tags:
- OCR
- C#
- Aspose
title: Αναγνώριση κειμένου εικόνας σε C# – Πλήρης Οδηγός με Εξαγωγή σε JSON
url: /el/net/text-recognition/recognize-image-text-in-c-full-guide-with-json-export/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση κειμένου εικόνας σε C# – Πλήρης Οδηγός Βήμα‑βήμα

Έχετε χρειαστεί ποτέ να **αναγνωρίσετε κείμενο εικόνας** από μια σαρωμένη απόδειξη αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη να επιλέξετε; Δεν είστε ο μόνος. Σε πολλές πραγματικές εφαρμογές—εφαρμογές παρακολούθησης εξόδων, επεξεργαστές τιμολογίων, ακόμη και εργαλεία προσβασιμότητας—η εξαγωγή των λέξεων από μια εικόνα είναι το πρώτο εμπόδιο.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από μια πρακτική λύση που **αναγνωρίζει κείμενο εικόνας** χρησιμοποιώντας τη βιβλιοθήκη Aspose OCR, δείχνει **πώς να εξάγετε κείμενο**, παρουσιάζει **πώς να φορτώσετε αρχείο εικόνας c#** σωστά, και τελικά **να γράψετε json σε c#** ώστε να μπορείτε να αποθηκεύσετε ή να μεταδώσετε τα αποτελέσματα. Στο τέλος θα έχετε μια έτοιμη για εκτέλεση εφαρμογή console που μετατρέπει οποιοδήποτε PNG σε ένα τακτοποιημένο JSON payload.

---

## Τι Θα Χρειαστείτε

- **.NET 6+** (ο κώδικας λειτουργεί επίσης με .NET Framework 4.8, αλλά το .NET 6 είναι η ιδανική επιλογή).
- **Aspose.OCR for .NET** πακέτο NuGet. Εγκαταστήστε το με `dotnet add package Aspose.OCR`.
- Ένα δείγμα εικόνας (`input.png`) τοποθετημένο κάπου που η εφαρμογή σας μπορεί να το διαβάσει.  
- Visual Studio 2022 ή οποιονδήποτε επεξεργαστή προτιμάτε—χωρίς απαιτήσεις περίπλοκων IDE.

> Pro tip: Κρατήστε τα αρχεία εικόνας σε φάκελο που ονομάζεται `Resources` μέσα στο project· έτσι διατηρείτε τα paths τακτοποιημένα και αποφεύγετε προβλήματα «file not found».

---

## Βήμα 1: αναγνώριση κειμένου εικόνας – Φόρτωση του αρχείου εικόνας

Πριν η μηχανή OCR μπορέσει να κάνει τη μαγεία της, πρέπει να **φορτώσετε το αρχείο εικόνας c#** με ασφάλεια. Η μέθοδος `Image.FromFile` ρίχνει εξαίρεση αν το μονοπάτι είναι λάθος ή το αρχείο δεν υποστηρίζεται, οπότε θα προστατεύσουμε τον κώδικα από αυτό.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Export;

class Program
{
    static void Main()
    {
        // Define input and output paths
        string inputPath  = Path.Combine("Resources", "input.png");
        string outputPath = Path.Combine("Resources", "output.json");

        // Verify the image exists
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"❌ Image not found at {inputPath}");
            return;
        }

        // Load the image – this is the “load image file c#” step
        using (Image receiptImage = Image.FromFile(inputPath))
        {
            // Continue to OCR...
        }
    }
}
```

*Γιατί είναι σημαντικό*: Η φόρτωση της εικόνας μέσα σε ένα `using` block εξασφαλίζει ότι οι μη διαχειριζόμενοι πόροι GDI+ απελευθερώνονται άμεσα, αποτρέποντας διαρροές μνήμης σε υπηρεσίες που τρέχουν για μεγάλο χρονικό διάστημα.

---

## Βήμα 2: Πώς να εξάγετε κείμενο με Aspose OCR

Τώρα που το bitmap βρίσκεται στη μνήμη, το παραδίδουμε στη **αναγνώριση κειμένου εικόνας** μηχανή. Η `OcrEngine` της Aspose είναι απλή: δημιουργείτε ένα αντικείμενο, καλείτε το `Recognize`, και λαμβάνετε ένα αντικείμενο `OcrResult` που περιέχει το ακατέργαστο κείμενο, τις βαθμολογίες εμπιστοσύνης και ακόμη και τα bounding boxes.

```csharp
// Inside the using block from Step 1
var ocrEngine = new OcrEngine();

// Perform OCR – this is the core “how to extract text” operation
OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

// Quick sanity check
if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
{
    Console.WriteLine("⚠️ No text detected. Try a clearer image.");
    return;
}
Console.WriteLine("✅ OCR succeeded. Extracted text:");
Console.WriteLine(ocrResult.Text);
```

*Εξήγηση*: Η μέθοδος `Recognize` εκτελεί το ενσωματωμένο νευρωνικό δίκτυο. Λειτουργεί καλύτερα με εικόνες υψηλής αντίθεσης, 300 DPI. Αν της δώσετε μια θολή φωτογραφία, η εμπιστοσύνη μειώνεται—σκεφτείτε προεπεξεργασία (ευθυγράμμιση, δυαδικοποίηση) για κώδικα παραγωγής.

---

## Βήμα 3: Γράψτε JSON σε C# – Εξαγωγή του αποτελέσματος OCR

Οι περισσότερες API αναμένουν JSON, οπότε θα **γράψουμε json σε c#** χρησιμοποιώντας το `JsonExport` της Aspose. Η βιβλιοθήκη σειριοποιεί ολόκληρο το `OcrResult`, διατηρώντας τις πληροφορίες γραμμής και τις τιμές εμπιστοσύνης.

```csharp
// Still inside the same using block
string jsonResult = JsonExport.ToJson(ocrResult);

// Persist the JSON to disk
File.WriteAllText(outputPath, jsonResult);
Console.WriteLine($"💾 JSON written to {outputPath}");
```

### Αναμενόμενη έξοδος JSON

```json
{
  "Text": "Total: $12.34\r\nDate: 2026-04-01\r\n...",
  "Words": [
    { "Text": "Total", "Confidence": 0.98, "Rectangle": { "X": 10, "Y": 15, "Width": 50, "Height": 12 } },
    { "Text": "$12.34", "Confidence": 0.96, "Rectangle": { "X": 70, "Y": 15, "Width": 45, "Height": 12 } }
    // … more words …
  ]
}
```

*Γιατί JSON;* Είναι ανεξάρτητο από γλώσσα, εύκολο στην αποσυμπίεση, και διατηρεί τα λεπτομερή μεταδεδομένα OCR που μπορεί να χρειαστείτε για επακόλουθη επικύρωση.

---

## Βήμα 4: Πλήρης, εκτελέσιμο πρόγραμμα

Συνδυάζοντας όλα τα κομμάτια, εδώ είναι η πλήρης εφαρμογή console. Αντιγράψτε‑επικολλήστε, επαναφέρετε τα πακέτα NuGet, και πατήστε **F5**.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Export;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Configuration – adjust these paths as needed
        // -------------------------------------------------
        string inputPath  = Path.Combine("Resources", "input.png");
        string outputPath = Path.Combine("Resources", "output.json");

        // -------------------------------------------------
        // Validate input file
        // -------------------------------------------------
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"❌ Image not found at {inputPath}");
            return;
        }

        // -------------------------------------------------
        // Load image (load image file c#)
        // -------------------------------------------------
        using (Image receiptImage = Image.FromFile(inputPath))
        {
            // -------------------------------------------------
            // Initialize OCR engine and recognize text
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();
            OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("⚠️ No text detected. Try a clearer image.");
                return;
            }

            Console.WriteLine("✅ OCR succeeded. Sample output:");
            Console.WriteLine(ocrResult.Text.Substring(0, Math.Min(100, ocrResult.Text.Length)) + "...");

            // -------------------------------------------------
            // Convert result to JSON (write json in c#)
            // -------------------------------------------------
            string jsonResult = JsonExport.ToJson(ocrResult);
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"💾 JSON written to {outputPath}");
        }
    }
}
```

Τρέξτε το πρόγραμμα και ανοίξτε το `Resources/output.json`—θα πρέπει να δείτε μια ωραία δομημένη αναπαράσταση JSON όλων όσων η μηχανή αναγνώρισε.

---

## Διαχείριση Συνηθισμένων Περιπτώσεων

| Κατάσταση | Τι να κάνετε | Γιατί |
|-----------|--------------|-------|
| **Η εικόνα είναι null ή κατεστραμμένη** | Τυλίξτε το `Image.FromFile` σε try/catch και καταγράψτε την εξαίρεση. | Αποτρέπει την κατάρρευση της εφαρμογής και παρέχει σαφές μήνυμα σφάλματος. |
| **Χαμηλές βαθμολογίες εμπιστοσύνης** | Ελέγξτε το `ocrResult.Words[i].Confidence`. Αν είναι κάτω από 0.75, σκεφτείτε προεπεξεργασία (αύξηση DPI, ακονίστρα). | Βελτιώνει την αξιοπιστία για επόμενες διεργασίες όπως η εξαγωγή ποσού. |
| **Μεγάλα αρχεία (>10 MB)** | Μειώστε την ανάλυση της εικόνας πριν το OCR (`receiptImage = new Bitmap(receiptImage, new Size(width/2, height/2))`). | Μειώνει την πίεση μνήμης και επιταχύνει την αναγνώριση. |
| **Έγγραφα πολλαπλών γλωσσών** | Ορίστε `ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;` | Επιτρέπει στη μηχανή να εντοπίζει χαρακτήρες και από τις δύο γλώσσες. |

---

## Bonus: Οπτικοποίηση του αποτελέσματος OCR (προαιρετικό)

Αν θέλετε να δείτε πού τοποθετείται κάθε λέξη στην εικόνα, μπορείτε να σχεδιάσετε τα bounding boxes:

```csharp
using (Graphics g = Graphics.FromImage(receiptImage))
{
    foreach (var word in ocrResult.Words)
    {
        var rect = new Rectangle(word.Rectangle.X, word.Rectangle.Y,
                                 word.Rectangle.Width, word.Rectangle.Height);
        g.DrawRectangle(Pens.Red, rect);
    }
    receiptImage.Save(Path.Combine("Resources", "annotated.png"));
}
```

Το παραγόμενο `annotated.png` θα εμφανίζει κόκκινες ορθογώνιες γύρω από κάθε αναγνωρισμένη λέξη—χρήσιμο για εντοπισμό σφαλμάτων.

---

## Συμπέρασμα

Μόλις **αναγνωρίσαμε κείμενο εικόνας** σε C# από την αρχή μέχρι το τέλος: φορτώσαμε το αρχείο εικόνας, καλέσαμε το Aspose OCR για **πώς να εξάγετε κείμενο**, και τελικά **γράψαμε json σε c#** ώστε τα δεδομένα να μπορούν να ταξιδέψουν οπουδήποτε. Το πλήρες παράδειγμα λειτουργεί αμέσως, και οι επιπλέον συμβουλές σας βοηθούν να αντιμετωπίσετε θολές αποδείξεις, τεράστια αρχεία ή πολυγλωσσικές σαρώσεις.

Τι έπεται; Δοκιμάστε να αντικαταστήσετε το Aspose με άλλη μηχανή (Tesseract, Microsoft OCR) και συγκρίνετε τις βαθμολογίες εμπιστοσύνης, ή τροφοδοτήστε το JSON σε μια βάση δεδομένων για αναφορά εξόδων. Μπορείτε επίσης να επεκτείνετε την εφαρμογή console σε ένα ASP .NET Core Web API που δέχεται μεταφορτώσεις εικόνας και επιστρέφει JSON άμεσα.

Έχετε ερωτήσεις σχετικά με κλιμάκωση, διαχείριση σφαλμάτων ή ενσωμάτωση με Azure Functions; Αφήστε ένα σχόλιο ή στείλτε μου μήνυμα στο GitHub. Καλή προγραμματιστική, και ας είναι πάντα καθαρό το OCR σας! 

---

![Στιγμιότυπο του OCR JSON εξόδου – παράδειγμα αναγνώρισης κειμένου εικόνας](https://example.com/ocr-example.png "παράδειγμα αναγνώρισης κειμένου εικόνας")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}