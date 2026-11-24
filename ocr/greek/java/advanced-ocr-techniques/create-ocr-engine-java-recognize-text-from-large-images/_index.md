---
category: general
date: 2026-09-28
description: Μάθετε πώς να εξάγετε κείμενο από TIFF χρησιμοποιώντας Aspose OCR σε
  Java. Αυτό το βήμα‑βήμα tutorial σας δείχνει πώς να δημιουργήσετε μια OCR engine,
  να διαβάσετε μεγάλα αρχεία TIFF και να αναγνωρίζετε κείμενο αποδοτικά.
draft: false
keywords:
- extract text from tiff
- aspose ocr java tutorial
- read tiff file java
- large image ocr java
- ocr engine java
lastmod: 2026-09-28
og_description: Εξαγωγή κειμένου από TIFF χρησιμοποιώντας Aspose OCR σε Java. Ακολουθήστε
  αυτό το tutorial για να δημιουργήσετε μια OCR engine, να διαβάσετε μεγάλα αρχεία
  TIFF και να λάβετε ακριβή αποτελέσματα.
og_image_alt: Diagram showing OCR engine workflow for large TIFF files in Java
og_title: Εξαγωγή κειμένου από TIFF – Οδηγός Aspose OCR Java
schemas:
- author: Aspose
  dateModified: '2026-09-28'
  description: Learn how to extract text from TIFF using Aspose OCR in Java. This
    step‑by‑step tutorial shows you how to create an OCR engine, read large TIFF files,
    and recognize text efficiently.
  headline: Extract text from TIFF with Aspose OCR in Java
  type: TechArticle
- questions:
  - answer: Yes, provided you have a valid Aspose.OCR license. The library’s commercial
      license covers both development and production use.
    question: Can I use this solution in a commercial application?
  - answer: TIFF does not have a standard password mechanism, so the library treats
      it as a regular image. For encrypted containers (e.g., ZIP), decrypt before
      passing the stream to the engine.
    question: Does Aspose.OCR support password‑protected TIFF files?
  - answer: Aspose.OCR for Java supports JDK 8 through JDK 21, including both Java
      SE and OpenJDK distributions.
    question: Which Java versions are officially supported?
  - answer: 'Enable preprocessing: `ocrEngine.getConfiguration().setPreprocessOptions(PreprocessOptions.CONTRAST_ENHANCE);`
      This boosts OCR confidence on noisy images.'
    question: How can I improve accuracy on low‑contrast scans?
  - answer: The engine can handle images up to several gigabytes, limited only by
      available disk space for temporary tiles. Memory usage stays under 200 MB thanks
      to streaming.
    question: Is there a limit to the image size I can process?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: Εξαγωγή κειμένου από TIFF με Aspose OCR σε Java
url: /el/java/advanced-ocr-techniques/create-ocr-engine-java-recognize-text-from-large-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή κειμένου από TIFF με Aspose OCR σε Java  

Αν χρειάζεστε **εξαγωγή κειμένου από TIFF** αρχεία που έχουν μέγεθος δεκάδων ή εκατοντάδων megabytes, αυτό το tutorial σας παρέχει μια λύση έτοιμη για παραγωγή. Θα μάθετε πώς να δημιουργήσετε μια μηχανή OCR σε Java, να μεταφέρετε ένα τεράστιο TIFF μέσω `InputStream`, και να αποκτήσετε ακριβές κείμενο Unicode χωρίς να εξαντλήσετε τη μνήμη heap της JVM.

## Γρήγορες απαντήσεις
- **Ποια βιβλιοθήκη διαχειρίζεται το OCR μεγάλων TIFF;** Aspose.OCR for Java.  
- **Ελάχιστη έκδοση Java;** JDK 8 ή νεότερη.  
- **Χρειάζομαι άδεια;** Ναι, ένα έγκυρο αρχείο `.lic` ξεκλειδώνει την πλήρη ανάλυση tiling.  
- **Μπορώ να επεξεργαστώ πολυ‑σελίδες TIFF;** Απόλυτα – η μηχανή δημιουργεί tiles για κάθε σελίδα αυτόματα.  
- **Τυπικός χρόνος εκτέλεσης για εικόνα 50 MP;** Περίπου 12 δευτερόλεπτα σε τυπικό διακομιστή 4‑πυρήνων.

## Τι είναι η εξαγωγή κειμένου από TIFF;

