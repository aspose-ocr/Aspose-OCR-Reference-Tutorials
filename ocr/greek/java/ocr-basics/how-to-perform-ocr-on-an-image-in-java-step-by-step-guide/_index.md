---
category: general
date: 2026-11-17
description: Μάθετε πώς να εκτελείτε OCR σε μια εικόνα με Java και να εξάγετε κείμενο
  από φωτογραφίες χρησιμοποιώντας ένα απλό παράδειγμα κώδικα. Περιλαμβάνει συμβουλές
  για ανάγνωση εικόνας σε Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text image
- read image java
- convert image to text
- image to text java
language: el
lastmod: 2026-11-17
og_description: Πώς να εκτελέσετε OCR σε μια εικόνα σε Java και να εξάγετε κείμενο
  γρήγορα. Ακολουθήστε αυτόν τον οδηγό για να διαβάσετε εικόνα σε Java και να μετατρέψετε
  την εικόνα σε κείμενο με ένα έτοιμο παράδειγμα προς εκτέλεση.
og_image_alt: Screenshot showing Java code that performs OCR on an image
og_title: Πώς να εκτελέσετε OCR σε εικόνα με Java – οδηγός βήμα‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: Learn how to perform OCR on an image in Java and extract text from
    pictures using a simple code example. Includes read image Java tips.
  headline: How to perform OCR on an image in Java – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Java
- Image processing
- Text extraction
title: Πώς να εκτελέσετε OCR σε εικόνα σε Java – βήμα‑βήμα οδηγός
url: /el/java/ocr-basics/how-to-perform-ocr-on-an-image-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εκτελέσετε OCR σε εικόνα με Java – οδηγός βήμα‑βήμα

Αν χρειάζεστε **πώς να εκτελέσετε OCR** σε μια εικόνα, αυτό το tutorial σας δείχνει μια πλήρη, εκτελέσιμη λύση σε Java. Θα δείτε πώς να διαβάσετε ένα αρχείο εικόνας, να ρυθμίσετε μια μηχανή OCR και να εξάγετε το κείμενο που η μηχανή αναγνωρίζει.

Η εργασία με σαρωμένα έγγραφα, αποδείξεις ή στιγμιότυπα οθόνης συχνά απαιτεί τη μετατροπή του οπτικού περιεχομένου σε αναζητήσιμο κείμενο. Αυτός ο οδηγός σας καθοδηγεί σε κάθε βήμα, από τη φόρτωση της εικόνας μέχρι την εκτύπωση του εξαγόμενου κειμένου, και καλύπτει επίσης κοινά προβλήματα όπως μη υποστηριζόμενες μορφές αρχείων και μηδενικά αποτελέσματα.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* Java Development Kit (JDK) 8 ή νεότερο εγκατεστημένο.  
* Ένα εργαλείο κατασκευής (Maven ή Gradle) για την λήψη της βιβλιοθήκης OCR.  
* Ένα αρχείο εικόνας (JPEG, PNG, BMP) που θέλετε να επεξεργαστείτε.

Ο κώδικας χρησιμοποιεί τη **βιβλιοθήκη OCR από το πακέτο `com.asprise.ocr`** επειδή απαιτεί μόνο ένα JAR και λειτουργεί σε όλες τις κύριες πλατφόρμες. Αντικαταστήστε την με άλλο πάροχο (Tesseract, Google Vision κ.λπ.) αλλάζοντας τις δηλώσεις import και τον κώδικα αρχικοποίησης της μηχανής.

## Βήμα 1: Προσθήκη της εξάρτησης OCR

Αν χρησιμοποιείτε Maven, προσθέστε την παρακάτω εξάρτηση στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.2.0</version>
</dependency>
```

Για Gradle, τοποθετήστε αυτή τη γραμμή στο `build.gradle`:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.2.0'
```

Αυτές οι γραμμές εξασφαλίζουν ότι ο κώδικας **read image Java** μπορεί να μεταγλωττιστεί και ότι η μηχανή OCR είναι διαθέσιμη κατά την εκτέλεση.

## Βήμα 2: Ανάγνωση της εικόνας με Java

