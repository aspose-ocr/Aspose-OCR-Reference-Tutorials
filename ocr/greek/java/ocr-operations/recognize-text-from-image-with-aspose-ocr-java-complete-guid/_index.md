---
category: general
date: 2026-03-18
description: Μάθετε πώς να αναγνωρίζετε κείμενο από εικόνα σε Java χρησιμοποιώντας
  το Aspose OCR. Αυτό το βήμα‑βήμα tutorial δείχνει πώς να φορτώσετε εικόνα για OCR
  και να απενεργοποιήσετε το διορθωτή ορθογραφίας.
draft: false
keywords:
- recognize text from image
- load image for ocr
- aspose ocr java example
- extract text from image
- turn off spell corrector
language: el
og_description: Αναγνωρίστε κείμενο από εικόνα σε Java χρησιμοποιώντας το Aspose OCR.
  Μάθετε πώς να φορτώνετε εικόνα για OCR και να απενεργοποιήσετε το διορθωτή ορθογραφίας
  σε αυτό το πρακτικό σεμινάριο.
og_title: Αναγνώριση κειμένου από εικόνα με Aspose OCR Java – Πλήρης Οδηγός
tags:
- Aspose OCR
- Java
- Image Processing
title: Αναγνώριση κειμένου από εικόνα με Aspose OCR Java – Πλήρης οδηγός
url: /el/java/ocr-operations/recognize-text-from-image-with-aspose-ocr-java-complete-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση Κειμένου από Εικόνα με Aspose OCR Java – Πλήρης Οδηγός

Έχετε χρειαστεί ποτέ να **αναγνωρίσετε κείμενο από εικόνα** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη να επιλέξετε; Δεν είστε μόνοι. Σε πολλά πραγματικά έργα—σκεφτείτε σάρωση αποδείξεων, ψηφιοποίηση φορμών ή εξαγωγή λεζάντων από στιγμιότυπα—η λήψη καθαρού, ακατέργαστου κειμένου από ένα bitmap είναι καθημερινή δουλειά.  

Σε αυτό το tutorial θα περάσουμε από ένα πρακτικό **Aspose OCR Java example** που δείχνει ακριβώς πώς να **load image for OCR**, να τρέξετε τη μηχανή, και ακόμη να **turn off spell corrector** όταν χρειάζεστε τους αμετάβλητους χαρακτήρες. Στο τέλος θα έχετε ένα εκτελέσιμο πρόγραμμα που εξάγει κείμενο από εικόνα χωρίς ανεπιθύμητες τροποποιήσεις.

## Τι Θα Κερδίσετε

- Μια σαφή εικόνα της ροής εργασίας **Aspose OCR** για Java.  
- Τον ακριβή κώδικα που χρειάζεται για **recognize text from image** και για **extract text from image** στην αρχική του μορφή.  
- Συμβουλές για το πότε μπορεί να θέλετε να απενεργοποιήσετε τον ενσωματωμένο spell corrector και πώς να το κάνετε με ασφάλεια.  
- Ένα γρήγορο sanity‑check που μπορείτε να τρέξετε για να επαληθεύσετε ότι το αποτέλεσμα ταιριάζει με τις προσδοκίες σας.

### Προαπαιτούμενα (το ελάχιστο)

- Java 8 ή νεότερη εγκατεστημένη στο σύστημά σας.  
- Maven ή Gradle για διαχείριση εξαρτήσεων (θα δείξουμε το Maven snippet).  
- Το αρχείο JAR `Aspose.OCR` (μπορείτε να κατεβάσετε μια δωρεάν δοκιμή από την ιστοσελίδα της Aspose).  
- Ένα αρχείο εικόνας (PNG, JPG, BMP, κλπ.) που περιέχει το κείμενο που θέλετε να διαβάσετε. Για το demo θα χρησιμοποιήσουμε το `mixed-lang.png`.

> **Pro tip:** Αν σκοπεύετε να επεξεργαστείτε πολλές εικόνες, σκεφτείτε να τις φορτώνετε ως streams για να αποφύγετε διαρροές file‑handle.

---

![Διάγραμμα που δείχνει τη ροή εργασίας OCR – αναγνώριση κειμένου από εικόνα](ocr-pipeline.png)

*Κείμενο alt: διάγραμμα που απεικονίζει τα βήματα για την αναγνώριση κειμένου από εικόνα χρησιμοποιώντας Aspose OCR.*

## Βήμα 1 – Ρύθμιση του Έργου και Προσθήκη της Εξάρτησης Aspose OCR

Πριν μπορέσουμε να καλέσουμε οποιεσδήποτε μεθόδους OCR, η βιβλιοθήκη πρέπει να βρίσκεται στο classpath. Αν χρησιμοποιείτε Maven, προσθέστε αυτό στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Αν προτιμάτε Gradle, το ισοδύναμο είναι:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

