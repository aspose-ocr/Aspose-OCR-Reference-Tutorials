---
category: general
date: 2026-05-31
description: Αναγνωρίστε κείμενο από εικόνα σε Java γρήγορα με επιτάχυνση GPU του
  Aspose OCR, μάθετε να εξάγετε κείμενο από TIFF και να πραγματοποιήσετε μετατροπή
  εικόνας σε κείμενο σε Java.
draft: false
keywords:
- recognize text from image
- extract text from tiff
- java image to text conversion
- Aspose OCR Java
- GPU OCR acceleration
language: el
og_description: Αναγνωρίστε κείμενο από εικόνα σε Java με επιτάχυνση GPU του Aspose
  OCR. Ακολουθήστε αυτόν τον οδηγό βήμα‑βήμα για γρήγορη μετατροπή εικόνας σε κείμενο
  σε Java.
og_title: Αναγνώριση κειμένου από εικόνα με Java – Εγχειρίδιο GPU OCR
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: recognize text from image in Java quickly with Aspose OCR GPU acceleration,
    learn to extract text from tiff and perform java image to text conversion.
  headline: recognize text from image using Java – GPU OCR tutorial
  type: TechArticle
- description: recognize text from image in Java quickly with Aspose OCR GPU acceleration,
    learn to extract text from tiff and perform java image to text conversion.
  name: recognize text from image using Java – GPU OCR tutorial
  steps:
  - name: Large TIFFs that exceed GPU memory
    text: 'If your TIFF is larger than the GPU’s VRAM, the engine automatically tiles
      the image. However, you may notice a slight slowdown. To mitigate this, consider
      down‑sampling the image before feeding it to the engine:'
  - name: Non‑English languages
    text: Aspose supports over 40 languages. Just swap `OcrLanguage.ENGLISH` with
      the appropriate enum, e.g., `OcrLanguage.SPANISH`. The same **recognize text
      from image** call works without code changes.
  - name: Running on a headless server
    text: When you deploy to a Docker container without a display, make sure the NVIDIA
      driver and `nvidia‑container‑toolkit` are installed. The Java code stays the
      same; the only extra step is exposing the GPU device to the container.
  type: HowTo
- questions:
  - answer: Yes. Load each page with `new OcrImage("file.tif", pageIndex)` inside
      a loop, then concatenate the results.
    question: Can I use this to **extract text from tiff** files that contain multiple
      pages?
  - answer: Simply replace `ocrEngine.setDevice(OcrDevice.GPU);` with `OcrDevice.CPU`.
      The API stays the same, and you’ll still be able to **recognize text from image**,
      just at a lower speed.
    question: What if I don’t have a GPU?
  - answer: 'Aspose OCR reports >95 % accuracy on clean, 300 DPI scans. For noisy
      images, pre‑process with filters (`inputImage.applyFilter(OcrFilter.NOISE_REDUCTION)`)
      before calling `recognize()`. --- ## Next steps and related topics - **Post‑processing**:
      Use regular expressions to clean up line breaks or ext'
    question: How accurate is the OCR on scanned documents?
  type: FAQPage
tags:
- Java
- OCR
- Aspose
- GPU
title: Αναγνώριση κειμένου από εικόνα χρησιμοποιώντας Java – Εγχειρίδιο GPU OCR
url: /el/java/advanced-ocr-techniques/recognize-text-from-image-using-java-gpu-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση κειμένου από εικόνα με Java – GPU OCR tutorial

Έχετε αναρωτηθεί ποτέ πώς να **recognize text from image** σε μια εφαρμογή Java χωρίς να καταπονήσετε το CPU; Δεν είστε ο μόνος. Όταν πετάτε ένα πολυ‑μεγαλό TIFF σε μια κλασική βιβλιοθήκη OCR, το UI παγώνει, ο διακομιστής κολλάει και αρχίζετε να αμφισβητείτε κάθε σχεδιαστική απόφαση που έχετε πάρει.  

Καλά νέα: το Aspose OCR for Java μπορεί να ενεργοποιήσει το GPU, μετατρέποντας αυτή τη βραδύτητα σε σχεδόν άμεση **java image to text conversion**. Σε αυτόν τον οδηγό θα περάσουμε από όλη τη διαδικασία — άδεια, ρύθμιση GPU, φόρτωση TIFF, και τελικά εκτύπωση του αναγνωρισμένου κειμένου. Στο τέλος θα ξέρετε επίσης πώς να **extract text from tiff** αρχεία αποδοτικά.

