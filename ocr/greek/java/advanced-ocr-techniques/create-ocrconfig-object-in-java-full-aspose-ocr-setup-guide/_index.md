---
category: general
date: 2026-06-25
description: Δημιουργήστε αντικείμενο OCRConfig στη Java και ενεργοποιήστε τη λειτουργία
  αξιολόγησης του Aspose OCR. Μάθετε πώς να ορίσετε όριο σελίδων, να αρχικοποιήσετε
  τη μηχανή και να εκτελείτε OCR αποδοτικά.
draft: false
keywords:
- create ocrconfig object
- aspose ocr evaluation mode
- java ocr configuration
- set page limit ocr
- asposeocr engine initialization
language: el
og_description: Create OCRConfig object in Java, enable Aspose OCR evaluation mode,
  and configure page limits. Follow this step‑by‑step tutorial for a ready‑to‑use
  OCR engine.
og_title: Δημιουργία αντικειμένου OCRConfig σε Java – Πλήρης οδηγός Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Create OCRConfig object in Java and enable Aspose OCR evaluation mode.
    Learn to set page limit, initialize the engine, and run OCR efficiently.
  headline: Create OCRConfig Object in Java – Full Aspose OCR Setup Guide
  type: TechArticle
tags:
- Aspose OCR
- Java
- OCR Configuration
title: Δημιουργία αντικειμένου OCRConfig σε Java – Πλήρης οδηγός εγκατάστασης Aspose
  OCR
url: /el/java/advanced-ocr-techniques/create-ocrconfig-object-in-java-full-aspose-ocr-setup-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία αντικειμένου OCRConfig σε Java – Πλήρης Οδηγός Ρύθμισης Aspose OCR

Έχετε ποτέ χρειαστεί να **δημιουργήσετε αντικείμενο OCRConfig** σε Java αλλά δεν ήσασταν σίγουροι ποιες ιδιότητες πρέπει να ρυθμίσετε πρώτα; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν εμπόδιο όταν προσπαθούν να ενεργοποιήσουν τη λειτουργία αξιολόγησης του Aspose OCR ενώ ταυτόχρονα διατηρούν τον προϋπολογισμό επεξεργασίας υπό έλεγχο.

Το θέμα είναι το εξής: με ένα σωστά διαμορφωμένο `OCRConfig`, μπορείτε να ξεκινήσετε τη μηχανή AsposeOCR σε λίγα δευτερόλεπτα, να περιορίσετε τον αριθμό των σελίδων που θα επεξεργαστεί και να εξάγετε αξιόπιστο κείμενο. Σε αυτό το tutorial θα περάσουμε από κάθε γραμμή που χρειάζεστε, θα εξηγήσουμε *γιατί* κάθε ρύθμιση είναι σημαντική και θα σας δώσουμε ένα πλήρες, εκτελέσιμο παράδειγμα που μπορείτε να ενσωματώσετε στο πρόγραμμά σας άμεσα.

> **Τι θα αποκομίσετε**  
> * Ένα λειτουργικό απόσπασμα Java που **δημιουργεί αντικείμενο OCRConfig** με ενεργοποιημένη τη λειτουργία αξιολόγησης.  
> * Γνώση για το **πώς να θέσετε όριο σελίδων OCR** ώστε να αποφύγετε ανεξέλεγκτη επεξεργασία.  
> * Μια σαφή διαδρομή για **την αρχικοποίηση της μηχανής AsposeOCR** ώστε να ξεκινήσετε αμέσως την αναγνώριση κειμένου.  

Καμία εξωτερική τεκμηρίωση, καμία ασαφής αναφορά — μόνο καθαρός κώδικας, στέρεη λογική και μερικές επαγγελματικές συμβουλές που δεν θα βρείτε στο επίσημο quick‑start.

---

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

