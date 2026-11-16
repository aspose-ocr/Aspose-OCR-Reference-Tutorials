---
category: general
date: 2026-03-05
description: Μετατρέψτε TIFF σε κείμενο σε C# γρήγορα με το Aspose OCR. Μάθετε πώς
  να εμφανίζετε κείμενο OCR από πολυσελιδικά αρχεία TIFF σε λίγα λεπτά.
draft: false
keywords:
- convert tiff to text
- aspose ocr c#
- display ocr text
language: el
og_description: Μετατρέψτε TIFF σε κείμενο σε C# με το Aspose OCR. Αυτός ο οδηγός
  σας δείχνει πώς να εμφανίσετε το κείμενο OCR από πολυ‑σελίδες TIFF εικόνες βήμα‑βήμα.
og_title: Μετατροπή TIFF σε Κείμενο σε C# – Πλήρης Οδηγός Aspose OCR
tags:
- Aspose
- OCR
- C#
- TIFF
title: Μετατροπή TIFF σε κείμενο σε C# χρησιμοποιώντας Aspose OCR
url: /el/net/text-recognition/convert-tiff-to-text-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή TIFF σε Κείμενο σε C# Χρησιμοποιώντας Aspose OCR

Χρειάζεστε **μετατροπή TIFF σε κείμενο** σε C#; Δεν είστε μόνοι—πολλοί προγραμματιστές προσπαθούν να εξάγουν αναγνώσιμες συμβολοσειρές από αρχεία TIFF πολλαπλών σελίδων. Τα καλά νέα είναι ότι το Aspose OCR C# κάνει τη δουλειά σχεδόν αβίαστη, και μπορείτε να **εμφανίσετε το κείμενο OCR** στην κονσόλα ή να το δώσετε σε άλλο σύστημα σε δευτερόλεπτα.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που δείχνει ακριβώς πώς να φορτώσετε ένα TIFF πολλαπλών σελίδων, να τρέξετε OCR και να εκτυπώσετε το κείμενο κάθε σελίδας. Χωρίς κρυφά βήματα, χωρίς συντομεύσεις «δείτε την τεκμηρίωση». Στο τέλος θα έχετε ένα αυτόνομο πρόγραμμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET.

## Τι Θα Χρειαστείτε

- .NET 6.0 ή νεότερο (το παράδειγμα στοχεύει .NET 6, αλλά .NET 5 λειτουργεί επίσης)  
- Ένα έγκυρο αρχείο άδειας Aspose OCR (`Aspose.OCR.lic`). Η βιβλιοθήκη λειτουργεί χωρίς άδεια, αλλά θα εμφανίσει υδατογράφημα δοκιμής 20 δευτερολέπτων.  
- Ένα αρχείο TIFF πολλαπλών σελίδων που θέλετε να επεξεργαστείτε (θα το ονομάσουμε `multipage.tif`).  
- Visual Studio 2022 ή οποιονδήποτε επεξεργαστή προτιμάτε—τίποτα εξειδικευμένο.

Αν έχετε τσεκάρει όλα τα παραπάνω, ας βουτήξουμε.

## Βήμα 1: Εγκατάσταση του Πακέτου NuGet Aspose OCR

Πριν τρέξει οποιοσδήποτε κώδικας, χρειάζεστε τη βιβλιοθήκη. Ανοίξτε ένα τερματικό στο φάκελο του έργου σας και εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

Αυτή η εντολή τραβά την πιο πρόσφατη σταθερή έκδοση (από Μάρτιο 2026 είναι η 23.9).  

> **Συμβουλή:** Κρατήστε τα πακέτα σας ενημερωμένα· οι νεότερες εκδόσεις συχνά περιλαμβάνουν βελτιώσεις απόδοσης για μεγάλα TIFF.

## Βήμα 2: Ρύθμιση της Άδειας Aspose OCR C# (Προαιρετικό αλλά Συνιστάται)

Η εκτέλεση της μηχανής OCR χωρίς άδεια είναι δυνατή, αλλά το αποτέλεσμα θα προεξέχει με προειδοποίηση δοκιμής. Για να το αποφύγετε, δείξτε στη μηχανή το αρχείο `.lic` σας:

