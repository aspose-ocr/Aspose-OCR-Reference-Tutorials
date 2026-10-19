---
category: general
date: 2026-04-29
description: Μάθετε πώς να κάνετε OCR σε αρχεία TIFF χρησιμοποιώντας τη λειτουργία
  ροής του Aspose OCR. Αυτός ο οδηγός σας δείχνει πώς να εξάγετε πλακίδια κειμένου
  από πλακιδισμένες εικόνες TIFF αποδοτικά.
draft: false
keywords:
- how to ocr tiff
- extract text tiles
language: el
og_description: πώς να κάνετε OCR σε TIFF χρησιμοποιώντας το Aspose OCR streaming.
  Κώδικας βήμα‑βήμα για την εξαγωγή πλακιδίων κειμένου από μεγάλες εικόνες TIFF.
og_title: Πώς να κάνετε OCR TIFF – Πλήρης Οδηγός Streaming
tags:
- OCR
- Java
- Aspose
- TIFF
title: πώς να κάνετε OCR σε TIFF – Ροή μεγάλων TIFF και εξαγωγή πλακιδίων κειμένου
  σε Java
url: /el/java/advanced-ocr-techniques/how-to-ocr-tiff-stream-large-tiffs-and-extract-text-tiles-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# πώς να κάνετε OCR σε TIFF – Ροή μεγάλων TIFF και εξαγωγή πλακιδίων κειμένου σε Java

Έχετε αναρωτηθεί ποτέ **πώς να κάνετε OCR σε TIFF** αρχεία που είναι πολύ μεγάλα για να φορτωθούν στη μνήμη ταυτόχρονα; Δεν είστε ο μόνος. Πολλοί προγραμματιστές συναντούν πρόβλημα όταν οι εικόνες TIFF τους χωρίζονται σε δεκάδες πλακίδια, και η συνηθισμένη κλήση `ocrEngine.recognize()` απλώς αποτυγχάνει.  

Τα καλά νέα; Η λειτουργία ροής του Aspose OCR σας επιτρέπει να τροφοδοτείτε κάθε πλακίδιο ως ξεχωριστό stream, ώστε να μπορείτε **να εξάγετε πλακίδια κειμένου** χωρίς να εξαντλήσετε τη μνήμη. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα Java, θα εξηγήσουμε γιατί κάθε γραμμή είναι σημαντική και θα επισημάνουμε τις παγίδες που πρέπει να αποφύγετε.

> **Τι θα πάρετε:** ένα εκτελέσιμο πρόγραμμα που ενώνει τα πλακίδια TIFF σε πραγματικό χρόνο, εκτυπώνει το συνδυασμένο κείμενο και σας δείχνει πώς να προσαρμόσετε τον κώδικα για άλλες γλώσσες ή μορφές εικόνας.

---

## Προαπαιτούμενα

- **Java 17** ή νεότερη (ο κώδικας χρησιμοποιεί try‑with‑resources, οπότε λειτουργεί και με JDK 8+, αλλά το JDK 17 είναι η τρέχουσα LTS).
- **Aspose.OCR for Java** βιβλιοθήκη (v23.10 ή νεότερη). Προσθέστε την μέσω Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

- Ένας φάκελος που περιέχει τα μεμονωμένα πλακίδια TIFF (π.χ., `tile_0.tif`, `tile_1.tif`, …).  
- Προαιρετικά: ένα IDE όπως IntelliJ IDEA ή VS Code – αλλά ένας απλός επεξεργαστής κειμένου αρκεί.

---

## Βήμα 1 – Προετοιμασία διαδρομών πλακιδίων (Γιατί είναι σημαντικό)

Πριν η μηχανή OCR κάνει οτιδήποτε, πρέπει να γνωρίζει πού βρίσκεται κάθε κομμάτι της εικόνας. Η σκληρή κωδικοποίηση των διαδρομών είναι αποδεκτή για μια επίδειξη, αλλά στην παραγωγή θα θέλατε πιθανώς να σαρώσετε έναν φάκελο ή να διαβάσετε ένα αρχείο manifest.

```java
// Define the absolute or relative paths to each TIFF tile
String[] tilePaths = {
    "YOUR_DIRECTORY/tile_0.tif",
    "YOUR_DIRECTORY/tile_1.tif",
    "YOUR_DIRECTORY/tile_2.tif"
};
```

> **Pro tip:** κρατήστε τα πλακίδια σε λεκτική σειρά (0, 1, 2…) επειδή η μηχανή θα συνενώσει το αναγνωρισμένο κείμενο με την ίδια ακολουθία που τροφοδοτείτε τα streams.

---

## Βήμα 2 – Ενεργοποίηση λειτουργίας ροής στην μηχανή OCR (Κύρια λέξη‑κλειδί)

