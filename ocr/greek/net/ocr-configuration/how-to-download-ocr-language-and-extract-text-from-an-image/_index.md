---
category: general
date: 2026-11-23
description: Κατεβάστε τη γλώσσα OCR και εξάγετε κείμενο από μια εικόνα με το Aspose.OCR.
  Μάθετε πώς να αναγνωρίζετε κυριλλικό κείμενο από αρχεία PNG σε λίγα εύκολα βήματα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- download OCR language
- extract text from image
- how to recognize cyrillic
- recognize text from PNG
- recognize Cyrillic text
language: el
lastmod: 2026-11-23
og_description: Κατεβάστε τη γλώσσα OCR και εξάγετε κείμενο από μια εικόνα χρησιμοποιώντας
  το Aspose.OCR. Ακολουθήστε αυτόν τον βήμα‑βήμα οδηγό για να αναγνωρίσετε κυριλλικό
  κείμενο από αρχεία PNG.
og_image_alt: Screenshot of Aspose.OCR engine recognizing Cyrillic text from a PNG
  image
og_title: Κατεβάστε τη γλώσσα OCR και εξάγετε κείμενο από εικόνες – Οδηγός Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-11-23'
  description: download OCR language and extract text from an image with Aspose.OCR.
    Learn how to recognize Cyrillic text from PNG files in a few easy steps.
  headline: How to download OCR language and extract text from an image
  type: TechArticle
- description: download OCR language and extract text from an image with Aspose.OCR.
    Learn how to recognize Cyrillic text from PNG files in a few easy steps.
  name: How to download OCR language and extract text from an image
  steps:
  - name: '**Multiple languages** – you can load several language modules at once,
      e.g., `engine.LoadLanguage("cyrillic,english");`. The engine will attempt to
      recognize characters from any loaded set.'
    text: '**Multiple languages** – you can load several language modules at once,
      e.g., `engine.LoadLanguage("cyrillic,english");`. The engine will attempt to
      recognize characters from any loaded set.'
  - name: '**Large images** – for high‑resolution files, consider down‑sampling before
      OCR to reduce memory usage.'
    text: '**Large images** – for high‑resolution files, consider down‑sampling before
      OCR to reduce memory usage.'
  - name: '**Batch processing** – wrap the recognition logic in a loop that iterates
      over a directory of PNG files. Remember to re‑assign `engine.Image` for each
      file; the engine can be reused.'
    text: '**Batch processing** – wrap the recognition logic in a loop that iterates
      over a directory of PNG files. Remember to re‑assign `engine.Image` for each
      file; the engine can be reused.'
  type: HowTo
- questions:
  - answer: Download the language module manually from the Aspose download portal,
      place the `.zip` file in the folder you specify with `SetLocalResourcesPath`,
      and the engine will load it without contacting the internet.
    question: What if the download fails because of a firewall?
  - answer: Yes. The OCR engine accepts any format that `System.Drawing.Image` can
      load. Simply change the file extension in `ImageStream.FromFile`.
    question: Can I recognize text from other image formats (e.g., JPEG, BMP)?
  - answer: The underlying API is the same; PNG is just one of many supported formats.
      Mentioning “recognize text from PNG” helps surface the tutorial for users searching
      for that exact phrase.
    question: How does this differ from “recognize text from PNG” vs. “recognize text
      from image”?
  - answer: 'Each `OcrEngine` instance is not thread‑safe. Create a separate instance
      per thread or use a pool pattern if you need high‑throughput processing. ##
      Edge cases and variations 1. **Multiple languages** – you can load several language
      modules at once, e.g., `engine.LoadLanguage("cyrillic,english");`. '
    question: Is the OCR engine thread‑safe?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Πώς να κατεβάσετε τη γλώσσα OCR και να εξάγετε κείμενο από μια εικόνα
url: /el/net/ocr-configuration/how-to-download-ocr-language-and-extract-text-from-an-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να κατεβάσετε γλώσσα OCR και να εξάγετε κείμενο από μια εικόνα

