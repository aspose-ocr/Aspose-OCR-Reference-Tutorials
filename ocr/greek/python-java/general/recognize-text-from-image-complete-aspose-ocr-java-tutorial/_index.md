---
category: general
date: 2026-03-18
description: Μάθετε πώς να αναγνωρίζετε κείμενο από εικόνα και να εξάγετε κείμενο
  από JPEG με το Aspose OCR. Οδηγός βήμα‑προς‑βήμα για τη βελτίωση της ακρίβειας του
  OCR και τη φόρτωση εικόνας για OCR.
draft: false
keywords:
- recognize text from image
- extract text from jpeg
- improve OCR accuracy
- load image for OCR
language: el
og_description: Μάθετε να αναγνωρίζετε κείμενο από εικόνα με το Aspose OCR. Αυτό το
  σεμινάριο δείχνει πώς να εξάγετε κείμενο από JPEG, να βελτιώσετε την ακρίβεια του
  OCR και να φορτώσετε εικόνα για OCR σε Java.
og_title: αναγνώριση κειμένου από εικόνα – Οδηγός Aspose OCR Java
tags:
- Aspose OCR
- Java
- Image Processing
title: Αναγνώριση κειμένου από εικόνα – Πλήρης οδηγός Aspose OCR Java
url: /el/python-java/general/recognize-text-from-image-complete-aspose-ocr-java-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# αναγνώριση κειμένου από εικόνα – Πλήρες Μάθημα Aspose OCR Java

Κάποτε χρειάστηκε να **αναγνωρίσετε κείμενο από εικόνα** αλλά να κολλήσετε στο “πώς‑το‑κάνω‑πραγματικά” μέρος; Δεν είστε μόνοι. Σε πολλά έργα—όπως σάρωση τιμολογίων, επαλήθευση ταυτότητας ή απλώς εξαγωγή λεζάντων από φωτογραφίες—η αξιόπιστη εξαγωγή κειμένου από ένα JPEG μπορεί να φαίνεται σαν κυνήγι μονόκερου.  

Τα καλά νέα; Με το Aspose OCR for Java μπορείτε να **αναγνωρίσετε κείμενο από εικόνα** με μερικές μόνο γραμμές κώδικα, και θα μάθετε επίσης πώς να **εξάγετε κείμενο από jpeg**, **βελτιώσετε την ακρίβεια OCR**, και να **φορτώσετε εικόνα για OCR** σωστά. Στο τέλος αυτού του οδηγού θα έχετε ένα έτοιμο κομμάτι κώδικα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Maven ή Gradle.

## Τι Θα Χρειαστείτε

- **Java Development Kit (JDK) 8 ή νεότερο** – το API λειτουργεί με οποιοδήποτε πρόσφατο JDK.  
- **Aspose OCR for Java** JAR (ή η εξάρτηση Maven/Gradle).  
- Ένα έγκυρο **αρχείο άδειας Aspose OCR** (`Aspose.OCR.Java.lic`).  
- Ένα αρχείο εικόνας (JPEG, PNG, BMP…) που θέλετε να επεξεργαστείτε· θα το ονομάσουμε `input.jpg`.  

Καμία επιπλέον εγγενής βιβλιοθήκη, κανένα κλειδί cloud—απλώς καθαρή Java.

---

![αναγνώριση κειμένου από εικόνα χρησιμοποιώντας Aspose OCR](image.png)

*Alt text: αναγνώριση κειμένου από εικόνα χρησιμοποιώντας Aspose OCR*

## Βήμα 1 – Αναγνώριση Κειμένου από Εικόνα: Εφαρμογή της Άδειας Aspose OCR

Πριν η μηχανή OCR μπορέσει να κάνει οποιαδήποτε εργασία χρειάζεται μια άδεια· διαφορετικά θα παραμείνετε σε λειτουργία αξιολόγησης με υδατογραφήματα. Η εφαρμογή της άδειας είναι μια ενέργεια μίας φοράς ανά κύκλο ζωής της εφαρμογής.

```java
import com.aspose.ocr.License;

public class OcrSetup {
    public static void applyLicense() {
        try {
            License license = new License();
            // Point to the .lic file on your classpath or file system
            license.setLicense("Aspose.OCR.Java.lic");
            System.out.println("License applied successfully.");
        } catch (Exception e) {
            System.err.println("Failed to apply license: " + e.getMessage());
        }
    }
}
```

