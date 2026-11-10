---
category: general
date: 2026-09-18
description: Μάθετε πώς να εξάγετε κείμενο από εικόνες σε Java χρησιμοποιώντας Aspose
  OCR. Επεξεργαστείτε μαζικά αρχεία PNG, JPG και TIFF αποδοτικά σε μία κλήση.
keywords:
- extract text from images
- convert images to text
- how to batch ocr
- extract text from png
- extract text from jpg
- extract text from tiff
lastmod: 2026-09-18
og_description: Κατακτήστε την εξαγωγή κειμένου από εικόνες σε Java με batch OCR.
  Χρησιμοποιήστε Aspose OCR για να μετατρέψετε αρχεία PNG, JPG και TIFF σε μία κλήση.
og_image_alt: Diagram showing multiple image files processed together for batch OCR
og_title: Εξαγωγή κειμένου από εικόνες σε Java – οδηγός batch OCR
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to extract text from images in Java using Aspose OCR. Batch
    process PNG, JPG, and TIFF files efficiently in a single call.
  headline: How to extract text from images in Java by batch OCR
  type: TechArticle
- questions:
  - answer: Yes, Aspose OCR is pure Java and requires no UI components, so it works
      perfectly on headless environments.
    question: Can I run this on a headless server?
  - answer: A commercial license is needed for production deployments; a free trial
      is available for evaluation.
    question: Is a license required for production use?
  - answer: Any OS that can run Java 17+, including Windows, Linux, and macOS.
    question: Which operating systems are supported?
  - answer: Over 60 languages are supported out of the box, ranging from English and
      Spanish to Arabic and Chinese.
    question: How many languages can Aspose OCR recognise?
  - answer: Individual image files up to 200 MB are supported; larger files should
      be split before processing.
    question: What is the maximum file size Aspose OCR can handle?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: Πώς να εξάγετε κείμενο από εικόνες σε Java με batch OCR
url: /el/java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εξάγετε κείμενο από εικόνες σε Java με batch OCR

Αν χρειάζεστε **εξαγωγή κειμένου από εικόνες** γρήγορα και χωρίς να γράψετε βρόχο για κάθε αρχείο, το batch OCR είναι η λύση. Σε πολλά πραγματικά έργα λαμβάνετε έναν φάκελο γεμάτο σαρώσεις—αποδείξεις PNG, στιγμιότυπα JPG ή πολυσελίδες TIFF—και πρέπει να τις μετατρέψετε σε αναζητήσιμο κείμενο. Το Aspose OCR σας επιτρέπει να το κάνετε αυτό με μία κλήση μεθόδου που επεξεργάζεται αρχεία PNG, JPG και TIFF μαζί, εξοικονομώντας χρόνο ανάπτυξης και κύκλους CPU.

## Γρήγορες απαντήσεις
- **Τι κάνει το batch OCR;** Επεξεργάζεται πολλαπλά αρχεία εικόνας σε μία αίτηση, επιστρέφοντας κείμενο για κάθε αρχείο.
- **Ποιες μορφές υποστηρίζονται;** PNG, JPG/JPEG και πολυσελίδες TIFF υποστηρίζονται από προεπιλογή.
- **Χρειάζομαι ξεχωριστή εγγενή βιβλιοθήκη;** Όχι, το JAR του Aspose OCR περιέχει όλα όσα χρειάζεστε.
- **Μπορώ να ελέγξω πόσα νήματα εκτελούνται;** Ναι, χρησιμοποιήστε `setMaxParallelism` στον batch επεξεργαστή.
- **Ποια έκδοση της Java απαιτείται;** Java 17 ή νεότερη.

## Τι είναι το Aspose OCR;
Το Aspose OCR είναι μια βιβλιοθήκη Java που αναγνωρίζει τυπωμένο και χειρόγραφο κείμενο σε αρχεία εικόνας χωρίς εξωτερικές εξαρτήσεις. Υποστηρίζει πάνω από 60 γλώσσες και μπορεί να επεξεργαστεί έως 100 εικόνες ανά batch, καθιστώντας το ιδανικό για μεγάλης κλίμακας ψηφιοποίηση εγγράφων.

## Τι καλύπτει αυτό το tutorial
Φορτώστε μια λίστα διαδρομών εικόνων, δημιουργήστε ένα `OcrBatchProcessor`, ρυθμίστε την παραλληλία, εκτελέστε μία κλήση `recognize` και εκτυπώστε τις εξαγόμενες συμβολοσειρές. Στο τέλος θα έχετε ένα έτοιμο πρόγραμμα Java που εξάγει κείμενο από αρχεία PNG, JPG και TIFF μαζικά.

