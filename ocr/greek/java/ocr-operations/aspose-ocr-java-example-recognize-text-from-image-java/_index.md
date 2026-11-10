---
category: general
date: 2026-06-25
description: παράδειγμα Aspose OCR Java που δείχνει πώς να αναγνωρίζετε κείμενο από
  εικόνα Java χρησιμοποιώντας το Aspose OCR με διόρθωση ορθογραφίας – ένας γρήγορος,
  εκτελέσιμος οδηγός.
draft: false
keywords:
- aspose ocr java example
- recognize text from image java
- Aspose OCR spell correction
- Java OCR library
- image to text Java
language: el
og_description: Το παράδειγμα Aspose OCR Java δείχνει πώς να αναγνωρίζετε κείμενο
  από εικόνα Java με το Aspose OCR, συμπεριλαμβανομένης της διόρθωσης ορθογραφίας
  για τα Αγγλικά.
og_title: παράδειγμα Aspose OCR Java – αναγνώριση κειμένου από εικόνα
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: aspose ocr java example that shows how to recognize text from image
    java using Aspose OCR with spell‑correction – a quick, runnable guide.
  headline: 'aspose ocr java example: recognize text from image java'
  type: TechArticle
tags:
- Aspose OCR
- Java
- Image Recognition
title: 'Παράδειγμα Aspose OCR Java: Αναγνώριση κειμένου από εικόνα Java'
url: /el/java/ocr-operations/aspose-ocr-java-example-recognize-text-from-image-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# aspose ocr java example: recognize text from image java

Έχετε αναρωτηθεί ποτέ πώς να εξάγετε καθαρό, διορθωμένο κείμενο από μια θορυβώδη εικόνα χρησιμοποιώντας Java; **aspose ocr java example** είναι η συντόμευση που ψάχνατε. Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα από ένα πλήρως λειτουργικό απόσπασμα κώδικα που όχι μόνο διαβάζει την εικόνα αλλά εφαρμόζει διόρθωση ορθογραφίας για κείμενο στα Αγγλικά.

Θα ενσωματώσουμε επίσης τη δευτερεύουσα φράση *recognize text from image java* ώστε να δείτε ακριβώς πώς συνδέονται οι δύο έννοιες. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση έργο, μια σαφή εικόνα του γιατί κάθε γραμμή είναι σημαντική, και μερικές επαγγελματικές συμβουλές για να διατηρήσετε την OCR αλυσίδα σας ομαλή.

## Τι Θα Δημιουργήσετε

- Μια μικρή εφαρμογή κονσόλας Java που φορτώνει μια εικόνα (`misspelled.png`) με σκόπιμα λανθασμένες λέξεις.  
- Μια παρουσία `AsposeOCR` ρυθμισμένη με ενεργοποιημένη τη spell‑correction για τα Αγγλικά.  
- Μια καθαρή έξοδος κονσόλας που εκτυπώνει το διορθωμένο κείμενο.

Χωρίς εξωτερικές υπηρεσίες, χωρίς βαριά πλαίσια—μόνο απλή Java και η βιβλιοθήκη Aspose OCR.

## Προαπαιτούμενα (Τι Χρειάζεστε Πριν Ξεκινήσετε)

| Απαίτηση | Γιατί Είναι Σημαντικό |
|-------------|----------------|
| **Java 17+** (ή οποιοδήποτε πρόσφατο JDK) | Το Aspose OCR παρέχει δυαδικά αρχεία συμβατά με Java 8, αλλά η χρήση ενός πρόσφατου JDK προσφέρει καλύτερη απόδοση και υποστήριξη μονάδων. |
| **Maven or Gradle** | Ο πιο εύκολος τρόπος για να προσθέσετε το Aspose OCR JAR και τις εξαρτήσεις του στο έργο σας. |
| **Aspose OCR for Java** license (or a 30‑day trial) | Η βιβλιοθήκη είναι εμπορική· μια δοκιμαστική έκδοση λειτουργεί καλά για μάθηση. |
| **An image file** (`misspelled.png`) with some misspelled words | Αυτή είναι η πηγή που θα διαβάσει η μηχανή OCR. Μπορείτε να δημιουργήσετε μία με το Paint ή οποιοδήποτε εργαλείο στιγμιοτύπου. |

Αν τα έχετε, είστε έτοιμοι. Διαφορετικά, κατεβάστε το JDK από την Oracle ή το AdoptOpenJDK, εγκαταστήστε το Maven (`brew install maven` στο macOS, `choco install maven` στα Windows), και εγγραφείτε για μια δωρεάν δοκιμή του Aspose.

