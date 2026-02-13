---
category: general
date: 2026-02-13
description: Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας το Aspose OCR σε C#. Μάθετε
  πώς να διαβάζετε κείμενο από jpg και να εκτελείτε OCR σε εικόνα με ένα πλήρες, εκτελέσιμο
  παράδειγμα.
draft: false
keywords:
- extract text from image
- read text from jpg
- run OCR on image
- Aspose OCR C#
- OCR language packs
language: el
og_description: Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας το Aspose OCR σε C#. Αυτός
  ο οδηγός δείχνει πώς να διαβάσετε κείμενο από jpg και να εκτελέσετε OCR στην εικόνα
  με ένα πλήρες παράδειγμα κώδικα.
og_title: Εξαγωγή κειμένου από εικόνα με Aspose OCR – Γρήγορη εκκίνηση C#
tags:
- C#
- OCR
- Aspose
title: Εξαγωγή κειμένου από εικόνα με Aspose OCR – Γρήγορη εκκίνηση C#
url: /el/net/text-recognition/extract-text-from-image-with-aspose-ocr-c-quickstart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Γρήγορη Εκκίνηση C#

Έχετε χρειαστεί ποτέ να **εξάγετε κείμενο από εικόνα** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη να επιλέξετε; Δεν είστε μόνοι—οι προγραμματιστές αντιμετωπίζουν συνεχώς την ανάγνωση κειμένου από αρχεία jpg, ειδικά όταν το περιεχόμενο είναι σε μη λατινικό αλφάβητο. Τα καλά νέα; Με το Aspose OCR μπορείτε να εκτελέσετε OCR σε αρχεία εικόνας με λίγες μόνο γραμμές κώδικα C#, και η βιβλιοθήκη φροντίζει για τη λήψη των πακέτων γλώσσας κατά απαίτηση.

Σε αυτό το tutorial θα περάσουμε από ένα πλήρες, end‑to‑end παράδειγμα που δείχνει πώς να **εξάγετε κείμενο από εικόνα** χρησιμοποιώντας το Aspose OCR, να περιορίσετε την αναγνώριση στα Ρωσικά και να εκτυπώσετε το αποτέλεσμα στην κονσόλα. Στο τέλος θα μπορείτε να διαβάζετε κείμενο από αρχεία jpg, να τρέχετε OCR σε εικόνες οποιουδήποτε μεγέθους και να προσαρμόζετε τον κώδικα για άλλες γλώσσες με ελάχιστες αλλαγές.

> **Τι θα μάθετε**
> * Πώς να εγκαταστήσετε και να αναφέρετε το Aspose OCR σε ένα έργο .NET.  
> * Τα ακριβή βήματα για **εξαγωγή κειμένου από εικόνα**—αρχικοποίηση της μηχανής, επιλογή γλώσσας και κλήση του `RecognizeImage`.  
> * Γιατί μπορεί να θέλετε να κλειδώσετε τη μηχανή σε ένα μόνο πακέτο γλώσσας (ταχύτητα, ακρίβεια).  
> * Συνηθισμένα προβλήματα όπως ελλιπή αρχεία ή μη υποστηριζόμενες μορφές, και πώς να τα αντιμετωπίσετε με χάρη.  

## Προαπαιτήσεις

Πριν βουτήξουμε, βεβαιωθείτε ότι έχετε τα παρακάτω στον υπολογιστή σας:

| Requirement | Reason |
|-------------|--------|
| .NET 6.0 SDK ή νεότερο | Το Aspose OCR στοχεύει στο .NET Standard 2.0+, οπότε το .NET 6 σας δίνει τις πιο πρόσφατες δυνατότητες του runtime. |
| Visual Studio 2022 (ή οποιοδήποτε IDE προτιμάτε) | Χρήσιμο για debugging, αλλά όχι απολύτως απαραίτητο. |
| Ένα αρχείο εικόνας (`cyrillic_sample.jpg`) που περιέχει κυριλλικό κείμενο | Θα χρησιμοποιήσουμε αυτό το αρχείο για να δείξουμε **ανάγνωση κειμένου από jpg**. |
| Σύνδεση στο Internet (μόνο στην πρώτη εκτέλεση) | Το Aspose OCR κατεβάζει τα πακέτα γλώσσας κατά απαίτηση. |

