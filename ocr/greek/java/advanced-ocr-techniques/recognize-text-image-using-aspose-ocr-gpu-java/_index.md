---
category: general
date: 2026-10-30
description: Μάθετε πώς να εξάγετε κείμενο από εικόνα γρήγορα με την υποστήριξη Aspose
  OCR GPU σε Java. Αυτός ο οδηγός δείχνει πώς να ορίσετε το GPU device ID και να επιτύχετε
  OCR υψηλής απόδοσης.
draft: false
keywords:
- extract text from image
- how to extract text
- aspose ocr gpu
- recognize text image java
- gpu acceleration OCR
lastmod: 2026-10-30
og_description: Μάθετε πώς να εξάγετε κείμενο από εικόνα γρήγορα με την υποστήριξη
  Aspose OCR GPU σε Java. Αυτός ο οδηγός δείχνει πώς να ορίσετε το GPU device ID για
  βέλτιστη απόδοση.
og_image_alt: 'Developer guide: extract text from image using Aspose OCR GPU in Java'
og_title: Πώς να εξάγετε κείμενο από εικόνα με το Aspose OCR GPU σε Java
schemas:
- author: Aspose
  dateModified: '2026-10-30'
  description: Learn how to extract text from image quickly with Aspose OCR GPU support
    in Java. This guide shows how to set GPU device ID and achieve high‑performance
    OCR.
  headline: How to extract text from image with Aspose OCR GPU in Java
  type: TechArticle
- questions:
  - answer: Yes—just install a valid Aspose OCR license. The free trial is for evaluation
      only.
    question: Can I use this in a commercial application?
  - answer: Absolutely; as long as the NVIDIA driver and CUDA toolkit are installed,
      the library runs on headless Linux environments.
    question: Does the GPU version work on Linux servers?
  - answer: Aspose OCR can process images up to **5000 × 5000 px** without loading
      the whole file into memory.
    question: What is the maximum image size supported?
  - answer: Replace the old JAR with the new one and update your Maven/Gradle dependency
      version number.
    question: How do I upgrade to the latest Aspose OCR version?
  - answer: Yes—`OcrResult` provides layout information, including word‑level bounding
      boxes, when you enable the `setIncludeLayout(true)` option.
    question: Is there a way to get bounding‑box coordinates for each word?
  type: FAQPage
tags:
- Java
- OCR
- Aspose
- GPU
title: Πώς να εξάγετε κείμενο από εικόνα με το Aspose OCR GPU σε Java
url: /el/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εξάγετε κείμενο από εικόνα με το Aspose OCR GPU σε Java

Αν έχετε προσπαθήσει ποτέ να **εξάγετε κείμενο από εικόνα** σε μια εφαρμογή Java και διαπιστώσατε ότι η CPU δυσκολεύεται με σαρώσεις υψηλής ανάλυσης, δεν είστε μόνοι. Πολλοί προγραμματιστές αντιμετωπίζουν προβλήματα απόδοσης όταν επεξεργάζονται μεγάλα έγγραφα. Το Aspose OCR για Java αφαιρεί αυτό το εμπόδιο, επιτρέποντάς σας να εκτελείτε OCR στην GPU, μειώνοντας δραστικά τον χρόνο επεξεργασίας. Σε αυτό το tutorial θα δείτε ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που δείχνει πώς να ορίσετε την άδεια, να ενεργοποιήσετε την επιτάχυνση GPU και **να ορίσετε το gpu device id** όταν υπάρχουν πολλαπλές κάρτες γραφικών.

## Γρήγορες απαντήσεις
- **Ποιος είναι ο πιο γρήγορος τρόπος για να εξάγετε κείμενο από εικόνα σε Java;** Χρησιμοποιήστε το Aspose OCR με επιτάχυνση GPU και ορίστε το κατάλληλο GPU device ID.  
- **Ποια έκδοση της Java απαιτείται;** Συνιστάται η Java 17 ή νεότερη για την καλύτερη απόδοση.  
- **Χρειάζομαι άδεια για υποστήριξη GPU;** Ναι—οι δυνατότητες GPU ξεκλειδώνουν μόνο με έγκυρη άδεια Aspose OCR.  
- **Μπορώ να το τρέξω σε headless server;** Απόλυτα· απαιτούνται μόνο ο οδηγός GPU και το toolkit CUDA.  
- **Πόσες γλώσσες υποστηρίζονται;** Πάνω από 30 γλώσσες, συμπεριλαμβανομένων των Αγγλικών, Κινέζικων, Αραβικών και Χίντι.

