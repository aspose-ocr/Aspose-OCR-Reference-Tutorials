---
category: general
date: 2026-06-19
description: Δημιουργία PDF με δυνατότητα αναζήτησης σε Java χρησιμοποιώντας το Aspose
  OCR – επεξεργασία OCR κατά παρτίδες για μετατροπή εικόνων σε PDF με δυνατότητα αναζήτησης
  και υποστήριξη της ισπανικής γλώσσας.
draft: false
keywords:
- create searchable pdf
- batch ocr processing
- images to searchable pdf
- batch convert images
- ocr language spanish
language: el
og_description: Δημιουργήστε αναζητήσιμο PDF σε Java με το Aspose OCR. Μάθετε την
  επεξεργασία OCR σε παρτίδες, μετατρέψτε εικόνες σε αναζητήσιμο PDF και ορίστε τη
  γλώσσα OCR στα Ισπανικά.
og_title: Δημιουργία PDF με δυνατότητα αναζήτησης από εικόνες σε Java – Πλήρης Οδηγός
  OCR σε Batch
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Create searchable PDF in Java using Aspose OCR – batch OCR processing
    to convert images to searchable PDF with Spanish language support.
  headline: Create Searchable PDF from Images in Java – Complete Batch OCR Guide
  type: TechArticle
tags:
- Java
- OCR
- Aspose
- PDF
title: Δημιουργία Αναζητήσιμου PDF από Εικόνες σε Java – Πλήρης Οδηγός Batch OCR
url: /el/java/advanced-ocr-techniques/create-searchable-pdf-from-images-in-java-complete-batch-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Αναζητήσιμου PDF από Εικόνες σε Java – Πλήρης Οδηγός Batch OCR

Έχετε ποτέ χρειαστεί να **δημιουργήσετε αναζητήσιμο PDF** από ένα σωρό σαρωμένων εικόνων; Δεν είστε μόνοι—οι εταιρείες συνεχώς μετατρέπουν τα χαρτικά αρχεία σε αναζητήσιμα PDF ώστε τα δεδομένα τους να είναι άμεσα εύρετα.  

Τι θα λέγατε αν μπορούσατε να αυτοματοποιήσετε όλη αυτή τη ροή εργασίας με ένα μόνο πρόγραμμα Java, επεξεργαζόμενο δεκάδες ή ακόμη και χιλιάδες αρχεία σε μία εκτέλεση; Σε αυτό το tutorial θα περάσουμε από **batch OCR processing** χρησιμοποιώντας το Aspose OCR, μετατρέποντας έναν φάκελο εικόνων σε αναζητήσιμα PDF ενώ ορίζουμε **OCR language Spanish**. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση project που **batch converts images** σε αναζητήσιμα PDF χωρίς να χρειάζεται να αγγίξετε κάθε αρχείο ξεχωριστά.

## Τι Θα Μάθετε

* Πώς να ρυθμίσετε το Aspose OCR σε ένα έργο Java.  
* Διαμόρφωση ενός batch επεξεργαστή που σαρώει έναν φάκελο, φιλτράρει τύπους εικόνων και γράφει τα PDF εξόδου.  
* Ενεργοποίηση επιτάχυνσης GPU για εργασίες κρίσιμης ταχύτητας.  
* Εφαρμογή χρήσιμων βημάτων προεπεξεργασίας όπως ευθυγράμμιση (deskew) και αποθορυβοποίηση (denoise).  
* Καθορισμός της γλώσσας OCR (Ισπανικά) και της μορφής εξόδου (αναζητήσιμο PDF).  

Καμία εξωτερική script, καμία χειροκίνητη αντιγραφή‑επικόλληση—μόνο μια καθαρή μέθοδος `main` που κάνει τα πάντα.

---

