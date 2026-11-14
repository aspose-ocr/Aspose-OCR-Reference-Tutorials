---
category: general
date: 2026-11-14
description: Μάθετε πώς να αναγνωρίζετε κείμενο από PNG σε Java χρησιμοποιώντας το
  Aspose OCR. Ο οδηγός καλύπτει επίσης πώς να εξάγετε κείμενο από εικόνα και να φορτώσετε
  την εικόνα για OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from png
- extract text from image
- convert scanned image to text
- load image for ocr
- read text from image java
language: el
lastmod: 2026-11-14
og_description: Αναγνωρίστε κείμενο από PNG σε Java με το Aspose OCR. Ακολουθήστε
  αυτό το βήμα‑βήμα οδηγό για να εξάγετε κείμενο από εικόνα, να φορτώσετε εικόνα για
  OCR και να διαβάσετε κείμενο από εικόνα σε έργα Java.
og_image_alt: Screenshot of Java console showing recognized text from a PNG file
og_title: Αναγνώριση κειμένου από PNG σε Java – πλήρης οδηγός Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-11-14'
  description: Learn how to recognize text from PNG in Java using Aspose OCR. The
    guide also covers how to extract text from image and load image for OCR.
  headline: How to recognize text from PNG in Java with Aspose OCR
  type: TechArticle
tags:
- Aspose OCR
- Java
- Image processing
title: Πώς να αναγνωρίσετε κείμενο από PNG σε Java με το Aspose OCR
url: /el/java/ocr-operations/how-to-recognize-text-from-png-in-java-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αναγνωρίσετε κείμενο από PNG σε Java με το Aspose OCR

Αν χρειάζεστε **αναγνώριση κειμένου από PNG** αρχεία σε μια εφαρμογή Java, αυτό το tutorial σας παρουσιάζει μια πλήρη, έτοιμη‑για‑εκτέλεση λύση. Στο τέλος του οδηγού θα μπορείτε να **εξάγετε κείμενο από εικόνα**, να μετατρέψετε μια σαρωμένη εικόνα σε κείμενο, και να **φορτώσετε εικόνα για OCR** χρησιμοποιώντας τη βιβλιοθήκη Aspose OCR.

Το παράδειγμα δείχνει επίσης πώς να **διαβάσετε κείμενο από εικόνα Java** κώδικα, ώστε να ενσωματώσετε το OCR σε οποιαδήποτε υπηρεσία backend, εργαλείο επιφάνειας εργασίας ή έργο Android.

## Προαπαιτούμενα

* Java Development Kit (JDK) 8 ή νεότερο εγκατεστημένο.
* Maven ή Gradle για διαχείριση εξαρτήσεων (το παράδειγμα χρησιμοποιεί Maven).
* Αρχείο άδειας Aspose OCR for Java (η δωρεάν αξιολόγηση λειτουργεί για δοκιμές).
* Μια εικόνα με όνομα `input.png` τοποθετημένη σε φάκελο που μπορείτε να αναφέρετε από τον κώδικά σας.

Αυτές οι απαιτήσεις εξασφαλίζουν ότι ο κώδικας θα μεταγλωττιστεί και θα εκτελεστεί χωρίς πρόσθετη ρύθμιση.

## Βήμα 1: Προσθέστε το Aspose OCR στο έργο σας

