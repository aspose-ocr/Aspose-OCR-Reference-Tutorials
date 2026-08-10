---
category: general
date: 2026-06-25
description: Η επιτάχυνση OCR με GPU στη Java σας επιτρέπει να αναγνωρίζετε κείμενο
  από εικόνα γρήγορα. Μάθετε να εξάγετε κείμενο από jpg, να ορίσετε όριο μνήμης GPU
  και να επεξεργάζεστε την εικόνα με OCR.
draft: false
keywords:
- ocr gpu acceleration
- recognize text from image
- extract text from jpg
- set gpu memory limit
- process image with OCR
language: el
og_description: Η επιτάχυνση OCR με GPU στη Java σας βοηθά να αναγνωρίζετε κείμενο
  από εικόνα γρήγορα. Ανακαλύψτε πώς να εξάγετε κείμενο από jpg, να ορίσετε όριο μνήμης
  GPU και να επεξεργαστείτε εικόνα με OCR.
og_title: Επιτάχυνση OCR με GPU στην Java – Πλήρης Οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: OCR GPU acceleration in Java lets you recognize text from image quickly.
    Learn to extract text from jpg, set GPU memory limit, and process image with OCR.
  headline: OCR GPU Acceleration in Java – Complete Programming Guide
  type: TechArticle
