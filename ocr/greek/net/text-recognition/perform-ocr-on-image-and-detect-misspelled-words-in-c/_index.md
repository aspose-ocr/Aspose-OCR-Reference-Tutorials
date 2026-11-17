---
category: general
date: 2026-06-03
description: Πραγματοποιήστε OCR σε εικόνα και εξάγετε κείμενο από την εικόνα χρησιμοποιώντας
  το Aspose.OCR. Μάθετε πώς να εντοπίζετε λανθασμένες λέξεις και να λαμβάνετε προτάσεις
  ορθογραφίας σε μια ενιαία επίδειξη C#.
draft: false
keywords:
- perform OCR on image
- extract text from image
- detect misspelled words
- get spelling suggestions
- how to extract text
language: el
og_description: Εκτελέστε OCR σε εικόνα για να εξάγετε κείμενο από αυτήν, στη συνέχεια
  εντοπίστε ορθογραφικά λάθη και λάβετε προτάσεις διόρθωσης με το Aspose.OCR σε C#.
og_title: Εκτελέστε OCR σε εικόνα και εντοπίστε λανθασμένες λέξεις σε C#
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Perform OCR on image and extract text from image using Aspose.OCR.
    Learn how to detect misspelled words and get spelling suggestions in a single
    C# demo.
  headline: Perform OCR on Image and Detect Misspelled Words in C#
  type: TechArticle
tags:
- Aspose OCR
- C#
- Spell Checking
title: Εκτέλεση OCR σε εικόνα και ανίχνευση ορθογραφικών λαθών σε C#
url: /el/net/text-recognition/perform-ocr-on-image-and-detect-misspelled-words-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε εικόνα και ανίχνευση λανθασμένων λέξεων σε C#

Έχετε αναρωτηθεί ποτέ πώς να **εκτελέσετε OCR σε εικόνα** αρχεία χωρίς να τρελαίνεστε; Δεν είστε οι μόνοι. Είτε ψηφιοποιείτε παλιά γράμματα, σαρώνετε αποδείξεις, είτε δημιουργείτε μια έξυπνη ροή εργασίας εγγράφων, η εξαγωγή καθαρού κειμένου από εικόνες είναι το πρώτο εμπόδιο. Τα καλά νέα; Με το Aspose.OCR μπορείτε να δημιουργήσετε μια λύση σε λίγα λεπτά, και το επιπλέον είναι ότι μπορείτε επίσης **να ανιχνεύσετε λανθασμένες λέξεις** και **να λάβετε προτάσεις ορθογραφίας** στην ίδια εκτέλεση.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από μια πλήρη, έτοιμη‑για‑εκτέλεση C# κονσόλα εφαρμογή που **εξάγει κείμενο από εικόνα**, εκτελεί έναν αγγλικό ορθογραφικό ελεγκτή, και εκτυπώνει κάθε σφάλμα με χρήσιμες ιδέες διόρθωσης. Στο τέλος θα γνωρίζετε ακριβώς **πώς να εξάγετε κείμενο**, πώς να συνδέσετε το spell‑check API, και πώς φαίνεται η αναμενόμενη έξοδος της κονσόλας.

## Τι θα δημιουργήσετε

- Φορτώστε ένα bitmap (ή PNG) που περιέχει τυπογραφικά λάθη.  
- Εκτελέστε το Aspose.OCR για **εκτελέσετε OCR σε εικόνα** και λάβετε ακατέργαστα δεδομένα συμβολοσειράς.  
- Αρχικοποιήστε τον ενσωματωμένο αγγλικό ορθογραφικό ελεγκτή.  
- **να ανιχνεύσετε λανθασμένες λέξεις** και **να λάβετε προτάσεις ορθογραφίας** για κάθε ένα.  
- Εκτυπώστε μια τακτοποιημένη αναφορά στην κονσόλα.

Χωρίς εξωτερικές υπηρεσίες, χωρίς περίπλοκες κλήσεις HTTP—μόνο ένα ενιαίο πακέτο NuGet και λίγες γραμμές κώδικα.

## Προαπαιτούμενα