Αν λείπει κάτι από αυτά, αποκτήστε το τώρα—δεν χρειάζεται επανεκκίνηση μετά την εγκατάσταση του SDK.

## Βήμα 1: Εγκατάσταση του Πακέτου NuGet Aspose OCR

Το πρώτο πράγμα που χρειάζεστε είναι η βιβλιοθήκη Aspose OCR. Ανοίξτε ένα τερματικό στον φάκελο του έργου σας και εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

Αυτή η εντολή κατεβάζει την πιο πρόσφατη σταθερή έκδοση (από τον Φεβρουάριο 2026 είναι η 23.12) και την προσθέτει στο `.csproj`. Το πακέτο περιλαμβάνει τον πυρήνα της μηχανής OCR και έναν ελαφρύ downloader για τα πακέτα γλώσσας, ώστε να μην χρειάζεται να συμπεριλάβετε τεράστια αρχεία στην εφαρμογή σας.

> **Pro tip:** Αν εργάζεστε πίσω από εταιρικό proxy, ορίστε τη μεταβλητή περιβάλλοντος `http_proxy` πριν τρέξετε την εντολή για να αποφύγετε σφάλματα λήψης.

## Βήμα 2: Δημιουργία Σκελετού Εφαρμογής Κονσόλας

Ας δημιουργήσουμε μια ελάχιστη εφαρμογή κονσόλας που θα φιλοξενήσει τη λογική OCR. Ανοίξτε το `Program.cs` (ή δημιουργήστε νέο αρχείο) και επικολλήστε το σκελετό παρακάτω. Παρατηρήστε τις οδηγίες `using` στην κορυφή—φέρνουν τα namespaces του Aspose OCR στο πεδίο ορατότητας.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in in the next steps.
        }
    }
}
```

Σε αυτό το σημείο το έργο μεταγλωττίζεται, αλλά δεν κάνει τίποτα ακόμα. Τα επόμενα τμήματα θα αναπτύξουν τη ροή **εκτέλεσης OCR σε εικόνα**.

## Βήμα 3: Αρχικοποίηση της Μηχανής OCR (Εξαγωγή Κειμένου από Εικόνα)

Για να **εξάγετε κείμενο από εικόνα**, χρειάζεστε πρώτα μια παρουσία `OcrEngine`. Το Aspose OCR κατεβάζει αργά τους πόρους γλώσσας την πρώτη φορά που χρειάζονται, διατηρώντας το αρχικό binary μικρό.

```csharp
// Step 3: Initialize the OCR engine (resources are downloaded on demand)
var ocrEngine = new OcrEngine();
```

Γιατί να αρχικοποιήσουμε εδώ αντί για static πεδίο; Κάνοντας το μέσα στο `Main` εξασφαλίζουμε ότι τυχόν εξαιρέσεις (π.χ. ελλιπείς native εξαρτήσεις) εμφανίζονται νωρίς, κάνοντας το debugging πιο εύκολο.

## Βήμα 4: Περιορισμός Αναγνώρισης στην Επιθυμητή Γλώσσα (Ανάγνωση Κειμένου από JPG)

Αν γνωρίζετε τη γλώσσα του κειμένου που σαρώνετε—π.χ. Ρωσικά—μπορείτε να βελτιώσετε τόσο την ταχύτητα όσο και την ακρίβεια ορίζοντας την ιδιότητα `Language`. Αυτό είναι ιδιαίτερα χρήσιμο όταν **διαβάζετε κείμενο από jpg** αρχεία που περιέχουν κυριλλικούς χαρακτήρες.

```csharp
// Step 4: Limit recognition to the Russian language pack (ISO code "ru")
ocrEngine.Language = OcrLanguage.Russian;
```

Στο παρασκήνιο το Aspose OCR θα κατεβάσει το πακέτο γλώσσας Ρωσικά την πρώτη φορά που φτάσετε σε αυτή τη γραμμή. Οι επόμενες εκτελέσεις χρησιμοποιούν το αποθηκευμένο πακέτο, οπότε δεν υπάρχει καθυστέρηση δικτύου μετά την αρχική λήψη.

> **Γιατί να κλειδώσετε τη γλώσσα;**  
> * **Performance:** Η μηχανή παραλείπει το σκανάρισμα χαρακτήρων εκτός του επιλεγμένου αλφαβήτου.  
> * **Accuracy:** Εφαρμόζονται γλωσσικές ευρετικές (π.χ. συχνότητες κοινών λέξεων), μειώνοντας τις λανθασμένες αναγνώσεις.  

Αν χρειαστεί να υποστηρίξετε πολλαπλές γλώσσες, μπορείτε να περάσετε μια λίστα χωρισμένη με κόμμα, π.χ., `OcrLanguage.English | OcrLanguage.Russian`.

## Βήμα 5: Εκτέλεση OCR στο Στόχο JPG (Εκτέλεση OCR σε Εικόνα)

Τώρα πραγματικά **τρέχουμε OCR σε εικόνα**. Δώστε το πλήρες μονοπάτι του αρχείου JPG—το Aspose OCR δέχεται πολλές μορφές (`.png`, `.bmp`, `.tif`, κ.λπ.), αλλά θα μείνουμε στα `.jpg` για αυτή τη demo.

```csharp
// Step 5: Perform OCR on the image containing Cyrillic text
string imagePath = @"YOUR_DIRECTORY/cyrillic_sample.jpg";
var recognizedResult = ocrEngine.RecognizeImage(imagePath);
```

Αν το αρχείο δεν βρεθεί, το `RecognizeImage` ρίχνει `FileNotFoundException`. Για να κάνουμε το tutorial ανθεκτικό, τυλίξτε την κλήση σε μπλοκ try‑catch:

```csharp
try
{
    var recognizedResult = ocrEngine.RecognizeImage(imagePath);
    Console.WriteLine("✅ OCR succeeded!");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(recognizedResult.Text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"❌ Error during OCR: {ex.Message}");
}
```

Η μέθοδος `RecognizeImage` επιστρέφει ένα αντικείμενο `OcrResult` του οποίου η ιδιότητα `Text` περιέχει την εξαγόμενη απλή κειμενική μορφή. Μπορείτε επίσης να προσπελάσετε το `Boxes` για δεδομένα bounding‑box αν χρειάζεστε πληροφορίες διάταξης αργότερα.

## Βήμα 6: Επαλήθευση του Αποτελέσματος

Όταν τρέξετε το πρόγραμμα (`dotnet run`), θα πρέπει να δείτε κάτι σαν:

```
✅ OCR succeeded!
Extracted text:
Пример текста на кириллице
```

Αν το αποτέλεσμα φαίνεται παραμορφωμένο, ελέγξτε ξανά ότι η εικόνα είναι καθαρή και ότι έχετε επιλέξει τη σωστή γλώσσα. Οι θολές ή χαμηλής αντίθεσης εικόνες είναι η πιο κοινή αιτία κακών αποτελεσμάτων OCR.

### Ακραίες Περιπτώσεις & Συχνές Ερωτήσεις

| Situation | What to Do |
|-----------|------------|
| **Image contains multiple languages** | Set `ocrEngine.Language` to a combination, e.g., `OcrLanguage.English | OcrLanguage.Russian`. |
| **Large batch of images** | Reuse the same `OcrEngine` instance across files; it caches language data. |
| **Running on a headless server** | No UI is required—Aspose OCR works fine in Docker or Azure Functions. |
| **Need higher accuracy** | Adjust `ocrEngine.Options` (e.g., `ocrEngine.Options.Denoise = true`). |
| **Unsupported file format** | Convert the image to a supported format (PNG or JPG) before calling `RecognizeImage`. |

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω είναι το πλήρες, έτοιμο για αντιγραφή‑και‑επικόλληση πρόγραμμα που ενσωματώνει όλα τα παραπάνω βήματα. Αποθηκεύστε το ως `Program.cs` και τρέξτε το από τη γραμμή εντολών.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine (downloads language packs on first use)
            var ocrEngine = new OcrEngine();

            // 2️⃣ Restrict recognition to Russian – speeds up processing and boosts accuracy
            ocrEngine.Language = OcrLanguage.Russian;

            // 3️⃣ Path to the JPG you want to read text from
            string imagePath = @"YOUR_DIRECTORY/cyrillic_sample.jpg";

            // 4️⃣ Perform OCR and handle possible errors
            try
            {
                var result = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("✅ OCR completed successfully.");
                Console.WriteLine("🖼️ Extracted text:");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Failed to extract text from image: {ex.Message}");
            }
        }
    }
}
```

