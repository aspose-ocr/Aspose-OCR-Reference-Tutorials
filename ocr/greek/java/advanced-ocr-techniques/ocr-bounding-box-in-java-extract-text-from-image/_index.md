---
category: general
date: 2026-06-16
description: Το tutorial OCR bounding box σε Java δείχνει πώς να εξάγετε κείμενο από
  εικόνα, να διαβάσετε κείμενο από εικόνα και να λάβετε το σκορ εμπιστοσύνης OCR για
  αρχεία JPG.
draft: false
keywords:
- ocr bounding box
- extract text from image
- ocr confidence score
- recognize text from jpg
- read text from image
language: el
og_description: Το OCR bounding box στη Java σάς επιτρέπει να αναγνωρίζετε κείμενο
  από αρχεία JPG, να εξάγετε κείμενο από εικόνα και να προβάλετε τους δείκτες εμπιστοσύνης
  του OCR — όλα σε ένα απλό παράδειγμα κώδικα.
og_title: Πλαίσιο Οριοθέτησης OCR σε Java – Εξαγωγή Κειμένου από Εικόνα
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: OCR bounding box tutorial in Java shows how to extract text from image,
    read text from image, and get OCR confidence score for JPG files.
  headline: OCR Bounding Box in Java – Extract Text from Image
  type: TechArticle
tags:
- OCR
- Java
- image-processing
- text-recognition
title: Πλαίσιο Οριοθέτησης OCR σε Java – Εξαγωγή κειμένου από εικόνα
url: /el/java/advanced-ocr-techniques/ocr-bounding-box-in-java-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Bounding Box σε Java – Εξαγωγή Κειμένου από Εικόνα

Έχετε αναρωτηθεί ποτέ πώς να λάβετε το **ocr bounding box** για κάθε κομμάτι κειμένου σε μια εικόνα Java; Σε αυτό το tutorial θα σας δείξουμε πώς να **extract text from image** αρχεία, **read text from image**, και ακόμη να δείτε το **ocr confidence score** ενώ **recognize text from jpg** αρχεία. Η σύντομη απάντηση; Μερικές γραμμές κώδικα χρησιμοποιώντας μια σύγχρονη βιβλιοθήκη OCR, συν λίγο εξήγηση για το γιατί κάθε κλήση έχει σημασία.

Παρακάτω θα βρείτε ένα πλήρες, έτοιμο‑να‑εκτελεστεί παράδειγμα, ανάλυση βήμα‑βήμα, και μια σειρά πρακτικών συμβουλών που μπορείτε να αντιγράψετε απευθείας στο δικό σας έργο. Στο τέλος, θα μπορείτε να εμφανίσετε κάτι όπως:

```
Text: "Hello World"  Confidence: 0.97  Box: (x=12, y=45, width=210, height=30)
```

## Τι Θα Χρειαστείτε

