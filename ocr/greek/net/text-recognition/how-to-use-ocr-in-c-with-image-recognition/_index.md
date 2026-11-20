---
category: general
date: 2026-11-20
description: Πώς να χρησιμοποιήσετε OCR σε C# για την αναγνώριση κειμένου από μια
  εικόνα. Μάθετε πώς να φορτώνετε εικόνα OCR, να ορίζετε τη γλώσσα OCR και να εξάγετε
  κείμενο από αρχεία JPEG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use OCR
- recognize text image
- load image OCR
- recognize text JPEG
- set OCR language
language: el
lastmod: 2026-11-20
og_description: Πώς να χρησιμοποιήσετε OCR σε C# για την εξαγωγή κειμένου από εικόνες.
  Αυτός ο οδηγός δείχνει τη φόρτωση μιας εικόνας, τον καθορισμό της γλώσσας OCR και
  την αναγνώριση κειμένου από αρχεία JPEG.
og_image_alt: Screenshot of C# code demonstrating how to use OCR to recognize text
  from an image
og_title: Πώς να χρησιμοποιήσετε OCR σε C# – πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: How to use OCR in C# to recognize text from an image. Learn to load
    image OCR, set OCR language, and extract text from JPEG files.
  headline: How to use OCR in C# with image recognition
  type: TechArticle
tags:
- OCR
- C#
- Image processing
- Text extraction
title: Πώς να χρησιμοποιήσετε OCR σε C# με αναγνώριση εικόνας
url: /el/net/text-recognition/how-to-use-ocr-in-c-with-image-recognition/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να χρησιμοποιήσετε OCR σε C# με αναγνώριση εικόνας

Αν χρειάζεστε **πώς να χρησιμοποιήσετε OCR** σε μια εφαρμογή C#, αυτός ο οδηγός σας καθοδηγεί βήμα‑βήμα σε όλη τη διαδικασία. Είτε ψηφιοποιείτε σαρωμένα συμβόλαια είτε εξάγετε πληροφορίες από φωτογραφίες, θα μάθετε να **αναγνωρίζετε κείμενο σε εικόνα** γρήγορα και αξιόπιστα.

Το tutorial καλύπτει τη φόρτωση μιας εικόνας, τη ρύθμιση της μηχανής OCR και την ανάκτηση του αναγνωρισμένου κειμένου από αρχεία JPEG. Στο τέλος θα έχετε ένα αυτόνομο, εκτελέσιμο παράδειγμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 (ή νεότερη) εγκατεστημένο.  
* Πρόσβαση σε βιβλιοθήκη OCR που παρέχει `OcrEngine`, `ImageStream` και μονάδες γλώσσας (π.χ. **Leadtools**, **Aspose.OCR**, ή οποιοδήποτε συμβατό πακέτο).  
* Ένα δείγμα εικόνας με όνομα `sample.jpg` σε γνωστό φάκελο.

Δεν απαιτούνται πρόσθετες εξωτερικές υπηρεσίες — η μηχανή OCR θα κατεβάσει αυτόματα τα ελλιπή πακέτα γλώσσας.

## Βήμα 1: Φόρτωση της εικόνας για OCR

Η φόρτωση της εικόνας είναι το πρώτο βήμα σε οποιαδήποτε ροή εργασίας OCR. Ο παρακάτω κώδικας δημιουργεί ένα `ImageStream` από ένα αρχείο JPEG στον δίσκο.

```csharp
// Step 1: Load the image to be recognized
var imagePath = Path.Combine("YOUR_DIRECTORY", "sample.jpg");
var image = ImageStream.FromFile(imagePath);
```

*Γιατί είναι σημαντικό:* Το αντικείμενο `ImageStream` αφαιρεί την πολυπλοκότητα της διαχείρισης αρχείων και παρέχει τα δεδομένα εικονοστοιχείων που καταναλώνει η μηχανή OCR. Αν το αρχείο δεν βρεθεί, το `FromFile` ρίχνει μια σαφή εξαίρεση, κάνοντας το debugging πιο απλό.

