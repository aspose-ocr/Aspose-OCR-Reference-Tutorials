---
category: general
date: 2026-08-28
description: Μάθετε πώς να εξάγετε κείμενο από εικόνες png σε Java χρησιμοποιώντας
  Aspose OCR. Αυτό το σεμινάριο καλύπτει την επεξεργασία batch OCR, την ανάγνωση εικόνων
  από φάκελο και το φιλτράρισμα αρχείων κατά επέκταση.
draft: false
keywords:
- extract text from png
- read images from folder
- filter files by extension
- how to batch ocr
- aspose ocr java tutorial
lastmod: 2026-08-28
og_description: Μάθετε πώς να εξάγετε κείμενο από εικόνες png σε Java χρησιμοποιώντας
  Aspose OCR. Αυτό το σεμινάριο καλύπτει την επεξεργασία batch OCR, την ανάγνωση εικόνων
  από φάκελο και το φιλτράρισμα αρχείων κατά επέκταση.
og_image_alt: 'Developer guide: extract text from png images in Java using Aspose
  OCR'
og_title: Πώς να εξάγετε κείμενο από png σε Java – οδηγός batch OCR
schemas:
- author: Aspose
  dateModified: '2026-08-28'
  description: Learn how to extract text from png images in Java using Aspose OCR.
    This tutorial covers batch OCR processing, reading images from a folder, and filtering
    files by extension.
  headline: How to extract text from png in Java – batch OCR guide
  type: TechArticle
- questions:
  - answer: Absolutely. Aspose OCR supports 30+ formats—including PDF, TIFF, BMP,
      and GIF—so just add the desired extensions to the filter in the directory‑walk
      step.
    question: Can I process PDFs or TIFFs as well?
  - answer: Change `RecognitionLanguage.ENGLISH` to `RecognitionLanguage.SPANISH`
      (or any supported language). The language packs are bundled with the library,
      so no extra download is required.
    question: What if I need a language other than English, such as Spanish?
  - answer: Yes. `Files.walk` traverses the entire tree recursively, so every nested
      PNG/J
    question: My folder contains sub‑folders—will they be scanned?
  - answer: Enable streaming mode by calling `ocrEngine.setUseStreaming(true)`. This
      tells the engine to read the image in chunks, dramatically reducing peak memory
      usage.
    question: How do I handle extremely large images that exceed 200 MB?
  - answer: Yes. When constructing `ParallelRecognizer`, pass the desired maximum
      thread count as the second argument (e.g., `new ParallelRecognizer(ocrEngine,
      4)`).
    question: Is there a way to limit the number of concurrent OCR threads?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: Πώς να εξάγετε κείμενο από png σε Java – οδηγός batch OCR
url: /el/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εξάγετε κείμενο από png σε Java – οδηγός batch OCR

Αν ποτέ χρειαστήκατε να **εξάγετε κείμενο από png** αρχεία αλλά δεν ήσασταν σίγουροι πώς να κλιμακώσετε τη λειτουργία πέρα από μερικές εικόνες, βρίσκεστε στο σωστό μέρος. Πολλοί προγραμματιστές ξεκινούν με μια κλήση OCR για μία εικόνα και γρήγορα αντιμετωπίζουν περιορισμούς απόδοσης όταν ο φάκελος μεγαλώνει σε δεκάδες ή εκατοντάδες αρχεία. Με το Aspose OCR for Java μπορείτε να δημιουργήσετε μια ισχυρή αλυσίδα batch OCR που διασχίζει έναν κατάλογο, φιλτράρει μόνο τους τύπους εικόνων που σας ενδιαφέρουν, εκτελεί την αναγνώριση παράλληλα και επιστρέφει τα αποτελέσματα με την ίδια σειρά όπως τα αρχικά αρχεία. Στο τέλος αυτού του οδηγού θα έχετε ένα έτοιμο κομμάτι κώδικα Java που διαχειρίζεται **batch OCR processing** αξιόπιστα και αποδοτικά.