**Η εξαγωγή κειμένου από TIFF** σημαίνει τη μετατροπή του οπτικού περιεχομένου μιας εικόνας TIFF σε αναζητήσιμους, επεξεργάσιμους χαρακτήρες Unicode χρησιμοποιώντας οπτική αναγνώριση χαρακτήρων (OCR). Αυτή η διαδικασία σας επιτρέπει να ευρετηριάσετε σαρωμένους χάρτες, να αυτοματοποιήσετε την εισαγωγή δεδομένων από σαρωμένες φόρμες, και να κάνετε μεγάλες αρχειακές εικόνες αναζητήσιμες χωρίς να πληκτρολογείτε χειροκίνητα το περιεχόμενό τους. Το αποτέλεσμα είναι απλό κείμενο που μπορεί να αποθηκευτεί, να ευρετηριαστεί ή να τροφοδοτηθεί σε επόμενες αναλυτικές pipelines.

## Γιατί να χρησιμοποιήσετε Aspose OCR για Java;

Το Aspose.OCR υποστηρίζει **πάνω από 50 μορφές εικόνας**, μπορεί να επεξεργαστεί **πολυ‑εκατοντάδες σελίδες TIFF** χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη, και παρέχει ενσωματωμένη ανίχνευση γλώσσας και αυτόματο tiling. Αυτά τα χαρακτηριστικά μειώνουν την κατανάλωση μνήμης έως και 90 % σε σύγκριση με απλές προσεγγίσεις `BufferedImage`, ενώ προσφέρουν υψηλή ακρίβεια σε θορυβώδεις ή χαμηλής αντίθεσης σκαναρίσματα. Η βιβλιοθήκη προσφέρει επίσης εύκολη ενσωμάτωση με άλλα προϊόντα Aspose για δημιουργία PDF ή μετατροπή εγγράφων.

## Προαπαιτούμενα
- Java Development Kit (JDK) 8 ή νεότερο.  
- Aspose.OCR for Java (τελευταία έκδοση μέχρι Φεβρουάριο 2026).  
- Ένα μεγάλο αρχείο TIFF που θέλετε να επεξεργαστείτε.  
- Ένα αρχείο άδειας Aspose.OCR (`Aspose.OCR.lic`).  

> **Συμβουλή:** Τοποθετήστε το αρχείο TIFF στον ίδιο φάκελο με τον πηγαίο κώδικά σας ή αναφέρετέ το με απόλυτη διαδρομή· η μηχανή θα διαχειριστεί το tiling εσωτερικά, έτσι δεν χρειάζεται να χωρίσετε την εικόνα εσείς.

![Διάγραμμα ροής δημιουργίας μηχανής OCR Java](ocr-workflow.png){alt="Διάγραμμα ροής δημιουργίας μηχανής OCR Java"}  
[Διάγραμμα ροής δημιουργίας μηχανής OCR Java](ocr-workflow.png)

## Πώς να εξάγετε κείμενο από TIFF σε Java;

Φορτώστε το TIFF σας με ένα `InputStream`, εφαρμόστε την άδεια, δημιουργήστε τη μηχανή OCR, και καλέστε `recognize`. Η μηχανή θα δημιουργήσει tiles για την εικόνα, θα τρέξει το νευρωνικό μοντέλο σε κάθε tile, και θα ενώσει τα αποτελέσματα, παρέχοντας το τελικό κείμενο σε μία κλήση. Αυτή η προσέγγιση αποφεύγει τη φόρτωση ολόκληρης της εικόνας στη μνήμη, καθιστώντας την κατάλληλη για αρχεία gigapixel ενώ διατηρεί την χρήση CPU προβλέψιμη.

### Βήμα 1 – εφαρμόστε την άδεια Aspose.OCR (δημιουργία μηχανής OCR Java)

Η κλάση `License` ενημερώνει τη μηχανή OCR να ξεκλειδώσει τον αλγόριθμο πλήρους ανάλυσης tiling, ο οποίος είναι απαραίτητος για την αποδοτική επεξεργασία μιας **μεγάλης εικόνας**.

```java
import com.aspose.ocr.*;

public class LicenseHelper {
    /** Loads the Aspose.OCR license from the given path. */
    public static void applyLicense(String licensePath) throws Exception {
        License license = new License();
        license.setLicense(licensePath);   // throws if the file is missing or invalid
    }
}
```  

