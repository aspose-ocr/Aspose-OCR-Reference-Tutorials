---
category: general
date: 2026-05-25
description: Πώς να αποκτήσετε OCR σε Java και να εξάγετε ακατέργαστο κείμενο από
  εικόνες. Μάθετε πώς να απενεργοποιήσετε τη διόρθωση ορθογραφίας, να αναγνωρίζετε
  χειρόγραφο κείμενο και πώς να φορτώνετε την εικόνα αποδοτικά.
draft: false
keywords:
- how to get ocr
- extract raw text
- turn off spell correction
- recognize handwritten text
- how to load image
language: el
og_description: Πώς να αποκτήσετε OCR σε Java και να εξάγετε ακατέργαστο κείμενο από
  μια εικόνα. Αυτός ο οδηγός δείχνει πώς να απενεργοποιήσετε τη διόρθωση ορθογραφίας,
  να αναγνωρίσετε χειρόγραφο κείμενο και πώς να φορτώσετε σωστά την εικόνα.
og_title: Πώς να αποκτήσετε OCR στη Java – Εξαγωγή ακατέργαστου κειμένου βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: How to get OCR in Java and extract raw text from images. Learn to turn
    off spell correction, recognize handwritten text, and how to load image efficiently.
  headline: How to Get OCR in Java – Complete Guide to Extract Raw Text
  type: TechArticle
- description: How to get OCR in Java and extract raw text from images. Learn to turn
    off spell correction, recognize handwritten text, and how to load image efficiently.
  name: How to Get OCR in Java – Complete Guide to Extract Raw Text
  steps:
  - name: Maven Dependency
    text: If you’re using Maven, paste this into your `pom.xml`. It pulls the latest
      Aspose.OCR library (as of May 2026).
  - name: Gradle Alternative
    text: '```gradle implementation ''com.aspose:aspose-ocr:23.11'' ```'
  - name: Expected Output
    text: 'Assuming `handwritten.png` contains the phrase *“Hello World”* written
      in cursive, you’ll see something like:'
  type: HowTo
tags:
- OCR
- Java
- Aspose.OCR
title: Πώς να αποκτήσετε OCR στη Java – Πλήρης οδηγός για την εξαγωγή ακατέργαστου
  κειμένου
url: /el/java/advanced-ocr-techniques/how-to-get-ocr-in-java-complete-guide-to-extract-raw-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Λάβετε OCR σε Java – Πλήρης Οδηγός για την Εξαγωγή Ακατέργαστου Κειμένου

Έχετε αναρωτηθεί ποτέ **πώς να λάβετε OCR** αποτελέσματα χωρίς τον αυτόματο καθαρισμό της βιβλιοθήκης; Ίσως να δουλεύετε με ένα χειρόγραφο σημείωμα και χρειάζεστε ακριβώς τους χαρακτήρες που είδε η μηχανή, όχι μια «καλαίσθητη» έκδοση. Σε αυτό το tutorial θα περάσουμε από ένα πρακτικό παράδειγμα που δείχνει ακριβώς **πώς να λάβετε OCR** έξοδο, πώς να **εξάγετε ακατέργαστο κείμενο**, και γιατί ίσως θελήσετε να **απενεργοποιήσετε τη διόρθωση ορθογραφίας** όταν αναγνωρίζετε χειρόγραφο κείμενο. Στο τέλος θα γνωρίζετε επίσης **πώς να φορτώσετε εικόνα** αρχεία στη μηχανή Aspose OCR χωρίς προβλήματα.

Θα χρησιμοποιήσουμε το Aspose.OCR για Java, αλλά οι έννοιες ισχύουν για οποιοδήποτε OCR SDK που προσφέρει διακόπτη διόρθωσης ορθογραφίας. Χωρίς βαριά θεωρία—απλώς μια πρακτική, αντιγραφή‑και‑επικόλληση λύση που μπορείτε να τρέξετε σήμερα.

---

## Τι Θα Μάθετε

- Πώς να ρυθμίσετε το Aspose.OCR σε ένα έργο Java  
- Τα ακριβή βήματα **πώς να λάβετε OCR** ακατέργαστη έξοδο  
- Γιατί και **πώς να απενεργοποιήσετε τη διόρθωση ορθογραφίας** για ακατέργαστο κείμενο  
- Ο καλύτερος τρόπος **πώς να φορτώσετε εικόνα** αρχεία για βέλτιστη αναγνώριση  
- Πώς να **αναγνωρίσετε χειρόγραφο κείμενο** και να επαληθεύσετε το αποτέλεσμα  

