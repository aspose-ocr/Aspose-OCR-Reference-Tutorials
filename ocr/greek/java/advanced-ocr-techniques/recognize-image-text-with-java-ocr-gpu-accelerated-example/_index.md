---
category: general
date: 2026-03-28
description: Μάθετε πώς να αναγνωρίζετε κείμενο σε εικόνες στη Java χρησιμοποιώντας
  το Aspose OCR, να εξάγετε αρχεία PNG κειμένου και να χρησιμοποιείτε επιτάχυνση GPU
  για γρήγορο OCR μεγάλων εικόνων.
draft: false
keywords:
- recognize image text
- extract text png
- use gpu acceleration
- ocr large image
- java ocr example
language: el
og_description: Ανακαλύψτε πώς να αναγνωρίζετε κείμενο σε εικόνες στη Java, να εξάγετε
  κείμενο από αρχεία PNG και να χρησιμοποιείτε επιτάχυνση GPU για OCR μεγάλων εικόνων.
og_title: Αναγνώριση κειμένου σε εικόνα με Java OCR – Παράδειγμα με επιτάχυνση GPU
tags:
- OCR
- Java
- GPU
title: Αναγνώριση κειμένου εικόνας με Java OCR – Παράδειγμα με επιτάχυνση GPU
url: /el/java/advanced-ocr-techniques/recognize-image-text-with-java-ocr-gpu-accelerated-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση κειμένου εικόνας με Java OCR – Παράδειγμα με επιτάχυνση GPU

Έχετε ποτέ χρειαστεί να **αναγνωρίσετε κείμενο εικόνας** από ένα τεράστιο PNG αλλά βρήκατε ότι η έκδοση CPU είναι αργή; Δεν είστε οι μόνοι. Σε πολλές πραγματικές ροές εργασίας—π.χ. σάρωση τιμολογίων ή αρχειοθέτηση ιστορικών εγγράφων—το μέγεθος της εικόνας μπορεί να αυξηθεί πολύ, και η προεπιλεγμένη μηχανή OCR απλώς δεν μπορεί να τα καταφέρει.  

Καλά νέα: το Aspose OCR for Java σας επιτρέπει να **χρησιμοποιήσετε επιτάχυνση GPU** για να επιταχύνετε τη διαδικασία, και ο κώδικας είναι εκπληκτικά σύντομος. Σε αυτό το tutorial θα δείτε ένα πλήρες, εκτελέσιμο παράδειγμα Java OCR που **εξάγει κείμενο PNG** αρχεία, αξιοποιεί μια GPU με υποστήριξη CUDA, και διαχειρίζεται ένα **OCR large image** με λίγες μόνο γραμμές κώδικα. Στο τέλος θα ξέρετε ακριβώς πώς να το ενσωματώσετε στο δικό σας έργο Java και γιατί κάθε ρύθμιση είναι σημαντική.

## Τι θα μάθετε

- Πώς να ρυθμίσετε το Aspose OCR σε ένα έργο Maven ή Gradle.  
- Η διαδικασία βήμα‑βήμα για **αναγνωρίση κειμένου εικόνας** στην GPU.  
- Γιατί η ρύθμιση του αριθμού των ροών GPU μπορεί να βελτιώσει τη διαμεταγωγή.  
- Πώς να επαληθεύσετε το αποτέλεσμα και να αντιμετωπίσετε κοινά προβλήματα.  

> **Προαπαιτούμενα** – Java 17 (ή νεότερη), μια GPU συμβατή με CUDA με τον πιο πρόσφατο οδηγό, και μια έγκυρη άδεια Aspose OCR για Java (η δωρεάν δοκιμή λειτουργεί για αξιολόγηση). Δεν απαιτούνται άλλες εξωτερικές βιβλιοθήκες.

---

## Βήμα 1: Προσθήκη εξάρτησης Aspose OCR

Πρώτα, φέρετε τη βιβλιοθήκη Aspose OCR στο build σας. Αν χρησιμοποιείτε **Maven**, προσθέστε το παρακάτω απόσπασμα στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check Maven Central for the latest version -->
</dependency>
```

Για **Gradle**, τοποθετήστε αυτό στο `build.gradle`:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Pro tip:** Η τελευταία έκδοση (από Μάρτιο 2026) περιλαμβάνει βελτιώσεις απόδοσης για φορτία εργασίας GPU, οπότε πάντα τραβάτε την πιο πρόσφατη κυκλοφορία.

---

## Βήμα 2: Αρχικοποίηση της μηχανής OCR και ενεργοποίηση GPU

Η δημιουργία μιας μηχανής OCR είναι απλή. Το κρίσιμο μέρος είναι η ενεργοποίηση της σημαίας GPU—διαφορετικά η μηχανή επιστρέφει σε λειτουργία CPU.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // 3️⃣ (Optional) Set the number of GPU streams for parallel processing
        //    More streams can improve throughput on multi‑core GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);
```