*Γιατί είναι σημαντικό:* Χωρίς άδεια η μηχανή λειτουργεί σε λειτουργία αξιολόγησης, περιορίζοντας τις σελίδες και προσθέτοντας υδατογράφημα στο αποτέλεσμα.

### Βήμα 2 – δημιουργήστε τη μηχανή OCR (δημιουργία μηχανής OCR Java)

`OcrEngine` είναι το βασικό αντικείμενο που εκτελεί τη μετατροπή pixel‑to‑text.

```java
/** Returns a fresh OcrEngine ready for recognition. */
public static OcrEngine buildEngine() {
    // No special configuration needed for basic text extraction.
    // You can tweak language, DPI, or preprocessing here if required.
    return new OcrEngine();
}
```  

*Γιατί το κρατάμε απλό:* Οι προεπιλεγμένες ρυθμίσεις περιλαμβάνουν ήδη αυτόματη ανίχνευση γλώσσας και βέλτιστο tiling. Η υπερβολική διαμόρφωση μπορεί στην πραγματικότητα να επιβραδύνει την επεξεργασία μεγάλων αρχείων.

### Βήμα 3 – φορτώστε το αρχείο TIFF χρησιμοποιώντας ένα `InputStream` (ανάγνωση αρχείου TIFF Java)

Η ροή του αρχείου αποτρέπει τη JVM από το να εκχωρήσει μια τεράστια `BufferedImage`. Το Aspose.OCR διαβάζει και δημιουργεί tiles για την εικόνα εν κινήσει.

```java
import java.io.*;

public static InputStream openTiff(String filePath) throws FileNotFoundException {
    // Using try‑with‑resources later guarantees the stream is closed.
    return new FileInputStream(filePath);
}
```  

*Ακραία περίπτωση:* Εάν το TIFF σας χρησιμοποιεί συμπίεση CCITT Group 4, μπορείτε προαιρετικά να ορίσετε `ocrEngine.getConfiguration().setTiffCompression(TiffCompression.CCITT4)` για μια μικρή αύξηση ταχύτητας.

### Βήμα 4 – προετοιμάστε την είσοδο OCR και δώστε υπόδειξη της μορφής

`OcrInput` μπορεί να περιέχει πολλαπλές εικόνες, αλλά χρειαζόμαστε μόνο μία για αυτήν τη demo. Η παροχή της συμβολοσειράς μορφής (`"tif"`) παρακάμπτει το δαπανηρό sniffing μορφής.

```java
import com.aspose.ocr.*;

public static OcrInput buildInput(InputStream imageStream) throws Exception {
    OcrInput input = new OcrInput();
    input.add(imageStream, "tif");   // second argument is the optional file extension hint
    return input;
}
```  

*Γιατί η υπόδειξη είναι χρήσιμη:* Όταν δουλεύετε με **μεγάλες εικόνες**, κάθε χιλιοστό του δευτερολέπτου μετράει. Η υπόδειξη μορφής λέει στον parser να παρακάμψει την δαπανηρή ανάλυση κεφαλίδας.

### Βήμα 5 – αναγνωρίστε κείμενο από τη μεγάλη εικόνα (αναγνώριση κειμένου από μεγάλη εικόνα)

Η κλήση OCR επιστρέφει ένα `OcrResult` που περιέχει απλό κείμενο, βαθμούς εμπιστοσύνης, και προαιρετικά πλαίσια οριοθέτησης.

```java
public static OcrResult runRecognition(OcrEngine engine, OcrInput input) throws Exception {
    // The recognize method performs tiling internally, so memory usage stays low.
    return engine.recognize(input);
}
```  

*Τι συμβαίνει στο παρασκήνιο:* Το Aspose.OCR χωρίζει το TIFF σε tiles 1024 × 1024 px, τρέχει το νευρωνικό μοντέλο σε κάθε tile, και ενώσει τα αποτελέσματα. Αυτός είναι ο λόγος που μπορείτε να **αναγνωρίσετε κείμενο από μεγάλες εικόνες** χωρίς χειροκίνητη προεπεξεργασία.

### Βήμα 6 – εμφανίστε προεπισκόπηση του εξαγόμενου κειμένου

Η εκτύπωση ολόκληρου του εγγράφου μπορεί να κατακλύσει την κονσόλα. Η εμφάνιση των πρώτων 200 χαρακτήρων σας επιτρέπει να επαληθεύσετε το αποτέλεσμα γρήγορα.

