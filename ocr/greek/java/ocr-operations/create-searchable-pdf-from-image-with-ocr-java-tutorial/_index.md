---
category: general
date: 2026-01-07
description: Δημιουργήστε PDF με δυνατότητα αναζήτησης από μια εικόνα χρησιμοποιώντας
  το Aspose OCR σε Java. Μάθετε πώς να μετατρέψετε την εικόνα σε PDF, να αναγνωρίσετε
  κείμενο από την εικόνα και να δημιουργήσετε PDF από JPG.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- recognize text from image
- how to use ocr
- generate pdf from jpg
language: el
og_description: Δημιουργήστε PDF με δυνατότητα αναζήτησης από μια εικόνα με το Aspose
  OCR σε Java. Οδηγός βήμα‑προς‑βήμα για τη μετατροπή εικόνας σε PDF, την αναγνώριση
  κειμένου από την εικόνα και τη δημιουργία PDF από JPG.
og_title: Δημιουργία Αναζητήσιμου PDF από Εικόνα – Οδηγός OCR σε Java
tags:
- OCR
- Java
- PDF
- Aspose
title: Δημιουργία Αναζητήσιμου PDF από Εικόνα με OCR – Εκμάθηση Java
url: /el/java/ocr-operations/create-searchable-pdf-from-image-with-ocr-java-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Αναζητήσιμου PDF από Εικόνα με OCR – Java Tutorial

Έχετε χρειαστεί ποτέ να **δημιουργήσετε αναζητήσιμο PDF** από μια σαρωμένη εικόνα αλλά δεν ήξερατε από πού να ξεκινήσετε; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν προσπαθούν για πρώτη φορά να μετατρέψουν ένα JPEG σε PDF που μπορείτε πραγματικά να αναζητήσετε.  

Σε αυτόν τον οδηγό θα περάσουμε από ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει πώς να **μετατρέψετε εικόνα σε PDF**, **αναγνωρίσετε κείμενο από εικόνα**, και τελικά **δημιουργήσετε PDF από JPG** χρησιμοποιώντας το Aspose OCR for Java. Καμία ασαφής αναφορά, μόνο κώδικας που μπορείτε να αντιγράψετε‑επικολλήσετε και να τρέξετε σήμερα.

## Τι Θα Χρειαστείτε

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τα παρακάτω στο μηχάνημά σας:

* **Java 17** ή νεότερη (το API λειτουργεί με οποιοδήποτε πρόσφατο JDK).  
* **Aspose.OCR for Java** βιβλιοθήκη – μπορείτε να κατεβάσετε το τελευταίο JAR από το Maven Central ή την ιστοσελίδα της Aspose.  
* Μια δείγμα εικόνας, π.χ. `sample.jpg`, τοποθετημένη σε φάκελο που μπορείτε να αναφέρετε.  
* Ένα IDE ή έναν απλό επεξεργαστή κειμένου μαζί με τερματικό—ό,τι σας βολεύει.

Αυτό είναι όλο. Χωρίς βαρύτατα frameworks, χωρίς επιπλέον εγγενείς εξαρτήσεις. Ας ξεκινήσουμε.

## Βήμα 1 – Δημιουργία Αναζητήσιμου PDF: Αρχικοποίηση του OCR Engine

Το πρώτο που κάνουμε είναι να δημιουργήσουμε ένα αντικείμενο `OcrEngine` και να το κατευθύνουμε στην πηγή εικόνας. Αυτό το αντικείμενο είναι η καρδιά του Aspose OCR· διαχειρίζεται τα πάντα, από τη φόρτωση του bitmap μέχρι την έκθεση του αναγνωρισμένου κειμένου.

```java
import com.aspose.ocr.*;

public class HelloOcrTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the image you want to turn into a searchable PDF
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

> **Γιατί είναι σημαντικό:** Η σωστή αρχικοποίηση του engine εξασφαλίζει ότι η βιβλιοθήκη μπορεί να διαβάσει τη μορφή εικόνας που της παρέχετε. Αν η διαδρομή είναι λανθασμένη, θα λάβετε `FileNotFoundException` και όλη η αλυσίδα θα σταματήσει.

## Βήμα 2 – Βελτιστοποίηση Απόδοσης: Ενεργοποίηση GPU, Πολυπύρηνου CPU και Διόρθωση Ορθογραφίας

Το OCR μπορεί να καταναλώνει πολύ CPU, ειδικά σε μεγάλα έγγραφα. Το Aspose παρέχει μερικές ρυθμίσεις που μπορείτε να ενεργοποιήσετε για να κάνετε τη διαδικασία πιο γρήγορη και ακριβή.

```java
        // 2️⃣ Turn on performance helpers – GPU, multi‑core CPU, and spell correction
        ocrEngine.getEngineOptions()
                 .setUseGpu(true)                 // uses GPU if one is available
                 .setUseMultiCore(true)           // spreads work across CPU cores
                 .setEnableSpellCorrection(true); // cleans up common OCR mistakes
