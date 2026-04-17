---
category: general
date: 2026-03-07
description: Εξάγετε κείμενο από εικόνα με Java OCR. Μάθετε πώς να φορτώνετε εικόνα
  για OCR, να ρυθμίζετε τη γλώσσα και να εκτελείτε ένα πλήρες σεμινάριο Java OCR σε
  λίγα λεπτά.
draft: false
keywords:
- extract text from image
- load image for ocr
- use OCR in java
- java ocr tutorial
language: el
og_description: Εξάγετε κείμενο από εικόνα χρησιμοποιώντας Java OCR. Αυτό το σεμινάριο
  δείχνει πώς να φορτώσετε μια εικόνα για OCR, να διαμορφώσετε τη γλώσσα και να εκτελέσετε
  ένα Java OCR σεμινάριο βήμα‑βήμα.
og_title: Εξαγωγή κειμένου από εικόνα σε Java – Πλήρης οδηγός OCR
tags:
- OCR
- Java
- Image Processing
title: Εξαγωγή κειμένου από εικόνα σε Java – Οδηγός OCR Java
url: /el/java/ocr-basics/extract-text-from-image-in-java-java-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Εικόνα σε Java – Πλήρης Οδηγός OCR

Έχετε ποτέ χρειαστεί να **εξάγετε κείμενο από εικόνα** αλλά δεν ήξερες από πού να ξεκινήσεις σε Java; Δεν είστε ο μόνος—οι προγραμματιστές συχνά αντιμετωπίζουν αυτό το πρόβλημα όταν μετατρέπουν σαρωμένες πινακίδες, αποδείξεις ή χειρόγραφες σημειώσεις σε αναζητήσιμες συμβολοσειρές.  

Τα καλά νέα; Σε λίγα μόνο λεπτά μπορείτε να έχετε μια λειτουργική γραμμή OCR που διαβάζει Κανάντα, Αγγλικά ή οποιαδήποτε υποστηριζόμενη γλώσσα. Σε αυτό το tutorial θα **φορτώσουμε εικόνα για OCR**, θα διαμορφώσουμε τη μηχανή και θα περάσουμε από ένα **Java OCR tutorial** που μπορείτε να αντιγράψετε‑επικολλήσετε και να τρέξετε σήμερα.

## Τι Καλύπτει Αυτός ο Οδηγός

Θα ξεκινήσουμε με την λίστα των εργαλείων που θα χρειαστείτε, μετά θα βυθιστούμε κατευθείαν σε μια **βήμα‑βήμα** υλοποίηση. Στο τέλος θα μπορείτε να:

* Φορτώσετε ένα αρχείο εικόνας σε ένα Java `ImageInputStream`.
* Διαμορφώσετε μια μηχανή OCR για να αναγνωρίζει μια συγκεκριμένη γλώσσα (Kannada στο παράδειγμά μας).
* Εκτελέσετε τη διαδικασία αναγνώρισης και εκτυπώσετε το εξαγόμενο κείμενο.
* Ρυθμίσετε τις ρυθμίσεις για καλύτερη ακρίβεια και αντιμετωπίσετε κοινά προβλήματα.

Δεν απαιτείται εξωτερική τεκμηρίωση—όλα όσα χρειάζεστε είναι εδώ.  

**Prerequisites**: Java 17 ή νεότερη, ένα εργαλείο κατασκευής όπως Maven ή Gradle, και μια βιβλιοθήκη OCR που προσφέρει μια κλάση `OcrEngine` (για παράδειγμα, το υποθετικό *SimpleOCR* SDK). Αν χρησιμοποιείτε Maven, προσθέστε την εξάρτηση που φαίνεται παρακάτω.

---

## Βήμα 1 – Ρυθμίστε το Έργο σας και Προσθέστε τη Βιβλιοθήκη OCR

Πριν γράψουμε κώδικα, βεβαιωθείτε ότι το έργο σας μπορεί να δει τις κλάσεις OCR. Με Maven, προσθέστε αυτό το απόσπασμα στο `pom.xml` σας:

```xml
<!-- Maven dependency for SimpleOCR (replace with your actual OCR SDK) -->
<dependency>
    <groupId>com.example</groupId>
    <artifactId>simple-ocr</artifactId>
    <version>1.4.2</version>
</dependency>
```

Αν προτιμάτε Gradle, το ισοδύναμο είναι:

```gradle
implementation 'com.example:simple-ocr:1.4.2'
```

> **Pro tip:** Κρατήστε την έκδοση της βιβλιοθήκης ενημερωμένη· οι νεότερες εκδόσεις συχνά περιλαμβάνουν βελτιώσεις στα μοντέλα γλώσσας που αυξάνουν την ακρίβεια.

Μόλις η εξάρτηση λυθεί, ανανεώστε το IDE σας και είστε έτοιμοι να κωδικοποιήσετε.

## Βήμα 2 – Εισάγετε τις Απαιτούμενες Κλάσεις

Παρακάτω είναι η πλήρης λίστα των imports που θα χρειαστείτε για το παράδειγμα. Είναι σκόπιμα ελαχιστοποιημένα ώστε να βλέπετε ακριβώς τι κάνει κάθε κλάση.

