---
category: general
date: 2026-06-25
description: Πώς να βελτιώσετε το OCR με μια αξιόπιστη αλυσίδα προεπεξεργασίας. Μάθετε
  πώς να εξάγετε κείμενο με OCR, να ορίσετε το μέγεθος του μπλοκ και να δημιουργήσετε
  ένα παράδειγμα Aspose OCR σε Java.
draft: false
keywords:
- how to improve OCR
- extract text OCR
- set block size
- aspose OCR example
- OCR preprocessing pipeline
language: el
og_description: Πώς να βελτιώσετε το OCR χρησιμοποιώντας μια αλυσίδα προεπεξεργασίας.
  Αυτός ο οδηγός δείχνει πώς να εξάγετε κείμενο με OCR, να ορίσετε το μέγεθος του
  μπλοκ και να δημιουργήσετε ένα πλήρες παράδειγμα Aspose OCR.
og_title: Πώς να βελτιώσετε την ακρίβεια του OCR – Παράδειγμα OCR σε Java με Aspose
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: How to improve OCR with a robust preprocessing pipeline. Learn to extract
    text OCR, set block size, and build an Aspose OCR example in Java.
  headline: How to Improve OCR Accuracy with Java – Full Aspose OCR Example
  type: TechArticle
- description: How to improve OCR with a robust preprocessing pipeline. Learn to extract
    text OCR, set block size, and build an Aspose OCR example in Java.
  name: How to Improve OCR Accuracy with Java – Full Aspose OCR Example
  steps:
  - name: Build the Image Preprocessing Pipeline
    text: '```java // Import Aspose OCR classes import com.aspose.ocr.ImagePreprocess;
      import com.aspose.ocr.AdaptiveThreshold; import com.aspose.ocr.MedianFilter;'
  - name: Attach the Pipeline to the OCR Configuration
    text: '```java import com.aspose.ocr.OcrConfig;'
  - name: Create the OCR Engine with the Configured Options
    text: '```java import com.aspose.ocr.AsposeOCR;'
  - name: Recognize Text from the Target Image
    text: '```java import com.aspose.ocr.ImageRecognitionResult;'
  - name: Output the Extracted Text
    text: '```java // Step 5: Output the extracted text System.out.println(recognitionResult.getText());
      ```'
  - name: Expected Output
    text: 'If `noisy_doc.jpg` contains the sentence “**The quick brown fox jumps over
      the lazy dog.**”, you should see something like:'
  - name: What if the text is rotated?
    text: 'Aspose OCR can auto‑detect orientation, but for heavily skewed scans you
      might want to add a *deskew* filter before the adaptive threshold. The API provides
      `new DeskewFilter()` which you can chain:'
  - name: How does changing `setBlockSize` affect performance?
    text: A larger block size means the algorithm scans bigger neighborhoods, which
      can increase CPU time—roughly O(N × blockSize²). For real‑time scenarios (e.g.,
      scanning receipts on a mobile device), keep the block size between 11 and 15.
      For batch processing of high‑resolution PDFs, feel free to experimen
  - name: Can I use a different noise‑reduction filter?
    text: 'Absolutely. The pipeline is *fluent*—you can replace `MedianFilter` with
      `GaussianBlur` or stack multiple filters:'
  - name: Does this work with colored images?
    text: Aspose OCR automatically converts color images to grayscale before applying
      the preprocessing pipeline. If you need to preserve color information for downstream
      tasks (e.g., barcode detection), run the preprocessing on a copy of the image
      and keep the original untouched.
  type: HowTo
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Πώς να βελτιώσετε την ακρίβεια OCR με τη Java – Πλήρες παράδειγμα Aspose OCR
url: /el/java/advanced-ocr-techniques/how-to-improve-ocr-accuracy-with-java-full-aspose-ocr-exampl/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να βελτιώσετε την ακρίβεια OCR με Java – Πλήρες παράδειγμα Aspose OCR

Έχετε αναρωτηθεί ποτέ **πώς να βελτιώσετε τα αποτελέσματα OCR** όταν οι σαρώσεις σας φαίνονται ακατάστατες; Δεν είστε μόνοι. Θορυβώδη έγγραφα, άνιση φωτισμό και κείμενο χαμηλής αντίθεσης μπορούν να μετατρέψουν μια τέλεια μηχανή OCR σε ένα παιχνίδι μαντεψιάς. Τα καλά νέα; Ένα έξυπνο pipeline προεπεξεργασίας μπορεί να μετατρέψει αυτές τις ασταθείς εικόνες σε καθαρό, μηχανικά αναγνώσιμο κείμενο.

Σε αυτό το tutorial θα περάσουμε βήμα-βήμα από ένα πλήρες **παράδειγμα Aspose OCR** που δείχνει πώς να **εξάγετε κείμενο OCR** από ένα θορυβώδες JPEG, πώς να **ορίσετε το μέγεθος του μπλοκ** για προσαρμοστική κατωφλίωση, και γιατί κάθε βήμα είναι σημαντικό. Στο τέλος θα έχετε ένα έτοιμο πρόγραμμα Java που αυξάνει την ακρίβεια OCR χωρίς να θυσιάζει την απόδοση.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

- Εγκατεστημένο το Java Development Kit 8 ή νεότερο.
- Maven (ή το αγαπημένο σας εργαλείο κατασκευής) για να κατεβάσετε τη βιβλιοθήκη Aspose.OCR for Java.
- Ένα δείγμα εικόνας (`noisy_doc.jpg`) που περιέχει κείμενο με άνιση φωτεινότητα ή σπογγώδη θόρυβο.
- Βασική κατανόηση της σύνταξης Java — δεν απαιτείται κάτι περίπλοκο.

Αν κάποιο από τα παραπάνω δεν σας είναι γνωστό, κάντε μια παύση και φροντίστε να το έχετε έτοιμο. Το υπόλοιπο του οδηγού υποθέτει ότι μπορείτε να εκτελέσετε ένα απλό πρόγραμμα `java` από τη γραμμή εντολών.

## Επισκόπηση της Λύσης

Θα δημιουργήσουμε ένα pipeline τεσσάρων βημάτων:

1. **Δημιουργία pipeline προεπεξεργασίας OCR** – προσαρμοστική κατωφλίωση + φίλτρο διαμέσου.
2. **Σύνδεση του pipeline με τη ρύθμιση OCR** – λέει στο Aspose πώς να αντιμετωπίσει την εικόνα.
3. **Δημιουργία του κινητήρα OCR** με αυτές τις επιλογές.
4. **Εκτέλεση του κινητήρα** και **εξαγωγή κειμένου OCR** από το αρχείο στόχο.

Κάθε μέρος εξηγείται λεπτομερώς, ώστε να κατανοήσετε όχι μόνο *τι* πρέπει να πληκτρολογήσετε, αλλά και *γιατί* λειτουργεί ο κώδικας.

---

## Πώς να βελτιώσετε το OCR με ένα Pipeline Προεπεξεργασίας

Η καρδιά κάθε βελτίωσης OCR είναι ο καθαρισμός της εικόνας πριν την δει η μηχανή. Σκεφτείτε το βήμα προεπεξεργασίας ως μια λίστα ελέγχου πριν την πτήση ενός πιλότου· θέλετε όλα σε τάξη πριν την απογείωση. Δείτε πώς να το ρυθμίσετε σε Java χρησιμοποιώντας το Fluent API του Aspose.

### Βήμα 1: Δημιουργία του Pipeline Προεπεξεργασίας Εικόνας

```java
// Import Aspose OCR classes
import com.aspose.ocr.ImagePreprocess;
import com.aspose.ocr.AdaptiveThreshold;
import com.aspose.ocr.MedianFilter;

