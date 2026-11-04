---
category: general
date: 2026-02-22
description: Πώς να εκτελέσετε OCR γρήγορα χρησιμοποιώντας το Aspose OCR για Java.
  Μάθετε να αναγνωρίζετε κείμενο από εικόνα, να εξάγετε κείμενο από PNG και να μετατρέπετε
  την εικόνα σε κείμενο σε λίγα λεπτά.
draft: false
keywords:
- how to perform OCR
- recognize text from image
- extract text from png
- how to read text
- convert image to text
language: el
og_description: Πώς να εκτελέσετε OCR με το Aspose OCR για Java. Αυτός ο οδηγός σας
  δείχνει πώς να αναγνωρίζετε κείμενο από εικόνα, να εξάγετε κείμενο από PNG και να
  μετατρέπετε την εικόνα σε κείμενο αποδοτικά.
og_title: Πώς να εκτελέσετε OCR σε Java – Οδηγός Aspose βήμα προς βήμα
tags:
- OCR
- Java
- Aspose
title: Πώς να εκτελέσετε OCR σε Java – Πλήρης οδηγός Aspose OCR
url: /el/java/ocr-operations/how-to-perform-ocr-in-java-complete-aspose-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εκτελέσετε OCR σε Java – Πλήρες Εγχειρίδιο Aspose OCR

Έχετε αναρωτηθεί ποτέ **πώς να εκτελέσετε OCR** σε ένα αρχείο PNG χωρίς να ασχοληθείτε με χαμηλού επιπέδου επεξεργασία εικόνας; Δεν είστε οι μόνοι. Σε πολλά έργα — σάρωση τιμολογίων, ψηφιοποίηση αποδείξεων ή απλώς εξαγωγή κειμένου από στιγμιότυπα οθόνης — οι προγραμματιστές χρειάζονται έναν αξιόπιστο τρόπο για **να αναγνωρίσουν κείμενο από εικόνα**. Τα καλά νέα; Με το Aspose OCR για Java μπορείτε **να μετατρέψετε εικόνα σε κείμενο** με λίγες μόνο γραμμές κώδικα.

Σε αυτό το εγχειρίδιο θα περάσουμε από όλα όσα χρειάζεστε: εφαρμογή άδειας, φόρτωση εικόνας, εξαγωγή κειμένου και αντιμετώπιση μερικών κοινών προβλημάτων. Στο τέλος θα μπορείτε **να εξάγετε κείμενο από PNG** αρχεία και οποιαδήποτε άλλη υποστηριζόμενη μορφή, διατηρώντας τον κώδικά σας καθαρό και έτοιμο για παραγωγή.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

* Java 11 ή νεότερη εγκατεστημένη (η βιβλιοθήκη λειτουργεί με Java 8+ αλλά συνιστάται η 11+).
* Αρχείο άδειας Aspose OCR για Java (`Aspose.OCR.Java.lic`). Μπορείτε να λάβετε δωρεάν δοκιμή από την ιστοσελίδα της Aspose.
* Maven ή Gradle για διαχείριση εξαρτήσεων (θα δείξουμε το απόσπασμα Maven).
* Ένα δείγμα εικόνας (`sample.png`) τοποθετημένο κάπου που το έργο σας μπορεί να το διαβάσει.

Δεν απαιτούνται άλλοι τρίτοι μηχανισμοί OCR — το Aspose διαχειρίζεται όλη τη βαριά δουλειά εσωτερικά.

---

## Βήμα 1: Προσθήκη Εξάρτησης Aspose OCR

Πρώτα, συμπεριλάβετε τη βιβλιοθήκη Aspose OCR στο `pom.xml`. Αυτή η μοναδική γραμμή τραβά την πιο πρόσφατη σταθερή έκδοση από το Maven Central.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the newest version -->
</dependency>
```

> **Pro tip:** Αν χρησιμοποιείτε Gradle, το ισοδύναμο είναι  
> `implementation 'com.aspose:aspose-ocr:23.10'`.

Η προσθήκη της εξάρτησης εξασφαλίζει ότι μπορείτε **να αναγνωρίσετε κείμενο από εικόνα** χωρίς επιπλέον ρυθμίσεις.

## Βήμα 2: Εφαρμογή της Άδειας Aspose OCR

Χωρίς έγκυρη άδεια η μηχανή λειτουργεί σε λειτουργία αξιολόγησης, η οποία προσθέτει υδατογράφημα και περιορίζει τον αριθμό των σελίδων που μπορείτε να επεξεργαστείτε. Η εφαρμογή της άδειας είναι απλή — απλώς δείξτε στο αρχείο `.lic` στο δίσκο.

```java
import com.aspose.ocr.*;

