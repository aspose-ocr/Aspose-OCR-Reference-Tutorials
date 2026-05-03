---
category: general
date: 2026-05-03
description: Μάθετε πώς να αναγνωρίζετε κείμενο από εικόνα και να μετατρέπετε την
  εικόνα σε κείμενο χρησιμοποιώντας το Aspose OCR για Java. Περιλαμβάνει συμβουλές
  για τη βελτίωση της ακρίβειας του OCR και την εκτέλεση OCR σε αρχεία PNG.
draft: false
keywords:
- recognize text from image
- convert image to text
- improve ocr accuracy
- load image for ocr
- run ocr on png
language: el
og_description: Οδηγός βήμα‑προς‑βήμα για την αναγνώριση κειμένου από εικόνα χρησιμοποιώντας
  το Aspose OCR για Java. Μάθετε πώς να μετατρέπετε εικόνα σε κείμενο, να βελτιώνετε
  την ακρίβεια του OCR και να εκτελείτε OCR σε PNG.
og_title: Αναγνώριση κειμένου από εικόνα με Aspose OCR – Java Tutorial
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Αναγνώριση κειμένου από εικόνα με το Aspose OCR – Πλήρης Οδηγός Java
url: /el/python-java/general/recognize-text-from-image-with-aspose-ocr-complete-java-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# αναγνώριση κειμένου από εικόνα με Aspose OCR – Πλήρης Οδηγός Java

Έχετε ποτέ χρειαστεί να **αναγνωρίσετε κείμενο από εικόνα** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη θα σας δώσει αξιόπιστα αποτελέσματα; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν προσπαθούν για πρώτη φορά να εξάγουν δεδομένα από σαρωμένα PDF, αποδείξεις ή εργαστηριακές αναφορές. Τα καλά νέα είναι ότι το Aspose OCR for Java κάνει όλη τη διαδικασία παιχνιδάκι, και μπορείτε ακόμη και να **μετατρέψετε εικόνα σε κείμενο** με μερικές μόνο γραμμές.

Σε αυτό το tutorial θα περάσουμε από όλα όσα χρειάζεται να γνωρίζετε: από τη φόρτωση μιας εικόνας για OCR, τη ρύθμιση παραμέτρων για **βελτιώστε την ακρίβεια του OCR**, μέχρι τελικά **run OCR on PNG** αρχεία και την εκτύπωση του εξαγόμενου κειμένου. Χωρίς περιττές πληροφορίες, μόνο ένα πρακτικό, εκτελέσιμο παράδειγμα που μπορείτε να ενσωματώσετε στο πρότζεκτ σας σήμερα.

---

## Τι Θα Χρειαστείτε

| Απαίτηση | Αιτία |
|--------------|--------|
| Java 17 (ή νεότερη) | Το Aspose OCR στοχεύει σε Java 8+, αλλά η πιο πρόσφατη JDK προσφέρει καλύτερη απόδοση. |
| Aspose OCR for Java library (`aspose-ocr.jar`) | Ο βασικός μηχανισμός που κάνει τη βαριά δουλειά. |
| A valid Aspose OCR license file (`Aspose.OCR.Java.lic`) | Ενεργοποιεί το πλήρες σύνολο λειτουργιών· διαφορετικά θα δείτε υδατογράφημα δοκιμής. |
| An image file (PNG, JPEG, TIFF, κ.λπ.) containing clear text | Θα χρησιμοποιήσουμε το `lab_report.png` ως συγκεκριμένο παράδειγμα. |
| A custom dictionary (optional) | Βελτιώνει την αναγνώριση για όρους ειδικού τομέα όπως το “hemoglobin”. |

Αν κάποιο από αυτά σας φαίνεται άγνωστο, μην πανικοβληθείτε—η εγκατάσταση ενός JAR και η δημιουργία ενός απλού αρχείου κειμένου είναι τετριμμένες εργασίες που θα καλύψουμε σε λίγο.

## Βήμα 1 – Ρύθμιση του Έργου και Εισαγωγή Εξαρτήσεων

Πρώτα, δημιουργήστε ένα νέο Maven (ή Gradle) project και προσθέστε την εξάρτηση Aspose OCR. Οι χρήστες Maven μπορούν να επικολλήσουν αυτό το απόσπασμα στο `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check the latest version on Maven Central -->
</dependency>
```

Αν προτιμάτε Gradle, το ισοδύναμο είναι:

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

