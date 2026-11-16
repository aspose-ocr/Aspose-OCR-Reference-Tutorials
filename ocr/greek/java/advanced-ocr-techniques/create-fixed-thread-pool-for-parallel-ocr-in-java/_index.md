---
category: general
date: 2026-05-03
description: Δημιουργήστε σταθερό σύνολο νημάτων στην Java για να εξάγετε κείμενο
  από εικόνες γρήγορα. Μάθετε πώς να εκτελείτε OCR, να μετατρέπετε την εικόνα σε κείμενο
  και να ενισχύετε την απόδοση με παράλληλη επεξεργασία OCR.
draft: false
keywords:
- create fixed thread pool
- extract text from images
- how to run OCR
- convert image to text
- parallel OCR processing
language: el
og_description: Δημιουργήστε σταθερό σύνολο νημάτων στην Java για γρήγορη εξαγωγή
  κειμένου από εικόνες. Μάθετε πώς να εκτελείτε OCR, να μετατρέπετε εικόνα σε κείμενο
  και να ενισχύετε την απόδοση με παράλληλη επεξεργασία OCR.
og_title: Δημιουργία Σταθερής Πισίνας Νημάτων για Παράλληλο OCR σε Java
tags:
- Java
- OCR
- Multithreading
title: Δημιουργία Σταθερής Πισίνας Νημάτων για Παράλληλη OCR σε Java
url: /el/java/advanced-ocr-techniques/create-fixed-thread-pool-for-parallel-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Σταθερού Πισίνας Νημάτων για Παράλληλο OCR σε Java

Έχετε ποτέ χρειαστεί να **create fixed thread pool** για να επιταχύνετε τις εργασίες OCR, αλλά δεν ήξερες από πού να ξεκινήσετε; Δεν είστε μόνοι. Σε πολλά έργα με πολλές εικόνες το στενό σημείο είναι η κλήση OCR με ένα νήμα, και η λύση είναι εκπληκτικά απλή: δημιουργήστε μια πισίνα εργαζομένων νημάτων και αφήστε τα να επεξεργάζονται τα αρχεία παράλληλα.  

Σε αυτό το tutorial θα μάθετε πώς να **extract text from images** χρησιμοποιώντας Aspose OCR, πώς να **run OCR** αποδοτικά, και πώς να **convert image to text** χωρίς να υπερφορτώνετε την CPU σας. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση πρόγραμμα Java που δείχνει **parallel OCR processing** σε ένα μικρό σύνολο δείγματος εικόνων.

## Τι Θα Κατασκευάσετε

Θα φτιάξουμε μια μικρή εφαρμογή κονσόλας που:

* Διαβάζει μια λίστα διαδρομών εικόνων (PNG, JPG, TIFF, BMP).
* **Creates a fixed thread pool** με μέγεθος ίσο με τον αριθμό των πυρήνων της CPU.
* Αποστέλλει μια εργασία OCR για κάθε εικόνα.
* Συλλέγει το αναγνωρισμένο κείμενο και το εκτυπώνει στην κονσόλα.
* Κλείνει τον εκτελεστή (executor) καθαρά.

Καμία εξωτερική εργαλειοθήκη κατασκευής, κανένα περίπλοκο framework—απλώς καθαρή Java και η βιβλιοθήκη Aspose OCR. Αν έχετε Java 8+ και ένα καλό IDE, είστε έτοιμοι.

## Προαπαιτούμενα

* **Java Development Kit (JDK) 8 or newer** – ο κώδικας χρησιμοποιεί lambdas, οπότε παλαιότερες εκδόσεις δεν θα μεταγλωττιστούν.
* **Aspose OCR for Java** – κατεβάστε το JAR από την ιστοσελίδα Aspose ή προσθέστε το μέσω Maven (`com.aspose:aspose-ocr`).
* Ένας φάκελος με μερικές δοκιμαστικές εικόνες (ο κώδικας δείχνει στο `YOUR_DIRECTORY`).  
* Βασική εξοικείωση με τη σύγχρονη Java (θα εξηγήσουμε τα υπόλοιπα).

> *Pro tip:* Αν χρησιμοποιείτε Maven, προσθέστε την εξάρτηση στο `pom.xml` και αφήστε το IDE να διαχειριστεί το classpath.  

---

## Step 1: Add the Required Imports

