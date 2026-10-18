---
category: general
date: 2026-02-09
description: Μάθετε πώς να εκτελείτε μαζική OCR σε Java με το Aspose OCR. Εξάγετε
  κείμενο από εικόνες, αναγνωρίστε κείμενο από αρχεία PNG, JPG και TIFF με μία μόνο
  κλήση.
draft: false
keywords:
- how to batch ocr
- extract text from images
- recognize text from png
- recognize text from jpg
- recognize text from tiff
language: el
og_description: Μάθετε πώς να εκτελείτε μαζική OCR σε Java. Αυτό το σεμινάριο σας
  δείχνει πώς να εξάγετε κείμενο από εικόνες PNG, JPG και TIFF χρησιμοποιώντας το
  Aspose OCR με σαφή παραδείγματα κώδικα.
og_title: Πώς να κάνετε μαζική OCR σε Java – Εξαγωγή κειμένου από εικόνες αποδοτικά
tags:
- OCR
- Java
- Aspose
title: Πώς να εκτελέσετε μαζική OCR σε Java – Πλήρης οδηγός για την εξαγωγή κειμένου
  από εικόνες
url: /el/java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να κάνετε Batch OCR σε Java – Πλήρης Οδηγός για Εξαγωγή Κειμένου από Εικόνες

Έχετε αναρωτηθεί **πώς να κάνετε batch OCR** σε μια σειρά εικόνων χωρίς να γράψετε βρόχο για κάθε αρχείο; Δεν είστε οι μόνοι. Σε πολλά πραγματικά έργα λαμβάνετε έναν φάκελο γεμάτο σκανάρισμα—αποδείξεις PNG, στιγμιότυπα JPG ή ακόμη και πολυσελίδες TIFF—και χρειάζεστε το κείμενο γρήγορα.  

Τα καλά νέα είναι ότι το Aspose OCR σας επιτρέπει ακριβώς αυτό: μία κλήση μεθόδου που αναγνωρίζει κείμενο από αρχεία PNG, JPG και TIFF ταυτόχρονα. Σε αυτό το tutorial θα περάσουμε από τη ρύθμιση του έργου μέχρι την εκτύπωση των αποτελεσμάτων, ώστε να μπορείτε να αρχίσετε να εξάγετε κείμενο από εικόνες σήμερα.

## Τι καλύπτει αυτό το Tutorial

* **Πώς να κάνετε batch OCR** χρησιμοποιώντας το `OcrBatchProcessor` της Aspose.
* Τρόποι **εξαγωγής κειμένου από εικόνες** διαφορετικών μορφών (PNG, JPG, TIFF).
* Συμβουλές για έλεγχο του parallelism ώστε η εφαρμογή σας να παραμένει αποκριτική.
* Ένα πλήρες, εκτελέσιμο πρόγραμμα Java που μπορείτε να αντιγράψετε‑επικολλήσετε και να τρέξετε αμέσως.

Δεν απαιτείται προγενέστερη εμπειρία με την Aspose—απλώς μια βασική εγκατάσταση Java και ένα IDE της επιλογής σας. Στο τέλος, θα έχετε μια σταθερή βάση για την αναγνώριση κειμένου από αρχεία PNG, JPG και TIFF μαζικά.

---

![Διάγραμμα που απεικονίζει πώς να κάνετε batch OCR σε πολλαπλά αρχεία εικόνας](/images/batch-ocr-diagram.png "πώς να κάνετε batch ocr")

*Κείμενο alt εικόνας: διάγραμμα που δείχνει πώς να κάνετε batch OCR, παρουσιάζοντας πολλαπλά αρχεία εικόνας που επεξεργάζονται μαζί.*

## Προαπαιτούμενα

| Απαίτηση | Γιατί είναι σημαντική |
|-------------|----------------|
| Java 17 ή νεότερη | Το Aspose OCR στοχεύει σε σύγχρονα JVM. |
| Maven ή Gradle | Απλοποιεί την προσθήκη της βιβλιοθήκης Aspose OCR. |
| Βασικές γνώσεις Java | Απαιτούνται για την κατανόηση της ροής κώδικα. |
| Ένα σύνολο δείγματος εικόνων (`.png`, `.jpg`, `.tif`) | Για να δείτε την εξαγωγή σε δράση. |

Αν έχετε ήδη όλα αυτά, υπέροχα—ας ξεκινήσουμε.

## Βήμα 1: Προσθήκη Aspose OCR στο Έργο σας

