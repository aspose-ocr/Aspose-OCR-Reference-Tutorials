---
category: general
date: 2026-04-26
description: Δημιουργήστε αναζητήσιμο PDF από εικόνα χρησιμοποιώντας το Aspose OCR
  σε Java. Μάθετε πώς να μετατρέπετε εικόνα σε PDF, να κάνετε OCR εικόνας σε PDF και
  να εξάγετε κείμενο από την εικόνα γρήγορα.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- ocr image to pdf
- extract text from image
- how to set language
language: el
og_description: Δημιουργήστε PDF με δυνατότητα αναζήτησης από μια εικόνα χρησιμοποιώντας
  το Aspose OCR. Αυτός ο οδηγός δείχνει πώς να μετατρέψετε την εικόνα σε PDF, να κάνετε
  OCR στην εικόνα σε PDF και να εξάγετε κείμενο από την εικόνα.
og_title: Δημιουργία PDF με δυνατότητα αναζήτησης από εικόνα με Java OCR
tags:
- Java
- OCR
- PDF
title: Δημιουργία αναζητήσιμου PDF από εικόνα με Java OCR
url: /el/java/ocr-operations/create-searchable-pdf-from-image-with-java-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία αναζητήσιμου PDF από εικόνα με Java OCR

Έχετε ποτέ χρειαστεί να **create searchable PDF** από ένα σαρωμένο τιμολόγιο αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είστε ο μόνος—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το εμπόδιο όταν θέλουν ένα PDF που μπορείτε πραγματικά να αναζητήσετε. Τα καλά νέα; Με το Aspose OCR for Java μπορείτε να **convert image to PDF**, να εκτελέσετε OCR άμεσα, και να καταλήξετε με ένα τακτοποιημένο αναζητήσιμο αρχείο σε λίγες μόνο γραμμές κώδικα.

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία: φόρτωση μιας εικόνας, ενημέρωση της μηχανής για τη γλώσσα που αναμένεται, εκτέλεση OCR, και τελικά αποθήκευση ενός **searchable PDF**. Στο τέλος θα ξέρετε επίσης πώς να **extract text from image** χειροκίνητα, να ρυθμίσετε τις ρυθμίσεις γλώσσας, και να αντιμετωπίσετε μερικές κοινές περιπτώσεις. Χωρίς εξωτερικές υπηρεσίες, χωρίς ασαφή εργαλεία γραμμής εντολών—απλώς καθαρή Java.

## Τι θα χρειαστείτε

- Java 17 ή νεότερο (το API λειτουργεί και με παλαιότερες εκδόσεις, αλλά το 17 είναι η ιδανική επιλογή).  
- Βιβλιοθήκη Aspose OCR for Java – μπορείτε να κατεβάσετε το τελευταίο JAR από το Maven Central (`com.aspose:aspose-ocr:23.10`).  
- Ένα αρχείο εικόνας που περιέχει αναγνώσιμο κείμενο (λειτουργεί PNG, JPG ή TIFF).  
- Μια μικρή δόση υπομονής στο IDE—IntelliJ IDEA ή VS Code αρκούν.

Αν τα έχετε ήδη, τέλεια! Αν όχι, το παρακάτω απόσπασμα Maven θα σας βοηθήσει να ξεκινήσετε:

```xml
<!-- Add to your pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

Τώρα που η βάση είναι έτοιμη, ας βουτήξουμε στον κώδικα.

## Βήμα 1: Αρχικοποίηση της μηχανής OCR – η καρδιά του **create searchable pdf**

Πριν ξεκινήσει οποιαδήποτε μετατροπή, πρέπει να δημιουργήσετε μια παρουσία `OcrEngine`. Σκεφτείτε το ως τον εγκέφαλο που θα διαβάσει τα pixel και θα τα μετατρέψει σε χαρακτήρες.

```java
import com.aspose.ocr.*;

public class PdfExportDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

*Γιατί είναι σημαντικό:* Η μηχανή κρατά όλες τις ρυθμίσεις αναγνώρισης (γλώσσα, λειτουργία ακρίβειας κ.λπ.). Η δημιουργία της μία φορά και η επαναχρησιμοποίησή της σε πολλές εικόνες είναι πιο αποδοτική από το να δημιουργείτε νέα μηχανή για κάθε αρχείο.

## Βήμα 2: **How to set language** – βελτιώστε την ακρίβεια για Γαλλικά, Γερμανικά ή οποιοδήποτε σύστημα γραφής

