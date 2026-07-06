---
date: 2026-06-19
description: Μάθετε πώς να μετατρέψετε εικόνα σε κείμενο με Java, να εξάγετε παραγράφους
  από εικόνα και να ανακτήσετε ορθογώνια περιοχών κειμένου χρησιμοποιώντας τη βιβλιοθήκη
  Aspose OCR Java.
keywords:
- image to text java
- convert scanned image text
- extract paragraphs from image
- aspose ocr java tutorial
linktitle: Image to Text Java – Αναγνώριση κειμένου από εικόνα και ανάκτηση ορθογωνίων
  περιοχών κειμένου
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to convert image to text in Java, extract paragraphs from
    image, and retrieve text area rectangles using Aspose OCR Java library.
  headline: Image to Text Java – Convert Image to Text and Retrieve Text Area Rectangles
  type: TechArticle
- description: Learn how to convert image to text in Java, extract paragraphs from
    image, and retrieve text area rectangles using Aspose OCR Java library.
  name: Image to Text Java – Convert Image to Text and Retrieve Text Area Rectangles
  steps:
  - name: Set Up Your Project
    text: Create a new Java project (or add to an existing one) and place the Aspose.OCR
      JAR on the classpath. If you use Maven, add the dependency as described in the
      download package.
  - name: Define Document Directory and Image Path
    text: 'Specify where your sample image resides:'
  - name: Create AsposeOCR Instance
    text: '`AsposeOCR` is the main class that provides OCR functionality. Instantiate
      the OCR engine:'
  - name: Recognize Text in the Image
    text: Load your image and call `RecognizePage` to convert the picture into plain
      text. This single method call performs image preprocessing, character segmentation,
      and language‑specific recognition in one step.
  - name: Get Rectangles with Text Areas
    text: Retrieve the bounding rectangles for each paragraph (or other area types).
      This step returns a collection of `Rectangle` objects that precisely enclose
      the detected text blocks, enabling you to highlight or further process individual
      sections. CODE_BLOCK_PLACEHOLDER_5_END
  type: HowTo
