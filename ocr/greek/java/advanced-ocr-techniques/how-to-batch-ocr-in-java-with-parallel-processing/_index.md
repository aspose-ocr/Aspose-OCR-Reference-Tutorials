---
category: general
date: 2026-04-26
description: Πώς να κάνετε παρτίδα OCR χρησιμοποιώντας Java και Aspose OCR – αναγνώριση
  κειμένου από εικόνες, εξαγωγή κειμένου από PNG και χρήση όλων των πυρήνων CPU για
  παράλληλη επεξεργασία OCR.
draft: false
keywords:
- how to batch OCR
- recognize text from images
- extract text from PNG
- use all CPU cores
- parallel OCR processing
language: el
og_description: Πώς να εκτελείτε ομαδική OCR σε Java. Μάθετε να αναγνωρίζετε κείμενο
  από εικόνες, να εξάγετε κείμενο από PNG και να χρησιμοποιείτε όλους τους πυρήνες
  CPU για γρήγορη παράλληλη επεξεργασία OCR.
og_title: Πώς να εκτελέσετε ομαδική OCR σε Java – Οδηγός παράλληλης επεξεργασίας
tags:
- OCR
- Java
- Aspose
- Performance
title: Πώς να κάνετε ομαδική OCR σε Java με παράλληλη επεξεργασία
url: /el/java/advanced-ocr-techniques/how-to-batch-ocr-in-java-with-parallel-processing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να κάνετε Batch OCR σε Java – Ένας Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να κάνετε batch OCR** όταν έχετε δεκάδες PNG στιγμιότυπα που σας κοιτάζουν; Δεν είστε μόνοι. Οι περισσότεροι προγραμματιστές συναντούν πρόβλημα μόλις η επίδειξη με μία εικόνα λειτουργεί και το πραγματικό φορτίο εργασίας — εκατοντάδες αρχεία — αρχίζει να κατακλύζει την CPU.  

Σε αυτό το tutorial θα περάσουμε από μια πρακτική, ολοκληρωμένη λύση που **αναγνωρίζει κείμενο από εικόνες**, εξάγει το περιεχόμενο κάθε PNG και **χρησιμοποιεί όλους τους πυρήνες της CPU** για να επιταχύνει τη δουλειά. Στο τέλος θα έχετε μια επαναχρησιμοποιήσιμη κλάση Java που επεξεργάζεται έναν φάκελο εικόνων παράλληλα, προσφέροντάς σας την ταχύτητα μιας πολυνηματικής μηχανής χωρίς τον κόπο της διαχείρισης των thread pools.

> **Τι θα πάρετε:** ένα πλήρως εκτελέσιμο πρόγραμμα Java (Aspose OCR), εξηγήσεις βήμα‑βήμα, συμβουλές για ειδικές περιπτώσεις και μια προεπισκόπηση της αναμενόμενης εξόδου της κονσόλας.

---

## Προαπαιτούμενα

Πριν βουτήξουμε, βεβαιωθείτε ότι έχετε:

- **Java 17** (ή οποιοδήποτε πρόσφατο JDK) εγκατεστημένο και ρυθμισμένο `JAVA_HOME`.  
- **Aspose OCR for Java** βιβλιοθήκη (έκδοση 23.10 ή νεότερη). Μπορείτε να την κατεβάσετε από το Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

- Ένα φάκελο που περιέχει μερικές **PNG εικόνες** που θέλετε να επεξεργαστείτε.  
- Βασική εξοικείωση με τη σύνταξη της Java — δεν απαιτείται τίποτα περίπλοκο.

Αν κάτι από αυτά σας φαίνεται άγνωστο, κάντε παύση εδώ και ρυθμίστε τα· το υπόλοιπο του οδηγού υποθέτει ότι είναι έτοιμα.

---

## Βήμα 1 – Δημιουργία Μονονηματικού OCR Engine (Η Βάση)

Πρώτα απ' όλα: δημιουργήστε ένα αντικείμενο `OcrEngine`. Αυτό το αντικείμενο κάνει το σκληρό έργο — φορτώνει την εικόνα, εκτελεί το νευρωνικό δίκτυο και επιστρέφει απλό κείμενο.

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **Γιατί είναι σημαντικό:** Η επαναχρησιμοποίηση του ίδιου engine σε πολλά αρχεία αποφεύγει το κόστος φόρτωσης των μοντέλων γλώσσας ξανά και ξανά, κάτι που μπορεί να είναι καταστροφικό για την απόδοση όταν κάνετε **batch processing**.

---

## Βήμα 2 – Ενεργοποίηση Παράλληλης Επεξεργασίας με Όλους τους Διαθέσιμους Πυρήνες

