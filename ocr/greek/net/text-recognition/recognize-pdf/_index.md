---
date: 2026-05-29
description: Μάθετε πώς να κάνετε OCR PDF σε .NET, να εξάγετε κείμενο PDF, να μετατρέψετε
  PDF σε κείμενο και να διαβάσετε κείμενο PDF σε C# χρησιμοποιώντας το Aspose.OCR.
  Αναλυτικός οδηγός για προγραμματιστές .NET.
keywords:
- how to ocr pdf
- read pdf text c#
- extract pdf text c#
- convert scanned pdf searchable
- pdf text extraction .net
linktitle: Πώς να κάνετε OCR PDF σε .NET με το Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-05-29'
  description: Learn how to ocr pdf in .NET, extract text pdf, convert pdf to text,
    and read pdf text c# using Aspose.OCR. Detailed guide for .NET developers.
  headline: How to OCR PDF in .NET with Aspose.OCR (how to ocr pdf)
  type: TechArticle
- questions:
  - answer: Yes. Use the overload of `RecognizePdf` that accepts a password parameter.
    question: Can I extract text from a password‑protected PDF?
  - answer: Aspose.OCR can recognize printed text reliably; handwritten text may require
      additional preprocessing or a specialized engine.
    question: Does OCR work on handwritten PDFs?
  - answer: Processing time scales with page count and image resolution. Splitting
      the document into smaller batches can improve responsiveness.
    question: What is the performance impact on large documents?
  - answer: Inside the `foreach` loop, write `result.Text` to a `StreamWriter` for
      each page.
    question: How do I save the OCR results to a text file?
  - answer: You can create a new searchable PDF by overlaying the OCR text on the
      original pages using Aspose.PDF after extraction.
    question: Is there a way to keep the original PDF layout after OCR?
  type: FAQPage
second_title: Aspose.OCR .NET API
title: Πώς να κάνετε OCR PDF σε .NET με το Aspose.OCR (πώς να κάνετε ocr pdf)
url: /el/net/text-recognition/recognize-pdf/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να κάνετε OCR PDF σε .NET με το Aspose.OCR (πώς να κάνετε ocr pdf)

## Εισαγωγή

Αν ψάχνετε για έναν αξιόπιστο τρόπο **πώς να κάνετε ocr pdf** αρχεία σε περιβάλλον .NET, βρίσκεστε στο σωστό μέρος. Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία εξαγωγής κειμένου από PDF, μετατροπής PDF σε κείμενο και ανάγνωσης κειμένου PDF σε στυλ C# χρησιμοποιώντας τη βιβλιοθήκη Aspose.OCR. Είτε χρειάζεστε επεξεργασία μιας μόνο σελίδας είτε ενός **ocr multi page pdf**, τα παρακάτω βήματα θα σας προσφέρουν μια σταθερή, έτοιμη για παραγωγή λύση.

## Γρήγορες Απαντήσεις
- **Ποια βιβλιοθήκη πρέπει να χρησιμοποιήσω;** Aspose.OCR για .NET  
- **Μπορώ να εξάγω κείμενο από PDF πολλαπλών σελίδων;** Ναι – ορίστε `StartPage` και `PagesNumber` στο `DocumentRecognitionSettings`.  
- **Χρειάζομαι άδεια για παραγωγή;** Απαιτείται εμπορική άδεια· διατίθεται δωρεάν δοκιμαστική έκδοση.  
- **Ποιες εκδόσεις .NET υποστηρίζονται;** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Είναι το OCR η καλύτερη μέθοδος για εξαγωγή κειμένου;** Για σκαναρισμένα PDF ή εικόνες μέσα σε PDF, το OCR είναι απαραίτητο· για εγγενή PDF, ένας parser PDF μπορεί να είναι πιο γρήγορος.

**DocumentRecognitionSettings** ρυθμίζει ποιες σελίδες ενός PDF επεξεργάζονται από τη μηχανή OCR.

## Πώς να κάνετε OCR PDF σε .NET;

Φορτώστε το αρχείο PDF με `new AsposeOcr()` και καλέστε `RecognizePdf` καθορίζοντας `StartPage` και `PagesNumber`; η μέθοδος επιστρέφει μια συλλογή αντικειμένων `RecognitionResult` που περιέχουν το εξαγόμενο κείμενο για κάθε επεξεργασμένη σελίδα. Αυτή η διπλή προσέγγιση διαχειρίζεται έγγραφα μονής και πολλαπλών σελίδων, λειτουργεί με .NET Framework, .NET Core και .NET 5/6, και απαιτεί μόνο λίγες γραμμές κώδικα.

