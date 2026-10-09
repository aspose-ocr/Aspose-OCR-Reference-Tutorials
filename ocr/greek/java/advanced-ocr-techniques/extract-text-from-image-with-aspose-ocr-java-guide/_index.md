---
category: general
date: 2026-09-28
description: Μάθετε πώς να εξάγετε κείμενο από εικόνα java με Aspose OCR, συμπεριλαμβανομένης
  της εξαγωγής form data java μέσω regions of interest για ακριβή αποτελέσματα.
draft: false
keywords:
- extract text from image java
- extract form data java
- aspose ocr tutorial java
lastmod: 2026-09-28
og_description: Μάθετε πώς να εξάγετε κείμενο από εικόνα java με Aspose OCR, συμπεριλαμβανομένης
  της εξαγωγής form data java μέσω regions of interest. Γρήγορος οδηγός για developers.
og_image_alt: Guide showing how to extract text from image java using Aspose OCR
og_title: Εξαγωγή κειμένου από εικόνα java χρησιμοποιώντας Aspose OCR – οδηγός
schemas:
- author: Aspose
  dateModified: '2026-09-28'
  description: Learn how to extract text from image java with Aspose OCR, including
    extracting form data java via regions of interest for precise results.
  headline: Extract text from image java using Aspose OCR – guide
  type: TechArticle
- questions:
  - answer: Not directly. Convert each PDF page to an image first (e.g., using Aspose
      PDF) and then feed the image to the OCR engine.
    question: Does this work with PDFs?
  - answer: OCR can’t read boolean states, but you can treat the checkbox area as
      an ROI and inspect the pixel density to infer a tick.
    question: What if my form has checkboxes?
  - answer: Loop over each page image, reuse the same ROI list, and concatenate the
      results.
    question: Can I extract text from a multi‑page form in one go?
  - answer: Increase the contrast, enable binarization via `ocrEngine.getEngineOptions().setBinarization(true)`,
      and consider pre‑processing the image to remove noise.
    question: How do I improve accuracy on low‑quality scans?
  - answer: Yes. Aspose OCR offers a free trial, but a commercial license is needed
      for deployment.
    question: Is a license required for production use?
  type: FAQPage
tags:
- extract text from image java
- aspose ocr tutorial java
- extract form data java
title: Εξαγωγή κειμένου από εικόνα java χρησιμοποιώντας Aspose OCR – οδηγός
url: /el/java/advanced-ocr-techniques/extract-text-from-image-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Απόσπαση κειμένου από εικόνα java χρησιμοποιώντας Aspose OCR – οδηγός

Έχετε ποτέ χρειαστεί να **αποσπάσετε κείμενο από εικόνα** αλλά καταλήξατε στο να αναλύετε ολόκληρη τη φωτογραφία, σπαταλώντας κύκλους CPU και λαμβάνοντας θορυβώδη αποτελέσματα; Δεν είστε ο μόνος. Σε πολλές πραγματικές εφαρμογές—σκεφτείτε σαρωτές τιμολογίων, αναγνώστες διαβατηρίων ή φόρμες εισαγωγής δεδομένων—σας ενδιαφέρουν μόνο μερικά πεδία, όχι ολόκληρος ο καμβάς.  

Τα καλά νέα είναι ότι το Aspose OCR σας επιτρέπει να **αποσπάσετε κείμενο από εικόνα** *και* από συγκεκριμένες περιοχές φόρμας ορίζοντας πολύγωνα. Σε αυτό το tutorial θα δείτε ακριβώς πώς να **αποσπάσετε κείμενο από πεδία φόρμας** χρησιμοποιώντας Java, γιατί η προσέγγιση είναι σημαντική και τι να ρυθμίσετε όταν τα πράγματα δεν πάνε όπως πρέπει.