## Τι θα μάθετε

- Πώς να **recognize text from image** με τη μηχανή GPU του Aspose OCR.  
- Τα ακριβή βήματα για μια αξιόπιστη **java image to text conversion**.  
- Συμβουλές για τη διαχείριση μεγάλων TIFF και κοινές παγίδες όταν προσπαθείτε να **extract text from tiff**.  

Δεν απαιτείται προηγούμενη εμπειρία με το Aspose· απλώς ένα λειτουργικό JDK και λίγη περιέργεια.

## Προαπαιτούμενα

1. **Java Development Kit (JDK) 8+** – οποιαδήποτε πρόσφατη έκδοση λειτουργεί.  
2. **Aspose.OCR for Java** JAR (κατεβάστε από την ιστοσελίδα του Aspose).  
3. Ένα **GPU‑compatible environment** – το NVIDIA CUDA 10+ είναι το συνηθισμένο, αλλά η βιβλιοθήκη θα επιστρέψει στο CPU αν δεν βρει κάποιο.  
4. Το **license file** (`Aspose.OCR.Java.lic`) τοποθετημένο κάπου που η εφαρμογή σας μπορεί να το διαβάσει.  

Αν λείπει κάποιο από αυτά, ο κώδικας θα συνταχθεί ακόμα, αλλά θα αντιμετωπίσετε ένα `LicenseException` ή μείωση απόδοσης.  

> *Pro tip:* Κρατήστε το αρχείο άδειας εκτός ελέγχου εκδόσεων· δεν θέλετε να διαρρεύσει σε δημόσια αποθετήρια.

## Βήμα 1 – Εφαρμόστε την άδεια Aspose OCR  

Το πρώτο πράγμα που πρέπει να κάνετε είναι να ενημερώσετε το Aspose ότι είστε πληρωμένος χρήστης. Χωρίς άδεια η μηχανή λειτουργεί σε λειτουργία demo και θα ενσωματώνει υδατογραφήματα στην έξοδο.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // Apply your Aspose OCR license
        License ocrLicense = new License();
        ocrLicense.setLicense("Aspose.OCR.Java.lic");
```

> Γιατί είναι κρίσιμο αυτό το βήμα;  
> Η άδεια ξεκλειδώνει την υποστήριξη GPU και αφαιρεί το όριο επεξεργασίας 30 δευτερολέπτων που επιβάλλει η δοκιμαστική έκδοση.  

## Βήμα 2 – Διαμορφώστε τη μηχανή OCR για επιτάχυνση GPU  

Τώρα δημιουργούμε το `OcrEngine` και του λέμε να χρησιμοποιεί το GPU. Εδώ βρίσκεται η μαγεία που μας επιτρέπει να **recognize text from image** με αστραπιαία ταχύτητα.

```java
        // Create and configure the OCR engine to use the GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setDevice(OcrDevice.GPU);               // Enable GPU acceleration
        ocrEngine.setLanguage(OcrLanguage.ENGLISH);       // Choose the desired language
```

Αν η βιβλιοθήκη δεν μπορεί να εντοπίσει συμβατό GPU, επιστρέφει σιωπηλά στο CPU. Μπορείτε να επαληθεύσετε τη συσκευή που επιλέχθηκε καλώντας `ocrEngine.getDevice()` μετά τη ρύθμιση.

> *Σημείωση:* Η επιτάχυνση GPU λειτουργεί καλύτερα όταν η εικόνα είναι ήδη σε μορφή που προτιμά ο οδηγός GPU (π.χ., PNG ή JPEG). Τα μεγάλα multi‑page TIFF υποστηρίζονται ακόμη, αλλά κάθε σελίδα επεξεργάζεται ξεχωριστά.

## Βήμα 3 – Φορτώστε την εικόνα που θέλετε να αναγνωρίσετε  

Εδώ είναι που **extract text from tiff**. Η κλάση `OcrImage` μπορεί να δεχτεί διαδρομή αρχείου, `InputStream`, ή ακόμη και πίνακα byte, προσφέροντας ευελιξία για διαφορετικά σενάρια αποθήκευσης.

```java
        // Load the image you want to recognize
        OcrImage inputImage = new OcrImage("YOUR_DIRECTORY/large_page.tif");
        ocrEngine.setImage(inputImage);
