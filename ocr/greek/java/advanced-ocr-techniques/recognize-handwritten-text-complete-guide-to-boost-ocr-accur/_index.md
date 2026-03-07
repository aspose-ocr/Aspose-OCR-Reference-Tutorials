---
category: general
date: 2026-03-07
description: Μάθετε πώς να αναγνωρίζετε χειρόγραφο κείμενο, να βελτιώνετε την ακρίβεια
  του OCR και να εκτελείτε OCR σε αρχεία εικόνας. Παράδειγμα Java βήμα‑προς‑βήμα με
  προσαρμοσμένο λεξικό.
draft: false
keywords:
- recognize handwritten text
- improve ocr accuracy
- run OCR on image
- load image for OCR
- OCR engine configuration
- custom dictionary OCR
language: el
og_description: αναγνωρίστε χειρόγραφο κείμενο με μια μηχανή OCR Java. Ακολουθήστε
  τον οδηγό μας για να βελτιώσετε την ακρίβεια του OCR, εκτελέστε OCR σε εικόνα και
  φορτώστε εικόνα για OCR.
og_title: αναγνώριση χειρόγραφου κειμένου – Πλήρης οδηγός Java
tags:
- OCR
- Java
- Handwriting Recognition
title: Αναγνώριση χειρόγραφου κειμένου – Πλήρης οδηγός για τη βελτίωση της ακρίβειας
  OCR
url: /el/java/advanced-ocr-techniques/recognize-handwritten-text-complete-guide-to-boost-ocr-accur/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# αναγνώριση χειρόγραφου κειμένου – Πλήρες Java Tutorial

Έχετε ποτέ χρειαστεί να **αναγνωρίσετε χειρόγραφο κείμενο** από μια φωτογραφία αλλά να λαμβάνετε ακατανόητο κείμενο; Δεν είστε μόνοι. Σε πολλά έργα—σκανάρια αποδείξεων, εφαρμογές λήψης σημειώσεων ή εργαλεία αρχειοθέτησης—το χειρόγραφο OCR μπορεί να φαίνεται σαν να κυνηγάτε ένα κινούμενο στόχο.  

Τα καλά νέα; Με λίγες ρυθμίσεις μπορείτε να **βελτιώσετε την OCR accuracy** δραματικά, και η ολόκληρη διαδικασία **run OCR on image** αρχείων είναι μόνο μερικές γραμμές Java. Παρακάτω θα δείτε ακριβώς πώς να **load image for OCR**, ενεργοποιήσετε τη διόρθωση ορθογραφίας, και ακόμη να ενσωματώσετε το δικό σας λεξικό.

Σε αυτό το tutorial θα καλύψουμε:

* Τα ελάχιστα προαπαιτούμενα (Java 11+, μια βιβλιοθήκη OCR, και ένα δείγμα εικόνας).
* Πώς να ρυθμίσετε τη μηχανή OCR για διορθώσεις ορθογραφίας.
* Προσθήκη προσαρμοσμένου λεξικού για διαχείριση λέξεων ειδικών τομέων.
* Εκτέλεση της γραμμής αναγνώρισης και εκτύπωση του διορθωμένου αποτελέσματος.

Στο τέλος θα έχετε ένα έτοιμο προς εκτέλεση πρόγραμμα που μπορεί να **αναγνωρίσει χειρόγραφο κείμενο** με πολύ λιγότερα σφάλματα από τις προεπιλεγμένες ρυθμίσεις.

---

## Τι θα χρειαστείτε

| Στοιχείο | Γιατί είναι σημαντικό |
|------|----------------|
| **Java 11 or newer** | Το παράδειγμα χρησιμοποιεί τη σύγχρονη λέξη-κλειδί `var` και το `try‑with‑resources`. |
| **OCR library** (e.g., `com.example.ocr` – replace with your actual vendor) | Παρέχει `OcrEngine`, `OcrResult` και αντικείμενα ρυθμίσεων. |
| **Handwritten image** (`handwritten_note.jpg`) | Ένα δείγμα JPEG που περιέχει το κείμενο που θέλετε να αναγνωρίσετε. |
| **Optional custom dictionary** (`custom_dict.txt`) | Βελτιώνει την αναγνώριση όρων ειδικών κλάδων, συντομογραφιών ή ονομάτων. |