Οι προαπαιτούμενες γνώσεις είναι ελάχιστες: Java 8+ εγκατεστημένη, ένα IDE συμβατό με Maven (IntelliJ, Eclipse ή VS Code) και ένα δείγμα εικόνας που περιέχει χειρόγραφους χαρακτήρες. Αν λείπει κάτι από αυτά, απλώς κατεβάστε το JDK από την Oracle και τη φωτογραφία από το τηλέφωνό σας—δεν υπάρχει πρόβλημα.

---

![Διάγραμμα που απεικονίζει τη ροή εργασίας OCR, δείχνοντας πώς να λάβετε ακατέργαστο κείμενο OCR από μια εικόνα](/images/ocr-workflow.png){: .center alt="πώς να λάβετε ακατέργαστο κείμενο OCR ροή εργασίας"}

---

## Βήμα 1: Προσθέστε το Aspose.OCR στο Έργο Σας

### Maven Dependency

Αν χρησιμοποιείτε Maven, επικολλήστε αυτό στο `pom.xml`. Θα κατεβάσει την πιο πρόσφατη βιβλιοθήκη Aspose.OCR (από Μάιο 2026).

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.11</version>
</dependency>
```

> **Pro tip:** Πάντα ελέγχετε το επίσημο αποθετήριο Maven της Aspose για νεότερες εκδόσεις. Η έκδοση `23.11` προσθέτει καλύτερη υποστήριξη για καλλιγραφικά σενάρια, κάτι που είναι χρήσιμο όταν **αναγνωρίζετε χειρόγραφο κείμενο**.

### Gradle Alternative

```gradle
implementation 'com.aspose:aspose-ocr:23.11'
```

Μόλις η εξάρτηση λυθεί, είστε έτοιμοι να γράψετε κώδικα που πραγματικά **λαμβάνει OCR** αποτελέσματα.

---

## Βήμα 2: Δημιουργήστε το Αντικείμενο OCR Engine

Η μηχανή είναι η καρδιά της διαδικασίας. Η δημιουργία της είναι απλή, αλλά η πραγματική μαγεία ξεκινά όταν την διαμορφώσετε.

```java
import com.aspose.ocr.*;

public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 2.1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();
```

Γιατί χρειάζεται ένα ξεχωριστό αντικείμενο `OcrEngine`; Αποθηκεύει όλες τις επιλογές χρόνου εκτέλεσης, συμπεριλαμβανομένου του διακόπτη διόρθωσης ορθογραφίας που θα χρησιμοποιήσουμε αμέσως μετά. Η απομόνωση της μηχανής επιτρέπει επίσης την εκτέλεση πολλαπλών αναγνωρίσεων παράλληλα χωρίς αλληλοεπικάλυψη.

---

## Βήμα 3: Απενεργοποιήστε τη Διόρθωση Ορθογραφίας (Αν Χρειάζεστε Ακατέργαστη Έξοδο)

Οι περισσότερες βιβλιοθήκες OCR προσπαθούν να βοηθήσουν διορθώνοντας αυτόματα τις λανθασμένες λέξεις. Αυτό είναι εξαιρετικό για τυπωμένο κείμενο, αλλά καταστροφικό για εξαγωγή ακατέργαστων δεδομένων. Να πώς **απενεργοποιείτε τη διόρθωση ορθογραφίας**:

```java
        // Step 3: Turn off the built‑in spell‑corrector to get raw text
        engine.getEngineOptions().setSpellCorrectorEnabled(false);
```

Όταν η σημαία είναι `false`, η μηχανή επιστρέφει ακριβώς αυτό που είδε στο bitmap, διατηρώντας τις αλλαγές γραμμής, τη στίξη και ακόμη και τυχόν τυχαία σύμβολα. Αυτό είναι απαραίτητο όταν αργότερα τροφοδοτείτε την έξοδο σε μια αλυσίδα μηχανικής μάθησης που αναμένει το αρχικό «θόρυβο».

---

## Βήμα 4: Φορτώστε την Εικόνα – Ο Σωστός Τρόπος

Μπορεί να νομίζετε ότι `engine.getImage().loadFromFile("path")` αρκεί, αλλά υπάρχουν μερικές λεπτομέρειες:

1. **Απόλυτες vs. σχετικές διαδρομές** – Χρησιμοποιήστε `Paths.get(...)` για ανεξαρτησία πλατφόρμας.  
2. **Υποστηριζόμενες μορφές** – Το Aspose.OCR διαχειρίζεται PNG, JPEG, BMP, TIFF και GIF.  
3. **Η ανάλυση μετρά** – Υψηλότερο DPI προσφέρει καλύτερη αναγνώριση, ειδικά για καλλιγραφικά.

Ακολουθεί ένα αξιόπιστο απόσπασμα κώδικα που δείχνει **πώς να φορτώσετε εικόνα** με ασφάλεια:

```java
        // Step 4: Load the image that contains handwritten text
        String imagePath = "YOUR_DIRECTORY/handwritten.png";
        // Validate the file exists
        java.nio.file.Path path = java.nio.file.Paths.get(imagePath);
        if (!java.nio.file.Files.exists(path)) {
            throw new IllegalArgumentException("Image file not found: " + imagePath);
        }

        // Load the image into the OCR engine
        engine.getImage().loadFromFile(path.toAbsolutePath().toString());
