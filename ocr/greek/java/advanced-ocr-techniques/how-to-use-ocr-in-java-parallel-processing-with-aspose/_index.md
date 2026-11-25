---
category: general
date: 2026-10-24
description: Μάθετε πώς να εκτελείτε OCR σε αρχεία PDF και εικόνες TIFF με Java χρησιμοποιώντας
  την παράλληλη επεξεργασία του Aspose OCR. Γρήγορος, αξιόπιστος οδηγός για προγραμματιστές.
draft: false
keywords:
- perform ocr pdf
- extract image text
- java ocr library
- process scanned pdf
- aspose ocr maven
lastmod: 2026-10-24
og_description: Εκτελέστε OCR σε αρχεία PDF με Java γρήγορα χρησιμοποιώντας την παράλληλη
  επεξεργασία του Aspose OCR. Αυτός ο οδηγός σας δείχνει πώς να ενεργοποιήσετε το
  multi‑threaded OCR, να ρυθμίσετε τα όρια των thread limits και να εξάγετε κείμενο
  τόσο από PDF όσο και από εικόνες TIFF αποδοτικά.
og_image_alt: Diagram of Java OCR pipeline with parallel processing using Aspose OCR
og_title: Εκτελέστε OCR σε PDF με Java – Παράλληλη επεξεργασία με Aspose
schemas:
- author: Aspose
  dateModified: '2026-10-24'
  description: Learn how to perform OCR on PDF and TIFF images in Java using Aspose
    OCR's parallel processing. Fast, reliable guide for developers.
  headline: How to perform OCR on PDF in Java with parallel processing
  type: TechArticle
- questions:
  - answer: Yes, Aspose OCR’s parallel engine runs on Windows, Linux, and macOS as
      long as the JVM can create native threads.
    question: Does the parallel mode work on any operating system?
  - answer: Absolutely—pass the password to `processImage` via the overload that accepts
      a `PdfLoadOptions` object.
    question: Can I process password‑protected PDFs?
  - answer: Aspose OCR supports Java 8, 11, 17, and later LTS releases.
    question: What Java versions are officially supported?
  - answer: For images under 300 dpi, accuracy drops to around 80 %; increasing the
      resolution to 400 dpi typically pushes it above 95 %.
    question: How accurate is the OCR for low‑resolution scans?
  - answer: Yes, a valid Aspose license removes evaluation limits and enables full‑performance
      features like parallel processing.
    question: Is a commercial license required for production use?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
- parallel processing
- PDF
title: Πώς να πραγματοποιήσετε OCR σε PDF με Java και παράλληλη επεξεργασία
url: /el/java/advanced-ocr-techniques/how-to-use-ocr-in-java-parallel-processing-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εκτελέσετε OCR σε PDF σε Java με παράλληλη επεξεργασία

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε OCR** για να εξάγετε κείμενο από ένα σαρωμένο έγγραφο χωρίς καμία δυσκολία; Σε αυτό το tutorial θα μάθετε πώς να **εκτελείτε OCR PDF** εργασίες σε Java χρησιμοποιώντας την ενσωματωμένη παράλληλη επεξεργασία του Aspose OCR. Η προσέγγιση λειτουργεί τόσο για πηγές PDF όσο και TIFF, μειώνει δραστικά το χρόνο επεξεργασίας και σας δίνει λεπτομερή έλεγχο της χρήσης νημάτων. Στο τέλος θα έχετε μια έτοιμη προς εκτέλεση κλάση Java που μπορεί να εξάγει κείμενο εικόνας από οποιοδήποτε σαρωμένο PDF ή πολυ‑σελίδα TIFF σε κλάσμα του χρόνου που απαιτεί μια λύση μονόνημα.

## Γρήγορες απαντήσεις
- **Τι κάνει το παράλληλο OCR;** Διαχωρίζει τις σελίδες σε πολλαπλούς πυρήνες CPU, επιτρέποντας την ταυτόχρονη επεξεργασία πολλών σελίδων.  
- **Ποια βιβλιοθήκη χρησιμοποιείται;** Aspose.OCR για Java, διαθέσιμη μέσω Maven Central.  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή λειτουργεί για ανάπτυξη· απαιτείται εμπορική άδεια για παραγωγή.  
- **Μπορώ να περιορίσω τον αριθμό των νημάτων;** Ναι—χρησιμοποιήστε `setMaxThreads(int)` για να περιορίσετε την πισίνα νημάτων.  
- **Είναι η λύση συμβατή με Java 8 και νεότερες;** Απόλυτα, λειτουργεί σε Java 8, 11, 17 και μεταγενέστερες.

