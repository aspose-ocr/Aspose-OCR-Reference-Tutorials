---
date: 2026-05-19
description: Μάθετε πώς να εξάγετε κείμενο από tiff και να το μετατρέψετε σε περιεχόμενο
  αναζητήσιμο χρησιμοποιώντας το Aspose.OCR for Java. Αυτό το step‑by‑step tutorial
  καλύπτει τη ρύθμιση, τον κώδικα και τις βέλτιστες πρακτικές.
keywords:
- extract text from tiff
- how to recognize tiff
- java ocr library
- convert tiff to searchable
- java ocr tutorial
linktitle: OCR Αναγνώριση Εικόνων TIFF στο Aspose.OCR for Java
schemas:
- author: Aspose
  dateModified: '2026-05-19'
  description: Learn how to extract text from tiff and convert it to searchable content
    using Aspose.OCR for Java. This step‑by‑step tutorial covers setup, code, and
    best practices.
  headline: How to extract text from tiff with Aspose.OCR for Java
  type: TechArticle
- description: Learn how to extract text from tiff and convert it to searchable content
    using Aspose.OCR for Java. This step‑by‑step tutorial covers setup, code, and
    best practices.
  name: How to extract text from tiff with Aspose.OCR for Java
  steps:
  - name: Set Up Your Project
    text: Create a new Java project (IDE or command line) and place the Aspose.OCR
      JAR on the classpath.
  - name: Define Your Document Directory and Image Path
    text: Set `dataDir` to the folder that contains your TIFF files, e.g., `String
      dataDir = "C:/Images/";`.
  - name: Create AsposeOCR Instance
    text: Instantiate `AsposeOCR ocr = new AsposeOCR();` to access OCR functions.
  - name: Set Recognition Options
    text: Create a `DocumentRecognitionSettings` object to specify language, mode,
      and output options.
  - name: Perform Text Recognition
    text: The method returns an `OcrResult` containing the extracted text and metadata.
  - name: Print Recognition Results
    text: Iterate over the `OcrResult` fields to display the recognized text.
  - name: Implement the `printResult` Method
    text: The `printResult` helper formats and outputs the OCR data to the console.
  type: HowTo
- questions:
  - answer: It means converting the visual characters inside a TIFF image into editable,
      searchable text using OCR.
    question: What does “extract text from tiff” mean?
  - answer: Aspose.OCR for Java, available from the official Aspose site.
    question: Which library should I use?
  - answer: Yes—use a free trial for evaluation, then purchase a commercial license
      for deployment.
    question: Is a license required for production?
  - answer: Absolutely; the `RecognizeTiff` method processes all pages automatically.
    question: Can I handle multi‑page TIFFs?
  - answer: Java 8 or later is fully supported.
    question: What Java version is supported?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Πώς να εξάγετε κείμενο από tiff με το Aspose.OCR for Java
url: /el/java/ocr-operations/recognize-tiff/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Εικόνες TIFF Χρησιμοποιώντας το Aspose.OCR για Java

## Γρήγορες Απαντήσεις
- **Τι σημαίνει “extract text from tiff”;** Σημαίνει τη μετατροπή των οπτικών χαρακτήρων μέσα σε μια εικόνα TIFF σε επεξεργάσιμο, αναζητήσιμο κείμενο χρησιμοποιώντας OCR.  
- **Ποια βιβλιοθήκη πρέπει να χρησιμοποιήσω;** Aspose.OCR για Java, διαθέσιμη από την επίσημη ιστοσελίδα της Aspose.  
- **Απαιτείται άδεια για παραγωγή;** Ναι—χρησιμοποιήστε μια δωρεάν δοκιμή για αξιολόγηση, στη συνέχεια αγοράστε εμπορική άδεια για την ανάπτυξη.  
- **Μπορώ να επεξεργαστώ πολυσελίδες TIFF;** Απόλυτα· η μέθοδος `RecognizeTiff` επεξεργάζεται όλες τις σελίδες αυτόματα.  
- **Ποια έκδοση Java υποστηρίζεται;** Η Java 8 ή νεότερη υποστηρίζεται πλήρως.

