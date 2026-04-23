---
category: general
date: 2026-02-22
description: Δημιουργήστε PDF με δυνατότητα αναζήτησης και εξάγετε κείμενο από εικόνα
  χρησιμοποιώντας το Aspose OCR. Μάθετε πώς να μετατρέπετε μια εικόνα σε PDF και να
  εξάγετε απλό κείμενο σε ένα ενιαίο σεμινάριο.
draft: false
keywords:
- generate searchable pdf
- extract text from image
- convert image to pdf
- output plain text
- convert scanned image pdf
language: el
og_description: Δημιουργήστε αναζητήσιμο PDF από σαρωμένες εικόνες με το Aspose OCR.
  Αυτός ο οδηγός δείχνει πώς να εξάγετε κείμενο από εικόνα, να παράγετε απλό κείμενο
  και να μετατρέψετε την εικόνα σε PDF.
og_title: Δημιουργία Αναζητήσιμου PDF από Εικόνες – Πλήρης Οδηγός C#
tags:
- C#
- OCR
- PDF generation
- Aspose
title: Δημιουργία Αναζητήσιμου PDF από Εικόνες σε C# – Οδηγός Βήμα‑βήμα
url: /el/net/text-recognition/generate-searchable-pdf-from-images-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Αναζητήσιμου PDF από Εικόνες σε C# – Πλήρης Οδηγός

Έχετε χρειαστεί ποτέ να **δημιουργήσετε αναζητήσιμο PDF** από μια σαρωμένη εικόνα αλλά δεν ήξερατε από πού να ξεκινήσετε; Δεν είστε μόνοι—οι περισσότεροι προγραμματιστές αντιμετωπίζουν αυτό το εμπόδιο όταν συναντούν για πρώτη φορά το OCR. Τα καλά νέα; Με το Aspose OCR μπορείτε να **εξάγετε κείμενο από εικόνα**, **παράγετε απλό κείμενο** και **μετατρέψετε εικόνα σε PDF** με λίγες μόνο γραμμές C#.

Σε αυτόν τον οδηγό θα περάσουμε από τη διαδικασία από τη φόρτωση ενός αρχείου PNG μέχρι την αποθήκευση ενός αναζητήσιμου PDF και ενός αρχείου απλού κειμένου. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο απόσπασμα κώδικα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET. Χωρίς περιττές πληροφορίες, μόνο αυτό που κάνει τη δουλειά.

## Τι Θα Μάθετε

- Πώς να ρυθμίσετε το **Aspose.OCR** σε μια εφαρμογή κονσόλας .NET.  
- Η διαφορά μεταξύ των λειτουργιών **output plain text** και **searchable PDF**.  
- Πώς να **extract text from image** και να το γράψετε σε αρχείο `.txt`.  
- Πώς να **convert image to PDF** που διατηρεί το αρχικό bitmap ενώ προσθέτει ένα κρυφό στρώμα κειμένου.  
- Συμβουλές για επεξεργασία μεγάλων παρτίδων, κοινά προβλήματα και πού να ρυθμίσετε τις παραμέτρους για καλύτερη ακρίβεια.

> **Prerequisites** – Χρειάζεστε .NET 6+ (ή .NET Framework 4.7+), Visual Studio 2022 (ή οποιονδήποτε επεξεργαστή) και άδεια Aspose OCR (ή δωρεάν δοκιμή). Δεν απαιτούνται άλλες βιβλιοθήκες τρίτων.

![παράδειγμα δημιουργημένου αναζητήσιμου PDF](image-placeholder.png "Παράδειγμα ενός δημιουργημένου αναζητήσιμου PDF")

## Βήμα 1: Εγκατάσταση Aspose OCR και Δημιουργία του Μηχανήματος

Πρώτα απ' όλα—προσθέστε το πακέτο NuGet στο έργο σας:

```bash
dotnet add package Aspose.OCR
```

