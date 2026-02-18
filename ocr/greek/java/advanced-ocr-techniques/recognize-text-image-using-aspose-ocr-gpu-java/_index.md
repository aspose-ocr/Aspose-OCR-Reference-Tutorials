---
category: general
date: 2026-02-17
description: Αναγνωρίστε γρήγορα κείμενο σε εικόνα με την υποστήριξη GPU του Aspose
  OCR στη Java. Μάθετε πώς να εξάγετε κείμενο από εικόνα και να ορίσετε το ID της
  συσκευής GPU για βέλτιστη απόδοση.
draft: false
keywords:
- recognize text image
- extract text from image
- set gpu device id
- Aspose OCR Java
- GPU acceleration OCR
language: el
og_description: Αναγνωρίστε γρήγορα κείμενο σε εικόνα με την υποστήριξη GPU του Aspose
  OCR σε Java. Αυτός ο οδηγός δείχνει πώς να εξάγετε κείμενο από εικόνα και να ορίσετε
  το αναγνωριστικό της συσκευής GPU.
og_title: Αναγνώριση κειμένου σε εικόνα με Aspose OCR GPU – Java
tags:
- Java
- OCR
- Aspose
- GPU
title: Αναγνώριση κειμένου σε εικόνα με Aspose OCR GPU – Java
url: /el/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση κειμένου σε εικόνα με Aspose OCR GPU – Java

Έχετε ποτέ χρειαστεί να **αναγνωρίσετε κείμενο σε εικόνα** σε μια εφαρμογή Java, αλλά η CPU να κολλάει με μεγάλα αρχεία; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν επεξεργάζονται σαρώσεις υψηλής ανάλυσης. Τα καλά νέα; Το Aspose OCR σας επιτρέπει να **εξάγετε κείμενο από εικόνα** στην GPU, μειώνοντας δραστικά το χρόνο επεξεργασίας.  

Σε αυτό το tutorial θα περάσουμε βήμα-βήμα από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που δείχνει ακριβώς πώς να ρυθμίσετε την άδεια, να ενεργοποιήσετε την επιτάχυνση GPU και να **ορίσετε το gpu device id** όταν έχετε πολλαπλές κάρτες γραφικών. Στο τέλος θα έχετε ένα αυτόνομο πρόγραμμα που εκτυπώνει το αναγνωρισμένο κείμενο στην κονσόλα—χωρίς επιπλέον βήματα.

## Τι Θα Χρειαστεί

- **Java 17** ή νεότερη (το API είναι συμβατό με Java 8+, αλλά η πιο πρόσφατη LTS προσφέρει καλύτερη απόδοση).  
- **Aspose OCR for Java** βιβλιοθήκη (κατεβάστε το JAR από την ιστοσελίδα Aspose).  
- Ένα έγκυρο **Aspose OCR license file** (`Aspose.OCR.lic`). Η δωρεάν δοκιμή λειτουργεί, αλλά οι δυνατότητες GPU είναι κλειδωμένες πίσω από μια αδειοδοτημένη έκδοση.  
- Ένα αρχείο εικόνας (`sample-image.png`) που περιέχει καθαρό, μηχανικά αναγνώσιμο κείμενο.  
- Ένα περιβάλλον με ενεργοποιημένη GPU (η κάρτα NVIDIA CUDA‑compatible είναι η καλύτερη).  

Αν κάποιο από αυτά σας φαίνεται άγνωστο, μην ανησυχείτε—κάθε σημείο θα εξηγηθεί καθώς προχωράμε.

## Βήμα 1: Προσθήκη Aspose OCR στο Έργο Σας

Αρχικά, συμπεριλάβετε το JAR του Aspose OCR στο classpath σας. Αν χρησιμοποιείτε Maven, προσθέστε την παρακάτω εξάρτηση στο `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

Για Gradle, είναι:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

Αν προτιμάτε τη χειροκίνητη προσέγγιση, τοποθετήστε το JAR στον φάκελο `libs/` και προσθέστε το στη διαδρομή του module του IDE.

> **Pro tip:** Διατηρήστε τον αριθμό έκδοσης σε συγχρονισμό με τις σημειώσεις κυκλοφορίας της βιβλιοθήκης· οι νεότερες εκδόσεις συχνά φέρνουν βελτιώσεις απόδοσης για την επεξεργασία GPU.

## Βήμα 2: Φόρτωση της Άδειας Aspose OCR (απαιτείται για χρήση GPU)

Χωρίς άδεια η κλήση `setEnableGpu(true)` θα επιστρέψει σιωπηλά σε λειτουργία CPU. Φορτώστε την άδεια ακριβώς στην αρχή του `main`:

```java
import com.aspose.ocr.License;

