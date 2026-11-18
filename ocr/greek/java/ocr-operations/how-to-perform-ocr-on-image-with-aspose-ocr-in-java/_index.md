---
category: general
date: 2026-09-10
description: Εκτελέστε OCR σε εικόνα χρησιμοποιώντας το Aspose OCR Java. Μάθετε να
  αναγνωρίζετε κείμενο από JPEG, να εξάγετε κείμενο από εικόνα και να μετατρέπετε
  την εικόνα σε κείμενο αποδοτικά.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- recognize text from JPEG
- extract text from image
- convert image to text
- load image for OCR
language: el
lastmod: 2026-09-10
og_description: Εκτελέστε OCR σε εικόνα με το Aspose OCR Java. Αυτό το σεμινάριο δείχνει
  πώς να αναγνωρίζετε κείμενο από JPEG, να εξάγετε κείμενο από εικόνα και να μετατρέπετε
  την εικόνα σε κείμενο με λίγες γραμμές κώδικα.
og_image_alt: Screenshot of Java code that performs OCR on an image using Aspose OCR
og_title: Εκτελέστε OCR σε εικόνα με το Aspose OCR – Οδηγός Java
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: perform OCR on image using Aspose OCR Java. Learn to recognize text
    from JPEG, extract text from image, and convert image to text efficiently.
  headline: How to perform OCR on image with Aspose OCR in Java
  type: TechArticle
- description: perform OCR on image using Aspose OCR Java. Learn to recognize text
    from JPEG, extract text from image, and convert image to text efficiently.
  name: How to perform OCR on image with Aspose OCR in Java
  steps:
  - name: Prerequisites
    text: '* Java Development Kit (JDK) 8 or later. * Maven or Gradle to manage dependencies
      (the example uses Maven). * A valid Aspose OCR for Java license (or a temporary
      evaluation key). * An image file named `sample.jpg` placed in a known directory.'
  - name: Load image for OCR
    text: '```java // Step 1: Load the image you want to process String imagePath
      = "YOUR_DIRECTORY/sample.jpg"; ImageStream imageStream = ImageStream.fromFile(imagePath);
      ```'
  - name: Create and configure the OCR engine
    text: '```java // Step 2: Create an OCR engine instance OcrEngine engine = new
      OcrEngine();'
  - name: Recognize text from JPEG
    text: '```java // Step 3: Attach the image to the engine engine.setImage(imageStream);'
  - name: Extract text from image and output
    text: '```java // Step 5: Output the recognized text System.out.println("=== Recognized
      Text ==="); System.out.println(result.getText()); ```'
  - name: Expected output
    text: 'Assuming `sample.jpg` contains the text “Hello World”, the console will
      display:'
  type: HowTo
tags:
- OCR
- Java
- Aspose
title: Πώς να εκτελέσετε OCR σε εικόνα με το Aspose OCR σε Java
url: /el/java/ocr-operations/how-to-perform-ocr-on-image-with-aspose-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εκτελέσετε OCR σε εικόνα με το Aspose OCR σε Java

Αν χρειάζεστε **να εκτελέσετε OCR σε εικόνα** σε αρχεία σε μια εφαρμογή Java, αυτός ο οδηγός παρέχει μια πλήρη, έτοιμη προς εκτέλεση λύση. Θα δείτε πώς να **αναγνωρίσετε κείμενο από JPEG** αρχεία, **εξάγετε κείμενο από δεδομένα εικόνας** και **μετατρέψετε εικόνα σε κείμενο** χρησιμοποιώντας το σύγχρονο API του Aspose OCR.

Το tutorial περνάει από κάθε απαιτούμενο βήμα — από τη φόρτωση της εικόνας μέχρι την εκτύπωση του αναγνωρισμένου κειμένου — ώστε να μπορείτε να ενσωματώσετε τη λειτουργία OCR χωρίς να ψάχνετε για πρόσθετους πόρους. Δεν απαιτούνται εξωτερικά εργαλεία εκτός από τη βιβλιοθήκη Aspose OCR for Java.

## Τι θα επιτύχετε

Στο τέλος αυτού του άρθρου θα μπορείτε:

* **Να φορτώσετε μια εικόνα για OCR** απευθείας από το σύστημα αρχείων.  
* Να ενεργοποιήσετε την προεπεξεργασία του Aspose OCR (π.χ., denoising) για βελτίωση της ακρίβειας.  
* **Να αναγνωρίσετε κείμενο από JPEG** και άλλες μορφές raster.  
* **Να εξάγετε κείμενο από εικόνα** και να το εμφανίσετε στην κονσόλα.  
* Να κατανοήσετε πώς **να μετατρέψετε εικόνα σε κείμενο** σε ένα παραγωγικά έτοιμο δείγμα κώδικα.