- .NET 6.0 SDK ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.7+).  
- Visual Studio 2022 (ή οποιονδήποτε επεξεργαστή προτιμάτε).  
- Πακέτο NuGet Aspose.OCR για .NET (`Aspose.OCR`).  
- Ένα αρχείο εικόνας (`letter_with_typos.png`) τοποθετημένο κάπου που μπορείτε να το αναφέρετε από το έργο.

Αν δεν έχετε χρησιμοποιήσει ποτέ το Aspose, μην ανησυχείτε—η εγκατάσταση του πακέτου είναι τόσο εύκολη όσο η εκτέλεση:

```bash
dotnet add package Aspose.OCR
```

Τώρα ας βουτήξουμε στην υλοποίηση.

## Βήμα 1: Ρύθμιση του έργου και εγκατάσταση του Aspose.OCR

Δημιουργήστε ένα νέο έργο κονσόλας και προσθέστε τη βιβλιοθήκη OCR:

```bash
dotnet new console -n OcrSpellDemo
cd OcrSpellDemo
dotnet add package Aspose.OCR
```

Αφού ολοκληρωθεί η επαναφορά, ανοίξτε το `Program.cs`. Θα αντικαταστήσουμε το προεπιλεγμένο περιεχόμενο με τον πλήρη κώδικα επίδειξης αργότερα, αλλά πρώτα ας συζητήσουμε γιατί κάθε namespace είναι σημαντικό.

- `Aspose.OCR` – Πυρήνας μηχανής OCR και διαχείριση εικόνων.  
- `Aspose.OCR.SpellCheck` – Εργαλεία ορθογραφικού ελέγχου που παρέχονται με τη βιβλιοθήκη.  
- `System` – Πρότυπες βασικές κλάσεις .NET (π.χ., `Console`).

## Βήμα 2: Φόρτωση της εικόνας και εκτέλεση OCR σε εικόνα

Η πρώτη πραγματική εργασία είναι η παροχή της εικόνας στη μηχανή OCR. Το Aspose.OCR διαβάζει πολλές μορφές (PNG, JPEG, TIFF). Εδώ είναι το απόσπασμα κώδικα που κάνει τη βαριά δουλειά:

```csharp
// Step 2: Load the image that contains the text to be recognized
var image = OcrImage.FromFile(@"YOUR_DIRECTORY/letter_with_typos.png");

// Step 3: Perform OCR to extract the raw text from the image
var ocrEngine = new OcrEngine();
var ocrResult = ocrEngine.Recognize(image);
```

> **Γιατί είναι σημαντικό:** `OcrImage.FromFile` αφαιρεί τις λεπτομέρειες σε επίπεδο pixel, ενώ `OcrEngine.Recognize` εκτελεί το εκπαιδευμένο νευρωνικό μοντέλο που μετατρέπει τα οπτικά σύμβολα σε χαρακτήρες Unicode. Η ιδιότητα `ocrResult.Text` τώρα περιέχει την ακατέργαστη συμβολοσειρά—ακριβώς ό,τι χρειάζεστε για **εξάγετε κείμενο από εικόνα**.  
> **Συμβουλή:** Εάν η εικόνα σας περιέχει πολλαπλές γλώσσες, μπορείτε να ορίσετε `ocrEngine.Language = OcrLanguage.Multilingual;` πριν καλέσετε το `Recognize`.

## Βήμα 3: Αρχικοποίηση του αγγλικού Spell‑Checker

Το Aspose.OCR περιλαμβάνει μια ενσωματωμένη μηχανή ορθογραφικού ελέγχου που καταλαβαίνει τα Αγγλικά αμέσως. Η αρχικοποίησή της γίνεται με μία γραμμή:

```csharp
// Step 4: Initialise the English spell‑checker
var spellChecker = new SpellChecker(OcrLanguage.English);
```

> **Γιατί αυτό το βήμα είναι κρίσιμο:** Η έξοδος OCR μπορεί να περιλαμβάνει λανθασμένα αναγνωρισμένους χαρακτήρες (π.χ., “l” vs “1”) ή πραγματικά τυπογραφικά λάθη από το αρχικό έγγραφο. Ο ορθογραφικός ελεγκτής θα σαρώσει τη συμβολοσειρά, θα εντοπίσει ύποπτα tokens, και θα προτείνει εναλλακτικές.

