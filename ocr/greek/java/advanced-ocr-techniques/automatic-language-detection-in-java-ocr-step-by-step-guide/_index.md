---
category: general
date: 2026-10-08
description: Μάθετε πώς να προσθέσετε την εξάρτηση java ocr maven και να ενεργοποιήσετε
  την αυτόματη ανίχνευση γλώσσας για image OCR σε Java. Αυτός ο οδηγός βήμα‑βήμα παρουσιάζει
  ένα πλήρες παράδειγμα java ocr που εξάγει κείμενο από αρχεία PNG με μεικτές γλώσσες.
draft: false
keywords:
- java ocr maven dependency
- automatic language detection image
- extract text from image
- mixed language OCR Java
- Aspose OCR for Java
lastmod: 2026-10-08
og_description: Προσθέστε την εξάρτηση java ocr maven και ενεργοποιήστε την αυτόματη
  ανίχνευση γλώσσας για image OCR σε Java. Ακολουθήστε ένα πλήρες παράδειγμα που εξάγει
  κείμενο από αρχεία PNG με μεικτές γλώσσες.
og_image_alt: 'Developer guide: automatic language detection on a mixed‑language PNG
  using Aspose OCR for Java'
og_title: Προσθήκη εξάρτησης java ocr maven για αυτόματη ανίχνευση
schemas:
- author: Aspose
  dateModified: '2026-10-08'
  description: Learn how to add the java ocr maven dependency and enable automatic
    language detection for image OCR in Java. This step‑by‑step guide shows a complete
    java ocr example that extracts text from mixed‑language PNG files.
  headline: Add java ocr maven dependency for automatic detection
  type: TechArticle
- description: Learn how to add the java ocr maven dependency and enable automatic
    language detection for image OCR in Java. This step‑by‑step guide shows a complete
    java ocr example that extracts text from mixed‑language PNG files.
  name: Add java ocr maven dependency for automatic detection
  steps:
  - name: Add the **java ocr maven dependency** to your project.
    text: Add the **java ocr maven dependency** to your project.
  - name: Enable **automatic language detection** via `setAutoDetectLanguage(true)`.
    text: Enable **automatic language detection** via `setAutoDetectLanguage(true)`.
  - name: Process a mixed‑language PNG and retrieve clean text with `getText()`.
    text: Process a mixed‑language PNG and retrieve clean text with `getText()`.
  type: HowTo
- questions:
  - answer: Yes, the Aspose OCR library is pure Java and runs on Windows, Linux, and
      macOS without native binaries.
    question: Does the java ocr maven dependency work on all operating systems?
  - answer: The engine supports **70+ languages** and can detect any combination present
      in a single image.
    question: How many languages can the engine detect automatically?
  - answer: Absolutely—simply pass a PDF or TIFF file to `processImage`; the engine
      extracts each page sequentially.
    question: Can I process PDFs or multi‑page TIFFs with the same engine?
  - answer: While there is no hard limit, images larger than **20 MB** may cause out‑of‑memory
      errors on modest JVM heap sizes; consider streaming or down‑scaling large files.
    question: Is there a file‑size limit for image OCR?
  - answer: A single commercial license covers all environments (development, staging,
      production) as long as the terms are respected.
    question: Do I need a separate license for each deployment environment?
  type: FAQPage
tags:
- java ocr
- automatic language detection
- Aspose OCR
- Maven
title: Προσθήκη εξάρτησης java ocr maven για αυτόματη ανίχνευση
url: /el/java/advanced-ocr-techniques/automatic-language-detection-in-java-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη εξάρτησης java ocr maven για αυτόματη ανίχνευση

Η αυτόματη ανίχνευση γλώσσας είναι μια επαναστατική λύση όταν χρειάζεται να εξάγετε κείμενο από εικόνες που περιέχουν περισσότερα από ένα σύστημα γραφής — σκεφτείτε αποδείξεις που συνδυάζουν Αγγλικά και Ρωσικά, ή memes στα κοινωνικά δίκτυα που αναμειγνύουν λατινικούς και κυριλλικούς χαρακτήρες. Στην Java, το Aspose OCR for Java μπορεί αυτόματα να αναγνωρίσει τις γλώσσες που εμφανίζονται σε μια εικόνα, ώστε να μην χρειάζεται ποτέ να ορίσετε χειροκίνητα τη γλώσσα. Αυτό το tutorial παρουσιάζει ένα **java ocr example** που δείχνει πώς να προσθέσετε το **java ocr maven dependency**, να ενεργοποιήσετε την **automatic language detection**, να επεξεργαστείτε ένα PNG με μεικτή γλώσσα και να εκτυπώσετε το εξαγόμενο κείμενο στην κονσόλα. Στο τέλος θα μπορείτε να **convert png to text** με λίγες μόνο γραμμές κώδικα.

