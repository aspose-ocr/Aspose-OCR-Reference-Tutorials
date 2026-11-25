---
category: general
date: 2026-06-25
description: Εκτελέστε OCR σε εικόνα χρησιμοποιώντας C# και Aspose OCR, στη συνέχεια
  γράψτε αρχείο JSON με C# και αποθηκεύστε το αρχείο JSON με C# με ένα σαφές, βήμα‑βήμα
  παράδειγμα.
draft: false
keywords:
- perform ocr on image
- c# write json file
- save json file c#
- aspose ocr example
- load image for ocr
language: el
og_description: Πραγματοποιήστε OCR σε εικόνα με C# χρησιμοποιώντας το Aspose OCR,
  στη συνέχεια αποθηκεύστε το αποτέλεσμα ως JSON. Ένας πλήρης, εκτελέσιμος οδηγός
  για προγραμματιστές.
og_title: Εκτέλεση OCR σε εικόνα σε C# – Πλήρες παράδειγμα Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Perform OCR on image using C# and Aspose OCR, then c# write json file
    and save json file c# with a clear, step‑by‑step example.
  headline: Perform OCR on Image in C# – Complete Aspose OCR Example
  type: TechArticle
- questions:
  - answer: It builds a platform‑independent path, preventing “file not found” errors
      on Windows vs. Linux.
    question: Why use `Path.Combine`?
  - answer: The engine scans the bitmap, applies language‑specific classifiers, and
      builds a hierarchical result object containing pages, blocks, lines, and words.
    question: What happens under the hood?
  - answer: Human‑readable output makes debugging easier, especially when you later
      feed the JSON into other services.
    question: Why pretty‑print?
  - answer: Wrap the write in a try/catch and surface a clear message—this helps in
      Docker containers where the working directory may be mounted read‑only.
    question: What if the folder is read‑only?
  type: FAQPage
tags:
- C#
- Aspose OCR
- JSON
- Image Processing
title: Εκτέλεση OCR σε εικόνα με C# – Πλήρες παράδειγμα Aspose OCR
url: /el/net/text-recognition/perform-ocr-on-image-in-c-complete-aspose-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε εικόνα με C# – Πλήρες παράδειγμα Aspose OCR

Ever needed to **perform OCR on image** files from a C# console app but weren’t sure how to get the text out and store it nicely? You’re not the only one. In many automation pipelines—think invoice digitization or multilingual document archiving—the ability to turn a picture into searchable text and then **c# write json file** is a real productivity booster.

Έχετε ποτέ χρειαστεί να **perform OCR on image** αρχεία από μια κονσόλα C# αλλά δεν ήσασταν σίγουροι πώς να εξάγετε το κείμενο και να το αποθηκεύσετε σωστά; Δεν είστε οι μόνοι. Σε πολλά αυτοματοποιημένα pipelines—σκεφτείτε την ψηφιοποίηση τιμολογίων ή την αρχειοθέτηση πολυγλωσσικών εγγράφων—η δυνατότητα να μετατρέψετε μια εικόνα σε αναζητήσιμο κείμενο και στη συνέχεια **c# write json file** είναι ένας πραγματικός ενισχυτής παραγωγικότητας.

In this tutorial we’ll walk through an end‑to‑end **aspose ocr example** that loads an image, extracts the characters, formats the result as pretty‑printed JSON, and finally **save json file c#** to disk. By the end you’ll have a self‑contained program you can drop into any .NET project.

Σε αυτό το tutorial θα περάσουμε βήμα-βήμα ένα end‑to‑end **aspose ocr example** που φορτώνει μια εικόνα, εξάγει τους χαρακτήρες, μορφοποιεί το αποτέλεσμα ως pretty‑printed JSON, και τελικά **save json file c#** στο δίσκο. Στο τέλος θα έχετε ένα αυτόνομο πρόγραμμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET.

![Perform OCR on image example](perform-ocr-on-image.png "Screenshot showing OCR result – perform ocr on image")

## Τι θα πετύχετε

- **Load image for OCR** χρησιμοποιώντας το `OcrImage.FromFile` του Aspose.OCR.
- **Perform OCR on image** με μία κλήση μεθόδου.
- Μετατρέψτε το αποτέλεσμα αναγνώρισης σε ένα ωραία μορφοποιημένο JSON string.
- **Save JSON file C#** με τη χρήση του `File.WriteAllText`.
- Κατανοήστε τις κοινές παγίδες (έλλειψη πακέτου NuGet, μη υποστηριζόμενες μορφές εικόνας, διαχείριση Unicode).