// ...

License ocrLicense = new License();
ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

Αντικαταστήστε το `YOUR_DIRECTORY` με την απόλυτη ή σχετική διαδρομή όπου αποθηκεύσατε το αρχείο `.lic`. Αν η διαδρομή είναι λανθασμένη, το Aspose θα ρίξει ένα `FileNotFoundException`, οπότε ελέγξτε ξανά την ορθογραφία.

## Βήμα 3: Δημιουργία του OCR engine και ενεργοποίηση επιτάχυνσης GPU

Τώρα δημιουργούμε ένα αντικείμενο `OcrEngine` και του λέμε να χρησιμοποιήσει την GPU. Η μέθοδος `setGpuDeviceId` σας επιτρέπει να επιλέξετε μια συγκεκριμένη κάρτα όταν υπάρχουν περισσότερες από μία.

```java
import com.aspose.ocr.OcrEngine;

// ...

OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getDevice().setEnableGpu(true);       // activate GPU support
ocrEngine.getDevice().setGpuDeviceId(0);        // optional: choose GPU index (0 = first card)
```

Γιατί να ασχοληθείτε με το device ID; Σε έναν server με πολλαπλές GPU μπορεί να κρατήσετε μια κάρτα για προεπεξεργασία εικόνας και άλλη για OCR. Ορίζοντας το ID εξασφαλίζετε ότι το σωστό υλικό κάνει τη βαριά δουλειά.

## Βήμα 4: Προετοιμασία της εικόνας εισόδου

Το Aspose OCR λειτουργεί με μια ποικιλία μορφών (PNG, JPG, BMP, TIFF). Τυλίξτε το αρχείο σας σε ένα αντικείμενο `OcrInput`:

```java
import com.aspose.ocr.OcrInput;

// ...

OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/sample-image.png"); // path to the image you want to process
```

Αν χρειάζεται να επεξεργαστείτε ένα stream (π.χ., ένα ανεβασμένο αρχείο), χρησιμοποιήστε `ocrInput.add(InputStream)` αντί αυτού.

## Βήμα 5: Εκτέλεση της διαδικασίας αναγνώρισης και λήψη του αποτελέσματος

Η μέθοδος `recognize` επιστρέφει ένα `OcrResult` που περιέχει το απλό κείμενο, τις βαθμολογίες εμπιστοσύνης και ακόμη και πληροφορίες διάταξης αν τις χρειάζεστε.

```java
import com.aspose.ocr.OcrResult;

// ...

OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("Recognized text:\n" + ocrResult.getText());
```

Η κονσόλα θα εμφανίσει κάτι όπως:

```
Recognized text:
Hello, world!
This is a sample image.
```

Αν η εικόνα είναι θολή ή η γλώσσα δεν υποστηρίζεται, το αποτέλεσμα μπορεί να είναι κενό. Σε αυτή την περίπτωση, ελέγξτε την τιμή `ocrResult.getConfidence()` (0‑100) για να αποφασίσετε αν θα ξαναπροσπαθήσετε με προεπεξεργασία.

## Πλήρες, Εκτελέσιμο Παράδειγμα