## Βήμα 4: Ανίχνευση λανθασμένων λέξεων και λήψη προτάσεων ορθογραφίας

Τώρα τροφοδοτούμε το κείμενο OCR στον ελεγκτή:

```csharp
// Step 5: Check the recognized text for misspelled words and obtain suggestions
var misspellings = spellChecker.Check(ocrResult.Text);
```

`misspellings` είναι μια συλλογή όπου κάθε καταχώρηση περιέχει τη λανθασμένη λέξη και έναν πίνακα πιθανών διορθώσεων.

## Βήμα 5: Εξαγωγή των αποτελεσμάτων

Τέλος, επαναλαμβάνουμε τη συλλογή και εκτυπώνουμε μια αναφορά φιλική προς τον χρήστη:

```csharp
// Step 6: Output each misspelled word together with its suggested corrections
foreach (var entry in misspellings)
{
    Console.WriteLine($"Misspelled: {entry.Word}");
    Console.WriteLine("  Suggestions: " + string.Join(", ", entry.Suggestions));
}
```

### Αναμενόμενη έξοδος κονσόλας

Υποθέτοντας ότι το `letter_with_typos.png` περιέχει την πρόταση:

```
Ths is an exampel of a lettter with som misspelled wrds.
```

Η εκτέλεση της επίδειξης θα παράγει κάτι όπως:

```
Misspelled: Ths
  Suggestions: This, Thus, The
Misspelled: exampel
  Suggestions: example, exemplar, exampell
Misspelled: lettter
  Suggestions: letter, litter, lett
Misspelled: som
  Suggestions: some, sum, son
Misspelled: wrds
  Suggestions: words, wards, wryds
```

Παρατηρήστε πώς κάθε τυπογραφικό λάθος συνδυάζεται με μια σειρά πιθανών διορθώσεων—ακριβώς ό,τι χρειάζεστε όταν δημιουργείτε ένα φιλικό προς το χρήστη UI διόρθωσης.

## Πλήρες λειτουργικό παράδειγμα

Παρακάτω βρίσκεται το **πλήρες, έτοιμο για αντιγραφή‑επικόλληση** πρόγραμμα. Αντικαταστήστε το `YOUR_DIRECTORY` με την πραγματική διαδρομή του αρχείου εικόνας σας.

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System;