Αν δεν έχετε ήδη ένα OCR JAR, κατεβάστε την πιο πρόσφατη έκδοση από το Maven repository του προμηθευτή και προσθέστε το στο classpath του έργου σας.

---

## Βήμα 1 – Δημιουργία και ρύθμιση της μηχανής OCR  

Το πρώτο που πρέπει να κάνετε είναι να δημιουργήσετε την μηχανή και να ενεργοποιήσετε τη ενσωματωμένη λειτουργία διόρθωσης ορθογραφίας. Αυτό μόνο μπορεί να αφαιρέσει πολλές λανθασμένες λέξεις που είναι κοινές σε χειρόγραφες σημειώσεις.

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrConfig;

// Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Enable spell‑correction to automatically fix common mistakes
OcrConfig config = ocrEngine.getConfig();
config.setEnableSpellCorrection(true);
```

**Γιατί είναι σημαντικό:** Τα χειρόγραφα χαρακτήρες συχνά μοιάζουν με άλλα γράμματα (π.χ., “m” vs. “n”). Η ενεργοποίηση της διόρθωσης ορθογραφίας επιτρέπει στη μηχανή να εφαρμόσει ένα μοντέλο γλώσσας που προβλέπει τη πιο πιθανή λέξη, αυξάνοντας τη συνολική **OCR accuracy**.

---

## Βήμα 2 – (Προαιρετικό) Ενσωμάτωση προσαρμοσμένου λεξικού  

Αν οι σημειώσεις σας περιέχουν όρους, κωδικούς προϊόντων ή ονόματα που δεν υπάρχουν στο προεπιλεγμένο λεξικό, μπορείτε να κατευθύνετε τη μηχανή σε ένα αρχείο απλού κειμένου—μία λέξη ανά γραμμή.

```java
// Path to a custom dictionary; comment out if you don't need it
config.setCustomDictionaryPath("YOUR_DIRECTORY/custom_dict.txt");
```

**Συμβουλή:** Κρατήστε το αρχείο κωδικοποιημένο σε UTF‑8 και αποφύγετε κενές γραμμές· η μηχανή διαβάζει κάθε γραμμή ως ξεχωριστό token. Η παροχή μιας προσαρμοσμένης λίστας μπορεί να **βελτιώσει την OCR accuracy** έως και 15 % σε εξειδικευμένους τομείς.

---

## Βήμα 3 – Φόρτωση της εικόνας για OCR  

Τώρα πρέπει να τροφοδοτήσουμε τη μηχανή με ένα ρεύμα bytes που αντιπροσωπεύει τη χειρόγραφη εικόνα. Η κλάση `ImageInputStream` αφαιρεί την πολυπλοκότητα του I/O αρχείων και επιτρέπει στη μηχανή OCR να δουλεύει με οποιαδήποτε μορφή εικόνας υποστηρίζει.

```java
import com.example.ocr.ImageInputStream;

// Load the image you want to process
ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/handwritten_note.jpg");
```

**Τι γίνεται αν η εικόνα είναι μεγάλη;** Οι περισσότερες μηχανές OCR δέχονται μια παράμετρο `maxResolution`. Μπορείτε να μειώσετε την ανάλυση της εικόνας εκ των προτέρων με μια βιβλιοθήκη όπως η `java.awt.Image` για να διατηρήσετε τη χρήση μνήμης χαμηλή.

---

## Βήμα 4 – Εκτέλεση OCR στην εικόνα και λήψη του διορθωμένου κειμένου  

Με τη μηχανή ρυθμισμένη και την εικόνα φορτωμένη, η πραγματική αναγνώριση είναι μια κλήση μεθόδου. Το αντικείμενο αποτελέσματος περιέχει το ακατέργαστο κείμενο καθώς και τις βαθμολογίες εμπιστοσύνης για κάθε γραμμή.

```java
import com.example.ocr.OcrResult;

// Perform the recognition
OcrResult ocrResult = ocrEngine.recognize(imageStream);

