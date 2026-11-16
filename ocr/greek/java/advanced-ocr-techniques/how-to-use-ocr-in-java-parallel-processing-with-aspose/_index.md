---
category: general
date: 2026-02-27
description: Μάθετε πώς να χρησιμοποιείτε OCR στη Java για να εξάγετε κείμενο εικόνας
  από αρχεία TIFF και PDF, χρησιμοποιώντας την παράλληλη επεξεργασία του Aspose OCR.
  Γρήγορος, απλός οδηγός.
draft: false
keywords:
- how to use ocr
- perform ocr on pdf
- extract text from tiff
- extract image text java
language: el
og_description: Μάθετε πώς να χρησιμοποιείτε OCR στη Java για να εξάγετε κείμενο εικόνας
  από αρχεία TIFF και PDF χρησιμοποιώντας την παράλληλη επεξεργασία του Aspose OCR.
og_title: Πώς να χρησιμοποιήσετε OCR στη Java – Παράλληλη επεξεργασία με το Aspose
tags:
- OCR
- Java
- Aspose
title: Πώς να χρησιμοποιήσετε OCR στη Java – Παράλληλη επεξεργασία με το Aspose
url: /el/java/advanced-ocr-techniques/how-to-use-ocr-in-java-parallel-processing-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε OCR σε Java – Παράλληλη Επεξεργασία με Aspose

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε OCR** για να εξάγετε κείμενο από ένα σαρωμένο έγγραφο χωρίς κόπο; Δεν είστε οι μόνοι. Οι προγραμματιστές συχνά αντιμετωπίζουν δυσκολίες όταν πρέπει να διαβάσουν κείμενο από εικόνες—ιδιαίτερα TIFF και PDF—διατηρώντας ταυτόχρονα την απόδοση.

Σε αυτό το tutorial θα σας δείξουμε μια πλήρη, έτοιμη‑για‑εκτέλεση λύση που **εξάγει κείμενο εικόνας σε Java** χρησιμοποιώντας Aspose OCR, ενεργοποιεί την παράλληλη επεξεργασία και ακόμη σας επιτρέπει να περιορίσετε τον αριθμό των νημάτων. Στο τέλος θα έχετε μια μοναδική κλάση που μπορεί **να εκτελεί OCR σε PDF** αρχεία και **να εξάγει κείμενο από TIFF** εικόνες σε κλάσμα του χρόνου που απαιτεί μια μονονηματική προσέγγιση.

> **Τι θα αποκομίσετε**  
> * Μια σαφή εξήγηση γιατί η παράλληλη OCR είναι σημαντική.  
> * Ένα πλήρες πρόγραμμα Java (χωρίς ελλιπείς εισαγωγές).  
> * Συμβουλές για τη ρύθμιση της χρήσης νημάτων και την αντιμετώπιση κοινών παγίδων.  

## Προαπαιτούμενα

- Java 8 ή νεότερη (ο κώδικας μεταγλωττίζεται και με JDK 11).  
- Βιβλιοθήκη Aspose.OCR for Java – μπορείτε να κατεβάσετε το τελευταίο JAR από το Maven Central (`com.aspose:aspose-ocr`).  
- Ένα αρχείο εικόνας (`.tif`, `.tiff`) ή ένα PDF που θέλετε να επεξεργαστείτε.  
- Μια μέτρια ποσότητα RAM—η παράλληλη επεξεργασία θα δημιουργήσει μερικά νήματα, αλλά το Aspose είναι αποδοτικό στη μνήμη.

Αν έχετε όλα αυτά, ας ξεκινήσουμε.

![Διάγραμμα που δείχνει τη ροή εργασίας OCR – πώς να χρησιμοποιήσετε OCR σε Java με παράλληλη επεξεργασία](how-to-use-ocr-pipeline.png)

*Κείμενο εναλλακτικής εικόνας: διάγραμμα παραδείγματος χρήσης OCR*

---

## Βήμα 1: Ρυθμίστε το Έργο σας και Προσθέστε το Aspose OCR

### Γιατί είναι σημαντικό

