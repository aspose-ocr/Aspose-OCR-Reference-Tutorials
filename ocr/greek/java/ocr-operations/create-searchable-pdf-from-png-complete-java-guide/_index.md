---
category: general
date: 2026-01-07
description: Δημιουργήστε PDF με δυνατότητα αναζήτησης από μια εικόνα σε Java. Μάθετε
  πώς να μετατρέψετε την εικόνα σε PDF, να εξάγετε κείμενο από την εικόνα και να αναγνωρίσετε
  κείμενο από PNG χρησιμοποιώντας το Aspose OCR.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- image to searchable pdf
- recognize text from png
language: el
og_description: Δημιουργήστε αναζητήσιμο PDF σε Java με Aspose OCR. Αυτός ο οδηγός
  δείχνει πώς να μετατρέψετε εικόνα σε PDF, να εξάγετε κείμενο από εικόνα και να αναγνωρίσετε
  κείμενο από PNG.
og_title: Δημιουργία Αναζητήσιμου PDF από PNG – Μαθήματα Java
tags:
- OCR
- Java
- PDF
title: Δημιουργία PDF με δυνατότητα αναζήτησης από PNG – Πλήρης οδηγός Java
url: /el/java/ocr-operations/create-searchable-pdf-from-png-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Αναζητήσιμου PDF από PNG – Πλήρης Οδηγός Java

Κάποτε χρειάστηκε να **δημιουργήσετε αναζητήσιμο pdf** από μια σαρωμένη εικόνα αλλά δεν ήξερατε από πού να ξεκινήσετε; Δεν είστε οι μόνοι—οι προγραμματιστές συχνά αντιμετωπίζουν αυτό το εμπόδιο όταν χτίζουν pipelines διαχείρισης εγγράφων. Τα καλά νέα; Με λίγες γραμμές Java και Aspose OCR μπορείτε να **μετατρέψετε εικόνα σε pdf**, να ενσωματώσετε κρυφό κείμενο και να καταλήξετε με ένα τέλεια αναζητήσιμο έγγραφο.

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία: φόρτωση ενός PNG, εκτέλεση OCR και αποθήκευση του αποτελέσματος ως αναζητήσιμο PDF. Στο τέλος θα μπορείτε να **εξάγετε κείμενο από εικόνα** αρχεία, να τα μετατρέψετε σε **εικόνα σε αναζητήσιμο pdf** και ακόμη να διαχειριστείτε ειδικές περιπτώσεις όπως πολυ-σελίδες TIFF. Χωρίς εξωτερικές υπηρεσίες, μόνο καθαρός κώδικας Java που μπορείτε να τρέξετε σήμερα.

## Δημιουργία Αναζητήσιμου PDF – Επισκόπηση

Πριν βουτήξουμε στον κώδικα, ας διευκρινίσουμε τι σημαίνει «αναζητήσιμο PDF». Ένα αναζητήσιμο PDF περιέχει δύο στρώματα:

1. **Ορατό στρώμα εικόνας** – η αρχική φωτογραφία (το PNG, JPEG κ.λπ.).
2. **Κρυφό στρώμα κειμένου** – κείμενο που δημιουργήθηκε από OCR και βρίσκεται πίσω από την εικόνα, καθιστώντας το έγγραφο αναζητήσιμο σε οποιονδήποτε προβολέα PDF.

Γιατί χρειάζονται και τα δύο; Η εικόνα διατηρεί την αρχική εμφάνιση, ενώ το στρώμα κειμένου επιτρέπει αντιγραφή‑επικόλληση, ευρετηρίαση και πλήρη αναζήτηση κειμένου. Αυτό είναι το ιδανικό για αρχειοθέτηση, νομική συμμόρφωση και δημιουργία αναζητήσιμων αρχείων.

## Βήμα 1: Ρύθμιση Aspose OCR στο Java Project σας

Πρώτα απ’ όλα—χρειάζεστε τη βιβλιοθήκη Aspose OCR. Ο πιο απλός τρόπος είναι να προσθέσετε την εξάρτηση Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

Αν δεν χρησιμοποιείτε Maven, κατεβάστε το JAR από την ιστοσελίδα της Aspose και προσθέστε το στο classpath. **Συμβουλή:** κρατήστε την έκδοση της βιβλιοθήκης συγχρονισμένη με το Java runtime σας (Java 8+ λειτουργεί άψογα).

### Γιατί είναι σημαντικό
Aspose OCR υποστηρίζει ευρύ φάσμα μορφών εικόνας και γλωσσών «από το κουτί», έτσι δεν χρειάζεται να γράψετε δικό σας κώδικα επεξεργασίας pixel. Επιπλέον παρέχει το enum `OcrOutputFormat.PDF` που θα χρησιμοποιήσουμε αργότερα για τη δημιουργία του αναζητήσιμου PDF.

## Βήμα 2: Φόρτωση της Εικόνας που Θέλετε να Επεξεργαστείτε

