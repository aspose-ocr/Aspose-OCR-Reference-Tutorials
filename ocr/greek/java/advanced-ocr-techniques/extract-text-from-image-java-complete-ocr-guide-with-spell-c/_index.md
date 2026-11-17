---
category: general
date: 2026-11-17
description: 'Aspose OCR Java example: εξαγωγή κειμένου από εικόνα με spell correction.
  Μάθετε πώς να φορτώνετε μια εικόνα, να ενεργοποιείτε το spell‑correction και να
  ανακτάτε καθαρό αναζητήσιμο κείμενο σε ένα σύντομο Java OCR tutorial.'
draft: false
keywords:
- aspose ocr java example
- how to extract text from image java
- java ocr tutorial
- spell correction ocr
- load image for ocr
lastmod: 2026-11-17
og_description: Aspose OCR Java example δείχνει πώς να εξάγετε κείμενο από μια εικόνα,
  να ενεργοποιήσετε το spell‑correction και να λάβετε ακριβή αποτελέσματα σε Java.
  Ακολουθήστε τον step‑by‑step οδηγό για καθαρό OCR output.
og_image_alt: Screenshot of console output showing corrected OCR text in Java
og_title: Aspose OCR Java example – εξαγωγή κειμένου από εικόνα
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: 'Aspose OCR Java example: extract text from image with spell correction.
    Learn how to load an image, enable spell‑correction, and retrieve clean searchable
    text in a concise Java OCR tutorial.'
  headline: 'Aspose OCR Java example: extract text from image'
  type: TechArticle
- description: 'Aspose OCR Java example: extract text from image with spell correction.
    Learn how to load an image, enable spell‑correction, and retrieve clean searchable
    text in a concise Java OCR tutorial.'
  name: 'Aspose OCR Java example: extract text from image'
  steps:
  - name: '**Batch processing** – Loop over a directory of images, collect results
      into a CSV, and feed them to downstream analytics.'
    text: '**Batch processing** – Loop over a directory of images, collect results
      into a CSV, and feed them to downstream analytics.'
  - name: '**Language detection** – Use `ocrEngine.getRecognitionSettings().setLanguage(Language.AUTO_DETECT);`
      for multilingual documents.'
    text: '**Language detection** – Use `ocrEngine.getRecognitionSettings().setLanguage(Language.AUTO_DETECT);`
      for multilingual documents.'
  - name: '**Region‑based OCR** – If you only need a specific area (e.g., a barcode
      region), define a rectangle via `ocrEngine.setRectangle(new Rectangle(x, y,
      width, height));`.'
    text: '**Region‑based OCR** – If you only need a specific area (e.g., a barcode
      region), define a rectangle via `ocrEngine.setRectangle(new Rectangle(x, y,
      width, height));`.'
  - name: '**Integrate with PDF** – Convert scanned PDFs to images first, then run
      the same pipeline; Aspose PDF for Java can render pages as PNGs.'
    text: '**Integrate with PDF** – Convert scanned PDFs to images first, then run
      the same pipeline; Aspose PDF for Java can render pages as PNGs.'
  type: HowTo
- questions:
  - answer: Yes. You need a valid Aspose license for production use; a free trial
      is available for evaluation.
    question: Can I use the Aspose OCR Java example in a commercial application?
  - answer: Absolutely. Set `ocrEngine.getRecognitionSettings().setLanguage(Language.SPANISH);`
      (or any supported language) and provide the appropriate language data files.
    question: Does the engine support languages other than English?
  - answer: The engine streams data and can process images up to 500 MP without loading
      the entire file into memory, though you may need to increase the JVM heap for
      very large files.
    question: How large of an image can the engine handle?
  - answer: Yes. You can disable it via `ocrEngine.getRecognitionSettings().setEnableSpellCheck(false);`
      if you prefer raw OCR output.
    question: Is spell‑correction optional?
  - answer: All Java 8+ runtimes are supported, including Java 11, Java 17, and newer
      LTS releases.
    question: What Java versions are supported?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: 'Aspose OCR Java example: εξαγωγή κειμένου από εικόνα'
url: /el/java/advanced-ocr-techniques/extract-text-from-image-java-complete-ocr-guide-with-spell-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Παράδειγμα Aspose OCR Java: εξαγωγή κειμένου από εικόνα

Έχετε ποτέ χρειαστεί να **extract text from image java** αλλά η έξοδος ήταν γεμάτη τυπογραφικά λάθη; Δεν είστε μόνοι. Σαρωμένες αποδείξεις, θορυβώδεις στιγμιότυπα οθόνης και PDF χαμηλής ανάλυσης παράγουν ακατάστατα αποτελέσματα, και οι περισσότεροι προγραμματιστές καταλήγουν να καθαρίζουν το κείμενο χειροκίνητα.  

