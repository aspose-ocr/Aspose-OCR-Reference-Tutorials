---
category: general
date: 2026-02-14
description: Εξάγετε κείμενο από εικόνα χρησιμοποιώντας το Aspose OCR. Μάθετε πώς
  να φορτώνετε εικόνα για OCR, να διαβάζετε κείμενο από ορθογώνιο και να ακολουθήσετε
  αυτό το σεμινάριο Aspose OCR σε λίγα λεπτά.
draft: false
keywords:
- extract text from image
- load image for ocr
- read text from rectangle
- aspose ocr tutorial
language: el
og_description: Εξάγετε κείμενο από εικόνα άμεσα. Αυτός ο οδηγός δείχνει πώς να φορτώσετε
  εικόνα για OCR, να διαβάσετε κείμενο από ορθογώνιο και να ολοκληρώσετε έναν οδηγό
  Aspose OCR.
og_title: Εξαγωγή κειμένου από εικόνα με Aspose OCR – Σύντομος οδηγός
tags:
- Aspose
- OCR
- Java
title: Εξαγωγή κειμένου από εικόνα με το Aspose OCR – Demo βήμα‑βήμα
url: /el/java/ocr-operations/extract-text-from-image-with-aspose-ocr-step-by-step-demo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή κειμένου από εικόνα με Aspose OCR – Βήμα‑βήμα επίδειξη

Έχετε ποτέ χρειαστεί να **εξάγετε κείμενο από εικόνα** αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το εμπόδιο όταν προσπαθούν για πρώτη φορά να σαρώσουν αποδείξεις ή να επαληθεύσουν ταυτότητες. Τα καλά νέα; Με το Aspose OCR μπορείτε να φορτώσετε μια εικόνα, να ορίσετε την ακριβή περιοχή όπου βρίσκεται το κείμενο και να εξάγετε τους χαρακτήρες σε λίγες γραμμές.

Σε αυτό το **aspose ocr tutorial** θα περάσουμε από όλα όσα χρειάζεστε: τη φόρτωση της εικόνας για OCR, τον ορισμό ενός ορθογωνίου που λέει στη μηχανή πού να κοιτάξει, και τέλος την ανάγνωση του εξαγόμενου κειμένου. Στο τέλος θα έχετε ένα εκτελέσιμο πρόγραμμα Java που εκτυπώνει το κείμενο ROI στην κονσόλα—χωρίς μυστήριο, μόνο μια σαφής, λειτουργική λύση.

## Τι θα χρειαστείτε

| Προαπαιτούμενο | Γιατί είναι σημαντικό |
|--------------|----------------|
| **Java JDK 8+** | Το Aspose OCR διανέμεται ως βιβλιοθήκη Java· οποιοδήποτε σύγχρονο JDK είναι επαρκές. |
| **Aspose.OCR for Java** (download from the Aspose website or add via Maven) | Παρέχει τις κλάσεις `OcrEngine`, `ImageStream` και σχετικές. |
| **An image file** (e.g., `receipt.jpg`) that contains printable text | Θα υποδείξουμε στη μηχανή ένα ορθογώνιο μέσα σε αυτό το αρχείο. |
| **IDE or editor** (IntelliJ, Eclipse, VS Code…) | Σας βοηθά να μεταγλωττίσετε και να εκτελέσετε το παράδειγμα γρήγορα. |

Αν χρησιμοποιείτε Maven, προσθέστε αυτήν την εξάρτηση στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check Aspose for the latest version -->
</dependency>
```

> **Συμβουλή:** Ο αριθμός έκδοσης παραπάνω είναι τρέχων από τον Φεβρουάριο 2026. Η ενημέρωση στην τελευταία έκδοση εξασφαλίζει διορθώσεις σφαλμάτων και βελτιώσεις απόδοσης.

## Βήμα 1 – Αρχικοποίηση του OCR Engine

Πρώτα απ' όλα: χρειάζεστε μια παρουσία του `OcrEngine`. Σκεφτείτε το ως τον εγκέφαλο που θα αναλύσει τα pixel.

```java
// Step 1: Create the OCR engine object
OcrEngine ocrEngine = new OcrEngine();
```

Γιατί το δημιουργούμε με αυτόν τον τρόπο; Το Aspose διαχωρίζει τη μηχανή (που κρατά τη διαμόρφωση) από τα δεδομένα εικόνας, δίνοντάς σας ευελιξία να επαναχρησιμοποιήσετε την ίδια μηχανή για πολλαπλές εικόνες αν το επιθυμείτε.

## Βήμα 2 – Φόρτωση εικόνας για OCR

Τώρα πραγματικά **φορτώνουμε εικόνα για OCR**. Η βοηθητική μέθοδος `ImageStream.fromFile` διαβάζει το αρχείο σε μια ροή που μπορεί να καταλάβει το Aspose.

```java
// Step 2: Load the target image (replace with your own path)
String imagePath = "YOUR_DIRECTORY/receipt.jpg";
ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

