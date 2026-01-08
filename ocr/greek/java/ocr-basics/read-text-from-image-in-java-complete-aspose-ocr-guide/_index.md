---
category: general
date: 2026-01-07
description: Μάθετε πώς να διαβάζετε κείμενο από εικόνα και να μετατρέπετε την εικόνα
  σε κείμενο σε Java. Αυτό το βήμα‑βήμα tutorial OCR σε Java δείχνει επίσης πώς να
  αναγνωρίζετε κείμενο από φωτογραφία και να εκτελείτε OCR σε PNG.
draft: false
keywords:
- read text from image
- convert image to text
- recognize text from picture
- perform ocr on png
- java ocr tutorial
language: el
og_description: Διαβάστε κείμενο από εικόνα χρησιμοποιώντας το Aspose OCR σε Java.
  Αυτός ο οδηγός σας καθοδηγεί στη μετατροπή εικόνας σε κείμενο, στην αναγνώριση κειμένου
  από εικόνα και στην εκτέλεση OCR σε PNG.
og_title: Ανάγνωση κειμένου από εικόνα σε Java – Πλήρες σεμινάριο Aspose OCR
tags:
- OCR
- Java
- Aspose
title: Ανάγνωση κειμένου από εικόνα σε Java – Πλήρης οδηγός Aspose OCR
url: /el/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ανάγνωση Κειμένου από Εικόνα σε Java – Πλήρης Οδηγός Aspose OCR

Έχετε ποτέ χρειαστεί να **read text from image** αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είστε μόνοι—οι προγραμματιστές συχνά ρωτούν: «Πώς μπορώ να **convert image to text** χωρίς να τσακώνομαι;» Τα καλά νέα είναι ότι με το Aspose OCR for Java μπορείτε να το κάνετε με λίγες γραμμές κώδικα. Σε αυτό το **java ocr tutorial** θα περάσουμε από όλη τη διαδικασία, από τη φόρτωση ενός αρχείου PNG μέχρι την απόκτηση καθαρού, ελεγμένου ορθογραφικά αποτελέσματος.

Θα καλύψουμε επίσης μερικά σενάρια «τι γίνεται αν», όπως η διαχείριση διαφορετικών μορφών εικόνας ή η ρύθμιση της μηχανής για ταχύτητα. Στο τέλος θα μπορείτε να **recognize text from picture** αρχεία, **perform OCR on PNG** πόρους, και να ενσωματώσετε τη λύση σε οποιοδήποτε έργο Java. Χωρίς εξωτερικές υπηρεσίες, μόνο ένα JAR και ένα σαφές, εκτελέσιμο παράδειγμα.

## Προαπαιτούμενα

- Εγκατεστημένο Java 8 ή νεότερο (ο κώδικας χρησιμοποιεί τα τυπικά πακέτα `java.io` και `java.nio`).  
- Ένα IDE ή κειμενογράφο της επιλογής σας (IntelliJ IDEA, Eclipse, VS Code—οποιοδήποτε λειτουργεί).  
- Η βιβλιοθήκη Aspose OCR for Java (κατεβάστε το τελευταίο JAR από την ιστοσελίδα Aspose ή προσθέστε το μέσω Maven/Gradle).  
- Ένα δείγμα εικόνας, π.χ., `english-text.png`, τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε.

> **Pro tip:** Αν χρησιμοποιείτε Maven, προσθέστε την εξάρτηση `<groupId>com.aspose</groupId><artifactId>aspose-ocr</artifactId>` με την κατάλληλη έκδοση. Σας εξοικονομεί το χειροκίνητο χειρισμό των αρχείων JAR.

## Πώς να Διαβάσετε Κείμενο από Εικόνα σε Java

Παρακάτω βρίσκεται το πλήρες, αυτόνομο πρόγραμμα που **reads text from image** και εκτυπώνει το διορθωμένο αποτέλεσμα στην κονσόλα. Μπορείτε ελεύθερα να το αντιγράψετε σε μια νέα κλάση με όνομα `SpellCorrectTutorial`.

