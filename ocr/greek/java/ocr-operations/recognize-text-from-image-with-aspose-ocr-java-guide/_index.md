---
category: general
date: 2026-06-19
description: Αναγνωρίστε κείμενο από εικόνα χρησιμοποιώντας το Aspose OCR σε Java
  και μάθετε πώς να μετατρέπετε εικόνα σε docx, να εξάγετε κείμενο από png και να
  μετατρέπετε σαρωμένη εικόνα σε υπολογιστικό φύλλο.
draft: false
keywords:
- recognize text from image
- convert image to docx
- extract text from png
- convert scanned image to spreadsheet
language: el
og_description: αναγνωρίστε κείμενο από εικόνα σε Java χρησιμοποιώντας το Aspose OCR.
  Ακολουθήστε αυτό το βήμα‑βήμα οδηγό για να μετατρέψετε την εικόνα σε docx, να εξάγετε
  κείμενο από png και να μετατρέψετε σαρωμένη εικόνα σε υπολογιστικό φύλλο.
og_title: Αναγνώριση κειμένου από εικόνα με Aspose OCR – Οδηγός Java
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: recognize text from image using Aspose OCR in Java and learn to convert
    image to docx, extract text from png, and convert scanned image to spreadsheet.
  headline: recognize text from image with Aspose OCR – Java guide
  type: TechArticle
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Αναγνώριση κειμένου από εικόνα με Aspose OCR – Οδηγός Java
url: /el/java/ocr-operations/recognize-text-from-image-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση κειμένου από εικόνα με Aspose OCR – οδηγός Java

Έχετε ποτέ χρειαστεί να **αναγνωρίσετε κείμενο από εικόνα** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη μπορεί να διαχειριστεί γερμανικά PDF, PNG και ακόμη να παράγει ένα υπολογιστικό φύλλο; Δεν είστε μόνοι. Σε αυτό το tutorial θα περάσουμε από ένα πλήρες παράδειγμα Java που όχι μόνο εξάγει τους χαρακτήρες αλλά επίσης **μετατρέπει εικόνα σε docx**, **εξάγει κείμενο από png**, και ακόμη **μετατρέπει σαρωμένη εικόνα σε υπολογιστικό φύλλο**—όλα με λίγες γραμμές.

Θα χρησιμοποιήσουμε το Aspose.OCR, μια εμπορική βιβλιοθήκη που παρέχει ένα απλό API. Μην ανησυχείτε αν δεν έχετε άδεια· η demo λειτουργεί σε λειτουργία αξιολόγησης, αν και ορισμένα χαρακτηριστικά (όπως η εξαγωγή υψηλής ανάλυσης) είναι περιορισμένα. Στο τέλος θα έχετε ένα εκτελέσιμο πρόγραμμα που παίρνει ένα στιγμιότυπο PNG μιας αναφοράς και παράγει αυτόματα αρχεία DOCX, XLSX και EPUB.

## Προαπαιτήσεις

* **Java Development Kit (JDK) 17** ή νεότερο εγκατεστημένο.
* **Aspose.OCR for Java** JAR (κατεβάστε από τον ιστότοπο της Aspose ή προσθέστε μέσω Maven).
* Ένα προαιρετικό αρχείο **Aspose.OCR.lic** αν θέλετε πλήρη λειτουργικότητα χωρίς υδατογράμματα αξιολόγησης.
* Ένα δείγμα εικόνας—ας το ονομάσουμε `report.png`—τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε από τον κώδικα.

Αν χρησιμοποιείτε Maven, προσθέστε αυτήν την εξάρτηση στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

Τώρα που η βάση είναι έτοιμη, ας ξεκινήσουμε.

## Βήμα 1: αναγνώριση κειμένου από εικόνα – εφαρμογή της άδειας (προαιρετικό)

Πρώτα απ' όλα, πρέπει να ενημερώσουμε το Aspose ότι διαθέτουμε άδεια. Η παράλειψη αυτού του βήματος δεν θα σπάσει τη demo, αλλά θα δείτε μια μικρή ένδειξη “Evaluation” στα αρχεία εξόδου.

```java
import com.aspose.ocr.*;

public class ExportDemo {
    public static void main(String[] args) throws Exception {
        // Apply the Aspose.OCR license (optional for full functionality)
        License license = new License();
        try {
            license.setLicense("Aspose.OCR.lic");
            System.out.println("License loaded successfully.");
        } catch (Exception e) {
            System.out.println("License not found – running in evaluation mode.");
        }
```