## Βήμα 1: Ρυθμίστε το Maven Project και Προσθέστε το Aspose OCR

Δημιουργήστε ένα νέο φάκελο, τρέξτε `mvn archetype:generate` (ή χρησιμοποιήστε τον οδηγό “New Maven Project” του IDE σας), και προσθέστε την παρακάτω εξάρτηση στο `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- replace with the latest version -->
</dependency>
```

> **Pro tip:** Αν χρησιμοποιείτε Gradle, το ισοδύναμο είναι  
> `implementation 'com.aspose:aspose-ocr:23.10'`.

Μετά την αποθήκευση του αρχείου, τρέξτε `mvn clean compile` για να κατεβάσει το Maven τα JARs. Θα δείτε έναν φάκελο `target` να εμφανίζεται—τέλεια, η βάση είναι έτοιμη.

## Βήμα 2: Δημιουργήστε Ρύθμιση OCR με Spell‑Correction

Τώρα ας γράψουμε την κλάση Java που περιέχει τη λογική OCR. Το πρώτο βήμα είναι η δημιουργία ενός αντικειμένου `OcrConfig` και η ενεργοποίηση του spell‑corrector για τα Αγγλικά. Αυτό είναι η καρδιά του **aspose ocr java example** επειδή χωρίς αυτό η μηχανή θα επέστρεφε ακατέργαστο, πιθανώς χαλασμένο κείμενο.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.config.*;

public class OcrSpellCorrectDemo {

    public static void main(String[] args) {
        // Step 2.1: Build OCR configuration and enable spell correction for English
        OcrConfig cfg = new OcrConfig()
                .setSpellCorrectorSettings(new SpellCorrectorSettings()
                        .setEnabled(true)          // turn on correction
                        .setLanguage("en"));       // language of the text

        // Step 2.2: Initialize the OCR engine with the configuration
        AsposeOCR ocr = new AsposeOCR(cfg);
```

**Γιατί είναι σημαντικό:**  
- `setEnabled(true)` λέει στη μηχανή να εκτελεί έναν λεξικο‑βασισμένο μετα‑επεξεργαστή μετά την αναγνώριση χαρακτήρων.  
- `setLanguage("en")` επιλέγει το λεξικό Αγγλικών· μπορείτε να το αλλάξετε σε `"fr"` ή `"de"` για Γαλλικά ή Γερμανικά αντίστοιχα.

## Βήμα 3: Recognize Text from Image Java – Φόρτωση και Επεξεργασία της Εικόνας

Με τη μηχανή έτοιμη, η επόμενη γραμμή πραγματικά *recognize text from image java*. Η μέθοδος `recognizeImage` παίρνει μια διαδρομή αρχείου, εκτελεί την αλυσίδα OCR και επιστρέφει ένα `ImageRecognitionResult`. Να η συνέχεια του κώδικα:

```java
        // Step 3: Recognize text from the image containing misspelled words
        ImageRecognitionResult result = ocr.recognizeImage("YOUR_DIRECTORY/misspelled.png");

        // Step 4: Output the corrected text
        System.out.println("Corrected text:\n" + result.getText());
    }
}
```

> **What could go wrong?**  
> - **File not found:** Ελέγξτε ξανά τη διαδρομή· η χρήση απόλυτης διαδρομής εξαλείφει την αμφιβολία.  
> - **Unsupported image format:** Το Aspose OCR υποστηρίζει PNG, JPEG, BMP και TIFF. Οποιοδήποτε άλλο θα προκαλέσει εξαίρεση.

## Βήμα 4: Εκτελέστε το Πρόγραμμα και Επαληθεύστε την Έξοδο

Συγκεντρώστε και τρέξτε:

```bash
mvn exec:java -Dexec.mainClass=OcrSpellCorrectDemo
```

Αν όλα είναι σωστά συνδεδεμένα, η κονσόλα θα εκτυπώσει κάτι όπως:

```
Corrected text:
The quick brown fox jumps over the lazy dog.
```

Ακόμη και αν η αρχική εικόνα έδειχνε “Teh quikc brwon fox jmps oevr teh lazi dog”, η spell‑corrector το καθαρίζει. Αυτή είναι η δύναμη αυτού του **aspose ocr java example**—συνδέει την ακατέργαστη έξοδο OCR με κείμενο αναγνώσιμο από άνθρωπο αυτόματα.

## Βήμα 5: Ρυθμίστε τη Διαμόρφωση (Προηγμένες Επιλογές)

Ο προεπιλεγμένος spell‑corrector λειτουργεί καλά για καθημερινά Αγγλικά, αλλά ίσως χρειαστεί να προσαρμόσετε τη συμπεριφορά του:

| Ρύθμιση | Περιγραφή | Παράδειγμα |
|---------|-------------|---------|
| `setCustomDictionary(List<String>)` | Προσθέτει λέξεις ειδικές για το domain (π.χ., ονόματα προϊόντων). | `.setCustomDictionary(Arrays.asList("Aspose", "OCR"))` |
| `setMaxEditDistance(int)` | Ελέγχει πόσο επιθετική είναι η διόρθωση (προεπιλογή 2). | `.setMaxEditDistance(1)` |
| `setIgnoreCase(boolean)` | Διατηρεί την αρχική κεφαλαιοποίηση αν το προτιμάτε. | `.setIgnoreCase(false)` |

Παίξτε με αυτές τις επιλογές αν παρατηρήσετε ότι η μηχανή “υπερ‑διορθώνει” εξειδικευμένη ορολογία.

## Βήμα 6: Συνηθισμένα Πιθανά Σφάλματα και Πώς να τα Αποφύγετε

- **Missing native libraries:** Το Aspose OCR μπορεί να χρειάζεται εγγενή δυαδικά αρχεία για ορισμένες μορφές εικόνας. Το Maven τα κατεβάζει αυτόματα, αλλά σε Linux ίσως χρειαστεί να εγκαταστήσετε το `libjpeg`.  
- **Large images:** Η επεξεργασία μιας φωτογραφίας 10 MB μπορεί να είναι αργή. Μεγέθυνση ή σμίκρυνση πριν τη δώσετε στη μηχανή (`java.awt.Image#getScaledInstance`).  
- **Incorrect language code:** Η χρήση του `\"en-US\"` αντί του `\"en\"` θα επανέλθει σιωπηλά στο προεπιλεγμένο λεξικό, δίνοντας υποβέλτιστα αποτελέσματα.

