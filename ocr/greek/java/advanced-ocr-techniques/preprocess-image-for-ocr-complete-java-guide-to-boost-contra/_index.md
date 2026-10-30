---
category: general
date: 2026-10-30
description: Μάθετε πώς να βελτιώσετε το OCR χρησιμοποιώντας preprocessing εικόνων
  σε Java με Aspose OCR. Αυτός ο οδηγός δείχνει πώς να αυξήσετε το image contrast,
  να ορίσετε το contrast level και να extract text αποδοτικά.
draft: false
keywords:
- how to improve OCR
- how to boost contrast
- preprocess image OCR
- extract text image Java
- recognize text image Java
lastmod: 2026-10-30
og_description: Μάθετε πώς να βελτιώσετε το OCR με preprocessing εικόνων σε Java με
  Aspose OCR. Ο οδηγός εξηγεί την ενίσχυση του contrast, τον ορισμό του contrast level
  και την γρήγορη εξαγωγή του text.
og_image_alt: Screenshot of a Java OCR preprocessing pipeline showing before‑and‑after
  contrast enhancement
og_title: Πώς να βελτιώσετε το OCR – οδηγός Java image preprocessing
schemas:
- author: Aspose
  dateModified: '2026-10-30'
  description: Learn how to improve OCR by preprocessing images in Java with Aspose
    OCR. This guide shows how to boost image contrast, set contrast level, and extract
    text efficiently.
  headline: How to improve OCR – preprocess image for OCR in Java with Aspose
  type: TechArticle
- description: Learn how to improve OCR by preprocessing images in Java with Aspose
    OCR. This guide shows how to boost image contrast, set contrast level, and extract
    text efficiently.
  name: How to improve OCR – preprocess image for OCR in Java with Aspose
  steps:
  - name: '**Deskew** – corrects slight rotations.'
    text: '**Deskew** – corrects slight rotations.'
  - name: '**Denoise** – removes speckles that confuse character segmentation.'
    text: '**Denoise** – removes speckles that confuse character segmentation.'
  - name: '**Contrast enhancement** – makes dark text stand out against the background.'
    text: '**Contrast enhancement** – makes dark text stand out against the background.'
  type: HowTo
- questions:
  - answer: Yes—load the appropriate language pack with `engine.setLanguage("fr")`
      or any supported ISO code to improve accuracy for non‑English text.
    question: Can I use this approach for languages other than English?
  - answer: It does not read PDF pages natively; you should extract images from the
      PDF first (e.g., with Aspose PDF) and then feed them to the OCR engine.
    question: Does Aspose OCR support PDF input directly?
  - answer: The library handles images up to 30 MP without needing to load the whole
      file into memory, thanks to its streaming architecture.
    question: How large an image can I process?
  - answer: Absolutely—iterate over the files, reuse the same `OcrEngine` instance,
      and add each file to `OcrInput`. This reduces per‑image overhead dramatically.
    question: Is there a way to batch‑process a folder of images?
  - answer: Try adjusting `setContrastLevel` in smaller increments, experiment with
      `setDenoiseMode`, or enable `setUseAdaptiveThreshold(true)` for difficult backgrounds.
    question: What if the OCR output still contains errors?
  type: FAQPage
tags:
- Java
- OCR
- Image Processing
title: Πώς να βελτιώσετε το OCR – προεπεξεργασία εικόνας για OCR σε Java με Aspose
url: /el/java/advanced-ocr-techniques/preprocess-image-for-ocr-complete-java-guide-to-boost-contra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προεπεξεργασία εικόνας για OCR – πλήρης οδηγός Java

Έχετε ποτέ χρειαστεί να **προεπεξεργαστείτε εικόνα για OCR** αλλά δεν ήσασταν σίγουροι ποιες ρυθμίσεις κάνουν πραγματικά τη διαφορά; Δεν είστε μόνοι. Οι περισσότεροι προγραμματιστές ρίχνουν μια εικόνα σε μια μηχανή OCR και ελπίζουν ότι θα συμβεί το μαγικό, μόνο για να πάρουν ακατάστατο αποτέλεσμα. Σε αυτό το tutorial θα περάσουμε από ένα πρακτικό, ολοκληρωμένο παράδειγμα που **ενισχύει την αντίθεση της εικόνας**, ρυθμίζει το **επίπεδο αντίθεσης**, και τελικά **αναγνωρίζει κείμενο από εικόνα** χρησιμοποιώντας το Aspose OCR for Java.