Το πρώτο που χρειάζεστε είναι το JAR του Aspose OCR. Με Maven, προσθέστε το στο `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

Αν προτιμάτε Gradle, το ισοδύναμο είναι:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

Η προσθήκη της εξάρτησης φέρνει όλα όσα χρειάζονται για **αναγνώριση κειμένου από png**, **αναγνώριση κειμένου από jpg**, και **αναγνώριση κειμένου από tiff**. Δεν απαιτούνται επιπλέον native βιβλιοθήκες.

## Βήμα 2: Ορισμός των Αρχείων Εικόνας που Θέλετε να Επεξεργαστείτε

Τώρα θα πούμε στη μηχανή OCR ποια αρχεία πρέπει να διαχειριστεί. Εδώ είναι που **πώς να κάνετε batch OCR** δείχνει την αξία του—απλώς περάστε μια λίστα διαδρομών και αφήστε τη βιβλιοθήκη να κάνει το σκληρό έργο.

```java
import java.util.Arrays;
import java.util.List;

// Step 2: List your image files (PNG, JPG, TIFF)
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/img1.png",   // PNG file – recognize text from png
        "YOUR_DIRECTORY/img2.jpg",   // JPG file – recognize text from jpg
        "YOUR_DIRECTORY/img3.tif");  // TIFF file – recognize text from tiff
```

> **Συμβουλή επαγγελματία:** Κρατήστε τις διαδρομές αρχείων απόλυτες ή χρησιμοποιήστε `Paths.get(...)` για να αποφύγετε εκπλήξεις σε διαφορετικά λειτουργικά συστήματα.

## Βήμα 3: Δημιουργία του Batch Processor και Ρύθμιση του Parallelism

Το Aspose OCR παρέχει το `OcrBatchProcessor`, το οποίο μπορεί να εκτελεί πολλές αναγνώσεις παράλληλα. Ο έλεγχος του αριθμού νημάτων αποτρέπει την εφαρμογή σας να καταναλώνει όλη την CPU όταν έχετε δεκάδες εικόνες.

```java
import com.aspose.ocr.OcrBatchProcessor;

// Step 3: Initialise the batch processor
OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();

// Limit to 4 concurrent threads – a sweet spot for most desktops
ocrProcessor.setMaxParallelism(4);
```

Γιατί να περιορίσουμε το parallelism; Αν τρέξετε πάρα πολλά νήματα σε ένα μέτριο laptop, μπορεί να παρατηρήσετε επιβράδυνση αντί για επιτάχυνση. Η ρύθμιση `setMaxParallelism` σας επιτρέπει να ισορροπήσετε την ταχύτητα με τη σταθερότητα.

## Βήμα 4: Εκτέλεση της Κλήσης Batch OCR

Εδώ είναι η καρδιά του **πώς να κάνετε batch OCR**: μία κλήση `recognize` που επιστρέφει μια λίστα αντικειμένων `RecognitionResult`, ένα ανά εικόνα.

```java
import com.aspose.ocr.RecognitionResult;
import java.util.List;

// Step 4: Execute batch OCR
List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);
```

Η μέθοδος μπλοκάρει μέχρι να επεξεργαστούν όλες οι εικόνες, μετά σας παραδίδει το κείμενο. Αν χρειάζεστε μη‑μπλοκαριστική συμπεριφορά, μπορείτε να τυλίξετε αυτό σε ένα `CompletableFuture`, αλλά για τα περισσότερα σενάρια η συγχρονική κλήση κρατά τον κώδικα καθαρό.

## Βήμα 5: Εκτύπωση του Εξαγόμενου Κειμένου

Τέλος, επαναλάβετε τα αποτελέσματα και εμφανίστε τις αναγνωρισμένες συμβολοσειρές. Αυτό δείχνει ότι έχουμε εξαγάγει επιτυχώς **κείμενο από εικόνες** διαφόρων μορφών.

```java
// Step 5: Output the recognized text for each file
for (int i = 0; i < recognitionResults.size(); i++) {
    System.out.println("File: " + imageFiles.get(i));
    System.out.println(recognitionResults.get(i).getText());
    System.out.println("---");
}
```

### Αναμενόμενο Αποτέλεσμα

```
File: YOUR_DIRECTORY/img1.png
The quick brown fox jumps over the lazy dog.
---
File: YOUR_DIRECTORY/img2.jpg
Invoice #12345
Total: $567.89
---
File: YOUR_DIRECTORY/img3.tif
Page 1 of 3
Report generated on 2026-02-09
---
```

Αν η μηχανή OCR δεν μπορεί να διαβάσει ένα αρχείο, η μέθοδος `getText()` επιστρέφει κενή συμβολοσειρά, οπότε μπορείτε να προσθέσετε έναν απλό έλεγχο για να καταγράψετε προειδοποιήσεις.

## Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας τα πάντα, εδώ είναι η πλήρης, έτοιμη‑για‑εκτέλεση κλάση Java. Αντιγράψτε την σε ένα αρχείο με όνομα `BatchOcrTutorial.java`, προσαρμόστε τις διαδρομές εικόνων, και τρέξτε `javac && java`.

```java
import com.aspose.ocr.*;
import java.util.Arrays;
import java.util.List;

public class BatchOcrTutorial {
    public static void main(String[] args) throws Exception {

        // Step 1: Define the image files to be processed
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/img1.png",
                "YOUR_DIRECTORY/img2.jpg",
                "YOUR_DIRECTORY/img3.tif");