Η ανάγνωση ενός αρχείου εικόνας είναι το πρώτο συγκεκριμένο βήμα σε οποιαδήποτε ροή εργασίας **extract text image**. Η ενσωματωμένη κλάση `ImageIO` της Java διαχειρίζεται τις πιο κοινές μορφές.

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Loads an image from the supplied path.
 *
 * @param path absolute or relative path to the image file
 * @return a BufferedImage instance, or null if the file cannot be read
 */
private static BufferedImage loadImage(String path) {
    try {
        return ImageIO.read(new File(path));
    } catch (Exception e) {
        System.err.println("Failed to read image: " + e.getMessage());
        return null;
    }
}
```

**Γιατί είναι σημαντικό:** Η `ImageIO.read` επιστρέφει `null` για μη υποστηριζόμενες μορφές ή κατεστραμμένα αρχεία. Η παραπάνω μέθοδος καταγράφει το πρόβλημα και επιστρέφει `null` ώστε το επόμενο βήμα να μπορεί να αντιδράσει ομαλά.

## Βήμα 3: Δημιουργία και ρύθμιση της μηχανής OCR

Η μηχανή OCR πρέπει να γνωρίζει ποια γλώσσα θα αναγνωρίσει. Η ρύθμιση της γλώσσας βελτιώνει δραματικά την ακρίβεια, ειδικά για έγγραφα που δεν είναι στα Αγγλικά.

```java
import com.asprise.ocr.Ocr;

/**
 * Instantiates an OCR engine configured for English.
 *
 * @return a ready‑to‑use Ocr object
 */
private static Ocr createEngine() {
    Ocr ocrEngine = new Ocr();
    // The first argument is the language; "eng" is the ISO code for English.
    ocrEngine.startEngine("eng", Ocr.SPEED_FAST);
    return ocrEngine;
}
```

**Γιατί είναι σημαντικό:** Η εκκίνηση της μηχανής είναι μια σχετικά βαριά λειτουργία, γι' αυτό θα πρέπει να τη δημιουργείτε μία φορά και να την επαναχρησιμοποιείτε για πολλές εικόνες εάν η εφαρμογή σας επεξεργάζεται παρτίδες.

## Βήμα 4: Εκτέλεση OCR και μετατροπή της εικόνας σε κείμενο

Τώρα που η εικόνα φορτώθηκε και η μηχανή είναι έτοιμη, μπορείτε να εκτελέσετε το βήμα αναγνώρισης. Αυτό είναι το κεντρικό μέρος του **πώς να εκτελέσετε OCR**.

```java
/**
 * Runs OCR on a BufferedImage and returns the recognized text.
 *
 * @param ocrEngine an initialized Ocr instance
 * @param image     the image to process
 * @return the extracted text, or an empty string if nothing is recognized
 */
private static String extractText(Ocr ocrEngine, BufferedImage image) {
    if (image == null) {
        return "";
    }
    // The third parameter (0) tells the engine to return plain text.
    String result = ocrEngine.recognize(image, 0);
    return result != null ? result.trim() : "";
}
```

**Διαχείριση ειδικών περιπτώσεων:** Αν η εικόνα είναι `null`, η μέθοδος επιστρέφει μια κενή συμβολοσειρά αντί να ρίξει `NullPointerException`. Αυτό κάνει τον περιβάλλοντα κώδικα πιο ανθεκτικό όταν δουλεύει με αρχεία που παρέχονται από χρήστες.

## Βήμα 5: Εμφάνιση του εξαγόμενου κειμένου

Τέλος, εκτυπώστε το αποτέλεσμα στην κονσόλα ή προωθήστε το σε άλλο στοιχείο (π.χ. βάση δεδομένων ή widget UI).

```java
/**
 * Demonstrates the full OCR workflow.
 *
 * @param args command‑line arguments (first argument = path to image)
 */
