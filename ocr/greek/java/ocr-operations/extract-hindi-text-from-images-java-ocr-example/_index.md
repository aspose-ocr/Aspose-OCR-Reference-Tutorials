---
category: general
date: 2026-03-18
description: Εξάγετε κείμενο στα Χίντι από μια εικόνα χρησιμοποιώντας Java OCR. Μάθετε
  πώς να μετατρέψετε την εικόνα σε κείμενο με το Aspose OCR σε αυτό το παράδειγμα
  Java OCR.
draft: false
keywords:
- extract hindi text
- convert image to text
- java ocr example
- ocr hindi image
- load image ocr
language: el
og_description: Εξάγετε κείμενο στα Χίντι από μια εικόνα χρησιμοποιώντας Java OCR.
  Αυτός ο οδηγός δείχνει πώς να μετατρέψετε την εικόνα σε κείμενο με το Aspose OCR
  σε ένα σαφές παράδειγμα Java OCR.
og_title: Εξαγωγή κειμένου Χίντι από εικόνες – Παράδειγμα Java OCR
tags:
- Java
- OCR
- Aspose
- Hindi
title: Εξαγωγή κειμένου Χίντι από εικόνες – Παράδειγμα OCR Java
url: /el/java/ocr-operations/extract-hindi-text-from-images-java-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή κειμένου Χίντι από εικόνες – Παράδειγμα Java OCR

Έχετε χρειαστεί ποτέ να **εξάγετε κείμενο Χίντι** από ένα σαρωμένο έγγραφο αλλά δεν ήξερατε από πού να ξεκινήσετε; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το εμπόδιο όταν δουλεύουν με πολυγλωσσικές εικόνες. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες **java ocr example** που δείχνει πώς να **μετατρέψετε εικόνα σε κείμενο** και, πιο σημαντικό, πώς να **εξάγετε αξιόπιστα κείμενο Χίντι** χρησιμοποιώντας το Aspose OCR.

Θα καλύψουμε τα πάντα, από τη ρύθμιση της εξάρτησης Maven μέχρι τη φόρτωση της εικόνας, τη διαμόρφωση της μηχανής για Χίντι και, τέλος, την εκτύπωση του αποτελέσματος. Στο τέλος, θα έχετε ένα έτοιμο‑για‑εκτέλεση πρόγραμμα που μπορεί να **φορτώσει αρχεία τύπου image ocr** και να παράγει καθαρά Unicode strings στα Χίντι. Χωρίς περιττά, μόνο μια πρακτική λύση που μπορείτε να ενσωματώσετε στο δικό σας project.

## Προαπαιτούμενα

Πριν βυθιστείτε, βεβαιωθείτε ότι έχετε:

* Java 17 (ή οποιοδήποτε πρόσφατο JDK) εγκατεστημένο.  
* Maven ή Gradle για διαχείριση εξαρτήσεων.  
* Ένα αρχείο εικόνας που περιέχει χαρακτήρες Χίντι (π.χ., `hindi-sample.png`).  
* Μια δωρεάν δοκιμή Aspose OCR for Java ή αδειοδοτημένο DLL – το API λειτουργεί με τον ίδιο τρόπο και στις δύο περιπτώσεις.

Αν κάποιο από αυτά σας φαίνεται άγνωστο, μην ανησυχείτε—θα δείξουμε ακριβώς πού ταιριάζει κάθε κομμάτι.

## Βήμα 1: Ρυθμίστε το Project σας για **Εξαγωγή κειμένου Χίντι**

Πρώτα, προσθέστε τη βιβλιοθήκη Aspose OCR στο `pom.xml`. Αυτή η μοναδική εξάρτηση σας δίνει πρόσβαση στις κλάσεις `OcrEngine`, `Image` και `Language` που χρησιμοποιούνται σε όλο το παράδειγμα.

```xml
<!-- pom.xml -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.11</version> <!-- latest as of Mar 2026 -->
    </dependency>
</dependencies>
```

> **Pro tip:** Αν χρησιμοποιείτε Gradle, το ισοδύναμο είναι `implementation 'com.aspose:aspose-ocr:23.11'`. Η ενημέρωση του αριθμού έκδοσης εξασφαλίζει ότι έχετε τα πιο πρόσφατα μοντέλα γλώσσας Χίντι.

## Βήμα 2: **Φόρτωση Image OCR** – Προετοιμασία του Αρχείου για Επεξεργασία