class SpellCheckDemo
{
    static void Main()
    {
        // Step 1: Load the image that contains the text to be recognized
        var image = OcrImage.FromFile(@"YOUR_DIRECTORY/letter_with_typos.png");

        // Step 2: Perform OCR to extract the raw text from the image
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(image);

        // Step 3: Initialise the English spell‑checker
        var spellChecker = new SpellChecker(OcrLanguage.English);

        // Step 4: Check the recognized text for misspelled words and obtain suggestions
        var misspellings = spellChecker.Check(ocrResult.Text);

        // Step 5: Output each misspelled word together with its suggested corrections
        foreach (var entry in misspellings)
        {
            Console.WriteLine($"Misspelled: {entry.Word}");
            Console.WriteLine("  Suggestions: " + string.Join(", ", entry.Suggestions));
        }

        // Optional: Keep console window open when debugging
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

> **Περιπτώσεις Άκρων προς εξέταση**  
> - **Κενή εικόνα:** Εάν η μηχανή OCR επιστρέψει μια κενή συμβολοσειρά, το `spellChecker.Check` θα επιστρέψει απλώς μια κενή συλλογή—χωρίς κατάρρευση.  
> - **Μη‑Αγγλικό κείμενο:** Αντικαταστήστε το `OcrLanguage.English` με `OcrLanguage.French` (ή οποιαδήποτε υποστηριζόμενη γλώσσα) για **να ανιχνεύσετε λανθασμένες λέξεις** σε άλλες περιοχές.  
> - **Μεγάλα έγγραφα:** Για PDF πολλαπλών σελίδων, θα επαναλάβετε για κάθε σελίδα, θα εκτελέσετε OCR, και στη συνέχεια θα συγκεντρώσετε τα αποτελέσματα πριν τον ορθογραφικό έλεγχο.

## Οπτική επισκόπηση (Κείμενο alt εικόνας)

![Διάγραμμα που δείχνει τη ροή για εκτέλεση OCR σε εικόνα, εξαγωγή κειμένου από εικόνα, και στη συνέχεια ανίχνευση λανθασμένων λέξεων με προτάσεις ορθογραφίας](perform-ocr-on-image-flow.png)

*Το παραπάνω διάγραμμα απεικονίζει τη διαδικασία από άκρη σε άκρη: εικόνα → μηχανή OCR → ακατέργαστο κείμενο → ορθογραφικός ελεγκτής → προτάσεις.*

## Συχνές ερωτήσεις & Συμβουλές Pro

| Ερώτηση | Απάντηση |
|----------|--------|
| **Χρειάζομαι σύνδεση στο internet;** | Όχι. Το Aspose.OCR λειτουργεί εξ ολοκλήρου τοπικά· ιδανικό για περιβάλλοντα εκτός σύνδεσης ή ασφαλή. |
| **Πόσο ακριβής είναι ο ορθογραφικός ελεγκτής;** | Χρησιμοποιεί λεξικό περίπου 150k αγγλικών λέξεων και ασαφή αντιστοίχιση, έτσι τα περισσότερα κοινά τυπογραφικά λάθη εντοπίζονται. |
| **Μπορώ να προσαρμόσω το λεξικό;** | Ναι. `SpellChecker.AddUserDictionary("custom.txt")` σας επιτρέπει να φορτώσετε όρους ειδικούς για το domain (π.χ., ονόματα προϊόντων). |
| **Τι γίνεται αν η εικόνα είναι κεκλιμένη;** | Η μηχανή OCR ανιχνεύει αυτόματα τον προσανατολισμό, αλλά μπορείτε να καλέσετε χειροκίνητα `ocrEngine.ImagePreprocessing.Rotate(angle)` για επίμονες περιπτώσεις. |
| **Υπάρχει τρόπος να επισημάνω τις προτάσεις στο UI;** | Αφού έχετε τη συλλογή `misspellings`, μπορείτε να αντιστοιχίσετε κάθε `entry.Word` στην θέση του στο `ocrResult.Text` και να το υπογραμμίσετε σε RichTextBox ή web view. |

## Συμπέρασμα

Μόλις σας δείξαμε **πώς να εκτελέσετε OCR σε εικόνα**, **πώς να εξάγετε κείμενο από εικόνα**, και στη συνέχεια **πώς να ανιχνεύσετε λανθασμένες λέξεις** ενώ **λαμβάνετε προτάσεις ορθογραφίας**—όλα με μια σύντομη C# κονσόλα εφαρμογή. Η βασική ιδέα είναι απλή: αφήστε το Aspose.OCR να κάνει τη βαριά δουλειά της αναγνώρισης χαρακτήρων, και στη συνέχεια αφήστε τον ενσωματωμένο ορθογραφικό ελεγκτή να καθαρίσει την έξοδο. Από εδώ μπορείτε να επεκτείνετε την επίδειξη σε μια πλήρη υπηρεσία επεξεργασίας εγγράφων, να την ενσωματώσετε με ένα web API, ή να την συνδέσετε με έναν επεξεργαστή επιφάνειας εργασίας.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να αλλάξετε τη γλώσσα στα Ισπανικά, τροφοδοτήστε ένα PDF πολλαπλών σελίδων, ή δημιουργήστε ένα μικρό WPF front‑end που επιτρέπει στους χρήστες να κάνουν κλικ σε μια λέξη για να αποδεχτούν μια πρόταση. Τα δομικά στοιχεία είναι ήδη στη θέση τους—συνεχίστε να πειραματίζεστε.

Αν αντιμετωπίσατε προβλήματα ή έχετε ιδέες για επεκτάσεις, αφήστε ένα σχόλιο παρακάτω. Καλή προγραμματιστική!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετικά θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Εξαγωγή κειμένου από εικόνα – Βελτιστοποίηση OCR με Aspose.OCR για .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}