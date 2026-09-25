---
category: general
date: 2026-01-01
description: Προεπεξεργασία εικόνας OCR για βελτίωση της ακρίβειας. Μάθετε πώς να
  αναγνωρίζετε κείμενο σε εικόνα, να βελτιώνετε την ακρίβεια του OCR, να φορτώνετε
  εικόνα OCR και να εμφανίζετε το κείμενο OCR χρησιμοποιώντας το Aspose OCR.
draft: false
keywords:
- preprocess image ocr
- recognize text image
- improve ocr accuracy
- display ocr text
- load image ocr
language: el
og_description: Προεπεξεργασία OCR εικόνας για βελτίωση της ακρίβειας. Αυτός ο οδηγός
  δείχνει πώς να αναγνωρίζετε κείμενο σε εικόνα, να φορτώνετε OCR εικόνας, να εφαρμόζετε
  φίλτρα και να εμφανίζετε το κείμενο OCR.
og_title: Προεπεξεργασία OCR εικόνας σε C# – Βελτιώστε την ακρίβεια με το Aspose OCR
tags:
- Aspose OCR
- C#
- Image preprocessing
title: Προεπεξεργασία OCR εικόνας σε C# – Βελτιώστε την ακρίβεια με το Aspose OCR
url: /el/net/ocr-optimization/preprocess-image-ocr-in-c-boost-accuracy-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# preprocess image ocr in C# – Boost Accuracy with Aspose OCR

Ever wondered how to **preprocess image ocr** so the engine actually reads what’s on the page? You’re not alone—most developers hit a wall when a noisy, skewed scan refuses to cooperate. The good news is that a few smart preprocessing steps can turn a disaster‑zone image into clean, readable text.

Σε αυτό το tutorial θα περάσουμε από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που **recognize text image** αρχεία, **improve OCR accuracy**, και τελικά **display OCR text** στην κονσόλα. Στο τέλος θα ξέρετε πώς να **load image OCR** πόρους, να προσθέσετε φίλτρα όπως η διόρθωση κλίσης και η αποθορυβοποίηση, και να λάβετε αξιόπιστα αποτελέσματα—όλα με το Aspose.OCR για .NET.

## What You’ll Learn

- Πώς να δημιουργήσετε ένα στιγμιότυπο `OcrEngine` και να ρυθμίσετε τα φίλτρα προεπεξεργασίας.
- Γιατί η διόρθωση κλίσης και τα φίλτρα αποθορυβοποίησης είναι σημαντικά για **improve OCR accuracy**.
- Ο ακριβής κώδικας για **load image ocr** αρχεία και εκτέλεση αναγνώρισης.
- Πώς να **display OCR text** με φιλικό προς τον χρήστη τρόπο.
- Συμβουλές, παγίδες και προαιρετικές ρυθμίσεις που μπορείτε να εφαρμόσετε σε πραγματικά έργα.

### Prerequisites

- .NET 6+ (ή .NET Framework 4.7+) εγκατεστημένο στον υπολογιστή σας.  
- Άδεια για το Aspose.OCR (η δωρεάν δοκιμή λειτουργεί για αυτήν την επίδειξη).  
- Βασικές γνώσεις C#—δεν απαιτούνται προχωρημένα κόλπα.  

Αν κάποιο από αυτά σας φαίνεται άγνωστο, απλώς κάντε παύση και εγκαταστήστε τα ελλείποντα στοιχεία· το υπόλοιπο του οδηγού υποθέτει ότι είναι ήδη στη θέση τους.

## preprocess image ocr – Setting Up Filters