Παρακάτω θα καλύψουμε τα πάντα, από τη ρύθμιση της βιβλιοθήκης μέχρι την αντιμετώπιση δύσκολων περιπτώσεων, ώστε στο τέλος να έχετε ένα έτοιμο προς εκτέλεση απόσπασμα κώδικα που εξάγει μόνο τα δεδομένα που χρειάζεστε.

## Γρήγορες απαντήσεις
- **Ποιο είναι το κύριο όφελος;** Η στοχευμένη OCR μειώνει το χρόνο επεξεργασίας έως και 70 % και εξαλείφει τον άσχετο θόρυβο.  
- **Ποια βιβλιοθήκη χρησιμοποιείται;** Aspose OCR for Java, τελευταία έκδοση 23.10.  
- **Χρειάζομαι Maven/Gradle;** Όχι, απλώς προσθέστε το JAR στο classpath σας.  
- **Μπορώ να επεξεργαστώ πολλαπλά πεδία;** Ναι—ορίστε ένα πολύγωνο για κάθε πεδίο και προσθέστε τα στη λίστα ROI.  
- **Ποια φορμά υποστηρίζονται;** Πάνω από 30 μορφές εικόνας, έως 100 MB ανά αρχείο χωρίς πλήρη φόρτωση στη μνήμη.

## Τι είναι η απόσπαση κειμένου από εικόνα java;
**Extract text from image java** αναφέρεται στη χρήση μιας μηχανής OCR βασισμένης σε Java για την ανάγνωση χαρακτήρων από γραφικά raster. Το Aspose OCR παρέχει μια υψηλής ακρίβειας μηχανή που υποστηρίζει Unicode, πολλές γλώσσες και προσαρμοσμένες περιοχές ενδιαφέροντος. Λειτουργεί αναλύοντας μοτίβα εικονοστοιχείων, τμηματοποιώντας χαρακτήρες και εφαρμόζοντας μοντέλα γλώσσας για την παραγωγή μηχανικά αναγνώσιμων συμβολοσειρών.

## Γιατί να χρησιμοποιήσετε το Aspose OCR για εξαγωγή δεδομένων φόρμας java;
Το Aspose OCR υποστηρίζει **πάνω από 50 μορφές εικόνας εισόδου** (συμπεριλαμβανομένων PNG, JPEG, TIFF, BMP) και μπορεί να επεξεργαστεί έγγραφα πολλαπλών σελίδων χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη, επιτυγχάνοντας έως και **3× ταχύτερη** απόδοση σε σχέση με γενικές λύσεις OCR όταν εφαρμόζεται φιλτράρισμα ROI. Επιπλέον, η δυνατότητα ROI μειώνει τη χρήση μνήμης, καθιστώντας το κατάλληλο για μεγάλης κλίμακας επεξεργασία παρτίδων σε περιβάλλοντα cloud.

## Προαπαιτούμενα

- Java 17 (ή οποιοδήποτε πρόσφατο JDK) – οι νεότερες εκδόσεις έχουν καλύτερη υποστήριξη Unicode.  
- Aspose.OCR for Java 23.10 (ή η πιο πρόσφατη έκδοση τη στιγμή της ανάγνωσης).  
- Ένα δείγμα εικόνας με όνομα `form.png` που περιέχει σαφώς ορισμένα πεδία.  
- Ένα IDE ή απλός επεξεργαστής κειμένου—IntelliJ IDEA, VS Code, ή ακόμη και Notepad αρκεί.

Δεν απαιτείται μαγεία Maven/Gradle για το βασικό demo· απλώς προσθέστε το JAR του Aspose OCR στο classpath.

---

## Βήμα 1 – Αρχικοποίηση της μηχανής OCR και φόρτωση της εικόνας σας

