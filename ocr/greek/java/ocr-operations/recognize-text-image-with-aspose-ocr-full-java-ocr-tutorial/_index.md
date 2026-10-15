---
category: general
date: 2026-02-27
description: Μάθετε πώς να εκτελέσετε ένα παράδειγμα OCR σε Java με το Aspose OCR,
  να εξάγετε κείμενο από εικόνα, να προεπεξεργαστείτε το OCR και να δημιουργήσετε
  αναζητήσιμο PDF με OCR σε Java.
draft: false
keywords:
- recognize text image
- how to extract text
- java ocr example
- how to preprocess ocr
- aspose ocr java tutorial
og_description: παράδειγμα OCR σε Java χρησιμοποιώντας Aspose OCR – βήμα‑βήμα οδηγός
  για εξαγωγή κειμένου από εικόνα, προεπεξεργασία OCR και δημιουργία PDF με δυνατότητα
  αναζήτησης.
og_title: παράδειγμα java ocr – Αναγνώριση κειμένου σε εικόνα με Aspose OCR
tags:
- OCR
- Java
- Aspose
- GPU
title: παράδειγμα java ocr – Αναγνώριση εικόνας κειμένου με Aspose OCR – Πλήρες σεμινάριο
  Java OCR
url: /el/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# java ocr example – Αναγνώριση κειμένου σε εικόνα – Πλήρες tutorial Aspose OCR Java

Αν ψάχνετε για ένα **java ocr example** που σας επιτρέπει να **εξάγετε κείμενο από εικόνα** αρχεία γρήγορα και αξιόπιστα, βρίσκεστε στο σωστό μέρος. Σε πολλά πραγματικά έργα το μεγαλύτερο εμπόδιο δεν είναι η μηχανή OCR, αλλά η σωστή διαμόρφωση—ιδιαίτερα όταν θέλετε επιτάχυνση GPU και υψηλή ακρίβεια. Αυτό το tutorial σας οδηγεί μέσα από ένα πλήρες, εκτελέσιμο πρόγραμμα Java που δείχνει **πώς να προεπεξεργαστείτε OCR**, αξιοποιεί το fluent builder του Aspose OCR, και ακόμη υποδεικνύει τη δημιουργία ενός **searchable PDF with OCR** αργότερα.

## Γρήγορες απαντήσεις
- **Τι καλύπτει αυτό το tutorial;** Ένα πλήρες java ocr example χρησιμοποιώντας Aspose OCR, συμπεριλαμβανομένης της ρύθμισης GPU και της προεπεξεργασίας adaptive‑threshold.  
- **Χρειάζομαι GPU;** Όχι, αλλά η ενεργοποίησή του (`enableGpu(true)`) αυξάνει δραματικά την ταχύτητα επεξεργασίας σε υποστηριζόμενο υλικό.  
- **Ποια γλώσσα παρουσιάζεται;** Αγγλικά, αλλά μπορείτε να μεταβείτε σε οποιαδήποτε υποστηριζόμενη γλώσσα μέσω του builder.  
- **Πώς εξάγω κείμενο από εικόνα;** Καλέστε `ocrEngine.recognize(imagePath)` και διαβάστε `ocrResult.getText()`.  
- **Μπορώ να δημιουργήσω searchable PDF;** Ναι – μετά την εξαγωγή μπορείτε να ενσωματώσετε το επίπεδο κειμένου σε PDF με Aspose.PDF (δεν φαίνεται εδώ).

## Τι θα χρειαστείτε

Πριν βουτήξουμε, βεβαιωθείτε ότι έχετε:

- **Java Development Kit (JDK) 11 ή νεότερο** – Το Aspose OCR υποστηρίζει Java 8+, αλλά το JDK 11 προσφέρει την καλύτερη διαχείριση μονάδων.  
- **Aspose.OCR for Java** JAR (κατεβάστε από τον ιστότοπο Aspose ή προσθέστε μέσω Maven/Gradle).  
  Παράδειγμα Maven:
  ```xml
  <dependency>
      <groupId>com.aspose</groupId>
      <artifactId>aspose-ocr</artifactId>
      <version>23.10</version>
  </dependency>
  ```
