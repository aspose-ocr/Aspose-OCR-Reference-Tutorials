---
category: general
date: 2026-07-05
description: πώς να κάνετε OCR πίνακα χρησιμοποιώντας τη τεχνική επιλεγμένης περιοχής
  του Java OCR. Μάθετε πώς να εξάγετε εικόνα δεδομένων πίνακα και να αναγνωρίσετε
  περιοχή κειμένου με ένα έτοιμο παράδειγμα προς εκτέλεση.
draft: false
keywords:
- how to ocr table
- ocr selected area
- extract table data image
- recognize text region
language: el
og_description: 'πώς να κάνετε OCR πίνακα σε Java: ένα πρακτικό σεμινάριο που δείχνει
  πώς να κάνετε OCR σε επιλεγμένη περιοχή, να εξάγετε την εικόνα δεδομένων του πίνακα
  και να αναγνωρίσετε την περιοχή κειμένου με πλήρες κώδικα πηγής.'
og_title: πώς να κάνετε OCR πίνακα σε Java – Πλήρης Οδηγός
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: how to ocr table using Java OCR selected area technique. Learn to extract
    table data image and recognize text region with a ready‑to‑run example.
  headline: how to ocr table in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: how to ocr table using Java OCR selected area technique. Learn to extract
    table data image and recognize text region with a ready‑to‑run example.
  name: how to ocr table in Java – Complete Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '- Java 17 or newer (the code compiles on JDK 11+ as well). - An OCR library
      that provides `OcrEngine`, `Region`, and `RecognitionResult` classes (e.g.,
      Aspose.OCR for Java, Tesseract‑Java wrapper, or any vendor‑specific SDK). -
      A sample image (`rotated_table.png`) placed in a known directory. - Basi'
  - name: 1. Different Image Formats
    text: Most OCR SDKs accept PNG, JPEG, BMP, and TIFF. If you receive a PDF, convert
      the first page to an image first (e.g., using Apache PDFBox). This extra step
      ensures the **ocr selected area** logic works on a raster image.
  - name: 2. Varying Rotation Angles
    text: The automatic deskew works best for rotations up to ±15°. For extreme angles,
      pre‑rotate the image using a library like `java.awt.Graphics2D` before feeding
      it to the OCR engine.
  - name: 3. Large Images and Memory Footprint
    text: If the source image is huge (several megabytes), consider scaling it down
      while preserving DPI. Most SDKs expose a `setResolution(int dpi)` method; 300
      dpi is a good compromise between speed and accuracy.
  - name: 4. Capturing Structured Data
    text: Some OCR engines can return a table model (rows × columns) instead of plain
      text. Look for methods like `recognitionResult.getTable()` or `recognitionResult.getCsv()`.
      When available, you can directly feed the result into a database or spreadsheet.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
- Table Extraction
title: πώς να κάνετε OCR πίνακα σε Java – Πλήρης Οδηγός Βήμα‑προς‑Βήμα
url: /el/java/advanced-ocr-techniques/how-to-ocr-table-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# πώς να κάνετε OCR πίνακα σε Java – Πλήρης Οδηγός Βήμα‑βήμα

Έχετε αναρωτηθεί ποτέ **how to ocr table** από ένα σαρωμένο έγγραφο χωρίς να φορτώνετε ολόκληρη τη σελίδα στη μνήμη; Δεν είστε οι μόνοι. Σε πολλά πραγματικά έργα—π.χ. επεξεργασία τιμολογίων ή μεταφορά δεδομένων από παλαιά PDF—μόνο η περιοχή του πίνακα έχει σημασία, ενώ το υπόλοιπο είναι απλώς θόρυβος.  

Σε αυτό το tutorial θα περάσουμε από ένα συμπαγές, εκτελέσιμο παράδειγμα που δείχνει **how to ocr table** στοχεύοντας ένα συγκεκριμένο ορθογώνιο, αφήνοντας τη μηχανή να διορθώσει αυτόματα την κλίση του περιεχομένου. Στο τέλος θα μπορείτε να **ocr selected area**, **extract table data image**, και **recognize text region** με λίγες μόνο γραμμές Java.

## Τι Θα Μάθετε

