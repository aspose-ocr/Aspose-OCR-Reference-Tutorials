---
category: general
date: 2026-10-24
description: Μάθετε πώς να εξάγετε κείμενο από εικόνα χρησιμοποιώντας Aspose OCR σε
  Java, υποστηρίζοντας Αγγλικά, Ουκρανικά και Αραβικά. Οδηγός βήμα προς βήμα για τη
  φόρτωση της εικόνας για OCR και την εκτέλεση OCR στην εικόνα.
draft: false
keywords:
- extract text from image
- load image for ocr
- run ocr on image
- Aspose OCR Java
- multi language OCR
lastmod: 2026-10-24
og_description: Μάθετε πώς να εξάγετε κείμενο από εικόνα χρησιμοποιώντας Aspose OCR
  σε Java, υποστηρίζοντας Αγγλικά, Ουκρανικά και Αραβικά. Βήματα για τη φόρτωση της
  εικόνας για OCR και την εκτέλεση OCR στην εικόνα.
og_image_alt: 'Developer guide: extract text from image using Aspose OCR in Java'
og_title: Πώς να εξάγετε κείμενο από εικόνα με Aspose OCR σε Java
schemas:
- author: Aspose
  dateModified: '2026-10-24'
  description: Learn how to extract text from image using Aspose OCR in Java, supporting
    English, Ukrainian and Arabic. Step‑by‑step guide to load image for OCR and run
    OCR on image.
  headline: How to extract text from image with Aspose OCR in Java
  type: TechArticle
- questions:
  - answer: No, a single Aspose OCR license covers all bundled language packs.
    question: Do I need a separate license for each language pack?
  - answer: The only practical limit is memory; Aspose processes each image sequentially,
      so you can add hundreds of files without issue.
    question: Is there a limit on the number of images I can add to `OcrInput`?
  - answer: The engine analyses each text block independently, so it can switch languages
      mid‑line and still produce accurate results.
    question: How does auto‑detection handle mixed scripts on the same line?
  - answer: Yes, `OcrResult` provides a `getConfidence()` method for granular quality
      metrics.
    question: Can I get confidence scores for each recognized word?
  - answer: Aspose OCR works with Java 8 through Java 21, including LTS releases.
    question: What Java versions are supported?
  type: FAQPage
tags:
- Aspose
- OCR
- Java
- extract text from image
- multi language OCR
title: Πώς να εξάγετε κείμενο από εικόνα με Aspose OCR σε Java
url: /el/java/advanced-ocr-techniques/how-to-use-aspose-for-multi-language-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εξάγετε κείμενο από εικόνα με το Aspose OCR σε Java

Αν χρειάζεστε **εξαγωγή κειμένου από εικόνα** αρχεία που περιέχουν ένα μείγμα αγγλικών, ουκρανικών και αραβικών χαρακτήρων, το Aspose OCR το καθιστά απλό. Σε αυτό το tutorial θα δείτε ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που δείχνει πώς να **φορτώσετε εικόνα για OCR**, ενεργοποιήσετε *πολυγλωσσικό OCR*, και τελικά **εκτελέσετε OCR στην εικόνα** για να λάβετε καθαρό, αναγνώσιμο κείμενο. Τα βήματα εξηγούνται με απλή γλώσσα, ώστε να κατανοείτε τόσο *τι* πρέπει να κάνετε όσο και *γιατί* είναι σημαντικό.

## Γρήγορες απαντήσεις
- **Ποια είναι η πρώτη γραμμή κώδικα;** `OcrEngine engine = new OcrEngine();`
- **Ποιες γλώσσες υποστηρίζονται έτοιμες προς χρήση;** English (`en`), Ukrainian (`uk`), Arabic (`ar`) and 27 additional languages.
- **Χρειάζομαι άδεια για δοκιμή;** No, a free trial works, but a license removes the watermark.
- **Μπορώ να επεξεργαστώ πολλές εικόνες ταυτόχρονα;** Yes, use `OcrInput` to add several files before calling `recognize`.
- **Ποια έκδοση Java απαιτείται;** Java 8 or newer.

## Πώς να εξάγετε κείμενο από εικόνα χρησιμοποιώντας το Aspose OCR σε Java;
Φορτώστε την εικόνα σας με `OcrInput`, ρυθμίστε το `OcrEngine` για τις απαιτούμενες γλώσσες, και καλέστε `engine.recognize(input)`. Η μηχανή ανιχνεύει αυτόματα τα μπλοκ γλώσσας, εφαρμόζει το σωστό μοντέλο OCR, και επιστρέφει ένα `OcrResult` που περιέχει το αναγνωρισμένο κείμενο. Αυτή η ροή ενός βήματος λειτουργεί για οποιοδήποτε μέγεθος εικόνας έως 10 000 × 10 000 pixel και υποστηρίζει πάνω από 30 πακέτα γλώσσας.

