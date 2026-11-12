---
category: general
date: 2026-09-19
description: Μετατροπή εικόνας σε κείμενο σε Java χρησιμοποιώντας Aspose OCR – ένας
  οδηγός βήμα‑προς‑βήμα για την ανάγνωση κειμένου από εικόνα, τη ρύθμιση OCR εικόνας
  και την αποδοτική αναγνώριση κειμένου εικόνας σε Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert image to text
- read text from image
- how to ocr java
- set image ocr
- recognize text image java
language: el
lastmod: 2026-09-19
og_description: Μετατρέψτε εικόνα σε κείμενο σε Java με το Aspose OCR. Μάθετε πώς
  να κάνετε OCR σε εικόνες Java, να ρυθμίσετε το OCR εικόνας και να διαβάσετε κείμενο
  από την εικόνα με λίγες μόνο γραμμές κώδικα.
og_image_alt: Diagram showing convert image to text workflow in Java
og_title: Μετατροπή εικόνας σε κείμενο σε Java – πλήρες σεμινάριο Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-09-19'
  description: convert image to text in Java using Aspose OCR – a step‑by‑step guide
    to read text from image, set image OCR, and recognize text image java efficiently.
  headline: How to convert image to text in Java with Aspose OCR
  type: TechArticle
tags:
- OCR
- Java
- Aspose
- Image processing
title: Πώς να μετατρέψετε εικόνα σε κείμενο σε Java με το Aspose OCR
url: /el/java/ocr-operations/how-to-convert-image-to-text-in-java-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να μετατρέψετε εικόνα σε κείμενο σε Java με Aspose OCR

Αν χρειάζεστε **γρήγορη μετατροπή εικόνας σε κείμενο**, αυτό το tutorial σας δείχνει τον ακριβή κώδικα που μπορείτε να αντιγράψετε‑επικολλήσετε σε οποιοδήποτε έργο Java. Θα μάθετε πώς να **διαβάζετε κείμενο από αρχεία εικόνας** χρησιμοποιώντας τη βιβλιοθήκη Aspose OCR, να ορίσετε την εικόνα για OCR και να ανακτήσετε το αναγνωρισμένο string — όλα σε λιγότερο από δέκα γραμμές κώδικα.

Θα καλύψουμε όλα όσα χρειάζεστε: τις απαιτούμενες εξαρτήσεις, ένα πλήρες εκτελέσιμο παράδειγμα, κοινά προβλήματα και συμβουλές για επεξεργασία διαφορετικών μορφών εικόνας. Στο τέλος, θα μπορείτε να καλέσετε `engine.recognize()` και να λάβετε καθαρό, αναζητήσιμο κείμενο από οποιοδήποτε αρχείο PNG, JPEG ή BMP.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* Java 8 ή νεότερη εγκατεστημένη (ο κώδικας λειτουργεί σε οποιοδήποτε JDK 8+).
* Maven ή Gradle για διαχείριση εξαρτήσεων (το παράδειγμα χρησιμοποιεί Maven).
* Ένα αρχείο εικόνας (π.χ. `sample.png`) που θέλετε να επεξεργαστείτε.
* Ένα έγκυρο άδεια χρήσης Aspose OCR (η δωρεάν αξιολόγηση λειτουργεί για δοκιμές).

## Ρύθμιση έργου και προσθήκη εξάρτησης Aspose OCR

Προσθέστε τη βιβλιοθήκη Aspose OCR στο `pom.xml`. Η χρήση του Maven διατηρεί το classpath καθαρό και εξασφαλίζει ότι λαμβάνετε πάντα την πιο πρόσφατη σταθερή έκδοση.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check Maven Central for the newest version -->
</dependency>
```

Αν προτιμάτε Gradle, η αντίστοιχη εγγραφή είναι:

```gradle
implementation 'com.aspose:aspose-ocr:23.10'
```

> **Συμβουλή:** Αποθηκεύστε το αρχείο άδειας (`Aspose.OCR.lic`) στο φάκελο `resources` και φορτώστε το κατά την εκκίνηση της εφαρμογής για να αποφύγετε το υδατογράφημα αξιολόγησης.

## Πώς να μετατρέψετε εικόνα σε κείμενο σε Java χρησιμοποιώντας Aspose OCR

Αυτή η ενότητα περνάει βήμα‑βήμα από κάθε γραμμή κώδικα που απαιτείται για **ορισμό εικόνας OCR**, **αναγνώριση κειμένου εικόνας java**, και τελικά **ανάγνωση κειμένου από εικόνα**.

```java
package com.aspose.ocr.examples;

import com.aspose.ocr.*;