OcrEngine είναι η βασική κλάση που συντονίζει τις λειτουργίες OCR, εκθέτοντας ρυθμίσεις όπως η γλώσσα και η προεπεξεργασία εικόνας.  
ImageStream αντιπροσωπεύει τα δεδομένα της πηγαίας εικόνας και παρέχει στατικές βοηθητικές μεθόδους όπως `fromFile` για τη φόρτωση μιας εικόνας από δίσκο.  
Polygon είναι ένα σχήμα Java AWT που χρησιμοποιείται για τον ορισμό των κορυφών μιας περιοχής ενδιαφέροντος.

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the source image – replace the path if your file lives elsewhere
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));
```

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the source image – replace the path if your file lives elsewhere
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));
```

*Γιατί είναι σημαντικό:*  
Δημιουργώντας ένα νέο `OcrEngine` έχετε ένα καθαρό ξεκίνημα, εξασφαλίζοντας ότι δεν υπάρχουν απομεινάρια ρυθμίσεων που να επηρεάζουν την εκτέλεσή σας. Η πρόωρη φόρτωση της εικόνας επίσης επαληθεύει ότι το αρχείο υπάρχει, ώστε να λάβετε μια χρήσιμη εξαίρεση πριν σπαταλήσετε χρόνο σε επόμενα βήματα.

> **Συμβουλή:** Αν η εικόνα σας είναι τεράστια (πάνω από 5 MB), σκεφτείτε να την αλλάξετε μέγεθος πρώτα. Το Aspose OCR λειτουργεί πιο γρήγορα σε εικόνες κάτω από 2000 px σε οποιαδήποτε διάσταση.

## Βήμα 2 – Ορισμός πολυγώνων για τα πεδία που θέλετε να διαβάσετε

Μια *Περιοχή ενδιαφέροντος* (ROI) είναι απλώς ένα πολύγωνο που λέει στη μηχανή πού να κοιτάξει. Παρακάτω δημιουργούμε δύο ορθογώνια—ένα για το “First Name” και ένα άλλο για το “Date of Birth”. Προσαρμόστε τις συντεταγμένες ώστε να ταιριάζουν στη δική σας φόρμα.

```java
        // Polygon for the first field (e.g., First Name)
        Polygon firstField = new Polygon(
                new int[]{50, 200, 200, 50},   // X‑coordinates
                new int[]{100, 100, 150, 150}, // Y‑coordinates
                4);

        // Polygon for the second field (e.g., Date of Birth)
        Polygon secondField = new Polygon(
                new int[]{300, 500, 500, 300},
                new int[]{200, 200, 250, 250},
                4);
```

*Γιατί πολύγωνα αντί για ορθογώνια;*  
Τα πολύγωνα σας δίνουν την ευελιξία να χειρίζεστε παραμορφωμένα ή μη-ορθογώνια κουτιά—συνηθισμένο όταν σαρώνονται έντυπες φόρμες που δεν είναι τέλεια ευθυγραμμισμένες.

## Βήμα 3 – Ενημέρωση του Aspose OCR να εστιάσει μόνο σε αυτές τις περιοχές

Τώρα συνδέουμε τα πολύγωνα με τη μηχανή. Η μέθοδος `setRegionsOfInterest` καταχωρεί τη λίστα των πολυγώνων στις οποίες η μηχανή πρέπει να εστιάσει, και δέχεται μια λίστα, ώστε να μπορείτε να προσθέσετε όσα πεδία θέλετε.

```java
        // Limit OCR to the defined regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));
```

*Τι συμβαίνει στο παρασκήνιο;*  
Το Aspose OCR περικόπτει κάθε πολύγωνο σε ξεχωριστό bitmap, εκτελεί τον αλγόριθμο αναγνώρισης και στη συνέχεια συνενώνει τα αποτελέσματα. Αυτό μειώνει δραστικά τα ψευδώς θετικά από τα γύρω γραφικά.

## Βήμα 4 – Εκτέλεση της διαδικασίας OCR

OcrResult περιλαμβάνει το αναγνωρισμένο κείμενο μαζί με μετρικές εμπιστοσύνης για κάθε επεξεργασμένη περιοχή.

```java
        // Execute OCR on the selected ROIs
        OcrResult ocrResult = ocrEngine.process();
```