// Step 1: Build an image preprocessing pipeline (adaptive threshold + median filter)
ImagePreprocess preprocessPipeline = new ImagePreprocess()
        .add(new AdaptiveThreshold()
                .setBlockSize(15)   // size of the local window – this is where we **set block size**
                .setC(10))          // constant subtracted from mean
        .add(new MedianFilter(3)); // 3×3 median kernel removes salt‑and‑pepper noise
```

**Γιατί είναι σημαντικό:**  
- *Η προσαρμοστική κατωφλίωση* μετατρέπει μια εικόνα σε κλίμακα του γκρι σε καθαρό μαύρο‑άσπρο, αλλά το κάνει **τοπικά**. Ρυθμίζοντας το **μέγεθος του μπλοκ**, λέτε στον αλγόριθμο πόσο μεγάλη θα είναι η γειτονιά για τον υπολογισμό του τοπικού μέσου. Ένα μικρότερο μπλοκ καταγράφει λεπτομερείς λεπτομέρειες· ένα μεγαλύτερο μπλοκ εξομαλύνει τις ευρύτερες διακυμάνσεις.  
- *Το φίλτρο διαμέσου* καθαρίζει απομονωμένα θορυβώδη pixel χωρίς να θολώνει τις άκρες—ιδανικό για τη διατήρηση των καθαρών χαρακτήρων.

> **Συμβουλή:** Αν το έγγραφό σας έχει μεγάλες σκιές, αυξήστε το `setBlockSize` σε 25 ή 31. Αν το κείμενο είναι ήδη αρκετά ομοιόμορφο, ένα μέγεθος μπλοκ 11 ή 13 μπορεί να είναι αρκετό και θα τρέξει ελαφρώς πιο γρήγορα.

### Βήμα 2: Σύνδεση του Pipeline με τη Ρύθμιση OCR

```java
import com.aspose.ocr.OcrConfig;

