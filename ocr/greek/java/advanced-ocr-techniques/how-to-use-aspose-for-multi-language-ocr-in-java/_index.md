---
category: general
date: 2026-02-22
description: Πώς να χρησιμοποιήσετε το Aspose για να εκτελέσετε OCR πολλαπλών γλωσσών
  και να εξάγετε κείμενο από αρχεία εικόνας—μάθετε πώς να φορτώνετε εικόνα για OCR
  και να εκτελείτε OCR στην εικόνα αποδοτικά.
draft: false
keywords:
- how to use aspose
- multi language ocr
- extract text from image
- load image for ocr
- run ocr on image
language: el
og_description: Πώς να χρησιμοποιήσετε το Aspose για να εκτελέσετε OCR σε εικόνες
  με πολλές γλώσσες – βήμα‑βήμα οδηγός για τη φόρτωση εικόνας για OCR και την εξαγωγή
  κειμένου από την εικόνα.
og_title: Πώς να χρησιμοποιήσετε το Aspose για OCR πολλαπλών γλωσσών σε Java
tags:
- Aspose
- OCR
- Java
title: Πώς να χρησιμοποιήσετε το Aspose για OCR πολλαπλών γλωσσών σε Java
url: /el/java/advanced-ocr-techniques/how-to-use-aspose-for-multi-language-ocr-in-java/
---

the whole content with same shortcodes.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε το Aspose για OCR Πολλαπλών Γλωσσών σε Java

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε το Aspose** όταν η εικόνα σας περιέχει κείμενο στα Αγγλικά, Ουκρανικά και Αραβικά ταυτόχρονα; Δεν είστε μόνοι—πολλοί προγραμματιστές συναντούν αυτό το πρόβλημα όταν πρέπει να *εξάγουν κείμενο από εικόνα* που δεν είναι μονογλωσσική.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που δείχνει πώς να **φορτώσετε εικόνα για OCR**, να ενεργοποιήσετε *OCR πολλαπλών γλωσσών* και τέλος να **εκτελέσετε OCR στην εικόνα** για να λάβετε καθαρό, αναγνώσιμο κείμενο. Χωρίς ασαφείς αναφορές, μόνο συγκεκριμένος κώδικας και η λογική πίσω από κάθε γραμμή.

## Τι Θα Μάθετε

- Προσθήκη της βιβλιοθήκης Aspose OCR σε έργο Java (Maven ή Gradle).
- Αρχικοποίηση της μηχανής OCR σωστά.
- Διαμόρφωση της μηχανής για *OCR πολλαπλών γλωσσών* και ενεργοποίηση της αυτόματης ανίχνευσης.
- Φόρτωση μιας εικόνας που περιέχει μεικτά σενάρια.
- Εκτέλεση της αναγνώρισης και **εξαγωγή κειμένου από εικόνα**.
- Διαχείριση κοινών προβλημάτων όπως μη υποστηριζόμενες γλώσσες ή ελλιπή αρχεία.

Στο τέλος θα έχετε μια αυτόνομη κλάση Java που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο και να αρχίσετε αμέσως την επεξεργασία εικόνων.

---

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

| Απαίτηση | Γιατί είναι σημαντική |
|----------|------------------------|
| Java 8 ή νεότερη | Το Aspose OCR στοχεύει σε Java 8+. |
| Maven ή Gradle (οποιοδήποτε εργαλείο κατασκευής) | Για την αυτόματη λήψη του JAR του Aspose OCR. |
| Ένα αρχείο εικόνας με κείμενο πολλαπλών γλωσσών (π.χ., `mixed_script.jpg`) | Αυτό είναι που θα **φορτώσουμε εικόνα για OCR**. |
| Έγκυρη άδεια Aspose OCR (προαιρετική) | Χωρίς άδεια θα έχετε υδατογράφημα στην έξοδο, αλλά ο κώδικας λειτουργεί το ίδιο. |

Τα έχετε όλα; Τέλεια—ας ξεκινήσουμε.

---

## Βήμα 1: Προσθήκη του Aspose OCR στο Έργο Σας

### Maven

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- latest as of Feb 2026 -->
</dependency>
```

### Gradle

```groovy
// build.gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

> **Pro tip:** Παρακολουθείτε τον αριθμό έκδοσης· οι νεότερες κυκλοφορίες προσθέτουν πακέτα γλωσσών και βελτιώσεις απόδοσης.

