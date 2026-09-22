---
category: general
date: 2026-01-09
description: c# οδηγός OCR που δείχνει πώς να εξάγετε κείμενο από αρχεία εικόνας και
  να μετατρέψετε DJVU σε κείμενο χρησιμοποιώντας το Aspose.OCR. Μάθετε την εξαγωγή
  βήμα‑βήμα σε λίγα λεπτά.
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- how to extract text
- convert djvu to text
- extract text from djvu
language: el
og_description: c# OCR tutorial που δείχνει γρήγορα πώς να εξάγετε κείμενο από αρχεία
  εικόνας και να μετατρέψετε DJVU σε κείμενο χρησιμοποιώντας το Aspose.OCR. Ακολουθήστε
  τον οδηγό για μια λειτουργική λύση.
og_title: c# OCR οδηγός – Εξαγωγή κειμένου από εικόνα & DJVU
tags:
- OCR
- C#
- Aspose
title: 'c# OCR οδηγός: Εξαγωγή κειμένου από εικόνα και αρχεία DJVU'
url: /el/net/text-recognition/c-ocr-tutorial-extract-text-from-image-and-djvu-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR tutorial – Εξαγωγή κειμένου από εικόνα και αρχεία DJVU

Αναρωτηθήκατε ποτέ πώς να εξάγετε κείμενο από αρχεία εικόνας χωρίς να τσακώσετε τα μαλλιά σας; Σε αυτό το **c# OCR tutorial** θα περάσουμε από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που εξάγει κείμενο από μια κανονική εικόνα *και* ένα έγγραφο DJVU.  

Αν ψάχνετε επίσης για έναν γρήγορο τρόπο να **convert DJVU to text**, βρίσκεστε στο σωστό μέρος—χωρίς επιπλέον μετατροπείς, μόνο καθαρός κώδικας C#.

## Τι θα μάθετε

- Πώς να εγκαταστήσετε τη βιβλιοθήκη Aspose.OCR σε ένα έργο .NET.  
- Ο ακριβής κώδικας που χρειάζεστε για **extract text from image** αρχεία.  
- Μια σύντομη μέθοδος για **extracting text from DJVU** αρχεία (ναι, η ίδια μηχανή το κάνει).  
- Κοινά προβλήματα (μεγάλα αρχεία, ελλιπείς γραμματοσειρές, άδειες) και πώς να τα αποφύγετε.  

Το μόνο που χρειάζεστε είναι ένα πρόσφατο .NET SDK και σύνδεση στο διαδίκτυο για να κατεβάσετε το πακέτο NuGet. Δεν απαιτείται προηγούμενη εμπειρία OCR.

## Προαπαιτούμενα

| Απαίτηση | Γιατί είναι σημαντικό |
|-------------|----------------|
| .NET 6.0 ή νεότερο | Το Aspose.OCR στοχεύει στο .NET Standard 2.0, έτσι το .NET 6+ προσφέρει την καλύτερη απόδοση. |
| Visual Studio 2022 (ή VS Code) | Τα IDE κάνουν τη διαχείριση πακέτων απλή, αλλά οποιοσδήποτε επεξεργαστής λειτουργεί. |
| Πακέτο NuGet **Aspose.OCR** | Αυτή είναι η μηχανή που πραγματικά κάνει τη βαριά δουλειά. |
| Ένα δείγμα εικόνας (`sample.png`) και ένα αρχείο DJVU (`sample.djvu`) | Θα τα χρησιμοποιήσουμε για να δείξουμε και τα δύο σενάρια εξαγωγής. |

Μπορείτε να εγκαταστήσετε το πακέτο με την ακόλουθη εντολή:

```bash
dotnet add package Aspose.OCR
```

> **Συμβουλή:** Αν βρίσκεστε σε διακομιστή CI, προσθέστε `--no-restore` στο βήμα κατασκευής και κάντε restore μία φορά στην αρχή για να επιταχύνετε τη διαδικασία.

## Βήμα 1: Αρχικοποίηση της μηχανής OCR – η καρδιά του c# OCR tutorial

Το πρώτο που κάνουμε είναι να δημιουργήσουμε μια παρουσία του `OcrEngine`. Σκεφτείτε το σαν να ενεργοποιείτε το σαρωτή στο λογισμικό σας.

```csharp
using Aspose.OCR;

var ocrEngine = new OcrEngine();
```

Γιατί να δημιουργούμε νέα μηχανή κάθε φορά; Επειδή η μηχανή κρατάει ρυθμίσεις (γλώσσα, λειτουργία ανίχνευσης κλπ.). Ξεκινώντας φρέσκο αποφεύγετε τις παλιές ρυθμίσεις να διαρρέουν μεταξύ εκτελέσεων.

