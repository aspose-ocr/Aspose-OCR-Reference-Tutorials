---
category: general
date: 2026-03-26
description: Πώς να διορθώσετε την κλίση μιας εικόνας χρησιμοποιώντας το Aspose OCR
  σε C#. Μάθετε πώς να προεπεξεργαστείτε την εικόνα για OCR, να μειώσετε τον θόρυβο
  και να αναγνωρίσετε κείμενο από την εικόνα αποδοτικά.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- recognize text from image
- how to reduce noise
- how to use aspose
language: el
og_description: Πώς να διορθώσετε την κλίση μιας εικόνας χρησιμοποιώντας το Aspose
  OCR σε C#. Μάθετε πώς να προεπεξεργαστείτε την εικόνα για OCR, να μειώσετε τον θόρυβο
  και να αναγνωρίσετε κείμενο από την εικόνα αποδοτικά.
og_title: Πώς να διορθώσετε την κλίση μιας εικόνας με το Aspose OCR – Πλήρης οδηγός
  C#
tags:
- Aspose
- OCR
- C#
- Image Processing
title: Πώς να διορθώσετε την κλίση εικόνας με το Aspose OCR – Πλήρης οδηγός C#
url: /el/net/skew-angle-calculation/how-to-deskew-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να διορθώσετε την κλίση μιας εικόνας με Aspose OCR – Πλήρης Οδηγός C#

Η διόρθωση κλίσης μιας εικόνας είναι ένα συχνό εμπόδιο όταν προσπαθείτε να εξάγετε κείμενο από μια κεκλιμένη φωτογραφία. Αν έχετε ποτέ δυσκολευτεί να **προεπεξεργαστείτε εικόνα για OCR**, θα εκτιμήσετε ένα καθαρό, ευθυγραμμισμένο αρχείο που επίσης **μειώνει το θόρυβο** πριν **αναγνωρίσετε κείμενο από εικόνα**.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα τις ακριβείς διαδικασίες για να δημιουργήσετε μια αλυσίδα φίλτρων με Aspose OCR, θα εξηγήσουμε γιατί κάθε φίλτρο είναι σημαντικό και θα σας δείξουμε ένα έτοιμο πρόγραμμα C# που εκτυπώνει το εξαγόμενο κείμενο. Χωρίς ασαφείς συνδέσμους «δείτε την τεκμηρίωση»—όλα όσα χρειάζεστε είναι εδώ.

## Τι θα χρειαστείτε

- **Aspose.OCR for .NET** (τελευταίο πακέτο NuGet, π.χ., 23.12).  
- .NET 6 ή νεότερο (ο κώδικας μεταγλωττίζεται και σε .NET Framework 4.8).  
- Ένα δείγμα εικόνας που είναι τόσο κεκλιμένη όσο και θορυβώδης (θα το ονομάσουμε `skewed_noisy.png`).  
- Visual Studio, Rider ή οποιονδήποτε επεξεργαστή προτιμάτε—τίποτα περίπλοκο.

Αυτό είναι όλο. Αν έχετε ήδη ένα project, απλώς προσθέστε την αναφορά NuGet:

```bash
dotnet add package Aspose.OCR
```

Τώρα ας βουτήξουμε.

## Πώς να διορθώσετε την κλίση της εικόνας – Δημιουργία της αλυσίδας φίλτρων

