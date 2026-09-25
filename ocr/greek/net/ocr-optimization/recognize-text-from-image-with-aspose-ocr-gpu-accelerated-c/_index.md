---
category: general
date: 2026-01-13
description: Μάθετε πώς να αναγνωρίζετε κείμενο από εικόνα και να εξάγετε κείμενο
  από την απόδειξη γρήγορα χρησιμοποιώντας το Aspose OCR. Περιλαμβάνει βήματα φόρτωσης
  εικόνας για OCR και ορισμού του ID της συσκευής GPU.
draft: false
keywords:
- recognize text from image
- extract text from receipt
- load image for ocr
- set gpu device id
language: el
og_description: Αναγνωρίστε κείμενο από εικόνα άμεσα με το Aspose OCR. Ακολουθήστε
  αυτόν τον οδηγό βήμα‑βήμα για να φορτώσετε την εικόνα για OCR, να ορίσετε το ID
  της συσκευής GPU και να εξάγετε κείμενο από την απόδειξη.
og_title: Αναγνώριση κειμένου από εικόνα – Πλήρης Οδηγός C# με Επιτάχυνση GPU
tags:
- Aspose OCR
- C#
- GPU computing
title: Αναγνώριση κειμένου από εικόνα με το Aspose OCR – Οδηγός C# με επιτάχυνση GPU
url: /el/net/ocr-optimization/recognize-text-from-image-with-aspose-ocr-gpu-accelerated-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση κειμένου από εικόνα – Πλήρης Οδηγός C# με Επιτάχυνση GPU

Κάποτε χρειάστηκε να **αναγνωρίσετε κείμενο από εικόνα** αλλά η έκδοση CPU ήταν εξαιρετικά αργή; Ίσως προσπαθείτε να **εξάγετε κείμενο από αποδείξεις** και η καθυστέρηση επηρεάζει την εμπειρία του χρήστη. Τα καλά νέα είναι ότι δεν χρειάζεται να συμβιβαστείτε με αργή απόδοση — το πακέτο GPU της Aspose OCR μπορεί να επιταχύνει τη διαδικασία, και ο κώδικας είναι μόλις μερικές γραμμές.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει πώς να **φορτώσετε εικόνα για OCR**, να ρυθμίσετε το GPU με **set GPU device ID**, και τέλος να ανακτήσετε το αποτέλεσμα ως απλό κείμενο. Στο τέλος θα έχετε ένα έτοιμο κομμάτι κώδικα που λειτουργεί σε οποιοδήποτε σύγχρονο Windows ή Linux μηχάνημα με υποστηριζόμενη κάρτα NVIDIA.

---

## Τι Θα Χρειαστεί

- **.NET 6+** (ή .NET Framework 4.7.2+) – το API λειτουργεί και με τις δύο.
- **Aspose.OCR** πακέτο NuGet **συν** το **Aspose.OCR.Gpu** add‑on.
- Μια κάρτα NVIDIA GPU με τουλάχιστον 2 GB VRAM (η επίδειξη περιορίζει τη χρήση στα 1 GB).
- Ένα δείγμα εικόνας, π.χ. μια σκαναρισμένη απόδειξη (`receipt.jpg`).

Αν έχετε ήδη έργο, απλώς τρέξτε `dotnet add package Aspose.OCR` και `dotnet add package Aspose.OCR.Gpu`. Δεν απαιτούνται επιπλέον native βιβλιοθήκες· το SDK περιλαμβάνει τα απαραίτητα binaries CUDA.

---

## Υλοποίηση Βήμα‑Βήμα

### ## Πώς να αναγνωρίσετε κείμενο από εικόνα χρησιμοποιώντας Aspose OCR και GPU

Παρακάτω βρίσκεται το **πλήρες, αυτόνομο πρόγραμμα**. Αντιγράψτε‑και‑επικολλήστε το σε ένα νέο console project και πατήστε `Ctrl+F5`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑accelerated namespace

class GpuOcrDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize a GPU‑enabled OCR engine
        // -------------------------------------------------
        var ocrEngine = new GpuOcrEngine();

        // -------------------------------------------------
        // Step 2: (Optional) Select the GPU device and limit memory usage
        // -------------------------------------------------
        ocrEngine.DeviceId = 0;        // set GPU device ID – first GPU in the system
        ocrEngine.MaxMemoryMb = 1024;  // cap at 1 GB to avoid OOM on shared machines

        // -------------------------------------------------
        // Step 3: Load the image you want to recognize
        // -------------------------------------------------
        var receiptImage = OcrImage.FromFile(@"YOUR_DIRECTORY/receipt.jpg");

        // -------------------------------------------------
        // Step 4: Perform OCR – here we extract text from receipt (English)
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(receiptImage, OcrLanguage.English);

        // -------------------------------------------------
        // Step 5: Output the recognized plain text
        // -------------------------------------------------
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

> **Συμβουλή:** Αν το μηχάνημά σας έχει πολλαπλές GPU, αλλάξτε το `DeviceId` σε `1`, `2`, κ.λπ., για να επιλέξετε την λιγότερο απασχολημένη κάρτα. Το SDK θα ρίξει ένα σαφές `GpuDeviceNotFoundException` αν το ID είναι εκτός εύρους.

### ### Βήμα 1: Φόρτωση εικόνας για OCR

Η κλήση `OcrImage.FromFile` κάνει περισσότερα από το απλό διάβασμα bitmap — προεπεξεργάζεται την εικόνα (απλοποίηση κλίσης, δυαδικοποίηση) βάσει εσωτερικών ευριστηρίων. Γι’ αυτό το **load image for OCR** είναι ξεχωριστό βήμα: μπορείτε να το αντικαταστήσετε με `MemoryStream` αν η εικόνα βρίσκεται σε βάση δεδομένων.

```csharp
var receiptImage = OcrImage.FromFile(@"C:\Invoices\receipt.jpg");
```

Αν χρειάζεται να **αναγνωρίσετε κείμενο από εικόνα** που είναι ήδη στη μνήμη:

```csharp
using (var ms = new MemoryStream(File.ReadAllBytes(@"receipt.jpg")))
{
    var receiptImage = OcrImage.FromStream(ms);
}
```

### ### Βήμα 2: Ορισμός GPU device ID και ορίων μνήμης

Οι πόροι GPU είναι περιορισμένοι. Εκθέτοντας τα `DeviceId` και `MaxMemoryMb`, η Aspose σας επιτρέπει να **set GPU device ID** με ασφάλεια, αποτρέποντας μια διεργασία να καταναλώσει ολόκληρη την κάρτα.

```csharp
ocrEngine.DeviceId = 0;        // first GPU
ocrEngine.MaxMemoryMb = 1024; // 1 GB ceiling
```

Αν υπερβείτε το όριο μνήμης, η μηχανή θα μεταφέρει αυτόματα δεδομένα στη RAM του συστήματος, κάτι που είναι πιο αργό αλλά αποτρέπει καταρρεύσεις.

### ### Βήμα 3: Εξαγωγή κειμένου από απόδειξη (recognize text from image)

