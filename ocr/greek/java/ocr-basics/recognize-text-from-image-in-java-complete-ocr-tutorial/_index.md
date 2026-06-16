---
category: general
date: 2026-04-29
description: Αναγνωρίστε κείμενο από εικόνα χρησιμοποιώντας το Aspose OCR σε Java
  – μάθετε πώς να εξάγετε κείμενο από τιμολόγιο, να φορτώσετε εικόνα για OCR και να
  κατακτήσετε ένα tutorial OCR σε Java σε λίγα λεπτά.
draft: false
keywords:
- recognize text from image
- extract text from invoice
- load image for ocr
- java ocr tutorial
language: el
og_description: Αναγνωρίστε κείμενο από εικόνα με το Aspose OCR σε Java. Αυτός ο οδηγός
  σας καθοδηγεί στην εξαγωγή κειμένου από τιμολόγιο, τη φόρτωση εικόνας για OCR και
  την ολοκλήρωση ενός οδηγού OCR σε Java.
og_title: Αναγνώριση κειμένου από εικόνα σε Java – Πλήρης οδηγός OCR
tags:
- OCR
- Java
- Aspose
title: Αναγνώριση κειμένου από εικόνα σε Java – Πλήρης Οδηγός OCR
url: /el/java/ocr-basics/recognize-text-from-image-in-java-complete-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση κειμένου από εικόνα σε Java – Πλήρες Μάθημα OCR

Έχετε χρειαστεί ποτέ να **αναγνωρίσετε κείμενο από εικόνα** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη Java θα κάνει τη βαριά δουλειά; Δεν είστε μόνοι. Πολλοί προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν προσπαθούν να εξάγουν δεδομένα από σαρωμένα τιμολόγια ή αποδείξεις.  

Σε αυτόν τον οδηγό θα σας δείξουμε, βήμα‑βήμα, πώς να **αναγνωρίσετε κείμενο από εικόνα** χρησιμοποιώντας το Aspose OCR, πώς να **εξάγετε κείμενο από τιμολόγιο** και ακριβώς πώς να **φορτώσετε εικόνα για OCR** σε ένα καθαρό **java ocr tutorial**. Στο τέλος θα έχετε ένα εκτελέσιμο πρόγραμμα που εκτυπώνει το διορθωμένο κείμενο απευθείας στην κονσόλα — χωρίς μυστήριο, χωρίς ελλείψεις.

## What You’ll Need

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τα εξής:

- **Java Development Kit (JDK) 8+** – ο κώδικας χρησιμοποιεί τυπικά Java APIs.
- **Aspose.OCR for Java** JAR (έκδοση 23.9 ή νεότερη). Κατεβάστε το από το αποθετήριο Maven της Aspose ή το ZIP από την επίσημη ιστοσελίδα.
- Μια **εικόνα τιμολογίου** (JPEG, PNG, TIFF) που θέλετε να δοκιμάσετε – ας την ονομάσουμε `invoice.jpg`.
- Το αγαπημένο σας IDE (IntelliJ, Eclipse, VS Code) – όποιο και αν είναι.

Αυτό είναι όλο. Χωρίς επιπλέον frameworks, χωρίς πολύπλοκα εργαλεία κατασκευής. Αν έχετε ήδη Maven, απλώς προσθέστε την εξάρτηση Aspose· διαφορετικά, τοποθετήστε το JAR στο classpath σας.

## Step 1 – Set Up Your Project and Import Aspose OCR

Πρώτα, δημιουργήστε ένα νέο Maven project (ή έναν απλό φάκελο αν προτιμάτε). Προσθέστε την εξάρτηση Aspose OCR στο `pom.xml`:

```xml
<!-- pom.xml -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.9</version>
        <classifier>jdk17</classifier> <!-- adjust if you use a different JDK -->
    </dependency>
</dependencies>
```

Αν δεν χρησιμοποιείτε Maven, τοποθετήστε το `aspose-ocr-23.9.jar` στον φάκελο `libs/` και προσθέστε το στο classpath κατά την μεταγλώττιση.

> **Pro tip:** Το Maven διαχειρίζεται αυτόματα τις μεταβιβαστικές εξαρτήσεις, αποφεύγοντας τα “class not found” προβλήματα αργότερα.

## Step 2 – Load Image for OCR

Τώρα που η βιβλιοθήκη είναι έτοιμη, ας **φορτώσουμε εικόνα για OCR**. Αυτό το βήμα είναι κρίσιμο επειδή η μηχανή χρειάζεται ένα ρεύμα (stream) που μπορεί να διαβάσει. Θα χρησιμοποιήσουμε το βοηθητικό `ImageStream.fromFile` της Aspose, το οποίο αφαιρεί την ανάγκη για το χαμηλού επιπέδου `FileInputStream`.

