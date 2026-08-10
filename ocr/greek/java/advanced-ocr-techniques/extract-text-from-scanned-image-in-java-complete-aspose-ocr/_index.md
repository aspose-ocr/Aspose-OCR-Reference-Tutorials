---
category: general
date: 2026-06-06
description: Εξαγωγή κειμένου από σαρωμένη εικόνα χρησιμοποιώντας το Aspose OCR για
  Java. Μάθετε πώς να αναγνωρίζετε κείμενο από αρχεία TIFF με παράλληλη επεξεργασία.
draft: false
keywords:
- extract text from scanned image
- recognize text from tiff
- Aspose OCR Java tutorial
- parallel OCR processing
- Java image recognition
language: el
og_description: Εξαγωγή κειμένου από σαρωμένη εικόνα με το Aspose OCR. Αυτός ο οδηγός
  δείχνει πώς να αναγνωρίζετε κείμενο από αρχεία TIFF αποδοτικά χρησιμοποιώντας τη
  Java.
og_title: Εξαγωγή κειμένου από σαρωμένη εικόνα – Οδηγός Aspose OCR Java
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from scanned image using Aspose OCR for Java. Learn how
    to recognize text from tiff files with parallel processing.
  headline: Extract Text from Scanned Image in Java – Complete Aspose OCR Guide
  type: TechArticle
