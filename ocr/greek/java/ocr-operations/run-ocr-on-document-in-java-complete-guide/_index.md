---
category: general
date: 2026-06-16
description: Εκτελέστε OCR σε έγγραφο χρησιμοποιώντας Java σε λίγα μόνο βήματα. Μάθετε
  πώς να ρυθμίσετε το OCR, να αναγνωρίσετε κείμενο από TIFF και να εξάγετε κείμενο
  από πολυ‑σελίδες εικόνες.
draft: false
keywords:
- run OCR on document
- how to configure OCR
- recognize text from TIFF
- extract text from multi-page
language: el
og_description: Εκτελέστε OCR σε έγγραφο με Java. Αυτός ο οδηγός δείχνει πώς να ρυθμίσετε
  το OCR, να αναγνωρίσετε κείμενο από αρχεία TIFF και να εξάγετε κείμενο από εικόνες
  πολλαπλών σελίδων.
og_title: Εκτέλεση OCR σε Έγγραφο με Java – Αναλυτικός Οδηγός Βήμα‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Run OCR on document using Java in just a few steps. Learn how to configure
    OCR, recognize text from TIFF, and extract text from multi‑page images.
  headline: Run OCR on Document in Java – Complete Guide
  type: TechArticle
- description: Run OCR on document using Java in just a few steps. Learn how to configure
    OCR, recognize text from TIFF, and extract text from multi‑page images.
  name: Run OCR on Document in Java – Complete Guide
  steps:
  - name: '**Streamed processing** – Some OCR SDKs let you feed pages one‑by‑one instead
      of loading the entire TIFF into memory. Look for methods like `engine.setImageStream(...)`
      that accept an `InputStream`.'
    text: '**Streamed processing** – Some OCR SDKs let you feed pages one‑by‑one instead
      of loading the entire TIFF into memory. Look for methods like `engine.setImageStream(...)`
      that accept an `InputStream`.'
  - name: '**Memory limits** – If you hit `OutOfMemoryError`, lower the thread count
      or increase the JVM heap (`-Xmx2g`).'
    text: '**Memory limits** – If you hit `OutOfMemoryError`, lower the thread count
      or increase the JVM heap (`-Xmx2g`).'
  - name: '**Post‑processing** – Use regex or natural‑language libraries to clean
      up line breaks, remove headers/footers, or extract specific fields (e.g., invoice
      numbers).'
    text: '**Post‑processing** – Use regex or natural‑language libraries to clean
      up line breaks, remove headers/footers, or extract specific fields (e.g., invoice
      numbers).'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Εκτέλεση OCR σε Έγγραφο με Java – Πλήρης Οδηγός
url: /el/java/ocr-operations/run-ocr-on-document-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε Έγγραφο με Java – Πλήρης Οδηγός

Έχετε ποτέ χρειαστεί να **εκτελέσετε OCR σε έγγραφα** αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είστε μόνοι. Είτε ψηφιοποιείτε παλιά αρχεία είτε εξάγετε δεδομένα από σαρωμένες φόρμες, η λήψη αξιόπιστου κειμένου από εικόνες είναι ένα συχνό πρόβλημα.

Σε αυτό το tutorial θα περάσουμε από ένα πρακτικό, end‑to‑end παράδειγμα που δείχνει **πώς να ρυθμίσετε OCR**, **να αναγνωρίσετε κείμενο από TIFF**, και **να εξάγετε κείμενο από πολυ‑σελίδες** έγγραφα—όλα με λίγες μόνο γραμμές Java. Χωρίς περιττές πληροφορίες, μόνο μια λειτουργική λύση που μπορείτε να ενσωματώσετε στο πρότζεκτ σας σήμερα.

## Τι Θα Μάθετε

- Ρύθμιση μιας παρουσίας μηχανής OCR σε Java  
- Φόρτωση μιας πολυσελίδας εικόνας TIFF για επεξεργασία  
- Βελτιστοποίηση της μηχανής με ρύθμιση του αριθμού των νημάτων (το μέρος «πώς να ρυθμίσετε OCR»)  
- Εκτέλεση αναγνώρισης και εξαγωγή του κειμένου  
- Διαχείριση ειδικών περιπτώσεων όπως μεγάλα αρχεία και όρια μνήμης  

Στο τέλος αυτού του οδηγού θα μπορείτε να **εκτελέσετε OCR σε έγγραφα** με σιγουριά, και θα έχετε μια σταθερή βάση για να επεκτείνετε τη λύση σε PDFs, PNGs ή ακόμη και ζωντανές ροές από κάμερα.

## Προαπαιτούμενα

- Java 17 ή νεότερη (ο κώδικας χρησιμοποιεί τη λέξη‑κλειδί `var` για συντομία)  
- Μια βιβλιοθήκη OCR που εκθέτει μια κλάση `OcrEngine` (π.χ., *Aspose.OCR for Java* ή *Tesseract‑Java* wrapper).  
- Ένα αρχείο multi‑page TIFF με όνομα `multi_page.tif` τοποθετημένο σε γνωστό φάκελο.  