> **Pro tip:** Κρατήστε το αρχείο `.lic` δίπλα στο μεταγλωττισμένο JAR ή δείξτε σε απόλυτη διαδρομή· διαφορετικά η κλήση `setLicense` θα αποτύχει.

## Βήμα 2: αναγνώριση κειμένου από εικόνα – δημιουργία και ρύθμιση του OCR engine

Τώρα εκκινούμε τον OCR engine και του λέμε ποια γλώσσα περιμένουμε. Σε αυτό το παράδειγμα δουλεύουμε με Γερμανικά, αλλά το Aspose υποστηρίζει δεκάδες γλώσσες έτοιμες προς χρήση.

```java
        // Create an OCR engine and set the recognition language to German
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setLanguage(Language.German); // change to Language.English for English text
```

Γιατί να ορίσουμε τη γλώσσα; Ο engine χρησιμοποιεί λεξικά ειδικά για τη γλώσσα ώστε να βελτιώσει την ακρίβεια, ειδικά για χαρακτήρες όπως “ß” ή “ü”. Αν το παραλείψετε, θα λάβετε αποτελέσματα, αλλά θα είναι πιο «θορυβώδη».

## Βήμα 3: αναγνώριση κειμένου από εικόνα – τροφοδοσία του PNG και λήψη ακατέργαστων αποτελεσμάτων

Εδώ είναι η καρδιά της demo: δίνουμε στον engine μια διαδρομή σε αρχείο PNG και τον αφήνουμε να κάνει τη βαριά δουλειά.

```java
        // Recognize text from the input image
        String inputImagePath = "YOUR_DIRECTORY/report.png"; // <-- replace with your actual path
        OcrResult ocrResult = ocrEngine.recognizeImage(inputImagePath);
        System.out.println("OCR completed. Extracted " + ocrResult.getText().length() + " characters.");
```

Το αντικείμενο `OcrResult` περιέχει το ακατέργαστο Unicode string, καθώς και πληροφορίες διάταξης που μπορείτε να χρησιμοποιήσετε αργότερα αν χρειαστεί να διατηρήσετε τη μορφοποίηση. Αν η εικόνα είναι ένας σαρωμένος πίνακας, ο engine θα επιστρέψει ακόμη και απλό κείμενο—ιδανικό για το επόμενο βήμα όπου **μετατρέπουμε σαρωμένη εικόνα σε υπολογιστικό φύλλο**.

## Βήμα 4: μετατροπή εικόνας σε docx – αποθήκευση του αποτελέσματος ως έγγραφο Word

Το Aspose κάνει εξαιρετικά εύκολη την εξαγωγή του OCR output σε αρχείο DOCX. Αυτό είναι χρήσιμο όταν χρειάζεστε ένα επεξεργάσιμο έγγραφο Word για επόμενη επεξεργασία.

```java
        // Save the recognized text in DOCX format
        String outputDocxPath = "YOUR_DIRECTORY/report.docx";
        ocrResult.save(outputDocxPath, OutputFormat.Docx);
        System.out.println("Saved DOCX to " + outputDocxPath);
```

Πίσω από τις σκηνές, η βιβλιοθήκη δημιουργεί ένα απλό έγγραφο Word με μια παράγραφο που περιέχει το εξαγόμενο κείμενο. Αν χρειάζεστε πιο πλούσια μορφοποίηση (κεφαλίδες, πίνακες), μπορείτε να επεξεργαστείτε το DOCX αργότερα με Apache POI ή Aspose.Words.

## Βήμα 5: μετατροπή σαρωμένης εικόνας σε υπολογιστικό φύλλο – εξαγωγή σε XLSX

Μερικές φορές ένα σαρωμένο τιμολόγιο ή ένας οικονομικός πίνακας είναι πιο εύκολο να δουλέψει σε Excel. Το ίδιο `OcrResult` μπορεί να αποθηκευτεί ως αρχείο XLSX, και το Aspose θα προσπαθήσει να διατηρήσει τις δομές πινάκων όταν τις εντοπίσει.

```java
        // Save the same result in additional formats (XLSX, EPUB)
        String outputXlsxPath = "YOUR_DIRECTORY/report.xlsx";
        ocrResult.save(outputXlsxPath, OutputFormat.Xlsx);
        System.out.println("Saved XLSX to " + outputXlsxPath);
```

Αν το αρχικό PNG περιείχε καθαρό πλέγμα, το παραγόμενο υπολογιστικό φύλλο θα έχει ξεχωριστά κελιά για κάθε στήλη. Διαφορετικά θα έχετε μία στήλη με αλλαγές γραμμής—ακόμη καλύτερο από το χειροκίνητο copy‑paste.

