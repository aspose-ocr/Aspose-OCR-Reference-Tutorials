---
category: general
date: 2026-04-29
description: πώς να διορθώσετε την κλίση μιας εικόνας και να βελτιώσετε την ακρίβεια
  OCR με το Aspose OCR – μάθετε πώς να αφαιρέσετε τον θόρυβο, να ενισχύσετε την αντίθεση
  της εικόνας και να εξάγετε κείμενο από εικόνες.
draft: false
keywords:
- how to deskew image
- remove noise from image
- boost image contrast
- extract text from image
- improve ocr accuracy
language: el
og_description: πώς να διορθώσετε την κλίση μιας εικόνας και να βελτιώσετε την ακρίβεια
  του OCR. Αυτό το σεμινάριο δείχνει πώς να αφαιρέσετε τον θόρυβο από την εικόνα,
  να ενισχύσετε την αντίθεση της εικόνας και να εξάγετε κείμενο από την εικόνα χρησιμοποιώντας
  το Aspose OCR.
og_title: πώς να ευθυγραμμίσετε την εικόνα – Πλήρης Οδηγός Aspose OCR
tags:
- Aspose OCR
- C#
- Image preprocessing
title: πώς να διορθώσετε την κλίση της εικόνας – Οδηγός προεπεξεργασίας Aspose OCR
url: /el/net/ocr-optimization/how-to-deskew-image-aspose-ocr-preprocessing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# πώς να διορθώσετε την κλίση εικόνας – Πλήρης Οδηγός Aspose OCR

Έχετε αναρωτηθεί ποτέ **πώς να διορθώσετε την κλίση εικόνας** πριν τη δώσετε σε μια μηχανή OCR; Δεν είστε οι μόνοι. Μια λοξή σάρωση ή μια φωτογραφία τραβηγμένη υπό γωνία μπορεί να «σπάσει» την αναγνώριση κειμένου, αφήνοντάς σας με ακατάληπτο αποτέλεσμα.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από μια πλήρη, end‑to‑end λύση που όχι μόνο **πώς να διορθώσετε την κλίση εικόνας** αλλά και **να αφαιρέσετε το θόρυβο από την εικόνα**, **να ενισχύσετε την αντίθεση της εικόνας**, και τελικά **να εξάγετε κείμενο από την εικόνα** με το Aspose OCR. Στο τέλος θα δείτε πώς να **βελτιώσετε την ακρίβεια OCR** χωρίς να ψάχνετε στην τεκμηρίωση.

> **Τι θα πάρετε:** μια έτοιμη για εκτέλεση εφαρμογή C# console, μια σαφή εξήγηση κάθε βήματος προεπεξεργασίας, και μια σειρά πρακτικών συμβουλών που μπορείτε να αντιγράψετε‑επικολλήσετε στα δικά σας έργα.

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Core και .NET Framework)  
- Πακέτο NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- Ένα δείγμα εικόνας που είναι κεκλιμένο, θορυβώδες ή χαμηλής αντίθεσης (π.χ., `skewed_noisy.jpg`)  
- Visual Studio, VS Code, ή οποιοσδήποτε επεξεργαστής C# προτιμάτε  

Δεν απαιτούνται επιπλέον εγγενείς βιβλιοθήκες – το Aspose διαχειρίζεται τα πάντα εντός της διαδικασίας.

---

## Πώς να διορθώσετε την κλίση εικόνας με Aspose OCR

Το πρώτο που χρειαζόμαστε είναι ένα φίλτρο deskew που διορθώνει τη γωνία περιστροφής. Το Aspose OCR περιλαμβάνει το `FilterDeskew`, το οποίο αναλύει τις βάσεις κειμένου και περιστρέφει το bitmap ανάλογα.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this is the core object that will later recognize text.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Build an image‑processing pipeline.
        //    The order matters: deskew → denoise → contrast boost.
        ImageProcessingPipeline processingPipeline = new ImageProcessingPipeline();
        processingPipeline.Add(new FilterDeskew());          // ✅ how to deskew image
        processingPipeline.Add(new FilterDenoise());         // ✅ remove noise from image
        processingPipeline.Add(new FilterContrastBoost());   // ✅ boost image contrast

        // 3️⃣ Load your source picture.
        var sourceImage = OcrEngine.LoadImage(@"YOUR_DIRECTORY/skewed_noisy.jpg");

        // 4️⃣ Apply the pipeline – the image is now straight, cleaner, and sharper.
        var processedImage = processingPipeline.Apply(sourceImage);

        // 5️⃣ Run OCR on the cleaned‑up bitmap.
        var ocrResult = ocrEngine.Recognize(processedImage);

        // 6️⃣ Print the extracted text.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Γιατί ξεκινάμε με το deskew:**  