Αν γνωρίζετε τη γλώσσα του αρχικού εγγράφου, ενημερώστε τη μηχανή OCR. Αυτό επιταχύνει την επεξεργασία και μειώνει τις λανθασμένες αναγνώσεις.

```java
        // Step 2: (Optional) Specify the language to improve text extraction
        ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.FRENCH);
```

Μπορείτε να αντικαταστήσετε το `OcrLanguage.FRENCH` με `ENGLISH`, `SPANISH`, `GERMAN`, κ.λπ. Όταν δεν είστε σίγουροι, παραλείψτε τη γραμμή και αφήστε το Aspose να μαντέψει—αλλά περιμένετε μια μικρή πτώση στην ακρίβεια.

## Βήμα 3: Φορτώστε την εικόνα που θέλετε να **convert image to pdf**

Η μέθοδος `setImage` δέχεται διαδρομή αρχείου, `InputStream`, ή ακόμη και αντικείμενο `java.awt.Image`. Αν έχετε έναν πίνακα byte (π.χ., από ανέβασμα στο web), τυλίξτε τον σε `ByteArrayInputStream` και περάστε τον απευθείας.

```java
        // Step 3: Load the image that contains the text to be recognized
        ocrEngine.setImage("YOUR_DIRECTORY/french_invoice.png");
```

## Βήμα 4: Εκτελέστε OCR και **ocr image to pdf** σε μία κλήση

Το Aspose κάνει αυτό το βήμα απλό: το `recognizeToPdf` εκτελεί τη μηχανή αναγνώρισης και γράφει ένα αναζητήσιμο PDF σε μία ενέργεια.

```java
        // Step 4: Recognize the text and save it as a searchable PDF
        ocrEngine.recognizeToPdf("YOUR_DIRECTORY/french_invoice_searchable.pdf");
```

Πίσω από τη σκηνή, η βιβλιοθήκη δημιουργεί ένα αόρατο στρώμα κειμένου που ευθυγραμμίζεται με την αρχική εικόνα. Όταν ανοίξετε το παραγόμενο αρχείο στο Adobe Reader, θα μπορείτε να πληκτρολογήσετε μια λέξη στο πεδίο αναζήτησης και άμεσα να μεταβείτε στη θέση που ταιριάζει.

## Βήμα 5: Επαλήθευση του αποτελέσματος – πώς φαίνεται η έξοδος;

```java
        // Step 5: Inform the user that the PDF has been created
        System.out.println("Searchable PDF generated.");
    }
}
```

Εκτελέστε το πρόγραμμα, μετά ανοίξτε το `french_invoice_searchable.pdf`. Δοκιμάστε να αναζητήσετε μια λέξη που γνωρίζετε ότι εμφανίζεται στο τιμολόγιο (π.χ., “Total”). Αν η επισήμανση εμφανιστεί στη σωστή θέση, έχετε δημιουργήσει επιτυχώς **create searchable pdf**.  
![Create searchable PDF example](example.png)<!-- alt text includes primary keyword -->

### Αναμενόμενη έξοδος

```
Searchable PDF generated.
```

Και ένα αρχείο PDF στο `YOUR_DIRECTORY` που μπορείτε να μοιραστείτε, να καταχωρίσετε ή να αρχειοθετήσετε.

## Βήμα 6: Εξαγωγή ακατέργαστου κειμένου από την εικόνα (προαιρετικό)

Μερικές φορές χρειάζεστε το απλό κείμενο για περαιτέρω επεξεργασία—ίσως για να το εισάγετε σε βάση δεδομένων ή να εκτελέσετε ανάλυση συναισθήματος. Το Aspose σας επιτρέπει να εξάγετε το αναγνωρισμένο κείμενο άμεσα:

```java
        // Optional: Get the extracted text as a String
        String extractedText = ocrEngine.getText();
        System.out.println("Extracted text:");
        System.out.println(extractedText);
```

Αυτό το απόσπασμα δείχνει **extract text from image** χωρίς δημιουργία PDF. Είναι χρήσιμο όταν σας ενδιαφέρει μόνο το περιεχόμενο, όχι η οπτική διάταξη.

## Διαχείριση πολλαπλών σελίδων ή εικόνων

Τι γίνεται αν η πηγή σας είναι ένα multi‑page TIFF ή ένας φάκελος με JPEG; Μπορείτε να κάνετε βρόχο στα αρχεία και να καλέσετε `recognizeToPdf` για το καθένα, έπειτα να συγχωνεύσετε τα PDFs χρησιμοποιώντας το Aspose PDF ή οποιαδήποτε άλλη βιβλιοθήκη. Εδώ είναι ένα γρήγορο παράδειγμα:

```java
import java.io.File;
import com.aspose.pdf.*;

public class MultiPageDemo {
    public static void main(String[] args) throws Exception {
        OcrEngine engine = new OcrEngine();
        File folder = new File("YOUR_DIRECTORY/images");
        Document finalDoc = new Document();

        for (File img : folder.listFiles((d, n) -> n.matches(".*\\.(png|jpg|tif)"))) {
            engine.setImage(img.getAbsolutePath());
            // Save each page as a temporary PDF
            String tempPdf = img.getName() + ".pdf";
            engine.recognizeToPdf(tempPdf);
            // Append to final document
            Document pageDoc = new Document(tempPdf);
            finalDoc.getPages().add(pageDoc.getPages().get_Item(1));
        }
        finalDoc.save("YOUR_DIRECTORY/combined_searchable.pdf");
        System.out.println("All pages merged into searchable PDF.");
    }
}
```

**Pro tip:** Διαγράψτε τα προσωρινά PDFs μετά τη συγχώνευση για να διατηρήσετε τον χώρο εργασίας καθαρό.

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

- **Low‑resolution images:** Η ακρίβεια του OCR μειώνεται δραματικά κάτω από 150 dpi. Αυξήστε την ανάλυση ή ζητήστε σάρωση υψηλότερης ανάλυσης αν είναι δυνατόν.  
- **Skewed pages:** Μια περιστραμμένη εικόνα μπορεί να μπερδέσει τη μηχανή. Χρησιμοποιήστε `ocrEngine.getImagePreprocessingSettings().setDeskew(true)` για αυτόματη διόρθωση ήπιας κλίσης.  
- **Unsupported language:** Βεβαιωθείτε ότι η γλώσσα που ορίσατε περιλαμβάνεται στην άδεια Aspose OCR· διαφορετικά η μηχανή θα επιστρέψει στην αγγλική.  
- **Large files:** Η επεξεργασία ενός 30‑MB TIFF μπορεί να απαιτεί πολύ μνήμη. Σκεφτείτε να το χωρίσετε σε μικρότερα τμήματα ή να αυξήσετε τη μνήμη heap της JVM (`-Xmx2g`).

## Επόμενα βήματα – πού να πάτε από εδώ

Τώρα που έχετε κατακτήσει τα βασικά του **create searchable pdf**, ίσως θέλετε να εξερευνήσετε:

- **Batch conversion:** Συνδυάστε το μοτίβο multi‑page με έναν χρονοπρογραμματιστή για να επεξεργάζεστε τις εισερχόμενες σάρωσες καθημερινά τη νύχτα.  
- **Metadata injection:** Χρησιμοποιήστε το Aspose PDF για να προσθέσετε τίτλο, συγγραφέα ή προσαρμοσμένες ετικέτες στο αναζητήσιμο PDF.  
- **Digital signatures:** Ασφαλίστε το PDF με πιστοποιητικό μετά το OCR, εξασφαλίζοντας συμμόρφωση για νομικά έγγραφα.  

Όλες αυτές οι επεκτάσεις βασίζονται ακόμα στις βασικές έννοιες που καλύψαμε: αρχικοποίηση της μηχανής OCR, προαιρετική ρύθμιση της γλώσσας, φόρτωση της εικόνας, και κλήση του `recognizeToPdf`.

---

### TL;DR

Διασχίσαμε ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει πώς να **create searchable PDF** από μια εικόνα χρησιμοποιώντας το Aspose OCR for Java. Τα βήματα περιλαμβάνουν την αρχικοποίηση της μηχανής, την προαιρετική ρύθμιση της γλώσσας (απαντώντας στο “how to set language”), τη φόρτωση της εικόνας, την εκτέλεση OCR, την αποθήκευση ενός αναζητήσιμου PDF, και την προαιρετική εξαγωγή απλού κειμένου. Επίσης καλύψαμε τη διαχείριση πολλαπλών σελίδων, κοινά προβλήματα, και ιδέες για περαιτέρω αυτοματοποίηση.

Δοκιμάστε το με τις δικές σας αποδείξεις, συμβόλαια ή χειρόγραφες σημειώσεις—μετατρέψτε αυτές τις στατικές εικόνες σε πλήρως αναζητήσιμα έγγραφα σε δευτερόλεπτα. Καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}