Προσθέστε το Maven artifact του Aspose OCR στο `pom.xml` σας. Αυτό θα φέρει όλες τις απαραίτητες κλάσεις, συμπεριλαμβανομένων των `OcrEngine` και `ImageStream`.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version>
</dependency>
```

> **Συμβουλή:** Χρησιμοποιήστε τον πιο πρόσφατο αριθμό έκδοσης (ελέγξτε το Maven Central) για να επωφεληθείτε από βελτιώσεις απόδοσης και νέα υποστήριξη γλωσσών.

## Βήμα 2: Φορτώστε την εικόνα PNG για OCR

Η μηχανή OCR λειτουργεί με ένα `ImageStream`. Πρέπει να την κατευθύνετε στην ακριβή θέση του αρχείου PNG που θέλετε να επεξεργαστείτε.

```java
// Load the PNG image that contains the text you want to recognize
String imagePath = "YOUR_DIRECTORY/input.png";
ImageStream imageStream = ImageStream.fromFile(imagePath);
ocrEngine.setImage(imageStream);
```

*Γιατί είναι σημαντικό*: Η σωστή φόρτωση της εικόνας αποτρέπει το κοινό σφάλμα “OCR failed” που προκαλείται από μη υποστηριζόμενη μορφή ή ελλιπή διαδρομή αρχείου.

## Βήμα 3: Δημιουργία και ρύθμιση της μηχανής OCR

Δημιουργήστε ένα αντικείμενο `OcrEngine` και προαιρετικά προσαρμόστε τη γλώσσα ή τις ρυθμίσεις αναγνώρισης. Η προεπιλεγμένη διαμόρφωση λειτουργεί για εκτυπωμένο κείμενο στα Αγγλικά, αλλά μπορείτε να αλλάξετε `ocrEngine.setLanguage(Language.French)` για άλλες γλώσσες.

```java
// Step 3: Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Optional: set recognition language (default is English)
// ocrEngine.setLanguage(Language.English);
```

## Βήμα 4: Εκτέλεση της διαδικασίας OCR

Η κλήση του `process()` εκτελεί το βαριά έργο—σάρωση της εικόνας, τμηματοποίηση χαρακτήρων και μετατροπή τους σε κείμενο Unicode.

```java
// Step 4: Execute the OCR operation
boolean success = ocrEngine.process();
```

Αν το `process()` επιστρέψει `true`, η μηχανή έχει μετατρέψει επιτυχώς **σαρωμένη εικόνα σε κείμενο**. Διαφορετικά, ελέγξτε την έξοδο της κονσόλας για διαγνωστικά μηνύματα.

## Βήμα 5: Ανάκτηση και εμφάνιση του αναγνωρισμένου κειμένου

Όταν το OCR είναι επιτυχές, μπορείτε να λάβετε το πλήρες κείμενο με `getText()`. Αυτό αποτελεί τον πυρήνα της λειτουργίας **read text from image Java**.

```java
if (success) {
    System.out.println("Recognized text:");
    System.out.println(ocrEngine.getText());
} else {
    System.err.println("OCR failed. Verify the image path and file format.");
}
```

Η κονσόλα τώρα εκτυπώνει τους ακριβείς χαρακτήρες που εμφανίστηκαν στο `input.png`. Μπορείτε να επεξεργαστείτε περαιτέρω τη συμβολοσειρά—να την αποθηκεύσετε σε βάση δεδομένων, να τη δώσετε σε ευρετήριο αναζήτησης ή να εκτελέσετε ανάλυση φυσικής γλώσσας.

## Πλήρες, εκτελέσιμο παράδειγμα

Συνδυάζοντας όλα τα βήματα δημιουργείται μια μοναδική, αυτόνομη κλάση. Αντιγράψτε τον κώδικα παρακάτω σε ένα αρχείο με όνομα `SimpleOcrDemo.java`, αντικαταστήστε το `YOUR_DIRECTORY` με την απόλυτη ή σχετική διαδρομή προς το PNG σας, και τρέξτε το με `mvn exec:java`.

```java
import com.aspose.ocr.*;