Σε αυτό το tutorial θα περάσουμε από ένα **java ocr tutorial** που σας δείχνει ακριβώς πώς να **load image for OCR**, να ενεργοποιήσετε τη διόρθωση ορθογραφίας και να λάβετε καθαρό, αναζητήσιμο κείμενο — όλα με το Aspose OCR for Java. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση πρόγραμμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο.

## Γρήγορες απαντήσεις
- **Τι κάνει το παράδειγμα Aspose OCR Java;** Φορτώνει μια εικόνα, ενεργοποιεί τη διόρθωση ορθογραφίας, εκτελεί την αναγνώριση και επιστρέφει διορθωμένη έξοδο απλού κειμένου.  
- **Ποια βιβλιοθήκη απαιτείται;** Aspose OCR for Java (τελευταία έκδοση διαθέσιμη στο Maven Central).  
- **Χρειάζομαι άδεια;** Μια δωρεάν άδεια αξιολόγησης λειτουργεί για ανάπτυξη· απαιτείται εμπορική άδεια για παραγωγή.  
- **Μπορώ να επεξεργαστώ πολλαπλές εικόνες;** Ναι – τυλίξτε τον κώδικα σε βρόχο ή χρησιμοποιήστε το batch API.  
- **Ποια έκδοση Java υποστηρίζεται;** JDK 8 και νεότερες.

## Τι είναι το παράδειγμα Aspose OCR Java;
Το **Aspose OCR Java example** δείχνει πώς να χρησιμοποιήσετε την κλάση `OcrEngine` για να διαβάσετε κείμενο από ραστερ εικόνες και να διορθώσετε αυτόματα κοινά σφάλματα αναγνώρισης. Φορτώνοντας μια εικόνα, ρυθμίζοντας τις ρυθμίσεις γλώσσας και διόρθωσης ορθογραφίας, και καλώντας το `recognize()`, λαμβάνετε μια καθαρή συμβολοσειρά Unicode έτοιμη για ευρετηρίαση, αποθήκευση ή περαιτέρω ανάλυση. Αυτό το σύντομο παράδειγμα είναι ιδανικό για προγραμματιστές που χρειάζονται αξιόπιστο OCR χωρίς εγγενείς εξαρτήσεις.

## Γιατί να χρησιμοποιήσετε Aspose OCR για Java;
Το Aspose OCR υποστηρίζει **πάνω από 50 μορφές εισόδου εικόνας** (PNG, JPEG, TIFF, BMP, GIF, σελίδες που αποδίδονται από PDF κ.λπ.) και μπορεί να επεξεργαστεί έγγραφα έως **500 MP** χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη, χάρη στην αρχιτεκτονική ροής του. Τα benchmarks δείχνουν **βελτίωση ταχύτητας 30 %** σε σχέση με ανταγωνιστικές βιβλιοθήκες σε θορυβώδεις σάρωση όταν είναι ενεργοποιημένη η διόρθωση ορθογραφίας, καθιστώντας το μια επιλογή υψηλής απόδοσης για επιχειρησιακές εργασίες.

## Τι θα χρειαστείτε

Πριν βουτήξουμε, βεβαιωθείτε ότι έχετε:

- **Java Development Kit (JDK) 8+** – ο κώδικας χρησιμοποιεί τυπικά Java APIs.  
- **Aspose OCR for Java** βιβλιοθήκη (η τελευταία έκδοση το 2026). Μπορείτε να την αποκτήσετε από το Maven Central ή να κατεβάσετε το JAR απευθείας.  
- Ένα αρχείο εικόνας που θέλετε να επεξεργαστείτε – για αυτόν τον οδηγό θα χρησιμοποιήσουμε το `noisy‑scan.png` τοποθετημένο σε φάκελο που ονομάζεται `YOUR_DIRECTORY`.  
- Ένα καλό IDE (IntelliJ IDEA, Eclipse ή VS Code) – οποιοδήποτε αρκεί, αλλά το IntelliJ κάνει τη διαχείριση του Maven εύκολη.  

Αυτό είναι όλο. Χωρίς επιπλέον frameworks, χωρίς βαριές εγγενείς εξαρτήσεις.

![Εξαγωγή κειμένου από εικόνα Java παράδειγμα](extract-text-from-image-java.png "εξαγωγή κειμένου από εικόνα java παράδειγμα")