Τώρα δημιουργούμε το αντικείμενο `OcrEngine` και ενεργοποιούμε τη ροή. Αυτό είναι το βασικό στοιχείο του **πώς να κάνετε OCR σε TIFF** χωρίς να φορτώσετε ολόκληρη την εικόνα στη μνήμη RAM.

```java
// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Activate streaming – essential for large or tiled TIFFs
ocrEngine.getProcessingSettings().setEnableStreaming(true);

// Set the language to English; change as needed (e.g., "fr", "de")
ocrEngine.getLanguageSettings().setLanguage("en");
```

**Γιατί ροή;**  
Όταν καλείται `setEnableStreaming(true)`, η μηχανή αντιμετωπίζει κάθε εισερχόμενο `ImageStream` ως συνέχεια του προηγούμενου. Δημιουργεί έναν εσωτερικό εικονικό καμβά, ενώνει τα πλακίδια εικονικά και εκτελεί OCR μία φορά στο τέλος. Αυτό αποτρέπει το “OutOfMemoryError” που θα συνέβαινε αν προσπαθούσατε να φορτώσετε ένα πολυ‑γιγαμπάιτ TIFF σε μία προσπάθεια.

---

## Βήμα 3 – Προσθήκη κάθε πλακιδίου ως Input Stream (Δευτερεύουσα λέξη‑κλειδί)

Ακολουθεί ο βρόχος που τροφοδοτεί κάθε πλακίδιο στη μηχανή. Το μπλοκ `try‑with‑resources` εγγυάται ότι το αρχείο κλείνει άμεσα, κάτι κρίσιμο όταν διαχειρίζεστε δεκάδες αρχεία.

```java
for (String tilePath : tilePaths) {
    try (InputStream stream = new FileInputStream(tilePath)) {
        // Wrap the raw InputStream in Aspose's ImageStream wrapper
        ocrEngine.appendImage(ImageStream.fromStream(stream));
    } catch (IOException e) {
        // If a single tile fails, we log and continue – you might want to abort instead
        System.err.println("Failed to load tile: " + tilePath);
        e.printStackTrace();
    }
}
```

Παρατηρήστε ότι η φράση **extract text tiles** είναι ενσωματωμένη φυσικά: κάθε επανάληψη *εξάγει* το κείμενο από ένα πλακίδιο και το προσθέτει στο αυξανόμενο σύνολο αποτελεσμάτων.

---

## Βήμα 4 – Εκτέλεση αναγνώρισης και έξοδος του συνενωμένου κειμένου (Κύρια λέξη‑κλειδί)

Αφού όλα τα πλακίδια έχουν προστεθεί στη σειρά, μία κλήση εκτελεί OCR στην εικονική εικόνα. Το αποτέλεσμα περιέχει το πλήρες κείμενο, όπως αν είχατε ένα ενιαίο τεράστιο TIFF.

```java
// Perform OCR on the combined virtual image
OcrResult ocrResult = ocrEngine.recognize();

// Print the extracted text to the console
System.out.println("=== OCR Output ===");
System.out.println(ocrResult.getText());
```

**Αναμενόμενη έξοδος** (υποθέτοντας ότι τα πλακίδια περιέχουν τη φράση “Hello World” κατανεμημένη μεταξύ τους):

```
=== OCR Output ===
Hello World
```

Αν τα πλακίδια σας περιέχουν περισσότερες γραμμές, θα εμφανιστούν με την ίδια σειρά που τα παραθέσατε. Μπορείτε επίσης να γράψετε `ocrResult.getText()` σε αρχείο για επόμενη επεξεργασία.

---

## Βήμα 5 – Πλήρες, εκτελέσιμο παράδειγμα (Όλα τα βήματα σε ένα μέρος)

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε στο `StreamingExample.java`. Περιλαμβάνει όλες τις εισαγωγές, σχόλια και διαχείριση σφαλμάτων.

```java
import com.aspose.ocr.*;
import java.io.*;

public class StreamingExample {
    public static void main(String[] args) throws Exception {
        // ------------------------------------------------------------
        // Step 1: List the TIFF tile files
        // ------------------------------------------------------------
        String[] tilePaths = {
            "YOUR_DIRECTORY/tile_0.tif",
            "YOUR_DIRECTORY/tile_1.tif",
            "YOUR_DIRECTORY/tile_2.tif"
        };

        // ------------------------------------------------------------
        // Step 2: Set up the OCR engine in streaming mode
        // ------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getProcessingSettings().setEnableStreaming(true);
        ocrEngine.getLanguageSettings().setLanguage("en");

        // ------------------------------------------------------------
        // Step 3: Feed each tile as a separate stream
        // ------------------------------------------------------------
        for (String tilePath : tilePaths) {
            try (InputStream stream = new FileInputStream(tilePath)) {
                ocrEngine.appendImage(ImageStream.fromStream(stream));
            } catch (IOException e) {
                System.err.println("Unable to read tile: " + tilePath);
                e.printStackTrace();
                // Optionally: return; // abort on missing tile
            }
        }

        // ------------------------------------------------------------
        // Step 4: Recognize the combined image and display the text
        // ------------------------------------------------------------
        OcrResult ocrResult = ocrEngine.recognize();
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
    }
}
```

