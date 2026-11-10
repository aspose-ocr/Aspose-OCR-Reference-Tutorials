---
category: general
date: 2026-03-05
description: Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας Aspose OCR σε C#. Μάθετε
  πώς να διαβάζετε αρχείο εικόνας σε C#, να μετατρέπετε DJVU σε κείμενο και να λαμβάνετε
  γρήγορα αποτελέσματα OCR εικόνας σε συμβολοσειρά.
draft: false
keywords:
- extract text from image
- read image file c#
- convert djvu to text
- ocr image to string
- recognize text from djvu
language: el
og_description: Εξαγωγή κειμένου από εικόνα με το Aspose OCR σε C#. Αυτός ο οδηγός
  δείχνει πώς να διαβάσετε ένα αρχείο εικόνας σε C#, να μετατρέψετε DJVU σε κείμενο
  και να χειριστείτε OCR εικόνας σε συμβολοσειρά με ευκολία.
og_title: Εξαγωγή κειμένου από εικόνα σε C# – Πλήρης Οδηγός Aspose OCR
tags:
- Aspose OCR
- C#
- Image Processing
title: Εξαγωγή κειμένου από εικόνα σε C# – Aspose OCR βήμα‑βήμα
url: /el/net/text-recognition/extract-text-from-image-in-c-aspose-ocr-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# εξαγωγή κειμένου από εικόνα σε C# – Πλήρης Οδηγός Aspose OCR

Έχετε ποτέ χρειαστεί να **εξάγετε κείμενο από εικόνα** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη θα σας δώσει αξιόπιστα αποτελέσματα; Ίσως έχετε μια σειρά από σάρωση DJVU και θέλετε απλώς το ακατέργαστο κείμενο χωρίς να παίζετε με εργαλεία τρίτων. Σε αυτό το tutorial θα λύσουμε το πρόβλημα σε λίγα λεπτά χρησιμοποιώντας το Aspose OCR για .NET.

Θα περάσουμε από την ανάγνωση ενός αρχείου εικόνας σε C#, τη μετατροπή ενός εγγράφου DJVU σε κείμενο, και τη μετατροπή οποιασδήποτε εικόνας OCR σε καθαρό string. Στο τέλος θα έχετε μια έτοιμη για εκτέλεση εφαρμογή κονσόλας που εκτυπώνει το αναγνωρισμένο κείμενο στην κονσόλα. Χωρίς ασαφείς συνδέσμους “δείτε την τεκμηρίωση” — μόνο μια πλήρη λύση copy‑paste.

## Τι Θα Χρειαστείτε

- **.NET 6.0** ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.6+).  
- **Aspose.OCR for .NET** πακέτο NuGet (η δωρεάν δοκιμαστική άδεια λειτουργεί για δοκιμές).  
- Ένα αρχείο DJVU ή οποιαδήποτε υποστηριζόμενη εικόνα (PNG, JPEG, BMP κ.λπ.).  
- Visual Studio, Rider ή ο αγαπημένος σας επεξεργαστής.

Αν λείπει κάποιο από αυτά, απλώς εγκαταστήστε το πακέτο NuGet:

```bash
dotnet add package Aspose.OCR
```

Αυτό είναι όλο το setup. Ας βουτήξουμε.

## Βήμα 1: Αρχικοποίηση του OCR Engine – εξαγωγή κειμένου από εικόνα

Το πρώτο που κάνετε είναι να δημιουργήσετε μια παρουσία του `OcrEngine`. Σκεφτείτε το ως τον εγκέφαλο που θα διαβάσει τα pixel και θα τα μετατρέψει σε χαρακτήρες.

```csharp
using Aspose.OCR;
using System;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine
        var ocrEngine = new OcrEngine();
```

Γιατί δημιουργούμε το engine *πριν* φορτώσουμε το αρχείο; Ο σχεδιασμός του Aspose διαχωρίζει τη διαμόρφωση (όπως η άδεια) από τα πραγματικά δεδομένα εικόνας, ώστε να μπορείτε να επαναχρησιμοποιήσετε το ίδιο engine για πολλά αρχεία χωρίς να δημιουργείτε ξανά αντικείμενα — ένα μικρό πλεονέκτημα απόδοσης.

## Βήμα 2: Εφαρμόστε την Άδεια Aspose OCR (προαιρετικό αλλά συνιστάται)

Αν έχετε εμπορική άδεια, ορίστε την τώρα. Παραλείποντας αυτό το βήμα ενεργοποιείται η λειτουργία demo, η οποία προσθέτει υδατογράφημα στην έξοδο και περιορίζει τον αριθμό των σελίδων.

```csharp
        // Apply license – remove this line if you’re using the free trial
        ocrEngine.SetLicense("Aspose.OCR.lic");
```

**Συμβουλή:** Κρατήστε το αρχείο άδειας εκτός του source control (π.χ., σε μεταβλητή περιβάλλοντος) για να αποφύγετε τυχαίες υποβολές.