## Προαπαιτούμενα

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|-----------------------|
| Java 17 ή νεότερη (ή οποιοδήποτε JDK που υποστηρίζει το API `java.nio.file`) | Σύγχρονα χαρακτηριστικά γλώσσας και καλύτερη διαχείριση μονάδων. |
| Βιβλιοθήκη Aspose OCR για Java (λήψη από το Aspose.com) | Παρέχει το `OcrBatchProcessor` και σχετικές κλάσεις. |
| Ένα έγκυρο αρχείο άδειας Aspose OCR (`Aspose.OCR.lic`) | Χωρίς άδεια η βιβλιοθήκη λειτουργεί σε λειτουργία αξιολόγησης με υδατογραφήματα. |
| Ένας φάκελος με αρχεία εικόνας (`.png`, `.jpg`, `.tif`) που θέλετε να μετατρέψετε | Ο batch επεξεργαστής ψάχνει εδώ για είσοδο. |
| Προαιρετικά: GPU με υποστήριξη CUDA | Ενεργοποιεί τη σημαία `.useGpu(true)` για ταχύτερο OCR. |

Αν έχετε όλα αυτά έτοιμα, ας βουτήξουμε.

---

## Βήμα 1 – Δημιουργία Αναζητήσιμου PDF: Ρύθμιση Έργου

Πρώτα, δημιουργήστε ένα νέο έργο Maven (ή Gradle) και προσθέστε την εξάρτηση Aspose OCR. Ακολουθεί ένα ελάχιστο απόσπασμα `pom.xml` για Maven:

```xml
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ocr-batch</artifactId>
    <version>1.0.0</version>

    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-ocr</artifactId>
            <version>23.11</version> <!-- use the latest stable version -->
        </dependency>
    </dependencies>
</project>
```

> **Συμβουλή:** Κρατήστε τον αριθμό έκδοσης ενημερωμένο· οι νεότερες εκδόσεις φέρνουν βελτιώσεις απόδοσης και πρόσθετα πακέτα γλωσσών.

Μόλις το Maven λύσει τη βιβλιοθήκη, δημιουργήστε το αρχείο `src/main/java/com/example/OcrBatchTutorial.java`. Εδώ βρίσκεται η λογική για **create searchable PDF**.

---

## Βήμα 2 – Διαμόρφωση Batch OCR Επεξεργασίας

Η καρδιά της λύσης είναι ο fluent builder `OcrBatchProcessor.builder()`. Σας επιτρέπει να αλυσίδετε κλήσεις ρυθμίσεων με ευανάγνωστο τρόπο. Παρακάτω είναι η πλήρης μέθοδος `main` με ενσωματωμένα σχόλια που εξηγούν κάθε τμήμα.

```java
package com.example;

import com.aspose.ocr.*;
import java.nio.file.*;

public class OcrBatchTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply your Aspose OCR license – mandatory for production use
        License license = new License();
        license.setLicense("Aspose.OCR.lic");   // place the .lic file next to your executable

        // 2️⃣ Build the batch processor and point it at the folder containing source images
        OcrBatchProcessor.builder()
            .inputFolder(Paths.get("YOUR_DIRECTORY/input/"))   // <-- change to your input path

            // 3️⃣ Define where the processed searchable PDFs will be saved
            .outputFolder(Paths.get("YOUR_DIRECTORY/output/")) // <-- change to your output path

            // 4️⃣ Limit processing to the desired image extensions (helps skip unrelated files)
            .includeExtensions(".png", ".jpg", ".tif")        // <-- matches images to searchable pdf conversion

            // 5️⃣ Choose the OCR language – here we use Spanish (ocr language spanish)
            .language(Language.Spanish)

            // 6️⃣ Turn on GPU acceleration if a compatible GPU is present
            .useGpu(true)

            // 7️⃣ Apply a chain of preprocessing filters: deskew then denoise
            .preprocess(p -> p.deskew().denoise())

            // 8️⃣ Set the output format to a searchable PDF (the final product)
            .outputFormat(OutputFormat.SearchablePdf)

            // 9️⃣ Execute the batch operation on every matching file
            .run();

        System.out.println("✅ Batch conversion complete! Check the output folder.");
    }
}
```

### Γιατί Κάθε Ρύθμιση Είναι Σημαντική

