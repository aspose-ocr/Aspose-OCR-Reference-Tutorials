---
category: general
date: 2026-06-16
description: Παράδειγμα OCR σε Java που δείχνει πώς να φορτώσετε μια εικόνα για OCR,
  να αναγνωρίσετε κείμενο σε Java και να εξάγετε κείμενο με το Aspose από αρχείο JPG
  σε λίγες μόνο γραμμές.
draft: false
keywords:
- java ocr example
- load image ocr
- recognize text java
- recognize jpg text
- extract text aspose
language: el
og_description: Το παράδειγμα Java OCR επιδεικνύει τη φόρτωση μιας εικόνας, την αναγνώριση
  κειμένου JPG και την εξαγωγή του με τη βιβλιοθήκη Aspose OCR.
og_title: Παράδειγμα OCR σε Java – Φόρτωση εικόνας και αναγνώριση κειμένου
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Java OCR example that shows how to load image OCR, recognize text Java,
    and extract text Aspose from a JPG file in just a few lines.
  headline: Java OCR Example – Load Image and Recognize Text with Aspose
  type: TechArticle
- questions:
  - answer: Absolutely. Just point `ImageStream.fromFile("image.png")` to the desired
      file; Aspose auto‑detects the format.
    question: Can I process PNG or TIFF files the same way?
  - answer: Check the image resolution (≥300 dpi is ideal) and consider enabling binarization.
      Also, verify that the correct language is set.
    question: What if the OCR returns garbled characters?
  - answer: 'Yes. `result.getWords()` returns a collection where each `OcrWord` has
      a `getConfidence()` method. ## Conclusion You now have a solid **java ocr example**
      that demonstrates how to **load image ocr**, **recognize text java**, and **extract
      text aspose** from a JPEG file. The snippet runs out‑of‑the‑b'
    question: Is there a way to get confidence scores for each word?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: Παράδειγμα OCR σε Java – Φόρτωση εικόνας και αναγνώριση κειμένου με το Aspose
url: /el/java/ocr-basics/java-ocr-example-load-image-and-recognize-text-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java OCR Example – Load Image and Recognize Text with Aspose

Έχετε αναρωτηθεί ποτέ πώς να **java ocr example** έναν γρήγορο τρόπο για να εξάγετε κείμενο από μια εικόνα; Δεν είστε οι μόνοι—οι προγραμματιστές χρειάζονται συνεχώς να μετατρέπουν σαρωμένες αποδείξεις, ταυτότητες ή ακόμη και στιγμιότυπα οθόνης σε επεξεργάσιμες συμβολοσειρές. Το καλό νέο; Με το Aspose.OCR για Java μπορείτε να φορτώσετε μια εικόνα, να εκτελέσετε OCR και να λάβετε καθαρό κείμενο σε λίγες μόνο γραμμές.

Σε αυτόν τον οδηγό θα περάσουμε βήμα-βήμα από ένα πλήρες, εκτελέσιμο πρόγραμμα που **load image ocr** από JPEG, **recognize text java**, και σας δείχνει πώς να **extract text aspose** ακόμη και όταν χρησιμοποιείτε την έκδοση αξιολόγησης. Στο τέλος θα έχετε ένα στιβαρό πρότυπο που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο.

## What You’ll Learn

- Πώς να προσθέσετε τη βιβλιοθήκη Aspose.OCR σε έργο Maven ή Gradle.  
- Τον ακριβή κώδικα που απαιτείται για **recognize jpg text** από αρχείο στο δίσκο.  
- Πώς να εντοπίσετε μια έκδοση αξιολόγησης και να διαχειριστείτε την προειδοποίηση υδατογραφήματος.  
- Συμβουλές για την αντιμετώπιση κοινών παγίδων όπως μη υποστηριζόμενες μορφές εικόνας ή χαμηλής ανάλυσης σάρωση.  

Δεν απαιτείται προηγούμενη εμπειρία με το Aspose· αρκεί μια βασική ρύθμιση Java και ένα αρχείο εικόνας για δοκιμή.

## Prerequisites

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|------------------------|
| JDK 17 ή νεότερο (η βιβλιοθήκη υποστηρίζει Java 8+ αλλά τα νεότερα JDK προσφέρουν καλύτερη απόδοση) | Εγγυάται συμβατότητα με τα πιο πρόσφατα δυαδικά του Aspose. |
| Maven 3.x ή Gradle 7+ (ή μπορείτε να προσθέσετε το JAR χειροκίνητα) | Απλοποιεί τη διαχείριση εξαρτήσεων. |
| Μια εικόνα JPEG (`sample.jpg`) που θέλετε να επεξεργαστείτε | Το παράδειγμα χρησιμοποιεί JPG, αλλά λειτουργεί με οποιαδήποτε υποστηριζόμενη μορφή. |
| Άδεια Aspose.OCR for Java (προαιρετική) | Χωρίς άδεια θα εμφανίζεται υδατογράφημα αξιολόγησης· ο κώδικας ελέγχει για αυτό. |