public class SimpleOcrExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Step 2: Load the image you want to process
        // The ImageStream.fromFile method reads the file into a stream that the engine can use.
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.png"));

        // Step 3: Perform OCR on the loaded image
        OcrResult result = engine.recognize();

        // Step 4: Retrieve and display the recognized text
        System.out.println(result.getText());
    }
}
```

### Επεξήγηση κάθε βήματος

| Βήμα | Τι κάνει | Γιατί είναι σημαντικό |
|------|----------|-----------------------|
| **Δημιουργία μηχανής OCR** | `new OcrEngine()` δημιουργεί το βασικό αντικείμενο που διαχειρίζεται όλες τις λειτουργίες OCR. | Η μηχανή περιλαμβάνει τους αλγόριθμους αναγνώρισης και τις επιλογές ρυθμίσεων. |
| **Ορισμός της εικόνας** | `engine.setImage(ImageStream.fromFile(...))` λέει στη μηχανή ποιο bitmap θα αναλύσει. | Χωρίς ορισμό εικόνας, το `recognize()` δεν θα έχει τίποτα να επεξεργαστεί· αυτή είναι η λειτουργία **set image OCR**. |
| **Αναγνώριση** | `engine.recognize()` εκτελεί τον αλγόριθμο OCR και επιστρέφει ένα `OcrResult`. | Αυτό είναι η καρδιά του **how to OCR Java** – η βιβλιοθήκη σαρώνει τα pixel και δημιουργεί μια αναπαράσταση κειμένου. |
| **Ανάγνωση του κειμένου** | `result.getText()` εξάγει το απλό‑κείμενο string από το αντικείμενο αποτελέσματος. | Σας παρέχει το τελικό **read text from image** αποτέλεσμα που μπορείτε να καταγράψετε, αποθηκεύσετε ή να αναζητήσετε. |

### Αναμενόμενη έξοδος

Αν το `sample.png` περιέχει τις λέξεις “Hello World”, η κονσόλα θα εμφανίσει:

```
Hello World
```

Η έξοδος είναι απλό κείμενο Unicode, ώστε να μπορείτε να το τροφοδοτήσετε απευθείας σε βάσεις δεδομένων, ευρετήρια αναζήτησης ή περαιτέρω pipelines επεξεργασίας φυσικής γλώσσας.

## Βήμα 1: Ρυθμίστε σωστά την εικόνα (set image OCR)

Η μηχανή OCR δέχεται πολλές πηγές εικόνας: αρχεία, streams ή ακατέργαστους πίνακες byte. Για τις περισσότερες περιπτώσεις, το `ImageStream.fromFile` είναι το πιο απλό. Αν χρειαστεί να φορτώσετε μια εικόνα από δικτυακή τοποθεσία, τυλίξτε το `InputStream` σε `ImageStream.fromStream`.

```java
// Load from a URL (example)
try (InputStream urlStream = new URL("https://example.com/image.jpg").openStream()) {
    engine.setImage(ImageStream.fromStream(urlStream));
}
```

> **Κοινό πρόβλημα:** Εικόνες μεγαλύτερες από 4 MB μπορεί να προκαλέσουν πίεση μνήμης. Αλλάξτε το μέγεθος ή συμπιέστε τις πριν καλέσετε `setImage`.

## Βήμα 2: Επιλέξτε τη σωστή γλώσσα (how to ocr java)

Η Aspose OCR υποστηρίζει πολλές γλώσσες έτοιμες προς χρήση. Από προεπιλογή χρησιμοποιεί τα Αγγλικά, αλλά μπορείτε να μεταβείτε σε άλλη γλώσσα ρυθμίζοντας την ιδιότητα `Language`.

```java
engine.setLanguage(Language.French); // Recognize French text
```

Αν χρειάζεστε πολυγλωσσική υποστήριξη, ενεργοποιήστε τη δυνατότητα `AutoDetect`:

```java
engine.setAutoDetect(true);
```

## Βήμα 3: Λεπτομερής ρύθμιση παραμέτρων αναγνώρισης (recognize text image java)

Η μηχανή εκθέτει πολλές ιδιότητες για βελτίωση της ακρίβειας σε θορυβώδεις εικόνες:

```java
engine.getRecognitionParameters().setNoiseRemoval(true);
engine.getRecognitionParameters().setDeskew(true);
engine.getRecognitionParameters().setContrast(1.2f);
```

Αυτές οι ρυθμίσεις είναι ιδιαίτερα χρήσιμες όταν δουλεύετε με σαρωμένα έγγραφα ή φωτογραφίες που λήφθηκαν σε φτωχή φωτισμό.

## Βήμα 4: Ασφαλής διαχείριση του αποτελέσματος (read text from image)

Το `OcrResult` μπορεί να περιέχει κενά strings αν η μηχανή δεν βρει αναγνωρίσιμους χαρακτήρες. Πάντα ελέγχετε για `null` ή κενά αποτελέσματα πριν χρησιμοποιήσετε το κείμενο.

```java
String extracted = result.getText();
if (extracted == null || extracted.isBlank()) {
    System.err.println("No text detected – try adjusting image quality or OCR parameters.");
} else {
    System.out.println("Extracted text:\n" + extracted);
}
```

## Ακραίες περιπτώσεις και βέλτιστες πρακτικές

| Κατάσταση | Προτεινόμενη προσέγγιση |
|-----------|------------------------|
| **Περιστρεφόμενη εικόνα** | Ενεργοποιήστε το `Deskew` (`engine.getRecognitionParameters().setDeskew(true)`). |
| **Σάρωση χαμηλής αντίθεσης** | Αυξήστε την αντίθεση (`setContrast`) ή εφαρμόστε δυαδικό κατώφλι πριν το OCR. |
| **PDF πολλαπλών σελίδων** | Μετατρέψτε κάθε σελίδα σε εικόνα πρώτα, έπειτα κάντε βρόχο με `engine.setImage` για κάθε σελίδα. |
| **Μεγάλο batch** | Επαναχρησιμοποιήστε ένα μόνο αντικείμενο `OcrEngine`; η δημιουργία νέας μηχανής ανά εικόνα προσθέτει επιπλέον κόστος. |
| **Δεν έχει οριστεί άδεια** | Η δωρεάν αξιολόγηση προσθέτει υδατογράφημα στο αποτέλεσμα· φορτώστε την άδειά σας νωρίς (`License lic = new License(); lic.setLicense("Aspose.OCR.lic");`). |

## Πλήρες εκτελέσιμο παράδειγμα

Παρακάτω βρίσκεται μια αυτόνομη κλάση Java που μπορείτε να μεταγλωττίσετε και να εκτελέσετε απευθείας (υπόθεση ότι το Maven έχει κατεβάσει το JAR της Aspose OCR).

```java
package com.aspose.ocr.examples;

