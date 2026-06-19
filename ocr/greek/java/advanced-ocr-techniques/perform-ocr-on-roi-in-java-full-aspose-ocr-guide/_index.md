---
category: general
date: 2026-06-19
description: Εκτελέστε OCR σε περιοχή ενδιαφέροντος (ROI) σε Java χρησιμοποιώντας
  το Aspose OCR. Μάθετε πώς να αναγνωρίζετε κείμενο σε μια περιοχή με βήμα‑βήμα κώδικα
  και βέλτιστες πρακτικές.
draft: false
keywords:
- perform OCR on ROI
- recognize text in region
- Aspose OCR Java
- OCR region detection
- Java image processing
language: el
og_description: Εκτελέστε OCR σε περιοχή ενδιαφέροντος (ROI) σε Java με το Aspose
  OCR. Αυτός ο οδηγός σας δείχνει πώς να αναγνωρίζετε κείμενο σε περιοχή, να διαχειρίζεστε
  πολλαπλές γλώσσες και να αποφεύγετε κοινά προβλήματα.
og_title: Εκτελέστε OCR σε ROI σε Java – Πλήρες Μάθημα Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Perform OCR on ROI in Java using Aspose OCR. Learn how to recognize
    text in region with step‑by‑step code and best practices.
  headline: Perform OCR on ROI in Java – Full Aspose OCR Guide
  type: TechArticle
- description: Perform OCR on ROI in Java using Aspose OCR. Learn how to recognize
    text in region with step‑by‑step code and best practices.
  name: Perform OCR on ROI in Java – Full Aspose OCR Guide
  steps:
  - name: 1. License Path Errors
    text: If `setLicense` throws a `FileNotFoundException`, double‑check the absolute
      path or place the `.lic` file in the project’s resources folder and load it
      with `getResourceAsStream`.
  - name: 2. Overlapping or Out‑of‑Bounds ROIs
    text: Aspose does not automatically clip ROIs that extend beyond the image dimensions.
      Overlapping rectangles can cause duplicated text. Use `engine.getImageSize()`
      to verify bounds before creating rectangles.
  - name: 3. Unsupported Languages
    text: Attempting to set a language not bundled with the library will raise `UnsupportedOperationException`.
      Stick to the languages listed in Aspose’s documentation, or download the additional
      language packs.
  - name: 4. Low‑Resolution Images
    text: OCR accuracy drops dramatically below 100 dpi. If you have a low‑resolution
      scan, consider up‑scaling with a library like **Imgscalr** before feeding it
      to Aspose.
  type: HowTo
tags:
- OCR
- Java
- Aspose
- Image Recognition
title: Εκτελέστε OCR στην ROI σε Java – Πλήρης Οδηγός Aspose OCR
url: /el/java/advanced-ocr-techniques/perform-ocr-on-roi-in-java-full-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε ROI σε Java – Πλήρης Οδηγός Aspose OCR

Έχετε αναρωτηθεί ποτέ πώς να **perform OCR on ROI** σε Java; Δεν είστε μόνοι—οι προγραμματιστές ρωτούν συνεχώς, *«Πώς μπορώ να εξάγω μόνο το τμήμα του πίνακα ενός τιμολογίου χωρίς να σαρώσω ολόκληρη την εικόνα;»* Σε αυτόν τον οδηγό θα περάσουμε βήμα-βήμα πώς να **perform OCR on ROI** χρησιμοποιώντας το Aspose OCR, και επίσης θα σας δείξουμε πώς να **recognize text in region** όταν διαφορετικές γλώσσες εμφανίζονται πλάι‑πλάι.

Το θέμα είναι: η στόχευση ενός συγκεκριμένου ορθογωνίου (ή ROI) εξοικονομεί χρόνο επεξεργασίας, μειώνει τον θόρυβο και συχνά αποδίδει πιο καθαρά αποτελέσματα. Είτε εργάζεστε με πολυγλωσσικές αποδείξεις, φόρμες ή σαρωμένα συμβόλαια, η εξοικείωση με το OCR βασισμένο σε ROI είναι αλλαγή παιχνιδιού. Ας βουτήξουμε.