## Τι είναι η εκτέλεση OCR PDF;
`perform OCR PDF` αναφέρεται στην ενέργεια εξαγωγής αναζητήσιμου, επεξεργάσιμου κειμένου από σαρωμένα PDF έγγραφα χρησιμοποιώντας οπτική αναγνώριση χαρακτήρων. Το Aspose OCR διαβάζει την raster εικόνα κάθε σελίδας, εκτελεί μια μηχανή αναγνώρισης και επιστρέφει απλό κείμενο Unicode που μπορείτε να αποθηκεύσετε, να ευρετήσετε ή να επεξεργαστείτε περαιτέρω.

## Γιατί να χρησιμοποιήσετε την παράλληλη επεξεργασία του Aspose OCR;
Το Aspose OCR υποστηρίζει **πάνω από 50 μορφές εισόδου** (συμπεριλαμβανομένων PDF, TIFF, JPEG, PNG, BMP) και μπορεί να διαχειριστεί **έγγραφα με εκατοντάδες σελίδες** χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη. Η παράλληλη επεξεργασία συνήθως μειώνει το χρόνο εκτέλεσης κατά **30‑70 % σε φορητό υπολογιστή με 4 πυρήνες** και έως **80 % σε διακομιστή με 32 πυρήνες**, σύμφωνα με το σύνολο benchmark του Aspose.

## Προαπαιτούμενα
- Java 8 ή νεότερη (ο κώδικας μεταγλωττίζεται επίσης με JDK 11).  
- Βιβλιοθήκη Aspose.OCR για Java – μπορείτε να κατεβάσετε το τελευταίο JAR από Maven Central (`com.aspose:aspose-ocr`).  
- Ένα αρχείο εικόνας (`.tif`, `.tiff`) ή ένα PDF που θέλετε να επεξεργαστείτε.  
- Μια μέτρια ποσότητα RAM—η παράλληλη επεξεργασία θα δημιουργήσει μερικά νήματα, αλλά το Aspose είναι αποδοτικό στη μνήμη.  

Αν τα έχετε, ας ξεκινήσουμε.

![Διάγραμμα που δείχνει τη ροή OCR – πώς να χρησιμοποιήσετε OCR σε Java με παράλληλη επεξεργασία](how-to-use-ocr-pipeline.png)

*Κείμενο alt εικόνας: παράδειγμα διαγράμματος χρήσης OCR*

---

## Πώς η παράλληλη επεξεργασία βελτιώνει την ταχύτητα του OCR;
Η παράλληλη επεξεργασία διανέμει την εργασία OCR σε όλους τους διαθέσιμους πυρήνες CPU, επιτρέποντας την ταυτόχρονη αναγνώριση πολλαπλών σελίδων. Σε ένα τυπικό φορητό υπολογιστή με τέσσερις πυρήνες, η ενεργοποίηση της παράλληλης λειτουργίας μειώνει το χρόνο επεξεργασίας ενός PDF 100 σελίδων από περίπου 45 δευτερόλεπτα σε περίπου 18 δευτερόλεπτα, ενώ ένας σταθμός εργασίας με 16 πυρήνες μπορεί να ολοκληρώσει την ίδια εργασία σε λιγότερο από 7 δευτερόλεπτα. Η αύξηση ταχύτητας έρχεται με ελάχιστο κόστος μνήμης επειδή κάθε νήμα εργάζεται σε ένα ενιαίο buffer σελίδας.

## Πώς να ρυθμίσετε το έργο σας και να προσθέσετε το Aspose OCR
Η σωστή ρύθμιση του έργου εξασφαλίζει ότι η μηχανή OCR μπορεί να φορτωθεί κατά το χρόνο εκτέλεσης. Προσθέτοντας την εξάρτηση Aspose OCR στο αρχείο κατασκευής σας, κάνετε τις κλάσεις διαθέσιμες στο classpath, κάτι που απαιτείται για οποιεσδήποτε επακόλουθες λειτουργίες OCR.

