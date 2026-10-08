---
category: general
date: 2026-02-22
description: Πώς να χρησιμοποιήσετε OCR σε Java για την εξαγωγή κειμένου από εικόνα,
  τη βελτίωση της ακρίβειας του OCR και τη φόρτωση εικόνας για OCR με πρακτικά παραδείγματα
  κώδικα.
draft: false
keywords:
- how to use OCR
- extract text from image
- improve OCR accuracy
- load image for OCR
- OCR preprocessing
language: el
og_description: Πώς να χρησιμοποιήσετε OCR στη Java για να εξάγετε κείμενο από εικόνα
  και να βελτιώσετε την ακρίβεια του OCR. Ακολουθήστε αυτόν τον οδηγό για ένα έτοιμο
  παράδειγμα προς εκτέλεση.
og_title: Πώς να χρησιμοποιήσετε OCR στη Java – Πλήρης οδηγός βήμα‑προς‑βήμα
tags:
- OCR
- Java
- Image Processing
title: Πώς να χρησιμοποιήσετε OCR στη Java – Πλήρης οδηγός βήμα‑προς‑βήμα
url: /el/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε OCR σε Java – Πλήρης Οδηγός Βήμα‑Βήμα

Έχετε ποτέ χρειαστεί να **how to use OCR** σε ένα θολό στιγμιότυπο οθόνης και αναρωτηθήκατε γιατί το αποτέλεσμα φαίνεται ακατανόητο; Δεν είστε ο μόνος. Σε πολλές πραγματικές εφαρμογές—σάρωση αποδείξεων, ψηφιοποίηση φορμών ή εξαγωγή κειμένου από memes—η λήψη αξιόπιστων αποτελεσμάτων εξαρτάται από μερικές απλές ρυθμίσεις.

Σε αυτό το tutorial θα περάσουμε από το **how to use OCR** για *extract text from image* αρχεία, θα σας δείξουμε πώς να **improve OCR accuracy**, και θα επιδείξουμε τον σωστό τρόπο **load image for OCR** χρησιμοποιώντας μια δημοφιλής βιβλιοθήκη OCR για Java. Στο τέλος θα έχετε ένα αυτόνομο πρόγραμμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο.

## Τι Θα Μάθετε

- Ο ακριβής κώδικας που χρειάζεστε για **load image for OCR** (χωρίς κρυφές εξαρτήσεις).
- Ποια flags προεπεξεργασίας ενισχύουν το **improve OCR accuracy** και γιατί είναι σημαντικά.
- Πώς να διαβάσετε το αποτέλεσμα OCR και να το εκτυπώσετε στην κονσόλα.
- Συνηθισμένα λάθη—όπως η παράλειψη ορισμού περιοχής ενδιαφέροντος ή η αγνόηση της μείωσης θορύβου—και πώς να τα αποφύγετε.

### Προαπαιτούμενα

- Java 17 ή νεότερη (ο κώδικας μεταγλωττίζεται με οποιοδήποτε πρόσφατο JDK).
- Μια βιβλιοθήκη OCR που παρέχει τις κλάσεις `OcrEngine`, `ImagePreprocessingOptions`, `OcrInput` και `OcrResult` (για παράδειγμα, το φανταστικό πακέτο `com.example.ocr` που χρησιμοποιείται στο απόσπασμα). Αντικαταστήστε το με την πραγματική βιβλιοθήκη που χρησιμοποιείτε.
- Μια δείγμα εικόνας (`skewed_noisy.png`) τοποθετημένη σε φάκελο που μπορείτε να αναφέρετε.

> **Pro tip:** Εάν χρησιμοποιείτε εμπορικό SDK, βεβαιωθείτε ότι το αρχείο άδειας βρίσκεται στο classpath σας· διαφορετικά η μηχανή θα ρίξει σφάλμα αρχικοποίησης.

---

## Βήμα 1: Δημιουργία Παραδείγματος OCR Engine – **how to use OCR** αποτελεσματικά

Το πρώτο πράγμα που χρειάζεστε είναι ένα αντικείμενο `OcrEngine`. Σκεφτείτε το ως τον εγκέφαλο που θα ερμηνεύσει τα pixel.

```java
// Step 1: Initialize the OCR engine
import com.example.ocr.OcrEngine;

OcrEngine ocrEngine = new OcrEngine();
```

*Γιατί είναι σημαντικό:* Χωρίς μηχανή δεν έχετε κανένα πλαίσιο για μοντέλα γλώσσας, σύνολα χαρακτήρων ή ευρετικές εικόνας. Η δημιουργία του νωρίς σας επιτρέπει επίσης να συνδέσετε επιλογές προεπεξεργασίας αργότερα.

---

