---
category: general
date: 2026-08-12
description: Αναγνώριση κειμένου από εικόνα χρησιμοποιώντας τη μηχανή OCR Java. Μάθετε
  πώς να εξάγετε κείμενο από εικόνα, να βελτιώσετε την ακρίβεια του OCR και να προεπεξεργαστείτε
  την εικόνα για OCR σε αρχεία PNG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from image
- how to extract text from image
- how to improve OCR accuracy
- how to preprocess image for OCR
- perform OCR on PNG
language: el
lastmod: 2026-08-12
og_description: Αναγνώριση κειμένου από εικόνα με Java. Αυτό το σεμινάριο δείχνει
  πώς να εξάγετε κείμενο από εικόνα, να βελτιώσετε την ακρίβεια του OCR και να εκτελέσετε
  OCR σε PNG χρησιμοποιώντας πολυνηματισμό και GPU.
og_image_alt: Diagram showing Java OCR engine recognizing text from image
og_title: Αναγνώριση κειμένου από εικόνα σε Java – βήμα‑βήμα οδηγός OCR
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: recognize text from image using Java OCR engine. Learn how to extract
    text from image, improve OCR accuracy, and preprocess image for OCR on PNG files.
  headline: recognize text from image in Java – complete OCR guide
  type: TechArticle
- description: recognize text from image using Java OCR engine. Learn how to extract
    text from image, improve OCR accuracy, and preprocess image for OCR on PNG files.
  name: recognize text from image in Java – complete OCR guide
  steps:
  - name: Explanation of each step
    text: '| Step | Why it matters | How it helps you **recognize text from image**
      | |------|----------------|-----------------------------------------------|
      | 1️⃣ Create the OCR engine | Instantiates the core component that drives all
      subsequent operations. | Provides the entry point for all OCR actions. | '
  - name: Expected output
    text: 'If `sample-image.png` contains the sentence “Hello, world! 123”, the console
      will display something similar to:'
  - name: 1. Binarization with Otsu’s method
    text: '```java import java.awt.image.BufferedImage; import com.example.image.Binarizer;
      // hypothetical helper class'
  - name: 2. Scaling to 300 dpi
    text: '```java import com.example.image.Resizer;'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Αναγνώριση κειμένου από εικόνα σε Java – πλήρης οδηγός OCR
url: /el/java/advanced-ocr-techniques/recognize-text-from-image-in-java-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση κειμένου από εικόνα σε Java – πλήρης οδηγός OCR

Αν χρειάζεστε **αναγνώριση κειμένου από εικόνα** σε μια εφαρμογή Java, αυτό το tutorial σας δείχνει ακριβώς πώς. Στο τέλος του οδηγού θα μπορείτε να εξάγετε κείμενο από αρχεία εικόνας, να βελτιώσετε την ακρίβεια του OCR και να εκτελέσετε OCR σε PNG πόρους με υποστήριξη πολυπύρηνης επεξεργασίας και GPU.

Πολλοί προγραμματιστές αναρωτιούνται **πώς να εξάγετε κείμενο από εικόνα** χωρίς να γράψουν ένα προσαρμοσμένο νευρωνικό δίκτυο. Η λύση είναι να χρησιμοποιήσετε μια αποδεδειγμένη μηχανή OCR, να τη ρυθμίσετε για ταχύτητα και ακρίβεια, και να εφαρμόσετε τα σωστά βήματα προεπεξεργασίας. Οι παρακάτω ενότητες σας καθοδηγούν βήμα‑βήμα, ώστε να μπορείτε να αντιγράψετε τον κώδικα απευθείας στο έργο σας.

## Τι θα μάθετε

* Ρύθμιση μιας μηχανής OCR σε Java.  
* Ενεργοποίηση πολυνηματικής επεξεργασίας και προαιρετικής επιτάχυνσης GPU.  
* Προσθήκη πακέτων γλώσσας για Αγγλικά και Ισπανικά.  
* Εφαρμογή φίλτρων προεπεξεργασίας εικόνας για βελτίωση της ποιότητας αναγνώρισης.  
* Ενεργοποίηση του ενσωματωμένου διορθωτή ορθογραφίας για καθαρότερο αποτέλεσμα.  
* Εκτέλεση OCR σε PNG αρχεία και εκτύπωση του αναγνωρισμένου κειμένου.