Αποθηκεύστε, μεταγλωττίστε και τρέξτε:

```bash
javac -cp "path/to/aspose-ocr.jar" StreamingExample.java
java -cp ".:path/to/aspose-ocr.jar" StreamingExample
```

Θα πρέπει να δείτε το συνενωμένο κείμενο OCR να εκτυπώνεται στην κονσόλα.

---

## Προχωρημένες συμβουλές & Συνηθισμένες παγίδες (Γιατί λειτουργεί)

| Πρόβλημα | Γιατί συμβαίνει | Πώς να διορθώσετε / βελτιστοποιήσετε |
|----------|------------------|--------------------------------------|
| **Σφάλματα Out‑of‑memory** | Η φόρτωση ενός πλήρους TIFF σε `BufferedImage` καταναλώνει όλη τη μνήμη heap. | Χρησιμοποιήστε λειτουργία ροής (`setEnableStreaming(true)`) – η μηχανή δεν υλοποιεί ποτέ ολόκληρη την εικόνα. |
| **Ασυμφωνία σειράς πλακιδίων** | Τα αρχεία ταξινομούνται αλφαβητικά αντί αριθμητικά (π.χ., `tile_10.tif` πριν από `tile_2.tif`). | Προσθέστε μηδενικά στην αρχή των αριθμών (`tile_00.tif`, `tile_01.tif`) ή ταξινομήστε προγραμματιστικά με `Comparator`. |
| **Λάθος γλώσσα** | Το OCR προεπιλογή είναι Αγγλικά· το κείμενο σε άλλες γλώσσες εμφανίζεται αλλοιωμένο. | Καλέστε `ocrEngine.getLanguageSettings().setLanguage("fr")` (ή οποιονδήποτε υποστηριζόμενο κωδικό ISO). |
| **Μερικές αποτυχίες** | Ένα κατεστραμμένο πλακίδιο σταματά όλη τη διαδικασία. | Πιάστε `IOException` ανά πλακίδιο, καταγράψτε το και αποφασίστε αν θα συνεχίσετε ή θα τερματίσετε. |
| **Σ bottleneck απόδοσης** | Η ανάγνωση πολλών μικρών αρχείων κυριαρχείται από I/O δίσκου. | Συμπιέστε τα πλακίδια σε ZIP και κάντε ροή από τη μνήμη, ή χρησιμοποιήστε SSD υψηλής ταχύτητας. |

---

## Πότε να χρησιμοποιήσετε ροή vs. OCR σε μονή εικόνα

- **Ροή** είναι ιδανική για:
  - Πολυ‑σελίδες TIFF ή σαρώσεις gigapixel.
  - Καταστάσεις όπου η μνήμη είναι περιορισμένη (π.χ., Docker containers, κινητές συσκευές).
  - Συστήματα που ήδη λαμβάνουν τμήματα εικόνας (π.χ., ροές κάμερας).

- **OCR σε μονή εικόνα** λειτουργεί καλά για:
  - Μικρά αρχεία PNG/JPEG (< 5 MB).
  - Μοναδικές σαρώσεις όπου η απλότητα υπερισχύει της απόδοσης.

---

## Συμπέρασμα

Τώρα έχετε μια σταθερή κατανόηση του **πώς να κάνετε OCR σε TIFF** χρησιμοποιώντας τις δυνατότητες ροής του Aspose OCR, και ξέρετε πώς να **εξάγετε πλακίδια κειμένου** αποδοτικά. Η πλήρης λύση—αρχικοποίηση της μηχανής, ενεργοποίηση ροής, προσθήκη κάθε πλακιδίου και τελική αναγνώριση του εικονικού καμβά—καλύπτει το “τι”, το “γιατί” και το “πώς” που χρειάζεστε για κώδικα έτοιμο για παραγωγή.

Τι θα κάνετε στη συνέχεια; Δοκιμάστε να αντικαταστήσετε το `"en"` με άλλη γλώσσα ή πειραματιστείτε με διαφορετικές μορφές εικόνας (`.png`, `.jpg`). Μπορείτε επίσης να στέλνετε το αποτέλεσμα OCR κατευθείαν σε ευρετήριο αναζήτησης ή σε δημιουργό PDF. Το μοτίβο παραμένει το ίδιο: ροή, σύνδεση, αναγνώριση.

Έχετε ερωτήσεις σχετικά με την κλιμάκωση σε εκατοντάδες πλακίδια ή χρειάζεστε βοήθεια με τη διαχείριση σφαλμάτων; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική δουλειά!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}