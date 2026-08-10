---
date: 2026-06-24
description: Μάθετε ένα ολοκληρωμένο παράδειγμα Aspose OCR Java για την εξαγωγή κειμένου
  εικόνας Java από φωτογραφίες. Υψηλής ακρίβειας ενσωμάτωση OCR για εφαρμογές Java.
keywords:
- aspose ocr java example
- recognize lines in image
- extract image text java
linktitle: Aspose OCR Java Example – Αναγνώριση Γραμμών σε Εικόνες
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Learn a comprehensive Aspose OCR Java example to extract image text
    java from pictures. High‑accuracy OCR integration for Java applications.
  headline: Aspose OCR Java Example – Recognizing Lines in Images
  type: TechArticle
- description: Learn a comprehensive Aspose OCR Java example to extract image text
    java from pictures. High‑accuracy OCR integration for Java applications.
  name: Aspose OCR Java Example – Recognizing Lines in Images
  steps:
  - name: Import Packages
    text: '`OcrEngine` is the primary class in Aspose.OCR that performs text extraction
      from images. First, import the required Aspose.OCR classes and standard Java
      utilities.'
  - name: Set Document Directory
    text: '`OcrEngine` works with a base directory that simplifies file handling.
      Define the folder that holds your image files. Replace `"Your Document Directory"`
      with the absolute path where your test image resides.'
  - name: Set Image Path
    text: '`OcrEngine` needs a concrete file path to load the target image. Point
      the OCR engine to the specific image you want to process. Feel free to change
      the file name to match your own image.'
  - name: Create API Instance
    text: '`OcrEngine` is instantiated to expose the recognition methods. Instantiate
      the main OCR class – this object will expose the recognition methods.'
  - name: Configure Recognition Settings
    text: '`OcrEngineSettings` lets you fine‑tune how the engine interprets the image.
      Tell Aspose.OCR what you expect. In this example we enable **single‑line** recognition.
      If you need to detect multiple lines, set `settings.setRecognizeSingleLine(false)`
      instead.'
  - name: Perform OCR Recognition
    text: '`OcrResult` holds the text that the engine extracts after processing. Run
      the OCR engine and print the recognised line to the console. When you execute
      the program, you should see the file path followed by the extracted line of
      text.'
  type: HowTo
