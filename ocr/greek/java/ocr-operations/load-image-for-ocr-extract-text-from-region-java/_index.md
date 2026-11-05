---
category: general
date: 2026-06-16
description: Φορτώστε εικόνα για OCR και εξάγετε γρήγορα κείμενο από περιοχή χρησιμοποιώντας
  το Aspose OCR σε Java. Οδηγός βήμα‑βήμα με πλήρες κώδικα, συμβουλές και διαχείριση
  ακραίων περιπτώσεων.
draft: false
keywords:
- load image for OCR
- extract text from region
- Aspose OCR Java
- OCR region processing
- Java image recognition
language: el
og_description: Φορτώστε εικόνα για OCR σε Java και εξάγετε κείμενο από περιοχή με
  Aspose OCR. Πλήρης οδηγός με κώδικα, εξηγήσεις και βέλτιστες πρακτικές.
og_title: Φόρτωση εικόνας για OCR – Οδηγός Εξαγωγής Περιοχής σε Java
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: load image for OCR and quickly extract text from region using Aspose
    OCR in Java. Step‑by‑step guide with full code, tips, and edge‑case handling.
  headline: load image for OCR, extract text from region – Java
  type: TechArticle
- description: load image for OCR and quickly extract text from region using Aspose
    OCR in Java. Step‑by‑step guide with full code, tips, and edge‑case handling.
  name: load image for OCR, extract text from region – Java
  steps:
  - name: Create the OCR engine and **load image for OCR**
    text: First we instantiate `OcrEngine` and point it at the file we want to process.
      The `ImageStream.fromFile` helper takes care of reading the bytes and wrapping
      them in a format the engine understands.
  - name: Define the **region** you want to **extract text from region**
    text: A `java.awt.Rectangle` describes the X/Y offset and the width/height of
      the area you care about. The numbers are pixel‑based, so you may need to experiment
      a bit with your particular document.
  - name: Apply the region to the engine
    text: The `RecognitionSettings` object holds all the knobs you can turn. Here
      we simply set the region we just created.
  - name: Run the OCR – the engine will also deskew the region automatically
    text: 'Calling `recognize()` does the heavy lifting: it deskews, binarizes, and
      runs the character recognizer on the defined rectangle.'
  - name: '**Extract text from region** and display it'
    text: Finally we pull the plain‑text representation out of the `OcrResult`. Trimming
      removes stray line breaks and spaces.
  type: HowTo
tags:
- Java
- OCR
- Aspose
- Image Processing
title: Φόρτωση εικόνας για OCR, εξαγωγή κειμένου από περιοχή – Java
url: /el/java/ocr-operations/load-image-for-ocr-extract-text-from-region-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Φόρτωση εικόνας για OCR, εξαγωγή κειμένου από περιοχή – Java

Έχετε χρειαστεί ποτέ να **φορτώσετε εικόνα για OCR** αλλά δεν ήσασταν σίγουροι πώς να περιορίσετε τη σάρωση μόνο στο τμήμα που σας ενδιαφέρει; Δεν είστε μόνοι. Σε πολλά πραγματικά έργα—σκεφτείτε τιμολόγια, φόρμες ή ταυτότητες—θέλετε μόνο να **εξάγετε κείμενο από περιοχή** που περιέχει πραγματικά τα δεδομένα, όχι ολόκληρη η εικόνα.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει ακριβώς πώς να φορτώσετε μια εικόνα για OCR χρησιμοποιώντας Aspose OCR, να ορίσετε μια ορθογώνια περιοχή και, στη συνέχεια, να εξάγετε το κείμενο από εκείνη την περιοχή. Στο τέλος θα έχετε ένα αυτόνομο πρόγραμμα Java που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Maven ή Gradle, μαζί με μια σειρά πρακτικών συμβουλών για την αντιμετώπιση κοινών προβλημάτων.

## Τι θα χρειαστείτε

| Προαπαιτούμενο | Γιατί είναι σημαντικό |
|----------------|------------------------|
| **Java 17** (ή οποιοδήποτε πρόσφατο JDK) | Το Aspose OCR διανέμεται ως JAR συμβατό με Java 17. |
| **Aspose OCR for Java** library (κατεβάστε από το Aspose ή προσθέστε μέσω Maven) | Παρέχει το `OcrEngine` και τις σχετικές κλάσεις. |
| **Αρχείο εικόνας** (π.χ., `form.jpg`) που περιέχει το πεδίο που θέλετε να διαβάσετε | Η μηχανή μπορεί να επεξεργαστεί μόνο ό,τι της δίνετε. |
| **Ένα καλό IDE** (IntelliJ, Eclipse, VS Code) – προαιρετικό αλλά χρήσιμο | Κάνει την αποσφαλμάτωση και την εκτέλεση του κώδικα πιο εύκολη. |