## Τι Θα Χρειαστείτε

- **Java 8+** (ο κώδικας λειτουργεί σε οποιοδήποτε πρόσφατο JDK)
- **Aspose.OCR for Java** βιβλιοθήκη (κατεβάστε από τον ιστότοπο Aspose ή προσθέστε μέσω Maven)
- Ένα έγκυρο αρχείο άδειας **Aspose OCR** (`Aspose.OCR.lic`) – η demo λειτουργεί χωρίς άδεια αλλά θα προσθέσει υδατογράφημα.
- Μια εικόνα που περιέχει διακριτές περιοχές που θέλετε να επεξεργαστείτε (π.χ., ένα τιμολόγιο με κεφαλίδα και έναν γαλλικό πίνακα).

Αυτό είναι όλο—χωρίς επιπλέον frameworks, χωρίς βαριές εξαρτήσεις. Αν αισθάνεστε άνετα με ένα βασικό IDE όπως το IntelliJ IDEA ή το Eclipse, είστε έτοιμοι.

## Εκτέλεση OCR σε ROI – Ρύθμιση της Μηχανής

Το πρώτο βήμα είναι να προετοιμάσετε τη μηχανή OCR και να της πείτε ποια γλώσσα θα χρησιμοποιεί εξ ορισμού. Εδώ αρχίζει πραγματικά η ροή εργασίας **perform OCR on ROI**.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.geometry.*;

public class RoiDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply the Aspose OCR license
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

> **Pro tip:** Αν ξεχάσετε να ορίσετε την άδεια, το Aspose θα λειτουργήσει ακόμη αλλά θα ενσωματώσει ένα υδατογράφημα “Evaluation” στην έξοδο. Είναι αβλαβές για δοκιμές αλλά όχι για παραγωγή.

## Ορίστε τις Περιοχές που Θέλετε να Αναγνωρίσετε

Τώρα δημιουργούμε τα ορθογώνια που αντιπροσωπεύουν τα τμήματα της εικόνας που μας ενδιαφέρουν. Σκεφτείτε κάθε `Rectangle` ως ένα “κουτί περικοπής” που λέει στη μηχανή *πού* να κοιτάξει.

```java
        // Step 2: Create an OCR engine and set the default language
        OcrEngine engine = new OcrEngine();
        engine.setLanguage(Language.English);

        // Step 3: Define the regions (ROIs) you want to recognize
        // Header region (top part of the image)
        Rectangle header = new Rectangle(0, 0, 1200, 200);
        // Table body region (below the header)
        Rectangle table = new Rectangle(0, 210, 1200, 800);
```

Παρατηρήστε πώς χρησιμοποιήσαμε την ορολογία **perform OCR on ROI** έμμεσα—κάθε `Rectangle` είναι ένα ROI. Μπορείτε να προσαρμόσετε τις συντεταγμένες ώστε να ταιριάζουν με τη διάταξη του δικού σας εγγράφου. Το ορθογώνιο `header` καταγράφει την κορυφαία λωρίδα, ενώ το ορθογώνιο `table` παίρνει το σώμα όπου θα **recognize text in region** αργότερα.

## Προσθήκη Περιοχών και Ορισμός Γλωσσών ανά Περιοχή

Το Aspose OCR σας επιτρέπει να ορίσετε μια γλώσσα ανά περιοχή, κάτι τέλειο για πολυγλωσσικά έγγραφα. Εδώ διατηρούμε τα Αγγλικά για την κεφαλίδα και μεταβαίνουμε στα Γαλλικά για τον πίνακα.

```java
        // Step 4: Add the regions to the engine
        engine.addRegion(header);                     // uses default language (English)
        engine.addRegion(table, Language.French);    // optional per‑region language
```

Αν χρειάζεστε μόνο μία γλώσσα, μπορείτε να παραλείψετε το δεύτερο όρισμα. Η μηχανή θα επιστρέψει αυτόματα στην προεπιλεγμένη γλώσσα που ορίσατε νωρίτερα.

## Εκτέλεση OCR σε ROI και Ανάκτηση Συνδυασμένου Κειμένου

