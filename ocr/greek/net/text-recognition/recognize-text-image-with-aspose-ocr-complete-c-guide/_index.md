---
category: general
date: 2026-06-22
description: Μάθετε πώς να αναγνωρίζετε εικόνες κειμένου και να εξάγετε κείμενο από
  εικόνες υψηλής ανάλυσης OCR σε τιμολόγια χρησιμοποιώντας το Aspose OCR. Περιλαμβάνει
  ορισμό γλώσσας OCR και επιτάχυνση GPU.
draft: false
keywords:
- recognize text image
- extract text image
- high resolution ocr
- process invoice ocr
- set ocr language
language: el
og_description: Αναγνώριση εικόνας κειμένου χρησιμοποιώντας το Aspose OCR σε C#. Αυτό
  το σεμινάριο δείχνει πώς να εξάγετε κείμενο από εικόνα υψηλής ανάλυσης σε τιμολόγια,
  να ορίσετε τη γλώσσα OCR και να ενισχύσετε την απόδοση.
og_title: Αναγνώριση κειμένου σε εικόνα με το Aspose OCR – Πλήρης Οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to recognize text image and extract text image from high
    resolution OCR invoices using Aspose OCR. Includes set OCR language and GPU acceleration.
  headline: recognize text image with Aspose OCR – Complete C# Guide
  type: TechArticle
- description: Learn how to recognize text image and extract text image from high
    resolution OCR invoices using Aspose OCR. Includes set OCR language and GPU acceleration.
  name: recognize text image with Aspose OCR – Complete C# Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 SDK or later (the code also works on .NET Framework 4.7+). -
      A valid Aspose.OCR NuGet package (free trial works fine). - A high‑resolution
      image of an invoice (e.g., `high_res_invoice.png`). - Basic familiarity with
      C# and Visual Studio or your favorite IDE.'
  - name: 1. Image Quality Matters
    text: Even the fastest GPU can’t fix a blurry scan. Aim for at least **300 dpi**
      for invoices; lower resolutions cause missed characters. If you can’t control
      the source, consider pre‑processing with a sharpening filter before sending
      the image to Aspose.
  - name: 2. Memory Consumption on Very Large Files
    text: A 5000 × 7000 pixel PNG can consume several hundred megabytes of RAM. If
      you hit `OutOfMemoryException`, split the invoice into pages or downscale slightly
      (e.g., to 250 dpi) before OCR.
  - name: 3. Fallback to CPU When GPU Fails
    text: If the GPU driver crashes, Aspose will silently revert to CPU. To ensure
      you’re always using the GPU, check `ocrEngine.ProcessingMode` after initialization
      and log a warning if it isn’t `ProcessingMode.Gpu`.
  - name: 4. Multi‑Language Documents
    text: 'When an invoice contains both English and Spanish, you can enable **multiple
      languages**:'
  type: HowTo
tags:
- Aspose OCR
- C#
- Image Processing
title: Αναγνώριση κειμένου σε εικόνα με Aspose OCR – Πλήρης οδηγός C#
url: /el/net/text-recognition/recognize-text-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση κειμένου σε εικόνα με Aspose OCR – Πλήρης Οδηγός C#

Έχετε χρειαστεί ποτέ να **αναγνωρίσετε κείμενο σε εικόνα** αλλά τα αποτελέσματα να είναι θολά ή εξαιρετικά αργά; Δεν είστε μόνοι. Είτε σαρώνετε ένα υψηλής ανάλυσης τιμολόγιο είτε εξάγετε δεδομένα από ένα σαρωμένο συμβόλαιο, η λήψη καθαρού, αξιόπιστου αποτελέσματος είναι κρίσιμη. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, έτοιμο προς εκτέλεση παράδειγμα που **αναγνωρίζει κείμενο σε εικόνα** από αρχείο υψηλής ανάλυσης, **εξάγει κείμενο από εικόνα**, και ακόμη **ορίζει τη γλώσσα OCR** για βέλτιστη ακρίβεια — όλα με χρήση επιτάχυνσης GPU.

