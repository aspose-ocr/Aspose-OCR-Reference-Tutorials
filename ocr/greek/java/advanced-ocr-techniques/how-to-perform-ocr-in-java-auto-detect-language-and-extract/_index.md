---
category: general
date: 2026-04-26
description: Μάθετε πώς να εκτελείτε OCR και να εξάγετε κείμενο από εικόνα χρησιμοποιώντας
  το Aspose OCR. Αυτός ο οδηγός δείχνει πώς να φορτώνετε εικόνα για OCR, να ενεργοποιείτε
  την αυτόματη ανίχνευση γλώσσας και να πραγματοποιείτε αυτόματη ανίχνευση γλώσσας
  στο OCR.
draft: false
keywords:
- how to perform OCR
- extract text from image
- load image for OCR
- enable automatic language detection
- auto detect language OCR
language: el
og_description: Πώς να εκτελέσετε OCR σε Java με το Aspose OCR. Μάθετε πώς να φορτώνετε
  εικόνα για OCR, να ενεργοποιείτε την αυτόματη ανίχνευση γλώσσας και να εξάγετε κείμενο
  από την εικόνα.
og_title: Πώς να εκτελέσετε OCR σε Java – Αυτόματη ανίχνευση γλώσσας
tags:
- OCR
- Java
- Aspose
title: Πώς να εκτελέσετε OCR σε Java – Αυτόματη ανίχνευση γλώσσας και εξαγωγή κειμένου
url: /el/java/advanced-ocr-techniques/how-to-perform-ocr-in-java-auto-detect-language-and-extract/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εκτελέσετε OCR σε Java – Αυτόματη Ανίχνευση Γλώσσας και Εξαγωγή Κειμένου

Έχετε ποτέ χρειαστεί να ξέρετε **πώς να εκτελέσετε OCR** σε μια φωτογραφία που συνδυάζει Αγγλικά, Ισπανικά και ίσως κάποια Ιαπωνικά χαρακτήρες; Δεν είστε μόνοι—οι προγραμματιστές συχνά αντιμετωπίζουν αυτό το εμπόδιο όταν οι εφαρμογές τους πρέπει να διαβάζουν κείμενο από σαρωμένα έγγραφα, αποδείξεις ή πολυγλωσσικές πινακίδες.  

Τα καλά νέα; Με λίγες γραμμές Java και Aspose OCR μπορείτε να **φορτώσετε εικόνα για OCR**, να ενεργοποιήσετε **την αυτόματη ανίχνευση γλώσσας**, και άμεσα **εξάγετε κείμενο από την εικόνα** χωρίς να μαντεύετε τη γλώσσα πρώτα. Σε αυτό το tutorial θα περάσουμε από το πλήρες, εκτελέσιμο παράδειγμα, θα εξηγήσουμε γιατί κάθε βήμα είναι σημαντικό, και θα σας δείξουμε πώς να επαληθεύσετε το αποτέλεσμα του **auto detect language OCR**.

> **Τι θα αποκομίσετε**  
> * Ένα λειτουργικό πρόγραμμα Java που διαβάζει ένα PNG με πολλαπλές γλώσσες.  
> * Γνώση των βασικών ρυθμίσεων OCR που κάνουν την ανίχνευση γλώσσας εύκολη.  
> * Συμβουλές για τη διαχείριση ελλιπών αρχείων, μη υποστηριζόμενων γλωσσών και βελτιώσεις απόδοσης.

## Προαπαιτούμενα

| Απαίτηση | Γιατί είναι σημαντικό |
|-------------|----------------|
| Java 17 (ή νεότερη) | Το Aspose OCR στοχεύει σε σύγχρονα JVM· παλαιότερες εκδόσεις μπορεί να λείπουν λειτουργίες API. |
| Βιβλιοθήκη Aspose OCR for Java (τελευταία έκδοση) | Παρέχει `OcrEngine` και δυνατότητες αυτόματης ανίχνευσης γλώσσας. |
| Αρχείο εικόνας (`mixed_lang.png`) που περιέχει κείμενο τουλάχιστον σε δύο γλώσσες | Δείχνει τη λειτουργία **auto detect language OCR**. |
| IDE Java ή απλή ρύθμιση γραμμής εντολών | Για τη μεταγλώττιση και εκτέλεση του δείγματος κώδικα. |

Αν δεν έχετε κατεβάσει ακόμη το JAR του Aspose OCR, κατεβάστε το από το επίσημο αποθετήριο Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- replace with the latest -->
</dependency>
```

## Βήμα 1: Δημιουργία του Αντικειμένου OCR Engine – Πώς να Εκτελέσετε OCR

Το πρώτο πράγμα που κάνετε όταν θέλετε να **εκτελέσετε OCR** είναι να δημιουργήσετε ένα αντικείμενο του κινητήρα. Σκεφτείτε το `OcrEngine` ως τον εγκέφαλο που θα αναλύσει το bitmap και θα μετατρέψει τα pixel σε χαρακτήρες.

```java
// Step 1: Initialize the OCR engine
import com.aspose.ocr.*;