Δεν απαιτούνται εξωτερικές υπηρεσίες—όλα εκτελούνται τοπικά, καθιστώντας το ιδανικό για εφαρμογές εκτός σύνδεσης ή με ευαίσθητα δεδομένα.

## Προαπαιτούμενα

* Java 17 ή νεότερη (ο κώδικας χρησιμοποιεί τη σύγχρονη σύνταξη `var` αλλά μπορεί να μεταφερθεί).  
* Μια βιβλιοθήκη OCR που παρέχει τις κλάσεις `OcrEngine`, `Language` και `EngineOptions` (π.χ., **GroupDocs.Parser**, **Aspose.OCR**, ή οποιοδήποτε συμβατό SDK).  
* Maven ή Gradle για διαχείριση εξαρτήσεων.  
* Ένα δείγμα PNG εικόνας (`sample-image.png`) τοποθετημένο στο `YOUR_DIRECTORY`.

> **Pro tip:** Αν σκοπεύετε να επεξεργαστείτε χιλιάδες εικόνες, διαθέστε αρκετή RAM για το buffer της GPU και απενεργοποιήστε τον διορθωτή ορθογραφίας μόνο όταν χρειάζεστε ακατέργαστη έξοδο OCR.

## Αναγνώριση κειμένου από εικόνα με Java OCR engine

Παρακάτω υπάρχει ένα πλήρες, εκτελέσιμο πρόγραμμα Java που ακολουθεί τα οκτώ βήματα που εμφανίζονται στο αρχικό απόσπασμα. Περιλαμβάνει εισαγωγές, μια μέθοδο `main` και ενσωματωμένα σχόλια που εξηγούν τον σκοπό κάθε γραμμής.

```java
// File: OcrDemo.java
import com.example.ocr.OcrEngine;            // Replace with your OCR library's package
import com.example.ocr.Language;
import com.example.ocr.EngineOptions;
import com.example.ocr.ImagePreprocessingOptions;

public class OcrDemo {

    public static void main(String[] args) {
        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable multi‑core processing for faster throughput
        ocrEngine.getEngineOptions().setUseMultiThreading(true);

        // Step 3: (Optional) Turn on GPU acceleration if a compatible GPU is present
        ocrEngine.getEngineOptions().setUseGpu(true);

        // Step 4: Add the languages you want to recognize (English and Spanish)
        ocrEngine.getLanguage().add(Language.English);
        ocrEngine.getLanguage().add(Language.Spanish);

        // Step 5: Apply common image‑preprocessing filters to improve OCR accuracy
        ImagePreprocessingOptions imgOpts = ocrEngine.getImagePreprocessingOptions();
        imgOpts.setRotate(true);   // Auto‑rotate based on EXIF orientation
        imgOpts.setDeskew(true);   // Straighten skewed text lines
        imgOpts.setDenoise(true);  // Reduce background noise

        // Step 6: Enable the built‑in spell corrector for cleaner output
        ocrEngine.getEngineOptions().setUseSpellCorrector(true);

        // Step 7: Perform OCR on the target PNG image
        // This demonstrates how to perform OCR on PNG files efficiently.
        String imagePath = "YOUR_DIRECTORY/sample-image.png";
        String ocrResult = ocrEngine.recognizeImage(imagePath);

        // Step 8: Output the recognized text
        System.out.println("=== OCR Result ===");
        System.out.println(ocrResult);
    }
}
```

### Εξήγηση κάθε βήματος

