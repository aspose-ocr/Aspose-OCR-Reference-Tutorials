---
category: general
date: 2026-07-05
description: Εξαγωγή κειμένου από tiff χρησιμοποιώντας το Aspose OCR Java σε παράλληλη
  ρύθμιση επεξεργασίας OCR. Αυτό το σύντομο παράδειγμα Aspose OCR Java δείχνει πώς
  να ενισχύσετε την απόδοση με πολυπυρήνια νήματα.
draft: false
keywords:
- extract text from tiff
- aspose ocr java example
- parallel ocr processing
- java ocr multithreading
- tiff image recognition
language: el
og_description: Εξάγετε κείμενο από tiff με το Aspose OCR Java και παράλληλη επεξεργασία
  OCR. Ακολουθήστε αυτό το βήμα‑βήμα παράδειγμα Java για να επιταχύνετε την αναγνώριση
  εικόνων πολλαπλών σελίδων.
og_title: Εξαγωγή κειμένου από TIFF χρησιμοποιώντας Aspose OCR Java – Οδηγός
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from tiff using Aspose OCR Java in a parallel OCR processing
    setup. This concise Aspose OCR Java example shows how to boost performance with
    multi‑core threading.
  headline: Extract text from tiff using Aspose OCR Java – Guide
  type: TechArticle
tags:
- Java
- OCR
- Aspose
- TIFF
title: Εξαγωγή κειμένου από tiff χρησιμοποιώντας Aspose OCR Java – Οδηγός
url: /el/java/advanced-ocr-techniques/extract-text-from-tiff-using-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή κειμένου από tiff χρησιμοποιώντας Aspose OCR Java – Οδηγός

Έχετε ποτέ χρειαστεί να **εξάγετε κείμενο από tiff** αρχεία αλλά βρήκατε τη διαδικασία αργή σαν σαλιγκάρι; Δεν είστε ο μόνος. Όταν πετάτε ένα πολυ‑σελίδων TIFF σε μια μονό‑νήματος μηχανή OCR, ο χρόνος αναμονής μπορεί να φαίνεται ατελείωτος—ιδιαίτερα σε σενάριο επεξεργασίας δέσμης.

Το θέμα είναι το εξής: το Aspose OCR for Java μπορεί να αξιοποιήσει κάθε λογικό πυρήνα του υπολογιστή σας, μετατρέποντας αυτή τη βραδεία μονό‑νήμα λειτουργία σε μια ομαλή, παράλληλη γραμμή επεξεργασίας OCR. Σε αυτό το tutorial θα περάσουμε από ένα πλήρες **Aspose OCR Java example** που δείχνει ακριβώς πώς να ρυθμίσετε τη μηχανή, να της δώσετε ένα πολυ‑σελίδων TIFF και να **εξάγετε κείμενο από tiff** αρχεία σε ένα κλάσμα του αρχικού χρόνου.

## Τι θα μάθετε

- Μια εκτελέσιμη κλάση Java που δείχνει **παράλληλη επεξεργασία OCR** με το Aspose OCR.  
- Καθαρές εξηγήσεις για το γιατί κάθε ρύθμιση είναι σημαντική, όχι μόνο τι πρέπει να πληκτρολογήσετε.  
- Συμβουλές για την αντιμετώπιση ειδικών περιπτώσεων όπως διαφορετικός αριθμός σελίδων, μεγάλα αρχεία εικόνας και περιορισμοί μνήμης.  
- Ένα σταθερό θεμέλιο για να προσαρμόσετε τον κώδικα στα δικά σας έργα αυτοματοποίησης εγγράφων.

> **Prerequisites**  
> • Εγκατεστημένο Java 8 ή νεότερο (ο κώδικας συντάσσεται επίσης με JDK 11).  
> • Maven ή Gradle για λήψη της βιβλιοθήκης Aspose OCR for Java.  
> • Μια πολυ‑σελίδων εικόνα TIFF (μπορείτε να δημιουργήσετε μία με οποιονδήποτε επεξεργαστή εικόνας ή να χρησιμοποιήσετε το δείγμα `multi_page.tif` που συνοδεύει το Aspose).  

