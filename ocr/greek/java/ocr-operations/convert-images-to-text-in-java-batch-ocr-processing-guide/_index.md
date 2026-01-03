---
category: general
date: 2026-01-02
description: Μετατρέψτε εικόνες σε κείμενο με Java χρησιμοποιώντας το Aspose OCR.
  Κατακτήστε την επεξεργασία OCR σε παρτίδες, διαβάστε εικόνες από φάκελο και φιλτράρετε
  τα αρχεία κατά επέκταση.
draft: false
keywords:
- convert images to text
- batch ocr processing
- read images from folder
- extract text from png
- filter files by extension
language: el
og_description: Μετατρέψτε γρήγορα εικόνες σε κείμενο με Java. Αυτό το σεμινάριο καλύπτει
  την επεξεργασία OCR σε παρτίδες, την ανάγνωση εικόνων από φάκελο και το φιλτράρισμα
  αρχείων κατά επέκταση.
og_title: Μετατροπή εικόνων σε κείμενο σε Java – Πλήρης οδηγός Batch OCR
tags:
- OCR
- Java
- Aspose
title: Μετατροπή Εικόνων σε Κείμενο σε Java – Οδηγός Επεξεργασίας OCR σε Παρτίδες
url: /el/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή Εικόνων σε Κείμενο σε Java – Οδηγός Batch OCR Επεξεργασίας

Ποτέ χρειάστηκε να **μετατρέψετε εικόνες σε κείμενο** αλλά δεν ήσασταν σίγουροι πώς να διαχειριστείτε δεκάδες αρχεία ταυτόχρονα; Δεν είστε μόνοι—οι προγραμματιστές αντιμετωπίζουν συνεχώς την πρόκληση της εξαγωγής δεδομένων από PNG, JPG και άλλες σαρώσεις. Τα καλά νέα; Με το Aspose OCR μπορείτε να στήσετε μια γραμμή επεξεργασίας batch OCR σε λίγα λεπτά, να διαβάζετε εικόνες από δομές φακέλων και ακόμη να φιλτράρετε αρχεία κατά επέκταση ώστε να εργάζεστε μόνο με ό,τι χρειάζεται.

Σε αυτό το tutorial θα δημιουργήσουμε ένα αυτόνομο πρόγραμμα Java που θα περιηγείται σε έναν κατάλογο, θα επιλέγει κάθε `.png` ή `.jpg`, θα στέλνει κάθε εικόνα στο Aspose OCR ασύγχρονα και θα εκτυπώνει το εξαγόμενο κείμενο στην αρχική σειρά. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο snippet που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο χρειάζεται **μετατροπή εικόνων σε κείμενο** σε κλίμακα.