| Βήμα | Γιατί είναι σημαντικό | Πώς σας βοηθά να **αναγνωρίσετε κείμενο από εικόνα** |
|------|-----------------------|------------------------------------------------------|
| 1️⃣ Δημιουργία του OCR engine | Δημιουργεί το βασικό στοιχείο που καθοδηγεί όλες τις επόμενες λειτουργίες. | Παρέχει το σημείο εισόδου για όλες τις ενέργειες OCR. |
| 2️⃣ Ενεργοποίηση επεξεργασίας πολυπύρηνου | Οι σύγχρονοι επεξεργαστές έχουν πολλούς πυρήνες· η αξιοποίησή τους μειώνει το συνολικό χρόνο επεξεργασίας. | Επιταχύνει τις εργασίες παρτίδας όταν **εκτελείτε OCR σε PNG** αρχεία παράλληλα. |
| 3️⃣ Ενεργοποίηση επιτάχυνσης GPU (προαιρετικό) | Οι GPU διαπρέπουν σε παράλληλες λειτουργίες pixel, ειδικά για μεγάλες εικόνες. | Μπορεί να μειώσει τον χρόνο αναγνώρισης έως και 70 % σε υποστηριζόμενο υλικό. |
| 4️⃣ Προσθήκη πακέτων γλώσσας | Η ακρίβεια του OCR εξαρτάται από τα μοντέλα γλώσσας· η καθορισμένη μόνο των απαραίτητων γλωσσών μειώνει τα ψευδώς θετικά. | Βελτιώνει τις πιθανότητες σωστής αναγνώρισης χαρακτήρων όταν **πώς να εξάγετε κείμενο από εικόνα** σε πολυγλωσσικά σενάρια. |
| 5️⃣ Προεπεξεργασία εικόνας | Η περιστροφή, η διόρθωση κλίσης και η μείωση θορύβου διορθώνουν κοινά προβλήματα σάρωσης. | Βελτιώνει άμεσα **πώς να βελτιώσετε την ακρίβεια του OCR** παρουσιάζοντας ένα καθαρότερο bitmap στην μηχανή. |
| 6️⃣ Διορθωτής ορθογραφίας | Βήμα μεταεπεξεργασίας που διορθώνει κοινά ορθογραφικά λάθη του OCR. | Παράγει πιο αναγνώσιμο αποτέλεσμα χωρίς χειροκίνητο καθαρισμό. |
| 7️⃣ Εκτέλεση OCR σε PNG | Η μέθοδος `recognizeImage` διαβάζει το αρχείο, εφαρμόζει προεπεξεργασία και εκτελεί τη διαδικασία αναγνώρισης. | Δείχνει **εκτέλεση OCR σε PNG** ενώ διαχειρίζεται ιδιαιτερότητες συγκεκριμένων μορφών (π.χ., απώλεια συμπίεσης). |
| 8️⃣ Εκτύπωση αποτελέσματος | Σας παρέχει άμεση ανατροφοδότηση για να επαληθεύσετε την επιτυχία. | Σας επιτρέπει να επιβεβαιώσετε ότι το κείμενο ήταν σωστά **αναγνωρισμένο από εικόνα**. |

### Αναμενόμενο αποτέλεσμα

Αν το `sample-image.png` περιέχει τη φράση “Hello, world! 123”, η κονσόλα θα εμφανίσει κάτι παρόμοιο με:

```
=== OCR Result ===
Hello, world! 123
```

Η ακριβής έξοδος μπορεί να διαφέρει ελαφρώς ανάλογα με την ποιότητα της εικόνας και τις ρυθμίσεις γλώσσας, αλλά ο διορθωτής ορθογραφίας συνήθως διορθώνει μικρά σφάλματα όπως “Helli” → “Hello”.

## πώς να προεπεξεργαστείτε εικόνα για OCR – πιο βαθιά ανάλυση

Ενώ ο παραπάνω κώδικας χρησιμοποιεί την ενσωματωμένη προεπεξεργασία της μηχανής, μπορείτε επίσης να εφαρμόσετε προσαρμοσμένα φίλτρα πριν παραδώσετε την εικόνα στη μηχανή OCR. Ακολουθούν δύο κοινές τεχνικές:

### 1. Δυαδικοποίηση με τη μέθοδο Otsu

```java
import java.awt.image.BufferedImage;
import com.example.image.Binarizer; // hypothetical helper class

BufferedImage original = ImageIO.read(new File(imagePath));
BufferedImage binary = Binarizer.otsuThreshold(original);
ocrEngine.recognizeImage(binary);
```