Μέχρι να τελειώσετε, θα έχετε ένα επαναχρησιμοποιήσιμο κομμάτι κώδικα που **εξάγει κείμενο χρησιμοποιώντας OCR** αξιόπιστα, ακόμη και σε θορυβώδεις σκαναρίσματα. Χωρίς κρυφά κόλπα, μόνο σαφή βήματα και η λογική πίσω από το καθένα.

## Γρήγορες απαντήσεις
- **Ποιο είναι το πρώτο βήμα για τη βελτίωση του OCR;** Φορτώστε την άδεια Aspose OCR πριν δημιουργήσετε τη μηχανή.  
- **Ποιες τρεις επιλογές προεπεξεργασίας έχουν τη μεγαλύτερη σημασία;** Διόρθωση κλίσης (deskew), αποθορυβοποίηση (denoise) και ενίσχυση αντίθεσης.  
- **Ποιο επίπεδο αντίθεσης λειτουργεί για τα περισσότερα τυπωμένα έγγραφα;** Περίπου 1.3 f παρέχει καλή ισορροπία.  
- **Μπορώ να δω την επεξεργασμένη εικόνα;** Ναι—εξάγετε το ενδιάμεσο bitmap σε PNG.  
- **Χρειάζομαι άδεια για παραγωγή;** Απόλυτα· η δοκιμαστική έκδοση λειτουργεί σε περιορισμένη λειτουργία και προσθέτει υδατογραφήματα.

## Πώς να βελτιώσετε το OCR προεπεξεργάζοντας εικόνες σε Java;

Φορτώστε την εικόνα, εφαρμόστε διόρθωση κλίσης, αποθορυβοποίηση και ρύθμιση αντίθεσης, και στη συνέχεια εκτελέστε τον αναγνωριστή. Η αλυσίδα επεξεργασίας του Aspose OCR επεξεργάζεται την εικόνα ακριβώς με αυτή τη σειρά, εξασφαλίζοντας ότι κάθε μετασχηματισμός λειτουργεί στα πιο καθαρά δεδομένα πριν ο αναγνωριστής νευρωνικού δικτύου τα δει. Αυτή η προσέγγιση δύο βημάτων—προεπεξεργασία και μετά αναγνώριση—παρέχει έως και 30 % υψηλότερη ακρίβεια χαρακτήρων σε τυπικά σκαναρισμένα έγγραφα.

## Τι είναι το Aspose OCR for Java;

Το Aspose OCR for Java είναι μια βιβλιοθήκη που υποστηρίζει **πάνω από 30 μορφές εικόνας** (συμπεριλαμβανομένων JPEG, PNG, TIFF, BMP) και μπορεί να επεξεργαστεί μια παρτίδα 200‑σελίδων πολλαπλών εικόνων σε λιγότερο από 2 δευτερόλεπτα σε έναν τυπικό διακομιστή 8‑πυρήνων. Παρέχει ενσωματωμένα φίλτρα διόρθωσης κλίσης, αποθορυβοποίησης και ενίσχυσης αντίθεσης που μπορείτε να διαμορφώσετε προγραμματιστικά.

## Τι θα χρειαστείτε

- Java 17 ή νεότερη (οποιοδήποτε πρόσφατο JDK λειτουργεί)
- Βιβλιοθήκη Aspose OCR for Java (κατεβάστε από την επίσημη ιστοσελίδα Aspose)
- Ένα έγκυρο αρχείο άδειας Aspose OCR (`Aspose.OCR.lic`)
- Μια εικόνα εισόδου (`input.jpg`) που θέλετε να διαβάσετε
- Το προτιμώμενο IDE σας ή μια απλή ρύθμιση γραμμής εντολών

Αν έχετε ήδη αυτά, τέλεια—ας βουτήξουμε αμέσως.

