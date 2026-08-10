---
category: general
date: 2026-05-06
description: Αναγνωρίστε κείμενο από εικόνα γρήγορα χρησιμοποιώντας ένα παράδειγμα
  OCR σε Java. Μάθετε να εξάγετε κείμενο από αρχεία TIFF με παράλληλη επεξεργασία
  OCR και πώς να κάνετε OCR σε Java αποδοτικά.
draft: false
keywords:
- recognize text from image
- java ocr example
- extract text from tiff
- parallel ocr processing
- how to ocr java
language: el
og_description: Αναγνωρίστε κείμενο από εικόνα γρήγορα με ένα πλήρες παράδειγμα Java
  OCR. Αυτό το σεμινάριο δείχνει πώς να εξάγετε κείμενο από tiff χρησιμοποιώντας παράλληλη
  επεξεργασία OCR.
og_title: Αναγνώριση κειμένου από εικόνα με Java OCR – Οδηγός Παράλληλης Επεξεργασίας
tags:
- OCR
- Java
- Image Processing
title: Αναγνώριση κειμένου από εικόνα με Java OCR – Οδηγός Παράλληλης Επεξεργασίας
url: /el/java/advanced-ocr-techniques/recognize-text-from-image-with-java-ocr-parallel-processing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση κειμένου από εικόνα με Java OCR – Οδηγός Παράλληλης Επεξεργασίας

Έχετε ποτέ χρειαστεί να **αναγνωρίσετε κείμενο από εικόνα** αλλά να έχετε κολλήσει στο εμπόδιο της απόδοσης; Δεν είστε μόνοι. Πολλοί προγραμματιστές χτυπούν το τοίχο όταν μια μονονηματική μηχανή OCR διασχίζει πολύπλευρα TIFF, μετατρέποντας μια γρήγορη εργασία σε μαραθώνιο.  

Σε αυτό το tutorial θα περάσουμε από ένα **java ocr example** που όχι μόνο εξάγει κείμενο από αρχεία tiff, αλλά αξιοποιεί και όλους τους πυρήνες του CPU σας για παράλληλη επεξεργασία OCR. Στο τέλος θα ξέρετε ακριβώς *πώς να κάνετε ocr java* έργα αποδοτικά, και θα έχετε ένα έτοιμο‑για‑εκτέλεση απόσπασμα κώδικα που μπορείτε να ενσωματώσετε σε οποιαδήποτε ρύθμιση Maven ή Gradle.

## Τι Θα Μάθετε

- Πώς να ρυθμίσετε τη βιβλιοθήκη Aspose.OCR σε ένα έργο Java.  
- Πώς να φορτώσετε ένα πολυ‑σελίδων TIFF και να το προετοιμάσετε για αναγνώριση.  
- Πώς να ενεργοποιήσετε **παράλληλη επεξεργασία OCR** ταιριάζοντας τον αριθμό νημάτων με τους λογικούς πυρήνες του CPU σας.  
- Πώς να ανακτήσετε και να εμφανίσετε το αναγνωρισμένο κείμενο, ολοκληρώνοντας τη ροή **αναγνώριση κειμένου από εικόνα**.  

> **Prerequisite:** Java 8 ή νεότερη και έγκυρη άδεια Aspose.OCR for Java (ή προσωρινό κλειδί αξιολόγησης). Δεν απαιτούνται άλλα εξωτερικά εργαλεία.

---

## Βήμα 1: Προσθήκη Εξάρτησης Aspose.OCR