Τώρα μπορούμε να δημιουργήσουμε το OCR engine και να του πούμε ποια γλώσσα χρησιμοποιούμε. Η αγγλική είναι η προεπιλογή, αλλά μπορείτε να μεταβείτε σε γαλλικά, ισπανικά κ.λπ., αλλάζοντας το enum `Language`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine for English
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };
```

**Γιατί είναι σημαντικό:** Η μηχανή κρατά όλες τις ρυθμίσεις—γλώσσα, μορφή εξόδου και προαιρετικές σημαίες προεπεξεργασίας. Ορίζοντάς την μία φορά και επαναχρησιμοποιώντας την αποφεύγετε το κόστος δημιουργίας νέας παρουσίας για κάθε αρχείο.

## Βήμα 2: Εξαγωγή Κειμένου και Αποθήκευση ως Απλό Κείμενο

Αν χρειάζεστε μόνο τους ακατέργαστους χαρακτήρες, αλλάξτε τη μηχανή σε `OutputFormat.Text`. Αυτό λέει στο Aspose OCR να παραλείψει εντελώς τη δημιουργία PDF και να σας δώσει μια συμβολοσειρά.

```csharp
        // Tell the engine to return plain text
        ocrEngine.OutputFormat = OutputFormat.Text;

        // Path to your source image (PNG, JPEG, BMP, etc.)
        string inputImagePath = @"YOUR_DIRECTORY/input.png";

        // Perform recognition – the result contains the extracted string
        OcrResult plainTextResult = ocrEngine.Recognize(Image.Load(inputImagePath));

        // Write the text to a .txt file
        string textOutputPath = @"YOUR_DIRECTORY/output.txt";
        File.WriteAllText(textOutputPath, plainTextResult.Text);
```

**Pro tip:** Το `plainTextResult.Text` αφαιρεί ήδη τις αλλαγές γραμμής που ανήκουν στη διάταξη του OCR. Αν χρειάζεστε το αρχικό διάστημα, εξετάστε το `plainTextResult.TextBlocks` αντί αυτού.

### Αναμενόμενο Αποτέλεσμα

Ανοίξτε το `output.txt` και θα δείτε κάτι σαν:

```
Hello, world!
This is a sample scanned document.
```

Αυτό είναι το **output plain text** μέρος του οδηγού—γρήγορο, ελαφρύ και τέλειο για επεξεργασία downstream (π.χ., ευρετηρίαση).

## Βήμα 3: Εναλλαγή σε Λειτουργία Αναζητήσιμου PDF

Τώρα ας δημιουργήσουμε ένα **αναζητήσιμο PDF**. Η μηχανή θα ενσωματώσει το αρχικό bitmap και θα τοποθετήσει το κείμενο που δημιουργήθηκε από OCR κάτω από αυτό, καθιστώντας το έγγραφο αναζητήσιμο σε οποιονδήποτε προβολέα PDF.

```csharp
        // Change the output format to searchable PDF
        ocrEngine.OutputFormat = OutputFormat.SearchablePdf;

        // Recognize the same image again – this time we get PDF bytes
        OcrResult pdfResult = ocrEngine.Recognize(Image.Load(inputImagePath));

        // Save the PDF bytes to a file
        string pdfOutputPath = @"YOUR_DIRECTORY/output.pdf";
        File.WriteAllBytes(pdfOutputPath, pdfResult.RawData);
    }
}
```

**Γιατί επανααναγνωρίζουμε:** Η μηχανή OCR αποθηκεύει στην κρυφή μνήμη την τελευταία εικόνα, αλλά η μορφή εξόδου καθορίζει ποια δεδομένα επιστρέφει. Η αλλαγή της μορφής αναγκάζει μια νέα διεργασία που περιλαμβάνει το κρυφό στρώμα κειμένου.

### Πώς Φαίνεται το PDF

Ανοίξτε το `output.pdf` στο Adobe Reader ή σε οποιονδήποτε προβολέα και δοκιμάστε να επιλέξετε κείμενο. Θα δείτε ότι μπορείτε να αντιγράψετε, να αναζητήσετε και να επισημάνετε το περιεχόμενο—παρόλο που η οπτική εμφάνιση παραμένει το αρχικό bitmap. Αυτό είναι το χαρακτηριστικό ενός **convert scanned image pdf**.

## Βήμα 4: Επεξεργασία Πολλαπλών Αρχείων (Προαιρετικό)

Στην πραγματική ζωή τα έργα σπάνια ασχολούνται με μία μόνο εικόνα. Παρακάτω υπάρχει ένας γρήγορος βρόχος που επεξεργάζεται κάθε PNG σε έναν φάκελο, παράγοντας αντίστοιχα αρχεία `.txt` και `.pdf`.

```csharp
        string folder = @"YOUR_DIRECTORY";
        foreach (var file in Directory.GetFiles(folder, "*.png"))
        {
            // Plain‑text extraction
            ocrEngine.OutputFormat = OutputFormat.Text;
            var txtResult = ocrEngine.Recognize(Image.Load(file));
            File.WriteAllText(Path.ChangeExtension(file, ".txt"), txtResult.Text);

            // Searchable PDF generation
            ocrEngine.OutputFormat = OutputFormat.SearchablePdf;
            var pdfResult = ocrEngine.Recognize(Image.Load(file));
            File.WriteAllBytes(Path.ChangeExtension(file, ".pdf"), pdfResult.RawData);
        }
