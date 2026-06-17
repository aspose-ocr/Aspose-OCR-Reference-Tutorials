---
category: general
date: 2026-02-14
description: Μάθετε πώς να διορθώνετε την κλίση της εικόνας και να προεπεξεργάζεστε
  την εικόνα για OCR χρησιμοποιώντας το Aspose OCR σε Java. Αυξήστε την ακρίβεια,
  εξάγετε κείμενο από φόρμα και βελτιώστε τα αποτελέσματα του OCR.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- extract text from form
- how to improve ocr
- process image with ocr
language: el
og_description: Μάθετε πώς να ευθυγραμμίζετε εικόνα και να την προεπεξεργάζεστε για
  OCR σε Java. Αυτός ο οδηγός σας δείχνει πώς να εξάγετε κείμενο από φόρμα και να
  βελτιώσετε την ακρίβεια του OCR.
og_title: Πώς να ευθυγραμμίσετε την εικόνα για OCR – Εισαγωγικό στην προεπεξεργασία
  Java
tags:
- OCR
- Java
- Image Processing
title: Πώς να διορθώσετε την κλίση της εικόνας για OCR – Πλήρης οδηγός προεπεξεργασίας
  Java
url: /el/java/advanced-ocr-techniques/how-to-deskew-image-for-ocr-complete-java-pre-processing-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να διορθώσετε την κλίση εικόνας για OCR – Πλήρης οδηγός προεπεξεργασίας Java

Σας έχει αναρωτηθεί ποτέ **how to deskew image** αρχεία πριν τα δώσετε σε μια μηχανή OCR; Δεν είστε μόνοι. Σε πολλά πραγματικά έργα—σκεφτείτε σαρωμένα τιμολόγια, χειρόγραφες φόρμες ή παλιά αρχεία εφημερίδων—μια λοξή σάρωση μπορεί να μειώσει δραστικά την ακρίβεια της αναγνώρισης. Τα καλά νέα; Με μερικές γραμμές Java και τη βιβλιοθήκη Aspose OCR, μπορείτε να ευθυγραμμίσετε, καθαρίσετε και δυαδικοποιήσετε τις εικόνες σας ώστε η μηχανή OCR να τις διαβάζει σαν επαγγελματίας.

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία: φόρτωση μιας σαρωμένης φόρμας, εφαρμογή φίλτρου διόρθωσης κλίσης, αφαίρεση θορύβου, μετατροπή σε καθαρή ασπρόμαυρη εικόνα και, τέλος, εξαγωγή του κειμένου. Στο τέλος θα γνωρίζετε **how to improve OCR**, **process image with OCR** αξιόπιστα, και θα έχετε ένα έτοιμο παράδειγμα κώδικα που **extracts text from form** αρχεία σε δευτερόλεπτα.

## What You’ll Need

- **Java Development Kit (JDK) 8 or newer** – ο κώδικας μεταγλωττίζεται με οποιοδήποτε πρόσφατο JDK.
- **Aspose.OCR for Java** library (τελευταία έκδοση τη στιγμή της συγγραφής, 23.12). Μπορείτε να το κατεβάσετε από το Maven Central ή να κατεβάσετε το JAR από την ιστοσελίδα της Aspose.
- Ένα αρχείο εικόνας για δοκιμή (π.χ., `scanned_form.jpg`). Ιδανικά μια σαρωμένη εγγραφή που είναι λίγο λοξή.
- Το αγαπημένο σας IDE (IntelliJ IDEA, Eclipse, VS Code…) – οτιδήποτε που σας επιτρέπει να εκτελέσετε μια απλή μέθοδο `main`.

> **Pro tip:** Αν χρησιμοποιείτε Maven, προσθέστε την εξάρτηση παρακάτω στο `pom.xml`. Θα φέρει αυτόματα όλες τις απαιτούμενες εξαρτήσεις.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version>
</dependency>
```

---

## Step 1 – Create the OCR Engine Instance  

Το πρώτο βήμα είναι να δημιουργήσετε ένα `OcrEngine`. Σκεφτείτε το ως τον εγκέφαλο που θα διαβάσει αργότερα τους χαρακτήρες στην εικόνα σας.

```java
import com.aspose.ocr.*;

