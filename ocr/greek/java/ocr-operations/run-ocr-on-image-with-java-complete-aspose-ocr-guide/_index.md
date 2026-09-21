---
category: general
date: 2026-02-09
description: Εκτελέστε OCR σε εικόνα χρησιμοποιώντας το Aspose OCR σε Java – μάθετε
  πώς να εξάγετε κείμενο από PNG και να ενεργοποιήσετε την αυτόματη ανίχνευση γλώσσας
  OCR σε λίγα μόνο βήματα.
draft: false
keywords:
- run OCR on image
- extract text from PNG
- auto detect language OCR
- Aspose OCR Java
- Hindi OCR example
language: el
og_description: Εκτελέστε OCR στην εικόνα άμεσα. Αυτός ο οδηγός δείχνει πώς να εξάγετε
  κείμενο από αρχεία PNG και να ενεργοποιήσετε την αυτόματη ανίχνευση γλώσσας OCR
  χρησιμοποιώντας το Aspose OCR για Java.
og_title: Εκτέλεση OCR σε εικόνα με Java – Πλήρης οδηγός Aspose OCR
tags:
- OCR
- Java
- Aspose
title: Εκτέλεση OCR σε εικόνα με Java – Πλήρης οδηγός Aspose OCR
url: /el/java/ocr-operations/run-ocr-on-image-with-java-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε Εικόνα με Java – Πλήρης Οδηγός Aspose OCR

Έχετε ποτέ χρειαστεί να **εκτελέσετε OCR σε εικόνα** αρχεία αλλά δεν ήξερες από πού να ξεκινήσεις; Ίσως έχετε μερικά PNG στιγμιότυπα που περιέχουν κείμενο στα Χίντι, και αναρωτιέστε αν η Java μπορεί να εξάγει τις λέξεις χωρίς μια τεράστια εγκατάσταση μηχανικής μάθησης. Τα καλά νέα είναι: μπορείτε, και είναι εκπληκτικά απλό με το Aspose OCR.

Σε αυτό το tutorial θα περάσουμε από ένα πραγματικό παράδειγμα που **extracts text from PNG** αρχεία, σας δείχνει πώς να ενεργοποιήσετε **auto detect language OCR**, και σας παρέχει ένα έτοιμο προς εκτέλεση πρόγραμμα Java. Στο τέλος, θα έχετε ένα λειτουργικό snippet που εκτυπώνει χαρακτήρες Χίντι στην κονσόλα, και θα καταλάβετε γιατί κάθε γραμμή είναι σημαντική.

## Τι Θα Χρειαστείτε

- **Java Development Kit (JDK) 8** ή νεότερο – ο κώδικας μεταγλωττίζεται με οποιαδήποτε πρόσφατη έκδοση.  
- **Aspose.OCR for Java** βιβλιοθήκη – κατεβάστε το τελευταίο JAR από τον ιστότοπο Aspose ή το Maven Central.  
- Ένα δείγμα εικόνας (`hindi_sample.png`) που περιέχει το σύστημα γραφής Devanagari – μπορείτε να δημιουργήσετε ένα με οποιοδήποτε εργαλείο στιγμιότυπων.  
- Ένα IDE ή απλός επεξεργαστής κειμένου – χρησιμοποιώ IntelliJ IDEA, αλλά το απλό `javac` λειτουργεί καλά.

Καμία εξωτερική υπηρεσία, κανένα κλειδί cloud API, μόνο ένα τοπικό JAR και μια εικόνα. Απλό, έτσι;

## Βήμα 1: Προσθήκη Aspose OCR στο Έργο σας

Πρώτα, βεβαιωθείτε ότι το JAR του Aspose OCR βρίσκεται στο classpath σας. Αν χρησιμοποιείτε Maven, προσθέστε αυτήν την εξάρτηση:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

Αν προτιμάτε τη χειροκίνητη μέθοδο, κατεβάστε το `aspose-ocr-23.10.jar` και τοποθετήστε το στον φάκελο `libs/`, μετά μεταγλωττίστε με:

```bash
javac -cp "libs/*" LanguageExample.java
```

> **Pro tip:** Κρατήστε τον αριθμό έκδοσης του JAR σε σχόλιο στην κορυφή του αρχείου πηγαίου κώδικα – βοηθά το μέλλον εσάς να θυμάται ποια API επιφάνεια στοχεύσατε.

## Βήμα 2: Δημιουργία του Αντικειμένου OCR Engine

