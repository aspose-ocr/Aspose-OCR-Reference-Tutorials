---
category: general
date: 2026-06-19
description: Αναγνώριση κειμένου από εικόνα με Aspose OCR σε Java. Μάθετε πώς να ενεργοποιήσετε
  τον ορθογραφικό έλεγχο, να προσθέσετε λεξικό και να εκτελέσετε OCR με ορθογραφικό
  έλεγχο σε ένα ενιαίο σεμινάριο.
draft: false
keywords:
- recognize text from image
- how to enable spellcheck
- how to add dictionary
- ocr with spell check
language: el
og_description: Αναγνώριση κειμένου από εικόνα χρησιμοποιώντας το Aspense OCR σε Java.
  Αυτός ο οδηγός δείχνει πώς να ενεργοποιήσετε τον ορθογραφικό έλεγχο, να προσθέσετε
  λεξικό και να εκτελέσετε OCR με ορθογραφικό έλεγχο.
og_title: Αναγνώριση κειμένου από εικόνα – Εκπαιδευτικό σεμινάριο ελέγχου ορθογραφίας
  Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Recognize text from image with Aspose OCR in Java. Learn how to enable
    spellcheck, add dictionary, and perform OCR with spell check in a single tutorial.
  headline: Recognize Text from Image in Java – Complete Aspose OCR Spell‑Check Guide
  type: TechArticle
- description: Recognize text from image with Aspose OCR in Java. Learn how to enable
    spellcheck, add dictionary, and perform OCR with spell check in a single tutorial.
  name: Recognize Text from Image in Java – Complete Aspose OCR Spell‑Check Guide
  steps:
  - name: How to Enable SpellCheck
    text: 'The spell checker lives inside the engine, but it’s disabled by default.
      Flip the switch with a single line:'
  - name: Expected Output
    text: 'Assuming `receipt.png` contains the line “Totel: $12.99” and your custom
      dictionary includes “Total”, the console will display:'
  - name: What if I need multiple languages?
    text: You can call `ocrEngine.setLanguage(Language.English, Language.French)`
      to enable multilingual recognition. Spell‑checking will follow each language’s
      rules, but you still need to enable it with `setEnable(true)`.
  - name: How does the engine handle unknown words?
    text: If a word isn’t in the internal dictionary *and* not in your custom dictionary,
      the spell checker attempts a best‑guess correction based on Levenshtein distance.
      For truly unknown terms, add them to `my-terms.txt`.
  - name: Does the spell checker work on numbers?
    text: By default, numeric strings are left untouched. If you have alphanumeric
      codes (e.g., “AB12C”), add them to your custom dictionary; otherwise the engine
      may try to “fix” them to real words.
  - name: Performance considerations
    text: Enabling spell checking adds a modest overhead—roughly 10‑15 % extra CPU
      per page. For batch processing, consider disabling it on the first pass, then
      re‑run only on pages that failed quality checks.
  type: HowTo
tags:
- OCR
- Java
- SpellCheck
title: Αναγνώριση κειμένου από εικόνα σε Java – Πλήρης οδηγός Aspose OCR για ορθογραφικό
  έλεγχο
url: /el/java/advanced-ocr-techniques/recognize-text-from-image-in-java-complete-aspose-ocr-spell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση Κειμένου από Εικόνα σε Java – Πλήρης Οδηγός Aspose OCR με Ορθογραφικό Έλεγχο

Κάποτε χρειάστηκε να **αναγνωρίσετε κείμενο από εικόνα** αλλά ανησυχείτε ότι το αποτέλεσμα θα είναι γεμάτο τυπογραφικά λάθη; Δεν είστε μόνοι. Σε πολλά έργα σάρωσης αποδείξεων ή ψηφιοποίησης εγγράφων το ακατέργαστο κείμενο OCR μοιάζει με κάτι που πληκτρολόγησε μια νυσταγμένη γάτα. Τα καλά νέα; Με το Aspose OCR μπορείτε να μετατρέψετε αυτό το θορυβώδες απόρριμμα σε καθαρό, ορθογραφικά ελεγμένο κείμενο — κατευθείαν μέσα από τη Java.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα έτοιμο παράδειγμα που δείχνει **πώς να ενεργοποιήσετε τον ορθογραφικό έλεγχο**, **πώς να προσθέσετε καταχωρήσεις λεξικού** για ειδικούς όρους, και τελικά **πώς να εκτελέσετε OCR με ορθογραφικό έλεγχο**. Στο τέλος θα έχετε ένα αυτόνομο πρόγραμμα που διαβάζει ένα αρχείο εικόνας, διορθώνει την ορθογραφία σε πραγματικό χρόνο και εκτυπώνει το τελικό αποτέλεσμα.