Θα προσθέσουμε επίσης μερικά επιπλέον κόλπα: πώς να **επεξεργαστείτε OCR τιμολογίων** αποδοτικά, γιατί μπορεί να θέλετε **OCR υψηλής ανάλυσης**, και τι να κάνετε όταν το GPU δεν είναι διαθέσιμο. Στο τέλος θα έχετε ένα ενιαίο πρόγραμμα C# που μετατρέπει ένα θολό PNG σε αναζητήσιμο κείμενο σε ελάχιστο χρόνο.

## Τι Θα Μάθετε

- Πώς να δημιουργήσετε ένα αντικείμενο `OcrEngine` με το Aspose OCR.  
- Ενεργοποίηση **GPU acceleration** για αστραπιαία **OCR υψηλής ανάλυσης**.  
- Χρήση της **set OCR language** για να στοχεύσετε στα Αγγλικά (ή οποιαδήποτε άλλη υποστηριζόμενη γλώσσα).  
- **Extract text image** από αρχείο υψηλής ανάλυσης τιμολογίου.  
- Μέτρηση του χρόνου επεξεργασίας ώστε να αποδείξετε τα κέρδη απόδοσης.  
- Διαχείριση σεναρίων fallback όταν το GPU δεν είναι παρόν.

### Προαπαιτούμενα

- .NET 6.0 SDK ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.7+).  
- Ένα έγκυρο πακέτο Aspose.OCR NuGet (η δωρεάν δοκιμή λειτουργεί κανονικά).  
- Μια εικόνα υψηλής ανάλυσης ενός τιμολογίου (π.χ. `high_res_invoice.png`).  
- Βασική εξοικείωση με C# και Visual Studio ή το αγαπημένο σας IDE.

---

## Βήμα 1: Εγκατάσταση Aspose.OCR και Προετοιμασία του Έργου

Πρώτα απ’ όλα—προσθέστε τη βιβλιοθήκη Aspose OCR στο έργο σας. Ανοίξτε ένα τερματικό στο φάκελο της λύσης και τρέξτε:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Κρατήστε το πακέτο ενημερωμένο· οι νεότερες εκδόσεις βελτιώνουν την υποστήριξη GPU και τα μοντέλα γλώσσας.

Δημιουργήστε μια νέα εφαρμογή console αν δεν έχετε ήδη:

```bash
dotnet new console -n OcrInvoiceDemo
cd OcrInvoiceDemo
```

Τώρα έχετε ένα καθαρό περιβάλλον για **αναγνώριση κειμένου σε εικόνα**.

## Βήμα 2: Αρχικοποίηση του OCR Engine (Ενεργοποίηση GPU)

