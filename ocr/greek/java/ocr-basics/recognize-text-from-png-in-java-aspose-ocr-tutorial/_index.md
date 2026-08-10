---
category: general
date: 2026-02-19
description: αναγνωρίστε κείμενο από PNG σε Java χρησιμοποιώντας Aspose OCR – μάθετε
  πώς να εξάγετε κείμενο από εικόνα Java και να επεξεργάζεστε την εικόνα με OCR αποδοτικά.
draft: false
keywords:
- recognize text from png
- extract text from image java
- process image with OCR
- Aspose OCR Java
- Java image processing
language: el
og_description: Αναγνωρίστε κείμενο από PNG σε Java με Aspose OCR. Αυτό το σεμινάριο
  δείχνει πώς να εξάγετε κείμενο από εικόνα Java και να επεξεργαστείτε την εικόνα
  με OCR βήμα-βήμα.
og_title: Αναγνώριση κειμένου από PNG σε Java – Πλήρης Οδηγός Aspose OCR
tags:
- OCR
- Java
- Image Processing
title: Αναγνώριση κειμένου από PNG σε Java – Εκπαιδευτικό σεμινάριο Aspose OCR
url: /el/java/ocr-basics/recognize-text-from-png-in-java-aspose-ocr-tutorial/
---

to recognize text from png using Aspose OCR". Should translate alt? The instruction: translate ALL text content naturally to Greek. Alt text is text content, so translate it. Title attribute also text, translate. But keep the markdown syntax.

Also headings translate.

Let's produce.

We need to keep code block placeholders unchanged.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση κειμένου από PNG σε Java – Πλήρης Οδηγός Aspose OCR

Έχετε χρειαστεί ποτέ να **αναγνωρίσετε κείμενο από PNG** αλλά δεν ήξερες ποια βιβλιοθήκη να επιλέξετε; Δεν είστε μόνοι—πολλοί προγραμματιστές Java αντιμετωπίζουν αυτό το πρόβλημα όταν προσπαθούν για πρώτη φορά να εξάγουν δεδομένα από εικόνες. Τα καλά νέα είναι ότι το Aspose OCR κάνει όλη τη διαδικασία σχεδόν άνετη, και σε αυτόν τον οδηγό θα δείτε ακριβώς πώς να **εξάγετε κείμενο από εικόνα java** έργα ενώ **επεξεργάζεστε εικόνα με OCR** με ασφαλή τρόπο για νήματα.

Στις επόμενες λίγες λεπτά θα δημιουργήσουμε ένα μικρό πρόγραμμα Java που φορτώνει ένα PNG, εκτελεί OCR στην CPU χρησιμοποιώντας έως και οκτώ νήματα, και εκτυπώνει τη αναγνωρισμένη συμβολοσειρά στην κονσόλα. Χωρίς εξωτερικές υπηρεσίες, χωρίς μυστικά κλειδιά API—απλός κώδικας Java που μπορείτε να αντιγράψετε‑επικολλήσετε και να τρέξετε σήμερα.

## Τι Θα Χρειαστείτε

- **Java 17** ή νεότερη (ο κώδικας μεταγλωττίζεται και με παλαιότερες εκδόσεις, αλλά η 17 είναι η ιδανική).  
- **Aspose.OCR for Java** JAR (λήψη από την ιστοσελίδα της Aspose ή μέσω Maven).  
- Ένα PNG αρχείο που θέλετε να διαβάσετε—π.χ. `document-page1.png` αποθηκευμένο κάπου στο δίσκο.  
- Το αγαπημένο σας IDE ή έναν απλό επεξεργαστή κειμένου και ένα τερματικό.

Αυτό είναι όλο. Αν έχετε αυτά, μπορούμε να βυθίσουμε κατευθείαν στη λύση.

![Java code to recognize text from png using Aspose OCR](image-placeholder.png "αναγνώριση κειμένου από png παράδειγμα Java"){alt="Κώδικας Java για αναγνώριση κειμένου από PNG χρησιμοποιώντας Aspose OCR"}

## Βήμα‑βήμα: αναγνώριση κειμένου από PNG

Παρακάτω χωρίζουμε την υλοποίηση σε σαφή, διαχειρίσιμα τμήματα. Κάθε τμήμα είναι μια επικεφαλίδα H2, ώστε να μπορείτε να μεταβείτε απευθείας στο μέρος που σας ενδιαφέρει.

### 1. Προσθήκη Aspose OCR στο Έργο Σας

