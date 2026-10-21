---
category: general
date: 2026-10-21
description: Μάθετε πώς να εκτελείτε OCR σε JPG, να εξάγετε κείμενο από εικόνα και
  να φορτώνετε εικόνα για OCR χρησιμοποιώντας το Aspose.OCR σε C#. Πλήρης οδηγός βήμα‑βήμα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- recognize text from jpg
- load image for OCR
- perform OCR on image
language: el
lastmod: 2026-10-21
og_description: Πώς να εκτελέσετε OCR σε μια εικόνα σε C# με το Aspose.OCR. Ακολουθήστε
  αυτόν τον οδηγό για να φορτώσετε εικόνα για OCR, να αναγνωρίσετε κείμενο από JPG
  και να εξάγετε κείμενο από την εικόνα.
og_image_alt: Screenshot showing how to perform OCR on a Cyrillic image in C#
og_title: Πώς να εκτελέσετε OCR σε μια εικόνα σε C# – βήμα‑βήμα οδηγός
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to perform OCR on a JPG, extract text from image and load
    image for OCR using Aspose.OCR in C#. Complete step‑by‑step guide.
  headline: How to perform OCR on an image in C# with Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose.OCR
- Image processing
- Text extraction
title: Πώς να εκτελέσετε OCR σε μια εικόνα σε C# με το Aspose.OCR
url: /el/net/text-recognition/how-to-perform-ocr-on-an-image-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εκτελέσετε OCR σε μια εικόνα με C# και Aspose.OCR

Αν χρειάζεστε **πώς να εκτελέσετε OCR** σε μια εικόνα, αυτό το tutorial σας παρουσιάζει μια πλήρη, έτοιμη προς εκτέλεση λύση. Θα μάθετε πώς να φορτώνετε μια εικόνα για OCR, να αναγνωρίζετε κείμενο από αρχεία JPG και να εξάγετε κείμενο από εικόνα χρησιμοποιώντας τη βιβλιοθήκη Aspose.OCR.

Ο οδηγός καλύπτει τα πάντα, από την εγκατάσταση του πακέτου NuGet μέχρι τη διαχείριση μοντέλων γλώσσας και την εκτύπωση του αναγνωρισμένου αποτελέσματος. Στο τέλος θα μπορείτε να ενσωματώσετε OCR σε οποιοδήποτε .NET project και να επεξεργαστείτε κυριλλικά ή άλλα κείμενα χωρίς να φύγετε από το IDE.

