---
date: 2026-07-18
description: Μάθετε πώς να εκτελείτε image to text java χρησιμοποιώντας Aspose.OCR
  για Java. Αυτό το βήμα‑βήμα οδηγό σας δείχνει πώς να εξάγετε κείμενο από εικόνα
  με BufferedImage.
keywords:
- image to text java
- extract text from png
- recognize text from png
- ocr java
- aspose ocr
lastmod: 2026-07-18
linktitle: 'Εξαγωγή κειμένου από εικόνα Java: OCR σε BufferedImage με Aspose.OCR'
og_description: Το image to text java tutorial δείχνει πώς να εξάγετε κείμενο από
  εικόνες χρησιμοποιώντας Aspose.OCR σε Java. Ακολουθήστε τον βήμα‑βήμα οδηγό για
  BufferedImage OCR.
og_image_alt: 'Guide: Convert Image to Text in Java using Aspose.OCR BufferedImage'
og_title: image to text java – Μετατροπή εικόνας σε κείμενο με Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-07-18'
  description: Learn how to perform image to text java using Aspose.OCR for Java.
    This step‑by‑step tutorial shows you how to extract text from image with a BufferedImage.
  headline: 'image to text java: Convert Image to Text with Aspose.OCR'
  type: TechArticle
- description: Learn how to perform image to text java using Aspose.OCR for Java.
    This step‑by‑step tutorial shows you how to extract text from image with a BufferedImage.
  name: 'image to text java: Convert Image to Text with Aspose.OCR'
  steps:
  - name: Define the document directory and image path
    text: Set the folder that contains your source images. This is the location the
      **image to text java** routine will read from.
  - name: Create an AsposeOCR instance
    text: '`AsposeOCR` is the core class that drives all OCR operations. It encapsulates
      language models, preprocessing options, and the `RecognizePage` method.'
  - name: Load the image and recognize text
    text: The `BufferedImage` class represents an image in memory. Load your file,
      then hand it to `api.RecognizePage`. The `RecognizePage` method processes a
      `BufferedImage` and returns the recognized text as a string. > **Pro tip:**
      You can also **recognize text from png** files with the same method; just p
  type: HowTo
- questions:
  - answer: Install the JDK, add the Aspose.OCR JAR to your project, and follow the
      three‑step code pattern shown above.
    question: What is the easiest way to start a **java ocr tutorial**?
  - answer: Yes. Loop over files in a directory, reuse the same `AsposeOCR` instance,
      and collect each result.
    question: Can I use this approach to **process scanned documents** in bulk?
  - answer: English is the default, but you can explicitly set it with `api.setLanguage(Language.English)`
      for clarity.
    question: Do I need to set a language for English text?
  - answer: The engine is lightweight; typical images (<2 MB) are processed in under
      a second. For high‑throughput scenarios, consider image pre‑scaling or multi‑threading.
    question: Is there any performance impact when running on a server?
  - answer: Load your license file with `License license = new License(); license.setLicense("Aspose.OCR.lic");`
      before creating the `AsposeOCR` instance.
    question: How do I handle licensing in production?
  type: FAQPage
second_title: Aspose.OCR Java API
tags:
- image to text
- Aspose.OCR
- Java OCR
- BufferedImage processing
- OCR tutorial
title: 'image to text java: Μετατροπή εικόνας σε κείμενο με Aspose.OCR'
url: /el/java/advanced-ocr-techniques/perform-ocr-buffered-image/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή Εικόνας σε Κείμενο σε Java: OCR σε BufferedImage με Aspose.OCR

## Εισαγωγή

Σε αυτό το **Aspose OCR Java tutorial** θα ανακαλύψετε πώς να **μετατρέψετε εικόνα σε κείμενο** χρησιμοποιώντας τη δυναμική βιβλιοθήκη Aspose.OCR. **Αυτός ο οδηγός σας καθοδηγεί μέσω του image to text java** με την υποστήριξη BufferedImage του Aspose.OCR, είτε χρειάζεται να επεξεργαστείτε σαρωμένα έγγραφα, να διαβάσετε αποδείξεις ή να εξάγετε κείμενο από στιγμιότυπα οθόνης. Θα αποκτήσετε μια σαφή εικόνα της απαιτούμενης ρύθμισης, των ακριβών εισαγωγών και του ελάχιστου κώδικα που χρειάζεστε για να ξεκινήσετε την άμεση εξαγωγή κειμένου.

