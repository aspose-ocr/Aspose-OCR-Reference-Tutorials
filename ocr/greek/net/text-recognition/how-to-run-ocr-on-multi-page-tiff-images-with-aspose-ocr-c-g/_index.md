---
category: general
date: 2026-02-11
description: Μάθετε πώς να εκτελείτε OCR σε ένα πολυσέλιδο αρχείο TIFF σε C# χρησιμοποιώντας
  το Aspose OCR. Μετατρέψτε το TIFF σε κείμενο, εξάγετε κείμενο από TIFF και αναγνωρίστε
  κείμενο από εικόνα γρήγορα.
draft: false
keywords:
- how to run OCR
- recognize text from image
- convert tiff to text
- extract text from tiff
- perform OCR on image
language: el
og_description: Πώς να εκτελέσετε OCR σε αρχείο TIFF πολλαπλών σελίδων χρησιμοποιώντας
  το Aspose OCR σε C#. Οδηγός βήμα‑προς‑βήμα για τη μετατροπή TIFF σε κείμενο, την
  εξαγωγή κειμένου από TIFF και την αναγνώριση κειμένου από εικόνα.
og_title: Πώς να εκτελέσετε OCR σε πολυσελιδικές εικόνες TIFF – Πλήρες σεμινάριο C#
tags:
- OCR
- C#
- Aspose
- TIFF
title: Πώς να εκτελέσετε OCR σε εικόνες TIFF πολλαπλών σελίδων με το Aspose OCR –
  Οδηγός C#
url: /el/net/text-recognition/how-to-run-ocr-on-multi-page-tiff-images-with-aspose-ocr-c-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εκτελέσετε OCR σε εικόνες TIFF πολλαπλών σελίδων με το Aspose OCR

Έχετε αναρωτηθεί ποτέ **πώς να εκτελέσετε OCR** σε ένα σαρωμένο TIFF που περιέχει πολλές σελίδες; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν πρέπει να εξάγουν αναζητήσιμο κείμενο από παλιά έγγραφα. Τα καλά νέα; Με το Aspose OCR μπορείτε να αναγνωρίσετε κείμενο από αρχεία εικόνας με λίγες μόνο γραμμές κώδικα C#, και θα έχετε ένα απλό ενωμένο κείμενο έτοιμο για ευρετηρίαση ή περαιτέρω επεξεργασία.

Σε αυτό το tutorial θα περάσουμε από όλη τη ροή εργασίας: από την εγκατάσταση του πακέτου Aspose OCR, τη φόρτωση ενός TIFF πολλαπλών σελίδων, τη μετατροπή TIFF σε κείμενο και, τέλος, την εμφάνιση του εξαγόμενου περιεχομένου. Στο τέλος θα μπορείτε να **εξάγετε κείμενο από TIFF** αρχεία, **αναγνωρίσετε κείμενο από εικόνα** πηγές, και ακόμη να αυτοματοποιήσετε τη διαδικασία για δεκάδες αρχεία σε μια παρτίδα. Χωρίς μαγεία, μόνο σαφή, πρακτικά βήματα.

## Τι θα μάθετε

- Πώς να ρυθμίσετε τη μηχανή Aspose OCR για αναγνώριση αγγλικής γλώσσας.  
- Ο ακριβής κώδικας που χρειάζεται για **μετατροπή TIFF σε κείμενο** χρησιμοποιώντας την κλάση `OcrEngine`.  
- Συμβουλές για τη διαχείριση εικόνων πολλαπλών σελίδων και τη σωστή διαχωριστική κάθε σελίδας.  
- Συνηθισμένα προβλήματα (όπως η έλλειψη εγγενών εξαρτήσεων) και πώς να τα αποφύγετε.  

