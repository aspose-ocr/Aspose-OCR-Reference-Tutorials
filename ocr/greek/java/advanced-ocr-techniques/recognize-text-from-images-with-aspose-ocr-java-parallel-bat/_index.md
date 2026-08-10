---
category: general
date: 2026-05-31
description: Αναγνωρίστε κείμενο από εικόνες γρήγορα χρησιμοποιώντας το Aspose OCR
  Java. Μάθετε πώς να εξάγετε κείμενο από αρχεία PNG και να ορίσετε τη γλώσσα OCR
  για βέλτιστα αποτελέσματα.
draft: false
keywords:
- recognize text from images
- extract text from png
- set OCR language
- Aspose OCR Java
- parallel OCR processing
language: el
og_description: Αναγνωρίστε κείμενο από εικόνες αποδοτικά με το Aspose OCR Java. Αυτό
  το σεμινάριο δείχνει πώς να εξάγετε κείμενο από αρχεία PNG και να ορίσετε τη γλώσσα
  OCR για επεξεργασία κατά παρτίδες.
og_title: αναγνώριση κειμένου από εικόνες – Aspose OCR Java Parallel Batch
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: recognize text from images quickly using Aspose OCR Java. Learn how
    to extract text from png files and set OCR language for optimal results.
  headline: recognize text from images with Aspose OCR – Java Parallel Batch Guide
  type: TechArticle
- description: recognize text from images quickly using Aspose OCR Java. Learn how
    to extract text from png files and set OCR language for optimal results.
  name: recognize text from images with Aspose OCR – Java Parallel Batch Guide
  steps:
  - name: How It Works
    text: '- **Thread Count** – The processor creates a thread pool of the size you
      specify. On a quad‑core laptop, `4` is a sweet spot; increase it for servers
      with more cores. - **Language Setting** – By calling `setLanguage(OcrLanguage.FRENCH)`,
      we tell the OCR engine to bias its dictionary toward French ch'
  - name: 1️⃣ Missing or Corrupt Images
    text: If an image path is invalid, `OcrBatchProcessor` throws an `IOException`.
      Wrap the call in a try‑catch block, log the problematic file, and continue with
      the rest of the batch.
  - name: 2️⃣ Mixed Languages in One Batch
    text: 'When you have documents in multiple languages, you can either:'
  - name: 3️⃣ Memory Constraints
    text: Processing very large images (e.g., >10 MB) can inflate heap usage. Pre‑scale
      the images or increase the JVM’s `-Xmx` flag if you encounter `OutOfMemoryError`.
  - name: 4️⃣ Customizing OCR Settings
    text: 'Beyond language, you can tweak recognition speed vs. accuracy:'
  - name: LicenseUtil.java
    text: '```java import com.aspose.ocr.*;'
  - name: ImageProvider.java
    text: '```java import java.util.*;'
  - name: ParallelBatchDemo.java
    text: '```java import com.aspose.ocr.*; import java.util.*;'
  type: HowTo
tags:
- Java
- OCR
- Aspose
- Image Processing
title: Αναγνώριση κειμένου από εικόνες με το Aspose OCR – Οδηγός Παράλληλης Παρτίδας
  Java
url: /el/java/advanced-ocr-techniques/recognize-text-from-images-with-aspose-ocr-java-parallel-bat/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση κειμένου από εικόνες – Aspose OCR Java Παράλληλο Batch Tutorial

Έχετε αναρωτηθεί ποτέ πώς να **αναγνωρίσετε κείμενο από εικόνες** με τρόπο που δεν κλειδώνει το UI σας; Ίσως έχετε έναν φάκελο γεμάτο σκαναρίσματα, στιγμιότυπα οθόνης ή ακόμη και ένα μείγμα αρχείων PNG και JPEG, και χρειάζεστε το κείμενο άμεσα. Τα καλά νέα; Με το Aspose OCR for Java μπορείτε να δημιουργήσετε ένα πολυνηματικό batch που **εξάγει κείμενο από png** (και άλλες μορφές) ενώ πίνετε τον καφέ σας.

Σε αυτόν τον οδηγό θα περάσουμε από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που δείχνει πώς να **ορίσετε τη γλώσσα OCR**, να εκκινήσετε τέσσερις παράλληλους εργαζόμενους και να εκτυπώσετε τα αποτελέσματα. Στο τέλος θα έχετε ένα σταθερό πρότυπο που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Java—χωρίς περιττά πρόσθετα, μόνο ο κώδικας που χρειάζεστε.

## Τι Θα Μάθετε

