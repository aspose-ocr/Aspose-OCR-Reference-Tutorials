---
category: general
date: 2026-06-16
description: Αναγνώριση κειμένου από εικόνα χρησιμοποιώντας Java OCR. Μάθετε πώς να
  φορτώνετε εικόνα για OCR, να εντοπίζετε γλώσσες στην εικόνα και να ενεργοποιείτε
  την αυτόματη ανίχνευση γλώσσας σε λίγα βήματα.
draft: false
keywords:
- recognize text from image
- load image for OCR
- detect languages in image
- enable auto language detection
language: el
og_description: Αναγνωρίστε κείμενο από εικόνα γρήγορα. Αυτό το σεμινάριο δείχνει
  πώς να φορτώσετε εικόνα για OCR, να εντοπίσετε γλώσσες στην εικόνα και να ενεργοποιήσετε
  την αυτόματη ανίχνευση γλώσσας χρησιμοποιώντας Java.
og_title: Αναγνώριση κειμένου από εικόνα με Java OCR – Πλήρης Οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: recognize text from image using Java OCR. Learn how to load image for
    OCR, detect languages in image, and enable auto language detection in a few steps.
  headline: recognize text from image with Java OCR – Complete Guide
  type: TechArticle
tags:
- OCR
- Java
- Image Processing
- Multilingual OCR
title: Αναγνώριση κειμένου από εικόνα με Java OCR – Πλήρης Οδηγός
url: /el/java/ocr-operations/recognize-text-from-image-with-java-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# αναγνώριση κειμένου από εικόνα με Java OCR – Πλήρης Οδηγός

Έχετε ποτέ χρειαστεί να **αναγνωρίσετε κείμενο από εικόνα** αλλά δεν ήσασταν σίγουροι ποιο Java API θα διαχειριστεί εικόνες με πολλαπλές γλώσσες; Δεν είστε οι μόνοι—οι προγραμματιστές συχνά αντιμετωπίζουν πολυγλωσσικές σαρώσεις, αποδείξεις ή πινακίδες που δεν ταιριάζουν σε μια ενιαία ρύθμιση γλώσσας.  

Σε αυτόν τον οδηγό θα σας δείξουμε πώς να φορτώσετε μια εικόνα για OCR, να ενεργοποιήσετε την αυτόματη ανίχνευση γλώσσας και, τέλος, να εξάγετε το κείμενο που προκύπτει. Στο τέλος θα έχετε ένα έτοιμο για εκτέλεση πρόγραμμα Java που **ανιχνεύει γλώσσες στην εικόνα** και εκτυπώνει το αναγνωρισμένο περιεχόμενο—χωρίς επιπλέον ρυθμίσεις.

> **Τι θα πάρετε:** μια αυτόνομη κλάση Java, εξηγήσεις βήμα‑βήμα και συμβουλές για την αντιμετώπιση ειδικών περιπτώσεων όπως σαρώσεις χαμηλής ανάλυσης ή μη υποστηριζόμενα σενάρια.

## Προαπαιτήσεις

- Java 8 ή νεότερη εγκατεστημένη (ο κώδικας μεταγλωττίζεται επίσης με JDK 11).  
- Μία πρόσφατη βιβλιοθήκη OCR που υποστηρίζει αυτόματη ανίχνευση γλώσσας—εδώ χρησιμοποιούμε **Aspose.OCR for Java**, αλλά οποιαδήποτε βιβλιοθήκη που εκθέτει παρόμοιες ρυθμίσεις θα λειτουργήσει.  
- Ένα αρχείο εικόνας (`mixed_languages.png`) που περιέχει κείμενο σε περισσότερες από μία γλώσσες.  
- Βασική εξοικείωση με Maven ή Gradle για τη διαχείριση εξαρτήσεων (θα δείξουμε ένα απόσπασμα Maven).

Αν κάποια από τα παραπάνω σας φαίνεται άγνωστη, μην ανησυχείτε· τα παρακάτω βήματα περιλαμβάνουν τις ακριβείς συντεταγμένες Maven και ένα ελάχιστο `pom.xml` ώστε να μπορείτε να αντιγράψετε‑και‑επικολλήσετε και να τρέξετε αμέσως.

## Ρύθμιση Έργου

Δημιουργήστε ένα νέο έργο Maven (ή προσθέστε στο υπάρχον) και συμπεριλάβετε την εξάρτηση OCR:

```xml
<!-- pom.xml snippet -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.9</version> <!-- Check for the latest version -->
    </dependency>
</dependencies>
```

Εκτελέστε `mvn clean compile` για να κατεβάσετε τη βιβλιοθήκη. Μόλις ολοκληρωθεί, είστε έτοιμοι να γράψετε τον κώδικα.

## Βήμα 1: Εισαγωγή των Απαιτούμενων Κλάσεων