![Παράδειγμα μετατροπής εικόνων σε κείμενο](https://example.com/convert-images-to-text.png "Στιγμιότυπο οθόνης της εξόδου της κονσόλας Java που εμφανίζει το μετατρεπόμενο κείμενο από αρχεία PNG")

## Γρήγορες απαντήσεις
- **Ποια βιβλιοθήκη διαχειρίζεται το OCR;** Aspose OCR for Java.
- **Μπορώ να επεξεργαστώ PNG και JPG μαζί;** Ναι – το παράδειγμα φιλτράρει και τις δύο επεκτάσεις.
- **Είναι η μηχανή OCR thread‑safe;** Μία κοινή παρουσία `AsposeOCR` είναι ασφαλής για ταυτόχρονη χρήση.
- **Χρειάζομαι άδεια για δοκιμές;** Ένα δωρεάν προσωρινό κλειδί είναι διαθέσιμο από την Aspose.
- **Θα σαρωθούν αυτόματα οι υπο‑φάκελοι;** `Files.walk` διασχίζει όλο το δέντρο αναδρομικά.

## Τι είναι η εξαγωγή κειμένου από png;

`extract text from png` αναφέρεται στη διαδικασία εφαρμογής αναγνώρισης οπτικών χαρακτήρων (OCR) σε αρχεία Portable Network Graphics ώστε οι ορατοί χαρακτήρες να γίνουν αναζητήσιμοι, επεξεργάσιμοι συμβολοσειρές. Η μηχανή του Aspose OCR διαβάζει τα δεδομένα pixel, εντοπίζει τα σχήματα των γλύφων και επιστρέφει κείμενο Unicode με μία κλήση μεθόδου.

## Γιατί να χρησιμοποιήσετε Aspose OCR για Java;

Το Aspose OCR υποστηρίζει **30+ γλώσσες**, επεξεργάζεται έως **500 εικόνες ανά λεπτό** σε έναν τυπικό διακομιστή 8‑πυρήνων και μπορεί να διαχειριστεί αρχεία έως **200 MB** χωρίς να φορτώνει ολόκληρη την εικόνα στη μνήμη. Αυτές οι ποσοτικοποιημένες δυνατότητες σημαίνουν ότι μπορείτε αξιόπιστα να εκτελείτε μεγάλης κλίμακας batch εργασίες σε κοινό υλικό χωρίς να φτάνετε τα όρια μνήμης.

## Προαπαιτούμενα
- Java 17 (ή οποιαδήποτε πρόσφατη έκδοση LTS).
- Maven ή Gradle για διαχείριση εξαρτήσεων.
- Ένας φάκελος που περιέχει εικόνες PNG/JPG που θέλετε να επεξεργαστείτε.
- Βασική εξοικείωση με τα Java streams και το πακέτο `java.nio.file`.
- (Προαιρετικό) Ένα προσωρινό κλειδί άδειας Aspose OCR για αξιολόγηση.

> **Pro tip:** Το δωρεάν προσωρινό κλειδί λήγει μετά από 30 ημέρες, αλλά σας παρέχει πλήρη πρόσβαση API για δοκιμές.

## Πώς η αλυσίδα batch OCR διατηρεί τη σειρά;

`Future<OcrResult>` αντιπροσωπεύει ένα εκκρεμές αποτέλεσμα OCR που μπορεί να ανακτηθεί όταν ολοκληρωθεί η επεξεργασία. Η αλυσίδα διατηρεί την αρχική σειρά των αρχείων αποθηκεύοντας τα αντικείμενα `Future<OcrResult>` σε μια λίστα που αντικατοπτρίζει τη σειρά της εισαγόμενης συλλογής `Path`. Όταν αργότερα επαναλάβετε τις futures και καλέσετε `get()`, κάθε κλήση μπλοκάρει μόνο για την αντίστοιχη εικόνα, έτσι η ακολουθία εξόδου ταιριάζει με την ακολουθία εισόδου χωρίς επιπλέον λογική ταξινόμησης.

## Τι είναι το Aspose OCR για Java;

`AsposeOCR` είναι η κεντρική κλάση της βιβλιοθήκης Aspose OCR που ενσωματώνει όλα τα πακέτα γλωσσών, τις ρυθμίσεις αναγνώρισης και τους εσωτερικούς φυσικούς πόρους. Σχεδιάστηκε ώστε να δημιουργείται μία φορά για τη διάρκεια ζωής της εφαρμογής και να μοιράζεται με ασφάλεια μεταξύ πολλών νημάτων. Επειδή φορτώνει τα δεδομένα γλώσσας μόνο μία φορά, η επαναχρησιμοποίηση της ίδιας παρουσίας μειώνει το κόστος εκκίνησης και βελτιώνει τη διαπερατότητα για batch λειτουργίες.

## Πώς να ρυθμίσετε το έργο και να προσθέσετε το Aspose OCR

Αρχικά, δημιουργήστε ένα έργο Maven (ή Gradle) και προσθέστε την εξάρτηση Aspose OCR στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.10</version>
</dependency>
```

> **Γιατί αυτό είναι σημαντικό:** Η δήλωση της εξάρτησης εκ των προτέρων εξασφαλίζει ότι ο μεταγλωττιστής μπορεί να δει τις κλάσεις `AsposeOCR`, `ParallelRecognizer` και σχετικές. Επίσης εγγυάται ότι η ίδια έκδοση χρησιμοποιείται σε όλα τα μηχανήματα, κάτι που είναι κρίσιμο για αναπαραγώγιμη **batch OCR processing**.

Ανανεώστε το IDE σας μετά την ολοκλήρωση της κατασκευής· θα πρέπει τώρα να δείτε τα πακέτα Aspose κάτω από **External Libraries**.

## Πώς να αρχικοποιήσετε τη μηχανή OCR – μοιραστείτε μία ενιαία παρουσία

`AsposeOCR` είναι η κύρια κλάση μηχανής OCR που παρέχεται από τη βιβλιοθήκη Aspose OCR. Χρειαζόμαστε μόνο **μία** παρουσία μηχανής OCR για όλη τη διαδικασία. Η κοινή χρήση της μεταξύ νημάτων εξοικονομεί μνήμη και επιταχύνει τη διαδικασία επειδή η μηχανή φορτώνει τα πακέτα γλώσσας μόνο μία φορά.

```java
AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");
```

`AsposeOCR` είναι thread‑safe, έτσι μπορείτε με ασφάλεια να το παραδώσετε σε ένα `ParallelRecognizer` που θα διαχειρίζεται μια ομάδα εργαζόμενων νημάτων.

> **Εξήγηση:** Το `ParallelRecognizer` τυλίγει τη μηχανή σε ένα thread‑pool. Όταν υποβάλετε πολλά αρχεία, το καθένα λαμβάνει το δικό του νήμα εργασίας, επιτρέποντας πραγματικό παράλληλο επεξεργασμό σε πολυπύρηνους επεξεργαστές.

## Πώς να διαβάσετε εικόνες από φάκελο – περιήγηση στο δέντρο καταλόγου

`Files.walk` είναι μια μέθοδος Java NIO που διασχίζει αναδρομικά ένα δέντρο αρχείων και επιστρέφει ένα stream από αντικείμενα `Path`. Τώρα χρειάζεται να **διαβάσουμε εικόνες από φάκελο** και να συλλέξουμε κάθε PNG ή JPG. Το API `Files.walk` το κάνει αυτό με μία γραμμή κώδικα, αλλά θα προσθέσουμε ένα φίλτρο για **extract text from png** μόνο όταν χρειάζεται.

```java
List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
    .filter(Files::isRegularFile)
    .filter(p -> {
        String lower = p.toString().toLowerCase();
        return lower.endsWith(".png") || lower.endsWith(".jpg");
    })
    .collect(Collectors.toList());
```

> **Γιατί φιλτράρουμε εδώ:** Η χρήση του `filter` μας επιτρέπει να **φιλτράρουμε αρχεία κατά επέκταση** νωρίς, μειώνοντας περιττές εισόδους/εξόδους αργότερα. Επίσης διατηρεί τον κώδικα ευανάγνωστο—χωρίς ανάγκη για σύνθετες εκφράσεις regex.

## Πώς να υποβάλετε εργασίες OCR ασύγχρονα

`recognizeAsync` υποβάλλει μια εικόνα στη μηχανή OCR για ασύγχρονη επεξεργασία και επιστρέφει ένα `Future<OcrResult>` που αντιπροσωπεύει το εκκρεμές αποτέλεσμα. Με τη λίστα αρχείων έτοιμη, σπρώχνουμε κάθε διαδρομή στο `ParallelRecognizer`. Η μέθοδος `recognizeAsync` επιστρέφει ένα `Future<OcrResult>` που αποθηκεύουμε για μετέπειτα ανάκτηση.

```java
ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine, Runtime.getRuntime().availableProcessors());
List<Future<OcrResult>> futures = new ArrayList<>();