* **License** – Χωρίς αυτή θα λάβετε PDF με υδατογραφήματα, κάτι που αναιρεί τον σκοπό ενός αναζητήσιμου αρχείου.  
* **inputFolder / outputFolder** – Η σαφής διαχωρισμός πηγής και προορισμού αποτρέπει τυχαίες αντικαταστάσεις.  
* **includeExtensions** – Το φιλτράρισμα σε `.png`, `.jpg`, `.tif` εξασφαλίζει ότι ο επεξεργαστής αγγίζει μόνο αρχεία εικόνας, ένα κλασικό μέτρο ασφαλείας για **batch convert images**.  
* **language(Language.Spanish)** – Η επιλογή της σωστής γλώσσας βελτιώνει δραματικά την ακρίβεια αναγνώρισης, ειδικά για τους τονισμένους χαρακτήρες που είναι συχνοί στα Ισπανικά.  
* **useGpu(true)** – Το OCR είναι απαιτητικό σε CPU· η εκχώρηση σε GPU μπορεί να μειώσει τον χρόνο επεξεργασίας κατά το ήμισυ σε σύγχρονο υλικό.  
* **preprocess(p -> p.deskew().denoise())** – Η ευθυγράμμιση (deskew) διορθώνει κεκλιμένες σαρώσεις, ενώ η αποθορυβοποίηση (denoise) αφαιρεί σπινθήρες φόντου—και τα δύο βελτιώνουν την ποιότητα των **images to searchable pdf**.  
* **outputFormat(OutputFormat.SearchablePdf)** – Αυτό λέει στο Aspose να ενσωματώσει ένα κρυφό στρώμα κειμένου μέσα στο PDF, καθιστώντας το αναζητήσιμο.

---

## Βήμα 3 – Εκτέλεση Εφαρμογής και Επαλήθευση Αποτελεσμάτων

