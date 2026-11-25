---
category: general
date: 2026-08-06
description: Αναγνώριση κειμένου από εικόνα χρησιμοποιώντας το Aspose OCR σε Java.
  Μάθετε πώς να εξάγετε κείμενο από jpg, να μετατρέψετε την εικόνα σε κείμενο και
  να λάβετε το αποτέλεσμα OCR εικόνας σε συμβολοσειρά.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from image
- extract text from jpg
- convert image to text
- how to extract text
- ocr image to string
language: el
lastmod: 2026-08-06
og_description: Αναγνώριση κειμένου από εικόνα χρησιμοποιώντας Aspose OCR σε Java.
  Αυτός ο οδηγός σας δείχνει πώς να εξάγετε κείμενο από αρχεία jpg, να μετατρέψετε
  την εικόνα σε κείμενο και να λάβετε το αποτέλεσμα OCR εικόνας σε συμβολοσειρά.
og_image_alt: Screenshot of Java code that recognizes text from an image using Aspose
  OCR
og_title: Αναγνώριση κειμένου από εικόνα με το Aspose OCR – βήμα‑βήμα οδηγός Java
schemas:
- author: Aspose
  dateModified: '2026-08-06'
  description: Recognize text from image using Aspose OCR in Java. Learn how to extract
    text from jpg, convert image to text, and get an OCR image to string result.
  headline: Recognize text from image with Aspose OCR – complete Java guide
  type: TechArticle
- description: Recognize text from image using Aspose OCR in Java. Learn how to extract
    text from jpg, convert image to text, and get an OCR image to string result.
  name: Recognize text from image with Aspose OCR – complete Java guide
  steps:
  - name: Load your Aspose OCR license (optional)
    text: Loading a license disables the evaluation watermark and unlocks full language
      support.
  - name: Create an OCR engine instance
    text: '```java import com.aspose.ocr.OcrEngine;'
  - name: (Optional) Specify the language for recognition
    text: '```java public ImageToText() { // Example: restrict recognition to English
      to improve accuracy engine.setLanguage("eng"); // Use ISO‑639‑2 codes, e.g.,
      "spa" for Spanish } ```'
  - name: Process the image file and obtain the OCR result
    text: '```java import com.aspose.ocr.OcrResult; import java.nio.file.Paths;'
  - name: Retrieve and display the recognized text
    text: '```java public static void main(String[] args) { ImageToText converter
      = new ImageToText(); String text = converter.extractText("YOUR_DIRECTORY/sample.jpg");
      System.out.println("Recognized text:"); System.out.println(text); } } ```'
  type: HowTo
tags:
- Aspose OCR
- Java
- Image processing
title: Αναγνώριση κειμένου από εικόνα με το Aspose OCR – πλήρης οδηγός Java
url: /el/java/ocr-operations/recognize-text-from-image-with-aspose-ocr-complete-java-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση κειμένου από εικόνα με Aspose OCR – πλήρης οδηγός Java

Αν χρειάζεστε **αναγνώριση κειμένου από εικόνα** σε μια εφαρμογή Java, αυτό το tutorial σας παρουσιάζει μια έτοιμη λύση. Στο τέλος του οδηγού θα μπορείτε να εξάγετε κείμενο από αρχεία jpg, να μετατρέψετε εικόνα σε κείμενο και να λάβετε μια τιμή `ocr image to string` με λίγες μόνο γραμμές κώδικα.

Το παράδειγμα χρησιμοποιεί το Aspose.OCR for Java, μια βιβλιοθήκη που υποστηρίζει πάνω από 70 γλώσσες και λειτουργεί σε οποιαδήποτε πλατφόρμα που τρέχει Java 8 ή νεότερη. Θα δείτε γιατί αυτή η προσέγγιση είναι αξιόπιστη, πώς να αντιμετωπίζετε κοινά προβλήματα, και τι να κάνετε όταν χρειάζεται να επεξεργαστείτε μεγάλες παρτίδες.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

- Java Development Kit 8 ή νεότερο εγκατεστημένο  
- Maven ή Gradle για διαχείριση εξαρτήσεων (ο οδηγός χρησιμοποιεί Maven)  
- Ένα αρχείο άδειας Aspose OCR (προαιρετικό αλλά συνιστάται για παραγωγή)  
- Ένα δείγμα εικόνας JPEG (`sample.jpg`) που περιέχει καθαρό τυπωμένο κείμενο  

Αν δεν έχετε άδεια, η βιβλιοθήκη λειτουργεί σε λειτουργία αξιολόγησης με υδατογράφημα στο αποτέλεσμα.

## Προσθήκη Aspose OCR στο έργο σας

Προσθέστε την ακόλουθη εξάρτηση στο `pom.xml`. Αυτό θα κατεβάσει την πιο πρόσφατη σταθερή έκδοση (ως Αύγουστο 2026).

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.11</version>
</dependency>
```

