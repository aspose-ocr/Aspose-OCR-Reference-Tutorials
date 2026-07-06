---
category: general
date: 2026-06-25
description: Παράδειγμα Aspose OCR Java που δείχνει πώς να εξάγετε κείμενο από αρχεία
  TIFF, να διαμορφώσετε τις ρυθμίσεις OCR και να ενεργοποιήσετε την παράλληλη επεξεργασία
  OCR για ταχύτερα αποτελέσματα.
draft: false
keywords:
- aspose ocr java example
- how to extract text
- extract text from tiff
- how to configure ocr
- parallel ocr processing
language: el
og_description: Παράδειγμα Aspose OCR Java που δείχνει πώς να εξάγετε κείμενο από
  εικόνες TIFF, να διαμορφώσετε το OCR και να εκτελέσετε παράλληλη επεξεργασία OCR
  για βέλτιστη απόδοση.
og_title: Παράδειγμα Aspose OCR Java – Γρήγορη Εξαγωγή Κειμένου από TIFF
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Aspose OCR Java example showing how to extract text from TIFF files,
    configure OCR settings, and enable parallel OCR processing for faster results.
  headline: Aspose OCR Java Example – Extract Text from TIFF with Parallel Processing
  type: TechArticle
- description: Aspose OCR Java example showing how to extract text from TIFF files,
    configure OCR settings, and enable parallel OCR processing for faster results.
  name: Aspose OCR Java Example – Extract Text from TIFF with Parallel Processing
  steps:
  - name: '**Add Aspose OCR to your project**'
    text: '**Add Aspose OCR to your project**'
  - name: '**Compile and execute**'
    text: '**Compile and execute**'
  - name: '**Observe the console** – you should see the OCR output sandwiched between
      the `=== OCR Output Start ===` markers.'
    text: '**Observe the console** – you should see the OCR output sandwiched between
      the `=== OCR Output Start ===` markers.'
  type: HowTo
tags:
- Aspose OCR
- Java
- Text Extraction
title: Παράδειγμα Aspose OCR Java – Εξαγωγή κειμένου από TIFF με παράλληλη επεξεργασία
url: /el/java/advanced-ocr-techniques/aspose-ocr-java-example-extract-text-from-tiff-with-parallel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Παράδειγμα Aspose OCR Java – Εξαγωγή Κειμένου από TIFF με Παράλληλη Επεξεργασία

Έχετε αναρωτηθεί ποτέ **πώς να εξάγετε κείμενο** από τεράστια σαρωμένα έγγραφα χωρίς η εφαρμογή σας να «παγώνει»; Δεν είστε μόνοι. Σε αυτό το **παράδειγμα Aspose OCR Java** θα δούμε πώς να ρυθμίσουμε τη μηχανή OCR, να ενεργοποιήσουμε την παράλληλη επεξεργασία και να πάρουμε καθαρό Unicode κείμενο από ένα αρχείο TIFF πολλαπλών megabytes — όλα σε λίγες γραμμές κώδικα.

Σκεφτείτε το σαν να δίνετε στην Java εφαρμογή σας έναν τροφοδοτικό‑σκανέρ που μπορεί να «μαζεύει» σελίδες ενώ εσείς πίνετε καφέ. Στο τέλος αυτού του οδηγού θα έχετε ένα εκτελέσιμο πρόγραμμα, θα καταλάβετε γιατί κάθε ρύθμιση είναι σημαντική και θα ξέρετε πώς να το προσαρμόσετε στις δικές σας ανάγκες.

---

## Τι Χρειάζεστε Πριν Ξεκινήσετε

Πριν βουτήξουμε στον κώδικα, βεβαιωθείτε ότι έχετε:

- **Java 17** (ή οποιοδήποτε πρόσφατο JDK) εγκατεστημένο και προστιθέμενο στο `PATH`.
- Άδεια **Aspose.OCR for Java** ή ένα δωρεάν κλειδί αξιολόγησης. Μπορείτε να το κατεβάσετε από το portal της Aspose.
- Ένα **μεγάλο αρχείο TIFF** (`large_scan.tif`) που θέλετε να δοκιμάσετε — κατά προτίμηση αρκετά megabytes για να δείτε τη δύναμη της παράλληλης επεξεργασίας.
- Ένα εργαλείο κατασκευής όπως **Maven** ή **Gradle** για να κατεβάσετε τη βιβλιοθήκη Aspose OCR.