```java
import com.aspose.ocr.*;

public class SpellCheckTutorial {
    public static void main(String[] args) throws Exception {

        // Step 2: Load the image you want to process
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.jpg"));
```

> **Why this matters:** Η παροχή ενός σωστού image stream αποτρέπει σιωπηλές αποτυχίες όπου η μηχανή OCR θεωρεί ότι η εικόνα είναι κενή.

## Step 3 – Tell the Engine What Language to Expect

Η ακρίβεια του OCR βελτιώνεται δραματικά όταν ενημερώσετε τη μηχανή για τη γλώσσα του κειμένου. Για τα περισσότερα τιμολόγια, τα Αγγλικά είναι επαρκή.

```java
        // Step 3: Specify the language (English)
        ocrEngine.getLanguageSettings().setLanguage("en");
```

Αν χρειαστεί ποτέ να επεξεργαστείτε ένα πολυγλωσσικό batch, απλώς αντικαταστήστε το `"en"` με `"fr"` ή `"de"` — η Aspose υποστηρίζει πάνω από 40 γλώσσες.

## Step 4 – Turn On Spell‑Correction (the Real Magic)

Το Aspose OCR περιλαμβάνει ενσωματωμένο μοντέλο spell‑correction. Η ενεργοποίησή του βοηθά να μετατρέψετε το “AcmeCprp” σε “AcmeCorp”, κάτι ιδιαίτερα χρήσιμο για ονόματα εταιρειών στα τιμολόγια.

```java
        // Step 4: Enable spell correction
        ocrEngine.getPostProcessingSettings().setEnableSpellCorrection(true);
```

> **Edge case:** Αν τα έγγραφά σας περιέχουν πολλή εξειδικευμένη ορολογία, θα θέλετε να την προσθέσετε σε ένα προσαρμοσμένο λεξικό (επόμενο βήμα). Διαφορετικά, το προεπιλεγμένο λεξικό μπορεί να τα “διορθώσει” λανθασμένα.

## Step 5 – Add Custom Words to the Dictionary

Ας **εξάγουμε κείμενο από τιμολόγιο** που περιέχει ένα προσαρμοσμένο όνομα εταιρείας και μια ειδική ετικέτα όπως `Invoice#`. Η προσθήκη αυτών στο προσαρμοσμένο λεξικό λέει στον spell‑corrector να τα αφήσει αμετάβλητα.

```java
        // Step 5: Add custom words so the spell‑corrector knows them
        ocrEngine.getPostProcessingSettings()
                 .getCustomDictionary()
                 .add("AcmeCorp")
                 .add("Invoice#");
```

Μπορείτε να αλυσίδετε κλήσεις `.add()` όπως φαίνεται, ή να τις καλέσετε επαναλαμβανόμενα. Το λεξικό παραμένει ζωντανό για όλη τη διάρκεια του αντικειμένου `OcrEngine`, οπότε μπορείτε να προσθέσετε όσες καταχωρήσεις χρειάζεστε.

## Step 6 – Run OCR and Print the Recognized Text

Τέλος, καλέστε `recognize()` και εκτυπώστε το αποτέλεσμα. Το επιστρεφόμενο `OcrResult` περιέχει το ακατέργαστο κείμενο καθώς και βαθμολογίες εμπιστοσύνης αν τις χρειαστείτε αργότερα.

```java
        // Step 6: Perform OCR and display the spell‑corrected text
        OcrResult ocrResult = ocrEngine.recognize();
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### Expected Output

Υποθέτοντας ότι το `invoice.jpg` περιέχει τη γραμμή:

```
AcmeCorp
Invoice# 2024-04-01
Total: $1,250.00
```

Θα πρέπει να δείτε κάτι σαν:

```
=== Recognized Text ===
AcmeCorp
Invoice# 2024-04-01
Total: $1,250.00
```

Αν η spell‑correction ήταν εσφαλμένη, θα μπορούσατε να δείτε “AcmeCprp” — το προσαρμοσμένο λεξικό μας απέτρεψε αυτό.

## Full Working Example

Παρακάτω είναι ο πλήρης κώδικας, έτοιμος για αντιγραφή‑επικόλληση στο `SpellCheckTutorial.java`. Αντικαταστήστε το `"YOUR_DIRECTORY/invoice.jpg"` με την απόλυτη διαδρομή της δοκιμαστικής σας εικόνας.

```java
import com.aspose.ocr.*;

public class SpellCheckTutorial {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.jpg"));

        // Step 3: Set the language (English)
        ocrEngine.getLanguageSettings().setLanguage("en");