### Γιατί αυτό έχει σημασία
Πριν μπορέσετε να **εκτελέσετε OCR σε PDF** αρχεία, η βιβλιοθήκη πρέπει να βρίσκεται στο classpath σας. Χωρίς αυτήν, ο μεταγλωττιστής θα ρίξει `ClassNotFoundException` και θα κολλήσετε στο επόμενο βήμα.

### Πώς να το κάνετε
Αν χρησιμοποιείτε Maven, προσθέστε την εξάρτηση:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.10</version>
</dependency>
```

Για Gradle, προσθέστε:

```gradle
implementation 'com.aspose:aspose-ocr:24.10'
```

> **Συμβουλή:** Κρατήστε τον αριθμό έκδοσης συγχρονισμένο με τις σημειώσεις κυκλοφορίας του Aspose· οι νεότερες εκδόσεις συχνά περιλαμβάνουν βελτιώσεις απόδοσης για την παράλληλη επεξεργασία.

## Τι είναι η κλάση OcrEngine;
`OcrEngine` είναι η κύρια κλάση στο Aspose OCR που καθοδηγεί τη διαδικασία αναγνώρισης για εικόνες και έγγραφα PDF.  
`OcrEngine` είναι η βασική κλάση του Aspose OCR που εκτελεί εξαγωγή κειμένου από εικόνες και αρχεία PDF. Παρέχει μεθόδους για ενεργοποίηση της παράλληλης επεξεργασίας, ορισμό γλώσσας και ανάκτηση του αναγνωρισμένου κειμένου ως συμβολοσειρά. Επιπλέον, προσφέρει επιλογές διαμόρφωσης για βελτιστοποίηση μνήμης και επιλογή γλώσσας, καθιστώντας την ευέλικτη για ένα ευρύ φάσμα σεναρίων OCR.

## Πώς να δημιουργήσετε τη μηχανή OCR και να ενεργοποιήσετε την παράλληλη επεξεργασία
Δημιουργώντας μια παρουσία του `OcrEngine` και ενεργοποιώντας τη παράλληλη λειτουργία προετοιμάζει τη βιβλιοθήκη να διανείμει την εργασία σε πυρήνες CPU. Μπορείτε επίσης να διαμορφώσετε τη γλώσσα και άλλες ρυθμίσεις πριν επεξεργαστείτε οποιαδήποτε αρχεία, και προαιρετικά να περιορίσετε τον αριθμό των νημάτων ώστε να ταιριάζει στο περιβάλλον ανάπτυξής σας.

Φορτώστε τη μηχανή, ενεργοποιήστε τη παράλληλη λειτουργία, και προαιρετικά περιορίστε την πισίνα νημάτων:

```java
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getConfig().setUseParallelProcessing(true);
ocrEngine.getConfig().setMaxThreads(Runtime.getRuntime().availableProcessors() - 1);
```

- `setUseParallelProcessing(true)`: λέει στο Aspose να χωρίσει το φορτίο εργασίας σε διαθέσιμους πυρήνες CPU.  
- `setMaxThreads(...)`: μπορείτε να περιορίσετε την πισίνα νημάτων αν βρίσκεστε σε κοινόχρηστο διακομιστή ή θέλετε να αφήσετε περιθώριο για άλλες υπηρεσίες.  
- `processImage(inputPath)`: λειτουργεί τόσο για αρχεία εικόνας όσο και για έγγραφα PDF, έτσι η ίδια κλήση **εκτελεί OCR σε PDF** και σε TIFF εξίσου.

## Πώς να διαχειριστείτε διαφορετικούς τύπους εισόδου – PDF vs. TIFF
Ακόμη και αν το `processImage` δέχεται μια συμβολοσειρά διαδρομής, η υποκείμενη διαχείριση διαφέρει. Τα PDF συχνά περιέχουν πολλαπλές σελίδες, καθεμία από τις οποίες γίνεται ξεχωριστή εργασία OCR. Τα TIFF μπορούν να είναι μονοσέλιδα ή πολυσέλιδα· το Aspose αντιμετωπίζει κάθε καρέ ως σελίδα.

### Τι πρέπει να προσέξετε

| Είσοδος | Συνηθισμένο πρόβλημα | Προτεινόμενη διόρθωση |
|------|----------------|-----------------|
| PDF | Τα μεγάλα PDF μπορεί να εξαντλήσουν τη μνήμη αν όλες οι σελίδες φορτωθούν ταυτόχρονα. | Χρησιμοποιήστε `ocrEngine.getConfig().setMemoryOptimization(true);` (διαθέσιμο σε νεότερες εκδόσεις). |
| Multi‑page TIFF | Ορισμένα παλιά TIFF χρησιμοποιούν μη υποστηριζόμενη συμπίεση. | Μετατρέψτε πρώτα σε υποστηριζόμενη μορφή ή χρησιμοποιήστε το βοηθητικό `TiffImage` του Aspose. |

Παρακάτω υπάρχει ένα σύντομο απόσπασμα που δείχνει πώς να ανιχνεύσετε τον τύπο αρχείου και να καταγράψετε ένα φιλικό μήνυμα:

```java
String ext = Files.getFileExtension(inputPath).toLowerCase();
if (ext.equals("pdf")) {
    System.out.println("Processing PDF document...");
} else if (ext.equals("tif") || ext.equals("tiff")) {
    System.out.println("Processing TIFF image...");
} else {
    System.out.println("Unsupported file type: " + ext);
}
```

## Πώς να επαληθεύσετε το αποτέλεσμα – τι πρέπει να δείτε;
Μετά την εκτέλεση το πρόγραμμα εκτυπώνει το εξαγόμενο κείμενο στην κονσόλα, διατηρώντας τις αλλαγές γραμμής και τους διαχωριστές σελίδων. Εξετάστε το αποτέλεσμα για να βεβαιωθείτε ότι εμφανίζεται όλο το αναμενόμενο περιεχόμενο και ότι τυχόν μη αναγνώσιμες ενότητες έχουν σημειωθεί με σύμβολα κράτησης θέσης, υποδεικνύοντας πού το OCR δεν μπόρεσε να αναγνωρίσει χαρακτήρες.

Όταν το πρόγραμμα ολοκληρωθεί, θα δείτε το ακατέργαστο εξαγόμενο κείμενο να εκτυπώνεται στην κονσόλα. Για ένα απλό σαρωμένο τιμολόγιο, το αποτέλεσμα μπορεί να μοιάζει με:

```
Invoice #12345
Date: 2023‑07‑15
Total Amount: $1,250.00
...
```

Αν το OCR αντιμετωπίζει δυσκολίες με κάποια σελίδα, το Aspose εισάγει μια γραμμή κράτησης θέσης όπως `[Unrecognizable]`. Μπορείτε να τις φιλτράρετε αργότερα εάν χρειάζεστε καθαρά δεδομένα.

**Γρήγορος έλεγχος λογικής**

Εκτελέστε το πρόγραμμα με ένα γνωστό αρχείο δοκιμής και συγκρίνετε το αποτέλεσμα στην κονσόλα με το αρχικό έγγραφο. Αν το κείμενο ταιριάζει εντός ενός ορίου ακρίβειας 95 %, η ρύθμιση σας λειτουργεί σωστά.

## Πώς να βελτιώσετε την απόδοση – πότε να ρυθμίσετε τον αριθμό των νημάτων
Η ρύθμιση του αριθμού των νημάτων σας επιτρέπει να ισορροπήσετε τη χρήση CPU με το κόστος. Σε μηχανήματα με λιγότερους πυρήνες, ένας μικρότερος αριθμός νημάτων μειώνει τις αλλαγές περιβάλλοντος, ενώ σε διακομιστές με πολλούς πυρήνες μπορείτε να τον αυξήσετε για να εκμεταλλευτείτε πλήρως την παράλληλη επεξεργασία, πάντα δοκιμάζοντας για να βρείτε τη βέλτιστη ρύθμιση.

### Πώς να βρείτε το ιδανικό σημείο
Εκτελέστε μια σειρά δοκιμών benchmark με διαφορετικές τιμές `setMaxThreads`, μετρώντας το συνολικό χρόνο εκτέλεσης για ένα αντιπροσωπευτικό έγγραφο. Σχεδιάστε τα αποτελέσματα για να εντοπίσετε το σημείο όπου η προσθήκη περισσότερων νημάτων δεν προσφέρει πλέον βελτιώσεις ταχύτητας.

```java
long start = System.nanoTime();
ocrEngine.processImage("large-document.pdf");
long elapsed = System.nanoTime() - start;
System.out.println("Elapsed ms: " + elapsed / 1_000_000);
```

Εκτελέστε το πρόγραμμα με διαφορετικές τιμές `setMaxThreads` και καταγράψτε τους χρόνους. Επιλέξτε τη διαμόρφωση που παρέχει τη μεγαλύτερη απόδοση και κλειδώστε την για παραγωγή.

## Πώς να επεκτείνετε τη demo – επεξεργασία πολλαπλών αρχείων σε παρτίδες
Για να επεξεργαστείτε πολλά αρχεία αυτόματα, επαναλάβετε πάνω σε έναν φάκελο και καλέστε τη ρουτίνα OCR για κάθε έγγραφο. Αυτός ο εξωτερικός βρόχος μπορεί επίσης να παραλληλιστεί χρησιμοποιώντας ένα `ExecutorService` εάν χρειάζεται να διαχειριστείτε μεγάλο όγκο αρχείων ταυτόχρονα.

```java
Files.list(Paths.get("input-folder"))
     .filter(Files::isRegularFile)
     .forEach(path -> ocrEngine.processImage(path.toString()));
