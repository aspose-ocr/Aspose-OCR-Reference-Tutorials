---
category: general
date: 2026-05-31
description: Προεπεξεργαστείτε την εικόνα για OCR ώστε να βελτιώσετε δραματικά την
  ακρίβεια του OCR με προεπεξεργασία χρησιμοποιώντας το Aspose OCR Java. Ακολουθήστε
  έναν πλήρη οδηγό βήμα‑προς‑βήμα.
draft: false
keywords:
- preprocess image for OCR
- improve OCR accuracy with preprocessing
language: el
og_description: Προεπεξεργασία εικόνας για OCR και μάθετε πώς να βελτιώσετε την ακρίβεια
  του OCR με προεπεξεργασία σε Java χρησιμοποιώντας το Aspose OCR.
og_title: Προεπεξεργασία εικόνας για OCR – Βελτιώστε την ακρίβεια με την προεπεξεργασία
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Preprocess image for OCR to dramatically improve OCR accuracy with
    preprocessing using Aspose OCR Java. Follow a complete step‑by‑step guide.
  headline: Preprocess Image for OCR – Boost Accuracy with Preprocessing
  type: TechArticle
- description: Preprocess image for OCR to dramatically improve OCR accuracy with
    preprocessing using Aspose OCR Java. Follow a complete step‑by‑step guide.
  name: Preprocess Image for OCR – Boost Accuracy with Preprocessing
  steps:
  - name: Loads the original PNG.
    text: Loads the original PNG.
  - name: Feeds it through `AutoDeskew`, `DenoiseMedian`, and `ContrastStretch`.
    text: Feeds it through `AutoDeskew`, `DenoiseMedian`, and `ContrastStretch`.
  - name: Runs the recognizer on the cleaned bitmap.
    text: Runs the recognizer on the cleaned bitmap.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Προεπεξεργασία εικόνας για OCR – Αυξήστε την ακρίβεια με την προεπεξεργασία
url: /el/java/advanced-ocr-techniques/preprocess-image-for-ocr-boost-accuracy-with-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προεπεξεργασία Εικόνας για OCR – Βελτιώστε την Ακρίβεια με Προεπεξεργασία

Έχετε αναρωτηθεί ποτέ γιατί τα αποτελέσματα του OCR σας φαίνονται σαν ακατάστατο μπερδεμένο κείμενο παρόλο που η αρχική εικόνα φαίνεται εντάξει; Στις περισσότερες περιπτώσεις ο ένοχος κρύβεται μέσα στην εικόνα—κλίση, θόρυβος, χαμηλή αντίθεση—στοιχεία που μπλοκάρουν ακόμη και τον πιο έξυπνο αναγνώστη. **Preprocess image for OCR** και θα δείτε μια δραματική βελτίωση στην ποιότητα.  

Σε αυτό το tutorial δεν θα σας δείξουμε μόνο πώς να προεπεξεργαστείτε εικόνα για OCR, αλλά θα εξηγήσουμε επίσης **πώς να βελτιώσετε την ακρίβεια του OCR με προεπεξεργασία** χτίζοντας μια μικρή αλλά ισχυρή γραμμή επεξεργασίας με Aspose OCR for Java. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση πρόγραμμα που μετατρέπει ένα θορυβώδες, κεκλιμένο PNG σε καθαρό, αναγνώσιμο κείμενο.

## Τι Θα Μάθετε

- Γιατί η προεπεξεργασία είναι σημαντική για τις μηχανές OCR  
- Πώς να ρυθμίσετε το Aspose OCR σε ένα έργο Java  
- Κώδικας βήμα‑βήμα που **preprocesses image for OCR** χρησιμοποιώντας φίλτρα ευθυγράμμισης, αποθορυβοποίησης και αντίθεσης  
- Συμβουλές για την προσαρμογή της γραμμής επεξεργασίας ώστε να **improve OCR accuracy with preprocessing** στα δικά σας σύνολα δεδομένων  

Χωρίς περιττές πληροφορίες, μόνο ένα πλήρες, εκτελέσιμο παράδειγμα και η λογική πίσω από κάθε γραμμή.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

| Απαίτηση | Αιτία |
|----------|-------|
| Java 8 or newer | Η βιβλιοθήκη Aspose OCR Java στοχεύει σε Java 8+ |
| Maven or Gradle (optional) | Απλοποιεί την προσθήκη της εξάρτησης Aspose OCR |
| Aspose OCR for Java license file (`Aspose.OCR.Java.lic`) | Απαιτείται για την ενεργοποίηση πλήρους λειτουργικότητας |
| A sample image (e.g., `noisy_skewed.png`) | Η εικόνα στην οποία θα *preprocess image for OCR* |

Αν κάποιο από αυτά λείπει, σταματήστε τώρα και φροντίστε το—η εκτέλεση του κώδικα χωρίς άδεια θα προκαλέσει εξαίρεση.

## Step 1: Apply Your Aspose OCR License