**Γιατί;** Η μηχανή OCR βρίσκεται μέσα στη βιβλιοθήκη Aspose· χωρίς αυτήν ο μεταγλωττιστής δεν θα ξέρει τι είναι το `OcrEngine`.

Αν χρησιμοποιείτε Maven, προσθέστε αυτό το απόσπασμα στο `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

Για Gradle, είναι ως εξής:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Συμβουλή:** Πάντα ελέγχετε τον πιο πρόσφατο αριθμό έκδοσης· οι νεότερες κυκλοφορίες συχνά φέρνουν βελτιώσεις απόδοσης για πολυ‑νηματική επεξεργασία.

### 2. Δημιουργία και Ρύθμιση της Μηχανής OCR

**Γιατί;** Η δημιουργία ενός `OcrEngine` σας δίνει ένα έτοιμο προς χρήση αντικείμενο, και η ρύθμιση των παραμέτρων της συσκευής σας επιτρέπει να αξιοποιήσετε όλους τους πυρήνες CPU που έχετε.

```java
// Step 2: Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine to run on the CPU (no GPU required)
ocrEngine.getDevice().setDeviceType(OcrDeviceType.CPU);

// Use up to 8 threads – adjust based on your hardware
ocrEngine.getDevice().setThreadCount(8);
```

Εδώ ορίζουμε ρητά τη συσκευή σε `CPU`. Αν αργότερα μεταβείτε σε περιβάλλον με GPU, απλώς αλλάξτε την τιμή του enum—δεν χρειάζεται άλλη αλλαγή κώδικα.

### 3. Φόρτωση της Εικόνας PNG

**Γιατί;** Το OCR λειτουργεί πάνω σε ροή εικόνας, όχι απευθείας σε διαδρομή αρχείου. Η μετατροπή του αρχείου σε `ImageStream` αφαιρεί την εξάρτηση από τη μορφή.

```java
// Step 3: Load the image you want to process
String imagePath = "YOUR_DIRECTORY/document-page1.png";
ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

Αντικαταστήστε το `YOUR_DIRECTORY` με το πραγματικό φάκελο. Αν το αρχείο δεν βρεθεί, η μηχανή θα ρίξει `IOException`, το οποίο θα πιάσουμε αργότερα.

### 4. Εκτέλεση Αναγνώρισης και Λήψη Αποτελέσματος

**Γιατί;** Η μέθοδος `recognize()` κάνει το βαρέως βάρους έργο—ανίχνευση χαρακτήρων, γραμμών και διάταξης. Το επιστρεφόμενο `OcrResult` περιέχει το απλό κείμενο.

```java
// Step 4: Perform OCR and fetch the plain text
String recognizedText = ocrEngine.recognize().getText();
```

Μπορείτε επίσης να ζητήσετε αποτέλεσμα σε `Pdf` ή `Html`, αλλά για τον σκοπό του **extract text from image java** παραμένουμε στο απλό κείμενο.

### 5. Εξαγωγή του Κειμένου και Καθαρισμός

**Γιατί;** Ένα απλό `System.out.println` αρκεί για επίδειξη, αλλά σε πραγματική εφαρμογή πιθανότατα θα γράψετε σε αρχείο ή βάση δεδομένων.

```java
// Step 5: Display the recognized text
System.out.println("=== OCR Result ===");
System.out.println(recognizedText);
```

Επειδή το `OcrEngine` υλοποιεί το `AutoCloseable`, είναι καλή πρακτική να τυλίξετε τα πάντα σε μπλοκ `try‑with‑resources`. Αυτό εξασφαλίζει ότι οι εγγενείς πόροι απελευθερώνονται άμεσα.

### 6. Πλήρες, Εκτελέσιμο Παράδειγμα

Συνδυάζοντας όλα τα παραπάνω, ορίστε το πλήρες πρόγραμμα που μπορείτε να μεταγλωττίσετε και να τρέξετε:

```java
import com.aspose.ocr.*;

public class ParallelOcrExample {
    public static void main(String[] args) {
        // Use try-with-resources to guarantee cleanup
        try (OcrEngine ocrEngine = new OcrEngine()) {

            // Configure the engine for CPU and multi‑threading
            ocrEngine.getDevice().setDeviceType(OcrDeviceType.CPU);
            ocrEngine.getDevice().setThreadCount(8);

            // Load the PNG you want to process
            ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/document-page1.png"));

            // Run OCR and collect the text
            String recognizedText = ocrEngine.recognize().getText();

            // Show the result
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);

        } catch (Exception e) {
            // Handle common pitfalls: missing file, unsupported format, etc.
            System.err.println("Error during OCR processing:");
            e.printStackTrace();
        }
    }
}
```

