---
category: general
date: 2026-06-16
description: Μάθετε πώς να εκτελείτε OCR σε αρχεία εικόνας στη Java. Αυτό το σεμινάριο
  καλύπτει την αναγνώριση κειμένου από PNG, την εξαγωγή κειμένου από εικόνα, τη μετατροπή
  εικόνας σε κείμενο και τη φόρτωση εικόνας για OCR.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- extract text from image
- convert image to text
- load image for OCR
language: el
og_description: Εκτελέστε OCR σε εικόνα χρησιμοποιώντας Java. Αυτός ο οδηγός δείχνει
  πώς να αναγνωρίσετε κείμενο από PNG, να εξάγετε κείμενο από εικόνα και να μετατρέψετε
  την εικόνα σε κείμενο με ένα έτοιμο παράδειγμα προς εκτέλεση.
og_title: Εκτελέστε OCR σε εικόνα με Java – Πλήρης οδηγός προγραμματισμού
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  headline: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  name: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'If `hello.png` contains the phrase “Hello, OCR world!”, the console will
      display something like:'
  - name: 5.1 Dealing with Low‑Resolution Images
    text: 'If the source PNG is blurry, OCR accuracy drops. A quick fix is to upscale
      the image before feeding it to the engine:'
  - name: 5.2 Multi‑Language Documents
    text: 'If you anticipate French or German text, simply add the language codes
      to `setLanguage`:'
  - name: 5.3 Skipping Empty Pages
    text: 'Sometimes a scanned PDF page renders as a blank PNG. Detecting an empty
      image saves processing time:'
  type: HowTo
tags:
- Java
- OCR
- Image Processing
title: Εκτέλεση OCR σε εικόνα με Java – Πλήρης οδηγός βήμα‑προς‑βήμα
url: /el/java/ocr-basics/perform-ocr-on-image-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτελέστε OCR σε Εικόνα με Java – Πλήρης Οδηγός Βήμα‑βήμα

Έχετε χρειαστεί ποτέ να **εκτελέσετε OCR σε αρχείο εικόνας** αλλά δεν ήξερες ποια βιβλιοθήκη Java να επιλέξεις; Δεν είστε μόνοι. Είτε χτίζετε έναν σαρωτή αποδείξεων, έναν αρχειοθέτη εγγράφων, είτε απλώς θέλετε να μετατρέψετε εικόνες σε αναζητήσιμο κείμενο, η εκμάθηση του **πώς να εκτελέσετε OCR σε εικόνα** με Java είναι μια χρήσιμη δεξιότητα.

Σε αυτό το tutorial θα περάσουμε από όλα όσα χρειάζεστε για να **εκτελέσετε OCR σε αρχεία εικόνας**: φόρτωση της εικόνας, ρύθμιση της μηχανής, αναγνώριση του κειμένου και, τέλος, εκτύπωση του αποτελέσματος. Στο τέλος θα μπορείτε να **αναγνωρίσετε κείμενο από PNG** αρχεία, **εξάγετε κείμενο από εικόνα** και **μετατρέψετε εικόνα σε κείμενο** με λίγες μόνο γραμμές κώδικα.

## Προαπαιτούμενα

- Java 17 ή νεότερη (ο κώδικας μεταγλωττίζεται με οποιοδήποτε πρόσφατο JDK)
- Maven εγκατεστημένο (ή το αγαπημένο σας εργαλείο κατασκευής)
- Βασική εξοικείωση με τη σύνταξη της Java
- Ένα αρχείο PNG που θέλετε να δοκιμάσετε (θα το ονομάσουμε `hello.png`)

> **Συμβουλή:** Αν δεν έχετε PNG, δημιουργήστε ένα κάνοντας screenshot οποιουδήποτε κειμένου και αποθηκεύστε το ως `hello.png` σε φάκελο που ονομάζεται `resources`.

## Τι Θα Δημιουργήσουμε

Μια μικρή εφαρμογή κονσόλας με όνομα `OcrDemo` που:

1. **Φορτώνει εικόνα για OCR** – διαβάζει ένα PNG από το δίσκο.
2. **Εκτελεί OCR σε εικόνα** – χρησιμοποιεί τη μηχανή Tesseract μέσω του Tess4J.
3. **Εξάγει κείμενο από εικόνα** – επιστρέφει ένα `String` με το αναγνωρισμένο περιεχόμενο.
4. Εκτυπώνει το αποτέλεσμα στην κονσόλα.

Ας βουτήξουμε.

## Βήμα 1: Ρύθμιση του Έργου και Προσθήκη Tess4J

