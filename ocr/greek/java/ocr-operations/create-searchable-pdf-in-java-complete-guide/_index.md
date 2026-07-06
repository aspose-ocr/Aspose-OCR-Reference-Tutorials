---
category: general
date: 2026-07-05
description: Δημιουργήστε αναζητήσιμο PDF σε Java χρησιμοποιώντας το Aspose OCR. Μάθετε
  πώς να συμπιέζετε εικόνες σε PDF, να μετατρέπετε σκαναρισμένη εικόνα σε PDF και
  να απενεργοποιείτε την ενσωμάτωση γραμματοσειρών στο PDF για μικρότερα αρχεία.
draft: false
keywords:
- create searchable pdf
- compress images in pdf
- convert scanned image to pdf
- disable font embedding pdf
language: el
og_description: Δημιουργήστε αναζητήσιμο PDF σε Java με το Aspose OCR. Αυτό το σεμινάριο
  δείχνει πώς να συμπιέσετε εικόνες σε PDF, να μετατρέψετε σκαναρισμένη εικόνα σε
  PDF και να απενεργοποιήσετε την ενσωμάτωση γραμματοσειρών σε PDF.
og_title: Δημιουργία Αναζητήσιμου PDF σε Java – Οδηγός Βήμα‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF in Java using Aspose OCR. Learn how to compress
    images in PDF, convert scanned image to PDF, and disable font embedding PDF for
    smaller files.
  headline: Create Searchable PDF in Java – Complete Guide
  type: TechArticle
tags:
- Java
- OCR
- PDF
title: Δημιουργία Αναζητήσιμου PDF σε Java – Πλήρης Οδηγός
url: /el/java/ocr-operations/create-searchable-pdf-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Αναζητήσιμου PDF σε Java – Πλήρης Οδηγός

Έχετε ποτέ χρειαστεί να **δημιουργήσετε αναζητήσιμο PDF** από ένα σαρωμένο έγγραφο αλλά να νιώσατε κολλημένοι στο κομμάτι “πώς το κάνω”; Δεν είστε μόνοι. Σε πολλά έργα, η μετατροπή ενός TIFF ή JPEG σε PDF που μπορείτε πραγματικά να αναζητήσετε είναι μια *απαραίτητη* λειτουργία, ειδικά όταν θέλετε επίσης να **συμπιέσετε εικόνες σε PDF** για να διατηρήσετε τα μεγέθη αρχείων διαχειρίσιμα.

Σε αυτό το tutorial θα περάσουμε από ένα πρακτικό παράδειγμα χρησιμοποιώντας Aspose OCR για Java. Στο τέλος θα ξέρετε ακριβώς πώς να **convert scanned image to PDF**, να ρυθμίσετε την επιλογή **compress images in PDF** και ακόμη να **disable font embedding PDF** για να εξοικονομήσετε μερικά επιπλέον kilobytes. Χωρίς περιττές πληροφορίες—απλώς μια πλήρης, εκτελέσιμη λύση που μπορείτε να ενσωματώσετε στον κώδικά σας σήμερα.

## Τι Θα Μάθετε

- Ρυθμίστε τη μηχανή Aspose OCR σε ένα έργο Java.  
- Εκτελέστε OCR σε ένα TIFF (ή οποιαδήποτε ραστερική εικόνα).  
- Διαμορφώστε το `PdfSaveOptions` για **συμπίεση εικόνων σε PDF** και **απενεργοποίηση ενσωμάτωσης γραμματοσειρών PDF**.  
- Αποθηκεύστε το αποτέλεσμα ως **αναζητήσιμο PDF** που μπορείτε να ευρετηριάσετε ή να αναζητήσετε αμέσως.  

**Προαπαιτούμενα**  
- Java 8 ή νεότερη εγκατεστημένη.  
- Maven ή Gradle για διαχείριση εξαρτήσεων (θα δείξουμε το απόσπασμα Maven).  
- Ένα αρχείο σαρωμένης εικόνας (TIFF, PNG ή JPEG) έτοιμο για επεξεργασία.  

Αν τα έχετε, ας βουτήξουμε.

![Δημιουργία ροής εργασίας αναζητήσιμου PDF – Μετατροπή Java OCR σε PDF](/images/create-searchable-pdf-workflow.png "Διάγραμμα που δείχνει τα βήματα για τη δημιουργία αναζητήσιμου PDF με Aspose OCR")

## Βήμα 1: Προσθήκη Εξάρτησης Aspose OCR

Πρώτα, προσθέστε τη βιβλιοθήκη Aspose OCR στο έργο σας. Με Maven, προσθέστε αυτό στο `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Αν προτιμάτε Gradle, το ισοδύναμο είναι:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Pro tip:** Παρακολουθείτε τις σημειώσεις έκδοσης του Aspose· οι νεότερες εκδόσεις συχνά προσφέρουν βελτιώσεις απόδοσης για την ακρίβεια του OCR.

## Βήμα 2: Αρχικοποίηση της Μηχανής OCR

Η δημιουργία μιας μηχανής OCR είναι τόσο απλή όσο η δημιουργία ενός αντικειμένου `OcrEngine`. Αυτό το αντικείμενο θα διαχειρίζεται τα πάντα, από τη φόρτωση της εικόνας μέχρι την εξαγωγή του κειμένου.

```java
import com.aspose.ocr.OcrEngine;