### Γιατί να ενεργοποιήσετε την GPU;

Όταν ενεργοποιείτε το `setUseGpu(true)`, το Aspose μεταφέρει τους βαριούς υπολογισμούς του convolutional neural network στην κάρτα γραφικών. Αυτό μπορεί να εξοικονομήσει δευτερόλεπτα από το χρόνο επεξεργασίας ενός **ocr large image**, ειδικά όταν η εικόνα υπερβαίνει τα 4000 × 4000 px. Αν το περιβάλλον σας δεν διαθέτει συμβατή GPU, η κλήση γίνεται απλώς no‑op και η μηχανή συνεχίζει στην CPU—χωρίς κατάρρευση, απλώς πιο αργή απόδοση.

---

## Βήμα 3: Αναγνώριση εικόνας PNG και εξαγωγή του κειμένου της

Τώρα δείξτε τη μηχανή στο αρχείο που θέλετε να επεξεργαστείτε. Το παράδειγμα χρησιμοποιεί το `sample-large.png`, αλλά μπορείτε να το αντικαταστήσετε με οποιοδήποτε PNG ή JPEG.

```java
        // 4️⃣ Perform OCR on the input image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // 5️⃣ Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Όταν εκτελέσετε το πρόγραμμα, θα πρέπει να δείτε κάτι σαν:

```
=== Recognized Text ===
Invoice #12345
Date: 2026‑03‑27
Total: $1,234.56
...
```

Αυτή η έξοδος επιβεβαιώνει ότι η λειτουργία **αναγνωρίσματος κειμένου εικόνας** ολοκληρώθηκε με επιτυχία και ότι εξάγατε επιτυχώς το περιεχόμενο **extract text png**.

---

## Βήμα 4: Επαλήθευση χρήσης GPU (Προαιρετικό αλλά χρήσιμο)

Αν σας ενδιαφέρει αν η GPU χρησιμοποιείται πραγματικά, ανοίξτε το εργαλείο παρακολούθησης GPU του συστήματός σας (π.χ. `nvidia-smi` σε Linux). Ενώ η διαδικασία Java εκτελείται, θα πρέπει να δείτε μια ήπια αύξηση στη χρήση μνήμης και στην υπολογιστική χρησιμοποίηση.

```bash
$ nvidia-smi
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   PID   Type   Process name                  GPU Memory               |
|  0    12345 C++    java                           1024MiB                  |
+-----------------------------------------------------------------------------+
```

Αν δεν δείτε καμία δραστηριότητα, ελέγξτε ξανά ότι:

1. Ο οδηγός CUDA ταιριάζει με το μοντέλο GPU.  
2. Η κλήση `setUseGpu(true)` δεν παρακάμπτεται αργότερα στον κώδικα.  
3. Το αρχείο άδειας (αν έχετε) δεν περιορίζει τη χρήση GPU.

---

## Βήμα 5: Διαχείριση κοινών ακραίων περιπτώσεων

### Μεγάλες εικόνες που υπερβαίνουν τη μνήμη GPU

Όταν μια εικόνα είναι τεράστια (π.χ. 8000 × 8000 px), η GPU μπορεί να εξαντλήσει τη μνήμη. Μια γρήγορη λύση είναι να μειώσετε την ανάλυση της εικόνας πριν τη δώσετε στο Aspose:

```java
import java.awt.image.BufferedImage;
import javax.imageio.ImageIO;
import java.io.File;

BufferedImage original = ImageIO.read(new File("sample-large.png"));
int maxDim = 4000; // target max dimension
int width = original.getWidth();
int height = original.getHeight();

float scale = Math.min((float)maxDim / width, (float)maxDim / height);
int newWidth = Math.round(width * scale);
int newHeight = Math.round(height * scale);