- **Πώς να κάνετε batch OCR** χρησιμοποιώντας το `OcrBatchProcessor` του Aspose.
- Τρόποι **εξαγωγής κειμένου από εικόνες** διαφορετικών μορφών (PNG, JPG, TIFF).
- Συμβουλές για έλεγχο της παραλληλίας ώστε η εφαρμογή σας να παραμένει αποκριτική.
- Ένα πλήρες, εκτελέσιμο πρόγραμμα Java που μπορείτε να αντιγράψετε‑επικολλήσετε και να τρέξετε αμέσως.

Δεν απαιτείται προηγούμενη εμπειρία με το Aspose—απλώς μια βασική εγκατάσταση Java και ένα IDE της επιλογής σας. Στο τέλος, θα έχετε μια σταθερή βάση για την αναγνώριση κειμένου από αρχεία PNG, JPG και TIFF μαζικά.

---

![Διάγραμμα που δείχνει πώς γίνεται batch OCR σε πολλαπλά αρχεία εικόνας](/images/batch-ocr-diagram.png "πώς να κάνετε batch OCR")

*Κείμενο alt εικόνας: διάγραμμα που δείχνει πώς γίνεται batch OCR σε πολλαπλά αρχεία εικόνας.*

## Προαπαιτούμενα

| Απαίτηση | Γιατί είναι σημαντικό |
|-------------|----------------|
| Java 17 ή νεότερη | Το Aspose OCR στοχεύει σε σύγχρονα JVM. |
| Maven ή Gradle | Απλοποιεί την προσθήκη της βιβλιοθήκης Aspose OCR. |
| Βασικές γνώσεις Java | Απαιτούνται για την κατανόηση της ροής κώδικα. |
| Ένα σύνολο δείγματος εικόνων (`.png`, `.jpg`, `.tif`) | Για να δείτε την εξαγωγή σε δράση. |

Αν έχετε ήδη όλα αυτά, υπέροχα—ας βουτήξουμε.

## Βήμα 1: προσθέστε το Aspose OCR στο έργο σας

Το πρώτο πράγμα που χρειάζεστε είναι το JAR του Aspose OCR. Με Maven, προσθέστε το στο `pom.xml`:

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

Η προσθήκη της εξάρτησης φέρνει όλα όσα απαιτούνται για **εξαγωγή κειμένου από png**, **εξαγωγή κειμένου από jpg**, και **εξαγωγή κειμένου από tiff**. Δεν χρειάζονται επιπλέον εγγενείς βιβλιοθήκες.

## Βήμα 2: ορίστε τα αρχεία εικόνας που θέλετε να επεξεργαστείτε

Τώρα θα πούμε στη μηχανή OCR ποια αρχεία πρέπει να διαχειριστεί. Εδώ το **πώς να κάνετε batch OCR** δείχνει την αξία του—απλώς περάστε μια λίστα διαδρομών και αφήστε τη βιβλιοθήκη να κάνει το σκληρό έργο.

```java
import java.util.Arrays;
import java.util.List;

// Step 2: List your image files (PNG, JPG, TIFF)
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/img1.png",   // PNG file – recognize text from png
        "YOUR_DIRECTORY/img2.jpg",   // JPG file – recognize text from jpg
        "YOUR_DIRECTORY/img3.tif");  // TIFF file – recognize text from tiff
```

> **Συμβουλή:** Κρατήστε τις διαδρομές αρχείων απόλυτες ή χρησιμοποιήστε `Paths.get(...)` για να αποφύγετε εκπλήξεις σε διαφορετικά λειτουργικά συστήματα.

## Βήμα 3: δημιουργήστε τον batch επεξεργαστή και ρυθμίστε την παραλληλία

Το Aspose OCR παρέχει το `OcrBatchProcessor`, το οποίο μπορεί να εκτελεί πολλές αναγνώσεις ταυτόχρονα. Ο έλεγχος του αριθμού των νημάτων αποτρέπει την εφαρμογή σας να καταναλώνει υπερβολικά CPU όταν έχετε δεκάδες εικόνες.

```java
import com.aspose.ocr.OcrBatchProcessor;

// Step 3: Initialise the batch processor
OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();

// Limit to 4 concurrent threads – a sweet spot for most desktops
ocrProcessor.setMaxParallelism(4);
```