- description: Extract text from scanned image using Aspose OCR for Java. Learn how
    to recognize text from tiff files with parallel processing.
  name: Extract Text from Scanned Image in Java – Complete Aspose OCR Guide
  steps:
  - name: Maven users
    text: 'Add the following dependency to your `pom.xml`:'
  - name: Manual JAR setup
    text: Download the latest `aspose-ocr-xx.jar` from the Aspose website and place
      it on your classpath.
  - name: Expected Output
    text: '``` === Extracted Text === Invoice Number: 12345 Date: 2024‑05‑01 Total:
      $1,250.00 ... ```'
  - name: What’s Next?
    text: '- **Batch processing**: Loop over a directory of TIFFs, store each result
      in its own file. - **Integrate with Elasticsearch**: Index the extracted text
      for fast full‑text search. - **Add language detection**: Use `OcrLanguage.AutoDetect`
      for multi‑lingual documents.'
  type: HowTo
- questions:
  - answer: Absolutely. `OcrInputImage` accepts any format that Java’s ImageIO can
      read. Just replace the file extension in the path.
    question: Does this work with PNG or JPEG files?
  - answer: You could, but remember other services may need CPU cycles. A good rule
      of thumb is “total cores – 1” for dedicated OCR workers.
    question: My server has 8 cores—should I set `setMaxThreads(8)`?
  - answer: 'Check that the image isn’t completely white, that you set the correct
      language, and that the resolution is at least 200 DPI. Low‑quality scans often
      need pre‑processing (deskew, contrast boost) before feeding them to Aspose OCR.
      --- ## Wrap‑Up We’ve just **extracted text from scanned image** files u'
    question: What if the OCR result is empty?
  type: FAQPage
tags:
- Java
- OCR
- Aspose
- Image Processing
title: Εξαγωγή κειμένου από σαρωμένη εικόνα σε Java – Πλήρης οδηγός Aspose OCR
url: /el/java/advanced-ocr-techniques/extract-text-from-scanned-image-in-java-complete-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Σαρωμένη Εικόνα – Πλήρης Οδηγός Aspose OCR

Έχετε χρειαστεί ποτέ να **εξάγετε κείμενο από σαρωμένη εικόνα** αλλά να μην ξέρετε πώς; Δεν είστε μόνοι. Είτε ψηφιοποιείτε παλιά αρχεία, είτε εξάγετε δεδομένα από τιμολόγια, είτε δημιουργείτε μια βιβλιοθήκη PDF με δυνατότητα αναζήτησης, η αξιόπιστη εξαγωγή κειμένου από ένα αρχείο TIFF μπορεί να είναι πρόκληση.  

Καλά νέα: με το Aspose OCR for Java μπορείτε να **αναγνωρίσετε κείμενο από tiff** αρχεία σε λίγες μόνο γραμμές κώδικα, και ακόμη να αυξήσετε την ταχύτητα περιορίζοντας τη μηχανή σε μερικούς πυρήνες CPU. Σε αυτό το tutorial θα περάσουμε από τη ρύθμιση της βιβλιοθήκης μέχρι τη διαχείριση του αποτελέσματος—ώστε να μπορείτε να αντιγράψετε‑επικολλήσετε ένα λειτουργικό παράδειγμα αμέσως.

## Τι Καλύπτει Αυτό το Tutorial

- Εγκατάσταση Aspose OCR for Java (Maven ή χειροκίνητο JAR)
- Φόρτωση μεγάλης σαρωμένης εικόνας TIFF
- Ρύθμιση της μηχανής για χρήση έως 4 νημάτων (παράλληλο OCR)
- Εκτέλεση της διαδικασίας OCR και εκτύπωση του εξαγόμενου κειμένου
- Συνηθισμένα προβλήματα (μνήμη, πολυ‑σελίδες TIFF) και πώς να τα αποφύγετε
- Γρήγορη συμβουλή απόδοσης: πότε να ρυθμίσετε το `setMaxThreads`

Στο τέλος θα μπορείτε να **εξάγετε κείμενο από σαρωμένη εικόνα** με αξιοπιστία, και θα καταλάβετε γιατί η ρύθμιση του αριθμού νημάτων είναι σημαντική όταν *αναγνωρίζετε κείμενο από tiff* σε παραγωγικό περιβάλλον.

---

![εξαγωγή κειμένου από σαρωμένη εικόνα παράδειγμα](example.png "Στιγμιότυπο που δείχνει το εξαγόμενο κείμενο από μια σαρωμένη εικόνα TIFF")

## Προαπαιτούμενα

Πριν προχωρήσουμε, βεβαιωθείτε ότι έχετε:

1. **Java Development Kit (JDK) 8+** – οποιαδήποτε πρόσφατη έκδοση λειτουργεί.
2. **Maven** (ή τη δυνατότητα προσθήκης JAR χειροκίνητα) – θα χρησιμοποιήσουμε Maven για απλότητα.
3. Άδεια **Aspose OCR for Java** (η δωρεάν δοκιμή λειτουργεί, αλλά προσθέτει υδατογράφημα).  
4. Μια **μεγάλη σάρωση TIFF** (π.χ. `large_scan.tif`) που θέλετε να επεξεργαστείτε.

Αν κάτι από αυτά σας είναι άγνωστο, μην ανησυχείτε—κάθε βήμα εξηγείται παρακάτω.

## Βήμα 1: Προσθήκη Aspose OCR στο Project σας

### Maven χρήστες

Προσθέστε την ακόλουθη εξάρτηση στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check the latest version on Maven Central -->
</dependency>
```

### Χειροκίνητη ρύθμιση JAR

Κατεβάστε το πιο πρόσφατο `aspose-ocr-xx.jar` από την ιστοσελίδα της Aspose και τοποθετήστε το στο classpath σας.  

> **Pro tip:** Κρατήστε το JAR σε φάκελο `libs/` και αναφερθείτε σε αυτό στις ρυθμίσεις του IDE. Αυτό αποτρέπει εκπλήξεις τύπου “class not found” αργότερα.

## Βήμα 2: Δημιουργία Απλής Java Κλάσης

Δημιουργήστε ένα αρχείο με όνομα `ParallelOcrDemo.java` στον φάκελο πηγαίου κώδικα (`src/main/java`). Αυτή η κλάση θα περιέχει ολόκληρη τη ροή εργασίας OCR.

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Load the scanned TIFF image you want to process
        // Replace the path with the actual location of your image
        ocrEngine.setImage(new OcrInputImage("YOUR_DIRECTORY/large_scan.tif"));

        // Step 2.3: Limit the engine to use up to 4 CPU cores.
        // This is useful on servers where you don't want to hog all cores.
        ocrEngine.getSettings().setMaxThreads(4);

        // Step 2.4: Run the OCR operation
        OcrResult ocrResult = ocrEngine.process();

        // Step 2.5: Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