## Τι θα χρειαστείτε

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.7+)
- Visual Studio 2022 (ή οποιονδήποτε επεξεργαστή C#)
- Πρόσβαση στο Internet για την πρώτη εκτέλεση (το Aspose.OCR κατεβάζει αυτόματα το μοντέλο γλώσσας)
- Ένα δείγμα εικόνας, π.χ. `cyrillic_sample.jpg`, τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε από τον κώδικα

## Βήμα 1: Εγκατάσταση Aspose.OCR

Ανοίξτε το NuGet Package Manager και προσθέστε **Aspose.OCR** στο project σας:

```bash
dotnet add package Aspose.OCR
```

Το πακέτο περιλαμβάνει τη μηχανή OCR, τα μοντέλα γλώσσας και τις βοηθητικές κλάσεις που απαιτούνται για την επεξεργασία εικόνας. Δεν απαιτούνται επιπλέον DLL.

## Βήμα 2: Δημιουργία της μηχανής OCR – πώς να εκτελέσετε OCR

Το πρώτο πραγματικό βήμα στο **πώς να εκτελέσετε OCR** είναι η δημιουργία της μηχανής. Αυτό το αντικείμενο διαχειρίζεται ολόκληρη τη διαδικασία αναγνώρισης.

```csharp
using Aspose.OCR;

// Create an OCR engine instance
OcrEngine engine = new OcrEngine();
```

Το `OcrEngine` είναι ελαφρύ· μπορείτε να επαναχρησιμοποιήσετε την ίδια παρουσία για πολλές εικόνες, βελτιώνοντας την απόδοση κατά την επεξεργασία παρτίδων.

## Βήμα 3: Φόρτωση εικόνας για OCR

Πριν από την αναγνώριση πρέπει να παρέχετε τα δεδομένα της εικόνας. Το βήμα **φόρτωση εικόνας για OCR** δέχεται πολλές μορφές, αλλά αυτό το παράδειγμα εστιάζει σε αρχείο JPEG.

```csharp
// Load the image you want to process
engine.Image = OcrImage.FromFile(@"C:\Images\cyrillic_sample.jpg");
```

Η `OcrImage.FromFile` διαβάζει το αρχείο στη μνήμη και το προετοιμάζει για τη μηχανή. Αν η διαδρομή του αρχείου είναι λανθασμένη, ρίχνεται `ArgumentException`, οπότε βεβαιωθείτε ότι η διαδρομή είναι σωστή.

## Βήμα 4: Επιλογή της κατάλληλης γλώσσας (προαιρετικό αλλά συνιστάται)

Αν η εικόνα σας περιέχει κυριλλικούς χαρακτήρες, ορίστε τη γλώσσα σε `Cyrillic`. Το απαιτούμενο μοντέλο κατεβαίνει αυτόματα στην πρώτη εκτέλεση.

```csharp
// Choose the language model
engine.Language = OcrLanguage.Cyrillic;
```

Μπορείτε να αλλάξετε σε άλλες γλώσσες (π.χ. `OcrLanguage.English`) τροποποιώντας αυτήν την ιδιότητα. Η βιβλιοθήκη υποστηρίζει πάνω από 60 γλώσσες.

## Βήμα 5: Αναγνώριση κειμένου από JPG – πώς να εκτελέσετε OCR σε JPEG

Τώρα καλέστε τη μέθοδο `Recognize`. Αυτό είναι το κεντρικό μέρος του **πώς να εκτελέσετε OCR** και μετατρέπει το bitmap σε κείμενο Unicode.

```csharp
// Perform the recognition
engine.Recognize();
```

Η μέθοδος μπλοκάρει μέχρι να ολοκληρωθεί η διαδικασία OCR. Για μεγάλες εικόνες ίσως θελήσετε να το εκτελέσετε σε ξεχωριστό νήμα ώστε η διεπαφή χρήστη να παραμένει ανταποκρινόμενη.

## Βήμα 6: Εξαγωγή κειμένου από εικόνα

Μετά την αναγνώριση, η μηχανή αποθηκεύει το αποτέλεσμα στην ιδιότητα `Text`. Αυτό ολοκληρώνει το βήμα **εξαγωγή κειμένου από εικόνα**.

```csharp
// Retrieve the extracted text
string extractedText = engine.Text;

// Output the recognized text to the console
Console.WriteLine(extractedText);
```

Η έξοδος θα περιέχει ακριβώς τους χαρακτήρες που βρέθηκαν στην εικόνα, διατηρώντας τις αλλαγές γραμμής και την στίξη.

## Πλήρες, εκτελέσιμο παράδειγμα

Συνδυάζοντας όλα τα βήματα παίρνετε ένα ενιαίο πρόγραμμα που μπορείτε να αντιγράψετε, να επικολλήσετε και να τρέξετε:

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 1: Create the OCR engine
        OcrEngine engine = new OcrEngine();

        // Step 2: Load the image for OCR
        engine.Image = OcrImage.FromFile(@"C:\Images\cyrillic_sample.jpg");

        // Step 3: Choose the language model (Cyrillic in this case)
        engine.Language = OcrLanguage.Cyrillic;

        // Step 4: Perform OCR on the image
        engine.Recognize();

        // Step 5: Extract text from image
        string extractedText = engine.Text;

        // Step 6: Output the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(extractedText);
    }
}
```

### Αναμενόμενη έξοδος

Αν το `cyrillic_sample.jpg` περιέχει τη φράση “Привет мир” (Hello world), η κονσόλα θα εμφανίσει:

```
=== OCR Result ===
Привет мир
```

Διαφορετικές γραμματοσειρές ή η ποιότητα της εικόνας μπορεί να επηρεάσουν την ακρίβεια, αλλά το Aspose.OCR γενικά πετυχαίνει >95 % αναγνώριση σε καθαρές εκτυπώσεις.

## Συνηθισμένα προβλήματα και πρακτικές συμβουλές

- **Η ποιότητα της εικόνας μετρά** – JPEG χαμηλής ανάλυσης ή θορυβώδη μειώνουν την ακρίβεια. Προεπεξεργαστείτε την εικόνα (π.χ. αυξήστε την αντίθεση) με `engine.Image.AdjustContrast()` αν χρειάζεται.
- **Λήψη μοντέλου γλώσσας** – η πρώτη εκτέλεση κατεβάζει το μοντέλο στο `%USERPROFILE%\.Aspose\OCR`. Βεβαιωθείτε ότι η διαδικασία έχει δικαίωμα εγγραφής.
- **Επεξεργασία παρτίδας** – επαναχρησιμοποιήστε την ίδια παρουσία `OcrEngine` και αλλάξτε μόνο το `engine.Image` μεταξύ των αρχείων. Αυτό αποφεύγει επαναλαμβανόμενη φόρτωση μοντέλου.
- **Κατανάλωση μνήμης** – μεγάλες εικόνες καταναλώνουν περισσότερη RAM. Καλέστε `engine.Image.Dispose()` μετά από κάθε αναγνώριση αν επεξεργάζεστε πολλά αρχεία σε βρόχο.
- **Ασφάλεια νήματος** – το `OcrEngine` δεν είναι thread‑safe. Δημιουργήστε ξεχωριστή παρουσία ανά νήμα όταν κάνετε παράλληλη επεξεργασία.

## Συμπέρασμα

Τώρα γνωρίζετε **πώς να εκτελέσετε OCR** σε JPEG, **πώς να φορτώσετε εικόνα για OCR**, και **πώς να εξάγετε κείμενο από εικόνα** χρησιμοποιώντας το Aspose.OCR σε C#. Η πλήρης λύση δείχνει πώς να ορίσετε τη γλώσσα, να αναγνωρίσετε κείμενο από JPG και να εκτυπώσετε το αποτέλεσμα, παρέχοντάς σας μια σταθερή βάση για οποιοδήποτε έργο εξαγωγής κειμένου.

Στη συνέχεια, εξερευνήστε σχετικές θεματικές όπως **εκτέλεση OCR σε παρτίδες εικόνων**, ενσωμάτωση OCR σε ASP.NET Core APIs, ή μετατροπή του εξαγόμενου κειμένου σε αναζητήσιμα PDF. Πειραματιστείτε με διαφορετικές γλώσσες και προεπεξεργασία εικόνας για μέγιστη ποιότητα αναγνώρισης.

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Perform OCR in C# – Convert Image to Text with Aspose OCR](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-convert-image-to-text-with-aspose-oc/)
- [How to Perform OCR in C# – Recognize Text from Image](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-recognize-text-from-image/)
- [How to extract text from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}