## Τι Θα Μάθετε

- Πώς να εφαρμόσετε μια άδεια Aspose OCR ώστε το API να λειτουργεί με πλήρη ταχύτητα.  
- Τα ακριβή βήματα για **ενεργοποίηση ορθογραφικού ελέγχου** στον μηχανισμό OCR.  
- Τον σωστό τρόπο για **προσθήκη προσαρμοσμένου λεξικού** για λέξεις όπως κωδικοί προϊόντων ή ονόματα εμπορικών σημάτων.  
- Πώς να καλέσετε `recognizeImage` και να λάβετε καθαρό, διορθωμένο κείμενο.  

Χωρίς εξωτερικά εργαλεία, χωρίς χειροποίητες βιβλιοθήκες ορθογραφικού ελέγχου — μόνο καθαρή Java και Aspose OCR.

## Προαπαιτούμενα

- Java 8+ (ο κώδικας μεταγλωττίζεται με οποιοδήποτε πρόσφατο JDK).  
- Ένα αρχείο άδειας Aspose OCR (`Aspose.OCR.lic`). Αν κάνετε μόνο δοκιμές, η δωρεάν αξιολόγηση λειτουργεί αλλά προσθέτει υδατογράφημα.  
- Maven ή Gradle για την προσθήκη της εξάρτησης `aspose-ocr`, ή μπορείτε να προσθέσετε τα JAR χειροκίνητα.  
- Ένα δείγμα εικόνας (π.χ. PNG από απόδειξη) και ένα αρχείο κειμένου που περιέχει προσαρμοσμένους όρους.

> **Pro tip:** Κρατήστε το προσαρμοσμένο λεξικό σας σε κωδικοποίηση UTF‑8 και μία λέξη ανά γραμμή — το Aspose OCR το διαβάζει απευθείας από το σύστημα αρχείων.

---

## Βήμα 1: Ρύθμιση του Έργου και Προσθήκη της Εξάρτησης Aspose OCR