Στη συνέχεια, πρέπει να πείτε στη μηχανή OCR ποιο αρχείο θα διαβάσει. Το API δέχεται ένα `ImageStream`, το οποίο μπορεί να δημιουργηθεί από διαδρομή αρχείου, `java.io.InputStream` ή ακόμη και από πίνακα byte.

```java
import com.aspose.ocr.*;

public class PdfOutputExample {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the PNG (or any supported image) from disk
        String inputPath = "YOUR_DIRECTORY/input.png"; // replace with your actual path
        ocrEngine.setImage(ImageStream.fromFile(inputPath));
```

Παρατηρήστε ότι χρησιμοποιούμε `ImageStream.fromFile`. Αν ποτέ χρειαστεί να **μετατρέψετε εικόνα σε pdf** από stream (π.χ. ένα ανεβασμένο αρχείο), μπορείτε να αντικαταστήσετε αυτήν την κλήση με `ImageStream.fromInputStream(yourInputStream)`.

### Προειδοποίηση για ειδικές περιπτώσεις
Αν η εικόνα σας είναι μεγαλύτερη από 10 MB, σκεφτείτε να τη μειώσετε πρώτα. Οι μεγάλες εικόνες αυξάνουν δραματικά το χρόνο OCR και μπορεί να προκαλέσουν σφάλματα out‑of‑memory σε μικρούς διακομιστές.

## Βήμα 3: Εκτέλεση OCR και Λήψη του Αποτελέσματος

Τώρα συμβαίνει η μαγεία. Η κλήση `recognize()` εκτελεί τον αλγόριθμο OCR και επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει τόσο το αναγνωρισμένο κείμενο όσο και πληροφορίες διάταξης.

```java
        // Perform OCR recognition
        OcrResult ocrResult = ocrEngine.recognize();

        // Optional: print extracted text to console (useful for debugging)
        System.out.println("Extracted Text:");
        System.out.println(ocrResult.getText());
```

Εδώ **εξάγουμε κείμενο από εικόνα** και το εκτυπώνουμε. Αυτό το βήμα είναι χρήσιμο όταν χρειάζεστε μόνο το ακατέργαστο κείμενο χωρίς να δημιουργήσετε PDF. Το ίδιο αντικείμενο `ocrResult` θα επαναχρησιμοποιηθεί αργότερα για τη δημιουργία του αναζητήσιμου PDF.

### Γιατί είναι κρίσιμο αυτό το βήμα
Η μηχανή OCR όχι μόνο διαβάζει χαρακτήρες, αλλά και διατηρεί τις θέσεις τους, κάτι που καθιστά δυνατή τη δημιουργία του κρυφού στρώματος κειμένου στο τελικό PDF. Αν παραλείψετε αυτό το βήμα, θα χάσετε τη δυνατότητα αναζήτησης.

## Βήμα 4: Αποθήκευση του Αποτελέσματος ως Αναζητήσιμο PDF

Τέλος, λέμε στο Aspose OCR να γράψει το αποτέλεσμα σε μορφή PDF. Η μέθοδος `save` δέχεται το όνομα του αρχείου προορισμού και ένα enum `OcrOutputFormat`.

```java
        // Save the OCR result as a searchable PDF (image + hidden text layer)
        String outputPath = "YOUR_DIRECTORY/output.pdf"; // replace with your desired output
        ocrResult.save(outputPath, OcrOutputFormat.PDF);

        System.out.println("Searchable PDF created at: " + outputPath);
    }
}
```

Όταν ανοίξετε το `output.pdf` σε Adobe Reader ή οποιονδήποτε σύγχρονο προβολέα PDF, θα δείτε το αρχικό PNG, αλλά θα μπορείτε επίσης να αναζητήσετε οποιαδήποτε λέξη εμφανίζεται στην εικόνα. Αυτή είναι η ουσία του **create searchable pdf**.

### Παραλλαγές που μπορεί να χρειαστείτε
- **Πολλές σελίδες:** Αν έχετε πολυ‑σελίδα TIFF, απλώς κάντε βρόχο σε κάθε σελίδα, καλέστε `ocrEngine.setImage` για κάθε μία και προσθέστε τα αποτελέσματα στο ίδιο `OcrResult` πριν αποθηκεύσετε.
- **Διάφορες γλώσσες:** Χρησιμοποιήστε `ocrEngine.getLanguage().setLanguage(OcrLanguage.FRENCH);` (ή οποιαδήποτε υποστηριζόμενη γλώσσα) πριν καλέσετε `recognize()`.
- **Προσαρμοσμένο DPI:** Για θολές σαρώσεις, μπορείτε να βελτιώσετε την ακρίβεια ορίζοντας `ocrEngine.getImage().setResolution(300);`.

## Βήμα 5: Επαλήθευση του Αποτελέσματος (Τι να Περιμένετε)

Αφού τρέξει το πρόγραμμα, ελέγξτε το αρχείο `output.pdf`:

1. **Οπτικό στρώμα:** Το PDF εμφανίζει ακριβώς το PNG που δώσατε.
2. **Στρώμα κειμένου:** Πατήστε `Ctrl+F` (ή Cmd+F) και αναζητήστε μια λέξη που ξέρετε ότι υπάρχει στην εικόνα. Θα πρέπει να βρεθεί αμέσως.
3. **Αντιγραφή‑επικόλληση:** Επιλέξτε μια παράγραφο και αντιγράψτε την σε έναν επεξεργαστή κειμένου· θα λάβετε καθαρό, αναζητήσιμο κείμενο.

Αν η αναζήτηση αποτύχει, ελέγξτε ξανά ότι η εικόνα δεν είναι πολύ χαμηλής ανάλυσης ή ότι η σωστή γλώσσα έχει οριστεί. Συχνά, μια απλή αύξηση DPI λύνει το πρόβλημα.

## Συχνές Ερωτήσεις & Συμβουλές Επαγγελματιών

- **Χρειάζομαι άδεια;**  
  Το Aspose OCR λειτουργεί σε λειτουργία δοκιμής με υδατογράφημα. Για παραγωγή, αγοράστε άδεια και ορίστε την με `License license = new License(); license.setLicense("Aspose.OCR.lic");`.

- **Μπορώ να **μετατρέψω εικόνα σε pdf** χωρίς OCR;**  
  Ναι—χρησιμοποιήστε `OcrOutputFormat.PDF` με `ocrEngine.setRecognizeText(false);` πριν το `recognize()`. Αυτό θα δημιουργήσει ένα απλό PDF μόνο με εικόνα.

- **Τι κάνω αν θέλω μόνο το εξαγόμενο κείμενο;**  
  Παραλείψτε την κλήση `save` και χρησιμοποιήστε `ocrResult.getText()`· μπορείτε να το γράψετε σε αρχείο `.txt` ή να το τροφοδοτήσετε σε ευρετήριο αναζήτησης.

- **Συμβουλή απόδοσης:**  
  Επαναχρησιμοποιήστε το ίδιο αντικείμενο `OcrEngine` για πολλές εικόνες· μειώνει το κόστος αρχικοποίησης.

## Πλήρες Παράδειγμα (Ολοκληρωμένο)

Ακολουθεί το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα Java. Αντικαταστήστε τις διαδρομές placeholder με τις δικές σας, προσθέστε την εξάρτηση Maven και είστε έτοιμοι.

```java
import com.aspose.ocr.*;

public class PdfOutputExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the image (PNG, JPG, TIFF, etc.)
        String inputPath = "YOUR_DIRECTORY/input.png"; // <-- change this
        ocrEngine.setImage(ImageStream.fromFile(inputPath));

        // 3️⃣ Run OCR to get text and layout
        OcrResult ocrResult = ocrEngine.recognize();

        // Optional: display extracted text in console
        System.out.println("Extracted Text:");
        System.out.println(ocrResult.getText());

        // 4️⃣ Save as searchable PDF (image + hidden text layer)
        String outputPath = "YOUR_DIRECTORY/output.pdf"; // <-- change this
        ocrResult.save(outputPath, OcrOutputFormat.PDF);

        System.out.println("Searchable PDF created at: " + outputPath);
    }
}
```

**Αναμενόμενο αποτέλεσμα:**  
```
Extracted Text:
[...the plain text that was recognized from the PNG...]
Searchable PDF created at: YOUR_DIRECTORY/output.pdf
```

Ανοίξτε το `output.pdf` σε οποιονδήποτε προβολέα PDF και δοκιμάστε να αναζητήσετε μια λέξη από το εξαγόμενο κείμενο—θα πρέπει να επισημανθεί, επιβεβαιώνοντας ότι δημιουργήσατε επιτυχώς **create searchable pdf**.

## Συμπέρασμα

Σας δείξαμε πώς να **create searchable pdf** από PNG χρησιμοποιώντας Java και Aspose OCR. Τα βήματα είναι απλά: ρυθμίστε τη βιβλιοθήκη, φορτώστε την εικόνα, εκτελέστε OCR και αποθηκεύστε το αποτέλεσμα ως PDF. Κατά τη διάρκεια, μάθατε επίσης πώς να **μετατρέψετε εικόνα σε pdf**, **εξάγετε κείμενο από εικόνα**, και ακόμη **αναγνωρίσετε κείμενο από png** για πιο προχωρημένες περιπτώσεις.

Τι θα ακολουθήσει; Δοκιμάστε να επεξεργαστείτε μια παρτίδα σαρωμένων τιμολογίων σε βρόχο, αποθηκεύστε το κρυφό κείμενο σε βάση δεδομένων για πλήρη αναζήτηση, ή πειραματιστείτε με διαφορετικές γλώσσες και τεχνικές προεπεξεργασίας εικόνας. Το ίδιο μοτίβο λειτουργεί και για άλλες μορφές—απλώς αλλάξτε το αρχείο εισόδου και θα μπορείτε να **image to searchable pdf** σε χρόνο μηδέν.

Έχετε ερωτήσεις ή αντιμετωπίζετε προβλήματα; Αφήστε ένα σχόλιο παρακάτω, και καλή κωδικοποίηση!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}