---
category: general
date: 2026-07-05
description: Συμπιέστε τις εικόνες PDF ενώ μετατρέπετε PNG σε PDF χρησιμοποιώντας
  Java. Μάθετε την προεπεξεργασία εικόνας για OCR, αναγνωρίστε κείμενο JPG και εκτελέστε
  ομαδικό OCR σε PDF σε ένα μόνο σεμινάριο.
draft: false
keywords:
- compress pdf images
- convert png to pdf
- image preprocessing for ocr
- recognize text jpg
- batch ocr to pdf
language: el
og_description: Συμπιέστε εικόνες PDF και μετατρέψτε PNG σε PDF χρησιμοποιώντας Java.
  Αυτός ο οδηγός καλύπτει την προεπεξεργασία εικόνας για OCR, την αναγνώριση κειμένου
  JPG και το μαζικό OCR σε PDF.
og_title: Συμπίεση εικόνων PDF με Java – Πλήρης οδηγός OCR παρτίδας
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  headline: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  type: TechArticle
- description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  name: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  steps:
  - name: Expected Output
    text: 'Running the program prints a line for each image, e.g.:'
  - name: What if my server has no GPU?
    text: Just set `gpuSettings.setEnabled(false)`. The rest of the pipeline remains
      unchanged, and you still get multithreaded CPU processing.
  - name: My PDFs are still too large—can I lower the quality further?
    text: Yes. Adjust `options.setImageQuality(70)` or even `50`. Lower values shrink
      size more aggressively but may blur fine glyphs. Test with a representative
      sample.
  - name: How do I handle other image formats (TIFF, BMP)?
    text: 'Add the extensions to the filter lambda:'
  - name: Can I keep the original color images instead of binarizing?
    text: Replace `.addBinarize()` with `.addGrayscale()` in the preprocessor builder
      if you need color retention for downstream analysis.
  type: HowTo
tags:
- ocr
- java
- pdf
- image-processing
title: Συμπίεση εικόνων PDF με Java – Οδηγός πλήρους παρτίδας OCR σε PDF
url: /el/java/advanced-ocr-techniques/compress-pdf-images-with-java-full-batch-ocr-to-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Συμπίεση Εικόνων PDF με Java – Οδηγός Πλήρους Batch OCR σε PDF

Έχετε ποτέ χρειαστεί να **συμπιέσετε εικόνες PDF** ενώ μετατρέπετε έναν φάκελο PNG σε αναζητήσιμα PDF; Δεν είστε μόνοι. Σε πολλά αυτοματοποιημένα pipelines το μεγαλύτερο πρόβλημα είναι η διαχείριση της ποιότητας της εικόνας, της ακρίβειας του OCR και του τελικού μεγέθους του PDF—όλα ταυτόχρονα.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από μια πρακτική λύση που **μετατρέπει PNG σε PDF**, εφαρμόζει **προεπεξεργασία εικόνας για OCR**, και τελικά **συμπιέζει εικόνες PDF** ώστε το αποτέλεσμα να παραμένει ελαφρύ. Στο τέλος θα ξέρετε πώς να **αναγνωρίζετε κείμενο JPG** αρχεία, να ρυθμίσετε μια ροή εργασίας **batch OCR σε PDF**, και να διατηρείτε τα PDF σας οργανωμένα.

## Τι Θα Μάθετε

- Ρύθμιση του Aspose OCR για Java και εφαρμογή άδειας.
- Διαμόρφωση της μηχανής για πολυνηματική εκτέλεση, επιτάχυνση GPU και διόρθωση ορθογραφίας.
- Δημιουργία επαναχρησιμοποιήσιμης **προεπεξεργασίας εικόνας για OCR** (αφαίρεση θορύβου, αντίθεση, δυαδικοποίηση).
- Χρήση του **PdfSaveOptions** για **συμπίεση εικόνων PDF** χωρίς να θυσιάζεται η αναγνωσιμότητα.
- Επανάληψη σε έναν φάκελο για **μετατροπή PNG σε PDF** και **αναγνώριση κειμένου JPG** μαζικά.
- Ένα πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα Java που μπορείτε να ενσωματώσετε σε οποιοδήποτε project.

