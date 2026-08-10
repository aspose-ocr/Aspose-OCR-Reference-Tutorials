---
category: general
date: 2026-06-19
description: Αυτόματη διόρθωση κλίσης εικόνας χρησιμοποιώντας Aspose OCR σε Java.
  Μάθετε πώς να διορθώνετε την κλίση, να εξάγετε κείμενο με OCR και να λαμβάνετε τη
  γωνία διόρθωσης κλίσης σε λίγα εύκολα βήματα.
draft: false
keywords:
- auto deskew image
- extract text ocr
- how to correct skew
- how to get deskew
language: el
og_description: Αυτόματη διόρθωση κλίσης εικόνας με Aspose OCR σε Java. Ανακαλύψτε
  πώς να διορθώσετε την κλίση, να εξάγετε κείμενο με OCR και να ανακτήσετε τη γωνία
  διόρθωσης—όλα σε έναν οδηγό.
og_title: Αυτόματη ευθυγράμμιση εικόνας σε Java – Πλήρες σεμινάριο Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Auto deskew image using Aspose OCR in Java. Learn how to correct skew,
    extract text OCR and get deskew angle in a few easy steps.
  headline: Auto Deskew Image in Java – Complete Aspose OCR Guide
  type: TechArticle
tags:
- Aspose OCR
- Java
- Image Processing
title: Αυτόματη διόρθωση κλίσης εικόνας σε Java – Πλήρης οδηγός Aspose OCR
url: /el/java/ocr-operations/auto-deskew-image-in-java-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αυτόματη Διόρθωση Στρέψης Εικόνας σε Java – Πλήρης Οδηγός Aspose OCR

Έχετε αναρωτηθεί ποτέ πώς να **auto deskew image** αρχεία πριν εκτελέσετε OCR; Ίσως έχετε τραβήξει μια απόδειξη σε λοξό τραπέζι, ή μια σαρωμένη φόρμα έφτασε με μικρή κλίση, και η εξαγωγή κειμένου καταλήγει σε ακαταλαβίστικα αποτελέσματα. Αυτό είναι ένα συχνό πρόβλημα, ειδικά όταν χρειάζεστε αξιόπιστα αποτελέσματα **extract text OCR** για επεξεργασία downstream.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα τις ακριβείς διαδικασίες για **auto deskew image** αρχεία χρησιμοποιώντας το Aspose OCR για Java, θα σας δείξουμε **how to correct skew**, και θα αποκαλύψουμε **how to get deskew** λεπτομέρειες μόλις ολοκληρωθεί η μηχανή. Στο τέλος, θα έχετε ένα έτοιμο‑για‑εκτέλεση πρόγραμμα Java που όχι μόνο ευθυγραμμίζει τις εικόνες αυτόματα αλλά επίσης εξάγει καθαρό κείμενο από αυτές. Χωρίς περιττές πληροφορίες, μόνο πρακτικός κώδικας και εξηγήσεις που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σήμερα.

## Τι Θα Μάθετε

- Φορτώστε και ενεργοποιήστε την άδεια του Aspose OCR σε ένα έργο Java.  
- Ενεργοποιήστε τη λειτουργία αυτόματης διόρθωσης στρέψης της μηχανής.  
- Ορίστε ένα όριο εμπιστοσύνης για να αποφύγετε την υπερδιόρθωση.  
- Εκτελέστε OCR σε μια λοξή εικόνα και ανακτήστε τη γωνία εφαρμοσμένης διόρθωσης στρέψης.  
- Εξάγετε το αναγνωρισμένο κείμενο με αποτελέσματα βασισμένα στην εμπιστοσύνη.  

**Prerequisites** – ένα Java 8+ SDK, Maven ή Gradle για διαχείριση εξαρτήσεων, και ένα αρχείο άδειας Aspose OCR. Αν είστε νέοι στο Maven, μην ανησυχείτε· θα καλύψουμε το ελάχιστο απόσπασμα `pom.xml` που χρειάζεστε.

---

