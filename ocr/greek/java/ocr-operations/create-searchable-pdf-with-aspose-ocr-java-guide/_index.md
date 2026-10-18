---
category: general
date: 2026-03-26
description: Δημιουργήστε αναζητήσιμο PDF χρησιμοποιώντας το Aspose.OCR Java – μάθετε
  πώς να φορτώνετε εικόνα OCR, να ορίζετε την κύρια γλώσσα, να εξάγετε κείμενο από
  την εικόνα και να αποθηκεύετε το OCR PDF.
draft: false
keywords:
- create searchable pdf
- set primary language
- extract text from image
- load image ocr
- save ocr pdf
language: el
og_description: Δημιουργήστε αναζητήσιμο PDF με το Aspose.OCR Java. Οδηγός βήμα‑βήμα
  για τη φόρτωση εικόνας OCR, τον ορισμό της κύριας γλώσσας, την εξαγωγή κειμένου
  από την εικόνα και την αποθήκευση PDF OCR.
og_title: Δημιουργία Αναζητήσιμου PDF με το Aspose.OCR – Οδηγός Java
tags:
- Aspose.OCR
- Java
- PDF
- OCR
title: Δημιουργία Αναζητήσιμου PDF με το Aspose.OCR – Οδηγός Java
url: /el/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Αναζητήσιμου PDF με Aspose.OCR – Οδηγός Java

Έχετε ποτέ χρειαστεί να **create searchable pdf** από ένα σαρωμένο έγγραφο αλλά δεν ήξερατε από πού να ξεκινήσετε; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν ασχολούνται για πρώτη φορά με OCR σε Java. Τα καλά νέα είναι ότι το Aspose.OCR κάνει ολόκληρη τη διαδικασία—από τη φόρτωση μιας εικόνας μέχρι τον ορισμό της κύριας γλώσσας και τελικά την αποθήκευση ενός PDF με δυνατότητα OCR—πολύ απλή. Σε αυτό το tutorial θα περάσουμε από ένα πλήρες, εκτελέσιμο παράδειγμα που **extracts text from image**, σας επιτρέπει να **set primary language**, και τελειώνει με ένα **save OCR pdf** που μπορείτε να ανοίξετε σε οποιονδήποτε αναγνώστη.

Θα καλύψουμε επίσης μερικές πρακτικές συμβουλές, όπως η ενεργοποίηση της επιτάχυνσης GPU για ταχύτερη επεξεργασία και η διαχείριση εγγράφων μικτής γλώσσας (Tamil + English στην περίπτωσή μας). Στο τέλος θα έχετε ένα σταθερό, έτοιμο για παραγωγή snippet που μπορείτε να ενσωματώσετε στο έργο σας.

## Τι Θα Χρειαστείτε

- **Java 17** (ή οποιοδήποτε πρόσφατο JDK· το Aspose.OCR υποστηρίζει Java 8+)
- **Aspose.OCR for Java** library (κατεβάστε από την επίσημη ιστοσελίδα ή προσθέστε μέσω Maven)
- Ένα **license file** (ή τη δοκιμή 30 ημερών)
- Ένα αρχείο εικόνας που περιέχει κείμενο (η demo χρησιμοποιεί `sample-mixed-tamil-eng.jpg`)

Καμία επιπλέον πλαίσιο, χωρίς εγγενείς εξαρτήσεις—μόνο απλή Java και τα Aspose.JARs.

## Βήμα 1: Δημιουργία Αναζητήσιμου PDF – Ρύθμιση του Έργου

Πριν βουτήξουμε στον κώδικα, ας βεβαιωθούμε ότι το έργο είναι έτοιμο να **create searchable pdf** αρχεία.

```bash
# Maven dependency (add to pom.xml)
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check the latest version -->
</dependency>
```

> **Pro tip:** Κρατήστε τον αριθμό έκδοσης ενημερωμένο· οι νεότερες εκδόσεις συχνά περιλαμβάνουν διορθώσεις απόδοσης για τη χρήση GPU.

Τώρα δημιουργήστε μια απλή κλάση Java με όνομα `RecentFeaturesDemo`. Η κλάση θα περιέχει όλη τη λογική που χρειαζόμαστε για **load image OCR**, τη ρύθμιση των ρυθμίσεων γλώσσας και τελικά **save OCR pdf**.