for (Path imagePath : imagePaths) {
    futures.add(recognizer.recognizeAsync(imagePath));
}
```

> **Τι συμβαίνει στο παρασκήνιο;** Κάθε κλήση τοποθετεί μια εργασία στην εσωτερική υπηρεσία εκτελεστή του recognizer. Οι εργασίες εκτελούνται παράλληλα, έτσι ένας φάκελος με 100 εικόνες μπορεί να επεξεργαστεί σε ένα κλάσμα του χρόνου που θα απαιτούσε ένας βρόχος μονόνημα.

## Πώς να ανακτήσετε τα αποτελέσματα διατηρώντας τη σειρά των αρχείων

`Future<OcrResult>` κρατά το αποτέλεσμα μιας ασύγχρονης εργασίας OCR και παρέχει τη μέθοδο `get()` για την απόκτηση του αναγνωρισμένου κειμένου. Επειδή αποθηκεύσαμε τις futures στην ίδια σειρά με το `imagePaths`, μπορούμε απλώς να επαναλάβουμε τη λίστα και να καλέσουμε `get()`. Η κλήση μπλοκάρει μόνο μέχρι να ολοκληρωθεί η συγκεκριμένη εικόνα, διατηρώντας τη σειρά χωρίς επιπλέον λογιστική.

```java
for (int i = 0; i < futures.size(); i++) {
    try {
        OcrResult result = futures.get(i).get();
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println("Text: " + result.getText());
    } catch (Exception e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

**Δείγμα εξόδου κονσόλας** (truncated for brevity):

```
File: invoice1.png
Text: Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...
```

> **Διαχείριση ειδικών περιπτώσεων:** Εάν μια συγκεκριμένη εικόνα προκαλέσει εξαίρεση (κατεστραμμένο αρχείο, μη υποστηριζόμενη μορφή), τη συλλαμβάνουμε και συνεχίζουμε την επεξεργασία των υπολοίπων—μια απαραίτητη συνήθεια για αξιόπιστες **batch OCR processing** αλυσίδες.

## Πώς να καθαρίσετε πόρους – τερματισμός του recognizer

`ParallelRecognizer.shutdown()` σταματά την εσωτερική ομάδα νημάτων, εξασφαλίζοντας ότι όλες οι εργασίες OCR ολοκληρώνονται πριν η εφαρμογή κλείσει. Μην ξεχνάτε ποτέ να τερματίζετε την εσωτερική ομάδα νημάτων· διαφορετικά η JVM σας μπορεί να κολλήσει κατά το κλείσιμο.

```java
recognizer.shutdown();
```

Αυτό ήταν! Το πρόγραμμα τώρα διασχίζει οποιονδήποτε φάκελο, φιλτράρει αρχεία PNG/JPG, εκτελεί OCR παράλληλα και εκτυπώνει τα αποτελέσματα στην αρχική σειρά.

---

## Πλήρες λειτουργικό παράδειγμα (αντιγραφή‑και‑επικόλληση)

Παρακάτω βρίσκεται η πλήρης, έτοιμη‑για‑εκτέλεση κλάση Java. Αντικαταστήστε το `"YOUR_DIRECTORY"` με τη διαδρομή του φακέλου εικόνων σας και τρέξτε το από το IDE ή τη γραμμή εντολών.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.*;

public class BatchOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine (single shared instance)
        AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");

        // Create a parallel recognizer that uses a thread pool
        ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine,
                Runtime.getRuntime().availableProcessors());

        // Walk the directory and collect PNG/JPG files
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(Files::isRegularFile)
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        // Submit OCR jobs asynchronously
        List<Future<OcrResult>> futures = new ArrayList<>();
        for (Path imagePath : imagePaths) {
            futures.add(recognizer.recognizeAsync(imagePath));
        }

        // Retrieve results in the original order
        for (int i = 0; i < futures.size(); i++) {
            try {
                OcrResult result = futures.get(i).get();
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println("Text: " + result.getText());
            } catch (Exception e) {
                System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Clean up the recognizer's thread pool
        recognizer.shutdown();
    }
}
```

Τρέξτε την κλάση, παρακολουθήστε την κονσόλα να γεμίζει με εξαγόμενες συμβολοσειρές, και γιορτάστε το γεγονός ότι μόλις **μετατρέψατε εικόνες σε κείμενο** χωρίς να γράψετε κανένα βρόχο που μπλοκάρει στο I/O.

---

## Συχνές ερωτήσεις (FAQs)

**Q: Μπορώ να επεξεργαστώ επίσης PDF ή TIFF;**  
A: Απόλυτα. Το Aspose OCR υποστηρίζει 30+ μορφές—συμπεριλαμβανομένων PDF, TIFF, BMP και GIF—οπότε απλώς προσθέστε τις επιθυμητές επεκτάσεις στο φίλτρο στο βήμα περιήγησης καταλόγου.

**Q: Τι αν χρειαστώ μια γλώσσα διαφορετική από την Αγγλική, όπως Ισπανική;**  
A: Αλλάξτε το `RecognitionLanguage.ENGLISH` σε `RecognitionLanguage.SPANISH` (ή οποιαδήποτε υποστηριζόμενη γλώσσα). Τα πακέτα γλώσσας περιλαμβάνονται στη βιβλιοθήκη, έτσι δεν απαιτείται επιπλέον λήψη.

**Q: Ο φάκελός μου περιέχει υπο‑φακέλους—θα σαρωθούν;**  
A: Ναι. Το `Files.walk` διασχίζει όλο το δέντρο αναδρομικά, έτσι κάθε ένθετο PNG/J

**Q: Πώς να διαχειριστώ εξαιρετικά μεγάλες εικόνες που υπερβαίνουν τα 200 MB;**  
A: Ενεργοποιήστε τη λειτουργία streaming καλώντας `ocrEngine.setUseStreaming(true)`. Αυτό λέει στη μηχανή να διαβάζει την εικόνα σε τμήματα, μειώνοντας δραστικά τη μέγιστη χρήση μνήμης.

**Q: Υπάρχει τρόπος να περιορίσω τον αριθμό των ταυτόχρονων νημάτων OCR;**  
A: Ναι. Κατά την κατασκευή του `ParallelRecognizer`, περάστε τον επιθυμητό μέγιστο αριθμό νημάτων ως δεύτερο όρισμα (π.χ., `new ParallelRecognizer(ocrEngine, 4)`).

---

**Τελευταία ενημέρωση:** 2026-08-28  
**Δοκιμή με:** Aspose OCR for Java 24.10  
**Συγγραφέας:** Aspose  






```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

// ...

// Step 2: Create a single OCR engine instance and a parallel recognizer that uses it
AsposeOCR ocrEngine = new AsposeOCR();               // Loads language data internally
ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);
```

```java
import java.nio.file.*;
import java.util.*;
import java.util.stream.Collectors;

