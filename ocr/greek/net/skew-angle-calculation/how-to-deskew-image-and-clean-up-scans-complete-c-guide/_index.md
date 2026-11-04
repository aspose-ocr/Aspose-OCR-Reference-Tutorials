---
category: general
date: 2026-03-18
description: Πώς να διορθώσετε την κλίση της εικόνας και να μειώσετε τον θόρυβο σε
  σαρωμένα αρχεία. Μάθετε πώς να φορτώνετε εικόνα από αρχείο, να εξάγετε κείμενο από
  TIFF και να αναγνωρίζετε κείμενο από εικόνα με το Aspose OCR.
draft: false
keywords:
- how to deskew image
- how to reduce noise
- recognize text from image
- load image from file
- extract text from tiff
language: el
og_description: Πώς να διορθώσετε την κλίση μιας εικόνας γρήγορα χρησιμοποιώντας το
  Aspose OCR. Αυτός ο οδηγός σας δείχνει πώς να μειώσετε τον θόρυβο, να φορτώσετε
  εικόνα από αρχείο και να εξάγετε κείμενο από TIFF σε C#.
og_title: Πώς να διορθώσετε την κλίση εικόνας – Πλήρες σεμινάριο OCR σε C#
tags:
- OCR
- C#
- Image Processing
title: Πώς να διορθώσετε την κλίση εικόνας και να καθαρίσετε τις σαρώσεις – Πλήρης
  οδηγός C#
url: /el/net/skew-angle-calculation/how-to-deskew-image-and-clean-up-scans-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Διορθώσετε την Κλίση Εικόνας – Πλήρης Οδηγός OCR σε C#

Έχετε αναρωτηθεί ποτέ **πώς να διορθώσετε την κλίση μιας εικόνας** που φαίνεται σαν να έχει ληφθεί από έναν ασταθή σαρωτή; Δεν είστε μόνοι. Οι περισσότεροι προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν το αρχικό TIFF είναι λίγο στραβό και τα αποτελέσματα του OCR γίνονται ακατάστατα. Τα καλά νέα; Με μερικές γραμμές C# μπορείτε να ευθυγραμμίσετε την εικόνα, να αφαιρέσετε το θολό φόντο και να εξάγετε καθαρό, αναζητήσιμο κείμενο απευθείας από το αρχείο.

Σε αυτόν τον οδηγό θα περάσουμε από το **πώς να μειώσουμε τον θόρυβο**, **πώς να φορτώσουμε εικόνα από αρχείο**, και τελικά **πώς να αναγνωρίσουμε κείμενο από εικόνα** χρησιμοποιώντας το Aspose OCR. Στο τέλος θα μπορείτε να **εξάγετε κείμενο από αρχεία tiff** χωρίς καμία δυσκολία.

> **Pro tip:** Αν ήδη χρησιμοποιείτε το Aspose OCR για άλλα έργα, μπορείτε να ενσωματώσετε αυτά τα φίλτρα χωρίς επιπλέον προβλήματα αδειοδότησης.

---

## Τι Θα Χρειαστείτε

- .NET 6 ή νεότερο (ο κώδικας λειτουργεί και σε .NET Core)  
- Πακέτο NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- Σαρωμένο TIFF που είναι ελαφρώς περιστραμμένο ή θορυβώδες (θα χρησιμοποιήσουμε το `skewed_scanned_doc.tif` ως παράδειγμα)  
- Ένας επεξεργαστής κειμένου ή IDE (Visual Studio, VS Code, Rider – διαλέξτε το αγαπημένο σας)

Δεν απαιτούνται πρόσθετες βιβλιοθήκες· τα φίλτρα που θα χρησιμοποιήσουμε είναι ενσωματωμένα στο Aspose OCR.

## Βήμα 1 – Δημιουργία του OCR Engine (Πώς να Διορθώσετε την Κλίση Εικόνας)

Το πρώτο που κάνετε είναι να δημιουργήσετε ένα `OcrEngine`. Σκεφτείτε το ως τον εγκέφαλο που θα διαβάσει αργότερα τους χαρακτήρες για εσάς.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Initialize the OCR engine – this object holds all settings
        var ocrEngine = new OcrEngine();