- questions:
  - answer: Yes, Aspose.OCR works with Java 11 and later versions.
    question: Is Aspose.OCR compatible with Java 11?
  - answer: Yes, you can use it in any type of project. For licensing details, visit
      [here](https://purchase.aspose.com/buy).
    question: Can I use Aspose.OCR for both personal and commercial projects?
  - answer: You can obtain a temporary license [here](https://purchase.aspose.com/temporary-license/).
    question: How do I obtain a temporary license for evaluation?
  - answer: For support and discussions, visit the [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16).
    question: Where can I find community support or official assistance?
  - answer: Yes, the library is thread‑safe and can be used in concurrent environments
      for better performance.
    question: Does Aspose.OCR support multithreading?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Image to Text Java – Μετατροπή εικόνας σε κείμενο και ανάκτηση ορθογωνίων περιοχών
  κειμένου
url: /el/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εικόνα σε Κείμενο Java – Μετατροπή Εικόνας σε Κείμενο και Ανάκτηση Ορθογωνίων Περιοχών Κειμένου

## Εισαγωγή

Αν χρειάζεστε **μετατροπή εικόνας σε κείμενο** σε μια εφαρμογή Java, το Aspose.OCR for Java προσφέρει μια γρήγορη, ακριβή λύση. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα τις ακριβείς ενέργειες που απαιτούνται για την εξαγωγή παραγράφων από μια εικόνα, την απόκτηση των ορθογωνίων περιορισμού για κάθε περιοχή κειμένου, και την εκτύπωση αυτών των συντεταγμένων στην κονσόλα. Στο τέλος θα καταλάβετε γιατί αυτή η προσέγγιση λειτουργεί, πώς να ενσωματώσετε τη βιβλιοθήκη, και πού μπορείτε να την επεκτείνετε για τις δικές σας περιπτώσεις χρήσης.

## Γρήγορες Απαντήσεις
`AreasType` είναι μια απαρίθμηση που καθορίζει το επίπεδο τμηματοποίησης κειμένου (λέξεις, γραμμές, παράγραφοι).

- **Τι σημαίνει “recognize text from image”;** Σημαίνει τη μετατροπή των οπτικών χαρακτήρων σε μια εικόνα σε επεξεργάσιμα δεδομένα συμβολοσειράς.  
- **Ποια βιβλιοθήκη το διαχειρίζεται σε Java;** Aspose.OCR for Java.  
- **Χρειάζεται άδεια για ανάπτυξη;** Διατίθεται προσωρινή άδεια για δοκιμές· απαιτείται πλήρης άδεια για παραγωγή.  
- **Μπορώ να εξάγω παραγράφους αντί για μεμονωμένες λέξεις;** Ναι – χρησιμοποιήστε `AreasType.PARAGRAPHS` για να λάβετε ορθογώνια επιπέδου παραγράφου.  
- **Είναι ο κώδικας συμβατός με Java 11+;** Απόλυτα, το API λειτουργεί με Java 11 και νεότερες εκδόσεις.

## Τι είναι η “convert image to text” στο Aspose.OCR;

`convert image to text` αναφέρεται στη διαδικασία ανάλυσης ενός bitmap, εφαρμογής αλγορίθμων OCR, και επιστροφής των αναγνωρισμένων χαρακτήρων ως συμβολοσειρά. Η μέθοδος `RecognizePage` του Aspose.OCR εκτελεί αυτή τη μετατροπή ενώ προαιρετικά παρέχει τις ακριβείς συντεταγμένες `Rectangle` για κάθε ανιχνευμένο μπλοκ κειμένου.

## Γιατί να χρησιμοποιήσετε αυτή τη **java ocr library**;

Το Aspose.OCR υποστηρίζει **30+ γλώσσες** και μπορεί να επεξεργαστεί εικόνες έως **50 MB** χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη, προσφέροντας χρόνους απόκρισης κάτω του δευτερολέπτου σε τυπικό εξοπλισμό διακομιστή. Η βιβλιοθήκη είναι thread‑safe, απαιτεί μόνο ένα JAR, και προσφέρει ευέλικτες μορφές εξόδου—συμπεριλαμβανομένου του ακατέργαστου κειμένου, HTML, και ακριβών ορθογωνίων περιοχών κειμένου—κάνοντας την ιδανική για σενάρια υψηλής διακίνησης σε επιχειρησιακό επίπεδο.

## Προαπαιτούμενα

- **Java Development Kit** (JDK 11 ή νεότερο) εγκατεστημένο στο σύστημά σας.  
- **Aspose.OCR for Java** βιβλιοθήκη – κατεβάστε την από την επίσημη ιστοσελίδα [εδώ](https://releases.aspose.com/ocr/java/).  
- Ένα IDE ή εργαλείο κατασκευής (Maven/Gradle) για τη διαχείριση της εξάρτησης JAR.

## Εισαγωγή Πακέτων

Στο έργο Java σας, εισάγετε τις απαραίτητες κλάσεις:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AreasType;
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Οδηγός Βήμα‑Βήμα

### Βήμα 1: Ρύθμιση του Έργου Σας
Δημιουργήστε ένα νέο έργο Java (ή προσθέστε σε υπάρχον) και τοποθετήστε το Aspose.OCR JAR στην classpath. Αν χρησιμοποιείτε Maven, προσθέστε την εξάρτηση όπως περιγράφεται στο πακέτο λήψης.

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### Βήμα 2: Ορισμός Καταλόγου Εγγράφου και Διαδρομής Εικόνας
Καθορίστε πού βρίσκεται η δείγμα εικόνα σας:

```java
// Create AsposeOCR instance
AsposeOCR api = new AsposeOCR();
```

### Βήμα 3: Δημιουργία Παράδειγμα AsposeOCR
`AsposeOCR` είναι η κύρια κλάση που παρέχει λειτουργικότητα OCR.

Δημιουργήστε την μηχανή OCR:

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### Βήμα 4: Αναγνώριση Κειμένου στην Εικόνα
Φορτώστε την εικόνα σας και καλέστε `RecognizePage` για να μετατρέψετε την εικόνα σε απλό κείμενο. Αυτή η ενιαία κλήση μεθόδου εκτελεί προεπεξεργασία εικόνας, τμηματοποίηση χαρακτήρων, και γλωσσική αναγνώριση σε ένα βήμα.

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

### Βήμα 5: Λήψη Ορθογωνίων με Περιοχές Κειμένου
Αποκτήστε τα ορθογώνια περιορισμού για κάθε παράγραφο (ή άλλους τύπους περιοχών). Αυτό το βήμα επιστρέφει μια συλλογή αντικειμένων `Rectangle` που περικλείουν ακριβώς τα ανιχνευμένα μπλοκ κειμένου, επιτρέποντάς σας να τα επισημάνετε ή να τα επεξεργαστείτε περαιτέρω.

CODE_BLOCK_PLACEHOLDER_5_END

## Συχνά Προβλήματα & Επίλυση

| Σύμπτωμα | Πιθανή Αιτία | Διόρθωση |
|---------|--------------|-----|
| `IOException` on `RecognizePage` | Λανθασμένη διαδρομή αρχείου ή έλλειψη δικαιώματος ανάγνωσης | Επαληθεύστε ότι το `imagePath` δείχνει σε ένα υπάρχον PNG/JPG και ότι η εφαρμογή έχει πρόσβαση στο σύστημα αρχείων. |
| Empty result string | Εικόνα χαμηλής ποιότητας ή μη υποστηριζόμενη γλώσσα | Προεπεξεργαστείτε την εικόνα (αυξήστε την αντίθεση, δυαδικοποιήστε) ή καθορίστε τη σωστή γλώσσα χρησιμοποιώντας `api.setLanguage("eng")`. |
| No rectangles returned | Χρήση λανθασμένου `AreasType` (π.χ., `WORDS` όταν αναμένονται παράγραφοι) | Αλλάξτε σε `AreasType.PARAGRAPHS` ή `AreasType.LINES` ανάλογα. |

## Συχνές Ερωτήσεις

**Q: Είναι το Aspose.OCR συμβατό με Java 11;**  
A: Ναι, το Aspose.OCR λειτουργεί με Java 11 και μεταγενέστερες εκδόσεις.

**Q: Μπορώ να χρησιμοποιήσω το Aspose.OCR για προσωπικά και εμπορικά έργα;**  
A: Ναι, μπορείτε να το χρησιμοποιήσετε σε οποιοδήποτε τύπο έργου. Για λεπτομέρειες αδειοδότησης, επισκεφθείτε [εδώ](https://purchase.aspose.com/buy).

**Q: Πώς μπορώ να αποκτήσω προσωρινή άδεια για αξιολόγηση;**  
A: Μπορείτε να αποκτήσετε μια προσωρινή άδεια [εδώ](https://purchase.aspose.com/temporary-license/).

**Q: Πού μπορώ να βρω υποστήριξη από την κοινότητα ή επίσημη βοήθεια;**  
A: Για υποστήριξη και συζητήσεις, επισκεφθείτε το [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16).

**Q: Υποστηρίζει το Aspose.OCR πολυνηματικότητα;**  
A: Ναι, η βιβλιοθήκη είναι thread‑safe και μπορεί να χρησιμοποιηθεί σε ταυτόχρονες περιβάλλοντα για καλύτερη απόδοση.

## Συμπέρασμα

Σε αυτό το **aspose ocr java tutorial** μάθατε πώς να **μετατρέψετε εικόνα σε κείμενο** χρησιμοποιώντας το Aspose.OCR for Java, να εξάγετε παραγράφους, και να λάβετε τα ακριβή ορθογώνια που περιβάλλουν κάθε μπλοκ κειμένου. Αυτές οι δυνατότητες σας επιτρέπουν να δημιουργήσετε αναζητήσιμα PDF, να επισημάνετε κείμενο σε UI overlays, ή να τροφοδοτήσετε δομημένα δεδομένα σε επόμενες διαδικασίες. Εξερευνήστε περαιτέρω το API για προσαρμογή ρυθμίσεων γλώσσας, διαχείριση διαφορετικών μορφών εικόνας, ή ενσωμάτωση με αποθήκευση στο σύννεφο.

---

**Τελευταία Ενημέρωση:** 2026-06-19  
**Δοκιμάστηκε Με:** Aspose.OCR 23.10 for Java  
**Συγγραφέας:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Σχετικά Μαθήματα

- [Εξαγωγή Κειμένου από Εικόνες – Βασικά OCR με Aspose.OCR για Java](/ocr/java/ocr-basics/)
- [Εξαγωγή Κειμένου από Εικόνα Java με Aspose.OCR Λειτουργία Ανίχνευσης Περιοχών](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Μετατροπή Εικόνας σε Κείμενο σε Java χρησιμοποιώντας Aspose.OCR BufferedImage](/ocr/java/advanced-ocr-techniques/perform-ocr-buffered-image/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}