Πρώτα, φέρνουμε τις κλάσεις που θα χρειαστούμε. Αυτό περιλαμβάνει τη μηχανή OCR, βοηθητικές κλάσεις διαχείρισης εικόνας και δομές αποτελεσμάτων.

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.ImageStream;
import com.aspose.ocr.OcrResult;
```

> **Pro tip:** Κρατήστε τις εισαγωγές σας τακτοποιημένες—συντομεύσεις IDE (`Ctrl+Shift+O` στο IntelliJ) μπορούν να τις οργανώσουν αυτόματα.

## Βήμα 2: Δημιουργία του Αντικειμένου OCR Engine

Η μηχανή είναι η καρδιά της διαδικασίας. Η δημιουργία της μας δίνει πρόσβαση σε ρυθμίσεις όπως η ανίχνευση γλώσσας.

```java
// Step 2: Initialize the OCR engine
OcrEngine engine = new OcrEngine();
```

Γιατί χωρίζουμε τη δημιουργία της μηχανής από τη φόρτωση της εικόνας; Επιτρέπει την επαναχρήση της ίδιας μηχανής για πολλές εικόνες χωρίς επανεκκίνηση βαρέων πόρων, κάτι που μπορεί να βελτιώσει την απόδοση σε σενάρια batch.

## Βήμα 3: Φόρτωση Εικόνας για OCR

Τώρα φορτώνουμε πραγματικά την **εικόνα για OCR**. Η μέθοδος `ImageStream.fromFile` διαβάζει το αρχείο σε ροή που η μηχανή μπορεί να καταναλώσει.

```java
// Step 3: Load the image that contains mixed languages
engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/mixed_languages.png"));
```

Αντικαταστήστε το `YOUR_DIRECTORY` με την απόλυτη ή σχετική διαδρομή όπου βρίσκεται η δοκιμαστική σας εικόνα. Αν η διαδρομή είναι λανθασμένη, θα δείτε ένα `FileNotFoundException`—ένα κοινό λάθος για αρχάριους.

> **Image tip:** Για τα καλύτερα αποτελέσματα, χρησιμοποιήστε μορφές PNG ή TIFF· η συμπίεση JPEG μπορεί να εισάγει τεχνητά εφέ που μπερδεύουν τον αναγνώστη.

## Βήμα 4: Ενεργοποίηση Αυτόματης Ανίχνευσης Γλώσσας

Αυτή είναι η ουσία του οδηγού: **ενεργοποιήστε την αυτόματη ανίχνευση γλώσσας** ώστε η μηχανή αποφασίσει ποια μοντέλα γλώσσας θα εφαρμόσει αυτόματα.

```java
// Step 4: Turn on automatic language detection
engine.getRecognitionSettings().setAutoDetectLanguage(true);
```

Όταν αυτή η σημαία είναι `true`, η μηχανή OCR σαρώνει την εικόνα, προσδιορίζει ποιες γλώσσες υπάρχουν και φορτώνει εσωτερικά τα αντίστοιχα πακέτα γλώσσας. Αν παραλείψετε αυτό το βήμα, η μηχανή θα χρησιμοποιήσει την προεπιλεγμένη γλώσσα της (συνήθως Αγγλικά) και θα χάσετε κείμενο σε άλλες γραφές.

## Βήμα 5: Εκτέλεση Αναγνώρισης OCR

Με όλα έτοιμα, τελικά **αναγνωρίζουμε κείμενο από την εικόνα** και λαμβάνουμε τόσο τη λίστα των ανιχνευμένων γλωσσών όσο και το εξαγόμενο κείμενο.

```java
// Step 5: Run the recognition process
OcrResult result = engine.recognize();

// Display detected languages and the extracted text
System.out.println("Detected languages: " + result.getDetectedLanguages());
System.out.println("Extracted text:\n" + result.getText());
```

Η μέθοδος `getDetectedLanguages()` επιστρέφει μια συλλογή όπως `[en, fr, de]`, επιτρέποντάς σας να επαληθεύσετε ότι η μηχανή εντόπισε σωστά το πολυγλωσσικό περιεχόμενο.

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω βρίσκεται η πλήρης, εκτελέσιμη κλάση Java. Αντιγράψτε την στο `src/main/java/com/example/OcrDemo.java`, προσαρμόστε τη διαδρομή της εικόνας και εκτελέστε `mvn exec:java -Dexec.mainClass="com.example.OcrDemo"`.

```java
package com.example;

import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.ImageStream;
import com.aspose.ocr.OcrResult;

/**
 * Demo program that recognises text from an image,
 * automatically detects languages present, and prints the result.
 */
public class OcrDemo {
    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine
        OcrEngine engine = new OcrEngine();

        // 2️⃣ Load image for OCR – change the path as needed
        String imagePath = "YOUR_DIRECTORY/mixed_languages.png";
        engine.setImage(ImageStream.fromFile(imagePath));

