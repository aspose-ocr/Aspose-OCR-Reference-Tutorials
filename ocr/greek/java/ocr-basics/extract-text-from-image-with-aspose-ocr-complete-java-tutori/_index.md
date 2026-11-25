---
category: general
date: 2026-05-31
description: Εξάγετε κείμενο από εικόνα χρησιμοποιώντας το Aspose OCR σε Java. Ακολουθήστε
  αυτό το βήμα‑βήμα οδηγό Aspose OCR για να φορτώσετε την εικόνα για OCR και να λάβετε
  ακριβή αποτελέσματα.
draft: false
keywords:
- extract text from image
- load image for ocr
- aspose ocr tutorial
language: el
og_description: Εξαγωγή κειμένου από εικόνα σε Java με Aspose OCR. Αυτό το σεμινάριο
  σας καθοδηγεί στη φόρτωση μιας εικόνας για OCR και παρέχει ένα πλήρες, εκτελέσιμο
  παράδειγμα.
og_title: Εξαγωγή κειμένου από εικόνα με Aspose OCR – Οδηγός Java
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Extract text from image using Aspose OCR in Java. Follow this step‑by‑step
    Aspose OCR tutorial to load image for OCR and get accurate results.
  headline: Extract Text from Image with Aspose OCR – Complete Java Tutorial
  type: TechArticle