```

**Σημείωση για άκρες περιπτώσεις:** Μεγάλες εικόνες μπορούν να εξαντλήσουν τη μνήμη. Αν αντιμετωπίσετε `OutOfMemoryException`, σκεφτείτε να μειώσετε την ανάλυση με `Image.Resize` πριν την αναγνώριση, ή να επεξεργαστείτε τα αρχεία σε μικρότερες παρτίδες.

## Βήμα 5: Βελτιστοποίηση Ακρίβειας OCR

Το Aspose OCR προσφέρει μερικές ρυθμίσεις που μπορείτε να ενεργοποιήσετε:

| Setting | Τι κάνει | Πότε να το χρησιμοποιήσετε |
|---------|----------|----------------------------|
| `ocrEngine.PageSegmentationMode` | Ελέγχει πώς η μηχανή χωρίζει την εικόνα σε μπλοκ κειμένου. | Χρήσιμο για διατάξεις πολλαπλών στηλών. |
| `ocrEngine.Deskew` | Αυτόματη περιστροφή ελαφρώς κλινόμενων σελίδων. | Σαρωμένα έγγραφα που δεν είναι τέλεια ευθυγραμμισμένα. |
| `ocrEngine.RemoveNoise` | Προσπαθεί να καθαρίσει στίγματα και παρασιτικές ατέλειες του φόντου. | Χαμηλής ποιότητας σαρώσεις ή fax. |

Παράδειγμα:

```csharp
ocrEngine.Deskew = true;
ocrEngine.RemoveNoise = true;
```

Η ενεργοποίηση αυτών των επιλογών μπορεί να αυξήσει τον χρόνο επεξεργασίας, αλλά η βελτίωση στην **extract text from image** ποιότητα συχνά αξίζει τον κόπο.

## Βήμα 6: Επαλήθευση της Εξόδου Προγραμματιστικά

Μερικές φορές χρειάζεται να βεβαιωθείτε ότι το PDF περιέχει πράγματι αναζητήσιμο κείμενο (π.χ., σε αυτοματοποιημένες δοκιμές). Ο πιο απλός έλεγχος είναι να επαληθεύσετε ότι ο πίνακας byte του PDF δεν είναι κενός και ότι το μήκος του `RawData` υπερβαίνει το μέγεθος της εικόνας.

```csharp
if (pdfResult.RawData.Length > Image.Load(inputImagePath).Data.Length)
{
    Console.WriteLine("Searchable PDF generated successfully!");
}
else
{
    Console.WriteLine("Warning: PDF may not contain hidden text.");
}
```

Για πιο βαθιά επικύρωση μπορείτε να χρησιμοποιήσετε μια βιβλιοθήκη PDF (όπως iTextSharp) για να εξάγετε το ρεύμα κειμένου και να το συγκρίνετε με το `plainTextResult.Text`.

## Συνηθισμένα Πιθανά Προβλήματα & Πώς να τα Αποφύγετε

- **Απουσία Άδειας** – Χωρίς έγκυρη άδεια Aspose η βιβλιοθήκη λειτουργεί σε λειτουργία αξιολόγησης, προσθέτοντας υδατογράφημα στα PDF. Καταχωρίστε την άδειά σας νωρίς (`License license = new License(); license.SetLicense("Aspose.OCR.lic");`).  
- **Λάθος Διαδρομή** – Η σκληρή κωδικοποίηση απόλυτων διαδρομών λειτουργεί στον δικό σας υπολογιστή αλλά σπάει αλλού. Χρησιμοποιήστε `Path.Combine` με `AppDomain.CurrentDomain.BaseDirectory` για φορητότητα.  
- **Μη Υποστηριζόμενες Μορφές Εικόνας** – Τα GIF και TIFF με πολλαπλά πλαίσια απαιτούν ειδική διαχείριση (`Image.LoadMultiPage`). Μετατρέψτε τα σε PNG/JPEG πρώτα αν χρειάζεστε μόνο την πρώτη σελίδα.  
- **Σημεία Σπάσης Απόδοσης** – Η επαναδημιουργία `OcrEngine` μέσα σε βρόχο είναι δαπανηρή. Διατηρήστε μια μόνο παρουσία και αλλάξτε μόνο το `OutputFormat` όπως φαίνεται.

## Ανακεφαλαίωση

Καλύψαμε ολόκληρη τη ροή εργασίας για **δημιουργία αναζητήσιμου PDF** από μια σαρωμένη εικόνα χρησιμοποιώντας το Aspose OCR:

1. Εγκαταστήστε το πακέτο NuGet και δημιουργήστε ένα `OcrEngine`.  
2. Ορίστε `OutputFormat.Text` για **output plain text** και γράψτε το σε αρχείο `.txt`.  
3. Αλλάξτε σε `OutputFormat.SearchablePdf` για **convert image to PDF** με αόρατο στρώμα κειμένου.  
4. Αποθηκεύστε τα byte του PDF και, προαιρετικά, επεξεργαστείτε έναν φάκελο για επεξεργασία παρτίδας.  
5. Βελτιώστε την ακρίβεια με επιλογές deskew, αφαίρεση θορύβου και σεγμεντοποίηση σελίδας.  

Όλα αυτά χωράνε σε ένα σύντομο, αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε στο Visual Studio.

## Τι Να Δοκιμάσετε Στη Σύννεφη

- **Επεξεργασία παρτίδας** με διεπαφή χρήστη (WinForms ή WPF) ώστε οι χρήστες να σύρουν‑και‑αποθέτουν αρχεία.  
- **Ανίχνευση γλώσσας** – Το Aspose OCR μπορεί να ανιχνεύσει αυτόματα τη γλώσσα· δοκιμάστε `ocrEngine.Language = Language.AutoDetect`.  
- **Μετα-επεξεργασία** – Ενσωματώστε το εξαγόμενο κείμενο σε ευρετήριο αναζήτησης (ElasticSearch, Azure Cognitive Search) για άμεση ανάκτηση εγγράφων.  
- **Εναλλακτικές εξόδους** – Χρησιμοποιήστε `OutputFormat.Hocr` για αποτελέσματα OCR σε HTML, χρήσιμα για προεπισκοπήσεις στο web.

Μην διστάσετε να πειραματιστείτε με διαφορετικές αναλύσεις εικόνας, χρωματικούς τρόπους και ρυθμίσεις OCR. Όσο περισσότερο πειραματιστείτε, τόσο καλύτερη θα είναι η κατανόησή σας για τις ανταλλαγές μεταξύ ταχύτητας και ακρίβειας.

---

**Καλή προγραμματιστική!** Αν συναντήσετε δυσκολίες, αφήστε ένα σχόλιο παρακάτω ή ελέγξτε την τεκμηρίωση του Aspose OCR για πιο λεπτομερείς πληροφορίες. Το επόμενο σας έργο—είτε είναι τιμολόγηση, αρχειοθέτηση ή δημιουργία μιας αναζητήσιμης βάσης γνώσεων—γίνεται πολύ πιο εύκολο.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}