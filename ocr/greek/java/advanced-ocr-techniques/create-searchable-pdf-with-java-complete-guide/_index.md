---
category: general
date: 2026-03-18
description: Δημιουργήστε αναζητήσιμο PDF από σαρωμένα αρχεία χρησιμοποιώντας το Aspose
  OCR. Μάθετε πώς να μετατρέψετε σαρωμένο PDF, να ορίσετε την ανάλυση του PDF και
  να κατακτήσετε τη μετατροπή PDF σε αναζητήσιμο.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- how to convert pdf
- convert pdf to searchable
- set pdf resolution
language: el
og_description: Δημιουργήστε αναζητήσιμο PDF από σαρωμένα αρχεία χρησιμοποιώντας το
  Aspose OCR. Αυτό το σεμινάριο δείχνει πώς να μετατρέψετε σαρωμένο PDF, να ορίσετε
  την ανάλυση του PDF και να λάβετε ένα αναζητήσιμο αποτέλεσμα.
og_title: Δημιουργία Αναζητήσιμου PDF με Java – Πλήρης Οδηγός
tags:
- Java
- OCR
- PDF
- Aspose
title: Δημιουργία Αναζητήσιμου PDF με Java – Πλήρης Οδηγός
url: /el/java/advanced-ocr-techniques/create-searchable-pdf-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Αναζητήσιμου PDF με Java – Πλήρης Οδηγός

Έχετε χρειαστεί ποτέ να **δημιουργήσετε αναζητήσιμο PDF** από μια στοίβα σαρωμένων εγγράφων αλλά δεν ήξερατε από πού να ξεκινήσετε; Δεν είστε οι μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν προσπαθούν να μετατρέψουν PDFs μόνο με εικόνες σε αρχεία με δυνατότητα αναζήτησης κειμένου. Τα καλά νέα; Με μερικές γραμμές Java και τη βιβλιοθήκη Aspose OCR, μπορείτε να **μετατρέψετε σαρωμένο PDF** σε αναζητήσιμο PDF σε δευτερόλεπτα.  

Σε αυτό το tutorial θα περάσουμε από όλα όσα χρειάζεται να γνωρίζετε: από την εγκατάσταση της βιβλιοθήκης, τη ρύθμιση της ανάλυσης, μέχρι την πραγματική εκτέλεση της μετατροπής. Στο τέλος, θα μπορείτε να **δημιουργήσετε αναζητήσιμα PDF** αρχεία που οι χρήστες σας μπορούν να αναζητήσουν, αντιγράψουν και ευρετηριάσουν χωρίς καν κόπο. Χωρίς περιττές πληροφορίες, μόνο ένα πρακτικό, εκτελέσιμο παράδειγμα.

## Τι Θα Χρειαστείτε

- Java 17 ή νεότερο (ο κώδικας χρησιμοποιεί τη σύγχρονη σύνταξη `var`, αλλά μπορείτε να υποβαθμίσετε αν χρειαστεί)
- Maven ή Gradle για να κατεβάσετε την εξάρτηση Aspose OCR
- Ένα σαρωμένο αρχείο PDF (οποιοδήποτε έγγραφο πολλαπλών σελίδων αρκεί)
- Ένα IDE ή κειμενογράφο της επιλογής σας—το IntelliJ IDEA λειτουργεί εξαιρετικά, αλλά το Eclipse είναι επίσης εντάξει

Η προετοιμασία αυτών των προαπαιτήσεων θα διασφαλίσει ομαλή ροή—χωρίς διακοπές στη μέση.

## Βήμα 1: Προσθήκη Aspose OCR στο Έργο σας

Πρώτα, πρέπει να φέρουμε τη μηχανή OCR στην κλάση‑διαδρομή. Αν χρησιμοποιείτε Maven, προσθέστε το παρακάτω στο `pom.xml` σας:

```xml
<!-- Aspose OCR for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- latest as of 2026 -->
</dependency>
```

Οι χρήστες Gradle μπορούν να προσθέσουν:

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

> **Pro tip:** Πάντα ελέγχετε το επίσημο αποθετήριο Aspose Maven για την πιο πρόσφατη έκδοση· οι νεότερες κυκλοφορίες μπορεί να περιλαμβάνουν βελτιώσεις απόδοσης για PDF υψηλής ανάλυσης.

## Βήμα 2: Αρχικοποίηση της Μηχανής OCR

Τώρα που η βιβλιοθήκη είναι διαθέσιμη, δημιουργούμε μια παρουσία του `OcrEngine`. Σκεφτείτε αυτό το αντικείμενο ως τον εγκέφαλο που θα διαβάσει τις rasterized σελίδες και θα μετατρέψει τα pixel σε κείμενο.

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.PdfRecognitionOptions;