Αν λείπει η βιβλιοθήκη OCR, προσθέστε την στο `pom.xml` (Maven) ή στο `build.gradle` (Gradle) – οι ακριβείς συντεταγμένες εξαρτώνται από τον προμηθευτή, αλλά οι περισσότερες παρέχουν ένα μόνο JAR που μπορείτε να αναφέρετε.

---

## Βήμα 1: Αρχικοποίηση της Μηχανής OCR – Πώς να Εκτελέσετε OCR σε Έγγραφο

Πρώτα απ’ όλα: χρειάζεστε ένα αντικείμενο μηχανής που θα κάνει το σκληρό έργο. Σκεφτείτε το ως τον εγκέφαλο πίσω από τη λειτουργία.

```java
import com.example.ocr.OcrEngine;   // Replace with your actual package
import com.example.ocr.ImageStream;
import com.example.ocr.OcrResult;

public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();
```

> **Why this matters:** Η `OcrEngine` περιλαμβάνει όλες τις ρυθμίσεις αναγνώρισης, τα πακέτα γλωσσών και τις επιλογές αξιοποίησης υλικού. Η δημιουργία της μία φορά και η επαναχρησιμοποίησή της για πολλές εικόνες είναι πιο αποδοτική από τη συνεχή δημιουργία νέας παρουσίας.

---

## Βήμα 2: Φόρτωση του Multi‑Page TIFF – Εξαγωγή Κειμένου από Πολυσελίδες Εικόνες

Τώρα κατευθύνουμε τη μηχανή στο αρχείο που θέλουμε να επεξεργαστούμε. Το TIFF είναι κοινή μορφή για σαρωμένα έγγραφα επειδή μπορεί να αποθηκεύσει πολλές σελίδες σε ένα μόνο αρχείο.

```java
        // Step 2: Load the multi‑page image to be processed
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multi_page.tif"));
```

> **Pro tip:** Αν το TIFF σας βρίσκεται σε κοινόχρηστο δίκτυο, χρησιμοποιήστε `ImageStream.fromUrl(...)` αντί αυτού. Αυτό αποφεύγει την αντιγραφή ολόκληρου του αρχείου στη μνήμη πριν ξεκινήσει το OCR.

---

## Βήμα 3: Πώς να Ρυθμίσετε το OCR για Μέγιστη Απόδοση

Οι βιβλιοθήκες OCR συνήθως τρέχουν σε ένα μόνο νήμα, κάτι που μπορεί να γίνει bottleneck σε σύγχρονες πολυπύρηνες μηχανές. Εδώ απαντάμε στο κομμάτι «**πώς να ρυθμίσετε OCR**» του παζλ.

```java
        // Step 3: Configure the engine to use all available CPU cores
        int availableCores = Runtime.getRuntime().availableProcessors();
        engine.getRecognitionSettings().setThreadCount(availableCores);
```

> **Why this works:** Αν ταιριάξετε τον αριθμό των νημάτων με τον αριθμό των λογικών επεξεργαστών, η μηχανή OCR μπορεί να επεξεργάζεται διαφορετικές σελίδες παράλληλα. Σε ένα laptop με 4‑πυρήνες θα δείτε περίπου 3‑4× αύξηση ταχύτητας όταν δουλεύετε με πολυ‑σελίδες έγγραφα.  

> **Edge case:** Ορισμένα περιβάλλοντα (π.χ., Docker containers με περιορισμένα CPU quotas) αναφέρουν περισσότερους πυρήνες από όσους επιτρέπεται να χρησιμοποιήσουν. Σε τέτοιες περιπτώσεις, περιορίστε τον αριθμό των νημάτων χειροκίνητα: `engine.getRecognitionSettings().setThreadCount(Math.min(availableCores, 2));`

---

## Βήμα 4: Αναγνώριση Κειμένου από TIFF – Η Κεντρική Κλήση OCR

Με όλα συνδεδεμένα, ήρθε η ώρα να τρέξουμε την αναγνώριση. Αυτή η ενιαία κλήση θα διασχίσει κάθε σελίδα του TIFF, θα εφαρμόσει τα μοντέλα γλώσσας και θα επιστρέψει ένα σύνθετο αποτέλεσμα.

```java
        // Step 4: Perform the OCR recognition
        OcrResult result = engine.recognize();
```

> **What’s happening under the hood?** Η μηχανή χωρίζει το TIFF σε ξεχωριστές raster εικόνες, τροφοδοτεί καθεμία στο νευρωνικό δίκτυο OCR και ενώνει τα κειμενικά αποτελέσματα. Αν χρειάζεστε λεπτομέρεια ανά σελίδα, το `result.getPages()` θα σας δώσει μια λίστα με αντικείμενα `OcrPageResult`.

---

## Βήμα 5: Έξοδος του Αναγνωρισμένου Κειμένου – Επαλήθευση της Εξαγωγής

