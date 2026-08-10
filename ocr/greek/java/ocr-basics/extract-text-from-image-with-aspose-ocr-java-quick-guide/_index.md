---
category: general
date: 2026-02-19
description: Εξάγετε κείμενο από εικόνα σε Java χρησιμοποιώντας το Aspose OCR. Μάθετε
  πώς να αναγνωρίζετε κείμενο από PNG, να μετατρέπετε την εικόνα σε συμβολοσειρά και
  να διαβάζετε κείμενο από σάρωση σε λίγα μόνο βήματα.
draft: false
keywords:
- extract text from image
- recognize text from png
- convert image to string
- ocr image to text
- read text from scan
language: el
og_description: Εξαγάγετε κείμενο από εικόνα γρήγορα. Αυτό το σεμινάριο δείχνει πώς
  να αναγνωρίζετε κείμενο από PNG, να μετατρέπετε την εικόνα σε συμβολοσειρά και να
  διαβάζετε κείμενο από σάρωση χρησιμοποιώντας το Aspose OCR.
og_title: Εξαγωγή κειμένου από εικόνα με Aspose OCR – Οδηγός Java
tags:
- Java
- OCR
- Aspose
title: Εξαγωγή κειμένου από εικόνα με Aspose OCR – Γρήγορος οδηγός Java
url: /el/java/ocr-basics/extract-text-from-image-with-aspose-ocr-java-quick-guide/
---

", etc.

Make sure to keep the same markdown formatting.

Let's produce the translated content.

We need to keep Greek RTL? Not needed; Greek is LTR.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Εικόνα – Πλήρες Java Tutorial

Κάποτε χρειάστηκε να **εξάγετε κείμενο από εικόνα** αλλά δεν ήξερες ποια βιβλιοθήκη να επιλέξεις; Ίσως έχεις μια σαρωμένη απόδειξη σε μορφή PNG και θέλεις το κείμενο ως απλό string για περαιτέρω επεξεργασία. Από την εμπειρία μου, η βιβλιοθήκη Aspose OCR κάνει αυτή τη δουλειά παιχνιδάκι, ειδικά όταν δουλεύεις με Java.  

Σε αυτόν τον οδηγό θα περάσουμε από όλα όσα χρειάζεται να ξέρεις: από τη ρύθμιση της εξάρτησης Aspose OCR, τη φόρτωση ενός αρχείου PNG, **αναγνώριση κειμένου από png**, μέχρι τη μετατροπή του αποτελέσματος σε ένα χρήσιμο Java `String`. Στο τέλος θα μπορείς να **μετατρέψεις εικόνα σε string**, και θα δεις επίσης πώς να **διαβάσεις κείμενο από scan** αρχεία χωρίς κόπο.

## Τι Θα Μάθεις

- Πώς να προσθέσεις το Aspose OCR σε ένα έργο Maven ή Gradle.  
- Τον ακριβή κώδικα που απαιτείται για **εξαγωγή κειμένου από εικόνα** με μία μόνο κλήση μεθόδου.  
- Γιατί η κλάση `ImageStream` είναι η προτιμώμενη μέθοδος τροφοδοσίας δεδομένων στη μηχανή.  
- Συμβουλές για διαχείριση μεγάλων σαρώσεων, πολυ‑σελίδων PDF και κοινών παγίδων.  

Δεν απαιτείται προηγούμενη εμπειρία OCR, μόνο βασική κατανόηση της Java και ένα PNG που θέλεις να επεξεργαστείς.

## Προαπαιτούμενα

| Απαίτηση | Λόγος |
|-------------|--------|
| Java 8 ή νεότερη | Το Aspose OCR στοχεύει σε Java 8+. |
| Maven ή Gradle (προαιρετικό) | Απλοποιεί τη διαχείριση εξαρτήσεων. |
| Μια εικόνα PNG (π.χ., `quick.png`) | Η πηγή που θα τρέξουμε OCR. |
| Πρόσβαση στο Internet (πρώτη εκτέλεση) | Η βιβλιοθήκη μπορεί να κατεβάσει αυτόματα πακέτα γλώσσας. |