Αν χρησιμοποιείτε Maven, προσθέστε το παρακάτω απόσπασμα στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.8</version> <!-- use the latest version -->
</dependency>
```

Για Gradle, η ιδέα είναι η ίδια:

```groovy
implementation 'com.aspose:aspose-ocr:23.8'
```

Αφού η εξάρτηση λυθεί, δημιουργήστε μια νέα κλάση Java με όνομα `SpellCheckDemo`. Εδώ θα συμβεί η μαγεία.

## Βήμα 2: Εφαρμογή της Άδειας Aspose OCR

Πριν ξεκινήσει οποιαδήποτε εργασία OCR, πρέπει να ενημερώσετε το Aspose ότι επιτρέπεται η απεριόριστη λειτουργία. Η παράλειψη αυτού του βήματος προκαλεί εξαίρεση χρόνου εκτέλεσης.

```java
// Apply the Aspose OCR license – this removes evaluation watermarks
License license = new License();
license.setLicense("Aspose.OCR.lic");   // path to your .lic file
```

> **Γιατί είναι σημαντικό:** Η άδεια ξεκλειδώνει ολόκληρο τον κινητήρα OCR, συμπεριλαμβανομένου του ενσωματωμένου μοντέλου ορθογραφικού ελέγχου. Χωρίς αυτήν, ο κινητήρας λειτουργεί αλλά αρνείται να χρησιμοποιήσει ορισμένες premium λειτουργίες.

## Βήμα 3: Δημιουργία και Διαμόρφωση του OCR Engine

Τώρα δημιουργούμε το βασικό `OcrEngine` και ορίζουμε τη γλώσσα σε English. Αυτό αποτελεί τη βάση τόσο για την αναγνώριση όσο και για τον ορθογραφικό έλεγχο.

```java
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.setLanguage(Language.English);   // choose the language that matches your image
```

### Πώς να Ενεργοποιήσετε τον SpellCheck

Ο ορθογραφικός ελεγκτής βρίσκεται μέσα στον κινητήρα, αλλά είναι απενεργοποιημένος από προεπιλογή. Απλώστε το διακόπτη με μία μόνο γραμμή:

```java
ocrEngine.getSpellChecker().setEnable(true);   // enables spell‑checking
```

Αυτή η γραμμή ικανοποιεί την απαίτηση **πώς να ενεργοποιήσετε τον ορθογραφικό έλεγχο**. Μόλις ενεργοποιηθεί, ο κινητήρας θα συγκρίνει αυτόματα κάθε αναγνωρισμένη λέξη με το εσωτερικό του λεξικό και θα προτείνει διορθώσεις.

## Βήμα 4: Φόρτωση Προσαρμοσμένου Λεξικού (Πώς να Προσθέσετε Λεξικό)

Αν τα έγγραφά σας περιέχουν ειδικούς όρους — σκεφτείτε SKU προϊόντων, ιατρικούς όρους ή ονόματα εμπορικών σημάτων — θα θέλετε να διδάξετε τον ορθογραφικό ελεγκτή για αυτά. Το Aspose OCR σας επιτρέπει να δείξετε σε ένα απλό αρχείο κειμένου, μία λέξη ανά γραμμή.

```java
// Load a custom word list for spell‑checking
Path customDict = java.nio.file.Paths.get("YOUR_DIRECTORY/my-terms.txt");
ocrEngine.getSpellChecker().addUserDictionary(customDict);
```

> **Τι γίνεται αν το αρχείο δεν βρεθεί;** Το API ρίχνει `FileNotFoundException`. Τυλίξτε την κλήση σε `try/catch` αν χρειάζεστε ευγενική υποβάθμιση.

Τώρα ο κινητήρας γνωρίζει για “AcmeWidget” ή “RX‑9000” και δεν θα τα σημαίνει ως ορθογραφικά λάθη.

## Βήμα 5: Αναγνώριση Κειμένου από την Εικόνα

Με τον κινητήρα έτοιμο, μπορείτε επιτέλους να **αναγνωρίσετε κείμενο από εικόνα**. Η μέθοδος `recognizeImage` επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει το ακατέργαστο και το διορθωμένο κείμενο.

```java
// Recognize text from the image file
OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/receipt.png");
```

Επειδή ενεργοποιήσαμε τον ορθογραφικό έλεγχο νωρίτερα, η κλήση `getText()` επιστρέφει ήδη την διορθωμένη έκδοση.

## Βήμα 6: Έξοδος του Διορθωμένου Κειμένου

Το μόνο που απομένει είναι να εκτυπώσετε (ή να αποθηκεύσετε) τη καθαρή συμβολοσειρά.

```java
// Output the corrected, spell‑checked text
System.out.println(ocrResult.getText());
```

Όταν τρέξετε το πρόγραμμα, θα δείτε μια ωραία μορφοποιημένη απόδειξη με σωστή ορθογραφία, ακόμη και αν η αρχική εικόνα περιείχε θολούς χαρακτήρες.

---

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω βρίσκεται το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα Java. Αντιγράψτε‑και‑επικολλήστε το στο IDE σας, προσαρμόστε τις διαδρομές αρχείων και πατήστε **Run**.

```java
import com.aspose.ocr.*;

import java.nio.file.Path;
import java.nio.file.Paths;