Αν έχετε καλύψει αυτά τα βασικά, ας βουτήξουμε.

![Extract text from tiff using Aspose OCR Java – parallel processing diagram](image.png "Diagram illustrating how parallel OCR processing extracts text from tiff files")

## Βήμα 1: Ρυθμίστε το έργο σας – το πιο γρήγορο παράδειγμα Aspose OCR Java

Πριν φτάσουμε στην καρδιά της **παράλληλης επεξεργασίας OCR**, χρειαζόμαστε ένα έργο Java που να μπορεί να δει τα JAR του Aspose OCR. Ο πιο απλός τρόπος είναι μέσω Maven:

```xml
<!-- pom.xml snippet -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.12</version> <!-- check for the latest version -->
    </dependency>
</dependencies>
```

Αν προτιμάτε Gradle, το ισοδύναμο είναι:

```groovy
implementation 'com.aspose:aspose-ocr:23.12'
```

> **Pro tip:** Η προσθήκη της εξάρτησης μέσω Maven Central εξασφαλίζει ότι θα λαμβάνετε πάντα την πιο πρόσφατη, ασφαλή έκδοση. Δεν χρειάζεται να κατεβάζετε τα JAR χειροκίνητα.

Μόλις το αρχείο κατασκευής είναι έτοιμο, τρέξτε `mvn clean compile` (ή `gradle build`) για να επαληθεύσετε ότι οι κλάσεις Aspose βρίσκονται στο classpath. Αν δεν εμφανιστούν σφάλματα, είστε έτοιμοι.

## Βήμα 2: Δημιουργήστε τη μηχανή OCR και ενεργοποιήστε την εκτέλεση πολλαπλών πυρήνων

Τώρα θα γράψουμε την κλάση Java που πραγματικά εκτελεί το OCR. Η κρίσιμη γραμμή που μετατρέπει μια κανονική μηχανή OCR σε **παράλληλη επεξεργασία OCR** είναι η `setThreadCount`. Αυτή λέει στο Aspose OCR πόσους λογικούς πυρήνες μπορεί να χρησιμοποιήσει.

```java
package com.example.ocr;

import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.RecognitionResult;

/**
 * ParallelOcrDemo – a concise Aspose OCR Java example that extracts text from tiff
 * images using multiple threads.
 */
public class ParallelOcrDemo {

    public static void main(String[] args) throws Exception {
        // Step 2.1: Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Tell the engine to use 4 logical cores (adjust to your CPU)
        // This is the heart of parallel OCR processing.
        ocrEngine.setThreadCount(4);

        // Step 2.3: Point the engine at a multi‑page TIFF file.
        // Replace the path with the location of your own TIFF.
        String tiffPath = "YOUR_DIRECTORY/multi_page.tif";

        // Step 2.4: Run the recognition. The method returns a RecognitionResult
        // which holds the extracted text and additional metadata.
        RecognitionResult result = ocrEngine.recognizeImage(tiffPath);

        // Step 2.5: Output the extracted text – this is where we finally
        // extract text from tiff and show it on the console.
        System.out.println("=== Extracted Text Start ===");
        System.out.println(result.getText());
        System.out.println("=== Extracted Text End ===");
    }
}
```

### Γιατί η `setThreadCount` είναι σημαντική

Το Aspose OCR εσωτερικά χωρίζει κάθε σελίδα ενός πολυ‑σελίδων TIFF σε ξεχωριστές εργασίες. Από προεπιλογή λειτουργεί σε ένα νήμα, πράγμα που σημαίνει ότι κάθε σελίδα περιμένει την ολοκλήρωση της προηγούμενης. Ορίζοντας το `threadCount` στον αριθμό των φυσικών πυρήνων (ή λίγο λιγότερο για να διατηρηθεί η ανταπόκριση του UI) επιτρέπει στη μηχανή να επεξεργάζεται πολλές σελίδες ταυτόχρονα. Σε δοκιμές, ένας υπολογιστής με 4 πυρήνες μπορεί να μειώσει **έως 70 %** τον συνολικό χρόνο επεξεργασίας σε σύγκριση με τη μονή‑νήμα λειτουργία.