- Πώς να εφαρμόσετε μια άδεια Aspose OCR ώστε να μην αντιμετωπίζετε περιορισμούς αξιολόγησης.  
- Τα ακριβή βήματα για **αναγνώριση κειμένου από εικόνες** παράλληλα, αυξάνοντας την απόδοση σε πολυπύρηνες μηχανές.  
- Γιατί και πώς να **ορίσετε τη γλώσσα OCR** (Γαλλικά στο demo) για καλύτερη ακρίβεια.  
- Ένας πρακτικός τρόπος για **εξαγωγή κειμένου από png** αρχεία, αλλά η ίδια λογική λειτουργεί για JPG, TIFF, BMP κ.λπ.  

**Προαπαιτούμενα** – θα χρειαστείτε Java 8 ή νεότερη, Maven ή Gradle για να κατεβάσετε τη βιβλιοθήκη Aspose OCR, και ένα έγκυρο αρχείο άδειας Aspose OCR (`Aspose.OCR.Java.lic`). Δεν απαιτούνται ειδικά κόλπα IDE· οποιοσδήποτε επεξεργαστής που μπορεί να μεταγλωττίσει Java αρκεί.

---

## Βήμα 1: Προσθήκη Εξάρτησης Aspose OCR

Πρώτα, βεβαιωθείτε ότι το JAR του Aspose OCR βρίσκεται στο classpath. Αν χρησιμοποιείτε Maven, προσθέστε:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

Για Gradle:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

> **Pro tip:** Παρακολουθείτε τις σημειώσεις έκδοσης του Aspose· συχνά προσθέτουν πακέτα γλωσσών ή βελτιώσεις απόδοσης που μπορούν να μειώσουν δευτερόλεπτα από τις εκτελέσεις batch.

## Βήμα 2: Εφαρμογή της Άδειας Aspose OCR

Χωρίς άδεια η βιβλιοθήκη λειτουργεί σε λειτουργία demo και θα ενσωματώνει υδατογραφήματα στην έξοδο. Φορτώστε το αρχείο άδειας μία φορά, προτιμότερα κατά την εκκίνηση της εφαρμογής.

```java
import com.aspose.ocr.*;

public class LicenseUtil {
    /** Loads the Aspose OCR license from the given path. */
    public static void applyLicense(String licensePath) throws Exception {
        License license = new License();
        license.setLicense(licensePath);
        System.out.println("Aspose OCR license applied successfully.");
    }
}
```

Η κλήση `LicenseUtil.applyLicense("Aspose.OCR.Java.lic")` εξασφαλίζει ότι κάθε επόμενη κλήση **αναγνώριση κειμένου από εικόνες** εκτελείται χωρίς περιορισμούς.

## Βήμα 3: Προετοιμασία Λίστας Εικόνων

Μπορείτε να τροφοδοτήσετε τον επεξεργαστή batch οποιαδήποτε συλλογή διαδρομών αρχείων. Παρακάτω δείχνουμε **εξαγωγή κειμένου από png** μαζί με αρχεία JPEG και TIFF — απλώς αντικαταστήστε τις διαδρομές με το δικό σας φάκελο.

```java
import java.util.*;

public class ImageProvider {
    /** Returns a list of absolute image paths to be processed. */
    public static List<String> getImagePaths() {
        return Arrays.asList(
            "YOUR_DIRECTORY/doc1.png",   // PNG – our primary example
            "YOUR_DIRECTORY/doc2.jpg",
            "YOUR_DIRECTORY/doc3.tif"
        );
    }
}
```

> **Γιατί Λίστα;** Ο `OcrBatchProcessor` αναμένει ένα `List<String>` ώστε να μπορεί να διανείμει την εργασία αυτόματα μεταξύ των νημάτων.

## Βήμα 4: Διαμόρφωση και Εκτέλεση του Παράλληλου Batch Processor

Τώρα έρχεται η καρδιά του tutorial: δημιουργία ενός `OcrBatchProcessor`, καθορισμός του αριθμού των νημάτων που θα δημιουργηθούν, και **ορισμός γλώσσας OCR** στα Γαλλικά (αλλάξτε σε `OcrLanguage.ENGLISH` ή οποιαδήποτε υποστηριζόμενη γλώσσα χρειάζεστε).