Τώρα δημιουργούμε το βασικό αντικείμενο που κάνει όλη τη βαριά δουλειά. Σκεφτείτε το `OcrEngine` ως τον εγκέφαλο πίσω από τη λειτουργία.

```java
// Step 2: Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

Γιατί να το δημιουργήσουμε εδώ; Η μηχανή κρατά ρυθμίσεις διαμόρφωσης (όπως η γλώσσα) και επαναχρησιμοποιήσιμους πόρους, έτσι η δημιουργία του μία φορά ανά εφαρμογή μειώνει το κόστος.

## Βήμα 3: Διαμόρφωση Ρυθμίσεων Γλώσσας (και Ενεργοποίηση Auto‑Detect)

Αν γνωρίζετε τη γλώσσα εκ των προτέρων—π.χ. Χίντι—μπορείτε να πείτε στη μηχανή να εστιάσει στο Devanagari. Αυτό αυξάνει την ακρίβεια και επιταχύνει την επεξεργασία.

```java
// Step 3a: Force Hindi (Devanagari) recognition
ocrEngine.getConfiguration().setLanguage(Language.HINDI);

// Step 3b (optional): Let the engine guess the language if you're unsure
ocrEngine.getConfiguration().setAutoDetectLanguage(true);
```

Η γραμμή `setAutoDetectLanguage(true)` είναι ο διακόπτης **auto detect language OCR**. Όταν τροφοδοτείτε μια εικόνα με μικτή γλώσσα, η μηχανή θα προσπαθήσει να αναγνωρίσει αυτόματα κάθε γραφή. Είναι χρήσιμο για εργασίες batch όπου δεν μπορείτε να επισημάνετε χειροκίνητα κάθε αρχείο.

## Βήμα 4: Εκτέλεση OCR στην PNG Εικόνα

Εδώ είναι που πραγματικά **run OCR on image** δεδομένα. Η μέθοδος `recognize` δέχεται μια διαδρομή αρχείου, διαβάζει το bitmap και επιστρέφει ένα `RecognitionResult`.

```java
// Step 4: Perform OCR on the PNG file
RecognitionResult result = ocrEngine.recognize("YOUR_DIRECTORY/hindi_sample.png");
```

Αντικαταστήστε το `YOUR_DIRECTORY` με την πραγματική διαδρομή φακέλου. Αν το αρχείο δεν βρεθεί, το Aspose ρίχνει μια σαφή εξαίρεση – δεν χρειάζεται να μαντέψετε γιατί απέτυχε αργότερα.

## Βήμα 5: Ανάκτηση και Εμφάνιση του Εξαγόμενου Κειμένου

Τέλος, εξάγετε τη αναγνωρισμένη συμβολοσειρά από το αντικείμενο result και την εκτυπώστε. Για Χίντι, θα δείτε χαρακτήρες Unicode στην κονσόλα, εφόσον το τερματικό σας υποστηρίζει UTF‑8.

```java
// Step 5: Output the recognized Hindi text
System.out.println("Hindi text:");
System.out.println(result.getText());
```

**Αναμενόμενη έξοδος** (υποθέτοντας ότι η δείγμα εικόνας λέει “नमस्ते दुनिया”):

```
Hindi text:
नमस्ते दुनिया
```

Αν ενεργοποιήσατε το auto‑detect και η εικόνα περιείχε επίσης Αγγλικά, η έξοδος θα περιλάμβανε και τις δύο γραφές, αναμεμιγμένες ωραία.

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω είναι το πλήρες, εκτελέσιμο πρόγραμμα. Αντιγράψτε‑και‑επικολλήστε το στο `LanguageExample.java`, προσαρμόστε τη διαδρομή της εικόνας, και είστε έτοιμοι.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.enums.*;

public class LanguageExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Specify the language to be recognized (Hindi – Devanagari script)
        ocrEngine.getConfiguration().setLanguage(Language.HINDI);

        // Step 3: (Optional) Enable automatic fallback to language detection
        ocrEngine.getConfiguration().setAutoDetectLanguage(true);

        // Step 4: Run OCR on the input image
        RecognitionResult result = ocrEngine.recognize("YOUR_DIRECTORY/hindi_sample.png");

        // Step 5: Print the extracted Hindi text
        System.out.println("Hindi text:");
        System.out.println(result.getText());
    }
}
```

> **Note:** Αν χρησιμοποιείτε IDE, βεβαιωθείτε ότι το build path του έργου περιλαμβάνει το Aspose OCR JAR. Στο IntelliJ, μεταβείτε στο *File → Project Structure → Libraries* και προσθέστε το JAR εκεί.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν το PNG μου είναι χαμηλής ανάλυσης;

