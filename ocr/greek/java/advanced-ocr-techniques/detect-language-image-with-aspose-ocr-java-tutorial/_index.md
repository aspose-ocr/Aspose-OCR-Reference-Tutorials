---
category: general
date: 2026-10-08
description: Μάθετε πώς να OCR εικόνα σε κείμενο σε Java χρησιμοποιώντας το Aspose
  OCR. Αυτός ο οδηγός βήμα‑βήμα καλύπτει την ανίχνευση γλώσσας, την εξαγωγή κειμένου
  από PNG και την αποθήκευση των αποτελεσμάτων.
draft: false
keywords:
- ocr image to text java
- aspose ocr java tutorial
- detect language image
- extract text image
- read text png
lastmod: 2026-10-08
og_description: OCR εικόνα σε κείμενο σε Java με Aspose OCR – ένας γρήγορος οδηγός
  που δείχνει πώς να εντοπίσετε τη γλώσσα σε μια εικόνα, να εξάγετε το κείμενο και
  να το αποθηκεύσετε. Λάβετε τη ανιχνευμένη γλώσσα σε δευτερόλεπτα.
og_image_alt: Screenshot of Java OCR image to text output using Aspose OCR
og_title: OCR εικόνα σε κείμενο σε Java χρησιμοποιώντας το Aspose OCR – πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-10-08'
  description: Learn how to OCR image to text in Java using Aspose OCR. This step‑by‑step
    tutorial covers language detection, extracting text from PNGs, and saving results.
  headline: How to OCR image to text in Java with Aspose OCR
  type: TechArticle
- questions:
  - answer: Yes. Aspose OCR supports PNG, JPEG, BMP, TIFF, and GIF—just change the
      file extension in `setImage`.
    question: Does this work with JPEG or BMP files?
  - answer: The engine returns the primary language, but you can call `process()`
      on separate regions to capture each script individually.
    question: Can I detect more than one language in the same image?
  - answer: Aspose OCR excels with printed fonts; for handwritten text you’ll need
      a specialized model such as Azure Cognitive Services.
    question: What if the image contains handwritten text?
  - answer: Loop over a directory, reuse a single `OcrEngine` instance, and write
      each result to its own `.txt` file to minimise memory overhead.
    question: How do I handle very large image batches?
  - answer: Yes, a valid Aspose OCR license is needed for production use; a free 30‑day
      trial is available for evaluation.
    question: Is a commercial license required for production?
  type: FAQPage
tags:
- OCR
- Java
- Aspose OCR
- image language detection
- ocr image to text
title: Πώς να OCR εικόνα σε κείμενο σε Java με Aspose OCR
url: /el/java/advanced-ocr-techniques/detect-language-image-with-aspose-ocr-java-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR εικόνα σε κείμενο σε Java με Aspose OCR

Αν χρειάζεστε **ocr image to text in Java** και επίσης θέλετε να ανακαλύψετε ποια γλώσσα περιέχει η εικόνα, το Aspose OCR το κάνει εύκολο. Σε αυτό το tutorial θα μάθετε πώς να ρυθμίσετε τη μηχανή, να ενεργοποιήσετε την αυτόματη ανίχνευση γλώσσας, να εξάγετε κείμενο που μπορεί να αναζητηθεί από ένα PNG και να ανακτήσετε τον κωδικό της ανιχνευμένης γλώσσας — όλα χωρίς να γράψετε ένα προσαρμοσμένο μοντέλο μηχανικής μάθησης.

## Γρήγορες απαντήσεις
- **Ποια βιβλιοθήκη διαχειρίζεται πολυγλωσσικό OCR σε Java;** Aspose OCR for Java.
- **Πόσες γλώσσες υποστηρίζει η αυτόματη ανίχνευση;** Over 100 built‑in scripts.
- **Ποια έκδοση της Java απαιτείται;** Java 17 or newer.
- **Χρειάζομαι άδεια για δοκιμές;** A free 30‑day trial works for demos.
- **Μπορώ να αποθηκεύσω το αποτέλεσμα σε αρχείο;** Yes, using standard Java I/O.

