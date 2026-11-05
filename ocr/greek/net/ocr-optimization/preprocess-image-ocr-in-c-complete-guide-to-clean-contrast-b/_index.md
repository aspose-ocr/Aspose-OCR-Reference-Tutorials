---
category: general
date: 2026-03-05
description: Προεπεξεργασία OCR εικόνας με το Aspose OCR για την αφαίρεση θορύβου
  εικόνας, την αύξηση της αντίθεσης, τη φόρτωση του αρχείου εικόνας και την εξαγωγή
  κειμένου OCR σε λίγα μόνο βήματα.
draft: false
keywords:
- preprocess image OCR
- remove image noise
- increase image contrast
- load image file
- extract OCR text
language: el
og_description: Μάθετε πώς να προεπεξεργάζεστε OCR εικόνας, να αφαιρείτε τον θόρυβο
  της εικόνας, να αυξάνετε την αντίθεση της εικόνας, να φορτώνετε αρχείο εικόνας και
  να εξάγετε κείμενο OCR με το Aspose OCR σε C#.
og_title: Προεπεξεργασία OCR εικόνας σε C# – Καθαρή εξαγωγή κειμένου με ενίσχυση αντίθεσης
tags:
- OCR
- C#
- Image Processing
title: Προεπεξεργασία OCR εικόνας σε C# – Πλήρης οδηγός για καθαρή εξαγωγή κειμένου
  με ενισχυμένη αντίθεση
url: /el/net/ocr-optimization/preprocess-image-ocr-in-c-complete-guide-to-clean-contrast-b/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προεπεξεργασία Image OCR – Καθαρή, Ενισχυμένη Αντίθεση Εξαγωγή Κειμένου σε C#

Έχετε ποτέ χρειαστεί να **preprocess image OCR** επειδή η πηγή της εικόνας είναι λοξομένη, θορυβώδης ή απλώς δύσκολη στην ανάγνωση; Δεν είστε μόνοι. Σε πολλά πραγματικά έργα—σκεφτείτε τη σάρωση αποδείξεων, την ψηφιοποίηση παλιών εγγράφων ή την τροφοδοσία δεδομένων σε μια αλυσίδα μηχανικής μάθησης—η ακατέργαστη εικόνα σπάνια βγαίνει τέλεια επεξεργασμένη.  

Το καλό νέο; Με μερικά έξυπνα φίλτρα μπορείτε να βελτιώσετε δραματικά τα ποσοστά αναγνώρισης. Σε αυτό το tutorial θα περάσουμε από τη φόρτωση ενός αρχείου εικόνας, την αφαίρεση θορύβου εικόνας, την αύξηση της αντίθεσης εικόνας και τελικά την εξαγωγή κειμένου OCR χρησιμοποιώντας το Aspose.OCR για .NET. Στο τέλος θα έχετε ένα έτοιμο προς εκτέλεση πρόγραμμα C# που παράγει καθαρό, αναγνώσιμο κείμενο από μια ακατάστατη εικόνα.

> **Γιατί να ασχοληθείτε με την προεπεξεργασία;**  
> Οι περισσότερες μηχανές OCR, συμπεριλαμβανομένου του Aspose OCR, υποθέτουν μια σχετικά καθαρή είσοδο. Ο θόρυβος, η χαμηλή αντίθεση ή η κλίση μπορούν να μειώσουν την ακρίβεια κατά 30 % ή περισσότερο. Η προεπεξεργασία αντιμετωπίζει αυτά τα προβλήματα πριν η μηχανή ακόμη δει την εικόνα.

---

## Τι Θα Χρειαστείτε

- **Aspose.OCR for .NET** (τελευταία έκδοση, π.χ., 23.10) – εγκατάσταση μέσω NuGet: `Install-Package Aspose.OCR`
- **.NET 6.0** ή νεότερο (ο κώδικας λειτουργεί και σε .NET Framework, αλλά το .NET 6 είναι η ιδανική επιλογή)
- Ένα δείγμα εικόνας, π.χ., `skewed_noisy.jpg`, τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε
- Μια μέτρια εμπειρία με C# – τίποτα περίπλοκο, απλώς η δυνατότητα εκτέλεσης μιας εφαρμογής κονσόλας

Καμία εξωτερική εργαλεία, καμία βαριά βιβλιοθήκη εικόνας, και απολύτως καμία μαγεία. Όλα ζουν μέσα στο πακέτο Aspose OCR.

## Υλοποίηση Βήμα‑Βήμα

Παρακάτω χωρίζουμε τη διαδικασία σε λογικά τμήματα. Κάθε τμήμα έχει ένα σαφές **γιατί** και μια συνοπτική **πώς**, ακολουθούμενο από ένα εκτελέσιμο απόσπασμα κώδικα.

### ## Βήμα 1: Φόρτωση Αρχείου Εικόνας και Αρχικοποίηση της Μηχανής OCR

> **Η κύρια λέξη-κλειδί εμφανίζεται εδώ:** *preprocess image OCR* ξεκινά με τη φόρτωση της πηγής.

