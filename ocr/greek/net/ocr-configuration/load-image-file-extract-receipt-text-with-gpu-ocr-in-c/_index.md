---
category: general
date: 2026-02-14
description: Φορτώστε αρχείο εικόνας και εξάγετε κείμενο από την απόδειξη χρησιμοποιώντας
  τη μηχανή Aspose OCR GPU. Μάθετε πώς να ορίσετε τη μέγιστη μνήμη GPU, να διαμορφώσετε
  τη μνήμη GPU και να εκτελέσετε OCR στην εικόνα αποδοτικά.
draft: false
keywords:
- load image file
- extract text from receipt
- set max gpu memory
- run OCR on image
- configure gpu memory
language: el
og_description: Φορτώστε αρχείο εικόνας και εξάγετε κείμενο από απόδειξη χρησιμοποιώντας
  τη μηχανή Aspose OCR GPU. Αυτός ο οδηγός δείχνει πώς να ορίσετε τη μέγιστη μνήμη
  GPU και να εκτελέσετε OCR σε εικόνα σε C#.
og_title: Φόρτωση αρχείου εικόνας & εξαγωγή κειμένου από απόδειξη με GPU OCR σε C#
tags:
- C#
- OCR
- Aspose
- GPU
title: Φόρτωση αρχείου εικόνας & εξαγωγή κειμένου από απόδειξη με GPU OCR σε C#
url: /el/net/ocr-configuration/load-image-file-extract-receipt-text-with-gpu-ocr-in-c/
---

answer with all content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Φόρτωση Αρχείου Εικόνας & Εξαγωγή Κειμένου Από Απόδειξη με GPU OCR σε C#

Έχετε ποτέ χρειαστεί να **load image file** και να εξάγετε το ακριβές κείμενο από μια απόδειξη, αλλά να έχετε κολλήσει στο βήμα OCR; Δεν είστε οι μόνοι. Σε πολλές πραγματικές εφαρμογές—εφαρμογές παρακολούθησης εξόδων, συστήματα αποθεμάτων ή ακόμη και απλοί bot σάρωσης αποδείξεων—η δυνατότητα γρήγορης ανάγνωσης μιας εικόνας απόδειξης μπορεί να είναι καθοριστική.  

Τα καλά νέα; Με τη μηχανή GPU‑accelerated της Aspose.OCR μπορείτε να **load image file**, **set max GPU memory**, και **run OCR on image** με λίγες καθαρές γραμμές C#. Παρακάτω θα περάσουμε από όλη τη διαδικασία, από τη ρύθμιση του GPU μέχρι την εκτύπωση του εξαγόμενου plain‑text.

## Τι Θα Μάθετε

Σε αυτό το tutorial θα ανακαλύψετε πώς να:

* **Load image file** από το δίσκο χρησιμοποιώντας το `ImageStream` της Aspose.
* **Configure GPU memory** ώστε η μηχανή να μην καταναλώνει περισσότερη RAM από ό,τι επιτρέπετε.
* **Run OCR on image** και να εξάγετε κάθε χαρακτήρα από μια απόδειξη.
* Αντιμετωπίσετε κοινά προβλήματα—όπως σφάλματα out‑of‑memory ή θολές σαρώσεις.
* Επαληθεύσετε το αποτέλεσμα και να ρυθμίσετε τις παραμέτρους για καλύτερη ακρίβεια.

Καμία εξωτερική υπηρεσία, κανένα περίπλοκο κόλπο—απλώς καθαρός κώδικας C# που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET 6+.

---

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

* .NET 6 SDK ή νεότερη έκδοση εγκατεστημένη.
* Ένα έγκυρο license της Aspose.OCR (ή μπορείτε να χρησιμοποιήσετε τη δωρεάν λειτουργία evaluation).
* Τα πακέτα NuGet `Aspose.OCR` και `Aspose.OCR.Gpu` προστεμένα στο project σας.
* Μια δείγμα εικόνας απόδειξης (`receipt.png`) έτοιμη στο δίσκο.

Αν κάτι από αυτά δεν σας είναι γνωστό, κάντε μια παύση και εγκαταστήστε τα πακέτα:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

Αυτό είναι όλο—δεν απαιτούνται επιπλέον native libraries επειδή η υποστήριξη GPU είναι ενσωματωμένη στο NuGet package.

---

## Φόρτωση Αρχείου Εικόνας και Προετοιμασία Μηχανής GPU

