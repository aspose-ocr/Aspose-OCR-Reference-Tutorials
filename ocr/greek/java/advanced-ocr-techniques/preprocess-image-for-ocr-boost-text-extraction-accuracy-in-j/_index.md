---
category: general
date: 2026-03-28
description: Προεπεξεργασία εικόνας για OCR και αναγνώριση κειμένου από εικόνα με
  το Aspose OCR. Μάθετε πώς να εξάγετε κείμενο από φωτογραφία, βελτιώνοντας την ακρίβεια
  του OCR βήμα‑βήμα.
draft: false
keywords:
- preprocess image for OCR
- recognize text from image
- extract text from photo
- improve OCR accuracy preprocessing
- Aspose OCR Java
- image preprocessing pipeline
language: el
og_description: Προεπεξεργασία εικόνας για OCR και εξαγωγή κειμένου από φωτογραφία
  με το Aspose OCR Java. Ακολουθήστε αυτό το σεμινάριο για να βελτιώσετε την ακρίβεια
  του OCR με προεπεξεργασία σε λίγα μόνο βήματα.
og_title: Προεπεξεργασία εικόνας για OCR – Πλήρης οδηγός Java
tags:
- OCR
- Java
- Image Processing
title: Προεπεξεργασία εικόνας για OCR – Βελτιώστε την ακρίβεια εξαγωγής κειμένου σε
  Java
url: /el/java/advanced-ocr-techniques/preprocess-image-for-ocr-boost-text-extraction-accuracy-in-j/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προεπεξεργασία Εικόνας για OCR – Ένας Πλήρης Οδηγός Java

Προσπαθήσατε ποτέ να **preprocess image for OCR** και να καταλήξετε με ακατάληπτο αποτέλεσμα; Δεν είστε μόνοι. Σε πολλά πραγματικά έργα, μια ακατέργαστη σάρωση ή μια λήψη από smartphone περιέχει κλίση, θόρυβο ή χαμηλή αντίθεση που αποπροσανατολίζει ακόμη και τη πιο έξυπνη μηχανή αναγνώρισης. Τα καλά νέα; Μια σύντομη αλυσίδα προεπεξεργασίας — de‑skew, denoise, binarize — μπορεί να βελτιώσει δραστικά **improve OCR accuracy preprocessing**.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα ένα πρακτικό παράδειγμα που δείχνει ακριβώς πώς να **recognize text from image** χρησιμοποιώντας το Aspose OCR for Java. Στο τέλος θα μπορείτε να **extract text from photo** αρχεία με πολύ λιγότερα σφάλματα, και θα καταλάβετε γιατί κάθε βήμα προεπεξεργασίας είναι σημαντικό.

> **What you’ll walk away with**  
> * Ένα πλήρως εκτελέσιμο πρόγραμμα Java που φορτώνει μια κεκλιμένη φωτογραφία, εφαρμόζει τρία κλασικά φίλτρα και εκτυπώνει καθαρό κείμενο.  
> * Κατανόηση του “γιατί” πίσω από de‑skew, denoise και binarize.  
> * Συμβουλές για τη διαχείριση edge cases — μεγάλα αρχεία, διαφορετικές μορφές εικόνας και προσαρμοσμένη σειρά φίλτρων.

## Προαπαιτούμενα

- Java 8 ή νεότερη εγκατεστημένη (ο κώδικας μεταγλωττίζεται επίσης με JDK 11).  
- Maven ή Gradle για λήψη της βιβλιοθήκης Aspose OCR.  
- Ένα δείγμα εικόνας (π.χ. `angled-photo.jpg`) που είναι ελαφρώς περιστραμμένο και περιέχει κάποιο οπτικό θόρυβο.  
- Βασική εξοικείωση με τη μέθοδο `main` της Java — δεν απαιτείται βαθιά εξειδίκευση στο OCR.

