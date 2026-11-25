---
category: general
date: 2026-05-06
description: Πώς να χρησιμοποιήσετε το OCR για να εξάγετε κείμενο από εικόνα σε Java.
  Μάθετε τη μετατροπή εικόνας σε κείμενο με OCR, διορθώστε τα σφάλματα OCR και φορτώστε
  εικόνα για OCR με το Aspose OCR.
draft: false
keywords:
- how to use ocr
- extract text from image
- ocr image to text
- correct ocr errors
- load image for ocr
language: el
og_description: Πώς να χρησιμοποιήσετε OCR στη Java για να εξάγετε κείμενο από εικόνα,
  να διορθώσετε σφάλματα OCR και να φορτώσετε εικόνα για OCR χρησιμοποιώντας το Aspose
  OCR.
og_title: Πώς να χρησιμοποιήσετε OCR στη Java – Πλήρης οδηγός
tags:
- OCR
- Java
- Aspose
title: Πώς να χρησιμοποιήσετε OCR στη Java – Εξαγωγή κειμένου από εικόνα με διόρθωση
  ορθογραφίας
url: /el/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε OCR σε Java – Εξαγωγή Κειμένου από Εικόνα με Διόρθωση Ορθογραφίας

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε OCR** για να μετατρέψετε μια θολή φωτογραφία από απόδειξη σε καθαρό, αναζητήσιμο κείμενο; Δεν είστε μόνοι. Σε πολλά έργα—εφαρμογές παρακολούθησης εξόδων, δίκτυα ψηφιοποίησης τιμολογίων ή ακόμη και ένα γρήγορο σενάριο λήψης σημειώσεων—η απόκτηση αξιόπιστου κειμένου από μια εικόνα είναι το πρώτο εμπόδιο.  

Αυτό το tutorial σας δείχνει ακριβώς πώς να χρησιμοποιήσετε OCR σε Java, καλύπτοντας τα πάντα από τη φόρτωση της εικόνας για OCR μέχρι τη διόρθωση σφαλμάτων OCR ώστε το αποτέλεσμα να διαβάζεται σαν να είχε πληκτρολογηθεί από άνθρωπο. Στο τέλος, θα μπορείτε να **εξάγετε κείμενο από εικόνα**, να εκτελέσετε μετατροπή **OCR εικόνα σε κείμενο** και να διορθώσετε αυτόματα κοινά λάθη αναγνώρισης.

## Τι Θα Δημιουργήσετε

Θα δημιουργήσουμε ένα μικρό πρόγραμμα κονσόλας Java που:

1. Φορτώνει ένα PNG (ή οποιαδήποτε υποστηριζόμενη μορφή) στη μηχανή Aspose OCR.  
2. Ενεργοποιεί τη ενσωματωμένη λειτουργία διόρθωσης ορθογραφίας για **διόρθωση σφαλμάτων OCR**.  
3. Τρέχει τη διαδικασία αναγνώρισης και εκτυπώνει το καθαρισμένο κείμενο.  

Χωρίς εξωτερικές υπηρεσίες, χωρίς βαριά πλαίσια—μόνο ένα JAR και μερικές γραμμές κώδικα.

### Προαπαιτούμενα

- Java Development Kit (JDK) 8 ή νεότερο.  
- Maven (ή οποιοδήποτε εργαλείο κατασκευής) για να κατεβάσετε τη βιβλιοθήκη Aspose OCR.  
- Ένα αρχείο εικόνας (π.χ., `receipt.png`) που θέλετε να αναλύσετε.  

Αν λείπει το Aspose OCR JAR, προσθέστε αυτήν την εξάρτηση στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

> **Συμβουλή:** Η δωρεάν έκδοση αξιολόγησης λειτουργεί για δοκιμές, αλλά μια άδεια αφαιρεί το υδατογράφημα αξιολόγησης.

## Βήμα 1 – Αρχικοποίηση της Μηχανής OCR (Κύρια Λέξη-Κλειδί σε Δράση)

Το πρώτο πράγμα που πρέπει να κάνετε είναι να δημιουργήσετε μια παρουσία του `OcrEngine`. Σκεφτείτε το ως τον εγκέφαλο που θα διαβάσει τα pixel και θα τα μετατρέψει σε χαρακτήρες.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this is where we start using OCR
        OcrEngine ocrEngine = new OcrEngine();