Πρώτα, δημιουργήστε ένα νέο Maven project (ή Gradle αν προτιμάτε). Προσθέστε την εξάρτηση Tess4J, η οποία τυλίγει τη δημοφιλή μηχανή Tesseract OCR.

```xml
<!-- pom.xml -->
<project>
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

> **Γιατί Tess4J;** Είναι ενεργά συντηρημένο, λειτουργεί δια-πλατφόρμα και παρέχει ένα καθαρό Java API για εργασίες **εκτέλεσης OCR σε εικόνα**.

## Βήμα 2: Προετοιμασία της Λογικής Φόρτωσης Εικόνας

Τώρα θα γράψουμε μια βοηθητική μέθοδο που **φορτώνει εικόνα για OCR**. Η μέθοδος χρησιμοποιεί το `ImageIO` της Java για να διαβάσει ένα PNG σε ένα `BufferedImage`.

```java
package com.example.ocr;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Utility class responsible for loading images from the file system.
 */
public final class ImageLoader {

    private ImageLoader() { /* utility class */ }

    /**
     * Loads a PNG (or any supported format) from the given path.
     *
     * @param path absolute or relative path to the image file
     * @return BufferedImage instance ready for OCR processing
     * @throws IOException if the file cannot be read
     */
    public static BufferedImage load(String path) throws IOException {
        File imgFile = new File(path);
        if (!imgFile.exists()) {
            throw new IOException("Image file not found: " + path);
        }
        return ImageIO.read(imgFile);
    }
}
```

Παρατηρήστε ότι το όνομα της μεθόδου αντανακλά σαφώς την πρόθεση **φόρτωσης εικόνας για OCR**, κάνοντας τον κώδικα αυτο‑εξηγηματικό.

## Βήμα 3: Ρύθμιση της Μηχανής OCR για **Εκτέλεση OCR σε Εικόνα**

Με την εικόνα στα χέρια, δημιουργούμε ένα αντικείμενο `Tesseract`, ενεργοποιούμε την αυτόματη ανίχνευση γλώσσας και καλούμε το `doOCR`. Αυτό είναι το κεντρικό κομμάτι του πώς **εκτελούμε OCR σε δεδομένα εικόνας**.

```java
package com.example.ocr;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

/**
 * Wrapper around Tess4J that abstracts the OCR workflow.
 */
public final class OcrEngine {

    private final ITesseract tesseract;

    public OcrEngine() {
        tesseract = new Tesseract();

        // Use the bundled tessdata folder (you can also point to a custom one)
        tesseract.setDatapath("tessdata");

        // Enable automatic language detection – improves accuracy across multilingual images
        tesseract.setLanguage("eng"); // fallback language
        tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
        tesseract.setPageSegMode(ITesseract.PSM_AUTO);
    }

    /**
     * Performs OCR on the supplied BufferedImage and returns the recognized text.
     *
     * @param image image to be processed
     * @return the text extracted from the image
     * @throws TesseractException if OCR fails
     */
    public String recognize(BufferedImage image) throws TesseractException {
        return tesseract.doOCR(image);
    }
}
```

> **Γιατί να ενεργοποιήσετε την αυτόματη ανίχνευση;** Επιτρέπει στη μηχανή να επιλέξει το καλύτερο μοντέλο γλώσσας για την εικόνα, κάτι που είναι ιδιαίτερα χρήσιμο όταν **μετατρέπετε εικόνα σε κείμενο** από πηγές που συνδυάζουν Αγγλικά και άλλες γραφές.

## Βήμα 4: Συνδυάστε Όλα – Η Κύρια Εφαρμογή

Ακολουθεί το σημείο εισόδου που **αναγνωρίζει κείμενο από PNG**, **εξάγει κείμενο από εικόνα**, και τέλος εκτυπώνει το αποτέλεσμα. Αυτό είναι το πλήρες, εκτελέσιμο παράδειγμα.

```java
package com.example.ocr;

import net.sourceforge.tess4j.TesseractException;
import java.awt.image.BufferedImage;
import java.io.IOException;

