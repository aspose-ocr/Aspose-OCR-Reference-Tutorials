---
category: general
date: 2026-02-09
description: Μάθετε πώς να αναγνωρίζετε κείμενο από εικόνα χρησιμοποιώντας το Aspose
  OCR σε Java. Αυτό το βήμα‑βήμα εκπαιδευτικό υλικό καλύπτει επίσης τον ορθογραφικό
  έλεγχο, τα προσαρμοσμένα λεξικά και τη διαμόρφωση της μηχανής OCR.
draft: false
keywords:
- recognize text from image
- Aspose OCR Java
- OCR spell checking
- custom OCR dictionary
- Java image processing
language: el
og_description: Αναγνωρίστε κείμενο από εικόνα σε Java χρησιμοποιώντας το Aspose OCR.
  Ακολουθήστε αυτόν τον οδηγό για να ενεργοποιήσετε τον έλεγχο ορθογραφίας, να ορίσετε
  τη γλώσσα και να λάβετε άμεσα διορθωμένο αποτέλεσμα.
og_title: Αναγνώριση κειμένου από εικόνα με Aspose OCR – Πλήρης οδηγός Java
tags:
- OCR
- Java
- Aspose
title: Αναγνώριση κειμένου από εικόνα με το Aspose OCR – Πλήρης οδηγός Java
url: /el/java/advanced-ocr-techniques/recognize-text-from-image-with-aspose-ocr-full-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση Κειμένου από Εικόνα – Πλήρης Java Tutorial

Έχετε ποτέ χρειαστεί να **αναγνωρίσετε κείμενο από εικόνα** αλλά δεν ήσασταν σίγουροι ποιο API να εμπιστευτείτε; Δεν είστε οι μόνοι. Σε πολλά έργα—σάρωση τιμολογίων, ψηφιοποίηση χειρόγραφων σημειώσεων ή δημιουργία αναζητήσιμου αρχείου—η δυνατότητα εξαγωγής καθαρού, αναγνώσιμου κειμένου από μια εικόνα είναι καθοριστική.  

Τα καλά νέα; Με το Aspose OCR for Java μπορείτε να το κάνετε αυτό με λίγες γραμμές κώδικα, και θα έχετε ακόμη ενσωματωμένο έλεγχο ορθογραφίας για να καθαρίσετε το αποτέλεσμα του OCR. Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία, από τη δημιουργία της μηχανής OCR μέχρι την εκτύπωση του διορθωμένου αποτελέσματος. Στο τέλος θα έχετε μια έτοιμη προς εκτέλεση κλάση Java που **αναγνωρίζει κείμενο από εικόνα** αξιόπιστα.

---

## Τι Θα Χρειαστείτε

- **Java 8+** (ο κώδικας λειτουργεί με οποιοδήποτε πρόσφατο JDK)
- **Aspose OCR for Java** library – μπορείτε να κατεβάσετε το τελευταίο JAR από το αποθετήριο Maven του Aspose ή να το κατεβάσετε απευθείας από τον ιστότοπο Aspose.
- Ένα αρχείο εικόνας που περιέχει τυπωμένο ή εκτυπωμένο κείμενο (π.χ., `typed_scanned_doc.png`).
- Μια μέτρια ποσότητα RAM· το OCR δεν είναι βαριά, αλλά ένας σωρός 1 GB είναι περισσότερο από αρκετός για τις περισσότερες σαρώσεις.

> *Συμβουλή:* Αν χρησιμοποιείτε Maven, προσθέστε την παρακάτω εξάρτηση στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

Τώρα που οι προαπαιτούμενες ενέργειες έχουν ολοκληρωθεί, ας βουτήξουμε στον κώδικα.

---

## Βήμα 1: Αρχικοποίηση της Μηχανής OCR και Λήψη της Διαμόρφωσής της