```java
import com.aspose.ocr.*;

public class SpellCorrectTutorial {

    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance and point it at your image file
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/english-text.png"));

        // Step 2: Turn on the built‑in spell‑correction feature (optional but handy)
        ocrEngine.getEngineOptions().setEnableSpellCorrection(true);

        // Step 3: Run the OCR process – this is where we actually **read text from image**
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 4: Output the corrected text; you now have **converted image to text**
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

### Τι κάνει ο κώδικας, βήμα προς βήμα

| Βήμα | Γιατί είναι σημαντικό | Κύριο συμπέρασμα |
|------|------------------------|-------------------|
| **Create OcrEngine** | Δημιουργεί τη βασική μηχανή που γνωρίζει πώς να αναλύει δεδομένα raster. | Χρειάζεστε μια μηχανή πριν μπορέσετε να **recognize text from picture** αρχεία. |
| **setImage** | Φορτώνει το PNG (ή οποιαδήποτε υποστηριζόμενη μορφή) στη μνήμη. | Αυτό είναι το σημείο όπου **perform OCR on PNG** πόρους. |
| **Enable spell correction** | Βελτιώνει την ακρίβεια για αγγλικό κείμενο διορθώνοντας κοινά τυπογραφικά λάθη. | Προαιρετικό, αλλά συχνά δίνει πιο καθαρά αποτελέσματα όταν **convert image to text**. |
| **recognize()** | Εκτελεί τον απαιτητικό αλγόριθμο που εξάγει χαρακτήρες. | Η καρδιά του **java ocr tutorial** – στην πραγματικότητα **reads text from image**. |
| **Print result** | Αποστέλλει το τελικό string στο `System.out`. | Τώρα έχετε μια αναπαράσταση απλού κειμένου που μπορείτε να αποθηκεύσετε, αναζητήσετε ή εμφανίσετε. |

> **Common question:** *Τι γίνεται αν η εικόνα μου δεν είναι PNG;*  
> Το Aspose OCR υποστηρίζει JPEG, BMP, TIFF, και ακόμη και PDF πολλαπλών σελίδων. Απλώς αλλάξτε την επέκταση αρχείου στο `fromFile(...)` και η μηχανή θα διαχειριστεί το υπόλοιπο.

## Μετατροπή Εικόνας σε Κείμενο – Προχωρημένες Επιλογές

Αν χρειάζεστε περισσότερο έλεγχο, η κλάση `EngineOptions` σας επιτρέπει να ρυθμίσετε μια σειρά παραμέτρων:

```java
ocrEngine.getEngineOptions().setLanguage(OcrLanguage.ENGLISH);
ocrEngine.getEngineOptions().setResolution(300); // DPI for better accuracy
ocrEngine.getEngineOptions().setDetectWhiteSpace(true);
```

Αυτές οι ρυθμίσεις είναι χρήσιμες όταν **recognize text from picture** αρχεία είναι χαμηλής ανάλυσης ή περιέχουν πολλές γλώσσες. Η ρύθμιση του DPI, για παράδειγμα, μπορεί να κάνει αξιοσημείωτη διαφορά όταν **perform OCR on PNG** εικόνες που λήφθηκαν από τη φωτογραφική μηχανή του τηλεφώνου.

## Επαλήθευση του Αποτελέσματος

Όταν εκτελέσετε το πρόγραμμα, θα πρέπει να δείτε κάτι όπως:

```
Corrected text:
The quick brown fox jumps over the lazy dog.
```

Αν το αποτέλεσμα φαίνεται χαοτικό, ελέγξτε ξανά:

1. Η διαδρομή της εικόνας είναι σωστή (`YOUR_DIRECTORY` πρέπει να είναι απόλυτη ή σχετική διαδρομή).  
2. Η εικόνα είναι καθαρή—υψηλή αντίθεση και ευανάγνωστοι χαρακτήρες βελτιώνουν την ποιότητα του OCR.  
3. Αν χρειάζεται η διόρθωση ορθογραφίας· μερικές φορές η απενεργοποίηση της δίνει πιο πιστή μεταγραφή.

## Συχνά Ζητούμενες Παραλλαγές

### 1. Ανάγνωση Κειμένου από Σελίδα PDF

```java
ocrEngine.setImage(ImageStream.fromFile("sample.pdf"));
```

Το Aspose OCR αντιμετωπίζει κάθε σελίδα ως εικόνα εσωτερικά, έτσι η ίδια λογική **read text from image** ισχύει.

### 2. Εξαγωγή Κειμένου από Πολλαπλά Αρχεία

```java
String[] files = {"page1.png", "page2.png", "page3.png"};
for (String file : files) {
    ocrEngine.setImage(ImageStream.fromFile(file));
    OcrResult result = ocrEngine.recognize();
    System.out.println("File: " + file);
    System.out.println(result.getText());
}
```

Η επανάληψη σας επιτρέπει να **convert image to text** σε λειτουργία δέσμης—χρήσιμο για έργα ψηφιοποίησης εγγράφων.

### 3. Αποθήκευση Αποτελεσμάτων σε Αρχείο Κειμένου

```java
java.nio.file.Files.write(
    java.nio.file.Paths.get("output.txt"),
    ocrResult.getText().getBytes(),
    java.nio.file.StandardOpenOption.CREATE);
