---
category: general
date: 2026-01-12
description: Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας το Aspose OCR σε Java. Μάθετε
  πώς να εξάγετε κείμενο από εικόνα τιμολόγησης με ένα παράδειγμα OCR σε Java και
  να λάβετε το κείμενο εξόδου OCR.
draft: false
keywords:
- extract text from image
- how to extract text
- java ocr example
- process invoice image
- output ocr text
language: el
og_description: Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας το Aspose OCR σε Java.
  Αυτός ο οδηγός δείχνει πώς να εξάγετε κείμενο από εικόνα τιμολογίου, περιλαμβάνει
  ένα παράδειγμα OCR σε Java και εμφανίζει το κείμενο OCR.
og_title: Εξαγωγή κειμένου από εικόνα σε Java – Πλήρες παράδειγμα OCR
tags:
- OCR
- Java
- Aspose
title: Εξαγωγή κειμένου από εικόνα σε Java – Πλήρες παράδειγμα OCR
url: /el/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Εικόνα σε Java – Πλήρες Παράδειγμα OCR

Έχετε ποτέ αναρωτηθεί πώς να **εξαγάγετε κείμενο από εικόνα** αρχεία χωρίς να τσακίζετε τα μαλλιά σας; Ίσως έχετε μια στοίβα σαρωμένων τιμολογίων και χρειάζεστε τους αριθμούς γρήγορα. Κατά τη γνώμη μου, ο πιο εύκολος τρόπος είναι να αφήσετε μια εξειδικευμένη βιβλιοθήκη OCR να κάνει τη σκληρή δουλειά. Αυτό το σεμινάριο δείχνει *πώς να εξάγετε κείμενο* από μια τυπική εικόνα τιμολογίου χρησιμοποιώντας το Aspose OCR for Java, και ακόμη παρουσιάζει ένα **java ocr example** που παράγει το κείμενο OCR που μπορείτε να μεταβιβάσετε στο σύστημα downstream.

> **Τι θα λάβετε:** ένα έτοιμο‑για‑εκτέλεση πρόγραμμα Java, σαφείς εξηγήσεις κάθε βήματος, και πρακτικές συμβουλές για τη διαχείριση πραγματικών τιμολογίων.

## Προαπαιτούμενα

- Java Development Kit (JDK) 8 ή νεότερο εγκατεστημένο.
- Maven ή Gradle για διαχείριση εξαρτήσεων (παρατίθεται παράδειγμα Maven).
- Άδεια Aspose OCR for Java (η δωρεάν δοκιμή λειτουργεί για δοκιμές).
- Μια εικόνα τιμολογίου (`invoice.png`) τοποθετημένη σε γνωστό φάκελο.

Αν κάποιο από αυτά σας φαίνεται άγνωστο, μην ανησυχείτε — τα περισσότερα είναι απλώς ένα κλικ μακριά, και ο κώδικας θα εξακολουθήσει να μεταγλωττίζεται με την έκδοση community.

## Βήμα 1: Ρύθμιση του Maven Project σας

Πρώτα, δημιουργήστε ένα νέο Maven project (ή προσθέστε σε ένα υπάρχον). Στο `pom.xml` σας, προσθέστε την εξάρτηση Aspose OCR:

```xml
<!-- pom.xml -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.9</version> <!-- Use the latest version available -->
    </dependency>
</dependencies>
```

> **Pro tip:** Κρατήστε τον αριθμό έκδοσης ενημερωμένο· οι νεότερες εκδόσεις συχνά βελτιώνουν την ακρίβεια για δύσκολες γραμματοσειρές που βρίσκονται σε τιμολόγια.

Μετά την αποθήκευση του αρχείου, εκτελέστε `mvn clean install` για να κατεβάσετε τη βιβλιοθήκη στο τοπικό σας αποθετήριο.

## Βήμα 2: Φόρτωση της Εικόνας Τιμολογίου

Τώρα που η βιβλιοθήκη είναι έτοιμη, ας γράψουμε μια μικρή κλάση Java. Το πρώτο που κάνουμε είναι να δημιουργήσουμε μια παρουσία `OcrEngine` και να την κατευθύνουμε στην εικόνα που θέλετε να διαβάσετε.

```java
import com.aspose.ocr.*;

public class RoiExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage("YOUR_DIRECTORY/invoice.png"); // <-- replace with your path
```