```csharp
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

// Initialize the OCR engine with your license
var ocrEngine = new OcrEngine();
ocrEngine.SetLicense("Aspose.OCR.lic");

// Load the image you want to process
using var imageStream = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");

// Assign the image to the engine (still raw at this point)
ocrEngine.Image = imageStream;
```

**Εξήγηση**  
`ImageStream.FromFile` είναι ο πιο απλός τρόπος για **φόρτωση αρχείου εικόνας**. Η δήλωση `using` εγγυάται ότι το χειριστήριο του αρχείου απελευθερώνεται άμεσα. Σε αυτό το στάδιο η εικόνα παραμένει αμετάβλητη—τέλεια για την επίδειξη της επίδρασης των επόμενων φίλτρων.

### ## Βήμα 2: Αφαίρεση Θορύβου Εικόνας με Φίλτρο Denoise

Ο θόρυβος είναι ο σιωπηλός δολοφόνος της ακρίβειας OCR. Ένα κηλίδες φόντο μπορεί να μπερδέψει τη διαχωριστική διαδικασία χαρακτήρων.

```csharp
// Apply a denoise filter to clean up grainy pixels
imageStream.ApplyPreprocessing(new ImagePreprocessing[]
{
    new DenoiseFilter()
});
```

**Γιατί Denoise;**  
Το `DenoiseFilter` χρησιμοποιεί έναν αλγόριθμο βασισμένο στη διάμεσο που εξομαλύνει τα απομονωμένα pixel ενώ διατηρεί τις άκρες. Στην πράξη, θα δείτε λιγότερους λανθασμένα αναγνωρισμένους χαρακτήρες, ειδικά σε σαρώσεις χαμηλής ανάλυσης.

### ## Βήμα 3: Αύξηση Αντίθεσης Εικόνας με Φίλτρο Contrast‑Stretch

Η χαμηλή αντίθεση κάνει το σκούρο κείμενο να ενσωματώνεται στο φόντο. Η επέκταση της αντίθεσης διευρύνει το τόνικό εύρος, κάνοντας το μαύρο πραγματικά μαύρο και το λευκό πραγματικά λευκό.

```csharp
// Boost contrast to make text pop
imageStream.ApplyPreprocessing(new ImagePreprocessing[]
{
    new ContrastStretchFilter()
});
```

**Τι Συμβαίνει Κρυφά;**  
Το `ContrastStretchFilter` αντιστοιχίζει το πιο σκοτεινό 5 % των pixel σε καθαρό μαύρο και το πιο φωτεινό 5 % σε καθαρό λευκό, ενισχύοντας ουσιαστικά τη οπτική διαφορά μεταξύ προσκηνίου και φόντου.

### ## Βήμα 4: Διόρθωση Κλίσης Εικόνας (Προαιρετικό αλλά Συνιστάται)

Εάν η εικόνα σας είναι κλινή, οι χαρακτήρες γίνονται κεκλιμένοι και η μηχανή OCR μπορεί να χωρίσει τα γράμματα. Μια γρήγορη διόρθωση κλίσης ευθυγραμμίζει τη βάση του κειμένου.

```csharp
// Straighten a skewed image – optional but often vital
imageStream.ApplyPreprocessing(new ImagePreprocessing[]
{
    new DeskewFilter()
});
```

**Συμβουλή:**  
Εάν γνωρίζετε ότι οι εικόνες σας είναι ήδη ευθυγραμμισμένες, μπορείτε να παραλείψετε αυτό το βήμα για να εξοικονομήσετε μερικά χιλιοστά του δευτερολέπτου.

### ## Βήμα 5: Δυαδική Μετατροπή – Μετατροπή της Εικόνας σε Μαύρο‑Άσπρο

Η δυαδική μετατροπή απλοποιεί τα δεδομένα raster σε δύο χρώματα, κάτι που αγαπούν πολλές μηχανές OCR.

```csharp
// Convert to pure black‑and‑white pixels
imageStream.ApplyPreprocessing(new ImagePreprocessing[]
{
    new BinarizeFilter()
});
```

**Πότε να τη Χρησιμοποιήσετε;**  
Εάν η πηγή περιέχει χρωματιστά φόντα ή διαβαθμίσεις, η δυαδική μετατροπή αφαιρεί αυτές τις αποσπάσεις. Είναι ιδιαίτερα χρήσιμη μετά την επέκταση της αντίθεσης.

### ## Βήμα 6: Εκτέλεση OCR και Εξαγωγή Κειμένου

Τώρα ξεκινά η βαριά δουλειά—αναγνώριση χαρακτήρων από την καθαρισμένη εικόνα.

```csharp
// Run OCR on the pre‑processed image
var ocrResult = ocrEngine.Recognize();

// Output the extracted text to the console
Console.WriteLine("=== Extracted OCR Text ===");
Console.WriteLine(ocrResult.Text);
```

**Αναμενόμενη Έξοδος**  
Υποθέτοντας ότι η αρχική εικόνα περιείχε την πρόταση “Aspose OCR makes image processing easy.”, η κονσόλα θα πρέπει να εμφανίσει:

```
=== Extracted OCR Text ===
Aspose OCR makes image processing easy.
```

Εάν εξακολουθείτε να βλέπετε ακατανόητους χαρακτήρες, επανεξετάστε την αλυσίδα προεπεξεργασίας—ίσως η εικόνα χρειάζεται πιο ισχυρό επίπεδο denoise ή διαφορετικό όριο δυαδικής μετατροπής.

## Πλήρες Παράδειγμα Λειτουργίας

Αντιγράψτε‑επικολλήστε ολόκληρο το μπλοκ σε ένα νέο έργο κονσόλας (`dotnet new console -n OcrDemo`) και πατήστε **F5**. Βεβαιωθείτε ότι η διαδρομή `skewed_noisy.jpg` ταιριάζει με το περιβάλλον σας.

```csharp
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Step 1: Initialize OCR engine and load the image
        var ocrEngine = new OcrEngine();
        ocrEngine.SetLicense("Aspose.OCR.lic");

        using var imageStream = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
        ocrEngine.Image = imageStream;

        // Step 2‑5: Apply preprocessing filters
        imageStream.ApplyPreprocessing(new ImagePreprocessing[]
        {
            new DeskewFilter(),
            new DenoiseFilter(),
            new ContrastStretchFilter(),
            new BinarizeFilter()
        });

        // Step 6: Recognize and display text
        var ocrResult = ocrEngine.Recognize();
        Console.WriteLine("=== Extracted OCR Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Συμβουλή Pro:**  
> Τυλίξτε τον πίνακα προεπεξεργασίας σε μια μεταβλητή εάν σκοπεύετε να ενεργοποιείτε/απενεργοποιείτε φίλτρα βάσει συνθηκών χρόνου εκτέλεσης. Κρατά τον κώδικα τακτοποιημένο και κάνει το debugging πιο εύκολο.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

| Ερώτηση | Απάντηση |
|----------|--------|
| *Τι γίνεται αν η εικόνα μου είναι ήδη υψηλής αντίθεσης;* | Μπορείτε να παραλείψετε το `ContrastStretchFilter`. Η εκτέλεσή του σε μια τέλεια εικόνα δεν θα βλάψει, αλλά προσθέτει μια μικρή επιβάρυνση. |
| *Μπορώ να ρυθμίσω την ισχύ του φίλτρου denoise;* | Ναι. `new DenoiseFilter { Strength = 2 }` (η προεπιλογή είναι 1). Μεγαλύτερες τιμές αφαιρούν περισσότερα στίγματα αλλά μπορεί να θολώσουν λεπτομερείς λεπτομέρειες. |
| *Πώς να διαχειριστώ PDF με πολλαπλές σελίδες;* | Μετατρέψτε κάθε σελίδα σε εικόνα (π.χ., χρησιμοποιώντας Aspose.PDF), έπειτα περάστε κάθε εικόνα μέσω της ίδιας αλυσίδας προεπεξεργασίας. |
| *Υπάρχει τρόπος να λάβω βαθμολογίες εμπιστοσύνης;* | Το `ocrResult` περιέχει μια ιδιότητα `Confidence` ανά χαρακτήρα. Επανάληψη μέσω `ocrResult.Lines` για λεπτομερή πληροφορία. |
| *Τι γίνεται με γλώσσες εκτός των Αγγλικών;* | Ορίστε `ocrEngine.Language = OcrLanguage.French;` (ή οποιαδήποτε υποστηριζόμενη γλώσσα) πριν καλέσετε το `Recognize()`. |

## Συμπεράσματα

Μόλις **preprocess image OCR** από την αρχή μέχρι το τέλος: φόρτωση του αρχείου, **αφαίρεση θορύβου εικόνας**, **αύξηση αντίθεσης εικόνας**, διόρθωση κλίσης, δυαδική μετατροπή, και τελικά **εξαγωγή κειμένου OCR**. Η πλήρης λύση βρίσκεται σε ένα μόνο, εύκολο‑να‑διαβαστεί πρόγραμμα C#, και η προσέγγιση κλιμακώνεται για επεξεργασία δέσμης ή ενσωμάτωση σε μεγαλύτερες υπηρεσίες.

Επόμενα βήματα; Δοκιμάστε να αντικαταστήσετε το `DenoiseFilter` με το `GaussianBlurFilter` εάν οι εικόνες σας είναι θολές αντί για κηλίδες. Πειραματιστείτε με το `ThresholdFilter` εάν χρειάζεστε προσαρμοσμένο επίπεδο δυαδικής μετατροπής. Και φυσικά, εξερευνήστε τις προχωρημένες επιλογές του Aspose OCR όπως το `PageSegmentationMode` για διατάξεις πολλαπλών στηλών.

Καλό προγραμματισμό, και εύχομαι τα αποτελέσματα OCR σας να είναι κρυστάλλινα καθαρά!  

*Image illustrating the preprocessing pipeline*  
![ροή εργασίας προεπεξεργασίας image OCR](https://example.com/ocr-workflow.png "ροή εργασίας προεπεξεργασίας image OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}