Αν χρειάζεστε εμπιστοσύνη ανά πεδίο, μπορείτε να ελέγξετε το `ocrResult.getRegions()`—κάθε περιοχή φέρει το δικό της σκορ. Για τις περισσότερες απλές φόρμες, το συνολικό κείμενο είναι επαρκές.

## Βήμα 5 – Εμφάνιση (ή αποθήκευση) του εξαγόμενου κειμένου

Τέλος, εκτυπώνουμε το αποτέλεσμα στην κονσόλα. Σε μια πραγματική εφαρμογή μπορεί να γράψετε σε βάση δεδομένων, αρχείο JSON ή να το στείλετε μέσω API.

```java
        // Output the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**Αναμενόμενο αποτέλεσμα (παράδειγμα):**

```
=== Extracted Text ===
John Doe
12/04/1990
```

Οι δύο γραμμές αντιστοιχούν στα δύο πολύγωνα που ορίσαμε. Αν δείτε επιπλέον κενά, αφαιρέστε τα με `String.trim()`.

## Πώς να αποσπάσετε κείμενο από φόρμα όταν έχετε πολλά πεδία

Η χειροκίνητη εισαγωγή συντεταγμένων για κάθε πεδίο γίνεται γρήγορα επιρρεπής σε σφάλματα και χρονοβόρα, ειδικά όταν οι φόρμες εξελίσσονται. Εξωτερικοποιώντας τους ορισμούς ROI σε ένα CSV, μπορείτε να τους διατηρείτε ξεχωριστά, να ελέγχετε τις αλλαγές με version‑control και να επιτρέψετε στον κώδικα Java να δημιουργεί δυναμικά τα απαιτούμενα πολύγωνα κατά το χρόνο εκτέλεσης.

1. **Δημιουργήστε ένα CSV** όπου κάθε γραμμή περιέχει `fieldName, x1, y1, x2, y2, x3, y3, x4, y4`.  
2. **Φορτώστε το CSV** κατά το χρόνο εκτέλεσης, επαναλάβετε για κάθε γραμμή, δημιουργήστε ένα `Polygon` και προσθέστε το στη λίστα ROI.  

```java
List<Polygon> rois = new ArrayList<>();
try (BufferedReader br = new BufferedReader(new FileReader("fields.csv"))) {
    String line;
    while ((line = br.readLine()) != null) {
        String[] parts = line.split(",");
        int[] xs = { Integer.parseInt(parts[1]), Integer.parseInt(parts[3]),
                    Integer.parseInt(parts[5]), Integer.parseInt(parts[7]) };
        int[] ys = { Integer.parseInt(parts[2]), Integer.parseInt(parts[4]),
                    Integer.parseInt(parts[6]), Integer.parseInt(parts[8]) };
        rois.add(new Polygon(xs, ys, 4));
    }
}
ocrEngine.getEngineOptions().setRegionsOfInterest(rois);
```

*Γιατί να ασχοληθείτε;*  
Η αυτοματοποίηση της δημιουργίας ROI σας επιτρέπει να επαναχρησιμοποιήσετε τον ίδιο κώδικα Java σε πολλαπλές διατάξεις φόρμας, διατηρώντας το έργο σας DRY (Don’t Repeat Yourself).

## Περιπτώσεις άκρων & συμβουλές που ίσως δεν είχατε σκεφτεί

- **Περιστροφές σαρώσεων:** Αν ολόκληρη η εικόνα είναι περιστραμμένη, καλέστε `ocrEngine.getEngineOptions().setRotateAngle(degrees)`.  
- **Χαμηλή αντίθεση:** Ορίστε `ocrEngine.getEngineOptions().setContrast(1.5f)` για να βελτιώσετε την αναγνωσιμότητα.  
- **Μη‑λατινικά σενάρια:** Αλλάξτε τη γλώσσα με `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.Spanish)` (ή οποιαδήποτε υποστηριζόμενη γλώσσα).  
- **Μερικές αποτυχίες OCR:** Πάντα ελέγχετε το `ocrResult.getConfidence()`· αν πέσει κάτω από 80 %, σκεφτείτε να ζητήσετε από τον χρήστη χειροκίνητη επαλήθευση.  

## Πλήρες λειτουργικό παράδειγμα (έτοιμο για αντιγραφή‑επικόλληση)

Παρακάτω είναι το πλήρες πρόγραμμα, έτοιμο για μεταγλώττιση και εκτέλεση. Αντικαταστήστε το `YOUR_DIRECTORY` με το φάκελο που περιέχει το `form.png`.

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Step 1 – Initialize engine and load image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));

        // Step 2 – Define polygons for each form field
        Polygon firstField = new Polygon(
                new int[]{50, 200, 200, 50},
                new int[]{100, 100, 150, 150},
                4);
        Polygon secondField = new Polygon(
                new int[]{300, 500, 500, 300},
                new int[]{200, 200, 250, 250},
                4);

        // Step 3 – Limit OCR to those regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));

        // Step 4 – Run OCR
        OcrResult ocrResult = ocrEngine.process();

        // Step 5 – Show the result
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Μεταγλώττιση με:

```bash
javac -cp "aspose-ocr-23.10.jar" MultiRoiDemo.java
java -cp ".:aspose-ocr-23.10.jar" MultiRoiDemo
```

Θα πρέπει να δείτε τις δύο γραμμές κειμένου που ανήκουν στις ορισμένες ROI.

## Συχνές ερωτήσεις

**Q: Λειτουργεί αυτό με PDFs;**  
A: Όχι άμεσα. Μετατρέψτε κάθε σελίδα PDF σε εικόνα πρώτα (π.χ., χρησιμοποιώντας Aspose PDF) και στη συνέχεια δώστε την εικόνα στη μηχανή OCR.

**Q: Τι γίνεται αν η φόρμα μου έχει κουτάκια ελέγχου;**  
A: Το OCR δεν μπορεί να διαβάσει boolean καταστάσεις, αλλά μπορείτε να θεωρήσετε την περιοχή του κουτιού ως ROI και να εξετάσετε την πυκνότητα εικονοστοιχείων για να υποθέσετε ένα σημάδι.

**Q: Μπορώ να αποσπάσω κείμενο από μια πολύ‑σελίδα φόρμα σε μία φορά;**  
A: Επαναλάβετε για κάθε εικόνα σελίδας, χρησιμοποιήστε ξανά την ίδια λίστα ROI και συνενώστε τα αποτελέσματα.

**Q: Πώς βελτιώνω την ακρίβεια σε σαρώσεις χαμηλής ποιότητας;**  
A: Αυξήστε την αντίθεση, ενεργοποιήστε τη δυαδικοποίηση μέσω `ocrEngine.getEngineOptions().setBinarization(true)`, και σκεφτείτε προεπεξεργασία της εικόνας για αφαίρεση θορύβου.

**Q: Απαιτείται άδεια για χρήση σε παραγωγή;**  
A: Ναι. Το Aspose OCR προσφέρει δωρεάν δοκιμή, αλλά απαιτείται εμπορική άδεια για την ανάπτυξη.

---

**Τελευταία ενημέρωση:** 2026-09-28  
**Δοκιμάστηκε με:** Aspose.OCR for Java 23.10  
**Συγγραφέας:** Aspose

## Σχετικά Μαθήματα

- [Απόσπαση Κειμένου από Εικόνα Java με Aspose.OCR Detect Areas Mode](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Προεπεξεργασία Εικόνας Ocr σε Java για Βελτίωση Ακρίβειας Απόσπασης Κειμένου](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)
- [Ανίχνευση Γλώσσας Εικόνας με Aspose Ocr Java Tutorial](/ocr/java/advanced-ocr-techniques/detect-language-image-with-aspose-ocr-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}