Γιατί δημιουργούμε τη μηχανή **πριν** φορτώσουμε την εικόνα; Η μηχανή διατηρεί ρυθμίσεις όπως γλώσσα, DPI και ROI. Ορίζοντας την εικόνα νωρίς εξασφαλίζουμε ότι αυτές οι ρυθμίσεις εφαρμόζονται στο ακριβές αρχείο που πρόκειται να επεξεργαστούμε.

## Βήμα 3: Ορισμός Περιοχών Ενδιαφέροντος (ROI)

Τα τιμολόγια συχνά περιέχουν πολύ θόρυβο — πίνακες, λογότυπα και μικρογράμματα. Περιορίζοντας το OCR μόνο στην κεφαλίδα και το συνολικό ποσό, αυξάνετε δραστικά τόσο την ταχύτητα όσο και την ακρίβεια. Το Aspose σας επιτρέπει να περιγράψετε αυτές τις ζώνες με ορθογώνια.

```java
        // Step 3: Define the regions of interest (header and total amount)
        OcrRegion region = OcrRegion.builder()
                .addRectangle(0, 0, 800, 150)      // header area
                .addRectangle(0, 1200, 800, 200)   // total amount area
                .build();

        // Apply ROI to the engine
        engine.setRegion(region);
```

Οι συντεταγμένες είναι σε εικονοστοιχεία (`x`, `y`, `width`, `height`). Αν τα τιμολόγια σας διαφέρουν σε μέγεθος, μπορείτε να υπολογίσετε αυτές τις τιμές δυναμικά — ίσως ελέγχοντας πρώτα τις διαστάσεις της εικόνας. Αυτή είναι μια ωραία επέκταση αν χρειάζεστε μια λύση **process invoice image** που λειτουργεί σε παρτίδες.

## Βήμα 4: Εκτέλεση OCR στις Καθορισμένες Περιοχές

Με το ROI σε θέση, η μηχανή OCR μπορεί να εστιάσει την προσοχή της εκεί που έχει μεγαλύτερη σημασία. Η μέθοδος `recognize()` επιστρέφει ένα `OcrResult` που περιέχει το εξαγόμενο κείμενο.

```java
        // Step 4: Run OCR on the specified regions
        OcrResult result = engine.recognize();
```

Πίσω από τη σκηνή, το Aspose εκτελεί αρκετά βήματα προεπεξεργασίας: δυαδικοποίηση, αφαίρεση θορύβου και τμηματοποίηση χαρακτήρων. Δεν χρειάζεται να τα καλέσετε χειροκίνητα — απλώς αφήστε το `recognize()` να κάνει τη δουλειά του.

## Βήμα 5: Εξαγωγή του Εξαχθέντος Κειμένου

Τέλος, εκτυπώνουμε το κείμενο στην κονσόλα. Σε μια πραγματική εφαρμογή μπορεί να το αποθηκεύσετε σε βάση δεδομένων, να το περάσετε σε μια downstream pipeline ανάλυσης, ή ακόμη να δημιουργήσετε ένα αναζητήσιμο PDF.

```java
        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(result.getText());
    }
}
```

Όταν εκτελέσετε το πρόγραμμα, θα πρέπει να δείτε κάτι όπως:

```
ROI text:
Acme Corp.
Invoice #12345
Date: 2025-12-31
Total Amount: $1,250.00
```

Αν η έξοδος φαίνεται ακατάληπτη, ελέγξτε ξανά τις συντεταγμένες του ορθογωνίου ή αυξήστε την ανάλυση της εικόνας. Οι μηχανές OCR αγαπούν καθαρές, υψηλής DPI σαρώσεις.

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω βρίσκεται το πλήρες, αυτόνομο αρχείο Java που μπορείτε να αντιγράψετε‑επικολλήσετε στο `src/main/java/RoiExample.java`. Δεν απαιτούνται εξωτερικά αποσπάσματα — όλα όσα χρειάζεστε είναι εδώ.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.region.*;

public class RoiExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage("YOUR_DIRECTORY/invoice.png");

        // Step 2: Define the regions of interest (header and total amount)
        OcrRegion region = OcrRegion.builder()
                .addRectangle(0, 0, 800, 150)      // header area
                .addRectangle(0, 1200, 800, 200)   // total amount area
                .build();

        // Step 3: Apply the ROI configuration to the engine
        engine.setRegion(region);

        // Step 4: Run OCR on the specified regions
        OcrResult result = engine.recognize();

        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(result.getText());
    }
}
```

> **Σημείωση:** Αντικαταστήστε το `YOUR_DIRECTORY` με την απόλυτη διαδρομή προς την εικόνα του τιμολογίου σας. Αν χρησιμοποιείτε σχετική διαδρομή, βεβαιωθείτε ότι ο τρέχων φάκελος ταιριάζει με το σημείο όπου εκτελείτε την εντολή `java`.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν το μέγεθος του τιμολογίου αλλάζει;

Μπορείτε να υπολογίσετε το ROI δυναμικά:

```java
int imgWidth = engine.getImage().getWidth();
int imgHeight = engine.getImage().getHeight();