Πρώτα, φέρνουμε τις κλάσεις που χρειαζόμαστε στο πεδίο ορατότητας. Αυτό δεν είναι απλώς boiler‑plate· κάθε import λέει στο JVM πού να βρει τη μηχανή OCR, τα βοηθητικά εργαλεία επεξεργασίας εικόνας, και τα εργαλεία σύγχρονης εκτέλεσης που μας επιτρέπουν να **create fixed thread pool**.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;
```

* `com.aspose.ocr.*` – το βασικό OCR API.  
* `java.util.*` – συλλογές για αποθήκευση διαδρομών εικόνων και αποτελεσμάτων.  
* `java.util.concurrent.*` – το πακέτο σύγχρονης εκτέλεσης που περιέχει `ExecutorService` και `Future`.

---

## Step 2: Define the Images to Process

Στη συνέχεια, καταγράφουμε τα αρχεία από τα οποία θέλουμε να **extract text from images**. Η χρήση του `Arrays.asList` κρατά τον κώδικα σύντομο και μας επιτρέπει να αντικαταστήσουμε το δικό σας φάκελο χωρίς να αλλάξουμε τη λογική.

```java
List<String> imagePaths = Arrays.asList(
        "YOUR_DIRECTORY/image1.png",
        "YOUR_DIRECTORY/image2.jpg",
        "YOUR_DIRECTORY/image3.tif",
        "YOUR_DIRECTORY/image4.bmp"
);
```

Μπορείτε να προσθέσετε περισσότερες καταχωρήσεις· η πισίνα νημάτων θα κλιμακωθεί αυτόματα με βάση τον αριθμό των πυρήνων της CPU που διαθέτετε.

---

## Step 3: **Create Fixed Thread Pool** Matching the CPU Cores

Αυτή είναι η καρδιά του tutorial. Ρωτάμε το runtime πόσοι πυρήνες είναι διαθέσιμοι και ζητάμε από το εργοστάσιο `Executors` να μας δώσει μια πισίνα ακριβώς αυτού του μεγέθους. Γιατί σταθερό; Επειδή ένας προβλέψιμος αριθμός νημάτων αποτρέπει την ανεπιθύμητη «έκρηξη νημάτων» που μπορεί να αφανίσει τους πόρους του λειτουργικού συστήματος.

```java
int coreCount = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(coreCount);
```

* `availableProcessors()` επιστρέφει τον λογικό αριθμό πυρήνων (συμπεριλαμβανομένων των hyper‑threads).  
* `newFixedThreadPool(coreCount)` εγγυάται ότι δεν θα ξεπεράσουμε ποτέ τη δυνατότητα της CPU, που είναι ο ασφαλέστερος τρόπος να **run OCR** παράλληλα.

---

## Step 4: Submit an OCR Task for Each Image

Τώρα μετατρέπουμε κάθε διαδρομή αρχείου σε ένα callable που **runs OCR**, αναγνωρίζει το κείμενο και επιστρέφει το αποτέλεσμα. Παρατηρήστε ότι δημιουργούμε ένα νέο `OcrEngine` μέσα στο lambda· αυτό αποτρέπει την μη‑ασφαλή κοινή χρήση της κατάστασης της μηχανής μεταξύ νημάτων.

```java
List<Future<String>> ocrResults = new ArrayList<>();
for (String path : imagePaths) {
    ocrResults.add(executor.submit(() -> {
        OcrEngine engine = new OcrEngine();          // fresh engine per task
        engine.setImage(ImageStream.fromFile(path));
        engine.getLanguage().setEnglish(true);
        return engine.recognize() ? engine.getText()
                                   : "Failed: " + path;
    }));
}
```

* Κάθε κλήση `submit` παραδίδει το lambda στην πισίνα, η οποία το προγραμματίζει σε ένα αδρανές νήμα.  
* Τα αντικείμενα `Future<String>` μας επιτρέπουν να ανακτήσουμε το αναγνωρισμένο κείμενο αργότερα, διατηρώντας τη σειρά αν το χρειάζεστε.

---

## Step 5: Retrieve and Display the Recognized Text

Μόλις όλες οι εργασίες μπουν στην ουρά, απλώς διατρέχουμε τη λίστα `Future`, καλώντας `get()` για να μπλοκάρουμε μέχρι να ολοκληρωθεί κάθε εργασία OCR. Εδώ γίνεται ορατό το βήμα **convert image to text**: η κλήση `engine.getText()` επιστρέφει το ακατέργαστο string.

```java
for (Future<String> result : ocrResults) {
    System.out.println("OCR result:\n" + result.get());
}
```

Η τυπική έξοδος στην κονσόλα μοιάζει με:

```
OCR result:
Hello world!
OCR result:
Invoice #12345
Date: 2026‑04‑30
...
```

Αν κάποιο αρχείο αποτύχει (π.χ. είναι κατεστραμμένο), θα δείτε μια γραμμή που αρχίζει με `Failed:` ακολουθούμενη από τη διαδρομή—χρήσιμο για γρήγορο debugging.

---

## Step 6: Clean Up the Executor Service

Ποτέ μην ξεχνάτε να κλείσετε την πισίνα· διαφορετικά η JVM μπορεί να παραμείνει ενεργή, νομίζοντας ότι υπάρχει ακόμη δουλειά. Ένα καλοσχεδιασμένο κλείσιμο επιτρέπει σε τυχόν ενεργές εργασίες να ολοκληρωθούν πριν τερματιστεί η διαδικασία.

```java
executor.shutdown();
```

Μπορείτε επίσης να καλέσετε `awaitTermination` αν χρειάζεται να επιβάλετε χρονικό όριο, αλλά για τις περισσότερες εφαρμογές γραμμής εντολών ένα απλό `shutdown()` αρκεί.

---

## Full Working Example

Παρακάτω βρίσκεται το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα. Αντιγράψτε‑και‑επικολλήστε το σε ένα αρχείο με όνομα `ParallelOcrTutorial.java`, προσαρμόστε τις διαδρομές εικόνων, και τρέξτε `javac` + `java` όπως συνήθως.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;

public class ParallelOcrTutorial {
    public static void main(String[] args) throws Exception {
        // Step 2: Define the images to be processed
        List<String> imagePaths = Arrays.asList(
                "YOUR_DIRECTORY/image1.png",
                "YOUR_DIRECTORY/image2.jpg",
                "YOUR_DIRECTORY/image3.tif",
                "YOUR_DIRECTORY/image4.bmp"
        );

        // Step 3: Create a fixed‑size thread pool matching the CPU cores
        int coreCount = Runtime.getRuntime().availableProcessors();
        ExecutorService executor = Executors.newFixedThreadPool(coreCount);

        // Step 4: Submit an OCR task for each image
        List<Future<String>> ocrResults = new ArrayList<>();
        for (String path : imagePaths) {
            ocrResults.add(executor.submit(() -> {
                OcrEngine engine = new OcrEngine();          // fresh engine per task
                engine.setImage(ImageStream.fromFile(path));
                engine.getLanguage().setEnglish(true);
                return engine.recognize() ? engine.getText()
                                           : "Failed: " + path;
            }));
        }

        // Step 5: Retrieve and display the recognized text
        for (Future<String> result : ocrResults) {
            System.out.println("OCR result:\n" + result.get());
        }

        // Step 6: Clean up the executor service
        executor.shutdown();
    }
}
```