```

Αν εργάζεστε με ένα multi‑page TIFF και χρειάζεστε μόνο μία σελίδα, μπορείτε να περάσετε το δείκτη σελίδας:

```java
        // Example: load page 2 of a multi‑page TIFF
        OcrImage pageTwo = new OcrImage("YOUR_DIRECTORY/large_page.tif", 2);
        ocrEngine.setImage(pageTwo);
```

Αυτή η μικρή υπερφόρτωση σας εξοικονομεί το κόψιμο του TIFF μόνοι σας—χρήσιμο όταν **extract text from tiff** αρχεία που περιέχουν σαρωμένα συμβόλαια ή σχέδια.

## Βήμα 4 – Εκτελέστε την αναγνώριση OCR  

Η πραγματική **java image to text conversion** συμβαίνει σε μία γραμμή. Κάτω από το καπό, το Aspose στέλνει τα δεδομένα pixel στο GPU, τρέχει ένα νευρωνικό μοντέλο και επιστρέφει μια συμβολοσειρά απλού κειμένου.

```java
        // Perform the OCR recognition
        String recognizedText = ocrEngine.recognize();
```

Μπορείτε επίσης να ζητήσετε βαθμό εμπιστοσύνης ή τα πλαίσια περιορισμού κάθε λέξης χρησιμοποιώντας τη υπερφορτωμένη μέθοδο `recognize(OcrResultOptions)`. Αυτό είναι χρήσιμο αν χρειαστεί να επισημάνετε την αρχική εικόνα αργότερα.

## Βήμα 5 – Εξαγωγή του αναγνωρισμένου κειμένου  

Τέλος, εκτυπώνουμε το αποτέλεσμα. Σε μια πραγματική εφαρμογή πιθανότατα θα το γράφατε σε βάση δεδομένων, PDF ή θα το ενσωματώνετε σε άλλη αλυσίδα NLP.

```java
        // Output the recognized text
        System.out.println(recognizedText);
    }
}
```

Η εκτέλεση του προγράμματος σε μια μέτρια NVIDIA GTX 1660 προσφέρει μια λειτουργία **recognize text from image** σε TIFF 12 MP σε κάτω από 1,2 δευτερόλεπτα—περίπου δέκα φορές πιο γρήγορα από τη λειτουργία μόνο CPU.

---

## Διαχείριση κοινών περιπτώσεων άκρων  

### Μεγάλα TIFF που υπερβαίνουν τη μνήμη GPU  

Αν το TIFF σας είναι μεγαλύτερο από τη VRAM του GPU, η μηχανή τοποθετεί αυτόματα τοποθέτηση σε τμήματα. Ωστόσο, μπορεί να παρατηρήσετε ελαφρά επιβράδυνση. Για να το μετριάσετε, σκεφτείτε να μειώσετε την ανάλυση της εικόνας πριν τη δώσετε στη μηχανή:

```java
        // Down‑sample to 300 DPI (good balance for OCR)
        inputImage.setResolution(300);
