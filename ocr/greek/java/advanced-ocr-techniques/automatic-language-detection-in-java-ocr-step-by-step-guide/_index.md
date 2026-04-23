---
category: general
date: 2026-02-27
description: Η αυτόματη ανίχνευση γλώσσας σας επιτρέπει να εξάγετε κείμενο από αρχεία
  εικόνας όπως PNG σε Java—δείτε ένα παράδειγμα java OCR που ενεργοποιεί την αυτόματη
  ανίχνευση γλώσσας.
draft: false
keywords:
- automatic language detection
- extract text from image
- convert png to text
- java ocr example
- enable auto language detection
language: el
og_description: Η αυτόματη ανίχνευση γλώσσας στο Java OCR καθιστά εύκολο την εξαγωγή
  κειμένου από αρχεία εικόνας. Μάθετε πώς να ενεργοποιήσετε την αυτόματη ανίχνευση
  γλώσσας με ένα πλήρες παράδειγμα Java OCR.
og_title: Αυτόματη Ανίχνευση Γλώσσας σε Java OCR – Πλήρης Οδηγός
tags:
- Java
- OCR
- Aspose
title: Αυτόματη Ανίχνευση Γλώσσας σε Java OCR – Οδηγός Βήμα‑Βήμα
url: /el/java/advanced-ocr-techniques/automatic-language-detection-in-java-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αυτόματη Ανίχνευση Γλώσσας σε Java OCR – Πλήρης Οδηγός

Κάποτε χρειάστηκε **αυτόματη ανίχνευση γλώσσας** όταν εξάγετε κείμενο από ένα στιγμιότυπο οθόνης που συνδυάζει Αγγλικά και Ρωσικά; Δεν είστε οι μόνοι. Σε πολλές πραγματικές εφαρμογές — σκεφτείτε σαρωτές αποδείξεων, πολυγλωσσικές φόρμες ή bots εικόνων κοινωνικών δικτύων — η προεπιλογή της γλώσσας εκ των προτέρων αποτελεί πρόβλημα.  

Το καλό νέο είναι ότι το Aspose OCR for Java μπορεί να εντοπίσει τη γλώσσα για εσάς, ώστε να μπορείτε απλώς **να εξάγετε κείμενο από αρχεία εικόνας** χωρίς καμία χειροκίνητη ρύθμιση. Σε αυτό το tutorial θα δείξουμε ένα **java ocr example** που ενεργοποιεί **την αυτόματη ανίχνευση γλώσσας**, επεξεργάζεται ένα PNG με μιξ‑γλώσσα και εκτυπώνει το αποτέλεσμα στην κονσόλα. Στο τέλος θα ξέρετε ακριβώς πώς να **μετατρέψετε png σε κείμενο** με λίγες μόνο γραμμές κώδικα.

## Τι Θα Χρειαστείτε

- Java 17 (ή οποιοδήποτε πρόσφατο JDK) – το API λειτουργεί με Java 8+ αλλά τα πιο νέα runtime προσφέρουν καλύτερη απόδοση.  
- Βιβλιοθήκη Aspose OCR for Java (η πιο πρόσφατη έκδοση μέχρι 2026‑02‑27). Μπορείτε να την κατεβάσετε από το Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version>
</dependency>
```

- Ένα αρχείο εικόνας που περιέχει περισσότερες από μία γλώσσες. Για το demo μας θα χρησιμοποιήσουμε το `mixed-eng-rus.png` (Αγγλικά + Ρωσικά).  
- Ένα καλό IDE (IntelliJ IDEA, Eclipse, VS Code…) – όποιο και αν προτιμάτε.

> **Pro tip:** Αν δεν έχετε δοκιμαστική εικόνα, δημιουργήστε ένα PNG με μερικές αγγλικές λέξεις και τις ρωσικές τους αντιστοιχίες. Η μηχανή OCR δεν ενδιαφέρεται για την πηγή, μόνο για τα δεδομένα pixel.

Παρακάτω βρίσκεται το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα.

![Αυτόματη ανίχνευση γλώσσας σε PNG με μιξ‑γλώσσα](/images/mixed-eng-rus.png "παράδειγμα αυτόματης ανίχνευσης γλώσσας")

## Βήμα 1: Ρύθμιση του OCR Engine

Πρώτα, δημιουργήστε μια παρουσία του `OcrEngine`. Αυτό το αντικείμενο είναι η καρδιά της βιβλιοθήκης· κρατά όλες τις επιλογές ρυθμίσεων, συμπεριλαμβανομένης εκείνης που ενεργοποιεί **την αυτόματη ανίχνευση γλώσσας**.

```java
import com.aspose.ocr.*;