## Τι θα μάθετε
- Προσθέστε τη βιβλιοθήκη Aspose OCR σε ένα έργο Java (Maven ή Gradle).  
- Αρχικοποιήστε σωστά τη μηχανή OCR.  
- Ρυθμίστε τη μηχανή για *πολυγλωσσικό OCR* και ενεργοποιήστε την αυτόματη ανίχνευση.  
- Φορτώστε μια εικόνα που περιέχει μεικτά σενάρια.  
- Εκτελέστε την αναγνώριση και **εξάγετε κείμενο από εικόνα**.  
- Αντιμετωπίστε κοινά προβλήματα όπως μη υποστηριζόμενες γλώσσες ή ελλιπή αρχεία.

Στο τέλος θα έχετε μια αυτόνομη κλάση Java που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο και να ξεκινήσετε αμέσως την επεξεργασία εικόνων.

## Προαπαιτούμενα

| Απαίτηση | Γιατί είναι σημαντικό |
|-------------|----------------|
| Java 8 ή νεότερη | Το Aspose OCR στοχεύει σε Java 8+. |
| Maven ή Gradle (οποιοδήποτε εργαλείο κατασκευής) | Κατεβάζει αυτόματα το JAR του Aspose OCR. |
| Ένα αρχείο εικόνας με κείμενο μεικτής γλώσσας (π.χ., `mixed_script.jpg`) | Αυτό είναι που θα **φορτώσουμε εικόνα για OCR**. |
| Μία έγκυρη άδεια Aspose OCR (προαιρετική) | Χωρίς άδεια λαμβάνετε έξοδο με υδατογράφημα, αλλά ο κώδικας λειτουργεί το ίδιο. |

Το έχετε όλα; Τέλεια—ας ξεκινήσουμε.

## Βήμα 1: προσθέστε το Aspose OCR στο έργο σας

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

> **Συμβουλή:** Το Aspose OCR υποστηρίζει πάνω από 30 πακέτα γλώσσας και μπορεί να επεξεργαστεί εικόνες έως 10 000 × 10 000 pixel χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη, ώστε να μπορείτε να διαχειρίζεστε αποδοτικά σαρώσεις υψηλής ανάλυσης.

Η προσθήκη της εξάρτησης είναι το πρώτο συγκεκριμένο βήμα στο **πώς να χρησιμοποιήσετε το Aspose**—η βιβλιοθήκη φέρνει τις κλάσεις `OcrEngine`, `OcrInput` και `OcrResult` που θα χρειαστούμε αργότερα.

## Βήμα 2: αρχικοποιήστε τη μηχανή OCR

Η κλάση `OcrEngine` είναι το βασικό στοιχείο του Aspose OCR που εκτελεί τη διαδικασία αναγνώρισης.  

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
Αν παραλείψετε την αρχικοποίηση της μηχανής, δεν θα υπάρχει τίποτα για *εκτέλεση OCR στην εικόνα* αργότερα, και θα αντιμετωπίσετε ένα `NullPointerException`.

## Βήμα 3: ρυθμίστε την υποστήριξη πολυγλωσσικότητας και την αυτόματη ανίχνευση

`OcrEngine` παρέχει τη μέθοδο `setRecognitionLanguages` για να καθορίσετε ποια μοντέλα γλώσσας θα φορτωθούν, και το `setAutoDetectLanguage` ενεργοποιεί την αυτόματη ανίχνευση γλώσσας ανά μπλοκ κειμένου.  

```java
        // Step 3.1: Tell the engine which languages you expect.
        engine.setRecognitionLanguages(new String[] { "en", "uk", "ar" });

        // Step 3.2: Enable automatic language detection – crucial for mixed‑script images.
        engine.setAutoDetectLanguage(true);
```

**Εξήγηση:**  
- `"en"` = English, `"uk"` = Ukrainian, `"ar"` = Arabic.  
- Η αυτόματη ανίχνευση επιτρέπει στο Aspose να σαρώσει την εικόνα, να αποφασίσει σε ποια γλώσσα ανήκει κάθε τμήμα, και να εφαρμόσει το σωστό μοντέλο OCR. Χωρίς αυτήν θα έπρεπε να εκτελέσετε τρεις ξεχωριστές αναγνωρίσεις—πρόσφορο και επιρρεπές σε σφάλματα.