Τώρα ας **φορτώσουμε image ocr** δεδομένα. Η μέθοδος `Image.load` δέχεται διαδρομή αρχείου ή `InputStream`. Η χρήση σχετικής διαδρομής κρατά τον κώδικα φορητό μεταξύ περιβαλλόντων.

```java
import com.aspose.ocr.Image;

// ...

// Step 2: Load the image that contains Hindi characters
Image hindiImage = Image.load("src/main/resources/hindi-sample.png");
```

> **Why this matters:** Η σωστή φόρτωση της εικόνας είναι το θεμέλιο κάθε pipeline OCR. Αν η διαδρομή είναι λανθασμένη, η μηχανή ρίχνει `FileNotFoundException` και δεν θα φτάσετε ποτέ στο **convert image to text**.

## Βήμα 3: Διαμόρφωση της Μηχανής για **Εξαγωγή κειμένου Χίντι**

Το Aspose OCR υποστηρίζει πάνω από 100 γλώσσες. Για το Χίντι απλώς ορίζουμε τη γλώσσα σε `Language.HI`. Αυτό λέει στη μηχανή ποιο σύνολο χαρακτήρων και λεξικό να χρησιμοποιήσει κατά την αναγνώριση.

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.Language;

// ...

// Step 3: Create an instance of the OCR engine and set Hindi language
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.setLanguage(Language.HI); // equivalent to Language.fromCode("hi")
```

> **What’s the “why”**: Η καθορισμένη `Language.HI` βελτιώνει δραματικά την ακρίβεια, επειδή η μηχανή μπορεί να εφαρμόσει ειδικές για το Χίντι ευρετικές (όπως matras φωνηέντων και συνδυασμούς) αντί να μαντεύει από ένα γενικό μοντέλο Λατινικών.

## Βήμα 4: Εκτέλεση της λειτουργίας **Convert Image to Text**

Με την εικόνα φορτωμένη και τη γλώσσα ορισμένη, η πραγματική κλήση OCR είναι μια γραμμή κώδικα. Η μέθοδος `recognize` επιστρέφει το ανιχνευμένο Unicode string.

```java
// Step 4: Perform OCR on the loaded image
String recognizedText = ocrEngine.recognize(hindiImage);
```

Αν χρειαστεί να ρυθμίσετε όρια εμπιστοσύνης, η `OcrEngine` εκθέτει τη μέθοδο `setRecognitionConfidence`, αλλά οι προεπιλογές λειτουργούν καλά για τις περισσότερες καθαρές σκαναρίσματα.

## Βήμα 5: Εξαγωγή του Αποτελέσματος – **Επιτυχής Εξαγωγή κειμένου Χίντι**

Τέλος, εκτυπώστε το αναγνωρισμένο κείμενο Χίντι στην κονσόλα ή προωθήστε το σε οποιαδήποτε επόμενη διαδικασία (π.χ., αποθήκευση σε βάση δεδομένων).

```java
// Step 5: Output the extracted Hindi text
System.out.println("Hindi text:\n" + recognizedText);
```

Όταν τρέξετε το πρόγραμμα, θα πρέπει να δείτε κάτι σαν:

```
Hindi text:
नमस्ते दुनिया! यह एक परीक्षण चित्र है।
```

> **Edge case note:** Αν η έξοδος περιέχει ακατάλληλους χαρακτήρες, ελέγξτε ότι η κονσόλα σας χρησιμοποιεί κωδικοποίηση UTF‑8 (`-Dfile.encoding=UTF-8` JVM flag). Αυτό είναι ένα συχνό εμπόδιο όταν δουλεύετε με γραφήματα Devanagari.

## Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι το πλήρες αρχείο `HindiOcrDemo.java` που μπορείτε να αντιγράψετε‑και‑επικολλήσετε απευθείας στο IDE σας.

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.Image;
import com.aspose.ocr.Language;

/**
 * Java OCR example that demonstrates how to extract Hindi text from an image.
 * Make sure to place hindi-sample.png under src/main/resources before running.
 */
public class HindiOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialize OCR engine – this is where we start to extract Hindi text
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Tell the engine we want Hindi (Language.HI)
        ocrEngine.setLanguage(Language.HI); // equivalent to Language.fromCode("hi")

        // Step 3: Load the image that contains Hindi characters (load image ocr style)
        Image hindiImage = Image.load("src/main/resources/hindi-sample.png");

        // Step 4: Run the OCR – this converts image to text internally
        String recognizedText = ocrEngine.recognize(hindiImage);

        // Step 5: Show the result – the extracted Hindi text appears here
        System.out.println("Hindi text:\n" + recognizedText);
    }
}
```

