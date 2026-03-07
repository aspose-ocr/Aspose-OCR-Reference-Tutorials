---
category: general
date: 2026-03-07
description: Μάθετε πώς να διορθώσετε την κλίση μιας εικόνας, να ενισχύσετε την αντίθεση
  και να εξάγετε κείμενο από σάρωση χρησιμοποιώντας το Aspose OCR. Εκτελέστε OCR σε
  εικόνα με ένα πλήρες παράδειγμα C# και φορτώστε την εικόνα για OCR εύκολα.
draft: false
keywords:
- how to deskew image
- extract text from scan
- how to boost contrast
- perform ocr on image
- load image for OCR
language: el
og_description: Μάθετε πώς να διορθώνετε την κλίση της εικόνας, να ενισχύετε την αντίθεση
  και να εξάγετε κείμενο από σάρωση χρησιμοποιώντας το Aspose OCR σε C#. Εκτελέστε
  OCR στην εικόνα με βήμα‑βήμα κώδικα.
og_title: Πώς να διορθώσετε την κλίση εικόνας και να εκτελέσετε OCR σε C# – Πλήρης
  οδηγός
tags:
- C#
- OCR
- Image Processing
title: Πώς να διορθώσετε την κλίση μιας εικόνας και να εκτελέσετε OCR σε C# – Πλήρης
  οδηγός
url: /el/net/ocr-optimization/how-to-deskew-image-and-run-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Διορθώσετε την Κλίση μιας Εικόνας και να Εκτελέσετε OCR σε C# – Πλήρης Οδηγός

Αν ποτέ αναρωτηθήκατε **πώς να διορθώσετε την κλίση μιας εικόνας** πριν εκτελέσετε OCR, βρίσκεστε στο σωστό μέρος. Σε αυτό το tutorial θα σας καθοδηγήσουμε στη βελτίωση της αντίθεσης, τη φόρτωση μιας εικόνας για OCR, και τελικά **την εξαγωγή κειμένου από τη σάρωση** με το Aspose OCR.  

Είτε ψηφιοποιείτε παλιές αποδείξεις, καθαρίζετε σαρωμένα συμβόλαια, ή απλώς χρειάζεστε έναν αξιόπιστο τρόπο για να διαβάσετε κείμενο από μια λοξή φωτογραφία, τα παρακάτω βήματα καλύπτουν όλα όσα χρειάζεστε. Χωρίς περιττές πληροφορίες—απλώς ένα λειτουργικό παράδειγμα που μπορείτε να αντιγράψετε‑επικολλήσετε στο Visual Studio.  

## Τι Θα Επιτύχετε

* Διορθώστε την κλίση έως 30° (αυτό είναι το **πώς να διορθώσετε την κλίση μιας εικόνας** μέρος).  
* Αυξήστε την αντίθεση της εικόνας για πιο καθαρά άκρα χαρακτήρων (**πώς να ενισχύσετε την αντίθεση**).  
* Φορτώστε την εικόνα σας στη μηχανή OCR (**φόρτωση εικόνας για OCR**).  
* Εκτελέστε τη διαδικασία αναγνώρισης και **εξάγετε κείμενο από τη σάρωση**.  

Όλα αυτά λειτουργούν με το πιο πρόσφατο πακέτο Aspose.OCR .NET NuGet (v23.11 τη στιγμή της συγγραφής).  

---

![Παράδειγμα Διόρθωσης Κλίσης Εικόνας](/images/deskew-example.png "πώς να διορθώσετε την κλίση μιας εικόνας")

*Η παραπάνω εικόνα δείχνει ένα σαρωμένο έγγραφο πριν και μετά τη διόρθωση κλίσης.*

## Προαπαιτούμενα