```csharp
using Aspose.OCR;

// ...

// Step 2: Apply your Aspose OCR license (optional but recommended)
var ocrEngine = new OcrEngine();
ocrEngine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
```

Αν παραλείψετε αυτό το βήμα, ο κώδικας λειτουργεί ακόμα—απλώς θυμηθείτε το επιπλέον κείμενο στα αποτελέσματα.

## Βήμα 3: Φόρτωση και Αναγνώριση του TIFF Πολλαπλών Σελίδων

Τώρα πραγματικά **μετατρέπουμε TIFF σε κείμενο**. Η βοηθητική μέθοδος `ImageStream.FromFile` διαβάζει το αρχείο σε μορφή που καταλαβαίνει η μηχανή. Μετά καλούμε το `Recognize()` που επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει το κείμενο κάθε σελίδας.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

// ...

// Step 3: Load the multi‑page TIFF image to be processed
ocrEngine.Image = ImageStream.FromFile(@"C:\Images\multipage.tif");

// Step 4: Perform OCR on the loaded image
OcrResult ocrResult = ocrEngine.Recognize();
```

> **Γιατί είναι σημαντικό:** Η `Recognize()` κάνει το σκληρό έργο—ανάλυση εικονοστοιχείων, ανίχνευση γλώσσας και ανασύνθεση γραμμών κειμένου—όλα σε γνήσιο κώδικα C#. Το αντικείμενο αποτελέσματος σας δίνει πρόσβαση σελίδα‑με‑σελίδα, κάτι τέλειο για **εμφάνιση κειμένου OCR** αργότερα.

## Βήμα 4: Επανάληψη στις Σελίδες και **Εμφάνιση Κειμένου OCR**

Με το αποτέλεσμα στα χέρια, απλώς διασχίζουμε τις σελίδες και εκτυπώνουμε καθεμία. Αυτό είναι το τμήμα όπου βλέπετε πραγματικά τη μετατροπή από εικόνα σε απλό κείμενο.

```csharp
// Step 5: Iterate through each page of the result and display the recognized text
for (int pageIndex = 0; pageIndex < ocrResult.PageCount; pageIndex++)
{
    Console.WriteLine($"--- Page {pageIndex + 1} ---");
    Console.WriteLine(ocrResult.GetPageText(pageIndex));
    Console.WriteLine(); // Blank line for readability
}
```

Η εκτέλεση του προγράμματος δίνει έξοδο παρόμοια με την παρακάτω (το πραγματικό κείμενο θα διαφέρει ανάλογα με το περιεχόμενο του TIFF):

```
--- Page 1 ---
Hello, world!
This is the first page of our multi‑page TIFF.

--- Page 2 ---
Second page starts here.
More sample text follows.
```

Αυτό ήταν—έχετε **μετατρέψει επιτυχώς TIFF σε κείμενο** και **εμφανίσει κείμενο OCR** για κάθε σελίδα.

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε ένα νέο κονσόλα έργο (`dotnet new console`). Περιλαμβάνει όλες τις οδηγίες `using`, τη διαχείριση άδειας και έλεγχο σφαλμάτων.

```csharp
// ConvertTiffToText.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ConvertTiffToText
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Create an OCR engine instance
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine();

            // -----------------------------------------------------------------
            // Step 2: Apply your Aspose OCR license (optional but recommended)
            // -----------------------------------------------------------------
            try
            {
                ocrEngine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
            }
            catch (Exception ex)
            {
                Console.WriteLine("License file not found or invalid. Running in trial mode.");
                Console.WriteLine($"Details: {ex.Message}");
            }

            // -----------------------------------------------------------------
            // Step 3: Load the multi‑page TIFF image to be processed
            // -----------------------------------------------------------------
            const string tiffPath = @"C:\Images\multipage.tif";

            if (!System.IO.File.Exists(tiffPath))
            {
                Console.WriteLine($"Error: TIFF file not found at {tiffPath}");
                return;
            }

            ocrEngine.Image = ImageStream.FromFile(tiffPath);

            // -----------------------------------------------------------------
            // Step 4: Perform OCR – this is where we convert TIFF to text
            // -----------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize();

            // -----------------------------------------------------------------
            // Step 5: Iterate through each page and display OCR text
            // -----------------------------------------------------------------
            Console.WriteLine($"Successfully processed {ocrResult.PageCount} page(s).");
            for (int i = 0; i < ocrResult.PageCount; i++)
            {
                Console.WriteLine($"--- Page {i + 1} ---");
                Console.WriteLine(ocrResult.GetPageText(i));
                Console.WriteLine(); // Add spacing between pages
            }

            // Keep the console window open when debugging
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Αναμενόμενη έξοδος** (κομμένη για συντομία) φαίνεται παραπάνω. Αν δείτε το υδατογράφημα δοκιμής, ελέγξτε ξανά τη διαδρομή της άδειας.

