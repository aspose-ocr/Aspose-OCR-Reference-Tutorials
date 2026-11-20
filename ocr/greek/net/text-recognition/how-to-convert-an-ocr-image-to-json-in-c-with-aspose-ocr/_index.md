---
category: general
date: 2026-09-06
description: Μετατροπή εικόνας OCR σε JSON με C# χρησιμοποιώντας το Aspose.OCR – βήμα‑βήμα
  οδηγός για εξαγωγή κειμένου από εικόνα και λήψη εξόδου JSON.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- ocr image to json
- extract text from image
- convert image to text
- recognize text from photo
- load image for ocr
language: el
lastmod: 2026-09-06
og_description: ocr εικόνα σε json σε C# με Aspose.OCR. Μάθετε πώς να φορτώνετε μια
  εικόνα για OCR, να αναγνωρίζετε κείμενο από φωτογραφία και να μετατρέπετε το αποτέλεσμα
  σε JSON.
og_image_alt: Screenshot of C# code that converts an OCR image to JSON using Aspose.OCR
og_title: Μετατροπή εικόνας OCR σε JSON σε C# – πλήρης οδηγός Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-09-06'
  description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  headline: How to convert an OCR image to JSON in C# with Aspose.OCR
  type: TechArticle
- description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  name: How to convert an OCR image to JSON in C# with Aspose.OCR
  steps:
  - name: Place an image named `input.jpg` in the project root.
    text: Place an image named `input.jpg` in the project root.
  - name: Execute `dotnet run`.
    text: Execute `dotnet run`.
  - name: Observe the console output and open `output.json` to see the structured
      data.
    text: Observe the console output and open `output.json` to see the structured
      data.
  type: HowTo
- questions:
  - answer: Yes. Use `ocrEngine.SaveJson(Stream)` to write directly to a `MemoryStream`,
      then call `stream.ToArray()`.
    question: Can I get the OCR result as a byte array instead of a file?
  - answer: Aspose.OCR can accept PDF pages converted to images via Aspose.PDF, but
      the OCR engine itself works on raster images. Convert PDFs to images first,
      then **load image for ocr**.
    question: Does the engine support PDF input?
  - answer: 'Set `ocrEngine.Language = OcrLanguage.Arabic`. The JSON includes the
      correct text direction, which you can render in UI frameworks that support RTL.
      ## Conclusion You now have a complete solution for **ocr image to json** in
      C#. By loading an image, configuring the language, running the OCR engine, '
    question: How do I handle right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- Aspose.OCR
- C#
- JSON
- Image processing
title: Πώς να μετατρέψετε μια εικόνα OCR σε JSON σε C# με το Aspose.OCR
url: /el/net/text-recognition/how-to-convert-an-ocr-image-to-json-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να μετατρέψετε μια εικόνα OCR σε JSON σε C# με Aspose.OCR

Εάν χρειάζεστε **ocr image to json** σε εφαρμογή .NET, αυτός ο οδηγός σας δείχνει πώς να το κάνετε με το Aspose.OCR. Θα περάσουμε από τη φόρτωση μιας εικόνας για OCR, την αναγνώριση κειμένου από φωτογραφία και τη μετατροπή του αποτελέσματος σε JSON ώστε να μπορείτε να χρησιμοποιήσετε τα δεδομένα σε API ή βάσεις δεδομένων.

Η εξαγωγή κειμένου από αρχεία εικόνας είναι συχνή απαίτηση για επεξεργασία τιμολογίων, σάρωση αποδείξεων και αρχειοθέτηση. Στο τέλος αυτού του tutorial θα μπορείτε να **convert image to text**, να λάβετε το αποτέλεσμα ως απλό κείμενο και να δημιουργήσετε ένα δομημένο payload JSON που διατηρεί τις πληροφορίες διάταξης.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

- .NET 6.0 SDK ή νεότερο εγκατεστημένο  
- Visual Studio 2022 (ή οποιονδήποτε επεξεργαστή που υποστηρίζει .NET)  
- Πακέτο NuGet Aspose.OCR (`Aspose.OCR`) προστιθέμενο στο πρόγραμμά σας  
- Ένα δείγμα εικόνας (`input.jpg`) τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε από τον κώδικα  

Δεν χρειάζεστε επιπλέον μηχανές OCR· το Aspose.OCR διαχειρίζεται όλη τη βαριά δουλειά εσωτερικά.

## Βήμα 1: Εγκατάσταση του πακέτου NuGet Aspose.OCR

Ανοίξτε ένα τερματικό στο φάκελο του έργου σας και εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

