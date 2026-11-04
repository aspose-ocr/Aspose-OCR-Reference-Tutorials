---
category: general
date: 2026-09-23
description: Μάθετε πώς να εκτελείτε OCR σε εικόνες σε Java χρησιμοποιώντας Aspose
  OCR, εξάγετε κείμενο από την εικόνα και ενεργοποιήστε τη διόρθωση ορθογραφίας με
  προσαρμοσμένο λεξικό.
draft: false
keywords:
- how to perform ocr
- how to extract text from image
- java ocr maven dependency
- java image to text conversion
- aspose ocr java
lastmod: 2026-09-23
og_description: Πώς να εκτελέσετε OCR σε εικόνες σε Java με Aspose OCR. Αυτός ο οδηγός
  δείχνει πώς να φορτώνετε μια εικόνα, να εξάγετε κείμενο από την εικόνα και να προσθέτετε
  διόρθωση ορθογραφίας για ακριβή αποτελέσματα.
og_image_alt: 'Aspose OCR Java tutorial: extracting text from images with spell correction'
og_title: Πώς να εκτελέσετε OCR σε εικόνες με Aspose OCR σε Java
schemas:
- author: Aspose
  dateModified: '2026-09-23'
  description: Learn how to perform OCR on images in Java using Aspose OCR, extract
    text from image, and enable spell correction with a custom dictionary.
  headline: How to perform OCR on images with Aspose OCR in Java
  type: TechArticle
- description: Learn how to perform OCR on images in Java using Aspose OCR, extract
    text from image, and enable spell correction with a custom dictionary.
  name: How to perform OCR on images with Aspose OCR in Java
  steps:
  - name: set up the project and import dependencies
    text: Add the Aspose OCR Maven dependency to your `pom.xml`. This single line
      pulls in the core OCR engine and all required transitive libraries. > **Pro
      tip:** Verify the version number on Maven Central; newer releases add language
      packs and performance improvements.
  - name: load the image for OCR
    text: '`OcrEngine` works with any `InputStream`. Use `ImageStream` to wrap a file
      path, byte array, or URL. **Definition anchor:** `ImageStream` is Aspose OCR’s
      lightweight wrapper that reads image data from various sources without converting
      it to a `BufferedImage` first.'
  - name: enable spell‑correction (optional but powerful)
    text: Turn on the built‑in spell‑correction flag to automatically fix common OCR
      mis‑recognitions such as “l” vs “1”. Spell‑correction can improve accuracy by
      up to **80 %** on low‑contrast scans, turning “Inv0ice” into “Invoice” without
      extra code.
  - name: provide a custom dictionary (tailor the engine)
    text: Supply a plain‑text dictionary for industry‑specific terminology—medical
      codes, legal terms, product SKUs, etc. **Definition anchor:** `CustomDictionary`
      loads a UTF‑8 word list that the OCR engine consults during post‑processing
      to prefer your domain vocabulary.
  - name: run the OCR process
    text: Invoke `process()` to get an `OcrResult` containing the recognized text,
      confidence scores, and optional layout data. If an error occurs, `ocrResult.getErrorMessage()`
      returns a detailed description you can log or display.
  - name: output the recognized (and corrected) text
    text: 'Print the extracted string to the console or write it to a file. For quick
      testing, a simple `System.out.println` is sufficient. Running the program should
      produce clean, searchable text similar to: If you notice stray characters, revisit
      your custom dictionary and consider pre‑processing the image '
  type: HowTo