No external services, no cloud keys—just pure C# code that runs locally.

Χωρίς εξωτερικές υπηρεσίες, χωρίς κλειδιά cloud—απλώς καθαρός κώδικας C# που εκτελείται τοπικά.

---

## Βήμα 1: Ρύθμιση του έργου και προσθήκη του Aspose.OCR

Before we can **perform OCR on image**, we need the right libraries.

Πριν μπορέσουμε να **perform OCR on image**, χρειαζόμαστε τις σωστές βιβλιοθήκες.

1. Ανοίξτε το Visual Studio (ή το αγαπημένο σας IDE) και δημιουργήστε μια νέα **Console App (.NET 6 or later)**.  
2. Ανοίξτε το NuGet Package Manager και εγκαταστήστε το `Aspose.OCR`:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** If you target .NET Framework, the same package works, but make sure you have at least .NET 4.6.2.

> **Συμβουλή επαγγελματία:** Αν στοχεύετε στο .NET Framework, το ίδιο πακέτο λειτουργεί, αλλά βεβαιωθείτε ότι έχετε τουλάχιστον .NET 4.6.2.

> **Why this matters:** Aspose.OCR bundles language packs and a high‑performance engine, so you don’t have to ship separate OCR binaries.

> **Γιατί είναι σημαντικό:** Το Aspose.OCR περιλαμβάνει πακέτα γλωσσών και μια υψηλής απόδοσης μηχανή, ώστε να μην χρειάζεται να διανείμετε ξεχωριστά OCR binaries.

---

## Βήμα 2: Φόρτωση της εικόνας για OCR

The engine needs an `OcrImage` instance. This is where the **load image for OCR** step comes in.

Η μηχανή χρειάζεται μια παρουσία `OcrImage`. Εδώ έρχεται το βήμα **load image for OCR**.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // Create the OCR engine
        var ocrEngine = new OcrEngine();

        // 👉 Load the image you want to recognize
        var imagePath = Path.Combine(Environment.CurrentDirectory, "multi_lang.png");
        var image = OcrImage.FromFile(imagePath);

        // Continue with recognition...
```

- **Why use `Path.Combine`?** Δημιουργεί μια ανεξάρτητη από την πλατφόρμα διαδρομή, αποτρέποντας σφάλματα “file not found” σε Windows vs. Linux.
- **Supported formats:** PNG, JPEG, BMP, TIFF. Αν δώσετε ένα PDF, το Aspose.OCR θα ρίξει `NotSupportedException`.

**Supported formats:** PNG, JPEG, BMP, TIFF. Αν δώσετε ένα PDF, το Aspose.OCR θα ρίξει `NotSupportedException`.

---

## Βήμα 3: Εκτέλεση OCR στην εικόνα

Now the core operation. One line does the heavy lifting.

Τώρα η κύρια λειτουργία. Μία γραμμή κάνει το σκληρό έργο.

```csharp
        // Perform OCR recognition on the image
        var ocrResult = ocrEngine.Recognize(image);
```

- **What happens under the hood?** Η μηχανή σαρώει το bitmap, εφαρμόζει ταξινομητές ειδικούς για τη γλώσσα, και δημιουργεί ένα ιεραρχικό αντικείμενο αποτελέσματος που περιέχει σελίδες, μπλοκ, γραμμές και λέξεις.
- **Edge case:** Αν η εικόνα είναι κενή ή πολύ θορυβώδης, το `ocrResult` μπορεί να περιέχει ένα κενό πεδίο `Text`. Μπορείτε να ελέγξετε `ocrResult.IsEmpty` για να το προστατέψετε.

**Edge case:** Αν η εικόνα είναι κενή ή πολύ θορυβώδης, το `ocrResult` μπορεί να περιέχει ένα κενό πεδίο `Text`. Μπορείτε να ελέγξετε `ocrResult.IsEmpty` για να το προστατέψετε.

---

## Βήμα 4: Μετατροπή του αποτελέσματος σε JSON (c# write json file)

Aspose.OCR’s `OcrResult` already knows how to serialize itself. We’ll ask it for a *pretty‑printed* JSON string.

Το `OcrResult` του Aspose.OCR ήδη ξέρει πώς να σειριοποιηθεί. Θα του ζητήσουμε ένα *pretty‑printed* JSON string.

```csharp
        // Convert the recognition result to a nicely formatted JSON string
        string jsonResult = ocrResult.ToJson(prettyPrint: true);