Το πρώτο που κάνετε είναι να δημιουργήσετε μια παρουσία `OcrEngine`. Αυτό το αντικείμενο είναι η καρδιά της βιβλιοθήκης· περιέχει όλες τις ρυθμίσεις που θα τροποποιήσετε αργότερα.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.enums.*;

public class SpellCheckExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and obtain its configuration object
        OcrEngine ocrEngine = new OcrEngine();
        OcrEngineConfiguration ocrConfig = ocrEngine.getConfiguration();
```

Γιατί είναι σημαντικό: Το αντικείμενο διαμόρφωσης σας δίνει άμεση πρόσβαση στην επιλογή γλώσσας, στις σημαίες ελέγχου ορθογραφίας και στις διαδρομές λεξικού. Χωρίς αυτό, θα είστε περιορισμένοι στις προεπιλογές, οι οποίες μπορεί να μην ταιριάζουν με το υλικό σας.

## Βήμα 2: Επιλογή Γλώσσας και Ενεργοποίηση Ελέγχου Ορθογραφίας

Στη συνέχεια, ενημερώστε τη μηχανή ποια γλώσσα περιμένετε στην εικόνα. Εδώ επιλέγουμε τα Αγγλικά, αλλά το Aspose υποστηρίζει δεκάδες τοπικές ρυθμίσεις.

```java
        // Step 2: Choose the language for recognition and turn on spell‑checking
        ocrConfig.setLanguage(Language.ENGLISH);
        ocrConfig.setSpellCheckEnabled(true);
```

Η ενεργοποίηση του ελέγχου ορθογραφίας είναι προαιρετική, αλλά βελτιώνει δραματικά την αναγνωσιμότητα του αποτελέσματος—ιδιαίτερα για σαρωμένα έγγραφα όπου η μηχανή OCR μπορεί να ερμηνεύσει λανθασμένα το “0” ως “O”.  

## Βήμα 3: (Προαιρετικό) Φόρτωση Προσαρμοσμένου Λεξικού Ελέγχου Ορθογραφίας

Αν εργάζεστε με ειδική ορολογία κλάδου—π.χ. ιατρικούς όρους, νομικές συντομογραφίες ή προσαρμοσμένους κωδικούς προϊόντων—το Aspose σας επιτρέπει να ενσωματώσετε το δικό σας λεξικό.

```java
        // Step 3: (Optional) Provide a custom spell‑check dictionary
        ocrConfig.setSpellCheckDictionary("en_US"); // use a locale‑specific dictionary
```

Μπορείτε επίσης να κατευθύνετε το `setSpellCheckDictionary` σε ένα αρχείο `.dic` με πλήρη διαδρομή εάν έχετε μια προσαρμοσμένη λίστα. Η μηχανή θα συγχωνεύσει τις προσαρμοσμένες λέξεις σας με το ενσωματωμένο λεξικό, διασφαλίζοντας ότι η ορολογία του τομέα παραμένει αμετάβλητη.

## Βήμα 4: Εκτέλεση OCR στο Αρχείο Εικόνας σας

Τώρα αρχίζει η πραγματική δουλειά. Δώστε τη διαδρομή στην εικόνα σας και αφήστε τη μηχανή να κάνει τη μαγεία της.

```java
        // Step 4: Run OCR on the input image file
        RecognitionResult recognitionResult = ocrEngine.recognize("YOUR_DIRECTORY/typed_scanned_doc.png");
