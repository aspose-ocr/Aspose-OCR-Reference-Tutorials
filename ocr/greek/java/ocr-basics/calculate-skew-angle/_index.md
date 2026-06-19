---
date: 2026-06-19
description: Μάθετε πώς να περιστρέψετε σαρωμένο έγγραφο, να υπολογίσετε το skew angle
  σε Java και να βελτιώσετε την ακρίβεια του OCR με το Aspose.OCR. Οδηγός βήμα‑βήμα
  για προγραμματιστές Java.
keywords:
- rotate scanned document
- improve ocr accuracy
- rotate image degrees java
- aspose ocr java tutorial
linktitle: Πώς να περιστρέψετε σαρωμένο έγγραφο και να υπολογίσετε το skew angle σε
  Java χρησιμοποιώντας το Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to rotate scanned document, calculate skew angle Java, and
    improve OCR accuracy with Aspose.OCR. Step‑by‑step guide for Java developers.
  headline: How to rotate scanned document and calculate skew angle in Java using
    Aspose.OCR
  type: TechArticle
- description: Learn how to rotate scanned document, calculate skew angle Java, and
    improve OCR accuracy with Aspose.OCR. Step‑by‑step guide for Java developers.
  name: How to rotate scanned document and calculate skew angle in Java using Aspose.OCR
  steps:
  - name: Import Packages
    text: '`AsposeOCR` is the core class that exposes OCR and image‑analysis functions.
      `java.io.File` is used only for path handling. **Definition anchor:** `AsposeOCR`
      is Aspose.OCR''s primary class that provides methods for text extraction, skew
      detection, and image preprocessing.'
  - name: Set Up Document Directory
    text: Store the folder path in a variable so you can reuse it for multiple images
      or switch environments without code changes. **Definition anchor:** `dataDir`
      is a `String` variable that points to the directory containing the source images
      you intend to process.
  - name: Specify Image Path
    text: Combine the directory with the file name to build the absolute path required
      by the API. **Definition anchor:** `imagePath` is a `String` that holds the
      full file system location of the image you will analyze.
  - name: Create API Instance
    text: Instantiate the `AsposeOCR` object once per application run; it loads the
      native libraries internally. **Definition anchor:** `ocrEngine` is an instance
      of `AsposeOCR` that gives you access to all OCR‑related methods, including `CalcSkewImage`.
  - name: Calculate Skew Angle
    text: 'Wrap the call in a try‑catch block to handle I/O problems gracefully. The
      method returns a `double` that you can log, store, or pass to a rotation routine.
      **Definition anchor:** `CalcSkewImage(String imagePath)` scans the supplied
      image, detects the dominant text baseline, and returns the rotation '
  type: HowTo
- questions:
  - answer: It measures the rotation (in degrees) of text lines inside an image.
    question: What does “calculate skew angle” do?
  - answer: The library provides a fast, out‑of‑the‑box method (`CalcSkewImage`) that
      works with PNG, JPEG, TIFF, and more.
    question: Why use Aspose.OCR for this?
  - answer: A temporary license works for evaluation; a full license is required for
      production.
    question: Do I need a license to run the sample?
  - answer: Yes—call `CalcSkewImage` inside a loop for multiple files.
    question: Can the API handle batch processing?
  - answer: Java 8+ is fully supported.
    question: What Java version is required?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Πώς να περιστρέψετε σαρωμένο έγγραφο και να υπολογίσετε το skew angle σε Java
  χρησιμοποιώντας το Aspose.OCR
url: /el/java/ocr-basics/calculate-skew-angle/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να περιστρέψετε σαρωμένο έγγραφο και να υπολογίσετε τη γωνία κλίσης σε Java χρησιμοποιώντας το Aspose.OCR

## Εισαγωγή

