---
category: general
date: 2026-02-22
description: Πώς να χρησιμοποιήσετε το OCR σε Java για να εξάγετε κείμενο από PDF
  γρήγορα με το Aspose OCR – βήμα‑βήμα οδηγός που καλύπτει την παράλληλη επεξεργασία
  και πλήρες παράδειγμα κώδικα.
draft: false
keywords:
- how to use OCR
- extract text from pdf
- aspose ocr java example
- parallel OCR processing
- Java PDF extraction
language: el
og_description: Πώς να χρησιμοποιήσετε OCR σε Java για γρήγορη εξαγωγή κειμένου από
  PDF με το Aspose OCR – πλήρης οδηγός με παράλληλη επεξεργασία και εκτελέσιμο κώδικα.
og_title: Πώς να χρησιμοποιήσετε OCR στη Java – Εξαγωγή κειμένου από PDF (Aspose OCR)
tags:
- OCR
- Java
- Aspose
- PDF
title: Πώς να χρησιμοποιήσετε OCR στη Java – Εξαγωγή κειμένου από PDF (Aspose OCR)
url: /el/java/advanced-ocr-techniques/how-to-use-ocr-in-java-extract-text-from-pdf-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να χρησιμοποιήσετε OCR σε Java – Εξαγωγή κειμένου από PDF (Aspose OCR)

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε OCR** σε Java όταν έχετε μια στοίβα σαρωμένων PDF που περιμένουν να γίνουν αναζητήσιμα; Δεν είστε μόνοι. Σε πολλά έργα το στενό λαιμό είναι η εξαγωγή καθαρού, αναζητήσιμου κειμένου από ένα πολυσελίδες έγγραφο χωρίς να καταναλώνετε πολλούς πόρους CPU. Αυτό το σεμινάριο σας δείχνει **πώς να χρησιμοποιήσετε OCR** με το Aspose OCR για Java, ενεργοποιώντας την παράλληλη επεξεργασία ώστε να μπορείτε να εξάγετε κείμενο από αρχεία PDF σε ελάχιστο χρόνο.

Θα περάσουμε βήμα-βήμα από κάθε γραμμή ενός λειτουργικού **παραδείγματος Aspose OCR Java**, θα εξηγήσουμε γιατί κάθε ρύθμιση είναι σημαντική και ακόμη θα καλύψουμε μερικές περιπτώσεις που μπορεί να συναντήσετε στην πράξη. Στο τέλος, θα έχετε ένα έτοιμο‑για‑εκτέλεση πρόγραμμα που μπορεί να διαβάσει οποιοδήποτε PDF, να εκτελέσει OCR σε όλες τις σελίδες του ταυτόχρονα και να εκτυπώσει το συνδυασμένο αποτέλεσμα στην κονσόλα.

![πώς να χρησιμοποιήσετε OCR με Aspose OCR Java](/images/ocr-parallel.png "Εικονογράφηση της παράλληλης επεξεργασίας OCR σε Java – πώς να χρησιμοποιήσετε OCR")

## Τι θα πετύχετε

- Αρχικοποιήστε ένα `OcrEngine` από τη βιβλιοθήκη Aspose OCR.  
- Ενεργοποιήστε την **παράλληλη επεξεργασία** και προαιρετικά περιορίστε το thread pool.  
- Φορτώστε ένα πολυσελίδες PDF μέσω του `OcrInput`.  
- Εκτελέστε OCR σε όλες τις σελίδες ταυτόχρονα και συλλέξτε το συνδυασμένο κείμενο.  
- Εκτυπώστε το αποτέλεσμα ή το διοχετεύστε σε οποιοδήποτε σύστημα downstream που θέλετε.

Θα μάθετε επίσης πότε να ρυθμίζετε τον αριθμό των νημάτων, πώς να διαχειρίζεστε PDF προστατευμένα με κωδικό πρόσβασης, και γιατί μπορεί να θέλετε να απενεργοποιήσετε την παράλληλη επεξεργασία για πολύ μικρά αρχεία.

---

## Πώς να χρησιμοποιήσετε OCR με Aspose OCR Java

### Βήμα 1: Ρυθμίστε το έργο σας

Πριν γράψετε οποιονδήποτε κώδικα, βεβαιωθείτε ότι έχετε τη βιβλιοθήκη Aspose OCR για Java στο classpath σας. Ο πιο εύκολος τρόπος είναι μέσω Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Αν προτιμάτε Gradle, απλώς αντικαταστήστε το απόσπασμα ανάλογα. Αφού η εξάρτηση λυθεί, είστε έτοιμοι να εισάγετε τις κλάσεις που θα χρειαστείτε.

### Βήμα 2: Δημιουργήστε και διαμορφώστε τη μηχανή OCR