**Αναμενόμενη έξοδος στην κονσόλα** (υποθέτοντας ότι η δείγμα εικόνα περιέχει τη φράση “Пример текста на кириллице”):

```
✅ OCR completed successfully.
🖼️ Extracted text:
Пример текста на кириллице
```

Αν αντικαταστήσετε την εικόνα με μια αγγλική φωτογραφία και αλλάξετε `ocrEngine.Language = OcrLanguage.English;`, ο ίδιος κώδικας θα **διαβάσει κείμενο από jpg** στα Αγγλικά χωρίς περαιτέρω αλλαγές.

## Μπόνους: Εκτέλεση OCR σε Πολλαπλά Αρχεία

Συχνά θα χρειαστεί να **τρέξετε OCR σε εικόνες** συλλογές. Εδώ είναι ένα σύντομο απόσπασμα που διατρέχει έναν φάκελο:

```csharp
string folder = @"YOUR_DIRECTORY";
foreach (var file in System.IO.Directory.GetFiles(folder, "*.jpg"))
{
    try
    {
        var result = ocrEngine.RecognizeImage(file);
        Console.WriteLine($"[{System.IO.Path.GetFileName(file)}] => {result.Text}");
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Error processing {file}: {ex.Message}");
    }
}
```

Η μηχανή επαναχρησιμοποιεί το προηγουμένως ληφθέν πακέτο γλώσσας, οπότε η παρτίδα εκτελείται αποδοτικά.

