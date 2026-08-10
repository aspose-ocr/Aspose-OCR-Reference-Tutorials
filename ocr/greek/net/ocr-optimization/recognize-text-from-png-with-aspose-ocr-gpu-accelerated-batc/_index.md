---
category: general
date: 2026-04-01
description: Μάθετε πώς να αναγνωρίζετε κείμενο από αρχεία PNG γρήγορα, ορίζοντας
  το αναγνωριστικό της συσκευής GPU και ενεργοποιώντας την επιτάχυνση GPU στο Aspose
  OCR. Οδηγός C# βήμα‑προς‑βήμα.
draft: false
keywords:
- recognize text from png
- set gpu device id
- Aspose OCR GPU
- batch OCR C#
- OCR performance tips
language: el
og_description: Αναγνωρίστε κείμενο από αρχεία PNG γρήγορα ορίζοντας το ID της συσκευής
  GPU. Ακολουθήστε αυτόν τον πλήρη οδηγό C# για να ενεργοποιήσετε την επιτάχυνση GPU
  με το Aspose OCR.
og_title: Αναγνώριση κειμένου από PNG – Οδηγός Aspose OCR με επιτάχυνση GPU
tags:
- C#
- OCR
- GPU
- Aspose
title: Αναγνώριση κειμένου από PNG με Aspose OCR – Παρουσίαση Μαζικής Επεξεργασίας
  με Επιτάχυνση GPU
url: /el/net/ocr-optimization/recognize-text-from-png-with-aspose-ocr-gpu-accelerated-batc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση κειμένου από PNG – Πλήρης C# GPU‑Επιταχυμένη Παρτίδα Εκπαίδευση

Κάποτε χρειάστηκε να **αναγνωρίσετε κείμενο από png** εικόνες αλλά βρήκατε τη διαδικασία εξαιρετικά αργή; Δεν είστε μόνοι. Οι περισσότεροι προγραμματιστές ξεκινούν με μια απλή κλήση OCR, μετά κοιτάζουν ένα τερματικό που προχωρά σαν σαλιγκάρι όταν ένας φάκελος περιέχει δεκάδες στιγμιότυπα οθόνης.  

Τα καλά νέα; Το Aspose OCR μπορεί να μεταφέρει το βαρέως βάρους στην κάρτα γραφικών σας, και με λίγες μόνο γραμμές μπορείτε να **ορίσετε το gpu device id** για να επιλέξετε την ακριβή GPU που θέλετε. Σε αυτόν τον οδηγό θα περάσουμε από ένα πλήρες, εκτελέσιμο παράδειγμα που παίρνει κάθε PNG από έναν φάκελο, ενεργοποιεί την επιτάχυνση GPU, επιλέγει την πρώτη GPU και εκτυπώνει τον αριθμό χαρακτήρων για κάθε αρχείο.

Στο τέλος θα έχετε ένα αυτόνομο πρόγραμμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε .NET project, και θα καταλάβετε γιατί η ενεργοποίηση της GPU είναι σημαντική, πώς να διαχειριστείτε τις ειδικές περιπτώσεις, και τι να ρυθμίσετε για ακόμη καλύτερη απόδοση.

## Τι Θα Χρειαστεί

- **.NET 6.0** ή νεότερο (ο κώδικας μεταγλωττίζεται επίσης με .NET Core).  
- Το **Aspose.OCR** πακέτο NuGet – εγκαταστήστε το με `dotnet add package Aspose.OCR`.  
- Ένα μηχάνημα με GPU συμβατό με CUDA (συνήθως NVIDIA) και τον κατάλληλο οδηγό.  
- Ένας φάκελος γεμάτος **PNG** εικόνες που θέλετε να επεξεργαστείτε.  

Αν κάτι από αυτά σας φαίνεται άγνωστο, μην πανικοβληθείτε. Τα παρακάτω βήματα περιλαμβάνουν τις ακριβείς εντολές που χρειάζεστε, και θα συζητήσουμε επίσης τι να κάνετε όταν δεν υπάρχει GPU.

## Βήμα 1: Αρχικοποίηση του OCR Engine και Ενεργοποίηση της GPU Επιτάχυνσης  

Το πρώτο που πρέπει να κάνετε είναι να δημιουργήσετε μια παρουσία `OcrEngine` και να ενεργοποιήσετε την υποστήριξη GPU. Αυτή η σημαία λέει στο Aspose να χρησιμοποιεί τις εγγενείς βιβλιοθήκες CUDA στο παρασκήνιο.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // Enable GPU acceleration – huge speed boost for large batches
        ocrEngine.UseGpuAcceleration = true;
