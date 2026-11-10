---
category: general
date: 2026-05-02
description: Αναγνωρίστε εικόνα κειμένου χρησιμοποιώντας το Aspose OCR C#. Μάθετε
  πώς να προεπεξεργαστείτε την εικόνα για OCR, να βελτιώσετε την ακρίβεια και να εξάγετε
  καθαρό κείμενο σε λίγα μόνο βήματα.
draft: false
keywords:
- recognize text image
- aspose ocr c#
- preprocess image ocr
- ocr preprocessing
- deskew denoise binarization
language: el
og_description: Αναγνωρίστε γρήγορα εικόνες κειμένου με το Aspose OCR C#. Αυτός ο
  οδηγός δείχνει πώς να προεπεξεργαστείτε την εικόνα για OCR ώστε να πετύχετε βέλτιστα
  αποτελέσματα.
og_title: Αναγνώριση εικόνας κειμένου με Aspose OCR C# – Πλήρης οδηγός προεπεξεργασίας
tags:
- OCR
- C#
- Image Processing
title: Αναγνώριση εικόνας κειμένου με Aspose OCR C# – Πλήρης Οδηγός Προεπεξεργασίας
url: /el/net/ocr-optimization/recognize-text-image-with-aspose-ocr-c-complete-preprocess-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση εικόνας κειμένου με Aspose OCR C# – Πλήρης Οδηγός Προεπεξεργασίας

Έχετε ποτέ χρειαστεί να **αναγνωρίσετε εικόνα κειμένου**, αλλά τα αποτελέσματα έμοιαζαν περισσότερο με ακαταλαβίστικο κείμενο παρά με αναγνώσιμες προτάσεις; Δεν είστε μόνοι—θορυβώδεις σάρωση, λοξά αποδείξεις ή εικόνες χαμηλής αντίθεσης μπορούν να μετατρέψουν το OCR σε παιχνίδι μαντεψιάς. Τα καλά νέα; Με το Aspose OCR C# μπορείτε να καθαρίσετε αυτές τις προβληματικές εικόνες πριν ακόμη το μηχανισμό τις επεξεργαστεί, και το αποτέλεσμα γίνεται δραματικά πιο καθαρό.

Σε αυτό το σεμινάριο θα περάσουμε βήμα‑βήμα μια **step‑by‑step** λύση που όχι μόνο δείχνει πώς να αναγνωρίσετε εικόνα κειμένου, αλλά και πώς να *προεπεξεργαστείτε εικόνα OCR* χρησιμοποιώντας ευθυγράμμιση (deskew), αποθορυβοποίηση (denoise) και δυαδικοποίηση (binarization). Στο τέλος θα έχετε ένα έτοιμο προς εκτέλεση πρόγραμμα C#, μια σαφή κατανόηση του γιατί κάθε επιλογή προεπεξεργασίας είναι σημαντική, και μια σειρά από συμβουλές που μπορείτε να εφαρμόσετε σε οποιοδήποτε έργο OCR.

## Τι Θα Χρειαστείτε

- **.NET 6** ή νεότερο (ο κώδικας λειτουργεί τόσο με .NET Core όσο και με .NET Framework).  
- **Aspose.OCR for .NET** πακέτο NuGet (`Install-Package Aspose.OCR`)  
- Ένα δείγμα εικόνας που είναι λοξοτομημένο, θορυβώδες ή χαμηλής αντίθεσης (π.χ., `skewed_noisy.jpg`)  
- Visual Studio 2022 ή οποιοδήποτε IDE C# προτιμάτε  

Καμία επιπλέον εγγενής βιβλιοθήκη, καμία εξωτερική υπηρεσία—μόνο καθαρός διαχειριζόμενος κώδικας.

---

## Βήμα 1: Εγκατάσταση Aspose OCR C# και Προσθήκη Namespaces

