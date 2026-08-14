---
category: general
date: 2026-07-05
description: Μετατρέψτε εικόνα σε κείμενο με Java χρησιμοποιώντας το Aspose OCR. Μάθετε
  πώς να εξάγετε κείμενο από σάρωση, αρχεία TIFF και ροές γρήγορα και αξιόπιστα.
draft: false
keywords:
- convert image to text
- extract text from scan
- extract text from tif
- recognize text from stream
- how to ocr stream
language: el
og_description: Μετατρέψτε εικόνα σε κείμενο με το Aspose OCR σε Java. Αυτός ο οδηγός
  δείχνει πώς να εξάγετε κείμενο από σάρωση, αρχεία TIFF και ροές, καλύπτοντας κάθε
  βήμα από τη ρύθμιση έως την έξοδο.
og_title: Μετατροπή εικόνας σε κείμενο σε Java – Πλήρης οδηγός Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Convert image to text with Java using Aspose OCR. Learn how to extract
    text from scan, TIFF files, and streams quickly and reliably.
  headline: Convert Image to Text in Java Using Aspose OCR – Full Guide
  type: TechArticle
tags:
- Java
- OCR
- Aspose
title: Μετατροπή εικόνας σε κείμενο σε Java χρησιμοποιώντας Aspose OCR – Πλήρης οδηγός
url: /el/java/ocr-operations/convert-image-to-text-in-java-using-aspose-ocr-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή Εικόνας σε Κείμενο σε Java Χρησιμοποιώντας Aspose OCR – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ πώς να **convert image to text** χωρίς να παλεύετε με τεχνάσματα επεξεργασίας εικόνας χαμηλού επιπέδου; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν δυσκολίες όταν πρέπει να εξάγουν κείμενο από αρχεία σάρωσης ή μεγάλα έγγραφα TIFF, ειδικά όταν η πηγή προέρχεται από ροή (stream) αντί για απλό μονοπάτι αρχείου.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα μια πρακτική, ολοκληρωμένη λύση που **extracts text from scan** εικόνες, διαχειρίζεται **extract text from tif** αρχεία, και σας δείχνει ακριβώς **how to ocr stream** δεδομένα χρησιμοποιώντας τη βιβλιοθήκη Aspose OCR για Java. Στο τέλος, θα έχετε ένα επαναχρησιμοποιήσιμο snippet που εκτυπώνει το αναγνωρισμένο κείμενο απευθείας στην κονσόλα.

## Τι Θα Χρειαστείτε

- **Java Development Kit (JDK) 8 ή νεότερο** – ο κώδικας εκτελείται σε οποιοδήποτε πρόσφατο JDK.
- **Maven ή Gradle** (το αγαπημένο σας εργαλείο κατασκευής) για να προσθέσετε την εξάρτηση Aspose OCR.
- Ένα αρχείο εικόνας – προτιμότερα ένα πολυ‑σελίδων **TIFF** (`large_image.tif`) που θέλετε να δοκιμάσετε.
- Μια μέτρια ποσότητα υπομονής (απλώς αστειεύομαι – τα βήματα είναι αρκετά γρήγορα).

Αν κάποιο από αυτά σας φαίνεται άγνωστο, μην ανησυχείτε. Θα καλύψουμε τη ρύθμιση Maven στο πρώτο βήμα, και το υπόλοιπο είναι καθαρή Java.

## Βήμα 1: Προσθήκη Aspose OCR στο Έργο Σας

Το πρώτο εμπόδιο είναι η προσθήκη της μηχανής OCR στην classpath σας. Η Aspose δημοσιεύει τις βιβλιοθήκες της στο Maven Central, ώστε να μπορείτε να προσθέσετε μια μόνο εξάρτηση.

```xml
<!-- pom.xml -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.9</version> <!-- Use the latest stable version -->
    </dependency>
</dependencies>
```

> **Pro tip:** Αν χρησιμοποιείτε Gradle, το ισοδύναμο είναι  
> `implementation 'com.aspose:aspose-ocr:23.9'`.  
> Αυτή η μικρή προσθήκη σας δίνει πρόσβαση σε `OcrEngine`, `RecognitionResult`, και όλη τη βαριά δουλειά στο παρασκήνιο.

## Βήμα 2: Αρχικοποίηση της Μηχανής OCR

