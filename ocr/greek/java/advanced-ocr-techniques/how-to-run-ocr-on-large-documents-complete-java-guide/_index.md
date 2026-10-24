---
category: general
date: 2026-10-24
description: Μάθετε πώς να εξάγετε κείμενο από αρχεία TIFF με το σεμινάριο Aspose
  OCR Java, διαχειριζόμενοι μεγάλες εγγραφές αποδοτικά και λαμβάνοντας το κείμενο
  OCR γρήγορα.
draft: false
keywords:
- extract text from tiff
- aspose ocr java tutorial
- ocr large documents java
- extract text from scanned tiff
- java ocr tutorial
lastmod: 2026-10-24
og_description: Μάθετε πώς να εξάγετε κείμενο από αρχεία TIFF με το σεμινάριο Aspose
  OCR Java, διαχειριζόμενοι μεγάλες εγγραφές αποδοτικά και λαμβάνοντας το κείμενο
  OCR γρήγορα.
og_image_alt: 'Developer guide: extract text from TIFF using Aspose OCR Java'
og_title: Πώς να εξάγετε κείμενο από TIFF χρησιμοποιώντας το Aspose OCR σε Java
schemas:
- author: Aspose
  dateModified: '2026-10-24'
  description: Learn how to extract text from TIFF files with Aspose OCR Java tutorial,
    handling large documents efficiently and getting OCR text quickly.
  headline: How to extract text from TIFF using Aspose OCR in Java
  type: TechArticle
- questions:
  - answer: Yes, Aspose OCR for Java works completely in‑process and does not require
      a GUI environment.
    question: Can I run this on a headless server?
  - answer: The engine can stream any number of pages; practical limits are defined
      by available disk space and CPU, not by an internal page cap.
    question: How many pages can a single TIFF contain?
  - answer: Yes, you can set a `Rectangle` on the `Image` object before calling `recognize()`
      to focus on a region.
    question: Is it possible to limit OCR to specific regions of a page?
  - answer: Absolutely. Language packs for Arabic, Hebrew, and Persian handle bidirectional
      text out of the box.
    question: Does the library support right‑to‑left languages?
  - answer: Aspose offers site‑wide and concurrent‑user licenses; contact sales for
      volume pricing.
    question: What licensing model applies to large‑scale deployments?
  type: FAQPage
tags:
- extract text from tiff
- Aspose OCR
- Java OCR
- large documents
title: Πώς να εξάγετε κείμενο από TIFF χρησιμοποιώντας το Aspose OCR σε Java
url: /el/java/advanced-ocr-techniques/how-to-run-ocr-on-large-documents-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εξάγετε κείμενο από TIFF χρησιμοποιώντας το Aspose OCR σε Java

Έχετε αναρωτηθεί ποτέ **πώς να εκτελέσετε OCR** σε ένα τεράστιο αρχείο TIFF χωρίς η εφαρμογή σας να «παγώσει»; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν πρόβλημα όταν προσπαθούν να **αποκτήσουν κείμενο OCR** από σαρωμένες πολλαπλών σελίδων εικόνες, ειδικά όταν η απόδοση είναι κρίσιμη. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πρακτικό παράδειγμα που δείχνει ακριβώς πώς να **εξάγετε κείμενο από TIFF**, να αναγνωρίσετε σκαναρισμένο κείμενο και να διατηρήσετε την ταχύτητα για OCR μεγάλων εγγράφων.

## Γρήγορες απαντήσεις
- **Μπορεί το Aspose OCR να διαχειριστεί TIFF πολλαπλών σελίδων;** Ναι, μεταδίδει τις σελίδες μία τη φορά για να αποφεύγει τη μεγάλη χρήση μνήμης.  
- **Είναι η επεξεργασία πολλαπλών πυρήνων προαιρετική;** Είναι ενεργοποιημένη από προεπιλογή και επιταχύνει δραματικά το OCR μεγάλων εγγράφων.  
- **Ποια έκδοση της Java απαιτείται;** Java 17 ή νεότερη.  
- **Χρειάζομαι άδεια για ανάπτυξη;** Μια δωρεάν δοκιμή λειτουργεί για δοκιμές· απαιτείται εμπορική άδεια για παραγωγή.  
- **Πόσες γλώσσες υποστηρίζονται;** Πάνω από 70 πακέτα γλωσσών είναι ενσωματωμένα.