Τώρα λέμε στο Aspose OCR να διανείμει τη δουλειά σε κάθε λογικό επεξεργαστή που προσφέρει το μηχάνημά σας. Η κλήση `Runtime.getRuntime().availableProcessors()` επιστρέφει αυτόν τον αριθμό, είτε έχετε laptop με 4‑πυρήνες είτε server με 32‑πυρήνες.

```java
        // Step 2: Enable parallel processing by using all available logical processors
        ocrEngine.getRecognitionSettings()
                 .setNumberOfThreads(Runtime.getRuntime().availableProcessors());
```

> **Συμβουλή:** Σε CPU με hyper‑threading θα δείτε διπλάσιο αριθμό πυρήνων, αλλά η βιβλιοθήκη περιορίζει το thread pool έξυπνα, ώστε να μην χρειάζεται να το ρυθμίσετε χειροκίνητα.

---

## Βήμα 3 – Συλλογή των Εικόνων που Θέλετε να Επεξεργαστείτε

Η σκληρή κωδικοποίηση ενός μικρού πίνακα λειτουργεί για μια επίδειξη, αλλά σε μια πραγματική εργασία batch πιθανότατα θα σαρώσετε έναν κατάλογο. Παρακάτω δείχνουμε και τις δύο προσεγγίσεις.

```java
        // Step 3a: Define a static list (quick demo)
        String[] imageFiles = {
            "YOUR_DIRECTORY/image1.png",
            "YOUR_DIRECTORY/image2.png",
            "YOUR_DIRECTORY/image3.png"
        };

        // Step 3b: Or, dynamically load every PNG in a folder
        // File folder = new File("YOUR_DIRECTORY");
        // String[] imageFiles = folder.list((dir, name) -> name.toLowerCase().endsWith(".png"));
```

> **Γιατί μπορεί να το χρειαστείτε:** Αν χρειάζεται να **εξάγετε κείμενο από PNG** αρχεία που φθάνουν μέσω ενός pipeline ανεβάσματος, η δυναμική έκδοση εντοπίζει αυτόματα νέα αρχεία χωρίς αλλαγές κώδικα.

---

## Βήμα 4 – Εκτέλεση OCR σε Κάθε Εικόνα Χρησιμοποιώντας το Ίδιο Engine

Ο βρόχος παρακάτω ορίζει την τρέχουσα εικόνα, εκτελεί `recognize()` και εκτυπώνει το αποτέλεσμα. Επειδή ενεργοποιήσαμε το multi‑threading νωρίτερα, κάθε κλήση μπορεί να τρέξει σε ξεχωριστό worker thread στο παρασκήνιο.

```java
        // Step 4: Recognize text from each image (reusing the same engine instance)
        for (String imagePath : imageFiles) {
            ocrEngine.setImage(imagePath);
            String recognizedText = ocrEngine.recognize().getText();
            System.out.println("Result for " + imagePath + ":\n" + recognizedText);
        }
    }
}
```

### Αναμενόμενη Έξοδος Κονσόλας

```
Result for YOUR_DIRECTORY/image1.png:
Welcome to the OCR demo.
Result for YOUR_DIRECTORY/image2.png:
Invoice #12345
Total: $567.89
Result for YOUR_DIRECTORY/image3.png:
© 2026 MyCompany. All rights reserved.
```

Αν οι εικόνες περιέχουν μη‑λατινικά σενάρια ή στιγμιότυπα χαμηλής ανάλυσης, μπορεί να δείτε ακατάληπτους χαρακτήρες — προσαρμόστε τις ρυθμίσεις DPI ή μείωσης θορύβου του engine ανάλογα (δείτε την ενότητα «Advanced Tweaks» παρακάτω).

---

## Προχωρημένες Ρυθμίσεις – Λεπτομερής Βελτιστοποίηση για Πραγματικά Batches

| Κατάσταση | Προτεινόμενη Ρύθμιση | Απόσπασμα Κώδικα |
|-----------|-------------------|--------------|
| PNG χαμηλής ανάλυσης | Αύξηση `setResolution` | `ocrEngine.getRecognitionSettings().setResolution(300);` |
| Έγγραφα με μικτές γλώσσες | Προσθήκη πακέτων γλώσσας | `ocrEngine.getRecognitionSettings().addLanguage(OcrLanguage.Spanish);` |
| Πολύ μεγάλα batches (10k+ αρχεία) | Ροή αρχείων αντί φόρτωσης όλων των ονομάτων ταυτόχρονα | Use `Files.walk(Paths.get("YOUR_DIRECTORY"))` with a filter. |
| Περιορισμοί μνήμης | Καταστροφή engine μετά από κάθε N αρχεία | `if (counter % 500 == 0) ocrEngine.dispose();` |