> **Pro tip:** Χρησιμοποιήστε συγκεκριμένο αριθμό έκδοσης αντί του `LATEST` για να αποφύγετε τυχαίες αλλαγές που μπορεί να σπάσουν τον κώδικά σας όταν η βιβλιοθήκη ενημερωθεί.

## Υλοποίηση βήμα‑βήμα

Κάθε βήμα παρακάτω αντιστοιχεί σε μια γραμμή του αρχικού αποσπάσματος κώδικα, αλλά το επεκτείνουμε με περιεχόμενο, διαχείριση σφαλμάτων και σχόλια βέλτιστων πρακτικών.

### Βήμα 1: Φόρτωση της άδειας Aspose OCR (προαιρετικό)

Η φόρτωση μιας άδειας απενεργοποιεί το υδατογράφημα αξιολόγησης και ξεκλειδώνει πλήρη υποστήριξη γλωσσών.

```java
import com.aspose.ocr.License;

public class ImageToText {
    static {
        try {
            // Replace the path with the location of your .lic file
            new License().setLicense("YOUR_LICENSE_PATH");
        } catch (Exception e) {
            // In development you may skip licensing; the catch logs the issue.
            System.err.println("License file not found: " + e.getMessage());
        }
    }
```

*Γιατί είναι σημαντικό:* Χωρίς έγκυρη άδεια η μηχανή OCR λειτουργεί σε δοκιμαστική λειτουργία, η οποία προσθέτει υδατογράφημα στο εξαγόμενο κείμενο σε ορισμένες μορφές. Η φόρτωση της άδειας μία φορά σε static block εξασφαλίζει ότι εφαρμόζεται πριν από οποιαδήποτε λειτουργία OCR.

### Βήμα 2: Δημιουργία στιγμιοτύπου του OCR engine

```java
import com.aspose.ocr.OcrEngine;

    private final OcrEngine engine = new OcrEngine();
```

Το αντικείμενο `OcrEngine` είναι το κεντρικό στοιχείο που εκτελεί την βαριά δουλειά. Η δημιουργία του μία φορά και η επαναχρησιμοποίησή του για πολλαπλές εικόνες μειώνει το κόστος κατανομής μνήμης.

### Βήμα 3: (Προαιρετικό) Καθορισμός γλώσσας για την αναγνώριση

```java
    public ImageToText() {
        // Example: restrict recognition to English to improve accuracy
        engine.setLanguage("eng"); // Use ISO‑639‑2 codes, e.g., "spa" for Spanish
    }
```

*Γιατί μπορεί να θέλετε να ορίσετε γλώσσα:* Ο περιορισμός του συνόλου γλωσσών περιορίζει το σύνολο χαρακτήρων που αξιολογεί η μηχανή, κάτι που συχνά οδηγεί σε υψηλότερη ακρίβεια και ταχύτερη επεξεργασία. Αν χρειάζεστε πολυγλωσσική υποστήριξη, παραλείψτε αυτήν την κλήση ή ορίστε πολλαπλές γλώσσες με λίστα χωρισμένη με κόμμα.

### Βήμα 4: Επεξεργασία του αρχείου εικόνας και λήψη του αποτελέσματος OCR

```java
import com.aspose.ocr.OcrResult;
import java.nio.file.Paths;

    public String extractText(String imagePath) {
        try {
            // Validate that the file exists and is a JPEG
            if (!Files.isRegularFile(Paths.get(imagePath))) {
                throw new IllegalArgumentException("File not found: " + imagePath);
            }

            // The processImage method returns an OcrResult object containing the recognized text.
            OcrResult result = engine.processImage(imagePath);
            return result.getText(); // This is the "ocr image to string" value.
        } catch (Exception ex) {
            System.err.println("Error during OCR processing: " + ex.getMessage());
            return "";
        }
    }
```

