---
category: general
date: 2026-03-07
description: Φορτώστε εικόνα για OCR σε Java γρήγορα. Μάθετε πώς να ρυθμίσετε τη μηχανή
  OCR, να ορίσετε περιοχή ενδιαφέροντος (ROI) και να εξάγετε κείμενο – περιλαμβάνει
  πλήρες παράδειγμα κώδικα και συμβουλές για τη ρύθμιση του OCR.
draft: false
keywords:
- load image for OCR
- how to set OCR
- OCR region of interest
- Java OCR example
- image processing Java
language: el
og_description: Φορτώστε εικόνα για OCR σε Java και μάθετε πώς να ρυθμίσετε τη μηχανή
  OCR. Αυτός ο οδηγός σας καθοδηγεί στη διαχείριση ROI, την περιστροφή και τον πλήρη
  κώδικα.
og_title: Φόρτωση εικόνας για OCR σε Java – Πλήρης οδηγός προγραμματισμού
tags:
- OCR
- Java
- Image Processing
title: Φόρτωση εικόνας για OCR σε Java – Οδηγός βήμα‑προς‑βήμα
url: /el/java/ocr-operations/load-image-for-ocr-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Φόρτωση Εικόνας για OCR σε Java – Πλήρης Οδηγός Προγραμματισμού

Έχετε χρειαστεί ποτέ να **φορτώσετε εικόνα για OCR** αλλά δεν ήξερες ποιες κλήσεις να κάνεις; Δεν είστε μόνοι—οι περισσότεροι προγραμματιστές συναντούν αυτό το εμπόδιο όταν η πρώτη εικόνα εμφανίζεται και η μηχανή OCR φαίνεται μπερδεμένη. Τα καλά νέα είναι ότι η λύση είναι αρκετά απλή μόλις γνωρίζετε τα σωστά βήματα.

Σε αυτό το tutorial θα σας δείξουμε **πώς να ρυθμίσετε τις παραμέτρους OCR**, να ορίσετε μια περιοχή ενδιαφέροντος (ROI) και, τέλος, να εξάγετε το κείμενο από εκείνο το τμήμα της εικόνας. Στο τέλος θα έχετε ένα εκτελέσιμο πρόγραμμα Java που φορτώνει μια εικόνα για OCR, την περιστρέφει αυτόματα αν χρειάζεται και εκτυπώνει το εξαγόμενο κείμενο—χωρίς καμία μυστική μαγεία.

## Τι Θα Χρειαστείτε

- Java 17 ή νεότερη (ο κώδικας χρησιμοποιεί τη λέξη-κλειδί `var` για συντομία, αλλά μπορείτε να υποβαθμίσετε αν πρέπει).  
- Ένα OCR SDK που παρέχει τις κλάσεις `OcrEngine`, `OcrResult` και `ImageInputStream` — σκεφτείτε βιβλιοθήκες όπως **Tesseract‑Java**, **ABBYY** ή μια ιδιόκτητη λύση.  
- Μια δείγμα εικόνας (`multi_page_form.png`) που περιέχει το κείμενο που θέλετε να διαβάσετε.  
- Ένα απλό IDE (IntelliJ IDEA, Eclipse, VS Code) — οποιοδήποτε αρκεί.

Δεν απαιτείται επιπλέον Maven ή Gradle μαγεία για τη βασική λογική· απλώς προσθέστε το OCR JAR στο classpath και είστε έτοιμοι.

## Βήμα 1: Ρύθμιση του OCR Engine – Πώς να Ρυθμίσετε το OCR Σωστά

Πριν μπορέσετε να **φορτώσετε εικόνα για OCR**, χρειάζεστε μια παρουσία του engine που ξέρει τι να ψάξει. Τα περισσότερα SDK εκθέτουν ένα αντικείμενο ρυθμίσεων· εκεί λέτε στο engine να περιστρέφει αυτόματα το κείμενο μέσα στην ROI.

```java
import com.example.ocr.OcrEngine;   // Replace with your actual package
import com.example.ocr.OcrConfig;

public class OcrSetup {
    public static OcrEngine createEngine() {
        OcrEngine engine = new OcrEngine();

        // Enable automatic rotation handling within the region of interest
        engine.getConfig().setAutoRotateWithinRegion(true);

        // You can also tweak language, confidence thresholds, etc.
        // engine.getConfig().setLanguage("eng");
        // engine.getConfig().setMinConfidence(0.75);

        return engine;
    }
}
```

**Γιατί είναι σημαντικό:** Η ενεργοποίηση του `setAutoRotateWithinRegion` σας εξοικονομεί πολύ επεξεργασία μετά. Φανταστείτε μια σαρωμένη φόρμα όπου ο χρήστης έλκυσε τη σελίδα με μερικές μοίρες—χωρίς αυτή τη σημαία το OCR θα διάβαζε άσχετο κείμενο. Η ενεργοποίηση των επιλογών *πώς να ρυθμίσετε το OCR* εξασφαλίζει ανθεκτικότητα από την αρχή.