// Extract the corrected text
String correctedText = ocrResult.getText();
```

Αν χρειάζεστε αποσφαλμάτωση, το `ocrResult.getConfidence()` επιστρέφει ένα float μεταξύ 0 και 1 που υποδεικνύει τη συνολική βεβαιότητα.

---

## Βήμα 5 – Εμφάνιση του αποτελέσματος  

Τέλος, εκτυπώστε το καθαρισμένο αποτέλεσμα στην κονσόλα. Σε μια πραγματική εφαρμογή μπορεί να το αποθηκεύσετε σε μια βάση δεδομένων ή να το περάσετε σε μια επόμενη διαδικασία NLP.

```java
public class HandwrittenOcrDemo {
    public static void main(String[] args) {
        // Steps 1‑4 are encapsulated above; just print the result
        System.out.println("Corrected text:");
        System.out.println(correctedText);
    }
}
```

**Αναμενόμενο αποτέλεσμα (παράδειγμα):**

```
Corrected text:
Meeting notes:
- Discuss quarterly targets
- Review budget allocations
- Assign action items to team leads
```

Παρατηρήστε πώς τα ορθογραφικά λάθη που υπήρχαν στην ακατέργαστη σάρωση έχουν εξαφανιστεί χάρη στη σημαία spell‑correction και στο προαιρετικό λεξικό.

---

## Πλήρες, Εκτελέσιμο Παράδειγμα  

Παρακάτω υπάρχει ένα μόνο αρχείο Java που μπορείτε να αντιγράψετε, να προσαρμόσετε τις διαδρομές και να εκτελέσετε απευθείας (`javac HandwrittenOcrDemo.java && java HandwrittenOcrDemo`). Όλες οι απαραίτητες εισαγωγές και σχόλια περιλαμβάνονται.

```java
// HandwrittenOcrDemo.java
// -----------------------------------------------------
// Demonstrates how to recognize handwritten text,
// improve OCR accuracy with spell‑correction, and
// optionally use a custom dictionary.
// -----------------------------------------------------

import com.example.ocr.OcrEngine;
import com.example.ocr.OcrConfig;
import com.example.ocr.ImageInputStream;
import com.example.ocr.OcrResult;

public class HandwrittenOcrDemo {
    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable spell‑correction (crucial for accuracy)
        OcrConfig config = ocrEngine.getConfig();
        config.setEnableSpellCorrection(true);

        // 3️⃣ (Optional) Attach a custom dictionary
        //    Uncomment and point to your file if needed
        // config.setCustomDictionaryPath("YOUR_DIRECTORY/custom_dict.txt");

        // 4️⃣ Load the image you want to process
        ImageInputStream imageStream = new ImageInputStream(
                "YOUR_DIRECTORY/handwritten_note.jpg"
        );

        // 5️⃣ Run OCR on the image and fetch corrected text
        OcrResult ocrResult = ocrEngine.recognize(imageStream);
        String correctedText = ocrResult.getText();