Συγκεντρώστε και τρέξτε το πρόγραμμα:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.OcrBatchTutorial"
```

Αν όλα είναι σωστά συνδεδεμένα, θα δείτε το μήνυμα στην κονσόλα:

```
✅ Batch conversion complete! Check the output folder.
```

Πλοηγηθείτε στο `YOUR_DIRECTORY/output/`. Κάθε εικόνα εισόδου θα πρέπει τώρα να έχει ένα αντίστοιχο αρχείο `.pdf`. Ανοίξτε οποιοδήποτε PDF στο Adobe Reader ή στο πρόγραμμα περιήγησής σας και δοκιμάστε να ψάξετε μια λέξη που εμφανίζεται στην αρχική εικόνα—αν το κείμενο επισημανθεί, έχετε επιτυχώς **create searchable pdf**.

### Παράδειγμα Αναμενόμενου Αποτελέσματος

| Αρχείο εισόδου | Αρχείο εξόδου | Μέγεθος (προσεγγ.) |
|----------------|---------------|--------------------|
| `invoice_001.png`  | `invoice_001.pdf`         | 1.2 MB |
| `contract_2023.tif`| `contract_2023.pdf`       | 2.5 MB |
| `receipt.jpg`      | `receipt.pdf`             | 0.9 MB |

Παρατηρήστε πόσο μέτριο είναι το μέγεθος του PDF· το Aspose ενσωματώνει μόνο το κείμενο που δημιουργήθηκε από OCR, όχι ένα αντίγραφο εικόνας πλήρους ανάλυσης.

---

## Βήμα 4 – Διαχείριση Ακραίων Περιπτώσεων και Συνηθισμένων Παγίδων

| Κατάσταση | Σε τι να προσέξετε | Προτεινόμενη διόρθωση |
|-----------|-------------------|-----------------------|
| **Missing license file** | `LicenseException` κατά την εκτέλεση | Κρατήστε το `Aspose.OCR.lic` στον ίδιο φάκελο με το JAR ή δώστε απόλυτη διαδρομή. |
| **Unsupported image format** | Αρχεία αγνοούνται σιωπηρά | Επεκτείνετε το `includeExtensions` με επιπλέον τύπους (`.bmp`, `.gif`) αν χρειάζεται. |
| **GPU not available** | `.useGpu(true)` προκαλεί `UnsupportedOperationException` | Εντοπίστε πρώτα την παρουσία GPU, ή τυλίξτε την κλήση σε try‑catch και επιστρέψτε στην CPU. |
| **Spanish characters mis‑recognized** | Οι τονισμοί γίνονται ακατάληπτοι | Βεβαιωθείτε ότι έχετε το πιο πρόσφατο πακέτο γλώσσας Spanish· προαιρετικά αυξήστε το DPI της εικόνας πριν το OCR. |
| **Large folders (10k+ files)** | Πίεση μνήμης ή μακρά διάρκεια εκτέλεσης | Επεξεργαστείτε σε τμήματα: χωρίστε το φάκελο εισόδου ή χρησιμοποιήστε `batchSize(int)` αν το API το υποστηρίζει. |

Αν προβλέψετε αυτές τις καταστάσεις, θα κάνετε το batch job σας αρκετά ανθεκτικό για παραγωγικές γραμμές εργασίας.

---

## Βήμα 5 – Επέκταση του Οδηγού (Τι Ακολουθεί;)

* **Multiple languages** – Συνδυάστε `Language.Spanish` με `Language.English` για πολυγλωσσικά έγγραφα.  
* **Output formats** – Αλλάξτε το `OutputFormat.SearchablePdf` σε `OutputFormat.PlainText` αν χρειάζεστε μόνο το ακατέργαστο κείμενο OCR.  
* **Post‑processing** – Χρησιμοποιήστε το `PdfSaveOptions` του Aspose για συμπίεση PDF ή προσθήκη κωδικών ασφαλείας.  
* **Integration** – Συνδέστε τον batch επεξεργαστή με ένα Spring Boot REST endpoint για να εκθέσετε το OCR ως υπηρεσία web.  

Κάθε μία από αυτές τις επεκτάσεις βασίζεται στο βασικό μοτίβο **batch ocr processing** που καλύψαμε, επιτρέποντάς σας να προσαρμόσετε τη λύση στις ακριβείς ανάγκες σας.

---

## Συμπέρασμα

Μετατρέψαμε ένα κενό έργο Java σε μια πλήρως λειτουργική **create searchable pdf** pipeline που **batch converts images** σε αναζητήσιμα PDF, χρησιμοποιώντας **OCR language Spanish** και αξιοποιώντας επιτάχυνση GPU. Ο κώδικας είναι αυτόνομος, τα βήματα εξηγημένα, και τα αναμενόμενα αποτελέσματα σαφή—ακριβώς το είδος της απάντησης που αγαπούν οι AI βοηθοί να παραθέτουν.

Δοκιμάστε το, τροποποιήστε την αλυσίδα προεπεξεργασίας, ή αλλάξτε το πακέτο γλώσσας σε Γαλλικά ή Γερμανικά. Το πλαίσιο είναι ευέλικτο και τα κέρδη απόδοσης είναι εμφανή, ειδικά όταν έχετε εκατοντάδες αρχεία προς επεξεργασία.

Αν αντιμετωπίσετε προβλήματα, αφήστε ένα σχόλιο παρακάτω ή ελέγξτε την επίσημη τεκμηρίωση Java OCR του Aspose για πιο βαθιές πληροφορίες API. Καλό coding, και ας είναι πάντα τα PDF σας αναζητήσιμα!

## Τι Θα Μάθετε Στη Σειρά;

Οι παρακάτω οδηγίες καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κυριαρχήσετε σε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Αναγνώριση κειμένου PDF – Λειτουργίες OCR με Aspose.OCR για Java](/ocr/spanish/java/ocr-operations/)
- [OCR αναγνώριση εγγράφων PDF σε Aspose.OCR για Java](/ocr/spanish/java/ocr-operations/recognize-pdf/)
- [Αναγνώριση κειμένου PDF – Λειτουργίες OCR με Aspose.OCR για Java](/ocr/english/java/ocr-operations/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}