- **Οδηγός συμβατός με GPU** (CUDA 11+ αν σκοπεύετε να ενεργοποιήσετε την επιτάχυνση GPU). Αν δεν έχετε GPU, ορίστε `enableGpu(false)` και ο κώδικας θα επιστρέψει σε CPU.  
- **Δείγμα εικόνας υψηλής ανάλυσης** (`sample-highres.png`) τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε, π.χ., `C:/ocr-demo/`.

Αυτό είναι όλο—χωρίς επιπλέον εγγενή δυαδικά αρχεία ή πολύπλοκα αρχεία διαμόρφωσης.

![Διάγραμμα που δείχνει τη ροή OCR για την αναγνώριση κειμένου σε εικόνα χρησιμοποιώντας Aspose OCR Java](https://example.com/ocr-pipeline.png "αναγνώριση κειμένου σε εικόνα χρησιμοποιώντας Aspose OCR Java")

*Κείμενο alt εικόνας: αναγνώριση κειμένου σε εικόνα χρησιμοποιώντας Aspose OCR Java*

## Γιατί αυτό το java ocr example είναι σημαντικό

- **Ταχύτητα:** Η επιτάχυνση GPU μπορεί να μειώσει τον χρόνο επεξεργασίας από δευτερόλεπτα σε κλάσματα δευτερολέπτου σε μεγάλες εικόνες.  
- **Ακρίβεια:** Η επιλογή της σωστής γλώσσας και η εφαρμογή **how to preprocess OCR** (adaptive threshold) βελτιώνει δραματικά την αναγνώριση χαρακτήρων.  
- **Ευελιξία:** Η ίδια μηχανή μπορεί αργότερα να χρησιμοποιηθεί για τη δημιουργία ενός **searchable PDF with OCR**, καθιστώντας τα έγγραφά σας αναζητήσιμα χωρίς επιπλέον εργαλεία.

## Βήμα 1: Ρύθμιση του OCR Engine – αναγνώριση κειμένου σε εικόνα με τις σωστές επιλογές

Το πρώτο που κάνουμε είναι να δημιουργήσουμε μια παρουσία `OcrEngine`. Το Aspose παρέχει ένα πρότυπο builder που σας επιτρέπει να αλυσίδετε κλήσεις διαμόρφωσης, κάνοντας τον κώδικα τόσο αναγνώσιμο όσο και ευέλικτο.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // Build the OCR engine:
        // • Language: English
        // • GPU acceleration: enabled
        // • Pre‑processing: Adaptive Threshold to improve contrast
        OcrEngine ocrEngine = new OcrEngineBuilder()
                .setLanguage(Language.English)          // set OCR language
                .enableGpu(true)                        // turn on GPU (requires CUDA)
                .addPreprocessFilter(PreprocessFilter.AdaptiveThreshold) // improve binarization
                .build();
```

**Γιατί είναι σημαντικό:**  
- **Επιλογή γλώσσας** πληροφορεί τη μηχανή για το σύνολο χαρακτήρων που πρέπει να περιμένει, βελτιώνοντας δραματικά την ακρίβεια.  
- **Επιτάχυνση GPU** μπορεί να μειώσει τον χρόνο επεξεργασίας από δευτερόλεπτα σε κλάσματα δευτερολέπτου για μεγάλες εικόνες.  
- **Προεπεξεργασία Adaptive‑threshold** είναι μια κλασική τεχνική για την αντιμετώπιση άνιχου φωτισμού—ακριβώς το είδος του προβλήματος που συναντάτε όταν προσπαθείτε να **how to preprocess OCR** για σαρωμένα έγγραφα.

## Βήμα 2: Αναγνώριση κειμένου σε εικόνα – Εκτέλεση του OCR

Τώρα που η μηχανή είναι έτοιμη, της παρέχουμε την εικόνα μας. Η μέθοδος `recognize` επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει το ακατέργαστο κείμενο, τις βαθμολογίες εμπιστοσύνης, και ακόμη δεδομένα bounding box αν τα χρειαστείτε αργότερα.

```java
        // Path to the high‑resolution image you want to analyze
        String imagePath = "C:/ocr-demo/sample-highres.png";

        // Perform OCR – this is where we actually recognize text image
        OcrResult ocrResult = ocrEngine.recognize(imagePath);
```

**Κύριο σημείο:** Η κλήση `recognize` είναι συγχρονισμένη· μπλοκάρει μέχρι να ολοκληρωθεί το OCR. Αν επεξεργάζεστε δεκάδες αρχεία, σκεφτείτε να το τυλίξετε σε thread pool, αλλά για μία εικόνα η απλότητα κερδίζει.

## Βήμα 3: Εξαγωγή και εμφάνιση του κειμένου – πώς να εξάγετε κείμενο από το αποτέλεσμα

Τέλος, εξάγουμε το απλό κείμενο από το αποτέλεσμα και το εκτυπώνουμε. Μπορείτε επίσης να το γράψετε σε αρχείο, να το δώσετε σε ευρετήριο αναζήτησης, ή να το περάσετε σε API μετάφρασης.

```java
        // Print the extracted text to the console
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());

        // Optional: you can also check confidence if needed
        System.out.println("Confidence: " + ocrResult.getConfidence());
    }
}
```

Όταν εκτελέσετε το πρόγραμμα, θα πρέπει να δείτε κάτι όπως:

```
=== OCR Output ===
This is a sample document.
It contains several lines of text.
The OCR engine recognized it successfully!
Confidence: 0.97
```

Αν η έξοδος φαίνεται ακατάληπτη, ελέγξτε ξανά ότι η εικόνα είναι καθαρή και ότι το βήμα **how to preprocess OCR** (adaptive threshold) ταιριάζει με τις συνθήκες φωτισμού της εικόνας.

## Συνηθισμένα προβλήματα & Pro Tips (java ocr example)

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|------------------|----------|
| **GPU δεν εντοπίστηκε** | Απουσία οδηγών CUDA ή μη συμβατό GPU | Εγκαταστήστε CUDA 11+, επαληθεύστε ότι λειτουργεί `nvidia-smi`, ή ορίστε `.enableGpu(false)` |
| **Χαμηλή ακρίβεια σε σκοτεινά φόντα** | Το adaptive threshold μπορεί να υπερ‑εξομαλύνει | Δοκιμάστε `PreprocessFilter.GaussianBlur` πριν το threshold |
| **Έλλειψη μνήμης σε τεράστιες εικόνες** | Όριο μνήμης GPU | Αλλάξτε το μέγεθος της εικόνας σε μέγιστο πλάτος 2000 px πριν το OCR, ή χρησιμοποιήστε λειτουργία CPU |
| **Λάθος γλώσσα** | Η προεπιλογή είναι Αγγλικά, αλλά το έγγραφο είναι πολυγλωσσικό | Καλέστε `.setLanguage(Language.French)` ή χρησιμοποιήστε `Language.Multilingual` |

**Pro tip:** Όταν δημιουργείτε ένα **java ocr example** για επεξεργασία σε παρτίδες, αποθηκεύστε στην cache την παρουσία `OcrEngine` αντί να την ξαναδημιουργείτε για κάθε αρχείο. Ο builder είναι φθηνός, αλλά το εγγενές πλαίσιο GPU μπορεί να είναι ακριβό στην επαναδημιουργία.

## Επέκταση του παραδείγματος – τι ακολουθεί μετά την αναγνώριση κειμένου σε εικόνα;

1. **Δημιουργία searchable PDF with OCR** – Το Aspose OCR μπορεί να ενσωματώσει το αναγνωρισμένο κείμενο ως κρυφό στρώμα, μετατρέποντας τα σαρωμένα PDF σε πλήρως αναζητήσιμα έγγραφα.  
2. **Συνδυασμός με Aspose.PDF** – Συγχωνεύστε το αποτέλεσμα OCR με τη δημιουργία PDF για να παράγετε ολοκληρωμένες ροές εργασίας εγγράφων.  
3. **Real‑time video OCR** – Καταγράψτε καρέ από webcam, τροφοδοτήστε τα στην ίδια μηχανή, και εμφανίστε ζωντανές υπότιτλους.  
4. **Post‑processing** – Χρησιμοποιήστε κανονικές εκφράσεις για να καθαρίσετε κοινά σφάλματα OCR (`"0"` vs `"O"`), ειδικά όταν **how to extract text** για αναλύσεις downstream.

## Πλήρης κώδικας πηγής (έτοιμος για αντιγραφή)

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Build the OCR engine with English language, GPU acceleration,
        // and adaptive‑threshold preprocessing
        OcrEngine ocrEngine = new OcrEngineBuilder()
                .setLanguage(Language.English)
                .enableGpu(true)
                .addPreprocessFilter(PreprocessFilter.AdaptiveThreshold)
                .build();

        // Step 2: Recognize text from a high‑resolution image
        String imagePath = "C:/ocr-demo/sample-highres.png";
        OcrResult ocrResult = ocrEngine.recognize(imagePath);

        // Step 3: Print the extracted text to the console
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
        System.out.println("Confidence: " + ocrResult.getConfidence());
    }
}
```