public class SimpleOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image to be processed
        String imagePath = "YOUR_DIRECTORY/input.png";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 3: Run the OCR process
        if (ocrEngine.process()) {
            // Step 4: Retrieve and display the recognized text
            System.out.println("Recognized text:");
            System.out.println(ocrEngine.getText());
        } else {
            System.err.println("OCR failed. Check the image path and format.");
        }
    }
}
```

**Αναμενόμενη έξοδος** (παράδειγμα για ένα απλό PNG “Hello World”):

```
Recognized text:
Hello World
```

Αν η εικόνα περιέχει πολλαπλές γραμμές, η μηχανή διατηρεί τις αλλαγές γραμμής, καθιστώντας την επεξεργασία μετά το OCR απλή.

## Διαχείριση κοινών περιπτώσεων άκρων

| Κατάσταση | Προτεινόμενη ενέργεια |
|-----------|-----------------------|
| **Η εικόνα δεν είναι PNG** | Μετατρέψτε το αρχείο σε PNG ή χρησιμοποιήστε `ImageStream.fromFile` με υποστηριζόμενη μορφή (BMP, JPEG, TIFF). |
| **Σάρωση χαμηλής ανάλυσης** | Αυξήστε το DPI πριν το OCR (`ocrEngine.setResolution(300)`) για βελτίωση της ακρίβειας. |
| **Κείμενο μη‑Αγγλικής γλώσσας** | Καλέστε `ocrEngine.setLanguage(Language.<YourLanguage>)` και βεβαιωθείτε ότι το πακέτο γλώσσας είναι εγκατεστημένο. |
| **Μεγάλο batch αρχείων** | Επαναχρησιμοποιήστε ένα μόνο αντικείμενο `OcrEngine` και καλέστε επανειλημμένα το `setImage` για αποφυγή επαναλαμβανόμενης αρχικοποίησης. |

Αυτές οι συμβουλές σας βοηθούν να **εξάγετε κείμενο από εικόνα** αξιόπιστα από διάφορες πηγές.

## Σκέψεις απόδοσης

- **Ασφάλεια νήματος** – Το `OcrEngine` δεν είναι thread‑safe. Δημιουργήστε ξεχωριστό αντικείμενο ανά νήμα αν σκοπεύετε να επεξεργάζεστε εικόνες ταυτόχρονα.
- **Χρήση μνήμης** – Μεγάλες εικόνες καταναλώνουν περισσότερο heap. Σκεφτείτε να μειώσετε το μέγεθος των εικόνων με `ImageResize` πριν τις περάσετε στη μηχανή.
- **Άδεια** – Η έκδοση αξιολόγησης προσθέτει υδατογράφημα στο κείμενο εξόδου. Αναπτύξτε μια αδειοδοτημένη έκδοση για παραγωγική χρήση.

## Επόμενα βήματα

Τώρα που μπορείτε να **αναγνωρίσετε κείμενο από PNG** αρχεία, ίσως θέλετε να εξερευνήσετε:

- **Επεξεργασία σε batch** – Διατρέξτε έναν φάκελο και γράψτε κάθε αποτέλεσμα OCR σε αρχείο `.txt`.
- **Ενσωμάτωση με Apache Tika** – Συνδυάστε OCR με εξαγωγή μεταδεδομένων για αγωγούς πλήρους κειμένου αναζήτησης.
- **Χρήση Aspose OCR με Spring Boot** – Εκθέστε ένα HTTP endpoint που δέχεται ανεβασμένες εικόνες και επιστρέφει κείμενο κωδικοποιημένο σε JSON.

Αυτές οι επεκτάσεις βασίζονται στις ίδιες βασικές έννοιες που καλύπτονται σε αυτόν τον οδηγό.

---

*Έχετε μάθει πώς να φορτώσετε μια εικόνα για OCR, να μετατρέψετε μια σαρωμένη εικόνα σε κείμενο και να διαβάσετε κείμενο από εικόνα Java κώδικα χρησιμοποιώντας το Aspose OCR. Εφαρμόστε το μοτίβο σε άλλες μορφές εικόνας, γλώσσες και σενάρια ανάπτυξης για να αξιοποιήσετε ισχυρές δυνατότητες αυτοματοποίησης εγγράφων.*

## Τι θα πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε σε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Παράδειγμα Java OCR – Φόρτωση εικόνας και αναγνώριση κειμένου με Aspose](/ocr/english/java/ocr-basics/java-ocr-example-load-image-and-recognize-text-with-aspose/)
- [OCR εικόνας σε batch σε Java – Γρήγορη εξαγωγή κειμένου από αρχεία PNG](/ocr/english/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)
- [Εξαγωγή κειμένου από εικόνα java χρησιμοποιώντας Aspose OCR – οδηγός](/ocr/english/java/advanced-ocr-techniques/extract-text-from-image-with-aspose-ocr-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}