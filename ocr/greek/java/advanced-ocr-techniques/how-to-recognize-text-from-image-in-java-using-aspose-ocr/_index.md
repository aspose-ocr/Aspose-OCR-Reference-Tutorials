---
category: general
date: 2026-09-29
description: Μάθετε πώς να αναγνωρίζετε κείμενο από εικόνα με Java και Aspose OCR.
  Αυτός ο οδηγός δείχνει επίσης πώς να εξάγετε κείμενο από jpg και πώς να βελτιώσετε
  την ακρίβεια του OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from image
- extract text from jpg
- how to improve OCR accuracy
- Aspose OCR Java
- Java image processing
language: el
lastmod: 2026-09-29
og_description: Αναγνωρίστε κείμενο από εικόνα σε Java με το Aspose OCR. Ακολουθήστε
  αυτό το βήμα‑βήμα οδηγό για να εξάγετε κείμενο από jpg και μάθετε πώς να βελτιώσετε
  την ακρίβεια του OCR.
og_image_alt: Java code screenshot that recognizes text from image using Aspose OCR
og_title: Αναγνώριση κειμένου από εικόνα σε Java – πλήρης οδηγός Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Learn how to recognize text from image with Java and Aspose OCR. This
    guide also shows how to extract text from jpg and how to improve OCR accuracy.
  headline: How to recognize text from image in Java using Aspose OCR
  type: TechArticle
- description: Learn how to recognize text from image with Java and Aspose OCR. This
    guide also shows how to extract text from jpg and how to improve OCR accuracy.
  name: How to recognize text from image in Java using Aspose OCR
  steps:
  - name: '**Pre‑process the image** – apply contrast stretching or binarization using
      OpenCV before handing it to Aspose OCR. Cleaner edges give higher confidence.'
    text: '**Pre‑process the image** – apply contrast stretching or binarization using
      OpenCV before handing it to Aspose OCR. Cleaner edges give higher confidence.'
  - name: '**Crop unnecessary margins** – the engine spends time analyzing blank space,
      which can lower the overall confidence score.'
    text: '**Crop unnecessary margins** – the engine spends time analyzing blank space,
      which can lower the overall confidence score.'
  - name: '**Choose the correct language pack** – loading only the languages you need
      speeds up recognition and reduces false positives.'
    text: '**Choose the correct language pack** – loading only the languages you need
      speeds up recognition and reduces false positives.'
  - name: '**Use the latest Aspose OCR version** – each release includes updated neural
      models that improve accuracy out‑of‑the‑box.'
    text: '**Use the latest Aspose OCR version** – each release includes updated neural
      models that improve accuracy out‑of‑the‑box.'
  type: HowTo
tags:
- OCR
- Java
- Aspose
title: Πώς να αναγνωρίσετε κείμενο από εικόνα σε Java χρησιμοποιώντας το Aspose OCR
url: /el/java/advanced-ocr-techniques/how-to-recognize-text-from-image-in-java-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αναγνωρίσετε κείμενο από εικόνα σε Java χρησιμοποιώντας το Aspose OCR

Αν χρειάζεστε **αναγνώριση κειμένου από εικόνα** σε μια εφαρμογή Java, αυτό το tutorial σας παρουσιάζει μια έτοιμη λύση. Θα δείτε πώς να εξάγετε κείμενο από αρχεία jpg, να ενεργοποιήσετε την επιτάχυνση GPU και να εφαρμόσετε διόρθωση ορθογραφίας για να απαντήσετε στην κοινή ερώτηση *πώς να βελτιώσετε την ακρίβεια του OCR*.

Ο οδηγός καλύπτει όλα όσα χρειάζεστε: ρύθμιση Maven, πλήρες πηγαίο κώδικα, εξηγήσεις για κάθε επιλογή διαμόρφωσης και συμβουλές για τη διαχείριση εικόνων χαμηλής ποιότητας. Στο τέλος θα έχετε ένα λειτουργικό πρόγραμμα που εκτυπώνει το αναγνωρισμένο κείμενο στην κονσόλα.

## Προαπαιτούμενα

