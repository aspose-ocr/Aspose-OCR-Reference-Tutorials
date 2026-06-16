---
category: general
date: 2026-02-17
description: Εκτελέστε OCR σε εικόνα χρησιμοποιώντας το Aspose OCR σε C#. Μάθετε πώς
  να εξάγετε κείμενο από jpg, να προεπεξεργαστείτε την εικόνα για OCR και να φορτώσετε
  την εικόνα για OCR με βήμα‑βήμα κώδικα.
draft: false
keywords:
- run OCR on image
- extract text from jpg
- preprocess image for OCR
- load image for OCR
language: el
og_description: Εκτελέστε OCR σε εικόνα χρησιμοποιώντας το Aspose OCR σε C#. Αυτός
  ο οδηγός δείχνει πώς να εξάγετε κείμενο από jpg, να προεπεξεργαστείτε την εικόνα
  και να τη φορτώσετε για OCR.
og_title: Εκτελέστε OCR σε εικόνα με το Aspose OCR – Πλήρης οδηγός C#
tags:
- Aspose OCR
- C#
- Image Processing
title: Εκτέλεση OCR σε εικόνα με το Aspose OCR – Πλήρης οδηγός C#
url: /el/net/text-recognition/run-ocr-on-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε εικόνα με Aspose OCR – Πλήρης οδηγός C# 

Έχετε ποτέ χρειαστεί να **run OCR on image** αρχεία αλλά δεν ήξερες από πού να ξεκινήσεις; Σε πολλές πραγματικές εφαρμογές – σκεφτείτε σαρωτές τιμολογίων ή παρακολούθηση αποδείξεων – το πρώτο εμπόδιο είναι η απόκτηση αξιόπιστου κειμένου από ένα JPEG. Τα καλά νέα; Με το Aspose OCR μπορείτε να **run OCR on image** αρχεία με λίγες γραμμές κώδικα C#, και θα μάθετε επίσης πώς να **extract text from jpg**, **preprocess image for OCR**, και **load image for OCR** χωρίς να ψάχνετε σε διάσπαρτη τεκμηρίωση. 

Σε αυτόν τον οδηγό θα περάσουμε από ένα πλήρες, έτοιμο για αντιγραφή‑και‑επικόλληση παράδειγμα που δείχνει ακριβώς πώς να ρυθμίσετε το engine, να προσθέσετε χρήσιμα φίλτρα προεπεξεργασίας, να τροφοδοτήσετε μια εικόνα στον αναγνωριστή και να εκτυπώσετε το αποτέλεσμα στην κονσόλα. Στο τέλος θα έχετε ένα αυτόνομο πρόγραμμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET και να αρχίσετε αμέσως να εξάγετε κείμενο από εικόνες. 

## Τι θα χρειαστείτε

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί και σε .NET Core)  
- Πακέτο NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- Ένα δείγμα JPEG (`input.jpg`) τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε  
- Βασική κατανόηση της σύνταξης C# (τίποτα εξωπραγματικό)  

Αν έχετε ήδη αυτά τα στοιχεία, υπέροχα – ας βουτήξουμε. Αν όχι, κατεβάστε το πακέτο NuGet και μια δοκιμαστική εικόνα· το υπόλοιπο του οδηγού υποθέτει ότι το έχετε κάνει. 

## Βήμα 1: Δημιουργία του OCR Engine – Ο πυρήνας της εκτέλεσης OCR σε εικόνα