public class DeskewDemo {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine – this object holds all settings.
        OcrEngine ocrEngine = new OcrEngine();
```

Γιατί είναι κρίσιμο αυτό το βήμα; Χωρίς μηχανή, δεν υπάρχει που να προσαρτήσουμε τα φίλτρα προεπεξεργασίας που θα προσθέσουμε αργότερα. Η μηχανή διαχειρίζεται επίσης πακέτα γλώσσας, μοντέλα αναγνώρισης και μορφές εξόδου.

---

## Step 2 – Load the Image You Want to Clean  

Στη συνέχεια, δείξτε στη μηχανή το αρχείο που θέλετε να ευθυγραμμίσετε. Η `ImageStream.fromFile` διαβάζει το αρχείο σε ροή που μπορεί να επεξεργαστεί η Aspose.

```java
        // Load the image (replace the path with your own file location)
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/scanned_form.jpg"));
```

Αν η εικόνα βρίσκεται σε φάκελο πόρων μέσα σε ένα JAR, μπορείτε να χρησιμοποιήσετε `ImageStream.fromResource` αντί αυτού. Το σημαντικό είναι η μηχανή να λαμβάνει ένα **bitmap** που μπορεί να χειριστεί.

---

## Step 3 – Add Pre‑processing Filters in the Right Order  

Εδώ συμβαίνει η μαγεία. Θα αλυσσοδείξουμε τρία φίλτρα:

1. **DeskewFilter** – ανιχνεύει αυτόματα τη γωνία κλίσης και περιστρέφει την εικόνα πίσω στην οριζόντια θέση.
2. **NoiseRemovalFilter** – αφαιρεί στίγματα και κόκκο που συνήθως εμφανίζονται σε σαρώσεις χαμηλής ποιότητας.
3. **BinarizationFilter** – μετατρέπει την εικόνα σε καθαρό ασπρόμαυρο, κάτι που αγαπούν οι περισσότερες μηχανές OCR.

```java
        // Attach preprocessing filters: deskew → denoise → binarize
        ocrEngine.getEngineOptions()
                 .addPreprocessingFilter(new DeskewFilter())
                 .addPreprocessingFilter(new NoiseRemovalFilter())
                 .addPreprocessingFilter(new BinarizationFilter());
```

> **Why this order?** Το Deskew πρώτα διασφαλίζει ότι η περιστροφή εφαρμόζεται στα αρχικά pixel· ο καθαρισμός μετά τη περιστροφή αποτρέπει την εισαγωγή νέου θορύβου. Η δυαδικοποίηση στο τέλος δίνει στο OCR μια καθαρή, υψηλής αντίθεσης εικόνα — ακριβώς αυτό που χρειάζεστε για **process image with OCR** αποδοτικά.

---

## Step 4 – Run OCR on the Pre‑processed Image  

Τώρα ζητάμε από τη μηχανή να διαβάσει το κείμενο. Η κλήση `process()` επιστρέφει ένα `OcrResult` που περιέχει τη αναγνωρισμένη συμβολοσειρά και προαιρετικά σκορ εμπιστοσύνης.

```java
        // Perform OCR on the cleaned image
        OcrResult ocrResult = ocrEngine.process();

