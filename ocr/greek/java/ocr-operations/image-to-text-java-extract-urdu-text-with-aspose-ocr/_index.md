---
category: general
date: 2026-02-17
description: 'Εκπαίδευση Java για μετατροπή εικόνας σε κείμενο: μάθετε πώς να εξάγετε
  κείμενο Urdu από μια εικόνα χρησιμοποιώντας το Aspose OCR. Συμπεριλαμβάνεται πλήρες
  παράδειγμα Java OCR.'
draft: false
keywords:
- image to text java
- how to extract text
- extract urdu text
- java ocr example
- load image ocr
language: el
og_description: Το tutorial image to text java δείχνει πώς να εξάγετε κείμενο Urdu
  από μια εικόνα χρησιμοποιώντας το Aspose OCR. Ακολουθήστε το πλήρες παράδειγμα Java
  OCR βήμα‑βήμα.
og_title: 'εικόνα σε κείμενο java: Εξαγωγή κειμένου Urdu με Aspose OCR'
tags:
- OCR
- Java
- Aspose
title: 'Από εικόνα σε κείμενο Java: Εξαγωγή κειμένου Urdu με Aspose OCR'
url: /el/java/ocr-operations/image-to-text-java-extract-urdu-text-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# image to text java: Εξαγωγή κειμένου Urdu με Aspose OCR

Αν χρειάζεστε μετατροπή **image to text java** για έγγραφα Urdu, βρίσκεστε στο σωστό μέρος. Αναρωτηθήκατε ποτέ *πώς να εξάγετε κείμενο* από μια εικόνα χειρόγραφης σημείωσης ή από μια σαρωμένη σελίδα εφημερίδας; Αυτός ο οδηγός θα σας καθοδηγήσει μέσα από ένα **java ocr example** που εξάγει χαρακτήρες Urdu απευθείας από μια εικόνα χρησιμοποιώντας το Aspose OCR.

Θα καλύψουμε τα πάντα, από την αδειοδότηση της βιβλιοθήκης μέχρι την εκτύπωση του αποτελέσματος στην κονσόλα. Στο τέλος θα μπορείτε να **load image ocr** αρχεία, να ορίσετε τη γλώσσα σε Urdu και να λάβετε καθαρή έξοδο Unicode — χωρίς επιπλέον εργαλεία.

## What You’ll Need

- **Java Development Kit (JDK) 8+** – ο κώδικας λειτουργεί σε οποιοδήποτε πρόσφατο JDK.  
- **Aspose.OCR for Java** JAR (κατεβάστε από την ιστοσελίδα Aspose).  
- Ένα έγκυρο αρχείο **Aspose OCR license** (`Aspose.OCR.lic`).  
- Μια εικόνα που περιέχει κείμενο Urdu, π.χ. `urdu-sample.png`.  

Αν έχετε αυτά τα βασικά, μπορείτε να περάσετε κατευθείαν στον κώδικα χωρίς να ψάχνετε για ελλιπείς εξαρτήσεις.

## image to text java – Setting Up Aspose OCR

Πρώτα, πρέπει να ενημερώσουμε το Aspose ότι διαθέτουμε άδεια. Χωρίς αυτήν η βιβλιοθήκη λειτουργεί σε λειτουργία αξιολόγησης και προσθέτει υδατογράμματα στο αποτέλεσμα.

```java
import com.aspose.ocr.*;

public class UrduDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply the Aspose OCR license
        License license = new License();
        license.setLicense("Aspose.OCR.lic");
```

**Γιατί είναι σημαντικό:** Η αδειοδότηση αφαιρεί το όριο επεξεργασίας των 5 δευτερολέπτων και ξεκλειδώνει το πλήρες πακέτο γλώσσας Urdu που προστέθηκε το 2025‑Q3. Αν παραλείψετε αυτό το βήμα, η μηχανή OCR θα λειτουργήσει, αλλά θα δείτε μια μικρή ετικέτα “Evaluation” στα αποτελέσματα.

