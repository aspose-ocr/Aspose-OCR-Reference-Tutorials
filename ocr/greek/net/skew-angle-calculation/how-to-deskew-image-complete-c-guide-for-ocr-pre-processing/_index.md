---
category: general
date: 2025-12-29
description: Μάθετε πώς να διορθώνετε την κλίση μιας εικόνας, να αφαιρείτε το φόντο
  και να εξάγετε κείμενο με το Aspose OCR. Βήμα‑βήμα κώδικας C# για προεπεξεργασία
  εικόνας για OCR και αναγνώριση κειμένου από εικόνα.
draft: false
keywords:
- how to deskew image
- how to remove background
- how to extract text
- preprocess image for ocr
- recognize text from image
language: el
og_description: Πώς να διορθώσετε την κλίση μιας εικόνας και να βελτιώσετε την ακρίβεια
  του OCR. Ακολουθήστε αυτόν τον οδηγό για να αφαιρέσετε το φόντο, να προεπεξεργαστείτε
  την εικόνα για OCR και να αναγνωρίσετε κείμενο από την εικόνα χρησιμοποιώντας το
  Aspose.
og_title: Πώς να διορθώσετε την κλίση εικόνας – Εγχειρίδιο προεπεξεργασίας OCR σε
  C#
tags:
- Aspose OCR
- C#
- Image preprocessing
title: Πώς να διορθώσετε την κλίση εικόνας – Πλήρης οδηγός C# για προεπεξεργασία OCR
url: /el/net/skew-angle-calculation/how-to-deskew-image-complete-c-guide-for-ocr-pre-processing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Deskew Image – Πλήρης Οδηγός C# για Προεπεξεργασία OCR

Έχετε αναρωτηθεί ποτέ **how to deskew image** αρχεία που βγήκαν από σαρωτή και μοιάζουν με μια στραβή κάρτα; Δεν είστε μόνοι. Σε πολλά πραγματικά έργα οι πηγαίες εικόνες είναι κεκλιμένες, θορυβώδεις ή έχουν ακατάστατο φόντο, και αυτό κάνει το OCR να δυσκολεύεται.

Σε αυτό το tutorial θα περάσουμε από μια πρακτική λύση που όχι μόνο **how to deskew image**, αλλά επίσης **how to remove background**, **how to extract text**, και τελικά **recognize text from image** χρησιμοποιώντας το Aspose OCR για .NET. Στο τέλος θα έχετε ένα έτοιμο προς εκτέλεση πρόγραμμα C# που προεπεξεργάζεται μια εικόνα για OCR και επιστρέφει καθαρό, αναζητήσιμο κείμενο.

## Τι Θα Χρειαστείτε

- .NET 6 SDK ή νεότερο (ο κώδικας λειτουργεί σε .NET Core και .NET Framework)  
- Visual Studio 2022 (ή οποιονδήποτε επεξεργαστή προτιμάτε)  
- Πακέτο NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- Ένα δείγμα εικόνας που είναι κεκλιμένη και θορυβώδης (π.χ., `skewed_noisy.jpg`)  

Αυτό είναι όλο—χωρίς επιπλέον εγγενείς βιβλιοθήκες, χωρίς περίπλοκα εργαλεία γραμμής εντολών. Ας βουτήξουμε.

## Βήμα 1 – Φόρτωση της Εισαγόμενης Εικόνας (How to Deskew Image Ξεκινά Εδώ)

