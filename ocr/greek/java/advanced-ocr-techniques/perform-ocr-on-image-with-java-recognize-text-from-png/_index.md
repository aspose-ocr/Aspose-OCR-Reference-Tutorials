---
category: general
date: 2026-03-28
description: Εκτελέστε OCR σε εικόνα χρησιμοποιώντας το Aspose OCR σε Java. Μάθετε
  πώς να αναγνωρίζετε κείμενο από PNG και να βελτιώνετε την ακρίβεια του OCR με ενσωματωμένη
  διόρθωση ορθογραφίας.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- read image text
- improve OCR accuracy
- Aspose OCR Java
- spell correction OCR
language: el
og_description: Εκτελέστε OCR σε εικόνα με το Aspose OCR για Java. Αυτός ο οδηγός
  δείχνει πώς να αναγνωρίζετε κείμενο από PNG και να βελτιώσετε την ακρίβεια του OCR
  σε λίγα λεπτά.
og_title: Εκτέλεση OCR σε εικόνα με Java – Πλήρης οδηγός
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Διενέργεια OCR σε εικόνα με Java – Αναγνώριση κειμένου από PNG
url: /el/java/advanced-ocr-techniques/perform-ocr-on-image-with-java-recognize-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε εικόνα με Java – Αναγνώριση κειμένου από PNG

Έχετε ποτέ χρειαστεί να **perform OCR on image** αρχεία αλλά να λαμβάνετε ακατάστατα αποτελέσματα; Δεν είστε μόνοι—θορυβώδεις σαρώσεις, PNG με χαμηλή αντίθεση και παράξενες γραμματοσειρές μπορούν να μετατρέψουν ένα καθαρό έγγραφο σε μια μπάστα χαρακτήρων.  

Σε αυτόν τον οδηγό θα σας καθοδηγήσουμε βήμα-βήμα μέσα από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα Java που **recognize text from PNG** χρησιμοποιώντας το Aspose OCR, και θα σας δείξουμε επίσης πώς να **improve OCR accuracy** με τη λειτουργία διόρθωσης ορθογραφίας της βιβλιοθήκης. Στο τέλος, θα μπορείτε να **read image text** αξιόπιστα, ακόμη και όταν η πηγή δεν είναι τέλεια.

## Τι θα μάθετε

- Πώς να ρυθμίσετε το Aspose OCR για Java σε ένα έργο Maven.  
- Τα ακριβή βήματα για **perform OCR on image** δεδομένα, από τη φόρτωση του αρχείου μέχρι την εξαγωγή καθαρού κειμένου.  
- Γιατί η ενεργοποίηση της διόρθωσης ορθογραφίας μπορεί να αυξήσει δραματικά την ποιότητα του αποτελέσματος.  
- Κοινά προβλήματα (απουσία αρχείων, μη υποστηριζόμενες μορφές) και πώς να τα αντιμετωπίσετε με χάρη.  
- Ένα πλήρες, έτοιμο για αντιγραφή‑επικόλληση δείγμα κώδικα που μπορείτε να εκτελέσετε σήμερα.

### Προαπαιτούμενα

- Java 8 ή νεότερη εγκατεστημένη στο σύστημά σας.  
- Maven για διαχείριση εξαρτήσεων (οποιοδήποτε IDE με υποστήριξη Maven αρκεί).  
- Μια εικόνα PNG που περιέχει κάποιο αναγνώσιμο κείμενο—κατά προτίμηση μια ελαφρώς θορυβώδης ώστε να δείτε το όφελος της διόρθωσης ορθογραφίας.

> **Συμβουλή επαγγελματία:** Αν δεν έχετε άμεσα διαθέσιμη PNG, πάρτε οποιοδήποτε στιγμιότυπο οθόνης ενός εγγράφου ή μια φωτογραφία μιας πινακίδας. Όσο πιο “θορυβώδης” φαίνεται, τόσο περισσότερο θα εκτιμήσετε την αύξηση της ακρίβειας.

## Βήμα 1: Προσθήκη εξάρτησης Aspose OCR

Πρώτα απ' όλα—προσθέστε τη βιβλιοθήκη Aspose OCR στο `pom.xml` σας. Αυτή η μοναδική γραμμή φέρνει την πιο πρόσφατη έκδοση (από Μάρτιο 2026) και επιλύει όλες τις εσωτερικές εξαρτήσεις.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version>
</dependency>
```

> **Γιατί είναι σημαντικό:** Χωρίς τη βιβλιοθήκη δεν μπορείτε να δημιουργήσετε ένα `OcrEngine`, και όλη η διαδικασία **perform OCR on image** θα διακοπεί κατά την εκτέλεση.

## Βήμα 2: Αρχικοποίηση του OCR Engine

Η δημιουργία του engine είναι απλή, αλλά υπάρχει ένας λεπτός λόγος για να κρατήσετε την αρχικοποίηση ξεχωριστά από την κλήση αναγνώρισης: σας δίνει τη δυνατότητα να ρυθμίσετε παραμέτρους όπως η γλώσσα, το DPI ή, το πιο σημαντικό για εμάς, η διόρθωση ορθογραφίας.

```java
import com.aspose.ocr.*;