Αν χρησιμοποιείτε Maven, προσθέστε αυτήν την εξάρτηση στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check Aspose for the latest version -->
</dependency>
```

*Συμβουλή:* Η δωρεάν έκδοση αξιολόγησης λειτουργεί καλά για δοκιμές, αλλά προσθέτει υδατογράφημα στο αποτέλεσμα. Αποκτήστε πλήρη άδεια αν σκοπεύετε να διανείμετε τη λύση.

## Φόρτωση εικόνας για OCR – Υλοποίηση βήμα‑βήμα

Παρακάτω χωρίζουμε τη διαδικασία σε πέντε σαφή βήματα. Κάθε βήμα περιλαμβάνει ένα απόσπασμα κώδικα, μια σύντομη εξήγηση του **γιατί** το κάνουμε, και μια γρήγορη συμβουλή για την αποφυγή των συνηθισμένων παγίδων.

### Βήμα 1: Δημιουργία της μηχανής OCR και **φόρτωση εικόνας για OCR**

Πρώτα δημιουργούμε ένα αντικείμενο `OcrEngine` και το κατευθύνουμε στο αρχείο που θέλουμε να επεξεργαστούμε. Η βοηθητική μέθοδος `ImageStream.fromFile` αναλαμβάνει την ανάγνωση των bytes και τη συσκευή τους σε μορφή που καταλαβαίνει η μηχανή.

```java
import com.aspose.ocr.*;
import java.awt.Rectangle;

public class RoiOcr {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine and load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.jpg"));
```

> **Γιατί είναι σημαντικό:**  
> Η μηχανή χρειάζεται ένα bitmap για να δουλέψει. Η παροχή λανθασμένης διαδρομής προκαλεί `FileNotFoundException`, γι’ αυτό ελέγξτε προσεκτικά την απόλυτη ή σχετική θέση. Αν η εικόνα βρίσκεται στο φάκελο resources, χρησιμοποιήστε `ClassLoader.getResourceAsStream` αντί αυτού.

### Βήμα 2: Ορισμός της **περιοχής** που θέλετε να **εξάγετε κείμενο από περιοχή**

Ένα `java.awt.Rectangle` περιγράφει την μετατόπιση X/Y και το πλάτος/ύψος της περιοχής που σας ενδιαφέρει. Οι τιμές είναι σε pixel, οπότε ίσως χρειαστεί να πειραματιστείτε λίγο με το συγκεκριμένο έγγραφό σας.

```java
        // Step 2: Define the rectangular region that contains the field to read
        Rectangle region = new Rectangle(120, 340, 560, 80); // x, y, width, height
```

> **Γιατί είναι σημαντικό:**  
> Περιορίζοντας τη μηχανή OCR σε συγκεκριμένη περιοχή, βελτιώνετε δραστικά την ακρίβεια και την ταχύτητα. Η μηχανή δεν θα σπαταλήσει χρόνο προσπαθώντας να διαβάσει ολόκληρη τη σελίδα και αποφεύγει το θόρυβο του φόντου που θα μπορούσε να αλλοιώσει το αποτέλεσμα.

### Βήμα 3: Εφαρμογή της περιοχής στη μηχανή

Το αντικείμενο `RecognitionSettings` περιέχει όλες τις ρυθμίσεις που μπορείτε να προσαρμόσετε. Εδώ απλώς ορίζουμε την περιοχή που δημιουργήσαμε μόλις πριν.

```java
        // Step 3: Apply the region to the engine so only this area is processed
        engine.getRecognitionSettings().setRegion(region);
```

> **Συμβουλή:** Αν χρειαστεί ποτέ να επεξεργαστείτε πολλαπλά πεδία, μπορείτε να καλέσετε `setRegion` επανειλημμένα μέσα σε βρόχο, ενημερώνοντας το rectangle κάθε φορά πριν καλέσετε `recognize()`.

### Βήμα 4: Εκτέλεση του OCR – η μηχανή θα ευθυγραμμίσει αυτόματα την περιοχή

Η κλήση `recognize()` κάνει το σκληρό έργο: διορθώνει την κλίση, κάνει δυαδικοποίηση και τρέχει τον αναγνώστη χαρακτήρων στην καθορισμένη περιοχή.

```java
        // Step 4: Perform recognition (the engine will deskew the region automatically)
        OcrResult result = engine.recognize();
```

> **Γιατί είναι σημαντικό:**  
> Η διόρθωση κλίσης (deskew) επιλύει κοινά προβλήματα όπου η σαρωμένη φόρμα δεν είναι τέλεια ευθυγραμμισμένη. Χωρίς αυτή τη λειτουργία, μπορεί να εμφανιστούν ακατανόητοι χαρακτήρες ακόμη και αν η περιοχή είναι σωστή.

### Βήμα 5: **Εξαγωγή κειμένου από περιοχή** και εμφάνιση

Τέλος, παίρνουμε την αναπαράσταση plain‑text από το `OcrResult`. Η μέθοδος `trim()` αφαιρεί τυχόν περιττές αλλαγές γραμμής και κενά.

```java
        // Step 5: Output the extracted text
        System.out.println("Field value: " + result.getText().trim());
    }
}
```

Η εκτέλεση του προγράμματος εκτυπώνει κάτι σαν:

```
Field value: 12345-AB
```

Αυτή είναι η πλήρης διαδικασία: **φόρτωση εικόνας για OCR**, περιορισμός της σάρωσης, και **εξαγωγή κειμένου από περιοχή**.

## Πλήρες, εκτελέσιμο παράδειγμα (χωρίς ελλείψεις)

Αν προτιμάτε να αντιγράψετε‑και‑επικολλήσετε τα πάντα μονομιάς, εδώ είναι η ολοκληρωμένη κλάση, συμπεριλαμβανομένων των δηλώσεων import και ενός ελάχιστου αποσπάσματος `pom.xml` για χρήστες Maven.

```java
// File: RoiOcr.java
import com.aspose.ocr.*;
import java.awt.Rectangle;

