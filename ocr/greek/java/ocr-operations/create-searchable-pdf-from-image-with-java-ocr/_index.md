---
category: general
date: 2026-05-06
description: Δημιουργήστε αναζητήσιμο PDF από μια εικόνα χρησιμοποιώντας το Aspose
  OCR σε Java. Μάθετε πώς να μετατρέψετε την εικόνα σε PDF, να ενεργοποιήσετε τη διόρθωση
  ορθογραφίας και να χρησιμοποιήσετε το OCR GPU για γρήγορα αποτελέσματα.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- enable spell correction
- use ocr gpu
- process image ocr
language: el
og_description: Δημιουργήστε PDF με δυνατότητα αναζήτησης από μια εικόνα χρησιμοποιώντας
  το Aspose OCR σε Java. Αυτός ο οδηγός δείχνει πώς να μετατρέψετε την εικόνα σε PDF,
  να ενεργοποιήσετε τη διόρθωση ορθογραφίας και να χρησιμοποιήσετε το OCR GPU.
og_title: Δημιουργία Αναζητήσιμου PDF από Εικόνα με Java OCR
tags:
- OCR
- Java
- PDF
title: Δημιουργία Αναζητήσιμου PDF από Εικόνα με Java OCR
url: /el/java/ocr-operations/create-searchable-pdf-from-image-with-java-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Αναζητήσιμου PDF από Εικόνα με Java OCR

Έχετε ποτέ χρειαστεί να **δημιουργήσετε αναζητήσιμο PDF** από μια σαρωμένη εικόνα αλλά δεν ήξερτε από πού να ξεκινήσετε; Δεν είστε μόνοι—οι περισσότεροι προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν ασχολούνται για πρώτη φορά με PDF βασισμένα σε εικόνες. Ευτυχώς, με το Aspose OCR for Java μπορείτε να **μετατρέψετε εικόνα σε PDF**, να μετατρέψετε το κείμενο σε επιλέξιμο περιεχόμενο, και ακόμη να προσθέσετε διόρθωση ορθογραφίας για ένα πιο επαγγελματικό αποτέλεσμα.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που δείχνει πώς να **χρησιμοποιήσετε OCR GPU** όταν είναι διαθέσιμο, πώς να **επεξεργαστείτε OCR εικόνας** αποδοτικά, και γιατί η ενεργοποίηση της διόρθωσης ορθογραφίας είναι σημαντική για την αναζήτηση. Στο τέλος θα έχετε έναν τρόπο με ένα κλικ για να δημιουργήσετε ένα αναζητήσιμο PDF που μπορείτε να διανείμετε σε χρήστες ή να αρχειοθετήσετε για συμμόρφωση.

> **Pro tip:** Αν τρέχετε σε μηχάνημα χωρίς GPU, ο κώδικας επιστρέφει ήρεμα στην CPU, ώστε να μην χρειαστεί να ξαναγράψετε τίποτα.

---

## Τι Θα Χρειαστείτε

- **Java 8+** (ο κώδικας μεταγλωττίζεται με JDK 8 και νεότερα)
- **Aspose OCR for Java** library (κατεβάστε το τελευταίο JAR από τον ιστότοπο της Aspose)
- Μια **εικόνα εισόδου** (JPEG, PNG, TIFF, κ.λπ.) που θέλετε να μετατρέψετε σε αναζητήσιμο PDF
- (Προαιρετικά) Μια **GPU** με υποστήριξη CUDA αν θέλετε την ταχύτερη δυνατή αναγνώριση

Δεν απαιτούνται επιπλέον frameworks, κανένα Maven/Gradle μαγικό—απλώς ένα JAR στην classpath και είστε έτοιμοι.

## Βήμα 1: Αρχικοποίηση της Μηχανής OCR – Η Καρδιά της Διαδικασίας  

Πρώτα δημιουργούμε μια παρουσία `OcrEngine` και την κατευθύνουμε στο αρχείο πηγής. Αυτό το αντικείμενο είναι ο εργαζόμενος που θα διαβάσει την εικόνα, θα τρέξει το νευρωνικό δίκτυο και θα μας επιστρέψει το κείμενο.

```java
import com.aspose.ocr.*;

public class QuickStart {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image you want to convert
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));
```

*Why this matters:* Η αρχικοποίηση της μηχανής μία φορά και η επαναχρησιμοποίησή της αποφεύγει το κόστος φόρτωσης των εγγενών βιβλιοθηκών—μια μικρή βελτίωση απόδοσης που συσσωρεύεται όταν επεξεργάζεστε δεκάδες αρχεία σε παρτίδα.

## Βήμα 2: Επιλογή Συσκευής Επεξεργασίας – Χρήση OCR GPU Όταν Είναι Δυνατό  

Αν ο σταθμός εργασίας σας διαθέτει συμβατή GPU, μπορείτε να πείτε στο Aspose να εκτελεί το βαρέως τύπου έργο εκεί. Διαφορετικά η μηχανή μεταβαίνει αυτόματα στην CPU.