Πρώτα απ' όλα. Κατεβάστε τη βιβλιοθήκη Aspose OCR από το NuGet και προσθέστε τα απαιτούμενα namespaces. Αυτό διασφαλίζει ότι ο μεταγλωττιστής γνωρίζει πού βρίσκονται οι κλάσεις `OcrEngine`, `PreprocessOptions` και οι συναφείς.

```csharp
// Install via NuGet Package Manager Console:
// PM> Install-Package Aspose.OCR

using Aspose.OCR;
using Aspose.OCR.Settings;
```

> **Pro tip:** Αν χρησιμοποιείτε το .NET CLI, εκτελέστε `dotnet add package Aspose.OCR` αντί αυτού. Η διατήρηση των πακέτων σας ενημερωμένων (προς το παρόν 23.8) σας βοηθά να επωφεληθείτε από τους πιο πρόσφατους αλγόριθμους προεπεξεργασίας.

---

## Βήμα 2: Δημιουργία του OCR Engine και Ενεργοποίηση Προεπεξεργασίας

Η καρδιά της λύσης είναι το `OcrEngine`. Από προεπιλογή προσπαθεί να διαβάσει το ακατέργαστο bitmap, κάτι που συχνά οδηγεί σε χαμένα χαρακτήρες σε θορυβώδη σάρωση. Επομένως ενεργοποιούμε τρεις σημαίες προεπεξεργασίας:

- **Deskew** – ευθυγραμμίζει τις περιστρεφόμενες γραμμές κειμένου.  
- **Denoise** – εξομαλύνει τα στίγματα και τα τεχνουργήματα συμπίεσης.  
- **Binarization** – μετατρέπει την εικόνα σε ασπρόμαυρη, ενισχύοντας την αντίθεση.  

```csharp
// Step 2: Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Configure preprocessing options
ocrEngine.Settings.PreprocessOptions = new PreprocessOptions
{
    EnableDeskew = true,          // Auto‑detect and correct rotation
    EnableDenoise = true,         // Reduce random noise
    EnableBinarization = true,    // Force black‑white conversion
    BinarizationThreshold = 120   // Tune based on your image brightness
};
```

**Γιατί αυτές οι επιλογές;**  
Το Deskew διορθώνει το πρόβλημα γωνίας που κάνει τους χαρακτήρες να φαίνονται κεκλιμένοι, κάτι με το οποίο οι περισσότερες αλγόριθμικές OCR δυσκολεύονται. Το Denoise αφαιρεί τυχαία pixels που θα μπορούσαν να ληφθούν λανθασμένα ως σημεία στίξης. Η δυαδικοποίηση ενισχύει τον διαχωρισμό προσκηνίου/υπόβαθρου, έναν κρίσιμο παράγοντα για ακριβή τμηματοποίηση χαρακτήρων.

---

## Βήμα 3: Καθορισμός του Αρχείου Εικόνας για το Engine

Τώρα λέμε στο engine ποιο αρχείο να επεξεργαστεί. Χρησιμοποιήστε απόλυτη διαδρομή ή σχετική από το φάκελο εξόδου του έργου. Αν πειραματίζεστε, αντιγράψτε μερικές δοκιμαστικές εικόνες σε έναν φάκελο `Resources`.

```csharp
// Step 3: Specify the input image
string imagePath = @"Resources/skewed_noisy.jpg";

// Optional: Verify the file exists before proceeding
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"Image not found: {imagePath}");
    return;
}
```

> **Edge case:** Αν η εικόνα σας βρίσκεται σε μορφή που δεν υποστηρίζεται εγγενώς (π.χ., TIFF με πολλαπλές σελίδες), μετατρέψτε την πρώτα σε PNG ή JPEG, ή χρησιμοποιήστε το `Aspose.Imaging` για να εξάγετε τη ζητούμενη σελίδα.

---

## Βήμα 4: Εκτέλεση OCR στην Προεπεξεργασμένη Εικόνα

