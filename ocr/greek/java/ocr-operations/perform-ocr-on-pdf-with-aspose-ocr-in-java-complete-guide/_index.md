---
category: general
date: 2026-05-25
description: Εκτελέστε OCR σε PDF χρησιμοποιώντας το Aspose OCR σε Java. Μάθετε πώς
  να εξάγετε κείμενο από PDF, να μετατρέψετε PDF σε κείμενο και να φορτώνετε PDF για
  OCR γρήγορα.
draft: false
keywords:
- perform ocr on pdf
- extract text from pdf
- convert pdf to text
- extract scanned pdf text
- load pdf for ocr
language: el
og_description: εκτελέστε OCR σε PDF με Java χρησιμοποιώντας Aspose OCR. Αυτός ο οδηγός
  δείχνει πώς να εξάγετε κείμενο από σαρωμένο PDF, να μετατρέψετε PDF σε κείμενο και
  να φορτώσετε PDF για OCR.
og_title: Εκτελέστε OCR σε PDF με το Aspose OCR – Εγχειρίδιο Java
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: perform ocr on pdf using Aspose OCR in Java. Learn how to extract text
    from pdf, convert pdf to text and load pdf for ocr quickly.
  headline: perform ocr on pdf with Aspose OCR in Java – Complete Guide
  type: TechArticle
- description: perform ocr on pdf using Aspose OCR in Java. Learn how to extract text
    from pdf, convert pdf to text and load pdf for ocr quickly.
  name: perform ocr on pdf with Aspose OCR in Java – Complete Guide
  steps:
  - name: Expected Output
    text: 'Running the program against a three‑page brochure might yield something
      like:'
  - name: 5.1 Setting the Language (for better accuracy)
    text: 'Aspose OCR defaults to English, but scanned PDFs often contain other languages.
      To improve accuracy, set the language before calling `recognize()`:'
  - name: 5.2 Handling Large PDFs
    text: 'Processing a 500‑page PDF in one go can be memory‑intensive. A practical
      workaround is to process pages in batches:'
  - name: 5.3 Dealing with Low‑Quality Scans
    text: 'If the source PDF is blurry, consider enabling image preprocessing:'
  - name: 5.4 Exporting to a Text File (Full Convert PDF to Text)
    text: 'If you prefer a single `.txt` file instead of console output, just pipe
      the strings:'
  type: HowTo
tags:
- Java
- Aspose OCR
- PDF processing
title: Εκτέλεση OCR σε PDF με Aspose OCR σε Java – Πλήρης Οδηγός
url: /el/java/ocr-operations/perform-ocr-on-pdf-with-aspose-ocr-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# εκτέλεση ocr σε pdf με Aspose OCR σε Java – Πλήρης Οδηγός

Ποτέ δεν χρειάστηκε να **εκτελέσετε OCR σε αρχεία PDF** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη θα το έκανε χωρίς προβλήματα; Δεν είστε μόνοι—τα σαρωμένα PDF είναι παντού, από αποδείξεις μέχρι νομικά συμβόλαια, και η εξαγωγή του κειμένου μπορεί να μοιάζει με άνοιγμα θυρίδας χρηματοκιβωτίου.

Σε αυτό το μάθημα θα περάσουμε από ένα πρακτικό, ολοκληρωμένο παράδειγμα που δείχνει πώς να **εξάγετε κείμενο από PDF**, **μετατρέψετε PDF σε κείμενο**, και ακόμη **φορτώσετε PDF για OCR** χρησιμοποιώντας τη βιβλιοθήκη Aspose OCR για Java. Στο τέλος θα έχετε ένα έτοιμο πρόγραμμα που εκτυπώνει το περιεχόμενο κάθε σελίδας στην κονσόλα.

## Τι Θα Χρειαστείτε

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τα εξής:

- **Java Development Kit (JDK) 8+** – οποιαδήποτε πρόσφατη έκδοση αρκεί.
- **Maven ή Gradle** – για να προσθέσετε την εξάρτηση Aspose OCR.
- Ένα **σκαναρισμένο PDF** (θα το ονομάσουμε `brochure.pdf`) τοποθετημένο κάπου που μπορείτε να το αναφέρετε.
- Μια μέτρια ποσότητα RAM (η επίδειξη τρέχει άνετα σε laptop).

Καμία επιπλέον εγγενής βιβλιοθήκη, κανένα περίπλοκο αρχείο ρυθμίσεων—μόνο καθαρή Java και μια ενιαία συντεταγμένη Maven.

![διάγραμμα ροής εκτέλεσης ocr σε pdf](images/ocr-workflow.png "διάγραμμα ροής εκτέλεσης ocr σε pdf")

*(Image alt text: διάγραμμα ροής εκτέλεσης ocr σε pdf)*

## Βήμα 1: Εκτέλεση OCR σε PDF – Ρύθμιση του Aspose OCR