> **Γιατί περιορίζουμε τα νήματα:** Από προεπιλογή το Aspose OCR προσπαθεί να χρησιμοποιήσει όλους τους πυρήνες, κάτι που μπορεί να «πνίξει» άλλες υπηρεσίες σε κοινόχρηστη μηχανή. Ορίζοντας `setMaxThreads(4)` λέμε στη μηχανή να τρέχει έως τέσσερις παράλληλους εργαζόμενους—αρκετό για αισθητή βελτίωση ταχύτητας στα περισσότερα σύγχρονα CPUs χωρίς να καταλαμβάνει όλους τους πόρους.

## Βήμα 3: Συγκομιδή και Εκτέλεση

Ανοίξτε ένα τερματικό στο ριζικό φάκελο του project και εκτελέστε:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.ocr.ParallelOcrDemo"
```

Αν δεν χρησιμοποιείτε Maven, συνθέστε με `javac` και τρέξτε:

```bash
javac -cp "libs/*" src/main/java/com/example/ocr/ParallelOcrDemo.java
java -cp "libs/*:src/main/java" com.example.ocr.ParallelOcrDemo
```

### Αναμενόμενη Εξαγωγή

```
=== Extracted Text ===
Invoice Number: 12345
Date: 2024‑05‑01
Total: $1,250.00
...
```

Η κονσόλα θα εμφανίσει την απλή κειμενική έκδοση ό,τι υπήρχε στη σαρωμένη σελίδα. Αν η εικόνα περιέχει πολλαπλές σελίδες, το Aspose OCR τις συνενώνει με τη σωστή σειρά.

## Βήμα 4: Διαχείριση Πολυ‑Σελίδων TIFF (Edge Case)

Ένα κοινό σενάριο είναι ένα **πολυ‑σελίδες TIFF**—σκεφτείτε ένα σαρωμένο βιβλίο. Από προεπιλογή το `OcrInputImage` διαβάζει μόνο το πρώτο πλαίσιο. Για να επεξεργαστείτε όλες τις σελίδες, χρησιμοποιήστε το `OcrInputImage` με `FileInputStream` και ενεργοποιήστε την υποστήριξη πολυ‑σελίδων:

```java
import java.io.FileInputStream;
import com.aspose.ocr.*;

FileInputStream fis = new FileInputStream("YOUR_DIRECTORY/multi_page.tif");
ocrEngine.setImage(new OcrInputImage(fis, true)); // 'true' enables multi‑page
```

Τώρα το `ocrEngine.process()` θα επιστρέψει ένα μοναδικό `OcrResult` που περιέχει το συνενωμένο κείμενο από κάθε σελίδα.

## Βήμα 5: Λεπτομερής Ρύθμιση Ακρίβειας Αναγνώρισης

Αν παρατηρήσετε **ακατάλληλους χαρακτήρες** ή λείπουν λέξεις, δοκιμάστε τις παρακάτω προσαρμογές:

| Ρύθμιση | Τι κάνει | Πότε να τη χρησιμοποιήσετε |
|---------|----------|----------------------------|
| `ocrEngine.getSettings().setLanguage(OcrLanguage.English)` | Εξαναγκάζει το μοντέλο αγγλικής γλώσσας (γρηγορότερο, πιο ακριβές για αγγλικά scans) | Το έγγραφό σας είναι μονογλωσσικό αγγλικό |
| `ocrEngine.getSettings().setResolution(300)` | Αυξάνει την ανάλυση εικόνων χαμηλής ανάλυσης πριν την αναγνώριση | Σαρώσεις κάτω από 200 DPI |
| `ocrEngine.getSettings().setNoiseRemoval(true)` | Προσπαθεί να καθαρίσει ψιλά στίγματα και ελαττώματα | Σαρώσεις με πολύ θόρυβο |

Παράδειγμα κώδικα:

```java
ocrEngine.getSettings().setLanguage(OcrLanguage.English);
ocrEngine.getSettings().setResolution(300);
ocrEngine.getSettings().setNoiseRemoval(true);
```

## Βήμα 6: Εξαγωγή Αποτελεσμάτων σε Αρχείο

Η εκτύπωση στην κονσόλα είναι εντάξει για demo, αλλά σε παραγωγικό κώδικα συνήθως γράφουμε το αποτέλεσμα κάπου χρήσιμο:

```java
import java.io.FileWriter;
import java.io.IOException;