Η καρδιά της λύσης είναι μια **αλυσίδα φίλτρων**. Σκεφτείτε την ως γραμμή συναρμολόγησης όπου κάθε φίλτρο καθαρίζει ένα συγκεκριμένο πρόβλημα. Μέχρι η εικόνα να φτάσει στη μηχανή OCR, είναι πρακτικά έτοιμη για ανάγνωση.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessExample
{
    static void Main()
    {
        // 1️⃣  Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣  Assemble a pipeline: deskew → denoise → optional channel filter
        FilterPipeline filterPipeline = new FilterPipeline();
        filterPipeline.Add(new AdaptiveDeskewFilter());               // auto‑corrects rotation
        filterPipeline.Add(new NoiseReductionFilter());              // AI‑based denoise
        filterPipeline.Add(new ColorChannelFilter(Channel.Red));     // focus on the red channel (optional)

        // 3️⃣  Hook the pipeline to the engine
        ocrEngine.Filters = filterPipeline;

        // 4️⃣  Load the image you want to process
        OcrImage inputImage = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png");

        // 5️⃣  Run OCR – the engine will first apply the pipeline
        OcrResult ocrResult = ocrEngine.Recognize(inputImage);

        // 6️⃣  Output the recognized text
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Γιατί λειτουργεί αυτό:**  
- `AdaptiveDeskewFilter` αναλύει τη βασική γραμμή της εικόνας και την περιστρέφει πίσω στο 0°, που είναι το βήμα *πώς να διορθώσετε την κλίση της εικόνας*.  
- `NoiseReductionFilter` χρησιμοποιεί ένα ελαφρύ μοντέλο AI για να εξομαλύνει τα στίγματα χωρίς να θολώνει τους χαρακτήρες—απαντώντας στο *πώς να μειώσετε το θόρυβο*.  
- `ColorChannelFilter` είναι προαιρετικό αλλά χρήσιμο όταν το κείμενο ξεχωρίζει σε ένα συγκεκριμένο κανάλι (κόκκινο σε αυτήν την περίπτωση).  

Η αλυσίδα εκτελείται **πριν** η μηχανή OCR κοιτάξει τα pixel, ώστε να έχετε έναν πιο καθαρό καμβά για την αναγνώριση.

## Προεπεξεργασία εικόνας για OCR – Μείωση θορύβου και κανάλι χρώματος

Αν παραλείψετε το φίλτρο μείωσης θορύβου, συχνά θα δείτε παραμορφωμένους χαρακτήρες, ειδικά σε σαρωμένες αποδείξεις ή φωτογραφίες με χαμηλό φωτισμό. Εδώ είναι ένα γρήγορο πείραμα που μπορείτε να δοκιμάσετε:

```csharp
// Swap the order: denoise first, then deskew
filterPipeline = new FilterPipeline();
filterPipeline.Add(new NoiseReductionFilter());
filterPipeline.Add(new AdaptiveDeskewFilter());
ocrEngine.Filters = filterPipeline;
```

Η εκτέλεση της μηχανής με την αλλαγή σειράς μερικές φορές δίνει ελαφρώς πιο οξύ αποτέλεσμα σε πολύ σπόρια εικόνες. Ο λόγος; Η αποθορυβοποίηση πρώτα παρέχει στον αλγόριθμο διόρθωσης κλίσης έναν πιο καθαρό χάρτη ακμών για επεξεργασία.  

**Συμβουλή:** Αν οι πηγαίες εικόνες είναι ασπρόμαυρες, παραλείψτε τελείως το `ColorChannelFilter`. Προσθέτει μόνο μικρό επιπλέον φορτίο.

## Αναγνώριση κειμένου από εικόνα – Εκτέλεση της μηχανής OCR

Μόλις η αλυσίδα συνδεθεί, η κλήση `Recognize` κάνει το σκληρό έργο. Στο παρασκήνιο το Aspose OCR εκτελεί:

1. Δυαδικοποίηση (μετατρέπει την εικόνα σε ασπρόμαυρη).  
2. Ανάλυση διάταξης (εντοπίζει γραμμές, στήλες, πίνακες).  
3. Τμηματοποίηση χαρακτήρων (διαχωρίζει κάθε γλύφο).  
4. Κατηγοριοποίηση με νευρωνικό δίκτυο (αντιστοιχίζει γλύφους σε Unicode).  

Όλα αυτά συμβαίνουν σε λίγα χιλιοστά του δευτερολέπτου σε σύγχρονο CPU. Η ιδιότητα `OcrResult.Text` επιστρέφει μια απλή συμβολοσειρά, έτοιμη να αποθηκευτεί, να ευρετηριαστεί ή να τροφοδοτηθεί σε άλλο σύστημα.

### Αναμενόμενη έξοδος

Αν το `skewed_noisy.png` περιέχει τη φράση “Invoice #12345 – Total $89.99”, η κονσόλα θα εκτυπώσει:

```
Invoice #12345 – Total $89.99
```

Αν δείτε επιπλέον αλλαγές γραμμής ή άσχετα σύμβολα, ελέγξτε ξανά το επίπεδο θορύβου· η προσθήκη δεύτερου `NoiseReductionFilter` συχνά βοηθά.

## Πώς να μειώσετε το θόρυβο – Συμβουλές και ειδικές περιπτώσεις

- **Πολλαπλές διεργασίες:** `filterPipeline.Add(new NoiseReductionFilter());` δύο φορές μπορεί να είναι ωφέλιμο για εξαιρετικά σποριακές σαρώσεις.  
- **Ρύθμιση κατωφλίου:** Το φίλτρο εκθέτει μια ιδιότητα `Strength` (0‑100). Χαμηλότερες τιμές διατηρούν λεπτές λεπτομέρειες· υψηλότερες τιμές εξομαλύνουν επιθετικά.  
- **Σημασία μορφής αρχείου:** Το PNG διατηρεί δεδομένα χωρίς απώλειες, ενώ το JPEG εισάγει τεχνητά συμπιεστικά artefacts που μπορεί να δυσκολεύουν τον αποθορυβωτή. Προτιμήστε PNG για προεπεξεργασία.

```csharp
var heavyNoiseFilter = new NoiseReductionFilter { Strength = 80 };
filterPipeline.Add(heavyNoiseFilter);
```

## Πώς να χρησιμοποιήσετε το Aspose – Εγκατάσταση, Αδειοδότηση και Πιθανές παγίδες

Το Aspose είναι εμπορική βιβλιοθήκη, αλλά διατίθεται με **δωρεάν δοκιμή** που λειτουργεί έως 30 ημέρες. Για να ξεκλειδώσετε όλες τις δυνατότητες:

```csharp
// Somewhere early in your app (e.g., Main)
Aspose.OCR.License license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

Τοποθετήστε το αρχείο `.lic` δίπλα στο εκτελέσιμο ή ενσωματώστε το ως πόρο.  

**Κοινό λάθος:** Η παράλειψη ορισμού της άδειας προσθέτει υδατογράφημα στο αναγνωρισμένο κείμενο. Η μηχανή λειτουργεί, αλλά η έξοδος περιέχει συμβολοσειρές “Aspose OCR”.  

Επιπλέον, η βιβλιοθήκη είναι **thread‑safe** για λειτουργίες ανάγνωσης, αλλά το `OcrEngine` δεν πρέπει να μοιράζεται μεταξύ νημάτων εκτός αν δημιουργήσετε νέο στιγμιότυπο ανά αίτημα.

## Πλήρες λειτουργικό παράδειγμα – Συνδυάστε τα όλα

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε μια εφαρμογή console:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessExample
{
    static void Main()
    {
        // OPTIONAL: Apply your Aspose license
        // var license = new Aspose.OCR.License();
        // license.SetLicense("Aspose.OCR.lic");

        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Build filter pipeline
        FilterPipeline pipeline = new FilterPipeline();
        pipeline.Add(new AdaptiveDeskewFilter());               // how to deskew image
        pipeline.Add(new NoiseReductionFilter());              // how to reduce noise
        pipeline.Add(new ColorChannelFilter(Channel.Red));     // optional color focus

        // 3️⃣ Attach pipeline
        ocrEngine.Filters = pipeline;

        // 4️⃣ Load image
        string imagePath = @"YOUR_DIRECTORY/skewed_noisy.png";
        OcrImage img = OcrImage.FromFile(imagePath);

        // 5️⃣ Perform OCR
        OcrResult result = ocrEngine.Recognize(img);

        // 6️⃣ Output result
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);
    }
}
```

Τρέξτε το πρόγραμμα και θα δείτε το καθαρισμένο κείμενο να εκτυπώνεται στην κονσόλα. Αν θέλετε να γράψετε την έξοδο σε αρχείο:

```csharp
System.IO.File.WriteAllText("output.txt", result.Text);
```

## Οπτικό αποτέλεσμα – Πριν & Μετά

Παρακάτω υπάρχει μια εικονική απεικόνιση που δείχνει την αρχική κεκλιμένη εικόνα στα αριστερά και την διορθωμένη, αποθορυβωμένη έκδοση στα δεξιά.

![Πώς να διορθώσετε την κλίση της εικόνας – πριν και μετά την επεξεργασία](https://example.com/deskew-before-after.png "παράδειγμα διόρθωσης κλίσης εικόνας")

*Alt text:* πώς να διορθώσετε την κλίση της εικόνας – οπτική σύγκριση της αρχικής εικόνας με την επεξεργασμένη.

## Συμπέρασμα

Καλύψαμε **πώς να διορθώσετε την κλίση της εικόνας** χρησιμοποιώντας Aspose OCR, περάσαμε από **προεπεξεργασία εικόνας για OCR** με μείωση θορύβου, και παρουσιάσαμε έναν καθαρό τρόπο για **αναγνώριση κειμένου από εικόνα** σε C#. Συνδυάζοντας τα `AdaptiveDeskewFilter`, `NoiseReductionFilter` και ένα προαιρετικό `ColorChannelFilter`, αποκτάτε μια ισχυρή αλυσίδα που λειτουργεί στις περισσότερες πραγματικές φωτογραφίες.

Τι ακολουθεί; Δοκιμάστε να αντικαταστήσετε το φίλτρο κόκκινου καναλιού με

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}