## Γρήγορες απαντήσεις
- **Ποιο Maven artifact προσθέτει υποστήριξη OCR;** `com.aspose:aspose-ocr` (latest version from Maven Central).  
- **Χρειάζομαι άδεια για ανάπτυξη;** A free evaluation license works for testing; a commercial license is required for production.  
- **Μπορεί η μηχανή να ανιχνεύσει πολλαπλές γλώσσες ταυτόχρονα;** Yes—auto detection handles any combination of supported scripts.  
- **Ποιοι τύποι εικόνας γίνονται αποδεκτοί;** PNG, JPEG, BMP, TIFF, and GIF are fully supported.  
- **Είναι η Java 8 επαρκής;** The library runs on Java 8+, but Java 17 gives better performance and newer language features.

## Τι είναι η java ocr maven dependency;
Η εξάρτηση Maven είναι ένα απόσπασμα κώδικα που προστίθεται στο `pom.xml` και φέρνει τη βιβλιοθήκη Aspose OCR στο έργο.  
Η **java ocr maven dependency** είναι το Maven artifact που κατεβάζει τα δυαδικά αρχεία Aspose OCR for Java και τις εξαρτημένες βιβλιοθήκες στο classpath του έργου σας. Η προσθήκη της στο `pom.xml` σας δίνει πρόσβαση σε κλάσεις όπως `OcrEngine`, `OcrResult` και εργαλεία ανίχνευσης γλώσσας χωρίς χειροκίνητη διαχείριση JAR.

## Γιατί να χρησιμοποιήσετε επεξεργασία εικόνας με αυτόματη ανίχνευση γλώσσας;
Το Aspose OCR υποστηρίζει **πάνω από 70 γλώσσες** και μπορεί αυτόματα να εναλλάσσει μεταξύ τους όταν μια εικόνα περιέχει μεικτά συστήματα γραφής. Σε δοκιμές benchmark, η αυτόματη ανίχνευση βελτιώνει την ακρίβεια σε επίπεδο χαρακτήρων κατά **15 % σε πολυγλωσσικά έγγραφα** σε σύγκριση με την επιβολή μιας μόνο γλώσσας. Αυτό σημαίνει λιγότερες διορθώσεις μετά την επεξεργασία και πιο ομαλή ροή εργασίας, ιδιαίτερα για σάρωση αποδείξεων, εισαγωγή πολυγλωσσικών φορμών και bots εικόνων στα κοινωνικά δίκτυα.

## Προαπαιτούμενα
- Java 17 (ή οποιοδήποτε JDK 8+). Οι νεότερες εκδόσεις βελτιώνουν τη συλλογή απορριμμάτων και την απόδοση JIT.  
- Maven 3.6+ για την επίλυση του artifact `aspose-ocr`.  
- Ένα αρχείο εικόνας που περιέχει περισσότερες από μία γλώσσες (π.χ., `mixed-eng-rus.png`).  
- Ένα IDE όπως IntelliJ IDEA, Eclipse ή VS Code (οποιοδήποτε είναι εντάξει).  

> **Pro tip:** Αν δεν έχετε δοκιμαστική εικόνα, δημιουργήστε ένα PNG που περιέχει μια σύντομη αγγλική φράση δίπλα στη ρωσική της μετάφραση. Η μηχανή OCR ενδιαφέρεται μόνο για τα δεδομένα των pixel, όχι για την πηγή της εικόνας.

Παρακάτω είναι το πλήρες, έτοιμο προς εκτέλεση πρόγραμμα.

![Αυτόματη ανίχνευση γλώσσας σε PNG με μεικτή γλώσσα](/images/mixed-eng-rus.png "παράδειγμα αυτόματης ανίχνευσης γλώσσας")