Τώρα που η βιβλιοθήκη είναι έτοιμη, μπορούμε να δημιουργήσουμε μια παρουσία του `OcrEngine`. Σκεφτείτε τη μηχανή ως τον εγκέφαλο που θα **recognize text from stream** δεδομένα.

```java
import com.aspose.ocr.OcrEngine;

// ...

// Step 2: Initialize the OCR engine – this is where the magic starts.
OcrEngine engine = new OcrEngine();
```

Γιατί δημιουργούμε την μηχανή μία φορά; Η επαναχρησιμοποίηση του ίδιου αντικειμένου `OcrEngine` για πολλαπλές εικόνες μειώνει το κόστος και βελτιώνει την απόδοση, ειδικά όταν επεξεργαζόμαστε μια παρτίδα σελίδων σάρωσης.

## Βήμα 3: Άνοιγμα της Εικόνας Σας ως Ροή (Stream)

Οι περισσότερες πραγματικές περιπτώσεις περιλαμβάνουν ανάγνωση εικόνων από δικτυακή τοποθεσία, βάση δεδομένων ή ανεβασμένο αρχείο – όλα αυτά εμφανίζονται ως ροές. Εδώ είναι πώς μπορείτε να **recognize text from stream** χωρίς να αγγίξετε άμεσα το σύστημα αρχείων.

```java
import java.io.FileInputStream;
import java.io.InputStream;

// ...

// Step 3: Load the image (a TIFF in this case) as an InputStream.
try (InputStream imageStream = new FileInputStream("YOUR_DIRECTORY/large_image.tif")) {
    // The try‑with‑resources block ensures the stream closes automatically.
```

Αν η πηγή σας είναι ένα `ByteArrayInputStream` ή ένα `InputStream` από αίτημα servlet, απλώς αντικαταστήστε τον κατασκευαστή `FileInputStream` – το υπόλοιπο του κώδικα παραμένει ίδιο.

## Βήμα 4: Εκτέλεση OCR και Εξαγωγή Κειμένου

Με τη ροή στα χέρια, καλούμε το `engine.recognizeImage`. Αυτή η μέθοδος επιστρέφει ένα αντικείμενο `RecognitionResult` που περιέχει το εξαγόμενο κείμενο.

```java
import com.aspose.ocr.RecognitionResult;

// ...

    // Step 4: Recognize text from the image stream
    RecognitionResult ocrResult = engine.recognizeImage(imageStream);

    // Step 5: Print the extracted text to the console
    System.out.println("=== OCR Output ===");
    System.out.println(ocrResult.getText());
}
```

Παρατηρήστε πώς η κλήση στο `recognizeImage` κάνει όλη τη βαριά δουλειά: αποκωδικοποιεί το TIFF, εκτελεί τη μηχανή OCR και επιστρέφει το απλό κείμενο. Αυτό είναι ο πυρήνας της λειτουργικότητας **convert image to text**.

## Βήμα 5: Διαχείριση Πολυ‑Σελίδων TIFF (Προαιρετικό)

Αν το TIFF σας περιέχει πολλαπλές σελίδες, το Aspose OCR θα συνενώσει το κείμενο από κάθε σελίδα αυτόματα. Ωστόσο, μπορεί να θέλετε να διαχωρίσετε τις σελίδες για ευκολία ανάγνωσης. Εδώ είναι μια γρήγορη τροποποίηση:

```java
String fullText = ocrResult.getText();
String[] pages = fullText.split("\\f"); // Form feed character denotes page break

for (int i = 0; i < pages.length; i++) {
    System.out.println("--- Page " + (i + 1) + " ---");
    System.out.println(pages[i].trim());
}
```

Αυτό το snippet **extracts text from scan** έγγραφα σελίδα προς σελίδα, δίνοντάς σας λεπτομερή έλεγχο του αποτελέσματος.

## Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας όλα, εδώ είναι μια πλήρης, έτοιμη‑για‑εκτέλεση κλάση που μπορείτε να αντιγράψετε στο IDE σας.

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.RecognitionResult;
import java.io.FileInputStream;
import java.io.InputStream;