* .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.7+).  
* Visual Studio 2022 (ή οποιοδήποτε IDE C# προτιμάτε).  
* Πακέτο NuGet Aspose.OCR – εγκαταστήστε το μέσω `dotnet add package Aspose.OCR`.  

Αυτό είναι όλο. Χωρίς εξωτερικές υπηρεσίες, χωρίς κλειδιά API.

---

## Πώς να Διορθώσετε την Κλίση μιας Εικόνας με Aspose OCR

Το πρώτο που κάνουμε είναι να δημιουργήσουμε ένα **ImageProcessingPipeline** και να προσθέσουμε ένα `DeskewFilter`. Το φίλτρο εντοπίζει αυτόματα τη γωνία της κυρίαρχης γραμμής κειμένου και περιστρέφει την εικόνα πίσω στην οριζόντια θέση.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Build a pipeline – Deskew is the first filter
var processingPipeline = new ImageProcessingPipeline()
    .Add(new DeskewFilter { MaxAngle = 30 })   // how to deskew image up to 30°
    .Add(new DenoiseFilter { Level = DenoiseLevel.High }) // remove noise
    .Add(new ContrastBoostFilter { Strength = 1.5 })      // how to boost contrast
    .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize

// Attach the pipeline to the engine
ocrEngine.Settings.ImageProcessing = processingPipeline;
```

**Γιατί αυτό είναι σημαντικό:**  
Μια κλιμακωμένη σάρωση μπερδεύει τη μηχανή OCR επειδή οι χαρακτήρες δεν είναι πλέον ευθυγραμμισμένοι με τη βάση γραμμής. Το `DeskewFilter` αναλύει το ιστόγραμμα της εικόνας, βρίσκει τη γωνία και την περιστρέφει, βελτιώνοντας δραματικά την ακρίβεια αναγνώρισης.

> **Pro tip:** Αν γνωρίζετε ότι τα έγγραφά σας δεν υπερβαίνουν κλίση 15°, ορίστε `MaxAngle = 15` για να επιταχύνετε την επεξεργασία.

---

## Πώς να Ενισχύσετε την Αντίθεση για Καλύτερη Αναγνώριση

Μετά τη διόρθωση κλίσης, το επόμενο βήμα είναι να κάνετε το κείμενο πιο εμφανές. Το `ContrastBoostFilter` τεντώνει το εύρος έντασης των pixel, κάτι που είναι ιδιαίτερα χρήσιμο για ξεθωριασμένες εκτυπώσεις.

```csharp
// The ContrastBoostFilter is already in the pipeline above.
// You can tweak the Strength value (1.0 = no change, >1.0 = stronger boost)
.Add(new ContrastBoostFilter { Strength = 1.5 })
```

**Γιατί βοηθά:**  
Οι σάρωσες χαμηλής αντίθεσης παράγουν γκριζά χαρακτήρες που ο δυαδικοποιητής μπορεί να ερμηνεύσει ως φόντο. Η ενίσχυση της αντίθεσης κάνει τα σκοτεινά pixel πιο σκοτεινά και τα φωτεινά πιο φωτεινά, προσφέροντας στο επόμενο `BinarizationFilter` έναν πιο καθαρό καμβά.

---

## Εκτέλεση OCR στην Εικόνα – Φόρτωση του Αρχείου

Τώρα που η εικόνα έχει προεπεξεργαστεί, πρέπει να **φορτώσουμε την εικόνα για OCR**. Η Aspose προσφέρει ένα βολικό βοηθητικό `ImageStream.FromFile`.

```csharp
// Load the source image – replace the path with your own file
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
```

Αν η εικόνα σας βρίσκεται σε ροή (π.χ., ανεβάστηκε μέσω web API), μπορείτε να χρησιμοποιήσετε `ImageStream.FromStream(yourStream)` αντί αυτού. Η μηχανή δέχεται BMP, JPEG, PNG, TIFF και πολλά άλλα.

---

## Εκτέλεση της Διαδικασίας Αναγνώρισης και Εξαγωγή Κειμένου από τη Σάρωση

Με όλα συνδεδεμένα, η κλήση `Recognize()` κάνει το σκληρό έργο. Μετά την κλήση, το αναγνωρισμένο κείμενο είναι διαθέσιμο μέσω `ocrEngine.Text`.

```csharp
// Run OCR
ocrEngine.Recognize();

// Output the result
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrEngine.Text);
```

**Αναμενόμενη έξοδος** (παράδειγμα για απλό τιμολόγιο):

```
=== Extracted Text ===
Invoice #12345
Date: 03/05/2026
Total: $1,250.00
Thank you for your business!
```

Αν η έξοδος φαίνεται ακατάστατη, ελέγξτε ξανά τη σειρά του pipeline—πρώτα deskew, μετά denoise, ενίσχυση αντίθεσης και τέλος δυαδικοποίηση. Η αλλαγή της σειράς μπορεί να υποβαθμίσει τα αποτελέσματα.

---

## Συνηθισμένα Προβλήματα και Ακραίες Περιπτώσεις

| Πρόβλημα | Γιατί Συμβαίνει | Διόρθωση |
|----------|------------------|----------|
| **Κενό αποτέλεσμα** | Η εικόνα είναι πολύ σκοτεινή ή πολύ φωτεινή για τη προεπιλεγμένη μέθοδο δυαδικοποίησης. | Αυξήστε το `ContrastBoostFilter.Strength` ή μεταβείτε σε `BinarizationMethod.Otsu`. |
| **Μερικό κείμενο λείπει** | Υπάρχει θόρυβος μετά την αποθορυβοποίηση. | Χρησιμοποιήστε `DenoiseLevel.Medium` για πιο ήπιες εικόνες, ή προσθέστε δεύτερο `DenoiseFilter`. |
| **Λάθος κατεύθυνση περιστροφής** | Το έγγραφο έχει μικτή προσανατολισμό (π.χ., φωτογραφία μιας περιστρεφόμενης σελίδας). | Ορίστε χειροκίνητα `DeskewFilter.MaxAngle` χαμηλότερο και προ-περιστρέψτε την εικόνα με `ImageProcessor.Rotate`. |
| **Μείωση απόδοσης** | Μεγάλο όγκο εικόνων υψηλής ανάλυσης. | Μειώστε την ανάλυση των εικόνων (`ImageProcessor.Resize`) πριν το pipeline, ή επεξεργαστείτε παράλληλα (`Parallel.ForEach`). |

---

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Build image‑processing pipeline
        var processingPipeline = new ImageProcessingPipeline()
            .Add(new DeskewFilter { MaxAngle = 30 })                     // how to deskew image up to 30°
            .Add(new DenoiseFilter { Level = DenoiseLevel.High })       // remove high‑level noise
            .Add(new ContrastBoostFilter { Strength = 1.5 })            // how to boost contrast
            .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize image

        // 3️⃣ Attach pipeline to OCR settings
        ocrEngine.Settings.ImageProcessing = processingPipeline;

        // 4️⃣ Load the image you want to OCR
        // Replace the path with the location of your own file
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");

        // 5️⃣ Run the recognition engine
        ocrEngine.Recognize();

        // 6️⃣ Display the extracted text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrEngine.Text);
    }
}
```