Πριν μπορέσετε **να εκτελέσετε OCR σε PDF** ή σε οποιαδήποτε εικόνα, η βιβλιοθήκη πρέπει να βρίσκεται στο classpath. Χωρίς αυτήν, ο μεταγλωττιστής θα πετάξει `ClassNotFoundException` και θα κολλήσετε στο βήμα δύο.

### Πώς να το κάνετε

Αν χρησιμοποιείτε Maven, προσθέστε την εξάρτηση:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check for the newest version -->
</dependency>
```

Για Gradle:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Pro tip:** Διατηρήστε τον αριθμό έκδοσης συγχρονισμένο με τις σημειώσεις κυκλοφορίας του Aspose· οι νεότερες εκδόσεις συχνά περιλαμβάνουν βελτιώσεις απόδοσης για την παράλληλη επεξεργασία.

---

## Βήμα 2: Δημιουργήστε τη Μηχανή OCR και Ενεργοποιήστε την Παράλληλη Επεξεργασία

### Γιατί είναι σημαντικό

Από προεπιλογή το Aspose OCR λειτουργεί σε ένα μόνο νήμα. Όταν του δώσετε ένα PDF πολλαπλών σελίδων ή μια δέσμη TIFF, η μηχανή θα επεξεργαστεί κάθε σελίδα διαδοχικά—αργά και αναποτελεσματικά. Η ενεργοποίηση της παράλληλης επεξεργασίας επιτρέπει στον επεξεργαστή να επεξεργάζεται πολλές σελίδες ταυτόχρονα, μειώνοντας δραστικά τον χρόνο εκτέλεσης.

### Κώδικας

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Path to the input file (TIFF or PDF)
        String inputPath = "YOUR_DIRECTORY/input.tif";

        // 2️⃣ Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Turn on parallel processing – this is the core of how to use OCR efficiently
        ocrEngine.getConfig().setUseParallelProcessing(true);

        // 4️⃣ (Optional) Limit threads – you can cap it to the number of cores you have
        // ocrEngine.getConfig().setMaxThreads(Runtime.getRuntime().availableProcessors());

        // 5️⃣ Run OCR
        OcrResult ocrResult = ocrEngine.processImage(inputPath);

        // 6️⃣ Output the recognised text
        System.out.println(ocrResult.getText());
    }
}
```

**Επεξήγηση των βασικών γραμμών**

- `setUseParallelProcessing(true)`: λέει στο Aspose να χωρίσει το φορτίο εργασίας στα διαθέσιμα πυρήνα CPU.  
- `setMaxThreads(...)`: μπορείτε να περιορίσετε το pool νημάτων αν βρίσκεστε σε κοινόχρηστο διακομιστή ή θέλετε να αφήσετε περιθώριο για άλλες υπηρεσίες.  
- `processImage(inputPath)`: λειτουργεί τόσο για αρχεία εικόνας όσο και για PDF, οπότε η ίδια κλήση **εκτελεί OCR σε PDF** και σε TIFF εξίσου.

---

## Βήμα 3: Διαχείριση Διαφορετικών Τύπων Εισόδου – PDF vs. TIFF

### Γιατί είναι σημαντικό

Παρόλο που το `processImage` δέχεται μια συμβολοσειρά διαδρομής, η εσωτερική διαχείριση διαφέρει. Τα PDF συχνά περιέχουν πολλές σελίδες, η καθεμία από τις οποίες γίνεται ξεχωριστή εργασία OCR. Τα TIFF μπορούν να είναι μονοσέλιδα ή πολυσέλιδα· το Aspose αντιμετωπίζει κάθε καρέ ως σελίδα.

### Σε τι πρέπει να προσέξετε

| Είσοδος | Συνηθισμένο πρόβλημα | Συνιστώμενη λύση |
|------|----------------|-----------------|
| PDF | Μεγάλα PDF μπορεί να εξαντλήσουν τη μνήμη αν φορτωθούν όλες οι σελίδες ταυτόχρονα. | Χρησιμοποιήστε `ocrEngine.getConfig().setMemoryOptimization(true);` (διαθέσιμο σε νεότερες εκδόσεις). |
| Πολυσέλιδο TIFF | Ορισμένα παλαιότερα TIFF χρησιμοποιούν μη υποστηριζόμενη συμπίεση. | Μετατρέψτε σε υποστηριζόμενο φορμά ή χρησιμοποιήστε το βοηθητικό `TiffImage` του Aspose. |

