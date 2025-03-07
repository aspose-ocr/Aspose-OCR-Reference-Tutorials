---
title: Προετοιμάστε ορθογώνια στο OCR Image Recognition
linktitle: Προετοιμάστε ορθογώνια στο OCR Image Recognition
second_title: Aspose.OCR .NET API
description: Ξεκλειδώστε τις δυνατότητες του Aspose.OCR για .NET με τον ολοκληρωμένο οδηγό μας. Μάθετε βήμα προς βήμα πώς να προετοιμάζετε ορθογώνια για αναγνώριση εικόνας. Αναβαθμίστε τις εφαρμογές σας .NET με απρόσκοπτη ενσωμάτωση OCR.
weight: 11
url: /el/net/ocr-optimization/prepare-rectangles/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προετοιμάστε ορθογώνια στο OCR Image Recognition

## Εισαγωγή

Στο συνεχώς εξελισσόμενο τοπίο της τεχνολογίας, η οπτική αναγνώριση χαρακτήρων (OCR) παίζει καθοριστικό ρόλο στη μετατροπή των εικόνων σε κείμενο αναγνώσιμο από μηχανή. Το Aspose.OCR για .NET ξεχωρίζει ως μια ισχυρή λύση για προγραμματιστές που αναζητούν απρόσκοπτη ενσωμάτωση των δυνατοτήτων OCR στις εφαρμογές τους .NET. Σε αυτόν τον περιεκτικό οδηγό, θα εξερευνήσουμε τη διαδικασία προετοιμασίας ορθογωνίων στην αναγνώριση εικόνας OCR χρησιμοποιώντας το Aspose.OCR για .NET.

## Προαπαιτούμενα

Πριν βουτήξετε στο σεμινάριο, βεβαιωθείτε ότι έχετε τις ακόλουθες προϋποθέσεις:

- Γνώση εργασίας για την ανάπτυξη .NET.
-  Εγκαταστάθηκε το Aspose.OCR για τη βιβλιοθήκη .NET. Μπορείτε να το κατεβάσετε[εδώ](https://releases.aspose.com/ocr/net/).
- Μια βασική κατανόηση των εννοιών αναγνώρισης εικόνας.

## Εισαγωγή χώρων ονομάτων

Ας ξεκινήσουμε εισάγοντας τους απαραίτητους χώρους ονομάτων για να ξεκινήσουμε το ταξίδι μας στο OCR:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Βήμα 1: Ρυθμίστε τον Κατάλογο Εγγράφων σας

 Ξεκινήστε καθορίζοντας τον κατάλογο όπου αποθηκεύονται τα έγγραφά σας. Αντικαθιστώ`"Your Document Directory"` με την πραγματική διαδρομή προς τα έγγραφά σας.

```csharp
// Η διαδρομή προς τον κατάλογο εγγράφων.
string dataDir = "Your Document Directory";

// Αρχικοποιήστε μια παρουσία του AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Βήμα 2: Αναγνώριση εικόνας με πολλαπλά ορθογώνια

Σε αυτό το βήμα, θα δείξουμε πώς να αναγνωρίζετε κείμενο από μια εικόνα χρησιμοποιώντας πολλά ορθογώνια. Ακολουθήστε αυτά τα υποβήματα:

### 2.1 Ορίστε ορθογώνια

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

### 2.2 Εκτελέστε Αναγνώριση OCR

```csharp
// πρώτη περίπτωση
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Εμφάνιση του αναγνωρισμένου κειμένου
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

## Βήμα 3: Αναγνώριση εικόνας με τις ρυθμίσεις αναγνώρισης

Σε αυτό το βήμα, θα παρουσιάσουμε μια εναλλακτική μέθοδο χρησιμοποιώντας το RecognitionSettings για την αναγνώριση εικόνας:

### 3.1 Καθορισμός ρυθμίσεων αναγνώρισης

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

### 3.2 Εμφάνιση αναγνωρισμένου κειμένου

```csharp
// Εμφάνιση του αναγνωρισμένου κειμένου
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## συμπέρασμα

Συγχαρητήρια! Πραγματοποιήσατε με επιτυχία την πλοήγηση στη διαδικασία προετοιμασίας ορθογωνίων στην αναγνώριση εικόνας OCR χρησιμοποιώντας το Aspose.OCR για .NET. Αυτός ο οδηγός σάς δίνει τη δυνατότητα να ενσωματώνετε απρόσκοπτα το OCR στις εφαρμογές σας .NET, ενισχύοντας τις δυνατότητές τους για αναγνώριση κειμένου.

### Συχνές ερωτήσεις

### Ε1: Μπορώ να χρησιμοποιήσω το Aspose.OCR για .NET με άλλα πλαίσια .NET;

A1: Ναι, το Aspose.OCR για .NET είναι συμβατό με διάφορα πλαίσια .NET.

### Ε2: Υπάρχει διαθέσιμη δωρεάν δοκιμή για το Aspose.OCR για .NET;

 Α2: Απολύτως! Μπορείτε να αποκτήσετε πρόσβαση στη δωρεάν δοκιμή[εδώ](https://releases.aspose.com/).

### Ε3: Πώς μπορώ να λάβω υποστήριξη για το Aspose.OCR για .NET;

 A3: Επισκεφθείτε το[Aspose.OCR φόρουμ](https://forum.aspose.com/c/ocr/16) για αποκλειστική υποστήριξη.

### Ε4: Μπορώ να αποκτήσω μια προσωρινή άδεια για σκοπούς δοκιμής;

 A4: Ναι, μπορείτε να αποκτήσετε προσωρινή άδεια[εδώ](https://purchase.aspose.com/temporary-license/).

### Ε5: Πού μπορώ να βρω την τεκμηρίωση για το Aspose.OCR για .NET;

 A5: Η τεκμηρίωση είναι διαθέσιμη[εδώ](https://reference.aspose.com/ocr/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