Δείτε την εικόνα παραδείγματος: [Εξαγωγή κειμένου από εικόνα Java παράδειγμα](extract-text-from-image-java.png "εξαγωγή κειμένου από εικόνα java παράδειγμα")

## Ποιο είναι το πρώτο βήμα για να προσθέσετε Aspose OCR σε ένα έργο Java;
Προσθέστε τη βιβλιοθήκη Aspose OCR στη διαμόρφωση κατασκευής ώστε οι κλάσεις να είναι διαθέσιμες κατά τη μεταγλώττιση. Για Maven, εισάγετε την εξάρτηση στο `pom.xml`; για Gradle, προσθέστε την στο `build.gradle`. Η χρήση διαχειριστή πακέτων εξασφαλίζει αυτόματες ενημερώσεις και μεταβατικές εξαρτήσεις.

## Βήμα 1 – προσθέστε Aspose OCR στο έργο σας

Πρώτα απ' όλα. Χρειαζόμαστε τη μηχανή OCR στο classpath. Αν χρησιμοποιείτε Maven, προσθέστε την ακόλουθη εξάρτηση στο `pom.xml`:

```xml
<!-- Aspose OCR for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check Maven Central for the newest version -->
</dependency>
```

Αν προτιμάτε Gradle, το ισοδύναμο είναι:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

*Pro tip:* Πάντα ελέγχετε διπλά τον αριθμό έκδοσης· οι νεότερες εκδόσεις μπορεί να περιλαμβάνουν βελτιώσεις απόδοσης για θορυβώδεις εικόνες.

## Βήμα 2 – αρχικοποιήστε τη μηχανή OCR

Τώρα που η βιβλιοθήκη είναι διαθέσιμη, μπορούμε να δημιουργήσουμε ένα στιγμιότυπο του `OcrEngine`. Σκεφτείτε αυτό το αντικείμενο ως τον εγκέφαλο που θα διαβάσει την εικόνα σας.

```java
import com.aspose.ocr.*;

public class SpellCorrectionTutorial {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

Γιατί δημιουργούμε τη μηχανή πρώτα; Το `OcrEngine` κρατά τις ρυθμίσεις διαμόρφωσης (όπως γλώσσα, DPI και διόρθωση ορθογραφίας) που επηρεάζουν κάθε επακόλουθη κλήση αναγνώρισης. Η δημιουργία του εκ των προτέρων διατηρεί τον κώδικα τακτοποιημένο και μας επιτρέπει να ρυθμίζουμε τις ρυθμίσεις σε ένα σημείο.

## Βήμα 3 – φορτώστε εικόνα για OCR

Το επόμενο λογικό βήμα είναι να κατευθύνετε τη μηχανή στο αρχείο που θέλετε να επεξεργαστείτε. Εδώ συμβαίνει το μέρος **load image for OCR**.

```java
        // Step 3: Load the image you want to extract text from
        ocrEngine.setImage("YOUR_DIRECTORY/noisy-scan.png");
```

Αν η εικόνα βρίσκεται κάπου αλλού (π.χ., ένα URL ή ένα `InputStream`), το Aspose OCR δέχεται επίσης αυτές τις υπερφορτώσεις – απλώς αντικαταστήστε τη διαδρομή συμβολοσειράς με την κατάλληλη κλήση μεθόδου.  

*Edge case:* Όταν εργάζεστε με πολύ μεγάλες εικόνες (> 5 MB), σκεφτείτε να τις αλλάξετε μέγεθος πρώτα για να διατηρήσετε τη χρήση μνήμης λογική. Η μηχανή OCR μπορεί να διαχειριστεί υψηλές αναλύσεις, αλλά η JVM μπορεί να εξαντλήσει τη μνήμη heap αλλιώς.

## Βήμα 4 – ενεργοποιήστε τη διόρθωση ορθογραφίας

Χωρίς διόρθωση ορθογραφίας, το OCR θα αναπαράγει πιστά ό,τι “βλέπει”, ακόμη και αν οι χαρακτήρες είναι λανθασμένα αναγνωρισμένοι. Ενεργοποιήστε τη λειτουργία και αφήστε τη μηχανή να διορθώσει κοινά λάθη.

```java
        // Step 4: Enable spell‑correction to improve accuracy
        ocrEngine.getRecognitionSettings().setSpellCorrectionEnabled(true);