## Πώς να εξάγετε κείμενο από TIFF χρησιμοποιώντας το Aspose OCR;
Φορτώστε το TIFF, ενεργοποιήστε την επεξεργασία πολλαπλών πυρήνων, εκτελέστε την αναγνώριση και διαβάστε το κείμενο που προκύπτει—όλα σε λίγες απλές γραμμές Java. Πρώτα, δημιουργήστε ένα `OcrEngine`, δείξτε το στο ρεύμα εικόνας, ενεργοποιήστε το `setUseMultiCore(true)`, καλέστε `recognize()` και τέλος διαβάστε `ocrResult.getText()`. Αυτό το πρότυπο λειτουργεί για TIFF οποιουδήποτε μεγέθους και κλιμακώνεται με τον αριθμό των πυρήνων CPU, προσφέροντας γρήγορα, αξιόπιστα αποτελέσματα OCR χωρίς εξάντληση RAM.

## Τι είναι το Aspose OCR για Java;
`Aspose OCR for Java` είναι μια βιβλιοθήκη που μετατρέπει σαρωμένες εικόνες και PDF σε αναζητήσιμο, επεξεργάσιμο κείμενο. Υποστηρίζει πάνω από 70 γλώσσες, μπορεί να επεξεργαστεί αρχεία μεγαλύτερα από 2 GB και παρέχει ενσωματωμένη εκτέλεση πολλαπλών πυρήνων για επιτάχυνση μεγάλων εργασιών OCR. Η βιβλιοθήκη περιλαμβάνει επίσης βοηθητικά εργαλεία για προεπεξεργασία εικόνας, ανίχνευση γλώσσας και βαθμολόγηση εμπιστοσύνης, καθιστώντας την ολοκληρωμένη λύση για προγραμματιστές που χρειάζονται υψηλή ακρίβεια OCR σε πολλές μορφές αρχείων.

## Γιατί να χρησιμοποιήσετε το Aspose OCR για επεξεργασία μεγάλων εγγράφων;
Η βιβλιοθήκη μπορεί να διαχειριστεί **πάνω από 50 μορφές εισόδου** (συμπεριλαμβανομένων TIFF, JPEG, PNG, PDF) και επεξεργάζεται αρχεία με εκατοντάδες σελίδες χωρίς να φορτώνει ολόκληρο το έγγραφο στη μνήμη, μειώνοντας την κορυφαία κατανάλωση RAM έως και 80 %. Τα benchmarks δείχνουν τριπλασιασμό της ταχύτητας σε μηχάνημα με 6 πυρήνες όταν είναι ενεργοποιημένο το `setUseMultiCore(true)`.

## Προαπαιτούμενα

- Java 17 (ή νεότερη) εγκατεστημένη – η βιβλιοθήκη στοχεύει σε σύγχρονες εκδόσεις.  
- Maven ή Gradle για διαχείριση εξαρτήσεων (θα δείξουμε το απόσπασμα Maven).  
- Μια σαρωμένη εικόνα, κατά προτίμηση ένα πολυσελίδες TIFF με όνομα `large-document.tif`.  
- Τουλάχιστον 2 GB RAM· περισσότερο είναι χρήσιμο για πολύ υψηλή ανάλυση σκαναρίσματος.

## Βήμα 1: προσθέστε την εξάρτηση Aspose OCR

Πρώτα, προσθέστε τη βιβλιοθήκη στο έργο σας. Αν χρησιμοποιείτε Maven, προσθέστε το παρακάτω στο `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

> **Συμβουλή:** Ελέγχετε πάντα την πιο πρόσφατη έκδοση στο επίσημο αποθετήριο Aspose Maven για να επωφεληθείτε από διορθώσεις σφαλμάτων και βελτιώσεις απόδοσης.

## Βήμα 2: αρχικοποιήστε τη μηχανή OCR

Η δημιουργία μιας παρουσίας `OcrEngine` είναι το θεμέλιο. Σκεφτείτε το ως τον εγκέφαλο που θα ερμηνεύσει τη σαρωμένη εικόνα σας.  
`OcrEngine` είναι η κύρια κλάση που εκτελεί λειτουργίες OCR.

```java
import com.aspose.ocr.*;

