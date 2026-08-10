---
category: general
date: 2026-06-28
description: Μάθετε ένα παράδειγμα Aspose OCR Java για την εξαγωγή κειμένου από εικόνες
  σε έργα Java και ορίστε το όριο μνήμης GPU για ταχύτερα αποτελέσματα.
draft: false
keywords:
- aspose ocr java example
- extract text from image java
- set gpu memory limit
- gpu accelerated OCR Java
- Aspose OCR licensing
language: el
og_description: Παράδειγμα Aspose OCR Java που δείχνει πώς να εξάγετε κείμενο από
  εικόνα με κώδικα Java, ορίζοντας το όριο μνήμης GPU για βέλτιστη απόδοση.
og_title: Παράδειγμα Aspose OCR Java – Γρήγορη Εξαγωγή Κειμένου με Επιτάχυνση GPU
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn an Aspose OCR Java example to extract text from image Java projects
    and set GPU memory limit for faster results.
  headline: Aspose OCR Java Example – Extract Text from Image with GPU
  type: TechArticle
tags:
- Aspose OCR
- Java
- GPU
title: Παράδειγμα Aspose OCR Java – Εξαγωγή κειμένου από εικόνα με GPU
url: /el/java/advanced-ocr-techniques/aspose-ocr-java-example-extract-text-from-image-with-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Παράδειγμα Aspose OCR Java – Εξαγωγή Κειμένου από Εικόνα με GPU

Έχετε αναρωτηθεί ποτέ πώς να **εξάγετε κείμενο από εικόνα Java** εφαρμογές χωρίς να καταπολεμάτε την CPU σας; Δεν είστε μόνοι. Σε πολλές πραγματικές περιπτώσεις—σκεφτείτε σάρωση αποδείξεων, επαλήθευση ταυτοτήτων ή μαζική αρχειοθέτηση εγγράφων—το στενό λαιμό είναι ο ίδιος ο κινητήρας OCR.  

Καλά νέα: αυτό το **Aspose OCR Java example** σας καθοδηγεί βήμα‑βήμα μέσα από ένα πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα που εκμεταλλεύεται την επιτάχυνση GPU και ακόμη δείχνει πώς να **ορίσετε όριο μνήμης GPU** ώστε ο διακομιστής σας να παραμένει ευχαριστημένος. Στο τέλος αυτού του οδηγού θα έχετε μια λειτουργική κλάση Java που διαβάζει ένα αρχείο εικόνας, εκτελεί OCR στην GPU και εκτυπώνει το αναγνωρισμένο κείμενο στην κονσόλα. Χωρίς ασαφείς αναφορές, μόνο συγκεκριμένος κώδικας και σαφείς εξηγήσεις.

Θα καλύψουμε τα πάντα, από την άδεια μέχρι τη λεπτομερή ρύθμιση της GPU, ώστε είτε είστε έμπειρος προγραμματιστής Java είτε μόλις βουτάτε στον χώρο της υπολογιστικής όρασης, να βρείτε αξία εδώ. Η μόνη προϋπόθεση είναι ένα περιβάλλον ανάπτυξης Java (JDK 8 ή νεότερο) και πρόσβαση σε GPU συμβατό με CUDA ή OpenCL.

---

## Προαπαιτούμενα

- **Java Development Kit (JDK) 8+** – μπορείτε να το κατεβάσετε από την Oracle ή να υιοθετήσετε το OpenJDK.  
- **Aspose.OCR for Java** library – αποκτήστε το JAR από την ιστοσελίδα Aspose ή το Maven Central.  
- **Ένα έγκυρο αρχείο άδειας Aspose OCR** (`Aspose.OCR.Java.lic`). Η δωρεάν δοκιμή λειτουργεί για δοκιμές, αλλά η άδεια αφαιρεί τα υδατογράμματα αξιολόγησης.  
- **GPU με υποστήριξη CUDA ή OpenCL** – η demo ανιχνεύει αυτόματα τη βέλτιστη λειτουργία, αλλά χρειάζονται οι οδηγοί εγκατεστημένοι.  
- **Μια εικόνα για δοκιμή** – ένα καθαρό PNG ή JPEG από απόδειξη, σήμα ή οποιοδήποτε τυπωμένο κείμενο.  