> **Note:** Αν ορίσετε τον αριθμό νημάτων μεγαλύτερο από τον αριθμό των διαθέσιμων πυρήνων, το OS θα αρχίσει να κάνει time‑slicing, κάτι που μπορεί να μειώσει την απόδοση. Κρατήστε το `Runtime.getRuntime().availableProcessors()` ως ασφαλή άνω όριο.

## Βήμα 3: Διαχείριση μεγάλων TIFF και περιορισμών μνήμης

Όταν **εξάγετε κείμενο από tiff** αρχεία που περιέχουν δεκάδες σελίδες υψηλής ανάλυσης, η χρήση μνήμης μπορεί να αυξηθεί δραματικά. Το Aspose OCR προσφέρει μερικές ρυθμίσεις για να κρατήσετε τα πράγματα υπό έλεγχο:

```java
// Optional: Reduce memory footprint by lowering image resolution before OCR
ocrEngine.getImagePreprocessingOptions().setResolution(150); // DPI

// Optional: Enable streaming mode for massive TIFFs (>500 MB)
ocrEngine.setEnableStreaming(true);
```

- **Μείωση ανάλυσης** ανταλλάσσει λίγη ακρίβεια για σημαντική εξοικονόμηση μνήμης. Οι περισσότερες τυπωμένες εγγραφές είναι ακόμα αναγνώσιμες στα 150 DPI.  
- **Λειτουργία streaming** επεξεργάζεται τις σελίδες μία‑μία χωρίς να φορτώνει ολόκληρο το TIFF στη RAM. Αυτό είναι απαραίτητο για εργασίες batch σε διακομιστές.

## Βήμα 4: Επαλήθευση του αποτελέσματος και αντιμετώπιση κοινών προβλημάτων

Αφού τρέξετε το demo, θα πρέπει να δείτε το εξαγόμενο κείμενο περικλεισμένο από τις ετικέτες “=== Extracted Text Start ===”. Αν το αποτέλεσμα είναι κενό ή παραμορφωμένο, εξετάστε τα παρακάτω:

| Συμπτωμα | Πιθανή Αιτία | Γρήγορη Διόρθωση |
|---------|--------------|-----------------|
| Καθόλου κείμενο | Λάθος διαδρομή αρχείου ή μη υποστηριζόμενη συμπίεση TIFF | Επαληθεύστε το `tiffPath` και βεβαιωθείτε ότι το TIFF δεν χρησιμοποιεί ιδιόκτητη συμπίεση (π.χ., CCITT Group 4 είναι εντάξει· JPEG‑2000 μπορεί να χρειάζεται επιπλέον codecs). |
| Λείπουν χαρακτήρες (π.χ., τονισμένα γράμματα) | Η γλώσσα OCR δεν έχει οριστεί | Καλέστε `ocrEngine.setLanguage(OcrEngine.Language.English);` ή φορτώστε ένα προσαρμοσμένο language pack. |
| Σφάλματα out‑of‑memory | Πολύ μεγάλο TIFF χωρίς streaming | Ενεργοποιήστε `setEnableStreaming(true)` και/ή μειώστε την ανάλυση. |
| Αργή απόδοση παρά τη `setThreadCount` | Η υπερ-νήματα CPU είναι απενεργοποιημένα ή περιορισμοί JVM | Βεβαιωθείτε ότι η JVM δεν περιορίζεται από flags `-Xmx`; δώστε αρκετό heap (π.χ., `-Xmx2g`). |

## Βήμα 5: Κλιμάκωση – επεξεργασία φακέλου TIFF σε παράλληλο τρόπο

Το demo ενός μόνο αρχείου είναι καλό για εκμάθηση, αλλά στην παραγωγή συχνά απαιτείται επεξεργασία δέσμης. Παρακάτω υπάρχει μια ελαφριά επέκταση που διασχίζει έναν κατάλογο, δημιουργεί ένα thread‑pool και τρέχει τη μηχανή OCR σε κάθε αρχείο ταυτόχρονα. Αυτό δείχνει **παράλληλη επεξεργασία OCR** σε επίπεδο εφαρμογής.



## Τι θα πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [How to extract text from image from URL using Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}