- questions:
  - answer: No. The library runs entirely offline; all recognition happens locally
      on your JVM.
    question: Does Aspose OCR require an internet connection?
  - answer: Aspose OCR supports Java 8 through Java 21, including both standard and
      OpenJDK distributions.
    question: Which Java versions are supported?
  - answer: Yes. The engine streams data and can handle images up to 500 MB, limited
      only by available heap memory.
    question: Can I process images larger than 10 MB?
  - answer: Purchase a commercial license from the Aspose store and set the license
      file with `License license = new License(); license.setLicense("Aspose.OCR.lic");`.
    question: How do I license Aspose OCR for production?
  - answer: Aspose OCR includes a handwriting mode that can be enabled via `ocrEngine.getEngineOptions().setHandwriting(true);`,
      improving accuracy on cursive scripts.
    question: Is there built‑in support for handwritten text?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
- image to text
- OCR Maven dependency
title: Πώς να εκτελέσετε OCR σε εικόνες με Aspose OCR σε Java
url: /el/java/advanced-ocr-techniques/perform-ocr-on-image-with-aspose-ocr-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτελέστε OCR σε εικόνα – πλήρης οδηγός Java

Αν ψάχνετε για έναν αξιόπιστο τρόπο να **how to perform OCR** σε αρχεία εικόνας χρησιμοποιώντας Java, βρίσκεστε στο σωστό μέρος. Με το Aspose OCR for Java μπορείτε να εξάγετε κείμενο από εικόνες με λίγες γραμμές κώδικα, να βελτιώσετε την ακρίβεια με ένα προσαρμοσμένο λεξικό και να ενεργοποιήσετε τη διόρθωση ορθογραφίας για να καθαρίσετε θορυβώδεις σάρωση. Αυτό το tutorial σας οδηγεί βήμα‑βήμα—από τη φόρτωση της εικόνας για OCR έως την εκτύπωση του διορθωμένου κειμένου—ώστε να ενσωματώσετε τη μετατροπή εικόνας‑σε‑κείμενο στις εφαρμογές σας σήμερα.

## Γρήγορες απαντήσεις
- **What is the main class to start OCR?** `OcrEngine` είναι η βασική κλάση του Aspose OCR που εκτελεί την οπτική αναγνώριση χαρακτήρων.
- **Which Maven artifact adds OCR support?** Προσθέστε `com.aspose:aspose-ocr` στο `pom.xml` σας.
- **Do I need a license for development?** Μια δωρεάν προσωρινή άδεια λειτουργεί για δοκιμές· απαιτείται εμπορική άδεια για παραγωγή.
- **Can I improve accuracy on low‑quality scans?** Ναι—ενεργοποιήστε τη διόρθωση ορθογραφίας και παρέχετε ένα προσαρμοσμένο λεξικό.
- **Is multi‑page support built‑in?** Επεξεργαστείτε κάθε εικόνα σελίδας σε βρόχο· η μηχανή είναι thread‑safe για ταυτόχρονη εκτέλεση.

## Τι είναι η **how to perform OCR**;
Η φράση **how to perform OCR** αναφέρεται στη διαδικασία μετατροπής τυπωμένου ή χειρόγραφου κειμένου σε εικόνα σε επεξεργάσιμους, αναζητήσιμους ψηφιακούς χαρακτήρες χρησιμοποιώντας τεχνολογία οπτικής αναγνώρισης χαρακτήρων. Το Aspose OCR υλοποιεί αυτή τη διαδικασία με μια μονοδιάστικη μηχανή που υποστηρίζει πάνω από 20 μορφές raster και 50+ γλώσσες.

## Γιατί να χρησιμοποιήσετε το Aspose OCR για Java;
Το Aspose OCR υποστηρίζει **20+ μορφές εικόνας** (συμπεριλαμβανομένων PNG, JPEG, TIFF, BMP και GIF) και μπορεί να επεξεργαστεί **παρτίδες εκατοντάδων σελίδων** χωρίς να φορτώνει ολόκληρο το έγγραφο στη μνήμη, παρέχοντας έως **300 σελίδες ανά λεπτό** σε έναν τυπικό διακομιστή 4‑πυρήνων. Οι ενσωματωμένες λειτουργίες διόρθωσης ορθογραφίας και προσαρμοσμένου λεξικού μειώνουν τα τυπικά ποσοστά σφάλματος OCR από 12 % σε κάτω από 2 % σε θορυβώδεις τιμολόγια.