import com.aspose.ocr.*;
import java.io.InputStream;
import java.net.URL;

public class SimpleOcrExample {
    public static void main(String[] args) throws Exception {
        // Load license (optional for evaluation)
        // new License().setLicense("Aspose.OCR.lic");

        // 1️⃣ Create OCR engine
        OcrEngine engine = new OcrEngine();

        // 2️⃣ Set image – replace with your own path or URL
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.png"));
        // Example for URL:
        // try (InputStream stream = new URL("https://example.com/image.jpg").openStream()) {
        //     engine.setImage(ImageStream.fromStream(stream));
        // }

        // 3️⃣ Optional: improve accuracy
        engine.getRecognitionParameters().setNoiseRemoval(true);
        engine.getRecognitionParameters().setDeskew(true);
        engine.getRecognitionParameters().setContrast(1.2f);

        // 4️⃣ Recognize text
        OcrResult result = engine.recognize();

        // 5️⃣ Display the result
        String text = result.getText();
        if (text == null || text.isBlank()) {
            System.err.println("No text detected – adjust image quality or OCR settings.");
        } else {
            System.out.println("Recognized text:");
            System.out.println(text);
        }
    }
}
```

Η εκτέλεση του προγράμματος εκτυπώνει το εξαγόμενο string στην κονσόλα, ολοκληρώνοντας τη ροή **convert image to text**.

![convert image to text workflow in Java](image-placeholder.png){: .align-center alt="Ροή εργασίας μετατροπής εικόνας σε κείμενο σε Java"}

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **μετατρέψετε εικόνα σε κείμενο** σε Java χρησιμοποιώντας Aspose OCR, από τον ορισμό της εικόνας (`set image OCR`) μέχρι την κλήση του `recognize()` και τελικά την **ανάγνωση κειμένου από εικόνα**. Το παράδειγμα παρουσιάζει τα βασικά βήματα — δημιουργία μηχανής, φόρτωση εικόνας, ρύθμιση παραμέτρων αναγνώρισης και διαχείριση του αποτελέσματος — ενώ καλύπτει και τις πιο συχνές ακραίες περιπτώσεις.

Έτοιμοι για επόμενο βήμα; Σκεφτείτε:

* Ενσωμάτωση του αποτελέσματος OCR με Apache Lucene για αναζητήσιμα έγγραφα.
* Επεξεργασία PDF πολλαπλών σελίδων μετατρέποντας κάθε σελίδα σε εικόνα πρώτα.
*


## Τι Θα Μάθετε Στη Σειρά Επόμενη;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Read Text from an Image in Java Using Aspose OCR – Complete Guide](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [image to text java: Convert Image to Text with Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}