public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable automatic language detection
        ocrEngine.setAutoDetectLanguage(true);
```

Γιατί το ενεργοποιούμε εδώ;  
Επειδή χωρίς το `setAutoDetectLanguage(true)`, η μηχανή θα υποθέσει μια προεπιλεγμένη γλώσσα (συνήθως Αγγλικά). Όταν η εικόνα σας συνδυάζει διαφορετικά αλφάβητα, το βήμα ανίχνευσης βελτιώνει δραστικά την ακρίβεια — είναι σαν ένας πολύγλωσσος διερμηνέας που ακούει πριν μεταφράσει.

## Βήμα 2: Φόρτωση της Εικόνας και Εκτέλεση της Διαδικασίας OCR

Τώρα δείξτε στη μηχανή το αρχείο PNG. Η μέθοδος `processImage` επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει το αναγνωρισμένο κείμενο, τις βαθμολογίες εμπιστοσύνης και ακόμη και τον κωδικό της ανιχνευθείσας γλώσσας.

```java
        // Step 3: Process the image that contains both English and Russian text
        OcrResult ocrResult = ocrEngine.processImage("YOUR_DIRECTORY/mixed-eng-rus.png");
```

Μερικά σημεία που πρέπει να προσέξετε:

- **Διαχείριση διαδρομής:** Χρησιμοποιήστε απόλυτη διαδρομή ή τοποθετήστε την εικόνα στο φάκελο resources του έργου σας και φορτώστε την μέσω `getResourceAsStream`.  
- **Συμβουλή απόδοσης:** Αν επεξεργάζεστε πολλές εικόνες, επαναχρησιμοποιήστε την ίδια παρουσία `OcrEngine` αντί να δημιουργείτε νέα κάθε φορά. Η μηχανή αποθηκεύει στην κρυφή μνήμη τα μοντέλα γλώσσας, οπότε οι επόμενες κλήσεις είναι γρηγορότερες.

## Βήμα 3: Ανάκτηση και Εμφάνιση του Αναγνωρισμένου Κειμένου

Τέλος, εξάγετε το απλό κείμενο από το `OcrResult`. Η μέθοδος `getText()` αφαιρεί τυχόν πληροφορίες διάταξης, δίνοντάς σας μια καθαρή συμβολοσειρά που μπορείτε να αποθηκεύσετε, να αναζητήσετε ή να περάσετε σε άλλο σύστημα.

```java
        // Step 4: Print the recognized text to the console
        System.out.println(ocrResult.getText());
    }
}
```

Όταν εκτελέσετε το πρόγραμμα, θα πρέπει να δείτε κάτι σαν:

```
Hello world!
Привет мир!
```

Αυτή η έξοδος επιβεβαιώνει ότι η μηχανή ανίχνευσε σωστά τόσο τα Αγγλικά όσο και τα Ρωσικά τμήματα, χάρη στην **αυτόματη ανίχνευση γλώσσας**. Αν απενεργοποιήσετε τη σημαία, πιθανότατα θα λάβετε ακατανόητους κυριλλικούς χαρακτήρες, δείχνοντας γιατί η λειτουργία auto‑detect είναι απαραίτητη για σενάρια μιξ‑γλώσσας.

## Συνηθισμένες Παραλλαγές & Ακραίες Περιπτώσεις

### Μετατροπή PNG σε Κείμενο χωρίς Ανίχνευση Γλώσσας

Αν γνωρίζετε ότι η εικόνα περιέχει μόνο μία γλώσσα, μπορείτε να παραλείψετε το βήμα auto‑detect:

```java
ocrEngine.setLanguage(OcrLanguage.English);
```

Αλλά θυμηθείτε, η στιγμή που εμφανιστεί ένας τυχαίος χαρακτήρας από άλλο αλφάβητο, η ακρίβεια πέφτει απότομα.

### Διαχείριση Μεγάλων Εικόνων

Για σαρώσεις υψηλής ανάλυσης, σκεφτείτε να μειώσετε την ανάλυση σε μέγιστο 300 DPI πριν φορτώσετε την εικόνα. Η μηχανή OCR αποδίδει καλύτερα στην κλίμακα 150‑300 DPI· πέρα από αυτό σπαταλάτε μνήμη χωρίς μετρήσιμα οφέλη.

```java
BufferedImage original = ImageIO.read(new File("large.png"));
BufferedImage resized = ImageUtil.resize(original, 1024, 0); // keep aspect ratio
ocrEngine.processImage(resized);
```

### Εξαγωγή Κειμένου από Εικόνα σε Web Service

Αν εκθέτετε αυτή τη λειτουργία μέσω ενός REST endpoint, θυμηθείτε να:

- Επικυρώσετε τον τύπο του ανεβασμένου αρχείου (αποδεχτείτε μόνο PNG/JPEG).  
- Εκτελέσετε το OCR σε ξεχωριστό νήμα ή ασύγχρονη εργασία για να μην μπλοκάρετε το νήμα της αίτησης.  
- Επιστρέψετε το κείμενο ως JSON:

```json
{ "extractedText": "Hello world!\nПривет мир!" }
```

## Πλήρες Παράδειγμα (Όλα τα Βήματα Συνδυασμένα)

Παρακάτω είναι το ολοκληρωμένο πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε ένα αρχείο `MixedLanguageDemo.java`. Περιλαμβάνει τις δηλώσεις import, τη διαχείριση σφαλμάτων και ένα σχόλιο που εξηγεί κάθε γραμμή.

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

Τρέξτε το με:

```bash
mvn compile exec:java -Dexec.mainClass=MixedLanguageDemo
```

Αν όλα είναι ρυθμισμένα σωστά, η κονσόλα θα εμφανίσει τη γραμμή στα Αγγλικά ακολουθούμενη από το ρωσικό ισοδύναμο.

## Ανακεφαλαίωση & Επόμενα Βήματα

Διασχίσαμε ένα **java ocr example** που **ενεργοποιεί την αυτόματη ανίχνευση γλώσσας**, επεξεργάζεται ένα PNG μιξ‑γλώσσας και **εξάγει κείμενο από αρχεία εικόνας** χωρίς καμία χειροκίνητη επιλογή γλώσσας. Τα κύρια σημεία:

1. Ενεργοποιήστε το `setAutoDetectLanguage(true)` ώστε το Aspose να διαχειρίζεται πολυγλωσσικό περιεχόμενο.  
2. Χρησιμοποιήστε το `processImage` για να τροφοδοτήσετε οποιοδήποτε PNG (ή JPEG) και πάρτε μια καθαρή συμβολοσειρά μέσω `getText()`.  
3. Το ίδιο μοτίβο λειτουργεί για PDFs, TIFFs ή ακόμη και ζωντανές ροές κάμερας — απλώς αλλάξτε την πηγή εισόδου.

Θέλετε να προχωρήσετε παραπέρα; Δοκιμάστε τις παρακάτω ιδέες:

- **Επεξεργασία παρτίδας:** Επανάληψη πάνω σε έναν φάκελο PNG και αποθήκευση κάθε αποτελέσματος σε βάση δεδομένων.  
- **Μετα-επεξεργασία ανά γλώσσα:** Μετά την ανίχνευση, δρομολογήστε το αγγλικό κείμενο σε ελεγκτή ορθογραφίας και το ρωσικό σε υπηρεσία μεταγραφής.  
- **Συνδυασμός με AI:** Στείλτε το εξαγόμενο κείμενο σε μοντέλο γλώσσας για περίληψη ή μετάφραση.

Αυτό ήταν για τώρα. Αν αντιμετωπίσετε προβλήματα — π.χ. η μηχανή δεν ανιχνεύει τη γλώσσα που περιμένετε — ελέγξτε ότι η εικόνα είναι καθαρή και ότι χρησιμοποιείτε την πιο πρόσφατη έκδοση του Aspose OCR. Καλό κώδικα και απολαύστε τη δύναμη της **αυτόματης ανίχνευσης γλώσσας** στα Java projects σας!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}