// ...

// Step 3: Find all PNG and JPG images in the target directory
Path imagesRoot = Paths.get("YOUR_DIRECTORY"); // <-- replace with your path
List<Path> imagePaths = Files.walk(imagesRoot)
        .filter(p -> {
            String name = p.toString().toLowerCase();
            return name.endsWith(".png") || name.endsWith(".jpg");
        })
        .collect(Collectors.toList());

if (imagePaths.isEmpty()) {
    System.out.println("No PNG or JPG files found in " + imagesRoot);
    return;
}
```

```java
import java.util.concurrent.*;

// ...

// Step 4: Submit each image for asynchronous recognition
List<Future<OcrResult>> recognitionFutures = new ArrayList<>();

for (Path image : imagePaths) {
    Future<OcrResult> future = parallelRecognizer.recognizeAsync(
            image.toString(),
            RecognitionLanguage.ENGLISH); // Change language if needed
    recognitionFutures.add(future);
}
```

```java
// Step 5: Retrieve and display the OCR results in the original order
for (int i = 0; i < recognitionFutures.size(); i++) {
    try {
        OcrResult result = recognitionFutures.get(i).get(); // blocks if not ready
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println(result.getText()); // The extracted text
        System.out.println("-----");
    } catch (InterruptedException | ExecutionException e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

```
File: invoice_001.png
Invoice #001
Date: 2024‑03‑15
Total: $1,250.00
-----
File: receipt_202403.jpg
Receipt
Item A - $45.00
Item B - $30.00
Grand Total: $75.00
-----
```

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.Collectors;

public class BatchParallelExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a single OCR engine instance and a parallel recognizer that uses it
        AsposeOCR ocrEngine = new AsposeOCR();
        ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);

        // Step 2: Find all PNG and JPG images in the target directory
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        if (imagePaths.isEmpty()) {
            System.out.println("No images found – nothing to convert.");
            parallelRecognizer.shutdown();
            return;
        }

        // Step 3: Submit each image for asynchronous recognition
        List<Future<OcrResult>> recognitionFutures = new ArrayList<>();
        for (Path image : imagePaths) {
            recognitionFutures.add(
                    parallelRecognizer.recognizeAsync(
                            image.toString(),
                            RecognitionLanguage.ENGLISH));
        }

        // Step 4: Retrieve and display the OCR results in the original order
        for (int i = 0; i < recognitionFutures.size(); i++) {
            try {
                OcrResult result = recognitionFutures.get(i).get(); // blocks until processed
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println(result.getText());
                System.out.println("-----");
            } catch (InterruptedException | ExecutionException e) {
                System.err.println("Error processing " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Step 5: Shut down the recognizer to clean up its internal thread pool
        parallelRecognizer.shutdown();
    }
}
```

## Σχετικά Μαθήματα

- [Μετατροπή Εικόνων σε Κείμενο σε Java Οδηγός Batch OCR Επεξεργασίας](/ocr/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/)
- [Ανάγνωση Κειμένου από Εικόνα σε Java Πλήρης Οδηγός Aspose OCR](/ocr/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Εξαγωγή Κειμένου από Εικόνες Χρησιμοποιώντας Aspose.OCR – Επιτρεπόμενοι Χαρακτήρες](/ocr/java/advanced-ocr-techniques/specify-allowed-characters/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}