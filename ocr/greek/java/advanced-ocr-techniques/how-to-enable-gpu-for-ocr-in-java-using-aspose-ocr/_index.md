---
category: general
date: 2026-08-18
description: Πώς να ενεργοποιήσετε την GPU για OCR σε Java και να αναγνωρίσετε γρήγορα
  το κείμενο της εικόνας, να εξάγετε κείμενο JPG, να προσθέσετε φίλτρο και να ορίσετε
  τη γλώσσα με το Aspose.OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable gpu
- recognize image text
- extract text jpg
- how to add filter
- how to set language
language: el
lastmod: 2026-08-18
og_description: Πώς να ενεργοποιήσετε την GPU για OCR σε Java και να αναγνωρίζετε
  αμέσως κείμενο εικόνας, να εξάγετε κείμενο JPG, να προσθέσετε φίλτρο και να ορίσετε
  γλώσσα χρησιμοποιώντας το Aspose.OCR.
og_image_alt: Screenshot showing Java code that enables GPU for OCR with Aspose.OCR
og_title: Πώς να ενεργοποιήσετε την GPU για OCR σε Java – πλήρης οδηγός Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-08-18'
  description: How to enable GPU for OCR in Java and quickly recognize image text,
    extract text JPG, add filter, and set language with Aspose.OCR.
  headline: How to enable GPU for OCR in Java using Aspose.OCR
  type: TechArticle
- description: How to enable GPU for OCR in Java and quickly recognize image text,
    extract text JPG, add filter, and set language with Aspose.OCR.
  name: How to enable GPU for OCR in Java using Aspose.OCR
  steps:
  - name: 3.1 Set the OCR language
    text: '```java // Choose the language for recognition – this is the “how to set
      language” step engine.setLanguage(OcrLanguage.ENGLISH); ```'
  - name: 3.2 Add a preprocessing filter
    text: 'Noise, compression artifacts, or uneven lighting can hurt accuracy. Adding
      a denoise filter is the typical **how to add filter** approach:'
  - name: Expected output
    text: '``` Recognized text: The quick brown fox jumps over the lazy dog. ```'
  type: HowTo
tags:
- OCR
- Java
- Aspose
- GPU acceleration
title: Πώς να ενεργοποιήσετε την GPU για OCR σε Java χρησιμοποιώντας το Aspose.OCR
url: /el/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ενεργοποιήσετε το GPU για OCR σε Java χρησιμοποιώντας το Aspose.OCR

Αν χρειάζεστε **how to enable GPU** για OCR σε Java, αυτός ο οδηγός σας καθοδηγεί βήμα προς βήμα. Η ενεργοποίηση της επιτάχυνσης GPU σας επιτρέπει να **recognize image text** αρκετές φορές πιο γρήγορα, κάτι που είναι απαραίτητο όταν πρέπει να **extract text JPG** αρχεία μαζικά. Θα καλύψουμε επίσης **how to add filter**, **how to set language**, και πώς να ανακτήσετε το τελικό αποτέλεσμα.

Με την ολοκλήρωση αυτού του tutorial θα έχετε ένα πλήρες, εκτελέσιμο πρόγραμμα που:

* Ξεκινά τη μηχανή Aspose.OCR με υποστήριξη GPU.  
* Διαμορφώνει τη γλώσσα OCR (π.χ., English).  
* Εφαρμόζει φίλτρο αποθορυβοποίησης για βελτίωση της ακρίβειας.  
* Φορτώνει μια εικόνα JPEG, εκτελεί την αναγνώριση και εκτυπώνει το εξαγόμενο κείμενο.

> **Απαίτηση:** Java 17 ή νεότερη, Maven, και άδεια Aspose.OCR for Java (η δωρεάν δοκιμή λειτουργεί για αξιολόγηση).

---

![How to enable GPU for OCR in Java](/images/ocr-gpu.png){alt="Πώς να ενεργοποιήσετε το GPU για OCR σε Java"}

## Τι θα χρειαστείτε

| Στοιχείο | Αιτία |
|------|--------|
| **Java Development Kit (JDK) 17+** | Απαιτείται για τη μεταγλώττιση και εκτέλεση του παραδείγματος. |
| **Maven** | Απλοποιεί τη διαχείριση εξαρτήσεων για το Aspose.OCR. |
| **Aspose.OCR for Java** | Παρέχει την κλάση `OcrEngine` και υποστήριξη GPU. |
| **Δειγματική εικόνα JPEG** (`sample.jpg`) | Χρησιμοποιείται για την επίδειξη **extract text JPG**. |
| **Υλικό συμβατό με GPU** (προαιρετικό αλλά συνιστάται) | Ενεργοποιεί την επιτάχυνση απόδοσης που θα ρυθμίσουμε. |

---

## Βήμα 1: Ρύθμιση του έργου Maven

Δημιουργήστε ένα νέο έργο Maven (ή προσθέστε στο υπάρχον) και συμπεριλάβετε την εξάρτηση Aspose.OCR:

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ocr-gpu-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- Aspose.OCR for Java -->
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-ocr</artifactId>
            <version>23.12</version> <!-- Use the latest stable version -->
        </dependency>
    </dependencies>
</project>
```

