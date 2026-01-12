---
category: general
date: 2026-01-12
description: Εξαγωγή κειμένου από εικόνα με Java χρησιμοποιώντας Aspose OCR. Μάθετε
  πώς να φορτώνετε εικόνα για OCR, να ενεργοποιήσετε τη διόρθωση ορθογραφίας και να
  λαμβάνετε ακριβή αποτελέσματα – ένα πλήρες tutorial OCR σε Java.
draft: false
keywords:
- extract text from image java
- load image for ocr
- java ocr tutorial
- Aspose OCR Java
- spell correction OCR
language: el
og_description: Εξαγωγή κειμένου από εικόνα Java με Aspose OCR. Αυτός ο οδηγός δείχνει
  πώς να φορτώσετε εικόνα για OCR, να ενεργοποιήσετε τη διόρθωση ορθογραφίας και να
  ανακτήσετε καθαρό κείμενο σε ένα tutorial OCR Java.
og_title: Εξαγωγή κειμένου από εικόνα Java – Πλήρης οδηγός OCR
tags:
- OCR
- Java
- Aspose
title: Εξαγωγή κειμένου από εικόνα Java – Πλήρης οδηγός OCR με διόρθωση ορθογραφίας
url: /el/java/advanced-ocr-techniques/extract-text-from-image-java-complete-ocr-guide-with-spell-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Απόσπαση Κειμένου από Εικόνα Java – Πλήρης Οδηγός OCR με Διόρθωση Ορθογραφίας

Έχετε ποτέ χρειαστεί να **extract text from image java** αλλά η έξοδος ήταν γεμάτη τυπογραφικά λάθη; Δεν είστε μόνοι. Σαρωμένες αποδείξεις, θορυβώδεις στιγμιότυπα οθόνης και PDF χαμηλής ανάλυσης παράγουν ακατάστατα αποτελέσματα, και οι περισσότεροι προγραμματιστές καταλήγουν να καθαρίζουν το κείμενο χειροκίνητα.  

Σε αυτόν τον οδηγό θα περάσουμε από ένα **java ocr tutorial** που σας δείχνει ακριβώς πώς να **load image for OCR**, να ενεργοποιήσετε τη διόρθωση ορθογραφίας και να λάβετε καθαρό, αναζητήσιμο κείμενο — όλα με το Aspose OCR for Java. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση πρόγραμμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο.

## Τι Θα Χρειαστεί

- **Java Development Kit (JDK) 8+** – ο κώδικας χρησιμοποιεί τυπικά Java APIs.
- **Aspose OCR for Java** library (η τελευταία έκδοση μέχρι το 2026). Μπορείτε να το αποκτήσετε από το Maven Central ή να κατεβάσετε το JAR απευθείας.
- Ένα αρχείο εικόνας που θέλετε να επεξεργαστείτε – για αυτόν τον οδηγό θα χρησιμοποιήσουμε το `noisy-scan.png` τοποθετημένο σε φάκελο που ονομάζεται `YOUR_DIRECTORY`.
- Ένα καλό IDE (IntelliJ IDEA, Eclipse ή VS Code) – οποιοδήποτε αρκεί, αλλά το IntelliJ κάνει τη διαχείριση του Maven άνετη.

Αυτό είναι όλο. Χωρίς επιπλέον frameworks, χωρίς βαριές εγγενείς εξαρτήσεις.

![Παράδειγμα εξαγωγής κειμένου από εικόνα Java](extract-text-from-image-java.png "παράδειγμα εξαγωγής κειμένου από εικόνα java")

*Το παραπάνω στιγμιότυπο οθόνης απεικονίζει την έξοδο της κονσόλας μετά την εκτέλεση του κώδικα – παρατηρήστε το καθαρό, διορθωμένο κείμενο.*

## Βήμα 1 – Προσθήκη Aspose OCR στο Έργο σας

Πρώτα απ' όλα. Χρειαζόμαστε τη μηχανή OCR στο classpath. Αν χρησιμοποιείτε Maven, προσθέστε την ακόλουθη εξάρτηση στο `pom.xml` σας:

```xml
<!-- Aspose OCR for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check Maven Central for the newest version -->
</dependency>
```

Αν προτιμάτε Gradle, το ισοδύναμο είναι:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

*Συμβουλή:* Πάντα ελέγχετε διπλά τον αριθμό έκδοσης· οι νεότερες κυκλοφορίες μπορεί να περιλαμβάνουν βελτιώσεις απόδοσης για θορυβώδεις εικόνες.

