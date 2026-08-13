---
category: general
date: 2026-03-05
description: πώς να χρησιμοποιήσετε OCR σε C# για την εξαγωγή κειμένου από εικόνες
  αποδείξεων. Μάθετε πώς να φορτώνετε εικόνα για OCR και να αναγνωρίζετε την εικόνα
  της απόδειξης σε λίγα λεπτά.
draft: false
keywords:
- how to use OCR
- extract text from receipt
- load image for OCR
- recognize receipt image
language: el
og_description: πώς να χρησιμοποιήσετε OCR σε C# για την εξαγωγή κειμένου από αποδείξεις.
  Ακολουθήστε αυτόν τον βήμα‑βήμα οδηγό για να φορτώσετε μια εικόνα για OCR και να
  αναγνωρίσετε την εικόνα της απόδειξης αποδοτικά.
og_title: πώς να χρησιμοποιήσετε OCR σε C# – Γρήγορη εξαγωγή κειμένου από απόδειξη
tags:
- OCR
- C#
- Aspose
- Receipt Processing
title: Πώς να χρησιμοποιήσετε OCR σε C# – Εξαγωγή κειμένου από αποδείξεις γρήγορα
url: /el/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-receipts-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# πώς να χρησιμοποιήσετε OCR σε C# – Εξαγωγή κειμένου από αποδείξεις γρήγορα

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε OCR** για να εξάγετε δεδομένα κατευθείαν από μια φωτογραφία απόδειξης αγορών; Δεν είστε μόνοι. Σε πολλές εφαρμογές μικρών επιχειρήσεων, το στενό λαιμό είναι η μετατροπή ενός θολού PNG σε δομημένο κείμενο με το οποίο μπορείτε πραγματικά να εργαστείτε.  

Τα καλά νέα; Με λίγες γραμμές C# και Aspose.OCR μπορείτε να **φορτώσετε εικόνα για OCR**, να εκτελέσετε τη μηχανή και να **αναγνωρίσετε εικόνα απόδειξης** σε λιγότερο από ένα λεπτό. Παρακάτω θα δείτε ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα, μαζί με συμβουλές για τα δύσκολα σημεία που παραλείπουν τα περισσότερα tutorials.

## Τι καλύπτει αυτός ο οδηγός

Θα περάσουμε από όλα όσα χρειάζεστε:

* Εγκατάσταση του πακέτου NuGet Aspose.OCR.  
* Ρύθμιση του OCR engine – η καρδιά του **πώς να χρησιμοποιήσετε OCR** σωστά.  
* Φόρτωση αρχείου απόδειξης (αυτό είναι το βήμα **φορτώστε εικόνα για OCR**).  
* Εκτέλεση της διαδικασίας αναγνώρισης και εξαγωγή τόσο των δεδομένων διάταξης JSON όσο και XML.  
* Διαχείριση κοινών παγίδων όπως ελλιπείς άδειες ή μη υποστηριζόμενες μορφές εικόνας.  

Στο τέλος θα έχετε ένα αυτόνομο πρόγραμμα που εξάγει το κείμενο από οποιαδήποτε απόδειξη ρίχνετε σε έναν φάκελο. Χωρίς εξωτερικές υπηρεσίες, χωρίς κρυφή μαγεία.

## Προαπαιτούμενα

* .NET 6 SDK ή νεότερο (ο κώδικας μεταγλωττίζεται και με .NET Core).  
* Ένα έγκυρο αρχείο άδειας Aspose.OCR (`Aspose.OCR.lic`). Μπορείτε να πάρετε δωρεάν δοκιμαστική έκδοση από την Aspose αν δεν έχετε ακόμη.  
* Ένα δείγμα εικόνας απόδειξης – το `receipt.png` λειτουργεί καλά, αλλά οποιαδήποτε κοινή μορφή raster θα κάνει.  

Αν έχετε ήδη όλα αυτά, τέλεια – ας βουτήξουμε.