Παρακάτω ένα σύντομο απόσπασμα που δείχνει πώς να ανιχνεύσετε τον τύπο αρχείου και να καταγράψετε ένα φιλικό μήνυμα:

```java
import java.nio.file.*;

String ext = Files.probeContentType(Paths.get(inputPath)).toLowerCase();
if (ext.contains("pdf")) {
    System.out.println("Processing a PDF – expect multiple pages.");
} else if (ext.contains("tiff") || ext.contains("tif")) {
    System.out.println("Processing a TIFF image.");
} else {
    System.out.println("Unsupported file type. This demo works with PDF and TIFF.");
}
```

---

## Βήμα 4: Επαλήθευση του Αποτελέσματος – Τι Πρέπει να Δείτε;

Όταν το πρόγραμμα ολοκληρωθεί, θα δείτε το ακατέργαστο εξαγόμενο κείμενο εκτυπωμένο στην κονσόλα. Για ένα απλό σαρωμένο τιμολόγιο, η έξοδος μπορεί να μοιάζει με:

```
Invoice #12345
Date: 02/15/2026
Total Amount: $1,250.00
Thank you for your business!
```

Αν το OCR αντιμετωπίσει δυσκολία σε κάποια σελίδα, το Aspose εισάγει μια γραμμή placeholder όπως `[Unrecognizable]`. Μπορείτε να τις φιλτράρετε αργότερα αν χρειάζεστε καθαρά δεδομένα.

**Γρήγορος έλεγχος λογικής**

```java
if (ocrResult.getText().trim().isEmpty()) {
    System.err.println("No text detected – verify the image quality or try a different language.");
}
```

---

## Βήμα 5: Ρύθμιση Απόδοσης – Πότε να Προσαρμόσετε τον Αριθμό Νημάτων

### Γιατί είναι σημαντικό

Περισσότερα νήματα δεν σημαίνουν πάντα ταχύτερα αποτελέσματα. Σε laptop με 4 πυρήνες, η εκκίνηση 8 νημάτων μπορεί να προκαλέσει υπερβολική εναλλαγή περιβάλλοντος. Αντίθετα, σε διακομιστή με 32 πυρήνες ίσως θέλετε να αξιοποιήσετε όλη τη δύναμη.

### Πώς να βρείτε το ιδανικό σημείο

```java
int cores = Runtime.getRuntime().availableProcessors();
System.out.println("Available processors: " + cores);

// Experiment: set max threads to half the cores first
ocrEngine.getConfig().setMaxThreads(Math.max(1, cores / 2));
```

Τρέξτε το πρόγραμμα με διαφορετικές ρυθμίσεις και μετρήστε τον χρόνο:

```java
long start = System.nanoTime();
ocrEngine.processImage(inputPath);
long elapsed = System.nanoTime() - start;
System.out.println("Elapsed time (ms): " + elapsed / 1_000_000);
```

Καταγράψτε τους χρόνους, επιλέξτε τη διαμόρφωση που δίνει την καλύτερη απόδοση και κλειδώστε την για παραγωγή.

---

## Βήμα 6: Επέκταση του Demo – Επεξεργασία Πολλαπλών Αρχείων Μαζικά

Αν χρειάζεται να **εξάγετε κείμενο εικόνας java** από ολόκληρο φάκελο, τυλίξτε τη βασική λογική σε έναν βρόχο:

```java
Path folder = Paths.get("YOUR_DIRECTORY");
try (DirectoryStream<Path> stream = Files.newDirectoryStream(folder, "*.{tif,tiff,pdf}")) {
    for (Path file : stream) {
        System.out.println("\n--- Processing: " + file.getFileName() + " ---");
        OcrResult result = ocrEngine.processImage(file.toString());
        // Save or further process result.getText()
    }
}
```