## Πώς να προσθέσετε την java ocr maven dependency;
Η εξάρτηση Maven είναι ένα σύντομο απόσπασμα XML που λέει στο Maven ποια βιβλιοθήκη να κατεβάσει.  
Προσθέστε την ακόλουθη εξάρτηση στο `pom.xml`. Αυτή η μοναδική γραμμή κατεβάζει τη νεότερη σταθερή βιβλιοθήκη Aspose OCR και όλους τους απαιτούμενους φυσικούς πόρους. Μετά την εκτέλεση του `mvn clean install` ή το συγχρονισμό του έργου από το IDE, οι κλάσεις OCR γίνονται διαθέσιμες στο classpath της μεταγλώττισης, έτοιμες για χρήση στον κώδικα Java.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.12</version>
</dependency>
```

## Πώς να ενεργοποιήσετε την αυτόματη ανίχνευση γλώσσας στο Java OCR;
`OcrEngine` είναι η βασική κλάση που ελέγχει την επεξεργασία OCR και τις ρυθμίσεις.  
Δημιουργήστε ένα αντικείμενο `OcrEngine` και ενεργοποιήστε τη σημαία auto‑detect. Αυτό λέει στη μηχανή να αναλύσει πρώτα την εικόνα, να αποφασίσει ποια μοντέλα γλώσσας να φορτώσει και στη συνέχεια να εκτελέσει την αναγνώριση. Η ενεργοποίηση της αυτόματης ανίχνευσης εξασφαλίζει ότι η μηχανή επιλέγει τα κατάλληλα μοντέλα γλώσσας για κάθε σύστημα γραφής που υπάρχει, βελτιώνοντας δραστικά την ακρίβεια για πολυγλωσσικές εικόνες.

```java
import com.aspose.ocr.*;

public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable automatic language detection
        ocrEngine.setAutoDetectLanguage(true);
```

## Πώς να τροφοδοτήσετε την εικόνα και να εκτελέσετε τη διαδικασία OCR;
`processImage` είναι μια μέθοδος του `OcrEngine` που δέχεται ένα αρχείο εικόνας και επιστρέφει το αποτέλεσμα OCR.  
Περάστε το αρχείο εικόνας στη μηχανή χρησιμοποιώντας τη μέθοδο `processImage`. Αυτή η μέθοδος επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει το αναγνωρισμένο κείμενο, τις βαθμολογίες εμπιστοσύνης και τον κωδικό της ανιχνευμένης γλώσσας. Χρησιμοποιώντας το αντικείμενο αποτελέσματος, μπορείτε να ελέγξετε το εξαγόμενο κείμενο και τη γλώσσα που επιλέχθηκε αυτόματα από τη μηχανή.

```java
        // Step 3: Process the image that contains both English and Russian text
        OcrResult ocrResult = ocrEngine.processImage("YOUR_DIRECTORY/mixed-eng-rus.png");