## ## Αυτόματη Διόρθωση Στρέψης Εικόνας με Aspose OCR – Βήμα 1: Ρύθμιση του Έργου

Πρώτα απ' όλα, ας προσθέσουμε τη βιβλιοθήκη στο έργο σας. Προσθέστε την ακόλουθη εξάρτηση στο `pom.xml` σας (ή την αντίστοιχη καταχώρηση Gradle):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

> **Pro tip:** Παρακολουθείτε τον αριθμό έκδοσης· η Aspose κυκλοφορεί συχνά βελτιώσεις απόδοσης για τους αλγόριθμους deskew.

Μόλις το Maven επιλύσει το artifact, δημιουργήστε μια απλή κλάση Java με όνομα `SkewDemo`. Αυτό θα είναι το πεδίο δοκιμών όπου θα δείξουμε **how to correct skew** και **how to get deskew** πληροφορίες.

## ## Πώς να Διορθώσετε Στρέψη – Βήμα 2: Άδεια και Αρχικοποίηση Μηχανής

Πριν καλέσετε οποιαδήποτε μέθοδο OCR, πρέπει να φορτώσετε την άδειά σας. Διαφορετικά, η βιβλιοθήκη λειτουργεί σε λειτουργία αξιολόγησης και περιορίζει τον αριθμό των σελίδων που μπορείτε να επεξεργαστείτε.

```java
import com.aspose.ocr.*;

public class SkewDemo {
    public static void main(String[] args) throws Exception {
        // Load the Aspose OCR license (replace with your actual path)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

Παρατηρήστε πώς το βήμα άδειας είναι απομονωμένο στην αρχή—αυτό αντικατοπτρίζει τις βέλτιστες πρακτικές όπου η άδεια είναι μια εφάπαξ ρύθμιση, όχι επαναλαμβανόμενη ανά εικόνα. Αν το παραλείψετε, η μηχανή θα πετάξει μια εξαίρεση άδειας, κάτι που είναι κοινό εμπόδιο για τους νέους χρήστες.

## ## Πώς να Λάβετε Deskew – Βήμα 3: Ενεργοποίηση Auto‑Deskew και Ορισμός Εμπιστοσύνης

Τώρα δημιουργούμε την μηχανή OCR και της λέμε να **auto deskew image** αυτόματα. Η κλήση `setAutoDeskew(true)` ενεργοποιεί τον εσωτερικό αλγόριθμο που ανιχνεύει τη γωνία περιστροφής και περιστρέφει το bitmap πίσω σε οριζόντια βάση.

```java
        // Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Enable automatic deskewing
        ocrEngine.setAutoDeskew(true);                     // auto deskew image
        // Define how confident the engine must be before applying the correction
        ocrEngine.setDeskewConfidenceThreshold(0.85);     // 85% confidence is a safe default
```

Γιατί το όριο εμπιστοσύνης; Φανταστείτε μια φωτογραφία ενός διαφημιστικού πινακίδας ληφθείσα σε παράξενη γωνία· η μηχανή μπορεί να υποθέσει μια τεράστια περιστροφή και να χαλάσει το κείμενο. Ορίζοντας το `0.85`, λέμε «εφαρμόστε deskew μόνο αν είμαστε τουλάχιστον 85 % σίγουροι». Μπορείτε να ρυθμίσετε αυτήν την τιμή πάνω ή κάτω ανάλογα με το πόσο θορυβώδη είναι το σύνολο των εικόνων σας.

## ## Εξαγωγή Κειμένου OCR – Βήμα 4: Αναγνώριση Εικόνας

Με τη μηχανή έτοιμη, δώστε της τη διαδρομή μιας λοξής εικόνας. Η μέθοδος `recognizeImage` εκτελεί τόσο το deskew (αν είναι ενεργοποιημένο) όσο και το OCR σε μία μόνο εκτέλεση.

```java
        // Recognize text from a skewed image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/angled-photo.jpg");