Αν κάποιο από αυτά σας φαίνεται άγνωστο, μην πανικοβληθείτε. Τα παρακάτω βήματα θα σας δείξουν ακριβείς συνδέσμους λήψης και πού να τοποθετήσετε τα αρχεία.

## Βήμα 1: Παράδειγμα Aspose OCR Java – Ρύθμιση του Έργου

Πρώτα, δημιουργήστε ένα νέο έργο Maven (ή έναν απλό φάκελο αν προτιμάτε το απλό `javac`). Προσθέστε την εξάρτηση Aspose OCR στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Use the latest version -->
</dependency>
```

> **Pro tip:** Το Maven θα κατεβάσει όλες τις μεταβιβαστικές εξαρτήσεις, συμπεριλαμβανομένων των βιβλιοθηκών υποστήριξης GPU, ώστε να μην χρειάζεται να ψάχνετε για επιπλέον JARs.

Τοποθετήστε το αρχείο `Aspose.OCR.Java.lic` στη ρίζα του έργου (ή σε οποιονδήποτε φάκελο θα αναφέρετε αργότερα). Το **aspose ocr java example** που χτίζουμε αναμένει η διαδρομή άδειας να είναι `"Aspose.OCR.Java.lic"`.

## Βήμα 2: Εφαρμογή της Άδειας Aspose OCR

Το βήμα της άδειας είναι κρίσιμο—χωρίς αυτήν, ο κινητήρας OCR λειτουργεί σε λειτουργία αξιολόγησης και προσθέτει υδατογράφημα στην έξοδο. Εδώ είναι ο ελάχιστος κώδικας που χρειάζεστε:

```java
import com.aspose.ocr.*;

public class LicenseUtil {
    public static void applyLicense() throws Exception {
        License license = new License();
        // Adjust the path if your license file lives elsewhere
        license.setLicense("Aspose.OCR.Java.lic");
        System.out.println("Aspose OCR license applied successfully.");
    }
}
```

Η εκτέλεση αυτού μία φορά στην αρχή της εφαρμογής σας εγγυάται ότι **όλες οι επόμενες κλήσεις OCR** είναι πλήρως αδειοδοτημένες.

## Βήμα 3: Διαμόρφωση Επιτάχυνσης GPU – Ορισμός Ορίου Μνήμης GPU

Τώρα έρχεται το διασκεδαστικό μέρος: να πείτε στην Aspose να χρησιμοποιήσει την GPU και προαιρετικά **να ορίσετε όριο μνήμης GPU**. Η βιβλιοθήκη παρέχει το `GpuEngineOptions`, το οποίο σας επιτρέπει να ενεργοποιήσετε τη λειτουργία GPU, να επιλέξετε συσκευή και να περιορίσετε τη χρήση μνήμης. Ο περιορισμός μνήμης είναι χρήσιμος σε κοινόχρηστους διακομιστές όπου δεν θέλετε η εργασία OCR να καταναλώσει όλη τη μνήμη της GPU.

```java
import com.aspose.ocr.gpu.*;