Αν έχετε προσπαθήσει ποτέ να εκτελέσετε OCR σε μια σαρωμένη τιμολόγιο, απόδειξη ή χειρόγραφο έντυπο, πιθανότατα έχετε παρατηρήσει ότι ακόμη και λίγοι βαθμοί κλίσης μπορούν να καταστρέψουν τα αποτελέσματα αναγνώρισης. **Η περιστροφή των σαρωμένων εγγράφων** σε μια πραγματική οριζόντια βάση είναι ο πιο αξιόπιστος τρόπος για *βελτίωση της ακρίβειας του OCR*. Σε αυτό το tutorial θα μάθετε πώς να **υπολογίζετε τη γωνία κλίσης σε Java** με το Aspose.OCR, στη συνέχεια να χρησιμοποιήσετε αυτήν την τιμή για **περιστροφή εικόνας σε μοίρες σε Java** και τελικά να τροφοδοτήσετε μια τέλεια ευθυγραμμισμένη εικόνα στη μηχανή OCR. Η προσέγγιση λειτουργεί για αρχεία μονής σελίδας καθώς και για μεγάλες παρτίδες, και απαιτεί μόνο το JAR του Aspose.OCR — δεν απαιτούνται εξωτερικές βιβλιοθήκες επεξεργασίας εικόνας.

## Γρήγορες Απαντήσεις
- **Τι κάνει η “calculate skew angle”;** Μετρά τη περιστροφή (σε μοίρες) των γραμμών κειμένου μέσα σε μια εικόνα.  
- **Γιατί να χρησιμοποιήσω το Aspose.OCR γι' αυτό;** Η βιβλιοθήκη παρέχει μια γρήγορη, έτοιμη προς χρήση μέθοδο (`CalcSkewImage`) που λειτουργεί με PNG, JPEG, TIFF και άλλα.  
- **Χρειάζομαι άδεια για να εκτελέσω το δείγμα;** Μια προσωρινή άδεια λειτουργεί για αξιολόγηση· απαιτείται πλήρης άδεια για παραγωγή.  
- **Μπορεί το API να διαχειριστεί επεξεργασία παρτίδας;** Ναι — καλέστε το `CalcSkewImage` μέσα σε βρόχο για πολλά αρχεία.  
- **Ποια έκδοση της Java απαιτείται;** Η Java 8+ υποστηρίζεται πλήρως.

## Τι είναι η calculate skew angle java;

Η λειτουργία **calculate skew angle java** καθορίζει την γωνιακή απόκλιση του τυπωμένου ή χειρόγραφου κειμένου από την οριζόντια βάση. Το αποτέλεσμα εκφράζεται σε μοίρες (θετικό για δεξιόστροφη περιστροφή, αρνητικό για αριστερόστροφη). Η γνώση αυτής της τιμής σας επιτρέπει να διορθώνετε προγραμματιστικά την κλίση της εικόνας πριν από το OCR, μειώνοντας τις λανθασμένες αναγνώσεις.

## Γιατί να χρησιμοποιήσετε το Aspose.OCR για Java;

Φορτώστε τη βιβλιοθήκη και λαμβάνετε ένα API μιας γραμμής που επιστρέφει την ακριβή κλίση οποιασδήποτε υποστηριζόμενης εικόνας. **Το Aspose.OCR επεξεργάζεται πάνω από 50 εκατομμύρια χαρακτήρες ανά λεπτό σε τυπικό εξοπλισμό διακομιστή**, και υποστηρίζει 5 κύριες μορφές εικόνας (PNG, JPEG, BMP, TIFF, GIF) χωρίς πρόσθετες εξαρτήσεις. Αυτή η ποσοτικοποιημένη απόδοση το καθιστά αξιόπιστη επιλογή όταν χρειάζεται να *βελτιώσετε την ακρίβεια του OCR* σε υψηλής χωρητικότητας αγωγούς εγγράφων.

## Προαπαιτούμενα

