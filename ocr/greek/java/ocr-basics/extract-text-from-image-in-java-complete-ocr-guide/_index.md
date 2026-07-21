---
category: general
date: 2026-07-21
description: Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας Java OCR. Μάθετε πώς να μετατρέπετε
  PNG σε κείμενο, να διαβάζετε κείμενο από PNG, να φορτώνετε εικόνα για OCR και να
  εκτελείτε OCR σε εικόνα σε λίγα μόνο βήματα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert png to text
- read text from png
- load image for ocr
- perform ocr on image
language: el
lastmod: 2026-07-21
og_description: Εξαγωγή κειμένου από εικόνα με Java. Αυτός ο οδηγός σας δείχνει πώς
  να μετατρέψετε PNG σε κείμενο, να διαβάσετε κείμενο από PNG, να φορτώσετε εικόνα
  για OCR και να εκτελέσετε OCR στην εικόνα αποδοτικά.
og_image_alt: Screenshot of Java code extracting text from an image using OCR
og_title: Εξαγωγή κειμένου από εικόνα σε Java – Βήμα‑βήμα οδηγός OCR
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  headline: Extract Text from Image in Java – Complete OCR Guide
  type: TechArticle
- description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  name: Extract Text from Image in Java – Complete OCR Guide
  steps:
  - name: Low‑Quality Images
    text: 'If the PNG is blurry or has low contrast, OCR accuracy drops. A quick fix
      is to pre‑process the image:'
  - name: Multi‑Language Support
    text: Tess4J can handle many languages. Just download the appropriate `.traineddata`
      file and point `tesseract.setLanguage("spa")` for Spanish, for example.
  - name: Large PDFs or Multi‑Page Images
    text: If you need to **extract text from image** files inside a PDF, split each
      page into PNGs first (using PDFBox) and then feed each PNG to the same OCR routine.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Εξαγωγή κειμένου από εικόνα σε Java – Πλήρης οδηγός OCR
url: /el/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Εικόνα σε Java – Πλήρης Οδηγός OCR

Έχετε χρειαστεί ποτέ να **εξάγετε κείμενο από εικόνα** αλλά δεν ήξερες ποια βιβλιοθήκη Java να επιλέξεις; Δεν είστε μόνοι. Είτε ψηφιοποιείτε αποδείξεις, είτε σκανάρετε PDF, είτε δημιουργείτε ένα αναζητήσιμο αρχείο, η εξαγωγή κειμένου από ένα PNG αποτελεί καθημερινό πρόβλημα για πολλούς προγραμματιστές.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από μια πρακτική λύση που σας επιτρέπει να **μετατρέψετε PNG σε κείμενο**, **διαβάσετε κείμενο από PNG**, **φορτώσετε εικόνα για OCR**, και **εκτελέσετε OCR σε εικόνα** — όλα με λίγες γραμμές καθαρού κώδικα Java. Στο τέλος θα έχετε ένα εκτελέσιμο πρόγραμμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε project.

## Τι Θα Δημιουργήσετε

Θα φτιάξουμε μια μικρή εφαρμογή κονσόλας Java που:

1. Φορτώνει ένα αρχείο PNG από το δίσκο.  
2. Στέλνει την εικόνα σε μια μηχανή OCR (Tess4J, ένα Java wrapper για το Tesseract).  
3. Εκτυπώνει το αναγνωρισμένο κείμενο στην κονσόλα.

Καμία εξωτερική υπηρεσία, καμία μαγεία — μόνο καθαρή Java και μια ανοιχτή μηχανή OCR.

## Προαπαιτούμενα

- **Java 17** ή νεότερη (ο κώδικας συντάσσεται και με παλαιότερες εκδόσεις, αλλά η Java 17 προσφέρει τα πιο πρόσφατα χαρακτηριστικά της γλώσσας).  
- **Maven** ή **Gradle** για διαχείριση εξαρτήσεων.  
- Ένα δείγμα PNG με όνομα `sample.png` τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε (π.χ. `src/main/resources`).  
- Βασική εξοικείωση με τη μέθοδο `main` της Java και τη διαχείριση εξαιρέσεων.

Αν κάποιο από αυτά σας φαίνεται άγνωστο, μην ανησυχείτε — κάθε βήμα περιλαμβάνει μια σύντομη επανάληψη.

## Βήμα 1: Ρύθμιση του Project και Προσθήκη της Βιβλιοθήκης OCR