## Βήμα 2 – Αρχικοποίηση της Μηχανής OCR

Τώρα που η βιβλιοθήκη είναι διαθέσιμη, μπορούμε να δημιουργήσουμε μια παρουσία του `OcrEngine`. Σκεφτείτε αυτό το αντικείμενο ως τον εγκέφαλο που θα διαβάσει την εικόνα σας.

```java
import com.aspose.ocr.*;

public class SpellCorrectionTutorial {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

Γιατί δημιουργούμε πρώτα τη μηχανή; Το `OcrEngine` κρατά ρυθμίσεις παραμετροποίησης (όπως γλώσσα, DPI και διόρθωση ορθογραφίας) που επηρεάζουν κάθε επόμενη κλήση αναγνώρισης. Η προημεροληπτική δημιουργία το κρατάει ο κώδικας καθαρό και μας επιτρέπει να ρυθμίσουμε τις παραμέτρους από ένα σημείο.

## Βήμα 3 – Φόρτωση Εικόνας για OCR

Το επόμενο λογικό βήμα είναι να κατευθύνετε τη μηχανή στο αρχείο που θέλετε να επεξεργαστείτε. Εδώ συμβαίνει το τμήμα **load image for OCR**.

```java
        // Step 3: Load the image you want to extract text from
        ocrEngine.setImage("YOUR_DIRECTORY/noisy-scan.png");
```

Αν η εικόνα βρίσκεται κάπου αλλού (π.χ., σε URL ή σε `InputStream`), το Aspose OCR δέχεται επίσης αυτές τις υπερφορτώσεις – απλώς αντικαταστήστε τη διαδρομή string με την κατάλληλη κλήση μεθόδου.  

*Περίπτωση άκρης:* Όταν εργάζεστε με πολύ μεγάλες εικόνες (> 5 MB), σκεφτείτε να τις μειώσετε πρώτα για να διατηρήσετε τη χρήση μνήμης λογική. Η μηχανή OCR μπορεί να διαχειριστεί υψηλές αναλύσεις, αλλά η JVM μπορεί να εξαντλήσει τη μνήμη heap διαφορετικά.

## Βήμα 4 – Ενεργοποίηση Διόρθωσης Ορθογραφίας

Χωρίς διόρθωση ορθογραφίας, το OCR θα αναπαράγει πιστά ό,τι «βλέπει», ακόμη και αν οι χαρακτήρες είναι λανθασμένα αναγνωρισμένοι. Ενεργοποιήστε τη δυνατότητα και αφήστε τη μηχανή να διορθώσει κοινά λάθη.

```java
        // Step 4: Enable spell‑correction to improve accuracy
        ocrEngine.getRecognitionSettings().setSpellCorrectionEnabled(true);
```

Πίσω από τη σκηνή, η μηχανή εκτελεί έναν ελαφρύ έλεγχο λεξικού. Είναι ιδιαίτερα χρήσιμο για κείμενο στα Αγγλικά, αλλά το Aspose υποστηρίζει επίσης άλλες γλώσσες – απλώς ορίστε την ιδιότητα `Language` αναλόγως.

## Βήμα 5 – Αναγνώριση Κειμένου και Ανάκτηση του Αποτελέσματος

Τώρα ζητάμε τελικά από τη μηχανή να κάνει τη δουλειά της. Η μέθοδος `recognize()` επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει το εξαγόμενο κείμενο και, προαιρετικά, πληροφορίες bounding‑box.

```java
        // Step 5: Perform recognition
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 6: Display the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