// Step 2: Attach the preprocessing pipeline to the OCR configuration
OcrConfig ocrConfig = new OcrConfig()
        .setPreprocess(preprocessPipeline);
```

**Γιατί είναι σημαντικό:**  
Το αντικείμενο `OcrConfig` είναι εκεί όπου λέτε στο Aspose *πώς* να αντιμετωπίσει τις εισερχόμενες εικόνες. Καλώντας το `setPreprocess`, παραδίδετε το pipeline που μόλις δημιουργήσατε. Ο κινητήρας θα εφαρμόσει αυτόματα την προσαρμοστική κατωφλίωση και το φίλτρο διαμέσου πριν προσπαθήσει την αναγνώριση χαρακτήρων.

### Βήμα 3: Δημιουργία του Κινητήρα OCR με τις Ρυθμισμένες Επιλογές

```java
import com.aspose.ocr.AsposeOCR;

// Step 3: Create the OCR engine with the configured options
AsposeOCR ocrEngine = new AsposeOCR(ocrConfig);
```

**Γιατί είναι σημαντικό:**  
Η δημιουργία του `AsposeOCR` με προσαρμοσμένη ρύθμιση απομονώνει τις επιλογές σας από τις προεπιλογές. Αυτό κάνει τον κώδικα επαναχρησιμοποιήσιμο—απλώς ανταλλάξτε το `preprocessPipeline` με ένα διαφορετικό σύνολο φίλτρων αν θέλετε να πειραματιστείτε.

### Βήμα 4: Αναγνώριση Κειμένου από την Εικόνα Στόχο

```java
import com.aspose.ocr.ImageRecognitionResult;