Αυτό είναι όλο. Δεν χρειάζονται βαριές μηχανές OCR ή εγγενή DLLs. Έτοιμοι; Ας μπει χέρι.

---

## Παράδειγμα Aspose OCR Java: Πλήρης Διάσχιση Κώδικα

Παρακάτω βρίσκεται το πλήρες, αυτόνομο πρόγραμμα Java. Αντιγράψτε‑και‑επικολλήστε το σε ένα αρχείο με όνομα `ParallelOcrDemo.java`, προσαρμόστε τη διαδρομή της εικόνας και είστε έτοιμοι.

```java
// ParallelOcrDemo.java
// Demonstrates an Aspose OCR Java example with parallel processing.

import com.aspose.ocr.*;
import com.aspose.ocr.config.*;
import com.aspose.ocr.results.*;

public class ParallelOcrDemo {
    public static void main(String[] args) {
        // -------------------------------------------------------------
        // Step 1: Create OCR configuration and enable parallel processing
        // -------------------------------------------------------------
        OcrConfig config = new OcrConfig()
                // ParallelSettings lets us run up to 8 threads simultaneously.
                .setParallelSettings(new ParallelSettings()
                        .setMaxThreads(8)); // Adjust based on CPU cores.

        // -------------------------------------------------------------
        // Step 2: Initialise the Aspose OCR engine with the configuration
        // -------------------------------------------------------------
        AsposeOCR ocrEngine = new AsposeOCR(config);

        // -------------------------------------------------------------
        // Step 3: Recognise text from a large image (extract text from tiff)
        // -------------------------------------------------------------
        // Replace the path with your actual TIFF file location.
        ImageRecognitionResult result = ocrEngine.recognizeImage("YOUR_DIRECTORY/large_scan.tif");

        // -------------------------------------------------------------
        // Step 4: Output the recognised text (how to extract text)
        // -------------------------------------------------------------
        System.out.println("=== OCR Output Start ===");
        System.out.println(result.getText());
        System.out.println("=== OCR Output End ===");
    }
}
```

> **Αναμενόμενη έξοδος** (συνοπτικά):  
> ```
> === OCR Output Start ===
> Lorem ipsum dolor sit amet, consectetur adipiscing elit...
> === OCR Output End ===
> ```