```

Τώρα δεν έχετε μόνο **read text from image**, αλλά το έχετε επίσης αποθηκεύσει για μεταγενέστερη ανάλυση.

## Πλήρες Παράδειγμα Εργασίας (Όλα τα Βήματα Συνδυασμένα)

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που περιλαμβάνει προαιρετικές ρυθμίσεις, επεξεργασία δέσμης και έξοδο σε αρχείο. Είναι ένα έτοιμο προς εκτέλεση απόσπασμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Java.

```java
import com.aspose.ocr.*;
import java.nio.file.*;

public class FullOcrDemo {

    public static void main(String[] args) throws Exception {
        // Configure engine once
        OcrEngine engine = new OcrEngine();
        engine.getEngineOptions().setEnableSpellCorrection(true);
        engine.getEngineOptions().setLanguage(OcrLanguage.ENGLISH);
        engine.getEngineOptions().setResolution(300);

        // Files to process – you can add as many as you like
        String[] imageFiles = {
            "YOUR_DIRECTORY/english-text.png",
            "YOUR_DIRECTORY/second-image.png"
        };

        StringBuilder allText = new StringBuilder();

        for (String imgPath : imageFiles) {
            engine.setImage(ImageStream.fromFile(imgPath));
            OcrResult result = engine.recognize();

            System.out.println("=== Result for " + imgPath + " ===");
            System.out.println(result.getText());
            System.out.println();

            allText.append(result.getText()).append(System.lineSeparator());
        }

        // Save combined output
        Path outPath = Paths.get("YOUR_DIRECTORY/ocr-output.txt");
        Files.write(outPath, allText.toString().getBytes(),
                    StandardOpenOption.CREATE, StandardOpenOption.TRUNCATE_EXISTING);

        System.out.println("All OCR results saved to " + outPath.toAbsolutePath());
    }
}
```

Η εκτέλεση αυτού θα **recognize text from picture** αρχεία, **convert image to text**, και τελικά **perform OCR on PNG** (ή οποιαδήποτε υποστηριζόμενη μορφή) γράφοντας τα πάντα στο `ocr-output.txt`.

![ανάγνωση κειμένου από εικόνα χρησιμοποιώντας Aspose OCR](https://example.com/placeholder-image.png "ανάγνωση κειμένου από εικόνα χρησιμοποιώντας Aspose OCR")

*Η παραπάνω εικόνα απλώς εικονογραφεί την ιδέα της εξαγωγής κειμένου από μια εικόνα· η πραγματική εργασία OCR γίνεται στον κώδικα.*

## Συμπέρασμα

Καλύψαμε όλα όσα χρειάζεστε για να **read text from image** χρησιμοποιώντας Aspose OCR σε Java. Από το βασικό παράδειγμα ενός αρχείου μέχρι την επεξεργασία δέσμης και την έξοδο σε αρχείο, έχετε τώρα ένα σταθερό **java ocr tutorial** που μπορείτε να προσαρμόσετε σε οποιοδήποτε έργο.

- Επιλέξτε τη σωστή ανάλυση και τις ρυθμίσεις γλώσσας για τη μέγιστη ακρίβεια.  
- Η διόρθωση ορθογραφίας είναι προαιρετική αλλά συχνά δίνει πιο καθαρά αποτελέσματα όταν **convert image to text**.  
- Η ίδια ροή εργασίας λειτουργεί για JPEG, BMP, TIFF, και ακόμη και αρχεία PDF—απλώς αλλάξτε την επέκταση του αρχείου.

Τι ακολουθεί; Δοκιμάστε να τροφοδοτήσετε το αποτέλεσμα του OCR σε ευρετήριο αναζήτησης, σε API μετάφρασης ή σε ταξινομητή φυσικής γλώσσας. Οι δυνατότητες είναι ατελείωτες, και έχετε τη βάση για να χτίσετε πάνω σε αυτήν.

Έχετε ερωτήσεις, σενάρια άκρων ή συμβουλές να μοιραστείτε; Αφήστε ένα σχόλιο παρακάτω—ας συνεχίσουμε τη συζήτηση. Καλό προγραμματισμό!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}