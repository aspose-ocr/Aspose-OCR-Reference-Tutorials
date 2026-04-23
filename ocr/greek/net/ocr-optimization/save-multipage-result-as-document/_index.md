---
date: 2026-04-23
description: Μάθετε πώς να μετατρέπετε εικόνες σε PDF με C# χρησιμοποιώντας το Aspose.OCR,
  να αποθηκεύετε αποτελέσματα OCR πολλαπλών σελίδων ως έγγραφα και να εξάγετε κείμενο
  από εικόνες.
keywords:
- extract text from images
- batch image to pdf
- convert scanned images pdf
linktitle: Μετατροπή εικόνων σε PDF C# – Αποθήκευση αποτελέσματος OCR πολλαπλών σελίδων
second_title: Aspose.OCR .NET API
title: Εξαγωγή κειμένου από εικόνες – Μετατροπή εικόνων σε PDF C#
url: /el/net/ocr-optimization/save-multipage-result-as-document/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Εικόνες – Μετατροπή Εικόνων σε PDF C#

## Εισαγωγή

Σε αυτό το tutorial θα ανακαλύψετε πώς να **extract text from images** ενώ **convert images to PDF C#** χρησιμοποιώντας το Aspose.OCR για .NET, και στη συνέχεια να αποθηκεύσετε το πολυσελιδικό αποτέλεσμα OCR ως έγγραφο. Είτε χρειάζεστε **batch image to pdf** για αρχειοθέτηση, **convert scanned images pdf** για συμμόρφωση, ή απλώς να εξάγετε αναζητήσιμο κείμενο από εικόνες, θα περάσουμε από κάθε βήμα με σαφείς εξηγήσεις, πρακτικές συμβουλές και συστάσεις βέλτιστων πρακτικών.

## Γρήγορες Απαντήσεις
- **Τι καλύπτει αυτό το tutorial;** Μετατροπή πολλαπλών εικόνων σε PDF/Docx/Txt/Xlsx και εξαγωγή κειμένου από εικόνες με Aspose.OCR σε C#.
- **Ποιοι μορφές εξόδου υποστηρίζονται;** Docx, Text, Pdf, και Xlsx (μπορείτε επίσης να εξάγετε PDF απευθείας).
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή λειτουργεί για αξιολόγηση· απαιτείται μόνιμη άδεια για παραγωγή.
- **Ποιες εκδόσεις .NET είναι συμβατές;** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
- **Μπορώ να εξάγω κείμενο κατά τη μετατροπή;** Ναι—χρησιμοποιήστε τα αποτελέσματα OCR για να εξάγετε κείμενο πριν την αποθήκευση.

## Τι είναι η “extract text from images” και γιατί να τη συνδυάσετε με τη μετατροπή PDF;

Η εξαγωγή κειμένου από εικόνες σημαίνει χρήση OCR (Optical Character Recognition) για τη μετατροπή οπτικών χαρακτήρων σε αναζητήσιμες, επεξεργάσιμες συμβολοσειρές. Όταν **convert images to PDF C#**, ενσωματώνετε αυτές τις συμβολοσειρές στο PDF ώστε το έγγραφο να γίνεται αναζητήσιμο και ευρετηρίσιμο—ιδανικό για ψηφιακή αρχειοθέτηση και εξόρυξη δεδομένων.

## Γιατί να χρησιμοποιήσετε το Aspose.OCR για αυτήν την εργασία;

- **Υψηλή ακρίβεια** σε δεκάδες γλώσσες.  
- **Υποστήριξη πολλαπλών σελίδων** – διαχειριστείτε παρτίδες εικόνων σε μία κλήση (ιδανικό για σενάρια **batch image to pdf**).  
- **Άμεση αποθήκευση** σε δημοφιλείς μορφές γραφείου χωρίς επιπλέον βήματα μετατροπής.  
- **Πλήρης ενσωμάτωση .NET** – χωρίς εγγενείς εξαρτήσεις, λειτουργεί σε Windows, Linux και cloud runtimes.

## Προαπαιτούμενα