public class SpellCheckDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply the Aspose OCR license
        License license = new License();
        license.setLicense("Aspose.OCR.lic");   // <-- replace with your license path

        // Step 2: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setLanguage(Language.English);

        // Step 3: Load a custom word list for spell‑checking
        Path dictPath = Paths.get("YOUR_DIRECTORY/my-terms.txt"); // <-- your dictionary file
        ocrEngine.getSpellChecker().addUserDictionary(dictPath);
        ocrEngine.getSpellChecker().setEnable(true); // <-- how to enable spellcheck

        // Step 4: Recognize text from the image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/receipt.png"); // <-- your image

        // Step 5: Output the corrected text
        System.out.println(ocrResult.getText());
    }
}
```

### Αναμενόμενη Έξοδος

Αν το `receipt.png` περιέχει τη γραμμή “Totel: $12.99” και το προσαρμοσμένο λεξικό σας περιλαμβάνει το “Total”, η κονσόλα θα εμφανίσει:

```
Total: $12.99
```

Το τυπογραφικό λάθος “Totel” διορθώθηκε αυτόματα χάρη στο **ocr with spell check**.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν χρειαστώ πολλές γλώσσες;

Μπορείτε να καλέσετε `ocrEngine.setLanguage(Language.English, Language.French)` για ενεργοποίηση πολυγλωσσικής αναγνώρισης. Ο ορθογραφικός έλεγχος θα ακολουθήσει τους κανόνες κάθε γλώσσας, αλλά πρέπει να τον ενεργοποιήσετε με `setEnable(true)`.

### Πώς αντιμετωπίζει ο κινητήρας άγνωστες λέξεις;

Αν μια λέξη δεν υπάρχει στο εσωτερικό λεξικό *και* δεν βρίσκεται στο προσαρμοσμένο λεξικό, ο ορθογραφικός ελεγκτής προσπαθεί μια βέλτιστη διόρθωση βάσει της απόστασης Levenshtein. Για πραγματικά άγνωστους όρους, προσθέστε τα στο `my-terms.txt`.

### Λειτουργεί ο ορθογραφικός έλεγχος και σε αριθμούς;

Από προεπιλογή, οι αριθμητικές ακολουθίες παραμένουν αμετάβλητες. Αν έχετε αλφαριθμητικούς κωδικούς (π.χ. “AB12C”), προσθέστε τους στο προσαρμοσμένο λεξικό· διαφορετικά ο κινητήρας μπορεί να προσπαθήσει να “διορθώσει” σε πραγματικές λέξεις.

### Σκέψεις για την απόδοση

Η ενεργοποίηση του ορθογραφικού ελέγχου προσθέτει μια ήπια επιβάρυνση — περίπου 10‑15 % επιπλέον CPU ανά σελίδα. Για επεξεργασία σε παρτίδες, σκεφτείτε να τον απενεργοποιήσετε στην πρώτη διέλευση και να το ξανατρέξετε μόνο στις σελίδες που δεν πέρασαν τον έλεγχο ποιότητας.

---

## Ανακεφαλαίωση

Καλύψαμε όλα όσα χρειάζεστε για **αναγνώριση κειμένου από εικόνα** με Aspose OCR σε Java, διατηρώντας το αποτέλεσμα καθαρό. Τα βήματα ήταν:

1. Εφαρμογή της άδειας.  
2. Δημιουργία του `OcrEngine` και ορισμός της γλώσσας.  
3. **Πώς να προσθέσετε λεξικό** — φόρτωση λίστας προσαρμοσμένων λέξεων.  
4. **Πώς να ενεργοποιήσετε τον ορθογραφικό έλεγχο** — ενεργοποίηση του spell‑checker.  
5. Εκτέλεση `recognizeImage` (η κύρια κλήση **ocr with spell check**).  
6. Εκτύπωση του διορθωμένου κειμένου.

Αυτή είναι η πλήρης αλυσίδα — από ακατέργαστα pixel μέχρι πολωμένες, ορθογραφικά ελεγμένες συμβολοσειρές.

---

## Τι Ακολουθεί;

- **Επεξεργασία παρτίδας:** Επανάληψη σε φάκελο εικόνων και αποθήκευση κάθε αποτελέσματος σε ξεχωριστό αρχείο `.txt`.  
- **Έξοδος PDF:** Χρήση Aspose PDF για ενσωμάτωση του διορθωμένου κειμένου σε αναζητήσιμο PDF.  
- **Προηγμένα λεξικά:** Φόρτωση πολλαπλών λεξικών χρήστη για διαφορετικούς τομείς (π.χ. χρηματοοικονομικό vs. ιατρικό).  
- **Σκορ εμπιστοσύνης:** Εξέταση του `ocrResult.getConfidence()` για φιλτράρισμα αποτελεσμάτων χαμηλής βεβαιότητας.

Πειραματιστείτε — αλλάξτε τη γλώσσα, τροποποιήστε το λεξικό ή συνδυάστε το με βιβλιοθήκες προεπεξεργασίας εικόνας για ακόμη καλύτερη ακρίβεια.

Αν αντιμετωπίσατε κάποιο πρόβλημα, αφήστε ένα σχόλιο παρακάτω. Καλό coding, και ας είναι πάντα το OCR σας ορθογραφικά ελεγμένο!

## Τι Θα Μάθετε Στη Σειρά Επόμενη;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κυριαρχήσετε σε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to extract text from image from URL using Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}