Αν λείπει κάτι από αυτά, απλώς κατεβάστε το τελευταίο JDK από την Oracle ή το OpenJDK και προσθέστε την ακόλουθη εξάρτηση Maven στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check Maven Central for the newest version -->
</dependency>
```

## Βήμα 1 – Δημιουργία του Αντικειμένου OCR Engine

Το πρώτο πράγμα που χρειάζεστε είναι ένα αντικείμενο `OcrEngine`. Σκεφτείτε το ως τον εγκέφαλο που θα διαβάσει αργότερα την επεξεργασμένη εικόνα.

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine – this object holds all settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **Why this matters:** Η μηχανή περιλαμβάνει ρυθμίσεις αναγνώρισης, πακέτα γλωσσών και — το πιο σημαντικό για εμάς — επιλογές προεπεξεργασίας. Χωρίς αυτήν, θα έπρεπε να συνδέετε χειροκίνητα βιβλιοθήκες επεξεργασίας εικόνας, κάτι που αναιρεί τον σκοπό μιας καθαρής αλυσίδας.

## Βήμα 2 – Δημιουργία Αλυσίδας Προεπεξεργασίας (de‑skew → denoise → binarize)

Το Aspose OCR περιλαμβάνει μια ενσωματωμένη κλάση `PreprocessingOptions` που σας επιτρέπει να στοιβάζετε φίλτρα με τη ακριβή σειρά που χρειάζεστε. Εδώ προσθέτουμε τρία φίλτρα:

1. **DE_SKEW** – ευθυγραμμίζει το περιστραμμένο κείμενο.  
2. **DENOISE** – εξομαλύνει τα σπόρια των εικονοστοιχείων που θα μπορούσαν να ληφθούν λανθασμένα ως χαρακτήρες.  
3. **BINARIZE** – μετατρέπει την εικόνα σε καθαρό μαύρο‑και‑άσπρο, διευκολύνοντας τη δουλειά της μηχανής OCR.

```java
        // Step 2: Assemble the preprocessing pipeline
        PreprocessingOptions preprocessingOptions = new PreprocessingOptions();
        preprocessingOptions.addFilter(PreprocessFilter.DE_SKEW);   // correct rotation
        preprocessingOptions.addFilter(PreprocessFilter.DENOISE);  // remove grain
        preprocessingOptions.addFilter(PreprocessFilter.BINARIZE); // high‑contrast B&W

        // Attach the pipeline to the OCR engine
        ocrEngine.getRecognitionSettings().setPreprocessingOptions(preprocessingOptions);
```

> **Pro tip:** Η σειρά των φίλτρων είναι κρίσιμη. Αν κάνετε binarize *πριν* το denoise, ο θόρυβος μπορεί να μετατραπεί σε σκληρά μαύρα στίγματα που μπερδεύουν τον αναγνωριστή. Το de‑skew πρώτα εξασφαλίζει ότι η βάση του κειμένου είναι οριζόντια, κάτι που βελτιώνει τόσο το denoise όσο και το binarize.

## Βήμα 3 – Παροχή της Εικόνας στη Μηχανή

Τώρα κατευθύνουμε τη μηχανή στο αρχείο που θέλουμε να διαβάσουμε. Η διαδρομή μπορεί να είναι απόλυτη ή σχετική με τη ρίζα του έργου σας.

```java
        // Step 3: Run OCR on the target image
        String imagePath = "YOUR_DIRECTORY/angled-photo.jpg";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

> **What if the image is huge?** Το Aspose OCR αυτόματα μειώνει εικόνες μεγαλύτερες από 2000 px στην μεγαλύτερη πλευρά, αλλά μπορείτε να το παρακάμψετε μέσω του `ocrEngine.getRecognitionSettings().setMaxImageDimension(1500)` εάν η μνήμη είναι πρόβλημα.

## Βήμα 4 – Εξαγωγή του Αναγνωρισμένου Κειμένου

Τέλος, εκτυπώνουμε τη εξαγόμενη συμβολοσειρά στην κονσόλα. Σε μια πραγματική εφαρμογή μπορεί να την γράψετε σε βάση δεδομένων, σε αρχείο ή να τη δώσετε σε μια επόμενη αλυσίδα NLP.

```java
        // Step 4: Print the result
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### Αναμενόμενη Έξοδος

Αν το `angled-photo.jpg` περιέχει την πρόταση *«The quick brown fox jumps over the lazy dog.»* θα πρέπει να δείτε κάτι σαν:

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
```

Παρατηρήστε πόσο καθαρή είναι η έξοδος — χωρίς τυχαία σύμβολα, χωρίς σπασμένες γραμμές. Αυτή είναι η δύναμη του **preprocess image for OCR**.

## Βήμα 5 – Επαλήθευση και Ρύθμιση (Προαιρετικό)

Ακόμη και με μια σταθερή αλυσίδα, μπορεί να συναντήσετε edge cases:

| Κατάσταση | Προτεινόμενη ρύθμιση |
|-----------|----------------------|
| **Πολύ χαμηλή αντίθεση** (π.χ. ξεθωριασμένα σαρωμένα έγγραφα) | Εισάγετε ένα επιπλέον φίλτρο `ContrastAdjustment` πριν το binarization. |
| **Χρωματικό φόντο** (π.χ. αποδείξεις με χρωματιστές σφραγίδες) | Προσθέστε φίλτρο `BackgroundRemoval` ή μετατρέψτε πρώτα σε γκρι κλίμακα. |
| **PDF πολλαπλών σελίδων** | Επαναλάβετε τη λούπα για κάθε εικόνα σελίδας και χρησιμοποιήστε ξανά το ίδιο `preprocessingOptions`. |

Μπορείτε να πειραματιστείτε καλώντας το `preprocessingOptions.addFilter(PreprocessFilter.CONTRAST)` ή οποιοδήποτε άλλο φίλτρο που αναφέρεται στην τεκμηρίωση του Aspose OCR API.

## Πλήρες, Εκτελέσιμο Παράδειγμα

