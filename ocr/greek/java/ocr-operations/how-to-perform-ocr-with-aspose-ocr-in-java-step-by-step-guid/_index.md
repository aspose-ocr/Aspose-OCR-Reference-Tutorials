---
category: general
date: 2026-07-15
description: Πώς να εκτελέσετε OCR σε Java και να εξάγετε κείμενο από εικόνα χρησιμοποιώντας
  το Aspose OCR. Μάθετε να αναγνωρίζετε κείμενο στα Χίντι, να εκτελείτε OCR σε εικόνα
  και να λαμβάνετε ακριβή αποτελέσματα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform ocr
- extract text from image
- recognize hindi text
- perform ocr on image
- run ocr recognition
language: el
lastmod: 2026-07-15
og_description: Η εκτέλεση OCR σε Java καθιστά την εξαγωγή κειμένου από εικόνα αβίαστη.
  Ακολουθήστε αυτόν τον οδηγό για να αναγνωρίσετε κείμενο στα Χίντι, να εκτελέσετε
  OCR σε εικόνα και να ενσωματώσετε τα αποτελέσματα αμέσως.
og_image_alt: Screenshot showing how to perform OCR on a Hindi image using Aspose
  OCR in Java
og_title: Πώς να εκτελέσετε OCR σε Java – Πλήρες σεμινάριο Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-07-15'
  description: How to perform OCR in Java and extract text from image using Aspose
    OCR. Learn to recognize Hindi text, run OCR on image and get accurate results.
  headline: How to Perform OCR with Aspose OCR in Java – Step‑by‑Step Guide
  type: TechArticle
- description: How to perform OCR in Java and extract text from image using Aspose
    OCR. Learn to recognize Hindi text, run OCR on image and get accurate results.
  name: How to Perform OCR with Aspose OCR in Java – Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '- Java 8 or newer installed on your machine. - Maven or Gradle for dependency
      management (we’ll show the Maven snippet). - An image file containing Hindi
      characters (e.g., `sample_hindi.png`). - Internet access the first time you
      run the code – Aspose OCR will fetch the language model automatically.'
  - name: Set the Local Path for OCR Resources and Download the Hindi Model
    text: Aspose OCR stores language packs and other assets on the local file system.
      By pointing the library to a folder of your choice you keep everything tidy,
      and the first call will download the Hindi model (`aspose-ocr-hindi-v1`) if
      it isn’t already present.
  - name: Create the OCR Engine and Configure Recognition Settings
    text: The `AsposeOCR` class does the heavy lifting. We also instantiate `RecognitionSettings`
      to tell the engine which language to look for. This is where the **recognize
      hindi text** directive lives.
  - name: Prepare the Input Image for OCR
    text: Aspose OCR works with an `OcrInput` object that can hold one or many images.
      For this tutorial we’ll stick to a single image, but the same code works for
      a batch.
  - name: Perform OCR Recognition and Capture the Results
    text: Now we call `recognize`. The method returns a list of `RecognitionResult`
      objects—one per page or image. Since we only passed a single image, we’ll read
      the first element.
  - name: Extract the Recognized Text from the Result
    text: The `RecognitionResult` object exposes `recognition_text`, which holds the
      plain string. Print it to the console, write it to a file, or feed it to another
      service—your call.
  - name: Wrap Everything in a Runnable Java Class
    text: Below is the full, self‑contained program that you can paste into `src/main/java/com/example/OcrDemo.java`.
      It includes all imports, a `main` method, and the steps above in logical order.
  type: HowTo
tags:
- OCR
- Java
- Aspose
- Image Processing
- Hindi
title: Πώς να εκτελέσετε OCR με το Aspose OCR σε Java – Οδηγός βήμα‑προς‑βήμα
url: /el/java/ocr-operations/how-to-perform-ocr-with-aspose-ocr-in-java-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εκτελέσετε OCR με το Aspose OCR σε Java – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να εκτελέσετε OCR** σε μια φωτογραφία που μόλις τραβήξατε με το τηλέφωνό σας; Ίσως χρειάζεται να εξάγετε προτάσεις στα Χίντι από μια σαρωμένη απόδειξη ή να ψηφιοποιήσετε ένα χειρόγραφο σημείωμα. Τα καλά νέα είναι ότι δεν χρειάζεται να γράψετε ένα νευρωνικό δίκτυο από το μηδέν. Με το Aspose OCR για Java μπορείτε **να εξάγετε κείμενο από εικόνα** σε λίγες μόνο γραμμές κώδικα.