Τέλος, εκτελούμε τη διαδικασία OCR σε ολόκληρη την εικόνα, αλλά μόνο οι ορισμένες ROIs θα υποβληθούν σε επεξεργασία. Το αποτέλεσμα ενώνει το κείμενο με τη σειρά που προσθέσατε τις περιοχές, κάτι που κάνει την μεταεπεξεργασία απλή.

```java
        // Step 5: Perform OCR on the image and retrieve the combined text
        OcrResult result = engine.recognizeImage("YOUR_DIRECTORY/invoice.png");
        System.out.println(result.getText()); // text from all defined regions in order
    }
}
```

**Αναμενόμενο αποτέλεσμα** (συνοπτικά για συντομία):

```
Invoice #12345
Date: 2026‑06‑01
...
Produit   Quantité   Prix
Café      2          5,00 €
...
```

Το πρώτο μπλοκ προέρχεται από την αγγλική κεφαλίδα, το δεύτερο από τον γαλλικό πίνακα—ένα κλασικό παράδειγμα **recognize text in region** με μεικτές γλώσσες.

## Διαχείριση Συνηθισμένων Προβλημάτων

Ακόμη και μια απλή ροή **perform OCR on ROI** μπορεί να αντιμετωπίσει μερικά κρυφά προβλήματα. Παρακάτω είναι τα πιο συχνά ζητήματα και πώς να τα αποφύγετε.

### 1. Σφάλματα Διαδρομής Άδειας

Αν το `setLicense` ρίξει `FileNotFoundException`, ελέγξτε ξανά την απόλυτη διαδρομή ή τοποθετήστε το αρχείο `.lic` στο φάκελο resources του έργου και φορτώστε το με `getResourceAsStream`.

```java
License license = new License();
license.setLicense(RoiDemo.class.getResourceAsStream("/Aspose.OCR.lic"));
```

### 2. Αλληλοεπικάλυπτα ή Εκτός Ορίων ROIs

Το Aspose δεν κόβει αυτόματα τα ROIs που εκτείνονται πέρα από τις διαστάσεις της εικόνας. Τα αλληλοεπικάλυπτα ορθογώνια μπορούν να προκαλέσουν διπλότυπο κείμενο. Χρησιμοποιήστε `engine.getImageSize()` για να επαληθεύσετε τα όρια πριν δημιουργήσετε τα ορθογώνια.

```java
Size imgSize = engine.getImageSize("YOUR_DIRECTORY/invoice.png");
if (header.getRight() > imgSize.getWidth()) {
    // Adjust width to stay inside the image
    header.setWidth(imgSize.getWidth() - header.getX());
}
```

### 3. Μη Υποστηριζόμενες Γλώσσες

Η προσπάθεια ορισμού γλώσσας που δεν περιλαμβάνεται στη βιβλιοθήκη θα προκαλέσει `UnsupportedOperationException`. Παραμείνετε στις γλώσσες που αναφέρονται στην τεκμηρίωση του Aspose ή κατεβάστε τα πρόσθετα πακέτα γλωσσών.

### 4. Εικόνες Χαμηλής Ανάλυσης

Η ακρίβεια του OCR μειώνεται δραματικά κάτω από 100 dpi. Αν έχετε σάρωση χαμηλής ανάλυσης, σκεφτείτε την αύξηση κλίμακας με μια βιβλιοθήκη όπως η **Imgscalr** πριν την δώσετε στο Aspose.

```java
BufferedImage src = ImageIO.read(new File("invoice.png"));
BufferedImage highRes = Scalr.resize(src, Scalr.Method.QUALITY, 300);
ImageIO.write(highRes, "png", new File("invoice_high.png"));
```

Στη συνέχεια, κατευθύνετε το `recognizeImage` στο `invoice_high.png`.

## Επέκταση του Παραδείγματος: Πολλαπλά ROIs και Δυναμική Ανίχνευση