## Τι είναι η εξαγωγή κειμένου από εικόνα;
Η εξαγωγή κειμένου από μια εικόνα σημαίνει τη μετατροπή της οπτικής αναπαράστασης χαρακτήρων που αποθηκεύονται σε μορφές bitmap όπως PNG, JPG ή TIFF σε επεξεργάσιμο, αναζητήσιμο κείμενο Unicode. Αυτή η διαδικασία, γνωστή ως Optical Character Recognition (OCR), επιτρέπει επακόλουθες εργασίες όπως η δημιουργία ευρετηρίου, η μετάφραση και η εξαγωγή δεδομένων.

## Γιατί να χρησιμοποιήσετε το Aspose OCR GPU;
Το Aspose OCR αξιοποιεί την επιτάχυνση GPU για να διαχειρίζεται μεγάλες, υψηλής ανάλυσης εικόνες πολύ πιο αποδοτικά από την επεξεργασία μόνο με CPU. Υποστηρίζει πάνω από 30 μορφές εισόδου και μπορεί να επεξεργαστεί εικόνες έως 5000 × 5000 px διατηρώντας χαμηλή χρήση μνήμης, παρέχοντας έως και πέντε φορές ταχύτερη αναγνώριση σε σύγχρονες κάρτες NVIDIA GPU.

## Τι θα χρειαστείτε
- **Java 17** ή νεότερη (συμβατή με Java 8+, αλλά οι εκδόσεις LTS προσφέρουν καλύτερη απόδοση JIT).  
- **Aspose OCR for Java** βιβλιοθήκη (κατεβάστε το JAR από την ιστοσελίδα Aspose).  
- Ένα έγκυρο **αρχείο άδειας Aspose OCR** (`Aspose.OCR.lic`). Η δωρεάν δοκιμή λειτουργεί, αλλά οι δυνατότητες GPU απαιτούν έκδοση με άδεια.  
- Ένα αρχείο εικόνας (`sample-image.png`) που περιέχει καθαρό, μηχανικά αναγνώσιμο κείμενο.  
- Μια NVIDIA GPU συμβατή με CUDA (ή ισοδύναμη) με εγκατεστημένο τον κατάλληλο οδηγό.

Αν κάποιο από αυτά σας φαίνεται άγνωστο, μην ανησυχείτε—κάθε σημείο θα εξηγηθεί καθώς προχωράμε.

## Βήμα 1: προσθέστε το Aspose OCR στο έργο σας
Πρώτα, συμπεριλάβετε το JAR του Aspose OCR στο classpath σας. Αν χρησιμοποιείτε Maven, προσθέστε την ακόλουθη εξάρτηση στο `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

Για Gradle, χρησιμοποιήστε:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

Αν προτιμάτε τη χειροκίνητη μέθοδο, τοποθετήστε το JAR σε φάκελο `libs/` και προσθέστε το στη διαδρομή του module του IDE.

> **Συμβουλή:** Διατηρήστε τον αριθμό έκδοσης σύμφωνο με τις σημειώσεις έκδοσης· οι νεότερες εκδόσεις συχνά περιλαμβάνουν βελτιώσεις απόδοσης για την επεξεργασία GPU.

## Βήμα 2: φορτώστε την άδεια Aspose OCR (απαιτείται για χρήση GPU)
Χωρίς άδεια η κλήση `setEnableGpu(true)` θα επιστρέψει σιωπηλά σε λειτουργία CPU. Φορτώστε την άδεια αμέσως στην αρχή του `main`:

```java
import com.aspose.ocr.License;

// ...

License ocrLicense = new License();
ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

Αντικαταστήστε το `YOUR_DIRECTORY` με την απόλυτη ή σχετική διαδρομή όπου αποθηκεύσατε το αρχείο `.lic`. Μια εσφαλμένη διαδρομή προκαλεί `FileNotFoundException`, οπότε ελέγξτε ξανά την ορθογραφία.

## Βήμα 3: δημιουργήστε τη μηχανή OCR και ενεργοποιήστε την επιτάχυνση GPU
Η κλάση `OcrEngine` είναι το κύριο στοιχείο που εκτελεί λειτουργίες OCR σε εικόνες.

```java
import com.aspose.ocr.OcrEngine;

// ...

OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getDevice().setEnableGpu(true);       // activate GPU support
ocrEngine.getDevice().setGpuDeviceId(0);        // optional: choose GPU index (0 = first card)
```

Γιατί να ασχοληθείτε με το device ID; Σε περιβάλλον με πολλαπλές GPU μπορείτε να αφιερώσετε μία κάρτα στην προεπεξεργασία και άλλη στην OCR. Ορίζοντας το ID εξασφαλίζετε ότι η βαριά εργασία εκτελείται στο επιθυμητό υλικό.