Αν έχετε ήδη ένα έργο, προσθέστε την παρακάτω εξάρτηση και είστε έτοιμοι.

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

```gradle
// Gradle
implementation 'com.aspose:aspose-ocr:23.10'
```

> **Pro tip:** Κρατήστε τον αριθμό έκδοσης ενημερωμένο· το Aspose κυκλοφορεί τριμηνιαίες βελτιώσεις που αυξάνουν την ακρίβεια, ειδικά σε εικόνες χαμηλής αντίθεσης.

## Step 1: Create the OCR Engine Instance

Το πρώτο που χρειάζεστε είναι ένα `OcrEngine`. Σκεφτείτε το ως τον εγκέφαλο που θα αναλύσει τα pixel και θα τα μετατρέψει σε χαρακτήρες.

```java
// Step 1 – Initialize the OCR engine
OcrEngine engine = new OcrEngine();
```

Γιατί ένα ξεχωριστό αντικείμενο μηχανής; Σας επιτρέπει να επαναχρησιμοποιήσετε την ίδια διαμόρφωση για πολλές εικόνες, εξοικονομώντας μνήμη και χρόνο εκκίνησης.

## Step 2: Load the Image for OCR

Τώρα φορτώνουμε πραγματικά **load image ocr** δεδομένα από το δίσκο. Το Aspose παρέχει έναν βολικό wrapper `ImageStream` που αφαιρεί την ανάγκη χειρισμού ακατέργαστου `InputStream`.

```java
// Step 2 – Load the JPEG file you want to process
engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

Αντικαταστήστε το `YOUR_DIRECTORY` με το απόλυτο ή σχετικό μονοπάτι όπου βρίσκεται το `sample.jpg`. Η μέθοδος υποστηρίζει PNG, BMP, TIFF και ακόμη και πολυ‑σελίδες PDF—οπότε δεν περιορίζεστε μόνο στα JPG.

> **Common question:** *Τι γίνεται αν η εικόνα μου είναι σε byte array;*  
> Χρησιμοποιήστε `ImageStream.fromBytes(byteArray)`· η υπόλοιπη ροή παραμένει ίδια.

## Step 3: Recognize Text in Java

Με την εικόνα στη μνήμη, ζητάμε από το Aspose να κάνει το βαριά δουλειά. Η κλήση `recognize()` εκτελεί τον αλγόριθμο OCR και επιστρέφει ένα αντικείμενο `OcrResult`.

```java
// Step 3 – Perform OCR and get the result object
OcrResult result = engine.recognize();
```

Η βιβλιοθήκη ανιχνεύει αυτόματα τη γλώσσα, τον προσανατολισμό και εκτελεί βασική μείωση θορύβου. Αν χρειάζεται να επιβάλετε μια γλώσσα (π.χ., French), μπορείτε να ορίσετε `engine.getLanguage().setLanguage(Language.French);` πριν καλέσετε `recognize()`.

## Step 4: Handle Evaluation Version Warnings

Αν τρέχετε την δωρεάν έκδοση αξιολόγησης, το αποτέλεσμα μπορεί να περιέχει ένα διακριτικό υδατογράφημα. Η σημαία `isEvaluation()` σας επιτρέπει να προειδοποιήσετε τους χρήστες ή να καταγράψετε την κατάσταση.

```java
// Step 4 – Check for evaluation mode
if (result.isEvaluation()) {
    System.out.println("[EVALUATION] Result may contain a watermark.");
}
```

Όταν αργότερα αγοράσετε άδεια και την εφαρμόσετε μέσω `License license = new License(); license.setLicense("Aspose.Total.Java.lic");`, αυτό το τμήμα δεν θα εκτελείται ποτέ.

## Step 5: Extract Text Aspose and Print It

Τέλος, εξάγουμε τη αναγνωρισμένη συμβολοσειρά από το αποτέλεσμα και την εμφανίζουμε. Εδώ συμβαίνει το **extract text aspose**.

```java
// Step 5 – Output the recognized text
System.out.println(result.getText());
```

Η επιστρεφόμενη συμβολοσειρά διατηρεί τις αλλαγές γραμμής, ώστε να λαμβάνετε μια αρκετά πιστή αναπαράσταση της αρχικής διάταξης.

### Expected Output

Υποθέτοντας ότι το `sample.jpg` περιέχει τη φράση “Hello, Aspose OCR!”, θα δείτε κάτι όπως:

```
[EVALUATION] Result may contain a watermark.
Hello, Aspose OCR!
```

Αν η εικόνα είναι θολή ή χαμηλής ανάλυσης, μπορεί να εμφανιστούν επιπλέον κενά ή λανθασμένοι χαρακτήρες—συνηθισμένα quirks του OCR που θα συζητήσουμε παρακάτω.

## Step 6: Tips for Better Accuracy (Optional Enhancements)

| Συμβουλή | Πώς βοηθά |
|----------|-----------|
| **Αύξηση DPI** – Κλιμακώστε την εικόνα στα 300 dpi πριν τη δώσετε στο `engine` | Η υψηλότερη ανάλυση δίνει στη μηχανή περισσότερες λεπτομέρειες. |
| **Προεπεξεργασία με δυαδικοποίηση** – Μετατρέψτε σε ασπρόμαυρο με `engine.getImageProcessingOptions().setBinarization(true);` | Απομακρύνει τον θόρυβο φόντου που μπορεί να μπερδέψει την ανίχνευση χαρακτήρων. |
| **Καθορισμός γλώσσας** – `engine.getLanguage().setLanguage(Language.English);` | Καθοδηγεί τη μηχανή OCR, μειώνοντας ψευδείς θετικές σε παρόμοια σύμβολα. |
| **Επεξεργασία παρτίδας** – Επαναχρησιμοποίηση του ίδιου αντικειμένου `OcrEngine` για πολλά αρχεία | Μειώνει το κόστος δημιουργίας αντικειμένων. |

Αυτές οι βελτιώσεις είναι ιδιαίτερα χρήσιμες όταν **recognize jpg text** από σαρωμένες αποδείξεις ή επαγγελματικές κάρτες που συχνά είναι χαμηλής ποιότητας JPEG.

## Full Working Example

Παρακάτω βρίσκεται η πλήρης, αυτόνομη κλάση Java που μπορείτε να αντιγράψετε‑επικολλήσετε στο IDE σας. Περιλαμβάνει τις προαιρετικές βελτιώσεις που αναφέρθηκαν παραπάνω, αλλά μπορείτε να τις σχολιάσετε αν προτιμάτε ένα ελάχιστο παράδειγμα.

```java
import com.aspose.ocr.*;