## Βήμα 2: Φόρτωση Εικόνας για OCR – Τροφοδοτώντας το Engine

Τώρα που το engine είναι έτοιμο, στην πραγματικότητα **φορτώνουμε εικόνα για OCR**. Η κλάση `ImageInputStream` αφαιρεί την πολυπλοκότητα του χειρισμού αρχείων και επιτρέπει στο OCR SDK να καταναλώσει ένα ρεύμα δεδομένων άμεσα.

```java
import com.example.ocr.ImageInputStream;
import java.nio.file.Paths;

public class ImageLoader {
    public static ImageInputStream load(String path) throws Exception {
        // Validate the file exists and is readable
        if (!java.nio.file.Files.isReadable(Paths.get(path))) {
            throw new IllegalArgumentException("Cannot read image at: " + path);
        }

        // Create the stream – most SDKs accept a simple file path, but a stream is more flexible
        return new ImageInputStream(path);
    }
}
```

**Συμβουλή:** Αν εργάζεστε με PDF πολλαπλών σελίδων, πολλές βιβλιοθήκες OCR σας επιτρέπουν να περάσετε έναν δείκτη σελίδας στον κατασκευαστή του stream. Έτσι μπορείτε να κάνετε βρόχο στις σελίδες χωρίς επιπλέον βήματα μετατροπής.

## Βήμα 3: Ορισμός της Περιοχής Ενδιαφέροντος (ROI)

Η σάρωση ολόκληρης της εικόνας μπορεί να είναι σπατάλη, ειδικά για μεγάλες φόρμες. Περιορίζοντας την εστίαση σε ένα ορθογώνιο, επιταχύνετε την επεξεργασία και βελτιώνετε την ακρίβεια.

```java
import java.awt.Rectangle;

public class RoiHelper {
    public static Rectangle defineRoi() {
        // x, y, width, height – adjust these numbers to match your form layout
        int x = 120;
        int y = 350;
        int width = 800;
        int height = 200;

        return new Rectangle(x, y, width, height);
    }
}
```

**Ακραία περίπτωση:** Αν η ROI εκτείνεται πέρα από τα όρια της εικόνας, τα περισσότερα engines θα πετάξουν εξαίρεση. Ένας γρήγορος έλεγχος λογικής (π.χ. σύγκριση `x + width` με `image.getWidth()`) μπορεί να αποτρέψει καταρρεύσεις.

## Βήμα 4: Εκτέλεση OCR στην ROI

Με το engine, την εικόνα και την ROI έτοιμα, ήρθε η ώρα να **φορτώσετε εικόνα για OCR** και να αναγνωρίσετε το κείμενο.

```java
import com.example.ocr.OcrResult;

public class OcrRunner {
    public static OcrResult run(OcrEngine engine,
                                ImageInputStream image,
                                Rectangle roi) throws Exception {
        // The recognize method returns both text and confidence data
        return engine.recognize(image, roi);
    }
}
```

Αν χρειάζεστε το σκορ εμπιστοσύνης για κάθε λέξη, το `OcrResult` συνήθως εκθέτει μια συλλογή `getWords()` όπου κάθε στοιχείο έχει μέθοδο `getConfidence()`. Η φιλτράρισμα λέξεων χαμηλής εμπιστοσύνης μπορεί να είναι χρήσιμη για επακόλουθη επικύρωση.

## Βήμα 5: Εξαγωγή του Κειμένου και Επαλήθευση του Αποτελέσματος

Τέλος, εκτυπώνουμε το εξαγόμενο string. Σε μια πραγματική εφαρμογή πιθανότατα θα το γράφατε σε βάση δεδομένων ή θα το τροφοδοτούσατε σε έναν parser, αλλά μια εκτύπωση στην κονσόλα αρκεί για επίδειξη.

