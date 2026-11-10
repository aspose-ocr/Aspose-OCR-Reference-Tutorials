---
category: general
date: 2026-05-21
description: Πώς να εκτελέσετε OCR σε C# χρησιμοποιώντας το Aspose OCR – μάθετε πώς
  να μετατρέπετε εικόνα σε κείμενο, να διαβάζετε κείμενο από jpg και να φορτώνετε
  εικόνα για OCR γρήγορα και αξιόπιστα.
draft: false
keywords:
- how to perform OCR
- convert image to text
- read text from jpg
- how to extract text from image
- load image for OCR
language: el
og_description: Πώς να εκτελέσετε OCR σε C# με το Aspose OCR. Αυτός ο οδηγός σας δείχνει
  πώς να μετατρέψετε εικόνα σε κείμενο, να διαβάσετε κείμενο από JPG και να φορτώσετε
  εικόνα για OCR βήμα‑βήμα.
og_title: Πώς να εκτελέσετε OCR σε C# – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: How to perform OCR in C# using Aspose OCR – learn to convert image
    to text, read text from jpg, and load image for OCR quickly and reliably.
  headline: How to Perform OCR in C# – Convert Image to Text with Aspose OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: Πώς να εκτελέσετε OCR σε C# – Μετατροπή εικόνας σε κείμενο με το Aspose OCR
url: /el/net/text-recognition/how-to-perform-ocr-in-c-convert-image-to-text-with-aspose-oc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εκτελέσετε OCR σε C# – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να εκτελέσετε OCR** σε μια εφαρμογή C# χωρίς να παλεύετε με επεξεργασία εικόνας χαμηλού επιπέδου; Δεν είστε μόνοι. Πολλοί προγραμματιστές χρειάζονται έναν αξιόπιστο τρόπο για **μετατροπή εικόνας σε κείμενο**, ειδικά όταν εργάζονται με σαρωμένα έγγραφα ή φωτογραφίες αποδείξεων. Σε αυτό το tutorial θα περάσουμε βήμα-βήμα τις ακριβείς ενέργειες για τη φόρτωση μιας εικόνας για OCR, την εκτέλεση της μηχανής αναγνώρισης και, τέλος, την ανάγνωση του εξαγόμενου κειμένου—όλα με το Aspose OCR.

Θα καλύψουμε επίσης πώς να **διαβάσετε κείμενο από jpg** αρχεία, θα συζητήσουμε τις λεπτομέρειες του **πώς να εξάγετε κείμενο από εικόνα** πηγές, και θα σας δώσουμε ένα γρήγορο cheat‑sheet για σενάρια **φόρτωσης εικόνας για OCR**. Στο τέλος, θα έχετε ένα έτοιμο δείγμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET.

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί τόσο σε .NET Core όσο και σε .NET Framework)
- Visual Studio 2022 ή οποιοδήποτε IDE προτιμάτε
- Ένα αρχείο άδειας Aspose OCR για .NET (προαιρετικό αλλά συνιστάται για πλήρη λειτουργία)
- Μια δείγμα εικόνας (π.χ., `sample.jpg`) τοποθετημένη σε γνωστό φάκελο
- Πρόσβαση στο Internet για λήψη του πακέτου NuGet `Aspose.OCR`

Αν κάποιο από αυτά σας φαίνεται άγνωστο, μην πανικοβληθείτε—κάθε απαίτηση θα αντιμετωπιστεί καθώς προχωράμε.

## Βήμα 1 – Εγκατάσταση Aspose OCR μέσω NuGet

Το πρώτο που χρειάζεστε είναι η βιβλιοθήκη Aspose OCR. Ανοίξτε το Package Manager Console και εκτελέστε:

```powershell
Install-Package Aspose.OCR
```

Ή, αν χρησιμοποιείτε τη γραμμή εντολών (CLI):

```bash
dotnet add package Aspose.OCR
```

> **Συμβουλή:** Η προσθήκη του πακέτου επαναφέρει όλες τις εξαρτήσεις, ώστε να μην χρειάζεται να ψάχνετε χειροκίνητα για επιπλέον DLLs.

## Βήμα 2 – Φόρτωση Εικόνας για OCR

Τώρα που η βιβλιοθήκη είναι στη θέση της, πρέπει να **φορτώσουμε εικόνα για OCR**. Αυτό το βήμα είναι κρίσιμο επειδή η μηχανή αναμένει ένα αντικείμενο `ImageStream`, όχι μια ακατέργαστη διαδρομή αρχείου.

```csharp
using Aspose.OCR;

// Assume the image lives in the same folder as the executable
string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "sample.jpg");

// Create an ImageStream from the file
ImageStream imgStream = ImageStream.FromFile(imagePath);
```