## Βήμα 2: Φόρτωση Image OCR και Αρχικοποίηση της Μηχανής

Το πρώτο πραγματικό βήμα στη διαδικασία είναι να **load image OCR**. Αυτό ενημερώνει το Aspose.OCR ποιο αρχείο πρέπει να αναλύσει.

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // 2️⃣ Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Enable GPU acceleration – speeds up recognition dramatically
        ocrEngine.getEngineSettings().setUseGpu(true);
        // Use all available CPU cores for parallel processing
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);
```

> **Why this matters:** Η ενεργοποίηση του GPU (`setUseGpu(true)`) μπορεί να μειώσει τον χρόνο επεξεργασίας έως και 70 % σε σύγχρονο υλικό, ενώ η παράλληλη επεξεργασία εξασφαλίζει ότι η CPU δεν μένει αδρανής όταν το GPU είναι απασχολημένο.

## Βήμα 3: Ορισμός Πρωτεύουσας Γλώσσας (και Δευτερεύουσας)

Αν παραλείψετε αυτό το βήμα, το Aspose.OCR θα προσπαθήσει να μαντέψει τη γλώσσα, κάτι που είναι πιο αργό και λιγότερο ακριβές. Να πώς να **set primary language** στα Tamil και να προσθέσετε τα Αγγλικά ως εναλλακτική.

```java
        // 3️⃣ Define languages – primary is Tamil, secondary is English
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English);
```

> **Explanation:** Η πρωτεύουσα γλώσσα επηρεάζει το σύνολο χαρακτήρων και το λεξικό που χρησιμοποιείται κατά την αναγνώριση. Η προσθήκη δευτερεύουσας γλώσσας είναι κρίσιμη για έγγραφα μικτής γραφής (σκεφτείτε μια απόδειξη με κείμενο τόσο στα Tamil όσο και στα Αγγλικά).  

> **Edge case:** Αν το έγγραφό σας περιέχει περισσότερες από δύο γλώσσες, μπορείτε να καλέσετε `addAdditionalLanguage(...)` για κάθε επιπλέον.

## Βήμα 4: Προεπεξεργασία της Εικόνας – Διόρθωση Στροφής & Αφαίρεση Θορύβου

Οι σαρωμένες εικόνες συχνά υποφέρουν από περιστροφή ή θόρυβο φόντου. Η προεπεξεργασία βοηθά τη μηχανή OCR να **extract text from image** πιο αξιόπιστα.

```java
        // 4️⃣ Pre‑processing options
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // auto‑rotate tilted pages
                 .setDenoise(true); // suppress speckles and background patterns
```

> **Tip:** Αν γνωρίζετε ότι η εικόνα είναι ήδη καθαρή, μπορείτε να παραλείψετε το `setDenoise(true)` για να κερδίσετε μερικά χιλιοστά του δευτερολέπτου.

## Βήμα 5: Φόρτωση του Αρχείου Εικόνας

Τώρα που η μηχανή είναι έτοιμη, την κατευθύνουμε στο αρχείο που θέλουμε να αναλύσουμε.

```java
        // 5️⃣ Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

> **What if the path is wrong?** Το Aspose.OCR πετάει ένα σαφές `FileNotFoundException`. Τυλίξτε την κλήση σε try‑catch αν χρειάζεστε ευγενική διαχείριση σφαλμάτων.

## Βήμα 6: Εκτέλεση OCR και Εξαγωγή Κειμένου από Εικόνα

Με όλα ρυθμισμένα, ήρθε η ώρα να εκτελέσουμε την αναγνώριση. Αυτό το βήμα τόσο **extracts text from image** όσο και προετοιμάζει τα δεδομένα που χρειάζονται για τη δημιουργία PDF.

```java
        // 6️⃣ Perform recognition
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Print the raw OCR output – handy for debugging
            System.out.println("Recognized text:");
            System.out.println(recognizedText);
```

Η τυπική έξοδος κονσόλας για τη demo εικόνα είναι:

```
வணக்கம் World
This is a mixed language sample.
```

Θα παρατηρήσετε ότι η γραμμή στα Tamil εμφανίζεται σωστά, ακολουθούμενη από τα Αγγλικά. Αυτό είναι το αποτέλεσμα του σωστού **set primary language**.

## Βήμα 7: Αποθήκευση OCR PDF – Το Τελευταίο Κομμάτι