*Γιατί αυτό το βήμα είναι κρίσιμο:* Η `processImage` διαβάζει το bitmap, εκτελεί τον αλγόριθμο αναγνώρισης και γεμίζει το `OcrResult`. Η μέθοδος ρίχνει εξαιρέσεις για μη υποστηριζόμενες μορφές ή σφάλματα I/O, τις οποίες πιάσαμε για να διατηρήσουμε την εφαρμογή σταθερή.

### Βήμα 5: Ανάκτηση και εμφάνιση του αναγνωρισμένου κειμένου

```java
    public static void main(String[] args) {
        ImageToText converter = new ImageToText();
        String text = converter.extractText("YOUR_DIRECTORY/sample.jpg");
        System.out.println("Recognized text:");
        System.out.println(text);
    }
}
```

Η εκτέλεση της μεθόδου `main` εκτυπώνει το εξαγόμενο string στην κονσόλα. Αυτό δείχνει τη ροή **convert image to text** σε ένα ενιαίο, αυτόνομο πρόγραμμα.

## Πλήρες, εκτελέσιμο παράδειγμα

Παρακάτω βρίσκεται το πλήρες αρχείο πηγαίου κώδικα που μπορείτε να αντιγράψετε στο `src/main/java/com/example/ImageToText.java`. Προσαρμόστε τη διαδρομή της άδειας και τη θέση της εικόνας πριν το μεταγλωττίσετε.

```java
package com.example;

import com.aspose.ocr.License;
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.OcrResult;

import java.nio.file.Files;
import java.nio.file.Paths;

public class ImageToText {
    // Load license (optional)
    static {
        try {
            new License().setLicense("YOUR_LICENSE_PATH");
        } catch (Exception e) {
            System.err.println("License file not loaded: " + e.getMessage());
        }
    }

    // Reusable OCR engine
    private final OcrEngine engine = new OcrEngine();

    public ImageToText() {
        // Optional language restriction – improves accuracy for English text
        engine.setLanguage("eng");
    }

    /**
     * Extracts text from the given image file.
     *
     * @param imagePath absolute or relative path to a JPEG image
     * @return recognized text; empty string if an error occurs
     */
    public String extractText(String imagePath) {
        try {
            if (!Files.isRegularFile(Paths.get(imagePath))) {
                throw new IllegalArgumentException("File not found: " + imagePath);
            }
            OcrResult result = engine.processImage(imagePath);
            return result.getText();
        } catch (Exception ex) {
            System.err.println("Error during OCR processing: " + ex.getMessage());
            return "";
        }
    }

    public static void main(String[] args) {
        ImageToText converter = new ImageToText();
        String text = converter.extractText("YOUR_DIRECTORY/sample.jpg");
        System.out.println("Recognized text:");
        System.out.println(text);
    }
}
```

**Αναμενόμενο αποτέλεσμα** (υπόθεση ότι το `sample.jpg` περιέχει τη φράση “Hello World”):

```
Recognized text:
Hello World
```

Αν η εικόνα είναι θολή ή περιέχει μη‑λατινικούς χαρακτήρες, το αποτέλεσμα μπορεί να περιέχει λανθασμένες αναγνώσεις. Σε τέτοιες περιπτώσεις, εξετάστε:

- Προεπεξεργασία της εικόνας (αύξηση αντίθεσης, μετατροπή σε γκρι κλίμακα)  
- Χρήση διαφορετικού κωδικού γλώσσας (`engine.setLanguage("chi_sim")` για Απλοποιημένα Κινέζικα)  
- Προσαρμογή της μεθόδου `setResolution` του OCR engine για εικόνες υψηλότερης DPI

## Διαχείριση κοινών περιπτώσεων άκρων