Τέλος, εκτυπώνουμε το εξαγόμενο κείμενο στην κονσόλα. Σε μια πραγματική εφαρμογή πιθανότατα θα το γράφατε σε βάση δεδομένων ή σε αρχείο JSON.

```java
        // Step 5: Output the recognized text
        System.out.println(result.getText());
    }
}
```

**Expected output (truncated):**

```
Page 1:
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00

Page 2:
Terms and Conditions...
```

Αν δείτε ακατανόητο κείμενο αντί για καθαρούς χαρακτήρες, ελέγξτε ξανά ότι τα σωστά πακέτα γλώσσας είναι εγκατεστημένα και ότι η εικόνα δεν είναι πολύ θορυβώδης. Προ‑επεξεργασίες όπως η διόρθωση κλίσης ή η δυαδικοποίηση μπορούν να βελτιώσουν δραστικά την ακρίβεια.

---

## Διαχείριση Μεγάλων Πολυσελίδων Αρχείων – Συμβουλές για Εξαγωγή

Ακόμη και αν έχουμε ήδη δείξει τη βασική ροή, τα πραγματικά έγγραφα μπορεί να είναι τεράστια. Εδώ είναι μερικές επιπλέον παρατηρήσεις:

1. **Επεξεργασία ροής** – Ορισμένα OCR SDK επιτρέπουν την τροφοδοσία των σελίδων μία‑μια αντί για φόρτωση ολόκληρου του TIFF στη μνήμη. Αναζητήστε μεθόδους όπως `engine.setImageStream(...)` που δέχονται ένα `InputStream`.  
2. **Όρια μνήμης** – Αν αντιμετωπίσετε `OutOfMemoryError`, μειώστε τον αριθμό των νημάτων ή αυξήστε το heap της JVM (`-Xmx2g`).  
3. **Μετα‑επεξεργασία** – Χρησιμοποιήστε regex ή βιβλιοθήκες φυσικής γλώσσας για να καθαρίσετε τις αλλαγές γραμμής, να αφαιρέσετε κεφαλίδες/υποσέλιδα ή να εξάγετε συγκεκριμένα πεδία (π.χ., αριθμούς τιμολογίων).

---

## Πλήρες Παράδειγμα Εργασίας (Όλα τα Βήματα Συνδυασμένα)

Παρακάτω είναι η πλήρης, έτοιμη προς εκτέλεση κλάση Java. Επικολλήστε την στο IDE σας, προσαρμόστε το πακέτο/τις εισαγωγές, και τρέξτε την.

```java
package com.example.ocrdemo;

import com.example.ocr.OcrEngine;
import com.example.ocr.ImageStream;
import com.example.ocr.OcrResult;

/**
 * Demonstrates how to run OCR on document images, configure the engine,
 * recognize text from TIFF files, and extract text from multi‑page documents.
 */
public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Create the OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Load the multi‑page TIFF image
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multi_page.tif"));

        // Configure the engine to use all CPU cores (how to configure OCR)
        int cores = Runtime.getRuntime().availableProcessors();
        engine.getRecognitionSettings().setThreadCount(cores);

        // Perform recognition (recognize text from TIFF)
        OcrResult result = engine.recognize();

        // Output the extracted text (extract text from multi‑page)
        System.out.println(result.getText());
    }
}
```

> **Pro tip:** Τυλίξτε την κλήση `recognize()` σε ένα `try‑catch` block για να χειριστείτε το `OcrException` με χάρη, ειδικά όταν αντιμετωπίζετε κατεστραμμένα αρχεία εικόνας.

---

## Συμπέρασμα

Σας δείξαμε πώς να **εκτελέσετε OCR σε έγγραφα** χρησιμοποιώντας Java, καλύπτοντας όλα από την αρχικοποίηση της μηχανής μέχρι την εξαγωγή κειμένου από πολυ‑σελίδες. Κατανοώντας **πώς να ρυθμίσετε OCR**, μπορείτε να εξάγετε κάθε δυνατότητα από τους σύγχρονους επεξεργαστές, ενώ τα βήματα για **αναγνώριση κειμένου από TIFF** και **εξαγωγή κειμένου από πολυ‑σελίδες** σας δίνουν μια σταθερή βάση για οποιοδήποτε έργο ψηφιοποίησης εγγράφων.

Τι ακολουθεί; Δοκιμάστε να αντικαταστήσετε το TIFF με PDF, πειραματιστείτε με προσαρμοσμένα μοντέλα γλώσσας, ή στέλνετε το αποτέλεσμα σε ευρετήριο αναζήτησης. Ο ουρανός είναι το όριο μόλις έχετε αυτή τη βάση.

Αν αντιμετωπίσετε δυσκολίες—ίσως η βιβλιοθήκη OCR που επιλέξατε χρησιμοποιεί διαφορετικό API—αφήστε ένα σχόλιο παρακάτω. Καλό κώδικα και καλή διασκέδαση με τη μετατροπή των σαρωμένων σελίδων σε αναζητήσιμο κείμενο!

## Τι Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετα χαρακτηριστικά API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to recognize tiff with Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}