Πρώτο πράγμα: προσθέστε τη βιβλιοθήκη Aspose OCR στο έργο σας. Αν χρησιμοποιείτε Maven, τοποθετήστε αυτό το απόσπασμα στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

Οι χρήστες Gradle μπορούν να προσθέσουν:

```gradle
implementation 'com.aspose:aspose-ocr:23.10'
```

Γιατί η προσοχή στον αριθμό έκδοσης; Οι νέες κυκλοφορίες συχνά φέρνουν βελτιώσεις απόδοσης για **εξαγωγή κειμένου από σκαναρισμένο PDF**, και διατηρούν το API σταθερό. Μόλις η εξάρτηση λυθεί, είστε έτοιμοι να γράψετε τον κώδικα Java.

## Βήμα 2: Φόρτωση PDF για OCR – Ανάγνωση του Εγγράφου

Τώρα που η βιβλιοθήκη βρίσκεται στο classpath, πρέπει να **φορτώσουμε PDF για OCR**. Αυτό το βήμα είναι κρίσιμο επειδή το Aspose αντιμετωπίζει κάθε σελίδα ως εικόνα εσωτερικά, γι' αυτό λειτουργεί σε σκαναρισμένα PDF που δεν έχουν στρώση κειμένου.

```java
import com.aspose.ocr.*;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {
        // Create an OCR engine instance – this is the heart of the operation
        OcrEngine ocrEngine = new OcrEngine();

        // Load the multi‑page PDF you want to process
        // Replace the path with the actual location of your file
        ocrEngine.getImage().loadFromFile("YOUR_DIRECTORY/brochure.pdf");
```

Παρατηρήστε την κλήση στο `loadFromFile`. Είναι ο πιο απλός τρόπος για **φόρτωση pdf για ocr**· μπορείτε επίσης να περάσετε ένα `byte[]` αν το PDF βρίσκεται σε βάση δεδομένων. Η μηχανή τώρα κρατά μια rasterized αναπαράσταση κάθε σελίδας, έτοιμη για αναγνώριση.

## Βήμα 3: Εξαγωγή Κειμένου από PDF – Εκτέλεση της Μηχανής OCR

Με το PDF φορτωμένο, το επόμενο λογικό βήμα είναι να τρέξετε τη διαδικασία OCR. Το Aspose το κάνει με μία γραμμή:

```java
        // Perform OCR on all pages and obtain the result
        OcrResult ocrResult = ocrEngine.recognize();
```

Γιατί μια μόνο μέθοδος; Στο παρασκήνιο, το Aspose κάνει όλη τη βαριά δουλειά—προεπεξεργασία εικόνας, ανίχνευση γλώσσας, και διαχωρισμό χαρακτήρων. Η κλήση `recognize()` επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει μια συλλογή αντικειμένων `Page`, το καθένα με το δικό του εξαγόμενο κείμενο.

## Βήμα 4: Μετατροπή PDF σε Κείμενο – Επανάληψη στις Σελίδες

Τώρα που έχουμε το `ocrResult`, ας **μετατρέψουμε PDF σε κείμενο** διασχίζοντας κάθε σελίδα και εκτυπώνοντας το αποτέλεσμα. Εδώ μπορείτε επίσης να γράψετε τις συμβολοσειρές σε αρχείο, βάση δεδομένων ή να τις περάσετε σε άλλη υπηρεσία.

```java
        // Iterate through each recognized page and print its text
        for (int i = 0; i < ocrResult.getAllPages().size(); i++) {
            System.out.println("=== Page " + (i + 1) + " ===");
            System.out.println(ocrResult.getAllPages().get(i).getText());
        }
    }
}
```

Μια σύντομη σημείωση για τη μέθοδο `getAllPages()`: επιστρέφει μια `List<Page>` με την ίδια σειρά όπως το αρχικό PDF, έτσι διατηρείτε αυτόματα την αρίθμηση σελίδων. Αν χρειάζεστε μόνο την πρώτη σελίδα, αντικαταστήστε το βρόχο με `ocrResult.getAllPages().get(0).getText()`.

### Αναμενόμενη Έξοδος

Η εκτέλεση του προγράμματος σε ένα τρισελίδες φυλλάδιο μπορεί να δώσει κάτι όπως:

```
=== Page 1 ===
Welcome to Our Summer Catalog
...

=== Page 2 ===
Featured Products
...

=== Page 3 ===
Contact Information
...
```

Αν το PDF περιέχει μη λατινικούς χαρακτήρες, μπορείτε να προσαρμόσετε τις ρυθμίσεις γλώσσας του `OcrEngine`—κάτι που θα καλύψουμε στην επόμενη ενότητα.

## Βήμα 5: Επαγγελματικές Συμβουλές & Συνηθισμένα Πιθανά Σφάλματα

### 5.1 Ορισμός της Γλώσσας (για καλύτερη ακρίβεια)