public class ParallelExample {
    public static void main(String[] args) throws Exception {
        // Step 2.1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

Γιατί είναι σημαντικό: Η μηχανή κρατά όλες τις ρυθμιζόμενες επιλογές, όπως πακέτα γλωσσών και συμπεριφορά νήματος. Η σωστή ρύθμιση διασφαλίζει ότι μπορείτε να **εξάγετε κείμενο από TIFF** αποδοτικά αργότερα.

## Βήμα 3: φορτώστε την εικόνα σας

Το Aspose OCR μπορεί να διαβάσει εικόνες απευθείας από το σύστημα αρχείων ή ρεύματα. Για μεγάλα αρχεία TIFF, η ροή αποφεύγει τη φόρτωση ολόκληρου του αρχείου στη μνήμη ταυτόχρονα.  
`ImageStream.fromStream()` δημιουργεί ένα αντικείμενο εικόνας από ένα ρεύμα εισόδου.

```java
        // Step 3.1: Specify the path to the large document
        String imagePath = "YOUR_DIRECTORY/large-document.tif";

        // Step 3.2: Load the image as a stream
        ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

> **Σημείωση:** Αντικαταστήστε το `YOUR_DIRECTORY` με το πραγματικό φάκελο όπου βρίσκεται το TIFF. Αν προτιμάτε `FileInputStream`, μπορείτε να το περάσετε στο `ImageStream.fromStream()`.

## Βήμα 4: ενεργοποιήστε την επεξεργασία πολλαπλών πυρήνων

Η επεξεργασία ενός υψηλής ανάλυσης TIFF μπορεί να είναι απαιτητική για τον CPU. Το Aspose OCR σας επιτρέπει να ενεργοποιήσετε τη λειτουργία πολλαπλών πυρήνων, αφήνοντας τη μηχανή να αποφασίσει τον βέλτιστο αριθμό νημάτων. Αυτό είναι το κλειδί για **να αναγνωρίσετε σκαναρισμένο κείμενο** γρήγορα σε OCR μεγάλων εγγράφων.  
`setUseMultiCore(true)` ενεργοποιεί τη χρήση πολλαπλών πυρήνων CPU για παράλληλη επεξεργασία.

```java
        // Step 4.1: Turn on multi‑core mode (recommended for large docs)
        ocrEngine.getEngineOptions().setUseMultiCore(true);

        // Optional: If you need a fixed thread count, uncomment the next line
        // ocrEngine.getEngineOptions().setThreadCount(4);
```

Γιατί να το ενεργοποιήσετε; Όταν το `setUseMultiCore(true)` είναι ενεργό, η μηχανή διανέμει το φορτίο εργασίας στα διαθέσιμα πυρήνα, μειώνοντας δραματικά το χρόνο που απαιτείται για **να λάβετε κείμενο OCR** από κάθε σελίδα.

## Βήμα 5: εκτελέστε την αναγνώριση

Τώρα αρχίζει η βαριά δουλειά. Η κλήση `recognize()` επεξεργάζεται την εικόνα και επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει το εξαγόμενο κείμενο, βαθμούς εμπιστοσύνης και άλλα.  
`recognize()` εκτελεί τη διαδικασία OCR στην φορτωμένη εικόνα και επιστρέφει ένα `OcrResult`.

```java
        // Step 5.1: Perform OCR recognition
        OcrResult ocrResult = ocrEngine.recognize();
```

Αν χρειάζεται να διαχειριστείτε σφάλματα (π.χ. κατεστραμμένες σελίδες), τυλίξτε το σε μπλοκ try‑catch και ελέγξτε το `ocrResult.getErrorCode()`.

## Βήμα 6: εξαγωγή του αναγνωρισμένου κειμένου

Τέλος, εκτυπώστε το αποτέλεσμα OCR στην κονσόλα. Σε πραγματική εφαρμογή μπορεί να το γράψετε σε αρχείο, βάση δεδομένων ή να το τροφοδοτήσετε σε ευρετήριο αναζήτησης.  
`ocrResult.getText()` ανακτά το εξαγόμενο απλό κείμενο από το αποτέλεσμα OCR.

```java
        // Step 6.1: Print the extracted text
        System.out.println("=== OCR Output Start ===");
        System.out.println(ocrResult.getText());
        System.out.println("=== OCR Output End ===");
    }
}
```

Η εκτέλεση του προγράμματος θα πρέπει να εμφανίσει κάτι όπως:

```
=== OCR Output Start ===
Page 1: Sample extracted text from the first page of the document.
Page 2: Additional text recognized on the second page.
...
=== OCR Output End ===
```

Αυτή είναι η πλήρης ροή για **πώς να εκτελέσετε OCR** σε ένα μεγάλο σαρωμένο έγγραφο χρησιμοποιώντας το Aspose OCR Java.

![πώς να εκτελέσετε OCR σε μια σαρωμένη εικόνα TIFF](/images/ocr-java-example.png "Εικονογράφηση του πώς να εκτελέσετε OCR σε μια σαρωμένη εικόνα TIFF")

*Το κείμενο alt της εικόνας περιλαμβάνει τη βασική λέξη-κλειδί, βοηθώντας τόσο τις μηχανές αναζήτησης όσο και τους βοηθούς AI να κατανοήσουν το οπτικό περιεχόμενο.*

## Συνηθισμένες παραλλαγές & ακραίες περιπτώσεις

### 1. επεξεργασία PDF αντί για TIFF
Αν η πηγή σας είναι PDF, μετατρέψτε το πρώτα σε εικόνες (το Aspose PDF μπορεί να το κάνει) ή χρησιμοποιήστε `ocrEngine.setPdfDocument(...)`. Το υπόλοιπο pipeline παραμένει το ίδιο.

### 2. περιορισμός χρήσης μνήμης
Για εξαιρετικά μεγάλα αρχεία πολλαπλών σελίδων, εξετάστε την επεξεργασία μιας σελίδας τη φορά:

```java
for (int i = 0; i < ocrEngine.getImage().getPageCount(); i++) {
    ocrEngine.setPage(i);
    OcrResult pageResult = ocrEngine.recognize();
    // Append or store pageResult.getText()
}
```

Αυτή η προσέγγιση σας βοηθά να **εξάγετε κείμενο** χωρίς να εξαντλήσετε τη RAM.

### 3. αλλαγή πακέτων γλώσσας
Από προεπιλογή το Aspose OCR χρησιμοποιεί την αγγλική. Για **να αναγνωρίσετε σκαναρισμένο κείμενο** σε άλλες γλώσσες, φορτώστε τα αντίστοιχα δεδομένα γλώσσας:

```java
ocrEngine.getEngineOptions().setLanguage(Language.Spanish);
```

### 4. διαχείριση χαμηλής ποιότητας σκαναρίσματος
Αν η εικόνα είναι θορυβώδης, ενεργοποιήστε την προεπεξεργασία:

```java
ocrEngine.getEngineOptions().setPreprocess(true);
```

Η προεπεξεργασία εφαρμόζει φίλτρα όπως δυαδικοποίηση και διόρθωση κλίσης, βελτιώνοντας την ακρίβεια του εξαγόμενου κειμένου OCR.

## Συμβουλές απόδοσης

- **Κρατήστε το `setUseMultiCore(true)`** εκτός αν έχετε συγκεκριμένη απαίτηση για αριθμό νημάτων.  
- **Αποφύγετε τη φόρτωση ολόκληρου του αρχείου σε byte array**· χρησιμοποιήστε ρεύματα για αποδοτική μνήμη.  
- **Αναβαθμίστε στην πιο πρόσφατη έκδοση Aspose OCR**—οι βελτιώσεις απόδοσης είναι συχνές.  
- **Προφίλ το πρόγραμμα** με Java Flight Recorder αν υποπτεύεστε σημεία συμφόρησης.

## Συχνές ερωτήσεις

**Ε: Μπορώ να το τρέξω σε server χωρίς οθόνη;**  
Α: Ναι, το Aspose OCR for Java λειτουργεί πλήρως εντός διεργασίας και δεν απαιτεί περιβάλλον GUI.

**Ε: Πόσες σελίδες μπορεί να περιέχει ένα μόνο TIFF;**  
Α: Η μηχανή μπορεί να ρέει οποιονδήποτε αριθμό σελίδων· τα πρακτικά όρια καθορίζονται από τον διαθέσιμο χώρο δίσκου και CPU, όχι από εσωτερικό όριο σελίδων.

**Ε: Είναι δυνατόν να περιορίσω το OCR σε συγκεκριμένες περιοχές μιας σελίδας;**  
Α: Ναι, μπορείτε να ορίσετε ένα `Rectangle` στο αντικείμενο `Image` πριν καλέσετε `recognize()` για να εστιάσετε σε μια περιοχή.

**Ε: Υποστηρίζει η βιβλιοθήκη γλώσσες από δεξιά προς τα αριστερά;**  
Α: Απόλυτα. Τα πακέτα γλωσσών για Αραβικά, Εβραϊκά και Περσικά διαχειρίζονται το bidirectional κείμενο έτοιμα.

**Ε: Ποιο μοντέλο αδειοδότησης ισχύει για μεγάλες εγκαταστάσεις;**  
Α: Το Aspose προσφέρει άδειες site‑wide και concurrent‑user· επικοινωνήστε με το τμήμα πωλήσεων για τιμολόγηση κατά όγκο.

---

**Τελευταία ενημέρωση:** 2026-10-24  
**Δοκιμάστηκε με:** Aspose OCR for Java 24.10  
**Συγγραφέας:** Aspose

## Σχετικά Tutorials

- [Πώς να ενεργοποιήσετε GPU για OCR και να εξάγετε κείμενο από TIFF](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-and-extract-text-from-tiff/)
- [Εξαγωγή κειμένου από εικόνα με τον οδηγό Aspose OCR Java](/ocr/java/advanced-ocr-techniques/extract-text-from-image-with-aspose-ocr-java-guide/)
- [Παράδειγμα Aspose OCR Java για εξαγωγή κειμένου από περιοχή](/ocr/java/ocr-operations/aspose-ocr-java-example-extract-text-from-a-region/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}