// ...

// Step 2: Create an OCR engine instance
OcrEngine engine = new OcrEngine();
```

Γιατί χρειάζεται μια αφιερωμένη μηχανή; Η Aspose διαχωρίζει το βαρέως βάρους (προεπεξεργασία εικόνας, μοντέλα γλώσσας) από το υπόλοιπο της εφαρμογής σας, ώστε να μπορείτε να επαναχρησιμοποιήσετε το ίδιο `engine` για πολλά αρχεία χωρίς επανεκκίνηση των βαρέων πόρων.

## Βήμα 3: Εκτέλεση OCR στην Σαρωμένη Εικόνα

Τώρα τροφοδοτούμε τη μηχανή με ένα σαρωμένο αρχείο. Η μέθοδος `recognizeImage` επιστρέφει ένα `RecognitionResult` που περιέχει το εξαγόμενο κείμενο και τις πληροφορίες διάταξης.

```java
import com.aspose.ocr.RecognitionResult;

// ...

// Step 3: Perform OCR on the source image
String sourcePath = "YOUR_DIRECTORY/document_scan.tif"; // could be .png or .jpg too
RecognitionResult result = engine.recognizeImage(sourcePath);
```

> **Τι γίνεται αν η εικόνα δεν είναι TIFF;**  
> Η Aspose OCR ανιχνεύει αυτόματα κοινές ραστερικές μορφές, ώστε να μπορείτε να τη στοχεύσετε σε JPEG, PNG ή BMP χωρίς αλλαγή κώδικα.

## Βήμα 4: Διαμόρφωση Επιλογών Αποθήκευσης PDF (Συμπίεση Εικόνων & Απενεργοποίηση Ενσωμάτωσης Γραμματοσειρών)

Εδώ έρχονται στο προσκήνιο οι δευτερεύουσες λέξεις-κλειδιά. Θα πούμε στην Aspose να **compress images in PDF** και να **disable font embedding PDF**. Και οι δύο ρυθμίσεις μειώνουν το τελικό μέγεθος του αρχείου—χρήσιμο όταν αποστέλλετε δεκάδες έγγραφα.

```java
import com.aspose.ocr.pdf.PdfSaveOptions;

// ...

// Step 4: Set up PDF save options
PdfSaveOptions pdfOpts = new PdfSaveOptions();

// Reduce PDF size by compressing images
pdfOpts.setCompressImages(true);
pdfOpts.setImageQuality(80); // 0‑100, 80 is a good balance

// Prevent fonts from being embedded – saves a few KB per page
pdfOpts.setEmbedFonts(false);
```

**Γιατί να συμπιέζετε εικόνες;**  
Οι σαρωμένες σελίδες είναι συχνά υψηλής ανάλυσης· η συμπίεση τους στο 80 % ποιότητας μπορεί να μειώσει ένα PDF 10 σελίδων από 12 MB σε κάτω από 3 MB χωρίς οπτική απώλεια.

**Γιατί να απενεργοποιήσετε την ενσωμάτωση γραμματοσειρών;**  
Αν η μηχανή OCR χρησιμοποιεί τυπικές συστημικές γραμματοσειρές (όπως Arial ή Times New Roman), η ενσωμάτωση τους είναι περιττή. Η απενεργοποίησή τους περικόπτει περαιτέρω το μέγεθος του αρχείου, ειδικά για μεγάλες παρτίδες.

## Βήμα 5: Αποθήκευση του Αποτελέσματος OCR ως Αναζητήσιμο PDF

Το τελικό βήμα ενώνει τα πάντα: την ακατέργαστη εικόνα, το εξαγόμενο επίπεδο κειμένου και τις επιλογές PDF που μόλις ορίσαμε.

```java
// Step 5: Save the OCR result as a searchable PDF
String outputPath = "YOUR_DIRECTORY/document.pdf";
engine.saveAsSearchablePdf(outputPath, pdfOpts);