**Γιατί είναι σημαντικό:**  
Το αντικείμενο `License` ενημερώνει το Aspose ότι είστε πελάτης με πληρωμή, ξεκλειδώνοντας το πλήρες σύνολο λειτουργιών—συμπεριλαμβανομένης της AI‑βασισμένης προεπεξεργασίας που θα χρησιμοποιήσουμε αργότερα για **βελτίωση της ακρίβειας OCR**. Παραλείποντας αυτό το βήμα θα μπορείτε ακόμη **να αναγνωρίσετε κείμενο από εικόνα**, αλλά το αποτέλεσμα θα έχει υδατογραφήματα και θα είναι πιο αργό.

---

## Βήμα 2 – Φόρτωση Εικόνας για OCR (εξαγωγή κειμένου από jpeg)

Τώρα που η μηχανή έχει άδεια, πρέπει να της δώσουμε μια εικόνα. Εδώ μπαίνει η φράση **φορτώστε εικόνα για OCR**. Το Aspose μπορεί να διαβάσει οποιαδήποτε τυπική μορφή raster· θα το δείξουμε με JPEG επειδή είναι η πιο κοινή.

```java
import com.aspose.ocr.OcrEngine;

public class ImageLoader {
    public static OcrEngine createEngine(String imagePath) {
        OcrEngine engine = new OcrEngine();
        // This call both creates the engine and loads the image file
        engine.setImageFromFile(imagePath);
        System.out.println("Image loaded from: " + imagePath);
        return engine;
    }
}
```

**Συμβουλή:** Αν η εικόνα σας βρίσκεται μέσα σε JAR ή φάκελο resources, χρησιμοποιήστε `getResourceAsStream` και `engine.setImageFromStream(...)` αντί αυτού. Με αυτόν τον τρόπο μπορείτε **να εξάγετε κείμενο από jpeg** που είναι ενσωματωμένο στην εφαρμογή σας.

---

## Βήμα 3 – Αύξηση Ακρίβειας: Βελτίωση OCR Ακρίβειας με AI‑Βασισμένη Προεπεξεργασία

Οι ακατέργαστες σάρωση σπάνια είναι τέλειες—κλίση, σπασμένα pixel ή χαμηλή αντίθεση μπορούν να καταστρέψουν την αναγνώριση. Το Aspose OCR διαθέτει την κλάση `PreprocessingOptions` που εκτελεί φίλτρα AI πριν από το πραγματικό πέρασμα OCR. Η ρύθμιση αυτών των επιλογών είναι ο πιο γρήγορος τρόπος για **βελτίωση της ακρίβειας OCR** χωρίς να γράψετε κώδικα επεξεργασίας εικόνας.

```java
import com.aspose.ocr.PreprocessingOptions;

public class Preprocessor {
    public static void configure(OcrEngine engine) {
        PreprocessingOptions options = new PreprocessingOptions();
        options.setAutoDeskew(true);          // Aligns the image to 0°
        options.setDespeckle(true);          // Removes isolated noise
        options.setContrastBoost(1.3f);       // 30 % contrast boost
        engine.setPreprocessingOptions(options);
        System.out.println("Preprocessing configured: auto‑deskew, despeckle, contrast boost.");
    }
}
```

**Τι συμβαίνει στο παρασκήνιο;**  
- **Auto‑deskew** τρέχει ένα μικρό νευρωνικό δίκτυο που εντοπίζει τη βασική γραμμή κειμένου και περιστρέφει την εικόνα ανάλογα.  
- **Despeckle** εφαρμόζει ένα μέσο φίλτρο για να αφαιρέσει τυχαία pixel που εμφανίζονται συχνά σε σκαναρισμένα JPEG.  
- **Contrast boost** τεντώνει το ιστόγραμμα ώστε οι αδύναμοι χαρακτήρες να γίνουν πιο διακριτοί.

Μαζί, συνήθως αυξάνουν το ποσοστό αναγνώρισης από τα υψηλά 70% στα μεσαία 90% για καθαρές εγγράφους.

---

## Βήμα 4 – Ανάκτηση και Εκτύπωση του Αναγνωρισμένου Κειμένου

Το τελικό βήμα είναι η κλήση OCR και η εκτύπωση του αποτελέσματος. Η μέθοδος `recognize()` επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει το εξαγόμενο string και τις βαθμολογίες εμπιστοσύνης.

```java
import com.aspose.ocr.OcrResult;

public class Runner {
    public static void main(String[] args) {
        // 1️⃣ Apply license
        OcrSetup.applyLicense();

        // 2️⃣ Load the image (you can change the path to any JPEG you like)
        OcrEngine engine = ImageLoader.createEngine("YOUR_DIRECTORY/input.jpg");

        // 3️⃣ Optional: improve accuracy
        Preprocessor.configure(engine);

        // 4️⃣ Run OCR
        OcrResult result = engine.recognize();

        // 5️⃣ Output
        System.out.println("Recognised text:");
        System.out.println(result.getText());
    }
}
```