> **Θυμηθείτε:** Παρόλο που **χρησιμοποιούμε όλους τους πυρήνες της CPU**, το OS εξακολουθεί να διαχειρίζεται τον προγραμματισμό των threads. Αν παρατηρήσετε ότι το μηχάνημά σας γίνεται αργό, σκεφτείτε να περιορίσετε τα threads σε `availableProcessors() - 1`.

---

## Συνηθισμένα Παράπλοκα & Πώς να τα Αποφύγετε

1. **Τερματισμός λόγω έλλειψης file handles** – Η Java περιορίζει τα ανοιχτά αρχεία ανά διεργασία. Κλείστε κάθε εικόνα ρητά αν αντιμετωπίσετε σφάλματα `Too many open files`:

   ```java
   ocrEngine.setImage(imagePath);
   String text = ocrEngine.recognize().getText();
   ocrEngine.getImage().close(); // releases the handle
   ```

2. **Λανθασμένοι διαχωριστές διαδρομών στα Windows** – Χρησιμοποιήστε `File.separator` ή `Paths.get()` για να παραμείνετε ανεξάρτητοι από την πλατφόρμα.

3. **Μη‑ασφαλή thread προσαρμοσμένα callbacks** – Αν προσθέσετε έναν progress listener, βεβαιωθείτε ότι είναι thread‑safe (π.χ., `AtomicInteger`).

---

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

```java
import com.aspose.ocr.*;
import java.io.File;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable parallelism – use every logical CPU core
        ocrEngine.getRecognitionSettings()
                 .setNumberOfThreads(Runtime.getRuntime().availableProcessors());

        // 3️⃣ Locate PNG files (adjust the folder path)
        File folder = new File("YOUR_DIRECTORY");
        String[] imageFiles = folder.list((dir, name) ->
                name.toLowerCase().endsWith(".png"));

        if (imageFiles == null || imageFiles.length == 0) {
            System.out.println("No PNG files found in the directory.");
            return;
        }

        // 4️⃣ Process each image – same engine, multi‑threaded under the hood
        for (String imageName : imageFiles) {
            String imagePath = folder.getAbsolutePath() + File.separator + imageName;
            ocrEngine.setImage(imagePath);
            String recognizedText = ocrEngine.recognize().getText();

            System.out.println("Result for " + imagePath + ":\n" + recognizedText);
            // Optional: free the image handle (good for huge batches)
            ocrEngine.getImage().close();
        }

        // Clean up
        ocrEngine.dispose();
    }
}
```

> **Τι κάνει αυτό:** Σαρώνει το `YOUR_DIRECTORY` για κάθε `.png`, εκτελεί OCR παράλληλα, εκτυπώνει κάθε αποτέλεσμα και τελικά απελευθερώνει πόρους. Μπορείτε να ενσωματώσετε αυτήν την κλάση σε οποιοδήποτε Maven project, να τρέξετε `mvn exec:java` και να δείτε την αύξηση ταχύτητας σε σύγκριση με έναν μονονηματικό βρόχο.

---

## Συμπέρασμα

Τώρα έχετε ένα στιβαρό, έτοιμο για παραγωγή μοτίβο για **πώς να κάνετε batch OCR** σε Java. Επαναχρησιμοποιώντας ένα μόνο `OcrEngine`, ενεργοποιώντας **παράλληλη επεξεργασία OCR** και αξιοποιώντας **όλους τους πυρήνες της CPU**, μπορείτε να **αναγνωρίζετε κείμενο από εικόνες** σε ένα κλάσμα του χρόνου που θα απαιτούσε ένας απλός βρόχος.

Από εδώ μπορείτε:

- Συνδέστε το αποτέλεσμα με έναν δείκτη αναζήτησης (Elasticsearch) για γρήγορη ανάκτηση.  
- Συνδυάστε το με έναν μετατροπέα PDF‑σε‑PNG για **εξαγωγή κειμένου από PNG** ενσωματωμένο σε σαρωμένα έγγραφα.  
- Προσθέστε διαχείριση σφαλμάτων και λογική επανάληψης για ασταθείς δίσκους δικτύου.

Συνεχίστε να πειραματίζεστε — αντικαταστήστε με JPEG, ρυθμίστε το DPI, ή ακόμη και τροφοδοτήστε καρέ βίντεο για μεταγραφή σε πραγματικό χρόνο. Οι βασικές ιδέες παραμένουν ίδιες, και τα κέρδη απόδοσης είναι συνήθως εντυπωσιακά.

Καλή προγραμματιστική, και εύχομαι οι OCR pipelines σας να τρέχουν τόσο γρήγορα όσο η μηχανή του καφέ σας! 🚀

---

![Διάγραμμα που δείχνει τη ροή παράλληλου OCR – πώς να κάνετε batch OCR σε πολλαπλούς πυρήνες CPU]

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}