Πρώτα, δημιουργήστε ένα νέο Maven project (ή Gradle αν προτιμάτε). Προσθέστε την εξάρτηση Tess4J, η οποία φέρνει τα δυαδικά αρχεία του Tesseract.

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ocr-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- Tess4J – Java wrapper for Tesseract OCR -->
        <dependency>
            <groupId>net.sourceforge.tess4j</groupId>
            <artifactId>tess4j</artifactId>
            <version>5.5.1</version>
        </dependency>
    </dependencies>
</project>
```

> **Συμβουλή:** Αν χρησιμοποιείτε Gradle, η αντίστοιχη γραμμή είναι `implementation 'net.sourceforge.tess4j:tess4j:5.5.1'`.

Η προσθήκη αυτής της βιβλιοθήκης σας δίνει την κλάση `Tesseract`, η οποία διαχειρίζεται το βαρέως βάρους **εκτέλεση OCR σε εικόνα**.

## Βήμα 2: Φόρτωση Εικόνας για OCR

Τώρα πρέπει να **φορτώσετε εικόνα για OCR**. Το Tess4J δουλεύει με `java.awt.image.BufferedImage`, οπότε θα διαβάσουμε το PNG χρησιμοποιώντας `ImageIO`.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

public class OcrDemo {

    /**
     * Loads a PNG file from the given path and returns a BufferedImage.
     *
     * @param path absolute or relative path to the PNG file
     * @return BufferedImage containing the image data
     * @throws IOException if the file cannot be read
     */
    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image to be recognized
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }
```

Η παραπάνω μέθοδος απομονώνει καθαρά τη λογική **φόρτωσης εικόνας για OCR**, κάνοντας τον υπόλοιπο κώδικα πιο εύκολο στην δοκιμή. Παρατηρήστε το σχόλιο — αντανακλά το αρχικό απόσπασμα ενώ επεκτείνεται για σαφήνεια.

## Βήμα 3: Εκτέλεση OCR σε Εικόνα

Με την εικόνα στη μνήμη, μπορούμε τώρα να **εκτελέσουμε OCR σε εικόνα**. Η παρουσία `Tesseract` είναι η μηχανή μας· θα τη ρυθμίσουμε να χρησιμοποιεί τα προεπιλεγμένα αγγλικά δεδομένα γλώσσας που έρχονται με το Tess4J.

```java
    /**
     * Runs OCR on the supplied BufferedImage and returns the extracted text.
     *
     * @param image the image to analyze
     * @return plain text recognized from the image
     * @throws TesseractException if the OCR process fails
     */
    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();

        // Optional: set the datapath if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");

        // Step 4: Run OCR and capture the recognized text
        return tesseract.doOCR(image);
    }
```

Εδώ συγχωνεύσαμε τα αρχικά “Βήμα 1” και “Βήμα 4” σε μία μέθοδο, επειδή το αντικείμενο `Tesseract` είναι φθηνό να δημιουργηθεί και θέλουμε ο κώδικας να παραμείνει συμπαγής. Το σχόλιο εξακολουθεί να αναφέρει τα αρχικά βήματα για διαφάνεια.

## Βήμα 4: Συνδυάστε Όλα – Μέθοδος main

Τέλος, φέρνουμε όλα μαζί στο `main`. Εδώ θα **διαβάσετε κείμενο από PNG** και θα δείτε το αποτέλεσμα στην κονσόλα.

```java
    public static void main(String[] args) {
        // Adjust the path to point at your PNG file
        String imagePath = "src/main/resources/sample.png";

        try {
            // Load the PNG image
            BufferedImage image = loadImage(imagePath);

            // Extract text from the image
            String recognizedText = extractText(image);

            // Step 5: Display the extracted text
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR error: " + e.getMessage());
        }
    }
}
```

Όταν εκτελέσετε `mvn compile exec:java -Dexec.mainClass="com.example.ocrdemo.OcrDemo"` (ή το αντίστοιχο Gradle), θα πρέπει να δείτε κάτι όπως:

```
=== OCR Result ===
Hello, world!
This is a sample PNG file.
```

Αυτή η έξοδος αποδεικνύει ότι έχετε εξαγάγει επιτυχώς **κείμενο από εικόνα**, **μετατρέψει PNG σε κείμενο**, και **διαβάσει κείμενο από PNG** σε ένα ενιαίο, τακτοποιημένο πρόγραμμα.

## Διαχείριση Συνηθισμένων Περιπτώσεων