Σε αυτό το tutorial θα περάσουμε από όλα όσα χρειάζεστε: τη ρύθμιση των πόρων OCR, τη διαμόρφωση της μηχανής για **αναγνώριση κειμένου στα Χίντι**, την εκτέλεση της αναγνώρισης και τέλος την εκτύπωση του αποτελέσματος. Στο τέλος θα μπορείτε να **εκτελείτε OCR σε εικόνες** και **να τρέχετε αναγνώριση OCR** αξιόπιστα σε οποιοδήποτε έργο Java.

## Τι Θα Μάθετε

- Πώς να κατεβάσετε και να αναφέρετε το μοντέλο γλώσσας Χίντι που απαιτείται για ακριβή αναγνώριση.  
- Πώς να διαμορφώσετε το `RecognitionSettings` ώστε η μηχανή να γνωρίζει ότι πρέπει να **εξάγει κείμενο από εικόνα** στα Χίντι.  
- Πώς να τροφοδοτήσετε μια μοναδική εικόνα (ή μια δέσμη) στη μηχανή OCR και να ανακτήσετε το αναγνωρισμένο κείμενο.  
- Συνηθισμένα προβλήματα όπως ελλιπείς πόροι, λανθασμένος τύπος εισόδου, και πώς να τα εντοπίσετε.  
- Ένα πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα Java που μπορείτε να αντιγράψετε‑και‑επικολλήσετε στο IDE σας.

### Προαπαιτούμενα

- Java 8 ή νεότερη εγκατεστημένη στο σύστημα σας.  
- Maven ή Gradle για διαχείριση εξαρτήσεων (θα δείξουμε το απόσπασμα Maven).  
- Ένα αρχείο εικόνας που περιέχει χαρακτήρες Χίντι (π.χ., `sample_hindi.png`).  
- Πρόσβαση στο Internet την πρώτη φορά που τρέχετε τον κώδικα – το Aspose OCR θα κατεβάσει αυτόματα το μοντέλο γλώσσας.

---

## Πώς να Εκτελέσετε OCR με το Aspose OCR σε Java

Αυτή η ενότητα είναι η καρδιά του tutorial. Θα χωρίσουμε τη διαδικασία σε έξι σαφή βήματα, το καθένα με μια σύντομη εξήγηση και ένα μπλοκ κώδικα που μπορείτε να εκτελέσετε αμέσως.

### Βήμα 1: Ορίστε τη Τοπική Διαδρομή για τους Πόρους OCR και Κατεβάστε το Μοντέλο Χίντι

Το Aspose OCR αποθηκεύει τα πακέτα γλωσσών και άλλα περιουσιακά στοιχεία στο τοπικό σύστημα αρχείων. Καθορίζοντας τη βιβλιοθήκη σε έναν φάκελο της επιλογής σας διατηρείτε όλα τακτοποιημένα, και η πρώτη κλήση θα κατεβάσει το μοντέλο Χίντι (`aspose-ocr-hindi-v1`) αν δεν υπάρχει ήδη.

```java
import com.aspose.ocr.Resources;

// Define where Aspose OCR will store its data
Resources.setLocalPath("aspose/ocr");

// Download the Hindi language pack (only once)
Resources.fetchResource("aspose-ocr-hindi-v1");
```

> **Συμβουλή:** Χρησιμοποιήστε έναν φάκελο που περιλαμβάνεται στο `.gitignore` του έργου σας ώστε να μην κάνετε κατά λάθος commit μεγάλων δυαδικών αρχείων.

### Βήμα 2: Δημιουργήστε τη Μηχανή OCR και Διαμορφώστε τις Ρυθμίσεις Αναγνώρισης

Η κλάση `AsposeOCR` κάνει τη βαριά δουλειά. Επίσης δημιουργούμε ένα αντικείμενο `RecognitionSettings` για να πούμε στη μηχανή ποια γλώσσα πρέπει να αναζητήσει. Εδώ βρίσκεται η οδηγία **recognize hindi text**.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.Language;

// Initialize the OCR engine
AsposeOCR ocrEngine = new AsposeOCR();