## Βήμα 2: Διαμόρφωση Προεπεξεργασίας Εικόνας – **improve OCR accuracy**

Η προεπεξεργασία είναι η μυστική σάλτσα που μετατρέπει μια θορυβώδη σάρωση σε καθαρό, μηχανικά αναγνώσιμο κείμενο. Παρακάτω ενεργοποιούμε το deskew, τη μείωση θορύβου υψηλού επιπέδου, το auto‑contrast και μια περιοχή ενδιαφέροντος (ROI) για να εστιάσουμε στο σχετικό τμήμα της εικόνας.

```java
import com.example.ocr.ImagePreprocessingOptions;
import java.awt.Rectangle;

// Step 2: Set up preprocessing to improve OCR accuracy
ImagePreprocessingOptions preprocessing = new ImagePreprocessingOptions();
preprocessing.setDeskewEnabled(true); // Correct image rotation
preprocessing.setNoiseReductionLevel(
        ImagePreprocessingOptions.NoiseReduction.HIGH); // Reduce speckles
preprocessing.setAutoContrastEnabled(true); // Boost contrast
preprocessing.setRegionOfInterest(new Rectangle(100, 200, 800, 600)); // Process a sub‑region only

ocrEngine.setPreprocessingOptions(preprocessing);
```

*Γιατί είναι σημαντικό:*  
- **Deskew** ευθυγραμμίζει το περιστραμμένο κείμενο, κάτι που είναι ουσιώδες όταν σαρώνετε αποδείξεις που δεν είναι τέλεια επίπεδες.  
- **Noise reduction** αφαιρεί τυχαία pixel που διαφορετικά θα ερμηνευόταν ως χαρακτήρες.  
- **Auto‑contrast** επεκτείνει το τόνικό εύρος, κάνοντας τα αχνά γράμματα να ξεχωρίζουν.  
- **ROI** λέει στη μηχανή να αγνοεί άσχετα περιθώρια, εξοικονομώντας χρόνο και μνήμη.

Αν παραλείψετε κάποιο από αυτά, πιθανότατα θα δείτε μείωση στα αποτελέσματα του **improve OCR accuracy**.

---

## Βήμα 3: Φόρτωση Εικόνας για OCR – **load image for OCR** σωστά

Τώρα δείχνουμε πραγματικά τη μηχανή στο αρχείο που θέλουμε να διαβάσουμε. Η κλάση `OcrInput` μπορεί να δέχεται πολλαπλές εικόνες, αλλά για αυτό το παράδειγμα το κρατάμε απλό.

```java
import com.example.ocr.OcrInput;

// Step 3: Load the image you want to extract text from
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/skewed_noisy.png"); // replace with your real path
```

*Γιατί είναι σημαντικό:* Η διαδρομή πρέπει να είναι απόλυτη ή σχετική με τον τρέχοντα φάκελο εργασίας· διαφορετικά η μηχανή ρίχνει `FileNotFoundException`. Επίσης, σημειώστε ότι το όνομα μεθόδου `add` υποδηλώνει ότι μπορείτε να βάλετε σε σειρά πολλές εικόνες—χρήσιμο για επεξεργασία παρτίδας.

---

## Βήμα 4: Εκτέλεση OCR και Εξαγωγή του Αναγνωρισμένου Κειμένου – **how to use OCR** από άκρη σε άκρη

Τέλος, ζητάμε από τη μηχανή να αναγνωρίσει το κείμενο και να το εκτυπώσει. Το αντικείμενο `OcrResult` περιέχει τη ακατέργαστη συμβολοσειρά, τις βαθμολογίες εμπιστοσύνης και μεταδεδομένα γραμμή‑προς‑γραμμή (αν τα χρειαστείτε αργότερα).

```java
import com.example.ocr.OcrResult;

// Step 4: Run OCR and print the extracted text
OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("=== OCR Output ===");
System.out.println(ocrResult.getText());
```

**Αναμενόμενη έξοδος** (υπόθεση ότι η δείγμα εικόνα περιέχει “Hello, OCR World!”):

```
=== OCR Output ===
Hello, OCR World!
```

Αν το αποτέλεσμα φαίνεται ακατάληπτο, επιστρέψτε στο Βήμα 2 και προσαρμόστε τις επιλογές προεπεξεργασίας—ίσως μειώσετε το επίπεδο μείωσης θορύβου ή προσαρμόστε το ορθογώνιο ROI.

---

## Πλήρες, Εκτελέσιμο Παράδειγμα

Παρακάτω είναι ένα πλήρες πρόγραμμα Java που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα αρχείο με όνομα `OcrDemo.java`. Συνδέει όλα τα βήματα που συζητήσαμε.

