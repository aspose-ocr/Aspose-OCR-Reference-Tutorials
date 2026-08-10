---
date: 2026-07-23
description: Μάθετε πώς η ocr library for .net εξάγει κείμενο εικόνας C# χρησιμοποιώντας
  το Aspose.OCR. Αυτός ο οδηγός καλύπτει το πολυγλωσσικό OCR, την επιλογή γλώσσας
  και πρακτικές συμβουλές.
keywords:
- ocr library for .net
- extract image text c#
- Aspose.OCR
- multilingual OCR
lastmod: 2026-07-23
linktitle: Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας το Aspose.OCR
og_description: Η ocr library for .net επιτρέπει την εξαγωγή κειμένου εικόνας C# με
  το Aspose.OCR. Λάβετε πολυγλωσσικό OCR, επιλογή γλώσσας και παραδείγματα κώδικα
  βήμα‑βήμα.
og_image_alt: 'Guide: Extract image text C# using Aspose.OCR OCR library for .NET'
og_title: ocr library for .net – Εξαγωγή κειμένου εικόνας C#
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Learn how the ocr library for .net extracts image text C# using Aspose.OCR.
    This guide covers multilingual OCR, language selection, and practical tips.
  headline: ocr library for .net – Extract image text C#
  type: TechArticle