```java
        // Prefer GPU; fall back to CPU if no compatible device is found
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);
```

*What’s the benefit?* Η επιτάχυνση με GPU μπορεί να εξοικονομήσει δευτερόλεπτα ανά σελίδα, ειδικά για σαρώσεις υψηλής ανάλυσης. Η εναλλακτική λύση εξασφαλίζει ότι ο ίδιος κώδικας λειτουργεί παντού, γι’ αυτό συνιστούμε **use OCR GPU** ως προεπιλογή.

## Βήμα 3: Επιτάχυνση Σάρωσης – Εκμετάλλευση Όλων των Πυρήνων CPU  

Ακόμη και όταν η GPU είναι απασχολημένη, τα περιβάλλοντα βήματα προεπεξεργασίας μπορούν να παραλληλοποιηθούν. Ορίζοντας τον αριθμό νημάτων στο πλήθος των διαθέσιμων επεξεργαστών δίνει στη μηχανή την ευκαιρία να επεξεργαστεί πολλαπλά τμήματα ταυτόχρονα.

```java
        // Use all logical cores for preprocessing and language detection
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());
```

*Note:* Σε ένα laptop με 4 πυρήνες αυτό θα δημιουργήσει τέσσερα νήματα· σε έναν σταθμό εργασίας με 16 πυρήνες θα έχετε το πλήρες όφελος. Να θυμάστε ότι περισσότερα νήματα σημαίνουν μεγαλύτερη χρήση μνήμης.

## Βήμα 4: Καθαρισμός Εικόνας – Φίλτρα Προ‑επεξεργασίας  

Μια θολή ή θορυβώδης σάρωση θα παράγει άχρηστο κείμενο. Η προσθήκη μερικών ενσωματωμένων φίλτρων βελτιώνει δραστικά την ακρίβεια.

```java
        // Deskew the image so text lines are horizontal
        ocrEngine.getPreprocessing().add(new DeskewFilter());

        // Remove speckles and background noise
        ocrEngine.getPreprocessing().add(new NoiseRemovalFilter());
```

*Why these filters?* Το `DeskewFilter` διορθώνει την περιστροφή που συχνά εμφανίζεται όταν ένα έγγραφο τροφοδοτείται στον σαρωτή υπό γωνία. Το `NoiseRemovalFilter` αφαιρεί ανεπιθύμητα pixel που διαφορετικά θα ερμηνευτούν ως χαρακτήρες. Σκεφτείτε το ως παροχή ενός καθαρού φύλλου χαρτιού στη μηχανή OCR.

## Βήμα 5: Ενεργοποίηση Έξυπνων Λειτουργιών – Διόρθωση Ορθογραφίας & Αυτόματη Ανίχνευση Γλώσσας  

Αν εργάζεστε με πολυγλωσσικά έγγραφα, ή απλώς θέλετε λιγότερα τυπογραφικά λάθη, ενεργοποιήστε τον ενσωματωμένο ελεγκτή ορθογραφίας και αφήστε τη μηχανή να μαντέψει τη γλώσσα.

```java
        // Activate spell correction to fix common OCR mistakes
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Let the engine automatically detect the language of the input
        ocrEngine.getSettings().setAutoDetectLanguage(true);
```

*When is this useful?* Υποθέστε ότι η σάρωση περιέχει τόσο αγγλικά όσο και ισπανικά τμήματα. Η λειτουργία αυτόματης ανίχνευσης εναλλάσσει λεξικά σε πραγματικό χρόνο, ενώ η διόρθωση ορθογραφίας καθαρίζει λανθασμένα αναγνωσμένους χαρακτήρες όπως το “0” αντί για “O”. Αυτό το βήμα είναι ουσιώδες για την παραγωγή ενός **αναζητήσιμου PDF** που επιστρέφει σωστά αποτελέσματα.

## Βήμα 6: Αποθήκευση Αποτελέσματος – Μετατροπή Εικόνας σε PDF και Κατάσταση Αναζητήσιμου  

Τέλος ζητάμε από τη μηχανή να γράψει ένα PDF όπου η αρχική εικόνα βρίσκεται πίσω από ένα αόρατο στρώμα κειμένου. Αυτή είναι η κλασική ροή εργασίας **convert image to PDF**, αλλά το PDF είναι πλέον αναζητήσιμο.

```java
        // Generate a searchable PDF – the text layer sits behind the original image
        ocrEngine.save("YOUR_DIRECTORY/output-searchable.pdf", OcrSaveFormat.PDF_SEARCHABLE);

        System.out.println("Searchable PDF generated successfully.");
    }
}
```

Το αρχείο εξόδου (`output-searchable.pdf`) μπορεί να ανοιχθεί σε οποιονδήποτε προβολέα PDF· θα μπορείτε να επιλέγετε, να αντιγράφετε και να αναζητάτε το κείμενο όπως σε ένα εγγενές PDF. Δεν απαιτούνται επιπλέον εργαλεία.

