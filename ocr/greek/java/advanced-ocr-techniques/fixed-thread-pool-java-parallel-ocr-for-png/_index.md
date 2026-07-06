---
category: general
date: 2026-02-17
description: Μάθετε πώς να χρησιμοποιείτε ένα σταθερό thread pool στη Java για την
  εξαγωγή κειμένου από εικόνες PNG με παράλληλη επεξεργασία OCR και το σωστό τερματισμό
  της υπηρεσίας εκτελεστή.
draft: false
keywords:
- fixed thread pool java
- extract text from png
- parallel ocr processing
- convert scanned pages text
- shut down executor service
language: el
og_description: Ανακαλύψτε πώς ένα σταθερό σύνολο νημάτων Java μπορεί να εξάγει κείμενο
  από εικόνες PNG παράλληλα, να μετατρέπει το κείμενο των σαρωμένων σελίδων και να
  τερματίζει με ασφάλεια την υπηρεσία εκτελεστή.
og_title: Σταθερό σύνολο νημάτων Java – παράλληλη OCR για PNG
tags:
- java
- ocr
- multithreading
- aspose
title: Σταθερό pool νημάτων Java – Παράλληλη OCR για PNG
url: /el/java/advanced-ocr-techniques/fixed-thread-pool-java-parallel-ocr-for-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# fixed thread pool java – παράλληλο OCR για PNG

Έχετε αναρωτηθεί ποτέ πώς να επιταχύνετε το OCR σε μια σειρά αρχείων PNG χρησιμοποιώντας ένα **fixed thread pool java**; Σε αυτό το tutorial θα δούμε πώς να **extract text from PNG** εικόνες παράλληλα, **convert scanned pages text** σε επεξεργάσιμες συμβολοσειρές, και να κλείσουμε με ασφάλεια το **shut down executor service** μόλις ολοκληρωθεί η εργασία.

Αν έχετε ποτέ κολλήσει σε έναν βρόχο μονό-νήματος που διαρκεί λεπτά, ξέρετε την απογοήτευση του να περιμένετε κάθε σελίδα να τελειώσει πριν ξεκινήσει η επόμενη. Τα καλά νέα; Με λίγες γραμμές Java και Aspose OCR μπορείτε να αξιοποιήσετε τη δύναμη όλων των πυρήνων CPU, να μετατρέψετε τις σαρωμένες σελίδες σε αναζητήσιμο κείμενο και να κρατήσετε την εφαρμογή σας ανταποκρινόμενη.  

Παρακάτω θα βρείτε ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα, μαζί με εξηγήσεις για το γιατί κάθε μέρος είναι σημαντικό, κοινές παγίδες και συμβουλές που μπορείτε να εφαρμόσετε σε οποιαδήποτε βιβλιοθήκη OCR.

---

## Τι Θα Χρειαστείτε

- **Java 17** (ή οποιοδήποτε πρόσφατο JDK) – ο κώδικας χρησιμοποιεί τη σύγχρονη σύνταξη `var` περιορισμένα, αλλά λειτουργεί και σε παλαιότερες εκδόσεις.  
- **Aspose.OCR for Java** library – μπορείτε να το κατεβάσετε από το Maven Central ή να κατεβάσετε μια δοκιμαστική έκδοση από το Aspose.  
- Ένα σύνολο αρχείων **PNG** που θέλετε να επεξεργαστείτε – σκεφτείτε αποδείξεις, σελίδες βιβλίων ή στιγμιότυπα οθόνης.  
- Βασική εξοικείωση με το Java concurrency – δεν είναι απαραίτητη, αλλά χρήσιμη.

Αυτό είναι όλο. Χωρίς εξωτερικές υπηρεσίες, χωρίς Docker, μόνο καθαρή Java και λίγη μαγεία πολυνηματισμού.

## Βήμα 1: Προσθήκη Εξάρτησης Aspose OCR & Άδειας (Προαιρετικό)

Πρώτα, βεβαιωθείτε ότι το JAR του Aspose OCR βρίσκεται στο classpath σας. Αν χρησιμοποιείτε Maven, προσθέστε:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

Αν δεν έχετε άδεια, η βιβλιοθήκη θα λειτουργήσει σε λειτουργία αξιολόγησης· ο κώδικας λειτουργεί με τον ίδιο τρόπο. Για να φορτώσετε μια άδεια (συνιστάται για παραγωγή), τοποθετήστε το `Aspose.OCR.lic` στον φάκελο resources και χρησιμοποιήστε:

```java
// Load the Aspose OCR license (optional)
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

> **Συμβουλή:** Κρατήστε το αρχείο άδειας εκτός ελέγχου έκδοσης για να αποφύγετε τυχαία έκθεση.

## Βήμα 2: Δημιουργία Ένας Thread‑Safe `OcrEngine` Αντικειμένου

Το `OcrEngine` του Aspose OCR είναι thread‑safe εφόσον επαναχρησιμοποιείτε το ίδιο αντικείμενο σε όλες τις εργασίες. Η δημιουργία του μία φορά εξοικονομεί μνήμη και αποτρέπει το κόστος επανεκκίνησης της μηχανής για κάθε εικόνα.

```java
// One shared OcrEngine for all threads
OcrEngine ocrEngine = new OcrEngine();
```

Γιατί η επαναχρήση; Σκεφτείτε τη μηχανή ως έναν βαρύ εργαζόμενο που φορτώνει μοντέλα γλώσσας στη μνήμη. Η δημιουργία νέας μηχανής ανά εικόνα θα ήταν σαν να προσλαμβάνετε νέο ειδικό για κάθε μικρή δουλειά – δαπανηρό και περιττό.

## Βήμα 3: Ρύθμιση Fixed Thread Pool Java

Τώρα έρχεται το αστέρι της παράστασης: ένα **fixed thread pool java**. Θα το διαμορφώσουμε ώστε να ταιριάζει με τον αριθμό των λογικών επεξεργαστών, ώστε κάθε πυρήνας να λαμβάνει δουλειά χωρίς υπερπλήρωση.

```java
// Determine available processors and create a fixed pool
int threadCount = Runtime.getRuntime().availableProcessors();
ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);
```

Η χρήση ενός *fixed* pool (αντί για cached) σας παρέχει προβλέψιμη χρήση πόρων και αποτρέπει τα φοβερά «out‑of‑memory» spikes όταν δεκάδες εικόνες φτάνουν ταυτόχρονα.

## Βήμα 4: Καταγραφή των PNG Αρχείων που Θέλετε να Επεξεργαστείτε (Extract Text from PNG)

Συλλέξτε τις διαδρομές προς τις εικόνες που θέλετε να OCR. Σε ένα πραγματικό έργο μπορεί να σαρώσετε έναν φάκελο ή να διαβάσετε από βάση δεδομένων· εδώ θα κωδικοποιήσουμε μερικά παραδείγματα.

```java
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/page1.png",
        "YOUR_DIRECTORY/page2.png",
        "YOUR_DIRECTORY/page3.png"
);
```

> **Σημείωση:** Η επέκταση αρχείου **png** είναι σημαντική επειδή το Aspose OCR ανιχνεύει αυτόματα τη μορφή, αλλά μπορείτε επίσης να δώσετε JPEG ή TIFF.

## Βήμα 5: Υποβολή OCR Εργασιών – Parallel OCR Processing

Κάθε εικόνα γίνεται ένα callable που επιστρέφει το αναγνωρισμένο κείμενο. Επειδή το `OcrEngine` είναι κοινόχρηστο, χρειάζεται μόνο να περάσουμε τη διαδρομή του αρχείου στην εργασία.

```java
List<Future<String>> ocrFutures = new ArrayList<>();

for (String imagePath : imageFiles) {
    ocrFutures.add(threadPool.submit(() -> {
        // Prepare input for this image
        OcrInput input = new OcrInput();
        input.add(imagePath);

        // Perform OCR using the shared engine
        OcrResult result = ocrEngine.recognize(input);

        // Return the plain text
        return result.getText();
    }));
}
```

Γιατί να το τυλίξουμε σε `Future`; Σας επιτρέπει να εκκινήσετε όλες τις εργασίες αμέσως, και στη συνέχεια να συλλέξετε τα αποτελέσματα με τη σειρά που υποβλήθηκαν – ιδανικό για τη διατήρηση της σειράς των σελίδων όταν **convert scanned pages text** ξανά σε ένα έγγραφο.

## Βήμα 6: Ανάκτηση Αποτελεσμάτων και Εμφάνιση (Convert Scanned Pages Text)

Τώρα περιμένουμε κάθε `Future` να ολοκληρωθεί και εκτυπώνουμε το αποτέλεσμα. Η κλήση `get()` μπλοκάρει μόνο μέχρι να ολοκληρωθεί η συγκεκριμένη εργασία, όχι ολόκληρο το pool.

```java
for (Future<String> future : ocrFutures) {
    System.out.println("----");
    System.out.println(future.get()); // prints OCR result for one PNG
}
```

Η τυπική έξοδος στην κονσόλα μοιάζει με:

```
----
The quick brown fox jumps over the lazy dog.
----
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----
Page 3 content goes here…
```

Αν προτιμάτε να γράψετε τα αποτελέσματα σε αρχεία, αντικαταστήστε το `System.out.println` με μια κλήση `Files.writeString`.

## Βήμα 7: Καθαρό Shut Down του Executor Service

Όταν ολοκληρωθεί κάθε εργασία, είναι κρίσιμο να **shut down executor service**· διαφορετικά η JVM μπορεί να κρατήσει μη‑daemon νήματα ενεργά, εμποδίζοντας ομαλή έξοδο.

```java
threadPool.shutdown();               // No new tasks accepted
if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
    threadPool.shutdownNow();        // Force shutdown after timeout
}
```

Το πρότυπο `awaitTermination` δίνει στο pool την ευκαιρία να τελειώσει την τρέχουσα δουλειά πριν το εξαναγκάσουμε. Η παράβλεψη αυτού του βήματος είναι κοινή πηγή διαρροών μνήμης σε εφαρμογές που τρέχουν πολύ ώρα.

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε στο `ParallelBatchDemo.java` και να τρέξετε:

```java
import com.aspose.ocr.*;

import java.util.*;
import java.util.concurrent.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license (optional)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // 2️⃣ Shared, thread‑safe OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Fixed thread pool java – one thread per core
        int threadCount = Runtime.getRuntime().availableProcessors();
        ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);

        // 4️⃣ Files to process – extract text from png
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/page1.png",
                "YOUR_DIRECTORY/page2.png",
                "YOUR_DIRECTORY/page3.png"
        );

        // 5️⃣ Submit tasks – parallel OCR processing
        List<Future<String>> ocrFutures = new ArrayList<>();
        for (String imagePath : imageFiles) {
            ocrFutures.add(threadPool.submit(() -> {
                OcrInput input = new OcrInput();
                input.add(imagePath);
                OcrResult result = ocrEngine.recognize(input);
                return result.getText();
            }));
        }

        // 6️⃣ Retrieve and print – convert scanned pages text
        for (Future<String> future : ocrFutures) {
            System.out.println("----");
            System.out.println(future.get());
        }

        // 7️⃣ Shut down executor service cleanly
        threadPool.shutdown();
        if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
            threadPool.shutdownNow();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}