| Κατάσταση | Προτεινόμενη ενέργεια |
|-----------|----------------------|
| **Μεγάλη εικόνα ( >5 MP )** | Σμίκρυνση της εικόνας σε 300 DPI πριν τη μεταβίβαση στη `processImage` για μείωση κατανάλωσης μνήμης. |
| **Πολλές γλώσσες σε μία εικόνα** | Χρησιμοποιήστε `engine.setLanguage("eng,spa,fre")` για ταυτόχρονη ανίχνευση. |
| **Επεξεργασία παρτίδας** | Δημιουργήστε μια δεξαμενή στιγμιοτύπων `OcrEngine` ή επαναχρησιμοποιήστε ένα μοναδικό στιγμιότυπο σε βρόχο· αποφύγετε τη δημιουργία νέου engine ανά εικόνα. |
| **Μη‑JPEG μορφές** | Το Aspose OCR υποστηρίζει PNG, BMP, TIFF και PDF. Βεβαιωθείτε ότι η επέκταση αρχείου ταιριάζει με την πραγματική μορφή ή μετατρέψτε το αρχείο σε PNG πρώτα. |
| **Βελτιστοποίηση απόδοσης** | Καλέστε `engine.setPageSegMode(OcrEngine.PageSegMode.AUTO)` για αυτόματη ανίχνευση διάταξης, ή `SINGLE_BLOCK` για απλά μπλοκ κειμένου. |

## Συχνές ερωτήσεις

**Πώς εξάγω κείμενο από JPG που περιέχει χειρόγραφα σημειώσεις;**  
Το χειρόγραφο κείμενο είναι πιο δύσκολο για τις μηχανές OCR. Το Aspose OCR παρέχει `setLanguage("eng")` για τυπωμένη αγγλική, αλλά για πλάγια γραφή ίσως χρειαστεί να ενεργοποιήσετε τη σημαία `setRecognitionMode(OcrEngine.RecognitionMode.HANDWRITING)` (διαθέσιμη σε νεότερες εκδόσεις). Η ακρίβεια θα παραμείνει χαμηλότερη από αυτήν του τυπωμένου κειμένου.

**Μπορώ να μετατρέψω εικόνα σε κείμενο χωρίς να εγκαταστήσω τη βιβλιοθήκη Aspose;**  
Ναι, μπορείτε να χρησιμοποιήσετε το Tesseract μέσω του wrapper `tess4j`, αλλά το Aspose OCR προσφέρει API υψηλότερου επιπέδου, καλύτερη υποστήριξη γλωσσών και χωρίς εγγενείς εξαρτήσεις. Ο κώδικας που παρουσιάζεται εδώ είναι ο πιο σύντομος τρόπος για να πετύχετε `ocr image to string` σε καθαρή Java.

**Τι κάνω αν πρέπει να εξάγω κείμενο από πολλά JPG σε έναν φάκελο;**  
Τυλίξτε τη μέθοδο `extractText` σε βρόχο που διατρέχει τα `Files.list(Paths.get("folder"))` και φιλτράρει με `*.jpg`. Αποθηκεύστε κάθε αποτέλεσμα σε έναν χάρτη (map) για επεξεργασία αργότερα.

## Συμπέρασμα

Τώρα ξέρετε πώς να **αναγνωρίζετε κείμενο από εικόνα** χρησιμοποιώντας Aspose OCR σε Java. Ο οδηγός κάλυψε κάθε βήμα—από τη φόρτωση άδειας και τη δημιουργία του OCR engine, μέχρι την επεξεργασία JPEG και την εκτύπωση του εξαγόμενου string. Με αυτή τη βάση μπορείτε να **εξάγετε κείμενο από jpg** αρχεία, **μετατρέψετε εικόνα σε κείμενο**, και να ενσωματώσετε το αποτέλεσμα `ocr image to string` σε μεγαλύτερες ροές εργασίας όπως ευρετηρίαση εγγράφων, αυτοματοποίηση εισαγωγής δεδομένων ή εργαλεία προσβασιμότητας.

**Επόμενα βήματα**  
- Εξερευνήστε την κλάση `OcrResult` για να λάβετε βαθμολογίες εμπιστοσύνης (`result.getConfidence()`).  
- Συνδυάστε αυτή τη γραμμή OCR με το Apache PDFBox για εξαγωγή κειμένου από σαρωμένα PDF.  
- Πειραματιστείτε με επεξεργασία παρτίδας και πολυνηματική εκτέλεση για μεγάλες συλλογές εικόνων.  

Καλή προγραμματιστική, και αφήστε το κείμενο στις εικόνες σας να δουλέψει για εσάς!

## Τι πρέπει να μάθετε μετά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}