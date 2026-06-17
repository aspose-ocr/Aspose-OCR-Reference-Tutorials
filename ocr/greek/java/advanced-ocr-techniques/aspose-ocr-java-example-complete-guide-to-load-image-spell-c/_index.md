---
category: general
date: 2026-06-06
description: Παράδειγμα Aspose OCR Java που δείχνει πώς να φορτώσετε OCR εικόνας,
  να διορθώσετε σφάλματα OCR, να ορίσετε προσαρμοσμένο λεξικό και να επεξεργαστείτε
  OCR εικόνας σε λίγα μόνο βήματα.
draft: false
keywords:
- aspose ocr java example
- correct ocr errors
- load image ocr
- set custom dictionary
- process image ocr
language: el
og_description: Παράδειγμα Aspose OCR Java που φορτώνει μια εικόνα, διορθώνει σφάλματα
  OCR, ορίζει προσαρμοσμένο λεξικό και επεξεργάζεται το OCR της εικόνας αποδοτικά.
og_title: Παράδειγμα Aspose OCR Java – Φόρτωση εικόνας, ορθογραφική διόρθωση & επεξεργασία
  OCR
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Aspose OCR Java example showing how to load image OCR, correct OCR
    errors, set custom dictionary, and process image OCR in just a few steps.
  headline: Aspose OCR Java Example – Complete Guide to Load Image, Spell‑Correct,
    and Process OCR
  type: TechArticle
tags:
- Aspose
- OCR
- Java
- Text Recognition
title: Παράδειγμα Aspose OCR Java – Πλήρης Οδηγός για Φόρτωση Εικόνας, Διόρθωση Ορθογραφίας
  και Επεξεργασία OCR
url: /el/java/advanced-ocr-techniques/aspose-ocr-java-example-complete-guide-to-load-image-spell-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Παράδειγμα Aspose OCR Java – Πλήρης Οδηγός για Φόρτωση Εικόνας, Διόρθωση Ορθογραφίας και Επεξεργασία OCR

Κάποτε χρειάστηκε ένα **Aspose OCR Java example** που να λειτουργεί αμέσως; Δεν είστε μόνοι—οι προγραμματιστές συχνά κοιτάζουν μια θολή λήψη οθόνης και αναρωτιούνται γιατί το εξαγόμενο κείμενο είναι ακατάστατο. Τα καλά νέα είναι ότι η μηχανή OCR της Aspose έρχεται ήδη με ενσωματωμένη διόρθωση ορθογραφίας, και μπορείτε ακόμη να προσθέσετε τη δική σας λίστα λέξεων. Σε αυτό το tutorial θα περάσουμε από τη φόρτωση εικόνας OCR, την ενεργοποίηση της λειτουργίας διόρθωσης, την προαιρετική ρύθμιση προσαρμοσμένου λεξικού, και τέλος την επεξεργασία εικόνας OCR για να πάρουμε καθαρό, αναγνώσιμο κείμενο.  

Θα καλύψουμε επίσης γιατί μπορεί να θέλετε να **correct OCR errors**, πώς να **load image OCR** αποδοτικά, τα οφέλη μιας κλήσης **set custom dictionary**, και πώς φαίνεται η πλήρης ροή **process image OCR**. Στο τέλος θα έχετε ένα πλήρως εκτελέσιμο πρόγραμμα Java που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Maven ή Gradle.

---

## What You’ll Need

- Java 8 ή νεότερη (το API λειτουργεί επίσης με Java 11+)  
- Βιβλιοθήκη Aspose.OCR for Java (κατεβάστε το πιο πρόσφατο JAR από την ιστοσελίδα της Aspose ή προσθέστε την εξάρτηση Maven)  
- Ένα αρχείο εικόνας που περιέχει κείμενο (κατά προτίμηση ένα σαρωμένο έγγραφο ή ένα στιγμιότυπο οθόνης με κάποιο θόρυβο)  
- Προαιρετικά: ένα αρχείο λεξικού απλού κειμένου αν θέλετε να **set custom dictionary** για όρους ειδικού τομέα  

Αυτό είναι όλο—χωρίς βαριές μηχανές OCR, χωρίς εγγενείς εξαρτήσεις, μόνο ένα JAR και μερικές γραμμές κώδικα.

---

## Step 1: Aspose OCR Java Example – Load Image OCR