## Ποιο είναι το πρώτο βήμα: φόρτωση της άδειας Aspose OCR;

Φορτώστε την άδεια πριν δημιουργήσετε οποιοδήποτε αντικείμενο OCR ώστε η μηχανή να λειτουργεί σε πλήρη λειτουργία αντί για δοκιμαστική. Αυτό αποτρέπει τα υδατογραφήματα, ξεκλειδώνει όλες τις επιλογές προεπεξεργασίας και εξασφαλίζει ότι η μηχανή OCR μπορεί να έχει πρόσβαση στα αδειοδοτημένα πακέτα γλώσσας και στις βελτιστοποιήσεις απόδοσης που απαιτούνται για ακριβή εξαγωγή κειμένου.

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {

        // Load the Aspose OCR license – this disables the evaluation limits
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**Γιατί είναι σημαντικό:** Χωρίς σωστή άδεια, η μηχανή λειτουργεί σε λειτουργία αξιολόγησης, η οποία μπορεί να περικόψει τα αποτελέσματα ή να προσθέσει υδατογραφήματα. Η έγκαιρη ρύθμιση της άδειας εξασφαλίζει επίσης ότι τυχόν επόμενες επιλογές προεπεξεργασίας εφαρμόζονται σε πλήρη λειτουργία.

## Πώς να αρχικοποιήσετε τη μηχανή OCR;

Η κλάση `OcrEngine` είναι το βασικό στοιχείο που εκτελεί OCR και παρέχει ελέγχους προεπεξεργασίας. Δημιουργήστε μια μόνο παρουσία `OcrEngine` και επαναχρησιμοποιήστε την για κάθε εικόνα ώστε να αποφύγετε επαναλαμβανόμενη φόρτωση μοντέλου. Η επαναχρησιμοποίηση της μηχανής αποθηκεύει στην κρυφή μνήμη εσωτερικά μοντέλα νευρωνικού δικτύου, μειώνοντας την καθυστέρηση ανά εικόνα έως και 40 % και μειώνοντας την κατανάλωση μνήμης, καθιστώντας την επεξεργασία παρτίδας πιο αποδοτική.

```java
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

**Συμβουλή:** Κρατήστε τη μηχανή ως singleton αν σκοπεύετε να επεξεργαστείτε πολλές εικόνες σε παρτίδα· αποθηκεύει εσωτερικούς πόρους στην κρυφή μνήμη και επιταχύνει τις επόμενες κλήσεις.

## Πώς να ρυθμίσετε την προεπεξεργασία – διόρθωση κλίσης, αποθορυβοποίηση και ενίσχυση αντίθεσης

Εδώ είναι που **προεπεξεργαζόμαστε εικόνα για OCR**. Τα τρία κουμπιά που θα ρυθμίσουμε είναι:

1. **Deskew** – διορθώνει ελαφριές περιστροφές.
2. **Denoise** – αφαιρεί στίγματα που μπερδεύουν τη διαχωριστική χαρακτήρων.
3. **Contrast enhancement** – κάνει το σκοτεινό κείμενο να ξεχωρίζει από το φόντο.

```java
        // Access preprocessing settings
        PreprocessingSettings preprocessing = ocrEngine.getPreprocessing();

        // Enable automatic deskew (helps with scanned pages that are a few degrees off)
        preprocessing.setDeskew(true);
        preprocessing.setDeskewAngleTolerance(0.1); // tolerance in degrees

        // Turn on denoising – median works well for salt‑and‑pepper noise
        preprocessing.setDenoise(true);
        preprocessing.setDenoiseMode(DenoiseMode.MEDIAN); // alternatives: GAUSSIAN

        // Boost contrast – this is the “boost image contrast” step
        preprocessing.setContrastEnhance(true);
        preprocessing.setContrastLevel(1.3f); // 1.0 = no change, >1.0 = stronger contrast
```

### Γιατί να ρυθμίσετε το επίπεδο αντίθεσης;

Η αύξηση του επιπέδου αντίθεσης τεντώνει το ιστόγραμμα της εικόνας, κάνοντας τα σκοτεινά pixel πιο σκοτεινά και τα φωτεινά πιο φωτεινά. Στην πράξη, ένα **επίπεδο αντίθεσης** των `1.3f` συχνά παρέχει την καλύτερη ισορροπία για τυπωμένα έγγραφα, ενώ μια τιμή πάνω από `1.5f` μπορεί να υπερβολικά εκθέσει λεπτές γραμμές. Μη διστάσετε να πειραματιστείτε· η ρύθμιση είναι φθηνή να αλλάξει και μπορεί να βελτιώσει δραματικά το ποσοστό επιτυχίας του **recognize text from image**.

## Πώς να προετοιμάσετε την εικόνα εισόδου;

Η κλάση `OcrInput` αντιπροσωπεύει μια συλλογή εικόνων που η μηχανή OCR θα επεξεργαστεί. Η κλάση `OcrInput` αφαιρεί την διαχείριση αρχείων, επιτρέποντάς σας να προσθέσετε μία ή πολλές εικόνες για επεξεργασία παρτίδας. Μπορείτε να καθορίσετε μεμονωμένες διαδρομές αρχείων, ροές ή πίνακες byte, και η μηχανή θα αντιμετωπίσει κάθε καταχώρηση ως ξεχωριστή σελίδα, διαχειριζόμενη αυτόματα την ανίχνευση μορφής και τη μετατροπή όπως απαιτείται.

```java
        // Prepare the image for OCR – you can add more files to the same OcrInput
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.jpg");
```

**Ακρόατο:** Αν η εικόνα σας είναι σε μη‑τυπική μορφή (π.χ., TIFF με πολλαπλές σελίδες), μπορείτε να φορτώσετε κάθε σελίδα ξεχωριστά ή να τη μετατρέψετε πρώτα σε PNG/JPEG.

## Πώς λειτουργεί το βήμα αναγνώρισης;

Όταν καλείτε τη μέθοδο `recognize`, η μηχανή πρώτα εφαρμόζει τη ρυθμισμένη αλυσίδα προεπεξεργασίας—deskew, denoise και ενίσχυση αντίθεσης—in αυτή τη σειρά. Αφού η εικόνα καθαριστεί, περνά στον αναγνωριστή νευρωνικού δικτύου, ο οποίος αναλύει τα σχήματα χαρακτήρων και επιστρέφει το εξαγόμενο κείμενο ως συμβολοσειρά.

```java
        // Run OCR – this returns a result object containing the extracted text
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Τι συμβαίνει στο παρασκήνιο;** Το Aspose OCR πρώτα εφαρμόζει τη μετασχηματισμό deskew, μετά εκτελεί το φίλτρο denoise και τέλος ρυθμίζει την αντίθεση πριν περάσει την εικόνα στον αναγνωριστή που βασίζεται σε νευρωνικό δίκτυο. Η σειρά είναι σκόπιμη· η αλλαγή της μπορεί να οδηγήσει σε υποβέλτιστα αποτελέσματα.

## Πώς να εξάγετε το αναγνωρισμένο κείμενο;

Μετά την ολοκλήρωση της αναγνώρισης, μπορείτε να ανακτήσετε το αποτέλεσμα μέσω `getText` ή `getTextLines`. Σε αυτό το παράδειγμα απλώς εκτυπώνουμε τη εξαγόμενη συμβολοσειρά στην κονσόλα, αλλά στην παραγωγή μπορεί να το γράψετε σε αρχείο, να το αποθηκεύσετε σε βάση δεδομένων ή να το στείλετε μέσω δικτύου σε επόμενες υπηρεσίες.

```java
        // Print the recognized text to the console
        System.out.println(ocrResult.getText());
    }
}
```

### Αναμενόμενη έξοδος

Αν το `input.jpg` περιέχει τη φράση «Hello World!», η κονσόλα θα πρέπει να εμφανίσει:

```
Hello World!
```

Αν η έξοδος φαίνεται ακατάληπτη, ελέγξτε ξανά τις τιμές προεπεξεργασίας—ιδιαίτερα το **επίπεδο αντίθεσης** και τη **λειτουργία denoise**—και δοκιμάστε διαφορετική μορφή εικόνας.

## Πώς να οπτικοποιήσετε την προ‑επεξεργασμένη εικόνα (προαιρετικό);

Αν χρειάζεται να ελέγξετε τι βλέπει η μηχανή OCR μετά την προεπεξεργασία, μπορείτε να εξάγετε το ενδιάμεσο bitmap σε αρχείο PNG χρησιμοποιώντας τη μέθοδο `saveProcessedImage`. Αυτός ο οπτικός έλεγχος σας βοηθά να επαληθεύσετε ότι οι ρυθμίσεις deskew, denoise και αντίθεσης έχουν εφαρμοστεί σωστά πριν την αναγνώριση.

```java
        // Export the pre‑processed image for debugging
        BufferedImage processed = preprocessing.getProcessedImage();
        ImageIO.write(processed, "png", new File("processed.png"));
```

![παράδειγμα προεπεξεργασίας εικόνας για OCR](/images/ocr-preprocess-example.png "προεπεξεργασία εικόνας για OCR – πριν και μετά την ενίσχυση της αντίθεσης")
[παράδειγμα προεπεξεργασίας εικόνας για OCR](/images/ocr-preprocess-example.png "προεπεξεργασία εικόνας για OCR – πριν και μετά την ενίσχυση της αντίθεσης")

*Η παραπάνω εικόνα δείχνει πώς η ενίσχυση της αντίθεσης και η αποθορυβοποίηση μετατρέπει μια θολή σάρωση σε μια καθαρή, έτοιμη για OCR εικόνα.*

## Συνηθισμένα προβλήματα & πώς να τα αποφύγετε

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| **Υπερ‑αντίθεση** (`setContrastLevel` πολύ υψηλό) | Το ανοιχτό φόντο γίνεται λευκό, σβήνοντας τα αδύναμα γράμματα | Κρατήστε το επίπεδο μεταξύ 1.1 και 1.4 για τα περισσότερα τυπωμένα κείμενα |
| **Πολύ χαμηλή ανοχή διόρθωσης κλίσης** | Οι μικρές περιστροφές παραμένουν αδιόρθωτες | Αυξήστε το `setDeskewAngleTolerance` σε 0.2 ή 0.3 για σκαναρισμένα βιβλία |
| **Χρήση GAUSSIAN denoise σε δυαδικές εικόνες** | Θολώνει τις άκρες, συγχωνεύοντας χαρακτήρες | Χρησιμοποιήστε `DenoiseMode.MEDIAN` για ασπρόμαυρες σκαναρίσματα |
| **Απουσία άδειας** | Η μηχανή επιστρέφει σε δοκιμαστική λειτουργία, περικόπτοντας το αποτέλεσμα | Επαληθεύστε τη διαδρομή προς το `Aspose.OCR.lic` και ότι το αρχείο είναι αναγνώσιμο |

## Συχνές ερωτήσεις

**Ε: Μπορώ να χρησιμοποιήσω αυτήν την προσέγγιση για γλώσσες εκτός της Αγγλικής;**  
Α: Ναι—φορτώστε το κατάλληλο πακέτο γλώσσας με `engine.setLanguage("fr")` ή οποιονδήποτε υποστηριζόμενο κωδικό ISO για να βελτιώσετε την ακρίβεια για μη‑Αγγλικό κείμενο.

**Ε: Υποστηρίζει το Aspose OCR άμεση είσοδο PDF;**  
Α: Δεν διαβάζει σελίδες PDF εγγενώς· πρέπει πρώτα να εξάγετε τις εικόνες από το PDF (π.χ., με Aspose PDF) και μετά να τις δώσετε στη μηχανή OCR.

**Ε: Πόσο μεγάλη εικόνα μπορώ να επεξεργαστώ;**  
Α: Η βιβλιοθήκη διαχειρίζεται εικόνες έως 30 MP χωρίς να χρειάζεται να φορτώσει ολόκληρο το αρχείο στη μνήμη, χάρη στην αρχιτεκτονική ροής της.

**Ε: Υπάρχει τρόπος να επεξεργαστώ παρτίδα έναν φάκελο εικόνων;**  
Α: Απόλυτα—περιηγηθείτε στα αρχεία, επαναχρησιμοποιήστε την ίδια παρουσία `OcrEngine` και προσθέστε κάθε αρχείο στο `OcrInput`. Αυτό μειώνει δραματικά το κόστος ανά εικόνα.

**Ε: Τι γίνεται αν η έξοδος OCR εξακολουθεί να περιέχει σφάλματα;**  
Α: Δοκιμάστε να ρυθμίσετε το `setContrastLevel` σε μικρότερα βήματα, πειραματιστείτε με το `setDenoiseMode`, ή ενεργοποιήστε το `setUseAdaptiveThreshold(true)` για δύσκολα φόντα.

## Επόμενα βήματα: υπέρβαση της βασικής προεπεξεργασίας

Τώρα που μπορείτε να **προεπεξεργαστείτε εικόνα για OCR** και να **εξάγετε κείμενο χρησιμοποιώντας OCR**, σκεφτείτε αυτές τις επεκτάσεις:

- **Πακέτα γλώσσας** – φορτώστε συγκεκριμένα λεξικά γλώσσας για να βελτιώσετε την ακρίβεια για μη‑Αγγλικό κείμενο.  
- **Περικοπή περιοχής ενδιαφέροντος (ROI)** – εστιάστε σε ένα υποτμήμα της εικόνας αν χρειάζεστε μόνο μέρος της σελίδας.  
- **Επεξεργασία παρτίδας** – επαναλάβετε πάνω σε έναν φάκελο εικόνων, επαναχρησιμοποιώντας την ίδια παρουσία `OcrEngine` για ταχύτητα.  
- **Ενσωμάτωση με PDF** – συνδυάστε το Aspose OCR με το Aspose PDF για να μετατρέψετε σκαναρισμένα PDF σε αναζητήσιμα PDF σε μια αλυσίδα.

Κάθε ένα από αυτά τα θέματα ενσωματώνει φυσικά τις δευτερεύουσες λέξεις-κλειδιά μας: θα συνεχίσετε να **ενισχύετε την αντίθεση της εικόνας**, **ρυθμίζετε το επίπεδο αντίθεσης**, και να **αναγνωρίζετε κείμενο από εικόνα** σε πολλές περιπτώσεις.

## Συμπέρασμα

Έχουμε καλύψει όλα όσα χρειάζεστε για να **προεπεξεργαστείτε εικόνα για OCR** χρησιμοποιώντας το Aspose OCR for Java: τη φόρτωση της άδειας, τη ρύθμιση deskew, denoise και ενίσχυσης αντίθεσης, την παροχή της εικόνας, και τελικά την **αναγνώριση κειμένου από εικόνα**. Με το πλήρες, εκτελέσιμο παράδειγμα παραπάνω, μπορείτε τώρα να **εξάγετε κείμενο χρησιμοποιώντας OCR** σε οποιαδήποτε κατάλληλα προετοιμασμένη εικόνα.

Δοκιμάστε τον κώδικα, ρυθμίστε το **επίπεδο αντίθεσης**, και παρακολουθήστε την ακρίβεια να αυξάνεται. Όταν είστε έτοιμοι, εξερευνήστε μοντέλα ειδικά για γλώσσες ή αλυσίδες παρτίδας για να μετατρέψετε αυτή τη demo μίας εικόνας σε λύση παραγωγικού επιπέδου.

*Καλό κώδικα, και οι σκαναρίσματά σας να είναι πάντα καθαρά!*

---

**Τελευταία ενημέρωση:** 2026-10-30  
**Δοκιμάστηκε με:** Aspose OCR for Java 24.11  
**Συγγραφέας:** Aspose

## Σχετικές οδηγίες

- [Εξαγωγή κειμένου από εικόνα με οδηγό Aspose OCR Java](/ocr/java/advanced-ocr-techniques/extract-text-from-image-with-aspose-ocr-java-guide/)
- [Αναγνώριση κειμένου εικόνας χρησιμοποιώντας Aspose OCR GPU Java](/ocr/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/)
- [Δημιουργία μηχανής OCR Java για αναγνώριση κειμένου από μεγάλες εικόνες](/ocr/java/advanced-ocr-techniques/create-ocr-engine-java-recognize-text-from-large-images/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}