## Τι είναι το OCR image to text σε Java;

Το OCR image to text σε Java σημαίνει τη λήψη μιας bitmap εικόνας που περιέχει τυπωμένους χαρακτήρες και τη μετατροπή αυτών των οπτικών γλυφών σε μια συμβολοσειρά Unicode που μπορεί να επεξεργαστεί, να αναζητηθεί ή να υποστεί περαιτέρω επεξεργασία. Η μηχανή Aspose OCR διαβάζει τα δεδομένα εικονοστοιχείων, αναγνωρίζει τα σχήματα των χαρακτήρων και εξάγει το αντίστοιχο κείμενο χωρίς την ανάγκη εξωτερικών υπηρεσιών.

## Γιατί να χρησιμοποιήσετε το Aspose OCR για ανίχνευση γλώσσας;

Το Aspose OCR υποστηρίζει περισσότερα από 50 μορφές εικόνας και μπορεί αυτόματα να αναγνωρίσει πάνω από 100 γλώσσες, καθιστώντας το μια ευέλικτη επιλογή για πολυγλωσσικά έγγραφα. Επεξεργάζεται μεγάλα αρχεία σελίδα‑με‑σελίδα χωρίς να φορτώνει ολόκληρο το έγγραφο στη μνήμη, παρέχοντας αποτελέσματα έως και τρεις φορές πιο γρήγορα από πολλές ανοιχτού κώδικα εναλλακτικές ενώ διατηρεί υψηλή ακρίβεια.

## Πώς να ρυθμίσετε το έργο σας και να εισάγετε το Aspose OCR

Για να ξεκινήσετε, προσθέστε τη βιβλιοθήκη Aspose OCR στη διαμόρφωση της κατασκευής σας ώστε οι κλάσεις να είναι διαθέσιμες στο classpath. Χρησιμοποιώντας Maven, συμπεριλάβετε το απόσπασμα εξάρτησης στο `pom.xml`· με Gradle, προσθέστε την αντίστοιχη γραμμή στο `build.gradle`. Μετά την ανανέωση του έργου, μπορείτε να εισάγετε τις κλάσεις OCR στα αρχεία πηγαίου κώδικα Java.

**Απάντηση:** Προσθέστε την εξάρτηση Aspose OCR στο `pom.xml`, ανανεώστε το έργο και η βιβλιοθήκη θα είναι διαθέσιμη στο classpath για άμεση χρήση.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.10</version>
</dependency>
```
```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- latest as of Feb 2026 -->
</dependency>
```

Αν προτιμάτε Gradle, χρησιμοποιήστε τις αντίστοιχες συντεταγμένες:

```gradle
implementation 'com.aspose:aspose-ocr:24.10'
```
```gradle
// build.gradle
implementation 'com.aspose:aspose-ocr:23.10'
```

> **Συμβουλή:** Διατηρήστε τη βιβλιοθήκη ενημερωμένη· κάθε νέα έκδοση προσθέτει περισσότερα σενάρια στη λίστα αυτόματης ανίχνευσης.

Τώρα δημιουργήστε μια απλή κλάση Java με όνομα `AutoLangDemo`. Αυτό το αρχείο θα περιέχει το πλήρες εκτελέσιμο παράδειγμα.

## Πώς να αρχικοποιήσετε τη μηχανή OCR για αυτόματη ανίχνευση γλώσσας

`OcrEngine` είναι η βασική κλάση στο Aspose OCR που εκτελεί την αναγνώριση στις παρεχόμενες εικόνες.

**Απάντηση:** Δημιουργήστε μια παρουσία του `OcrEngine`, ενεργοποιήστε την επιλογή `OcrLanguage.AUTO_DETECT` και προαιρετικά προσαρμόστε τις `EngineOptions` όπως ανάλυση ή φίλτρα προεπεξεργασίας. Αυτή η διαμόρφωση επιτρέπει στη μηχανή να καθορίζει αυτόματα το σενάριο της εισερχόμενης εικόνας και να εφαρμόζει το πιο κατάλληλο μοντέλο γλώσσας, απλοποιώντας την πολυγλωσσική επεξεργασία με λίγες μόνο γραμμές κώδικα.

```java
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getEngineOptions().setLanguage(OcrLanguage.AUTO_DETECT);
ocrEngine.setImage(new File("multilang.png"));
```
```java
import com.aspose.ocr.*;