// Prepare recognition settings
RecognitionSettings settings = new RecognitionSettings();
settings.setLanguage(Language.Hin);          // Hindi language
settings.setDetectOrientation(true);        // Auto‑rotate if needed
settings.setRemoveNoise(true);              // Improves accuracy on noisy scans
```

> **Γιατί είναι σημαντικό:** Χωρίς την ρητή ρύθμιση της γλώσσας, η μηχανή προεπιλέγει τα Αγγλικά, κάτι που μειώνει δραστικά την ακρίβεια για τα σενάρια Devanagari.

### Βήμα 3: Προετοιμάστε την Εικόνα Εισόδου για OCR

Το Aspose OCR λειτουργεί με ένα αντικείμενο `OcrInput` που μπορεί να περιέχει μία ή πολλές εικόνες. Για αυτό το tutorial θα χρησιμοποιήσουμε μία μόνο εικόνα, αλλά ο ίδιος κώδικας λειτουργεί και για δέσμη.

```java
import com.aspose.ocr.OcrInput;
import com.aspose.ocr.InputType;

// Wrap your image file
OcrInput ocrInput = new OcrInput(InputType.SingleImage);
ocrInput.add("YOUR_DIRECTORY/sample_hindi.png");   // replace with your actual path
```

> **Ακραία περίπτωση:** Αν λάβετε ένα `ArrayIndexOutOfBoundsException`, ελέγξτε ξανά ότι η διαδρομή του αρχείου είναι σωστή και ότι η εικόνα είναι αναγνώσιμη (υποστηριζόμενες μορφές: PNG, JPEG, BMP, TIFF).

### Βήμα 4: Εκτελέστε Αναγνώριση OCR και Συλλέξτε τα Αποτελέσματα

Τώρα καλούμε το `recognize`. Η μέθοδος επιστρέφει μια λίστα από αντικείμενα `RecognitionResult` — ένα ανά σελίδα ή εικόνα. Εφόσον περάσαμε μόνο μία εικόνα, θα διαβάσουμε το πρώτο στοιχείο.

```java
import com.aspose.ocr.RecognitionResult;
import java.util.ArrayList;

// Run the OCR engine
ArrayList<RecognitionResult> results = ocrEngine.recognize(ocrInput, settings);
```

> **Τι γίνεται αν αποτύχει;**  
> - Βεβαιωθείτε ότι το μοντέλο Χίντι έχει κατέβει (ελέγξτε το φάκελο `aspose/ocr`).  
> - Επαληθεύστε ότι η εικόνα περιέχει καθαρούς, υψηλής αντίθεσης χαρακτήρες Χίντι.  
> - Ενεργοποιήστε το `settings.setDebugMode(true)` για λεπτομερείς καταγραφές.

### Βήμα 5: Εξάγετε το Αναγνωρισμένο Κείμενο από το Αποτέλεσμα

Το αντικείμενο `RecognitionResult` εκθέτει το `recognition_text`, το οποίο περιέχει το απλό κείμενο. Εκτυπώστε το στην κονσόλα, γράψτε το σε αρχείο ή δώστε το σε άλλη υπηρεσία — όπως προτιμάτε.

```java
// Grab the first (and only) result
RecognitionResult firstResult = results.get(0);

// Output the recognized Hindi text
System.out.println("Recognized Hindi text:");
System.out.println(firstResult.getRecognitionText());
```

**Αναμενόμενη έξοδος (παράδειγμα):**

```
Recognized Hindi text:
नमस्ते दुनिया! यह एक परीक्षण टेक्स्ट है।
```

Αν η έξοδος φαίνεται χαοτική, δοκιμάστε να αυξήσετε την ανάλυση της εικόνας ή να προεπεξεργαστείτε την εικόνα (δυαδικοποίηση, ρύθμιση αντίθεσης) πριν τη δώσετε στη μηχανή OCR.

### Βήμα 6: Συσκευάστε Όλα σε Μία Εκτελέσιμη Κλάση Java

Παρακάτω είναι το πλήρες, αυτόνομο πρόγραμμα που μπορείτε να επικολλήσετε στο `src/main/java/com/example/OcrDemo.java`. Περιλαμβάνει όλες τις εισαγωγές, μια μέθοδο `main` και τα παραπάνω βήματα με λογική σειρά.

```java
package com.example;

import com.aspose.ocr.*;
import java.util.ArrayList;

