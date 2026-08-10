---
category: general
date: 2026-02-14
description: 'Η μαζική OCR εικόνων έγινε εύκολη: μάθετε πώς να εξάγετε κείμενο από
  αρχεία PNG χρησιμοποιώντας το Aspose OCR με παράλληλη επεξεργασία σε Java.'
draft: false
keywords:
- batch image OCR
- extract text from png
- parallel OCR Java
- Aspose OCR async
- OCR batch processing
language: el
og_description: Εκπαιδευτικό σετ OCR εικόνων κατά παρτίδες που δείχνει πώς να εξάγετε
  κείμενο από αρχεία PNG χρησιμοποιώντας το ασύγχρονο API του Aspose OCR σε Java.
og_title: Ομαδική OCR εικόνων σε Java – Γρήγορη εξαγωγή κειμένου από PNG
tags:
- Java
- OCR
- Aspose
- Image Processing
title: Ομαδική OCR εικόνων σε Java – Γρήγορη εξαγωγή κειμένου από αρχεία PNG
url: /el/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ομαδική OCR Εικόνας σε Java – Γρήγορη Εξαγωγή Κειμένου από Αρχεία PNG

Έχετε ποτέ χρειαστεί να εκτελέσετε **batch image OCR** σε έναν φάκελο με σάρωση PNG αλλά να ανησυχείτε για την ταχύτητα; Δεν είστε μόνοι. Σε πολλά πραγματικά έργα—ψηφιοποίηση τιμολογίων, αρχειοθέτηση σαρωμένων βιβλίων ή επεξεργασία αποδείξεων—οι προγραμματιστές πρέπει να **εξάγουν κείμενο από PNG** εικόνες γρήγορα και αξιόπιστα.  

Τα καλά νέα; Με το ασύγχρονο API του Aspose OCR μπορείτε να δημιουργήσετε μια παράλληλη γραμμή OCR με λίγες μόνο γραμμές κώδικα Java. Σε αυτόν τον οδηγό θα περάσουμε από τη πλήρη, εκτελέσιμη λύση, θα εξηγήσουμε γιατί κάθε μέρος είναι σημαντικό και θα σας δείξουμε πώς να επαληθεύσετε τα αποτελέσματα. Στο τέλος θα έχετε ένα αυτόνομο πρόγραμμα που επεξεργάζεται ολόκληρη τη δέσμη αρχείων PNG παράλληλα, παρέχοντάς σας καθαρό κείμενο με ορθογραφικό έλεγχο.

## Τι Θα Μάθετε

- Πώς να καταγράψετε αρχεία PNG για ομαδική επεξεργασία  
- Διαμόρφωση του Aspose `OcrEngine` για αγγλική γλώσσα και ορθογραφική διόρθωση  
- Εκτέλεση OCR ασύγχρονα με `processAsync` και διαχείριση του αποτελέσματος `Future`  
- Ανάγνωση και εμφάνιση του αναγνωρισμένου κειμένου για κάθε εικόνα  
- Συμβουλές για κλιμάκωση, διαχείριση σφαλμάτων και βελτιστοποίηση απόδοσης  

### Προαπαιτούμενα

- Εγκατεστημένο Java 8 ή νεότερο (ο κώδικας χρησιμοποιεί το τυπικό πακέτο `java.util.concurrent`)  
- Άδεια Aspose OCR για Java ή δωρεάν δοκιμή (λήψη από την ιστοσελίδα Aspose)  
- Ένας φάκελος που περιέχει μερικά PNG στιγμιότυπα ή σαρωμένες σελίδες που θέλετε να δοκιμάσετε  

Τώρα, ας βουτήξουμε.

## Βήμα 1 – Συλλογή των Αρχείων PNG για Μια Δέσμη