```java
import com.aspose.ocr.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply the license
        LicenseUtil.applyLicense("Aspose.OCR.Java.lic");

        // 2️⃣ Gather image files
        List<String> imagePaths = ImageProvider.getImagePaths();

        // 3️⃣ Create and configure the batch processor
        OcrBatchProcessor batchProcessor = new OcrBatchProcessor();
        batchProcessor.setThreadCount(4);                 // 4 parallel workers
        batchProcessor.setLanguage(OcrLanguage.FRENCH);   // set OCR language

        // 4️⃣ Run OCR on the entire batch – this is where we **recognize text from images**
        List<OcrResult> ocrResults = batchProcessor.recognize(imagePaths);

        // 5️⃣ Output the recognized text for each file
        for (int i = 0; i < ocrResults.size(); i++) {
            System.out.println("File: " + imagePaths.get(i));
            System.out.println(ocrResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

### Πώς Λειτουργεί

- **Αριθμός Νημάτων** – Ο επεξεργαστής δημιουργεί μια ομάδα νημάτων του μεγέθους που ορίζετε. Σε ένα φορητό υπολογιστή με τετραπύρηνο, το `4` είναι ιδανικό· αυξήστε το για διακομιστές με περισσότερους πυρήνες.  
- **Ρύθμιση Γλώσσας** – Καλώντας `setLanguage(OcrLanguage.FRENCH)`, λέμε στη μηχανή OCR να προτιμήσει το λεξικό της γαλλικής γλώσσας, βελτιώνοντας δραστικά την ακρίβεια για μη‑αγγλικά έγγραφα.  
- **Batch Αναγνώριση** – Η μέθοδος `recognize` διατρέχει εσωτερικά τη λίστα, κατανέμει την εργασία και επιστρέφει ένα `List<OcrResult>` διατηρώντας τη σειρά των αρχείων. Αυτός είναι ο πιο απλός τρόπος για **αναγνώριση κειμένου από εικόνες** χωρίς να γράψετε δικό σας κώδικα διαχείρισης νημάτων.

## Βήμα 5: Επαλήθευση της Εξόδου

Όταν εκτελέσετε το πρόγραμμα, θα πρέπει να δείτε κάτι σαν:

```
File: YOUR_DIRECTORY/doc1.png
Bonjour le monde! Ceci est un test d'OCR.
---
File: YOUR_DIRECTORY/doc2.jpg
Hello world! This is an OCR test.
---
File: YOUR_DIRECTORY/doc3.tif
¡Hola mundo! Prueba de OCR.
---
```

Αν το γαλλικό αρχείο (`doc1.png`) περιέχει γαλλικό κείμενο, το βήμα **ορισμός γλώσσας OCR** θα έχει βοηθήσει στην σωστή καταγραφή των τονισμένων χαρακτήρων. Για αρχεία PNG, αυτό δείχνει έναν καθαρό τρόπο **εξαγωγής κειμένου από png** ενώ χειρίζεται και άλλες μορφές στο ίδιο batch.

---

## Διαχείριση Συνηθισμένων Περιπτώσεων

### 1️⃣ Ελλιπή ή Κατεστραμμένα Αρχεία Εικόνας

Αν μια διαδρομή εικόνας είναι άκυρη, ο `OcrBatchProcessor` ρίχνει `IOException`. Τυλίξτε την κλήση σε μπλοκ try‑catch, καταγράψτε το προβληματικό αρχείο και συνεχίστε με το υπόλοιπο batch.

```java
try {
    List<OcrResult> results = batchProcessor.recognize(imagePaths);
} catch (IOException ex) {
    System.err.println("Failed to process: " + ex.getMessage());
}
```

### 2️⃣ Μικτές Γλώσσες σε Ένα Batch

Όταν έχετε έγγραφα σε πολλές γλώσσες, μπορείτε είτε:

- Να εκτελέσετε ξεχωριστά batches, το καθένα με το δικό του `setLanguage`.  
- Ή να αφήσετε τη γλώσσα ακαθορισμένη (`OcrLanguage.AUTO_DETECT`) και να αφήσετε το Aspose να μαντέψει, αν και η ακρίβεια μπορεί να μειωθεί.

### 3️⃣ Περιορισμοί Μνήμης

Η επεξεργασία πολύ μεγάλων εικόνων (π.χ. >10 MB) μπορεί να αυξήσει τη χρήση heap. Προσυμπιέστε τις εικόνες ή αυξήστε τη σημαία `-Xmx` της JVM αν αντιμετωπίσετε `OutOfMemoryError`.

```bash
java -Xmx2g -cp yourapp.jar ParallelBatchDemo
```

### 4️⃣ Προσαρμογή Ρυθμίσεων OCR

Πέρα από τη γλώσσα, μπορείτε να ρυθμίσετε την ταχύτητα αναγνώρισης έναντι της ακρίβειας:

```java
batchProcessor.setRecognitionMode(OcrRecognitionMode.ACCURATE); // default is BALANCED
```

Η επιλογή `ACCURATE` είναι πιο αργή αλλά προσφέρει καλύτερα αποτελέσματα για θορυβώδεις σκαναρίσματα.

---

## Πλήρες Παράδειγμα Εργασίας (Όλα τα Αρχεία)

Παρακάτω βρίσκεται το πλήρες σύνολο των αρχείων πηγής που χρειάζεστε. Αντιγράψτε τα σε ένα έργο Maven, προσαρμόστε τη διαδρομή της άδειας και του φακέλου εικόνων, και εκτελέστε `mvn exec:java -Dexec.mainClass=ParallelBatchDemo`.

### LicenseUtil.java
```java
import com.aspose.ocr.*;