- description: OCR GPU acceleration in Java lets you recognize text from image quickly.
    Learn to extract text from jpg, set GPU memory limit, and process image with OCR.
  name: OCR GPU Acceleration in Java – Complete Programming Guide
  steps:
  - name: Point to the Image You Want to Process
    text: '```java // Step 1 – Specify the image file (can be a JPG, PNG, BMP, etc.)
      String imagePath = "YOUR_DIRECTORY/sample.jpg"; ```'
  - name: Build an OCR Configuration with GPU Support
    text: '```java // Step 2 – Create OCR configuration and turn on GPU acceleration
      OcrConfig ocrConfig = new OcrConfig() .setGpuSettings(new GpuSettings() .setEnabled(true)
      // <-- enable GPU usage .setDeviceId(0) // first GPU in the system .setMemoryLimitMb(4096));
      // optional: set GPU memory limit ```'
  - name: Instantiate the OCR Engine
    text: '```java // Step 3 – Create the OCR engine with the GPU‑enabled configuration
      AsposeOCR ocrEngine = new AsposeOCR(ocrConfig); ```'
  - name: Run the Recognition
    text: '```java // Step 4 – Perform text recognition on the chosen image ImageRecognitionResult
      result = ocrEngine.recognizeImage(imagePath); ```'
  - name: Output the Recognized Text
    text: '```java // Step 5 – Print the extracted text to the console System.out.println("Recognized
      text:

      " + result.getText()); ```'
  type: HowTo
tags:
- Java
- OCR
- GPU
title: Επιτάχυνση OCR με GPU στη Java – Πλήρης Οδηγός Προγραμματισμού
url: /el/java/advanced-ocr-techniques/ocr-gpu-acceleration-in-java-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Επιτάχυνση OCR GPU σε Java – Πλήρης Οδηγός Προγραμματισμού

Έχετε αναρωτηθεί ποτέ πώς η **ocr gpu acceleration** μπορεί να μειώσει κατά δευτερόλεπτα τη διαδικασία εξαγωγής κειμένου; Αν έχετε περάσει ώρες κάνοντας χειροκίνητη κύλιση σε σελίδες σαρωμένων PDF ή παλεύετε με αργό OCR μόνο CPU, δεν είστε μόνοι. Με λίγες γραμμές Java μπορείτε να **recognize text from image** σε ενα στιγμή, ακόμη και όταν τα αρχεία είναι βαριά JPG.

Σε αυτό το tutorial θα περάσουμε από ένα πραγματικό παράδειγμα που δείχνει πώς να **extract text from jpg**, να ρυθμίσετε ένα όριο μνήμης με **set gpu memory limit**, και τελικά να **process image with OCR** χρησιμοποιώντας το Java SDK της Aspose. Στο τέλος θα έχετε ένα πρόγραμμα έτοιμο για copy‑and‑paste που τρέχει σε οποιονδήποτε υπολογιστή με υποστηριζόμενο GPU.

## What You’ll Need

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

| Prerequisite | Why it matters |
|--------------|----------------|
| Java 17 (ή νεότερη) | Η βιβλιοθήκη Aspose OCR στοχεύει σε σύγχρονα JDK. |
| Maven ή Gradle | Για την προσθήκη της εξάρτησης `aspose-ocr`. |
| Ένα GPU συμβατό με CUDA (NVIDIA) με τουλάχιστον 4 GB VRAM | Ενεργοποιεί την **ocr gpu acceleration**· αλλιώς το SDK επιστρέφει σε CPU. |
| Ένα αρχείο εικόνας (`sample.jpg`) που θέλετε να διαβάσετε | Θα **extract text from jpg** στην επίδειξη. |

Αν λείπει κάποιο από αυτά, ο κώδικας θα τρέξει—αλλά περιμένετε πιο αργή απόδοση.

## OCR GPU Acceleration – Setting Up the Environment

Πρώτα απ’ όλα, προσθέστε τη βιβλιοθήκη Aspose OCR στο πρότζεκτ σας. Με Maven φαίνεται έτσι:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check for the latest version -->
</dependency>
```

> **Pro tip:** Κρατήστε τον αριθμό έκδοσης ενημερωμένο· οι νεότερες κυκλοφορίες συχνά φέρνουν καλύτερη υποστήριξη GPU και διορθώσεις σφαλμάτων.

Μόλις η εξάρτηση λυθεί, είστε έτοιμοι να ενεργοποιήσετε την **ocr gpu acceleration**.

## Recognize Text from Image Using Aspose OCR

Η καρδιά της λύσης βρίσκεται σε τέσσερα απλά βήματα. Ας τα αναλύσουμε.

### Step 1: Point to the Image You Want to Process

```java
// Step 1 – Specify the image file (can be a JPG, PNG, BMP, etc.)
String imagePath = "YOUR_DIRECTORY/sample.jpg";
```

> **Why?** Η μηχανή OCR χρειάζεται συγκεκριμένο μονοπάτι αρχείου· λειτουργούν και σχετικές διαδρομές, εφόσον η JVM μπορεί να βρει το αρχείο.

### Step 2: Build an OCR Configuration with GPU Support

```java
// Step 2 – Create OCR configuration and turn on GPU acceleration
OcrConfig ocrConfig = new OcrConfig()
        .setGpuSettings(new GpuSettings()
                .setEnabled(true)          // <-- enable GPU usage
                .setDeviceId(0)            // first GPU in the system
                .setMemoryLimitMb(4096));  // optional: set GPU memory limit
```

* `setEnabled(true)` είναι ο διακόπτης που λέει στην Aspose να χρησιμοποιήσει το GPU αντί για την CPU.  
* `setDeviceId(0)` επιλέγει το πρώτο GPU· αλλάξτε το δείκτη αν έχετε πολλαπλές κάρτες.  
* `setMemoryLimitMb(4096)` **set gpu memory limit** στα 4 GB, αποτρέποντας καταρρεύσεις μνήμης σε μεγάλες εικόνες. Προσαρμόστε αυτή την τιμή ανάλογα με το υλικό σας.

### Step 3: Instantiate the OCR Engine

```java
// Step 3 – Create the OCR engine with the GPU‑enabled configuration
AsposeOCR ocrEngine = new AsposeOCR(ocrConfig);
```

Τώρα η μηχανή ξέρει ότι πρέπει να κατευθύνει το βαριά φορτίο στο GPU, κάτι που μεταφράζεται σε πιο γρήγορους χρόνους αναγνώρισης—ιδιαίτερα για υψηλής ανάλυσης φωτογραφίες.

### Step 4: Run the Recognition

```java
// Step 4 – Perform text recognition on the chosen image
ImageRecognitionResult result = ocrEngine.recognizeImage(imagePath);
```

Πίσω από τη σκηνή το SDK στέλνει την εικόνα στο GPU, τρέχει ένα convolutional neural network, και επιστρέφει ένα αντικείμενο αποτελέσματος που περιέχει τη μεταγραφή σε απλό κείμενο.

### Step 5: Output the Recognized Text

```java
// Step 5 – Print the extracted text to the console
System.out.println("Recognized text:\n" + result.getText());
```

**Expected output** (truncated for brevity):

```
Recognized text:
Hello, world!
This is a sample image containing text.
```

Αν το GPU δεν είναι διαθέσιμο, η Aspose αυτόματα επιστρέφει σε λειτουργία CPU και εκτυπώνει μια προειδοποίηση—ώστε το πρόγραμμα σας ποτέ να μην καταρρεύσει.

## Extract Text from JPG – Handling File Paths

Όταν δουλεύετε με **extract text from jpg**, είναι συχνό να αντιμετωπίζετε προβλήματα κωδικοποίησης διαδρομών στα Windows. Μια ασφαλής προσέγγιση είναι η χρήση του `java.nio.file.Paths`:

```java
import java.nio.file.Paths;

// Convert a possibly relative path to an absolute one
String absolutePath = Paths.get(imagePath).toAbsolutePath().toString();
ImageRecognitionResult result = ocrEngine.recognizeImage(absolutePath);
```

Αυτή η μικρή αλλαγή εξαλείφει τις εκπλήξεις “file not found”, ειδικά όταν εκκινείτε το πρόγραμμα από IDE αντί για γραμμή εντολών.

## Set GPU Memory Limit for Stable Performance

Μπορεί να αναρωτιέστε γιατί χρησιμοποιούμε το `setMemoryLimitMb`. Τα σύγχρονα GPU κατανέμουν μνήμη κατά απαίτηση, και μια ασταθής εργασία OCR μπορεί εύκολα να καταναλώσει όλο το VRAM, προκαλώντας τερματισμό της διαδικασίας. Με το περιορισμό της κατανομής:

```java
.setMemoryLimitMb(2048) // limit to 2 GB if your GPU is modest
```

προστατεύετε το υπόλοιπο σύστημα από έλλειψη πόρων γραφικών. Αν το όριο είναι πολύ χαμηλό, το SDK θα μεταβεί αυτόματα στη RAM του συστήματος, η οποία είναι πιο αργή αλλά παραμένει λειτουργική.

> **Watch out for:** Ορισμός του ορίου χαμηλότερου από το απαιτούμενο buffer της εικόνας μπορεί να προκαλέσει `GpuMemoryException`. Σε αυτήν την περίπτωση, αυξήστε το όριο ή μειώστε την ανάλυση της εικόνας πριν το OCR.

## Process Image with OCR – Full End‑to‑End Example

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι μια πλήρης, έτοιμη για εκτέλεση κλάση:

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.config.GpuSettings;
import com.aspose.ocr.config.OcrConfig;
import com.aspose.ocr.ImageRecognitionResult;
import java.nio.file.Paths;

public class GpuExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Specify the image to be processed
        String imagePath = "YOUR_DIRECTORY/sample.jpg";

        // 2️⃣ Build OCR configuration with GPU acceleration enabled
        OcrConfig ocrConfig = new OcrConfig()
                .setGpuSettings(new GpuSettings()
                        .setEnabled(true)          // enable GPU usage
                        .setDeviceId(0)            // select the first GPU device
                        .setMemoryLimitMb(4096));  // optional memory limit

        // 3️⃣ Create the OCR engine using the configured settings
        AsposeOCR ocrEngine = new AsposeOCR(ocrConfig);

        // 4️⃣ Convert to absolute path (helps when extracting text from jpg)
        String absolutePath = Paths.get(imagePath).toAbsolutePath().toString();

        // 5️⃣ Perform text recognition on the image
        ImageRecognitionResult recognitionResult = ocrEngine.recognizeImage(absolutePath);

        // 6️⃣ Output the recognized text
        System.out.println("Recognized text:\n" + recognitionResult.getText());
    }
}
```

**Running the program**:

```bash
$ mvn compile exec:java -Dexec.mainClass=GpuExample
```

Θα πρέπει να δείτε την εκτύπωση του κειμένου που περιέχεται στο `sample.jpg`. Αν παρατηρήσετε ότι η διαδικασία διαρκεί περισσότερο από λίγα δευτερόλεπτα, ελέγξτε ότι οι οδηγοί GPU είναι ενημερωμένοι και ότι η σημαία `setGpuSettings().setEnabled(true)` εφαρμόζεται (το log θα περιέχει γραμμή όπως *“GPU acceleration enabled – device 0”*).

## Common Questions & Edge Cases

| Question | Answer |
|----------|--------|
| **What if I don’t have a GPU?** | Το SDK επιστρέφει ήρεμα σε λειτουργία CPU. Μπορείτε ακόμα να χρησιμοποιήσετε τον ίδιο κώδικα· απλώς θέστε `setEnabled(false)` ή παραλείψτε το μπλοκ `GpuSettings`. |
| **My image is 8 K resolution – will it still work?** | Ναι, αλλά ίσως χρειαστεί να αυξήσετε την τιμή `setMemoryLimitMb` ή να μειώσετε την ανάλυση της εικόνας για να αποφύγετε `GpuMemoryException`. |
| **Can I process a batch of images?** | Τυλίξτε την κλήση αναγνώρισης σε βρόχο. Η επαναχρησιμοποίηση του ίδιου αντικειμένου `AsposeOCR` είναι πιο αποδοτική επειδή το context του GPU παραμένει ενεργό. |
| **Is there a way to get confidence scores?** | Το `ImageRecognitionResult` εκθέτει `getConfidence()` για κάθε αναγνωρισμένο μπλοκ· μπορείτε να το καταγράψετε ή να φιλτράρετε τα χαμηλής εμπιστοσύνης αποτελέσματα. |
| **How do I switch to a different GPU device?** | Αλλάξτε το `setDeviceId(1)` (ή όποιο δείκτη ταιριάζει με τη δεύτερη κάρτα). Χρησιμοποιήστε το `nvidia-smi` για να δείτε τα IDs. |

## Tips for Production‑Ready Deployments

1. **Warm‑up the GPU** – Εκτελέστε μια μικρή ψεύτικη εικόνα μία φορά κατά την εκκίνηση· αυτό αποτρέπει την αρχική καθυστέρηση κλήσης.  
2. **Thread safety** – Το αντικείμενο `AsposeOCR` είναι thread‑safe μετά την αρχικοποίηση, οπότε μπορείτε να το μοιραστείτε μεταξύ πολλαπλών νημάτων.

## What Should You Learn Next?

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετα χαρακτηριστικά API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [αναγνώριση κειμένου εικόνας με Aspose OCR – Πλήρης Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Εξαγωγή κειμένου από εικόνα Java με Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Πώς να κάνετε OCR κειμένου εικόνας με γλώσσα χρησιμοποιώντας Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}