* Java 17 (ή οποιοδήποτε πρόσφατο JDK) εγκατεστημένο στο σύστημά σας.  
* Το Maven artifact **Aspose.OCR for Java** προστιθέμενο στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.11</version> <!-- Use the latest version available -->
</dependency>
```

* Ένα IDE ή επεξεργαστή με τον οποίο αισθάνεστε άνετα (IntelliJ IDEA, Eclipse, VS Code…).

Αυτό είναι όλο. Δεν χρειάζονται επιπλέον εγγενείς βιβλιοθήκες, ούτε προβλήματα αδειοδότησης για την έκδοση αξιολόγησης — το Aspose παρέχει όλα όσα χρειάζεστε μέσα στο JAR.

---

## Βήμα 1: **Create OCRConfig Object** σε Java

Το πρώτο πράγμα που κάνετε όταν δουλεύετε με το Aspose OCR είναι να δημιουργήσετε ένα `OcrConfig`. Σκεφτείτε το ως τον πίνακα ελέγχου για ολόκληρη τη μηχανή.

```java
// Step 1: Create an OCR configuration object
OcrConfig ocrConfig = new OcrConfig();
```

Γιατί ξεκινάμε από εδώ; Το `OcrConfig` περιέχει τα πάντα, από πακέτα γλωσσών μέχρι ρυθμίσεις απόδοσης. Αν παραλείψετε αυτό το βήμα, η μηχανή θα επιστρέψει στις προεπιλογές της — συνήθως εντάξει για γρήγορα demos, αλλά όχι ιδανικό για παραγωγικά φορτία εργασίας όπου απαιτείται πιο αυστηρός έλεγχος.

> **Pro tip:** Μπορείτε να επαναχρησιμοποιήσετε το ίδιο `OCRConfig` σε πολλαπλές παρουσίες `AsposeOCR` εάν επεξεργάζεστε παρτίδες παράλληλα. Απλώς βεβαιωθείτε ότι δεν το τροποποιείτε μετά την εκκίνηση της μηχανής.

---

## Βήμα 2: Ενεργοποίηση **Aspose OCR Evaluation Mode** και **Set Page Limit OCR**

Η λειτουργία αξιολόγησης είναι ένα «sandbox» που σας επιτρέπει να δοκιμάσετε τη μηχανή OCR χωρίς να καταναλώνετε το αδειοδοτημένο σας απόθεμα. Συνδυάστε το με όριο σελίδων και δεν θα επεξεργαστείτε ποτέ περισσότερες σελίδες από ό,τι προοριζόσασταν.

```java
// Step 2: Enable evaluation mode and limit the number of pages processed
EvaluationSettings evalSettings = new EvaluationSettings()
        .setEnabled(true)          // Turn on evaluation mode
        .setPageLimit(100);        // Process at most 100 pages
ocrConfig.setEvaluationSettings(evalSettings);
```

*`setEnabled(true)`* ενεργοποιεί τη λειτουργία αξιολόγησης. Όταν αργότερα καλέσετε `ocrEngine.recognize(...)`, το Aspose θα μετρήσει τις σελίδες ενάντια στο όριο των 100 σελίδων που ορίσατε με `setPageLimit`. Μόλις το όριο επιτευχθεί, η μηχανή ρίχνει μια φιλική εξαίρεση, επιτρέποντας στην εφαρμογή σας να σταματήσει ομαλά.

**Γιατί να σας ενδιαφέρουν τα όρια σελίδων;**  
Η επεξεργασία μεγάλων PDF μπορεί να καταναλώνει πολύ μνήμη. Θέτοντας όριο στον αριθμό των σελίδων, προστατεύετε το διακομιστή σας από σφάλματα OOM και διατηρείτε το μοντέλο κόστους προβλέψιμο — κάτι ιδιαίτερα σημαντικό όταν μεταβαίνετε από την αξιολόγηση σε πληρωμένη άδεια.

---

## Βήμα 3: **AsposeOCR Engine Initialization** με τις Διαμορφωμένες Ρυθμίσεις

Τώρα που το `OCRConfig` είναι πλήρως διαμορφωμένο, το περνάμε στον κατασκευαστή `AsposeOCR`. Εδώ αρχίζει η «μαγεία» (ή μάλλον η βαριά δουλειά).

```java
// Step 3: Initialise the AsposeOCR engine with the configured settings
AsposeOCR ocrEngine = new AsposeOCR(ocrConfig);
```

Στο παρασκήνιο, το Aspose διαβάζει τις `EvaluationSettings` που δώσατε, κατανέμει εσωτερικές μνήμες και προφορτώνει τα δεδομένα γλώσσας. Αν κάτι είναι λανθασμένο, θα λάβετε αμέσως ένα `IllegalArgumentException` — πολύ πιο φιλικό από μια σιωπηλή αποτυχία αργότερα.

> **Edge case:** Εάν τρέχετε σε περιβάλλον κοντέινερ, βεβαιωθείτε ότι η JVM διαθέτει αρκετό heap (`-Xmx` flag). Η μηχανή OCR μπορεί να καταναλώσει έως και 2 GB για εικόνες υψηλής ανάλυσης.

---

## Βήμα 4: Εκτέλεση Λειτουργιών OCR μετά τη Διαμόρφωση

Με τη μηχανή έτοιμη, μπορείτε τώρα να καλέσετε οποιαδήποτε από τις μεθόδους OCR. Παρακάτω υπάρχει ένα γρήγορο παράδειγμα που διαβάζει ένα μοναδικό αρχείο εικόνας και εκτυπώνει το εξαγόμενο κείμενο.

```java
// Step 4: Proceed with normal OCR operations using ocrEngine...
String imagePath = "src/main/resources/sample.png";