        // Step 2: Create the batch OCR processor and optionally limit parallelism
        OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();
        ocrProcessor.setMaxParallelism(4); // limit to 4 concurrent threads

        // Step 3: Perform OCR on all images in a single batch call
        List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);

        // Step 4: Output the recognized text for each file
        for (int i = 0; i < recognitionResults.size(); i++) {
            System.out.println("File: " + imageFiles.get(i));
            System.out.println(recognitionResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

Τρέξτε το, και θα δείτε την κονσόλα να εκτυπώνει το εξαγόμενο κείμενο για κάθε αρχείο PNG, JPG και TIFF—ακριβώς αυτό που χρειάζεστε όταν η ερώτηση είναι **πώς να κάνετε batch OCR**.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν έχω περισσότερες από τρεις εικόνες;

Απλώς προσθέστε περισσότερες καταχωρήσεις στη λίστα `imageFiles`. Ο batch processor θα χωρίσει αυτόματα τη δουλειά στα νήματα που διαμορφώσατε με το `setMaxParallelism`.

### Οι εικόνες μου είναι σε υπο‑φάκελο—πρέπει να τις καταγράψω όλες χειροκίνητα;

Μπορείτε να συλλέξετε προγραμματιστικά όλα τα αρχεία με συγκεκριμένη επέκταση:

```java
try (Stream<Path> paths = Files.walk(Paths.get("YOUR_DIRECTORY"))) {
    List<String> imageFiles = paths
        .filter(Files::isRegularFile)
        .filter(p -> p.toString().matches(".*\\.(png|jpg|tif|tiff)$"))
        .map(Path::toString)
        .collect(Collectors.toList());
}
```

Αυτό κρατά τον κώδικα ευέλικτο και εξακολουθεί να σέβεται το **πώς να κάνετε batch OCR**.

### Πώς να χειριστώ αποτελέσματα χαμηλής εμπιστοσύνης;

Το `RecognitionResult` παρέχει τη μέθοδο `getConfidence()`. Μπορείτε να φιλτράρετε τα αποτελέσματα κάτω από ένα όριο και να ξαναδοκιμάσετε με υψηλότερες ρυθμίσεις DPI:

```java
ocrProcessor.setResolution(300); // increase DPI for better accuracy
```

### Υποστηρίζει το Aspose OCR άλλες γλώσσες;

Ναι—απλώς καλέστε `ocrProcessor.setLanguage(OcrLanguage.Spanish)` (ή οποιοδήποτε υποστηριζόμενο enum) πριν από την κλήση `recognize`. Αυτό επεκτείνει τη χρησιμότητα πέρα από τα Αγγλικά, κάνοντας το **εξαγωγή κειμένου από εικόνες** πραγματικά πολυγλωσσικό.

## Συμβουλές Απόδοσης

* **Το μέγεθος batch μετρά** – Μεγαλύτερα batches μειώνουν το overhead, αλλά πολύ μεγάλες λίστες μπορεί να καταναλώσουν περισσότερη μνήμη. Δοκιμάστε με 50–200 εικόνες ανά batch.
* **Parallelism** – Σε CPU με 4 πυρήνες, το `setMaxParallelism(4)` συνήθως δίνει την καλύτερη διαπερατότητα. Προσαρμόστε το ανάλογα με το φορτίο του διακομιστή σας.
* **Προεπεξεργασία εικόνας** – Η μετατροπή εικόνων σε γκρι ή η αύξηση της αντίθεσης πριν το OCR μπορεί να βελτιώσει την ακρίβεια, ειδικά σε θορυβώδεις σκαναρίσματα.

## Συμπέρασμα

Τώρα γνωρίζετε **πώς να κάνετε batch OCR** σε Java χρησιμοποιώντας το Aspose OCR, πώς να **εξάγετε κείμενο από εικόνες** διαφόρων μορφών, και γιατί ο έλεγχος του parallelism είναι σημαντικός. Το πλήρες παράδειγμα κώδικα δείχνει την αναγνώριση κειμένου από αρχεία PNG, JPG και TIFF με μία μόνο, αποδοτική κλήση.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να τροφοδοτήσετε την έξοδο OCR σε έναν δείκτη αναζήτησης, μια βάση δεδομένων ή ακόμη και έναν AI summarizer. Μπορείτε επίσης να πειραματιστείτε με είσοδο PDF (το Aspose OCR το υποστηρίζει) ή να συνδυάσετε αυτό με βιβλιοθήκες προεπεξεργασίας εικόνας όπως το OpenCV για ακόμη μεγαλύτερη ακρίβεια.

Καλή προγραμματιστική δουλειά, και θυμηθείτε—το batch OCR δεν χρειάζεται να είναι πρόβλημα. Με τα κατάλληλα εργαλεία και ένα σαφές μοτίβο, θα μετατρέπετε σωρούς εικόνων σε αναζητήσιμο κείμενο σε χρόνο μηδέν.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}