- Πώς να δημιουργήσετε μια παρουσία OCR engine σε Java.  
- Πώς να ορίσετε μια **Region** που απομονώνει τον περιστραμμένο πίνακα.  
- Πώς να αφήσετε το OCR engine να **recognize text region** ενώ διορθώνει την κλίση.  
- Πώς να εκτυπώσετε το εξαγόμενο κείμενο του πίνακα στην κονσόλα.  
- Συμβουλές για διαχείριση διαφορετικών μορφών εικόνας, γωνιών περιστροφής και βελτιστοποιήσεων απόδοσης.

### Προαπαιτούμενα

- Java 17 ή νεότερη (ο κώδικας μεταγλωττίζεται και σε JDK 11+).  
- Μια βιβλιοθήκη OCR που παρέχει τις κλάσεις `OcrEngine`, `Region` και `RecognitionResult` (π.χ. Aspose.OCR for Java, Tesseract‑Java wrapper, ή οποιοδήποτε SDK προμηθευτή).  
- Ένα δείγμα εικόνας (`rotated_table.png`) τοποθετημένο σε γνωστό φάκελο.  
- Βασική εξοικείωση με Maven/Gradle για διαχείριση εξαρτήσεων.

> **Pro tip:** Αν χρησιμοποιείτε Maven, προσθέστε την εξάρτηση της βιβλιοθήκης OCR στο `pom.xml`. Για Gradle, τοποθετήστε την στο `build.gradle`. Οι ακριβείς συντεταγμένες διαφέρουν ανά προμηθευτή, αλλά συνήθως είναι της μορφής `com.aspose:aspose-ocr:23.10`.

---

## Βήμα 1: Αρχικοποίηση του OCR Engine – ο Πυρήνας του **how to ocr table**

Η δημιουργία μιας παρουσίας engine είναι το πρώτο βήμα κάθε φορά που θέλετε να **ocr selected area**. Σκεφτείτε το engine ως τον εγκέφαλο που θα ερμηνεύσει τα pixel μέσα στο ορθογώνιο που ορίζετε.

```java
// Step 1: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

> **Γιατί είναι σημαντικό:** Χωρίς engine δεν υπάρχει πλαίσιο για γλώσσα, λειτουργία ανίχνευσης ή επιλογές διόρθωσης κλίσης. Τα περισσότερα SDK επιτρέπουν την προσαρμογή αυτών των ρυθμίσεων (π.χ. `ocrEngine.setLanguage(Language.English)`) πριν καλέσετε οποιαδήποτε μέθοδο αναγνώρισης.

---

## Βήμα 2: Ορισμός της Περιοχής που Περιέχει τον Περιστραμμένο Πίνακα

Ένα αντικείμενο **Region** περιγράφει τις συντεταγμένες `(x, y, width, height)` της περιοχής που θέλετε να επεξεργαστείτε. Στην περίπτωσή μας ο πίνακας βρίσκεται στο `(120, 350)` και έχει διαστάσεις `800 × 500` pixel. Προσαρμόστε αυτούς τους αριθμούς ώστε να ταιριάζουν με το δικό σας έγγραφο.

```java
// Step 2: Define the region (x, y, width, height) that contains the rotated table
Region tableRegion = new Region(120, 350, 800, 500);
```

> **Γιατί είναι σημαντικό:** Περιορίζοντας το OCR σε μια **selected area**, μειώνετε δραστικά το χρόνο επεξεργασίας και βελτιώνετε την ακρίβεια. Το engine θα διορθώσει αυτόματα την κλίση του περιεχομένου μέσα σε αυτό το ορθογώνιο, κάτι που είναι κρίσιμο όταν ο πίνακας είναι περιστραμμένος.

---

## Βήμα 3: Αναγνώριση Κειμένου Μέσα στην Περιοχή – **recognize text region** σε Δράση

Τώρα δίνουμε στο engine τη διαδρομή της εικόνας και την προηγουμένως ορισμένη `Region`. Η μέθοδος `recognizeRegion` κάνει δύο πράγματα: κόβει την εικόνα στο ορθογώνιο και στη συνέχεια εκτελεί OCR, εφαρμόζοντας τυχόν απαραίτητη διόρθωση περιστροφής.

```java
// Step 3: Recognize text only within the specified region; the engine will deskew it automatically
RecognitionResult recognitionResult = ocrEngine.recognizeRegion(
        "YOUR_DIRECTORY/rotated_table.png",   // path to your image
        tableRegion);                         // the region we defined above
