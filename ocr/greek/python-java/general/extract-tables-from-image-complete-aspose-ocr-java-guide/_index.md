---
category: general
date: 2026-05-03
description: Εξαγωγή πινάκων από εικόνα χρησιμοποιώντας το Aspose OCR Java. Μάθετε
  πώς να φορτώνετε εικόνα για OCR, να εξάγετε πίνακα από PNG, να μετατρέπετε το κείμενο
  του πίνακα εικόνας και να αναγνωρίζετε γρήγορα εικόνες αποδείξεων.
draft: false
keywords:
- extract tables from image
- extract table from png
- load image for ocr
- convert image table text
- recognize receipt image
language: el
og_description: Εξαγωγή πινάκων από εικόνα με το Aspose OCR Java. Αυτός ο οδηγός δείχνει
  πώς να φορτώσετε εικόνα για OCR, να εξάγετε πίνακα από PNG, να μετατρέψετε το κείμενο
  του πίνακα εικόνας και να αναγνωρίσετε εικόνα απόδειξης.
og_title: Εξαγωγή πινάκων από εικόνα – Οδηγός Aspose OCR Java
tags:
- Aspose OCR
- Java
- Image Processing
title: Εξαγωγή πινάκων από εικόνα – Πλήρης οδηγός Aspose OCR Java
url: /el/python-java/general/extract-tables-from-image-complete-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή πινάκων από εικόνα – Πλήρης Οδηγός Aspose OCR Java

Έχετε ποτέ χρειαστεί να **εξάγετε πίνακες από εικόνα** αρχεία αλλά αντιμετωπίζετε δυσκολίες; Ίσως έχετε μια σαρωμένη απόδειξη ή ένα φωτογραφημένο τιμολόγιο και τα δεδομένα σε μορφή πίνακα είναι κρυμμένα σε ένα PNG. Σε αυτό το σεμινάριο θα δείτε ακριβώς πώς να *φορτώσετε εικόνα για OCR*, να μετατρέψετε αυτή τη φωτογραφία σε δομημένες γραμμές και **να μετατρέψετε το κείμενο πίνακα εικόνας** σε κάτι με το οποίο μπορείτε να εργαστείτε σε Java.  

Θα περάσουμε από κάθε βήμα, από την αδειοδότηση της μηχανής Aspose OCR μέχρι την εκτύπωση κάθε κελιού των εντοπισμένων πινάκων. Στο τέλος θα μπορείτε να **αναγνωρίσετε εικόνες αποδείξεων** και να εξάγετε τους πίνακές τους χωρίς κόπο.

## Τι Θα Μάθετε

- Πώς να αρχικοποιήσετε τη μηχανή Aspose OCR και να εφαρμόσετε την άδειά σας.
- Γιατί η ενεργοποίηση της ανίχνευσης πινάκων είναι το κλειδί για **εξαγωγή πινάκων από εικόνα**.
- Ο ακριβής κώδικας που απαιτείται για **φόρτωση εικόνας για OCR** και εκτέλεση αναγνώρισης σε PNG.
- Τρόποι διαχείρισης πολλαπλών πινάκων, σαρώσεων χαμηλής ανάλυσης και κοινών παγίδων.
- Πώς να **μετατρέψετε το κείμενο πίνακα εικόνας** σε εκτυπώσιμη (ή έτοιμη για βάση δεδομένων) μορφή.

Δεν απαιτείται εξωτερική τεκμηρίωση — όλα όσα χρειάζεστε είναι εδώ.

## Προαπαιτούμενα

- Java 17 ή νεότερη (ο κώδικας χρησιμοποιεί το σύγχρονο σύστημα μονάδων).
- Ένα αρχείο άδειας Aspose OCR for Java (`Aspose.OCR.Java.lic`). Αν κάνετε μόνο πειραματισμό, ένα προσωρινό κλειδί αξιολόγησης λειτουργεί επίσης.
- Μια εικόνα PNG που περιέχει έναν καθαρό πίνακα (π.χ., `receipt_with_table.png`).  
- Maven ή Gradle για να κατεβάσετε την εξάρτηση Aspose OCR:

```xml
<!-- Maven snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

> **Pro tip:** Κρατήστε το αρχείο άδειας δίπλα στο φάκελο `src/main/resources` ώστε η διαδρομή να παραμένει σταθερή σε όλα τα περιβάλλοντα.

---

## Βήμα 1 – Αρχικοποίηση της μηχανής OCR για **εξαγωγή πινάκων από εικόνα**

Πριν η μηχανή μπορέσει να κάνει οτιδήποτε, πρέπει να γνωρίζει ότι είστε έγκυρος χρήστης.

```java
import com.aspose.ocr.*;