Αν χρειάζεστε να **κατεβάσετε γλώσσα OCR** πόρους και να εξάγετε κείμενο από μια εικόνα, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε με το Aspose.OCR. Είτε η πηγή είναι ένα PNG που περιέχει κυριλλικούς χαρακτήρες είτε οποιαδήποτε άλλη υποστηριζόμενη μορφή, θα λάβετε μια πλήρη, εκτελέσιμη λύση.

Θα μάθετε πώς να:

* Φορτώσετε ένα γλωσσικό μοντέλο κατά απαίτηση (το βήμα “κατεβάστε γλώσσα OCR”)  
* Αναγνωρίσετε κυριλλικό κείμενο από αρχείο PNG  
* Προαιρετικά, ορίσετε τη μηχανή σε τοπικό φάκελο για προ‑κατεβασμένους πόρους  

Στο τέλος του οδηγού θα μπορείτε να ενσωματώσετε OCR σε οποιαδήποτε εφαρμογή .NET και αξιόπιστα **εξάγετε κείμενο από εικόνα** αρχεία.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 SDK ή νεότερο εγκατεστημένο  
* Ένα έγκυρο άδεια Aspose.OCR (η δωρεάν δοκιμή λειτουργεί για αξιολόγηση)  
* Visual Studio 2022 ή οποιοδήποτε IDE συμβατό με C#  
* Ένα αρχείο εικόνας (`sample_cyrillic.png`) που περιέχει κυριλλικό κείμενο  

Τα αποσπάσματα κώδικα χρησιμοποιούν χαρακτηριστικά γλώσσας C# 10, αλλά μπορείτε να τα προσαρμόσετε σε παλαιότερες εκδόσεις αν χρειαστεί.

## Βήμα 1: Εγκατάσταση του πακέτου NuGet Aspose.OCR

Ανοίξτε ένα τερματικό στον φάκελο του έργου σας και εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

## Βήμα 2: Δημιουργία έργου console και προσθήκη των using directives

Δημιουργήστε μια νέα εφαρμογή console (αν δεν έχετε ήδη μία):

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Ανοίξτε το `Program.cs` και προσθέστε τα απαιτούμενα namespaces στην αρχή:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Helpers;   // Provides ImageStream helper methods
```

Το namespace `Aspose.OCR.Helpers` σας παρέχει βολικές μεθόδους για φόρτωση εικόνων από το δίσκο.

## Βήμα 3: Αρχικοποίηση της μηχανής OCR και **κατεβάστε γλώσσα OCR** πόρων

Η μηχανή OCR έρχεται με ένα ελάχιστο σύνολο πόρων. Για να αναγνωρίσετε κυριλλικούς χαρακτήρες πρέπει να φορτώσετε το αντίστοιχο γλωσσικό μοντέλο. Αν το μοντέλο δεν υπάρχει τοπικά, το Aspose.OCR το κατεβάζει αυτόματα.

```csharp
// Step 3: Create the OCR engine with default (basic) resources
var engine = new OcrEngine();

// Load the Cyrillic language module; this triggers a download if missing
engine.LoadLanguage("cyrillic");

// Optional: specify a folder for cached language files
// engine.ResourceManager.SetLocalResourcesPath(@"C:\AsposeOCRResources");
```

**Γιατί αυτό το βήμα είναι σημαντικό:**  
*`LoadLanguage("cyrillic")`* λέει στη μηχανή ποιο σύνολο χαρακτήρων να χρησιμοποιήσει. Χωρίς αυτή την κλήση, η μηχανή θα επανέλθει στο προεπιλεγμένο λατινικό σύνολο και θα αποτύχει να αναγνωρίσει κυριλλικά σύμβολα. Η λήψη γίνεται μόνο μία φορά, μετά την οποία το μοντέλο αποθηκεύεται στην κρυφή μνήμη για μελλοντικές εκτελέσεις.

## Βήμα 4: Φόρτωση της εικόνας που περιέχει κυριλλικό κείμενο

Το Aspose.OCR λειτουργεί με οποιαδήποτε μορφή εικόνας υποστηρίζεται από το `System.Drawing` του .NET. Για αυτόν τον οδηγό χρησιμοποιούμε ένα αρχείο PNG επειδή διατηρεί την απώλεια ποιότητας, κάτι που βελτιώνει την ακρίβεια της αναγνώρισης.

```csharp
// Step 4: Load the image containing Cyrillic text
engine.Image = ImageStream.FromFile(@"C:\Images\sample_cyrillic.png");
```

Αν προτιμάτε σχετικό μονοπάτι, τοποθετήστε την εικόνα μέσα στον φάκελο του έργου και χρησιμοποιήστε `Path.Combine(Directory.GetCurrentDirectory(), "sample_cyrillic.png")`.

## Βήμα 5: Αναγνώριση του κειμένου και εμφάνιση του αποτελέσματος

Τώρα που η μηχανή είναι διαμορφωμένη και η εικόνα φορτωμένη, καλέστε το `Recognize()` και διαβάστε την ιδιότητα `Text`.

```csharp
// Step 5: Perform OCR and output the recognized text
engine.Recognize();