```

> **Γιατί είναι σημαντικό:** Αυτή η ενιαία κλήση αντικαθιστά μια πολυβήμα διαδικασία που θα απαιτούσε χειροκίνητο κόψιμο, διόρθωση κλίσης και μετά OCR. Είναι η καρδιά του **how to ocr table** με αποδοτικό τρόπο.

---

## Βήμα 4: Εξαγωγή του Κειμένου του Πίνακα – Επαλήθευση του Αποτελέσματος **extract table data image**

Τέλος, εκτυπώνουμε το αποτέλεσμα του OCR. Το αντικείμενο `RecognitionResult` συνήθως περιέχει το ακατέργαστο κείμενο, βαθμούς εμπιστοσύνης και, προαιρετικά, μια δομημένη αναπαράσταση (π.χ. μια συμβολοσειρά CSV).

```java
// Step 4: Output the extracted text
System.out.println("Table text:");
System.out.println(recognitionResult.getText());
```

> **Αναμενόμενο αποτέλεσμα (παράδειγμα):**  

```
Table text:
Item   Qty   Price
Apple   10   $1.20
Banana   5   $0.80
Total        $16.00
```

Αν ο πίνακας παραμένει λανθασμένα ευθυγραμμισμένος, μπορείτε να προσαρμόσετε τις διαστάσεις της `Region` ή να ενεργοποιήσετε επεξεργασία υψηλότερης ανάλυσης μέσω των ρυθμίσεων του engine.

---

## Διαχείριση Συνηθισμένων Περιπτώσεων

### 1. Διαφορετικές Μορφές Εικόνας

Τα περισσότερα OCR SDK αποδέχονται PNG, JPEG, BMP και TIFF. Αν λάβετε PDF, μετατρέψτε πρώτα την πρώτη σελίδα σε εικόνα (π.χ. με Apache PDFBox). Αυτό το επιπλέον βήμα εξασφαλίζει ότι η λογική **ocr selected area** λειτουργεί σε raster εικόνα.

### 2. Μεταβαλλόμενες Γωνίες Περιστροφής

Η αυτόματη διόρθωση κλίσης λειτουργεί καλύτερα για περιστροφές έως ±15°. Για ακραίες γωνίες, προ-περιστρέψτε την εικόνα χρησιμοποιώντας βιβλιοθήκη όπως `java.awt.Graphics2D` πριν τη δώσετε στο OCR engine.

```java
BufferedImage src = ImageIO.read(new File("rotated_table.png"));
AffineTransform tx = new AffineTransform();
tx.rotate(Math.toRadians(30), src.getWidth() / 2, src.getHeight() / 2);
AffineTransformOp op = new AffineTransformOp(tx, AffineTransformOp.TYPE_BILINEAR);
BufferedImage rotated = op.filter(src, null);
ImageIO.write(rotated, "png", new File("pre_rotated.png"));
```

Στη συνέχεια κατευθύνετε το `recognizeRegion` στο `pre_rotated.png`.

### 3. Μεγάλες Εικόνες και Χρήση Μνήμης

Αν η πηγή εικόνας είναι τεράστια (μερικά megabytes), σκεφτείτε να τη σμικρύνετε διατηρώντας το DPI. Τα περισσότερα SDK εκθέτουν μέθοδο `setResolution(int dpi)`· 300 dpi είναι καλή ισορροπία μεταξύ ταχύτητας και ακρίβειας.

### 4. Λήψη Δομημένων Δεδομένων

Κάποια OCR engines μπορούν να επιστρέψουν μοντέλο πίνακα (γραμμές × στήλες) αντί για απλό κείμενο. Αναζητήστε μεθόδους όπως `recognitionResult.getTable()` ή `recognitionResult.getCsv()`. Όταν είναι διαθέσιμες, μπορείτε να τροφοδοτήσετε άμεσα το αποτέλεσμα σε βάση δεδομένων ή υπολογιστικό φύλλο.

---

## Πλήρες Παράδειγμα Εφαρμογής

Παρακάτω βρίσκεται το ολοκληρωμένο, έτοιμο‑για‑εκτέλεση πρόγραμμα Java που συνδυάζει όλα τα παραπάνω. Αντικαταστήστε το `YOUR_DIRECTORY` με την πραγματική διαδρομή της εικόνας σας.

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.Region;

public class TableOcrDemo {
    public static void main(String[] args) {
        // Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Optional: set language and other settings
        // ocrEngine.setLanguage(Language.English);
        // ocrEngine.setResolution(300);

        // Define the region that contains the rotated table
        Region tableRegion = new Region(120, 350, 800, 500);

        // Perform OCR on the selected area – the engine deskews automatically
        RecognitionResult recognitionResult = ocrEngine.recognizeRegion(
                "YOUR_DIRECTORY/rotated_table.png",
                tableRegion);

        // Print the extracted table text
        System.out.println("Table text:");
        System.out.println(recognitionResult.getText());
    }
}
```

