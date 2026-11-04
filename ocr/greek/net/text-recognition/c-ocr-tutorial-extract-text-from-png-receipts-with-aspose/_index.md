---
category: general
date: 2026-05-25
description: c# OCR tutorial που δείχνει πώς να φορτώσετε αρχείο εικόνας c# και να
  αναγνωρίσετε κείμενο png από απόδειξη χρησιμοποιώντας το Aspose OCR – βήμα‑βήμα
  οδηγός.
draft: false
keywords:
- c# OCR tutorial
- load image file c#
- recognize png text
- read receipt OCR
- perform OCR image
language: el
og_description: c# OCR tutorial που σας καθοδηγεί στη φόρτωση αρχείου εικόνας c# και
  στην αναγνώριση κειμένου png από απόδειξη χρησιμοποιώντας το Aspose OCR.
og_title: c# OCR οδηγός – Εξαγωγή κειμένου από αποδείξεις PNG
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: c# OCR tutorial that shows how to load image file c# and recognize
    png text from a receipt using Aspose OCR – step‑by‑step guide.
  headline: 'c# OCR tutorial: Extract Text from PNG Receipts with Aspose'
  type: TechArticle
- description: c# OCR tutorial that shows how to load image file c# and recognize
    png text from a receipt using Aspose OCR – step‑by‑step guide.
  name: 'c# OCR tutorial: Extract Text from PNG Receipts with Aspose'
  steps:
  - name: Why Aspose?
    text: Aspose OCR supports over 30 languages, works offline, and returns a rich
      `OcrResult` object—perfect for **perform OCR image** tasks where you need more
      than just plain text.
  - name: Handling Common Edge Cases
    text: '| Situation | What to do | |-----------|------------| | **Image is blurry**
      | Pre‑process with `System.Drawing` to sharpen or increase DPI. | | **Receipt
      contains multiple languages** | Set `ocrEngine.Language = OcrLanguage.English
      | OcrLanguage.Spanish;` | | **Large batch processing** | Reuse a sin'
  - name: What’s Next?
    text: '- Experiment with **load image file c#** using `SkiaSharp` for true cross‑platform
      support. - Dive deeper into `OcrResult.Words` to extract line items, prices,
      and dates—perfect for expense‑tracking apps. - Combine this tutorial with Azure
      Functions or AWS Lambda to build a serverless receipt‑proces'
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: 'c# OCR tutorial: Εξαγωγή κειμένου από αποδείξεις PNG με Aspose'
url: /el/net/text-recognition/c-ocr-tutorial-extract-text-from-png-receipts-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR tutorial – Εξαγωγή Κειμένου από Αποδείξεις PNG με Aspose

Έχετε ποτέ χρειαστεί ένα **c# OCR tutorial** που πραγματικά ολοκληρώνει τη δουλειά χωρίς ατέλειωτη αναζήτηση στο Google; Βρίσκεστε στο σωστό μέρος. Σε αυτόν τον οδηγό θα **load image file c#**, **recognize png text**, και **read receipt OCR** αποτελέσματα, όλα ενώ σας δείχνουμε πώς να **perform OCR image** επεξεργασία με το Aspose OCR.

Θα ξεκινήσουμε εγκαθιστώντας το απαιτούμενο πακέτο NuGet, θα περάσουμε γραμμή-γραμμή τον κώδικα, και θα τελειώσουμε με ένα καθαρό JSON dump που μπορείτε να μεταβιβάσετε απευθείας στην επόμενη διαδρομή δεδομένων σας. Χωρίς περιττά, μόνο μια πρακτική, έτοιμη‑για‑εκτέλεση λύση.

## Τι Θα Μάθετε

- Πώς να ρυθμίσετε το Aspose OCR σε ένα έργο .NET 6 (ή νεότερο).  
- Τα ακριβή βήματα για **load an image file c#** και να το παραδώσετε στη μηχανή.  
- Πώς να **recognize png text** από μια εικόνα απόδειξης και να καταγράψετε το αποτέλεσμα.  
- Τρόποι για **read receipt OCR** έξοδο ως ωραία μορφοποιημένο JSON.  
- Συμβουλές για **perform OCR image** λειτουργίες σε διαφορετικούς τύπους αρχείων και διαχείριση κοινών προβλημάτων.

**Απαιτούμενα**  
- Visual Studio 2022 (ή οποιοδήποτε IDE προτιμάτε).  
- .NET 6 SDK ή νεότερο.  
- Μια εικόνα απόδειξης PNG διαθέσιμη (θα την ονομάσουμε `receipt.png`).  

Αν τα έχετε αυτά, ας ξεκινήσουμε.