### Εικόνες Χαμηλής Ποιότητας

Αν το PNG είναι θολό ή έχει χαμηλή αντίθεση, η ακρίβεια του OCR μειώνεται. Μια γρήγορη λύση είναι η προεπεξεργασία της εικόνας:

```java
// Example: Convert to grayscale and apply a binary threshold
BufferedImage gray = new BufferedImage(
        image.getWidth(), image.getHeight(),
        BufferedImage.TYPE_BYTE_GRAY);
Graphics2D g = gray.createGraphics();
g.drawImage(image, 0, 0, null);
g.dispose();

// Simple binary threshold
for (int y = 0; y < gray.getHeight(); y++) {
    for (int x = 0; x < gray.getWidth(); x++) {
        int rgb = gray.getRGB(x, y) & 0xFF;
        int binary = rgb < 128 ? 0x000000 : 0xFFFFFF;
        gray.setRGB(x, y, binary);
    }
}
String text = extractText(gray);
```

### Υποστήριξη Πολλαπλών Γλωσσών

Το Tess4J μπορεί να χειριστεί πολλές γλώσσες. Απλώς κατεβάστε το κατάλληλο αρχείο `.traineddata` και ορίστε `tesseract.setLanguage("spa")` για Ισπανικά, για παράδειγμα.

### Μεγάλα PDF ή Πολυσελίδες Εικόνες

Αν χρειάζεται να **εξάγετε κείμενο από εικόνα** μέσα σε PDF, πρώτα χωρίστε κάθε σελίδα σε PNG (χρησιμοποιώντας PDFBox) και μετά τροφοδοτήστε κάθε PNG στην ίδια ρουτίνα OCR.

## Πλήρες Παράδειγμα (Όλος ο Κώδικας σε Ένα Αρχείο)

Παρακάτω βρίσκεται η πλήρης, έτοιμη προς εκτέλεση κλάση Java. Αντιγράψτε‑και‑επικολλήστε την στο `src/main/java/com/example/ocrdemo/OcrDemo.java` και είστε έτοιμοι.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Demonstrates how to extract text from image (PNG) using Java and Tess4J.
 */
public class OcrDemo {

    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image for OCR
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }

    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();
        // Uncomment and set if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");
        // Step 4: Perform OCR on image
        return tesseract.doOCR(image);
    }

    public static void main(String[] args) {
        // Path to the PNG you want to convert to text
        String imagePath = "src/main/resources/sample.png";

        try {
            BufferedImage image = loadImage(imagePath);
            String recognizedText = extractText(image);
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("Error during OCR: " + e.getMessage());
        }
    }
}
```

Η εκτέλεση της κλάσης εκτυπώνει το αποτέλεσμα του OCR, επιβεβαιώνοντας ότι έχετε επιτυχώς **εκτελέσει OCR σε εικόνα** και μετατρέψει το PNG σας σε επεξεργάσιμο κείμενο.

## Ανακεφαλαίωση & Επόμενα Βήματα

Ξεκινήσαμε **εξάγοντας κείμενο από εικόνα** με μια ελαφριά ρύθμιση Java. Τώρα ξέρετε πώς να **φορτώνετε εικόνα για OCR**, **να εκτελείτε OCR σε εικόνα**, και **να διαβάζετε κείμενο από PNG** — βασικά δομικά στοιχεία για οποιοδήποτε pipeline ψηφιοποίησης εγγράφων.

Θέλετε να προχωρήσετε παραπέρα; Δοκιμάστε τις παρακάτω ιδέες:

- **Επεξεργασία παρτίδας:** Επανάληψη σε έναν φάκελο PNG και αποθήκευση κάθε αποτελέσματος σε αρχείο `.txt`.  
- **Ενσωμάτωση με βάση δεδομένων:** Αποθήκευση των εξαγόμενων συμβολοσειρών μαζί με μεταδεδομένα για αναζητήσιμα αρχεία.  
- **Συνδυασμός με NLP:** Εισαγωγή του αποτελέσματος OCR σε μοντέλο ανάλυσης συναισθήματος για γρήγορες γνώσεις.  

Κάθε μία από αυτές τις επεκτάσεις βασίζεται στις ίδιες βασικές έννοιες που καλύψαμε, οπότε είστε έτοιμοι να πειραματιστείτε.

---

*Καλό κώδικα! Αν αντιμετωπίσετε οποιοδήποτε πρόβλημα*

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίησή σας.

- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [image to text java: Convert Image to Text with Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}