```java
import com.example.ocr.OcrEngine;      // Main OCR engine
import com.example.ocr.OcrResult;      // Holds recognition result
import com.example.io.ImageInputStream; // Wrapper for image files
import java.nio.file.Paths;             // Convenient path handling
import java.io.IOException;             // For proper exception handling
```

> **Why these imports?** `OcrEngine` και `OcrResult` είναι η καρδιά της διαδικασίας OCR, ενώ `ImageInputStream` αφαιρεί το boilerplate ανάγνωσης αρχείων. Η χρήση του `java.nio.file.Paths` κάνει τον κώδικα ανεξάρτητο από το λειτουργικό σύστημα.

## Βήμα 3 – Φορτώστε Εικόνα για OCR

Τώρα έρχεται το μέρος που συχνά προκαλεί προβλήματα: η παροχή του σωστού μορφότυπου εικόνας στη μηχανή. Το OCR SDK αναμένει ένα `ImageInputStream`, το οποίο μπορείτε να αποκτήσετε από οποιοδήποτε αρχείο στο δίσκο.

```java
// Step 3: Load the image that contains the text you want to extract
String imagePath = "YOUR_DIRECTORY/kannada_sign.jpg";
ImageInputStream imageStream = new ImageInputStream(Paths.get(imagePath));
```

> **Edge case:** Αν η εικόνα είναι κατεστραμμένη ή σε μη υποστηριζόμενο μορφότυπο (π.χ., GIF), ο κατασκευαστής θα ρίξει ένα `IOException`. Τυλίξτε την κλήση σε μπλοκ try‑catch ή επικυρώστε το αρχείο εκ των προτέρων.

## Βήμα 4 – Διαμορφώστε τη Μηχανή για Αναγνώριση Συγκεκριμένης Γλώσσας

Οι περισσότερες μηχανές OCR παρέχουν πολυγλωσσική υποστήριξη. Για να βελτιώσετε την ακρίβεια, πρέπει να πείτε στη μηχανή ακριβώς ποια γλώσσα να ψάξει. Στην περίπτωσή μας χρησιμοποιούμε τον κωδικό γλώσσας `"kn"` για Kannada.

```java
// Step 4: Create and configure the OCR engine for Kannada
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getConfig().setLanguage("kn"); // 'kn' = Kannada
```

> **Why set the language?** Ο περιορισμός του συνόλου χαρακτήρων μειώνει τα ψευδώς θετικά, ειδικά όταν δουλεύετε με γραφές που έχουν πολλά παρόμοια γλυφά.

Αν χρειαστεί ποτέ να αλλάξετε γλώσσες, απλώς αλλάξτε το string του κώδικα—δεν απαιτούνται άλλες αλλαγές.

## Βήμα 5 – Εκτελέστε τη Διαδικασία OCR και Εξάγετε το Κείμενο

Με την εικόνα φορτωμένη και τη μηχανή διαμορφωμένη, η πραγματική αναγνώριση είναι μια κλήση μεθόδου. Το αντικείμενο αποτελέσματος σας δίνει το απλό κείμενο και, προαιρετικά, τις βαθμολογίες εμπιστοσύνης.

```java
// Step 5: Run OCR and retrieve the recognized text
OcrResult ocrResult = ocrEngine.recognize(imageStream);
String extractedText = ocrResult.getText();
```

> **Common question:** *Τι γίνεται αν το OCR επιστρέψει κενή συμβολοσειρά;*  
> Συνήθως σημαίνει ότι η ποιότητα της εικόνας είναι πολύ χαμηλή (θολή, χαμηλή αντίθεση) ή ότι η γλώσσα δεν ορίστηκε σωστά. Δοκιμάστε προεπεξεργασία της εικόνας (αύξηση αντίθεσης, δυαδικοποίηση) ή ελέγξτε ξανά τον κωδικό γλώσσας.

## Βήμα 6 – Εμφανίστε το Αποτέλεσμα

Τέλος, εκτυπώστε το αποτέλεσμα στην κονσόλα. Σε μια πραγματική εφαρμογή μπορεί να το αποθηκεύσετε σε βάση δεδομένων ή να το τροφοδοτήσετε σε ευρετήριο αναζήτησης.

```java
// Step 6: Output the recognized Kannada text
System.out.println("Extracted text:");
System.out.println(extractedText);
```

### Αναμενόμενο Αποτέλεσμα

Αν η πηγή εικόνας περιέχει τη φράση Kannada “ಕರ್ನಾಟಕ” (Karnataka), η κονσόλα θα πρέπει να εμφανίσει:

```
Extracted text:
ಕರ್ನಾಟಕ
```

Αυτό είναι—μια πλήρης ροή εργασίας **use OCR in Java** που μπορείτε να προσαρμόσετε σε οποιαδήποτε γλώσσα ή πηγή εικόνας.

---

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω είναι ολόκληρο το πρόγραμμα, έτοιμο για μεταγλώττιση. Αντικαταστήστε το `YOUR_DIRECTORY` με την πραγματική διαδρομή του αρχείου εικόνας.

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrResult;
import com.example.io.ImageInputStream;
import java.nio.file.Paths;
import java.io.IOException;