## Βήμα 4: προετοιμάστε την εικόνα εισόδου
Η κλάση `OcrInput` αντιπροσωπεύει τη συλλογή των εικόνων που θέλετε να επεξεργαστείτε.

```java
import com.aspose.ocr.OcrInput;

// ...

OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/sample-image.png"); // path to the image you want to process
```

Αν χρειάζεται να επεξεργαστείτε ένα ρεύμα (π.χ., ένα ανεβασμένο αρχείο), χρησιμοποιήστε `ocrInput.add(InputStream)` αντί αυτού.

## Βήμα 5: εκτελέστε τη διαδικασία αναγνώρισης και ανακτήστε το αποτέλεσμα
Η κλάση `OcrResult` περιλαμβάνει το απλό κείμενο, τις βαθμολογίες εμπιστοσύνης και προαιρετικές πληροφορίες διάταξης που επιστρέφει η μηχανή.

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

Αν η εικόνα είναι θολή ή η γλώσσα δεν υποστηρίζεται, το αποτέλεσμα μπορεί να είναι κενό. Σε αυτήν την περίπτωση, ελέγξτε την τιμή `ocrResult.getConfidence()` (0‑100) για να αποφασίσετε αν θα επαναλάβετε με προεπεξεργασία.

## Πλήρες, εκτελέσιμο παράδειγμα
Συνδυάζοντας όλα τα κομμάτια παίρνετε μια μοναδική κλάση Java που μπορείτε να αντιγράψετε‑και‑επικολλήσετε στο IDE σας:

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

> **Αναμενόμενο αποτέλεσμα:** Η κονσόλα εκτυπώνει το ακριβές κείμενο που εμφανίζεται στο `sample-image.png`. Όταν η GPU είναι ενεργή, ο χρόνος επεξεργασίας συνήθως μειώνεται από αρκετά δευτερόλεπτα (CPU) σε κάτω από ένα δευτερόλεπτο για μια τυπική σάρωση 300 dpi.

## Συχνές ερωτήσεις & ειδικές περιπτώσεις

### Λειτουργεί αυτό σε headless server;
Ναι. Πρέπει να εγκατασταθεί ο οδηγός GPU, αλλά δεν απαιτείται οθόνη. Βεβαιωθείτε ότι το toolkit `CUDA` (ή το ισοδύναμο για τη GPU σας) είναι διαθέσιμο στο σύστημα `PATH`. Αυτή η ρύθμιση επιτρέπει στο OCR να εκτελείται σε περιβάλλοντα cloud ή container χωρίς γραφική διεπαφή.

### Τι γίνεται αν έχω περισσότερες από μία GPU και θέλω να χρησιμοποιήσω την GPU 1;
Αλλάξτε το device ID όπως φαίνεται:

```java
ocrEngine.getDevice().setGpuDeviceId(1); // selects the second GPU (zero‑based index)
```

Ορίζοντας το ID σε `1` κατευθύνει τη μηχανή OCR να χρησιμοποιήσει τη δεύτερη GPU του συστήματος, κάτι που μπορεί να είναι χρήσιμο όταν η πρώτη GPU είναι δεσμευμένη για άλλες εργασίες.

### Πώς να εξάγετε κείμενο από εικόνα σε διαφορετική γλώσσα;
Ορίστε τη γλώσσα πριν καλέσετε `recognize`:

```java
ocrEngine.setLanguage(OcrLanguage.FRENCH);
```

Το Aspose OCR υποστηρίζει **πάνω από 30 γλώσσες**, συμπεριλαμβανομένων των δεξιά‑προς‑αριστερά γραφών όπως η Αραβική και η Εβραϊκή. Η επιλογή της σωστής γλώσσας βελτιώνει δραματικά την ακρίβεια.

### Τι γίνεται αν η εικόνα περιέχει πολλαπλές σελίδες (π.χ., PDF μετατρεπόμενο σε εικόνες);
Δημιουργήστε ξεχωριστή καταχώρηση `OcrInput` για κάθε σελίδα ή κάντε βρόχο πάνω στα αρχεία:

```java
for (String path : imagePaths) {
    ocrInput.add(path);
}
```

Η μηχανή ενώνει τα αποτελέσματα με τη σειρά, διατηρώντας τη σειρά των σελίδων στην τελική έξοδο.

### Πώς να διαχειριστείτε αποτελέσματα χαμηλής εμπιστοσύνης;
Ελέγξτε το σκορ εμπιστοσύνης:

```java
if (ocrResult.getConfidence() < 70) {
    System.out.println("Low confidence – consider preprocessing the image.");
}
```