```

> **Συμβουλή:** Αν τρέχετε σε διακομιστή χωρίς GPU, το `setUseGpu(false)` δεν θα προκαλέσει πρόβλημα—απλώς θα επιστρέψετε στην επεξεργασία με πολυπύρηνο CPU.

## Βήμα 3 – Βελτίωση Ποιότητας Εικόνας: Διόρθωση Στρέψης και Απομάκρυνση Θορύβου (Προαιρετικό αλλά Συνιστάται)

Οι σαρώσεις σπάνια είναι τέλειες. Μικρή κλίση ή θόρυβος μπορεί να μπλοκάρει τον αναγνώστη. Η κλάση `ImageProcessingOptions` σας επιτρέπει να καθαρίσετε την εικόνα πριν ο engine προσπαθήσει να την διαβάσει.

```java
        // 3️⃣ Pre‑process the image – straighten it and remove noise
        ocrEngine.getImageProcessingOptions()
                 .setDeskew(true)   // automatically rotates tilted text
                 .setDespeckle(true); // reduces background speckles
```

> **Ακραία περίπτωση:** Αν η πηγή εικόνας είναι ήδη καθαρή, μπορείτε να παραλείψετε αυτό το βήμα. Δεν θα βλάψει, αλλά προσθέτει μερικά χιλιοστά του δευτερολέπτου επιπλέον χρόνου.

## Βήμα 4 – Αναγνώριση Κειμένου από Εικόνα και Δημιουργία PDF

Τώρα συμβαίνει η μαγεία. Καλούμε το `recognize()` και ο engine επιστρέφει ένα `OcrResult`. Από εκεί μπορούμε να αποθηκεύσουμε το αποτέλεσμα σε διάφορες μορφές—το PDF είναι η πιο κοινή για αναζητήσιμα έγγραφα.

```java
        // 4️⃣ Perform OCR and get the result object
        OcrResult ocrResult = ocrEngine.recognize();

        // 5️⃣ Save the result as a searchable PDF (you could also choose TXT, DOCX, etc.)
        ocrResult.save("YOUR_DIRECTORY/sample-output.pdf", OcrOutputFormat.PDF);
    }
}
```

> **Τι θα δείτε:** Το `sample-output.pdf` περιέχει την αρχική εικόνα ως επίπεδο φόντου, ενώ το αναγνωρισμένο κείμενο βρίσκεται από πάνω ως αόρατη επικάλυψη. Ανοίξτε το σε Adobe Reader και προσπαθήστε να επιλέξετε κείμενο—θα εκπλαγείτε.

## Βήμα 5 – Επαλήθευση του Αποτελέσματος Αναζητήσιμου PDF

Αφού το αρχείο γραφτεί, είναι καλή πρακτική να ελέγξετε ξανά ότι το PDF είναι πραγματικά αναζητήσιμο.

```java
import java.awt.Desktop;
import java.io.File;