Το πρώτο πράγμα που πρέπει να κάνετε είναι να φορτώσετε την εικόνα στη μνήμη. Η μέθοδος `Image.Load` του Aspose OCR δέχεται μια διαδρομή αρχείου και επιστρέφει ένα αντικείμενο `Image` που μπορείτε να επεξεργαστείτε.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class Program
{
    static void Main()
    {
        // Load the original photo that needs deskewing and cleaning
        Image originalImage = Image.Load("YOUR_DIRECTORY/skewed_noisy.jpg");
```

> **Γιατί είναι σημαντικό:** Η φόρτωση της εικόνας μας δίνει ένα χειριστήριο για να εφαρμόσουμε κάθε επόμενο μετασχηματισμό, από το deskewing μέχρι την αφαίρεση φόντου.

## Βήμα 2 – Deskew την Εικόνα (How to Deskew Image στην Πράξη)

Το Aspose OCR περιλαμβάνει ένα βολικό φίλτρο `Deskew` που ανιχνεύει αυτόματα τη γωνία κλίσης μέχρι ένα ρυθμιζόμενο όριο. Εδώ επιτρέπουμε έως **5°** επειδή τα περισσότερα σαρωμένα έγγραφα δεν ξεπερνούν αυτό.

```csharp
        // Auto‑detect and correct rotation up to 5 degrees
        Image deskewed = ImageFilters.Deskew(originalImage, angleThreshold: 5);
```

> **Συμβουλή:** Αν τα έγγραφά σας είναι περιστραμμένα περισσότερο από 5°, αυξήστε το `angleThreshold` σε 10 ή 15. Ο αλγόριθμος παραμένει γρήγορος ακόμη και με μεγαλύτερες γωνίες.

## Βήμα 3 – Απενεργοποίηση Θορύβου στην Deskewed Εικόνα

Ο θόρυβος είναι ο σιωπηλός δολοφόνος της ακρίβειας του OCR. Ένα απλό πέρασμα απενεργοποίησης θορύβου εξομαλύνει τις κηλίδες χωρίς να θολώνει τους πραγματικούς χαρακτήρες.

```csharp
        // Reduce random speckles and grain
        Image denoised = deskewed.Denoise();
```

> **Τι συμβαίνει στο παρασκήνιο;** Το φίλτρο εφαρμόζει μια μεσαία θόλωση που διατηρεί τις άκρες (τα γράμματα) ενώ καταστέλλει τα απομονωμένα pixel.

## Βήμα 4 – Αφαίρεση Φόντου (How to Remove Background Αποτελεσματικά)

Ένα ανοιχτό ή με μοτίβο φόντο μπορεί να μπερδέψει τη μηχανή OCR. Η μέθοδος `RemoveBackground` του Aspose OCR απομονώνει το κείμενο στο προσκήνιο.

```csharp
        // Strip away uneven lighting or paper texture
        Image processedImage = denoised.RemoveBackground();
```

> **Γιατί να αφαιρέσετε το φόντο;** Με την ενίσχυση της αντίθεσης μεταξύ κειμένου και καμβά, η μηχανή μπορεί να διακρίνει τους χαρακτήρες πιο αξιόπιστα, κάτι που βελτιώνει άμεσα τα αποτελέσματα του **how to extract text**.

## Βήμα 5 – Αρχικοποίηση της Μηχανής OCR

Τώρα που η εικόνα είναι ευθεία, καθαρή και υψηλής αντίθεσης, δημιουργούμε την μηχανή OCR. Δεν απαιτείται πρόσθετη διαμόρφωση για βασικά λατινικά σενάρια, αλλά μπορείτε να αλλάξετε γλώσσες αν χρειάζεται.

```csharp
        // Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **Σημείωση:** Το Aspose OCR υποστηρίζει πάνω από 100 γλώσσες. Αν χρειάζεστε πολυγλωσσική υποστήριξη, ορίστε `ocrEngine.Language = OcrLanguage.YourLanguage;` πριν από την αναγνώριση.

## Βήμα 6 – Αναγνώριση Κειμένου από Εικόνα (How to Extract Text)

Με τη μηχανή έτοιμη, δώστε της την προεπεξεργασμένη εικόνα. Η μέθοδος `Recognize` επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει το ακατέργαστο κείμενο και τις βαθμολογίες εμπιστοσύνης.

```csharp
        // Perform the actual OCR
        OcrResult ocrResult = ocrEngine.Recognize(processedImage);
```

> **Επισκόπηση αποτελέσματος:** Το `ocrResult.Text` περιέχει το απλό κείμενο, ενώ το `ocrResult.Confidence` (αν το ερωτήσετε) σας λέει πόσο σίγουρη είναι η μηχανή για κάθε γραμμή.

## Βήμα 7 – Εξαγωγή του Αναγνωρισμένου Κειμένου

Τέλος, εκτυπώστε το εξαγόμενο κείμενο στην κονσόλα—ή γράψτε το σε αρχείο, βάση δεδομένων, ό,τι ταιριάζει στη ροή εργασίας σας.

```csharp
        // Show the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Το πλήρες πρόγραμμα είναι τώρα εκτελέσιμο. Κατασκευάστε και τρέξτε το, και θα δείτε καθαρό, αναγνώσιμο κείμενο παρόλο που η αρχική εικόνα ήταν κεκλιμένη και θορυβώδης.

![how to deskew image example](/images/deskew-demo.png "Demo of how to deskew image using Aspose OCR")

*Το παραπάνω screenshot δείχνει πριν‑και‑μετά της deskewed εικόνας, απεικονίζοντας την επίδραση της αλυσίδας προεπεξεργασίας.*

## Περιπτώσεις Άκρων & Συχνές Ερωτήσεις

### Τι γίνεται αν η εικόνα είναι περιστραμμένη περισσότερο από 5°;

Αυξήστε το `angleThreshold` στην κλήση `Deskew`. Ο αλγόριθμος θα εξακολουθήσει να ανιχνεύει αυτόματα τη σωστή γωνία, απλώς μέσα σε μεγαλύτερο παράθυρο αναζήτησης.

### Το έγγραφό μου περιέχει χρωματιστό κείμενο—η `RemoveBackground` το καταστρέφει;

Η `RemoveBackground` λειτουργεί πάνω στη φωτεινότητα, έτσι το χρωματιστό κείμενο μετατρέπεται σε γκρι κλίμακα πριν τον καθαρισμό. Αν χρειάζεται να διατηρήσετε το χρώμα για επόμενη επεξεργασία, παραλείψτε αυτό το βήμα και βασιστείτε μόνο στην απενεργοποίηση θορύβου.

### Πώς να διαχειριστώ PDF πολλαπλών σελίδων;

Μετατρέψτε κάθε σελίδα PDF σε εικόνα (π.χ., χρησιμοποιώντας Aspose.PDF), μετά δώστε κάθε εικόνα στην ίδια αλυσίδα. Επανάληψη πάνω στις σελίδες και συνένωση των συμβολοσειρών `ocrResult.Text`.

### Μπορώ να βελτιώσω την ακρίβεια για χειρόγραφες σημειώσεις;

Σκεφτείτε να ενεργοποιήσετε το `ocrEngine.Options.UseNeuralNetwork = true;` (διαθέσιμο σε νεότερες εκδόσεις Aspose) και αυξήστε την ανάλυση της εικόνας τουλάχιστον στα 300 dpi πριν την επεξεργασία.

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω βρίσκεται ολόκληρο το αρχείο πηγαίου κώδικα με όλες τις απαραίτητες δηλώσεις `using` και σχόλια. Επικολλήστε το σε ένα νέο έργο κονσόλας και πατήστε **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the original image (skewed, noisy, etc.)
            Image originalImage = Image.Load("YOUR_DIRECTORY/skewed_noisy.jpg");

            // 2️⃣ Deskew – auto‑detect tilt up to 5°
            Image deskewed = ImageFilters.Deskew(originalImage, angleThreshold: 5);

            // 3️⃣ Denoise – smooth out speckles
            Image denoised = deskewed.Denoise();

            // 4️⃣ Remove background – boost contrast
            Image processedImage = denoised.RemoveBackground();

            // 5️⃣ Initialise OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 6️⃣ Recognize text from the cleaned image
            OcrResult ocrResult = ocrEngine.Recognize(processedImage);

            // 7️⃣ Output the extracted text
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**Αναμενόμενη έξοδος** (παράδειγμα για απλό τιμολόγιο):

```
=== OCR Output ===
Invoice #12345
Date: 2025‑12‑01
Total: $1,250.00
Thank you for your business!
```

Αν η έξοδος φαίνεται ακατάληπτη, ελέγξτε ξανά ότι η πηγή εικόνας είναι αρκετά καθαρή και ότι η γωνία deskew δεν είναι μεγαλύτερη από το όριο που ορίσατε.

## Συμπέρασμα

Καλύψαμε **how to deskew image** βήμα προς βήμα, δείξαμε **how to remove background**, επιδείξαμε **how to extract text** μέσω προεπεξεργασίας, και τελικά χρησιμοποιήσαμε το Aspose OCR για **recognize text from image**. Ολόκληρη η αλυσίδα ζει σε ένα συμπαγές πρόγραμμα C# που μπορείτε να επεκτείνετε για επεξεργασία σε παρτίδες, μετατροπή PDF ή ενσωμάτωση σε μεγαλύτερο σύστημα διαχείρισης εγγράφων.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να τροφοδοτήσετε έναν φάκελο σαρωμένων PDF σε αυτήν την αλυσίδα, ή πειραματιστείτε με διαφορετικές ρυθμίσεις denoise για να δείτε πώς επηρεάζουν τις βαθμολογίες εμπιστοσύνης. Όσο περισσότερο παίζετε με τις παραμέτρους, τόσο καλύτερα θα κατανοήσετε τις ανταλλαγές μεταξύ ταχύτητας και ακρίβειας.

Έχετε ερωτήσεις ή μια δύσκολη εικόνα που δεν συνεργάζεται; Αφήστε ένα σχόλιο παρακάτω, και ας το αντιμετωπίσουμε μαζί. Καλή προγραμματιστική, και εύχομαι τα αποτελέσματα OCR σας πάντα να είναι κρυστάλλινα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}