**Prerequisites** – θα χρειαστείτε .NET 6 ή νεότερο, Visual Studio (ή οποιονδήποτε επεξεργαστή C#) και σύνδεση στο διαδίκτυο για τη λειτουργία αυτόματης λήψης πόρων. Αυτό είναι όλο· δεν απαιτούνται επιπλέον εγγενές βιβλιοθήκες.

---

## Step 1 – Install Aspose OCR NuGet Package

Πριν μπορέσετε να **εκτελέσετε OCR σε εικόνα** αρχεία, πρέπει να προσθέσετε τη βιβλιοθήκη στο έργο σας.

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Αν εργάζεστε στο Visual Studio, μπορείτε επίσης να κάνετε δεξί‑κλικ στο έργο → *Manage NuGet Packages* → ψάξτε για “Aspose.OCR” και κάντε κλικ στο *Install*.

Το πακέτο περιλαμβάνει όλα όσα χρειάζεστε, και με `AutomaticResourceDownload = true` η μηχανή θα κατεβάσει τα πακέτα γλώσσας αυτόματα.

---

## Step 2 – Initialize the OCR Engine (How to Run OCR)

Τώρα που το πακέτο είναι στη θέση του, δημιουργούμε και διαμορφώνουμε ένα στιγμιότυπο `OcrEngine`. Αυτό είναι η καρδιά του **πώς να εκτελέσετε OCR** στο σενάριό μας.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.Drawing;   // For Image class
using System;

// Step 2: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,          // Recognize English text
    AutomaticResourceDownload = true,        // Auto‑download language data
    OutputFormat = OcrOutputFormat.Text      // Get plain concatenated text
};
```

**Why this matters:** Η ρύθμιση του `Language` λέει στη μηχανή ποιο σύνολο χαρακτήρων να περιμένει, ενώ το `AutomaticResourceDownload` σας απαλλάσσει από το χειροκίνητοποθέτηση αρχείων γλώσσας στον διακομιστή. Το `OutputFormat` ως `Text` μας δίνει ένα απλό string—ιδανικό για pipelines **μετατροπής TIFF σε κείμενο**.

---

## Step 3 – Load the Multi‑Page TIFF (Recognize Text from Image)

Ένα TIFF μπορεί να περιέχει πολλά frames, το καθένα αντιπροσωπεύει μια σελίδα. Η κλάση `System.Drawing.Image` το αφαιρεί αυτό για εμάς.

```csharp
// Step 3: Load the multi‑page image to be processed
using (var image = Image.FromFile("YOUR_DIRECTORY/multi_page.tiff"))
{
    // Step 4: Run OCR on the image
    var ocrResult = ocrEngine.Recognize(image);

    // Step 5: Display the extracted text
    Console.WriteLine(ocrResult.Text);
}
```

> **What if the file isn’t in the same folder?** Απλώς δώστε το πλήρες απόλυτο μονοπάτι ή χρησιμοποιήστε `Path.Combine` με `AppContext.BaseDirectory`.  
> **What about memory usage?** Η δήλωση `using` απελευθερώνει την εικόνα μετά την επεξεργασία, αποτρέποντας διαρροές—σημαντικό όταν επεξεργάζεστε δεκάδες μεγάλα TIFF σε παρτίδα.

Η κλήση `Recognize` διασχίζει αυτόματα κάθε σελίδα του TIFF, ενώνωντας τα αποτελέσματα με αλλαγές γραμμής. Γι' αυτό θα δείτε κάθε σελίδα χωρισμένη όταν τυπώσετε το `ocrResult.Text`.

---

## Step 4 – Full Working Example (All Steps in One File)

Παρακάτω υπάρχει μια πλήρης, έτοιμη προς εκτέλεση εφαρμογή κονσόλας. Αντιγράψτε‑και‑επικολλήστε την σε ένα νέο .NET console project και πατήστε **F5**.

```csharp
// File: Program.cs
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Configure the OCR engine
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.English,
                AutomaticResourceDownload = true,
                OutputFormat = OcrOutputFormat.Text
            };

            // 2️⃣ Load your multi‑page TIFF (replace with your actual path)
            const string tiffPath = @"YOUR_DIRECTORY\multi_page.tiff";

            if (!System.IO.File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            // 3️⃣ Perform OCR
            using (var image = Image.FromFile(tiffPath))
            {
                var result = ocrEngine.Recognize(image);

                // 4️⃣ Output the extracted text
                Console.WriteLine("=== OCR RESULT ===");
                Console.WriteLine(result.Text);
                Console.WriteLine("==================");
            }

            // Keep console open
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Expected output** (truncated for brevity):

```
=== OCR RESULT ===
Page 1: The quick brown fox jumps over the lazy dog.
Page 2: Lorem ipsum dolor sit amet, consectetur adipiscing elit.
...
==================
Press any key to exit...
```

Κάθε σελίδα εμφανίζεται σε ξεχωριστή γραμμή επειδή το `OcrOutputFormat.Text` εισάγει αλλαγή γραμμής μεταξύ των frames. Αν χρειάζεστε διαφορετικό διαχωριστικό, μπορείτε να επεξεργαστείτε το `result.Text` με `String.Replace`.

---

## Step 5 – Handling Common Edge Cases

### 5.1 Large TIFF Files  
Όταν εργάζεστε με TIFF μεγέθους gigabyte, η φόρτωση ολόκληρου του αρχείου στη μνήμη μπορεί να είναι προβληματική. Μια λύση είναι η επεξεργασία κάθε frame ξεχωριστά:

```csharp
using (var image = Image.FromFile(tiffPath))
{
    for (int i = 0; i < image.GetFrameCount(FrameDimension.Page); i++)
    {
        image.SelectActiveFrame(FrameDimension.Page, i);
        var pageResult = ocrEngine.Recognize(image);
        Console.WriteLine($"--- Page {i + 1} ---");
        Console.WriteLine(pageResult.Text);
    }
}
```

### 5. Non‑English Documents  
Αν χρειάζεται να **αναγνωρίσετε κείμενο από εικόνα** στα Ισπανικά ή Γαλλικά, απλώς αλλάξτε την ιδιότητα `Language`:

```csharp
ocrEngine.Language = OcrLanguage.Spanish; // or OcrLanguage.French
```

Το Aspose θα κατεβάσει αυτόματα τους κατάλληλους πόρους γλώσσας.

### 5. Saving the Output  
Συχνά θα θέλετε να **μετατρέψετε TIFF σε κείμενο** και να αποθηκεύσετε το αποτέλεσμα σε αρχείο `.txt`:

```csharp
System.IO.File.WriteAllText("output.txt", ocrResult.Text);
```

Μπορείτε επίσης να χωρίσετε το αποτέλεσμα ανά σελίδα χρησιμοποιώντας `String.Split(Environment.NewLine)` και να γράψετε κάθε τμήμα σε ξεχωριστό αρχείο.

---

## Pro Tips & Gotchas

- **AutomaticResourceDownload** λειτουργεί την πρώτη φορά που τρέχετε την εφαρμογή· οι επόμενες εκτελέσεις είναι offline.  
- Αν δείτε ακατάλληλους χαρακτήρες, ελέγξτε ξανά τη ρύθμιση `Language`; τα λανθασμένα πακέτα γλώσσας προκαλούν λανθασμένη αναγνώριση.  
- Για PDF που έχουν rasterized σε TIFF, ίσως θελήσετε να αυξήσετε το `ocrEngine.Dpi` (προεπιλογή 300) για καλύτερη ακρίβεια.  
- Πάντα τυλίξτε το `Image.FromFile` σε μπλοκ `using`; διαφορετικά θα κλειδώσετε το αρχείο και δεν θα μπορείτε να το διαγράψετε ή μετακινήσετε αργότερα.

---

## Frequently Asked Questions

**Q: Does this work with single‑page TIFFs?**  
A: Absolutely. Η μηχανή αντιμετωπίζει ένα single‑frame TIFF με τον ίδιο τρόπο· θα λάβετε μόνο μία γραμμή κειμένου.

**Q: Can I process PNG or JPEG files the same way?**  
A: Yes—απλώς αλλάξτε την επέκταση του αρχείου. Η μέθοδος `Recognize` αποδέχεται οποιαδήποτε μορφή `System.Drawing.Image`.

**Q: What if I need the OCR result as PDF instead of plain text?**  
A: Ορίστε `OutputFormat = OcrOutputFormat.Pdf` και το `ocrResult` θα περιέχει έναν πίνακα byte PDF που μπορείτε να γράψετε στο δίσκο.

---

## Conclusion

Τώρα έχετε μια πλήρη, end‑to‑end λύση για **πώς να εκτελέσετε OCR** σε αρχεία TIFF πολλαπλών σελίδων χρησιμοποιώντας το Aspose OCR σε C#. Με τη διαμόρφωση της μηχανής, τη φόρτωση της εικόνας και την κλήση του `Recognize`, μπορείτε να **εξάγετε κείμενο από TIFF**, **μετατρέψετε TIFF σε κείμενο**, και **αναγνωρίσετε κείμενο από εικόνα** με λίγες μόνο γραμμές κώδικα. Μη διστάσετε να προσαρμόσετε τη γλώσσα, τη μορφή εξόδου ή την επεξεργασία frame‑by‑frame ώστε να ταιριάζει στις ανάγκες σας για παρτίδες.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να συνδυάσετε αυτήν την προσέγγιση με μια υπηρεσία folder‑watcher για να **εκτελείτε OCR αυτόματα σε εικόνες** καθώς καταλήγουν σε φάκελο εισόδου, ή ενσωματώστε το αποτέλεσμα σε ευρετήριο αναζήτησης για άμεση πλήρη κειμενική αναζήτηση. Οι δυνατότητες είναι ατελείωτες, και ο κώδικας που μόλις είδατε αποτελεί μια σταθερή βάση.

Αν αντιμετωπίσατε δυσκολίες, αφήστε ένα σχόλιο παρακάτω ή στείλτε μου μήνυμα στο GitHub. Καλή προγραμματιστική, και απολαύστε τη μετατροπή εκείνων των επίμονων TIFF σε αναζητήσιμο κείμενο!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}