Console.WriteLine("Recognized text:");
Console.WriteLine(engine.Text);
```

**Expected output**

```
Recognized text:
Привет, мир!
```

Η ακριβής συμβολοσειρά εξαρτάται από το περιεχόμενο του `sample_cyrillic.png`, αλλά θα πρέπει να δείτε κυριλλικούς χαρακτήρες να εκτυπώνονται στην κονσόλα.

## Βήμα 6: Πλήρες, εκτελέσιμο πρόγραμμα

Συνδυάζοντας όλα μαζί, εδώ είναι το πλήρες αρχείο πηγαίου κώδικα που μπορείτε να αντιγράψετε στο `Program.cs` και να εκτελέσετε:

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Helpers;

namespace OcrDemo
{
    internal class Program
    {
        private static void Main(string[] args)
        {
            // Initialize OCR engine
            var engine = new OcrEngine();

            // Load Cyrillic language – downloads if not cached
            engine.LoadLanguage("cyrillic");

            // (Optional) Set a custom folder for language resources
            // engine.ResourceManager.SetLocalResourcesPath(@"C:\AsposeOCRResources");

            // Load the PNG image that contains Cyrillic text
            engine.Image = ImageStream.FromFile(@"C:\Images\sample_cyrillic.png");

            // Run OCR
            engine.Recognize();

            // Output the result
            Console.WriteLine("Recognized text:");
            Console.WriteLine(engine.Text);
        }
    }
}
```

Εκτελέστε το πρόγραμμα με:

```bash
dotnet run
```

Θα πρέπει να δείτε τη φράση στα κυριλλικά να εκτυπώνεται στην κονσόλα, επιβεβαιώνοντας ότι η λειτουργία **recognize Cyrillic text** ολοκληρώθηκε με επιτυχία.

## Συμβουλή: βελτιώστε την ακρίβεια για θορυβώδεις PNG αρχεία

- **Προεπεξεργασία της εικόνας** – μετατρέψτε σε κλίμακα του γκρι, αυξήστε την αντίθεση ή εφαρμόστε ένα μέσο φίλτρο χρησιμοποιώντας `System.Drawing` πριν τη μεταβιβάσετε στη μηχανή OCR.  
- **Ορίστε επιλογές `engine.Config`** – ενεργοποιήστε `engine.Config.DetectOrientation = true` αν το κείμενο μπορεί να είναι περιστραμμένο.  
- **Αποθήκευση γλωσσικών μοντέλων στην κρυφή μνήμη** – καλώντας το `SetLocalResourcesPath` αποφεύγετε την καθυστέρηση δικτύου σε επόμενες εκτελέσεις.

## Συχνές ερωτήσεις

**Ε: Τι γίνεται αν η λήψη αποτύχει λόγω τείχους προστασίας;**  
Α: Κατεβάστε το γλωσσικό μοντέλο χειροκίνητα από το portal λήψεων του Aspose, τοποθετήστε το αρχείο `.zip` στον φάκελο που καθορίζετε με `SetLocalResourcesPath`, και η μηχανή θα το φορτώσει χωρίς να χρειαστεί σύνδεση στο διαδίκτυο.