/**
 * Demonstrates how to create a searchable PDF from a scanned source.
 */
public class PdfToSearchableDemo {

    public static void main(String[] args) throws Exception {
        // Step 2: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

Γιατί χρειάζεται μια ρητή μηχανή; Επειδή η Aspose διαχωρίζει τη λογική OCR από τη λογική διαχείρισης αρχείων, δίνοντάς σας λεπτομερή έλεγχο σε στοιχεία όπως πακέτα γλώσσας και λειτουργίες αναγνώρισης.

## Βήμα 3: Ρύθμιση Ανάλυσης PDF – **set pdf resolution**

Η ανάλυση είναι τα DPI (σημεία ανά ίντσα) που χρησιμοποιούνται όταν η βιβλιοθήκη rasterizes κάθε σελίδα PDF πριν την περάσει στη μηχανή OCR. Υψηλότερα DPI προσφέρουν καλύτερη ακρίβεια κειμένου αλλά καταναλώνουν περισσότερη μνήμη και χρόνο CPU.

```java
        // Step 3: Configure PDF recognition options
        PdfRecognitionOptions pdfOptions = new PdfRecognitionOptions();
        pdfOptions.setPageRange(1, 5);      // optional: process pages 1‑5 only
        pdfOptions.setResolution(300);     // 300 DPI is a sweet spot for most scans
```

Αν εργάζεστε με μικρές, χαμηλής ποιότητας σαρώσεις, αυξήστε την ανάλυση στα 400 DPI· για τεράστια έγγραφα όπου η ταχύτητα μετράει, 200 DPI μπορεί να είναι αρκετό. Η κλήση `setPageRange` είναι προαιρετική—παραλείψτε την για να επεξεργαστείτε ολόκληρο το αρχείο.

## Βήμα 4: Μετατροπή Σαρωμένου PDF σε Αναζητήσιμο PDF – **convert scanned pdf**

Εδώ είναι η ουσία. Η μέθοδος `convertPdfToSearchablePdf` δέχεται τρία ορίσματα: τη διαδρομή προέλευσης, τη διαδρομή προορισμού και τις επιλογές που μόλις ορίσαμε.

```java
        // Step 4: Convert the scanned PDF into a searchable PDF
        ocrEngine.convertPdfToSearchablePdf(
                "YOUR_DIRECTORY/scanned.pdf",      // input scanned PDF
                "YOUR_DIRECTORY/searchable.pdf",   // output searchable PDF
                pdfOptions);
```

Όταν εκτελείται αυτή η γραμμή, η Aspose rasterizes κάθε σελίδα, εκτελεί OCR και ενσωματώνει ένα αόρατο στρώμα κειμένου ακριβώς πάνω στην αρχική εικόνα. Το παραγόμενο αρχείο φαίνεται πανομοιότυπο με το αρχικό, αλλά τώρα μπορείτε να αναζητήσετε οποιαδήποτε λέξη μέσα του.

## Βήμα 5: Επαλήθευση του Αποτελέσματος

Ένα γρήγορο `System.out.println` σας λέει πού αποθηκεύτηκε το αρχείο. Μετά το τέλος του προγράμματος, ανοίξτε το αποτέλεσμα σε οποιονδήποτε αναγνώστη PDF και δοκιμάστε την ενσωματωμένη αναζήτηση (Ctrl + F). Θα πρέπει να δείτε αντιστοιχίες παρόλο που το αρχικό PDF ήταν μόνο μια εικόνα.

```java
        // Step 5: Notify the user
        System.out.println("Searchable PDF created at YOUR_DIRECTORY/searchable.pdf");
    }
}
```

**Αναμενόμενη έξοδος κονσόλας**

```
Searchable PDF created at YOUR_DIRECTORY/searchable.pdf
```

Και όταν πληκτρολογήσετε μια λέξη που υπάρχει στις σαρωμένες σελίδες, ο προβολέας θα την επισημάνει—απόδειξη ότι δημιουργήσατε επιτυχώς **αναζητήσιμο pdf**.

## Βήμα 6: Προαιρετικό – Πώς να Μετατρέψετε PDF Όταν Χρειάζεστε Μόνο Ορισμένες Σελίδες

Μερικές φορές θέλετε να κάνετε αναζητήσιμο μόνο ένα υποσύνολο (π.χ., τις πρώτες δέκα σελίδες ενός συμβολαίου 200 σελίδων). Απλώς προσαρμόστε την κλήση `setPageRange`:

```java
pdfOptions.setPageRange(1, 10); // process only pages 1‑10
```

Όλα τα άλλα παραμένουν ίδια. Αυτή η μικρή προσαρμογή μπορεί να εξοικονομήσει ώρες χρόνου επεξεργασίας σε τεράστια αρχεία.

## Βήμα 7: Καλές Πρακτικές για τη Μετατροπή PDF σε Αναζητήσιμη Μορφή

- **Batch processing:** Τυλίξτε τον κώδικα μετατροπής σε βρόχο αν έχετε δεκάδες αρχεία. Θυμηθείτε να επαναχρησιμοποιείτε την ίδια παρουσία `OcrEngine` για να μειώσετε το κόστος.
- **Memory management:** Για πολύ μεγάλα PDF, σκεφτείτε να αυξήσετε τη μνήμη heap της JVM (`-Xmx2g` ή περισσότερο) ώστε να αποφύγετε `OutOfMemoryError`.
- **Language support:** Από προεπιλογή η Aspose OCR ανιχνεύει Αγγλικά. Αν τα έγγραφά σας είναι στα Ισπανικά, Γαλλικά ή άλλη γλώσσα, φορτώστε το κατάλληλο πακέτο γλώσσας μέσω `ocrEngine.getLanguage().add(Language.Spanish);`.
- **Post‑processing:** Μετά τη μετατροπή, ίσως θέλετε να συμπιέσετε το PDF (`PdfSaveOptions.setCompressionLevel`) για να μειώσετε το μέγεθος του αρχείου χωρίς να χάσετε το κρυφό στρώμα κειμένου.

## Οπτική Επισκόπηση

Παρακάτω υπάρχει ένα απλό διάγραμμα που δείχνει τη ροή από ένα σαρωμένο PDF σε ένα αναζητήσιμο PDF. Το κείμενο alt περιλαμβάνει τη βασική λέξη-κλειδί, βοηθώντας τόσο τις μηχανές αναζήτησης όσο και τα μοντέλα AI να κατανοήσουν το περιεχόμενο της εικόνας.

![Create searchable PDF example](https://example.com/images/create-searchable-pdf.png "create searchable pdf workflow")

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.PdfRecognitionOptions;

/**
 * Complete, runnable example that demonstrates how to create a searchable PDF
 * from a scanned PDF using Aspose OCR for Java.
 */
public class PdfToSearchableDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Configure PDF recognition options
        PdfRecognitionOptions pdfOptions = new PdfRecognitionOptions();
        pdfOptions.setPageRange(1, 5);      // optional: limit to pages 1‑5
        pdfOptions.setResolution(300);     // set PDF resolution (DPI)

        // Convert the scanned PDF into a searchable PDF
        ocrEngine.convertPdfToSearchablePdf(
                "YOUR_DIRECTORY/scanned.pdf",
                "YOUR_DIRECTORY/searchable.pdf",
                pdfOptions);

        // Notify the user
        System.out.println("Searchable PDF created at YOUR_DIRECTORY/searchable.pdf");
    }
}
```

Εκτελέστε την κλάση, ορίστε τις διαδρομές στα πραγματικά σας αρχεία και παρακολουθήστε τη μαγεία. Δεν απαιτείται πρόσθετη διαμόρφωση για μια βασική μετατροπή.

## Συμπέρασμα

Τώρα ξέρετε ακριβώς **πώς να δημιουργήσετε αναζητήσιμα PDF** αρχεία από σαρωμένες πηγές χρησιμοποιώντας Java και Aspose OCR. Τα βήματα—εγκατάσταση της βιβλιοθήκης, αρχικοποίηση της μηχανής, ρύθμιση της ανάλυσης και κλήση του `convertPdfToSearchablePdf`—είναι απλά, και ο κώδικας είναι έτοιμος να ενσωματωθεί σε οποιοδήποτε έργο.

Αν είστε έτοιμοι να **μετατρέψετε σαρωμένα pdf** αρχεία μαζικά, εξερευνήστε τις συμβουλές batch‑processing παραπάνω, ή εμβαθύνετε στις επιλογές **convert pdf to searchable** όπως πακέτα γλώσσας OCR και ρυθμίσεις συμπίεσης. Στη συνέχεια, ίσως θελήσετε να δείτε **πώς να μετατρέψετε pdf** σε άλλες μορφές (DOCX, HTML) ή να πειραματιστείτε με OCR για πολυγλωσσικά έγγραφα.

Καλό κώδικα, και εύχομαι τα PDF σας να είναι πάντα αναζητήσιμα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}