Πριν η μηχανή OCR μπορέσει να κάνει οποιαδήποτε εργασία, πρέπει να γνωρίζει ποιες εικόνες θα επεξεργαστεί. Ο πιο απλός τρόπος είναι να δημιουργήσετε μια `List<String>` με απόλυτες ή σχετικές διαδρομές αρχείων.

```java
// Step 1: Prepare a list of PNG files you want to run OCR on
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/page1.png",
        "YOUR_DIRECTORY/page2.png",
        "YOUR_DIRECTORY/page3.png",
        "YOUR_DIRECTORY/page4.png");
```

**Γιατί είναι σημαντικό:**  
Η δημιουργία της λίστας εκ των προτέρων επιτρέπει στη μηχανή να προγραμματίσει κάθε αρχείο ανεξάρτητα, κάτι που αποτελεί τη βάση της πραγματικής ομαδικής επεξεργασίας. Αν αργότερα χρειαστεί να σαρώσετε έναν φάκελο δυναμικά, απλώς αντικαταστήστε το στατικό `Arrays.asList` με ένα ρεύμα `Files.walk`.

## Βήμα 2 – Αρχικοποίηση και Ρύθμιση της Μηχανής Aspose OCR

Το `OcrEngine` της Aspose είναι ιδιαίτερα παραμετροποιήσιμο. Εδώ ορίζουμε τη γλώσσα στα Αγγλικά και ενεργοποιούμε την ορθογραφική διόρθωση—δύο επιλογές που βελτιώνουν δραματικά την ποιότητα του εξαγόμενου κειμένου, ειδικά από θορυβώδεις σάρωση PNG.

```java
// Step 2: Create and configure the OCR engine
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getEngineOptions()
         .setLanguage(OcrLanguage.ENGLISH)          // English language model
         .setSpellCorrectionEnabled(true);          // Enable spell‑checking
```

**Γιατί αυτές οι ρυθμίσεις:**  
- **Επιλογή γλώσσας** ενημερώνει τη μηχανή ποιο σύνολο χαρακτήρων και λεξικό θα χρησιμοποιήσει, μειώνοντας τις λανθασμένες αναγνώσεις.  
- **Ορθογραφική διόρθωση** εντοπίζει κοινά λάθη OCR (π.χ., “1” vs “l”) χωρίς να χρειάζεται να επεξεργαστείτε το αποτέλεσμα.

> **Pro tip:** Αν οι εικόνες σας περιέχουν πολλαπλές γλώσσες, μπορείτε να περάσετε μια λίστα όπως `setLanguage(OcrLanguage.ENGLISH, OcrLanguage.FRENCH)`.

## Βήμα 3 – Εκκίνηση Ασύγχρονης Ομαδικής Επεξεργασίας

Η βαριά δουλειά γίνεται στο `processAsync`. Επιστρέφει ένα `Future<List<OcrResult>>`, επιτρέποντας στο κύριο νήμα σας να συνεχίσει άλλες εργασίες ενώ το OCR τρέχει στο παρασκήνιο.

```java
// Step 3: Start asynchronous processing of the image batch
Future<List<OcrResult>> ocrFuture = ocrEngine.processAsync(imageFiles);

// (Optional) Do something useful while OCR runs, e.g., log progress, load UI, etc.
System.out.println("OCR started – you can perform other tasks now...");
```

**Γιατί ασύγχρονα:**  
Η εκτέλεση OCR διαδοχικά μπορεί να είναι εξαιρετικά αργή—κάθε PNG μπορεί να πάρει ένα δευτερόλεπτο ή περισσότερο. Αναθέτοντας τη δουλειά σε μια ομάδα νημάτων, εκμεταλλεύεστε πολλαπλούς πυρήνες CPU και μειώνετε δραματικά το συνολικό χρόνο εκτέλεσης.

## Βήμα 4 – Ανάκτηση των Αποτελεσμάτων Όταν Είναι Έτοιμα