```java
public class RoiOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create and configure the OCR engine
        OcrEngine ocrEngine = OcrSetup.createEngine();

        // Step 2: Load the image you want to process
        ImageInputStream imageStream = ImageLoader.load("YOUR_DIRECTORY/multi_page_form.png");

        // Step 3: Define where to look – the ROI
        Rectangle regionOfInterest = RoiHelper.defineRoi();

        // Step 4: Run OCR limited to that region
        OcrResult ocrResult = OcrRunner.run(ocrEngine, imageStream, regionOfInterest);

        // Step 5: Show the result
        System.out.println("ROI text:");
        System.out.println(ocrResult.getText());
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Υποθέτοντας ότι η ROI περιέχει τη φράση “Invoice #12345”, θα δείτε κάτι σαν:

```
ROI text:
Invoice #12345
Date: 2026-03-07
Total: $1,250.00
```

Αν η μηχανή OCR δεν βρει κανένα κείμενο, το `ocrResult.getText()` θα επιστρέψει κενή συμβολοσειρά – ένα καλό σημάδι να ελέγξετε ξανά τις συντεταγμένες της ROI ή την ποιότητα της εικόνας.

## Διαχείριση Συνηθισμένων Προβλημάτων

| Πρόβλημα | Γιατί Συμβαίνει | Γρήγορη Λύση |
|---------|----------------|-----------|
| **Κενό αποτέλεσμα** | ROI εκτός ορίων εικόνας ή η εικόνα είναι γκρι με χαμηλή αντίθεση. | Επαληθεύστε τις συντεταγμένες με έναν επεξεργαστή εικόνας· αυξήστε την αντίθεση ή δυαδικοποιήστε πριν το OCR. |
| **Ακατάλληλοι χαρακτήρες** | Η περιστροφή δεν διαχειρίζεται, ή το λάθος language pack. | Βεβαιωθείτε ότι το `setAutoRotateWithinRegion(true)` είναι ενεργό· φορτώστε το σωστό μοντέλο γλώσσας (`engine.getConfig().setLanguage("eng")`). |
| **Καθυστέρηση απόδοσης** | Επεξεργασία ολόκληρης της εικόνας αντί της ROI. | Πάντα περάστε ένα `Rectangle` για περιορισμό της περιοχής σάρωσης· εξετάστε την υποβάθμιση μεγάλων εικόνων πρώτα. |
| **Σφάλματα Out‑of‑memory** | Πολύ μεγάλες εικόνες φορτωμένες ως ακατέργαστα bytes. | Χρησιμοποιήστε APIs ροής (`ImageInputStream`) και, αν υποστηρίζεται, ζητήστε επεξεργασία σε tiles. |

**Pro tip:** Όταν δουλεύετε με φόρμες πολλαπλών σελίδων, τυλίξτε την κλήση OCR σε βρόχο που αυξάνει το δείκτη σελίδας. Τα περισσότερα SDK επιτρέπουν την επαναχρησιμοποίηση της ίδιας παρουσίας `OcrEngine`, κάτι που εξοικονομεί χρόνο εκκίνησης.

## Περαιτέρω Επέκταση – Τι Αν Χρειαστείτε Περισσότερο;

- **Batch processing:** Συλλέξτε μια λίστα διαδρομών αρχείων, κάντε βρόχο σε αυτές και αποθηκεύστε κάθε αποτέλεσμα OCR σε αρχείο CSV.  
- **Δυναμική ROI:** Χρησιμοποιήστε OpenCV για αυτόματη ανίχνευση πεδίων φόρμας, στη συνέχεια περάστε αυτές τις συντεταγμένες στο βήμα OCR.  
- **Post‑processing:** Εφαρμόστε regex για καθαρισμό ημερομηνιών, αριθμών τιμολογίων ή τιμών νομισμάτων που εξήχθησαν από την ROI.  

Όλες αυτές οι επεκτάσεις βασίζονται στο βασικό μοτίβο που καλύψαμε: **φόρτωση εικόνας για OCR**, ρύθμιση **πώς να ρυθμίσετε το OCR**, ορισμός περιοχής, εκτέλεση του engine και διαχείριση του αποτελέσματος.

![Screenshot showing ROI highlighted on a form – load image for OCR example](roi-screenshot.png "load image for OCR example")

*Κείμενο alt εικόνας: φόρτωση εικόνας για OCR – επισημασμένη περιοχή ενδιαφέροντος σε ένα δείγμα φόρμας.*

## Συμπέρασμα

Τώρα έχετε ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει πώς να **φορτώνετε εικόνα για OCR** σε Java, ρυθμίζοντας σωστά τις **επιλογές πώς να ρυθμίσετε το OCR**, και να εξάγετε κείμενο από συγκεκριμένη περιοχή. Τα βήματα είναι μοντέλα, ώστε να μπορείτε να αντικαταστήσετε μια διαφορετική βιβλιοθήκη OCR ή να προσαρμόσετε την ROI χωρίς να ξαναγράψετε ολόκληρο το πρόγραμμα.

Στην επόμενη φάση, δοκιμάστε διαφορετικές μορφές εικόνας (TIFF, BMP) ή προσθέστε βήμα προεπεξεργασίας με OpenCV για βελτίωση της ακρίβειας σε θορυβώδεις σαρώσεις. Και αν σας ενδιαφέρει η διαχείριση πολλαπλών σελίδων, επεκτείνετε το βρόχο στο `RoiOcrExample` για επανάληψη πάνω σε δείκτες σελίδων.

Καλή προγραμματιστική δουλειά, και εύχομαι τα αποτελέσματα OCR σας να είναι πάντα kristall‑καθαρά!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}