public class StreamOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // Step 2: Open the image file as a stream
        try (InputStream imageStream = new FileInputStream("YOUR_DIRECTORY/large_image.tif")) {

            // Step 3: Recognize text from the image stream
            RecognitionResult ocrResult = engine.recognizeImage(imageStream);

            // Step 4: Print the extracted text
            System.out.println("=== OCR Output ===");
            System.out.println(ocrResult.getText());

            // Optional: Separate pages if it's a multi‑page TIFF
            String[] pages = ocrResult.getText().split("\\f");
            for (int i = 0; i < pages.length; i++) {
                System.out.println("--- Page " + (i + 1) + " ---");
                System.out.println(pages[i].trim());
            }
        }
    }
}
```

**Αναμενόμενη έξοδος** (συντομευμένη για συντομία):

```
=== OCR Output ===
This is the first line of the scanned document.
Another line follows...
--- Page 1 ---
This is the first line of the scanned document.
...
```

Αν η εικόνα είναι θολή ή η γλώσσα δεν είναι Αγγλικά, μπορείτε να ρυθμίσετε το `engine.setLanguage` ή να προσαρμόσετε τις επιλογές προεπεξεργασίας – αλλά η βασική ροή παραμένει η ίδια.

## Συνηθισμένα Προβλήματα & Πώς να τα Αποφύγετε

| Συμπτωμα | Πιθανή Αιτία | Διόρθωση |
|---------|--------------|-----|
| `NullPointerException` on `ocrResult.getText()` | Η μηχανή δεν έχει αρχικοποιηθεί ή η ροή εικόνας κλείστηκε πρόωρα | Βεβαιωθείτε ότι το `OcrEngine` δημιουργείται **πριν** το άνοιγμα της ροής και διατηρήστε τη ροή ανοιχτή μέχρι να επιστρέψει το `recognizeImage`. |
| Παραμορφωμένοι χαρακτήρες | DPI εικόνας πολύ χαμηλό (κάτω από 300) | Χρησιμοποιήστε πηγή υψηλότερης ανάλυσης ή ενεργοποιήστε τη βελτίωση εικόνας της Aspose (`engine.getImagePreprocessingOptions().setDpi(300)`). |
| Καμία έξοδος για πολυ‑σελίδες TIFF | Το αποτέλεσμα δεν χωρίζεται σωστά | Χρησιμοποιήστε `\\f` (form feed) όπως φαίνεται παραπάνω για διαχωρισμό σελίδων. |
| `OutOfMemoryError` σε τεράστια αρχεία | Φόρτωση ολόκληρου του αρχείου στη μνήμη | Επεξεργαστείτε το TIFF σελίδα‑με‑σελίδα χρησιμοποιώντας `engine.recognizeImage(pageStream)` μέσα σε βρόχο. |

## Bonus: Μετατροπή του Αποτελέσματος σε Αρχείο Κειμένου

Αν χρειάζεστε να **convert image to text** και να το αποθηκεύσετε για μελλοντική χρήση, προσθέστε μερικές γραμμές:

```java
import java.nio.file.Files;
import java.nio.file.Paths;

// ...

String outputPath = "output.txt";
Files.write(Paths.get(outputPath), ocrResult.getText().getBytes());
System.out.println("Text saved to " + outputPath);
```

## Συμπέρασμα

Μόλις μάθατε πώς να **convert image to text** σε Java χρησιμοποιώντας Aspose OCR, καλύπτοντας τα πάντα από αρχεία **extract text from scan** έως εικόνες **extract text from tif**, και κυριαρχώντας στις τεχνικές **recognize text from stream**. Το πλήρες παράδειγμα δείχνει τα ακριβή βήματα που χρειάζεστε για να τρέξετε σήμερα, και τα προαιρετικά snippets σας δείχνουν πώς να διαχειριστείτε πολυ‑σελίδες έγγραφα ή να αποθηκεύσετε τα αποτελέσματα στο δίσκο.

Τι ακολουθεί; Δοκιμάστε να τροφοδοτήσετε τη μηχανή OCR με PDF, πειραματιστείτε με τις ρυθμίσεις γλώσσας, ή ενσωματώστε το αποτέλεσμα σε ευρετήριο αναζήτησης. Το ίδιο μοτίβο λειτουργεί για δεδομένα **how to ocr stream** που προέρχονται από ανεβάσματα στο web, αποθήκευση στο cloud, ή ακόμη και από ουρά μηνυμάτων.

Έχετε ερωτήσεις ή μια δύσκολη εικόνα που δεν συνεργάζεται; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική! 

![Διάγραμμα που δείχνει τη ροή από αρχείο εικόνας → InputStream → OcrEngine → Έξοδο κειμένου – convert image to text](https://example.com/convert-image-to-text-diagram.png "διάγραμμα ροής convert image to text")

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε σε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to extract text from tiff with Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}