## Προαπαιτούμενα
- **Java Development Kit (JDK) 8+** – τυπικό περιβάλλον εκτέλεσης Java.
- **Aspose OCR for Java** library – αποκτήστε το πιο πρόσφατο JAR από το Maven Central ή το portal λήψεων της Aspose.
- Ένα αρχείο εικόνας (π.χ., `invoice.png`) που θέλετε να επεξεργαστείτε.
- (Προαιρετικό) `custom_dict.txt` – ένα αρχείο κειμένου UTF‑8 που περιέχει ειδικούς όρους τομέα, ένας ανά γραμμή.

Αυτό είναι ό,τι χρειάζεστε—χωρίς εξωτερικές υπηρεσίες ή βαριά πλαίσια.

## Πώς να εκτελέσετε OCR σε εικόνα με Java;
Φορτώστε την εικόνα σας, ενεργοποιήστε τη διόρθωση ορθογραφίας, προαιρετικά παρέχετε ένα προσαρμοσμένο λεξικό, εκτελέστε τη μηχανή και διαβάστε το αποτέλεσμα. Αυτή η προσέγγιση λειτουργεί για αρχεία μονής σελίδας καθώς και για επεξεργασία παρτίδας, και η μηχανή χειρίζεται αυτόματα την αποκωδικοποίηση εικόνας, την ανίχνευση γλώσσας και την αξιολόγηση εμπιστοσύνης, παρέχοντάς σας αξιόπιστη έξοδο κειμένου έτοιμη για περαιτέρω επεξεργασία. Οι παρακάτω ενότητες διασπούν κάθε βήμα με σαφείς εξηγήσεις και τον ακριβή κώδικα που χρειάζεται να αντιγράψετε.

### Βήμα 1: ρυθμίστε το έργο και εισάγετε τις εξαρτήσεις
Προσθέστε την εξάρτηση Maven του Aspose OCR στο `pom.xml` σας. Αυτή η μοναδική γραμμή φέρνει τη βασική μηχανή OCR και όλες τις απαιτούμενες μεταβατικές βιβλιοθήκες.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

> **Συμβουλή:** Επαληθεύστε τον αριθμό έκδοσης στο Maven Central· οι νεότερες εκδόσεις προσθέτουν πακέτα γλωσσών και βελτιώσεις απόδοσης.

### Βήμα 2: φορτώστε την εικόνα για OCR
`OcrEngine` λειτουργεί με οποιοδήποτε `InputStream`. Χρησιμοποιήστε `ImageStream` για να τυλίξετε μια διαδρομή αρχείου, πίνακα byte ή URL.

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 2: Load the image you wish to process
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));
```

**Definition anchor:** `ImageStream` είναι το ελαφρύ wrapper του Aspose OCR που διαβάζει δεδομένα εικόνας από διάφορες πηγές χωρίς να τα μετατρέπει πρώτα σε `BufferedImage`.

### Βήμα 3: ενεργοποιήστε τη διόρθωση ορθογραφίας (προαιρετικό αλλά ισχυρό)
Ενεργοποιήστε τη σημαία ενσωματωμένης διόρθωσης ορθογραφίας για να διορθώνονται αυτόματα κοινές λανθασμένες αναγνώσεις OCR όπως “l” vs “1”.

```java
        // Step 3: Turn on spell‑checking to improve result quality
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);
```

Η διόρθωση ορθογραφίας μπορεί να βελτιώσει την ακρίβεια έως **80 %** σε σάρωση χαμηλής αντίθεσης, μετατρέποντας το “Inv0ice” σε “Invoice” χωρίς επιπλέον κώδικα.

### Βήμα 4: παρέχετε ένα προσαρμοσμένο λεξικό (προσαρμόστε τη μηχανή)
Παρέχετε ένα απλό κείμενο λεξικό για ορολογία συγκεκριμένου κλάδου—ιατρικούς κωδικούς, νομικούς όρους, SKU προϊόντων κλπ.

```java
        // Step 4: Load a custom dictionary to boost recognition of domain terms
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));
```

**Definition anchor:** `CustomDictionary` φορτώνει μια λίστα λέξεων UTF‑8 που η μηχανή OCR συμβουλεύεται κατά τη μετα‑επεξεργασία για να προτιμήσει το λεξιλόγιο του τομέα σας.

### Βήμα 5: εκτελέστε τη διαδικασία OCR
Κληθείτε `process()` για να λάβετε ένα `OcrResult` που περιέχει το αναγνωρισμένο κείμενο, τις βαθμολογίες εμπιστοσύνης και προαιρετικά δεδομένα διάταξης.

```java
        // Step 5: Execute OCR and capture the result
        OcrResult ocrResult = ocrEngine.process();