Το τελευταίο κομμάτι του παζλ είναι να **save OCR pdf**. Το Aspose.OCR μπορεί να ενσωματώσει ένα αόρατο στρώμα κειμένου πάνω στην αρχική εικόνα, καθιστώντας το PDF αναζητήσιμο.

```java
            // 7️⃣ (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

Ανοίξτε το `searchable.pdf` στο Adobe Reader, πατήστε **Ctrl + F**, και μπορείτε να αναζητήσετε τόσο λέξεις στα Tamil όσο και στα Αγγλικά—ακριβώς αυτό που υπόσχεται μια ροή εργασίας **create searchable pdf**.

## Πλήρες Παράδειγμα Εργασίας (Αντιγραφή‑Επικόλληση)

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να μεταγλωττίσετε και να εκτελέσετε όπως είναι. Αντικαταστήστε τις διαδρομές placeholder με τις δικές σας.

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // Step 2: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getEngineSettings().setUseGpu(true);                     // enable CUDA GPU acceleration
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);     // use multiple CPU cores
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);      // primary language
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English); // secondary language
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // correct image rotation
                 .setDenoise(true); // reduce background noise

        // Step 3: Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 4: Run OCR and obtain the plain‑text result
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Step 5: (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("Recognized text:");
            System.out.println(recognizedText);
            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

Τρέξτε το με:

```bash
javac -cp "path/to/aspose-ocr.jar" RecentFeaturesDemo.java
java -cp ".:path/to/aspose-ocr.jar" RecentFeaturesDemo
```

Θα πρέπει να δείτε το εξαγόμενο κείμενο να εκτυπώνεται στην κονσόλα, ακολουθούμενο από μια επιβεβαίωση ότι το **searchable pdf** γράφτηκε στο δίσκο.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν χρειαστεί να **load image OCR** από έναν πίνακα byte;

Μπορείτε να αντικαταστήσετε το `ImageStream.fromFile(imagePath)` με `ImageStream.fromBytes(byteArray)`. Αυτό είναι χρήσιμο όταν η εικόνα προέρχεται από βάση δεδομένων ή υπηρεσία web.

### Πώς να διαχειριστώ PDF που ήδη περιέχουν εικόνες;

Το Aspose.OCR μπορεί να δουλέψει απευθείας σε σελίδες PDF: `ocrEngine.setDocument(PdfDocument.fromFile("input.pdf"))`. Η μηχανή θα ραστεροποιήσει κάθε σελίδα εσωτερικά πριν από την αναγνώριση.

### Η GPU μου δεν εντοπίζεται—πρέπει να κρατήσω το `setUseGpu(true)`;

Αν το `setUseGpu(true)` αποτύχει, το Aspose.OCR επιστρέφει αυτόματα στην CPU. Μπορείτε να ελέγξετε το `ocrEngine.getEngineSettings().isGpuAvailable()` πριν το ενεργοποιήσετε.

### Μπορώ να **save OCR pdf** με προσαρμοσμένα μεταδεδομένα;

Ναι. Μετά την αναγνώριση, χρησιμοποιήστε `ocrEngine.getPdfSaveOptions().setTitle("My Document")` ή `setAuthor("John Doe")` πριν καλέσετε το `save`.

## Συμβουλές Απόδοσης για Μεγάλες Παρτίδες

- **Batch processing:** Επαναχρησιμοποιήστε την ίδια παρουσία `OcrEngine` σε πολλές εικόνες. Καλέστε μόνο `ocrEngine.clear()` μεταξύ των εκτελέσεων.
- **Thread pool:** Τυλίξτε κάθε εργασία εικόνας σε ένα `Callable` και υποβάλετε το σε ένα `ExecutorService`. Επειδή ενεργοποιήσαμε την παράλληλη επεξεργασία, κάθε νήμα θα ωφεληθεί από τη χρήση πολλαπλών πυρήνων.
- **Memory management:** Για εικόνες gig‑pixel, σκεφτείτε τη μείωση ανάλυσης με `ocrEngine.getPreprocessingSettings().setResizeFactor(0.5)` για να διατηρήσετε τη χρήση RAM σε λογικά επίπεδα.

## Συμπέρασμα

Μόλις περάσαμε από μια πλήρη ροή εργασίας **create searchable pdf** χρησιμοποιώντας το Aspose.OCR για Java. Ξεκινώντας από **load image OCR**, εμείς

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}