Μόλις η εξάρτηση λυθεί, μπορείτε να εισάγετε τις δύο κλάσεις που θα χρειαστούμε:

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.Image;
```

> **Why this matters:** Η προσθήκη του JAR μέσω εργαλείου build εγγυάται ότι η σωστή έκδοση χρησιμοποιείται σε όλα τα περιβάλλοντα, εξαλείφοντας τα “class not found” προβλήματα αργότερα.

## Βήμα 2 – Δημιουργία του OCR Engine και Απενεργοποίηση του Spell Corrector

Το Aspose OCR έρχεται με έναν ενσωματωμένο spell corrector που προσπαθεί να μαντέψει τι θέλατε να γράψετε. Αυτό είναι χρήσιμο για καθαρά έγγραφα, αλλά αν σκανάρετε πολυγλωσσικές πινακίδες ή αποσπάσματα κώδικα θα καταλήξετε με “διορθώσεις” που δεν θέλετε. Να πώς το απενεργοποιείτε:

```java
// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Disable the automatic spell correction
ocrEngine.getSpellCorrector().setEnabled(false);
```

**What’s happening under the hood?** Το αντικείμενο `SpellCorrector` εκτελεί μια διπλωματική διεργασία μετά την αποκωδικοποίηση των ακατέργαστων glyphs. Καλώντας `setEnabled(false)`, λέμε στη μηχανή να παραλείψει αυτή τη διεργασία, διατηρώντας ακριβώς τη σειρά χαρακτήρων που ανίχνευσε.

## Βήμα 3 – Φόρτωση Εικόνας για OCR

Τώρα πραγματικά **load image for OCR**. Η μέθοδος `Image.load` του Aspose δέχεται διαδρομή αρχείου, `InputStream`, ή ακόμα και byte array. Για απλότητα θα χρησιμοποιήσουμε διαδρομή αρχείου:

```java
// Replace the path with the location of your image file
Image inputImage = Image.load("YOUR_DIRECTORY/mixed-lang.png");
```

> **Edge case:** Αν η εικόνα είναι μεγαλύτερη από 5 MB, σκεφτείτε να τη μειώσετε πρώτα. Οι μεγάλες εικόνες αυξάνουν την κατανάλωση μνήμης και μπορούν να επιβραδύνουν τη μηχανή αναγνώρισης.

## Βήμα 4 – Αναγνώριση Κειμένου και Καταγραφή του Ακατέργαστου Αποτελέσματος

Με τη μηχανή έτοιμη και την εικόνα στη μνήμη, η πραγματική αναγνώριση είναι μια γραμμή κώδικα:

```java
// Perform OCR and store the raw text
String rawText = ocrEngine.recognize(inputImage);
```

Η μέθοδος `recognize` επιστρέφει ένα `String` που περιέχει το **extract text from image** ακριβώς όπως το είδε η μηχανή—χωρίς spell‑checking, χωρίς post‑processing.

## Βήμα 5 – Εμφάνιση του Αποτελέσματος (Χωρίς Spell‑Check)

Τέλος, ας εκτυπώσουμε το ακατέργαστο OCR output στην κονσόλα ώστε να το επαληθεύσετε:

```java
System.out.println("Raw OCR (no spell‑check):\n" + rawText);
```

Όταν τρέξετε το πρόγραμμα, θα πρέπει να δείτε κάτι σαν:

```
Raw OCR (no spell‑check):
Hello, 世界!
12345
```

Αν η εικόνα περιείχε πολυγλωσσικά κείμενα ή ειδικά σύμβολα, θα εμφανιστούν αμετάβλητα επειδή απενεργοποιήσαμε τον spell corrector.

## Πλήρες, Εκτελέσιμο Παράδειγμα

Συνδυάζοντας όλα τα κομμάτια, εδώ είναι το **complete Aspose OCR Java example** που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα αρχείο `SpellCorrectionDemo.java`:

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.Image;

public class SpellCorrectionDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Turn off the built‑in spell corrector
        ocrEngine.getSpellCorrector().setEnabled(false);

        // Step 3: Load the image you want to recognize
        Image inputImage = Image.load("YOUR_DIRECTORY/mixed-lang.png");

        // Step 4: Run OCR on the image and obtain the raw text
        String rawText = ocrEngine.recognize(inputImage);

        // Step 5: Display the OCR result without spell‑checking
        System.out.println("Raw OCR (no spell‑check):\n" + rawText);
    }
}
```

### Πώς να Εκτελέσετε