## Βήμα 2: Δημιουργία στιγμιότυπου μηχανής OCR (auto‑dispose)

Η χρήση ενός μπλοκ `using` εγγυάται ότι οι μη διαχειριζόμενοι πόροι απελευθερώνονται αμέσως μόλις ολοκληρωθεί η εργασία OCR.

```csharp
// Step 2: Create an OCR engine instance (automatically disposes when done)
using var ocrEngine = new OcrEngine();
```

*Συμβουλή:* Η δήλωση `using` προτιμάται έναντι των χειροκίνητων κλήσεων `Dispose()` επειδή εξαλείφει τον κίνδυνο να ξεχάσετε να ελευθερώσετε τη φυσική μνήμη, κάτι που μπορεί να προκαλέσει διαρροές μνήμης σε υπηρεσίες που τρέχουν για μεγάλο χρονικό διάστημα.

## Βήμα 3: Ορισμός γλώσσας OCR (προαιρετικό αλλά συνιστάται)

Αν γνωρίζετε τη γλώσσα του πηγαίου εγγράφου, ο ορισμός της βελτιώνει την ακρίβεια και επιταχύνει την επεξεργασία. Το παράδειγμα ορίζει τη γλώσσα σε Κυριλλική· μπορείτε να την αντικαταστήσετε με οποιοδήποτε υποστηριζόμενο enum γλώσσας.

```csharp
// Step 3 (optional): Specify the language module, e.g., Cyrillic
// The required language pack will be downloaded automatically if missing
ocrEngine.Language = OcrLanguage.Cyrillic;
```

*Γιατί να ορίσετε τη γλώσσα;* Οι μηχανές OCR περιέχουν μοντέλα χαρακτήρων ειδικά για κάθε γλώσσα. Επιλέγοντας το σωστό, μειώνετε τα ψευδώς θετικά και αποφεύγετε περιττές αντικαταστάσεις χαρακτήρων.

## Βήμα 4: Εκτέλεση OCR στην φορτωμένη εικόνα

Τώρα η μηχανή επεξεργάζεται το bitmap και επιστρέφει το αναγνωρισμένο κείμενο ως συμβολοσειρά.

```csharp
// Step 4: Perform OCR on the loaded image
string recognizedText = ocrEngine.Recognize(image);
```

*Ακραία περίπτωση:* Αν η εικόνα είναι χαμηλής ανάλυσης ή υπερβολικά συμπιεσμένη, η μηχανή μπορεί να επιστρέψει μερικά αποτελέσματα. Σκεφτείτε προεπεξεργασία (π.χ. δυαδικοποίηση) για καλύτερα αποτελέσματα.

## Βήμα 5: Εξαγωγή του αναγνωρισμένου κειμένου

Τέλος, εμφανίστε το εξαγόμενο κείμενο στην κονσόλα ή προωθήστε το σε άλλο στοιχείο.

```csharp
// Step 5: Output the recognized text
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(recognizedText);
```

**Αναμενόμενη έξοδος**

```
=== Recognized Text ===
Пример текста, полученного из изображения.
```

Το ακριβές περιεχόμενο εξαρτάται από την πηγή εικόνας, αλλά η κονσόλα θα εμφανίσει τη πλήρη συμβολοσειρά που ανίχνευσε η μηχανή OCR.

## Πλήρες, εκτελέσιμο παράδειγμα

Συνδυάζοντας όλα τα βήματα παίρνουμε ένα σύντομο πρόγραμμα που μπορείτε να μεταγλωττίσετε και να τρέξετε αμέσως.

```csharp
using System;
using System.IO;

// Ensure you reference the OCR library that provides these types
// e.g., using Leadtools.OCR;

class Program
{
    static void Main()
    {
        // Load the image to be recognized
        var imagePath = Path.Combine("YOUR_DIRECTORY", "sample.jpg");
        var image = ImageStream.FromFile(imagePath);

        // Create an OCR engine instance (auto‑dispose)
        using var ocrEngine = new OcrEngine();

        // Optional: set the language (Cyrillic in this case)
        ocrEngine.Language = OcrLanguage.Cyrillic;

        // Perform OCR
        string recognizedText = ocrEngine.Recognize(image);

        // Output the result
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
}
```

