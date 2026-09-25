---
category: general
date: 2026-02-17
description: Πώς να χρησιμοποιήσετε OCR σε Java για την εξαγωγή κειμένου από PDF,
  τη μετατροπή PDF σε εικόνες και την εκτέλεση OCR σε σαρωμένα αρχεία PDF χρησιμοποιώντας
  το Aspose.OCR.
draft: false
keywords:
- how to use OCR
- extract text from pdf
- convert pdf to images
- perform OCR on pdf
- recognize scanned pdf
language: el
og_description: Πώς να χρησιμοποιήσετε OCR στη Java για να εξάγετε κείμενο από αρχεία
  PDF. Μάθετε πώς να μετατρέπετε PDF σε εικόνες και να αναγνωρίζετε σαρωμένα PDF με
  το Aspose.OCR.
og_title: Πώς να χρησιμοποιήσετε OCR στη Java – Πλήρης οδηγός
tags:
- OCR
- Java
- Aspose
title: Πώς να χρησιμοποιήσετε OCR στη Java – Εξαγωγή κειμένου από PDF με το Aspose.OCR
url: /el/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-pdf-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε OCR σε Java – Εξαγωγή Κειμένου από PDF με Aspose.OCR

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε OCR** για να μετατρέψετε ένα σκαναρισμένο PDF σε κείμενο που μπορεί να αναζητηθεί; Δεν είστε οι μόνοι. Οι περισσότεροι προγραμματιστές συναντούν πρόβλημα όταν ένα PDF εμφανίζεται ως μια σειρά εικόνων, και οι συνήθεις εξαγωγείς κειμένου δεν επιστρέφουν τίποτα. Τα καλά νέα; Με λίγες γραμμές Java και Aspose.OCR μπορείτε να **εξάγετε κείμενο από PDF**, **μετατρέψετε PDF σε εικόνες**, και **αναγνωρίσετε σκαναρισμένο PDF** σε μια ενιαία, χωρίς κόπο διαδικασία.

Σε αυτό το tutorial θα περάσουμε από όλα όσα χρειάζεται να γνωρίζετε — από την αδειοδότηση της βιβλιοθήκης μέχρι την εκτύπωση του τελικού αποτελέσματος. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση πρόγραμμα που εξάγει απλό κείμενο από οποιαδήποτε σκαναρισμένη αναφορά, τιμολόγιο ή ebook. Χωρίς εξωτερικές υπηρεσίες, χωρίς μαγεία — μόνο καθαρός κώδικας Java που ελέγχετε εσείς.

## Τι Θα Χρειαστείτε

- **Java Development Kit (JDK) 8+** – οποιαδήποτε πρόσφατη έκδοση λειτουργεί.  
- **Aspose.OCR for Java** JAR (λήψη από την ιστοσελίδα της Aspose).  
- Ένα **έγκυρο αρχείο άδειας Aspose.OCR** (`Aspose.OCR.lic`). Η δωρεάν δοκιμή λειτουργεί, αλλά μια άδεια ξεκλειδώνει πλήρη ακρίβεια.  
- Ένα **δείγμα σκαναρισμένου PDF** (π.χ., `scanned-report.pdf`).  
- Ένα IDE ή απλός επεξεργαστής κειμένου συν τερματικό.

Αυτό είναι όλο. Χωρίς Maven, χωρίς Gradle, χωρίς επιπλέον εξαρτήσεις — μόνο το Aspose.OCR JAR στο classpath σας.

![πώς να χρησιμοποιήσετε OCR παράδειγμα](image-placeholder.png "πώς να χρησιμοποιήσετε OCR παράδειγμα")

## Βήμα 1 – Φορτώστε την Άδεια Aspose.OCR (Γιατί Είναι Σημαντικό)

Πριν η μηχανή λειτουργήσει με πλήρη ταχύτητα, πρέπει να της πείτε πού βρίσκεται η άδειά σας. Η παράλειψη αυτού του βήματος θέτει τη βιβλιοθήκη σε λειτουργία αξιολόγησης, η οποία προσθέτει υδατογραφήματα στο αποτέλεσμα και μπορεί να περιορίσει την ακρίβεια.

```java
import com.aspose.ocr.*;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {
        // Load the license – required for unrestricted OCR
        License license = new License();
        license.setLicense("Aspose.OCR.lic");
```

**Γιατί λειτουργεί αυτό:** Η κλάση `License` διαβάζει το αρχείο `.lic` και το καταχωρεί παγκοσμίως. Μόλις οριστεί, κάθε `OcrEngine` που δημιουργείτε θα χρησιμοποιεί αυτόματα τις αδειοδοτημένες δυνατότητες.