Αν ήδη έχεις ένα IDE Java όπως IntelliJ IDEA ή Eclipse, είσαι έτοιμος να ξεκινήσεις.

---

## Βήμα 1: Ρύθμιση Aspose OCR στο Έργο Σου

### Maven

Πρόσθεσε την παρακάτω εξάρτηση στο `pom.xml` σου:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

### Gradle

```gradle
implementation 'com.aspose:aspose-ocr:23.10' // verify the latest version on Maven Central
```

> **Pro tip:** Αν χρησιμοποιείς εταιρικό proxy, βεβαιώσου ότι το Maven/Gradle μπορεί να φτάσει στο `repo.maven.apache.org`. Διαφορετικά η κατασκευή θα αποτύχει πριν γράψεις και μια γραμμή κώδικα.

---

## Βήμα 2: Φόρτωση της Εικόνας PNG

Η κλάση `ImageStream` αφαιρεί τις λεπτομέρειες του συστήματος αρχείων και λειτουργεί με streams, URLs ή byte arrays. Να πώς φορτώνεις ένα τοπικό PNG:

```java
import com.aspose.ocr.ImageStream;

// ...

// Replace the path with the location of your PNG file.
String imagePath = "YOUR_DIRECTORY/quick.png";
ImageStream image = ImageStream.fromFile(imagePath);
```

> **Why this matters:** Η χρήση του `ImageStream.fromFile` εγγυάται ότι η μηχανή OCR λαμβάνει την εικόνα σε μορφή που καταλαβαίνει πλήρως, βελτιώνοντας την ακρίβεια αναγνώρισης σε σχέση με την τροφοδοσία ακατέργαστων byte arrays.

---

## Βήμα 3: Αναγνώριση Κειμένου από PNG

Το Aspose OCR εκθέτει μια μοναδική static μέθοδο που κάνει το σκληρό έργο: `OcrEngine.recognize`. Επιστρέφει ένα απλό Java `String`, που είναι ακριβώς ό,τι χρειάζεσαι όταν θέλεις να **μετατρέψεις εικόνα σε string**.

```java
import com.aspose.ocr.OcrEngine;

// ...

String extractedText = OcrEngine.recognize(image);
```

### Τι Συμβαίνει Πίσω από τη Σκηνή;

1. **Προεπεξεργασία:** Η μηχανή διορθώνει αυτόματα την κλίση της εικόνας και κανονικοποιεί την αντίθεση.  
2. **Ανίχνευση Γλώσσας:** Αν δεν καθορίσεις γλώσσα, το Aspose προσπαθεί να τη συμπεράνει, κάτι χρήσιμο για γρήγορες σαρώσεις.  
3. **Αναγνώριση:** Ο πυρήνας OCR τρέχει ένα νευρωνικό μοντέλο εκπαιδευμένο σε εκατομμύρια χαρακτήρες.  

Επειδή όλα αυτά είναι ενσωματωμένα σε μία κλήση, δεν χρειάζεται να παίζεις με ρυθμίσεις χαμηλού επιπέδου εκτός αν έχεις πολύ εξειδικευμένη περίπτωση χρήσης.

---

## Βήμα 4: Εμφάνιση και Χρήση του Εξαγόμενου String

Τώρα που έχεις το κείμενο, μπορείς να το εκτυπώσεις, να το αποθηκεύσεις σε βάση δεδομένων ή να το δώσεις σε άλλο API. Η πιο απλή μέθοδος—απλώς `System.out.println`:

```java
public class OcrTutorial {
    public static void main(String[] args) throws Exception {
        // Load the PNG image
        ImageStream image = ImageStream.fromFile("YOUR_DIRECTORY/quick.png");

        // Recognize text from the image
        String extractedText = OcrEngine.recognize(image);

        // Display the recognized text
        System.out.println("=== OCR Result ===");
        System.out.println(extractedText);
    }
}
```

#### Αναμενόμενη Έξοδος

```
=== OCR Result ===
Hello, world!
This is a sample OCR extraction.
```