```

Αν δουλεύετε με ροή (π.χ. ανεβάζετε από φόρμα web), αντικαταστήστε το `loadFromFile` με `loadFromStream`. Το βασικό μάθημα: πάντα επαληθεύετε το αρχείο πριν το δώσετε στη μηχανή, γιατί ένα ελλιπές αρχείο προκαλεί ένα ασαφές `NullPointerException` που είναι δύσκολο να εντοπιστεί.

---

## Βήμα 5: Εκτελέστε την Αναγνώριση

Τώρα έρχεται η στιγμή της αλήθειας—**πώς να λάβετε OCR** αποτελέσματα. Η μέθοδος `recognize()` εκτελεί την εσωτερική αλυσίδα, εφαρμόζοντας μοντέλα γλώσσας, τμηματοποίηση και (αν είναι ενεργοποιημένη) διόρθωση ορθογραφίας. Εφόσον την απενεργοποιήσαμε, θα λάβετε τους ακατέργαστους χαρακτήρες.

```java
        // Step 5: Perform OCR recognition
        OcrResult result = engine.recognize();
```

Το αντικείμενο `OcrResult` περιέχει περισσότερα από απλό κείμενο· μπορείτε επίσης να ανακτήσετε βαθμολογίες εμπιστοσύνης, περιοριστικά πλαίσια και ακόμη πιθανότητες ανά χαρακτήρα. Για αυτό το tutorial εστιάζουμε στο απλό κείμενο.

---

## Βήμα 6: Εκτυπώστε το Ακατέργαστο OCR Αποτέλεσμα

Τέλος, εκτυπώστε το αποτέλεσμα στην κονσόλα. Αυτός είναι ο πιο απλός τρόπος να **εξάγετε ακατέργαστο κείμενο** για αποσφαλμάτωση ή επεξεργασία σε επόμενο στάδιο.

```java
        // Step 6: Output the raw OCR result
        System.out.println("Raw OCR output:");
        System.out.println(result.getText());
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Υποθέτοντας ότι το `handwritten.png` περιέχει τη φράση *«Hello World»* γραμμένη καλλιγραφικά, θα δείτε κάτι όπως:

```
Raw OCR output:
H e l l o   W o r l d
```

Παρατηρήστε τα επιπλέον κενά—είναι σκόπιμα επειδή η μηχανή διατηρεί την ακριβή απόσταση που ανίχνευσε. Αν αργότερα χρειαστεί να συμπτύξετε τα κενά, κάντε το στο δικό σας βήμα μετα-επεξεργασίας.

---

## Συνηθισμένα Πόδια & Πώς να Τα Αποφύγετε

| Πρόβλημα | Γιατί Συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| **Κενή συμβολοσειρά** | DPI εικόνας πολύ χαμηλό ή η εικόνα είναι εντελώς λευκή. | Βεβαιωθείτε ότι η πηγή εικόνας είναι τουλάχιστον 300 DPI· χρησιμοποιήστε `engine.getImage().setResolution(300, 300)`. |
| **Ασυνήθιστα σύμβολα** | Λάθος μορφή αρχείου ή κατεστραμμένα bytes. | Επαληθεύστε το αρχείο με προβολέα εικόνας· εξάγετε ξανά ως PNG. |
| **Διόρθωση ορθογραφίας ενεργή** | Ενδεχομένως ενεργοποιήθηκε ξανά κάπου στον κώδικα. | Κρατήστε την κλήση `setSpellCorrectorEnabled(false)` αμέσως μετά τη δημιουργία της μηχανής. |
| **Χειρόγραφο κείμενο δεν αναγνωρίζεται** | Η προεπιλεγμένη γλώσσα της μηχανής είναι για τυπωμένο αγγλικό κείμενο. | Καλέστε `engine.getEngineOptions().setLanguage(Language.English);` και προαιρετικά `engine.getEngineOptions().setUseDictionary(false);`. |