public class AutoLangDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Load the image that contains multiple languages
        String imagePath = "YOUR_DIRECTORY/multilang.png";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 2.3: Enable automatic language detection
        ocrEngine.getEngineOptions().setLanguage(OcrLanguage.AUTO_DETECT);

        // Step 2.4: Perform OCR processing on the image
        OcrResult ocrResult = ocrEngine.process();

        // Step 2.5: Output the detected language and extracted text
        System.out.println("Detected language: " + ocrResult.getDetectedLanguage());
        System.out.println(ocrResult.getText());
    }
}
```

## Πώς να εκτελέσετε το demo και να επαληθεύσετε το αποτέλεσμα

`process()` εκτελεί τη λειτουργία OCR στην φορτωμένη εικόνα και γεμίζει τις ιδιότητες αποτελέσματος της μηχανής.

**Απάντηση:** Μετά την κλήση του `ocrEngine.process()`, ανακτήστε το αναγνωρισμένο κείμενο μέσω `ocrEngine.getText()` και τον αναγνωριστικό γλώσσας με `ocrEngine.getDetectedLanguage()`. Εκτυπώστε και τις δύο τιμές στην κονσόλα ή καταγράψτε τις για επαλήθευση. Αυτή η άμεση ανάδραση επιβεβαιώνει ότι η μηχανή ερμήνευσε σωστά την εικόνα και εντόπισε την κύρια γλώσσα, επιτρέποντάς σας να διαχειριστείτε τυχόν βήματα μετα‑επεξεργασίας.

```java
if (ocrEngine.process()) {
    System.out.println("Detected language: " + ocrEngine.getDetectedLanguage());
    System.out.println("Extracted text: " + ocrEngine.getText());
}
```
```bash
mvn compile exec:java -Dexec.mainClass=AutoLangDemo
```

Αν όλα έχουν ρυθμιστεί σωστά, θα δείτε κάτι όπως:

```text
Detected language: en
Extracted text: Hello world! This is a sample.
```
```
Detected language: en
Hello World!
Bonjour le monde!
Hola Mundo!
```

Η κονσόλα εκτυπώνει τη **detected language** (`en` για Αγγλικά) ακολουθούμενη από το **extracted text**. Ανάλογα με την εικόνα, ο κωδικός γλώσσας μπορεί να είναι `fr`, `es`, `de`, κ.λπ.

> **Why this works:** Το Aspose OCR σαρώει το bitmap, αξιολογεί τα σύνολα χαρακτήρων και επιλέγει τη πιο πιθανή γλώσσα από το ενσωματωμένο λεξικό του. Ορίζοντας το `OcrLanguage.AUTO_DETECT`, αφήνετε τη μηχανή να αναλάβει το βαριά έργο.

## Πώς να αντιμετωπίσετε περιπτώσεις άκρων όταν η ανίχνευση αποτυγχάνει

`BufferedImage` είναι μια κλάση Java που αντιπροσωπεύει μια εικόνα στη μνήμη, παρέχοντας πρόσβαση σε επίπεδο pixel για επεξεργασία.

**Απάντηση:** Εάν η μηχανή OCR αποτύχει να εντοπίσει τη σωστή γλώσσα, βελτιώστε πρώτα την ποιότητα εισόδου. Μεγεθύνετε θολές εικόνες με `BufferedImage.getScaledInstance` ή εφαρμόστε φίλτρα ενίσχυσης μέσω `ConvolveOp`. Για έγγραφα που περιέχουν πολλαπλά σενάρια, χωρίστε την εικόνα σε περιοχές χρησιμοποιώντας `ocrEngine.setRegion(Rectangle)` και επεξεργαστείτε κάθε μία ξεχωριστά. Ως εναλλακτική, ορίστε ρητά μια συγκεκριμένη γλώσσα με `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.<YOUR_LANG>)`.

## Πώς να αποθηκεύσετε το εξαγόμενο κείμενο για μελλοντική χρήση

`FileWriter` είναι μια κλάση Java που χρησιμοποιείται για να γράφει ροές χαρακτήρων απευθείας σε αρχείο στο δίσκο.

**Απάντηση:** Γράψτε το αποτέλεσμα OCR σε αρχείο δημιουργώντας ένα `FileWriter` ή χρησιμοποιώντας `Files.writeString` για μια πιο απλή προσέγγιση. Αποθηκεύστε το κείμενο σε αρχείο `.txt`, το οποίο μπορεί αργότερα να τροφοδοτηθεί σε υπηρεσίες μετάφρασης, ευρετήρια αναζήτησης ή αγωγούς ανάλυσης δεδομένων. Βεβαιωθείτε ότι διαχειρίζεστε τις εξαιρέσεις και κλείνετε το writer για να αποφύγετε διαρροές πόρων.

```java
try (Writer writer = new BufferedWriter(new FileWriter("output.txt"))) {
    writer.write(ocrEngine.getText());
}
```
```java
import java.nio.file.*;