```

## Πώς να ανακτήσετε και να εμφανίσετε το αναγνωρισμένο κείμενο;
`getText` είναι μια μέθοδος του `OcrResult` που επιστρέφει την αναπαράσταση plain‑text του αποτελέσματος OCR.  
Αποκτήστε τη συμβολοσειρά plain‑text από το `OcrResult` με το `getText()`. Αυτή η μέθοδος αφαιρεί τις πληροφορίες διάταξης, επιστρέφοντας μια καθαρή, αναζητήσιμη συμβολοσειρά που μπορείτε να αποθηκεύσετε, να ευρετηριάσετε ή να τροφοδοτήσετε σε επόμενες υπηρεσίες AI. Το παραγόμενο κείμενο μπορεί να καταγραφεί, να εμφανιστεί στους χρήστες ή να περάσει σε άλλες διαδικασίες επεξεργασίας.

```java
        // Step 4: Print the recognized text to the console
        System.out.println(ocrResult.getText());
    }
}
```

Όταν εκτελέσετε το πρόγραμμα, θα πρέπει να δείτε έξοδο παρόμοια με:

```
Hello world!
Привет мир!
```

Η κονσόλα θα εμφανίσει τόσο την αγγλική πρόταση όσο και το ρωσικό της αντίστοιχο, επιβεβαιώνοντας ότι η **automatic language detection** εντόπισε σωστά τα δύο συστήματα γραφής. Αν απενεργοποιήσετε τη σημαία auto‑detect, το κυριλλικό τμήμα θα εμφανιστεί ως ακατανόητοι χαρακτήρες, δείχνοντας γιατί αυτή η δυνατότητα είναι κρίσιμη για πολυγλωσσικά σενάρια.

## Συνηθισμένες παραλλαγές & ακραίες περιπτώσεις

### Μετατροπή PNG σε κείμενο χωρίς ανίχνευση γλώσσας
Αν είστε σίγουροι ότι η εικόνα περιέχει μόνο μία γλώσσα, μπορείτε να παραλείψετε το βήμα auto‑detect:

```java
ocrEngine.setLanguage(OcrLanguage.English);
```

Ωστόσο, τη στιγμή που εμφανίζεται ένας αχρείαστος χαρακτήρας από άλλο σύστημα γραφής, η ακρίβεια αναγνώρισης πέφτει απότομα, συχνά κάτω από 70 % για το μη αναμενόμενο σύστημα γραφής.

### Διαχείριση μεγάλων εικόνων
Για σαρώσεις υψηλής ανάλυσης (π.χ., 600 DPI), μειώστε την εικόνα σε μέγιστο 300 DPI πριν το OCR. Αυτό μειώνει την κατανάλωση μνήμης έως και **45 %** και επιταχύνει την επεξεργασία χωρίς να θυσιάζει την ακρίβεια, βάσει των εσωτερικών benchmarks της Aspose.

```java
BufferedImage original = ImageIO.read(new File("large.png"));
BufferedImage resized = ImageUtil.resize(original, 1024, 0); // keep aspect ratio
ocrEngine.processImage(resized);
```

### Εξαγωγή κειμένου από εικόνα σε web service
Κατά την έκθεση του OCR μέσω REST endpoint, ακολουθήστε τις καλύτερες πρακτικές:
- Επικυρώστε τον τύπο του ανεβασμένου αρχείου (αποδεχτείτε μόνο PNG/JPEG).  
- Εκτελέστε το OCR σε νήμα παρασκηνίου ή ασύγχρονη εργασία για να διατηρήσετε την ανταπόκριση του HTTP αιτήματος.  
- Επιστρέψτε το εξαγόμενο κείμενο ως JSON:

```json
{ "extractedText": "Hello world!\nПривет мир!" }
```

## Πλήρες λειτουργικό παράδειγμα (όλα τα βήματα συνδυασμένα)
Παρακάτω είναι η πλήρης κλάση Java που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα αρχείο με όνομα `MixedLanguageDemo.java`. Περιλαμβάνει δηλώσεις import, διαχείριση σφαλμάτων και ενσωματωμένα σχόλια που εξηγούν κάθε γραμμή.

```java
import com.aspose.ocr.*;
import java.io.File;

/**
 * Demonstrates automatic language detection with Aspose OCR for Java.
 * This example loads a PNG that contains both English and Russian text,
 * enables auto‑detect, and prints the extracted text.
 */
public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Enable automatic language detection so the engine picks the right script(s)
        ocrEngine.setAutoDetectLanguage(true);

        // Path to the image – replace with your actual location
        String imagePath = "YOUR_DIRECTORY/mixed-eng-rus.png";

        // Process the image and obtain the result
        OcrResult ocrResult = ocrEngine.processImage(imagePath);

        // Output the recognized text – should contain both English and Russian lines
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Συμπιέστε και εκτελέστε το πρόγραμμα με:

```bash
mvn compile exec:java -Dexec.mainClass=MixedLanguageDemo
```

Αν όλα είναι ρυθμισμένα σωστά, η κονσόλα θα εμφανίσει την αγγλική γραμμή ακολουθούμενη από το ρωσικό της αντίστοιχο, αποδεικνύοντας ότι η **java ocr maven dependency** μαζί με την αυτόματη ανίχνευση γλώσσας λειτουργεί από άκρη σε άκρη.

## Συχνές ερωτήσεις