```

Γιατί να δημιουργήσετε τον engine εκ των προτέρων; Σας παρέχει ένα ενιαίο σημείο για την προσθήκη φίλτρων προεπεξεργασίας, πακέτων γλώσσας και επιλογών εξόδου. Αν παραλείψετε αυτό το βήμα και καλέσετε απευθείας το `OcrEngine.Recognize`, χάνετε την ευκαιρία να καθαρίσετε πρώτα την εικόνα, κάτι που είναι ακριβώς ο λόγος που μας ενδιαφέρει η διόρθωση κλίσης.

## Βήμα 2 – Προσθήκη Φίλτρων Διόρθωσης Κλίσης και Μείωσης Θορύβου (Πώς να Μειώσετε τον Θόρυβο)

Τώρα προσθέτουμε δύο φίλτρα:

| Filter | Τι κάνει | Γιατί είναι σημαντικό |
|--------|----------|------------------------|
| `AutoDeskewFilter` | Ανιχνεύει και διορθώνει την περιστροφή | Ευθυγραμμίζει τις γραμμές κειμένου ώστε η μηχανή OCR να τις διαβάσει σωστά |
| `NoiseReductionFilterV2` | Αφαιρεί στίγματα και θόρυβο φόντου | Καθαρές εικονοστοιχεία σημαίνουν λιγότερες λανθασμένες αναγνώσεις |

```csharp
        // Add filters to improve OCR accuracy
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // corrects rotation
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduces background noise
```

Μπορείτε να αντικαταστήσετε το `NoiseReductionFilterV2` με την παλαιότερη έκδοση, αλλά ο αλγόριθμος v2 διαχειρίζεται καλύτερα τους σύγχρονους σαρωτές. Αν το έγγραφό σας είναι ήδη τέλεια επίπεδο, το φίλτρο deskew θα περάσει απλώς την εικόνα αμετάβλητη — χωρίς καμία ζημιά.

## Βήμα 3 – Φόρτωση της Εικόνας από Αρχείο (Load Image from File)

Το Aspose παρέχει ένα χρήσιμο βοηθητικό `ImageStream.FromFile` που διαβάζει διάφορες μορφές, όπως TIFF, JPEG, PNG και BMP. Δείτε πώς φορτώνουμε το αρχείο στη μνήμη:

```csharp
        // Load the scanned image you want to preprocess
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");
```

Αντικαταστήστε το `YOUR_DIRECTORY` με την πραγματική διαδρομή στο μηχάνημά σας. Αν εργάζεστε με σχετική διαδρομή, βεβαιωθείτε ότι το αρχείο βρίσκεται δίπλα στο εκτελέσιμο ή ορίστε το working directory αναλόγως.

## Βήμα 4 – Εκτέλεση OCR στην Προεπεξεργασμένη Εικόνα (Recognize Text from Image)

Με τα φίλτρα ενεργοποιημένα και την εικόνα φορτωμένη, τελικά ζητάμε από το Aspose να διαβάσει τους χαρακτήρες:

```csharp
        // Perform OCR – the engine will automatically apply the filters first
        var ocrResult = ocrEngine.Recognize(image);
```

Πίσω από τη σκηνή, ο engine εκτελεί τον αλγόριθμο deskew, εξομαλύνει τον θόρυβο και στη συνέχεια τρέχει έναν αναγνώστη βασισμένο σε νευρωνικό δίκτυο. Το αποτέλεσμα είναι ενσωματωμένο σε ένα αντικείμενο `OcrResult` που σας παρέχει το ακατέργαστο κείμενο, τα σκορ εμπιστοσύνης και ακόμη και τα πλαίσια οριοθέτησης αν τα χρειαστείτε αργότερα.

## Βήμα 5 – Εμφάνιση ή Αποθήκευση του Εξαγόμενου Κειμένου (Extract Text from TIFF)

Για μια γρήγορη επίδειξη απλώς εκτυπώνουμε το κείμενο στην κονσόλα, αλλά μπορείτε να το γράψετε σε αρχείο, βάση δεδομένων ή να το ενσωματώσετε σε μια επόμενη ροή εργασίας.

```csharp
        // Show the recognized text in the console
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Αναμενόμενη έξοδος** (παράδειγμα, θα διαφέρει ανάλογα με το έγγραφό σας):

```
Invoice #12345
Date: 2023‑04‑01
Total: $1,250.00
Thank you for your business!
```

Αν η έξοδος εξακολουθεί να περιέχει ακατανόητους χαρακτήρες, ελέγξτε ξανά ότι το αρχικό TIFF δεν είναι πολύ χαμηλής ανάλυσης (συνιστάται τουλάχιστον 300 dpi) και ότι η γλώσσα έχει οριστεί σωστά στο `ocrEngine.Settings.Language`.