```

*Γιατί είναι σημαντικό:* Η αρχικοποίηση της μηχανής ρυθμίζει εσωτερικούς πόρους (μοντέλα γλώσσας, λεξικά κ.λπ.). Η παράλειψη αυτού του βήματος θα προκαλούσε `NullPointerException` αργότερα όταν προσπαθήσετε να φορτώσετε μια εικόνα.

## Βήμα 2 – Φόρτωση Εικόνας για OCR

Τώρα πραγματικά **φορτώνουμε εικόνα για OCR**. Η Aspose παρέχει ένα βολικό βοηθητικό `ImageStream.fromFile`, αλλά μπορείτε επίσης να δώσετε ένα `byte[]` αν προτιμάτε.

```java
        // Load the image you want to analyse – replace the path with your own file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));
```

*Συνηθισμένο λάθος:* Η διαδρομή του αρχείου πρέπει να είναι απόλυτη ή σχετική με τον τρέχοντα φάκελο εργασίας. Αν η εικόνα δεν βρεθεί, η μηχανή ρίχνει `IOException`. Ελέγξτε ξανά τη διαδρομή, ειδικά όταν τρέχετε από IDE σε σχέση με ένα πακεταρισμένο JAR.

## Βήμα 3 – Ενεργοποίηση Διόρθωσης Ορθογραφίας για **Διόρθωση Σφαλμάτων OCR**

Το έτοιμο OCR μπορεί να είναι θορυβώδες—σκεφτείτε “l0ve” αντί για “love” ή “0” αντί για “O”. Η ενεργοποίηση της διόρθωσης ορθογραφίας λέει στη μηχανή να εκτελέσει μια φάση μετα-επεξεργασίας που διορθώνει τυπικά λάθη.

```java
        // Turn on the spell‑correction feature – this helps to correct OCR errors
        ocrEngine.getSettings().setEnableSpellCorrection(true);
```

*Γιατί το θέλετε:* Χωρίς διόρθωση ορθογραφίας, ίσως χρειαστεί να καθαρίσετε χειροκίνητα την έξοδο, κάτι που αναιρεί το σκοπό του αυτοματισμού. Το ενσωματωμένο λεξικό λειτουργεί καλά για τα Αγγλικά και αρκετές άλλες γλώσσες.

## Βήμα 4 – Εκτέλεση Αναγνώρισης (**OCR Εικόνα σε Κείμενο**)

Με τη φορτωμένη εικόνα και τη διόρθωση ορθογραφίας ενεργοποιημένη, μπορούμε τελικά να ζητήσουμε από τη μηχανή να αναγνωρίσει το κείμενο.

```java
        // Run the OCR process – this converts the image to text
        OcrResult ocrResult = ocrEngine.recognize();
```

*Ακραία περίπτωση:* Αν η εικόνα έχει χαμηλή αντίθεση ή είναι πολύ κεκλιμένη, το αποτέλεσμα μπορεί ακόμα να περιέχει ακαταλαβίστικο κείμενο. Σκεφτείτε προ-επεξεργασία (π.χ., δυαδικοποίηση, διόρθωση κλίσης) πριν τη δώσετε στη μηχανή.

## Βήμα 5 – Εξαγωγή του Καθαρισμένου Κειμένου

Το τελικό βήμα είναι απλώς η εκτύπωση του αποτελέσματος. Σε μια πραγματική εφαρμογή μπορεί να το γράψετε σε βάση δεδομένων ή αρχείο, αλλά για αυτήν την επίδειξη το `System.out` αρκεί.

```java
        // Display the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

### Αναμενόμενη Έξοδος

Υποθέτοντας ότι το `receipt.png` περιέχει μια σαφή λίστα αντικειμένων, μπορεί να δείτε κάτι όπως:

```
Corrected text:
Item           Qty   Price
Apple          2     $1.20
Banana         5     $0.75
Total               $5.55
```

Παρατηρήστε πώς τα “Qty” και “Price” είναι ορθογραφημένα σωστά ακόμη και αν η αρχική σάρωση είχε ένα λανθασμένο “Qy”.

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα αρχείο με όνομα `SpellCorrectDemo.java`. Βεβαιωθείτε ότι το Aspose OCR JAR βρίσκεται στο classpath σας.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // Replace "YOUR_DIRECTORY/receipt.png" with the actual path
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));

        // Step 3: Enable spell correction to improve accuracy
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Step 4: Perform OCR recognition (OCR image to text)
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