- **Java 11** ή νεότερη (η σύνταξη παρακάτω χρησιμοποιεί τη λέξη‑κλειδί `var` για συντομία, αλλά μπορείτε να την αφαιρέσετε για παλαιότερα JDK).  
- Μια βιβλιοθήκη OCR που προσφέρει Java API – για αυτόν τον οδηγό θα χρησιμοποιήσουμε το **[Tesseract4J](https://github.com/nguyenq/tess4j)**, ένα ελαφρύ wrapper γύρω από τη δημοφιλή μηχανή Tesseract.  
- Μια εικόνα JPEG (`.jpg`) που περιέχει καθαρό, τυπωμένο κείμενο.  
- Το αγαπημένο σας IDE (IntelliJ IDEA, Eclipse, VS Code…) – όποιο και αν είναι.

Αν λείπει η βιβλιοθήκη, προσθέστε απλώς αυτήν την εξάρτηση Maven:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

Τώρα ας βουτήξουμε.

![OCR bounding box example](ocr-bounding-box.png "OCR bounding box example")

## OCR Bounding Box: Ρύθμιση της Μηχανής

Το πρώτο πράγμα που πρέπει να κάνετε είναι να δημιουργήσετε μια παρουσία OCR engine. Σκεφτείτε το ως το άνοιγμα του σαρωτή που θα διαβάσει αργότερα τα pixel.

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

ITesseract ocrEngine = new Tesseract();          // Step 1 – create the OCR engine
ocrEngine.setDatapath("tessdata");               // point to the language data files
ocrEngine.setLanguage("eng");                    // we’ll work with English for now
```

**Γιατί αυτό είναι σημαντικό:**  
Χωρίς να ορίσετε το `datapath`, το Tesseract δεν θα ξέρει πού βρίσκονται τα language packs του, και θα λάβετε ένα ασαφές σφάλμα “Failed loading language”. Η κλήση `setLanguage` είναι προαιρετική αν χρειάζεστε μόνο το προεπιλεγμένο πακέτο αγγλικής, αλλά η ρητή δήλωση κάνει τον κώδικα πιο σαφή για μελλοντικούς αναγνώστες.

## Φόρτωση της Εικόνας που Θέλετε να Επεξεργαστείτε

Στη συνέχεια, δώστε στη μηχανή το JPEG που θέλετε να αναλύσετε. Η βιβλιοθήκη δέχεται ένα `File` ή `BufferedImage`; θα χρησιμοποιήσουμε ένα `File` για απλότητα.

```java
import java.io.File;

File imageFile = new File("YOUR_DIRECTORY/text_page.jpg");   // Step 2 – load the image
```

**Συμβουλή επαγγελματία:**  
Αν η εικόνα σας βρίσκεται στους πόρους (π.χ., μέσα σε JAR), χρησιμοποιήστε `getResourceAsStream` και τυλίξτε την με `ImageIO.read`. Με αυτόν τον τρόπο το tutorial λειτουργεί τόσο τοπικά όσο και σε πακεταρισμένη εφαρμογή.

## Εκτέλεση OCR Αναγνώρισης

Τώρα ζητάμε πραγματικά από τη μηχανή να διαβάσει την εικόνα. Το αποτέλεσμα είναι μια συμβολοσειρά plain‑text, αλλά θέλουμε επίσης το **ocr confidence score** και το **ocr bounding box** για κάθε γραμμή.

```java
try {
    // Step 3 – run OCR and get a result object with layout data
    var result = ocrEngine.doOCR(imageFile, null);
    // The simple doOCR call returns only text; to get boxes we need the
    // getWords method with a specific page iterator level.
    var words = ocrEngine.getWords(imageFile, ITesseract.PageIteratorLevel.RIL_WORD);
    
    // Step 4 – iterate over each detected word
    for (var word : words) {
        System.out.printf(
            "Text: \"%s\"  Confidence: %.2f  Box: %s%n",
            word.getText(),
            word.getConfidence(),
            word.getBoundingBox().toString()
        );
    }
} catch (TesseractException e) {
    System.err.println("OCR failed: " + e.getMessage());
}
```

**Γιατί χρησιμοποιούμε `getWords` αντί για το απλό `doOCR`:**  
`doOCR` σας δίνει τη ακατέργαστη συμβολοσειρά αλλά απορρίπτει τις χωρικές πληροφορίες. Καλώντας `getWords` με `RIL_WORD` (ή `RIL_TEXTLINE` αν προτιμάτε κουτιά επιπέδου γραμμής), λαμβάνουμε μια λίστα από αντικείμενα `Word` που καθένα φέρει το κείμενο, την εμπιστοσύνη και το ορθογώνιο περιγράμματος. Αυτό είναι η καρδιά της λειτουργίας **ocr bounding box**.

## Κατανόηση της Εξόδου

Η εκτέλεση του παραπάνω αποσπάσματος σε ένα καθαρό JPEG παράγει έξοδο παρόμοια με:

```
Text: "Hello"  Confidence: 0.99  Box: java.awt.Rectangle[x=34,y=12,width=112,height=28]
Text: "World"  Confidence: 0.97  Box: java.awt.Rectangle[x=156,y=12,width=98,height=28]
```

- **Text** – οι αναγνωρισμένοι χαρακτήρες.  
- **Confidence** – μια τιμή κινητής υποδιαστολής μεταξύ 0 και 1· όσο υψηλότερη, τόσο πιο σίγουρη είναι η μηχανή.  
- **Box** – το ορθογώνιο που περιβάλλει τη λέξη σε συντεταγμένες pixel (x, y, width, height).  

Τώρα μπορείτε να **read text from image** και επίσης να γνωρίζετε ακριβώς πού βρίσκεται κάθε απόσπασμα στον καμβά—ιδανικό για επισήμανση, περικοπή ή τροφοδότηση σε επόμενα pipelines NLP.

## Περιπτώσεις Άκρων & Συνηθισμένα Πιθανά Σφάλματα

| Κατάσταση | Τι να Προσέξετε | Διόρθωση / Παράκαμψη |
|-----------|-------------------|-------------------|
| Η εικόνα είναι θολή ή χαμηλής αντίθεσης | Οι βαθμοί εμπιστοσύνης πέφτουν δραματικά (συχνά κάτω από 0.6). | Προεπεξεργασία με OpenCV: αύξηση αντίθεσης, εφαρμογή κατωφλίου. |
| Το JPEG περιέχει περιστραμμένο κείμενο | Τα bounding boxes εμφανίζονται παραμορφωμένα ή λείπουν. | Χρησιμοποιήστε `ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO_OSD)` για να αφήσετε το Tesseract να ανιχνεύσει αυτόματα τον προσανατολισμό. |
| Μεγάλες εικόνες προκαλούν OutOfMemoryError | Η μνήμη heap της Java γεμίζει όταν φορτώνει μεγάλες εικόνες. | Μειώστε την κλίμακα της εικόνας πριν το OCR (`ImageIO.read` → `BufferedImage.getScaledInstance`). |
| Χρειάζεστε κουτιά επιπέδου γραμμής αντί για επίπεδο λέξης | `RIL_WORD` επιστρέφει κουτιά ανά λέξη. | Αλλάξτε σε `ITesseract.PageIteratorLevel.RIL_TEXTLINE`. |
| Μη‑Αγγλικοί χαρακτήρες εμφανίζονται ως � | Τα δεδομένα γλώσσας δεν έχουν φορτωθεί. | Κατεβάστε το κατάλληλο αρχείο `.traineddata` και δείξτε το `setDatapath` στο φάκελό του. |

Η αντιμετώπιση αυτών των προβλημάτων νωρίς σας εξοικονομεί ώρες εντοπισμού σφαλμάτων αργότερα.

## Πλήρες Παράδειγμα Εργασίας (Όλα τα Βήματα σε Ένα Αρχείο)

Παρακάτω είναι μια αυτόνομη κλάση Java που μπορείτε να αντιγράψετε‑επικολλήσετε σε φάκελο `src/main/java` και να εκτελέσετε με `mvn exec:java`. Συγκεντρώνει όλα όσα συζητήσαμε.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.ITesseract.RenderedFormat;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;
import net.sourceforge.tess4j.Word;

import java.io.File;
import java.util.List;

public class OcrBoundingBoxDemo {

    public static void main(String[] args) {
        // ==== Step 1: Initialize the OCR engine ====
        ITesseract ocrEngine = new Tesseract();
        ocrEngine.setDatapath("tessdata"); // folder containing .traineddata files
        ocrEngine.setLanguage("eng");      // English language pack

        // Optional: improve accuracy for printed text
        ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO);
        ocrEngine.setOcrEngineMode(ITesseract.OEM_TESSERACT_ONLY);

        // ==== Step 2: Load the JPEG you want to read ====
        File imageFile = new File("YOUR_DIRECTORY


## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή Κειμένου από Εικόνα Java με Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Εξαγωγή Κειμένου από Εικόνες – Βασικά OCR με Aspose.OCR για Java](/ocr/english/java/ocr-basics/)
- [Πώς να OCR Κείμενο Εικόνας με Γλώσσα Χρησιμοποιώντας Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}