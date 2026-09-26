---
category: general
date: 2026-09-25
description: αναγνώριση κειμένου από εικόνες PNG με το Aspose OCR σε Java – ένας οδηγός
  βήμα‑προς‑βήμα για την εξαγωγή κειμένου από εικόνα και τη μετατροπή εικόνας σε κείμενο.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from png
- extract text from image
- convert image to text
- load image for ocr
- read english text image
language: el
lastmod: 2026-09-25
og_description: Αναγνωρίστε κείμενο από εικόνες PNG χρησιμοποιώντας το Aspose OCR
  σε Java. Ακολουθήστε αυτόν τον οδηγό για να εξάγετε κείμενο από την εικόνα, να μετατρέψετε
  την εικόνα σε κείμενο και να διαβάσετε εικόνα κειμένου στα αγγλικά.
og_image_alt: Screenshot showing recognized text output after processing a PNG with
  Aspose OCR
og_title: Αναγνώριση κειμένου από εικόνες PNG σε Java – πλήρες σεμινάριο Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-09-25'
  description: recognize text from PNG images with Aspose OCR in Java – a step‑by‑step
    guide to extract text from image and convert image to text.
  headline: How to recognize text from PNG images using Aspose OCR in Java
  type: TechArticle
- description: recognize text from PNG images with Aspose OCR in Java – a step‑by‑step
    guide to extract text from image and convert image to text.
  name: How to recognize text from PNG images using Aspose OCR in Java
  steps:
  - name: Why each line matters
    text: '| Line | Purpose | How it helps you **extract text from image** | |------|---------|---------------------------------------------|
      | `new OcrEngine()` | Instantiates the OCR processor. | Provides the engine
      that performs character analysis. | | `engine.setImage(...)` | Loads the PNG
      file into memory'
  - name: 4.1 Missing or corrupt PNG file
    text: 'If the file path is wrong, `ImageStream.fromFile` throws an `IOException`.
      Wrap the loading code in a `try‑catch` block to present a friendly message:'
  - name: 4.2 Non‑English languages
    text: 'Aspose OCR supports many languages. To recognize French, for example, replace
      the language line with:'
  - name: 4.3 Low‑resolution PNGs
    text: OCR accuracy drops when the source image is below 300 dpi. If you notice
      poor results, consider preprocessing the PNG (e.g., scaling up with `java.awt.Image`)
      before passing it to the engine.
  type: HowTo
tags:
- Aspose OCR
- Java
- Image processing
title: Πώς να αναγνωρίζετε κείμενο από εικόνες PNG χρησιμοποιώντας το Aspose OCR σε
  Java
url: /el/java/ocr-operations/how-to-recognize-text-from-png-images-using-aspose-ocr-in-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αναγνωρίσετε κείμενο από εικόνες PNG χρησιμοποιώντας το Aspose OCR σε Java

Αν χρειάζεστε **αναγνώριση κειμένου από PNG** αρχεία σε μια εφαρμογή Java, αυτό το tutorial σας δείχνει ακριβώς πώς να το κάνετε. Στο τέλος του οδηγού θα μπορείτε να **εξάγετε κείμενο από εικόνα**, να μετατρέψετε την εικόνα σε απλό κείμενο και να εμφανίσετε το αποτέλεσμα στην κονσόλα.

Θα χρησιμοποιήσουμε τη βιβλιοθήκη Aspose OCR, η οποία προσφέρει ένα απλό API για τη φόρτωση μιας εικόνας, την επιλογή γλώσσας και την ανάκτηση των αναγνωρισμένων χαρακτήρων. Τα βήματα καλύπτουν επίσης πώς να **φορτώσετε εικόνα για OCR** με ασφάλεια και τι να κάνετε όταν η μηχανή αποτύχει. Δεν απαιτούνται εξωτερικές υπηρεσίες και ο κώδικας εκτελείται σε οποιοδήποτε runtime Java 8+.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* Java 8 ή νεότερη εγκατεστημένη (υποστηρίζονται JDK 8‑21)
* Maven ή Gradle για διαχείριση εξαρτήσεων (θα δείξουμε το απόσπασμα Maven)
* Ένα αρχείο εικόνας με όνομα `sample.png` τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε από τον κώδικα
* Βασική εξοικείωση με τη σύνταξη Java και τον χειρισμό εξαιρέσεων

## Βήμα 1: Προσθήκη Aspose OCR στο έργο σας