Η demo χρησιμοποιεί στατικά ορθογώνια, αλλά σε πραγματικές περιπτώσεις ίσως θέλετε να εντοπίζετε πίνακες αυτόματα. Συνδυάστε το Aspose OCR με μια απλή βιβλιοθήκη **image processing** (π.χ., OpenCV) για να εντοπίσετε περιγράμματα, και στη συνέχεια περάστε αυτά τα όρια στο `engine.addRegion`. Αυτό μετατρέπει ένα στατικό script **perform OCR on ROI** σε μια δυναμική γραμμή εργασίας που λειτουργεί σε οποιαδήποτε διάταξη τιμολογίου.

```java
// Pseudo‑code: Detect contours → create Rectangle objects → addRegion()
List<Rect> detected = OpenCVHelper.findTables("invoice.png");
for (Rect r : detected) {
    engine.addRegion(new Rectangle(r.x, r.y, r.width, r.height), Language.French);
}
```

Τώρα μπορείτε να **recognize text in region** χωρίς να κωδικοποιείτε σκληρά τις τιμές pixel—χρήσιμο για επεξεργασία παρτίδων.

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω είναι το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα. Αντικαταστήστε το `YOUR_DIRECTORY` με την πραγματική διαδρομή στο μηχάνημά σας.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.geometry.*;

public class RoiDemo {
    public static void main(String[] args) throws Exception {
        // Apply license (optional for evaluation)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // Initialize engine with default language
        OcrEngine engine = new OcrEngine();
        engine.setLanguage(Language.English);

        // Define ROIs
        Rectangle header = new Rectangle(0, 0, 1200, 200);   // top banner
        Rectangle table  = new Rectangle(0, 210, 1200, 800); // body table

        // Add regions – per‑region language optional
        engine.addRegion(header);                     // English (default)
        engine.addRegion(table, Language.French);    // French for table

        // Run OCR on the image – only the defined ROIs are processed
        OcrResult result = engine.recognizeImage("YOUR_DIRECTORY/invoice.png");

        // Output combined text
        System.out.println("--- OCR Result ---");
        System.out.println(result.getText());
    }
}
```

Εκτελέστε `javac RoiDemo.java && java RoiDemo`. Αν όλα είναι ρυθμισμένα σωστά, θα δείτε το ενωμένο κείμενο από τις δύο περιοχές να εκτυπώνεται στην κονσόλα.

## Συμπέρασμα

Μόλις καλύψαμε πώς να **perform OCR on ROI** σε Java χρησιμοποιώντας το Aspose OCR, και τώρα ξέρετε πώς να **recognize text in region** για σενάρια μονογλωσσικών και πολυγλωσσικών κειμένων. Με το να χωρίζετε την εικόνα σε λογικά ορθογώνια μπορείτε:

1. Να μειώσετε τον χρόνο επεξεργασίας,
2. Να μειώσετε τα ψευδώς θετικά,
3. Να αποκτήσετε λεπτομερή έλεγχο της επιλογής γλώσσας.

Από εδώ μπορείτε να εξερευνήσετε δυναμική ανίχνευση ROI, να ενσωματώσετε τα αποτελέσματα σε μια βάση δεδομένων, ή να δημιουργήσετε PDF με δυνατότητα αναζήτησης. Ο ουρανός είναι το όριο—απλώς θυμηθείτε να επικυρώσετε τις συντεταγμένες ROI, να διατηρήσετε τη διαδρομή της άδειας τακτική, και να επιλέξετε τα σωστά πακέτα γλώσσας.

Έχετε μια δύσκολη διάταξη με την οποία παλεύετε; Αφήστε ένα σχόλιο ή στείλτε ένα pull request με τις βελτιώσεις σας. Καλή προγραμματιστική δουλειά, και εύχομαι το OCR σας να είναι πάντα ακριβές!

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικά θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε σε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Αναγνωρίσετε Τα Ορθογώνια Σελίδας για Αναγνώριση Κειμένου OCR στο Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/)
- [Εξαγωγή Κειμένου από Εικόνα Java με Aspose.OCR Λειτουργία Ανίχνευσης Περιοχών](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Πώς να Κάνετε OCR Κειμένου Εικόνας με Γλώσσα Χρησιμοποιώντας Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}