public class JavaOcrExample {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // OPTIONAL: Improve accuracy for low‑resolution JPEGs
        // engine.getImageProcessingOptions().setBinarization(true);
        // engine.getLanguage().setLanguage(Language.English);

        // Load the image (replace the path with your own)
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // Perform OCR
        OcrResult result = engine.recognize();

        // Detect evaluation mode
        if (result.isEvaluation()) {
            System.out.println("[EVALUATION] Result may contain a watermark.");
        }

        // Print the extracted text
        System.out.println(result.getText());
    }
}
```

> **Note:** Αν τρέξετε αυτόν τον κώδικα χωρίς άδεια, η έξοδος θα περιλαμβάνει την ειδοποίηση αξιολόγησης. Μόλις προσθέσετε ένα έγκυρο αρχείο άδειας, η ειδοποίηση εξαφανίζεται και λαμβάνετε καθαρό κείμενο.

## Frequently Asked Questions

**Q: Μπορώ να επεξεργαστώ αρχεία PNG ή TIFF με τον ίδιο τρόπο;**  
A: Απόλυτα. Απλώς κατευθύνετε το `ImageStream.fromFile("image.png")` στο επιθυμητό αρχείο· το Aspose ανιχνεύει αυτόματα τη μορφή.

**Q: Τι γίνεται αν το OCR επιστρέψει ακατάλληλους χαρακτήρες;**  
A: Ελέγξτε την ανάλυση της εικόνας (≥300 dpi είναι ιδανική) και σκεφτείτε να ενεργοποιήσετε τη δυαδικοποίηση. Επίσης, βεβαιωθείτε ότι έχει οριστεί η σωστή γλώσσα.

**Q: Υπάρχει τρόπος να λάβω βαθμολογίες εμπιστοσύνης για κάθε λέξη;**  
A: Ναι. `result.getWords()` επιστρέφει μια συλλογή όπου κάθε `OcrWord` έχει τη μέθοδο `getConfidence()`.

## Conclusion

Τώρα έχετε ένα στιβαρό **java ocr example** που δείχνει πώς να **load image ocr**, **recognize text java**, και **extract text aspose** από αρχείο JPEG. Το απόσπασμα λειτουργεί αμέσως, διαχειρίζεται προειδοποιήσεις αξιολόγησης και σας παρέχει σαφή διαδρομή για βελτίωση της ακρίβειας σε πιο δύσκολες εικόνες.

Τι θα κάνετε στη συνέχεια; Δοκιμάστε να τροφοδοτήσετε τη μηχανή με μια παρτίδα τιμολογίων, πειραματιστείτε με διαφορετικές ρυθμίσεις γλώσσας, ή ενσωματώστε την έξοδο σε μια βάση δεδομένων για αναζητήσιμα αρχεία. Η βιβλιοθήκη Aspose OCR είναι αρκετά ευέλικτη για να τροφοδοτήσει από απλές επιτραπέζιες βοηθητικές εφαρμογές έως μεγάλης κλίμακας pipelines επεξεργασίας εγγράφων.

Έχετε περισσότερες ερωτήσεις ή θέλετε να μοιραστείτε μια ενδιαφέρουσα περίπτωση χρήσης; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

## What Should You Learn Next?

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε πρόσθετα χαρακτηριστικά του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}