public class LicenseDemo {
    public static void main(String[] args) throws Exception {

        // 👉 Step 2.1: Apply the Aspose OCR license (replace with your actual path)
        AsposeLicense.apply("C:/licenses/Aspose.OCR.Java.lic");

        // Continue with OCR operations...
    }
}
```

> **Γιατί είναι σημαντικό:** Η άδεια αφαιρεί το banner “Evaluation” και ξεκλειδώνει πλήρη ακρίβεια, κάτι που είναι απαραίτητο όταν θέλετε καθαρά **αποτελέσματα εξαγωγής κειμένου από png** για επεξεργασία downstream.

## Βήμα 3: Αρχικοποίηση του OcrEngine

Τώρα που η άδεια είναι ενεργή, δημιουργήστε ένα αντικείμενο `OcrEngine`. Αυτό το αντικείμενο είναι το κεντρικό στοιχείο που εκτελεί την πραγματική αναγνώριση.

```java
        // 👉 Step 3.1: Create a fully‑licensed OcrEngine
        OcrEngine ocrEngine = new OcrEngine();

        // Optional: tweak language or DPI settings here if needed
        ocrEngine.getLanguage().setLanguage(OcrLanguage.ENGLISH);
        ocrEngine.setResolution(300); // higher DPI can improve accuracy
```

> **Edge case:** Αν η εικόνα σας περιέχει μη‑αγγλικά χαρακτήρες, αλλάξτε το `OcrLanguage` ανάλογα (π.χ., `OcrLanguage.FRENCH`). Η μηχανή υποστηρίζει πάνω από 30 γλώσσες έτοιμες προς χρήση.

## Βήμα 4: Φόρτωση Εικόνας και Αναγνώριση Κειμένου

Με τη μηχανή έτοιμη, δείξτε την στην εικόνα που θέλετε να επεξεργαστείτε. Το Aspose OCR μπορεί να διαβάσει PNG, JPEG, BMP, TIFF και αρκετές άλλες μορφές.

```java
        // 👉 Step 4.1: Load the image file
        String imagePath = "C:/images/sample.png";
        OcrResult result = ocrEngine.recognizeImage(imagePath);

        // 👉 Step 4.2: Print the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
```

Όταν εκτελέσετε το πρόγραμμα, θα πρέπει να δείτε κάτι παρόμοιο με:

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑12‑01
Total: $256.78
Thank you for your business!
```

Αυτή η έξοδος δείχνει **πώς να διαβάσετε κείμενο** από ένα αρχείο PNG και να το μετατρέψετε σε μια συμβολοσειρά απλού κειμένου που μπορείτε να αποθηκεύσετε, να αναζητήσετε ή να περάσετε σε άλλο σύστημα.

## Βήμα 5: Αντιμετώπιση Κοινών Προβλημάτων

### 5.1 Διαχείριση Εικόνων Χαμηλής Ποιότητας

Αν το αποτέλεσμα OCR φαίνεται ακατάστατο, δοκιμάστε:

* Αύξηση της ανάλυσης (`ocrEngine.setResolution(400)`).
* Μετατροπή της εικόνας σε κλίμακα του γκρι πριν τη δώσετε στη μηχανή.
* Χρήση `ocrEngine.getPreProcessingOptions().setAutoDeskew(true)` για ευθυγράμμιση κεκλιμένου κειμένου.

### 5.2 Εξαγωγή Δομημένων Δεδομένων

Μερικές φορές χρειάζεστε κάτι παραπάνω από ένα σύνολο κειμένου — πίνακες, γραμμές στοιχείων ή ζεύγη κλειδί/τιμή. Αφού **μετατρέψετε εικόνα σε κείμενο**, μπορείτε να κάνετε post‑processing με κανονικές εκφράσεις:

```java
        String raw = result.getText();
        Pattern invoicePattern = Pattern.compile("Invoice #(\\d+)");
        Matcher m = invoicePattern.matcher(raw);
        if (m.find()) {
            System.out.println("Found invoice number: " + m.group(1));
        }
```

### 5.3 Μαζική Επεξεργασία Πολλαπλών Αρχείων

Όταν έχετε έναν φάκελο γεμάτο αποδείξεις, τυλίξτε την κλήση OCR σε βρόχο:

```java
        File folder = new File("C:/images/receipts");
        for (File file : folder.listFiles((dir, name) -> name.toLowerCase().endsWith(".png"))) {
            OcrResult batchResult = ocrEngine.recognizeImage(file.getAbsolutePath());
            // Save or index batchResult.getText() as needed
        }
```

Αυτό το μοτίβο σας επιτρέπει **να εξάγετε κείμενο από PNG** αρχεία μαζικά, κάτι που είναι χρήσιμο για νυχτερινές εργασίες ETL.

