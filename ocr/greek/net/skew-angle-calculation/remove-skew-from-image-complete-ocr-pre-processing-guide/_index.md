---
category: general
date: 2026-02-14
description: Μάθετε πώς να αφαιρέσετε την κλίση από την εικόνα, να προεπεξεργαστείτε
  την εικόνα για OCR, να μειώσετε τον θόρυβο στην εικόνα και να εξάγετε κείμενο από
  την εικόνα χρησιμοποιώντας το Aspose OCR σε C#.
draft: false
keywords:
- remove skew from image
- preprocess image for ocr
- reduce noise in image
- extract text from image
- recognize text from document
language: el
og_description: Αφαιρέστε την κλίση από την εικόνα, προεπεξεργαστείτε την εικόνα για
  OCR και εξάγετε κείμενο από την εικόνα με ένα βήμα‑βήμα tutorial σε C# χρησιμοποιώντας
  το Aspose OCR.
og_title: Αφαίρεση κλίσης από την εικόνα – Πλήρης οδηγός προεπεξεργασίας OCR
tags:
- OCR
- CSharp
- ImageProcessing
title: Αφαίρεση κλίσης από την εικόνα – Πλήρης οδηγός προεπεξεργασίας OCR
url: /el/net/skew-angle-calculation/remove-skew-from-image-complete-ocr-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αφαίρεση Κλίσης από Εικόνα – Πλήρης Οδηγός Προεπεξεργασίας OCR

Έχετε ποτέ χρειαστεί να **αφαιρέσετε κλίση από εικόνα** πριν τη δώσετε σε μια μηχανή OCR; Δεν είστε ο μόνος—σκανάρισμα εγγράφων, φωτογραφίες αποδείξεων ή στιγμιότυπα συχνά έρχονται κεκλιμένα, και αυτή η μικρή γωνία μπορεί να υπονομεύσει την αναγνώριση κειμένου.  

Τα καλά νέα; Με μια σειρά από φίλτρα Aspose OCR μπορείτε να ευθυγραμμίσετε, να αφαιρέσετε θόρυβο, να ενισχύσετε την αντίθεση, και στη συνέχεια **να εξάγετε κείμενο από εικόνα** σε μια ενιαία, ομαλή αλυσίδα. Σε αυτόν τον οδηγό θα περάσουμε από όλη τη διαδικασία, από τη φόρτωση μιας κεκλιμένης εικόνας μέχρι **να αναγνωρίσετε κείμενο από έγγραφο** και να εκτυπώσετε το αποτέλεσμα.

---

## Τι Θα Δημιουργήσετε

Στο τέλος αυτού του tutorial θα έχετε μια έτοιμη προς εκτέλεση εφαρμογή κονσόλας C# που:

1. **Αφαιρεί κλίση από εικόνα** χρησιμοποιώντας το `DeskewFilter`.
2. **Μειώνει τον θόρυβο στην εικόνα** με το `DenoiseFilter`.
3. **Προετοιμάζει την εικόνα για OCR** ενισχύοντας την αντίθεση.
4. **Αναγνωρίζει κείμενο από έγγραφο** μέσω του `Engine` του Aspose OCR.
5. **Εξάγει κείμενο από εικόνα** και το εμφανίζει στην κονσόλα.

Καμία εξωτερική υπηρεσία, μόνο το πακέτο NuGet Aspose OCR και μερικές γραμμές κώδικα.

## Προαπαιτούμενα

- .NET 6.0 SDK ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Core και .NET Framework).
- Visual Studio 2022 ή οποιονδήποτε επεξεργαστή προτιμάτε.
- Aspose.OCR για .NET εγκατεστημένο (`dotnet add package Aspose.OCR`).
- Ένα δείγμα εικόνας (`skewed_noisy.jpg`) τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε.

Αν έχετε όλα αυτά, ας ξεκινήσουμε.

## Βήμα 1: Φόρτωση της Πηγαίας Εικόνας