## Βήμα 2: Φόρτωση και αναγνώριση εικόνας – πώς να extract text from image

Τώρα θα τροφοδοτήσουμε μια κανονική bitmap (PNG, JPEG, BMP…) στη μηχανή. Η μέθοδος `RecognizeImage` επιστρέφει τη ανιχνευμένη συμβολοσειρά.

```csharp
// Path to your image file
string imagePath = @"C:\OCR\sample.png";

// Perform OCR
string imageText = ocrEngine.RecognizeImage(imagePath);

// Show the result
Console.WriteLine("=== Text extracted from image ===");
Console.WriteLine(imageText);
```

Μερικά πράγματα που πρέπει να σημειώσετε:

* **Υπάρχον αρχείο** – Αν η διαδρομή είναι λανθασμένη η μέθοδος ρίχνει `FileNotFoundException`. Τυλίξτε την σε `try/catch` αν περιμένετε διαδρομές από χρήστη.
* **Ποιότητα εικόνας** – Το OCR λειτουργεί καλύτερα σε 300 dpi ή περισσότερο. Σαρώσεις χαμηλής ανάλυσης μπορεί να παράγουν ακατάστατο κείμενο.
* **Υποστήριξη γλώσσας** – Από προεπιλογή το Aspose.OCR υποθέτει Αγγλικά. Για αλλαγή, ορίστε `ocrEngine.Language = Language.Spanish;` πριν το `RecognizeImage`.

## Βήμα 3: Αναγνώριση κειμένου από έγγραφο DJVU – convert DJVU to text

Το DJVU είναι μορφή κοντέινερ που μπορεί να περιέχει πολλαπλές σελίδες. Το Aspose.OCR μπορεί να το διαχειριστεί άμεσα· απλώς δείχνετε στο αρχείο.

```csharp
// Path to your DJVU file
string djvuPath = @"C:\OCR\sample.djvu";

// Perform OCR on the DJVU file
string djvuText = ocrEngine.RecognizeImage(djvuPath);

// Output the result
Console.WriteLine("\n=== Text extracted from DJVU ===");
Console.WriteLine(djvuText);
```

Στο παρασκήνιο, η μηχανή εξάγει κάθε σελίδα ως εικόνα και εκτελεί την ίδια διαδικασία αναγνώρισης. Γι’ αυτό δεν χρειάζεται ξεχωριστό βήμα “convert DJVU to text”—η μηχανή OCR το κάνει για εσάς.

### Διαχείριση αρχείων DJVU πολλαπλών σελίδων

Αν το DJVU σας περιέχει πολλές σελίδες, το `RecognizeImage` τις συνενώνει με τη σειρά. Αν χρειάζεστε κάθε σελίδα ξεχωριστά, μπορείτε να χρησιμοποιήσετε την υπερφόρτωση που επιστρέφει `List<string>`:

```csharp
var pagesText = ocrEngine.RecognizeImage(djvuPath, true); // true = return per‑page list
for (int i = 0; i < pagesText.Count; i++)
{
    Console.WriteLine($"\n--- Page {i + 1} ---");
    Console.WriteLine(pagesText[i]);
}
```

## Βήμα 4: Λεπτομερής ρύθμιση της μηχανής για καλύτερη ακρίβεια – γιατί είναι σημαντικό

Τα αρχικά αποτελέσματα είναι αποδεκτά, αλλά μπορείτε να τα βελτιώσετε ρυθμίζοντας μερικές παραμέτρους:

```csharp
ocrEngine.Language = Language.English;      // set detection language
ocrEngine.Dpi = 300;                        // enforce 300 DPI processing
ocrEngine.IsDetectOrientation = true;      // auto‑rotate tilted pages
ocrEngine.IsDetectSkew = true;              // correct slanted text
```

Αυτές οι σημαίες είναι ιδιαίτερα χρήσιμες όταν **how to extract text** από σαρωμένα PDF που πρώτα αποθηκεύτηκαν ως DJVU. Η ενεργοποίηση της ανίχνευσης προσανατολισμού σας εξοικονομεί το χειροκίνητο περιστροφή των εικόνων.

## Βήμα 5: Διαχείριση αδειών και σφαλμάτων χρόνου εκτέλεσης

Το Aspose.OCR διανέμεται με δωρεάν δοκιμή που προσθέτει το σήμα “Demo” στην έξοδο μετά από μερικές σελίδες. Για να αφαιρέσετε το υδατογράφημα, προσθέστε το αρχείο άδειας:

```csharp
// Assuming you have a license.xml in the project root
var license = new Aspose.OCR.License();
license.SetLicense("license.xml");
```