try {
    String extractedText = ocrEngine.recognize(imagePath);
    System.out.println("Recognized Text:");
    System.out.println(extractedText);
} catch (Exception e) {
    // Handles both evaluation limit breaches and I/O errors
    System.err.println("OCR failed: " + e.getMessage());
}
```

Αν φτάσετε το όριο των 100 σελίδων, το τμήμα `catch` θα εκτυπώσει κάτι όπως:

```
OCR failed: Evaluation mode page limit of 100 exceeded.
```

Αυτό το μήνυμα είναι σκόπιμα σαφές ώστε να αποφασίσετε αν θα σταματήσετε την επεξεργασία, θα ζητήσετε αναβάθμιση άδειας ή θα χωρίσετε το εισερχόμενο σε μικρότερα τμήματα.

---

## Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι η πλήρης κλάση που μπορείτε να μεταγλωττίσετε και να τρέξετε αμέσως:

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.config.OcrConfig;
import com.aspose.ocr.config.EvaluationSettings;

public class EvalModeTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR configuration object
        OcrConfig ocrConfig = new OcrConfig();

        // Step 2: Enable evaluation mode and limit the number of pages processed
        EvaluationSettings evalSettings = new EvaluationSettings()
                .setEnabled(true)          // Turn on evaluation mode
                .setPageLimit(100);        // Process at most 100 pages
        ocrConfig.setEvaluationSettings(evalSettings);

        // Step 3: Initialise the AsposeOCR engine with the configured settings
        AsposeOCR ocrEngine = new AsposeOCR(ocrConfig);

        // Step 4: Perform OCR on a sample image
        String imagePath = "src/main/resources/sample.png";
        try {
            String extracted = ocrEngine.recognize(imagePath);
            System.out.println("Recognized Text:");
            System.out.println(extracted);
        } catch (Exception e) {
            System.err.println("OCR failed: " + e.getMessage());
        }
    }
}
```

**Αναμενόμενη έξοδος** (υποθέτοντας ότι το `sample.png` περιέχει τη λέξη “Hello”) :

```
Recognized Text:
Hello
```

Αν τρέξετε το πρόγραμμα εναντίον ενός PDF πολλαπλών σελίδων και υπερβείτε το όριο, θα δείτε την προειδοποίηση λειτουργίας αξιολόγησης αντί για το κανονικό αποτέλεσμα.

---

## Συχνές Ερωτήσεις & Pro Tips

| Ερώτηση | Απάντηση |
|----------|--------|
| *Χρειάζομαι άδεια για τη λειτουργία αξιολόγησης;* | Όχι. Η λειτουργία αξιολόγησης είναι δωρεάν, αλλά περιορίζεται από το όριο σελίδων που ορίζετε. |
| *Μπορώ να αλλάξω το όριο σελίδων κατά την εκτέλεση;* | Ναι, απλώς καλέστε `ocrConfig.getEvaluationSettings().setPageLimit(newLimit)` πριν από οποιαδήποτε κλήση OCR. |
| *Τι γίνεται αν θέλω να απενεργοποιήσω την αξιολόγηση μετά τη δοκιμή;* | Ορίστε `setEnabled(false)` ή απλώς παραλείψτε το τμήμα `EvaluationSettings` κατά τη δημιουργία του `OCRConfig`. |
| *Είναι το OCRConfig thread‑safe;* | Το config γίνεται αμετάβλητο μετά τη μεταβίβαση του σε `AsposeOCR`. Κοινή χρήση της μηχανής μεταξύ νημάτων προσφέρει την καλύτερη απόδοση. |

---

## Συμπέρασμα

Μάθατε **πώς να δημιουργήσετε αντικείμενο OCRConfig** σε Java, ενεργοποιήσατε τη **λειτουργία αξιολόγησης Aspose OCR** και θέσατε με ασφάλεια **όριο σελίδων OCR** ώστε η επεξεργασία να παραμένει υπό έλεγχο. Με μια πλήρως αρχικοποιημένη **μηχανή AsposeOCR**, μπορείτε τώρα να αναγνωρίζετε κείμενο από εικόνες, PDF ή οποιαδήποτε υποστηριζόμενη μορφή χωρίς να ανησυχείτε για ανεξέλεγκτη χρήση πόρων.

Τα επόμενα λογικά βήματα είναι η εξερεύνηση πακέτων γλώσσας (`ocrConfig.setLanguage("eng")`), η ρύθμιση προεπεξεργασίας εικόνας ή η ενσωμάτωση της μηχανής σε ένα REST endpoint Spring Boot. Όλα αυτά τα θέματα βασίζονται άμεσα στο θεμέλιο που θέσαμε εδώ.

Έχετε περισσότερες ερωτήσεις; Αφήστε ένα σχόλιο, πειραματιστείτε με διαφορετικά όρια και καλή προγραμματιστική!

---

![Screenshot showing how to create OCRConfig object in Java](/images/create-ocrconfig-object-java.png "create OCRConfig object Java example")


## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κυριαρχήσετε σε πρόσθετα χαρακτηριστικά του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίησή σας.

- [How to Set License and Verify Aspose.OCR License in Java](/ocr/english/java/ocr-basics/set-license/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [OCR Recognizing PDF Documents in Aspose.OCR for Java](/ocr/hongkong/java/ocr-operations/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}