Συνδυάζοντας όλα τα κομμάτια μαζί, παίρνετε μια μοναδική κλάση Java που μπορείτε να αντιγράψετε‑επικολλήσετε στο IDE σας:

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license – required for GPU usage
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // 2️⃣ Create OCR engine and turn on GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getDevice().setEnableGpu(true);      // enable GPU acceleration
        ocrEngine.getDevice().setGpuDeviceId(0);       // optional: select GPU index

        // 3️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/sample-image.png");

        // 4️⃣ Perform recognition
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 5️⃣ Output the recognized text
        System.out.println("Recognized text:\n" + ocrResult.getText());
    }
}
```

> **Expected output:** Η κονσόλα εκτυπώνει το ακριβές κείμενο που εμφανίζεται στο `sample-image.png`. Αν η GPU είναι ενεργή, θα παρατηρήσετε ότι ο χρόνος επεξεργασίας μειώνεται από αρκετά δευτερόλεπτα (CPU) σε κάτω από ένα δευτερόλεπτο για τυπικές σαρώσεις 300 dpi.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Λειτουργεί αυτό σε headless server;

Ναι. Ο οδηγός GPU πρέπει να είναι εγκατεστημένος, αλλά δεν απαιτείται οθόνη. Απλώς βεβαιωθείτε ότι το toolkit `CUDA` (ή το ισοδύναμο για την GPU σας) βρίσκεται στο σύστημα `PATH`.

### Τι γίνεται αν έχω περισσότερες από μία GPU και θέλω να χρησιμοποιήσω την GPU 1;

Αλλάξτε το device ID:

```java
ocrEngine.getDevice().setGpuDeviceId(1); // selects the second GPU (zero‑based index)
```

### Πώς να εξάγετε κείμενο από εικόνα σε διαφορετική γλώσσα;

Ορίστε τη γλώσσα πριν καλέσετε `recognize`:

```java
ocrEngine.setLanguage(OcrLanguage.FRENCH);
```

Το Aspose υποστηρίζει πάνω από 30 γλώσσες· δείτε τα API docs για την πλήρη απαρίθμηση.

### Τι γίνεται αν η εικόνα περιέχει πολλαπλές σελίδες (π.χ., PDF μετατρεπόμενο σε εικόνες);

Δημιουργήστε μια ξεχωριστή καταχώρηση `OcrInput` για κάθε σελίδα, ή κάντε βρόχο πάνω στα αρχεία:

```java
for (String path : imagePaths) {
    ocrInput.add(path);
}
```

Η μηχανή θα συνενώσει τα αποτελέσματα με τη σωστή σειρά.

### Πώς να διαχειριστείτε αποτελέσματα χαμηλής εμπιστοσύνης;

Ελέγξτε το σκορ εμπιστοσύνης:

```java
if (ocrResult.getConfidence() < 70) {
    System.out.println("Low confidence – consider preprocessing the image.");
}
```

Τυπικά βήματα προεπεξεργασίας περιλαμβάνουν δυαδικοποίηση, μείωση θορύβου ή αλλαγή μεγέθους σε 300 dpi.

## Συμβουλές Απόδοσης

- **Batch processing:** Η προσθήκη πολλών εικόνων σε ένα μόνο `OcrInput` μειώνει το κόστος επανειλημμένης εκκίνησης του GPU context.  
- **Warm‑up:** Εκτελέστε μια ψεύτικη αναγνώριση μία φορά μετά την εκκίνηση του JVM· η πρώτη κλήση προκαλεί καθυστέρηση αρχικοποίησης του οδηγού.  
- **Memory management:** Αποδεσμεύστε μεγάλα αντικείμενα `OcrInput` (`ocrInput.clear()`) μετά τη χρήση για να ελευθερώσετε μνήμη GPU.  

## Συμπέρασμα

Τώρα ξέρετε πώς να **αναγνωρίζετε κείμενο σε εικόνα** αποδοτικά με τη μηχανή GPU του Aspose OCR σε Java, πώς να **εξάγετε κείμενο από εικόνα** σε οποιαδήποτε υποστηριζόμενη γλώσσα, και πώς να **ορίσετε το gpu device id** όταν εργάζεστε με πολλαπλές κάρτες γραφικών. Ο πλήρης, εκτελέσιμος κώδικας παραπάνω θα λειτουργήσει αμέσως—απλώς αντικαταστήστε την άδεια και τις διαδρομές των εικόνων.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε την επεξεργασία ενός φακέλου σαρωμένων PDF, πειραματιστείτε με διαφορετικές επιλογές `setLanguage`, ή συνδυάστε το OCR με μοντέλο μηχανικής μάθησης για μεταεπεξεργασία. Οι δυνατότητες είναι ατελείωτες, και τα κέρδη απόδοσης της επιτάχυνσης GPU κάνουν ακόμη και μεγάλης κλίμακας έργα εφικτά.

Καλό κώδικα, και μη διστάσετε να αφήσετε ένα σχόλιο αν συναντήσετε κάποιο πρόβλημα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}