## Βήμα 4: φορτώστε την εικόνα για OCR

`OcrInput` είναι το κοντέινερ του Aspose OCR που κρατά ένα ή περισσότερα ρεύματα εικόνας για επεξεργασία.  

```java
        // Step 4.1: Prepare an OcrInput container.
        OcrInput input = new OcrInput();

        // Step 4.2: Add the image file. Replace the path with your actual location.
        input.add("YOUR_DIRECTORY/mixed_script.jpg");
```

> **Γιατί χρησιμοποιούμε το `OcrInput`:** Μπορεί να κρατήσει πολλαπλές σελίδες ή εικόνες, δίνοντάς σας την ευελιξία να **φορτώσετε εικόνα για OCR** σε λειτουργία batch αργότερα. Αν το αρχείο δεν βρεθεί, το Aspose ρίχνει ένα `FileNotFoundException`. Μια γρήγορη προστασία (`if (!new File(path).exists())`) εξοικονομεί χρόνο εντοπισμού σφαλμάτων.

## Βήμα 5: εκτελέστε OCR στην εικόνα

Η μέθοδος `recognize` αναλύει την εικόνα, εντοπίζει τα μπλοκ γλώσσας, και παράγει ένα αντικείμενο `OcrResult` που περιέχει το αναγνωρισμένο κείμενο.  

```java
        // Step 5.1: Execute the recognition process.
        OcrResult result = engine.recognize(input);
```

## Βήμα 6: εξάγετε κείμενο από την εικόνα και εμφανίστε το

`OcrResult` περιλαμβάνει την τελική έξοδο κειμένου, συμπεριλαμβανομένων των αλλαγών γραμμής και των βαθμών εμπιστοσύνης.  

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

Αυτή είναι η πλήρης λύση για **πώς να χρησιμοποιήσετε το Aspose** για **εξαγωγή κειμένου από εικόνα** με πολλαπλές γλώσσες.

## Ακραίες περιπτώσεις & συχνές ερωτήσεις

### Τι γίνεται αν μια γλώσσα δεν αναγνωρίζεται;
Το Aspose υποστηρίζει μόνο γλώσσες για τις οποίες παρέχει μοντέλα OCR. Για να προσθέσετε Ιαπωνικά, συμπεριλάβετε `"ja"` στο `setRecognitionLanguages`. Αν το μοντέλο δεν υπάρχει, η μηχανή επιστρέφει στην προεπιλογή (English) και θα λάβετε ακατάλληλους χαρακτήρες.

### Πώς να βελτιώσετε την ακρίβεια σε εικόνες χαμηλής ανάλυσης;
`setResolution` ορίζει την τιμή DPI που υποθέτει η μηχανή για την εικόνα εισόδου, κάτι που βοηθά σε σαρώσεις χαμηλής ανάλυσης.  
`setPreprocessOptions` επιλέγει ενέργειες προεπεξεργασίας όπως η αυτόματη περιστροφή πριν το OCR.  

- Προεπεξεργαστείτε την εικόνα (αυξήστε το DPI, εφαρμόστε δυαδικοποίηση).  
- Χρησιμοποιήστε `engine.setResolution(300)` για να ενημερώσετε τη μηχανή για το αναμενόμενο DPI.  
- Ενεργοποιήστε `engine.setPreprocessOptions(OcrEngine.PreprocessOptions.AutoRotate)` για περιστρεφόμενες σαρώσεις.

### Μπορώ να επεξεργαστώ έναν φάκελο εικόνων;
Απολύτως. Τυλίξτε την κλήση `input.add()` σε έναν βρόχο που διατρέχει όλα τα αρχεία σε έναν φάκελο. Η ίδια κλήση `engine.recognize(input)` θα επιστρέψει το ενωμένο κείμενο για κάθε σελίδα.

## Πλήρες λειτουργικό παράδειγμα (έτοιμο για αντιγραφή‑επικόλληση)

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

Αποθηκεύστε το ως `MultiLangOcrDemo.java`, μεταγλωττίστε με `javac`, και εκτελέστε `java MultiLangOcrDemo`. Αν όλα είναι ρυθμισμένα σωστά, θα δείτε το αναγνωρισμένο κείμενο να εκτυπώνεται στην κονσόλα.

## Συχνές ερωτήσεις