Το `OcrEngine` είναι η καρδιά της βιβλιοθήκης. Η ενεργοποίηση της παράλληλης επεξεργασίας λέει στο Aspose να δημιουργήσει μια ομάδα εργαζόμενων νημάτων, το καθένα να χειρίζεται μια ξεχωριστή σελίδα.

```java
// Step 2: Initialise the OCR engine and enable parallel processing
OcrEngine ocrEngine = new OcrEngine();

// Turn on parallel processing – this is the key to faster PDF extraction
ocrEngine.setParallelProcessing(true);

// Optional: limit the number of threads (helps on low‑end machines)
ocrEngine.setMaxThreadCount(4);
```

**Γιατί είναι σημαντικό:**
- `setParallelProcessing(true)` χωρίζει το φορτίο εργασίας, το οποίο μπορεί να μειώσει δραματικά τον χρόνο επεξεργασίας σε CPU με πολλούς πυρήνες.
- `setMaxThreadCount` αποτρέπει τη μηχανή από το να καταναλώνει όλους τους πυρήνες, ένα χρήσιμο μέτρο ασφαλείας σε κοινόχρηστους διακομιστές ή CI pipelines.

### Βήμα 3: Φορτώστε το PDF που θέλετε να επεξεργαστείτε

Το Aspose OCR λειτουργεί με οποιαδήποτε μορφή εικόνας, αλλά δέχεται επίσης PDF απευθείας μέσω του `OcrInput`. Μπορείτε να προσθέσετε πολλαπλά αρχεία ή ακόμη και να αναμείξετε εικόνες και PDF στην ίδια δέσμη.

```java
// Step 3: Prepare the input – add your multi‑page PDF
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/multi_page_document.pdf");

// If the PDF is password‑protected, supply the password like this:
// ocrInput.add("protected.pdf", "mySecretPassword");
```

**Συμβουλή:** Διατηρήστε τη διαδρομή του PDF απόλυτη ή σχετική με τον τρέχοντα φάκελο εργασίας για να αποφύγετε το `FileNotFoundException`. Επίσης, η μέθοδος `add` μπορεί να κληθεί επανειλημμένα αν χρειάζεται να επεξεργαστείτε πολλά PDF σε μία εκτέλεση.

### Βήμα 4: Εκτελέστε OCR σε όλες τις σελίδες παράλληλα

Τώρα η μηχανή κάνει τη βαριά δουλειά. Η κλήση στο `recognize` επιστρέφει ένα `OcrResult` που συγκεντρώνει το κείμενο από κάθε σελίδα.

```java
// Step 4: Perform OCR – this will run on multiple threads
OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Πίσω από τη σκηνή:** Κάθε σελίδα παραδίδεται σε ξεχωριστό νήμα (μέχρι το `maxThreadCount` που έχετε ορίσει). Η βιβλιοθήκη διαχειρίζεται το συγχρονισμό, έτσι το τελικό `OcrResult` είναι ήδη σωστά ταξινομημένο.

### Βήμα 5: Ανακτήστε και εμφανίστε το συνδυασμένο κείμενο

Τέλος, λάβετε το έξοδο plain‑text. Μπορείτε να το γράψετε σε αρχείο, να το σπρώξετε σε ευρετήριο αναζήτησης ή απλώς να το εκτυπώσετε για γρήγορη επαλήθευση.

```java
// Step 5: Output the combined OCR result
System.out.println("Combined text from all pages:");
System.out.println(ocrResult.getText());
```

**Αναμενόμενο αποτέλεσμα:** Η κονσόλα θα εμφανίσει μια ενιαία συμβολοσειρά που περιέχει το αναγνώσιμο κείμενο από κάθε σελίδα, με τις αλλαγές γραμμής να διατηρούνται όπως εμφανίστηκαν στο αρχικό PDF.

---

## Πλήρες παράδειγμα Aspose OCR Java – Έτοιμο για εκτέλεση

Συνδυάζοντας όλα τα κομμάτια, εδώ είναι το πλήρες, αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα αρχείο `ParallelOcrDemo.java` και να το εκτελέσετε.

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable parallel processing and optionally limit threads
        ocrEngine.setParallelProcessing(true);
        ocrEngine.setMaxThreadCount(4); // Adjust based on your hardware

        // Step 3: Load the multi‑page PDF to be processed
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/multi_page_document.pdf");
        // Uncomment and set password if needed:
        // ocrInput.add("protected.pdf", "mySecretPassword");

        // Step 4: Recognize text from all pages in parallel
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Step 5: Display the combined OCR result
        System.out.println("Combined text from all pages:");
        System.out.println(ocrResult.getText());
    }
}
```

Τρέξτε το με:

```bash
javac -cp "path/to/aspose-ocr.jar" ParallelOcrDemo.java
java -cp ".:path/to/aspose-ocr.jar" ParallelOcrDemo
```

Αν όλα είναι ρυθμισμένα σωστά, θα δείτε το εξαγόμενο κείμενο να εκτυπώνεται λίγο μετά την έναρξη του προγράμματος.