![παράδειγμα χρήσης OCR](https://example.com/ocr-receipt.png "παράδειγμα χρήσης OCR")

## Βήμα 1: Εγκατάσταση Aspose.OCR και δημιουργία νέου έργου

Πρώτο πράγμα πρώτα: χρειάζεστε τη βιβλιοθήκη που πραγματικά κάνει το βαριά δουλειά. Ανοίξτε ένα τερματικό στο φάκελο του έργου σας και τρέξτε:

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

Αυτή η εντολή δημιουργεί μια εφαρμογή κονσόλας και προσθέτει το πιο πρόσφατο πακέτο Aspose.OCR. Από την εμπειρία μου, η διατήρηση του ονόματος του έργου σύντομης διευκολύνει την ανάγνωση των παραγόμενων διαδρομών, ειδικά όταν αρχίζετε να διαχειρίζεστε πολλαπλές demo εφαρμογές.

## Βήμα 2: Αρχικοποίηση του OCR Engine – η καρδιά του **πώς να χρησιμοποιήσετε OCR**

Τώρα θα γράψουμε τον κώδικα που απαντά στην ερώτηση “**πώς να χρησιμοποιήσετε OCR** σε C#”. Ανοίξτε το `Program.cs` και αντικαταστήστε το περιεχόμενό του με το παρακάτω απόσπασμα. Παρατηρήστε τα σχόλια – εξηγούν το *γιατί* πίσω από κάθε γραμμή, όχι μόνο το *τι*.

```csharp
using System;
using System.IO;
using Aspose.OCR;          // Aspose OCR namespace
using Aspose.OCR.Image;   // For loading images

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Create and configure the OCR engine.
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // Why set a license? Without it the engine runs in evaluation mode,
        // which adds a watermark to the output and limits batch size.
        ocrEngine.SetLicense("Aspose.OCR.lic");

        // -------------------------------------------------
        // 2️⃣ Load the receipt image – this is the **load image for OCR** step.
        // -------------------------------------------------
        // Change the path to point at your own receipt file.
        string imagePath = Path.Combine(
            Environment.CurrentDirectory, "receipt.png");

        // The ImageStream class abstracts file I/O and supports many formats.
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // -------------------------------------------------
        // 3️⃣ Run the recognition process – this is where we **recognize receipt image**.
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize();

        // -------------------------------------------------
        // 4️⃣ Export the layout information as JSON.
        // -------------------------------------------------
        string jsonResult = ocrResult.ToJson();
        File.WriteAllText("receipt.json", jsonResult);
        Console.WriteLine("✅ JSON saved to receipt.json");

        // -------------------------------------------------
        // 5️⃣ Export the same layout information as XML.
        // -------------------------------------------------
        string xmlResult = ocrResult.ToXml();
        File.WriteAllText("receipt.xml", xmlResult);
        Console.WriteLine("✅ XML saved to receipt.xml");

        // -------------------------------------------------
        // 6️⃣ Quick preview – print the plain text to console.
        // -------------------------------------------------
        Console.WriteLine("\n--- Extracted Text ---");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Γιατί λειτουργεί αυτό

* **`OcrEngine`** είναι το σημείο εισόδου· διατηρεί όλες τις ρυθμίσεις που μπορεί να τροποποιήσετε αργότερα (γλώσσα, DPI κ.λπ.).  
* **`SetLicense`** αφαιρεί το υδατογράφημα αξιολόγησης – ένα κρίσιμο βήμα όταν σκοπεύετε να διανείμετε τον κώδικα.  
* **`ImageStream.FromFile`** εκτελεί το **φορτώστε εικόνα για OCR**, διαχειριζόμενο PNG, JPEG, BMP, TIFF και άλλα.  
* **`Recognize()`** είναι η μέθοδος που πραγματικά **αναγνωρίζει εικόνα απόδειξης**. Στο παρασκήνιο εκτελεί δυαδικοποίηση, τμηματοποίηση και ταξινόμηση χαρακτήρων.  
* Η εξαγωγή σε JSON και XML σας δίνει τόσο ένα ανθρώπινα αναγνώσιμο dump όσο και μια δομή φιλική προς μηχανές που μπορείτε να τροφοδοτήσετε σε downstream parsers.

## Βήμα 3: Εκτέλεση της επίδειξης και επαλήθευση του αποτελέσματος

Μεταγλώττιση και εκτέλεση:

```bash
dotnet run
```

Αν όλα είναι συνδεδεμένα σωστά, θα δείτε κάτι σαν:

```
✅ JSON saved to receipt.json
✅ XML saved to receipt.xml

--- Extracted Text ---
Walmart Supercenter
Date: 03/04/2026
Item    Qty   Price
Milk    2     2.58
Bread   1     1.99
Total   4.57
```

Η κονσόλα εκτυπώνει το απλό κείμενο, ενώ τα `receipt.json` και `receipt.xml` περιέχουν λεπτομερείς πληροφορίες διάταξης (συντεταγμένες, βαθμοί εμπιστοσύνης κ.λπ.). Αυτά τα αρχεία είναι χρήσιμα αν χρειαστεί να αντιστοιχίσετε κάθε γραμμή σε πεδίο βάσης δεδομένων αργότερα.

## Περιπτώσεις Άκρων & Επαγγελματικές Συμβουλές

### 1️⃣ Έλλειψη ή Μη Έγκυρη Άδεια

Αν το `SetLicense` αποτύχει, η μηχανή επιστρέφει σε λειτουργία δοκιμής και θα εμφανιστεί υδατογράφημα στην έξοδο. Τυλίξτε την κλήση σε try/catch και καταγράψτε ένα φιλικό μήνυμα:

```csharp
try { ocrEngine.SetLicense("Aspose.OCR.lic"); }
catch (Exception ex)
{
    Console.WriteLine("⚠️ License not found – running in trial mode.");
    Console.WriteLine(ex.Message);
}
```

### 2️⃣ Μη υποστηριζόμενες μορφές εικόνας

Το Aspose.OCR υποστηρίζει τις περισσότερες μορφές raster, αλλά αν του δώσετε PDF ή multi‑page TIFF θα πρέπει πρώτα να μετατρέψετε τη σελίδα που σας ενδιαφέρει σε εικόνα. Η βιβλιοθήκη `Aspose.PDF` μπορεί να διαχειριστεί αυτή τη μετατροπή.

### 3️⃣ Μεγάλες αποδείξεις & Απόδοση

Η επεξεργασία μιας εικόνας 10 MB μπορεί να είναι αργή. Μειώστε την ανάλυση πριν τη δώσετε στη μηχανή:

```csharp
ocrEngine.Image = ImageStream.FromFile(imagePath).Resize(1024, 0);
```

Η μέθοδος `Resize` διατηρεί την αναλογία διαστάσεων (`0` για το ύψος) και μειώνει δραστικά το μέγεθος του αρχείου χωρίς να θυσιάζει την ακρίβεια OCR για τυπικές αποδείξεις.

### 4️⃣ Προβλήματα γλώσσας & γραμματοσειράς

Οι αποδείξεις μπορεί να περιέχουν ειδικούς χαρακτήρες (€, ¥, κ.λπ.). Ορίστε τη γλώσσα ρητά αν γνωρίζετε την τοπική ρύθμιση:

```csharp
ocrEngine.Language = Language.English; // or Language.Spanish, etc.
```

Για αποδείξεις με ανάμειξη γλωσσών, μπορείτε να ενεργοποιήσετε τη πολυγλωσσική λειτουργία:

```csharp
ocrEngine.Language = Language.English | Language.French;
```

### 5️⃣ Εξαγωγή δομημένων δεδομένων

Το ακατέργαστο κείμενο είναι χρήσιμο, αλλά οι περισσότερες εφαρμογές χρειάζονται δομημένα πεδία (ημερομηνία, σύνολο, είδη). Η διάταξη JSON περιλαμβάνει συντεταγμένες `BoundingBox` για κάθε λέξη. Μπορείτε να το επεξεργαστείτε ως εξής:

```csharp
var layout = Newtonsoft.Json.Linq.JObject.Parse(jsonResult);
foreach (var word in layout["Words"])
{
    string text = (string)word["Text"];
    // Simple heuristics: look for "$" or "Total"
}
```

Αυτό το απόσπασμα δείχνει την ιδέα· σε παραγωγή πιθανότατα θα χρησιμοποιούσατε κανονική έκφραση ή έναν μικρό μηχανισμό κανόνων.

## Συχνές Ερωτήσεις

**Q: Μπορώ να το τρέξω σε Linux;**  
A: Απόλυτα. Το Aspose.OCR είναι cross‑platform· απλώς εγκαταστήστε το .NET runtime στο Linux box σας και ο ίδιος κώδικας λειτουργεί.

**Q: Τι γίνεται αν χρειαστεί να επεξεργαστώ δεκάδες αποδείξεις ανά λεπτό;**  
A: Εκκινήστε έναν βρόχο `Parallel.ForEach` και επαναχρησιμοποιήστε ένα μόνο αντικείμενο `OcrEngine` – είναι thread‑safe για λειτουργίες μόνο ανάγνωσης. Θυμηθείτε να διαχειριστείτε τα όρια ταυτόχρονης χρήσης της άδειας.

**Q: Λειτουργεί αυτό με φωτογραφίες κινητού που έχουν ληφθεί υπό γωνία;**  
A: Η μηχανή περιλαμβάνει βασική διόρθωση κλίσης, αλλά για πολύ κεκλιμένες εικόνες ίσως χρειαστεί προεπεξεργασία με βιβλιοθήκη επεξεργασίας εικόνας (π.χ., OpenCV) για να ευθυγραμμίσετε την απόδειξη πρώτα.

## Πλήρες Παράδειγμα Λειτουργίας (Αντιγραφή‑Επικόλληση)

Παρακάτω είναι το *ολόκληρο* πρόγραμμα που μπορείτε να τοποθετήσετε στο `Program.cs`. Δεν απαιτούνται άλλα αρχεία εκτός από την άδεια και μια εικόνα απόδειξης.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Create and configure the OCR engine
        var ocrEngine = new OcrEngine();
        try
        {
            ocrEngine.SetLicense("Aspose.OCR.lic");
        }
        catch (Exception)
        {
            Console.WriteLine("⚠️ Running in trial mode – license not found.");
        }

        // Load the image to be processed (load image for OCR)
        string imagePath = Path.Combine(Environment.CurrentDirectory, "

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}