## How to Extract Text – Initialize the OCR Engine

Τώρα δημιουργούμε τη μηχανή και δηλώνουμε ρητά ότι μας ενδιαφέρει η Urdu. Η σταθερά `OcrLanguage.URDU` ενεργοποιεί το σωστό σύνολο χαρακτήρων και τους κανόνες τμηματοποίησης.

```java
        // Step 2: Create the OCR engine and set the language to Urdu
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getLanguage().setLanguage(OcrLanguage.URDU); // added in 2025‑Q3
```

**Pro tip:** Αν χρειαστεί ποτέ να επεξεργαστείτε πολλές γλώσσες σε μία εκτέλεση, μπορείτε να περάσετε μια λίστα χωρισμένη με κόμμα, π.χ. `OcrLanguage.ENGLISH, OcrLanguage.URDU`. Η μηχανή θα εντοπίσει αυτόματα κάθε περιοχή.

## Load Image OCR – Preparing the Input

Το Aspose δουλεύει με ένα αντικείμενο `OcrInput` που μπορεί να κρατήσει μία ή πολλές εικόνες. Εδώ **load image ocr** δεδομένα από τοπικό αρχείο.

```java
        // Step 3: Load the image that contains Urdu text
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/urdu-sample.png");
```

> **Note:** Αντικαταστήστε το `YOUR_DIRECTORY` με την απόλυτη διαδρομή ή μια σχετική διαδρομή από τη ρίζα του έργου σας. Αν το αρχείο δεν βρεθεί, το Aspose ρίχνει `FileNotFoundException`. Μια γρήγορη έλεγχος με `new File(path).exists()` μπορεί να σας εξοικονομήσει πολύ χρόνο εντοπισμού σφαλμάτων.

## Recognize the Text – Running the OCR Process

Με τη μηχανή ρυθμισμένη και την εικόνα φορτωμένη, καλούμε τελικά τη μέθοδο `recognize`. Η μέθοδος επιστρέφει ένα `OcrResult` που περιέχει το εξαγόμενο κείμενο.

```java
        // Step 4: Recognize the text from the image
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Τι συμβαίνει στο παρασκήνιο;** Η μηχανή OCR χωρίζει την εικόνα σε γραμμές, έπειτα σε χαρακτήρες, εφαρμόζοντας κανόνες σχηματισμού ειδικούς για Urdu (όπως η σύνδεση μορφών). Γι’ αυτό η προηγόρική ρύθμιση της γλώσσας είναι κρίσιμη· διαφορετικά θα λάβετε ακατάστατα λατινικά σύμβολα.

## Print the Recognized Urdu Text

Το τελευταίο βήμα είναι απλώς η εκτύπωση του αποτελέσματος. Επειδή η Urdu χρησιμοποιεί δεξιά‑προς‑αριστερό σενάριο, βεβαιωθείτε ότι η κονσόλα σας υποστηρίζει Unicode (τα περισσότερα σύγχρονα τερματικά το κάνουν).

```java
        // Step 5: Print the recognized Urdu text
        System.out.println("Urdu text:\n" + ocrResult.getText());
    }
}
```

**Αναμενόμενη έξοδος (παράδειγμα):**

```
Urdu text:
یہ ایک مثال کا متن ہے جو تصویر سے نکالا گیا ہے۔
```

Αν δείτε ερωτηματικά ή κενές συμβολοσειρές, ελέγξτε ξανά ότι η κωδικοποίηση της κονσόλας είναι UTF‑8 (`chcp 65001` στα Windows, ή εκτελέστε τη Java με `-Dfile.encoding=UTF-8`).

## Full Working Example – All Steps in One Place

Παρακάτω βρίσκεται το πλήρες, έτοιμο για αντιγραφή‑και‑επικόλληση πρόγραμμα. Δεν απαιτούνται εξωτερικές αναφορές, μόνο ένα αρχείο Java.

```java
import com.aspose.ocr.*;