Πρώτα απ' όλα. Η μηχανή OCR δεν θα κάνει τίποτα χρήσιμο χωρίς έγκυρη άδεια. Αυτό το βήμα **preprocesses image for OCR** έμμεσα, ξεκλειδώνοντας το πλήρες σύνολο φίλτρων εικόνας.

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {
        // Apply your Aspose OCR license
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");
```

> **Pro tip:** Keep the license file out of version control. Use environment variables or a secure vault in production.

## Step 2: Initialise the OCR Engine and Load the Source Image

Τώρα δημιουργούμε τη μηχανή, δηλώνουμε τη γλώσσα που περιμένουμε και την κατευθύνουμε στο αρχείο που θέλουμε να *preprocess image for OCR*.

```java
        // Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Set the language – English works for most demos
        ocrEngine.setLanguage(OcrLanguage.ENGLISH);

        // Load the source image (the one that needs preprocessing)
        ocrEngine.setImage(new OcrImage("YOUR_DIRECTORY/noisy_skewed.png"));
```

Γιατί να ορίσουμε τη γλώσσα; Επειδή η μηχανή μπορεί να εφαρμόσει γλωσσ‑συγκεκριμένες ευρετικές, που ήδη **improve OCR accuracy with preprocessing** πριν καν αγγίξουμε τα φίλτρα.

## Step 3: Build a Preprocessing Pipeline

Αυτή είναι η καρδιά του tutorial. Εδώ **preprocess image for OCR** συνδέοντας τρία φίλτρα:

| Φίλτρο | Τι κάνει | Γιατί είναι σημαντικό για την ακρίβεια |
|--------|----------|----------------------------------------|
| `AutoDeskew` | Ανιχνεύει και διορθώνει την περιστροφή | Οι κεκλιμένες γραμμές κειμένου μπερδεύουν τη διαχωριστική διαδικασία χαρακτήρων |
| `DenoiseMedian(3)` | Μείωση θορύβου με μέσο φίλτρο (πυρήνας = 3) | Αφαιρεί στίγματα που μοιάζουν με αχρείαστους χαρακτήρες |
| `ContrastStretch` | Τεντώνει το ιστόγραμμα για ενίσχυση της αντίθεσης | Σκοτεινά υπόβαθρα γίνονται αναγνώσιμα, το ανοιχτό κείμενο ξεχωρίζει |

```java
        // Access the preprocessor
        OcrPreprocessor preprocessor = ocrEngine.getPreprocessor();

        // 1️⃣ Correct image skew
        preprocessor.addFilter(new AutoDeskew());

        // 2️⃣ Reduce noise with a median filter (kernel size = 3)
        preprocessor.addFilter(new DenoiseMedian(3));

        // 3️⃣ Enhance contrast for sharper edges
        preprocessor.addFilter(new ContrastStretch());
```

Παρατηρήστε ότι δεν χρειάζεται να γράψουμε κώδικα επεξεργασίας εικόνας από το μηδέν—το Aspose παρέχει έτοιμα φίλτρα. Αυτό βελτιώνει δραματικά **improve OCR accuracy with preprocessing** ενώ διατηρεί την υλοποίηση σύντομη.

## Step 4: Run OCR on the Pre‑processed Image

Με τη γραμμή επεξεργασίας σε θέση, η μηχανή εφαρμόζει αυτόματα τα φίλτρα πριν την αναγνώριση. Το μόνο που χρειάζεστε είναι μία κλήση:

```java
        // Perform OCR on the pre‑processed image
        String extractedText = ocrEngine.recognize();
```

Πίσω από τη σκηνή η μηχανή:

1. Φορτώνει το αρχικό PNG.  
2. Το περνάει μέσω των `AutoDeskew`, `DenoiseMedian` και `ContrastStretch`.  
3. Τρέχει τον αναγνωριστή πάνω στο καθαρό bitmap.  

Αυτή είναι η μαγεία του **preprocess image for OCR**—η βαριά δουλειά αφαιρείται.

## Step 5: Output the Recognized Text

Τέλος, εκτυπώστε το αποτέλεσμα στην κονσόλα ή γράψτε το σε αρχείο. Για σκοπούς επίδειξης, ένα απλό `System.out.println` κάνει τη δουλειά.

```java
        // Show the extracted text
        System.out.println(extractedText);
    }
}
```

Αν όλα πήγαν καλά, θα δείτε καθαρές, αναγνώσιμες προτάσεις αντί για ακατάστατο κείμενο. Η ακριβής έξοδος εξαρτάται από την αρχική εικόνα, αλλά θα παρατηρήσετε σαφή βελτίωση σε σχέση με την εκτέλεση OCR στο ακατέργαστο αρχείο.

### Αναμενόμενη Έξοδος (παράδειγμα)

```
The quick brown fox jumps over the lazy dog.
This is a sample text line for OCR testing.
```

Αν εξακολουθείτε να λαμβάνετε παράξενους χαρακτήρες, ελέγξτε ξανά τη σειρά των φίλτρων—μερικές φορές η εφαρμογή του `ContrastStretch` *πριν* το `DenoiseMedian` δίνει καλύτερα αποτελέσματα σε πολύ κατεστραμμένες σάρωση.

## Οπτικοποίηση της Γραμμής Επεξεργασίας (Προαιρετικό)

Παρακάτω υπάρχει ένα σχήμα του πώς η εικόνα ρέει μέσα από κάθε φίλτρο. Μπορεί να βοηθήσει στην εξήγηση της διαδικασίας σε συναδέλφους ή στην ενσωμάτωση σε τεκμηρίωση.

![Διάγραμμα προεπεξεργασίας εικόνας για OCR](pipeline.png "Διάγραμμα που δείχνει τα στάδια AutoDeskew → DenoiseMedian → ContrastStretch για προεπεξεργασία εικόνας για OCR")

*Alt text:* *Διάγραμμα προεπεξεργασίας εικόνας για OCR που απεικονίζει τα τρία φίλτρα που εφαρμόζονται πριν από την αναγνώριση.*

## Συνηθισμένα Προβλήματα & Πώς να τα Διορθώσετε

| Σύμπτωμα | Πιθανή Αιτία | Διόρθωση |
|----------|--------------|----------|
| Το κείμενο παραμένει θολό μετά την προεπεξεργασία | Το φίλτρο αντίθεσης δεν είναι αρκετά ισχυρό | Αυξήστε τον παράγοντα τέντωσης ή δοκιμάστε το `HistogramEqualization` |
| Το OCR ρίχνει `NullPointerException` | Λάθος διαδρομή αρχείου άδειας | Επαληθεύστε τη διαδρομή και βεβαιωθείτε ότι το αρχείο είναι αναγνώσιμο |
| Η κλίση παραμένει | Περιστροφή εικόνας > 15° (όριο AutoDeskew) | Προ‑στρέψτε χειροκίνητα χρησιμοποιώντας `AffineTransform` πριν από τη γραμμή επεξεργασίας |
| Πάρα πολλές ψευδείς θετικές | Υψηλό επίπεδο θορύβου, μικρό μέγεθος πυρήνα | Αυξήστε τον πυρήνα του μέσου φίλτρου (π.χ., `new DenoiseMedian(5)`) |

Αντιλαμβανόμενοι αυτά τα ζητήματα, θα **improve OCR accuracy with preprocessing** ακόμη και στις πιο δύσκολες σάρωσες.

## Επέκταση της Γραμμής Επεξεργασίας

Θέλετε περισσότερο έλεγχο; Το Aspose OCR σας επιτρέπει να προσθέσετε προσαρμοσμένα φίλτρα ή να αλλάξετε τη σειρά των υπαρχόντων. Εδώ μερικές ιδέες:

- **Δυαδικοποίηση**: `preprocessor.addFilter(new BinarizeOtsu());` – επιβάλλει καθαρό μαύρο‑και‑λευκό, χρήσιμο για έντυπα έγγραφα.  
- **Αλλαγή Μεγέθους**: `preprocessor.addFilter(new Scale(2.0));` – αυξάνει την ανάλυση εικόνων χαμηλής ανάλυσης, συχνά βελτιώνοντας την ακρίβεια.  
- **Όξυνση**: `preprocessor.addFilter(new Sharpen());` – τονίζει τις άκρες για μικρές γραμματοσειρές.

Θυμηθείτε, κάθε επιπλέον φίλτρο προσθέτει χρόνο επεξεργασίας, οπότε κάντε benchmark στο υλικό-στόχο σας.

## Πλήρης Πηγαίος Κώδικας (Έτοιμος για Αντιγραφή‑Επικόλληση)

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply your Aspose OCR license
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // Step 2: Create the OCR engine and configure language & source image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setLanguage(OcrLanguage.ENGLISH);
        ocrEngine.setImage(new OcrImage("YOUR_DIRECTORY/noisy_skewed.png"));

        // Step 3: Build a preprocessing pipeline to improve OCR accuracy with preprocessing
        OcrPreprocessor preprocessor = ocrEngine.getPreprocessor();
        preprocessor.addFilter(new AutoDeskew());               // Correct image skew
        preprocessor.addFilter(new DenoiseMedian(3));           // Reduce noise (kernel size = 3)
        preprocessor.addFilter(new ContrastStretch());         // Enhance contrast

        // Step 4: Perform OCR on the pre‑processed image
        String extractedText = ocrEngine.recognize();

        // Step 5: Output the recognized text
        System.out.println(extractedText);
    }
}
```

Αποθηκεύστε το ως `PreprocessDemo.java`, προσθέστε το Aspose OCR JAR στο classpath σας (ή δηλώστε το στο Maven), και τρέξτε:



## Τι Θα Μάθετε Στη Σειρά;

- [Πώς να κάνετε OCR κειμένου εικόνας με γλώσσα χρησιμοποιώντας Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Εξαγωγή Κειμένου από Εικόνα Java με Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Πώς να υπολογίσετε τη γωνία κλίσης java χρησιμοποιώντας Aspose.OCR](/ocr/english/java/ocr-basics/calculate-skew-angle/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}