## Βήμα 6: Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας τα παραπάνω, εδώ είναι μια μοναδική κλάση Java που μπορείτε να αντιγράψετε‑επικολλήσετε στο IDE σας και να τρέξετε αμέσως (απλώς αντικαταστήστε τις διαδρομές άδειας και εικόνας).

```java
import com.aspose.ocr.*;

public class AsposeOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply license – mandatory for full functionality
        AsposeLicense.apply("C:/licenses/Aspose.OCR.Java.lic");

        // 2️⃣ Create engine (now fully licensed)
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Optional tweaks – language, DPI, preprocessing
        ocrEngine.getLanguage().setLanguage(OcrLanguage.ENGLISH);
        ocrEngine.setResolution(300);
        ocrEngine.getPreProcessingOptions().setAutoDeskew(true);

        // 4️⃣ Recognize a PNG image
        String imgPath = "C:/images/sample.png";
        OcrResult result = ocrEngine.recognizeImage(imgPath);

        // 5️⃣ Output the text – this is the core “convert image to text” step
        System.out.println("=== OCR Output ===");
        System.out.println(result.getText());

        // 6️⃣ Simple post‑processing example (extract invoice number)
        java.util.regex.Pattern p = java.util.regex.Pattern.compile("Invoice #(\\d+)");
        java.util.regex.Matcher m = p.matcher(result.getText());
        if (m.find()) {
            System.out.println("Detected invoice #: " + m.group(1));
        }
    }
}
```

Τρέξτε το πρόγραμμα και θα δείτε το εξαγόμενο κείμενο να εμφανίζεται στην κονσόλα, ακολουθούμενο από τυχόν ανιχνευμένους αριθμούς τιμολογίων. Αυτό είναι ένα πλήρες **workflow εκτέλεσης OCR** από την αρχή μέχρι το τέλος.

---

## Συχνές Ερωτήσεις (FAQ)

**Ε: Λειτουργεί το Aspose OCR σε αρχεία PDF;**  
Α: Ναι. Μπορείτε να δώσετε μια σελίδα PDF ως εικόνα χρησιμοποιώντας `ocrEngine.recognizePdf("file.pdf", pageNumber)`. Το API επιστρέφει το ίδιο αντικείμενο `OcrResult`.

**Ε: Τι γίνεται αν χρειαστεί να **αναγνωρίσω κείμενο από εικόνα** ροές αντί για αρχεία;**  
Α: Χρησιμοποιήστε `ocrEngine.recognizeImage(InputStream)` — ιδανικό για μεταφορτώσεις web ή blobs αποθήκευσης στο cloud.

**Ε: Μπορώ να το τρέξω σε Android;**  
Α: Η βιβλιοθήκη είναι μόνο Java και δεν υποστηρίζεται επίσημα σε Android, αλλά μπορείτε να χρησιμοποιήσετε την έκδοση .NET με Xamarin αν χρειάζεστε υποστήριξη κινητών.

**Ε: Πόσο ακριβής είναι η μηχανή σε σύγκριση με ανοιχτού κώδικα εναλλακτικές;**  
Α: Το Aspose OCR καταγράφει σταθερά πάνω από 95 % ακρίβεια σε καθαρές τυπωμένες εγγράφους και διαχειρίζεται καλύτερα θορυβώδεις σκαναρίσματα από πολλά δωρεάν εργαλεία, ειδικά όταν ενεργοποιείτε την προεπεξεργασία.

---

## Συμπέρασμα

Καλύψαμε **πώς να εκτελέσετε OCR** σε Java χρησιμοποιώντας το Aspose OCR, από την άδεια μέχρι την εξαγωγή καθαρού κειμένου από αρχείο PNG. Τώρα ξέρετε πώς να **αναγνωρίζετε κείμενο από εικόνα**, **να εξάγετε κείμενο από png**, **πώς να διαβάζετε κείμενο** προγραμματιστικά, και **να μετατρέπετε εικόνα σε κείμενο** για επεξεργασία downstream.  

Νιώστε ελεύθεροι να πειραματιστείτε με διαφορετικές γλώσσες, ρυθμίσεις DPI και μαζική επεξεργασία — αυτές οι ρυθμίσεις συχνά κάνουν τη διαφορά μεταξύ ενός αβέβαιου πρωτοτύπου και μιας λύσης παραγωγικής κλίμακας. Αν σας άρεσε αυτός ο οδηγός, δείτε τα tutorials μας για **προεπεξεργασία εικόνας για OCR** και **ενσωμάτωση αποτελεσμάτων OCR με Elasticsearch** για αρχεία εγγράφων με δυνατότητα αναζήτησης.

Καλή προγραμματιστική, και ας είναι τα αποτελέσματα OCR σας πάντα kristall‑clear!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}