---

## Συχνές ερωτήσεις & Ακραίες περιπτώσεις

### Χρειάζομαι πραγματικά την παράλληλη επεξεργασία;

Αν το PDF σας έχει **περισσότερες από λίγες σελίδες** και βρίσκεστε σε μηχάνημα με τουλάχιστον 4 πυρήνες, η ενεργοποίηση της παράλληλης επεξεργασίας μπορεί να μειώσει **30‑70 %** του συνολικού χρόνου εκτέλεσης. Για σάρωση μίας σελίδας, το κόστος διαχείρισης νημάτων μπορεί να υπερβαίνει το όφελος, οπότε μπορείτε απλώς να καλέσετε `ocrEngine.setParallelProcessing(false)`.

### Τι γίνεται αν μια σελίδα αποτύχει στο OCR;

Το Aspose OCR ρίχνει ένα `OcrException` μόνο για μοιραίες σφάλματα (π.χ., κατεστραμμένο αρχείο). Οι μη αναγνωρίσιμες σελίδες επιστρέφουν απλώς μια κενή συμβολοσειρά για εκείνη τη σελίδα, την οποία η μηχανή ενώνει σιωπηλά. Μπορείτε να εξετάσετε το `ocrResult.getPageResults()` για να δείτε τις βαθμολογίες εμπιστοσύνης ανά σελίδα και να χειριστείτε χειροκίνητα τις σελίδες χαμηλής εμπιστοσύνης.

### Πώς ελέγχω τη γλώσσα εξόδου;

Η μηχανή προεπιλογή είναι η αγγλική, αλλά μπορείτε να αλλάξετε γλώσσες με:

```java
ocrEngine.getLanguageEngine().setLanguage(OcrLanguage.FRENCH);
```

Αντικαταστήστε το `FRENCH` με οποιοδήποτε υποστηριζόμενο enum γλώσσας. Αυτό είναι χρήσιμο όταν χρειάζεται να **εξάγετε κείμενο από PDF** έγγραφα σε πολλαπλές τοπικές γλώσσες.

### Μπορώ να περιορίσω τη χρήση μνήμης;

Ναι. Χρησιμοποιήστε `ocrEngine.setMemoryLimit(256);` για να περιορίσετε το αποτύπωμα μνήμης στα 256 MB. Η βιβλιοθήκη θα αποθηκεύσει τα επιπλέον δεδομένα σε προσωρινά αρχεία, αποτρέποντας καταρρεύσεις λόγω έλλειψης μνήμης σε τεράστια PDF.

---

## Επαγγελματικές συμβουλές για OCR έτοιμο για παραγωγή

- **Επεξεργασία παρτίδας:** Τυλίξτε όλη τη ροή σε έναν βρόχο που διαβάζει ονόματα αρχείων από έναν φάκελο. Αυτό μετατρέπει το demo σε κλιμακούμενη υπηρεσία.  
- **Καταγραφή:** Το Aspose OCR παρέχει τη μέθοδο `setLogLevel` – ορίστε την σε `LogLevel.ERROR` στην παραγωγή για να αποφύγετε θορυβώδη έξοδο.  
- **Καθαρισμός αποτελεσμάτων:** Μετα-επεξεργαστείτε το `ocrResult.getText()` για να αφαιρέσετε ανεπιθύμητα κενά ή τεχνάσματα αλλαγής γραμμής. Οι κανονικές εκφράσεις λειτουργούν καλά για αυτό.  
- **Ρύθμιση του thread pool:** Σε διακομιστή με πολλούς πυρήνες, πειραματιστείτε με `setMaxThreadCount(Runtime.getRuntime().availableProcessors())` για βέλτιστη απόδοση.  

---

## Συμπέρασμα

Συζητήσαμε **πώς να χρησιμοποιήσετε OCR** σε Java με το Aspose OCR, παρουσιάσαμε μια πλήρη ροή **εξαγωγής κειμένου από PDF**, και παρέχουμε ένα ολοκληρωμένο **παράδειγμα Aspose OCR Java** που εκτελείται παράλληλα για ταχύτητα. Ακολουθώντας τα παραπάνω βήματα, μπορείτε να μετατρέψετε οποιοδήποτε σαρωμένο PDF σε αναζητήσιμο κείμενο με λίγες μόνο γραμμές κώδικα.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να τροφοδοτήσετε το αποτέλεσμα του OCR στο Elasticsearch για πλήρη αναζήτηση κειμένου, ή συνδυάστε το με ένα API μετάφρασης γλώσσας για να δημιουργήσετε μια πολυγλωσσική γραμμή επεξεργασίας εγγράφων. Ο ουρανός είναι το όριο μόλις κυριαρχήσετε τα βασικά.

Αν αντιμετωπίσετε προβλήματα, αφήστε ένα σχόλιο παρακάτω—καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}