```

Πίσω από τη σκηνή, το Aspose εφαρμόζει μια σειρά βημάτων προεπεξεργασίας—ευθυγράμμιση, δυαδικοποίηση και διαχωρισμό χαρακτήρων—πριν περάσει τα δεδομένα εικονοστοιχείων στον αναγνωριστή νευρωνικού δικτύου του. Το αποτέλεσμα τυλίγεται σε ένα αντικείμενο `RecognitionResult` που περιέχει τόσο το ακατέργαστο όσο και το διορθωμένο κείμενο.

## Βήμα 5: Εμφάνιση του Διορθωμένου Κειμένου

Τέλος, εκτυπώστε τη καθαρισμένη συμβολοσειρά στην κονσόλα. Θα δείτε το αποτέλεσμα του OCR **με εφαρμοσμένο έλεγχο ορθογραφίας**, το οποίο συχνά είναι έτοιμο να αποθηκευτεί απευθείας σε μια βάση δεδομένων ή να τροφοδοτηθεί σε ευρετήριο αναζήτησης.

```java
        // Step 5: Display the corrected text returned by the engine
        System.out.println("Corrected text:");
        System.out.println(recognitionResult.getText());
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Υποθέτοντας ότι το `typed_scanned_doc.png` περιέχει την πρόταση *«The quick brown fox jumps over the lazy dog.»*, η κονσόλα θα εμφανίσει:

```
Corrected text:
The quick brown fox jumps over the lazy dog.
```

Αν η αρχική σάρωση είχε μια λεκέ που μετέτρεψε το “quick” σε “qu1ck”, ο ελεγκτής ορθογραφίας θα το διορθώσει αυτόματα πίσω σε “quick”.

## Διαχείριση Συνηθισμένων Περιπτώσεων Άκρων

### 1. Εικόνες Χαμηλής Ανάλυσης

Η ακρίβεια του OCR μειώνεται απότομα κάτω από 150 dpi. Εάν οι πηγές εικόνων σας είναι χαμηλής ανάλυσης, σκεφτείτε να τις αυξήσετε πρώτα (π.χ., με OpenCV) ή ζητήστε μια σάρωση υψηλότερης ποιότητας.  

### 2. Πολυγλωσσικά Έγγραφα

Το Aspose OCR μπορεί να αλλάζει γλώσσες εν κινήσει, αλλά πρέπει να ορίσετε το κατάλληλο enum `Language` πριν από κάθε κλήση `recognize`. Για σελίδες με μεικτές γλώσσες, ίσως χρειαστεί να τρέξετε την εικόνα στη μηχανή δύο φορές—μία για κάθε γλώσσα—και έπειτα να συγχωνεύσετε τα αποτελέσματα.

### 3. Μεγάλα PDF ή Πολυσελιδικά TIFF

Αν χρειάζεται να **αναγνωρίσετε κείμενο από εικόνα** αρχεία ενσωματωμένα σε PDF, εξάγετε κάθε σελίδα ως εικόνα (χρησιμοποιώντας Aspose PDF ή άλλη βιβλιοθήκη) και τροφοδοτήστε τις ξεχωριστά στη μηχανή OCR. Η μηχανή είναι χωρίς κατάσταση, έτσι μπορείτε να επαναχρησιμοποιήσετε την ίδια παρουσία `OcrEngine` σε πολλές σελίδες.

### 4. Προσαρμογή Ευαισθησίας Ελέγχου Ορθογραφίας

Το προεπιλεγμένο όριο ελέγχου ορθογραφίας λειτουργεί για τα περισσότερα αγγλικά κείμενα. Για ιδιαίτερα τεχνικά έγγραφα μπορείτε να μειώσετε την ευαισθησία τροποποιώντας το εσωτερικό `SpellCheckOptions`—αν και αυτό απαιτεί εμβάθυνση στο προχωρημένο API του Aspose, κάτι που υπερβαίνει το εύρος αυτού του οδηγού για αρχάριους.

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω βρίσκεται η πλήρης κλάση Java, έτοιμη για μεταγλώττιση και εκτέλεση. Αντικαταστήστε το `YOUR_DIRECTORY/typed_scanned_doc.png` με την πραγματική διαδρομή στην εικόνα σας.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.enums.*;