BufferedImage resized = new BufferedImage(newWidth, newHeight, original.getType());
// Simple scaling (for demo purposes)
resized.getGraphics().drawImage(original, 0, 0, newWidth, newHeight, null);
ImageIO.write(resized, "png", new File("sample-resized.png"));
```

Στη συνέχεια περάστε το `"sample-resized.png"` στη `recognizeImage`. Αυτό διατηρεί την ακρίβεια του OCR ενώ παραμένει εντός των ορίων μνήμης GPU.

### Πολυ-σελίδες PDF

Το Aspose OCR μπορεί επίσης να χειριστεί PDF σελίδα‑με‑σελίδα. Επαναλάβετε για κάθε σελίδα, μετατρέψτε την σε εικόνα και δώστε τη στη μηχανή. Η ίδια σημαία **use gpu acceleration** ισχύει, προσφέροντας μια γρήγορη αλυσίδα PDF‑to‑text.

---

## Πλήρες λειτουργικό παράδειγμα (Έτοιμο για αντιγραφή‑επικόλληση)

Παρακάτω είναι η πλήρης κλάση Java, έτοιμη για μεταγλώττιση και εκτέλεση. Αντικαταστήστε το `YOUR_DIRECTORY` με τη διαδρομή του αρχείου PNG σας.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // Step 3: (Optional) Set the number of GPU streams for parallel processing
        // Using 2 streams works well on most modern GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);

        // Step 4: Perform OCR on the input image
        // This will **recognize image text** from a PNG file.
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // Step 5: Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**Αναμενόμενη έξοδος** – μια αναπαράσταση plain‑text όλων όσων η μηχανή μπόρεσε να διαβάσει από την εικόνα. Αν η εικόνα περιέχει πίνακα, θα λάβετε τα περιεχόμενα των κελιών ενωμένα με αλλαγές γραμμής· το Aspose δεν διατηρεί τη διάταξη, αλλά μπορείτε να επεξεργαστείτε το string αν χρειάζεται.

---

## Συχνές Ερωτήσεις

| Ερώτηση | Απάντηση |
|----------|--------|
| **Χρειάζομαι πληρωμένη άδεια;** | Η δοκιμή λειτουργεί για έως 200 σελίδες και απενεργοποιεί το υδατογράφημα για OCR. Για παραγωγή, μια άδεια αφαιρεί τους περιορισμούς και ξεκλειδώνει ολόκληρο το σύνολο GPU. |
| **Τι γίνεται αν η GPU μου είναι παλαιότερη (π.χ. GTX 750);** | Οι παλαιότερες GPU μπορεί να λειτουργούν, αλλά με μειωμένη ταχύτητα· βεβαιωθείτε ότι έχετε τουλάχιστον Compute Capability 3.0. |
| **Μπορώ να επεξεργαστώ αρχεία JPG ή BMP;** | Απόλυτα—`recognizeImage` δέχεται οποιαδήποτε μορφή υποστηρίζεται από το Java ImageIO. |
| **Υπάρχει τρόπος να επεξεργαστώ πολλαπλές εικόνες σε batch;** | Τυλίξτε την κλήση OCR σε βρόχο και εξετάστε το ενδεχόμενο αύξησης του `setGpuStreams` ώστε να ταιριάζει με τον αριθμό των ταυτόχρονων ροών που θέλετε. |
| **Τι κάνω αν χρειάζεται να διατηρήσω τη διάταξη;** | Χρησιμοποιήστε το `LayoutOptions` του Aspose OCR για να λάβετε τα πλαίσια περιορισμού· αυτό υπερβαίνει το πεδίο αυτού του γρήγορου οδηγού, αλλά τεκμηριώνεται στο API. |

---

## Συμπέρασμα

Τώρα έχετε ένα σύντομο, end‑to‑end **java ocr example** που **αναγνωρίζει κείμενο εικόνας**, **εξάγει κείμενο png**, και **χρησιμοποιεί επιτάχυνση GPU** για να επιταχύνει την επεξεργασία ενός **ocr large image**. Ρυθμίζοντας τον αριθμό ροών GPU και, αν χρειαστεί, μειώνοντας την ανάλυση υπερμεγέθων εικόνων, μπορείτε να προσαρμόσετε τη λύση σε σχεδόν οποιαδήποτε διαμόρφωση υλικού.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να τροφοδοτήσετε έναν φάκελο σαρωμένων αποδείξεων στην ίδια αλυσίδα, ή πειραματιστείτε με το `TextRegion` API του Aspose για να διατηρήσετε τη αρχική διάταξη. Και αν αντιμετωπίσετε δυσκολίες, τα φόρουμ του Aspose και το Javadoc είναι εξαιρετικούς πόροι—απλώς θυμηθείτε τα βασικά που καλύψαμε εδώ.

Καλό κώδικα, και εύχομαι το OCR σας να είναι αστραπιαία γρήγορο!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}