* Java 17 (ή νεότερη) εγκατεστημένη – το Aspose OCR υποστηρίζει Java 8+ αλλά τα νεότερα runtime προσφέρουν καλύτερη απόδοση.
* Maven 3.8+ για διαχείριση εξαρτήσεων.
* Άδεια Aspose OCR for Java (η δωρεάν δοκιμή λειτουργεί για αξιολόγηση).  
* Μια εικόνα JPG (`sample.jpg`) που περιέχει καθαρό, ευανάγνωστο κείμενο.

Αν λείπει κάτι από αυτά, εγκαταστήστε το JDK από [oracle.com/java](https://www.oracle.com/java/technologies/downloads/) και ακολουθήστε τον οδηγό εγκατάστασης Maven στην ιστοσελίδα της Apache.

## Προσθήκη Aspose OCR στο έργο σας

Δημιουργήστε ένα `pom.xml` (ή προσθέστε σε ένα υπάρχον) και συμπεριλάβετε την εξάρτηση Aspose OCR:

```xml
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>ocr-demo</artifactId>
  <version>1.0.0</version>
  <dependencies>
    <dependency>
      <groupId>com.aspose</groupId>
      <artifactId>aspose-ocr</artifactId>
      <version>23.12</version> <!-- latest stable at time of writing -->
    </dependency>
  </dependencies>
</project>
```

Εκτελέστε `mvn clean compile` για να κατεβάσετε τη βιβλιοθήκη. Η εξάρτηση φέρνει όλα τα εγγενή δυαδικά αρχεία που απαιτούνται για χρήση GPU και διόρθωση ορθογραφίας.

## Βήμα 1: Ρύθμιση της μηχανής OCR για αναγνώριση κειμένου από εικόνα

Το πρώτο που κάνετε είναι να δημιουργήσετε μια παρουσία του `OcrEngine`. Αυτό το αντικείμενο οργανώνει ολόκληρη τη διαδικασία OCR.

```java
// Step 1: Create an OCR engine instance
OcrEngine engine = new OcrEngine();
```

Η δημιουργία της μηχανής δεν φορτώνει ακόμη καμία εικόνα· προετοιμάζει μόνο εσωτερικούς πόρους. Αυτή η διαχωριστική λειτουργία σας επιτρέπει να επαναχρησιμοποιήσετε την ίδια μηχανή για πολλαπλές εικόνες, κάτι χρήσιμο σε σεναρίων παρτίδας.

## Βήμα 2: Ενεργοποίηση επιτάχυνσης GPU για ταχύτερη επεξεργασία

Αν ο υπολογιστής σας διαθέτει συμβατό GPU, η ενεργοποίησή του μπορεί να μειώσει το χρόνο αναγνώρισης έως και 70 %. Αυτό απαντά άμεσα στην ερώτηση *πώς να βελτιώσετε την ακρίβεια του OCR* όσον αφορά την ταχύτητα, κάτι που συχνά σας επιτρέπει να επεξεργάζεστε εικόνες υψηλότερης ανάλυσης χωρίς απώλεια απόδοσης.

```java
// Step 2 (optional): Use GPU if available
engine.getConfiguration().setUseGpu(true);
```

> **Συμβουλή:** Όταν εκτελείτε σε διακομιστή χωρίς οθόνη, βεβαιωθείτε ότι οι οδηγοί CUDA είναι εγκατεστημένοι· διαφορετικά η κλήση επιστρέφει στην CPU χωρίς σφάλμα.

## Βήμα 3: Ενεργοποίηση διόρθωσης ορθογραφίας για βελτίωση της ακρίβειας του OCR

Η διόρθωση ορθογραφίας είναι ένα ελαφρύ μοντέλο γλώσσας που διορθώνει κοινά λάθη αναγνώρισης (π.χ., “l0ve” → “love”). Η ενεργοποίησή της είναι ένας από τους πιο αποτελεσματικούς τρόπους για να απαντήσετε στην ερώτηση *πώς να βελτιώσετε την ακρίβεια του OCR* για τυπωμένο κείμενο.

```java
// Step 3 (optional): Enable spell correction
engine.getConfiguration().setSpellCorrector(true);
```

Αν επεξεργάζεστε σαρωμένα χειρόγραφα σημειώματα, ίσως θελήσετε να απενεργοποιήσετε αυτή τη λειτουργία, καθώς το μοντέλο είναι βελτιστοποιημένο για τυπωμένες γραμματοσειρές.

## Βήμα 4: Φόρτωση της εικόνας JPG από την οποία θέλετε να εξάγετε κείμενο

Τώρα φορτώστε το αρχείο εικόνας. Η βοηθητική μέθοδος `ImageStream.fromFile` δέχεται οποιαδήποτε μορφή υποστηρίζεται από το Aspose OCR, αλλά το παράδειγμα εστιάζει σε JPG επειδή είναι η πιο κοινή μορφή στο web.

```java
// Step 4: Load the image that contains the text to be recognized
engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

**Γιατί JPG;** Η συμπίεση JPEG μπορεί να εισάγει τεχνουργήματα που μπερδεύουν το OCR. Για μέγιστη ακρίβεια, παρέχετε μια εικόνα με DPI τουλάχιστον 300 και αποφύγετε υπερβολική συμπίεση. Αν έχετε PNG ή TIFF, μπορείτε να το περάσετε απευθείας στο `fromFile`; ο ίδιος κώδικας λειτουργεί χωρίς αλλαγές.

## Βήμα 5: Εκτέλεση OCR και ανάκτηση του αναγνωρισμένου κειμένου

Τέλος, καλέστε `recognize()` και εκτυπώστε το αποτέλεσμα. Η μέθοδος επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει το ακατέργαστο κείμενο, τις βαθμολογίες εμπιστοσύνης και τα πλαίσια περιορισμού κάθε λέξης.

```java
// Step 5: Run OCR and get the result
OcrResult result = engine.recognize();
System.out.println("=== Recognized text ===");
System.out.println(result.getText());
```

### Αναμενόμενη έξοδος

```
=== Recognized text ===
Welcome to Aspose OCR demo.
This text was extracted from a JPG image.
```

Αν η έξοδος περιέχει ακατανόητους χαρακτήρες, επανεξετάστε το **Βήμα 3** (διόρθωση ορθογραφίας) και βεβαιωθείτε ότι η εικόνα πληροί την πρόταση DPI.

## Συνηθισμένες παραλλαγές και ειδικές περιπτώσεις

| Κατάσταση | Συνιστώμενη προσαρμογή |
|-----------|------------------------|
| **Εικόνα χαμηλής ανάλυσης (< 150 DPI)** | Αυξήστε την ανάλυση της εικόνας πριν τη δώσετε στη μηχανή ή χρησιμοποιήστε `engine.getConfiguration().setScaleFactor(2.0)` ώστε η μηχανή να κάνει εσωτερική επαναδειγματοληψία. |
| **Έγγραφο πολλαπλών γλωσσών** | Ορίστε `engine.getConfiguration().setLanguage("eng,spa")` για να φορτώσετε λεξικά αγγλικών και ισπανικών. |
| **Μεγάλη παρτίδα αρχείων** | Επαναχρησιμοποιήστε την ίδια παρουσία `OcrEngine`, καλώντας μόνο `engine.setImage(...)` για κάθε νέο αρχείο. Αυτό αποφεύγει την επαναλαμβανόμενη φόρτωση της εγγενούς βιβλιοθήκης. |
| **Περιβάλλον με περιορισμένη μνήμη** | Απενεργοποιήστε το GPU (`setUseGpu(false)`) και τη διόρθωση ορθογραφίας (`setSpellCorrector(false)`) για μείωση της χρήσης RAM. |
| **Εξαγωγή κειμένου από PNG αντί για JPG** | Δεν απαιτείται αλλαγή κώδικα· απλώς δείξτε το `fromFile` σε διαδρομή `.png`. Η βιβλιοθήκη ανιχνεύει αυτόματα τη μορφή. |

## Επαγγελματικές συμβουλές για το πώς να βελτιώσετε την ακρίβεια του OCR

1. **Προεπεξεργασία της εικόνας** – εφαρμόστε τέντωμα αντίθεσης ή δυαδικοποίηση χρησιμοποιώντας OpenCV πριν τη δώσετε στο Aspose OCR. Καθαρές άκρες δίνουν υψηλότερη εμπιστοσύνη.
2. **Κόψτε περιττά περιθώρια** – η μηχανή δαπανά χρόνο στην ανάλυση κενών περιοχών, κάτι που μπορεί να μειώσει τη συνολική βαθμολογία εμπιστοσύνης.
3. **Επιλέξτε το σωστό πακέτο γλώσσας** – η φόρτωση μόνο των γλωσσών που χρειάζεστε επιταχύνει την αναγνώριση και μειώνει τα ψευδώς θετικά.
4. **Χρησιμοποιήστε την πιο πρόσφατη έκδοση του Aspose OCR** – κάθε έκδοση περιλαμβάνει ενημερωμένα νευρωνικά μοντέλα που βελτιώνουν την ακρίβεια αμέσως.

## Πλήρες, εκτελέσιμο παράδειγμα

Παρακάτω βρίσκεται η πλήρης κλάση Java που συνδυάζει όλα τα βήματα. Αποθηκεύστε την ως `SimpleOcr.java`, προσαρμόστε τη διαδρομή της εικόνας και εκτελέστε `mvn exec:java -Dexec.mainClass=SimpleOcr`.

```java
import com.aspose.ocr.*;

public class SimpleOcr {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Step 2: (Optional) Enable GPU acceleration for faster processing
        engine.getConfiguration().setUseGpu(true);

        // Step 3: (Optional) Enable spell correction to improve OCR accuracy
        engine.getConfiguration().setSpellCorrector(true);

        // Step 4: Load the image that contains the text to be recognized
        // This example extracts text from jpg, but any supported format works.
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // Step 5: Perform OCR and retrieve the recognized text
        OcrResult result = engine.recognize();

        System.out.println("=== Recognized text ===");
        System.out.println(result.getText());
    }
}
```

Η εκτέλεση του προγράμματος εκτυπώνει το αναγνωρισμένο κείμενο στην κονσόλα, επιβεβαιώνοντας ότι έχετε μάθει με επιτυχία πώς να **αναγνωρίζετε κείμενο από εικόνα**, πώς να **εξάγετε κείμενο από jpg**, και τις βασικές τεχνικές για **πώς να βελτιώσετε την ακρίβεια του OCR**.

## Συμπέρασμα

Σε αυτό το tutorial μάθατε πώς να **αναγνωρίζετε κείμενο από εικόνα** σε Java με το Aspose OCR, πώς να **εξάγετε κείμενο από jpg**, και αρκετούς πρακτικούς τρόπους για να απαντήσετε στην ερώτηση *πώς να βελτιώσετε την ακρίβεια του OCR*. Η προσέγγιση είναι πλήρως αυτόνομη: χρειάζεστε μόνο την εξάρτηση Maven, ένα αρχείο JPEG και μερικές σημαίες διαμόρφωσης.

Επόμενα βήματα που μπορείτε να εξερευνήσετε:

* Μετατρέψτε το αναγνωρισμένο κείμενο σε PDF αναζητήσιμο χρησιμοποιώντας Aspose PDF.
* Επεξεργαστείτε ολόκληρο φάκελο εικόνων με έναν απλό βρόχο (batch OCR).
* Ενσωματώστε τη μηχανή OCR σε ένα endpoint REST του Spring Boot για επεξεργασία εικόνας κατόπιν ζήτησης.

Μη διστάσετε να πειραματιστείτε με διαφορετικές ποιότητες εικόνας, πακέτα γλώσσας και ρυθμίσεις υλικού για να δείτε πώς κάθε παράγοντας επηρεάζει την απόδοση του OCR. Καλή προγραμματιστική!

## Τι θα πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετικούς θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Προεπεξεργασία εικόνας OCR σε Java με Aspose OCR – Βελτιώστε την ακρίβεια & εξάγετε κείμενο](/ocr/english/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)
- [Πώς να χρησιμοποιήσετε OCR σε Java – Αναγνωρίστε κείμενο από εικόνα γρήγορα](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/)
- [Αναγνώριση κειμένου από εικόνα με Aspose OCR – Πλήρης οδηγός Java](/ocr/english/java/advanced-ocr-techniques/recognize-text-from-image-with-aspose-ocr-full-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}