public class SpellCorrectExample {

    public static void main(String[] args) {
        try {
            // Step 2: Initialize the OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Pro tip: you can set the language here if you need something other than English
            // ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.FRENCH);
```

Παρατηρήστε το σχόλιο—η ρύθμιση της γλώσσας μπορεί να σώσει τη ζωή όταν το PNG σας περιέχει μη‑Αγγλικούς χαρακτήρες.

## Βήμα 3: Ενεργοποίηση διόρθωσης ορθογραφίας για **Improve OCR Accuracy**

Το Aspose OCR περιλαμβάνει ενσωματωμένο μονάδα διόρθωσης ορθογραφίας που λειτουργεί σαν ελαφρύ λεξικό. Η ενεργοποίησή της είναι μια εντολή, όμως η επίδραση στο τελικό αποτέλεσμα μπορεί να είναι τεράστια, ειδικά για θορυβώδεις εικόνες.

```java
            // Step 3: Enable spell correction to improve OCR accuracy on noisy text
            ocrEngine.getRecognitionSettings().setEnableSpellCorrection(true);
```

> **Τι γίνεται αν δεν το χρειάζεστε;** Μπορείτε απλώς να ορίσετε τη σημαία σε `false`. Η απενεργοποίησή του μπορεί να είναι χρήσιμη για κείμενο ειδικού τομέα όπου το λεξικό θα σημειώσει ως σφάλματα έγκυρους όρους.

## Βήμα 4: Φόρτωση και αναγνώριση του PNG

Τώρα διαβάζουμε πραγματικά **read image text** από το αρχείο. Η μέθοδος `recognizeImage` δέχεται μια συμβολοσειρά διαδρομής, αλλά μπορείτε επίσης να της δώσετε ένα `java.io.InputStream` αν αντλείτε την εικόνα από μια βάση δεδομένων ή το διαδίκτυο.

```java
            // Step 4: Perform OCR on the input image
            String imagePath = "YOUR_DIRECTORY/noisy-image.png"; // replace with your actual path
            OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

Αν το αρχείο δεν βρεθεί, το Aspose ρίχνει μια περιγραφική εξαίρεση—δεν χρειάζεται να ελέγξετε χειροκίνητα το `File.exists()`. Παρόλα αυτά, η περιτύλιξη της κλήσης σε `try/catch` (όπως κάνουμε) σας δίνει ένα καθαρό μήνυμα σφάλματος για τον τελικό χρήστη.

## Βήμα 5: Εξαγωγή του διορθωμένου κειμένου

Τέλος, εκτυπώστε το αποτέλεσμα στην κονσόλα. Σε μια πραγματική εφαρμογή πιθανότατα θα το γράφατε σε μια βάση δεδομένων ή σε μια υπηρεσία downstream, αλλά η κονσόλα είναι ιδανική για μια γρήγορη επίδειξη.

```java
            // Step 5: Output the corrected text
            System.out.println("Corrected text:\\n" + ocrResult.getText());
        } catch (Exception e) {
            System.err.println("Error during OCR processing: " + e.getMessage());
        }
    }
}
```

**Αναμενόμενο αποτέλεσμα** (υποθέτοντας ότι το PNG περιέχει τη φράση “Aspose OCR library” με κάποιο θόρυβο):

```
Corrected text:
Aspose OCR library
```

Αν απενεργοποιήσετε τη διόρθωση ορθογραφίας, μπορεί να δείτε κάτι όπως “Asp0se OCR libr@ry” — ακριβώς ο λόγος για τον οποίο η **improve OCR accuracy** είναι σημαντική.

## Βήμα 6: Επαλήθευση του αποτελέσματος – Διαβάζει πραγματικά **Read Image Text**;

Μπορεί να είναι δελεαστικό να εμπιστευτείτε τυφλά το αποτέλεσμα της κονσόλας, αλλά ένας γρήγορος έλεγχος λογικής μπορεί να σας εξοικονομήσει ώρες αργότερα. Εδώ είναι μερικοί τρόποι για να επαληθεύσετε το εξαγόμενο κείμενο:

1. **Length check** – Συγκρίνετε το `ocrResult.getText().length()` με τον αναμενόμενο αριθμό χαρακτήρων.  
2. **Keyword search** – Χρησιμοποιήστε το `String.contains("Aspose")` για να βεβαιωθείτε ότι εμφανίζονται οι βασικοί όροι.  
3. **Unit test** – Αν ενσωματώνετε αυτό σε μεγαλύτερο σύστημα, γράψτε ένα τεστ JUnit που επιβεβαιώνει ότι το αποτέλεσμα ταιριάζει με μια γνωστή σωστή τιμή.

```java
// Example sanity check
if (ocrResult.getText().contains("Aspose")) {
    System.out.println("✅ Text successfully read from image.");
} else {
    System.out.println("⚠️ Unexpected OCR result – consider tweaking settings.");
}
```

## Κοινές Ακραίες Περιπτώσεις & Πώς να τις Διαχειριστείτε

| Κατάσταση | Γιατί Συμβαίνει | Γρήγορη Διόρθωση |
|-----------|----------------|-------------------|
| **File not found** | Λάθος διαδρομή ή έλλειψη δικαιωμάτων | Επαληθεύστε το `imagePath` και χρησιμοποιήστε `Files.isReadable(Paths.get(imagePath))` πριν καλέσετε το `recognizeImage`. |
| **Unsupported format** | Το Aspose OCR υποστηρίζει PNG, JPEG, BMP, TIFF κ.λπ. | Μετατρέψτε την εικόνα σε PNG πρώτα (π.χ., με ImageIO) ή χρησιμοποιήστε `ocrEngine.recognizeImage(InputStream)`. |
| **Very low DPI** | Οι μηχανές OCR χρειάζονται τουλάχιστον ~300 DPI για αποδεκτή ακρίβεια | Μεγεθύνετε την εικόνα χρησιμοποιώντας `BufferedImage` και `Graphics2D` πριν τη δώσετε στο engine. |
| **Domain‑specific jargon** | Η διόρθωση ορθογραφίας μπορεί να αντικαταστήσει έγκυρους όρους με λέξεις του λεξικού | Απενεργοποιήστε τη διόρθωση ορθογραφίας (`setEnableSpellCorrection(false)`) ή παρέχετε προσαρμοσμένο λεξικό μέσω `ocrEngine.getRecognitionSettings().setCustomDictionary(...)`. |

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω βρίσκεται ολόκληρο το αρχείο πηγαίου κώδικα, έτοιμο για μεταγλώττιση και εκτέλεση. Αντικαταστήστε το `YOUR_DIRECTORY/noisy-image.png` με την πραγματική διαδρομή της δοκιμαστικής σας εικόνας.

```java
import com.aspose.ocr.*;

public class SpellCorrectExample {
    public static void main(String[] args) {
        try {
            // Initialize the OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Enable spell correction to improve OCR accuracy on noisy text
            ocrEngine.getRecognitionSettings().setEnableSpellCorrection(true);

            // Path to the PNG you want to process
            String imagePath = "YOUR_DIRECTORY/noisy-image.png";

            // Perform OCR on the input image
            OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

            // Output the corrected text
            System.out.println("Corrected text:\\n" + ocrResult.getText());

            // Simple verification that we actually read image text
            if (ocrResult.getText().toLowerCase().contains("aspose")) {
                System.out.println("✅ OCR succeeded – key term found.");
            } else {
                System.out.println("⚠️ OCR may need tweaking – key term missing.");
            }
        } catch (Exception e) {
            System.err.println("Error during OCR processing: " + e.getMessage());
        }
    }
}
```

Τρέξτε το με:

```bash
mvn compile exec:java -Dexec.mainClass=SpellCorrectExample
```

Θα πρέπει να δείτε το **corrected text** εκτυπωμένο, επιβεβαιώνοντας ότι έχετε εκτελέσει με επιτυχία **performed OCR on image** δεδομένα.

## Οπτική Σύνοψη

![Παράδειγμα εκτέλεσης OCR σε εικόνα](/images/ocr-example.png){alt="εκτέλεση OCR σε εικόνα – πριν και μετά τη διόρθωση ορθογραφίας"}

Το στιγμιότυπο δείχνει ένα θορυβώδες PNG στα αριστερά και το καθαρό, διορθωμένο με ορθογραφία αποτέλεσμα στα δεξιά.

## Συμπέρασμα

Μόλις περάσαμε από μια πλήρη, ολοκληρωμένη λύση για το πώς να **perform OCR on image** αρχεία χρησιμοποιώντας το Aspose OCR για Java. Ενεργοποιώντας τη ενσωματωμένη σημαία διόρθωσης ορθογραφίας, μπορείτε να **improve

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}