// Step 4: Recognize text from the target image
ImageRecognitionResult recognitionResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/noisy_doc.jpg");
```

**Γιατί είναι σημαντικό:**  
Η κλήση `recognizeImage` ενεργοποιεί ολόκληρο το pipeline: φορτώνει το JPEG, εφαρμόζει τα βήματα προεπεξεργασίας, και μετά τροφοδοτεί το καθαρό bitmap στον κινητήρα OCR. Το αντικείμενο αποτελέσματος περιέχει το εξαγόμενο κείμενο, τους δείκτες εμπιστοσύνης, και ακόμη τα πλαίσια οριοθέτησης αν τα χρειαστείτε αργότερα.

### Βήμα 5: Εκτύπωση του Εξαγόμενου Κειμένου

```java
// Step 5: Output the extracted text
System.out.println(recognitionResult.getText());
```

Η εκτέλεση του προγράμματος θα πρέπει να εκτυπώσει ένα καθαρό μπλοκ κειμένου στην κονσόλα—συνήθως πολύ πιο ακριβές από το να τροφοδοτήσετε την ακατέργαστη εικόνα απευθείας στο Aspose.

---

## Πλήρες Παράδειγμα (Όλες οι Εισαγωγές Περιλαμβάνονται)

Παρακάτω είναι η πλήρης, έτοιμη προς εκτέλεση κλάση Java. Αντιγράψτε‑και‑επικολλήστε την στο `src/main/java/com/example/OcrDemo.java`, προσαρμόστε τη διαδρομή της εικόνας, και εκτελέστε `mvn compile exec:java` (ή την αγαπημένη σας εντολή εκτέλεσης).

```java
package com.example;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ImagePreprocess;
import com.aspose.ocr.AdaptiveThreshold;
import com.aspose.ocr.MedianFilter;
import com.aspose.ocr.OcrConfig;
import com.aspose.ocr.ImageRecognitionResult;

/**
 * Demonstrates how to improve OCR accuracy using a preprocessing pipeline.
 * This is a self‑contained Aspose OCR example that extracts text OCR from a noisy image.
 */