## Πλήρες Παράδειγμα – Αντιγραφή‑και‑Εκτέλεση  

Παρακάτω βρίσκεται ολόκληρο το πρόγραμμα, έτοιμο για μεταγλώττιση. Αντικαταστήστε το `YOUR_DIRECTORY` με το φάκελο που περιέχει το `input.jpg`.

```java
import com.aspose.ocr.*;

public class QuickStart {
    public static void main(String[] args) throws Exception {
        // Step 1: Create the OCR engine and load the source image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));

        // Step 2: Select the processing device (GPU if available, otherwise CPU)
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);

        // Step 3: Use all available CPU cores to speed up recognition
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Step 4: Add preprocessing filters to improve image quality
        ocrEngine.getPreprocessing().add(new DeskewFilter());
        ocrEngine.getPreprocessing().add(new NoiseRemovalFilter());

        // Step 5: Enable spell correction and automatic language detection
        ocrEngine.getSettings().setEnableSpellCorrection(true);
        ocrEngine.getSettings().setAutoDetectLanguage(true);

        // Step 6: Perform OCR and save the result as a searchable PDF
        ocrEngine.save("YOUR_DIRECTORY/output-searchable.pdf", OcrSaveFormat.PDF_SEARCHABLE);

        System.out.println("Searchable PDF generated successfully.");
    }
}
```

**Expected output:** Όταν τρέξετε το πρόγραμμα θα δείτε τη γραμμή κονσόλας *“Searchable PDF generated successfully.”* Το άνοιγμα του `output-searchable.pdf` στο Adobe Reader σας επιτρέπει να πληκτρολογήσετε μια λέξη από την αρχική εικόνα στο πεδίο αναζήτησης και να μεταβείτε αμέσως στη θέση της.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις  

- **What if the GPU isn’t detected?**  
  Η κλήση `setDeviceType(OcrDeviceType.GPU)` δεν πετάει εξαίρεση· απλώς υποδεικνύει στη μηχανή να δοκιμάσει πρώτα την GPU. Αν αποτύχει, η μηχανή επιστρέφει σιωπηλά στην CPU.

- **Can I process multiple images in one run?**  
  Ναι. Τυλίξτε τον κώδικα μέσα σε βρόχο, αλλάξτε το όνομα αρχείου σε κάθε επανάληψη, και επαναχρησιμοποιήστε την ίδια παρουσία `OcrEngine` για να κρατήσετε τη χρήση μνήμης χαμηλή.

- **My PDF is huge—how do I shrink it?**  
  Μετά το OCR μπορείτε να χρησιμοποιήσετε τα API βελτιστοποίησης PDF της Aspose, ή απλώς να μειώσετε την ανάλυση της πηγαίας εικόνας πριν τη δώσετε στη μηχανή (`ImageStream.fromFile(...).setResolution(150)` για 150 DPI).

- **I need to keep the original image resolution for legal compliance.**  
  Η μορφή `PDF_SEARCHABLE` διατηρεί το αρχικό bitmap ακριβώς· το αόρατο στρώμα κειμένου προστίθεται από πάνω χωρίς να αλλάξει η οπτική ποιότητα.

## Οπτική Σύνοψη  

![create searchable pdf example](placeholder-image.png "create searchable pdf example")

*Alt text:* *παράδειγμα δημιουργίας αναζητήσιμου pdf – Μηχανή Java OCR που μετατρέπει ένα σαρωμένο JPG σε αναζητήσιμο PDF.*

## Συμπέρασμα  

Τώρα έχετε μια **πλήρη, end‑to‑end λύση** για τη μετατροπή οποιασδήποτε εικόνας σε **αναζητήσιμο PDF** χρησιμοποιώντας το Aspose OCR for Java. Με **convert image to PDF**, **enabling spell correction**, και **using OCR GPU** όταν είναι δυνατό, λαμβάνετε γρήγορα, ακριβή και αναζητήσιμα αποτελέσματα που λειτουργούν σε όλες τις πλατφόρμες.

Τι ακολουθεί; Δοκιμάστε:

- **Different output formats** (`PDF`, `DOCX`, `HTML`) για να δείτε πώς συμπεριφέρεται το στρώμα κειμένου.
- **Custom dictionaries** αν επεξεργάζεστε ειδική ορολογία.
- **Batch processing** για αυτόματη διαχείριση χιλιάδων σαρώσεων.

Αισθανθείτε ελεύθεροι να ρυθμίσετε τον αριθμό νημάτων, να αλλάξετε φίλτρα, ή να ενσωματώσετε τη δική σας γραμμή προεπεξεργασίας. Το βασικό μοτίβο παραμένει το ίδιο: load → preprocess → configure → OCR → save.

Καλή προγραμματιστική, και οι PDF σας να είναι πάντα αναζητήσιμοι!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}