Το πακέτο περιλαμβάνει την κλάση `Aspose.OCR.OcrEngine`, η οποία παρέχει μεθόδους για **load image for ocr**, επιλογή γλώσσας και εξαγωγή αποτελεσμάτων.

## Βήμα 2: Δημιουργία νέου έργου κονσόλας C#

Εάν δεν έχετε ήδη έργο, δημιουργήστε ένα:

```bash
dotnet new console -n OcrToJsonDemo
cd OcrToJsonDemo
```

Προσθέστε τις οδηγίες `using` που θα χρειαστείτε:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;
```

## Βήμα 3: Φόρτωση της εικόνας και ρύθμιση του κινητήρα OCR

Ο παρακάτω κώδικας δείχνει πώς να **load image for ocr**, να ορίσετε τη γλώσσα και να προετοιμάσετε τον κινητήρα για επεξεργασία. Σε αυτό το παράδειγμα χρησιμοποιούμε κυριλλική, αλλά μπορείτε να αλλάξετε σε `OcrLanguage.English`, `OcrLanguage.French` κ.λπ., ανάλογα με τη γλώσσα προέλευσης.

```csharp
// Step 3: Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Choose the language that matches the text in the image.
// Replace OcrLanguage.Cyrillic with the language you need.
ocrEngine.Language = OcrLanguage.Cyrillic;

// Load the image file. The ImageStream class abstracts file, stream, or byte[] sources.
string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
ocrEngine.Image = ImageStream.FromFile(imagePath);
```

> **Γιατί είναι σημαντικό:** Η σωστή ρύθμιση της γλώσσας βελτιώνει δραστικά την ακρίβεια όταν **recognize text from photo**. Ο κινητήρας χρησιμοποιεί λεξικά και σύνολα χαρακτήρων ειδικά για τη γλώσσα.

## Βήμα 4: Εκτέλεση της διαδικασίας OCR και ανάκτηση αποτελεσμάτων

Τώρα εκτελέστε τον κινητήρα OCR. Εάν η διαδικασία ολοκληρωθεί με επιτυχία, μπορείτε να **extract text from image** ως απλό κείμενο, HTML ή JSON. Το Aspose.OCR παρέχει τη μέθοδο `SaveJson` που γράφει το δομημένο αποτέλεσμα σε αρχείο.

```csharp
// Step 4: Execute the OCR process
if (ocrEngine.Process())
{
    // Plain‑text output
    string plainText = ocrEngine.Text;
    Console.WriteLine("=== Plain Text ===");
    Console.WriteLine(plainText);

    // JSON output – includes bounding boxes, confidence scores, and line information
    string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
    ocrEngine.SaveJson(jsonPath);
    Console.WriteLine($"\nJSON result saved to: {jsonPath}");
}
else
{
    Console.WriteLine("OCR processing failed. Check the image path and format.");
}
```

### Αναμενόμενη δομή JSON

Ένα τυπικό αρχείο `output.json` έχει την εξής μορφή (μορφοποιημένο για ευκολία ανάγνωσης):

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Пример текста",
          "Confidence": 0.96,
          "Rect": { "X": 45, "Y": 120, "Width": 210, "Height": 30 }
        },
        {
          "Text": "Еще одна строка",
          "Confidence": 0.93,
          "Rect": { "X": 45, "Y": 160, "Width": 230, "Height": 28 }
        }
      ]
    }
  ]
}
```

Το payload JSON περιέχει το κείμενο κάθε γραμμής, ένα σκορ εμπιστοσύνης και το ορθογώνιο που περιβάλλει τη γραμμή στην αρχική φωτογραφία. Αυτό διευκολύνει τη χαρτογράφηση του αποτελέσματος OCR σε στοιχεία UI ή πεδία βάσης δεδομένων.

## Βήμα 5: Πλήρης κώδικας πηγαίου για τη demo