## Βήμα 6: εξαγωγή κειμένου από png – επίσης εξαγωγή σε EPUB (προαιρετικό)

Για πληρότητα, ας δείξουμε πώς να δημιουργήσετε ένα ebook EPUB. Αυτό δείχνει την ευελιξία της μεθόδου `save` του Aspose και σας δίνει έναν ακόμη τρόπο να **εξάγετε κείμενο από png** για δημοσίευση.

```java
        // Optional: export to EPUB for e‑reading devices
        String outputEpubPath = "YOUR_DIRECTORY/report.epub";
        ocrResult.save(outputEpubPath, OutputFormat.Epub);
        System.out.println("Saved EPUB to " + outputEpubPath);
    }
}
```

Αυτό είναι ολόκληρο το πρόγραμμα. Συγκεντρώστε το (`javac ExportDemo.java`) και τρέξτε το (`java ExportDemo`). Αν όλα είναι ρυθμισμένα σωστά, θα δείτε τέσσερα αρχεία να εμφανίζονται στο `YOUR_DIRECTORY`: `report.docx`, `report.xlsx`, `report.epub`, και η κονσόλα θα εμφανίσει τον αριθμό των χαρακτήρων που εξήχθησαν.

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| **License not found** | Η διαδρομή προς το `Aspose.OCR.lic` είναι λανθασμένη ή λείπει. | Τοποθετήστε το αρχείο δίπλα στο JAR ή χρησιμοποιήστε απόλυτη διαδρομή στο `setLicense`. |
| **Garbage characters** | Λάθος γλώσσα έχει οριστεί (π.χ. Αγγλικά για γερμανικό κείμενο). | Καλέστε `ocrEngine.setLanguage(Language.German)` ή το σωστό enum γλώσσας. |
| **Empty output files** | Λάθος διαδρομή αρχείου εισόδου ή μη υποστηριζόμενη μορφή. | Επαληθεύστε τη διαδρομή, βεβαιωθείτε ότι το αρχείο υπάρχει και ότι είναι υποστηριζόμενη μορφή raster (PNG, JPEG, BMP). |
| **Large file size** | Χρήση εικόνων υψηλής ανάλυσης χωρίς μείωση μεγέθους. | Αλλάξτε το μέγεθος της εικόνας σε ~300 dpi πριν το OCR· το Aspose μπορεί να το κάνει αυτόματα μέσω `ocrEngine.setResolution(300)`. |

## Επέκταση της λύσης

Τώρα που μπορείτε να **αναγνωρίσετε κείμενο από εικόνα** και να **μετατρέψετε σαρωμένη εικόνα σε υπολογιστικό φύλλο**, ίσως αναρωτιέστε τι άλλο μπορείτε να κάνετε:

* **Batch processing** – επανάληψη πάνω σε φάκελο PNG και δημιουργία ZIP με αρχεία DOCX/XLSX.
* **Post‑processing** – χρήση κανονικών εκφράσεων για καθαρισμό του θορύβου OCR (π.χ. περιττές αλλαγές γραμμής).
* **Integration** – ενσωμάτωση του κώδικα σε ένα endpoint Spring Boot REST που δέχεται μεταφορτώσεις εικόνας και επιστρέφει ένα κατεβάσιμο DOCX.

## Συμπέρασμα

Μόλις μάθατε πώς να **αναγνωρίζετε κείμενο από εικόνα** χρησιμοποιώντας το Aspose OCR για Java, και τώρα ξέρετε πώς να **μετατρέπετε εικόνα σε docx**, **εξάγετε κείμενο από png**, και **μετατρέπετε σαρωμένη εικόνα σε υπολογιστικό φύλλο** με λίγες κλήσεις μεθόδων. Το πλήρες, εκτελέσιμο παράδειγμα παραπάνω δείχνει κάθε import, κάθε ρύθμιση, και το ακριβές αποτέλεσμα που μπορείτε να περιμένετε.

Στη συνέχεια, δοκιμάστε να αλλάξετε τη γλώσσα σε Αγγλικά, να τροφοδοτήσετε ένα πολυ‑σελίδες TIFF, ή να συνδέσετε το DOCX output με το Aspose.Words για προχωρημένη μορφοποίηση. Ο ουρανός είναι το όριο όταν συνδυάζετε OCR με βιβλιοθήκες δημιουργίας εγγράφων.

Έχετε ερωτήσεις ή αντιμετωπίζετε κάποιο πρόβλημα; Αφήστε ένα σχόλιο, και καλή προγραμματιστική!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετα χαρακτηριστικά του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}