Το Aspose OCR διανέμεται ως Maven artifact. Προσθέστε την ακόλουθη εξάρτηση στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Use the latest version available -->
</dependency>
```

Αν προτιμάτε Gradle, το ισοδύναμο είναι:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

Η προσθήκη της βιβλιοθήκης σας δίνει πρόσβαση στα `OcrEngine`, `ImageStream` και στα enums γλώσσας που απαιτούνται για **μετατροπή εικόνας σε κείμενο**.

## Βήμα 2: Δημιουργία κλάσης Java και εισαγωγή των απαιτούμενων πακέτων

Δημιουργήστε μια νέα κλάση με όνομα `SampleDemo`. Εισάγετε τις κλάσεις OCR και τυχόν τυπικές βοηθητικές κλάσεις Java που θα χρησιμοποιήσετε.

```java
package com.example.ocrdemo;

import com.aspose.ocr.*;
import java.io.IOException;
```

Η γραμμή `import com.aspose.ocr.*;` φέρνει όλα όσα χρειάζονται για λειτουργίες OCR, ενώ το `java.io.IOException` θα μας βοηθήσει να διαχειριστούμε σφάλματα σχετιζόμενα με αρχεία.

## ## Αναγνώριση κειμένου από PNG με Aspose OCR

Ο πυρήνας της λύσης βρίσκεται στη μέθοδο `main`. Ακολουθήστε τα αριθμημένα βήματα μέσα στη μέθοδο για να δείτε πώς λειτουργεί κάθε μέρος.

```java
public class SampleDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Step 2: Load the image to be processed (load image for OCR)
        // Replace "YOUR_DIRECTORY" with the actual path to your PNG file.
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.png"));

        // Step 3: (Optional) Specify the language for recognition.
        // The default language is English, but we set it explicitly to
        // demonstrate how to read english text image.
        engine.setLanguage(OcrLanguage.English);

        // Step 4: Execute the OCR process
        if (engine.process()) {
            // Step 5: Retrieve and display the recognized text
            String text = engine.getText();
            System.out.println("Recognized text: " + text);
        } else {
            System.err.println("OCR processing failed.");
        }
    }
}
```

### Γιατί κάθε γραμμή είναι σημαντική

| Γραμμή | Σκοπός | Πώς σας βοηθά να **εξάγετε κείμενο από εικόνα** |
|------|---------|---------------------------------------------|
| `new OcrEngine()` | Δημιουργεί τον επεξεργαστή OCR. | Παρέχει τη μηχανή που εκτελεί την ανάλυση χαρακτήρων. |
| `engine.setImage(...)` | Φορτώνει το αρχείο PNG στη μνήμη. | Αυτό είναι το βήμα **φόρτωσης εικόνας για OCR**· χωρίς αυτό η μηχανή δεν έχει τίποτα να διαβάσει. |
| `engine.setLanguage(OcrLanguage.English)` | Καθορίζει το μοντέλο γλώσσας που θα χρησιμοποιηθεί. | Εξασφαλίζει ακριβή αναγνώριση για σενάρια **ανάγνωσης αγγλικού κειμένου σε εικόνα**. |
| `engine.process()` | Εκτελεί τον αλγόριθμο αναγνώρισης. | Η καρδιά της **μετατροπής εικόνας σε κείμενο** – σαρώνει το bitmap και δημιουργεί μια συμβολοσειρά. |
| `engine.getText()` | Επιστρέφει τους αναγνωρισμένους χαρακτήρες ως `String` της Java. | Σας δίνει το τελικό αποτέλεσμα σε απλό κείμενο που μπορείτε να αποθηκεύσετε, αναζητήσετε ή εμφανίσετε. |

## Βήμα 4: Διαχείριση κοινών περιπτώσεων άκρων

Ακόμα και μια καλά γραμμένη ροή OCR μπορεί να αντιμετωπίσει προβλήματα. Παρακάτω μερικές πρακτικές συμβουλές.

### 4.1 Απουσία ή κατεστραμμένο αρχείο PNG

Αν η διαδρομή του αρχείου είναι λανθασμένη, το `ImageStream.fromFile` πετάει `IOException`. Τυλίξτε τον κώδικα φόρτωσης σε μπλοκ `try‑catch` για να εμφανίσετε φιλικό μήνυμα:

```java
try {
    engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.png"));
} catch (IOException e) {
    System.err.println("Unable to load image: " + e.getMessage());
    return;
}
```

### 4.2 Μη‑Αγγλικές γλώσσες

Το Aspose OCR υποστηρίζει πολλές γλώσσες. Για να αναγνωρίσετε Γαλλικά, για παράδειγμα, αντικαταστήστε τη γραμμή γλώσσας με:

```java
engine.setLanguage(OcrLanguage.French);
```

Η ίδια προσέγγιση λειτουργεί για Κινέζικα, Αραβικά κ.λπ., επιτρέποντάς σας να **εξάγετε κείμενο από εικόνα** ανεξάρτητα από το σύστημα γραφής.

### 4.3 PNG χαμηλής ανάλυσης

Η ακρίβεια του OCR μειώνεται όταν η πηγή είναι κάτω από 300 dpi. Αν παρατηρήσετε χαμηλά αποτελέσματα, σκεφτείτε προεπεξεργασία του PNG (π.χ., μεγέθυνση με `java.awt.Image`) πριν το περάσετε στη μηχανή.

## Βήμα 5: Επαλήθευση του αποτελέσματος

Εκτελέστε το πρόγραμμα από το IDE ή τη γραμμή εντολών:

```bash
mvn compile exec:java -Dexec.mainClass="com.example.ocrdemo.SampleDemo"
```

Θα πρέπει να δείτε κάτι όπως:

```
Recognized text: Hello, world! This is a sample PNG image.
```

Αν η κονσόλα εκτυπώσει `OCR processing failed.`, ελέγξτε ξανά τη διαδρομή του αρχείου και βεβαιωθείτε ότι η εικόνα δεν είναι κατεστραμμένη.

## Πρόσθετες συμβουλές για παραγωγική χρήση

* **Επεξεργασία παρτίδας** – Επανάληψη πάνω σε φάκελο PNG αρχείων, επαναχρησιμοποιώντας ένα μόνο αντικείμενο `OcrEngine` για καλύτερη απόδοση.
* **Διαχείριση μνήμης** – Καλέστε `engine.dispose()` μετά την επεξεργασία μεγάλων εικόνων για να ελευθερώσετε εγγενείς πόρους.
* **Καταγραφή** – Ενσωματώστε ένα πλαίσιο logging (SLF4J, Log4j) αντί για `System.out` για κλιμακούμενες εφαρμογές.
* **Κωδικοί σφάλματος** – Το `engine.process()` επιστρέφει `false` για πολλούς λόγους· χρησιμοποιήστε `engine.getErrorCode()` για διάγνωση συγκεκριμένων αποτυχιών.

## Συμπέρασμα

Τώρα ξέρετε πώς να **αναγνωρίζετε κείμενο από PNG** εικόνες σε Java χρησιμοποιώντας το Aspose OCR. Η πλήρης ροή εργασίας—**φόρτωση εικόνας για OCR**, προαιρετικά ορισμός γλώσσας για **ανάγνωση αγγλικού κειμένου σε εικόνα**, **επεξεργασία**, και **εξαγωγή κειμένου από εικόνα**—είναι έτοιμη να ενσωματωθεί σε οποιοδήποτε έργο Java. Από εδώ μπορείτε να επεκτείνετε τη λύση για **μετατροπή εικόνας σε κείμενο** για PDF, σαρωμένα έγγραφα ή ροές κάμερας σε πραγματικό χρόνο.

## Επόμενα βήματα

* Εξερευνήστε το API **μετατροπής εικόνας σε κείμενο** για μορφές PDF ή TIFF.
* Συνδυάστε αυτή τη ροή OCR με το Apache Tika για ευρετηρίαση του εξαγόμενου κειμένου σε μηχανή αναζήτησης.
* Πειραματιστείτε με πολυγλωσσική υποστήριξη αλλάζοντας το `OcrLanguage.English` με άλλα enums γλώσσας.
* Εξετάστε τις προχωρημένες ρυθμίσεις του Aspose OCR (π.χ., `engine.setPreprocessOptions`) για βελτίωση της ακρίβειας σε θορυβώδεις PNG.

Καλή προγραμματιστική δουλειά και απολαύστε τη μετατροπή εικόνων σε αναζητήσιμο κείμενο!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετα χαρακτηριστικά του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίησή σας.

- [Recognize Text from Image with Aspose OCR – Full Java Guide](/ocr/english/java/advanced-ocr-techniques/recognize-text-from-image-with-aspose-ocr-full-java-guide/)
- [Batch Image OCR in Java – Extract Text from PNG Files Fast](/ocr/english/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)
- [recognize text image using Aspose OCR GPU – Java](/ocr/english/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}