Πριν μπορέσουμε να **αναγνωρίσουμε κείμενο από εικόνα**, χρειάζεται η μηχανή OCR στην κλάση‑διαδρομή. Αν χρησιμοποιείτε Maven, προσθέστε το παρακάτω στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check for the latest version -->
</dependency>
```

Για Gradle, το ισοδύναμο είναι:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

> *Pro tip:* Κρατήστε τον αριθμό έκδοσης ενημερωμένο· οι νεότερες εκδόσεις συχνά περιλαμβάνουν βελτιώσεις απόδοσης που κάνουν την **παράλληλη επεξεργασία ocr** ακόμη πιο γρήγορη.

---

## Βήμα 2: Προετοιμασία της Κλάσης Java – Πλήρες Παράδειγμα Εργασίας

Παρακάτω υπάρχει ένα αυτόνομο **java ocr example** που δείχνει πώς να **εξάγετε κείμενο από tiff** χρησιμοποιώντας όλους τους διαθέσιμους πυρήνες CPU. Αποθηκεύστε το ως `ParallelOcrDemo.java`.

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create an OCR engine instance – this is the heart of the recognize text from image process
        OcrEngine engine = new OcrEngine();

        // 2️⃣ Load the multi‑page TIFF you want to process.
        //    Replace the path with your actual file location.
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/document-multi-page.tif"));

        // 3️⃣ Enable parallel processing.
        //    We ask the JVM for the number of logical processors and feed that to the engine.
        engine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // 4️⃣ Perform the recognition. This call blocks until every page is processed.
        OcrResult result = engine.recognize();

        // 5️⃣ Output the recognized text – the final step in our recognize text from image pipeline.
        System.out.println("=== Recognized Text ===");
        System.out.println(result.getText());
    }
}
```

**Γιατί κάθε γραμμή είναι σημαντική**

- **Δημιουργία μηχανής**: Το `OcrEngine` ενσωματώνει όλη τη βαριά δουλειά. Χωρίς αυτό, δεν μπορείτε καθόλου να **αναγνωρίσετε κείμενο από εικόνα**.  
- **Φόρτωση εικόνας**: Το `ImageStream.fromFile` υποστηρίζει TIFF, PNG, JPEG κ.λπ. Η χρήση ενός πολυ‑σελίδων TIFF δοκιμάζει την ικανότητα της μηχανής να διαχειρίζεται σύνθετα έγγραφα.  
- **Αριθμός νημάτων**: Η `Runtime.getRuntime().availableProcessors()` επιστρέφει τον αριθμό λογικών πυρήνων (συμπεριλαμβανομένων των hyper‑threads). Ορίζοντας αυτή την τιμή ενεργοποιεί την **παράλληλη επεξεργασία ocr**, μειώνοντας δραστικά το χρόνο εκτέλεσης σε πολυπύρημα μηχανές.  
- **Αναγνώριση**: Η `engine.recognize()` εκτελεί τη διαδικασία OCR. Εσωτερικά, διανέμει τις σελίδες στο pool νημάτων που ορίσατε.  
- **Διαχείριση αποτελέσματος**: Η `result.getText()` επιστρέφει ένα ενιαίο `String` που περιέχει το ενωμένο κείμενο όλων των σελίδων – ιδανικό για επεξεργασία ή αποθήκευση.

---

## Βήμα 3: Εκτέλεση του Demo και Επαλήθευση του Αποτελέσματος

Συμπιέστε και εκτελέστε το πρόγραμμα:

```bash
javac -cp "path/to/aspose-ocr-23.12.jar" ParallelOcrDemo.java
java -cp ".:path/to/aspose-ocr-23.12.jar" ParallelOcrDemo
```

Θα πρέπει να δείτε κάτι σαν:

```
=== Recognized Text ===
Page 1: Invoice #12345
Date: 2024‑11‑01
Total: $1,250.00
...
Page 2: Terms and Conditions
...
```

Αν η κονσόλα εκτυπώσει το αναμενόμενο κείμενο, συγχαρητήρια—έχετε επιτυχώς **αναγνωρίσει κείμενο από εικόνα** χρησιμοποιώντας ένα **java ocr example** που τρέχει παράλληλα.

---

## Βήμα 4: Προσαρμογές για Πραγματικά Σενάρια (Προαιρετικό)