```

**Γιατί είναι σημαντικό:** Χωρίς το `UseGpuAcceleration`, κάθε εικόνα επεξεργάζεται από την CPU, κάτι που μπορεί να είναι πολύ πιο αργό, ειδικά για PNG υψηλής ανάλυσης. Η ενεργοποίηση της σημαίας προετοιμάζει επίσης το engine να δεχτεί μια συγκεκριμένη συσκευή GPU αργότερα.

## Βήμα 2: Ορισμός του GPU Device ID (Προαιρετικό αλλά Συνιστώμενο)  

Αν ο σταθμός εργασίας σας έχει περισσότερες από μία GPU, μπορείτε να αποφασίσετε ποια θα χρησιμοποιήσετε. Τα IDs των συσκευών ξεκινούν από **0**, έτσι το `0` επιλέγει την πρώτη GPU, το `1` τη δεύτερη, κ.ο.κ.

```csharp
        // Optional: Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id
```

**Συμβουλή:** Όταν τρέχετε σε κοινόχρηστο server, ο καθορισμός του GPU device ID μπορεί να αποτρέψει την κλοπή πόρων από άλλες διεργασίες. Αν παραλείψετε αυτή τη γραμμή, το Aspose θα επιλέξει την προεπιλεγμένη συσκευή, κάτι που συνήθως είναι εντάξει για ρύθμιση με μία GPU.

## Βήμα 3: Συλλογή Όλων των PNG Αρχείων από το Φάκελο Παρτίδας  

Στη συνέχεια πρέπει να εντοπίσουμε κάθε PNG που θέλετε να επεξεργαστείτε με OCR. Η μέθοδος `Directory.GetFiles` κάνει το βαρέως βάρους.

```csharp
        // Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // <-- replace with your path
            "*.png",                  // only PNG files
            System.IO.SearchOption.TopDirectoryOnly);
```

**Ειδική περίπτωση:** Αν ο φάκελος είναι κενός, το `imageFiles` θα είναι ένας κενός πίνακας. Θα το διαχειριστούμε αργότερα με ένα φιλικό μήνυμα.

## Βήμα 4: Επεξεργασία Κάθε Εικόνας και Εκτύπωση του Αναγνωρισμένου Αριθμού Χαρακτήρων  

Τώρα ο κύριος βρόχος. Για κάθε PNG καλούμε το `Recognize`, μετά εκτυπώνουμε το όνομα του αρχείου και το μήκος του εξαγόμενου κειμένου.

```csharp
        // Verify we actually found files
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

**Τι θα δείτε:**  
```
invoice1.png → 342 chars
receipt_2023.png → 127 chars
screenshot.png → 0 chars
```

Αν μια εικόνα δεν περιέχει κείμενο, ο αριθμός θα είναι `0`. Αυτό είναι απολύτως φυσιολογικό για στιγμιότυπα οθόνης που είναι μόνο γραφικά.

## Βήμα 5: Εκτέλεση του Προγράμματος και Επαλήθευση της Χρήσης GPU  

Συγκεντρώστε το αρχείο (`dotnet build`) και τρέξτε το (`dotnet run`). Καθώς το τερματικό κυλάει, μπορείτε να ανοίξετε το εργαλείο παρακολούθησης GPU (όπως το NVIDIA Smi) για να δείτε την ξαφνική αύξηση χρήσης GPU για κάθε εικόνα. Αν δεν δείτε καμία δραστηριότητα, ελέγξτε ξανά ότι:

1. Ο οδηγός CUDA είναι εγκατεστημένος.  
2. `UseGpuAcceleration` είναι ορισμένο σε `true`.  
3. Το σωστό `GpuDeviceId` ταιριάζει με μια φυσική GPU.

Αν η GPU δεν είναι διαθέσιμη, το Aspose θα επιστρέψει αυτόματα στην CPU, αλλά θα χάσετε το πλεονέκτημα ταχύτητας.

## Συνηθισμένες Παραλλαγές & Συμβουλές  