Αυτό το μοτίβο κλιμακώνεται καλά επειδή η μηχανή ήδη εκτελεί τις σελίδες κάθε αρχείου παράλληλα. Ο εξωτερικός βρόχος τρέχει διαδοχικά, αλλά μπορείτε επίσης να υποβάλετε κάθε αρχείο σε ένα `ExecutorService` αν θέλετε να εκμεταλλευτείτε ένα τεράστιο farm CPU.

---

## Συνηθισμένες Παγίδες & Πώς να τις Αποφύγετε

| Συμπτωμα | Πιθανή αιτία | Διόρθωση |
|---------|--------------|-----|
| `OutOfMemoryError` | Πάρα πολλές σελίδες φορτωμένες ταυτόχρονα (ιδιαίτερα με τεράστια PDF). | Ενεργοποιήστε τη βελτιστοποίηση μνήμης (`setMemoryOptimization(true)`) ή επεξεργαστείτε το PDF σελίδα‑με‑σελίδα χρησιμοποιώντας `processPage`. |
| Παραμορφωμένοι χαρακτήρες | Λανθασμένη ρύθμιση γλώσσας/charset. | Καλέστε `ocrEngine.getConfig().setLanguage(OcrLanguage.English);` ή το αντίστοιχο enum γλώσσας. |
| Αργή απόδοση παρόλο που είναι ενεργοποιημένη η παράλληλη λειτουργία | Το OS περιορίζει τη δημιουργία νημάτων ή η JVM τρέχει με μικρό heap. | Αυξήστε τη σημαία `-Xmx`, και ελέγξτε τα όρια νημάτων του OS (`ulimit -u`). |
| Κενό αποτέλεσμα | Η ανάλυση της εικόνας εισόδου < 300 dpi. | Ανεβάστε την ανάλυση της εικόνας πριν το OCR ή χρησιμοποιήστε σαρωτή με υψηλότερη ανάλυση. |

---

## Ανακεφαλαίωση – Τι Καλύψαμε

- **Πώς να χρησιμοποιήσετε OCR** σε Java με το `OcrEngine` του Aspose.  
- Ενεργοποίηση **παράλληλης επεξεργασίας** για επιτάχυνση **εκτέλεσης OCR σε PDF** και **εξαγωγής κειμένου από TIFF**.  
- Ρύθμιση του αριθμού νημάτων για βέλτιστη απόδοση.  
- Διαχείριση ειδικών περιπτώσεων όπως μεγάλα PDF, πολυσέλιδα TIFF και ρυθμίσεις γλώσσας.  
- Επέκταση του demo ενός αρχείου σε επεξεργασία δέσμης για πραγματικές εργασίες.

---

## Επόμενα Βήματα

Τώρα που έχετε κατακτήσει τα βασικά, εξετάστε τα παρακάτω σχετικά θέματα:

- **Εξαγωγή κειμένου εικόνας java** από χειρόγραφα σημειώματα (ενεργοποιήστε `setHandwritingRecognition(true)`).  
- Ενσωμάτωση του αποτελέσματος OCR με Apache Tika για εξαγωγή μεταδεδομένων.  
- Αποθήκευση των αποτελεσμάτων σε Elasticsearch για αναζητήσιμα αρχεία.  
- Χρήση του Aspose OCR με άλλες γλώσσες όπως Python ή .NET—οι αρχές παραμένουν ίδιες.

Μη διστάσετε να πειραματιστείτε με διαφορετικά όρια νημάτων, φορμά εικόνας και πακέτα γλώσσας. Όσο περισσότερο πειραματιστείτε, τόσο καλύτερη θα είναι η κατανόησή σας για τις ανταλλαγές μεταξύ ταχύτητας και ακρίβειας.

---

### Καλή προγραμματιστική!

Αν αντιμετωπίσετε προβλήματα ή έχετε ιδέες για περαιτέρω βελτιστοποίηση, αφήστε ένα σχόλιο παρακάτω. Είμαι πάντα ανοιχτός σε συζήτηση για τεχνικές OCR—χωρίς άγχος, μόνο κώδικας.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}