public class OcrDemo {
    public static void main(String[] args) {
        // 1️⃣ Set up resources and download Hindi model
        Resources.setLocalPath("aspose/ocr");
        Resources.fetchResource("aspose-ocr-hindi-v1");

        // 2️⃣ Initialize OCR engine and settings
        AsposeOCR ocrEngine = new AsposeOCR();
        RecognitionSettings settings = new RecognitionSettings();
        settings.setLanguage(Language.Hin);          // recognize Hindi text
        settings.setDetectOrientation(true);
        settings.setRemoveNoise(true);

        // 3️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput(InputType.SingleImage);
        // Replace with your actual image path
        ocrInput.add("YOUR_DIRECTORY/sample_hindi.png");

        // 4️⃣ Run OCR and get results
        ArrayList<RecognitionResult> results = ocrEngine.recognize(ocrInput, settings);

        // 5️⃣ Output the recognized string
        if (!results.isEmpty()) {
            RecognitionResult result = results.get(0);
            System.out.println("Recognized Hindi text:");
            System.out.println(result.getRecognitionText());
        } else {
            System.err.println("No text was recognized. Check the image and settings.");
        }
    }
}
```

**Εξάρτηση Maven** (προσθέστε στο `pom.xml` σας):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest version available -->
</dependency>
```

Τρέξτε το πρόγραμμα με `mvn compile exec:java -Dexec.mainClass="com.example.OcrDemo"` και παρακολουθήστε την κονσόλα να εκτυπώνει την πρόταση στα Χίντι.

---

## Συχνές Ερωτήσεις & Συμβουλές

| Question | Answer |
|----------|--------|
| **Μπορώ να εξάγω κείμενο από PDF αντί για εικόνα;** | Ναι. Μετατρέψτε κάθε σελίδα PDF σε εικόνα (π.χ., χρησιμοποιώντας Aspose PDF) και δώστε τις εικόνες στην ίδια διαδικασία OCR. |
| **Τι γίνεται αν χρειάζεται να επεξεργαστώ πολλές εικόνες ταυτόχρονα;** | Χρησιμοποιήστε `InputType.MultipleImages` και προσθέστε κάθε αρχείο στο `OcrInput`. Η μηχανή θα επιστρέψει μια λίστα αποτελεσμάτων με την ίδια σειρά. |
| **Υπάρχει τρόπος να λάβω βαθμούς εμπιστοσύνης;** | `RecognitionResult` παρέχει το `getConfidence()` για κάθε αναγνωρισμένη λέξη, χρήσιμο για μετα-επεξεργασία. |
| **Λειτουργεί το OCR offline μετά τη λήψη του μοντέλου;** | Απολύτως. Μόλις το μοντέλο Χίντι αποθηκευτεί στην cache στο `aspose/ocr`, δεν γίνονται περαιτέρω κλήσεις δικτύου. |
| **Πώς μπορώ να βελτιώσω την ακρίβεια σε σαρώσεις χαμηλής ποιότητας;** | Προεπεξεργαστείτε την εικόνα: αυξήστε το DPI σε ≥300, εφαρμόστε δυαδικοποίηση, και προαιρετικά χρησιμοποιήστε `settings.setDeskew(true)`. |

## Συμπέρασμα

Τώρα έχετε ένα ισχυρό, ολοκληρωμένο παράδειγμα του **πώς να εκτελέσετε OCR** σε μια εικόνα χρησιμοποιώντας το Aspose OCR σε Java. Διαμορφώνοντας τη μηχανή για **αναγνώριση κειμένου στα Χίντι**, μπορείτε αξιόπιστα **να εξάγετε κείμενο από εικόνα** και **να τρέχετε αναγνώριση OCR** σε οποιοδήποτε έγγραφο συναντήσετε.

Από εδώ ίσως θέλετε να:

- Δοκιμάστε άλλες γλώσσες αλλάζοντας το `settings.setLanguage(Language.Eng)` ή `Language.Fra`.  
- Ενσωματώστε το βήμα OCR σε μια μεγαλύτερη ροή εργασίας, όπως η αυτόματη αρχειοθέτηση τιμολογίων ή η ενημέρωση ενός ευρετηρίου αναζήτησης.  
- Εξερευνήστε προχωρημένα χαρακτηριστικά όπως το `settings.setTextOrientation(Orientation.Auto)` για σκύδρες σαρώσεις.

Δοκιμάστε το, προσαρμόστε τις ρυθμίσεις, και αφήστε τη μηχανή OCR να κάνει τη βαριά δουλειά για εσάς. Καλή προγραμματιστική!

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να κάνετε OCR Κειμένου Εικόνας με Γλώσσα χρησιμοποιώντας Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Πώς να εξάγετε κείμενο από εικόνα από URL χρησιμοποιώντας Aspose.OCR για Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)
- [αναγνώριση κειμένου εικόνας με Aspose OCR – Πλήρης Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}