Η προσθήκη της εξάρτησης είναι το πρώτο συγκεκριμένο βήμα στο **πώς να χρησιμοποιήσετε το Aspose**—η βιβλιοθήκη φέρνει τις κλάσεις `OcrEngine`, `OcrInput` και `OcrResult` που θα χρειαστούμε αργότερα.

---

## Βήμα 2: Αρχικοποίηση της Μηχανής OCR

```java
import com.aspose.ocr.*;

public class MultiLangOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Create the OCR engine – the core object that does all the heavy lifting.
        OcrEngine engine = new OcrEngine();

        // Step 2.2: (Optional) Apply your license to avoid watermarks.
        // engine.setLicense("Aspose.Total.lic");
```

**Γιατί είναι σημαντικό:**  
Η `OcrEngine` περιλαμβάνει τους αλγόριθμους αναγνώρισης. Αν παραλείψετε αυτό το βήμα, δεν θα υπάρχει τίποτα για *εκτέλεση OCR στην εικόνα* αργότερα και θα αντιμετωπίσετε `NullPointerException`.

---

## Βήμα 3: Διαμόρφωση Υποστήριξης Πολλαπλών Γλωσσών και Αυτόματης Ανίχνευσης

```java
        // Step 3.1: Tell the engine which languages you expect.
        engine.setRecognitionLanguages(new String[] { "en", "uk", "ar" });

        // Step 3.2: Enable automatic language detection – crucial for mixed‑script images.
        engine.setAutoDetectLanguage(true);
```

**Εξήγηση:**  
- `"en"` = English, `"uk"` = Ukrainian, `"ar"` = Arabic.  
- Η αυτόματη ανίχνευση επιτρέπει στο Aspose να σαρώσει την εικόνα, να αποφασίσει ποια γλώσσα ανήκει σε κάθε τμήμα και να εφαρμόσει το σωστό μοντέλο OCR. Χωρίς αυτήν θα έπρεπε να εκτελέσετε τρεις ξεχωριστές αναγνώσεις—πρόσθετη δουλειά και πιθανές σφάλματα.

---

## Βήμα 4: Φόρτωση της Εικόνας για OCR

```java
        // Step 4.1: Prepare an OcrInput container.
        OcrInput input = new OcrInput();

        // Step 4.2: Add the image file. Replace the path with your actual location.
        input.add("YOUR_DIRECTORY/mixed_script.jpg");
```

> **Γιατί χρησιμοποιούμε το `OcrInput`:** Μπορεί να περιέχει πολλαπλές σελίδες ή εικόνες, δίνοντάς σας την ευελιξία να *φορτώσετε εικόνα για OCR* σε λειτουργία batch αργότερα.

Αν το αρχείο δεν βρεθεί, το Aspose ρίχνει `FileNotFoundException`. Μια γρήγορη προστασία `if (!new File(path).exists())` μπορεί να σας εξοικονομήσει χρόνο εντοπισμού σφαλμάτων.

---

## Βήμα 5: Εκτέλεση OCR στην Εικόνα

```java
        // Step 5.1: Execute the recognition process.
        OcrResult result = engine.recognize(input);
```

Σε αυτό το σημείο η μηχανή αναλύει την εικόνα, εντοπίζει τα μπλοκ γλωσσών και παράγει ένα αντικείμενο `OcrResult` που περιέχει το αναγνωρισμένο κείμενο.

---

## Βήμα 6: Εξαγωγή Κειμένου από την Εικόνα και Εμφάνιση του

```java
        // Step 6.1: Pull the plain text out of the result.
        String extractedText = result.getText();

        // Step 6.2: Print it to the console – you could also write it to a file.
        System.out.println("=== Extracted Text ===");
        System.out.println(extractedText);
    }
}
```

**Τι θα δείτε:**  
Αν το `mixed_script.jpg` περιέχει “Hello мир مرحبا”, η έξοδος στην κονσόλα θα είναι:

```
=== Extracted Text ===
Hello мир مرحبا
```

Αυτή είναι η πλήρης λύση για **πώς να χρησιμοποιήσετε το Aspose** ώστε να *εξάγετε κείμενο από εικόνα* με πολλές γλώσσες.

---

## Ακραίες Περιπτώσεις & Συχνές Ερωτήσεις

### Τι γίνεται αν μια γλώσσα δεν αναγνωρίζεται;