public class LicenseUtil {
    public static void applyLicense(String licensePath) throws Exception {
        License license = new License();
        license.setLicense(licensePath);
        System.out.println("Aspose OCR license applied successfully.");
    }
}
```

### ImageProvider.java
```java
import java.util.*;

public class ImageProvider {
    public static List<String> getImagePaths() {
        return Arrays.asList(
            "YOUR_DIRECTORY/doc1.png",
            "YOUR_DIRECTORY/doc2.jpg",
            "YOUR_DIRECTORY/doc3.tif"
        );
    }
}
```

### ParallelBatchDemo.java
```java
import com.aspose.ocr.*;
import java.util.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // Apply license
        LicenseUtil.applyLicense("Aspose.OCR.Java.lic");

        // Gather images
        List<String> imagePaths = ImageProvider.getImagePaths();

        // Configure batch processor
        OcrBatchProcessor batchProcessor = new OcrBatchProcessor();
        batchProcessor.setThreadCount(4);                 // Parallelism
        batchProcessor.setLanguage(OcrLanguage.FRENCH);   // set OCR language

        // Recognize text from images
        List<OcrResult> ocrResults = batchProcessor.recognize(imagePaths);

        // Output results
        for (int i = 0; i < ocrResults.size(); i++) {
            System.out.println("File: " + imagePaths.get(i));
            System.out.println(ocrResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

Τρέξτε το και θα δείτε το κείμενο που εξήχθη από κάθε αρχείο να εκτυπώνεται στην κονσόλα—ακριβώς ό,τι χρειάζεστε όταν δημιουργείτε αναζητήσιμα αρχεία, αυτοματισμούς εισαγωγής δεδομένων ή εργαλεία προσβασιμότητας.

---

## Συμπέρασμα

Μόλις καλύψαμε ένα πλήρες, έτοιμο για παραγωγή πρότυπο για **αναγνώριση κειμένου από εικόνες** χρησιμοποιώντας το Aspose OCR for Java. Διαμορφώνοντας τον batch processor, μπορείτε να **εξάγετε κείμενο από png** (και άλλες μορφές) παράλληλα, και η δυνατότητα **ορισμού γλώσσας OCR** εξασφαλίζει τη μέγιστη δυνατή ακρίβεια για πολυγλωσσικά φορτία εργασίας.

Τι θα κάνετε στη συνέχεια; Δοκιμάστε να αλλάξετε τη γλώσσα σε `OcrLanguage.SPANISH` ή πειραματιστείτε με `OcrRecognitionMode.ACCURATE` για πιο δύσκολα σκαναρίσματα. Μπορείτε επίσης να ενσωματώσετε τα αποτελέσματα σε μια βάση δεδομένων, να τα τροφοδοτήσετε σε ευρετήριο αναζήτησης ή να τα περάσετε σε API μετάφρασης.

Έχετε κάποιο δύσκολο σενάριο—όπως OCR σε PDF ή σε εικόνες αποθηκευμένες στο cloud; Αυτά είναι φυσικές επεκτάσεις του τι χτίσαμε σήμερα. Βυθιστείτε, προσαρμόστε τις ρυθμίσεις και αφήστε τη μηχανή OCR να κάνει το σκληρό έργο.

Καλό κώδικα, και εύχομαι η εξαγωγή κειμένου σας να είναι γρήγορη και ακριβής!

## Τι Να Μάθετε Στη Σύντομη Μελλοντική

- [Εξαγωγή Κειμένου από Εικόνες – Βασικά OCR με Aspose.OCR για Java](/ocr/english/java/ocr-basics/)
- [Πώς να κάνετε OCR Κειμένου Εικόνας με Γλώσσα Χρησιμοποιώντας Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [αναγνώριση κειμένου εικόνας με Aspose OCR – Πλήρες Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}