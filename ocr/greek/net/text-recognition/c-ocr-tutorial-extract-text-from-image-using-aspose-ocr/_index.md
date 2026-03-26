---
category: general
date: 2026-03-26
description: c# OCR tutorial που δείχνει πώς να εξάγετε κείμενο από εικόνα, να αναγνωρίσετε
  κείμενο από JPEG και να φορτώσετε εικόνα για OCR – περιλαμβάνει υποστήριξη κυριλλικού.
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- recognize text from jpeg
- load image for ocr
- recognize cyrillic text
language: el
og_description: c# OCR οδηγός που σας καθοδηγεί στη φόρτωση μιας εικόνας για OCR,
  στην αναγνώριση κειμένου από JPEG και στην εξαγωγή κυριλλικού κειμένου σε λίγα εύκολα
  βήματα.
og_title: c# OCR οδηγός – Εξαγωγή κειμένου από εικόνα με Aspose OCR
tags:
- OCR
- C#
- Aspose
- ImageProcessing
title: c# OCR οδηγός – Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας Aspose OCR
url: /el/net/text-recognition/c-ocr-tutorial-extract-text-from-image-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Εξαγωγή Κειμένου από Εικόνα Χρησιμοποιώντας το Aspose OCR

Ποτέ χρειάστηκες ένα **c# ocr tutorial** που πραγματικά σε οδηγεί από ένα κενό JPEG σε αναγνώσιμο κείμενο Unicode; Ίσως δημιουργείς ένα εργαλείο αρχειοθέτησης εγγράφων, έναν σαρωτή αποδείξεων, ή απλώς είσαι περίεργος για το πώς να εξάγεις κείμενο από εικόνες. Σε κάθε περίπτωση, βρίσκεσαι στο σωστό μέρος. Σε αυτόν τον οδηγό θα σου δείξουμε πώς να **extract text from image** αρχεία, **recognize text from jpeg** πόρους, και ακόμη να αντιμετωπίσεις το δύσκολο σενάριο **recognize cyrillic text**—χωρίς κλήσεις στο cloud.

Θα χρησιμοποιήσουμε το Aspose.OCR, μια πλήρως offline βιβλιοθήκη που παρέχει μονάδες γλώσσας που μπορείτε να δείξετε σε φάκελο στο δίσκο. Στο τέλος αυτού του tutorial θα έχετε μια αυτόνομη εφαρμογή console που φορτώνει μια εικόνα για OCR, εκτελεί τη μηχανή και εκτυπώνει το αποτέλεσμα στην κονσόλα. Χωρίς εξωτερικές υπηρεσίες, χωρίς κλειδιά API—απλώς καθαρό C#.

## Τι Θα Χρειαστείτε

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Core και .NET Framework)
- Visual Studio 2022 ή οποιοδήποτε IDE προτιμάτε
- Πακέτο NuGet Aspose.OCR (`Aspose.OCR`) και ο αντίστοιχος φάκελος `Aspose.OCR.Resources`
- Μια εικόνα JPEG που περιέχει χαρακτήρες κυριλλικού (ή οποιαδήποτε γλώσσα θέλετε να δοκιμάσετε)

Αν λείπει κάποιο από αυτά, κατεβάστε το πακέτο NuGet μέσω του Package Manager Console:

```powershell
Install-Package Aspose.OCR
```

και κατεβάστε τους πόρους γλώσσας από την ιστοσελίδα Aspose, αποσυμπιέστε τα σε φάκελο όπως `C:\OCR\Aspose.OCR.Resources`.

Τώρα, ας ξεκινήσουμε.

## Βήμα 1: Φόρτωση Πόρων OCR – load image for ocr

Το πρώτο που χρειάζεται η μηχανή είναι μια διαδρομή προς τις μονάδες γλώσσας. Σκεφτείτε το ως το να λέτε στο OCR πού βρίσκεται το λεξικό του.

```csharp
using Aspose.OCR;
using Aspose.OCR.Resources;

// Point to the folder that contains the language modules
ResourceManager.SetLocalResourcesPath(@"C:\OCR\Aspose.OCR.Resources");
```