**Q: Χρειάζομαι ξεχωριστή άδεια για κάθε πακέτο γλώσσας;**  
A: Όχι, μια μόνο άδεια Aspose OCR καλύπτει όλα τα ενσωματωμένα πακέτα γλώσσας.

**Q: Υπάρχει όριο στον αριθμό των εικόνων που μπορώ να προσθέσω στο `OcrInput`;**  
A: Το μόνο πρακτικό όριο είναι η μνήμη· το Aspose επεξεργάζεται κάθε εικόνα διαδοχικά, έτσι μπορείτε να προσθέσετε εκατοντάδες αρχεία χωρίς πρόβλημα.

**Q: Πώς η αυτόματη ανίχνευση διαχειρίζεται μεικτά σενάρια στην ίδια γραμμή;**  
A: Η μηχανή αναλύει κάθε μπλοκ κειμένου ανεξάρτητα, έτσι μπορεί να αλλάξει γλώσσες μέσα στη γραμμή και να παραγάγει ακριβή αποτελέσματα.

**Q: Μπορώ να λάβω βαθμούς εμπιστοσύνης για κάθε αναγνωρισμένη λέξη;**  
A: Ναι, το `OcrResult` παρέχει τη μέθοδο `getConfidence()` για λεπτομερή μετρική ποιότητας.

**Q: Ποιες εκδόσεις Java υποστηρίζονται;**  
A: Το Aspose OCR λειτουργεί με Java 8 έως Java 21, συμπεριλαμβανομένων των εκδόσεων LTS.

## Συμπέρασμα

Έχουμε καλύψει **πώς να χρησιμοποιήσετε το Aspose** από την αρχή μέχρι το τέλος: από την προσθήκη της βιβλιοθήκης, μέσω της ρύθμισης του *πολυγλωσσικού OCR*, μέχρι **φόρτωση εικόνας για OCR**, **εκτέλεση OCR στην εικόνα**, και τελικά **εξαγωγή κειμένου από εικόνα**. Η προσέγγιση κλιμακώνεται—απλώς προσθέστε περισσότερους κωδικούς γλώσσας ή δώστε μια λίστα αρχείων, και θα έχετε μια ισχυρή γραμμή OCR σε λίγα λεπτά.

Τι ακολουθεί; Δοκιμάστε αυτές τις ιδέες:

- **Επεξεργασία παρτίδας:** Επανάληψη σε έναν φάκελο και εγγραφή κάθε αποτελέσματος σε ξεχωριστό αρχείο `.txt`.  
- **Μετα‑επεξεργασία:** Χρησιμοποιήστε regex ή βιβλιοθήκες NLP για να καθαρίσετε την έξοδο (αφαιρέστε περιττές αλλαγές γραμμής, διορθώστε κοινά σφάλματα OCR).  
- **Ενσωμάτωση:** Εκθέστε το βήμα OCR μέσω ενός Spring Boot REST endpoint ώστε άλλες υπηρεσίες να μπορούν να υποβάλουν εικόνες και να λαμβάνουν κείμενο κωδικοποιημένο σε JSON.

Μη διστάσετε να πειραματιστείτε, να σπάσετε πράγματα, και μετά να τα διορθώσετε—αυτή είναι η πραγματική εξοικείωση με το OCR μέσω Aspose. Αν αντιμετωπίσατε προβλήματα, αφήστε ένα σχόλιο παρακάτω. Καλή προγραμματιστική!  

---

![πώς να χρησιμοποιήσετε το aspose OCR screenshot](/images/aspose-ocr-demo.png){alt="παράδειγμα χρήσης aspose OCR που δείχνει κώδικα Java"}

[πώς να χρησιμοποιήσετε το aspose OCR screenshot](/images/aspose-ocr-demo.png)

**Τελευταία ενημέρωση:** 2026-10-24  
**Δοκιμάστηκε με:** Aspose OCR 24.11 for Java  
**Συγγραφέας:** Aspose

## Σχετικά μαθήματα

- [Φόρτωση εικόνας για OCR σε Java – Οδηγός βήμα προς βήμα](/ocr/java/ocr-operations/load-image-for-ocr-in-java-step-by-step-guide/)
- [Αυτόματη ανίχνευση γλώσσας σε OCR Java – Οδηγός βήμα προς βήμα](/ocr/java/advanced-ocr-techniques/automatic-language-detection-in-java-ocr-step-by-step-guide/)
- [Πώς να ενεργοποιήσετε GPU για OCR σε Java – Εξαγωγή κειμένου από εικόνα](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}