Τρέξτε το με:

```bash
javac -cp "aspose-ocr-23.9.jar" SpellCorrectDemo.java
java -cp ".:aspose-ocr-23.9.jar" SpellCorrectDemo
```

Τώρα θα πρέπει να δείτε το καθαρισμένο κείμενο να εκτυπώνεται στην κονσόλα.

## Μπόνους: Ρύθμιση Παραμέτρων για Καλύτερη Ακρίβεια

Αν και η προεπιλεγμένη διαμόρφωση λειτουργεί για τα περισσότερα έντυπα έγγραφα, ίσως χρειαστεί να προσαρμόσετε μερικές παραμέτρους για εξειδικευμένα σενάρια:

| Ρύθμιση | Τι Κάνει | Πότε να Αλλάξει |
|---------|----------|-----------------|
| `setLanguage(OcrLanguage.English)` | Επιβάλλει το λεξικό Αγγλικών (μειώνει ψευδώς θετικά) | Εάν η εικόνα σας περιέχει μόνο κείμενο στα Αγγλικά. |
| `setResolution(300)` | Ενημερώνει τη μηχανή για το DPI της πηγαίας εικόνας | Για υψηλής ανάλυσης σάρωση. |
| `setEnableAutoSkewCorrection(true)` | Αυτόματη περιστροφή ελαφρώς κεκλιμένων σελίδων | Όταν οι εικόνες λαμβάνονται με κινητό. |

```java
ocrEngine.getSettings().setLanguage(OcrLanguage.English);
ocrEngine.getSettings().setResolution(300);
ocrEngine.getSettings().setEnableAutoSkewCorrection(true);
```

## Συχνές Ερωτήσεις

**Ε: Λειτουργεί αυτό με PDF;**  
Α: Ναι. Μετατρέψτε κάθε σελίδα PDF σε εικόνα (π.χ., χρησιμοποιώντας Aspose PDF) και δώστε την εικόνα στη μηχανή OCR.

**Ε: Τι γίνεται αν η εικόνα μου είναι σε μορφή BMP;**  
Α: Το `ImageStream.fromFile` υποστηρίζει PNG, JPEG, BMP, TIFF και GIF από προεπιλογή. Απλώς αλλάξτε την επέκταση του αρχείου.

**Ε: Μπορώ να απενεργοποιήσω τη διόρθωση ορθογραφίας;**  
Α: Απόλυτα—ορίστε `setEnableSpellCorrection(false)` αν χρειάζεστε ακατέργαστη έξοδο OCR για επεξεργασία σε επόμενο στάδιο.

## Συμπέρασμα

Τώρα ξέρετε **πώς να χρησιμοποιήσετε OCR** σε Java για **εξαγωγή κειμένου από εικόνα**, αυτόματη **διόρθωση σφαλμάτων OCR**, και σωστή **φόρτωση εικόνας για OCR** χρησιμοποιώντας Aspose OCR. Η ροή πέντε βημάτων—αρχικοποίηση, φόρτωση, ενεργοποίηση διόρθωσης ορθογραφίας, αναγνώριση και έξοδος—καλύπτει την πλειονότητα των καθημερινών εργασιών OCR.

Από εδώ, σκεφτείτε να συνδέσετε αυτή τη λογική με εγγραφή σε βάση δεδομένων, ένα REST endpoint ή έναν επεξεργαστή παρτίδας για να διαχειριστείτε δεκάδες αποδείξεις ταυτόχρονα. Πειραματιστείτε με τον παραπάνω πίνακα επιπλέον ρυθμίσεων για να εξάγετε κάθε τελευταίο χαρακτήρα ακρίβειας.

Καλό κώδικα, και εύχομαι τα αποτελέσματα OCR σας να είναι πάντα πιο καθαρά από τις αποδείξεις που λεκιάστηκαν από καφέ!

![διάγραμμα πώς να χρησιμοποιήσετε OCR που δείχνει εικόνα → μηχανή OCR → ροή διορθωμένου κειμένου]

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}