**Αναμενόμενο αποτέλεσμα** (υπόθεση ότι το `input.jpg` περιέχει τη φράση “Hello World!”):

```
Recognised text:
Hello World!
```

Αν η εικόνα είναι θορυβώδης, μπορεί να δείτε επιπλέον αλλαγές γραμμής ή λανθασμένους χαρακτήρες—προσαρμόστε τις επιλογές προεπεξεργασίας ή δοκιμάστε υψηλότερη τιμή `setContrastBoost` για περαιτέρω **βελτίωση της ακρίβειας OCR**.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν η εικόνα μου είναι PNG αντί για JPEG;

Κανένα πρόβλημα. Η ίδια κλήση `setImageFromFile` λειτουργεί για PNG, BMP, GIF ή TIFF. Απλώς αλλάξτε την επέκταση του αρχείου στη διαδρομή. Η φράση **εξάγετε κείμενο από jpeg** είναι μόνο παράδειγμα· το Aspose OCR είναι ανεξάρτητο μορφής.

### Πώς διαχειρίζομαι PDF πολλαπλών σελίδων;

Το Aspose OCR μπορεί επίσης να δεχτεί ροές PDF, αλλά θα χρειαστεί να μετατρέψετε κάθε σελίδα σε εικόνα πρώτα—συνήθως μέσω Aspose PDF ή τρίτης βιβλιοθήκης. Μόλις έχετε μια raster σελίδα, η ροή παραμένει η ίδια: **φορτώστε εικόνα για OCR**, προαιρετικά προεπεξεργαστείτε, μετά αναγνωρίστε.

### Λαμβάνω πολλά σύμβολα “?” στο αποτέλεσμα. Τι κάνω;

Αυτό συνήθως σημαίνει ότι η μηχανή δεν μπόρεσε να αντιστοιχίσει το μοτίβο pixel σε κανένα γνωστό γλύφο. Δοκιμάστε να αυξήσετε το contrast boost, ή ενεργοποιήστε `options.setBinarization(true)` για πιο επιθετική μετατροπή σε ασπρόμαυρο. Σε ακραίες περιπτώσεις, μια εικόνα υψηλότερης ανάλυσης (300 dpi ή περισσότερο) είναι η πιο αξιόπιστη λύση.

### Μπορώ να το τρέξω σε Android;

Ναι, το Aspose OCR διαθέτει JAR συμβατό με Android. Απλώς βεβαιωθείτε ότι το αρχείο άδειας βρίσκεται στο φάκελο `assets` και καλέστε `license.setLicense("Aspose.OCR.Android.lic")`. Το υπόλοιπο του κώδικα—**φορτώστε εικόνα για OCR**, **βελτίωση της ακρίβειας OCR**, **αναγνώριση κειμένου από εικόνα**—παραμένει το ίδιο.

---

## Συμπέρασμα

Τώρα έχετε ένα συμπαγές, ολοκληρωμένο παράδειγμα που δείχνει πώς να **αναγνωρίσετε κείμενο από εικόνα** χρησιμοποιώντας Aspose OCR for Java. Με την άδεια της μηχανής, τη σωστή **φόρτωση εικόνας για OCR**, την εφαρμογή AI‑βασισμένης προεπεξεργασίας, και τέλος την κλήση `recognize()`, μπορείτε αξιόπιστα να **εξάγετε κείμενο από jpeg** και άλλες μορφές raster ενώ **βελτιώνετε την ακρίβεια OCR** με λίγες μόνο γραμμές κώδικα.

Πειραματιστείτε: αλλάξτε τις σημαίες προεπεξεργασίας, αυξήστε το contrast boost, ή τροφοδοτήστε τη μηχανή με μια δέσμη εικόνων σε βρόχο. Το ίδιο μοτίβο λειτουργεί για PDFs, TIFFs και ακόμη και για στιγμιότυπα οθόνης σε κινητές συσκευές.  

Αν θέλετε τα επόμενα βήματα, εξετάστε:

- **Επεξεργασία δέσμης** με `OcrEngine` pools για σενάρια υψηλής απόδοσης.  
- **Πακέτα γλωσσών** για υποστήριξη κυριλλικών, αραβικών ή κινέζικων χαρακτήρων.  
- **Μετα-επεξεργασία** με κανονικές εκφράσεις για καθαρισμό κοινών σφαλμάτων OCR (π.χ., “0” vs “O”).

Καλό κώδικα, και οι OCR αποτελέσματά σας να είναι πάντα κρυστάλλινα καθαρά!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}