Η καρδιά της διαδικασίας είναι το `OcrEngine`. Από προεπιλογή τρέχει στην CPU, αλλά για **OCR υψηλής ανάλυσης** σε μεγάλες σαρώνες τιμολογίων το GPU μπορεί να μειώσει σημαντικά το χρόνο εκτέλεσης.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Step 2: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    // Enable GPU processing – dramatically speeds up high‑resolution OCR
    ProcessingMode = ProcessingMode.Gpu
};
```

> **Γιατί GPU;** Μια εικόνα υψηλής ανάλυσης μπορεί να περιέχει εκατομμύρια pixel. Η GPU τα επεξεργάζεται παράλληλα, μετατρέποντας μια εργασία 5 δευτερολέπτων στην CPU σε υποδευτερόλεπτο στην πλειονότητα των σύγχρονων καρτών γραφικών.

Αν το μηχάνημα-στόχος δεν διαθέτει συμβατό GPU, το Aspose θα επιστρέψει αυτόματα σε λειτουργία CPU. Μπορείτε να εντοπίσετε αυτό το fallback ως εξής:

```csharp
if (ocrEngine.ProcessingMode != ProcessingMode.Gpu)
{
    Console.WriteLine("GPU not available – using CPU fallback.");
}
```

## Βήμα 3: **set OCR language** – Επιλέξτε το Σωστό Λεξικό

Το Aspose OCR περιλαμβάνει βασικές γλώσσες· τα Αγγλικά είναι η προεπιλογή, αλλά μπορείτε να τα ορίσετε ρητά. Αυτό είναι σημαντικό επειδή το μοντέλο γλώσσας επηρεάζει τη διαχωριστική λειτουργία χαρακτήρων και τις αναζητήσεις λεξικού.

```csharp
// Step 3: Explicitly set the language to English (core language)
ocrEngine.Language = OcrLanguage.English;
```

> **Edge case:** Αν χρειάζεται να διαβάσετε ένα γαλλικό τιμολόγιο, απλώς αντικαταστήστε το `OcrLanguage.English` με `OcrLanguage.French`. Η ίδια κλήση **set OCR language** λειτουργεί για οποιαδήποτε υποστηριζόμενη γλώσσα.

## Βήμα 4: **recognize text image** – Φορτώστε ένα Υψηλής Ανάλυσης Τιμολόγιο

Τώρα πραγματικά **αναγνωρίζουμε κείμενο σε εικόνα**. Κατευθύνετε τη μηχανή σε ένα PNG (ή TIFF) υψηλής ανάλυσης που θέλετε να επεξεργαστείτε. Η διαδρομή μπορεί να είναι απόλυτη ή σχετική· απλώς βεβαιωθείτε ότι το αρχείο υπάρχει.

```csharp
// Step 4: Recognize the image and capture the result
string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);
```

Το αντικείμενο `OcrResult` περιέχει τόσο το εξαγόμενο κείμενο όσο και πληροφορίες χρονομέτρησης, τις οποίες θα εμφανίσουμε αμέσως μετά.

## Βήμα 5: **extract text image** – Εμφάνιση Αποτελεσμάτων και Χρόνου Επεξεργασίας

Τέλος, εκτυπώστε το κείμενο OCR και το χρόνο που χρειάστηκε. Αυτή είναι η στιγμή που μπορείτε να επαληθεύσετε ότι η **process invoice OCR** εκτελέστηκε όπως αναμενόταν.

```csharp
// Step 5: Output processing time and extracted text
Console.WriteLine($"GPU OCR time: {ocrResult.ProcessingTimeMs} ms");
Console.WriteLine("=== Extracted Text Start ===");
Console.WriteLine(ocrResult.Text);
Console.WriteLine("=== Extracted Text End ===");
```

Η εκτέλεση του προγράμματος θα πρέπει να παράγει κάτι όπως:

```
GPU OCR time: 312 ms
=== Extracted Text Start ===
Invoice #12345
Date: 2024‑04‑15
Total: $1,250.00
...
=== Extracted Text End ===
```

Αυτό ήταν—η ροή εργασίας **extract text image** ολοκληρώθηκε.

---

## Bonus: Διαχείριση Συνηθισμένων Παγίδων

### 1. Η Ποιότητα της Εικόνας Μετράει

Ακόμη και η πιο γρήγορη GPU δεν μπορεί να διορθώσει μια θολή σάρωση. Στοχεύστε τουλάχιστον σε **300 dpi** για τιμολόγια· χαμηλότερες αναλύσεις οδηγούν σε χαμένα χαρακτήρες. Αν δεν μπορείτε να ελέγξετε την πηγή, σκεφτείτε προεπεξεργασία με φίλτρο όξυνσης πριν στείλετε την εικόνα στο Aspose.

### 2. Κατανάλωση Μνήμης σε Πολύ Μεγάλες Αρχεία

Ένα PNG 5000 × 7000 pixel μπορεί να καταναλώσει αρκετά εκατοντάδες megabytes RAM. Αν αντιμετωπίσετε `OutOfMemoryException`, χωρίστε το τιμολόγιο σε σελίδες ή μειώστε ελαφρώς την ανάλυση (π.χ. σε 250 dpi) πριν το OCR.

### 3. Fallback σε CPU Όταν Αποτύχει το GPU

Αν ο οδηγός GPU καταρρεύσει, το Aspose θα επιστρέψει σιωπηλά στην CPU. Για να βεβαιωθείτε ότι χρησιμοποιείτε πάντα το GPU, ελέγξτε το `ocrEngine.ProcessingMode` μετά την αρχικοποίηση και καταγράψτε προειδοποίηση αν δεν είναι `ProcessingMode.Gpu`.

### 4. Πολυγλωσσικά Έγγραφα

Όταν ένα τιμολόγιο περιέχει τόσο Αγγλικά όσο και Ισπανικά, μπορείτε να ενεργοποιήσετε **multiple languages**:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

Η μηχανή θα προσπαθήσει να αναγνωρίσει χαρακτήρες από οποιοδήποτε από τα δύο σύνολα γλωσσών.

---

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω βρίσκεται το **πλήρες, εκτελέσιμο πρόγραμμα** που ενσωματώνει όλα τα βήματα που συζητήθηκαν. Αντιγράψτε‑και‑επικολλήστε το στο `Program.cs`, αντικαταστήστε τη διαδρομή της εικόνας και πατήστε **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 2: Create an OCR engine instance and enable GPU acceleration
        var ocrEngine = new OcrEngine
        {
            ProcessingMode = ProcessingMode.Gpu // Fast high‑resolution OCR
        };

        // Verify GPU availability (optional but helpful)
        if (ocrEngine.ProcessingMode != ProcessingMode.Gpu)
        {
            Console.WriteLine("GPU not detected – falling back to CPU processing.");
        }

        // Step 3: Set the OCR language (set OCR language for better accuracy)
        ocrEngine.Language = OcrLanguage.English; // Change as needed

        // Step 4: Recognize text from a high‑resolution invoice image
        string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
        OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

        // Step 5: Display processing time and the extracted text
        Console.WriteLine($"GPU OCR time: {ocrResult.ProcessingTimeMs} ms");
        Console.WriteLine("=== Extracted Text Start ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("=== Extracted Text End ===");
    }
}
```