// After processing
String extractedText = ocrResult.getText();
try (FileWriter writer = new FileWriter("output.txt")) {
    writer.write(extractedText);
}
System.out.println("Text saved to output.txt");
```

Τώρα έχετε ένα αρχείο κειμένου που μπορείτε να τροφοδοτήσετε σε ευρετήριο αναζήτησης, βάση δεδομένων ή σε downstream pipeline ανάλυσης.

---

## Συχνές Ερωτήσεις (FAQ)

**Ε: Λειτουργεί αυτό με αρχεία PNG ή JPEG;**  
Α: Απόλυτα. Το `OcrInputImage` δέχεται οποιαδήποτε μορφή που μπορεί να διαβάσει το Java ImageIO. Απλώς αλλάξτε την επέκταση του αρχείου στη διαδρομή.

**Ε: Ο διακομιστής μου έχει 8 πυρήνες—να θέσω `setMaxThreads(8)`;**  
Α: Θα μπορούσατε, αλλά θυμηθείτε ότι άλλες υπηρεσίες μπορεί να χρειάζονται CPU cycles. Ένας καλός κανόνας είναι “συνολικοί πυρήνες – 1” για αφιερωμένους OCR εργαζόμενους.

**Ε: Τι γίνεται αν το αποτέλεσμα OCR είναι κενό;**  
Α: Ελέγξτε ότι η εικόνα δεν είναι εντελώς λευκή, ότι έχετε ορίσει τη σωστή γλώσσα και ότι η ανάλυση είναι τουλάχιστον 200 DPI. Σαρώσεις χαμηλής ποιότητας συχνά απαιτούν προεπεξεργασία (ευθυγράμμιση, ενίσχυση αντίθεσης) πριν τα δώσετε στο Aspose OCR.

---

## Συμπέρασμα

Μόλις **εξάγαμε κείμενο από σαρωμένη εικόνα** χρησιμοποιώντας το Aspose OCR for Java, και τώρα ξέρετε πώς να **αναγνωρίζετε κείμενο από tiff** αποδοτικά με παράλληλη επεξεργασία. Ο πλήρης κώδικας βρίσκεται στα αποσπάσματα παραπάνω, και μπορείτε να τον αντιγράψετε‑επικολλήσετε στο δικό σας project αμέσως.

### Τι Ακολουθεί;

- **Batch processing**: Επανάληψη πάνω σε έναν φάκελο TIFF, αποθήκευση κάθε αποτελέσματος σε ξεχωριστό αρχείο.  
- **Ενσωμάτωση με Elasticsearch**: Ευρετηρίαση του εξαγόμενου κειμένου για γρήγορη πλήρη αναζήτηση κειμένου.  
- **Προσθήκη ανίχνευσης γλώσσας**: Χρήση του `OcrLanguage.AutoDetect` για πολυ‑γλωσσικά έγγραφα.  

Δοκιμάστε αυτές τις ιδέες, και θα μετατρέψετε γρήγορα ένα βουνό σαρωμένων εγγράφων σε αναζητήσιμα, επεξεργάσιμα δεδομένα.

Καλή προγραμματιστική, και μη διστάσετε να αφήσετε σχόλιο αν αντιμετωπίσετε κάποιο πρόβλημα!

## Τι Πρέπει να Μάθετε Στη Σύντομη Επόμενη

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας projects.

- [How to recognize tiff with Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}