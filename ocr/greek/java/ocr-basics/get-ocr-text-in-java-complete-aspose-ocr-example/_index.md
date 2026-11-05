---
category: general
date: 2026-11-04
description: Μάθετε πώς να χρησιμοποιείτε OCR σε Java με Aspose OCR. Αυτός ο οδηγός
  παρουσιάζει ένα java OCR example, πώς να εξάγετε κείμενο από μια σαρωμένη εικόνα
  και πώς να φορτώνετε image OCR αποδοτικά.
draft: false
keywords:
- how to use ocr
- image to text java
- java ocr example
- aspose ocr license
- extract text scanned image
lastmod: 2026-11-04
og_description: Πώς να χρησιμοποιήσετε OCR σε Java με Aspose OCR. Αυτό το tutorial
  παρέχει ένα java OCR example, δείχνει πώς να εξάγετε κείμενο από scanned images
  και εξηγεί τη φόρτωση image OCR με license.
og_image_alt: 'Developer guide: extract OCR text from images using Aspose OCR Java'
og_title: Πώς να χρησιμοποιήσετε OCR σε Java – πλήρες παράδειγμα Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-11-04'
  description: Learn how to use OCR in Java with Aspose OCR. This guide shows a java
    OCR example, how to extract text from a scanned image, and how to load image OCR
    efficiently.
  headline: How to use OCR in Java – complete Aspose OCR example
  type: TechArticle
- description: Learn how to use OCR in Java with Aspose OCR. This guide shows a java
    OCR example, how to extract text from a scanned image, and how to load image OCR
    efficiently.
  name: How to use OCR in Java – complete Aspose OCR example
  steps:
  - name: The file path in `setImage` (is it correct?).
    text: The file path in `setImage` (is it correct?).
  - name: The language code matches the script in the image.
    text: The language code matches the script in the image.
  - name: The image quality (contrast, DPI) is sufficient.
    text: The image quality (contrast, DPI) is sufficient.
  type: HowTo
- questions:
  - answer: Yes, a full **aspose ocr license** removes evaluation limits and enables
      all premium features.
    question: Do I need a paid license for production use?
  - answer: It supports printed and some cursive handwriting, but accuracy varies;
      preprocessing improves results.
    question: Can Aspose OCR read handwritten text?
  - answer: Use Aspose.PDF to create a new PDF and write the string returned by `OcrResult.getText()`.
    question: How do I convert the extracted text to a PDF?
  - answer: The engine handles images up to **200 MB**; larger files should be split
      or down‑scaled first.
    question: Is there a limit on image size?
  - answer: Yes, Aspose OCR for Java is platform‑independent and runs in Docker containers
      without native dependencies.
    question: Does the library work on Linux containers?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Πώς να χρησιμοποιήσετε OCR σε Java – πλήρες παράδειγμα Aspose OCR
url: /el/java/ocr-basics/get-ocr-text-in-java-complete-aspose-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να χρησιμοποιήσετε OCR σε Java – πλήρες παράδειγμα Aspose OCR

Αν χρειάζεστε **να λάβετε κείμενο OCR** από ένα σαρωμένο έγγραφο και αναρωτιέστε **πώς να χρησιμοποιήσετε OCR** σε ένα έργο Java, βρίσκεστε στο σωστό μέρος. Είτε αυτοματοποιείτε την επεξεργασία τιμολογίων, εξάγετε δεδομένα από πολύγλωσσες αποδείξεις, είτε μετατρέπετε χειρόγραφες φόρμες σε αναζητήσιμο κείμενο, το πρώτο βήμα είναι η μετατροπή μιας εικόνας σε επεξεργάσιμους χαρακτήρες. Αυτό το tutorial περνάει από ένα **java OCR example** χτισμένο με Aspose OCR for Java, δείχνοντας πώς να **φορτώσετε εικόνα OCR**, να ρυθμίσετε τις γλωσσικές ρυθμίσεις και να **εξάγετε κείμενο από σαρωμένη εικόνα** με λίγες μόνο γραμμές κώδικα.