public class VerifyPdf {
    public static void main(String[] args) throws Exception {
        File pdf = new File("YOUR_DIRECTORY/sample-output.pdf");
        if (pdf.exists() && Desktop.isDesktopSupported()) {
            Desktop.getDesktop().open(pdf); // opens the PDF in the default viewer
        } else {
            System.out.println("PDF not found or cannot be opened on this platform.");
        }
    }
}
```

Ανοίξτε το PDF, πατήστε **Ctrl F**, πληκτρολογήστε μια λέξη που γνωρίζετε ότι εμφανίζεται στην εικόνα—αν η αναζήτηση τη βρει, έχετε δημιουργήσει επιτυχώς **αναζητήσιμο pdf**!

## Πώς να Χρησιμοποιήσετε το OCR σε Πραγματικές Περιπτώσεις (Bonus)

* **Επεξεργασία παρτίδας:** Τυλίξτε τον κώδικα σε βρόχο που διατρέχει έναν φάκελο με JPG. Θυμηθείτε να επαναχρησιμοποιείτε ένα μόνο αντικείμενο `OcrEngine` για να κρατήσετε τη χρήση μνήμης χαμηλή.  
* **Υποστήριξη γλωσσών:** Το Aspose OCR υποστηρίζει πάνω από 60 γλώσσες. Απλώς καλέστε `ocrEngine.getEngineOptions().setLanguage(Language.English);` (ή οποιαδήποτε άλλη τιμή enum).  
* **Διαχείριση σφαλμάτων:** Πιάστε `OcrException` για να χειριστείτε κορεσμένα αρχεία με χάρη.  

Αυτές οι προσαρμογές κάνουν τη λύση ανθεκτική για παραγωγικές γραμμές εργασίας.

## Πλήρες Παράδειγμα Java – Δημιουργία Αναζητήσιμου PDF από JPG

Παρακάτω είναι το πλήρες, αυτόνομο πρόγραμμα που μπορείτε να μεταγλωττίσετε και να τρέξετε όπως είναι. Αντικαταστήστε το `YOUR_DIRECTORY` με την πραγματική διαδρομή στο σύστημά σας.

```java
import com.aspose.ocr.*;

public class CreateSearchablePdf {
    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Load the source image
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // -------------------------------------------------
        // 2️⃣ Performance helpers
        // -------------------------------------------------
        ocrEngine.getEngineOptions()
                 .setUseGpu(true)
                 .setUseMultiCore(true)
                 .setEnableSpellCorrection(true);

        // -------------------------------------------------
        // 3️⃣ Image pre‑processing (optional but helpful)
        // -------------------------------------------------
        ocrEngine.getImageProcessingOptions()
                 .setDeskew(true)
                 .setDespeckle(true);

        // -------------------------------------------------
        // 4️⃣ Run OCR and save as searchable PDF
        // -------------------------------------------------
        OcrResult result = ocrEngine.recognize();
        result.save("YOUR_DIRECTORY/sample-output.pdf", OcrOutputFormat.PDF);

        System.out.println("✅ Searchable PDF created at YOUR_DIRECTORY/sample-output.pdf");
    }
}
```

**Αναμενόμενο αποτέλεσμα:**  

```
✅ Searchable PDF created at YOUR_DIRECTORY/sample-output.pdf
```

Ανοίξτε το παραγόμενο PDF και θα πρέπει να μπορείτε να αναζητήσετε οποιαδήποτε λέξη εμφανίστηκε στο `sample.jpg`. Αν δεν δείτε το επίπεδο κειμένου, ελέγξτε ξανά τη διαδρομή της εικόνας και βεβαιωθείτε ότι ο OCR engine δεν πετάει κρυφές εξαιρέσεις.

## Συμπέρασμα

Σας δείξαμε πώς να **δημιουργήσετε αναζητήσιμο PDF** από ένα JPEG χρησιμοποιώντας το Aspose OCR for Java. Από τη φόρτωση της εικόνας, τη ρύθμιση των παραμέτρων απόδοσης, τον καθαρισμό της εικόνας, μέχρι την τελική αναγνώριση κειμένου και αποθήκευση ενός αναζητήσιμου PDF—κάθε βήμα εξηγήθηκε με το *γιατί* και το *πώς*.  

Τώρα μπορείτε να **μετατρέψετε εικόνα σε PDF**, **αναγνωρίσετε κείμενο από εικόνα**, και **δημιουργήσετε PDF από JPG** στις δικές σας εφαρμογές. Στο επόμενο βήμα, δοκιμάστε την επεξεργασία ολόκληρου φακέλου σαρώσεων, πειραματιστείτε με διαφορετικές γλώσσες, ή προσθέστε προστασία με κωδικό πρόσβασης στο παραγόμενο PDF. Ο ουρανός είναι το όριο.

Έχετε ερωτήσεις σχετικά με ακραίες περιπτώσεις, άδειες ή βελτιστοποίηση απόδοσης; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική! 

![Διάγραμμα που απεικονίζει τη ροή εργασίας OCR – δημιουργία αναζητήσιμου pdf](/images/ocr-pipeline.png "Διάγραμμα δημιουργίας αναζητήσιμου PDF")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}