Το πρώτο που πρέπει να κάνετε είναι να δημιουργήσετε ένα αντικείμενο `OcrEngine` και να το κατευθύνετε στο αρχείο που θέλετε να αναλύσετε. Σκεφτείτε το σαν το άνοιγμα ενός βιβλίου πριν αρχίσετε να διαβάζετε.

```java
import com.aspose.ocr.*;

public class AsposeOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image you want to process
        // Replace YOUR_DIRECTORY/noisy_doc.png with your actual file path
        ocrEngine.setImage(new OcrInputImage("YOUR_DIRECTORY/noisy_doc.png"));
```

> **Why this matters:** Η κλήση `setImage` είναι η καρδιά του **load image OCR**. Χωρίς έγκυρη εικόνα, η μηχανή δεν έχει τίποτα να αναγνωρίσει, και θα καταλήξετε με κενή συμβολοσειρά ή εξαίρεση.  

![aspose ocr java example loading image](image.png){alt="aspose ocr java example loading image"}

---

## Step 2: Enable Spell‑Correction to Correct OCR Errors

Η Aspose OCR έρχεται με τη διόρθωση ορθογραφίας ενεργοποιημένη από προεπιλογή, αλλά ποτέ δεν βλάπτει να το δηλώσετε ρητά—ειδικά όταν παρουσιάζετε ένα **aspose ocr java example**. Η ενεργοποίηση αυτής της λειτουργίας μειώνει δραματικά το «ακαταλαβίστικο» κείμενο όπως “t1e” ή “rec0gn1tion”.

```java
        // Explicitly enable spell‑correction (enabled by default)
        ocrEngine.getSettings().setEnableSpellCorrection(true);
```

> **Pro tip:** Αν παρατηρήσετε ότι η μηχανή εξακολουθεί να αναγνωρίζει λανθασμένα ορισμένες λέξεις, ελέγξτε τις ρυθμίσεις γλώσσας ή προσθέστε ένα προσαρμοσμένο λεξικό (επόμενο βήμα).  

Η ενεργοποίηση της διόρθωσης ορθογραφίας είναι ο πιο γρήγορος τρόπος να **correct OCR errors** χωρίς να γράψετε επιπλέον κώδικα.

---

## Step 3: Set Custom Dictionary for Better Accuracy

Μερικές φορές το προεπιλεγμένο λεξικό δεν γνωρίζει την ορολογία του κλάδου σας—σκεφτείτε ιατρικούς όρους, κωδικούς προϊόντων ή ονόματα εμπορικών σημάτων. Εδώ έρχεται η **set custom dictionary**. Παρέχετε ένα αρχείο απλού κειμένου, μία λέξη ανά γραμμή, και η μηχανή OCR θα θεωρεί αυτές τις καταχωρήσεις έγκυρες κατά τη διόρθωση.

```java
        // OPTIONAL: Provide a custom dictionary to improve correction
        // Uncomment and adjust the path to your dictionary file
        // ocrEngine.getSettings().setCustomDictionary("YOUR_DIRECTORY/my_dict.txt");
```

> **When to use it:** Αν επεξεργάζεστε τιμολόγια και τα ονόματα εταιρειών παραμορφώνονται, ένα προσαρμοσμένο λεξικό που περιέχει αυτά τα ονόματα θα κάνει το στάδιο **process image OCR** πολύ πιο αξιόπιστο.

---

## Step 4: Process Image OCR and Retrieve the Text

Τώρα που η μηχανή είναι ρυθμισμένη, ήρθε η ώρα να τρέξετε την αναγνώριση. Η μέθοδος `process` κάνει όλη τη βαριά δουλειά—εντοπίζει μπλοκ κειμένου, εφαρμόζει τη διόρθωση ορθογραφίας και επιστρέφει ένα αντικείμενο `OcrResult`.