Το πρώτο που χρειαζόμαστε είναι ένα `ImageStream` που δείχνει στο αρχείο που θέλουμε να καθαρίσουμε.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the source image that needs cleaning
ImageStream sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
```

> **Γιατί είναι σημαντικό:** Το `ImageStream` αφαιρεί την άμεση διαχείριση του bitmap, επιτρέποντας στα φίλτρα Aspose να λειτουργούν χωρίς να χρειάζεται να διαχειρίζεστε ακατέργαστα δεδομένα εικονοστοιχείων.

## Βήμα 2: Δημιουργία Αλυσίδας Προεπεξεργασίας (Αφαίρεση Κλίσης & Μείωση Θορύβου)

Αντί να καλέσετε κάθε φίλτρο ξεχωριστά, το Aspose σας επιτρέπει να τα συνδέσετε σε μια `ImageProcessingPipeline`. Αυτό διατηρεί τον κώδικα τακτοποιημένο και εξασφαλίζει ότι οι λειτουργίες εκτελούνται με τη σωστή σειρά.

```csharp
// Create a pipeline and add desired filters
var processingPipeline = new ImageProcessingPipeline()
    .AddFilter(new DeskewFilter())                     // Remove skew
    .AddFilter(new DenoiseFilter())                    // Reduce noise
    .AddFilter(new ContrastBoostFilter { Level = 30 });// Boost contrast (0‑100)
```

### Γιατί η Σειρά Είναι Σημαντική

1. **Πρώτα Deskew** – Η ευθυγράμμιση της εικόνας πριν την αφαίρεση θορύβου αποτρέπει το φίλτρο θορύβου να αντιμετωπίζει τις κεκλιμένες άκρες ως τεχνουργήματα.  
2. **Δεύτερο Denoise** – Μόλις η εικόνα είναι επίπεδη, ο αλγόριθμος μπορεί να διακρίνει καλύτερα το σήμα από το σπόρο.  
3. **Τελευταίο Contrast boost** – Η ενίσχυση της αντίθεσης μετά τον καθαρισμό της εικόνας μεγιστοποιεί την αναγνωσιμότητα για OCR χωρίς να ενισχύει τον θόρυβο.

## Βήμα 3: Εφαρμογή της Αλυσίδας και Λήψη Καθαρισμένης Εικόνας

Τώρα εκτελούμε την αλυσίδα πάνω στο αρχικό stream.

```csharp
// Apply the pipeline to obtain a cleaned image
ImageStream cleanedImage = processingPipeline.Apply(sourceImage);
```

Σε αυτό το σημείο η εικόνα είναι ευθυγραμμισμένη, χωρίς θόρυβο και με υψηλότερη αντίθεση—ιδανική για OCR.

## Βήμα 4: Αρχικοποίηση του OCR Engine και Αναγνώριση Κειμένου

Με μια άψογη εικόνα στα χέρια μας, μπορούμε τελικά να τη δώσουμε στο Aspose OCR.

```csharp
// Initialise the OCR engine
Engine ocrEngine = new Engine();