        // 6️⃣ Show the output
        System.out.println("Corrected text:");
        System.out.println(correctedText);
    }
}
```

### Εκτέλεση του κώδικα

```bash
javac -cp ocr-lib.jar HandwrittenOcrDemo.java
java -cp .:ocr-lib.jar HandwrittenOcrDemo
```

Αντικαταστήστε το `ocr-lib.jar` με το πραγματικό όνομα του JAR που κατεβάσατε. Το πρόγραμμα θα εκτυπώσει τη διορθωμένη μεταγραφή στην κονσόλα.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις  

### Τι γίνεται αν η εικόνα είναι περιστραμμένη;

Πολλές βιβλιοθήκες OCR εκθέτουν μια σημαία `setAutoRotate(true)`. Ενεργοποιήστε την πριν καλέσετε το `recognize`:

```java
config.setAutoRotate(true);
```

### Το προσαρμοσμένο λεξικό μου δεν εφαρμόζεται—γιατί;

Βεβαιωθείτε ότι η διαδρομή του αρχείου είναι απόλυτη ή σχετική με τον τρέχοντα φάκελο, και ότι κάθε γραμμή λήγει με χαρακτήρα νέας γραμμής (`\n`). Επίσης, ελέγξτε ότι το αρχείο λεξικού είναι κωδικοποιημένο σε UTF-8· διαφορετικά η μηχανή μπορεί να παραλείψει άγνωστους χαρακτήρες.

### Πώς μπορώ να επεξεργαστώ πολλές εικόνες σε παρτίδα;

Τυλίξτε τη λογική αναγνώρισης μέσα σε έναν βρόχο:

```java
for (String path : imagePaths) {
    ImageInputStream stream = new ImageInputStream(path);
    OcrResult result = ocrEngine.recognize(stream);
    System.out.println("File: " + path);
    System.out.println(result.getText());
}
```

Θυμηθείτε να επαναχρησιμοποιήσετε το ίδιο αντικείμενο `OcrEngine`; η δημιουργία νέας μηχανής για κάθε εικόνα είναι σπατάλη και μπορεί να μειώσει την απόδοση.

### Λειτουργεί αυτό σε σαρωμένα PDF;

Αν η βιβλιοθήκη σας υποστηρίζει PDF ως μορφή εισόδου, μπορείτε ακόμη να χρησιμοποιήσετε το `ImageInputStream` εξάγοντας κάθε σελίδα ως εικόνα πρώτα (π.χ., με το Apache PDFBox). Μόλις έχετε μια raster εικόνα, η ίδια διαδικασία εφαρμόζεται.

---

## Συμβουλές για μέγιστη ακρίβεια OCR  

| Συμβουλή | Αιτία |
|-----|--------|
| **Προεπεξεργασία της εικόνας** (αύξηση αντίθεσης, δυαδικοποίηση) | Καθαρές εικονοστοιχεία μειώνουν τις λανθασμένες αναγνώσεις. |
| **Χρήση σάρωσης υψηλής ανάλυσης (≥300 dpi)** | Περισσότερες λεπτομέρειες δίνουν στη μηχανή περισσότερα στοιχεία. |
| **Ενεργοποίηση μοντέλων γλώσσας** (`config.setLanguage("en")`) | Συμφωνεί η διόρθωση ορθογραφίας με το σωστό λεξιλόγιο. |
| **Παροχή προσαρμοσμένου λεξικού** | Διαχειρίζεται λέξεις ειδικών τομέων που τα γενικά μοντέλα παραβλέπουν. |
| **Ενεργοποίηση auto‑rotate** | Διαχειρίζεται φωτογραφίες που τραβήχτηκαν σε ασυνήθιες γωνίες. |

Η εφαρμογή πολλών από αυτά μαζί μπορεί να αυξήσει τα ποσοστά επιτυχίας της **αναγνώρισης χειρόγραφου κειμένου** πάνω από το 90 % για τυπικές σημειώσεις.

---

## Συμπέρασμα  

Διασχίσαμε ένα πλήρες, ολοκληρωμένο παράδειγμα που δείχνει πώς να **αναγνωρίσετε χειρόγραφο κείμενο** χρησιμοποιώντας μια Java OCR μηχανή, πώς να **βελτιώσετε την OCR accuracy** με διόρθωση ορθογραφίας και προσαρμοσμένο λεξικό, και πώς να **run OCR on image** αρχεία αφού **load image for OCR**.  

Ο κώδικας είναι αυτόνομος, οι εξηγήσεις καλύπτουν τόσο το *τι* όσο και το *γιατί*, και τώρα έχετε μια σταθερή βάση για να προσαρμόσετε τη διαδικασία στα δικά σας έργα—είτε πρόκειται για επεξεργασία παρτίδας αποδείξεων, ψηφιοποίηση σημειώσεων διαλέξεων, ή τροφοδότηση του αναγνωρισμένου κειμένου σε ένα επόμενο μοντέλο AI.

### Τι ακολουθεί;

* Δοκιμάστε διαφορετικές βιβλιοθήκες προεπεξεργασίας εικόνας (OpenCV, TwelveMonkeys) για να δείτε πώς οι ρυθμίσεις αντίθεσης επηρεάζουν τα αποτελέσματα.  
* Δοκιμάστε να αλλάξετε το μοντέλο γλώσσας σε άλλη τοπική ρύθμιση αν έχετε πολυγλωσσικές σημειώσεις.  
* Ενσωματώστε το βήμα OCR σε ένα μικροϋπηρεσία Spring Boot ώστε άλλες εφαρμογές να μπορούν να **run OCR on image** μέσω ενός REST endpoint.  

Αν αντιμετωπίσετε δυσκολίες ή έχετε ιδέες για περαιτέρω βελτιώσεις, αφήστε ένα σχόλιο παρακάτω. Καλή προγραμματιστική, και εύχομαι οι χειρόγραφες σαρώσεις σας να γίνουν τελικά αναγνώσιμο κείμενο!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}