        // Print the extracted text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Αν όλα λειτουργήσουν, θα δείτε τους ακατέργαστους χαρακτήρες που υπήρχαν στην αρχική φόρμα. Αυτό είναι ο πυρήνας των ροών εργασίας **extract text from form** — μόλις έχετε τη συμβολοσειρά, μπορείτε να εξάγετε πεδία, να τη στείλετε σε βάση δεδομένων ή να δημιουργήσετε PDFs.

---

## Step 5 – Verify the Output and Tune Parameters  

Η εκτέλεση του demo σε ένα ελαφρώς λοξό τιμολόγιο θα πρέπει να παράγει ευανάγνωστη έξοδο. Ωστόσο, υπάρχουν ακραίες περιπτώσεις:

- **Extreme angles (>15°)** – ίσως χρειαστεί να αυξήσετε την ανοχή του `DeskewFilter` μέσω `setAngleThreshold`.
- **Heavy background patterns** – σκεφτείτε να προσθέσετε ένα `ContrastEnhancementFilter` πριν τη δυαδικοποίηση.
- **Multi‑page PDFs** – κάντε βρόχο σε κάθε σελίδα, μετατρέποντάς την πρώτα σε εικόνα, και στη συνέχεια χρησιμοποιήστε την ίδια μηχανή.

Παρακάτω φαίνεται ένα δείγμα εξόδου κονσόλας από μια απόδειξη που περιστράφηκε 10°:

```
=== Recognized Text ===
Date: 02/13/2026
Item          Qty   Price
Coffee        2     $4.00
Bagel         1     $2.50
Total                $6.50
```

Παρατηρήστε πώς οι γραμμές κειμένου ευθυγραμμίζονται τέλεια παρά την αρχική κλίση. Αυτή είναι η δύναμη του σωστού **how to deskew image**.

---

## Common Pitfalls and How to Avoid Them  

| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| **Garbage output after deskew** | Η εικόνα είναι πολύ σκοτεινή για το φίλτρο να εντοπίσει άκρα. | Αυξήστε τη φωτεινότητα με `BrightnessContrastFilter` πριν το deskew. |
| **Missing characters** | Το κατώφλι δυαδικοποίησης είναι πολύ επιθετικό. | Χρησιμοποιήστε `OtsuBinarizationFilter` για προσαρμοστική δυαδικοποίηση. |
| **Slow processing on large files** | Τα φίλτρα τρέχουν σε bitmap πλήρους ανάλυσης. | Μειώστε την ανάλυση με `ResizeFilter` (π.χ., max 1500 px) πριν τα άλλα βήματα. |

---

## Bonus: Visualizing the Pre‑processing Result  

Αν θέλετε να δείτε την καθαρισμένη εικόνα πριν το OCR, μπορείτε να την εξάγετε:

```java
        // Save the pre‑processed image for inspection
        ocrEngine.getEngineOptions()
                 .getPreprocessedImage()
                 .save("cleaned_form.png");
```

![how to deskew image example](https://example.com/cleaned_form.png "Result of how to deskew image using Aspose OCR")

Το **alt text** περιλαμβάνει τη βασική λέξη‑κλειδί, ικανοποιώντας την απαίτηση SEO και βοηθώντας τα προγράμματα ανάγνωσης οθόνης.

---

## Recap – What We Covered  

- **How to deskew image** χρησιμοποιώντας `DeskewFilter`.
- Μια πλήρης αλυσίδα **preprocess image for OCR** (deskew → denoise → binarize).
- Ο ακριβής κώδικας για **extract text from form** αρχεία με Aspose OCR.
- Συμβουλές για **how to improve OCR** ακρίβεια και αντιμετώπιση δύσκολων περιπτώσεων.
- Ένας γρήγορος τρόπος για **process image with OCR** σε παραγωγική μέθοδο Java.

---

## Next Steps  

Τώρα που μπορείτε να ευθυγραμμίσετε και να διαβάσετε μια σελίδα, σκεφτείτε την κλιμάκωση:

1. **Batch processing** – επαναλάβετε τη διαδικασία για έναν φάκελο σαρώσεων, εφαρμόζοντας την ίδια αλυσίδα.
2. **Field extraction** – χρησιμοποιήστε κανονικές εκφράσεις ή μια βιβλιοθήκη όπως η Apache PDFBox για να μετατρέψετε το ακατέργαστο κείμενο σε δομημένα δεδομένα.
3. **Integration with cloud services** – στείλτε την καθαρισμένη εικόνα στο Azure Form Recognizer ή στο Google Document AI για προχωρημένη ανάλυση διάταξης.

Κάθε ένα από αυτά τα θέματα βασίζεται στο θεμέλιο που μόλις θέσατε, και όλα ωφελούνται από μια σταθερή ρουτίνα **preprocess image for OCR**.

---

### Final Thought  

Η επίτευξη τέλειας απόδοσης OCR σπάνια εξαρτάται από ένα μόνο κόλπο· είναι θέμα μιας συστηματικής ροής εργασίας. Με την εξοικείωση σας με το **how to deskew image**, αφαιρέσατε το μεγαλύτερο εμπόδιο. Από εδώ, μπορείτε να πειραματιστείτε με άλλα φίλτρα, να ρυθμίσετε τα όρια και να δείτε τα ποσοστά αναγνώρισης να ανεβαίνουν.

Αν αντιμετωπίσατε προβλήματα ή έχετε ιδέες για περαιτέρω βελτιώσεις, αφήστε ένα σχόλιο παρακάτω. Καλό κώδικα, και οι σαρώσεις σας να είναι πάντα τέλεια ευθυγραμμισμένες!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}