Η μέθοδος `Recognize` κάνει το βαρέως βάρους έργο. Μπορείτε να περάσετε οποιαδήποτε γλώσσα υποστηρίζεται από το Aspose OCR· για αποδείξεις, τα Αγγλικά λειτουργούν στις περισσότερες περιπτώσεις, αλλά μπορείτε επίσης να προσθέσετε `OcrLanguage.Spanish` ή ένα προσαρμοσμένο language pack.

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, OcrLanguage.English);
Console.WriteLine(ocrResult.Text);
```

**Αναμενόμενο αποτέλεσμα** (παράδειγμα):

```
Store: QuickMart
Date: 2025-12-01
Total: $23.45
Thank you for shopping!
```

---

## Συχνές Παραλλαγές & Ακραίες Περιπτώσεις

| Κατάσταση | Τι να Αλλάξετε | Γιατί |
|-----------|----------------|------|
| **Πολλαπλές αποδείξεις σε μία εικόνα** | Κλήση `ocrEngine.Recognize` σε κάθε κομμένο τμήμα (χρησιμοποιήστε `OcrImage.Crop`) | Βελτιώνει την ακρίβεια επειδή η μηχανή βλέπει μικρότερο, καθαρότερο χώρο. |
| **Σάρωση χαμηλής ανάλυσης (<150 dpi)** | Προεπεξεργασία με `receiptImage.Resize(2.0)` πριν την αναγνώριση | Η υψηλότερη πυκνότητα εικονοστοιχείων δίνει στο GPU περισσότερα δεδομένα για επεξεργασία. |
| **Μη‑Αγγλικές αποδείξεις** | Πέρασμα `OcrLanguage.French` (ή προσαρμοσμένο `.traineddata`) | Τα μοντέλα ανά γλώσσα μειώνουν τα ψευδώς θετικά. |
| **GPU μη διαθέσιμο** | Εναλλακτική χρήση `OcrEngine` (CPU) μέσα σε try‑catch block | Εξασφαλίζει ότι η εφαρμογή λειτουργεί ακόμα και σε servers χωρίς GPU. |

```csharp
try
{
    var gpuEngine = new GpuOcrEngine();
    // configure GPU as shown earlier …
    var result = gpuEngine.Recognize(receiptImage, OcrLanguage.English);
    Console.WriteLine(result.Text);
}
catch (GpuDeviceNotFoundException)
{
    // Graceful fallback
    var cpuEngine = new OcrEngine();
    var result = cpuEngine.Recognize(receiptImage, OcrLanguage.English);
    Console.WriteLine(result.Text);
}
```

---

## Συμβουλές για Παραγωγική OCR

- **Επεξεργασία σε παρτίδες:** Τυλίξτε τον βρόχο αναγνώρισης σε `Parallel.ForEach` αλλά περιορίστε το degree of parallelism στον αριθμό των GPU streams που μπορείτε να διαθέσετε (συνήθως 1‑2 ανά κάρτα).
- **Καθαριότητα μνήμης:** Καλό είναι να διαγράφετε άμεσα τα αντικείμενα `OcrImage` (`receiptImage.Dispose()`), ειδικά όταν επεξεργάζεστε χιλιάδες αποδείξεις.
- **Καταγραφή:** Καταγράψτε το `ocrResult.Confidence` για κάθε γραμμή· χαμηλή εμπιστοσύνη μπορεί να ενεργοποιήσει διαδικασία χειροκίνητης ανασκόπησης.
- **Ασφάλεια:** Όταν χειρίζεστε ευαίσθητες αποδείξεις, αποθηκεύστε τα αρχεία εικόνας σε κρυπτογραφημένους προσωρινούς φακέλους και διαγράψτε τα μετά την επεξεργασία.

---

## Συμπέρασμα

Τώρα έχετε ένα **πλήρες, εκτελέσιμο παράδειγμα** που δείχνει πώς να **αναγνωρίσετε κείμενο από εικόνα** με την επιτάχυνση GPU του Aspose OCR, **load image for OCR**, **set GPU device ID**, και τέλος **extract text from receipt** σε λίγα σύντομα βήματα. Ο κώδικας είναι έτοιμος για αντιγραφή‑επικόλληση, και οι εξηγήσεις παρέχουν το απαραίτητο πλαίσιο για προσαρμογή σε πολυγλωσσικά, πολυ‑GPU ή υψηλής διαπερατότητας σενάρια.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να τροφοδοτήσετε μια ζωντανή ροή βίντεο στο `GpuOcrEngine` για πραγματικό‑χρόνο σάρωση αποδείξεων, ή ενσωματώστε το αποτέλεσμα σε ένα API λογιστικής. Ο ουρανός είναι το όριο όταν συνδυάζετε γρήγορο GPU OCR με καθαρό σχεδιασμό C#.

*Καλή προγραμματιστική, και ας είναι η OCR σας πάντα γρήγορη!* 

![recognize text from image demo screenshot](placeholder-image.png "recognize text from image example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}