Η αντιμετώπιση αυτών νωρίς σας εξοικονομεί ώρες εντοπισμού σφαλμάτων αργότερα.

## Οπτική Επισκόπηση (Προαιρετικό)

![OCR flow diagram showing aspose ocr java example processing steps](/images/ocr-flow.png){alt="aspose ocr java example flow"}

Το διάγραμμα απεικονίζει την αλυσίδα τεσσάρων βημάτων: configuration → engine init → image recognition → corrected output.

## Ανακεφαλαίωση: Τι Καταφέραμε

- Ρυθμίσαμε ένα **aspose ocr java example** που φορτώνει μια εικόνα, εκτελεί OCR και εφαρμόζει English spell correction.  
- Δείξαμε τη συγκεκριμένη φράση *recognize text from image java* σε συμφραζόμενα, ικανοποιώντας τόσο τις απαιτήσεις SEO όσο και τις προσδοκίες AI‑search.  
- Παρέχουμε ένα πλήρες, έτοιμο‑για‑αντιγραφή Java πρόγραμμα, μαζί με συμβουλές προσαρμογής και αντιμετώπισης προβλημάτων.

## Τι Ακολουθεί; (Περαιτέρω Εξερεύνηση)

- **Batch processing:** Επανάληψη σε φάκελο εικόνων και εγγραφή κάθε αποτελέσματος σε αρχείο κειμένου.  
- **Multi‑language support:** Συνδυάστε πολλαπλές `SpellCorrectorSettings` για δίγλωσσα έγγραφα.  
- **Integration with Spring Boot:** Εκθέστε τη λογική OCR ως REST endpoint—ιδανικό για μικροϋπηρεσίες.  

Όλα αυτά τα θέματα επεκτείνουν φυσικά το **aspose ocr java example** που μόλις δημιουργήσατε, και θα ενισχύσουν τη δευτερεύουσα λέξη-κλειδί *recognize text from image java* σε διαφορετικές περιπτώσεις χρήσης.

Αισθανθείτε ελεύθεροι να τροποποιήσετε τη διαδρομή της εικόνας, να πειραματιστείτε με άλλες γλώσσες ή να ενσωματώσετε αυτό το απόσπασμα σε μια μεγαλύτερη αλυσίδα επεξεργασίας εγγράφων. Αν αντιμετωπίσετε κάποιο πρόβλημα, αφήστε ένα σχόλιο παρακάτω—καλή προγραμματιστική!

## Τι Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη, λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετα χαρακτηριστικά του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [αναγνώριση κειμένου εικόνας με Aspose OCR – Πλήρης Οδηγός Java OCR](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Εξαγωγή Κειμένου από Εικόνα Java με Aspose.OCR Λειτουργία Ανίχνευσης Περιοχών](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Μετατροπή Εικόνας σε Κείμενο σε Java χρησιμοποιώντας Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}