public class GpuConfig {
    public static GpuEngineOptions createOptions() {
        GpuEngineOptions gpuOptions = new GpuEngineOptions();
        gpuOptions.setEnableGpu(true);          // turn on GPU acceleration
        gpuOptions.setDeviceId(0);              // use the first GPU device
        gpuOptions.setMemoryLimitMb(2048);      // **set GPU memory limit** to 2 GB
        System.out.println("GPU options configured (memory limit = 2048 MB).");
        return gpuOptions;
    }
}
```

> **Why set a memory limit?** Αν οι εργασίες OCR περιλαμβάνουν πολύ μεγάλες εικόνες ή εκτελείτε πολλά ταυτόχρονα, η GPU μπορεί γρήγορα να εξαντλήσει τη VRAM, προκαλώντας καταρρεύσεις. Με τον περιορισμό της κατανομής, διατηρείτε τη διαδικασία εντός ασφαλών ορίων και επιτρέπετε σε άλλες εργασίες να συνυπάρχουν ήρεμα.

## Βήμα 4: Εξαγωγή Κειμένου από Εικόνα Java – Φόρτωση της Εικόνας

Με την άδεια και τις ρυθμίσεις GPU εκτός του δρόμου, μπορούμε τελικά να **εξάγουμε κείμενο από εικόνα Java**. Το παρακάτω απόσπασμα δημιουργεί ένα `OcrEngine` χρησιμοποιώντας τις επιλογές GPU, φορτώνει ένα αρχείο εικόνας και εκτελεί την αναγνώριση.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply the license
        LicenseUtil.applyLicense();

        // 2️⃣ Set up GPU options (including memory limit)
        GpuEngineOptions gpuOptions = GpuConfig.createOptions();

        // 3️⃣ Create the OCR engine with GPU acceleration
        OcrEngine ocrEngine = new OcrEngine(gpuOptions);

        // 4️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        // Replace the placeholder with your actual image path
        ocrInput.add("YOUR_DIRECTORY/receipt.png");

        // 5️⃣ Perform OCR recognition
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 6️⃣ Output the recognized text
        System.out.println("Recognized Text (GPU):");
        System.out.println(ocrResult.getText());
    }
}
```

**Key points** σε αυτό το **aspose ocr java example**:

- Το `OcrInput.add()` μπορεί να δεχτεί πολλαπλές εικόνες· η μηχανή θα τις επεξεργαστεί διαδοχικά.  
- Το `ocrResult.getText()` επιστρέφει μια συμβολοσειρά απλού κειμένου, διατηρώντας τις αλλαγές γραμμής αλλά όχι πληροφορίες διάταξης.  
- Ολόκληρη η αλυσίδα εκτελείται στην GPU, η οποία μπορεί να είναι **5‑10× πιο γρήγορη** από την επεξεργασία μόνο με CPU για εικόνες υψηλής ανάλυσης.

## Βήμα 5: Εκτέλεση της Επίδειξης και Επαλήθευση του Αποτελέσματος

Συγκεντρώστε και τρέξτε το πρόγραμμα:

```bash
mvn compile exec:java -Dexec.mainClass=GpuOcrDemo
```

Αν όλα είναι σωστά συνδεδεμένα, θα δείτε κάτι όπως:

```
Aspose OCR license applied successfully.
GPU options configured (memory limit = 2048 MB).
Recognized Text (GPU):
Item   Qty   Price
Apple   2    $1.20
Banana  5    $0.75
Total          $5.85
```

Το ακριβές κείμενο εξαρτάται από την εικόνα σας, αλλά το σημαντικό είναι ότι η κονσόλα εκτυπώνει **το αναγνωρισμένο κείμενο** χωρίς το υδατογράφημα “Evaluation version”. Αν αντιμετωπίσετε σφάλμα `CUDA driver not found`, ελέγξτε ξανά ότι οι οδηγοί GPU είναι ενημερωμένοι και ότι το toolkit CUDA βρίσκεται στη διαδρομή συστήματος.

## Συνηθισμένα Προβλήματα & Πώς να τα Αποφύγετε

