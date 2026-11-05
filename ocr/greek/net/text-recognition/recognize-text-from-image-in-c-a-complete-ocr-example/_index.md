---
category: general
date: 2026-06-19
description: recognize text from image using Aspose OCR in C#. Follow this c# ocr
  example to extract text from jpg files and learn how to set ocr language quickly.
draft: false
keywords:
- recognize text from image
- extract text from jpg
- c# ocr example
- read text from image file
- set OCR language
language: el
og_description: Αναγνωρίστε κείμενο από εικόνα με Aspose OCR σε C#. Αυτός ο οδηγός
  παρουσιάζει ένα πλήρες παράδειγμα OCR σε C#, καλύπτοντας πώς να ορίσετε τη γλώσσα
  OCR και να εξάγετε κείμενο από αρχεία JPG.
og_title: Αναγνώριση κειμένου από εικόνα σε C# – Πλήρες παράδειγμα OCR
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: recognize text from image using Aspose OCR in C#. Follow this c# ocr
    example to extract text from jpg files and learn how to set ocr language quickly.
  headline: recognize text from image in C# – a complete OCR example
  type: TechArticle
- questions:
  - answer: Absolutely. Wrap the recognition call in a `foreach (var file in Directory.GetFiles(folder,
      "*.jpg"))` loop. Remember to reuse the same `engine` instance for speed.
    question: Can I process a folder of JPG files automatically?
  - answer: The default models focus on printed text. For handwritten recognition
      you’d need a specialized model—Aspose currently offers a separate Handwriting
      OCR package.
    question: Does Aspose.OCR support handwritten text?
  - answer: 'Convert the PDF page to an image first (e.g., using Aspose.PDF) and then
      feed that image to the OCR engine. --- ## Conclusion We’ve just **recognize
      text from image** using a concise **c# OCR example** that shows how to **set
      OCR language**, trigger automatic resource download, and **extract text fr'
    question: What if I need to extract text from a PDF page instead of a JPG?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
title: Αναγνώριση κειμένου από εικόνα σε C# – ένα πλήρες παράδειγμα OCR
url: /el/net/text-recognition/recognize-text-from-image-in-c-a-complete-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# αναγνώριση κειμένου από εικόνα σε C# – Πλήρες παράδειγμα OCR

Ποτέ χρειάστηκε να **αναγνωρίσετε κείμενο από εικόνα** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη να επιλέξετε; Δεν είστε μόνοι. Σε πολλά έργα—σάρωση τιμολογίων, επαλήθευση ταυτότητας ή απλώς εξαγωγή λεζάντων από φωτογραφίες—η δυνατότητα ανάγνωσης κειμένου από αρχείο εικόνας είναι πραγματικό ενισχυτικό παραγωγικότητας.

Σε αυτό το tutorial θα περάσουμε από ένα **c# OCR example** που χρησιμοποιεί το Aspose.OCR για **εξαγωγή κειμένου από αρχεία jpg**. Στο τέλος θα ξέρετε ακριβώς πώς να **ρυθμίσετε τη γλώσσα OCR**, να διαχειριστείτε τις αυτόματες λήψεις μοντέλων και να εμφανίσετε το αναγνωρισμένο κείμενο—όλα με λίγες μόνο γραμμές κώδικα.

## Τι θα μάθετε

- Πώς να διαμορφώσετε τη μηχανή OCR για συγκεκριμένη γλώσσα (π.χ., English, Arabic, Hindi).  
- Πώς να καλέσετε τη μηχανή ώστε η πρώτη κλήση να κατεβάζει αυτόματα τους απαιτούμενους πόρους.  
- Πώς να τροφοδοτήσετε μια εικόνα JPEG και να λάβετε καθαρό, αναγνώσιμο κείμενο.  
- Συμβουλές για την αντιμετώπιση κοινών προβλημάτων όπως ελλιπείς γραμματοσειρές ή μη υποστηριζόμενες μορφές.  

**Προαπαιτούμενα**: .NET 6+ (ή .NET Core 3.1), μια πρόσφατη έκδοση του Visual Studio ή του VS Code, και ένα πακέτο NuGet Aspose.OCR. Δεν απαιτείται προηγούμενη εμπειρία OCR.

---