```

Αυτό το πρότυπο κλιμακώνεται καλά επειδή η μηχανή ήδη εκτελεί τις σελίδες κάθε αρχείου παράλληλα. Ο εξωτερικός βρόχος εκτελείται διαδοχικά, αλλά μπορείτε επίσης να υποβάλετε κάθε αρχείο σε ένα `ExecutorService` εάν χρειάζεται να εκμεταλλευτείτε μια τεράστια φάρμα CPU.

## Συνηθισμένα προβλήματα & πώς να τα αποφύγετε

| Σύμπτωμα | Πιθανή αιτία | Διόρθωση |
|----------|--------------|----------|
| `OutOfMemoryError` | Πάρα πολλές σελίδες φορτωμένες ταυτόχρονα (ιδιαίτερα με τεράστια PDF). | Ενεργοποιήστε τη βελτιστοποίηση μνήμης (`setMemoryOptimization(true)`) ή επεξεργαστείτε τα PDF σελίδα‑με‑σελίδα χρησιμοποιώντας `processPage`. |
| Κατεστραμμένοι χαρακτήρες | Λάθος ρύθμιση γλώσσας/σύνολο χαρακτήρων. | Καλέστε `ocrEngine.getConfig().setLanguage(OcrLanguage.English);` ή το κατάλληλο enum γλώσσας. |
| Αργή απόδοση παρά τη ρύθμιση parallel | Το OS περιορίζει τη δημιουργία νημάτων ή η JVM τρέχει με μικρό μέγεθος heap. | Αυξήστε τη σημαία heap `-Xmx` και ελέγξτε τα όρια νημάτων του OS (`ulimit -u`). |
| Κενό αποτέλεσμα | Η ανάλυση της εικόνας εισόδου < 300 dpi. | Αυξήστε την ανάλυση της εικόνας πριν το OCR ή χρησιμοποιήστε σαρωτή που παράγει υψηλότερη ανάλυση. |

## Ανασκόπηση – τι καλύψαμε
- **Πώς να εκτελέσετε OCR σε PDF** και αρχεία TIFF σε Java με το `OcrEngine` του Aspose.  
- Ενεργοποίηση **παράλληλης επεξεργασίας** για επιτάχυνση της αναγνώρισης.  
- Ρύθμιση του αριθμού των νημάτων για βέλτιστη απόδοση.  
- Διαχείριση ειδικών περιπτώσεων όπως μεγάλα PDF, έγγραφα με εκατοντάδες σελίδες και ρυθμίσεις γλώσσας.  
- Επέκταση της demo ενός αρχείου σε επεξεργασία παρτίδας για πραγματικά φορτία εργασίας.

## Επόμενα βήματα
Τώρα που έχετε κατακτήσει τα βασικά, σκεφτείτε να εξερευνήσετε τα παρακάτω σχετικά θέματα:

- **Εξαγωγή κειμένου εικόνας java** από χειρόγραφες σημειώσεις (ενεργοποιήστε `setHandwritingRecognition(true)`).  
- Ενσωμάτωση του αποτελέσματος OCR με το Apache Tika για εξαγωγή μεταδεδομένων.  
- Αποθήκευση των αποτελεσμάτων στο Elasticsearch για αναζητήσιμα αρχεία εγγράφων.  
- Χρήση του OCR του Aspose με άλλες γλώσσες όπως Python ή .NET—οι αρχές παραμένουν οι ίδιες.

Μη διστάσετε να πειραματιστείτε με διαφορετικά όρια νημάτων, μορφές εικόνας και πακέτα γλώσσας. Όσο περισσότερο πειραματιστείτε, τόσο καλύτερα θα κατανοήσετε τις ανταλλαγές μεταξύ ταχύτητας και ακρίβειας.

## Συχνές ερωτήσεις

**Ε: Λειτουργεί η παράλληλη λειτουργία σε οποιοδήποτε λειτουργικό σύστημα;**  
Α: Ναι, η παράλληλη μηχανή του Aspose OCR λειτουργεί σε Windows, Linux και macOS εφόσον η JVM μπορεί να δημιουργήσει εγγενή νήματα.

**Ε: Μπορώ να επεξεργαστώ PDF με κωδικό πρόσβασης;**  
Α: Απόλυτα—περάστε τον κωδικό στο `processImage` μέσω της υπερφόρτωσης που δέχεται ένα αντικείμενο `PdfLoadOptions`.

**Ε: Ποιες εκδόσεις Java υποστηρίζονται επίσημα;**  
Α: Το Aspose OCR υποστηρίζει Java 8, 11, 17 και μεταγενέστερες εκδόσεις LTS.

**Ε: Πόσο ακριβές είναι το OCR για σαρώσεις χαμηλής ανάλυσης;**  
Α: Για εικόνες κάτω από 300 dpi, η ακρίβεια πέφτει περίπου στο 80 %; η αύξηση της ανάλυσης στα 400 dpi συνήθως την ανεβάζει πάνω από 95 %.

**Ε: Απαιτείται εμπορική άδεια για χρήση σε παραγωγή;**  
Α: Ναι, μια έγκυρη άδεια Aspose αφαιρεί τα όρια αξιολόγησης και ενεργοποιεί πλήρεις δυνατότητες απόδοσης όπως η παράλληλη επεξεργασία.

**Τελευταία ενημέρωση:** 2026-10-24  
**Δοκιμή με:** Aspose.OCR 24.10 for Java  
**Συγγραφέας:** Aspose  






```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check for the newest version -->
</dependency>
```

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

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

```
Invoice #12345
Date: 02/15/2026
Total Amount: $1,250.00
Thank you for your business!
```

```java
if (ocrResult.getText().trim().isEmpty()) {
    System.err.println("No text detected – verify the image quality or try a different language.");
}
```

```java
int cores = Runtime.getRuntime().availableProcessors();
System.out.println("Available processors: " + cores);

// Experiment: set max threads to half the cores first
ocrEngine.getConfig().setMaxThreads(Math.max(1, cores / 2));
```

```java
long start = System.nanoTime();
ocrEngine.processImage(inputPath);
long elapsed = System.nanoTime() - start;
System.out.println("Elapsed time (ms): " + elapsed / 1_000_000);
```

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

## Σχετικά Μαθήματα

- [Πώς να χρησιμοποιήσετε OCR σε Java για εξαγωγή κειμένου από PDF Aspose OCR](/ocr/java/advanced-ocr-techniques/how-to-use-ocr-in-java-extract-text-from-pdf-aspose-ocr/)
- [Αναγνώριση κειμένου PDF με Aspose OCR σε Java – Πλήρης Οδηγός](/ocr/java/ocr-operations/recognize-pdf-text-with-aspose-ocr-in-java-complete-guide/)
- [Πώς να ενεργοποιήσετε GPU για OCR σε Java για εξαγωγή κειμένου από εικόνα](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}