public class UrduDemo {
    public static void main(String[] args) throws Exception {
        // Apply the Aspose OCR license
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // Create the OCR engine and set the language to Urdu
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getLanguage().setLanguage(OcrLanguage.URDU); // added in 2025‑Q3

        // Load the image that contains Urdu text
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/urdu-sample.png");

        // Recognize the text from the image
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Print the recognized Urdu text
        System.out.println("Urdu text:\n" + ocrResult.getText());
    }
}
```

Τρέξτε το με:

```bash
javac -cp "aspose-ocr-23.10.jar" UrduDemo.java
java -cp ".:aspose-ocr-23.10.jar" UrduDemo
```

Αντικαταστήστε την έκδοση του JAR (`23.10`) με αυτήν που κατεβάσατε. Η κονσόλα θα πρέπει να εμφανίσει την πρόταση Urdu που εξήχθη από το PNG σας.

## Common Pitfalls & Edge Cases

| Issue | Why it Happens | How to Fix |
|-------|----------------|------------|
| **Empty output** | Η εικόνα είναι πολύ σκοτεινή ή χαμηλής ανάλυσης. | Προεπεξεργαστείτε την εικόνα (αυξήστε την αντίθεση, δυαδικοποιήστε) χρησιμοποιώντας `BufferedImage` πριν τη δώσετε στο Aspose. |
| **Garbage characters** | Λάθος γλώσσα ορισμένη (η προεπιλογή είναι Αγγλικά). | Βεβαιωθείτε ότι καλείται `ocrEngine.getLanguage().setLanguage(OcrLanguage.URDU);` πριν το `recognize`. |
| **License not found** | Λάθος διαδρομή ή λείπει το αρχείο. | Χρησιμοποιήστε απόλυτη διαδρομή ή τοποθετήστε το αρχείο `.lic` στο classpath και καλέστε `license.setLicense("Aspose.OCR.lic");`. |
| **Out‑of‑memory on large images** | Μεγάλες PNG καταναλώνουν heap. | Καλέστε `ocrEngine.setMaxImageSize(2000);` για εσωτερική σμίκρυνση, ή αλλάξτε το μέγεθος της εικόνας εσείς. |

## Extending the Demo

- **Batch processing:** Επανάληψη σε φάκελο, προσθήκη κάθε αρχείου στο ίδιο `OcrInput` και συλλογή αποτελεσμάτων σε CSV.  
- **Different languages:** Αντικαταστήστε το `OcrLanguage.URDU` με `OcrLanguage.ARABIC` ή συνδυάστε πολλαπλές γλώσσες.  
- **Saving to file:** Χρησιμοποιήστε `Files.write(Paths.get("output.txt"), ocrResult.getText().getBytes(StandardCharsets.UTF_8));`.  

Όλες αυτές οι ιδέες βασίζονται στο **java ocr example** που μόλις δημιουργήσαμε, επιτρέποντάς σας να προσαρμόσετε τη λύση σε πραγματικά έργα.

## Conclusion

Τώρα έχετε μια σταθερή ροή εργασίας **image to text java** που εξάγει χαρακτήρες Urdu από μια εικόνα χρησιμοποιώντας το Aspose OCR. Το tutorial κάλυψε κάθε βήμα — από την αδειοδότηση και την επιλογή γλώσσας μέχρι τη φόρτωση της εικόνας και την εκτύπωση του αποτελέσματος — ώστε να μπορείτε να επικολλήσετε τον κώδικα σε οποιοδήποτε έργο Java και να δείτε τη λειτουργία του.

Στη συνέχεια, δοκιμάστε να πειραματιστείτε με μεγαλύτερα PDF, διαφορετικά σενάρια ή ακόμη και να ενσωματώσετε το βήμα OCR σε ένα Spring Boot REST endpoint. Οι ίδιες αρχές—**how to extract text**, **load image o

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}