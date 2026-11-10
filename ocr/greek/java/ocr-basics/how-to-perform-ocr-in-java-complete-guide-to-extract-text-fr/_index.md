---
category: general
date: 2026-06-06
description: πώς να εκτελέσετε OCR σε Java – γρήγορη εξαγωγή κειμένου από εικόνα,
  μετατροπή εικόνας σε κείμενο και ανάγνωση κειμένου από jpg χρησιμοποιώντας ένα απλό
  παράδειγμα κώδικα.
draft: false
keywords:
- how to perform OCR
- ocr in java
- extract text from image
- convert image to text
- read text from jpg
language: el
og_description: πώς να εκτελέσετε OCR στην Java – μάθετε πώς να εξάγετε κείμενο από
  εικόνα, να μετατρέψετε εικόνα σε κείμενο και να διαβάσετε κείμενο από jpg με ένα
  έτοιμο παράδειγμα.
og_title: Πώς να εκτελέσετε OCR σε Java – Οδηγός βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  headline: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  type: TechArticle
- description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  name: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  steps:
  - name: What You’ll Learn
    text: '- Install an OCR library (yes, **ocr in java** is easier than you think).
      - Create and configure an OCR engine instance. - Load a JPG (or any image) and
      set the language. - Process the image and **extract text from image** files.
      - Print the recognized string to the console.'
  - name: Expected Output
    text: 'If `input.jpg` contains the Mongolian phrase “Сайн байна уу?” the console
      will show:'
  - name: 'Pro Tip: Batch Processing'
    text: 'If you need to **extract text from image** files in bulk, wrap the core
      logic in a loop:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Πώς να εκτελέσετε OCR σε Java – Πλήρης οδηγός για την εξαγωγή κειμένου από
  εικόνες
url: /el/java/ocr-basics/how-to-perform-ocr-in-java-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εκτελέσετε OCR σε Java – Πλήρης Οδηγός για την Εξαγωγή Κειμένου από Εικόνες

Έχετε αναρωτηθεί ποτέ **πώς να εκτελέσετε OCR** σε μια φωτογραφία που τραβήξατε με το τηλέφωνό σας; Δεν είστε ο μόνος. Είτε δημιουργείτε μια εφαρμογή σάρωσης αποδείξεων είτε απλώς χρειάζεστε να εξάγετε κείμενο από ένα σαρωμένο PDF, **πώς να εκτελέσετε OCR** σε Java είναι μια δεξιότητα που αποδίδει γρήγορα. Σε αυτόν τον οδηγό θα περάσουμε από ένα πρακτικό παράδειγμα που **εξάγει κείμενο από αρχεία εικόνας**, **μετατρέπει εικόνα σε κείμενο**, και ακόμη δείχνει πώς να **διαβάσετε κείμενο από jpg** με λίγες μόνο γραμμές κώδικα.

> *Συμβουλή επαγγελματία:* Η ίδια προσέγγιση λειτουργεί για PNG, BMP ή οποιαδήποτε μορφή υποστηρίζει η μηχανή OCR—απλώς αλλάξτε το όνομα του αρχείου.

## Πώς να Εκτελέσετε OCR σε Java – Επισκόπηση

Η Οπτική Αναγνώριση Χαρακτήρων (OCR) είναι η τεχνολογία που μετατρέπει εικόνες γραμμάτων σε πραγματικό, αναζητήσιμο κείμενο. Στο οικοσύστημα της Java υπάρχουν πολλές βιβλιοθήκες—Tesseract, Asprise και εμπορικά SDK—όλες εκθέτουν μια παρόμοια ροή εργασίας: φορτώνετε μια εικόνα, λέτε στη μηχανή ποια γλώσσα να περιμένει, εκτελείτε την αναγνώριση και παίρνετε το αποτέλεσμα. Παρακάτω θα χρησιμοποιήσουμε μια γενική κλάση `OcrEngine` για να διατηρήσουμε το παράδειγμα σαφές, αλλά μπορείτε να την αντικαταστήσετε με οποιαδήποτε συγκεκριμένη υλοποίηση που ακολουθεί το ίδιο μοτίβο.

### Τι Θα Μάθετε

