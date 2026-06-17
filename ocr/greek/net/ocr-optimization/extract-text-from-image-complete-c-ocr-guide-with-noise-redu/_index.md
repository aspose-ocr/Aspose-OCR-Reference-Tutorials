---
category: general
date: 2026-02-25
description: Εξάγετε κείμενο από εικόνα χρησιμοποιώντας το Aspose OCR. Μάθετε πώς
  να φορτώνετε εικόνα για OCR, να εφαρμόζετε μείωση θορύβου και να βελτιώνετε την
  ακρίβεια του OCR με προεπεξεργασία.
draft: false
keywords:
- extract text from image
- apply noise reduction
- improve ocr accuracy
- load image for ocr
- preprocess ocr image
language: el
og_description: Εξάγετε κείμενο από εικόνα χρησιμοποιώντας το Aspose OCR. Αυτός ο
  οδηγός δείχνει πώς να φορτώσετε την εικόνα για OCR, να εφαρμόσετε μείωση θορύβου
  και να βελτιώσετε την ακρίβεια του OCR με προεπεξεργασία.
og_title: Εξαγωγή κειμένου από εικόνα – Πλήρης οδηγός OCR σε C#
tags:
- OCR
- C#
- Aspose
title: Εξαγωγή κειμένου από εικόνα – Πλήρης οδηγός OCR σε C# με μείωση θορύβου
url: /el/net/ocr-optimization/extract-text-from-image-complete-c-ocr-guide-with-noise-redu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Εικόνα – Πλήρης Οδηγός OCR σε C#

Έχετε χρειαστεί ποτέ να **εξάγετε κείμενο από εικόνα** και τα αποτελέσματα να είναι γεμάτα λάθη; Ίσως η φωτογραφία να ήταν ελαφρώς θολή, το φόντο θορυβώδες ή το κείμενο ελαφρώς κεκλιμένο. Από την εμπειρία μου, αυτές οι μικρές ατέλειες είναι οι κύριοι λόγοι για κακή ακρίβεια OCR. Τα καλά νέα; Με μερικά βήματα προεπεξεργασίας — όπως μείωση θορύβου και διόρθωση κλίσης — μπορείτε να **βελτιώσετε δραστικά την ακρίβεια OCR** χωρίς να αλλάξετε ούτε μία γραμμή κώδικα αναγνώρισης.

Σε αυτό το tutorial θα περάσουμε από ένα πραγματικό παράδειγμα που δείχνει πώς να **φορτώσετε εικόνα για OCR**, να δημιουργήσετε μια αλυσίδα **προεπεξεργασίας εικόνας OCR**, και τελικά να εξάγετε καθαρό κείμενο χρησιμοποιώντας το Aspose.OCR για .NET. Στο τέλος θα έχετε μια έτοιμη εφαρμογή κονσόλας C# που διαχειρίζεται θορυβώδεις, κεκλιμένες εικόνες σαν επαγγελματίας.

## Τι Θα Μάθετε

- Πώς να εγκαταστήσετε και να αναφέρετε τη βιβλιοθήκη Aspose.OCR.  
- Τον ακριβή κώδικα που χρειάζεται για **φόρτωση εικόνας για OCR** από δίσκο.  
- Πώς να **εφαρμόσετε μείωση θορύβου**, προσαρμοστικό κατώφλι και διόρθωση κλίσης σε ένα ενιαίο fluent φίλτρο.  
- Γιατί κάθε βήμα προεπεξεργασίας είναι σημαντικό για **βελτίωση της ακρίβειας OCR**.  
- Αναμενόμενη έξοδος στην κονσόλα και έναν γρήγορο τρόπο επαλήθευσης του αποτελέσματος.

> **Συμβουλή:** Αν είστε νέοι στο Aspose, η βιβλιοθήκη λειτουργεί με .NET 6+, .NET Framework 4.6+ και ακόμη και .NET Core. Δεν απαιτούνται επιπλέον εγγενείς εξαρτήσεις — μόνο ένα πακέτο NuGet.

---

## Προαπαιτούμενα