Όταν είστε έτοιμοι να χρησιμοποιήσετε το αποτέλεσμα, απλώς καλέστε `get()` στο `Future`. Αυτή η κλήση μπλοκάρει μόνο μέχρι να ολοκληρωθεί το OCR, μετά σας παραδίδει μια λίστα αντικειμένων `OcrResult` με την ίδια σειρά όπως η λίστα εισόδου.

```java
// Step 4: Wait for all results and retrieve them
List<OcrResult> ocrResults = ocrFuture.get(); // blocks until completion
```

**Διαχείριση λήξης χρόνου:**  
Αν θέλετε να αποφύγετε ένα απεριόριστο μπλοκάρισμα, χρησιμοποιήστε `ocrFuture.get(60, TimeUnit.SECONDS)` και πιάστε το `TimeoutException` για να υλοποιήσετε εναλλακτική λύση.

## Βήμα 5 – Εμφάνιση του Αναγνωρισμένου Κειμένου για Κάθε PNG

Τώρα που έχετε τα αποτελέσματα, επαναλάβετε τα και εκτυπώστε το εξαγόμενο κείμενο μαζί με το αρχικό όνομα αρχείου. Εδώ τελικά **εξάγετε κείμενο από PNG** αρχεία.

```java
// Step 5: Show the OCR output for each image
for (int i = 0; i < ocrResults.size(); i++) {
    System.out.println("File: " + imageFiles.get(i));
    System.out.println(ocrResults.get(i).getText());
    System.out.println("---");
}
```

**Παράδειγμα αναμενόμενης εξόδου**

```
File: YOUR_DIRECTORY/page1.png
Invoice #12345
Date: 2024‑03‑01
Total: $1,250.00
---
File: YOUR_DIRECTORY/page2.png
...
```