public class OcrDemo {
    public static void main(String[] args) {
        // 1️⃣ Build preprocessing pipeline (adaptive threshold + median filter)
        ImagePreprocess preprocessPipeline = new ImagePreprocess()
                .add(new AdaptiveThreshold()
                        .setBlockSize(15)   // <-- set block size for local thresholding
                        .setC(10))          // constant subtracted from the mean
                .add(new MedianFilter(3)); // 3×3 median kernel removes speckle noise

        // 2️⃣ Attach pipeline to OCR configuration
        OcrConfig ocrConfig = new OcrConfig()
                .setPreprocess(preprocessPipeline);

        // 3️⃣ Create OCR engine with our custom config
        AsposeOCR ocrEngine = new AsposeOCR(ocrConfig);

        // 4️⃣ Recognize text from the image (change path to your actual file)
        ImageRecognitionResult result = ocrEngine.recognizeImage("YOUR_DIRECTORY/noisy_doc.jpg");

        // 5️⃣ Print the extracted text to console
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Αν το `noisy_doc.jpg` περιέχει την πρόταση “**The quick brown fox jumps over the lazy dog.**”, θα δείτε κάτι όπως:

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
```

Παρατηρήστε την έλλειψη τυχαίων χαρακτήρων ή χαραγμένων συμβόλων—αυτά είναι τυπικά σημάδια έλλειψης βήματος προεπεξεργασίας. Προσθέτοντας το pipeline **βελτιώσαμε δραματικά την ακρίβεια OCR**.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν το κείμενο είναι περιστραμμένο;

Το Aspose OCR μπορεί να ανιχνεύσει αυτόματα την προσανατολισμό, αλλά για έντονα λοξά σκαναρίσματα ίσως θελήσετε να προσθέσετε ένα φίλτρο *deskew* πριν την προσαρμοστική κατωφλίωση. Το API παρέχει `new DeskewFilter()` το οποίο μπορείτε να αλυσίδωση:

```java
.add(new DeskewFilter())
```

### Πώς η αλλαγή του `setBlockSize` επηρεάζει την απόδοση;

Μεγαλύτερο μέγεθος μπλοκ σημαίνει ότι ο αλγόριθμος σαρώνει μεγαλύτερες γειτονιές, κάτι που μπορεί να αυξήσει τον χρόνο CPU—περίπου O(N × blockSize²). Για σενάρια πραγματικού χρόνου (π.χ. σάρωση αποδείξεων σε κινητό), κρατήστε το μέγεθος μπλοκ μεταξύ 11 και 15. Για μαζική επεξεργασία υψηλής ανάλυσης PDF, πειραματιστείτε με 25‑31.

### Μπορώ να χρησιμοποιήσω διαφορετικό φίλτρο μείωσης θορύβου;

Απόλυτα. Το pipeline είναι *fluent*—μπορείτε να αντικαταστήσετε το `MedianFilter` με `GaussianBlur` ή να συνδυάσετε πολλαπλά φίλτρα:

```java
.add(new GaussianBlur(1.5))
.add(new MedianFilter(3));
```

Απλώς θυμηθείτε ότι κάθε επιπλέον φίλτρο προσθέτει επιπλέον χρόνο επεξεργασίας.

### Λειτουργεί αυτό με έγχρωμες εικόνες;

Το Aspose OCR μετατρέπει αυτόματα τις έγχρωμες εικόνες σε γκρι κλίμακα πριν εφαρμόσει το pipeline προεπεξεργασίας. Αν χρειάζεται να διατηρήσετε τις χρωματικές πληροφορίες για επόμενες εργασίες (π.χ. ανίχνευση barcode), εκτελέστε την προεπεξεργασία σε αντίγραφο της εικόνας και κρατήστε το αρχικό ανέπαφο.

---

## Συμβουλές για Πραγματικά Έργα

- **Μαζική επεξεργασία:** Τυλίξτε το τμήμα αναγνώρισης σε βρόχο που διατρέχει έναν φάκελο εικόνων. Καταγράψτε κάθε όνομα αρχείου και το εξαγόμενο κείμενο για μεταγενέστερη ανάλυση.
- **Δείκτες εμπιστοσύνης:** `recognitionResult.getConfidence()` επιστρέφει float (0‑1). Χρησιμοποιήστε το για να φιλτράρετε αποτελέσματα χαμηλής εμπιστοσύνης και να τα σημαδέψετε για χειροκίνητη επανεξέταση.
- **Παράλληλη εκτέλεση:** Ο κινητήρας Aspose OCR είναι thread‑safe. Μπορείτε να δημιουργήσετε μια ομάδα νημάτων και να επεξεργαστείτε πολλές εικόνες ταυτόχρονα—απλώς μοιραστείτε το ίδιο αντικείμενο `AsposeOCR` για να αποφύγετε επαναλαμβανόμενη φόρτωση μοντέλου.
- **Καταγραφή (Logging):** Αντικαταστήστε το `System.out.println` με έναν πραγματικό logger (π.χ. SLF4J) για κώδικα παραγωγής. Αυτό διευκολύνει τον εντοπισμό σφαλμάτων όταν εμφανιστούν απρόσμενοι χαρακτήρες.

---

## Συμπέρασμα

Διασχίσαμε **πώς να βελτιώσετε το OCR** δημιουργώντας ένα προσαρμοσμένο **pipeline προεπεξεργασίας OCR** σε Java. Ρυθμίζοντας το μέγεθος του μπλοκ, προσθέτοντας φίλτρο διαμέσου, και ενσωματώνοντας το pipeline σε ένα **παράδειγμα Aspose OCR**, μπορείτε αξιόπιστα **να εξάγετε κείμενο OCR** ακόμη και από τις πιο ακατάστατες σαρώσεις. Ο πλήρης κώδικας είναι αυτόνομος, περιλαμβάνει όλες τις απαραίτητες εισαγωγές, και εκτυπώνει το καθαρό κείμενο στην κονσόλα.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να αντικαταστήσετε το φίλτρο διαμέσου με ένα bilateral filter, πειραματιστείτε με διαφορετικά μεγέθη μπλοκ, ή ενσωματώστε τους δείκτες εμπιστοσύνης σε έναν πίνακα ελέγχου ποιότητας. Ο ουρανός είναι το όριο όταν συνδυάζετε τη δυνατή μηχανή OCR του Aspose με προσεγμένη προεπεξεργασία εικόνας.

Έχετε ερωτήσεις ή βρήκατε κάποιο έξυπνο κόλπο; Αφήστε ένα σχόλιο παρακάτω—ας συνεχίσουμε τη συζήτηση. Καλό κώδικα!

## Τι Θα Μάθετε Στη Σειρά;

Οι παρακάτω οδηγίες καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [How to Set License and Verify Aspose.OCR License in Java](/ocr/english/java/ocr-basics/set-license/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [How to calculate skew angle java using Aspose.OCR](/ocr/english/java/ocr-basics/calculate-skew-angle/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}