```

Εάν προκύψει σφάλμα, `ocrResult.getErrorMessage()` επιστρέφει μια λεπτομερή περιγραφή που μπορείτε να καταγράψετε ή να εμφανίσετε.

### Βήμα 6: εξάγετε το αναγνωρισμένο (και διορθωμένο) κείμενο
Εκτυπώστε τη εξαγόμενη συμβολοσειρά στην κονσόλα ή γράψτε την σε αρχείο. Για γρήγορη δοκιμή, ένα απλό `System.out.println` αρκεί.

```java
        // Step 6: Print the corrected text to the console
        System.out.println(ocrResult.getText());
    }
}
```

Η εκτέλεση του προγράμματος θα πρέπει να παράγει καθαρό, αναζητήσιμο κείμενο παρόμοιο με:

```
Invoice Number: 12345
Date: 2023‑07‑15
Total Amount: $1,250.00
```

Εάν παρατηρήσετε ανεπιθύμητους χαρακτήρες, επανεξετάστε το προσαρμοσμένο λεξικό σας και σκεφτείτε προ‑επεξεργασία της εικόνας (αύξηση αντίθεσης, αποθορυβοποίηση ή μετατροπή σε γκρι κλίμακα).

## Πώς να εξάγετε κείμενο από εικόνα χρησιμοποιώντας προσαρμοσμένο λεξικό;
Φορτώστε το λεξικό πριν από την επεξεργασία, στη συνέχεια καλέστε `ocrEngine.setCustomDictionary(customDict)`. Η μηχανή θα δώσει προτεραιότητα στις λέξεις από τη λίστα, μειώνοντας δραστικά τα ψευδώς θετικά για εξειδικευμένα λεξιλόγια. Παρέχοντας όρους συγκεκριμένου κλάδου, βοηθάτε τον μετα‑επεξεργαστή OCR να επιλύσει ασαφείς χαρακτήρες, όπως η διάκριση μεταξύ του γράμματος “O” και του αριθμού “0”, βελτιώνοντας τη συνολική ακρίβεια σε τεχνικά έγγραφα.

## Πώς να προσθέσετε σωστά την εξάρτηση Maven java ocr;
Προσθέστε το παρακάτω απόσπασμα στο `pom.xml` σας μέσα στην ενότητα `<dependencies>`. Αυτή η εξάρτηση φέρνει τη βασική βιβλιοθήκη Aspose OCR μαζί με όλα τα απαιτούμενα μεταβατικά στοιχεία, διασφαλίζοντας ότι η μηχανή OCR μπορεί να δημιουργηθεί χωρίς πρόσθετη διαμόρφωση. Βεβαιωθείτε ότι εκτελείτε `mvn clean install` μετά την ενημέρωση του αρχείου ώστε το Maven να επιλύσει την τελευταία έκδοση από το κεντρικό αποθετήριο.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

## Συχνές ερωτήσεις & ειδικές περιπτώσεις

### Τι γίνεται αν η εικόνα είναι σε διαφορετική μορφή (PDF, TIFF, κλπ.;)
Το Aspose OCR χειρίζεται απευθείας μορφές raster. Για PDFs, εξάγετε κάθε σελίδα ως εικόνα πρώτα—το Aspose PDF for Java παρέχει `PdfExtractor` για να το κάνετε αυτό αποδοτικά. Μonce έχετε ένα `BufferedImage` ή ροή byte, η ίδια κλήση `setImage` λειτουργεί. Αυτή η προσέγγιση σας επιτρέπει να επεξεργαστείτε έγγραφα πολλαπλών σελίδων χωρίς να μετατρέψετε ολόκληρο το PDF στη μνήμη, διατηρώντας τη ροή εργασίας γρήγορη και κλιμακώσιμη.

### Πώς να διαχειριστώ έγγραφα πολλαπλών σελίδων;
Επαναλάβετε για κάθε εικόνα σελίδας, δημιουργήστε μια νέα `OcrEngine` (ή επαναρυθμίστε την υπάρχουσα) και συνδέστε τις τιμές `OcrResult.getText()`. Αυτή η προσέγγιση διατηρεί τα συμφραζόμενα ορθογραφικού ελέγχου ανεξάρτητα ανά σελίδα. Επεξεργαζόμενοι τις σελίδες διαδοχικά ή σε παράλληλα νήματα, μπορείτε να διατηρήσετε υψηλή απόδοση ενώ εξασφαλίζετε ότι κάθε σελίδα ωφελείται από το ίδιο λεξικό και τις ρυθμίσεις διόρθωσης ορθογραφίας.

### Μπορώ να περιορίσω τη γλώσσα ή το σύνολο χαρακτήρων;
Ναι. Καλέστε `ocrEngine.getEngineOptions().setLanguage(Language.English)` (ή οποιαδήποτε υποστηριζόμενη γλώσσα) για να περιορίσετε το πεδίο αναγνώρισης, κάτι που επιταχύνει την επεξεργασία έως **30 %**. Ο περιορισμός της γλώσσας μειώνει το σύνολο χαρακτήρων που πρέπει να εξετάσει η μηχανή, μειώνοντας την αμφισημία και βελτιώνοντας τόσο την ταχύτητα όσο και την ακρίβεια, ειδικά για έγγραφα που περιέχουν μόνο λατινικούς χαρακτήρες.

### Πώς είναι η απόδοση σε μεγάλες παρτίδες;
Η μηχανή είναι thread‑safe για λειτουργίες μόνο ανάγνωσης. Δημιουργήστε μια ομάδα νήματος και εκχωρήστε κάθε εικόνα σε δική της `OcrEngine` παρουσία. Σε μηχάνημα 4‑πυρήνων, μπορείτε να πετύχετε **≈250 σελίδες/λεπτό** με παράλληλη εκτέλεση. Βεβαιωθείτε ότι έχετε εκχωρήσει επαρκή heap μνήμη και παρακολουθήστε τη χρήση CPU για να αποφύγετε bottlenecks όταν επεξεργάζεστε χιλιάδες εικόνες υψηλής ανάλυσης.

## Συμβουλές για καλύτερη ακρίβεια

- **Προ‑επεξεργασία της εικόνας**: αυξήστε την αντίθεση, εφαρμόστε φίλτρο median ή μετατρέψτε σε γκρι κλίμακα πριν το OCR.
- **Χρησιμοποιήστε σάρωση 300 dpi ή υψηλότερη**· οι χαμηλότερες αναλύσεις αυξάνουν δραματικά τα ποσοστά σφάλματος.
- **Διατηρήστε το προσαρμοσμένο λεξικό εστιασμένο**: υπερβολικές άσχετες λέξεις μπορούν να μπερδέψουν τον ελεγκτή ορθογραφίας.
- **Μετα‑επεξεργασία με regex**: επικυρώστε ημερομηνίες, αριθμούς ή IDs μετά την εξαγωγή για να εντοπίσετε τυχόν ανωμαλίες.

## Επόμενα βήματα

Τώρα που γνωρίζετε **how to perform OCR** σε εικόνες και **how to extract text from image** αρχεία, μπορείτε να εξερευνήσετε:

- Αποθήκευση του αποτελέσματος OCR ως αναζητήσιμο PDF με κρυφό στρώμα κειμένου.
- Αποθήκευση των εξαγόμενων δεδομένων τιμολογίου απευθείας σε σχεσιακή βάση δεδομένων.
- Εφαρμογή μοντέλων μηχανικής μάθησης για περαιτέρω καθαρισμό χειρόγραφων σημειώσεων.
- Έκθεση της ροής εργασίας OCR ως υπηρεσία RESTful για εικόνες που ανεβάζουν οι χρήστες.

Κάθε μία από αυτές τις επεκτάσεις βασίζεται στα βασικά βήματα που καλύφθηκαν παραπάνω, έτσι η μετάβαση θα είναι ομαλή.

---

**Τελευταία ενημέρωση:** 2026-09-23  
**Δοκιμή με:** Aspose OCR 24.12 for Java  
**Συγγραφέας:** Aspose  

## Συχνές ερωτήσεις

**Q: Απαιτεί το Aspose OCR σύνδεση στο διαδίκτυο;**  
A: Όχι. Η βιβλιοθήκη λειτουργεί εντελώς εκτός σύνδεσης· όλη η αναγνώριση γίνεται τοπικά στη JVM σας.

**Q: Ποιες εκδόσεις Java υποστηρίζονται;**  
A: Το Aspose OCR υποστηρίζει Java 8 έως Java 21, συμπεριλαμβανομένων τόσο των τυπικών όσο και των διανομών OpenJDK.

**Q: Μπορώ να επεξεργαστώ εικόνες μεγαλύτερες από 10 MB;**  
A: Ναι. Η μηχανή μεταδίδει δεδομένα σε ροή και μπορεί να διαχειριστεί εικόνες έως 500 MB, περιορισμένες μόνο από τη διαθέσιμη μνήμη heap.

**Q: Πώς αδειοδοτώ το Aspose OCR για παραγωγή;**  
A: Αγοράστε εμπορική άδεια από το κατάστημα Aspose και ορίστε το αρχείο άδειας με `License license = new License(); license.setLicense("Aspose.OCR.lic");`.

**Q: Υπάρχει ενσωματωμένη υποστήριξη για χειρόγραφο κείμενο;**  
A: Το Aspose OCR περιλαμβάνει λειτουργία χειρογράφου που μπορεί να ενεργοποιηθεί μέσω `ocrEngine.getEngineOptions().setHandwriting(true);`, βελτιώνοντας την ακρίβεια σε καλλιγραφικά σενάρια.

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you wish to process
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));

        // Step 3: Enable spell‑checking for the OCR result
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);

        // Step 4: Provide a custom dictionary (one word per line)
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));

        // Step 5: Run the OCR process
        OcrResult ocrResult = ocrEngine.process();

        // Step 6: Output the recognized (and corrected) text
        System.out.println(ocrResult.getText());
    }
}
```

## Σχετικά μαθήματα

- [Εκτέλεση OCR σε εικόνα με Aspose OCR Java – Οδηγός βήμα‑βήμα](/ocr/java/advanced-ocr-techniques/perform-ocr-on-image-with-aspose-ocr-java-step-by-step-guide/)
- [Προεπεξεργασία εικόνας OCR σε Java – Βελτιώστε την ακρίβεια εξαγωγής κειμένου](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)
- [Πώς να ενεργοποιήσετε GPU για OCR σε Java – Αναγνώριση κειμένου από εικόνα](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-recognize-text-from-image/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}