Με το engine διαμορφωμένο και την εικόνα εντοπισμένη, καλέστε το `RecognizeImage`. Η μέθοδος επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει το εξαγόμενο κείμενο, τις βαθμολογίες εμπιστοσύνης, και ακόμη τα πλαίσια οριοθέτησης αν τα χρειαστείτε αργότερα.

```csharp
// Step 4: Perform OCR
OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

// Check if any text was found
if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
{
    Console.WriteLine("No recognizable text found.");
    return;
}
```

**Τι συμβαίνει στο παρασκήνιο;**  
Το Aspose OCR πρώτα εκτελεί τη σειρά προεπεξεργασίας που ορίσατε στο Βήμα 2, στη συνέχεια τροφοδοτεί το καθαρισμένο bitmap στον αναγνωριστή που βασίζεται σε νευρωνικό δίκτυο. Το αποτέλεσμα είναι συνήθως μια δραματική αύξηση στην ακρίβεια — συχνά από 60 % σε πάνω από 95 % σε απαιτητικές σάρωσες.

---

## Βήμα 5: Εμφάνιση ή Αποθήκευση του Αναγνωρισμένου Κειμένου

Τέλος, εξάγετε το αναγνωρισμένο κείμενο στην κονσόλα, σε αρχείο ή σε οποιαδήποτε υπηρεσία downstream. Για μια γρήγορη επίδειξη, η κονσόλα είναι επαρκής.

```csharp
// Step 5: Output the recognized text
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(ocrResult.Text);
Console.WriteLine("======================");

// Optional: Save to a .txt file
System.IO.File.WriteAllText("output.txt", ocrResult.Text);
```

Η αναμενόμενη έξοδος μοιάζει με καθαρό, γραμμή‑με‑γραμμή κείμενο — χωρίς περιττά σύμβολα ή σπασμένες λέξεις.

---

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε μια εφαρμογή κονσόλας. Περιλαμβάνει όλα τα βήματα, τη διαχείριση σφαλμάτων και τα σχόλια που χρειάζεστε για να ξεκινήσετε αμέσως.

```csharp
// ------------------------------------------------------------
// Full Example: Recognize Text Image with Aspose OCR C#
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class PreprocessExample
{
    public static void Run()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable preprocessing – deskew, denoise, binarization
        ocrEngine.Settings.PreprocessOptions = new PreprocessOptions
        {
            EnableDeskew = true,
            EnableDenoise = true,
            EnableBinarization = true,
            BinarizationThreshold = 120 // Adjust for your images
        };

        // 3️⃣ Specify the input image
        string imagePath = @"Resources/skewed_noisy.jpg";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found: {imagePath}");
            return;
        }

        // 4️⃣ Run OCR on the preprocessed image
        OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No recognizable text found.");
            return;
        }

        // 5️⃣ Display the recognized text
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("======================");

        // Save to a file for later use
        System.IO.File.WriteAllText("output.txt", ocrResult.Text);
    }

    // Entry point for quick testing
    static void Main()
    {
        Run();
    }
}
```

**Αναμενόμενη έξοδος κονσόλας (παράδειγμα):**

```
=== Recognized Text ===
Invoice #12345
Date: 2024-04-30
Total: $1,250.00
Thank you for your business!
======================
```

Αν εκτελέσετε τον ίδιο κώδικα χωρίς προεπεξεργασία, πιθανότατα θα δείτε ακατάληπτους χαρακτήρες όπως “Ivn0i#12?5” αντί για “Invoice #12345”.

---

## Συχνές Ερωτήσεις (FAQs)

### Λειτουργεί αυτό με **Aspose OCR C#** σε .NET Core;
Απολύτως. Η βιβλιοθήκη είναι **platform‑agnostic**· απλώς κάντε αναφορά στο πακέτο NuGet και είστε έτοιμοι.