        // Step 4: Enable the built‑in spell correction
        ocrEngine.getPostProcessingSettings().setEnableSpellCorrection(true);

        // Step 5: Add custom dictionary entries
        ocrEngine.getPostProcessingSettings()
                 .getCustomDictionary()
                 .add("AcmeCorp")
                 .add("Invoice#");

        // Step 6: Run OCR and print the result
        OcrResult ocrResult = ocrEngine.recognize();
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Τρέξτε το με:

```bash
javac -cp "libs/*" SpellCheckTutorial.java
java -cp ".:libs/*" SpellCheckTutorial
```

Θα δείτε το καθαρισμένο κείμενο του τιμολογίου να εκτυπώνεται στην κονσόλα.

## Common Questions & Gotchas

### What if the image is blurry?

Η ακρίβεια του OCR μειώνεται όταν η πηγή εικόνας έχει χαμηλή αντίθεση ή θόρυβο. Προεπεξεργαστείτε την εικόνα με μια βιβλιοθήκη όπως η OpenCV: αυξήστε την αντίθεση, εφαρμόστε median blur ή μετατρέψτε σε ασπρόμαυρο πριν τη δώσετε στην Aspose. Η μέθοδος `setImage` δέχεται ένα `BufferedImage`, οπότε μπορείτε να το επεξεργαστείτε πρώτα.

### Can I process PDFs directly?

Ναι. Το Aspose OCR μπορεί να διαβάσει σελίδες PDF ως εικόνες εσωτερικά. Απλώς καλέστε `ocrEngine.setImage(ImageStream.fromFile("file.pdf"))`. Η μηχανή θα rasterize κάθε σελίδα και θα εκτελέσει OCR. Παρακολουθήστε την κατανάλωση μνήμης για **large PDFs**.

### How do I get confidence scores for each word?

Το `OcrResult` εκθέτει τη μέθοδο `getWords()` που επιστρέφει μια συλλογή αντικειμένων `OcrWord`. Κάθε λέξη έχει μέθοδο `getConfidence()` (0‑100). Περάστε τις σε βρόχο αν χρειάζεστε να επισημάνετε γραμμές χαμηλής εμπιστοσύνης για χειροκίνητη ανασκόπηση.

```java
for (OcrWord word : ocrResult.getWords()) {
    System.out.println(word.getText() + " – confidence: " + word.getConfidence());
}
```

### Is there a way to batch‑process many invoices?

Απόλυτα. Τυλίξτε τον κώδικα που φαίνεται παραπάνω σε έναν βρόχο `for` που διατρέχει έναν φάκελο εικόνων. Θυμηθείτε να επαναχρησιμοποιήσετε το ίδιο αντικείμενο `OcrEngine` για να αποφύγετε το κόστος επανεκκίνησης των εγγενών βιβλιοθηκών κάθε φορά.

## Pro Tips for a Smooth java ocr tutorial Experience

- **Reuse the engine**: Η δημιουργία νέου `OcrEngine` ανά αρχείο είναι δαπανηρή. Δημιουργήστε το μία φορά, αλλάξτε την εικόνα και καλέστε `recognize()` επανειλημμένα.
- **Memory management**: Μετά την επεξεργασία μιας μεγάλης εικόνας, καλέστε `ocrEngine.dispose()` ή αφήστε το αντικείμενο να βγει εκτός εμβέλειας για να ελευθερωθούν οι εγγενείς πόροι.
- **Thread safety**: Το `OcrEngine` **δεν** είναι thread‑safe. Αν χρειάζεστε παράλληλη επεξεργασία, δημιουργήστε ξεχωριστό engine ανά νήμα.
- **Custom dictionary size**: Η προσθήκη χιλιάδων καταχωρήσεων μπορεί να επιβραδύνει το spell correction. Κρατήστε το λεξικό ελαφρύ — μόνο οι όροι που εμφανίζονται πραγματικά στα τιμολόγια σας.

## Conclusion

Τώρα έχετε ένα ολοκληρωμένο, end‑to‑end **java ocr tutorial** που δείχνει πώς να **αναγνωρίσετε κείμενο από εικόνα**, **φορτώσετε εικόνα για OCR** και **εξάγετε κείμενο από τιμολόγιο**, αξιοποιώντας τις δυνατότητες spell‑correction του Aspose. Ο δείγματος κώδικας είναι έτοιμος για εκτέλεση, οι εξηγήσεις καλύπτουν το “γιατί” κάθε βήματος, και οι συμβουλές αντιμετωπίζουν κοινά προβλήματα που μπορεί να συναντήσετε.

Τι ακολουθεί; Δοκιμάστε να επεκτείνετε τη λύση:

- Parse the recognized text into structured fields (

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}