Το Aspose OCR προεπιλογή είναι τα Αγγλικά, αλλά τα σκαναρισμένα PDF συχνά περιέχουν άλλες γλώσσες. Για να βελτιώσετε την ακρίβεια, ορίστε τη γλώσσα πριν καλέσετε το `recognize()`:

```java
ocrEngine.getLanguage().setLanguage(OcrLanguage.FRENCH);
```

Μπορείτε επίσης να ενεργοποιήσετε πολλαπλές γλώσσες ταυτόχρονα.

### 5.2 Διαχείριση Μεγάλων PDF

Η επεξεργασία ενός PDF 500 σελίδων σε μία φορά μπορεί να καταναλώσει πολύ μνήμη. Μια πρακτική λύση είναι η επεξεργασία των σελίδων σε παρτίδες:

```java
int batchSize = 50;
for (int start = 0; start < totalPages; start += batchSize) {
    ocrEngine.getImage().loadFromFile("brochure.pdf", start, batchSize);
    OcrResult batchResult = ocrEngine.recognize();
    // handle batchResult...
}
```

### 5.3 Αντιμετώπιση Χαμηλής Ποιότητας Σαρώσεων

Αν το πηγαίο PDF είναι θολό, σκεφτείτε να ενεργοποιήσετε την προεπεξεργασία εικόνας:

```java
ocrEngine.getPreprocessingOptions().setAutoDeskew(true);
ocrEngine.getPreprocessingOptions().setContrast(1.2);
```

Αυτές οι ρυθμίσεις συχνά μετατρέπουν ένα ακαταλαβίστικο αποτέλεσμα σε αναγνώσιμο κείμενο.

### 5.4 Εξαγωγή σε Αρχείο Κειμένου (Πλήρης Μετατροπή PDF σε Κείμενο)

Αν προτιμάτε ένα ενιαίο αρχείο `.txt` αντί για έξοδο στην κονσόλα, απλώς περάστε τις συμβολοσειρές:

```java
import java.nio.file.*;

Path output = Paths.get("brochure.txt");
try (BufferedWriter writer = Files.newBufferedWriter(output)) {
    for (Page page : ocrResult.getAllPages()) {
        writer.write(page.getText());
        writer.newLine();
        writer.write(System.lineSeparator());
    }
}
System.out.println("PDF converted to text file at " + output.toAbsolutePath());
```

Τώρα έχετε **μετατρέψει PDF σε κείμενο** σε μορφή που μπορεί να επαναχρησιμοποιηθεί.

## Βήμα 6: Πέρα από το Βασικό – Ενσωμάτωση με Άλλα Συστήματα

Μόλις μπορείτε να **εξάγετε κείμενο από σκαναρισμένο PDF**, ανοίγονται πολλές δυνατότητες:

- **Δημιουργία ευρετηρίου αναζήτησης** – τροφοδοτήστε τις εξαγόμενες συμβολοσειρές στο Elasticsearch.
- **Εξαγωγή δεδομένων** – εφαρμόστε κανονικές εκφράσεις για να βγάλτε αριθμούς τιμολογίων.
- **Μηχανική μάθηση** – χρησιμοποιήστε το ακατέργαστο κείμενο ως δεδομένα εκπαίδευσης για μοντέλα NLP.

Όλα αυτά τα σενάρια ξεκινούν από τον ίδιο πυρήνα κώδικα που μόλις χτίσαμε, αποδεικνύοντας πόσο ευέλικτο είναι το Aspose OCR API.

## Συμπέρασμα

Καλύψαμε όλα όσα χρειάζεστε για να **εκτελέσετε OCR σε PDF** αρχεία χρησιμοποιώντας το Aspose OCR σε Java: από την προσθήκη της βιβλιοθήκης, **φόρτωση PDF για OCR**, **εξαγωγή κειμένου από PDF**, και τέλος **μετατροπή PDF σε κείμενο** για αποθήκευση ή περαιτέρω επεξεργασία. Με τα αποσπάσματα κώδικα παραπάνω μπορείτε να τρέξετε τη demo σήμερα, να ρυθμίσετε τις γλώσσες και να κλιμακώσετε σε τεράστια έγγραφα χωρίς προβλήματα.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να **εξάγετε κείμενο από σκαναρισμένο PDF** από αρχεία με κωδικό πρόσβασης, ή συνδυάστε αυτή τη ροή εργασίας με το Aspose PDF για να τροποποιήσετε το αρχικό έγγραφο μετά το OCR. Ο ουρανός είναι το όριο, και τώρα έχετε μια σταθερή βάση για να χτίσετε πάνω της.

Καλός κώδικας, και ας είναι πάντα τα PDF σας αναζητήσιμα!

## Σχετικά Μαθήματα

- [Αναγνώριση Κειμένου PDF – Λειτουργίες OCR με Aspose.OCR για Java](/ocr/english/java/ocr-operations/)
- [OCR Αναγνώριση Εγγράφων PDF στο Aspose.OCR για Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Πώς να εξάγετε κείμενο από εικόνα από URL χρησιμοποιώντας Aspose.OCR για Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}