public class TableExtractor {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Apply your Aspose OCR license – this removes evaluation watermarks
        License license = new License();
        license.setLicense("Aspose.OCR.Java.lic");
        ocrEngine.setLicense(license);
```

*Γιατί είναι σημαντικό:* Χωρίς έγκυρη άδεια η μηχανή OCR λειτουργεί σε δοκιμαστική λειτουργία, η οποία μπορεί να περικόπτει τα αποτελέσματα ή να προσθέτει ανεπιθύμητα υδατογραφήματα — καθιστώντας την εξαγωγή πινάκων μη αξιόπιστη.

---

## Βήμα 2 – Ενεργοποίηση ανίχνευσης πινάκων (**εξαγωγή πίνακα από png**)

Η ανίχνευση πινάκων δεν είναι ενεργοποιημένη από προεπιλογή· πρέπει να ενεργοποιήσετε τη λειτουργία.

```java
        // Step 2: Turn on table detection so the engine looks for tabular structures
        ocrEngine.getConfig().setEnableTableDetection(true);
```

Η ενεργοποίηση αυτής της σημαίας λέει στο Aspose OCR να αντιμετωπίζει ομάδες ευθυγραμμισμένου κειμένου ως γραμμές και στήλες, κάτι που χρειάζεστε όταν θέλετε να **εξάγετε πίνακες από εικόνα** αρχεία που είναι PNG.

---

## Βήμα 3 – **Φόρτωση εικόνας για OCR** και **αναγνώριση εικόνας απόδειξης**

Τώρα τροφοδοτούμε πραγματικά την εικόνα στη μηχανή.

```java
        // Step 3: Load the PNG that contains the table
        // You can also use Image.fromStream(...) for in‑memory data
        Image inputImage = Image.fromFile("YOUR_DIRECTORY/receipt_with_table.png");

        // Run the recognition process – this returns an OcrResult object
        OcrResult ocrResult = ocrEngine.recognize(inputImage);
```

Αν αντιμετωπίζετε ένα σενάριο **αναγνώρισης εικόνας απόδειξης**, ίσως θελήσετε να προεπεξεργαστείτε την εικόνα (ευθυγράμμιση, αύξηση αντίθεσης). Αυτό δεν περιλαμβάνεται στον οδηγό, αλλά αξίζει να το εξερευνήσετε για θορυβώδεις σαρώσεις.

---

## Βήμα 4 – Επεξεργασία αποτελέσματος OCR και **μετατροπή κειμένου πίνακα εικόνας**

Το αντικείμενο `OcrResult` μπορεί να περιέχει έναν ή περισσότερους πίνακες. Ας τα διατρέξουμε και να εκτυπώσουμε κάθε κελί.

```java
        // Step 4: Iterate over every detected table
        if (ocrResult.getTables().isEmpty()) {
            System.out.println("No tables were detected. Try improving image quality.");
            return;
        }

        for (Table table : ocrResult.getTables()) {
            System.out.println("Table detected:");
            for (TableRow row : table.getRows()) {
                // Join each cell's text with a tab for easy copy‑paste
                String line = row.getCells()
                                 .stream()
                                 .map(Cell::getText)
                                 .reduce((a, b) -> a + "\t" + b)
                                 .orElse("");
                System.out.println(line);
            }
            System.out.println(); // Blank line between tables
        }
    }
}
```

**Τι κάνει αυτό:**  

- Ελέγχει αν βρέθηκαν πίνακες· αν όχι, προτείνει βελτίωση της ποιότητας.  
- Για κάθε πίνακα, εκτυπώνει γραμμές με κελιά χωρισμένα με tabs, κάτι που είναι βολική μορφή για εισαγωγές CSV.  
- Η κλήση `Cell::getText` είναι η καρδιά του **μετατροπής κειμένου πίνακα εικόνας** – εξάγει το ακατέργαστο κείμενο OCR από κάθε κελί.

### Αναμενόμενη Έξοδος

Υποθέτοντας ότι το `receipt_with_table.png` περιέχει έναν απλό πίνακα 3 × 2, θα δείτε κάτι όπως:

```
Table detected:
Item	Quantity
Apple	2
Banana	5
```

Αν η εικόνα έχει πολλαπλούς πίνακες, ο καθένας θα διαχωρίζεται με μια κενή γραμμή.

---

## Βήμα 5 – Επαλήθευση των εξαγόμενων πινάκων και διαχείριση ειδικών περιπτώσεων

### Συνηθισμένες παγίδες

| Πρόβλημα | Γιατί συμβαίνει | Γρήγορη διόρθωση |
|----------|----------------|-------------------|
| **Δεν εντοπίστηκαν πίνακες** | Η εικόνα είναι πολύ θολή ή χαμηλής αντίθεσης | Εφαρμόστε δυαδικοποίηση (`ImageProcessing.applyThreshold`) πριν το OCR |
| **Συγχωνευμένα κελιά** | Οι γραμμές του πίνακα είναι αχνές, το OCR τις αντιμετωπίζει ως ένα μπλοκ | Αυξήστε το `TableDetectionSensitivity` στο `ocrEngine.getConfig()` |
| **Λανθασμένη σειρά στηλών** | Καμπυλωμένη εικόνα που προκαλεί κακή ευθυγράμμιση | Χρησιμοποιήστε `ImageProcessing.deskew` ή περιστρέψτε την εικόνα κατά 90° |

### Τι να κάνετε στη συνέχεια

- **Εξαγωγή σε CSV** – αντικαταστήστε το `System.out.println(line);` με ένα `FileWriter` για να αποθηκεύσετε τα δεδομένα.  
- **Εισαγωγή σε βάση δεδομένων** – αντιστοιχίστε κάθε γραμμή σε ένα POJO και χρησιμοποιήστε JPA για την αποθήκευση.  
- **Συνδυασμός με άλλα APIs** – για επεξεργασία αποδείξεων μπορεί επίσης να εξάγετε τα σύνολα χρησιμοποιώντας κανονικές εκφράσεις στο κείμενο OCR.

---

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

```java
import com.aspose.ocr.*;