### Τι γίνεται αν η εικόνα είναι ήδη υψηλής αντίθεσης—πρέπει να ενεργοποιήσω ακόμα τη δυαδικοποίηση;
Συνήθως ναι. Η δυαδικοποίηση με ένα λογικό όριο (120 λειτουργεί για πολλά σαρωμένα έγγραφα) δεν βλάπτει μια καθαρή εικόνα, και εγγυάται ότι το engine λειτουργεί με δυαδικό bitmap, που είναι η βέλτιστη μορφή εισόδου του.

### Μπορώ να ρυθμίσω τη γωνία deskew χειροκίνητα;
Μπορείτε, προσπερνώντας το `ocrEngine.Settings.PreprocessOptions.DeskewAngle`. Ωστόσο, ο αλγόριθμος αυτόματης ανίχνευσης είναι αξιόπιστος για γωνίες μεταξύ –15° και +15°. Για ακραίες περιστροφές, προ‑στρέψτε την εικόνα με μια βιβλιοθήκη επεξεργασίας εικόνας πρώτα.

### Πώς να διαχειριστώ PDF πολλαπλών σελίδων;
Μετατρέψτε κάθε σελίδα σε εικόνα (π.χ., χρησιμοποιώντας το `Aspose.PDF`), στη συνέχεια επαναλάβετε τις σελίδες καλώντας το `RecognizeImage` για κάθε μία. Αποθηκεύστε τα αποτελέσματα σε λίστα και ενώστε τα αν χρειάζεται.

---

## Pro Tips & Συνηθισμένα Παγίδες

- **Ρύθμιση Κατωφλίου:** Αν παρατηρήσετε ότι αδύναμοι χαρακτήρες παραλείπονται, μειώστε το `BinarizationThreshold` στα 90· αν εμφανιστούν πολλά μαύρα στίγματα, αυξήστε το στα 150.  
- **Διαχείριση Μνήμης:** Για μεγάλες παρτίδες, επαναχρησιμοποιήστε ένα μόνο αντικείμενο `OcrEngine` αντί να δημιουργείτε νέο για κάθε εικόνα — μειώνει την πίεση του GC.  
- **Υποστήριξη Γλώσσας:** Το Aspose OCR υποστηρίζει πολλαπλές γλώσσες αμέσως. Ορίστε `ocrEngine.Language = Language.English` (ή άλλη) πριν καλέσετε το `RecognizeImage` για καλύτερη ακρίβεια σε μη‑Αγγλικό κείμενο.  
- **Καταγραφή (Logging):** Ενεργοποιήστε `ocrEngine.Settings.LogLevel = LogLevel.Debug` αν χρειαστεί να εντοπίσετε γιατί μια συγκεκριμένη εικόνα αποτυγχάνει.

---

## Συμπέρασμα

Μόλις σας δείξαμε πώς να **αναγνωρίσετε εικόνα κειμένου** αξιόπιστα χρησιμοποιώντας το Aspose OCR C# ενώ εφαρμόζετε τις βασικές τεχνικές *προεπεξεργασίας εικόνας OCR*. Ενεργοποιώντας το deskew, το denoise και τη δυαδικοποίηση, το engine λαμβάνει ένα καθαρό bitmap, το οποίο μεταφράζεται σε υψηλότερες βαθμολογίες εμπιστοσύνης και πολύ λιγότερα σφάλματα μεταγραφής.

Πάρτε αυτόν τον κώδικα, δείξτε τον στις δικές σας σαρώσεις, ρυθμίστε τα όρια, και θα δείτε την ίδια βελτίωση σε τιμολόγια, αποδείξεις ή χειρόγραφες σημειώσεις. Στη συνέχεια, μπορείτε να εξερευνήσετε τις προχωρημένες δυνατότητες του **aspose ocr c#**, όπως προσαρμοσμένα λεξικά, OCR με βάση περιοχές, ή ενσωμάτωση με Azure Blob storage για μεγάλης κλίμακας pipelines.

Καλό κώδικα, και εύχομαι τα αποτελέσματα OCR σας να είναι πάντα κρυστάλλινα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}