### Προαπαιτούμενα

* Java Development Kit (JDK) 8 ή νεότερο.  
* Maven ή Gradle για διαχείριση εξαρτήσεων (το παράδειγμα χρησιμοποιεί Maven).  
* Ένα έγκυρο license του Aspose OCR for Java (ή προσωρινό κλειδί αξιολόγησης).  
* Ένα αρχείο εικόνας με όνομα `sample.jpg` τοποθετημένο σε γνωστό φάκελο.

> **Pro tip:** Χρησιμοποιήστε JPEG υψηλής ανάλυσης (300 dpi ή περισσότερο) για τα καλύτερα ποσοστά αναγνώρισης.  

## Βήμα 1: Προσθέστε το Aspose OCR στο έργο σας

Αν διαχειρίζεστε τις εξαρτήσεις με Maven, εισάγετε το παρακάτω απόσπασμα στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version>
</dependency>
```

Για Gradle, προσθέστε:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

Αυτές οι συντεταγμένες κατεβάζουν τη νεότερη σταθερή βιβλιοθήκη Aspose OCR, η οποία περιλαμβάνει τις λειτουργίες προεπεξεργασίας που χρησιμοποιούνται αργότερα.

## Εκτέλεση OCR σε εικόνα – βήμα‑βήμα

Οι παρακάτω ενότητες διασπούν το πλήρες πρόγραμμα. Κάθε μπλοκ είναι αυτόνομο κομμάτι που μπορείτε να αντιγράψετε, να επικολλήσετε και να τρέξετε.

### Φόρτωση εικόνας για OCR

```java
// Step 1: Load the image you want to process
String imagePath = "YOUR_DIRECTORY/sample.jpg";
ImageStream imageStream = ImageStream.fromFile(imagePath);
```

*Γιατί είναι σημαντικό:*  
`ImageStream.fromFile` διαβάζει τα ακατέργαστα byte του JPEG και τα προετοιμάζει για τη μηχανή OCR. Η μέθοδος λειτουργεί με οποιαδήποτε μορφή raster υποστηρίζεται από το Aspose OCR, ώστε να μπορείτε να αντικαταστήσετε το JPEG με PNG ή BMP χωρίς αλλαγές κώδικα.

### Δημιουργία και ρύθμιση της μηχανής OCR

```java
// Step 2: Create an OCR engine instance
OcrEngine engine = new OcrEngine();

// Enable preprocessing to improve accuracy (e.g., denoising)
engine.getPreprocessing().setDenoise(true);
```

*Γιατί είναι σημαντικό:*  
Η δημιουργία ενός `OcrEngine` διανέμει τη βασική μηχανή αναγνώρισης. Η ενεργοποίηση της σημαίας **denoise** αφαιρεί οπτικό θόρυβο που συχνά παρεμβαίνει στην ανίχνευση χαρακτήρων, ειδικά σε σαρωμένα JPEG.

### Αναγνώριση κειμένου από JPEG

```java
// Step 3: Attach the image to the engine
engine.setImage(imageStream);

// Step 4: Perform OCR recognition
OcrResult result = engine.recognize();
```

*Γιατί είναι σημαντικό:*  
`engine.setImage` συνδέει τα δεδομένα εικόνας με τη γραμμή επεξεργασίας OCR. `engine.recognize()` εκτελεί τη διαδικασία πλήρους αναγνώρισης, επιστρέφοντας ένα `OcrResult` που περιέχει το εξαγόμενο κείμενο και μετρικές εμπιστοσύνης.

### Εξαγωγή κειμένου από εικόνα και εμφάνιση

```java
// Step 5: Output the recognized text
System.out.println("=== Recognized Text ===");
System.out.println(result.getText());
```

*Γιατί είναι σημαντικό:*  
`result.getText()` παρέχει την αναπαράσταση plain‑text του περιεχομένου της εικόνας. Η εκτύπωση στην κονσόλα δείχνει ότι **η μετατροπή εικόνας σε κείμενο** πέτυχε, και μπορείτε να ανακατευθύνετε αυτή τη συμβολοσειρά σε αρχεία, βάσεις δεδομένων ή downstream services.

## Πλήρες, εκτελέσιμο παράδειγμα

Παρακάτω βρίσκεται η πλήρης κλάση Java που ενσωματώνει όλα τα βήματα. Αντικαταστήστε το `YOUR_DIRECTORY` με την απόλυτη διαδρομή προς το αρχείο JPEG σας.

```java
import com.aspose.ocr.*;