public class KannadaOcrExample {
    public static void main(String[] args) {
        try {
            // Create OCR engine instance
            OcrEngine ocrEngine = new OcrEngine();

            // Configure for Kannada (language code "kn")
            ocrEngine.getConfig().setLanguage("kn");

            // Load the image you want to extract text from
            String imagePath = "YOUR_DIRECTORY/kannada_sign.jpg";
            ImageInputStream imageStream = new ImageInputStream(Paths.get(imagePath));

            // Run the OCR process
            OcrResult ocrResult = ocrEngine.recognize(imageStream);

            // Print the extracted text
            System.out.println("Extracted text:");
            System.out.println(ocrResult.getText());
        } catch (IOException e) {
            System.err.println("Failed to load image or run OCR: " + e.getMessage());
        } catch (Exception e) {
            System.err.println("Unexpected error during OCR: " + e.getMessage());
        }
    }
}
```

> **Tip:** Για κώδικα παραγωγής, σκεφτείτε την επαναχρησιμοποίηση μιας μόνο στιγμής `OcrEngine` για πολλαπλές εικόνες· η δημιουργία της επανειλημμένα μπορεί να είναι δαπανηρή.

---

## Συχνές Ερωτήσεις & Edge Cases

### Πώς βελτιώνω την ακρίβεια σε θορυβώδεις φωτογραφίες;

- **Pre‑process** την εικόνα: μετατρέψτε σε κλίμακα του γκρι, εφαρμόστε φιλτράρισμα μεσαίας τιμής ή αυξήστε την αντίθεση.
- **Resize** την εικόνα τουλάχιστον σε 300 DPI· οι περισσότερες μηχανές OCR αναμένουν αυτήν την ανάλυση.
- **Set a whitelist** χαρακτήρων αν γνωρίζετε το αναμενόμενο αποτέλεσμα (π.χ., μόνο ψηφία).

### Μπορώ να χρησιμοποιήσω αυτήν την προσέγγιση για PDFs;

Ναι. Εξάγετε κάθε σελίδα ως εικόνα (χρησιμοποιώντας PDFBox ή iText), μετά τροφοδοτήστε αυτές τις εικόνες στην ίδια γραμμή εργασίας. Ο κώδικας παραμένει ίδιος· μόνο η πηγή εικόνας αλλάζει.

### Τι γίνεται αν χρειαστεί να αναγνωρίσω πολλαπλές γλώσσες σε μία εικόνα;

Οι περισσότερες SDK επιτρέπουν να περάσετε μια λίστα χωρισμένη με κόμμα, όπως `"en,kn"`. Η μηχανή θα προσπαθήσει να ταιριάξει με οποιοδήποτε από τα παρεχόμενα σενάρια.

### Υπάρχει τρόπος να λάβω βαθμολογίες εμπιστοσύνης;

`OcrResult` συχνά περιλαμβάνει μια μέθοδο `getConfidence()` που επιστρέφει ένα float μεταξύ 0 και 1 για κάθε γραμμή. Χρησιμοποιήστε το για να φιλτράρετε αποτελέσματα χαμηλής εμπιστοσύνης.

---

## Επόμενα Βήματα

Τώρα που μπορείτε να **εξάγετε κείμενο από εικόνα** χρησιμοποιώντας Java, μπορείτε να εξερευνήσετε:

* **Batch processing** – επανάληψη σε φάκελο εικόνων και εγγραφή αποτελεσμάτων σε CSV.
* **Integration with Apache Tika** – συνδυάστε OCR με ανάλυση εγγράφων για ένα ενοποιημένο ευρετήριο αναζήτησης.
* **Server‑side API** – εκθέστε τη λογική OCR μέσω ενός REST endpoint (το Spring Boot το κάνει εύκολο).
* **Alternative libraries** – δοκιμάστε το Tesseract μέσω `tess4j` αν χρειάζεστε μια ανοιχτού κώδικα λύση.

Κάθε ένα από αυτά τα θέματα βασίζεται στις βασικές έννοιες που καλύπτονται σε αυτό το **java ocr tutorial**, οπότε νιώστε ελεύθεροι να πειραματιστείτε και να επεκτείνετε τον κώδικα.

---

## Συμπέρασμα

Διασχίσαμε ένα πλήρες παράδειγμα Java που **εξάγει κείμενο από εικόνα**, δείχνοντας ακριβώς πώς να **φορτώσετε εικόνα για OCR**, να διαμορφώσετε τις ρυθμίσεις γλώσσας και να **χρησιμοποιήσετε OCR σε Java** για να λάβετε αναγνώσιμες συμβολοσειρές. Το απόσπασμα είναι αυτόνομο, διαχειρίζεται σφάλματα με χάρη, και μπορεί να ενσωματωθεί σε οποιοδήποτε έργο Java με ελάχιστη προσπάθεια.  

Δοκιμάστε το, τροποποιήστε τον κωδικό γλώσσας, και σύντομα θα μετατρέπετε σαρωμένα έγγραφα σε αναζητήσιμα δεδομένα χωρίς κόπο. Καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}