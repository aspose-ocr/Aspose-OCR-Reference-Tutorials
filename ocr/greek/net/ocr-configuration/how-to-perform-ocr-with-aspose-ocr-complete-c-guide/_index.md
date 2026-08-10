---
category: general
date: 2026-07-05
description: Μάθετε πώς να εκτελείτε OCR σε C# χρησιμοποιώντας το Aspose.OCR, να ορίζετε
  τη γλώσσα, να φορτώνετε εικόνα OCR και να μετατρέπετε PNG σε JSON σε λίγα εύκολα
  βήματα.
draft: false
keywords:
- how to perform OCR
- how to set language
- convert png to json
- load image ocr
- set ocr language
language: el
og_description: Πώς να εκτελέσετε OCR σε C# με το Aspose.OCR, να ορίσετε τη γλώσσα
  OCR, να φορτώσετε εικόνα OCR και να μετατρέψετε PNG σε JSON—όλα σε έναν σύντομο
  οδηγό.
og_title: Πώς να εκτελέσετε OCR με το Aspose.OCR – Πλήρης οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Learn how to perform OCR in C# using Aspose.OCR, set language, load
    image OCR, and convert PNG to JSON in a few easy steps.
  headline: How to Perform OCR with Aspose.OCR – Complete C# Guide
  type: TechArticle
- description: Learn how to perform OCR in C# using Aspose.OCR, set language, load
    image OCR, and convert PNG to JSON in a few easy steps.
  name: How to Perform OCR with Aspose.OCR – Complete C# Guide
  steps:
  - name: – Install the Aspose.OCR NuGet Package
    text: 'Before you can even think about **how to perform OCR**, the library has
      to be on your machine. Open a terminal in your project folder and run:'
  - name: – Load the Image for OCR (load image OCR)
    text: 'Now that the package is ready, you need to **load image OCR**. The engine
      expects an `ImageStream`, which you can create from a file path, a `MemoryStream`,
      or even a byte array. Here’s the simplest approach using a PNG file on disk:'
  - name: – Set the OCR Language (how to set language / set OCR language)
    text: Aspose.OCR supports over 60 languages, but it defaults to English. If your
      document is in another language, you must tell the engine which one to use.
      That’s where **how to set language** and **set OCR language** come into play.
  - name: – Perform OCR and Convert PNG to JSON
    text: 'With the image loaded and the language set, the final piece is to run the
      OCR engine and **convert PNG to JSON**. Aspose.OCR makes this a one‑liner:'
  - name: Full Working Example (All Steps Combined)
    text: 'Putting everything together, here’s a compact program you can compile and
      run instantly:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: Πώς να εκτελέσετε OCR με το Aspose.OCR – Πλήρης οδηγός C#
url: /el/net/ocr-configuration/how-to-perform-ocr-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εκτελέσετε OCR με το Aspose.OCR – Πλήρης Οδηγός C#

Έχετε αναρωτηθεί ποτέ **πώς να εκτελέσετε OCR** σε ένα σαρωμένο τιμολόγιο χωρίς να γράψετε πολλή επαναλαμβανόμενη κώδικα; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν δυσκολίες όταν πρέπει να εξάγουν κείμενο από εικόνες, ειδικά όταν η επόμενη μορφή πρέπει να είναι JSON για εύκολη κατανάλωση.

Σε αυτό το tutorial θα δείτε ακριβώς **πώς να εκτελέσετε OCR** χρησιμοποιώντας τη βιβλιοθήκη Aspose.OCR, θα μάθετε **πώς να ορίσετε τη γλώσσα**, θα ανακαλύψετε τον καλύτερο τρόπο να **φορτώσετε εικόνα OCR**, και θα λάβετε ένα έτοιμο‑για‑εκτέλεση απόσπασμα που **μετατρέπει PNG σε JSON**. Στο τέλος, θα έχετε μια σταθερή, έτοιμη για παραγωγή λύση που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET.