Αν ξεχάσετε αυτό το βήμα, η μηχανή λειτουργεί, αλλά το αποτέλεσμα θα περιέχει τη λέξη “Demo”. Επίσης, προσέξτε το `OutOfMemoryException` όταν επεξεργάζεστε τεράστια αρχεία DJVU—σκεφτείτε επεξεργασία σελίδα‑με‑σελίδα όπως φαίνεται νωρίτερα.

## Πλήρες, εκτελέσιμο παράδειγμα

Παρακάτω είναι ένα αυτόνομο πρόγραμμα κονσόλας που συνδυάζει όλα. Αντιγράψτε‑επικολλήστε, προσαρμόστε τις διαδρομές αρχείων, και πατήστε **Run**.

```csharp
// Complete c# OCR tutorial – extract text from image and DJVU
using System;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Set up licensing (optional, removes demo watermark)
            // var license = new License();
            // license.SetLicense("license.xml");

            // 2️⃣ Create the OCR engine
            var ocrEngine = new OcrEngine
            {
                Language = Language.English,
                Dpi = 300,
                IsDetectOrientation = true,
                IsDetectSkew = true
            };

            // 👉 Extract text from a regular image
            string imagePath = @"C:\OCR\sample.png";
            try
            {
                string imageText = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("=== Text extracted from image ===");
                Console.WriteLine(imageText);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Image OCR failed: {ex.Message}");
            }

            // 👉 Extract text from a DJVU file (convert DJVU to text)
            string djvuPath = @"C:\OCR\sample.djvu";
            try
            {
                // Single string for all pages
                string djvuText = ocrEngine.RecognizeImage(djvuPath);
                Console.WriteLine("\n=== Text extracted from DJVU ===");
                Console.WriteLine(djvuText);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"DJVU OCR failed: {ex.Message}");
            }

            // Keep console open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Expected output** (assuming the files contain the phrase “Hello World”):

```
=== Text extracted from image ===
Hello World

=== Text extracted from DJVU ===
Hello World
```

Αν η πηγή περιέχει πολλές γραμμές, θα εμφανιστούν ακριβώς όπως στο αρχικό έγγραφο.

## Συχνές ερωτήσεις & διαχείριση ειδικών περιπτώσεων

* **Τι γίνεται αν η εικόνα είναι ασπρόμαυρη;**  
  Το OCR λειτουργεί καλά, αλλά μπορείτε να βελτιώσετε την αντίθεση με `ocrEngine.ImagePreprocessOptions = ImagePreprocessOptions.Contrast;`.

* **Μπορώ να εξάγω μόνο αριθμούς;**  
  Ναι—ορίστε `ocrEngine.CharWhitelist = "0123456789";` πριν καλέσετε το `RecognizeImage`.

* **Υπάρχει όριο στο μέγεθος του αρχείου;**  
  Η μηχανή διαβάζει ολόκληρο το αρχείο στη μνήμη. Για αρχεία μεγαλύτερα από ~100 MB, επεξεργαστείτε σελίδα‑με‑σελίδα (δείτε την υπερφόρτωση λίστας του Βήματος 3).

* **Πώς διαφέρει αυτό από το Tesseract;**  
  Το Aspose.OCR είναι εμπορική βιβλιοθήκη με ενσωματωμένη υποστήριξη DJVU και χωρίς εγγενείς εξαρτήσεις, ενώ το Tesseract απαιτεί εγγενή binaries και ξεχωριστά εργαλεία μετατροπής DJVU.

## Συμπέρασμα

Μόλις ολοκληρώσατε ένα **c# OCR tutorial** που δείχνει πώς να **extract text from image** αρχεία και αβίαστα **convert DJVU to text** χρησιμοποιώντας το Aspose.OCR. Το παράδειγμα καλύπτει τα πάντα από την εγκατάσταση του πακέτου μέχρι τις άδειες, από την εξαγωγή εικόνας μιας σελίδας μέχρι τη διαχείριση DJVU πολλαπλών σελίδων, και ακόμη συμβουλές για βελτίωση της ακρίβειας.  

Στη συνέχεια, μπορείτε να εξερευνήσετε **how to extract text** από PDF, να ενσωματώσετε το βήμα OCR σε ένα web API, ή να πειραματιστείτε με πακέτα γλωσσών για πολυγλωσσικά έγγραφα. Ο ουρανός είναι το όριο—απλώς θυμηθείτε τα βασικά: ρυθμίστε τη μηχανή, τροφοδοτήστε την με ένα αρχείο, και διαβάστε τη συμβολοσειρά πίσω.  

Έχετε περισσότερες ερωτήσεις; Αφήστε ένα σχόλιο, δοκιμάστε τον κώδικα στα δικά σας έγγραφα, και καλή προγραμματιστική! 

![c# OCR tutorial screenshot showing console output](/images/csharp-ocr-tutorial.png "c# OCR tutorial – παράδειγμα εξόδου κονσόλας")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}