- questions:
  - answer: Yes. Set `settings.setRecognizeSingleLine(false)` to enable multi‑line
      detection.
    question: Can Aspose.OCR recognize multiple lines in an image?
  - answer: JPEG, PNG, TIFF, BMP, GIF, WebP, and several others—over 12 formats in
      total.
    question: Which image formats are supported?
  - answer: Aspose.OCR delivers >98 % accuracy on standard benchmarks when images
      are clear and properly oriented.
    question: How accurate is the text extraction?
  - answer: Absolutely. The same Java code works on server‑side frameworks such as
      Spring Boot, Tomcat, or any servlet container.
    question: Can I use this library in a web application?
  - answer: Yes. Download a free trial from the Aspose website [here](https://releases.aspose.com/).
      The trial includes all features but adds a small watermark to the output.
    question: Is a trial version available?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Aspose OCR Java Example – Αναγνώριση Γραμμών σε Εικόνες
url: /el/java/advanced-ocr-techniques/recognize-lines/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR Java Example – Αναγνώριση Γραμμών σε Εικόνες

## Γρήγορες Απαντήσεις
- **Τι κάνει το παράδειγμα;** Αναγνωρίζει μια μόνο γραμμή κειμένου σε μια παρεχόμενη εικόνα.  
- **Ποια βιβλιοθήκη απαιτείται;** Aspose.OCR for Java (τελευταία έκδοση).  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή λειτουργεί για ανάπτυξη· απαιτείται εμπορική άδεια για παραγωγή.  
- **Μπορώ να εξάγω κείμενο από οποιαδήποτε μορφή εικόνας;** Ναι – υποστηρίζονται JPEG, PNG, TIFF, BMP και άλλα.  
- **Πόσο χρόνο παίρνει η υλοποίηση;** Περίπου 10‑15 λεπτά για αντιγραφή, προσαρμογή της διαδρομής και εκτέλεση.

## Τι είναι ένα Aspose OCR Java Example;
Ένα σύντομο, εκτελέσιμο απόσπασμα που δείχνει πώς να καλέσετε το Aspose.OCR API από Java, να διαμορφώσετε τις επιλογές αναγνώρισης και να ανακτήσετε τη αναγνωρισμένη γραμμή κειμένου. Αυτό το παράδειγμα σας παρέχει μια σταθερή βάση που μπορείτε να προσαρμόσετε για μαζική επεξεργασία τιμολογίων, αποδείξεων ή οποιασδήποτε εικόνας με φόρμα όπου απαιτείται μια μόνο γραμμή κειμένου.

## Γιατί να Χρησιμοποιήσετε το Aspose OCR για Java για την εξαγωγή κειμένου από εικόνα java;
Το Aspose OCR παρέχει **>98 % ακρίβεια σε επίπεδο χαρακτήρα** σε καθαρές, υψηλής ανάλυσης σαρώσεις και υποστηρίζει **12+ μορφές εικόνας** (συμπεριλαμβανομένων JPEG, PNG, TIFF, BMP, GIF, WebP και άλλα). Το API είναι ελαφρύ, δεν απαιτεί εγγενείς εξαρτήσεις και μπορεί να εκτελεστεί σε οποιαδήποτε πλατφόρμα συμβατή με Java—από εφαρμογές επιφάνειας εργασίας μέχρι μικρο‑υπηρεσίες βασισμένες στο cloud.

## Προαπαιτούμενα
Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

1. **Java Development Kit (JDK)** – έκδοση 8 ή νεότερη εγκατεστημένη και ρυθμισμένη στο PATH σας.  
2. **Aspose.OCR for Java library** – κατεβάστε το τελευταίο JAR από την επίσημη σελίδα [here](https://releases.aspose.com/ocr/java/).  
3. **Ένα αρχείο εικόνας** που περιέχει το κείμενο που θέλετε να αναγνωρίσετε. Ενημερώστε τη μεταβλητή `imagePath` στον κώδικα ώστε να δείχνει σε αυτό το αρχείο.

## Οδηγός Βήμα‑Βήμα

### Βήμα 1: Εισαγωγή Πακέτων
`OcrEngine` είναι η κύρια κλάση στο Aspose.OCR που εκτελεί εξαγωγή κειμένου από εικόνες.  
Πρώτα, εισάγετε τις απαιτούμενες κλάσεις Aspose.OCR και τις τυπικές βοηθητικές κλάσεις Java.

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;
```

### Βήμα 2: Ορισμός Καταλόγου Εγγράφου
`OcrEngine` λειτουργεί με έναν βασικό κατάλογο που απλοποιεί τη διαχείριση αρχείων.  
Ορίστε το φάκελο που περιέχει τα αρχεία εικόνας σας.

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

Αντικαταστήστε το `"Your Document Directory"` με την απόλυτη διαδρομή όπου βρίσκεται η δοκιμαστική σας εικόνα.

### Βήμα 3: Ορισμός Διαδρομής Εικόνας
`OcrEngine` χρειάζεται μια συγκεκριμένη διαδρομή αρχείου για να φορτώσει την εικόνα-στόχο.  
Κατευθύνετε τη μηχανή OCR στην συγκεκριμένη εικόνα που θέλετε να επεξεργαστείτε.

```java
// The image path
String imagePath = dataDir + "0001460985.Jpeg";
```

Μπορείτε να αλλάξετε το όνομα του αρχείου ώστε να ταιριάζει με τη δική σας εικόνα.

### Βήμα 4: Δημιουργία Αντικειμένου API
`OcrEngine` δημιουργείται για να εκθέσει τις μεθόδους αναγνώρισης.  
Δημιουργήστε την κύρια κλάση OCR – αυτό το αντικείμενο θα εκθέτει τις μεθόδους αναγνώρισης.

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

### Βήμα 5: Διαμόρφωση Ρυθμίσεων Αναγνώρισης
`OcrEngineSettings` σας επιτρέπει να ρυθμίσετε λεπτομερώς πώς η μηχανή ερμηνεύει την εικόνα.  
Πείτε στο Aspose.OCR τι περιμένετε. Σε αυτό το παράδειγμα ενεργοποιούμε την αναγνώριση **single‑line**.

```java
RecognitionSettings settings = new RecognitionSettings();
settings.setRecognizeSingleLine(true);
```

Αν χρειάζεστε ανίχνευση πολλαπλών γραμμών, ορίστε `settings.setRecognizeSingleLine(false)` αντί αυτού.

### Βήμα 6: Εκτέλεση Αναγνώρισης OCR
`OcrResult` περιέχει το κείμενο που εξάγει η μηχανή μετά την επεξεργασία.  
Εκτελέστε τη μηχανή OCR και εκτυπώστε τη αναγνωρισμένη γραμμή στην κονσόλα.

```java
RecognitionResult result = api.RecognizePage(imagePath, settings);
System.out.println("File: " + imagePath);
System.out.println("Result line: " + result.recognitionText);
```

Όταν εκτελέσετε το πρόγραμμα, θα πρέπει να δείτε τη διαδρομή του αρχείου ακολουθούμενη από την εξαγόμενη γραμμή κειμένου.

## Γιατί Είναι Σημαντικό
Χρησιμοποιώντας αυτό το **aspose ocr java example** για την εξαγωγή κειμένου από εικόνα java, αποκτάτε έναν γρήγορο, αξιόπιστο τρόπο να μετατρέψετε σαρωμένα έγγραφα, στιγμιότυπα οθόνης ή φωτογραφημένες αποδείξεις σε αναζητήσιμο, επεξεργάσιμο κείμενο. Η λειτουργία μονής γραμμής είναι ιδανική για επεξεργασία φορμών, ετικετών barcode ή οποιαδήποτε κατάσταση όπου χρειάζεστε μόνο μία γραμμή κειμένου ανά εικόνα.

## Συχνά Προβλήματα και Λύσεις
| Πρόβλημα | Λύση |
|----------|------|
| **`java.lang.NoClassDefFoundError`** | Βεβαιωθείτε ότι το JAR του Aspose.OCR έχει προστεθεί στο classpath του έργου σας. |
| **Κενό αποτέλεσμα** | Επαληθεύστε ότι η εικόνα περιέχει μια καθαρή, οριζόντια γραμμή κειμένου και ότι το `setRecognizeSingleLine(true)` ταιριάζει με το σενάριό σας. |
| **Μη υποστηριζόμενη μορφή εικόνας** | Μετατρέψτε την εικόνα σε μια υποστηριζόμενη μορφή (π.χ., JPEG ή PNG) πριν την επεξεργασία. |
| **Καθυστέρηση απόδοσης σε μεγάλες εικόνες** | Αλλάξτε το μέγεθος ή συμπιέστε την εικόνα σε λογική ανάλυση (≤ 1500 px πλάτος) πριν το OCR. |

## Συχνές Ερωτήσεις

**Ε: Μπορεί το Aspose.OCR να αναγνωρίσει πολλαπλές γραμμές σε μια εικόνα;**  
Α: Ναι. Ορίστε `settings.setRecognizeSingleLine(false)` για ενεργοποίηση της ανίχνευσης πολλαπλών γραμμών.

**Ε: Ποιες μορφές εικόνας υποστηρίζονται;**  
Α: JPEG, PNG, TIFF, BMP, GIF, WebP και αρκετές άλλες—πάνω από 12 μορφές συνολικά.

**Ε: Πόσο ακριβής είναι η εξαγωγή κειμένου;**  
Α: Το Aspose.OCR παρέχει >98 % ακρίβεια σε τυπικά benchmarks όταν οι εικόνες είναι καθαρές και σωστά προσανατολισμένες.

**Ε: Μπορώ να χρησιμοποιήσω αυτή τη βιβλιοθήκη σε μια web εφαρμογή;**  
Α: Απόλυτα. Ο ίδιος κώδικας Java λειτουργεί σε πλαίσια διακομιστή όπως Spring Boot, Tomcat ή οποιονδήποτε servlet container.

**Ε: Διατίθεται δοκιμαστική έκδοση;**  
Α: Ναι. Κατεβάστε μια δωρεάν δοκιμή από την ιστοσελίδα Aspose [here](https://releases.aspose.com/). Η δοκιμή περιλαμβάνει όλες τις λειτουργίες αλλά προσθέτει ένα μικρό υδατογράφημα στο αποτέλεσμα.

**Τελευταία Ενημέρωση:** 2026-06-24  
**Δοκιμή Με:** Aspose.OCR for Java 24.11 (τελευταία τη στιγμή της συγγραφής)  
**Συγγραφέας:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Σχετικά Μαθήματα

- [Εξαγωγή Κειμένου από Εικόνα Java με Aspose.OCR Detect Areas Mode](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Εξαγωγή Κειμένου από Εικόνες Χρησιμοποιώντας Aspose.OCR – Επιτρεπόμενοι Χαρακτήρες](/ocr/java/advanced-ocr-techniques/specify-allowed-characters/)
- [Μετατροπή Εικόνας σε Κείμενο σε Java χρησιμοποιώντας Aspose.OCR BufferedImage](/ocr/java/advanced-ocr-techniques/perform-ocr-buffered-image/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}