## Βήμα 2 – Δημιουργήστε τη Μηχανή OCR (Η Μηχανή Πίσω από τη Μαγεία)

Μια παρουσία `OcrEngine` είναι ο εργαζόμενος που σαρώνει εικόνες και παράγει κείμενο. Σκεφτείτε το ως τον εγκέφαλο που ερμηνεύει τα μοτίβα των pixel.

```java
        // Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

**Pro tip:** Μπορείτε να ρυθμίσετε τη γλώσσα, τα όρια εμπιστοσύνης, ή ακόμη και να ενεργοποιήσετε επιτάχυνση GPU μέσω των ιδιοτήτων της μηχανής. Για τα περισσότερα αγγλικά PDF, οι προεπιλογές είναι επαρκείς.

## Βήμα 3 – Προετοιμάστε την Είσοδο: Προσθέστε το PDF Σας (Μετατροπή PDF σε Εικόνες στο Παρασκήνιο)

Το Aspose.OCR αντιμετωπίζει κάθε σελίδα ενός PDF ως εικόνα. Όταν καλείτε `addPdf`, η βιβλιοθήκη σιωπηρά rasterizes κάθε σελίδα, που είναι ακριβώς ό,τι χρειάζεστε για **μετατροπή PDF σε εικόνες** πριν από την αναγνώριση.

```java
        // Prepare OCR input – each PDF page becomes an image internally
        OcrInput ocrInput = new OcrInput();
        ocrInput.addPdf("YOUR_DIRECTORY/scanned-report.pdf");
```

**Τι συμβαίνει:**  
- Το PDF ανοίγει.  
- Κάθε σελίδα αποδίδεται στα 300 dpi (προεπιλογή) για να διατηρηθεί η λεπτομέρεια των χαρακτήρων.  
- Τα αντικείμενα bitmap αποθηκεύονται στη συλλογή `OcrInput`.

Αν χρειαστείτε τις ακατέργαστες εικόνες (για αποσφαλμάτωση ή προεπεξεργασία), καλέστε `ocrInput.getPages()` μετά από αυτό το βήμα.

## Βήμα 4 – Εκτελέστε τη Διαδικασία OCR (Εκτέλεση OCR σε PDF)

Τώρα αρχίζει η βαριά δουλειά. Η μέθοδος `recognize` επαναλαμβάνει κάθε εικόνα, τρέχει τον αλγόριθμο αναγνώρισης, και συγκεντρώνει τα αποτελέσματα σε ένα `OcrResult`.

```java
        // Run OCR on the prepared input
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Γιατί σας ενδιαφέρει:** Το `OcrResult` περιέχει όχι μόνο απλό κείμενο, αλλά και βαθμολογίες εμπιστοσύνης, περιοριστικά πλαίσια, και την αρχική αναφορά εικόνας. Για τις περισσότερες περιπτώσεις, θα χρειαστείτε μόνο το `getText()`.

## Βήμα 5 – Ανακτήστε και Εμφανίστε το Εξαγόμενο Κείμενο

Τέλος, εξάγετε τη συμβολοσειρά κειμένου από το αποτέλεσμα και την εκτυπώστε. Μπορείτε επίσης να τη γράψετε σε αρχείο, να τη στείλετε σε ευρετήριο αναζήτησης, ή να τη δώσετε σε μια επόμενη διαδικασία NLP.