**Expected result:** το κείμενο κάθε εικόνας εκτυπώνεται στην κονσόλα, με την ίδια σειρά όπως η λίστα `imagePaths`. Αν κάποια εικόνα δεν μπορεί να επεξεργαστεί, θα δείτε μια ειδοποίηση αποτυχίας αντί για κενή γραμμή.

---

## Common Questions & Edge Cases

### What if I have more images than threads?

Η σταθερή πισίνα νημάτων θα βάλει αυτόματα σε ουρά τις επιπλέον εργασίες. Μόλις ένα νήμα ολοκληρώσει την τρέχουσα εργασία OCR, θα πάρει την επόμενη. Αυτή η συμπεριφορά ουράς αποτελεί την ουσία του **parallel OCR processing**—παίρνετε μέγιστη απόδοση χωρίς να υπερφορτώνετε την CPU.

### Can I change the language?

Απόλυτα. Αντικαταστήστε το `engine.getLanguage().setEnglish(true);` με το κατάλληλο flag γλώσσας, π.χ. `setFrench(true)` ή ενεργοποιήστε πολλαπλές γλώσσες καλώντας αρκετούς setters πριν το `recognize()`.

### How do I handle very large images?

Τα μεγάλα αρχεία μπορούν να καταναλώσουν πολύ μνήμη ανά νήμα. Αν παρατηρήσετε `OutOfMemoryError`, σκεφτείτε να μειώσετε την ανάλυση της εικόνας πριν τη δώσετε στη μηχανή, ή αυξήστε το μέγεθος του heap με `-Xmx`. Μια άλλη προσέγγιση είναι η χρήση μιας **cached thread pool** (`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}