Η ακρίβεια του OCR πέφτει απότομα κάτω από 150 dpi. Ανεβάστε την ανάλυση της εικόνας με ένα εργαλείο όπως το ImageMagick (`convert input.png -resize 200% output.png`) πριν τη δώσετε στη μηχανή. Η σημαία `auto detect language OCR` λειτουργεί ακόμη, αλλά θα δείτε λιγότερα λάθη αναγνώρισης.

### Μπορώ να επεξεργαστώ πολλές εικόνες σε βρόχο;

Απολύτως. Τυλίξτε την κλήση `recognize` σε έναν βρόχο `for`, και επαναχρησιμοποιήστε το ίδιο αντικείμενο `OcrEngine`. Η επαναχρήση της μηχανής αποφεύγει την επαναφόρτωση μοντέλων γλώσσας σε κάθε επανάληψη, εξοικονομώντας μνήμη και χρόνο CPU.

```java
String[] files = {"img1.png", "img2.png", "img3.png"};
for (String file : files) {
    RecognitionResult r = ocrEngine.recognize(file);
    System.out.println("Text from " + file + ":");
    System.out.println(r.getText());
}
```

### Πώς να διαχειριστώ κονσόλες που δεν υποστηρίζουν Unicode;

Αν το τερματικό σας εμφανίζει ακατάληπτα σύμβολα, ορίστε την κωδικοποίηση αρχείου σε UTF‑8 όταν εκκινείτε τη Java:

```bash
java -Dfile.encoding=UTF-8 -cp "libs/*" LanguageExample
```

### Υπάρχει τρόπος να λάβω βαθμολογίες εμπιστοσύνης;

Ναι. Το `RecognitionResult` περιέχει τη μέθοδο `getConfidence()` που επιστρέφει ένα float μεταξύ 0 και 1 για κάθε αναγνωρισμένη γραμμή. Μπορείτε να επαναλάβετε το `result.getLines()` για να εξάγετε αυτές τις τιμές—χρήσιμο για φιλτράρισμα αποτελεσμάτων χαμηλής εμπιστοσύνης.

## Pro Συμβουλές για Χρήση σε Παραγωγή

- **Cache language models**: Αν επεξεργάζεστε χιλιάδες εικόνες, κρατήστε τη μηχανή ενεργή για όλο το batch.  
- **Parallel processing**: Τυλίξτε κάθε εικόνα σε ένα `Callable` και δώστε το σε ένα thread pool. Απλώς θυμηθείτε ότι η μηχανή δεν είναι thread‑safe· δημιουργήστε μία ανά νήμα.  
- **Logging**: Χρησιμοποιήστε έναν κατάλληλο logger (SLF4J) αντί για `System.out.println` για μεγάλες εργασίες.  
- **Memory management**: Καλέστε `ocrEngine.dispose()` όταν τελειώσετε για να ελευθερώσετε τους εγγενείς πόρους.

## Οπτική Επισκόπηση

![Διάγραμμα παραδείγματος εκτέλεσης OCR σε εικόνα](ocr_flow.png "Διάγραμμα παραδείγματος εκτέλεσης OCR σε εικόνα")

Το παραπάνω διάγραμμα απεικονίζει τη ροή: **run OCR on image → language configuration → auto detect language OCR (optional) → extract text from PNG**.

## Συμπέρασμα

Μόλις δείξαμε πώς να **run OCR on image** αρχεία χρησιμοποιώντας το Aspose OCR για Java, πώς να **extract text from PNG** με ρυθμίσεις ειδικές για τη γλώσσα, και πώς να ενεργοποιήσετε το **auto detect language OCR** για ευέλικτα, πολυγλωσσικά σενάρια. Το πλήρες παράδειγμα κώδικα είναι έτοιμο για αντιγραφή, μεταγλώττιση και εκτέλεση—χωρίς κρυφά βήματα, χωρίς εξωτερικές υπηρεσίες.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να αντικαταστήσετε το `Language.HINDI` με το `Language.AUTO` και δώστε ένα έγγραφο μικτής γραφής, ή πειραματιστείτε με είσοδο PDF (το Aspose OCR υποστηρίζει επίσης PDF). Μπορείτε επίσης να ενσωματώσετε αυτό το snippet σε ένα Spring Boot REST endpoint για να εκθέσετε το OCR ως υπηρεσία web.

Καλό κώδικα, και εύχομαι οι εικόνες σας να είναι πάντα αναγνώσιμες!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}