## Τι είναι η εξαγωγή κειμένου από tiff;
*Extract text from tiff* είναι η λειτουργία OCR που διαβάζει τα δεδομένα pixel σε ένα αρχείο TIFF και επιστρέφει τους υποκείμενους χαρακτήρες ως κείμενο Unicode. Αυτό επιτρέπει πλήρη αναζήτηση κειμένου, ευρετηρίαση και ανάλυση δεδομένων. Με τη μετατροπή των σαρωμένων εικόνων σε μηχανικά αναγνώσιμες συμβολοσειρές, μπορείτε να ενσωματώσετε το περιεχόμενο σε βάσεις δεδομένων, να εφαρμόσετε επεξεργασία φυσικής γλώσσας ή να δημιουργήσετε αναζητήσιμα PDF για αρχειοθέτηση.

## Γιατί να χρησιμοποιήσετε το Aspose.OCR για Java;
Aspose.OCR υποστηρίζει **πάνω από 50 μορφές εισόδου και εξόδου** και μπορεί να επεξεργαστεί αρχεία TIFF έως **500 MB** χωρίς να φορτώνει ολόκληρο το έγγραφο στη μνήμη. Το API είναι καθαρά Java, **χωρίς εξωτερικές εξαρτήσεις**, και παρέχει **>95 % ακρίβεια** σε τυπωμένο αγγλικό κείμενο αμέσως μετά την εγκατάσταση.