Το πρώτο βήμα είναι να **load image file** σε ένα `ImageStream`. Αυτό το αντικείμενο αφαιρεί τις λεπτομέρειες του συστήματος αρχείων και παρέχει στη μηχανή OCR μια καθαρή, in‑memory αναπαράσταση.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;

// Step 1️⃣: Initialize the GPU‑accelerated engine.
var gpuEngine = new GpuEngine
{
    // Step 2️⃣: Set a safety net for GPU RAM usage.
    // Here we limit the engine to 1024 MB (1 GB). Adjust as needed.
    MaxDeviceMemory = 1024 // MB
};

// Step 3️⃣: Load the receipt image from disk.
var receiptImage = ImageStream.FromFile(@"C:\MyReceipts\receipt.png");

// At this point the image is ready for OCR.
```

**Γιατί είναι σημαντικό:**  
*Loading the image file* μέσω `ImageStream.FromFile` εγγυάται ότι η μηχανή βλέπει τα ακριβή pixel data, διατηρώντας DPI και βάθος χρώματος. Η παράλειψη αυτού του βήματος ή η παροχή κατεστραμμένου stream θα κάνει την OCR να χάσει χαρακτήρες ή να πετάξει εξαιρέσεις.

> **Pro tip:** Αν διαχειρίζεστε αρχεία που ανεβάζουν χρήστες, τυλίξτε την κλήση `FromFile` σε block `try‑catch` και επικυρώστε πρώτα το μέγεθος του αρχείου. Μεγάλες εικόνες μπορούν να εξαντλήσουν τη μνήμη GPU αν δεν **configure GPU memory** σωστά.

---

## Ορισμός Μέγιστης Μνήμης GPU για Βέλτιστη Απόδοση

Οι πόροι GPU είναι πολύτιμοι, ειδικά σε κοινόχρηστους servers ή laptops με περιορισμένο VRAM. Η ιδιότητα `MaxDeviceMemory` λέει στην Aspose πόση μνήμη του GPU μπορεί να δεσμεύσει με ασφάλεια.

```csharp
// Example: Restrict to 512 MB for low‑end GPUs.
gpuEngine.MaxDeviceMemory = 512; // MB
```

Όταν **set max GPU memory**, η μηχανή θα επιστρέψει αυτόματα στην επεξεργασία CPU αν δεν μπορεί να ικανοποιήσει το αίτημα—αποτρέποντας καταρρεύσεις. Αυτός είναι ο ασφαλέστερος τρόπος να **configure GPU memory** χωρίς σκληρή κωδικοποίηση περιορισμών ανά συσκευή.

**Πότε να προσαρμόσετε:**  
* Αν παρατηρήσετε `OutOfMemoryException` κατά την επεξεργασία μεγάλων batch, μειώστε το όριο.  
* Αν οι αποδείξεις σας είναι υψηλής ανάλυσης (300 DPI+), αυξήστε το σε 2 GB για να διατηρήσετε την ταχύτητα.

---

## Εκτέλεση OCR στην Εικόνα για Εξαγωγή Κειμένου Από Απόδειξη

Τώρα το διασκεδαστικό μέρος—να **run OCR on image** και να εξάγετε το κείμενο της απόδειξης. Η μέθοδος `Recognize` επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει την ιδιότητα `Text` με το plain‑text αποτέλεσμα.

```csharp
// Step 4️⃣: Perform OCR.
OcrResult ocrResult = gpuEngine.Recognize(receiptImage);