- questions:
  - answer: Yes, Aspose.OCR supports over 30 languages, providing flexibility for
      multilingual OCR tasks.
    question: Is Aspose.OCR suitable for multilingual text recognition?
  - answer: Absolutely! Adjust parameters like `AutoSkew`, `SkewAngle`, and `LineDetectionMode`
      to optimise results for different scenarios.
    question: Can I fine‑tune OCR settings for specific image characteristics?
  - answer: Visit the [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) for support
      and discussions with the community.
    question: Where can I find additional support or community discussions?
  - answer: Yes, explore the [free trial](https://releases.aspose.com/) to experience
      the capabilities of Aspose.OCR.
    question: Is there a free trial available?
  - answer: To purchase, visit the [purchase page](https://purchase.aspose.com/buy).
    question: How can I purchase Aspose.OCR for .NET?
  type: FAQPage
second_title: Aspose.OCR .NET API
tags:
- ocr library
- Aspose.OCR
- C# OCR
- image text extraction
title: ocr library for .net – Εξαγωγή κειμένου εικόνας C#
url: /el/net/ocr-configuration/ocr-operation-with-language-selection/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR

## Εισαγωγή

Αν χρειάζεστε **extract image text C#** από εικόνες ή PDF σε μια εφαρμογή .NET, το Aspose.OCR είναι μια ισχυρή **ocr library for .net** που παρέχει γρήγορη, ακριβή και γλωσσικά‑συνειδητή αναγνώριση. Σε αυτό το tutorial θα περάσουμε από ένα πραγματικό παράδειγμα που δείχνει την αναγνώριση εικόνας OCR με επιλογή γλώσσας, ώστε να μπορείτε να εξάγετε πολυγλωσσικό κείμενο από εικόνες με λίγες μόνο γραμμές κώδικα. Στο τέλος θα δείτε γιατί αυτή η προσέγγιση είναι μια αξιόπιστη επιλογή για παραγωγικά φορτία εργασίας και πόσο εύκολο είναι να ενσωματώσετε το OCR στα C# projects σας.

## Γρήγορες Απαντήσεις
- **Τι κάνει το Aspose.OCR;** Αναγνωρίζει τυπωμένο και χειρόγραφο κείμενο σε εικόνες και επιστρέφει το εξαγόμενο κείμενο.  
- **Μπορώ να επιλέξω τη γλώσσα;** Ναι – μπορείτε να καθορίσετε οποιαδήποτε υποστηριζόμενη γλώσσα, όπως English, German, Spanish, Chinese, κ.λπ.  
- **Χρειάζομαι άδεια για ανάπτυξη;** Μια δωρεάν δοκιμή λειτουργεί για αξιολόγηση· απαιτείται άδεια για χρήση σε παραγωγή.  
- **Ποιες εκδόσεις .NET υποστηρίζονται;** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Είναι η διόρθωση κλίσης αυτόματη;** Μπορείτε να ενεργοποιήσετε το `AutoSkew` και να ρυθμίσετε λεπτομερώς τη ρύθμιση `SkewAngle`.  

`AutoSkew` ανιχνεύει και διορθώνει αυτόματα την κλίση της εικόνας. `SkewAngle` επιτρέπει τη χειροκίνητη ρύθμιση της γωνίας περιστροφής.

## Τι είναι το “extract image text C#”;

Η εξαγωγή κειμένου εικόνας σε C# σημαίνει χρήση μιας βιβλιοθήκης για ανάγνωση του οπτικού περιεχομένου μιας εικόνας (PNG, JPEG, TIFF, κλπ.) και μετατροπή του σε αναζητήσιμο, επεξεργάσιμο κείμενο. **ocr library for .net** Aspose.OCR εκτελεί αυτή τη μετατροπή τοπικά, διατηρώντας τα δεδομένα εντός των εγκαταστάσεων και αποφεύγοντας εξωτερικές κλήσεις υπηρεσιών.

## Γιατί να επιλέξετε το Aspose.OCR για εργασίες OCR;

Το Aspose.OCR παρέχει **95 %+ ακρίβεια** σε τυπικές τυπωμένες γραμματοσειρές και μπορεί να επεξεργαστεί **έως 300 σελίδες ανά λεπτό** σε έναν τυπικό διακομιστή 2.5 GHz, καθιστώντας το μία από τις πιο γρήγορες λύσεις **ocr library for .net**. Περιλαμβάνει επίσης ενσωματωμένα πακέτα γλωσσών, ώστε να μην χρειάζεστε ποτέ πόρους τρίτων, και λειτουργεί εξ ολοκλήρου offline για μέγιστη ασφάλεια.

## Προαπαιτούμενα

Πριν βυθιστούμε στον κώδικα, βεβαιωθείτε ότι έχετε τα παρακάτω προαπαιτούμενα:

- Aspose.OCR for .NET: Βεβαιωθείτε ότι έχετε εγκαταστήσει τη βιβλιοθήκη Aspose.OCR. Μπορείτε να τη κατεβάσετε από τη [Aspose.OCR for .NET download page](https://releases.aspose.com/ocr/net/).
- Development Environment: Ρυθμίστε ένα περιβάλλον εργασίας με μια εφαρμογή .NET. Αν δεν το έχετε κάνει ακόμη, ανατρέξτε στην [documentation](https://reference.aspose.com/ocr/net/) για λεπτομερείς οδηγίες.

## Εισαγωγή Namespaces

Στην εφαρμογή .NET σας, ξεκινήστε εισάγοντας τα απαραίτητα namespaces:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Βήμα 1: Αρχικοποίηση Aspose.OCR

`OcrEngine` είναι η βασική κλάση του Aspose.OCR που εκτελεί οπτική αναγνώριση χαρακτήρων σε εικόνες. Ξεκινήστε δημιουργώντας μια παρουσία αυτής της κλάσης· αυτό θέτει τη βάση για όλες τις επόμενες λειτουργίες OCR.

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Βήμα 2: Καθορισμός Διαδρομής Εικόνας

Ορίστε την απόλυτη ή σχετική διαδρομή προς την εικόνα που θέλετε να επεξεργαστείτε. Η διαδρομή πρέπει να δείχνει σε ένα αναγνώσιμο αρχείο· διαφορετικά η μηχανή θα εγείρει εξαίρεση.

```csharp
// Image Path
string fullPath = dataDir + "sample.png";
```

## Βήμα 3: Αναγνώριση Εικόνας με Επιλογή Γλώσσας

`RecognizeImage` είναι η μέθοδος που σαρώει το παρεχόμενο bitmap, εφαρμόζει μοντέλα γλώσσας και επιστρέφει ένα αντικείμενο `RecognitionResult` που περιέχει το εξαγόμενο κείμενο. Ορίζοντας την ιδιότητα `Language` λέτε στη μηχανή ποιους γλωσσικούς κανόνες να εφαρμόσει, βελτιώνοντας δραστικά την ακρίβεια για περιεχόμενο μη‑Αγγλικών.

Η ιδιότητα `Language` επιλέγει το μοντέλο γλώσσας OCR που θα χρησιμοποιηθεί.

```csharp
// Recognize image           
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    SkewAngle = 0.2F,
    Language = Language.Eng, // Choose the language: none, eng, deu, por, spa, fra, ita, cze, dan, dum, est, fin, lav, lit, nor, pol, rum, srp_hrv, slk, slv, swe, chi
});
```

## Βήμα 4: Εκτύπωση και Εμφάνιση Αποτελεσμάτων

Μετά τη λειτουργία OCR, μπορείτε να έχετε πρόσβαση στο αναγνωρισμένο κείμενο, στα πλαίσια περιορισμού για κάθε λέξη, σε τυχόν προειδοποιήσεις, και ακόμη σε μια εξαγωγή JSON για επεξεργασία downstream.

```csharp
// Print result
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
// ExEnd:1
```

## Πώς να εξάγετε κείμενο εικόνας C# με επιλογή γλώσσας;

Φορτώστε την εικόνα σας με `new OcrEngine()` και ορίστε `engine.Language = Language.English` (ή οποιαδήποτε υποστηριζόμενη γλώσσα) πριν καλέσετε `engine.RecognizeImage(imagePath)`. Η μέθοδος επιστρέφει το πλήρες κείμενο σε μια ενιαία συμβολοσειρά, την οποία μπορείτε στη συνέχεια να εμφανίσετε, να αποθηκεύσετε ή να τη δώσετε σε άλλες υπηρεσίες. Αυτό το μοτίβο δύο βημάτων λειτουργεί για όλες τις υποστηριζόμενες γλώσσες και δεν απαιτεί εξωτερικές εξαρτήσεις.

## Κοινά Προβλήματα και Συμβουλές

- **Incorrect language selection** – Αν το αποτέλεσμα φαίνεται ακατάληπτο, ελέγξτε ξανά ότι η ιδιότητα `Language` ταιριάζει με τη γλώσσα της πηγαίας εικόνας.  
- **Skewed images** – Ενεργοποιήστε το `AutoSkew` ή ρυθμίστε χειροκίνητα το `SkewAngle` για καλύτερη ακρίβεια σε κεκλιμένες σκαναρίσματα.  
- **Large files** – Επεξεργαστείτε μεγάλες εικόνες σε τμήματα ή μειώστε την ανάλυση πριν τις δώσετε στο `RecognizeImage` για εξοικονόμηση μνήμης.  

## Συχνές Ερωτήσεις

**Q: Είναι το Aspose.OCR κατάλληλο για αναγνώριση πολυγλωσσικού κειμένου;**  
A: Ναι, το Aspose.OCR υποστηρίζει πάνω από 30 γλώσσες, παρέχοντας ευελιξία για πολυγλωσσικές εργασίες OCR.

**Q: Μπορώ να ρυθμίσω λεπτομερώς τις ρυθμίσεις OCR για συγκεκριμένα χαρακτηριστικά εικόνας;**  
A: Απολύτως! Ρυθμίστε παραμέτρους όπως `AutoSkew`, `SkewAngle` και `LineDetectionMode` για βελτιστοποίηση των αποτελεσμάτων σε διαφορετικά σενάρια.

**Q: Πού μπορώ να βρω πρόσθετη υποστήριξη ή συζητήσεις της κοινότητας;**  
A: Επισκεφθείτε το [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) για υποστήριξη και συζητήσεις με την κοινότητα.

**Q: Υπάρχει διαθέσιμη δωρεάν δοκιμή;**  
A: Ναι, εξερευνήστε τη [free trial](https://releases.aspose.com/) για να δοκιμάσετε τις δυνατότητες του Aspose.OCR.

**Q: Πώς μπορώ να αγοράσω το Aspose.OCR για .NET;**  
A: Για αγορά, επισκεφθείτε τη [purchase page](https://purchase.aspose.com/buy).

## Συμπέρασμα

Συγχαρητήρια! Έχετε μάθει **how to extract image text C#** με επιλογή γλώσσας χρησιμοποιώντας το Aspose.OCR για .NET. Αυτό το tutorial σας έδειξε πώς να διαμορφώσετε τη μηχανή OCR, να επιλέξετε τη σωστή γλώσσα και να διαχειριστείτε τα αποτελέσματα, παρέχοντάς σας μια ισχυρή βάση για την κατασκευή πολυγλωσσικών λειτουργιών εξαγωγής κειμένου στις εφαρμογές σας.

---

**Last Updated:** 2026-07-23  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Σχετικά Tutorials

- [αναγνώριση κειμένου εικόνας με Aspose OCR για πολλές γλώσσες](/ocr/net/ocr-settings/working-with-different-languages/)
- [Εξαγωγή Κειμένου από Εικόνες – Ρυθμίσεις OCR με Aspose.OCR](/ocr/net/ocr-settings/)
- [Πώς να Εξάγετε Κείμενο από Εικόνα Χρησιμοποιώντας Aspose.OCR για .NET](/ocr/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}