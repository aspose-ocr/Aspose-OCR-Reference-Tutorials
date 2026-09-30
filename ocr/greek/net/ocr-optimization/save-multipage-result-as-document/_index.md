---
date: 2026-04-29
description: Μάθετε πώς να μετατρέπετε εικόνες σε PDF με C# χρησιμοποιώντας το Aspose.OCR,
  να αποθηκεύετε αποτελέσματα OCR πολλαπλών σελίδων ως έγγραφα και να εξάγετε κείμενο
  από εικόνες με C#.
keywords:
- convert images to pdf
- extract text from images
- c# ocr library
- convert images to xlsx
- generate pdf from tiff
linktitle: Μετατροπή εικόνων σε PDF C# – Αποθήκευση αποτελέσματος OCR πολλαπλών σελίδων
second_title: Aspose.OCR .NET API
title: Μετατροπή εικόνων σε PDF C# – Αποθήκευση αποτελέσματος OCR πολλαπλών σελίδων
url: /el/net/ocr-optimization/save-multipage-result-as-document/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή Εικόνων σε PDF C# – Αποθήκευση Πολυσελίδας Αποτελέσματος OCR

## Εισαγωγή

Σε αυτό το tutorial θα ανακαλύψετε πώς να **convert images to PDF C#** χρησιμοποιώντας τη ισχυρή βιβλιοθήκη **Aspose.OCR** για .NET. Είτε χρειάζεστε να **convert scanned TIFF files to searchable PDFs**, να εξάγετε κείμενο από εικόνες για εξόρυξη δεδομένων, είτε να δημιουργήσετε ένα βιβλίο εργασίας Excel από μια δέσμη εικόνων, αυτός ο οδηγός σας καθοδηγεί βήμα προς βήμα με σαφείς εξηγήσεις, πρακτικές συμβουλές και προτάσεις βέλτιστων πρακτικών.

## Γρήγορες Απαντήσεις
- **What does this tutorial cover?** Μετατροπή πολλαπλών εικόνων σε PDF, Docx, Text και Xlsx χρησιμοποιώντας το Aspose.OCR σε C# και αποθήκευση του αποτελέσματος OCR ως πολυσελίδα έγγραφο.  
- **Which output formats are supported?** Docx, Text, Pdf και Xlsx (μπορείτε επίσης να εξάγετε PDF απευθείας).  
- **Do I need a license?** Μια δωρεάν δοκιμή λειτουργεί για αξιολόγηση· απαιτείται μόνιμη άδεια για παραγωγή.  
- **What .NET versions are compatible?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **Can I extract text while converting?** Ναι—χρησιμοποιήστε τα αποτελέσματα OCR για να εξάγετε αναζητήσιμο κείμενο πριν από την αποθήκευση.

## Τι είναι το “convert images to PDF C#”;

Η μετατροπή εικόνων σε PDF σε C# σημαίνει προγραμματιστική λήψη ενός ή περισσότερων αρχείων bitmap (PNG, JPEG, TIFF κ.λπ.) και δημιουργία ενός εγγράφου PDF που διατηρεί τη οπτική διάταξη, ενώ προαιρετικά ενσωματώνει αναζητήσιμο κείμενο μέσω OCR. Το Aspose.OCR παρέχει μια **c# ocr library** που διαχειρίζεται όλο το workflow, συμπεριλαμβανομένης της υποστήριξης πολυσελίδων και της άμεσης αποθήκευσης σε δημοφιλείς μορφές γραφείου.

## Γιατί να χρησιμοποιήσετε το Aspose.OCR για αυτήν την εργασία;

- **High‑accuracy OCR** που υποστηρίζει δεκάδες γλώσσες.  
- **Multipage processing** – τροφοδοτήστε ολόκληρο φάκελο εικόνων και λάβετε ένα ενιαίο αναζητήσιμο PDF.  
- **Direct export** σε Docx, Text, Pdf και Xlsx χωρίς ανάγκη δεύτερου βήματος μετατροπής.  
- **Pure .NET** – χωρίς εγγενείς εξαρτήσεις, λειτουργεί σε Windows, Linux και cloud runtimes.  