> **Pro tip:** Χρησιμοποιήστε απόλυτη διαδρομή κατά την ανάπτυξη. Όταν διανείμετε την εφαρμογή, σκεφτείτε να ενσωματώσετε τους πόρους ή να τους αντιγράψετε δίπλα στο εκτελέσιμο.

## Βήμα 2: Επιλογή Γλώσσας – recognize cyrillic text

Το Aspose υποστηρίζει δεκάδες γλώσσες, αλλά πρέπει να επιλέξετε αυτή που χρειάζεστε. Για κυριλλικό κείμενο χρησιμοποιούμε το `OcrLanguage.CyrillicExtended`. Αν χρειάζεστε μόνο λατινικούς χαρακτήρες, αντικαταστήστε το με `OcrLanguage.English`.

```csharp
// Create the OCR engine and set the language
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.CyrillicExtended   // This enables Cyrillic recognition
};
```

Γιατί είναι σημαντικό; Η μηχανή φορτώνει ταξινομητές ειδικούς για κάθε γλώσσα· η επιλογή του λάθους μπορεί να μειώσει δραματικά την ακρίβεια.

## Βήμα 3: Φόρτωση JPEG – recognize text from jpeg

Τώρα φορτώνουμε πραγματικά την εικόνα που θέλουμε να σαρώσουμε. Το Aspose μπορεί να διαβάσει κοινές μορφές όπως JPEG, PNG, BMP και TIFF.

```csharp
// Load the image file (replace with your own path)
var ocrImage = OcrImage.FromFile(@"C:\OCR\Samples\cyrillic_doc.jpg");
```

Αν η εικόνα είναι μεγάλη, ίσως θελήσετε να τη μειώσετε πριν τη δώσετε στη μηχανή—αυτό επιταχύνει την επεξεργασία και μειώνει τη χρήση μνήμης.

## Βήμα 4: Εκτέλεση Αναγνώρισης – extract text from image

Με τη μηχανή ρυθμισμένη και την εικόνα στη μνήμη, το βήμα αναγνώρισης είναι μια μόνο γραμμή.

```csharp
// Perform the OCR operation
OcrResult ocrResult = ocrEngine.Recognize(ocrImage);
```

Πίσω από τη σκηνή, η μηχανή εκτελεί μια αλυσίδα προεπεξεργασίας (αφαίρεση θορύβου, δυαδικοποίηση) και στη συνέχεια ταιριάζει τα οπτικά μοτίβα με το επιλεγμένο μοντέλο γλώσσας.

## Βήμα 5: Εμφάνιση Αποτελέσματος – extract text from image

Τέλος, εμφανίζουμε τη αναγνωρισμένη συμβολοσειρά. Σε μια πραγματική εφαρμογή μπορεί να την γράψετε σε αρχείο, βάση δεδομένων ή να τη δώσετε σε ευρετήριο αναζήτησης.