```java
public static void printPreview(OcrResult result) {
    String text = result.getText();
    if (text.length() > 200) {
        System.out.println(text.substring(0, 200) + "…");
    } else {
        System.out.println(text);
    }
}
```  

**Αναμενόμενη έξοδος κονσόλας:**  

```
The quick brown fox jumps over the lazy dog. This map shows the historic...
```  

Αν δείτε ακατανόητο κείμενο, ελέγξτε ξανά ότι η σωστή γλώσσα είναι επιλεγμένη (η προεπιλογή είναι Αγγλικά) και ότι το TIFF δεν είναι κατεστραμμένο.

## Πλήρες λειτουργικό παράδειγμα

Συνδυάζοντας όλα τα κομμάτια παίρνετε μια μοναδική κλάση που μπορείτε να μεταγλωττίσετε και να εκτελέσετε:

```java
import com.aspose.ocr.*;
import java.io.*;

public class LargeImageDemo {

    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Apply your Aspose.OCR license (Create OCR Engine Java)
        // -------------------------------------------------
        LicenseHelper.applyLicense("Aspose.OCR.lic");

        // -------------------------------------------------
        // 2️⃣ Build the OCR engine (Create OCR Engine Java)
        // -------------------------------------------------
        OcrEngine ocrEngine = buildEngine();

        // -------------------------------------------------
        // 3️⃣ Open the huge TIFF (Read TIFF File Java)
        // -------------------------------------------------
        try (InputStream imageStream = openTiff("YOUR_DIRECTORY/huge-map.tif")) {

            // -------------------------------------------------
            // 4️⃣ Prepare OCR input, hint the format
            // -------------------------------------------------
            OcrInput ocrInput = buildInput(imageStream);

            // -------------------------------------------------
            // 5️⃣ Recognize text from large image (Recognize Text from Large Image)
            // -------------------------------------------------
            OcrResult ocrResult = runRecognition(ocrEngine, ocrInput);

            // -------------------------------------------------
            // 6️⃣ Show a preview of the extracted text
            // -------------------------------------------------
            printPreview(ocrResult);
        }
    }

    // Helper methods from previous sections ------------------------------------
    public static void applyLicense(String path) throws Exception {
        License lic = new License();
        lic.setLicense(path);
    }

    public static OcrEngine buildEngine() {
        return new OcrEngine();
    }

    public static InputStream openTiff(String filePath) throws FileNotFoundException {
        return new FileInputStream(filePath);
    }

    public static OcrInput buildInput(InputStream stream) throws Exception {
        OcrInput input = new OcrInput();
        input.add(stream, "tif");
        return input;
    }

    public static OcrResult runRecognition(OcrEngine engine, OcrInput input) throws Exception {
        return engine.recognize(input);
    }

    public static void printPreview(OcrResult result) {
        String txt = result.getText();
        System.out.println(txt.length() > 200 ? txt.substring(0, 200) + "…" : txt);
    }
}
```  

Μεταγλώττιση με:  

```bash
javac -cp "aspose-ocr-23.12.jar" LargeImageDemo.java
java -cp ".:aspose-ocr-23.12.jar" LargeImageDemo
```  

Αντικαταστήστε το `aspose-ocr-23.12.jar` με την πραγματική έκδοση που κατεβάσατε.

## Συχνά προβλήματα & συμβουλές  

| Πρόβλημα | Γιατί συμβαίνει | Γρήγορη διόρθωση |
|------|----------------|-----------|
| **OutOfMemoryError** | Φόρτωση του TIFF σε `BufferedImage` αντί για ροή. | Χρησιμοποιείτε πάντα `InputStream` όπως φαίνεται· αφήστε το Aspose να διαχειριστεί το tiling. |
| **Κενό αποτέλεσμα** | Λάθος υπόδειξη επέκτασης αρχείου (`"tif"` vs `"tiff"`). | Χρησιμοποιήστε την ακριβή συμβολοσειρά που περάσατε στο `add`. |
| **Ακατάλληροι χαρακτήρες** | Η άδεια δεν εφαρμόστηκε ή έληξε. | Επαληθεύστε τη διαδρομή του αρχείου `.lic` και εφαρμόστε την άδεια πριν δημιουργήσετε τη μηχανή. |
| **Αργή αναγνώριση** | Προσαρμοσμένη `OcrConfiguration` με υψηλό DPI. | Παραμείνετε στις προεπιλογές· τροποποιήστε μόνο αν χρειάζεστε μεγαλύτερη ακρίβεια. |