public class TableExtractor {
    public static void main(String[] args) throws Exception {

        // Initialize OCR engine and apply license
        OcrEngine ocrEngine = new OcrEngine();
        License license = new License();
        license.setLicense("Aspose.OCR.Java.lic");
        ocrEngine.setLicense(license);

        // Enable table detection – crucial for extracting tables from image
        ocrEngine.getConfig().setEnableTableDetection(true);

        // Load the PNG image (replace with your actual path)
        Image inputImage = Image.fromFile("YOUR_DIRECTORY/receipt_with_table.png");

        // Recognize the image – this step performs OCR on the whole picture
        OcrResult ocrResult = ocrEngine.recognize(inputImage);

        // Verify we have tables; otherwise suggest a quality fix
        if (ocrResult.getTables().isEmpty()) {
            System.out.println("No tables were detected. Try improving image quality.");
            return;
        }

        // Print each table row by row, converting image table text into tab‑separated values
        for (Table table : ocrResult.getTables()) {
            System.out.println("Table detected:");
            for (TableRow row : table.getRows()) {
                String line = row.getCells()
                                 .stream()
                                 .map(Cell::getText)
                                 .reduce((a, b) -> a + "\t" + b)
                                 .orElse("");
                System.out.println(line);
            }
            System.out.println(); // Blank line between tables
        }
    }
}
```

Εκτελέστε αυτό το πρόγραμμα, δείξτε το σε ένα PNG που περιέχει καθαρό πίνακα, και παρακολουθήστε την κονσόλα να γεμίζει με καλοσχηματισμένες γραμμές.

---

## Συμπέρασμα

Τώρα έχετε μια σταθερή, ολοκληρωμένη λύση για **εξαγωγή πινάκων από εικόνα** αρχεία χρησιμοποιώντας το Aspose OCR for Java. Από την αδειοδότηση μέχρι το **φόρτωση εικόνας για OCR**, την ενεργοποίηση του **εξαγωγής πίνακα από png**, και τελικά το **μετατροπή κειμένου πίνακα εικόνας**, κάθε βήμα καλύπτεται με εξηγήσεις και πρακτικές συμβουλές.  

Στη συνέχεια, δοκιμάστε να συνδέσετε την έξοδο με ένα αρχείο CSV, να σπρώξετε τις γραμμές σε μια σχεσιακή βάση δεδομένων, ή να συνδυάσετε το βήμα OCR με μια ρουτίνα εξαγωγής συνολικού ποσού από απόδειξη. Το ίδιο μοτίβο λειτουργεί για τιμολόγια, τιμοκαταλόγους και οποιοδήποτε σαρωμένο έγγραφο που κρύβει δεδομένα πίσω από ένα πλέγμα.

Έχετε ερωτήσεις σχετικά με τη διαχείριση αποδείξεων χαμηλής ανάλυσης ή την κλιμάκωση σε επεξεργασία παρτίδων; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!  

![Παράδειγμα εξαγωγής πινάκων από εικόνα](https://example.com/assets/extract-tables-from-image.png "Εξαγωγή πινάκων από εικόνα – δείγμα εξόδου")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}