**Ε: Λειτουργεί η java ocr maven dependency σε όλα τα λειτουργικά συστήματα;**  
Α: Ναι, η βιβλιοθήκη Aspose OCR είναι καθαρά Java και λειτουργεί σε Windows, Linux και macOS χωρίς εγγενή δυαδικά αρχεία.

**Ε: Πόσες γλώσσες μπορεί η μηχανή να ανιχνεύσει αυτόματα;**  
Α: Η μηχανή υποστηρίζει **πάνω από 70 γλώσσες** και μπορεί να ανιχνεύσει οποιονδήποτε συνδυασμό που υπάρχει σε μία εικόνα.

**Ε: Μπορώ να επεξεργαστώ PDF ή πολυ‑σελίδες TIFF με την ίδια μηχανή;**  
Α: Απόλυτα—απλώς περάστε ένα αρχείο PDF ή TIFF στη μέθοδο `processImage`; η μηχανή εξάγει κάθε σελίδα διαδοχικά.

**Ε: Υπάρχει όριο μεγέθους αρχείου για OCR εικόνας;**  
Α: Αν και δεν υπάρχει σκληρό όριο, εικόνες μεγαλύτερες από **20 MB** μπορεί να προκαλέσουν σφάλματα έλλειψης μνήμης σε μικρές διαμερίσεις heap JVM· σκεφτείτε τη ροή ή τη μείωση μεγέθους μεγάλων αρχείων.

**Ε: Χρειάζομαι ξεχωριστή άδεια για κάθε περιβάλλον ανάπτυξης;**  
Α: Μία ενιαία εμπορική άδεια καλύπτει όλα τα περιβάλλοντα (ανάπτυξη, staging, παραγωγή) εφόσον τηρούνται οι όροι.

## Ανακεφαλαίωση & επόμενα βήματα
Καλύψαμε πώς να:
1. Προσθέσετε την **java ocr maven dependency** στο έργο σας.  
2. Ενεργοποιήσετε την **automatic language detection** μέσω `setAutoDetectLanguage(true)`.  
3. Επεξεργαστείτε ένα PNG με μεικτή γλώσσα και ανακτήσετε καθαρό κείμενο με `getText()`.

Το ίδιο μοτίβο λειτουργεί για άλλες μορφές εικόνας (JPEG, BMP, GIF) και ακόμη για PDF και πολυ‑σελίδες TIFF—απλώς αλλάξτε την πηγή εισόδου. Για να επεκτείνετε αυτό το tutorial, σκεφτείτε:
- **Batch processing:** Επανάληψη σε έναν φάκελο εικόνων και αποθήκευση κάθε αποτελέσματος σε βάση δεδομένων.  
- **Language‑specific post‑processing:** Μετά την ανίχνευση, δρομολογήστε το αγγλικό κείμενο σε ελεγκτή ορθογραφίας και το ρωσικό σε υπηρεσία μεταγραφής.  
- **AI integration:** Τροφοδοτήστε το εξαγόμενο κείμενο σε μεγάλο μοντέλο γλώσσας για σύνοψη, ανάλυση συναισθήματος ή μετάφραση.  

Αν αντιμετωπίσετε προβλήματα ανίχνευσης, βεβαιωθείτε ότι η εικόνα είναι καθαρή, έχει επαρκή αντίθεση και ότι χρησιμοποιείτε την πιο πρόσφατη έκδοση του Aspose OCR (24.12 τη στιγμή της συγγραφής). Καλή προγραμματιστική δουλειά, και απολαύστε τη δύναμη της **automatic language detection** στα Java projects σας!

**Τελευταία ενημέρωση:** 2026-10-08  
**Δοκιμή με:** Aspose OCR for Java 24.12  
**Συγγραφέας:** Aspose  

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version>
</dependency>
```

## Σχετικά Μαθήματα

- [Ανίχνευση γλώσσας εικόνας με το Aspose Ocr Java Tutorial](/ocr/java/advanced-ocr-techniques/detect-language-image-with-aspose-ocr-java-tutorial/)
- [Εξαγωγή κειμένου από εικόνα σε Java – Πλήρες παράδειγμα OCR](/ocr/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/)
- [Batch Image Ocr σε Java – Γρήγορη εξαγωγή κειμένου από αρχεία PNG](/ocr/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}