```java
        // Run the OCR process
        OcrResult ocrResult = ocrEngine.process();

        // Output the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

> **What you’ll see:** Η κονσόλα εκτυπώνει μια καθαρή, ανθρώπινα αναγνώσιμη συμβολοσειρά. Αν είχατε απενεργοποιήσει τη διόρθωση ορθογραφίας, πιθανότατα θα δείτε παράξενους χαρακτήρες, γι' αυτό η ενεργοποίηση νωρίτερα είναι κρίσιμη για **correct OCR errors**.

---

## Step 5: Run the Example and Verify the Output

Συμπιέστε και εκτελέστε την κλάση με το αγαπημένο σας IDE ή από τη γραμμή εντολών:

```bash
javac -cp "path/to/aspose-ocr.jar" AsposeOcrDemo.java
java -cp ".:path/to/aspose-ocr.jar" AsposeOcrDemo
```

Θα πρέπει να δείτε κάτι σαν:

```
Corrected text:
This is a sample document containing several lines of text.
The OCR engine has successfully recognized and corrected the content.
```

Αν η έξοδος εξακολουθεί να περιέχει ορθογραφικά λάθη, προσθέστε αυτές τις λέξεις στο προσαρμοσμένο λεξικό σας και ξανατρέξτε το βήμα **process image OCR**.  

---

## Common Pitfalls and How to Avoid Them

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Blank output** | Λάθος διαδρομή εικόνας ή μη υποστηριζόμενη μορφή | Επαληθεύστε τη διαδρομή, χρησιμοποιήστε PNG/JPEG, και βεβαιωθείτε ότι το αρχείο είναι αναγνώσιμο |
| **Garbage characters** | Η διόρθωση ορθογραφίας είναι απενεργοποιημένη ή η εικόνα είναι χαμηλής ποιότητας | Ενεργοποιήστε `setEnableSpellCorrection(true)` και σκεφτείτε προεπεξεργασία της εικόνας (αύξηση αντίθεσης) |
| **Domain‑specific words still wrong** | Δεν υπάρχει προσαρμοσμένο λεξικό | Χρησιμοποιήστε `setCustomDictionary` με αρχείο που περιέχει τους όρους σας |
| **Out‑of‑memory errors** | Πολύ μεγάλες εικόνες φορτώνονται χωρίς κλιμάκωση | Αλλάξτε το μέγεθος της εικόνας πριν τη δώσετε στο `OcrEngine` |

---

## Extending the Example

Τώρα που έχετε ένα σταθερό **aspose ocr java example**, ίσως θελήσετε να:

- **Batch process** έναν φάκελο εικόνων, επαναλαμβάνοντας τα ονόματα αρχείων και ξαναχρησιμοποιώντας το ίδιο αντικείμενο `OcrEngine`.  
- **Extract layout information** (πίνακες, στήλες) χρησιμοποιώντας `ocrResult.getPages()` για πιο προχωρημένη ανάλυση εγγράφων.  
- **Integrate with Apache PDFBox** για να ενσωματώσετε το αναγνωρισμένο κείμενο πίσω σε PDF.  

Όλες αυτές οι επεκτάσεις βασίζονται στα ίδια βασικά βήματα που καλύψαμε: load image OCR, enable correction, optionally set a custom dictionary, and process image OCR.

---

## Conclusion

Μόλις δημιουργήσατε ένα πλήρες **aspose ocr java example** που φορτώνει μια εικόνα, ενεργοποιεί τη διόρθωση ορθογραφίας για **correct OCR errors**, προαιρετικά **set custom dictionary**, και τέλος **process image OCR** για να ανακτήσει καθαρό κείμενο. Ο κώδικας είναι σύντομος, οι έννοιες σαφείς, και έχετε τώρα μια βάση που μπορείτε να επεκτείνετε για μαζικές εργασίες, ενσωματώσεις UI ή ακόμη και μικρο‑υπηρεσίες στο cloud.

Τι θα κάνετε μετά; Δοκιμάστε να τροφοδοτήσετε τη μηχανή με μια φωτογραφία χαμηλής ανάλυσης, προσθέστε μια λίστα SKU προϊόντων στο προσαρμοσμένο λεξικό, και δείτε πώς βελτιώνεται η ακρίβεια. Όσο περισσότερο πειραματίζεστε, τόσο καλύτερη θα είναι η κατανόησή σας για τις ανταλλαγές μεταξύ ποιότητας εικόνας, μεγέθους λεξικού και ταχύτητας επεξεργασίας.

Αφήστε ένα σχόλιο αν αντιμετωπίσετε δυσκολίες ή έχετε ιδέες για περαιτέρω βελτιώσεις. Καλή προγραμματιστική!

## What Should You Learn Next?

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε πρόσθετα χαρακτηριστικά του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [How to Set License and Verify Aspose.OCR License in Java](/ocr/english/java/ocr-basics/set-license/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Aspose OCR Java Example – Recognizing Lines in Images](/ocr/english/java/advanced-ocr-techniques/recognize-lines/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}