**Αναμενόμενο αποτέλεσμα** (οι χρόνοι θα διαφέρουν ανά υλικό):

```
GPU OCR time: 287 ms
=== Extracted Text Start ===
Invoice #98765
Date: 2024‑03‑22
Amount Due: $2,340.00
...
=== Extracted Text End ===
```

Τρέξτε το σε μερικά διαφορετικά τιμολόγια για να δείτε πώς ο χρόνος επεξεργασίας παραμένει κάτω από μισό δευτερόλεπτο σε μια μέτρια GPU.

---

## Συμπέρασμα

Μόλις μάθατε πώς να **αναγνωρίζετε κείμενο σε εικόνα** χρησιμοποιώντας το Aspose OCR, να **εξάγετε κείμενο από εικόνα** από ένα τιμολόγιο υψηλής ανάλυσης, και να **ορίσετε τη γλώσσα OCR** για βέλτιστα αποτελέσματα — όλα αξιοποιώντας την επιτάχυνση GPU για **OCR υψηλής ανάλυσης**. Ο κώδικας που παρουσιάστηκε είναι έτοιμος για παραγωγή, περιλαμβάνει λογική fallback, και μπορεί να επεκταθεί για διαχείριση πολυσελιδών PDF, διαφορετικών γλωσσών ή ακόμη και ροών βίντεο σε πραγματικό χρόνο.

Τι θα κάνετε στη συνέχεια; Δοκιμάστε:

- Μετατροπή του εξαγόμενου κειμένου σε δομημένο αντικείμενο JSON τιμολογίου.  
- Προσθήκη προεπεξεργασίας εικόνας (απλοποίηση, διόρθωση κλίσης) για βελτίωση της ακρίβειας σε χαμηλής ποιότητας σαρώσεις.  
- Ενσωμάτωση της κλήσης OCR σε ένα ASP.NET Core API ώστε η υπηρεσία σας να επεξεργάζεται τιμολόγια κατ’ απαίτηση.

Έχετε ερωτήσεις σχετικά με την **process invoice OCR** ή χρειάζεστε βοήθεια με τα πακέτα γλώσσας; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική δουλειά!

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}