```java
        // Output the extracted text
        System.out.println("Extracted text:\n" + ocrResult.getText());
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Αν το `scanned-report.pdf` περιέχει μια απλή παράγραφο, θα δείτε κάτι σαν:

```
Extracted text:
Quarterly Sales Report
Region: North America
Total Revenue: $4,527,000
...
```

Η ακριβής μορφοποίηση αντικατοπτρίζει την αρχική διάταξη, διατηρώντας τις αλλαγές γραμμής όπου είναι δυνατόν.

## Διαχείριση Συνηθισμένων Περιπτώσεων

### 1. PDF Πολλαπλών Γλωσσών

Αν το έγγραφό σας περιέχει κείμενο στα Γαλλικά ή Ισπανικά, ορίστε τη γλώσσα πριν καλέσετε `recognize`:

```java
ocrEngine.getLanguage().setLanguage(OcrLanguage.FRENCH);
```

Μπορείτε να παρέχετε έναν πίνακα γλωσσών ώστε η μηχανή να εντοπίζει αυτόματα.

### 2. Σαρώσεις Χαμηλής Ανάλυσης

Για σαρώσεις 150 dpi, αυξήστε το εσωτερικό DPI απόδοσης:

```java
ocrInput.addPdf("low-res.pdf", 600); // render at 600 dpi for better accuracy
```

Υψηλότερο DPI βελτιώνει την ευκρίνεια των χαρακτήρων αλλά καταναλώνει περισσότερη μνήμη.

### 3. Μεγάλα PDF (Διαχείριση Μνήμης)

Για PDF με δεκάδες σελίδες, επεξεργαστείτε τα σε παρτίδες:

```java
int batchSize = 10;
for (int i = 0; i < ocrInput.getPages().size(); i += batchSize) {
    List<OcrPage> batch = ocrInput.getPages().subList(i, Math.min(i + batchSize, ocrInput.getPages().size()));
    OcrInput batchInput = new OcrInput();
    batchInput.getPages().addAll(batch);
    OcrResult batchResult = ocrEngine.recognize(batchInput);
    // Append batchResult.getText() to your final output
}
```

Αυτή η προσέγγιση αποτρέπει την υπερφόρτωση του heap της JVM.

## Πλήρες, Έτοιμο‑για‑Εκτέλεση Παράδειγμα

Παρακάτω βρίσκεται το πλήρες πρόγραμμα — συμπεριλαμβανομένων των imports και της διαχείρισης άδειας — ώστε να το αντιγράψετε‑και‑εκτελέσετε αμέσως.

```java
import com.aspose.ocr.*;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (required for full functionality)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // Step 2: Create an OCR engine instance that will perform the recognition
        OcrEngine ocrEngine = new OcrEngine();

        // Step 3: Prepare the OCR input by adding the PDF file.
        // Each page of the PDF is internally converted to an image.
        OcrInput ocrInput = new OcrInput();
        ocrInput.addPdf("YOUR_DIRECTORY/scanned-report.pdf");

        // Step 4: Run the OCR process on the prepared input
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Step 5: Display the extracted text
        System.out.println("Extracted text:\n" + ocrResult.getText());
    }
}
```

Τρέξτε το με:

```bash
javac -cp "path/to/aspose-ocr.jar" PdfOcrDemo.java
java -cp ".:path/to/aspose-ocr.jar" PdfOcrDemo
```

Θα πρέπει να δείτε το εξαγόμενο κείμενο να εκτυπώνεται στην κονσόλα.

## Ανακεφαλαίωση – Τι Καλύψαμε

- **Πώς να χρησιμοποιήσετε OCR** σε Java με Aspose.OCR.  
- Η ροή εργασίας για **εξαγωγή κειμένου από PDF**.  
- Εσωτερικά, η βιβλιοθήκη **μετατρέπει PDF σε εικόνες** πριν αναγνωρίσει χαρακτήρες.  
- Συμβουλές για **εκτέλεση OCR σε PDF** με πολλαπλές γλώσσες, σαρώσεις χαμηλής ανάλυσης, και μεγάλα έγγραφα.  
- Ένα πλήρες, εκτελέσιμο δείγμα κώδικα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Java.

## Επόμενα Βήματα & Σχετικά Θέματα

Τώρα που μπορείτε να **αναγνωρίσετε σκαναρισμένο PDF**, σκεφτείτε τις παρακάτω ιδέες:

- **Δημιουργία Αναζητήσιμου PDF** – επικάλυψη του κειμένου OCR πάνω στο αρχικό PDF για δημιουργία εγγράφου αναζητήσιμου.  
- **Υπηρεσία Μαζικής Επεξεργασίας** – τυλίξτε τον κώδικα σε μικροϋπηρεσία Spring Boot που δέχεται PDF μέσω REST.  
- **Ενσωμάτωση με Elasticsearch** – ευρετηρίαση του εξαγόμενου κειμένου για γρήγορη πλήρη αναζήτηση κειμένου στο αποθετήριο εγγράφων σας.  
- **Προεπεξεργασία Εικόνας** – χρήση OpenCV για διόρθωση κλίσης ή μείωση θορύβου των σελίδων πριν το OCR για ακόμη μεγαλύτερη ακρίβεια.

Κάθε ένα από αυτά τα θέματα βασίζεται στις βασικές έννοιες που εξερευνήσαμε, οπότε μη διστάσετε να πειραματιστείτε και να αφήσετε τη μηχανή OCR να κάνει το σκληρό έργο.

---

*Καλή προγραμματιστική! Αν αντιμετωπίσετε προβλήματα — όπως σφάλματα άδειας ή απροσδόκητα null αποτελέσματα — αφήστε ένα σχόλιο παρακάτω. Είμαι πάντα διαθέσιμος για μια συνεδρία αποσφαλμάτωσης.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}