```java
// OcrDemo.java – A complete, runnable example showing how to use OCR in Java
import com.example.ocr.OcrEngine;
import com.example.ocr.ImagePreprocessingOptions;
import com.example.ocr.OcrInput;
import com.example.ocr.OcrResult;
import java.awt.Rectangle;

public class OcrDemo {
    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing (this is the key to improve OCR accuracy)
        ImagePreprocessingOptions preprocessing = new ImagePreprocessingOptions();
        preprocessing.setDeskewEnabled(true);
        preprocessing.setNoiseReductionLevel(
                ImagePreprocessingOptions.NoiseReduction.HIGH);
        preprocessing.setAutoContrastEnabled(true);
        preprocessing.setRegionOfInterest(new Rectangle(100, 200, 800, 600));
        ocrEngine.setPreprocessingOptions(preprocessing);

        // 3️⃣ Load the image you want to extract text from
        OcrInput ocrInput = new OcrInput();
        // 👉 Replace the path with your own image location
        ocrInput.add("YOUR_DIRECTORY/skewed_noisy.png");

        // 4️⃣ Run the OCR engine and print the result
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
    }
}
```

Αποθηκεύστε το αρχείο, μεταγλωττίστε με `javac OcrDemo.java` και τρέξτε `java OcrDemo`. Αν όλα είναι ρυθμισμένα σωστά, θα δείτε το εξαγόμενο κείμενο να εκτυπώνεται στην κονσόλα.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

| Ερώτηση | Απάντηση |
|----------|--------|
| **Τι γίνεται αν η εικόνα μου είναι σε μορφή JPEG;** | Η μέθοδος `OcrInput.add()` δέχεται οποιαδήποτε υποστηριζόμενη μορφή raster—PNG, JPEG, BMP, TIFF. Απλώς αλλάξτε την επέκταση του αρχείου στη διαδρομή. |
| **Μπορώ να επεξεργαστώ πολλές σελίδες ταυτόχρονα;** | Απόλυτα. Καλέστε `ocrInput.add()` για κάθε αρχείο, μετά περάστε το ίδιο `ocrInput` στη `recognize()`. Η μηχανή θα επιστρέψει ένα ενωμένο `OcrResult`. |
| **Τι γίνεται αν το αποτέλεσμα OCR είναι κενό;** | Ελέγξτε ξανά ότι το ROI περιέχει πραγματικά κείμενο. Επίσης, βεβαιωθείτε ότι το `setDeskewEnabled(true)` είναι ενεργό· μια περιστροφή 90° θα κάνει τη μηχανή να νομίζει ότι η εικόνα είναι κενή. |
| **Πώς αλλάζω το μοντέλο γλώσσας;** | Οι περισσότερες βιβλιοθήκες εκθέτουν μια μέθοδο `setLanguage(String)` στο `OcrEngine`. Καλέστε την πριν το `recognize()`, π.χ., `ocrEngine.setLanguage("eng")`. |
| **Υπάρχει τρόπος να λάβω βαθμολογίες εμπιστοσύνης;** | Ναι, το `OcrResult` συχνά παρέχει `getConfidence()` ανά γραμμή ή ανά χαρακτήρα. Χρησιμοποιήστε το για να φιλτράρετε αποτελέσματα χαμηλής εμπιστοσύνης. |

---

## Συμπέρασμα

Καλύψαμε το **how to use OCR** σε Java από την αρχή μέχρι το τέλος: δημιουργία της μηχανής, διαμόρφωση προεπεξεργασίας για **improve OCR accuracy**, σωστή **load image for OCR**, και τέλος εκτύπωση του εξαγόμενου κειμένου. Το πλήρες απόσπασμα κώδικα είναι έτοιμο για εκτέλεση, και οι εξηγήσεις απαντούν στο “γιατί” πίσω από κάθε γραμμή.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να αλλάξετε το ορθογώνιο ROI για να εστιάσετε σε διαφορετικά τμήματα της εικόνας, πειραματιστείτε με `NoiseReduction.MEDIUM`, ή ενσωματώστε το αποτέλεσμα σε ένα αναζητήσιμο PDF. Μπορείτε επίσης να εξερευνήσετε συναφή θέματα όπως **extract text from image** χρησιμοποιώντας υπηρεσίες cloud, ή να επεξεργαστείτε χιλιάδες αρχεία σε παρτίδες με μια πολυνηματική ουρά.

Έχετε περισσότερες ερωτήσεις σχετικά με OCR, προεπεξεργασία εικόνας ή ενσωμάτωση Java; Αφήστε ένα σχόλιο, και καλή προγραμματιστική!

![Παράδειγμα χρήσης OCR](/images/ocr-demo.png "πώς να χρησιμοποιήσετε OCR – Παράδειγμα Java που δείχνει προεπεξεργασία και αποτέλεσμα")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}