- Εγκατάσταση βιβλιοθήκης OCR (ναι, **ocr in java** είναι πιο εύκολο απ' ό,τι νομίζετε).
- Δημιουργία και ρύθμιση μιας παρουσίας OCR engine.
- Φόρτωση ενός JPG (ή οποιασδήποτε εικόνας) και ορισμός της γλώσσας.
- Επεξεργασία της εικόνας και **εξαγωγή κειμένου από εικόνα** αρχεία.
- Εκτύπωση του αναγνωρισμένου string στην κονσόλα.

Στο τέλος θα έχετε ένα αυτόνομο πρόγραμμα Java που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο και να τρέξετε αμέσως.

![παράδειγμα εκτέλεσης OCR](ocr-example.png "εικονογράφηση του πώς να εκτελέσετε OCR σε Java")

## Βήμα 1 – Εγκατάσταση και Εισαγωγή Βιβλιοθήκης OCR (ocr in java)

Πριν γράψετε μια γραμμή Java, χρειάζεστε μια βιβλιοθήκη που πραγματικά κάνει το βαρέως έργο. Αν χρησιμοποιείτε Maven, προσθέστε μια εξάρτηση όπως αυτή (αντικαταστήστε το `com.example.ocr` με το πραγματικό group ID του επιλεγμένου SDK):

```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>ocr-sdk</artifactId>
    <version>1.4.2</version>
</dependency>
```

Αν προτιμάτε Gradle:

```gradle
implementation 'com.example:ocr-sdk:1.4.2'
```

Μόλις το JAR είναι στο classpath, εισάγετε τις κλάσεις που θα χρειαστείτε:

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;
```

> **Γιατί είναι σημαντικό:** Η εισαγωγή των σωστών κλάσεων αποτρέπει σφάλματα “cannot find symbol” και κάνει το IDE σας ευχαριστημένο—τίποτα δεν είναι πιο απογοητευτικό από μια ελλιπή εισαγωγή όταν προσπαθείτε να **μετατρέψετε εικόνα σε κείμενο**.

## Βήμα 2 – Δημιουργία Παρουσίας OCR Engine (how to perform OCR)

Τώρα που η βιβλιοθήκη είναι έτοιμη, ξεκινήστε τη μηχανή. Σκεφτείτε τη μηχανή ως τον εγκέφαλο που θα κοιτάξει τα pixel και θα μαντέψει τα γράμματα.

```java
// Step 2: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

Η δημιουργία της μηχανής είναι συνήθως φθηνή· τα περισσότερα SDKs εκχωρούν εσωτερικές μνήμες αργά, έτσι μπορείτε με ασφάλεια να επαναχρησιμοποιήσετε την ίδια παρουσία για πολλές εικόνες αν επεξεργάζεστε μια παρτίδα.

## Βήμα 3 – Φόρτωση Εικόνας και Ορισμός Γλώσσας (extract text from image)

Το επόμενο βήμα είναι να δώσετε στη μηχανή κάτι να διαβάσει. Εδώ φορτώνουμε ένα JPEG από το δίσκο και λέμε στη μηχανή OCR ότι το κείμενο είναι στα Μογγολικά (κωδικός ISO 639‑2 “mon”). Μπορείτε να αλλάξετε τη διαδρομή ή τον κωδικό γλώσσας ώστε να ταιριάζει στην περίπτωση χρήσης σας.

```java
// Step 3: Load the image you want to recognize
ocrEngine.setImage(new OcrInputImage("YOUR_DIRECTORY/input.jpg"));

// Step 3b: Specify the language (e.g., English = "eng", Mongolian = "mon")
ocrEngine.getSettings().setLanguage("mon");
```

> **Σημείωση:** Αν δεν ορίσετε γλώσσα, η μηχανή προεπιλέγει τα Αγγλικά, κάτι που μπορεί να μειώσει δραστικά την ακρίβεια όταν το κείμενο είναι στην πραγματικότητα Κυριλλική ή άλλη γραφή. Πάντα καθορίζετε τη σωστή γλώσσα όταν μπορείτε.

## Βήμα 4 – Επεξεργασία Εικόνας και Λήψη Αποτελέσματος (convert image to text)

Με την εικόνα και τη γλώσσα στη θέση τους, ζητήστε από τη μηχανή να κάνει τη μαγεία της. Η κλήση `process()` τρέχει τον αλγόριθμο OCR και επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει τη αναγνωρισμένη συμβολοσειρά και τις βαθμολογίες εμπιστοσύνης.

```java
// Step 4: Process the image and obtain the recognition result
OcrResult ocrResult = ocrEngine.process();
```

Πίσω από τη σκηνή, η μηχανή μπορεί να εκτελεί προεπεξεργασία—ευθυγράμμιση, δυαδικοποίηση, μείωση θορύβου—ώστε να μην χρειάζεται να γράψετε αυτά τα βήματα μόνοι σας. Γι' αυτό οι περισσότερες σύγχρονες βιβλιοθήκες OCR είναι ευχάριστες στη χρήση για εργασίες **μετατροπής εικόνας σε κείμενο**.

## Βήμα 5 – Έξοδος του Εξαγόμενου Κειμένου (read text from jpg)

Τέλος, εξάγετε το απλό κείμενο από το αποτέλεσμα και κάντε κάτι χρήσιμο με αυτό. Για αυτήν τη demo απλώς το εκτυπώνουμε στην κονσόλα, αλλά θα μπορούσατε να το γράψετε σε αρχείο, να το τροφοδοτήσετε σε ευρετήριο αναζήτησης ή να το περάσετε σε άλλη υπηρεσία.

```java
// Step 5: Output the extracted text
System.out.println(ocrResult.getText());
```

Αυτή η γραμμή αποδεικνύει ότι έχετε διαβάσει επιτυχώς **κείμενο από jpg** (ή οποιαδήποτε υποστηριζόμενη μορφή). Αν η έξοδος φαίνεται ακατάληπτη, ελέγξτε ξανά τον κωδικό γλώσσας και την ποιότητα της εικόνας.

## Πλήρες Παράδειγμα Λειτουργίας (Όλα τα Βήματα Συνδυασμένα)

Παρακάτω είναι μια πλήρης, έτοιμη‑για‑εκτέλεση κλάση Java που ενώνει όλα τα κομμάτια. Αντιγράψτε την σε ένα αρχείο με όνομα `OcrDemo.java`, προσαρμόστε τη διαδρομή της εικόνας και τη γλώσσα, μετά τρέξτε `javac OcrDemo.java && java OcrDemo`.

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;

/**
 * Demonstrates how to perform OCR in Java using a generic OCR SDK.
 * This example loads a JPG, sets the language to Mongolian, and prints
 * the recognized text to the console.
 *
 * Replace the import package with the actual library you are using.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Validate command‑line arguments
        if (args.length < 2) {
            System.err.println("Usage: java OcrDemo <image-path> <language-code>");
            System.exit(1);
        }

        String imagePath = args[0];   // e.g., "input.jpg"
        String language = args[1];    // e.g., "mon" for Mongolian

        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image
        ocrEngine.setImage(new OcrInputImage(imagePath));

        // Step 3: Set the language (ISO‑639‑2)
        ocrEngine.getSettings().setLanguage(language);

        // Step 4: Run the recognition
        OcrResult result = ocrEngine.process();

        // Step 5: Print the extracted text
        System.out.println("=== Recognized Text ===");
        System.out.println(result.getText());
    }
}
```

### Αναμενόμενη Έξοδος

Αν το `input.jpg` περιέχει τη μογγολική φράση “Сайн байна уу?” η κονσόλα θα εμφανίσει:

```
=== Recognized Text ===
Сайн байна уу?
```

Αν η εικόνα είναι θολή ή ο κωδικός γλώσσας είναι λανθασμένος, θα δείτε ακατάληπτους χαρακτήρες ή μια κενή συμβολοσειρά—συνηθισμένα προβλήματα που θα συζητήσουμε παρακάτω.

## Συνηθισμένα Προβλήματα και Πώς να τα Διορθώσετε

| Σύμπτωμα | Πιθανή Αιτία | Διόρθωση |
|----------|--------------|----------|
| Ακατάληπτοι Κυριλλικοί χαρακτήρες | Λάθος κωδικός γλώσσας (προεπιλογή στα Αγγλικά) | Ορίστε `ocrEngine.getSettings().setLanguage("mon")` ή τον κατάλληλο κωδικό. |
| Καμία έξοδος καθόλου | Λανθασμένη διαδρομή εικόνας ή μη αναγνώσιμο αρχείο | Επαληθεύστε τη διαδρομή, βεβαιωθείτε ότι το αρχείο υπάρχει και ότι η διαδικασία έχει δικαιώματα ανάγνωσης. |
| Χαμηλή ακρίβεια (<70 %) | Η εικόνα έχει χαμηλή αντίθεση ή είναι περιστραμμένη | Προεπεξεργαστείτε την εικόνα: αυξήστε την αντίθεση, ευθυγραμμίστε ή μετατρέψτε σε κλίμακα του γκρι πριν τη δώσετε στη μηχανή. |
| `OutOfMemoryError` σε μεγάλα PDF | Φόρτωση πολλών σελίδων υψηλής ανάλυσης ταυτόχρονα | Επεξεργαστείτε τις σελίδες μία τη φορά ή μειώστε την ανάλυση των εικόνων πριν το OCR. |

### Συμβουλή Επαγγελματία: Επεξεργασία σε Παρτίδες

Αν χρειάζεστε **εξαγωγή κειμένου από εικόνα** αρχείων μαζικά, τυλίξτε τη βασική λογική σε έναν βρόχο:

```java
for (File img : new File("batchFolder").listFiles()) {
    ocrEngine.setImage(new OcrInputImage(img.getAbsolutePath()));
    OcrResult r = ocrEngine.process();
    System.out.println(r.getText());
}
```

## Περαιτέρω – Τι να Εξερευνήσετε Στη Σειρά;

- **Language Packs:** Τα περισσότερα OCR SDK επιτρέπουν τη λήψη πρόσθετων αρχείων δεδομένων γλώσσας. Η προσθήκη ενός νέου πακέτου σας επιτρέπει να **μετατρέψετε εικόνα σε κείμενο** για γλώσσες πέρα από τα Αγγλικά και τη Μογγολική.
- **PDF OCR:** Συνδυάστε αυτόν τον κώδικα με το Apache PDFBox για

## Τι Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε σε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή Κειμένου από Εικόνες – Βασικά OCR με Aspose.OCR για Java](/ocr/english/java/ocr-basics/)
- [Μετατροπή Εικόνας σε Κείμενο σε Java χρησιμοποιώντας Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Πώς να OCR Κείμενο Εικόνας με Γλώσσα Χρησιμοποιώντας Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}