## Τι είναι το OCR και γιατί το χρησιμοποιούμε για PDF;

Η Οπτική Αναγνώριση Χαρακτήρων (OCR) μετατρέπει εικόνες κειμένου—όπως σκαναρισμένες σελίδες—σε αναζητήσιμους, επεξεργάσιμους χαρακτήρες. Όταν ένα PDF περιέχει σκαναρισμένες σελίδες, η παραδοσιακή εξαγωγή κειμένου αποτυγχάνει, καθιστώντας το OCR την προτιμώμενη τεχνική για **extract text pdf** και **convert pdf to text** αξιόπιστα. Συνεπώς, το OCR είναι απαραίτητο για να γίνουν τα σκαναρισμένα PDF αναζητήσιμα και επεξεργάσιμα.

## Γιατί να επιλέξετε το Aspose.OCR για .NET;

- **Υψηλή ακρίβεια** σε περισσότερες από 30 γλώσσες και ευρύ φάσμα γραμματοσειρών.  
- **Ενσωματωμένη υποστήριξη** για PDF πολλαπλών σελίδων, επιτρέποντας τον καθορισμό του εύρους σελίδων προς επεξεργασία.  
- **Απλό API** που ενσωματώνεται άψογα σε έργα C#, διευκολύνοντας το **read pdf text c#** ή **extract pdf text c#**.  
- **Μετρήσιμη απόδοση:** Το Aspose.OCR μπορεί να επεξεργαστεί PDF έως 500 MB χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη, και αναγνωρίζει 30+ γλώσσες με μέση ακρίβεια πάνω από 95 % σε τυπικά σύνολα δοκιμών.

## Προαπαιτούμενα

Πριν βυθιστούμε στον κώδικα, βεβαιωθείτε ότι έχετε τα εξής:

- Το Aspose.OCR για .NET εγκατεστημένο. Αν δεν το έχετε ακόμη, κατεβάστε το από την [τεκμηρίωση Aspose.OCR για .NET](https://reference.aspose.com/ocr/net/).  
- Ένα αρχείο PDF στο οποίο θέλετε να εκτελέσετε OCR. Σημειώστε τη πλήρη διαδρομή του αρχείου στον υπολογιστή σας.

Τώρα που είστε έτοιμοι, ας αρχίσουμε τον κώδικα.

## Εισαγωγή Namespaces

Στην εφαρμογή .NET, εισάγετε το namespace Aspose.OCR για πρόσβαση στη λειτουργικότητα OCR:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Βήμα 1: Αρχικοποίηση Aspose.OCR

`AsposeOcr` είναι η κεντρική κλάση στη βιβλιοθήκη Aspose.OCR που εκτελεί οπτική αναγνώριση χαρακτήρων σε εικόνες και έγγραφα PDF. Εδώ ορίζουμε το φάκελο που περιέχει το PDF μας και δημιουργούμε ένα αντικείμενο `AsposeOcr` που θα εκτελέσει την αναγνώριση.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Βήμα 2: Παροχή Διαδρομής PDF

```csharp
// Image Path
string fullPath = dataDir + "multi_page_1.pdf";
```

Αντικαταστήστε το `multi_page_1.pdf` με το όνομα του PDF που θέλετε να επεξεργαστείτε. Αυτή η διαδρομή χρησιμοποιείται από τη μηχανή OCR.

## Βήμα 3: Αναγνώριση PDF (OCR Multi Page PDF)

```csharp
// Recognize image
List<RecognitionResult> results = api.RecognizePdf(fullPath, new DocumentRecognitionSettings { StartPage = 2, PagesNumber = 2 });
```

Η μέθοδος `RecognizePdf` εκτελεί OCR στις καθορισμένες σελίδες. Ρυθμίστε τα `StartPage` και `PagesNumber` για να στοχεύσετε οποιοδήποτε εύρος, κάτι που είναι ιδιαίτερα χρήσιμο για σενάρια **ocr multi page pdf**.

## Βήμα 4: Εκτύπωση Αποτελεσμάτων

```csharp
// Print result
int pageCounter = 0;
foreach (var result in results)
{
    PrintRecognitionResult(result, pageCounter++);
}
```

Ο βρόχος διατρέχει το `RecognitionResult` κάθε σελίδας και εκτυπώνει το εξαγόμενο κείμενο. Η **PrintRecognitionResult** είναι μια βοηθητική μέθοδος που εμφανίζει το κείμενο OCR στην κονσόλα. Μπορείτε να αντικαταστήσετε το `PrintRecognitionResult` με τη δική σας λογική για αποθήκευση του κειμένου σε βάση δεδομένων ή εγγραφή σε αρχείο.

## Συνηθισμένες Περιπτώσεις Χρήσης

- **Αυτοματοποίηση επεξεργασίας τιμολογίων** – εξαγωγή στοιχείων γραμμής από σκαναρισμένα τιμολόγια.  
- **Ψηφιακή αρχειοθέτηση** – μετατροπή παλαιών σκαναρισμένων εγγράφων σε αναζητήσιμα PDF.  
- **Εξόρυξη δεδομένων** – λήψη κειμένου από εκθέσεις που διατίθενται μόνο ως σκαναρισμένα PDF.

## Επίλυση Προβλημάτων & Συμβουλές

- **Χαμηλή ακρίβεια;** Βεβαιωθείτε ότι το PDF είναι υψηλής ανάλυσης (300 dpi ή περισσότερο).  
- **Προβλήματα μνήμης σε μεγάλα PDF;** Επεξεργαστείτε το έγγραφο σε μικρότερα batch σελίδων.  
- **Απαιτείται διαχείριση PDF με κωδικό πρόσβασης;** Φορτώστε το αρχείο σε ροή (stream) και περάστε τον κωδικό στην API OCR (ανατρέξτε στην τεκμηρίωση Aspose.OCR).

## Συμπέρασμα

Συγχαρητήρια! Μάθατε **πώς να κάνετε ocr pdf** αρχεία σε .NET, εξαγάγατε κείμενο και είδατε πώς να **convert pdf to text** για έγγραφα μονής και πολλαπλών σελίδων. Αυτή η προσέγγιση σας δίνει την ευελιξία να ενσωματώσετε OCR σε οποιαδήποτε εφαρμογή C#, είτε πρόκειται για web service, desktop utility ή background job.

## Συχνές Ερωτήσεις

**Ε: Μπορώ να εξάγω κείμενο από PDF με κωδικό πρόσβασης;**  
Α: Ναι. Χρησιμοποιήστε την υπερφόρτωση της `RecognizePdf` που δέχεται παράμετρο κωδικού πρόσβασης.

**Ε: Λειτουργεί το OCR σε χειρόγραφα PDF;**  
Α: Το Aspose.OCR μπορεί να αναγνωρίσει τυπωμένο κείμενο αξιόπιστα· το χειρόγραφο κείμενο μπορεί να απαιτεί πρόσθετη προεπεξεργασία ή εξειδικευμένη μηχανή.

**Ε: Ποιος είναι ο αντίκτυπος στην απόδοση για μεγάλα έγγραφα;**  
Α: Ο χρόνος επεξεργασίας κλιμακώνεται ανάλογα με τον αριθμό σελίδων και την ανάλυση εικόνας. Η διαίρεση του εγγράφου σε μικρότερα batch μπορεί να βελτιώσει την ανταπόκριση.

**Ε: Πώς αποθηκεύω τα αποτελέσματα OCR σε αρχείο κειμένου;**  
Α: Μέσα στον βρόχο `foreach`, γράψτε το `result.Text` σε ένα `StreamWriter` για κάθε σελίδα.

**Ε: Υπάρχει τρόπος να διατηρήσω την αρχική διάταξη PDF μετά το OCR;**  
Α: Μπορείτε να δημιουργήσετε ένα νέο αναζητήσιμο PDF επικάλυπτοντας το κείμενο OCR στις αρχικές σελίδες χρησιμοποιώντας το Aspose.PDF μετά την εξαγωγή.

---

**Τελευταία ενημέρωση:** 2026-05-29  
**Δοκιμασμένο με:** Aspose.OCR 24.11 για .NET  
**Συγγραφέας:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Σχετικά Tutorials

- [Extract image text C# with language selection using Aspose.OCR](/ocr/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [How to extract table from image using Aspose.OCR for .NET](/ocr/net/text-recognition/recognize-table/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}