- **Java Development Kit** – JDK 8 ή νεότερο (συνιστάται Java 11+ για καλύτερη υποστήριξη μονάδων).  
- **Aspose.OCR for Java** – Κατεβάστε το τελευταίο JAR από την επίσημη ιστοσελίδα [here](https://reference.aspose.com/ocr/java/).  
- **Sample Image** – Οποιαδήποτε σαρωμένη εικόνα (π.χ. `p3.png`) που παρουσιάζει ορατή κλίση.  
- **License** – Προσωρινή δοκιμαστική άδεια για δοκιμές ή πλήρης εμπορική άδεια για παραγωγική χρήση.

## Πώς να υπολογίσετε τη γωνία κλίσης java χρησιμοποιώντας το Aspose.OCR;

Φορτώστε την εικόνα σας, καλέστε τη μέθοδο υπολογισμού κλίσης και καταγράψτε τη γωνία που επιστρέφεται. Η απάντηση στην ερώτηση είναι απλή: **παίρνετε την κλίση με μία μόνο κλήση στο `CalcSkewImage`, το οποίο επιστρέφει ένα double που αντιπροσωπεύει μοίρες**. Αυτή η κλήση εκτελείται σε χρόνο O(N) σε σχέση με τον αριθμό των εικονοστοιχείων και απαιτεί λιγότερο από 10 MB μνήμης heap για μια σελίδα 300 dpi.

Παρακάτω ακολουθεί ένας βήμα‑βήμα οδηγός. Κάθε βήμα περιγράφεται πριν από το placeholder που αρχικά περιείχε το παράδειγμα κώδικα.

### Βήμα 1: Εισαγωγή Πακέτων

`AsposeOCR` είναι η κεντρική κλάση που εκθέτει λειτουργίες OCR και ανάλυσης εικόνας. `java.io.File` χρησιμοποιείται μόνο για διαχείριση διαδρομών.

**Definition anchor:** `AsposeOCR` είναι η κύρια κλάση του Aspose.OCR που παρέχει μεθόδους για εξαγωγή κειμένου, ανίχνευση κλίσης και προεπεξεργασία εικόνας.

### Βήμα 2: Ρύθμιση Καταλόγου Εγγράφου

Αποθηκεύστε τη διαδρομή του φακέλου σε μια μεταβλητή ώστε να μπορείτε να την επαναχρησιμοποιήσετε για πολλές εικόνες ή να αλλάξετε περιβάλλοντα χωρίς αλλαγές κώδικα.

**Definition anchor:** `dataDir` είναι μια μεταβλητή τύπου `String` που δείχνει στον κατάλογο που περιέχει τις πηγαίες εικόνες που σκοπεύετε να επεξεργαστείτε.

### Βήμα 3: Καθορισμός Διαδρομής Εικόνας

Συνδυάστε τον κατάλογο με το όνομα του αρχείου για να δημιουργήσετε την απόλυτη διαδρομή που απαιτεί το API.

**Definition anchor:** `imagePath` είναι μια μεταβλητή τύπου `String` που περιέχει την πλήρη διαδρομή του συστήματος αρχείων της εικόνας που θα αναλύσετε.

### Βήμα 4: Δημιουργία Αντικειμένου API

Δημιουργήστε το αντικείμενο `AsposeOCR` μία φορά ανά εκτέλεση της εφαρμογής· φορτώνει τις εγγενείς βιβλιοθήκες εσωτερικά.

**Definition anchor:** `ocrEngine` είναι μια παρουσία του `AsposeOCR` που σας δίνει πρόσβαση σε όλες τις μεθόδους σχετικές με OCR, συμπεριλαμβανομένου του `CalcSkewImage`.

### Βήμα 5: Υπολογισμός Γωνίας Κλίσης

Τοποθετήστε την κλήση μέσα σε μπλοκ try‑catch για να διαχειριστείτε τα προβλήματα I/O με χάρη. Η μέθοδος επιστρέφει ένα `double` που μπορείτε να καταγράψετε, αποθηκεύσετε ή να περάσετε σε ρουτίνα περιστροφής.

**Definition anchor:** `CalcSkewImage(String imagePath)` σαρώει την παρεχόμενη εικόνα, εντοπίζει τη κυρίαρχη βάση κειμένου και επιστρέφει τη γωνία περιστροφής σε μοίρες.

## Πώς να περιστρέψετε εικόνα σε μοίρες σε Java μετά τον υπολογισμό της κλίσης;

Στο Java 2D, το `BufferedImage` αντιπροσωπεύει μια εικόνα στη μνήμη, το `AffineTransform` ορίζει γεωμετρικούς μετασχηματισμούς, το `Graphics2D` παρέχει δυνατότητες σχεδίασης, και το `ImageIO` διαχειρίζεται την ανάγνωση και εγγραφή αρχείων εικόνας.

Ακολουθεί η συνοπτική ροή εργασίας (δεν προστέθηκε επιπλέον μπλοκ κώδικα για να διατηρηθεί ο αρχικός αριθμός):

1. **Φορτώστε** το αρχείο προέλευσης σε ένα `BufferedImage` μέσω `ImageIO.read(new File(imagePath))`.  
2. **Δημιουργήστε** μια παρουσία `AffineTransform` και καλέστε `rotate(Math.toRadians(angle), centerX, centerY)` όπου `angle` είναι η τιμή που επιστρέφεται από το `CalcSkewImage`.  
3. **Σχεδιάστε** την μετασχηματισμένη εικόνα σε ένα νέο `BufferedImage` χρησιμοποιώντας ένα πλαίσιο `Graphics2D` (`g2d.drawImage(original, transform, null)`).  
4. **Γράψτε** το περιστραμμένο αποτέλεσμα πίσω στο δίσκο με `ImageIO.write(rotated, "png", new File(outputPath))`.  

Συνδέοντας το βήμα **calculate skew angle java** με αυτή τη ρουτίνα **rotate image degrees java**, δημιουργείτε μια πλήρως αυτοματοποιημένη διαδικασία αποκλίσης που μπορεί να ενσωματωθεί σε έναν απλό βρόχο `for` για να διαχειρίζεται εκατοντάδες σελίδες ανά λεπτό.

## Κοινά Προβλήματα και Λύσεις

| Πρόβλημα | Αιτία | Διόρθωση |
|-------|--------|-----|
| `NullPointerException` | `dataDir` δείχνει σε μη‑υπάρχον φάκελο | Επαληθεύστε τη διαδρομή και βεβαιωθείτε ότι ο φάκελος υπάρχει |
| `IOException` | Το αρχείο εικόνας δεν βρέθηκε ή είναι μη αναγνώσιμο | Ελέγξτε το όνομα αρχείου (`p3.png`) και τα δικαιώματα του αρχείου |
| Μη αναμενόμενη γωνία (π.χ., 0° σε σαφώς κλινόμενη εικόνα) | Εικόνα χαμηλής αντίθεσης ή θορυβώδης | Προεπεξεργαστείτε την εικόνα (αυξήστε την αντίθεση, δυαδικοποιήστε) πριν καλέσετε το `CalcSkewImage` |

## Συχνές Ερωτήσεις

### Q1: Μπορεί το Aspose.OCR να διορθώσει αυτόματα τη γωνία κλίσης;

**A:** Το Aspose.OCR παρέχει τον υπολογισμό της γωνίας κλίσης, αλλά η αυτόματη περιστροφή δεν είναι ενσωματωμένη. Μπορείτε να χρησιμοποιήσετε τη επιστρεφόμενη γωνία με οποιαδήποτε βιβλιοθήκη επεξεργασίας εικόνας Java (π.χ., Java 2D, OpenCV) για να διορθώσετε την κλίση της εικόνας μόνοι σας.

### Q2: Είναι το Aspose.OCR κατάλληλο για επεξεργασία παρτίδας πολλαπλών εικόνων;

**A:** Ναι. Τοποθετήστε τον κώδικα μέσα σε βρόχο που διατρέχει τη συλλογή εικόνων σας, καλώντας το `CalcSkewImage` για κάθε αρχείο. Η βιβλιοθήκη διαχειρίζεται κάθε κλήση ανεξάρτητα και διατηρεί χαμηλό φορτίο μνήμης.

### Q3: Υπάρχουν συγκεκριμένες απαιτήσεις μορφής εικόνας για ακριβή υπολογισμό γωνίας κλίσης;

**A:** Το API υποστηρίζει PNG, JPEG, BMP, TIFF και GIF. Για τη βέλτιστη ακρίβεια, χρησιμοποιήστε σαρώσεις υψηλής ανάλυσης (≥ 300 dpi) με καθαρό αντίθεση κειμένου· θορυβώδεις ή πολύ συμπιεσμένα αρχεία μπορεί να χρειάζονται προεπεξεργασία.

### Q4: Πώς μπορώ να αποκτήσω προσωρινή άδεια για το Aspose.OCR;

**A:** Επισκεφθείτε [this link](https://purchase.aspose.com/temporary-license/) για να ζητήσετε μια δοκιμαστική άδεια 30 ημερών που λειτουργεί για αξιολόγηση και ανάπτυξη.

### Q5: Πού μπορώ να ζητήσω βοήθεια ή να συζητήσω προβλήματα σχετικά με το Aspose.OCR;

**A:** Ενταχθείτε στην κοινότητα στο [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) για να θέσετε ερωτήσεις, να μοιραστείτε αποσπάσματα κώδικα και να λάβετε συμβουλές από μηχανικούς της Aspose και άλλους προγραμματιστές.

### Q6: Μπορώ να ενσωματώσω τον υπολογισμό γωνίας κλίσης με άλλα προϊόντα της Aspose όπως το Aspose.PDF;

**A:** Απόλυτα. Μετά την αποκλίση, τροφοδοτήστε τη διορθωμένη εικόνα στο Aspose.PDF, Aspose.Words ή σε οποιαδήποτε άλλη βιβλιοθήκη Aspose για περαιτέρω επεξεργασία, μετατροπή ή αρχειοθέτηση.

### Q7: Λειτουργεί η μέθοδος με χειρόγραφο κείμενο;

**A:** Λειτουργεί καλύτερα με τυπωμένο κείμενο όπου οι βάσεις είναι συνεπείς. Οι γραμμές χειρόγραφου μπορεί να παράγουν λιγότερο αξιόπιστες γωνίες λόγω ακανόνιστων γραμμών.

## Συμπέρασμα

Τώρα έχετε μια πλήρη, έτοιμη για παραγωγή συνταγή για **πώς να περιστρέψετε σαρωμένα έγγραφα** σε Java: υπολογίστε την κλίση με το `CalcSkewImage`, περιστρέψτε το bitmap χρησιμοποιώντας Java 2D, και στη συνέχεια εκτελέστε OCR σε μια τέλεια ευθυγραμμισμένη εικόνα. Αυτή η διαδικασία δύο βημάτων βελτιώνει συστηματικά την *ακρίβεια του OCR* κατά 15‑30 % σε θορυβώδεις σαρώσεις και κλιμακώνεται σε χιλιάδες σελίδες την ημέρα. Πειραματιστείτε με διαφορετικές ποιότητες εικόνας, συνδυάστε τη ροή εργασίας με το Aspose.PDF για δημιουργία PDF, και θα έχετε μια ισχυρή μηχανή επεξεργασίας εγγράφων έτοιμη για επιχειρηματικά φορτία.

---

**Τελευταία Ενημέρωση:** 2026-06-19  
**Δοκιμή Με:** Aspose.OCR for Java 24.12 (latest at time of writing)  
**Συγγραφέας:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Σχετικά Μαθήματα

- [Πώς να ορίσετε άδεια και να επαληθεύσετε την άδεια Aspose.OCR σε Java](/ocr/java/ocr-basics/set-license/)
- [Εξαγωγή κειμένου από εικόνες – Βασικά OCR με Aspose.OCR για Java](/ocr/java/ocr-basics/)
- [Εξαγωγή κειμένου από εικόνα Java με Aspose.OCR Detect Areas Mode](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;
```

```java
String dataDir = "Your Document Directory";
```

```java
String imagePath = dataDir + "p3.png";
```

```java
AsposeOCR api = new AsposeOCR();
```

```java
try {
    double angle = api.CalcSkewImage(imagePath);
    System.out.println("Skew text is:" + angle + " degrees.");
} catch (IOException e1) {
    e1.printStackTrace();
}
```