1. Αποθηκεύστε το αρχείο ως `SpellCorrectionDemo.java`.  
2. Συγκεντρώστε: `javac -cp "path/to/aspose-ocr-23.9.jar" SpellCorrectionDemo.java`  
3. Εκτελέστε: `java -cp ".;path/to/aspose-ocr-23.9.jar" SpellCorrectionDemo`

Αντικαταστήστε το `path/to` με την πραγματική θέση του Aspose JAR στο σύστημά σας.

## Συχνές Ερωτήσεις & Προβλήματα

### Τι γίνεται αν η εικόνα είναι σε διαφορετική μορφή (π.χ., PDF);

Το Aspose OCR μπορεί επίσης να διαβάσει σελίδες PDF απευθείας, αλλά θα χρειαστεί να μετατρέψετε τη σελίδα PDF σε εικόνα πρώτα ή να χρησιμοποιήσετε την υπερφόρτωση `OcrEngine.recognizePdf`. Είναι ένα διαφορετικό tutorial, αλλά η ίδια αρχή **recognize text from image** ισχύει.

### Επηρεάζει η απενεργοποίηση του spell corrector την απόδοση;

Λίγο. Η παράλειψη του λεξικού βήματος εξοικονομεί μερικά χιλιοστά του δευτερολέπτου ανά σελίδα, κάτι που μπορεί να αθροιστεί όταν επεξεργάζεστε χιλιάδες αρχεία. Η ανταλλαγή είναι η απώλεια αυτόματων διορθώσεων τυπογραφικών λαθών—οπότε αποφασίστε βάσει της ποιότητας των δεδομένων σας.

### Μπορώ ακόμα να λάβω αποτελέσματα ειδικά για γλώσσες;

Ναι. Η μηχανή ανιχνεύει αυτόματα το script, αλλά μπορείτε να εξαναγκάσετε μια γλώσσα καλώντας `ocrEngine.setLanguage(OcrEngine.Language.English)`, για παράδειγμα. Αυτό είναι χρήσιμο όταν ξέρετε ότι η εικόνα περιέχει μόνο μία γλώσσα και θέλετε να βελτιώσετε την ακρίβεια.

### Πώς να διαχειριστώ πολυ‑σελίδες TIFF;

Θεωρήστε κάθε σελίδα ως ξεχωριστό αντικείμενο `Image`: `Image.load("file.tif", pageIndex)`. Επανάληψη στις σελίδες, αναγνώριση της κάθε μιας, και συνένωση των αποτελεσμάτων.

## Συμβουλές για Πραγματικά Έργα

- **Batch processing:** Τυλίξτε τη λογική OCR σε μια μέθοδο που δέχεται `InputStream`. Αυτό σας επιτρέπει να μεταφέρετε εικόνες από S3, Azure Blob, ή οποιοδήποτε άλλο αποθηκευτικό χώρο χωρίς να αγγίζετε το σύστημα αρχείων.  
- **Memory management:** Καλέστε `ocrEngine.dispose()` μετά το τέλος για να ελευθερώσετε τους εγγενείς πόρους.  
- **Logging:** Καταγράψτε το ακατέργαστο output σε αρχείο καταγραφής για audit trails—ιδιαίτερα σημαντικό όταν έχετε απενεργοποιήσει το spell correction.  
- **Testing:** Γράψτε unit test που τροφοδοτεί μια γνωστή εικόνα και ελέγχει το αναμενόμενο ακατέργαστο string. Εξασφαλίζει ότι μελλοντικές αναβαθμίσεις της βιβλιοθήκης δεν αλλάζουν σιωπηρά τη συμπεριφορά.

## Συμπέρασμα

Σας δείξαμε πώς να **recognize text from image** χρησιμοποιώντας Aspose OCR για Java, πώς να **load image for OCR**, και τα ακριβή βήματα για **turn off spell corrector** όταν χρειάζεστε τους αμετάβλητους χαρακτήρες. Το σύντομο, αυτόνομο code snippet παραπάνω είναι έτοιμο να ενσωματωθεί σε οποιοδήποτε Java project, και οι εξηγήσεις σας δίνουν το “γιατί” πίσω από κάθε γραμμή.

Στη συνέχεια, ίσως θελήσετε να εξερευνήσετε **extract text from image** μαζικά, να πειραματιστείτε με hints γλώσσας, ή να ενσωματώσετε το αποτέλεσμα σε ευρετήριο αναζήτησης. Ό,τι και αν επιλέξετε, τα θεμέλια που καλύψαμε εδώ θα κρατήσουν την OCR pipeline σας αξιόπιστη και εύκολη στη συντήρηση.

Έχετε κάποιο twist που δοκιμάζετε; Μη διστάσετε να αφήσετε σχόλιο ή να μοιραστείτε το δικό σας **Aspose OCR Java example**. Καλή κωδικοποίηση!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}