Path outPath = Paths.get("output.txt");
Files.writeString(outPath, ocrResult.getText(), StandardOpenOption.CREATE);
System.out.println("Text saved to " + outPath.toAbsolutePath());
```

Τώρα δεν έχετε μόνο **detect language image** και **extract text image**, αλλά έχετε επίσης ένα μόνιμο αντίγραφο που μπορείτε να τροφοδοτήσετε σε ευρετήρια αναζήτησης, APIs μετάφρασης ή αγωγούς δεδομένων.

## Πλήρες λειτουργικό παράδειγμα – όλα τα βήματα συνδυασμένα

Παρακάτω βρίσκεται ο πλήρης, έτοιμος‑για‑εκτέλεση κώδικας. Αντιγράψτε‑και‑επικολλήστε το στο `src/main/java/AutoLangDemo.java` και εκτελέστε το.

**Απάντηση:** Το παρακάτω πρόγραμμα δημιουργεί ένα `OcrEngine`, ενεργοποιεί το auto‑detect, επεξεργάζεται ένα PNG, εκτυπώνει τον κωδικό γλώσσας και το εξαγόμενο κείμενο, και τελικά γράφει το κείμενο στο `output.txt`.

```java
public class AutoLangDemo {
    public static void main(String[] args) throws Exception {
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getEngineOptions().setLanguage(OcrLanguage.AUTO_DETECT);
        ocrEngine.setImage(new File("multilang.png"));

        if (ocrEngine.process()) {
            System.out.println("Detected language: " + ocrEngine.getDetectedLanguage());
            System.out.println("Extracted text: " + ocrEngine.getText());

            try (Writer writer = new BufferedWriter(new FileWriter("output.txt"))) {
                writer.write(ocrEngine.getText());
            }
        } else {
            System.err.println("OCR processing failed.");
        }
    }
}
```
```java
import com.aspose.ocr.*;
import java.nio.file.*;