Η δυαδικοποίηση μετατρέπει την εικόνα σε ασπρόμαυρο, κάτι που συχνά **πώς να βελτιώσετε την ακρίβεια του OCR** για σάρωση χαμηλής αντίθεσης.

### 2. Κλιμάκωση σε 300 dpi

```java
import com.example.image.Resizer;

BufferedImage scaled = Resizer.scaleToDPI(original, 300);
ocrEngine.recognizeImage(scaled);
```

Οι περισσότερες μηχανές OCR απαιτούν τουλάχιστον 300 dpi για βέλτιστη αναγνώριση χαρακτήρων. Η κλιμάκωση αποτρέπει τη μηχανή από το να διαβάσει λανθασμένα μικροσκοπικά γλύφους.

> **Note:** Αν ενεργοποιήσετε τόσο την προσαρμοσμένη προεπεξεργασία όσο και τις ενσωματωμένες επιλογές της μηχανής, η μηχανή θα εφαρμόσει τα φίλτρα της *μετά* τα δικά σας. Επιλέξτε τη σειρά που ταιριάζει καλύτερα στα χαρακτηριστικά της εικόνας σας.

## πώς να εξάγετε κείμενο από εικόνα – αντιμετώπιση ακραίων περιπτώσεων

| Κατάσταση | Συνιστώμενη προσαρμογή |
|-----------|------------------------|
| **Πολύ θορυβώδες φόντο** | Αυξήστε την ένταση του `setDenoise(true)` ή εκτελέστε ένα μέσο φίλτρο πριν από το OCR. |
| **Skew > 15°** | Χρησιμοποιήστε `setDeskew(true)` *και* παρέχετε μια χειροκίνητη γωνία περιστροφής μέσω `imgOpts.setRotateAngle(θ)`. |
| **Μικτές γλώσσες (π.χ., Αγγλικά + Ισπανικά)** | Προσθέστε και τα δύο πακέτα γλώσσας όπως φαίνεται στο Βήμα 4· η μηχανή θα αλλάξει αυτόματα το πλαίσιο. |
| **Μεγάλα PDF μετατρεπόμενα σε PNG** | Επεξεργαστείτε κάθε σελίδα ως ξεχωριστό PNG και συγκεντρώστε τα αποτελέσματα· η πολυνηματική επεξεργασία (Βήμα 2) θα διατηρήσει το συνολικό χρόνο χαμηλό. |
| **GPU μη διαθέσιμο** | Διατηρήστε το `setUseGpu(true)` αλλά τυλίξτε το σε try‑catch· η μηχανή θα επιστρέψει στην CPU χωρίς να καταρρεύσει. |

## εκτέλεση OCR σε PNG – παράδειγμα επεξεργασίας παρτίδας

Όταν χρειάζεται να **εκτελέσετε OCR σε PNG** αρχεία σε έναν φάκελο, ένας απλός βρόχος με το ίδιο αντικείμενο μηχανής λειτουργεί άψογα:

```java
Path dir = Paths.get("YOUR_DIRECTORY");
try (Stream<Path> files = Files.list(dir)) {
    files.filter(p -> p.toString().endsWith(".png"))
         .forEach(p -> {
             String text = ocrEngine.recognizeImage(p.toString());
             System.out.println("File: " + p.getFileName());
             System.out.println(text);
             System.out.println("---");
         });
}
```

Επειδή η μηχανή είναι ήδη ρυθμισμένη για πολυπύρηνη επεξεργασία και GPU, αυτός ο βρόχος μπορεί να επεξεργαστεί δεκάδες εικόνες παράλληλα χωρίς επιπλέον κώδικα.

## Πλήρες λειτουργικό παράδειγμα

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι μια αυτόνομη κλάση που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα IDE, να προσθέσετε την κατάλληλη εξάρτηση Maven και να τρέξετε αμέσως:



## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να OCR κείμενο εικόνας με γλώσσα χρησιμοποιώντας Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Εξαγωγή κειμένου από εικόνα Java με Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [image to text java: Μετατροπή εικόνας σε κείμενο με Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}