## Βήμα 3: Φόρτωση της Εικόνας – ανάγνωση αρχείου εικόνας c# εύκολη

Το Aspose μπορεί να διαβάσει πολλές μορφές, συμπεριλαμβανομένου του σπάνιου DJVU. Θα χρησιμοποιήσουμε τη βοηθητική μέθοδο `ImageStream.FromFile` για να φορτώσουμε το αρχείο στο engine.

```csharp
        // Load the image (DJVU, PNG, JPEG, etc.)
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/input.djvu");
```

Αν προτιμάτε να δουλεύετε με ένα `byte[]` (π.χ., όταν η εικόνα προέρχεται από βάση δεδομένων), μπορείτε να χρησιμοποιήσετε το `ImageStream.FromBytes(byteArray)` αντί αυτού. Αυτή η ευελιξία είναι χρήσιμη όταν χρειάζεται να **διαβάσετε αρχείο εικόνας C#** από ροή αντί για δίσκο.

## Βήμα 4: Εκτέλεση OCR – εικόνα OCR σε string με μία κλήση

Τώρα συμβαίνει η μαγεία. Η κλήση `Recognize()` εκτελεί το OCR engine και επιστρέφει ένα `RecognitionResult` που περιέχει το εξαγόμενο κείμενο, τις βαθμολογίες εμπιστοσύνης και άλλα.

```csharp
        // Run OCR and get the result
        var result = ocrEngine.Recognize();

        // Extract plain text
        string recognizedText = result.Text;
```

Γιατί να μην καλέσετε απλώς `Recognize().Text`; Ο χωρισμός της κλήσης σας επιτρέπει να εξετάσετε το `result.Confidence` ή το `result.Regions` αν χρειάζεστε πιο λεπτομερή δεδομένα αργότερα — χρήσιμο για εντοπισμό σφαλμάτων ή για δημιουργία UI που επισημαίνει λέξεις χαμηλής εμπιστοσύνης.

## Βήμα 5: Εμφάνιση του Εξαγόμενου Κειμένου – η τελική έξοδός σας

Τέλος, γράψτε το κείμενο στην κονσόλα. Σε μια πραγματική εφαρμογή μπορεί να γράψετε σε αρχείο, βάση δεδομένων ή να το στείλετε μέσω API.

```csharp
        // Show the result
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(recognizedText);
    }
}
```

**Αναμενόμενη έξοδος** (συνοπτικά):

```
=== OCR Output ===
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Αν το OCR engine δεν μπορεί να αναγνωρίσει κανέναν χαρακτήρα, το `recognizedText` θα είναι κενό string. Σε αυτήν την περίπτωση, ελέγξτε ξανά την ποιότητα της εικόνας ή δοκιμάστε να ρυθμίσετε τις ρυθμίσεις γλώσσας του engine (π.χ., `ocrEngine.Language = Language.English;`).

## Μετατροπή DJVU σε Κείμενο – αναγνώριση κειμένου από djvu μαζικά

Μπορεί να έχετε δεκάδες αρχεία DJVU για επεξεργασία. Τυλίξτε τη λογική που ακολουθήσαμε σε έναν βρόχο:

```csharp
string[] files = Directory.GetFiles("YOUR_DIRECTORY", "*.djvu");
foreach (var file in files)
{
    ocrEngine.Image = ImageStream.FromFile(file);
    string text = ocrEngine.Recognize().Text;
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), text);
    Console.WriteLine($"Converted {Path.GetFileName(file)} → {Path.GetFileNameWithoutExtension(file)}.txt");
}
```

Αυτό το απόσπασμα **μετατρέπει DJVU σε κείμενο** αυτόματα, δημιουργώντας ένα αρχείο `.txt` δίπλα σε κάθε πηγή. Είναι ένας γρήγορος τρόπος να δημιουργήσετε ένα αναζητήσιμο αρχείο από παλιά σαρωμένα έγγραφα.

## Διαχείριση Ακραίων Περιπτώσεων – τι γίνεται αν η εικόνα είναι θορυβώδης;

Η ακρίβεια του OCR μειώνεται όταν η εικόνα είναι θολή, έχει χαμηλή αντίθεση ή περιέχει χρωματικό φόντο. Το Aspose OCR προσφέρει επιλογές προεπεξεργασίας:

```csharp
// Example: Binarize the image to improve contrast
ocrEngine.Image = ImageProcessing.Binarize(ocrEngine.Image, threshold: 128);
```

Εναλλακτικά, μπορείτε να ορίσετε το engine να ανιχνεύει τη γλώσσα αυτόματα:

```csharp
ocrEngine.Language = Language.Detect; // Detects language based on content
```

Αυτές οι ρυθμίσεις συχνά μετατρέπουν ένα αποτέλεσμα 60 % ακρίβειας σε 95 %. Πειραματιστείτε με τις μεθόδους `Threshold`, `Denoise` ή `Deskew` αν αντιμετωπίσετε προβλήματα.

## Πλήρες Παράδειγμα Εργασίας – αντιγράψτε, επικολλήστε, εκτελέστε

Παρακάτω είναι ολόκληρο το πρόγραμμα, έτοιμο για μεταγλώττιση. Αντικαταστήστε το `"YOUR_DIRECTORY/input.djvu"` με τη διαδρομή του αρχείου σας και βεβαιωθείτε ότι το αρχείο άδειας είναι προσβάσιμο.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Apply license (optional)
        // ocrEngine.SetLicense("Aspose.OCR.lic"); // Uncomment if you have a license

        // 3️⃣ Load the image (DJVU, PNG, JPEG, etc.)
        string imagePath = "YOUR_DIRECTORY/input.djvu";
        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // 4️⃣ Perform OCR
        var result = ocrEngine.Recognize();
        string recognizedText = result.Text;

        // 5️⃣ Output the text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(recognizedText);
    }
}
```