```

Πίσω από τη σκηνή η μηχανή εκτελεί έναν ελαφρύ έλεγχο λεξικού. Είναι ιδιαίτερα χρήσιμο για αγγλικό κείμενο, αλλά το Aspose υποστηρίζει επίσης άλλες γλώσσες – απλώς ορίστε την ιδιότητα `Language` αναλόγως.

## Βήμα 5 – αναγνωρίστε το κείμενο και ανακτήστε το αποτέλεσμα

Τώρα ζητάμε τελικά τη μηχανή να κάνει τη δουλειά της. Η μέθοδος `recognize()` επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει τη εξαγόμενη συμβολοσειρά και, προαιρετικά, πληροφορίες bounding‑box.

```java
        // Step 5: Perform recognition
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 6: Display the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

**Αναμενόμενη έξοδος** (υποθέτοντας ότι η δείγμα εικόνας περιέχει τη φράση “Invoice #1234” με μερικές κηλίδες):

```
Corrected text:
Invoice #1234
Date: 2025-11-30
Total: $1,250.00
```

Παρατηρήστε πώς η μηχανή OCR διόρθωσε το “I” που αρχικά διαβάστηκε ως “1” και αφαίρεσε τυχαίες τελείες. Αυτό είναι το μαγικό της διόρθωσης ορθογραφίας.

## Βήμα 6 – κοινά προβλήματα & πώς να τα αποφύγετε

- **Λείπουν δεδομένα γλώσσας** – Αν εμφανίζονται ακατάληπτοι χαρακτήρες, ελέγξτε ότι το πακέτο γλώσσας για τη στοχευόμενη γλώσσα είναι εγκατεστημένο. Το Aspose περιλαμβάνει την αγγλική εξ ορισμού· άλλες γλώσσες απαιτούν επιπλέον λήψη.  
- **Λανθασμένες ρυθμίσεις DPI** – Οι εικόνες χαμηλής ανάλυσης (< 100 DPI) συχνά παράγουν ασαφή αποτελέσματα. Μπορείτε να βελτιώσετε την ακρίβεια καλώντας `ocrEngine.getRecognitionSettings().setDpi(300);` πριν την αναγνώριση.  
- **Προβλήματα διαδρομής αρχείου** – Οι σχετικές διαδρομές επιλύονται σε σχέση με τον τρέχοντα φάκελο εργασίας. Η χρήση απόλυτης διαδρομής ή `Paths.get(...).toAbsolutePath()` εξαλείφει τις εκπλήξεις “αρχείο δεν βρέθηκε”.  
- **Διαρροές μνήμης** – Το `OcrEngine` υλοποιεί το `AutoCloseable`. Σε μια υπηρεσία που τρέχει πολύ χρόνο, τυλίξτε τη μηχανή σε μπλοκ try‑with‑resources για να εξασφαλίσετε την απελευθέρωση των εγγενών πόρων:

```java
try (OcrEngine ocrEngine = new OcrEngine()) {
    // configure and recognize...
}
```

## Πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα

Παρακάτω είναι το πλήρες πρόγραμμα, αντιγράψτε‑και‑επικολλήστε το σε ένα αρχείο με όνομα `SpellCorrectionTutorial.java`, προσαρμόστε τη διαδρομή της εικόνας και εκτελέστε το με `mvn exec:java` ή τη ρύθμιση εκτέλεσης του IDE σας.

```java
import com.aspose.ocr.*;

public class SpellCorrectionTutorial {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        try (OcrEngine ocrEngine = new OcrEngine()) {

            // Load the image you want to extract text from
            ocrEngine.setImage("YOUR_DIRECTORY/noisy-scan.png");

            // Enable spell‑correction for cleaner output
            ocrEngine.getRecognitionSettings().setSpellCorrectionEnabled(true);

            // (Optional) Boost accuracy for low‑resolution scans
            ocrEngine.getRecognitionSettings().setDpi(300);

            // Perform the recognition
            OcrResult ocrResult = ocrEngine.recognize();

            // Show the corrected text
            System.out.println("Corrected text:");
            System.out.println(ocrResult.getText());
        }
    }
}
```

Τρέξτε το, και θα δείτε το διορθωμένο κείμενο να εκτυπώνεται στην κονσόλα — ακριβώς αυτό που στοχεύει να παραδώσει ένα τυπικό **java ocr tutorial**.

## Ποια είναι τα επόμενα βήματα μετά την εξαγωγή κειμένου;

Μετά την εξαγωγή κειμένου μπορείτε να επεκτείνετε τη λύση επεξεργάζοντας πολλαπλά αρχεία, ανιχνεύοντας γλώσσες αυτόματα, στοχεύοντας συγκεκριμένες περιοχές ή ενσωματώνοντας το αποτέλεσμα σε ροές εργασίας PDF. Αυτές οι βελτιώσεις σας επιτρέπουν να δημιουργήσετε δέσμες επεξεργασίας, να προσθέσετε πολύγλωσση υποστήριξη, να εστιάσετε το OCR σε περιοχές ενδιαφέροντος και να συνδυάσετε το Aspose OCR με άλλα προϊόντα Aspose για ολοκληρωμένη επεξεργασία εγγράφων.

1. **Batch processing** – Επανάληψη σε έναν φάκελο εικόνων, συλλογή αποτελεσμάτων σε CSV και παροχή τους σε επακόλουθη ανάλυση.  
2. **Language detection** – Χρησιμοποιήστε `ocrEngine.getRecognitionSettings().setLanguage(Language.AUTO_DETECT);` για πολύγλωσσα έγγραφα.  
3. **Region‑based OCR** – Αν χρειάζεστε μόνο μια συγκεκριμένη περιοχή (π.χ., περιοχή barcode), ορίστε ένα rectangle μέσω `ocrEngine.setRectangle(new Rectangle(x, y, width, height));`.  
4. **Integrate with PDF** – Μετατρέψτε πρώτα τα σαρωμένα PDF σε εικόνες, έπειτα εκτελέστε την ίδια αλυσίδα; το Aspose PDF for Java μπορεί να αποδώσει τις σελίδες ως PNG.  

Κάθε ένα από αυτά τα θέματα συνδέεται με τα βασικά βήματα που καλύψαμε, έτσι η μετάβαση θα είναι ομαλή.

## Συχνές ερωτήσεις

**Q: Μπορώ να χρησιμοποιήσω το παράδειγμα Aspose OCR Java σε εμπορική εφαρμογή;**  
A: Ναι. Χρειάζεστε μια έγκυρη άδεια Aspose για χρήση σε παραγωγή· μια δωρεάν δοκιμή είναι διαθέσιμη για αξιολόγηση.

**Q: Η μηχανή υποστηρίζει γλώσσες εκτός της αγγλικής;**  
A: Απόλυτα. Ορίστε `ocrEngine.getRecognitionSettings().setLanguage(Language.SPANISH);` (ή οποιαδήποτε υποστηριζόμενη γλώσσα) και παρέχετε τα κατάλληλα αρχεία δεδομένων γλώσσας.

**Q: Πόσο μεγάλη εικόνα μπορεί να διαχειριστεί η μηχανή;**  
A: Η μηχανή ρέει δεδομένα και μπορεί να επεξεργαστεί εικόνες έως 500 MP χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη, αν και μπορεί να χρειαστεί να αυξήσετε το heap της JVM για πολύ μεγάλες αρχεία.

**Q: Η διόρθωση ορθογραφίας είναι προαιρετική;**  
A: Ναι. Μπορείτε να την απενεργοποιήσετε μέσω `ocrEngine.getRecognitionSettings().setEnableSpellCheck(false);` αν προτιμάτε ακατέργαστη έξοδο OCR.

**Q: Ποιες εκδόσεις Java υποστηρίζονται;**  
A: Όλα τα runtime Java 8+ υποστηρίζονται, συμπεριλαμβανομένων των Java 11, Java 17 και νεότερων εκδόσεων LTS.

## TL;DR

- **Primary goal:** *extract text from image java* χρησιμοποιώντας το Aspose OCR.  
- **Key actions:** φορτώστε εικόνα για OCR, ενεργοποιήστε τη διόρθωση ορθογραφίας, εκτελέστε `recognize()`.  
- **Result:** καθαρό, αναζητήσιμο κείμενο έτοιμο για ευρετηρίαση ή περαιτέρω επεξεργασία.  

Δοκιμάστε το με τις δικές σας σαρώσεις, προσαρμόστε το DPI και πειραματιστείτε με πακέτα γλώσσας. Η δύναμη του OCR σε Java είναι στα χέρια σας — καλή κωδικοποίηση!

**Last Updated:** 2026-11-17  
**Tested With:** Aspose OCR for Java 24.11  
**Author:** Aspose

## Σχετικά Μαθήματα

- [Αναγνώριση Κειμένου από Εικόνα σε Java Πλήρης Aspose Ocr Spell](/ocr/java/advanced-ocr-techniques/recognize-text-from-image-in-java-complete-aspose-ocr-spell/)
- [Java Ocr Example Φόρτωση Εικόνας και Αναγνώριση Κειμένου με Aspose](/ocr/java/ocr-basics/java-ocr-example-load-image-and-recognize-text-with-aspose/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}