**Εκτέλεση του προγράμματος** (`javac TableOcrDemo.java && java TableOcrDemo`) θα πρέπει να εκτυπώσει τα περιεχόμενα του πίνακα στην κονσόλα, επιβεβαιώνοντας ότι έχετε εξάγει επιτυχώς **extract table data image** από μια περιστραμμένη πηγή.

---

## Pro Tips & Gotchas

- **Επεξεργασία σε παρτίδες:** Τυλίξτε τη λογική σε βρόχο αν έχετε πολλές εικόνες. Η επαναχρησιμοποίηση της ίδιας παρουσίας `OcrEngine` μειώνει το κόστος αρχικοποίησης.  
- **Φίλτρο εμπιστοσύνης:** Μερικά engines εκθέτουν `recognitionResult.getConfidence()`. Απορρίψτε γραμμές με εμπιστοσύνη < 80 % και σημειώστε τις για χειροκίνητη επανεξέταση.  
- **Βελτιστοποίηση απόδοσης:** Για μεγάλες παρτίδες, ενεργοποιήστε πολυνηματικότητα (`ExecutorService`) αλλά θυμηθείτε ότι τα περισσότερα OCR engines είναι περιορισμένα από την CPU και μπορεί να μην κλιμακώνονται γραμμικά.  
- **Νομική σημείωση:** Σεβαστείτε πάντα τα πνευματικά δικαιώματα όταν επεξεργάζεστε σαρωμένα έγγραφα· βεβαιωθείτε ότι έχετε το δικαίωμα εξαγωγής δεδομένων.

---

## Συμπέρασμα

Ολοκληρώσαμε έναν σύντομο αλλά πλήρη οδηγό **how to ocr table** που δείχνει πώς να **ocr selected area**, **extract table data image**, και **recognize text region** χρησιμοποιώντας μια Java OCR engine. Τα βασικά βήματα—δημιουργία engine, ορισμός περιοχής, αναγνώριση με βάση την περιοχή, και έξοδο—αποτελούν ένα επαναχρησιμοποιήσιμο μοτίβο που μπορείτε να προσαρμόσετε σε οποιοδήποτε σενάριο εξαγωγής πινάκων.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να εξάγετε το αποτέλεσμα OCR σε CSV, να το τροφοδοτήσετε σε μοντέλο μηχανικής μάθησης, ή να δημιουργήσετε μικροϋπηρεσία που δέχεται URL εικόνας και επιστρέφει δομημένο JSON. Ο ουρανός είναι το όριο όταν κυριαρχήσετε στο **how to ocr table** σε Java.

Καλή προγραμματιστική, και μη διστάσετε να αφήσετε ερωτήσεις ή ιστορίες επιτυχίας στα σχόλια παρακάτω! 

![how to ocr table example](ocr-table-diagram.png "how to ocr table example")


## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Πώς να Αναγνωρίζετε Πλαίσια Σελίδας για OCR Αναγνώριση Κειμένου στο Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/)
- [Εξαγωγή Κειμένου από Εικόνα Java με Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Αναγνώριση εικόνας κειμένου με Aspose OCR – Πλήρης Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}