Αν οι γραμμές κειμένου δεν είναι οριζόντιες, η μηχανή OCR θα προσπαθήσει να ερμηνεύσει κεκλιμένους χαρακτήρες ως διαφορετικά glyphs, μειώνοντας δραματικά **βελτιώστε την ακρίβεια OCR**. Το deskew ευθυγραμμίζει τις βάσεις, δίνοντας στον αναγνωριστή έναν καθαρό καμβά.

> *Pro tip:* Αν γνωρίζετε εκ των προτέρων τη γωνία περιστροφής (π.χ., όλες οι σάρωσες είναι 90° λανθασμένες), μπορείτε να παραλείψετε το φίλτρο και να περιστρέψετε χειροκίνητα – είναι μια μικρή βελτίωση απόδοσης.

---

## Αφαίρεση θορύβου από την εικόνα – Καθαρισμός σάρωσης

Ο θόρυβος εμφανίζεται ως τυχαίες μαύρες ή λευκές κηλίδες (το κλασικό μοτίβο «αλάτι‑και‑πέπερ») και μπορεί να μπερδέψει τη διαχωριστική διαδικασία χαρακτήρων. Το `FilterDenoise` εφαρμόζει ένα median filter που εξομαλύνει αυτά τα σημεία διατηρώντας τις άκρες.

```csharp
// Inside the pipeline we already added FilterDenoise.
// If you need a custom strength, you can instantiate it like:
var denoise = new FilterDenoise { Strength = 2 }; // 1‑3 are typical values
processingPipeline.Add(denoise);
```

**Πότε να ρυθμίσετε τη δύναμη:**  
- **Strength = 1** – Ελαφρύς κόκκος, γρήγορη επεξεργασία.  
- **Strength = 3** – Πολύ θορυβώδεις σάρωσες (π.χ., fax έγγραφα).  

Η υπερβολική αύξηση της δύναμης μπορεί να θολώσει τα λεπτά στίγματα, κάτι που μπορεί να *βλάψει* **βελτιώστε την ακρίβεια OCR**. Δοκιμάστε μερικές τιμές σε ένα αντιπροσωπευτικό δείγμα.

---

## Ενίσχυση αντίθεσης εικόνας – Ανάδειξη αχνών χαρακτήρων

Οι εικόνες χαμηλής αντίθεσης (σκεφτείτε ξεθωριασμένες αποδείξεις) συχνά κάνουν τη μηχανή OCR να παραβλέπει ελαφρούς glyphs. Το `FilterContrastBoost` τεντώνει το ιστόγραμμα ώστε τα σκοτεινά pixel να γίνουν πιο σκοτεινά και τα φωτεινά πιο φωτεινά.

```csharp
var contrast = new FilterContrastBoost { ContrastLevel = 1.5f }; // 1.0 = no change
processingPipeline.Add(contrast);
```

**Γιατί η αντίθεση είναι σημαντική:**  
Μεγαλύτερη αντίθεση βελτιώνει το σήμα‑προς‑θόρυβο, καθιστώντας πιο εύκολο για τον νευρωνικό αναγνωριστή του Aspose να διακρίνει το “I” από το “l”. Ωστόσο, η υπερβολική ενίσχυση μπορεί να κορεστεί η εικόνα, μετατρέποντας ομαλές διαβαθμίσεις σε σκληρές άκρες που μοιάζουν με τεχνουργήματα. Στοχεύστε σε ισορροπία· 1.5‑2.0 είναι ένα καλό σημείο εκκίνησης.

---

## Εξαγωγή κειμένου από την εικόνα – Το τελικό βήμα OCR

Τώρα που η εικόνα είναι ευθεία, καθαρή και ζωντανή, η μηχανή OCR μπορεί να κάνει τη δουλειά της. Η μέθοδος `Recognize` επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει το ακατέργαστο κείμενο, βαθμολογίες εμπιστοσύνης, και ακόμη και τα bounding boxes αν τα χρειάζεστε.

```csharp
var ocrResult = ocrEngine.Recognize(processedImage);
Console.WriteLine(ocrResult.Text);
```