## Προαπαιτούμενα

1. Εγκαταστήστε το Aspose.OCR για .NET. Μπορείτε να το κατεβάσετε [εδώ](https://releases.aspose.com/ocr/net/).  
2. Αποκτήστε μια δωρεάν δοκιμή ή αγορασμένη άδεια – πάρτε δοκιμή [εδώ](https://releases.aspose.com/) ή αγοράστε μία [εδώ](https://purchase.aspose.com/buy).  
3. Ανασκοπήστε την επίσημη [documentation](https://reference.aspose.com/ocr/net/) για να εξοικειωθείτε με το API.  
4. Εγγραφείτε στην κοινότητα στα [support forums](https://forum.aspose.com/c/ocr/16) για βοήθεια με τυχόν προβλήματα.  

Τώρα που όλα είναι έτοιμα, ας ξεκινήσουμε τον κώδικα.

## Εισαγωγή Namespaces

Ξεκινήστε προσθέτοντας τα απαιτούμενα namespaces στο αρχείο C# σας:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using Aspose.OCR;
```

Αυτές οι εισαγωγές σας δίνουν πρόσβαση σε συλλογές, διαχείριση αρχείων, LINQ και τις κλάσεις Aspose OCR.

## Βήμα 1: Ορίστε τον Κατάλογο Εγγράφων σας

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

Αντικαταστήστε `"Your Document Directory"` με το απόλυτο ή σχετικό μονοπάτι όπου βρίσκονται οι πηγαίες εικόνες σας και όπου θέλετε να αποθηκευτούν τα αρχεία εξόδου.

## Βήμα 2: Αρχικοποίηση Aspose.OCR

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

Δημιουργώντας ένα αντικείμενο `AsposeOcr` αποκτάτε πρόσβαση σε όλες τις λειτουργίες OCR, συμπεριλαμβανομένης της ροής εργασίας **convert images to PDF C#**.

## Βήμα 3: Αναγνώριση Εικόνων

```csharp
// Recognize image
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

Η μέθοδος `RecognizeMultipleImages` επεξεργάζεται κάθε αρχείο στη λίστα και επιστρέφει μια συλλογή από `RecognitionResult`. Μπορείτε να δώσετε οποιονδήποτε αριθμό εικόνων, κάτι που είναι ιδανικό για σενάρια **convert scanned images to PDF**.

## Βήμα 4: Αποθήκευση Αποτελεσμάτων σε Προτιμώμενες Μορφές

```csharp
// Save the result in your preferred format
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

Επιλέξτε τη μορφή που ταιριάζει καλύτερα στη ροή εργασίας σας:

- **Docx** – επεξεργάσιμο έγγραφο Word με αναζητήσιμο κείμενο.  
- **Text** – εξαγωγή απλού κειμένου για γρήγορη εξόρυξη δεδομένων (**extract text from images**).  
- **Pdf** – η κλασική έξοδος PDF, ιδανική για αρχειοθέτηση.  
- **Xlsx** – αναπαράσταση φύλλου εργασίας για δομημένα δεδομένα (**convert images to xlsx**).

## Πώς να μετατρέψετε εικόνες σε PDF C# – Ανασκόπηση βήμα‑βήμα

1. **Prepare the folder** με τις εικόνες που θέλετε να μετατρέψετε.  
2. **Create an `AsposeOcr` instance** για πρόσβαση στις λειτουργίες OCR.  
3. **Call `RecognizeMultipleImages`** για να λάβετε τα αποτελέσματα OCR για κάθε αρχείο.  
4. **Save the multipage result** χρησιμοποιώντας `SaveMultipageDocument` στη μορφή που χρειάζεστε.

## Κοινές Περιπτώσεις Χρήσης

- **Digital archiving:** Μετατροπή σαρωμένων συμβάσεων σε αναζητήσιμα PDF.  
- **Data entry automation:** Εξαγωγή κειμένου από αποδείξεις ή τιμολόγια και ενσωμάτωση σε βάση δεδομένων.  
- **Batch processing:** Διαχείριση χιλιάδων εικόνων σε μία εργασία με ελάχιστο κώδικα.  
- **Generate PDF from TIFF:** Ιδανικό για υψηλής ανάλυσης σαρωμένα έγγραφα που πρέπει να διατηρήσουν την αυθεντικότητα.

## Αντιμετώπιση Προβλημάτων & Συμβουλές

- **Large image sets:** Επεξεργαστείτε εικόνες σε μικρότερες δόσεις για αποφυγή αυξήσεων μνήμης.  
- **Image quality:** Βεβαιωθείτε ότι οι εικόνες έχουν τουλάχιστον 300 dpi για βέλτιστη ακρίβεια OCR.  
- **License errors:** Επαληθεύστε ότι το αρχείο άδειας έχει φορτωθεί σωστά πριν καλέσετε τις μεθόδους OCR.  
- **Empty results:** Εάν μια εικόνα δεν μπορεί να διαβαστεί, το αντίστοιχο `RecognitionResult` θα έχει κενή ιδιότητα `Text`—ελέγξτε για null ή κενές συμβολοσειρές πριν την αποθήκευση.  

## Συχνές Ερωτήσεις

**Q: Μπορώ να μετατρέψω εικόνες σε PDF C# χωρίς χρήση OCR;**  
A: Ναι, μπορείτε να χρησιμοποιήσετε το Aspose.PDF ή άλλες βιβλιοθήκες για καθαρή μετατροπή εικόνας‑σε‑PDF, αλλά το OCR προσθέτει αναζητήσιμο κείμενο που κάνει το PDF πολύ πιο χρήσιμο.

**Q: Πώς μπορώ να εξάγω κείμενο από εικόνες C# μετά τη μετατροπή;**  
A: Η λίστα `result` που επιστρέφεται από το `RecognizeMultipleImages` περιέχει μια ιδιότητα `Text` για κάθε σελίδα. Μπορείτε να γράψετε αυτές τις συμβολοσειρές σε αρχείο `.txt` ή να τις επεξεργαστείτε απευθείας στην εφαρμογή σας.

**Q: Είναι δυνατόν να ορίσετε προσαρμοσμένα περιθώρια σελίδας ή προσανατολισμό;**  
A: Κατά την αποθήκευση σε PDF ή Docx, μπορείτε να τροποποιήσετε τη διάταξη του εγγράφου μέσω των API Aspose.Words ή Aspose.PDF πριν καλέσετε το `SaveMultipageDocument`.

**Q: Τι συμβαίνει αν μια εικόνα δεν μπορεί να διαβαστεί;**  
A: Η μηχανή OCR επιστρέφει ένα κενό `RecognitionResult` για αυτή τη σελίδα· μπορείτε να το εντοπίσετε και να παραλείψετε ή να καταγράψετε το προβληματικό αρχείο.

**Q: Υποστηρίζει το API την ανάπτυξη στο cloud;**  
A: Ναι, η βιβλιοθήκη λειτουργεί σε οποιοδήποτε .NET runtime, συμπεριλαμβανομένων των Azure Functions και AWS Lambda, εφόσον το runtime πληροί τις απαιτήσεις έκδοσης.

## Συμπέρασμα

Τώρα έχετε μια πλήρη, έτοιμη για παραγωγή ροή εργασίας για **convert images to PDF C#**, εξαγωγή αναζητήσιμου κειμένου, και ακόμη δημιουργία αρχείων Word, plain‑text ή Excel από μια δέσμη εικόνων. Μη διστάσετε να πειραματιστείτε με διαφορετικές μορφές εξόδου, να προσαρμόσετε τις ρυθμίσεις OCR για συγκεκριμένες γλώσσες, ή να ενσωματώσετε τον κώδικα σε μεγαλύτερους αγωγούς επεξεργασίας εγγράφων.

---

**Τελευταία Ενημέρωση:** 2026-04-29  
**Δοκιμή με:** Aspose.OCR 24.11 for .NET  
**Συγγραφέας:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}