![Παράδειγμα μετατροπής εικόνων σε κείμενο](https://example.com/convert-images-to-text.png "Στιγμιότυπο οθόνης της εξόδου της κονσόλας Java που εμφανίζει το μετατρεπόμενο κείμενο από αρχεία PNG")

## Τι Θα Κατασκευάσετε

- Ένας μοναδικός κινητήρας `AsposeOCR` κοινόχρηστος μεταξύ νημάτων (αποδοτικός και thread‑safe).  
- Ένα `ParallelRecognizer` που εκτελεί εργασίες OCR παράλληλα, ιδανικό για **batch OCR processing**.  
- Λογική που **διαβάζει εικόνες από φάκελο** χρησιμοποιώντας `java.nio.file.Files`.  
- Απλά φίλτρα για **εξαγωγή κειμένου από PNG** αρχεία ενώ διαχειρίζεται και JPGs.  
- Καθαρή τερματισμός του εσωτερικού thread pool για αποφυγή διαρροών πόρων.

### Προαπαιτούμενα

- Java 17 (ή οποιαδήποτε πρόσφατη LTS έκδοση).  
- Maven ή Gradle για λήψη της βιβλιοθήκης Aspose OCR.  
- Ένας φάκελος γεμάτος PNG/JPG εικόνες που θέλετε να επεξεργαστείτε.  
- Βασική εξοικείωση με Java streams—δεν απαιτείται κάτι περίπλοκο.

> **Pro tip:** Αν δεν έχετε ακόμη άδεια, η Aspose προσφέρει ένα δωρεάν προσωρινό κλειδί που μπορείτε να χρησιμοποιήσετε για δοκιμές.

## Βήμα 1 – Ρύθμιση του Έργου και Προσθήκη του Aspose OCR

Πρώτα, δημιουργήστε ένα νέο Maven project (ή Gradle, όπως προτιμάτε). Προσθέστε την εξάρτηση Aspose OCR στο `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

> **Why this matters:** Η δήλωση της εξάρτησης εκ των προτέρων εξασφαλίζει ότι ο μεταγλωττιστής μπορεί να δει τα `AsposeOCR`, `ParallelRecognizer` και τις σχετικές κλάσεις. Επίσης εγγυάται ότι η ίδια έκδοση χρησιμοποιείται σε όλα τα μηχανήματα, κάτι κρίσιμο για επαναλήψιμη **batch OCR processing**.

Μόλις ολοκληρωθεί η κατασκευή, ανανεώστε το IDE σας και θα πρέπει να δείτε τα πακέτα Aspose κάτω από `External Libraries`.

## Βήμα 2 – Μετατροπή Εικόνων σε Κείμενο – Αρχικοποίηση του OCR Engine

Χρειαζόμαστε μόνο **ένα** στιγμιότυπο OCR engine για ολόκληρη τη διαδικασία. Η κοινή χρήση του μεταξύ νημάτων εξοικονομεί μνήμη και επιταχύνει την εκτέλεση επειδή το engine φορτώνει τα language packs μόνο μία φορά.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

// ...

// Step 2: Create a single OCR engine instance and a parallel recognizer that uses it
AsposeOCR ocrEngine = new AsposeOCR();               // Loads language data internally
ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);
```

> **Explanation:** Το `ParallelRecognizer` τυλίγει το engine σε ένα thread‑pool. Όταν υποβάλλετε πολλά αρχεία, το καθένα παίρνει το δικό του worker thread, επιτρέποντας αληθινό parallelism σε multi‑core CPUs.

## Βήμα 3 – Ανάγνωση Εικόνων από Φάκελο – Περπάτημα του Δέντρου Καταλόγου

Τώρα χρειάζεται να **διαβάσουμε εικόνες από φάκελο** και να συλλέξουμε κάθε PNG ή JPG. Το API `Files.walk` το κάνει με μία γραμμή κώδικα, αλλά θα προσθέσουμε ένα φίλτρο για **εξαγωγή κειμένου από PNG** μόνο όταν χρειάζεται.

```java
import java.nio.file.*;
import java.util.*;
import java.util.stream.Collectors;

// ...

// Step 3: Find all PNG and JPG images in the target directory
Path imagesRoot = Paths.get("YOUR_DIRECTORY"); // <-- replace with your path
List<Path> imagePaths = Files.walk(imagesRoot)
        .filter(p -> {
            String name = p.toString().toLowerCase();
            return name.endsWith(".png") || name.endsWith(".jpg");
        })
        .collect(Collectors.toList());

if (imagePaths.isEmpty()) {
    System.out.println("No PNG or JPG files found in " + imagesRoot);
    return;
}
```

> **Why we filter here:** Η χρήση του `filter` μας επιτρέπει να **φιλτράρουμε αρχεία κατά επέκταση** νωρίς, μειώνοντας περιττό I/O αργότερα. Επίσης διατηρεί τον κώδικα ευανάγνωστο—χωρίς ανάγκη για σύνθετα regexes.

## Βήμα 4 – Batch OCR Επεξεργασία – Υποβολή Εργασιών Ασύγχρονα

Με τη λίστα αρχείων έτοιμη, σπρώχνουμε κάθε διαδρομή στο `ParallelRecognizer`. Η μέθοδος `recognizeAsync` επιστρέφει ένα `Future<OcrResult>` που αποθηκεύουμε για μετέπειτα ανάκτηση.

```java
import java.util.concurrent.*;

// ...

// Step 4: Submit each image for asynchronous recognition
List<Future<OcrResult>> recognitionFutures = new ArrayList<>();

for (Path image : imagePaths) {
    Future<OcrResult> future = parallelRecognizer.recognizeAsync(
            image.toString(),
            RecognitionLanguage.ENGLISH); // Change language if needed
    recognitionFutures.add(future);
}
```

> **What’s happening under the hood?** Κάθε κλήση τοποθετεί μια εργασία στην εσωτερική υπηρεσία εκτελεστή του recognizer. Οι εργασίες τρέχουν παράλληλα, έτσι ένας φάκελος με 100 εικόνες μπορεί να επεξεργαστεί σε κλάσμα του χρόνου που θα απαιτούσε ένας βρόχος μονόνημα.

## Βήμα 5 – Ανάκτηση Αποτελεσμάτων στην Αρχική Σειρά – Διατήρηση της Σειράς Αρχείων

Επειδή αποθηκεύσαμε τα futures στην ίδια σειρά με το `imagePaths`, μπορούμε απλώς να διατρέξουμε τη λίστα και να καλέσουμε `get()`. Η κλήση μπλοκάρει μόνο μέχρι να ολοκληρωθεί η συγκεκριμένη εικόνα, διατηρώντας τη σειρά χωρίς επιπλέον bookkeeping.

```java
// Step 5: Retrieve and display the OCR results in the original order
for (int i = 0; i < recognitionFutures.size(); i++) {
    try {
        OcrResult result = recognitionFutures.get(i).get(); // blocks if not ready
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println(result.getText()); // The extracted text
        System.out.println("-----");
    } catch (InterruptedException | ExecutionException e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

**Sample console output** (truncated for brevity):

```
File: invoice_001.png
Invoice #001
Date: 2024‑03‑15
Total: $1,250.00
-----
File: receipt_202403.jpg
Receipt
Item A - $45.00
Item B - $30.00
Grand Total: $75.00
-----
```

> **Edge case handling:** Αν κάποια εικόνα προκαλέσει εξαίρεση (κατεστραμμένο αρχείο, μη υποστηριζόμενη μορφή), τη πιάμε και συνεχίζουμε την επεξεργασία των υπολοίπων—μια απαραίτητη συνήθεια για αξιόπιστες **batch OCR processing** pipelines.

## Βήμα 6 – Καθαρισμός – Τερματισμός του Recognizer

Μην ξεχνάτε ποτέ να τερματίσετε το εσωτερικό thread pool· διαφορετικά η JVM σας μπορεί να κολλήσει κατά την έξοδο.

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

Αυτό ήταν! Το πρόγραμμα θα περιηγηθεί σε οποιονδήποτε κατάλογο, θα φιλτράρει για αρχεία PNG/JPG, θα τρέξει OCR παράλληλα και θα εκτυπώσει τα αποτελέσματα.

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω βρίσκεται η πλήρης, έτοιμη για αντιγραφή‑και‑επικόλληση κλάση Java. Αντικαταστήστε το `"YOUR_DIRECTORY"` με τη διαδρομή του φακέλου εικόνων σας και τρέξτε το από το IDE ή τη γραμμή εντολών.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.Collectors;

public class BatchParallelExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a single OCR engine instance and a parallel recognizer that uses it
        AsposeOCR ocrEngine = new AsposeOCR();
        ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);

        // Step 2: Find all PNG and JPG images in the target directory
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        if (imagePaths.isEmpty()) {
            System.out.println("No images found – nothing to convert.");
            parallelRecognizer.shutdown();
            return;
        }

        // Step 3: Submit each image for asynchronous recognition
        List<Future<OcrResult>> recognitionFutures = new ArrayList<>();
        for (Path image : imagePaths) {
            recognitionFutures.add(
                    parallelRecognizer.recognizeAsync(
                            image.toString(),
                            RecognitionLanguage.ENGLISH));
        }

        // Step 4: Retrieve and display the OCR results in the original order
        for (int i = 0; i < recognitionFutures.size(); i++) {
            try {
                OcrResult result = recognitionFutures.get(i).get(); // blocks until processed
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println(result.getText());
                System.out.println("-----");
            } catch (InterruptedException | ExecutionException e) {
                System.err.println("Error processing " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Step 5: Shut down the recognizer to clean up its internal thread pool
        parallelRecognizer.shutdown();
    }
}
```

Τρέξτε την κλάση, παρακολουθήστε την κονσόλα να γεμίζει με εξαγόμενες συμβολοσειρές και γιορτάστε το γεγονός ότι μόλις **μετατρέψατε εικόνες σε κείμενο** χωρίς να γράψετε έναν μόνο βρόχο που μπλοκάρει στο I/O.

## Συχνές Ερωτήσεις (FAQs)

**Q: Μπορώ επίσης να επεξεργαστώ PDFs ή TIFFs;**  
A: Απόλυτα. Το Aspose OCR υποστηρίζει πολλές μορφές—απλώς προσθέστε τις κατάλληλες επεκτάσεις αρχείων στο φίλτρο στο Βήμα 2.

**Q: Τι γίνεται αν χρειάζομαι διαφορετική γλώσσα, όπως Ισπανικά;**  
A: Αλλάξτε το `RecognitionLanguage.ENGLISH` σε `RecognitionLanguage.SPANISH`. Βεβαιωθείτε ότι το language pack είναι εγκατεστημένο (το Aspose περιλαμβάνει τις περισσότερες κύριες γλώσσες από προεπιλογή).

**Q: Ο φάκελός μου περιέχει υπο‑φακέλους—θα σαρώνονται;**  
A: Ναι. Το `Files.walk` διασχίζει όλο το δέντρο αναδρομικά, έτσι κάθε εσωτερικό PNG/J

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}