| Σύμπτωμα | Πιθανή Αιτία | Διόρθωση |
|----------|--------------|----------|
| `OutOfMemoryError: CUDA out of memory` | Η μνήμη GPU εξαντλήθηκε | Μειώστε το `setMemoryLimitMb` (π.χ., 1024) ή επεξεργαστείτε μικρότερα τμήματα εικόνας. |
| `LicenseException` | Το αρχείο άδειας λείπει ή η διαδρομή είναι λανθασμένη | Βεβαιωθείτε ότι το `Aspose.OCR.Java.lic` είναι προσβάσιμο και η διαδρομή ταιριάζει. |
| Δεν επιστρέφεται κείμενο | Η εικόνα είναι πολύ θολή ή σε λάθος χρωματικό χώρο | Προεπεξεργαστείτε την εικόνα (αυξήστε την αντίθεση, μετατρέψτε σε γκρι) πριν τη δώσετε στο OCR. |
| Η GPU δεν χρησιμοποιείται | `setEnableGpu(false)` ή λείπουν οδηγοί | Επαληθεύστε ότι `gpuOptions.setEnableGpu(true)` και επανεγκαταστήστε τους οδηγούς GPU. |

## Επέκταση του Παραδείγματος

Τώρα που έχετε ένα σταθερό **aspose ocr java example**, ίσως θέλετε να:

- **Επεξεργαστείτε μαζικά έναν φάκελο** – κάντε βρόχο πάνω στα αρχεία και αποθηκεύστε τα αποτελέσματα σε βάση δεδομένων.  
- **Ανιχνεύσετε γλώσσα** – χρησιμοποιήστε `ocrEngine.setLanguage(OcrLanguage.English)` ή προσθέστε πολλαπλές γλώσσες.  
- **Εφαρμόσετε post‑processing** – καθαρίστε τη ακατέργαστη συμβολοσειρά με regex ή στείλτε την σε ορθογραφικό έλεγχο.  

Όλες αυτές οι επεκτάσεις επαναχρησιμοποιούν τον ίδιο κώδικα αδειοδότησης και ρύθμισης GPU, οπότε χρειάζεται μόνο να προσθέσετε τη λογική της επιχείρησής σας.

## Τελικές Σκέψεις

Μόλις είδατε ένα πλήρες **aspose ocr java example** που **εξάγει κείμενο από εικόνα Java** εφαρμογές ενώ **ορίζει όριο μνήμης GPU** για αξιόπιστη απόδοση. Οι βασικές ιδέες—να αδειοδοτείτε νωρίς, να ρυθμίζετε την GPU, να τροφοδοτείτε την εικόνα, να διαβάζετε το κείμενο—είναι επαναχρησιμοποιήσιμες σε αμέτρητα έργα, από σαρωτές αποδείξεων μέχρι αυτοματοποιημένα συστήματα εισαγωγής φορμών.

Από εδώ, πειραματιστείτε με διαφορετικές τιμές `GpuEngineOptions`, δοκιμάστε μεγαλύτερες εικόνες ή ενσωματώστε το βήμα OCR σε μικροϋπηρεσία Spring Boot. Ο ουρανός είναι το όριο, και χάρη στην επιτάχυνση GPU, το όριο είναι πολύ υψηλότερο από ό,τι ήταν παλιά.

Έχετε ερωτήσεις ή χρειάζεστε βοήθεια για τη ρύθμιση των μνημονικών παραμέτρων στο συγκεκριμένο υλικό σας; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

![Διάγραμμα παραδείγματος Aspose OCR Java που δείχνει τη ροή από είσοδο εικόνας → OCR με επιτάχυνση GPU → έξοδο κειμένου](https://example.com/images/aspose-ocr-java-example-diagram.png "διάγραμμα παραδείγματος aspose ocr java")

## Τι Θα Μάθετε Στη Σειρά;

Οι παρακάτω εκπαιδευτικές οδηγίες καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Ορίσετε Άδεια και να Επαληθεύσετε την Άδεια Aspose.OCR σε Java](/ocr/english/java/ocr-basics/set-license/)
- [Εξαγωγή Κειμένου από Εικόνα Java με Λειτουργία Ανίχνευσης Περιοχών Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Μετατροπή Εικόνας σε Κείμενο σε Java χρησιμοποιώντας Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}