// Recognise text from the cleaned image
OcrResult ocrResult = ocrEngine.Recognize(cleanedImage);
```

> **Συμβουλή:** Αν χρειάζεστε ρύθμιση ανά γλώσσα, το `Engine` δέχεται μια ιδιότητα `Language` (π.χ., `ocrEngine.Language = Language.English;`). Για τα περισσότερα έγγραφα με λατινικό αλφάβητο η προεπιλογή λειτουργεί καλά.

## Βήμα 5: Εμφάνιση του Εξαγόμενου Κειμένου

Ένα γρήγορο `Console.WriteLine` εμφανίζει το αποτέλεσμα.

```csharp
// Output the extracted text
Console.WriteLine(ocrResult.Text);
```

Όταν εκτελέσετε το πρόγραμμα, θα πρέπει να δείτε το κειμενικό περιεχόμενο του `skewed_noisy.jpg` να εκτυπώνεται στο τερματικό—καθαρό, ευανάγνωστο και έτοιμο για επόμενη επεξεργασία.

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω είναι το πλήρες, έτοιμο για αντιγραφή πρόγραμμα. Αποθηκεύστε το ως `Program.cs`, αντικαταστήστε το `YOUR_DIRECTORY` με την πραγματική διαδρομή, και τρέξτε `dotnet run`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace ImageOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Load the source image that needs cleaning
            ImageStream sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");

            // Step 2: Create an image‑processing pipeline and add desired filters
            var processingPipeline = new ImageProcessingPipeline()
                .AddFilter(new DeskewFilter())                     // Remove skew
                .AddFilter(new DenoiseFilter())                    // Reduce noise
                .AddFilter(new ContrastBoostFilter { Level = 30 });// Boost contrast (0‑100)

            // Step 3: Apply the pipeline to obtain a cleaned image
            ImageStream cleanedImage = processingPipeline.Apply(sourceImage);

            // Step 4: Initialise the OCR engine and recognize text from the cleaned image
            Engine ocrEngine = new Engine();
            OcrResult ocrResult = ocrEngine.Recognize(cleanedImage);

            // Step 5: Display the extracted text
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**Αναμενόμενη έξοδος** (παράδειγμα για μια απλή απόδειξη):

```
=== Extracted Text ===
Store: Coffee Corner
Date: 02/12/2026
Item          Qty   Price
Latte          2    $5.80
Croissant      1    $2.50
Total                $8.30
```

Αν η έξοδος φαίνεται ακατάληπτη, ελέγξτε ξανά ότι η διαδρομή της εικόνας είναι σωστή και ότι το αρχείο πηγής περιέχει πραγματικά αναγνώσιμο κείμενο.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν η εικόνα είναι περιστραμμένη κατά 90° αντί για μικρή κλίση;

`DeskewFilter` διαχειρίζεται μικρές γωνίες (±15°). Για πλήρεις περιστροφές, καλέστε `new RotateFilter { Angle = 90 }` πριν το βήμα deskew.

### Η εικόνα μου είναι σε μορφή PNG—αλλάζει κάτι;

Όχι. Το `ImageStream.FromFile` ανιχνεύει αυτόματα τη μορφή, έτσι PNG, JPEG, BMP ή TIFF λειτουργούν με τον ίδιο τρόπο.

### Πώς μπορώ να ρυθμίσω την ισχύ της μείωσης θορύβου;

Το `DenoiseFilter` εκθέτει μια ιδιότητα `Strength` (0‑100). Μεγαλύτερες τιμές αφαιρούν περισσότερο σπόρο αλλά μπορεί να θολώσουν λεπτομέρειες. Πειραματιστείτε με τιμές γύρω στα 30‑50 για έγγραφα με πολύ κείμενο.

### Χρειάζομαι να επεξεργαστώ μια δέσμη αρχείων—μπορώ να επαναχρησιμοποιήσω την αλυσίδα;

Απόλυτα. Δημιουργήστε το `processingPipeline` μία φορά, μετά κάντε βρόχο πάνω σε κάθε αρχείο:

```csharp
foreach (var path in Directory.GetFiles("batch_folder", "*.jpg"))
{
    var src = ImageStream.FromFile(path);
    var cleaned = processingPipeline.Apply(src);
    var result = ocrEngine.Recognize(cleaned);
    // Save or log result.Text
}
```

Η επαναχρησιμοποίηση του ίδιου αντικειμένου `Engine` επίσης βελτιώνει την απόδοση.

## Επαγγελματικές Συμβουλές για OCR Έτοιμο στην Παραγωγή

- **Cache την αλυσίδα**: Η δημιουργία φίλτρων επανειλημμένα μπορεί να είναι δαπανηρή σε σενάρια υψηλής απόδοσης.  
- **Ορίστε τη γλώσσα OCR**: `ocrEngine.Language = Language.Spanish;` για έγγραφα μη‑αγγλικά.  
- **Διαχειριστείτε κενά αποτελέσματα**: Πάντα ελέγξτε `ocrResult.Text?.Length > 0` πριν προχωρήσετε.  
- **Καταγράψτε ενδιάμεσες εικόνες**: Η αποθήκευση του `cleanedImage` στο δίσκο (`cleanedImage.Save("debug.png");`) σας βοηθά να ρυθμίσετε ακριβώς τις παραμέτρους των φίλτρων.

## Συμπέρασμα

Σας δείξαμε πώς να **αφαιρέσετε κλίση από εικόνα**, **μειώσετε τον θόρυβο στην εικόνα**, και **προετοιμάσετε την εικόνα για OCR** χρησιμοποιώντας την ισχυρή αλυσίδα φίλτρων του Aspose OCR, στη συνέχεια **να αναγνωρίσετε κείμενο από έγγραφο** και τελικά **να εξάγετε κείμενο από εικόνα**. Η πλήρης ροή εργασίας χωράει σε λιγότερο από 50 γραμμές C# και είναι εύκολη στην επέκταση για επεξεργασία δέσμης, προσαρμοσμένα μοντέλα γλώσσας ή επιπλέον φίλτρα.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να προσθέσετε ένα `BinarizeFilter` για εξαναγκασμό εξόδου μαύρο‑άσπρου, ή πειραματιστείτε με διαφορετικά επίπεδα `ContrastBoostFilter` για να δείτε πώς επηρεάζουν την ακρίβεια αναγνώρισης. Όσο περισσότερο παίζετε με την αλυσίδα, τόσο καλύτερα θα καταλάβετε πώς κάθε φίλτρο συμβάλλει σε ένα καθαρό αποτέλεσμα OCR.

Καλή προγραμματιστική δουλειά, και εύχομαι οι εικόνες σας να παραμένουν πάντα ευθυγραμμισμένες!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}