int headerHeight = imgHeight / 10;
int totalHeight = imgHeight / 8;

OcrRegion region = OcrRegion.builder()
        .addRectangle(0, 0, imgWidth, headerHeight)
        .addRectangle(0, imgHeight - totalHeight, imgWidth, totalHeight)
        .build();
```

### Πώς να διαχειριστώ πολλαπλές γλώσσες;

Το Aspose OCR υποστηρίζει πακέτα γλωσσών. Απλώς ορίστε τη γλώσσα πριν καλέσετε το `recognize()`:

```java
engine.setLanguage(OcrLanguage.Spanish); // or OcrLanguage.English, etc.
```

### Τι γίνεται αν το OCR επιστρέψει κενές συμβολοσειρές;

Τυπικοί λόγοι είναι:

- Χαμηλή ανάλυση εικόνας (< 300 DPI). Ανεβάστε την ανάλυση ή ζητήστε σαρώσεις υψηλότερης ποιότητας.
- Πολύ σκοτεινά ή πολύ φωτεινά υπόβαθρα. Εφαρμόστε ένα απλό φίλτρο ενίσχυσης αντίθεσης πριν το OCR.
- Λανθασμένες συντεταγμένες ROI που παραβλέπουν εντελώς το κείμενο.

## Συμβουλές για OCR Έτοιμο για Παραγωγή

1. **Batch Processing:** Τυλίξτε τη λογική σε έναν βρόχο που διατρέχει έναν φάκελο με αρχεία τιμολογίων. Καταγράψτε κάθε αποτέλεσμα για δυνατότητα ελέγχου.
2. **Error Handling:** Πιάστε το `OcrException` για να παραλείψετε ευαίσθητες εικόνες χωρίς να διακόψετε ολόκληρη τη δουλειά.
3. **Performance:** Επαναχρησιμοποιήστε μια ενιαία παρουσία `OcrEngine` για πολλαπλές εικόνες· η δημιουργία νέας μηχανής ανά αρχείο προσθέτει περιττό φορτίο.
4. **Validation:** Μετά την εξαγωγή, εκτελέστε έναν έλεγχο regex στο συνολικό ποσό (`\$\d{1,3}(,\d{3})*(\.\d{2})?`) για να διασφαλίσετε ότι ο αριθμός φαίνεται ρεαλιστικός.

Η υλοποίηση αυτών των προτάσεων μετατρέπει ένα απλό **java ocr example** σε μια ανθεκτική, κλιμακώσιμη λύση για κάθε επιχείρηση που χρειάζεται να **process invoice image** αρχεία καθημερινά.

## Συμπέρασμα

Μόλις καλύψαμε πώς να **εξάγετε κείμενο από εικόνα** αρχεία σε Java χρησιμοποιώντας το Aspose OCR, εστιάζοντας σε ένα πρακτικό σενάριο επεξεργασίας τιμολογίων. Ορίζοντας μια περιοχή ενδιαφέροντος, εκτελώντας τη μηχανή OCR και εκτυπώνοντας το **output OCR text**, έχετε τώρα μια ισχυρή βάση για την κατασκευή αυτοματοποιημένων pipelines συλλογής δεδομένων.

Επόμενα βήματα; Δοκιμάστε να επεκτείνετε το ROI ώστε να περιλαμβάνει πίνακες γραμμών, πειραματιστείτε με διαφορετικές ρυθμίσεις γλώσσας, ή περάστε τις εξαγόμενες συμβολοσειρές σε μια βιβλιοθήκη δημιουργίας PDF για αναζητήσιμα έγγραφα. Ο ουρανός είναι το όριο όταν συνδυάζετε OCR με σύγχρονα εργαλεία Java.

Έχετε περισσότερες ερωτήσεις σχετικά με το **πώς να εξάγετε κείμενο** από άλλους τύπους εγγράφων, ή χρειάζεστε βοήθεια για τη ρύθμιση του ROI σε ασυνήθιστα layouts; Αφήστε ένα σχόλιο παρακάτω — καλή κωδικοποίηση!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}