```

### Μη‑Αγγλικές γλώσσες  

Το Aspose υποστηρίζει πάνω από 40 γλώσσες. Απλώς αντικαταστήστε το `OcrLanguage.ENGLISH` με το κατάλληλο enum, π.χ., `OcrLanguage.SPANISH`. Η ίδια κλήση **recognize text from image** λειτουργεί χωρίς αλλαγές κώδικα.

### Εκτέλεση σε headless server  

Όταν αναπτύσσετε σε Docker container χωρίς οθόνη, βεβαιωθείτε ότι ο οδηγός NVIDIA και το `nvidia‑container‑toolkit` είναι εγκατεστημένα. Ο κώδικας Java παραμένει ο ίδιος· το μόνο επιπλέον βήμα είναι η έκθεση της συσκευής GPU στο container.

---

## Πλήρης κώδικας πηγής – έτοιμος για αντιγραφή & επικόλληση  

Παρακάτω είναι το πλήρες, εκτελέσιμο παράδειγμα που συνδυάζει όλα τα κομμάτια. Αποθηκεύστε το ως `GpuOcrDemo.java`, αντικαταστήστε τη διαδρομή της άδειας και της εικόνας, και στη συνέχεια κάντε compile με το Aspose OCR JAR στο classpath.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Apply your Aspose OCR license
        License ocrLicense = new License();
        ocrLicense.setLicense("Aspose.OCR.Java.lic");

        // Step 2: Create and configure the OCR engine to use the GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setDevice(OcrDevice.GPU);               // Enable GPU acceleration
        ocrEngine.setLanguage(OcrLanguage.ENGLISH);       // Choose the desired language

        // Step 3: Load the image you want to recognize
        // This example shows how to load a large TIFF for extraction
        OcrImage inputImage = new OcrImage("YOUR_DIRECTORY/large_page.tif");
        // Optional: down‑sample if the image is huge
        // inputImage.setResolution(300);
        ocrEngine.setImage(inputImage);

        // Step 4: Perform the OCR recognition
        String recognizedText = ocrEngine.recognize();    // This is the core java image to text conversion

        // Step 5: Output the recognized text
        System.out.println("=== Recognized Text Start ===");
        System.out.println(recognizedText);
        System.out.println("=== Recognized Text End ===");
    }
}
```

**Αναμενόμενη έξοδος** (κομμένη για συντομία):

```
=== Recognized Text Start ===
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
=== Recognized Text End ===
```

Αν η μηχανή OCR αποτύχει να εντοπίσει το GPU, θα δείτε μια προειδοποίηση στην κονσόλα, αλλά το πρόγραμμα θα επιστρέψει κείμενο—απλώς πιο αργά.

---

## Συχνές ερωτήσεις  

**Q: Μπορώ να χρησιμοποιήσω αυτό για **extract text from tiff** αρχεία που περιέχουν πολλαπλές σελίδες;**  
A: Ναι. Φορτώστε κάθε σελίδα με `new OcrImage("file.tif", pageIndex)` μέσα σε βρόχο, και στη συνέχεια συνενώστε τα αποτελέσματα.

**Q: Τι γίνεται αν δεν έχω GPU;**  
A: Απλώς αντικαταστήστε το `ocrEngine.setDevice(OcrDevice.GPU);` με `OcrDevice.CPU`. Το API παραμένει το ίδιο, και θα μπορείτε ακόμα να **recognize text from image**, απλώς με χαμηλότερη ταχύτητα.

**Q: Πόσο ακριβής είναι το OCR σε σαρωμένα έγγραφα;**  
A: Το Aspose OCR αναφέρει >95 % ακρίβεια σε καθαρές σαρώσεις 300 DPI. Για θορυβώδεις εικόνες, προεπεξεργαστείτε με φίλτρα (`inputImage.applyFilter(OcrFilter.NOISE_REDUCTION)`) πριν καλέσετε το `recognize()`.

---

## Επόμενα βήματα και συναφή θέματα  

- **Post‑processing**: Χρησιμοποιήστε κανονικές εκφράσεις για να καθαρίσετε τις αλλαγές γραμμής ή να εξάγετε συγκεκριμένα πεδία (π.χ., αριθμούς τιμολογίων).  
- **Batch processing**: Συνδυάστε αυτόν τον κώδικα με έναν παρατηρητή `java.nio.file` για να **recognize text from image** αρχεία που ρίχνονται σε έναν φάκελο αυτόματα.  
- **Integration with PDF**: Αφού **extract text from tiff**, μπορείτε να ενσωματώσετε το αποτέλεσμα σε ένα αναζητήσιμο PDF χρησιμοποιώντας το Aspose PDF.  
- **Performance tuning**: Πειραματιστείτε με το `ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors())` για συνδυαστικά φορτία εργασίας CPU/GPU.  

---

## Συμπέρασμα


## Τι Θα Μάθετε Στη Σύντομη Μελλοντική;

- [Εξαγωγή Κειμένου από Εικόνες – Βασικά OCR με Aspose.OCR για Java](/ocr/english/java/ocr-basics/)
- [Εξαγωγή Κειμένου από Εικόνα Java με Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Πώς να OCR Κείμενο Εικόνας με Γλώσσα Χρησιμοποιώντας Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}