/**
 * Demo application that shows how to perform OCR on image files.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Path to the PNG you want to process
        String imagePath = "resources/hello.png";

        try {
            // Step 1: Load image for OCR
            BufferedImage image = ImageLoader.load(imagePath);

            // Step 2: Create OCR engine instance
            OcrEngine engine = new OcrEngine();

            // Step 3: Perform OCR on image and retrieve the text
            String recognizedText = engine.recognize(image);

            // Step 4: Output the recognized text to the console
            System.out.println("=== Recognized Text ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR processing error: " + e.getMessage());
        }
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Αν το `hello.png` περιέχει τη φράση «Hello, OCR world!», η κονσόλα θα εμφανίσει κάτι σαν:

```
=== Recognized Text ===
Hello, OCR world!
```

Το ακριβές αποτέλεσμα μπορεί να διαφέρει ελαφρώς ανάλογα με την ποιότητα της εικόνας, αλλά θα πρέπει να δείτε το κείμενο που τοποθετήσατε στο PNG.

## Βήμα 5: Διαχείριση Συνηθισμένων Περιπτώσεων

### 5.1 Αντιμετώπιση Χαμηλής Ανάλυσης Εικόνων

Αν το πηγαίο PNG είναι θολό, η ακρίβεια του OCR μειώνεται. Μια γρήγορη λύση είναι η μεγέθυνση της εικόνας πριν τη δώσετε στη μηχανή:

```java
import java.awt.Graphics2D;
import java.awt.RenderingHints;

public static BufferedImage upscale(BufferedImage original, int factor) {
    int width = original.getWidth() * factor;
    int height = original.getHeight() * factor;
    BufferedImage scaled = new BufferedImage(width, height, original.getType());
    Graphics2D g = scaled.createGraphics();
    g.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                       RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g.drawImage(original, 0, 0, width, height, null);
    g.dispose();
    return scaled;
}
```

Καλέστε `upscale(image, 2)` πριν το `engine.recognize(image)` για βελτιωμένα αποτελέσματα.

### 5.2 Πολυγλωσσικά Έγγραφα

Αν προβλέπετε κείμενο στα Γαλλικά ή Γερμανικά, απλώς προσθέστε τους κωδικούς γλώσσας στο `setLanguage`:

```java
tesseract.setLanguage("eng+fra+deu");
```

Η μηχανή θα προσπαθήσει τότε να **εξάγει κείμενο από εικόνα** χρησιμοποιώντας τα συνδυασμένα μοντέλα γλώσσας.

### 5.3 Παράλειψη Κενών Σελίδων

Μερικές φορές μια σαρωμένη σελίδα PDF εμφανίζεται ως κενό PNG. Η ανίχνευση μιας κενής εικόνας εξοικονομεί χρόνο επεξεργασίας:

```java
if (image.getWidth() == 0 || image.getHeight() == 0) {
    System.out.println("Empty image – skipping OCR.");
    return;
}
```

## Βήμα 6: Συσκευασία και Εκτέλεση της Εφαρμογής

1. **Συγγραφή:** `mvn clean compile`
2. **Εκτέλεση:** `mvn exec:java -Dexec.mainClass="com.example.ocr.OcrDemo"`

Βεβαιωθείτε ότι ο φάκελος `tessdata` (που περιέχει τα αρχεία γλώσσας) βρίσκεται δίπλα στο μεταγλωττισμένο JAR ή ορίστε την απόλυτη διαδρομή του στο `OcrEngine`.

## Συμπέρασμα

Τώρα έχετε ένα σταθερό, έτοιμο για παραγωγή μοτίβο για **εκτέλεση OCR σε αρχεία εικόνας** χρησιμοποιώντας Java. Από το **φόρτωμα εικόνας για OCR** μέχρι το **αναγνώριση κειμένου από PNG**, καλύψαμε πώς να **εξάγετε κείμενο από εικόνα**, **μετατρέψετε εικόνα σε κείμενο**, και πώς να αντιμετωπίσετε δύσκολες περιπτώσεις όπως χαμηλής ανάλυσης σάρωση ή πολυγλωσσικό περιεχόμενο.

Στη συνέχεια, μπορείτε να εξερευνήσετε:

- **Επεξεργασία παρτίδας** – βρόχος πάνω από έναν φάκελο PNG και εγγραφή κάθε αποτελέσματος σε αρχείο `.txt`.
- **Δημιουργία PDF** – ενσωμάτωση του εξαγόμενου κειμένου σε αναζητήσιμα PDF.
- **Υπηρεσίες OCR στο σύννεφο** – σύγκριση της τοπικής απόδοσης του Tesseract με APIs όπως το Google Vision ή το Azure Cognitive Services.

Πειραματιστείτε, ρυθμίστε τις παραμέτρους και μοιραστείτε τα ευρήματά σας. Καλό προγραμματισμό, και εύχομαι οι εικόνες σας να μετατρέπονται πάντα σε καθαρό, αναζητήσιμο κείμενο!

![Διάγραμμα που δείχνει τη ροή εργασίας OCR για εκτέλεση OCR σε εικόνα](https://example.com/ocr-workflow.png "παράδειγμα εκτέλεσης OCR σε εικόνα")


## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}