```csharp
// Print the extracted text to the console
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

**Expected output** (assuming the sample image contains “Привет мир!”):

```
=== OCR Output ===
Привет мир!
```

Αν δείτε ακατάστατους χαρακτήρες, ελέγξτε ξανά ότι έχετε επιλέξει τη σωστή γλώσσα και ότι η εικόνα δεν είναι πολύ θορυβώδης.

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω είναι το πλήρες πρόγραμμα, έτοιμο για αντιγραφή‑και‑επικόλληση. Αποθηκεύστε το ως `Program.cs` μέσα σε ένα νέο έργο console και τρέξτε το.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Resources;

class OfflineOcrDemo
{
    static void Main()
    {
        // Step 1: Point the OCR engine to the folder that contains the language modules
        ResourceManager.SetLocalResourcesPath(@"C:\OCR\Aspose.OCR.Resources");

        // Step 2: Create the OCR engine and select the required language (Cyrillic Extended)
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.CyrillicExtended
        };

        // Step 3: Load the image that contains the text to be recognized
        var ocrImage = OcrImage.FromFile(@"C:\OCR\Samples\cyrillic_doc.jpg");

        // Step 4: Perform the recognition operation
        OcrResult ocrResult = ocrEngine.Recognize(ocrImage);

        // Step 5: Display the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Note:** Αντικαταστήστε τις διαδρομές με τις πραγματικές τοποθεσίες στο σύστημά σας. Το πρόγραμμα λειτουργεί offline· δεν απαιτείται σύνδεση στο internet μόλις οι πόροι είναι παρόντες.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν η εικόνα μου είναι PNG αντί για JPEG;
Το Aspose.OCR αντιμετωπίζει το PNG με τον ίδιο τρόπο όπως το JPEG. Απλώς αλλάξτε την επέκταση αρχείου στο `FromFile`. Το βήμα **recognize text from jpeg** λειτουργεί για οποιαδήποτε υποστηριζόμενη μορφή.

### Πώς μπορώ να βελτιώσω την ακρίβεια σε σαρώσεις χαμηλής ποιότητας;
- Προεπεξεργαστείτε την εικόνα (αυξήστε την αντίθεση, διορθώστε την κλίση) χρησιμοποιώντας `ocrImage.AdjustContrast(1.2)` ή παρόμοιες μεθόδους.
- Χρησιμοποιήστε `OcrEngine.PreprocessImage` πριν καλέσετε το `Recognize`.
- Επιλέξτε μια γλώσσα που ταιριάζει στο σύστημα γραφής· για μεικτό Latin/Cyrillic μπορείτε να ορίσετε `Language = OcrLanguage.Multilingual`.

### Μπορώ να εξάγω μόνο αριθμούς ή ημερομηνίες;
Ναι. Αφού έχετε το `ocrResult.Text`, εφαρμόστε κανονικές εκφράσεις για να φιλτράρετε τα τμήματα που χρειάζεστε. Το OCR επιστρέφει τη ακατέργαστη συμβολοσειρά· η περαιτέρω ανάλυση είναι δική σας.

### Είναι δυνατό να τρέξει αυτό σε Linux;
Απολύτως. Το Aspose.OCR είναι cross‑platform. Απλώς εγκαταστήστε το .NET runtime στο Linux σύστημά σας και δείξτε το `SetLocalResourcesPath` στον κατάλληλο φάκελο.

## Pro Συμβουλές για Παραγωγή

- **Cache the OcrEngine**: Η δημιουργία νέας μηχανής για κάθε αίτημα προσθέτει επιβάρυνση. Διατηρήστε ένα singleton αν επεξεργάζεστε πολλές εικόνες.
- **Thread safety**: Η μηχανή δεν είναι thread‑safe από προεπιλογή. Ε είτε κλειδώστε γύρω από το `Recognize` ή δημιουργήστε ξεχωριστές μηχανές ανά νήμα.
- **Memory management**: Αποδεσμεύστε τα αντικείμενα `OcrImage` μετά τη χρήση (`ocrImage.Dispose()`) για να ελευθερώσετε τους εγγενείς buffer.
- **Logging**: Καταγράψτε το `ocrResult.Confidence` (αν υπάρχει) για να εντοπίσετε σαρώσεις χαμηλής εμπιστοσύνης και να ενεργοποιήσετε εναλλακτική λύση.

## Συμπέρασμα

Τώρα έχετε ένα **c# ocr tutorial** που σας οδηγεί βήμα-βήμα στο **load image for ocr**, **recognize text from jpeg**, **extract text from image**, και **recognize cyrillic text** χρησιμοποιώντας το Aspose.OCR. Ο κώδικας δείγματος είναι έτοιμος για εκτέλεση, και οι εξηγήσεις δείχνουν γιατί κάθε γραμμή είναι σημαντική—όχι μόνο πώς.

Από εδώ μπορείτε να πειραματιστείτε με άλλες γλώσσες, να ενσωματώσετε το OCR σε ένα web API, ή να τροφοδοτήσετε τις εξαγόμενες συμβολοσειρές σε μια μηχανή αναζήτησης. Οι δυνατότητες είναι τόσο ευρείες όσο οι εικόνες που τροφοδοτείτε.

Αν αντιμετωπίσατε προβλήματα, αφήστε ένα σχόλιο παρακάτω ή ελέγξτε την τεκμηρίωση του Aspose για πιο προχωρημένες επιλογές ρύθμισης. Καλή προγραμματιστική δουλειά, και εύχομαι οι εικόνες σας να είναι πάντα κρυστάλλινα καθαρές!

![c# ocr tutorial screenshot showing console output of extracted text](/images/ocr-demo.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}