**Αναμενόμενη έξοδος** (υποθέτοντας ότι η δείγμα εικόνας περιέχει τη φράση “Invoice #1234” με λίγες κηλίδες):

```
Corrected text:
Invoice #1234
Date: 2025-11-30
Total: $1,250.00
```

Παρατηρήστε πώς η μηχανή OCR διόρθωσε το “I” που αρχικά διαβάστηκε ως “1” και αφαίρεσε τα περιττά σημεία. Αυτή είναι η μαγεία της διόρθωσης ορθογραφίας.

## Βήμα 6 – Συνηθισμένα Πιθανά Σφάλματα & Πώς να τα Αποφύγετε

- **Missing language data** – Εάν λαμβάνετε ακατάληπτους χαρακτήρες, επαληθεύστε ότι το πακέτο γλώσσας για τη στοχευόμενη γλώσσα σας είναι εγκατεστημένο. Το Aspose περιλαμβάνει τα Αγγλικά από προεπιλογή· άλλες γλώσσες απαιτούν πρόσθετη λήψη.
- **Incorrect DPI settings** – Οι εικόνες χαμηλής ανάλυσης (< 100 DPI) συχνά παράγουν θολά αποτελέσματα. Μπορείτε να βελτιώσετε την ακρίβεια καλώντας `ocrEngine.getRecognitionSettings().setDpi(300);` πριν από την αναγνώριση.
- **File path issues** – Οι σχετικές διαδρομές επιλύονται σε σχέση με τον τρέχοντα φάκελο εργασίας. Η χρήση απόλυτης διαδρομής ή `Paths.get(...).toAbsolutePath()` εξαλείφει τις εκπλήξεις “αρχείο δεν βρέθηκε”.
- **Memory leaks** – Το `OcrEngine` υλοποιεί το `AutoCloseable`. Σε μια υπηρεσία που τρέχει πολύ χρόνο, τυλίξτε τη μηχανή σε μπλοκ try‑with‑resources για να διασφαλίσετε ότι οι εγγενείς πόροι απελευθερώνονται:

```java
try (OcrEngine ocrEngine = new OcrEngine()) {
    // configure and recognize...
}
```

## Πλήρες, Έτοιμο‑για‑Εκτέλεση Παράδειγμα

Παρακάτω βρίσκεται το πλήρες πρόγραμμα, αντιγράψτε‑και‑επικολλήστε το σε ένα αρχείο με όνομα `SpellCorrectionTutorial.java`, προσαρμόστε τη διαδρομή της εικόνας και τρέξτε το με `mvn exec:java` ή τη ρύθμιση εκτέλεσης του IDE σας.

```java
import com.aspose.ocr.*;

public class SpellCorrectionTutorial {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        try (OcrEngine ocrEngine = new OcrEngine()) {

            // Load the image you want to extract text from
            ocrEngine.setImage("YOUR_DIRECTORY/noisy-scan.png");

            // Enable spell‑correction for cleaner output
            ocrEngine.getRecognitionSettings().setSpellCorrectionEnabled(true);

            // (Optional) Boost accuracy for low‑resolution scans
            ocrEngine.getRecognitionSettings().setDpi(300);

            // Perform the recognition
            OcrResult ocrResult = ocrEngine.recognize();

            // Show the corrected text
            System.out.println("Corrected text:");
            System.out.println(ocrResult.getText());
        }
    }
}
```

Τρέξτε το, και θα δείτε το διορθωμένο κείμενο να εκτυπώνεται στην κονσόλα — ακριβώς αυτό που στοχεύει να παραδώσει ένας τυπικός **java ocr tutorial**.

## Επόμενα Βήματα – Πέρα από τη Βασική Εξαγωγή

Τώρα που μπορείτε να **extract text from image java** με διόρθωση ορθογραφίας, σκεφτείτε αυτές τις βελτιώσεις:

1. **Batch processing** – Επανάληψη πάνω σε έναν φάκελο εικόνων, συλλογή αποτελεσμάτων σε CSV και παροχή τους σε ανάλυση downstream analytics.
2. **Language detection** – Χρησιμοποιήστε `ocrEngine.getRecognitionSettings().setLanguage(Language.AUTO_DETECT);` για πολυγλωσσικά έγγραφα.
3. **Region‑based OCR** – Εάν χρειάζεστε μόνο μια συγκεκριμένη περιοχή (π.χ., περιοχή barcode), ορίστε ένα rectangle μέσω `ocrEngine.setRectangle(new Rectangle(x, y, width, height));`.
4. **Integrate with PDF** – Μετατρέψτε πρώτα τα σαρωμένα PDF σε εικόνες, έπειτα εκτελέστε την ίδια αλυσίδα; το Aspose PDF for Java μπορεί να αποδώσει τις σελίδες ως PNG.

Κάθε ένα από αυτά τα θέματα συνδέεται με τα βασικά βήματα που καλύψαμε, οπότε θα βρείτε τη μετάβαση ομαλή.

---

### TL;DR

- **Primary goal:** *extract text from image java* χρησιμοποιώντας το Aspose OCR.
- **Key actions:** load image for OCR, enable spell‑correction, run `recognize()`.
- **Result:** καθαρό, αναζητήσιμο κείμενο έτοιμο για ευρετηρίαση ή περαιτέρω επεξεργασία.

Δοκιμάστε το με τις δικές σας σαρώσεις, προσαρμόστε το DPI και πειραματιστείτε με τα πακέτα γλώσσας. Η δύναμη του OCR στη Java είναι στα χέρια σας — καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}