> **Συμβουλή:** Κρατήστε τον αριθμό έκδοσης ενημερωμένο· οι νεότερες εκδόσεις βελτιώνουν τη διαχείριση GPU και προσθέτουν πακέτα γλωσσών.

---

## Βήμα 2: Αρχικοποίηση της μηχανής OCR και **how to enable GPU**

Η καρδιά της λύσης είναι η `OcrEngine`. Η δημιουργία της είναι απλή, αλλά πρέπει ρητά να ενεργοποιήσετε την επιτάχυνση GPU:

```java
import com.aspose.ocr.*;

public class HelloWorldOcr {
    public static void main(String[] args) throws Exception {
        // Step 2.1: Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // Step 2.2: Enable GPU acceleration (this is the “how to enable GPU” part)
        engine.setUseGpu(true); // <-- GPU is now active

        // Step 2.3: Configure language and preprocessing filter (covered later)
```

**Γιατί να ενεργοποιήσετε το GPU;**  
Όταν καλείται το `setUseGpu(true)`, το Aspose.OCR μεταφέρει τα βαριά kernels επεξεργασίας εικόνας στην κάρτα γραφικών. Σε μια σύγχρονη κάρτα NVIDIA/AMD η ταχύτητα αναγνώρισης μπορεί να αυξηθεί από ~200 ms ανά σελίδα σε < 80 ms, μειώνοντας δραστικά το συνολικό χρόνο επεξεργασίας μεγάλων παρτίδων.

---

## Βήμα 3: **How to set language** και **how to add filter**

### 3.1 Ορισμός της γλώσσας OCR

```java
        // Choose the language for recognition – this is the “how to set language” step
        engine.setLanguage(OcrLanguage.ENGLISH);
```

Το Aspose.OCR περιλαμβάνει πακέτα γλωσσών για πάνω από 100 γλώσσες. Αντικαταστήστε το `ENGLISH` με `FRENCH`, `CHINESE_SIMPLIFIED`, κ.λπ., ώστε να ταιριάζει με το υλικό σας.

### 3.2 Προσθήκη φίλτρου προεπεξεργασίας

Ο θόρυβος, τα σφάλματα συμπίεσης ή η ανώμαλη φωτισμός μπορούν να μειώσουν την ακρίβεια. Η προσθήκη φίλτρου αποθορυβοποίησης είναι η τυπική **how to add filter** προσέγγιση:

```java
        // Add a denoising filter to improve OCR quality – “how to add filter”
        engine.addPreprocessFilter(FilterType.DENOISE);
```

Άλλα χρήσιμα φίλτρα περιλαμβάνουν `FilterType.CONTRAST`, `FilterType.BRIGHTNESS` και `FilterType.BINARIZE`. Μπορείτε να συνδέσετε πολλαπλά φίλτρα καλώντας επανειλημμένα το `addPreprocessFilter`.

---

## Βήμα 4: Φόρτωση της εικόνας – **extract text JPG**

Τώρα κατευθύνουμε τη μηχανή στο αρχείο JPEG που θέλουμε να επεξεργαστούμε:

```java
        // Load the JPEG image – this demonstrates “extract text JPG”
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

Αντικαταστήστε το `YOUR_DIRECTORY` με την πραγματική διαδρομή όπου βρίσκεται το `sample.jpg`. Το Aspose.OCR υποστηρίζει επίσης PNG, BMP, TIFF και PDF· η ίδια κλήση λειτουργεί και για αυτές τις μορφές.

---

## Βήμα 5: Εκτέλεση OCR και **recognize image text**

Με τη μηχανή διαμορφωμένη, καλέστε τη διαδικασία αναγνώρισης:

```java
        // Run the OCR operation – “recognize image text”
        engine.recognize();

        // Retrieve the recognized text
        String text = engine.getText();
        System.out.println("Recognized text: " + text);
    }
}
```

Η μέθοδος `recognize()` επεξεργάζεται την εικόνα στο GPU (αν είναι ενεργοποιημένο) και γεμίζει το εσωτερικό buffer κειμένου. Το `getText()` επιστρέφει ένα `String` απλού κειμένου, το οποίο μπορείτε να γράψετε σε αρχείο, βάση δεδομένων ή να το περάσετε σε επόμενες NLP διεργασίες.

### Αναμενόμενη έξοδος

```
Recognized text: The quick brown fox jumps over the lazy dog.
```

Αν η εικόνα περιέχει πολλές γραμμές, η επιστρεφόμενη συμβολοσειρά περιλαμβάνει χαρακτήρες νέας γραμμής (`\n`) διατηρώντας την αρχική διάταξη.

---

## Βήμα 6: Επαλήθευση χρήσης GPU (προαιρετικό)

Για να βεβαιωθείτε ότι το GPU χρησιμοποιείται πράγματι, ενεργοποιήστε το logging του Aspose:

```java
        // Enable diagnostic logging (optional)
        engine.setLogLevel(com.aspose.ocr.logging.LogLevel.DEBUG);
        engine.setLogFile("ocr-debug.log");
```

Εξετάστε το `ocr-debug.log` μετά την εκτέλεση· θα πρέπει να δείτε καταχωρήσεις όπως `GPU device: NVIDIA GeForce RTX 3080` και `Processing time (GPU): 78 ms`. Αν το log αναφέρει **CPU**, ελέγξτε ξανά την εγκατάσταση του οδηγού και ότι η κλήση `setUseGpu(true)` υπάρχει.

---

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Σύμπτωμα | Πιθανή αιτία | Διόρθωση |
|---------|--------------|-----|
| **`java.lang.UnsatisfiedLinkError: no aspose_ocr_native`** | Λείπουν οι εγγενείς βιβλιοθήκες GPU | Εγκαταστήστε τον πιο πρόσφατο οδηγό GPU και βεβαιωθείτε ότι τα εγγενή binaries του `aspose-ocr` βρίσκονται στο `java.library.path`. |
| **Κακή ακρίβεια σε σκοτεινές εικόνες** | Έλλειψη φίλτρου προεπεξεργασίας | Προσθέστε `engine.addPreprocessFilter(FilterType.BRIGHTNESS)` ή αυξήστε το `FilterType.CONTRAST`. |
| **`OutOfMemoryError` σε μεγάλες παρτίδες** | Εξάντληση μνήμης GPU | Επεξεργαστείτε τις εικόνες σε μικρότερες παρτίδες ή απενεργοποιήστε το GPU (`engine.setUseGpu(false)`) για πολύ υψηλές αναλύσεις. |
| **Λανθασμένη έξοδος γλώσσας** | Λάθος γλώσσα ορίστηκε | Επαληθεύστε ότι `engine.setLanguage(OcrLanguage.YOUR_LANGUAGE)` ταιριάζει με το κείμενο προέλευσης. |

---

## Πλήρες, εκτελέσιμο παράδειγμα

Ακολουθεί η πλήρης κλάση Java που μπορείτε να αντιγράψετε στο `src/main/java/com/example/HelloWorldOcr.java`. Περιλαμβάνει όλα τα βήματα, διαχείριση σφαλμάτων και προαιρετικό logging.

```java
package com.example;