Αποθηκεύστε το ως `Program.cs`, τρέξτε `dotnet run`, και παρακολουθήστε την κονσόλα να εκτυπώνει το αποτέλεσμα **εξαγωγής κειμένου από τη σάρωση**.  

---

## Επόμενα Βήματα & Σχετικά Θέματα

* **Batch processing** – Τυλίξτε τη λογική παραπάνω σε βρόχο για να επεξεργαστείτε δεκάδες αρχεία.  
* **Custom language packs** – Αν χρειάζεστε ανάγνωση μη‑λατινικών γραφών, φορτώστε ένα μοντέλο γλώσσας μέσω `ocrEngine.Settings.Language = OcrLanguage.ChineseSimplified;`.  
* **PDF output** – Συνδυάστε Aspose.PDF με OCR για να ενσωματώσετε αναζητήσιμο κείμενο απευθείας σε αρχείο PDF.  
* **Performance tuning** – Πειραματιστείτε με τη σειρά του `ImageProcessingPipeline`; μερικές φορές η αποθορυβοποίηση πριν το deskew δίνει ταχύτερα αποτελέσματα σε θορυβώδεις φωτογραφίες.  

Όλα αυτά βασίζονται στις βασικές έννοιες που καλύψαμε: **πώς να διορθώσετε την κλίση μιας εικόνας**, **πώς να ενισχύσετε την αντίθεση**, **φόρτωση εικόνας για OCR**, **εκτέλεση OCR στην εικόνα**, και τέλος **εξαγωγή κειμένου από τη σάρωση**.

---

## Συμπέρασμα

Δείξαμε μια πλήρη, έτοιμη για παραγωγή μέθοδο για **πώς να διορθώσετε την κλίση μιας εικόνας** και να εκτελέσετε OCR σε C#. Συνδυάζοντας ένα φίλτρο deskew, ένα βήμα αποθορυβοποίησης, μια ενίσχυση αντίθεσης και έναν δυαδικοποιητή, λαμβάνετε καθαρή είσοδο που επιτρέπει στο Aspose OCR να εξάγει αξιόπιστα **κείμενο από τη σάρωση**.  

Δοκιμάστε τον κώδικα, προσαρμόστε τις παραμέτρους των φίλτρων στα δικά σας έγγραφα, και θα δείτε πόσο γρήγορα βελτιώνεται η ακρίβεια αναγνώρισης. Έχετε ερωτήσεις; Αφήστε ένα σχόλιο, και καλή προγραμματιστική διασκέδαση!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}