> **Note:** Η ακριβής έξοδος εξαρτάται από το περιεχόμενο του `quick.png`. Αν η εικόνα περιέχει χειρόγραφο σημείωμα, μπορεί να δεις κάποιες λανθασμένες αναγνώσεις—τίποτα που δεν μπορεί να διορθωθεί με λίγη μετα-επεξεργασία.

---

## Βήμα 5: Διαχείριση Συνηθισμένων Edge Cases

### Μεγάλες Σαρώσεις ή Πολυ‑σελίδες PDF

Αν χρειάζεται να **διαβάσεις κείμενο από scan** αρχεία που είναι μεγαλύτερα από ένα τυπικό PNG, σκέψου:

- Διαίρεση της εικόνας σε τμήματα (`ImageStream.fromRegion`).  
- Χρήση του `OcrEngine.recognizeMultiplePages` για εισόδους PDF.

### Μη‑Αγγλικές Γλώσσες

```java
OcrEngine engine = new OcrEngine();
engine.setLanguage(OcrEngine.Language.FRENCH); // or any supported language
String frenchText = engine.recognize(image);
```

### Συμβουλές Απόδοσης

- Επανάχρησε την ίδια παρουσία `OcrEngine` για πολλαπλές εικόνες ώστε να αποφύγεις επαναλαμβανόμενη αρχικοποίηση.  
- Για επεξεργασία σε παρτίδες, ενεργοποίησε πολυ‑νηματισμό αλλά περιορίστε τα νήματα στον αριθμό των πυρήνων CPU για να αποφύγεις υπερβολική χρήση μνήμης.

---

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω είναι η πλήρης, έτοιμη‑για‑εκτέλεση κλάση Java. Αντέγραψε‑επικόλλησέ το στο IDE σου, προσαρμόζοντας τη διαδρομή της εικόνας, και πάτα **Run**.

```java
import com.aspose.ocr.*;

public class OcrTutorial {
    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // Step 1: Load the image to be processed
        // -------------------------------------------------
        ImageStream image = ImageStream.fromFile("YOUR_DIRECTORY/quick.png");

        // -------------------------------------------------
        // Step 2: Recognize text from the image using Aspose OCR
        // -------------------------------------------------
        String extractedText = OcrEngine.recognize(image);

        // -------------------------------------------------
        // Step 3: Display the recognized text
        // -------------------------------------------------
        System.out.println("=== OCR Result ===");
        System.out.println(extractedText);
    }
}
```

Η εκτέλεση αυτού του προγράμματος εκτυπώνει το αποτέλεσμα OCR στην κονσόλα, μετατρέποντας αποτελεσματικά **την εικόνα σε string** σε λίγες μόνο γραμμές κώδικα.

---

## Συμπέρασμα

Τώρα ξέρεις πώς να **εξάγεις κείμενο από εικόνα** σε Java χρησιμοποιώντας το Aspose OCR. Η διαδικασία περιορίζεται σε τρία απλά βήματα: φόρτωση του PNG, κλήση του `OcrEngine.recognize`, και χρήση του προκύπτοντος string. Είτε προσπαθείς να **αναγνωρίσεις κείμενο από png**, **μετατρέψεις εικόνα σε string**, είτε απλώς **διαβάσεις κείμενο από scan** έγγραφα, αυτή η προσέγγιση σου προσφέρει μια αξιόπιστη, έτοιμη‑για‑παραγωγή λύση.

Έτοιμος για την επόμενη πρόκληση; Δοκίμασε να τροφοδοτήσεις έναν φάκελο με σαρωμένες αποδείξεις σε βρόχο, αποθήκευσε κάθε αποτέλεσμα σε CSV, ή πειραματίσου με ρυθμίσεις γλώσσας για να βελτιώσεις την ακρίβεια σε μη‑Αγγλικά κείμενα. Ο ουρανός είναι το όριο, και ο κώδικας που μόλις έγραψες είναι μια σταθερή βάση.

Καλή προγραμματιστική, και μη διστάσεις να αφήσεις ερωτήσεις στα σχόλια—θα χαρώ να βοηθήσω!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}