**Δείγμα εξόδου** (υποθέτοντας ότι η πηγή εικόνας περιέχει “Invoice #12345”):

```
=== OCR Output ===
Invoice #12345
Date: 04/28/2026
Total: $1,234.56
```

Αν δείτε ελλιπή χαρακτήρες, ελέγξτε ξανά τη γραμμή προεπεξεργασίας – ίσως η εικόνα χρειάζεται πιο ισχυρό denoise ή διαφορετικό επίπεδο αντίθεσης.  

> *Συχνή ερώτηση:* “Τι γίνεται αν χρειαστεί να αναγνωρίσω γλώσσα διαφορετική από τα Αγγλικά?”  
> Απλώς ορίστε `ocrEngine.Language = Language.English;` σε άλλη υποστηριζόμενη γλώσσα (π.χ., `Language.French`). Τα βήματα προεπεξεργασίας παραμένουν τα ίδια.

---

## Βελτίωση ακρίβειας OCR – Επιπλέον ρυθμίσεις

Ακόμη και με τέλεια γραμμή, μερικοί επιπλέον «knobs» μπορούν να προωθήσουν **βελτιώστε την ακρίβεια OCR** ακόμη περισσότερο:

| Συμβουλή | Πότε να χρησιμοποιηθεί | Πώς |
|-----|--------------|-----|
| **Binary Thresholding** | Πολύ σκοτεινές ή πολύ φωτεινές σάρωσες | `processingPipeline.Add(new FilterBinarize());` |
| **Resize Image** | Μικρές γραμματοσειρές (<10 pt) | `processedImage = OcrEngine.Resize(processedImage, 2.0);` |
| **Specify Character Set** | Γνωστό αλφάβητο (μόνο ψηφία κ.λπ.) | `ocrEngine.Characters = "0123456789";` |
| **Multi‑page PDFs** | Επεξεργασία δέσμης | Επανάληψη πάνω σε κάθε σελίδα και επαναχρησιμοποίηση της ίδιας pipeline. |

Θυμηθείτε: κάθε επιπλέον φίλτρο προσθέτει χρόνο επεξεργασίας, οπότε ενεργοποιήστε μόνο ό,τι πραγματικά χρειάζεστε.

---

## Πλήρες Παράδειγμα (Έτοιμο για Copy‑Paste)

Παρακάτω βρίσκεται ολόκληρο το πρόγραμμα, έτοιμο για μεταγλώττιση. Αντικαταστήστε το `YOUR_DIRECTORY` με το φάκελο που περιέχει το `skewed_noisy.jpg`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Build preprocessing pipeline
        ImageProcessingPipeline pipeline = new ImageProcessingPipeline();
        pipeline.Add(new FilterDeskew());                     // how to deskew image
        pipeline.Add(new FilterDenoise { Strength = 2 });    // remove noise from image
        pipeline.Add(new FilterContrastBoost { ContrastLevel = 1.8f }); // boost image contrast

        // Load source image
        var sourcePath = @"YOUR_DIRECTORY/skewed_noisy.jpg";
        var sourceImage = OcrEngine.LoadImage(sourcePath);

        // Apply pipeline
        var cleanImage = pipeline.Apply(sourceImage);

        // Perform OCR
        var result = ocrEngine.Recognize(cleanImage);

        // Output
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(result.Text);
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Καθαρό, ευθυγραμμισμένο κείμενο τυπωμένο στην κονσόλα, με πολύ λιγότερα λάθη αναγνώρισης σε σύγκριση με την άμεση χρήση του `ocrEngine.Recognize` πάνω στο ακατέργαστο αρχείο.

---

## Συμπέρασμα

Καλύψαμε **πώς να διορθώσετε την κλίση εικόνας**, πώς να **αφαιρέσετε θόρυβο από την εικόνα**, πώς να **ενισχύσετε την αντίθεση της εικόνας**, και τέλος πώς να **εξάγετε κείμενο από την εικόνα** χρησιμοποιώντας το Aspose OCR. Συνδυάζοντας αυτά τα φίλτρα θα δείτε μια αξιοσημείωτη άνοδο στην **βελτιώστε την ακρίβεια OCR**, ειδικά σε σάρωσες χαμηλής ποιότητας.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να τροφοδοτήσετε ένα multi‑page PDF στην ίδια pipeline, ή πειραματιστείτε με προσαρμοσμένα όρια για το binarization. Οι ίδιες αρχές ισχύουν – ευθυγραμμίστε, καθαρίστε, φωτίστε, και μετά αναγνωρίστε.

Έχετε ερωτήσεις ή κάποιο παράξενο edge case; Αφήστε ένα σχόλιο και ας το λύσουμε μαζί. Καλό coding!  

![how to deskew image example](deskew-example.png "how to deskew image example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}