        // 3️⃣ Enable auto language detection so we can detect languages in image
        engine.getRecognitionSettings().setAutoDetectLanguage(true);

        // 4️⃣ Perform the recognition
        OcrResult result = engine.recognize();

        // 5️⃣ Output the findings
        System.out.println("Detected languages: " + result.getDetectedLanguages());
        System.out.println("Extracted text:\n" + result.getText());
    }
}
```

**Αναμενόμενη έξοδος** (οι πραγματικές γλώσσες μπορεί να διαφέρουν):

```
Detected languages: [en, es, fr]
Extracted text:
Hello World!
¡Hola Mundo!
Bonjour le monde!
```

Αν η εικόνα περιέχει μόνο Αγγλικά, η λίστα θα δείχνει `[en]` και το κείμενο θα αντανακλά αυτή τη μοναδική γλώσσα.

## Διαχείριση Συνηθισμένων Edge Cases

| Κατάσταση | Γιατί είναι σημαντικό | Γρήγορη λύση |
|-----------|----------------------|--------------|
| Εικόνα χαμηλής ανάλυσης | Η μηχανή μπορεί να αναγνωρίσει λανθασμένα χαρακτήρες, οδηγώντας σε ακατανόητο αποτέλεσμα. | Προεπεξεργασία της εικόνας (αύξηση DPI, εφαρμογή δυαδικοποίησης) πριν τη δώσετε στο OCR. |
| Μη υποστηριζόμενο σενάριο (π.χ., Bengali) | Η αυτόματη ανίχνευση θα παραλείψει άγνωστα σενάρια, επιστρέφοντας κενό κείμενο για εκείνο το τμήμα. | Προσθέστε χειροκίνητα το πακέτο γλώσσας εάν η βιβλιοθήκη το υποστηρίζει, ή χρησιμοποιήστε διαφορετική μηχανή OCR. |
| Μεγάλο batch εικόνων | Η επανδημιουργία της μηχανής κάθε φορά προσθέτει επιπλέον φόρτο. | Επαναχρησιμοποιήστε ένα ενιαίο αντικείμενο `OcrEngine` και απλώς καλέστε `setImage` για κάθε νέο αρχείο. |
| Περιβάλλον με περιορισμένη μνήμη | Η φόρτωση πολλών εικόνων υψηλής ανάλυσης μπορεί να εξαντλήσει τη μνήμη heap. | Χρησιμοποιήστε `ImageStream.fromFile` με επιλογές streaming ή μειώστε την ανάλυση των εικόνων κατά την πτήση. |

## Pro Tips & Best Practices

- **Cache language packs**: Ορισμένες βιβλιοθήκες OCR επιτρέπουν την προφόρτωση δεδομένων γλώσσας. Αυτό μειώνει την καθυστέρηση όταν επεξεργάζεστε πολλά αρχεία.  
- **Log the detected languages**: Η αποθήκευση της λίστας γλωσσών μαζί με το εξαγόμενο κείμενο βοηθά σε επακόλουθες αναλύσεις (π.χ., ανάλυση συναισθήματος ανά γλώσσα).  
- **Validate the output**: Μια απλή έλεγχος με regex για τα αναμενόμενα σύνολα χαρακτήρων μπορεί να εντοπίσει αποτυχίες OCR νωρίς σε μια αλυσίδα.

## Επόμενα Βήματα

Τώρα που μπορείτε να **αναγνωρίσετε κείμενο από εικόνα** με αυτόματη ανίχνευση γλώσσας, σκεφτείτε να επεκτείνετε τη λύση:

- **Export to PDF**: Τυλίξτε το εξαγόμενο κείμενο σε PDF αναζητήσιμο χρησιμοποιώντας iText ή Apache PDFBox.  
- **Integrate with a database**: Αποθηκεύστε τη διαδρομή της εικόνας, τις ανιχνευμένες γλώσσες και το κείμενο OCR για μελλοντική ανάκτηση.  
- **Add a GUI**: Δημιουργήστε ένα ελαφρύ front‑end Swing ή JavaFX ώστε μη‑τεχνικοί χρήστες να μπορούν να σύρουν εικόνες και να λαμβάνουν άμεσα αποτελέσματα.  

Κάθε ένα από αυτά τα θέματα συνδέεται με τις δευτερεύουσες λέξεις‑κλειδιά—**load image for OCR**, **detect languages in image**, και **enable auto language detection**—οπότε θα συνεχίσετε να χτίζετε πάνω στην ίδια βάση.

---

*Καλή προγραμματιστική! Αν αντιμετωπίσετε κάποιο πρόβλημα, αφήστε ένα σχόλιο παρακάτω και θα το λύσουμε μαζί.*

## Τι Πρέπει να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}