Γιατί να περιορίσετε την παραλληλία; Αν τρέξετε πάρα πολλά νήματα σε ένα μέτριο laptop, μπορεί να παρατηρήσετε επιβράδυνση αντί για επιτάχυνση. Η ρύθμιση `setMaxParallelism` σας επιτρέπει να ισορροπήσετε την ταχύτητα και τη σταθερότητα.

## Βήμα 4: εκτελέστε την κλήση batch OCR

Εδώ είναι η καρδιά του **πώς να κάνετε batch OCR**: μία κλήση `recognize` που επιστρέφει μια λίστα αντικειμένων `RecognitionResult`, ένα για κάθε εικόνα.  
Η `recognize` επεξεργάζεται τις παρεχόμενες εικόνες και επιστρέφει μια λίστα `RecognitionResult`, το καθένα περιέχει το εξαγόμενο κείμενο.

```java
import com.aspose.ocr.RecognitionResult;
import java.util.List;

// Step 4: Execute batch OCR
List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);
```

Η μέθοδος μπλοκάρει μέχρι να επεξεργαστούν όλες οι εικόνες, μετά σας παραδίδει το κείμενο. Αν χρειάζεστε μη‑συγχρονιστική συμπεριφορά, μπορείτε να το τυλίξετε σε `CompletableFuture`, αλλά για τα περισσότερα σενάρια η συγχρονική κλήση κρατάει τον κώδικα καθαρό.

## Βήμα 5: εκτυπώστε το εξαγόμενο κείμενο

Τέλος, επαναλάβετε τα αποτελέσματα και εμφανίστε τις αναγνωρισμένες συμβολοσειρές. Αυτό δείχνει ότι έχουμε εξαγάγει επιτυχώς **κείμενο από εικόνες** διαφόρων μορφών.  
Το `RecognitionResult` περιέχει το OCR αποτέλεσμα για μία εικόνα, συμπεριλαμβανομένου του εξαγόμενου κειμένου και του βαθμού εμπιστοσύνης.

```java
// Step 5: Output the recognized text for each file
for (int i = 0; i < recognitionResults.size(); i++) {
    System.out.println("File: " + imageFiles.get(i));
    System.out.println(recognitionResults.get(i).getText());
    System.out.println("---");
}
```

### Αναμενόμενη έξοδος

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

Αν η μηχανή OCR δεν μπορεί να διαβάσει ένα αρχείο, η μέθοδος `getText()` επιστρέφει κενή συμβολοσειρά, ώστε να μπορείτε να προσθέσετε έναν απλό έλεγχο για καταγραφή προειδοποιήσεων.

## Πλήρες λειτουργικό παράδειγμα

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι η πλήρης, έτοιμη‑για‑εκτέλεση κλάση Java. Αντιγράψτε την σε ένα αρχείο με όνομα `BatchOcrTutorial.java`, προσαρμόστε τις διαδρομές εικόνων και τρέξτε `javac && java`.

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

Τρέξτε το και θα δείτε την κονσόλα να εκτυπώνει το εξαγόμενο κείμενο για κάθε αρχείο PNG, JPG και TIFF—ακριβώς αυτό που χρειάζεστε όταν η ερώτηση είναι **πώς να κάνετε batch OCR**.

## Συχνές ερωτήσεις & ειδικές περιπτώσεις

### Τι γίνεται αν έχω περισσότερες από τρεις εικόνες;
Απλώς προσθέστε περισσότερες καταχωρήσεις στη λίστα `imageFiles`. Ο batch επεξεργαστής θα χωρίσει αυτόματα τη δουλειά στα νήματα που έχετε ρυθμίσει με `setMaxParallelism`.

### Οι εικόνες μου βρίσκονται σε υποφάκελο—πρέπει να τις απαριθμήσω όλες χειροκίνητα;
Η `Files.list` επιστρέφει ένα ροή διαδρομών σε έναν κατάλογο.

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

### Πώς να διαχειριστώ αποτελέσματα χαμηλής εμπιστοσύνης;
Η `getConfidence()` επιστρέφει έναν αριθμητικό δείκτη εμπιστοσύνης που υποδεικνύει πόσο πιθανό είναι το αναγνωρισμένο κείμενο να είναι σωστό.

```java
ocrProcessor.setResolution(300); // increase DPI for better accuracy
```