**Αναμενόμενη έξοδος** (υποθέτοντας ότι το PNG περιέχει “Hello World”):

```
=== OCR Result ===
Hello World
```

Αν η εικόνα είναι πιο σύνθετη—πολλές γραμμές, πίνακες ή χειρόγραφες σημειώσεις—η έξοδος θα αντανακλά ακριβώς ό,τι ανιχνεύει το Aspose OCR, διατηρώντας τις αλλαγές γραμμής όπου χρειάζεται.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν το PNG είναι τεράστιο;

Μεγάλες εικόνες μπορούν να καταναλώσουν πολύ μνήμη. Μια πρακτική λύση είναι να **μειώσετε την ανάλυση** της εικόνας πριν τη δώσετε στη μηχανή:

```java
// Optional: downscale to 1500px width while preserving aspect ratio
ocrEngine.setImage(ImageStream.fromFile("big-image.png")
    .resize(1500, ResizeMode.PRESERVE_ASPECT_RATIO));
```

Η μείωση της ανάλυσης μειώνει το φορτίο της CPU χωρίς να θυσιάζει την ακρίβεια του OCR για τις περισσότερες τυπωμένες γραμματοσειρές.

### Μπορώ να τρέξω OCR σε PDF αντί για PNG;

Απολύτως. Το Aspose OCR δέχεται επίσης PDFs μέσω αντικειμένων `PdfDocument`. Η ίδια κλήση `recognize()` λειτουργεί, ώστε να μπορείτε να **process image with OCR** ανεξαρτήτως μορφής πηγής.

### Πώς βελτιώνω την ακρίβεια για μη‑λατινικά αλφάβητα;

Ορίστε τη γλώσσα πριν την αναγνώριση:

```java
ocrEngine.getLanguage().setLanguage(OcrLanguage.FRENCH);
```

Το Aspose παρέχει δεκάδες πακέτα γλωσσών· απλώς επιλέξτε αυτό που ταιριάζει στο περιεχόμενο της εικόνας σας.

### Είναι πάντα ωφέλιμος ο αριθμός των νημάτων;

Περισσότερα νήματα επιταχύνουν την επεξεργασία σε πολυπύρηνους επεξεργαστές, αλλά πέρα από τον αριθμό των φυσικών πυρήνων θα δείτε μειωμένα οφέλη. Αν παρατηρήσετε υψηλότερη χρήση CPU χωρίς ανάλογη αύξηση ταχύτητας, μειώστε τον αριθμό σε `Runtime.getRuntime().availableProcessors()`.

## Συμπέρασμα: Τι Καταφέραμε

Μόλις **αναγνωρίσαμε κείμενο από PNG** χρησιμοποιώντας ένα σύντομο πρόγραμμα Java, δείξαμε πώς να **extract text from image java** με Aspose OCR, και καλύψαμε τα βασικά βήματα για **process image with OCR** σε παραγωγικό επίπεδο. Ο κώδικας είναι αυτόνομος, οι εξηγήσεις απαντούν τόσο στο “πώς” όσο και στο “γιατί”, και οι συμβουλές αντιμετωπίζουν τα τυπικά προβλήματα που μπορεί να συναντήσετε.

## Τι Ακολουθεί;

- **Επεξεργασία παρτίδας:** Επανάληψη σε έναν φάκελο PNG και αποθήκευση κάθε αποτελέσματος σε αρχείο `.txt`.  
- **Δημιουργία PDF:** Χρήση της εξόδου OCR με Aspose.PDF για δημιουργία αναζητήσιμων PDF.  
- **Κλιμάκωση στο Cloud:** Ανάπτυξη του ίδιου κώδικα σε κοντέινερ που διαχειρίζεται Kubernetes και αφήστε το thread pool να προσαρμοστεί στους πόρους του pod.  

Πειραματιστείτε—αλλάξτε την εικόνα, προσαρμόστε τον αριθμό νημάτων ή αλλάξτε γλώσσες. Η μηχανή OCR είναι αρκετά ευέλικτη για τις περισσότερες περιπτώσεις, και με τη βάση που έχετε τώρα, η επέκταση είναι παιχνιδάκι.

Έχετε ερωτήσεις ή βρήκατε μια έξυπνη βελτιστοποίηση; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}