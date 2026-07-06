---
category: general
date: 2026-02-11
description: Εξαγωγή κειμένου από εικόνα σε C# χρησιμοποιώντας το Aspose OCR. Μάθετε
  πώς να φορτώνετε εικόνα για OCR, να βελτιώνετε την ακρίβεια του OCR και να διορθώνετε
  σφάλματα OCR με ορθογραφικό έλεγχο.
draft: false
keywords:
- extract text from image
- image to text c#
- improve ocr accuracy
- load image for ocr
- fix ocr errors
language: el
og_description: Εξαγωγή κειμένου από εικόνα σε C# με Aspose OCR. Αυτός ο οδηγός δείχνει
  πώς να φορτώσετε εικόνα για OCR, να βελτιώσετε την ακρίβεια του OCR και να διορθώσετε
  τα σφάλματα του OCR.
og_title: Εξαγωγή κειμένου από εικόνα σε C# – Πλήρης οδηγός OCR
tags:
- C#
- OCR
- Aspose
- Text Extraction
title: Εξαγωγή κειμένου από εικόνα σε C# – Πλήρης οδηγός OCR
url: /el/net/ocr-optimization/extract-text-from-image-in-c-complete-ocr-guide/
---

to keep all code block placeholders as they were.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Εικόνα σε C# – Πλήρης Οδηγός OCR

Σας έχει συμβεί ποτέ να χρειάζεστε **εξαγωγή κειμένου από εικόνα** αλλά τα αποτελέσματα να μοιάζουν με ακαταλαβίστικα; Δεν είστε οι μόνοι. Σε πολλές πραγματικές εφαρμογές—όπως σάρωση αποδείξεων, ψηφιοποίηση σημειώσεων ή μεταφορά παλαιών εγγράφων—η λήψη καθαρού κειμένου από μια εικόνα είναι το πρώτο, και συχνά το πιο δύσκολο, εμπόδιο.

Ευτυχώς, με το Aspose OCR μπορείτε να **φορτώσετε εικόνα για OCR**, να εκτελέσετε ορθογραφικό έλεγχο και να αποκτήσετε καθαρό, αναζητήσιμο κείμενο. Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία, από την ανάγνωση ενός JPEG μέχρι την τελειοποίηση του αποτελέσματος, και θα δείτε ακριβώς πώς να **βελτιώσετε την ακρίβεια του OCR**.

> **Τι θα πάρετε στο τέλος:** ένα έτοιμο προς εκτέλεση πρόγραμμα C# console που εξάγει κείμενο από εικόνα, διορθώνει κοινά σφάλματα OCR, και εκτυπώνει τόσο τα ακατέργαστα όσο και τα καθαρισμένα αποτελέσματα.

---

## Τι Θα Χρειαστείτε

- .NET 6 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.7+)
- Visual Studio 2022 (ή οποιοδήποτε IDE προτιμάτε)
- Ένα δωρεάν κλειδί δοκιμής Aspose OCR ή μια άδεια έκδοση
- Ένα αρχείο εικόνας που περιέχει τυπωμένο ή εκτυπωμένο κείμενο (π.χ., `typed_note.jpg`)

Δεν απαιτούνται άλλες βιβλιοθήκες τρίτων—το Aspose διαχειρίζεται αυτόματα τα μοντέλα γλώσσας και τον ορθογραφικό έλεγχο.

## Βήμα 1 – Εγκατάσταση του πακέτου NuGet Aspose OCR

Πριν μπορέσουμε να **εξάγουμε κείμενο από εικόνα**, η μηχανή OCR πρέπει να είναι διαθέσιμη στον υπολογιστή.

```powershell
# From the Package Manager Console
Install-Package Aspose.OCR
```

Ή, αν προτιμάτε τη γραμμή εντολών (CLI):

```bash
dotnet add package Aspose.OCR
```

Το πακέτο περιλαμβάνει δεδομένα γλώσσας, αλλά ο ορισμός του `AutomaticResourceDownload = true` (όπως θα κάνουμε αργότερα) εξασφαλίζει ότι τυχόν λείποντα λεξικά θα ληφθούν κατά την εκτέλεση.

## Βήμα 2 – Φόρτωση Εικόνας για OCR

Το πρώτο που χρειάζεται η μηχανή είναι ένα bitmap. Μπορείτε να της δώσετε οποιαδήποτε μορφή υποστηρίζεται από το `System.Drawing.Image`, όπως PNG, JPEG, BMP ή TIFF.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

// Path to your source picture – change this to your own folder
string imagePath = @"C:\MyImages\typed_note.jpg";