**Ε: Μπορώ να αναγνωρίσω κείμενο από άλλες μορφές εικόνας (π.χ., JPEG, BMP);**  
Α: Ναι. Η μηχανή OCR δέχεται οποιαδήποτε μορφή μπορεί να φορτώσει το `System.Drawing.Image`. Απλώς αλλάξτε την επέκταση αρχείου στο `ImageStream.FromFile`.

**Ε: Πώς διαφέρει αυτό από το “recognize text from PNG” σε σχέση με το “recognize text from image”;**  
Α: Το υποκείμενο API είναι το ίδιο· το PNG είναι απλώς μία από τις πολλές υποστηριζόμενες μορφές. Η αναφορά στο “recognize text from PNG” βοηθά να εμφανίζεται ο οδηγός σε χρήστες που ψάχνουν αυτή τη φράση.

**Ε: Είναι η μηχανή OCR ασφαλής για πολλαπλά νήματα (thread‑safe);**  
Α: Κάθε αντικείμενο `OcrEngine` δεν είναι thread‑safe. Δημιουργήστε ξεχωριστό αντικείμενο ανά νήμα ή χρησιμοποιήστε μοτίβο pool αν χρειάζεστε υψηλή απόδοση επεξεργασίας.

## Περιπτώσεις άκρων και παραλλαγές

1. **Πολλαπλές γλώσσες** – μπορείτε να φορτώσετε πολλά γλωσσικά μοντέλα ταυτόχρονα, π.χ., `engine.LoadLanguage("cyrillic,english");`. Η μηχανή θα προσπαθήσει να αναγνωρίσει χαρακτήρες από οποιοδήποτε φορτωμένο σύνολο.  
2. **Μεγάλες εικόνες** – για αρχεία υψηλής ανάλυσης, σκεφτείτε την υποδειγματοληψία (down‑sampling) πριν το OCR για να μειώσετε τη χρήση μνήμης.  
3. **Επεξεργασία παρτίδας** – τυλίξτε τη λογική αναγνώρισης σε βρόχο που διατρέχει έναν φάκελο PNG αρχείων. Θυμηθείτε να επανα‑αναθέσετε το `engine.Image` για κάθε αρχείο· η μηχανή μπορεί να επαναχρησιμοποιηθεί.

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **κατεβάσετε γλώσσα OCR** πόρους, να διαμορφώσετε το Aspose.OCR για κυριλλικά, και να **εξάγετε κείμενο από μια εικόνα**—συγκεκριμένα ένα αρχείο PNG—χρησιμοποιώντας μια σύντομη εφαρμογή console C#. Αυτή η βάση σας επιτρέπει να δημιουργήσετε πιο σύνθετες λύσεις όπως σαρωτές εγγράφων, αυτοματοποιημένες γραμμές εισαγωγής δεδομένων ή υπηρεσίες πολυγλωσσικής εξαγωγής κειμένου.

Επόμενα βήματα που μπορείτε να εξερευνήσετε:

* Συνδυάστε **recognize text from PNG** με **how to recognize cyrillic** για έγγραφα πολλαπλών γλωσσών.  
* Ενσωματώστε τη ροή OCR σε ένα ASP.NET Core API για να εκθέσετε το OCR ως υπηρεσία web.  
* Πειραματιστείτε με άλλα γλωσσικά μοντέλα (π.χ., `engine.LoadLanguage("arabic")`) για να επεκτείνετε την εμβέλεια της εφαρμογής σας.

Καλό κώδικα, και απολαύστε τη δύναμη των άμεσων λήψεων γλώσσας OCR!

## Τι θα πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετικά θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να εκτελέσετε OCR σε C# – Αναγνώριση κυριλλικού κειμένου με Aspose](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-recognize-cyrillic-text-with-aspose/)
- [Πώς να κατεβάσετε πόρους OCR και να αναγνωρίσετε κείμενο από εικόνα σε C#](/ocr/english/net/text-recognition/how-to-download-ocr-resources-and-recognize-text-from-image/)
- [Πώς να κατεβάσετε το μοντέλο Aspose.OCR και να εξάγετε κείμενο από PNG σε C#](/ocr/english/net/text-recognition/how-to-download-ocr-model-and-extract-text-from-png-using-as/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}