Τυπικά βήματα προεπεξεργασίας περιλαμβάνουν δυαδικοποίηση, μείωση θορύβου ή αλλαγή μεγέθους σε 300 dpi. Η επανεκτέλεση OCR μετά από τέτοια προεπεξεργασία συχνά αυξάνει τα επίπεδα εμπιστοσύνης.

## Συμβουλές απόδοσης
- **Επεξεργασία παρτίδας:** Η προσθήκη πολλών εικόνων σε ένα `OcrInput` μειώνει το κόστος επανειλημής εκκίνησης του context GPU.  
- **Προθέρμανση:** Εκτελέστε μια ψεύτικη αναγνώριση μία φορά μετά την εκκίνηση του JVM· η πρώτη κλήση προκαλεί καθυστέρηση αρχικοποίησης του οδηγού.  
- **Διαχείριση μνήμης:** Αποδεσμεύστε μεγάλα αντικείμενα `OcrInput` (`ocrInput.clear()`) μετά τη χρήση για να ελευθερώσετε μνήμη GPU.  

## Συμπέρασμα
Τώρα ξέρετε πώς να **εξάγετε κείμενο από εικόνα** αποδοτικά με τη μηχανή GPU του Aspose OCR σε Java, πώς να **ορίσετε το gpu device id** όταν εργάζεστε με πολλαπλές κάρτες γραφικών, και πώς να διαχειριστείτε πολυγλωσσικά σενάρια. Ο πλήρης, εκτελέσιμος κώδικας παραπάνω πρέπει να λειτουργεί αμέσως—απλώς αντικαταστήστε την άδεια και τις διαδρομές εικόνας.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε την επεξεργασία ολόκληρου φακέλου σκαναρισμένων PDF, πειραματιστείτε με διαφορετικές επιλογές `setLanguage`, ή συνδυάστε την έξοδο OCR με μοντέλο μηχανικής μάθησης για μεταεπεξεργασία. Τα κέρδη απόδοσης της επιτάχυνσης GPU καθιστούν εφικτά μεγάλης κλίμακας έργα.

Καλό προγραμματισμό, και μη διστάσετε να αφήσετε σχόλιο αν αντιμετωπίσετε προβλήματα!

## Συχνές ερωτήσεις

**Ε: Μπορώ να το χρησιμοποιήσω σε εμπορική εφαρμογή;**  
Α: Ναι—απλώς εγκαταστήστε μια έγκυρη άδεια Aspose OCR. Η δωρεάν δοκιμή είναι μόνο για αξιολόγηση.

**Ε: Λειτουργεί η έκδοση GPU σε διακομιστές Linux;**  
Α: Απόλυτα· εφόσον είναι εγκατεστημένος ο οδηγός NVIDIA και το toolkit CUDA, η βιβλιοθήκη λειτουργεί σε περιβάλλοντα Linux χωρίς οθόνη.

**Ε: Ποιο είναι το μέγιστο μέγεθος εικόνας που υποστηρίζεται;**  
Α: Το Aspose OCR μπορεί να επεξεργαστεί εικόνες έως **5000 × 5000 px** χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη.

**Ε: Πώς αναβαθμίζω στην πιο πρόσφατη έκδοση Aspose OCR;**  
Α: Αντικαταστήστε το παλιό JAR με το νέο και ενημερώστε τον αριθμό έκδοσης της εξάρτησης Maven/Gradle.

**Ε: Υπάρχει τρόπος να λάβω συντεταγμένες bounding‑box για κάθε λέξη;**  
Α: Ναι—το `OcrResult` παρέχει πληροφορίες διάταξης, συμπεριλαμβανομένων των περιοχών bounding box ανά λέξη, όταν ενεργοποιήσετε την επιλογή `setIncludeLayout(true)`.

**Τελευταία ενημέρωση:** 2026-10-30  
**Δοκιμή με:** Aspose OCR for Java 24.11  
**Συγγραφέας:** Aspose

## Σχετικά Tutorials

- [Αναγνώριση Κειμένου από Εικόνα Java OCR με Επιτάχυνση GPU](/ocr/java/advanced-ocr-techniques/recognize-text-from-image-java-ocr-with-gpu-acceleration/)
- [Πώς να Ενεργοποιήσετε GPU για OCR σε Java Εξαγωγή Κειμένου από Εικόνα](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)
- [Εξαγωγή Κειμένου από Εικόνα με Aspose OCR Java Γρήγορος Οδηγός](/ocr/java/ocr-basics/extract-text-from-image-with-aspose-ocr-java-quick-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}