```

- **Why pretty‑print?** Η έξοδος που μπορεί να διαβαστεί από άνθρωπο κάνει το debugging πιο εύκολο, ειδικά όταν αργότερα τροφοδοτείτε το JSON σε άλλες υπηρεσίες.
- **Alternative:** Αν χρειάζεστε ένα συμπαγές payload για μετάδοση δικτύου, ορίστε `prettyPrint: false`.

**Alternative:** Αν χρειάζεστε ένα συμπαγές payload για μετάδοση δικτύου, ορίστε `prettyPrint: false`.

---

## Βήμα 5: Αποθήκευση αρχείου JSON C# – Διατήρηση του αποτελέσματος

Finally, we write the JSON to disk. This is the **save json file c#** part of the tutorial.

Τέλος, γράφουμε το JSON στο δίσκο. Αυτό είναι το τμήμα **save json file c#** του tutorial.

```csharp
        // Define where the JSON will be saved
        var jsonPath = Path.Combine(Environment.CurrentDirectory, "result.json");

        // Write the JSON string to the file system
        File.WriteAllText(jsonPath, jsonResult);

        // Inform the user
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

- **Encoding note:** Το `WriteAllText` χρησιμοποιεί UTF‑8 εξ ορισμού, το οποίο διατηρεί τυχόν χαρακτήρες Unicode που εξάγονται από πολυγλωσσικές εικόνες.
- **What if the folder is read‑only?** Τυλίξτε τη γραφή σε try/catch και εμφανίστε ένα σαφές μήνυμα—αυτό βοηθά σε Docker containers όπου ο φάκελος εργασίας μπορεί να είναι προσαρτημένος μόνο για ανάγνωση.

**What if the folder is read‑only?** Τυλίξτε τη γραφή σε try/catch και εμφανίστε ένα σαφές μήνυμα—αυτό βοηθά σε Docker containers όπου ο φάκελος εργασίας μπορεί να είναι προσαρτημένος μόνο για ανάγνωση.

---

## Πλήρες λειτουργικό παράδειγμα

Putting it all together, here’s the complete program you can copy‑paste into `Program.cs` and run immediately (assuming `multi_lang.png` sits next to the executable).

Συνδυάζοντας όλα, εδώ είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε στο `Program.cs` και να τρέξετε αμέσως (υποθέτοντας ότι το `multi_lang.png` βρίσκεται δίπλα στο εκτελέσιμο).

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // Step 1: Create OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image for OCR
        var imagePath = Path.Combine(Environment.CurrentDirectory, "multi_lang.png");
        var image = OcrImage.FromFile(imagePath);

        // Step 3: Perform OCR on image
        var ocrResult = ocrEngine.Recognize(image);

        // Optional: guard against empty results
        if (ocrResult == null || ocrResult.IsEmpty)
        {
            Console.WriteLine("No text recognized. Check the image quality.");
            return;
        }

        // Step 4: Convert result to pretty‑printed JSON
        string jsonResult = ocrResult.ToJson(prettyPrint: true);

        // Step 5: Save JSON file C#
        var jsonPath = Path.Combine(Environment.CurrentDirectory, "result.json");
        File.WriteAllText(jsonPath, jsonResult);

        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

### Αναμενόμενη έξοδος

When you run the program, you should see something like:

Όταν εκτελέσετε το πρόγραμμα, θα πρέπει να δείτε κάτι όπως:

```
JSON saved to C:\Projects\OcrDemo\result.json
```

Opening `result.json` reveals a structured document:

Ανοίγοντας το `result.json` αποκαλύπτεται ένα δομημένο έγγραφο:

```json
{
  "Pages": [
    {
      "Blocks": [
        {
          "Lines": [
            {
              "Words": [
                { "Text": "Hello", "Confidence": 0.98 },
                { "Text": "World", "Confidence": 0.97 }
              ]
            }
          ]
        }
      ]
    }
  ]
}
```

The exact content varies based on the source image, but the JSON schema stays consistent—ideal for downstream processing (e.g., feeding into ElasticSearch or a NoSQL store).