Το Aspose υποστηρίζει μόνο τις γλώσσες για τις οποίες διαθέτει μοντέλα OCR. Αν χρειάζεστε, π.χ., Ιαπωνικά, προσθέστε `"ja"` στο `setRecognitionLanguages`. Αν το μοντέλο δεν υπάρχει, η μηχανή επιστρέφει στην προεπιλογή (συνήθως Αγγλικά) και θα δείτε ακατάλληλους χαρακτήρες.

### Πώς να βελτιώσετε την ακρίβεια σε εικόνες χαμηλής ανάλυσης;

- Προεπεξεργασία της εικόνας (αύξηση DPI, εφαρμογή δυαδικοποίησης).  
- Χρησιμοποιήστε `engine.setResolution(300)` για να ενημερώσετε τη μηχανή για το αναμενόμενο DPI.  
- Ενεργοποιήστε `engine.setPreprocessOptions(OcrEngine.PreprocessOptions.AutoRotate)` για σκαλιστές σκαναρίσματα.

### Μπορώ να επεξεργαστώ έναν φάκελο εικόνων;

Απολύτως. Τυλίξτε την κλήση `input.add()` μέσα σε βρόχο που διατρέχει όλα τα αρχεία ενός καταλόγου. Η ίδια κλήση `engine.recognize(input)` θα επιστρέψει το ενωμένο κείμενο για κάθε σελίδα.

---

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

```java
import com.aspose.ocr.*;

public class MultiLangOcrDemo {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine
        OcrEngine engine = new OcrEngine();

        // Optional: apply your license to avoid watermarks
        // engine.setLicense("Aspose.Total.lic");

        // Configure languages (English, Ukrainian, Arabic) and enable auto‑detect
        engine.setRecognitionLanguages(new String[] { "en", "uk", "ar" });
        engine.setAutoDetectLanguage(true);

        // Load the image that contains mixed‑language text
        OcrInput input = new OcrInput();
        input.add("YOUR_DIRECTORY/mixed_script.jpg"); // <-- replace with your path

        // Run the recognition process
        OcrResult result = engine.recognize(input);

        // Print the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

Αποθηκεύστε το ως `MultiLangOcrDemo.java`, μεταγλωττίστε με `javac` και τρέξτε `java MultiLangOcrDemo`. Αν όλα είναι ρυθμισμένα σωστά, θα δείτε το αναγνωρισμένο κείμενο στην κονσόλα.

---

## Συμπέρασμα

Καλύψαμε **πώς να χρησιμοποιήσετε το Aspose** από την αρχή μέχρι το τέλος: από την προσθήκη της βιβλιοθήκης, τη διαμόρφωση του *OCR πολλαπλών γλωσσών*, μέχρι το **φόρτωμα εικόνας για OCR**, την **εκτέλεση OCR στην εικόνα** και τελικά την **εξαγωγή κειμένου από εικόνα**. Η προσέγγιση κλιμακώνεται—απλώς προσθέστε περισσότερους κωδικούς γλώσσας ή μια λίστα αρχείων και θα έχετε μια ισχυρή γραμμή OCR σε λίγα λεπτά.

Τι ακολουθεί; Δοκιμάστε τις παρακάτω ιδέες:

- **Επεξεργασία σε παρτίδες:** Επανάληψη σε έναν φάκελο και αποθήκευση κάθε αποτελέσματος σε ξεχωριστό αρχείο `.txt`.  
- **Μετα‑επεξεργασία:** Χρησιμοποιήστε regex ή βιβλιοθήκες NLP για να καθαρίσετε την έξοδο (αφαίρεση περιττών αλλαγών γραμμής, διόρθωση κοινών σφαλμάτων OCR).  
- **Ενσωμάτωση:** Συνδέστε το βήμα OCR σε ένα endpoint REST Spring Boot ώστε άλλες υπηρεσίες να στέλνουν εικόνες και να λαμβάνουν κείμενο σε μορφή JSON.

Νιώστε ελεύθεροι να πειραματιστείτε, να σπάσετε πράγματα και μετά να τα διορθώσετε—αυτή είναι η πραγματική μάθηση του OCR με το Aspose. Αν αντιμετωπίσετε δυσκολίες, αφήστε ένα σχόλιο παρακάτω. Καλό κώδικα!  

---

![how to use aspose OCR screenshot](/images/aspose-ocr-demo.png){alt="παράδειγμα χρήσης aspose OCR που δείχνει κώδικα Java"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}