### Εξαγωγή Κειμένου μόνο από Συγκεκριμένες Σελίδες

Μερικές φορές χρειάζεστε μόνο ορισμένες σελίδες από ένα μεγάλο TIFF. Μπορείτε να φιλτράρετε μετά την αναγνώριση:

```java
String[] pages = result.getPageResults();
for (int i = 0; i < pages.length; i++) {
    if (i == 0 || i == 2) { // keep page 1 and 3 (0‑based index)
        System.out.println("Page " + (i + 1) + ":");
        System.out.println(pages[i]);
    }
}
```

### Χειροκίνητη Ρύθμιση Αριθμού Νημάτων

Αν ο διακομιστής σας είναι ήδη απασχολημένος με άλλες εργασίες, μπορείτε να περιορίσετε τα νήματα OCR:

```java
engine.setThreadCount(2); // use only two cores regardless of total count
```

### Διαχείριση Μνήμης‑Απαιτητικών TIFF

Τα μεγάλα πολυ‑σελίδων TIFF μπορούν να καταναλώσουν πολύ RAM. Για να το μετριάσετε, επεξεργαστείτε το αρχείο σε τμήματα:

```java
engine.setImage(ImageStream.fromFile("bigfile.tif"));
engine.setPageRange(1, 5); // process pages 1‑5 first
OcrResult part1 = engine.recognize();
// later, change the range and call recognize again for pages 6‑10, etc.
```

---

## Βήμα 5: Συνηθισμένα Πιθανά Προβλήματα & Πώς να τα Αποφύγετε

| Issue | Symptom | Fix |
|-------|---------|-----|
| **Insufficient license** | Runtime throws `LicenseException` | Apply a valid license file or use the free evaluation mode (adds a watermark). |
| **Wrong file path** | `FileNotFoundException` | Double‑check the path and use absolute paths during testing. |
| **CPU throttling** | No speed gain despite `setThreadCount` | Ensure your JVM isn’t limited by `-Xmx` memory caps or OS power‑saving settings. |
| **Unsupported image format** | `UnsupportedFormatException` | Convert the image to TIFF, PNG, or JPEG before feeding it to the engine. |

---

## Οπτική Σύνοψη

![recognize text from image example](image-placeholder.png "αναγνώριση κειμένου από εικόνα")

*Alt text:* “Διάγραμμα που δείχνει τη ροή της αναγνώρισης κειμένου από εικόνα χρησιμοποιώντας Java OCR με παράλληλη επεξεργασία”

---

## Συμπέρασμα

Μόλις περάσαμε από ένα πλήρες **java ocr example** που **αναγνωρίζει κείμενο από εικόνα** αρχεία, ειδικά πολυ‑σελίδων TIFF, αξιοποιώντας πλήρως την **παράλληλη επεξεργασία ocr**. Ταιριάζοντας το pool νημάτων με τους πυρήνες του CPU, λαμβάνετε σχεδόν γραμμική επιτάχυνση σε σύγχρονο υλικό—ακριβώς η απάντηση στο “*πώς να κάνετε ocr java* αποδοτικά;”.  

Στη συνέχεια, μπορείτε να εξερευνήσετε:

- **extract text from tiff** αρχεία σε παρτίδες και αποθήκευση των αποτελεσμάτων σε βάση δεδομένων.  
- Συνδυασμός OCR με βιβλιοθήκες NLP (π.χ., OpenNLP) για αυτόματη σήμανση εξαγόμενων οντοτήτων.  
- Ανάπτυξη της λύσης ως μικροϋπηρεσία πίσω από ένα REST endpoint για OCR κατόπιν ζήτησης.

Δοκιμάστε το, προσαρμόστε τον αριθμό νημάτων, και δείτε πόσο πιο γρήγορη γίνεται η διαδικασία σας. Αν αντιμετωπίσετε δυσκολίες, αφήστε ένα σχόλιο παρακάτω—καλή κωδικοποίηση!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}