> **Running the demo:**  
> 1. Αποθηκεύστε το αρχείο ως `src/main/java/HindiOcrDemo.java`.  
> 2. Τοποθετήστε το `hindi-sample.png` στο `src/main/resources`.  
> 3. Εκτελέστε `mvn compile exec:java -Dexec.mainClass=HindiOcrDemo`.  
> 4. Επαληθεύστε ότι η έξοδος της κονσόλας ταιριάζει με το κείμενο Χίντι στην εικόνα.

## Συνηθισμένα Πιθανά Προβλήματα & Πώς να τα Αποφύγετε

| Κατάσταση | Γιατί συμβαίνει | Διόρθωση |
|-----------|----------------|----------|
| **Ακατάλληλοι χαρακτήρες** | Η κονσόλα δεν χρησιμοποιεί UTF‑8. | Προσθέστε `-Dfile.encoding=UTF-8` στα JVM args ή ρυθμίστε το τερματικό του IDE σας. |
| **Δεν επιστρέφεται κείμενο** | Η εικόνα είναι πολύ θορυβώδης ή χαμηλής ανάλυσης. | Προεπεξεργαστείτε με ένα απλό βήμα δυαδικοποίησης (π.χ., OpenCV) πριν τη δώσετε στο Aspose. |
| **Εξαίρεση στο `Image.load`** | Λάθος διαδρομή αρχείου. | Χρησιμοποιήστε `Paths.get(...).toAbsolutePath()` ή τοποθετήστε την εικόνα στο φάκελο resources όπως φαίνεται. |
| **Χαμηλή ακρίβεια για Χίντι** | Η γλώσσα δεν έχει οριστεί ή χρησιμοποιείται η προεπιλογή (Λατινικά). | Πάντα καλέστε `ocrEngine.setLanguage(Language.HI)`· εξετάστε επίσης `ocrEngine.setUseDictionary(true)`. |

## Επέκταση του Demo

Τώρα που μπορείτε να **εξάγετε κείμενο Χίντι**, σκεφτείτε τα επόμενα βήματα:

* **Επεξεργασία παρτίδας** – επαναλάβετε πάνω σε φάκελο εικόνων για **load image ocr** μαζικά.  
* **Ενσωμάτωση PDF** – δώστε κάθε σελίδα ενός σαρωμένου PDF στην ίδια pipeline για **convert image to text** σε πολλαπλές σελίδες.  
* **Μετα‑επεξεργασία** – τρέξτε το αποτέλεσμα από έναν ορθογραφικό έλεγχο Χίντι για να καθαρίσετε τα OCR artefacts.  
* **Υποστήριξη πολλαπλών γλωσσών** – αλλάξτε το `Language.HI` σε `Language.EN` ή οποιονδήποτε άλλο υποστηριζόμενο κωδικό για να μετατρέψετε το παράδειγμα σε ένα γενικό **java ocr example**.

Όλα αυτά ακολουθούν το ίδιο μοτίβο: φόρτωση, διαμόρφωση, αναγνώριση και διαχείριση του αποτελέσματος.

## Συμπέρασμα

Μόλις περάσαμε από ένα απλό **java ocr example** που σας επιτρέπει να **εξάγετε κείμενο Χίντι** από οποιοδήποτε αρχείο εικόνας. Ορίζοντας τη γλώσσα σε Χίντι, φορτώνοντας σωστά την εικόνα και καλώντας `recognize`, μπορείτε να **μετατρέψετε εικόνα σε κείμενο** με λίγες μόνο γραμμές κώδικα. Το πλήρες, εκτελέσιμο απόσπασμα παραπάνω πρέπει να λειτουργεί αμέσως για τις περισσότερες περιπτώσεις, και η ενότητα συμβουλών σας βοηθά να αποφύγετε τα τυπικά εμπόδια.

Πειραματιστείτε ελεύθερα—αλλάξτε την εικόνα δείγμα, δοκιμάστε διαφορετικούς κωδικούς γλώσσας, ή συνδέστε την έξοδο με μια υπηρεσία μετάφρασης. Ο ουρανός είναι το όριο όταν συνδυάζετε το Aspose OCR με το οικοσύστημα της Java. Αν αντιμετωπίσετε δυσκολίες, αφήστε ένα σχόλιο παρακάτω ή ελέγξτε την τεκμηρίωση Aspose Java OCR για πιο προχωρημένες επιλογές διαμόρφωσης.

Καλή κωδικοποίηση και απολαύστε τη μετατροπή εκείνων των screenshots Χίντι σε αναζητήσιμο, επεξεργάσιμο κείμενο!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}