Αν το αρχείο δεν βρεθεί, η μηχανή ρίχνει εξαίρεση, οπότε ίσως θέλετε να το τυλίξετε σε μπλοκ try‑catch σε κώδικα παραγωγής. Για αυτήν την επίδειξη αφήνουμε την εξαίρεση να ανεβεί—διατηρεί το παράδειγμα καθαρό.

## Βήμα 3 – Ορισμός του Ορθογωνίου (Ανάγνωση κειμένου από ορθογώνιο)

Εδώ λάμπει το τμήμα **read text from rectangle**. Λέτε στη μηχανή ακριβώς πού να κοιτάξει, κάτι που επιταχύνει την επεξεργασία και μειώνει τα ψευδώς θετικά.

```java
// Step 3: Create a rectangle that covers the area with the receipt total
// Parameters: x, y, width, height (all in pixels)
Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);
```

> **Γιατί ένα ορθογώνιο;**  
> Τα περισσότερα έγγραφα έχουν προβλέψιμες διατάξεις—σκεφτείτε μια απόδειξη όπου το ποσό εμφανίζεται πάντα κοντά στο κάτω μέρος. Εστιάζοντας σε αυτό το τμήμα, η μηχανή OCR αγνοεί άσχετα γραφικά και αυξάνει την ακρίβεια.

**Περίπτωση άκρης:** Αν το ορθογώνιο υπερβαίνει τα όρια της εικόνας, το Aspose το περιορίζει σιωπηρά, αλλά θα χάσετε δεδομένα. Μια γρήγορη έλεγχος λογικής μπορεί να το αποτρέψει:

```java
if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
    regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
    throw new IllegalArgumentException("ROI exceeds image dimensions.");
}
```

## Βήμα 4 – Επεξεργασία της εικόνας

Με όλα ρυθμισμένα, ζητάμε από τη μηχανή να κάνει τη μαγεία της.

```java
// Step 4: Run OCR on the defined ROI
OcrResult ocrResult = ocrEngine.process();
```

Η κλήση `process()` επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει το εξαγόμενο κείμενο, τις βαθμολογίες εμπιστοσύνης, και ακόμη τα πλαίσια περιγράμματος για κάθε λέξη αν τα χρειαστείτε αργότερα.

## Βήμα 5 – Εξαγωγή του εξαγόμενου κειμένου

Τέλος, εκτυπώστε το αποτέλεσμα. Σε μια πραγματική εφαρμογή μπορεί να το αποθηκεύσετε σε βάση δεδομένων ή να το στείλετε σε άλλη υπηρεσία, αλλά για αυτό το tutorial η έξοδος στην κονσόλα είναι αρκετή.

```java
// Step 5: Display the recognized text
System.out.println("ROI text:");
System.out.println(ocrResult.getText());
```

**Αναμενόμενη έξοδος** (υποθέτοντας ότι το ορθογώνιο κατέγραψε το συνολικό ποσό σε μια απόδειξη):

```
ROI text:
$12.34
```

Αν το ROI είναι κενό ή η εικόνα είναι θολή, θα δείτε μια κενή συμβολοσειρά ή ακατάληπτους χαρακτήρες. Προσαρμόστε το ορθογώνιο, βελτιώστε την ποιότητα της εικόνας, ή ενεργοποιήστε τις επιλογές προεπεξεργασίας του Aspose (π.χ., `setAutoSkewCorrection(true)`).

## Πλήρες λειτουργικό παράδειγμα

Παρακάτω είναι το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα. Αντιγράψτε‑και‑επικολλήστε το σε ένα αρχείο με όνομα `RoiDemo.java`, προσαρμόστε τη διαδρομή της εικόνας, και εκτελέστε `javac RoiDemo.java && java RoiDemo`.