public static void main(String[] args) {
    if (args.length == 0) {
        System.err.println("Usage: java OcrDemo <path-to-image>");
        return;
    }

    String imagePath = args[0];
    BufferedImage image = loadImage(imagePath);
    Ocr ocrEngine = createEngine();

    String text = extractText(ocrEngine, image);
    System.out.println("=== Recognized Text ===");
    System.out.println(text.isEmpty() ? "(no text detected)" : text);

    // Clean up the OCR engine to free native resources.
    ocrEngine.stopEngine();
}
```

Όταν τρέξετε το πρόγραμμα με `java OcrDemo sample.jpg`, η κονσόλα θα εμφανίσει τους αναγνωρισμένους χαρακτήρες. Αυτό ολοκληρώνει τον κύκλο **convert image to text**.

### Αναμενόμενο αποτέλεσμα

```
=== Recognized Text ===
The quick brown fox jumps over the lazy dog.
```

Αν η εικόνα δεν περιέχει αναγνώσιμους χαρακτήρες, το πρόγραμμα εκτυπώνει `(no text detected)`.

## Συχνές παραλλαγές και πώς να τις προσαρμόσετε

| Παραλλαγή | Τι αλλάζει | Πότε να χρησιμοποιηθεί |
|-----------|------------|------------------------|
| **Διαφορετική γλώσσα** | Αντικαταστήστε το `"eng"` με `"spa"` για Ισπανικά, `"fra"` για Γαλλικά κ.λπ. | Έγγραφα γραμμένα σε γλώσσα διαφορετική από τα Αγγλικά |
| **Επεξεργασία παρτίδας** | Επανάληψη πάνω σε λίστα διαδρομών αρχείων, επαναχρησιμοποίηση του ίδιου αντικειμένου `Ocr`. | Μεγάλες συλλογές σαρωμένων σελίδων |
| **Υψηλότερη ακρίβεια** | Χρησιμοποιήστε `Ocr.SPEED_SLOW` ή ενεργοποιήστε `ocrEngine.setConfig("tessedit_char_whitelist", "0123456789")` για σάρωση μόνο αριθμών. | Όταν η ποιότητα OCR είναι κρίσιμη (π.χ. αριθμοί τιμολογίων) |
| **Εναλλακτική Tesseract** | Αλλάξτε το import σε `net.sourceforge.tess4j.Tesseract` και προσαρμόστε τον κώδικα αρχικοποίησης. | Έργα που ήδη εξαρτώνται από το Tesseract |

## Pro tips

* **Αλλάξτε το μέγεθος μεγάλων εικόνων** πριν τις δώσετε στη μηχανή· η ταχύτητα OCR κλιμακώνεται με τον αριθμό των εικονοστοιχείων.  
* **Προεπεξεργασία** της εικόνας (αποχρωματισμός, ενίσχυση αντίθεσης) χρησιμοποιώντας βιβλιοθήκες όπως το OpenCV εάν η πηγή είναι θορυβώδης.  
* **Cache τη μηχανή OCR** εάν την καλείτε πολλές φορές σε σύντομο χρονικό διάστημα· η εκκίνηση και η διακοπή της μηχανής δημιουργούν κόστος.  
* **Επαληθεύστε το αποτέλεσμα** με κανονικές εκφράσεις όταν περιμένετε συγκεκριμένη μορφή (π.χ. ημερομηνίες, αριθμούς τηλεφώνου).

## Συμπέρασμα

Τώρα γνωρίζετε **πώς να εκτελέσετε OCR** σε μια εικόνα με Java, από την ανάγνωση του αρχείου μέχρι την εμφάνιση του εξαγόμενου κειμένου. Το tutorial κάλυψε τεχνικές **read image Java**, **extract text image**, **convert image to text**, και **image to text java**, και παρείχε πρακτικές συμβουλές για πραγματικές περιπτώσεις.

Από εδώ μπορείτε:

* Να ενσωματώσετε το βήμα OCR σε μια υπηρεσία web που δέχεται ανεβάσματα.  
* Να συνδυάσετε το αποτέλεσμα με έναν ευρετήριο αναζήτησης για πλήρη κειμενική αναζήτηση σε σαρωμένα έγγραφα.  
* Να εξερευνήσετε προχωρημένες επιλογές OCR όπως υποστήριξη πολλαπλών γλωσσών ή προσαρμοσμένα σύνολα χαρακτήρων.

Καλή προγραμματιστική δουλειά και απολαύστε τη μετατροπή εικόνων σε αναζητήσιμο κείμενο!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετα χαρακτηριστικά API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Use OCR in Java – Extract Text from Image with Spell Correction](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/)
- [Convert Image to Text in Java Using Aspose OCR – Full Guide](/ocr/english/java/ocr-operations/convert-image-to-text-in-java-using-aspose-ocr-full-guide/)
- [How to Enable GPU for OCR in Java – Extract Text from Image](/ocr/english/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}