| Κατάσταση | Τι να Αλλάξετε |
|-----------|----------------|
| **Διαφορετική μορφή εικόνας** (π.χ., JPEG) | Αλλάξτε το μοτίβο αναζήτησης σε `*.jpg` ή `*.*` και το Aspose θα αναγνωρίσει ακόμη το κείμενο. |
| **Το μέγεθος παρτίδας είναι τεράστιο** (χίλια αρχεία) | Επεξεργαστείτε σε τμήματα για να αποφύγετε την πίεση μνήμης: χωρίστε το `imageFiles` σε μικρότερους πίνακες. |
| **Χρειάζεστε το πραγματικό κείμενο, όχι μόνο το μήκος** | Αντικαταστήστε το `ocrResult.Text.Length` με `ocrResult.Text` στην `WriteLine`. |
| **Εκτέλεση σε headless server** | Βεβαιωθείτε ότι ο server έχει οδηγό GPU· διαφορετικά, ορίστε `UseGpuAcceleration = false` για να αποφύγετε περιττά σφάλματα. |
| **Πολλαπλές GPU, θέλετε εξισορρόπηση φορτίου** | Κάντε βρόχο πάνω στο `ocrEngine.GpuDeviceId = i % gpuCount` μέσα στο `foreach` για να εναλλάσσετε τις συσκευές. |

## Αναμενόμενο Αποτέλεσμα & Επαλήθευση  

Όταν όλα λειτουργούν, το τερματικό εκτυπώνει το όνομα κάθε αρχείου ακολουθούμενο από τον αριθμό χαρακτήρων, όπως φαίνεται παραπάνω. Για να ελέγξετε ξανά το πραγματικό αποτέλεσμα OCR, μπορείτε προσωρινά να εκτυπώσετε το κείμενο:

```csharp
Console.WriteLine($"{Path.GetFileName(imagePath)} → {ocrResult.Text}");
```

Απλώς θυμηθείτε να αφαιρέσετε ή να σχολιάσετε αυτή τη γραμμή για μεγάλες παρτίδες· η εκτύπωση χιλιάδων γραμμών μπορεί να κατακλύσει το τερματικό σας.

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine and enable GPU acceleration
        var ocrEngine = new OcrEngine();
        ocrEngine.UseGpuAcceleration = true;

        // Step 2: (Optional) Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id

        // Step 3: Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // replace with your folder path
            "*.png",
            System.IO.SearchOption.TopDirectoryOnly);

        // Guard clause if no files are found
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Step 4: Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

Αποθηκεύστε το ως `GpuBatchDemo.cs`, τρέξτε `dotnet add package Aspose.OCR`, μετά `dotnet run`. Θα πρέπει να δείτε τους αριθμούς χαρακτήρων να εμφανίζονται σχεδόν άμεσα για κάθε PNG, χάρη στην επιτάχυνση GPU.

## Συμπέρασμα  

Τώρα ξέρετε πώς να **αναγνωρίζετε κείμενο από png** αρχεία αποδοτικά ενεργοποιώντας την επιτάχυνση GPU και ρητά **ορίζοντας το gpu device id** στο Aspose OCR. Το πλήρες, αντιγραφή‑και‑επικόλληση πρόγραμμα διαχειρίζεται την ανίχνευση φακέλου, ελέγχους ειδικών περιπτώσεων, και σας παρέχει άμεση ανατροφοδότηση για την απόδοση OCR.  

Επόμενα βήματα; Δοκιμάστε να αντικαταστήσετε την κλήση `Recognize` με `ocrEngine.RecognizeAsync` αν χρειάζεστε μη‑αποκλειστική επεξεργασία, ή πειραματιστείτε με διαφορετικές επιλογές προεπεξεργασίας εικόνας (π.χ., δυαδικοποίηση) που παρέχει το Aspose. Μπορείτε επίσης να διοχετεύσετε τα αποτελέσματα OCR σε μια βάση δεδομένων ή σε ευρετήριο αναζήτησης για λύση πλήρους κειμενικής αναζήτησης.  

Έχετε ερωτήσεις σχετικά με τη διαχείριση PDF πολλαπλών σελίδων, ή θέλετε να συγκρίνετε το Aspose OCR με το Tesseract; Αφήστε ένα σχόλιο ή εξερευνήστε τα άλλα μας tutorials για **batch OCR C#**, **συμβουλές απόδοσης OCR**, και **επεξεργασία εικόνας με GPU**. Καλό κώδικα!  

![Έξοδος κονσόλας που εμφανίζει τους αναγνωρισμένους αριθμούς χαρακτήρων για αρχεία PNG – αναγνώριση κειμένου από png με επιτάχυνση GPU](image-placeholder.png "παράδειγμα εξόδου αναγνώρισης κειμένου από png")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}