![Διάγραμμα που απεικονίζει πώς να εκτελέσετε OCR με το Aspose.OCR σε C#](ocr-flow.png "πώς να εκτελέσετε OCR")

## Τι Θα Μάθετε

- Τα ελάχιστα προαπαιτούμενα για την εκτέλεση του Aspose.OCR.
- Κώδικας βήμα‑βήμα που **φορτώνει μια εικόνα OCR**, επιλέγει τη σωστή γλώσσα, και **μετατρέπει PNG σε JSON**.
- Γιατί η ρύθμιση της σωστής γλώσσας OCR είναι σημαντική και πώς να το κάνετε με ασφάλεια.
- Κοινά προβλήματα (μεγάλα αρχεία, μη υποστηριζόμενες γλώσσες) και πώς να τα αποφύγετε.
- Ένα πλήρες, εκτελέσιμο παράδειγμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε αμέσως.

## Πώς να Εκτελέσετε OCR με το Aspose.OCR σε C#

### Βήμα 1 – Εγκατάσταση του Πακέτου Aspose.OCR NuGet

Πριν μπορέσετε ακόμη και να σκεφτείτε **πώς να εκτελέσετε OCR**, η βιβλιοθήκη πρέπει να είναι στον υπολογιστή σας. Ανοίξτε ένα τερματικό στο φάκελο του έργου σας και εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

Αυτή η εντολή φέρνει την πιο πρόσφατη σταθερή έκδοση (από τον Ιούλιο 2026, έκδοση 23.10). Χωρίς επιπλέον DLLs, χωρίς χειροκίνητη ρύθμιση—απλώς μια καθαρή αναφορά πακέτου.

### Βήμα 2 – Φόρτωση της Εικόνας για OCR (load image OCR)

Τώρα που το πακέτο είναι έτοιμο, πρέπει να **φορτώσετε εικόνα OCR**. Η μηχανή αναμένει ένα `ImageStream`, το οποίο μπορείτε να δημιουργήσετε από διαδρομή αρχείου, ένα `MemoryStream`, ή ακόμη και από έναν πίνακα byte. Ακολουθεί η πιο απλή προσέγγιση χρησιμοποιώντας ένα αρχείο PNG στο δίσκο:

```csharp
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

// Create an OCR engine instance
var engine = new OcrEngine();

// Load the image you want to process
engine.Image = ImageStream.FromFile(@"C:\Invoices\invoice.png");

// Optional: verify that the image was loaded
if (engine.Image == null)
{
    throw new InvalidOperationException("Failed to load the image. Check the file path.");
}
```

> **Γιατί είναι σημαντικό:** Η σωστή φόρτωση της εικόνας είναι η βάση κάθε pipeline OCR. Αν η εικόνα δεν φορτωθεί, η μηχανή ρίχνει μια ασαφή `NullReferenceException`, που είναι εφιάλτης για αποσφαλμάτωση.

### Βήμα 3 – Ορισμός της Γλώσσας OCR (how to set language / set OCR language)

Το Aspose.OCR υποστηρίζει πάνω από 60 γλώσσες, αλλά η προεπιλογή είναι τα Αγγλικά. Αν το έγγραφό σας είναι σε άλλη γλώσσα, πρέπει να ενημερώσετε τη μηχανή ποια να χρησιμοποιήσει. Εκεί έρχονται σε δράση τα **πώς να ορίσετε τη γλώσσα** και **ορισμός γλώσσας OCR**.

```csharp
// Specify the language of the text in the image
engine.Language = OcrLanguage.English; // Change to OcrLanguage.Spanish, etc.

// You can also set multiple languages if needed
// engine.Language = OcrLanguage.English | OcrLanguage.French;
```

> **Συμβουλή:** Πάντα ορίζετε τη γλώσσα ρητά. Ακόμη και αν το κείμενό σας είναι στα Αγγλικά, η ρητή ανάθεση `OcrLanguage.English` μπορεί να βελτιώσει την ακρίβεια επειδή η μηχανή παραλείπει το βήμα ανίχνευσης γλώσσας.

### Βήμα 4 – Εκτέλεση OCR και Μετατροπή PNG σε JSON

Με την εικόνα φορτωμένη και τη γλώσσα ορισμένη, το τελευταίο βήμα είναι η εκτέλεση της μηχανής OCR και **η μετατροπή PNG σε JSON**. Το Aspose.OCR το κάνει με μία μόνο γραμμή κώδικα:

```csharp
// Perform OCR and save the recognized text as JSON
engine.Save(@"C:\Invoices\invoice.json", OcrOutputFormat.Json);
```

Το παραγόμενο JSON φαίνεται ως εξής:

```json
{
  "Pages": [
    {
      "Text": "Invoice #12345\nDate: 2026-07-01\nTotal: $1,250.00\n..."
    }
  ]
}
```

Αυτή η δομή είναι τέλεια για downstream APIs, εισαγωγές σε βάσεις δεδομένων ή γρήγορες προεπισκοπήσεις UI.

### Πλήρες Παράδειγμα Εργασίας (Όλα τα Βήματα Συνδυασμένα)

Συνδυάζοντας όλα, εδώ είναι ένα συμπαγές πρόγραμμα που μπορείτε να μεταγλωττίσετε και να εκτελέσετε αμέσως:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine
        var engine = new OcrEngine();

        // 2️⃣ Load the PNG image (load image OCR)
        string inputPath = @"C:\Invoices\invoice.png";
        engine.Image = ImageStream.FromFile(inputPath);
        if (engine.Image == null)
        {
            Console.WriteLine($"Unable to load image from {inputPath}");
            return;
        }

        // 3️⃣ Set the language (how to set language / set OCR language)
        engine.Language = OcrLanguage.English; // Adjust as needed

        // 4️⃣ Run OCR and write JSON (convert PNG to JSON)
        string outputPath = @"C:\Invoices\invoice.json";
        engine.Save(outputPath, OcrOutputFormat.Json);

        Console.WriteLine($"OCR complete! JSON saved to {outputPath}");
    }
}
```

**Αναμενόμενη έξοδος στην κονσόλα:**

```
OCR complete! JSON saved to C:\Invoices\invoice.json
```

Ανοίξτε το αρχείο JSON και θα δείτε το εξαγόμενο κείμενο έτοιμο για ό,τι χρειάζεστε στη συνέχεια.

## Συνηθισμένες Ακραίες Περιπτώσεις & Πώς να τις Διαχειριστείτε

| Κατάσταση | Τι να Προσέξετε | Προτεινόμενη Διόρθωση |
|-----------|-------------------|-----------------|
| **Μεγάλο PNG (>10 MB)** | Αιχμές μνήμης, πιο αργή επεξεργασία | Μειώστε πρώτα το μέγεθος της εικόνας χρησιμοποιώντας `engine.Image = ImageStream.FromFile(...).Resize(1024, 0)` |
| **Μη υποστηριζόμενη γλώσσα** | `ArgumentException` κατά τον ορισμό του `engine.Language` | Επαληθεύστε το enum γλώσσας μέσω `OcrLanguage.GetSupportedLanguages()` |
| **Κατεστραμμένο αρχείο εικόνας** | `InvalidOperationException` κατά τη φόρτωση | Τυλίξτε την κλήση φόρτωσης σε `try/catch` και επαληθεύστε το αρχείο με `File.Exists` |
| **Απαιτείται απλό κείμενο αντί για JSON** | Λάθος μορφή εξόδου | Χρησιμοποιήστε `engine.Save(outputPath, OcrOutputFormat.PlainText)` |

Προβλέποντας αυτά τα σενάρια, θα αποφύγετε τα συνηθισμένα «γιατί αποτυγχάνει το OCR μου;» προβλήματα.

## Επαγγελματικές Συμβουλές για Καλύτερη Ακρίβεια

1. **Προεπεξεργασία της εικόνας** – Αυξήστε την αντίθεση ή μετατρέψτε σε γκρι κλίμακα πριν την δώσετε στη μηχανή. Το Aspose.OCR προσφέρει `engine.Image = engine.Image.AdjustContrast(1.2f)` για γρήγορες ρυθμίσεις.  
2. **Διόρθωση κλίσης σαρωμένων εικόνων** – Χρησιμοποιήστε `engine.Image = engine.Image.Deskew()` αν το έγγραφο δεν είναι τέλεια ευθυγραμμισμένο.  
3. **Επεξεργασία σε παρτίδες** – Όταν διαχειρίζεστε δεκάδες τιμολόγια, επαναχρησιμοποιήστε το ίδιο αντικείμενο `OcrEngine`; αποθηκεύει τα μοντέλα γλώσσας και επιταχύνει τις επόμενες κλήσεις.  
4. **Επικύρωση JSON** – Μετά την αποθήκευση, εκτελέστε έναν γρήγορο έλεγχο σχήματος για να διασφαλίσετε ότι η έξοδος ταιριάζει με τα downstream συμβόλαιά σας.

## Ανακεφαλαίωση: Πώς να Εκτελέσετε OCR Από‑Αρχή‑Μέχρι‑Τέλος

- Εγκαταστήστε το Aspose.OCR μέσω NuGet.  
- **Φορτώστε εικόνα OCR** με `ImageStream.FromFile`.  
- **Ορίστε τη γλώσσα OCR** (ή **πώς να ορίσετε τη γλώσσα**) χρησιμοποιώντας `engine.Language`.  
- Καλέστε `engine.Save(..., OcrOutputFormat.Json)` για **να μετατρέψετε PNG σε JSON**.  

Αυτή είναι η πλήρης ροή εργασίας για **πώς να εκτελέσετε OCR** με καθαρό, συντηρήσιμο τρόπο.

## Τι Ακολουθεί;

- Πειραματιστείτε με **ορισμό γλώσσας OCR** για πολύγλωσσα τιμολόγια (π.χ., Αγγλικά | Ισπανικά).  
- Αντικαταστήστε το `OcrOutputFormat.Json` με `OcrOutputFormat.PlainText` αν χρειάζεστε μόνο ακατέργαστες συμβολοσειρές.  
- Ενσωματώστε την έξοδο JSON σε Azure Function ή AWS Lambda για serverless επεξεργασία.  

Μη διστάσετε να τροποποιήσετε το παράδειγμα, να προσθέσετε καταγραφή σφαλμάτων, ή να το τυλίξετε σε επαναχρησιμοποιήσιμη κλάση υπηρεσίας. Ο ουρανός είναι το όριο μόλις κυριαρχήσετε τα βασικά του **πώς να εκτελέσετε OCR** με το Aspose.OCR.

Καλή προγραμματιστική, και εύχομαι η εξαγωγή κειμένου σας να είναι πάντα ακριβής!

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Χρησιμοποιήσετε το Aspose OCR για Αποτέλεσμα JSON στην Αναγνώριση Εικόνας](/ocr/english/net/text-recognition/get-result-as-json/)
- [Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Πώς να Εξάγετε Κείμενο από Εικόνα Χρησιμοποιώντας Aspose.OCR για .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}