## Συμπέρασμα

Τώρα έχετε ένα σταθερό, έτοιμο για παραγωγή πρότυπο για **εξαγωγή κειμένου από εικόνα** χρησιμοποιώντας το Aspose OCR σε C#. Το tutorial κάλυψε τα πάντα—from την εγκατάσταση του πακέτου NuGet μέχρι τη διαχείριση σφαλμάτων και την κλιμάκωση σε πολλαπλά αρχεία. Είτε **διαβάζετε κείμενο από jpg** περιουσιακά στοιχεία, είτε σαρώνετε PDFs, είτε χτίζετε μια γραμμή αυτοματοποίησης εγγράφων, η ίδια προσέγγιση ισχύει—απλώς αλλάξτε το πακέτο γλώσσας ή ρυθμίστε τις επιλογές OCR.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε:

* Πειραματισμό με άλλες γλώσσες (π.χ., `OcrLanguage.ChineseSimplified`).  
* Εξαγωγή πληροφοριών διάταξης μέσω `recognizedResult.Boxes`.  
* Ενσωμάτωση της ροής OCR σε ένα ASP.NET Core API ώστε άλλες υπηρεσίες να μπορούν να ζητούν εξαγωγή κειμένου κατ' απαίτηση.

Καλό κώδικα, και ας είναι πάντα οι εικόνες σας αρκετά καθαρές για τέλειο OCR!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}