1. Εγκατεστημένο Aspose.OCR για .NET. Μπορείτε να το κατεβάσετε [εδώ](https://releases.aspose.com/ocr/net/).  
2. Αποκτήσατε δωρεάν δοκιμή ή αγορασμένη άδεια – λάβετε δοκιμή [εδώ](https://releases.aspose.com/) ή αγοράστε μία [εδώ](https://purchase.aspose.com/buy).  
3. Ανασκόπησε την επίσημη [τεκμηρίωση](https://reference.aspose.com/ocr/net/) για να εξοικειωθείτε με το API.  
4. Συμμετείχατε στην κοινότητα στα [φόρουμ υποστήριξης](https://forum.aspose.com/c/ocr/16) για βοήθεια με τυχόν προβλήματα.  

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

Αντικαταστήστε το `"Your Document Directory"` με την απόλυτη ή σχετική διαδρομή όπου βρίσκονται οι πηγαίες εικόνες σας και όπου θέλετε να αποθηκευτούν τα αρχεία εξόδου.

## Βήμα 2: Αρχικοποίηση Aspose.OCR

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

Δημιουργώντας ένα αντικείμενο `AsposeOcr` έχετε πρόσβαση σε όλες τις λειτουργίες OCR, συμπεριλαμβανομένης της ροής εργασίας **convert images to PDF C#**.

## Βήμα 3: Αναγνώριση Εικόνων

```csharp
// Recognize image
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

Η μέθοδος `RecognizeMultipleImages` επεξεργάζεται κάθε αρχείο στη λίστα και επιστρέφει μια συλλογή από `RecognitionResult`. Μπορείτε να δώσετε οποιονδήποτε αριθμό εικόνων, κάτι που είναι ιδανικό για σενάρια **convert scanned images pdf**.

## Βήμα 4: Αποθήκευση Αποτελεσμάτων σε Επιλεγμένες Μορφές

```csharp
// Save the result in your preferred format
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

Επιλέξτε τη μορφή που ταιριάζει καλύτερα στη συνέχεια της ροής εργασίας σας:

- **Docx** – επεξεργάσιμο έγγραφο Word με αναζητήσιμο κείμενο.  
- **Text** – εξαγωγή απλού κειμένου για γρήγορη εξόρυξη δεδομένων (**extract text from images**).  
- **Pdf** – η κλασική έξοδος PDF, ιδανική για αρχειοθέτηση.  
- **Xlsx** – αναπαράσταση φύλλου εργασίας για δομημένα δεδομένα.

## Συνηθισμένες Περιπτώσεις Χρήσης

- **Ψηφιακή αρχειοθέτηση:** Μετατροπή σαρωμένων συμβάσεων σε αναζητήσιμα PDF.  
- **Αυτοματοποίηση εισαγωγής δεδομένων:** Εξαγωγή κειμένου από αποδείξεις ή τιμολόγια και ενσωμάτωση σε βάση δεδομένων.  
- **Επεξεργασία παρτίδας:** Διαχείριση χιλιάδων εικόνων σε μία εργασία με ελάχιστο κώδικα—ιδανικό για ανάγκες **batch image to pdf**.

## Επίλυση Προβλημάτων & Συμβουλές

- **Μεγάλα σύνολα εικόνων:** Επεξεργαστείτε εικόνες σε μικρότερες παρτίδες για να αποφύγετε αυξήσεις μνήμης.  
- **Ποιότητα εικόνας:** Βεβαιωθείτε ότι οι εικόνες είναι τουλάχιστον 300 dpi για βέλτιστη ακρίβεια OCR.  
- **Σφάλματα άδειας:** Επαληθεύστε ότι το αρχείο άδειας έχει φορτωθεί σωστά πριν καλέσετε τις μεθόδους OCR.  
- **Κενά αποτελέσματα:** Η μηχανή OCR επιστρέφει κενό `RecognitionResult` για μη αναγνώσιμες σελίδες· ελέγξτε το `result[i].Text` για null ή κενές συμβολοσειρές και διαχειριστείτε ανάλογα.

## Συχνές Ερωτήσεις

**Ε: Μπορώ να μετατρέψω εικόνες σε PDF C# χωρίς χρήση OCR;**  
Α: Ναι, μπορείτε να χρησιμοποιήσετε Aspose.PDF ή άλλες βιβλιοθήκες για καθαρή μετατροπή εικόνας‑σε‑PDF, αλλά το OCR προσθέτει αναζητήσιμο κείμενο.

**Ε: Πώς εξάγω κείμενο από εικόνες C# μετά τη μετατροπή;**  
Α: Η λίστα `result` που επιστρέφεται από το `RecognizeMultipleImages` περιέχει ιδιότητες `Text` που μπορείτε να γράψετε σε αρχείο `.txt` ή να επεξεργαστείτε άμεσα.

**Ε: Είναι δυνατόν να ορίσετε προσαρμοσμένα περιθώρια σελίδας ή προσανατολισμό;**  
Α: Κατά την αποθήκευση σε PDF ή Docx, μπορείτε να τροποποιήσετε τη διάταξη του εγγράφου μέσω των API Aspose.Words ή Aspose.PDF πριν καλέσετε το `SaveMultipageDocument`.

**Ε: Τι συμβαίνει αν μια εικόνα δεν μπορεί να διαβαστεί;**  
Α: Η μηχανή OCR επιστρέφει κενό `RecognitionResult` για αυτή τη σελίδα· μπορείτε να ελέγξετε το `result[i].Text` για null ή κενές συμβολοσειρές και να το διαχειριστείτε ανάλογα.

**Ε: Υποστηρίζει το API την ανάπτυξη στο cloud;**  
Α: Ναι, η βιβλιοθήκη λειτουργεί σε οποιοδήποτε runtime .NET, συμπεριλαμβανομένων των Azure Functions και AWS Lambda, εφόσον το runtime πληροί τις απαιτήσεις έκδοσης.

---

**Τελευταία ενημέρωση:** 2026-04-23  
**Δοκιμή με:** Aspose.OCR 24.11 for .NET  
**Συγγραφέας:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}