- description: Extract text from image using Aspose OCR in Java. Follow this step‑by‑step
    Aspose OCR tutorial to load image for OCR and get accurate results.
  name: Extract Text from Image with Aspose OCR – Complete Java Tutorial
  steps:
  - name: Prerequisites
    text: '- Java Development Kit 8 or newer - Maven or Gradle (any build tool that
      can pull the Aspose OCR JAR) - An Aspose OCR license file (`Aspose.OCR.Java.lic`)
      – you can get a free trial from Aspose.com - A sample image (`telugu_sample.png`)
      containing clear Telugu characters (or swap it for any language'
  - name: Expected Output
    text: 'If `telugu_sample.png` contains the phrase “నమస్తే ప్రపంచం”, the console
      will print something like:'
  - name: 1. Processing Multiple Images in a Loop
    text: 'If you need to **extract text from image** files in bulk, wrap steps 4‑5
      in a loop:'
  - name: 2. Switching Languages Dynamically
    text: 'Sometimes a folder contains mixed‑language documents. You can query the
      engine’s `detectLanguage()` method (available in newer versions) and set it
      on the fly:'
  - name: 3. Dealing with Low‑Resolution Images
    text: 'If the OCR confidence is low, try these tricks:'
  - name: 4. Handling Exceptions Gracefully
    text: Network drives, missing files, or corrupt images will throw exceptions.
      Always catch `Exception` (as shown in the main method) and log the stack trace
      or fallback to a default image.
  type: HowTo
tags:
- Aspose OCR
- Java
- Image Processing
title: Εξαγωγή κειμένου από εικόνα με το Aspose OCR – Πλήρης οδηγός Java
url: /el/java/ocr-basics/extract-text-from-image-with-aspose-ocr-complete-java-tutori/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Απόσπασμα Κειμένου από Εικόνα με Aspose OCR – Πλήρης Java Tutorial

Έχετε ποτέ χρειαστεί να **εξάγετε κείμενο από εικόνα** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη θα σας προσφέρει ταυτόχρονα ταχύτητα και ακρίβεια; Δεν είστε μόνοι. Σε πολλά έργα—σκεφτείτε σάρωση τιμολογίων, ψηφιοποίηση αποδείξεων ή πολυγλωσσική αρχειοθέτηση εγγράφων—η δυνατότητα να εξάγετε χαρακτήρες απευθείας από μια εικόνα είναι καθοριστική.

Τα καλά νέα; Με το Aspose OCR για Java μπορείτε να **φορτώσετε εικόνα για OCR** σε λίγες μόνο γραμμές και να έχετε το κείμενο έτοιμο για περαιτέρω επεξεργασία. Σε αυτό το **Aspose OCR tutorial** θα περάσουμε από όλη τη ροή εργασίας, από την άδεια χρήσης μέχρι την εκτύπωση του αναγνωρισμένου κειμένου, ώστε να μπορείτε να αντιγράψετε‑επικολλήσετε τον κώδικα και να τον εκτελέσετε σήμερα.

## Τι Καλύπτει Αυτό το Tutorial

- Ρύθμιση της άδειας Aspose OCR (ώστε η demo να τρέχει χωρίς υδατογραφήματα αξιολόγησης)  
- Δημιουργία ενός αντικειμένου `OcrEngine` και επιλογή γλώσσας (Telugu στο παράδειγμά μας)  
- **Φόρτωση εικόνας για OCR** χρησιμοποιώντας το `OcrImage`  
- Εκτέλεση της αναγνώρισης και εκτύπωση του αποτελέσματος  
- Συμβουλές για διαχείριση πολλαπλών σελίδων, διαφορετικών μορφών εικόνας και κοινών προβλημάτων  

Στο τέλος θα έχετε ένα αυτόνομο πρόγραμμα Java που **εξάγει κείμενο από εικόνα** αξιόπιστα, και θα ξέρετε πώς να το προσαρμόσετε για άλλες γλώσσες ή επεξεργασία σε παρτίδες.

### Προαπαιτούμενα

- Java Development Kit 8 ή νεότερο  
- Maven ή Gradle (οποιοδήποτε εργαλείο κατασκευής που μπορεί να κατεβάσει το Aspose OCR JAR)  
- Ένα αρχείο άδειας Aspose OCR (`Aspose.OCR.Java.lic`) – μπορείτε να λάβετε δωρεάν δοκιμή από το Aspose.com  
- Μια δείγμα εικόνας (`telugu_sample.png`) που περιέχει καθαρούς χαρακτήρες Telugu (ή αντικαταστήστε το με οποιαδήποτε γλώσσα προτιμάτε)

---

## Βήμα 1: Προσθήκη του Aspose OCR στο Έργο σας

Πρώτα απ' όλα—το έργο σας χρειάζεται τη βιβλιοθήκη Aspose OCR. Αν χρησιμοποιείτε Maven, προσθέστε αυτήν την εξάρτηση στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest version at the time of writing -->
</dependency>
```

Οι χρήστες του Gradle μπορούν να προσθέσουν:

```gradle
implementation 'com.aspose:aspose-ocr:23.10'
```

> **Pro tip:** Παρακολουθείτε το αποθετήριο Aspose Maven για εκδόσεις patch· οι νεότερες εκδόσεις συχνά βελτιώνουν την υποστήριξη γλωσσών και την ταχύτητα.

---

## Βήμα 2: Εφαρμογή της Άδειας Aspose OCR

Χωρίς έγκυρη άδεια η βιβλιοθήκη λειτουργεί, αλλά κάθε σελίδα που επεξεργάζεστε θα φέρει μια σήμανση «Evaluation». Ακολουθεί ο απλός τρόπος για να την εφαρμόσετε:

```java
import com.aspose.ocr.*;

public class LicenseHelper {
    /** Loads the Aspose OCR license from the given path. */
    public static void applyLicense(String licensePath) throws Exception {
        License license = new License();
        license.setLicense(licensePath);
        System.out.println("Aspose OCR license applied successfully.");
    }
}
```

*Γιατί είναι σημαντικό:* Η εφαρμογή της άδειας μία φορά στην αρχή εξασφαλίζει ότι η μηχανή λειτουργεί με πλήρη ταχύτητα και αφαιρεί τυχόν ανεπιθύμητα υδατογραφήματα από το αποτέλεσμα.

---

## Βήμα 3: Δημιουργία και Διαμόρφωση της Μηχανής OCR

Τώρα εκκινούμε τη μηχανή και της λέμε ποια γλώσσα μας ενδιαφέρει. Το Aspose OCR περιλαμβάνει πάνω από 100 γλώσσες· στο παράδειγμά μας θα χρησιμοποιήσουμε τη Telugu.

```java
import com.aspose.ocr.*;

public class EngineFactory {
    /** Returns a ready‑to‑use OcrEngine configured for the requested language. */
    public static OcrEngine createEngine(OcrLanguage language) {
        OcrEngine engine = new OcrEngine();
        engine.setLanguage(language);
        System.out.println("OCR engine created for language: " + language);
        return engine;
    }
}
```

Αν χρειάζεται να επεξεργαστείτε Αγγλικά, Αραβικά ή ακόμη και ένα προσαρμοσμένο πακέτο γλώσσας, απλώς αντικαταστήστε το `OcrLanguage.TELUGU` με την κατάλληλη τιμή enum.

---

## Βήμα 4: **Φόρτωση Εικόνας για OCR**

Αυτό είναι ο πυρήνας της ροής εργασίας **εξαγωγής κειμένου από εικόνα**. Η κλάση `OcrImage` δέχεται διαδρομή αρχείου, `InputStream` ή `BufferedImage`. Παρακάτω χρησιμοποιούμε μια απλή διαδρομή συστήματος αρχείων.

```java
import com.aspose.ocr.*;

public class ImageLoader {
    /** Loads an image from disk and attaches it to the OCR engine. */
    public static void attachImage(OcrEngine engine, String imagePath) throws Exception {
        OcrImage ocrImage = new OcrImage(imagePath);
        engine.setImage(ocrImage);
        System.out.println("Image loaded for OCR: " + imagePath);
    }
}
```

> **Γιατί είναι σημαντικό:** Η παροχή ενός υψηλής ανάλυσης PNG ή TIFF μπορεί να βελτιώσει δραστικά την ακρίβεια αναγνώρισης, ειδικά για σύνθετες γραφές όπως η Telugu.

---

## Βήμα 5: Εκτέλεση της Αναγνώρισης

Με τη μηχανή διαμορφωμένη και την εικόνα συνδεδεμένη, η πραγματική εξαγωγή κειμένου είναι μια κλήση μεθόδου.

```java
import com.aspose.ocr.*;

public class Recognizer {
    /** Executes OCR and returns the recognized string. */
    public static String recognizeText(OcrEngine engine) throws Exception {
        String text = engine.recognize();
        System.out.println("Recognition completed.");
        return text;
    }
}
```

Το επιστρεφόμενο `String` περιέχει αλλαγές γραμμής ακριβώς όπως εμφανίζονται στην εικόνα, κάτι που καθιστά την επεξεργασία μετά (π.χ., διαίρεση σε γραμμές) απλή.

---

## Βήμα 6: Συνδυάστε Όλα – Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω βρίσκεται η πλήρης, έτοιμη προς εκτέλεση κλάση Java που συνδέει όλα τα τμήματα από τα βήματα 1‑5. Αποθηκεύστε την ως `ExtractTeluguText.java` (ή οποιοδήποτε όνομα θέλετε) και εκτελέστε την από το IDE ή τη γραμμή εντολών.

```java
import com.aspose.ocr.*;

public class ExtractTeluguText {
    public static void main(String[] args) {
        try {
            // 1️⃣ Apply license – replace with your actual .lic file location
            LicenseHelper.applyLicense("Aspose.OCR.Java.lic");

            // 2️⃣ Create OCR engine for Telugu (feel free to switch language)
            OcrEngine ocrEngine = EngineFactory.createEngine(OcrLanguage.TELUGU);

            // 3️⃣ Load the image you want to process
            String imagePath = "YOUR_DIRECTORY/telugu_sample.png";
            ImageLoader.attachImage(ocrEngine, imagePath);

            // 4️⃣ Run the OCR engine
            String recognizedText = Recognizer.recognizeText(ocrEngine);

            // 5️⃣ Display the extracted text
            System.out.println("=== Extracted Text ===");
            System.out.println(recognizedText);
        } catch (Exception e) {
            System.err.println("Error during OCR processing:");
            e.printStackTrace();
        }
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Αν το `telugu_sample.png` περιέχει τη φράση “నమస్తే ప్రపంచం”, η κονσόλα θα εκτυπώσει κάτι όπως:

```
=== Extracted Text ===
నమస్తే ప్రపంచం
```

Φυσικά, το ακριβές αποτέλεσμα εξαρτάται από την ποιότητα της εικόνας, τη γραμματοσειρά και τις ιδιαιτερότητες της γλώσσας.

---

## Διαχείριση Συνηθισμένων Σεναρίων & Ακραίων Περιπτώσεων

### 1. Επεξεργασία Πολλαπλών Εικόνων σε Βρόχο

Αν χρειάζεται να **εξάγετε κείμενο από εικόνα** σε μεγάλες ποσότητες, τυλίξτε τα βήματα 4‑5 σε έναν βρόχο:

```java
String[] images = {"img1.png", "img2.png", "img3.png"};
for (String path : images) {
    ImageLoader.attachImage(ocrEngine, path);
    String text = Recognizer.recognizeText(ocrEngine);
    System.out.println("Result for " + path + ":\n" + text);
}
```

### 2. Δυναμική Αλλαγή Γλωσσών

Μερικές φορές ένας φάκελος περιέχει έγγραφα πολλαπλών γλωσσών. Μπορείτε να ερωτήσετε τη μέθοδο `detectLanguage()` της μηχανής (διαθέσιμη σε νεότερες εκδόσεις) και να τη ρυθμίσετε άμεσα:

```java
OcrLanguage detected = ocrEngine.detectLanguage();
ocrEngine.setLanguage(detected);
```

### 3. Διαχείριση Εικόνων Χαμηλής Ανάλυσης

Αν η εμπιστοσύνη του OCR είναι χαμηλή, δοκιμάστε αυτές τις τεχνικές:

- Αυξήστε την εικόνα τουλάχιστον σε 300 dpi πριν τη δώσετε στο Aspose OCR.  
- Μετατρέψτε την εικόνα σε κλίμακα του γκρι για μείωση του θορύβου.  
- Χρησιμοποιήστε `engine.setPreprocessOptions(PreprocessOptions.ENHANCE_CONTRAST);`

### 4. Χειρισμός Εξαίρεσεων με Ευγένεια

Δίκτυα αποθήκευσης, ελλιπή αρχεία ή κατεστραμμένες εικόνες θα προκαλέσουν εξαιρέσεις. Πάντα πιάστε το `Exception` (όπως φαίνεται στη κύρια μέθοδο) και καταγράψτε το stack trace ή επιστρέψτε σε προεπιλεγμένη εικόνα.

---

## Συμβουλές Απόδοσης & Καλές Πρακτικές

- **Επαναχρησιμοποίηση του αντικειμένου `OcrEngine`** για πολλαπλές αναγνώσεις· η δημιουργία νέας μηχανής κάθε φορά προσθέτει επιβάρυνση.  
- **Αποδέσμευση μεγάλων εικόνων** μετά την επεξεργασία (`ocrEngine.getImage().dispose();`) για ελευθέρωση εγγενούς μνήμης.  
- **Επεξεργασία παρτίδας**: Αν έχετε χιλιάδες σελίδες, σκεφτείτε την τοποθέτηση σε ουρά και τη χρήση thread pool—το Aspose OCR είναι thread‑safe όταν κάθε νήμα έχει τη δική του μηχανή.  
- **Τοποθέτηση άδειας**: Αποθηκεύστε το αρχείο `.lic` εκτός του δέντρου πηγαίου κώδικα (π.χ., μεταβλητή περιβάλλοντος) ώστε να μην το δεσμεύσετε στον έλεγχο εκδόσεων.

---

## Συμπέρασμα

Μόλις περάσαμε από ένα πλήρες **Aspose OCR tutorial** που σας δείχνει πώς να **εξάγετε κείμενο από εικόνα** σε Java, βήμα προς βήμα. Από την άδεια χρήσης μέχρι τη φόρτωση της εικόνας, την εκτέλεση της μηχανής και τη διαχείριση ακραίων περιπτώσεων, ο παραπάνω κώδικας αποτελεί μια σταθερή βάση που μπορείτε να επεκτείνετε για οποιαδήποτε γλώσσα υποστηρίζει το Aspose.

Τώρα που έχετε κατακτήσει τα βασικά, γιατί να μην πειραματιστείτε; Δοκιμάστε να αντικαταστήσετε το `OcrLanguage.TELUGU` με `OcrLanguage.ENGLISH`, δώστε ένα PDF πολλαπλών σελίδων (μετατρέποντας πρώτα κάθε σελίδα σε εικόνα), ή ενσωματώστε το αποτέλεσμα σε ευρετήριο αναζήτησης. Οι δυνατότητες είναι πρακτικά ατελείωτες, και το API του Aspose OCR είναι αρκετά ευέλικτο για να τα καταφέρει.

Έχετε ερωτήσεις για συγκεκριμένο σενάριο—ίσως OCR σε χειρόγραφες σημειώσεις ή σε φωτογραφία από κινητό; Αφήστε ένα σχόλιο και θα εμβαθύνουμε μαζί. Καλό κώδικα!

## Τι Θα Μάθετε Στη Σειρά;

- [Εξαγωγή Κειμένου από Εικόνα Java με Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Πώς να κάνετε OCR Κειμένου Εικόνας με Γλώσσα χρησιμοποιώντας Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Μετατροπή Εικόνας σε Κείμενο σε Java χρησιμοποιώντας Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}