> **Prerequisites**: Java 8+, Maven ή Gradle, άδεια Aspose OCR για Java, και ένας φάκελος με εικόνες PNG/JPG που θέλετε να επεξεργαστείτε.

---

## Βήμα 1: Εφαρμογή της Άδειας Aspose OCR (Απαραίτητο για Παραγωγή)

Πριν καλέσετε οποιοδήποτε OCR API πρέπει να φορτώσετε μια έγκυρη άδεια· διαφορετικά θα περιοριστείτε από τους περιορισμούς της δοκιμαστικής έκδοσης.

```java
import com.aspose.ocr.*;

public class LicenseSetup {
    public static void loadLicense() throws Exception {
        License license = new License();
        // Point to your license file – keep it out of source control!
        license.setLicense("Aspose.OCR.Java.lic");
    }
}
```

*Γιατί είναι σημαντικό*: Μια αδειοδοτημένη μηχανή ξεκλειδώνει την υποστήριξη GPU, υψηλότερη ακρίβεια και αφαιρεί τα υδατογραφήματα που διαφορετικά θα αυξάσουν το μέγεθος των PDF σας.

---

## Βήμα 2: Διαμόρφωση της Μηχανής OCR – Νήματα, GPU και Διόρθωση Ορθογραφίας

Μια γρήγορη μηχανή OCR είναι η ραχοκοκαλιά κάθε εργασίας **batch OCR σε PDF**. Θα δημιουργήσουμε όσες νήματα μπορεί να χειριστεί η CPU του κεντρικού υπολογιστή, θα ενεργοποιήσουμε την επιτάχυνση GPU (αν έχετε συμβατή κάρτα) και θα ενισχύσουμε τη διόρθωση ορθογραφίας για να καθαρίσουμε τα σφάλματα του OCR.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.gpu.GPUSettings;
import com.aspose.ocr.spell.SpellCorrectionOptions;

public class EngineConfig {
    public static OcrEngine createEngine() {
        OcrEngine ocrEngine = new OcrEngine();

        // Use all available logical processors
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Enable GPU – huge speedup for large batches
        GPUSettings gpu = new GPUSettings();
        gpu.setEnabled(true);
        ocrEngine.setGpuSettings(gpu);

        // Light spell correction: fix common typos without over‑correcting
        SpellCorrectionOptions spellOpts = new SpellCorrectionOptions();
        spellOpts.setMaxEditDistance(1);
        ocrEngine.getSpellCorrection().setOptions(spellOpts);

        return ocrEngine;
    }
}
```

*Pro tip*: Αν τρέχετε σε έναν headless server χωρίς GPU, απλώς ορίστε `gpu.setEnabled(false)` – ο κώδικας θα λειτουργεί κανονικά, μόνο λίγο πιο αργά.

---

## Βήμα 3: Δημιουργία Pipeline Προεπεξεργασίας Εικόνας

Οι ακατέργαστες σάρωση συχνά υποφέρουν από θόρυβο, χαμηλή αντίθεση ή άνιση φωτισμό. Η **προεπεξεργασία εικόνας για OCR** βελτιώνει δραστικά τα ποσοστά αναγνώρισης, ειδικά σε σενάρια **αναγνώριση κειμένου JPG**.

```java
import com.aspose.ocr.*;

public class PreprocessorSetup {
    public static ImagePreprocessor createPreprocessor() {
        return new ImagePreprocessor.Builder()
                .addDenoise(0.7)      // Reduce grain while preserving edges
                .addContrast(1.15)    // Boost contrast for clearer glyphs
                .addBinarize()        // Convert to black‑and‑white for OCR
                .build();
    }
}
```

*Γιατί αλυσσοδόνουμε αυτά*: Η αφαίρεση θορύβου πρώτα αποτρέπει τον δυαδικοποιητή από το να ενισχύσει τα σπαστά σημεία· η αντίθεση έπειτα εξασφαλίζει ότι οι χαρακτήρες ξεχωρίζουν· τέλος, η δυαδικοποίηση παρέχει στη μηχανή OCR μια καθαρή δυαδική εικόνα.

---

## Βήμα 4: Προετοιμασία Επιλογών Αποθήκευσης PDF – **Συμπίεση Εικόνων PDF** Αποτελεσματικά

Το Aspose σας επιτρέπει να ρυθμίσετε λεπτομερώς την έξοδο PDF. Θα ενεργοποιήσουμε τη συμπίεση εικόνας και θα ορίσουμε ένα επίπεδο ποιότητας που εξισορροπεί το μέγεθος και την ευκρίνεια.

```java
import com.aspose.ocr.pdf.PdfSaveOptions;