![c# OCR tutorial screenshot](ocr-demo.png "c# OCR tutorial result showing JSON output")

## c# OCR Tutorial – Ρύθμιση του Μηχανήματος Aspose OCR

Πρώτα απ' όλα, χρειαζόμαστε τη βιβλιοθήκη Aspose OCR. Ανοίξτε το τερματικό σας στον φάκελο της λύσης και εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

Αυτή η εντολή φέρνει όλα τα απαραίτητα, συμπεριλαμβανομένων των εγγενών δυαδικών αρχείων για την αποκωδικοποίηση εικόνας. Μόλις εγκατασταθεί, δημιουργήστε ένα νέο έργο κονσόλας ή προσθέστε τον κώδικα σε ένα υπάρχον.

### Why Aspose?

Το Aspose OCR υποστηρίζει πάνω από 30 γλώσσες, λειτουργεί εκτός σύνδεσης και επιστρέφει ένα πλούσιο αντικείμενο `OcrResult`—ιδανικό για εργασίες **perform OCR image** όπου χρειάζεστε περισσότερα από απλό κείμενο.

## Load image file c# και Προετοιμασία της Απόδειξης

Τώρα που η βιβλιοθήκη είναι έτοιμη, ας **load image file c#**. Η κλάση `System.Drawing.Image` κάνει το σκληρό έργο, αλλά μπορείτε επίσης να χρησιμοποιήσετε το `SkiaSharp` αν προτιμάτε μια εναλλακτική δια‑πλατφόρμα.

```csharp
using System;
using System.Drawing;               // For Image loading
using Aspose.OCR;                  // OCR engine
using System.Text.Json;            // JSON serialization

// Step 1: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    // English works for most receipts; change as needed
    Language = OcrLanguage.English
};

// Step 2: Load the image to be processed
// Replace the path with the actual location of your receipt PNG
string imagePath = @"C:\Receipts\receipt.png";
if (!File.Exists(imagePath))
{
    Console.WriteLine($"File not found: {imagePath}");
    return;
}
using Image receiptImage = Image.FromFile(imagePath);
```

> **Pro tip:** Τυλίξτε το `Image` σε μια δήλωση `using` (όπως φαίνεται) για να ελευθερώσετε άμεσα τους εγγενείς πόρους—ιδιαίτερα σημαντικό όταν **perform OCR image** σε πολλά αρχεία σε βρόχο.

## Recognize PNG text with Aspose

Με την εικόνα στη μνήμη, η μηχανή μπορεί τώρα να **recognize png text**. Το Aspose επιστρέφει ένα `OcrResult` που περιέχει τόσο τη ακατέργαστη συμβολοσειρά όσο και λεπτομερή δεδομένα για κάθε αναγνωρισμένη λέξη.

```csharp
// Step 3: Perform OCR and obtain the result object
OcrResult ocrResult = ocrEngine.RecognizeWithResult(receiptImage);

// Quick sanity check – was anything recognized?
if (string.IsNullOrWhiteSpace(ocrResult.Text))
{
    Console.WriteLine("No text detected. Verify image quality or language settings.");
    return;
}
```

Γιατί να καλέσετε το `RecognizeWithResult` αντί για το πιο απλό `Recognize`; Το πρώτο σας δίνει πρόσβαση σε βαθμολογίες εμπιστοσύνης, περιοριστικά πλαίσια και αλλαγές γραμμής—χρήσιμο αν αργότερα χρειαστείτε **read receipt OCR** για εξαγωγή στοιχείων γραμμής.

## Read receipt OCR Result ως JSON

Τα περισσότερα downstream συστήματα αγαπούν το JSON, οπότε ας σειριοποιήσουμε το `OcrResult`. Ο σειριοποιητής `System.Text.Json` διαχειρίζεται πολύπλοκα αντικείμενα άψογα, και θα ενεργοποιήσουμε την εσοχή για ευανάγνωστη μορφή.

```csharp
// Step 4: Convert the OCR result to a readable JSON string (indented)
string jsonResult = JsonSerializer.Serialize(
    ocrResult,
    new JsonSerializerOptions { WriteIndented = true }
);
```

Το παραγόμενο JSON φαίνεται κάπως έτσι (κομμένο για συντομία):

```json
{
  "Text": "Walmart\n123 Main St\nTotal $12.34",
  "Words": [
    {
      "Text": "Walmart",
      "Confidence": 0.98,
      "Rectangle": { "X": 10, "Y": 20, "Width": 150, "Height": 30 }
    },
    {
      "Text": "Total",
      "Confidence": 0.95,
      "Rectangle": { "X": 10, "Y": 150, "Width": 80, "Height": 25 }
    }
  ]
}
```

Τώρα μπορείτε να μεταβιβάσετε το `jsonResult` σε μια βάση δεδομένων, μια ουρά μηνυμάτων, ή απλώς να το καταγράψετε για εντοπισμό σφαλμάτων.

## Perform OCR Image Processing και Εμφάνιση Αποτελέσματος

Τέλος, εξάγετε το JSON στην κονσόλα. Σε μια πραγματική εφαρμογή πιθανότατα θα το γράφατε σε αρχείο ή θα το στέλνατε μέσω HTTP, αλλά η κονσόλα το κάνει εύκολο για να επαληθεύσετε ότι όλα λειτούργησαν.

```csharp
// Step 5: Output the JSON to the console
Console.WriteLine("=== OCR Result (JSON) ===");
Console.WriteLine(jsonResult);
```

Εκτελέστε το πρόγραμμα (`dotnet run`) και θα πρέπει να δείτε το ωραία μορφοποιημένο JSON εκτυπωμένο. Αν η εικόνα της απόδειξης είναι καθαρή, το κείμενο θα είναι ακριβές· αν όχι, σκεφτείτε να αυξήσετε την ανάλυση της εικόνας ή να εφαρμόσετε ένα φίλτρο προεπεξεργασίας (π.χ., γκρι κλίμακα, ενίσχυση αντίθεσης) πριν το δώσετε στη μηχανή.

### Διαχείριση Συνηθισμένων Περιπτώσεων Άκρων

| Situation | What to do |
|-----------|------------|
| **Η εικόνα είναι θολή** | Προεπεξεργαστείτε με `System.Drawing` για να ενισχύσετε την ευκρίνεια ή να αυξήσετε το DPI. |
| **Η απόδειξη περιέχει πολλές γλώσσες** | Ορίστε `ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;` |
| **Μεγάλη επεξεργασία παρτίδας** | Ξαναχρησιμοποιήστε ένα μόνο αντικείμενο `OcrEngine`; αλλάξτε μόνο το `Image` σε κάθε επανάληψη. |
| **Πίεση μνήμης** | Αποδεσμεύστε άμεσα τα αντικείμενα `Image` και σκεφτείτε `await Task.Run` για ασύγχρονες διαδρόμους. |

Αυτές οι προσαρμογές διατηρούν τη ροή εργασίας **perform OCR image** ανθεκτική ακόμη και όταν η είσοδος δεν είναι τέλεια.

## Συμπέρασμα

Συγχαρητήρια—μόλις ολοκληρώσατε ένα **c# OCR tutorial** που φορτώνει μια εικόνα, **recognizes png text**, και **reads receipt OCR** έξοδο ως καθαρό JSON. Τα βασικά βήματα (ρύθμιση μηχανής, φόρτωση εικόνας, εκτέλεση OCR, σειριοποίηση και εμφάνιση) αποτελούν μια σταθερή βάση που μπορείτε να επεκτείνετε σε τιμολόγια, διαβατήρια ή οποιοδήποτε άλλο σαρωμένο έγγραφο.

### Τι Έρχεται Στη Σειρά;

- Πειραματιστείτε με **load image file c#** χρησιμοποιώντας `SkiaSharp` για αληθινή δια‑πλατφορμική υποστήριξη.  
- Βυθιστείτε περισσότερο στο `OcrResult.Words` για να εξάγετε στοιχεία γραμμής, τιμές και ημερομηνίες—ιδανικό για εφαρμογές παρακολούθησης εξόδων.  
- Συνδυάστε αυτόν τον οδηγό με Azure Functions ή AWS Lambda για να δημιουργήσετε ένα serverless API επεξεργασίας αποδείξεων.  

Νιώστε ελεύθεροι να τροποποιήσετε τον κώδικα, να προσθέσετε περισσότερες εικόνες, ή ακόμη και να αλλάξετε σε διαφορετικό πακέτο γλώσσας. Ο κόσμος του OCR είναι γεμάτος εκπλήξεις, και τώρα έχετε τα εργαλεία για να τις εξερευνήσετε.

Καλό προγραμματισμό, και εύχομαι οι αποδείξεις σας πάντα να είναι αναγνώσιμες!

## Σχετικά Μαθήματα

- [Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Εξαγωγή κειμένου από εικόνα – Βελτιστοποίηση OCR με Aspose.OCR για .NET](/ocr/english/net/ocr-optimization/)
- [Πώς να χρησιμοποιήσετε OCR - Αναγνώριση εικόνας χωρίς ανίχνευση περιοχής κειμένου](/ocr/english/net/image-and-drawing-recognition/recognize-image-without-text-area-detection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}