| Απαίτηση | Γιατί είναι σημαντική |
|----------|------------------------|
| .NET 6 SDK (ή νεότερο) | Σύγχρονα χαρακτηριστικά γλώσσας και καλύτερη απόδοση. |
| Visual Studio 2022 (ή VS Code) | Άνετο debugging και IntelliSense. |
| Aspose.OCR for .NET πακέτο NuGet | Παρέχει τα `OcrEngine`, `PreprocessFilter` και σχετικούς τύπους. |
| Δείγμα εικόνας (`noisy_skewed.jpg`) | Επιδεικνύει την επίδραση της προεπεξεργασίας. |

Αν έχετε ήδη ένα project, απλώς τρέξτε `dotnet add package Aspose.OCR` για να προσθέσετε τη βιβλιοθήκη.

---

## Βήμα 1 – Δημιουργία Νέου Project Κονσόλας

Πρώτα, δημιουργήστε μια νέα εφαρμογή κονσόλας ώστε να κρατήσουμε το παράδειγμα οργανωμένο.

```bash
dotnet new console -n AsposeOcrDemo
cd AsposeOcrDemo
dotnet add package Aspose.OCR
```

Αυτή η εντολή δημιουργεί ένα αρχείο `Program.cs` και προσθέτει το πακέτο OCR. Ανοίξτε το project στον αγαπημένο σας επεξεργαστή· θα αντικαταστήσουμε τη δημιουργημένη αυτόματα μέθοδο `Main` με μια πιο περιγραφική έκδοση.

---

## Βήμα 2 – Φόρτωση Εικόνας για OCR

Πριν μπορέσει να γίνει οποιαδήποτε αναγνώριση, η μηχανή χρειάζεται ένα ρεύμα εικόνας. Η μέθοδος `ImageStream.FromFile` διαχειρίζεται τις πιο κοινές μορφές (JPG, PNG, BMP). Ας την τυλίξουμε σε ένα `using` block ώστε ο χειριστής αρχείου να απελευθερώνεται αυτόματα.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 👉 Step 2: Load the raw image we want to process.
        // Replace the path with the location of your own test picture.
        ImageStream rawImage = ImageStream.FromFile("YOUR_DIRECTORY/noisy_skewed.jpg");

        // The rest of the pipeline follows…
        RunOcrPipeline(rawImage);
    }

    static void RunOcrPipeline(ImageStream rawImage)
    {
        // Placeholder – we’ll fill this in next.
    }
}
```

> **Γιατί είναι σημαντικό:** Η σωστή φόρτωση της εικόνας αποτελεί τη βάση. Αν το μονοπάτι του αρχείου είναι λανθασμένο, η μηχανή πετάει `FileNotFoundException` και δεν θα φτάσετε ποτέ στο στάδιο προεπεξεργασίας.

---

## Βήμα 3 – Δημιουργία Φίλτρου Προεπεξεργασίας (Μείωση Θορύβου + Περισσότερα)

Τώρα έρχεται η μαγεία. Ένα φίλτρο **preprocess OCR image** σας επιτρέπει να αλυσίδετε πολλαπλές λειτουργίες με fluent στυλ. Να γιατί κάθε βήμα είναι απαραίτητο:

1. **Adaptive Threshold** – Μετατρέπει την εικόνα σε ασπρόμαυρη βάση τοπικής αντίθεσης, βοηθώντας τη μηχανή OCR να διακρίνει χαρακτήρες από το φόντο.  
2. **Deskew** – Ανιχνεύει και διορθώνει τυχόν περιστροφή, εξασφαλίζοντας ότι οι γραμμές κειμένου είναι οριζόντιες. Κεκλιμένο κείμενο συχνά οδηγεί σε χαμένα χαρακτήρες.  
3. **Noise Reduction** – Αφαιρεί σπινθήρες, σκόνη ή τεχνουργήματα συμπίεσης που αλλιώς εμφανίζονται ως άσχετα pixel.

```csharp
static void RunOcrPipeline(ImageStream rawImage)
{
    // 👉 Step 3: Build a preprocessing filter that applies three operations.
    PreprocessFilter preprocessFilter = new PreprocessFilter()
        .ApplyAdaptiveThreshold()   // Enhance contrast for better binarization
        .ApplyDeskew()              // Correct any rotation in the image
        .ApplyNoiseReduction();     // Remove speckles and background noise

    // Execute the filter and get a cleaned image stream.
    ImageStream cleanedImage = preprocessFilter.Execute(rawImage);

    // Pass the cleaned image to the OCR engine.
    PerformRecognition(cleanedImage);
}
```

> **Pro tip:** Μπορείτε να αλλάξετε τη σειρά των κλήσεων, αλλά η παραπάνω σειρά (threshold → deskew → noise reduction) είναι γενικά η πιο αποτελεσματική, επειδή πρώτα διαχωρίζει το προσκήνιο από το φόντο, μετά ευθυγραμμίζει το κείμενο, και τέλος καθαρίζει τυχόν υπολειπόμενα τεχνουργήματα.

---

## Βήμα 4 – Εκτέλεση OCR και Εμφάνιση Αναγνωρισμένου Κειμένου

Με μια προεπεξεργασμένη εικόνα στα χέρια, το `OcrEngine` κάνει το σκληρό έργο. Η μηχανή επιλέγει αυτόματα το κατάλληλο μοντέλο γλώσσας (Αγγλικά από προεπιλογή) εκτός αν ορίσετε κάτι διαφορετικό.

```csharp
static void PerformRecognition(ImageStream image)
{
    // 👉 Step 4: Create the OCR engine and assign the cleaned image.
    OcrEngine ocrEngine = new OcrEngine
    {
        Image = image
    };

    // Run the recognition process.
    OcrResult result = ocrEngine.Recognize();

    // Output the extracted text to the console.
    Console.WriteLine("=== Extracted Text ===");
    Console.WriteLine(result.Text);
}
```

Όταν τρέξετε το πρόγραμμα (`dotnet run`), θα δείτε κάτι σαν:

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
```