// Step 5️⃣: Output the extracted text.
Console.WriteLine("=== Receipt Text ===");
Console.WriteLine(ocrResult.Text);
```

Η κονσόλα θα εμφανίσει κάτι όπως:

```
=== Receipt Text ===
Store: Coffee Corner
Date: 02/13/2026
Item            Qty   Price
Latte           2     $5.00
Muffin          1     $2.50
Total                     $12.50
```

**Γιατί λειτουργεί:**  
Η μηχανή GPU εκτελεί ένα deep‑learning μοντέλο που έχει εκπαιδευτεί σε ποικίλες διατάξεις εγγράφων. Με μια καθαρή, σωστά φορτωμένη εικόνα, δίνετε στο μοντέλο την καλύτερη ευκαιρία να **extract text from receipt** με ακρίβεια.

---

## Επαλήθευση Αποτελέσματος και Συνηθισμένα Προβλήματα

Ακόμη και με μια ισχυρή μηχανή, το OCR δεν είναι μαγικό. Εδώ είναι μερικά πράγματα στα οποία πρέπει να προσέχετε:

| Issue | Cause | Fix |
|-------|-------|-----|
| Garbled characters | Low contrast or blurred image | Pre‑process with Aspose’s `ImageProcessor` to increase contrast |
| Missing lines | Image cropped too tightly | Ensure the receipt fits fully within the image bounds |
| Out‑of‑memory errors | `MaxDeviceMemory` too low for image size | Increase `MaxDeviceMemory` or downscale the image first |
| Wrong language | Receipt contains non‑English text | Set `gpuEngine.Language = OcrLanguage.Spanish;` (or appropriate) |

Αν αντιμετωπίσετε κάποιο από αυτά, η γρήγορη λύση είναι να αλλάξετε το μέγεθος της εικόνας σε κάτω από 2000 px στην μεγαλύτερη πλευρά—αυτό μειώνει δραστικά την πίεση στη GPU χωρίς να θυσιάζει την αναγνωσιμότητα για τις περισσότερες αποδείξεις.

---

## Πλήρες Παράδειγμα (Έτοιμο για Copy‑Paste)

Παρακάτω είναι ολόκληρο το πρόγραμμα, έτοιμο για μεταγλώττιση. Αντικαταστήστε τη διαδρομή αρχείου με τη δική σας θέση αποδείξεων.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

class ReceiptOcrDemo
{
    static void Main()
    {
        // 1️⃣ Create GPU‑accelerated engine with a safe memory cap.
        var gpuEngine = new GpuEngine
        {
            MaxDeviceMemory = 1024 // MB – adjust for your hardware
        };

        // 2️⃣ Load the receipt image from disk.
        //    Make sure the path points to a valid PNG/JPEG file.
        var receiptImage = ImageStream.FromFile(@"C:\MyReceipts\receipt.png");

        // 3️⃣ Run OCR – this will automatically use the GPU if available.
        OcrResult ocrResult = gpuEngine.Recognize(receiptImage);

        // 4️⃣ Print the extracted text.
        Console.WriteLine("=== Receipt Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Αναμενόμενη έξοδος στην κονσόλα** (η δική σας απόδειξη θα διαφέρει, φυσικά):

```
=== Receipt Text ===
Store: Coffee Corner
Date: 02/13/2026
Item            Qty   Price
Latte           2     $5.00
Muffin          1     $2.50
Total                     $12.50
```

Τρέξτε το πρόγραμμα με `dotnet run`. Αν δείτε το κείμενο να εκτυπώνεται, συγχαρητήρια—έχετε επιτυχώς **load image file**, **set max GPU memory**, και **run OCR on image** για **extract text from receipt**.

---

## Συχνές Ερωτήσεις

**Q: Λειτουργεί αυτό σε μηχανήματα χωρίς dedicated GPU;**  
A: Ναι. Η Aspose.OCR θα επιστρέψει ομαλά σε λειτουργία CPU αν δεν εντοπιστεί συμβατό GPU. Θα μπορείτε ακόμα να **load image file** και να **run OCR on image**, απλώς με λίγο χαμηλότερη ταχύτητα.

**Q: Μπορώ να επεξεργαστώ πολλαπλές αποδείξεις σε batch;**  
A: Απόλυτα. Τυλίξτε τον κώδικα αναγνώρισης σε βρόχο `foreach`, αλλά θυμηθείτε να επαναχρησιμοποιήσετε το ίδιο αντικείμενο `GpuEngine`—αυτό αποφεύγει την επανεκκίνηση των πόρων GPU για κάθε αρχείο.

**Q: Τι γίνεται αν η απόδειξή μου είναι σε γλώσσα διαφορετική από τα Αγγλικά;**  
A: Ορίστε τη γλώσσα πριν καλέσετε το `Recognize`:

```csharp
gpuEngine.Language = OcrLanguage.French;
```

Η μηχανή θα εφαρμόσει το αντίστοιχο σύνολο χαρακτήρων.

---

## Επόμενα Βήματα & Σχετικά Θέματα

Τώρα που έχετε κατακτήσει τα βασικά, σκεφτείτε να εξερευνήσετε:

* **Fine‑tuning OCR accuracy** – πειραματιστείτε με `gpuEngine.RecognitionOptions` όπως `EnableDeskew` ή `ContrastEnhancement`.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}