```

Αν το αρχείο δεν βρεθεί, η Java θα πετάξει ένα `FileNotFoundException`. Έλεγχος λογικής—βεβαιωθείτε ότι η διαδρομή είναι απόλυτη ή σχετική με τον κατάλογο εργασίας από τον οποίο εκκινείτε το πρόγραμμα.

## ## Αυτόματη Διόρθωση Στρέψης Εικόνας – Βήμα 5: Ανάκτηση Γωνίας Deskew και Εξαγόμενου Κειμένου

Μετά την αναγνώριση, το αντικείμενο `OcrResult` σας δίνει δύο πολύτιμα στοιχεία: τη γωνία που εφάρμοσε η μηχανή και το κείμενο απλού κειμένου.

```java
        // Print the applied deskew angle
        System.out.println("Applied angle: " + ocrResult.getAppliedDeskewAngle());

        // Print the extracted text
        System.out.println("Extracted text:");
        System.out.println(ocrResult.getText());
    }
}
```

Η μέθοδος `getAppliedDeskewAngle()` επιστρέφει ένα `double` που αντιπροσωπεύει μοίρες (θετικό για δεξιόστροφη περιστροφή). Αν η εικόνα ήταν ήδη επίπεδη, θα δείτε `0.0`. Αυτό είναι το βασικό στοιχείο της **how to get deskew** πληροφορίας, η οποία μπορεί να καταγραφεί για αρχεία ελέγχου ή να επιστραφεί σε UI για να δείξει στους χρήστες τη διόρθωση που έγινε στο παρασκήνιο.

## ## Πλήρες Παράδειγμα Εργασίας – Όλα τα Βήματα σε Ένα Αρχείο

Παρακάτω είναι η πλήρης, έτοιμη‑για‑εκτέλεση κλάση Java. Αντιγράψτε την στο IDE σας, αντικαταστήστε τις διαδρομές της άδειας και της εικόνας, και πατήστε *Run*.

```java
import com.aspose.ocr.*;