## Προαπαιτούμενα
- Java Development Kit (JDK) 8 ή νεότερο εγκατεστημένο.  
- Βιβλιοθήκη Aspose.OCR για Java λήφθηκε και προστέθηκε στο έργο σας. Κατεβάστε την από την επίσημη σελίδα λήψης **[εδώ](https://releases.aspose.com/ocr/java/)**.  
- Μια εικόνα TIFF που περιέχει το κείμενο που θέλετε να εξάγετε.  
- (Προαιρετικό) Βασική εξοικείωση με **read tiff file java** χρησιμοποιώντας `java.io` αν προτιμάτε χειροκίνητη διαχείριση αρχείων.

## Εισαγωγή Πακέτων
Η κλάση `AsposeOCR` και οι σχετικές ρυθμίσεις βρίσκονται στο namespace `com.aspose.ocr`. Εισάγετέ τις στην αρχή του αρχείου πηγαίου κώδικα.

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.DetectAreasMode;
import com.aspose.ocr.DocumentRecognitionSettings;
import com.aspose.ocr.Language;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionResult.LinesResult;
import com.aspose.ocr.pdf.AsposeOCRPdf;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.util.ArrayList;
```

## Πώς να εξάγετε κείμενο από tiff χρησιμοποιώντας το Aspose.OCR για Java;
Φορτώστε το TIFF με `new AsposeOCR()` και καλέστε `recognizeTiff()`—αυτή η ενιαία κλήση διαβάζει κάθε σελίδα, εφαρμόζει μοντέλα ειδικά για τη γλώσσα και επιστρέφει ένα δομημένο αντικείμενο `OcrResult` που περιέχει απλό κείμενο, παραγράφους και βαθμολογίες εμπιστοσύνης. Η μέθοδος λειτουργεί σε λιγότερο από ένα δευτερόλεπτο για τυπικές σαρώσεις 300 dpi.

### Βήμα 1: Ρυθμίστε το Έργο Σας
Δημιουργήστε ένα νέο έργο Java (IDE ή γραμμή εντολών) και τοποθετήστε το JAR του Aspose.OCR στο classpath.

### Βήμα 2: Ορίστε τον Κατάλογο Εγγράφων και τη Διαδρομή Εικόνας
Ορίστε το `dataDir` στον φάκελο που περιέχει τα αρχεία TIFF, π.χ., `String dataDir = "C:/Images/";`.

```java
String dataDir = "Your Document Directory";
String file = dataDir + "multipage.tif";
```

### Βήμα 3: Δημιουργήστε Παράδειγμα AsposeOCR
Δημιουργήστε το αντικείμενο `AsposeOCR ocr = new AsposeOCR();` για πρόσβαση στις λειτουργίες OCR.

```java
AsposeOCR api = new AsposeOCR();
```

### Βήμα 4: Ορίστε Επιλογές Αναγνώρισης
Δημιουργήστε ένα αντικείμενο `DocumentRecognitionSettings` για να καθορίσετε τη γλώσσα, τη λειτουργία και τις επιλογές εξόδου.

```java
DocumentRecognitionSettings settings = new DocumentRecognitionSettings(2);
settings.setDetectAreasMode(DetectAreasMode.PHOTO);
```

### Βήμα 5: Εκτελέστε την Αναγνώριση Κειμένου
Η μέθοδος επιστρέφει ένα `OcrResult` που περιέχει το εξαγόμενο κείμενο και τα μεταδεδομένα.

```java
ArrayList<RecognitionResult> result = api.RecognizeTiff(file, settings);
```

### Βήμα 6: Εκτυπώστε τα Αποτελέσματα Αναγνώρισης
Επανάληψη στα πεδία του `OcrResult` για εμφάνιση του αναγνωρισμένου κειμένου.

```java
for (RecognitionResult r : result) {
    printResult(r);
}
```

### Βήμα 7: Υλοποιήστε τη Μέθοδο `printResult`
Η βοηθητική μέθοδος `printResult` μορφοποιεί και εκτυπώνει τα δεδομένα OCR στην κονσόλα.

```java
static void printResult(RecognitionResult result) {
    // Your implementation here
}
```

## Συχνά Προβλήματα και Λύσεις

| Πρόβλημα | Γιατί συμβαίνει | Πώς να διορθώσετε |
|----------|----------------|-------------------|
| **Δεν επιστρέφεται κείμενο** | Λάθος διαδρομή αρχείου ή μη υποστηριζόμενη συμπίεση TIFF. | Επαληθεύστε τη διαδρομή `dataDir`, βεβαιωθείτε ότι το TIFF δεν είναι κατεστραμμένο και χρησιμοποιήστε μη συμπιεσμένο TIFF όταν είναι δυνατόν. |
| **Ασχημοί χαρακτήρες** | Εικόνα χαμηλής ανάλυσης ή χαμηλής αντίθεσης. | Προεπεξεργαστείτε την εικόνα (αυξήστε το DPI σε 300+, ενισχύστε την αντίθεση) πριν καλέσετε το `recognizeTiff`. |
| **Μη υποστηριζόμενη γλώσσα** | Η γλώσσα δεν έχει οριστεί στο `DocumentRecognitionSettings`. | Προσθέστε `settings.setLanguage(Language.SPANISH);` (ή τη γλώσσα-στόχο σας) πριν από την αναγνώριση. |

## Συχνές Ερωτήσεις

**Ε1: Είναι το Aspose.OCR κατάλληλο για αναγνώριση κειμένου σε πολλές γλώσσες;**  
Α: Ναι, το Aspose.OCR υποστηρίζει πάνω από 60 γλώσσες, επιτρέποντάς σας να ορίσετε τη ζητούμενη γλώσσα στο `DocumentRecognitionSettings`.

**Ε2: Μπορώ να ενσωματώσω το Aspose.OCR σε μια υπηρεσία web;**  
Α: Απόλυτα. Η βιβλιοθήκη λειτουργεί σε οποιονδήποτε διακομιστή συμβατό με Java, και μπορείτε να εκθέσετε τη λειτουργία OCR μέσω REST endpoints.

**Ε3: Ποιες επιλογές αδειοδότησης είναι διαθέσιμες;**  
Α: Μπορείτε να εξερευνήσετε τις επιλογές αδειοδότησης και να αγοράσετε άδεια **[εδώ](https://purchase.aspose.com/buy)**.

**Ε4: Διατίθεται δωρεάν δοκιμή;**  
Α: Ναι—κατεβάστε μια δοκιμή **[εδώ](https://releases.aspose.com/)** για να αξιολογήσετε όλες τις δυνατότητες χωρίς κόστος.

**Ε5: Πού μπορώ να λάβω υποστήριξη από την κοινότητα;**  
Α: Συμμετέχετε στη συζήτηση στο **[φόρουμ Aspose.OCR](https://forum.aspose.com/c/ocr/16)** για συμβουλές, αποσπάσματα κώδικα και βοήθεια αντιμετώπισης προβλημάτων.

**Τελευταία Ενημέρωση:** 2026-05-19  
**Δοκιμάστηκε Με:** Aspose.OCR for Java 24.11 (latest at time of writing)  
**Συγγραφέας:** Aspose

## Σχετικά Μαθήματα

- [Εξαγωγή Κειμένου από Εικόνες – Βασικά OCR με Aspose.OCR για Java](/ocr/java/ocr-basics/)
- [OCR Αναγνώριση Εγγράφων PDF στο Aspose.OCR για Java](/ocr/java/ocr-operations/recognize-pdf/)
- [Εξαγωγή Κειμένου από Εικόνα Java με Aspose.OCR Detect Areas Mode](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< blocks/products/products-backtop-button >}}
{{< /blocks/products/pf/main-wrap-class >}}