Το πρώτο που πρέπει να κάνετε για να **run OCR on image** δεδομένα είναι να δημιουργήσετε ένα αντικείμενο `OcrEngine`. Αυτό το αντικείμενο περιέχει όλες τις ρυθμίσεις και την κατάσταση που απαιτούνται για την αναγνώριση. 

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessExample
{
    static void Main()
    {
        // Step 1 – create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **Γιατί αυτό είναι σημαντικό:** Το `OcrEngine` είναι η πύλη στο pipeline αναγνώρισης της Aspose. Χωρίς αυτό δεν μπορείτε να έχετε πρόσβαση στα φίλτρα, τα πακέτα γλώσσας ή στη μέθοδο `Recognize`. 

## Βήμα 2: Προσθήκη φίλτρων προεπεξεργασίας – Βελτιώστε την ακρίβεια όταν **extract text from jpg**

Οι εικόνες που βγάζονται απευθείας από μια κάμερα σπάνια είναι τέλειες. Λανθασμένες γωνίες ή τυχαίος θόρυβος μπορούν να μπλοκάρουν ακόμη και τα καλύτερα αλγόριθμα OCR. Η προσθήκη μερικών φίλτρων πριν κάνετε **extract text from jpg** μπορεί να βελτιώσει δραστικά τα αποτελέσματα. 

```csharp
        // Step 2 – add preprocessing filters
        // Deskew corrects rotation; DenoiseGaussian reduces visual noise
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseGaussianFilter { Sigma = 1.5 });
```

> **Pro tip:** Αν οι πηγαίες εικόνες είναι ήδη καθαρές, μπορείτε να παραλείψετε το `DenoiseGaussianFilter`. Πάρα πολύ ομαλοποίηση μπορεί να διαγράψει αδύναμα χαρακτήρες. 

## Βήμα 3: Φόρτωση εικόνας για OCR – Τροφοδοτώντας το Engine με το JPEG

Τώρα έρχεται το τμήμα όπου **load image for OCR**. Η Aspose παρέχει μια βολική βοηθητική μέθοδο `ImageStream.FromFile` που τυλίγει μια διαδρομή αρχείου σε ροή που καταλαβαίνει το engine. 

```csharp
        // Step 3 – specify the path to the JPEG you want to process
        var imagePath = @"YOUR_DIRECTORY/input.jpg";

        // Load the image and run OCR in one call
        var ocrResult = ocrEngine.Recognize(ImageStream.FromFile(imagePath));
```

> **Edge case:** Αν το αρχείο δεν υπάρχει, το `FromFile` πετάει μια `FileNotFoundException`. Τυλίξτε την κλήση σε try/catch αν περιμένετε ελλιπή αρχεία κατά την εκτέλεση. 

## Βήμα 4: Ανάκτηση και εμφάνιση του αναγνωρισμένου κειμένου

Τέλος, όταν το engine ολοκληρώσει, μπορείτε να αποκτήσετε το αποτέλεσμα plain‑text μέσω της ιδιότητας `Text`. Η εκτύπωση στην κονσόλα αρκεί για μια γρήγορη επίδειξη, αλλά μπορείτε επίσης να το γράψετε σε βάση δεδομένων ή σε αρχείο κειμένου. 

```csharp
        // Step 4 – output the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Αναμενόμενο αποτέλεσμα**  

```
=== OCR Result ===
Invoice #12345
Date: 02/15/2026
Total: $1,234.56
```

Το ακριβές περιεχόμενο θα εξαρτηθεί από την εικόνα που θα τροφοδοτήσετε, αλλά θα πρέπει να δείτε ένα ωραία μορφοποιημένο μπλοκ κειμένου αντί για ακατανόητο. 

![Διάγραμμα που δείχνει το pipeline OCR – run OCR on image, preprocess, load, recognize](/images/ocr-pipeline.png "διάγραμμα pipeline εκτέλεσης OCR σε εικόνα")

### Γιατί κάθε βήμα είναι σημαντικό

| Βήμα | Σκοπός | Τι συμβαίνει αν παραληφθεί |
|------|--------|----------------------------|
| **Create engine** | Αρχικοποιεί τις εσωτερικές δομές | Δεν υπάρχει διαθέσιμο recognizer – θα λάβετε `NullReferenceException`. |
| **Add filters** | Βελτιώνει την ακρίβεια διορθώνοντας την περιστροφή και το θόρυβο | Καμπυλωτές ή θορυβώδεις εικόνες παράγουν ακατάληπτο αποτέλεσμα. |
| **Load image** | Παρέχει το ακατέργαστο bitmap στο engine | Το engine δεν έχει τίποτα να επεξεργαστεί, με αποτέλεσμα ένα κενό πεδίο `Text`. |
| **Read result** | Αποκτά τη συμβολοσειρά plain‑text για περαιτέρω χρήση | Έχετε εκτελέσει OCR αλλά δεν βλέπετε ποτέ το αποτέλεσμα – δεν είναι πολύ χρήσιμο! |

## Κοινές παραλλαγές & πώς να προσαρμόσετε τη διαδικασία

### Αλλαγή του πακέτου γλώσσας

Η Aspose OCR υποστηρίζει πολλαπλές γλώσσες έτοιμες προς χρήση. Αν χρειάζεται να **run OCR on image** αρχεία που περιέχουν, π.χ., γαλλικό ή γερμανικό κείμενο, ορίστε την ιδιότητα `Language` πριν καλέσετε το `Recognize`. 

```csharp
ocrEngine.Language = OcrLanguage.French;
```

### Διαχείριση PDF πολλαπλών σελίδων

Αν η πηγή σας είναι PDF πολλαπλών σελίδων αντί για ένα μόνο JPEG, μπορείτε πρώτα να μετατρέψετε κάθε σελίδα σε εικόνα (χρησιμοποιώντας Aspose.PDF) και στη συνέχεια να τροφοδοτήσετε κάθε εικόνα στο ίδιο pipeline. Η επανάληψη πάνω στις σελίδες είναι απλή: 

```csharp
foreach (var pageImage in pdfPagesAsImages)
{
    var result = ocrEngine.Recognize(ImageStream.FromMemory(pageImage));
    Console.WriteLine(result.Text);
}
```

### Αντιμετώπιση μεγάλων αρχείων

Κατά την επεξεργασία εικόνων υψηλής ανάλυσης, η κατανάλωση μνήμης μπορεί να αυξηθεί απότομα. Σκεφτείτε να μειώσετε την ανάλυση της εικόνας πριν κάνετε **load image for OCR**: 

```csharp
using Aspose.Imaging;
using Aspose.Imaging.ImageOptions;

var loadOptions = new JpegLoadOptions { Width = 1024, Height = 768 };
using (var img = (Image)Image.Load(imagePath, loadOptions))
{
    var stream = new MemoryStream();
    img.Save(stream, new JpegOptions());
    var ocrResult = ocrEngine.Recognize(ImageStream.FromMemory(stream.ToArray()));
}
```

## Πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα

Παρακάτω είναι το πλήρες πρόγραμμα που ενσωματώνει όλα όσα συζητήσαμε. Αντιγράψτε‑και‑επικολλήστε το σε ένα νέο έργο κονσόλας, αντικαταστήστε το `YOUR_DIRECTORY` με το φάκελο που περιέχει το `input.jpg`, και πατήστε **F5**. 

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessExample
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Add useful preprocessing filters
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseGaussianFilter { Sigma = 1.5 });

        // 3️⃣ Load the JPEG you want to process
        var imagePath = @"YOUR_DIRECTORY/input.jpg";

        try
        {
            // Recognize text – this is where we actually run OCR on image
            var ocrResult = ocrEngine.Recognize(ImageStream.FromFile(imagePath));

            // 4️⃣ Print the extracted text
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error processing image: {ex.Message}");
        }
    }
}
```

### Επαλήθευση του αποτελέσματος

1. Εκτελέστε το πρόγραμμα.  
2. Ελέγξτε την κονσόλα – θα πρέπει να δείτε το κείμενο που υπήρχε στο `input.jpg`.  
3. Αν το αποτέλεσμα φαίνεται παραμορφωμένο, δοκιμάστε να ρυθμίσετε την τιμή `Sigma` στο `DenoiseGaussianFilter` ή προσθέστε επιπλέον φίλτρα όπως το `ContrastEnhancementFilter`. 

## Ανακεφαλαίωση & επόμενα βήματα

Μόλις καλύψαμε πώς να **run OCR on image** αρχεία χρησιμοποιώντας Aspose OCR, από τη ρύθμιση του engine μέχρι την παροχή καθαρού, αναγνώσιμου κειμένου. Τα βασικά σημεία:

- Δημιουργήστε μια παρουσία του `OcrEngine`.  
- **Preprocess image for OCR** με φίλτρα όπως `DeskewFilter` και `DenoiseGaussianFilter`.  
- **Load image for OCR** χρησιμοποιώντας `ImageStream.FromFile`.  
- Καλέστε `Recognize` και διαβάστε `ocrResult.Text` για να **extract text from jpg**.  

Θέλετε να προχωρήσετε παραπέρα; Δοκιμάστε αυτές τις ιδέες:

- **Batch processing** – διαβάστε έναν φάκελο JPEG και εξάγετε το αποτέλεσμα σε ξεχωριστό αρχείο `.txt` για κάθε εικόνα.  
- **Integrate with Azure Blob Storage** – τραβήξτε εικόνες από το cloud, εκτελέστε OCR, και αποθηκεύστε το κείμενο ξανά.  
- **Combine with NLP** – τροφοδοτήστε το εξαγόμενο κείμενο σε μοντέλο κατανόησης γλώσσας για αυτόματη κατηγοριοποίηση τιμολογίων.  

Νιώστε ελεύθεροι να πειραματιστείτε με διαφορετικούς συνδυασμούς φίλτρων, πακέτα γλώσσας, ή ακόμη και να μεταβείτε σε PNG και TIFF – το ίδιο pipeline λειτουργεί εφόσον **load image for OCR** γίνεται σωστά. 

---

Αν αντιμετωπίσατε προβλήματα, αφήστε ένα σχόλιο παρακάτω ή ελέγξτε την τεκμηρίωση Aspose OCR για προχωρημένες ρυθμίσεις. Καλή προγραμματιστική δουλειά και απολαύστε τη μετατροπή εικόνων σε αναζητήσιμο κείμενο! 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}