public class AutoLangDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load multi‑language PNG (replace with your actual path)
        String imagePath = "YOUR_DIRECTORY/multilang.png";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // 3️⃣ Auto‑detect language – this is the heart of detect language image
        ocrEngine.getEngineOptions().setLanguage(OcrLanguage.AUTO_DETECT);

        // 4️⃣ Run OCR
        OcrResult ocrResult = ocrEngine.process();

        // 5️⃣ Show detected language and extracted text
        System.out.println("Detected language: " + ocrResult.getDetectedLanguage());
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());

        // 6️⃣ Persist the text (optional)
        Path outPath = Paths.get("output.txt");
        Files.writeString(outPath, ocrResult.getText(), StandardOpenOption.CREATE);
        System.out.println("Saved extracted text to " + outPath.toAbsolutePath());
    }
}
```

**Αναμενόμενη έξοδος κονσόλας**

```text
Detected language: en
Extracted text: This is a sample multi‑language image.
```
```
Detected language: fr
=== Extracted Text ===
Bonjour le monde!
Hello World!
¡Hola Mundo!
```

Ο ακριβής κωδικός γλώσσας θα διαφέρει ανάλογα με το περιεχόμενο της εικόνας, αλλά το μοτίβο παραμένει το ίδιο.

## Συχνές ερωτήσεις

**Ε: Λειτουργεί αυτό με αρχεία JPEG ή BMP;**  
Ναι. Το Aspose OCR υποστηρίζει PNG, JPEG, BMP, TIFF και GIF — απλώς αλλάξτε την επέκταση αρχείου στο `setImage`.

**Ε: Μπορώ να ανιχνεύσω περισσότερες από μία γλώσσες στην ίδια εικόνα;**  
Η μηχανή επιστρέφει την κύρια γλώσσα, αλλά μπορείτε να καλέσετε `process()` σε ξεχωριστές περιοχές για να καταγράψετε κάθε σενάριο ξεχωριστά.

**Ε: Τι γίνεται αν η εικόνα περιέχει χειρόγραφο κείμενο;**  
Το Aspose OCR διαπρέπει με τυπωμένες γραμματοσειρές· για χειρόγραφο κείμενο θα χρειαστείτε ένα εξειδικευμένο μοντέλο όπως το Azure Cognitive Services.

**Ε: Πώς να διαχειριστώ πολύ μεγάλες δέσμες εικόνων;**  
Κάντε βρόχο πάνω από έναν φάκελο, επαναχρησιμοποιήστε μια ενιαία παρουσία `OcrEngine` και γράψτε κάθε αποτέλεσμα σε δικό του αρχείο `.txt` για να ελαχιστοποιήσετε τη χρήση μνήμης.

**Ε: Απαιτείται εμπορική άδεια για παραγωγή;**  
Ναι, απαιτείται έγκυρη άδεια Aspose OCR για χρήση σε παραγωγή· ένα δωρεάν δοκιμαστικό 30‑ημέρας είναι διαθέσιμο για αξιολόγηση.

## Συμπέρασμα

Τώρα έχετε μια ολοκληρωμένη, από‑αρχή‑μέχρι‑τέλος συνταγή για **detect language image**, **extract text image**, και **ocr image to text** χρησιμοποιώντας το Aspose OCR για Java. Ενεργοποιώντας το `OcrLanguage.AUTO_DETECT` αφήνετε τη βιβλιοθήκη να λαμβάνει αυτόματα **get detected language**, και με μερικές επιπλέον γραμμές μπορείτε να **read text png**, αποθηκεύσετε το αποτέλεσμα και να διαχειριστείτε κοινές περιπτώσεις άκρων.

Επόμενα βήματα; Τροφοδοτήστε το εξαγόμενο κείμενο στο API του Google Translate, ευρετηριάστε το με Elasticsearch για αναζητήσιμα PDF, ή επεξεργαστείτε μαζικά ολόκληρο φάκελο εικόνων. Πειραματιστείτε με τις `EngineOptions` για να ρυθμίσετε την ταχύτητα έναντι της ακρίβειας για το συγκεκριμένο φορτίο εργασίας σας.

Καλό κώδικο, και οι OCR αγωγοί σας να είναι πάντα ακριβείς!  

---

![παράδειγμα εικόνας ανίχνευσης γλώσσας](detect-language-image.png "παράδειγμα εικόνας ανίχνευσης γλώσσας")
[παράδειγμα εικόνας ανίχνευσης γλώσσας](detect-language-image.png "παράδειγμα εικόνας ανίχνευσης γλώσσας")

**Τελευταία ενημέρωση:** 2026-10-08  
**Δοκιμή με:** Aspose OCR for Java 24.10  
**Συγγραφέας:** Aspose

## Σχετικά μαθήματα

- [Ανίχνευση γλώσσας εικόνας με το Aspose Ocr Java Tutorial](/ocr/java/advanced-ocr-techniques/detect-language-image-with-aspose-ocr-java-tutorial/)
- [Ανάγνωση κειμένου από εικόνα σε Java – Πλήρης οδηγός Aspose Ocr](/ocr/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Εξαγωγή κειμένου από εικόνα Java με Aspose.OCR Detect Areas Mode](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}