import com.aspose.ocr.*;

public class HelloWorldOcr {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // -------------------------------------------------
        // 1️⃣ Enable GPU acceleration – how to enable GPU
        // -------------------------------------------------
        engine.setUseGpu(true);

        // -------------------------------------------------
        // 2️⃣ Set language – how to set language
        // -------------------------------------------------
        engine.setLanguage(OcrLanguage.ENGLISH); // Change if needed

        // -------------------------------------------------
        // 3️⃣ Add preprocessing filter – how to add filter
        // -------------------------------------------------
        engine.addPreprocessFilter(FilterType.DENOISE);
        // Optional: engine.addPreprocessFilter(FilterType.CONTRAST);

        // -------------------------------------------------
        // 4️⃣ Load the JPEG image – extract text JPG
        // -------------------------------------------------
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        engine.setImage(ImageStream.fromFile(imagePath));

        // -------------------------------------------------
        // 5️⃣ Perform OCR – recognize image text
        // -------------------------------------------------
        engine.recognize();

        // Retrieve and display the recognized text
        String text = engine.getText();
        System.out.println("Recognized text: " + text);

        // -------------------------------------------------
        // 6️⃣ Optional: write output to a file
        // -------------------------------------------------
        java.nio.file.Files.writeString(
                java.nio.file.Paths.get("output.txt"),
                text,
                java.nio.charset.StandardCharsets.UTF_8
        );

        // -------------------------------------------------
        // 7️⃣ Optional: enable debug logging to verify GPU usage
        // -------------------------------------------------
        engine.setLogLevel(com.aspose.ocr.logging.LogLevel.DEBUG);
        engine.setLogFile("ocr-debug.log");
    }
}
```

**Εκτέλεση του προγράμματος**

```bash
mvn compile exec:java -Dexec.mainClass=com.example.HelloWorldOcr
```

Θα πρέπει να δείτε το αναγνωρισμένο κείμενο στην κονσόλα και αποθηκευμένο στο `output.txt`. Το αρχείο `ocr-debug.log` θα επιβεβαιώσει τη χρήση του GPU.

---

## Συμπέρασμα

Σε αυτό το tutorial δείξαμε **how to enable GPU** για το Aspose.OCR σε Java, πώς να **recognize image text**, **extract text JPG**, **how to add filter**, και **how to set language**—όλα μέσα σε ένα ενιαίο, αυτόνομο πρόγραμμα. Η ενεργοποίηση του GPU προσφέρει σημαντική αύξηση ταχύτητας, ενώ τα φίλτρα και οι ρυθμίσεις γλώσσας εξασφαλίζουν υψηλή ακρίβεια σε διάφορες πηγές εικόνας.

**Επόμενα βήματα**

* Πειραματιστείτε με επιπλέον φίλτρα όπως `FilterType.BINARIZE` για σαρωμένα έγγραφα.  
* Μεταβείτε σε άλλες γλώσσες (`OcrLanguage.SPANISH`, `OcrLanguage.CHINESE_SIMPLIFIED`) για να επεκτείνετε την πολυγλωσσία.  
* Συνδυάστε αυτή τη ροή OCR με το Apache PDFBox για εξαγωγή κειμένου απευθείας από σελίδες PDF.  

Αισθανθείτε ελεύθεροι να προσαρμόσετε τον κώδικα για επεξεργασία παρτίδων, να τον ενσωματώσετε σε υπηρεσία Spring Boot, ή να τον συνδέσετε με ουρά μηνυμάτων για πραγματικού χρόνου OCR. Καλή προγραμματιστική!

## Τι πρέπει να μάθετε στη συνέχεια;

Οι παρακάτω οδηγίες καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Πώς να διαβάσετε κείμενο από εικόνα σε Java χρησιμοποιώντας το Aspose OCR – Πλήρης Οδηγός](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Πώς να κάνετε OCR κειμένου εικόνας με γλώσσα χρησιμοποιώντας το Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Προεπεξεργασία εικόνας OCR σε Java με Aspose OCR – Βελτιώστε την ακρίβεια & εξάγετε κείμενο](/ocr/english/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}