Αποθηκεύστε το ως `GpuOcrDemo.java`, μεταγλωττίστε με `javac -cp "aspose-ocr-23.10.jar;." GpuOcrDemo.java`, και εκτελέστε με `java -cp "aspose-ocr-23.10.jar;." GpuOcrDemo`. Αν όλα είναι ρυθμισμένα σωστά, θα δείτε το εξαγόμενο κείμενο εκτυπωμένο—απόδειξη ότι έχετε επιτυχώς **recognize text image** με το Aspose OCR.

## Συχνές Ερωτήσεις

**Q: Μπορώ να δημιουργήσω searchable PDF απευθείας από αυτό το παράδειγμα;**  
A: Ναι. Μετά την εξαγωγή του κειμένου, χρησιμοποιήστε Aspose.PDF για να δημιουργήσετε PDF και να ενσωματώσετε το OCR text layer, μετατρέποντας το αρχείο σε searchable PDF.

**Q: Τι γίνεται αν δεν έχω GPU συμβατό με CUDA;**  
A: Απλώς αλλάξτε `.enableGpu(true)` σε `.enableGpu(false)`· η μηχανή θα επιστρέψει σε λειτουργία CPU με μόνο ήπιο αντίκτυπο στην απόδοση.

**Q: Πώς διαχειρίζομαι έγγραφα πολλαπλών γλωσσών;**  
A: Χρησιμοποιήστε `Language.Multilingual` ή ορίστε το κατάλληλο enum γλώσσας για κάθε έγγραφο πριν καλέσετε `recognize`.

**Q: Υπάρχει τρόπος να επεξεργαστώ σε παρτίδες πολλές εικόνες αποδοτικά;**  
A: Ναι. Δημιουργήστε μία ενιαία παρουσία `OcrEngine`, έπειτα επαναλάβετε τη λίστα εικόνων σας, προαιρετικά χρησιμοποιώντας thread pool για παράλληλη εκτέλεση των κλήσεων `recognize`.

**Q: Πού μπορώ να βρω πιο προχωρημένα φίλτρα προεπεξεργασίας;**  
A: Το enum `PreprocessFilter` περιλαμβάνει επιλογές όπως `GaussianBlur`, `MedianFilter`, και `ContrastStretch`. Πειραματιστείτε για να δείτε ποιο λειτουργεί καλύτερα για το σύνολο εικόνων σας.

**Τελευταία ενημέρωση:** 2026-02-27  
**Δοκιμάστηκε με:** Aspose.OCR 23.10 for Java  
**Συγγραφέας:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}