public class AutoDetectDemo {
    public static void main(String[] args) throws Exception {

        // Create a fresh OcrEngine object – this is where the magic starts
        OcrEngine ocrEngine = new OcrEngine();
```

> **Συμβουλή επαγγελματία:** Η επαναχρησιμοποίηση του ίδιου `OcrEngine` για πολλές εικόνες μπορεί να βελτιώσει την απόδοση επειδή ο κινητήρας αποθηκεύει εσωτερικά τα μοντέλα γλώσσας.

## Βήμα 2: Ενεργοποίηση Αυτόματης Ανίχνευσης Γλώσσας – Enable Automatic Language Detection

Από προεπιλογή το Aspose OCR υποθέτει Αγγλικά. Για πολυγλωσσικές εικόνες πρέπει να του πείτε να “μαντέψει” τη γλώσσα ανά μπλοκ κειμένου. Αυτό είναι που κάνει η σημαία **enable automatic language detection**.

```java
        // Step 2: Turn on auto‑language detection for each region
        ocrEngine.getRecognitionSettings()
                 .setLanguage(OcrLanguage.AUTO_DETECT);
```

Γιατί είναι σημαντικό: Ο κινητήρας τώρα εξετάζει κάθε τμήμα της εικόνας, επιλέγει τη πιο πιθανή γλώσσα και εφαρμόζει το σωστό σύνολο χαρακτήρων. Χωρίς αυτό, θα έχετε ακατάληπτο αποτέλεσμα για τα τμήματα που δεν είναι Αγγλικά.

## Βήμα 3: Φόρτωση της Εικόνας για OCR – Load Image for OCR

Τώρα πραγματικά **φορτώνουμε εικόνα για OCR**. Η διαδρομή μπορεί να είναι απόλυτη ή σχετική· απλώς βεβαιωθείτε ότι το αρχείο υπάρχει, αλλιώς θα προκύψει `FileNotFoundException`.

```java
        // Step 3: Point the engine at the image that contains mixed‑language text
        ocrEngine.setImage("YOUR_DIRECTORY/mixed_lang.png");
```

> **Περίπτωση άκρης:** Αν η εικόνα σας βρίσκεται στο φάκελο resources ενός έργου Maven, χρησιμοποιήστε `getClass().getResource("/mixed_lang.png")` για να αποφύγετε σκληρά κωδικοποιημένες διαδρομές.

## Βήμα 4: Εκτέλεση Αναγνώρισης και Εξαγωγή Κειμένου από την Εικόνα – Extract Text from Image

Με τον κινητήρα ρυθμισμένο και την εικόνα φορτωμένη, ήρθε η ώρα να **εκτελέσετε OCR**. Η κλήση `recognize()` κάνει το βαριά έργο, ενώ το `getText()` επιστρέφει ένα απλό `String`.

```java
        // Step 4: Execute OCR and fetch the recognized text
        String recognizedText = ocrEngine.recognize().getText();
```

Σε αυτό το σημείο η βιβλιοθήκη έχει ήδη **auto detect language OCR** για κάθε μπλοκ, έτσι η μεταβλητή `recognizedText` περιέχει μια καθαρή, γλωσσικά ενημερωμένη μεταγραφή.

## Βήμα 5: Εμφάνιση του Αποτελέσματος – Verify Auto‑Detect Language OCR Output

Τέλος, εκτυπώνουμε το αποτέλεσμα στην κονσόλα. Σε μια πραγματική εφαρμογή μπορεί να το γράψετε σε αρχείο, βάση δεδομένων ή να το στείλετε σε υπηρεσία μετάφρασης.

```java
        // Step 5: Show the output – you’ll see language tags if you enable them
        System.out.println("Auto‑detected language output:\n" + recognizedText);
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Υποθέτοντας ότι το `mixed_lang.png` περιέχει “Hello” (Αγγλικά) και “¡Hola!” (Ισπανικά), θα δείτε κάτι όπως:

```
Auto‑detected language output:
Hello
¡Hola!
```

Αν ενεργοποιήσετε το `setShowLanguage(true)` στις ρυθμίσεις, ο κινητήρας προσθέτει σε κάθε γραμμή έναν κωδικό γλώσσας, π.χ., `[en] Hello` και `[es] ¡Hola!`.

## Συχνές Ερωτήσεις & Παγίδες

### Τι γίνεται αν η διαδρομή της εικόνας είναι λανθασμένη;

Ο κινητήρας ρίχνει `FileNotFoundException`. Τυλίξτε την κλήση σε μπλοκ try‑catch και δώστε στον χρήστη ένα φιλικό μήνυμα:

```java
try {
    ocrEngine.setImage("path/to/image.png");
} catch (FileNotFoundException e) {
    System.err.println("Image not found – check the file path!");
    return;
}
```

### Μπορώ να περιορίσω τις γλώσσες για να επιταχύνω την ανίχνευση;

Ναι. Αντί για `AUTO_DETECT`, μπορείτε να δώσετε μια λίστα:

```java
ocrEngine.getRecognitionSettings()
         .setLanguage(new OcrLanguage[]{OcrLanguage.ENGLISH, OcrLanguage.SPANISH});
```

Αυτό μειώνει το χώρο αναζήτησης και μπορεί να βελτιώσει την απόδοση σε μεγάλες παρτίδες.

### Πώς το **auto detect language OCR** διαχειρίζεται το χειρόγραφο κείμενο;

Το Aspose OCR εστιάζει σε τυπωμένο κείμενο. Τα χειρόγραφα σενάρια συνήθως απαιτούν διαφορετικό κινητήρα (π.χ., Aspose OCR for Handwriting). Η προσπάθεια εξαναγκασμού της ανίχνευσης θα δώσει φτωχά αποτελέσματα.

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω βρίσκεται ολόκληρο το πρόγραμμα, έτοιμο για μεταγλώττιση και εκτέλεση. Αντικαταστήστε το `YOUR_DIRECTORY` με το πραγματικό φάκελο που περιέχει το `mixed_lang.png`.

```java
import com.aspose.ocr.*;

public class AutoDetectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialize the OCR engine – this is where the magic starts
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable automatic language detection for each text block
        ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.AUTO_DETECT);

        // Step 3: Load the image that contains mixed‑language text
        // Make sure the file exists; otherwise an exception is thrown
        ocrEngine.setImage("YOUR_DIRECTORY/mixed_lang.png");

        // Step 4: Run the recognition process and obtain the extracted text
        String recognizedText = ocrEngine.recognize().getText();

        // Step 5: Display the auto‑detected language output
        System.out.println("Auto‑detected language output:\n" + recognizedText);
    }
}
```

Τρέξτε το με:

```bash
javac -cp "aspose-ocr-23.10.jar" AutoDetectDemo.java
java -cp ".:aspose-ocr-23.10.jar" AutoDetectDemo
```

Θα πρέπει να δείτε την έξοδο κονσόλας που περιγράφηκε νωρίτερα.

## Επέκταση της Λύσης

Τώρα που ξέρετε **πώς να εκτελέσετε OCR**, σκεφτείτε τα επόμενα βήματα:

* **Batch processing** – Επανάληψη σε φάκελο εικόνων, επαναχρησιμοποίηση του ίδιου αντικειμένου `OcrEngine` για ταχύτητα.  
* **Saving results** – Εγγραφή του εξαγόμενου κειμένου σε αρχεία `.txt` ή αποθήκευση σε βάση δεδομένων.  
* **Post‑processing** – Χρήση κανονικών εκφράσεων για καθαρισμό αλλαγών γραμμής ή αφαίρεση ανεπιθύμητων χαρακτήρων.  
* **Integration** – Ενσωμάτωση του αποτελέσματος σε API μετάφρασης (Google Translate, Azure Translator) για πολυγλωσσικές εφαρμογές.  

Κάθε μία από αυτές τις επεκτάσεις βασίζεται στις βασικές έννοιες που καλύψαμε: φόρτωση της εικόνας, ενεργοποίηση της ανίχνευσης γλώσσας και εξαγωγή του κειμένου.

## Συμπέρασμα

Διασχίσαμε ένα πλήρες, ολοκληρωμένο παράδειγμα που δείχνει **πώς να εκτελέσετε OCR** σε Java ενώ ανιχνεύει αυτόματα τις γλώσσες. Ακολουθώντας τα πέντε βήματα—δημιουργία του κινητήρα, ενεργοποίηση της αυτόματης ανίχνευσης γλώσσας, φόρτωση της εικόνας, εκτέλεση αναγνώρισης και εμφάνιση αποτελεσμάτων—μπορείτε αξιόπιστα **να εξάγετε κείμενο από εικόνα** αρχεία που περιέχουν πολλαπλά σενάρια.  

Θυμηθείτε, το κλειδί για ομαλό **auto detect language OCR** είναι να αφήσετε τον κινητήρα να αποφασίζει ανά μπλοκ· η εξαναγκαστική επιλογή μιας μόνο γλώσσας συχνά οδηγεί σε ακατάληπτο αποτέλεσμα. Πειραματιστείτε με διαφορετικές ποιότητες εικόνας, λίστες γλωσσών και ρυθμίσεις απόδοσης για να βελτιώσετε την εμπειρία σύμφωνα με τη συγκεκριμένη σας περίπτωση.  

Έχετε μια περίπτωση που δεν καλύπτεται εδώ; Αφήστε ένα σχόλιο και ας το επιλύσουμε μαζί. Καλό κώδικα!  

![παράδειγμα εκτέλεσης OCR](/images/ocr-demo.png "Στιγμιότυπο οθόνης που δείχνει πώς να εκτελέσετε OCR με Aspose OCR σε Java")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}