## Γρήγορες Απαντήσεις
- **Ποια βιβλιοθήκη είναι η καλύτερη για Java OCR;** Aspose.OCR for Java.  
- **Μπορώ να επεξεργαστώ ένα BufferedImage απευθείας;** Yes – the `RecognizePage` method accepts `BufferedImage`.  
- **Χρειάζομαι άδεια για δοκιμές;** A free trial works for development; a license is required for production.  
- **Ποιοι τύποι εικόνας υποστηρίζονται;** PNG, JPEG, BMP, TIFF, and more.  
- **Πόσο χρόνο χρειάζεται μια τυπική εικόνα για επεξεργασία;** Usually under a second for standard‑size images.

## Τι είναι το image to text java;

Το image to text java είναι η διαδικασία χρήσης κώδικα Java για την ανάγνωση ενός αρχείου εικόνας και την έξοδο των χαρακτήρων που περιέχει. Η Οπτική Αναγνώριση Χαρακτήρων (OCR) αναλύει οπτικά μοτίβα και τα μετατρέπει σε επεξεργάσιμο κείμενο, επιτρέποντας αυτοματοποιημένη εισαγωγή δεδομένων, αρχεία αναζήτησης και ροές εργασίας με AI χωρίς χειροκίνητη μεταγραφή.

## Γιατί να επιλέξετε το Aspose.OCR για Java;

Το Aspose.OCR προσφέρει ακρίβεια κορυφαίας βιομηχανίας ενώ διατηρεί το API απλό και γρήγορο. Υποστηρίζει δεκάδες γλώσσες, διαχειρίζεται σύνθετες διατάξεις και μπορεί να ενσωματωθεί με ελάχιστες εξαρτήσεις, καθιστώντας το ιδανικό τόσο για μικρά βοηθήματα όσο και για λύσεις μεγάλων επιχειρήσεων.  

- **Υψηλή ακρίβεια** σε 70+ γλώσσες και 150+ γραμματοσειρές.  
- **Απλό API** – μια γραμμή κώδικα μπορεί να αναγνωρίσει ολόκληρη τη σελίδα.  
- **Χωρίς εξωτερικές εξαρτήσεις** – λειτουργεί απευθείας με `BufferedImage`.  
- **Ποσοτικοποιημένη απόδοση** – επεξεργάζεται ένα PNG 1 MB σε ~0.8 δευτερόλεπτα σε τυπική CPU 2.8 GHz, και μπορεί να διαχειριστεί πολυ‑σελίδες TIFF χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη.  

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τα εξής:

1. **Java Development Kit (JDK)** – έκδοση 8 ή νεότερη. Κατεβάστε το από [Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.OCR for Java** – αποκτήστε το τελευταίο JAR από την ιστοσελίδα Aspose [εδώ](https://releases.aspose.com/ocr/java/).  
3. **Φάκελος με εικόνες** – δημιουργήστε έναν κατάλογο στο μηχάνημά σας και τοποθετήστε τις εικόνες που θέλετε να επεξεργαστείτε. Ενημερώστε τη μεταβλητή `dataDir` στον κώδικα ώστε να δείχνει σε αυτόν το φάκελο.

## Εισαγωγή Πακέτων

Ξεκινήστε εισάγοντας τις απαραίτητες κλάσεις. Η κλάση `AsposeOCR` παρέχει τη μηχανή OCR, ενώ `ImageIO` και `BufferedImage` διαχειρίζονται τη φόρτωση εικόνας.

`import com.aspose.ocr.AsposeOCR;`  
`import com.aspose.ocr.Language;`  
`import javax.imageio.ImageIO;`  
`import java.awt.image.BufferedImage;`  
`import java.io.File;`

`BufferedImage` αντιπροσωπεύει μια εικόνα στη μνήμη και είναι ο κύριος τύπος εισόδου για τη μηχανή OCR.

## Πώς να **Μετατρέψετε Εικόνα σε Κείμενο** σε Java – Οδηγός Βήμα‑βήμα

### Βήμα 1: Ορίστε τον φάκελο εγγράφου και τη διαδρομή εικόνας  

Ορίστε το φάκελο που περιέχει τις πηγαίες εικόνες σας. Αυτή είναι η θέση από την οποία η ρουτίνα **image to text java** θα διαβάσει.

```text
String dataDir = "C:/OCRImages/";   // change to your actual path
String imagePath = dataDir + "sample.png";
```

### Βήμα 2: Δημιουργήστε μια παρουσία AsposeOCR  

`AsposeOCR` είναι η βασική κλάση που διευθύνει όλες τις λειτουργίες OCR. Περιλαμβάνει μοντέλα γλώσσας, επιλογές προεπεξεργασίας και τη μέθοδο `RecognizePage`.

```text
AsposeOCR api = new AsposeOCR();
```

### Βήμα 3: Φορτώστε την εικόνα και αναγνωρίστε το κείμενο  

Η κλάση `BufferedImage` αντιπροσωπεύει μια εικόνα στη μνήμη. Φορτώστε το αρχείο σας, στη συνέχεια δώστε το στο `api.RecognizePage`. Η μέθοδος `RecognizePage` επεξεργάζεται ένα `BufferedImage` και επιστρέφει το αναγνωρισμένο κείμενο ως συμβολοσειρά.

```text
BufferedImage loaded = ImageIO.read(new File(imagePath));
String result = api.RecognizePage(loaded);
System.out.println("Extracted text: " + result);
```

> **Συμβουλή:** Μπορείτε επίσης να **αναγνωρίσετε κείμενο από αρχεία png** με την ίδια μέθοδο· απλώς ορίστε το `imagePath` σε μια εικόνα PNG.

Επαναλάβετε τα τρία βήματα για κάθε εικόνα που χρειάζεται να επεξεργαστείτε, απλώς προσαρμόζοντας το `imagePath`.

## Πώς λειτουργεί η κλάση AsposeOCR;

`AsposeOCR` είναι η κύρια μηχανή του Aspose.OCR που εκτελεί διαχωρισμό χαρακτήρων, ανίχνευση γλώσσας και εξαγωγή κειμένου. Μόλις δημιουργηθεί, μπορείτε προαιρετικά να ορίσετε τη γλώσσα (`api.setLanguage(Language.English)`) και να ρυθμίσετε τις ρυθμίσεις αναγνώρισης πριν καλέσετε το `RecognizePage`.

## Πώς φορτώνω μια εικόνα για OCR;

Φορτώστε την εικόνα σε ένα `BufferedImage` χρησιμοποιώντας το `ImageIO.read(File)`. Αυτή η μέθοδος υποστηρίζει μορφές PNG, JPEG, BMP, TIFF και GIF, επιστρέφοντας μια πλήρως αποκωδικοποιημένη εικόνα έτοιμη για αναγνώριση χωρίς επιπλέον βιβλιοθήκες. Μετά τη φόρτωση, μπορείτε να περάσετε το `BufferedImage` απευθείας στη μηχανή OCR για άμεση επεξεργασία.

## Κοινές Περιπτώσεις Χρήσης

- **Επεξεργασία τιμολογίων:** Εξαγωγή λεπτομερειών γραμμής από σαρωμένα PDF ή αποδείξεις PNG.  
- **Αρχειοθέτηση εγγράφων:** Μετατρέψτε σαρωμένες συμβάσεις σε αναζητήσιμο κείμενο για γρήγορη ανάκτηση.  
- **Bots αυτοματοποίησης:** Εξάγετε κείμενο από στιγμιότυπα οθόνης ιστοσελίδων ή εφαρμογών επιφάνειας εργασίας.

## Κοινά Προβλήματα & Επίλυση

| Σύμπτωμα | Πιθανή Αιτία | Διόρθωση |
|----------|--------------|----------|
| `null` έξοδος | Το αρχείο εικόνας δεν βρέθηκε ή δεν είναι αναγνώσιμο | Επαληθεύστε το `dataDir` και το όνομα αρχείου· βεβαιωθείτε ότι η εικόνα είναι σε υποστηριζόμενη μορφή |
| Ασυνεπές κείμενο | Λανθασμένες ρυθμίσεις γλώσσας | Χρησιμοποιήστε `api.setLanguage(Language.<desired>)` πριν το `RecognizePage` |
| Αργή απόδοση σε μεγάλες εικόνες | Η ανάλυση της εικόνας είναι πολύ υψηλή | Αλλάξτε το μέγεθος της εικόνας ή περάστε ένα κλιμακωμένο `BufferedImage` στο API |

## Συχνές Ερωτήσεις (Πρόσθετες)

**Q1: Μπορεί το Aspose.OCR να χειριστεί πολλαπλές γλώσσες;**  
A: Ναι – υποστηρίζει 70+ γλώσσες από την αρχή. Ορίστε τη γλώσσα-στόχο με `api.setLanguage(Language.English)` (ή οποιαδήποτε άλλη υποστηριζόμενη γλώσσα).

**Q2: Είναι το Aspose.OCR συμβατό με διαφορετικές μορφές εικόνας;**  
A: Απόλυτα. PNG, JPEG, BMP, TIFF, and GIF are all supported.

**Q3: Πόσο συχνά ενημερώνεται το Aspose.OCR;**  
A: Το Aspose κυκλοφορεί τακτικές ενημερώσεις. Ελέγξτε τις τελευταίες σημειώσεις έκδοσης στη [documentation page](https://reference.aspose.com/ocr/java/).

**Q4: Μπορώ να δοκιμάσω το Aspose.OCR πριν την αγορά;**  
A: Ναι – μια δωρεάν δοκιμή είναι διαθέσιμη [εδώ](https://releases.aspose.com/).

**Q5: Πού μπορώ να βρω υποστήριξη κοινότητας για το Aspose.OCR;**  
A: Συμμετέχετε στη συζήτηση στο [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16).

## FAQ – Γρήγορη Αναφορά για το Java OCR Tutorial

**Q: Ποιος είναι ο πιο εύκολος τρόπος για να ξεκινήσετε ένα **java ocr tutorial**;**  
A: Εγκαταστήστε το JDK, προσθέστε το Aspose.OCR JAR στο έργο σας και ακολουθήστε το τρι‑βήμα μοτίβο κώδικα που φαίνεται παραπάνω.

**Q: Μπορώ να χρησιμοποιήσω αυτήν την προσέγγιση για **process scanned documents** μαζικά;**  
A: Ναι. Επανάληψη πάνω στα αρχεία σε έναν φάκελο, επαναχρησιμοποίηση της ίδιας παρουσίας `AsposeOCR`, και συλλογή κάθε αποτελέσματος.

**Q: Χρειάζεται να ορίσω γλώσσα για αγγλικό κείμενο;**  
A: Η αγγλική είναι η προεπιλογή, αλλά μπορείτε ρητά να την ορίσετε με `api.setLanguage(Language.English)` για σαφήνεια.

**Q: Υπάρχει κάποιος αντίκτυπος στην απόδοση όταν τρέχει σε διακομιστή;**  
A: Η μηχανή είναι ελαφριά· τυπικές εικόνες (<2 MB) επεξεργάζονται κάτω από ένα δευτερόλεπτο. Για σενάρια υψηλής απόδοσης, εξετάστε την προ‑κλιμάκωση εικόνας ή το multi‑threading.

**Q: Πώς διαχειρίζομαι την άδεια σε παραγωγή;**  
A: Φορτώστε το αρχείο άδειας με `License license = new License(); license.setLicense("Aspose.OCR.lic");` πριν δημιουργήσετε την παρουσία `AsposeOCR`.

**Τελευταία Ενημέρωση:** 2026-07-18  
**Δοκιμάστηκε Με:** Aspose.OCR for Java 24.11 (latest at time of writing)  
**Συγγραφέας:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Σχετικά Μαθήματα

- [Εξαγωγή Κειμένου από Εικόνες – Βασικά OCR με Aspose.OCR για Java](/ocr/java/ocr-basics/)
- [Εξαγωγή Κειμένου από Εικόνα Java με Aspose.OCR Detect Areas Mode](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Πώς να OCR Κείμενο Εικόνας με Γλώσσα Χρησιμοποιώντας Aspose.OCR](/ocr/java/ocr-operations/perform-ocr-language-selection/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;
```

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

```java
// Recognize page from BufferedImage
try {
    BufferedImage loaded = ImageIO.read(new File(imagePath));
    String result = api.RecognizePage(loaded);
    System.out.println("Result BufferedImage: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```