Ακολουθεί το ολοκληρωμένο, έτοιμο‑για‑εκτέλεση πρόγραμμα που υλοποιεί τη ροή εργασίας **ocr image to json**. Αντιγράψτε το στο `Program.cs` και τρέξτε `dotnet run`.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrToJsonDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Select the language (Cyrillic in this example)
            ocrEngine.Language = OcrLanguage.Cyrillic;

            // 3️⃣ Load the image you want to process
            string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found: {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 4️⃣ Run the OCR process
            if (ocrEngine.Process())
            {
                // 5️⃣ Retrieve plain text (optional)
                string plainText = ocrEngine.Text;
                Console.WriteLine("=== Plain Text ===");
                Console.WriteLine(plainText);

                // 6️⃣ Save the result as JSON
                string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
                ocrEngine.SaveJson(jsonPath);
                Console.WriteLine($"\nJSON result saved to: {jsonPath}");
            }
            else
            {
                Console.WriteLine("OCR processing failed. Verify the image format and language settings.");
            }
        }
    }
}
```

### Εκτέλεση του παραδείγματος

1. Τοποθετήστε μια εικόνα με όνομα `input.jpg` στη ρίζα του έργου.  
2. Εκτελέστε `dotnet run`.  
3. Παρακολουθήστε την έξοδο της κονσόλας και ανοίξτε το `output.json` για να δείτε τα δομημένα δεδομένα.

## Συμβουλές και κοινά προβλήματα

| Situation | Recommendation |
|-----------|----------------|
| **Low‑resolution photos** | Αυξήστε το DPI πριν την επεξεργασία ή χρησιμοποιήστε `ocrEngine.Image = ImageStream.FromFile(path, 300)` για να εξαναγκάσετε 300 DPI. |
| **Mixed languages** | Ορίστε `ocrEngine.Language = OcrLanguage.Multilingual` και προαιρετικά δώστε λίστα γλωσσών μέσω `ocrEngine.Language = new[] { OcrLanguage.English, OcrLanguage.Cyrillic }`. |
| **Large documents** | Επεξεργαστείτε μία σελίδα τη φορά για να κρατήσετε τη χρήση μνήμης χαμηλή· ο κινητήρας υποστηρίζει πολυ‑σελίδες TIFF. |
| **Incorrect characters** | Βεβαιωθείτε ότι έχετε επιλέξει το σωστό `OcrLanguage`; η λανθασμένη γλώσσα μειώνει την ακρίβεια όταν **convert image to text**. |
| **JSON missing fields** | Βεβαιωθείτε ότι χρησιμοποιείτε την έκδοση Aspose.OCR 23.6 ή νεότερη· παλαιότερες εκδόσεις δεν εκθέτουν τη μέθοδο `SaveJson`. |

## Συχνές ερωτήσεις

**Q: Μπορώ να λάβω το αποτέλεσμα OCR ως byte array αντί για αρχείο;**  
A: Ναι. Χρησιμοποιήστε `ocrEngine.SaveJson(Stream)` για να γράψετε απευθείας σε `MemoryStream`, έπειτα καλέστε `stream.ToArray()`.

**Q: Υποστηρίζει ο κινητήρας είσοδο PDF;**  
A: Το Aspose.OCR μπορεί να δεχτεί σελίδες PDF που έχουν μετατραπεί σε εικόνες μέσω Aspose.PDF, αλλά ο ίδιος ο κινητήρας OCR λειτουργεί μόνο σε raster εικόνες. Μετατρέψτε τα PDF σε εικόνες πρώτα, έπειτα **load image for ocr**.

**Q: Πώς διαχειρίζομαι γραφές από δεξιά προς αριστερά όπως η αραβική;**  
A: Ορίστε `ocrEngine.Language = OcrLanguage.Arabic`. Το JSON περιλαμβάνει τη σωστή κατεύθυνση κειμένου, την οποία μπορείτε να αποδώσετε σε UI frameworks που υποστηρίζουν RTL.

## Συμπέρασμα

Τώρα έχετε μια πλήρη λύση για **ocr image to json** σε C#. Φορτώνοντας μια εικόνα, ρυθμίζοντας τη γλώσσα, τρέχοντας τον κινητήρα OCR και εξάγοντας το αποτέλεσμα ως JSON, μπορείτε να **extract text from image**, **convert image to text** και **recognize text from photo** σε μια ενιαία, απλοποιημένη ροή εργασίας.  

Από εδώ μπορείτε να εξερευνήσετε:

- Ενσωμάτωση του JSON output σε Web API (`ASP.NET Core`)  
- Αποθήκευση του αποτελέσματος σε NoSQL βάση δεδομένων όπως MongoDB  
- Προσθήκη post‑processing για διόρθωση κοινών σφαλμάτων OCR  

Μη διστάσετε να πειραματιστείτε με διαφορετικές γλώσσες, μορφές εικόνας και επιλογές εξόδου ώστε να ταιριάζουν στις ανάγκες του έργου σας. Καλή προγραμματιστική διασκέδαση!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [recognize text from image in C# – Complete Guide to OCR and JSON](/ocr/english/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/)
- [Convert Image to Text in C# with Aspose OCR – Step‑by‑Step Guide](/ocr/english/net/text-recognition/convert-image-to-text-in-c-with-aspose-ocr-step-by-step-guid/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}