Τρέξτε το με:

```bash
dotnet run
```

Θα πρέπει να δείτε το εξαγόμενο κείμενο να εκτυπώνεται στην κονσόλα, ακριβώς όπως φαίνεται στο προηγούμενο παράδειγμα.

## Συχνές Ερωτήσεις & Πιθανά Προβλήματα

- **Λειτουργεί αυτό με αρχεία PDF;**  
  Όχι άμεσα. Το Aspose OCR χειρίζεται raster εικόνες· για PDFs θα πρέπει πρώτα να μετατρέψετε κάθε σελίδα σε εικόνα (π.χ., χρησιμοποιώντας Aspose.PDF) και στη συνέχεια να τροφοδοτήσετε αυτές τις εικόνες στο OCR engine.

- **Τι γίνεται αν χρειαστεί να επεξεργαστώ μεγάλη παρτίδα σε διακομιστή;**  
  Δημιουργήστε ένα **μοναδικό** `OcrEngine` και επαναχρησιμοποιήστε το μεταξύ νημάτων. Το engine είναι thread‑safe για λειτουργίες μόνο ανάγνωσης, αλλά πρέπει να αποφεύγετε την ταυτόχρονη κοινή χρήση της ίδιας `Image` παρουσίασης.

- **Μπορώ να εξάγω μορφοποιημένο κείμενο (γραμματοσειρές, μεγέθη);**  
  Το Aspose OCR επιστρέφει μόνο απλό Unicode κείμενο. Για εξαγωγή που διατηρεί τη διάταξη θα χρειαστείτε μια πιο προχωρημένη λύση όπως OCR με OCR‑ML ή μια βιβλιοθήκη PDF που διατηρεί τη διάταξη.

## Επόμενα Βήματα – επεκτείνετε τη ροή εργασίας σας

Τώρα που μπορείτε να **εξάγετε κείμενο από εικόνα** αξιόπιστα, σκεφτείτε:

- Αποθήκευση των αποτελεσμάτων στο Elasticsearch για αναζήτηση πλήρους κειμένου.  
- Τροφοδοσία του κειμένου σε μοντέλο γλώσσας για περίληψη.  
- Προσθήκη απλού UI με ASP.NET Core για ανέβασμα αρχείων και άμεση προβολή των αποτελεσμάτων OCR.

Όλα αυτά βασίζονται στον ίδιο βασικό κώδικα που καλύψαμε, έτσι είστε καλά προετοιμασμένοι να επεκτείνετε τη λύση.

### Σύντομη Ανακεφαλαίωση

- Αρχικοποιήσαμε το `OcrEngine` (η καρδιά του Aspose OCR).  
- Εφαρμόσαμε μια **άδεια** για να ξεκλειδώσουμε όλες τις δυνατότητες.  
- **Φορτώσαμε** ένα αρχείο DJVU χρησιμοποιώντας `ImageStream.FromFile`.  
- Καλύσαμε το `Recognize()` για να πάρουμε ένα αποτέλεσμα **ocr image to string**.  
- Εκτυπώσαμε το **εξαγόμενο κείμενο** στην κονσόλα.  

Αυτή είναι η πλήρης συνταγή για τη μετατροπή οποιασδήποτε υποστηριζόμενης εικόνας — συμπεριλαμβαμένου του DJVU — σε αναζητήσιμο κείμενο με C#.

Μη διστάσετε να πειραματιστείτε με διαφορετικές μορφές εικόνας, να ρυθμίσετε τις ρυθμίσεις προεπεξεργασίας ή να συνδυάσετε αυτόν τον κώδικα με άλλες βιβλιοθήκες Aspose. Αν αντιμετωπίσετε πρόβλημα, αφήστε ένα σχόλιο παρακάτω — καλή προγραμματιστική!

![παράδειγμα εξαγωγής κειμένου από εικόνα](/images/ocr-example.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}