```java
import com.aspose.ocr.*;
import java.awt.Rectangle;

/**
 * Demo: Extract text from a specific rectangle (ROI) in an image using Aspose OCR.
 * Adjust the rectangle coordinates to match the area you want to read.
 */
public class RoiDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image for OCR
        // Replace YOUR_DIRECTORY with the actual folder containing receipt.jpg
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.jpg"));

        // Step 3: Define the region of interest where text is expected
        // (x, y, width, height) in pixels
        Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
        ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);

        // Optional sanity check – ensures ROI fits inside the image
        if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
            regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
            throw new IllegalArgumentException("ROI exceeds image dimensions.");
        }

        // Step 4: Perform OCR on the defined ROI
        OcrResult ocrResult = ocrEngine.process();

        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(ocrResult.getText());
    }
}
```

> **Επαλήθευση αποτελέσματος:** Μετά την εκτέλεση, συγκρίνετε την έξοδο της κονσόλας με το πραγματικό κείμενο μέσα στο ορθογώνιο. Αν ταιριάζουν, έχετε εξαγάγει επιτυχώς **κείμενο από εικόνα** χρησιμοποιώντας το Aspose OCR.

## Συχνές ερωτήσεις & Συμβουλές

### Τι γίνεται αν χρειαστεί να επεξεργαστώ πολλαπλά ROI στην ίδια εικόνα;
Δημιουργήστε ένα νέο `Rectangle` για κάθε περιοχή, καλέστε ξανά `setRegionOfInterest` και ξανα‑εκτελέστε `process()`. Η μηχανή επαναχρησιμοποιεί τα ίδια δεδομένα εικόνας, οπότε η απόδοση παραμένει γρήγορη.

### Πώς διαχειρίζεται το Aspose διαφορετικές γλώσσες ή γραμματοσειρές;
Μπορείτε να αλλάξετε το μοντέλο γλώσσας μέσω `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.English)`. Για μη‑λατινικά σενάρια, φορτώστε το κατάλληλο πακέτο γλώσσας (διαθέσιμο στη σελίδα λήψης του Aspose).

### Υποστηρίζει η βιβλιοθήκη είσοδο PDF;
Ναι—το Aspose OCR μπορεί να δεχτεί ροές PDF απευθείας. Απλώς αντικαταστήστε το `ImageStream.fromFile` με `ImageStream.fromPdfFile("doc.pdf")` και προαιρετικά καθορίστε τον αριθμό σελίδας.

### Μπορώ να βελτιώσω την ακρίβεια σε σαρώσεις χαμηλής ποιότητας;
Ενεργοποιήστε την προεπεξεργασία:

```java
ocrEngine.getEngineOptions().setAutoSkewCorrection(true);
ocrEngine.getEngineOptions().setBinarizationMethod(BinarizationMethod.Otsu);
```

## Συμπέρασμα

Μόλις περάσαμε από ένα πλήρες **aspose ocr tutorial** που δείχνει πώς να **εξάγετε κείμενο από εικόνα**, **φορτώσετε εικόνα για OCR**, και **διαβάσετε κείμενο από ορθογώνιο** χρησιμοποιώντας Java. Τα βασικά βήματα είναι η αρχικοποίηση της μηχανής, η παροχή μιας εικόνας, ο ορισμός μιας περιοχής ενδιαφέροντος, η επεξεργασία, και τέλος η εκτύπωση του αποτελέσματος.

Από εδώ μπορείτε να εξερευνήσετε:

* **Batch processing** – επανάληψη πάνω σε φάκελο αποδείξεων και αποθήκευση κάθε συνολικού ποσού σε βάση δεδομένων.  
* **Dynamic ROI detection** – χρήση βιβλιοθηκών επεξεργασίας εικόνας (OpenCV) για αυτόματη εντοπισμό μπλοκ κειμένου.  
* **Post‑processing** – εφαρμογή regex ή fuzzy matching για καθαρισμό των ιδιομορφιών του OCR.

Δοκιμάστε αυτές τις ιδέες, προσαρμόστε το ορθογώνιο ώστε να ταιριάζει στα δικά σας έγγραφα, και θα έχετε μια αξιόπιστη αλυσίδα εξαγωγής κειμένου σε ελάχιστο χρόνο. Καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}