public class SpellCheckExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and obtain its configuration object
        OcrEngine ocrEngine = new OcrEngine();
        OcrEngineConfiguration ocrConfig = ocrEngine.getConfiguration();

        // Step 2: Choose the language for recognition and turn on spell‑checking
        ocrConfig.setLanguage(Language.ENGLISH);
        ocrConfig.setSpellCheckEnabled(true);

        // Step 3: (Optional) Provide a custom spell‑check dictionary
        ocrConfig.setSpellCheckDictionary("en_US"); // or a full path to your .dic file

        // Step 4: Run OCR on the input image file
        RecognitionResult recognitionResult = ocrEngine.recognize("YOUR_DIRECTORY/typed_scanned_doc.png");

        // Step 5: Display the corrected text returned by the engine
        System.out.println("Corrected text:");
        System.out.println(recognitionResult.getText());
    }
}
```

Μεταγλώττιση με:

```bash
javac -cp "path/to/aspose-ocr.jar" SpellCheckExample.java
java -cp ".;path/to/aspose-ocr.jar" SpellCheckExample
```

Θα πρέπει να δείτε το διορθωμένο κείμενο να εκτυπώνεται στην κονσόλα, επιβεβαιώνοντας ότι έχετε επιτυχώς **αναγνωρίσει κείμενο από εικόνα** και έχετε εφαρμόσει έλεγχο ορθογραφίας.

## Συχνές Ερωτήσεις

**Ε: Υποστηρίζει το Aspose OCR χειρόγραφη γραφή;**  
Α: Η βιβλιοθήκη είναι βελτιστοποιημένη για τυπωμένο κείμενο. Η αναγνώριση χειρόγραφου είναι διαθέσιμη σε ξεχωριστό module (`aspose-ocr-handwriting`), το οποίο μπορείτε να ενσωματώσετε με παρόμοιο τρόπο.

**Ε: Μπορώ να επεξεργαστώ εικόνες από URL αντί για τοπικό αρχείο;**  
Α: Ναι. Κατεβάστε την εικόνα σε προσωρινή μνήμη (π.χ., χρησιμοποιώντας `java.net.URL`) και περάστε το byte array στο `ocrEngine.recognize(InputStream)`.

**Ε: Τι γίνεται αν χρειαστεί να εξάγω μόνο συγκεκριμένες περιοχές της εικόνας;**  
Α: Χρησιμοποιήστε `ocrEngine.setRegion(Rectangle)` πριν καλέσετε το `recognize`. Αυτό περιορίζει το OCR στο καθορισμένο ορθογώνιο, εξοικονομώντας χρόνο και μειώνοντας τα ψευδώς θετικά.

## Συμπέρασμα

Μόλις περάσαμε από ένα πλήρες, ολοκληρωμένο παράδειγμα για το πώς να **αναγνωρίσετε κείμενο από εικόνα** χρησιμοποιώντας το Aspose OCR for Java. Διαμορφώνοντας τη μηχανή OCR, ενεργοποιώντας τον έλεγχο ορθογραφίας και προαιρετικά φορτώνοντας ένα προσαρμοσμένο λεξικό, μπορείτε να μετατρέψετε θορυβώδεις σαρώσεις σε καθαρό, αναζητήσιμο κείμενο με ελάχιστο κώδικα.

Από εδώ μπορείτε να εξερευνήσετε:

- **Batch processing** – επανάληψη πάνω σε φάκελο εικόνων και αποθήκευση κάθε αποτελέσματος σε μια βάση δεδομένων.  
- **Integration with Aspose PDF** – εξαγωγή εικόνων από PDF και τροφοδοσία τους στη μηχανή OCR.  
- **Advanced language support** – αλλαγή του `ocrConfig.setLanguage` σε `Language.FRENCH` ή `Language.SPANISH` για πολυγλωσσικά έργα.  

Δοκιμάστε το, ρυθμίστε τις παραμέτρους και δείτε πώς βελτιώνεται η ποιότητα για τη δική σας περίπτωση χρήσης. Καλή προγραμματιστική δουλειά, και οι σαρώσεις σας να είναι πάντα καθαρές!  

![Διάγραμμα που δείχνει τη ροή εργασίας OCR για την αναγνώριση κειμένου από εικόνα](/images/ocr-workflow.png "ροή εργασίας αναγνώρισης κειμένου από εικόνα")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}