// Load the image inside a using block so the file handle is released promptly
using (Image image = Image.FromFile(imagePath))
{
    // The rest of the OCR pipeline lives inside this block
}
```

> **Γιατί το μπλοκ `using`;** Αποδεσμεύει αυτόματα το αντικείμενο `Image`, αποτρέποντας προβλήματα κλειδώματος αρχείων που συχνά ενοχλούν τους προγραμματιστές που ξεχνούν να απελευθερώσουν πόρους.

## Βήμα 3 – Εκτέλεση OCR – “Image to Text C#” σε Δράση

Τώρα πραγματικά **εξάγουμε κείμενο από εικόνα**. Η κλάση `OcrEngine` κάνει τη βαριά δουλειά.

```csharp
// Step 3: Initialise the OCR engine
var ocrEngine = new OcrEngine
{
    AutomaticResourceDownload = true, // pulls language packs if missing
    Language = OcrLanguage.English    // set to your document's language
};

// Inside the using block from Step 2
var ocrResult = ocrEngine.Recognize(image);
string rawText = ocrResult.Text;
Console.WriteLine("Raw OCR output:");
Console.WriteLine(rawText);
```

Σε αυτό το σημείο έχετε μια συμβολοσειρά που αντικατοπτρίζει ό,τι βλέπει η μηχανή στην εικόνα. Στην πράξη, το αποτέλεσμα μπορεί να περιέχει άσχετους χαρακτήρες, λανθασμένα αναγνωρισμένες λέξεις ή περίεργα διαχωριστικά γραμμών—γι' αυτό το επόμενο βήμα.

## Βήμα 4 – Βελτίωση της Ακρίβειας του OCR με Ορθογραφικό Έλεγχο

Το Aspose περιλαμβάνει έναν ειδικό `SpellChecker` που γνωρίζει τη γλώσσα που επεξεργάζεστε. Η εκτέλεσή του πάνω στη ακατέργαστη συμβολοσειρά συχνά διορθώνει τα πιο εμφανή σφάλματα.

```csharp
// Step 4: Initialise spell‑check (resources are auto‑downloaded)
var spellChecker = new SpellChecker(OcrLanguage.English);

// Correct the OCR output
string correctedText = spellChecker.Correct(rawText);
Console.WriteLine("\nCorrected OCR output:");
Console.WriteLine(correctedText);
```

**Συμβουλή:** Αν εργάζεστε με λεξιλόγια ειδικών τομέων (π.χ. ιατρικούς όρους), μπορείτε να παρέχετε ένα προσαρμοσμένο λεξικό στο `SpellChecker` μέσω των υπερφορτώσεων του.

## Βήμα 5 – Διόρθωση Σφαλμάτων OCR Χειροκίνητα (Προαιρετικό)

Ακόμη και ο καλύτερος ορθογραφικός ελεγκτής μπορεί να παραλείψει λάθη που εξαρτώνται από το συμφραζόμενο. Μια γρήγορη επεξεργασία μετά την εξαγωγή μπορεί να εντοπίσει πράγματα όπως “l” vs “1” ή “O” vs “0”.

```csharp
// Simple regex to replace common OCR confusions
string finalText = System.Text.RegularExpressions.Regex.Replace(
    correctedText,
    @"\b([lI])\b", // isolated l or I
    "1");

// Additional custom rules can be added here
Console.WriteLine("\nFinal cleaned text:");
Console.WriteLine(finalText);
```

Μη διστάσετε να επεκτείνετε αυτήν την ενότητα με τις δικές σας ευρετικές μεθόδους—ίσως έναν πίνακα αναζήτησης για κωδικούς προϊόντων ή μια λίστα γνωστών συντομογραφιών.

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα νέο έργο Console App. Περιλαμβάνει κάθε βήμα που συζητήθηκε, συν χρήσιμα σχόλια.

```csharp
// ------------------------------------------------------------
// Extract Text from Image in C# – Full Example
// ------------------------------------------------------------
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure OCR engine – automatic download ensures language data is present
        var ocrEngine = new OcrEngine
        {
            AutomaticResourceDownload = true,
            Language = OcrLanguage.English
        };

        // 2️⃣ Load the image you want to analyse
        string imagePath = @"C:\MyImages\typed_note.jpg";
        using (Image image = Image.FromFile(imagePath))
        {
            // 3️⃣ Run OCR – this is where we *extract text from image*
            var ocrResult = ocrEngine.Recognize(image);
            string rawText = ocrResult.Text;
            Console.WriteLine("Before (raw OCR):");
            Console.WriteLine(rawText);
            Console.WriteLine(new string('-', 40));

            // 4️⃣ Spell‑check to *improve OCR accuracy*
            var spellChecker = new SpellChecker(OcrLanguage.English);
            string correctedText = spellChecker.Correct(rawText);
            Console.WriteLine("After (spell‑checked):");
            Console.WriteLine(correctedText);
            Console.WriteLine(new string('-', 40));

            // 5️⃣ Optional custom clean‑up – *fix OCR errors* that the spell‑checker missed
            string finalText = Regex.Replace(correctedText,
                @"\b([lI])\b", // replace isolated 'l' or 'I' with '1'
                "1");

            Console.WriteLine("Final (post‑processed):");
            Console.WriteLine(finalText);
        }
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Υποθέτοντας ότι το `typed_note.jpg` περιέχει την πρόταση “Hello world, this is a test 123”, η κονσόλα θα εμφανίσει κάτι όπως:

```
Before (raw OCR):
H3llo w0rld, th1s is a test 123

After (spell‑checked):
Hello world, this is a test 123

Final (post‑processed):
Hello world, this is a test 123
```

Παρατηρήστε πώς ο ορθογραφικός ελεγκτής μετατρέπει το “H3llo” σε “Hello”, και η regex καθαρίζει το άσχετο “1” που εμφανίστηκε στο “th1s”.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

| Ερώτηση | Απάντηση |
|----------|--------|
| **Μπορώ να χρησιμοποιήσω διαφορετική γλώσσα;** | Ναι. Ορίστε `ocrEngine.Language = OcrLanguage.Spanish` (ή οποιοδήποτε υποστηριζόμενο enum) και περάστε την ίδια γλώσσα στο `SpellChecker`. |
| **Τι γίνεται αν η εικόνα μου είναι πολύ μεγάλη;** | Μειώστε την ανάλυση πριν τη δώσετε στο OCR· το `Image` διαθέτει τη μέθοδο `GetThumbnailImage` για γρήγορη αλλαγή μεγέθους. |
| **Χρειάζεται σύνδεση στο διαδίκτυο;** | Μόνο την πρώτη φορά που λείπει ένα πακέτο γλώσσας· μετά από αυτό οι πόροι αποθηκεύονται τοπικά. |
| **Πώς διαχειρίζομαι PDF με πολλές σελίδες;** | Μετατρέψτε κάθε σελίδα σε εικόνα (π.χ., χρησιμοποιώντας το `PdfRenderer`) και εκτελέστε την ίδια διαδικασία ανά σελίδα. |
| **Ο ορθογραφικός ελεγκτής είναι γλωσσικά ευαίσθητος;** | Απόλυτα. Χρησιμοποιεί το ίδιο μοντέλο γλώσσας που δώσατε στη μηχανή OCR, εξασφαλίζοντας συνέπεια. |

## Επόμενα Βήματα & Σχετικά Θέματα

- **Επεξεργασία κατά παρτίδες:** Τυλίξτε τον κώδικα σε βρόχο `foreach` για να επεξεργαστείτε έναν φάκελο εικόνων.
- **Χειρόγραφο κείμενο:** Αλλάξτε σε `OcrLanguage.EnglishHandwritten` για καλύτερα αποτελέσματα σε καλλιγραφικές σημειώσεις.
- **Παράλληλη εκτέλεση:** Χρησιμοποιήστε `Parallel.ForEach` για να επιταχύνετε μεγάλες εργασίες σε πολυπύρημες μηχανές.
- **Εξαγωγή σε JSON/CSV:** Σειριοποιήστε το `finalText` μαζί με μεταδεδομένα (όνομα αρχείου, βαθμολογίες εμπιστοσύνης) για επακόλουθη ανάλυση.

Αν σας ενδιαφέρει να μετατρέψετε τις εξαγόμενες συμβολοσειρές σε αναζητήσιμα PDF, δείτε τον οδηγό μας για **«Δημιουργία αναζητήσιμου PDF από εικόνα σε C#»**. Βασίζεται άμεσα στην ίδια διαδικασία OCR που καλύψαμε.

## Συμπέρασμα

Μόλις παρουσιάσαμε έναν πρακτικό τρόπο για **εξαγωγή κειμένου από εικόνα** σε C# χρησιμοποιώντας το Aspose OCR, ενώ δείξαμε επίσης πώς να **φορτώσετε εικόνα για OCR**, **βελτιώσετε την ακρίβεια του OCR**, και **διορθώσετε σφάλματα OCR** με έναν ενσωματωμένο ορθογραφικό ελεγκτή και μια μικρή καθαριότητα με regex. Το πλήρες παράδειγμα λειτουργεί αμέσως, απαιτεί μόνο ένα πακέτο NuGet, και μπορεί να επεκταθεί ώστε να ταιριάζει σε σχεδόν οποιοδήποτε σενάριο ψηφιοποίησης εγγράφων

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}