Το ακριβές περιεχόμενο διαφέρει ανάλογα με την εικόνα προέλευσης, αλλά το σχήμα JSON παραμένει συνεπές—ιδανικό για επεξεργασία downstream (π.χ., τροφοδοσία σε ElasticSearch ή αποθήκη NoSQL).

---

## Συχνές ερωτήσεις & παγίδες

| Ερώτηση | Απάντηση |
|----------|--------|
| **Do I need a license?** | Το Aspose.OCR λειτουργεί σε λειτουργία αξιολόγησης για έως 20 σελίδες. Για παραγωγή θα χρειαστείτε αρχείο άδειας (`Aspose.OCR.lic`). |
| **What languages are supported?** | English, French, German, Spanish, Chinese, Japanese, Arabic, και πολλά άλλα. Ορίστε `ocrEngine.Language = Language.English;` για περιορισμό ή `ocrEngine.Language = Language.All;` για αυτόματη ανίχνευση. |
| **Can I process PDFs directly?** | Δεν είναι δυνατόν μόνο με Aspose.OCR. Συνδυάστε το με Aspose.PDF για να rasterize τις σελίδες σε εικόνες πρώτα. |
| **Why is the JSON empty?** | Συνήθως μια εικόνα χαμηλής αντίθεσης. Δοκιμάστε να αυξήσετε την αντίθεση ή χρησιμοποιήστε `ocrEngine.Config.PreprocessOptions` για βελτίωση του bitmap. |
| **Is the JSON schema stable?** | Ναι, το Aspose εγγυάται συμβατότητα προς τα πίσω για την έξοδο `ToJson` σε μικρές εκδόσεις. |

---

## Επέκταση του παραδείγματος

Now that you know how to **perform OCR on image** and **save json file c#**, you might want to:

Τώρα που ξέρετε πώς να **perform OCR on image** και **save json file c#**, ίσως θέλετε να:

- **Batch process** έναν φάκελο εικόνων (`Directory.GetFiles(..., "*.png")`).
- **Upload the JSON** σε ένα REST API χρησιμοποιώντας το `HttpClient`.
- **Insert the text** σε μια βάση δεδομένων για αρχειοθέτηση με δυνατότητα αναζήτησης.
- **Add image preprocessing** (deskew, binarization) μέσω του `ocrEngine.Config.PreprocessOptions`.

All of these follow the same pattern: load → recognize → serialize → persist.

Όλα αυτά ακολουθούν το ίδιο μοτίβο: φόρτωση → αναγνώριση → σειριοποίηση → αποθήκευση.

---

## Συμπέρασμα

We’ve just completed a concise **aspose ocr example** that demonstrates how to **perform OCR on image**, transform the result into a **pretty‑printed JSON**, and **save JSON file C#** with only a handful of lines. The approach is straightforward, requires no external services, and can be expanded to suit any production workflow.

Μόλις ολοκληρώσαμε ένα σύντομο **aspose ocr example** που δείχνει πώς να **perform OCR on image**, να μετατρέψετε το αποτέλεσμα σε **pretty‑printed JSON**, και να **save JSON file C#** με μόνο λίγες γραμμές. Η προσέγγιση είναι απλή, δεν απαιτεί εξωτερικές υπηρεσίες, και μπορεί να επεκταθεί για οποιαδήποτε παραγωγική ροή εργασίας.

Give it a spin, tweak the language settings, and watch the OCR accuracy improve. If you hit any snags, check the Aspose.OCR documentation or drop a comment below—happy coding!

Δοκιμάστε το, προσαρμόστε τις ρυθμίσεις γλώσσας, και παρακολουθήστε τη βελτίωση της ακρίβειας OCR. Αν αντιμετωπίσετε προβλήματα, ελέγξτε την τεκμηρίωση του Aspose.OCR ή αφήστε ένα σχόλιο παρακάτω—καλή προγραμματιστική!

## Τι πρέπει να μάθετε στη συνέχεια;

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να χρησιμοποιήσετε το Aspose OCR για αποτέλεσμα JSON στην αναγνώριση εικόνας](/ocr/english/net/text-recognition/get-result-as-json/)
- [Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας το Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Πώς να εκτελέσετε εξαγωγή κειμένου εικόνας από ροή χρησιμοποιώντας το Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}