> **Συμβουλή:** Παρακολουθείτε τον αριθμό έκδοσης· οι πιο πρόσφατες εκδόσεις συχνά περιέχουν διορθώσεις σφαλμάτων που επηρεάζουν άμεσα **βελτιώστε την ακρίβεια του OCR**.

Τώρα, δημιουργήστε μια κλάση Java με όνομα `OcrDemo.java`. Στην κορυφή του αρχείου, εισάγετε τις απαιτούμενες κλάσεις:

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.License;
import com.aspose.ocr.Image;
import com.aspose.ocr.OcrResult;
```

## Βήμα 2 – Αρχικοποίηση της Μηχανής OCR και Εφαρμογή της Άδειας

Δεν μπορείτε να **run OCR on PNG** αρχεία χωρίς πρώτα να ενημερώσετε τη μηχανή ότι είναι αδειοδοτημένη. Να πώς γίνεται:

```java
public class OcrDemo {
    public static void main(String[] args) {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Apply your license – replace the path with your actual license location
        License lic = new License();
        lic.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");
        ocrEngine.setLicense(lic);
```

Γιατί το επιπλέον αντικείμενο `License`; Το Aspose διαχωρίζει τη διαχείριση της άδειας από τη μηχανή ώστε να μπορείτε να αλλάζετε άδειες εν κινήσει, κάτι που μπορεί να φανεί χρήσιμο σε σενάρια multi‑tenant SaaS.

## Βήμα 3 – Φόρτωση Προσαρμοσμένου Λεξικού (Προαιρετικό αλλά Ισχυρό)

Αν εργάζεστε με ιατρική ορολογία, χημικούς τύπους ή ονόματα εμπορικών σημάτων, ένα προσαρμοσμένο λεξικό μπορεί να **βελτιώστε την ακρίβεια του OCR** δραματικά. Το λεξικό είναι ένα απλό αρχείο κειμένου με μία λέξη ανά γραμμή:

```java
        // Optional: improve accuracy with a custom dictionary
        // Create a file named custom_dictionary.txt in YOUR_DIRECTORY
        ocrEngine.getConfig().setCustomDictionary("YOUR_DIRECTORY/custom_dictionary.txt");
```

> **Γιατί λειτουργεί:** Η μηχανή OCR χρησιμοποιεί το λεξικό για να κατευθύνει το γλωσσικό της μοντέλο προς τις λέξεις που σας ενδιαφέρουν, μειώνοντας λανθασμένες αναγνώσεις όπως “hemo­globin” → “hemoglobin”.

Αν δεν έχετε λεξικό, απλώς παραλείψτε αυτή τη γραμμή—το Aspose λειτουργεί καλά και με τα ενσωματωμένα πακέτα γλώσσας.

## Βήμα 4 – Φόρτωση της Εικόνας που Θέλετε να Επεξεργαστείτε

Τώρα πραγματικά **load image for OCR**. Το Aspose υποστηρίζει πολλές μορφές, αλλά το PNG είναι ιδιαίτερα lossless, καθιστώντας το ασφαλή επιλογή για σαρωμένα έγγραφα.

```java
        // Load the PNG image containing the text you want to extract
        Image inputImage = Image.fromFile("YOUR_DIRECTORY/lab_report.png");
```

> **Edge case:** Αν η εικόνα σας είναι τεράστια (πάνω από 5 MB), σκεφτείτε να τη μειώσετε πρώτα για να επιταχύνετε την επεξεργασία. Η κλάση `Image` παρέχει μέθοδο `resize` που μπορείτε να καλέσετε πριν από την αναγνώριση.

## Βήμα 5 – Εκτέλεση της Διαδικασίας OCR και Ανάκτηση του Κειμένου

Με όλα έτοιμα, ενεργοποιήστε τη μηχανή OCR. Η μέθοδος `recognize` επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει το εξαγόμενο κείμενο, βαθμούς εμπιστοσύνης και ακόμη και bounding boxes αν χρειάζεστε πληροφορίες διάταξης.

```java
        // Perform OCR on the loaded image
        OcrResult result = ocrEngine.recognize(inputImage);

        // Print the extracted text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

Όταν τρέξετε το πρόγραμμα, θα πρέπει να δείτε κάτι σαν:

```
=== Extracted Text ===
Patient Name: John Doe
Hemoglobin: 13.5 g/dL
...
```

Αυτό είναι—έχετε επιτυχώς **recognize text from image** και **convert image to text** χρησιμοποιώντας το Aspose OCR.

## Βήμα 6 – Συνηθισμένα Προβλήματα και Πώς να τα Διορθώσετε

| Σύμπτωμα | Πιθανή Αιτία | Διόρθωση |
|---------|--------------|-----|
| Κενό αποτέλεσμα | Η άδεια δεν έχει εφαρμοστεί ή έχει λήξει | Επαληθεύστε τη διαδρομή προς το `Aspose.OCR.Java.lic` και βεβαιωθείτε ότι ταιριάζει με την έκδοση. |
| Παραμορφωμένοι χαρακτήρες | Η εικόνα είναι χαμηλής ανάλυσης ή πολύ συμπιεσμένη | Χρησιμοποιήστε πηγή υψηλότερης ανάλυσης ή προεπεξεργαστείτε την εικόνα (δυαδικοποίηση, διόρθωση κλίσης). |
| Απουσία ειδικών όρων | Δεν υπάρχει προσαρμοσμένο λεξικό | Προσθέστε ένα αρχείο λεξικού με τους χαμένα όρους, έναν ανά γραμμή. |
| Αργή επεξεργασία σε μεγάλες παρτίδες | Δεν υπάρχει πολυνηματική επεξεργασία | Δημιουργήστε μια δεξαμενή από αντικείμενα `OcrEngine` (είναι ασφαλή για νήματα) και επεξεργαστείτε τις εικόνες παράλληλα. |

## Βήμα 7 – Επέκταση του Παραδείγματος: Αποθήκευση Αποτελεσμάτων σε Αρχείο

Αν χρειάζεται να διατηρήσετε το εξαγόμενο κείμενο για μετέπειτα ανάλυση, απλώς γράψτε το σε αρχείο:

```java
import java.nio.file.Files;
import java.nio.file.Paths;
import java.nio.charset.StandardCharsets;

// ...

        // Save the text to a .txt file
        Files.write(Paths.get("output.txt"),
                    result.getText().getBytes(StandardCharsets.UTF_8));
        System.out.println("Text saved to output.txt");
```

Τώρα έχετε μια επαναχρησιμοποιήσιμη pipeline που **load image for OCR**, εξάγει το περιεχόμενο και το αποθηκεύει όπου θέλετε.

## Bonus: Εκτέλεση OCR σε Πολλαπλά Αρχεία PNG σε Φάκελο

Τα πραγματικά έργα συχνά χρειάζονται επεξεργασία δεκάδων σαρώσεων. Εδώ είναι ένας γρήγορος βρόχος που διαβάζει κάθε `.png` σε έναν φάκελο:

```java
import java.io.File;

// ...

        File folder = new File("YOUR_DIRECTORY/scans");
        File[] pngFiles = folder.listFiles((dir, name) -> name.toLowerCase().endsWith(".png"));

        for (File png : pngFiles) {
            Image img = Image.fromFile(png.getAbsolutePath());
            OcrResult res = ocrEngine.recognize(img);
            System.out.println("---- " + png.getName() + " ----");
            System.out.println(res.getText());
        }
```

Θυμηθείτε να επαναχρησιμοποιείτε το ίδιο αντικείμενο `ocrEngine`—η δημιουργία νέου για κάθε αρχείο προσθέτει περιττό φόρτο.

## Συμπέρασμα

Τώρα έχετε μια πλήρη, end‑to‑end λύση που **recognize text from image** χρησιμοποιώντας το Aspose OCR for Java. Από τη φόρτωση της εικόνας, προαιρετικά τον εμπλουτισμό της μηχανής με προσαρμοσμένο λεξικό για **βελτιώστε την ακρίβεια του OCR**, μέχρι το **run OCR on PNG** αρχεία και την αποθήκευση του αποτελέσματος, ο κώδικας είναι έτοιμος να ενσωματωθεί σε οποιοδήποτε Java project.

Τι ακολουθεί; Δοκιμάστε να τροφοδοτήσετε το εξαγόμενο κείμενο σε μια pipeline επεξεργασίας φυσικής γλώσσας, ή πειραματιστείτε με OCR σε χειρόγραφες σημειώσεις (το Aspose προσφέρει επίσης λειτουργία χειρογράφου). Οι δυνατότητες είναι ατελείωτες, και μόλις ξεκλειδώσατε το πρώτο βήμα.

Καλό κώδικα! Αν αντιμετωπίσατε δυσκολίες, αφήστε ένα σχόλιο παρακάτω—ας τα λύσουμε μαζί.

![Στιγμιότυπο οθόνης του αποτελέσματος OCR στην κονσόλα – αναγνώριση κειμένου από εικόνα](/images/ocr_console_result.png "παράδειγμα αναγνώρισης κειμένου από εικόνα")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}