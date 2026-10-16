---
category: general
date: 2026-06-19
description: Πραγματοποιήστε OCR σε εικόνα χρησιμοποιώντας το Aspose OCR Java. Μάθετε
  πώς να φορτώνετε εικόνα για OCR, να χρησιμοποιείτε την άδεια Aspose και να εξάγετε
  κείμενο από την εικόνα σε λίγα λεπτά.
draft: false
keywords:
- perform ocr on image
- extract text from image
- recognize text image
- use aspose license
- load image for ocr
language: el
og_description: Εκτελέστε OCR σε εικόνα με το Aspose OCR Java. Αυτός ο οδηγός δείχνει
  πώς να χρησιμοποιήσετε την άδεια Aspose, να φορτώσετε εικόνα για OCR και να εξάγετε
  κείμενο από την εικόνα αποδοτικά.
og_title: Εκτελέστε OCR σε εικόνα με το Aspose OCR Java – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Perform OCR on image using Aspose OCR Java. Learn how to load image
    for OCR, use Aspose license, and extract text from image in minutes.
  headline: Perform OCR on Image with Aspose OCR Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Perform OCR on image using Aspose OCR Java. Learn how to load image
    for OCR, use Aspose license, and extract text from image in minutes.
  name: Perform OCR on Image with Aspose OCR Java – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Console Output
    text: '``` Aspose OCR license applied successfully. Image loaded from: YOUR_DIRECTORY/mixed_latin_cyrillic.png
      === OCR RESULT === Hello World! Привет мир! ```'
  - name: Why a License Matters
    text: Running the library in evaluation mode is fine for quick tests, but it adds
      a watermark to the output and limits the number of pages you can process per
      run. Applying the **use aspose license** step removes these restrictions and
      signals to Aspose that you’re a paying customer.
  - name: How to Obtain and Apply It
    text: 1. Purchase a license from the Aspose store. 2. Download the `Aspose.OCR.Java.lic`
      file. 3. Place it somewhere your application can read—commonly the `src/main/resources`
      folder. 4. Call `new License().setLicense("Aspose.OCR.Java.lic");` before any
      OCR work, as shown in the code above.
  - name: Common Pitfalls
    text: '| Issue | Symptom | Fix | |-------|---------|-----| | Wrong file path |
      `FileNotFoundException` | Double‑check the path; use `Paths.get(...)` for OS‑independent
      separators. | | Unsupported format | `UnsupportedOperationException` | Convert
      the image to PNG or JPEG before loading. | | Huge image ( > '
  - name: Dealing with Multiple Languages
    text: Because we set `engine.setLanguage(Language.Auto)`, Aspose will attempt
      to detect languages on‑the‑fly. If you know the language in advance (e.g., all
      documents are Russian), you can replace `Language.Auto` with `Language.Russian`
      for a performance boost.
  - name: Post‑Processing Tips
    text: "- **Trim whitespace**: `result.getText().trim()`. - **Normalize line endings**:
      `result.getText().replace(\"\r\n\", \"\n\")`. - **Remove non‑printable characters**:
      use a regex like `result.getText().replaceAll(\"[^\\p{Print}]\", \"\")`."
  type: HowTo
tags:
- Aspose OCR
- Java
- Image Processing
title: Εκτελέστε OCR σε εικόνα με το Aspose OCR Java – Πλήρης οδηγός βήμα‑προς‑βήμα
url: /el/python-java/general/perform-ocr-on-image-with-aspose-ocr-java-complete-step-by-s/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Διεκπεραίωση OCR σε Εικόνα με Aspose OCR Java – Πλήρης Οδηγός Βήμα‑βήμα

Έχετε ποτέ χρειαστεί να **perform OCR on image** αρχεία αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη θα σας δώσει αξιόπιστα αποτελέσματα χωρίς άφθονη διαμόρφωση; Δεν είστε μόνοι. Σε πολλά πραγματικά έργα—σκεφτείτε τη σάρωση διαβατηρίων, την ψηφιοποίηση τιμολογίων ή την εξαγωγή κειμένου από στιγμιότυπα—η δυνατότητα γρήγορης αναγνώρισης δεδομένων κειμένου σε εικόνα είναι καθοριστική.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα ένα πρακτικό παράδειγμα που δείχνει ακριβώς πώς να **perform OCR on image** χρησιμοποιώντας το Aspose OCR για Java. Θα καλύψουμε τα πάντα, από την εφαρμογή της άδειας Aspose μέχρι τη φόρτωση της εικόνας, την εκτέλεση της μηχανής και τελικά το **extract text from image** ώστε να το χρησιμοποιήσετε παρακάτω. Χωρίς περιττές πληροφορίες, μόνο μια λειτουργική λύση που μπορείτε να αντιγράψετε‑επικολλήσετε.

## Τι Θα Αποκομίσετε

- Μια σαφής εικόνα για το πώς να **use Aspose license** σε ένα έργο Java.  
- Ο ακριβής κώδικας που χρειάζεται για **load image for OCR** και να αφήσει τη μηχανή να ανιχνεύσει αυτόματα τις γλώσσες.  
- Οδηγίες βήμα‑βήμα για **recognize text image** περιεχόμενο και **extract text from image** με ασφάλεια.  
- Συμβουλές για την αντιμετώπιση κοινών προβλημάτων (κενά αποτελέσματα, μη υποστηριζόμενες μορφές και προβλήματα μνήμης).  

> **Prerequisites** – Java 8 ή νεότερη, Maven ή Gradle για διαχείριση εξαρτήσεων, και αρχείο άδειας Aspose OCR για Java (ή μπορείτε να τρέξετε σε λειτουργία αξιολόγησης).

---

## Πώς να Διεκπεραιώσετε OCR σε Εικόνα με Aspose OCR Java

Παρακάτω είναι το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα Java που δείχνει ολόκληρη τη ροή. Αποθηκεύστε το ως `AsposeOcrDemo.java` και τρέξτε το από το IDE ή τη γραμμή εντολών.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.License;

/**
 * Demonstrates how to perform OCR on an image using Aspose OCR for Java.
 * This example shows:
 *   • Applying an Aspose license (or skipping for evaluation)
 *   • Loading an image for OCR
 *   • Setting automatic language detection
 *   • Recognizing the image and extracting the detected text
 */
public class AsposeOcrDemo {

    public static void main(String[] args) {
        // -------------------------------------------------
        // Step 1: Apply your Aspose OCR license (optional)
        // -------------------------------------------------
        // If you have a license file, uncomment the next two lines.
        // This removes the evaluation watermark and lifts usage limits.
        try {
            License license = new License();
            license.setLicense("Aspose.OCR.Java.lic"); // <-- use aspose license
            System.out.println("Aspose OCR license applied successfully.");
        } catch (Exception ex) {
            // In evaluation mode we simply continue without a license.
            System.out.println("License not found – running in evaluation mode.");
        }

        // -------------------------------------------------
        // Step 2: Create an OCR engine instance
        // -------------------------------------------------
        OcrEngine engine = new OcrEngine();

        // -------------------------------------------------
        // Step 3: Set language detection to automatic
        // -------------------------------------------------
        engine.setLanguage(Language.Auto); // <-- recognize text image automatically

        // -------------------------------------------------
        // Step 4: Load the image you want to recognize
        // -------------------------------------------------
        // Replace the path with the location of your test picture.
        // This demonstrates the “load image for OCR” step.
        String imagePath = "YOUR_DIRECTORY/mixed_latin_cyrillic.png";
        Image image = Image.load(imagePath);
        System.out.println("Image loaded from: " + imagePath);

        // -------------------------------------------------
        // Step 5: Perform OCR and output the recognized text
        // -------------------------------------------------
        OcrResult result = engine.recognize(image);
        if (result != null && result.getText() != null && !result.getText().isEmpty()) {
            System.out.println("=== OCR RESULT ===");
            System.out.println(result.getText());          // <-- extract text from image
        } else {
            System.out.println("No text was recognized. Check image quality or language settings.");
        }
    }
}
```

### Αναμενόμενη Έξοδος Κονσόλας

```
Aspose OCR license applied successfully.
Image loaded from: YOUR_DIRECTORY/mixed_latin_cyrillic.png
=== OCR RESULT ===
Hello World!
Привет мир!
```

Αν τρέξετε το πρόγραμμα χωρίς αρχείο άδειας, η πρώτη γραμμή θα δηλώνει απλώς ότι βρίσκεστε σε λειτουργία αξιολόγησης, αλλά το OCR λειτουργεί κανονικά.

---

## Ρύθμιση και Χρήση Άδειας Aspose

### Γιατί είναι Σημαντική η Άδεια

Η εκτέλεση της βιβλιοθήκης σε λειτουργία αξιολόγησης είναι εντάξει για γρήγορες δοκιμές, αλλά προσθέτει υδατογράφημα στην έξοδο και περιορίζει τον αριθμό των σελίδων που μπορείτε να επεξεργαστείτε ανά εκτέλεση. Η εφαρμογή του βήματος **use aspose license** αφαιρεί αυτούς τους περιορισμούς και ενημερώνει το Aspose ότι είστε πελάτης με πληρωμή.

### Πώς να Αποκτήσετε και να Εφαρμόσετε την Άδεια

1. Αγοράστε μια άδεια από το κατάστημα Aspose.  
2. Κατεβάστε το αρχείο `Aspose.OCR.Java.lic`.  
3. Τοποθετήστε το κάπου που η εφαρμογή σας μπορεί να το διαβάσει—συνήθως στο φάκελο `src/main/resources`.  
4. Καλέστε `new License().setLicense("Aspose.OCR.Java.lic");` πριν από οποιαδήποτε εργασία OCR, όπως φαίνεται στον παραπάνω κώδικα.  

> **Pro tip:** Αν αναπτύξετε σε διακομιστή, χρησιμοποιήστε απόλυτη διαδρομή ή φορτωτή πόρων class‑path για να αποφύγετε το `FileNotFoundException`.

---

## Φόρτωση Εικόνας για Επεξεργασία OCR

Η γραμμή `Image.load("YOUR_DIRECTORY/mixed_latin_cyrillic.png")` είναι η καρδιά του βήματος **load image for OCR**. Το Aspose OCR υποστηρίζει μια ευρεία γκάμα μορφών: PNG, JPEG, BMP, TIFF, και ακόμη πολυ‑σελίδες PDF (όταν συνδυάζεται με το Aspose.Pdf).

### Συνηθισμένα Προβλήματα

| Πρόβλημα | Σύμπτωμα | Διόρθωση |
|----------|----------|----------|
| Λάθος διαδρομή αρχείου | `FileNotFoundException` | Ελέγξτε ξανά τη διαδρομή· χρησιμοποιήστε `Paths.get(...)` για διαχωριστές ανεξάρτητους από το OS. |
| Μη υποστηριζόμενη μορφή | `UnsupportedOperationException` | Μετατρέψτε την εικόνα σε PNG ή JPEG πριν τη φόρτωση. |
| Μεγάλη εικόνα ( > 10 MP) | Σφάλματα έλλειψης μνήμης | Μειώστε την ανάλυση της εικόνας χρησιμοποιώντας `java.awt.Image` πριν τη δώσετε στο Aspose. |

---

## Εξαγωγή Κειμένου από Εικόνα και Διαχείριση Αποτελεσμάτων

Μόλις ολοκληρωθεί η μηχανή OCR, το αντικείμενο `OcrResult` περιέχει το αναγνωρισμένο κείμενο. Εδώ είναι που **extract text from image** για περαιτέρω επεξεργασία—αποθήκευση σε βάση δεδομένων, τροφοδοσία ευρετηρίου αναζήτησης ή ενσωμάτωση σε pipeline NLP.

### Διαχείριση Πολλαπλών Γλωσσών

Επειδή ορίσαμε `engine.setLanguage(Language.Auto)`, το Aspose θα προσπαθήσει να εντοπίσει τις γλώσσες αυτόματα. Αν γνωρίζετε τη γλώσσα εκ των προτέρων (π.χ., όλα τα έγγραφα είναι Ρωσικά), μπορείτε να αντικαταστήσετε το `Language.Auto` με `Language.Russian` για βελτίωση απόδοσης.

### Συμβουλές Μετα‑επεξεργασίας

- **Αποκοπή κενών**: `result.getText().trim()`.  
- **Κανονικοποίηση λήξεων γραμμής**: `result.getText().replace("\r\n", "\n")`.  
- **Αφαίρεση μη‑εκτυπώσιμων χαρακτήρων**: χρησιμοποιήστε regex όπως `result.getText().replaceAll("[^\\p{Print}]", "")`.

## Αναγνώριση Εικόνας Κειμένου με Προηγμένες Επιλογές (Προαιρετικό)

Αν χρειάζεστε πιο λεπτομερή έλεγχο, το Aspose OCR προσφέρει επιπλέον ιδιότητες:

```java
engine.getImagePreprocessingOptions().setDeskew(true);  // correct tilted text
engine.getImagePreprocessingOptions().setContrast(1.2f); // boost faint characters
engine.getRecognitionOptions().setExtractAreas(true);   // get bounding boxes
```

Αυτές οι ρυθμίσεις είναι χρήσιμες όταν εργάζεστε με σαρωμένα έγγραφα που έχουν παραμόρφωση ή χαμηλή αντίθεση.

## Συνοπτική Παρουσίαση Πλήρους Παραδείγματος

Συνδυάζοντας όλα, το τελικό πρόγραμμα εκτελεί τα εξής με τη σωστή σειρά:

1. **Perform OCR on image** – δημιουργώντας ένα `OcrEngine`.  
2. **Use Aspose license** – προαιρετικό αλλά συνιστάται.  
3. **Load image for OCR** – μέσω `Image.load`.  
4. **Set language detection** – `Language.Auto` για **recognize text image** αυτόματα.  
5. **Extract text from image** – εκτύπωση του αποτελέσματος, με ευγενική διαχείριση κενών απαντήσεων.  

Μπορείτε να αντιγράψετε το παραπάνω μπλοκ κώδικα απευθείας σε ένα έργο Maven με αυτήν την εξάρτηση:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check for the latest version -->
</dependency>
```

Τρέξτε `mvn compile exec:java -Dexec.mainClass="AsposeOcrDemo"` και παρακολουθήστε την κονσόλα να εμφανίζει το αναγνωρισμένο κείμενο.

## Συμπέρασμα

Μόλις σας δείξαμε πώς να **perform OCR on image** αρχεία χρησιμοποιώντας το Aspose OCR για Java, από την εφαρμογή άδειας μέχρι το **loading the image for OCR**, το **recognizing text image** περιεχόμενο, και τελικά το **extracting text from image** για περαιτέρω χρήση. Η προσέγγιση είναι απλή, λειτουργεί με πολλές γλώσσες αμέσως, και μπορεί να επεκταθεί με προχωρημένες επιλογές προεπεξεργασίας όταν χρειάζεται.

Τι ακολουθεί; Δοκιμάστε να τροφοδοτήσετε το αποτέλεσμα OCR σε ευρετήριο αναζήτησης, να δημιουργήσετε PDF με το εξαγόμενο κείμενο, ή να πειραματιστείτε με διαφορετικές μορφές εικόνας. Οι δυνατότητες είναι ατελείωτες, και με το ισχυρό API του Aspose θα περάσετε περισσότερο χρόνο δημιουργώντας λειτουργίες παρά αντιμετωπίζοντας προβλήματα OCR.

Έχετε ερωτήσεις ή αντιμετωπίζετε κάποιο σενάριο; Αφήστε ένα σχόλιο παρακάτω—καλή προγραμματιστική!

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να εξάγετε κείμενο από εικόνα από URL χρησιμοποιώντας Aspose.OCR για Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)
- [Μετατροπή Εικόνας σε Κείμενο σε Java χρησιμοποιώντας Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Εξαγωγή Κειμένου από Εικόνα Java με Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}