![Διάγραμμα που απεικονίζει τη ροή εργασίας αναγνώρισης κειμένου από εικόνα χρησιμοποιώντας Aspose OCR σε C#](/images/ocr-workflow.png "διάγραμμα ροής εργασίας αναγνώρισης κειμένου από εικόνα")

## Βήμα 1: Εγκατάσταση του πακέτου NuGet Aspose.OCR

Πριν γράψουμε οποιονδήποτε κώδικα, χρειάζεται η βιβλιοθήκη. Ανοίξτε ένα τερματικό στον φάκελο του έργου σας και εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

> **Συμβουλή:** Αν χρησιμοποιείτε Visual Studio, κάντε δεξί‑κλικ στο έργο → *Manage NuGet Packages* → αναζητήστε “Aspose.OCR” και κάντε κλικ στο *Install*. Το πακέτο περιλαμβάνει τη βασική μηχανή και τις κλάσεις διαμόρφωσης που θα χρησιμοποιήσουμε αργότερα.

## Βήμα 2: Διαμόρφωση της μηχανής OCR – **set OCR language**

Το πρώτο πράγμα που πρέπει να κάνετε είναι να πείτε στη μηχανή ποια γλώσσα πρέπει να αναζητήσει. Εδώ ξεχωρίζει η λέξη‑κλειδί **set OCR language**. Το αντικείμενο `OcrEngineConfig` περιέχει όλες τις ρυθμίσεις που χρειάζεστε.

```csharp
using Aspose.OCR;
using Aspose.OCR.Configuration;

// Choose the language you want to recognize.
// Language.English is the default, but you can switch to Arabic, Hindi, etc.
var config = new OcrEngineConfig
{
    Language = Language.English,          // <-- set OCR language here
    AutoDownloadResources = true         // downloads the model on first use
};
```

Γιατί να ασχοληθείτε με το `AutoDownloadResources`; Την πρώτη φορά που εκτελείτε το πρόγραμμα, το Aspose θα κατεβάσει το κατάλληλο μοντέλο από το cloud. Αυτό σημαίνει ότι δεν χρειάζεται να συμπεριλάβετε μεγάλα αρχεία μοντέλων στην εφαρμογή σας—ένα ωραίο πλεονέκτημα για το μέγεθος της διανομής.

## Βήμα 3: Δημιουργία της μηχανής OCR

Τώρα που έχουμε μια διαμόρφωση, μπορούμε να δημιουργήσουμε τη μηχανή. Η χρήση μιας δήλωσης `using` εξασφαλίζει ότι η μηχανή θα απελευθερωθεί σωστά, απελευθερώνοντας τους εγγενείς πόρους.

```csharp
// The engine respects the configuration we just defined.
using var engine = new OcrEngine(config);
```

Αν χρειαστεί ποτέ να αλλάξετε γλώσσες κατά την εκτέλεση, μπορείτε απλώς να αντιστοιχίσετε μια νέα τιμή `Language` στο `engine.Config.Language` πριν καλέσετε το `RecognizeImage`.

## Βήμα 4: Αναγνώριση κειμένου από εικόνα – το κεντρικό **c# OCR example**

Εδώ είναι η στιγμή της αλήθειας: τροφοδοτούμε ένα αρχείο JPEG και ζητάμε από τη μηχανή να κάνει τη μαγεία της. Η πρώτη κλήση θα ενεργοποιήσει την αυτόματη λήψη μοντέλου αν δεν έχει γίνει ακόμη.

```csharp
// Replace the path with the location of your test image.
string imagePath = Path.Combine(Environment.CurrentDirectory, "sample_english.jpg");

// RecognizeImage returns an OcrResult containing the extracted string.
OcrResult result = engine.RecognizeImage(imagePath);
```

> **Τι γίνεται αν η εικόνα είναι PNG ή BMP;**  
> Η μέθοδος `RecognizeImage` δέχεται οποιαδήποτε μορφή υποστηρίζεται από το System.Drawing, ώστε να μπορείτε να περάσετε PNG, BMP ή ακόμη και TIFF χωρίς αλλαγές.

## Βήμα 5: Εξαγωγή του αναγνωρισμένου κειμένου – **read text from image file**

Τέλος, γράφουμε το αποτέλεσμα στην κονσόλα. Σε μια πραγματική εφαρμογή μπορεί να το αποθηκεύσετε σε μια βάση δεδομένων ή να το περάσετε σε άλλη υπηρεσία.

```csharp
// The Text property holds the plain‑text representation of the image.
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(result.Text);
```

### Αναμενόμενη έξοδος

Αν το `sample_english.jpg` περιέχει τη φράση “Hello, Aspose OCR!”, η κονσόλα θα εμφανίσει:

```
=== Recognized Text ===
Hello, Aspose OCR!
```

Παρατηρήστε πόσο καθαρή είναι η έξοδος—χωρίς επιπλέον αλλαγές γραμμής ή τεχνικά artefacts OCR. Το Aspose κάνει καλή δουλειά στην κανονικοποίηση των κενών χαρακτήρων από προεπιλογή.

## Διαχείριση κοινών περιπτώσεων άκρων

| Κατάσταση | Τι πρέπει να κάνετε |
|-----------|---------------------|
| **Αποτυχία λήψης μοντέλου** | Βεβαιωθείτε ότι η μηχανή έχει πρόσβαση στο internet. Μπορείτε επίσης να προ‑κατεβάσετε το μοντέλο καλώντας το `engine.DownloadResources()` χειροκίνητα. |
| **Λανθασμένος εντοπισμός γλώσσας** | Ορίστε ρητά το `config.Language` στην σωστή τιμή enum (π.χ., `Language.Arabic`). |
| **Εικόνα χαμηλής ανάλυσης** | Αυξήστε την ανάλυση της εικόνας ή εφαρμόστε φίλτρο ενίσχυσης πριν καλέσετε το `RecognizeImage`. |
| **Μεγάλη επεξεργασία παρτίδας** | Ξαναχρησιμοποιήστε ένα μόνο αντικείμενο `OcrEngine` σε πολλαπλές κλήσεις για να αποφύγετε την επαναλαμβανόμενη φόρτωση μοντέλου. |

## Πλήρες λειτουργικό παράδειγμα (Έτοιμο για αντιγραφή‑επικόλληση)

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Configuration;

class Program
{
    static void Main()
    {
        // Step 1: Configure the OCR engine – select the language and enable auto‑download
        var config = new OcrEngineConfig
        {
            Language = Language.English,          // e.g., Language.Arabic, Language.Hindi, etc.
            AutoDownloadResources = true         // downloads the required model on first use
        };

        // Step 2: Create the OCR engine with the specified configuration
        using var engine = new OcrEngine(config);

        // Step 3: Recognize text from an image (the first call triggers the model download if needed)
        string imagePath = Path.Combine(Environment.CurrentDirectory, "sample_english.jpg");
        OcrResult result = engine.RecognizeImage(imagePath);

        // Step 4: Output the recognized text
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);
    }
}
```

Εκτελέστε το πρόγραμμα με `dotnet run`. Αν όλα είναι ρυθμισμένα σωστά, θα δείτε το εξαγόμενο κείμενο να εμφανίζεται στην κονσόλα.

---

## Συχνές Ερωτήσεις

**Ε: Μπορώ να επεξεργαστώ αυτόματα έναν φάκελο με αρχεία JPG;**  
Α: Απόλυτα. Τυλίξτε την κλήση αναγνώρισης σε έναν βρόχο `foreach (var file in Directory.GetFiles(folder, "*.jpg"))`. Θυμηθείτε να ξαναχρησιμοποιήσετε το ίδιο αντικείμενο `engine` για ταχύτητα.

**Ε: Υποστηρίζει το Aspose.OCR χειρόγραφο κείμενο;**  
Α: Τα προεπιλεγμένα μοντέλα εστιάζουν σε τυπωμένο κείμενο. Για αναγνώριση χειρογράφου χρειάζεται εξειδικευμένο μοντέλο—το Aspose προσφέρει αυτή τη στιγμή ξεχωριστό πακέτο Handwriting OCR.

**Ε: Τι γίνεται αν χρειαστεί να εξάγω κείμενο από σελίδα PDF αντί για JPG;**  
Α: Μετατρέψτε πρώτα τη σελίδα PDF σε εικόνα (π.χ., χρησιμοποιώντας το Aspose.PDF) και στη συνέχεια τροφοδοτήστε αυτήν την εικόνα στη μηχανή OCR.

---

## Συμπέρασμα

Μόλις **αναγνωρίσαμε κείμενο από εικόνα** χρησιμοποιώντας ένα σύντομο **c# OCR example** που δείχνει πώς να **ρυθμίσετε τη γλώσσα OCR**, να ενεργοποιήσετε την αυτόματη λήψη πόρων και να **εξάγετε κείμενο από αρχεία jpg** με ελάχιστο κώδικα. Η πλήρης ροή—από την εγκατάσταση του πακέτου NuGet μέχρι την εκτύπωση του αποτελέσματος—χωρά άνετα σε μια μόνο μέθοδο, καθιστώντας εύκολη την ενσωμάτωση σε μεγαλύτερες εφαρμογές.

Τι ακολουθεί; Δοκιμάστε να αντικαταστήσετε το `Language.English` με `Language.French` ή `Language.Hindi` και δείτε πώς προσαρμόζεται η μηχανή. Πειραματιστείτε με διαφορετικές αναλύσεις εικόνας ή τροφοδοτήστε μια παρτίδα αρχείων για να αξιολογήσετε την απόδοση. Το API του Aspose.OCR είναι αρκετά ευέλικτο για γρήγορα πρωτότυπα και υπηρεσίες παραγωγικής κλίμακας.

Αν βρήκατε αυτόν τον οδηγό χρήσιμο, δώστε του ένα αστέρι στο GitHub, μοιραστείτε τον με συναδέλφους ή αφήστε ένα σχόλιο παρακάτω με τις δικές σας OCR περιπέτειες. Καλή προγραμματιστική!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε σε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [αναγνώριση κειμένου εικόνας με Aspose OCR για πολλαπλές γλώσσες](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Πώς να εξάγετε κείμενο από εικόνα χρησιμοποιώντας Aspose.OCR για .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}