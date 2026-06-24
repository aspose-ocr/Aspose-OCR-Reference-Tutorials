---
category: general
date: 2026-06-22
description: Δημιουργήστε αναζητήσιμο PDF σε Java με το Aspose OCR. Μάθετε πώς να
  μετατρέπετε σαρωμένα PDF, να διαχειρίζεστε OCR πολλαπλών γλωσσών και να βελτιώσετε
  την ακρίβεια.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- how to ocr document
- mixed language ocr
- aspose ocr java
language: el
og_description: Δημιουργήστε PDF με δυνατότητα αναζήτησης σε Java χρησιμοποιώντας
  το Aspose OCR. Αυτό το σεμινάριο δείχνει πώς να κάνετε OCR σε ένα έγγραφο, να διαχειριστείτε
  κείμενο με μεικτές γλώσσες και να εξάγετε ένα PDF με δυνατότητα αναζήτησης.
og_title: Δημιουργία Αναζητήσιμου PDF από Σαρωμένες Εικόνες – Οδηγός Java OCR
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create searchable PDF in Java with Aspose OCR. Learn how to convert
    scanned PDF, handle mixed language OCR and boost accuracy.
  headline: Create Searchable PDF from Scanned Images – Java OCR Guide
  type: TechArticle
- description: Create searchable PDF in Java with Aspose OCR. Learn how to convert
    scanned PDF, handle mixed language OCR and boost accuracy.
  name: Create Searchable PDF from Scanned Images – Java OCR Guide
  steps:
  - name: Expected Output
    text: 'When you open `processed.pdf` in Adobe Reader (or any PDF viewer), you
      should be able to:'
  - name: 1. What if my document contains more than two languages?
    text: '`config.setLanguage` accepts a var‑args list, so you can pass as many `OcrLanguage`
      constants as you need:'
  - name: 2. Can I run this on a headless server without a GPU?
    text: Absolutely. Set `config.setUseGpu(false)` or simply omit the call. The engine
      will fall back to multi‑core CPU processing, which is still fast thanks to the
      thread pool we configured.
  - name: 3. How do I handle huge PDFs (hundreds of pages)?
    text: Aspose OCR streams pages one‑by‑one, so memory usage stays modest. However,
      you might want to split the PDF into smaller chunks using Aspose PDF’s `split`
      method, process each chunk, then merge the results back together.
  - name: 4. Is there a way to keep the original PDF’s metadata (author, creation
      date)?
    text: 'Yes. After you obtain `searchablePdf`, you can copy metadata from the original
      PDF:'
  type: HowTo
tags:
- OCR
- Java
- PDF
title: Δημιουργία Αναζητήσιμου PDF από Σαρωμένες Εικόνες – Οδηγός Java OCR
url: /el/java/advanced-ocr-techniques/create-searchable-pdf-from-scanned-images-java-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Αναζητήσιμου PDF από Σαρωμένες Εικόνες – Οδηγός OCR για Java

Αναρωτηθήκατε ποτέ πώς να **δημιουργήσετε αναζητήσιμο PDF** από μια στοίβα σαρωμένων σελίδων χωρίς να ξοδέψετε μια περιουσία σε υπηρεσίες τρίτων; Δεν είστε μόνοι. Πολλοί προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν χρειάζεται να **μετατρέψουν σαρωμένα PDF** σε κάτι που οι χρήστες τους μπορούν πραγματικά να αναζητήσουν.  

Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα από ένα πλήρες, εκτελέσιμο παράδειγμα που χρησιμοποιεί **Aspose OCR for Java** για **πώς να OCR έγγραφα**‑επιπέδου, θα αντιμετωπίσουμε **OCR μεικτής γλώσσας**, και τελικά θα παραγάγουμε ένα γυαλιστερό αναζητήσιμο PDF. Στο τέλος θα έχετε ένα αυτόνομο πρόγραμμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Maven ή Gradle και να αρχίσετε να επεξεργάζεστε έγγραφα σήμερα.

## Prerequisites – What You’ll Need

Πριν βουτήξουμε στον κώδικα, βεβαιωθείτε ότι έχετε τα εξής:

- Java 17 (ή οποιοδήποτε πρόσφατο JDK) εγκατεστημένο και ρυθμισμένο στο PATH.  
- Ένα IDE ή επεξεργαστή με τον οποίο αισθάνεστε άνετα (IntelliJ IDEA, Eclipse, VS Code…).  
- Βιβλιοθήκη Aspose.OCR for Java – μπορείτε να κατεβάσετε το τελευταίο JAR από το [Aspose Maven repository](https://repo.aspose.com/repo/com/aspose/aspose-ocr/).  
- Ένα πολυ‑σελίδων σαρωμένο PDF που θέλετε να κάνετε αναζητήσιμο.  
- (Προαιρετικά) Μηχανή με GPU εάν σκοπεύετε να χρησιμοποιήσετε `setUseGpu(true)` για ταχύτερη επεξεργασία.

Αυτά τα στοιχεία έτοιμα σημαίνουν ότι μπορείτε να αντιγράψετε‑επικολλήσετε τον παρακάτω κώδικα και να πατήσετε **Run** χωρίς να ψάχνετε για ελλιπείς εξαρτήσεις.

## Step 1: Set Up the Project and Import Aspose OCR

Πρώτα, δημιουργήστε ένα νέο Maven module (ή Gradle project) και προσθέστε την εξάρτηση Aspose OCR:

```xml
<!-- pom.xml snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- replace with the latest version -->
</dependency>
```

Αν προτιμάτε Gradle, η ισοδύναμη γραμμή είναι:

```gradle
implementation 'com.aspose:aspose-ocr:23.10'
```

Μόλις συγχρονιστεί η κατασκευή, θα μπορείτε να εισάγετε τις κλάσεις που χρειαζόμαστε.

## Step 2: Initialize the OCR Engine

Η δημιουργία της μηχανής είναι απλή, αλλά αξίζει να καταλάβουμε γιατί το κάνουμε νωρίς. Το αντικείμενο `OcrEngine` κρατά ρυθμίσεις, νήματα και ρυθμίσεις GPU που επηρεάζουν κάθε επόμενη λειτουργία.

```java
import com.aspose.ocr.*;

public class AdvancedOcr {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine – this is the heart of the create searchable pdf process
        OcrEngine ocrEngine = new OcrEngine();
```

> **Pro tip:** Η δημιουργία της μηχανής μία φορά και η επαναχρησιμοποίησή της για πολλά αρχεία μειώνει το κόστος, ειδικά όταν επεξεργάζεστε μια παρτίδα PDF.

## Step 3: Load the Scanned PDF (or Image Stream)

Το Aspose OCR λειτουργεί με ροές εικόνας, οπότε τροφοδοτούμε το σαρωμένο PDF απευθείας. Η βιβλιοθήκη εσωτερικά rasterizes κάθε σελίδα, γι’ αυτό μπορείτε να ξεκινήσετε από PDF και να καταλήξετε σε αναζητήσιμο PDF σε ένα βήμα.

```java
        // Load the source PDF – replace the path with your actual file location
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multi_page_scanned.pdf"));
```

Αν έχετε μια συλλογή TIFF ή JPEG αντί αυτού, απλώς κατευθύνετε το `ImageStream.fromFile` στα αρχεία αυτά· το υπόλοιπο της αλυσίδας παραμένει το ίδιο.

## Step 4: Fine‑Tune OCR Settings for Mixed Language Support

Εδώ είναι που το **OCR μεικτής γλώσσας** δείχνει τη δύναμή του. Με τη μεταβίβαση πολλαπλών `OcrLanguage` enums λέτε στη μηχανή να ψάξει τόσο για Αγγλικά όσο και για Ρωσικά (ή οποιονδήποτε άλλο συνδυασμό) στην ίδια σελίδα.

```java
        // Grab the mutable config object
        OcrConfig config = ocrEngine.getConfig();

        // Enable English + Russian detection – you can add more languages as needed
        config.setLanguage(OcrLanguage.ENGLISH, OcrLanguage.RUSSIAN);

        // Speed vs. accuracy trade‑off: use all available cores
        config.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Turn on GPU acceleration if the runtime detects a compatible device
        config.setUseGpu(true);

        // Spell‑check improves accuracy for noisy scans
        config.setEnableSpellCorrection(true);

        // Tell Aspose we want a searchable PDF as the final output
        config.setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);
```

> **Why this matters:** Χωρίς να καθορίσετε γλώσσες, η μηχανή προεπιλέγει μόνο τα Αγγλικά, κάτι που μειώνει δραστικά τα ποσοστά αναγνώρισης για έγγραφα που περιέχουν κυριλλικά ή άλλα αλφάβητα.

## Step 5: Add Pre‑Processing Filters to Clean Up the Scan

Τα σαρωμένα PDF συχνά έχουν κλίση, στίγματα ή χαμηλή αντίθεση. Η προσθήκη ενός `DeskewFilter` και ενός `DenoiseFilter` βοηθά τη μηχανή OCR να βλέπει τους χαρακτήρες πιο καθαρά.

```java
        // Set up image preprocessing
        ImagePreprocessOptions preprocess = new ImagePreprocessOptions();
        preprocess.addFilter(new DeskewFilter());   // Straighten tilted pages
        preprocess.addFilter(new DenoiseFilter()); // Reduce background noise
        ocrEngine.setPreprocessOptions(preprocess);
```

Μπορείτε να αλυσίδωσετε επιπλέον φίλτρα — όπως `ContrastFilter` ή `BinarizationFilter` — εάν το υλικό σας είναι ιδιαίτερα βρώμικο.

## Step 6: Run the OCR and Generate the Searchable PDF

Τώρα αρχίζει η βαριά δουλειά. Η κλήση `recognizeToPdf()` εκτελεί την αλυσίδα OCR, εφαρμόζει τα βήματα προεπεξεργασίας και γράφει το αναγνωρισμένο κείμενο σε ένα αόρατο στρώμα κειμένου μέσα στο PDF.

```java
        // Perform OCR and retrieve a searchable PDF document object
        PdfDocument searchablePdf = ocrEngine.recognizeToPdf();
```

Το επιστρεφόμενο `PdfDocument` είναι ένα πλήρες αντικείμενο Aspose PDF, πράγμα που σημαίνει ότι μπορείτε να επεξεργαστείτε περαιτέρω μεταδεδομένα, να προσθέσετε σελιδοδείκτες ή να το συγχωνεύσετε με άλλα PDF πριν το αποθηκεύσετε.

## Step 7: Save the Result and Verify

Τέλος, αποθηκεύστε το αποτέλεσμα στο δίσκο. Το μήνυμα στην κονσόλα σας δίνει μια γρήγορη οπτική ένδειξη ότι όλα λειτούργησαν.

```java
        // Save the searchable PDF to the desired location
        searchablePdf.save("YOUR_DIRECTORY/processed.pdf");
        System.out.println("OCR completed – searchable PDF saved at YOUR_DIRECTORY/processed.pdf");
    }
}
```

### Expected Output

Όταν ανοίξετε το `processed.pdf` στο Adobe Reader (ή σε οποιοδήποτε πρόγραμμα προβολής PDF), θα πρέπει να μπορείτε:

1. **Επιλογή κειμένου** – κάντε κλικ και σύρετε πάνω σε οποιαδήποτε λέξη και αντιγράψτε την.  
2. **Αναζήτηση** – πατήστε `Ctrl+F` και πληκτρολογήστε μια φράση που εμφανίζεται κάπου στις αρχικές σαρώσεις.  
3. **Διατήρηση αρχικής διάταξης** – η οπτική εμφάνιση παραμένει ακριβώς όπως η σαρωμένη πηγή· προστέθηκε μόνο ένα αόρατο στρώμα κειμένου.

Αν δείτε ακατάστατους χαρακτήρες ή λείπουν σελίδες, ελέγξτε ξανά τις ρυθμίσεις γλώσσας και βεβαιωθείτε ότι το αρχικό PDF δεν είναι προστατευμένο με κωδικό.

## Common Questions & Edge Cases

### 1. What if my document contains more than two languages?

`config.setLanguage` δέχεται λίστα var‑args, οπότε μπορείτε να περάσετε όσες `OcrLanguage` σταθερές χρειάζεστε:

```java
config.setLanguage(OcrLanguage.ENGLISH, OcrLanguage.RUSSIAN, OcrLanguage.CHINESE_SIMPLIFIED);
```

Απλώς θυμηθείτε ότι κάθε επιπλέον γλώσσα αυξάνει ελαφρώς τον χρόνο επεξεργασίας.

### 2. Can I run this on a headless server without a GPU?

Απολύτως. Ορίστε `config.setUseGpu(false)` ή απλώς παραλείψτε την κλήση. Η μηχανή θα επιστρέψει στην επεξεργασία πολλαπλών πυρήνων CPU, η οποία είναι ακόμα γρήγορη χάρη στο thread pool που διαμορφώσαμε.

### 3. How do I handle huge PDFs (hundreds of pages)?

Το Aspose OCR μεταδίδει τις σελίδες μία‑μία, έτσι η χρήση μνήμης παραμένει μέτρια. Ωστόσο, ίσως θελήσετε να χωρίσετε το PDF σε μικρότερα τμήματα χρησιμοποιώντας τη μέθοδο `split` του Aspose PDF, να επεξεργαστείτε κάθε τμήμα και, στη συνέχεια, να συγχωνεύσετε τα αποτελέσματα.

### 4. Is there a way to keep the original PDF’s metadata (author, creation date)?

Ναι. Αφού λάβετε το `searchablePdf`, μπορείτε να αντιγράψετε τα μεταδεδομένα από το αρχικό PDF:

```java
PdfDocument original = new PdfDocument("YOUR_DIRECTORY/multi_page_scanned.pdf");
searchablePdf.getInfo().setAuthor(original.getInfo().getAuthor());
// repeat for other metadata fields
```

## Pro Tips for Production‑Ready OCR

- **Batch processing:** Τυλίξτε όλη τη ροή μέσα σε έναν βρόχο που διατρέχει έναν φάκελο αρχείων. Επαναχρησιμοποιήστε ένα μόνο αντικείμενο `OcrEngine` για να αποφύγετε επαναλαμβανόμενη αρχικοποίηση.  
- **Error handling:** Πιάστε `OcrException` για να καταγράψετε τα αρχεία που απέτυχαν, και συνεχίστε με το επόμενο έγγραφο.  
- **Performance monitoring:** Χρησιμοποιήστε `System.nanoTime()` πριν και μετά το `recognizeToPdf()` για να καταγράψετε τον χρόνο επεξεργασίας ανά αρχείο· αυτό σας βοηθά να αποφασίσετε αν χρειάζεται κλιμάκωση σε cloud worker pool.  
- **Security:** Εάν διαχειρίζεστε ευαίσθητα έγγραφα, σκεφτείτε την κρυπτογράφηση του εξαγόμενου PDF με `searchablePdf.encrypt(...)` πριν το αποθηκεύσετε.

## Conclusion

Καλύψαμε όλα όσα χρειάζεστε για να **δημιουργήσετε αναζητήσιμο PDF** από σαρωμένες πηγές χρησιμοποιώντας **Aspose OCR for Java**. Ο οδηγός έδειξε πώς να **μετατρέψετε σαρωμένο PDF**, να ρυθμίσετε **OCR μεικτής γλώσσας**, και να βελτιώσετε τα φίλτρα προεπεξεργασίας — όλα ενώ διατηρούμε τον κώδικα σύντομο και έτοιμο για παραγωγή.  

Από εδώ μπορείτε να εξερευνήσετε την προσθήκη μικρογραφιών που παράγονται από OCR, την ενσωμάτωση με σύστημα διαχείρισης εγγράφων, ή ακόμη και την τροφοδοσία του εξαγόμενου κειμένου σε ευρετήριο αναζήτησης όπως το Elasticsearch. Οι δυνατότητες είναι τόσο ευρείες όσο τα έγγραφα που χρειάζεται να ψηφιοποιήσετε.

Έχετε περισσότερες ερωτήσεις για το **πώς να OCR έγγραφα** σε Java, ή θέλετε μια πιο βαθιά ανάλυση της διαχείρισης PDF; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική δουλειά!

## What Should You Learn Next?

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [OCR Recognizing PDF Documents in Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}