## Συνηθισμένα Προβλήματα Κατά τη Μετατροπή TIFF σε Κείμενο

| Πρόβλημα | Γιατί Συμβαίνει | Πώς να Το Διορθώσετε |
|----------|------------------|----------------------|
| **Έλλειψη μνήμης σε τεράστια TIFF** | Η μηχανή φορτώνει ολόκληρη την εικόνα στη RAM. | Χρησιμοποιήστε `ImageStream.FromFile(..., loadOnlyFirstPage: false)` και επεξεργαστείτε τις σελίδες σε παρτίδες, ή αυξήστε το όριο μνήμης της διεργασίας. |
| **Ασυνήθιστα χαρακτήρες** | Εικόνες χαμηλής ανάλυσης μπερδεύουν τη μηχανή OCR. | Προεπεξεργαστείτε το TIFF (π.χ., αυξήστε το DPI σε 300) πριν το δώσετε στο Aspose OCR. |
| **Η άδεια δεν εφαρμόστηκε** | Η `SetLicense` πετάει εξαίρεση που αγνοείτε. | Περιβάλλετε την κλήση σε try/catch (όπως φαίνεται) και καταγράψτε το σφάλμα. |
| **Λείπουν δεδομένα γλώσσας** | Από προεπιλογή το OCR υποθέτει Αγγλικά. | Ορίστε `ocrEngine.Language = OcrLanguage.French;` (ή οποιαδήποτε υποστηριζόμενη γλώσσα) πριν το `Recognize()`. |

Η αντιμετώπιση αυτών των περιπτώσεων εξασφαλίζει ομαλή λειτουργία της μετατροπής σε παραγωγικό περιβάλλον.

## Επόμενα Βήματα: Πέρα από την Απλή Εμφάνιση

Τώρα που μπορείτε να **μετατρέψετε TIFF σε κείμενο** και να **εμφανίσετε κείμενο OCR**, ίσως θελήσετε να:

- **Αποθηκεύσετε το εξαγόμενο κείμενο** σε αρχείο `.txt` ή σε βάση δεδομένων για μετέπειτα ανάλυση.  
- **Συνδυάσετε πολλαπλά TIFF** σε ένα ενιαίο αναζητήσιμο PDF χρησιμοποιώντας Aspose.PDF.  
- **Εφαρμόσετε μετα‑επεξεργασία** (ορθογραφικό έλεγχο, καθαρισμό με regex) για βελτίωση της ακρίβειας.  

Όλες αυτές οι επεκτάσεις βασίζονται στο ίδιο βασικό μοτίβο που καλύψαμε.

---

### TL;DR

Διασχίσαμε μια πλήρη λύση C# που **μετατρέπει TIFF σε κείμενο** χρησιμοποιώντας Aspose OCR C#. Ο κώδικας δημιουργεί ένα `OcrEngine`, προαιρετικά φορτώνει άδεια, διαβάζει ένα TIFF πολλαπλών σελίδων, τρέχει OCR και **εμφανίζει κείμενο OCR** σελίδα‑με‑σελίδα. Με το παρεχόμενο πλήρες παράδειγμα, μπορείτε να το ενσωματώσετε σε οποιοδήποτε έργο .NET και να αρχίσετε αμέσως την εξαγωγή κειμένου.

Έχετε ερωτήσεις σχετικά με την απόδοση, την υποστήριξη γλωσσών ή την ενσωμάτωση με άλλα προϊόντα Aspose; Αφήστε ένα σχόλιο παρακάτω—καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}