public class SkewDemo {
    public static void main(String[] args) throws Exception {
        // -------------------- Step 1: License --------------------
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic"); // <-- update path

        // -------------------- Step 2: Engine --------------------
        OcrEngine ocrEngine = new OcrEngine();

        // -------------------- Step 3: Auto‑Deskew --------------------
        ocrEngine.setAutoDeskew(true);                     // auto deskew image
        ocrEngine.setDeskewConfidenceThreshold(0.85);     // high‑confidence only

        // -------------------- Step 4: Recognize --------------------
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/angled-photo.jpg"); // <-- update path

        // -------------------- Step 5: Results --------------------
        System.out.println("Applied angle: " + ocrResult.getAppliedDeskewAngle());
        System.out.println("Extracted text:");
        System.out.println(ocrResult.getText());
    }
}
```

**Αναμενόμενη έξοδος** (παράδειγμα):

```
Applied angle: -2.7
Extracted text:
Invoice #12345
Date: 2024‑04‑01
Total: $89.99
Thank you for your business!
```

Παρατηρήστε πως η γωνία είναι ένας μικρός αρνητικός αριθμός—δηλαδή η αρχική φωτογραφία ήταν λοξοκατευθυνόμενη με μερικές μοίρες αριστερόστροφα, και η Aspose τη διόρθωσε πριν το OCR.

## ## Συνηθισμένα Πιθανά Προβλήματα και Ακραίες Περιπτώσεις

| Ζήτημα | Γιατί Συμβαίνει | Διόρθωση |
|-------|----------------|----------|
| **Δεν εφαρμόστηκε deskew (γωνία = 0)** | Η εικόνα είναι ήδη επίπεδη ή η εμπιστοσύνη είναι κάτω από το όριο. | Μειώστε το `setDeskewConfidenceThreshold` σε `0.6` για θορυβώδεις σαρώσεις. |
| **Αχρείοι χαρακτήρες στην έξοδο** | Η ποιότητα της εικόνας είναι πολύ χαμηλή· ο θόρυβος επηρεάζει τόσο το deskew όσο και το OCR. | Προεπεξεργαστείτε με φίλτρο εξομάλυνσης ή αυξήστε το DPI πριν το δώσετε στην Aspose. |
| **Η άδεια δεν βρέθηκε** | Λάθος διαδρομή ή λείπει το αρχείο. | Χρησιμοποιήστε απόλυτη διαδρομή ή τοποθετήστε το αρχείο `.lic` στην classpath και καλέστε `license.setLicense("Aspose.OCR.lic");`. |
| **Έλλειψη μνήμης σε μεγάλες δέσμες** | Κάθε κλήση φορτώνει ολόκληρη την εικόνα στη μνήμη. | Επαναχρησιμοποιήστε ένα μόνο αντικείμενο `OcrEngine` και καλέστε `ocrEngine.clear()` μετά από κάθε εικόνα. |

## ## Προχωρώντας Περαιτέρω – Επόμενα Βήματα

- **Batch processing:** Επανάληψη σε έναν φάκελο εικόνων, συλλογή κάθε `appliedDeskewAngle` και αποθήκευση των αποτελεσμάτων σε CSV για αναλύσεις.  
- **Language selection:** Χρησιμοποιήστε `ocrEngine.setLanguage(OcrLanguage.English);` για βελτίωση της ακρίβειας σε πολυγλωσσικά έγγραφα.  
- **Region‑based OCR:** Αν σας ενδιαφέρει μόνο μια συγκεκριμένη περιοχή (π.χ., ένας barcode), καλέστε `ocrEngine.recognizeRegion(rect);`.  

Όλες αυτές οι επεκτάσεις εξακολουθούν να ωφελούνται από τη βάση **auto deskew image** που δημιουργήσαμε, επειδή ένα σωστά προσανατολισμένο bitmap είναι ο πιο σημαντικός παράγοντας για OCR υψηλής ποιότητας.

## ## Συμπέρασμα

Συζητήσαμε όλα όσα χρειάζεστε για **auto deskew image** αρχεία σε Java με Aspose OCR, δείξαμε **how to correct skew**, παρουσιάσαμε **how to get deskew** γωνίες, και τελικά εξάγαμε καθαρό κείμενο μέσω **extract text OCR**. Το σύντομο, αυτόνομο πρόγραμμα εκτελείται σε δευτερόλεπτα, αλλά αντιμετωπίζει ένα δύσκολο πρόβλημα που διαφορετικά θα απαιτούσε ξεχωριστή βιβλιοθήκη επεξεργασίας εικόνας.

Δοκιμάστε το με τις δικές σας φωτογραφίες, ρυθμίστε το όριο εμπιστοσύνης, και παρακολουθήστε τη γωνία deskew να εμφανίζεται στην κονσόλα. Μόλις εξοικειωθείτε, προσθέστε λογική batch ή ενσωματώστε το αποτέλεσμα σε μια αλυσίδα διαχείρισης εγγράφων. Ο ουρανός είναι το όριο—απλώς θυμηθείτε ότι μια ευθυγραμμισμένη εικόνα είναι το μυστικό συστατικό πίσω από αξιόπιστο OCR.

Αν αντιμετωπίσετε προβλήματα, αφήστε ένα σχόλιο παρακάτω ή ελέγξτε την επίσημη τεκμηρίωση Java της Aspose για τις τελευταίες αλλαγές API. Καλό προγραμματισμό, και εύχομαι οι σαρώσεις σας να παραμένουν πάντα επίπεδες! 

![Διάγραμμα που απεικονίζει την αυτόματη διόρθωση στρέψης μιας λοξής εικόνας πριν την εξαγωγή OCR – διαδικασία auto deskew image](auto-deskew-diagram.png "ροή εργασίας auto deskew image")

## Τι Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετα χαρακτηριστικά API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να υπολογίσετε τη γωνία στρέψης java χρησιμοποιώντας Aspose.OCR](/ocr/english/java/ocr-basics/calculate-skew-angle/)
- [Αναγνώριση κειμένου εικόνας με Aspose OCR – Πλήρης Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Εξαγωγή Κειμένου από Εικόνα Java με Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}