### Υποστηρίζει το Aspose OCR άλλες γλώσσες;
Ναι—καλέστε `ocrProcessor.setLanguage(OcrLanguage.Spanish)` (ή οποιοδήποτε υποστηριζόμενο enum) πριν από την κλήση `recognize`. Αυτό επεκτείνει τη χρησιμότητα πέρα από τα Αγγλικά, κάνοντας την **εξαγωγή κειμένου από εικόνες** πραγματικά πολύγλωσση.

## Συμβουλές απόδοσης

* **Το μέγεθος του batch έχει σημασία** – Μεγαλύτερα batches μειώνουν το κόστος, αλλά πολύ μεγάλες λίστες μπορεί να καταναλώσουν περισσότερη μνήμη. Δοκιμάστε με 50–200 εικόνες ανά batch.
* **Παραλληλία** – Σε CPU με 4 πυρήνες, το `setMaxParallelism(4)` συνήθως δίνει την καλύτερη απόδοση. Προσαρμόστε ανάλογα με το φορτίο του διακομιστή σας.
* **Προεπεξεργασία εικόνας** – Η μετατροπή εικόνων σε γκρι ή η αύξηση της αντίθεσης πριν το OCR μπορεί να βελτιώσει την ακρίβεια, ειδικά για θορυβώδεις σαρώσεις.

## Συμπέρασμα

Τώρα ξέρετε **πώς να κάνετε batch OCR** σε Java χρησιμοποιώντας το Aspose OCR, πώς να **εξάγετε κείμενο από εικόνες** διαφόρων μορφών, και γιατί η παραλληλία είναι σημαντική. Το πλήρες παράδειγμα κώδικα δείχνει την αναγνώριση κειμένου από PNG, JPG και TIFF σε μία αποδοτική κλήση.

Έτοιμοι για το επόμενο βήμα; Ενσωματώστε το OCR αποτέλεσμα σε ευρετήριο αναζήτησης, βάση δεδομένων ή AI summariser. Μπορείτε επίσης να πειραματιστείτε με είσοδο PDF (το Aspose OCR το υποστηρίζει) ή να συνδυάσετε αυτό με βιβλιοθήκες προεπεξεργασίας εικόνας όπως το OpenCV για ακόμη μεγαλύτερη ακρίβεια.

Καλή προγραμματιστική, και θυμηθείτε—το batch OCR δεν χρειάζεται να είναι πρόβλημα. Με τα σωστά εργαλεία και ένα σαφές μοτίβο, θα μετατρέπετε σωρούς εικόνων σε αναζητήσιμο κείμενο σε χρόνο μηδέν.

## Συχνές ερωτήσεις

**Ε: Μπορώ να τρέξω αυτό σε server χωρίς οθόνη;**  
Α: Ναι, το Aspose OCR είναι καθαρά Java και δεν απαιτεί UI στοιχεία, λειτουργεί άψογα σε περιβάλλοντα headless.

**Ε: Απαιτείται άδεια για παραγωγική χρήση;**  
Α: Ναι, απαιτείται εμπορική άδεια για παραγωγικές εγκαταστάσεις· διατίθεται δωρεάν δοκιμαστική έκδοση για αξιολόγηση.

**Ε: Ποια λειτουργικά συστήματα υποστηρίζονται;**  
Α: Οποιοδήποτε OS μπορεί να τρέξει Java 17+, συμπεριλαμβανομένων Windows, Linux και macOS.

**Ε: Πόσες γλώσσες μπορεί να αναγνωρίσει το Aspose OCR;**  
Α: Υπάρχουν πάνω από 60 γλώσσες διαθέσιμες από προεπιλογή, από τα Αγγλικά και Ισπανικά μέχρι Αραβικά και Κινέζικα.

**Ε: Ποιο είναι το μέγιστο μέγεθος αρχείου που μπορεί να χειριστεί το Aspose OCR;**  
Α: Υποστηρίζονται μεμονωμένα αρχεία εικόνας έως 200 MB· μεγαλύτερα αρχεία πρέπει να χωριστούν πριν την επεξεργασία.

---

**Τελευταία ενημέρωση:** 2026-09-18  
**Δοκιμασμένο με:** Aspose OCR 24.9 for Java  
**Συγγραφέας:** Aspose

## Σχετικά Tutorials

- [Extract Text from Images – OCR Basics for Java](/ocr/java/ocr-basics/)
- [How To Batch Ocr In Java Complete Guide To Extract Text From](/ocr/java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/)
- [Preprocess Image Ocr In Java Boost Accuracy Extract Text](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}