public class RoiOcr {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine and load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.jpg"));

        // Step 2: Define the rectangular region that contains the field to read
        Rectangle region = new Rectangle(120, 340, 560, 80); // x, y, width, height

        // Step 3: Apply the region to the engine so only this area is processed
        engine.getRecognitionSettings().setRegion(region);

        // Step 4: Perform recognition (the engine will deskew the region automatically)
        OcrResult result = engine.recognize();

        // Step 5: Output the extracted text
        System.out.println("Field value: " + result.getText().trim());
    }
}
```

```xml
<!-- pom.xml excerpt -->
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ocr-demo</artifactId>
    <version>1.0.0</version>
    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-ocr</artifactId>
            <version>23.10</version>
        </dependency>
    </dependencies>
</project>
```

Αποθηκεύστε το αρχείο Java, τρέξτε `mvn compile exec:java -Dexec.mainClass=RoiOcr`, και θα δείτε την εξαγόμενη τιμή να εμφανίζεται στην κονσόλα.

![Διάγραμμα που δείχνει πώς να φορτώσετε εικόνα για OCR και να ορίσετε μια περιοχή](/images/ocr-region-diagram.png "παράδειγμα φόρτωσης εικόνας για OCR")

*Η παραπάνω εικονογράφηση απεικονίζει το ορθογώνιο (120, 340, 560, 80) πάνω σε ένα δείγμα φόρμας.*

## Διαχείριση κοινών περιπτώσεων άκρων

| Κατάσταση | Τι να προσέξετε | Γρήγορη λύση |
|-----------|-------------------|--------------|
| **Η εικόνα είναι περιστραμμένη περισσότερο από 15°** | Η λειτουργία deskew λειτουργεί καλύτερα για ήπιες γωνίες. | Προ‑περιστρέψτε την εικόνα με `java.awt.Image` πριν τη δώσετε στη μηχανή. |
| **Η περιοχή βγαίνει εκτός των ορίων της εικόνας** | Θα πεταχτεί `IllegalArgumentException`. | Επαληθεύστε ότι `region.x + region.width <= imageWidth` και αντίστοιχα για το Y. |
| **Κείμενο χαμηλής αντίθεσης** | Η ακρίβεια του OCR μειώνεται. | Αυξήστε την αντίθεση προγραμματιστικά ή χρησιμοποιήστε `engine.getRecognitionSettings().setPreprocessOptions(PreprocessOptions.CONTRAST_ENHANCEMENT)`. |
| **Πολλαπλές γλώσσες** | Η προεπιλεγμένη γλώσσα είναι τα Αγγλικά. | Καλέστε `engine.getRecognitionSettings().setLanguage(Language.FRENCH)` ή παρέχετε λίστα γλωσσών. |

## Συμβουλές για παραγωγική OCR

1. **Cache the engine** – η δημιουργία νέου `OcrEngine` για κάθε εικόνα είναι δαπανηρή. Επαναχρησιμοποιήστε ένα μόνο αντικείμενο όταν επεξεργάζεστε πολλές εικόνες.

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή κειμένου από εικόνες – Βασικά OCR με Aspose.OCR για Java](/ocr/english/java/ocr-basics/)
- [Εξαγωγή κειμένου από εικόνα Java με λειτουργία ανίχνευσης περιοχών του Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Πώς να κάνετε OCR κείμενο εικόνας με γλώσσα χρησιμοποιώντας Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}