Παρακάτω βρίσκεται το πλήρες πρόγραμμα, έτοιμο για αντιγραφή‑επικόλληση σε ένα αρχείο με όνομα `PreprocessExample.java`. Βεβαιωθείτε ότι η εξάρτηση Maven έχει λυθεί πριν το μεταγλωττίσετε.

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing: de‑skew → denoise → binarize
        PreprocessingOptions preprocessingOptions = new PreprocessingOptions();
        preprocessingOptions.addFilter(PreprocessFilter.DE_SKEW);
        preprocessingOptions.addFilter(PreprocessFilter.DENOISE);
        preprocessingOptions.addFilter(PreprocessFilter.BINARIZE);
        ocrEngine.getRecognitionSettings().setPreprocessingOptions(preprocessingOptions);

        // 3️⃣ Perform OCR on the chosen image
        String imagePath = "YOUR_DIRECTORY/angled-photo.jpg";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

        // 4️⃣ Output the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Μεταγλώττιση και εκτέλεση:

```bash
mvn compile exec:java -Dexec.mainClass=PreprocessExample
```

Θα πρέπει να δείτε το καθαρό κείμενο να εκτυπώνεται στην κονσόλα, επιβεβαιώνοντας ότι έχετε ολοκληρώσει με επιτυχία την **preprocess image for OCR** και την **recognize text from image**.

## Συχνές Ερωτήσεις & Απαντήσεις

**Q1: Λειτουργεί αυτό με αρχεία PNG ή TIFF;**  
Ναι — το Aspose OCR υποστηρίζει JPEG, PNG, BMP, TIFF και αρκετές άλλες μορφές. Η ίδια αλυσίδα προεπεξεργασίας εφαρμόζεται· η βιβλιοθήκη ανιχνεύει αυτόματα τη μορφή.

**Q2: Τι γίνεται αν χρειαστεί να εξάγω κείμενο από φωτογραφία που τραβήχτηκε με τηλέφωνο;**  
Οι φωτογραφίες από τηλέφωνο συχνά υποφέρουν από άνιση φωτισμό. Η προσθήκη ενός φίλτρου `LIGHTING_CORRECTION` πριν το binarization μπορεί να βοηθήσει. Η αλλαγή κώδικα είναι μια μόνο γραμμή:

```java
preprocessingOptions.addFilter(PreprocessFilter.LIGHTING_CORRECTION);
```

**Q3: Μπορώ να αλλάξω τη γλώσσα του OCR;**  
Απόλυτα. Μετά τη δημιουργία της μηχανής, ορίστε τη γλώσσα:

```java
ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.SPANISH);
```

**Q4: Πώς αυτό βελτιώνει την ακρίβεια του OCR μέσω προεπεξεργασίας;**  
Κάθε φίλτρο μειώνει έναν συγκεκριμένο τύπο οπτικού θορύβου. Το de‑skew ευθυγραμμίζει τις γραμμές κειμένου, το denoise αφαιρεί τυχαίες κηλίδες, και το binarize δημιουργεί μια εικόνα υψηλής αντίθεσης. Μαζί παρέχουν στο αλγόριθμο αναγνώρισης ένα πιο καθαρό σήμα, που μεταφράζεται σε υψηλότερη ακρίβεια σε επίπεδο χαρακτήρων — συχνά μια αύξηση 15‑30 % σε θορυβώδεις εισόδους.

## Επόμενα Βήματα & Σχετικά Θέματα

- **Batch processing:** Τυλίξτε τη βασική λογική σε βρόχο για να επεξεργαστείτε ολόκληρους φακέλους φωτογραφιών.  
- **Custom filter order:** Πειραματιστείτε με `BINARIZE` πριν το `DENOISE` για έγγραφα που είναι ήδη υψηλής αντίθεσης.  
- **Performance tuning:** Χρησιμοποιήστε `ocrEngine.getRecognitionSettings().setThreadCount(4)` για παράλληλη εκτέλεση σε πολυπύρημες μηχανές.  
- **Alternative libraries:** Συγκρίνετε το Aspose OCR με το Tesseract‑Java για ανοιχτού κώδικα σενάρια.  
- **Post‑processing:** Εφαρμόστε ορθογραφικό έλεγχο ή καθαρισμό με regex στην ακατέργαστη έξοδο για ακόμη πιο καθαρά αποτελέσματα.

Αναπτύσσοντας τη ροή εργασίας **preprocess image for OCR**, θα διαπιστώσετε ότι η εξαγωγή κειμένου από φωτογραφικές πηγές γίνεται μια προβλέψιμη, επαναλήψιμη εργασία αντί για πείραμα τύπου hit‑or‑miss.

---

*Έτοιμοι να ενισχύσετε τη γραμμή OCR; Πάρτε τον κώδικα, προσαρμόστε τα φίλτρα και δείτε την ακρίβεια να αυξάνεται. Αν αντιμετωπίσετε πρόβλημα, αφήστε ένα σχόλιο παρακάτω — καλή προγραμματιστική!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}