### Πότε να προσαρμόσετε τις ρυθμίσεις  

- **Έγγραφα πολλαπλών γλωσσών:** `ocrEngine.getConfiguration().setLanguage(Language.English, Language.French);`  
- **Μεγαλύτερη ακρίβεια σε μικρές γραμματοσειρές:** `ocrEngine.getConfiguration().setPreprocessOptions(PreprocessOptions.ENHANCE);`  

Θυμηθείτε, κάθε επιπλέον επιλογή μπορεί να αυξήσει τον χρόνο CPU, ειδικά σε μια **μεγάλη εικόνα**. Δοκιμάστε πρώτα με ένα μόνο tile.

## Τι ακολουθεί μετά την εξαγωγή κειμένου από TIFF;

Τώρα που μπορείτε να **εξάγετε κείμενο από TIFF** αποδοτικά, σκεφτείτε την επέκταση της ροής εργασίας για δημιουργία αναζητήσιμων PDF, αποθήκευση συντεταγμένων bounding‑box για επισήμανση, ή παράλληλη επεξεργασία των tiles σε πολλαπλούς πυρήνες CPU. Αυτές οι βελτιώσεις σας επιτρέπουν να δημιουργήσετε ολοκληρωμένες pipelines εγγράφων που μετατρέπει τεράστιες σαρωμένες αρχειοθήκες σε πλήρως αναζητήσιμους, ευρετηριασμένους πόρους κατάλληλους για επιχειρηματική αναζήτηση ή εφαρμογές GIS.

## Συχνές ερωτήσεις

**Ε: Μπορώ να χρησιμοποιήσω αυτή τη λύση σε εμπορική εφαρμογή;**  
Α: Ναι, εφόσον διαθέτετε έγκυρη άδεια Aspose.OCR. Η εμπορική άδεια της βιβλιοθήκης καλύπτει τόσο την ανάπτυξη όσο και την παραγωγική χρήση.

**Ε: Υποστηρίζει το Aspose.OCR αρχεία TIFF με κωδικό πρόσβασης;**  
Α: Το TIFF δεν διαθέτει τυπικό μηχανισμό κωδικού πρόσβασης, έτσι η βιβλιοθήκη το αντιμετωπίζει ως κανονική εικόνα. Για κρυπτογραφημένα containers (π.χ., ZIP), αποκρυπτογραφήστε πριν περάσετε το stream στη μηχανή.

**Ε: Ποιες εκδόσεις Java υποστηρίζονται επίσημα;**  
Α: Το Aspose.OCR for Java υποστηρίζει JDK 8 έως JDK 21, συμπεριλαμβανομένων των Java SE και OpenJDK διανομών.

**Ε: Πώς μπορώ να βελτιώσω την ακρίβεια σε σκαναρίσματα χαμηλής αντίθεσης;**  
Α: Ενεργοποιήστε την προεπεξεργασία: `ocrEngine.getConfiguration().setPreprocessOptions(PreprocessOptions.CONTRAST_ENHANCE);` Αυτό αυξάνει την εμπιστοσύνη OCR σε θορυβώδεις εικόνες.

**Ε: Υπάρχει όριο στο μέγεθος εικόνας που μπορώ να επεξεργαστώ;**  
Α: Η μηχανή μπορεί να επεξεργαστεί εικόνες έως αρκετά gigabytes, περιορισμένο μόνο από τον διαθέσιμο χώρο δίσκου για προσωρινά tiles. Η χρήση μνήμης παραμένει κάτω από 200 MB χάρη στη ροή.

---

**Τελευταία ενημέρωση:** 2026-09-28  
**Δοκιμή με:** Aspose.OCR 23.12 for Java  
**Συγγραφέας:** Aspose

## Σχετικά Μαθήματα

- [Αναγνώριση Κειμένου από Εικόνα με Aspose OCR Java Tutorial](/ocr/java/ocr-operations/recognize-text-from-image-with-aspose-ocr-java-tutorial/)
- [Εξαγωγή Κειμένου από Εικόνα με Aspose OCR Java Quick Guide](/ocr/java/ocr-basics/extract-text-from-image-with-aspose-ocr-java-quick-guide/)
- [Αναγνώριση Κειμένου Εικόνας χρησιμοποιώντας Aspose OCR GPU Java](/ocr/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}