Αν η μηχανή OCR δεν μπορεί να αναγνωρίσει μια σελίδα, το αντίστοιχο `getText()` θα επιστρέψει μια κενή συμβολοσειρά—αξίζει πάντα να το ελέγχετε σε κώδικα παραγωγής.

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω βρίσκεται το πλήρες, έτοιμο προς εκτέλεση πρόγραμμα που συνδυάζει όλα τα μέρη. Αντιγράψτε‑και‑επικολλήστε το σε ένα αρχείο με όνομα `ParallelOcrDemo.java`, αντικαταστήστε το `YOUR_DIRECTORY` με τη διαδρομή του φακέλου PNG, και εκτελέστε `javac ParallelOcrDemo.java && java ParallelOcrDemo`.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Prepare a list of image files to be processed
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/page1.png",
                "YOUR_DIRECTORY/page2.png",
                "YOUR_DIRECTORY/page3.png",
                "YOUR_DIRECTORY/page4.png");

        // Step 2: Create and configure the OCR engine (set language and enable spell‑checking)
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getEngineOptions()
                 .setLanguage(OcrLanguage.ENGLISH)
                 .setSpellCorrectionEnabled(true);

        // Step 3: Start asynchronous processing of the image batch
        Future<List<OcrResult>> ocrFuture = ocrEngine.processAsync(imageFiles);

        // (Optional) Perform other work here while OCR runs in the background...
        System.out.println("OCR processing started in background...");

        // Step 4: Wait for all results and retrieve them
        List<OcrResult> ocrResults = ocrFuture.get(); // blocks until completion

        // Step 5: Display the recognized text for each file
        for (int i = 0; i < ocrResults.size(); i++) {
            System.out.println("File: " + imageFiles.get(i));
            System.out.println(ocrResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

### Εκτέλεση του Demo

1. **Συγγραφή** – `javac -cp "aspose-ocr.jar" ParallelOcrDemo.java`  
2. **Εκτέλεση** – `java -cp ".:aspose-ocr.jar" ParallelOcrDemo`  

Θα πρέπει να δείτε κάθε όνομα αρχείου PNG ακολουθούμενο από το εξαγόμενο κείμενο, χωρισμένα με παύλες.  

> **Σημείωση:** Αν αντιμετωπίσετε ένα `LicenseException`, βεβαιωθείτε ότι φορτώνετε την άδεια Aspose πριν δημιουργήσετε τη μηχανή:

```java
License lic = new License();
lic.setLicense("Aspose.OCR.Java.lic");
```

## Κλιμάκωση – Συμβουλές για OCR Ομαδικής Επεξεργασίας στον Πραγματικό Κόσμο

| Κατάσταση | Σύσταση |
|-----------|----------|
| **Hundreds of PNGs** | Increase the thread pool size via `ocrEngine.setThreadPoolSize(8)` (or higher, matching CPU cores). |
| **Memory constraints** | Process files in smaller chunks (e.g., batches of 50) and release the `OcrResult` list after each chunk. |
| **Variable image quality** | Enable `setPreprocessingOptions` to auto‑rotate, deskew, or enhance contrast before recognition. |
| **Multiple languages** | Call `setLanguage(OcrLanguage.ENGLISH, OcrLanguage.SPANISH)` and optionally set a custom dictionary. |
| **Error handling** | Wrap `ocrFuture.get()` in a try‑catch block for `ExecutionException` to log failed files without aborting the whole batch. |

## Συχνές Ερωτήσεις

**Q: Λειτουργεί αυτό με αρχεία JPEG ή TIFF;**  
A: Απόλυτα. Η μέθοδος `processAsync` δέχεται οποιαδήποτε μορφή υποστηρίζεται από το Aspose OCR (PNG, JPEG, TIFF, BMP, κλπ.). Απλώς αλλάξτε τις επεκτάσεις αρχείων στη λίστα σας.

**Q: Τι γίνεται αν χρειαστεί να διατηρήσω τη διάταξη (πίνακες, στήλες);**  
A: Το Aspose OCR παρέχει τη μέθοδο `getLayoutResult()` που επιστρέφει δεδομένα θέσης. Μπορείτε να ανακατασκευάσετε πίνακες αναλύοντας τα πλαίσια (bounding boxes) κάθε λέξης.

**Q: Μπορώ να το τρέξω σε πλατφόρμα serverless;**  
A: Ναι—απλώς πακετάρετε το JAR με τη βιβλιοθήκη Aspose και αναπτύξτε το σε AWS Lambda, Azure Functions ή Google Cloud Functions. Θυμηθείτε να διατηρήσετε την εκχώρηση μνήμης της λειτουργίας αρκετά υψηλή για το OCR thread pool.

## Συμπέρασμα

Τώρα έχετε μια πλήρη, αυτόνομη λύση **batch image OCR** που εξάγει αποδοτικά **κείμενο από PNG** αρχεία χρησιμοποιώντας το ασύγχρονο API του Aspose OCR σε Java. Ο οδηγός κάλυψε τα πάντα, από την προετοιμασία της λίστας αρχείων μέχρι τη διαμόρφωση γλώσσας και ορθογραφικού ελέγχου, την εκκίνηση παράλληλης επεξεργασίας, τη διαχείριση των αποτελεσμάτων και την κλιμάκωση της γραμμής παραγωγής για φορτία παραγωγής.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να αλλάξετε τη γλώσσα στα Γαλλικά, πειραματιστείτε με προσαρμοσμένα λεξικά ή ενσωματώστε το αποτέλεσμα σε έναν αναζητήσιμο δείκτη ElasticSearch. Ο ουρανός είναι το όριο όταν συνδυάζετε γρήγορο batch OCR με σύγχρονη ταυτόχρονη επεξεργασία Java.

Καλό κώδικα, και η εξαγωγή κειμένου σας να είναι γρήγορη και ακριβής! 

![Diagram showing parallel OCR workers handling multiple PNG files](/images/batch-ocr-diagram.png){: .center alt="Διάγραμμα επεξεργασίας παράλληλου OCR για πολλαπλά αρχεία PNG"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}