Αν η αρχική σας εικόνα ήταν θορυβώδης, θα παρατηρήσετε πολύ λιγότερους ακατανόητους χαρακτήρες σε σύγκριση με το OCR πάνω στο ακατέργαστο αρχείο.

---

## Βήμα 5 – Πλήρες, Εκτελέσιμο Παράδειγμα

Συνδυάζοντας όλα τα κομμάτια, εδώ είναι ο **πλήρης κώδικας** που μπορείτε να αντιγράψετε‑επικολλήσετε στο `Program.cs`. Χωρίς ελλείψεις, χωρίς κρυφές εξαρτήσεις.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // Load the image you want to OCR.
        ImageStream rawImage = ImageStream.FromFile("YOUR_DIRECTORY/noisy_skewed.jpg");

        // Build and execute the preprocessing pipeline.
        PreprocessFilter preprocessFilter = new PreprocessFilter()
            .ApplyAdaptiveThreshold()
            .ApplyDeskew()
            .ApplyNoiseReduction();

        ImageStream cleanedImage = preprocessFilter.Execute(rawImage);

        // Run OCR on the cleaned image.
        OcrEngine ocrEngine = new OcrEngine
        {
            Image = cleanedImage
        };

        OcrResult result = ocrEngine.Recognize();

        // Show the extracted text.
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(result.Text);
    }
}
```

### Αναμενόμενη Έξοδος

Αν η πηγή εικόνα περιέχει τη φράση *«The quick brown fox jumps over the lazy dog.»* θα δείτε ακριβώς αυτή τη γραμμή εκτυπωμένη, χωρίς τυχαία σύμβολα ή ελλείποντα γράμματα. Αυτό είναι το χαρακτηριστικό της **βελτιωμένης ακρίβειας OCR** μετά την εφαρμογή μείωσης θορύβου και διόρθωσης κλίσης.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν η εικόνα μου είναι σε διαφορετική μορφή (π.χ., PNG);

Η `ImageStream.FromFile` ανιχνεύει αυτόματα τον τύπο αρχείου, οπότε μπορείτε να δείξετε σε ένα `.png` ή `.bmp` χωρίς αλλαγές κώδικα.

### Πώς διαχειρίζομαι πολυ‑σελίδες PDF;

Το Aspose.OCR μπορεί να επεξεργαστεί κάθε σελίδα ξεχωριστά. Κάντε βρόχο στα `PdfDocument.Pages`, μετατρέψτε κάθε σελίδα σε ρεύμα εικόνας, και τροφοδοτήστε το στο ίδιο pipeline προεπεξεργασίας.

### Μπορώ να αλλάξω το μοντέλο γλώσσας;

Ναι. Ορίστε `ocrEngine.Language = OcrLanguage.Spanish;` (ή οποιαδήποτε υποστηριζόμενη γλώσσα) πριν καλέσετε `Recognize()`.

### Τι γίνεται αν η εικόνα είναι ήδη καθαρή;

Μπορείτε να παραλείψετε τα βήματα που δεν χρειάζεστε. Για ένα τέλεια σαρωμένο έγγραφο, απλώς καλέστε `ApplyAdaptiveThreshold()` ή ακόμη και παραλείψτε το φίλτρο εντελώς — το OCR θα λειτουργήσει, αν και ίσως χάσετε μικρές βελτιώσεις.

---

## Pro Tips για Παραγωγική Χρήση OCR

- **Batch Processing:** Τυλίξτε το pipeline σε `Parallel.ForEach` όταν επεξεργάζεστε δεκάδες εικόνες για να αξιοποιήσετε πολλούς πυρήνες CPU.  
- **Διαχείριση Μνήμης:** Καλείτε `Dispose()` στα αντικείμενα `ImageStream` μετά τη χρήση (`rawImage.Dispose();`) για άμεση απελευθέρωση εγγενών πόρων.  
- **Logging:** Καταγράψτε το `ocrResult.Text` μαζί με το αρχικό όνομα αρχείου για ιχνηλασιμότητα.  
- **Error Handling:** Περιβάλλετε όλη τη ροή με `try/catch` και καταγράψτε τις λεπτομέρειες του `OcrException`; συχνά περιέχουν ενδείξεις για μη υποστηριζόμενες μορφές εικόνας.

---

## Συμπέρασμα

Μόλις **εξάγαμε κείμενο από εικόνα** χρησιμοποιώντας το Aspose.OCR, δείξαμε πώς να **φορτώσουμε εικόνα για OCR**, και αποδείξαμε γιατί η **εφαρμογή μείωσης θορύβου** (μαζί με thresholding και deskew) είναι η μυστική σάλτσα για **βελτίωση της ακρίβειας OCR**. Η ολοκληρωμένη λύση χωράει σε ένα μόνο, εύκολο‑να‑διαβάσει αρχείο C#, και μπορείτε να το ενσωματώσετε σε οποιοδήποτε project .NET αύριο.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε διαφορετική γλώσσα, πειραματιστείτε με προσαρμοσμένα φίλτρα, ή επεξεργαστείτε μια δέσμη σαρωμένων τιμολογίων μέσω του ίδιου pipeline. Οι έννοιες που μάθατε — προεπεξεργασία, καθαρά ρεύματα εικόνας, και στιβαρός χειρισμός σφαλμάτων — ισχύουν σε όλα τα σενάρια OCR.

Έχετε ερωτήσεις ή εντοπίσατε κάποια ασυνήθιστη περίπτωση; Αφήστε ένα σχόλιο παρακάτω· θα χαρώ να σας βοηθήσω να βελτιώσετε τη ροή εργασίας. Καλό coding, και εύχομαι το OCR σας να είναι πάντα kristall‑καθαρό! 

![Διάγραμμα που δείχνει το pipeline προεπεξεργασίας OCR – εξαγωγή κειμένου από εικόνα μετά τη μείωση θορύβου, προσαρμοστικό κατώφλι και διόρθωση κλίσης](extract-text-from-image-ocr-pipeline.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}