System.out.println("Searchable PDF created at: " + outputPath);
```

Όταν ανοίξετε το `document.pdf` στο Adobe Reader ή σε οποιονδήποτε σύγχρονο προβολέα, θα δείτε την αρχική σαρωμένη εικόνα **συν** ένα αόρατο επίπεδο κειμένου. Πληκτρολογώντας μια λέξη στο πεδίο αναζήτησης θα επισημαίνονται τα ταιριάσματα—ακριβώς αυτό που υπόσχεται το “create searchable pdf”.

### Αναμενόμενο Αποτέλεσμα

Η εκτέλεση του προγράμματος με ένα έγκυρο TIFF αποδίδει κάτι όπως:

```
Searchable PDF created at: YOUR_DIRECTORY/document.pdf
```

Ανοίξτε το PDF, πατήστε `Ctrl+F`, πληκτρολογήστε μια λέξη που εμφανίζεται στη σαρωμένη σελίδα και δείτε το να μεταπηδά στη σωστή θέση. Αυτό είναι το χαρακτηριστικό ενός επιτυχημένου **create searchable pdf** workflow.

## Συνηθισμένα Προβλήματα & Πώς να τα Αποφύγετε

| Πρόβλημα | Γιατί Συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| **Κενό PDF** | `PdfSaveOptions` δεν περνιέται στο `saveAsSearchablePdf`. | Βεβαιωθείτε ότι καλείτε την υπερφόρτωση που δέχεται `PdfSaveOptions`. |
| **Ακατάλληλοι χαρακτήρες** | Η γλώσσα OCR δεν έχει οριστεί (η προεπιλογή είναι Αγγλικά). | Χρησιμοποιήστε `engine.getLanguage().setLanguage(OcrLanguage.FRENCH);` πριν από το `recognizeImage`. |
| **Μεγάλο μέγεθος αρχείου** | `setCompressImages(false)` ή `setEmbedFonts(true)`. | Διατηρήστε και τις δύο σημαίες όπως φαίνεται παραπάνω. |
| **Παραμόρφωση εικόνας** | `setImageQuality` ορίστηκε πολύ χαμηλό (<50). | Κρατήστε το στο 70‑90 για καλή ισορροπία. |

## Επέκταση του Παραδείγματος

Τώρα που μπορείτε να **convert scanned image to PDF** και να ελέγχετε το μέγεθος, ίσως θέλετε να:

- **Επεξεργασία κατά παρτίδες** ενός φακέλου σαρώσεων με έναν απλό βρόχο `for(File f : folder.listFiles())`.  
- Προσθέστε **υδατογραφήματα** χρησιμοποιώντας Aspose PDF (`PdfDocument.addWatermarkText`).  
- Εξάγετε το κείμενο OCR σε ένα **απλό .txt** αρχείο για συστήματα ευρετηρίασης (`result.getText().writeToFile("doc.txt")`).  

Όλες αυτές οι επεκτάσεις επαναχρησιμοποιούν το ίδιο αντικείμενο `OcrEngine`, διατηρώντας τη χρήση μνήμης χαμηλή.

## Πλήρης, Έτοιμος‑για‑Εκτέλεση Κώδικας

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.pdf.PdfSaveOptions;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Step 2: Perform OCR on the source image
        String source = "YOUR_DIRECTORY/document_scan.tif";
        RecognitionResult result = engine.recognizeImage(source);

        // Step 3: Configure PDF save options (compress images & disable fonts)
        PdfSaveOptions pdfOpts = new PdfSaveOptions();
        pdfOpts.setCompressImages(true);      // Reduce PDF size by compressing images
        pdfOpts.setImageQuality(80);          // Image quality (0‑100)
        pdfOpts.setEmbedFonts(false);         // Do not embed fonts to keep file size small

        // Step 4: Save the OCR result as a searchable PDF
        String output = "YOUR_DIRECTORY/document.pdf";
        engine.saveAsSearchablePdf(output, pdfOpts);

        // Step 5: Inform the user that the PDF has been created
        System.out.println("Searchable PDF created at: " + output);
    }
}
```

Αντιγράψτε‑και‑επικολλήστε αυτό στο IDE σας, αντικαταστήστε το `YOUR_DIRECTORY` με μια πραγματική διαδρομή και τρέξτε. Αν όλα είναι ρυθμισμένα σωστά, θα έχετε ένα **searchable PDF** που είναι επίσης ελαφρύ χάρη στη συμπίεση εικόνας και την απενεργοποίηση ενσωμάτωσης γραμματοσειρών.

## Συμπέρασμα

Συνοψίσαμε όλα όσα χρειάζεστε για να **create searchable pdf** αρχεία σε Java χρησιμοποιώντας Aspose OCR. Από την αρχικοποίηση της μηχανής, την εκτέλεση OCR, τη ρύθμιση **compress images in pdf** και **disable font embedding pdf**, μέχρι την τελική αποθήκευση ενός αναζητήσιμου εγγράφου—κάθε βήμα εξηγήθηκε με το *γιατί* πίσω από αυτό.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να προσθέσετε πακέτα γλώσσας OCR, επεξεργασία κατά παρτίδες ολόκληρων φακέλων ή στρώση PDF με σημειώσεις. Τα θεμέλια που μόλις μάθατε θα κάνουν αυτές τις επεκτάσεις παιχνιδάκι.

Έχετε ερωτήσεις ή θέλετε να μοιραστείτε τα δικά σας κόλπα; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Αναγνώριση Κειμένου PDF – Λειτουργίες OCR με Aspose.OCR για Java](/ocr/english/java/ocr-operations/)
- [OCR Αναγνώριση Εγγράφων PDF σε Aspose.OCR για Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Πώς να κάνετε OCR PDF σε .NET με Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}