public class PdfOptions {
    public static PdfSaveOptions createOptions() {
        PdfSaveOptions options = new PdfSaveOptions();
        options.setCompressImages(true);   // This is the key to compress PDF images
        options.setImageQuality(90);       // 90% retains sharp text while shrinking file size
        return options;
    }
}
```

*Αποτέλεσμα*: Κάθε αναζητήσιμο PDF θα είναι αισθητά μικρότερο—ιδανικό για αρχειοθέτηση ή αποστολή μέσω email.

---

## Βήμα 5: Επεξεργασία του Φακέλου – **Μετατροπή PNG σε PDF** και **Αναγνώριση Κειμένου JPG** σε Έναν Βρόχο

Τώρα φέρνουμε όλα μαζί. Ο βρόχος διασχίζει έναν φάκελο εισόδου, εκτελεί OCR σε κάθε PNG ή JPG, και γράφει ένα αναζητήσιμο PDF σε έναν φάκελο εξόδου. Το όνομα του PDF αντικατοπτρίζει το όνομα της πηγαίας εικόνας.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.pdf.PdfSaveOptions;
import java.io.File;

public class BatchOcrTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license
        LicenseSetup.loadLicense();

        // 2️⃣ Engine & preprocessing
        OcrEngine ocrEngine = EngineConfig.createEngine();
        ocrEngine.setPreprocessor(PreprocessorSetup.createPreprocessor());

        // 3️⃣ PDF options (compress PDF images)
        PdfSaveOptions pdfOptions = PdfOptions.createOptions();

        // 4️⃣ Define input / output folders
        File inputFolder = new File("YOUR_DIRECTORY/input");
        File outputFolder = new File("YOUR_DIRECTORY/output");
        if (!outputFolder.exists()) outputFolder.mkdirs();

        // 5️⃣ Filter PNG & JPG files
        File[] imageFiles = inputFolder.listFiles((dir, name) ->
                name.toLowerCase().endsWith(".png") || name.toLowerCase().endsWith(".jpg"));

        if (imageFiles == null || imageFiles.length == 0) {
            System.out.println("No PNG or JPG files found in the input folder.");
            return;
        }

        // 6️⃣ Process each file
        for (File image : imageFiles) {
            // Recognize text – works for both PNG and JPG
            ocrEngine.recognizeImage(image.getAbsolutePath());

            // Build output PDF path (same base name)
            String pdfPath = outputFolder.getAbsolutePath() + File.separator +
                    image.getName().replaceAll("\\.(png|jpg)$", ".pdf");

            // Save as searchable PDF – this step also compresses images
            ocrEngine.saveAsSearchablePdf(pdfPath, pdfOptions);

            System.out.println("✅ Processed: " + image.getName() + " → " + pdfPath);
        }

        System.out.println("🎉 All files have been converted and compressed!");
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Η εκτέλεση του προγράμματος εκτυπώνει μια γραμμή για κάθε εικόνα, π.χ.:

```
✅ Processed: invoice1.png → /output/invoice1.pdf
✅ Processed: receipt23.jpg → /output/receipt23.pdf
🎉 All files have been converted and compressed!
```

Ανοίξτε οποιοδήποτε παραγόμενο PDF σε έναν προβολέα και θα δείτε επιλέξιμο, αναζητήσιμο κείμενο ενώ το μέγεθος του αρχείου είναι συνήθως **30‑50 % μικρότερο** από το μη‑συμπιεσμένο αντίστοιχο.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν ο διακομιστής μου δεν έχει GPU;
Απλώς ορίστε `gpuSettings.setEnabled(false)`. Το υπόλοιπο pipeline παραμένει αμετάβλητο και εξακολουθείτε να έχετε πολυνηματική επεξεργασία CPU.

### Τα PDF μου είναι ακόμα πολύ μεγάλα—μπορώ να μειώσω περαιτέρω την ποιότητα;
Ναι. Ρυθμίστε `options.setImageQuality(70)` ή ακόμη και `50`. Οι χαμηλότερες τιμές μειώνουν το μέγεθος πιο έντονα, αλλά μπορεί να θολώσουν λεπτές γλυφές. Δοκιμάστε με ένα αντιπροσωπευτικό δείγμα.

### Πώς να διαχειριστώ άλλες μορφές εικόνας (TIFF, BMP);
Προσθέστε τις επεκτάσεις στο λήμμα φίλτρου:

```java
name.toLowerCase().endsWith(".png") ||
name.toLowerCase().endsWith(".jpg") ||
name.toLowerCase().endsWith(".tif") ||
name.toLowerCase().endsWith(".bmp")
```

Το ίδιο pipeline προεπεξεργασίας λειτουργεί για τις περισσότερες μορφές raster.

### Μπορώ να διατηρήσω τις αρχικές χρωματιστές εικόνες αντί για δυαδικοποίηση;
Αντικαταστήστε το `.addBinarize()` με `.addGrayscale()` στον builder του προεπεξεργαστή αν χρειάζεστε διατήρηση χρώματος για επόμενες αναλύσεις.

---

## Pro Tips για Batch OCR Έτοιμο στην Παραγωγή

- **Διαχείριση μνήμης**: Επαναχρησιμοποιήστε ένα μόνο αντικείμενο `OcrEngine` (όπως δείχνει το παράδειγμα) για να αποφύγετε το κόστος δημιουργίας/καταστροφής αντικειμένων ανά εικόνα.
- **Διαχείριση σφαλμάτων**: Τυλίξτε το μπλοκ ανά αρχείο σε `try/catch` για να καταγράφετε αποτυχίες χωρίς να διακόπτετε ολόκληρο το batch.
- **Καταγραφή (Logging)**: Χρησιμοποιήστε ένα κατάλληλο πλαίσιο καταγραφής (SLF4J, Log4j) αντί για `System.out.println` για πιο κλιμακώσιμες λύσεις.
- **Παραλληλισμός**: Για τεράστιους φακέλους, σκεφτείτε την επεξεργασία υποφακέλων με parallel streams, αλλά παρακολουθείτε την ανταγωνιστικότητα του GPU.
- **Ασφάλεια**: Αποθηκεύστε το αρχείο άδειας εκτός του αποθετηρίου και προστατέψτε το με δικαιώματα συστήματος αρχείων.

---

## Συμπέρασμα

Δείξαμε πώς να **συμπιέσετε εικόνες PDF** ενώ εκτελείτε μια **batch OCR σε PDF** μετατροπή που **μετατρέπει PNG σε PDF**, **αναγνωρίζει κείμενο JPG**, και εφαρμόζει ένα ισχυρό pipeline **προεπεξεργασίας εικόνας για OCR**. Το πλήρες πρόγραμμα Java είναι αυτόνομο, τρέχει σε οποιοδήποτε σύγχρονο JDK και παράγει ελαφριά, αναζητήσιμα PDF έτοιμα για αρχειοθέτηση ή περαιτέρω ανάλυση.

Τι επόμενα; Πειραματιστείτε με διαφορετικές παραμέτρους προεπεξεργασίας, δοκιμάστε γλώσσες OCR πέρα από τα Αγγλικά, ή ενσωματώστε τη ροή εργασίας σε ένα microservice Spring Boot που παρακολουθεί έναν φάκελο και επεξεργάζεται αρχεία σε πραγματικό χρόνο. Οι βασικές έννοιες—φόρτωση άδειας, διαμόρφωση μηχανής, προεπεξεργασία, και συμπίεση PDF—παραμένουν ίδιες, προσφέροντάς σας μια σταθερή βάση για οποιοδήποτε OCR‑προσανατολισμένο έργο.

Έχετε ερωτήσεις ή θέλετε να μοιραστείτε τις δικές σας βελτιώσεις; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

![Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output](alt="Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output")


## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας projects.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}