![Flowchart showing how to get OCR text from an image using Aspose OCR Java](https://example.com/ocr-flowchart.png "Get OCR text flow diagram")

## Γρήγορες απαντήσεις
- **Ποια βιβλιοθήκη λειτουργεί καλύτερα για OCR σε Java;** Η Aspose OCR for Java παρέχει υψηλή ακρίβεια και πολύγλωσση υποστήριξη έτοιμη προς χρήση.  
- **Πόσες γραμμές κώδικα χρειάζονται;** Περίπου 10 γραμμές για να φορτώσετε μια εικόνα, να τρέξετε τη μηχανή και να εκτυπώσετε το αποτέλεσμα.  
- **Χρειάζεται άδεια;** Μια δωρεάν δοκιμή λειτουργεί για αξιολόγηση· μια πλήρης **aspose ocr license** αφαιρεί τους περιορισμούς αξιολόγησης.  
- **Μπορεί να διαχειριστεί πολλαπλές γλώσσες;** Ναι – ορίστε τον κωδικό γλώσσας ή ενεργοποιήστε την αυτόματη ανίχνευση για πάνω από 60 γραφές.  
- **Ποια έκδοση της Java απαιτείται;** Java 8 ή νεότερη.

## Τι είναι η χρήση OCR;
**Η χρήση OCR** σημαίνει την αξιοποίηση μιας μηχανής οπτικής αναγνώρισης χαρακτήρων για την ανάγνωση τυπωμένων ή χειρόγραφων χαρακτήρων από bitmap εικόνες και την επιστροφή τους ως απλό κείμενο. Η διαδικασία συνήθως περιλαμβάνει τη φόρτωση της εικόνας, την επιλογή του κατάλληλου μοντέλου γλώσσας, την εκτέλεση της μηχανής αναγνώρισης και, στη συνέχεια, την ανάκτηση του εξαγόμενου κειμένου για περαιτέρω επεξεργασία ή αποθήκευση.

## Γιατί να χρησιμοποιήσετε Aspose OCR για Java;
Η Aspose OCR υποστηρίζει **50+ μορφές εισόδου** (συμπεριλαμβανομένων PNG, JPEG, TIFF, BMP) και μπορεί να επεξεργαστεί αρχεία έως **200 MB** χωρίς να φορτώνει ολόκληρη την εικόνα στη μνήμη, παρέχοντας έως **95 % ακρίβεια** σε καθαρές εκτυπώσεις και **80 %+** σε χαμηλής ποιότητας σαρώσεις όταν εφαρμόζεται προεπεξεργασία.

## Προαπαιτούμενα
- Java 8 ή νεότερη εγκατεστημένη.  
- IDE συμβατό με Maven (IntelliJ IDEA, Eclipse ή VS Code).  
- Έγκυρη **aspose ocr license** (το κλειδί δοκιμής λειτουργεί για ανάπτυξη).  

## Πώς να προσθέσετε την εξάρτηση Aspose OCR (φόρτωση εικόνας OCR)
Η προσθήκη της βιβλιοθήκης Aspose OCR στο έργο σας σας δίνει πρόσβαση στη μηχανή OCR και σε όλα τα σχετικά εργαλεία. Συμπεριλάβετε την εξάρτηση Maven (ή το ισοδύναμο Gradle) στο αρχείο build, στη συνέχεια ανανεώστε το έργο ώστε τα JAR να ληφθούν από το αποθετήριο Maven. Αυτό το βήμα είναι απαραίτητο πριν μπορέσετε να δημιουργήσετε οποιεσδήποτε κλάσεις OCR.

```xml
<!-- Aspose OCR for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest version available -->
</dependency>
```

> **Συμβουλή**: Αν προτιμάτε Gradle, χρησιμοποιήστε `implementation 'com.aspose:aspose-ocr:23.9'`. Η προσθήκη της εξάρτησης είναι ο πιο οικονομικός τρόπος για **φόρτωση εικόνας OCR** στο έργο σας.

## Πώς να δημιουργήσετε τη μηχανή OCR και να φορτώσετε την εικόνα σας
Αρχικά, δημιουργήστε μια παρουσία του `OcrEngine`, που είναι το κύριο συστατικό που εκτελεί την αναγνώριση. Στη συνέχεια, κατευθύνετε τη μηχανή στο αρχείο εικόνας που θέλετε να επεξεργαστείτε και, προαιρετικά, ορίστε τον κωδικό γλώσσας. Αυτό προετοιμάζει τη μηχανή για το επόμενο βήμα αναγνώρισης.

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class LanguageExample {

    public static void main(String[] args) throws Exception {
        // 2️⃣ Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // 2️⃣ Load the image you want to process – this is the "load image OCR" step
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multilingual.png"));

        // 2️⃣ Choose the language (ISO‑639‑2). Change "tam" to any supported code.
        engine.getEngineOptions().setLanguage("tam");
        // If you prefer automatic detection, uncomment the next line:
        // engine.getEngineOptions().setAutoDetectLanguage(true);
```

### Γιατί να ορίσετε τη γλώσσα ρητά;
Η καθορισμένη γλώσσα μειώνει τα ψευδώς θετικά και επιταχύνει την αναγνώριση. Για πολύγλωσσα PDFs μπορείτε να κάνετε βρόχο πάνω σε έναν πίνακα κωδικών γλώσσας ή να ενεργοποιήσετε την αυτόματη ανίχνευση για ευκολία.

## Πώς να εκτελέσετε τη διαδικασία OCR και να λάβετε κείμενο OCR
Κληθείτε τη μέθοδο `recognize()` στην ρυθμισμένη `OcrEngine` για να ξεκινήσετε την ανάλυση. Η μέθοδος επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει το εξαγόμενο κείμενο απλού κειμένου και προαιρετικά μεταδεδομένα όπως βαθμοί εμπιστοσύνης και περιοχές περιγράμματος.

```java
        // 3️⃣ Perform OCR – this is where we finally **get OCR text**
        OcrResult result = engine.recognize();

        // 3️⃣ Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

Όταν εκτελέσετε το παράδειγμα, η κονσόλα θα εμφανίσει τους αναγνωρισμένους χαρακτήρες:

```
=== Extracted Text ===
தமிழ் உரை இங்கு வருகிறது...
```

Αν ενεργοποιήσετε `setAutoDetectLanguage(true)`, η μηχανή θα μαντέψει αυτόματα τη γλώσσα, κάτι χρήσιμο για άγνωστα έγγραφα.

## Πώς να αντιμετωπίσετε κοινές περιπτώσεις άκρων (εξαγωγή κειμένου από παραλλαγές εικόνας)
Οι πραγματικές σαρώσεις συχνά υποφέρουν από χαμηλή ανάλυση, θόρυβο ή την ανάγκη εξαγωγής μόνο ενός τμήματος της εικόνας. Η αντιμετώπιση αυτών των προβλημάτων βελτιώνει την ακρίβεια και την απόδοση. Παρακάτω είναι κοινές προσαρμογές που μπορείτε να εφαρμόσετε πριν ή κατά τη διάρκεια του OCR για να αντιμετωπίσετε τέτοιες παραλλαγές.

### Αντιμετώπιση εικόνων χαμηλής ανάλυσης
Η ακρίβεια του OCR πέφτει απότομα κάτω από 300 dpi. Αν η πηγή σας είναι χαμηλής ανάλυσης, σκεφτείτε να την αυξήσετε πρώτα:

```java
engine.getEngineOptions().setResolution(300); // forces 300 DPI
```

### Αφαίρεση θορύβου φόντου
Σαρωμένες φόρμες συχνά περιέχουν στίγματα που μπερδεύουν τη μηχανή. Μπορείτε να ενεργοποιήσετε την προεπεξεργασία για καθαρισμό της εικόνας:

```java
engine.getEngineOptions().setPreprocessMode(EngineOptions.PreprocessMode.Auto);
```

### Εξαγωγή κειμένου από συγκεκριμένες περιοχές
Αν χρειάζεστε κείμενο μόνο από ένα συγκεκριμένο ορθογώνιο (π.χ. ένα κελί πίνακα), ορίστε ένα `Rectangle` πριν καλέσετε `recognize()`:

```java
engine.setRegion(new Rectangle(50, 100, 400, 200));
```

Αυτές οι προσαρμογές κάνουν το **java OCR example** σας ανθεκτικό για παραγωγικά φορτία.

## Πώς να επαληθεύσετε το αποτέλεσμα (τι πρέπει να περιμένετε;)
Μια επιτυχημένη εκτέλεση εκτυπώνει την έκδοση απλού κειμένου της εικόνας. Για πολύγλωσσες εικόνες μπορεί να δείτε μεικτές γραφές:

```
Hello World
こんにちは世界
مرحبا بالعالم
```

Αν το αποτέλεσμα είναι κενό ή ακατάληπτο, ελέγξτε:

1. Το μονοπάτι αρχείου στο `setImage` (είναι σωστό;).  
2. Ο κωδικός γλώσσας ταιριάζει με τη γραφή στην εικόνα.  
3. Η ποιότητα της εικόνας (αντίθεση, DPI) είναι επαρκής.

## Πλήρες λειτουργικό παράδειγμα (έτοιμο για αντιγραφή‑επικόλληση)
Παρακάτω βρίσκεται ολόκληρο το αρχείο, έτοιμο για μεταγλώττιση και εκτέλεση. Αντικαταστήστε το `YOUR_DIRECTORY/multilingual.png` με το πραγματικό μονοπάτι της δοκιμαστικής σας εικόνας.

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class LanguageExample {
    public static void main(String[] args) throws Exception {
        // Initialize OCR engine
        OcrEngine engine = new OcrEngine();

        // Load the image – this is the core "load image OCR" step
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multilingual.png"));

        // Set language (ISO‑639‑2). For Tamil use "tam". Change as needed.
        engine.getEngineOptions().setLanguage("tam");
        // Uncomment for auto‑detect:
        // engine.getEngineOptions().setAutoDetectLanguage(true);

        // Optional: improve accuracy on low‑res images
        // engine.getEngineOptions().setResolution(300);
        // engine.getEngineOptions().setPreprocessMode(EngineOptions.PreprocessMode.Auto);

        // Perform OCR and retrieve text
        OcrResult result = engine.recognize();

        // Print the extracted text – this is how we **get OCR text**
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

Μεταγλώττιση και εκτέλεση:

```bash
mvn compile exec:java -Dexec.mainClass="com.example.ocr.LanguageExample"
```

Τώρα θα πρέπει να δείτε το εξαγόμενο περιεχόμενο στην κονσόλα σας.

## Συχνές ερωτήσεις

**Ε: Χρειάζομαι πληρωμένη άδεια για παραγωγική χρήση;**  
Α: Ναι, μια πλήρης **aspose ocr license** αφαιρεί τους περιορισμούς αξιολόγησης και ενεργοποιεί όλες τις premium λειτουργίες.

**Ε: Μπορεί η Aspose OCR να διαβάσει χειρόγραφο κείμενο;**  
Α: Υποστηρίζει τυπωμένο και κάποιο κυρτό χειρόγραφο, αλλά η ακρίβεια διαφέρει· η προεπεξεργασία βελτιώνει τα αποτελέσματα.

**Ε: Πώς μετατρέπω το εξαγόμενο κείμενο σε PDF;**  
Α: Χρησιμοποιήστε την Aspose.PDF για να δημιουργήσετε νέο PDF και να γράψετε το string που επιστρέφει το `OcrResult.getText()`.

**Ε: Υπάρχει όριο στο μέγεθος της εικόνας;**  
Α: Η μηχανή διαχειρίζεται εικόνες έως **200 MB**· μεγαλύτερα αρχεία πρέπει να χωριστούν ή να μειωθεί η κλίμακά τους πρώτα.

**Ε: Λειτουργεί η βιβλιοθήκη σε Linux containers;**  
Α: Ναι, η Aspose OCR for Java είναι ανεξάρτητη από πλατφόρμα και τρέχει σε Docker containers χωρίς εγγενείς εξαρτήσεις.

## Συμπέρασμα

Δείξαμε **πώς να χρησιμοποιήσετε OCR** σε Java με Aspose OCR, καλύπτοντας τη ρύθμιση εξαρτήσεων, τη διαμόρφωση της μηχανής, τη διαχείριση γλώσσας και κοινές τεχνικές προεπεξεργασίας. Ενσωματώνοντας αυτό το **java OCR example** στη ροή εργασίας σας, μπορείτε αξιόπιστα να μετατρέπετε σαρωμένα έγγραφα σε αναζητήσιμο, επεξεργάσιμο κείμενο, να τροφοδοτείτε τα αποτελέσματα σε υπηρεσίες μετάφρασης ή να τα αποθηκεύετε για μεταγενέστερη ανάλυση.

---

**Τελευταία ενημέρωση:** 2026-11-04  
**Δοκιμάστηκε με:** Aspose OCR for Java 23.9  
**Συγγραφέας:** Aspose

## Σχετικά Μαθήματα

- [Convert Image To Text Java Complete Aspose Ocr Example](/ocr/java/ocr-basics/convert-image-to-text-java-complete-aspose-ocr-example/)
- [Load Image For Ocr With Aspose Ocr Java Complete Guide](/ocr/java/ocr-operations/load-image-for-ocr-with-aspose-ocr-java-complete-guide/)
- [How to extract text from image from URL using Aspose.OCR for Java](/ocr/java/advanced-ocr-techniques/perform-ocr-image-from-url/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}