## Πλήρες Παράδειγμα Εργασίας (Όλα τα Βήματα σε Ένα Σημείο)

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα νέο έργο console και να το εκτελέσετε αμέσως.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Add preprocessing filters
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // deskew image
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduce noise

        // 3️⃣ Load the image file (TIFF, JPEG, etc.)
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");

        // 4️⃣ Recognize text – filters run automatically
        var ocrResult = ocrEngine.Recognize(image);

        // 5️⃣ Output the extracted text
        Console.WriteLine(ocrResult.Text);
    }
}
```

Αποθηκεύστε το αρχείο ως `Program.cs`, τρέξτε `dotnet run` και θα πρέπει να δείτε το καθαρισμένο κείμενο να εμφανίζεται στο τερματικό σας.

## Συχνές Ερωτήσεις & Ειδικές Περιπτώσεις

### Τι γίνεται αν το TIFF μου έχει πολλαπλές σελίδες;

Το Aspose OCR μπορεί να επεξεργαστεί πολυσελιδικές εικόνες επαναλαμβάνοντας το `image.GetPages()` (ή χρησιμοποιώντας το `image.Pages`). Κάθε σελίδα επιστρέφει το δικό της `OcrResult`. Συνδυάστε τα με `StringBuilder` αν χρειάζεστε ένα ενιαίο κείμενο.

### Λειτουργεί το φίλτρο deskew σε έντονα περιστραμμένες εικόνες;

Διαχειρίζεται περιστροφές έως περίπου ±15°. Πέρα από αυτό ίσως χρειαστεί να προ‑στρέψετε την εικόνα χειροκίνητα χρησιμοποιώντας μια βιβλιοθήκη γραφικών (π.χ., `System.Drawing` ή `SkiaSharp`) πριν τη δώσετε στο Aspose.

### Πώς μπορώ να βελτιώσω την ακρίβεια για μη‑Αγγλικό κείμενο;

Ορίστε τη γλώσσα ρητά:

```csharp
ocrEngine.Settings.Language = Language.English; // or Language.French, etc.
```

Μπορείτε επίσης να φορτώσετε προσαρμοσμένα πακέτα γλώσσας αν τα ενσωματωμένα δεν καλύπτουν το αλφάβητό σας.

### Μπορώ να το τρέξω σε Linux;

Απολύτως. Το Aspose OCR είναι cross‑platform· απλώς βεβαιωθείτε ότι οι εγγενείς εξαρτήσεις είναι παρούσες (συνήθως καμία για την καθαρή .NET έκδοση). Χρησιμοποιήστε `dotnet publish -r linux-x64` για ένα αυτόνομο εκτελέσιμο.

## Επιπλέον: Οπτικοποίηση της Διορθωμένης Εικόνας

Αν θέλετε να δείτε την διορθωμένη εικόνα πριν το OCR, μπορείτε να την αποθηκεύσετε ξανά στο δίσκο:

```csharp
// After OCR, the filtered image is stored in ocrEngine.Settings.FiltersResult
var corrected = ocrEngine.Settings.FiltersResult;
corrected.Save(@"output/deskewed_cleaned.tif");
```

![παράδειγμα διόρθωσης κλίσης εικόνας](https://example.com/deskew-demo.png "παράδειγμα διόρθωσης κλίσης εικόνας")

*Κείμενο alt εικόνας:* **παράδειγμα διόρθωσης κλίσης εικόνας** – δείχνει πριν/μετά ενός περιστρεφόμενου TIFF που διορθώθηκε από το AutoDeskewFilter.

## Συμπέρασμα

Καλύψαμε **πώς να διορθώσετε την κλίση εικόνας**, **πώς να μειώσετε τον θόρυβο**, και ολόκληρη τη ροή για **να αναγνωρίσετε κείμενο από εικόνα**, **να φορτώσετε εικόνα από αρχείο**, και **να εξάγετε κείμενο από tiff** χρησιμοποιώντας το Aspose OCR σε C#. Το κύριο συμπέρασμα; Η προσθήκη μόνο δύο φίλτρων προεπεξεργασίας μπορεί να μετατρέψει μια ασταθή, θορυβώδη σάρωση σε ένα καθαρό, αναζητήσιμο έγγραφο χωρίς εξωτερικά εργαλεία.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να αντικαταστήσετε το `AutoDeskewFilter` με το `AutoRotateFilter` αν τα έγγραφά σας είναι ανάποδα, ή πειραματιστείτε με το `ContrastEnhancementFilter` για ξεθωριασμένες εκτυπώσεις. Το ίδιο μοτίβο—engine → filters → load → recognize—ισχύει για όλα τα σενάρια του Aspose OCR, ώστε να μπορείτε να επαναχρησιμοποιήσετε αυτή τη δομή για PDFs, PNGs ή ακόμη και φωτογραφίες από κάμερα.

Καλό κώδικα, και το OCR σας να είναι πάντα ακριβές!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}