Το πρώτο που πρέπει να καταλάβετε είναι **why preprocessing matters**. Οι μηχανές OCR είναι εξαιρετικές στο να διαβάζουν καθαρό, ευθεία κείμενο, αλλά οι πραγματικές σαρώσεις συχνά υποφέρουν από περιστροφή, θολότητα ή θόρυβο φόντου. Με την παροχή μιας καθαρισμένης εικόνας στη μηχανή αυξάνετε δραματικά τις πιθανότητες σωστής μεταγραφής.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Add preprocessing filters.
        //    • SkewCorrectionFilter: straightens tilted text.
        //    • DenoiseFilter: removes speckles and grain.
        ocrEngine.Settings.PreprocessingFilters.Add(new SkewCorrectionFilter());
        ocrEngine.Settings.PreprocessingFilters.Add(new DenoiseFilter());

        // 3️⃣ (Optional) Fine‑tune filter parameters.
        // ((SkewCorrectionFilter)ocrEngine.Settings.PreprocessingFilters[0]).MaxAngle = 25;

        // 4️⃣ Load the image you want to run OCR on.
        OcrImage inputImage = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_noisy.jpg");

        // 5️⃣ Run the recognition.
        OcrResult ocrResult = ocrEngine.Recognize(inputImage);

        // 6️⃣ Show the recognized text.
        Console.WriteLine("Corrected text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Τι συμβαίνει εδώ;**  
- **Βήμα 1** δημιουργεί τη μηχανή—την καρδιά της βιβλιοθήκης Aspose OCR.  
- **Βήμα 2** προσθέτει δύο φίλτρα. Το `SkewCorrectionFilter` περιστρέφει την εικόνα πίσω στην οριζόντια θέση, ενώ το `DenoiseFilter` εξομαλύνει τον θόρυβο σε επίπεδο pixel.  
- **Βήμα 3** είναι προαιρετικό αλλά χρήσιμο· μπορείτε να περιορίσετε τη μέγιστη γωνία που η μηχανή θα προσπαθήσει να διορθώσει, αποτρέποντας την υπερβολική περιστροφή σε ήδη ευθείες σελίδες.  
- **Βήμα 4** είναι όπου **load image OCR** δεδομένα. Αντικαταστήστε το `YOUR_DIRECTORY/skewed_noisy.jpg` με τη διαδρομή του αρχείου δοκιμής σας.  
- **Βήμα 5** εκτελεί πραγματικά το OCR και παράγει ένα `OcrResult`.  
- **Βήμα 6** **display OCR text** στην κονσόλα, παρέχοντάς σας άμεση ανάδραση.

> **Συμβουλή:** Αν παρατηρήσετε ότι η έξοδος εξακολουθεί να περιέχει ακατάληπτους χαρακτήρες, δοκιμάστε να αυξήσετε το `MaxAngle` ή να προσθέσετε ένα `ContrastFilter` πριν από το βήμα αποθορυβοποίησης.

## recognize text image – Loading Your Files Correctly

Ένα κοινό εμπόδιο είναι το **load image ocr** με λάθος μορφή ή DPI. Το Aspose.OCR υποστηρίζει PNG, JPEG, TIFF, BMP, και ακόμη εικόνες βασισμένες σε PDF. Ωστόσο, η μηχανή λειτουργεί καλύτερα με 300 DPI ή περισσότερο για έντυπα έγγραφα.

```csharp
// Example: loading a high‑resolution PNG
string imagePath = @"C:\Images\invoice_300dpi.png";
OcrImage highRes = OcrImage.FromFile(imagePath);
```

Αν εργάζεστε με ένα multi‑page TIFF, μπορείτε να επαναλάβετε για κάθε καρέ:

```csharp
var tiff = Aspose.OCR.ImageProcessing.TiffImage.FromFile(@"multi_page.tif");
foreach (var frame in tiff.Frames)
{
    OcrResult pageResult = ocrEngine.Recognize(frame);
    Console.WriteLine(pageResult.Text);
}
```

**Why does this matter for improve OCR accuracy?** Η υψηλότερη ανάλυση διατηρεί το σχήμα κάθε χαρακτήρα, παρέχοντας στον αναγνωριστή περισσότερα σημεία δεδομένων. Οι εικόνες με χαμηλότερο DPI συχνά οδηγούν σε συγχωνευμένα ή σπασμένα γλύφους, που η μηχανή θα ερμηνεύσει λανθασμένα.

## improve OCR accuracy – Tweaking Filter Parameters

Οι προεπιλεγμένες ρυθμίσεις φίλτρων είναι ένα καλό σημείο εκκίνησης, αλλά μπορείτε να εξάγετε επιπλέον απόδοση από αυτές.

| Φίλτρο | Κύρια Ιδιότητα | Τυπική Τιμή | Πότε να Προσαρμόσετε |
|--------|----------------|------------|----------------------|
| `SkewCorrectionFilter` | `MaxAngle` | `15` (degrees) | Εικόνες που είναι πολύ κεκλιμένες (μέχρι 30°). |
| `DenoiseFilter` | `Strength` | `0.5` (0‑1) | Πολύ θορυβώδεις σαρώσεις· αυξήστε σε `0.8`. |
| `ContrastFilter` (optional) | `Level` | `1.2` | Στιγμιότυπα οθόνης χαμηλής αντίθεσης. |

Παράδειγμα προσαρμογής και των δύο:

```csharp
var skew = new SkewCorrectionFilter { MaxAngle = 25 };
var denoise = new DenoiseFilter { Strength = 0.8 };
ocrEngine.Settings.PreprocessingFilters.Clear(); // start fresh
ocrEngine.Settings.PreprocessingFilters.Add(skew);
ocrEngine.Settings.PreprocessingFilters.Add(denoise);
```

**Edge case:** Αν η εικόνα σας περιέχει τόσο χειρόγραφες σημειώσεις όσο και τυπωμένο κείμενο, ίσως θέλετε να προσθέσετε ένα `BinarizationFilter` πριν από την αποθορυβοποίηση για να διαχωρίσετε το προσκήνιο από το φόντο.

## display OCR text – Formatting the Output

Η απλή έξοδος στην κονσόλα λειτουργεί για επιδείξεις, αλλά ο κώδικας παραγωγής συχνά χρειάζεται καθαρισμένες συμβολοσειρές, αλλαγές γραμμής ή ακόμη και JSON.

```csharp
// Remove extra whitespace and line breaks
string cleaned = System.Text.RegularExpressions.Regex
    .Replace(ocrResult.Text, @"\s+", " ")
    .Trim();

Console.WriteLine("📝 Recognized Text:");
Console.WriteLine(cleaned);
```

Αν χρειάζεστε JSON για μια απάντηση API:

```csharp
var payload = new {
    source = imagePath,
    text = cleaned,
    confidence = ocrResult.Confidence // overall confidence score
};
string json = System.Text.Json.JsonSerializer.Serialize(payload, new JsonSerializerOptions { WriteIndented = true });
Console.WriteLine(json);
```

Τώρα έχετε **display OCR text** σε μορφή που μπορούν να καταναλώσουν οι επόμενες υπηρεσίες.

## Full Working Example – Put It All Together

Παρακάτω είναι το τελικό, αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα νέο έργο κονσόλας. Περιλαμβάνει προαιρετικά φίλτρα, φόρτωση εικόνας υψηλής ανάλυσης και καθαρή έξοδο.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;
using System.Text.Json;
using System.Text.RegularExpressions;

class PreprocessDemo
{
    static void Main()
    {
        // ---------- 1️⃣ Initialize OCR engine ----------
        OcrEngine ocrEngine = new OcrEngine();

        // ---------- 2️⃣ Configure preprocessing ----------
        // Skew correction (up to 25°) + strong denoise
        var skew = new SkewCorrectionFilter { MaxAngle = 25 };
        var denoise = new DenoiseFilter { Strength = 0.8 };
        ocrEngine.Settings.PreprocessingFilters.Add(skew);
        ocrEngine.Settings.PreprocessingFilters.Add(denoise);

        // Optional: increase contrast for low‑visibility scans
        // ocrEngine.Settings.PreprocessingFilters.Add(new ContrastFilter { Level = 1.3 });

        // ---------- 3️⃣ Load the image ----------
        string imagePath = @"YOUR_DIRECTORY/skewed_noisy.jpg";
        OcrImage inputImage = OcrImage.FromFile(imagePath);

        // ---------- 4️⃣ Run OCR ----------
        OcrResult result = ocrEngine.Recognize(inputImage);

        // ---------- 5️⃣ Clean & display ----------
        string cleaned = Regex.Replace(result.Text, @"\s+", " ").Trim();
        Console.WriteLine("✅ Corrected text:");
        Console.WriteLine(cleaned);

        // ---------- 6️⃣ JSON payload (if needed) ----------
        var payload = new {
            source = imagePath,
            text = cleaned,
            confidence = result.Confidence
        };
        string json = JsonSerializer.Serialize(payload, new JsonSerializerOptions { WriteIndented = true });
        Console.WriteLine("\n📦 JSON output:");
        Console.WriteLine(json);
    }
}
```

**Αναμενόμενη έξοδος κονσόλας (παράδειγμα):**

```
✅ Corrected text:
Invoice #12345 Date: 01/15/2026 Total: $1,250.00

📦 JSON output:
{
  "source": "YOUR_DIRECTORY/skewed_noisy.jpg",
  "text": "Invoice #12345 Date: 01/15/2026 Total: $1,250.00",
  "confidence": 0.97
}
```

Αν εκτελέσετε το πρόγραμμα με διαφορετικό αρχείο, το κείμενο και η εμπιστοσύνη θα αλλάξουν ανάλογα.

## Common Questions & Answers

**Ε: Τι γίνεται αν η εικόνα μου είναι ήδη ευθεία;**  
**Α:** Το φίλτρο κλίσης θα εντοπίσει γωνία σχεδόν μηδενική και ουσιαστικά θα γίνει no‑op, οπότε μπορείτε να το αφήσετε ενεργό με ασφάλεια.

**Ε: Υποστηρίζει το Aspose.OCR γλώσσες εκτός της Αγγλικής;**  
**Α:** Ναι—απλώς ορίστε `ocrEngine.Settings.Language = OcrLanguage.Spanish;` (ή οποιαδήποτε υποστηριζόμενη γλώσσα) πριν καλέσετε `Recognize`.

**Ε: Πώς να διαχειριστώ PDF πολλαπλών σελίδων;**  
**Α:** Μετατρέψτε κάθε σελίδα σε εικόνα (το Aspose.PDF μπορεί να το κάνει) και τροφοδοτήστε τα μία‑μια στο ίδιο στιγμιότυπο `OcrEngine`.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}