> **Εικονογράφηση**  
> ![Aspose OCR Java example processing image](https://example.com/images/aspose-ocr-java-example.png)

> *Alt text:* Παράδειγμα Aspose OCR Java που δείχνει την παράλληλη επεξεργασία μιας εικόνας TIFF.

---

## Πώς να Ρυθμίσετε το OCR για Παράλληλη Επεξεργασία OCR

Η γραμμή `new ParallelSettings().setMaxThreads(8)` είναι η καρδιά της **παράλληλης επεξεργασίας OCR**. Γιατί είναι σημαντική;

- **Χρήση CPU:** Σύγχρονοι διακομιστές έχουν συχνά CPU με 8 πυρήνες. Δημιουργώντας έως και οκτώ νήματα, η μηχανή μπορεί να αποκωδικοποιεί πολλαπλά τμήματα εικόνας ταυτόχρονα, μειώνοντας δραστικά το συνολικό χρόνο εκτέλεσης.
- **Σκέψεις μνήμης:** Κάθε νήμα κρατά ένα αντίγραφο εσωτερικών buffers. Αν εργάζεστε σε μηχάνημα με περιορισμένη μνήμη, μειώστε τον αριθμό νημάτων (`setMaxThreads(4)`) για να αποφύγετε `OutOfMemoryError`.
- **Ασφάλεια νήματος:** Το Aspose OCR είναι thread‑safe από προεπιλογή, οπότε δεν χρειάζεστε επιπλέον κώδικα συγχρονισμού.

Αν χρειαστεί ποτέ να επεξεργαστείτε μια δέσμη αρχείων, απλώς τυλίξτε την κλήση `recognizeImage` μέσα σε ένα `ExecutorService` της Java και επαναχρησιμοποιήστε την ίδια παρουσία `AsposeOCR` — χάρη στην εσωτερική πισίνα νημάτων που διαμορφώσατε.

---

## Πώς να Εξάγετε Κείμενο από Αρχεία TIFF

Το TIFF (Tagged Image File Format) είναι δημοφιλές για σαρωμένα έγγραφα επειδή μπορεί να αποθηκεύει πολλαπλές σελίδες και δεδομένα χωρίς απώλειες. Ωστόσο, δεν χειρίζονται όλες οι βιβλιοθήκες OCR τα πολυ‑σελίδα TIFF άνετα.

Το Aspose OCR εντοπίζει αυτόματα τον τύπο της εικόνας και, όταν του δοθεί ένα πολυ‑σελίδα TIFF, επεξεργάζεται κάθε σελίδα διαδοχικά *μέσα* στην παράλληλη μηχανή. Αυτό σημαίνει ότι λαμβάνετε το όφελος του multi‑threading χωρίς επιπλέον κώδικα βρόχου.

Αν χρειάζεστε μόνο την πρώτη σελίδα, περάστε ένα αντικείμενο `PageOptions`:

```java
ImageRecognitionResult result = ocrEngine.recognizeImage(
        "YOUR_DIRECTORY/large_scan.tif",
        new ImageRecognitionOptions().setPageNumber(1));
```

Αλλά για την πλήρη **εξαγωγή κειμένου από tiff** εμπειρία, αφήστε τις επιλογές εκτός όπως φαίνεται στο παράδειγμα.

---

## Πώς να Εξάγετε Κείμενο – Επαλήθευση του Αποτελέσματος

Αφού η μηχανή OCR ολοκληρώσει, το `result.getText()` επιστρέφει ένα απλό `String`. Μπορείτε να:

- Το γράψετε σε αρχείο `.txt` με `Files.writeString(Path.of("output.txt"), result.getText());`.
- Το περάσετε σε μια downstream NLP pipeline.
- Το αναζητήσετε με Lucene για γρήγορη ανάκτηση εγγράφων.

Θυμηθείτε να αφαιρέσετε τα κενά (trim) αν σκοπεύετε να συνδυάσετε αποτελέσματα από πολλές σελίδες:

```java
String cleaned = result.getText().trim();
```

---

## Συνηθισμένα Πίνακες και Επαγγελματικές Συμβουλές

| Πιθανό Πρόβλημα | Γιατί Συμβαίνει | Λύση |
|------------------|------------------|------|
| **Καταρρεύσεις λόγω έλλειψης μνήμης** | Πάρα πολλά νήματα σε VM με χαμηλή RAM. | Μειώστε το `setMaxThreads` ή αυξήστε το heap (`-Xmx2g`). |
| **Κενή έξοδος** | Λάθος διαδρομή εικόνας ή αρχείο μη προσβάσιμο. | Επαληθεύστε την απόλυτη διαδρομή και τα δικαιώματα αρχείου. |
| **Ασυνήθιστα σύμβολα** | Το TIFF προέρχεται από κωδικοποίηση που δεν υποστηρίζεται. | Προεπεξεργαστείτε με ImageMagick ώστε να είναι 8‑bit grayscale. |
| **Αργή απόδοση σε μονοπύρηνους υπολογιστές** | Η παράλληλη εκτέλεση προσθέτει overhead. | Ορίστε `setMaxThreads(1)` για μονοπύρηνα περιβάλλοντα. |

Γρήγορη συμβουλή: πάντα καλέστε `ocrEngine.dispose()` (ή χρησιμοποιήστε try‑with‑resources αν το τυλίξετε) για να απελευθερώσετε εγγενείς πόρους όταν τελειώσετε. Είναι μια μικρή συνήθεια που αποτρέπει διαρροές μνήμης σε υπηρεσίες που τρέχουν πολύ ώρα.

---

## Εκτέλεση του Παραδείγματος

1. **Προσθέστε το Aspose OCR στο πρόγραμμά σας**  
   Maven:
   ```xml
   <dependency>
       <groupId>com.aspose</groupId>
       <artifactId>aspose-ocr</artifactId>
       <version>23.10</version>
   </dependency>
   ```
   Gradle:
   ```groovy
   implementation 'com.aspose:aspose-ocr:23.10'
   ```

2. **Συμπιέστε και εκτελέστε**  
   ```bash
   javac -cp ".:path/to/aspose-ocr.jar" ParallelOcrDemo.java
   java -cp ".:path/to/aspose-ocr.jar" ParallelOcrDemo
   ```

3. **Παρατηρήστε την κονσόλα** – θα πρέπει να δείτε το OCR αποτέλεσμα ενσωματωμένο μεταξύ των σημάνσεων `=== OCR Output Start ===`.

Αν η έξοδος φαίνεται παραμορφωμένη, ελέγξτε ξανά ότι το TIFF σας δεν είναι μια συμπιεσμένη παραλλαγή που δεν υποστηρίζεται από την τρέχουσα έκδοση της βιβλιοθήκης. Η ενημέρωση στην πιο πρόσφατη έκδοση του Aspose OCR συχνά διορθώνει τέτοια σενάρια.

---

## Επόμενα Βήματα – Επέκταση του Παραδείγματος Aspose OCR Java

Τώρα που έχετε κατακτήσει τα βασικά, σκεφτείτε τα παρακάτω πειράματα:

- **Επεξεργασία δέσμης:** Επανάληψη σε έναν φάκελο με TIFFs, αποθήκευση κάθε αποτελέσματος σε βάση δεδομένων.
- **Πακέτα γλωσσών:** Φορτώστε επιπλέον μοντέλα γλώσσας (`ocrEngine.addLanguage(Language.Spanish);`) για καλύτερη ακρίβεια σε μη‑αγγλικά έγγραφα.
- **Προεπεξεργασία εικόνας:** Χρησιμοποιήστε `java.awt` ή OpenCV για διόρθωση κλίσης, απομάκρυνση θορύβου ή βελτίωση αντίθεσης πριν περάσετε την εικόνα στη μηχανή OCR.
- **Ενσωμάτωση με Spring Boot:** Εκθέστε ένα REST endpoint που δέχεται ανεβασμένη εικόνα και επιστρέφει αμέσως το εξαγόμενο κείμενο.

Κάθε ένα από αυτά τα θέματα συνδέεται φυσικά με τις **ρυθμίσεις OCR** και τις **παράλληλες στρατηγικές OCR** που συζητήσαμε, προσφέροντάς σας μια ισχυρή, έτοιμη για παραγωγή γραμμή εργασίας.

---

## Συμπέρασμα

Σε αυτό το **παράδειγμα Aspose OCR Java** καλύψαμε όλα όσα χρειάζεστε για να **εξάγετε κείμενο** από ένα μεγάλο αρχείο TIFF, να ρυθμίσετε τη μηχανή OCR για βέλτιστη απόδοση και να αξιοποιήσετε την **παράλληλη επεξεργασία OCR** ώστε η εφαρμογή σας να παραμένει ευέλικτη. Ακολουθώντας τον κώδικα βήμα‑βήμα, ρυθμίζοντας τον αριθμό νημάτων και προσέχοντας τα κοινά προβλήματα, θα μπορείτε να ενσωματώσετε OCR υψηλής ταχύτητας σε οποιαδήποτε Java υπηρεσία σήμερα.

Δοκιμάστε το, προσαρμόστε τις ρυθμίσεις και αφήστε τη μηχανή OCR να κάνει το σκληρό κομμάτι ενώ εσείς εστιάζετε στην ανάπτυξη της επόμενης μεγάλης λειτουργίας νοημοσύνης εγγράφων. Καλή προγραμματιστική!

## Τι Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική

Οι παρακάτω εκπαιδευτικοί οδηγοί καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κυριαρχήσετε σε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση των δικών σας έργων.

- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to recognize tiff with Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [How to Use OCR - Advanced Techniques with Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}