Παρατηρήστε πώς δημιουργούμε την πλήρη διαδρομή με `AppDomain.CurrentDomain.BaseDirectory`. Αυτό κάνει τον κώδικα ανθεκτικό, είτε τον εκτελείτε από το Visual Studio, μια κονσόλα ή ένα δημοσιευμένο exe. Επίσης, η κλάση `ImageStream` υποστηρίζει πολλές μορφές, ώστε να μπορείτε εύκολα να **διαβάσετε κείμενο από jpg**, **png**, ή **bmp** αρχεία.

## Βήμα 3 – Πώς να Εκτελέσετε OCR στην Φορτωμένη Εικόνα

Αυτή είναι η καρδιά του tutorial—**πώς να εκτελέσετε OCR** χρησιμοποιώντας τη μηχανή Aspose. Θα ορίσουμε επίσης τη γλώσσα στα Αγγλικά· μπορείτε να αντικαταστήσετε το `OcrLanguage.English` με άλλες υποστηριζόμενες γλώσσες αν χρειάζεται.

```csharp
// Step 3: Create an OCR engine and specify the language
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,
    Image = imgStream // assign the previously loaded image
};

// Optionally, apply your license to unlock the full feature set
var license = new License();
license.SetLicense(@"YOUR_DIRECTORY\Aspose.OCR.NET.lic");

// Run the recognition process
ocrEngine.Recognize();
```

Γιατί ορίζουμε την ιδιότητα `Image` πριν καλέσουμε το `Recognize()`; Η μηχανή χρειάζεται μια έγκυρη πηγή εικόνας· διαφορετικά, πετάει `NullReferenceException`. Αναθέτοντας το `ImageStream` που προετοιμάσαμε στο Βήμα 2, εξασφαλίζουμε ομαλή εκτέλεση.

## Βήμα 4 – Ανάκτηση και Εμφάνιση του Εξαγόμενου Κειμένου (Μετατροπή Εικόνας σε Κείμενο)

Αφού η μηχανή ολοκληρώσει, το αναγνωρισμένο κείμενο βρίσκεται στην ιδιότητα `Text`. Εδώ συμβαίνει η μαγεία της **μετατροπής εικόνας σε κείμενο**.

```csharp
// Step 4: Get the recognized text
string extractedText = ocrEngine.Text;

// Display it in the console
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(extractedText);
```

Η τυπική έξοδος μπορεί να μοιάζει με:

```
=== OCR Result ===
Invoice #12345
Date: 2026-04-30
Total: $1,250.00
Thank you for your business!
```

Αν η εικόνα είναι θολή ή περιέχει πολύπλοκες γραμματοσειρές, μπορεί να δείτε ακατάληπτους χαρακτήρες. Σε αυτήν την περίπτωση, σκεφτείτε να ρυθμίσετε την ιδιότητα `Resolution` της μηχανής ή να προεπεξεργαστείτε την εικόνα (π.χ., δυαδικοποίηση) πριν τη δώσετε στο OCR.

## Βήμα 5 – Προχωρημένο: Πώς να Εξάγετε Κείμενο από Εικόνα με Προσαρμοσμένες Ρυθμίσεις

Μερικές φορές οι προεπιλεγμένες ρυθμίσεις δεν αρκούν. Παρακάτω υπάρχουν μερικές προσαρμογές που βοηθούν όταν το **πώς να εξάγετε κείμενο από εικόνα** γίνεται ένα δύσκολο πρόβλημα.

```csharp
// Increase DPI for better accuracy on low‑resolution images
ocrEngine.Image = ImageStream.FromFile(imagePath);
ocrEngine.Image.DpiX = 300;
ocrEngine.Image.DpiY = 300;

// Enable auto‑rotate if the image might be skewed
ocrEngine.AutoRotate = true;

// Restrict recognition to a specific character set (e.g., digits only)
ocrEngine.RecognitionSettings.Characters = "0123456789.-";
```

Αυτές οι προσαρμογές μπορούν να βελτιώσουν δραματικά τα αποτελέσματα όταν δουλεύετε με αποδείξεις, φόρμες ή σαρωμένους πίνακες. Θυμηθείτε, το **πώς να εκτελέσετε OCR** δεν είναι μια λύση για όλα· συχνά χρειάζεται να πειραματιστείτε με τις ρυθμίσεις ανάλογα με το υλικό προέλευσης.

## Βήμα 6 – Συνηθισμένα Πιθανά Σφάλματα Κατά την Ανάγνωση Κειμένου από Αρχεία JPG

Ακόμη και με μια σταθερή βιβλιοθήκη, οι προγραμματιστές αντιμετωπίζουν εμπόδια. Εδώ είναι μερικά που μπορεί να συναντήσετε προσπαθώντας να **διαβάσετε κείμενο από jpg**:

| Πρόβλημα | Γιατί Συμβαίνει | Γρήγορη Διόρθωση |
|----------|----------------|-------------------|
| **Χαμηλή αντίθεση** | Η συμπίεση JPG μπορεί να ισοσταθμίσει τα χρώματα, καθιστώντας το κείμενο αδιάκριτο από το φόντο. | Προεπεξεργαστείτε την εικόνα με φίλτρα ενίσχυσης αντίθεσης (π.χ., `ImageSharp` ή `System.Drawing`). |
| **Λανθασμένος προσανατολισμός** | Τα τηλέφωνα μερικές φορές αποθηκεύουν μεταδεδομένα προσανατολισμού αντί να περιστρέφουν τα pixel. | Ορίστε `ocrEngine.AutoRotate = true` ή περιστρέψτε χειροκίνητα την εικόνα πριν το OCR. |
| **Μεγάλο μέγεθος αρχείου** | Τα πολύ υψηλής ανάλυσης JPG καταναλώνουν μνήμη και επιβραδύνουν την αναγνώριση. | Μειώστε την εικόνα σε λογικό DPI (π.χ., 300) πριν τη φόρτωση. |

Κρατώντας αυτά κατά νου θα σας εξοικονομήσει ώρες εντοπισμού σφαλμάτων όταν αργότερα **φορτώσετε εικόνα για OCR** στην παραγωγή.

## Βήμα 7 – Κωδικός Συμπερασμού: Παράδειγμα Μίας Μονοαρχείου

Παρακάτω είναι το πλήρες, εκτελέσιμο πρόγραμμα που ενώνει όλα τα παραπάνω. Αντιγράψτε‑επικολλήστε το σε ένα νέο έργο κονσόλας και πατήστε **F5**.

```csharp
using System;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣  Set up license (optional but recommended)
        // -------------------------------------------------
        var license = new License();
        // Replace with your actual license path or comment out for trial mode
        license.SetLicense(@"YOUR_DIRECTORY\Aspose.OCR.NET.lic");

        // -------------------------------------------------
        // 2️⃣  Load the image you want to process
        // -------------------------------------------------
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "sample.jpg");
        ImageStream imgStream = ImageStream.FromFile(imagePath);

        // -------------------------------------------------
        // 3️⃣  Create OCR engine – this is where we **perform OCR**
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            Image = imgStream,
            AutoRotate = true   // helpful for photos taken at odd angles
        };

        // -------------------------------------------------
        // 4️⃣  Run recognition
        // -------------------------------------------------
        ocrEngine.Recognize();

        // -------------------------------------------------
        // 5️⃣  Retrieve and display the result – **convert image to text**
        // -------------------------------------------------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrEngine.Text);
    }
}
```

**Αναμενόμενη έξοδος** (υποθέτοντας ότι το `sample.jpg` περιέχει σαφή αγγλικό κείμενο):

```
=== OCR Result ===
Hello, world!
This is a sample image for OCR testing.
```

Αν δείτε κενή έξοδο, ελέγξτε ξανά τη διαδρομή της εικόνας και βεβαιωθείτε ότι το αρχείο δεν είναι κατεστραμμένο.

## Συμπέρασμα

Τώρα γνωρίζετε **πώς να εκτελέσετε OCR** σε C# χρησιμοποιώντας το Aspose OCR, από την εγκατάσταση του πακέτου μέχρι το **φόρτωμα εικόνας για OCR**, την εκτέλεση της μηχανής, και τέλος τη **μετατροπή εικόνας σε κείμενο**. Ο οδηγός κάλυψε επίσης πρακτικές συμβουλές για **ανάγνωση κειμένου από jpg** αρχεία και απάντησε στην κοινή ερώτηση **πώς να εξάγετε κείμενο από εικόνα** όταν οι προεπιλεγμένες ρυθμίσεις δεν επαρκούν.

Τι έπεται; Δοκιμάστε να τροφοδοτήσετε τη μηχανή με PDF (μετατρέποντας πρώτα κάθε σελίδα σε εικόνα), πειραματιστείτε με πολυγλωσσική αναγνώριση, ή ενσωματώστε το βήμα OCR σε μια μεγαλύτερη αλυσίδα επεξεργασίας εγγράφων. Οι δυνατότητες είναι ατελείωτες, και με τη σταθερή βάση που μόλις χτίσατε, θα μπορείτε να αντιμετωπίσετε οποιαδήποτε πρόκληση εξαγωγής κειμένου.

Μη διστάσετε να αφήσετε ένα σχόλιο αν αντιμετωπίσετε πρόβλημα ή ανακαλύψετε ένα έξυπνο κόλπο—καλή προγραμματιστική!

![Παράδειγμα εκτέλεσης OCR](/images/ocr-example.png "Πώς να εκτελέσετε OCR σε C# – οπτική επισκόπηση")


## Σχετικά Μαθήματα

- [Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Μετατροπή Εικόνας σε Κείμενο – Εκτέλεση OCR σε Εικόνα από URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Πώς να κάνετε OCR σε Εικόνα – Εκτέλεση OCR σε Εικόνα στην Αναγνώριση Εικόνας OCR](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}