---

## Επέκταση του Παραδείγματος: Αναγνώριση Χειρόγραφου Κειμένου

Αν η περίπτωση χρήσης σας στοχεύει ειδικά στο **αναγνωρίσετε χειρόγραφο κείμενο**, μπορείτε να ρυθμίσετε μερικές επιλογές για καλύτερη ακρίβεια:

```java
        // Enable handwritten mode (available in 23.11+)
        engine.getEngineOptions().setRecognitionMode(RecognitionMode.Handwritten);
```

Αυτό ενημερώνει το εσωτερικό νευρωνικό δίκτυο να προτιμά καλλιγραφικά μοτίβα αντί για τυπωμένα. Στην πράξη, θα δείτε σημαντική αύξηση στις βαθμολογίες εμπιστοσύνης για υπογραφές, σημειώσεις ή γρήγορα σκίτσα.

---

## Πλήρες Παράδειγμα (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω βρίσκεται η ολοκληρωμένη, αυτόνομη κλάση Java που ενσωματώνει όλα τα βήματα που συζητήσαμε. Απλώς αντικαταστήστε το `YOUR_DIRECTORY/handwritten.png` με τη διαδρομή της δικής σας εικόνας και τρέξτε το.

```java
import com.aspose.ocr.*;

import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create OCR engine
        OcrEngine engine = new OcrEngine();

        // 2️⃣ Turn off spell correction to get raw output
        engine.getEngineOptions().setSpellCorrectorEnabled(false);

        // Optional: set handwritten mode if needed
        // engine.getEngineOptions().setRecognitionMode(RecognitionMode.Handwritten);

        // 3️⃣ Load the image (how to load image safely)
        String imagePath = "YOUR_DIRECTORY/handwritten.png";
        Path path = Paths.get(imagePath);
        if (!Files.exists(path)) {
            throw new IllegalArgumentException("Image file not found: " + imagePath);
        }
        engine.getImage().loadFromFile(path.toAbsolutePath().toString());

        // 4️⃣ Perform OCR (how to get OCR raw text)
        OcrResult result = engine.recognize();

        // 5️⃣ Print raw result (extract raw text)
        System.out.println("Raw OCR output:");
        System.out.println(result.getText());
    }
}
```

Τρέξτε το με:

```bash
mvn compile exec:java -Dexec.mainClass=SpellCorrectDemo
```

Θα πρέπει να δείτε τους ακατέργαστους χαρακτήρες εκτυπωμένους ακριβώς όπως τους διάβασε η μηχανή.

---

## Συμπέρασμα

Καλύψαμε **πώς να λάβετε OCR** ακατέργαστα αποτελέσματα σε Java, δείξαμε τον σωστό τρόπο **να απενεργοποιήσετε τη διόρθωση ορθογραφίας**, παρουσιάσαμε την βέλτιστη πρακτική **πώς να φορτώσετε εικόνα**, και εξηγήσαμε τις λεπτομέρειες του **αναγνωρίστε χειρόγραφο κείμενο**. Ακολουθώντας αυτά τα βήματα, θα μπορείτε να **εξάγετε ακατέργαστο κείμενο** αξιόπιστα, είτε χτίζετε μια γραμμή ψηφιοποίησης εγγράφων, ένα εργαλείο δικαστικής ανάλυσης, ή μια απλή εφαρμογή σημειώσεων.

Στη συνέχεια, μπορείτε να εξερευνήσετε:

- **Μετα-επεξεργασία**: αφαίρεση κενών, κανονικοποίηση Unicode, ή τροφοδοσία της εξόδου σε μοντέλο γλώσσας.  
- **Επεξεργασία σε παρτίδες**: βρόχος πάνω από έναν φάκελο εικόνων και αποθήκευση αποτελεσμάτων σε βάση δεδομένων.  
- **Προχωρημένες επιλογές**: ρύθμιση `EngineOptions` για πολυγλωσσική υποστήριξη ή προσαρμοσμένα λεξικά.

Δοκιμάστε τα και μη διστάσετε να αφήσετε τις ερωτήσεις σας στα σχόλια. Καλό κώδικα, και εύχομαι το OCR σας να είναι πάντα ακριβές!

## Σχετικά Tutorials

- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}