public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Load the image for OCR
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        ImageStream imageStream = ImageStream.fromFile(imagePath);

        // Create and configure the OCR engine
        OcrEngine engine = new OcrEngine();
        engine.getPreprocessing().setDenoise(true); // improve accuracy

        // Attach the image and run recognition
        engine.setImage(imageStream);
        OcrResult result = engine.recognize();

        // Print the extracted text
        System.out.println("=== Recognized Text ===");
        System.out.println(result.getText());
    }
}
```

### Αναμενόμενη έξοδος

Υποθέτοντας ότι το `sample.jpg` περιέχει το κείμενο “Hello World”, η κονσόλα θα εμφανίσει:

```
=== Recognized Text ===
Hello World
```

Αν η εικόνα περιέχει πολλές γραμμές, κάθε γραμμή θα εμφανιστεί στη δική της γραμμή στην έξοδο.

## Συνηθισμένες παραλλαγές και ειδικές περιπτώσεις

| Κατάσταση                                 | Συνιστώμενη προσαρμογή |
|-------------------------------------------|------------------------|
| **JPEG χαμηλής ανάλυσης** (≤150 dpi)      | Αυξήστε `engine.getPreprocessing().setUpsample(true);` ώστε το Aspose να επεκτείνει την εικόνα πριν την αναγνώριση. |
| **Χρωματικό φόντο** (π.χ., σαρωμένες φόρμες) | Ενεργοποιήστε `engine.getPreprocessing().setBinarize(true);` για μετατροπή της εικόνας σε ασπρόμαυρο. |
| **Μη‑λατινικό σύστημα γραφής** (π.χ., Κυριλλικό) | Ορίστε τη γλώσσα: `engine.getLanguage().setLanguage(OcrLanguage.RUSSIAN);`. |
| **Μεγάλη επεξεργασία παρτίδας**           | Επαναχρησιμοποιήστε ένα μόνο αντικείμενο `OcrEngine` για πολλές εικόνες ώστε να μειώσετε το κόστος εκκίνησης. |
| **Ανάγκη βαθμολογιών εμπιστοσύνης**      | Πρόσβαση στο `result.getConfidence()` για τιμές εμπιστοσύνης ανά χαρακτήρα. |

Αυτές οι προσαρμογές δείχνουν πώς μπορείτε **να φορτώσετε εικόνα για OCR** υπό διαφορετικές συνθήκες ενώ εξακολουθείτε να **εκτελείτε OCR σε εικόνα** αξιόπιστα.

## Σκέψεις για την απόδοση

* **Χρήση μνήμης:** Κάθε `ImageStream` κρατά ολόκληρη την εικόνα στη μνήμη. Για πολύ μεγάλα αρχεία (π.χ., >10 MB), σκεφτείτε τη ροή της εικόνας σε τμήματα χρησιμοποιώντας `ImageStream.fromByteArray`.  
* **Ασφάλεια νήματος:** Το `OcrEngine` *δεν* είναι thread‑safe. Δημιουργήστε ξεχωριστό αντικείμενο ανά νήμα αν σκοπεύετε να παραλληλοποιήσετε εργασίες OCR.  
* **Λειτουργία άδειας:** Η λειτουργία αξιολόγησης περιορίζει τον αριθμό σελίδων που επεξεργάζονται ανά συνεδρία. Αναπτύξτε μια αδειοδοτημένη έκδοση για παραγωγικά φορτία εργασίας.

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **εκτελέσετε OCR σε εικόνα** σε αρχεία Java χρησιμοποιώντας το Aspose OCR. Το tutorial κάλυψε τη φόρτωση εικόνας, την ενεργοποίηση προεπεξεργασίας, την αναγνώριση κειμένου από JPEG, την εξαγωγή του κειμένου και τη μετατροπή της εικόνας σε κείμενο — όλα σε ένα σύντομο πρόγραμμα.

Από εδώ μπορείτε να εξερευνήσετε συναφή θέματα όπως **αναγνώριση κειμένου από JPEG** μαζικά, να ενσωματώσετε το αποτέλεσμα σε ευρετήριο αναζήτησης ή να συνδυάσετε OCR με επεξεργασία φυσικής γλώσσας για πιο έξυπνες ροές εγγράφων. Πειραματιστείτε με τις επιλογές προεπεξεργασίας για να πετύχετε τη βέλτιστη ακρίβεια για τις συγκεκριμένες πηγές εικόνας σας.

--- 

*Εικόνα που απεικονίζει την έξοδο του κώδικα*  
![perform OCR on image Java example](image-placeholder.png){alt="εκτέλεση OCR σε εικόνα χρησιμοποιώντας Aspose OCR Java"}

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [αναγνώριση κειμένου εικόνας με Aspose OCR – Πλήρης Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Πώς να κάνετε OCR κειμένου εικόνας με γλώσσα χρησιμοποιώντας Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Προεπεξεργασία εικόνας OCR σε Java με Aspose OCR – Βελτιώστε την ακρίβεια & εξάγετε κείμενο](/ocr/english/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}