Αντιγράψτε τον κώδικα σε ένα νέο έργο console, αντικαταστήστε το `YOUR_DIRECTORY` με τη διαδρομή της εικόνας σας και τρέξτε `dotnet run`. Το πρόγραμμα θα εκτυπώσει το αναγνωρισμένο κείμενο στην κονσόλα.

## Συχνές ερωτήσεις και αντιμετώπιση προβλημάτων

| Ερώτηση | Απάντηση |
|----------|--------|
| **Τι γίνεται αν το πακέτο γλώσσας δεν έχει κατέβει;** | Η βιβλιοθήκη OCR θα προσπαθήσει να το κατεβάσει αυτόματα. Βεβαιωθείτε ότι το μηχάνημα έχει πρόσβαση στο internet ή προ‑εγκαταστήστε το πακέτο γλώσσας σύμφωνα με την τεκμηρίωση της βιβλιοθήκης. |
| **Μπορώ να αναγνωρίσω κείμενο από αρχεία PNG ή BMP;** | Ναι. Το `ImageStream.FromFile` λειτουργεί με οποιαδήποτε μορφή υποστηρίζεται από τη βασική βιβλιοθήκη εικόνων. Απλώς αλλάξτε την επέκταση του αρχείου. |
| **Πώς βελτιώνω την ακρίβεια για θορυβώδεις σαρώσεις;** | Προεπεξεργαστείτε την εικόνα (ρύθμιση αντίθεσης, αφαίρεση θορύβου) πριν τη περάσετε στο `Recognize`. Πολλές βιβλιοθήκες εκθέτουν κλάσεις `ImageProcessor` για αυτό το σκοπό. |
| **Είναι ασφαλές να τρέχω OCR σε αρχεία που ανεβάζουν χρήστες;** | Επικυρώστε το μέγεθος και τον τύπο του αρχείου και εκτελέστε το OCR σε περιβάλλον sandbox για να αποτρέψετε κακόβουλα payloads. |

## Συμπέρασμα

Τώρα γνωρίζετε **πώς να χρησιμοποιήσετε OCR** σε C# για **αναγνώριση κειμένου σε εικόνα**, **φόρτωση εικόνας OCR**, **ορισμό γλώσσας OCR** και **αναγνώριση κειμένου JPEG** αξιόπιστα. Το πλήρες παράδειγμα δείχνει μια καθαρή, διαχειρίσιμη ροή εργασίας που μπορείτε να επεκτείνετε με πρόσθετη προεπεξεργασία, υποστήριξη πολλαπλών γλωσσών ή ενσωμάτωση σε μεγαλύτερους σωλήνες επεξεργασίας εγγράφων.

### Επόμενα βήματα

* Εξερευνήστε την επεξεργασία παρτίδων με βρόχο πάνω σε έναν φάκελο JPEG.  
* Συνδυάστε OCR με Επεξεργασία Φυσικής Γλώσσας (NLP) για εξαγωγή δομημένων δεδομένων.  
* Πειραματιστείτε με άλλες μονάδες γλώσσας όπως `OcrLanguage.English` ή `OcrLanguage.Arabic`.  

Αν προσαρμόσετε τον κώδικα στις δικές σας ανάγκες, καλή προγραμματιστική δουλειά!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Use Windows.Media.Ocr to recognize text image in C# – Full OCR Guide](/ocr/english/net/text-recognition/recognize-text-image-in-c-full-ocr-guide/)
- [How to Use OCR in C# – Extract Text from Image Asynchronously](/ocr/english/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-asynchronously/)
- [How to Use OCR in C# – Extract Text from Image with Aspose OCR](/ocr/english/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-with-aspose-ocr/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}